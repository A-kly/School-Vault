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
- Client server model
	- client requests, receives and displays web objects
	- Server sends objects in response to requests
### HTTP is built on TCP
- Client initiates TCP connection with a socket on port 80
- Server accepts TCP connection
- HTTP messages exchanged between client and server
- TCP connection closed
- HTTP is "stateless"
	- Server maintains no info about client requests
	- State maintenance is super complex, so we don't do this
## HTTP connections
- **Non-Persistent HTTP**
	1. Connection opened with TCP
	2. One object is sent over TCP
	3. Connection closed
- **Persistent HTTP**
	1. Connection opened with TCP
	2. Multiple objects sent
	3. Connection closed
### Non persistent example
![[Pasted image 20250116114924.png]]
![[Pasted image 20250116114944.png]]
### Non-persistent HTTP: response time
- **RTT**
	- At least one Round Trip TIme required to establish connection
- HTTP response time (per object)
	- one RTT to initiate TCP connection
	- one RTT for HTTP request and first few bytes of HTTP response to return
	- object/file transmission time
![[Pasted image 20250116115146.png]]
**Non-persistent HTTP response time = 2RTT+ file transmission time**
### Persistent HTTP
![[Pasted image 20250116115216.png]]
## HTTP request message
- ASCII data
	- EVERY LINE ENDS WITH CARRAGE RETURN AND LINE FEED
- Request line
	- GET, POST, HEAD, etc
		- `GET this/is/a/resource HTTP/1.1\h`
- Header
	- Host
	- User-Agent
	- etc.
- Body
	- Good for post and put requests
### General format
![[Pasted image 20250116115538.png]]
### Example request headers
- Connection: keep-alive
	- "don't terminate connection"
- User-Agent: Mozilla/5.0 (X11; Linux x86_64)  
- Accept: text/html
	- "What am I expecting to receive?"
- Host: cs.ualberta.ca
	- "What page am i accessing?"
...
- Referer: amazon.com
	- "Go to another web server to get content from the page I'm requesting"
- Cookie: 1678  
...
- If-Modified-Since: Wed, 21 Oct 2015 07:28:00 GMT
	- "Give me a new page if the page has been changed"
- If-None-Match: "33a64df551425fcc55e4d42a148795d9f25f89d4"
	- "Give me the resource if the hash of the resource has changed and is different from this hash"
### Other HTTP request methods
![[Pasted image 20250116120225.png]]
## HTTP response message
- Status line
	- `HTTP/1.1 200 OK`
- Header lines
	- Date
	- Server
	- Last-Modified
	- ETag
	- Content-length
	- Content-Type
- Data
### Status codes
- 100s Informational responses  
- 200s Successful responses  
- 300s Redirection messages  
- 400s Client error responses  
- 500s Server error responses
- Examples
	- 200 OK  
		- request succeeded, requested object later in this message  
	- 301 Moved Permanently  
		- requested object moved, new location specified later in this message (in Location: field)  
	- 400 Bad Request  
		- request msg not understood by server  
	- 404 Not Found  
		- requested document not found on this server  
	- 505 HTTP Version Not Supported
## Trying out HTTP (client side) for yourself
![[Pasted image 20250116120657.png]]
## Maintaining user/server state: cookies
- We need to sometimes store the state of what happened between client and server
- Notion of multi step exchanges to complete "transaction"
	- No need for client or server to track state
	- All HTTP requests are independent
	- no need for client/server to “recover” from a partially-completed-but-never-completely-comp leted transaction
- **Web sites and client browser use cookies to maintain some state between transactions**
	- Four components
		1) cookie header line of HTTP response  message 
		2) cookie header line in next HTTP request message 
		3) cookie file kept on user’s host, managed by user’s browser 
		4) back-end database at Web site
![[Pasted image 20250116121219.png|300]]
![[Pasted image 20250116121311.png]]
### Cookies
- What cookies can be used for
	- authorization  
	- shopping carts  
	- recommendations  
	- user session state (Web e-mail)
- Challenge: How to keep state?
	- at protocol endpoints: maintain state at sender/receiver over multiple transactions
	- in messages: cookies in HTTP messages carry state

#### 3rd party cookies example: displaying a NY Times web page
![[Pasted image 20250116121629.png|300]]
![[Pasted image 20250116121651.png]]
![[Pasted image 20250116121810.png]]
![[Pasted image 20250116121826.png]]
![[Pasted image 20250116121852.png]]
