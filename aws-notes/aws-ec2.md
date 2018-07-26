# EC2

- on Demand
	- low cost and flexibility
	- pay by hour or by sec
	- applications with short term spikes, unpredictated workloads
	- application developed or tested on Amazon EC2 for first time

- Reserved Instances
	- offers significant discount on the hourly charge
	- contact 1 or 3 years
	- application with steady state or predicated usage
	- application that require reserved capacity
	
- Spot Instances
	- enables you to bid
		- Say you bid for 100 and price goes to 90 you are provisioned instances then the prices go back up to 150 the instances are terminated
		- if AWS terminated - you will not be charged for partial hour of usage
		- if you terminate it, you will be charged for full hour
	- flexible start and end time
	- users with urgent needs for large amount of addtional capacity

- Dedicated hosts
	- regulatory requirement
	- physical EC2 servers
	- licensing which does not support multi-tenancy 

> Ec2 Instance Types: FIGHT DR MC PX
	
### EBS - Elastic block storage 
-	Disk in cloud which is attached to EC2 instances
	
- EBS Volumne types
	- General purpose SSD (GP2)
		- 3 to 10,000 IOPS
	- Provisioned IOPS SSD (101)
		- more than 10,000 IOPS
		- I/O intensive apps RDBMS or NoSQL Db			
	- Magnetic
		- Throughput Optimized HDD (ST1)
			- Cannot be a boot volume
			- Sequential writes
			- Big data, data warehouse, log processing
		- Cold HDD (SC1)
			- lowest price, infrequent accessed workloads
			- File serverce 
			- Cannot be boot volume
		- Magnetic (Standard)
			- Legacy
			- lowest cost bootable volume	
- You cannot mount 1 EBS volume to multiple EC2 instances use EFS(block based storage) 

- Termination protection is turned off by default
- on EBS-backed instances default action is for the root EBS volume to be deleted when instance is terminated
- EBS root volume 
	- Default AMI cannot be enrypted
	- You can use third party tools for encryption or can encrypt - taking snapshot of the volume - create a copy of that snap with encryption - deploy the encrypted root device volume
- Additional volume can be encrypted using console, CLI or API

> Volumes will **ALWAYS** be in the same availability zone as the EC2 instance

- You can change ESB volume on the fly - size, storage type
- Snapshots exist on S3, but you cannot see them
- Snapshots are incremental
- Snapshots of encrypted Volume are encrypted automatically
- Volumes restored from encrypted snapshot => encryted
- Share snapshots = should **NOT** be encrypted. Can be shared with other account or made public

#### Move Volume 

- Move EBS Volume - different AZ : 
	- Create snapshot - create volume from snapshot
- Move EBS Volume - different Region: 
	- Create snapshot - copy snapshot to different region - create volume from snapshot
	- Create snapshot - create image from snapshot - Copy image to different region - create instance from image
	- Create image from the instance - Copy the image to a different region

#### Security groups
- Changes to security groups effects immediately
- All inbound traffic is blocked by default
- All outbound traffic is allowed by default		
- You can have any number of EC2 instances within a security group
- You can have multiple security groups for a EC2 instance
- Security groups are statefull	(Network Access Control Lists are stateless)
	- When you add an inbound rule outbound rule is automatically addedd
- You **cannot** block specific IP addresses using security groups instead use Network Access Control Lists
- You can specify allow rules, but not deny rules

#### CLI
- Least Privilege
- Create groups - assign users to groups
- Group permisson are assigned using policy documents
- Secret Access key 
	- seen only onces. 
	- Else Delete the access key and regernerate
	- run aws configure again to set the new access key and secret key
- Dont use just one access key - One key pair per developer
- You can use CLI on your PC			

***Commands***

- aws configure
- aws ec2 describe-instances
- aws ec2 describe-images
- aws ec2 run-instances - CREAT/ LAUNCH INSTANCES
- aws ec2 start-instances - START INSTANCE
- aws ec2 terminate-instances

- aws s3 ls - LIST
- aws s3 mb s3://<bucket name> - MAKE BUCKET
- aws s3 cp <file> s3://<bucket name> - upload File	
- aws s3 ls s3://<bucket name> - LIST inside a bucket
	
### Elastic Load Balancer

- Application Load Balancer
	- Operate at layer 7 
	- application aware
- Network Load Balancer
	- Operate at layer 4
	- TCP traffic
	- Extreme performance
- Classic Load Balancer (Elastic load balancers)
	- Legacy
	- Operate at layer 4 / 7
	- Application stops responding load balancer throws 504 (Gateway timeout) 	
	- load balance HTTP / HTTPS using X-Forwarded and sticky sessions
	- X-Forwarded-For => Gives IPV4 address of your end user
	