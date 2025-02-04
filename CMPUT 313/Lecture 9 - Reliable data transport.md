# Why is realiability important?
- Many apps need it
- Design goals
	- Correctness
		- Every packet is received at least once
	- Timeliness
		- each packet is delivered asap!
	- efficiency
		- maximize throughput and avoid wasting bandwidth for unecessary retransmission
# Abstraction -> Implementation
![[Pasted image 20250204110825.png]]
- How it started -> how its going
## Challenge: Building a reliable service on top of unreliable network
![[Pasted image 20250204111040.png]]
![[Pasted image 20250204111051.png]]
## Reliable data transfer protocol (rdt): interfaces
![[Pasted image 20250204111206.png]]
# Reliable data transfer: getting started
- Do sender and receiver repeatedly to implement reliable data transfer protocol (rdt)
- consider only unidirectional data transfer
	- but control info will flow in both directions!
- use finite state machines (FSM) to specify sender and receiver
![[Pasted image 20250204111525.png]]
## rdt1.0: reliable transfer over a reliable channel
- Underlying channel perfectly reliable
	- no bit errors
	- no loss of packets
- Separate FSMs for sender and receiver:
	- sender sends data into underlying channel
	- receiver reads data from underlying channel
![[Pasted image 20250204111608.png]]
![[Pasted image 20250204112120.png]]
![[Pasted image 20250204112132.png]]
![[Pasted image 20250204112142.png]]
![[Pasted image 20250204112157.png]]
![[Pasted image 20250204112209.png]]
## rdt2.0 has a fatal flaw!
- What happens if ACK/NAK gets corrupted?
	- corruption of ACK/NAK can be detected using a checksum too
	- sender does not know what happened at receiver and can’t just retransmit (possible duplicate)
- How to handle duplicates?
	- sender retransmits current packet if ACK/NAK is corrupted
	- sender adds sequence number to each packet
	- receiver discards duplicate packet
![[Pasted image 20250204113034.png]]
![[Pasted image 20250204113049.png]]
> *hella distracted, worked on work availability #review*
![[Pasted image 20250204114253.png]]
![[Pasted image 20250204114309.png]]
![[Pasted image 20250204114336.png]]
![[Pasted image 20250204114413.png]]
![[Pasted image 20250204114545.png]]
- This last example wastes bandwidth but cane be mitigated with longer timer
## Performance of rdt3.0 (stop-and-wait)
![[Pasted image 20250204114800.png]]
![[Pasted image 20250204114908.png]]
![[Pasted image 20250204114917.png]]
# rdt3.0: pipelined protocols operation
![[Pasted image 20250204115123.png]]
## Pipelining: increased utilization
![[Pasted image 20250204115141.png]]
## GBN
### Go-Back-N: sender
- sender: window of up to N, consecutive transmitted but unACKed packets, where N is sender window size (SWS)
	- assign sequence number to each packet: k-bit seq # in packet header
	- ![[Pasted image 20250204115430.png]]
- cumulative ACK: ACK(n): ACKs all packets up to, including seq # n
	- on receiving ACK(n): move window forward to begin at n+1
	- avoids unnecessary retransmision if ACK of a received packet is lost
- timer for oldest in-flight packet
- timeout(n): retransmit packet n and all higher seq number packets in window

### Go-Back-N: receiver
![[Pasted image 20250204120041.png]]
### Go-Back-N in action
![[Pasted image 20250204120104.png]]
## Selective repeat
- multiple packets are in flight due to pipelining
	- receiver individually ACKs all correctly received packets
		-  buffers packets, as needed, for in-order delivery to upper layer
		-  receiver window size (RWS) > 1
- sender:
	-  maintains (conceptually) a timer for each unACKed packet
		-  timeout: retransmits single unACKed packet associated with timeout
	-  maintains (conceptually) window over N consecutive sequence numbers
		-  limits pipelined, “in flight” packets to be within this window
### Selective Repeat: sender, receiver windows
![[Pasted image 20250204120505.png]]
![[Pasted image 20250204120519.png]]
### Selective Repeat in action
![[Pasted image 20250204120535.png]]
