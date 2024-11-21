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

# Unit 1
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
# Packet Switching Technology

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

