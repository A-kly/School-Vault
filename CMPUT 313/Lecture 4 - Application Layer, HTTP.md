# How are the layers implemented?
![[Pasted image 20250116110423.png]]
# Network Applications
- Social networks
- Web browsers
- Text
- Email
- Remote login
- p2p file sharing
- video streaming
- multiplayer games
- real time video (zoom) or VOIP - interactive
## Creating an application
- programs that:
	- run on different end systems
	- communicate over the network
- No need to write software for network core devices
	- They just don't run application and transport layer
# Client-server paradigm
- Server
	- Always-on host
	- often has a permanent IP
	- often in data centers for scaling
- Clients
	- Communicate with server
	- may be intermittently connected
	- may have dynamic IP
	- do NOT communicate with each other directly
	- protocols
		- HTTP, IMAP, FTP, etc
## Peer 2 Peer architecture
- No always on server
- arbitrary end systems (peers) communicate directly
- peers request services from other peers in return for other services
	- self scalable
		- new peers increase both demand and capacity
- IP addresses can change
	- We need to come up with a better way to track hosts consistently