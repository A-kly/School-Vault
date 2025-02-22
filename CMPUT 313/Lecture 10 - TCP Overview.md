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
	- packets carry data AND Ack info
- Cumulative Ack
- pipelining
	- congestion and flow control change window size
- Single retransmission timer
- Flow controlled
- connection-oriented
	- handshaking (control messages) initializes sender and receiver state variables
## What is a byte stream
- Sequence of bytes
![[Pasted image 20250206112114.png]]
- Application writes some bytes to socket buffer
- TCP protocol grabs these bytes, once we reach enough of them, it sends them over the network
- Other machine removes header and reconstructs the byte stream from these packets
- **For every socket, we have a send buffer and a receive buffer**
	- Buffer size can change during runtime
## When is a TCP segment sent?
![[Pasted image 20250206112441.png]]
## MSS vs MTU
- **Maximum segment size (MSS)**: maximum size of payload in TCP segments (i.e. application-layer data)
	- negotiated during connection setup
- **Maximum transmission unit (MTU)**: maximum size of link-layer frames, including transport and IP headers
	- for TCP segments: MSS = MTU - IP header - TCP header
	- MTU depends on network technology
	- Ethernet and PPP link-layer protocols have an MTU of 1,500 Bytes
- Typical size of TCP/IP headers is 40 Bytes in total, so a typical value of MSS is 1460 bytes
## TCP segment structure
![[Pasted image 20250206113113.png]]
- Don't need to memorize
- look online lol
- RST
	- Reset
- SYN
	- Synchronize
- FIN
	- For tearing down connection
## TCP sequence numbers
- Indicates where the first bute of this segment fits into byte stream (byte offset)
	- Expressed in terms of # of bytes rather than # of Packets
![[Pasted image 20250206114654.png]]
- Acknowledgement contains sequence number of the next byte expected from the other side
	- TCP uses cumulative ACK
	- ACK can piggyback on data segment
![[Pasted image 20250206114802.png]]
## TCP sequence numbers and ACKs
![[Pasted image 20250206115226.png]]
- ISN in this scenario is `41` for host A and `78` for host B
- Host `A` sends 'C' and ISN plus 1
- First packet sent from `B` to `A` is the sequence number of the received packet, plus `1` indicating that we have received all data up to 43
- We echo back 'C' just because telnet does that
## TCP sliding window and pipelining
- Window size is **maximum contiguous bytes in flight**
	- expresses in bytes not packets
![[Pasted image 20250206115835.png]]
How big should W be?
- definitely less than delay-bandwidth product
- minimum of receiver advertised window to avoid overwhelming receiver and sender congestion window (discussed next lecture) to avoid network congestion
## TCP timeout
- How to set TCP timeout value?
	- longer than rtt, but rtt changes
	- too short:
		- premature timeout, extra retransmissions
	- too long
		- slow reaction to segment loss
- How to estimate RTT
	- SampleRTT
		- measured time from segment transmission until ACK receipt
			- only measured for segments transmitted once
		- SampleRTT will fluctuate due to varying network conditions; we want estimated RTT smoother
			- average several recent measurements, not just current SampleRTT
### Estimating round trip time
- Exponential weighted moving average (EWMA) of SampleRTT
	- `EstimatedRTT = (1- α)*EstimatedRTT + α*SampleRTT`
	- Influence of past sample decreases exponentially fast
	- Typical value: α = 0.125
![[Pasted image 20250206120245.png]]
### Setting timeout value
- Timeout interval: EstimatedRTT plus some safety margin
	- large variation in EstimatedRTT want a larger safety margin
![[Pasted image 20250206120314.png]]
- DevRTT: EWMA of SampleRTT deviation from EstimatedRTT
![[Pasted image 20250206120331.png]]

## TCP Sender (simplified)
![[Pasted image 20250206120353.png]]
## TCP Receiver: ACK generation \[RFC 5681]
![[Pasted image 20250206120457.png]]
## TCP: retransmission scenarios
![[Pasted image 20250206120717.png]]
![[Pasted image 20250206120728.png|250]]
## TCP fast retransmit (with implicit NAK)
![[Pasted image 20250206120847.png]]
# Flow Control
## TCP flow control
 - What happens if network layer delivers data faster than application layer removes data from socket buffers?
![[Pasted image 20250206121021.png]]
## TCP flow control (speed matching)
- Flow control: receiver controls sender, so sender won’t overflow receiver’s buffer by transmitting too much, too fast
![[Pasted image 20250206121312.png]]
# Connection setup and tear-down
## TCP connection management
- Before exchanging data, sender and receiver handshake:
	- agree to establish connection (each knowing the other willing to establish connection)
	- agree on connection parameters (e.g., starting seq numbers or ISNs), set aside buffers
![[Pasted image 20250206121433.png]]
## Agreeing to establish a connection
![[Pasted image 20250206121521.png]]
### 2-way handshake scenarios
![[Pasted image 20250206121546.png|300]]
### 2-way handshake scenario: misinterpreting as new connection request
![[Pasted image 20250206121619.png|300]]
### 2-way handshake scenario: duplicate data
![[Pasted image 20250206121728.png|300]]
## TCP 3-way handshake
![[Pasted image 20250206121758.png]]
### A human 3-way handshake protocol
![[Pasted image 20250206121924.png]]
## Closing a TCP connection
- client and server each close their side of connection
	- sending TCP segment with FIN bit = 1
- respond to received FIN with ACK
	- on receiving FIN, ACK can be combined with own FIN
- simultaneous FIN exchanges can be handled
## Abrupt termination (e.g. server not accepting connection on this port)
- Receiver sends TCP segment with RST bit = 1 to sender
	- this segment is not acknowledged
- If sender sends more data, another TCP segment with RST bit = 1 will be sent
- nmap port scanning tool uses this technique to discover open TCP ports
	- for non-matching UDP port, an ICMP packet is returned