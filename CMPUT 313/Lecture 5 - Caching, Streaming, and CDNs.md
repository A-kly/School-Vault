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
## Web caches (aka proxy servers)
- Users make browser point to web cache
	- web cache is also client to get objects from server
- Browsers send all HTTP requests to cache
	- if object in cache, return object
	- if object not in cache, request from origin server and return to user
![[Pasted image 20250121113233.png]]
### Advantages of Web caching
- Reduces reponse time for client request
	- due to proximity to user
- reduces trafic to institution's access link
- enables "poor" content provider to more effectively deliver content
	- poor content providers can use web cache instead of buying and building their own servers
### Example
![[Pasted image 20250121113445.png]]
![[Pasted image 20250121113459.png]]
![[Pasted image 20250121113509.png]]
# Calculating access link utilization, end-end delay with cache:
![[Pasted image 20250121114125.png]]
# Video streaming
## Video Streaming and CDNs: context
- Most of internet bandwidth is video streaming
	- netfix, youtube, prime, 80% of residential isp traffic
- Challenge
	- How do we scale this to nearly 1B users?
	- dealing with device heterogeneity
		- network tech, client computing power
- Solution
	- distributed application level infrastructure
		- CDNs that are controlled by streaming companies
## Multimedia: video
- video is sequence of images
	- many arrays of pixels
- lots of redundancy between images
	- Spacial compression = send pixel value and number of pixels to repeat
	- temporal compression = send pixel value and then send only new pixels
![[Pasted image 20250121115030.png|300]]
- **constant bit rate (CBR):** video encoding rate is fixed
- **variable bit rate (VBR):** video encoding rate changes as amount of spatial, temporal coding changes
## Streaming stored video
![[Pasted image 20250121115143.png]]
- Main challenges
	- server-client bandwidth varries over time with changing network congestion levels
	- packet loss and delay due to congestion will delay playout or result in poor video quality
![[Pasted image 20250121115241.png]]
- Continuous playout constraint: during client video playout, playout timing must match original timing
	- … but network delays are variable (jitter), so will need client-side buffer to match continuous playout constraint
- Other challenges:
	- client interactivity: pause, fast-forward, rewind, jump through video
	- video packets may be lost, retransmitted
![[Pasted image 20250121115440.png]]
# Streaming multimedia: DASH
- **Dynamic, Adaptive Streaming over HTTP**
- Server
	- Divides video into chunks (segments)
	- each chunk is encoded at multiple rates
	- different rates are stored in different files
	- files are replicated in many CDN nodes
	- **manifest file** is provided for getting different chunks
- Client
	- periodically estimates client-server-bandwidth
	- consults **manifest** requesting one chunk at a time
		- Chose best coding rate that is sustainable for bandwidth
- Inteligence is at client side
	- **when** we request chunk
	- **what encoding rate**
	- **where do we get chunk from**
- *Streaming video = encoding + DASH + playout buffering*
# CDNS
- How do we stream content to hundreds of thousands of users?
- Option 1 - MEGA server
	- Single point of failure
	- one point of congestion
	- long (and congested) path to distant clients
	- **Does not scale**
- Option 2 - save many copies of video to many distributed sites (CDN)
	- **Enter deep**
		- push CDN servers as deep as possible towards access networks
		- Close to users
		- eg. Akamai: 240,000 servers deployed in 120+ countries
	- **bring home**
		- smaller number of servers in larger