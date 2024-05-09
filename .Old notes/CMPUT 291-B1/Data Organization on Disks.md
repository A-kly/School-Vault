- Used in [[Databases]]

- We saw that modern DBs decouple the physical schema (or layer)...
	- Low-level data structures and encodings used to store, represent, and access information on some physical medium (e.g., HDDs, SSDs, ...).  
- ...from the conceptual schema.
	- Mapping between abstract concepts (e.g., relations) and the low-level machinery used to store/represent/access them. 

-  Physical data independence: changing the physical schema does not  impact the conceptual schema.
- Over the next few classes we will focus on the physical layer.
- In particular, we will cover: 
	- Physical properties of disks, how data is stored/accessed on disks, use of files to structure information in a DB, and use of indexes to speed up accesses. 
- Goal: better understanding of the overhead and cost of I/O operations, and how to solve some data management problems (even outside the context of DBs).

# Computer memory hierarchy

- The collection of data that makes up a DB must be stored physically on some computer storage medium. Which one?  
- Databases typically have to store large amounts of data that must persist over long periods of time.  
- Parts of the DB are accessed and processed repeatedly.  
- In a modern computer system, data resides and is transported throughout a hierarchy of storage media.  
- Need to determine the appropriate medium for online storage of DBs
- ![[Pasted image 20230209111752.png|600]]

- **Primary storage**
	- cache (L1/L2/L3/...) memories: speed up the execution of program instructions; exploit spatial/temporal locality when processing data.
	- DRAM (main memory): provides to the CPU the main working area where keeping instructions and (chunks of) data to process.
	- _Characteristics_: very high throughput, fast random accesses, limited capacity, expensive, transient storage (content lost with power failure/crash).
		- _transient storage:_ if you pull the plug, it is wiped
- **Secondary storage**
	- HDDs (magnetic disks), SSDs, Flash disks, ...
	- _Characteristics_: reasonable throughput, reasonable capacity, reasonable cost, random accesses with reasonable performance, persistent storage.
	- HDDs: still primary choice for online storage of enterprise databases.
- **Tertiary storage**: removable media such as
	- Tapes
	- Optical disks (DVD, blu-ray, ...)
	- Cloud?
	- _Characteristics_: high sequential throughput, huge capacity, very affordable, persistent storage, but very slow random accesses.
	- Feasible for archiving databases (offline storage).

![[Pasted image 20230209112443.png]]

# HDDs

- Databases typically store large amounts of data that must persist over long periods of time. 
- Parts of the DB are accessed and processed repeatedly during the storage period. 
- Typical setting with modern DBs: data is stored on HDDs, and parts are fetched to RAM when needed.  
	- DBs are typically too large to entirely fit in main memory.  
	- Circumstances that cause permanent loss arise way less frequently with secondary storage.  
	- Cost of storage per unit of data consistently lower than primary storage
![[Pasted image 20230209112820.png|500]]

- All HDDs contain a set of thin disks, each called platter, made by magnetic material.
- The set of platters forms a disk pack that rotates around an axis called spindle.
- Platters can be single sided or (more typically) double sided. Each surface requires a read/write head.
- Each surface hosts a set of fixed concentric circles called tracks.
- Each track has a fixed diameter. Read/write heads operate on one track at a time.
- ![[Pasted image 20230209114344.png]]
- ![[Pasted image 20230209114400.png]]
- ![[Pasted image 20230209114840.png]]
- 

# Physical Disk Structure
![[Pasted image 20230209112929.png|300]]![[Pasted image 20230209112944.png|300]]
![[Pasted image 20230209113012.png|300]]

# Example specs

Given the specs of the following HDD (Seagate Barracuda)...
- 930,408 cylinders
- 2 tracks per cylinder (1 single double-sided platter)
- 63 sectors per track
- 512 bytes per sector

..determine the capacity of the HDD.
- bytes/track = bytes/sector * sectors/track = 512 * 63 = 32,256 bytes.
- bytes/cylinder = bytes/track * tracks/cylinder = 32,256 * 2 = 64,512 bytes.
- bytes/disk = bytes/cylinder * cylinders/disk = 64,512 * 930,408 = 60,022,480,896 bytes = 60 GB.

# Data units in HDDs

- A sector represents the smallest unit that can be transferred to/from a
disk head.
- Tracks are logically divided in pages (or blocks) by the OS when formatting an HDD.
	- Page size is c * sector size (for some constant c)
- _A page is the smallest unit of transfer for most applications._
- The address of a page is given by the combination of:
	- Cylinder index
	- Track index (i.e., surface index within the cylinder)
	- Block index (within the track).

# Access time

How long does it take to access a specific page?  
1.  HDD controller accepts a high-level I/O command to access a specific page.  
2.  HDD mechanically positions its read/write heads on the correct track (given by the cylinder index) => _AVG SEEK TIME_.  
3. Then, wait for the beginning of the page to rotate into position under the head => _AVG ROTATIONAL_ (formula = DELAY (60/RPM)/2)
4. Then, read/write data from the page => TRANSFER TIME. 
	- (# bytes to transfer / # bytes per track) * time for one disk rotation 
	- Alternatively, if we reason in terms of sectors instead of bytes: 
		 - transf. time per sector = transf. time per track / # sectors per track 
		- transfer time = # sectors to transfer * transfer time per sector.

_Best case scenario is when data is on multiple sequential sectors on the same track_
_Worst case is when data is on very spread out tracks and sectors_

## Example

Consider a Barracuda disk from Seagate with the following specs:  
- 63 sectors per track  
- 512 bytes per sector  
- average seek time of 9 ms  
- disk platters rotate at 7200 rpm  
- pages of 5 sectors each. (Time needed to transfer a page is that of transferring 5 sectors)

- Avg seek time = 9ms.
- Time to complete one rotation: 60/7200 = 0.00833 s = 8.33 ms.
- **Avg rotational delay** = time for one rotation / 2 = **4.16ms**.
- **Transfer time** = sectors transferred * transf. time per sector
- **transf. time per sector** = transf. time per track / # sectors track = 8.33ms / 63 = 0.13ms. => **TT** = 5 * 0.13ms = **0.65ms** (a page = 5 sectors)
- **Access time** = 9ms + 4.16ms + 0.65ms = **13.81ms**

# Reducing I/O costs

How crucial is the problem?  
- Disk capacity has improved 1,000+ times in the last 15 years.  
- The size of data also has increased at least in the same rate.  
- But,  
	- platters only spin 4x faster.  
	- the transfer rate has improved only 40x in the same period.  
Thus:  
- _disk accesses are precious_
- they are expected to be more precious in future.

Key to lower I/O cost: reduce seek/rotation delays  
- Software solutions  
	- arrange blocks of a file **sequentially** on disk  
	- read/write in **bigger chunks**  
	- **buffering**  
- Hardware solutions  
	- Will not be discussed in detail ... (très désolé)

# Sequential Access

- Store pages containing related information close together on disk (contiguous blocks/cylinders).
	- Justification: locality principle, i.e., if application accesses x, it will next access data related to x with high probability
- Page size tradeoff:
	- Large page size - data related to x stored in same page; hence additional page transfer can be avoided.
		- Issue: data of a page must be entirely read/written.
		- Issue: increased buffer size in main memory.
- Small page size - reduce transfer time (do not read “useless” data), reduce buffer size in main memory.
- Typical page size - 4096 bytes

# Bigger Chunks
**ON MIDTERM** #review 
- Consider:  
	- An IBM Deskstar disk with 40 sectors/track, 512 bytes/sector and average seek time of 9.1 msec. Disk platters spin at 7,200 rpm.  
		- average rotational delay=(1/7200)/2 minutes = 4.17 msec.  
		- transfer time for a sector= (1/7200)/40 minutes = 0.21 msec  
	- A file of 6400 256-byte records = 1638 KB occupies 3200 sectors of the disk.  
- Case 1:  
	- The file is stored in 100 extents (contiguous chunks), each of size 4 pages where each page is 8 sectors.  
	- Time to read the file = 100 x ( 9.1 + 4.17 + (4x8) x 0.21) = 2 seconds  
- Case 2:  
	- The file is stored in 3200 pages each of size one sector.  
	- Time to read the file = 3200 * (9.1 + 4.17 + 0.21) = 43 seconds

# Buffering

- Typical database applications need only to access small portions of the data within a DB.  
- Each portion (set of pages) must be first located on the disk, copied to main memory for processing, and finally rewritten to disk in case of modifications  
- Idea: keep cache of recently accessed pages in main memory. 
	- Goal: request for page can be satisfied from cache instead of disk.  
	- Purge pages when cache is full:  
		- For example, use _LRU algorithm_  
		- Record clean/dirty state of page (clean pages don’t have to be written)

# Accessing data through cache
![[Pasted image 20230209121722.png]]
# Hardware Solutions
![[Pasted image 20230209121751.png]]
# Summary

![[Pasted image 20230209121817.png]]
