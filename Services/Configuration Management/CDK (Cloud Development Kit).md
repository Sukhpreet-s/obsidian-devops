- Used to create AWS services/process with code.
	- services/resources are created using Application Constructs
- Example: create DynamoDB instance and tables in it.
- To use, install CDK for required programming language.
- Can use any language. 
- Better version of CloudFormation !?
	- Helps with errors in the resource creation code, whereas cannot detect errors in yaml file.
- CDK is compiled to [[CloudFormation]] then deploys to AWS.
	`cdk synth` command is used to compile to CF template.
- Can use SAM CLI to test CDK apps (lambda functions) locally
	`sam local invoke -t MyCDKStack.template.json myFunction`
