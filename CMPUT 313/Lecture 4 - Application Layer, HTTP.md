# How are the layers implemented?
![[Pasted image 20250116110423.png]]
# Network Applications
- Social networks
- Web browsers
- Text
- Email
- Remote login
- p2p file sharing
- video streaming
- multiplayer games
- real time video (zoom) or VOIP - interactive
## Creating an application
- programs that:
	- run on different end systems
	- communicate over the network
- No need to write software for network core devices
	- They just don't run application and transport layer
# Client-server paradigm
- Server
	- Always-on host
	- often has a permanent IP
	- often in data centers for scaling
- Clients
	- Communicate with server
	- may be intermittently connected
	- may have dynamic IP
	- do NOT communicate with each other directly
	- protocols
		- HTTP, IMAP, FTP, etc
## Peer 2 Peer architecture
- No always on server
- arbitrary end systems (peers) communicate directly
- peers request services from other peers in return for other services
	- self scalable
		- new peers increase both demand and capacity
- IP addresses can change
	- We need to come up with a better way to track hosts consistently
# Communicating processes
- Process = program running in host
- Within host, processes communicate using inter-process communication methods from OS
- processes in separate hosts exchange messages
- ![[Pasted image 20250116112127.png|200]]
## Sockets
- Process sends/receives messages to and from socket defined by IP and port num
	- Abstraction of network I/O
	- Client and server sockets (one on each side)
- Socket = door
	- Sending data =  push messages out door
	- Receiving data = Open door to see if message is there
## Addressing processes
- Process needs identifier to receive message
- host has unique 32 bit IP
- **Port numbers are used to connect to a specific process, on a host, from an IP**
	- IP is not enough, host has many processes
# Application layer protocols defines...
- **Type of messages exchanged**
	- request, response
- **Syntax**
	- message "format"
- **Semantics**
	- Meaning
- **Rules for when and how messages are sent and responded to**
---
- **Open protocols**:
	- defined in RFCs, everyone has access to definition
	- allow for interoperability
	- evolve slowly
- **Proprietary protocols**
	- Skype, zoom, etc.
# What transport services does an app need?
- **Data integrity**
	- reliable data transfer
	- some apps tolerate loss
- **Timing**
	- delay must sometimes be low (destiny 2 lmao)
- **Throughput**
	- Some apps need minimum throughput
- **Security**
	- encryption, data integrity
## Transport service requirements: common apps
![[Pasted image 20250116113236.png]]
# Internet transport protocols services
![[Pasted image 20250116113426.png]]
# Internet applications, and transport protocols
![[Pasted image 20250116113444.png]]
# Securing TCP
- **Vanilla TCP & UDP sockets:**  
	- no encryption  
	- cleartext passwords sent into socket traverse Internet in plaintext
- **Transport Layer Security (TLS)** 
	- provides encrypted TCP connections  
	- data integrity, confidentiality, and endpoint authentication  
	- implemented in application layer  
	- requires a handshake for certificate exchange and key generation
# HTTP and Web
- Web page is a collection of objects
	- HTML, jpeg, audio file
- Page is a base HTML file which includes reference objects, addressable by URL
- `www.hostname.com/path/to/resource.gif`
## HTTP overview
- HTTP is application layer protocol
- 