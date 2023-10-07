#### Status Checks
- Automated checks to identify hardware/software issues

Types:
- System Status Check
	- Issue with AWS hardware/software
	- Notified in AWS Health Dashboard
	- Resolution: Stop and Start instance to migrate to healthy host.
- Instance Status Check
	- Issue with software/network configuration of instance (invalid network config, exhausted memory)
	- Resolution: reboot instance/change instance config

CW Metrics & Recovery
- Separate metric for System and Instance

Recover Option 1: (Preferred)
- Trigger CW Alarm based on EC2 CW Metric and then trigger to recover EC2 and send notification

Recover Option 2: 
- Set up ASG with min/max/desired to 1 with health check. won't keep same IP, EIP