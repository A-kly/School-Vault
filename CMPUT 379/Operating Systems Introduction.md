# Intro
Computer is made of two parts:
- Hardware
- software
## Software
- Application software
	- user programs, games, etc.
- System Software
	- OS, utilities, login windows, etc.

### User views
User Applications: Calculations, file manipulation, communication, etc.
**interacts with**
Hardware: CPU, memory, storage, I/O etc.

- We put in a simple request and the OS figures the rest out

## Contemporary Hardware/Software Structure
![[Pasted image 20230908121207.png]]
# Operating Systems
## What Is an Operating System?
- Resource manager of *time* and *space*
- manage processor, main memory, I/O devices
- provides **orderly** and **controlled** resource allocation and use by the users (jobs) that compete for them
- Hides complexity of underlying hardware and give the user a better view (an abstraction) of the computer.
## Why study OS?
- Abstractions effect application structure
- Largest and most complicated software systems
- Draws on many domains in CompSci
	- software engineering, architecture, data structures, networks, algorithms
- Can apply OS techniques to other areas
	- Data structure design
	- concurrency
	- resource management
	- conflict resolution
	- security
## OS Roles
- Referee
	- Resource allocation for users + applications
	- Isolate users/programs from each other
	- Communication between users + applications
- Illusionist
	- Applications/users see a machine all to themselves
	- users/apps see a perfect computer w/ infinite resources, memory, storage, etc.
		- details not necessary for users to see or mess with
- Glue
	- Libraries, UI Widgets

## History
**Multiprogramming:** One processor, Multiple Programs
**Multiprocessing:** Many processors, Many programs per processor
**Parallel processing**:
- multiprocessors (share a common bus, clock, and memory), multi-core
- tightly-coupled; multiprocessing
**Distributed processing**:
- multicomputers (do not share memory and clock)
- loosely-coupled
**Real-time**:
- deadline (time critical) requirements
- soft real-time (miss some, performance degrades); hard real-time (must make deadlines)
### Job Interleaving
- Uniprogramming
	- One job after the other, no I/O sharing, 
	- ![[Pasted image 20230911121541.png]]
	- Job A goes to completion and then Job B does the same
- "Pure" Multiprogramming
	- I/O and Cpu use is Interweaved, more efficient and less component downtime
	- ![[Pasted image 20230911121611.png]]
### Memory partitionning
- Divide system memory into chunks that programs can use seperately
- ![[Pasted image 20230911121707.png|300]]
# Hardware considerations
## Interrupts 
**External from program execution**
External or internal event (or an exception) interrupts the CPU for it to deal with. Notification of an external event that occurs asynchronously from current processor activity. Time of interrupt is not known or predictable
### External Events
- Character typed on keyboard or console
- Completion of I/O operation
- Timer to make sure operating system eventually gets control (infinite loop)

## Traps
**Internal to program execution**
A trap is the notification of an (internal) event that occurs while a program is executing, therefore is synchronous with the current activity of the processor.
Traps are immediate and are usually predictable since they occur while executing (or as a result of) a machine instruction.
### Internal Events
- System call.
- Error item (e.g., illegal instruction, addressing violation, divide by zero).
- Page fault (memory management).