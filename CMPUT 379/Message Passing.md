# Introduction
- Shared memory and files allow communication between processes/threads on the same machine.
- How do you communicate between machines?
	- Send information (data, data structures, signals) between machines using message passing.
# Writing Network Code
Details *best left for a networking course*.
==Code for creating connections and sending/receiving data is available on the Internet. An example is:==
www.thegeekstuff.com/2011/12/c-socket-programming

**Introduce you to the basics, for use in Assignment #3**.
Use sockets as the internal endpoint for network transmission.
• Analogous to an electrical connector
# Usage
- **Parallel applications**
	- Multiple processes on multiple machines each contributing to performing a computation
	- Message Passing Interface (MPI)
- **Network Devices**
	- Printers, scanners, file servers on local network
- **Internet**
	- Sending/receiving data from remote sites
	- World Wide Web, search engines, ecommerce, etc.
# Messages
Each machine has an address
Send a “letter” from one address to another
Letter’s contents are the message to be conveyed
![[Pasted image 20231106121020.png]]
# Transmission
![[Pasted image 20231106121047.png]]
# IP Addresses 
Every machine is given an Internet Protocol (IP) address and a symbolic name for ease of reference:
```
```