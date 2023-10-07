### Versions 
- $LATEST version is always the most recent one. It is immutable
- When publishing, new version is published from the $LATEST to v1 (example)
- Every version can be accessible using its ARN

### Aliases
- Pointers to a specific Lambda version. Useful to point to a dev version, prod version ...
- The versions created using aliases are mutable
- Alias can point to any version and still be mutable.
- Enables canary deployments
- cannot reference other aliases
- get their own ARN


### Environment Variables
- Key value pairs
- can be store secrets encrypted with KMS
- secrets can be encrypted by Lambda service key or your own CMK


### Concurrency
- Can scale very easily
- upto 1000 concurrent executions
- should set max concurrency limit
	- limit is common across the account for all the lambda functions.
	- if one lambda function scales to 1000, then all other lambda functions will throttle.
- if lambda instances are already busy, then the additional requests will be throttled
	- the additional requests will be sent to internal queue and try to process it for next 6 hours
	- the retry time increases exponentially from 1 second after every 5 minutes
- Cold start
	- on first lambda instance -> the init handler is executed 
	- if init is large, the first request takes long time 
	- Provisioned Concurrency - concurrency is allocated before function is invoked
		- Application Auto Scaling can manage concurrency

### File System Mounting
- Lambda can access EFS if running in a VPC.
- Configure Lambda to mount EFS to local directory during init
- Must use EFS Access Point
- Each lambda instance creates new connection to EFS.
	- So if burst of instances are created, then it might hit the limit of connections to EFS.
- Storage types for Lambda:
	- Ephemeral Storage (/tmp)
		- not shared
	- Lambda Layers
		- Static content (immutable)
		- it is shared across all invocations
	- Amazon S3
	- Amazon EFS

#### Cross Account EFS mounting
- Connect VPCs across accounts using VPC peering.
- Provide Lambda in 1st account permissions required to use EFS.
- Provide EFS in 2nd account Policy to allow EFS operations from 1st account root user.
- that's it.
