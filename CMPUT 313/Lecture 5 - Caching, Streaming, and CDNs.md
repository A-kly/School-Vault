# Cookies: tracking a user’s browsing behavior
![[Pasted image 20250121110059.png]]
## First-party versus third-party cookies
- Cookies used to..
	- Track user bejaviour on a website (first party)
	- Track user behaviour across websites (third party)
	- tracking may be invisible to user, e.g. rather than displayed ad triggering HTTP GET to tracker, could be an invisible link
- Third-party tracking via cookies:
	- disabled by default in Firefox and Safari browsers
	- to be disabled in Chrome
## GDPR (EU General Data Protection Regulation)
![[Pasted image 20250121110541.png]]
## Other security and privacy considerations
- Cookie requests can be sent over a secure connection, i.e. encrypted
	- using HTTPS (aka HTTP over TLS)
- Cross-site requests to set a cookie can be declined
	- to prevent third-party cookies
# Pipelining in HTTP/1.1
- Allowing multiple requests to be pipelined without waiting for responses
- persistent connection
- successive GET requests
![[Pasted image 20250121110942.png]]
# Beyond HTTP/1.1: HTTP/2
- Lower delay in multi-object http requests
- 1.1 introduced multiple-pipeline GET
	- server response to FCFS order (first come first serve)
	- small objects that are queued after large objects cause Head-of-line (HOL) blocking
	- retransmitting TCP causes slowdowns
- 2 increases flexibility at server in sending objects to client
	- methods, codes, headers are unchanged from 1.1
	- transmission order is now up to server
	- server can push unrequested objects
	- 