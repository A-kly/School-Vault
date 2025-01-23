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
## Scenario: Alice sends e-mail to Bob
![[Pasted image 20250123111704.png]]
## Sample SMTP interaction
```
S: 220 hamburger.edu //handshake prt1
C: HELO crepes.fr //handshake prt2
S: 250 Hello crepes.fr, pleased to meet you //handshake prt1
C: MAIL FROM: <alice@crepes.fr>
S: 250 alice@crepes.fr... Sender ok
C: RCPT TO: <bob@hamburger.edu>
S: 250 bob@hamburger.edu ... Recipient ok
C: DATA
S: 354 Enter mail, end with "." on a line by itself
C: Do you like ketchup?
C: How about pickles?
C: .
S: 250 Message accepted for delivery
C: QUIT
S: 221 hamburger.edu closing connection
```

## SMTP: Comparison with HTTP
- HTTP: client pull
- SMTP: client push
- Both have ASCII command/response interaction, status codes
- HTTP: each object encapsulated in its own response message
	- sends binary objects
- SMTP: multiple objects sent in multipart message
	- forces all data to be encoded using 7 bit ascii, including attatchments
	- SMTP server uses CRLF.CRLF to determine end of message
	- SMTP uses persistent connections
## Mail message format