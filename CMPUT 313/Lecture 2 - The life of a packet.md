# Network edge
- Network edge
	- Host: client and servers
- Access Networks
	- wired and wireless links to connect nodes
# Network Core
- Mesh of interconnected routers
	- High speed links
- **Packet Switching**
	- Host breaks application-layer messages into packets and the network forwards packets from one router to the next, across links on path from source to destination
# Links: Physical media
- Twisted pair
	- insulated copper wire
- coaxial
	- concentric copper conductors
	- bidirectional
- fiber optic
	- glass fiber
	- high speed
	- low error rate
- wireless radio
	- "bands" of electromagnetic spectrum
	- Wi-Fi, wide-area, Bluetooth, terrestrial microwave, satellite
# How is data organized in a network?
- data is chunked into packets before it is sent through link
- Each packet has:
	- Payload which is meaningful to the end host
		- chunks of data (bits) in network byte order
	- Header which is meaningful to network and end host
		-  metadata describing how data must be delivered
		-  in practice, there are multiple headers
## Link properties
- **bandwidth/transmission rate**
	- \# bits sent per second
- **propagation delay**
	- time for bit to travel along link
- **bandwidth-Delay Product (BDP)**: amount of bits that can travel in the link (bits/second * seconds)
	- AKA **Link capacity**
	- ![[Pasted image 20250109111757.png]]
- **Packet transmission delay**
	- time it takes to transmit all bits in a packet
- **transmission delay** = packet size (in bits) / link bandwidth (in bits per second)