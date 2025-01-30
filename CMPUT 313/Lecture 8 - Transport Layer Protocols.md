# Transport services and protocols
- Provide logical communication between application processes on different hosts
- Transport protocol actions
	- sender breaks app message into **segments**, passes to network layer
	- receiver reassembles segments into messages, passes to application layer
- TCP and UDP are protocols in this layer
# Transport vs. network layer services and protocols
- Transport layer
	- communication between processes on the same or different hosts
	- many processes run on each host
	- relies on and enhances network layer services
- Network layer
	- communication between hosts
	- ![[Pasted image 20250130111404.png]]
## Transport Layer Actions
![[Pasted image 20250130111122.png]]
![[Pasted image 20250130111134.png]]

# Transport protocols
- TCP: transmission control protocol
	- reliable, in-order delivery
	- congestion control
	- flow control
- UDP: user datagram protocol
	- unreliable, unordered delivery
	- no-frills extension of "best-effort" IP
- Services not available in any protocols
	- delay guarantees
	- bandwidth guarantees
# Multiplexing/demultiplexing
![[Pasted image 20250130111643.png]]
![[Pasted image 20250130112137.png]]
- How did transport layer know to deliver message to Firefox browser process rather than Netflix or Skype process?
- How did transport layer know to deliver message to a specific thread/process of HTTP server?
![[Pasted image 20250130112203.png]]
![[Pasted image 20250130112350.png|300]]![[Pasted image 20250130112435.png|300]]
## How demultiplexing works
- Host gets IP datagram
	- contains source and destination IP
	- contains one transport-layer segment
	- contains source and destination port number
- **Host uses IP address & port number to direct segment to appropriate socket**
![[Pasted image 20250130112621.png|400]]
### Connectionless demultiplexing (UDP)
- For UDP
- When we create sockets, we specify a local port number
- when we create datagram to send over UDP, must specify...
	- desination IP
	- port number

- When receiving UDP segment..
	- check destination port number
	- direct segment to socket with that port number
- `IP/UDP` datagrams with **same dest. port #**, but *different source IP addresses and/or source port numbers* will be directed to ==same socket at receiving host==
#### Connectionless demultiplexing: Python example
![[Pasted image 20250130112925.png]]
### Connection-oriented demultiplexing (TCP)
- For TCP
- TCP connection is identified by a 4-tuple
	- source IP address
	- source port number
	- dest IP address
	- dest port number
- **Demux:** receiver uses all four values to direct segment to appropriate socket
- Concurrent server supports many simultaneous TCP connections
	- each connection is identified by its own 4-tuple 
	- each connection socket is associated with a different connecting client, so client IP address and port number can be used for demultiplexing
#### Connection-oriented demultiplexing: example
![[Pasted image 20250130113336.png]]
## Summary
- Multiplexing and demultiplexing are done based on segment and datagram header field values
- **UDP:** demultiplex using destination port number only
- **TCP:** demultiplex using 4-tuple: source and destination IP addresses, and port numbers
- Multiplexing/demultiplexing happen at all layers
# UDP: User Datagram Protocol
