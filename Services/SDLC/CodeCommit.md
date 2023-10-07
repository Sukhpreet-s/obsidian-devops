Authentication
- SSH 
- HTTPS

Authorization
- IAM policies

Encryption


Can use EventBridge to run stuff based on events:
- react to pullRequestCreated a...

##### Cross-Region Replication repo
- Use case: achieve lower latency pulls for global developers, backups
- Create EventBridge event to invoke ECS Task on referenceUpdated event
- ECS Task run git clone on the server and use `git remove set-url --push origin {origin}` to push it to the CodeCommit on different region.

Branch Security
- Use IAM policies to restrict user to push or merge code to specific branch

Pull Request Approval Rules

