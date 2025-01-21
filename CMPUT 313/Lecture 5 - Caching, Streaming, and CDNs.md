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
	- we can now divide objects into "frames" to mitigate HOL blocking
## HTTP/2: mitigating HOL blocking
- HTTP 1.1: client requests 1 large object (e.g., video file) and 3 smaller objects
![[Pasted image 20250121111448.png]]
## HTTP/2: mitigating HOL blocking
- HTTP/2: objects divided into frames, frame transmission interleaved (known as multiplexing)
![[Pasted image 20250121111527.png]]
# HTTP/2 to HTTP/3
- 2 over single TCP connection means
	- recovery from packet loss still requires retransmisson
		- as in 1.1, we are encouraged to open multiple parallel TCP connections to reduce stalling and increase throughput
	- no security over tcp
- 3 adds security, object error and congestion protocol (more pipelining) over Quick UDP internet Connections or QUIC
	- More on 3 in transport layer

# Lots of requests for loading a page
![[Pasted image 20250121111935.png]]
## Types of caching
- **Private**
	- local cache in browser
	- reduces delay on subsequent accesses, e.g. clicking on back button in browser
- **Proxy** (shared)
	- in-network cache installed by network operator
	- reducing bandwidth (and delay) required between network and origin server when multiple people locally access the same Web object
- **Managed** (shared)
	- in-network cache run by application provider, placed close to end users
	- application provider can redirect requests to servers that are closer, not overloaded, etc. using DNS (discussed later)
## How do we avoid a stale cache?
- Origin tells cache about length of time we can cache this object
	- `Cache-Control: no-cache`
	- `Cache-Control: max-age=<seconds> `or `Expires: <date-and-time> `(supported in HTTP 1.1)
- Poll origin before using Cached copy in request header
	- `if-Modified-Since: <date>` or `If-None-Math: "<etag>"` (this is a hash of the object)
- Origin server notifies client if data changes 
	- Server is responsible
	- requires tracking of clients (kinda impossible)
	- not used in HTTP
## Conditional GET
![[Pasted image 20250121112950.png]]

