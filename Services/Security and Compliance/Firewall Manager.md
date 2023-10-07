Manage multiple rules for all resources in all accounts of Organization

Security policy:
- WAF rules
- AWS Shield Advanced
- Security Groups for EC2, ALB, ...
- Network Firewall
- Route 53 Resolver DNS Firewall
- policies are created at region level

Rules are automatically applied to newly created resources in policy is present.


Policies types:
- WAF - able to specify whether to auto remediate issues or no
- Shiedl Advanced: option to view only compliance or auto remediate as well.
- Security Group Policy Type:
	- Common Security Groups - apply SGs to all EC2 instances
	- Auditing of Security Group Policy - check and manage SGs rules in all accounts
	- Usage Audit Security Group Policy - monitor unused and redundant SGs and perform cleanup
- Network Firewall
	- Distributed - one in each VPC
	- Centralized - one overall
- Route 53 Resolver DNS Firewall - manages associations between DNS firewall rule groups and VPC