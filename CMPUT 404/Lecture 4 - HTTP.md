# HTTP
- Hypertext - "over" text
- Transfer
- Protocol
- Accepted custom headers to allow for extensions and new features
#review
## HTTP basics
- Uses TCP
- uses port 80 usually
- HTTPS allows encrypted HTTP
- HTTPS uses port 443
- Works over IPV4 or IPV6
- requests are made to addresses called URIs
## URI vs URL
- One is **IDENTIFIER**
	- URI points to  a specific resource on
- one is **LOCATOR**
## URLs
1. scheme
	1. ftp, http or https, etc
2. ":"
3. authority
	1. username@password (optional)
		- Not used much anymore
		- Databases use this sometimes to log in
	2. hostname
	3. :port (optional)
4. path
5. ?query (optional)
6. \#argument (optional)

### URL access
#review ask Angela
- passwords and login in url
	- Vulnerable
- ssh keys
	- can be exposed
### Url analysis
#review Look online for example

## Request methods
- GET
	- gets a resource from server
- POST
	- send data to create or update resource
- PUT
	- Updates a resource from server
- DELETE
	- Deletes resource
- HEAD
	- Gets headers
## STATUS CODES
- 1xx
	- Informal (eg. 100 continue)
- 2xx
	- Successful (200 OK, 201 Created)
- 3xx
	- Redirections (301 Moved permanently, 302 found)
- 4xx
	- Client errors (404 not found, 400 bad request, 401 unauthorized)
- 5xx
	- Server errors (500 internal server error)
## HTTP Headers
- Request headers
	- Client to server
- Response headers
	- Server to client
- http uses port 80, https uses port 443

## Queries
- URLs have a query portion
- can have one or more arguments
- Usually `key=value&key2=value2`
- Other formats exist, using `;` or `&` separator or having just a string.
- starts with `?`
## Paths
- Can be absolute or relative
- absolute
	- Normal urls, from root to resource
- Relative
	- Uses linux 'dot' notation
	- eg. `http://[::1]:8000/images/../index.html`
		- root dir -> images dir ->back to root -> render index.html

- absolute authority
	- Like normal
- implied authority
	- used in html `href`, references resource relative to current directory/page
	- with relative path, don't use leading slash
	- with absolute path, use leading slash
## SCHEME
- http:
- https:
- spotify:
- tel:
- mailto:
## Fragments
- Links to part of a page
- uses `#`
## URIs and encoding
- Have to be able to handle everything
# PUT
- Like POST but does not handle the request, it is the request
- Sending a resource, putting it on the URI link that I'm calling
- adds / relaces new entities in database
# DELETE
- Opposite of PUT
- Erases the value of the URI
- request body is usually empty

# HTTP user agents
- Client/browser
	- Tells server about kind of browser that is accessing page
- Can allow for fingerprinting and tracking, this may be nice sometimes for preferences or personalization
# Status codes
- 100
	- info
- 200
	- success
- 300
	- redirection
- 400
	- server error
- 500
	- client error
## Info codes - 100s
- Everything is going okay, we are continuing
- 101
	- Switching protocols
	- switching from unencrypted to encrypted protocol
## Success - 200s
- we were successful
- 200
	- OK
- 201
	- responds to PUT
	- resource created
- 202
	- accepted, like ok but not finished yet
- 203
	- ???? #review 
- 204
	- good request, no content
- 205
	- like 204 but we should clear the page
- 206
	- partial content
	- client has to do GET with a range header to continue a big download that was interrupted
## Redirect - 300s
- we redirect for many reasons, quite useful
- 300
	- Multiple choices for user to browse to
- 301 
	- moved permanently
- #review 
> *the rest are online*

- Enterprise may have guidebook for error codes
- if we use cookie based login, usually use 302 or 307 if the cookie is expired
# Accepts
- Specifies the kind of media the client can receive
## Accept-charset
- specifies encoding
## accept-encoding
- specifies compression format
> *focus was kinda bad this day, and all notes are online*

# Administrivia
- **==Final is April 16th at 1:00 pm==**
	- final is 1.5 hours
- TAs have updated the pelican repository, look online and pull again (url/repo might be different???)
- to get python to work on cybera:
	- hub.docker.com
		- Search for python to get a docker container with the right python version
		- `docker pull python` then add tag to pull an entire container
	- conda is used to create virtual conda environments with a specific python version
		- look up conda cheat sheet to find info on it
		- mini-conda is good
		- can be big in terms of file size so maybe use on local machine
- Make sure to use NVM for the node lab assignment
# Server headers
- `Access-Control-Allow-Credentials: true`
	- whether we alow js running in browser to make requests with cookies
- `Access-Control-Allow-Headers: true`
	- same as the other one for headers
- *more online, too fast, can't keep up!*
- Security-policy
	- Make sure that the connection is safe, and validate input in text boxes to make sure that there isn't insecure test input
- Security policy reporting
	- if there is a violation in the security policy, send a report to a specific url
- Disconnections (aside)
	- If ghosted, Passive disconnection
	- If formal breakup, active disconnection
- keep alive
	- keep connection alive for a max of `time` if no responses
- Proxy authenticate & authorize
	- Gives user power to interact with server
	- Ask user to log into proxy server, as a first line of defence
	- proxy is middle man between server and client
	- Acts as a load balancer sometimes too
- referrer-policy:  no-referrer-when-downgrade
	- when i go back a URI directory, don't refer
- Extra headers
	- Start with `X-`
	- we are not abiding by a given protocol, we are adding on top of the protocol ourselves
- Warnings
	- warn about something
	- code means something specific
	- 199 is whatever you wanna make it
# Proxies
## Forward
- Forwards incomming http requests to you
- rare
- set up by you
- Basically like a consumer VPN
## Reverse proxy
- common
- forwards http requests to server
- how that one girl explained how she accessed cybera throught the cybera vpn
- caddy & nginx
	- use these for project
# Proxies
## Reverse
- Caching
- CDN
	- keep content near user
- Load balancing
- TLS
	- encryption
- Fail-over
	- Has redundancy
![[Pasted image 20250131131429.png]]
![[Pasted image 20250131131525.png]]

