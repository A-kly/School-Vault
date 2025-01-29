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
- `TE: gzip`
	- Like `Accept-Encoding` but with a proxy
- `Upgrade-Insecure-Requests: 1`
	- 