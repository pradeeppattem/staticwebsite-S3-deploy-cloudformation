# Deploying Static Website in Amazon S3 using AWS Cloudformation

## Objective: 
- Configure AWS CLI 
- Create S3 bucket using Cloudformation
- Create an Index html file to host and deploy it to S3 
- Make it publicly accessible for public to view the content of your website

## Take Aways: 
- Configuring AWS CLI 
- Using CloudFormation in AWS to create resources
- Creating S3 bucket and few of the properties required to create a basic S3 bucket 
- S3 Bucket Policies 


## AWS CLI Commands: 
- `aws sts get-caller-identity` # this provides the current AWS Account details that has been configured like UserID, Account ID and ARN 

    Ex: 
    {
        "UserId": "CXXXXXXXXXXXXX",
        "Account": "XXXXXXXXXXX",
        "Arn": "arn:aws:iam::XXXXXX:user/XXXXXXXX"
    }

    ![Alt Text](misc/AWS_Details.png)
- aws configure # pass in the AWS Access Key, Secret Access Key as prompted in the CLI to configure the CLI to use your AWS account 
- List and confirm if the bucket is already existing using 
    - Using AWS CLI run the command `aws s3 ls | grep <your_s3_bucket_name>`. As you can see in the below screenshot, bucket doesn't exist in the AWS. 
        ![Alt Text](misc/S3_bucket_checkl.png)
    - You can also check the buckets in AWS Console. Navigate to S3 in AWS Console and search with the `<your_s3_bucket_name>` mentioned in the cloudformation template file. 
        ![Alt Text](misc/AWS_S3_Console.png)

- aws cloudformation create-stack --stack-name s3-cf-web-stack --template-body file://s3-static-cf.yaml 
aws cloudformation create-stack --stack-name s3-cf-web-stack --template-body file://<your_cf_yaml_file_name> 
- aws cloudformation describe-stacks --stack-name s3-cf-web-stack  # to check the status of the stack creation from CLI 
    image.png
- aws s3 ls | grep my-s3-static-bucket-by-cf-pk  # To check the S3 bucket created
- aws s3 cp index.html s3://my-s3-static-bucket-by-cf-pk 
    image.png
    image.png

## Errors/ Challenges Faced: 
I did use wrong template format version '2019-09-09' which gave the below error message. Updated it to the right version as in the below screenshot in the resolution.

Error Message: An error occurred (ValidationError) when calling the CreateStack operation: Template format error: 2019-09-09 is not a supported value forAWSTemplateFormatVersion.

## Resolution: Update the AWSTemplateFormatVersion to correct version - 2010-09-09 
![Alt Text](misc/Version_Correction.png) 

## Validation: 
Go to AWS Console >> S3 Buckets >> Bucket >> Object URI 
image.png

## Deleting Stack:
- Deleting the cloudformation stack directly with S3 bucket created fails. 
- We need to delete the S3 bucket recursively and then delete the cloudformation stack 

## Deletion Commands: 
- aws s3 rm s3://<bucket-name> --recursive # to delete the S3 bucket from CLI recursivley all the objects
- aws s3 rb s3://<bucket-name>  # once the bucket is empty delete the bucket with this command
- aws cloudformation delete-stack --stack-name s3-cf-web-stack # to delete the cloudformation stack 

## Validation: Validate in the AWS Console to see the  S3 bucket is removed and Cloudformation Stack is removed. 

