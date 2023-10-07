- Helps manage EC2 and On-premise systems at scale
- Get operations insights about the state of infrastructure.
- Easily detect problems
- **Patching automation for enhanced compliance**
- for windows and Linux
- Integrated with CloudWatch metrics/dashboard
- Integrated with AWS Config
- Free service
- EC2 instances don't need security group inbound rule because SSM agent is communicating to the Systems Manager instead of Systems Manager accessing EC2.

#### Features
Resource Groups using AWS Tags
Insights:
- Dashboard
- Inventory: discover and audit the software installed 
- Compliance
**<u>Parameter Store</u>**
Shared Resources:
- Documents (scripts)
	- Run scripts on nodes
	- Can be used to install stuff on nodes
	- Example: run apache http server on target EC2 instances using shell script
	- logs the output to CloudWatch logs
FleetManager
- Dashboard to managed nodes (Ex: EC2 instances with SSM agents)

#### Actions
Automations (shutdown EC2, create AMI)
**<u>Run commands to all instances</u>**
<u>Session Manager</u>
<u>Patch Manager</u>
Maintenance Windows
State Manager: define and maintain configuration of OS and applications.


#### Setup 
Install SSM Agent to all the servers (EC2 or on-premise).
SSM agent then communicates with SSM service.
If SSM agent can't be controlled by SSM, it's probably issue with SSM agent/IAM roles to allow SSM actions.



#### AWS Tags
- Key value pairs
- Used to group resources, automation, cost allocation


#### Automations
- Simiplifies common maintenance and deployment tasks of EC2 instances and other resources
- Example: restart instances, create and AMI, EBS snapshot
- Automation Runbook (SSM document of type automation)
- Can be triggered by:
	- manually with AWS Console, CLI or SDK
	- EventBridge
	- on a schedule using Maintenance Windows
	- AWS Config for rules remediation


#### Parameter Store
- Can stores key values with encryption from KMS


#### Patch Manager
- Automate process of patching managed instances
- Supports both EC2 instances and on-premises
- Patch on demand or on schedule using Maintenance Windows.
- Generate patch reports

##### Patch Baseline
- Defines which patches to install and not
- Ability to create custom Patch Baselines (specify approved/rejected patches)
- By default, Install only critical patches and the one related to security.

###### Predefined
- Managed by AWS for different OS.
- `AWS-RunPatchBaseline` (SSM Document) - apply both os and application patches.
###### Custom Patch Baselines
- Specify OS, allowed, rejected patches and more
- ability to specify custom and alternative patch repository

##### Patch Group
- create group of instances to use Patch Baseline
- Instances can only be part of one Patch Group at a time.
- To use, create a tag with key name "Patch Group"


###### Flow:
- Define Patch Baselines using Patch Groups or default
- Run Document `AWS-RunBatchBaseline` using Console, SDK, or Maintenance Window
- SSM Agents on each instances will be triggered to fetch the Patch IDs based on the what is specified in Patch Manager for each of the instances. 
- SSM Agent installs the patches.
- When using Maintenance Window, use Rate Control to specify min/max of targets allowed in parallel: Also specify: 
	- Schedule
	- Duration
	- Set of registered instances
	- Set of registered tasks

### SSM - Session Manager
- Allows to start secure shell on EC2 and on-premises servers
- Does NOT need SSH access, bastion hosts, or SSH keys.
- Access through Console, CLI, or SDK
- Can log connection to instances and executed commands. Send logs to S3 or CloudWatch logs
- Use CloudTrail to intercept StartSession events
- Requires IAM permissions


#### Default Host Manager Configuration

- Usually, to have EC2 communicate with SSM, IAM role with correct policy is required.

But can work without it

- Must have DHMC enabled in Systems Manager.
- Each EC2 instance have Instance Identity Role (no permissions) allows other AWS services (Systems Manager) to identify the instance.
- After EC2 instance identifies with Systems Manager, then SSM will send the necessary IAM roles to EC2 which will allow SSM to make changes to EC2.
- Must enable IMDSv2 (metadata) on EC2 instances
- Must be enabled per Region basis.



#### Setup SSM on Hybrid Environments

- Can setup SSM on on-premises instances.
- Steps:
	- On SSM, create hybrid activation
	- Receive Activation Code and ID.
	- Install SSM Agent on on-premise instance.
	- Register with SSM using Activation Code and ID
	- On-premise instance should then show up in Systems Manager as `mi-...` managed instance.
- Automate the setup using API Gateway, Lambda, Systems Manager:
	- On-premise server sends HTTP GET request to API Gateway.
	- The Gateway passes payload to Lambda.
	- Lambda creates the hybrid activation on Systems Manager and retrieves the Activation Code and ID.


### Automation - Use cases

- Reduce costs by automatically start and stop EC2 instances and RDS DB instances. Setup:
	- Use EventBridge to schedule SSM Automation (Run Documents) at specific time to start and stop EC2 instances.
- Reduce compute capacity
- Automatically update app configuration if configuration is `NON_COMPLIANT` according to defined Config Rule. Create Config Remediation which will automatically run SSM automation to update configuration of specific service to meet the Config Rule.



### Compliance
- Scan managed nodes for patch compliance and configuration inconsistencies.
- Display current data about:
	- Patches in Patch Manager
	- Associations in State Manager
- Can sync compliance data from across regions to S3 using Resource Data Sync, and use analytics tools
- Send compliance data to Security Hub.



### OpsCenter

One place issue resolver for all services.
Example of issues:
- Security issues (Security Hub)
- Performance issues (DynamoDB throttle)
- Failures (ASG failed to launch instance)
- and more.

###### Ops Items
- Operational issues that need to be resolved
- Example: Event, resource, Config changes, CloudTrail logs, EventBridge, ....
- Provides recommended Runbooks to resolve.