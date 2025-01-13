# Ethernet
- Frame
	- Measure of data transmission
	- 1 ethernet frame is 64-1522 bytes
	- Preamble and SFD are part of package but not frame
# IPV4
- Ethernet is not **routable**
- Long distance and scale communications
- Stateless
	- We don't report if we are connected or not, or if packages are arrived or not.
	- (may be) implemented at other layers
- who has a fixed IPV4?
	- Very few people, because there is such a finite amount of them.
# IPV6
- Similar to IPV4 but with more addresses
- looks like
	- 2001:0db8:0000:0000:0000:0000:0000:0001
	- 2001:db8:0:0:0:0:0:1
	- 2001:db8::1
	- When accessing it, use square brackets, like:
		- https:// [2001:db8::1]/443
# UDP
- *Like someone screaming into a room*
- Stateless
- Lossy
- Real time applications lean towards it
- No connections
- No guarantees
# TCP
