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

