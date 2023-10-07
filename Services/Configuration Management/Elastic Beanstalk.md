Deploy and scale web applications (Managed)
Auto scaling
Load balancing
Provisioning
Health monitoring


Only supports RDS database connection through the UI.

Can create .ebextensions configuration file to create DynamoDB tables or similar.


Environment Types:
- Web server (ALB, ASG)
- Worker (SQS, SNS)

Can have multiple environments for dev, test, prod

Deployment options:
- All at once: fastest but most downtime
- Rolling: update few instances(bucket size) and then move to next bucket of instances to update.
- Rolling with additional batches: For a bucket, create new instances with updated version. transfer old to new instances.
- Immutable: new instances in new ASG, swap all the instances when deployed and healthy.
- Blue Green: create a new environment and switch over based on strategies.
- Traffic Splitting (Canary): send small % of traffic to new version of instances and later if eveything is healthy, move all the instances.