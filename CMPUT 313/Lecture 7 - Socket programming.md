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
