- Allows us to build network applications that communicate using a pair of sockets
- these apps are processes running on the same or different computers
![[Pasted image 20250128112814.png]]
# Socket specifies IP and port number
![[Pasted image 20250128112839.png]]
# Socket types
- Two socket types for two transport services:
	- **UDP:** unreliable (best effort) datagram (SOCK_DGRAM)
	- **TCP:** reliable, byte stream-oriented (SOCK_STREAM)
- Application Example:
	1. Client reads line of characters from keyboard and sends this data
	2. server receives this data, converts to uppercase
	3. server sends modified data
	4. client receives modified data and displays on screen
## Socket programming with UDP
- Requires no "connection" between client and server
	- no handshake, fast and lightweight
	- sender explicitly attaches destination IP and port number to every packet
	- receiver extracts sender IP and port number from received packet so we can respond
### Client/server socket interaction: UDP
![[Pasted image 20250128113822.png]]
## Socket programming with TCP
- TCP requires establishing connection between client and server
	- server listens to connection requests on a specific socket (listening socket)
		- This is a passive socket just for listening for connections
	- client contacts server specifying IP and Port, if connection is established
	- server creates new socket (connection socket) to send and receive data
		- server can communicate with multiple clients though different connection sockets
- Application viewpoint:  
- TCP provides reliable, in-order byte-stream transfer between client and server processes
### Client/server socket interaction: TCP
![[Pasted image 20250128115243.png]]
# Addressing
- Mapping may need to be performed to get
	- port number for a given service name
		- `getservbyname()` returns port number in network byte order; must be converted to host byte order
	- IP address for a given hostname:  
		- `gethostbyname()` returns IPv4 address in network byte order; must be converted to host byte order
	- or translate either one using `getaddrinfo()` `getaddrinfo(NULL, "http", &hints, &res)` `getaddrinfo("www.google.com", NULL, &hints, &res)` hints specifies criteria for selecting the socket address structures returned in the list pointed to by `res`, both of type `addrinfo`
		- **This is the better option to use**
## Structure addrinfo
![[Pasted image 20250128120337.png]]
# I/O operations on sockets
- accept, connect, send, recv are blocking call unless the non-blocking mode is enabled for the socket descriptor using the ioctl system call
	- **accept** blocks when there’s no connection request in the pending connection queue
	- **connect** blocks until the 3-way TCP handshake is done  
	- **send** blocks until data can be queued in the sender buffer  
	- **recv** blocks until data becomes available in the receive buffer
## Socket options
- Options can be set by using `setsockopt()` and read with `getsockopt()` for example:
	- `SO_KEEPALIVE` for periodically probing if connection is still alive  
	- `SO_RCVTIMEO` and `SO_SNDTIMEO` for setting receiving and sending timeouts resp.  
	- `SO_REUSEADDR` for allowing reuse of a local address (e.g., port) immediately after socket is closed  
	- `SO_LINGER` for controlling whether socket closes immediately or waits to send remaining data  
	- Other options can be found at https://linux.die.net/man/7/socket
## Dispatching accepted connections
![[Pasted image 20250128121158.png]]
