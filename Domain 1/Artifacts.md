The built app

Repositories for artifacts:
- CodeArtifact
- S3
- ECR - Elastic Container Registry

Securing the pipeline of committing code to master (CodeCommit)
- Create IAM roles for the Leader/Manager with full access
- Create IAM role for the Team that restricts Push, Delete and Merge APIs.

Automate EC2 and container images build processes
- EC2 Image Builder
	- Fully managed
	- Automates the creation, management, and deployment 
	- Integrates with AWS Resource Access Manager to manager shared resources.
	- AWS Organizations
	- 