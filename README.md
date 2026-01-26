# 🧾 Automated Receipts Processing System

### Serverless, Event-Driven Document processing on AWS

## 📌 Overview
This project is a **fully serverless, event-driven receipt processing system** built using AWS managed services.
It automatically processes uploaded receipt files, extracts structured financial data using OCR, stores it for querying and analytics, and sends real-time email summaries. All without managing servers.

The system demonstrates **cloud native design principles, AWS best practices**, and **real world automation workflows**.

## 🎯 Problem Statement
Manual receipt management is:
  - Time consuming
  - Error prone
  - Difficult to scale
  - Hard to organize and query
This project solves that by creating an automated cloud pipeline that processes receipts instantly on upload and makes the data searchable and actionable.

## 💡 Solution Summary
Receipts uploaded to Amazon S3 trigger an automated processing workflow powered by AWS Lambda.

### Processing Flow
1. Receipt is uploaded to an S3 bucket
2. S3 event triggers a Lambda function
3. Amazon Textract extracts receipt data
4. Structured data is stored in DynamoDB
5. Receipt summary is emailed via SES
This approach is **cost-efficient, scalable**, and **fully automated**.

🏗️ Architecture
**AWS Services Used**
- **Amazon S3** – Receipt file storage
- **AWS Lambda** – Serverless processing logic
- **Amazon Textract** – OCR and receipt data extraction
- **Amazon DynamoDB** – Structured NoSQL data storage
- **Amazon SES** – Email notifications
- **AWS IAM** – Secure service-to-service access

## ⚙️ Key Design Decisions

### Serverless First
- No infrastructure to manage
- Automatic scaling
- Pay-per-use pricing model

### Event-Driven Workflow
- S3 event notifications eliminate polling
- Instant processing on upload

### DynamoDB Data Modeling
- Partition key: `receipt_id`
- Sort key: `date`

This enables efficient lookups and future date-range queries.

### Security by Design
- Dedicated IAM role for Lambda
- Least-privilege permissions
- No hardcoded secrets (environment variables used)

## 🧪 How It Works 
1. Upload a receipt (PDF / JPG / PNG) to:
  ```
   s3://<bucket-name>/incoming/
  ```
2. Processing starts automatically
3. Receipt data is saved in DynamoDB
4. A summary email is sent via SES

No manual steps required after upload.

## 📘 Detailed Setup Guide
For step-by-step AWS configuration and deployment instructions, see:

👉 [Setup Guide](docs/setup-guide.md)

## 🔐 Security & Reliability
- IAM roles scoped strictly to required services
- Managed AWS services provide high availability
- CloudWatch logs available for monitoring and debugging
- Designed to handle increasing receipt volumes seamlessly
















