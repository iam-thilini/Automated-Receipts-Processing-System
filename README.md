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

![Image Alt](image_url)

