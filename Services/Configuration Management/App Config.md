Keep app configuration outside of app
Deploy dynamic configuration 
Able to gradually deploy config change and rollback if issue
Able to validate the config before deploying 

Flow:
- Deploy new configs to AppConfig
- EC2 will listen for config changes
- triggers CloudWatch Alarm if issue
- Rollbacks the config in AppConfig 