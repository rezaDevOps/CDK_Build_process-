![CDK_App_Build_Processing](https://github.com/user-attachments/assets/41aa5d9a-db65-4bad-897a-4f215100a9d9)


we're going to do a hands-on on CDK. And with this hands-on, we're going to deploy an application that allows us to deploy an S3 bucket

on which the users can put an image. This S3 bucket is going to trigger a Lambda function which is going to send an API call

to Rekognition to analyze the image and get the results back from Rekognition, and then the Lambda function is going to save the results

to Amazon DynamoDB. And all of this is going to define all from within a CDK script.

This is an AWS CDK application that creates an image processing pipeline using several AWS services. Here's how it works:

**1) Infrastructure Components (cdk-app-stack.js):**

- An S3 bucket to store images
- A DynamoDB table to store image labels
- A Lambda function with necessary IAM roles Event source mappings

**2) Processing Flow:**

- Images are uploaded to the S3 bucket
- This triggers the Lambda function automatically
- The Lambda function (index.py) then:
     *Uses AWS Rekognition to detect labels in the image
     *Stores the detected labels in DynamoDB
     *Processes up to 10 labels per image with minimum confidence of 60%

**3) Key Features:**

- Images are analyzed automatically upon upload
- Labels are stored with the image name as the partition key
- Each detected object gets stored as a separate attribute in DynamoDB
  
**The deployment process follows the steps in steps.sh, which includes CDK initialization, bootstrapping, and deployment commands.**

Example flow:

Upload an image like kid_and_pigeons.jpeg to the S3 bucket
Lambda automatically processes it using Rekognition
Results are stored in DynamoDB with the image name as the key and detected objects as attributes
