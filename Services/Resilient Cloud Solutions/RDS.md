#### Read Replicas
- upto 15 replicas
- within AZ, cross AZ, Cross Region
- ASYNC - read are **eventually** consistent
- can be promoted to its own database
- Use case:
	- Run some analytics on the read replica to not affect the performance of the original database 
- RDS replication across AZ within same region has no cost, but cross region does.

#### Multi AZ (Disaster Recovery)
- SYNC replication
- One DNS name - automatic app failover to standby
- Increase availability 
- On failover, the replica is promoted to be the primary database.


#### Single AZ -> Multi AZ
- Zero downtime operation
- "Modify" the database and enable multi AZ.
- How it is created in the backend?
	- A snapshot of OG is created 
	- The new DB is restored using that snapshot in new AZ
	- Sync is established 