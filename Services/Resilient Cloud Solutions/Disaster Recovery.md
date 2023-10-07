RPO - Recovery Point Objective - how back in time can you go and backup/restore
RTO - Recovery Time Objective - how quickly can you recover.

more expensive 1 -> 4
better reduced RPO and RTO 1 -> 4
### 1. Backup and restore

create snapshots
backup on-premises data on cloud (Storage Gateway, Snowball)

### 2. Pilot Light

Only have critical part running on cloud (separate region). Database (with continuous data replication)
Spin up other stuff on disaster. EC2.

### 3. Warm Standby

full system running, at small scale.
on disaster, scale to prod.

### 4. Host Site / Multi Site Approach

duplicate prod architecture to another region