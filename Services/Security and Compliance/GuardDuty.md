- Intelligent threat discovery to protect your AWS account.
- uses machine learning
- inputs data for learning:
	- CloudTrail logs
	- VPC Flow logs
	- DNS logs
	- optiosn features: EKS audit logs, RDS, Aurora ...
- Setup EventBridge to notify in case of findings
- Protect against CryptoCurrency attack 


multi account strategy
- manage multiple accounts in GuardDuty
- Associate Member accounts with Administrator account to start managing member accounts through administrator account.
- NOTE: non-administrator account can also be specified as Organization's delegated administrator for GuardDuty.

Automated Response
- all the findings are sent to EventBridge to then integrate with SNS, SQS, or Lambda.
- Events are published to both member (originated from) and administrator account

CloudFormation
- Can set up GuardDuty using CloudFormation (not directly, because CF will fail if GuardDuty is already enabled)
- instead invoke Lambda using CF to enable GuardDuty if not already.