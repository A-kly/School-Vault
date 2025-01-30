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
![[Pasted image 20250130112203.png]]

