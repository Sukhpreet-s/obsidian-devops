Infrastructure as code is further split into:
- Configuration management as code
- Policy as code
Infrastructure as products

Methods and strategies to interact with software-defined infrasturcture:
- Systems Manager, Config
	- Used to automate system inventory, configuration and patch management
- SDKs, Lambda and Step Functions
	- automations for complex scenarios
- OpsWorks, State Manager
	- used to set configuration of software applications to desired state.

Solution to automate tasks and processes:
##### Solution to protect and encrypt sensitive data and improve cache hit ratio for CloudFront distribution
- HTTPS secures the end-to-end connection
- Field level encryption to securely upload user-submitted sensitive info to servers.
- Increase the proportion of your viewers requests that are served from the CloudFront edge caches. Add Cache-control max-age directive to objects in S3 with longest practical value for max-age


##### Migration to AWS solution:
AWS Application Discovery Service - helps to plan migrations by collection usage and configuration data and integrates with AWS Migration Hub.

Using Application Discovery Service APIs, export system performance and utilization data for discovered servers and input the data to cost model to compute the cost of running your on-premise servers on AWS.

Can also export network connections and process data to understand the network connections that exists between the servers to determine network dependencies and group them into applications for migration planning. 

Agentless Discovery Connector, OVA file and deploying that to vCenter ????

Agent Based Discovery is Windows and Linux only.
It is a VMware appliance

Service Catalog can't integrate with on-premise VMware servers

More effort - to install Systems Manager on on-premise and EC2 servers.


##### Requirement to monthly audit all EC2 instances and send system details log reports to S3

Use Inspector? It is a security vulnerability service 
Can install Systems Manager Agents to each instances to send logs to CloudWatch. Systems Manager requires to connect to each instance to view the logs
Best solution: Use(install) CloudWatch Agents