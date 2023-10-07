## SDLC methodologies
- Linear sequential model
- Verification model
- Prototype model
- Agile model
- Big bang model

### CI/CD - is enhancement for the SDLC

Code -> Build -> Test -> Deploy -> Monitor
- CI -> Build and Test
- CD -> Deploy

[[DevOps/Domain 1/CodePipeline]] - used to automate the CI/CD process

[[Testing]]

[[Artifacts]]

[[Deployment Strategies]]


#### AWS Services
- CodeCommit
- CodeArtifact
- CodeBuild
- CodeDeploy
- CodePipeline
- Cloud Development Kit (CDK)
- [[CloudFormation]]
- CloudWatch
- X-Ray 
	- Example: want to detect high latency occurrence
	- X-Ray SDK sends the data to a daemon
		- listens on UDP port 2000
		- default network mode of bridge.
- CloudWatch
	- Synthetics
		- monitoring sites, API endpoints and web workflows
	- ServiceLens
		- for end-to-end views
- Systems Manager