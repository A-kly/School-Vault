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
- Reservation based service model vis 