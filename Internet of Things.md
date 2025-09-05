---
tags:
  - core
references:
  - https://youtu.be/6ptZr9VRxPs?si=2xhGkws6ni-G-sch
date_created: 2025-04-21
date_modified: 2025-04-22
---
---
# IoT (Internet of Things)

Interconnection of uniquely identifiable “things” (sensors/actuators) that collect, exchange and act on data over a network.

**Characteristics of IoT**
- *Unique Identity*: Each device has its own address/ID.
- *Dynamic Topology*: Devices join, leave or move, and network paths change.
- *Self‑Configuration*: Automatic device discovery, registration and setup.
- *Self‑Adaptation*: Systems adjust to varying conditions (e.g., network load).
- *Heterogeneity*: Different hardware/OS/protocols interoperate seamlessly.
- *Integrated Networking*: Devices collaborate toward a common goal.

**Benefits of IoT**
- Save time
- Efficient resource utilization
- Reduces human efforts and error
- Increased Security
- User friendly / ease of use

**Future of IoT**
- *AI & Machine Learning* for autonomous decision‑making
- *Voice UIs (VUI)* for hands‑free control
- *Miniaturization* of sensors/actuators
- *Energy Harvesting* & low‑power design
- *Big Data Analytics* on IoT‑generated data

## Architecture of IoT

```mermaid
flowchart TB
    SL["<b>Sensing Layer</b><br/>(Sensor & Actuators)<br/>(Data Gathering)"]
    TL["<b>Transport Layer</b><br/>(Gateway/Connect)<br/>(Data Transmission)"]
    DPL["<b>Data Processing Layer</b><br/>(Processing Unit)<br/>(Process Information)"]
    AL["<b>Application Layer</b><br/>(App Mgmt)<br/>(User Application)"]
    BL["<b>Business Layer</b><br/>(App & Business Mgmt)"]

    SL --> TL --> DPL --> AL --> BL
```

**Sensing Layer**
- Specific (only detect one thing) and Unchangeable (doesn't effect environment) nature.
- Types based on:
	- Output - Analog (continuous) and Digital (discrete)
	- Data type - Scalar (only magnitude) and Vector (with direction)

**Actuation Technology**
- Hydraulic
- Pneumatic (air)
- Electric
- Thermal / Magnetic
- Mechanical

## Core Components

- **Devices:** Sensors, actuators, gateways
- **Resources**: energy, internet, software, websites
- **Connectivity:** Wi‑Fi, cellular, LoRaWAN, Bluetooth
- **Controllers & APIs:** REST, MQTT, CoAP
- **Storage:** SQL/NoSQL, time‑series databases
- **Analytics:** Edge/Cloud processing, dashboards
- **Applications:** Web/mobile UIs, alerts

## Physical Design

- **Entities**: Internal (processing units) vs. External (users, external systems)
- **Data Flow**: Input → Processing → Output

1. UI Design: Input methods & displays
2. Data Design: Formats & storage models
3. Process Design: Flowcharts, validation, transformations

## Logical Design

Graphical and *textual* approach for system show casing its processes and flow of data in & out of processes.

- **Functional Blocks:** Devices, network, security, services, apps
- **Communication Models:**
    - Request–Response (HTTP/REST)
    - Publish–Subscribe (MQTT)
    - Push–Pull (Message queues)
    - Peer‑to‑Peer (WebSockets, full‑duplex)
- **API Types:** RESTful vs. WebSockets

| Rest                                                  | Web Sockets           |
| ----------------------------------------------------- | --------------------- |
| Stateless                                             | Stateful              |
| Request-response                                      | Full duplex           |
| Each request involves setting up a new TCP connection | Single TCP connection |
| Header overhead                                       | No header overhead    |
| Not suitable for Real time application                | Suitable for RTA      |

## IoT Enabling Technologies

- Wireless sensor network (WSN)
- Cloud computing N/W
- Big Data Analysis
- Low-power Embedded Systems
- Machine learning

## IoT Levels

Here’s a concise 6‑level deployment model for IoT, with simple examples:

1. **Fully Local** - All sensing, processing & control on‑device (no cloud).
2. **Local + Cloud Storage/Analysis** - Edge devices feed cloud for heavy analytics.
3. **Cloud Connectivity + Cloud Servers** - Local sensors/UI; all processing in cloud.
4. **Cloud‑Hosted Sensing & Compute** - Even basic sensing nodes run virtually in cloud.
5. **Local Coordinator + Cloud Observer** - Gateways aggregate device clusters; cloud monitors overall health.
6. **Centralized Cloud Controller** - Cloud directly manages all devices.

## IoT data management & compute stack

```mermaid
flowchart TB
  E["Edge (Devices)"] --> F["Fog (Gateways)"] --> C["Cloud (Data Centers)"]
```

**Goals**
- Minimize latency
- Conserving network bandwidth
- Increasing local efficiency
- Minimize data transmitted

## M2M (Machine‑to‑Machine)

Direct exchange of information between devices—often over short links—without human intervention.

**Core Functions**  
- **Remote Monitoring**
  Devices report status (e.g., meter readings).
- **Control**
  Central system or another device issues commands (e.g., start/stop machinery).
- **Data Transfer**
  Typically point‑to‑point or via simple gateways.

**Common Protocols**
- **Zigbee** (IEEE 802.15.4 mesh)
- **Bluetooth Classic & LE**
- **Modbus** (serial or TCP)
- **6LoWPAN** (IPv6 over low‑power wireless)

**Highlights**
- Usually closed, proprietary networks
- Focus on reliable, deterministic links
- Limited data types and volumes
- Minimal or no cloud involvement

**Benefits**
- Human Involvement (↓)
- Efficiency & Optimization (↑)

## IoT vs. M2M

| IOT                                                     | M2M                                                             |
| ------------------------------------------------------- | --------------------------------------------------------------- |
| Internet Required                                       | Not dependent of Internet                                       |
| Cloud communication                                     | Point-to-point communication                                    |
| Both H/W & S/W                                          | Mostly H/W                                                      |
| B2B & B2C                                               | B2B                                                             |
| Components: sensors, connectivity, UI & data processing | Components: device, area network, gateway & application servers |

---
## Wireless Sensor Nodes (WSN)

Distributed network of small, autonomous sensor nodes that cooperatively monitor physical or environmental conditions and forward data to a central sink (or gateway).  

### Sensor Node Architecture

- **Sensing Unit**
	- One or more transducers (e.g. temperature, humidity, light)
	- Analog‑to‑Digital Converter (ADC)
- **Storage Unit**
	- Local or Cloud data storage requirements
- **Processing Unit**
	- Microcontroller or small CPU
	- Local storage (RAM / flash)
- **Communication Unit**
	- Radio transceiver (IEEE 802.15.4, BLE, LoRa, etc.)
	- Antenna
- **Power Unit**
	- Battery or energy harvester (solar, vibration)
- **Optional Extras**
	- GPS or other localization module
	- Security co‑processor

### Types of Sensor Nodes

- **Stationary Nodes (SSN)**
	- _Terrestrial_: fixed on land (e.g. smart agriculture, environmental monitoring)
	- _Underwater_: acoustic communication (e.g. oceanography)
	- _Aerial_: mounted on UAVs (e.g. disaster surveillance)
- **Mobile Nodes (MSN)**
	- Attached to moving platforms (robots, vehicles, wildlife tags)
### Key Characteristics

- **Self‑Organizing**: automatic topology formation and healing
- **Energy‑Constrained**: duty‑cycling, low‑power radios, and energy‑harvesting strategies
- **Scalable & Fault‑Tolerant**: handles node failures without collapse
- **Heterogeneous**: mixed node capabilities (sensing, computation, power)

### Common Protocols & Standards
- **MAC/PHY Layers**
	- IEEE 802.15.4 (Zigbee, 6LoWPAN)
	- Bluetooth LE
	- LoRaWAN, NB‑IoT (LPWAN)
- **Routing & Transport**
	- RPL (Routing Protocol for Low‑Power and Lossy Networks)
	- CoAP (Constrained Application Protocol)
	- MQTT‑SN (MQTT for Sensor Networks)

---
## IoT Protocols

### Network‑Layer Protocols

**LAN / PAN**
- **Wi‑Fi (IEEE 802.11)**
	- High throughput (Mbps–Gbps), moderate power, ~100 m range.
- **Bluetooth & BLE**
	- Short‑range (10–100 m), very low power, ideal for wearables and phone‑to‑device links.

**Mesh Protocols**
- **Zigbee**
	- Built on IEEE 802.15.4 PHY/MAC
	- Self‑healing star/tree/mesh topologies
	- AES‑128 link‑layer security, authentication & secure routing
	- Used in smart lighting, home/industrial sensor networks

**LPWAN (Low‑Power Wide‑Area Networks)**
- **6LoWPAN**
	- IPv6 adaptation over 802.15.4
	- Header compression & fragmentation for tiny packets
	- Very low power, ~10–100 kbps, ~100 m range
- **LoRaWAN**
	- Ultra‑long range (1–15 km), star‑of‑stars
	- Adaptive data rate, battery life of years

**Cellular**
- **3G/4G/5G** for broad coverage & high bandwidth
- **NB‑IoT / LTE‑M** variants optimized for IoT (low power, extended range)

### Data Protocols

| Protocol | Style                | Transport | Key Features                          |
| -------- | -------------------- | --------- | ------------------------------------- |
| **MQTT** | Pub/Sub              | TCP       | Lightweight, QoS levels, retain flags |
| **CoAP** | RESTful              | UDP       | Very low overhead, DTLS security      |
| **AMQP** | Enterprise messaging | TCP       | Queues/topics, transactions           |
| **HTTP** | RESTful              | TCP       | Ubiquitous, easy integration          |
| **DDS**  | Data‑centric Pub/Sub | TCP/UDP   | Real‑time QoS, fine‑grained control   |
| **XMPP** | XML messaging        | TCP       | Presence, extensible                  |

### IEEE 802.15.4  

- **PHY & MAC** for low‑power wireless PANs
- Cost effective
- Low Data rate: up to 250 kbps
- Security: AES‑128 encryption at link layer
- Foundation for 6LoWPAN, Zigbee, Thread
- Works on Data link layer and physical layer

### 6LoWPAN

- Low-power wireless PANs
- Encapsulates IPv6 in 802.15.4 frames
- Header compression & fragmentation
- Enables direct IP addressing of tiny devices

### Zigbee

- Full stack: network, transport & application layers atop 802.15.4 (WSN)
- **ACE**: Additional Communication Enhancements—security, auth, encryption, routing
- Mesh Topologies:
	- **Star:** all end‑devices ↔ coordinator
	- **Tree:** hierarchical clusters
	- **Mesh:** multi‑hop, self‑healing

![[Screenshot 2025-04-21 at 5.33.19 PM.png | 500]]

### RFID (Radio‑Frequency ID)

- Derived from **AIDC** (Automatic Identification & Data Collection) - which was wired.
- **Tags** - for data encryption
	- **Components**:
		- IC (integrated circuit): Read‑only, Write‑once, or R/W
		- Antenna & protective casing
	- **Types**:
		- *Passive:* powered by reader’s RF field
		- *Active:* battery‑powered, longer range
- **Readers** - for data decryption
	- RF signal generator → emits interrogation
	- Signal detector → decodes backscatter
	- MCU (micro-controller) parses tag data & forwards to host

> [!Tip]
>- Use **802.15.4‑based** mesh (Zigbee/6LoWPAN) for local, low‑power sensor fabrics. 
>- Choose **LPWAN or cellular** when you need kilometers of range or wide‑area coverage.
>- Match your **data‑layer protocol** to device constraints (bandwidth, power, reliability).

### NFC (Near Field Communication)

- **Range:** Very short (≤ 4 cm)
- **Modes:**
    - **Reader/Writer:** phone reads passive tags
    - **Peer‑to‑Peer:** two devices exchange data
    - **Card Emulation:** device acts as smart card
- **Power:** Passive tags draw energy from reader; active devices use their own
- **Security:** Built‑in encryption and proximity requirement
- **Use Cases:** Contactless payments, smart posters, electronic business cards, access control

### MQTT (Message Queuing Telemetry Transport)

Lightweight, TCP‑based publish/subscribe protocol designed for low‑bandwidth, high‑latency networks.

**Core Components**
- **Publisher:** Produces and sends data (e.g. sensors)
- **Broker:** Central server that routes messages to subscribers
- **Subscriber:** Receives data of interest (e.g. dashboards, actuators)

**Key Operations**
1. **CONNECT / DISCONNECT** – establish or terminate session
2. **PUBLISH** – send message to a topic
3. **SUBSCRIBE / UNSUBSCRIBE** – register or deregister interest in topics
4. **PINGREQ / PINGRESP** – keep‑alive

**Topic Filters**
- **Exact:** `home/bedroom/temperature`
- **Single‑Level Wildcard:** `home/+/temperature` (any room)
- **Multi‑Level Wildcard:** `home/#` (all subtopics under home)

### AMQP (Advanced Message Queuing Protocol)

**Core Concepts**  
- **Connection**: TCP link  
- **Session (Channel)**: multiplexed exchange  
- **Link**: logical sender ↔ receiver  
- **Message**: headers + body  

**Frame Types**  

| Frame           | Purpose                             |
| --------------- | ----------------------------------- |
| Open / Close    | Connection setup / teardown         |
| Begin / End     | Session (channel) start / end       |
| Attach / Detach | Link setup / teardown               |
| Transfer        | Message delivery                    |
| Flow            | Credit‑based flow control           |
| Disposition     | Acknowledge or update message state |

![[Pasted image 20250422161220.png]]

**Exchange Types**  
- **Direct**: exact‑match routing key → queue  
- **Fanout**: broadcast to all bound queues  
- **Topic**: pattern‑match (`*` single‑level, `#` multi‑level)  
- **Headers**: route by header attributes (`all` or `any`)

**Basic Workflow**  
1. Producer → **Exchange** (provides routing key)  
2. Exchange → bound **Queue(s)** (based on type & bindings)  
3. Consumer pulls (or is pushed) messages from Queue

### CoAP (Constrained Application Protocol)

- Lightweight HTTP‑like protocol for resource‑constrained devices
- Designed for M2M / IoT: minimal overhead, low power, small code footprint

- **Transport:** UDP (low overhead)
- **Layer:** Application
- **Model:** Client ↔ Server (RESTful)
- **Resources:** URI-based (`coap://…`)
- **Methods:** `GET`, `POST`, `PUT`, `DELETE`

**“Constrained” Design Goals**
- Small header: 4‑byte base, optional tokens/options
- Low memory & CPU usage
- Minimal message size
- Simple parsing

**Messaging Types**

| Type    | Code            | Reliability                                 |
| ------- | --------------- | ------------------------------------------- |
| **CON** | Confirmable     | Retransmit until ACK received               |
| **NON** | Non‑confirmable | Fire‑and‑forget (no ACK)                    |
| **ACK** | Acknowledgement | Acknowledges a CON or piggybacks a response |
| **RST** | Reset           | Rejects a message or signals error          |

### XMPP (Extensible Messaging & Presence Protocol)

**What & Why**
- XML-streaming, client-server protocol for real-time messaging and presence
- Highly extensible via XEPs (XMPP Extension Protocols)

**Core Concepts**
- **Stanzas** (XML fragments):
	- `<message/>` – chat or data payload
	- `<presence/>` – advertise online/offline/busy status
	- `<iq/>` (“info/query”) – request/response for roster, vCard, service discovery
- **Roster** – contact list with subscription rules
- **Presence** – publish and subscribe to status changes
- **Multi‑user chat**, file transfer, voice/video (via Jingle XEPs), IoT pub/sub

**Key Features**  
- Decentralized (federated) servers
- Extensible namespace model
- Built‑in trust (TLS), pluggable auth (SASL)
- “Long‑lived” XML streams with heartbeats (XMPP keep‑alive)

**Use Cases**
- Instant messaging, presence services
- IoT signaling (lightweight pub/sub)
- Collaboration (voice/video conferencing)

### DDS (Data Distribution Service)

**What & Why**
- Broker‑less, peer‑to‑peer *pub/sub* middleware standardized by OMG
- Designed for high‑performance, real‑time M2M data exchange
- Eliminates single‑point failures via *distributed* discovery

**Architecture Layers**
1. **DCPS** (Data‑Centric Publish‑Subscribe)
	- Topics, DataWriters (publishers), DataReaders (subscribers)
	- QoS policies: reliability, durability, deadline, liveliness, latency
2. **DLRL** (Data Local Reconstruction Layer)
	- In‑memory data caching and access patterns

**Key Characteristics**
- **No Broker**: peers discover each other via RTPS (Real‑Time Pub/Sub)
- **Fine‑Grained QoS**: control over delivery, ordering, resource use
- **Scalable & Fault‑Tolerant**: dynamic domain discovery, multicast support
- **Language & OS Agnostic**: C/C++, Java, Python, etc.

**Use Cases**
- Industrial automation & SCADA
- Autonomous vehicles & robotics
- Defense, aerospace, healthcare monitoring

---
## SCADA (Supervisory Control & Data Acquisition)

**Definition:**
A centralized system for real‑time monitoring and control of industrial processes.

**Key Functions:**
- **Data Acquisition:** Polling field devices at set intervals
- **Real‑Time Monitoring:** Displaying live values, trends, alarms
- **Remote Control:** Start/stop or adjust set‑points on equipment
- **Alarm Management & Logging:** Alert on thresholds, store historical data

**Use Cases:**
Power grids, water/wastewater treatment, oil & gas pipelines, manufacturing lines

## IIoT (Industrial Internet of Things)

The application of IoT technologies (sensors, connectivity, analytics) to industrial environments.

**Key Capabilities:**
- **M2M Connectivity:** Reliable device‑to‑device sync & communication
- **Real‑Time Analytics:** Defect/problem detection before failures
- **Predictive Maintenance:** Condition‑based servicing
- **Digital Twins:** Virtual replicas for simulation & optimization

**Primary Benefits:**
- ↓ Manual errors
- ↓ Time & operational costs
- ↑ Efficiency & throughput
- ↑ Safety via automated alerts
- Faster, data‑driven business decisions

## Autonomous Vehicle

- **Level 0 – No Automation**  
  Driver does all steering, acceleration & braking.
- **Level 1 – Driver Assistance**  
  System assists with *either* steering **or** speed control (e.g. adaptive cruise control or lane‑keep).
- **Level 2 – Partial Automation**  
  System controls both steering **and** acceleration/braking simultaneously; driver must monitor and intervene.
- **Level 3 – Conditional Automation**  
  System drives under defined conditions (e.g. highway); driver must be ready to take over.
- **Level 4 – High Automation**  
  System handles all driving tasks in its operational design domain; human intervention optional.
- **Level 5 – Full Automation**  
  System drives everywhere, in all conditions—no human driver needed.

---
## Arduino and Raspberry Pi

**Arduino**
- Open source H/W & S/W platform
- Consists of a circuit board + ready made S/W (Arduino IDE)
- Uses simplified version of C++
- No extra hardware required on load code onto board, just use USB cable.

**Raspberry Pi**
- Single Board Computer (SBC) - consists of processor, memory, I/O interface on single circuit board.
- Uses - Gaming, Editing, Browsing, home automation, detectors, etc.
- Developed by Raspberry Pi Foundation
- Small in size and affordable

| Feature              | **Arduino Uno**                       | **Raspberry Pi 4**                              |
| -------------------- | ------------------------------------- | ----------------------------------------------- |
| **Core**             | ATmega328P 8‑bit MCU @ 16 MHz         | Broadcom BCM2711 64‑bit SoC @ 1.5 GHz quad‑core |
| **Memory & Storage** | 2 KB SRAM, 32 KB Flash; no SD slot    | 1 – 8 GB RAM; microSD boot & storage            |
| **I/O**              | 14 digital I/O (6 PWM), 6 analog      | 26 GPIO (digital); needs external ADC           |
| **OS**               | Bare‑metal (no OS)                    | Linux‑based (Raspbian, Ubuntu, etc.)            |
| **Programming**      | C/C++ via Arduino IDE                 | Python, C/C++, Java, Node.js, etc.              |
| **Power & Voltage**  | ~0.2 W @ 5 V; 5 V logic               | ~3 W @ 5 V; 3.3 V logic                         |
| **Connectivity**     | USB for programming; shields optional | USB, HDMI, Ethernet, Wi‑Fi, Bluetooth           |
| **Use Cases**        | Real‑time sensor/actuator control     | Multimedia, networking, edge computing          |
| **Cost**             | \$20 – \$30                           | \$35 – \$75                                     |

> **Tip:** Use Arduino when you need real‑time I/O and simplicity; choose Raspberry Pi for full‑fledged OS, networking, and heavier compute tasks.

---
# Reverse Engineered Assignments

## Assignment 0

- **RFID (Radio-Frequency Identification)**
    - Automatically identifies and tracks tags on objects via electromagnetic fields.
    - Extracts information without direct line of sight.
- **Zigbee Protocol Stack**
    1. Physical
    2. Medium Access Control (MAC)
    3. Network
    4. Application
- **Cloud-Computing Components**
    - **Clients** (end-user devices)
    - **Services** (e.g. IaaS, PaaS, SaaS)
    - **Applications**
    - **Platform**, **Storage**, **Infrastructure**
    - **Not:** Local servers
- **Common Sensor Modules**
    - **HC-SR04**: Ultrasonic distance sensor (2 cm – 450 cm)
    - **DHT22**: Temperature & humidity sensor
    - **TSL2591**: Ambient light sensor
    - **HC-SR505**: PIR motion sensor
- **Typical Sensor-Network Components**
    - **Sensor nodes** (data sources)
    - **Routers** (forward data)
    - **Gateways** (protocol translation)
    - **Sink** (data aggregation point)
- **Measuring Orientation & Angular Velocity**
    - **Gyroscope**: correct device
    - Accelerometer measures linear acceleration; GPS gives position
- **ISA100.11a Standard**
    - ISA = **International Society of Automation**
    - Defines wireless networking for industrial automation
- **Traditional Data Center vs. Cloud**
    - **Key differences**: Scalability, Flexibility, Elasticity, Automation, Running Costs, Security
    - **Not a differentiator**: Storage
- **Smart Grid**
    - Also known as the **Energy Internet**
- **Point-of-Node Failure**
    - In a stationary sensor network, a single-node failure **can partition** the network into fragments

## Assignment 1

### 1. What Is IoT?

- **Full Form**: Internet of Things
- **Evolution Drivers**:
    - Low-power embedded systems
    - Cloud computing
    - Big Data analytics
    - Machine Learning
    - Networking technologies

### 2. Enabling Technologies

- **RFID**: Radio-frequency tags for automatic identification and tracking
- **Nanotechnology**: Miniaturization of sensors, MEMS devices
- **Sensors**: Transducers converting physical parameters to electrical signals
- **Smart Networks**: IP-based, self-configuring communication backbones

### 3. IoT LAN vs. Gateway Functions

- **IoT LAN (Local Area Network)**
    - Short-range, local communication within buildings or campuses
    - Manages device discovery, data aggregation
- **Gateway**
    - Bridges IoT LAN to wide-area/internet
    - Handles protocol translation, security, QoS
- **Not a LAN Function**: long-range/global or world-wide connectivity

### 4. IPv6 Addressing & Multi-Homing

#### 4.1 Address Crunch
- Occurs when legacy, smart and constrained nodes share the same IP space

#### 4.2 Multi-Homing
- **Definition**: Connecting a node or network to **multiple** networks for redundancy and reliability (not single)
- **Approaches**:
    1. **Proxy-based**: A proxy server manages multiple interfaces
    2. **Gateway-based**: A dedicated gateway routes traffic across links

#### 4.3 IPv6 Notation
- **Format**: Hexadecimal fields separated by colons. e.g. `2001:0db8:85a3::8a2e:0370:7334`
- **Length**: 128 bits total (8 groups × 16 bits)

### 5. Sensing Fundamentals

- **Sensor Characteristics**:
    - **Selective Sensitivity**: Only responds to its target measurand
    - **Insensitivity**: Ignores other physical properties
- **Classification by Output**:
    - **Analog Sensors**: Continuous voltage/current proportional to measurand
    - **Digital Sensors**: Output discrete digital values (e.g. via ADC)
- **Data Flow**: Sensor readings can be transmitted to the cloud for storage, analytics, ML processing

### 6. Actuation Basics

- **Relays**
    - Electromechanical switches (actuators)
    - Use low-voltage DC to switch higher-voltage AC loads
- **Soft Actuators**
    - Polymer-based materials that deform under stimuli (electric field, pressure)
    - Enable gentle, bio-inspired motion

## Assignment 2

### 1. MQTT (Message Queuing Telemetry Transport)

- **Type**: Data-protocol optimized for IoT
- **Use Cases**:
    - Remote (often intermittent) connections
    - Constrained/low-bandwidth networks
- **Architecture**:
    1. **Publish–Subscribe** paradigm (event-driven)
    2. Underpinned by a lightweight **Client–Server** model
- **Core Components**:
    - **Publisher**: Sends messages to topics
    - **Subscriber**: Receives messages from topics
    - **Broker**: Routes messages based on topic filters
- **Topics**:
    - UTF-8 strings (not numeric only)
    - Act as routing keys within the broker
- **Message Methods**:
    - Five defined MQTT control packet types (CONNECT, PUBLISH, SUBSCRIBE, etc.)

### 2. CoAP (Constrained Application Protocol)

- **Based On**: HTTP semantics adapted for IoT
- **Designed For**: Machine-to-Machine (M2M) applications, constrained devices
- **Transport**: Asynchronous client–server over **UDP** (datagram)

### 3. AMQP (Advanced Message Queuing Protocol)

- **Full Form**: Advanced Message Queuing Protocol
- **Purpose**: Standardized, reliable message-oriented middleware
- **Frame Types**: 9 distinct frame structures for control, data transfer, and management

### 4. OSI Model

- **Layers** (from bottom up):
    1. Physical
    2. Data Link
    3. Network
    4. Transport
    5. Session
    6. Presentation
    7. Application
- **Purpose**: Conceptual framework to standardize network communication

### 5. IPv4 Packet: Destination Address

- **Definition**: 32-bit field identifying the **final** recipient node in the network
- **Not**:
    - Source address of the packet
    - Intermediate hop address

## Assignment 3

### 1. HART Protocol

#### 1.1 Overview
- **HART** = Highway Addressable Remote Transducer
- Designed for digital communication over legacy 4–20 mA wiring

#### 1.2 Wired vs. Wireless HART

| Feature               | Wired HART                           | WirelessHART                                                    |
| --------------------- | ------------------------------------ | --------------------------------------------------------------- |
| **Physical Layer**    | Proprietary FSK over 4–20 mA loop    | IEEE 802.15.4-based DSSS @ 2.4 GHz                              |
| **Data Link Layer**   | Time-division and master-slave logic | TDMA with channel-hopping for determinism and collision-freedom |
| **Network Layer**     | **Not present**                      | Mesh routing for multi-hop connectivity                         |
| **Application Layer** | Command/response framing             | Same HART commands over the mesh; extracts, executes, responds  |

- **Key Points**:  
	- WirelessHART is the **latest** HART release, adding network-layer mesh routing.
	- Operates exclusively in the 2.4 GHz ISM band.
	- Deterministic, collision-free scheduling via TDMA & channel hopping.

### 2. NFC (Near Field Communication)

#### 2.1 Principles & Range  
- Communication by **magnetic induction** between coils in close proximity (typically < 10 cm).
- **Passive NFC tags**: Contain information; are unpowered and read by an active device.
- **Active NFC devices**: Generate their own RF field for two-way communication.  

#### 2.2 Use Cases & Characteristics  
- Contactless payments, electronic ticketing, access control  
- Low data rates (106–424 kbps), ultra-short range for security  
- Simple pairing (tap-to-connect) without manual configuration  

### 3. Bluetooth

#### 3.1 Architecture  
- Based on **ad-hoc piconets**:  
  - One master, up to seven active slaves per piconet  
  - Can interconnect piconets into scatternets

#### 3.2 Protocol Stack Highlights  
- **Link Manager Protocol (LMP)**:  
  - Manages link establishment, authentication, encryption, and configuration (not just authentication).
- **L2CAP**: Multiplexes higher-layer protocols, segmentation/reassembly  
- **RFCOMM**: Serial-port emulation  
- **HCI**: Hardware abstraction to controller  

#### 3.3 PHY & MAC  
- 2.4 GHz ISM band; uses frequency-hopping spread spectrum (FHSS)  
- Data rates: Classic Bluetooth up to ~3 Mbps; BLE up to 2 Mbps  

### 4. Zigbee (IEEE 802.15.4-Based)

#### 4.1 Key Properties  
- **PHY/MAC**: Defined by IEEE 802.15.4 @ 2.4 GHz  
- **Data Rate**: 250 kbps
- **Topology**: Star, tree, and mesh networks  

#### 4.2 Application Layer  
- Profiles for home automation, smart energy, health care  
- Low-power, low-cost, and support for large mesh deployments  

## Assignment 4

### 1. Agricultural IoT Deployment (AID)  
- **Definition**: Deploying a grid of static sensor nodes across an agricultural field to monitor environmental parameters (e.g., soil moisture, temperature, humidity).
- **Use Cases**: Precision irrigation, pest detection, crop health monitoring

### 2. Ultrasonic Distance Sensing
- **Principle**: Emits ultrasonic pulses and measures echo return time; distance = (speed of sound × round-trip time)/2.
- **Typical Specs**:
  - Range: 2 cm to several meters (depending on sensor)  
  - Resolution: millimeter-scale
- **Applications**: Obstacle detection, liquid-level measurement, presence sensing.

### 3. Coverage in Static Wireless Sensor Networks (WSNs)

#### 3.1 Coverage Problem
- **Definition**: Determining optimal placement (and activation) of static sensors so that every point/area of interest is “covered” by at least one sensor’s sensing radius.

#### 3.2 Coverage Objectives
- **Minimize Sensor Count**: Reduce hardware cost and deployment complexity
- **Maximize Network Lifetime**: Conserve energy by avoiding redundant coverage and rotating active sensors

#### 3.3 Coverage Types
1. **Area Coverage**: Entire region must be within sensing range of ≥1 node
2. **Point Coverage**: Specific targets or locations need monitoring
3. **Barrier Coverage**: Creating a “fence” so that any crossing path intersects at least one sensor’s coverage disk

#### 3.4 Coverage Disk Model
- **Crossing Covered**: A path “crossing” is covered if its trajectory passes through the interior of at least one node’s circular sensing region.

### 4. Stationary WSN Characteristics  
- **Static Topology**: Nodes remain fixed after deployment; no self-reconfiguration  
- **Failure Impact**: A single node failure can partition the network into disconnected segments, affecting coverage and routing

### 5. UAV (Unmanned Autonomous Vehicle) Networks

#### 5.1 Key Features  
- **Multi-Tasking**: UAVs can carry multiple sensors or perform varied missions in one flight  
- **Large Coverage Area**: High altitude and mobility allow monitoring over wide regions
- **Scalability**: Easily add or remove UAVs to adjust coverage or data-gathering capacity

#### 5.2 Network Topologies  
- **Star**: All UAVs communicate through a central ground station or leader UAV  
- **Mesh**: UAVs relay data peer-to-peer, extending range and resilience

### 6. Mobile WSN & Data Mules  
- **Data Mule Concept**: Mobile entities (e.g., vehicles or robots) collect buffered data from static sensors, then transport and offload it at a sink node.
	1. **Collect Phase**: Visit sensor nodes within communication range
	2. **Delivery Phase**: Return to sink to offload accumulated readings
- **Advantages**: Reduces need for multi-hop forwarding; conserves sensor energy

### 7. Autonomous Underwater Vehicles (AUVs)
- **Full Form**: Autonomous Underwater Vehicle
- **Role**: Untethered platforms for deep-water sensing (e.g., oceanographic data, pipeline inspection)

### 8. Human-Centric Sensing
- **Definition**: Harnessing sensors embedded in personal devices (smartphones, wearables) carried by humans to collect context-aware data.
- **Major Challenges**:
	- **Energy Management**: Balancing battery life with continuous sensing
	- **Participant Selection**: Incentivizing and choosing appropriate users/devices for reliable data streams

### 9. Machine-to-Machine (M2M) Application Platforms  
- **Purpose**: Provide end-to-end services (device management, data analytics, visualization) by integrating heterogeneous device datasets.  
- **Examples**: Remote asset monitoring, smart metering dashboards, predictive maintenance systems

## Assignment 5

### 1. Current Challenges in IoT

- **Large-Scale Cooperation**
	- Billions of heterogeneous devices must coordinate, share data, and collaborate seamlessly.
	- Examples: Smart cities integrating traffic lights, parking sensors, public transport feeds.
- **Global Heterogeneity**  
	- Diverse hardware platforms (sensors, gateways), communication protocols (MQTT, CoAP, HTTP), and software stacks (JavaScript, Python, Java).  
	- Requires common interfaces and translation layers for cross-domain interoperability.   

### 2. Interoperability in IoT

#### 2.1 Definition  

> **Interoperability** is the ability of two or more systems or components to exchange information and use the exchanged information effectively.

#### 2.2 Why It Matters  

- **Protocol Diversity**: Devices use different network stacks (e.g., BLE, LoRaWAN, Wi-Fi).  
- **Language Diversity**: Firmware and cloud code written in various languages (C/C++, Python, JavaScript).
- **Data Formats**: JSON, XML, binary payloads, proprietary encodings.   

#### 2.3 Levels of Interoperability  
| Level         | Description                                                                              |     |
| ------------- | ---------------------------------------------------------------------------------------- | --- |
| **Syntactic** | Common message formats/schemas (e.g., JSON over MQTT)                                    |     |
| **Semantic**  | Shared vocabularies or ontologies so that “temp” on Device A means the same as “T” on B  |     |
| **Systemic**  | End-to-end service integration, including workflows, user interfaces, and business logic |     |

#### 2.4 Middleware Solutions  

**UMB (Universal Middleware Bridge):**
- Acts as a translation hub between disparate IoT platforms and protocols.
- Handles protocol adaptation, data-model mapping, authentication brokering.

### 3. Arduino: The Open-Source MCU Platform

#### 3.1 Overview  
- **Arduino**: A family of easy-to-use microcontroller boards and IDE for rapid prototyping.  
- **Open-Source**: Schematics and code libraries are publicly available.   

#### 3.2 Hardware Highlights (Arduino Uno)  
- **Microcontroller**: ATmega328P @ 16 MHz  
- **Digital I/O Pins**: 14 total (0–13), configurable as input or output   
- **Analog Inputs**: 6 channels (A0–A5)  
- **On-Board USB** for programming and serial comms  
- **No External Circuitry Needed** to upload sketches—just USB cable and IDE.   

### 4. Arduino Programming Fundamentals

#### 4.1 Sketch Structure  

```cpp
void setup() {
  // Runs once at startup
}

void loop() {
  // Runs repeatedly
}
```

#### 4.2 Control Flow: Loops

- **for loop**
	```cpp
	for (int i = 0; i < N; i++) { /* ... */ }
	```
- **while loop**
	```cpp
	while (condition) { /* ... */ }
	```
- **do-while loop**
	```cpp
	do { /* ... */ } while (condition);
	```

> Arduino supports all three C-style loops.

#### 4.3 Conditional (Ternary) Operator

```cpp
value = (condition) ? expressionIfTrue : expressionIfFalse;
```

### 5. Example: LED Blink Sketch

```cpp
int ledPin = 13;

void setup() {
  pinMode(ledPin, OUTPUT);
  for (int i = 0; i < 3; i++) {
    digitalWrite(ledPin, HIGH);   // LED ON
    delay(1000);                  // wait 1000 ms
    digitalWrite(ledPin, LOW);    // LED OFF
    delay(500);                   // wait 500 ms
  }
}

void loop() {
  // nothing else
}
```

- **Behavior**: Blinks the on-board LED three times, each ON for 1 s and OFF for 0.5 s.

### 6. Interfacing Sensors & Actuators

#### 6.1 DHT Temperature & Humidity Sensor

- **Library Initialization**
    ```cpp
    #include <DHT.h>
    DHT dht(pin, DHTTYPE);
    
    void setup() {
      dht.begin();   // Start communication with DHT sensor
    }
    ```
- **Reading Values**
    ```cpp
    float h = dht.readHumidity();     // %RH
    float t = dht.readTemperature();  // °C
    ```

> `dht.begin()` must be called before any readings to initialize timing and data pins.

#### 6.2 Servo Motor Control

- **Moving to Angle**
    ```cpp
    #include <Servo.h>
    Servo myServo;
    
    void setup() {
      myServo.attach(pin);
      myServo.write(90);  // Move to 90°
    }
    ```

> `ServoDemo.write()` (i.e., `myServo.write()`) sets the shaft angle in degrees (0–180°).

## Assignment 6

### 1. Python for Embedded Development

- **Lightweight language**: Python’s interpreter and libraries are small enough to run on microcontrollers and SBCs like Raspberry Pi, making it popular for embedded apps.
- **Indentation**: Blocks are defined by consistent indentation (usually 4 spaces); no braces.

### 2. Common Python Operations

- **File I/O Modes**
    - `'r'`: read (error if file missing)
    - `'w'`: write, truncate existing content or create new
    - `'a'`: append to end
    - `'r+'`: read/write without truncating

### 3. Working with Sensors & Libraries

- **DHT22 sensor**: Use Adafruit’s CircuitPython library (`adafruit_dht`) to read temperature/humidity.
- **PIL (Pillow)**: Install to get the updated fork of the old PIL image library.
    ```bash
    sudo pip install pillow
    ```

### 4. Raspberry Pi Networking & Services

- **Remote Access (client side)**: Needs both the server’s **IP address** and **port number** to connect via sockets/SSH.
- **File Server**: Raspberry Pi can be configured as a Samba or NFS file server to share storage on the network.

### 5. Raspberry Pi Configuration & Camera

- **Configure camera**:
    ```bash
    sudo raspi-config
    ```

→ Enable camera interface → **Reboot** the Pi.

- **Capture still image**:
    ```bash
    raspistill -o image.jpg
    ```

### 6. Nano Editor Shortcuts

- **Exit nano**: `Ctrl + X`
- **Save (write out)**: `Ctrl + O`
- **Cut line**: `Ctrl + K`

### 7. IoT Control Logic

- **Relay‐controlled fan**: Fan turns **ON** when surrounding temperature **exceeds** a predefined threshold; turns OFF otherwise.

## Assignment 7

### 1. Python Socket Programming

- **Socket Types**
    - `SOCK_STREAM` → TCP socket type
    - `SOCK_DGRAM` → UDP socket type
- **Address Families**
    - `AF_INET` → IPv4 Internet protocols
    - `AF_INET6` → IPv6
- **Basic Server Workflow**
    ```python
    sock = socket.socket(AF_INET, SOCK_STREAM)
    sock.bind((host, port))
    sock.listen(backlog)      # Waits for incoming client connections
    conn, addr = sock.accept()
    ```
	
    - `.listen()` makes the socket wait for clients
- **UDP vs TCP Receive**
    - TCP: `data = sock.recv(bufsize)`
    - UDP: `data, addr = sock.recvfrom(bufsize)`

### 2. Plot Customization with Matplotlib

- **Set Y-axis label**
    ```python
    import matplotlib.pyplot as plt
    plt.ylabel("Temperature (°C)")
    ```

### 3. SDN Fundamentals

- **Mobi-Flow Protocol**
	- Extends SDN to support **mobility** in wireless networks
- **Control-Data Plane Messages**
    - **PACKET_OUT**: sent **from controller to switch** to inject/forward a packet
- **Flow Rules vs Routing Tables**
    - Traditional Network → **Routing Table**
    - SDN → **Flow Table**
- **Time-outs in Flow Rules**
    - **Soft time-out**: idle timeout (removes rule if no matching packets seen)
    - **Hard time-out**: absolute timeout (removes rule after fixed time)
    - **Hard time-out ≥ Soft time-out**
- **Rule Placement Issue**
    - Deciding which switches get which flow rules is the **Flow Rule Placement** problem
- **APIs in SDN**
    - **Northbound**: controller → applications
    - **Southbound**: controller → switches
    - **East-Westbound**: controller ↔ **controller** (for multi-controller setups)
- **Hierarchical (Tree) SDN Architecture**  
    - Also called **Tree** architecture, with higher-level controllers managing lower ones
- **SDN & IoT**  
    - **Integration is recommended**: centralizes policy, simplifies management, scales better

## Assignment 8

### 1. SDN in IoT

#### Sensor OpenFlow

- A variant of the OpenFlow SDN protocol specifically optimized for resource-constrained IoT devices.

#### Mobi-Flow

- **Purpose**: A flow-rule placement scheme that tracks mobile IoT nodes and proactively installs/removes rules to minimize control-plane chatter.
- **Message overhead**:
    - **Mobi-Flow < Conventional**: By pre-empting handovers, it reduces the number of flow-mod and packet-in messages compared to a naive approach .
- **Where used**: Mobility-aware SDIoT setups (e.g., mobile asset tracking in a factory).

### 2. Virtualization & Cloud Foundations

#### Virtual Machines → Cloud

- **Order of emergence**:
    1. **Virtual Machines** (1960s–80s): software “boxes” emulating entire OSes on a host.
    2. **Cloud Computing** (2000s): on-demand delivery of compute/storage over the Internet, built on VM farms .

#### Cloud Deployment Models

| Model       | Description                                                      | Use-case                                                                              |
| ----------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Private** | Dedicated infra on-premise or in a private data center           | High security/regulatory requirements                                                 |
| **Public**  | Shared infra run by third-party provider (AWS, Azure, GCP)       | Variable workload, cost-efficiency                                                    |
| **Hybrid**  | Mix of both: sensitive data on private; bulk workloads on public | Data locality + scalability (e.g., keep PII on-premise, archive logs to public cloud) |

### 3. Cloud Service Models

| Service  | What’s delivered                                         | Example                     |
| -------- | -------------------------------------------------------- | --------------------------- |
| **IaaS** | Raw VMs, storage volumes, networking                     | AWS EC2, Google Compute     |
| **PaaS** | Runtime environment (OS + middleware + app-hosting APIs) | Heroku, Google App Engine   |
| **SaaS** | Complete applications accessed over network              | Salesforce CRM, Spotify Web |

- **Spotify Web**: You stream music via browser without installing—classic **SaaS** .

### 4. Client Types

- **Thin Client**:
    - Minimal local resources (no HDD, little RAM/CPU)
    - Depends on server for app execution; needs constant network connectivity .
- **Thick (Fat) Client**:
    - Rich local resources, can run apps offline.

### 5. Cloud Security Essentials

#### CIA Triad

1. **Confidentiality**: only authorized users/data access
2. **Integrity**: data isn’t tampered or corrupted
3. **Availability**: systems/data accessible when needed

#### Security Layers

- **Network-level**: firewalls, VPNs
- **Host-level**: HIDS/HIPS on VMs
- **Application-level**: secure coding, WAFs
- **All three** are required for robust defense

#### Model-wide Issues

- **Data security & client auth** are challenges in **all** three service models (IaaS, PaaS, SaaS) because attackers can target any layer .

### 6. Hypervisor

- **Role**: Software layer that creates and runs virtual machines (VMs) by abstracting hardware.
- **Types**:
    - **Type 1 (“bare-metal”)** runs directly on host hardware (e.g., VMware ESXi, Xen).
    - **Type 2** runs atop a host OS (e.g., VirtualBox, VMware Workstation) .

### 7. SaaS Limitations

- **Centralized control**:
    - Pros: uniform updates, single-pane management
    - Cons: single provider → potential vendor lock-in, less tenant customization

### 8. Key Term

- **Ubiquitous**: independent of device or location (e.g., cloud services accessible from any Internet-connected device) .

## Assignment 9

### 1. Cloud Computing Advantages

- **Elasticity** – Dynamically scale resources up/down on demand
- **Pay-per-use** – Only billed for actual resource consumption
- **Self-service** – Users provision services via portals/APIs without admin help

### 2. Fog Computing

- **Definition:** Middleware layer **between Cloud and edge devices** that runs services closer to sensors/actuators
- **Role:** Reduces latency, offloads bandwidth, supports real-time analytics

### 3. Sensor-Cloud Architecture

- **Managerial role:** Handled by the **Sensor-Cloud Service Provider** (they own, allocate, and monitor virtualized sensors)
- **Principal feature:** **Sensor virtualization** – abstracts physical sensors into on-demand virtual instances

### 4. OpenStack Components

- **Core services:**
    - **Nova** – Compute (VM provisioning)
    - **Swift** – Object storage
    - **Glance** – VM image service
    - **Neutron** – Networking
    - **Heat** – Orchestration (stack templates)
    - **Horizon** – Web dashboard (access point for all components)

### 5. Origins & Concepts

- **“Fog computing” coined by:** Cisco
- **Hardware virtualization:** Enables **sharing** of physical hardware among multiple VMs/tenants, forming the foundation of all cloud models

### 6. IoT Data Characteristics

- **Temporal sensitivity matters**:
    - **Time-sensitive**: real-time control (e.g., autonomous vehicles)
    - **Less sensitive**: periodic monitoring
    - **Not time-sensitive**: bulk analytics

### 7. Sensor-Cloud Management Issues

- **Optimal composition of virtual sensors:** Deciding how many and which virtual instances serve client demands
- **Caching mechanisms (2 types):**
    - **Internal Cache (IC):** within the sensor-cloud platform
    - **External Cache (EC):** at edge/fog nodes

### 8. Latency Calculation Example

- **Given:** One-way network delay = 10 s; processing time = x; total round-trip = 25 s
- **Equation:** 25 = 10 + x + 10 → **x = 5 s**

### 9. Fog vs Cloud

- **Complementary**: Fog **extends** cloud by handling latency-critical tasks at the edge; not a replacement

## Assignment 10

### 1. Smart City Active Entities

- **Police stations**, **banks**, **transport hubs**, etc., all act as **active connected nodes** in a holistic smart-city ICT fabric .

### 2. Citizen Engagement

- ICT tools (mobile apps, e-portals, social media) **boost participation** in governance—surveys, e-voting, service requests—all in real time .

### 3. Smart Parking Challenges

- **Auto-routing** vehicles to spots
- **Detecting** available spaces reliably
- **Automated charging** for EVs
- → A full smart-parking solution must tackle **all** of these .

### 4. Multi-Sensor Data Fusion

- **Definition:** Combining streams from different sensors into a unified estimate
- **Key theory:** ***Belief functions*** (Dempster–Shafer) let you mathematically fuse uncertain evidence.
- **Challenge:** **Outliers** (faulty or malicious readings) can skew the fusion result; detection and filtering are crucial.

### 5. Intelligent Connected Vehicles (ICV) Phases

1. Cellular-based telemetry (**2G**)
2. High-speed data links (**4G LTE**)
3. **Cloud-connected** vehicles exchanging data/platform services.

### 6. Decision-Making Gap

- **Bridged by AI**: Machine-learning/edge-AI modules can autonomously interpret sensor data and trigger actuator commands with minimal latency.

### 7. Home Area Network (HAN) Standards

- **IEEE 802.15.4**: Physical & MAC
- **Zigbee**: Network & Application

### 8. UPnP

- **Universal Plug and Play**: Zero-config network discovery/protocol for device interoperability (printers, media servers) .

### 9. V2X (Vehicle-to-Everything) Communication

- **Disadvantage:** **Movement tracking** risk → privacy concerns .
- **Mobility limits TCP/IP**: IP routing assumes relatively stable endpoints; highly mobile vehicles break that assumption .

### 10. VANET Dynamics

- **Link durations are short**: High relative speeds make connections brief—contrary to static network assumptions .

### 11. Content-Centric Networking

- **CCN** is a realization of **ICN** principles: data is addressed by name rather than location, ideal for dynamic IoT/V2X content delivery .

### 12. Cooperative ICV Safety

- Vehicles sharing trajectory, road-hazard, and proximity data enable **collision avoidance** and smoother traffic flow—proven to reduce accidents .

## Assignment 11

### 1. Smart Grid Overview

- **Core use-case**: **Intelligent power plants** with bidirectional energy flow (generation ↔ consumers) .
- **Stakeholders**: Both **service providers** (utilities) and **consumers** benefit via efficiency, real-time pricing, outage detection .
- **Load forecasting**: Feasible using historic usage data, weather, and demand models to balance supply/demand .

### 2. Architecture & Integration

- **IP Network role**: Globally interconnects grid components—RTUs, SCADA centers, smart meters—for seamless data exchange .
- **Smart Home synergy**: Not isolated—homes can inject stored solar power back to grid and respond to demand-response signals .

### 3. Cloud Applications & Vulnerabilities

- **Smart-Grid cloud apps**:
    - **Information management** (meter data analytics)
    - **Energy management** (dynamic load control)
    - **Security** (intrusion detection, anomaly alerts)
- **Vulnerabilities**:
    - **Integrity** breaches (false data injection)
    - **Physical threats** (tampering RTUs)
    - **Dynamic system attacks** (smart-relay exploits)

### 4. IIoT (Industrial IoT)

- **Revolution stage**: IIoT is hallmark of the **4th Industrial Revolution**, blending cyber-physical systems with Big Data & AI .
- **Data intensity**: Generates massive streams—sensor telemetry, machine logs—requiring edge processing & cloud analytics .
- **Key utility**: **Power-plant virtualization**—modeling plant behavior in software to optimize dispatch and maintenance remotely .

### 5. Data Lifecycle & Management

- **Data flow**:
    1. **Generation** (sensors, meters)
    2. **Acquisition** (gateways, edge nodes)
    3. **Storage** (time-series DBs, data lakes)
    4. **Analysis** (predictive analytics, dashboards) .
- **Unstructured data**: ~ **80%** of world’s data (logs, images, sensor blobs) – drives need for NoSQL and distributed file systems .
- **SQL vs NoSQL**: SQL excels at **structured** (tabular) data; use NoSQL for flexible schemas and unstructured streams.

### 6. Intelligent Transport System (ITS)

- **Connectivity modes**: V2V, V2S (sensors), V2I (infrastructure), but **not** typically V2H (home) in ITS scope .

## Assignment 12

### 1. Qualitative vs Quantitative

- **Qualitative analysis**: examination of non-numerical data (e.g., interviews, observations).
- **Quantitative analysis**: statistical treatment of numerical data.

### 2. Statistical Techniques

- **ANOVA (Analysis of Variance)**
    - Tests mean differences **across ≥2 groups** by comparing between-group to within-group variance.
    - **Assumptions**:
        1. Homogeneity of variances
        2. Normally distributed response
        3. Independence of observations
    - **Types**: One-way, Two-way, K-way .
- **Regression Analysis**
    - Models relationship: predicts **dependent** variable from one/more **independent** variables .
- **ARIMA**
    - Time-series forecasting (uses AutoRegressive & Moving Average components + differencing).
- **Effect Size**
    - Standardized **mean** difference between groups; complements p-values by quantifying magnitude .

### 3. Dispersion Measures

- **Range**: Max – Min
- **Variance**: Average squared deviation from the mean .

### 4. IoT Analytics Approaches

- **In-place processing**: Data is processed **on the device** (edge analytics), reducing latency and bandwidth use .
- **Network-based**: Data sent to cloud/fog for processing.

### 5. Case Study: AgriSens Architecture

- **Three logical layers**:
    1. **Perception** (sensors: soil moisture, water level)
    2. **Processing** (edge nodes, gateways)
    3. **Application** (dashboards, alerts) .
- **Real-time monitoring**: Soil moisture readings streamed to dashboard for instant irrigation control .

### 6. Smart Healthcare Data Aggregator

- Known as **LPU** (Local Processing Unit) — collects & pre-processes patient sensor data before cloud uplink .
- **AmbuSense**: Privacy-aware system with patient identity masking built in .

### 7. Wearable AI Use-Case

- **Fall detection**: Handheld/activity-monitoring device uses onboard AI on accelerometer/gyroscope streams to detect sudden drops .

### 8. Motion Sensing

- **Gyroscope**: Detects device **tilt/rotation** (e.g., 15° tilt) .
- **Accelerometer**: Measures linear acceleration; can infer orientation but less precise for angular velocity.

