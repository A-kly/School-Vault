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
External or internal event (or an exception) interrupts the CPU for it to deal with. Notification of an external event that occurs asynchronously from current processor activity. Time of interrupt is not known or predictable.
### External Events
- Character typed on keyboard or console
- Completion of I/O operation
- Timer to make sure operating system eventually gets control (infinite loop)

### More content
- Interrupts have various priority levels. One must be handled before another
- If a higher level interrupt happens while handling a lower level interrupt (nested interrupts) we have to deal with the higher level one while the lower level one is suspended.
- When interruption of an interrupt handler is undesirable, other interrupts can be ‘‘masked’’ (inhibited) temporarily.

## Traps
**Internal to program execution**
A trap is the notification of an (internal) event that occurs while a program is executing, therefore is synchronous with the current activity of the processor.
Traps are immediate and are usually predictable since they occur while executing (or as a result of) a machine instruction.
### Internal Events
- System call.
- Error item (e.g., illegal instruction, addressing violation, divide by zero).
- Page fault (memory management).

## Interrupt Handling
![[Pasted image 20230911123502.png]]

1. An interrupt occurs, branch to OS.
	1. Stop, Jump out of program and let OS deal with the problem.
2. Locate the interrupt service routine (ISR).
	1. This is done in interrupt vector
	2. Do a bunch of condition checks and figure out which one, Jump to code to deal with it (IRS).
3. Execute the ISR.
	1. Interrupts can be interrupted
	2. Certain interrupts have a priority over other interrupts
4. Return to interrupted program.

**When the CPU receives an interrupt, it is forced to a different context (kernel's) and the following occurs**:
- Current state of the CPU (PSW) is saved in a specific location.
- Interrupt information is stored in another specified location.
- CPU resumes execution at some other specific location: the Interrupt Service Routine.
- After servicing the interrupt, execution resumes at the saved point of the interrupted program.
- *The CPU suspends its (current) execution and services the interrupt.*
## I/O techniques
### Programmed I/O
- *Polling system*. Repeatedly check I/O until we see that is not in use anymore. *Slow*.
![[Pasted image 20230913120530.png]]

### Interrupt-driven I/O (slow speed, character device)
- CPU issues I/O operation, does other work and then when CPU receives interrupt, it handles data transfer. We have eliminated polling but *introduces interrupt overhead*.
![[Pasted image 20230913120656.png]]
### Direct Memory Access (DMA) (high speed, block device)
- CPU issues an I/O operation specifying the device, the memory location of the data, and the block size. This info is sent to DMA device. Once DMA device is done doing shit it Interrupts the CPU. *Memory access and CPU are used in parallel*.
![[Pasted image 20230913120938.png]]
# Architectural Support
- Modes of operation
	- Supervisor (protected, kernel) mode: *all (basic and privileged) instructions available*.
	- User mode: *a subset (basic only) of instructions*.
	- Hardware support for virtual machines.
- I/O protection
	- All I/O operations are privileged.
- Memory protection
	- Base/limit registers (in early systems).
	- Memory management unit.
- CPU control
	- Timer (alarm clock); time-quantum.
	- Context switch
## Modes of Operation, Why?
- Needs to protect itself from the user program. Don’t crash when a program misbehaves.
- Needs to protect multiple programs against themselves. A program should not be able to damage another program (e.g., a different user’s).
- Wants to be in charge of the resources, presenting a consistent logical view to the programs (and to the user). This is impossible if the programs are allowed to access those resources directly.

## Accessing OS Services
- Make a system call in order to do anything with the computer. System calls are an *interface* for the computer. (like an API)
- **procedure call / function call:** No CPU mode change
- **[[#System calls]]:** CPU changes to Supervisor mode
- System call interface: A set of functions that are called by (user) programs to perform specific tasks. *Often implemented as a trap*.

## System calls
### Mechanism
![[Pasted image 20230913122959.png]]
1. Program makes a system call
	- eg. "I wanna read a file!"
2. jump to system call handler, makes sure all arguments are good, make sure privileges, address, everything is good
	- If no, return with error code
	- If yes: OS changes mode! then:
3. Branch to service function
	-  deal with system call, if it fails return with error
4. switch mode back to user mode, return to system call handler and then return to user's program
### System Call Groups
- UNIX family:
	- Process control
		- `fork(), exec(), wait(), abort()`
	- File manipulation
		- `chmod(), link(), stat(), creat()`
	- Device manipulation
		- `open(), close(), ioctl(), select()`
	- Information maintenance
		- `time(), acct(), gettimeofday()`
	- Communications
		- `socket(), accept(), send(), recv()`
# System Structure
Possible Structures:
- **Simple, single-user**
	- [[#MSDOS Structure|MSDOS]], pre-OS X MacOS, early Windows
	- iOS (Apple)
- **Monolithic, multi-user**
	- Multics, OS/360, [[#UNIX Structure|UNIX]], Linux,
- **Virtual machine**
	- [[#IBM VM/370 Structure|IBM VM/370]], VMware ESX, Xen, Linux KVM
- **Client/Server (microkernel)**
	- [[#Chorus/MiX]], Mach, QNX
## OS Kernel
- **Core of the operating system. The center. Cannot exist without it.**
	- Highly refined, optimized, "perfect"
- ==Kernel = OS - transient components (comes and goes)==
- Kernel = dispatching, interrupt handling, or managing (critical) resources.
## MSDOS Structure
![[Pasted image 20230913124838.png]]
## UNIX Structure
![[Pasted image 20230913125005.png]]
## IBM VM/370 Structure
![[Pasted image 20230913125045.png]]
## Chorus/MiX ==(basically how linux works)==

![[Pasted image 20230915120354.png]]
