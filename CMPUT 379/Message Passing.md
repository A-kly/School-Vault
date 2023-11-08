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
	- hton = host to network (this is a conversion routine so that the endianness is the same)
# Behind the Scenes
- **TCP/IP:** Transmission Control Protocol/Internet Protocol.
	- Standardized rules that allow computers to communicate on a network such as the internet.
	- ![[Pasted image 20231106121656.png]]
## Connections
- **Transmission Control Protocol (TCP)**
	- Reliable, ordered, and error-checked delivery.
	- WWW, email, file transfers require TCP.
	- SOCK_STREAM
- **User Datagram Protocol (UDP)**
	- No guarantee of delivery, ordering, or duplicate protection.
	- Least overhead, hence fastest.
	- DNS, video/audio streaming.
	- SOCK_DGRAM
## Common Usage
Client-server architecture
![[Pasted image 20231106121856.png]]
# Overview
**The following is an overview of how all of the important functions work and their general use.**
![[Pasted image 20231106122002.png]]
THIS diagram is equivalent to:
![[Pasted image 20231106122026.png]]
## Socket()
```c
int listenfd;
// create socket
if((listenfd=socket(AF_INET, SOCK_STREAM, 0))<0)
	{ perror( "socket" ); exit( -1 ); }
```
==AF_INET – use the address family for the Internet (i.e., IP protocol addresses).==
## Ports
*IP address provides the address to send the message to*.
*The port number is the mailbox at that address*.
![[Pasted image 20231108120438.png]]
## Bind() (also inet_pton)
```c
struct sockaddr_in serv_addr;
serv_addr.sin_family = AF_INET;
serv_addr.sin_addr.s_addr = htonl(INADDR_ANY);
serv_addr.sin_port = htons(8888); // Change?
// tie the socket to the address
if(bind(listenfd, (struct sockaddr*)&serv_addr, sizeof(serv_addr))< 0)
	{ perror( "bind" ); exit( -1 ); }
```
## Listen()
Agree to accept incoming connections (listen) and give a queue limit for incoming connections.
```c
// accept a backlog of up to 10 connections
if( listen(listenfd, 10) < 0 )
	{ perror( "listen" ); exit( -1 ); }
```
If a connection request arrives with the queue full, the client may *receive an error with an indication of ECONNREFUSED*. Alternatively, if the underlying protocol supports retransmission, the request may be ignored so that retries may succeed.
## Accept()
```c
// wait for a message and accept it
if((connfd=accept(listenfd, &clnt_addr, &clnt_len))< 0)
	{ perror( "accept" ); exit( -1 ); }
```
Can receive a message from anyone.
Connfd is “file” descriptor for the connection, and clnt is who made the connection.
## Read()/Write()
**Note that socket i/o is just like file i/o!**
```c
// Read the message
if(read(connfd, &msg, sizeof(msg))!=sizeof(msg))
	{ perror( "read" ); exit( -1 ); }
// Write a message
if(write(connfd, &msg, sizeof(msg))!=sizeof(msg))
	{ perror( ”write" ); exit( -1 ); }
```
## Sockets == Files
Can convert a socket into a file descriptor:
```c
FILE *fin, *fout;
fin = fdopen(socket, “r”);
fout = fdopen(socket, “w”);
```
Now can use:
```c
fscanf(fin, “%30s%d”, &name, &age);
fprintf(fout, ”Hello to %s age %d\n”, name, age);
```
## Close()
**Note that socket closing is just like file closing!**
```c
close(connfd);
// “how” used to disallow sending any more messages,
// disallow receiving any more messages, or both
shutdown(connfd, how);
```
## Client
```c
connfd = socket(AF_INET,SOCK_STREAM,0);
// Change an IP address as a string into a network address
serv_addr.sin_addr.s_addr = inet_addr(”127.0.0.1”);
serv_addr.sin_family = AF_INET;
serv_addr.sin_port = htons(8888);
if(connect(connfd, (struct sockaddr *)&serv_addr, sizeof(serv_addr))<0)
	{ perror("Connect"); return 1; }
read()/write() //can be either or both in any order, many times
close()/shutdown() // must close the connection
```