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
# URIs and encoding
- Have to be able to handle everything

#