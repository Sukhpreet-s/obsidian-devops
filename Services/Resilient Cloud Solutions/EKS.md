Run managed containers
Open source, provides standardization across platforms, easy to switch platform
Two mode:
- EC2 for worker nodes
- Fargate for serverless containers
Use cases: 
- already using Kubernetes on-premises, then can shift to EKS for AWS managed service.
Node Types:
- Managed Node Groups:
	- creates and manage for you
	- part of ASG managed by EKS
	- Support for on-demand or spot instances
- Self managed nodes
	- created by you and registered to EKS cluster and managed by ASG
	- use prebuild AMI (Amazon optimized ami for EKS)
	- Support for on-demand or spot instances
- Fargate
	- No maintenance, management required
Data Volumns
- To attach data volumns to EKS clusters, need to specify `StorageClass` manifest
- It uses `Container Storage Interfase (CSI)` compliant driver
- Support for:
	- EBS
	- EFS (the only type supported with Fargate)
	- FSx for Lustre
	- FSx for NetApp ONTAP


#### Logging & Metrics

Enable logging for Control Plane to CloudWatch logs
Control Plane log type:
- API Server (api)
- Audit
- Authenticator
- Controller Manager
- Scheduler
Able to select exact logs types to send to CW

Nodes & Container logging
- Setup to capture node, pod & container logging to CW logs
- Use CloudWatch Agent 
- Use **Fluent Bit**, or **Fluentd** log drivers 
- container logs are stored on a Node directory:  `/var/log/containers`
- Finally, use CloudWatch Container Insights to get dashboard monitoring for nodes, pods, tasks, and services.
