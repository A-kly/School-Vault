# Canonical approaches to sharing network resources
## Sharing network resources
- network has many simultaneous flows
	- Shared resources can be bottlenecked
	- sizing shared resources (links, routers) to reduce congestion is an important thing to worry about
- **Observation:** peak average demand from N hosts, is typically much less than the sum of the peak demand of these hosts 
	- Peak demands for each host happens at different times
	- shared resources are **statistically multiplexed**, i.e. we don't plan for worst case
	- We can study the probability that all hosts are at peak demand
## Two approaches to share resources
- Best effort service model via packet switching (this is the default)
	- send packets and hope for the best, compete for bandwidth
	- resources are shared between packets in network
	- packets can be dropped, no guarantees
- Reservation based service model via circuit switching (telephone networks and ATMs)
	- reserve bandwidth on a **virtual circuit (path that the data takes, based on maximum demand of source)** between source and destination at start of **flow**
	- source sends reservation request to each router on path to reserve bandwidth, if all requests work, we establish a virtual circuit, packets are transferred, and then a tear down message is sent to tear down virtual circuit at end of flow
		- can be static or dynamic
	- Resources dedicated to this flow are not shared with other flows, so we can guarantee performance
### Circuit switching
![[Pasted image 20250114111549.png|400]]
- end to end resources allocated and reserved for a "call" or flow between source and destination
- eg. each link has 4 circuits
	- the flow goes from source, through link 2, to another switch/router, through link 1, to destination
	- reserved so quality is guaranteed
	- links are idle if not used
- Used in traditional telephone networks
#### FDM and TDM
- **Frequency division multiplexing (FDM)**
	- Slice connection into frquency bands, each call is allocated a band, and is limited by the section's bandwidth
![[Pasted image 20250114112138.png]]
- **Time division bandwidth (TDM)**
	- time is divided into slots
	- Call is allocated time slots and can transmit on a widerband for a limmites amount of time
![[Pasted image 20250114112149.png]]
### Packet switching versus circuit switching
- Does packet switching "win"?
	- It's simpler, no setup and teardown
	- faster recovery from a switch failure
		- in circuit switching, if link goes down we have to restart setup
	- better for bursty traffic
		- more hosts can share network resources because they do not reserve network capacity based on their peak demand
	- Does not provide performance guarantees, can have excessive congestion
		- Protocols needed for reliable data transfer
- **Packet switching is the default for these reasons**
# Internet structure
- Network of networks
- Hosts -> access networks -> tier 3 ISPs -> tier 2 ISPs -> tier 1 ISPs (global)
	- Causes hierarchical network
- Connecting all access networks to all other access networks is not possible
	- Using a hierarchy is better
	- Global ISPs are good to fix this
	- multiple global (Tier 1) ISPs exist and compete
		- They also have to be connected
		- We use **Internet exchange points** for this
			- These are links between ISPs in the same level.
			- They use **peering links** to connect them
	- Regional ISPs (Tier 2) can also use internet exchange points and peering links
	- **CDNS** can bypass T2 and T3 ISPs to connect to access networks
![[Pasted image 20250114113552.png]]
- At “center”: small number of well-connected large networks  
	- “tier-1” commercial ISPs (e.g., Level 3, Sprint, AT&T, NTT), national & international coverage  
	- content provider networks (e.g., Google, Facebook): private network that connects its data centers to the Internet, often bypassing tier-1 and regional ISPs
## Network modularity
- how do we decompose task of transferring data?
- What is needed to get packets between processes on different hosts?
### Protocol layers and reference models
- Networks have many pieces
- how do we organize and talk about network structure
> *look at example online, I'm not gonna write it out lmao*
![[Pasted image 20250114114308.png]]
- Only peers understand the same things (how to use letter, envelope, FedEx envelope)  
	- aides use envelope but don’t know what’s written in letter  
	- FedEx employees use FedEx envelopes but don’t know who will receive letter in company B
- Air travel is another example
	- ![[Pasted image 20250114114457.png]]
	- each layer implements a service  
		- via its own internal-layer actions  
		- relying on services provided by layer below (i.e. it builds on that layer)
#### Why layering?
- Easier approach to design complex systems
- Explicit structure alows identification, and relationship of system pieces
	- Uses reference models
- modularization eases maintenance, updating of system  
	- change in layer's service implementation: transparent to rest of system
### Layered Internet protocol stack
![[Pasted image 20250114114822.png|200]]
- **application:** supporting network applications  
	- HTTP, IMAP, SMTP, DNS, NTP
- **transport:** process-to-process data transfer  
	- TCP, UDP
	- Packet loss, delay, and congestion is felt roughly here
- **network:** global packet delivery – routing of datagrams from source to destination
	- IP, routing protocols
	- Only one communication protocol here, IP
- **link:** local packet delivery – data transfer between neighboring network elements  
	- Ethernet, 802.11 (WiFi), PPP
- **physical:** bits “on the wire”
## Global VS local packet delivery
![[Pasted image 20250114115804.png]]
## Services, layering and encapsulation
![[Pasted image 20250114115831.png]]
- Application just has messge
- transport layer adds a header indicating the source process and destination process
	- This is the **logical port number**
![[Pasted image 20250114120107.png]]
- Network layer adds another header for IP addresses
![[Pasted image 20250114120143.png]]
- Link layer adds ANOTHER header layer containing MAC address for the network access cord.
### This entire system is like pealing an onion or a Matryoshka doll
![[Pasted image 20250114120453.png]]
- message
- segment (includes port header)
- datagram (includes ip address)
- frame (includes mac address)
### Distributing layers across network
![[Pasted image 20250114120754.png]]
- No real distinction between routers and switches anymore
- Switch looks at link layer and sends to router
- routers look at network layer and send to destination
#### Protocol diagram for HTTP
![[Pasted image 20250114121319.png]]
- Routers may have multiple interfaces
- ![[Pasted image 20250114121341.png]]
- Between routers, we can use different protocols, for example OTN
- We need to map ethernet frames to OTN frames
	- Encapsulation of ethernet frames by OTN frames
## ISO/OSI reference model
- Two layers not found in Internet protocol stack!
- **presentation:** allow applications to interpret meaning of data, e.g., encryption, compression, machine-specific conventions
- **session:** synchronization, checkpointing, recovery of data exchange
- Internet stack “missing” these layers!  
	- these services, if needed, must be implemented in application  
	- needed?
![[Pasted image 20250114121556.png|200]]
