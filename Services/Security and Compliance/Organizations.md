
Root OU
- Management account
- contains another OU
- can have OU in OUs

OrganizationAcountAccessRole
- IAM role that grants the management account full access to the member account
- role is automatically added if the member account is created using AWS Organizations API.
- If inviting existing account to Organization, then must manully provide the role.



Multi Account Strategies
- Create separate accounts for per departments, per cost center, per dev/prod/test based on regulatory restrictions (using SCP)
- for resource isolation

Feature Modes:
- Consolidated billing feature
- All features (Consolidated billing feature and SCP)


Service Control Policies
- allow/restrict IAM actions
- applied at OU or Account level (does not apply to management accounts)
- applied to all users and roles in an account/OU including root user
- **SCP does not affect Service-linked roles** - Sevice-liked roles enable other services to integrate with Organizations
- must have explicit Allow