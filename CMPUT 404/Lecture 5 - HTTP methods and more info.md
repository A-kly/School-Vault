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
- 