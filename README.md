# AWS Serverless Application Repository Tutorial
* https://docs.aws.amazon.com/serverlessrepo/latest/devguide/what-is-serverlessrepo.html

* You can easily publish applications, sharing them publicly with the community at large, or privately within your team or across your organization. To publish a serverless application (or app), you can use the AWS Management Console, the AWS SAM command line interface (AWS SAM CLI), or AWS SDKs to upload your code. Along with your code, you upload a simple manifest file, also known as an AWS Serverless Application Model (AWS SAM) template. For more information about AWS SAM, see the AWS Serverless Application Model Developer Guide.

# Quick Start: Publishing Applications
* This guide walks you through the steps to download, build, test and publish an example serverless application to the AWS Serverless Application Repository using AWS SAM CLI. You can use this example application as a starting point for developing and publishing your own serverless application.

### Step 1: Initialize the Application

* `sam init --runtime python3.7`

### Step 2: Test the Application Locally

* `sam local start-api --region us-east-1`

### Step 3: Package the Application

* After testing your application locally, you use the AWS SAM CLI to create a deployment package and a packaged AWS SAM template.

1) Add a `Metadata` section to your AWS SAM template file providing the required application information. Here is an example `Metadata` section:
```yml
Metadata:
  AWS::ServerlessRepo::Application:
    Name: my-app
    Description: hello world
    Author: user1
    SpdxLicenseId: Apache-2.0
    LicenseUrl: LICENSE.txt
    ReadmeUrl: README.md
    Labels: ['tests']
    HomePageUrl: https://github.com/wesleyjr01/serverless-app-repository
    SemanticVersion: 0.0.1
    SourceCodeUrl: https://github.com/wesleyjr01/serverless-app-repository
```
2) Create an S3 bucket in the location where you want to save the packaged code. If you want to use an existing S3 bucket, skip this step.
3) Create the Lambda function deployment package by running the following package AWS SAM CLI command.
```yml
sam-app> sam package \
    --template-file template.yaml \
    --output-template-file packaged.yaml \
    --s3-bucket bucketname
```

### Step 4: Publish the Application
* Execute the following command to publish the new application in AWS Serverless Application Repository with the first version created as 0.0.1.   
```yml
sam-app> sam publish \
    --template packaged.yaml \
    --region us-east-1
```