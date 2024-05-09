# Supported Search Operations
Equality searches and range searches
- If data is stored in a heap file:
	- Linear scan: O(F) I/Os.
- If data was stored in a sorted file:
	-  Can use binary search: O(log2 F) I/Os
- can we reduce the cost further?

# Index File – simplified version
![[Pasted image 20230216110920.png]]
*Lame approach, binary search through ALL records. Reads and searches through a lot of data.*
*Better: Binary search over indexes instead of over actual data. Reads and searches through less data. Every set of records is identified by an index.*
# Multilevel indexing
![[Pasted image 20230216110951.png]]
*If we have an large set of nested indexes, (1 index talking to 1000 indexes, each of them talking to another 1000 indices) we can run binary search on the tree instead of on the entire set of data. Improves efficiency.*
***POINTERS TO POINTERS TO ...... TO DISK DATA***
**All non-leaf pages only direct you to the location of the desired value and don't hold any value themselves. Data is ONLY stored in leaf node.**
*Tree in main memory, leaf nodes (data) in disk*
# Searching the Index
![[Pasted image 20230216111021.png]]
![[Pasted image 20230216111039.png]]
![[Pasted image 20230216111138.png]]
*Bigger fan out with same height can accommodate more values. More values stored for the same height.*
# Tree Index Example
![[Pasted image 20230216113102.png]]
*Start at root, look at reach index closest to but less than our goal, get all data after.*

# B+ Tree
![[Pasted image 20230216113801.png]]
# Inserting a Data Entry into a B+ Tree
1. Find correct leaf node
2. Add index entry to the node
3. If enough space, done!
4. Else, split the node
	- Redistribute entries evenly between the current node and the new node
5. Insert <middle key, ptr to new node> to the parent: if not enough space in the parent, go to Step 3.

![[Pasted image 20230216114015.png]]
*Insert 40 works fine. When we want to insert values into a full leaf node, we need to split it somehow.*
# Split Policy
![[Pasted image 20230216114045.png]]
![[Pasted image 20230216114319.png]]
# Deleting a Data Entry from a B+ Tree
- If deletion preserves the “at least half full” property, all is good, otherwise ...  
- If possible borrow entry from a sibling node  
- If not possible, merge the node with the sibling node  
- Delete the separator between the node and the sibling from the parent node
	- If that causes that upper node to become less than half full continue recursively (up to root level)
![[Pasted image 20230216114531.png]]
![[Pasted image 20230216114549.png]]
![[Pasted image 20230216114604.png]]
# B+ Trees in Practice
- Typical trees
	- maximum fanout: 200
	- fill-factor: 67%.
	- average fanout = 133
- Typical capacities:
	- Height 4: 133 4 = 312,900,700 index entries
	- Height 3: 133 3 = 2,352,637 index entries
- Can often hold top levels in buffer pool:
	- Level 1 = 1 page = 8 Kbytes
	- Level 2 = 133 pages = 1 Mbyte
	- Level 3 = 17,689 pages = 133 MBytes

# Indexing and SQLite (using MA4.db)
![[Pasted image 20230216115111.png]]
## **IN ASSIGNMENT**
![[Pasted image 20230216115135.png]]
