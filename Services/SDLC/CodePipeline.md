Uses artifacts created by previous stage and push them to next stage.
Example: Output from CodeCommit is stored in S3 and the pushed by CP to CodeBuild to continue with the process.

Use CloudWatch (EventBridge) Events for troubleshooting
- Create events for specific cases, like for failed pipelines.

Requires to use IAM roles for restricted access for Pipeline.

CloudTrail to check(audit) denied API calls

Pipeline is list of stages
Each stage can have multiple actions.


For manual approval, the IAM user must have required permissions:
- codePipeline:GetPipeline - To access the pipeline.
- PutApprovalResult - To approve the approval

CloudFormation as a Target
- CF Deploy Action can be used to deploy to AWS resources.
- CF StackSets to deploy across multiple AWS accounts/Regions.
	- CREATE_UPDATE action to create the stack
	- DELETE_ONLY action to delete the stack

Best practices:
- Deployment groups to deploy parallel
- Parallel actions using in a State using RunOrder(same RunOrder)
- Deploy to Pre-Prod before deploying to Prod

EventBridge to detect/react to changes