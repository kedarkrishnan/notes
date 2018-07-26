# IAM
> IAM is universal. It does not apply to regions

- Root account is the account created when you setup AWS account. It has the complete Admin.
- New users have No permissions when first created
- Access Key Id and secret access key used to communicate using sdk or console.

- Users
- Groups
- Roles => apply to resources 
	- Ec2 instance to access S3
	- Roles allow you not to use Access Id's and Secret Access keys
	- Roles are always preferred
	- Roles are controlled by policies
	- You can change policy on a role and take IMMEDIATE affect
	- You can ATTACH and DETACH roles without stoping EC2 instances
- Policies = permissions

### Security Token Service - STS
- Federation
- Federation with mobile apps
- Cross Account Access

#### Terms

- Federation: Combine list of users from one service with list of users with other service

- Identity Broker: service to take identity from point A and join it (federate it) to point B
	- Does not come out of the box. Have to **develop your own identity broker**
	
- Identity Store: Service like Facebook, Active Directory, Google

- Identities: a user of a service like facebook	

- Arn: Amazon resource name

> Identity broker checks with LDAP first then with AWS STS
