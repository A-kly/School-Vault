Cooperating processes need to exchange information, as well as synchronize with each other, to perform their collective task(s). The primitives like `wait()` can be used to synchronize the operation of cooperating processes, but they **do not convey information between processes**. 

Methods for effective sharing of information among cooperating processes are collectively known as **inter-process communication (IPC)**.
## IPC mechanisms
The following are IPC mechanisms can be used for IPC:
- Shared Memory ([[Processes and Threads#Threads]])
- Files
- Pipes
- Signals
- Shared Memory (processes) – later
- Message Passing – later
- Sockets – later

## Files
## Pipes
## Signals
- Like an interrupt but *not in hardware*, they are **Software interrupts**.
- A signal can be sent:
	- by one process to another, including itself (in the lattercase it is synchronous).
	- by the kernel to a process.
- A signal is *generated* when the event first occurs and *delivered* when the process takes an action on that signal. 
- A signal is *pending* when generated but not yet delivered. 
### Sending a signal
- `Ctrl+C` in the shell **Kills** the current process
	- This is a signal
- `Ctrl+Z` 