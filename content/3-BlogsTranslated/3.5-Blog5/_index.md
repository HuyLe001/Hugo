---
title: "Strengthen Foundation Model Queries Through Amazon Bedrock-Amazon Alexa Integration"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 3.5. </b> "
---

{{% notice warning %}}
 **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# STRENGTHEN FOUNDATION MODEL QUERIES THROUGH AMAZON BEDROCK-AMAZON ALEXA INTEGRATION

**Original Article:** [Strengthen foundation model queries through Amazon Bedrock-Amazon Alexa integration](https://aws.amazon.com/vi/blogs/publicsector/strengthen-foundation-model-queries-through-amazon-bedrock-amazon-alexa-integration/)

**Original Authors:** Cristiano Scandura and Gabriel Martini

**Publication Date:** 17 JAN 2025

---

Today, generative artificial intelligence (AI) is at the core of many of the decisions and technologies businesses across the globe are implementing. The linchpin to ensuring that generative AI is effective depends on the foundation models (FMs) storing the data. To make sure that those FMs are pulling the correct data, Amazon Web Services (AWS) has developed a solution through Amazon Bedrock to generate SQL to answer user questions about the data. The solution was developed to support the Federal Institute of São Paulo (IFSP) and has optimized their decision-making.

Generative AI is based on large FMs, which are trained on vast amounts of data and are capable of generating text, images, audio, code, and much more. However, this data may be outdated or lack context, and these models have difficulty processing structured data and generating more deterministic answers. This difficulty can result in hallucinations, where the model generates outputs not based on the input data or factual knowledge. For example, when trying to sum values in a table, the model may produce random or inconsistent numbers instead of performing the calculations correctly.

This inability to properly interpret the structure of rows, columns, and cells, as well as the complex relationships between them, can lead to errors in identifying maximum, minimum, and other mathematical operations. Hallucination and inaccuracy issues are especially critical when dealing with sensitive data, such as financial, medical, or scientific information, where accuracy is essential, compromising the reliability of an application that uses generative AI.

One way to deal with the hallucination problem when answering questions in the context of structured data is to use the models to generate SQL queries. Instead of trying to directly interpret tables and perform mathematical operations, a trained model can be used to generate SQL queries based on natural language.

Anthropic created Claude 3, an AI assistant capable of interpreting large context windows. Using prompt engineering techniques, the model can combine natural language understanding with specialized knowledge in SQL and database structures. To assist users, Anthropic has a library of prompts for different use cases, including the SQL sorcerer prompt for generating SQL queries. With these prompts, users can generate a SQL code with natural language, orchestrate the execution of the query using database services, and generate a user-friendly response. The following diagram shows the high-level architecture of the solution.

![Architecture diagram showing the integration flow between Alexa, AWS Lambda, Amazon Bedrock, Amazon Athena, AWS Glue, and Amazon S3.](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2025/01/17/FM_queries_Bedrock_Alexa_figure1.png)

**Figure 1:** Architecture of the Alexa integration solution with Amazon Bedrock.

The major components are an Amazon S3 bucket, AWS Lambda, Amazon Athena, Amazon Bedrock, AWS Glue, and Amazon EventBridge.

In this solution, users can ask questions about data through Alexa using a skill. The Alexa Skills Kit is a software development framework you can use to create content, called skills. The solution also uses Amazon Bedrock, a fully managed service that offers several high-performance FM options from leading AI companies such as AI21 Labs, Anthropic, Cohere, Meta, Mistral AI, Stability AI, and Amazon, through a single API. Amazon Bedrock also has a broad set of necessary resources such as knowledge bases, agents, and guardrails to create generative AI applications with safety, privacy, and responsibility.

The flow of the architecture follows these steps:

1. The process starts with users asking questions in natural language through Alexa. These questions are forwarded to an AWS Lambda function. The function will interact with Anthropic's LLM, specifically the Claude 3 Haiku model, through Amazon Bedrock API calls.

2. Claude 3 Haiku receives the database structure as context, such as the description of tables and fields, through the user's question. Based on the question and the database structure, the model generates SQL code. The generated SQL query is then executed in Amazon Athena, which retrieves data from structured ".csv" files stored in Amazon Simple Storage Service (Amazon S3). Athena uses the metadata from the data catalog managed by AWS Glue Data Catalog.

3. The data returned after executing the SQL query is used as context in a new Amazon Bedrock API call for the Claude 3 Haiku to generate a text response, explaining the query data in a natural and understandable way. This response is then returned by the Lambda function to Alexa, which converts it to audio and responds to the user.

4. To keep the solution up-to-date in case of structural changes in the database, there is a rule created in Amazon EventBridge that is triggered every time data is updated in Amazon S3 and will trigger a Lambda function that updates the data catalogs in AWS Glue by executing the AWS Glue crawler and updating the solution's context files.

This solution arose from the need of the IFSP, which today has more than 50,000 students, to optimize decision-making for administrative managers in an increasingly dynamic environment that requires quick budgetary and educational decisions based on a large amount of data. IFSP worked on developing the Alexa skill in collaboration with AWS, thus enabling natural language interaction with a complex set of data present in the Nilo Peçanha Platform. This offered top management a means of accessing data and educational indicators to support decision-making with the correct alignment of the institution with its strategic and social demands.

"Natural language interaction with the data from the Nilo Peçanha Platform is a necessary evolution to streamline strategic decision-making, based on data and innovation through the integration of AWS generative AI tools in the daily life of our institution's managers," said Bruno Luz, pro-rector of planning and institutional development at IFSP.

The data was imported and stored in a serverless data lake architecture on AWS, using Amazon S3 as the storage layer and AWS Glue and Amazon Athena for data cataloging and querying. Different prompts were tested on the Claude 3 Haiku, using techniques such as zero-shot and few-shot. The following prompt best met this use case:

\\\
Human:
Transform this natural language question into a query for AWS Athena. Respond only with the SQL query in a single line. In the query, the table name and column names should be in quotes. ONLY the table name should have '"AwsDataCatalog"."s3".'. Do not generate queries related to any database alterations, only generate query questions. Assume that the database has the following tables and columns:

Table: TaxaEvasao

- Id (integer pk)
- Description (varchar)
- Quantity (number)

<others tables...>

For questions related to Dropout Rate, table TaxaEvasao, consider that the calculation of the dropout rate is the sum of the numero_de_matriculas column divided by the sum of the matriculas_numero_de_evadidos column. Additionally, the number must be in decimal format, and Athena will present a decimal if both sums have a CAST to decimal. For example, to list the dropout rates for 2022, the correct query would be:

SELECT instituicao, sum(numero_de_matriculas) as MAT, sum(matriculas_numero_de_evadidos) as EVD, CAST ((sum(numero_de_matriculas)) AS decimal(10,2))/CAST ((sum(matriculas_numero_de_evadidos)) AS decimal(10,2)) FROM "AwsDataCatalog"."s3"."TaxaEvasao" WHERE "ano" = 2022 GROUP BY instituicao ORDER BY "instituicao" DESC;

<other queries tables samples...>

Identify the query generated in your response and place it between the <query></query> tags
\\\

Through this prompt and according to the user's question, the Claude 3 Haiku responds with the SQL code. For example, for the question, "List the top 3 institutes with more student-teacher ratio for the year 2022" the result was:

\\\sql
SELECT instituicao_nome, rap
FROM "AwsDataCatalog"."s3"."RelacaoAlunoProfessorRAP"
WHERE ano = 2021 ORDER BY rap DESC LIMIT 3;
\\\

After the query is made in the data lake, the final response to the user is generated dynamically using the LLM. The following screenshot shows the returned result.

![Screenshot of Alexa developer console showing natural language question and AI-generated response with query results.](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2025/01/17/FM_queries_Bedrock_Alexa_figure2.png)

**Figure 2:** Example of questions and answers in tests on the Alexa developer console.

You can download the source code for this solution and run your version of the Alexa skill by accessing the published example in the official AWS sample GitHub repository.

"The use of AI with AWS allows IT areas to play an innovative role, opening doors to the use of new technologies for institutional evolution towards more prepared and agile environments at an affordable cost and compatible with the technological complexity involved," said Leonardo Menzani Silva, director of IT at IFSP.

---

## SECURITY, PRIVACY, AND PROTECTION

It's important to highlight that the solution provides resource security. Data is encrypted at rest and in transit, both by Amazon Bedrock and in the integration of Alexa with the Lambda function. In this solution, we enabled data encryption in S3 buckets by default using keys that can be created and managed in the AWS Key Management Service (AWS KMS).

Amazon Bedrock doesn't share your data with model providers and doesn't use it to retrain public models, meaning the service maintains data confidentiality. When you tune your FM, it is based on a private copy of that model. Amazon Bedrock complies with international standards, including ISO, SOC, CSA STAR Level 2, and GDPR, and is eligible for HIPAA.

The following diagram shows how access permissions to services and resources work using roles and policies created and maintained with AWS Identity and Access Management (IAM).

![Diagram showing IAM roles and policies for Alexa skill, Lambda function, Amazon Bedrock, Athena, AWS Glue, S3, and KMS access permissions.](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2025/01/17/FM_queries_Bedrock_Alexa_figure3.png)

**Figure 3:** Architectural diagram of access permissions to services and resources.

For the Alexa skill to be able to call a Lambda function, it needs to configure the Amazon Resource Name (ARN) of the Lambda function in the skill development console. In turn, it needs to create a resource-based policy with the ID of the skill associated with the Lambda function that allows it to be called by the skill.

Additionally, you need to create resource-based policies so that the Lambda function, when invoked, can access the Amazon Bedrock, Athena, and AWS Glue catalog services. Although the function does not directly access AWS Glue, the policy associated with it allows it, through Athena, to access resources stored in Amazon S3 and the data encryption key stored in AWS KMS.

The solution did not address data access authorization because the data is public. If you need to limit user access to data, you can use the account linking functionality of the Alexa Skills Kit.

---

## COSTS

This solution used Amazon Bedrock On-Demand billing, which allows the use of FMs without the need for time-based commitments. Text generation models are charged per input tokens processed and per output tokens generated.

A token comprises a few characters and refers to the basic unit of text that a model learns to understand the prompt. For Claude, a token represents approximately 3.5 characters in English, although the exact number may vary depending on the language used. Tokens are usually hidden when interacting with language models at the "text" level, but they become relevant when examining the exact inputs and outputs of a language model.

In the cost estimates with IFSP, 1,000 monthly calls were stipulated. To reduce costs, the first processing, where the SQL query was generated, used the Claude 3 Haiku LLM with the input prompt using around 6,000 tokens and generating an output with around 400 tokens, costing approximately USD 1.50. In the second part, where the final response was generated, we used the Claude 3 Sonnet LLM to have a more appropriate response. The result was 400 tokens as input and around 150 tokens as output, costing approximately USD 1.20.

For detailed pricing information, please refer to the Amazon Bedrock Pricing page.

---

## CONCLUSION

The integration of generative AI with Alexa for data analysis, using advanced models such as Anthropic's Claude 3 on Amazon Bedrock, simplifies interaction with complex data, transforming natural language queries and returning accurate responses. This solution, exemplified by the success at the Federal Institute of São Paulo, demonstrates the effectiveness of the approach, making data analysis more accessible. To learn more, contact your AWS account team or the AWS Public Sector team.

---

## ABOUT THE AUTHORS

![Cristiano Scandura](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2024/12/13/Cristiano_Scandura.jpg)

**Cristiano Scandura** has been in the IT industry since 1998. He joined Amazon Web Services (AWS) in 2018, where he worked on projects for enterprise clients. Currently, he specializes in generative artificial intelligence (AI), AI, and machine learning (ML) projects for AWS Worldwide Public Sector.

![Gabriel Martini](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2024/12/13/Gabriel_Martini.jpg)

**Gabriel Martini** has experience in software engineering, solution architecture, and data science. He has worked in IT since 2014 and joined Amazon Web Services (AWS) in 2017. At AWS, he's worked as a solutions architect for large clients and on open data research initiatives. He currently works as an artificial intelligence (AI) specialist solutions architect focusing on areas such as generative AI, machine learning operations (MLOps), and computer vision.
