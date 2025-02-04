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
