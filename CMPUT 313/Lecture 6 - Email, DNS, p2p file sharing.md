# Email
- Components
	- User agents
	- mail servers
	- protocols: SMTP, IMAP, etc
![[Pasted image 20250123111255.png]]
## User agents
- Composing, reading, forwarding and replying to mail messages
	- outlook, apple mail etc.
- outgoing and incoming messages stored on server
## Mail servers
- Contains users incoming messages
- contains queue of outgoing messages if we cannot transfer immediately
## SMTP protocol
- between mail servers to send messages
- client is sending main server
- servers receiving mail server
## IMAP protocol
- between mail client and mail server to retrieve mail
# SMTP RFC
- Uses tcp on port 25
- Three phases of transfer
	- SMTP handshaking
	- SMTP transfer of messages
	- SMTP closure
- Command/response interaction (like HTTP)
	- commands: ASCII text
	- response: status code and phrase
- Two handshakes (tcp for transport layer integrity and SMTP for application layer integrity)
# Scenario: Alice sends e-mail to Bob
![[Pasted image 20250123111704.png]]
