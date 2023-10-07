Launch Docker container on AWS = Launch ECS Tasks on ECS Clusters

2 launch types:
- Manual - Provision and Manage EC2 instances manually
- Fargate - Serverless

IAM roles
- EC2 Instance Profile (EC2 launch type only)
	- Used by ECS agent to communicate with other services
- ECS Task Role
	- Each task will have a specific role to only allow required permissions.

Load balancer integrations


EFS - Data Volume
- works with both EC2 and Fargate launch types
- Tasks running in any AZ will share the same data in EFS
- Fargate + EFS = Serverless
- NOTE: S3 cannot be mounted as file systems in ECS.


#### Auto Scaling
- CPU utilization
- Memory Utilization
- ALB request count per target
Scaling type:
- Target tracking - based on specific CloudWatch metric
- Step scaling - based on CloudWatch alarm
- Scheduled scaling

ECS Service Auto Scaling (task level) != EC2 Auto Scaling(instance level)

Auto Scaling EC2
- Auto Scaling Group Scaling
	- Scale ASG based on CPU utilization
- ECS Cluster Capacity Provider (Better way)
	- When lacking capacity to launch new tasks, automatically scales ASG


#### Use case:
- EventBridge can run ECS tasks on some event
- ECS Tasks required specific role to communicate with other services.
- EventBridge can record events within ECS tasks and react to it.



#### Logging
To setup logs from ECS to CloudWatch, 
- Configure `logConfiguration` parameter in Task Definition and turn on `awslogs` log driver
For Fargate:
- Tasks Execution Role must have required permissions for CloudWatch.
- Supports awslogs, splunk, awsfirelens log drivers
For EC2:
- send logs to CW logs and save disk space  on your container
- Uses CW Unified Agent & ECS Container Agent
- Enable logging using `ECS_AVAILABLE_LOGGING_DRIVERS` in `/etc/ecs/ecs.config`
- EC2 instances must have permssions. 