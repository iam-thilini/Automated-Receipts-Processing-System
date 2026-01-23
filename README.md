# Automated-Receipts-Processing-System
A serverless receipt processing system built on AWS.
This project automatically stores uploaded receipts, extracts key details using OCR, saves structured data, and sends receipt summaries via email. All without managing servers.

## Architecture Overview
Workflow:
  1. Receipts are uploaded to an Amazon S3 bucket
  2. An S3 event triggers an AWS Lambda function
  3. Amazon Textract extracts receipt details
  4. Extracted data is stored in DynamoDB
  5. A summary email is sent using Amazon SES

![Image Alt](https://github.com/iam-thilini/Automated-Receipts-Processing-System/blob/93f151aa9ca12b347c18cfaef05d15c3c4cb71f3/automated_receipt_processing_system.png)

## AWS Services Used
- Amazon S3 – Receipts storage
- AWS Lambda – Serverless processing logic
- Amazon Textract – OCR and receipt data extraction
- Amazon DynamoDB – Structured receipt data storage
- Amazon SES (Simple Email Service) – Email notifications
- AWS IAM – Secure service-to-service access

## Step-by-Step Setup Guide
### 1. Create S3 Storage
1. Open Amazon S3 → Create bucket
2. Bucket type: General purpose
3. Enter a unique bucket name
4. Keep all other settings default
5. Create the bucket

Create folder for incoming receipts
- Open the bucket
- Click Create folder
- Name it, for example:
```
incoming/
```
This folder will be used for all new receipt uploads.
