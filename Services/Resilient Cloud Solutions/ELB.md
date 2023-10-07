
Listener Rules
- Can create multiple rules for load balancing 
- Supported actions: forward, redirect, fixed-response
- Rule conditions:
	- host-header
	- http-request-method
	- path-pattern
	- source-ip
	- http-header
	- query-string

Target Group Weighting
- Traffic routing % (Blue/Green deployment)
- Specify target groups

DualStack Networking
- LB will automatically resolve whether to use IPv4 or IPv6.
	- Specify which target group allows IPv4 and which allows IPv6 for routing to the correct target

Privatelink Integration
- Problem: Connecting 2 VPCs with overlapping IPs (VPC Peering will not work)
- Solution: 
	- expose NLB from one VPC
	- enable PrivateLink in the other VPC, it will create VPC Endpoints
	- the VPC with PrivateLink can communicate with the other VPC through those VPC Endpoints.