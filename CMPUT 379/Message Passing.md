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
host ohaton
ohaton.cs.ualberta.ca has address 129.128.243.70
```
An IP address serves **two principal functions**. It *identifies the host, or more specifically its network interface*, and *it provides the location of the host in the network, and thus the capability of establishing a path to that host*.
Its role has been characterized as follows: “A name indicates what we seek. An address indicates where it is. A route indicates how to get there.” (wikipedia)

- Growth of Internet:
	- IPv4 – 32-bit addresses; 1983 (ARPANET)
	- IPv6 – 128-bit addresses; 1998 (de facto standard since mid-2000s)

- IP address consists of four fields, each specified by an 8-bit number (the “.”s are for readability)![[Pasted image 20231106121321.png]]
- Assignment of addresses managed by the Internet Assigned Numbers Authority (IANA)

- An Internet Service Provider (ISP) has an IP address known to the world.
	- It maintains its own local IP addresses.
	- All Internet traffic goes through the ISP, who translates external addresses to internal ones. ![[Pasted image 20231106121431.png]]

- 127.0.0.1 is the IP address commonly used for testing Internet applications
	• Refers to the machine that the program is running on
	• “loop-back address”
- ==GOTCHA: information must be sent in a machine-architecture independent way!==
	- htons/htonl – convert values between host byte order and network byte order
# Behind the Scenes
- TCP/IP: Transmission Control Protocol/Internet Protocol.