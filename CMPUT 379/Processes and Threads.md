# Processes
## What is a process?
- A *process* is a program in execution
- Components:
	- program to be executed
	- data on which the program will execute
	- CPU resurces (registers)
	- data resources required by the program (memory & files)
	- status of the execution
## Program vs Process
Are they the same?? ***NO***
- **It can be More:** a program is just part of a process context. tar can be executed by two different people, same program (shared code) as part of different processes.
- **It can be less:** a program may invoke several processes. cc invokes cpp, cc1, cc2, as, and ld.

## Uni-programming vs Multi-programming 
- **Uni-programming:** allows execution of only one process at a time (e.g., early personal computers).
- **Multi-programming:** allows more than one process, i.e., concurrent execution of many processes.
	- The CPU *switches automatically from process to process*, running each for tens or hundreds of milliseconds. In reality, the CPU is *actually running one and only one process at a time*.

## Multiple Processes: One CPU
How can several processes share one CPU?
OS makes sure to take care of processes by:
- Making sure every process has a chance to run (good *scheduling*).
- They do not modify each others state (*protection*).
- Resources (including CPU) are shared.
## Process States
- Lifetime of process, from birth to death, can be described by a number of states.
- The operation of a multiprogramming system can be described by a state transition diagram on the process states.
- Most of the state transitions are internal to the operating system and the user has no control.
### Process state diagram
![[Pasted image 20230915123638.png]]
**Internal:** OS makes change.
**External:** User/program makes change.
### Possible States
- **New:** a process being created but not yet included in the pool of executable processes (resource acquisition).
- **Ready:** processes that are prepared to execute when given the opportunity.
- **Active:** the process that is currently being executed by the CPU (only one at a time).
- **Blocked:** a process that cannot execute until some event occurs.
- **Stopped:** a special case of blocked where the process is suspended by the operator or the user.
- **Exiting:** a process that is about to be removed from the pool of executable processes (resource release).

## Process Description
- The operating system must know specific information about processes to manage and control them.
- Such information is usually grouped into two categories:
	- **Process state information**, such as CPU registers and program counter.
	- **Process control information**, such as scheduling priority, resources held, access privileges, memory allocated, and accounting.
- Information in both groups are OS dependent.
- This info is all kept in the **process control block (PCB)** or **process table**.

## Process Scheduling #COMEBACKTOTHIS
## Process Creation Mechanisms
![[Pasted image 20230920120351.png]]
### UNIX Example
![[Pasted image 20230920120414.png]]
- **Parent process:** Fork() returns name (pid) of child process.
	- `if` evaluates to true
- **Child process:** Fork() returns 0.
	- `if` evaluates to false. `else` block runs, child executes `else` code.
#### Example fork()
![[Pasted image 20230920120707.png]]
First one prints one parent pid twice.
Second one prints Parent pid and then child pid.
==Code example on eClass==
### Typical Use of fork()
![[Pasted image 20230920122056.png]]
- `exec()` causes the currrent (often child) process to rewrite itself. It tells the process to change the code and data that it is executing.
==code example online==
### Coordination
- Parent and child(ren) process(es) may need to coordinate with each other.
	- `wait()` allows the parent to check the running status of the child, and/or wait until the child process completes.
	- This is a form of synchronization, an important concept in concurrency (more later in the course).
#### Example wait()
![[Pasted image 20230920124833.png]]
==More code on eClass==
## Process examples
- Top - Shows currently running processes!
	- `top -o cpu -O +rsize -s 5 -n 30`
	- **PID:** process identification number
	- **COMMAND:** user or system program
	- **%CPU:** current CPU usage
	- **Time:** total CPU usage
	- **\#Th:** number of threads
	- **MEM:** amount of memory being used
	- **PPID:** pid of the parent process
	- **STATE:** process state
	- **UID:** id of the user
- ps - similar to top, PPIDs
	- `ps –efc`
	- output:![[Pasted image 20230922122646.png]]
	- **PID:** process identification number
	- **PPID:** *Parent* process identification number
## UNIX System Initialization
![[Pasted image 20230922123734.png]]
## Process Termination
A process enters the exiting state for one of the following reasons:
- Normal completion: A process executes a system call for termination (e.g., in UNIX exit() or abort() is called, either explicitly or implicitly by the user program).
- Abnormal termination:
	- Programming errors (e.g., divide by zero)
	- Run time (e.g., out of memory)
	- I/O (e.g., hardware errors)
	- User intervention (e.g., kill the process)
- You might even see a *zombie* process!
# Threads
