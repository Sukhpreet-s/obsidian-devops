Managed Redis or Memcached
In-memory database
reduce load off of database
Using involves heavy application code changes

### Solution Architecture
#### DB Cache
- App tries to find required resource with ElastiCache 
- If found, returned to client. (quick)
- Else grap the data from the database.
- Store it in the Cache for later.
#### User Session
- User signup
- Store user session in Cache
- When application uses another instance for another request, it retrieves the session data from Cache, keeping the user logged in.



#### Redis (good availability and backup feature, safe)
- Multi AZ with auto failover
- Read replicas for high availability
- Data durability with AOF persistence
- Backup and restore features
- Supports Sets and Sorted Sets
#### Memcached (must be able to live if data lose, not safe but fast)
- Multi-node for partioning of data (sharding)
- No high availability
- Non persistent
- No backup and restore
- Multithreaded architecture

### Replication

##### Cluster Mode Disabled
- 1 primary node, up to 5 read replicas
- primary node for both read/write, replicas only for read (scaling option 0-5)
- on failover, one of the read replica takes over
- ASYNC replication
- Scaling:
	- Horizontal
		- up/down number of replicas
	- Vertical
		- Scale up/down node size
##### Cluster Mode Enabled
- partitioned across multiple shards.
	- Total number of nodes available : 500
- data will be split into all the shards
- each shard will have 1 master node
- each shard can have 0-5 read replicas.
- multi AZ option 
- AutoScaling
	- automatically increase/decrease number of shards or replicas
	- Supports **Target Tracking** and **Scheduled Scaling Policies**
	- Use CloudWatch metrics to trigger the CW Alarm to scale the ElastiCache
	- Use Cluster's `Configuration Endpoint`  to modify ElastiCache


#### Connection Endpoints
- Cluster mode enabled
	- Primary Endpoint: for all write operations
	- Reader Endpoint: evenly split across all read replicas
	- Node Endpoint: for read operations
- Cluster mode disabled
	- Configuration Endpoints: For all read/write operations
	- Node Endpoint: for read operations