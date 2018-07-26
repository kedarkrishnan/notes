# Relational Database Service

- Types of RDS - OLTP
	- SQL Server
	- Oracle
	- MySQL Server
	- PostgreSQL
	- Aurora (Amazons own flagship db, compatible with MySQL)
	- Maria DB

- No SQL - DynamoDB

- RedShift - OLAP

- Elasticache - In Memory caching
	- Memcached
	- Redis


### Backups
- Automated
	- retention period 1 to 35
	- fully daily snapshot and stores transaction logs for the day
	- recovery to a point in time down to a second within the retention period 
		- when doing DR will choose the most recent daily back up and apply transaction logs relevant to the day
	- enabled by default
	- stored in s3, free storage space equal to the size of your database	
	- during backup window storage I/O may be suspended hence may experience latency	
	- deleted when RDS instance is deleted
- Snapshots
	- manually done
	- stored even when RDS instance is deleted
- Restoring backup
	- restored version of db will be a new RDS instance with a new DNS endpoint
- Encryption
	- MySQL, SQL Server, PostgreSQL, MariaDB & Aurora
	- Done using aws key management system (KMS)
	- RDS encrypted => data stored, automatic backups, read replicas and snapshots - encrypted
	- Enrypting existing DB NOT supported
			- Create a snapshot
			- Make a copy of snapshot
			- Encryt the copy

### Multi AZ
- **Used for DR - disaster recovery**
- Exact copy of the DB in another availability zone
- Aws handels the deplication - write automatically syncronized to stand by DB (Syncronous)
- Always use DNZ endpoint and not the IP addresses as the DNS would failover automatically to the secondary DB
- MySQL, SQL Server, PostgreSQL, MariaDB, **Oracle** & Aurora(built in db design, dont need to turn on multi AZ)

### Read Replica
- **Increase performance enhancement / scaling**
- read-only copy , Achived using Async replication
- must have automatic backup turned on
- Can have upto 5 read replicas
- Can have read replicas of read replicas
- **Can be multi AZ**
- **Can be promoted to become its own DB. Will break the replication**
- **Can be in different region then the DB**
- MySQL, PostgreSQL, MariaDB, Aurora

### Elasticache
- Improves latency and throughput for many read-heavy application workloads
- types:
	- Memcached
		- Object caching - offload a database
		- Simple caching model
		- Large cache nodes, require multithread performance with utilization of multiple cores
		- Ability to scale your cache horizontally as you grow (Scale out)
	- Redis 
		- Advance data types like lists, hashes and sets
		- Sorting and ranking in memory like leaderboards
		- Persistance of your key store
		- Run in multi AZ with failover
		- Pub/Sub capabilities
	
	` Dataware housing type requirement (OLAP) use Redshift`	
