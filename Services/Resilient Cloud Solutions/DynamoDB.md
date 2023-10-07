Fully managed
highly available
cross AZ capability
NoSQL with transaction support 
easily scalable to massive workloads, distributed environment
Fast and consistent in performance (single-digit millisecond)
low cost and auto scaling capabilities
No maintenance, always available
2 Options for tables:
- Standard
- Infrequent Access (IA)
Max size of an item is 400KB
combination of partition key and sort key makes the primary key
Supported data types:
- Scalar Types: String, Number, Binary, Boolean, Null
- Document Types: List, Map
- Set Types: String Set, Number Set, Binary Set
**Can rapidly evolve schemas**


#### Read/Write Capacity Mode
- Provisioned Mode (default) 
	- Need to specify number of read/writes per second
	- pay for provisioned Read Capacity Unit/ Write Capacity Unit
	- still allows auto scaling the RCU/WCU based on the load
- On-demand Mode
	- auto scaling read/write based on load
	- No capacity planning
	- pay for what you use (expensive)
	- Great for <u>unpredictability</u>, <u>steep sudden spikes</u>


### DynamoDB Accelerator (DAX)
- Fully managed, highly available, In-memory Cache DB
- Specifically to solve problem with read congestion of DynamoDB by caching
- <u>Microsecond</u> latency for cached data
- Preference
	- DAX - for individual object cache, query & scan cache
	- ElastiCache - for storing aggregation result (heavy computation)

### DynamoDB Stream Processing
- Ordered stream of item-level modification in a table.
- Use cases:
	- react to changes in real time
	- real-time usage analytics
	- implement cross-region replication
- Types:
	- Streams
		- 24 hours retention
		- Limited # of consumers
		- process using Lambda Triggers, DynamoDB Stream Kinesis Adapter
	- Kinesis Data Stream
		- 1 year retention
		- higher # of consumers
		- 

### DynamoDB Global Tables
- 2 way replication (active-active)
- requires Streams
### DynamoDB TTL

- Automatically delete items in table using TTL (expiry time)

### Backups for disaster recovery
- Continuous backups using PITR (point in time recovery)
	- optionally enabled for last 35 days
	- PITR to any time within the backup window
	- recovery the process create new table
- On-demand backups

### Integration with S3
- Export to S3 (must enable PITR)
	- doesn't affect read capacity
	- works for any point of time in last 35 days
	- perform data analysis on top of DynamoDB
	- Retail snapshots for auditing
	- ETL on top of S3 data before importing back into DDB
- Import from S3
	- import as CSV, DDB JSON or ION format
	- Doesn't consume write capacity
	- creates new table
	- import errors are logged in CW logs
