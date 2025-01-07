- Goals
	- Write protocols
	- understand internet and it's architecture
	- Learn socket programming
	- Using emulator and networking tools to learn protocols and applications
- Evaluation
	- Assignments ( 3 of them, 15% each)
		- Firm deadlines, no low score dropped, 20 point deduction if submitted up to 48hrs late
		- ==CANNOT DISCUSS solution==, borrow code, look at code, hire people or ==submit LLM generated code==.
		- Assignment is due in the early evening
		- ==CONSULT TAs BUT NO ONE ELSE==
	- Midterm (20%), Thursday, Feb. 13th, during class ==closed book==
	- Final Exam (35%) - ==Closed book==
		- Covers ALL class content, before and after midterm
		- Date announced later
- Other policies
	- Ask all questions on canvas forum
	- No AI generation Models
	- Assignments are on GitHub classroom
	- Appeals for graded work are within one week of receiving grade, Contact TA
	- all course materials are copywritten
	- see course outline for more policies

# Intro to computer networks
## what is a computer network
- Form of communication network
- **nodes:** devices
- network carries **packets** (chunks of data)
- **Links:** connections between devices
	- point to point connections (one wire connecting each computer to another computer)
	- Multiple access connections (Data that is sent can be seen by any other computer connected to the same line)
## Scaling more nodes
- Switches/routers connect multiple networks and forward packets
	- Can scale to be more and more nodes
	- These, all connected are called an **Access Network**
	- **Edge routers** connect between *access networks*
## Protocols
- Defines syntax and semantics of messages sent over a network
	- Format, order, actions taken 
	- TCP is an example of this
	- Data transfer between distributed entities in a network is governed by protocols

## What is the internet?
- Connects existing netowrks that use different internet technologies
- Nowadays connects over 100,000 independent networks
	- Each netowrk often represents administrative boundaries with competing intrests, so the internet is a federated system
	- no internal changes required to connect to internet
	- interoperability is biggest goal
### Nuts and bolts
- Billions of computing devices
	- end hosts, nodes, systems
	- running network apps at internet's edge
- Packet switches
	- Forwards packets, routers, switches
- Communication links
	- Fiber, copper, radio, satellite
- Networks
	- Collections of devices, routers and links, managed by organization
- Internet
	- Netowork of networks
- Protocols
	- control sending and receiving of messages
- Internet standsards
	- Developed by internet engineering task force (IETF) called Request for Comments (RFC)
	- nearly 9,000 RFCs
![[Pasted image 20250107115528.png|400]]

