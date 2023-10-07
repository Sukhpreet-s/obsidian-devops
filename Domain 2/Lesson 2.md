Deploy automation to create, onboard and secure AWS accounts in a multi-account/multi-Region environment

Infrastructure as products

AWS Organizations
- Restrict user capabilities to access/use services, products..

Service Catalog
- managing and provisioning infrastructure as a product.
- backed by [[CloudFormation]] and can be used with [[CDK (Cloud Development Kit)]]

AWS Control Tower Account Factory can be used to provide multi-accounts access to use CI/CD pipelines.
AWS Control Tower Account Factory doesn't allow to create custom VPC on account creation. It does automatically delete the default VPC.

Can create custom VPCs and security controls using Service Catalog for each account.

Security controls at scale
- Config
- Control Tower - helps and governs AWS accounts
- Security Hub
- Detective
- GuardDuty - Threat detection service
- Inspector - automated security assessment service
- Service Catalog
- service control policies (SCPs)

