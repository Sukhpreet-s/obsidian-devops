Define cloud infrastructure and reusable components to provision and manage systems throughout their lifecycle

### Configuration as Code

[[CDK (Cloud Development Kit)]] - defining cloud infrastructure and code. provision it through [[CloudFormation]]

Example: Create serverless app using CDK as well as Fargate.

### Infrastructure as Code

[[CloudFormation]]
- Stacks
- Chain sets
- permissions
- the template structure

Configuration tasks (configuration as code) sometimes can be easily configure with Chef or Puppet, [[OpsWorks]] would be helpful here.

#### Configuration management and strategies
- Control Tower
- Organizations
- Budgets
- Service Catalog
- Cost Explorer
- Proton
- Managed Grafana

Services used to provision resources and applications:
- [[CloudFormation]]
- [[OpsWorks]]
- Service Catalog

Services to operate and manage environments with speed and governance:
- CloudWatch
- CloudTrail
- Config
- Systems Manager
- Cost Explorer
- Proton
- Managed Grafana - to visualize operational metrics.
- Amazon Managed Services for Prometheus - to monitor containers