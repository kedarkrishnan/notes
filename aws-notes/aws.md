- [Elastic Compute Cloud - EC2](./aws-ec2.md)
- [Route53](./aws-r53.md)
- [RDS](./aws-rds.md)
- [S3 - Simple Storage Service](./aws-s3.md)
	- [Cloudfront](./aws-s3.md#cloud-front)
- [IAM - Identity Access Managment](./aws-iam.md)

# AWS Developer Associate
- [AWS Infrastructure](#aws-infrastructure)
- [Compute](#compute)
- [Storage](#storage)
- [Databases](#databases)
- [Networking & Content delivery](#network--content-delivery)
- [Management Tools](#management-tools)
- [Analytics](#analytics)
- [Security & Identity & Compliance](#security--identity--compliance)
- [Application Integrations](#application-integrations)

## AWS Infrastructure

#### Regions, AZ, Edge locations
- Regions 
	- Geographical distinct regions
- Avalibility Zones (AZ) 
	- Discrete data centers inside a region 
	- Atleast 2 avalibity zone
- Edge Locations 
	- Amazons CDN 
	- Caching data 

## Compute
#### [Elastic Compute Cloud - EC2](./aws-ec2.md)
-	Virtual machines
-	Dedicated machines

#### EC2 cloud container 
- Run and manage Docker container

#### Elastic beanstalk 
- Upload and run the code

#### Lamdba
- Control when it executes
- Dont have to worry about underlying virtual machines

#### Lightsail
- Virtual Private Service (VPS)
- Provisions a server and gives a fixed IP address
- Which can be access using RDP - Remote Desktop for windows or SSH for linix
- Gives a managment console

#### Batch
- Batch computing

## Storage
#### [S3 - Simple Storage Service](./aws-s3.md)
- Object based storage

#### EFS - Elastic file system

#### Glaicier
- Data archive

#### Snowball
- Migrating large about of data into cloud

#### Storage gateway
- Virtual appliances replicating data to S3

## Databases
#### [RDS](./aws-rds.md)
- Relational database

#### Dynamo DB
- Non Relational database

#### Elasticache
- Caching service for database

#### Red Shift
- Datawarehouse
- Business Intelligence

## Migration

#### AWS migration hub
- Tracking service track integration

#### Application discovery Service
- Tracking dependencies

#### Database Migration Service
- Migrate databases from on-prem to aws

#### Server migration service
- Migrate server to aws

#### Snowball
- Migrating large about of data into cloud

## Network & Content delivery
#### VPC - Virtual Private Cloud
- Virtual data center
- Configure firewall, acl

#### [Cloudfront](./aws-s3.md#cloud-front)
- Amazon's content delivery network

#### [Route53](./aws-r53.md)
- Amazon's DNS Server

#### API Gateway

#### Direct Connect
- Dedicated line from datacenter directly to Anazon's VPC

## Developer Tools
#### CodeStar
- Collabarating with other deveopers

#### CodeCommit
- Store code

#### CodeBuild
- Compile, run test, produce deployable package

#### CodeDeploy
- Deploy code to EC2, on Premises , lamda etc

#### CodePipeline
- CDS

#### X-Ray
- Analyse and debug code

#### Cloud9
- IDE environment

## Management Tools
#### CloudWatch
- Monitoring Service

#### CloudFormation
- Way of scripting infratructure

#### CloudTrail
- Log changes to AWS environment
- Stores records for 1 week
- Turned on by default

#### Config
- Monitors config of entire AWS environment

#### OpsWorks
- Chef and puppet - Automating environment, config

#### Service Catalog
- Managing group of IT Services that are approved to use on AWS
- Used for Govenance and complience requiremnets

#### Systems Manager
- Managing AWS resources
- Typically EC2 services for patching etc

#### Trusted Advisor
- Gives advice around multiple diciplines like Security, ports open, not using aws services as much as you can

#### Manage Services
- Manage service for your cloud

## Media Services
#### Elastic Transcoder
#### Media Convert
#### Media Live
#### Media Package
#### Media Store
#### Media Trailor

## Machine Learning
#### SageMaker
- Deep learning

#### Comprehend
- Centiment analysis

#### DeepLens
- Physical piece of hardware; artificially aware camera

#### Lex
- Amazon Alexa service

## Machine Learning

#### Polly
- Takes text and turns it into speech

#### Rekognition
- video & picture

#### Amazon Translate
- Traslate english into other languages

#### Amazon Transcribe
- Automatic speech recognition; speech into text

## Analytics
#### Athena
- Run SQL queries in the S3 buckets

#### EMR - Elastic map reduce
- Processing large amount of data

#### Cloud Search

#### Elastic Search Service

#### Kinesis
- Ingesting large amount of data into AWS like social media feeds, tweets, hash tags

#### Kinesis Video Streams

#### QuickSight
- Business intelligence tool

#### Data pipeline
- Moving data between services

#### Glue
- ETL: Extract Transform and Load


## Security & Identity & Compliance
#### [IAM - Identity Access Managment](./aws-iam.md)

#### Cognito
- Authentication service to give temporory access to AWS using mobile devices

#### Guard Duty
- Monitors malaciious activities on AWS account

#### Inspector
- Install on EC2 instances to check for vurnalabilities

#### Macie
- Scan S3 bucket for Personally Identifiable Information and give alert 

#### Certificate manager
- Managing SSL certificates

#### CloudHSM - Hardware security module
- Dedicate hardware to store keys to access EC2 instances and other encryption keys 
 
#### Directory Services
- Itegrating microsoft directory services with AWS

#### WAF - Web application firewall
- Stops SQL injection, CSRF etc

#### Shield
- Prevents DDOS (Distributed Denial of Service) attack

#### Artifact
- Portal to access and download AWS compliant reports
- Manage select aggrements

## Mobile Services
#### Mobile Hub
- Managment console for mobile applications

#### Pinpoint
- Target push notifications

#### AWS AppSync
- Updates data in web and mobile application

#### Device Farm
- Testing apps on real life devices

#### Mobile Analytics

## AR/VR - Augmented reality and Virtual reality
#### Sumerian

## Application Integrations
#### Step Functions
- Managing different Lamda functions

#### Amazon MQ
- Message queue

#### SNS - Simple Notification Service

#### SQS - Simple Queue Service

#### SWF - Simple Work Flow

## Customer Engagement
#### Connect
- Contact Center as a service, call center in the cloud

#### Simple Email Service

## Business Connectivity
#### Alexa for Business
 - Reorder ink, alert IT printer is broken etc
 
#### Chime
- Video conferencing

#### Work Doc
 
#### Work Mail

## Desktop and App streaming
#### Workspaces
- VDI solution, operating system in the cloud

#### AppStream 2.0
- Similar to Citris
 
## Internet of Things
#### iOT 

#### iOT Device Management

#### FreeRTOS
- Opearting system for micro controllers

#### Greengrass
- Software to let you run local compute, messaging, data cache, machine learning interface capabilities for connected devices in a secure way 
 
 
## Game Developer
#### GameLift
- Service to develop games
