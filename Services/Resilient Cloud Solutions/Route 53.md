
### Record Types

- A - maps a hostname to IPv4
- AAAA - IPv6
- CNAME - maps a hostname to another hostname
	- Target domain name must have A or AAAA record
	- can't create for DNS namespace 
- NS - Name servers for hosted zone

##### Hosted Zones
- Public
- Private

##### Routing Policies - Weighted
- Control % of the request to each resources
- Used for load balancing between regions, testing...
- Assigned weights are relative to each other and 
	- traffic = weight for specific / sum of all weights

##### Routing Policies - Latency
- Redirect to the resource that is the closest
- Latency is based on traffic between users and AWS Regions.
- can be associated with health checks

##### Routing Policies - Failover (Active - Passive)
- Setup Health check for the first DNS connection to instance
- If heath check fails, then use the second DNS connection to another instance