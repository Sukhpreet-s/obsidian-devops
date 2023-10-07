Web application firewall

- can be deployed on ALB, API Gateway, CloudFront, AppSync
- it is not for DDoS protection
- allows to define web ACL (Access Control List)

Managed Rules
- Baseline Rule Groups: Common rule set  for general protection
- Use-case Specific Rule Groups: protection for specific use cases (SQL, PHP, Windows, WordPress)
- IP Reputation Rule Group: block request based on source (malicious IPs)
	- AWSManagedRulesAmazonIpReputationList
	- Bot Control Managed Rule Group - block and manage requests from bots.

Logging
send logs to:
- CloudWatch logs - 5MB per second
- Simple Storage Service - 5 minute interval
- Kinesis Data Firehose - limited by firehose quotas

