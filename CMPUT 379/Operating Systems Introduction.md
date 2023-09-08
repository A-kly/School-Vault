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