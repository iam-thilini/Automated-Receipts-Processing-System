# Automated-Receipts-Processing-System
A serverless receipt processing system built on AWS.
This project automatically stores uploaded receipts, extracts key details using OCR, saves structured data, and sends receipt summaries via email. All without managing servers.

## Architecture Overview
**Workflow:**
  1. Receipts are uploaded to an Amazon S3 bucket
  2. An S3 event triggers an AWS Lambda function
  3. Amazon Textract extracts receipt details
  4. Extracted data is stored in DynamoDB
  5. A summary email is sent using Amazon SES

![Image Alt](https://github.com/iam-thilini/Automated-Receipts-Processing-System/blob/93f151aa9ca12b347c18cfaef05d15c3c4cb71f3/automated_receipt_processing_system.png)

## AWS Services Used
- **Amazon S3** – Receipts storage
- **AWS Lambda** – Serverless processing logic
- **Amazon Textract** – OCR and receipt data extraction
- **Amazon DynamoDB** – Structured receipt data storage
- **Amazon SES (Simple Email Service)** – Email notifications
- **AWS IAM** – Secure service-to-service access

## Step-by-Step Setup Guide
### 1️⃣ Create S3 Storage
1. Open **Amazon S3** → Create bucket
2. Bucket type: **General purpose**
3. Enter a **unique bucket name**
4. Keep all other settings **default**
5. Create the bucket

**Create folder for incoming receipts**
- Open the bucket
- Click **Create folder**
- Name it, for example:
  ```
  incoming/
  ```
This folder will be used for all new receipt uploads.

### 2️⃣ Setup DynamoDB Database
1. Open **DynamoDB** → Create table
2. Table name:
   ```
   Receipts
   ```
3. Partition key:
   ```
   receipt_id (String)
   ```
4. Sort key:
   ```
   date (String)
   ```
5. Keep all other settings default
6. Create table
This allows querying receipts by ID and date range.

### 3️⃣ Setup Email Notifications (SES)
1. Open **Amazon Simple Email Service (SES)**
2. Go to **Configuration → Identities**
3. Add a new **Email Address**
4. Verify the email via the confirmation email sent by AWS
This email will receive receipt summaries.

### 4️⃣ IAM Security Configuration
Create a role for Lambda to access AWS services securely.
1. Open **IAM** → Roles → Create role
2. Trusted entity:
    - **AWS service**
    - Use case: **Lambda**

Attach the following policies:
- AmazonS3ReadOnlyAccess
- AmazonTextractFullAccess
- AmazonDynamoDBFullAccess
- AmazonSESFullAccess
- AWSLambdaBasicExecutionRole
3. Role name:
```
ReceiptProcessingLambdaRole
```
4. Create role

### 5️⃣ Create the Lambda Function
1. Open **AWS Lambda** → Create function
2. Select **Author from scratch**
3. Function name:
```
ReceiptProcessor
```
4. Runtime:
```
Python 3.10
```
5. Architecture: Default
6. Permissions:
    - Choose **Change default execution role**
    - Select **ReceiptProcessingLambdaRole**
7. Create function

### 6️⃣ Configure Lambda Settings
Increase Timeout
1. Go to **Configuration → General configuration**
2. Edit timeout:
   ```
   3 minutes
   ```
4. Save

**Add Add Environment Variables**
Go to **Configuration → Environment variables** and add:

| Key                 | Value                                                                     |
| ------------------- | ------------------------------------------------------------------------- |
| DYNAMODB_TABLE      | Receipts                                                                  |
| SES_SENDER_EMAIL    | [your_verified_email@example.com](mailto:your_verified_email@example.com) |
| SES_RECIPIENT_EMAIL | [your_verified_email@example.com](mailto:your_verified_email@example.com) |

### 7️⃣ Add Lambda Code
1. Open the **Code** tab
2. Replace the default code with your Python receipt processing code
3. Click **Deploy**

### 8️⃣ Configure S3 Event Notification
1. Open your S3 bucket
2. Go to **Properties**
3. Scroll to **Event notifications**
4. Click **Create event notification**

**Event settings:**
  - **Name:** ReceiptUploadEvent
  - **Prefix:**
    ```
    incoming/
    ```
  - **Event types:**
    ✅ All object create events
  - **Destination:**
    - Lambda function
    - Select **ReceiptProcessor**
5. Save

### How to Test
1. Upload a receipt (PDF/JPG/PNG) into:
   ```
   s3://your-bucket-name/incoming/
   ```
3. Lambda automatically triggers
4. Receipt data is:
    - Extracted via Textract
    - Stored in DynamoDB
    - Emailed via SES
     
### Sample Email Output
- Receipt ID
- Merchant name
- Date
- Total amount

### Security Notes
- IAM role follows **least privelege access**
- No credentials are hardcoded
- Uses environment variables for configuration


