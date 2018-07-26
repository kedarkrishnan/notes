# S3 - Simple Storage Service

- Object Storage Only
- File - 0 to 5TB
- Unlimited storage
- Files stored in Buckets (similat to folder)
- Universal namesace - Should be unique globally

#### Data Consistency
- Amazon Guarantee
	- 99.99 Build for availibility
	- 99.9% Availibility
	- 11 X 9s durability
- PUTS - Read after Write
- Overrides PUTS  / DELETE - Eventual consistancy
- S3 Object
	- Key = name
	- Value = data
	- VersionId = Versioning
	- MetaData = Data about data
	- Subresources - bucket-specific config
		- Bucket policies, ACL
		- Cross origin resource sharing: CORS
		- Transfer Acceleration: Accelerate transfer speed when uploading - Uses cloud front edge locations
	
#### Sorage Tires/ Classes
- S3 : durable, immediately available, frequestly accessed
- S3 - IA : durable, immediately available, **Infrequently accessed**
		- Low fees
		- Charge for retrival of data
- S3 - One Zone IA : same as IA, data stored in only one AZ
		- 11 X 9s durability
		- 99.5% availability
		- 20% cost less
- Reduces Redundancy Storage : easy to reproduce data
		- 99.99% durability
		- 99.99% avalibility
		- Used for data that can be recreated (thumbnails)
- Glacier : Archived data
		- very cheap
		- 3/5 hrs to restore

#### Charge for:
- Storage per GB
- Requests (GET,PUT, Copy)
- Storage managment
	- Data Managment pricing
- Transfer data out of S3

#### Access control
- S3 buckets - private by default
- Bucket policies
- ACL for objects inside a bucket
- Can create access logs - can be written to same or another bucket

#### Encryption
- In Transit (encryption over network)
	- SSL /TLS (HTTPS)
- At rest
	- Server side encryption
		- S3 managed keys: SSE-S3 = AES256
		- AWS key management service, manages keys: SSE-KMS
			- separate premission for an envelop key which protects the data's encryption key
			- gets audit trail when key is used
		- With custom keys - SSE-C	
	- Client side encryption
	 	- Customer encrypts the file

**Enforcing encryption on S3 bucket**

- S3 *bucket policy* to deny all PUT request which don't include the x-amz-server-side-encryption header 
	- SSE-S3 = x-amz-server-side-encryption:AES256
	- SSE-KMS= x-amz-server-side-encryption:ams:kms

#### Cross origin resource sharing: CORS
- Allowing resources in one S2 bucket to access resources in another S3 buckets
- Enable cors on the bucket in which the resources are being shared
	- Always use the s3 website url 
		... url contains - s3-website

# Cloud front
- Amazon's Content delivery network (CDN)	
	- Edge location - location where content is cache
		- you can Write to them
		- **Amazon S3 Transfer Acceleration** enables fast, easy and secure transfer of files over long distance between your end users and an S3 bucket - data is routed to Amazon s3 over an optimized network path
	- Origin - origin of file - S3 bucket, EC2, Elastic load balancer, Route 53, non AWS web server
	- Distrubution - name for CDN
		- Web distribution - Typically used for websites
		- RTMP - Used for media streaming
- Objects are cached for the life of the TTL (Time to live: default 24 hrs)
- Can clear cache object manually - invalidations - Will be CHARGED
- Signed URL / Cookie - Access restricted content	

#### Performance
- GET Intensive - Cloud front : CDN
- Mixed request - Avoid sequential key names use random prefix to key names - forces s3 to distribute your keys across multiple partitions, distributing the I/O 
