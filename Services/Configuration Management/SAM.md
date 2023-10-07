Serverless Application Model

To generate complex serverless applications using YAML files

Only 2 commands to deploy

Can use CodeDeploy to deploy Lambda functions
Can help with running Lambda, API Gateway, DynamoDB locally


### SAM - Recipe

Transform header indicates how to parse SAM template to CF.
	`Transform: 'AWS::Serverless-2016-10-31'`
Write Code:
	`AWS::Serverless::Function`
	`AWS::Serverless::Api`
	`AWS::Serverless::SimpleTable`
Package and deploy:
	`aws cloudformation package / sam package`
	`aws cloudformation deploy / sam deploy`

##### Deployment flow

1st Stage: SAM Template + App Code

Process: transform `sam build`

2nd Stage: CF Template + App Code

Process: package (zip and upload) `sam package`

3rd Stage: S3 Bucket

Process: deploy (create/execute ChangeSet) `sam deploy`

4th Stage: CloudFormation stacks are created


##### SAM CLI + AWS Toolkits

SAM CLI
- locally build, test and debug Lambda functions (serverless apps)
- provides lambda-like environment locally

AWS Toolkit
- Supported with multiple IDEs: Cloud9, VS Code, JetBrains
- helps with build, test, debug, deploy, and invoke Lambda functions that are build using SAM


##### SAM and CodeDeploy

SAM natively uses CodeDeploy to update Lambda functions.
Uses traffic shifting feature when updating
Allows to run Pre and Post traffic hooks
Setup CloudWatch alarm to monitor CodeDeploy and rollback if necessary