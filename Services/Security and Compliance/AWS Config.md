- Overview of the configuration and compliance of your resources. 
- does not prevent actions instead it provides guidlines.
- Example: restrict SSH access to all EC2 instances from anywhere

#### Remediations
- Can execute System Manager Documents 
- Remediation tries

#### Notification
- Trigger EventBridge to send config changes to SNS/Lambda/SQS

#### Configuration Recorder
- create CR to records configs of resources as Configuration Item

#### Aggregators
- Each account is a source of configs
- Create one account which is the Aggregator, it aggregates all the rules, resources across multiple accounts/regions.
- If not using Organizations, then need to authorize the Aggregator to collect data
- Deploy rules to multiple accounts using CF StackSets

#### Conformance Packs
- pack of configs ruls and remediations using yaml file (similar to CF)
- Contains 
	- Config managed rules
	- Config custom rules (lambda)
	- SSM Automation for remediations
- CI/CD - check in the pack yaml file in CodeCommit 

#### Organizational Rules
- Define set of rules to apply to all accounts under organization 
- Similar to Conformance Packs but difference:
	- OR is only for Organizations, CP can be used for loose accounts.
	- OR supports only one rule at a time.
	- OR evaluates the resources against rules defined at Organizational level.