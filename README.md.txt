# ☁️ AWS Cloud Fun Facts Generator

A full-stack, serverless web application that delivers witty, AI-enhanced fun facts about cloud computing. This project demonstrates the evolution of a backend system from hardcoded serverless functions to a database-driven, Generative AI-powered application.

## 🚀 Project Overview

The Cloud Fun Facts Generator allows users to click a button on a web interface and instantly receive a random cloud computing fact. Behind the scenes, the application uses a fully serverless AWS architecture, fetching data from a NoSQL database and using a Foundation Model to rewrite the fact in a fun, engaging, and witty tone before sending it to the frontend.

### 🏗️ Architecture
1. **Frontend:** Hosted on **AWS Amplify**.
2. **API Layer:** **Amazon API Gateway** intercepts HTTP GET requests and routes them to the backend.
3. **Compute:** **AWS Lambda** (Python) processes the request, orchestrates data retrieval, and handles AI invocation.
4. **Database:** **Amazon DynamoDB** stores the raw cloud facts.
5. **Generative AI:** **Amazon Bedrock** (Anthropic Claude 3.5 Sonnet) transforms the raw facts into witty, engaging sentences.

![Architecture Diagram](./Screenshots/Architecture.png)

## 🛠️ Tech Stack
* **Frontend:** HTML, CSS, Vanilla JavaScript
* **Backend:** Python 3.13, Boto3 (AWS SDK)
* **AWS Services:** * AWS Amplify
  * Amazon API Gateway
  * AWS Lambda
  * Amazon DynamoDB
  * Amazon Bedrock
  * AWS IAM (Identity and Access Management)

## 💡 Key Learnings & Technical Insights

Building this project provided hands-on experience with cloud infrastructure and several key architectural concepts:

* **API Gateway & Lambda Integration:** Gained a clear understanding of the request/response lifecycle. API Gateway acts as the front door, forwarding the `GET` request to Lambda, and then catching the returned output to serve back to the client.
* **Database Evolution:** Transitioned the Lambda function from serving hardcoded arrays to scanning a DynamoDB table. 
  * *Observation:* While adding items manually through the AWS Console works, implementing batch-write operations or automated scripts would highly optimize bulk data entry for larger datasets.
* **CORS Configuration:** Encountered and resolved Cross-Origin Resource Sharing (CORS) constraints. Because the Amplify frontend and API Gateway operate on different domains, specific headers (`Access-Control-Allow-Origin`, `Access-Control-Allow-Methods`) had to be explicitly allowed in the API Gateway settings to permit browser requests.
* **Generative AI Integration:** Successfully utilized Amazon Bedrock to invoke Anthropic's Claude 3.5 Sonnet, adding an intelligent, dynamic layer to static database records.

## ⚙️ How It Works (Step-by-Step)

1. **User Interaction:** The user accesses the static website hosted on AWS Amplify and clicks "Generate Fun Fact".
2. **API Call:** The browser sends a `GET` request to the Amazon API Gateway endpoint.
3. **Compute Trigger:** API Gateway triggers the AWS Lambda function.
4. **Data Fetch:** The Python script uses `boto3` to scan the `CloudFacts` DynamoDB table and selects a random fact.
5. **AI Transformation:** Lambda passes the raw fact to Amazon Bedrock with a prompt to make it short and witty using Claude 3.5 Sonnet.
6. **Response:** The witty fact is passed back through Lambda and API Gateway to the Amplify frontend, where it is displayed to the user.

## 🧹 Resource Cleanup
To maintain a cost-effective cloud environment, all resources utilized in this project were provisioned with the principle of least privilege and successfully torn down post-deployment:
* Deleted AWS Amplify app (`cloud-fun-facts-generator`).
* Removed API Gateway endpoint (`FunfactsAPI`).
* Deleted AWS Lambda function and associated CloudWatch log groups.
* Deleted Amazon DynamoDB table (`CloudFacts`).
* Removed custom IAM roles and policies.

---
*Completed as part of the 'Tech With Lucy' AWS mini-project course.*
