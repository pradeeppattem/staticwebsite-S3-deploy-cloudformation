# s3-static-basic
Deploying and Hosting a basic HTML static website in Amazon S3


Objective: 
1. Configure AWS CLI 
1. Create S3 bucket using Cloudformation
3. Create an Index html file to host 


Take Aways: 
1. Configuring AWS CLI 
2. Using CloudFormation in AWS to create resources
3. Creating S3 bucket and few of the properties required to create a basic S3 bucket 
4. S3 Bucket Policies 


Commands that will be handy: 
1. aws sts get-caller-identity # this provides the current AWS Account details that has been configured like UserID, Account ID and ARN 

    Ex: 
    {
        "UserId": "CXXXXXXXXXXXXX",
        "Account": "XXXXXXXXXXX",
        "Arn": "arn:aws:iam::XXXXXX:user/XXXXXXXX"
    }