
Can deploy on:
- EC2 or on-premises servers
- Lambda
- ECS


### EC2

Can define deployment speed
- AllAtOnce: most downtime
- HalfAtATime:
- OneAtATime: least downtime
- Custom

Must install CodeDeploy Agent to EC2 instances (Can automate through Systems Manager)
EC2 Instance must have permissions to access S3

Deployment hooks: Used to run scripts in deployment lifecycle
- lifecycle scripts are mentioned in appspec.yml for CodeDeploy to execute them.

##### In-Place Deployment (Half At A Time)
Shut does existing instances and deploy and then start again
##### Blue-Green Deployment
Create new instances with updated version and shift the traffic to the new version depending on the strategy.
Requires to use ALB.
- Manual 
	- provision the EC2 instances manually
- Automatic
	- Requires auto scaling group
	- Automatically create the new ASG with same settings and new version of instances.
Instance termination


On deploy failure, CodeDeploy sends event (ex: InstanceFailure) to SNS topic

### Lambda

Alias?
Alias points to the Lambda version (ex: v1)

To automate:
- create the new Lambda with updated version
- Create `appspec.yml` file referencing the updated Lambda version 
- CodeDeploy uses the `appspec.yml` file as input artifact to update Lambda alias to point to updated Lambda function.

CodeDeploy Agent is NOT required.

Only Blue-Green deployment is supported

Traffic shifting strategies
- Linear
- Canary
- AllAtOnce

### ECS

To automate: 
- push updated docker image to ECR
- Create ECS Task Definition
- Create `appspec.yml` file in S3
- CodeDeploy will then use `appspec.yml` as input artifact to deploy.

CodeDeploy Agent is NOT required.

Only Blue-Green deployment with following strategies (Must be connected to LB):
- Linear
- Canary
- AllAtOnce (immediate)


Hooks are Lambda functions instead of scripts.


### Rollbacks
### Troubleshooting
Any deployment failure can be intercepted with EventBridge
ELB health checks