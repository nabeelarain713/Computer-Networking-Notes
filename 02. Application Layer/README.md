# Chapter 2.  Application Layer
## Section 1.  Principles of Network Applications
### Notes
- There is a difference between network architecture and application architecture.
- The predominant architectural paradigms are:
	- Client-Server Architecture
	- Peer-to-Peer (P2P) Architecture
- In the client-server architecture:
	- An always-on host with fixed ip address which responding to client's requests.
	- There is no way to make two clients talk to each other.
- In P2P architecture:
	- There is not reliance on a dedicated server.
	- The users share the content in a highly decenterliazed network.
- Processes on two different end systems communicate with each other by exchanging messages across the computer network.
	- processes communicating with each other reside in the application layer of the five-layer protocol stack.
- In the context of a communication session between a pair of processes, the process that initiates the communication (that is, initially contacts the other process at the beginning of the session) is labeled as the client. The process that waits to be contacted to begin the session is the server.
- A socket is the interface between the application layer and the transport layer within a host.
- The only control that the application developer has on the transport-
layer side is:
	- the choice of transport protocol
	- perhaps the ability to fix a few transport-layer parameters such as maximum buffer and maximum segment sizes
- To identify the receiving process, two pieces of information need to be specified:
	- the address of the host
	- an identifier that specifies the receiving process in the destination host.
- The trandport-layer protocol provides services that can be categorized into:
	- reliable data transfer
	- throughput
	- timing
	- security
- The Internet (TCP/IP networks) makes two transport protocols available to applications, UDP and TCP.
- The TCP service model includes a connection-oriented service and a reliable data transfer service.
	- It also has a congestion-control mechanism.
- UDP is a lightwight transport protocol, connectionless.
	- It provides unreliable data transfer service.
- Transport Layer Security (TLS) is an application layer enhancement for the TCP layer which provides data integrity, encryption, and end-point authentication.
- An application-layer protocol defines how an application's processes, running on different end systems, pass messages to each other.
	- The type of messages.
	- The syntax of the various message types.
	- The semantics of the fields.
	- Rules for determining when and how a process sends messages and responds to messages.
### Review Questions
- List five nonproprietary Internet applications and the application-layer protocols that they use.
	- Web: HTTP
	- E-mail: SMTP
	- Multimedia Streaming: RTP
	- Remote access: TELNET
	- File transfer: FTP
- What is the difference between network architecture and application architecture?
	- From application's developer point of view, network architecture is fixed and provides certain and well defined services to the application. On the other hand, the application architecture is defined by the application developer based on the nature of the problem being solved and other considerations.
- For a communication session between a pair of processes, which process is the client and which is the server?
	- The client is considered the one who started the converstation first in this session. While the server is considered the one who has the role to respond to this conversation.
- For a P2P file-sharing application, do you agree with the statement, “There is no notion of client and server sides of a communication session”? Why or why not?
	- No. As stated in the text, all communication sessions have a client side and a server side. In a P2P file-sharing application, the peer that is receiving a file is typically the client and the peer that is sending the file is typically the server.
- What information is used by a process running on one host to identify a process running on another host?
	- It uses the information provided by the socket.
- Suppose you wanted to do a transaction from a remote client to a server as fast as possible. Would you use UDP or TCP? Why?
	- It depends on the type of the transaction as the speed is not the only limitation. If this transaction should be gruanteed to reach the other end, then the best choice is TCP. But if not, then UDP is good.
- Referring to Figure 2.4, we see that none of the applications listed in Figure 2.4 requires both no data loss and timing. Can you conceive of an application that requires no data loss and that is also highly time-sensitive?
	- network games
	- network multimedia applications with high quality requirements
	- controlling hight sensitive devices over a network
- List the four broad classes of services that a transport protocol can provide. For each of the service classes, indicate if either UDP or TCP (or both) provides such a service.
	- Reliable data transfer: TCP
	- Timing: None
	- Security: None
	- Throughput: None
- Recall that TCP can be enhanced with TLS to provide process-to-process security services, including encryption. Does TLS operate at the transport layer or the application layer? If the application developer wants TCP to be enhanced with TLS, what does the developer have to do?
	- It operated in the application layer.
	- The developer should include TSL code in order to use.
## Section 2.  The Web and HTTP
### Notes
- The Hyper Text Transfer Protocol (HTTP), the Web's application-layer protocol, is at the heart of the Web.
	- It is defined in [RFC 1945], [RFC 7230], and [RFC 7540].
	- It is implemented in client and server program.
	- End-Systems talk to each other using HTTP messages.
- A Web page consists of objects.
	- An object is a file like: HTML file, JPEG file, etc.
	- The object is addressable by a single URL.
	- The URL consists of a hostname and the object's path.
	- Web browsers implement the HTTP client.
	- Web servers implement the HTTP server like Apache.
- HTTP uses TCP as its underlying transport protocol.
	- HTTP need not worry about lost data or the details of how TCP recovers from loss or reordering of data within the network.
- HTTP is a stateless protocol as it doesn't maintain information about the client.
- The Web uses the client-server architecture.
-  Persistant HTTP uses one TCP connection while the non-persistant uses sperate connnection for each  request.
- HTTP is a communication protocol and is not responsible how the client web browser will interpret the messages.
- In the non-persistant, users can configure some browsers to control the degree of parallelism.
	- Browsers may open multiple TCP connnections and request different parts of the web page over the multiple connections.
- Round-trip time (RTT) is the time it takes for a small packet to travel from client to server and then back to the client.
	- It includes packet-propagation delyas, packet-queuing delays, and packet-processing delays.
- Non-persistant connections has two shortcomings:
	- A new connection is maintained for each requested object.
	- Each object suffers a delivery delay of 2 RTTs.
- There are two types of HTTP messages.
	- Request messages.
	- Response messages.
- Cookies allow sites to keep track of users.
- Cookie technology has four components:
	- A cookie header line in the HTTP response message.
	- A cookie header line in the HTTP request message.
	- A cookie file kept on the user's end system and managed by the user's browser.
	- A back-end database at the web site.
- A web-cache (proxy server) is a network entity that satisfies HTTP requests on the behalf of an origin Web server.
- Conditional GET is a mechanism that ensures the updated version of an object in the cache.
	- An HTTP request message is a so-called conditional GET message if:
		- The request message uses the GET method.
		- The request message includes an "IF-Modified-Since:" header line.
- The primary goals for HTTP/2 are:
	- reduce perceived latency by enabling request and response multiplexing over a single TCP connection.
	- provide request prioritization and server push.
	- provide efficient compression of HTTP header fields.
- HTTP/2 only changed the mechansim of formatting data and transported between the client and the server.
- Head of Line (HOL) blocking problem happens when is there is a heavy data near the top of the response that blocks behind it the small one during a bottelneck congestion.
- HTTP/2 solution for HOL blocking is to break each message into smaller frames, and interleave the request and response messages on the same TCP connection.
- The HTTP/2 framing sub-layer breaks down each HTTP message into independent frames and binary encodes them.
	- Binary protocoles are more effient to parse, lead to slightly smaller frames, and are less error-prone.
	- HTTP/1.1 is an unstructured format made up of lines of text in ASCII encoding.
	- The advantage that HTTP/2 brings is that, by packaging messages into specific frames we can intermingle the messages: here’s a bit of request 1, here’s a bit of request 2, here’s some more of request 1... etc. In HTTP/1.1 this is not possible as the HTTP message is not wrapped into packets/frames tagged with an id as to which request this belongs to.  
- Message prioritization allows developers to customize the relative priority of requests to better optimize application performance.
- HTTP/2 has the ability to send multiple responses for a single client request (Pushing additional objects to the client).
## Section 3.  Electronic Mail in the Internet
### Notes
- SMTP is the principal application-layer protocol for Internet electronic mail.
	- It uses reliable data transfer service of TCP.
- SMTP does not normally use intermediate mail servers for sending mail, even when the two mail servers are located at opposite ends of the world.
- SMTP is a push operation.
- Internet Mail Access Protocol (IMAP) is a protocol for user agents to use manage their mail box in the mail server.
## Section 4.  DNS—The Internet’s Directory Service
### Notes
- The DNS is:
	- a distrbuted database implemented in a heirarchy of DNS servers
	- an application-layer protocol that allows hosts to query the distributed database
- The DNS protocol runs over UDP and uses port 53.
- Services provided by the DNS:
	- Host aliasing: a complex hostname may have a more simple alias and this converting process is provided by the DNS.
	- Mail server aliasing: the MX record permits a company's mail server and Web server to have identical (aliased) hostnames.
	- Load distribution: DNS is used to perform load distribution among replicated server.
- A centerlized database in a single DNS server doesn't scale. So, it is distributed by design.
- DNS servers are classified as follow:
	- Root DNS server: provides the IP addresses of the TLD servers.
	- Top-level domain (TLD) DNS servers
	- Authoritative DNS servers
- DNS exploits DNS caching in order to improve the delay performance and to reduce the number of DNS messages ricocheting around the Internet.
- A resource record is a four-tuple that contains the following fields:
	- Name: it depeneds on the type.
	- Value: it depeneds on the type.
	- Type: A, NS, CNAME, MX.
	- TTL: it determines when a resource should be removed from a cache.
- If Type=A, then Name is a hostname and Value is the IP address for the hostname. Thus, a Type A record provides the standard hostname-to-IP address mapping.
- If Type=NS, then Name is a domain (such as foo.com) and Value is the hostname of an authoritative DNS server that knows how to obtain the IP addresses for hosts in the domain.
- If Type=CNAME, then Value is a canonical hostname for the alias hostname Name. This record can provide querying hosts the canonical name for a hostname.
- If Type=MX, then Value is the canonical name of a mail server that has an alias hostname Name.
- There are only two types of DNS messages:
	- Query message.
	- Reply message.
### Review Questions - Section 2:5
- What is meant by a handshaking protocol?
	- It is a mechanism that allow each server to define himself to the other server after establishing the connection.
- Why do HTTP, SMTP, and IMAP run on top of TCP rather than on UDP?
	- Because all of them need a reliable data transfer that ensures the messages are sent to the destination correctly without error and ordered.
- Consider an e-commerce site that wants to keep a purchase record for each of its customers. Describe how this can be done with cookies.
	- After the client logs into the system, it will assign him  a cookie id which will be sent to the server in the subsequent responeses. This id will be persisted in the database and relates to the user data.
- Describe how Web caching can reduce the delay in receiving a requested object. Will Web caching reduce the delay for all objects requested by a user or for only some of the objects? Why?
	- Web cache will store the content of the request and if the same user or another one ordered the same content it will be served through the cache first before getting it from the original server.
	- The cache will reuce the delay for 20% to 70% in practice.
- List several popular messaging apps. Do they use the same protocols as SMS?
	- Gmail, Outlook, Proton Mail
- Suppose Alice, with a Web-based e-mail account (such as Hotmail or Gmail), sends a message to Bob, who accesses his mail from his mail server using IMAP. Discuss how the message gets from Alice’s host to Bob’s host. Be sure to list the series of application-layer protocols that are used to move the message between the two hosts.
	- Alice send the message to his mail server using SMTP or HTTP protocol.
	- Alice's mail server will put the message in a queue and attempt to send the message to Bob's mail server through SMTP.
	- When Bob's needs to find his messages, he communicate to his mail server through HTTP or IMAP to pull his messages in the mail box.
- What is the HOL blocking issue in HTTP/1.1? How does HTTP/2 attempt to solve it?
	- It is a problem faces the client on requesting a content has huge data near the top of this content. For example, a web page has a video clip near the top of the page. Which makes a blocking for the other smaller objects behind it to load.
	- HTTP/2 make a parallel streaming to the data with multiplexing and interleaving packets by using frames. HTTP/2 divide and package the packets in a new way using binary protocol and provide a mechanism of re-ordering and prioritization.
- Is it possible for an organization’s Web server and mail server to have exactly the same alias for a hostname (for example, foo.com)? What would be the type for the RR that contains the hostname of the mail server?
	- Yes, it is possible.
	- MX records.
## Section 6.  Video Streaming and Content Distribution Networks
### Review Questions
- CDNs typically adopt one of two different server placement philosophies. Name and briefly describe them.
	- Enter Deep.
	- Bring Home.
- Besides network-related considerations such as delay, loss, and bandwidth performance, there are other important factors that go into designing a CDN server selection strategy. What are they?
	- Latency
	- Throughput
	- Failure
	- Cost