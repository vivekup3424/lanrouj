---
tags:
  - database
  - system-design
  - replication
  - leader
---
## Types of Replication
- **Single Leader** 
	- All writes go into the singular master database
	- Master database sends list of writes to other slave databases using replication logs
	- Reads can come from any database
	
  ![[Pasted image 20250702235648.png|500]]
	- Methods for increasing avalibility insite this setup
		- Increasing the number of follower nodes
		- Handling Master crashing 
		- Handling Slave crashing
- Multileader
- Leaderless