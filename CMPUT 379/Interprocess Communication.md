Cooperating processes need to exchange information, as well as synchronize with each other, to perform their collective task(s). The primitives like `wait()` can be used to synchronize the operation of cooperating processes, but they **do not convey information between processes**. 

Methods for effective sharing of information among cooperating processes are collectively known as **inter-process communication (IPC)**.
## IPC mechanisms
The following are IPC mechanisms can be used for IPC:
- Shared Memory ([[Processes and Threads#Threads|Threads]])
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
	- `kill(int pid, int sig);` sends a signal sig to the process `pid`. Note that the name kill is a misnomer; the signal sent does not have to kill the process. Equivalent to `Ctrl+C`
- `Ctrl+Z` in the shell **Stops or suspends** a process
	- Also a signal, does not kill but stops temporarily.
- `bg` brings process to background after it has been stopped
- `fg` brings process to foreground after it has been stopped

### Receiving a signal

- Using the `signal()` system call, a process can:
	- **Ignore** the signal—all except for two signals (SIGKILL and SIGSTOP) can be ignored.
	-  **Catch** the signal—tell the kernel to call a function whenever the signal occurs.
	-  **Let the default action apply**—depending on the signal, the default action can be:
		- T (terminate)—perform all activities as if the exit system call is requested.
		- TC (terminate and core dump)—first produce a core image on disk and then perform the exit activities.
		- S (stop)—suspend the process.
		- I (ignore)—disregard the signal.

A process can declare a function to service a particular
signal as:
```C
#include <signal.h>
signal(int sig, SIGARG func);
```
(or the more modern `sigaction()`).
- Whenever the specified signal sig is received, the process is interrupted and `func()` is called immediately. This is a **catch**.
- On return from `func()`, the process resumes its execution from where it was interrupted.

#### Example
```C
#include <stdio.h>, <unistd.h>, <signal.h>
int i;
void interrupt(int code){ fprintf(stderr,
	"\nInterrupt (code= %d, i= %d)\n", code, i );
}
int main( void ){
	signal( SIGINT, interrupt );
	for( i = 0; i < 100; i++ ){
		putc( '.', stderr ); // IO issue?
		sleep( 1 );
	}
}
```
- This code prints "." until an interrupt is generated. It then prints the code of the interrupt.
- Output: ![[Pasted image 20230925122159.png|300]]
- `SIGINT` is defined as the kill signal (aka `Ctrl+C`).
- 