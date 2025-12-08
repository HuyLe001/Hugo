---
title: "Authentication for Mobile Games"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

{{% notice warning %}}
 **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# AUTHENTICATION FOR MOBILE GAMES

**Original Article:** [Authentication for Mobile Games](https://aws.amazon.com/vi/blogs/gametech/authentication-for-mobile-games/)

**Original Author:** Carl Prescott

**Publication Date:** 04 OCT 2023

---

## INTRODUCTION

User authentication and authorization is a critical aspect of almost any application. For mobile games in particular, managing the authentication and authorization of your players can pose some unique challenges. Some of these challenges relate to the use of mobile devices themselves. Other challenges relate to securing the many backend systems a modern mobile game may interact with, such as game servers, social networks, and payment providers.

This blog post looks to identify some of those challenges as well as providing some approaches and good practice when addressing them.

---

## AUTHENTICATION AND AUTHORIZATION

Firstly, a quick word on the difference between authentication and authorization.

**Authentication** (often shortened to AuthN) is the act of confirming a user or system's identity. For example, by logging in with a username and password, scanning a fingerprint, or by using facial recognition.

**Authorization** (or AuthZ) is the process of determining what permissions the user or systems linked to an authenticated identity have and whether actions they perform should be allowed or denied.

---

## MOBILE GAME AUTH CHALLENGES

Some of the common challenges we see with authentication and authorization implementation in mobile games are:

- **Anonymous user support:** Mobile games frequently allow anonymous or unauthenticated players to play without creating an account. Games therefore need to track and control the access of unauthenticated players as well as associate them with an authenticated account if a player later creates an account.

- **Creating simple sign-up processes:** Filling in forms or providing lots of user data via mobile touchscreens can create friction for new players, resulting in them becoming frustrated and abandoning the process entirely.

- **Offline authentication:** Mobile devices may not always have internet connectivity. In this case an approach to local authentication or authorization support needs to be implemented.

- **Caching of credentials:** Care needs to be taken with locally cached credentials to ensure they can not be accessed maliciously without authorization. These credentials could be used to take non-permitted actions, for example, directly accessing APIs used by the game.

- **Client tampering:** Modified binaries might be used by hackers or cheaters to obtain security credentials and take unwanted actions against the game backend, or to award themselves gold or experience in-game without being authorized to do so.

- **Outdated or insecure cryptography:** Many mobile devices run outdated operating systems which no longer receive security updates. This can lead to poor device cryptography or other security issues.

- **Spiky or unpredictable player traffic:** Game launches, in-game events, promotions within the mobile game stores, or even social media activity can result in significant short term increases in traffic which may temporarily overwhelm authentication services.

Authentication and authorization can be a complex topic. There are serious consequences if they are not implemented correctly, so it may be advisable to use a third-party Identity-as-a-Service (IDaaS) to take care of the key functionality. Some considerations in this area are explored in the next section.

---

## WHAT TO LOOK FOR IN AN AUTHENTICATION SOLUTION

Fundamentally an authentication system will be providing security for your players' accounts. A solution must support modern encryption mechanisms, both for data at rest and in transit. HTTPS is a must, and you should check the TLS version (you shouldn't be using anything less than TLS v1.2). iOS has App Transport Security which prevents any outbound connections using anything less than TLS v1.2. Android has a similar capability but this can be overridden. Find out how your players' data is stored in the authentication system, passwords shouldn't be stored directly, and any hashed values should be salted and hashed.

An authentication system should provide a good user experience, both for the developer and the player. It should be easy to register, sign-in and reset passwords. Social login integration, for platforms like Facebook, Twitter, Apple ID or others, that can make the sign-up and sign-in processes simpler for players is also something to consider.

The system should be scalable to meet the peak requests. If you have a successful launch, or some event drives a lot of users (existing or new) to your game, you need to be confident that the authentication system can scale to meet the sign-in and sign-up demand. For hosted services, look for quota/API limits, and for on premises systems, consider how the infrastructure will need to be sized to meet peak demand. Plan for peaks over and above your normal traffic patterns. For example, if your game is organically listed in the Google Play or Apple App Store New Games or Most Downloaded chart, this can result in significant additional player traffic.

If you need multi-platform support, look for systems that support cross-platform functionality that allows players to use the same account across different devices. This includes reviewing what SDKs are available for platforms such as iOS and Android, and for programming languages such as C# and JavaScript.

You will also need to think about the authentication flows you want to use. Do you need to use OAuth/OpenID flows such as authentication code or device grant? Do you want to implement a passwordless flow, such as fingerprint or facial recognition?

Look at the system's customisation options. You may want to build a custom sign-up or sign-in page, or use a pre-built page provided by the system. It should integrate with other systems that hold relevant player data and you should consider what options are available if you need to customise the either the authentication flow or the look-and-feel.

Check the analytics and reporting capability to see what insight you can get from player behaviour. Can you review the login patterns, identify suspicious activity and use this information to improve your game's security?

Make sure you understand the cost model and choose the most appropriate fit for your expected volume. There are options that allow you to pay for what you use (for example, per sign-in/sign-out request, or by number of accounts created), and other systems require an upfront investment. Each option has its pros and cons. The most appropriate fit will depend on your budget, expected volumes, and risk appetite.

If you have compliance requirements to adhere to, such as data protection or age verification, make sure the authentication system is compliant, or allows you to build a solution that is compliant with the correct implementation.

---

## GOOD PRACTICES

Some other key good practices to follow when planning your authentication and authorization approach for your mobile games are:

- Utilize the protection mechanisms provided by the app stores themselves. Google offer the Play Integrity API and Apple offers DeviceCheck, both of which you can use to ensure a player is using a genuine, unmodified game binary to access your backend server resources.

- Take advantage of the device's hardware secure element for locally storing any cryptographic secrets or cached credentials. For Android you should use Keystore, and for iOS you should use Keychain.

- Ensure you periodically authenticate against your backend services. You may need to sometimes trust cached authentication credentials (for example, where a user has no internet connectivity), but you should avoid trusting local-only validation for extended periods of time.

- Consider using two-factor authentication (2FA) for actions which require a higher level of authorization, such as in-app purchases or changes to user data. This could involve sending a code to a known email or phone number for the user to enter in-game. Alternatively, you could implement step-up auth using a device's biometric functionality, such as fingerprint or face ID.

- OAuth 2.0 requests should be made through external user agents, such as the device's browser, rather than directly from the game client. This prevents the host app (or any modified apps) from being able to copy or extract user credentials and cookies, and reduces the need for the user to authenticate separately in each app they use.

- Don't store any Personally Identifiable Information (PII) in authentication tokens. Tokens are signed but not necessarily encrypted, so they can be easily read. Including PII inside a token could result in the sensitive data being inadvertently exposed.

![Figure 1. Example authentication flow](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2023/09/29/mobileauth-1.png)

**Figure 1:** Example authentication flow

Figure 1 demonstrates a high-level authentication flow. The steps involved are as follows:

1. The user of the mobile app authenticates with their chosen identity provider (such as Google, Apple, Facebook, or others) which returns a token.
2. This token is sent to the identity service, which checks that they are trusted, and if so, a token is returned to the app which can be used to log the user in to the app.
3. Optionally, the token is then used to authorize the app to make calls to backend services.

---

## CONCLUSION

In summary, we have discussed the difference between authentication (the act of confirming identity) and authorization (providing access to resources). We also explored the main challenges of mobile game authentication, what to look for in a 3rd party authentication solution and some good practices.

In our next blog post in this series, we'll be looking at how you can use AWS services, such as Amazon Cognito, to build authentication into your mobile game.

For further information, check out the following resources:

- AWS Well Architected Framework Games Industry Lens identity and access management section
- [Guidance for Custom Game Backend Hosting on AWS](https://aws.amazon.com/solutions/guidance/custom-game-backend-hosting-on-aws/?did=sl_card&trk=sl_card)
- [Using Amazon Cognito to authenticate players for a game backend service](https://aws.amazon.com/blogs/gametech/using-amazon-cognito-to-authenticate-players-for-a-game-backend-service/)

**Blog authors:**
- Carl Prescott  AWS Games Solutions Architect
- James Thompson  AWS Senior Solutions Architect

---

## ABOUT THE AUTHOR

![Carl Prescott](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2024/09/26/Carl-Prescott.jpg)

**Carl Prescott** is a Solutions Architect focusing on gaming customers and use cases at AWS. He started gaming on a Commodore Plus/4 far too many years ago and never really stopped. Carl brings his passion for the industry to his role where he helps game developers Build, Run and Grow their games in the cloud using the wide variety of services AWS offers.
