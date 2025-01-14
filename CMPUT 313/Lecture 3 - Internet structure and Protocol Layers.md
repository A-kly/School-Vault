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