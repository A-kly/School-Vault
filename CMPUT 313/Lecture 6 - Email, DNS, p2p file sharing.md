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
- RFC 2822 defines syntax for e-mail message itself (like HTML defines syntax for web documents)
- Header lines, e.g.,
	- To:
	- From:
	- Subject:
	- these lines, within the body of the email message area different from SMTP MAIL FROM:,RCPT TO: commands!
- Body: the “message”, ASCII characters only
![[Pasted image 20250123112451.png]]
## Retrieving email: mail access protocols
![[Pasted image 20250123112507.png]]
- SMTP: delivery/storage of e-mail messages to receiver’s server
- mail access protocol: retrieval from server
	- IMAP: Internet Mail Access Protocol [RFC 3501]: messages stored on server, IMAP provides retrieval, deletion, folders of stored messages on server
- HTTP: gmail, Hotmail, Yahoo!Mail, etc. provides web-based interface on top of STMP (to send), IMAP (or POP) to retrieve e-mail messages
	- POP deletes message from mail server so you can't access the email on multiple devices
# Domain Name System (DNS)
## Addressing and naming
- name
	- easy to remember, NO character limmit
- ip address
	- used by address datagrams
- Mapping between name and IP required directory service
	- critical internet function
	- adds delay, can be reduced with caching
## Domain Name System (DNS)
- Distributed database implemented in hierarchy of name servers
- Application-layer protocol allowing hosts to query this distributed database (by communicating with DNS servers) to resolve names (address/name translation)
	- DNS runs over UDP and uses port 53
	- often used by other application-layer protocols such as HTTP and SMTP
	- mapping is requested by calling gethostbyname() in UNIX-based systems
- Core Internet function is implemented as an application-layer protocol!
	- complexity at network’s edge
## Services
- Mapping hostname to IP
- host aliasing:
	- `relay1.west-coast.enterprise.com` two aliases: `enterprise.com` and `www.enterprise.com`
- Mail server aliasing
- Local distribution
	- replicate web servers
		- Multiple IPs for one name
	- CDNs
## DNS Structure: Why not centralized design?
![[Pasted image 20250123114018.png]]
## Thinking about the DNS
- humongous distributed database
	- billion records, each simple
- handles many trillions of queries/day
	- many more reads than writes
	- performance matters: almost every Internet transaction interacts with DNS - msecs count!
- organizationally, physically decentralized
	- millions of different organizations responsible for their records
- “bulletproof”: reliability, security

## DNS: a distributed, hierarchical database
![[Pasted image 20250123114150.png]]
- Client wants IP address for www.amazon.com; 1st approximation:
	- client queries root server to find .com DNS server
	- client queries .com DNS server to get amazon.com DNS server
	- client queries amazon.com DNS server to get IP address for www.amazon.com
## DNS: root name servers
- official, contact-of-last-resort by name servers that can not resolve name
![[Pasted image 20250123114422.png]]
- Critically important for internet function
- ICANN (Internet Corporation for Assigned Names and Numbers) manages root DNS domain
![[Pasted image 20250123114603.png]]
## Top-Level Domain, and authoritative servers
- Top-Level Domain (TLD) servers
	- responsible for .com, .org, .net, .edu, .aero, .jobs, .museums, and all top-level country domains, e.g.: .cn, .uk, .fr, .ca, .jp
	- Network Solutions: authoritative registry for .com, .net TLD
	- Educause: .edu TLD
- authoritative DNS servers
	- organization’s own DNS server(s), providing authoritative hostname to IP mappings for organization’s named hosts
	- can be maintained by organization or service provider
## Local DNS servers
- Basically jsut a cache for isp and top level domain servers
- each ISP has local DNS name server; to find yours:
	- MacOS: % scutil --dns
	- Windows: >ipconfig /all
- Local DNS server does not strictly belong to hierarchy
## DNS name resolution: iterated query
- Example: host at `engineering.nyu.edu` wants IP address for `gaia.cs.umass.edu`
- Iterated query:
	- contacted server replies with name of server to contact
	- “I don’t know this name, but ask this server”
	- *contact local dns server, that server goes and asks servers, going down the hirarchy to get authoritative dns server response eventually, and then reply with correct IP*
![[Pasted image 20250123115129.png]]
## DNS name resolution: recursive query
 - Recursive query
	 - puts burden of name resolution on contacted name server
	- heavy load at upper levels of hierarchy?
	- *Ask root dns, which asks tld, which asks authoritative, which all resolves recursively*
![[Pasted image 20250123115344.png]]
- **We can combine these strategies to balance load and not overload single servers**
## Caching DNS Information
- Cache to improve response time
- Include TTL (time to live) to help make sure we don't start serving incorrect IPs
- if we change IPs, we need to wait a bit to make sure that the TTL expire in all required servers so that we can get new IPs to all servers
- we use best-effort name-to-address translation
## DNS records
![[Pasted image 20250123120104.png]]
## DNS protocol messages
![[Pasted image 20250123120238.png]]
![[Pasted image 20250123120257.png]]
## Inserting records into DNS database
- Register name `networkuptopia.com` at dns registrar
	- provide names, IP addresses of authoritative name server (primary and secondary)
	- registrar inserts NS and A RRs into .com TLD server: (networkutopia.com, dns1.networkutopia.com, NS) (dns1.networkutopia.com, 212.212.212.1, A)
- create authoritative server locally with IP address 212.212.212.1
	- type A record for www.networkuptopia.com
	- type MX record for networkutopia.com
## DNS security
- DDOS attack
	- bombard root server with traffic
	- not successful let
	- use local DNS filtering
	- bombard TLD server
		- lil easier and more dangerous
- Spoofing attacks
	- Pretend to be a certain hostname
	- Insert an entry in server or DNS protocol
	- Cache poisoning
	- intercept queries and return bogus replies

![[Pasted image 20250123121115.png]]
# Peer-to-peer file sharing
- Self scalable
	- More demand but also more capacity
- Examples
	- P2P file sharing (BitTorrent), streaming (KanKan), VoIP (Skype)
## File distribution: client-server vs P2P
- Time for file (size F) to be distributed to N hosts?
	- host upload/download is a limited resource
![[Pasted image 20250123121419.png]]
### Assumptions
- Internet core has hella bandwidth
	- all bottlenecks are in access networks
	- core bandwidth not required to be calculates
- bandwidth is fully devoted to distributing file
- only one server has file initially
## Minimum file distribution time: client-server
![[Pasted image 20250123121726.png]]
- server transmission: must sequentially send (upload) N file copies
	• time to send one copy: F/u_s
	• time to send N copies: NF/u_s
- client: each client must download file copy
	- d_min = min client download rate
	- client download time is at least F/d_min
![[Pasted image 20250123121715.png]]
## Minimum file distribution time: P2P
- Another assumption, peers can replicate files and add to upload
![[Pasted image 20250128110659.png]]
- server transmission
	- must upload at least one copy
- client
	- must each download a copy
	- as aggregate must download NF bits
		- max upload rate (limiting max download rate) is u_s + Σ u_i
![[Pasted image 20250128110822.png]]
## Self scalability of p2p
![[Pasted image 20250128111342.png]]
# BitTorrent
- Application layer protocol on top of TCP
- file divided into 256kb chunks
- peers in torrent send/receive file chunks
![[Pasted image 20250128111530.png]]
- peer joining torrent:  
	- has no chunks, but will accumulate them over time from other peers  
	- registers with tracker to get list of peers, connects to subset of peers (“neighbors”)
- while downloading, peers upload chunks to other peers
- peers change peers with who they wanna share data with
- Churn
	- peers can come and go
- once a peer has an entire file, it may (selfishly) leave, or (altruistically) remain in torrent
## BitTorrent: requesting, sending file chunks
- Requesting chunks
	- periodically ask neighbors for a lost of chunks
	- request from peer the missing chunks, starting with the chunk that is replicated the fewest times (rarest chunk first)
- Sending chunks: tit-for-tat trading
	- send chunks at the highest rate to 4 neighbor peers currently sending us our missing chunks at a higher rate
		- other peers are choked (don't receive chunks)
		- re-evaluate top 4 peers every 10 seconds
	- every 30 seconds: randomly select another peer, start sending chunks
		- optimistically unchoke this peer
		- newly chosen peer may join top 4
![[Pasted image 20250128112329.png]]
