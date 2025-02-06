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
