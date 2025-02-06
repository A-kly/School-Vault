# Technoques for reliability
- Checksums
	- one bit errors
- Acks, timeout, retransmission
	- dealing with packet loss
- Sequence number
	- detecting duplicates and reordering
# End-to-end principle
- Where do we implement reliability?
	- link-by-link
		- Cannot be perfectly reliable, caused by failures and bugs
	- so end-to-end checks are needed anyways
	- end-to-end reliability
		- Ensures end points are in correct state
![[Pasted image 20250206111102.png]]

## Ensuring link-by-link reliability
- Unnecessary
- adds complexity
- can improve performance sometimes tho
	- Reducing per-link drop rate
# TCP: overview
- Point-to-point
	- one sender and one receiver
- Reliable, in order byte stream
- full-duplex service
	- Bidirectional data flow
	- packets carry data AND Ack ifo
- Cumulative ACk
- pipelining
	- congestion and flow control change window size
- Single retransmission timer
- Flow controlled
- connection-oriented
	- handshaking (control messages) initializes sender and receiver state variables