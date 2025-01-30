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
- "no frills" and "bare bones" extension of Internet Transport Protocol (IP)
- best effort
	- we may lose data or
	- out of order delivery
- Connectionless
	- no handshaking between UDP sender and receiver
	- each UDP segment handled independently of others
![[Pasted image 20250130114608.png|300]]
- UDP used in:
	- some streaming multimedia protocols (loss tolerant and rate sensitive)
	- DNS
	- SNMP
- If reliable transfer needed over UDP (e.g., HTTP/3):
	- add needed reliability at application layer
	- add congestion control at application layer
- Described in [RFC 768]
	- Look online for spec
## UDP: Transport Layer Actions
![[Pasted image 20250130115247.png]]
![[Pasted image 20250130115257.png]]
## UDP segment header: 4 fields
![[Pasted image 20250130115607.png]]
- Min and max length
	- **Min:** 8 bytes (just the headers)
	- **Max:** 2^16 - 1 bytes (in one IP message)
		- minus 20 bytes for IP header
## End-to-end error detection: UDP checksum
- Goal: detect errors (i.e., flipped bits) in transmitted segment
![[Pasted image 20250130120211.png]]
### Internet checksum
- **sender**:
	- treat contents of UDP segment (including UDP header fields and IP addresses) as sequence of **16-bit integers**
	- **checksum:** addition (one’s complement sum) of segment content
	- checksum value put into UDP checksum field 
- receiver:
	- compute checksum of received segment and received checksum itself
	- check if computed checksum equals 1111111111111111
		- not equal (at least one 0 bit) - error detected
		- equal - no error detected. But maybe errors nonetheless? More later ….
#### example
![[Pasted image 20250130120705.png]]
- weak protection!
![[Pasted image 20250130120742.png]]
## UDP Summary
- “no frills” protocol
	- segments may be lost, delivered out of order
	- best effort service: “send and hope for the best”
- Why to build an application over UDP?
	- no setup/handshaking needed (no RTT incurred)
	- no congestion control (no throttling, immediate transfer)
	- can function when network service is compromised
	- helps with reliability (checksum)
- It is possible to build additional functionality on top of UDP in application layer (e.g., HTTP/3)
# Evolution of UDP
## QUIC: Quick UDP Internet Connections
- Application-layer protocol, on top of UDP
	- increase performance of HTTP
	- deployed on many Google servers, apps (Chrome, mobile YouTube app)
![[Pasted image 20250130121316.png]]
> *this photo is missing the second half, we combine `HTTP/2` and `TLS` to be `HTTP/3`*  #review

- Adopts approaches for connection establishment, error control, congestion control
- error and congestion control: “Readers familiar with TCP’s loss detection and congestion control will find algorithms here that parallel well-known TCP ones.” [from QUIC specification]
- connection establishment: reliability, congestion control, authentication, encryption, state established in one RTT
- Multiple application-level “streams” multiplexed over single QUIC connection
	- separate reliable data transfer, security
	- common congestion control
### QUIC: Connection establishment
![[Pasted image 20250130121424.png]]
### QUIC: streams: parallelism, no HOL blocking
![[Pasted image 20250130121439.png]]
