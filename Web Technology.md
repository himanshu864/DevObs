#core

# Syllabus
----
![[Screenshot 2024-09-26 at 2.57.00 PM.png]]

# How the Internet Works?
---

Basically a lot of data is stored at lots of *servers* all over the world.

For example, Google is stored at multiple locations inside many high level computers called servers.

This data could be transferred to us using satellites but that would mean too much delay.

That's why we have laid out *Optical Fiber* cables on over the world. From mountains to under the ocean. These fiber transmit data to our internet routers or nearby cell towers. Though which we can request and update information.

That's basically *Internet*.

To identify unique addresses, each device connected to internet is given as *IP address*.

Similarly all servers / websites are given as IP address. Eg: Google's 8.8.8.8

But these address's are too hard to remember, that's why we assign them with unique *Domain Names*. Eg: www.google.com

And we use a telephone book called *DNS* server (Domain Name System) to find the corresponding IP address.

After getting the IP address, the browser forwards the request to server. And so on..

The server sends the data is the form of a huge amount of 0's and 1's.

This data is sent in small chunks called *packets*. Each packet chooses the shortest path to reach your device and is again reassembled using their Serial numbers.

*Protocols* set the rules for this complex flow of data packets. Like, conversion, address allocation, routers, etc.

# UNIT 1
---

# Internet

	The **Internet** is a global network of interconnected computers that communicate using standard protocols. It allows users to access and share information, use web services, and communicate via emails, chats, and video calls. Think of it as a giant web connecting devices worldwide.

The Internet refers to the global information system that is logically linked together by a globally unique address space based on the Internet Protocol (IP) or its subsequent extensions/follow-ons and is able to support communications using the Transmission Control Protocol/Internet Protocol (TCP/IP) suite or its subsequent extensions/follow-ons, and/or other IP-compatible protocols; and provides, uses or makes accessible, either publicly or privately, high level services layered on the communications and related infrastructure described herein.

## Internet Growth

- **1960s-70s**: Started as ARPANET, a small research network to connect universities.
- **1980s**: Expanded into educational and research networks.
- **1990s**: Became public. The introduction of the **World Wide Web** (WWW) in 1991 by Tim Berners-Lee brought browsers, web pages, and hypertext links, making the Internet user-friendly.
- **2000s-Present**: Massive growth with mobile devices, social media, cloud computing, and IoT (Internet of Things).

The number of users has exploded from a few researchers to over 5 billion people today!

### Owners of Internet

No one person or organization "owns" the Internet. It’s a decentralized system managed by:

1. **ISPs (Internet Service Providers):** Provide access to the Internet.
2. **ICANN (Internet Corporation for Assigned Names and Numbers):** Manages domain names and IP addresses.
3. **Governments and Organizations:** Create laws and policies.
4. **Content Providers:** Companies like Google, YouTube, and Facebook provide services and data that flow through the Internet.

## Anatomy of Internet

When information is sent across the Internet, the Transmission Control Protocol (TCP: the networking-language computers use when communicating over the Internet) first breaks the information up into packets of data. The client computer sends those packets to the local network, Internet service provider (ISP), or online service. From here, the packets travel through many levels of networks, computers, and communications lines until they reach their final destinations. Many types of hardware help the packets on their way. These are:

**Hubs**, which link groups of computers together and let them intercommunicate through multiple ports.  
**Bridges**, which link local area networks (LANs) with each another.   
**Gateways**, which act like bridges, but also convey data between dissimilar networks.  
**Repeaters**_,_ which amplify the data at intervals so that the signal doesn't weaken.  
**Routers**, which ensure packets of data arrive at their proper destination across different technologies, media, and frame formats.  
**Servers**, which deliver web pages and other services as requested.  
**Client computers**, which make the initial request for Internet services, and run applications to handle those services.  
**Cables and/or satellite communications**, which make the hardware connections.  

All hardware units need common operating methods, basic instructions called protocols that specify to all parties how the data will be handled.

# ARPANET

- Created in 1969 by the **Advanced Research Projects Agency (ARPA)** in the U.S.
- Aimed to connect researchers and share data.
- Introduced packet switching (splitting data into packets to send faster and more efficiently).
- First node-to-node communication happened in October 1969 between UCLA and Stanford.

## Evolution of the Internet

- **1970s:** Introduction of TCP/IP protocol (backbone of modern Internet).
- **1980s:** NSFNET (National Science Foundation Network) extended ARPANET for academic use.
- **1990:** ARPANET shut down, and the Internet as we know it began.
- **1991:** The **World Wide Web** was invented by Tim Berners-Lee.

### History of the World Wide Web

- Invented in **1989** at CERN by Tim Berners-Lee to allow researchers to share documents.
- Introduced three core technologies:

1. **HTML (HyperText Markup Language):** For web pages.
2. **HTTP (HyperText Transfer Protocol):** To access web pages.
3. **Web Browser:** Software to view web pages (like Chrome or Firefox).

- Revolutionized how we interact with the Internet, making it accessible and useful for everyone.

### Basic Internet Terminology

1. **IP Address**: A unique numerical label assigned to each device on the Internet (e.g., 192.168.1.1).
2. **Domain Name**: The human-readable address for websites (e.g., `google.com`), linked to IP addresses via DNS.
3. **URL (Uniform Resource Locator)**: The full web address used to access resources (e.g., `https://www.example.com`).
4. **HTTP/HTTPS**: Protocols for transferring web pages. HTTPS is secure (uses encryption).
5. **DNS (Domain Name System)**: Translates domain names into IP addresses.
6. **Bandwidth**: The amount of data transferred over a network in a given time (measured in Mbps or Gbps).
7. **Firewall**: A security tool to block unauthorized access to a network.
8. **ISP (Internet Service Provider)**: A company that provides Internet access.
9. **Router**: A device that connects your local network to the Internet.
10. **Cache**: Temporarily stored data for faster future access.

### Net Etiquette (Netiquette)

Netiquette refers to polite and responsible behavior online:

1. **Respect Privacy**: Do not share someone’s private information without consent.
2. **Avoid Spamming**: Don’t send irrelevant messages or overuse group chats.
3. **Use Proper Language**: Avoid offensive, vulgar, or all-caps text (seen as shouting).
4. **Acknowledge Sources**: Credit original creators for their work (e.g., images, articles).
5. **Think Before Posting**: Ensure your comments/posts are respectful and appropriate.
6. **Secure Your Accounts**: Use strong passwords and don’t share login information.
7. **Stay Safe**: Avoid clicking on suspicious links and report harmful behavior.

### Working of the Internet

The Internet functions like a global postal system, where data is sent in small packets to the destination.

# Switching
---
-  Switching in Computer Networks helps in deciding the best route for data transmission if there are multiple in a larger network.
- One to one connection

## Circuit Switching
- Before data transmission, connection will be established.
- Eg: Telephone Network

![[Screenshot 2024-11-21 at 1.37.38 PM.png]]

1. Connection
2. Data Transmission
3. Disconnection

## Message Switching
![[Screenshot 2024-11-21 at 1.42.49 PM.png]]
- First message is broken into individual pieces, which are then reassembled at the Intermediary node.
- Then message is transferred as a complete unit and forwarded using *Store and Forward* mechanism.
- Not suited for streaming media and real time applications.

## Packet Switching
- Internet is a packet switching network.
- Message is broken into individual chunks called packets.
- Each packet is send individually.
- Each packet will have source and destination IP address with sequence number.
- **Sequence Number** will help the receiver to
	- Sort the packets
	- Detect missing packets
	- Send acknowledgements

### 1. Datagram Approach - Packet Switching
![[Screenshot 2024-11-21 at 1.51.24 PM.png]]
- Connectionless switching
- Each independent entity is called as *datagram*.
- Path is not fixed
- Intermediary nodes take routing decision to forward the packets using their destination information.

### 2. Virtual Circuit Approach - Packet Switching
![[Screenshot 2024-11-21 at 1.54.15 PM.png]]
- Connection Oriented Switching
- A preplanned route is established before sending the message
- Call request and call accept packets are used to establish the connection b/w sender and receiver
- Path is fixed for the duration of a logical connection

## Packet Switching Technology

Packet switching is the backbone of the Internet, dividing data into small pieces (packets) for efficient transfer:

1. **Data Splitting**:
	- When you send a file or request, it is divided into smaller packets (e.g., a video is split into chunks).
	- Each packet contains a header (source and destination info) and payload (the data).

2. **Routing**:
	- Packets travel independently through various routes across the Internet.
	- **Routers** decide the best path for each packet based on availability and speed.

3. **Reassembly**:
	- At the destination, packets are reassembled into the original file, even if they arrive out of order.

4. **Error Checking**:
	- If any packets are lost or corrupted during transmission, the receiving device requests a retransmission.

#### Advantages of Packet Switching
 
1. **Efficiency**: Maximizes network bandwidth as packets use available routes.
2. **Fault Tolerance**: If one route fails, packets can take alternative paths.
3. **Scalability**: Handles large amounts of traffic without crashing.

# IP Address
---

**IPv4** ->

- Internet Protocol
- Every node in computer network is identified with help of IP address.
- Logical Address, since can change based on Location of device.
- Assigned dynamically, but can be manual.
- Represented in decimal and has 4 *octets* (x.x.x.x)
- 0.0.0.0 to 255.255.255.255 (32bits)
- Decimal dotted notation and binary notation.

On UNIX based machines, type `ifconfig` inside terminal. to get your IP address. You'll see something like this

```bash
	inet 192.168.28.235 netmask 0xffffff00 broadcast 192.168.28.255
```

- That `inet` is current IP address. Given to you by your router. In my case, hotspot.
- The first three octets will stay the same in your network, called the *Network Portion*.
- And the last octet will change based on what device isn't assigned to, is the *Host*.

![[Screenshot 2024-11-21 at 2.34.35 PM.png]]

- If you want to exchange on the same network. I.e. IP have same Network Portion. We can directly do that.
- But If the network portion is different, then router will step in to transfer that data.
- Fun fact, Default Gateway is actually your router.

###### Now how many devices can you host on the same network?

- You might think, since network portions remains the same. And its from 0-255.
- 256? WRONG!
- 192.168.1.0 is reserved for the first born Network Address
- 192.168.1.255 is reserved for the chatty *Broadcast Address*. He everything to everyone.
- 192.168.1.1 is reserved for your router, ofc.

So that's makes it a total of **253** different hosts! 

## Layering
---

Layering means decomposing the problem into more manageable components (layers)

Advantages:
- More modular design
- Easier to troubleshoot

**Protocols**: Set of rules that govern data communication

**Layer** **Architectures**
- OSI Reference Model
- TCP / IP Model

# OSI Model
- Open System Interconnection
- It is a model for understanding and designing a network architecture that is flexible, robust, and interoperable (exchange data b/w diff machines of diff types or OS).
- Developed by ISO (International Standards Organization)
- The OSI Model is not a protocol. It is only a guideline.
- The purpose of the OSI model is to show how to facilitate communication between different systems without requiring changes to the logic of the underlying hardware and software.
- The OSI Model was never fully implemented.

![[Screenshot 2024-11-22 at 3.39.13 PM.png]]
- First data is *encapsulated* from Application Layer -> Physical Layer
- Then which is then forwarded using intermediary nodes (routers) which modify only the last three layers. Network, Data Link, and Physical
- Finally data is *de-encapsulated* to extract the data.

### 7 Layers of OSI Model

**Physical Layer**:
- Deals with physical connection
- Transmission of raw binary data (0's and 1's) over physical media (fiber optics, etc)
- Eg: Ethernet Cable, USB, Bluetooth

**Data Link Layer**:
- Ensures error-free data transfer between two devices on same network
- Divides data into *frames*
- Eg: MAC Addresses, Wi-Fi

**Network Layer**:
- Handles routing and addressing of data across different networks
- Divides data into *packets*, assigns IP address, chooses best path
- Eg: IPv4, routers

**Transport Layer**:
- Ensures reliable data delivery between devices
- Divides data into *segments*, provides error recovery, flow control and retransmission of lost packets.
- Eg: TCP, UDP

**Session Layer**:
- Manages and maintains connections (sessions) between devices
- Establishes, maintains and terminates sessions. Synchronous + dialog control
- Eg: APIs, NetBIOS

**Presentation Layer**:
- Translates data into a format application layer can understand
- Data encryption, compression and formatting. (from ACSII to Unicode)
- Eg: SSL/TLS, JPEG, MP3

**Application Layer**:
- Provides services directly to the end user
- Facilitates transfer related services like transfer, email and browsing.
- Acts as interface b/w user application and network
- Eg: HTTP, FTP, SMTP, DNS.

# TCP/IP Model
- Transmission Control Protocol / Internet Protocol
- Backbone of internet.
- Practical model focusing on simplicity and speed.
- Tightly tied to protocols like TCP, IP, UDP.

![[Screenshot 2024-11-22 at 4.21.19 PM.png]]
### 4 Layers of TCP/IP Model

**Application**: Represents data to user, with encoding and dialog control.

**Transport**: Supports communication between different devices across different networks.

**Internet**: Determines the best path thought the network, assigns IP, etc

**Network Access**: Controls the hardware devices and media that make up the network.

### Protocol Data Unit (PDU)
Named according to protocols of TCP / IP suite.

![[Screenshot 2024-11-22 at 4.32.10 PM.png]]

## Routers

A router is a networking device that forwards data packets between different networks.

#### How Routers Handle Packets
 
1. A packet arrives at a router.
2. The router examines the **destination IP** in the packet's header.
3. It consults its **routing table** to determine the next hop.
4. The packet is forwarded accordingly, moving closer to its destination.

##### Router's Role in IP Addressing

- **Default Gateway**: A router acts as a bridge for devices in your local network to access external networks.
- **NAT (Network Address Translation)**: Routers use NAT to allow multiple devices in a private network to share one public IP address for accessing the Internet.

#### Why Routers Are Important

1. **Scalability**: Enable millions of devices across the globe to connect without conflict.
2. **Security**: Can implement firewalls and filter malicious traffic.
3. **Reliability**: Provide alternate paths for data in case of network failures.

## UDP (User Datagram Protocol)

UDP is a lightweight, connectionless protocol used in the Transport Layer of the Internet protocol suite. Unlike TCP, it focuses on speed rather than reliability.

1. **Connectionless**:
- No need to establish a connection before sending data.
- Data is sent as independent packets (called datagrams).

2. **Unreliable:**
- Does not guarantee delivery, order, or error correction.
- Suitable for applications where speed is critical, and occasional data loss is acceptable.

3. **Use cases**:
- Streaming
- Video Gaming
- VoIP : Internet calls

# Internet Addressing Schemes
---

#### 1. Machine Addressing (IP Addressing)

This is how computers and devices are uniquely identified on a network.

1. **IP Address**:
    - Every device on the Internet has a unique IP address.
    - Two versions are commonly used:
        - **IPv4**: 32-bit address (e.g., `192.168.1.1`).
        - **IPv6**: 128-bit address (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).
		
2. **MAC Address**:
    - A unique hardware address assigned to a device’s network interface card (NIC).
    - It operates at the Data Link layer and is formatted like `00:1A:2B:3C:4D:5E`.
	
3. **Private vs. Public Addresses**:
    - **Private IPs**: Used within local networks (e.g., `192.168.0.x`).
    - **Public IPs**: Used to identify devices on the Internet.
	
4. **Dynamic vs. Static IPs**:
    - **Dynamic**: Assigned temporarily by a DHCP server.
    - **Static**: Manually assigned and remains fixed.

#### 2. Email Addressing

Email addressing identifies users for sending and receiving messages.

1. **Format**:
    - An email address has three parts:
        - **Username**: The user’s unique ID (e.g., `john.doe`).
        - **@ Symbol**: Separates the username and domain.
        - **Domain**: Specifies the mail server (e.g., `gmail.com`).
    Example: `john.doe@gmail.com`
    
2. **MX Records**:
    - Mail Exchange (MX) records help route emails to the correct mail server for a given domain.
3. **Protocols Involved**:
    - **SMTP (Simple Mail Transfer Protocol)**: Sending emails.
    - **IMAP/POP3**: Retrieving emails.

#### 3. Resource Addressing

This refers to identifying and locating web resources, like websites or files.

1. **URL (Uniform Resource Locator)**:
    - A URL specifies the location and method to access a resource.
    - Format: `protocol://domain/path`
        - **Protocol**: How to access the resource (e.g., HTTP, HTTPS, FTP).
        - **Domain**: Hostname or IP of the server (e.g., `www.example.com`).
        - **Path**: File or resource location (e.g., `/about.html`).
    Example: `https://www.example.com/products/item123`
    
2. **URN (Uniform Resource Name)**:
    - A persistent name for a resource, independent of its location.
    - Example: `urn:isbn:0451450523` (a book’s ISBN).
3. **DNS (Domain Name System)**:
    - Translates human-readable domain names (`google.com`) into machine-readable IP addresses (`142.250.190.78`).


## Classes of IPv4 Address

![[Screenshot 2024-11-22 at 5.06.44 PM.png]]

- If the first bit of first octet in Binary Notation is 0, then that IPv4 address is Class A
- If first bit is 1, then class B
- If first two bits are 11, then class C
- Similarly 111 -> D
- 1111 -> E

Hence, to find out a class of an IP address. Simply convert first octet of Dotted-decimal notation into binary, and count no. of 1's in the beginning.

# UNIT 2
---
## Email

- Electronic Mail is a method of exchanging messages over the internet.
- Email is send and received using a couple different protocols.

**IMAP** and **POP3** is used for receiving email

**SMTP** is used for sending email

Email basics
1. **Email address** unique identifier for each user
2. **Email Client**: Software program used to send, receive and message email
3. **Email Server**: Computer system responsible for storing and forwarding email

Components of E-Email System:
1. **User Agency (UA):** Program used to send, receiver, reply and read emails.
2. **Messaging Transfer Agency (MTA):**
- Transfers mail from one system to another.
- To send a mail, a system must have both client and system MTA
- It transfers mail to mailboxes of recipients if they share a machine
- Delivers to main to peer MTA if destination mailbox is in another machine using *Simple Mail Transfer Protocol*.
3. **Mailbox:** Fail on local hard drive to collect mails.

After email reaches SMTP server
1. Server will validate the emails contents in accordance to protocol.
2. Now server will lookup IP address of recipients email server on DNS.
3. Now server will establish a connection, and send email is packets.
4. Which will be re-assembled at recipients server and scan email for virus or spam.
5. Finally server will put email to recipients mail box, for him to read.

## Internet Chat

Real time text based communication between two or more users over the Internet. Mainly two types of web chat:
- **Instant messaging**: 1v1 b/w two ppl
- **Chat rooms**: This is a multi-user chat.

Advantage:
- Simple
- Accessible
- Real-time
- Cost-effective

Disadvantage:
- Security
- Improper use
- Spam

## Telnet

- Telecommunication Network
- Telnet is a network protocol that allows you to remotely connect to a computer and establish a two-way text-based communication between two computers.
- Creates remote sessions using TCP / IP protocols, controlled by logged in user to access privileged data and applications on that computer.
- Single operated port, hence only one connection at a time.
- Very old technology, no encryption and low security.
- uses PORT 23

## Usenet

- User Network
- Computer network that allows users to share large files and discuss topics in newsgroups.
- Usenet is a decentralized discussion system that began in 1979 as a text-based system. It has evolved into a network with millions of users and thousands of newsgroups, which are similar to forums or subreddits.

## FTP

- File Transfer Protocol.
- Client/server protocol that allows you to transmit and receive files from a host computer.
- FTP authentication may be done via usernames and passwords.
- Can also use FTP anonymously using "guest" as ID.
- uses PORT 20 for data and 21 for connection control.
- Use TCP for File transfer.
- But no encryption and no security. Use *SFTP* for security.
- data connection is non-persistent. Control is persistent
- Stable

## HTTP

- Hyper Text Transfer Protocol
- PORT 80
- widely used to fetch the webpages on www
- Isn't reliable itself, but uses TCP for reliability.
- Stateless
- HTTP 1.0 Non-persistent
- HTTP 1.1 Persistent
- Commands (head, get, post, put, delete, connect)

![[Screenshot 2024-11-22 at 11.56.42 PM.png]]

# PYQs
---

### 1. Explain Structure of HTML. Write HTML code for expanding Audio and Video

HTML (HyperText Markup Language) is a standard language for creating web pages. It defines the structure and layout of a web document using elements and tags. The basic structure of an HTML document includes:

1. **`<!DOCTYPE html>`**: Specifies the document type and version of HTML (HTML5 is commonly used).
2. **`<html>`**: The root element of the document.
3. **`<head>`**: Contains metadata such as title, links to stylesheets, and scripts.
4. **`<title>`**: Sets the title of the web page, displayed in the browser tab.
5. **`<body>`**: Contains the main content visible on the webpage.

**Example of Basic HTML Structure**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sample HTML Document</title>
</head>
<body>
    <h1>Welcome to HTML</h1>
    <p>This is a basic HTML structure example.</p>
</body>
</html>
```

**HTML Code for Audio and Video Elements**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Audio and Video Example</title>
</head>
<body>
    <h1>Media Elements in HTML</h1>

    <!-- Audio Element -->
    <h2>Audio</h2>
    <audio controls>
        <source src="audio-file.mp3" type="audio/mpeg">
        <source src="audio-file.ogg" type="audio/ogg">
        Your browser does not support the audio element.
    </audio>

    <!-- Video Element -->
    <h2>Video</h2>
    <video controls width="640" height="360" autoplay>
        <source src="video-file.mp4" type="video/mp4">
        <source src="video-file.ogg" type="video/ogg">
        Your browser does not support the video element.
    </video>
</body>
</html>
```

Explanation of Attributes
1. **For `<audio>`**:
    - `controls`: Displays playback controls.
    - `<source>`: Specifies the audio file and format.
    - Text inside the `<audio>` tag provides fallback content.
2. **For `<video>`**:
    - `controls`: Displays playback controls.
    - `autoplay`: Starts the video automatically.
    - `width` and `height`: Specify the dimensions of the video.
    - `<source>`: Provides multiple formats for browser compatibility.

## Remote Login in Web Server
