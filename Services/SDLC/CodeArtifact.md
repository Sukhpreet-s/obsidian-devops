
Stores all the packages used by the application within VPC.
For downloading dependencies, CodeArtifact acts as proxy to fetch the dependency from the public repo and store in AWS repo.

EventBridge integration (like package version updated)
- Trigger other services


Access authorization (Same account access/Cross-account access):
- Artifacts under same account can be accessed by any user, services, roles in the same account using IAM policies.
- To grant access to user outside your account, use Resource Policy.
	- Can only provide access to either all packages or none.


CodeArtifact Domain are used to manage repositories between multiple accounts.
