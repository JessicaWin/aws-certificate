# AWS Serverless Application Repository
+ The AWS Serverless Application Repository makes it easy for developers and enterprises to **quickly find, deploy, and publish serverless applications** in the AWS Cloud.
+ You can easily **publish applications**, sharing them publicly with the community at large, or privately within your team or across your organization. 
+ To publish a serverless application (or app), you can use the AWS Management Console, the AWS SAM command line interface (AWS SAM CLI), or AWS SDKs to **upload your code**. **Along with your code, you upload a simple manifest file**, also known as an AWS Serverless Application Model (AWS SAM) template. 
# Publishing Applications
+ Initialize. Download a sample application from template using sam init.
+ Test Locally. Test the application locally using sam local invoke and/or sam local start-api. Note that with these commands, even though your Lambda function is invoked locally, it reads from and writes to AWS resources in the AWS Cloud.
+ Package. When you're satisfied with your Lambda function, bundle the Lambda function, AWS SAM template, and any dependencies into an AWS CloudFormation deployment package using sam package. In this step you will also include information about the application that will be uploaded to AWS Serverless Application Repository.
+ Publish. Publish the application to the AWS Serverless Application Repository using sam publish. At the conclusion of this step, you're able to view your application in AWS Serverless Application Repository and deploy it to the AWS Cloud using AWS Serverless Application Repository.
+ View Your Application in AWS Serverless Application Repository – The output of the sam publish command will include a link to the AWS Serverless Application Repository directly to the detail page of your application. You can also go to the AWS Serverless Application Repository landing page and search for your application.
+ Share Your Application – Because your application is set to **private by default, it is not visible to other AWS Accounts**. In order to share your application with others, you must either make it public or grant permission to a specific list of AWS Accounts.
# Deploying Applications
+ There are three categories of applications that you have permissions to deploy:
    + Private – Applications that were created with the same account, and haven't been shared with any other account. You have permission to deploy applications that were created using your AWS account.
    + Privately shared – Applications that the publisher has explicitly shared with a specific set of AWS accounts. You have permission to deploy applications that have been shared with your AWS account.
    + Publicly shared – Applications that the publisher has shared with everyone. You have permission to deploy any publicly shared application.
# Reference
[AWS Serverless Application Repository](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/what-is-serverlessrepo.html)