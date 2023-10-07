Easy way to setup and govern a secure and compliant multi-account AWS environment.


Account Factory
- automates account provisioning and deployments
- create preapproved baselines and configs for accounts
- uses Service Catalog to provision new account

Customizing the account creation using Account Factory
- Use CloudFormation template to define account customizations - Blueprint
- it is in Service Catalog and must be stored in separate account (Hub account)
- Allow Management account access to use the Blueprint in Service catalog to create new account with customizations.


Guardrail - Detect and remediate policy violations
- governance over Control Tower (your accounts)
- **Preventive** - using SCP (block access)
- **Detective** - using AWS Config to make sure to follow defined rules


Customizations for Control Tower (CfCT)
- use code (CF templates and SCPs) to manage accounts through Control Tower

Account Factory for Terraform
- use terraform to provision and manage accounts in CT using deployment pipeline
- create an **account request Terraform file** to trigger AFT workflow
- built-in feature options:
	- CloudTrail Data events - creates trail and enable data events
	- Enterprise Support Plan
	- Delete default VPC