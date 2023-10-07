successor to Single Sign On

- provides one login to
	- access multiple accounts in Organizations
	- business cloud application
	- EC2 windows instances
	- SAML 2.0 enabled applications

Permission Sets - Specify list of access for users
- Multi-Account Permissions - give access to accounts
- Application Assignments - give access to SAML enabled applications
- Attribute-Based Access Control
	- allows to associate tags with users created in IAM identity center
	- create permission sets once and then use tags to provide permissions to resources
	- use case: assign tag to resource to have same tag as the user for user to access it


External IdPs
- use external Identity Providers to authenticate users
	- Must create users and groups in IAM center identical to the ones in external IdP.
- SCIM System for Cross-domain Identity Management
	- automate the process to creates/manages identities in IAM identity center from external IdPs.