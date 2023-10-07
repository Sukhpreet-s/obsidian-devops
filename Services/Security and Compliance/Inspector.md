Automated Security Assessments

For EC2
- uses SSM agent
- analyze against unintended accessiblity
- analyze the running OS against know vulnerabilities
For Container Images push to ECR
- assessment of the container image
- as they are pushed
For Lambda Functions
- software vulnerabilities in function code and package dependencies
- as they are deployed

Reporting & integration with AWS Security Hub
Sends findings to EvenBridge


What does it evaluate?
- It is only for EC2, container images and lambda functions
- continous scanning of infrastructure only when needed
- packages (EC2, ECR, Lambda) - database of CVE
- network reachability (EC2)
- A risk score is associated to all vulnerabilities.