Automate Operations with Chef and Puppet
- use code to automate the configurations of your servers

### Stacks
Manage infrastructure, configuration, and application

OpsWorks apps have multiple layers:
- Load Balancer Layer
- Application Layer
- Database Layer

To deploy apps, define the:
- App repository
- Cookbook (how to deploy)

##### Lifecycle events (5 events)
- Setup (After instance booting)
- Configure 
	- Runs on <b>all</b> instances if:
		- an instance enters or leaves the online state.
		- associate/disassociate Elastic IP from an instance
		- attach/detach load balancer from an instance.
- Deploy
	- Runs when deploy command
	- Setup lifecycle also executes the Deploy cookbook
- Undeploy
	- when deleting an app or running undeploy
- Shutdown
	- Before terminating the EC2 instance
	- Will trigger Configure lifecycle on all instances.

Can specify cookbook for each event



### CloudWatch Events
Auto healing feature
- How unhealthy instances are detected?
	- Every instance have OpsWorks Stacks agent that communicates regularly with the service.
	- If the agent has not communicated for more than approx. 5 minutes, it is considered failed (unhealthy).
	- Then Auto healing will kick in.
	- Or send notifications using CloudWatch event rule