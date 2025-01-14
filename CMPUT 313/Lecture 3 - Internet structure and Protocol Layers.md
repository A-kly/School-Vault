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
	- 
