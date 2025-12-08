---
title: "Wicked Saints Studios Integrates TikTok Within World Reborn Using AWS"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 3.6. </b> "
---

{{% notice warning %}}
 **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# WICKED SAINTS STUDIOS INTEGRATES TIKTOK WITHIN WORLD REBORN USING AWS

**Original Article:** [Wicked Saints Studios integrates TikTok within World Reborn using AWS](https://aws.amazon.com/vi/blogs/gametech/wicked-saints-studios-integrates-tiktok-within-world-reborn-using-aws/)

**Original Author:** Matthew Nimmo

**Publication Date:** 11 NOV 2025

---

Faced with integrating TikTok functionality into their new mobile game, World Reborn, Wicked Saints Studios encountered a dilemma. Available market solutions were either prohibitively expensive, time-consuming to implement, or lacked TikTok integration entirely. To meet their pressing deadline, while maintaining cost efficiency, the studio developed a creative solution by building upon existing Amazon Web Services (AWS) guidance.

---

## THE GAMING INDUSTRY'S TIKTOK INTEGRATION LANDSCAPE

TikTok has revolutionized gaming content sharing through its short-form format. Marketing strategies are now emphasizing authentic, behind-the-scenes content, which resonates with the style of TikTok. So, studios are implementing direct Share to TikTok functionality for achievements and victories.

---

## WICKED SAINTS IMPLEMENTATION

Wicked Saints, established in 2021 as a start-up mobile gaming company, is gearing up for their full launch of World Reborn next year. Recently they have utilized the [Guidance for Custom Game Backend Hosting on AWS](https://aws.amazon.com/solutions/guidance/custom-game-backend-hosting-on-aws/) to kickstart their backend solution for user authentication. The solution provides a battle-tested, ready-to-go, framework that seamlessly integrated into their existing backend infrastructure.

Guidance for Custom Game Backend Hosting on AWS provides a comprehensive framework for building scalable game backends. It offers expertise in player management, authentication, global deployment, and live service operations. The solution emphasizes building systems that can handle everything from casual mobile games to massive multiplayer experiences. It focuses on player management, scalable architecture, and global reach. Wicked Saints extended this solution to include a TikTok integration.

---

## CHALLENGES FACED DURING THE INTEGRATION

Wicked Saints encountered several challenges during the TikTok integration process:

1. **Deep link encoding and state size limits:** The team had to keep the state minimal and signed to work within TikTok constraints.
2. **Redirect allowlist mismatches:** Ensuring synchronization between TikTok app settings and runtime hostnames required careful configuration.
3. **Extended approval times:** Obtaining production API access from TikTok involved a lengthy approval process.
4. **User experience optimization:** Maintaining a clean and seamless user experience, while adhering to TikTok guidelines proved challenging.

---

## ARCHITECTURE OVERVIEW

![The image is that of an architecture drawing that details out Wicked Saint Studios architecture used within AWS to implement their TikTok integration. The following copy in the blog body describes the architecture and its uses for Wicked Saints Studios.](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/06/WS-Image-1.png)

**Figure 1:** High-level architecture.

Wicked Saints high-level architecture walkthrough:

- Players connect through [Amazon Route 53](https://aws.amazon.com/route53/), which passes through [Amazon CloudFront](https://aws.amazon.com/cloudfront/) and to [Amazon API Gateway](https://aws.amazon.com/api-gateway/).
- To protect against malicious attacks [AWS WAF](https://aws.amazon.com/waf/) is used to protect the API Gateway.
- From there players can refresh access tokens, login with Google, and now login with TikTok through [AWS Lambda](https://aws.amazon.com/lambda/).
- All secrets (for example: TikTok app credentials) are stored within [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) and all meta data associated with login purposes are stored within [Amazon DocumentDB](https://aws.amazon.com/documentdb/).
- [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) hosts any of the game content that is static in nature, such as art assets.

---

## MAPPING AWS FRAMEWORK TO TIKTOK PROVIDER

Wicked Saints started from the Google Play sample flow provided in the Guidance for Custom Game Backend Hosting on AWS and mirrored the pattern. Token exchange within the backend was needed for security reasons from TikTok, as they use OAuth so users can properly be authenticated with TikTok.

While the other login options already had off-the-shelf means, Wicked Saints had to create their own custom login pattern for TikTok using HTTP that mirrored the existing examples within the AWS guidance. As part of this token exchange Wicked Saints needed to keep things secure by encrypting the token. This encrypted token is stored within Secrets Manager, and the encrypted key is held within Amazon DocumentDB.

All uses cases expressed by the existing login features offered by the standard solution guidance is mirror with this newly mapped TikTok extension. These scenarios include link to an existing account, login to existing account, and create a new account and link to the provider.

---

## OAUTH FLOW IMPLEMENTATION

All following code sections describe how Wicked Saints made their TikTok integration possible. The code isn't intended to be prescriptive, but to be adapted to create TikTok integration with your own mobile games.

The first section of code illustrates how Wicked Saints built out the token exchange. First there is a server endpoint \GET /tiktok/login?redirectUrl={redirectUrl}\ that is called by the client. The \PlayerId\ and \IsLinking\ are something Wicked Saints put in place to track if there is an existing user or not that is logging in through TikTok.

This is not a requirement with TikTok, but instead a way to see if the user calling the TikTok login endpoint is already logged in on World Reborn. If that is the case, the solution links their player account to their TikTok account. Wicked Saints receives the user id from the user claims, if they exist. The player only exists if the user is already logged into the game.

\\\csharp
public IActionResult Login([FromQuery] string redirectUrl)
{
    var callbackUrl = \$"{enter your callback url here}";
    var playerId = User.FindFirstValue(ClaimTypes.NameIdentifier);
    var url = tikTokService.RequestAccessToken(callbackUrl, redirectUrl, playerId);
    return Redirect(url);
} 
\\\

When the redirection occurs there is a callback endpoint that is invoked. This endpoint is designed for validation. Wicked Saints validates the state, then re-redirects the client to the \RedirectURL\ with code. See the following example:

\\\csharp
public IActionResult Callback([FromQuery] string code, [FromQuery] string state)
{
    if (string.IsNullOrEmpty(code)) return BadRequest("No code provided");
    if (string.IsNullOrEmpty(state)) return BadRequest("No state provided");
    var oAuthState = AuthorizerService.GetOAuthState(state);
    if (oAuthState == null) return BadRequest("Invalid state provided");
    return Redirect(\$"{oAuthState.RedirectUrl}?code={code}&state={Uri.EscapeDataString(state)}");
} 
\\\

After a successful validation Wicked Saints exchanges the code for tokens. With another server endpoint call \GET /tiktok/exchange?code=...&state=...\ Wicked Saints can retrieve the access_token, refresh_token, and TikTok user ID. From there Wicked Saints proceeds exactly how it is described in the Google Play example provided in the Guidance for Custom Game Backend Hosting on AWS.

\\\csharp
public async Task<IActionResult> Exchange([FromQuery] string code, [FromQuery] string state)
{
    if (string.IsNullOrEmpty(code)) return BadRequest("No code provided");
    if (string.IsNullOrEmpty(state)) return BadRequest("No state provided");
    var oAuthState = AuthorizerService.GetOAuthState(state);
    if (oAuthState == null) return BadRequest("Invalid state provided");
    var callbackUrl = \$"{enter your same callback url here}";
    var accessToken = await tikTokService.GetAccessToken(callbackUrl, code);
    if (accessToken == null) return BadRequest("Failed to get access token from TikTok");
    var tikTokUserId = accessToken.UserId;
    if (string.IsNullOrEmpty(tikTokUserId)) return BadRequest("TikTok user ID missing from token");
    // proceed with same login flow :) 
}
\\\

Then Wicked Saints determines linking based on the following logic:

- If linking is occurring and the player has a JSON Web Token (JWT); attach TikTok user id to that player (this also guards against already linked accounts).
- If a TikTok ID exists already then go to login; if not, then create a new player and link the accounts (game account and TikTok).

Finally, Wicked Saints issues the game JWT.

Wicked Saints also built in some maintenance endpoints. One to refresh or reuse existing tokens. Another is to disconnect or revoke provider tokens and unlink the identity. Lastly, they built an end point that handles direct token hand-off flows.

---

## CLIENT INTEGRATION (UNITY)

To keep in sync with the rest of their endpoints that are REST-based, Wicked Saints implemented a REST-first approach:

- Open the system browser (or in-app web view) to the game backend TikTok Login endpoint.
- TikTok returns to a specified callback URL (TikTok callback endpoint), then the server re-redirects to the app with code and state.
- The client calls the TikTok exchange endpoint passing a code and state to receive the game JWT.

**NOTE:** TikTok requires you to register redirect URIs in the app config; after consent, users are sent back to that URI. Keep your redirects on an allowlist in \TikTok Login Kit\.

In the future Wicked Saints will be extending the AWS Mobile SDK for Unity to support the new TikTok integration. Even though Wicked Saints went with the \est api\ integration route, you could extend the Guidance for Custom Game Backend Hosting on AWS gaming backend with AWS Mobile SDK for Unity to support your new TikTok integration.

For example, you could use something like the following:

\\\csharp
public class AWSGameSDKClient : MonoBehaviour {
    public void LoginWithTikTok(string redirectUrl, bool mobile, Action<LoginRequestData> callback)
        => StartTikTokSignIn(redirectUrl, mobile, callback);

    public void LinkTikTokToCurrentUser(string redirectUrl, bool mobile, Action<LoginRequestData> callback)
    {
        StartTikTokSignIn(redirectUrl, mobile, callback);
    }

    public void StartTikTokSignIn(string redirectUrl, bool mobile, Action<LoginRequestData> callback)
    {
        if (this.loginEndpoint == null) { this.LoginErrorCallback?.Invoke("Login endpoint not defined"); return; }
        this.LoginCallback = callback;
        var url = \$"{this.loginEndpoint}tiktok?redirectUrl={UnityWebRequest.EscapeURL(redirectUrl)}";
        Application.OpenURL(url);
    }

    void OnEnable()
    {
        Application.deepLinkActivated += OnDeepLinkActivated;
        if (!string.IsNullOrEmpty(Application.absoluteURL)) OnDeepLinkActivated(Application.absoluteURL);
    }

    private void OnDeepLinkActivated(string url)
    {
        var uri = new System.Uri(url);
        var q = ParseQuery(uri.Query);
        if (!q.ContainsKey("code") || !q.ContainsKey("state")) return;
        StartCoroutine(this.CallRestApiGetForLogin(
            this.loginEndpoint,
            "tiktok/exchange",
            this.SdkLoginCallback,
            new Dictionary<string,string> { { "code", q["code"] }, { "state", q["state"] } }
        ));
    }
} 
\\\

---

## USING TIKTOK APIS FOR CREATOR WORKFLOWS

After players successfully authenticate through the TikTok Login Kit, Wicked Saints can provide players with a way to share content directly from the game, or companion app, to their TikTok accounts. This integration requires specific permissions and follows established workflows.

### Prerequisites

Before implementing TikTok content publishing, verify the following requirements are met:

**Developer application approval**
- Your TikTok developer application must be reviewed and approved for Content Posting API access
- Submit necessary documentation and use cases to TikTok for review

**User authorization requirements**
- Players must grant specific permissions through OAuth consent
- Required scopes include:
  - \ideo.upload\: For uploading video content
  - \ideo.publish\: For publishing content to TikTok

**Authentication implementation**
- Implement TikTok OAuth v2 authentication flow
- Properly manage and store user access tokens
- Handle token refresh and expiration

### Content publishing workflows

**Option 1: Deferred publishing workflow**

With this workflow players can upload content first and complete the posting process later in TikTok:

- **Initialize upload**
  - Create an upload session with the TikTok API
  - Obtain necessary upload tokens and endpoints
- **Transfer video content**
  - Either upload video data directly through API endpoints
  - Or provide a URL for TikTok to pull content (requires domain verification)
- **User completion**
  - Player receives a TikTok notification
  - They can then edit and complete the post within the TikTok app
  - Provides full access to TikTok native editing features

**Option 2: Direct publishing workflow**

This workflow enables immediate content posting from within your application:

- **Prepare publishing interface**
  - Query \creator_info\ API endpoint
  - Retrieve the user's TikTok profile information
  - Build appropriate publishing interface based on the user's TikTok account type
- **Initialize post**
  - Create new post session
  - Set initial post parameters
  - Prepare content metadata
- **Export and publish**
  - Upload video content
  - Submit post for immediate publication

---

## WHY CHOOSE AWS CUSTOM GAMING BACKEND FOR INTEGRATION

Wicked Saints chose the Guidance for Custom Game Backend Hosting on AWS solution as their starting point for several key reasons:

1. **Flexible by design:** The framework's identity layer is provider-agnostic, allowing the quick addition of TikTok without reshaping the client or backend.
2. **Production-ready scaffolding:** API Gateway with Lambda, token lifecycles, Secrets Manager, CDK stacks, and security guardrails provided proven building blocks.
3. **Scalability:** The serverless, event-driven architecture, with autoscaling data stores, maintained latency budgets during growth.
4. **Built-in observability and governance:** Distributed tracing, structured logs, metrics, and CDK-based tagging and cost allocation streamlined operations across development, staging, and production accounts.
5. **Faster time-to-value:** AWS Quick Starts (which are automated reference architectures that streamline the deployment of key workloads on the AWS Cloud) and sample components allowed rapid setup of a working identity flow, with quick integration of .NET minimal APIs and data models.
6. **Engine-friendly:** Unity samples and clean REST endpoints verify compatibility with existing Unity REST clients, with the option to extend the SDK later for TikTok helpers.
7. **Trusted security:** Leveraging battle-tested patterns from AWS architects reduced the risk in a critical area.
8. **Focus on player experience:** The team could concentrate on creating engaging TikTok-related features rather than building basic authentication infrastructure.
9. **Reduced development time and risk:** Leveraging the framework's extensible nature and proven security patterns accelerated the development process.

---

## SUMMARY

Wicked Saints successfully integrated TikTok into their game by using the Guidance for Custom Game Backend Hosting on AWS. By leveraging this framework and adding to it, they were able to implement a robust, scalable authentication system that seamlessly incorporated the OAuth flow of TikTok. Despite facing challenges, such as deep link encoding limitations and approval processes, the team was able to focus on creating engaging player experiences rather than building authentication infrastructure from scratch.

The AWS solution provided a flexible, production-ready foundation that provided Wicked Saints a way to rapidly deploy their TikTok integration, while maintaining security and scalability. This case study demonstrates how game studios can leverage cloud-based solutions to streamline social media integrations and focus on core gameplay features.

Contact an [AWS Representative](https://aws.amazon.com/contact-us/) to find out how we can help accelerate your business.

---

## FURTHER READING

- [Harmony Games Deploys a Fully Custom Game Backend Utilizing AWS Cloud Development Kit (AWS CDK)](https://aws.amazon.com/blogs/gametech/harmony-games-deploys-a-fully-custom-game-backend-utilizing-aws-cloud-development-kit-aws-cdk/?refid=88cbb1f8-d68e-4966-a75e-e04a1754ebd1)
- [Playable Worlds Scales MMO Gaming with Unity and AWS](https://aws.amazon.com/solutions/case-studies/playable-worlds-unity/)
- [Using latency-based routing with Amazon CloudFront for a multi-Region active-active architecture](https://aws.amazon.com/blogs/networking-and-content-delivery/latency-based-routing-leveraging-amazon-cloudfront-for-a-multi-region-active-active-architecture/)

---

## ABOUT THE AUTHOR

![Matthew Nimmo](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/06/Matthew-Nimmo.png)

**Matthew Nimmo** is a Solutions Architect for Game Tech at AWS. As both a technologist and avid gamer, he helps game studios leverage cloud technology to solve complex challenges and create better player experiences.
