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
### Example
Do You Want to Do This...
```BASH
grep “author” file >file1
sort –u <file1 >file2
wc <file2
```
(This code Uses files for intermediate storage.)
... Or This?
```BASH
grep “author” file | sort –u | wc
```
==This one is better, "|" is pipe command==
#### Implementation (how does it work internally?)
- Fork three processes (`grep, sort, wc`)
- Change input of `sort` to come from the output of `grep`
- Change the input of `wc` to come from the output of `sort`
- *This implies that the data flowing between processes has to look like standard I/O*

### UNIX Magic
- `grep “author” file`
	- Output to the screen
- `grep “author” file >fileout`
	- Output to a disk file
- `grep “author” file >fileout`
	- Output to a tape file
- `grep “author” file | sort -u`
	- Output to a program
==With no change to the program!==
### Pipe Communication
```C
#include <stdio.h>
FILE * p; // This is file P. It can be read by the OS for use in piping and output forwarding.
p = popen( command, “r” ); // command = any command executed. The output is read ("r") and stored in file p.
rc = pclose( p );
```
The output that gets produced by executing command is accessible as *file p*. Thus to the calling process, it looks exactly like standard I/O,
```C
printf( ”format”, <args>* ); // STDOUT is implicit
fprintf( file, “format”, <args>* );
sprintf( string, “format”, <args>* );
```
#### Example
```C
FILE * p; int c;
if(( p=popen("cat pipe.c","r") ) == NULL){
	perror( "Could not open pipe\n" );
} else {
	while(( c=fgetc(p) ) != EOF){
		putchar( c );
	}
	pclose( p );
}
```

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
### Signal Types 
Numerous system-level and user-level signals. Here are some examples.
Keyboard generated:
	- SIGSTP `ctl-z` keyboard stop signal (Type:S)
	- SIGINT `ctl-c` interrupt (Type:T)
	- SIGQUIT `ctl-\` quit signal (Type:TC)

Hardware exceptions:
- `SIGSEGV` segmentation fault TC
- `SIGFPE` floating point exception TC
- `SIGBUS` bus error TC
Software conditions:
- `SIGXCPU` cpu time limit exceeded T
- `SIGCHLD` change in child status I
- `SIGALARM` timer alarm T
- `SIGHUP` hangup T

Other signals to do with
- File I/O
- Timers/clock

User exceptions:
- `SIGUSR1` user defined T
- `SIGUSR2` user defined T