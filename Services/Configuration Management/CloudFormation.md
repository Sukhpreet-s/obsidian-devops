Used to automate creation of other services via config file.
Example: Config file (yaml/json) to create a DynamoDB instance.

CF Templates are uploaded on S3, then referenced in CF.
To edit template, we have to re-upload the updated version. Cannot edit existing templates.

What are Stacks?
List of resource that will be created by CF.
### Building Blocks

Template components:
- Resources (MANDATORY)
	- identifier: `AWS::aws-product-name::data-type-name`
- Parameters - dynamic inputs 
	- can be referenced using `!Ref` 
	- Need to specify when uploading a Stack on CF.
- Mappings - static maps
- Outputs - 
	- references to what has been created, can be used in other Stacks
	- cannot delete stack if the outputs in it are being referenced in some other stack.
- Conditionals - (if statements)
- Metadata

Template helpers:
- References
- Functions 


#### Intrinsic Functions
- !Ref
	- Retrieve Parameters -> returns value of parameter
	- Retrieve Resources -> returns physical ID of resource
- !GetAtt - To retrieve specific attribute of resource.
- !FindInMap [ MapName, TopLevelKey, LowLevelKey ]
- !ImportValue
- !Join [ delimilter, [ a, b, c]]
- !Sub (substitute values in string)
- Conditions:
	- !And
	- !Equals
	- !If ....

#### Rollbacks

Stack failure options:
- Roll back all stack resources
- Preserve successfully provisioned resources

Stack creation fails:
- By default, all stacks are deleted (check logs)
- options to disable rollback

Stack update fails:
- rollback to previous know working state
- check logs to find what happened

#### CF Drift
Feature to use when configurations are changed manually to track the "drifted configs"


#### Stack Policies
By default, CF can update all resources.
Use SP to protect against CF stack updates.
By default in SP, all resources are protected.
Specify an  explicit ALLOW for the resources


#### Nested Stacks
Examples: Load Balancer configuration, Security Group
To update nested stack, always updated parent stack (Example: To delete, only delete the parent stack and the nested stack will automatically be deleted.)


#### ChangeSets
When updating an existing Stack with updated version, use ChangeSets to view all the changes that will be made.
Helpful to check if some change will happen that we don't want to do.


#### DeletionPolicy

Can specify DP for each resources on CF template deletion.
Specify it in the resource options in CF template.

DeletionPolicy: Retain
- specify resources to preserve  (works for any resources/nested stack)
DeletionPolicy: Snapshot
- Only available for certain services: 
	- EBS Volume, ElastiCache Cluster, ElastiCache ReplicationGroup
	- RDS DBInstance, RDS DBCluster, Redshift Cluster
- Actual instance gets deleted, but a snapshot before deletion is saved
DeletionPolicy: Delete (Default)
- for DBCluster resource, snapshot is the default behavior
- To delete S3 bucket, you need to empty the bucket first.

#### Termination Protection
Extra step to secure the accidental deletion on a Stack. 
After stack is created -> stack settings -> Enable termination protection.
Now, to delete the stack, you need to first disable the termination protection.

#### EC2 User Data in CF

`Fn:Base64` function is used to pass the entire script.
Location for User Data script: `/var/log/cloud-init-output.log`
```
Resource:
	MyEC2Instance:
		Type: 
		Properties:
			UserData: !Base64 |
				first line of the script here
				second line of the script here
```

### Helper Scripts
Already bundled in Amazon ami or can be installed using yum
Scripts:
- `cfn-init`: To retrieve and interpret the resource metadata, installing packages, creating files and starting services.
- `cfn-signal`:  wrapper to signal CreationPolicy and WaitCondition
- `cfn-get-metadata`: wrapper to retrieve all or specific part of metadata.
- `cfn-hup`: daemon to check for updates on metadata and execute custom hooks.
`cfn-init -> cfn-signal -> cfn-hup (optional)`

#### CloudFormation Init
Helps with better organizing the EC2 UserData
```
Resources:
	MyInstacne:
		Type: 
		Metadata:
			AWS::CloudFormation::Init:
				config:
					packages:   // To download and install pre-packaged apps (MySQL, PHP)
					groups:     // User defined groups
					users:      // define users, which group they belong to 
					sources:    // download files and place them on EC2
					files:      // create file on EC2 using inline or pulled from URL
					commands:   // run a series of commands
					services:   // launch a list of sysvinit services
```
Can have multiple configs in `AWS::CloudFormation::Init`. Create `configSets` with multiple `configs`
Invoke `configSets` from EC2 user-data.

##### `cfn-init, cfn-signal, cfn-hup`
- Helps with complex EC2 configurations readability.
- These scripts are executed in EC2 user-data.
- Flow: CF will launch the EC2 -> EC2 will then run `cfn-init` -> EC2 will then fetch init data from CF Metadata.
- In `cfn-init` script, specify which resource to fetch the metadata from (name of the EC2 resource)
- In `cfn-signal` script, specify the resource which has the `WaitCondition`
- Logs go to `/var/log/cfn-init.log`.
- `cfn-signal` is run after `cfn-init` is done.
- `cfn-hup` is used to tell EC2 instance to check for Metadata changes every 15 mins and apply them.
- `cfn-hup` config files
	- `/etc/cfn/cfn-hub.conf`
	- `/etc/cfn/hooks.d/cfn-auto-reloader.conf`

`WaitCondition`
```
Resources:
	MyInstance:
		...
		WaitCondition:
			 CreationPolicy:
			 	ResourcePolicy:
					Timeout: PT15M
```
Specified in resource in CF template

**NOTE:** To debug the cfn-init on EC2 instance creation using CF. Make sure to set the "Stack creation option" of the CF stack to be "Disabled" for "Rollback on failure".
Otherwise, on EC2 instance termination, the cfn log files will be deleted.



### Rolling back an update

CF goes into `UPDATE_ROLLBACK_FAILED` state when CF can't rollback during an update.
Example: Roll back an database which was deleted outside of CF.
Solutions:
- Fix the issue outside of CF and then continue CF rollback
- Or, skip the resource that can't be rollback
For nested stack, rolling back parent will also trigger rollback for all nested stacks.





#### Custom Resource
Way to create custom CF resource type. Supports:
- SNS
- Lambda function
	- Example: empty S3 bucket before trying to delete it.
##### How to define?
- ServiceToken (required, must be in the same region) - where CF sends the request to
- Can also provide variables to send to the service with the ServiceToken

##### Flow
- CF Custom Resource -> sends request to Lambda using ServiceToken -> Lambda does it's thing -> Lambda saves the output in S3 bucket (where CF is listening for changes) -> CF get the response.

Example: Delete a non-empty bucket: Write a custom resource using Lambda that will empty the bucket before CF tries deleting it.



### Service Role

- By default, the CF stack will have all the permissions of the user who created the CF stack.
- Case: if user doesn't have permissions to create resource directly, but has `cloudformation:* iam:PassRole` permissions then, the user can create resource using CF.
- Use cases:
	- Least privilege principle
	- not giving the user direct permissions to create the stack resources.


Policies are created in json files, example:
```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Action": [
				"cloudformation:*",
				"s3:*",
				"iam:PassRole"
			],
			"Resource": "*"
		}
	]
}
```




### SSM Parameter Type

Reference parameters in Systems Manager Parameter Store

Allows to store key value pair in SSM Parameter Store. And CF Stack can access the value from SSM Parameter Store as below:
```
Parameter1:
	Type: AWS::SSM::Parameter::Value<String>
	Default: /dev/ec2/instanceType
```

Validations can be done on Parameter keys but not on the values.
Supported Parameter Types:
- `::Name`
- `::Value<String>`
- `::Value<List<String>>`
- `::Value<CommaDelimitedList>`
- some other AWS specific

Common example: Fetch latest AMI IDs



### Dynamic References
- Access external values stored in SSM Parameter Store and AWS Secrets Manager. 
- This is different than using Parameters in CF template. Now these references can be done within the template.
- CF retrieves the values every time stack or a change set operation
- Example: Retrieve RDS DB instance master password from Secrets Manager.
- Supports:
	- `ssm` for plain text
	- `ssm-secure` for secure strings
	- `secretsmanager`
- Can have up to 60 dynamic references in a CF template
- Syntax: `'{{resolve:service-name:reference-key:version}}'`
- Does NOT support to access public SSM parameters like public amazon ami
- Only limited resources support usage of dynamic references in CF template.



### Stack Sets

Used to create/update/delete stacks across multiple accounts and regions with single operation/template.

Administrator account creates the StackSets.
And target accounts executes the stack instances from the StackSets.

StackSet Operations
- Create StackSet
	- Provide template + accounts/regions
- Update StackSet
	- Updates always affect all stacks (not selective)
- Delete Stacks
	- Delete stack and its resources for target accounts/regions
	- Detach stack from your StackSet
	- Delete all stacks in StackSet to prepare for StackSet delete.
- Delete StackSet
	- Must delete all stacks before

Deployment Options:
- Deployment Order
- Maximum Concurrent Accounts
- Failure Tolerance
- Region Concurrency
- Retain Stacks

##### Permission Models for StackSet
- Self-managed Permissions
	- Create IAM roles for both administrator and target accounts
- Service-managed Permissions
	- Use AWS Organizations (enable trusted access)
	- StackSet creates IAM roles on your behalf
	- Merit: Able to deploy to accounts added in future.

StackSets with AWS Organization
- Able to deploy to accounts added in future.
- Can assign StackSet administration to any member account in AWS Organizaiton
- Must enable trusted access

StackSet Drift
- Changes made through CF to a stack are not considered as drifts




















### Questions

CDK does it better than CloudFormation??
###### Using CloudFormation to create custom VPC?
Can allow to create custom VPC using StackSets. But the default VPC will remain.