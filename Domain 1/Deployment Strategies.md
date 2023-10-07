
Deployment methods
- Blue/green
- Canary
- Immutable rolling
- Rolling with additional batch
- In-place
- Linear
- At-at-once

ECS deployment strategies:
- Rolling update
	- How to identify when deployment fails:
		- CloudWatch alarms
		- Deployment circuit breakers
- Blue/green deployment with CodeDeploy
- External deployment

Serverless deployment strategies
- [[CloudFormation]]
- Serverless Application Modal (SAM)
- All-at-once
- Blue/green
- Canary
- Linear
- Lambda versions and aliases
- CodeDeploy

CodeDeploy strategies
- define pre-traffic/post-traffic hooks
	- Pre-traffic hooks is a Lambda functions invoked by CodeDeploy
	- Post-traffic hook can be used for integration tests.
		- Post-traffic hook runs after the traffic shifting completes.

Troubleshooting
- Mutable
- Immutable