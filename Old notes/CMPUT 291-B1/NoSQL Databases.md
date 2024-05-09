# NoSQL != No SQL
- Not only SQL: umbrella term for data stores that do not follow [[The Entity-Relationship Model|RDBMS]] principles:  
	- Focus on distributed storage and computing. Goal: deal with huge datasets (big data)  
	- Data may not be relational  
	- Schema may not be available (too restrictive)  
	- SQL may or may not be used  
	- BASE consistency model (much looser than ACID): prioritize availability over consistency.

# ACID
- Set of properties of database transactions: guarantee validity even in the event of errors,  power failures, ...  
	- *Atomicity*  
		- Transactions seen as “atomic” work units: they either succeed or fail.  
	- *Consistency*  
		- The database is always moved from one consistent state to another (through transactions), according to all defined rules.  
	- *Isolation*  
		- Transactions that execute concurrently are guaranteed to leave the database in a consistent state as if they were executed sequentially.  
	- *Durability*  
		- Committed transactions cannot be lost (e.g. due to power failure).
# BASE Consistency Model
- *BA*sic availability  
	- Database available most of the time  
- *S*oft state  
	- Stores and replicas may not be consistent  
- *E*ventual consistency  
	- Stores may not have the latest updates  
		- common in distributed systems

**Trades consistency (which is expensive!) for high availability. Goal: tolerate network partitioning.**

![[Pasted image 20230321112037.png]]

![[Pasted image 20230321112050.png]]
# NoSQL Systems
![[Pasted image 20230321112113.png]]
- Key-value stores
- Wide column stores
- Document stores
- Graph data stores
- Map-reduce
- ...

# Key-Value Stores
![[Pasted image 20230321112952.png]]
![[Pasted image 20230321113002.png]]
![[Pasted image 20230321113013.png]]
![[Pasted image 20230321113021.png]]

# Document Store
![[Pasted image 20230321113126.png]]
![[Pasted image 20230321113134.png]]
![[Pasted image 20230321113145.png]]
![[Pasted image 20230321113154.png]]
![[Pasted image 20230321113256.png]]

## Example
![[Pasted image 20230321113216.png]]
![[Pasted image 20230321113229.png]]
# Graph Databases
![[Pasted image 20230321114701.png]]
![[Pasted image 20230321114712.png]]
![[Pasted image 20230321115318.png]]
![[Pasted image 20230321115343.png]]
![[Pasted image 20230321115408.png]]
