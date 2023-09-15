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
- Lifetime of process, from birth to death, can bedescribed by a number of states.
- The operation of a multiprogramming system can be described by a state transition diagram on the process states.
-  Most of the state transitions are internal to the operating system and the user has no control.