#core 

# Syllabus

![[Screenshot 2025-01-02 at 1.12.06 PM.png]]

---
# Unit 1

## Computer Networks

It is a telecommunication network, which allows autonomous digital devices (nodes) to exchange data between each other using either wired or wireless connections to share resources (hardware or software) interconnected by a single technology e.g. internet.

> Internet means empowerment
### Goals of Computer Networks

1. **Facilitating Communication**: Swift communication between individuals and organizations. Eg: video conferencing, emails, sms, etc.
2. **Resource Sharing**: Allows users to share hardware and software resources.
3. **Data Storage and Access**: Centralized storage system that allow data access from any connected device. Easy backup and recovery.
4. **Cost Efficiency**: Reduces cost by sharing resources and avoiding duplication of h/w and s/w.
5. **Reliability and Redundancy**: Enhanced reliability though alternate paths and redundant systems in case of failure.

### Applications of Computer Networks

1. **Business and Commerce**: banking, stock trading, e-commerce, etc. Remote working and global collaboration.
2. **Education**: E-learning, online exams, virtual classrooms. Research and more knowledge sharing.
3. **Healthcare**: Telemedicine, electronic health records, remote patient monitoring, etc.
4. **Government Services**: Online public services, secure communication between agencies.
5. **Entertainment**: Online gaming, streaming services, social media, etc.
6. **Scientific Research**: Worldwide data sharing and research collaboration.
7. **Travel**: GPS, online booking, etc.

---
## Data Communication

Exchange of data between two devices via some transmission medium.

Data communication system has *five components* -
![[Pasted image 20250102133339.png]]

1. **Message**: Information to be communicated.
2. **Sender**: Device that sends the message.
3. **Receiver**: Device that receives the message.
4. **Transmission Medium**: Physical path by which message travels.
5. **Protocol**: Rules (including Syntax, Semantics, Timing, De facto, De jure).

---
## Transmission Mode

Data flow between two systems can be categorized into three types - 

1. **Simple Mode**:
	- Communication is unidirectional.
	- One devices always sends, while other one only receives.
	- Can use entire capacity of channel to send data in one direction.
	- Eg: Broadcast radio.
2. **Half Duplex**:
	- Each station can both transmit and receive, but not at the same time.
	- One must receive when the other is sending, and vice versa.
	- Entire capacity of a channel is taken over by whichever of the two devices is transmitting at the time.
	- Eg: Walkie-talkies.
3. **Full Duplex**:
	- Both stations can transmit and receive at the same time.
	- Basically just two half duplex connections working closely.
	- Capacity of channel must be divided into two directions.
	- Eg: Telephone

---
### Network Criteria

1. **Delivery and Accuracy**: Must deliver error-free data to correct destination.
2. **Performance**: Transit time, response time, number of users, type of transmission medium, capabilities of connected hardware's and efficiency of software.
3. **Reliability**: Low frequency of failure and quick to resolve.
4. **Security**: Protection from unauthorized access and damage and development.

---
## Types of Connection

- **Point to Point**: Provides a dedicated link between two devices.
- **Multipoint**: (also called multidrop) Connection in which more than two specific devices share a single link.

![[Screenshot 2025-01-02 at 5.35.58 PM.png]]

---
## Physical Topology

Refers to the way in which a network is laid out physically. Topology of a network is the geometric representation of relationship of all the links and linking devices to one another.

![[Pasted image 20250102174423.png]]

### Mesh Topology

Every device has a dedicated point-to-point link to every other device. We need, $$\frac{n(n - 1)}{2}$$ duplex-mode links, where $n$ is the number of nodes.

| **Advantages**                          | **Disadvantages**                           |
| --------------------------------------- | ------------------------------------------- |
| Traffic handling                        | Installation and reconnection are difficult |
| Robust                                  | Sheer bulk of wiring is expensive           |
| Privacy and security                    |                                             |
| Easy fault identification and isolation |                                             |

### Star Topology

Each device has a dedicated point-to-point link only to a central controller, usually called a hub. The devices are not directly linked to one another.

The controller acts as an exchange.

| **Advantages**                          | **Disadvantages**                               |
| --------------------------------------- | ----------------------------------------------- |
| Less expensive than mesh                | Dependency of entire topology on a single point |
| Easy to install and reconfigure         | More cables?                                    |
| Robust (independent links)              |                                                 |
| Easy fault identification and isolation |                                                 |

### Bus Topology

- One long cable acts as a backbone to link all devices in a network. (Multipoint)
- Nodes are connected to the bus cable by drop lines and taps.
 - A drop line is a connection running between the device and the main cable.
- A tap is a connector that either splices into the main cable or punctures the sheathing of a cable to create a contact with the metallic core.

| **Advantages**       | **Disadvantages**                            |
| -------------------- | -------------------------------------------- |
| Ease of installation | Difficult reconnection and fault isolation   |
| Uses less cables     | Difficult to add new devices                 |
|                      | Low security and privacy                     |
|                      | A fault in bus cables stops all transmission |

### Ring Topology

- In a ring topology, each device has a dedicated point-to-point connection with the two devices on either side of it.
- A signal is passed along the ring in one direction, from device to device, until it reaches its destination. Each device in the ring incorporates a repeater.
- When a device receives a signal intended for another device, its repeater regenerates the bits and passes them along.


| **Advantages**                  | **Disadvantages**                          |
| ------------------------------- | ------------------------------------------ |
| Easy to install and reconfigure | A break in ring can disable entire network |
| Fault isolation is simplified   |                                            |

---

#### Local Area Network (LAN)

- Usually limited to a few kilometers of area.
- Privately owned or office or entire building.

#### Metropolitan Area Network (MAN)

- MAN is of size between LAN and WAN.
- City

#### Wide Area Network (WAN)

- WAN is made of all the networks in a larger area.
- State

---
## OSI Model

**Open System Interconnection**

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

- Ensures *error-free* data transfer between two devices on same network
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

---
## TCP/IP Model

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

---
## Switching

-  Switching in Computer Networks helps in deciding the best route for data transmission if there are multiple in a larger network.
- One to one connection

### Circuit Switching

- Before data transmission, connection will be established.
- Eg: Telephone Network

![[Screenshot 2024-11-21 at 1.37.38 PM.png]]

1. Connection
2. Data Transmission
3. Disconnection

### Message Switching

![[Screenshot 2024-11-21 at 1.42.49 PM.png]]
- First message is broken into individual pieces, which are then reassembled at the Intermediary node.
- Then message is transferred as a complete unit and forwarded using *Store and Forward* mechanism.
- Not suited for streaming media and real time applications.

### Packet Switching

- Internet is a packet switching network.
- Message is broken into chunks called packets.
- Each packet is send individually.
- Each packet will have source and destination IP address with sequence number.
- **Sequence Number** will help the receiver to
	- Sort the packets
	- Detect missing packets
	- Send acknowledgements

#### 1. Datagram Approach - Packet Switching

![[Screenshot 2024-11-21 at 1.51.24 PM.png]]

- Connectionless switching
- Each independent entity is called as *datagram*.
- Path is not fixed
- Intermediary nodes take routing decision to forward the packets using their destination information.

#### 2. Virtual Circuit Approach - Packet Switching

![[Screenshot 2024-11-21 at 1.54.15 PM.png]]

- Connection Oriented Switching
- A preplanned route is established before sending the message
- Call request and call accept packets are used to establish the connection b/w sender and receiver
- Path is fixed for the duration of a logical connection

### Packet Switching Technology

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

