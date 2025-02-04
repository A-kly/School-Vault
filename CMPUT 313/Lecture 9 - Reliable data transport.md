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
