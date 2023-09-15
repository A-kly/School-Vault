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


