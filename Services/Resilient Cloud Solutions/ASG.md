#### Dynamic Scaling Policies
- Target Scaling
	- Specify average CPU usage to be at 40%. ASG will add/remove to maintain that.
- Simple/Step Scaling
	- Specify CloudWatch Alarm (combine CPU>70%) and then how many add/remove instances.
- Scheduled Scaling
- Predictive Scaling - Machine learning


Scaling Cooldown


Lifecycle hooks - run Lambda, SNS, SQS on any hook call
- pending - runs some stuff then notify to continue
- InService
- terminating - runs some stuff then notify to continue
- terminated

Notifications:
- SNS - not great
- EventBridge - better information on events and ability to filter notifications.


Termination Policies
Default:
- AZ with max intances
- old launch template/configuration
- closed to billing date/hour 
There are other options available
Can use more than 1 policy at a time.
Can create Custom Termination Policy using Lambda



Warm Pools
- Problem: latency on instance startup
- Solution: Create set of pre-initialized instances and keep them `Stopped/hibernated` state. Once load increases, move pre-initialized instance to ASG.
- Instance Reuse Policy when scaling in
- Lifecycle hook: Must specify when the instance is initialized manually (does NOT happen automatically)


Application Auto Scaling - Integrated AWS Services
- Specify variety of services to scale in/out
- Importance services that can be scaled: Aurora, DynamoDB Table capacity/GSI, ECS, Lambda