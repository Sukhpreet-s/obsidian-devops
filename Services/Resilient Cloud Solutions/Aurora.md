
### Replicas - Auto Scaling
- Writes go to only write endpoint (instance)
- and reads go to only read endpoint (instances)
- Read replicas can scale based on the CPU usage


### Global 
- Aurora Cross Region Read Replicas:
	- for disaster recovery
- Aurora Global Database (recommended):
	- 1 primary region (read/write)
	- upto 5 secondary regions, replication lag is <1 second.
	- upto 16 read replicas per secondary region
	- For disaster recovery, promoting another region RTO<1 minute

 
