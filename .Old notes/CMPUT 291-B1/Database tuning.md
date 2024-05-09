![[Pasted image 20230307112024.png]]

*Tuning*: process of modifying an application, and adjusting the parameters of the underlying [[Databases|DBMS]], to improve performance.

Tuning does not effect the semantics of the system:
- Same info presented to users
- Same state after same operations

Aspects to consider:
- How to tweak relations?
- what indexes should be used?
	- Not in SQLite
- Hints to influence the query optimize
	- Not in SQLite
- *Performance measures*:
	- Response time
		- average time to wait for a response to a particular query.
	- Throughput
		- volume of work completed in a fixed amount of time (e.g., transactions per second, TPS).

# Performance Bottlenecks
- A table represents a performance bottleneck if:
	- rows are **wide** (many attributes), thus increasing I/O.
	- its **index** is **deep** (i.e., many rows), thus increasing I/O.
	- it is **heavily used**, causing **locking contention**.
- If some data in the table is *frequently accessed*, while other data may not:
	- Table partitioning:
		- Less I/Os.
		- Possible to access different partitions concurrently

# Horizontal Partitioning

- **Split rows**
	- *Geographically* (e.g., by province), *organizationally* (e.g., by department), *active/inactive* (e.g., *current students vs. alumni*). Useful when accesses are confined to disjoint subsets of rows.

- **Advantages**
	- Rows in a typical result set are concentrated in *fewer pages*.
	- Indexes have *fewer levels* (however, only marginally).
	- *Better* use of caching.
	- *Reduces contention* (in particular if tables can be spread over different devices).

- **Disadvantages**
	- Added *complexity*.
	- *Difficult* to *handle queries* over all tables.

## Horizontal Partitioning in Oracle
Methods: range, hash, list, etc. Example:
```sql
Create table transcripts (  
	StudId char(6),  
	CrsCode char(8),  
	Semester char(3),  
	Grade int,  
	Primary Key (StudId, CrsCode, Semester))  
Partition BY LIST (Semester) (  
	Partition p10 values (‘F10’, ‘W10’),  
	Partition p11 values (‘F11’, ‘W11’),  
	Partition rest values (default));
```

# Vertical Partitioning
- *Split columns* in partitions and *replicate the key* across partitions. Conceptually the same as decomposition (c.f., normalization).

- Useful when a table has many columns and when:
	- it is possible to *distinguish between frequently and infrequently accessed* columns
	- different queries use *different subsets* of columns

- E.g.: Split Employee(sin, department, skills, salary, tax, benefits) table into:
	- *Compensation(sin, salary, tax, benefits)* and *Job(sin, department, skills)*.
	- **Decomposition is (and must always be) lossless** (sin is included in both tables), but a join is required to reconstruct the entire table.

# Indexes
- **Advantages**: fast table access (for search, insert, delete, join, constraint checking).

- **Disadvantages**: storage overhead; might significantly increase the processing time of statements that modify the database.

- For some DBMSs when maximizing the performance of queries, the application programmer might have to “*encourage*” it to use *appropriate indexes*. (Not applicable to SQLite)

- Can be created:
	- Automatically, on primary key
	- Manually, on other columns

![[Pasted image 20230307112601.png]]

## Index Covering
- An index *covers* a query if:
	- the query can be *computed from the index alone*
- *All attributes* of the query must be *included in or computed from a covering index*.
- Index must be *dense*.
![[Pasted image 20230307113836.png]]
![[Pasted image 20230307113848.png]]
## Choosing an Index – Example 1

![[Pasted image 20230307113905.png]]
![[Pasted image 20230307113916.png]]
