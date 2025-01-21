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
- Allows 