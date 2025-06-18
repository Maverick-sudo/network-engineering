# Network Engineering Notes Table of Contents
1. CHAPTER 1: OSI & TCP/IP IMPLEMENTATION OF NETWORKING PROTOCOLS

2. CHAPTER 2: TCP/IP NETWORK MODEL AND IMPLEMENTATION

3. CHAPTER 3: INTERNET PROTOCOL ADDRESSING TECHNIQUES

4. CHAPTER 4: TRANSPORT LAYER

5. CHAPTER 5: APPLICATION LAYER

6. CHAPTER 6: VOICE AND VIDEO PROTOCOLS

7. CHAPTER 7: CABLING STANDARDS (ETHERNET && FIBRE)

8. CHAPTER 8: DEVICE CATEGORIZATION

9. CHAPTER 9: DEVICE CONFIGURATION

10. CHAPTER 10: SWITCHES (LAYER 2)

11. CHAPTER 11: ROUTERS (LAYER 3)

12. CHAPTER 12: MANAGEMENT PLANE/LAYER PROTOCOLS

13. CHAPTER 13: CONTROL PLANE/LAYER PROTOCOLS

14. CHAPTER 14: NETWORK DEVICE SECURITY

15. CHAPTER 15: ARCHITECTURE, DESIGN, TOPOLOGY

16. CHAPTER 16: TROUBLESHOOTING & INFORMATION GATHERING TOOLS

17. CHAPTER 17: NETWORK TROUBLESHOOTING METHODOLOGY

18. CHAPTER 18: WIRELESS STANDARD & WIRELESS SECURITY

19. CHAPTER 19: SOFTWARE DEFINED NETWORKING

20. CHAPTER 20: INFRASTRUCTURE AS CODE (IAC): AUTOMATION & ORCHESTRATION
---

# CHAPTER 1: OSI & TCP/IP IMPLEMENTATION OF NETWORKING PROTOCOLS

A NETWORK is two or more computers or devices that are linked in order to share information. Networks are broken into different subsets based on their size and function. The OSI (Open Systems Interconnection) model provides a conceptual framework for understanding network functions.
The OSI Model was developed in the 1970s and 1980s, and it is a conceptual model that breaks networking into seven separate layers. Each layer refers to a set of functions that are responsible for specific tasks. In the OSI model, the definition of the application layer is narrower in scope. The OSI model defines the application layer as only the interface responsible for communicating with host-based and user-facing applications. OSI then explicitly distinguishes the functionality of two additional layers, the session layer and presentation layer, as separate levels below the application layer and above the transport layer. OSI specifies a strict modular separation of functionality at these layers and provides protocol implementations for each. In contrast, the Internet Protocol Suite compiles these functions into a single layer.
￼
The processes of encapsulation and de-encapsulation work in exactly the same way with the TCP/IP model as they do with the OSI model. At each layer of the this models a header is added during Data_encapsulation, and removed during Data_de-encapsulation.

![OSI Model](images/OSI.jpeg)

### Layer 1: Physical Layer (Cabling involving Data Bits/Streams))

The Physical, and lowest layer of the model, covers how unstructured data, like bits, is transmitted. Over these wires and signals, the raw data bits are received as a stream of 0s and 1s. Fixing errors that occur just at this layer means considering physical damage or interference. Some concrete examples of this are the ways wires are configured, the way signals are transferred over those wires, and the radio frequencies computers use. Technology such as WiFi, Bluetooth, and cable standards such as CAT5 and CAT6 all operate at this layer. This layer also includes the hardware part of modems, adapters, and repeaters.

* **Function:** Defines the means of transmitting raw bits over a physical data link connecting network nodes. It deals with hardware, cabling, and communication specifications.
* **Key Aspects:**
    * Translates bits into physical signals (electrical, light, radio).
    * Specifies electrical signals, physical connections, cabling types, and pin-outs.
    * Governs hardware specifications (e.g., RJ-45, fiber optic connectors, radio frequencies).
    * **Media Types:** Cat-5, Cat-6, Fiber Optic, Radio Waves, Infrared, Copper.
    * **Units:** Bits.
    * **Protocols/Standards:** Ethernet Physical Layer, USB, DSL, ISDN, Bluetooth.
* **Devices:** Hubs (obsolete), repeaters, network interface cards (NICs), modems, transceivers.

### Layer 2: Data Link Layer (Switching involving Data Frames)
The Data Link layer covers how data is sent from device to device when they are connected on the same local network. 

* **Function:** Provides reliable data transfer between adjacent network nodes. It handles physical addressing (MAC addresses), error detection (and sometimes correction), and defines how devices access the physical medium (e.g., CSMA/CD for Ethernet, CSMA/CA for Wi-Fi). It creates **frames**.
* **Components:**
    * **Switches:** Modern Layer 2 devices that forward frames based on MAC addresses. They create **separate collision domains** for each port, improving performance significantly over hubs.
    * **Network Interface Cards (NICs):** Process MAC addresses and frames.
    * **Wireless Access Points (APs):** At Layer 2, they bridge wireless clients to the wired network.
* **Performance Impact:**
    * **Switching Speed/Throughput:** High-performance switches can forward frames at wire speed, preventing bottlenecks.
    * **VLANs:** Properly configured VLANs segment broadcast domains, reducing broadcast traffic and improving network efficiency and security. Misconfigured VLANs can cause communication issues.
    * **Spanning Tree Protocol (STP):** Prevents Layer 2 loops but can block redundant paths, impacting potential bandwidth if not managed (e.g., with EtherChannel/LAG).
    * **MAC Address Table Size:** Affects how many devices a switch can learn and manage.

### Layer 3: Network Layer (Routing involving Data Packets)
The Network layer describes how data packets are routed between wider networks such as the Internet.  Data packet at the network layer is routed from a source IP address to a destination IP address via Domain Name System.
* **Function:** Handles logical addressing (IP addresses), routing of packets across different networks (inter-network communication), and path determination. It creates **packets**.
* **Components:**
    * **Routers:** Dedicated Layer 3 devices that make forwarding decisions based on IP addresses and routing tables. They connect different IP networks and create **separate broadcast domains**.
    * **Layer 3 Switches (Multi-Layer Switches):** Can perform both Layer 2 switching and Layer 3 routing functions.
    * **Firewalls:** Often operate at Layer 3 (and higher) for filtering traffic based on IP addresses and ports.
* **Performance Impact:**
    * **Routing Protocol Efficiency:** Efficient routing protocols (e.g., OSPF, EIGRP, BGP) quickly learn network changes and converge, minimizing downtime and packet loss.
    * **Router Processing Power:** Affects how quickly packets can be forwarded, especially for complex routing decisions or large numbers of routes.
    * **Network Congestion:** Routers play a key role in managing traffic flow and can be points of congestion if not adequately provisioned.
    * **Subnetting/IP Addressing Scheme:** A well-designed IP addressing scheme simplifies routing and improves network efficiency.
    * **ACLs/Firewall Rules:** Can add processing overhead, impacting throughput if too complex or numerous.


### Layer 4: Transport Layer (Involves Data Segments-TCP, Datagrams-UDP)
Layers 1 through 3 of the OSI Model are concerned with addressing, packet forwarding, and delivery, establishing basic connectivity. Layer 4, the **Transport Layer**, focuses on providing the transport services that network applications depend upon. 
The Transport layer refers to how data is actually transferred. The transport layer handles how the data(files, media, etc) from user/client are split (segmentation), the rate at which the packets are sent, and how errors are handled if data packets don’t make it to the site’s server. The most common transport protocols on the Internet are TCP (Transmission Control Protocol) and UDP (User Datagram Protocol). 
* **Function:** Deals with the transparent transfer of data between end users, providing reliable data transfer services to the upper layers. It handles segmenting data from the session layer and reassembling it into a data stream on the receiving end.
* **Key Aspects:**
    * **Reliability:** Manages connection-oriented communication (e.g., TCP) or connectionless (e.g., UDP).
    * **Flow Control:** Manages data transmission rates to prevent faster senders from overwhelming slower receivers.
    * **Congestion Control:** Manages network traffic to avoid overloading the network.
    * **Segmentation & Reassembly:** Breaks data from the session layer into segments (TCP) or datagrams (UDP) and reassembles them at the destination.
    * **Error Correction:** Detects and handles errors in data transmission (primarily TCP).
    * **Port Numbers:** Uses port numbers to identify specific applications or services.
* **Units:** Segments (TCP) or Datagrams (UDP).
* **Protocols:** TCP (Transmission Control Protocol), UDP (User Datagram Protocol), SCTP (Stream Control Transmission Protocol), DCCP (Datagram Congestion Control Protocol).

### Layer 5: Session Layer
When two computers or devices have established connection / started an exchange of information, we call that a session. The Session layer in OSI is responsible for opening, closing, and maintaining sessions. In terms of opening and closing, the session layer includes authentication and authorization measures. For example, without logging in or having the right permissions, you may not be able to connect to parts of a website. But if you are logged in, your access permission is stored for a set amount of time, or session length.
* **Function:** Establishes, manages, and terminates the connections (sessions) between applications. It enables the applications to send and receive data in an organized manner.
* **Key Aspects:**
    * **Dialogue Control:** Manages turn-taking in communication (who sends, when, for how long).
    * **Synchronization:** Inserts checkpoints into the data stream (e.g., for large file transfers) to allow recovery from network failures.
    * **Session Management:** Creates, maintains, and tears down sessions between processes.
* **Units:** Data (as organized into sessions).
* **Protocols/APIs:** NetBIOS, RPC (Remote Procedure Call), Sockets API, SQL.

### Layer 6: Presentation Layer
The Presentation layer includes all the methods that convert data into a format usable by an application⬇️. This layer handles functions such as encoding/decoding, encryption/decryption, and compression/decompression of files.
* **Function:** Ensures that data is presented in a format that the application layer can understand. It handles data format, encryption/decryption, and compression/decompression.
* **Key Aspects:**
    * **Data Formatting/Translation:** Translates data into a standard format (e.g., ASCII, EBCDIC).
    * **Encryption/Decryption:** Handles the encryption and decryption of data for secure communication.
    * **Compression/Decompression:** Compresses data for efficient transmission and decompresses it upon reception.
* **Units:** Data (in formatted/translated state).
* **Protocols/Standards:** JPEG, GIF, MPEG, ASCII, EBCDIC, SSL/TLS (though often seen spanning Presentation and Session, sometimes Transport).

### Layer 7: Application Layer
The application layer of the OSI model essentially provides networking options to programs running on a computer. It works almost exclusively with applications, providing an interface for them to use in order to transmit data. The final layer of the OSI model is the Application layer. This layer includes websites, browsers, email, mobile applications, and how they render Internet data so that we can interact with it.
* **Function:** Provides network services directly to end-user applications. It is the layer closest to the end user and enables users to interact with network services.
* **Key Aspects:**
    * Interacts with software applications that implement a communicating component.
    * Defines protocols for end-user services.
    * Provides user interfaces for network services.
* **Units:** Data (in application-specific format).
* **Protocols:** HTTP, FTP, SMTP, DNS, SSH, Telnet, DHCP, POP3, IMAP, SNMP.

---


# CHAPTER 2: TCP/IP NETWORK MODEL AND IMPLEMENTATION 
In the Internet protocol suite, the application layer contains the communications protocols and interface methods used in process-to-process communications across an Internet Protocol (IP) computer network. The application layer only standardizes communication and depends upon the underlying transport layer protocols to establish host-to-host data transfer channels and manage the data exchange in a client–server or peer-to-peer networking model. Though the TCP/IP application layer does not describe specific rules or data formats that applications must consider when communicating, the original specification (in RFC 1123) does rely on and recommend the robustness principle for application design.
You will hear more often about the TCP/IP model, which is a 4-Abstraction layered model that makes direct reference to current Internet implementations. Its foundational protocols are TCP and IP.

### OSI vs. TCP/IP Model Comparison

| Feature           | OSI Model                                    | TCP/IP Model                                   |
| :---------------- | :------------------------------------------- | :--------------------------------------------- |
| **Layers** | 7 Layers                                     | 4 or 5 Layers (Network Access, Internet, Transport, Application) |
| **Purpose** | Conceptual framework, standardized design    | Practical, industry-standard, widely implemented |
| **Development** | Developed by ISO                              | Developed by ARPA (DOD)                         |
| **Reliability** | Connection-oriented (Transport), Connection-less (Network) can be implemented | Both connection-oriented (TCP) and connectionless (UDP) options |
| **Protocols** | Protocol independent                         | Protocols are built into the model              |
| **Focus** | Clear separation of services, interfaces, protocols | Less strict separation, more flexible           |
| **Relevance** | Primary reference model for understanding networking | Practical model for Internet communication      |
| **Interoperability**| More rigid due to strict layering             | More adaptable, easier for cross-platform communication |
| **Security** | Security considerations at all layers (conceptual) | Security often implemented at specific layers (e.g., IPSec at Network) |

### Network Interface layer / LINK LAYER https://en.wikipedia.org/wiki/Link_layer
This layer emcompasses group of methods and communications protocols confined to the link that a host is physically connected to i.e the physical interface between the host system and the network hardware. It defines how data packets are to be formatted for transmission and routings. The link is the physical and logical network component used to interconnect hosts or nodes in the network and a link protocol is a suite of methods and standards that operate only between adjacent network nodes of a network segment. The link layer includes the protocols that define communication between local (on-link) network nodes which fulfill the purpose of maintaining link states between the local nodes, such as the local network topology, and that usually use protocols that are based on the framing of packets specific to the link types.  
The goal of this layer is to provide reliable communications between hosts connected on a network. Some of the services provided by this layer of the network stack include.
Data Framing - Breaking up the data stream into individual frames in packets. Data frames are groups of data bits at the Link layer that need to be routed to the correct physical location.
Checksums - Sending checksum data for each frame to enable the receiving node to determine whether or not the frame was received error-free/Corruption-free via Frame Check Sequence
Acknowledgment - Sending either a positive (data was received) or negative (data was not received but expected) acknowledgement from receiver to sender to ensure reliable data transmission.
Flow Control - Buffering data transmissions to ensure that a fast sender does not overwhelm a slower receiver.
Includes Various Protocols such as Wired Ethernet IEEE802.3, Wireless LAN IEEE802.11(WIFI), Neighbor Discovery Protocol(NDP), Secure Neighbor Discovery (SEND), Gratuitous ARP(GARP), Point-to-point Protocol(PPP), Media Access Control Protocols I.e Carrier-sense multiple access with collision detection (CSMA/CD) is a media access control (MAC) method used most notably in early Ethernet technology for local area networking. It uses carrier-sensing to defer transmissions until no other stations are transmitting. This is used in combination with collision detection in which a transmitting station detects collisions by sensing transmissions from other stations while it is transmitting a frame. When this collision condition is detected, the station stops transmitting that frame, transmits a jam signal, and then waits for a random time interval before trying to resend the frame. CSMA/CD is a modification of pure carrier-sense multiple access (CSMA). CSMA/CD is used to improve CSMA performance by terminating transmission as soon as a collision is detected, thus shortening the time required before a retry can be attempted.  
In Internet Protocol (IP) networks, the MAC address of an interface corresponding to an IP address may be queried with the Address Resolution Protocol (ARP) for IPv4 and the Neighbor Discovery Protocol (NDP) for IPv6, It routes data frames to the correct physical/MAC addresses. A switch (could be your computer or router) keeps track of local devices and their MAC addresses and makes sure data frames get to the correct physical location. Also Reverse Address Resolution Protocol(RARP) Operates here.
This particular layer has several unique security vulnerabilities that can be exploited by a determined adversary. https://en.wikipedia.org/wiki/Network_interface_layer_security
Wired Networks 
✔️ Content Address Memory(CAM)/ MAC Address table exhaustion attack
✔️ Address Routing Protocol(ARP) spoofing
✔️ Dynamic Host Config Protocol(DHCP) starvation
Wireless Networks 
✔️ Hidden Node Attack
✔️ De-auth(De-authentication) Attack

### INTERNET LAYER https://en.wikipedia.org/wiki/Internet_layer
Is a Layer of group of Internetworking methods(concepts of connecting multiple networks with each other via gateways), protocols & specifications that are used to transport network packets(IP-based packets) from the ordination host across network boundaries, If necessary to the destination host specified by an Internet protocol address put simply, This is where IP Logical Addressing system and Routing occur. A common design aspect in the internet layer is the robustness principle: "Be liberal in what you accept, and conservative in what you send"

In its operation as a connectionless protocol, the internet layer is not responsible for reliable transmission. It provides only an unreliable service, and best effort delivery. This means that the network makes no guarantees about the proper arrival of packets. This in accordance with the *end-to-end principle*. Since packet delivery across diverse networks is an inherently unreliable and failure-prone operation, the burden of providing reliability was placed with the end points of a communication path, i.e., the hosts, rather than on the network. This is one of the reasons of the resiliency of the Internet against individual link failures and its proven scalability. The aspect of data integrity function of providing reliability of service is the duty of higher level protocols, such as the (TCP) in the transport layer. 

The internet layer has three basic functions:
Routing: Is the forwarding of packets from a source host to the next router that is one hop closer to the intended destination host on another network through gateways.
For outgoing packets, select the next-hop host (gateway) and transmit the packet to this host by passing it to the appropriate link layer implementation. 
For incoming packets, capture packets and pass the packet payload up to the appropriate transport layer protocol, if appropriate.
Provide Error Detection & Diagnostic Capability. Usually through Internet Control Message Protocol(ICMP) & Internet Group Management Protocol(IGMP)


### TRANSPORT LAYER https://en.wikipedia.org/wiki/Transport_layer
The transport layer is responsible for delivering data to the appropriate application process on the host computers. The services in this layer are conveyed to an Application Programming Interface through the transport layer protocols, Their services may include the following features.
✔️Connection-Oriented Communication
✔️Same Order Delivery
✔️Reliability through error-detection code I.e Checksum, SYN/ACK
✔️Flow Control Management
✔️Traffic Congestion Avoidance 
✔️Multiplexing==>Ports providing multiple endpoints on single node.
*Transport Layer Protocols includes also
UDP-lite https://en.wikipedia.org/wiki/UDP-Lite
Reliable UDP(RUDP) https://en.wikipedia.org/wiki/Reliable_User_Datagram_Protocol
Multipath TCP https://en.wikipedia.org/wiki/Multipath_TCP
Stream Control Transmission Protocol(SCTP) https://en.wikipedia.org/wiki/Stream_Control_Transmission_Protocol 
Datagram Congestion Control Protocol(DCCP) https://en.wikipedia.org/wiki/Datagram_Congestion_Control_Protocol

At this layer, the TCP/IP protocol suite defines how different applications on separate hosts establish connections and track communications.
Understanding how protocols use ports to establish connections is critical for configuring and supporting network services. Protocols at the Transport layer are concerned with the delivery of **multiplexed application data**.

A TCP/IP host may be running multiple services/applications or communicating in parallel with multiple servers, clients, and peers. This means that incoming packets must be directed to the appropriate service or application. To facilitate this, each TCP/IP application type is assigned a unique identifier called a **Port Number**.

* **0-1023:** **Well-known ports** (assigned by IANA to common services like HTTP, FTP, SSH).
* **1024-49151:** **Registered ports** (can be registered for specific applications but are not "well-known").
* **49152-65535:** **Dynamic/Private/Ephemeral ports** (client applications assign their own temporary port numbers to track their requests; often called **Source Ports**).

A **Socket** is a software process that identifies a specific endpoint for communication. A connection is formed when a client requests a service from a server using a combination of IP address and port number.

* **Client Socket:** `Client IP:Client PORT` (e.g., `192.168.1.10:51234`)
* **Server Socket:** `Server IP:Server PORT` (e.g., `192.168.1.1:80`)

A server socket can support multiple connections from a number of client sockets, and a client may open multiple connections to the same server port. Each combination of Source Socket and Destination Socket forms a separate connection, listed in the host's **State Table**. Server replies are directed to the ephemeral (client) port that opened the connection, allowing data to be received by the correct application on the client.


### APPLICATION LAYER https://en.wikipedia.org/wiki/Category:Application_layer_protocols
This includes the opening and closing of sessions, translating data, and the interaction with content at the application level. Here, there are multiple protocols for web content, email, and accessing files, including HTTP, FTP, SMTP, and more. 

---



# CHAPTER 3: INTERNET PROTOCOL ADDRESSING TECHNIQUES 

### Internet Protocols Packet Structure: IPv4 Header

![IPv4](images/IP-Header-v4.png)

* **Function:** Contains important information for routing and delivering IP packets.
* **Key Fields:**
    * **Version:** Identifies the IP protocol version (IPv4 or IPv6).
    * **Header Length:** Specifies the length of the IP header (in 32-bit words).
    * **Type of Service (ToS) / Differentiated Services Code Point (DSCP):** Used for Quality of Service (QoS), prioritizing certain types of traffic.
    * **Total Length:** The total length of the IP packet, including header and data.
    * **Identification, Flags, Fragment Offset:** Used for IP fragmentation and reassembly.
    * **Time To Live (TTL):** Prevents packets from looping infinitely; decremented at each router hop. When it reaches 0, the packet is discarded.
    * **Protocol:** The Protocol field within the IP header indicates the higher-layer protocol encapsulated within the IP packet.
        * **TCP (6)** or **UDP (17)** are common transport layer protocols.
        * Some protocols are used **directly on IP** (rather than relying on transport layers) for specific functions, such as:
            * **ICMP (1)**: Internet Control Message Protocol (for error reporting and diagnostics like ping).
            * **IGMP (2)**: Internet Group Management Protocol (for managing multicast group memberships).
            * **GRE (47)**: Generic Routing Encapsulation, used to tunnel packets across an intermediate network (e.g., VPN implementations).
            * **EIGRP (88)**: Enhanced Interior Gateway Routing Protocol.
            * **OSPF (89)**: Open Shortest Path First.
            * **AH (50)**: Authentication Header, used in IPsec for data integrity and authentication.
            * **ESP (50)**: Encapsulating Security Payload, also used in IPsec for encryption and authentication.
    * **Header Checksum:** Used for error detection in the header.
    * **Source IP Address:** The IP address of the sender.
    * **Destination IP Address:** The IP address of the intended recipient.
    * **Options (Optional):** Rarely used, provides additional functionality.


### IPv4 Addressing Techniques

Networks in an internetwork must have a way of uniquely identifying each logical network and each individual host within those networks.

* At the Layer 2 (Data Link Layer), **MAC addresses** are used to identify interface end systems within a local segment.
* The **IP address** provides two pieces of information:
    * The **Network Number (Network ID)**: This number is common to all hosts on the same IP network.
    * The **Host Number (Host ID)**: This number uniquely identifies a host within an IP network.

#### IPv4 Subnetting

SUBNETTING is a logical subdivision of IP network. The process of dividing a network into two or more networks is called subnetting. The main purpose of subnetting is to help relieve network congestion and improve network performance & security. 
Subnet		1		2		4		8		16		32		64		128		256
Host		256 	128 	64		32		16		8		4		2		1
S.Mask		/24 	/25		/26		/27		/28		/29		/30		/31		/32

The 1s in the mask are always contiguous. For example, this mask is valid: 11111111 11111111 11111111 00000000
But the following string is not a valid mask: 11111111 00000000 11111111 00000000

An IPv4 address represents both a Network ID and a Host ID. A **32-bit Network Mask (netmask)** is used to distinguish these two components within a single IP address. The mask "conceals" the host ID portion, thereby revealing the network portion.

* **Longer Network Portion (e.g., 255.255.255.0 or /24):** Allows for more network IDs within the overall internetwork but with fewer available host addresses per network.
* **Shorter Netmask (e.g., 255.0.0.0 or /8):** Allows for millions of hosts per network but only 126 possible network addresses (for Class A).

The scheme of using rigid octet boundaries (Classful addressing) is inflexible, so a system of dividing networks into **subnetworks** was devised.

* **Subnet Addressing Hierarchy:** Subnetting introduces a three-level hierarchical structure:
    1.  Network ID
    2.  Subnet ID
    3.  Host ID
* **Creating Logical Subnets:** To create logical subnets, bits from the host portion of the IP address must be allocated as a Subnetwork ID. This means the Subnet ID often lies within an octet boundary.
* **Purpose of Subnetting:** To create Layer 3 broadcast domain segments with fewer hosts, thereby reducing broadcast traffic and improving network performance. The trick with subnet design is to fit the scheme to the requirements for the number of subnetworks and the number of hosts per subnet.
* **Impact of Mask Extension:** Each bit added to the mask approximately halves the number of available host addresses. For example, a `/24` (255.255.255.0) network like `198.51.100.0/24` allows $2^8 - 2 = 254$ possible host IDs.
* **Example Subnetting:** Subdividing `198.51.100.0/24` into `/28` subnets (using a subnet mask of `255.255.255.240`):
    * This leaves 4 bits for host IDs ($2^4 - 2 = 14$ possible host addresses) per subnet.
    * Example Subnets:
        * `198.51.100.0/28` (Hosts 1-14, Network 0, Broadcast 15)
        * `198.51.100.16/28` (Hosts 17-30, Network 16, Broadcast 31)
        * `198.51.100.32/28` (Hosts 33-46, Network 32, Broadcast 47)
        * `198.51.100.48/28` (Hosts 49-62, Network 48, Broadcast 63)
    * **Important:** The first address in a subnet is the **Network ID**, and the last address is the **Broadcast Address**. These two addresses are reserved and cannot be assigned to hosts.
* **Mask Application:** Only one mask is ever applied to the IP address of each interface. The mask containing the subnet information is only used **within** the IP network. External IP networks continue to address the whole network by its network ID (e.g., `198.51.100.0/24`). Hosts within the same larger network use the longer subnet mask to differentiate the subnets.
* A wildcard mask uses opposite bits of a subnet mask. For example, a subnet mask of 255.255.255.0 is 11111111.11111111.11111111.00000000 in binary. The corresponding wildcard mask would be 0.0.0.255, which is 00000000.00000000.00000000.11111111 in binary.
Shortcut for Wildcard Masks
To quickly convert a regular subnet mask to a wildcard mask, subtract each octet in the subnet mask from 255. Example:
Subnet Mask: 255.255.255.0
Wildcard Mask: 255 - 255.255 - 255.255 - 255.255 - 0 = 0.0.0.255

#### IPv4 Addressing Scheme: Magic Numbers and Rules

When designing an IPv4 addressing scheme, it's essential to consider:

* The number of IP networks and subnetworks required.
* The number of hosts per subnet that must be supported.

**Fundamental Rules for IP Addressing:**
* The network and/or host IDs **cannot be all 1s in binary** (reserved for broadcast addresses).
* The network and/or host IDs **cannot be all 0s in binary** (means "this network").
* Each **host ID must be unique** on its IP network/subnet.
* The **network ID must be unique** on the internet (if using a public address scheme).
* The **network ID must be unique** on your internal system of networks (if using a private address scheme).
* The network ID must be from a **valid public or private address range** and not from a loopback range, link-local reserved range, multicast range, or experimental range.

#### IP Configuration Tools

IP command-line utilities enable you to gather information about how your systems are configured and how they communicate over a TCP/IP network.

* Each host adapter must be allocated an appropriate **IP address** and **subnet mask**.
* The **IP address of the default gateway (router)** for its network.
* The **IP addresses of the DNS servers** that can resolve IP addresses to name labels.

These settings can be configured **statically** or **dynamically (DHCP)**.

**Windows Configuration Methods:**

* The IP configuration for each adapter interface is often set using the **GUI Properties dialog** accessed via the Network Connections Applet.
* You can also use **`netsh` commands** from the legacy command prompt interface. `netsh interface ip show config` will report the IP configuration. Changes made with `netsh` are typically persistent.
* **PowerShell cmdlets** are now more commonly used for script-based configuration:
    * `Get-NetAdapter` and `Get-NetIPAddress` can be used to query the existing configuration.
    * `New-NetIPAddress` or `Set-NetIPAddress` can be used to apply a new configuration or modify an existing one.



##### Public IP Addresses

* A public IP address is one that can establish a connection with other public IP networks and hosts over the Internet.
* They are allocated and governed by **IANA (Internet Assigned Numbers Authority)** and administered by Regional Internet Registries (RIRs) and ISPs.

##### Private IP Addresses

* Hosts communicating over a LAN could use a public addressing scheme, but more typically use **private addressing**.
* Private IP address ranges are drawn from specific pools defined by **RFC 1918** as **non-routable over the internet**:
| Class | IP Address Range        | Subnet Mask       | CIDR |
| :---- | :---------------------- | :---------------- | :--- |
| A     | 10.0.0.0 – 10.255.255.255 | 255.0.0.0         | /8   |
| B     | 172.16.0.0 – 172.31.255.255 | 255.255.0.0       | /12  |
| C     | 192.168.0.0 – 192.168.255.255 | 255.255.255.0     | /16  |

**Internet Access for Private Networks:**

1.  **Network Address Translation (NAT):** Through a router configured with a single or block of valid public IP addresses. Address translation between private IP addresses (behind the router) and public IP addresses (forward-facing IP) is achieved using NAT.
2.  **Proxy Server:** Through a proxy server that fulfills requests for Internet resources on behalf of clients. The proxy server itself must be configured with a public IP on its external-facing interface.

##### Automatic Private IP Addressing (APIPA)

* A host's IP configuration can be applied statically or use an auto-configuration method. For IPv4, auto-configuration usually means **DHCP (Dynamic Host Configuration Protocol)**.
* However, for systems where failure to contact DHCP or receive a response occurs, Microsoft developed **APIPA**.
* APIPA allows devices to communicate on a local network by selecting an IP address from the **`169.254.1.1` to `169.254.254.254` range (`169.254.0.0/16`)**. The first and last subnets within this range are typically unused.
* This type of addressing is referred to as **link-local** in RFC 3927 documentation.
* `255.255.255.255` is used to broadcast to the local network when the local network address is unknown.


#### Classful Addressing (Legacy IPv4)

Before the widespread use of netmasks (subnet IDs) to identify the network ID portion of an address, **Classful Addressing** allocated a network ID based on the first octet of the IP address.

* `0.0.0.0/0`: The "unspecified address" used when a specific IP address is unknown, typically as a source when a client is seeking a DHCP lease.

##### IPv4 Address Classes

| Class | First Octet Range | Default Subnet Mask | Common Use           |
| :---- | :---------------- | :------------------ | :------------------- |
| A     | 1-126             | 255.0.0.0           | Large networks       |
| B     | 128-191           | 255.255.0.0         | Medium-sized networks|
| C     | 192-223           | 255.255.255.0       | Small networks       |
| D     | 224-239           | N/A (Multicast)     | Multicast            |
| E     | 240-255           | N/A (Reserved)      | Research/Reserved    |

**Reserved IP Ranges (Classful Legacy):**
* **Class D addresses (`224.0.0.0 - 239.255.255.255`):** Used for **multicasting**.
* **Class E addresses (`240.0.0.0 - 255.255.255.255`):** Reserved for testing and experimental use.
* **Loopback Address (`127.0.0.0 - 127.255.255.255` or `127.0.0.0/8`):**
    * This range is reserved and configured as a **loopback address**.
    * A special type of address typically used to check that TCP/IP is correctly installed on the local host.
    * It doesn't require a physical interface to function.
    * A packet sent to a loopback address is not processed by a network adapter but is otherwise processed as normal by the host's TCP/IP stack.
    * A host will process a packet addressed to a loopback interface regardless of the interface on which it is received.


#### CIDR (Classless Inter-Domain Routing) and Supernetting

**CIDR** was designed to solve two major problems with classful addressing:

1.  The near-exponential growth in Internet routing tables.
2.  Class B addresses were becoming very scarce.

CIDR collapsed routing entries into one single entry, simplifying the information Internet routers needed to locate networks. Unlike classful addressing, CIDR does not determine the network mask based on the first octet of the IP address.

* **Dynamic routing protocols** that support classless addressing include RIPv2, EIGRP, OSPF, and BGPv4.

#### Supernetting

* **Supernetting** simplifies routing tables by combining multiple smaller networks into a single, larger network prefix.
* It is done to summarize subnets into one network ID. This is simply done by **shrinking the subnet mask** (i.e., making the CIDR prefix shorter).
* **Example:** Four /24 subnets (`198.51.101.0/24`, `198.51.102.0/24`, etc.) can be summarized as `198.51.100.0/22` (a "supernet prefix").
* Edge routers hosting these four networks collapse them into one single entry in their routing table. Routers external to the network (like ISPs) just use this `/22` prefix, so the complexity of the LAN's subnets is hidden and doesn't clog up their routing tables.
* The LAN's internal routers, however, use the `/24` prefix or multiple prefixes to create subnets of different sizes.

##### VLSM (Variable Length Subnet Masks)

* **VLSM** allows a network designer to allocate ranges of IP addresses to subnets that match a predicted need for the number of subnets and hosts per subnet more closely.
* It's a complementary addressing technique. Without VLSM, you'd have to allocate subnetted ranges of addresses that are all the same size and use the same subnet mask throughout the network. This often means that some subnets have many wasted IP addresses, or additional routing interfaces must be installed to connect several smaller same-sized subnets together within a single building or department.
* VLSM allows for **different/variable length netmasks (subnet masks)** to be used within the same IP network, allowing more flexibility in the design process.
* **Relationship to CIDR:**
    * You use the predicted number of host addresses needed to find the number of bits required for the host portion, which then determines the CIDR notation (prefix length).
    * More host bits = a shorter CIDR notation (e.g., `/24` vs. `/28`).
    * A shorter CIDR prefix means fewer network addresses/subnets but more host addresses per subnet.
* **Router-to-Router Links:** For router-to-router links (point-to-point links), typically no more than two addresses are ever required. Therefore, a `/30` prefix is often selected for router-to-router links (2 bits remaining for host IDs, $2^2 - 2 = 2$ usable addresses, one for each router interface).

#### VLANs (Virtual LANs) and Subnets

VLANs are a Layer 2 mechanism to address the contention dilemma when too many hosts are attached to the same switch, as excessive broadcast traffic can reduce performance.

* Each port on a managed switch can be assigned a **VLAN ID**.
* Using VLANs means that different groups of computers on the same physical cabling and attached to the same switch(es) can appear to be in **separate LAN segments**.
* Each VLAN is a **separate broadcast domain**.
* A subnetting scheme can be applied at Layer 3 to represent the VLAN design in the Layer 3 topology.
* **Benefits:**
    * Useful to divide a network into logically distinct zones for security and administrative control.
    * Networks that use different physical and data link technologies (e.g., Token Ring vs. Ethernet) should be logically separated as different subnets.

#### IP Forwarding (Routing)

The core function of IP is to facilitate the creation of a group of distinct but interconnected networks, referred to as the "Internetwork." This means that packets addressed to hosts on remote networks must be forwarded via one or more intermediate systems that establish routing between networks.

* **Forwarding at Layer 3** is referred to as **Routing**.
* **Forwarding at Layer 2** is known as **Switching**.

Nodes within each subnet can see one another directly (they are in the same **broadcast domain**), but they can only communicate with nodes in other subnets via a **router**.

#### ARP (Address Resolution Protocol)

Within each subnet or broadcast domain, nodes use **MAC addresses** to forward frames to one another. TCP/IP includes the ARP protocol to perform the task of resolving an IP address to a hardware (MAC) address.

* **Local Address Resolution:** When both sending and receiving hosts are within the same subnet, local address resolution takes place using **ARP requests** (broadcast) and **ARP replies** (unicast).
* **Remote Address Resolution:** If the destination address is on a remote network, the local host must use its **Default Gateway** to forward the packet. The host determines the MAC address of its default gateway using ARP.
* **Router ARP Usage:** Routers also use ARP messaging for their Ethernet interfaces. ARP messaging is specific to Ethernet networks.
* **Default Gateway IP:** The default gateway is typically set to the **first usable address** in the subnet (i.e., not the Network ID). For example, in `198.51.100.0/28`, `198.51.100.1` might be the default gateway.

#### How Default Gateways are Implemented

* **Same Subnet Communication:** If the network mask portions of the source and destination IP addresses match, both source and destination are in the same IP network/broadcast domain. Packet forwarding is done locally (Layer 2 switching).
* **Different Subnet Communication (Routing):** If the network mask portions of the source and destination IP addresses do not match, the packet must be routed to another IP network.
    * First, the source host delivers the packet to its own **default gateway**.
    * The **default gateway is a router** configured with a path to remote networks.
    * The router determines what to do with the packet by performing a subnet mask comparison between the source and destination addresses.
    * The router then uses its **routing table** to determine which interface it should use to forward the packet.
    * If no suitable path is found, the router drops the packet and informs the source host (via ICMP).
* The default gateway is the device that provides a route for traffic to leave the local subnet and access external networks by routing traffic. It usually has an IP address that is part of the subnet's range but is not assigned to an individual device within the subnet (commonly the lowest usable address).


#### IP Addressing Techniques

These techniques define how an IP packet addresses its recipient(s).
* **Unicast:** (One-to-One) When an IPv4 host wants to send a packet to a single recipient, it uses a unicast packet addressed to the destination host's unique IP address.
* **Broadcast:** (One-to-Everyone on the local segment) A host addresses multiple recipients on its local subnet by sending a broadcast packet to the **broadcast address** of its subnet (all hosts sharing the same broadcast address receive it).
    * Broadcast packets are delivered using a special Layer 2 MAC address (`FF:FF:FF:FF:FF:FF`), meaning there is also a broadcast domain scope at Layer 2.
    * With legacy devices like hubs and bridges, every port on all physically connected nodes is part of the same broadcast domain.
* **Multicast:** (One-to-Many of a specific group) IPv4 multicasting allows one host (on the Internet or a private IP network) or server to send content to other hosts that have identified themselves as interested in receiving the originating host's content.
    * Multicast packets are sent to a **destination IP address from a special range** (e.g., `224.0.0.0` to `239.255.255.255`) configured for use with multicast groups.
    * At Layer 2, multicasts are delivered using a special range of **MAC addresses** (`01:00:5E:xx:xx:xx`).
    * The switch must be multicast-capable (e.g., using **IGMP Snooping**); otherwise, it treats the multicast packet like a broadcast and floods it out of all ports, wasting bandwidth. IGMP is typically used to configure group memberships.
* **Anycast:** (One-to-One of Many) A group of hosts are configured with the **same IP address**. When a router forwards a packet to an anycast group, it uses a prioritization algorithm and metrics (e.g., shortest path) to select the host that is "closest" (most quickly able to receive and process the packet).
    * This allows the service behind the address to be provisioned more reliably, enabling load balancing and failover between the server hosts sharing the IP address (commonly used for DNS root servers).


#### Internet Control Message Protocol (ICMP) 

ICMP is a supporting protocol in the Internet protocol suite. It is used by network devices, including routers, to send *Error Reporting, Diagnostic Functions* and operational information indicating success or failure when communicating with another IP address. This errors are directed to the source IP address of the originating packet. for example, an error is indicated when a requested service is not available or that a host or router could not be reached. Internet Control Message Protocol version 6 (ICMPv6) is the implementation of the Internet Control Message Protocol (ICMP) for Internet Protocol version 6 (IPv6)

##### Common ICMPv4 Message Types (and their IPv6 equivalents in ICMPv6)

* **Source Quench:** (Type 4, Code 0) A request that the sender decreases its sending rate. Acts as flow control in the network layer. **Deprecated** in modern networks.
* **Redirect:** (Type 5) Request data sent to an alternative route. A Redirect message is a mechanism for routers to convey routing messages or information to hosts, informing them to update their routing information. Typically sent by gateways.
* **Time Exceeded:** (Type 11) Generated by a gateway to inform the source of a discarded datagram due to the Time-to-Live (TTL) field reaching zero. It may also be sent by a host if it fails to reassemble a fragmented datagram within a certain time.
* **Timestamp Request/Reply:** (Type 13/14) Used for time synchronization. Includes originating, receive, and transmit timestamps.
* **Address Mask Request/Reply:** (Type 17/18) Normally sent by a host to a router to obtain an appropriate subnet mask. The recipient responds with an Address Mask Reply message.
* **Destination Unreachable:** (Type 3) Generated by the host or its inbound gateway to inform the source that the destination is unreachable for some reason (e.g., network connection doesn't exist, protocol/port is inactive, data needs fragmentation but "Don't Fragment" bit is set).
￼
#### Internet Group Management Protocol (IGMP) 

IGMP is a communications protocol used by hosts and adjacent routers on IPv4 networks to establish multicast group memberships. IGMP is an integral part of IP multicast and allows the network to direct multicast transmissions only to hosts that have requested them.
IGMP is used on IPv4 networks. Multicast management on IPv6 networks is handled by Multicast Listener Discovery (MLD) which is a part of ICMPv6 in contrast to IGMP's bare IP encapsulation.  Through **IGMP Snooping**, routers (and Layer 2 switches capable of snooping) become multicast-aware of IGMP group membership requests. This allows them to avoid flooding multicast transmissions out of all ports (treating them like broadcasts), thereby conserving bandwidth and reducing unnecessary traffic for hosts not interested in the multicast stream.


#### ICMPv6 Packet Structure

| Field         | Bits (Offset) | Description                                                                                                                             |
| :------------ | :------------ | :-------------------------------------------------------------------------------------------------------------------------------------- |
| **Type** | 8 (0-7)       | Identifies the ICMPv6 message type.                                                                                                     |
| **Code** | 8 (8-15)      | Provides more specific information about the message type.                                                                              |
| **Checksum** | 16 (16-31)    | For error-checking. In ICMPv6, it includes a pseudo-header (from the IPv6 header) for more robust error detection.                       |
| **Message Body** | Variable      | Contains the specific information related to the message type (e.g., unreachable code, router advertisement data).                      |

The ICMPv6 protocol must limit the number of error messages sent to the same destination to avoid network overload.



### Internet Protocols Packet Structure: IPv6 Header

	0.	Source & Destination Address
	0.	Hop Limit – Replaces the TTL field in IPv4 but performs the same function
	0.	Traffic Class – Describes the packet's priority
	0.	Flow Label – Used for Quality of Service (QoS) management, useful for real-time streams. Set to 0 for packets not part of any delivery sequence or structure
	0.	Payload Length – Indicates the length of the packet payload, up to a maximum of 64 kilobytes.For flows where the payload is bigger than that, this field is ignored and a special Jumbo Payload (up to 4GB) option is established
	0.	Next Header – Describes what the next extension header (if any) is or where the actual payload begins.Also tells the destination host/router how to interpret the data that follows the header.The extension headers replace the Options field in IPv4 and cover functions such as:
	•	Fragmentation
	•	Reassembly
	•	Security (e.g., AH, ESP)
	•	Source Routing
IPv6 routers do not perform IP fragmentation. IPv6 hosts are required to do one of the following: perform Path MTU Discovery, perform end-to-end fragmentation, or send packets no larger than the default maximum transmission unit (MTU), which is 1280 octets.

![Ipv6](images/IP-Header-v6.png)

IPv6 is the most recent version of the Internet Protocol, designed to replace IPv4 due to the exhaustion of IPv4 addresses. It uses 128-bit addresses, providing a significantly larger address space than IPv4's 32-bit addresses. This expansion allows for connecting a vast number of devices to the internet, including the increasing number of Internet of Things (IoT) devices. 

Key Features and Benefits:
	•	Larger Address Space: IPv6 provides a theoretical address pool of 340 undecillion addresses, compared to IPv4's 3.7 billion. 
	•	Improved Routing: IPv6 simplifies routing headers, uses hierarchical addressing, and enables more efficient routing through techniques like summary routes and route aggregation. 
	•	No Need for NAT: IPv6 eliminates the need for Network Address Translation (NAT), as devices have their own unique public IPv6 addresses. 
	•	Enhanced Security: IPv6 includes built-in authentication and privacy support. 
	•	Auto-configuration: IPv6 allows for automatic address configuration, simplifying network setup. 
	•	Improved Multicast Routing: IPv6 provides better support for multicast routing. 
	•	Flow Labeling: IPv6 supports flow labeling, a mechanism for marking network packets with specific quality of service (QoS) requirements. 
Transition to IPv6:
	•	The transition to IPv6 is a global effort, with major ISPs and network equipment manufacturers supporting it. 
	•	The transition is expected to be gradual, with many organizations continuing to use IPv4 for the time being. 
It's important to ensure that devices and applications are IPv6-compatible to avoid potential connectivity issues during the transition. 


#### IPv6 Packet Header vs. IPv4 Options Field

The IPv6 header is streamlined and differs significantly from IPv4.

* **Hop Limit:** This field replaces the **TTL (Time-to-Live)** field in IPv4 but performs the same function: it limits a datagram's lifetime to prevent network loops.
* **Traffic Class:** Describes the packet's priority, similar to the DSCP (Differentiated Services Code Point) or ToS (Type of Service) in IPv4.
* **Flow Label:** Used for Quality of Service (QoS) management, particularly for real-time streams. It's set to `0` for packets not part of any specific delivery sequence or structure.
* **Payload Length:** Indicates the length of the packet payload, up to a maximum of 64 kilobytes. If the payload is larger, this field is set to `0`, and a **Jumbo Payload** option (up to 4 GB) is established in an extension header.
* **Next Header:** Describes what the next **Extension Header** (if any) is, or where the actual payload begins. It also tells the destination host/router how to interpret the data that follows the header.

#### IPv6 Extension Headers

Extension Headers replace the **Options field** in IPv4 and cover various functions such as:
* **Function:** IPv6 headers can be followed by one or more optional extension headers, which provide additional functionality beyond what's in the base IPv6 header. They improve flexibility and performance by offloading complex operations from routers.
* **Key Characteristics:**
    * Processed in the order they appear in the packet.
    * Not all extension headers are processed by every router. Only the Hop-by-Hop Options Header is examined by every router on the path.
    * A Next Header field in the preceding header indicates the type of the next header (either an extension header or the upper-layer protocol, like TCP or UDP).
* **Common Extension Headers:**
    * **Hop-by-Hop Options Header:** Examined by *every* node on the path. Used for optional information that needs to be processed by every device (e.g., Jumbo frames).
    * **Destination Options Header:** Carries optional information that needs to be examined only by the destination node(s).
    * **Routing Header:** Used by a source node to specify a list of intermediate nodes to be visited along a packet's path. Provides source routing functionality.
    * **Fragment Header:** Used when a packet is larger than the Path MTU (Maximum Transmission Unit). Allows a source to fragment a packet for transmission.
    * **Authentication Header (AH):** Provides data integrity, data authentication, and anti-replay services for IP packets. Part of IPSec.
    * **Encapsulating Security Payload (ESP) Header:** Provides confidentiality (encryption), data origin authentication, data integrity, and anti-replay services for IP packets. Also part of IPSec.
    * **Mobility Header:** Used by mobile IPv6 nodes for managing mobility-related signaling.


#### IPv6 Packet Structure (Comparison to IPv4)

The IPv6 packet structure is simplified, even though the headers are larger (40 bytes compared to IPv4's 20-60 bytes).

* **No Header Checksum:** IPv6 headers do not include a checksum. Error checking for the entire packet is performed at lower layers (e.g., Ethernet CRC) and higher layers (e.g., TCP/UDP checksum).
* **No Fragmentation by Routers:** IPv6 does not support fragmentation by routers. IPv6 hosts are required to either perform **Path MTU Discovery** (to determine the largest packet size that can be sent without fragmentation along an entire path) and send datagrams within that MTU, or fragmentation must be performed at the link layer nodes. This minimizes packet header processing by routers.
* **Jumbograms:** While IPv4 limits packets to 65,535 octets (64 KB) of payload, IPv6 nodes can handle packets exceeding this limit, referred to as **Jumbograms** (up to 4 GB).


#### IPv6 Addressing: Format and Header Details

IPv6 addresses are **128 bits long** and are typically represented in **hexadecimal notation (16 bytes)**. Each double-byte (16 bits) number is expressed as 4 hexadecimal digits. ADDRESS FORMAT: HEXADECIMAL means 16-bit representation - Double-Octet / byte (1Byte = 8bits)With each double-octet field expressed as 4 hex digits

**Example:** `ABCD:0183:F2C6:2C4F:3B2D:A6F5:F53C:2605`

##### IPv6 Address Compression

To make IPv6 addresses easier to read and write, compression rules are used:

* **Omitting Leading Zeros:** Leading zeros within any 16-bit block (hextet) can be ignored (e.g., `0183` becomes `183`).
* **Double Colon (::) Compression:** One contiguous series of all zeros (one or more hextets of `0000`) can be replaced by a double colon (`::`).
    * **Crucial Rule:** You can only use double colon compression **once** in a given address to avoid ambiguity.
    * **Example:** `2001:db8:0000:0000:0abc:0000:defo:1234` can be compressed to `2001:db8::abc:0:defo:1234`.
* **IPv6 in URLs:** When an IPv6 address is used as part of a URL (web address), it **must be enclosed within square brackets `[]`** because both the URL and IPv6 address use colon delimiters for different purposes.
    * **Example:** `http://[2001:db8::1]/index.html`
* Use double colon compression once, Don’t compress twice: **Example:** `2001:db8:0000:0000:0abc:0000:ABCD:1234` Compressed as: `2001:db8::abc:0:ABCD:1234` 

IPv6 uses **128-bit addresses**, providing an exponentially larger address space than IPv4.
* **Features:** Designed to address IPv4 address exhaustion, provides larger address space, improved security, and simplified header.
* **Address Length:** 128-bit addresses, represented in hexadecimal, separated by colons.
* **Address Types:**
    * **Global Unicast Address (GUA):** Publicly routable, equivalent to IPv4 public addresses. Starts with `2000::/3`.
    * **Link-Local Address (LLA):** Used for communication on a single link/segment. Automatically configured. Starts with `FE80::/10`. Not routable.
    * **Unique Local Address (ULA):** Private IPv6 addresses, routable within an organization but not on the internet. Starts with `FC00::/7` or `FD00::/8`.
    * **Multicast Address:** Used to send a single packet to multiple destinations. Starts with `FF00::/8`.
    * **Anycast Address:** An address assigned to multiple interfaces (typically different devices). Packet sent to anycast address is delivered to the nearest interface.
* **Simplified Header:** More efficient processing by routers.
* **Built-in Security:** IPSec is a fundamental part of IPv6.
* **Auto-configuration:** Supports Stateless Address Auto-configuration (SLAAC) and DHCPv6.

#### IPv6 Address Structure (Global Unicast Example)

* `Prefix/Length`: IPv6 network addresses are written using classless inter-domain routing (CIDR) notation, where `/N` is the length of the network prefix in bits.
* **Network Prefix (64 bits):**
    * **Global Routing Prefix (48 bits):**
        * First 3 bits (0010 or 0011 for global scope).
        * Next 45 bits allocated hierarchically to regional registries, ISPs, and end-users.
    * **Subnet ID (16 bits):** Identifies site-specific subnet addresses within the network.
* **Interface ID (64 bits):** Equivalent to the host portion in IPv4.

#### IPv4 and IPv6 Transition Mechanisms

Networks are likely to run both IPv4 and IPv6 in some or all parts of the infrastructure. Transition mechanisms ensure interoperability.

##### Dual Stack
* **Concept:** A network or device configured with **both IPv4 and IPv6 protocol stacks**.
* **Functionality:** Allows a single device (e.g., a host, router, or server) to have **both an IPv4 and an IPv6 address** assigned to its interfaces.
* **Communication:**
    * It can communicate with IPv4-only devices using IPv4.
    * It can communicate with IPv6-only devices using IPv6.
    * It can communicate with other dual-stack devices using either IPv4 or IPv6, often preferring IPv6 if available.
* **Benefit:** Enables seamless communication across networks where both IPv4 and IPv6 exist, facilitating a **gradual transition from IPv4 to IPv6** without immediate compatibility issues.
* **Deployment:** The most common and straightforward method for enabling coexistence and transition between IPv4 and IPv6 networks.

##### Tunneling IPv6 over IPv4
* **Concept:** Allows IPv6 packets to travel over an IPv4 infrastructure by encapsulating the entire IPv6 packet inside an IPv4 packet. This is a common **IPv6 transition mechanism** used when direct IPv6 connectivity is not available end-to-end.
* **Process:** An IPv6 packet is placed inside the data portion of an IPv4 packet, which is then sent across the IPv4 network. At the other end, the IPv4 header is removed, and the original IPv6 packet is forwarded.
* **Common Tunneling Methods:**
    * **Manual Tunnels:** Configured manually between two IPv6 routers over an IPv4 infrastructure. Requires static configuration on both tunnel endpoints. Simple for point-to-point connections.
    * **Generic Routing Encapsulation (GRE) Tunnels:** A more flexible tunneling protocol that can encapsulate various network layer protocols (including IPv6) within an IPv4 header. It's often used to create virtual point-to-point links.
    * **6to4 Tunnels:** An automated tunneling mechanism that allows isolated IPv6 networks to communicate over an IPv4 infrastructure without explicit tunnel configuration for every connection. It uses a specific IPv6 prefix (`2002::/16`) for addresses assigned to 6to4 interfaces, which includes a representation of the IPv4 address.
    * **Intra-Site Automatic Tunnel Addressing Protocol (ISATAP) Tunnels:** Designed for internal IPv6 communication within an IPv4-only enterprise network. It creates a point-to-multipoint tunnel by dynamically using the IPv4 address of the destination as part of the IPv6 address.


#### IPv6 Integrated Auto-Configuration and Deployment

In IPv6, an interface must always be configured with a **link-local address** (one for each link), even if it also has a globally unique address. One or more routable addresses can be assigned in addition to the link-local address.

* As with IPv4, you can either assign a routable IPv6 address statically (generally reserved for routers and possibly some servers) or use an automatic addressing scheme.

#####  IPv6 Neighbor Discovery Protocol (NDP)

* **Function:** NDP is an essential IPv6 protocol that uses ICMPv6 messages to perform functions similar to ARP (Address Resolution Protocol) and ICMP Router Discovery in IPv4, along with new capabilities. It operates at the network layer.
* **Key Functions of NDP:**
    * **Address Resolution:** Resolves IPv6 addresses to MAC addresses (like ARP).
    * **Router Discovery:** Allows hosts to discover routers and learn network prefixes.
    * **Prefix Discovery:** Hosts learn on-link prefixes.
    * **Parameter Discovery:** Hosts learn other configuration parameters (e.g., MTU).
    * **Duplicate Address Detection (DAD):** Ensures a newly configured IPv6 address is unique on the link.
    * **Neighbor Unreachability Detection (NUD):** Confirms if a neighbor is still reachable.
    * **Redirect Functionality:** Routers can inform hosts of a better first-hop router for a specific destination.
* **NDP Messages (ICMPv6 Types):**
    * **Router Solicitation (RS):** Sent by hosts to discover routers on the link or to request Router Advertisements immediately.
    * **Router Advertisement (RA):** Sent by routers periodically or in response to an RS. Contains network prefixes, link MTU, hop limit, and flags for SLAAC or DHCPv6.
    * **Neighbor Solicitation (NS):** Sent by a node to resolve a neighbor's link-layer address (MAC) or to perform Duplicate Address Detection (DAD).
    * **Neighbor Advertisement (NA):** Sent by a node in response to an NS message, or unsolicited to announce a change in its link-layer address. Contains the node's link-layer address.
    * **Redirect:** Sent by a router to inform a host of a better first-hop router for a specific destination.


##### Stateless Address Auto-Configuration (SLAAC)

* **Function:** Allows IPv6 hosts to automatically configure their own addresses and network parameters without a DHCP server.
* **Process:**
    * Hosts generate a Link-Local Address (LLA) using their MAC address (or a privacy extension).
    * They send a Router Solicitation (RS) message to discover routers on the link.
    * Routers respond with a Router Advertisement (RA) message, which includes the network prefix and other configuration information.
    * The host combines the network prefix from the RA with its Interface ID to form a Global Unicast Address (GUA).
    * Duplicate Address Detection (DAD) is performed to ensure the address is unique on the link.
* **Key Characteristic:** No central server is required for IP address assignment for global addresses.


##### Interface ID (EUI-64 and Privacy Extensions)

The 64-bit Interface ID, which is the host portion of an IPv6 address, can be determined using two main techniques:

1.  **EUI-64 (Extended Unique Identifier):**
    * A relatively simple translation mechanism allows driver software to create a 64-bit Interface ID from the 48-bit MAC address.
    * The MAC address is split in half, `FF:FE` is inserted in the middle, and the 7th bit (Universal/Local bit) is inverted.
    * This is also known as a MAC-derived address or Interface Identifier.
2.  **Privacy Extensions (Temporary Interface ID / Token):**
    * The client uses a cryptographically generated pseudo-random number for the Interface ID.
    * **Why?** Because the EUI-64 method has privacy concerns as interface identifiers would allow a host to be identified and closely monitored when connecting to the Internet (since the MAC address is unique and semi-permanent). Using a token mitigates this to some degree by rotating the Interface ID regularly.

##### IPv6 Multicast Addressing

IPv6 supports multicast. The components of a multicast address (`ff00::/8`) are subdivided as follows:

* **`ff` (First 8 bits):** Indicate that the address is within the multicast scope (`11111111`).
* **Flags (Next 4 bits):** Used to indicate types of multicast, if necessary (e.g., transient or well-known).
* **Scope (Next 4 bits):** Determine the scope of the multicast group:
    * `1` (0001): Node-Local (to all interfaces on the same node).
    * `2` (0010): Link-Local (to all nodes on the same link).
    * `5` (0101): Site-Local (deprecated).
    * `E` (1110): Global.
* **Group ID (Final 112 bits):** Define multicast groups within that scope.

The **Multicast Listener Discovery (MLD)** protocol allows nodes to form a multicast group and discover whether members of a group are present on a local subnet. Well-known multicast addresses are reserved for specific functionality (e.g., `ff02::1` for all nodes, `ff02::2` for all routers). Hosts use an appropriate multicast address to communicate with groups.

**No Broadcast Addressing in IPv6:** IPv6 does not implement broadcast addresses. Multicast addresses are used instead for functionalities that would have used broadcasts in IPv4.

#### ICMPv6 Key Features

ICMPv6 is an updated version of ICMP (ICMPv4) with new features.
1.  **Error Messaging:**
    * Supports similar destination unreachable and time exceeded (TTL=0, now "Hop Limit=0") messaging as ICMPv4.
    * Introduces the **Packet Too Big** class of error. Under IPv6, routers are no longer responsible for packet fragmentation and reassembly. The host must ensure that packets fit within the **MTU (Maximum Transmission Unit)** of the underlying links used (Path MTU Discovery).
2.  **Informational Messaging:**
    * Supports ICMPv4 functions like Echo Request/Reply (ping).
    * Includes a whole new class of messages designed to support **Neighbor Discovery (NDP)** and **Multicast Listener Discovery (MLD)** protocols, such as Router Advertisements (RA) and Neighbor Solicitations (NS). MLD is used for multicast listener discovery.

#### RFC 5952 is "A Recommendation for IPv6 Address Text Representation" which suggests standard IPv6 address representation.

What is An RFC "Request for Comments" is a publication from the Internet Society (Internet Engineering Task Force)
and are the official documents of Internet specifications, protocols, procedures.
Leading zeros must be removed in each hextet (16-bit segment)/double-octet
Rules for Shortening IPv6 Addresses:
	•	:: Must be used to shorten the longest contiguous string of all 0 hextets.
	•	If there is only one hextet of all zeros, it can also be shortened to ::.
	•	If there are two equal length choices of all 0 hextets, use :: to shorten the one on the left.
	•	Hexadecimal characters must be written using lower case (a-f).

INTERFACE ID (Known as EUI-64)
Where MAC Address = 48-bit →→ Converted to 64-bit
Can be determined using 2 techniques:

#### MAC-Derived Interface Identifier (EUI-64 Format)
A relatively simple translation mechanism allows driver software to create a 64-bit Interface ID (EUI-64) from the MAC address by inserting 16 bits (FFFE) in the middle.
	•	Also known as:
	•	MAC-Derived Address
	•	Interface Identifier
	•	EUI-64
HOW [EUI-64] IS CREATED FROM MAC ADDRESS + fffe [16 bits]
Consider a MAC Address 00:0c:29:ab:1c:2d (Example MAC Address).
The MAC address is split into halves, and modified into EUI-64
by inserting a known constant 16bits (hexadecimal) of FFFE.
Consider a MAC Address b4:45:5a:1c:2d:3f
Split into halves: b4:45:5a and 1c:2d:3f
Insert FFFE: b4:45:5a:ff:fe:1c:2d:3f
7th bit of the first octet (b4 in binary is 1011 0100): 1
Flipping the 7th bit: 0
Binary after flipping: 1011 0000
Hexadecimal after flipping: b0
Therefore EUI-64 = b045:5aff:fe1c:2d3f
64 bit long.

EUI stands for Extended Unique Identifier: Modified EUI-64 is a method of converting a MAC Address (48 bits) into a 64-bit Interface Identifier [which then becomes the "host portion" of a /64 IPv6 Address]. 
How to Convert the MAC Address to a Modified EUI-64:
	0.	Divide the MAC Address in half: 12:34:56 and 78:90:AB (Example: 1234.5678.90AB)
	0.	Insert FFFE in the middle: 12:34:56:FF:FE:78:90:AB
	0.	Invert the 7th bit: The 7th bit (Universal/Local bit) of the first octet is inverted. Example: If the first octet is 12 (binary 00010010), inverting the 7th bit (from the left, starting at 1) results in 00010110, which is 16 in hexadecimal. So, 12:34:56:FF:FE:78:90:AB becomes 16:34:56:FF:FE:78:90:AB. WHY INVERT the 7th bit? Because MAC Addresses can be divided into 2 types: 
UNIVERSALLY ADMINISTERED ADDRESS (UAA) - Uniquely assigned to the device by the manufacturer.
LOCALLY ADMINISTERED ADDRESS (LAA) - Manually assigned by an administrator (MAC Address). 
You can identify a UAA / LAA by its 7th bit of the MAC address, called the U/L bit (Universal/Local bit).
U/L bit set to 0 → UAA (in MAC address) means the EUI-64 Interface ID was derived from a UAA. 
U/L bit set to 1 → LAA (in MAC address) means the EUI-64 Interface ID was derived from a LAA. 
IN the context of IPv6 addresses and EUI-64, the meaning of the U/L bit is reversed. Therefore: 
U/L bit set to 0 (in EUI-64) → Indicates a Universally Administered Address (derived from a UAA MAC). 
U/L bit set to 1 (in EUI-64) → Indicates a Locally Administered Address (derived from a LAA MAC).


#### Privacy Extensions / Temporary Interface ID (Token-Based)
The client uses a false pseudo-random number for the Interface ID.
⚠️ Why? The first method has privacy concerns, because the Interface Identifier exposes the MAC, making the host uniquely identifiable and trackable on the internet.
🔐 Using a token (random Interface ID) mitigates this to some degree.


### IPv6 Addressing Techniques

Network addresses are written using Classless Notation, where /nn is the length of the network prefix in bits. Within the /64-bit network IP — as with IPv4 subnets — the length of any given network prefix is used to determine whether two addresses belong to the same network, within that bit-limit, including the subnet as well.
IPv6 multicast addressing has features and protocols in common with IPv4 multicast, but also provides changes and improvements by eliminating the need for certain protocols. IPv6 does not implement traditional IP broadcast, i.e. the transmission of a packet to all hosts on the attached link using a special broadcast address, and therefore does not define broadcast addresses. In IPv6, the same result is achieved by sending a packet to the link-local all nodes multicast group at address ff02::1, which is analogous to IPv4 multicasting to address 224.0.0.1.
• UNICAST ADDRESSES: Used for one source to a single destination.
• MULTICAST ADDRESSES: Used for one source to multiple destinations (that joined the specific Multicast Group). The Destination-IP-Address is configured from a special range for use within the Multicast Group.
• ANYCAST ADDRESSES: Used for "one source" to "one of many destinations" (the nearest one).

UNICAST ADDRESSING (OR NETWORK ADDRESSING)
In IPv6, unicast addressing is scoped — it’s tied to a region of the network.
There are 3 common types:
	0.	Global Unicast Addressing
	0.	Link-Local Addressing (Private Addressing)
	0.	Unique Local Addressing

#### Global Unicast IPv6 Addressing
The equivalent of public IPv4 addresses. These are public addresses which can be used over an internetwork.
NOTE: They are globally unique and allow for regular routing across the internet. Originally defined as the 2000::/3 block, encompassing addresses from 2000:: to 3FFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF.
However, now defined as all addresses that do not fall within other reserved prefixes.
Example: 2001:0DB8:8B00:0001:0000:0000:0000:0001/64
	•	The first 3 bits indicate that the address is within the global scope.Globally scoped unicast addresses start with 2 (0010) or 3 (0011).
	•	48-bit Global Routing Prefix: Assigned by IANA to the ISP, are allocated hierarchically to regional registries → ISPs → End-users.
	•	16-bit Subnet Identifier: Used by the organization to create various subnets or identify site-specific subnet addresses.
	•	64-bit Interface Identifier: Specified by the organization to identify the host portion of the address.
Custom Routing Prefix + Subnet breakdown:
| 3-bit Network ID | 45-bit Global Routing Prefix | 16-bit Subnet ID | 64-bit Interface ID |
|------------------|------------------------------|-------------------|----------------------|
➡️ Total: 128-bit IPv6 Global Unicast Address

#### Unique Local Unicast Addressing
These are private addresses which cannot be used over the Internet.
They do not necessarily need to be globally unique since they are used freely within internal networks.
Cannot be routed over the Internet. Packets destined for a unique local address will be dropped by the ISP.
Uses the block FC00::/7 (FC00:: to FDFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF); however, a later update
requires the 8th bit to be set to 1, so the first two digits will be FD. Ranges are FD00::/8 to FDFF::/8.
Example: FD45:93AC:8A8F:0001:0000:0000:0000:0001/64
	•	8-bit Prefix: Indicates a Unique Local Address (FD::/8).
	•	40-bit Global ID: Randomly generated.
	•	16-bit Subnet Identifier: Used by the organization for subnetting.
	•	64-bit Interface Identifier: Assigned to the host.

#### Link-Local Unicast Addressing
Refers to addresses that are used for communication within a single link (subnet). Automatically generated on IPv6-enabled interfaces. Use command ipv6 enable on an interface (under interface configuration mode) to enable IPv6 on that interface.
Uses the address block FE80::/10 (FE80:: to FEBF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF).
However, the standard states that the 54 bits after FE80::/10 should be all 0 initially, and the last 64 bits form the interface identifier. Similar to the Global Unicast Address, the Host 64-bit / Interface-ID is generated using the Modified EUI-64 format.
Link-Local: 
Routers will not route packets with a Link-local destination IPv6 address, but they can be used for routing protocol peerings (OSPF uses Link-local addresses for Neighbor adjacencies) and for Static Routes as next-hop addresses. Also used by Neighbor Discovery Protocol to discover nodes and routers on the local link. ✅ No need for ARP or MAC-to-IP mapping tricks in IPv6.
	•	Nodes on the same subnet are referred to as neighbors
	•	 Link-local range: fe80::/10
	•	Starts with fe80 
	•	Prefix: 1111 1110 10 → 54-bit prefix
	•	Next 54 bits set to 0
	•	Last 64 bits are the Interface ID
Think of it as the IPv6 equivalent of IPv4’s APIPA (Automatic Private IP Addressing) → 169.254.0.0/16

However, unlike IPv4, an IPv6 host is always configured with a link-local address (one for each interface), even if it also has a globally unique address.
According to OS behavior, a link-local address is also appended with a Zone Index or Scope ID, in the form:
	•	%1 on Windows
	•	or an interface name like eth0 on Linux/macOS
📌 This is used to determine the source of the address and bind the traffic to a specific interface


#### IPv6 Multicast Addressing
	•	Uses special address ranges starting with ff__::/8
	•	Common link-local multicast: ff02::/16
Multicast scope and type is embedded in the address structure:
| 8 bits (Prefix)       | 4 bits (Flags)       | 4 bits (Scope)       | 112 bits (Group ID)        |
|------------------|------------------|-------------------|------------------------|
|      ff                      |   Flags (0000)     | Scope (e.g. 1, 2)    |    Group Identifier          |

	•	First 8 bits: Always 1111 1111 (ff) → Indicates multicast address
	•	Next 4 bits (Flags): Specify multicast type or behavior
	•	Next 4 bits (Scope): 🧠 Well-known Multicast Addresses are used for specific purposes (like all-routers or all-nodes groups). For example:
	•	0001 → Node-local (all interfaces on the same node) -> ff02::1 — All nodes on the local link
	•	0010 → Link-local (on the same subnet or link) -> ff02::2 — All routers on the local link
	•	Final 112 bits: Define the multicast group within that scope

#### IPv6 Anycast Addressing
A new feature of IPv6 whereby ONE source communicates with one of multiple destinations. Anycast means that a group of multiple routers are configured with the same IPv6 address. They make use of a Routing protocol to advertise the address and a Prioritization Algorithm & various Metrics to forward packets to the Destination Address (anycast group). Routers will forward packets to its nearest router configured with that Anycast Group IP Address based on the Routing protocol's prioritization & metrics.
There is no specific address range for Anycast Addresses. They use a regular Unicast address (Global Unicast or
Unique Local) and specify it as an anycast Group Address. This is configured using the "anycast" keyword.
Example:
Router(config-if)# ipv6 address 2001:db8:1:1::99 /128 anycast
Notice the use of a /128 prefix with a Global Unicast address being configured as anycast.

#### Multicast vs Broadcast in IPv6
	•	Multicast addresses are reserved to replace the functionality of broadcast addresses (which do not exist in IPv6).
	•	Instead of broadcasting, IPv6 hosts use appropriate multicast addresses to reach multiple devices on a local subnet.

@ * Unspecified Address ::= ::/128: Used for when a host hasn't obtained a valid address yet.
@ IPv6 Default Routes: Are configured as ::/0, which is the IPv6 equivalent of IPv4's 0.0.0.0/0.
@ * Loopback Address ::= ::1/128: Resolves to test the loopback TCP/IP protocol stack on the local device.
Messages sent to this address are processed within the local device, but not sent to other devices. This is the IPv6 equivalent of IPv4's 127.0.0.1.

NB: An IPv6 Solicited-Node multicast Address is calculated from a Unicast Address (typically Link-Local).
The format is ff02::1:ff followed by the last 24 bits (6 hexadecimal digits) of the Unicast Address.
Example: If a Unicast Address is fe80::aabb:ccdd:eeff, its Solicited-Node multicast address would be ff02::1:ffaa:bbcc:eeff.

Note: IPv6 defines Multicast scopes which indicate how far the packets should be forwarded. The addresses starting with "FF02::" are Link-Local Scope.
The Internet Protocol Version 6 (IPv6) address prefixes [FE80::/10 and FF02::/16] are not routable
over the public internet. [FE80::/10] are Link-Local Unicast addresses, and [FF02::/16] are Link-Local Multicast addresses. Likely the [FC00::/7] range used for Unique Local Unicast addressing are globally not routable outside the organization's internal network.

#### Multicast Listener Discovery (MLD) 
The MLD protocol allows nodes to Join a multicast group && Discover whether other members of a multicast group are present on the link

#### Neighbor Discovery Protocol (NDP)
Neighbor Discovery Protocol (NDP): Is a protocol used with IPv6. It replaces ARP (which is no longer used in IPv6)
and performs the ARP-like function. NDP uses ICMPv6 messages and solicited-node multicast addresses to learn the
MAC address of other hosts (ARP in IPv4 uses broadcast messages). Two key message types are within NDP:
	0.	Neighbor Solicitation (NS) + ICMPv6 Type135:
	•	Source IP: The IPv6 address of the node sending the solicitation.
	•	Destination IP: The Solicited-Node multicast address of the target IPv6 address.
	•	Destination MAC: A multicast MAC address based on the destination IPv6 address.
	0.	Neighbor Advertisement (NA) + ICMPv6 Type 136:
	•	Source IP: The IPv6 address of the node sending the advertisement.
	•	Destination IP: The IPv6 address of the node that sent the Neighbor Solicitation (Unicast).
	•	Destination MAC: The unicast MAC address of the node that sent the Neighbor Solicitation.

Routers on the local network communicate via two main message types within NDP:
	0.	Router Solicitation (RS) = ICMPv6 Type 133:
	•	Sent to Multicast address FF02::2 (All Routers).
	•	Sent when an interface is enabled/a host is connected to the network.
	•	Allows hosts to automatically discover routers on the local network.
	0.	Router Advertisement (RA) = ICMPv6 Type 134:
	•	Sent to Multicast Address FF02::1 (All Nodes).
	•	Sent periodically even if the router hasn't received an RS message.
	•	Sent in response to RS messages.
	•	Contains the IPv6 network prefix(es) allocated to the local link, default router information, and other configuration parameters.
	•	Facilitates Stateless Address Autoconfiguration (SLAAC).

IPv6 Address Allocation Methods:
	•	SLAAC (Stateless Address Autoconfiguration) in IPv6:
	•	Hosts use the RS/RA messages to learn/discover the known IPv6 Network prefix(es) that have been allocated to the Network Segment of the local link, then automatically generate an IPv6 address.
	•	Using EUI-64 or a privacy extension, the device generates its own interface ID.
	•	The device does not rely on a stateful server like DHCPv6 for address assignment.
	•	Using the "ipv6 address /prefix-length eui-64" command, you manually enter the prefix.
	•	Using the "ipv6 address autoconfig" command, you don't need to enter the prefix; the device uses NDP to learn the prefix used on the local link. The devices will use EUI-64 to generate the Interface ID, or a pseudo-randomly generated number.
	•	Stateful DHCPv6:
	•	Hosts explicitly request IPv6 addresses and other configuration parameters from a DHCPv6 server.
	•	The DHCPv6 server maintains state information about the addresses it has assigned.
	•	Static Allocation:
	•	IPv6 addresses are manually configured on the host.


#### Duplicate Address Detection (DAD): 
Allows hosts to check if other devices on the local link are using the same IPv6 Address. DAD Uses 2 Messages (NS & NA). DAD is performed any time an IPv6 enabled interface initializes or an IPv6 address is configured on an interface (SLAAC/Manual).
The Host will send an NS to its own IPv6 address [Solicited-Node Multicast] to perform DAD:
	•	If it doesn't get a Reply, it knows the address is Unique.
	•	If it gets a reply, it means another host on the network is already using the address. 


#### Common IPv6 Address Prefixes (w/ IPv4 Equivalents & Use Cases)

| Prefix / Address      | Name / Scope            | Description                                                   | IPv4 Equivalent           |
| :-------------------- | :---------------------- | :------------------------------------------------------------ | :------------------------ |
| `fe80::/10`           | Link-local (Unicast)    | Used on the local subnet; not forwarded by routers            | `169.254.0.0/16` (APIPA)  |
| `::/128`              | Unspecified Address     | A host that has not yet obtained an address                   | `0.0.0.0`                 |
| `::1/128`             | Loopback Address        | Used to test the local host (loopback interface)              | `127.0.0.1`               |
| `ff00::/8`            | Multicast (Internetwork Scope) | General prefix for multicast addresses                        | N/A (IPv4 used broadcast) |
| `ff02::1`             | All Nodes (Link-local Multicast) | Replaces broadcast; reaches all nodes on local link           | `255.255.255.255` (limited use) |
| `ff02::2`             | All Routers (Link-local Multicast) | Used to reach all routers on the local link                   | N/A                       |
| `ff02::1:ffXX:XXXX`   | Solicited-node Multicast | Used for NDP (Neighbor Discovery Protocol) to find link-layer addresses | ARP equivalent            |
| `::/0`                | Default Route           | Represents the default gateway                                | `0.0.0.0/0`               |

#### IPv6 Multicast Addresses and Scopes

| IPv6 Multicast Address | IPv4 Equivalent | Multicast Scope        | Description           | Notes                                                                                                                                                                                                            |
| :--------------------- | :-------------- | :--------------------- | :-------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `FF01::X/16`           | N/A             | Node/Interface-Local   | Used to send traffic to a service within the local interface/host. | Packet doesn't leave the local host. The Node/Interface-local multicast [`FF01::/16`] addresses are only used on the interface itself. |
| `FF02::1/16`           | `224.0.0.1`     | Link-Local             | All Nodes/Hosts       | Functions as a Broadcast. Refers to its use in the local subnet. Routers will not route these packets between subnets.                                                                                   |
| `FF02::2/16`           | `224.0.0.2`     | Link-Local             | All Routers           | Hello messages.                                                                                                                                                                                          |
| `FF02::5/16`           | `224.0.0.5`     | Link-Local             | All OSPF Routers      | Multicast message.                                                                                                                                                                                       |
| `FF02::6/16`           | `224.0.0.6`     | Link-Local             | All OSPF DR/BDRs      | Multicast message.                                                                                                                                                                                       |
| `FF02::9/16`           | `224.0.0.9`     | Link-Local             | All RIP Routers       | Multicast message.                                                                                                                                                                                       |
| `FF02::A/16`           | `224.0.0.10`    | Link-Local             | All EIGRP Routers     | Multicast message.                                                                                                                                                                                       |
| `FF05::X/16`           | N/A             | Site-Local             | N/A                   | Packets can be forwarded by Routers but should be limited to a small physical location.                                                                                                                  |
| `FF08::X/16`           | N/A             | Organization-Local     | N/A                   | Wider in scope than site-local, covering an entire company (organization).                                                                                                                               |
| `FF0E::X/16`           | N/A             | Global                 | N/A                   | No boundaries, possible to be routed over the Internet. ROUTABLE                                                                                                                                         |

#### Common IPv6 Address Prefixes and Types

| Address Type               | Prefix/Range (Hex)              | Description                                                                                                                                                                                                                                                                                                                                                                                               | IPv4 Equivalent (Conceptual)                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| :------------------------- | :------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Global Unicast** | `2000::/3` (`2xxx::/3` to `3xxx::/3`) | Routable over the internet, similar to public IPv4 addresses. Assigned hierarchically by IANA, RIRs, ISPs, and then to end-users. Begins with `2` or `3`.                                                                                                                                                                                                                                              | Public IPv4 Addresses                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **Link-Local Unicast** | `fe80::/10`                     | Spans a single subnet (they are not forwarded by routers). Nodes on the same link are referred to as neighbors. Each IPv6 interface **must always** be configured with a link-local address. Equivalent to IPv4 APIPA (`169.254.0.0/16`).                                                                                                                                                                                                | APIPA (`169.254.0.0/16`)                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| **Multicast** | `ff00::/8` (`ff02::/16` for link-local multicast) | Used for one-to-many communication within an internetwork or link-local scope. Replaces broadcast addressing (which is not implemented in IPv6).                                                                                                                                                                                                                                                                                         | IPv4 Multicast (e.g., `224.0.0.0/4`)                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **Solicited-Node Multicast** | `ff02::1:ff00:0/104`            | A special multicast address automatically created for each unicast or anycast address assigned to an interface. Used for Neighbor Discovery (NDP) to perform address resolution and duplicate address detection without broadcasting.                                                                                                                                                                                                    | Part of ARP functionality (but without broadcasts)                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **Unspecified Address** | `::/128` (`0:0:0:0:0:0:0:0`)     | Represents the absence of an address. Used as a source address when a host has not yet obtained a valid address (e.g., during DAD).                                                                                                                                                                                                                                                                                               | `0.0.0.0`                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| **Unique-Local Address** | `fc00::/7` to `fd00::/7`        | Similar to IPv4 private addresses (`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`). Used for private networks that are not meant to be routed on the internet. Has a larger random component than site-local addresses (now deprecated).                                                                                                                                                                                          | Private IPv4 Addresses                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| **Loopback Address** | `::1/128`                       | Used for testing the loopback TCP/IP stack on the local host.                                                                                                                                                                                                                                                                                                                                                                       | `127.0.0.1`                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **All-Nodes Multicast** | `ff02::1`                       | A link-local scope multicast address for all IPv6 devices on a local link. Equivalent to IPv4 limited broadcast.                                                                                                                                                                                                                                                                                                                            | `255.255.255.255` (limited broadcast)                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **All-Routers Multicast** | `ff02::2`                       | A link-local scope multicast address for all IPv6 routers on a local link. Used by hosts to find routers via Router Solicitation messages.                                                                                                                                                                                                                                                                                               | Part of router discovery functionality                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **DHCP Multicast** | `ff02::1:2`                     | Used by DHCPv6 clients to discover DHCPv6 servers.                                                                                                                                                                                                                                                                                                                                                                                  | Part of DHCP discovery functionality                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

#### IPV6 Vs IPV4

IPv6 provides other technical benefits in addition to a larger addressing space. In particular, it permits hierarchical address allocation methods that facilitate route aggregation across the Internet, and thus limit the expansion of routing tables. The use of multicast addressing is expanded and simplified, and provides additional optimization for the delivery of services. Device mobility, security, and configuration aspects have been considered in the design of the protocol. 
It simplifies aspects of address configuration, network renumbering, and router announcements when changing network connectivity providers. It simplifies processing of packets in routers by placing the responsibility for packet fragmentation into the end points. The IPv6 subnet size is standardized by fixing the size of the host identifier portion of an address to 64 bits.

The addressing architecture of IPv6 allows three different types of transmission: unicast, anycast and multicast. IPv6 is not foreseen to supplant IPv4 instantaneously. Both protocols will continue to operate simultaneously for some time. Therefore, IPv6 transition mechanisms are needed to enable IPv6 hosts to reach IPv4 services and to allow isolated IPv6 hosts and networks to reach each other over IPv4 infrastructure.
 
On the Internet, data is transmitted in the form of network packets. IPv6 specifies a new packet format, designed to minimize packet header processing by routers. Because the headers of IPv4 packets and IPv6 packets are significantly different, the two protocols are not interoperable. IPv6 does not implement traditional IP broadcast, i.e. the transmission of a packet to all hosts on the attached link using a special broadcast address, and therefore does not define broadcast addresses. The results are achieved using multicasting,  because it does not support the broadcast addressing method, on which the functionality of the Address Resolution Protocol (ARP) in IPv4 is based. IPv6 implements the Neighbor Discovery Protocol (NDP) in the link layer, which relies on ICMPv6 and multicast transmission

Both IPv4 and IPv6 addresses are ultimately represented in binary, although you'll commonly see them in decimal (IPv4) or hexadecimal (IPv6) format for convenience. Each segment (octet in IPv4, hextet in IPv6) ultimately represents 8 bits of binary.

---


# CHAPTER 4: TRANSPORT LAYER

### Transport Layer Overview
* **Function:** Responsible for end-to-end communication between applications on different hosts. It segments data from the application layer and reassembles it at the destination.
* **Key Services:**
    * **Segmentation and Reassembly:** Breaks application data into smaller units (segments/datagrams) for transmission and reconstructs them at the receiver.
    * **Multiplexing and Demultiplexing:** Allows multiple applications to share a single network connection by using port numbers.
    * **Error Checking:** Detects errors in transmission.
    * **Connection Management:** (For TCP) Establishes, maintains, and terminates connections.
    * **Flow Control:** Manages the rate of data transmission between sender and receiver.
    * **Congestion Control:** Manages network traffic to avoid overloading the network.
* **PDU:** Segments (TCP) or Datagrams (UDP).
* **Core Protocols:** TCP and UDP.


### Transmission Control Protocol (TCP)

The Transmission Control Protocol provides a communication service at an intermediate level between an Application program & the Internet Protocol. It provides host-to-host connectivity at the transport layer of the Internet model. At the transport layer, TCP handles all handshaking and transmission details and presents an abstraction of the network connection to the application typically through a network socket interface.

At the lower levels of the protocol stack(I.e IP), due to network congestion, traffic load balancing, or unpredictable network behaviour, IP packets may be lost, duplicated, or delivered out of order. TCP detects these problems, requests re-transmission of lost data, rearranges out-of-order data and even helps minimize network congestion to reduce the occurrence of the other problems. If the data still remains undelivered, the source is notified of this failure. Once the TCP receiver has reassembled the sequence of octets originally transmitted, it passes them to the receiving application. Thus, TCP abstracts the application's communication from the underlying networking details.

TCP is optimized for accurate delivery rather than timely delivery and can incur relatively long delays (on the order of seconds) while waiting for out-of-order messages or re-transmissions of lost messages. 
TCP is a reliable stream delivery service which guarantees that all bytes received will be identical and in the same order as those sent. Since packet transfer by many networks is not reliable, TCP achieves reliability using a technique known as Selective Acknowledgement(SACK) with Re-Transmission or Duplicate Cumulative Acknowledgements (DupAcks) with Retransmission Timeout(RTO). This requires the receiver to respond with an acknowledgement message as it receives the data. The sender keeps a record of each packet it sends and maintains a timer from when the packet was sent. The sender re-transmits a packet if the timer expires before receiving the acknowledgement. The timer is needed in case a packet gets lost or corrupted.

While IP handles actual delivery of the data, TCP keeps track of segments - the individual units of data transmission that a Data Stream is divided into for efficient routing through the network. Processes transmit data by calling on the TCP and passing buffers/streams of data as arguments. The TCP packages the data from these buffers into segments and calls on the internet module [e.g. IP] to transmit each segment to the destination TCP. For example, when an HTML file is sent from a web server, the TCP software layer of that server divides the file into segments and forwards them individually to the internet layer in the network stack. The internet layer software(IP) encapsulates each TCP segment into an IP packet by adding a header that includes (among other data) the destination IP address. When the client program on the destination computer receives them, the TCP software in the transport layer re-assembles the segments and ensures they are correctly ordered and error-free as it streams the file contents to the receiving application. 

Transmission Control Protocol is a connection-oriented protocol and requires handshaking to set up end-to-end communications. Once a connection is set up, user data may be sent bi-directionally over the connection. 	User Datagram Protocol is a simpler message-based connectionless protocol. Connectionless protocols do not set up a dedicated end-to-end connection. Communication is achieved by transmitting information in one direction from source to destination without verifying the readiness or state of the receiver. 
Reliable – TCP manages message acknowledgment, retransmission and timeouts. Multiple attempts to deliver the message are made. If data gets lost along the way, data will be re-sent. In TCP, there's either no missing data, or, in case of multiple timeouts, the connection is dropped.	Unreliable – When a UDP message is sent, it cannot be known if it will reach its destination; it could get lost along the way. There is no concept of acknowledgment, retransmission, or timeout.
Ordered – If two messages are sent over a connection in sequence, the first message will reach the receiving application first. When data segments arrive in the wrong order, TCP buffers the out-of-order data until all data can be properly re-ordered and delivered to the application.	Not ordered – If two messages are sent to the same recipient, the order in which they arrive cannot be guaranteed.
Heavyweight – TCP requires three packets to set up a socket connection, before any user data can be sent. TCP handles reliability and congestion control.	Lightweight – There is no ordering of messages, no tracking connections, etc. It is a very simple transport layer designed on top of IP.
Streaming – Data is read as a byte stream, no distinguishing indications are transmitted to signal message (segment) boundaries.	Datagrams – Packets are sent individually and are checked for integrity on arrival. Packets have definite boundaries which are honored upon receipt; a read operation at the receiver socket will yield an entire message as it was originally sent.
TCP is used extensively by many internet applications, including the World Wide Web (WWW),HTTP email, File Transfer Protocol, Secure Shell, peer-to-peer file sharing, and streaming media.	No congestion control – UDP itself does not avoid congestion. Congestion control measures must be implemented at the application level or in the network.
	Broadcasts – being connectionless, UDP can broadcast - sent packets can be addressed to be receivable by all devices on the subnet.
	Multicast – a multicast mode of operation is supported whereby a single datagram packet can be automatically routed without duplication to a group of subscribers.

![TCP](images/TCP-Header.png)

#### TCP Segment Structure and Header Fields

The use of sequencing, acknowledgments, and retransmission means that TCP requires numerous header fields to keep track and maintain state information. A TCP segment encapsulates application layer data.

| Field Name      | Size (Bytes) | Description                                                                                                                                              |
| :-------------- | :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Source Port** | 2            | Identifies the sending application.                                                                                                                      |
| **Destination Port** | 2            | Identifies the receiving application.                                                                                                                    |
| **Sequence Number (Seq #)** | 4            | The identification of the first byte of the current segment in the data stream. Allows the receiver to reassemble messages correctly and deal with out-of-order packets. |
| **Acknowledgment Number (Ack #)** | 4            | The Sequence Number of the next segment expected from the other host (i.e., the Sequence Number of the last segment received +1). Lack of acknowledgment (due to delays) or Negative Acknowledgment (NACK for lost/damaged packets) forces retransmission. |
| **Data Offset** | 4 bits       | Specifies the size of the TCP header.                                                                                                                    |
| **Reserved** | 6 bits       | Reserved for future use.                                                                                                                                 |
| **Flags** | 1 byte       | Contains control bits such as **ACK** (Acknowledgment), **SYN** (Synchronize sequence numbers - for connection initiation), **FIN** (Finish - for connection termination), **RST** (Reset - for abrupt termination). |
| **Window** | 2            | The amount of data the host is willing to receive before sending another acknowledgment. This is a key part of TCP's **flow control mechanism**.               |
| **Checksum** | 2            | Ensures the validity of the segment. Calculated on the value of not only the TCP header and payload but also part of the IP header.                           |
| **Urgent Pointer** | 2            | If urgent data is being sent, this specifies the end of that urgent data within the segment.                                                             |
| **Options** | Variable     | Allows further connection parameters to be configured. The most important is **Maximum Segment Size (MSS)**, which allows the host to specify how large the segments it receives should be, minimizing fragmentation as they are transported over data link frames. |

#### TCP Handshake and Teardown

A TCP connection is established using a **Three-Way Handshake**:
* **Function:** The process used by TCP to establish a reliable connection between two hosts before data transfer.
* **Steps:**
    1.  **SYN (Synchronize Sequence Numbers):** Client sends a SYN segment to the server, initiating the connection and proposing its initial sequence number.
    2.  **SYN-ACK (Synchronize-Acknowledgement):** Server receives SYN, responds with a SYN-ACK segment, acknowledging the client's SYN and proposing its own initial sequence number.
    3.  **ACK (Acknowledgement):** Client receives SYN-ACK, responds with an ACK segment, acknowledging the server's SYN.
* **Result:** A full-duplex, reliable connection is established, and data transfer can begin.

A host can end a session gracefully using a **Four-Way Handshake** (involving FIN and ACK flags from both sides). A host can also end a session abruptly using an **RST (Reset)** flag, typically indicating an error, failure, or suspicious activity. The server expects regular acknowledgments for segments it sends. If a timeout occurs without an acknowledgment, it means the information didn't arrive, and the server automatically resends that segment. This overhead makes TCP suitable when reliability and integrity are paramount, even if it results in slightly slower transmission.


### User Datagram Protocol (UDP)

User/Unreliable Datagram Protocol
UDP uses a simple connectionless communication model with a minimum of protocol mechanisms where Prior communications are not required in order to set up communication channels or data paths.
UDP provides checksums for data integrity, and port# for addressing different functions at the source and destination of the datagram. It has no handshaking dialogues, and thus exposes the user's program to any unreliability(no Assurance) of the underlying network; there is no guarantee of delivery, ordering, or duplicate protection. 
While these are certainly drawbacks for some types of applications, other applications that want to prioritize transmission speed and efficiency over security and reliability may leverage UDP. UDP is suitable for purposes where error checking and correction are either not necessary or are performed in the application; UDP avoids the overhead of such processing in the protocol stack. Time-sensitive applications often use UDP because dropping packets is preferable to waiting for packets delayed due to retransmission, which may not be an option in a real-time system In order to remedy the security issue, encryption protocols are commonly used. Lacking reliability, UDP applications must be willing to accept some packet loss, reordering, errors or duplication. If using UDP, the end user applications must provide any necessary handshaking such as real time confirmation that the message has been received.
A number of UDP's attributes make it especially suited for certain applications.
✔️It is transaction-oriented, suitable for simple query-response protocols where queries must be fast and only consist of a single request followed by a single reply packet I.e Domain Name System or the Network Time Protocol.
✔️It provides datagrams, suitable for modeling other protocols such as IP tunneling or remote procedure call and the Network File System.
✔️ It is simple, suitable for bootstrapping or other purposes without a full protocol stack, such as the DHCP and Trivial File Transfer Protocol.
✔️It is stateless, suitable for very large numbers of clients, such as in streaming media applications such as IPTV.
✔️The lack of retransmission delays makes it suitable for real-time applications such as Voice over IP, online games, and many protocols using Real Time Streaming Protocol.
✔️Because it supports multicast, it is suitable for broadcast information such as in many kinds of service discovery and shared information such as Precision Time Protocol and Routing Information Protocol.

Unlike TCP, **UDP** is a **Connectionless, Non-Reliable** method of communication with no acknowledgments or built-in flow control.

* There is no guarantee on datagram delivery, and no mechanism for retransmitting lost packets.
* When an application uses UDP, it must implement its own reliability mechanisms in the application layer headers or software logic if required.
* **Multicast** and **Broadcast** traffic are supported by UDP.
* It is typically used for applications that transport time-sensitive data but do not require complete reliability (e.g., video or voice streaming). Using smaller packets for transmission means that if a few are lost or arrive out of order, they manifest as minor glitches in playback quality. The reduced overhead means that overall delivery is faster.

![UDP](images/UDP-Header.png)

#### UDP Datagram Structure

A UDP header is only 8 bytes, consisting of:

* **Source Port (2 bytes)**
* **Destination Port (2 bytes)**
* **Message Length (2 bytes)**: The total length of the UDP header and data.
* **Checksum (2 bytes)**: Ensures the validity of the datagram.

The unit of data packets transferred between hosts using this protocol is referred to as a **Datagram**. No prior communications are required to set up communication channels or data paths, which is characteristic of **Connectionless** protocols (no handshake dialogue). This design exposes the user's program to the unreliability of the underlying network.


### Transport Layer Security (TLS)

**TLS (Transport Layer Security)** is the successor to the deprecated Secure Sockets Layer (SSL). It is a cryptographic protocol designed to provide communication security over computer networks. TLS runs in the **Application Layer** of the Internet protocol suite. It is composed of two layers: the **TLS Record Protocol** and the **TLS Handshake Protocol**.
*Transport Layer Security*
TLS is a widely adopted cryptographic security protocol designed to facilitate secure data transmission via encryption. TLS evolved out of the encryption protocol known as SSL (Secure Sockets Layer), which has since been deprecated in favor of TLS. While these two protocols are different, the terms are sometimes used interchangeably. Using TLS with HTTP will allow you to use HTTPS (Hypertext Transfer Protocol Secure), which helps denote the presence of the extra security.
Once the client and server have agreed to use TLS, they negotiate a stateful connection by using a handshaking procedure. The protocols use a handshake with an Asymmetric Encryption cipher (Initial Handshake/Hello Phase Cipher Suites) to establish not only cipher settings but also a session-specific shared key with which further communication is encrypted using a Symmetric cipher. During this handshake, the client and server agree on various parameters used to establish the connection's security:

- The handshake begins when a client connects to a TLS-enabled server requesting a secure connection and the client presents a list of supported cipher suites (ciphers and hash functions). From this list, the server picks a cipher and hash function that it also supports and notifies the client of the decision.
- The server usually then provides identification in the form of a digital certificate. The certificate contains the server name, the trusted certificate authority (CA) that vouches for the authenticity of the certificate, and the server's public encryption key. The client confirms the validity of the certificate before proceeding.
- To generate the session keys used for the secure connection, the client either:
i. Encrypts a random number (PreMasterSecret) with the server's public key and sends the result to the server (which only the server should be able to decrypt with its private key); both parties then use the random number to generate a unique session key for subsequent encryption and decryption of data during the session
ii. Uses Diffie–Hellman key exchange to securely generate a random and unique session key for encryption and decryption that has the additional property of forward secrecy: if the server's private key is disclosed in future, it cannot be used to decrypt the current session, even if the session is intercepted and recorded by a third party.
In Both Cases >> The client uses the server’s public key to encrypt the symmetric key and send it securely to the server, and the server uses its private key to decrypt it. Anyone can encrypt using the public key, but only the server can decrypt using the private key
This concludes the handshake and begins the secured connection, which is encrypted and decrypted with the session key Symmetrically until the connection closes. If any one of the above steps fails, then the TLS handshake fails and the connection is not created. When secured by TLS, connections between a client (e.g., a web browser) and a server (e.g., wikipedia.org) should have one or more of the following properties:
- The connection is private (or secure) because a symmetric-key algorithm is used to encrypt the data transmitted. The keys for this symmetric encryption are generated uniquely for each connection and are based on a shared secret that was negotiated at the start of the session. The server and client negotiate the details of which encryption algorithm and cryptographic keys to use before the first byte of data is transmitted (see below). The negotiation of a shared secret is both secure (the negotiated secret is unavailable to eavesdroppers and cannot be obtained, even by an attacker who places themself in the middle of the connection) and reliable (no attacker can modify the communications during the negotiation without being detected).
- The identity of the communicating parties can be authenticated using public-key cryptography. This authentication is required for the server and optional for the client.
- The connection is reliable because each message transmitted includes a message integrity check using a message authentication code to prevent undetected loss or alteration of the data during transmission.

In addition to the above, careful configuration of TLS can provide additional privacy-related properties such as forward secrecy, ensuring that any future disclosure of encryption keys cannot be used to decrypt any TLS communications recorded in the past.
TLS supports many different methods for exchanging keys, encrypting data, and authenticating message integrity. As a result, secure configuration of TLS involves many configurable parameters, and not all choices provide all of the privacy-related properties described in the list above (see the tables below § Key exchange, § Cipher security, and § Data integrity).
Attempts have been made to subvert aspects of the communications security that TLS seeks to provide, and the protocol has been revised several times to address these security threats. Developers of web browsers have repeatedly revised their products to defend against potential security weaknesses after these were discovered (see TLS/SSL support history of web browsers). 
*Forward Secrecy is a property of cryptographic systems which ensures that a “session key derived from a set of public and private keys” will not be compromised if one of the private keys is compromised in the future, ensuring that any future disclosure of encryption keys cannot be used to decrypt any TLS communications recorded in the past.
*A digital certificate certifies the ownership of a public key by the named subject of the certificate, and indicates certain expected usages of that key. This allows others (relying parties) to rely upon signatures or on assertions made by the private key that corresponds to the certified public key. Keystores and trust stores can be in various formats, such as .pem, .crt, .pfx, and .jks.
*Certificate authority TLS typically relies on a set of trusted third-party certificate authorities to establish the authenticity of certificates. Trust is usually anchored in a list of certificates distributed with user agent software. and can be modified by the relying party. 
*TLS interception (or HTTPS interception if applied particularly to that protocol) is the practice of intercepting an encrypted data stream in order to decrypt it, read and possibly manipulate it, and then re-encrypt it and send the data on its way again. This is done by way of a "transparent proxy": the interception software terminates the incoming TLS connection, inspects the HTTP plaintext, and then creates a new TLS connection to the destination


#### TLS Handshake Process

Clients request that a server sets up a TLS connection, achieved either by:
* Using HTTP port **443** (for encrypted HTTPS traffic).
* Protocol-specific negotiation (e.g., `STARTTLS` command) to switch a connection from unencrypted (e.g., port 80 for HTTP) to encrypted.

![TLS](images/TLS-handshake-protocol.png)

The TLS Handshake is a complex process but can be summarized:

1.  **Client Hello:** Client requests a secure connection and presents a list of supported **Cipher Suites** (combinations of ciphers and hash functions).
2.  **Server Hello:** Server picks a cipher and hash function it supports from the client's list and notifies the client.
3.  **Server Certificate:** Server provides its **Digital Certificate**, containing the server name, Certificate Authority (CA), and its Public Encryption Key.
4.  **Client Certificate Verification:** Client confirms the validity of the certificate before proceeding (e.g., checking trust chain, expiration).
5.  **Session Key Generation:** To generate **Session Keys** (symmetric keys used for the secure connection):
    * **Method 1 (RSA Key Exchange - older):** Client encrypts a random number (pre-master secret) with the server's public key and sends the result to the server. The server decrypts it with its private key. Both parties then use this random number to generate a unique symmetric session key for subsequent encryption and decryption of data during the session.
    * **Method 2 (Diffie-Hellman Key Exchange - preferred for Forward Secrecy):** Client and server use a Diffie-Hellman Key Exchange to securely generate a random and unique session key. This method has the additional property of **Forward Secrecy**, meaning if the server's private key is disclosed in the future, it cannot be used to decrypt current or past sessions.
6. This concludes the handshake, and the secure connection begins, encrypted with the session key until the connection closes.

#### Benefits of a Secure TLS Connection

When secure via TLS, connections between client and server offer:

1.  **Privacy (Confidentiality):** The connection is private via a symmetric key algorithm used for data encryption. The negotiation of a shared secret is both secure and reliable, as details (encryption algorithm and crypto keys) are negotiated before the first byte of data is transmitted.
2.  **Authentication:** The identity of the communicating parties can be authenticated using public-key cryptography. This is typically required by the server (client authentication is optional).
3.  **Reliability (Integrity):** Each transmitted message includes an "integrity check" using a Message Authentication Code (MAC) to prevent data loss, undetected alteration, or tampering during transmission.


### Internet Protocol Security (IPsec)

Internet Protocol Security(IPsec) is a suite of protocols defined by RFC 4301, "Security Architecture for the Internet Protocol" for securing IP communications by authenticating, encapsulating & encrypting each IP packet in a data stream. Which has found widespread use in securing virtual private networks. IPsec includes protocols for establishing mutual authentication between agents at the beginning of a session and negotiation of cryptographic keys to use during the session. IPsec can protect data flows between a pair of hosts (host-to-host), between a pair of security gateways (network-to-network), or between a security gateway and a host (network-to-host).
* **Function:** A suite of protocols used to secure IP communications by authenticating and encrypting each IP packet in a data stream. It operates at the Network Layer (Layer 3) of the OSI model.
* **Key Services Provided:**
    * **Confidentiality (Encryption):** Protects data from eavesdropping using encryption algorithms.
    * **Data Integrity:** Ensures that data has not been tampered with in transit using hashing algorithms.
    * **Authentication:** Verifies the identity of the sender, preventing spoofing.
    * **Anti-Replay Protection:** Prevents attackers from retransmitting captured packets.
* **Components/Protocols:**
    * **Authentication Header (AH):** Provides data integrity, data authentication, and anti-replay protection. It does *not* provide confidentiality (encryption).
    * **Encapsulating Security Payload (ESP):** Provides confidentiality (encryption), data integrity, data authentication, and anti-replay protection. It's the most commonly used IPsec protocol.
    * **Internet Key Exchange (IKE):** A protocol used to set up a Security Association (SA) in IPsec. It authenticates peers and securely establishes shared secret keys. IKE operates in two phases (Phase 1 for IKE SA, Phase 2 for IPsec SA).

IPsec can be used to secure IPv4 and/or IPv6 communications on local networks and for remote access protocols. Each host that uses IPsec must be assigned an IPsec policy. An IPsec policy sets the authentication mechanism and also the protocols and mode for the connection (Transport / Tunnel). Hosts must be able to match at least one security method for a connection to be established.

#### IPsec Modes of Operation
The IPsec protocols AH and ESP can be implemented in a host-to-host transport mode, as well as in a network tunneling mode.
In computer networks, a tunneling protocol is a communication protocol which allows for the movement of data from one network to another, by exploiting encapsulation. It involves allowing private network communications to be sent across a public network (such as the Internet) through a process called encapsulation. The tunneling protocol works by using the data portion of a packet (the payload) to carry the packets that actually provide the service. Tunneling uses a layered protocol model such as those of the OSI or TCP/IP protocol suite, but usually violates the layering when using the payload to carry a service not normally provided by the network. Typically, the delivery protocol operates at an equal or higher level in the layered model than the payload protocol. According to the definition of tunneling, one can use it to access resources that are available only to internal networks. To create/facilitate such tunnels, an appropriate application should be used. The most known one is SSH 

* **Transport Mode:**
    * **Function:** Encrypts or authenticates only the IP payload (the data portion of the packet). The original IP header remains intact.
    * **Use Case:** Primarily used for host-to-host or end-to-end communication, typically when traffic is already originating or terminating on the IPsec peer (e.g., a client securely communicating with a server).
    * **Header:** Adds IPsec headers (AH or ESP) between the original IP header and the transport layer header.


* **Tunnel Mode:**
    * **Function:** Encrypts or authenticates the *entire* original IP packet (header + payload). A *new* IP header is then added outside the encrypted original packet.
    * **Use Case:** Most commonly used for network-to-network (e.g., site-to-site VPNs) or host-to-network communication (e.g., remote access VPNs).
    * **Header:** Creates a new outer IP header for routing through the unsecured network, and the original IP packet becomes the payload of the new IP packet.


![IPSec](images/IPSec.png)



#### TUNNELING VS ENCAPSULATION
Encapsulation is a generic networking concept that involves wrapping one protocol's payload inside another so it can be transmitted across a network. It's used for routing and transporting data, but not by default for security or encryption. Examples include an IPv6 packet over an IPv4 network (6 to 4 Tunneling and Encapsulation), and Generic Routing Encapsulation (GRE) which wraps Layer 3 traffic inside IP packets with no mechanism for authentication.
Tunneling is a more specific use case of Encapsulation, which refers to Encapsulating and Routing packets through a "TUNNEL". IPsec VPN tunnels traffic with encryption, while GRE tunnels traffic without encryption. All Tunneling involves Encapsulation, but not all Encapsulation is Tunneling (e.g., MPLS and GRE). Also, not all tunnels are Encrypted (e.g., L2TP and GRE). Tunneling may or may not imply encryption.
IPsec doesn't support Broadcast & Multicast traffic, only Unicast. To SUMMARIZE:
* **Encapsulation:** The process of placing one packet (or frame) inside another. This involves adding a new header and/or trailer to an existing packet, treating the original packet as data.
    * **Reason:** Used to add new functionality (like security or routing across a different network type) or to prepare data for transmission at a lower layer.
* **Tunneling:** A networking technique that encapsulates an entire network protocol (the "payload" protocol) within another network protocol (the "carrier" protocol). This creates a "tunnel" through an intermediate network.
    * **Process:** Data from one network is encapsulated into another protocol's packet headers, allowing it to traverse an incompatible network before being decapsulated at the other end.
    * **Analogy:** Like putting a letter (your original packet) inside an envelope (the carrier protocol's header) to send it through a mail system (the intermediate network).
    * **Common Use:** Essential for VPNs, allowing secure or private communication over a public, unsecured network like the internet.


#### 1. Authentication Header (AH)

* **Header Inclusion:** `IP Header | AH Header | TCP/UDP Header | Payload`
* This protocol performs a cryptographic hash on the **whole IP packet**, including the IP Header, plus a shared secret key (known only to the communicating hosts).
* It adds this calculated hash in its header as an **Integrity Check Value (ICV)**. The recipient performs the same function on the packet + key; if it derives the same value, it authenticates that the packet has not been modified.
* **No Confidentiality:** The payload is **not encrypted**, so this protocol does not provide confidentiality.
* **NAT Incompatibility:** The inclusion of IP header fields in the ICV means that the check will fail across **NAT Gateways**, where the IP address is rewritten, making AH unsuitable for use with NAT.

#### 2. Encapsulating Security Payload (ESP)

* **Header Inclusion:** `IP Header | ESP Header | TCP/UDP Header | Payload | ESP Trailer | ESP Authentication Data`
* ESP provides **Confidentiality AND/OR Authentication & Integrity**.
* It can be used to encrypt the packet rather than simply calculating a hash.
* ESP attaches three fields to the packet: a header, a trailer (providing padding for the crypto function), and an ICV.
* **NAT Compatibility:** Unlike AH, ESP **excludes the IP header** when calculating the integrity check, making it compatible with NAT.
* **Encryption and Hashing:** With ESP, algorithms for both confidentiality (symmetric cipher) and authentication/integrity (hash function) are usually applied together. However, it's possible to use one or the other.
* **IP Protocol Numbers:** IPsec makes use of **Extension Headers in IPv6**, while in IPv4, ESP and AH are allocated new IP protocol numbers (50 & 51).

#### Internet Key Exchange (IKE)

IPsec's encrypting and hashing functions depend on shared secrets. The secrets must be communicated to both hosts, and the hosts must confirm one another's identity (**mutual authentication**). The **Internet Key Exchange (IKE)** protocol handles authentication and key exchange, establishing the Security Association (SA). Most IPsec implementations consist of an IKE daemon that runs in user space and an IPsec stack in the kernel that processes the actual Internet Protocol packets.

#### Tunneling Protocols

Tunneling involves encapsulating one protocol's packets within another protocol's packets to carry them across an incompatible network or to provide secure, logical links.

##### 1. Point-to-Point Protocol (PPP)

* PPP is an **encapsulation protocol** that works at the **Data Link Layer (Layer 2)**.
* It is used to encapsulate IP packets for transmission over serial digital lines.
* PPP has **no security mechanism**, so it must be used with other protocols to provide a secure tunnel.

##### 2. Generic Routing Encapsulation (GRE)

* **GRE** works at **Layer 3**.
* A GRE packet can encapsulate an ordinary Layer 3 IP packet as its payload. The "outer" GRE packet is assigned protocol number 47 and has its own IP Source/Destination Header Address fields.
* PPP (or another Layer 2 protocol) then encapsulates this outer GRE packet at Layer 2 for transmission (e.g., tunnelling to the next hop router).
* Each intermediate router inspects only the outer GRE header to determine forwarding. At the final destination, the receiving router de-encapsulates the GRE packet to extract the inner IP payload and forwards that inner packet to its true destination on the internal network.
* GRE does not have mechanisms for authenticating users/devices and is therefore often used with other protocols like IPsec to provide security.

##### 3. TLS over TCP / DTLS over UDP

* **TLS (Transport Layer Security)** over TCP or **DTLS (Datagram TLS)** over UDP can be used to encapsulate frames or IP packets.
* The main drawback is that these protocols already operate at the **Session Layer** (or Application layer, depending on model interpretation), meaning the headers from the inner and outer packets add up to a significant overhead compared to lower-layer tunneling.


### Virtual Private Networks (VPNs)

* **Definition:** A technology that creates a **secure, encrypted connection** (a "tunnel") over a less secure network, such as the internet. It extends a private network across a public network.
* **Core Purpose:** To provide secure remote access, site-to-site connectivity, and protect online privacy and anonymity.
* **Key Services:**
    * **Confidentiality:** Achieved through encryption (e.g., AES, 3DES).
    * **Data Integrity:** Ensured through hashing (e.g., SHA, MD5).
    * **Authentication:** Verifies the identity of users or devices (e.g., pre-shared keys, certificates).
    * **Secure Tunneling:** Encapsulates private data within a public network.

#### 1. Client-to-Site VPN (Remote Access VPN)

* **Topology:** In this implementation, the VPN client connects over the public network (Internet) to a VPN gateway positioned on the edge of the local network (typically, the VPN access server will be in a screened subnet/DMZ).
* **Use Case:** This is the "telecommuter model," allowing home workers and employees in the field to connect securely to the corporate network.
* **Protocols:** Can be configured using a number of protocols:
    * **SSL/TLS VPN solutions:** Use certificates to establish the secure tunnel.
    * **Secure Socket Tunneling Protocol (SSTP)**
    * **Layer 2 Tunneling Protocol (L2TP)** (often combined with IPsec for security)
* Most solutions require client software to operate (except clientless VPNs) and use Extensible Authentication Protocols (EAP) architecture to authenticate client users and devices.
* **Split Tunneling:** The client accesses the Internet directly using its native IP configuration and DNS servers. Internet-bound traffic does not traverse the VPN tunnel.
* **Full Tunneling:** Internet access is mediated by the corporate network. This will alter the client's IP address and DNS servers and may use a proxy. This offers better security as all traffic is forced through the corporate network's security controls. However, Network Address Translations (NAT) and DNS operations required may cause problems with some websites/cloud services, and more data is channeled over the VPN link, which may exhibit higher latency.

##### Clientless VPNs (HTML5 VPN)

Traditionally, application and client-suite VPNs require a client application that implements the protocols and authentication methods supported by the VPN gateway.
The `canvas` element introduced in HTML5 allows modern browsers to draw and update a desktop with relatively little lag, enabling many browsers to act as "clientless" VPN/RDP clients. Also referred to as an **HTML5 VPN**, this solution uses a protocol called **WebSockets**, which enables bidirectional messages to be sent between the server and client without requiring the overhead of separate HTTP requests.

##### Remote Host Access and Remote Desktop Gateways

Remote host access refers to operating a computer or configuring a network appliance without needing to use a terminal directly connected to it. This can be implemented within a local network or over a public network. (Image Placeholder - Remote Access VPN)

* **Remote Configuration of Network Appliances:** Most network appliances are "headless" (no monitor/keyboard), so remote connections are the only practical configuration option. This type of connection is typically implemented using **Secure Shell (SSH)** or **Telnet** (less secure).
* **Remote Desktop Connections:** Allow an administrator with privileges to configure a server or a user to operate a computer remotely.
    * **Remote Desktop Protocol (RDP)** provides full graphical access.
    * Other protocols can be used for terminal access only (e.g., Telnet, SSH).
* **Remote Desktop Gateways:** Allow user access to networked applications. A gateway can also be used to connect a user to a **Virtual Desktop**, where a client OS and application software are provisioned as a virtual appliance. Alternatively, a remote desktop gateway can function as a form of clientless VPN, where Microsoft RDP can be used to access a physical machine on a network. Several alternatives to RDP exist, such as **VNC (Virtual Network Computing)**.

#### 2. Site-to-Site Virtual Private Networks (VPNs)

* **Topology:** A VPN can also be deployed in a site-to-site model to connect two or more private networks (e.g., a branch office LAN to a head office LAN).
* **Automation:** Instead of a client initiating the VPN connection, site-to-site VPNs are configured to operate automatically. The gateways (e.g., routers or firewalls) exchange security information using whatever protocol the VPN is based on (commonly IPsec with GRE). This establishes a trust relationship between the gateways and sets up a secure connection through which to tunnel data.
* **Transparency to Hosts:** Hosts at each site do not need to be configured with any information about the VPN; the routing infrastructure at each site determines whether to deliver traffic locally or send it over the VPN tunnel.
* **Compulsory Tunnelling:** This is also referred to as "Compulsory Tunnelling." Compulsory tunnels can be in place permanently (static) or dynamically based on the client type or data type.
* **Non-Internet VPNs:** VPNs are not always established over the public Internet. A WAN Service Provider can implement VPNs over its own network (e.g., using VLAN-like technologies or MPLS to isolate customer's traffic from other traffic). This is a common model for site-to-site VPNs, offering private, secure connections without traversing the public Internet.
(Image Placeholder - Site-to-Site VPN)

#####  DYNAMIC MULTIPOINT VPNs (DMVPN)
DMVPN is a Cisco-developed solution that allows Routers to dynamically create a full Mesh of IPsec tunnels without having to manually configure every single tunnel.
DMVPN provides the configuration simplicity of a Hub and Spoke WAN topology (each Spoke Router only needs one tunnel configured) and the efficiency of direct spoke-to-spoke communication (spoke routers can communicate directly without traffic passing through the Hub (VPN HeadEnd)). They communicate between themselves by a temporary encrypted VPN setup between them by the DMVPN. This process also involves the use of Next Hop Resolution Protocol (NHRP) to identify destination addresses and GRE tunnels to encapsulate the encrypted IPsec packets.
DMVPN Configuration Commands
	•	Interface Tunnel 0
	•	tunnel source "Interface"
	•	tunnel Destination "ip-addr"


#### KEY TERMS
❗️Application Programming Interface (API)- A protocol intended to be used as an interface by software components to communicate with each other.
❗️Buffer- A region of a physical memory storage used to temporarily prevent data from continuing while it is being moved from one place to another.
❗️Buffer Underrun- A state occurring when a buffer used to communicate between two devices or processes is fed with data at a lower speed than the data is being read from it.
❗️Checksum- A fixed-size datum computed from an arbitrary block of digital data for the purpose of detecting accidental errors that may have been introduced during its transmission or storage.
❗️Connection Oriented Communication- A data communication mode whereby the devices at the end points use a protocol to establish an end-to-end logical or physical connection before any data may be sent.
❗️Connectionless- A data communication mode in which a message can be sent from one end point to another without prior arrangement.
❗️Data Stream- A sequence of digitally encoded coherent signals (packets of data or data packets) used to transmit or receive information that is in the process of being transmitted.
❗️Datagram- A basic transfer unit associated with a packet-switched network in which the delivery, arrival time, and order of arrival are not guaranteed by the network service.
❗️Deadlock- A situation in which two or more competing actions are each waiting for the other to finish, and thus neither ever does.
❗️Ephemeral Port- A short lived port allocated automatically from a predefined range.
❗️Handshaking- An automated process of negotiation that dynamically sets parameters of a communications channel established between two entities before normal communication over the channel begins.
❗️Latency- A measure of time delay experienced in a system.
❗️Maximum segment size (MSS)- A parameter of the TCP protocol that specifies the largest amount of data that a computer or communications device can receive in a single TCP segment.
❗️Multiplexing- A method by which multiple analog message signals or digital data streams are combined into one signal over a shared medium.
❗️Network Congestion- A data communication situation in which a link or node is carrying so much data that its quality of service deteriorates.
❗️Registered Port- A transport protocol port assigned by the Internet Assigned Numbers Authority (IANA) for use with a certain protocol or application.
❗️Reliability- A reliable protocol is a communication protocol that notifies the sender whether or not the delivery of data to intended recipients was successful with respect to the delivery of data to the intended recipient(s), as opposed to an unreliable protocol, which does not provide notifications to the sender as to the delivery of transmitted data.
❗️Slow start- One of the algorithms that TCP uses to control congestion inside the network, in which the TCP window size is increased each time an acknowledgment is received.
❗️TCP window scale option- An option to increase the TCP receive window size above its maximum value of 65,535 bytes
❗️Ports- A port is a software structure that is identified by the port number, a 16 bit integer value, allowing for port numbers between 0 and 65535. Applications can use datagram sockets to establish host-to-host communications. An application binds a socket to its endpoint of data transmission, which is a combination of an IP address and a port. In this way, UDP provides application multiplexing. Port 0 is reserved, but is a permissible source port value if the sending process does not expect messages in response. 
❗️Packet Retransmission(PAR)- is the resending of packets which have been either damaged or lost. Retransmission is one of the basic mechanisms used by protocols operating over a packet switched computer network to provide reliable communication.
Networks are usually "unreliable", meaning they offer no guarantees that they will not delay, damage, or lose packets, or deliver them out of order. Protocols which provide reliable communication over such networks use a combination of acknowledgments & Retransmission of missing or damaged packets (usually initiated by a time-out), and checksums to provide that reliability. *Positive Acknowledgment ACK *Negative Acknowledgment NACK *Selective Acknowledgments SACK *Cumulative Acknowledgments CACK 
❗️Automatic repeat request (ARQ), also known as automatic repeat query, is an error-control method for data transmission that uses acknowledgements (messages sent by the receiver indicating that it has correctly received a packet) and timeouts (specified periods of time allowed to elapse before an acknowledgment is to be received) to achieve reliable data transmission over an unreliable communication channel. If the sender does not receive an acknowledgment before the timeout, it re-transmits the packet until it receives an acknowledgment or exceeds a predefined number of retransmissions. The ARQ protocol also provides flow control, which may be combined with congestion avoidance. Variations of ARQ protocols include *Stop-and-wait ARQ *Go-Back-N ARQ *Selective Repeat ARQ

---


# CHAPTER 5: APPLICATION LAYER

## Domain Name System (DNS)
* **Function:** A hierarchical and decentralized naming system for computers, services, or any resource connected to the Internet or a private network. It translates human-readable domain names (e.g., `google.com`) into machine-readable IP addresses (e.g., `172.217.160.142`).
* **Core Purpose:** To make the Internet easier to use by eliminating the need to remember numerical IP addresses.
* **Protocol:** Primarily uses **UDP port 53** for standard queries, and **TCP port 53** for zone transfers.

Hosts on The Internet maintains two principal namespaces, the domain name hierarchy and the Internet Protocol (IP) address spaces., which is used for routing and network interface identification. An often-used analogy to explain the Domain Name System is that it serves as the phone book for the Internet by translating human-friendly computer hostnames into IP addresses. For example, the domain name www.example.com translates to the addresses 93.184.216.34 (IPv4) and 2606:2800:220:1:248:1893:25c8:1946 (IPv6). The translation between addresses and domain names is performed by the Domain Name System (DNS), a hierarchical, decentralized, distributed naming system that allows for the subdelegation of namespaces to Internet resources by designating authoritative name servers for each domain, Most prominently, it translates more readily memorized domain names to the numerical IP addresses needed for locating and identifying computer services and devices with the underlying network protocols.  

### DNS Hierarchy and Components
* **DNS Hierarchy:** A tree-like structure that organizes domain names.
    * **Root Servers:** The top of the DNS hierarchy. They know the addresses of the TLD name servers. Represented by a ".".
    * **Top-Level Domain (TLD) Servers:** Handle domains like `.com`, `.org`, `.net`, `.edu`, `.gov`, and country codes like `.uk`, `.de`. They know the addresses of authoritative name servers for second-level domains.
    * **Second-Level Domain (SLD):** The part of the domain name that comes before the TLD (e.g., `google` in `google.com`). These are registered by individuals or organizations.
    * **Authoritative Name Servers:** Hold the actual DNS records (A, AAAA, MX, CNAME, etc.) for a specific domain. They are the ultimate source of truth for a domain.
    * **Host (Subdomain):** Specific hosts or services within a domain (e.g., `www`, `mail`, `ftp` in `www.example.com`).
* **DNS Resolvers (Caching/Recursive Name Servers):**
    * **Function:** Act as intermediaries between clients and authoritative name servers. They receive DNS queries from clients and perform the recursive lookups on their behalf.
    * **Characteristics:** Cache query results to speed up future lookups.

(Image Placeholder - DNS Hierarchy)

The domain name space consists of a tree data structure. Each node or leaf in the tree has a label and zero or more resource records (RR), which hold information associated with the domain name. The domain name itself consists of the label, concatenated with the name of its parent node on the right, separated by a dot.
The tree sub-divides into zones beginning at the root name server zone. A DNS zone may consist of only one domain, or may consist of many domains and sub-domains, depending on the administrative choices of the zone manager. A domain name consists of one or more parts, technically called labels, that are conventionally concatenated, and delimited by dots, such as example.com.
The right-most label conveys Top-Level Domain (TLD) servers; for example, the domain name www.example.com belongs to the top-level domain COM <parent node>.
The hierarchy of domains descends from right to left; each label to the left specifies a subdivision, or subdomain of the domain to the right. As with root name servers, TLD servers keep track of the next level down: Authoritative name servers. When a TLD server receives your request for information, the server passes it down to an appropriate Authoritative name server.
Authoritative name servers are used to store DNS records for domains directly. In other words, every domain in the world will have its DNS records stored on an Authoritative name server somewhere or another; they are the source of the information. When your request reaches the authoritative name server for the domain you're querying, it will send the relevant information back to you, allowing your computer to connect to the IP address behind the domain you requested.

### DNS Query Types
* **Recursive Query:**
    * **Initiator:** Typically a client (stub resolver) to a recursive DNS server.
    * **Process:** The client asks the recursive server to provide the full answer. The recursive server is responsible for resolving the query completely, contacting other servers if necessary, and returning either the IP address or an error message.
* **Iterative Query:**
    * **Initiator:** Typically a recursive DNS server to a root, TLD, or authoritative name server.
    * **Process:** The querying server asks the queried server for the best answer it can provide. If the queried server doesn't have the answer, it responds with a referral (the address of another server higher up or closer to the authoritative server) that might know. The querying server then "iterates" by contacting the referred server.

(Image Placeholder - DNS Query Process)

DNS Resolvers➡️The client side of the DNS is called a DNS resolver. A resolver is responsible for initiating and sequencing the queries that ultimately lead to a full resolution (translation) of the resource sought. DNS resolvers are classified by a variety of query methods, such as recursive, non-recursive, and iterative. A resolution process may use a combination of these methods. DNS protocol transport primarily uses the UDP port 53 to serve requests.  TCP is also used for tasks such as zone transfers. Some resolver implementations use TCP for all queries. 
Record Caching➡️A standard practice in implementing name resolution in applications is to reduce the load on the Domain Name System servers by caching results locally, or in intermediate resolver hosts. Results obtained from a DNS request are always associated with the time to live (TTL), an expiration time after which the results must be discarded or refreshed.
Reverse Lookup➡️A reverse DNS lookup is a query of the DNS for domain names when the IP address is known. Multiple domain names may be associated with an IP address. The DNS stores IP addresses in the form of domain names as specially formatted names in pointer (PTR) records within the infrastructure top-level domain arpa. For IPv4, the domain is in-addr.arpa. For IPv6, the reverse lookup domain is ip6.arpa. The IP address is represented as a name in reverse-ordered octet representation for IPv4, and reverse-ordered nibble representation for IPv6. 
DNS message format➡️The DNS protocol uses two types of DNS messages, Queries and Replies; both have the same format. Each message consists of a Header + 4 sections: Question, Answer, Authority, & an additional space. A header field controls the content of these 4 sections.
The Header section consists of the following field: Identification, Flags, Number of questions, Number of answers, Number of authority resource records (RRs), and Number of additional RRs. Each field is 16 bits long, and appears in the order given. The identification field is used to match responses with queries.
DNS over HTTPS (DoH) is a protocol for performing remote Domain Name System (DNS) resolution via the HTTPS protocol. A goal of the method is to increase user privacy and security by preventing eavesdropping and manipulation of DNS data by man-in-the-middle attacks[1] by using the HTTPS protocol to encrypt the data between the DoH client and the DoH-based DNS resolver.
DNS over TLS (DoT) is a network security protocol for encrypting and wrapping Domain Name System (DNS) queries and answers via the Transport Layer Security (TLS) protocol. The goal of the method is to increase user privacy and security by preventing eavesdropping and manipulation of DNS data via man-in-the-middle attacks. 
While DNS-over-TLS is applicable to any DNS transaction, it was first standardized for use between stub or forwarding resolvers and recursive resolvers, in RFC 7858

### Host Names and Fully Qualified Domain Names (FQDN)

A **Host-Name** is assigned to a computer by an administrator, usually at the time of OS installation. The host name needs to be unique on the local network.

A **Fully Qualified Domain Name (FQDN)** is used to provide a unique identity for a host belonging to a particular Internetwork, to avoid the possibility of duplicate host names on the Internet.

**FQDN Structure:**
`MY.HOST.Domain.TLD` (e.g., `www.example.com`)
* `MY.HOST`: Host Name (unique within its domain)
* `Domain`: Second-Level Domain Name (unique within a TLD)
* `TLD`: Top-Level Domain (e.g., `.com`, `.org`, `.net`, `.gov`)

Numerous hosts may exist within the same Domain and TLD. The "root" (represented by a dot `.`) is at the end of the FQDN but is usually omitted in most cases.

A Domain Name is unique within a TLD. Once registered, it cannot be used by another organization. However, the same Domain Name may be registered within different TLDs (e.g., `example.com` and `example.org`).

**FQDN Rules:**
FQDNs must follow certain rules:
1.  **Unique Host Name:** The host name must be unique within its domain.
2.  **Case-Insensitivity:** DNS labels are not case-sensitive.
3.  **Length:** The total length of an FQDN cannot exceed 253 characters. Each label (part of the name divided by a period) can be no more than 63 characters (excluding periods).
4.  **Characters:** A DNS label should use letters, digits, and hyphen characters only.
5.  **Start Character:** A label should not start with a hyphen, punctuation, or forward slash character.


#### Domain Name System: Hierarchy and Management

The **Domain Name System (DNS)** is a global hierarchy of distributed name server databases that contain information on domains and hosts within those domains.

At the top of the DNS Hierarchy is the **Root**, which is represented by the null label (just a period `.`). There are 13 root name servers (A-M).

Below the root are the **Top-Level Domains (TLDs)**. These include:
* **Generic TLDs (gTLDs):** Most prevalent gTLDs include `.com`, `.org`, `.net`, `.biz`, `.gov`. ICANN (Internet Corporation for Assigned Names and Numbers) manages these generic TLDs.
* **Country Code TLDs (ccTLDs):** Such as `.uk`, `.ca`, `.au`. These are generally managed by an organization appointed by the relevant government.

The Root DNS Servers have complete information about the TLD Servers. In turn, the TLD Servers have information relating to servers for the second-level domains. No single name server has complete information about all domains. Records within the DNS tell them where an **Authoritative Name Server** for missing information can be found.

An FQDN reflects this hierarchy, from most specific on the left (the host's resource record with its Name:IP address mapping) to the least specific on the right (the TLD and root).


#### Name Resolution Using Domain Name System Servers

The process of translating an FQDN into an IP address is known as **Name Resolution**.

#### Iterative vs. Recursive Lookup Queries

1.  **Client Request:** A client requests a web address. It uses a **Stub Resolver** (a simple DNS client) which first checks its local cache for the name:IP mapping.
2.  **Local DNS Server (Recursive Query):** If the local client's cache doesn't have the record, it forwards the query to its configured **Local DNS Server** (also known as a **Recursive Resolver**). This local server performs a recursive query.
3.  **Root Name Server:** The local DNS server contacts one of the Root Name Servers (using a pre-configured list of IP addresses).
4.  **Iterative Responses (from Root/TLD):**
    * If the Root Server is not authoritative for the requested record, it returns the IP address of the Server for the TLD (`.com`, `.org`, etc.).
    * If the TLD name server is also not authoritative, it returns the IP address of the Authoritative Name Server for the specific domain (e.g., `example.com`).
    * **Iterative lookup** means that a name server responds to a query with either the requested record OR the address of a name server at a lower level in the hierarchy that is authoritative for the namespace. It makes no effort to try to make additional queries to locate the information it does not have.
5.  **Authoritative Name Server:** The local DNS server then directly queries the **Authoritative Name Server** for the domain.
6.  **Record Return & Caching:** This authoritative server returns the requested host record for the domain. The local DNS server caches the record and responds to the client.
7.  **Client Caching:** The client now has an IP address for the domain, which it then caches.

**Recursive lookup** means that if the required server is not authoritative, it takes on the task of querying other name servers until it finds the requested record or times out.

* A query from a client to its local DNS server is typically a **recursive lookup**.
* A query from a local DNS server to the Root, TLD, or Authoritative servers is an **iterative lookup**.

Most Internet-accessible DNS Servers disable recursive queries for external clients. **Recursive Resolvers** are typically only accessible by authorized clients (e.g., subscribers within an ISP's network or clients on a private LAN).


#### DNS Resource Records (RRs)

A DNS **Zone** contains numerous resource records. These records allow a DNS name server to resolve queries for names and services hosted in the domain into IP addresses. The most common types of records stored in the DNS database are for Start of Authority (SOA), IP addresses (A and AAAA), SMTP mail exchangers (MX), name servers (NS), pointers for reverse DNS lookups (PTR), and domain name aliases (CNAME)

* **Start of Authority (SOA) Record:** Identifies the primary Authoritative name server that maintains complete resource records for the zone. It includes contact info and a **Serial Number** for version control (critical for zone transfers).
* **Name Server (NS) Record:** Identifies authoritative DNS name servers for the zone. Most zones are configured with secondary name servers for redundancy and load balancing. Secondary NS hold read-only copies of resource records but are still authoritative for the zone.
* **Address (A) Record:** Used to resolve a host name to an **IPv4 address**.
* **Address (AAAA) Record:** Used to resolve a host name to an **IPv6 address**.
    * *Note:* AAAA records can exceed the typical UDP protocol transmission size (512 bytes) on port 53. This can result in UDP packets being fragmented into several IP packets, which may be blocked by firewalls if not configured to expect them. DNS servers are also configured to allow connections over TCP port 53, as this allows longer record transfers exceeding 512 Bytes.
    * An admin can configure multiple A or AAAA records to point different host names to the same IP address.
    * It is also possible to configure multiple A or AAAA records with the same host name but different IP addresses. This is a basic load balancing technique referred to as **Round Robin DNS**.
* **Canonical Name (CNAME) Record:** Used to configure an **ALIAS** for an existing address record (A or AAAA). CNAME records are often used to make DNS administration easier. An alias can be redirected to a completely different host temporarily during system maintenance. Multiple different named records can refer to the same IP address (and vice versa in the case of load balancing).
    * *Best Practice:* While it's possible to use multiple A/AAAA records for a single FQDN, using CNAME records is often considered best practice for aliases.
* **Mail Exchange (MX) Record:** Used to identify an email server for the domain.
    * The host identified in an MX record must have an associated A or AAAA record.
    * **An MX record MUST NOT point to a CNAME record.** It must point directly to an A or AAAA record.
* **Service (SRV) Record:** Contains the service name and port on which a particular application is hosted. They are an essential part of the infrastructure of Active Directory, used to locate domain controllers. As with MX, SRV records can be configured with a priority value.
* **Text (TXT) Record:** Used to store any free-form text that may be needed to support other network services. A single domain may have many TXT records. Most commonly, they are used as part of **Sender Policy Framework (SPF)** and **DomainKeys Identified Mail (DKIM)**.
    * **SPF (Sender Policy Framework):** Used to list the IP addresses or names of servers that are permitted to send email from a particular domain. Combats sending of spoofed email. Mail servers check that incoming mail really did come from an authorized host.
    * **DKIM (DomainKeys Identified Mail):** Used to decide whether you should allow received email from a given source. DKIM uses encrypted signatures to prove that a message really originated from the domain it claims, preventing spam and mail spoofing. You put your public key in the DKIM TXT record.

#### Pointer (PTR) Records / Reverse Lookup

DNS Servers have **Forward Lookup Zones** and **Reverse Lookup Zones**.
* All previously listed records (A, AAAA, CNAME, MX, SRV, TXT) are **forward lookup** records, as they all return an IP address when given a host name.
* A **reverse lookup / DNS Query** returns the Host name associated with a given IP address. This information is stored in a **Reverse Lookup Zone** as a **PTR Record**.
* Reverse DNS querying uses a special domain named by the first three octets of IPv4 addresses in the zone in reverse order, appended with `in-addr.arpa`. For IPv6, each character is expressed in reverse order up to the network prefix as a subdomain and appended with `ip6.arpa`.
    * Example IPv4: `198.51.100.1` becomes `1.100.51.198.in-addr.arpa`
    * Example IPv6: `2001:0db8::abcd:ef12:1234` becomes `4.3.2.1.2.1.f.e.d.c.b.a.d.c.b.0.0.0.0.0.0.0.0.0.8.b.d.0.1.0.0.0.2.ip6.arpa`
* Reverse lookup zones are not mandatory and are often omitted from DNS servers.


#### DNS Server Configuration

* The function of a **Resolver** is to perform Recursive queries in response to requests from client systems (and stub resolvers). An alternative to recursion is **Forwarding** queries.
* A Recursive Resolver must be configured with a **Root Hints File** so that it can query the whole DNS hierarchy from the Root Server down.
* DNS Servers should allow Recursive queries **only from Authorized Internal Clients** for security.

#### DNS Zones

DNS Name Servers maintain DNS namespace in **Zones**. A single Zone namespace might host records for multiple Domains. A single name server might be configured to manage multiple Zones.

* **Primary (Master) Zone:** Zone records held on this server are **editable (writable)**. A zone can be hosted by multiple primary servers for redundancy, but changes must be carefully replicated and synchronized. It is critical to update the **Serial Number** for each change.
* **Secondary (Slave) Zone:** This server holds a **Read-Only Copy** of the zone. This copy is maintained through a process of replication known as **Zone Transfer** from a primary name server. Typically, secondary servers are provided on two or more separate servers to provide fault tolerance and load balancing. The Serial Number is a critical part of Zone Transfer.

A name server that holds complete records for a domain can be defined as **Authoritative**. This means that a record in the zone identifies the server as a name server for that namespace. Both Primary & Secondary name servers are authoritative.

Servers that don't maintain a zone are referred to as **Cache-Only Servers** during the name resolution process. A non-authoritative answer from a server is one that derives from a cached record rather than directly from the zone records.

#### Time to Live (TTL)

Each Resource Record can be configured with a default **TTL (Time to Live)** value, measured in seconds. This value instructs resolvers how long a query result can be kept in cache.
* Setting a **low TTL** allows records to be updated more quickly but increases load on the server and can cause higher latency (delay) on client connections to services (due to more frequent queries).
* Common TTL values: 300 seconds (5 mins), 3600 seconds (1 hour), 86400 seconds (1 day), 604800 seconds (1 week).
* A very long TTL can cause issues if changes are made to the record, as the old cached information will persist for longer.

#### Forwarders and Conditional Forwarders

* A **Forwarder** transmits a client query to another DNS server and routes its reply back to the client.
* A **Conditional Forwarder** performs this task for certain domains only. For example, an admin might configure a DNS server that is authoritative for the local private network (Internal DNS), but that forwards any requests for Internet domains to an external DNS resolver run by your ISP, or to a trusted public service like Google DNS (8.8.8.8) or Cloudflare (1.1.1.1).


### Troubleshooting DNS

The use of caching and the distributed nature of DNS means that configuration errors can occur in several different places. To investigate name resolution issues:

1.  **Verify Host Configuration:**
    * Windows: `ipconfig /all`
    * Linux: `hostname -I` or `ip a`
2.  **DNS Lookup Tools:**
    * **`nslookup` (Windows):** Troubleshoots DNS name resolution.
        * Running `nslookup` without arguments starts it in interactive mode.
        * Full syntax: `nslookup [options] [Host] [DNS Server]`
        * `options`: Specifies lookup subcommand (e.g., `-type=ns` to query name servers, `-type=MX` for mail records).
        * `Host`: Can be a Host Name, Domain Name/FQDN, or an IP address.
        * `DNS Server`: The IP address of a specific server to use for the query (e.g., `8.8.8.8` for Google DNS).
    * **`Resolve-DnsName` (PowerShell - Windows):** Provides a more sophisticated, scripted approach using cmdlets. It allows for more flexible testing of name resolution (e.g., checking HOSTS file, DNS Cache, specific DNS servers).
    * **`dig` (Domain Information Groper - Linux/Unix/macOS):** A powerful command-line tool for querying DNS servers.
        * Can be run pointing at a specific DNS server; otherwise, it uses the default resolver.
        * Without any specific settings, it queries the DNS Root Zone.
        * A simple query like `dig host` will search for the A record for the Host, Domain, or FQDN; `dig -x [IP Address]` will perform a PTR (reverse) lookup.
3.  **Interpreting Results:**
    * "The Authority" / Authoritative: The DNS server queried is the authority for the zone; it contains the zone source file.
    * "Non-Authoritative": The answer is derived from cached information, not directly from the zone source file. This information is valid only for its TTL. A very long TTL can cause issues if changes are made.


### DNS Caching

DNS caching is performed by both DNS servers and client computers. Each application on a client computer might also be configured to manage its own DNS cache rather than relying on a shared Operating System cache.

Changes to Resource Records (and subsequent updates) can be relatively slow to propagate around the Internet due to caching.

**Planning for a Record Change:**
1.  **Reduce the TTL** in the period before the change (e.g., to 5 minutes).
2.  **Wait for the old TTL to expire** for existing cached records to clear.
3.  **Update the record** on the authoritative DNS server.
4.  **Wait for the change to propagate** (at least the reduced TTL duration) before expecting all clients to see the new record.
5.  **Revert to the original TTL value** when the update has safely propagated and is stable.


### Internal vs. External DNS Zones

A company will use primary & secondary NS to maintain authoritative zone records for the domains it manages.

* **Internal DNS Zones:** Refer to the domains used on the private network only. These are available only to internal clients. For instance, the zone records for `subdomain.bigsupport.com` would be served from internal name servers, allowing a client PC (`pc1.bigsupport.com`) to contact a local application server (`crm.bigsupport.com`). The name servers hosting these internal subdomain records **must not be accessible from the Internet** for security.
* **External DNS Zones:** Refer to records that Internet clients must be able to access. For a company running web and email services on `bigsupport.com`, in order for Internet hosts to use a web server at `www.bigsupport.com` or send email to an `@bigsupport.com` address, the zone records for `bigsupport.com` must be hosted on a name server that is accessible over the Internet.

It is generally a good idea to separate the DNS servers used to host zone records (authoritative servers) from the ones used to service client requests for non-authoritative domains (recursive resolvers/forwarders).


### Key Configuration Best Practices for DNS

* Configure primary & secondary name servers to host records for your LAN. These name servers should only be accessible by authorized internal clients.
* Configure the appropriate Host (A/AAAA), MX, Service (SRV), and TXT records for the forward lookup zone.
* Configure a reverse lookup zone to allow clients to resolve IP addresses to host names (PTR records).
* Configure secondary NS to obtain up-to-date records periodically through a Zone Transfer with the primary NS.
* To resolve client Internet queries, set up a forwarder to pass queries to trusted resolvers on the Internet (e.g., your ISP's DNS server, or trusted public services like Google DNS or Cloudflare DNS).
* For external DNS, consider using a third-party provider, ideally a Cloud Service, to ensure high availability. Without public DNS, your customers cannot browse your websites or send you email.
* Implement SPF and DKIM TXT records to prevent mail spoofing by proving sender validity and digitally signing your outgoing mail.
* Be aware that even with DNS server and client caching, changes to resource records can be relatively slow to propagate. Plan for record changes by reducing TTLs beforehand.


### DNS Configuration

Devices will save the DNS Server’s responses to a local DNS cache, this means they don’t have to query the server every single time they want to access a particular destination, this may lead to DNS cache poisoning. For hosts in a network to use dns, you don’t need to configure DNS on the routers , the routers simply forward the DNS messages like any other packets. Cisco router can be configured as a DNS server , although rare. A Cisco Router can also be configured as a DNS client Most devices have a Hosts file which existed before dns to save the Hostname of IP addresses local to a device, which is C:\windows\system32\drivers\etc\hosts or /etc/hosts
Normal DNS requests and responses are sent by UDP port 53, DNS can use TCP or generates TCP sessions for only Zone Transfers and query responses that exceed 512bytes—Recursive DNS Search [which allow DNS servers to provide authoritative name resolution to hosts]. 

A Recursive DNS server is that, when asked for information it does not have, performs a repetitive (recursive) process to ask other DNS servers in sequence, sending repeated DNS messages in an effort to identify the authoritative DNS server or DNS server that knows the information. 

Router> enable 
Router# configure terminal 
Router(config)# ip dns server -> Configure a Router to act as a DNS server
Router(config)# ip host hostname host-IP -> Add an entry to the ip hostname table, Building the router’s own host table with a list of hostname/IP address mappings. 
Router(config)# ip name-server 8.8.8.8 -> Specify address of name server to use, this Configures an external DNS Server that router will query, if the requested record is not in its own host table. 
Router(config)# ip domain lookup -> Enable Router to perform DNS queries. Becoming a DNS client.
Router(config)# ip domain name FQDN -> Configure the default domain name locally, once done all connected devices to the router, will have a FQDN of hostname.FQDN
Router(config)# do show hosts -> To view the routers DNS cache and host table.


---

## DYNAMIC HOST CONFIGURATION PROTOCOL (DHCP)

### Dynamic Host Configuration Protocol (DHCP)
* **Function:** A network management protocol used on Internet Protocol (IP) networks for dynamically assigning IP addresses and other communication parameters (like subnet mask, default gateway, DNS server addresses) to devices connected to the network.
* **Core Purpose:** Automates the configuration of network devices, eliminating the need for manual configuration and reducing errors.
* **Protocol:** Operates at the **Application Layer** of the OSI model but functions heavily with the **Transport Layer (UDP port 67 for server, UDP port 68 for client)**.
* **Key Concept:** DHCP uses a client-server model. A DHCP server manages a pool of IP addresses and configuration information.
* **Ports:** Client UDP 68, Server UDP 67.
**DHCP** provides an automatic method for allocating an IP address, subnet mask, and optional parameters (like Default Gateway and DNS Server Addresses) when a host joins a network. The IP address is leased by the server for a limited period only.

### DHCP DORA Process (IP Lease Process)
* **Function:** The four-step process a DHCP client uses to obtain an IP address and other configuration information from a DHCP server.
* **Steps:**
    1.  **Discover:** The client broadcasts a **DHCP Discover** message on the local network to find available DHCP servers. (Source IP: 0.0.0.0, Destination IP: 255.255.255.255)
    2.  **Offer:** Available DHCP servers receive the Discover message and respond with a **DHCP Offer** message. This message proposes an IP address and other configuration parameters to the client. (Source IP: Server's IP, Destination IP: 255.255.255.255 or Client's MAC)
    3.  **Request:** The client receives one or more Offer messages and broadcasts a **DHCP Request** message to the network, formally requesting the offered IP address from a specific server (usually the first one that offered).
    4.  **Acknowledge:** The chosen DHCP server sends a **DHCP Acknowledge (ACK)** message to the client, confirming the IP address assignment and providing all the necessary configuration parameters. The client then configures its network interface with the received information. Once the client receives the ACK, it performs an ARP message to check that the Address is unused. If so, it will start to use the Address and options.

(Image Placeholder - DHCP DORA Process)

### DHCP Server Configuration & Scopes

A DHCP Server must be allocated a static IP Address and configured with a range of IP Addresses and Subnet Masks, plus option values, to allocate as a **Scope**. To define a scope, you must provide a start & end IP Address along with a Subnet mask.

The server maintains a one-to-one mapping of scopes to subnets (i.e., no scope can cover more than one subnet & no subnet can contain more than one scope). The DHCP Server must be placed in the same Subnet as its clients.

More advanced DHCP servers might be configured to manage & support multiple scopes. Where a server provides IP Config for multiple subnets/scopes, it must choose the pool to service each request based on the subnet from which the request originated.

For fault tolerance and redundancy, **Split Scopes** can be configured with non-overlapping address ranges. DHCP for multiple subnets is usually handled by configuring **Relay Agents** to forward requests to a central DHCP server.


### DHCP Lease Management

An IP Address is leased by the server for a limited period only. A client can attempt to renew or rebind the lease before it expires. If the lease cannot be renewed, the client must release the IP address and start the DHCP DORA process again.

* **T1 Timer (Default: Half the lease period has elapsed):** Client attempts to renew the lease with the original DHCP server.
* **T2 Timer (Default: 87.5% of the lease duration is up):** If no response from the original DHCP server, the client attempts to rebind the lease by broadcasting a DHCP request to any available DHCP server.

A long lease time means the client doesn't have to renew the lease often. Where the DHCP server's Address pool is not replenished frequently or IP addresses are in short supply, a shorter lease period enables the DHCP Server to allocate addresses previously assigned to hosts that have become inactive on the Network.

If both T1 & T2 timers elapse, the client releases the IP address and broadcasts to discover a new server.

To force a release of a lease, a Windows Client can use `IPCONFIG /RELEASE` and `IPCONFIG /RENEW`. Linux clients can use `dhclient`, Network Manager, or Systemd-Networks.

Failure to renew a lease: A Windows host reverts to **Automatic Private IP Addressing (APIPA)** (addresses in the range `169.254.0.0/16`). Linux might use link-local config, set the Address to unknown, or leave the interface unconfigured.


### DHCP Options

Each additional Option supplied by a DHCP Server is identified by a byte or decimal Value. Such Options include:

* The **Default Gateway** (IP Address of the Router)
* The **IP Address(es) of DNS Servers** (i.e., act as resolvers for name queries)
* The **DNS Suffix** (domain name) to be used by the client
* Other Useful Options such as Network Time Sync (NTP), File Transfer (TFTP), and VoIP proxy.

A set of default/global options can be configured on a server-wise basis. Default Options can be overridden by setting scope-specific Options.


### DHCP Reservations & Exclusions

One disadvantage of the standard Dynamic Assignment method is that it doesn't guarantee that any given client will retain the same IP Address over time.

1.  One solution is to configure **Static Assignments** using IP Addresses outside the DHCP Scope OR a specially configured Exclusion Range.
2.  A **Reservation** is a mapping of a client's MAC Address or Interface ID to a specific IP Address within the DHCP Server's Address pool.
3.  An **Automatically Allocated Reservation** refers to an Address that is leased permanently to a client. The Admin doesn't predetermine which specific IP Address will be leased; the server automatically makes a permanent lease for the first requested IP.


### DHCP Relay Agent

* **Function:** A network device (typically a router) that forwards DHCP messages between clients and servers that are on different IP subnets. DHCP messages are usually broadcast, so they don't cross router boundaries by default.
* **Purpose:** Allows a single DHCP server to serve multiple subnets without needing a server on each subnet, saving administrative overhead and resources.
* **Mechanism:** The relay agent converts broadcast DHCP messages into unicast messages directed to the DHCP server.
A **DHCP Relay Agent** can be configured to provide forwarding of DHCP traffic between Subnets. Routers that can provide this type of forwarding are RFC 1542 Compliant.

The DHCP Relay Agent (configured on RFC 1542 Compliant Routers) intercepts DHCP broadcast frames, then applies a Unicast Address for the appropriate DHCP server(s) and forwards them over the interface for the subnet containing the server. The DHCP Server can identify the original IP Subnet from the packet and offer a lease from the appropriate scope (subnet range). The DHCP relay also performs the reverse process of directing responses from the server to the appropriate client Subnet.

**IP Helper** functionality can be configured on Routers to allow certain types of broadcast traffic (including DHCP) to be forwarded to an interface. The IP helper function supports the function of the DHCP relay agent. UDP forwarding is a more general application of the same principle.


### DHCPv6 (Ports: Client UDP 546, Server UDP 547)

IPv6's Stateless Address Auto-Configuration (SLAAC) process can locate routers and generate a host address with a suitable network prefix automatically. Therefore, the role of a DHCP Server in IPv6 is different. DHCPv6 is often just used to provide additional option settings, rather than leases for host addresses.
As IPv6 does not support broadcasts, clients use the multicast Address for routers (`ff02::1:2`) to discover a DHCPv6 server, using Neighbor Discovery Protocol (NDP).
* **Function:** Provides stateful address configuration and other network parameters (DNS servers, NTP servers) for IPv6 hosts.
* **Types:**
    * **Stateful DHCPv6:** Assigns unique IPv6 addresses and all configuration parameters to hosts, maintaining state (records of assigned addresses).
    * **Stateless DHCPv6:** Used in conjunction with SLAAC. SLAAC assigns the IPv6 address and default gateway, while Stateless DHCPv6 provides additional information like DNS server addresses or SIP server addresses.
* **Process:** Similar to DHCP for IPv4, involving messages like Solicit, Advertise, Request, Reply.
* **Requirement:** Requires a DHCPv6 server.


#### DHCPv6 Process Steps:

1.  **Step 1: Client Router Solicitation (RS):** Client uses NDP Router Solicitation to request information from the Router.
2.  **Step 2: Router Advertisement (RA):**
    * **Stateless Mode:** Router Advertisement; Client obtains a Network prefix from a Router Advertisement and, using it with the appropriate Interface ID, obtains only extra options from the DHCPv6 Server.
    * **Stateful Mode:** The Router Advertisement cannot help the client host obtain a routable IP address using usual NDP Router Advertisement. Hence, it directs the client to the DHCPv6 server to obtain it directly. (Therefore, the host obtains IP prefix AND extra options from DHCPv6 Server Directly!)
3.  **Step 3: Client Solicit:** Client solicits a DHCPv6 Server using the multicast address `ff02::1:2`.
4.  **Step 4: DHCPv6 Server Advertise:** DHCPv6 Server Advertises its availability.
5.  **Step 5: Client Request (Information Request):** Client requests information message on IP Addressing & Extra Options.
6.  **Step 6: DHCPv6 Server Reply:** DHCPv6 Server replies Message with IP Address from its scope and extra information (DNS, SIP, SNTP, Domain Options, etc.).

**Note:** There is no mechanism in DHCPv6 for setting the Default Route; the host learns the default gateway from the Router Advertisement (NDP).

### DHCP Scope Properties (General)

* **IP Address Range (+ excluded addresses):** A contiguous pool of IP Addresses for a subnet. This is called a pool (or scope). DHCP Exceptions & Exclusions can be made inside of this scope.
* **Lease Durations:** Addresses are reclaimed after a lease period. A longer lease time means the client doesn't have to renew often. If the Address pool is limited, use short lease times to prevent address exhaustion.
    * T1 Timer (50% of lease time).
    * T2 Timer (87.5% of lease time). If T1 & T2 are exceeded, the client restarts the DORA process.
* **DNS Server, Default Gateway, VoIP Servers:** Allocation & Reallocation.


### DHCP Assignment Methods

* **Dynamic Assignment:**
    * DHCP server has a pool of addresses to give out.
    * Addresses are reclaimed after a lease period.
* **Static Assignment / Static DHCP / IP Reservation / Address Reservation:**
    * Administratively configured using a table of MAC addresses to matching IP addresses.
    * Ensures a specific device always gets the same IP.
* **Automatic Assignment:**
    * Similar in principle to Dynamic.
    * DHCP server keeps a list of past assignments, so a client will always get the same IP address if available.
    * Additional overhead in storage for the server.

Renew lease after T1; if not, check back at timer T2. The countdown is reset if the lease is renewed.


### Best Practices

* Configure Secure DHCP & DNS services and ensure that all network hosts can contact them, using DHCP Relay where appropriate.
* Configure reservations or static assignments for hosts that need to be allocated a consistent IP address.

**EVERY HOST INTERFACE NEEDS AN IP CONFIG TO COMMUNICATE ON A TCP/IP NETWORK.**

### DHCP Configuration

DHCP (BootP-Server UDP 67 / BootP-Client UDP 68) is used to allow hosts to automatically/dynamically learn various aspects of their network configuration, such as IP ADDRESS, SUBNET MASK, DEFAULT GATEWAY, DNS SERVER without manual/static configuration. DHCP allows both the permanent assignment of host addresses, but more commonly, DHCP assigns a temporary lease of IP addresses. With these leases, the DHCP server can reclaim IP addresses when a device is removed from the network, making better use of the available addresses. DHCP also enables mobility.

DHCP server ‘lease’ IP address to clients. These leases are usually not permanent, and the client must give up the address at the end of the lease.

* To release a DHCP leased address → `ipconfig /release`.
* To obtain a DHCP address lease → `ipconfig /renew`.

DHCP operations fall into four phases: client-server discovery, IP lease offer, IP lease request, & IP lease acknowledgement. These stages are often abbreviated as DORA for:

* **DISCOVERY** → (Client → Server) Broadcast (always)
    * **Reason:** The client does not yet have an IP address, so it sends to the broadcast IP 255.255.255.255 to reach any available DHCP server.
* **OFFER** → (Server → Client) Usually Broadcast (can be unicast under specific conditions).
    * **Reason:** The client may not yet have a usable IP, so the server broadcasts the offer so the client can receive it even without a configured IP stack. However, if the server knows the client’s MAC address and the network allows it, it can unicast the offer directly to the client.
* **REQUEST** → (Client → Server) (broadcast msg ff:ff:ff:ff:ff:ff, 255.255.255.255 from client, however a field is filled in the DHCP packet - DHCP server identifier) The client still doesn’t have a valid IP and is notifying all DHCP servers of the chosen offer, so it uses broadcast again.
* **ACKNOWLEDGEMENT** → (either Broadcast or Unicast)(Server → Client):
    * **Broadcast or Unicast depending on the client state:**
        * Broadcast if it’s a new lease and the client has no IP yet.
        * Unicast if the client already has an IP and is renewing the lease (typically during the T1 or T2 timer stages). The client includes its current IP and can receive unicast packets now.
* **NAK (Negative Acknowledgment):** Opposite of Acknowledgment, used to decline a client's request.
* **RELEASE:** Used to tell the server that the client no longer requires its IP address.
* **DECLINE:** Used to decline the IP address offered by the DHCP server.

DHCP clients, however, have a somewhat unique problem: they do not have an IP address yet, but they need to send these DHCP messages inside IP packets. To make that work, DHCP messages make use of two special IPv4 addresses that allow a host that has no IP address to still be able to send and receive messages on the local subnet:

* **0.0.0.0:** An address reserved for use as a source IPv4 address for hosts that do not yet have an IP address.
* **255.255.255.255:** The local broadcast IP address. Packets sent to this destination address are broadcast on the local data link, but routers do not forward them.

Some Network Engineers might choose to configure each router in a network topology as the DHCP sever for its connected LANs to keep the protocol flow local. However, for large enterprises it’s recommended to use a centralized DHCP server. A centralized DHCP server approach has advantages as well. In fact, some Cisco design documents suggest a centralized design as a best practice, in part because it allows for centralized control and configuration of all the IPv4 addresses assigned throughout the enterprise.

If the server is centralized, it won’t receive the DHCP clients’ broadcast DHCP messages (as broadcast messages don’t leave the local subnet). To fix this, we configure a router to act as a DHCP RELAY AGENT. The router-RelayAgent will forward the clients' broadcast DHCP messages to the remote DHCP server as Unicast messages.

In some enterprise networks, that router configuration can be a single command on many of the router’s LAN interfaces (`ip helper-address server-ip`), which identifies the DHCP server by its IP address. This feature, by which a router relays DHCP messages by changing the IP addresses in the packet header, is called DHCP relay.

A DHCP pool is a subnet of addresses that can be given to DHCP clients, as such as other info such as default gateway and dns server. Ensure to create a separate DHCP pool for each network the router is acting as a DHCP server for.

#### DHCP Server Configuration for Dynamic Allocation - DHCP acting in the capacity of a server

```cli
Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.20
```
Specify a range of addresses that won’t be given to DHCP clients. The server needs to know which addresses in the subnet to not lease. This list allows the engineer to reserve addresses to be used as static IP addresses.

```cli
Router(config)# ip dhcp pool LAN_CLIENTs
```
Specify DHCP pool name.

```cli
Router(dhcp-config)# network 192.168.10.0/24
```
Specify the subnet of addresses to be assigned to clients (excluding the excluded addresses). The DHCP server can use this information to know all addresses in the subnet. (The DHCP server knows to not lease the subnet ID or subnet broadcast address.)

```cli
Router(dhcp-config)# default-router IP-ADDR
```
This is the IP address of the router on that subnet. Specify the default gateway that DHCP client should use. Host Default Router Setting Should Equal Router Interface Address.

```cli
Router(dhcp-config)# dns-server 8.8.8.8
```
Specify the DNS server that DHCP clients should use. This is a list of DNS server IP addresses.

```cli
Router(dhcp-config)# domain-name FQDN
```
Specify the Domain-Name of the Network.

```cli
Router(dhcp-config)# lease days hours minutes
```
The server leases an address for a time (usually a number of days), and then the client can ask to renew the lease. If the client does not renew, the server can reclaim the IP address and put it back in the pool of available IP addresses. The server configuration sets the maximum time for the lease.

```cli
Router(dhcp-config)# lease infinite
```
This configures AUTOMATIC ALLOCATION, which sets the DHCP lease time to infinite. As a result, once the server chooses an address from the pool and assigns the IP address to a client, the IP address remains with that same client indefinitely.

#### DHCP Relay Agent Configuration - DHCP acting in the capacity of a Relay agent

```cli
Router(config)# interface Gx/y
```
Specify the interface connected to the subnet of the client devices.

```cli
Router(config-if)# ip helper-address dhcp-server-IP
```
Configure an interface to forward/“RELAY” DHCP broadcasts across a network to the IP address of the DHCP server.

We first specified an interface on the router serving the subnet that requires a DHCP, and then we configured a relay agent for that interface using the IP address of a centralized DHCP server. Ensure the router has a static or dynamic route to the DHCP server. The DHCP relay feature must be configured for any router interface that connects to a subnet where:

* DHCP clients exist in the subnet
* DHCP servers do not exist in the subnet

Once such interfaces have been identified, the configuration requires the `ip helper-address` interface subcommand on each of those interfaces. The `ip helper-address server-ip` subcommand tells the router to do the following for the messages coming in an interface, from a DHCP client:

1.  Watch for incoming DHCP messages, with destination IP address 255.255.255.255.
2.  Change that packet’s source IP address to the router’s incoming interface IP address.
3.  Change that packet’s destination IP address to the address of the DHCP server (as configured in the `ip helper-address` command).
4.  Route the packet to the DHCP server.

This command gets around the “do not route packets sent to 255.255.255.255” rule by changing the destination IP address. Once the destination has been set to match the DHCP server’s IP address, the network can route the packet to the server.

**NOTE:** THE `IP HELPER-ADDRESS` command configures an interface to forward broadcasts to the following UDP ports for the protocols DNS, TFTP, NetBios, TACACS.

#### DHCP Client Configuration - DHCP acting in the capacity of a Client

```cli
Router(config)# interface Gx/y
```
Specify the interface connected to the DHCP server.

```cli
Router(config-if)# ip address dhcp
```
Use the command to tell the router to use DHCP to learn its own IP address. The router then adds a default route based on the default gateway (routers do not normally use a default gateway setting; only hosts use a default gateway setting. However, the router takes advantage of that information by turning that default gateway IP address into the basis for a default route) to its IP routing table. In most every case it makes more sense to statically configure router interface IP addresses with the address listed in the `ip address address mask` interface subcommand. However, configuring a router to lease an address using DHCP makes sense in some cases with a router connected to the Internet; in fact, most every home-based router does just that. A router with a link to the Internet can learn its IP address and mask with DHCP and also learn the neighboring ISP router’s address as the default gateway. Additionally, router can distribute that default route to the rest of the routers using an interior routing protocol like OSPF. To recognize this route as a DHCP-learned default route, look to the administrative distance value of 254. IOS uses a default administrative distance of 1 for static routes configured with the `ip route` configuration command but a default of 254 for default routes added because of DHCP. Like Windows, macOS adds a default route to its host routing table based on the default gateway, as well as a route to the local subnet calculated based on the IP address and mask learned with DHCP.

```cli
Router()# show ip dhcp binding
```
Displays all the DHCP clients that are currently assigned addresses, as well as information on Lease expiration, Device IP & MAC.

To see more details specific to DHCP, instead use the `show dhcp lease` command to see the (temporarily) leased IP address and other parameters.

```cli
Router()# show dhcp lease
```

```cli
Router()# show ip dhcp pool
```
Verify the configured IPv4 subnets in a DHCP pool, on a router configured as a DHCP server.

---

## Hypertext Transfer Protocol Secure (HTTPS)
* **Definition:** The secure version of HTTP (Hypertext Transfer Protocol). It uses SSL/TLS (Transport Layer Security) to encrypt communication between a web browser and a website.
* **Core Purpose:** To provide secure communication over a computer network, particularly the internet, ensuring data confidentiality, integrity, and authentication.
* **Protocol Stack:** HTTPS is essentially HTTP layered on top of SSL/TLS.
* **Port:** Primarily uses **TCP port 443**.
* **Key Benefit:** Protects sensitive data (e.g., login credentials, financial transactions) from eavesdropping and tampering by unauthorized parties.

### How HTTPS Works
* **Encryption:** The data exchanged between the client (browser) and the server is encrypted using symmetric encryption after an initial key exchange. TLS uses asymmetric encryption during the handshake to securely exchange the symmetric keys.
* **Digital Certificates:** Servers present a digital certificate (issued by a Certificate Authority - CA) to clients. This certificate contains the server's public key and verifies its identity.
* **Authentication:**
    * **Server Authentication:** The client verifies the server's identity using its digital certificate, ensuring it's communicating with the legitimate website.
    * **Client Authentication (Optional):** In some cases, the server may also request a client certificate to authenticate the client.
* **Data Integrity:** Hashing functions are used to detect any alteration of data during transmission.

(Image Placeholder - HTTPS Process)

The HTTP (The Hyper Text Transfer Protocol) handles our web requests to servers. HTTP functions as a request–response protocol in the client–server computing model. HTTP uses a set of verbs, like GET, POST, PUT, and HEAD, to retrieve and send data. Anytime a page is loaded, there are multiple web requests to retrieve content like images, text, and formatting code.  High-traffic websites often benefit from web “CACHE” servers that deliver content on behalf of upstream servers to improve response time. Web browsers “CACHE” previously accessed web resources and reuse them, when possible, to reduce network traffic. HTTP is a “STATELESS” protocol. A stateless protocol does not require the HTTP server to retain information or status about each user for the duration of multiple requests. However, some web applications implement “Statefulness” or server side sessions using for instance HTTP “COOKIES” or hidden variables within web forms. 

* HTTP/1.1➡️ was one of the first versions of the HTTP protocol to be designed and implemented. It operates by sending messages in the form of text. HTTP/1.1 is commonly used over TCP and is the slowest of the HTTP versions regarding data transmission.
* HTTP/2➡️ is a major revision of HTTP/1.1, developed with the intent to try and reduce web page load latency. However, the most significant departure from HTTP/1.1 is the encapsulation of all messages in binary format rather than plain text. This allows HTTP/2 to apply different techniques for data transmission, including sending smaller packets of data for greater flexibility of data transfer. This also allows a single connection to be made between two communicating entities rather than multiple as required by HTTP/1.1. Similar to HTTP/1.1, HTTP/2 also leverages TCP for transport.
* HTTP/3➡️ is the third major version of HTTP. While there are quite a few complex technological differences between HTTP/3 and the previous versions, one of the most important is how the protocol deals with lost packets. HTTP/3 also differs through its use of transport protocol, leveraging a transport protocol called QUIC, as opposed to earlier versions of HTTPS which use a combination of TCP and TLS to ensure reliability and security respectively. This means that HTTP/3 uses a single handshake to set up a connection, rather than having two separate handshakes for TCP and TLS, meaning the overall time to establish a connection is reduced.
* HTTP Strict Transport Security (HSTS) is a policy mechanism that helps to protect websites against man-in-the-middle attacks such as protocol downgrade attacks and cookie hijacking. It allows web servers to declare that web browsers (or other complying user agents) should automatically interact with it using only HTTPS connections, which provide Transport Layer Security (TLS/SSL), unlike the insecure HTTP used alone. The HSTS Policy is communicated by the server to the user agent via an HTTP response header field named "Strict-Transport-Security". HSTS Policy specifies a period of time during which the user agent should only access the server in a secure fashion. Websites using HSTS often do not accept clear text HTTP, either by rejecting connections over HTTP or systematically redirecting users to HTTPS (though this is not required by the specification). The consequence of this is that a user-agent not capable of doing TLS will not be able to connect to the site. The protection only applies after a user has visited the site at least once, relying on the principle of Trust on first use. The way this protection works is that a user entering or selecting a URL to the site that specifies HTTP, will automatically upgrade to HTTPS, without making an HTTP request, which prevents the HTTP man-in-the-middle attack from occurring.
* WebSocket is a computer communications protocol, providing full-duplex communication channels over a single TCP connection. Although they are different, RFC 6455 states that WebSocket "is designed to work over TCP-HTTP ports 443 and 80 as well as to support HTTP proxies and intermediaries," thus making it compatible with HTTP. To achieve compatibility, the WebSocket handshake uses the HTTP Upgrade header to change from the HTTP protocol to the WebSocket protocol. 
* WebRTC (Web Real-Time Communication) is a free and open-source project providing web browsers and mobile applications with real-time communication (RTC) via simple application programming interfaces (APIs). It allows audio and video communication to work inside web pages by allowing direct peer-to-peer communication, eliminating the need to install plugins or download native apps. It’s purpose of the project is to "enable rich, high-quality RTC applications to be developed for the browser, mobile platforms, and IoT devices, and allow them all to communicate via a common set of protocols"


## SMTP (Simple Mail Transfer Protocol) How does email work? 
To send email, the standard is SMTP is an internet standard connection-oriented, text-based, communication protocol for electronic mail transmission in which a mail sender communicates with a mail receiver by issuing command string & necessary data over a reliable ordered data stream channel(TCP). Mail servers and other Mail/Message Transfer agents use SMTP to send and receive mail messages, SMTP servers commonly use the TCP on port number 25 (for unencrypted plaintext) and 587 (for encrypted communications). The SMTP server performs three basic functions:
 1. It verifies who is sending emails through the SMTP server.
 2. It sends the outgoing mail
 3. If the outgoing mail can't be delivered it sends the message back to the sender

Email is submitted by a mail client (mail user agent, MUA) to a mail server (mail submission agent, MSA) using SMTP on TCP port 587 involving a SMTP Handshake. Most mailbox providers still allow submission on traditional port 25. The MSA delivers the mail to its mail transfer agent (mail transfer agent, MTA). Often, these two agents are instances of the same software launched with different options on the same machine. The main difference between an MTA and an MSA is that connecting to an MSA requires SMTP Authentication. 
The boundary MTA uses DNS to look up the MX (mail exchangers) DNS resource record for the recipient's domain (the part of the email address on the right of @). The MX record contains the name of the target-destination MTA. Based on the target host and other factors, the sending MTA selects a recipient server and connects to it to complete the mail exchange. An MDA (mail delivery agents) saves messages in the relevant mailbox format. As with sending, this reception can be done using one or multiple computers, Once delivered to the local mail server, the mail is stored for batch retrieval by authenticated mail clients (MUAs).
Sender MUA >> MSA >> MTA 📤 >> DNS Lookup of MX records
Recipient 📥 MTA >> MDA >> MUA >> Forwarded to IMAP/POP
 
Mail is retrieved by end-user applications, called email clients, using Internet Message Access Protocol (IMAP), a protocol that both facilitates access to mail and manages stored mail, or the Post Office Protocol (POP) which typically uses the traditional inbox mail file format. “SMTP defines message transport, not the message content. Thus, it defines the mail envelope and its parameters, such as the envelope sender, but not the header (except trace information) nor the body of the message itself. STD 10 and RFC 5321 define SMTP (the envelope), while STD 11 and RFC 5322 define the message (header and body), formally referred to as the Internet Message Format.”

## IMAP (Internet Message Access Protocol)
IMAP is an Internet standard protocol used by email clients to retrieve email messages from a mail server over a TCP/IP connection. IMAP was designed with the goal of permitting complete management of an email box by multiple email clients, therefore clients generally leave messages on the server until the user explicitly deletes them, This and other characteristics of IMAP operation allow multiple clients to manage the same mailbox. IMAP offers access to the mail storage. Clients may store local copies of the messages, but these are considered to be a temporary cache. An IMAP server typically listens on port number 143. IMAP over SSL/TLS (IMAPS) is assigned the port number 993.
Advantages over POP
- Connected and disconnected nodes       --Server Side Searches
- Multiple Simultaneous clients*              — Multiple Mailboxes on the server
- Access to Mulitpurpose Internet Mail Extensions message parts and partial fetch
- Message State Information (Use of Flags)   —Built-in Extension Mechanism

## POP (Post Office Protocol) 
POP is an application-layer Internet standard protocol used by e-mail clients to retrieve e-mail from a mail server. POP version 3 (POP3) is the version in common use. A POP3 server listens on well-known port number 110 for service requests. Encrypted communication for POP3 is either requested after protocol initiation, using the STLS command, if supported, or by POP3S, which connects to the server using Transport Layer Security (TLS) or Secure Sockets Layer (SSL) on well-known TCP port number 995.

## SSH Secure Shell (SSH) https://github.com/openssh/openssh-portable-ssh

### Secure Shell (SSH)

SSH Secure Shell (SSH) is a cryptographic network protocol for operating network services securely over an unsecured network. SSH provides a secure channel over an unsecured network by using a client–server architecture, connecting an SSH client application with an SSH server. IT professionals and engineers use this to help configure and program a system remotely and securely. The standard TCP/UDP/SCTP port for SSH is 22. The encryption used by SSH is intended to provide Confidentiality and Integrity of data over an unsecured network, such as the Internet. SSH uses public-key cryptography to Authenticate the remote computer and allow it to authenticate the user, if necessary. SSH is typically used to log into a remote machine and execute commands, but it also supports tunneling, forwarding TCP ports and X11 connections; it can transfer files using the associated SSH file transfer (SFTP) or secure copy (SCP) protocols.[2]

SSH is a secure alternative to the non-protected login protocols (such as telnet, rlogin) and insecure file transfer methods (such as FTP). Putty is for Windows Operating System. Just a regular GUI interface for SSH protocol.

In SSH, a private key is used for authenticating computers and users. A host key authenticates servers, and an Authorized keys and identity key serves as an authentication credential for a user. Together they are called SSH keys.
In SSH, public key cryptography is used for authenticating computers and users. Host keys authenticate hosts. Authorized keys and identity keys authenticate users.
The most common type of SSH key is an authorized key, which is a public key.

* `ssh-keygen` - creates a key pair for public key authentication
* `ssh-copy-id` - configures a public key as authorized on a server
* `ssh-agent` - Authentication Agent to hold private key for Public key authentication
* `ssh-add` - Adds private Key identities/fingerprints to the OPENSSH Authentication Agent.

SSH (Secure Shell) is a protocol primarily used for secure remote login and other secure network services over an insecure network. It uses the client-server model and supports various forms of tunneling, which can be utilized to securely forward traffic over the network.

#### SSH Architecture

Architecture—>The SSH-2 protocol has an internal architecture (defined in RFC 4251) with well-separated layers, namely:

* **The transport layer**: which typically runs on top of TCP/IP. This layer handles initial key exchange as well as server authentication, and sets up encryption, compression and integrity verification.
* **The user authentication layer**: This layer handles client authentication and provides a number of authentication methods. Authentication is client-driven: when one is prompted for a password, it may be the SSH client prompting, not the server. The server merely responds to the client's authentication requests. Widely used user-authentication methods include the following:
    * **password**: a method for straightforward password authentication, including a facility allowing a password to be changed. Not all programs implement this method.
    * **publickey**: a method for public-key-based authentication, usually supporting at least DSA, ECDSA or RSA keypairs, with other implementations also supporting X.509 certificates.
    * **keyboard-interactive** (RFC 4256): a versatile method where the server sends one or more prompts to enter information and the client displays them and sends back responses keyed-in by the user. Used to provide one-time password authentication such as S/Key or SecurID.
* **The connection layer**: This layer defines the concept of channels, channel requests and global requests using which SSH services are provided. A single SSH connection can host multiple channels simultaneously, each transferring data in both directions. Channel requests are used to relay out-of-band channel-specific data, such as the changed size of a terminal window or the exit code of a server-side process. Additionally, each channel performs its own flow control using the receive window size. The SSH client requests a server-side port to be forwarded using a global request. Standard channel types include:
    * **shell** for terminal shells, SFTP and exec requests (including SCP transfers)
    * **direct-tcpip** for client-to-server forwarded connections
    * **forwarded-tcpip** for server-to-client forwarded connections

The SSHFP DNS record provides the public host key fingerprints in order to aid in verifying the authenticity of the host.

#### Tips for Securing `SSHD_config`

* **TIPs to securing SSHD_config file**, default values for certain configuration options in OpenSSH are quite restrictive....note that keywords are case-insensitive and arguments are case-sensitive
* Change Default port 22, remember to change the firewall to allow incoming connections on the server to this port #, as well as configuring the remote login to use same port# whilst starting connections\*\*\*\*\*\*\*
    * `netstat -aep | grep ':\*'` — >LINUX
    * `sudo lsof -i -P | grep -i "listen"` —>MacOS
* Add SSH protocol version to 2. `[Protocol 2]`
* Disable Remote root login `[PermitRootLogin no]`
* `ChallengeResponseAuthentication no && HostBasedAuthentication no && PasswordAuthentication no && Pluggable Authentication Modules [UsePAM yes]`
* `PermitEmptyPasswords no`
* `AllowTcpForwarding no && AllowStreamLocalForwarding no && GatewayPorts no && PermitTunnel no`
* `LoginGraceTime` should be set to lowest amount in secs
* `LogLevel VERBOSE` —> This way, the key fingerprint for any SSH key used for login is logged. No longer needed therefore `SyslogFacility AUTH && LogLevel INFO`
* `ListenAddress host|IPv4_addr|IPv6_addr` or `ListenAddress host|IPv4_addr:port` or `ListenAddress [host|IPv6_addr]:port`
* Key exchange algorithms are selected by the `KexAlgorithms` option. We recommend `ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group14-sha1,diffie-hellman-group-exchange-sha256`
* Message authentication code algorithms are configured using the `MACs` option. A good value is `hmac-sha2-256,hmac-sha2-512`
* COMBO `[Ciphers aes128-ctr,aes192-ctr,aes256-ctr HostKeyAlgorithms ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,ssh-dss KexAlgorithms ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2- nistp521,diffie-hellman-group14-sha1,diffie-hellman-group-exchange-sha256 MACs hmac-sha2-256,hmac-sha2-512,hmac-sha1]`


### SOCKS Protocol

* SOCKS is an Internet protocol that exchanges network packets between a client and server through a proxy server. SOCKS5 optionally provides authentication so only authorized users may access a server. Practically, a SOCKS server proxies TCP connections to an arbitrary IP address, and provides a means for UDP packets to be forwarded.


### File Transfer Protocol (FTP)

* FTP- The File Transfer Protocol (FTP) is a standard communication protocol used for the transfer of computer files from a server to a client on a computer network. FTP is built on a client–server model architecture using separate command control and data connections between the client and the server Modern implementations of FTP can include encryption as well. FTP may run in active or passive mode, which determines how the data connection is established. In both cases, the client creates a TCP control connection from a random, usually an unprivileged, port N to the FTP server command port 21. FTP needs two ports (one for sending and one for receiving) because it was originally designed to operate on Network Control Program (NCP), which was a simplex protocol that utilized two port addresses, establishing two connections, for two-way communications. An odd and an even port were reserved for each application layer application or protocol. The FTP protocol was never altered to only use one port, and continued using two for backwards compatibility.
    * **Syntax**: `FTP URL syntax ftp://[user[:password]@]host[:port]/url-path` (the bracketed parts are optional). Users could connect to the FTP server anonymously if the server is configured to allow it, meaning that we could use it even if we had no valid credentials. If we look back at our nmap scan result, the FTP server is indeed configured to allow anonymous login: If you need a refresher, the `ftp -h` command will help you figure out the available commands for the FTP service on your local host.
    * `ftp-anon: Anonymous FTP login allowed (FTP code 230)` from NMAP SCAN
    * To connect to the remote FTP server, you need to specify the target's IP address (or hostname) The prompt will then ask us for our login credentials, which is where we can fill in the anonymous username. In our case, the FTP server does not request a password, and inputting the anonymous username proves enough for us to receive the 230 code, `Login successful`.
    * For example, the URL `ftp://public.ftp-servers.example.com/mydirectory/myfile.txt` represents the file `myfile.txt` from the directory `mydirectory` on the server `public.ftp-servers.example.com` as an FTP resource. The URL `ftp://user001:secretpassword@private.ftp-servers.example.com/mydirectory/myfile.txt` adds a specification of the username and password that must be used to access this resource.
* FTP is often secured with + ✅SSL/TLS (`Explicit FTPS` is an extension to the FTP standard that allows clients to request FTP sessions to be encrypted. This is done by sending the `"AUTH TLS"` command. The server has the option of allowing or denying connections that do not request TLS.) or entirely replaced by ✅SSH/Secure File Transfer Protocol (`SFTP` is a network protocol that provides file access, file transfer, and file management over any reliable data stream has a similar command set for users, but uses the Secure Shell protocol (SSH) to transfer files. Unlike FTP, it encrypts both commands and data, preventing passwords and sensitive information from being transmitted openly over the network.) This protocol assumes that it is run over a secure channel, such as SSH, that the server has already authenticated the client, and that the identity of the client user is available to the protocol. It cannot interoperate with FTP software. `*SFTP is not FTP run over SSH*`
* An SSH server is a software program which uses the secure shell protocol to accept connections from remote computers. SFTP/SCP file transfers and remote terminal connections are popular use cases for an SSH server
* An SSH client is a software program which uses the secure shell protocol to connect to a remote computer.

---

### Remote Synchronization (RSYNC)

Remote Synchronization is an open source utility that provides fast incremental file transfer, Fast and extraordinarily versatile file copying tool. It can copy locally, to/from another host over any remote shell, or to/from a remote rsync daemon. It offers a large number of options that control every aspect of its behavior and permit very flexible specification of the set of files to be copied. It is famous for its delta-transfer algorithm, which reduces the amount of data sent over the network by sending only the differences between the source files and the existing files in the destination. Rsync is widely used for backups and mirroring and as an improved copy command for everyday use. The main concern with FTP is that it is a very old and slow protocol. FTP is a protocol used for copying entire files over the network from a remote server. In many cases there is a need to transfer only some changes made to a few files and not to transfer every file every single time. For these scenarios, the rsync protocol is generally preferred. The changes that need to get transfered are called deltas. Using deltas to update files is an extremely efficient way to reduce the required bandwidth for the transfer as well as the required time for the transfer to complete. It follows directly from the definition of rsync that it's a great tool for creating/maintaining backups and keeping remote machines in sync with each other. Both of these functionalities are commonly implemented in corporate environment. In these environments time is of of the most importance, so rsync is preferred due to the speedup it offers for these tasks.

The main stages of an rsync transfer are the following:
1. rsync establishes a connection to the remote host and spawns another rsync receiver process.
2. The sender and receiver processes compare what files have changed.
3. What has changed gets updated on the remote host.

`rsync OPTION … USER@{TargetHOSTIP}::SRC DEST`
`rsync {target_IP}::public/flag.txt flag.txt`

where SRC is the file or directory (or a list of multiple files and directories) to copy from, DEST is the file or directory to copy to, and square brackets indicate optional parameters.
The `[OPTION]` portion of the syntax, refers to the available options in rsync . The list with all valid options is available over at the official manual page of rsync under the section Options Summary .
The `[USER@]` optional parameter is used when we want to access the the remote machine in an authenticated way. If we don't have any valid credentials at our disposal so we will omit this portion and try an anonymous authentication.
As our first attempt we will try to simply list all the available directories to an anonymous user. Reading through the manual page we can spot the option `--list-only` , which according to the definition is used to "list the files instead of copying them" ->> `rsync --list-only {target_IP}::`

### Other Relevant Protocols & Concepts

* **✔️Port 135: RPC**
    * The Remote Procedure Call (RPC) service supports communication between Windows applications.
    * Specifically, the service implements the RPC protocol — a low-level form of inter-process communication where a client process can make requests of a server process.
    * Microsoft’s foundational COM and DCOM technologies are built on top of RPC.
    * The service’s name is RpcSs and it runs inside the shared services host process, `svchost.exe`. This is one of the main processes in any Windows operating system & it should not be terminated.

* **✔️Port 139: NETBIOS**
    * This port is used for NetBIOS. NetBIOS is an acronym for Network Basic Input/Output System.
    * It provides services related to the session layer of the OSI model allowing applications on separate computers to communicate over a local area network.
    * As strictly an API, NetBIOS is not a networking protocol.
    * Older operating systems ran NetBIOS over IEEE 802.2 and IPX/SPX using the NetBIOS Frames (NBF) and NetBIOS over IPX/SPX (NBX) protocols, respectively.
    * In modern networks, NetBIOS normally runs over TCP/IP via the NetBIOS over TCP/IP (NBT) protocol. This results in each computer in the network having both an IP address and a NetBIOS name corresponding to a (possibly different) host name.
    * NetBIOS is also used for identifying system names in TCP/IP(Windows).
    * Simply saying, it is a protocol that allows communication of files and printers through the Session Layer of the OSI Model in a LAN.

* **✔️SMB - Server Message Block Protocol**
    * SMB - Server Message Block Protocol - is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network.
    * Servers make file systems and other resources (printers, Serial Ports between Endpoints, named pipes, APIs) available to clients on the network. Client computers may have their own hard disks, but they also want access to the shared file systems and printers on the servers.
    * The SMB protocol is known as a response-request protocol, meaning that it transmits multiple messages between the client and server to establish a connection.
    * During scanning, we will typically see port 445 TCP open on the target, reserved for the SMB protocol.
    * Usually, SMB runs at the Application or Presentation layers of the OSI model, pictured below. Due to this, it relies on lower-level protocols for transport. The Transport layer protocol that Microsoft SMB Protocol is most often used with is NetBIOS over TCP/IP (NBT). Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP {NBT} as specified in RFC1001 and RFC1002). Microsoft Windows operating systems since Windows 95 have included client and server SMB protocol support.
    * Samba, an open source server that supports the SMB protocol, was released for Unix systems. To access an SMB share, we need a client to access resources on servers (i.e SMBClient). We will be using SMBClient because it's part of the default samba suite.
    * Smbclient will attempt to connect to the remote host and check if there is any authentication required. If there is, it will ask you for a password for your local username. We should take note of this. If we do not specify a specific username to smbclient when attempting to connect to the remote host, it will just use your local machine's username. That is the one you are currently logged into your Virtual Machine with. This is because SMB authentication always requires a username, so by not giving it one explicitly to try to login with, it will just have to pass your current local username to avoid throwing an error with the protocol.
    * In this case, we do not have such credentials, so what we will be trying to perform is any of the following:
        * Guest authentication
        * Anonymous authentication
    * **ADMIN$ Share**: This is a special share that exists on Windows machines used primarily for system administration - allowing system admins to have remote access to every disk volume on the Remote system, typically allowing access to the `C:\Windows` directory on the remote machine. These shares may not be permanently deleted but may be disabled.
    * **IPC$ Share**: This share is used for inter-process communication (IPC), allowing programs running on networked computers to communicate with each other via named pipes and is not part of the file system.
    * **C$**: Administrative share for the `C:\` disk volume. This is where the operating system is hosted - File system of the Windows Machine the SMB server is hosted
    * **WorkShares**: Custom share
    * In the context of Impacket's `psexec.py`, here's what happens:
        * Impacket creates a remote service by uploading a randomly-named executable on the ADMIN$ share on the remote system & then register it as a Windows service.This will result in having an interactive shell available on the remote Windows system via TCP port 445
        * **Connection to IPC$**: The script uses `connectTree('IPC$')` to establish a session for IPC. This connection is crucial for sending commands & managing comms btw the local & remote systems.
        * **Uploading Executable**: While the script connects to the IPC$ for communication purposes, the actual uploading of executables typically involves the ADMIN$ share. This is because ADMIN$ provides access to the system directories where executables can be placed and executed.
        * **Execution as a Service**: Creating and Starting the Service: After uploading the executable to a suitable location (usually via ADMIN$), the next step is to create a service on the remote machine that points to the uploaded executable. This is typically done through Windows Service Control Manager remotely.
        * These functions interact with the SCM (Service Control Manager) to create and start a new service that executes the uploaded file. In summary, while IPC$ is used for initiating the session and sending some types of commands, ADMIN$ is crucial for the actual file upload process because it allows access to system directories.

    * **✔️Telnet**
    * Telnet is an application protocol which allows you, with the use of a telnet client, to connect to and execute commands on a remote machine that's hosting a telnet server.
    * The telnet client will establish a connection with the server. The client will then become a virtual terminal- allowing you to interact with the remote host.
    * The user connects to the server by using the Telnet protocol, which means entering "telnet" into a command prompt. The user then executes commands on the server by using specific Telnet commands in the Telnet prompt.
    * You can connect to a telnet server with the following syntax: `"telnet [ip] [port]"`

    * **✔️NFS**
    * NFS stands for "Network File System" and allows a system to share directories and files with others over a network.
    * By using NFS, users and programs can access files on remote systems almost as if they were local files. It does this by mounting all, or a portion of a file system on a server. The portion of the file system that is mounted can be accessed by clients with whatever privileges are assigned to each file.
    * First, the client will request to mount a directory from a remote host on a local directory just the same way it can mount a physical device. The mount service will then act to connect to the relevant mount daemon using RPC (Remote Procedure Call).
    * The server checks if the user has permission to mount whatever directory has been requested. It will then return a file handle which uniquely identifies each file and directory that is on the server.
    * If someone wants to access a file using NFS, an RPC call is placed to NFSD (the NFS daemon) on the server. This call takes parameters such as:
        * The file handle
        * The name of the file to be accessed
        * The user's, user ID
        * The user's group ID
    * These are used in determining access rights to the specified file. This is what controls user permissions, I.E read and write of files.
    * Open Network Computing Remote Procedure Call (ONC RPC) / Secure RPC is fundamental to the Secure NFS system. The goal of Secure RPC is to build a system that is at minimum as secure as a time-sharing system (one in which all users share a single computer). A time-sharing system authenticates a user through a login password. With data encryption standard (DES) authentication, the same authentication process is completed. Users can log in on any remote computer just as they can on a local terminal, and their login passwords are their passports to network security.
    * Further Reading [https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html](https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html)
    * The first of which is key to interacting with any NFS share from your local machine: `nfs-common`. It is important to have this package installed on any machine that uses NFS, either as client or server. It includes programs such as: `lockd`, `statd`, `showmount`, `nfsstat`, `gssd`, `idmapd` and `mount.nfs`. [https://www.kali.org/tools/nfs-utils/#nfs-common](https://www.kali.org/tools/nfs-utils/#nfs-common)

    ### End-to-End Principle Governing TCP/Internet Protocol Suite

* The fundamental notion behind the end-to-end principle is that for two processes communicating with each other via some communication means, the reliability obtained from that means(protocol) cannot be expected to be perfectly aligned with the reliability requirements of the protocol processes.

### PDU Terminology

* The term TCP `*packet*` appears in both informal and formal usage, whereas in more precise terminology
* `*segment*` refers to the TCP layer protocol data unit (PDU)
* `*datagram*` refers to the UDP layer protocol data unit (PDU)
* `*datagram*` to the IP protocol data unit (PDU)
* `*frame*` to the data link layer protocol data unit (PDU)

### Network Node and Host Definitions

* The word end-user directly relates & interacts with a computer(end-system/end-station) connected to a computer network providing information or services.
* End-systems include devices that the end-user doesn’t interact directly with, I.e mail servers, web servers, database servers, internet of things(IOT) devices-digital cameras, TV sets, etc.
* Nodes that send and receive information are referred to as End systems or as Host nodes. This type of node includes computers, laptops, servers, Voice over IP (VoIP) phones, smartphones, and printers.
* A Node that provides only a "forwarding function" is referred to as an intermediate system or infrastructure node.
* A NODE is either a redistribution point or a communication endpoint. The definition of a node depends on the network and protocol layer referred to. A physical network node is an electronic device that is attached to a network, and is capable of creating, receiving, or transmitting information over a communication channel hence referred to as a HOST.
* A network HOST is a computer or other device connected to a computer network. A host may work as a server offering information resources, services, and applications to users or other hosts on the network. Hosts are assigned at least one network address.
* `“Every network host is a node, but not every network node is a host”`
* A `“HOST is a NODE”` that participates in user applications, either as a server, client, or both. A server is a type of host that offers resources to the other hosts. Typically a server accepts connections from clients who request a service function.

### What is a Firewall?

A firewall is a tool designed to intercept and assess incoming and outgoing packets. Depending on the types of devices we are protecting, and what we are protecting them from, we may choose to use different types of firewalls. They work mostly on the Network & Internet-Protocol Layer. Firewalls implement Network Address Translation.

#### Firewall Types

* **✔️Packet-Filtering Firewalls**
    * do not check content, but they can inspect and filter on information like:
    * Source IP, Destination IP, Destination port numbers on a packet as well as the protocols used.
    * They are best suited Within your network to control traffic from internal network to internal network
    * For example, within an organization, we can use a packet-filtering firewall to prevent the flow of packets between different parts of the network. Project([https://www.codecademy.com/courses/introduction-to-cybersecurity/articles/project-firewall](https://www.codecademy.com/courses/introduction-to-cybersecurity/articles/project-firewall))

* **✔️Circuit-Level Firewalls**
    * reviews content related to individual sessions.
    * Ensure that sessions are properly configured & Identify illegitimate connections
    * While these may help to prevent malformed sessions from connecting, they might still allow certain threats to pass through. For example, a valid session transferring malware could be allowed as long as the session is established properly.
    * They can be used to implement virtual private networks VPN.

* **✔️Stateful Inspection Firewalls**
    * maintains a table of active sessions, similar to circuit-level firewalls.
    * They Are able to limit activity based on source and destination data, like packet-filtering firewalls
    * Attempt to review the contents of active sessions, dropping packets that don’t comply with the logged session. It’s goal is to identify hosts that represent a threat by accumulating evidence against them, if the negative evidence against a host exceeds a threshold established by the network firewall’s security policy the host can be blocked
    * Firewall uses stateful rules that drop unexpected packets. This feature was initially found mostly on high-end firewalls, though it has become much more common over the years. The Linux Netfilter/iptables system supports this through the `--state` option, which categorizes packets based on connection state as described in the following man page excerpt:
        * Possible states are `INVALID` meaning that the packet is associated with no known connection, `ESTABLISHED` meaning that the packet is associated with a connection which has seen packets in both directions, `NEW` meaning that the packet has started a new connection, or otherwise associated with a connection which has not seen packets in both directions, and `RELATED` meaning that the packet is starting a new connection, but is associated with an existing connection, such as an FTP data transfer, or an ICMP error.

* **✔️Application Firewalls**
    * with the use of pattern-matching, application firewalls can detect and block much more sophisticated attacks.
    * Utilize application-specific rules to identify malicious traffic
    * The firewall is represented through a wall that lets in good certain devices or requests while blocking the bad ones. In another example, an HTTP request may be passing data to a web server. While the request’s IP and session information may appear safe, content sent in individual HTTP requests could pose a danger to the receiving web servers. An application firewall could identify malicious content in HTTP requests and block the content.

* **✔️Next-Generation Level Firewalls (NGLF)**
    * are considered the most advanced firewalls, they will also identify additional malicious content in real-time.
    * Through the use artificial intelligence, or even global networks, to identify new and emerging threats in real-time

---

# CHAPTER 6: VOICE AND VIDEO PROTOCOLS

Voice over IP (VoIP) and Video Teleconferencing have become standard communication methods. Many networks are upgrading from legacy voice services to IP-based protocols and products. Voice and video communication over IP networks has become ubiquitous, replacing traditional circuit-switched telephony and enabling rich multimedia experiences. These services rely on a suite of specialized protocols to ensure real-time delivery, quality of service (QoS), and session management. This chapter explores the foundational protocols that enable voice (VoIP) and video communication across IP networks.
Voice over IP (VoIP) Fundamentals

Voice over IP (VoIP) is a methodology and group of technologies for the delivery of voice communications and multimedia sessions over Internet Protocol (IP) networks, such as the Internet. It functions by converting analog audio signals into digital packets that are then transmitted over the network.  

Key Components of a VoIP System:
    IP Phones: Devices that convert voice into IP packets and vice-versa. Can be hardware or software (softphones).
    VoIP Gateways: Connect traditional PSTN (Public Switched Telephone Network) lines to IP networks, allowing calls between the two.
    Call Processors/IP PBX (Private Branch Exchange): Manage call setup, routing, and features like voicemail, conferencing, etc.
    Codecs: Algorithms used to compress and decompress digital audio signals. Examples include G.711 (PCMU/PCMA), G.729, G.722.

## Legacy Voice Services

Legacy voice services traditionally use the **Public Switched Telephone Network (PSTN)**. A common residential telephone installation would be serviced by a simple box providing a single analog interface to the local exchange. This analog interface is known as **Plain Old Telephone Service (POTS)**, where each line provides a single channel for incoming and outgoing calls.

For businesses requiring many voice lines, a **digital trunk line** is used, often referred to as **Time Division Multiplexing (TDM)**. A TDM circuit can multiplex separate voice data channels for transmission over a single cable.

A **Private Branch Exchange (PBX)** is an automated switchboard providing a single connection point for an organization's voice lines. A TDM-based PBX connects to telecommunication carriers over a digital trunk line, which supports multiple channels (e.g., for multiple concurrent calls). This PBX allows for the configuration of the internal phone system to direct and route calls to local extensions and provides other telephony features such as call waiting, forwarding, music on hold, and voicemail.

## VoIP-Enabled PBX

A **VoIP-enabled PBX** replaces the TDM-based PBX. It establishes connections between local VoIP endpoints, with data transmitted over the local Ethernet network. A VoIP PBX can also route incoming/outgoing calls to and from an external network. This might involve calls between internal & external VoIP endpoints or with callers on the voice telephone network. VoIP-based PBXs also support traditional telephony features.

A VoIP PBX would normally be placed at the network edge and protected by a **firewall**. Internal clients connect to the PBX over Ethernet data cabling, using IP at network layers for addressing. The VoIP PBX uses the organization's Internet link to connect to a VoIP service provider, which facilitates inbound and outbound calling.


## VoIP Protocols

VoIP protocols are designed to support real-time services and cover one or more of the following functions:

* **Session Control:** Used to establish, manage, and disassociate communication sessions. This handles tasks such as user discovery, availability advertising, negotiation of session parameters, and session termination.
* **Data Transport:** Handles the delivery of the actual video or voice information transmission.
* **Quality of Service (QoS):** Provides information about the connection to a QoS system, which in turn ensures communications are problem-free (e.g., addressing dropped packets, delay, or jitter).

### 1. Session Initiation Protocol (SIP)

**SIP Endpoints** are the end-user devices, also known as **User Agents**, such as IP-enabled handsets or client-server web conferencing software. Each device, conference, or telephony user is assigned a unique SIP Address, known as a **SIP Uniform Resource Indicator (URI)**. Examples include `sip:jamie@support.com` or `sip:2622136227@support.com`. There is also a **`tel:` URI Scheme** allowing SIP Endpoints to dial a landline or cell phone. A `tel:` URI can either use the global telephone format or a local format for internal extensions.

SIP runs over UDP or TCP ports **5060** (unsecured) and **5061** (SIP-TLS). It has its own reliability & retransmission mechanisms, benefiting most from the lower overhead, reduced latency, and jitter of UDP. SIP primarily provides session management.
Key SIP Components/Roles:

    User Agent (UA): Endpoints that initiate or terminate calls. Divided into:
        User Agent Client (UAC): Initiates SIP requests.
        User Agent Server (UAS): Receives SIP requests and sends responses.
    SIP Proxy Server: Intermediary entities that receive SIP requests, forward them to the next hop, and return responses. Can also handle routing decisions.
    SIP Registrar Server: Accepts REGISTER requests from UAs to record their current location.
    SIP Redirect Server: Accepts a SIP request, maps the address of the called party to zero or more new addresses, and returns these addresses to the client. The client then contacts the new address directly.

Basic SIP Call Flow (Simplified):

    INVITE: UAC sends INVITE to UAS (via proxy) to initiate a call.
    100 Trying: Proxy acknowledges INVITE.
    180 Ringing: UAS informs UAC that the called party is being alerted.
    200 OK: Called party answers, UAS sends 200 OK.
    ACK: UAC acknowledges 200 OK, call is established.
    RTP: Media (voice/video) flows directly between UAs using RTP.
    BYE: Either UA sends BYE to terminate call.
    200 OK: Receiver acknowledges BYE.


### 2.  H.323 Protocol Suite

H.323 is an ITU-T recommendation that defines protocols for providing audio-visual communication sessions on any packet network. While less common for new deployments compared to SIP, it is still used in many legacy enterprise and service provider networks, particularly for video conferencing systems. H.323 is a binary, complex protocol that defines various components and their interactions.

**Key H.323 Components/Roles:**

* **Terminals:** Endpoints (e.g., video conferencing units, IP phones) that provide real-time, two-way communication.
* **Gateways:** Devices that connect H.323 networks to other networks, such as the PSTN or other IP networks using different protocols. They perform protocol translation and media conversion.
* **Gatekeepers:** Optional but highly recommended components that act as the central point for H.323 calls within their zone. They provide call control, address translation, bandwidth management, and admission control.
* **Multipoint Control Unit (MCU):** Supports multipoint conferences, allowing three or more H.323 terminals to participate in a conference.

**H.323 vs. SIP (Key Differences):**

| Feature         | H.323                                     | SIP                                       |
| :-------------- | :---------------------------------------- | :---------------------------------------- |
| **Origin** | ITU-T (Telecommunications Focus)          | IETF (Internet Focus)                     |
| **Complexity** | More complex, binary, monolithic          | Simpler, text-based, modular              |
| **Architecture**| Gatekeeper-centric, tightly coupled       | Client-server, peer-to-peer, loosely coupled |
| **Ports** | Uses multiple well-defined ports          | Primarily UDP/5060, TCP/5060              |
| **Scalability** | Less scalable in large, distributed environments | Highly scalable                           |
| **Extensibility**| Less flexible, harder to extend          | Highly extensible, easy to adapt         |
| **Legacy Use** | Common in legacy video conferencing, PSTN gateways | Dominant for modern VoIP/UC deployments   |


### 3. Real-time Transport Protocol (RTP) and RTP Control Protocol (RTCP)

RTP and RTCP are fundamental protocols for delivering real-time voice and video data over IP networks once a session has been established by signaling protocols like SIP or H.323.

* **Real-time Transport Protocol (RTP):**
    * **Function:** Carries the actual audio and video data payload.
    * **Operation:** Provides sequence numbering, timestamps, and payload type identification to enable real-time delivery and reconstruction of media streams.
    * **Transport:** Typically runs over UDP (User Datagram Protocol) for speed, as retransmissions are generally not practical for real-time media.
    * **Characteristics:** Does not guarantee quality of service (QoS) itself, but provides information for QoS mechanisms.
* **RTP Control Protocol (RTCP):**
    * **Function:** Works in conjunction with RTP to provide feedback on the quality of data distribution.
    * **Operation:** Sends control packets periodically to all participants in a session, reporting on reception quality (jitter, packet loss, round-trip delay).
    * **Use:** Enables adaptive applications to adjust transmission rates or codecs based on network conditions, and for diagnostic purposes.
    * **Characteristics:** Does not carry media data itself.

### Video Protocols and Codecs

Video communication over IP involves specific protocols and codecs for efficient compression, transmission, and rendering of video streams.

* **Video Codecs:**
    * **Function:** Algorithms that compress raw video data for transmission and decompress it for playback. High compression ratios are crucial due to large video data sizes.
    * **Examples:**
        * **H.264 (AVC - Advanced Video Coding):** Widely used for streaming, video conferencing, and broadcast. Offers good compression efficiency.
        * **H.265 (HEVC - High Efficiency Video Coding):** Successor to H.264, offering significantly better compression efficiency (up to 50% for same quality). Used for 4K/UHD video.
        * **VP8/VP9:** Open, royalty-free video compression formats developed by Google. Used in WebM and other web-based video.
        * **AV1:** A new, royalty-free video coding format designed to be competitive with H.265, backed by Google, Amazon, Netflix, etc.
* **Real-time Messaging Protocol (RTMP):**
    * **Function:** Developed by Adobe for streaming audio, video, and data over the Internet.
    * **Operation:** Originally designed for Flash Player, it's still used in some live streaming workflows (e.g., from encoders to streaming platforms).
    * **Characteristics:** Typically runs over TCP.
* **WebRTC (Web Real-Time Communication):**
    * **Function:** A free, open-source project that provides web browsers and mobile applications with Real-Time Communications (RTC) capabilities via simple APIs.
    * **Operation:** Enables peer-to-peer voice, video, and data communication directly within a browser without plugins. Leverages RTP for media transport, and ICE, STUN, TURN for NAT traversal.

---

## VoIP Endpoint Implementation

VoIP/SIP Endpoints can be implemented as software (softphones) or as dedicated hardware handsets.

* **VLAN Tagging:** VoIP phones use VLAN tagging to ensure that SIP control and RTP protocol traffic can be segregated from normal data traffic. Since both devices (PC & VoIP Phones) may share the same physical network drop, data traffic is distinguished from voice traffic by configuring separate VLAN IDs.
* **Power over Ethernet (PoE):** Handsets can use PoE to avoid separate power cabling or batteries.
* **Secure Connection:** Connection security for VoIP works similarly to HTTPS. To initiate a call, **Secure SIP (SIPS)** uses digital certificates and master keys to authenticate endpoints and establish SSH/TLS tunnels.
* **Call Quality Test:** Most service providers have test numbers to verify basic connectivity and perform an echo test call, which replays a recorded message to confirm voice quality.

---

## Voice Gateways

SIP Endpoints can establish communications directly in a peer-to-peer architecture. However, it's more typical to use intermediary servers, directory servers, and **VoIP Gateways**.
A **Voice Gateway** is a component that translates between a VoIP system and legacy voice equipment and networks (e.g., POTS lines, TDM PBXs).

### Voice Gateway Deployment Scenarios

1.  **Hybrid/Hardware-based VoIP PBX Integration (Type 1):**
    * A hybrid or hardware-based VoIP PBX can include a plug-in or integrated VoIP gateway. These gateways come in both **analog** and **digital** types to match the type of incoming landline. An analog version is sometimes called a **Foreign Exchange Office Gateway (FXO Gateway)**.
    * **Diagram:** External Analog or Digital Telephone Network <---> VoIP Gateway (integrated or separate) <---> VoIP PBX <---> Ethernet Cabling Connections <---> VoIP Endpoints (internal).

2.  **Legacy System Connecting to VoIP Service Provider (Type 2):**
    * A VoIP gateway can also be deployed to allow legacy analog/digital internal phone systems to use a VoIP service provider to place calls.
    * In this setup, local/low-rate national calls might be placed directly via the legacy PBX, while international calls (which would otherwise incur high charges if placed directly) are routed via the VoIP service provider.
    * **Diagram:** Legacy Handsets/Fax/TDM PBX <---> Analog/Digital Cabling <---> VoIP Gateway <---> Edge Router/Firewall <---> Internet Link <---> ISP's Telephone Network (VoIP Service Provider).

3.  **Connecting POTS Handsets to VoIP PBX (Type 3):**
    * A VoIP gateway/adapter can be used to connect POTS handsets or fax machines to a VoIP PBX. This type of device is also called a **Foreign Exchange Subscriber (FXS) gateway**.
    * **Diagram:** Legacy Handsets/Fax <---> Voice Legacy VoIP Gateway <---> Ethernet Cabling <---> VoIP PBX <---> Internet Link <---> VoIP Service Provider.

In essence, a VoIP Gateway is a component in a network that allows calls to be placed to and from voice telephony networks (PSTN) and packetized telephony networks (VoIP).

### Best Practices for VoIP Deployment

* Deploy VoIP/Hybrid PBXs with Voice Gateways to local and perimeter networks to support both legacy and packetized telephony.
* Configure VoIP endpoints to use **Secure SIP (TCP/5061)** for session control and **RTP/RTCP** for data transfer.
* Prioritize VoIP traffic using QoS mechanisms to ensure call quality and minimize latency and jitter.

---


# Chapter 7: CABLING STANDARDS (ETHERNET && FIBRE)

Cabling is the backbone of any network infrastructure, providing the physical medium for data transmission. Proper cabling ensures reliable and high-performance network operations. This chapter delves into the various standards and types of cabling, focusing on Ethernet (copper) and Fibre Optic cabling. Ethernet cabling, primarily copper-based, is widely used for local area networks (LANs) due to its cost-effectiveness and ease of installation. Different categories of Ethernet cables support varying speeds and distances.

## Ethernet & Fibre Optic Cabling

**IEEE 802.3 Standards** are the most important Ethernet specifications for effectively deploying wired LANs. Ethernet dominates the wired LAN market due to ease of installation and upgradability.

All Networking Signals use EM Radiation of one type or another, such as:
* Electric Current (Copper Cabling)
* Infrared Light (Fibre Optic)
* Radio Waves (Wireless)

Taking advantage of wave characteristics, signals are transmitted over the wave by modulation & encoding schemes. An example of encoding is transitioning between low to high voltage states in an electrical circuit, which in turn encodes digital info as 0, 1 data bits.


### Copper vs. Fibre Optic

**Copper Cable** transmits Electrical Signals using low voltage circuits between connected nodes in a circuit. It suffers from high **Attenuation** (i.e., signals lose strength over long distances).

**Fibre Optics**, on the other hand, carries very high frequency radiation in the Infrared light part of the EM spectrum. The light signals are not susceptible to outside noise interference and are less affected by attenuation, supporting higher bandwidth over longer links than copper cabling.


### Ethernet Naming Conventions

**`XGBase-Y`**

* `X`: Bit Rate in Mbps or Gbps (e.g., 10, 100, 1000, 10G, 40G).
* `Base`: Baseband (all Ethernet transmission is Baseband, meaning the entire frequency range is used for one signal at a time, versus broadband which divides the frequency).
* `Broadband`: Multiple frequencies sharing the same medium of connectivity. Common in Fiber Optic.
* `Y`: Media type designator (e.g., `T` for Twisted Pair, `SX` for Short wavelength multimode fiber, `LX` for Long wavelength multimode fiber).


### Ethernet Standards & Deployment

* **10 Base-T:** Standard dates from 1990. Unlikely to be deployed in modern LANs. Mostly used in SOHO networks and for maintaining legacy networks.
* **100 Base-Tx (Fast Ethernet):** Mostly used in SOHO Networks and for maintaining legacy networks.
* **Gigabit Ethernet (1000Base-T):** Used in mainstream offices to connect common workstations.
* **10G/40G Base-T:** Not really deployed in access networks as the cost for compatible network adapters and switch transceiver modules is high. Used in conglomerates, business centers, data centers, due to its high throughput.

### Bandwidth

**Bandwidth** refers to the frequency range measured in cycles per second or Hertz (Hz). In networking, this means the amount of data transferred, measured in bits per second (bps). For a signal with 100MHz frequency bandwidth, it can transfer much more than 100 Mbps. Due to the higher frequency required, sometimes this can cause interference. Therefore, shielding is required for longer distance Fibre Optic runs.

### Media Access Control and Collision Domains

Since Ethernet is a multiple access area network (i.e., available communication capacity is shared between nodes connected to the same medium of transmission), the **Media Access Control (MAC)** refers to the method a network technology uses to determine when nodes communicate in shared media and to deal with possible issues of two devices communicating simultaneously.

Each network node connected to the same media is said to be in the **Same Collision Domain**.

### CSMA/CD

**Carrier Sense Multiple Access with Collision Detection (CSMA/CD)** is a protocol governing media access. A **collision** is a state when signals are present in an interface's transmit and receive lines simultaneously. On detecting a collision, the node broadcasts a Jam Signal. Every other node attempts a Backed-off wait for a random period before attempting to retransmit again. This mechanism means only half-duplex transmission is possible (Transmit OR Receive, but NOT BOTH simultaneously).


### Twisted Pair Cabling

* **Unshielded Twisted Pair (UTP):** Pairs of wires are twisted together to form a balanced circuit, carrying the same signals but with different polarity. The wires are twisted at different rates to reduce external interference and crosstalk.
* **Shielded Twisted Pair (STP) / Screened Twisted Pair (SSTP):** Less susceptible to interference & crosstalk. Used mostly in environments with high levels of interference.
    * **F/UTP (Foiled/Unshielded Twisted Pair):** Overall foil shield, unshielded twisted pairs.
    * **U/FTP (Unshielded/Foiled Twisted Pair):** Unshielded overall, foiled twisted pairs.
    * **S/FTP (Shielded/Foiled Twisted Pair):** Shielded overall, foiled twisted pairs.
    * **F/FTP (Foiled/Foiled Twisted Pair):** Overall foil shield, foiled twisted pairs.

Using screened or shielded cable means that you must also use screened or shielded connectors. Their elements should not be mixed with unscreened/unshielded elements.

---

### Twisted Pair Connectors

* **F-Connector (Coaxial):** Used in cable television, commonly with RG-6 cable.
* **RJ-45 (8P8C - 8 Position, 8 Conductor):** Registered Jack. Supplied in pairs of 4 (8 wires). Most commonly installed type of wiring for data.
* **RJ-25 (6P6C):** 6 potential ports of contact, supplied with 3 pairs (6 wires).
* **RJ-14 (6P4C):** 6 potential ports of contact, supplied with 2 pairs (4 wires). Used in dual-line telephone/DSL.
* **RJ-11 (6P2C):** 6 potential ports of contact, supplied with 1 pair (2 wires). Used in single-line telephone/DSL.
* **GG45 / TERA:** Used in data centers, for higher performance.

---

### Cabling Fire Safety Ratings

A **Plenum space** is an air-handling space in a building (e.g., false ceilings, raised floors). This space can be used for telecommunications cabling. Therefore, building regulations demand the use of fire-retardant **Plenum Cabling** in such places. Plenum cables must not emit large amounts of smoke when burned, be self-extinguishing, and meet other fire safety standards. (Compare with General Purpose (non-plenum) CM/CMR/CMP cables).

**Riser Cables** are passed through floors, in conduits or lift shafts.

---

### Coaxial & Twin-Axial Cable & Connectors

**Coaxial Cable** is categorized using Radio Grade (RG) Standards, which represent the thickness of the core conductor and the cable's characteristics. Coaxial means a cable made of 2 conductors that share the same axis. The core conductor is made of a copper core (solid or stranded, not twisted) and enclosed by plastic insulation. A wire mesh (second conductor) serves as both shielding from EMI and as a ground (earth) surrounding the insulating material. Coax is usually terminated using BNC connectors, securely screwed or crimped.

**Twin-Axial (Twinax)** is similar to coax but contains 2 twin conductors. Mostly used in data centers (10GbE and 40GbE) interconnects up to 5m for passive cable types and 10m for active cable types. Terminated using SFP+ Direct Attach Copper (DAC) and QSFP+ DAC transceivers.

**American Wire Gauge (AWG)** is a measure of wire thickness. Increasing AWG number represents thinner wire.

---

### Deploying Ethernet Cabling (ANSI/TIA/EIA 568 - Structured Cabling Standards)

These standards define classes of networking infrastructure.
* **International ISO/IEC 11801:** International cabling standards.
* **Telecommunications Industry Association (TIA) standards:** US-centric cabling standards (e.g., ANSI/TIA/EIA 568).
Structured cabling is a scheme for deploying Ethernet cabling.

* **Work Area:** User space for equipment connected to the network, usually via a wall outlet.
* **Horizontal Cabling:** Connects user work areas to the nearest **Horizontal Cross-Connect (HCC)** / **Telecommunications Room (TR)**. Referred to as a "distribution frame." Consists of cabling from a single floor, made up of cables run horizontally through wall ducts.
* **Backbone Cabling:** Connecting Horizontal Cross-connects via Intermediate Cross-Connects (ICCs). Inside risers, elevator shafts, HVAC spaces referred to as Vertical cross-connects, running up and down between floors.
* **Telecommunications Room (TR):** Houses HCCs, essentially a termination point for the Horizontal Cabling along with a connection to backbone cabling.
* **Equipment Room:** Houses the main intermediate cross-connects, houses complex equipment such as switches, routers & modems.
* **Entrance Facilities / DEMARC POINT:** Required for the access provider's network and for inter-building communications, marking the point at which external cabling (outside plant) is joined to internal premises cabling.

---

### Cable Management Techniques & Tools for Ethernet (Copper Cabling)

These techniques ensure that cabling is reliable and easy to maintain.

Copper wire is terminated using a distribution frame or **Punchdown Block**. A punchdown block comprises a large number of Insulation-Displacement Connections (IDCs).

1.  **66 Block:** Used in distribution frames to terminate telephone cabling and legacy data applications (Pre-Cat 5).
    * *A Private Branch Exchange (PBX) is a telephone system serving local extensions of an office.*
2.  **110 Block:** A distribution frame supporting 100 MHz operation; Cat 5 and better.
3.  **BIX (NORTEL) & KRONE:** Other types of distribution frames.
4.  **Patch Panel / Patch Bay:** NOT a punchdown block, but a "forwarding" frame.

#### Patch Panel / Patch Bay

In data networks, numerous **MACs (Moves, Adds, Changes)** would require reterminating the wiring. A **Patch Panel** is a type of distribution block with IDCs on one side & pre-terminated RJ-45 modular ports on the other, allowing incoming & outgoing connections to be reconfigured by changing the Patch Cable Connections, which is much simpler than reterminating punchdown blocks.

The structured cabling forming a backbone is terminated at the back of the patch panel on the IDCs. An RJ-45 patch cord is used to connect the port to another network port, typically a switch port housed in the same rack.

Fixed cable is terminated using a **Punchdown Tool**, which fixes conductors into an IDC. Different formats for IDCs (66, 110, BIX & KRONE) all require different cutting blades. Blades are double-sided: one side pushes the core into the terminal while the other side cuts excess.

A **Patch Cord** is created using a **Cable Crimper**, which fixes a plug to a cable. The boots are specific to the type of connector and cable, though some may have modular dies to support a range of RJ type plugs.

You must untwist the ends of the wire pairs (no more than 0.375") and place them into the connector die in the correct order for the wiring configuration (T568A or T568B) you want. For shielded/screened cable, termination must be made to shielded RJ-45 or modular plugs. A shielded modular plug has a metal housing and is not terminated using a standard cable crimper.

This entire note is Cable Management for Copper Cabling Ethernet. Next, we will look into Fiber Distribution Panels.

---

### Wavelength Division Multiplexing (WDM)

**Wavelength Division Multiplexing (WDM)** is a means of using a single fiber strand to transmit and/or receive more than one channel at a time. This involves Optical Add/Drop Multiplexers (OADMs) which can insert or remove signals for a given wavelength. **Wavelength Division Multiplexing (WDM)** helps enable bi-directional communication over a single strand of fiber by using different wavelengths for each channel. This is achieved by combining multiple optical carriers into a single fiber.

* **Bi-directional Wavelength Division Multiplexing (Bidi WDM):** Transceivers support transmit and receive signals over the same strand of fiber. They must be installed in opposite pairs. For example, a downstream transceiver would use 1490nm for transmit (Tx) and 1310nm for receive (Rx), while the upstream would use 1310nm for Tx and 1490nm for Rx. They are also documented in Ethernet standards like 1000Base-BX or 10GBase-BX.
* **Coarse Wavelength Division Multiplexing (CWDM):** Supports up to 16 wavelengths and is typically used to deploy 4/8 bidirectional channels over a single strand of fiber.
* **Dense Wavelength Division Multiplexing (DWDM):** Provides greater numbers of channels (20, 40, 80, 160). This means less spacing between each channel and requires more precise and expensive optics.
    * CWDM & DWDM Transceivers support multi-channel 1G, 10G, 40G, 100G.
    * Each Transceiver in a Point-to-Point WDM Topology is cabled to a multiplexer/demultiplexer (Mux/Demux).

---

### Twisted Pair Copper Cabling

**Twisted Pairs** consist of two wires with equal and opposite signals (Transmit +, Transmit -, Receive +, Receive -). The twist provides advantages like **limited interference**. The pairs within the same cable have different twist rates, which helps in signal reconstruction by reducing crosstalk.

#### Ethernet Standards and Copper Cable Categories

#### Common Ethernet Cable Categories and Performance

| Category | Max Speed  | Max Distance (100Mbps) | Max Distance (1Gbps) | Max Distance (10Gbps) | Shielding   | Notes                                                        |
| :------- | :--------- | :--------------------- | :------------------- | :-------------------- | :---------- | :----------------------------------------------------------- |
| Cat3     | 10 Mbps    | 100 meters             | N/A                  | N/A                   | UTP         | Older voice and 10BASE-T data networks.                      |
| Cat5     | 100 Mbps   | 100 meters             | N/A                  | N/A                   | UTP         | Common for 100BASE-TX Ethernet.                              |
| Cat5e    | 1 Gbps     | 100 meters             | 100 meters           | N/A                   | UTP         | Enhanced for Gigabit Ethernet, reduced crosstalk.            |
| Cat6     | 1 Gbps     | 100 meters             | 100 meters           | 55 meters             | UTP/STP     | Better performance at higher bandwidths, often with internal separator. |
| Cat6a    | 10 Gbps    | N/A                    | N/A                  | 100 meters            | UTP/STP     | Enhanced for 10 Gigabit Ethernet over full distance.         |
| Cat7     | 10 Gbps    | N/A                    | N/A                  | 100 meters            | S/FTP       | Designed for 10 Gigabit Ethernet, individually shielded pairs. |
| Cat8     | 25/40 Gbps | N/A                    | N/A                  | 30 meters             | F/UTP, S/FTP | Designed for 25GBASE-T and 40GBASE-T, typically for data centers. |

**Note:**
* **10 Base-T (Category 3):** 100 meters max. This is a **legacy implementation** and only supports hubs.
* **100 Base-TX (Category 5):** 100 meters max. Commonly referred to as "Fast Ethernet," mostly for SOHO networks. Supports switches.
* **1000 Base-T (Gigabit Ethernet):** Uses 4 pairs of balanced twisted pairs. Deprecated for hubs, primarily used with switches. Mainstream choice for new installations.
* **10G Base-T (10 Gigabit Ethernet):** Uses higher frequencies (500MHz vs 125MHz) compared to 1 Gigabit Ethernet.

---

## Fiber Optic Cabling

**Optical Fiber** transmits data using light signals. Fiber Optic Cabling supports higher bandwidth over long distances than copper. Fiber Optic signals use Infrared pulses, which are not susceptible to interference or attenuation.

Both the **Cladding** and **Core** are made up of similar material, however, with different refractive indexes, so as to create a boundary that causes light to bounce back into the core via total internal reflection. The surrounding **buffer** is an outer protective plastic coating.

Each optic strand can only transfer light in a single direction at a time. Therefore, multiple strands are bundled together for transmission & reception simultaneously. Fiber Optic Cables are specified using the core/cladding size in microns, the composition (either Fiberglass rods or Kevlar plastic), and the mode of operation.

### Fiber Modes

* **Single Mode Fiber (SMF):** Characterized by a small core (5-10 microns), long wavelength laser light (1310nm → 1550nm). They support distances in cable runs of many kilometers and speeds up to 100 Gbps. Expensive to deploy.
    * **OS1 Grade:** For indoor use.
    * **OS2 Grade:** For outdoor deployment.
* **Multimode Fiber (MMF):** Characterized by a larger core (50-62.5 microns), short wavelength light (850nm-1300nm) transmitted in multiple waves of varying length. Doesn't support such high signaling speeds or long distances as SMF.
    * **OM1 (62.5 microns) / OM2 (50 microns):** Cables rated for 1Gbps and use LED light.
    * **OM3 / OM4 (50 micron core):** Designed for use with 850nm VCSEL (Vertical-Cavity Surface-Emitting Laser) lasers, also referred to as Laser Optimized MMF (LOMMF). Not as powerful as solid-state lasers used in SMF.

### Fiber Connector Types

* **ST (Straight Tip):** Uses push & twist locking, mostly for multimode networks.
* **SC (Subscriber Connector):** Uses push/pull design, used in Single or Multimode Gigabit Ethernet.
* **LC (Lucent Connector):** Uses tabbed push/pull design, a small form factor connector widely used in 10GbE and 40GbE.
* **MTRJ (Mechanical Transfer Registered Jack):** Uses a snap-in design for MMF.

Fibre Optics is used in backbone links in campus networks, data centers, and storage area networks due to the increased bandwidth for server interconnections.

---

### Fibre Optic Types

Fibre Optic is divided into Single Mode (SMF) and Multimode (MMF) types. MMF is characterized by the Optical Mode designators (OM1, OM2, OM3, OM4).

* **Single Mode Fiber (SMF):** Simple, single frequency transmitted.
* **Multi-Mode Fiber (MMF):** Multiple different frequency ranges transmitted.

**Comparison:** Fibre gives better upgrade potential in the future, while copper is cheaper to install, and more hosts are installed with network cards supporting copper than fiber.


### Advantages of Optical Fiber

* **No Radio Frequency (RF) Signal:** This makes it very difficult to monitor or tap, enhancing security.
* **Immune to RF Interference:** Light signals are not affected by electromagnetic interference.
* **Signal Slow to Degrade:** Can be transmitted over very long distances without significant loss.

### Fiber Optic Diagram Components

1.  **Core:** The central part where light travels, made of glass or plastic with a high refractive index.
2.  **Cladding:** A thin layer around the core with a lower refractive index, which causes light to reflect back into the core, keeping it contained.
3.  **Buffer Coating:** An outer protective plastic coating providing mechanical protection.

---

#### Common Fibre Optic Connector Types

Different types of connectors are used to terminate fibre optic cables, each with specific applications and advantages.

| Connector Type | Ferrule Size (mm) | Description                                                | Common Use Cases                                 | Notes                                                              |
| :------------- | :---------------- | :--------------------------------------------------------- | :----------------------------------------------- | :----------------------------------------------------------------- |
| **SC (Standard Connector)** | 2.5               | Push-pull latching mechanism, square connector.            | Data communications, telecom, LAN, Fibre Channel | Easy to use, good for high-density patching.                       |
| **LC (Lucent Connector)** | 1.25              | Small form-factor, latching mechanism, often used in duplex. | High-density patches, data centers, SFP/SFP+ transceivers | Half the size of SC, very popular due to small size.                |
| **ST (Straight Tip)** | 2.5               | Bayonet mount, typically used with multi-mode fiber.       | Older networks, campuses, military applications    | Twist-on/off mechanism, common with multi-mode.                     |
| **FC (Ferrule Connector)** | 2.5               | Screw-on locking mechanism, common in single-mode.         | Data communication, telecom, high-vibration environments | Provides high connection strength, often used in industrial settings. |
| **MPO/MTP (Multi-fiber Push-on/pull-off)** | N/A (Multi-fiber) | Multi-fiber connector housing 8, 12, 24, or more fibers.  | Data centers, backbone, high-density environments | Used for parallel optics, requires specialized tools.             |

#### Fibre Optic Cabling Standards (Ethernet over Fibre)

| Standard       | Speed   | Fibre Type             | Max Distance (Typical)              | Notes/Common Use Cases                                                                                                |
| :------------- | :------ | :--------------------- | :---------------------------------- | :-------------------------------------------------------------------------------------------------------------------- |
| **100BASE-FX** | 100 Mbps| Multi-Mode Fibre       | up to 2 km                          |                                                                                                                       |
| **1000BASE-SX** | 1 Gbps  | Multi-Mode Fibre       | up to 550 m                         | (Short Wavelength)                                                                                                    |
| **1000BASE-LX** | 1 Gbps  | Single-Mode or Multi-Mode Fibre | up to 5 km (SMF) / 550m (MMF)       | (Long Wavelength)                                                                                                     |
| **10GBASE-SR** | 10 Gbps | Multi-Mode Fibre       | up to 300 m (OM3) / 400 m (OM4)     | (Short Reach)                                                                                                         |
| **10GBASE-LR** | 10 Gbps | Single-Mode Fibre      | up to 10 km                         | (Long Reach)                                                                                                          |
| **40GBASE-SR4** | 40 Gbps | Multi-Mode Fibre       | up to 100 m (OM3) / 150 m (OM4)     | Uses MPO/MTP connectors.                                                                                              |
| **40GBASE-LR4** | 40 Gbps | Single-Mode Fibre      | up to 10 km                         |                                                                                                                       |
| **100GBASE-SR4** | 100 Gbps| Multi-Mode Fibre       | up to 70 m (OM3) / 100 m (OM4)      | Uses MPO/MTP connectors.                                                                                              |
| **100GBASE-LR4** | 100 Gbps| Single-Mode Fibre      | up to 10 km                         |                                                                                                                       |

---

### Challenges of Fiber Optics: Return Loss

Controlling light and applying the laws of physics are crucial at the physical contact (PC) points of connectors. **Return loss** refers to light reflected back to the source. This is resolved using different polishing techniques:

* **UPC (Ultra Polished Connectors):** High return loss but zero air gap.
* **APC (Angle Polished Connectors):** Lower return loss but generally has a slightly higher insertion loss than UPC.

---


### Fiber Distribution Panel and Fusion Splicing / Terminating Optic Fibre

Because continually reconnecting fiber optic cables risks wear & tear damage, and to avoid replacing cable runs through conduit, permanent cables are run through conduit walls to wall posts at the access area end and to a **Fiber Distribution Panel** at the switch end.

Fiber patch cables are used to complete the link from the wall post to the NIC, and from the patch panel to the switch port.

A **Fusion Splice** achieves a more permanent join with lower insertion loss. The Fusion splicing machine performs a precise alignment between the two strands and then permanently joins them together using heat; the strands are welded. A High precision instrument must be kept clean & maintained following guidelines.

---



# Chapter 8: DEVICE CATEGORIZATION

## Introduction to Network Devices

Network devices are the fundamental components that enable communication and data exchange within a computer network. They perform various functions, from simply extending a signal to intelligent routing and security. Understanding how these devices are categorized helps in designing, implementing, and troubleshooting networks effectively. Devices can be categorized based on their function, the OSI layer at which they primarily operate, or their role within a network's architecture.

### Categorization by OSI Layer

Network devices often operate predominantly at specific layers of the OSI (Open Systems Interconnection) model, influencing their functionality and interaction with data.

#### Layer 1 (Physical Layer) Devices

These devices operate at the lowest layer, dealing with the physical transmission of raw bit streams over a physical medium. They are primarily concerned with the electrical, mechanical, procedural, and functional characteristics of the network.

A **Hub** acts like a multi-port repeater so that every port receives transmissions sent from any other port. Consequently, every hub port is part of the same shared media access area and within the same Collision Domain. All node interfaces are half-duplex, using the CSMA/CD protocol. The media bandwidth (10 Mbps / 100 Mbps) is shared between all nodes. When Ethernet is wired with a hub, there needs to be a means of distinguishing the Interface on an End system (Computer host / client) from the Interface on an Intermediate system (a HUB). The end system is referred to as **MDI (Medium-Dependent Interface)**. The interface on the hub is referred to as **MDI Crossover (MDI-X)**. This means that the Transmit (Tx) wires on the host connect to Receive (Rx) wires on the hub.
* **Hubs:**
    * **Function:** Connect multiple Ethernet devices together, making them act as a single network segment.
    * **Operation:** A "dumb" device that broadcasts incoming data to all connected ports. Creates a single collision domain.
    * **Modern Use:** Largely obsolete in modern networks, replaced by switches.
    * **Characteristics:** Half-duplex communication.

* **Repeater:** Overcomes the distance limitation by boosting a signal at some point along the cable run. This is a Layer 1 (Physical Layer) device.
    * The attenuation of signals passing over copper or fiber cable imposes a distance limitation on links. A link where the cable length exceeds the distance limitation may not achieve the required speed or become unreliable.
    * Repeaters are available for both copper & fiber links (Optical-Electrical-Optical Repeaters).

* **Media Converter:** When a repeater is used to transition from one Cable type to another, thereby connecting two cable segments of different types.
    * **Single Mode Fiber to Twisted Pair:** Powered devices that convert light signals from SMF cabling into electrical signals carried over a copper wire, or vice versa (via Ethernet network).
    * **Multimode Mode Fiber to Twisted Pair:** Converts light signals in MMF.
    * **Single Mode to Multimode Fiber:** These passive (unpowered) devices convert between the two Fiber Cabling types.


* **Transceivers**
A network might involve multiple types of Cabling. When this occurs, switches & Router equipment must be able to terminate different cable and connector types, and devices must convert from one media type to another. There are also Transceiver modules for Copper wire Cabling. In the past, Transceiver modules were based on the **Gigabit Interface Converter (GBIC)** form factor, which used Subscriber Connector (SC) ports for Gigabit Ethernet. It has been replaced by **SFP (Small Form-Factor Pluggable)**, also known as **Mini-GBIC**. SFP uses LC connectors and is also designed for Gigabit Ethernet. **Enhanced SFP (SFP+)** is an updated specification to support 10GbE but still uses the LC form factor, with different modules to support various Ethernet standards. A transceiver is designed to support a specific wavelength. Transceivers must be installed as matched pairs.
The term **MSA (Multi-Source Agreement)** is intended to ensure that a transceiver from one vendor is compatible with the switch/router module of another vendor.
* The **Quad Small Form-Factor Pluggable (QSFP)** is a transceiver with a form factor of 4x1 Gigabit (4Gbps) links, typically aggregated to a single 4Gbps channel.
* The **Enhanced QSFP (QSFP+)** is designed to support the 40GbE standard by provisioning 4 x 10Gbps links, where four strands transmit and four are unused, to transmit a full-duplex 40Gbps link.
* **Transceiver** combines a Transmitter (Tx) and Receiver (Rx) in a single component.
    * **Function:** Provide a modular interface that matches network types to equipment. Enable physical layer signal conversion, converting between different media types (e.g., fiber to copper and back again). For example, if you have fiber, the switch provides copper ports via a transceiver.
    * **Operation:**
    * **Duplex Communication:** Typically uses two fibers (one for transmit, one for receive).
    * **Bi-directional Transceivers:** Allow traffic in both directions with a single fiber strand by using two different wavelengths, which reduces the number of fiber runs by half.
* **Transceiver Form Factors**
    * **SFP (Small Form-Factor Pluggable):** Also known as "mini-GBICs," these are compact hot-pluggable transceivers.
    * **SFP+ (Enhanced SFP):** Same size as SFP, however, supports longer bandwidth due to its higher frequency of transmission, commonly used for 10 Gigabit Ethernet.
    * **QSFP (Quad Small Form-Factor Pluggable):** A 4-channel SFP, combining four 1 Gigabit/s links for a total of 4 Gbit/s.
    * **QSFP+ (Enhanced QSFP):** Designed for 40 Gigabit Ethernet (4x 10 Gbit/s channels). It combines four SFP+ into a single transceiver. Further enhancements are creating bi-directional QSFP and QSFP+ for increased efficiency over a single fiber run.

---

#### Layer 2 (Data Link Layer) Devices

These devices operate at the Data Link Layer, dealing with MAC (Media Access Control) addresses and frames. They provide error-free transfer of data frames from one node to another over the physical layer.

* **Bridges:**
A **Bridge** works at the Data Link Layer (Layer 2). It separates physical segments into collision domains.

An Ethernet Bridge establishes a connection between separate physical network segments while keeping all nodes in the same logical network (Broadcast Domain), thereby reducing the number of collisions caused by having too many nodes contending for access. By isolating these segments from each other, nodes in one domain do not slow down or contend with nodes in another domain.

An Ethernet Bridge builds a **MAC address table** in memory to track which addresses are associated with which of its ports. It's initially empty pre-initialization, but information is constantly added as the bridge listens to the connected segments. Entries are flushed out of the table after a period to ensure information remains current. If no record of a hardware address (MAC) exists or the frame is a broadcast/multicast, then the bridge floods the frame to all segments except for the source segment (acting like a Layer 1 HUB).

The **contention problem** (where the probability of collision increases and opportunity to transmit becomes less frequent as more devices access the shared medium) is improved by bridges but not fully resolved.
* **Bridges:**
    * **Function:** Connects two or more LAN segments, forwarding frames based on MAC addresses.
    * **Operation:** Similar to a two-port switch, it filters traffic between segments.
    * **Modern Use:** Largely replaced by multi-port switches.

* **Switches:**
The contention problem can be completely resolved by moving from a shared Ethernet System to **Switched Ethernet**, thereby replacing Hubs & Bridges. Switches perform the same function as bridges, but in a more granular way and support many more ports. Gigabit and 10 Gigabit Ethernet (GbE / 10GbE) cannot be deployed without switches.

Each Switch port is a separate **Collision Domain**. In effect, the switch establishes a point-to-point link between any two network nodes. This is referred to as **MICRO SEGMENTATION** (absence of segments).

As with a bridge, traffic on all switch ports is in the same **Broadcast Domain**, unless the switch is configured to use **Virtual LANs (VLANs)**.
* **Switches:**
    * **Function:** Connect network segments or devices, forwarding data frames only to the destination port based on MAC addresses.
    * **Operation:** Builds a MAC address table (CAM table) by learning the MAC addresses of connected devices. Reduces collision domains, creating microsegments.
    * **Characteristics:** Full-duplex communication. Can be managed (VLANs, QoS) or unmanaged.
    * **Common Types:**
        * **Unmanaged Switches:** Plug-and-play, no configuration.
        * **Managed Switches:** Allow configuration of VLANs, QoS, port security, Spanning Tree Protocol (STP), etc.


#### Layer 3 (Network Layer) Devices

These devices operate at the Network Layer, dealing with IP (Internet Protocol) addresses and packets. They are responsible for routing packets between different networks (IP subnets).

* **Routers:**
    * **Function:** Connects different IP networks (e.g., LAN to WAN, home network to internet). Forwards data packets between networks.
    * **Operation:** Uses IP addresses to determine the best path for packet delivery, maintaining routing tables.
    * **Characteristics:** Creates separate broadcast domains. Key for inter-network communication.
* **Layer 3 Switches:**
    * **Function:** A switch that incorporates routing capabilities. Can perform both Layer 2 switching and Layer 3 routing.
    * **Operation:** Routes traffic between VLANs (Inter-VLAN Routing) at high speed using specialized hardware.
    * **Use Cases:** High-performance campus networks where routing between multiple VLANs is needed.

#### Layer 4-7 (Transport to Application Layers) Devices

These devices operate at higher OSI layers, often performing complex functions that go beyond simple packet forwarding, examining data content, and managing application-level traffic.

* **Firewalls:** (As detailed in Chapter 5's concluding section)
    * **Function:** Enforces security policies, controlling incoming and outgoing network traffic.
    * **Operation:** Can inspect traffic at various layers, from packet headers (packet-filtering) to application content (application firewalls).
* **Load Balancers:**
    * **Function:** Distributes incoming network traffic across multiple servers to ensure optimal resource utilization and prevent overload.
    * **Operation:** Improves application availability and responsiveness. Can operate at Layer 4 (TCP/UDP) or Layer 7 (HTTP/HTTPS).
* **Proxy Servers:**
    * **Function:** Acts as an intermediary for requests from clients seeking resources from other servers.
    * **Operation:** Can provide security (hiding client IP), caching (improving performance), and content filtering.
* **Intrusion Detection/Prevention Systems (IDS/IPS):**
    * **Function:** Monitors network traffic for suspicious activity and known threats.
    * **Operation:** IDS detects and alerts; IPS detects and actively blocks/prevents threats.

### Categorization by Function/Role (Network Design)

Network devices can also be categorized based on their logical placement and role within a network's design, especially in hierarchical models (e.g., Cisco's three-tier model).

| Role/Function           | Typical Devices                                         | Key Features                                                              |
| :---------------------- | :------------------------------------------------------ | :------------------------------------------------------------------------ |
| **Access Layer Devices** | Layer 2 Switches (unmanaged or basic managed)           | Port security, VLAN assignments, PoE (Power over Ethernet).               |
| **Distribution Layer Devices** | Layer 3 Switches, Routers                               | Inter-VLAN routing, ACLs (Access Control Lists), QoS (Quality of Service), redundancy (e.g., HSRP, VRRP). |
| **Core Layer Devices** | High-end Layer 3 Switches, Routers                      | Extreme forwarding capacity, redundancy, low latency. Focus solely on fast packet forwarding. |
| **Wireless Devices** | Wireless Access Points (APs), Wireless LAN Controllers (WLCs) | SSID management, security (WPA3), roaming, client management.             |
| **Security Devices** | Dedicated Firewalls, Intrusion Prevention Systems (IPS), VPN gateways, Web Application Firewalls (WAFs) | Packet filtering, stateful inspection, deep packet inspection, threat intelligence. |

---

# CHAPTER 9: DEVICE CONFIGURATION

## InterOperating System (IOS) Boot Phase

The InterOperating System (IOS) is the proprietary operating system used on Cisco Systems routers and network switches. Understanding its boot phase is crucial for network administrators to troubleshoot startup issues and manage device configurations. The IOS boot phase involves a sequence of steps that the device performs to load its operating system and configuration.

**The Cisco IOS Boot Sequence:**

1.  **Power-On Self-Test (POST):**
    * **Function:** This is the initial diagnostic routine executed immediately after the device is powered on or reset.
    * **Operation:** The CPU tests its own subsystem, then checks the basic hardware components like the CPU, memory (RAM), NVRAM (Non-Volatile RAM), and interfaces.
    * **Outcome:** If POST fails, the device may not boot or may indicate a hardware fault via LEDs.

2.  **Load Bootstrap (Boot Loader):**
    * **Function:** After a successful POST, the CPU looks for and loads the bootstrap program. The bootstrap is a small program stored in ROM (Read-Only Memory).
    * **Operation:** Its primary role is to initialize the CPU and manage the booting of the Cisco IOS image. It performs low-level CPU initialization.
    * **Purpose:** The bootstrap essentially tells the router how to load the IOS.

3.  **Locate and Load Cisco IOS Image:**
    * **Function:** The bootstrap program then searches for the Cisco IOS image (the actual operating system software).
    * **Search Order (default):** The default search order for the IOS image typically includes:
        1.  **Flash Memory:** The primary location where the IOS image is usually stored.
        2.  **TFTP Server:** If not found in Flash, the router can attempt to download the IOS image from a TFTP (Trivial File Transfer Protocol) server on the network. This requires a `boot system` command configured with a TFTP path.
        3.  **ROM Monitor (ROMmon) Mode:** If no valid IOS image is found or loaded, the device enters ROMmon mode (or Boot ROM mode). This is a command-line interface for basic operations like recovering a lost password or manually booting an IOS image.
    * **Configuration Register (Con-Reg):** The boot sequence is heavily influenced by the Configuration Register, a 16-bit software register in NVRAM. Its last four bits (bit 3 to bit 0) determine the boot process:
        * `0x2102` (default): Tells the router to attempt to load an IOS image from Flash, then ROM.
        * `0x2101`: Boots directly into ROMmon mode.
        * `0x2142`: Tells the router to ignore the startup-config during boot. (Useful for password recovery).

4.  **Load Configuration File (Startup-config):**
    * **Function:** Once the Cisco IOS image is successfully loaded, the operating system looks for the startup configuration file.
    * **Location:** The `startup-config` file is stored in NVRAM.
    * **Operation:** If found, the `startup-config` is copied into RAM and becomes the `running-config`. This applies all the saved configurations (interface settings, routing protocols, passwords, etc.) to the device.
    * **No Startup-config:** If no `startup-config` is found in NVRAM, the device enters **Setup Mode** (or initial configuration dialog), prompting the user to perform a basic configuration. This typically happens on a brand-new device or after erasing the NVRAM.

5.  **Running Configuration:**
    * **Function:** The device is now fully operational based on the loaded IOS and `running-config`.
    * **Operation:** All changes made to the configuration during active operation are stored in the `running-config` in RAM. These changes are lost upon reboot unless explicitly saved to `startup-config` in NVRAM using the `copy running-config startup-config` command (or `write memory`).

IOS exists as a file—a single file—that the router then loads into RAM to use as its operating system. To better understand the process, you need to understand the IO file system (IFS), which defines how IOS stores files (including the IOS file). The IOS image upgrade process occurs by copying new IOS files into the router and then booting the router with that new IOS. Every OS creates file systems to store files. A computer needs some type of permanent storage, but it needs more than just a place to store bytes. The OS organizes the storage into a file system, which includes directories, structure, and filenames, with the associated rules. By using a file system, the OS can keep data organized so the user and the applications can find the data later. As for the physical storage, Cisco routers typically use flash memory, with no hard disk drive. Flash memory is re-writeable, permanent storage, which is ideal for storing files that need to be retained when the router loses power. Cisco purposefully uses flash memory rather than hard disk drives in its products because there are no moving parts in flash memory, so there is a smaller chance of failure as compared with disk drives. Some routers have flash memory on the motherboard. Others have flash memory slots that allow easy removal and replacement of the flash card, but with the intent that the card remain in the device most of the time. Also, many devices have USB slots that support USB flash drives. Flash memory is where the IOS image (or multiple images) is permanently stored when the device is powered off. Think of it as the hard drive for your IOS.

Flash memory is electrically erasable programmable read-only memory (EEPROM), which allows for updates and storage of multiple IOS versions. For each physical memory device in the router, IOS creates a simple IOS file system and gives that device a name. IOS uses these file systems for other purposes as well, with these types:

* **Opaque:** To represent logical internal file systems for the convenience of internal functions and commands
* **Network:** To represent external file systems found on different types of servers for the convenience of reference in different IOS commands
* **Disk:** For external flash
* **Usbflash:** For USB flash
* **NVRAM:** A special type for NonVolatileRAM memory, the default location of the startup-config file.

Many IOS commands refer to files in an IFS, but only some commands refer directly to the files by their formal names. The `more` command itself displays the contents of a file. However, many commands use a keyword that indirectly refers to a formal filename, to reduce typing. For example:

* `show running-config` command: Refers to file `system:running-config`
* `show startup-config` command: Refers to file `nvram:startup-config`
* `show flash` command: shows the files in the default flash file system (`flash0:`)

```cli
Router# show file systems
```

* `boot system filepath` → This command tells the router the location of the Upgraded IOS image to boot from on device startup. I.e. `boot system flash:c2900-universalk9-mz.SPA.155-2.T1.bin`
* `delete filepath` → `delete flash:c2900-universalk9-mz.SPA.155-2.T1.bin`

The more general `dir flash0:` command lists the contents of that same file system, with similar information. You can use the `dir` command to display the contents of any local IFS.

```cli
Router# dir flash0:
```

### Upgrading IOS Images

One of the first steps to upgrade a router’s IOS to a new version is to obtain the new IOS image and put it in the right location. Typically, Cisco routers have their IOS in one of the local physical file systems, most often in permanent flash. The only requirement is that the IOS be in some reachable file system—even if the file sits on an external server and the device loads the OS over the network. However, the best practice is to store each device’s IOS file in flash that will remain with the device permanently.

The process to upgrade an IOS image into flash memory, using the following steps:

1.  **Step 1.** Obtain the IOS image from Cisco, usually by downloading the IOS image from Cisco.com using HTTP or FTP.
2.  **Step 2.** Place the IOS image someplace that the router can reach. Locations include TFTP or FTP servers in the network or a USB flash drive that is then inserted into the router.
3.  **Step 3.** Issue the `copy` command from the router, copying the file into the flash memory that usually remains with the router on a permanent basis. (Routers usually cannot boot from the IOS image in a USB flash drive.)

```cli
Router# copy tftp|ftp flash
```
The `copy tftp|ftp flash` command Copies the IOS Image to Flash Memory.

The `copy` command does a simple task—copy a file—but the command also has several small items to check. It needs a few pieces of information from the user, so the command prompts the user for that information by showing the user some text and waiting for the user’s input. The command works through these kinds of questions:

* What is the IP address or host name of the TFTP/FTP server?
* What is the name of the file?
* Ask the server to learn the size of the file, and then check the local router’s flash to ask whether enough space is available for this file in flash memory.
* Does the server actually have a file by that name?
* Do you want the router to erase any old files in flash?

The router prompts you for answers to some of these questions, as necessary. For each question, you should either type an answer or press Enter if the default answer (shown in square brackets at the end of the question) is acceptable. Afterward, the router erases flash memory if directed, copies the file, and then verifies that the checksum for the file shows that no errors occurred in transmission.

The `copy` command allows you to use a URI for the source and/or destination, which lets you put most or all of the information in the command line itself. Each URI refers to the formal name of a file in the IFS. The “ftp” part identifies the protocol, of course. After the `//`, the text references the username and password, as well as the FTP server’s IP address. After the single `/` comes the filename on the server. Although the command is long, it has only two parameters, with the long first parameter and the short keyword flash as the second parameter. The `COPY` command lists the source location as the first parameter and the destination as the second. The destination in this case, flash, is a keyword that refers to the default flash, typically `flash0:`, but it does not identify a specific filename. As a result, IOS prompts the user for a specific destination filename, with a default (in brackets) to keep the source filename. In this case, the user just pressed Enter to accept the default. To avoid being prompted at all, the command could have listed `flash:c2900-universalk9-mz.SPA.155-2.T1.bin` as that second parameter, fully defining the destination file.

The IOS `copy` command, when using the `tftp` or `ftp` keyword, makes the command act as a client. The client connects to a TFTP or FTP server and then attempts to transfer the file.

### Verifying IOS Code Integrity with MD5

Cisco provides a means to check the integrity of the IOS file to prevent malicious downloads. First, when Cisco builds a new IOS image, it calculates and publishes an MD5 hash value for that specific IOS file. That is, Cisco uses as input the IOS file itself, runs the MD5 math algorithm against that file, producing a hex code. Cisco places that code at the download site for all to see. Then, you run that same MD5 math on your router against the IOS file on the router, using the IOS `verify` command. That command will list the MD5 hash as recalculated on your router. If both MD5 hashes are equal, the file has not changed.

**MD5 Verification of IOS Images—** The `verify /md5` command generates the MD5 hash on your router/switch. Note that you can include the hash value computed by Cisco as the last parameter or leave it off. If you include it, IOS will tell you if the locally computed value matches what you copied into the command. If you leave it out, the `verify` command lists the locally computed MD5 hash, and you have to do the picky character-by-character check of the values yourself.

```cli
Router# verify /md5 flash:c2900-universalk9-mz.SPA.155-2.T1.bin [MD5_HASH_FROM_CISCO]
```

Device provisioning involves the automated setup and configuration of new network devices. This includes applying initial configurations, setting up interfaces, assigning IP addresses, and implementing basic security policies. Automating these steps eliminates manual, repetitive tasks, significantly speeding up the deployment process and minimizing the risk of human error.

Compliance checks automate the process of verifying if device configurations adhere to predefined standards and policies. While important for maintaining network health and security, they don't directly involve the initial configuration process.

Device software management focuses on automating the upgrading, patching, and managing of software versions on network devices. This is crucial for maintenance but not the primary task of initial configuration.

Data collection and telemetry involve the automated gathering of performance metrics and operational data from network devices. This provides valuable insights but doesn't directly impact the efficiency and accuracy of the configuration process itself.

### General Device Access and Mode Changes

* `SW/RT>enable` → Enter privileged mode
* `SW/RT>Exit` → Exit privileged exec mode or cli terminal
* `SW/RT# configure terminal` → Enter Global Configuration Mode Terminal

### Write Configuration to Memory Buffer

* `Write` or `Write Memory`
* `copy run start`
* `copy running-config startup-config`

### HostName Configuration

* `SW(config)# hostname Office` → Change Switch Hostname


---

## Security and Encryption

The ultimate way to protect passwords in Cisco IOS devices is to not store passwords in IOS devices. That is, for any functions that can use an external authentication, authorization, and accounting (AAA) server, use it. The configuration labelled SSH and TELNET in the figure supports both SSH and Telnet, but consider allowing SSH only by instead using the `transport input ssh` command. The Telnet protocol sends all data unencrypted, so any attacker who copies the message with a Telnet login will have a copy of the password.

```cli
SW/RT# enable passwd Cisco123
```
This sets password to protect privileged mode with a password. Cisco used the `enable password password` global command to define the password that users had to use to reach enable mode (after using the `enable` EXEC command).

```cli
SW/RT# service password-encryption
```
Encrypt the Clear Text password. Cisco attempted to solve this clear-text problem by adding a command to encrypt those passwords: the `service password-encryption` global configuration command. This command encrypts passwords that are normally held as clear text, specifically the passwords for these commands:

* `password password` (console or vty mode)
* `username name password password` (global)
* `enable password password` (global)

IOS adds the encryption or encoding type of “7” to the command, which specifically refers to passwords encrypted with the `service password-encryption` command. While the `service password-encryption` global command encrypts passwords, the `no service password-encryption` global command does not immediately decrypt the passwords back to their clear-text state. Instead, after you enter the `no service password-encryption` command, the passwords remain encrypted until you change a password. Unfortunately, the `service password-encryption` command does not protect the passwords very well. Armed with the encrypted value, you can search the Internet and find sites with tools to decrypt these passwords.

Cisco has never removed the much weaker `enable password` command from IOS. So, on a single switch (or router), you can configure one or the other, both, or neither. What, then, does the switch expect us to type as the password to reach enable mode? It boils down to these rules:

1.  **Both commands configured:** Users must use the password in the `enable secret password` command (and ignore the `enable password password` command).
2.  **Only one command configured:** Use the password in that one command.
3.  **Neither command configured (default):** Console users move directly to enable mode without a password prompt; Telnet and SSH users are rejected with no option to supply an enable password.

The Cisco `enable secret` command protects the password value by never even storing the clear-text password in the configuration. However, that one sentence may cause you a bit of confusion: If the router or switch does not remember the clear-text password, how can the switch know that the user typed the right password after using the `enable` command?

1.  **Step 1.** IOS computes the MD5 hash of the password in the `enable secret` command and stores the hash of the password in the configuration.
2.  **Step 2.** When the user types the `enable` command to reach enable mode, a password that needs to be checked against that configuration command, IOS hashes the clear-text password as typed by the user.
3.  **Step 3.** IOS compares the two hashed values: if they are the same, the user-typed password must be the same as the configured password.

As a result, IOS can store the hash of the password but never store the clear-text password; however, it can still determine whether the user typed the same password.

```cli
SW/RT# enable secret password
```
However, using `secret` uses a more secure encryption algorithm (MD5 Hashing {5}, PBKDF2 {4}, SHA-256 {8}, scrypt {9}) for encrypting the enable password stored in the configuration file.

* `enable [algorithm-type md5] secret password`
* `enable algorithm-type sha256 secret password`
* `enable algorithm-type scrypt secret password`

```cli
SW/RT# username user password pass
```
Encoding the Passwords for Local Usernames.

```cli
SW/RT# login local
```
Login to the Local User; Request for Username:password.

IOS does not use the same logic for the `username` command as it does for allowing both the `enable secret` plus `enable password` commands to exist in the same configuration. IOS allows:

* Only one `username` command for a given username—either a `username user password password` command or a `username user secret password` command.
* A mix of commands (`username password` and `username secret`) in the same router or switch (for different usernames).

You should use the `username secret` command instead of the `username password` command when possible. However, note that some IOS features require that the router knows a clear-text password via the `username` command (for instance, when performing some common authentication methods for serial links called PAP and CHAP). In those cases, you still need to use the `username password` command.

#### TELNET

```cli
SW1(config)#ip default-gateway 192.168.1.254
```
Configure the switch's default gateway. If SW1 doesn't have a default gateway, it can't communicate with devices outside its subnet.

```cli
SW1(config)#enable secret ccna
```
If an enable password/secret isn't configured, you won't be able to access privileged exec mode when connecting via Telnet.

```cli
SW1(config)#username maverick secret ccna
```

```cli
SW1(config)#access-list 1 permit host 192.168.2.1
```
Configure an ACL to limit which devices can connect to the VTY lines.

```cli
SW1(config)#line vty 0 15
```
Telnet/SSH access is configured on the VTY lines. There are 16 lines available, so up to 16 users can be connected at once. (VTY stands for Virtual TeleType).

```cli
SW1(config-line)#login local
```

```cli
SW1(config-line)#exec-timeout 5 0
```

```cli
SW1(config-line)#transport input telnet|ssh|all|none
```
Allows either Telnet/SSH or Both/No transport connections on the Virtual Teletypewriter console line configured.

```cli
SW1(config-line)#access-class 1 in
```
Apply the ACL to the VTY lines. `*access-class` applies an ACL to the VTY lines, `ip access-group` applies an ACL to an interface.

#### SSH (Secure Shell)

SSH (Secure Shell) was developed in 1995 to replace less secure protocols like Telnet. In computing, a shell is a computer program which exposes an operating system's services to a human user or other program. In general, operating system shells use either a command-line interface (CLI) or graphical user interface (GUI), depending on a computer's role and particular operation. It is named a shell because it is the outermost layer around the operating system. SSHV2, a major revision of SSHV1, was released in 2006. If a device supports both version 1 and version 2, it is said to run 'version 1.99'.

* Provides security features such as data encryption and authentication.
* IOS images that support SSH will have 'K9' in their name.
    * Cisco exports NPE (No Payload Encryption) IOS images to countries that have restrictions on encryption technologies. NPE IOS images do not support cryptographic features such as SSH.
* To enable and use SSH, you must generate an RSA public and private key pair.
* The keys are used for data encryption/decryption, authentication, etc.

1.  Configure HostName
2.  Configure DNS domain name
3.  Generate RSA key pair
4.  Configure enable PW, username/PW
5.  Enable SSHV2 (only)
6.  Configure VTY lines

**Connect:** `ssh -L username ip-address` or `ssh username@ip-address`

```cli
SW(config)# hostname Office
```
Change Switch Hostname.

```cli
SW1(config)#ip domain name jeremysitlab.com
```
The FQDN of the device is used to name the RSA keys. FQDN = Fully Qualified Domain Name (host name + domain name).

```cli
SW1(config)#crypto key generate rsa
```
Generate the RSA keys.

```cli
SW1(config)#crypto key generate rsa modulus Length is an alternate method.
```
`*length must be 768 bits or greater for SSHv2`

```cli
SW1(config)#enable secret ccna
```
or

```cli
SW1(config)#username Maverick secret ccna
```

```cli
SW1(config)#access-list 1 permit host 192.168.2.1
```

```cli
SW1(config)#ip ssh version 2
```
(optional, but recommended) Restrict SSH to version 2 only.

```cli
SW1(config)#line vty 0 15
```
Configure all VTY lines, just like Telnet.

```cli
SW1(config-line)#login local
```
Enable local user authentication. `*you can only use login local for SSH.`

```cli
SW1(config-line)#exec-timeout 5 0
```
(optional, but recommended) Configure the exec timeout.

```cli
SW1(config-line)#transport input ssh
```
Best practice is to limit VTY line connections to SSH only.

```cli
SW1(config-line)#access-class 1 in
```
(optional, but recommended) Apply the ACL to restrict VTY line connections. When an external user connects to a router or switch using Telnet or SSH, IOS uses a vty line to represent that user connection. IOS can apply an ACL to the vty lines, filtering the addresses that can telnet or SSH into the router or switch. If filtered, the user never sees a login prompt. ACL checks the source IP address of packets for incoming Telnet/SSH connections.

IOS also supports using ACLs to filter outbound Telnet and SSH connections. For example, consider a user who first uses Telnet or SSH to connect to the CLI and now sits in user or enable mode. With an outbound vty filter, IOS will apply ACL logic if the user tries the `telnet` or `ssh` commands to connect out of the local device to another device.

To configure an outbound VTY ACL, use the `access-class acl out` command in VTY configuration mode. Once configured, the router filters any attempts made by current vty users to use the `telnet` and `ssh` commands to initiate new connections to other devices.

Of the two options—to protect inbound and outbound connections—protecting inbound connections is by far the more important and more common. However, to be complete, outbound VTY ACLs have a surprisingly odd feature in how they use the ACL. When the `out` keyword is used, the standard IP ACL listed in the `access-class` command actually looks at the destination IP address, and not the source. That is, it filters based on the device to which the `telnet` or `ssh` command is trying to connect.

### Command Summaries

| Command / Context                 | Description                                                                                                                                                                                                            |
| :-------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `line console 0`                  | Command that changes the context to console configuration mode.                                                                                                                                                        |
| `line vty 1st-vty last-vty`       | Command that changes the context to vty configuration mode for the range of vty lines listed in the command.                                                                                                           |
| `login` (Console and vty config)  | Tells IOS to prompt for a password.                                                                                                                                                                                    |
| `password pass-value` (Console and vty config) | Lists the password required if the `login` command is configured.                                                                                                                                                      |
| `login local` (Console and vty config) | Tells IOS to prompt for a username and password, to be checked against locally configured `username` global configuration commands.                                                                                      |
| `username name [algorithm-type md5 | sha256 | scrypt] secret pass-value` (Global) | Defines one of possibly multiple usernames and associated passwords, stored as a hashed value (default MD5), with other hash options as well.                        |
| `username name password pass-value` (Global) | Defines a username and password, stored in clear text in the configuration by default.                                                                                                                                 |
| `crypto key generate rsa [modulus 512 | 768 | 1024]` (Global) | Creates and stores (in a hidden location in flash memory) the keys required by SSH.                                                                                                                    |
| `transport input {telnet | ssh | all | none}` (vty line config) | Defines whether Telnet and/or SSH access is allowed into this switch.                                                                                                                    |
| `[no] service password-encryption` (Global) | Global command that encrypts all clear-text passwords in the running-config. The `no` version of the command disables the encryption of passwords when the password is set.                                         |
| `enable password pass-value` (Global) | Global command to create the enable password, stored as a clear text instead of a hashed value.                                                                                                                        |
| `enable [algorithm-type md5 | sha256 | scrypt] secret pass-value` (Global) | Global command to create the enable password, stored as a hashed value instead of clear text, with the hash defined by the algorithm type.                           |
| `no enable secret` (Global)       | Global command to delete the enable secret command.                                                                                                                                                                    |
| `no enable password` (Global)     | Global command to delete the enable password command.                                                                                                                                                                  |

---

# CHAPTER 10: SWITCHES (LAYER 2) 

## Network Interface

A **Network Interface** is the means by which a node is connected to the media and exchanges data with other network nodes. A **Network Interface Card (NIC)** is a transceiver component responsible for physically connecting the node to the transmission medium (a chip).

Each Ethernet network interface port has a Unique **Media Access Control Address** (hardware address / Ethernet Address). In IEEE Terminology, this is an **EUI** (Extended Unique Identifier). An **EUI-64** is a 64-bit Hardware Address. A mechanism allows for translations between the 48-bit MAC address and 64-bit EUI-64 address.

---

### Ethernet Frame Format

Ethernet encapsulates the payload from higher layer protocols within a Protocol Data Unit (PDU) called a **frame**.

| Preamble | Start Frame Delimiter (SFD) | Destination MAC | Source MAC | Ether Type / Length | Payload Data (from higher layer protocols) | Frame Check Sequence (FCS) |
| :------- | :-------------------------- | :-------------- | :--------- | :------------------ | :----------------------------------------- | :------------------------- |
| 7 bytes  | 1 byte                      | 6 bytes         | 6 bytes    | 2 bytes             | 46-1500 bytes                              | 4 bytes                    |

Preamble and SFD are used for clock synchronization and as part of the CSMA/CD protocol to identify collisions during transmissions very early from the Physical Layer, and as such are not technically considered to be part of the frame.

### Error Checking

The frame contains a 4-byte long checksum called a **Cyclic Redundancy Check (CRC)** or **Frame Check Sequence (FCS)**, which is calculated based on the contents of the frame. The receiving node performs the same calculation, and if it matches, accepts the frame. There is no mechanism for retransmission if damage is detected. CRC is not completely accurate at error checks.

---

### MAC / EUI-48 Format

The IEEE gives each manufacturer a range of numbers hard coded to every interface produced, called a **Burned-In Address** or **Universal Address**.

The first 3 bytes or octets (the first 6 Hex Digits) are also known as the **Organizationally Unique Identifier (OUI)** / **OUI Admin Address**.

A **Locally Administered Address** is used on networks in place of the manufacturer's universal coding system. It is defined by changing the U/L bit from 0 to 1. It becomes the responsibility of an organization's Internal Network Admin to ensure that all connected Interfaces are configured with a Unique MAC.

**Broadcast Address:** `FF:FF:FF:FF:FF:FF`

The I/G bit of a MAC address determines whether the frame is addressed to an Individual Node and/or a Group. If the I/G bits are all 1s, the MAC address is referred to as a **Broadcast Address** and should be processed by all nodes within the same broadcast domain.

---

### Maximum Transmission Unit (MTU)

The maximum size of the Data payload found in Layer 2 is **1500 Bytes**. This upper limit size of the payload is referred to as **Maximum Transmission Unit (MTU)**.

Excluding the preamble and SFD, a standard Ethernet frame has a maximum length of 1518 bytes (6 bytes Source MAC + 6 bytes Dest MAC + 2 bytes Ether Type field + 4 bytes FCS + 1500 bytes Payload).

To comply with Ethernet standards, the minimum length of an Ethernet frame is 64 bytes, so the payload must be at least 46 bytes. If this is not the case, it is auto-padded with redundant data. Some Gigabit Ethernet (GbE) and 10 Gigabit Ethernet (10GbE) support **Jumbo Frames** with much larger Maximum Transmission Units.

---


### Advanced Ethernet Switches

Switches normally support a range of Ethernet Standards so that older and newer Network Adapters can all be connected to the same Network.

Advanced Ethernet Switches support interconnections via high-speed backplanes to expandable capacity through plug-in modules, plus power supply redundancy, management consoles, and transceivers for fiber optic connectivity. They can, however, be distinguished using the following general categories:

1.  **Unmanaged vs. Managed:**
    * On a Small Office/Home Office (SOHO) Network, Switches are more likely to be **Unmanaged** Standalone Units that can be added to the network and run without any configuration. The switch functionality might also be built into an Internet Router/modem.
    * On a Corporate network, Switches are likely **Managed** and need Configuration (e.g., Command Line Interface).
2.  **Stackable:** Switches connected together to operate as a single unit. A stack can be managed as a group, and the switch is managed.
3.  **Modular vs. Fixed:**
    * A **Fixed** switch comes with a set number of ports that cannot be changed or upgraded.
    * A **Modular** Switch has slots for plug-in cards/modules.
4.  **Desktop vs. Rack-Mounted:**
    * Simple Unmanaged switches might be supplied as small freestanding units that can be placed on a desktop platform.
    * Stackable units are designed to be fitted to standard-size racks.

---

### Managed Switch Configuration & Interface Identification

Configuration of a Managed Switch can be performed at a Command Line Interface (CLI). Most Switch OS work in multi-Command modes or Hierarchies:

1.  **User EXEC Mode:** Read-Only, used to report configuration, show system states & troubleshooting.
2.  **Privileged EXEC Mode (Enable Mode):** Allows users to reboot, shutdown & backup/restore the system's configuration.
3.  **Global Config Mode:** Allows user to write configuration updates (not read-only in this context; allows writing).

Stackable Switches precede Interface Identifiers with a module ID (different for each switch in the stack). Interfaces are identified by Type, slot on Switch used, and port number (directly correlated).

An Interface has a **line status** (up if a host is connected via a good cable), and a **protocol status** (up if an Ethernet link is established). Line status + protocol status "down" indicates a fault in either the link connection.

---

### Crossover Cable & Auto-MDI/MDIX

A **Crossover Cable** has T568A termination at one end and T568B termination at the other end of the cable. Historically, in the days of Hubs, dedicated Uplink ports and/or Crossover Cables were used to make connections between 2 separate hubs.

When a switch needs to be connected to another switch, communication would fail if both interfaces used MDI-X. Nowadays, most switch interfaces are configured to use **Auto-MDI/MDIX** by default. This means that the switch senses the configuration of the connected device or cable wiring. It senses that an MDI or Uplink to an MDIX port gets configured. This also ensures a link if a Crossover Cable is used to connect to an end system by mistake. Gigabit Ethernet Interfaces must support Auto-MDI/MDIX.

---

### MAC Address Learning & Flooding

A switch learns MAC addresses by reading the **source address** when a frame is received on its port. The address mapping for that port is cached in a **MAC Address Table**, which is stored in a special type of memory known as **Content Addressable Memory (CAM)**. CAM is optimized for searching rather than random access.

If a MAC address isn't found in a MAC Address table, the switch acts like a hub and transmits the frame out to all ports, except for the source port (**FLOODING**).

---

### Port Security

A Port Security Configuration validates the MAC Address of end systems that connect to a switch port. A port security configuration has three primary elements:

1.  Specify an **Enforcement action** when a policy violation is detected (e.g., restrict or shutdown).
2.  Specify a **static MAC Address** or allow the port to learn and accept a certain number of sticky addresses.

---

### Port Aggregation / Link Aggregation

**Port Aggregation** means combining two or more separate cabled links into a single logical channel. From the host end, this can also be called Network Interface Card (NIC) Teaming / Bonding.

**Link Aggregation Control Protocol (LACP)** is used to auto-negotiate the bonded link between the switch port and the end system, detect configuration errors, and recover from the failure of one of the physical links.

Either ingress (incoming) OR egress (outgoing) traffic, or both, can be captured.

---

### Unicast vs. Flooding & Port Mirroring

Unlike Hubs, Switches forward Unicast traffic only to the specific port connected to the intended destination interface, preventing sniffing of Unicast Traffic by hosts attached to the same switch.

**Port Mirroring** copies all packets sent to one or more source ports to a configured monitor port. On a Cisco Switch, this is referred to as **Switched Port Analyzer (SPAN)**. The mirror port would be used by management monitoring software, such as a packet sniffer, network analyzer, or Intrusion Detection System.

---

### Specialized Port Settings

Some types of ports need special optimized port settings, e.g., Storage Area Networks (SANs) found in data centers, which require special requirements to handle Jumbo Frames and Flow Control.

* A **Jumbo Frame** is one that supports a data payload of up to 9000 bytes (far exceeding the ordinary Ethernet frame MTU of 1500 bytes limit), thereby supporting transfer of data in a 10GbE network. This reduces the number of frames that needs to be transmitted (i.e., instead of transmitting 1500 x 6 frames = 9000). It also reduces the amount of processing that switches and routers need to do. It also reduces bandwidth requirement as fewer individual frame headers are transmitted. It's critical that all hosts and appliances along the communication path are able to support the configuration of Jumbo Frames.
* **IEEE 802.3x Flow Control** allows a server to instruct the switch to pause traffic temporarily to avoid overwhelming its buffer and causing it to drop frames. A Switch port can be Configured to Enable/Disable use of pause frames. The 802.3x global pause mechanism doesn't differentiate between traffic types. The updated Priority Flow Control (PFC) mechanism (IEEE 802.1Qbb) allows PAUSE to apply to certain traffic types through the use of Class of Service (CoS). This is related to Quality of Service (QoS).

---

### Power Over Ethernet (PoE)

**Power over Ethernet (PoE)** is a means of supplying electrical power from a Switch via data cabling to a connected powered device (PD).

* **IEEE 802.3af (Type 1) - PoE:** Powered devices can draw up to 13W over cabling. Power is supplied at 350mA / 48V.
* **IEEE 802.3at (Type 2) - PoE+:** Powered devices can draw up to 25W, delivered at 600mA.
* **IEEE 802.3bt (Type 3 / Type 4) - Ultra PoE:** Supplies up to 51W (Type 3) or 75W (Type 4) usable power.

PoE Switches are referred to as **Endpoint Power Sourcing Equipment**. If an existing switch doesn't support PoE, a device called a **Power Injector (Midspan)** can be used.

Cat 3 or better is required to support PoE, while PoE+ must be Cat 5e or better.

Drawing power down the cable generates more heat. If this heat is not dissipated, it can affect data rates. Thermal performance can be achieved or improved using pure copper cabling with large conductors; as a thin conductor will generate more heat through resistance. Also, shielded cable is capable of dispersing heat more efficiently too, through absorption.

---

## VIRTUAL LOCAL AREA NETWORKS (VLANs)

Unless configured differently, managed switches allow the configuration of **Virtual LANs (VLANs)** to logically separate ports into distinct **broadcast domains**. In a well-designed network, there is typically a 1:1 mapping between VLANs and subnets; it's like assigning one room (subnet) for each invisible space (VLAN) you've created.

### Benefits of Implementing VLANs

* **Reduced Broadcast Traffic:** VLANs significantly reduce broadcast traffic, especially beneficial in networks that have expanded beyond a certain number of hosts or users. Each VLAN represents a smaller broadcast domain.
* **Security Segmentation:** From a security point of view, each VLAN can represent a separate security zone, allowing for stricter access controls between different segments of the network. This helps in containing security breaches.
* **Traffic Prioritization (QoS):** VLANs are used to separate nodes based on traffic type and the need for Quality of Service (QoS). For example, switches and Layer 3 routers can be configured to give **Voice VLANs** priority over ordinary data VLANs, ensuring clear voice communication.

### VLAN ID and Assignment

* **VLAN ID 1:** This is the **default VLAN**. All ports on a switch default to being in VLAN 1 unless explicitly configured otherwise.
* **VLAN ID Range:** To assign a node to a VLAN, you configure the port interface on the switch with a VLAN ID in the range of **2 to 4,094**.
* **Reserved IDs:** VLAN IDs **0** (all zeros) and **4,095** (all ones) are reserved for system use and cannot be assigned.
* **Network Segmentation:** VLANs establish network segments (broadcast domains) at **Layer 2 (Data Link Layer)**. A VLAN represents a single broadcast domain.
* **Inter-VLAN Communication:** Communication between different VLANs **must go through a Layer 3 device**, such as a router or a Layer 3 switch.
* **Dynamic VLANs:** Nodes or hosts can also be configured to belong to dynamic VLANs using features supplied by the port, such as a host's MAC address or authentication credentials used (e.g., through 802.1X integration with a RADIUS server). This is referred to as **Dynamic VLAN Assignment**.

### Tagged and Untagged Ports

* **Untagged / Access / Host Port:** If a switch port will only ever participate in a single VLAN, it is configured as an **untagged** or **access port**. This is typically where end-user devices (PCs, printers) connect.
    * If a frame is addressed to a port in the same VLAN on the same switch, no tag needs to be added to the frame.
    * If the switch receives an 802.1Q tagged frame on an access port, it will usually strip the tag before forwarding it to the end device, as the end device typically doesn't understand VLAN tags.
* **Tagged / Trunk Port:** A **tagged port** will normally be operating as a **trunk**. A trunk is capable of transporting traffic addressed to multiple VLANs using the **IEEE 802.1Q frame format**.
    * A trunk might be used to connect switches to each other or to connect a switch to a router (or Layer 3 switch).
    * When frames designated for different VLANs are transported across a trunk, the VLAN ID of each frame must be preserved for the receiving switch or router to forward it correctly.
    * Under **802.1Q**, per-VLAN traffic is identified by a tag inserted in the Layer 2 Ethernet frame. This tag contains information about the **VLAN ID (1-4094)** and **priority** (used for QoS functions). A specific EtherType value is set to identify the frame as 802.1Q.
    * If a frame needs to be transported over a trunk link (e.g., connecting two different switches), the source switch adds the relevant 802.1Q tag to identify the VLAN, and then forwards the frame out the trunk port to the destination switch.
    * An administrative host or server that needs to access multiple VLANs might need to be attached to a trunk port rather than an access port, and its network interface configured to understand VLAN tagging.

### Voice VLANs

* **Voice over IP (VoIP)** transmits audio/voice traffic as data packets, rather than using circuit-based transmission.
* The bandwidth and latency requirements of voice traffic mean that it is often necessary to prioritize it over other types of data packets. This can be implemented using a dedicated VLAN for voice traffic.
* Normally, for a switch interface to process tagged frames, it would have to be configured as a trunk port. However, this can add configuration complexity, especially for ports connected to IP phones that also have a PC connected through them.
* Many switches now support the concept of a **Voice Auxiliary VLAN**. This allows the switch to distinguish VoIP traffic without having to configure the port as a full trunk.
* **Common Scenario:** A single physical wall port is shared between a PC and a VoIP handset. The handset has an internal 3-port switch.
    * The PC's untagged data traffic (e.g., VLAN ID 100) passes through the IP phone to the switch.
    * The VoIP handset's voice traffic is typically assigned a different VLAN ID (e.g., VLAN ID 101) and is sent to the switch as 802.1Q tagged traffic.
    * The switch will only accept tagged frames that match the configured Voice VLAN ID.
    * To avoid manual configuration, the Voice VLAN ID and other configuration parameters can be communicated to the handset using protocols like **Cisco Discovery Protocol (CDP)**.
    * **Switch Interface Configuration Example for Voice VLAN:** `switchport voice vlan [ID]`

### Private VLANs (PVLANs)

* A **Private VLAN (PVLAN)** applies an additional layer of segmentation by restricting the ability of hosts within a VLAN to communicate directly with one another, even if they are in the same subnet.
* **Use Cases:** This might be used by a hosting company to prevent web servers operated by different customers from being able to communicate with each other. Similarly, Internet Service Providers (ISPs) use PVLANs to isolate subscriber traffic. Isolating these server instances using PVLANs can be simpler than creating multiple VLANs and subnets for each isolated instance.
* **PVLAN Port Types:** When configuring a PVLAN, the host VLAN is referred to as the **Primary VLAN**. Several types of ports can be configured within a PVLAN:
    * **Promiscuous Port:** Can communicate with all other ports in all domains within the PVLAN. Routed/DHCP traffic typically goes through this port (e.g., a router interface).
    * **Isolated Port:** Can only communicate with the promiscuous port. This effectively creates a subdomain of a single host only. A PVLAN can contain multiple isolated ports, but each is in its own isolated subdomain.
    * **Community Port:** Can communicate with the promiscuous port and with other ports in the same community. This creates a domain that can contain multiple hosts that can communicate with each other, but not with hosts in other communities or isolated ports within the same PVLAN (except through the promiscuous port).

### Default VLAN vs. Native VLAN

* **Default VLAN (VLAN 1):** VLAN ID 1 is referred to as the DEFAULT VLAN. This cannot be changed. All ports on a switch default to being in VLAN 1. When implementing VLANs, you should **avoid sending user data traffic over the default VLAN**. It should remain unused or used only for inter-switch protocol traffic (e.g., Spanning Tree Protocol traffic is permitted to run over the default VLAN). Ensure that unused ports are not assigned to VLAN 1.
* **Native VLAN:** A **native VLAN** is the VLAN into which any **untagged traffic** is placed when receiving frames over a trunk port.
    * When a switch receives an untagged frame over a trunk, it assigns the frame to the native VLAN.
    * Such untagged traffic might come from legacy devices that do not support 802.1Q encapsulated frames (although this is rare in modern networks where trunking is used primarily with 802.1Q).
    * The native VLAN is initially set with the same VID as the default VLAN (VLAN 1).
    * You **can and should change this** to make the native VLAN a suitable, unused ID. This ID should ideally **not be the same as any VLAN used for any other data traffic**.
    * The same native VLAN ID should be configured for the trunk port on both interconnected switches to avoid potential VLAN hopping attacks or traffic misplacement.

---

#### Understanding Broadcast Domains

A broadcast domain is a network segment where a broadcast frame sent by any device is received by all other devices within the same segment. This characteristic defines the limitations and scope of broadcast traffic within a Layer 2 network (LAN).

* **Switch Behavior:**
    * Switches propagate broadcast frames out through all ports except the one on which the frame was received. Unlike switches, routers block broadcast frames from passing to other network segments, thereby limiting the spread of broadcast traffic.
* **Concerns with broadcast Traffic:**
    * Excessive broadcast traffic can degrade network performance and pose security risks. It's essential to manage and contain broadcast domains effectively.

#### VLANs (Virtual Local Area Networks)

VLANs are used to segment a physical network into multiple logical networks at Layer 2. Each VLAN forms its own broadcast domain, which helps in reducing unnecessary broadcast traffic and enhances network security and performance.

* **Configuration Steps:**
    1.  **Create VLAN:**
        ```cli
        Switch(config)# vlan [VLAN_NUMBER]
        Switch(config-vlan)# name [VLAN_NAME]
        ```
    2.  **Assign VLAN to Interface:** This sets the interface `fa0/1` as an access port in `[VLAN_ID]`.
        ```cli
        Switch(config)# interface fa0/1
        Switch(config-if)# switchport mode access
        Switch(config-if)# switchport access vlan [VLAN_ID]
        ```

* **Default VLANs and Ranges:**
    * All interfaces are in VLAN 1 by default.
    * Normal range VLANs: 1-1005.
    * Extended range VLANs: 1006-4094.

### Advanced Concepts in Inter-VLAN Routing and Trunking

#### Efficient Handling of Multiple VLANs

In a network where the number of VLANs increases, using a separate interface for each VLAN becomes impractical. This is due to physical limitations such as the number of router interfaces and the inefficiency of managing multiple cables and ports.

* **Trunk Ports:**
    * To efficiently manage traffic from multiple VLANs over a single interface, trunk ports are used. These ports can carry traffic for multiple VLANs simultaneously, distinguishing the traffic by tagging frames with VLAN IDs. Trunk ports carry traffic for multiple VLANs across a single link using tagging protocols like IEEE 802.1Q, which keeps the traffic for different VLANs segregated.

#### Trunking Protocols

The primary protocol used for trunking on modern networks is IEEE 802.1Q. It is essential for maintaining VLAN information as traffic moves between switches or to routers.

* **IEEE 802.1Q Tagging:**
    * **Frame Structure:** Adds a 4-byte tag into the original Ethernet frame, which includes:
        * **Tag Protocol Identifier (TPID):** A field that identifies the frame as an IEEE 802.1Q-tagged frame.
        * **Priority Code Point (PCP):** A 3-bit field used for class of service to prioritize traffic.
        * **Drop Eligible Indicator (DEI):** Indicates if the frame can be dropped if the network is congested.
        * **VLAN ID (VID):** A 12-bit field essential for identifying the VLAN to which the frame belongs. The range of possible VLAN IDs is 1-4095, offering extensive flexibility.

#### Frame Handling Across Switches

* **Same VLAN Communication:** No tagging is required if the destination port resides in the same VLAN on the same switch.
* **Different VLAN Communication:**
    * Within the same switch, frames destined for different VLANs are tagged with the destination VLAN ID.
    * Between different switches, frames are transmitted over trunk links with appropriate tagging according to IEEE 802.1Q standards.

#### Switch Processing and MAC Address Learning

When a frame enters a switch:

* If the VLAN ID from the tag is active and valid, the switch processes it according to configured interface port settings.
* The switch uses its MAC address table to determine the correct outgoing ports for the VLAN specified by the tag.
* If the destination MAC address is unknown, the switch may broadcast the frame to all ports in the specific VLAN, except the one it arrived on.

#### Native VLAN and Untagged Traffic

* **Native VLAN Concept:** By default, VLAN 1 is treated as the native VLAN on trunk ports.
* Untagged frames arriving on a trunk port are assumed to belong to the native VLAN.
* Frames destined for the native VLAN are transmitted without an IEEE 802.1Q tag.

#### Note on Security and Configuration

Ensuring that the native VLAN matches on all interconnected trunk ports is critical to prevent VLAN hopping attacks and other security vulnerabilities. It is advisable to change the native VLAN from the default (VLAN 1) to another unused VLAN ID and configure this consistently across all devices.

### Conclusion

Understanding and implementing inter-VLAN routing and trunking are vital for network scalability and efficiency. Proper use of trunking protocols like IEEE 802.1Q facilitates seamless communication across multiple VLANs while conserving physical resources. Additionally, careful configuration and management of VLAN settings and native VLAN configurations enhance network security and operational efficiency.

#### Inter-VLAN Routing

For traffic to flow between different VLANs, routing must occur at Layer 3:

* **Router-on-a-Stick:** A single physical router interface can be subdivided into multiple logical sub-interfaces, each corresponding to a different VLAN. Here, each sub-interface handles traffic for a specific VLAN, and the encapsulation specifies the VLAN ID associated with the sub-interface.
    ```cli
    Router(config)# interface fa0/0.1
    Router(config-subif)# encapsulation dot1Q [VLAN_ID]
    Router(config-subif)# ip address [IP_ADDRESS] [SUBNET_MASK]
    ```

* **Layer 3 Switches:**
    * Layer 2 switches don't perform packet routing and don't build a routing table. They aren't IP routing aware. However, you can assign an IP address to an SVI to allow remote connections to the CLI of the switch (using Telnet or SSH). These can perform routing between VLANs without needing separate router. Like ROAS Architecture.
    * **Example Configuration:**
        ```cli
        Switch(config)# interface vlan [VLAN_ID]
        Switch(config-if)# ip address [IP_ADDRESS] [SUBNET_MASK]
        Switch(config-if)# no shutdown
        ```
    * This configures a virtual interface for each VLAN, allowing the switch to route traffic between them directly.

Properly configuring VLANs and managing broadcast domains are critical for maintaining network efficiency, security, and scalability. By segmenting a network into VLANs and correctly configuring inter-VLAN routing, network administrators can ensure optimal performance and robust security across the network infrastructure.

### Multilayer Switching and Inter-VLAN Routing

#### Concepts and Implementation

Multilayer or Layer 3 switches are advanced devices capable of both switching and routing functions, allowing for efficient handling of traffic within VLANs and between different networks.

#### Native VLAN and IP Setup

* **Native VLAN:** This is used primarily for untagged traffic that arrives on trunk connections. This feature is crucial in environments where devices like VoIP phones are connected to the network, as these devices can tag their own traffic. PCs connected to these phones rely on the native VLAN configuration to route traffic.
* **Configuration Challenges:**
    * If there are discrepancies in native VLAN settings across interconnected switches, it may lead to "native VLAN mismatch" errors, causing traffic routing issues.
    * Correctly configuring the native VLAN across all devices ensures that traffic from PCs flows only through the intended paths without leaking into other VLANs.

#### Configuration Commands

To change the native VLAN on a router or switch, use the following commands depending on the device and requirement:

* **Router Subinterface (for Router-on-a-Stick configurations):**
    ```cli
    Router(config-subif)# encapsulation dot1Q <VLAN-ID> native
    ```
* **Switch Configuration (setting native VLAN on a trunk port):**
    ```cli
    Switch(config-if)# switchport trunk native vlan <VLAN-ID>
    ```

---

## Layer 3 / Multilayer Switch Features:

* **IP Address Assignment:**
    * **Routed ports:** Directly assign IP addresses to the physical interfaces on the switch which behave like router interfaces.
    * **SVIs (Switched Virtual Interfaces):** Create virtual Layer 3 interfaces for each VLAN, allowing the switch to route traffic between VLANs internally.

* **Routing Capabilities:**
    * Static and default routing configurations enable communication with external networks and other routers or Layer 3 switches.
    * **Enabling IP routing:**
        ```cli
        Switch(config)# ip routing
        ```
    * **Configuring a default route:**
        ```cli
        Switch(config)# ip route 0.0.0.0 0.0.0.0 <next-hop-address>
        ```

#### Practical Configuration Examples

* **Resetting an Interface to Default Configuration:**
    ```cli
    Switch(config)# default interface <interface-id>
    ```

* **Enabling Layer 3 Routing on the Switch:**
    ```cli
    Switch(config)#ip routing
    ```

* **Assigning an IP Address to a Routed Port:**
    ```cli
    Switch(config-if)# ip address <ip-address> <netmask>
    Switch(config-if)# no switchport  # This command transforms the interface from Layer 2 to Layer 3
    ```

Multilayer switches offer extensive flexibility and efficiency in managing inter-VLAN routing and overall network traffic. Proper configuration of native VLANs and understanding how to utilize and configure routed ports and SVIs are crucial for optimizing network performance and security. These capabilities allow network administrators to manage complex network topologies more effectively, integrating voice, data, and video traffic over a unified infrastructure.

### Switch Virtual Interfaces (SVI) and Multilayer Switch Configuration

Switch Virtual Interfaces (SVIs) represent a pivotal feature in Layer 3 switches, enabling inter-VLAN routing directly within the switch. This technique avoids the need for external routers for VLAN routing, simplifying network design and often enhancing performance.

#### Key Concepts for SVI:

* **SVI Initialization:** By default, SVIs are administratively down on Cisco switches. To use them for routing traffic between VLANs, they must be explicitly enabled.

* **VLAN Requirements:**
    * A VLAN must exist on the switch before you can assign an SVI to it. If an SVI is configured for a nonexistent VLAN, the switch will not create the VLAN automatically.
    * The VLAN associated with an SVI must not be shut down (`no shutdown` command).
    * There must be at least one operational access or trunk port associated with the VLAN for the SVI to be up.

* **Gateway Configuration:** End devices within VLANs should have their gateway set to the IP address of the corresponding SVI, not to an external router.


#### Practical SVI Configuration Example

The configuration of an SVI involves assigning it an IP address and enabling it. Here’s how to configure an SVI for VLAN 10 and VLAN 20 on a Cisco Layer 3 switch:

```cli
# Entering global configuration mode
Switch(config)# interface vlan 10
# Assigning an IP address to the SVI for VLAN 10
Switch(config-if)# ip address 192.168.1.1 255.255.255.192
# Enabling the SVI
Switch(config-if)# no shutdown
# Exiting back to global configuration mode
Switch(config-if)# exit

# Configuring SVI for VLAN 20
Switch(config)# interface vlan 20
Switch(config-if)# ip address 192.168.1.65 255.255.255.192
Switch(config-if)# no shutdown
Switch(config-if)# exit
```

Each SVI acts as a gateway for its respective VLAN, allowing inter-VLAN communication when combined with proper routing configurations.

#### Routed Ports

Besides SVIs, Layer 3 switches can also configure physical interfaces to act as routed ports. This setting transforms an interface from a Layer 2 switch port into a Layer 3 interface similar to a router's interface.

Here's how to configure a routed port:

```cli
# Selecting the interface
Switch(config)# interface gigabitethernet 0/1
# Disabling switching functionality
Switch(config-if)# no switchport
# Assigning an IP address
Switch(config-if)# ip address 10.0.0.1 255.255.255.0
# Enabling the interface
Switch(config-if)# no shutdown
```

This configuration is ideal for point-to-point links between switches or connections to other routers.
Configuring SVIs and routed ports on Layer 3 switches greatly enhances the flexibility and efficiency of network designs. These features facilitate advanced network segmentation, efficient routing, and simplified infrastructure with fewer devices and interconnections. Properly setting up and managing these interfaces ensures robust, scalable network architecture capable of supporting diverse organizational needs.


## VLAN and Trunk Configuration

* `SW(config-if)# switchport mode trunk` → Switch the Selected interface(s) port mode to Trunk (for Tagged Frames over Trunk Link).
* `SW(config-if)# switchport trunk encapsulation dot1q|ISL` → Sets the Encapsulation Negotiation Mode to either Dot1Q or ISL.
* `SW# switchport trunk allowed vlan {Add|except|All|None|Remove} ID` → This lets you configure vlan-IDs of the allowed VLAN when this port is In trunking mode.
* `SW# switchport trunk native VLAN ID` → The setting of native vlan is to ensure frames (untagged) coming over a trunk port gets forwarded to a specific native VLAN specified in the command.

### VLAN Management

* `SW(config)# vlan 20` → Select Vlan 20 for Configuration.
* `SW(config)# name UserNetwork` → Set Common Name of VLAN UserNetwork.
* `SW(config-if)# switchport access vlan ID` → Switch configuration to Vlan ID.

## Dynamic Trunking Protocol (DTP)

Dynamic Trunking Protocol (DTP) is a Cisco proprietary protocol that facilitates the automatic negotiation of trunk links between Cisco switches. This protocol simplifies network configuration and management by allowing switches to dynamically establish trunk links without manual intervention.

#### Key Concepts of DTP:

* **Default Settings:** DTP is enabled by default on all Cisco switch interfaces. However, for increased security, it's recommended to manually configure trunk settings.
* **Modes:** Interfaces can be configured in dynamic auto, dynamic desirable, or static access modes, influencing how they negotiate trunks with connected devices.

#### Configuration Commands:

* **Dynamic Mode Setting:**
    ```cli
    # Set the dynamic mode to either auto or desirable
    Switch(config-if)# switchport mode dynamic [auto | desirable]
    ```

* **Disabling DTP Negotiation:**
    ```cli
    # Disable DTP negotiation on an interface
    Switch(config-if)# switchport nonegotiate
    ```

#### Operation Modes

* **Trunk:** The port actively attempts to form a trunk with the remote switch.
* **Access:** The port strictly functions as an access port for a specific VLAN.
* **Dynamic Auto:** The port passively waits for DTP frames before switching to trunk mode.
* **Dynamic Desirable:** The port actively sends DTP frames, attempting to convert the link into a trunk.

#### Table: Interactions Between Configurations

| Mode / Config   | Auto      | Trunk     | Access    | Desirable |
| :-------------- | :-------- | :-------- | :-------- | :-------- |
| **Auto** | Auto      | Trunk     | Access    | Trunk     |
| **Trunk** | Trunk     | Trunk     | Misconfig | Trunk     |
| **Access** | Access    | Misconfig | Access    | Access    |
| **Desirable** | Trunk     | Trunk     | Access    | Trunk     |

* `MISCONFIG` indicates a misconfiguration error leading to possible traffic issues.

#### Best Practices:

* **Security:** For enhanced security, disable DTP on ports configured as static access or trunk ports.
* **Consistency:** Ensure that both ends of a trunk are configured consistently to prevent errors or undesired operation.
* **Switch Compatibility:** Newer Cisco switches default to dynamic auto, while older models may default to dynamic desirable. Adjust configurations appropriately based on model capabilities and network requirements.

Understanding Dynamic Trunking Protocol is crucial for configuring and managing VLANs effectively on Cisco switches. Properly leveraging DTP can lead to simplified management and automated switch configuration, but it requires careful handling to maintain network security and performance. Always ensure your switch configurations are deliberate and secure, especially in sensitive or complex network environments.

## VLAN Trunking Protocol (VTP)

VLAN Trunking Protocol (VTP) simplifies the management of VLANs in a network by allowing centralized configuration changes on a VTP server that are automatically propagated to all other switches in the VTP domain.

#### Key Features of VTP:

* **Central Management:** VTP allows VLAN configurations to be made centrally on a VTP server switch. Changes are then synchronized across all client switches.
* **VTP Modes:**
    * **Server Mode:** Can create, modify, or delete VLANs. This mode is default on Cisco switches.
    * **Client Mode:** Cannot create, modify, or delete VLANs. It only synchronizes with the server.
    * **Transparent Mode:** Does not participate in VTP. Maintains its own VLAN configuration and forwards VTP advertisements.

#### Version Differences:

* **VTP v1/v2:**
    * Primarily differ in support for Token Ring VLANs (only in v2).
    * Do not support extended range VLANs (1006-4094).
* **VTP v3:**
    * Supports extended VLANs up to 4094.
    * Provides better control over which device is allowed to update others.

#### Operational Details:

* **Revision Number:** Incremented each time a change is made on a VTP Server. Crucial for determining synchronization needs.
* **Synchronization:** Clients synchronize their VLAN database with a server that has the highest revision number within the VTP domain.

#### Configuration Commands:

```cli
# Set the VTP version
Sw(config)# vtp version [1 | 2 | 3]

# Set the VTP domain name
Sw(config)# vtp domain [Domain_Name]

# Configure VTP mode
Sw(config)# vtp mode [client | server | transparent]

# Display current VTP status
Sw# show vtp status
```

#### Best Practices:

* **Security:** Carefully manage the revision numbers and VTP modes, especially when adding new switches to a network to avoid unwanted database overrides.
* **Compatibility:** Ensure all switches within the VTP domain can support the intended VTP version, especially when using extended VLANs with VTP v3.
* **Precaution:** Reset the configuration revision number to zero when changing the domain name or switching a device from server/client to transparent to prevent accidental propagation of an old VLAN database.

Understanding VTP is essential for network administrators to efficiently manage large-scale networks with multiple VLANs. Proper use of VTP can significantly reduce administrative overhead and potential for configuration errors. However, it requires cautious handling to maintain network stability and security.

---

## Spanning Tree Protocol (STP) and Cisco Per-Vlan STP (PVST)

The Spanning Tree Protocol (STP) was developed to address the challenges in a network with redundant paths, specifically to prevent Layer 2 loops. This protocol is essential for maintaining a stable network environment by managing a loop-free logical topology.

#### Key Concepts of STP

* **Role of Root Bridge:** The root bridge in an STP topology is the focal point from which all path calculations are made. Each switch in the network uses the Spanning Tree Algorithm to determine the shortest path to the root bridge.
* **Port Roles:**
    * **Designated Ports:** Always in a forwarding state, these ports are selected on a per-link basis and are responsible for forwarding frames towards the root bridge.
    * **Root Ports:** Every non-root bridge has a single root port. Root ports are the best path from the non-root bridge to the root bridge.
    * **Blocked Ports:** These ports are non-designated ports and do not forward packets; they only listen to BPDUs to prevent loops.

#### States of STP Ports

* **Blocking:** In this initial state, the port does not participate in frame forwarding and listens to BPDUs to decide the future action.
* **Listening:** The port prepares for eventual packet forwarding and still listens to BPDUs to ensure no information has changed.
* **Learning:** At this stage, the port learns MAC addresses but does not forward frames yet.
* **Forwarding:** The port sends and receives all data frames if it is the designated or root port.
* **Disabled:** A network administrator manually disables the port and it does not participate in frame forwarding or reception.

Cisco’s Per-VLAN Spanning Tree (PVST) enhances STP by allowing separate spanning tree instances for each VLAN configured in the network. This granularity allows for better load balancing and specific tuning of the network infrastructure.

#### Potential Issues and Solutions with STP

* **MAC Address Flapping:** Occurs when a MAC address is found on different ports due to incorrect network configurations. This can be mitigated by proper network design and ensuring that all redundant paths are managed by STP.
* **Broadcast Storms:** Caused by infinite looping of broadcast frames in a network with redundant links. STP prevents this by creating a loop-free tree structure.

#### Administrative Options in STP

* **PortFast:** Bypasses the traditional listening/learning states and directly places a port into the forwarding state when connected to a single host.
* **BPDU Guard:** Automatically disables a port if a BPDU message is received on that port, useful in PortFast-enabled ports to prevent accidental loop formations.

The Spanning Tree Protocol and its enhancements like Cisco's PVST are critical for the design and operation of modern networks with redundancy. Understanding how to implement and manage these protocols helps in achieving a stable, efficient, and loop-free network topology, ensuring high availability and reliability in enterprise environments.

### Cisco STP and PVST Implementation Details

The Spanning Tree Protocol (STP) and Cisco's Per-VLAN Spanning Tree (PVST) play pivotal roles in preventing network loops and ensuring efficient traffic management across redundant paths. Understanding the mechanics of bridge priority and its impact on root bridge selection is crucial for network design and troubleshooting.

#### Bridge Priority in STP

* **Purpose:** The bridge priority determines the preference level a switch has to become the root bridge in an STP environment. The lower the priority value, the higher the chances of being elected as the root.
* **Default Priority:** The standard default priority for any Cisco switch is 32768. Adjustments made to this value influence the selection process for the root bridge.

#### MAC Address Role

* **Tie-breaking:** If two switches have the same priority, the MAC address serves as a tie-breaker. The switch with the lowest MAC address becomes the root bridge.

#### Extended System ID in PVST

* **Functionality:** Cisco’s enhancement to STP, PVST, incorporates VLAN information into the bridge priority by using an Extended System ID.
* **Calculation:** The Extended System ID typically represents the VLAN ID which is added to the base priority to form the total bridge priority.

#### Priority Configuration

* **Granularity:** The bridge priority can be adjusted in increments of 4096. This granularity helps in finely tuning the root bridge selection process across different network scenarios.
* **Values:**
    * Valid values range from 0 to 61440, in steps of 4096.
    * Sample settings: 4096, 8192, 12288, ..., up to 49152.

#### Cisco PVST Specifics

* **Per-VLAN Basis:** PVST runs an individual STP instance for each VLAN, allowing distinct bridge priorities for each VLAN. This capability enhances load balancing and provides flexibility in traffic management.
* **Example:** In a default VLAN (VLAN 1), if the base priority is set to 32768, adding the VLAN ID results in a total priority of 32769. Adjustments can be made uniquely per VLAN to influence the root bridge selection differently across VLANs.

### Practical Application and Impact

In practice, adjusting the bridge priority is a strategic decision used to optimize the topology of a network for reliability and efficiency. Network administrators must carefully plan these settings based on the network size, topology, traffic patterns, and organizational requirements.

For networks with multiple VLANs, PVST offers significant advantages by isolating potential issues and tuning performance on a per-VLAN basis, thereby enhancing overall network stability and responsiveness.

### Conclusion

Understanding the intricacies of STP and PVST, including the roles of bridge priority and MAC addresses, is essential for managing modern network infrastructures. These protocols ensure that even in environments with complex and redundant paths, data packets find an optimal route, maintaining both network integrity and performance.

For understanding the relationship and calculation of the Bridge ID in Spanning Tree Protocol (STP), we will break down each part of the formula and provide a tabular layout to illustrate how the bridge priority from the Spanning Tree Protocol Data Unit (BPDU) translates into the overall Bridge ID.

### Formula Breakdown:

1.  **Bridge Priority**: This is typically a value that can range from 0 to 65535, but only the top 4 bits are considered as "priority" in this context, which theoretically allows for 16 priority levels.
2.  **Extended System ID (VLAN ID)**: This is a 12-bit value representing the VLAN ID, which enhances the bridge priority to prevent switching loops across different VLANs.
3.  **Total Bridge Priority**: This is the sum of the Bridge Priority and the Extended System ID. It forms the first 16 bits of the Bridge ID.
4.  **MAC Address**: This is a 48-bit value unique to each switch, completing the remaining part of the Bridge ID.

### Example Table:

Here's how these components combine to form the Bridge ID:

| Component             | Description                          | Bits | Example Value        |
| :-------------------- | :----------------------------------- | :--- | :------------------- |
| Bridge Priority       | Base priority of the bridge          | 4    | `32768`              |
| +                     |                                      |      |                      |
| Extended System ID    | VLAN ID used as extended system ID   | 12   | `100`                |
| =                     |                                      |      |                      |
| Total Bridge Priority | Combined value of priority + VLAN ID | 16   | `32868`              |
| +                     |                                      |      |                      |
| MAC Address           | Unique identifier of the switch      | 48   | `00-1A-2B-3C-4D-5E`  |
| ->>                   |                                      |      |                      |
| Bridge ID             | Final bridge identifier              | 64   | `32868-001A2B3C4D5E` |

### Explanation of Values:

* **Bridge Priority (32768)**: A common default value for Cisco switches.
* **Extended System ID (100)**: Represents VLAN 100 being incorporated into the bridge priority.
* **Total Bridge Priority (32868)**: Sum of the base priority and the VLAN ID turned into a single 16-bit number.
* **MAC Address (`00-1A-2B-3C-4D-5E`)**: An example MAC address.
* **Bridge ID (`32868-001A2B3C4D5E`)**: The full 64-bit identifier used in STP operation to elect the root bridge and other roles.

This structure ensures each bridge in a network can be uniquely identified not just by its hardware (MAC), but also by its configuration role within specific VLAN contexts.

To visualize the bit-level distribution across the different fields within the Bridge ID as used in Spanning Tree Protocol (STP) BPDU, we can break it down into a more detailed tabular format. This will show how the bits are allocated towards each component of the Bridge ID.

### Bit Distribution Table:

| Field                     | Bits    | Description                          | Example Bits                                     |
| :------------------------ | :------ | :----------------------------------- | :----------------------------------------------- |
| Bridge Priority           | 4 bits  | Base priority of the bridge          | `1000`                                           |
| Extended System ID        | 12 bits | VLAN ID used as extended system ID   | `0000 0110 0100`                                 |
| **Total Bridge Priority** | **16 bits** | Sum of the above two fields          | `1000 0000 0110 0100`                            |
| MAC Address               | 48 bits | Unique identifier of the switch      | `0000 0001 1010 0010 1011 0011 1100 0100 1101 0101 1110` |

### Combined Bridge ID:

Combining the Total Bridge Priority with the MAC Address to form the complete 64-bit Bridge ID looks like this:

| Total Bridge Priority (`32868`) | MAC Address (`00-1A-2B-3C-4D-5E`)                               |
| :------------------------------ | :---------------------------------------------------------------- |
| `1000 0000 0110 0100`           | `0000 0001 1010 0010 1011 0011 1100 0100 1101 0101 1110`         |

### Full 64-bit Bridge ID Representation:

**`1000 0000 0110 0100 0000 0001 1010 0010 1011 0011 1100 0100 1101 0101 1110`**

### Explanation:

* The **first 4 bits** for the Bridge Priority typically allow for basic prioritization levels.
* The **next 12 bits** represent the VLAN ID, which is crucial in environments where multiple VLANs exist and STP calculations need to be VLAN-aware.
* These 16 bits combined form the **Total Bridge Priority**, which precedes the MAC Address in the Bridge ID.
* The **final 48 bits** are taken directly from the MAC address of the device.

This structure ensures that within the frame of an STP BPDU, the Bridge ID uniquely identifies each configured bridge, factoring in both its role in network topology and its physical hardware identity.

### Spanning Tree Protocol (STP) Initialization and Port Roles Determination

When a switch is powered on, each assumes it is the potential Root Bridge, initiating the Spanning Tree Protocol by sending out Bridge Protocol Data Units (BPDUs). The election of the actual Root Bridge and subsequent roles of ports across the network are determined through comparisons and changes of these BPDUs. Here's a detailed breakdown of the process:

#### Root Bridge Selection

* **Initial Assumption:** Every switch considers itself as the root upon startup and sends out BPDUs to assert this.
* **Superior BPDU Identification:** A switch relinquishes its claim as the root if it receives a BPDU with a lower bridge ID, which includes a combination of bridge priority and MAC address.
    * Lowest Bridge Priority
    * Lowest MAC Address Value
* **Consensus & Stability:** Once all switches agree on the identity of the root, the topology stabilizes and only the Root Bridge regularly transmits BPDUs.

#### Port Roles Configuration

1.  **Root Ports:**
    * Each non-root switch selects one port with the lowest path cost to the Root Bridge as its Root Port.
    * **Path Cost Calculation:** Based on the cumulative link speeds along the path to the root.
        * **Example Speed Costs:**
            * 10 Mbps = 100
            * 100 Mbps = 19
            * 1 Gbps = 4
            * 10 Gbps = 2

2.  **Designated Ports:**
    * In each collision domain between switches, the port on the switch with the lowest path cost to the root becomes the Designated Port and remains in forwarding state.
    * **Selection Criteria:**
        * Lowest Root Cost
        * Lowest Bridge ID on switch

3.  **Alternate Ports:**
    * Other ports in the same collision domain that are not chosen as designated are set to blocking state to prevent loops.
    * This ensures only one active path (a Designated Port) is used for data traffic, minimizing the risk of broadcast storms or loops.

#### Conflict Resolution

* In cases of ties in root path costs or bridge IDs:
    * **Neighbor's Bridge ID:** Lowest neighboring switch’s Bridge ID is considered.
    * **Neighbor's Port ID:** The specific port ID on the neighbor, incorporating both port priority and number, acts as a tie-breaker.

#### Special Considerations for Root Bridge

* All ports on a Root Bridge are inherently Designated Ports because they can directly forward packets without any intermediate devices.
* If multiple paths exist from a given switch to the Root Bridge, STP ensures only one is active at any time by selecting the optimal path based on the criteria mentioned above.

#### STP States and Functionalities

1.  **Blocking State:** No user data is forwarded; only BPDUs are sent/received. It's a stable state where the port doesn't participate in frame forwarding.
2.  **Listening State:** The switch processes BPDUs and awaits possible new information that warrants a topology change. No MAC addresses are learned in this state.
3.  **Learning State:** The switch begins to populate its MAC address table, but does not yet forward user data.
4.  **Forwarding State:** The switch forwards both user data and BPDUs. It fully participates in the active topology.
5.  **Disabled State:** The port does not participate in Spanning-tree forwarding or STP. It is effectively shut down.

#### STP Timers and Their Impact

* **Hello Time:** How often the Root Bridge sends a BPDU. Typically every 2 seconds.
* **Forward Delay:** The time spent in the Listening and Learning states. Commonly set to 15 seconds for each state.
* **Max Age:** The duration a BPDU is considered valid. If no new BPDU is received within this time, the existing BPDU is out and the switch may reconsider its own port roles and STP topology.

#### Port Role Transitions

* A non-designated port selected to become either a designated or root port will transition through the following states: Blocking → Listening → Learning → Forwarding. This total transition can typically take up to 50 seconds under default timer settings.

#### BPDU Management

* `Sw(config-if)# spanning-tree portfast bpdufilter default`: This command configures the interface to ignore BPDUs while PortFast is enabled, reverting to normal STP operation if a BPDU is received.

#### VLAN-Specific STP Configuration

* `Sw(config-if)# spanning-tree vlan [id] cost [value]`: Sets the path cost for sending BPDUs for a specific VLAN.
* `Sw(config-if)# spanning-tree vlan [id] priority [value]`: Sets the STP priority for a particular VLAN to influence root bridge selection.
* `Sw# spanning-tree mode [mstp | pvst | rapid-pvst]`: Configures the type of Spanning Tree Protocol to be used across the network.

#### Configuration Commands

* `Sw(config)# spanning-tree portfast default`: Globally enables the STP PortFast feature on all access ports. This should be used to skip the initial STP states for directly connected devices that do not result in network loops.
* `Sw(config-if)# spanning-tree bpdufilter enable/disable`: Enables or disables BPDU filtering on a specific interface. When enabled, it stops sending or receiving BPDUs on that port.

#### Command Examples

* `Sw# show spanning-tree VLAN-ID`: Displays STP details for a specified VLAN.
* `Sw# show spanning-tree detail`: Provides comprehensive details about the root bridge, time parameters, and port states for each VLAN.

These commands and settings are critical for managing how switches interact within a network, handling redundant paths, and ensuring there are no loops while maintaining optimal redundancy and failover capabilities.

Through the intelligent application of STP principles and careful configuration of bridge priorities and path costs, network administrators can effectively manage redundant paths and ensure robust network performance without loops. This makes STP a critical component in the design and operation of scalable, reliable Ethernet networks.

### Enhanced Spanning Tree Protocol (STP) Features and Configuration

#### 1. PortFast

* **Purpose:** Allows a port to immediately transition to the Forwarding state without going through the Listening and Learning states.
* **Usage Advice:**
    * Should only be enabled on ports connected to end hosts.
    * Enabling on a switch-to-switch connection could cause accidental Layer 2 loops.
    ```cli
    Sw(config-if)# spanning-tree portfast
    ```

#### 2. BPDU Guard

* **Function:** Prevents accidental topology changes by placing ports in an error-disabled state if BPDUs are received on PortFast-enabled ports where they should not be.
    ```cli
    Sw(config-if)# spanning-tree bpduguard enable
    ```

#### 3. BPDU Filter

* **Function:** Stops a switchport from sending or processing received BPDUs. Useful for ports connected directly to end devices where BPDUs are not expected.
    ```cli
    Sw(config-if)# spanning-tree bpdufilter enable
    ```

#### 4. Root Guard

* **Purpose:** Prevents a designated port from becoming a root port if a superior BPDU is received, ensuring the current switch retains its role as the root bridge.
    ```cli
    Sw(config-if)# spanning-tree guard root
    ```

#### 5. Loop Guard

* **Purpose:** Enhances STP stability in indirect link failure scenarios. If no BPDUs are received on a non-designated port that should be receiving them, Loop Guard puts the port into a loop-inconsistent state.
    ```cli
    Sw(config)# spanning-tree loopguard default
    ```

#### Configuration Examples

* **Enable PortFast on a Trunk Link:**
    * Use cases include connections to virtualization server hosts in different VLANs or a switchport connected to a Router (i.e. ROAS router-on-stick configurations).
    ```cli
    Sw(config-if)# spanning-tree portfast trunk
    ```

* **Error Recovery Setup:**
    * Re-enable an error-disabled port after addressing the underlying issue either manually or automatically.
    ```cli
    Sw(config)# errdisable recovery cause bpduguard
    Sw(config)# errdisable recovery interval 300
    ```

* **Priority Adjustment in STP:**
    * For designating primary or secondary root bridges in VLAN specific configurations.
    ```cli
    Sw(config)# spanning-tree vlan 11 root primary
    Sw(config)# spanning-tree vlan 12 root secondary
    ```

#### Summary

Each feature of STP serves to optimize network performance, prevent inadvertent network disruptions due to topology changes, and enhance security by controlling which ports participate in STP. Proper configuration and understanding of these features are critical to maintaining a stable and efficient network environment.

### Spanning Tree Protocol (STP) Enhancements and Configuration Tips

#### Root Guard

* **Purpose:** Protects your switch topology by preventing the switch from accepting superior BPDUs from switches outside your control. This is crucial when connecting LANs to external networks.
* **Behavior:** If a Root Guard-enabled port receives a superior BPDU, it will enter a "Root Inconsistent" state, effectively disabling the port until the superior BPDUs cease.
    ```cli
    Sw(config-if)# spanning-tree guard root
    ```

    To re-enable a port disabled by Root Guard:
    1.  Resolve the issue that triggered the guard (e.g., change priority settings on the other switch).
    2.  Wait for the BPDU max age timer (default 20 seconds) to expire; the port will then automatically recover.

#### Loop Guard

* **Purpose:** Prevents loop inconsistencies in unidirectional link scenarios where a port unexpectedly stops receiving BPDUs.
* **Implementation:** Should be enabled particularly on root and non-designated ports expected to receive BPDUs.
    ```cli
    Sw(config-if)# spanning-tree loopguard enable
    ```

    Recovery from Loop Guard:
    * Once a port starts receiving BPDUs again, it automatically transitions out of the "Loop Inconsistent" state.

#### BPDU Guard

* **Function:** Ensures that PortFast-enabled edge/access ports are protected against configuration mistakes that could introduce BPDUs into the network, putting the port into an error-disabled state.
    ```cli
    Sw(config-if)# spanning-tree bpduguard enable
    ```

    Manual recovery from BPDU Guard violation:
    * Administratively shut down and no shut down the port after resolving the configuration issue.

#### General STP Configuration Strategies

1.  **Optimal Traffic Flow:** To minimize latency, carefully select the root bridge based on stability and reliability to minimize congestion.
2.  **Handling External Connections:**
    * When connecting to external networks, ensure protection with Root Guard to maintain designated root roles within your network despite external influences.
3.  **Unidirectional Link Failures:**
    * Address potential physical layer issues (damaged cables, faulty connectors) that could cause unidirectional links which Loop Guard helps mitigate.

#### STP Configuration Commands Summary

* **Set a port's priority or designate a root bridge:**
    ```cli
    Sw(config)# spanning-tree vlan [vlan-id] priority [priority-value]
    Sw(config)# spanning-tree vlan [vlan-id] root primary|secondary
    ```

* **Recovery mechanisms:**
    ```cli
    Sw(config)# errdisable recovery cause [cause]
    Sw(config)# errdisable recovery interval [seconds]
    ```

#### Conclusion

Understanding and deploying STP enhancements correctly safeguards your network against unintentional loops and ensures optimal traffic flow through stable topology management. Each feature serves a specific purpose and should be configured according to the unique requirements of your network environment.

### Overview of Rapid Spanning Tree Protocol (RSTP) and Cisco Rapid PVST+

#### Key Concepts of RSTP (IEEE 802.1w)

* **Speed:** RSTP provides faster convergence compared to the classic STP by introducing a new handshake mechanism which allows ports to quickly transition between states.
* **Roles:** Introduces new port roles such as Alternate and Backup to improve network resilience.
* **Port States Simplification:** Merges STP's blocking, listening, and disabled states into a single discarding state.

### Port Roles in RSTP

1.  **Root Port:** The best (lowest cost) path from the switch to the root bridge.
2.  **Designated Port:** The port on each network segment that has the best path to the root bridge.
3.  **Alternate Port:** A backup port for the root port, providing an alternate path without the need to calculate spanning-tree topology.
4.  **Backup Port:** Serves as a backup for a designated port, typically used when multiple links are connected to the same collision domain.

#### Transition Enhancements in RSTP

* **Edge Ports:** Similar to PortFast in STP, directly transitions to forwarding state when connected to end devices.
* **Link Type:** Automatically determined as point-to-point or shared, influencing the BPDUs processing speed.

#### Cisco Rapid PVST+

* Extends RSTP by maintaining a separate spanning tree instance for each VLAN, allowing for better load balancing and redundancy over multiple VLANs.
* Faster convergence and individual control per VLAN enhance network tuning and performance optimization.

#### Configuration Commands for RSTP and Rapid PVST+

```cli
# Enter global configuration mode
Sw(config)#

# Set the spanning-tree mode to MST for Multiple instances or rapid-pvst for per VLAN RSTP calculation
Sw(config)# spanning-tree mode mst
Sw(config)# spanning-tree mode rapid-pvst

# Example to set link type on an interface, crucial for correct operation of RSTP
Sw(config-if)# spanning-tree link-type {point-to-point | shared }

# Set an interface as an edge port, equivalent to enabling PortFast
Sw(config-if)# spanning-tree portfast
```

#### Operational Differences Between STP and RSTP

* RSTP identifies and transitions certain ports immediately to the forwarding state without waiting for the full timer-based process, unlike STP.
* In scenarios with mixed environments (classic STP and RSTP), RSTP switches revert to STP on ports connected to STP-only switches.

### Summary

RSTP and Cisco’s Rapid PVST+ provide enhancements over traditional STP by offering quicker convergence times, more efficient handling of BPDU information, and specific improvements tailored to environments with multiple VLANs. Understanding these protocols and their configurations can significantly improve the robustness and responsiveness of your network infrastructure.

### Display Commands

* `SW3/RT#show ip interface brief` → Displays all the Router Interfaces.
* `SW/RT# Show Interfaces <ID>` → Displays specific interface information including duplex, speed and mac-address.
* `SW3/RT# show interfaces status` → Displays interfaces and their VLAN status (Trunk/Access/Routed Ports).
* `SW# show interfaces trunk` → Displays Information related to switchport configured as Trunk Ports.
* `SW# show vlan brief` → Displays the access interface ports assigned to each VLAN and not the trunk ports that allow each VLAN.
* `SW# show Spanning-Tree` → Displays Information {Root Bridge Information and the particular Switch/Bridge Information we queried via its CLI} about Spanning Tree Protocol for all VLANs that exist on the switch.
* `SW# show Spanning-Tree Vlan ID` → Displays Information about Spanning Tree Protocol for a specified VLAN.
* `SW# show Spanning-Tree Interface ID Detail` → Displays a more detailed/verbose Information about Spanning Tree Protocol for a specified Interface/switchport.
* `SW# Spanning-Tree mode ? {MST | PVST | Rapid-PVST}` → Sets the Spanning Tree Mode to MST, PVST, Rapid-PVST.
* `SW# show Spanning-Tree Detail` → Displays a more detailed/verbose Information about Spanning Tree Protocol for all VLANs that exist on the switch and an exact Root cost.
* `SW# Show interface Switchport`
* `SW# Show interface ID Switchport`
    * **Name:** The interface identifier per specific interface ID (f0/1 or g0/1).
    * **Administrative Mode:** The configured VLAN trunking mode (e.g., dynamic auto, dynamic desirable, trunk, access).
    * **Operational Mode:** The actual operational state of the interface (e.g., static access, trunking).
    * **Administrative Trunking Encapsulation:** The specified trunking encapsulation protocol (dot1q, isl, negotiate).
    * **Operational Trunking Encapsulation:** The operational trunking encapsulation protocol.
    * **Negotiation of Trunking:** Whether the trunking is set to on, off, or negotiating.

* `SW(config-if)# Spanning-Tree Portfast` → Enables Portfast on Specified Interfaces. Should only be enabled on interfaces connected to end Hosts (PC/Laptop)-Access Ports; and not interfaces connected to HUBS/SWITCHES/BRIDGES -Trunk Ports etc; can cause temporary bridging loops.
* `SW(config-if)# Spanning-Tree Portfast Trunk` → Enables Portfast on Trunk Interfaces. Should only be enabled on interfaces {connected to Virtualization Server with VMs in Separate VLANs OR connected to a Router via ROAS}.
* `SW# Spanning-Tree Portfast default` → Enables Portfast on all Access Ports, doesn’t enable it on Trunk Ports, as these interfaces are connected to other switches In the network topology.
* `SW(config-if)# Spanning-Tree bpduguard enable|disable` → This command enables/disables BPDU Guard on a specific interface, helping to protect the network from unwanted STP changes and ensuring that only designated switchports (Ports connected to other Switches) participate in the Spanning Tree process.
* `SW(config-if)# Spanning-Tree bpdufilter enable|disable` → This command enables/disables BPDU filter on a specific interface, stops a switchport from sending BPDUs or processing received BPDUs.
* `SW# Spanning-Tree portfast bpduguard default` → Enables BPDUGuard on all Portfast-enabled interfaces.
* `SW# Spanning-Tree Vlan ID root primary` → Sets a particular VLAN to become the root bridge by automatically reducing its Bridge Priority, thereby making it the lowest Bridge ID in the network.
* `SW# Spanning-Tree Vlan ID root secondary` → Sets a particular VLAN to become the secondary root bridge.
* `SW# Spanning-Tree Vlan ID Priority ?[4096 increments allowed {0-61440}]` → Manually Sets a particular VLAN Bridge Priority.
* `SW# Spanning-Tree guard root` → Sets/enables RootGuard on all STP ports, doesn’t have (config-if) versions.
* `SW(config-if)# Spanning-Tree guard loop | none` → Enables/disables loop guard on a specific Non-Designated Switchports.
* `SW# Spanning-Tree loopguard default` → Enables loop guard across all Non-Designated Switchports, this command reverses or nullifies the spanning-tree guard root.

### Notes:

* **PortFast** accelerates the convergence of network switches connected directly to end devices by immediately transitioning ports into the forwarding state, bypassing the traditional listening and learning phases.
* It's crucial to ensure that **PortFast** is only enabled on ports connected to single hosts to prevent potential network loops.
* **Ports**: Refers to the network ports where these tools are typically enabled or applicable.
* **Re-enablement Method**: Describes how the tool or feature is reactivated after being triggered or disabled.
* **Error Type in Terminal**: Represents a simplified example of what an error message might look like when issues arise related to each respective tool.


## Overview of EtherChannel and Port Aggregation

EtherChannel is a technology used in networking to combine multiple physical links between two network devices into a single logical link. This aggregation enhances bandwidth and provides redundancy without causing layer 2 loops that protocols like STP aim to avoid.

#### Why EtherChannel?
- **Increased Bandwidth**: By combining multiple network connections, the overall data path bandwidth increases.
- **Redundancy**: Provides redundancy for higher availability by aggregating multiple physical links.
- **Load Balancing**: Efficiently distributes network traffic across all available links in the channel, preventing any single link from being overloaded.

#### Types of EtherChannel
1.  **Static EtherChannel**: Manually configured, without any protocol negotiation.
2.  **PAgP (Port Aggregation Protocol)**: Cisco proprietary protocol that dynamically forms an EtherChannel if another PAgP device is detected.
3.  **LACP (Link Aggregation Control Protocol - IEEE 802.3ad)**: An industry standard method, more flexible and widely supported than PAgP.

#### Configuration Commands

| Command | Description |
| :------ | :---------- |
| `interface port-channel 1` | Creates or selects a port-channel interface. |
| `port-channel load-balance src-dst-ip` | Sets the EtherChannel load-balancing method based on source and destination IP addresses. |
| `interface range fa0/0-8` | Selects a range of interfaces for configuration. |
| `channel-group 1 mode active` | Adds interfaces to channel group 1 and sets the EtherChannel mode to active (LACP). |

#### Modes of Operation
-   **Active**: Unconditionally sends LACP packets (for LACP).
-   **Passive**: Waits to receive LACP packets before sending them (for LACP).
-   **Desirable**: Actively seeks to form an EtherChannel using PAgP.
-   **Auto**: Waits for PAgP packets to be received before responding.
-   **On**: Forces the port channel without a protocol negotiation.

#### Common Configuration Scenarios
-   `desirable + auto` = EtherChannel formed (PAgP)
-   `active + passive` = EtherChannel formed (LACP)
-   `auto + auto` = No EtherChannel (PAgP)
-   `passive + passive` = No EtherChannel (LACP)

#### EtherChannel Load-Balancing
Decides which port to use for each data flow. Factors influencing this decision might include:
-   Source and destination MAC addresses
-   Source and destination IP addresses
-   Combination of source and destination IPs and MACs

The choice of load balancing method can significantly impact the distribution of traffic across the links in an EtherChannel.

### EtherChannel Configuration and Guidelines

EtherChannel aggregates multiple physical interfaces into a single logical interface to enhance bandwidth and provide redundancy. Understanding the configuration requirements and ensuring consistency among member interfaces is crucial for proper operation.

#### Configuration Requirements for EtherChannel Members
-   **Duplex Settings**: All interfaces must operate at the same duplex mode.
-   **Speed**: All member interfaces must have the same speed settings.
-   **Switchport Mode**: Interfaces need to be configured in the same switchport mode (e.g., all access or all trunk).
-   **VLAN Settings**: For trunk modes, allowed VLANs must be consistent across all member interfaces.

#### Commands to Verify EtherChannel Configuration

| Command | Description |
| :------ | :---------- |
| `show etherchannel summary` | Displays a summary of all port-channels configured on the switch, including their status and associated physical ports. |
| `show etherchannel load-balance` | Displays the current method used for load balancing across EtherChannels. |

If there are discrepancies in the configuration of interfaces intended for an EtherChannel, they will not be eligible for inclusion in the EtherChannel group. This ensures stability and prevents issues like loops or mismatched traffic handling.

#### Compatibility Description

| Mode      | Compatible With   |
| :-------- | :---------------- |
| On        | Static Mode Only  |
| Active    | Active, Passive   |
| Passive   | Active Only       |
| Desirable | Auto, Desirable   |
| Auto      | Desirable Only    |

Choosing the correct mode and protocol is essential for forming a stable EtherChannel link between switches.

### Summary
Proper configuration and consistency across all member interfaces are key to successfully implementing an EtherChannel. By following these guidelines and using the appropriate commands, administrators can ensure high availability, increased bandwidth, and efficient use of infrastructure resources in their network environments.
EtherChannel is essential for optimizing the use of physical links between switches, enhancing both bandwidth utilization and network redundancy. Depending on the network requirements and equipment, administrators can choose between static configuration or dynamic protocols (PAgP or LACP) to manage EtherChannels efficiently.

| Command | Description |
| :------ | :---------- |
| `show etherchannel summary` | This command displays a summary of all port-channels configured on the switch including their status and associated physical ports. |
| `show etherchannel detail` | Provides detailed information about each port-channel, including protocol, member ports, and their individual statuses. |
| `show etherchannel load-balance` | Displays the current method used for load balancing across EtherChannels. |
| `show running-config interface Port-channel1` | Shows the running configuration specific to the Port-channel interface. |
| `port-channel load-balance <method>` | Enables EtherChannel Load Balancing Method. |
| `src-ip` | Balances based on source IP address. |
| `dst-ip` | Balances based on destination IP address. |
| `src-dst-ip` | Balances based on both source and destination IP addresses. |
| `src-mac` | Balances based on source MAC address. |
| `dst-mac` | Balances based on destination MAC address. |
| `src-dst-mac` | Balances based on both source and destination MAC addresses. |
| `src-port` | Balances based on source port. |
| `dst-port` | Balances based on destination port. |
| `src-dst-port` | Balances based on both source and destination ports. |

#### Layer 3 Switch EtherChannel Configuration on Routed Ports

| Command | Description |
| :------ | :---------- |
| `interface range GigabitEthernet0/1 - 2` | Selects a range of GigabitEthernet interfaces. |
| `no switchport` | Configures the physical interfaces as Layer 3 (routed) ports. |
| `channel-group 1 mode active { auto | desirable | passive | on}` | Command to set the channel protocol and mode for the interfaces. |
| `interface Port-channel2` | Selects or creates port-channel interface 2. |
| `no switchport` | Configures the port-channel interface as Layer 3 (routed). |
| `ip address 192.168.1.1 255.255.255.0` | Assigns an IP address and subnet mask to the port-channel interface. |

#### Layer 3 EtherChannel Configuration Steps

| Command | Description |
| :------ | :---------- |
| `interface range g0/1-3` | Selects a range of GigabitEthernet interfaces. |
| `no switchport` | Configures these interfaces as Layer 3 (Routed) ports. |
| `ip routing` | Enables IP routing on the switch (global configuration). |
| `channel-group 1 mode active` | Creates channel group 1 and sets LACP active mode for the interfaces in the range. |
| `interface port-channel 1` | Enters the port-channel interface configuration mode. |
| `ip address [ipAddr] [Netmask]` | Assigns an IP address and subnet mask to the port-channel interface. |

This setup uses IP address directly assigned to the port-channel, facilitating easier management and routing capabilities across the network.

#### Setting the Channel Protocol
The EtherChannel aggregation protocol (PAgP/LACP) must be uniform across all devices in the EtherChannel. If explicitly set, each switch port in the bundle must support the selected protocol.


# CHAPTER 11: ROUTERS (LAYER 3) 

## Router Basics

A **Router** is a multi-homed Intermediate System with Network Links and Topology Information to facilitate forwarding packets between subnets, to or around an internetwork.

Information about the location of other IP networks and hosts is stored in the **Routing Table**. Each entry represents an available path to its destination network or hosts. The key components that define an entry in the routing table are:

| Component             | Description                                                                 |
| :-------------------- | :-------------------------------------------------------------------------- |
| **Protocol** | The protocol implemented by the Router (e.g., OSPF, RIP, EIGRP, BGP, Static, Connected). |
| **Destination** | Routes can be defined to specific hosts but are more generally directed to Network IDs (Network ID / Host Address / Network Broadcast Address). |
| **Interface** | The local interface to use to forward a packet along the chosen route.      |
| **Gateway / Next Hop**| The IP address of the next router along the path to the destination.        |
| **Metric** | A value used to determine the best path among multiple routes to the same destination. |
| **Administrative Distance (AD)** | A value used to express the relative trustworthiness of the protocol supplying the route. |

### Routing Table Entry Categories

Routing Table Entries fall into four general categories:

| Category                     | Description                                                                                             |
| :--------------------------- | :------------------------------------------------------------------------------------------------------ |
| **Direct Network Routes** | For subnets to which the Router is directly attached. The IP Network or Subnet for each active Router Interface is automatically added. Also known as **Directly Connected Routes**. |
| **Remote Network Routes** | For subnets and IP Networks that are not directly attached. Learned through a routing protocol or static configuration. Typically have a mask length less than `/32`. |
| **Host Routes** | For routes to a specific Host IP Address. A host route has a `/32` prefix for IPv4 or `/128` prefix for IPv6. |
| **Default Routes** | Used when an exact match for a network or host route is not found. Also known as the **Gateway of Last Resort** (`0.0.0.0/0` for IPv4 or `::/0` for IPv6). |

### Configured Routes (Static & Default)

#### Static vs. Default Routes

| Feature         | Static Routes                                           | Default Routes                                  |
| :-------------- | :------------------------------------------------------ | :---------------------------------------------- |
| **Configuration** | Manually added by administrator.                        | A special type of static route.                 |
| **Purpose** | Directs traffic to a specific network or host.          | Catches all traffic not matched by other routes. |
| **Destination** | Specific Network ID/Prefix or Host IP.                  | `0.0.0.0/0` (IPv4) or `::/0` (IPv6).             |
| **Persistence** | Can be persistent (survives reboot) or non-persistent.  | Typically persistent.                           |
| **Reachability**| Disabled if not reachable.                              | Operates as "Gateway of Last Resort".           |

#### Floating Static Routes

A floating static route is a static route with an administrative distance higher than that of a dynamic route to the same destination. It remains inactive in the routing table until the dynamic route is removed or becomes unavailable. This setup provides a backup path, ensuring continuity if the primary route fails. Floating static routes are used as backup routes to dynamic routes learned via protocols like OSPF or EIGRP. They are configured with a higher Administrative Distance (AD) than the primary route to ensure they are only used when the primary route fails.

### Packet Forwarding (IP Layer 3)

When a Router Receives a packet, it reads the destination address in the packet and looks up a matching destination network IP address and prefix in its Routing table (Topology Database). If there is a match, the Router will forward the packet out of one of its interfaces by Encapsulating the packet in a new frame.

**Frame Encapsulation based on Destination:**

1.  **For directly connected networks via an Ethernet Interface:** The Router uses ARP (IPv4) or Neighbor Discovery (IPv6) to determine the interface address (MAC) of the destination host.
2.  **For packets that can be forwarded via a gateway over an Ethernet interface:** It inserts the next hop router's MAC address into the new frame.
3.  **For packets where the destination address cannot be matched to a Route table entry:** The packet is either forwarded via the default route (Gateway of Last Resort) or dropped.

* **NOTE:** Switches do NOT count as hops.
* **NOTE:** Routers do NOT forward broadcast traffic.

#### Hop Count & Time To Live (TTL) Comparison

| Feature      | IPv4 (Time To Live - TTL)                                       | IPv6 (Hop Limit)                                              |
| :----------- | :-------------------------------------------------------------- | :------------------------------------------------------------ |
| **Behavior** | Decremented by at least 1 at each router.                       | Decremented by 1 at each router.                              |
| **Purpose** | Prevents packets from endlessly circulating; nominally time unit, practically hop count. | Prevents packets from endlessly circulating; strictly hop count. |
| **Discard** | Packet discarded when TTL reaches 0.                            | Packet discarded when Hop Limit reaches 0.                    |

---

### Fragmentation

| Feature      | IPv4                                                          | IPv6                                                          |
| :----------- | :------------------------------------------------------------ | :------------------------------------------------------------ |
| **Fragmentation**| IP can fragment packets to fit within the MTU.           | Does not allow/perform fragmentation at the router level.       |
| **Fields Used**| ID, Flags, Fragment Offset IP header fields for reassembly. | N/A                                                           |
| **MTU Handling**| Router handles fragmentation.                                 | Host performs **Path MTU Discovery** to determine smallest MTU along path and crafts packets accordingly. |

---
### Brief Introduction to ICMP and ARP

#### ICMP Overview
- ICMP (Internet Control Message Protocol) is used in networks to diagnose network communication issues and operate management queries. It facilitates messages related to network operations, errors, and diagnostics.

#### Initial ICMP R&Q Timeout
- The Initial ICMP Request and Query (R&Q) timeout can occur if ARP (Address Resolution Protocol) has not yet resolved the destination MAC address. Since ICMP relies on IP addresses, ARP must first map the IP address to a MAC address for network-layer communication.

#### ARP Details
- ARP (Address Resolution Protocol) is utilized to discover the Layer 2 address (MAC address) of a known Layer 3 address (IP address).

| ARP Message | Direction             | Purpose                                                |
| :---------- | :-------------------- | :----------------------------------------------------- |
| **ARP Request** | Broadcast to local segment | Asks which host has a specific IP address.             |
| **ARP Reply** | Unicast response      | From the host with the requested IP, providing its MAC. |

*Command to view ARP table:* `show arp` or `show ip arp`

#### ICMP Echo Request and Reply
| ICMP Type       | Purpose                                                    |
| :-------------- | :--------------------------------------------------------- |
| **Echo Request (Ping)** | Measures round-trip time to a destination host.          |
| **Echo Reply** | Confirms reachability and provides round-trip time.        |

#### Network Addressing Basics
| IP Address Type          | Host Portion Bits | Description                                           |
| :----------------------- | :---------------- | :---------------------------------------------------- |
| **Network Address** | All 0s            | Identifies the network itself; cannot be assigned to a host. |
| **Broadcast Address** | All 1s            | Used to communicate with all hosts within that subnet. |
| **First Usable Address** | After network address | First valid assignable IP for a host.                 |
| **Last Usable Address** | Before broadcast address | Last valid assignable IP for a host.                  |

#### Example Router Configuration Commands
Here's a breakdown of common router interface configuration commands:

| Command                                      | Description                                                                                                    |
| :------------------------------------------- | :------------------------------------------------------------------------------------------------------------- |
| `RT(config)# interface g0/0`                 | Enters interface configuration mode for GigabitEthernet 0/0.                                                 |
| `RT(config-if)# description "Link to ISP"`   | Sets a descriptive text for the interface.                                                                     |
| `Router(config-if)# ip address 43.109.23.12 255.0.0.0` | Configures the IPv4 address and subnet mask on the interface.                                            |
| `Router(config-if)# no shutdown`             | Activates the interface.                                                                                       |
| `Router(config)# ipv6 unicast-routing`       | **Global Command:** Enables IPv6 routing on the router (required for forwarding IPv6 packets).                 |
| `Router(config-if)# ipv6 enable`             | Enables IPv6 on an interface and automatically assigns a Link-Local Unicast IPv6 Address.                      |
| `Router(config-if)# ipv6 address 2001:db8:0:0::1/64` | Configures a Global Unicast IPv6 address with a specified prefix.                                            |
| `Router(config-if)# ipv6 address autoconfig` | Lets the router interface obtain an IPv6 address using stateless autoconfiguration (SLAAC); uses NDP to learn prefix. |
| `Router(config-if)# ipv6 address 2001:db8:0:1::/64 EUI-64` | Configures a Global Unicast IPv6 address where the 64-bit host portion is generated using EUI-64 from the MAC address. |
| `do show ip interface brief`                 | Shows a summary of IPv4 interfaces and their status (executed from any mode with `do`).                      |
| `do show ipv6 interface brief`               | Shows a summary of IPv6 interfaces and their status (executed from any mode with `do`).                      |

### Understanding Connected and Local Routes

When you configure an IP address on a router interface and bring it up, two types of routes are automatically created in the routing table:

| Route Type       | Description                                                               | Example for `192.168.1.1 255.255.255.0` on `GigabitEthernet0/2` |
| :--------------- | :------------------------------------------------------------------------ | :--------------------------------------------------------------- |
| **Connected Route** | Represents the network or subnet to which the interface is directly attached. | `192.168.1.0/24` directly connected, GigabitEthernet0/2          |
| **Local Route** | Represents the specific IP address assigned to the interface itself. It's a host route to the interface's own IP. | `192.168.1.1/32` is directly connected, GigabitEthernet0/2        |

### Setting Up Static and Default Routes and Floating Routes:

| Route Type                  | IPv4 Command Syntax                                    | IPv6 Command Syntax                                                         | Notes                                                              |
| :-------------------------- | :----------------------------------------------------- | :-------------------------------------------------------------------------- | :----------------------------------------------------------------- |
| **Static Route** | `ip route [destination] [subnet mask] [next-hop-addr | exit-interface]` | `ipv6 route [destination/prefix] {next-hop-addr | exit-interface [next-hop]}` | Manually configured, specific to a destination.                    |
| **Floating Static Route** | `ip route [destination] [Netmask] [next-hop | exit-interface] [ad]` | `ipv6 route [destination/prefix] {next-hop-addr | exit-interface} [ad]` | `ad` (administrative distance) is higher than primary route.       |
| **Default Route** | `ip route 0.0.0.0 0.0.0.0 [next-hop-addr | exit-interface]` | `ipv6 route ::/0 {next-hop-addr | exit-interface}`                            | "Gateway of Last Resort" for unmatched traffic.                    |
| **Directly Attached Static (IPv6)** | N/A                                                    | `ipv6 route [destination/prefix] [exit-interface]`                            | Cannot be used with Ethernet interfaces in IPv6.                   |
| **Recursive Static (IPv6)** | N/A                                                    | `ipv6 route [destination/prefix] [next-hop-addr]`                             | `next-hop-addr` must be routable (not link-local).                 |
| **Fully Specified Static (IPv6)** | N/A                                                    | `ipv6 route [destination/prefix] [exit-interface] [next-hop-addr]`            | Most explicit; good for multi-access segments.                     |

---

### Supernetting & Subnetting Overview

#### CIDR (Classless Inter-Domain Routing)
- Allows for flexible division of networks by eliminating the strict boundaries of classful addressing.
- Uses notation `/x` to denote the number of bits used for the network portion.

#### Classful Addressing
Based on the first octet, IP addresses were divided into classes with default subnet masks:

| Class | First Octet Range | Default Subnet Mask (Decimal) | Default Subnet Mask (CIDR) |
| :---- | :---------------- | :---------------------------- | :------------------------- |
| **A** | 0-127             | `255.0.0.0`                   | `/8`                       |
| **B** | 128-191           | `255.255.0.0`                 | `/16`                      |
| **C** | 192-223           | `255.255.255.0`               | `/24`                      |


### Router Placement & Types

Routers serve both to link physically Remote networks and subdivide IP networks into multiple subnets. Router placement is generally driven by:

1.  Hosts with Addresses in the same subnet (IP network) mustn't be separated by a Router.
2.  Hosts with Addresses in different subnets (IP network) must be separated by a Router.

#### Edge Routers

**Edge Routers** are placed at the network perimeter (WAN side) to distinguish External (Internet) and Internal Interfaces. They perform framing to repackage data from the private LAN Frame format to the WAN/Internet access frame format.

* The Customer's Router is referred to as **Customer Edge (CE)**.
* The Service Provider Router is referred to as **Provider Edge (PE)**.

Edge Routers designed to work with DSL or cable broadband are often called **SOHO Routers**. Edge Routers with similar integrated functionality are also deployed by Enterprises for Branch Office Connectivity, which are designed to service medium to large networks with specialized processors to handle Routing & path forwarding processes, and memory to buffer data. They also support plug-in cards for WAN Interfaces and Site-to-Site VPN.

#### Internal Routers

An **Internal Router** has no public-facing interface to the Internetwork. They serve to implement whatever network topology is required, meaning that traffic between the local subnets (LAN) is controlled by a separate Internal Router.

Many networks are segmented using the **Virtual LANs (VLANs)** feature of managed Switches. Traffic between VLANs is Routed in two scenarios:

1.  **Using a Router with a single Interface Connected to a Trunk Port on the switch:** The Router's physical Interface is Configured with multiple "**SUBINTERFACES**". Each subinterface is configured with a specific VLAN ID. The Sub Interface routes traffic for a given VLAN and receives traffic from a given VLAN via the TRUNK PORT. The Sub Interface serving the destination VLAN receives traffic from the router. (This scenario does not scale well for tens of VLANs).

2.  **A Layer 3 Capable Switch:** This is one that is optimized for Routing between VLANs. They can use static or dynamic Routing to identify which VLAN an IP Address should be forwarded to, and maintain a mapping table of IP and MAC addresses, thereby using low-latency Hardware-based forwarding. However, they do not typically have WAN interfaces and are not usually used for Routing at the network edge.
    * A subinterface for each VLAN is created over the trunk. Each subinterface must be configured with an IP address and mask for the subnet mapped to the VLAN.


### Router Configuration

Routers are configured either via a Serial Connection (Console port) OR remotely over the network using SSH or Telnet with the Router via the IP Address of any configured Interface. Due to unforeseen Hardware Faults, best practice is to create a **Virtual Interface (Loopback Interface)** and assign it an IP address for use in remotely managing the Router. This is a way of giving the Router an internal IP Address not connected to any physical network, and therefore not reliant on a specific network link being available.

Principal Configuration tasks:

1.  Apply an IP configuration to each of its interfaces.
2.  Configure one or more Routing protocols or static routes to serve the Router's function.


### Viewing & Modifying Routing Tables on End Systems

* The `show route`, `show ip route`, `show ipv6 route` commands output the active Routing Table on Cisco Routers.
* The **`route` command** is used to view or modify the Routing table of End System (Linux and Windows) hosts. The routing table for an end system generally conforms to a single entry for the default route. Traffic that isn't addressed to the local subnet is sent over this default route.

#### Command Syntax Examples (Windows & Linux)

* **Windows:**
    * `Route [–p] add [Dest IP] mask [Netmask] [Gateway IP] metric [Metric Value] IF [Interface]`
* **Linux (using `ip route` which replaced deprecated legacy command-line tools):**
    * `ip route add [Dest IP] via [Gateway IP] dev [Interface]`
    * `ip route add [Dest IP]/[Netmask Value] via [Gateway IP] dev [Interface]`

#### Variables in the Syntax:

* **Destination IP:** A network or host address.
* **Netmask:** The subnet mask for Destination IP.
* **Gateway IP:** The Router to use to contact the network or host address.
* **Metric Value:** The cost of the Route.
* **Interface:** The adapter (NIC) the host should use (used if the host is multi-homed).

Routes added in this manner are non-persistent by default. Using the `-p` switch in Windows, routes can be permanently configured. In Linux, the command above cannot be used directly to add persistent (permanent) routes without additional configuration.

## Subnetting

Subnetting is the process of dividing a single large network into smaller, logical subnetworks. This improves network performance, security, and IP address management.

#### Subnet Masking Approaches

| Approach | Description                                          | Key Characteristic                             |
| :------- | :--------------------------------------------------- | :--------------------------------------------- |
| **FLSM (Fixed Length Subnet Mask)** | All subnets created use the same subnet mask. | Simpler to manage, but can waste IP addresses. |
| **VLSM (Variable Length Subnet Mask)** | Subnets can have different sizes, allowing for more efficient use of IP space. | More complex to manage, but optimizes IP usage. |

#### Practical Subnet Examples

| Subnet Mask | Common Use Case           | Number of Usable IPs | Total Addresses | Network Address | Broadcast Address |
| :---------- | :------------------------ | :------------------- | :-------------- | :-------------- | :---------------- |
| **/31** | Point-to-point links (2 routers) | 2                    | 2               | No (implied)    | No (implied)      |
| **/30** | Point-to-point links      | 2                    | 4               | Yes             | Yes               |

### Network Design Using VLSM Example:

Given a parent network of `192.168.1.0/24`, dividing this into multiple subnets could look like this:

| Subnet ID           | CIDR | Usable Hosts | Total Addresses | Network Address    | Broadcast Address    |
| :------------------ | :--- | :----------- | :-------------- | :----------------- | :------------------- |
| **First Subnet** | `/25`| 126          | 128             | `192.168.1.0`      | `192.168.1.127`    |
| **Second Subnet** | `/26`| 62           | 64              | `192.168.1.128`    | `192.168.1.191`    |
| **Third Subnet** | `/27`| 30           | 32              | `192.168.1.192`    | `192.168.1.223`    |
| **Fourth Subnet** | `/28`| 14           | 16              | `192.168.1.224`    | `192.168.1.239`    |
| **Point-to-Point** | `/30`| 2            | 4               | `192.168.1.240`    | `192.168.1.243`    |

### Key Considerations:

* **Number of Hosts vs. Number of Subnets**:
    * Increasing the number of network bits (`prefix length`) decreases the number of available hosts but increases the number of possible subnets within the given address space.
* **Supernetting**:
    * Used to summarize multiple contiguous subnets into a single network advertisement.
    * Reduces the complexity in routing tables by aggregating several smaller networks into a larger one using a shorter subnet mask.

This structured approach to subnetting and supernetting helps organizations efficiently utilize their assigned IP address spaces, tailoring network divisions to actual usage needs, ensuring both flexibility and scalability.

---

### Interface Configuration

Interface configuration is crucial for setting up how a router or multilayer switch interacts with different network segments.

#### Common Interface Configuration Commands

| Command                                        | Context                                      | Description                                                                                                                                              |
| :--------------------------------------------- | :------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `interface G0/1.10`                            | Sub-interface (Router/L3 Switch)             | Enters sub-interface configuration mode for interface G0/1, associated with VLAN 10. Used for Router-on-a-Stick or inter-VLAN routing.                     |
| `interface G0/1`                               | Physical Interface (Router/Switch)           | Selects a particular physical interface (e.g., GigabitEthernet 0/1) for configuration.                                                                   |
| `no switchport`                                | L3 Switch Interface (Global Config)          | Configures or upgrades the selected interface as a "Routed Port" (Layer 3 functionality), removing its Layer 2 switching capabilities.                 |
| `ip address IPAddress Netmask`                 | Interface (Router/L3 Switch)                 | Sets the IPv4 address and subnet mask for the interface. `IPAddress` must be a usable host address within the subnet range.                             |
| `no shutdown`                                  | Interface (Router/L3 Switch)                 | Enables or activates the interface.                                                                                                                      |
| `ipv6 unicast-routing`                         | Global (Router/L3 Switch)                    | **Global Command:** Enables IPv6 routing on the device, allowing it to forward IPv6 packets.                                                             |
| `ipv6 enable`                                  | Interface (Router/L3 Switch)                 | Enables IPv6 on an interface and automatically assigns a Link-Local Unicast IPv6 Address. Does not configure a Global Unicast Address.                   |
| `ipv6 address 2001:db8:0:0::1/64`              | Interface (Router/L3 Switch)                 | Configures a Global Unicast IPv6 address with a specified prefix on the interface.                                                                       |
| `ipv6 address autoconfig`                      | Interface (Router/L3 Switch)                 | Allows the router interface to obtain an IPv6 address using stateless autoconfiguration (SLAAC). Device uses NDP to learn the prefix.                      |
| `ipv6 address 2001:db8:0:1::/64 EUI-64`        | Interface (Router/L3 Switch)                 | Configures a Global Unicast IPv6 address where the 64-bit Host Portion is generated using EUI-64 from the interface's 48-bit MAC address.                |

---

### IP Routing and ARP

#### ARP Table Commands

| Command   | Description                   |
| :-------- | :---------------------------- |
| `show arp`| Displays the device's IPv4 ARP table. |
| `show ip arp` | Same as `show arp`.           |

#### Routing Enablement and Route Configuration Commands

| Command                                           | Context          | Description                                                                                                                                                                                                |
| :------------------------------------------------ | :--------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ip routing`                                      | Global (L3 Switch) | Enables Layer 3 routing on a multilayer switch, allowing it to build and use an IP routing table.                                                                                                          |
| `ip route 0.0.0.0 0.0.0.0 [Interface-ID | Interface-IP]` | Router/L3 Switch | Configures a Default Route (Gateway of Last Resort) for IPv4. Traffic not matching more specific routes is sent here. `Interface-ID` refers to the local outgoing interface, `Interface-IP` is the next hop. |
| `ipv6 route ::/0 [Interface-ID | Interface-IP]` | Router/L3 Switch | Configures a Default Route (Gateway of Last Resort) for IPv6.                                                                                                                                              |
| `ip route NetworkAddress NetMask {Next-hop-Addr | ExitInterface}` | Router/L3 Switch | Configures a Static Route for IPv4. Can specify a next-hop IP address or an exit interface.                                                                                                |
| `ipv6 route NetworkAddress/Prefix {Next-hop-Addr | ExitInterface}` | Router/L3 Switch | Configures a Static Route for IPv6.                                                                                                                                                        |
| `ip route NetworkAddress NetMask Next-hop-Addr AD` | Router/L3 Switch | Configures a Floating Static Route for IPv4. The `AD` (Administrative Distance) must be higher than the primary route's AD.                                                                        |
| `ipv6 route NetworkAddress/Prefix {Next-hop-Addr | ExitInterface} AD` | Router/L3 Switch | Configures a Floating Static Route for IPv6.                                                                                                                                               |

#### Important Considerations for Interface IP Addresses

| Invalid IP Address Assignment | Valid IP Address Assignment | Rationale                                                                                                   |
| :---------------------------- | :-------------------------- | :---------------------------------------------------------------------------------------------------------- |
| Network Address (e.g., `192.168.1.0/24`) | First Usable Address      | Network address identifies the network itself and cannot be assigned to a host or interface.                  |
| Broadcast Address (e.g., `192.168.1.255/24`) | Last Usable Address       | Broadcast address is reserved for sending data to all hosts on the subnet.                                  |
| IP outside subnet range     | Within defined subnet       | An IP address must belong to the subnet defined by the configured mask for proper communication.            |

*When setting up router interfaces, always ensure the IP address assigned:*
* Is not a network address (first address in the block).
* Is not a broadcast address (last address in the block).
* Falls within the correct subnet as defined by the subnet mask.

This understanding will help prevent errors like "Bad mask" and ensure proper communication within and between subnets.


##  Dynamic Routing Protocols

Complex Networks need to exchange Routing information rapidly to prevent outages, making static Routing updates impractical in most cases.

A **Dynamic Routing Protocol** uses an algorithm (categorized according to Topology & Metrics) to BUILD & maintain a Routing Information database. (These databases are separate from the Routing table). Most algorithms are classed as either **Distance Vector** OR **Link State** OR **Both (Hybrid)**.

The database might contain more than one Route to the Same Destination. In this case, a **metric** is used to determine which path will be selected for use in the IP Routing table. The path with the lowest cost metric is preferred.

### Convergence

**Convergence** is the process whereby Routers using dynamic routing protocols agree on the network Topology. Network Routers must be able to communicate changes to other routers quickly to avoid **Black Holes** (where a packet is discarded without notice given back to the source) and **loops** (where a packet is forwarded around the network until its TTL Expires, and an "ICMP Time Exceeded" notification is sent to the source).

A Network where all routers share the Same Topology is described as **Steady State**. The time taken to reach steady state is a measure of a protocol's Convergence performance.

**Route flapping** refers to a Router changing the properties of a Route it's advertising quickly, often leading to serious convergence problems. A flapping interface frequently changes from offline → online and vice versa.


### Autonomous Systems (AS) & Gateway Protocols

A Network under the administrative control of a single owner is referred to as an **Autonomous System (AS)**. An "AS" identifies a group of network prefixes.

* An **Interior Gateway Protocol (IGP)** is one that identifies Routes within an AS. (e.g., OSPF, EIGRP, RIP)
* An **Exterior Gateway Protocol (EGP)** is one that can advertise Routes between Autonomous Systems. An EGP includes a field to commit a network's Autonomous System ID and allows Network Owners to determine whether they can use paths through another organization's network. Used on the Internet backbone. (e.g., BGP)

Another factor comparing Routing protocols is whether they support Classless Addressing.


### Routing Protocol Comparison Table

| Protocol              | Class / Port #   | Type / Algorithms             |
| :-------------------- | :--------------- | :---------------------------- |
| Routing Information Protocol (RIP) | UDP 520 / 521 | Distance Vector               |
| Enhanced Interior Gateway Routing Protocol (EIGRP) | IP Protocol #88 | Distance Vector / Hybrid      |
| Open Shortest Path First (OSPF) | IP Protocol #89 | Link State                    |
| Border Gateway Protocol (BGP) | TCP 179          | Path Vector (Hybrid of DV/LS) |


### Route Selection Process

If a Router has multiple entries to similar networks in a Routing Table, it must determine which route to prefer. Preference is first based on the **LONGEST ADDRESS PREFIX MATCH OVER SHORTER ONES**. E.g., `198.51.100.0/28` is preferred over `198.51.100.0/24`. A longer prefix means fewer host IDs.

The next key point is **ADMINISTRATIVE DISTANCE (AD)**. AD Value is used to express the relative trustworthiness of the protocol supplying the Route. Default AD Values are hard coded into the router & can be adjusted by the administrator if necessary.

| Route Type             | Default AD (Cisco) |
| :--------------------- | :----------------- |
| Connected              | 0                  |
| Static                 | 1                  |
| EIGRP Summary Route    | 5                  |
| External BGP (EBGP)    | 20                 |
| Internal EIGRP         | 90                 |
| OSPF                   | 110                |
| IS-IS                  | 115                |
| RIP                    | 120                |
| External EIGRP         | 170                |
| Internal BGP (IBGP)    | 200                |
| Unknown / Unusable Route | 255                |

Given identical prefix lengths, a static route will be preferred to everything except a directly connected network. The value of 255 for Unknown Routes means that they will not be used. A Static Route with a higher AD could be defined to function as a backup if a preferred route update fails. Normally Router prefers Dynamic Routes because they have a lower AD.

I've analyzed your text on dynamic routing protocols. To improve clarity and comparison, I will add tables for:

1.  **Categories of Dynamic Routing Protocols**: A table comparing IGP vs. EGP, and then sub-categorizing IGPs.
2.  **Characteristics of Routing Protocols (Distance Vector vs. Link State)**: A direct comparative table.
3.  **Route Selection Factors**: A table for Metric, ECMP, and Administrative Distance.
4.  **Specific Metrics Used by Different Protocols**: A table listing protocols and their respective metrics.


Dynamic routing protocols significantly enhance network efficiency and scalability by automating route calculation and maintenance based on real-time network topology changes, which are quickly adapted to, ensuring efficient and reliable network communication. They contrast with static routes, which are manually set and do not adapt to network changes unless manually updated.

### Categories of Dynamic Routing Protocols

Dynamic routing protocols are broadly categorized based on their scope of operation:

| Category                     | Description                                            | Sub-categories / Examples                                           |
| :--------------------------- | :----------------------------------------------------- | :------------------------------------------------------------------ |
| **Interior Gateway Protocols (IGP)** | Used within a single Autonomous System (AS).           | **Distance Vector:** RIP, EIGRP \<br\> **Link State:** OSPF, IS-IS   |
| **Exterior Gateway Protocols (EGP)** | Used for routing between different Autonomous Systems. | **Path Vector:** BGP (Border Gateway Protocol)                      |

### Characteristics of Routing Protocols

Here's a comparison of Distance Vector and Link State protocols:

| Characteristic          | Distance Vector Protocols                                | Link State Protocols                                                    |
| :---------------------- | :------------------------------------------------------- | :---------------------------------------------------------------------- |
| **Information Exchange** | Exchange information about known destination networks and metrics with directly connected neighbors. | Each router advertises information about its directly connected links to all other routers in the network area. |
| **Network View** | "Routing by rumor"; information is passed sequentially from router to router, leading to a "tree" view of the network. | Each router builds an identical, comprehensive "map" or topology database of the entire network. |
| **Calculation** | Calculates routes based on information received from neighbors. | Independently calculates the best routes using its complete network map (e.g., Dijkstra's SPF algorithm). |
| **Resource Usage** | Generally less resource-intensive in terms of CPU/memory. | Generally requires more resources due to the amount of information processed and complex calculations. |
| **Convergence Speed** | Slower convergence due to "counting to infinity" issues and full table exchanges. | Faster convergence due to quick propagation of link state changes and independent recalculations. |
| **Examples** | RIP, EIGRP                                               | OSPF, IS-IS                                                             |

### Route Selection in Dynamic Routing

Routers use several criteria to select the best path when multiple routes to a destination exist:

| Selection Factor                | Description                                                                                                                                                                                                                                                                                                                      |
| :------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Metric Value Determination** | Routers use a metric value to determine the best route to a destination. The metric could be hop count, bandwidth, delay, or a combination of factors, depending on the routing protocol. Generally, a lower metric value indicates a better route.                                                                                        |
| **Equal Cost Multi-path (ECMP)**| If a router learns multiple routes to the same destination with the same metric via the same routing protocol, it can use ECMP to load balance traffic across all these routes. ECMP allows for load balancing across equally good paths, improving bandwidth utilization and redundancy.                                             |
| **Administrative Distance (AD)**| This is a value used to rank the trustworthiness of the information received from different routing protocols. A lower administrative distance is preferred because it indicates a more reliable source. In cases where routes are learned from different protocols, the route with the lower administrative distance will be chosen. |

### Specific Metrics Used by Different Protocols

Different dynamic routing protocols use distinct metrics to calculate the best path:

| Routing Protocol | Primary Metric(s)                                   | Notes                                                    |
| :--------------- | :-------------------------------------------------- | :------------------------------------------------------- |
| **RIP** | Hop Count                                           | Each router counts as one hop. Limited to 15 hops.       |
| **EIGRP** | Bandwidth, Delay (and optionally Reliability, Load) | Uses a composite metric; often considered a hybrid protocol. |
| **OSPF** | Cost (typically based on Bandwidth)                 | Cost is inversely proportional to bandwidth. Does not inherently consider latency. |
| **IS-IS** | Cost (typically based on Bandwidth)                 | Similar to OSPF in metric calculation.                   |
| **BGP** | Path Attributes (diverse set of parameters)         | BGP's path selection is complex, using many attributes beyond a simple metric. |


### 1. Routing Information Protocol (RIP)

#### Routing Information Protocol (RIP)

RIP considers only a single piece of info about the Network Topology: the optimal path to a given Destination Network (lowest Hop Count). RIP sends Regular updates / triggered updates when changes occur of its own Routing database to neighboring routers. These neighbors receive the update and add unknown routes to its own Routing table, increasing the hop count by 1, and identifies the Originator of the update as the next hop to the specified network.

To prevent loops, the max hop count allowed is 15. This limits the size of a RIP network, since networks that have a hop count of 16 or higher are Unreachable for RIP.

* **RIPv1:** "Classful" protocol; Inefficient broadcasts to communicate updates over UDP port 520.
* **RIPv2:** "Classless" protocol; Efficient multicasts to communicate updates over UDP port 520.
* **RIPng (next Generation):** Designed for IPv6, using UDP port 521.

RIP's simplicity makes it suited to small networks with few failover routes. Distance Vector Algorithms provide slower Convergence performance than link state algorithms due to the periodic need to propagate entire Routing tables to their neighbors. RIP is a non-native IP protocol, therefore encapsulated in the higher Transport layer datagrams (UDP 520/521).

RIP is used for small size networks with less than 15 subnets.

#### Overview
Type: Distance Vector protocol.
Metric: Hop count.
Maximum Hop Count: 15 (prevents routing loops).
Timers:
  Update Timer: 30 seconds (advertises routing table).
  Invalid Timer: 180 seconds (marks a route invalid if no updates).
  Hold Down Timer: 180 seconds (prevents regular update instability).
  Flush Timer: 240 seconds (removes an invalid route).

#### Versions:
RIPv1: Only supports classful routing, does not send subnet mask information.
RIPv2: Supports classless routing, sends subnet mask information, uses multicast address `224.0.0.9` for updates.
RIPnG: RIP Next Generation for IPv6.

### 2. Enhanced Interior Gateway Routing Protocol (EIGRP)

#### Overview
EIGRP is an advanced distance vector routing protocol, often described as a hybrid protocol. It incorporates features of both distance vector and link-state protocols, enabling rapid convergence and efficient network communication. EIGRP is classed as an advanced distance vector or hybrid Routing protocol. It shares some basic principles with RIP; however, advanced changes include:

1.  Uses a **metric** composed of administrator-weighted elements such as Bandwidth and Delay instead of only a simple hop count metric. (The lowest bandwidth link along a path; the sum of latency along the path).
2.  Updates are sent in full when contact is first established between neighbors, and thereafter only send updates when there is a topology change (partial updates).
3.  Maintains a **Topology table** alongside its routing information base, used to prevent loops whilst supporting max hops greater than RIP (nominally up to 255).
4.  Updates are transmitted via multicast addressing.
5.  EIGRP is a native IP protocol, meaning it is encapsulated directly in IP datagrams (IP Protocol #88 in protocol field).

Type: Advanced Distance Vector (sometimes referred to as a hybrid protocol).
Metric: Composite metric based on bandwidth, delay, reliability, load, and MTU.
Features: Supports unequal-cost load balancing using variance, rapid convergence.

#### Key Concepts:
Feasible Distance (FD): Best known metric to reach a destination.
Reported Distance/Advertised Distance (RD): Metric reported by a neighboring router to reach a destination.
Successor: Route with the lowest FD to a destination.
Feasible Successor: Backup route with a RD less than the FD of the successor.
Hybrid Routing Protocol: Combines the best of distance vector and link-state protocols.
Metric Calculation: Uses a composite metric based on bandwidth, delay, reliability, load, and MTU size.
Load Balancing: Capable of unequal-cost load balancing using VARIANCE.
Convergence: Faster than RIP due to its efficient algorithm and trigger updates.

#### Metric Calculation
EIGRP uses a complex formula to calculate its metric, considering multiple factors:
${Metric} = 256 * [ ( K_1 * {Bandwidth} +(K_2 * {Bandwidth}) / {256 - {Load}} + K_3 * {Delay}] * ({K_5}{{Reliability} + K_4}) ]$

Where $K_1$ to $K_5$ are constants that can be adjusted to prioritize certain metrics over others, but by default,
Cisco routers use $K_1 = K_3 = 1$ and $K_2 = K_4 = K_5 = 0$, focusing mainly on bandwidth and delay.

#### EIGRP Configuration Commands
To configure EIGRP on a router, you use the following commands within global configuration mode:
- `network [NETWORK_ADDRESS] [WILDCARD_MASK]`: Specifies the interfaces on which EIGRP is enabled. The wildcard mask is the inverse of a subnet mask.
- `eigrp router-id [ROUTER_ID]`: Manually sets a unique identifier for the EIGRP routing process.
- `no auto-summary`: Disables automatic summarization of subnet routes into their major networks.
- `maximum-paths [NUMBER_OF_PATHS]`: Allows load balancing across multiple paths if available.
- `variance [MULTIPLIER]`: Enables unequal cost load balancing. Routes with a metric less than the product of the variance multiplied by the lowest metric (feasible distance) will be included in the routing table.

#### Example Configuration
Router(config)# router eigrp 100
Router(config-router)# network 10.0.0.0 0.0.0.255
Router(config-router)# eigrp router-id 1.1.1.1
Router(config-router)# no auto-summary
Router(config-router)# maximum-paths 4
Router(config-router)# variance 2

This setup configures EIGRP for autonomous system 100, enables it on all interfaces with IP addresses in the 10.0.0.0/24 range,
sets the router ID to 1.1.1.1, disables auto-summarization, allows up to 4 equal or unequal paths for load balancing, and sets the variance multiplier to 2.

EIGRP's sophisticated metric calculation and flexibility make it a robust choice for large enterprise networks seeking efficient, reliable routing with quick convergence times. Its ability to balance load across multiple paths, even those of unequal cost, provides enhanced network utilization and redundancy.

A wildcard mask uses opposite bits of a subnet mask. For example, a subnet mask of `255.255.255.0` is `11111111.11111111.11111111.00000000` in binary. The corresponding wildcard mask would be `0.0.0.255`, which is `00000000.00000000.00000000.11111111` in binary.
Shortcut for Wildcard Masks
To quickly convert a regular subnet mask to a wildcard mask, subtract each octet in the subnet mask from 255. Example:
* Subnet Mask: `255.255.255.0`
* Wildcard Mask: `255 - 255.255 - 255.255 - 255.255 - 0` = `0.0.0.255`

### 3. OSPF Link State Routing Protocols (Based on the shortest path first algorithm by Dijkstra, Edsger)

### Open Shortest Path First (OSPF)

OSPF is the most widely adopted link-state protocol, suited to large organizations with multiple redundant paths between networks. It has a higher Convergence performance than RIP and supports Classless Addressing.
While RIP & EIGRP are generally flat, OSPF is **Hierarchical**, grouping connected hosts & Routers within an Autonomous System into Areas. Routers within a given area share the same Topological database of the network they serve. Routers that can connect to multiple areas are known as **Area Border Routers**. A **Backbone Area (Area 0)** is created by the collection of border routers.
The Router applies a shortest path first algorithm to analyze the link-state database and build best-cost, loop-free routes into its Routing table.
The use of areas to subdivide the network minimizes the amount of Routing traffic that must be passed around the network as a whole, further improving convergence performance, but requires more CPU and memory resources. Tagged as #89 in the IP datagram protocol header field. Supports clear text authentication.

Routers create a connectivity map of the network. Each router advertises information about its interfaces to its neighbors. These advertisements are passed along to other routers until all routers in the network develop the same map. Using this map, each router independently calculates the best routes to each destination. This allows OSPF to converge more quickly and react faster to topology changes than Distance Vector protocols. However, OSPF tends to be resource-intensive on the CPU. Routers store information about the network in Link State Advertisements (LSAs), which are organized in a structure called the Link State Database (LSDB). The LSDB is identical for all routers in the OSPF area. Routers will flood LSAs until all routers in the OSPF area develop the same map of the network.

- OSPF Hierarchy:
  - OSPF is hierarchical, grouping connected hosts and routers within an Autonomous System into areas.
  - Routers within a given area share the same topological database of the network they serve (LSDB).
  - Routers that can connect to multiple areas are known as Area Border Routers (ABRs).

- Connectivity:
  - All routers in the same OSPF area are connected.
  - Each router calculates the best routes by following a 3-step process:
    1. Become neighbors with other routers connected to the same area.
    2. Exchange link state advertisements with neighbor routers.
    3. Calculate the best routes to each destination and insert them into the routing table.

- Areas and Performance:
  - OSPF uses areas to subdivide the network, minimizing the amount of routing traffic that must be passed around the network as a whole, thereby improving convergence performance.
  - Small networks can be single-area without any negative effects on performance.
  - In larger networks, a single-area design can negatively impact performance because:
    - The SPF algorithm takes more time to calculate routes.
    - The SPF algorithm requires exponentially more processing power on the routers' CPUs.
    - The larger LSDB takes up more memory on the routers' RAM.
  - Small changes in the network cause every router to flood LSAs and run the SPF algorithm again.

- Area Rules:
  - An area is a set of routers and links that share the same topological link-state database (LSDB).
  - The Backbone Area (Area 0) is an area that all other areas must connect to.
  - All OSPF areas should be contiguous and must have at least one ABR connected to the Backbone Area (Area 0).
  - OSPF interfaces in the same subnet must be in the same area.

- Routers:
  - Routers with all interfaces in the same area are called Internal Routers.
  - Routers with interfaces in multiple areas are called Area Border Routers (ABRs).
  - ABRs maintain a separate LSDB for each area they are connected to. It is recommended that you connect an ABR to a maximum of two areas to avoid overburdening the router.

- Routing:
  - An Intra-Area Route is a route to a destination inside/within the same OSPF area.
  - An Inter-Area Route is a route to a destination in a different OSPF area.

- Basic OSPF Configuration:
  - Unlike AS number in EIGRP, OSPF PID is locally significant.
  - Routers with a default process ID can become OSPF neighbors.
  - A router can run multiple OSPF processes at once; the `router ospf <PID>` command is used on the router to identify each of them.
  - The OSPF network command tells OSPF to look for interfaces with an IP address contained in the range specified in the command and activates OSPF on the interface in the specified area. In OSPF this command will advertise a Router’s Gateway of last resort(Default Route) and that router will become an Autonomous System Boundary Router ASBR — This command configures OSPF to inject a router’s default external route into OSPF (similar to Redistribute command) in OSPF router configuration mode
  - The `passive-interface` command tells the router to stop sending OSPF Hello messages out of the interface; used on interfaces without OSPF neighbors.
  - The `default-information originate` command advertises a router's default route into the OSPF network.

#### Autonomous System Boundary Router (ASBR)
Default Information Originate Command: When you issue the `default-information originate` command, OSPF will advertise the router's Gateway of Last Resort (Default Route). This command configures OSPF to inject a router’s default external route into the OSPF domain. This is similar to redistributing routes in OSPF router configuration mode.

#### Redistribution
Redistributes Routes from Other Routing Protocols into OSPF: 
ASBR redistributes routes from other routing protocols into the OSPF domain.


### OSPF Initialization & Neighbor States Notes
This structured note provides clear instructions on various OSPF configurations including initialization, neighbor relationships, and detailed interface settings.

#### OSPF Hello Messages
- With OSPF enabled on an interface, the router starts sending OSPF hello messages out of the interface at regular intervals (default is 10 seconds for Ethernet connections). These messages are multicast to 224.0.0.5, the multicast address for all OSPF routers. OSPF messages are encapsulated in an IP header with a protocol field value of 89.
### OSPF States and Processes:
    •   DBD: Database Description
    •   LSR: Link State Request
    •   LSU: Link State Update
    •   DR: Designated Router
    •   BDR: Backup Designated Router


### Additional Points
OSPF Interface Priority: Higher priority wins DR/BDR election. Default priority is 1 for all interfaces
.
Router ID: In case of a tie in priority, the higher Router ID wins.
Election Non-preemptive: Once elected, roles are maintained unless the interface fails or OSPF is restarted.


### OSPF Neighbor Requirements
| Requirement                    | Description                                                                                                                                           |
| :----------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------- |
| Area number                    | Must match.                                                                                                                                           |
| Subnet                         | Interfaces must be within the same subnet.                                                                                                            |
| OSPF Process                   | Must be running (not shutdown).                                                                                                                       |
| Router IDs                     | Must be unique.                                                                                                                                       |
| Hello and Dead timers          | Must match.                                                                                                                                           |
| Authentication settings        | Must match.                                                                                                                                           |
| MTU settings                   | Must match.                                                                                                                                           |
| OSPF network type              | Must be consistent across interfaces.                                                                                                                 |
NB EVEN THOUGH MTU AND NETWORK TYPE MISMATCH MAY STILL RESULT TO PARTIAL ADJACENCY(stuck in 2-way State), a mismatch of MTU and NETWORK TYPE ensures that routers won’t fully synchronize their LSDBs and have full OSPF adjacency

Dead and hello timers are critical for detecting failed neighbors. To edit the dead interval and hello interval for an OSPF-enabled interface on a Cisco device, use the following commands in interface configuration mode:

```
Router(config)# interface [interface_id]
Router(config-if)# ip ospf hello-interval [seconds]
Router(config-if)# ip ospf dead-interval [seconds]
```

Note:The dead interval must be at least 4 times the hello interval (best practice).
Both routers on the link must have matching hello and dead timers to form or maintain an adjacency.

Link-State Advertisements (LSAs):
  - LSAs are shared among routers to ensure each has an up-to-date and accurate map of the network topology.

### Loopback Interface
Definition: A virtual interface internal to Cisco IOS, created via the command `interface loopback number`, where the number is an integer.
Purpose: Provides a consistent IP address to identify or reach the router, as it remains in an up/up state as long as the router is operational and not manually shut down.
State: Always "up/up" unless manually shut down.

```
Router(config)# interface loopback 0
Router(config-if)# ip address 1.1.1.1 255.255.255.255
```
This sequence of commands sets up a loopback interface with a specified IP address, ensuring that it is active and saved across reboots. Often configured for testing or management purposes.

### OSPF Network Types
| Network Type      | Default On                                      | Neighbor Discovery                                              | DR/BDR Election | Adjacency                                                      | Multicast Addresses                                     |
| :---------------- | :---------------------------------------------- | :-------------------------------------------------------------- | :-------------- | :------------------------------------------------------------- | :------------------------------------------------------ |
| **1. Broadcast** | Ethernet & Fiber Distributed Data Interfaces    | Uses multicast address `224.0.0.5` for OSPF Hello messages.     | Mandatory       | Full adjacency with DR and BDR. DROthers have a 2-way state.   | General Hello: `224.0.0.5` <br> To DR/BDR: `224.0.0.6` |
| **2. Point-to-Point** | Serial interfaces (PPP or HDLC encapsulations) | Directly between the two routers without DR/BDR elections.      | No              | Full adjacency automatically formed between the two connected routers. | General Hello: `224.0.0.5` <br> To DR/BDR: NO DR/BDR Messages |
| **3. Non-Broadcast (NBMA)** | Frame Relay                                     | Manual neighbor specification required due to lack of broadcast. | N/A             | N/A                                                            | N/A                                                     |

DCE/DTE Roles (for Serial Interfaces):
* **DCE (Data Communication Equipment):** Sets the clock rate.
* **DTE (Data Terminal Equipment):** Specifies the clock rate (speed) of the connection.

### Commands and Configurations
| Command                                                       | Description                                                                                                                                                 |
| :------------------------------------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RT(config-if)# ip ospf priority <value>`                     | Changes OSPF Priority: Higher priority wins DR/BDR election. Default priority is 1 for all interfaces.                                                    |
| `RT(config)# clear ip ospf process`                           | Clears the OSPF process, often used to force re-elections or database synchronization.                                                                    |
| `RT# show controllers <interface-id>`                         | Shows interface controllers, providing details about the physical layer and serial interface types (DCE/DTE).                                             |
| `RT(config-if)# ip ospf network {broadcast|non-broadcast|point-to-multipoint|point-to-point}` | Sets the OSPF Network Type for the interface.                                                                                                             |
| `RT(config-if)# clock rate <value>`                          | Sets Clock Rate for Serial Interface (DCE side).                                                                                                            |
| `RT# router RIP`                                              | Enters RIP router configuration mode.                                                                                                                       |
| `RT# version 2`                                               | Configures RIP version 2 (classless).                                                                                                                       |
| `RT# router eigrp Autonomous-system-id`                     | Enters EIGRP router configuration mode (AS number must match between routers).                                                                            |
| `RT# router ospf process-id`                                | Enters OSPF router configuration mode (Process ID does not have to match between routers to form adjacency). A router can run multiple OSPF processes. |
| `RT(config-router)# variance [multiplier]`                  | Allows EIGRP to use multiple paths that have a metric less than the best path multiplied by the variance value (unequal cost load balancing).             |
| `RT(config-router)# no auto-summary`                         | Prevents the router from summarizing routes to their classful boundaries (keeping addresses classless with CIDR/wildcard mask).                         |
| `RT(config-router)# passive-interface [Interface-ID]`        | Stops sending OSPF Hello messages (and EIGRP updates) out of a specified interface; used on interfaces without OSPF/EIGRP neighbors for security/efficiency. |
| `RT(config-router)# passive-interface default`               | Sets all interfaces to be Passive by default.                                                                                                               |
| `RT(config-router)# no passive-interface intf-ID`            | Un-selects specified interfaces from being passive.                                                                                                         |
| `RT(config-router)# Default-Information Originate`           | In OSPF, advertises a router’s Gateway of last resort (Default Route) into the OSPF domain, making the router an ASBR.                                   |
| `RT(config-router)# network [network-address] [wildcard-mask]` | For RIP/EIGRP/OSPF, specifies which networks on the router’s interfaces will participate.                                                                 |
| `RT(config-router)# network [network-address] [wildcard-mask] area No.` | For OSPF, activates OSPF on interfaces matching the network address/wildcard mask and assigns them to the specified area.                                 |
| `RT(config-if)# ip ospf [process-id] area [area-id]`         | Alternatively, activates OSPF directly on an interface.                                                                                                     |

#### OSPF Cost Metric

OSPF's metric, called cost, is automatically calculated based on the bandwidth (speed) of the interface. All interfaces are equal and have a cost of 1 if calculated by dividing a reference bandwidth by the interface's real bandwidth.

* **Default Reference Bandwidth:** The default reference bandwidth is 100 Mbps. For faster Ethernet (e.g., Gigabit Ethernet), you should change the reference bandwidth to better reflect the higher speeds, such as 10,000 Mbps.
    ```
    (config-router)# auto-cost reference-bandwidth [bandwidth in Mbps]
    ```
    A reference bandwidth greater than the fastest link's bandwidth should be configured on all OSPF routers in the network to allow for future upgrades. Note that changing the interface bandwidth setting does not change the actual operating speed of the interface; it's used to calculate OSPF cost.

Three Ways to Configure New Parameters for OSPF’s Metric Calculations:
| Method                          | Command                                    | Description                                                                                                                                                              | Recommendation        |
| :------------------------------ | :----------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------- |
| **Change Interface Bandwidth** | `RT(config-if)# bandwidth [bandwidth in kbps]` | Manually changes the interface speed (bandwidth) used in the OSPF cost calculation. This is NOT recommended as it affects other protocols' metric calculations.              | Not Recommended       |
| **Set OSPF Cost Manually per Interface** | `RT(config-if)# ip ospf cost [cost-value]`  | Manually configures the OSPF cost for an individual interface. This value overrides the calculated cost.                                                                 | Used for fine-tuning  |
| **Change Reference Bandwidth** | `RT(config-router)# auto-cost reference-bandwidth [bandwidth in mbps]` | Changes the reference bandwidth used in the OSPF cost calculation (Reference Bandwidth / Interface Bandwidth). This is the most recommended method for scaling OSPF costs. | Most Recommended      |

### Show Commands Overview

| Command                               | Description                                                                                                                                                                                               |
| :------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RT# show ip protocols`               | Displays detailed information about all IP routing protocols configured on the router, including types (OSPF, EIGRP), status, network types, timers, and specific configurations.                        |
| `RT# show ip {eigrp|ospf} interface`  | Displays detailed information about interfaces configured for EIGRP or OSPF, showing data like network type, cost, priority, state, and protocol-specific statistics.                                   |
| `RT# show ip {eigrp|ospf} interface brief` | Provides a summarized view of all interfaces running EIGRP or OSPF, listing interface names, IP addresses, and status indicators (e.g., passive/active).                                            |
| `RT# show ip {eigrp|ospf} interface intf-ID` | Displays detailed information about a specific interface participating in EIGRP or OSPF, including hello/dead intervals, wait times, and other protocol-specific metrics.                           |
| `RT# show ip {eigrp|ospf} neighbor`   | Lists all neighboring devices discovered by EIGRP or OSPF on all interfaces, showing neighbor ID, IP address, connecting interface, hold time, and adjacency status.                                  |
| `RT# show ip {eigrp|ospf} topology`   | For EIGRP, displays entries in the EIGRP topology table (successor/feasible successors). For OSPF, shows the OSPF link-state database (LSDB) for the area, detailing all learned and calculated routes. |

### Best Practices for Routing

| Do's                                         | Don'ts                                                               |
| :------------------------------------------- | :------------------------------------------------------------------- |
| Use Correct Subnet Masks.                    | Avoid Incorrect Next-Hop Addresses.                                  |
| Specify Exact Routes for Non-Broadcast Interfaces. | Don't Overlook Routing Protocols for Larger Networks.                |
| Verify Interface Statuses.                   | Avoid Unnecessary Routes.                                            |
| Use Descriptive Comments.                    | Don't Forget Security.                                               |
| Test Connectivity & Specify exact Default Gateway. | Avoid Misconfigurations.                                             |

#### Configuration Example for Floating Static Route
If OSPF (AD 110) is the primary routing protocol, and you need a backup static route:
```
Router(config)# ip route 192.168.1.0 255.255.255.0 10.1.1.2 200
```
This command configures a static route to the network 192.168.1.0/24 with a next-hop address of 10.1.1.2 and sets the AD to 200, ensuring it is used only if the OSPF route fails.

Route Preference Based on Address Length
* When a router has multiple routes to similar networks, it prefers the route with the longest prefix length (most specific match) over routes with shorter prefix lengths.
* In dynamic routing, routers automatically select the optimal path to each destination based on predefined metrics and administrative distances.

### 4. Border Gateway Protocol (BGP)

BGP replaced Exterior Gateway Protocol (EGP). BGP is designed to be used within and between Routing Domains in a mesh network and as such is used as the Routing protocol on the Internet, primarily between ISPs.

| BGP Term        | Description                                                                 |
| :-------------- | :-------------------------------------------------------------------------- |
| **MESH Network** | A network of Routers in separate Autonomous Systems.                        |
| **Interior BGP (IBGP)** | Implemented within an Autonomous System.                                    |
| **Exterior BGP (EBGP)** | Implemented between Autonomous Systems.                                     |

AS is designed to hide the complexity of private Organization networks from the public Internet.

If all Internet locations had to be propagated to all Network Routers, the Routing tables would become too large to process. BGP prioritizes stability, so it is slow to converge. BGP is a non-native IP protocol; it works over TCP on port 179. It uses a classless network prefix called **Network Layer Reachability Information (NLRI)**, a path routing vector. Path selection is based on multiple metrics: Hop count, Weight, Local Preference, Origin, AS Path, etc. (More complex than simple distance or bandwidth).

---

## Exploring Network Redundancy: From Layer 2's EtherChannel to Layer 3's FHRP

In the world of networking, ensuring continuous data flow and minimizing downtime is paramount. A fascinating aspect of network design involves the implementation of redundancy protocols across different layers. Let's delve into the similarities between EtherChannel at Layer 2 and First Hop Redundancy Protocols (FHRP) at Layer 3.

### Similarities:

| Feature           | EtherChannel (Layer 2)                                                               | FHRP (Layer 3)                                                                 |
| :---------------- | :----------------------------------------------------------------------------------- | :----------------------------------------------------------------------------- |
| **Redundancy** | Aggregates multiple physical links into a single logical link for enhanced bandwidth and redundancy. | Provides redundant gateway IPs to connected devices, preventing single points of failure (e.g., HSRP, VRRP, GLBP). |
| **Load Balancing**| Distributes traffic at Layer 2 among the links in the channel (e.g., source/dest MAC). | Distributes client requests among multiple routers, efficiently managing traffic at Layer 3. |
| **Failover Capability** | If one physical link fails, traffic automatically redistributes to remaining links without downtime. | Re-routes traffic to another router in the event of a gateway failure, ensuring high availability. |

While they operate at different layers within the OSI model, the core objectives align splendidly, showcasing the layered approach to network resilience.
Understanding these protocols is essential for designing robust networks that can efficiently handle failures and ensure uninterrupted service delivery.

A First Hop Redundancy Protocol (FHRP) is a **subnetwork** designed to protect the default gateway used on a network by allowing 2 or more routers to provide backup for that address.
In the event of a **failed** router, the backup router will take over the address, usually within a few seconds.
Due to the degree of complexity in Endpoint-Hosts Routing Algorithms, configuring multiple default gateways for fault tolerance is impractical - FHRP resolves this issue by allowing multiple physical router appliances to function as a single logical router. Named as "First Hop" due to being an Endpoint-Host(s) Default Gateway or first router (HOP) in the path to whatever destination the hosts are trying to send traffic to.

- A Virtual Router IP is configured on 2 or more routers, The Virtual IP is generated in accordance with specific rules with a Virtual MAC Address.(each FHRP uses a different format for the virtual MAC) 

An Active Router and a Standby Router are elected, Endpoints/Hosts in the network are configured to use the virtual IP as their default gateway.
The Active router replies to ARP requests using the virtual MAC Address, so traffic destined for other networks will be sent to it.
If the active router fails, the standby router becomes the next active router. However, with Non-Preemption enabled, the new Active Router will send Gratuitous ARP messages so that switches will update their MAC Address Tables. It now functions as the new default gateway. If the old active router comes back online/recovers from failure, by default it would not take back its role as the Active router. It becomes the standby router. Router selection is non-preemptive by default, similar to DR/BDR election in OSPF, although in FHRP, there's a way to configure "PREEMPTION."

### 📝 Here are some detailed notes on how FHRP operates at Layer 3:
FHRP plays a critical role in maintaining the accessibility of network services by providing seamless failover capabilities. 

### HOT STANDBY ROUTER PROTOCOL HSRP
| Feature          | Description                                                              | HSRPv1 Specifics                      | HSRPv2 Specifics                       |
| :--------------- | :----------------------------------------------------------------------- | :------------------------------------ | :------------------------------------- |
| **Developer** | Cisco proprietary                                                        | N/A                                   | N/A                                    |
| **Election** | An Active & Standby Router are elected.                                  | N/A                                   | N/A                                    |
| **Supported Versions** | V1 and V2 supported.                                                     | N/A                                   | Adds IPv6 support.                     |
| **Multicast IPv4 Address** | `224.0.0.2` (V1) / `224.0.0.102` (V2)                                    | `224.0.0.2`                           | `224.0.0.102`                          |
| **Virtual MAC Address** | `0000.0C07.ACxx` (V1) / `0000.0C9F.Fxxx` (V2)                           | `0000.0C07.ACxx`                      | `0000.0C9F.Fxxx`                       |
| **Group Number** | `xx`/`xxx` represents HSRP Group Number. Can be configured differently for each subnet/VLAN. | N/A                                   | N/A                                    |
| **Best Practice**| Group number settings should match VLAN numbers for organizational consistency. | N/A                                   | N/A                                    |

### VIRTUAL ROUTER REDUNDANCY PROTOCOL VRRP
| Feature          | Description                                                              |
| :--------------- | :----------------------------------------------------------------------- |
| **Standard** | Open Standard - IEEE (`IEEE 802.1Q` - actually `IEEE 802.1Q` for VLANs, VRRP is `RFC 3768`)                                                             |
| **Enhancements** | Cisco proprietary enhancements available.                                |
| **Election** | A Master and Backup Router are elected. Load balances among multiple routers elected. |
| **Multicast IPv4 Address** | `224.0.0.18`                                                             |
| **Virtual MAC Address** | `0000.5000.01XX` (XX represents the VRRP Group ID)                       |
| **Load Balancing**| Can be configured with a different master router in each subnet/VLAN to load balance. |

#### GATEWAY LOAD BALANCING PROTOCOL GLBP
| Feature          | Description                                                              |
| :--------------- | :----------------------------------------------------------------------- |
| **Capability** | Provides redundancy AND load balances traffic between multiple available routers. |
| **Load Balancing**| Load Balances among Multiple Routers within a single subnet.             |
| **Election (AVG)**| An Active Virtual Gateway (AVG) is elected.                              |
| **AVF Assignment**| Up to 4 Active Virtual Forwarders (AVF) are assigned by the AVG.         |
| **Multicast IPv4 Address** | `224.0.0.102` (same as V2 HSRP)                                          |
| **Default Gateway**| Each AVF acts as the default gateway.                                    |

### Hot Standby Router Protocol Configuration Notes
1.  **Highest Priority** (Default Priority 100)
2.  **The Active Router is determined in this order:**
    I. Highest Priority
    II. Highest IP Address (in case of a tie in priority)
    III. Manual Config with Preempt command (if preempt is enabled, a router with higher priority will take over the active role)

NOTE: The Active Router is determined by priority. Preempt causes the Router to take the role of active Router, even if another router already has the role. The Preempting Router must have a higher priority or IP Address.

Configuration commands:
```
RT# show standby  
RT(config-if)# interface gx/y
RT(config-if)# standby version 1|2  
RT(config-if)# standby group-number ip 'virtual-ip'
RT(config-if)# standby group-number priority 'priority'
RT(config-if)# standby group-number preempt
```

### VIRTUAL ROUTING AND FORWARDING (VRF)
VRF is commonly used to facilitate MPLS and VRF-Lite. VRF allows us to divide one physical router into multiple virtual routers, similar to VLANs for switches.

| Feature    | VLANs (Switches)                                | VRF (Routers)                                         |
| :--------- | :---------------------------------------------- | :---------------------------------------------------- |
| **Function** | Divide a switch into multiple virtual switches with their own logical broadcast domains. | Divide a Router into multiple Virtual Routers, each with its own Routing Table. |
| **Traffic Isolation** | Broadcast domain isolation.                     | Traffic is isolated from each other; customer IP address schemes can overlap. |
| **Configurable on**| Switchports, SVIs.                              | Router Interfaces, Switch Virtual Interfaces (SVIs), and Routed ports on Multilayer Switches. |
| **Traffic Flow**| Traffic within one VLAN is isolated from others. | Traffic in one VRF cannot be forwarded out of an interface in another VRF (except with VRF Leaking). |
| **Common Use** | Enterprise LAN segmentation.                    | Service providers to carry traffic from multiple customers (e.g., on a PE Router). |

Traffic in one VRF cannot be forwarded out of an interface in another VRF. As an exception, VRF Leaking can be configured to allow traffic to pass between VRFs.
VRF is used commonly by service providers to allow one device to carry traffic from multiple customers (e.g., on a PE Router).

---


## ACCESS CONTROL LISTS

IPv4 access control lists (ACL) give network engineers the ability to program a filter into a router. Each router, on each interface, for both the inbound and outbound direction, can enable a different ACL with different rules. Each ACL’s rules tell the router which packets to discard and which to allow through. IPv4 ACLs perform many functions in Cisco routers, with the most common use as a packet filter. Engineers can enable ACLs on a router so that the ACL sits in the forwarding path of packets as they pass through the router. After it is enabled, the router considers whether each IP packet will either be discarded or allowed to continue as if the ACL did not exist. ACLs can be used for many other IOS features as well. As an example, ACLs can be used to match packets for applying Quality of Service (QoS) features. QoS allows a router to give some packets better service, and other packets worse service.

### ACL Location and Direction

Cisco routers can apply ACL logic to packets at the point at which the IP packets enter an interface, or the point at which they exit an interface. In other words, the ACL becomes associated with an interface and for a direction of packet flow (either in or out). That is, the ACL can be applied inbound to the router, before the router makes its forwarding (routing) decision, or outbound, after the router makes its forwarding decision and has determined the exit interface to use. In short, to filter a packet, you must enable an ACL on an interface that processes the packet, in the same direction the packet flows through that interface. When enabled, the router then processes every inbound or outbound IP packet using that ACL. When you think about the location and direction for an ACL, you must already be thinking about what packets you plan to filter (discard), and which ones you want to allow through. To tell the router those same ideas, you must configure the router with an IP ACL that matches packets. Matching packets refers to how to configure the ACL commands to look at each packet, listing how to identify which packets should be discarded and which should be allowed through.

When doing ACL processing, the router processes the packet, compared to the ACL, as follows:
ACLs use first-match logic. Once a packet matches one line in the ACL, the router takes the action listed in that line of the ACL and stops looking further in the ACL.

This sequence of processing an ACL as a list happens for any type of IOS ACL: IP, other protocols, standard or extended, named or numbered. Finally, if a packet does not match any of the items in the ACL, the packet is discarded. The reason is that every IP ACL has a deny all statement implied at the end of the ACL. It does not exist in the configuration, but if a router keeps searching the list, and no match is made by the end of the list, IOS considers the packet to have matched an entry that has a deny action.

IOS refers to each line in an ACL as an Access Control Entry (ACE), but many engineers just call them ACL statements. IOS allows standard ACLs to match a range of addresses using a tool called a wildcard mask. Note that this is not a subnet mask. The wildcard mask (which this book abbreviates as WC mask) gives the engineer a way to tell IOS to ignore parts of the address when making comparisons, essentially treating those parts as wildcards, as if they already matched. You can think about WC masks in decimal and in binary, and both have their uses. To begin, think about WC masks in decimal, using these rules:
* Decimal 0: The router must compare this octet as normal.
* Decimal 255: The router ignores this octet, considering it to already match. The WC mask actually directs the router’s logic bit by bit. In short, a WC mask bit of 0 means the comparison should be done as normal, but a binary 1 means that the bit is a wildcard and can be ignored when comparing the numbers. First, to match any and all packets with an ACL command, just use the any keyword for the address. For example, to permit all packets: `access-list 1 permit any`

So, when and where should you use such a command? Remember, all Cisco IP ACLs end with an implicit deny any concept at the end of each ACL. That is, if a router compares a packet to the ACL, and the packet matches none of the configured statements, the router discards the packet. Want to override that default behavior? Configure a `permit any` at the end of the ACL. You might also want to explicitly configure a command to deny all traffic (for example, `access-list 1 deny any`) at the end of an ACL. Why, when the same logic already sits at the end of the ACL anyway? Well, the ACL show commands list counters for the number of packets matched by each command in the ACL, but there is no counter for that implicit deny any concept at the end of the ACL. So, if you want to see counters for how many packets are matched by the deny any logic at the end of the ACL, configure an explicit deny any. When routers apply an ACL to filter packets in the outbound direction, as shown in Example 2-3, the router checks packets that it routes against the ACL. However, a router does not filter packets that the router itself creates with an outbound ACL.
Examples of those packets include routing protocol messages and packets sent by the ping and traceroute commands on that router. In addition, if you add the `log` keyword to the end of an access-list command, IOS then issues log messages with occasional statistics about matches of that particular line of the ACL. Both the statistics and the log messages can be helpful in deciding which line in the ACL is being matched by a packet. When you troubleshoot an ACL for the first time, before getting into the details of the matching logic, take the time to think about both the interface on which the ACL is enabled and the direction of packet flow. Sometimes the matching logic is perfect—but the ACL has been enabled on the wrong interface, or for the wrong direction, to match the packets as configured for the ACL.

To match a specific address, just list the address. To match any and all addresses, use the ANY keyword. To match based only on the first one, two, or three octets of an address, use the 0.255.255.255, 0.0.255.255, and 0.0.0.255 WC masks, respectively. Also, make the source (address) parameter have 0s in the wildcard octets (those octets with 255 in the wildcard mask). To match a subnet, use the subnet ID as the source, and find the WC mask by subtracting the DDN subnet mask from 255.255.255.255.

The change IOS can make with an access-list command is to convert to 0 any octet of an address for which the wildcard mask’s octet is 255. For example, with a wildcard mask of 0.0.255.255, IOS ignores the last two octets. IOS expects the address field to end with two 0s. If not, IOS still accepts the access-list command, but IOS changes the last two octets of the address to 0s. Extended ACLs differ from standard ACLs mostly because of the larger variety of packet header fields that can be used to match a packet. One extended ACE (ACL statement) can examine multiple parts of the packet headers, requiring that all the parameters be matched correctly to match that one ACE. That powerful matching logic makes extended access lists both more useful and more complex than standard IP ACLs.

Numbered ACLs have existed in IOS since the early days of Cisco routers and IOS; however, for many years, through many IOS versions, the ability to edit a numbered IP ACL was poor. For example, to simply delete a line from the ACL, the user had to delete the entire ACL and then reconfigure it. The ACL editing feature uses an ACL sequence number that is added to each ACL permit or deny statement, with the numbers representing the sequence of statements in the ACL. ACL sequence numbers provide the following features for both numbered and named ACLs:
* New configuration style for numbered: Numbered ACLs use a configuration style like named ACLs, as well as the traditional style, for the same ACL; the new style is required to perform advanced ACL editing.
* Deleting single lines: An individual ACL permit or deny statement can be deleted with a `no sequence-number` subcommand.
* Inserting new lines: Newly added permit and deny commands can be configured with a sequence number before the deny or permit command, dictating the location of the statement within the ACL.
* Automatic sequence numbering: IOS adds sequence numbers to commands as you configure them, even if you do not include the sequence numbers.

ACLs have multiple uses, they function as a packet filter, instructing the router to permit or discard specific traffic, ACLs can filter traffic based on source/destination Layer 3 IP addresses, source /destination layer 4 ports. Different types of ACLs have a different range of numbers that can be used.

Configuring an ACL in Global Config Mode will not make the ACL take effect. The ACL must then be applied to an interface, ACLs are applied either inbound or outbound. ACLs are made up of one or more ACCESS CONTROL ENTRIES ACE. When the router checks a packet against the ACL, it processes the ACEs in order, from top to bottom. If the packet matches one of the ACEs in the ACL, the router takes the action and stops processing the ACL. All entries below the matching entry will be ignored. ACLs have multiple uses, and are processed sequentially from the first entry in the list to the last entry. They control packet flow across a network by either permitting or denying packets based on source network, destination network, (protocol or destination port-Extended). Each ACL can only be applied to a single protocol per interface and per direction, Multiples ACLs can be used to accomplish more complex packet flow through out an organization.

A very common point of confusion with Cisco ACLs! It seems counterintuitive, but the "in" and "out" directions in an ACL are always relative to the router interface itself, not the direction of the traffic flow in the network as a whole.

| Direction | Perspective                                    | Processing Point                                                | Action on Deny        | Action on Permit                  |
| :-------- | :--------------------------------------------- | :-------------------------------------------------------------- | :-------------------- | :-------------------------------- |
| **Inbound** | Traffic coming *into* the router interface.    | Router checks ACL *before* making any routing decisions.        | Router drops the packet. | Router proceeds with routing.     |
| **Outbound**| Traffic going *out of* the router interface.   | Router checks ACL *after* making routing decisions and determining the exit interface. | Router drops the packet. | Router sends the packet out.      |

NOTE: If you apply a new ACL named or numbered to the same interface in the same direction, it will replace/overwrite the previous one, in such case the last ACL we applied will be the running one.
NOTE: If you added ACEs to an existing ACL, the ACEs will be appended to the end of the existing ACL; consequently, it may be necessary to re-create the ACL if you need the add an entry that should appear at or near the top of the ACL. 

### Standard ACLs

STANDARD ACLs match traffic based only on the source IP address of the packet. Standard ACLs can use numbers 1-99 and 1300-1999. A rule of thumb is to apply standard ACLs as close to the destination as possible.

#### Standard Numbered ACLs:
They are identified with a number (i.e., ACL 1, ACL 2 etc). The Basic command to configure a “standard numbered” ACL is:

```cli
RT(config)# ip access-list standard number
RT(config-std-nacl)# deny 1.1.1.1 0.0.0.0
RT(config-std-nacl)# deny 1.1.1.1
RT(config-std-nacl)# permit any
RT(config-std-nacl)# permit 0.0.0.0 255.255.255.255
RT(config-std-nacl)# remark ## BLOCK BOB FROM ACCOUNTING ##
RT(config-std-nacl)# interface g0/0
RT(config-if)# ip access-group number {in | out}
```

Display commands for Standard Numbered ACLs:
```cli
RT(config)# do show access-lists
RT(config)# do show running-config | include access-lists
```

#### Standard Named ACLs:
They are identified with a Name (i.e., ‘BLOCK_BOB’). They are configured by entering ‘standard named ACL configuration mode’ and then configuring each entry within that configuration mode.

```cli
RT(config)# ip access-list standard ACL_NAME
RT(config-std-nacl)# [entry-number] {deny | permit} ip wildcard-mask
RT(config)# ip access-list standard BLOCK_BOB
RT(config-std-nacl)# deny 192.168.1.24 0.0.0.0
RT(config-std-nacl)# permit any
RT(config-std-nacl)# remark ## configured April21,2025 ##
RT(config-std-nacl)# interface g0/0
RT(config-if)# ip access-group BLOCK_BOB {in | out}
```

NOTE: One disadvantage of the numbered ACL is that when configuring/deleting numbered ACLs from global config mode, you can’t delete individual entries, you can only delete the entire ACL. However, from `config-std-nacl` mode, you can use `no entry-number` to delete individual entries.
NOTE: One advantage of the named ACL is that you can easily delete individual entries in the ACL with `RT(config-std-nacl)# NO sequence-number`, and you can insert new entries in between other entries by specifying the sequence number. Named ACLs originally had three big differences compared to numbered ACLs:
* Using names instead of numbers to identify the ACL, making it easier to remember the reason for the ACL
* Using ACL subcommands, not global commands, to define the action and matching parameters
* Using ACL editing features that allow the CLI user to delete individual lines from the ACL and insert new lines

Display commands for Standard Named ACLs:
```cli
RT(config)# do show access-lists
RT(config)# do show running-config | include access-list
RT(config)# do show running-config | section access-list
```

NOTE: There is a RESEQUENCING function that helps edit ACLs.
The command is:
```cli
#ip access-list resequence number/name starting-seq-num increment
```

### Extended ACLs

Extended ACLs let you imagine the exact path of the traffic you want to filter. This will make it easier to determine the source and destination. They match traffic based on more parameters -> on the src/dest IP address && src/dest Port/Protocol of the packet, so they are more precise and also more complex than standard ACLs. Extended ACLs can use numbers 100-199 and 2000-2699.
Use named ACLs instead of numbered ones. They are easier to read and modify.
If you specify the protocol, source IP, source Port, destination IP, destination Port, etc, a packet must match all of those values to match the ACL entry. Even if it matches all except one of the parameters, the packet won’t match that entry of the ACL.

#### Extended Numbered ACLs:
```cli
RT(config)# access-list number [permit | deny] protocol src-IP dest-ip
```

#### Extended Named ACLs:
```cli
RT(config)# ip access-list extended {name | number}
RT(config-ext-nacl)# [permit | deny] protocol src-IP dest-ip
RT(config-ext-nacl)# permit ip any any
RT(config-ext-nacl)# deny ip any any
```

* **Protocol Awareness:** Extended ACLs let you specify protocols (TCP, UDP, ICMP). Know their common port numbers (e.g., TCP port 80 for HTTP, 22 for SSH). The Protocol name IP-Internet Protocol Allows or Deny Any Internet Protocol, only specify this when we don’t care about the protocol, we just want to deny or permit all packets.
* **"Any" Keyword:** Use "any" as a shortcut for "0.0.0.0 255.255.255.255" (any IP address) to simplify rules.
* **"Host" Keyword:** Use "host" before an IP address (e.g., "host 192.168.1.10") instead of "192.168.1.10 0.0.0.0" for a single host.
* **Port Operators:** Utilize operators like "eq" (equal), "neq" (not equal), "gt" (greater than), "lt" (less than), "range" to specify port ranges. The most common being “eq”.
When you specify tcp/udp as the protocol to match you can optionally specify the source and /or destination port to match, this is optionally, if you just specified TCP or UDP without the port numbers, all port numbers will be matched.
```cli
RT(config-ext-nacl)# deny tcp src-ip “eq” src-port-num dest-ip “eq” dst-port-num
RT(config-ext-nacl)# deny udp src-ip “lt” src-port-num dest-ip “gt” dst-port-num
```

### ACL Placement Guidelines

"Ever wonder where to place them on your Cisco router? 🤔 It's all about control! 💡Placement is KEY. Standard ACLs = 🚫 destination. Extended ACLs = 🎯 source. This prevents headaches and keeps your network lean. Think of ACLs like bouncers! 🚪"

| ACL Type      | Analogy                                   | Placement Rule                                                     | Rationale                                                                                                                                                                                                                                                                                                                                                                                                                                        | Common Application |
| :------------ | :---------------------------------------- | :----------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------- |
| **Standard ACLs** | Like a 'destination only' filter.         | Place them near the destination.                                   | Because standard ACLs can filter packets only by source Internet Protocol (IP) address, they should be placed as close to the destination as possible. This prevents them from blocking legitimate traffic from the same source that needs to reach other destinations. If applied close to the source, there is a risk of blocking more traffic than intended. When applying them to an interface, applying them "outbound" is often the correct approach, meaning closer to the destination interface. The goal is to filter the traffic as it's about to leave the router towards its final destination, minimizing the impact on other traffic. | Often outbound     |
| **Extended ACLs** | Super precise, checking ID and destination. | Place them near the source for maximum efficiency.                 | By contrast, you can use extended ACLs to filter packets based on Source & Destination IP, Protocols, and Ports. Extended ACLs should be placed as "close to the source" of the packet as possible, to limit how far the packets travel in the network before being denied. As a result, applying them "inbound" is often the correct approach, meaning on the interface where the traffic (we intend to permit or deny) enters the router. | Often inbound      |

In Summary:
* Standard ACLs are placed closer to the destination (often outbound) to minimize their broad impact.
* Extended ACLs are placed closer to the source (often inbound) for more efficient filtering.


# CHAPTER 12: MANAGEMENT PLANE/LAYER PROTOCOLS

## CISCO DISCOVERY PROTOCOL (CDP)

Layer 2 Discovery Protocols such as CDP and LLDP share information with and Discover information about neighbouring connected devices. Although they are layer 2 discovery protocols, they could be used to share layer 3 information as well. The shared information includes Hostname, IP address, Device type.
Because they share information about devices in the network, they can be considered a security risk and are often not used. It is up to the network engineer/admin to decide if they want to use them in the network or not.

CDP is a Cisco Proprietary protocol, it’s enabled on Cisco devices (routers, switches, firewalls, IP phones, etc.).

| Feature                | Description                                                                                                                                                                                                                                                                   |
| :--------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Multicast Address** | CDP messages are periodically sent to multicast address `0100.0CCC.CCCC` (this same multicast address is used by Cisco on all its proprietary L2 Protocols, i.e., CDP/VTP/DTP/PagP/UDLD). When a device receives a CDP message, it processes and discards the message; it does not forward it to other devices. |
| **Neighbor Discovery** | CDP shows information about directly connected neighbors, because only directly connected devices share and receive CDP messages.                                                                                                                                              |
| **Default Timer** | By default, CDP messages are sent once every 60 seconds.                                                                                                                                                                                                                      |
| **CDP Holdtime** | By default, the CDP HOLDTIME is 180 seconds. If a message isn’t received from a Neighbor for 180 seconds, the neighbor is removed from the CDP neighbor table.                                                                                                                    |
| **CDPv2** | CDPv2 messages are sent by default. Version 2 offers a few more advanced features like the ability to identify native VLAN mismatches (between neighbors).                                                                                                                     |
| **Default State** | CDP is globally enabled by default on each interface.                                                                                                                                                                                                                         |

### CDP Configuration Commands

| Command                                | Description                                                                         |
| :------------------------------------- | :---------------------------------------------------------------------------------- |
| `RT(config)# cdp run`                  | To enable CDP globally.                                                             |
| `RT(config)# no cdp run`               | To disable CDP globally.                                                            |
| `RT(config-if)# cdp enable`            | To enable CDP on specific interfaces.                                               |
| `RT(config-if)# no cdp enable`         | To disable CDP on specific interfaces.                                              |
| `RT(config-if)# cdp timer seconds`     | To configure the CDP message timer.                                                 |
| `RT(config-if)# cdp holdtime seconds`  | To configure the CDP hold time.                                                     |

### CDP Show Commands

| Command                                 | Description                                                                                                                                                                                                                 |
| :-------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RT# show cdp`                          | States whether CDP is enabled globally and lists the default update and holdtime timers.                                                                                                                                    |
| `RT(config)# do show cdp traffic`      | Displays the number of CDP advertisement packets passed through an interface, and the number of CDP advertisements the device interfaces has sent and received.                                                               |
| `RT(config)# do show cdp interface [intf-ID]` | Gives basic information about each interface; you can also specify a specific interface.                                                                                                                                    |
| `RT(config)# do show cdp neighbors`    | Displays CDP details about its neighbors, including Local Interface (interface on the device issuing the command) & Device ID/Name of the Neighbor & Port ID (interface of the connected neighbor), their capabilities, and platform. |
| `RT(config)# do show cdp neighbors detail` | Displays more information for CDP neighbors, i.e., Operating system & version of the neighboring device, VTP Management Information, and Information about VLAN Duplexity.                                                  |
| `RT(config)# do show cdp entry [neighbor-ID]` | Lists the same information as the `show cdp neighbors detail` command, but only for the named neighbor (case sensitive).                                                                                                    |

## LINK LAYER DISCOVERY PROTOCOL (LLDP)

LLDP is an industry standard IEEE protocol (`IEEE 802.1AB`). It’s usually disabled globally on all interfaces on Cisco devices by default in favor of Cisco CDP. Cisco created the Cisco-proprietary CDP before any standard existed for a similar protocol. LLDP is usually more preferable to run in a Multi-vendor network. It must be manually enabled. A device can run CDP and LLDP at the same time.

| Feature                | Description                                                                                                                                                                                                     |
| :--------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Multicast MAC Address** | LLDP messages are periodically sent to Multicast MAC address `0180.C200.000E`. When a device receives an LLDP message, it processes and discards the message; it does not forward it to other devices.                   |
| **Message Concepts** | LLDP uses the same messaging concepts as CDP, encapsulating messages directly in data-link headers.                                                                                                                |
| **Default Timer** | By default, LLDP messages are sent out every 30 seconds, with a default HOLDTIME of 120 seconds.                                                                                                                |
| **Reinitialization Delay** | LLDP has an additional timer called the ‘Reinitialization Delay’; if LLDP is enabled (globally or on an interface), this timer will delay the actual initialization of LLDP by 2 seconds (default).                    |
| **Separate Functions** | LLDP separates the sending and receiving of LLDP messages as separate functions, allowing independent control of transmission and reception on an interface.                                                       |

### LLDP Configuration Commands

| Command                                        | Description                                                                                                                                                                                                                                                             |
| :--------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RT(config-if)# lldp transmit`                 | To enable LLDP on a specific interface (tx) to advertise LLDP messages.                                                                                                                                                                                                 |
| `RT(config-if)# lldp receive`                  | To enable LLDP on a specific interface (rx) as LLDP Recipient.                                                                                                                                                                                                          |
| `RT(config)# lldp run`                         | To enable LLDP globally (Cisco devices default to disable LLDP). This global configuration command sets the default mode of LLDP operation for any interface that does not have more specific LLDP subcommands (lldp transmit, lldp receive). Enables LLDP in both directions on those interfaces. |
| `RT(config)# no lldp run`                      | To disable LLDP globally.                                                                                                                                                                                                                                               |
| `RT(config)# lldp timer seconds`               | To configure the LLDP message timer.                                                                                                                                                                                                                                    |
| `RT(config)# lldp holdtime seconds`            | To configure the LLDP holdtime timer.                                                                                                                                                                                                                                   |
| `RT(config)# lldp reinit seconds`              | To configure the LLDP Reinitialization timer.                                                                                                                                                                                                                           |

### LLDP Show Commands

| Command                                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| :-------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RT(config)# do show lldp traffic`      | Displays the number of LLDP packets passed through an interface, and the number of LLDP advertisements the device interfaces have sent and received.                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `RT(config)# do show lldp interface [intf-ID]` | Gives some basic information about each interface; you can also specify a specific interface. It also displays the TX and RX state.                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `RT(config)# do show lldp neighbors`    | Displays LLDP details about its neighbors, including Local Interface (interface on the device issuing the command) & Device ID/Name of the Neighbor & Port ID (interface of the connected neighbor), their capabilities, and platform.                                                                                                                                                                                                                                                                                                                                                                  |
| `RT(config)# do show lldp neighbors detail` | Displays more information for LLDP neighbors, i.e., Operating system & version of the neighboring device. VTP Management Information won’t be displayed (as VTP is Cisco Proprietary). Information about VLAN Duplexity.                                                                                                                                                                                                                                                                                                                                                                                  |
| `RT(config)# do show lldp entry [neighbor-ID]` | Displays information per specific neighboring device ID, similar to `#show lldp neighbors detail`, but for the specified neighbor only.                                                                                                                                                                                                                                                                                                                                                                                                                                                         |

Both the `show cdp neighbors` and `show lldp neighbors` commands have “local intf” (interface) and “port ID” columns. These columns refer to the local device’s interface and the neighboring device’s interface, respectively. However, the LLDP output in the example does differ from CDP in a few important ways:
* LLDP uses `B` as the capability code for switching, referring to bridge, a term for the device type that existed before switches that performed the same basic functions.
* LLDP does not identify IGMP as a capability, while CDP does (I).
* CDP lists the neighbor’s platform, a code that defines the device type, while LLDP does not.
* LLDP lists capabilities with different conventions:
    * **System Capabilities:** What the device can do
    * **Enabled Capabilities:** What the device does now with its current configuration

---

## SIMPLE NETWORK MANAGEMENT PROTOCOL (SNMP)

SNMP Agent (UDP 161) and SNMP Manager (UDP 162)
In 1988, RFC 1065, “Structure and Identification of Management Information for TCP/IP-based Internet,” proposed that information about devices on a TCP/IP-based network—configuration settings, status information, counters, and so on—could be broken down into a database of variables. Those variables could then be collected by management software to monitor and manage the IP-based network. After all, the elements of any IP-based machines would have commonalities.
SNMP is an industry standard framework and protocol that was originally released in 1988. It can be used to monitor the status of devices, make configuration changes, etc.
SNMP is an Application layer protocol that provides a message format for communication between what are termed managers and agents.

| Component                  | Description                                                                                                                                                                                                                                                |
| :------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **SNMP Manager** | A network management application running on a PC or server, typically called a **Network Management Station (NMS)**. The SNMP Manager is the application on the NMS that interacts with the managed devices; it receives notifications, sends requests for information, sends configuration changes, etc. The SNMP Server Application provides an interface for the network admin to interact with, displays alerts, statistics, charts, graphs of performance metrics. The SNMP manager uses SNMP protocols to communicate with each SNMP agent. |
| **SNMP Agent** | The software running on the managed devices (router, switch, and so on) with knowledge of all the variables of that device that describes the device's configuration status and counters. It interacts with the SNMP Manager on the NMS by forwarding or receiving information from the NMS. |
| **Managed Devices** | Many SNMP agents exist in the network, one per device that is managed. Each agent keeps a database of variables that make up the parameters, status, and counters for the operations of the device.                                                              |
| **Management Information Base (MIB)** | This database, called the Management Information Base (MIB), has some core elements in common across most networking devices. It also has a large number of variables unique to that type of device—for instance, router MIBs will include variables not needed on switch MIBs, and vice versa. This information structure contains the variables that are managed by SNMP. The MIB defines/identifies each variable as an Object ID (OID). SNMP Object IDs are organized in a Hierarchical structure. The MIB then organizes the OIDs based in part on RFC standards and in part with vendor-proprietary variables. The MIB organizes all the variables into a hierarchy of OIDs, usually shown as a tree. Each node in the tree can be described based on the tree structure sequence, either by name or by number. |

IOS on routers and switches include an SNMP agent, with a built-in MIB, that can be enabled with the configuration shown later in this chapter. The NMS uses the SNMP Get, GetNext, and GetBulk messages (together referenced simply as Get messages) to ask for information from an agent. The NMS sends an SNMP Set message to write variables on the SNMP agent as a means to change the configuration of the device. These messages come in pairs, with, for instance, a Get Request asking the agent for the contents of a variable, and the Get “RESPONSE” supplying that information.

SNMP permits much flexibility in how you monitor variables in the MIB. The NMS, with historical stored data, can then analyze various statistical facts such as averages, minimums, and maximums. To be proactive, administrators can set thresholds for certain key variables, telling the NMS to send a notification (email, text, and so on) when a threshold is passed. In addition to asking for information with Get commands and setting variables on agents with the Set command, SNMP agents can initiate communications to the NMS. These messages, generally called notifications, use two specific SNMP messages: TRAP AND INFORM. SNMP agents send a Trap or Inform SNMP message to the NMS to list the state of certain MIB variables when those variables reach a certain state.

| Notification Type | Protocol Mechanism                                                                                                                                                                                                                                                          | Reliability |
| :---------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------- |
| **SNMP Traps** | Available since SNMPv1. Uses a fire-and-forget process. The SNMP agent sends the Trap to the IP address of the NMS, with UDP as the transport protocol (as with all SNMP messages), and with no application layer error recovery. If the Trap arrives, great; if it is lost in transit, it is lost. | Unreliable  |
| **Inform Messages** | Added with SNMPv2. Similar to Trap messages but with reliability. Still uses UDP but adds application layer reliability. The NMS must acknowledge receipt of the Inform with an an SNMP Response message, or the SNMP agent will time out and resend the Inform.                   | Reliable    |

---

### Securing SNMP

SNMP supports a few security mechanisms, depending on the particular version. First, one strong method to secure SNMP is to use ACLs to limit SNMP messages to those from known servers only. SNMP agents on Cisco routers and switches support SNMP messages that flow in both IPv4 and IPv6 packets. The SNMP agent can configure an IPv4 ACL to filter incoming SNMP messages that arrive in IPv4 packets and an IPv6 ACL to filter SNMP messages that arrive in IPv6 packets. Using an IPv4 and IPv6 ACL to secure an agent makes good sense. The only hosts that should be sending SNMP messages to the SNMP agent in a router or switch are the NMS hosts. Those NMS hosts seldom move and their IP addresses should be well known to the networking staff. It makes good sense to configure an ACL that permits packets sourced from the IP addresses of all NMS hosts, but no others.

| SNMP Version | Security Mechanism                                                                                                                                                                                                                          |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **SNMPv1** | Defined clear-text passwords called SNMP communities. Both the SNMP agent and the SNMP manager need prior knowledge of the same SNMP community value (called a community string). Defines both a read-only (RO) community (allows Get messages) and a read-write (RW) community (allows both reads and writes). |
| **SNMPv2c** | (Community-based SNMP Version 2) basically kept the same community security feature as SNMPv1.                                                                                                                                             |
| **SNMPv3** | Does away with communities and replaces them with: <br> - **Message integrity:** Confirms whether or not each message has been changed during transit. <br> - **Authentication (optional):** Adds authentication with username and password, using hashing (never clear text). <br> - **Encryption (Confidentiality, optional):** Encrypts the contents of SNMPv3 messages so attackers cannot read them. |

## SYSTEM MESSAGE LOGGING (SYSLOG)

SYSLOG is an industry standard protocol. On Network devices, Syslog can be used to log events such as changes in interface status, changes in OSPF neighbor status, and system restarts. These Logs are essential when troubleshooting issues, examining the cause of incidents, etc. SYSLOG and SNMP are both used for monitoring and troubleshooting devices; they are complementary but their functionalities are different.

| Protocol | Purpose                                                                                                 | Data Flow                                       | Capabilities                                                                        |
| :------- | :------------------------------------------------------------------------------------------------------ | :---------------------------------------------- | :---------------------------------------------------------------------------------- |
| **SYSLOG** | Used for system message logging. Events categorized by facility/severity are logged, used for system management, analysis, and troubleshooting. | Messages are sent *from* devices *to* the server. | Server cannot actively pull information (like SNMP GET) or modify variables (like SNMP Set). |
| **SNMP** | Used to retrieve and organize information about SNMP-managed devices.                                   | Manager queries clients (GET) and modifies variables (SET). | Manager can actively pull information and modify variables.                             |

IOS dictates most of the contents of the messages, but you can at least toggle on and off the use of the timestamp (which is included by default) and a log message sequence number (which is not enabled by default). Log messages may just tell you about some mundane event, or they may tell you of some critical event. To help you make sense of the importance of each message, IOS assigns each message a severity level: the lower the number, the more severe the event that caused the message.

### Syslog Severity Levels

| Level Number | Keyword       | Description                                  |
| :----------- | :------------ | :------------------------------------------- |
| `0`          | EMERGENCY     | System is Unusable                           |
| `1`          | ALERT         | Action must be taken immediately             |
| `2`          | CRITICAL      | Critical Conditions                          |
| `3`          | ERROR         | Error Conditions                             |
| `4`          | WARNING       | Warning Conditions                           |
| `5`          | NOTICE        | Normal But significant condition             |
| `6`          | INFORMATION   | Informational Messages                       |
| `7`          | DEBUG         | Debug Level Message                          |

Of the eight log message severity levels, one level, debug level (7), has a special purpose: for messages generated as a result of a user logged in to the router or switch who issues a debug command. The `DEBUG` EXEC command gives the network engineer a way to ask IOS to monitor for certain internal events, with that monitoring process continuing over time, so that IOS can issue log messages when those events occur. The engineer can log in, issue the debug command, and move on to other work. The user can even log out of the device, and the debug remains enabled. IOS continues to monitor the request in that debug command and generate log messages about any related events. The debug remains active until some user issues the “no debug” command with the same parameters, disabling the debug.
While the debug command is just one command, it has a huge number of options, much like the show command may be one command, but it also has many, many options. The console user sees the log messages created on behalf of that debug command after the debug command completes. Note that all enabled debug options use router CPU, which can cause problems for the router. You can monitor CPU use with the `show process cpu` command, but you should use caution when using debug commands carefully on production devices. Also, note the more CLI users that receive debug messages, the more CPU that is consumed. So, some installations choose to not include debug-level log messages for console and terminal logging, requiring users to look at the logging buffer or syslog for those messages, just to reduce router CPU load.

### SYSLOG MESSAGE FORMAT

```
Seq:time_stamp: %facility-severity-MNEMONIC:description
```
* **Sequence Number:** Indicating the order/sequence of messages
* **Time Stamp:** Indicating the time the message was generated
* **Facility:** A value that indicates which process on the devices generated the message
* **Severity:** A number that indicates the severity of the logged event
* **MNEMONIC:** A short code for the message, indicating what happened
* **Description:** Detailed Information in Natural Language about the event being reported

```cli
R1(config-line)# logging synchronous
R1(config)# service timestamps log [datetime | uptime] sec
R1(config)# service sequence-numbers
```

### SYSLOG MESSAGE LOCATION

#### Console Line
Syslog messages will be displayed in the CLI when connected to the device via the console port. By default, IOS shows log messages to console users for all severity levels of messages. That default happens because of the default `logging console` global configuration command.

```cli
R1(config)# logging console severity-level
R1(config)# logging console 6
```
*You can use the level number (6) or keyword (informational).
*This will enable logging for the informational severity and higher.

#### VTY Lines
Syslog messages will be displayed in the CLI when logged on to the device via Telnet/SSH. Disabled by default.

```cli
R1(config)# logging monitor severity-level
R1(config)# logging monitor informational
PC# terminal monitor
```
IOS has another global configuration setting—`logging monitor`—that tells IOS to enable the sending of log messages to all logged users. However, that default configuration is not enough to allow the user to see the log messages. The user must also issue the—`terminal monitor`—EXEC command during the login session, which tells IOS that this terminal session would like to receive log messages.

#### Buffer
Syslog messages will be saved to RAM. By default, all messages are displayed. View the messages with `show logging`.

```cli
R1(config)# logging buffered [size] severity
R1(config)# logging buffered 8192 6
```
*Same points as above about the level.
*Buffer size is in bytes.
IOS can store copies of the log messages in RAM by virtue of the `logging buffered` global configuration command. Then any user can come back later and see the old log messages by using the `show logging` EXEC command. You could also clear out the old messages from the log with the `clear logging` EXEC command.

#### External Server
You can Configure the device to send Syslog messages to an external server. Syslog servers will listen for messages on UDP port 514. A server application that collects syslog messages from many devices over the network and stores them in a database. The syslog server also provides a user interface, so that IT administrators can view the log messages to troubleshoot problems; it also has reporting capabilities on these system messages. Some syslog servers can even respond to select system messages with certain actions such as emailing and paging.

```cli
R1(config)# logging host 192.168.1.100
R1(config)# logging trap severity-level
```
An option used frequently in production networks—all devices store their log messages centrally to a syslog server. RFC 5424 defines the syslog protocol, which provides the means by which a device like a switch or router can use a UDP protocol to send messages to a syslog server for storage. All devices can send their log messages to the server. Later, a user can connect to the server (typically with a graphical user interface) and browse the log messages from various devices. To configure a router or switch to send log messages to a syslog server, add the `logging host {address | hostname }` global command, referencing the IP address or host name of the syslog server. Use the `logging trap severity-level` to configure the severity level.

### Syslog Configuration Commands Summary

| Command                                   | Description                                                                  |
| :---------------------------------------- | :--------------------------------------------------------------------------- |
| `[no] logging console`                    | Global command that enables (or disables with the `no` option) logging to the console device. |
| `[no] logging monitor`                    | Global command that enables (or disables with the `no` option) logging to users connected to the device with SSH or Telnet. |
| `[no] logging buffered`                   | Global command that enables (or disables with the `no` option) logging to an internal buffer. |
| `logging [host] ip-address | hostname` | Global command that enables logging to a syslog server.                       |
| `logging console level-name | level-number` | Global command that sets the log message level for console log messages.       |
| `logging monitor level-name | level-number` | Global command that sets the log message level for log messages sent to SSH and Telnet users. |
| `logging buffered level-name | level-number` | Global command that sets the log message level for buffered log messages displayed later by the `show logging` command. |
| `logging trap level-name | level-number` | Global command that sets the log message level for messages sent to syslog servers. |
| `[no] service sequence-numbers`           | Global command to enable or disable (with the `no` option) the use of sequence numbers in log messages. |

```markdown
## NETWORK TIME PROTOCOL (NTP) (UDP PORT 123)

NTP’s job is to synchronize clocks, but NTP works best if you set the device clock to a reasonably close time before enabling the NTP client function with the NTP server command. Setting the time correctly gives NTP a good start toward synchronizing.

Routers, switches, other networking devices, and pretty much every device known in the IT world has a time-of-day clock. For a variety of reasons, it makes sense to synchronize those clocks so that all devices have the same time of day, other than differences in time zone. The Network Time Protocol (NTP) provides the means to do just that. NTP gives any device a way to synchronize their time-of-day clocks. NTP provides protocol messages that devices use to learn the timestamp of other devices. Devices send timestamps to each other with NTP messages, continually exchanging messages, with one device changing its clock to match the other, eventually synchronizing the clocks. As a result, actions that benefit from synchronized timing, like the timestamps on log messages, work much better.

Manually configuring the time on devices is not scalable; the manually configured clocks will drift, resulting in inaccurate time. NTP allows automatic syncing of time over a Network. Although the hardware calendar (built-in-clock) is the default time-source, the hardware clock and software clock are separate and can be configured separately.

NTP Clients request the time from NTP Servers, and then they synchronize their time to the time of the server. A device can be an NTP Server and an NTP Client at the same time. It will sync its time to a server, and other devices will sync their time to it. NTP allows accuracy of time within ~1 millisecond if the NTP server is in the same LAN, or ~50 milliseconds if connecting to the NTP server over a WAN/via Internet.

Some NTP Servers are better/more reliable than others; the distance of an NTP Server from the original reference clock is called a **STRATUM**. A high stratum level is considered less accurate.

| Stratum Level | Description                                                                                                                                                                                                                                                              |
| :------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **0** | A Reference Clock is usually a very accurate time device like an atomic clock or a GPS clock. Reference clocks are stratum 0 within the NTP hierarchy.                                                                                                                   |
| **1** | NTP servers directly connected to reference clock @stratum0 are known as Stratum 1 (i.e., Google servers). These are also called Primary Servers (an NTP primary server acts only as a server, with a reference clock external to the device, and has a stratum level of 1). |
| **2** | Stratum 2 NTP servers get their time from stratum1 servers, and so on. These are called Secondary Servers. They operate in server mode and client mode at the same time. NTP secondary servers are servers that use client/server mode, relying on synchronization with some other NTP server. |
| **15** | Stratum 15 is the maximum useful stratum. Anything above that is considered unreliable.                                                                                                                                                                                  |

NTP servers and clients use a number to show the perceived accuracy of their reference clock data based on stratum level. The lower the stratum level, the more accurate the reference clock is considered to be. An NTP server that uses its internal hardware or external reference clock sets its own stratum level. Then, an NTP client adds 1 to the stratum level it learns from its NTP server, so that the stratum level increases the more hops away from the original clock source.

Devices can also peer with devices at the same stratum to provide more accurate time. This is called **Symmetric Active mode**. Cisco devices can operate in three NTP modes: Server Mode, Client Mode, Symmetric Active Mode.

### NTP Configuration Commands

| Command                                      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| :------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RT(config)# ntp peer peer-address`          | To configure Symmetric Active mode on devices connected, use this command on both devices participating in peering.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `RT(config)# ntp master`                     | When configured with the `ntp master` command, a Cisco router/switch uses its internal device hardware to determine the time.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `RT(config)# ntp master ?<1-15>StratumNumlevel` | Enables the device to act as NTP master clock in the absence of a configured Reference Clock/Primary/Secondary NTP server. Basically, the device will use its Internal Clock as the Reference Clock. Routers and switches use the default stratum level of 8 for their internal reference clock based on the default setting of 8 for the stratum level in the `ntp master [stratum-level]` command. NTP considers 15 to be the highest useful stratum level, so any devices that calculate their stratum as 16 consider the time data unusable and do not trust the time. So, avoid setting higher stratum values on the `ntp master` command.                                                                                                                                                                                                                |
| `RT(config)# ntp server {IP-addr | Hostname}` | NTP client/server mode—the device acts as both client and server. First, it acts as an NTP client, to synchronize time with a server specified by Ip-addr/Hostname. Once synchronized, the device can then act as an NTP server, to supply time to other NTP clients.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `RT(config)# ntp source interface-ID`        | This command sets the specified interface as the source of its NTP messages to other connected devices locally. Therefore, other connected devices will use the device’s loopback interface as their NTP server. It’s recommended to use a loopback interface for High Availability. An NTP server will accept NTP messages arriving to any of its IPv4 addresses by default. However, the clients reference a specific IP address on the NTP server. That creates an availability issue. Using Physical Interfaces might lead to issues with NTP between other devices depending on this device as its NTP server, as such interfaces are prone to failures. What is needed is a way to send a packet, a way that is not tied to the state of any one interface. That is, as long as there is some path to send packets to the NTP server, allow NTP to keep working. The goal is to avoid the case in which a single interface failure on a router also causes NTP to fail. Cisco uses the router loopback interface to meet that exact need. A Loopback interface is a virtual interface on a router, independent of physical interfaces. It provides a consistent IP address to identify or reach the router. |
| `RT(config)# ntp update-calendar`            | To synchronize/update the calendar with NTP.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### NTP Authentication

NTP Authentication can be configured, although optional, it allows NTP clients to ensure they only sync to the intended servers. To configure NTP authentication, use:

```cli
NTP authenticate
NTP authentication-key key-number md5 key-string
NTP trusted-key key-number
NTP server ip-address key key-number
NTP peer ip-address key key-number
```

### Time Zone Configuration

NTP uses only the UTC time zone, you must configure the appropriate timezone on each device. NTP doesn’t update the calendar (Hardware default time-source) by default, but updates the clock (Software Time-Source). The Hardware clock (time-source) tracks the date and time on a device between restarts or power loss. During a restart, a Hardware clock is usually the clock to initialize the software clock, meaning the software clock picks up time info from the hardware.

| Command                                                      | Description                                                                 |
| :----------------------------------------------------------- | :-------------------------------------------------------------------------- |
| `RT(config)# clock timezone name hours-offset [minutes-offset]` | Configures the Timezone from Global Config Mode. Name (i.e., GMT, EST) and Hours-Offset from UTC. |
| `RT(config)# clock summer-time name recurring start end [offset]` | Configures the DayLight Savings Time. The `recurring` keyword tells the device to spring forward an hour and fall back an hour automatically over the years. |
| `RT# clock set hh:mm:ss {day|month} {month|day} year`        | To configure Time (Software Time-Source) Manually.                        |
| `RT# calendar set hh:mm:ss {day|month} {month|day} year`     | To configure Time (Hardware default time-source) Clock Manually.          |
| `RT# clock update-calendar`                                  | To Synchronize/update the calendar to the clock’s time.                     |
| `RT# clock read-calendar`                                    | To Synchronize the clock’s time to the calendar’s time.                     |

### NTP Design Considerations

For good design, the enterprise NTP configuration ought to refer to at least two external NTP servers for redundancy. Additionally, just a few enterprise devices should refer to those external NTP servers and then act as both NTP client and server. The majority of the devices in the enterprise would act as NTP clients. In addition to referencing redundant NTP primary servers, some routers in the enterprise need to be ready to supply clock data if those NTP primary servers become unreachable. To overcome this potential issue, the routers can also be configured with the `ntp master` command, resulting in this logic:

1. Establish an association with the NTP servers per the `ntp server` command.
2. Establish an association with your internal clock using the `ntp master stratum` command.
3. Set the stratum level of the internal clock (per the `ntp master {stratum-level}` command) to a higher (worse) stratum level than the Internet-based NTP servers.
4. Synchronize with the best (lowest) known time source, which will be one of the Internet NTP servers in this scenario.

### NTP Show Commands

| Command                    | Description                                                                 |
| :------------------------- | :-------------------------------------------------------------------------- |
| `RT# show ntp associations`| Displays all NTP servers discovered, with their reference clock.            |
| `RT# show ntp status`      | Displays clock synchronization, Stratum level, Reference Clock IP address, Precision of Reference Clock, Offset from Reference clock in seconds, etc. |
| `RT# show clock`           | Displays the Clock Time (Software Clock) in UTC.                            |
| `RT# show calendar`        | Displays the Calendar Time (Hardware default time-source) in UTC.           |
| `RT# show clock detail`    | Displays the time and the Time-Source.                                      |
| `RT# show logging`         | This command displays the device logs (important for accurate timestamps).  |

---

## FTP AND TFTP

File Transfer Protocol (FTP) and Trivial File Transfer Protocol (TFTP). Both exist as TCP/IP protocols defined in RFCs. Both use a client and server model, in which the client connects to a server and then the client can copy files to the server or from the server.

### File Transfer Protocol (FTP)

FTP uses TCP as its transport protocol, relying on TCP to provide an error-free, in-order delivery of data so that the FTP application knows that each file transfer creates an exact copy of the file with no omissions. FTP reserves two well-known ports: port 21 for control connections and port 20 for data connections. However, due to changes to FTP over the years, FTP often uses other TCP ports for the TCP data connection.

A typical FTP process involves:
1.  Host A creating a TCP connection to the server (which takes the usual three TCP messages).
2.  Exchange that allows the server to authenticate the client.
3.  Once authenticated, the client and server can send FTP commands over the connection to tell the other device what to do. The commands that flow over this initial TCP connection—called the **FTP control connection**—define the kinds of functions supported by FTP.

**Summary of some of the FTP actions/functions:**
* **Navigate directories:** List the current directory, change the current directory to a new directory, go back to the home directory, all on both the server and client side of the connection.
* **Add/remove directories:** Create new directories and remove existing directories on both the client and server.
* **List files:** List files on both the client and server.
* **File transfer:** Get (client gets a copy of the file from the server), Put (client takes a file that exists on the client and puts a copy on the FTP server).

While many OSs support command-line FTP clients, which require you to learn the various FTP commands and use those from the command line, most users instead use an FTP client app (like FileZilla) that issues the FTP commands behind the scenes. The FTP server can be a server application installed and managed by others, or you can install or enable an FTP server for your own use. A simple Internet search can show a variety of FTP server applications that run on the common desktop OSs. A practical view of the most common use of TFTP and FTP by network engineers while on the job is updating & Managing Cisco IOS Images with FTP/TFTP.

#### FTP Active and Passive Modes

The choice of mode may impact whether the TCP client can or cannot connect to the server and perform normal functions. The user at the FTP client can choose which mode to use; FTP passive mode may be the more likely option to work. First, note that FTP uses two types of TCP connections:
* **Control Connection:** Used to exchange FTP commands.
* **Data Connection:** Used for sending and receiving data, both for file transfers and for output to display to a user.

When a client connects to an FTP server, the client first creates the FTP control connection. The server listens for new control connections on its well-known port 21; the client allocates any new dynamic port (e.g., 49222) and creates a TCP connection to the server.

**FTP Active Mode Process to Create the Data Connection:**
1.  The FTP client allocates a currently unused dynamic port and starts listening on that port.
2.  The client identifies that port (and its IP address) to the FTP server by sending an FTP PORT command to the server.
3.  The server, because it also operates in active mode, expects the PORT command; the server reacts and initiates the FTP data connection to the client’s address (e.g., 192.168.1.102) and port (e.g., 49333).
    * In Active Mode, the server initiates the data connection, hence the issues with firewalls.

Active mode works well with both the FTP client and server sitting inside the same enterprise network. When within the same network, typically no NAT function and no firewall sits between the two. However, if the FTP client sits in an enterprise network, and the FTP server resides somewhere in the Internet, an active mode connection typically fails. Most firewalls do not allow Internet-based hosts/outside devices to initiate TCP connections to hosts inside the enterprise without a specific firewall rule allowing connections to a known port, and in this case, the FTP client allocates any available port number.

**FTP Passive Mode Process to Create the Data Connection:**
Passive mode helps solve the firewall restrictions by “having the FTP client initiate the FTP data connection to the server”. However, passive mode does not simply cause the FTP client to connect to a well-known port on the server; it requires more exchanges of port numbers to use between the server and client, with these steps:
1.  The FTP client changes to use FTP passive mode, notifying the server using the FTP PASV command.
2.  The server chooses a port to listen on for the upcoming new TCP connection, in this case TCP port 49444.
3.  The FTP server notifies the FTP client of its IP address and chosen port with the FTP PORT command.
4.  The FTP client opens the TCP data connection to the IP address and port learned at the previous step.

#### FTP over TLS or as FTP Secure (FTPS)

Over the years, several RFCs defined security improvements for FTP. Those new features include using digital certificates for authentication as well as using Transport Layer Security (TLS) to encrypt all data (including usernames/passwords). Fast forward to today and many of those features converge into what most FTP clients and servers support as FTP over TLS or as FTP Secure (FTPS).
With FTPS, the client and server still use FTP commands and still use both a control and data connection. However, FTPS encrypts both the control and data connections with TLS, including the exchange of the usernames and passwords. FTPS includes a few variations, including the **FTPS Explicit Mode Control and Data Connection Establishment process:**
1.  The client creates the FTP control TCP connection to server well-known port 21.
2.  The client initiates the use of TLS in the control connection with the FTP AUTH command.
3.  When the user takes an action that requires an FTP data connection, the client creates an FTP data TCP connection to server well-known port 21.
4.  The client initiates the use of TLS in the data connection with the FTP AUTH command.

In contrast, the **Implicit Mode process** begins with a required TLS connection, with no need for an FTP AUTH command, using well-known ports 990 (for the control connection) and 989 (for the data connection).

**Note:** SSH File Transfer Protocol (SFTP) is a different protocol than FTPS. SFTP uses SSH to encrypt file transfers over an SSH connection.

### Trivial File Transfer Protocol (TFTP)

TFTP uses UDP well-known port 69. Because it uses UDP, which is connectionless and unreliable, TFTP adds a Reliability feature to check each file for transmission errors by using a checksum process on each file after the transfer completes. Timers are used, and if an expected message isn’t received in time, the waiting device will re-send its previous message. Every TFTP data message is acknowledged by either Client/Server. TFTP uses “lock-step” communication. The client and server alternately send a message and then wait for a reply (retransmissions are sent as needed). TFTP file transfers have three Phases: Connection, Data Transfer, Termination.

The word "Trivial" in the name refers to its relatively small number of features, meant to be an advantage by making the tool lightweight. For instance, it supports far fewer commands than FTP (fewer functions), meaning that the code requires less space to install, which can be useful for devices with limited memory. TFTP can Get and Put files, but it includes no commands to change directories, create/remove directories, or even to list files on the server. TFTP does not support even simple clear-text authentication. In effect, if a TFTP server is running, it should accept requests from any TFTP client. No Authentication, No Encryption; all data is sent in plain text. TFTP has its best use as a temporary tool for quick file transfers in a controlled environment, particularly when the data itself does not have to be secure.

---

## Network Address Translation (NAT)

NAT, as defined in RFC 3022, allows a host that does not have a valid, registered, globally unique IP address to communicate with other hosts through the Internet. The hosts might be using private addresses or addresses assigned to another organization. In either case, NAT allows these addresses that are not Internet-ready to continue to be used and still allows communication with hosts across the Internet.

NAT achieves its goal by using a valid registered Public IP address to advertise or represent the Private IP address to the rest of the Internet. The NAT function changes the private IP addresses to publicly registered IP addresses inside each IP packet. The router, performing NAT, changes the packet’s SOURCE IP address when the packet leaves the private organization. The router performing NAT also changes the destination address in each packet that is forwarded back into the private network.

This lecture discusses Source NAT, which is the type of NAT that allows enterprises to use private addresses and still communicate with hosts in the Internet. Within source NAT, Cisco IOS supports several different ways to configure NAT: Static NAT, Dynamic NAT, and PAT (Port Address Translation).

### Static NAT

Static NAT creates a permanent, one-to-one mapping between a private (inside local) IP address and a public (inside global) IP address. Each static mapping between a local (private) address and a global (public) address must be configured. In addition, because NAT may be used on a subset of interfaces, the router must be told on which interfaces it should use NAT. Those same interface subcommands tell NAT whether the interface is inside or outside.

**Configuration Steps:**
1.  Use the `ip nat inside` command in interface configuration mode to configure interfaces to be in the inside part of the NAT design.
2.  Use the `ip nat outside` command in interface configuration mode to configure interfaces to be in the outside part of the NAT design.
3.  Use the `ip nat inside source static {inside-local} {inside-global}` command in global configuration mode to configure the static mappings.

The static mappings are created using the `ip nat inside source static` command.
* The `inside` keyword means that NAT translates addresses for hosts on the inside part of the network.
* The `source` keyword means that NAT translates the source IP address of packets coming into its inside interfaces.
* The `static` keyword means that the parameters define a static entry, which should never be removed from the NAT table because of timeout.

**Configuration Commands Example (R1):**
* `R1(config)#int g0/1`
    * `R1(config-if)#ip nat inside`: Designates GigabitEthernet 0/1 as the interface connected to the internal network.
* `R1(config)#int g0/0`
    * `R1(config-if)#ip nat outside`: Designates GigabitEthernet 0/0 as the interface connected to the external network.
* `R1(config)#ip nat inside source static 192.168.0.167 100.0.0.1`: Creates a static mapping where the inside local IP 192.168.0.167 is translated to the inside global IP 100.0.0.1.
* `R1(config)#ip nat inside source static 192.168.0.168 100.0.0.2`: Creates another static mapping for 192.168.0.168 to 100.0.0.2.

**Key Takeaway:** Static NAT provides a predictable and persistent mapping, often used for servers or devices that need to be consistently accessible from the outside.

### Dynamic NAT

Dynamic NAT sets up a pool of possible inside global addresses and defines matching criteria to determine which inside local IP addresses should be translated with NAT. The router assigns public IP addresses from a pool to internal hosts on a first-come, first-served basis. The mapping of an inside local address to an inside global address happens dynamically. NAT can be configured with more IP addresses in the inside local address list than in the inside global address pool. The router allocates addresses from the pool until all are allocated. The inside global pool of addresses needs to be as large as the maximum number of concurrent hosts that need to use the Internet at the same time—unless you use PAT.

* **Access Control List (ACL):** An ACL is used to define which internal traffic is eligible for NAT. Traffic not permitted by the ACL will not be translated (but importantly, it won't be dropped at this stage). Dynamic NAT uses an access control list (ACL) to identify which inside local (private) IP addresses need to have their addresses translated.
* **NAT Pool:** A range of public IP addresses is defined in a NAT pool for dynamic assignment.
* **One-to-One Mapping (Initially):** Although dynamic, the initial mapping is still one-to-one until the pool is exhausted.
* **NAT Pool Exhaustion:** When all public IP addresses in the pool are in use, new connection attempts from internal hosts requiring NAT will fail, and their packets will be dropped.
* **Timeout:** Dynamic NAT translations have a timeout period and can also be cleared manually. The dynamic entry stays in the table as long as traffic flows occasionally. You can configure a timeout value that defines how long the router should wait, having not translated any packets with that address, before removing the dynamic entry. You can also manually clear the dynamic entries from the table using the `clear ip nat translation` command.

**Configuration Steps:**
1.  Use the `ip nat inside` command in interface configuration mode to configure interfaces to be in the inside part of the NAT design.
2.  Use the `ip nat outside` command in interface configuration mode to configure interfaces to be in the outside part of the NAT design.
3.  Configure an ACL that matches the packets entering inside interfaces for which NAT should be performed.
4.  Use the `ip nat pool name start-ip end-ip {netmask subnet-Mask | prefix-length length}` command in global configuration mode to configure the pool of public registered IP addresses. Dynamic NAT configures the pool of public (global) addresses with the `ip nat pool` command listing the first and last numbers in an inclusive range of inside global addresses.
5.  Use the `ip nat inside source list acl-number/acl-name pool pool-name` command in global configuration mode to enable dynamic NAT. Note the command references the ACL (step 3) and pool (step 4) per previous steps. The logic for the `ip nat inside source list X pool Y` command in this example is as follows: Create NAT table entries that map between hosts matched by ACL called X, for packets entering any inside interface, allocating an inside global address from the POOL called Y.

### Port Address Translation (PAT), also known as NAT Overloading

The NAT Overload feature, also called Port Address Translation (PAT), solves this problem of scaling. Overloading allows NAT to scale to support many clients with only a few public IP addresses. NAT overload (PAT) translates not only the address, but the port number when necessary, making what looks like many TCP or UDP flows from different hosts look like the same number of flows from one host. This allows multiple internal hosts to share a single public IP address by using different port numbers. When PAT creates the dynamic mapping, it selects not only an inside global IP address but also a unique port number to use with that address. The NAT router keeps a NAT table entry for every unique combination of inside local IP address and port, with translation to the inside global address and a unique port number associated with the inside global address. And because the port number field has 16 bits, NAT overload can use more than 65,000 port numbers, allowing it to scale well without needing many registered IP addresses—in many cases, needing only one inside global IP address.

Two variations of PAT configuration exist in IOS:
1.  If PAT uses a pool of inside global addresses, the configuration looks exactly like dynamic NAT, except the `ip nat inside source list global` command has an `overload` keyword added to the end.
2.  If PAT just needs to use one inside global IP address, the router can use one of its interface IP addresses (interface configured with `ip nat outside`). Because NAT can support over 65,000 concurrent flows with a single inside global address, a single public IP address can support an entire organization’s NAT needs.

**Configuration Commands for PAT using a Pool:**
1.  Use the `ip nat inside` command in interface configuration mode to configure interfaces to be in the inside part of the NAT design.
2.  Use the `ip nat outside` command in interface configuration mode to configure interfaces to be in the outside part of the NAT design.
3.  Configure an ACL that matches the packets entering inside interfaces for which NAT should be performed.
4.  Use the `ip nat pool name start-ip end-ip {netmask subnet-Mask | prefix-length length}` command in global configuration mode to configure the pool of public registered IP addresses. Dynamic NAT/PAT (1) configures the pool of public (global) addresses with the `ip nat pool` command listing the first and last numbers in an inclusive range of inside global addresses.
5.  Use the `ip nat inside source list {acl-number|acl-name} pool pool-name {overload}` command in global configuration mode to enable dynamic NAT.

**Configuration Commands for PAT using a Specified Interface:**
1.  Use the `ip nat inside` command in interface configuration mode to configure interfaces to be in the inside part of the NAT design.
2.  Use the `ip nat outside` command in interface configuration mode to configure interfaces to be in the outside part of the NAT design.
3.  Configure an ACL that matches the packets entering inside interfaces for which NAT should be performed.
4.  Configure the `ip nat inside source list {acl-number|acl-name} interface type/number {overload}` global configuration command, referring to the ACL created in step 3 and to the interface whose IP address will be used for translations.
    * **Note:** NAT translates only using the inside global address (IP address of the interface configured with `ip nat outside`) only, so the NAT pool is not required.

The `OVERLOAD` keyword is indeed the key differentiator that turns a dynamic NAT configuration (using a pool) into a Port Address Translation (PAT) configuration. The `overload` parameter means that overload is enabled. Without this parameter, the router does not perform overload, just dynamic NAT. Such configuration supports multiple internal hosts sharing the public IP range through PAT.

**Here's how it works:**
* **Without the `overload` keyword (Basic Dynamic NAT with a Pool):**
    When you configure dynamic NAT with a pool of public IP addresses and map it to an ACL, the router aims for a one-to-one mapping of inside local IP addresses to inside global IP addresses from the pool. Each internal host that initiates an an outside connection will be assigned a unique public IP address from the available pool. If the NAT pool becomes exhausted (all public IPs are in use), any new internal hosts trying to establish an outside connection will be blocked because there are no more unique public IPs to assign.
* **With the `overload` keyword (PAT):**
    The `overload` keyword fundamentally changes how the router utilizes the public IP addresses in the defined pool. Instead of aiming for a strict one-to-one IP mapping, it allows multiple inside local IP addresses to be translated to the same inside global IP address.
    * The router achieves this multiplexing by using different source port numbers for the connections originating from different internal hosts.
    * When an internal host sends traffic out, the router translates its private IP address to a public IP address from the pool (it might even use the same public IP for multiple internal hosts simultaneously). Crucially, it also assigns a unique high-numbered source port to this connection.
    * The combination of the public IP address and the unique source port acts as a unique identifier for the connection.
    * When the external server sends a reply, it comes back to the public IP address and the specific port number that the router had recorded. The router can then use this port number to determine which internal host the traffic belongs to and forward it accordingly.

In essence, the `overload` keyword instructs the router to:
* Utilize the public IP addresses in the pool more efficiently by allowing multiple private IPs to share a single public IP.
* Use port numbers as an additional layer of identification to distinguish between different connections originating from different internal hosts that are all translated to the same public IP.

Therefore, the presence of the `overload` keyword in the `ip nat inside source list <acl> pool <pool-name> overload` command is the defining characteristic that distinguishes a basic dynamic NAT configuration (where the goal is a one-to-one IP mapping from a pool) from a PAT configuration (where the goal is to allow many internal hosts to share a smaller number of public IPs using port multiplexing).

### NAT Troubleshooting

The majority of NAT troubleshooting issues relate to getting the configuration correct. Source NAT has several configuration options—static, dynamic, PAT—with several configuration commands for each. You should work hard at building skills with the configuration so that you can quickly recognize configuration mistakes. The following troubleshooting checklist summarizes the most common source NAT issues, most of which relate to incorrect configuration.

* **Reversed inside and outside:** Ensure that the configuration includes the `ip nat inside` and `ip nat outside` interface subcommands and that the commands are not reversed. With source NAT, only the inside interface triggers IOS to add new translations, so designating the correct inside interfaces is particularly important.
* **Static NAT:** Check the `ip nat inside source static` command to ensure it lists the inside local address first and the inside global IP address second.
* **Dynamic NAT (ACL):** Ensure that the ACL configured to match packets sent by the inside hosts match that host’s packets before any NAT translation has occurred.
* **Dynamic NAT (pool):** For dynamic NAT without PAT, ensure that the pool has enough IP addresses. When not using PAT, each inside host consumes one IP address from the pool. A large or growing value in the second misses counter in the `show ip nat statistics` command output can indicate this problem. Also, compare the configured pool to the list of addresses in the NAT translation table (`show ip nat translations`). Finally, if the pool is small, the problem may be that the configuration intended to use PAT and is missing the `overload` keyword (see the next item).
* **PAT:** It is easy to forget to add the `overload` option on the end of the `ip nat inside source list` command. PAT configuration is identical to a valid dynamic NAT configuration except that PAT requires the `overload` keyword. Without it, dynamic NAT works, but the pool of addresses is typically consumed very quickly. The NAT router will not translate nor forward traffic for hosts if there is not an available pool IP address for their traffic, so some hosts experience an outage.
* **ACL:** Perhaps NAT has been configured correctly, but an ACL exists on one of the interfaces, discarding the packets. Note that the order of operations inside the router matters in this case. For packets entering an interface, IOS processes ACLs before NAT. For packets exiting an interface, IOS processes any outbound ACL after translating the addresses with NAT.
* **User traffic required:** NAT reacts to user traffic. If you configure NAT in a lab, NAT does not act to create translations (`show ip nat translations`) until some user traffic enters the NAT router on an inside interface, triggering NAT to do a translation. The NAT configuration can be perfect, but if no inbound traffic occurs that matches the NAT configuration, NAT does nothing.
* **IPv4 routing:** IPv4 routing could prevent packets from arriving on either side of the NAT router. Note that the routing must work for the destination IP addresses used in the packets.

### Definitions of Address Types:

This section clearly defines the four types of IP addresses involved in NAT. Cisco uses the term **inside local** for the private IP addresses and **inside global** for the public IP addresses. Using NAT terminology, the enterprise network that uses private addresses, and therefore needs NAT, is the “inside” part of the network. The Internet side of the NAT function is the “outside” part of the network. A host that needs NAT has the IP address it uses inside the network, and it needs an IP address to represent it in the outside network. So, because the host essentially needs two different addresses to represent it, you need two terms. Cisco calls the private IP address used in the inside network the inside local address and the address used to represent the host to the rest of the Internet the inside global address.

* **Inside Local:** IP of the internal host from the internal network's perspective (private IP). *Local:* Means not global; that is, local. It is the address used for that host while the packet flows in the local enterprise rather than the global Internet.
* **Inside Global:** IP of the internal host as seen by the external network (public IP after NAT). *Global:* Means global as in the global Internet. It is the address used for that host while the packet flows in the Internet.
* **Outside Local:** This term is not used with source NAT. With destination NAT, IP of the external host as seen by its internal network. The address used to represent the external host as packets pass through its local network.
* **Outside Global:** IP of the external host as seen by the external network. Think of it as outside public, because the address is typically a public IPv4 address.

* **Important Note:** It highlights that unless Destination NAT is used, the Outside Local and Outside Global addresses will often be the same.

### Private IPv4 Addresses (RFC 1918)

IPv4 doesn't provide enough addresses for all devices that need an IP address in the modern world. The long-term solution is to switch to IPv6. There are three main short-term solutions:
1.  **CIDR (Classless Inter-Domain Routing):** Defined in RFC 4632, has two main goals. First, CIDR defines a way to assign public IP addresses, worldwide, to allow Route-Aggregation or Route-Summarization. These route summaries greatly reduce the size of routing tables in Internet routers. The second major CIDR feature allows RIRs and ISPs to reduce waste by assigning a subset of a classful network to a single customer. These CIDR blocks act very much like a public IP network; in particular, they give each company a consecutive set of public IPv4 addresses to use. The public address assignment process has much less waste than before as well. In fact, most public address assignments for the last 20 years have been a CIDR block rather than an entire Class A, B, or C network.
2.  **Private IPv4 addresses:** When building a private network that will have no Internet connectivity, you can use IP network numbers called **Private Internets**, as defined in RFC 1918, “Address Allocation for Private Internets.” This RFC defines a set of networks that will never be assigned to any organization as a registered network number. Instead of using someone else’s registered network numbers, you can use numbers in a range that are not used by anyone else in the public Internet. In other words, any organization can use these network numbers. However, no organization is allowed to advertise these networks using a routing protocol on the Internet.
3.  **NAT:** Defined in RFC 3022, allows a host that does not have a valid, registered, globally unique IP address to communicate with other hosts through the Internet. The hosts might be using private addresses or addresses assigned to another organization. In either case, NAT allows these addresses that are not Internet ready to continue to be used and still allows communication with hosts across the Internet. NAT achieves its goal by using a valid registered Public IP address to advertise or represent the Private IP address to the rest of the Internet. The NAT function changes the private IP addresses to publicly registered IP addresses inside each IP packet.

**RFC 1918 specifies the following IPv4 address ranges as private:**

| IP Network Range          | Class | Number of Networks |
| :------------------------ | :---- | :----------------- |
| `10.0.0.0/8` (10.0.0.0 to 10.255.255.255) | A     | 1                  |
| `172.16.0.0/12` (172.16.0.0 to 172.31.255.255) | B     | 16                 |
| `192.168.0.0/16` (192.168.0.0 to 192.168.255.255) | C     | 256                |

**Summary of IPv4 Address Solutions:**

| Feature       | RFC(s) | Main Benefits                                                                                                                                                                                                                                                                     |
| :------------ | :----- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **CIDR** | 4632   | Assign more-specific public IPv4 address blocks to companies than Class A, B, and C networks. Aggregate routes to public IPv4 addresses based on worldwide address allocation plan.                                                                                              |
| **NAT** | 3022   | Enable approximately 65,000 TCP/UDP sessions to be supported by a single public IPv4 address.                                                                                                                                                                                     |
| **Private Networks** | 1918   | Enable the use of NAT for enterprise Internet connections, with private addresses used inside the enterprise.                                                                                                                                                                 |

### NAT Show and Clear Commands

| Command                                                                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :------------------------------------------------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `show ip nat translations {verbose}`                                    | Lists the static & dynamic NAT entries created in the configuration.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `show ip nat statistics`                                                | Lists statistics, including the number of currently active translation table entries. The statistics also include the number of hits, which increments for every packet for which NAT must translate addresses. The `show ip nat statistics` command lists some particularly interesting troubleshooting information with two different counters labeled “misses.” The first occurrence of this counter counts the number of times a new packet comes along, needing a NAT entry, and not finding one. At that point, dynamic NAT reacts and builds an entry. The second misses counter toward the end of the command output lists the number of misses in the pool. This counter increments only when dynamic NAT tries to allocate a new NAT table entry and finds no dynamically available addresses, so the packet cannot be translated—probably resulting in an end user not getting to the application. |
| `debug ip nat`                                                          | Issues a log message describing each packet whose IP address is translated with NAT. This debug command causes the router to issue a message every time a packet has its address translated for NAT.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `clear ip nat translation {* | [inside global-ip local-ip] [outside local-ip global-ip]}` | Clears all or some of the dynamic entries in the NAT table, depending on which parameters are used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `clear ip nat translation protocol inside global-ip global-port local-ip local-port [outside local-ip global-ip]` | Clears some of the dynamic entries in the NAT table, depending on which parameters are used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |


# CHAPTER 13: CONTROL PLANE/LAYER PROTOCOLS

## Quality of Service (QoS)

Quality of Service (QoS) refers to tools that network devices can use to manage several related characteristics of what happens to a packet while it flows through a network. Specifically, these tools manage:
* **Bandwidth:** The capacity usage of the link.
* **Delay (Latency):** The time taken for one-way or round-trip transmission.
* **Jitter:** The variation in successive one-way delay/latency between packets in the same flow.
* **Loss:** The percentage of lost packets during transmission.

These tools balance the trade-offs of which types of traffic receive network resources and when, giving more preference to some traffic and less preference to others. QoS tools change the QoS characteristics of certain flows in the network, helping to control and avoid loss, often caused by device queues getting too full.

While QoS tools focus on managing bandwidth, delay, jitter, and loss, the user mainly cares about the quality of the overall experience. This is referred to as **Quality of Experience (QoE)**, which is a term referring to users’ perception of their use of the application on the network. QoS tools directly impact bandwidth, delay, jitter, and loss, which then should have some overall good effect to influence the users’ QoE. You can use QoS tools to create a better QoE for more important traffic.

### Per-Hop Behaviors (PHBs)

QoS tools define actions a device can apply to a packet between the time it enters the device until it exits the device. Such actions can delay, discard, or even change header fields. QoS defines these actions as **per-hop behaviors (PHBs)**, which is a formal term to refer to actions other than storing and forwarding a packet. The device can choose different PHBs for different kinds of messages, improving the QoS behavior for some messages while worsening the QoS behavior for others.

Common per-hop behaviors for QoS include:
* **Classification:** Identifying and categorizing different types of network traffic.
* **Marking:** Changing specific bits in packet headers to indicate their classification for subsequent QoS processing.
* **Queuing:** Managing buffers where packets wait to be transmitted, to prioritize certain traffic.
* **Policing:** Dropping or remarking packets that exceed a defined rate.
* **Shaping:** Buffering and delaying packets that exceed a defined rate to smooth out traffic bursts.

Overall, QoS refers to the tools that devices apply to provide differential treatment to packets as they traverse the network.

### Types of Traffic

Network traffic can be broadly categorized, each with different QoS requirements:

#### Data Applications
* **Interactive (e.g., Web Traffic):** Requires relatively low delay and jitter for a responsive user experience.
* **Non-Interactive (Batch Traffic):** This includes data backup or file transfers. Delay and jitter are less critical as the priority is for these applications to complete larger tasks within a longer time window, even if it means sending more data.

#### Voice and Video Applications
Both applications have similar breakdowns of Interactive & Non-Interactive "Flows." A flow is all the data moving from one application to another over the network, with one flow for each direction.

* **Voice over IP (VoIP):** Involves digitizing sound (e.g., 160 bytes with G.711 Codec for 20ms) and sending it in IP packets.
    * Though a single voice call or flow requires only a little bandwidth in comparison to data applications, Interactive Voice QoS requires a much better level of quality regarding delay, jitter, and loss: less delay, little or less jitter, and ideally no packet loss.
    * IP phones mark call signaling traffic (used to establish calls) as PCP 3. As soon as a session is established, they mark the actual voice traffic as PCP 5.
    * **Cisco's Enterprise QoS Solution Reference Network Design Guide suggests the following guidelines for Interactive Voice Applications:**
        * **Delay (one-way):** 150 ms or less
        * **Jitter:** 30 ms or less
        * **Loss:** 1% or less

* **Video Applications:** Similar to Voice but with much higher bandwidth requirements (per flow) and similar requirements for Delay, Jitter, and Loss.
    * **Bandwidth:** Video can use a variety of codecs that impact the amount of data sent. More technical features impacting bandwidth for a single video data flow are: Image Resolution (number of pixels) + Color Depth (RGB) + Frame Rate (FPS).
    * **End-to-End QoS Network Design Guide for Video Applications:**
        * **Bandwidth:** 384 kbps → 20+ Mbps
        * **Delay (one-way):** 200-400 ms
        * **Jitter:** 30-50 ms
        * **Loss:** 0.1% - 1%

### Classification

**"Classification"** refers to a type of QoS tool that identifies and categorizes packets based on their header contents. This is the first step in applying differential treatment to traffic.
To give priority to certain types of traffic, you have to identify which types of traffic to give priority to.

Methods of classification include:
* **Access Control List (ACL):** Traffic which is permitted by the ACL will be given certain treatment. ACLs can also serve the purpose of choosing which packets to discard by performing classification (matching of header fields) to decide which packets to take certain QoS actions against.
* **Network Based Application Recognition (NBAR):** Performs a deep packet inspection looking beyond Layer 3/4 up to Layer 7 to identify the specific kind of traffic. NBAR refers to this idea of defining the characteristics of different Applications as Application Signatures. NBAR looks for beyond what an ACL can examine in a packet; many applications can't be identified based on well-known ports alone. NBAR solves these problems and makes it easier to separate traffic into different classes.
* **PCP (Priority Code Point) field of the Ethernet - 802.1Q tag:** This field, also known as Class of Service (CoS), is a 3-bit field within the 3rd byte of the 4-byte 802.1Q header. It is only present when 802.1Q trunking is used on the link. As a result, QoS Tools can make use of the CoS field only for QoS features enabled on interfaces that are trunking.
* **DSCP (Differentiated Services Code Point) field of the IP Header:** Can be used to prioritize traffic.
* **TID header (exists in 802.11) over Wi-Fi**
* **EXP Header (MPLS label) over MPLS WAN**

### Marking

**Marking** is a crucial QoS tool that follows classification. After a packet is classified, it can be marked by changing some bits in specific header fields. This allows subsequent network devices to process the packet based on its marking, without needing to perform complex re-classification.

**Why Marking is Important:**
Applying complex matching of many header fields on every device and on most interfaces (both ingress and egress) requires extensive configuration and can degrade device performance. A better strategy, recommended by Cisco and RFCs, is to perform complex matching early in the packet's life (e.g., at the network edge) and then mark the packet. Devices downstream can then use simpler matching logic based on these marks.

**Marking Fields:**
* **IP DSCP (Differentiated Services Code Point):**
    * The IP Header exists for the entire trip of the packet across the IP network. Routers forward the IP packet, discarding the old data-link header and adding a new header. Because routers do not discard and reinsert IP headers, marking fields in the IP header stay with the data from the first place it is marked until it reaches its destination.
    * IPv4 defines a **Type of Service (ToS)** byte in its header. The original RFC defined a 3-bit **IP Precedence (IPP)** field for QoS marking. The remaining 5 bits of the ToS byte were unused.
    * Later RFCs redefined the ToS byte with the **DSCP** field, which increased the number of marking bits from 3 (giving 8 possible values) to 6 bits (giving $2^6 = 64$ possible values) that can be marked.
    * IPP and DSCP fields can be referenced by their decimal values as well as some convenient names.
    * IPv6 defines a **TRAFFIC CLASS Byte**, which serves a similar purpose.

* **Ethernet CoS (Class of Service) / PCP (Priority Code Point):**
    * This field is located in the 3rd byte of the 4-byte 802.1Q header, as a 3-bit field (3 possible values).
    * However, the 802.1Q header isn't included in all Ethernet frames; it exists only when 802.1Q trunking is used on the link. As a result, QoS Tools can make use of the CoS field only for QoS features enabled on interfaces that are trunking.

If the markings are trusted, the device will forward the packet without changing the markings, or they will change the markings according to the configured policy.

### Trust Boundary

The **Trust boundary** refers to the point in the path of a packet flowing through a network at which the Network Engineer creating a QoS plan has to choose where to place the trust boundary for a network. That boundary typically sits on a device under the control of the IT staff.

At the trust boundary, the network devices decide whether to "trust" the QoS markings applied by an upstream device or end-host. If the markings are trusted, the network will honor those markings and apply the corresponding QoS policies. If not trusted, the network device might re-mark the packets or ignore the existing markings and apply its own classification.

For example, IP phones can typically be a trust boundary, instead of an Access layer switch. IP phones can set the CoS and DSCP fields of the packets created by the phone, as well as those forwarded from the PC through the phone. By trusting the markings from an IP phone, the network can ensure that voice and video traffic originating from or passing through the phone receives the appropriate QoS treatment from the moment it enters the network.

### DiffServ Suggested Marking Values

DiffServ (Differentiated Services) aims to create a consistent usage of DSCP (Differentiated Services Code Point) values across networks to enable product vendors to provide good default settings for their QoS features.

| Marking Value         | DSCP (Decimal) | Description                                                                                                                                                                                                                               |
| :-------------------- | :------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Default Forwarding (DF)** | 0              | Represents best-effort traffic. Packets are forwarded without any special QoS treatment.                                                                                                                                                  |
| **Expedited Forwarding (EF)** (RFC 3246) | 46             | Designated for traffic requiring low latency, low jitter, and low loss. Primarily used for voice payload. Cisco IP phones, by default, mark voice payload at EF. Voice signaling packets (messages to set up a call) are typically marked as CS3. |
| **Assured Forwarding (AF)** (RFC 2597) | Varies           | Defines a set of 12 DSCP values used in concert. AF categorizes traffic into four separate queues and three levels of drop priority within each queue, for use with congestion avoidance algorithms. This requires 12 different DSCP markings (one for each combination of queue and drop priority). |
| **Class Selector (CS)** | Varies           | Recreates eight DSCP values for backward compatibility with IP Precedence (IPP) values (a 3-bit field with 8 possible values).                                                                                                              |

**The DSCP to IPP (Class Selector) and AF Mapping:**

| IPP | CS  | DSCP | Drop Precedence (within a given AF queue) |
| :-- | :-- | :--- | :---------------------------------------- |
| 0   | CS0 | 0    | Best Effort - DF                          |
| 1   | CS1 | 8    | AF11 (10), AF12 (12), AF13 (14) - Worst Queue (Higher Drop Precedence) |
| 2   | CS2 | 16   | AF21 (18), AF22 (20), AF23 (22)           |
| 3   | CS3 | 24   | AF31 (26), AF32 (28), AF33 (30)           |
| 4   | CS4 | 32   | AF41 (34), AF42 (36), AF43 (38) - Best Queue (Lower Drop Precedence) |
| 5   | CS5 | 40   | (38, 40, 42) - Note: These DSCP values are often used for control plane traffic or network management. |
| 6   | CS6 | 48   | (48, 50, 52) - Note: Often used for network control traffic. |
| 7   | CS7 | 56   | (56, 58, 60) - Note: Often used for network control traffic. |

* **Worst DROP (Highest drop precedence)** $\leftrightarrow$ **Best DROP**
* **Best Queue** $\leftrightarrow$ **Worst Queue**

**Cisco QoS Design Guides (based on RFC 4954 conventions):**
Cisco has adopted and extended RFC 4954, defining default marking conventions for various traffic types:

* **DSCP EF (46):** Voice payload
* **AF41 (34), AF42 (36):** Interactive Video
* **AF31 (26), AF32 (28):** Streaming Video (non-Interactive)
* **AF21 (18), AF22 (20):** High Priority (low latency) data
* **CS0 (0):** Standard Data

### Queuing and Congestion Avoidance

**Queuing** refers to the QoS tools for managing the queues that hold packets while they wait their turn to exit an interface.

Most networking devices can have a queuing system with **Multiple Queues**. To use multiple Queues, the queuing system needs:
* A **classifier function** to choose which packets are placed into which queue.
* A **Scheduler** to decide which packet to take next when the interface becomes available. The scheduler performs **prioritization** – the concept of giving priority to one queue.

**Packet Flow with QoS:**
INGRESS $\rightarrow$ Classifier $\rightarrow$ Marking $\rightarrow$ QUEUES $\rightarrow$ Scheduler $\rightarrow$ Prioritization Algorithm $\rightarrow$ Shaping $\rightarrow$ Policing $\rightarrow$ Egress

#### Prioritization

* **Round-Robin scheduling:** Cycles through the queues in order, taking turns with each queue.
* **Weighted Round-Robin:** In each cycle, the Scheduler either takes one packet or takes a number of bytes from each queue by taking enough packet bytes to reach that number of bytes. Also included in the concept of "Weighting" - the Scheduler takes a different number of packets (bytes) from each queue, giving more preference to one queue over another. Routers use a tool called **Class-Based Weighted Fair Queuing (CBWFQ)**.
    * **CBWFQ (Class-Based Weighted Fair Queuing):** Each class receives at least a guaranteed amount of bandwidth during times of congestion but potentially more. Internally, CBWFQ uses a Weighted Round-Robin Scheduling algorithm, while letting the network admin define the weightings as a fixed link bandwidth percent.
    * Unfortunately, a Round Robin Scheduler doesn't provide low enough delay, jitter, or loss for Video.

* **Low Latency Queuing (LLQ):**
    * The solution to the limitations of Round-Robin for real-time traffic is to add **Low Latency Queuing (LLQ)** to the Scheduler. A round-robin queuing system might add too much delay for Video/Voice packets because of the shuffling or cycling to pick packets from other queues.
    * LLQ tells the scheduler to treat one or more queues as **PRIORITY Queues**. The LLQ Scheduler always takes the next packet or bytes during times of congestion from one of these special priority queues.
    * As such, the LLQ might never have time to fill up, guaranteeing low delay, jitter, or loss to packets executing in LLQ / priority queues.
    * Unfortunately, using LLQ might also lead to a problem of **"Queue Starvation"** for other traffic.

* **Call Admission Control (CAC):**
    * The ultimate solution to prevent loss for voice and video traffic in conjunction with LLQ and policing is to find a way to limit the amount of Voice & Video traffic that the network routes out through the link (Interface) *before* it gets to the policer, so that the policer never discards any traffic.
    * CAC tools are implemented at the network point where calls or sessions are initiated. They assess network resources (e.g., available bandwidth) before allowing a new voice or video call to be established. If resources are insufficient to maintain the required QoS for the new call and existing calls, CAC might prevent the call from being set up, thus avoiding a poor user experience from the outset due to congestion and subsequent packet loss.

* **Round Robin:** Not good for Voice & Video data traffic; typically applied to Best-Effort / less critical traffic Queues.

### Shaping and Policing (mostly at WAN Edge)

**Shaping and Policing** are two QoS tools often used on opposite ends of a link. Both tools manage bandwidth, delay, jitter, and loss by monitoring the bitrate of combined messages that flow through a device. Once enabled, a policer or shaper notes each packet that passes and measures the number of bits per second. Both attempt to keep the bitrate at or below the configured bandwidth, but by using different actions:

* **Policers discard packets.**
* **Shapers hold packets in queues to delay the packets.**

#### Policing

* Policers allow for a burst beyond the policing rate for a short time, after a period of low traffic activity. Such peaks in network traffic are allowed for the nature of bursty data applications.
* It measures the traffic rate over time for comparison to the configured policing rate.
* It allows for a burst of data after a period of inactivity.
* It is enabled on an interface, in either direction, but typically at **ingress (incoming packets)**.
* It can discard excess messages but can also remark the message so that it's a candidate for more aggressive discard later in its journey (i.e., re-classify packet into Higher Drop precedence for QoS).
* **Question Example:** You have a 1 Gbps link from a Router into an SP, but with 200-Mbps CIR for traffic to another site. The SP (Service Provider) has told you that it discards incoming traffic exceeding the CIR. To resolve this **from the perspective of the SP discarding your traffic**, you would use a traffic **Shaper** on your router's egress interface to send traffic at or below the CIR. (Note: The prompt incorrectly suggests policing to resolve this, but policing discards *your* traffic, while shaping prevents the *SP* from discarding it by sending it at the agreed rate.)

#### Shaping

* Shapers slow messages down by queuing the messages. The shaper then services the shaping queues but not based on when an interface becomes available. Rather, it schedules messages from the Shaping queues based on the Shaping Rate. The shaper queues packets so that the sending rate over time doesn't exceed the shaping rate, thus avoiding congestion on the output.
* Because shapers create queues where messages wait, a Queuing tool should be applied to those queues (e.g., Round-Robin Scheduler, Priority Queuing features of CBWFQ & LLQ respectively).
* The unfortunate side effect of a shaper is that it slows down packets, leading to more delay & jitter.
* Thankfully, we can configure a shaper's setting that changes its internal operation: **A Shaper's Time Interval** refers to its internal logic for how a shaper averages, over time, sending at a particular rate. Basically, it sends as fast as it can & then waits; sends & waits; sends & waits.
* **Example:** Shaping @ 200 Mbps on a Router that has a 1000-Mbps (1 Gbps) Outgoing Interface. In that case, the shaper would result in the interface sending data 20% of the time, being silent for 80% of the time.
* When shaping, ensure to use a short time interval. By recommendation, use a 10-ms time interval to support voice and video. With such a setting, a voice/video packet should wait no more than 10ms while waiting for the next shaping interval, at which point the priority queue scheduling algorithm should take all the voice and video traffic out.
* Shapers measure the traffic rate over time for comparison to the configured shaping rate.
* Shapers allow for bursting after a period of inactivity.
* Shapers are enabled on an interface for **egress (outgoing packets)**.
* Shapers slow down packets by queuing them and over time releasing them from the queue at the shaping rate.
* Shapers use queuing tools to create and schedule the shaping queues, which is very important for the same reasons discussed for output queuing.

### Congestion Avoidance

**Congestion Avoidance** attempts to reduce overall packet loss in TCP connections via a mechanism of flow control called **Windowing**. Each TCP receiver grants a Window to the Sender. The window is a field in the TCP header that defines the number of bytes the sender can send over the TCP connection before receiving a TCP ACK for at least some of those bytes. The window size is the number of unacknowledged bytes that the sender can send before the sender must simply stop and wait.

* Each ACK TCP Segment doubles (2x) the window size.
* TCP Segment loss leads to a one-half Window Size Shrink.
* With multiple segment losses, the window size shrinks by half multiple times, slowing down the sender's rate significantly.

Without Congestion Avoidance, an event called **Tail Drop** causes the most drops in the network, which arises from **TCP Global Window Size Synchronization**.
* **Tail Drop:** If a queue is full, new packets are dropped.
* This leads to **Global TCP Window Size Decrease** (all TCP flows simultaneously slow down), followed by **Network Under-Utilization**, then a **Global TCP Window Size Increase** (all TCP flows try to double their window size), leading to **Congestion** again. This creates a "sawtooth" pattern of network utilization.

Congestion Avoidance discards some TCP Segments *before* Queues fill, hoping that enough TCP connections will slow down, reducing Congestion and avoiding a much worse problem: the effects of queue overflow which leads to Tail-Drop (harmful because it leads to TCP Global Synchronization). To resolve this, we use Congestion avoidance.

* A solution to prevent Tail Drop & TCP Global Sync is **Random Early Detection (RED)**. When the amount of traffic on the Queue reaches a certain threshold, the device will start randomly dropping packets from select TCP flows. Those TCP flows that have dropped packets will reduce the rate at which traffic is sent, but this will avoid TCP Global Sync, in which all TCP flows reduce their rate of transmission at the same time in waves.
* In standard RED, all kinds of traffic are treated the same. An improved version, **Weighted RED**, allows you to control which packets are dropped depending on the traffic class.

### The Iterative Nature of QoS Design

The journey to deliver a seamless experience for real-time applications like voice and video is a fascinating progression of problem-solving:

1.  **Problem 1: Round-Robin is Bad for Voice & Video Traffic due to its cyclic nature of picking traffic bytes from Queues.**
    * The inherent fairness of round-robin means that delay-sensitive traffic has to wait its turn behind less sensitive traffic, leading to unacceptable jitter and latency for voice and video.

2.  **Solution to Problem 1: This led to the creation of Special Queues to give priority to Low Latency Queues (LLQ).**
    * This is the direct solution to the round-robin problem for real-time traffic. LLQ's strict priority mechanism ensures these packets get out first.

3.  **Problem 2: Which then led to yet another problem of Queue Starvation for normal data traffic.**
    * If LLQ can consume all available bandwidth, other queues might never get a chance to transmit, leading to starvation for best-effort traffic.

4.  **Solution to Problem 2: To resolve this we introduced the concept of Policers which limit the amount of bandwidth placed into the LLQueues.**
    * Policing is the common mechanism to cap the bandwidth that priority traffic can consume, thus protecting other queues from starvation.

5.  **Problem 3: But this meant that excess traffic beyond the limit of the LLQueues Bandwidth were being discarded leading to tremendous LOSS.**
    * Unlike shaping (which buffers), policing for LLQ's primary goal of low latency means excess traffic must be dropped, as buffering would introduce the very delay LLQ is designed to avoid. This is indeed a source of potential loss.

6.  **Solution to Problem 3: Further resolved with other QoS tools $\rightarrow$ Call Admission Control (CAC).**
    * CAC is the logical next step to prevent excessive voice/video traffic from even entering the network segment where it might face policing drops. It is a preventative measure.

**The "Why" behind Policing vs. Shaping for LLQ:**
* **Policing (Drop):** For LLQ, the goal is always minimal delay. If traffic exceeds the allocated bandwidth, buffering it (like a shaper) would defeat the low-latency purpose. Therefore, policing's action of dropping excess is preferred.
* **Shaping (Buffer):** While you could technically apply shaping to an LLQ, it's counter-intuitive to its primary purpose. Shaping introduces delay by buffering. It's used when you want to smooth out a bursty flow, typically for non-real-time traffic, or when an ISP has a CIR and you want to prevent drops by them.

**The Role of CAC in the Overall QoS Strategy:**
* **Preventative vs. Reactive:** Policing is reactive (drops traffic once it's already in the queue and exceeding limits). CAC is preventative (prevents calls/sessions from being established if the network can't guarantee QoS for them). This is a crucial distinction.
* **User Experience:** CAC directly impacts the user experience by either allowing a call with guaranteed quality or rejecting it, rather than allowing a call to start and then suffer poor quality due to congestion and drops. It manages expectations and resource utilization at the entry point.
* **Applications:** CAC is typically associated with voice and video systems (e.g., Cisco Unified Communications Manager, IP PBXs) that integrate with network QoS policies.


# CHAPTER 14: NETWORK DEVICE SECURITY

## PORT SECURITY

Port security allows you to control which source MAC address(es) are allowed to enter a switchport. If an unauthorized source MAC address enters a port, an action will be taken. The default action is ERR-Disabled.

When enabled, port security on an interface with the default settings allows one MAC address. You can manually configure the allowed MAC address or change the maximum number of MAC addresses allowed. A combination of statically configured and dynamically learned MAC addresses is possible.

Port security is useful because it allows network administrators to control which devices are allowed to access the network. By default, the switch will allow the first MAC address that enters the switchport interface. However, the network can be compromised with MAC address spoofing, which is why port security allows you to limit the MAC addresses allowed on each switchport. This can protect against attacks like spoofing and Man-in-the-Middle (MITM).

The default state for Cisco switchports is `[Administrative mode: dynamic auto]`.

**Important Considerations for Port Security:**
* Port security can be enabled on access/trunk ports, but they **must be statically configured** as access/trunk.
    * `Switchport mode access` (✓)
    * `Switchport mode trunk` (✓)
    * `Switchport mode dynamic desirable` (X)
    * `Switchport mode dynamic auto` (X)

**Configuration and Verification Commands:**
* `switchport port-security`: Enables port-security on the selected interface.
* `show port-security interface [interface_id]`: Displays port-security status of an interface.
    * The default violation mode is `shutdown`. If an unauthorized frame enters the interface, it will be `ERR-Disabled`.
    * Aging Timer of 0 minutes means the addresses will never age out.
    * Aging Type: `Absolute` > If a default Aging Timer is configured manually on inactivity.
    * Output also includes: `Max MAC Addr`, `Total MAC Addr`, `Configured Max Addr`, `Sticky MAC Addr`, `Latest Source Addr`, `Security Violation Counter`, and `Violation Mode`.
    * The port status from `show port-security` command is `secure-shutdown`. From `show interface status`, it is `ERR-Disabled`.

**To Recover from the ERR-Disabled State:**
1.  Disconnect the unauthorized device; otherwise, it becomes the new secure MAC address on the interface.
2.  `shutdown` and then `no shutdown` the interface.
3.  Another less common way to recover is to use the `errdisable recovery` command.
    * `show errdisable recovery`: Displays an output of all possible reasons an interface will be in an ERR-Disabled state (e.g., `arp-inspection`, `bpduguard`, `dtp-flap`, `Port Security`, `storm-control`, `unicast flood`, `stp-config mismatch`, etc.).
    * `Errdisable Recovery Interval 180` (Default Time Out Interval: 300 seconds / 5 minutes). Every 5 minutes (by default timeout interval), all ERR-Disabled interfaces will be re-enabled if `errdisable recovery` has been enabled for the cause of the interface's disablement.
    * `errdisable recovery cause "Err Disable Reason"`: Manual recovery using re-enablement on the interface.

**Secure MAC Addresses:**
* Dynamically learned secure MAC addresses will have a type of `DYNAMIC`.
* Sticky static secure MAC addresses will have a type of `STATIC`.
* `show mac-address-table secure`: Displays output of all secure MAC addresses.

### Port Security Violation Modes

There are 3 different violation modes that determine what the switch will do if an unauthorized frame enters an interface configured with port-security:

1.  **Shutdown (Default):**
    * Effectively shuts down the port by placing it in an `ERR-Disabled` state.
    * The violation counter is set to 1 when the interface is disabled.
    * Generates syslog/SNMP messages.
2.  **Restrict:**
    * The switch discards traffic from unauthorized MAC addresses, but the port is not disabled.
    * The violation counter is incremented by 1 for each unauthorized frame.
    * Generates a syslog/SNMP message each time an unauthorized frame from a MAC is detected.
3.  **Protect:**
    * The switch discards traffic from unauthorized frames.
    * The interface is not disabled.
    * It **doesn't** increment the counter, neither does it generate syslog/SNMP messages for unauthorized traffic.

### Port Security Configuration Commands

* `switchport port-security maximum "decimal"`: Configures the acceptable maximum number of learned MAC addresses.
* `switchport port-security violation {restrict | protect | shutdown}`: Command to configure the violation mode.
* `switchport port-security mac-address 0000.0000.000c`: Statically configures a secure MAC address.

**Secure MAC Address Aging:**
MAC addresses dynamically learned or statically configured on a port-security enabled port are called Secure MAC Addresses. By default, secure MAC addresses will not age out (Aging Time: 0 minutes). However, you can configure this timer:
* `switchport port-security aging time "minutes"`
* **Aging Types:**
    * **Absolute Aging:** After a secure MAC address is learned, the aging timer starts, and the MAC address is removed after the timer expires, even if the switch continues receiving frames from that source. However, after the MAC address ages out, it can then immediately be re-learned if another frame with that source MAC address is received.
    * **Inactivity Aging:** After a secure MAC address is learned, the aging timer starts but is reset every time a frame from that source MAC address is received on the interface. Therefore, as long as the switchport keeps receiving frames from that MAC address, it will never age out.
    * `switchport port-security aging type {absolute | inactivity}`
* Secure static MAC Aging (addresses configured with `switchport port-security mac-address`) is disabled by default; it can be enabled with `switchport port-security aging static`. The address would be removed from the MAC address table if it ages out.

**Sticky Secure MAC Address Learning:**
* `switchport port-security mac-address sticky`: When enabled on an interface, dynamically learned secure MAC addresses will be added to the running configuration like this: `switchport port-security mac-address sticky 0009.000b.000c`. These are considered both dynamic and static.
* The 'Sticky' secure MAC addresses will never age out; you will need to save the running-config to the startup-config (`copy run start`) to make them truly permanent (else they will not be kept if the switch reboots).

## DHCP SNOOPING

DHCP Snooping is a security feature of switches used to filter DHCP messages received on **Untrusted** ports. DHCP Snooping only filters DHCP messages; non-DHCP messages are not affected. All ports are untrusted by default.

### Uplink vs. Downlink — Why Trust Matters in DHCP Snooping

In DHCP snooping, we manually define which ports are “trusted”.
* **Uplink Ports = Trusted:** These are ports that connect to known infrastructure—typically:
    * Your authorized DHCP server.
    * Core switch/router that relays DHCP messages (via DHCP relay/Helper Address).
    * These ports are trusted to send server-side DHCP messages (e.g., `DHCPOFFER`, `DHCPACK`, `DHCPNAK`).
* **Downlink Ports = Untrusted:** These are ports that connect to end devices or access layer hosts (e.g., laptops, printers).
    * Clients should only send Discover/Request messages—not server replies.
    * If an untrusted client port sends server messages, it’s likely a rogue DHCP server, so DHCP snooping will block/drop those messages.

### DHCP Message Filtering Logic

DHCP Snooping filters messages by differentiating between DHCP Server Messages and DHCP Client Messages. With DHCP snooping enabled, any DHCP message received on an untrusted port is inspected and possibly discarded.

1.  **Check if it’s a DHCP server message (e.g., `DHCPOFFER`, `DHCPACK`, `DHCPNAK`):**
    * **Action:** Discard it.
    * **Why?** Only trusted ports (typically uplinks toward legitimate DHCP servers) should be allowed to send server responses. Discarding such messages prevents rogue DHCP servers from assigning IPs, redirecting traffic, or performing MITM (man-in-the-middle) attacks. This is part of DHCP spoofing/MITM poisoning prevention.

2.  **Check if it’s a DHCP client message (e.g., `DHCPDISCOVER`, `DHCPREQUEST`, `DHCPDECLINE`, `DHCPRELEASE`) is received, DHCP snooping performs the following validations:**
    * **For `DISCOVER` or `REQUEST` messages:**
        * **Check:** Verify that the frame's Source MAC Address and DHCP message CHADDR fields match.
        * **Action:** MATCH - Forward; MISMATCH - Discard.
        * **Why?** Prevents an attacker from spoofing MAC addresses or using multiple fake clients to exhaust the DHCP pool (a form of DoS attack/DHCP starvation attack). This check is not entirely perfect as an attacker can temporarily spoof the client Hardware Address (CHADDR) field.
    * **For `RELEASE` or `DECLINE` messages:**
        * **Check:** Verify if the frame's Source IP address matches the IP in the DHCP binding table entry.
        * **Action:** MATCH - Forward; MISMATCH - Discard.
        * **Why?** Prevents clients from releasing/declining IPs they don’t own, which could disrupt other users or mess with address management.

### DHCP Snooping Binding Table

A **DHCP Snooping binding table** is created when a client successfully leases an IP address from a DHCP server. This is a dynamically built list of:
* MAC address
* IP address
* VLAN
* Interface
* Lease time

This table is critical for verifying legitimate client behavior and for integration with features like IP Source Guard and Dynamic ARP Inspection (DAI).

### DHCP Message Types and Broadcast/Unicast Behavior

* **`DISCOVERY`** (Client $\rightarrow$ Server): Always Broadcast.
    * Reason: The client does not yet have an IP address, so it sends to the broadcast IP 255.255.255.255 to reach any available DHCP server.
* **`OFFER`** (Server $\rightarrow$ Client): Usually Broadcast (can be unicast under specific conditions).
    * Reason: The client may not yet have a usable IP, so the server broadcasts the offer so the client can receive it even without a configured IP stack. However, if the server knows the client’s MAC address and the network allows it, it can unicast the offer directly to the client.
* **`REQUEST`** (Client $\rightarrow$ Server): Broadcast (`ff:ff:ff:ff:ff:ff`, 255.255.255.255 from client, though a DHCP server identifier field is filled in the DHCP packet).
    * Reason: The client still doesn’t have a valid IP and is notifying all DHCP servers of the chosen offer, so it uses broadcast again.
* **`ACKNOWLEDGEMENT`** (Server $\rightarrow$ Client): Either Broadcast or Unicast.
    * Broadcast if it’s a new lease and the client has no IP yet.
    * Unicast if the client already has an IP and is renewing the lease (typically during the T1 or T2 timer stages). The client includes its current IP and can receive unicast packets now.
* **`NAK` (Negative Acknowledgment):** Opposite of Acknowledgment, used to decline a client's request.
* **`RELEASE`:** Used to tell the server that the client no longer requires its IP address.
* **`DECLINE`:** Used to decline the IP address offered by the DHCP server.

### DHCP Snooping Configuration Commands

**DHCP Snooping Configuration Scope:** DHCP snooping is enabled per VLAN because:
* Each VLAN can represent a separate broadcast domain and may have its own DHCP configuration.
* The command `ip dhcp snooping vlan <vlan-id>` ensures that DHCP snooping inspects traffic only within that VLAN, not globally.
* You must explicitly trust interfaces (e.g., uplinks).

* `ip dhcp snooping`: Enables DHCP snooping globally.
* `ip dhcp snooping vlan [vlan_id]`: Enables it on each VLAN (VLANs are segmented groups of switchport interfaces).
* `interface [interface_id]` followed by `ip dhcp snooping trust`: Configures the selected interface as a trusted port. By default, all ports are untrusted. (Usually, the interface represents uplink ports.)
* **Note:** DHCP snooping does not block static IP assignments by default. If a rogue client uses a static IP, that may bypass some controls unless you pair DHCP snooping with IP Source Guard. Always remember to enable DHCP snooping globally before enabling it on VLANs.

**Rate Limiting DHCP Messages:**
* Rate limiting DHCP messages on untrusted ports helps mitigate DHCP exhaustion attacks where a malicious user floods the switch with fake `DHCPDISCOVER` messages. This limits the allowed number of DHCP messages per second, which is plenty for normal clients but restricts spamming attempts.
* `ip dhcp snooping limit rate "decimal"`: Prevents against DHCP Exhaustion Attack. DHCP Snooping rate limiting is disabled on all interfaces by default.
* `show ip dhcp snooping binding`: Displays the binding table - created after there's a DHCP entry.

**Error-Disabled State from DHCP Snooping Rate Limiting:**
DHCP Snooping can limit the rate at which DHCP messages are allowed to enter a switchport interface. If the rate of DHCP messages crosses the configured limit, the interface is `ERR-Disabled`. Like port security, the interface can be manually re-enabled or automatically recovered with `ERRDisable Recovery`.
* Automatically, if `errdisable recovery` is enabled for the specific reason: `errdisable recovery cause dhcp-rate-limit`.
* To recover from the `ERR-Disabled` state manually: `shutdown` and then `no shutdown`.

## DYNAMIC ARP INSPECTION (DAI)

**Address Resolution Protocol (ARP)** is used to learn the MAC Address of another device with a known IP Address. For example, a PC will use ARP to learn the MAC address of its Default Gateway to communicate with external networks. ARP uses 2 messages: Request & Reply.
A **Gratuitous ARP (G.ARP)** message is an ARP Reply that's sent without receiving any ARP Request. It allows other devices to learn the MAC address of the sending host without having to send ARP Requests. Some devices auto-send G.ARP messages when an interface is enabled, IP/MAC address is changed, etc.

**DAI (Dynamic ARP Inspection)** is a security feature of switches that is used to filter ARP messages received on **untrusted ports**. DAI doesn't inspect messages received on trusted ports; these ARP messages are forwarded normally. DAI only filters ARP messages; non-ARP messages aren't inspected or affected.

All ports are untrusted by default. Typically, all ports connected to other network devices (switches/routers) should be configured as **TRUSTED**, while interfaces connected to End Hosts should remain **UNTRUSTED**.

Similar to DHCP poisoning, **ARP poisoning** involves an attacker manipulating a target's ARP tables so traffic is sent to the attacker. To do this, the attacker can send Gratuitous ARP Replies using a spoofed device's IP address. This leads to other devices in the network receiving the G.ARP and updating their ARP tables, causing them to send traffic to the attacker instead of the target destination.

DAI prevents against such ARP poisoning attacks by inspecting the Sender/Source MAC & IP address fields of ARP messages received on untrusted ports and checks that there is a matching entry in the DHCP Snooping Binding Table. If there is a matching entry, the ARP message is forwarded; no matching entry means it is discarded.

DAI operations are usually reliant on DHCP snooping for its binding table feature to check entries. Another option is to use **ARP ACLs**, which can be manually configured to map IP Addresses to MAC Addresses for DAI to check entries. This is useful for hosts that don't use the DHCP Snooping security feature.

### What Are ARP ACLs?

ARP ACLs match Layer 2 information: IP and MAC address pairs. They're used only by features like Dynamic ARP Inspection (DAI). Unlike Layer 3 ACLs (which match IP, ports, protocols), ARP ACLs are not used to filter routed traffic. ARP ACLs are a must for non-DHCP-bound static IP clients.

**ARP ACL Configuration Example:**
```
arp access-list DAI_LIST
  permit ip host 192.168.1.10 mac host aabb.ccdd.eeff
  deny ip any mac any
interface FastEthernet0/1
  ip arp inspection filter DAI_LIST vlan 10
```

### Why ARP ACLs Are Bound to VLANs

DAI operates at Layer 2, and VLANs define Layer 2 broadcast domains. Since ARP requests and replies are broadcast-based protocols, they only matter within the VLAN (the broadcast domain). That’s why:
* DAI is enabled per VLAN, not per interface.
* ARP ACLs are applied to VLANs, ensuring only valid ARP traffic is allowed within that VLAN.
* In real networks: ARP ACLs are only used when DHCP snooping isn't an option. Most environments rely on DHCP Snooping to build dynamic IP-MAC bindings for DAI. ARP ACLs are typically used for static IP devices (e.g., servers, printers) that don’t get IPs via DHCP.

#### DAI Configuration Commands

* `ip arp inspection vlan [vlan_id]`: Enables DAI on a VLAN/on each VLAN in case of multiple VLANs.
* `interface [interface_id]` or `interface range [interface_range]` followed by `ip arp inspection trust`: Manually configures a port as trusted.
* `show ip arp inspection interfaces`: Displays an output of interfaces and their trust state with rate.
* `ip arp inspection limit rate X burst interval Y`: Configures rate limiting at X packets in Y seconds.

**DAI Rate Limiting:**
Like DHCP Snooping, Dynamic ARP Inspection also supports Rate-limiting to prevent attackers from overwhelming the switches with ARP message frames. Even if the attacker's messages are blocked, they can overload the switch's CPU with ARP messages.
* DAI Rate limiting is enabled on UNTRUSTED ports by default with a rate of 15 packets per second. It is disabled on trusted ports by default.
* DHCP Snooping Rate Limiting is configured as 'x packets per second'. DAI Burst Interval allows you to configure it this way $\rightarrow$ ‘X packets per Y seconds' for flexibility.

**Additional Validation Checks for DAI:**
The command `ip arp inspection validate {src-mac | dst-mac | ip}` is used in Dynamic ARP Inspection (DAI) to configure additional validation checks on ARP packets received on untrusted ports. While DAI's primary function is to compare ARP packets against the DHCP snooping binding table or static ARP ACLs, these validate options add more granular integrity checks to prevent specific types of ARP spoofing attacks.
You can combine these options in a single command, for example: `ip arp inspection validate src-mac dst-mac ip`

**Error-Disabled State from DAI Rate Limiting:**
If ARP messages are received faster than the specified rate, the switchport interface will be `ERR-Disabled`.
* Automatically, if `errdisable recovery` is enabled for the specific reason: `errdisable recovery cause arp-inspection`.
* To recover from the `ERR-Disabled` state manually: `shutdown` and then `no shutdown`.


# CHAPTER 15: ARCHITECTURE, DESIGN, TOPOLOGY

## Network Architecture

### LAN Architectures & Campus LAN Design

Network topologies describe the arrangement of elements (links, nodes, etc.) of a communication network. Common topologies include Mesh, Partial Mesh, Hybrid Mesh, and Star Topology.

#### 1. The Two-Tier LAN Design

The Two-Tier LAN Design consists of 2 hierarchical layers:
* **Access Layer:** This is the layer that end hosts connect to. Access Layer Switches typically have many ports. QoS marking is typically done here (early stage in a packet's life), and security services like Port Security, DAI (Dynamic ARP Inspection), and DHCP snooping are implemented. Switchports might be PoE-enabled for wireless APs, IP phones, etc.
* **Distribution Layer:** This layer aggregates connections from the Access Layer, providing fault-tolerant interconnections between different Access Blocks. It's typically placed at the border between Layer 2 and Layer 3 (routing). Distribution Layer switches implement traffic policies, routing boundaries, filtering, and QoS. They connect to services like WAN and the Internet. In a collapsed core design, the Distribution Layer is sometimes called the Core-Distribution Layer. Connections between Distribution Layer 3 switches are Layer 3. Routing information can be shared via OSPF, for example.

This design is also known as a **collapsed core design** because it omits a layer found in the Three-Tier Design.

**Topology within a Two-Tier Design:**
* At the Access Layer, many devices connect to Access Switches in a **Star Topology** (with DAI, Port Security, DHCP snooping implemented).
* At the intersection between the Access Layer and the Distribution Layer, we typically have a **Partial Mesh Topology** (leveraging STP and HSRP for redundancy).
* Between the Distribution Layer 3 Switches (if multiple), a **Full Mesh Topology** might be used for redundancy and load balancing.
* All together, this forms a **Hybrid Topology**.

In larger networks with many Distribution Layer switches (e.g., separate building facilities in a campus or a research lab), the number of mesh connections required between Distribution L3 Switches grows rapidly, leading to scalability complications. Cisco recommends adding a Core Layer if there are more than 3 Distribution Layers in a single location. Each Distribution Layer switch then connects to a Core Layer, eliminating the need for full mesh interconnection between them.

#### 2. Three-Tier LAN Design

The Three-Tier LAN Design consists of 3 hierarchical layers: Access, Distribution/Aggregation, and Core.
* **Core Layer:** This layer connects Distribution Layers together in large LAN networks. The focus is speed and fast transport. CPU-intensive operations such as security, QoS classification, and marking should be avoided at this layer. Connections are all Layer 3; therefore, there's no use for Spanning Tree Protocol. The Core Layer should maintain connectivity throughout the LAN even if devices fail. They connect to the Internet/Edge Router/Top Router used in traditional on-premises data centers (often using LACP, PAgP for link aggregation). This is also referred to as **North-South traffic**.

#### 3. Spine & Leaf Architecture

The Spine & Leaf Architecture is an advanced Two-Tier Design that provides better support for SDN Overlay Networks. Traditional data center designs used the Three-Tier Design, but it worked well when most traffic was North-South (traffic going in or out of the data center) and didn't function well for **East-West Traffic** (traffic between servers in the same part of the network).

With the precedence of virtual servers, applications are often deployed in a distributed manner, which increases the amount of East-West traffic in a data center. The traditional Three-Tier designs led to bottlenecks in bandwidth as well as variability in server-to-server latency depending on the path the traffic takes. To resolve this, Spine-Leaf Architecture has become prominent in data centers.

**Key characteristics of Spine & Leaf Architecture:**
* Every Leaf switch is connected to every Spine Switch.
* Every Spine Switch is connected to every Leaf Switch.
* Leaf switches do not connect to other Leaf switches.
* Spine switches do not connect to other Spine switches.
* End hosts only connect to Leaf switches.

The path taken by traffic is chosen randomly to balance the load, and each end host is separated by the same number of hops, providing consistent latency.

### WAN Architecture Design

To extend networks over a large geographical area, we use WANs (Wide Area Networks). Although internal traffic can be considered WAN, the term WAN is typically used to refer to an enterprise's private connections that link their offices, data centers, and other sites together. Over a public or shared network like the Internet, VPNs (Virtual Private Networks) can be used to create private connections between multiple LANs to a centralized WAN in a star topology style known as **Hub and Spoke Architecture**.

Each LAN can be connected to the WAN data center via a Telco/Comms/Leased Line in a Star Topology. This is similar to how on-premise data centers/LANs connect to a Cloud Provider WAN, like ExpressRoute or Direct Connect.

#### 1. Leased Line

A Leased Line is a dedicated physical link, typically connecting 2 sites, or multiple sites to a central hub. There are various standards that provide different speeds, and different standards are available in different countries.
Leased lines use Serial Connections (Point-to-Point Protocol and High-Level Data Link Control - HDLC) Encapsulation. Due to the higher cost, higher installation lead time, and slower speeds of leased lines, Ethernet WAN technologies are becoming more popular. A leased line is dedicated, so there is no need for MPLS labels.

#### 2. Multiprotocol Label Switching (MPLS) Circuits

MPLS networks are shared infrastructure because many customers/enterprises connect to and share the same infrastructure to make WAN Connections. The Label Switching in the term MPLS allows VPNs to be created over the MPLS infrastructure through the use of **LABELS**. Labels are used to separate the traffic of different customers as it travels over the shared infrastructure, ensuring it doesn't mix or congest with traffic from other customers.

* **CE Router (Customer Edge Router):** Customer Premise Equipment (CPE) at the customer's site.
* **PE Router (Provider Edge Router):** Connects directly to CE Routers and is the entry/exit point of the MPLS network for customer traffic.
* **P Router (Provider Core Router):** Forms the internal network infrastructure of the service provider's network but doesn't connect directly to the Customer Edge Routers.

When frames are received on the PE Routers from the CE Routers, they add a label to the frame. This label is placed in-between the Layer 2 Ethernet Header and the Layer 3 IP layer (effectively, Layer 2.5). These labels are used to make forwarding decisions within the Service Provider Network. MPLS Routers use the MPLS Label to decide where to forward the packet rather than a Routing table. CE Routers do not use MPLS; it's only used by the Provider Edge and Provider Core Routers.

When using MPLS VPNs, the CE and PE Routers peer using OSPF to share routing information. The customer may even decide to use static routes with the PE Router as the next-hop.

A Layer 2 MPLS VPN could be used in place of OSPF. In this manner, the CE-PE do not form peers. The Service Provider network is entirely transparent to the CE Routers. In effect, or logically, it's like the 2 CE Routers are directly connected; their WAN Interfaces will be in the same subnet. If a routing protocol is used, the 2 CE Routers will peer directly with each other, making the PE/P Routers act as one big switch.

MPLS stands apart from other WAN Services due to its provision of effective QoS features. It provides a Layer 3 service to customers. MPLS itself is sometimes called a Layer 2.5 protocol because it adds the MPLS Header between the data-link header (Layer 2) & the IP header (Layer 3).

The SP's MPLS VPN Network (between the Provider Edge Routers - PE and the Provider Core Routers - P) will use a routing protocol to build routing protocol relationships with customer routers (CE). It will learn customer subnets/routes with those routing protocol relationships (e.g., OSPF, EIGRP, RIPv2). It will advertise a customer's routes with a routing protocol so that all routers that a customer connects to the MPLS VPN can learn all routes as advertised through the MPLS VPN Network.

All the Customer Edge Routers (CE) need to learn routes from the other CE routers. However, a CE Router does not form routing protocol neighbor relationships directly with other CE Routers. The process solely relies on the Provider Edge Routers (PE) and their PE-CE routing protocol neighborhood. To advertise the customer routes between the PE Routers, the PE Routers use another routing protocol along with a process called **Route Redistribution**. This happens when one router takes routes from one routing protocol process and injects them into another. Redistribution is needed when the PE-CE routing protocol is not BGP.

A Router PE.1 might sit in one Point of Presence (PoP) but connect to different customers. Likewise, Router PE.2 might connect to many of those same customers. These Routers use **VRF (Virtual Routing and Forwarding)** to facilitate turning one single router into multiple virtual routers, each with its own Routing Table.
**MP-BGP (Multiprotocol BGP)** can mark which routes are from which customers so that only the correct routes are advertised to each CE router for that customer. WAN Routes on the CE Routers refer to the neighboring PE Router as the next-hop router, with each CE Router becoming a routing protocol neighbor with the SP's PE Router on the other end of the Access Link.

---

### Multi-Protocol Label Switching (MPLS)

When it comes to Wide Area Network (WAN) connectivity, solutions based on Generic Routing Encapsulation (GRE) or Dynamic Multipoint VPN (DMVPN) that utilize the public internet as the transport network can suffer from unpredictable performance levels. Many organizations, especially in corporate settings, prefer **Multi-Protocol Label Switching (MPLS)** as a means of establishing private links with guaranteed service levels.

MPLS operates as an **overlay network**, meaning it can configure point-to-point or point-to-multipoint links between network nodes regardless of the underlying physical and data-link layer topologies. This makes it a very flexible and powerful solution for WAN providers.

#### How MPLS Works

Imagine you have two customer premises (CPE) routers at different sites, Site I and Site II, that need to communicate through an MPLS provider's cloud.

1.  **Label Edge Router (LER) - Ingress:** The CPE Router at Site I is attached to the service provider's MPLS cloud via an **Ingress Label Edge Router (LER)**.
2.  **Label Insertion (Push):** The Ingress LER acts as the entry point into the MPLS network. It inspects the incoming packet's Layer 3 header (e.g., IPv4 or IPv6) and, based on forwarding equivalence classes (FECs) and pre-configured policies, **inserts (pushes) a shim header (containing a label)** into each packet.
3.  **Label Switched Routers (LSRs):** The packet, now with its label, is forwarded to an **Label Switched Router (LSR)** within the MPLS cloud.
4.  **Label Switched Path (LSP):** Each LSR in the path examines only the label (the "shim"). It determines the **Label Switched Path (LSP)** for the packet, based on the type of data, network congestion, and other traffic engineering parameters determined by the service provider. Crucially, it uses this label to forward the packet to its next neighbor, rather than performing complex Layer 3 header lookups. This process is called **label swapping** (the LSR removes the incoming label and applies a new outgoing label). By avoiding costly routing table lookups at each hop, MPLS significantly speeds up packet forwarding.
5.  **Label Edge Router (LER) - Egress:** The labeled packet continues traversing the LSRs until it reaches the **Egress LER** (the exit point from the MPLS network).
6.  **Label Removal (Pop):** The Egress LER **removes (pops) the label** from the packet and then delivers the original Layer 3 packet to the destination CPE Router (e.g., at Site II).

#### Benefits of MPLS

MPLS allows WAN providers to offer various robust solutions for enterprise networking requirements:

* **Guaranteed Service Levels:** MPLS providers can apply traffic shaping policies to communication between enterprise LANs and data centers. This enables them to guarantee specific service levels, ensuring predictable performance for critical applications.
* **Enhanced Reliability and Redundancy:** Providers can implement link redundancy within their MPLS cloud, making connections much more reliable than those over the open Internet.
* **Site-to-Site VPNs:** A primary use of MPLS is to create site-to-site VPNs to interconnect LANs or connect branch offices to a data center.
* **Traffic Isolation:** Traffic passing over an MPLS VPN is isolated from any other customer traffic or public internet traffic, enhancing security and privacy. **It is crucial to understand that MPLS VPNs do NOT use the public internet as the transport network; they operate over the service provider's private infrastructure.**
* **Flexible Access Methods:** Different sites can use any available access method (e.g., DSL, cellular, leased line, Ethernet) to connect to the MPLS cloud.
* Many protocols can be used to connect to an SP's MPLS Network: Metro Ethernet / Fiber Links, Cable Provider Links (CATV), Serial Lines, 4G/5G, Digital Subscriber Line (DSL).
* **Flexible Topologies:** Sites can utilize point-to-point or point-to-multipoint topologies as required, offering greater design flexibility than traditional VPNs.

### Metro Ethernet

**Metro Ethernet (MetroE)** service uses Ethernet physical links to connect the customer's device to the service provider's device. The service is a Layer 2 service in that the WAN provider forwards Ethernet frames from one customer device to another, acting as though the WAN service was created by one Ethernet switch. Each Customer Edge device (be it a Router or Layer 3 Switch) connects to the service with (at least) one Ethernet link (preferably Fiber Ethernet standards) rather than connecting directly to other customer (enterprise) routers. The physical link between the customer and the SP is called an Access Link, or when using Ethernet, an Ethernet Access Link.

#### MetroE Service Types (Topology)

* **Ethernet Line Service (point-to-point):** Two Customer Premise Equipment can exchange frames. This is similar in concept to a leased line.
* **Ethernet LAN Service (full-mesh):** Acts like a LAN; all devices can send frames to all other devices. All devices have to be in the same subnet and become OSPF neighbors.
* **Ethernet Tree Service (Hub-n-Spoke):** A central site can communicate to a defined set of remote sites, but the remote sites cannot communicate directly with each other. This is also referred to as "partial mesh, point-multipoint, hub-and-spoke."

## NETWORK TYPES AND CHARACTERISTICS

A network comprises **nodes** and **links**.
* **Intermediate system nodes** perform a forwarding function (e.g., routers, switches).
* **End system nodes** are those that send and receive traffic, classified either as clients or servers.

* **Server:** A server makes network applications and resources available to other hosts.
* **Client:** A client requests and consumes the services provided by the servers.

### Client-Server Network

* A network where some end system nodes act mostly as servers.
* Servers are typically more powerful computers.
* Application services and resources are centrally provisioned, managed, and secured.
* This model is common in corporate environments.

### Peer-to-Peer Network

* A network where each end system acts as both a client and a server.
* This is a decentralized model where the provisioning, management, and security of services and data are distributed around the network.
* Common in small home networks or file-sharing applications.

### Network Type by Scope and Size

A network type refers primarily to its **scope** and **size**.
* **Size:** Can be measured by the number of nodes.
* **Scope:** Refers to the area over which nodes sharing the same network are distributed.

1.  **Local Area Network (LAN):**
    * Describes a network type confined to a single geographical location (e.g., a home, small office/home office (SOHO), small/medium enterprise (SME) network, enterprise LAN, or data center).
    * The term **Campus Area Network (CAN)** is sometimes used for a LAN that spans multiple nearby buildings within a limited geographical area.
    * The term **Wireless Local Area Network (WLAN)** is used for LANs based on wireless technology (e.g., Wi-Fi hotspots).

2.  **Wide Area Network (WAN):**
    * Describes a "network of networks" connected by long-distance links.
    * A WAN connects two or more large LANs.
    * WANs are likely to use leased network devices and links, operated and managed by a service provider.
    * The term **Metropolitan Area Network (MAN)** is sometimes used for a network smaller than a WAN in scope, typically a city-wide network encompassing multiple different buildings.

3.  **Personal Area Network (PAN) and Wireless PAN (WPAN):**
    * Gaining traction as the Internet of Things (IoT) evolves.
    * Refer to close-range network links a person might establish between a variety of wearable or portable devices (e.g., Bluetooth devices, smartwatches, fitness trackers).

---

## NETWORK TOPOLOGY

A **network topology** describes the physical or logical structure of the network in terms of **nodes** and **links**.

1.  **Physical Structure:** Describes the actual placement of nodes and how they are connected by the network media (e.g., directly connected via a single cable, or connected to a switch via separate cables).
2.  **Logical Structure:** Describes the flow of data through the network, irrespective of the physical structure. Nodes share a logical layout in which they can send messages to one another.

### Common Topologies

* **Point-to-Point Link:**
    * The simplest type of topology where a single link is established between two nodes (a 1:1 relationship).
    * Point-to-point links can be a physical or logical topology. For example, in a WAN, two routers might be physically linked via multiple intermediate networks and physical devices but still share a logical point-to-point link (e.g., a VPN tunnel).

* **Star Topology:**
    * Each endpoint node is connected to a central forwarding node (e.g., a Layer 1 hub, Layer 2 switch, or Layer 3 router).
    * The central node mediates communications between endpoints.
    * **Advantages:**
        * Easy to reconfigure (add/remove nodes).
        * Easy to troubleshoot because all data goes through a central point, which can be used to monitor and manage the network.
        * Faults are isolated to the central node or the link to a specific endpoint.
    * **Disadvantages:**
        * A single point of failure at the central device.
        * Requires more cabling than a bus or ring.
    * **Hub-and-Spoke:** This terminology is often used when speaking about WANs with remote branches (spokes) connecting to a central office (hub).
    * **Ethernet deployments:** Modern Ethernet using switches (not hubs) often appear as a **physical star** but operate as a **logical bus** because switches still share a single broadcast domain by default unless VLANs are used. (Note: Deprecated physical bus topology is no longer used on LANs).

* **Mesh Topology:**
    * Each endpoint device has a point-to-point link with every other device on the network.
    * Commonly used in WANs, especially public networks like the Internet.
    * **Fully Connected Mesh:** Impractical for large networks as the number of links required is expressed as $n(n-1)/2$, where $n$ is the number of nodes.
    * **Hybrid Approach (Partial Mesh):** Often implemented, with only the most important devices interconnected in the mesh, perhaps with extra links for fault tolerance and redundancy.
    * **Advantages:**
        * Provides excellent redundancy and fault tolerance.
        * Packets can take multiple routes through the network, providing resilience if some nodes or links fail.
        * Nodes can forward packets to a destination by learning the network topology.
    * **Disadvantages:**
        * Complex to implement and manage.
        * High cabling costs for full mesh.

* **Ring Topology:**
    * Each node is wired to its neighbor in a closed loop.
    * Often employs the use of a **token** during transmissions (e.g., Token Ring, FDDI - Fiber Distributed Data Interface, though these are largely obsolete).
    * A node receives a transmission from its upstream neighbor and passes it to its downstream neighbor until the transmission reaches its intended destination.
    * **Advantages:**
        * Each node can regenerate the transmission, improving the potential range of the network.
        * Can cover long distances.
    * **Disadvantages:**
        * A break in the ring causes the whole network to fail.
        * **Dual Counter-Rotating Rings** can be used to provide fault tolerance, allowing the system to continue operating if there is a break in one ring.

* **Bus Topology:**
    * All nodes attach directly to a single cable segment (the "bus cable").
    * Signals travel down the bus in both directions from the source and are received by all nodes connected to the segment.
    * The bus is terminated at both ends of the cable to absorb the signal when it has passed all connected devices.
    * Nodes use **collision detection** (e.g., in early Ethernet) to find opportunities to transmit, as they all share the bandwidth of the media. A device recognizes and processes packets addressed to its hardware address or a broadcast address, otherwise, it ignores the packet.
    * **Disadvantages:**
        * No longer in widespread use due to limitations on the maximum number of nodes on a segment of cable.
        * Difficult to reconfigure, as adding or removing nodes can disrupt the entire network.
        * Difficult to troubleshoot, as a cable fault could be anywhere on the segment.
        * A single point of failure if the bus cable is damaged.
    * A bus network allowed cables to be connected using repeaters (which are not considered nodes, just passive devices amplifying signals).
    * A **logical bus topology** is one in which nodes receive the data transmitted all at the same time, regardless of the physical wiring layout (e.g., Ethernet using a hub). However, only one node can transmit at a time, leading to collisions.

* **Hybrid Topology:**
    * Anything using a mixture of point-to-point links or star, mesh, ring, or bus physical or logical topologies.
    * For example, a **Physical Star - Logical Bus** (modern Ethernet with switches by default).
    * Hybrid topologies are often used to implement redundancy and fault tolerance or when connecting local area networks (LANs) to Wide Area Networks (WANs).

### Hierarchical Topologies (Common in Enterprise Networks)

* A **Hierarchical Star / Tree Topology** establishes a parent/child relationship between layers in the hierarchy. Corporate networks are often designed using this overall hierarchy.
* **Links between nodes in the Tree** are referred to as **backbones or trunks** because they aggregate and distribute traffic from multiple areas of the network.

* **Hierarchical Star - Mesh:**
    * Alternatively, parent nodes or nodes at the top of the hierarchy can be configured in a partial or full mesh for redundancy.
    * Switches lower in the hierarchy establish a star topology that connects end systems to the network.
    * This is commonly implemented in a **Three-Tiered Switching Architecture** (Access, Distribution, Core layers).

* **Star of Stars (or Hub-and-Spoke Topology):**
    * A WAN might be configured as a hub-and-spoke between a central office (hub) and branch offices (spokes).
    * Each site (hub and spokes) then implements a star topology locally to connect end systems.

* **Star with Rings:**
    * Alternatively, a ring topology might be used to connect geographically separate sites.
    * Each site then implements a star topology locally to connect end systems.

---

### How Network Topology Affects Performance

Network topology significantly impacts a network's performance, reliability, and scalability:

* **Star Topology (Switched Ethernet):**
    * **Performance:** Excellent. Each device has a dedicated connection to the switch, meaning no collisions between devices connected to different ports. Bandwidth is not shared on a segment-by-segment basis.
    * **Reliability:** High. A failure of one device or its cable doesn't affect others. The central switch is a single point of failure, but modern switches are highly reliable.
    * **Scalability:** Good. Easy to add new devices by connecting them to an available port.
* **Mesh Topology:**
    * **Performance:** Very high. Multiple paths for data allow for load balancing and avoiding congested links.
    * **Reliability:** Extremely high. Redundant paths ensure network continues to operate even if multiple links or nodes fail.
    * **Scalability:** Good, but full mesh becomes impractical very quickly as 'n' increases due to cabling and port requirements. Partial mesh scales better.
* **Ring Topology (Historical):**
    * **Performance:** Deterministic access (e.g., token passing) can provide predictable performance, but adding devices could slow down the ring.
    * **Reliability:** Low for a single ring (one break can take down the whole network). High for dual rings.
    * **Scalability:** Limited, adding/removing devices typically requires taking down the ring.
* **Bus Topology (Historical):**
    * **Performance:** Poor. Shared medium means only one device can transmit at a time, leading to collisions and significant performance degradation as more devices are added.
    * **Reliability:** Low. A single cable break takes down the entire segment.
    * **Scalability:** Very poor. Limited number of devices and difficult to add/remove.
* **Hybrid/Hierarchical Topologies:**
    * **Performance:** Optimized. Allows for specialized equipment at different layers (e.g., high-speed core routers, high-density access switches) to handle traffic efficiently.
    * **Reliability:** Very high. Redundancy can be built into higher layers (e.g., mesh at core/distribution) while simplifying access.
    * **Scalability:** Excellent. Networks can be expanded by adding more access layer devices or entire new network modules.

In summary, choosing the right network type and topology, combined with appropriate Layer 1, 2, and 3 functions, is critical for designing a network that meets specific performance, reliability, security, and scalability requirements.

---

# CHAPTER 16: TROUBLESHOOTING & INFORMATION GATHERING TOOLS

This chapter details various network troubleshooting and information-gathering tools, focusing on their functionality and typical use cases.

## Basic Network Utilities (Command Line)

### `ping`

The `ping` command is used to test network connectivity to a remote host. It sends **ICMP ECHO_REQUEST** packets (Type 8) and expects **ICMP ECHO_REPLY** packets (Type 0) in return.

* **Syntax:**
    * `ping <IP_Address>`: To test connectivity to a specific IP address.
    * `ping <Hostname>`: To test connectivity to a domain name, also implicitly testing DNS resolution.
* **Specific Uses:**
    * `ping localhost` or `ping 127.0.0.1`: Can be used to diagnose issues related to a network card failure. If successful, the network stack on the local machine is functioning.
    * `ping DomainName`: Helps identify internet domain name resolution issues (DNS problems). If ping to IP works but to domain name fails, it indicates a DNS problem.
* **Packet Information:** `ping` displays the **Round Trip Time (RTT)** in milliseconds, indicating latency, and the **Time-to-Live (TTL)** value of the received packet.
    * **Time-to-Live (TTL):** A field in the IP header that is decremented by one by each router (hop) that forwards the packet. When TTL reaches 0, the packet is discarded, preventing indefinite looping. The TTL value in the `ping` response indicates how many hops the packet took to reach the destination.
* **Errors:**
    * "Destination host Unreachable": Indicates no routing information, an incorrect default gateway, loss of local connectivity, or a routing configuration error.
    * "No Reply" / "Request timed out": The host is unavailable, cannot route a reply, packet dropped due to TTL expiry, congestion, or a firewall blocking ICMP.

### `ipconfig` (Windows) / `ifconfig` / `ip` (Linux/macOS)

These commands display and sometimes configure network interface parameters.

* **`ipconfig /all` (Windows):** Lists comprehensive TCP/IP configuration details, including IP address, subnet mask, default gateway, DNS servers, DHCP server, MAC address, and lease information.
* **`ifconfig` (macOS, Linux - Legacy):** Lists IP address and mask for specific interfaces or all interfaces.
    * **Note:** In modern Linux distributions, `ifconfig` is largely superseded by the `ip` command from the `iproute2` utility suite.
* **`networksetup -getinfo interface` (Mac):** Lists IP settings, including the default router.
* **`networksetup -getdnsservers interface` (Mac):** Lists DNS servers used.
* **`ip address` (Linux):** Lists IP address and mask information for interfaces; the Linux replacement for `ifconfig`. Often abbreviated as `ip a`.
    * `ip addr show` or `ip a`: Reports address configuration for all interfaces.
    * `ip addr show dev [interface_name]`: Reports information for a single interface (e.g., `ip addr show dev etho`).
    * `ip -s link show`: Displays status of interfaces and statistics.
    * `ip link set [interface_name] up/down`: Enables or disables an interface.
    * `ip addr add [ip_address]/[prefix_length] dev [interface_name]`: Used to add an IP address.
    * `ip addr del [ip_address]/[prefix_length] dev [interface_name]`: Used to delete an IP address.
    * **Note on Persistent vs. Running Config:** `ip` commands by default modify only the running configuration, which is lost on reboot unless saved to persistent configuration files (e.g., `/etc/network/interfaces` or NetworkManager/systemd-network configurations).
* **Windows DNS Cache Management:**
    * `ipconfig /displaydns`: To view the local DNS cache.
    * `ipconfig /flushdns`: To purge the local DNS cache.
    * `ipconfig /all && nslookup command`: To display Windows device DNS servers.

### `netstat`

`netstat` (Network Statistics) resolves and displays network statistics such as current network connections and port activities.

* **`netstat -a`:** Shows all listening ports and established connections.
* **`netstat -at` or `netstat -au`:** List TCP or UDP protocols respectively.
* **`netstat -l`:** List ports in "listening" mode (open and ready to accept incoming connections). Can be combined with `t` or `u` (e.g., `netstat -lt`).
* **`netstat -s`:** List network usage statistics by protocol. Can be combined with `-t` or `-u`.
* **`netstat -tp`:** List connections with the service name and PID (Process ID) information.
* **`netstat -i`:** Shows interface statistics.
* **Common Use:** `netstat -ano` (Windows)
    * `-a`: Display all sockets.
    * `-n`: Do not resolve names (displays IP addresses and port numbers numerically).
    * `-o`: Display timers (Windows specific, shows PID).
* **`netstat -rn` (Windows, Mac, Linux):** Lists the host's routing table, including a default route that uses the DHCP-learned default gateway.
    * **Note:** In modern Linux, `ip route` is the replacement for `netstat -rn`.

### `arp` / `ip neigh`

The `arp` (Address Resolution Protocol) utility is used to manage the ARP cache, which stores mappings between IP addresses and MAC addresses on the local network.

* **`arp -a` (Windows, Mac, Linux):** Displays the current ARP cache contents.
* **`arp -d [IP Address]`:** Deletes a specific entry from the ARP cache.
* **`arp -d`:** Deletes all entries from the ARP cache.
* **`arp -s [IP Address] [MAC Address]`:** Adds a static entry to the ARP cache.
* **`ip neigh` (Linux - Modern):** The replacement for `arp` in Linux, for managing the neighbor table (which includes ARP entries).

### `traceroute` / `tracert`

`traceroute` (Linux/macOS/Routers) or `tracert` (Windows) determines the path (route) that packets take to reach a destination host, showing each intermediate router (hop).

* **How it works:** Sends probes with incrementally increasing TTL values.
    * TTL=1 probe: Causes the first router to respond with an ICMP Time Exceeded message.
    * TTL=2 probe: Causes the second router to respond, and so on.
    * This continues until the destination is reached, which responds (Windows `tracert` uses ICMP Echo Reply, Unix `traceroute` typically uses ICMP Port Unreachable).
* **Syntax:**
    * `traceroute <destination>` (Linux)
    * `tracert <destination>` (Windows)
* **Protocol:** By default, Windows `tracert` uses ICMP. Unix `traceroute` uses UDP. Both can be configured to use the other protocol with switches (e.g., `-I` for ICMP in Linux `traceroute`).
* **IPv6:** `traceroute -6` or `tracert -6` for IPv6 networks.
* **Output:** Shows the IP address of each hop and the RTT for multiple probes to that hop. An asterisk (`*`) indicates no response within the timeout period (e.g., router not responding, firewall blocking, packet looping).
* **Use Cases:** Isolating network bottlenecks, identifying where packets are being dropped, or mapping network paths.

### DNS Lookup Utilities (`nslookup`, `dig`, `host`)

These tools are used to query DNS servers for information about domain names.

#### `nslookup` (Name Server Look Up)

* Finds the IP address of a domain name.
* **Syntax:** `nslookup DOMAIN_NAME` or `nslookup -type=QUERY_TYPE DOMAIN_NAME SERVER`
    * `QUERY_TYPE`: (e.g., `A` for IPv4, `AAAA` for IPv6, `MX` for mail exchange, `NS` for name server).
    * `DOMAIN_NAME`: The domain you are querying.
    * `SERVER`: Optional; the specific DNS server to query (e.g., 1.1.1.1, 8.8.8.8).

#### `dig` (Domain Information Groper)

* A more flexible and powerful tool for interrogating DNS name servers, providing more detailed output than `nslookup`.
* **Syntax:** `dig @server name type`
    * `@server`: The name or IP address of the DNS server to query.
    * `name`: The domain name or resource record to look up.
    * `type`: The type of query (e.g., `ANY`, `A`, `MX`, `SIG`). If omitted, defaults to `A` record.
* **Key Feature:** Displays the **TTL (Time To Live)** of the queried DNS record, indicating how long the record should be cached by clients before being re-queried.

#### `host`

* A simple utility for performing DNS lookups, primarily used to convert names to IP addresses and vice versa.
* **Syntax:** `host {name} [server]`
    * `name`: The domain name, IPv4, or IPv6 address to look up.
    * `server`: Optional; the name or IP address of the DNS server to query instead of the default.

### `whois`

* Allows you to query public databases for information about domain name registrations (registrant, registrar, nameservers, registration dates).
* **Note:** May require installation (`sudo apt install whois` on Debian-based systems).
* Queries Network Information Centers (NICs) databases, starting with IANA and following referrals to more specific servers.

## Advanced Network Analysis Tools

### Protocol Analyzers

A **Protocol Analyzer** works in conjunction with a **packet capture** or **sniffer** tool.
* **Function:** Parses each frame in a stream of traffic to reveal its header fields and payload contents in a readable format (Packet Analysis).
* **Features:**
    * **Filters:** To show only particular frames or sequences of frames.
    * **Follow TCP/UDP Stream:** Reconstructs the packet contents for a TCP/UDP session.
    * **Conversation and Statistics:** Monitor communication flows (e.g., bandwidth consumed per protocol or per host), identify active network hosts, and monitor network utilization and bottlenecks.

#### Connecting a Sniffer:

1.  **Switched Port Analyzer (SPAN) / Mirror Port:** A specifically configured switch port that receives copies of frames addressed to nominated access ports.
2.  **Passive Test Access Point (TAP):** A hardware device that physically copies the signal from network cabling to a monitor port without interfering with the active link.
3.  **Active Test Access Point (TAP):** A powered device that performs signal regeneration, often used for more complex monitoring scenarios.

### `tcpdump`

`tcpdump` is a command-line packet capture utility on Linux, providing a user interface to the `libpcap` library.

* **Basic Syntax:** `tcpdump -i eth0` (captures traffic on `eth0`).
* **Filters:** Often used with filter expressions combined using Boolean Operators (`and`, `or`, `not`). Complex filters should be enclosed in quotes and can use parentheses for grouping.
    * **Example:** `sudo tcpdump ip proto \\icmp -i interfaceName` (listens specifically for ICMP traffic).
    * **Complex Filter Example:** `tcpdump -i eth0 "src host 10.0.1.100 and (dst port 53 or dst port 80)"`
* Supports Regex for searching within captured output.

### `Ncat` / `Wireshark` / `Tshark`

* **NCAT (Netcat Tool):** A versatile network utility used for reading from and writing to network connections. Can be used to copy network traffic across devices for analysis.
* **Wireshark:** An open-source graphical packet capture, filter, and analysis utility.
    * **Interface:** Displays output in a 3-pane view:
        * Upper pane: Each captured frame.
        * Middle pane: Decoded fields of the currently selected frame.
        * Bottom pane: Raw data in Hex and ASCII.
* **Tshark:** The command-line version of Wireshark.

### NetFlow (and IPFIX)

**NetFlow** gathers **metadata only** (summarized traffic information, not the full packet payload) and reports it to a structured database. It can also use sampling to further reduce processing demands. NetFlow has been redeveloped as the **IP Flow Information Export (IPFIX)** IETF standard.

**Components of a NetFlow deployment:**

1.  **NetFlow Exporter:** Configured on network appliances (switches, routers, firewalls).
    * A **traffic flow** is defined by packets that share the same characteristics (e.g., source IP, destination IP, source port, destination port, protocol – often called a **5-tuple**). A **7-tuple** flow adds the input interface and IP Type of Service.
    * The Exporter caches data for newly seen flows and transmits the data to a collector when the flow expires (e.g., after a period of inactivity or reaching a size limit).
2.  **NetFlow Collector:** Aggregates flows from multiple exporters. Requires high-bandwidth network links and substantial storage capacity. Must support compatible NetFlow versions (most widely deployed are v5 and v9) or IPFIX.
3.  **NetFlow Analyzer:** Reports and interprets information by querying the collector. Can be configured to generate alerts and notifications. In practical terms, the Collector and Analyzer are often integrated into one solution.

**Use Cases:** Network monitoring, security analysis, billing, traffic engineering, and capacity planning.
---

# CHAPTER 17: NETWORK TROUBLESHOOTING METHODOLOGY

Effective network troubleshooting requires a systematic approach to problem-solving and clear communication with users/clients. The following best practice model provides a proven process:

### 1. Identify the Problem

This initial phase is about gathering as much information as possible to understand the issue.

* **Gather Information:**
    * **Scope:** Determine the scope of the problem (e.g., single user affected, multiple users/group, specific workstation, entire network segment). This helps identify the source and prioritize the issue.
    * **Symptoms:** Identify facts and clues in the affected system. Symptoms can be correlated with known cases and issues. Issues that are difficult to reproduce are often the hardest to troubleshoot.
    * **Duplicate the Problem (If Possible):** This is crucial for understanding the exact conditions under which the problem occurs and for later testing your solution.
* **Question Users:**
    * Use **Open Questions** to encourage users to explain the problem in their own words (e.g., "Describe what happened when you tried to access the network.").
    * Use **Closed Questions** to get explicit Yes/No or fixed responses (e.g., "Is the power light on the router green?").
* **Determine if Anything Has Changed:** This is often the most critical question.
    * "Did it ever work?"
    * "What has changed since it last worked?" (e.g., new software, hardware, configuration change, user activity).
* **Approach Multiple Problems Individually:** If problems are not related, treat each issue as a separate case, advising the user to initiate a separate support request. However, if they seem related, check for outstanding support or maintenance tickets that might indicate existing problems.

### 2. Establish a Theory of Probable Cause

Based on the information gathered, formulate hypotheses about what might be causing the problem.

* **Question the Obvious:** Start with the simplest and most common potential points of failure.
* **Consider Multiple Approaches:** If one approach doesn't identify the problem, use a different one.
* **OSI Model Approach (Methodical Validation):**
    * **Top-to-Bottom / Bottom-to-Top:** Test or prove the functionality of each component at each layer of the OSI model in sequence, starting from either the top (Application layer) or bottom (Physical layer). Only move up/down when you have discounted a layer as the source of the problem.
    * **Divide and Conquer:** Rather than starting strictly at the top or bottom, begin with the layer most likely to be causing the problem (based on symptoms and scope) and then work either up or down depending on your tests' revelations. This is generally the most efficient for experienced troubleshooters.

### 3. Test the Theory to Determine Cause

Put your hypothesis to the test using diagnostic tools and techniques.

* **Confirm Theory:** If your test confirms the theory, you can proceed to determine the steps to solve the problem.
* **Re-establish New Theory / Escalate:** If the theory is not confirmed, re-evaluate the symptoms, gather more information, and establish a new theory. If you've exhausted your theories or expertise, **escalate** the problem. Escalation means referring the problem to a senior technician, specialized technical staff (developers, programmers), third-party vendors/suppliers, or service carriers/contractors.

### 4. Establish a Plan of Action to Resolve the Problem and Identify Potential Effects

Once the cause is confirmed, plan the solution.

* An action plan sets out the specific steps you will take to solve the problem (e.g., repair, replace, upgrade, reconfigure).
* **Test by Substitution:** A basic but effective technique when troubleshooting devices by having a known good duplicate on hand.
* **Assess Cost and Time:** Consider the cost and time required for the solution, as well as its potential disruptive effects on the rest of the system or users. Plan for minimal disruption.

### 5. Implement the Solution or Escalate as Necessary

Execute your action plan.

* **Authorization:** If you don't have authorization to implement a solution (e.g., requiring system downtime, significant configuration changes), escalate to a senior staff member for approval.
* **Scheduling:** If applying the solution is disruptive to the wider network, consider the most appropriate time to schedule the reconfiguration work (e.g., off-hours) and plan how to notify users/clients.

### 6. Verify Full System Functionality and Implement Preventive Measures

After implementing the solution, thoroughly check that the problem is fixed and that no new issues have been introduced.

* **Validate the Fix:** Confirm that the solution addresses the reported problem.
* **Verify Overall Functionality:** Ensure the system as a whole continues to function normally. Identify the effects/results of the solution.
* **Preventive Measures:** To fully solve a problem, you should try to eliminate any factors that may cause the problem to recur or persist by implementing preventive measures (e.g., documentation, training, process changes, hardware upgrades, monitoring).

### 7. Document Your Findings, Actions, and Outcomes

Documentation is crucial for knowledge management and future troubleshooting.

* **Clarity and Conciseness:** Write clearly, concisely, and free from grammatical/spelling errors.
* **Ticket System:** Most troubleshooting takes place within the context of a ticket system. This is immensely useful for future troubleshooting, as problems fitting into the same category can be reviewed to see if the same solution applies.

---

### Troubleshooting Common Issues that Affect Cabled Network Connectivity

#### Network Performance Characteristics

* **Speed:** Often used broadly to describe how well a link is performing.
* **Band Rate (Baud):** Measured in Hertz (Hz), this is the number of symbols that can be transmitted per second. A symbol is a series of events that make up signals (e.g., a pulse of higher voltage, or the transition between peak and trough in electrical signals). Encoding schemes ensure the bit rate will be higher than the baud rate. (Physical Layer)
* **Bandwidth:** The theoretical maximum amount of information that can be transmitted, measured in bits per second (bps). (Data Link Layer)
* **Throughput:** The actual average data transfer rate achieved over a period of time. This excludes encoding schemes, errors, and losses incurred at the physical and data link layers, and is affected by link distance and interference. Throughput is often referred to as **packet loss** when measured at the Network (Layer 3) and Transport (Layer 4) layers.
* **Latency / Delay:** The speed at which packets are delivered, measured in units of time (typically milliseconds, ms). Latency can occur at many layers of the OSI model.

#### Signal Issues

* **Attenuation:** Loss of signal strength (expressed in decibels, dB). Measured as the ratio between signal strength at the origin/source versus at the destination.
    * A logarithmic scale (dB) is used due to its non-linear function; a small change in dB value represents a large change in measured performance.
    * `+3dB` means doubling, `-3dB` means halving; `+6dB` means quadrupling, `-6dB` means quartering.
    * The maximum allowed value for insertion loss depends on the cable category and standard. Smaller values are better (less loss).
    * Solutions for high attenuation: Use higher grade or shielded cable, find a shorter cable run, or install a repeater/additional switch.
* **Noise:** Anything that is transmitted within or close to the channel that isn't the intended signal. Expressed in **Signal-to-Noise Ratio (SNR)**. Noise makes the signal itself difficult to distinguish, causing errors in data and leading to retransmissions.
    * A high SNR value means the signal strength is significantly greater than the noise present. A result closer to 0 dB indicates the link is subject to high error rates.
    * **Electromagnetic Interference (EMI):** Noise that should ideally be detected when the cable is installed. If it appears later, suspect a new source or a source not accounted for during initial testing.
    * **Radio Frequency Interference (RFI):** EMI that occurs in frequencies used for radio transmissions.
    * **Crosstalk:** Interference from nearby cables (also measured in dB). Usually indicates problems with bad wiring, poor quality cables, improper cable type for the application, or bad connectors/improper termination.

        * **NEXT (Near End Crosstalk):** Measures crosstalk on the receive pairs at the transmitter end.
        * **ACR-N (Attenuation to Crosstalk Ratio, Near End):** Difference between Insertion Loss and NEXT.
        * **ACR-F (Attenuation to Crosstalk Ratio, Far End):** Difference between Insertion Loss and FEXT (Far End Crosstalk).
        * **Power Sum (PSNEXT, PSACR-N, PSACR-F):** Combine crosstalk from multiple pairs.
* **Loss of Connectivity:**
    * **Complete Loss:** Indicates a break in the cable or faulty installation.
    * **Intermittent Loss:** Often indicates degradation from attenuation or crosstalk.

#### Cabling Issues (Physical Layer)

A typical Ethernet link for an office workstation includes:

1.  Network Transceiver in the host (end system)
2.  Patch cable between host and a wall port
3.  Structured cable between the wall port and a patch panel (permanent link)
4.  Patch cable between the patch panel and a switch port
5.  Network Transceiver in the switch port (intermediate system)

* **Network Loopback Adapter:** A specially wired RJ-45 plug with a stub of cable, used to test for bad ports and network cards. Wiring: pin 1 (Tx) to pin 3 (Rx) and pin 2 (Rx) to pin 6 (Tx), meaning packets sent by the NIC are received by itself.

* **LED Status Light Indicators (Link Lights):** On the Host NIC and Switch/Router ports.
    * **Solid Green:** Link is connected, but no traffic.
    * **Flickering Green:** Link is operating normally (with traffic). Blink rate often represents the speed.
    * **No Light:** The link is not working, or the port is shut down.
    * **Blinking Amber:** A fault has been detected (e.g., duplex mismatch, excessive collisions).
    * **Solid Amber:** The port is blocked by the Spanning Tree Algorithm (STP) to prevent loops within the domain.

* **Verifying Port Settings (Auto-negotiation, Speed, Duplex):**
    * Most NIC adapters and switches use **Auto-Negotiation** for port settings. If this process fails, the adapter and port can end up with mismatched speed or duplex settings, often because one end was manually configured. Setting both to auto-negotiate generally resolves this.
    * A **Speed Mismatch** will cause a **link failure** (no connectivity).
    * A **Duplex Mismatch** will slow the link down considerably, causing high packet loss and late collisions (often seen as blinking amber on Cisco switches for duplex mismatch detection).

* **Cable Installation and Types:**
    * Ensure the cable grade is appropriate for the application (e.g., Cat 6 for Gigabit Ethernet).
    * Ensure the cable jacket is suitable for the installation location: **Plenum-rated cable** in plenum spaces (for fire safety), **Riser-rated cable** in riser spaces.
    * The best time to verify wiring installation and termination is immediately after connections are made, while cable runs are still accessible.

* **Cable Testers:** Report detailed information on the physical and electrical properties of a cable.
    * They test and report on cable conditions, crosstalk, attenuation, noise, and resistance.
    * **Time Domain Reflectometer (TDR):** Often incorporated into advanced cable testers. A TDR measures the length of a cable run and locates breaks, shorts, kinks, sharp bends, and other imperfections affecting performance. It transmits a short signal pulse and measures the amplitude and time delay of reflections to determine distance to a fault (often within a meter).
    * **Multimeter:** For testing electrical circuits, can test continuity of copper wire, existence of a short, and integrity of a terminator.
    * **Wire Map Tester:** Multimeters designed for computer networks can incorporate this function to identify wiring problems.

* **Wiring Problems (Pin-out / Termination Issues):**
    * **Continuity (Open):** A conductor does not form a closed circuit (a break in the wire).
    * **Shorts:** Two conductors are joined at some point due to insulating wire damage.
    * **Incorrect Pin-out / Termination / Mismatched Cable Standards:** Conductors are incorrectly wired into the terminals.
        * **Reversed Pair:** Conductors in a pair have been wired to different terminals (e.g., pin 1 and 2 are swapped).
        * **Crossed Pair (Tx/Rx Reverse):** The conductors from one pair have been connected to pins belonging to a different pair (e.g., Tx pair connected to Rx pair pins).
        * **Split Pair:** Both ends of a single wire in one pair are wired to different pairs. Split pairs can only be measured by a cable tester that measures crosstalk.

* **Network Tone Generator / Probe (Fox and Hound):** Used to trace a cable from end to end, which is necessary when cables are bundled and not properly labeled.

#### Fibre-Optic Cable Testing Issues

While fiber optic cables do not suffer from attenuation to the same extent as copper, there is still some signal loss due to microscopic imperfections in the glass fiber core or its edges, causing light to scatter or be absorbed.

* **Attenuation:** EIA/TIA 568 specification allows for signal loss between `0.5 dB/km` to `3.5 dB/km`, depending on fiber type and wavelength.
    * Tested using an **Optical Power Meter** and **Optical Light Source**.
* **Cable Break:** Located using an **Optical Time Domain Reflectometer (OTDR)**, which can also verify the soundness of new splices and connections.
* **Optical Spectrum Analyzer (OSA):** Typically used with Wavelength Division Multiplexing (WDM) to ensure each channel has sufficient power, especially over long distances where attenuation of different wavelengths can vary (Spectral Attenuation).
* **Common Fibre Issues:**
    * **Dirty Optical Connectors:** Dirt, dust, or grease in the transmission path will greatly reduce signal strength or completely block transmission.
    * **Incorrect Transceivers:** Using mismatched transceivers (e.g., SFP, GBIC, media converters) at each optical interface. They must match for complete transmission, as they are designed for specific fiber types. For example, transceivers for single-mode fiber use lasers, while multi-mode fiber transceivers typically use LEDs (infrared light).
    * **Mismatch between Cable, Patch Cords, and Interfaces:** Can lead to significant signal loss.

---

#### Troubleshooting Common Network Layer and Application Layer Issues

#### DNS Issues (Can't Ping by Hostname)

* **DNS (Domain Name System):** Maps names to IP addresses. Many services use hostnames and domain names for ease of reconfiguration and user access. Name resolution is central to network functionality.
* **Common Problem:** Incorrect DNS server configuration. Most hosts are configured with primary and secondary DNS servers for redundancy, typically via DHCP.
    * **Windows:** `ipconfig /all`
    * **Linux:** `/etc/resolv.conf`
* **Troubleshooting Steps:**
    * Check that the correct DNS server addresses are configured.
    * Attempt to `ping` the DNS servers by their IP addresses to check connectivity between the host and its DNS servers. If you can ping the IP but not resolve names, the issue is likely DNS-related.

#### Multicast Flowing Issues

* **Multicast:** A "one-to-many" transmission designed for more efficient delivery of packets. Instead of a transmitter sending separate unicast packets to each receiver, a copy of the same packet is delivered to each receiver that has joined the relevant multicast group.
* **IGMP (Internet Group Management Protocol):** Used to establish multicast groups at Layer 3.
* **Problem:** If a switch is not "multicast-aware" (i.e., **IGMP Snooping** is not enabled), it will treat multicast transmissions as broadcasts and flood them across all ports in the broadcast domain. This consumes excessive bandwidth and slows down the network, especially if multicast traffic is flooded to VLANs that do not need to receive it.
* **Solution: IGMP Snooping:**
    * Enabling IGMP Snooping (globally on a switch and as a per-VLAN option) allows the switch to read IGMP messages.
    * The switch can then determine which hosts on an access port or within a VLAN have joined a multicast group, thereby filtering multicast traffic only to ports participating in the multicast group.

#### Intermittent Connectivity Issues (Often Complex)

It's wise to rule out physical hardware failures and data link layer issues before diagnosing network layer or service issues. Intermittent problems are often the most challenging.

* **Common Causes:**
    * Power failures (blackouts) or power loss (brownouts) - consider **Uninterruptible Power Supplies (UPS)**.
    * Hardware failure (host adapters, switches, routers, intermediary devices).
    * Cabling issues (e.g., damaged cable, loose connection).
    * Overheating of network devices.
* **Initial Steps:**
    * Use loopback testers and cable certifiers to rule out physical cable and port issues.
    * Often, restarting network devices can clear temporary errors.

#### Interface Status Issues

* If you isolate the issue to a single host and rule out cable/transceiver issues at the physical layer, the data link configuration might not be working.
* **Check LED Status Indicators:** (Connection UP/DOWN, Link Status).
* **Switch Command Line Utility:**
    * Check interface status (e.g., `show interfaces`).
    * Verify auto-negotiation, speed, and duplex settings are correctly configured.
    * Ensure the protocol status is "up." If the speed is mismatched between the host and switch port, the link will fail.
    * Check for faulty host NIC (Network Interface Card).

#### IP Configuration Issues

* Once physical and data link layers are ruled out, check basic IP addressing and protocol configurations.
* **Verify Host Configuration (`ipconfig` / `ifconfig` / `ip addr`):**
    * **Incorrect IP Address:** Each end system must have an IP address that produces a valid, unique host address within its subnet. Remember that the network address and broadcast address cannot be used for hosts.
    * **Incorrect Subnet Mask:** If a netmask is incorrect, the host might receive communications but misroute its replies, assuming the communicating hosts are on a different subnet. If the mask is shorter than it should be (e.g., `/24` instead of `/26`), it might cause packets to go via a router, placing unnecessary load on it.

### Routing Issues

* **Missing Route:** May arise because a required static routing entry has not been entered or was entered incorrectly, or due to a router's failure to communicate with its neighbors and thus not receiving routing protocol updates.
* **Troubleshooting Steps:**
    1.  **Ping Host's Default Gateway:** If you can ping a host's default gateway but cannot ping some/all hosts on remote networks, suspect a routing issue.
    2.  **Offline Router:** A router might have gone offline with no alternative path to the destination network. Be prepared for configuration issues.
    3.  **`traceroute` / `tracert`:** Utilize these commands to identify where the network path fails.
    4.  **Inspect Routing Tables (`show ip route` / `show route`):** Use these commands to confirm the presence of specific IP network routes.
    5.  **Identify Missing Route:** Due to incorrect static routing entries or communication failure.
    6.  **Device Config Review:** Ensure the device's running configuration matches the documented baseline.
    7.  **Ping Neighbor Router Nodes:** Verify basic connectivity between routers.
    8.  **Examine Routing Protocol Configuration:** If there is a network path and neighbors, focus on potential authentication issues or incorrect parameters in routing protocol configurations.

#### Routing Loops

* A **Routing Loop** occurs when two or more routers use one another as the path to a network. Packets caught in a routing loop circle around the routers until their TTL (Time-To-Live) expires.
* **Symptom:** Routers generating many ICMP Time Exceeded error messages.
* **Diagnosis (`traceroute`):** You can use `traceroute` to diagnose a routing loop by looking for IP addresses that appear multiple times in the output, as packets will traverse such routes more than once until TTL expires.
* **Prevention (Distance Vector Protocols):**
    1.  **Maximum Hop Count:** If the cost exceeds a certain value (e.g., 16 in RIP, 255 in EIGRP), the network is deemed unreachable ("poison route" advertised with a hop count of 16).
    2.  **Hold-down Timer:** If a node declares a network unreachable, its neighbors start a hold-down timer. Any updates received about that route from other nodes are discarded for the duration of the timer, ensuring all nodes have converged information about an unreachable network.
    3.  **Split Horizon:** Prevents a routing update from being copied back to the source interface from which it was learned.
* **Link-State Protocols:** Use timely updates and flood a consistent topology database to all nodes in the routing domain, ensuring each node has a consistent view of the network. A loop here indicates that timely updates are not propagated correctly.

#### Symmetric vs. Asymmetric Routing

* **Symmetrical Routing:** The return path of a route equals the forward path.
* **Asymmetrical Routing:** The return path of a route is different from the forward path.
    * **Problematic When:**
        * The return path has significantly higher latency/delay than the forward path.
        * Different paths cause stateful firewalls or NAT devices to filter or drop packet communication. This is common where load balancers or multiple redundant paths across the Internet are involved.
    * Such devices (stateful firewalls/NAT) should not be placed in the middle of a network where forward and return paths could diverge.

### Switching Loops

* A **Switching Loop** is where flooded frames circulate the network perpetually without intervention, causing a **Broadcast Storm**.
* **How it Happens:** Switches flood broadcasts (e.g., ARP, DHCP requests) out to all ports. If there's a loop (redundant link without proper control), these frames will go down one link to the next switch, which will send the broadcast back up the redundant link to the originating switch. As this repeats, switches start to see source MAC addresses associated with multiple ports, causing them to constantly clear their MAC address tables (MAC address flapping), which then causes them to flood unicast traffic as well (because they don't know where the MAC is).
* **Impact:** A broadcast storm can quickly consume all link bandwidth, crashing the network and connected appliances.
* **Prevention: Spanning Tree Protocol (STP):** STP detects loops and designates one port as a "blocking port" to prevent the loop, isolating the problem to a segment of the network.
* **Troubleshooting a Loop:**
    * Inspect physical ports that correspond to disabled interfaces for looped connections.
    * Check the switch log events related to MAC address flapping.
    * If a broadcast storm occurs on a network where STP is already enabled, investigate:
        * Verify compatible versions of STP are enabled on all switches.
        * Verify the physical configuration of segments that use legacy equipment (e.g., older Ethernet hubs).
        * Investigate network devices in the user environment (e.g., unmanaged desktop switches) and verify that they are not connected as part of a loop.
* Switching loops can be physical cabling issues or configuration interface issues.
* **Managed vs. Unmanaged Switches:** Unmanaged switches are basic plug-and-play devices with no configuration needed, offering less flexibility. Managed switches offer more control and can be customized (e.g., for creating VLANs, enabling STP).

---

### Network Visibility and Diagnostic Tools

* **Purpose:** To verify exactly what is connected to the network and what is being communicated over it. Necessary to confirm that servers and clients are in the correct VLAN/subnet and to identify unauthorized machines ("rogue hosts").
* **IP Scanners:** Tools that perform host discovery (determine if an IP address is "up") and can establish the overall topology of the network in terms of subnets and routers.
    * Often integrated with **IP Address Management (IPAM)** suites (combining DHCP, DNS, and IPAM, e.g., Windows Server, BlueCat, Infoblox, SolarWinds IPAM).
    * Some use SNMP queries for detailed network statistics.
    * Some are optimized for quick discovery of legitimate hosts; others are security-oriented for identifying hidden rogue hosts.
    * **Basic Tools:** `ping`, `arp`, `traceroute`.
    * **Advanced Tools:** `Nmap` (including `Zenmap` GUI) for host discovery, auditing, and penetration testing.

* **`netstat` Command (Network Statistics):** Allows you to check the state of ports on the "localhost."
    * Used to identify service misconfigurations, determine which services are running on which ports, and identify suspicious remote connections to services on the localhost.
    * **Common Switches:**
        * `-s`: Show TCP connections.
        * `-u`: Show UDP connections.
        * `-w`: Show raw sockets.
        * `-a`: Display all open ports, active ports, and listening ports.
        * `-l`: Display listening ports only.
        * `-n`: Display in numerical format (no name resolution).
        * `-4` or `-6`: Filter sockets by IPv4 or IPv6.
        * **Windows Specific:**
            * `-o`: Shows the Process ID (PID) that opened that port.
            * `-b`: Shows the process name.
        * **Linux Specific:**
            * `-p`: Shows PID and process name.
            * `-i`: Ethernet statistics.
            * `-r`: Routing table display. (Note: In Linux, `netstat` is deprecated in favor of `iproute2` commands like `ip link`, `ip addr`, `ss` for sockets, and `ip route`).
            * `-N`: Suppress name resolution.

* **Packet Analyzers (`tcpdump`, Wireshark, TShark):** Crucial for verifying exactly what traffic is on the wire, inspecting headers, and understanding communication flows. (Refer to previous notes on Protocol Analyzers).

---

## Interface Monitoring Metrics

Collecting data and configuring alerts for interface system metrics is crucial for proactive network management and troubleshooting.

**Key Interface Metrics:**

* **Link State:** Measures whether an interface is working (up) or not (down). This is the most basic connectivity check.
* **Resets:** The number of times an interface has restarted over a given period. Anything more than occasional resets should be closely monitored and investigated. An interface that continuously resets is described as **flapping**.
* **Speed:** The rated speed of an interface (e.g., Mbps, Gbps). For Ethernet links, the interface speed should match on both the host and switch ports. A speed mismatch will result in a link failure.
* **Duplex:** Most modern Ethernet interfaces operate in full-duplex mode. Operating in half-duplex mode requires investigation unless you are intentionally supporting legacy devices. A duplex mismatch will cause severe performance issues (high packet loss, late collisions).
* **Utilization:** The amount of data traffic (both sent and received) transferred over a period.
    * Calculated as a percentage of bandwidth.
    * Differentiate between **Average Utilization** and **Peak Utilization**. If average utilization is 80%, there might seem to be sufficient bandwidth, but if peak utilization spikes to 100%, this will manifest as delay and packet loss, indicating a need for an upgrade.
* **Per-Protocol Utilization:** Packet or byte counts for a specific protocol over a period. High packet counts for certain protocols can increase processing load on CPU and memory resources.
* **Error Rate:** The number of packets per second that cause errors. In general, error rates should be less than 1%. High error rates often indicate a driver problem, interference, or a poor quality link/cable.
* **Discards/Drops:** An interface may discard incoming or outgoing frames for several reasons, including:
    * Checksum errors.
    * Mismatched MTU (Maximum Transmission Unit).
    * Packets too small (runt) or too large (giant, jumbo frame mismatch).
    * High load/congestion.
    * Permissions (e.g., Interface Access Control List - ACL).
    * VLAN configuration problems.
    * Each interface is likely to categorize and type discards separately to assist with troubleshooting.
* **Retransmissions:** If you observe high levels of retransmissions (especially in TCP-based traffic), you must analyze and troubleshoot the specific cause of the underlying packet loss, errors, discards, or drops. This could involve multiple aspects of network configuration and connectivity.

### Troubleshooting Interface Errors

Interface errors often indicate a misconfiguration problem at Layer 2 (Data Link Layer) or Layer 1 (Physical Layer).

1.  **Cyclic Redundancy Check (CRC) Errors:**
    * A CRC is calculated by an interface when it sends a frame.
    * CRC errors are usually caused by interference due to poor quality cable or termination, attenuation, or mismatches of transceivers (SFPs) and cable types. These are typically Layer 1 issues.
2.  **Encapsulation Errors:**
    * Encapsulation refers to the frame format expected on the interface.
    * These errors prevent retransmission or reception. The physical link status will be "up," but the line protocol will be listed as "down."
    * Common causes include:
        * Incorrect Ethernet frame type.
        * Incorrect VLAN tagging (e.g., missing or wrong `802.1Q` tag).
        * WAN framing issues (e.g., PPP, Frame Relay configuration mismatch).
3.  **Runt Frame Errors:**
    * A runt frame is a frame that is smaller than the minimum 64-byte size for Ethernet frame format.
    * Usually caused by a **collision**.
    * In a switched environment, collisions should only be expected on an interface connected to a legacy hub device or if there is a duplex mismatch in the interface configuration.
    * If runt frames are generated in other conditions, suspect a driver issue on the transmitting host.
4.  **Giant Frame Errors:**
    * A giant frame is a frame that is larger than the maximum permissible MTU size (1518 bytes for Ethernet II, including preamble and Frame Check Sequence).
    * Two likely causes:
        * **Ethernet Trunks:** If one switch is configured for `802.1Q` (VLAN tagging) framing but the other is not, frames will appear too large to the receiver, as `802.1Q` adds 4 bytes to the header, making the max frame size 1522 bytes, which might not tally with the other end's expectation.
        * **Jumbo Frames Mismatch:** A host might be configured to use jumbo frames (typically up to 9000 bytes), but the switch interface is not configured to receive them. This type of issue often occurs when configuring Storage Area Network (SAN) links between SAN devices and data networks.

---

### Troubleshooting Service and Security Issues in the Application Layer

#### 1. DHCP Issues

If a client fails to obtain a DHCP lease, it defaults to using an **APIPA (Automatic Private IP Addressing)** address in the `169.254.0.0/16` range. Such a client will be limited to communication only with other APIPA hosts on the same network segment (broadcast domain).

**Possible Reasons for a Host to Fail to Obtain a DHCP Lease:**

* **DHCP Server is Offline:** Users will continue to connect to the network for a short period (until their existing lease expires), but will then start to lose contact with network services and servers as they try to renew their lease.
* **DHCP Scope / Port Exhaustion:** No more available addresses due to a high lease duration or a large number of devices.
* **Router Doesn't Support BOOTP Forwarding / DHCP Relays:** If the DHCP server is on a different subnet/VLAN than the client, the router between them must be configured to forward DHCP (BOOTP) requests.
    * **Solution:** Install RFC-1542 compliant routers or add another type of DHCP Relay agent to each subnet or VLAN.
* **Reconfiguration Issues:** During reconfiguration of DHCP servers and scopes, ensure to **lower the lease duration in advance** of changes. This forces all clients to renew their leases more frequently, mitigating the risk of expired IP, default gateway, or DNS server addresses not being updated when changes are applied.

#### Rogue DHCP Server Issues

A **Rogue DHCP Server** may be deployed accidentally (e.g., forgetting to disable a DHCP server in an access point/router) or by a malicious attacker to subvert the network.

* Since hosts have no means of preferring a DHCP server, clients could end up with an incorrect IP configuration because they obtained a lease from a rogue DHCP server.
* An attacker would normally use a rogue server to change the default gateway and/or DNS resolver addresses for the subnet, routing communications via their machine (an on-path attack).

#### 2. Name Resolution Issues

To troubleshoot name resolution, you should establish the different ways a host can use to resolve a hostname/FQDN to an IP address. In general, the following methods are tried in order:

a.  **Check Local Cache:** Individual applications (e.g., web browsers) and the operating system maintain their own caches of resolved names. Clear these caches for troubleshooting.
b.  **Check HOSTS File:** The `hosts` file (`%SystemRoot%\system32\drivers\etc\hosts` on Windows) is a static list of hostname-to-IP address mappings. In most cases, the `hosts` file should not contain any entries other than the loopback address (`127.0.0.1`). Any static entries here could be the cause of a name resolution issue.
c.  **Query DNS Servers:** A host uses the name servers defined in its IP configuration to resolve queries.
    * Modified forms of DNS allow clients to perform name resolution on a local link without needing a server, such as **Link-Local Multicast Name Resolution (LLMNR)** and **Multicast DNS (mDNS)**.

**DNS Configuration Issues:**

* Reconfiguration of DNS records should be planned and implemented carefully to avoid caching problems.
* In the absence of DNS servers, network clients will be unable to log on or connect to services or servers by name.
* **Troubleshooting Symptoms:**
    * **Ability to connect to a server by IP address but not by name:** This strongly suggests a name resolution problem. To verify, you can temporarily edit the `hosts` file on the client and place the correct name-to-IP address record for the target host. If it then works, the issue is DNS.
    * **If a single client is unable to resolve names:** The issue is likely with the client's current configuration.
        * Client has been configured with no DNS server address or an incorrect DNS address.
        * Client has an incorrect DNS suffix. Verify the DNS domain in which the client is supposed to be and verify the host's configuration matches.
    * **DHCP Impact:** Bear in mind that in both of these situations, DHCP might be configuring these settings incorrectly (address and suffix). Therefore, verify and check the server and scope options configuration on the DHCP server as well.
    * **If multiple clients are affected:** The issue is likely to lie with the DNS server service itself, or the way a subnet accesses the DNS server service. Check that the DNS server is online and available (e.g., `ping` the resolver from affected clients).

#### 3. Untrusted Certificate Issues

The most common reason for a certificate not to be trusted is that the **Certificate Authority (CA) issuer is not trusted**.

* If you trust a web server's CA issuer, you can add their certificate to the client's Root Certificate store.
    * **Windows:** Use `certmgr.msc` console to manage user certificates and `certlm.msc` console to manage machine certificates (certificates used by the computer or its user accounts).
* **Complication:** Different applications (e.g., web browsers, email clients) may have different stores of trusted certificates.
* **Other Causes of Untrusted Certificates:**
    1.  **Certificate Subject Name Does Not Match URL:** The certificate's common name (CN) or Subject Alternative Name (SAN) does not match the URL/hostname being accessed. Confirm the certificate common name and access the website by using that exact URL. This can also happen if a host is being accessed via an IP address instead of its hostname.
    2.  **Certificate Not Being Used for Its Stated Purpose:** For example, a certificate intended for signing email is being used on a web server. In such a case, do not add an exception. The service owner or subject should obtain a correctly formatted certificate.
    3.  **Certificate is Expired or Revoked:** Do not allow an exception unless you explicitly know and trust the situation.
    4.  **Time is Not Correctly Synchronized between Server and Client:** This is a common cause of certificate validation failures.

#### 4. NTP Issues (Network Time Protocol)

Most network services, especially authentication and authorization mechanisms, depend upon each host using a synchronized time source. Inaccurate time sources can:

* Affect the reliability and usability of log data, which can have implications for regulatory compliance.
* Cause certificate validation failures (as noted above).
* Lead to issues with Kerberos authentication, which has strict time synchronization requirements.

Clients must be able to access a time source over **UDP port 123**.
* **Windows:** The `w32tm /query /configuration` command can be used to check the current time synchronization configuration.

#### 5. VLAN Assignment Issues

Each VLAN is a discrete broadcast domain.

* **Service Availability:** Ensure services (e.g., DHCP, DNS) are available to all VLANs; otherwise, clients will be unable to access the Internet, for example, if there is no local DNS server available to handle their name resolutions.
* **Inter-VLAN Communication:** For devices in separate VLANs that wish to communicate, ensure proper routing has been configured and enabled (e.g., Router-on-a-Stick, Layer 3 switch with SVIs). Enable DHCP Relay to allow hosts to contact a DHCP server not in the same VLAN.
* **Incorrect VLAN Assignment:** A common issue is a host being placed in an incorrect VLAN as per its configuration baseline. This means its IP address, subnet mask, default gateway, and DNS servers do not match the expected VLAN assignment to the interface configuration for switch ports (if done manually).
* **Automatic VLAN Assignment Failures:** VLAN assignments configured automatically (e.g., using MAC addresses or authentication credentials) might have failed, or the database used to map the dynamic data to a VLAN ID might be misconfigured.

#### 6. Unresponsive Service and Network Performance Issues

If you can rule out connectivity problems with a local client or subnet, the issue may be with an application server rather than the client. Unresponsive service issues usually manifest with multiple clients being unable to connect.

**Underlying Causes to Consider:**

* **Application/OS Crash:** The application or operating system hosting the service has crashed.
* **Server Overload:** The server hosting the service is overloaded (e.g., high CPU, memory, or disk I/O utilization, insufficient disk space).
* **Network Congestion:** Congestion in the network, either at the client or server end. Use `ping` or `traceroute` to check the latency experienced over the network path and compare it to a network performance baseline.
* **Broadcast Storm:** A broadcast storm is causing a loss of network bandwidth. As this consumes all link bandwidth and can crash network appliances, check for excessive CPU utilization on switches and and hosts (symptom of a storm).
* **DDoS Attack:** Network congestion may also be a sign that the server service is being subjected to a Distributed Denial of Service (DDoS) attack. Look for unusual access patterns (e.g., use GeoIP to graph source IP addresses by country and compare to baseline access patterns).
* **External Service Issue:** Use external tools (e.g., "is it down right now.com") to test whether a LAN/external Internet service connection issue is local to your network or a problem with the service provider's site.
* **Proactive Monitoring:** Be proactive in monitoring service availability to resolve problems before they significantly affect clients.

#### 7. Misconfigured Firewall and ACL Issues

* **Blocked Traffic:** Firewall, ACL, or content filter misconfigurations can cause legitimate service ports or addresses to be blocked.
* **Diagnosis:** A "deny" type of error is usually easy to identify, as users will report incidents related to the failure of specific data traffic.
    * **Confirmation:** Try to establish the connection from both inside and outside the firewall. If a connection is established outside the firewall but not from inside, this confirms the firewall as the cause.
* **Host-based vs. Network-based Firewalls:** Another potential issue is when there are both network-based (e.g., dedicated firewall appliance) and host-based (e.g., Windows Defender Firewall) firewall settings to navigate in the communication path.
    * **Diagnosis:** To diagnose an issue with a host firewall, attempt the connection with it temporarily disabled. If the connection succeeds, then the network-based firewall/ACL is allowing packets, but the host-based firewall is configured to block them. If the connection still fails, investigate the network firewall/ACL first.
* **Firewall Logs:** Always inspect firewall log files to discover what rules have been applied to block traffic at a particular time.

#### 8. BYOD (Bring Your Own Device) Issues

**BYOD** is a smartphone/tablet provisioning model that allows users to select a personal device to interact with corporate network services and cloud applications. Allowing user selection of devices introduces numerous compatibility, support, and security challenges.

* **Mitigation:** The impact of these issues can be mitigated through the use of **Enterprise Mobility Management (EMM)** suites and **Corporate Workspaces**.
    * **EMM:** A type of network access control solution that registers devices as they connect to the network and enforces security policies thereafter.
    * **Corporate Workspace:** An application that is segmented from the rest of the device, allowing more centralized control over corporate data.
* **User Policies:** Users must also agree to acceptable use policies, prohibiting them from installing non-store apps, rooting/jailbreaking a device, and requiring them to keep the device up-to-date with patches. Users may also have to submit to inspection of the device to protect corporate data.

#### 9. Licensed Feature Issues

Licensing for servers and network appliances can be complex, and it's easy to make errors.

* Security and other features may have been configured under a trial or evaluation period and suddenly stop working when that grace period ends.
* **Troubleshooting:** The device's log (or beacon port) should be the starting point for troubleshooting. This should show whether an evaluation/trial period has just expired or when an instance count for a software has been exceeded.
* **Verification:**
    1.  Verify that the appliance has the correct licenses or activation keys installed.
    2.  If relevant, ensure that the appliance can connect to its licensing/activation server.

---

# CHAPTER 18: WIRELESS STANDARD & WIRELESS SECURITY

## Wireless LANs (WLANs) based on IEEE 802.11 Standard (Wi-Fi)

Wireless connectivity is a core feature of most network environments today, primarily because it supports users' need for mobility across various devices. The IEEE 802.11 standard defines the physical layer media by which data is encoded into a radio wave signal using various **modulation schemes**. Modulation changes one or more wave properties to encode a signal. Wi-Fi still uses different carrier methods to provide sufficient resistance to interference from noise and other radio sources.

### Wireless Access and Collision Avoidance

A wireless transmitter (TX) and receiver (RX) operating within a particular range of frequencies with the same modulation scheme constitute a **half-duplex shared access medium**. Unlike wired Ethernet, which uses CSMA/CD (Carrier Sense Multiple Access/Collision Detection), Wi-Fi uses **CSMA/CA (Carrier Sense Multiple Access/Collision Avoidance)** and a virtual carrier sense flow control mechanism to cope with contention and reduce the incidence of collisions.

Rather than detecting collisions after they occur, a wireless station indicates its intent to transmit by broadcasting a **Request to Send (RTS)** signal.

1.  A station (host) broadcasts an **RTS** frame, containing the source, destination, and the time required for transmission.
2.  The receiving station (Access Point - AP) responds with a **Clear to Send (CTS)** signal.
3.  Upon receiving the CTS, the sending station transmits its data. All other stations in range that hear either the RTS or CTS signal do not attempt to transmit within that period, thereby avoiding collisions.

The original 802.11 Wi-Fi standard worked only at 1 Mbps. It has been revised many times, with each iteration specifying different signaling and transmission mechanisms. Products conforming to the various standards can be certified by the Wi-Fi Alliance.

---

### Wi-Fi Standards Evolution (802.11 Generations)

The specific range of radio frequencies a wireless device operates on is referred to as a **channel**, within an overall frequency band of either 2.4 GHz or 5 GHz (and now 6 GHz with Wi-Fi 6E).

### 2.4 GHz Band vs. 5 GHz Band

| Feature                  | 2.4 GHz Band                                                               | 5 GHz Band                                                                                             |
| :----------------------- | :------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| **Propagation** | Better at propagating through solid surfaces, providing a longer signal range. | Less effective at penetrating solid surfaces, resulting in a shorter maximum signal range.               |
| **Channels & Congestion**| Does not support a high number of channels and is often congested (channels overlap considerably). | Supports a higher number of individual channels, suffering less congestion (non-overlapping channels). |
| **Interference & Data Rate** | Increased risk of interference, achievable data rates are typically lower. | Less risk of interference, supports higher data rate transmission at shorter signal ranges.              |

### IEEE 802.11 Generations (Wi-Fi 1 through Wi-Fi 6)

1.  **802.11b (Wi-Fi 1)**:
    * Uses the **2.4 GHz** frequency band.
    * Standardized **Direct Sequence Spread Spectrum (DSSS)** with **Complementary Code Keying (CCK)** signal encoding.
    * Nominal rate of **11 Mbps**.
    * The 2.4 GHz band is subdivided into up to 14 channels (spaced at 5 MHz intervals). Because Wi-Fi needs ~20 MHz channel bandwidth, 802.11b channels **overlap considerably**. This means co-channel interference is a real possibility unless widely spaced channels are chosen (e.g., 1, 6, and 11).

2.  **802.11a (Wi-Fi 2)**:
    * Uses the **5 GHz** frequency band.
    * Uses a multiplexed carrier scheme called **Orthogonal Frequency Division Multiplexing (OFDM)**.
    * Nominal rate of **54 Mbps**.
    * The 5 GHz band is subdivided into many (e.g., 23 non-overlapping) 20 MHz wide channels.
    * Introduced **Dynamic Frequency Selection (DFS)** to prevent APs from interfering with radar and satellite signals. Less likely to suffer co-channel interference due to its wider channel spacing.

3.  **802.11g (Wi-Fi 3)**:
    * An upgrade from 802.11b, operating in the **2.4 GHz** band.
    * Uses **OFDM** (like 802.11a) but with the 2.4 GHz band's channel layout.
    * Nominal data rate of **54 Mbps**.
    * Offers **backward compatibility** for legacy 802.11b clients. When in compatibility mode, it reverts to using DSSS instead of OFDM.

4.  **802.11n (Wi-Fi 4)**:
    * Introduced **Multiple Input Multiple Output (MIMO)** and **Channel Bonding**, significantly increasing bandwidth.
    * **MIMO:** Multiplexes signals from 2 to 4 separate antennas for simultaneous transmission and reception, boosting bandwidth and improving signal reliability. The configuration is identified by `A x B:C` notation (A = #Tx antennas, B = #Rx antennas, C = #simultaneous Tx/Rx streams, max 4x4:4).
    * **Spatial Multiplexing:** Like using multiple highway lanes to transmit/receive data simultaneously.
    * **Spatial Diversity:** Combining signals from multiple antennas to derive a stronger signal and increase range at a given data rate.
    * Can use channels in both **2.4 GHz and 5 GHz** frequency bands.
    * **Channel Bonding:** Allows 2 adjacent 20 MHz channels to be combined into a single 40 MHz channel (a practical option mainly in the 5 GHz band due to less congestion).
    * A **Dual-Band AP** supports both 2.4 GHz and 5 GHz simultaneously.
    * Data rate is 7.2 Mbps per stream, up to **600 Mbps** for a 40 MHz bonded channel with optimal 4x4:4 MIMO configuration.
    * Can operate in **High-Throughput (HT)/Greenfield mode** for maximum performance or **HT Mixed mode** for compatibility with older standards. Greenfield mode can cause substantial interference if legacy WLANs are operating nearby.

5.  **802.11ac (Wi-Fi 5)**:
    * Designed to work **only in the 5 GHz band**. The 2.4 GHz band can be used for legacy standards in mixed mode.
    * Aims to deliver **Very High Throughput (VHT)**, often gigabit Ethernet speeds or better.
    * Supports more channel bonding (e.g., 80 MHz, 160 MHz channels) and up to 8 simultaneous spatial streams with denser modulation at closer ranges.
    * Introduced **Multi-User MIMO (MU-MIMO)** for downlink (AP to client) transmissions.
    * APs are marketed using AC values (e.g., AC5300, indicating total theoretical throughput across bands).

6.  **802.11ax (Wi-Fi 6)**:
    * Uses more complex modulation and signal encoding to improve the amount of data sent per packet by about 40%. Designated as **High Efficiency (HE) Wi-Fi**.
    * Approximate bandwidth of **10 Gigabit speeds**, which can be achieved through the use of the **6 GHz frequency band (Wi-Fi 6E)**.
    * Reinstates operation in the **2.4 GHz band**, mostly to support IoT device connectivity.
    * Introduced **OFDMA (Orthogonal Frequency Division Multiple Access)** modulation scheme, allowing sub-carriers or "tones" to be allocated in groups of different sizes (Resource Units - RUs), each of which can communicate in parallel. RUs can be assigned based on Class of Service (CoS) parameters (e.g., prioritizing VoIP traffic).
        * Large RUs: More bandwidth, fewer devices transmit.
        * Small RUs: Less bandwidth, more devices transmit.
    * **MU-MIMO and OFDMA** are complementary technologies: MU-MIMO makes use of spatial streams, while OFDMA makes flexible use of sub-carriers within a channel. Both can work together to increase parallelism and support communication with more devices simultaneously.
    * **Beamforming (MU-MIMO)**: Like adjusting a spotlight to focus on specific stations (devices) instead of broadcasting signals in all directions. It directs a stronger, more concentrated signal to targeted stations, improving speed and efficiency for multiple client stations.
        * **Downlink (DL) MU-MIMO:** Allows the AP to initiate and use its multiple antennas to process spatial streams of signals in one direction separately to other streams, meaning groups of stations can connect simultaneously and obtain bandwidth.
        * Wi-Fi 5 supports up to 4 stations in parallel over 5 GHz only.
        * Wi-Fi 6 supports up to 8 stations in 2.4 GHz, 5 GHz, and 6 GHz bands.
        * **Uplink (UL) MU-MIMO:** Wi-Fi 6 supports stations initiating beamforming with the AP.

---

### Wireless LAN Fundamentals & Architecture

### Service Sets and SSIDs

* **Service Sets** are groups of wireless devices.
* **SSID (Service Set Identifier)**: A unique network name (up to 32 bytes in length) that identifies a WLAN. For maximum compatibility, it's best to only use ASCII letters, digits, hyphens, and underscores. APs send **Beacon frames** periodically to advertise their SSID.
* **BSSID (Basic Service Set Identifier)**: The MAC address of the Access Point that forms the Basic Service Set. Each BSS has a unique BSSID.

### Wireless Network Topologies

1.  **Independent Basic Service Set (IBSS) / Ad Hoc Mode**:
    * A wireless network where two or more wireless stations connect directly without an AP.
    * Does not require an Access Point.
    * All stations within an Ad Hoc network must be within range of one another.
    * Suits small workgroups, but not scalable for large networks.

2.  **Basic Service Set (BSS) / Infrastructure Mode**:
    * Clients connect to each other via an Access Point.
    * Wireless devices (clients/stations) request to **associate** with the BSS.
    * The area around an AP where its signal is usable is called a **Basic Service Area (BSA)** or Wireless Cell Segment.

3.  **Extended Service Set (ESS)**:
    * Used to create larger Wireless LANs beyond the range of a single AP.
    * Multiple APs, each with its own BSS (and unique BSSID), are connected by a wired network to a switch or Wireless LAN Controller (WLC).
    * Each BSS within an ESS uses the **same SSID** and security configuration.
    * Each BSS uses a **different channel** to avoid interference where their BSAs overlap.
    * **Roaming**: Clients can pass seamlessly between multiple APs in an Extended Service Area (ESA) without having to reconnect, if configured with the same SSID and security. If `802.11r` (fast roaming) is supported, it may use existing authentication status to generate security properties for the new association.
    * The upstream wired network connecting the APs is called the **Distribution System (DS)**.
    * Each wireless BSS or ESS is mapped to a **VLAN** in the wired network.
    * It's possible for an AP to provide **Multiple Wireless LANs**, each with a unique SSID (creating different broadcast domains), and each WLAN can be mapped to a separate VLAN.

4.  **Mesh Basic Service Set (MBSS) / Wireless Mesh Network (WMN)**:
    * Used in situations where it's difficult to run Ethernet connections to every Access Point.
    * Mesh APs use two radios: one to provide a BSS to wireless clients and one to form a "Backhaul Network" for bridging traffic from AP to AP.
    * At least one AP is connected to the wired network and is called the **Root Access Point (RAP)**. Other APs are called **Mesh Access Points (MAPs)**.
    * A routing protocol (e.g., **Hybrid Wireless Mesh Protocol - HWMP**) is used to determine effective paths.
    * Mesh topology is more scalable than ad-hoc because stations do not need to be within direct radio range of one another; transmissions can be relayed by intermediate stations.

### Association Process and Connection States

Wireless clients go through a process to connect to an AP:

* **Management Messages:** Not Authenticated, Not Associated
* **Authentication Request/Response:** Authenticated, Not Associated
* **Association Request/Response:** Authenticated & Associated
* **Data Messages:** Authenticated & Associated

---

### Wireless Deployment Models

There are three main types of Wireless Deployment models: Autonomous, Lightweight (Controller-Based), and Cloud-Based.

1.  **Autonomous APs ("Fat APs")**:
    * Self-contained systems that don't rely on a Wireless LAN Controller (WLC).
    * Each AP is configured individually (IP address for remote management, RF parameters, security policies, QoS rules).
    * Data traffic from wireless clients has a very direct path to the wired network.
    * Best practice to keep management traffic separate (e.g., different subnet/VLAN).
    * Each VLAN has to stretch across the entire network.

2.  **Lightweight APs ("Thin APs") with a Wireless LAN Controller (WLC)**:
    * Not self-contained; functions are split between the AP and a WLC (Split-MAC Architecture).
    * **Thin APs handle "real-time operations"**: Transmitting/receiving traffic, encrypting/decrypting traffic, sending beacons/probes.
    * **WLC handles "management operations"**: RF management, security policies, client association/dissociation, roaming management, QoS management.
    * The WLC can be located in the same subnet/VLAN as the lightweight APs it manages, or in a different subnet.
    * APs and WLCs authenticate each other using digital certificates.
    * They communicate using **CAPWAP (Control and Provisioning of Wireless Access Points)** protocol (UDP port 5246 for control tunnel, UDP port 5247 for data tunnel).
        * **Control Tunnel (UDP 5246):** Used to configure and manage AP operations; traffic is encrypted by default (DTLS - Datagram Transport Layer Security).
        * **Data Tunnel (UDP 5247):** All traffic from wireless clients is sent through this tunnel to the WLC (encapsulated with new headers); it does not go directly to the wired network.
    * **Benefits of Split-MAC Architecture:** Scalability, transmit power optimization, seamless roaming, dynamic channel assignment, client load balancing, self-healing wireless coverage, centralized security/QoS management.

3.  **Cloud-Based AP Architecture**:
    * A hybrid between autonomous APs and split-MAC architecture.
    * Autonomous APs that are centrally managed in the cloud (e.g., Cisco Meraki).
    * A cloud dashboard is used to configure APs, monitor the network, generate performance reports, and control settings like dynamic channel assignment and power optimization.
    * **Data traffic is NOT sent to the cloud**; it goes directly to the wired network (like autonomous APs). Only management (control) traffic and telemetry info are sent to the cloud.

### WLC Deployment Models

* **Unified (Hardware Appliance):** The WLC is a hardware appliance in a central location of the network (good for hundreds of APs).
* **Cloud-Based (VM):** The WLC is a VM running on a server, usually in a private cloud or data center (good for thousands of APs).
* **Embedded:** The WLC is integrated within a switch (good for up to 200 APs).
* **Mobility Express:** The WLC is integrated within an AP (good for up to 100 APs).

---

## Installing Wireless Networks

Designing a wireless network to meet requirements for multiple device types can be complex, ensuring that range and interference issues are accounted for. Wireless network devices are referred to as **stations**.

### Infrastructure Topology

* In an infrastructure topology, each station is configured to connect with a **Base Station or Access Point (AP)**, forming a logical star topology.
* The AP mediates communications between client devices and can also provide a bridge to a cabled network segment.
* The MAC address of the AP is used as the **BSSID**.
* Clients are configured to join a WLAN through the **Network Name or SSID**.
* The area served by a single AP is referred to as a **Basic Service Area (BSA)** or Wireless Cell Segment.
* The area in which stations can roam between APs to stay connected to the same SSID is referred to as an **Extended Service Area (ESA)**.

### SSID Broadcasting

* WLANs are configured to advertise their presence by **broadcasting their SSID**.
* If SSID broadcast is suppressed, user stations must configure the connection to the network manually. However, network sniffers can still detect the SSID even with broadcast disabled.
* A special management frame broadcast by an AP to advertise the WLAN is known as a **Beacon frame**.
* The Beacon frame contains the SSID (unless disabled), supported data rates, signaling, encryption, and authentication requirements.
* The default interval for beacon broadcasts is 100 milliseconds. Increasing this interval reduces overhead but can delay stations joining the network and hamper roaming.

### Site Survey

A **site survey** is a critical planning tool to ensure the WLAN delivers acceptable data rates to the supported number of devices in all expected physical locations.

* A Wi-Fi device usually has an indoor range of at least 30m/100ft. 2.4 GHz radios support better distance ranges than 5 GHz ones, but Wi-Fi 4 (802.11n) and later standards improve range. Outdoor range can be double or triple indoor range.
* Each station determines an appropriate data rate based on signal quality using **Dynamic Rate Switching/Selection (DRS)**. If the signal is strong, the station selects the highest available data rate; otherwise, it lowers the rate.
* Radio signals pass through solid objects but can be weakened or blocked by thick walls (e.g., dense concrete). Other radio-based devices (microwave ovens, heavy machinery, cordless phones) can cause interference.
* **Site Survey Process:**
    1.  Examine blueprints/floor plans to understand the layout and identify features causing RF interference. Back this up with a visual inspection.
    2.  Note locations of available network ports and power jacks for AP mounting. A switch that supports **Power over Ethernet (PoE)** can be used for PoE-compatible APs.
    3.  Create a plan marking WLAN cells, associated APs, and booster antennas. The goal is to place APs close enough to avoid "dead zones" (areas with difficult connectivity or low data rates) but far enough apart to prevent one AP from interfering with another, or from being over/underutilized.
    4.  Position an AP in the first planned location. Use a device with a wireless adapter and a Wi-Fi survey tool (e.g., Cisco Aironet, Ekahau Site Survey, NetAlly, MetaGeek InSSIDer) to record signal strength. Many tools can show signal strength within a particular channel graphically using a **Heat Map** (e.g., strong signal = green, low signal = orange/red).
    5.  This step is repeated for each planned location. Neighboring APs should be configured with **non-overlapping channels** to avoid interference.

### Wireless Roaming and Bridging

* Clients can roam within an **Extended Service Area (ESA)**.
* An ESA is created by installing APs with the same SSID and security configuration, connected by a wired network.
* The APs are configured with different channels to prevent interference where their BSAs overlap.
* If a client station detects a low signal, it checks for another stronger signal with the same SSID on other channels or a different frequency band, then disassociates from the current AP and reassociates with the new AP.
* Depending on the roaming infrastructure and security type, the client might have to re-authenticate. If 802.11r (fast roaming) is supported, it may use existing authentication status.
* Adapters support a "roaming aggressiveness" setting to prevent "flapping" (rapidly switching between two APs) and ensure the station disassociates from a distant, low-bandwidth AP.

### Wireless Distribution System (WDS)

* WDS is a configuration of multiple APs to cover areas where cabling is impossible.
* APs are configured in **WDS/Repeater mode**. One AP is configured as a **Base Station** (connected to a cabled segment), while others are configured as **Remote Stations**.
* Remote stations don't need to be connected to cable segments but can accept connections from wireless stations and forward all traffic to the base station.
* Another use of WDS is **bridging two separate cable segments**. When WDS is configured in **Bridge Mode**, the APs will not support wireless clients; they simply forward traffic between cabled segments. Best to use APs from the same vendor.

---

## Wireless Configuration via GUI/CLI

### WLAN Controller (WLC) Connectivity

* The WLC connects to a switch via a **Link Aggregation Group (LAG)** (also known as EtherChannel). WLCs often only support static LAG, not PAgP or LACP.
* **DHCP Option 43** can be used to tell APs the IP address of their WLC.

### WLC Ports and Interfaces

* **WLC Ports** are the physical ports that cables connect to.
* **WLC Interfaces** are the logical interfaces within the WLC (similar to SVIs on a switch).

1.  **Service Port:** A dedicated management port used for **out-of-band management**. Must connect to a switch access port as it only supports one VLAN. Used to connect to the device while it is booting.
2.  **Distribution System (DS) Ports:** Standard network ports that connect to the **Distribution System (wired network)** and are used for data traffic. These ports usually connect to switch trunk ports. If multiple, they can form a LAG.
3.  **Console Port:** Standard console port, using either RJ-45 or USB.
4.  **Redundancy Port:** Used to connect to another WLC to form a **High Availability (HA) pair** (one active, one standby).
5.  **Management Interface:** Used for management traffic such as Telnet, SSH, HTTP, HTTPS, RADIUS authentication, NTP, syslog, etc. CAPWAP tunnels are also formed from the WLC management interface.
6.  **Redundancy Management Interface:** When two WLCs are connected by their redundancy ports, this interface can be used to connect to and manage the "standby" WLC.
7.  **Virtual Interface:** This interface is used when communicating with wireless clients, relaying DHCP requests, performing client web authentication, etc. It's a logical interface that doesn't map directly to a physical port.
8.  **Service Port Interface:** If the service port is in use, this logical interface is bound to it.
9.  **Dynamic Interface:** These are the interfaces used to map a VLAN to a WLAN (i.e., a specific SSID).

---

---

## WIRELESS NETWORK SECURITY

Wireless networks, while offering mobility and convenience, pose considerable security risks if not properly secured with access controls. All clients must be authenticated before they can associate with an Access Point (AP). In corporate settings, a separate SSID (Service Set Identifier) with restricted access can be provided for guest Internet access, keeping them off the main corporate network.

### Authentication Methods

Here are multiple ways to authenticate clients on a wireless network, broadly categorized by their approach:

* **Open Authentication:** No authentication is performed by the AP. Often used in conjunction with a **Captive Portal** (web page requiring credentials or agreement to terms) for guest access or public Wi-Fi.
* **Wired Equivalent Privacy (WEP):** (Legacy and insecure) An older standard aiming to provide both authentication and encryption.
* **Extensible Authentication Protocol (EAP):** A framework that defines a set of standardized authentication methods, widely used in modern wireless security.
    * **EAP over LAN (EAPOL):** Used for wired port-based network access control (IEEE 802.1X).
    * **EAP over Wireless (EAPOW):** Used for wireless port-based network access control (IEEE 802.1X).
* **Lightweight EAP (LEAP):** Cisco-developed, an improvement over WEP.
* **Protected EAP (PEAP):** Establishes a secure TLS tunnel.
* **EAP-FAST (Flexible Authentication via Secure Tunneling):** Cisco-developed, similar to PEAP but uses Protected Access Credentials (PACs).
* **EAP-TLS (Transport Layer Security):** The most secure EAP method, requiring certificates on both the client and server.

### Extensible Authentication Protocol (EAP) Framework

EAP is an authentication protocol that defines a set of standards. It's integrated with **IEEE 802.1X** (Port-based Network Access Control - PNAC), which is used to limit network access for clients until they authenticate.

**Three Main EAP Entities:**

1.  **Supplicant:** The end-host (client device) seeking network access.
2.  **Authenticator:** The network access device (e.g., switch, router, Access Point, WLC) that restricts access and forwards authentication requests.
3.  **Authentication Server / AAA Server / RADIUS / TACACS+:** The server that performs the actual authentication logic.

### WEP (Wired Equivalent Privacy)

* An older security protocol designed to provide both authentication and encryption for WLANs.
* Uses the **RC4 stream cipher**.
* It's a shared-key protocol, meaning clients connect using a pre-shared key.
* WEP keys are typically **40-bit or 104-bit** in length.
* The WEP key is combined with a **24-bit Initialization Vector (IV)** for encryption.
* **WEP encryption is not secure** due to vulnerabilities in the RC4 key scheduling algorithm and the fixed IV.
* **Authentication in WEP** was based on a simple challenge-response (Challenge-Handshake Authentication Protocol - CHAP), which is also insecure.

### Lightweight Extensible Authentication Protocol (LEAP)

* Developed by Cisco as an improvement over WEP.
* Clients must provide a username/password to authenticate.
* **Mutual authentication** is provided, where both the client and server send challenge phrases to each other.
* Uses **dynamic WEP keys** that are changed frequently to mitigate some WEP vulnerabilities. Still not considered highly secure.

### Protected Extensible Authentication Protocol (PEAP)

* Like EAP-FAST, PEAP involves establishing a **secure TLS tunnel** between the client and the authentication server.
* The server's digital certificate is used to authenticate the server to the client and to establish the TLS tunnel.
* The client is then authenticated to the server using a less secure method (e.g., **MS-CHAPv2**) *within the protected tunnel*.
* PEAP requires the authentication server to have a digital certificate.

### EAP-FAST (Flexible Authentication via Secure Tunneling)

* Developed by Cisco, often consists of three phases:
    1.  **PAC (Protected Access Credential) Provisioning:** A secure credential (PAC) is securely provisioned to the client.
    2.  **Secure TLS Tunnel Establishment:** A secure TLS tunnel is established using the PAC.
    3.  **Further Communication within Secure Tunnel:** Further authentication or communication takes place within the established tunnel.
* Unlike PEAP, EAP-FAST does not require the authentication server to have a digital certificate (though it can use one). It primarily relies on PACs for mutual authentication.

### EAP-TLS (Transport Layer Security)

* Requires **both the client and the server to have digital certificates**. This makes it the most secure authentication method, but also the most difficult to implement due to the certificate management overhead (every client device needs a certificate).
* The TLS tunnel is used for key information exchange, but no further authentication is needed within the tunnel because both parties are already authenticated by their certificates.

### Temporal Key Integrity Protocol (TKIP) and Counter Mode with Cipher Block Chaining Message Authentication Code (CCMP)

These are cryptographic protocols used for encryption and integrity in modern wireless security:

* **TKIP (Temporal Key Integrity Protocol):**
    * Used in WPA.
    * Combines the RC4 cipher with enhancements designed to address WEP vulnerabilities (e.g., per-packet keying, message integrity check - MIC).
    * Still uses RC4, making it susceptible to some attacks, and is considered less secure than AES.
* **CCMP (Counter Mode with Cipher Block Chaining Message Authentication Code Protocol):**
    * Used in WPA2.
    * Combines the **AES (Advanced Encryption Standard) cipher** in Counter Mode (CTR) with **CBC-MAC (Cipher Block Chaining Message Authentication Code)** for data integrity and authentication.
    * Replaced TKIP for stronger security.
* **GCMP (Galois/Counter Mode Protocol):**
    * Used in WPA3.
    * Combines **AES** in Galois/Counter Mode for both encryption and authentication. Offers better performance and stronger security than CCMP.

---

## WIRELESS PROTECTED ACCESS (WPA, WPA2, WPA3)

The choice of security settings depends on device support for various Wi-Fi encryption standards, the type of authentication infrastructure, and the purpose of the WLAN. These standards determine the cryptographic protocols supported, key generation methods, and available authentication methods.

### WPA (Wi-Fi Protected Access) - Version 1

* Designed to counter vulnerabilities in the WEP standard.
* Like WEP, WPA uses the **RC4 stream cipher** to encrypt traffic.
* It adds **TKIP (Temporal Key Integrity Protocol)** to mitigate attacks against WEP. TKIP provides per-packet keying, message integrity checks (MIC), and rekeying, making replay attacks harder than with WEP.
* **Vulnerable to some replay attacks** that aim to recover the encryption key, as it still uses RC4.

### WPA2 (Wi-Fi Protected Access II)

* **Uses Advanced Encryption Standard (AES)** cipher deployed within the **CCMP (Counter Mode with Cipher Block Chaining Message Authentication Code Protocol)**.
* **AES replaces RC4**, and **CCMP replaces TKIP**.
* CCMP provides both authentication and encryption, designed to make replay attacks much harder.
* WPA2 is generally considered secure.
* **Protected Management Frames (PMF)** are an optional feature in WPA2, made mandatory in WPA3, to protect critical management frames from spoofing and denial-of-service attacks.

### WPA3 (Wi-Fi Protected Access III)

* Uses the **same AES and GCMP** as WPA2.
* However, the method by which session keys are agreed upon changes from the WPA2 4-way handshake to **SAE (Simultaneous Authentication of Equals)**.
* **SAE** (also referred to as Password Authenticated Key Exchange - PAKE) provides stronger protection against dictionary attacks and ensures forward secrecy.

### WPA Modes: Personal vs. Enterprise

Wireless security comes in two main flavors (and an "Open" category):

1.  **Personal (Pre-Shared Key - PSK / SAE):**
    * Also known as **WPA2-Personal** (WPA2-PSK) or **WPA3-Personal** (WPA3-SAE).
    * Uses a passphrase to generate the key that is used to encrypt communications.
    * Referred to as **group authentication** because all users share the same secret.
    * The administrator configures a passphrase (8-63 characters, 64 hex characters). This is converted to a hash value, known as the **Pairwise Master Key (PMK)**.
    * The PMK is used as part of the WPA2 4-way handshake or WPA3 SAE to derive various session keys.
    * **WPA2-PSK is vulnerable to dictionary attacks** if a weak passphrase is used, as the 4-way handshake can be captured offline and brute-forced.
    * **WPA3-Personal (SAE)** changes the key agreement method to mitigate these dictionary attacks. It provides a more robust and secure key exchange, even with weak passwords.
    * An AP can be configured for WPA3-only or with support for legacy WPA2, known as **WPA3-Personal Transition Mode**.

2.  **Enterprise (IEEE 802.1X Authentication for WPA2 or WPA3):**
    * Also known as **WPA2-Enterprise** or **WPA3-Enterprise**.
    * Addresses the limitations of the Personal model (e.g., distribution of keys, lack of accounting).
    * Implements **IEEE 802.1X** to use an **Extensible Authentication Protocol (EAP)** to authenticate against a network directory (e.g., RADIUS server, Active Directory).
    * 802.1X defines the use of **EAP over Wireless (EAPOW)** to allow an AP to forward authentication data without allowing any other type of network access initially.
    * **Authentication Process:**
        1.  When a wireless client requests an association, the AP enables the channel only for EAPOW traffic.
        2.  The AP passes the credentials of the Supplicant to an **AAA Server** on the wired network for validation.
        3.  When the Supplicant has been authenticated, the AAA server transmits a **Master Key** back to the Supplicant, with which both the client and AP derive the same **Pairwise Master Key (PMK)**.
        4.  The wireless station and AP use the PMK to derive session keys, using either the WPA2 4-way handshake or the WPA3 Simultaneous Authentication of Equals method.
    * Provides centralized authentication, authorization, and accounting (AAA).


## Troubleshooting Wireless Networks

Wireless network deployments can be complicated by various environmental and performance demands. A variety of tools and techniques are available to assess Wi-Fi performance and ensure a highly available network for all users.

Wireless issues can be broadly categorized into problems with:
1.  **Signal Strength / Interference**
2.  **Configuration Issues** (especially security and authentication)
3.  **Differences in Speed and Throughput**

### Wireless Performance Metrics

* **Speed (Data Rate):** The data rate established at the Physical Layer (Layer 1) and Data Link Layer (Layer 2).
    * Determined by Wi-Fi standards used (e.g., 802.11n, ac, ax), bonded channels, and optimization techniques such as MU-MIMO.
    * If sender and receiver are far apart or subject to interference, a lower data rate is negotiated to make the link reliable.
* **Throughput:** The amount of data that can be transferred at the Network Layer (Layer 3), discarding overhead from Layers 1 and 2.
    * Often used to describe the actual data transfer achieved at the Application Layer, accounting for packet loss and retransmissions.

### 1. Signal Issues

* **Attenuation:** The weakening of the signal as the distance between the station and the access point (AP) increases. Also referred to as **Radio Frequency (RF) Attenuation** or **Free Space Loss**.
    * As the distance from the antenna increases, the strength of the signal decreases in accordance with the **Inverse-Square Law**.
* **Interference:** Various interference sources collectively overlay a competing background signal, creating noise.
* **Measurement Units (dBm):** Attenuation and signal strength are measured in decibels (dB). Signal strength is represented as a ratio of a measurement to 1 milliwatt (mW).
    * `0 dBm = 1 mW`.
    * **dBm** is a unit of level used to indicate that a power ratio is expressed in decibels with reference to 1 milliwatt. It's convenient for expressing both large and small values concisely.
    * Formula: `Power (dBm) = 10 * log10 (Power (mW) / 1 mW)`
    * If `Power (mW) = 1 mW`, `Power (dBm) = 0 dBm`.
    * To convert back to milliwatts: `Power (mW) = 10^(Power (dBm) / 10)`
    * A negative dBm value represents a fraction of a milliwatt (e.g., `-3 dBm` is half a milliwatt). Positive values represent power more than 1 mW.
    * The conversion is logarithmic: every increase/decrease of 3 dBm equates to a doubling/halving of power. Every increase/decrease of 10 dBm equates to a tenfold increase/decrease in power.

* **Received Signal Strength Indicator (RSSI):** The strength of the signal from the transmitting station at the client end.
    * When measuring RSSI in dBm, it will be a negative value (a fraction of a milliwatt), with **values closer to zero representing better performance** (e.g., `-65 dBm` is better performance than `-80 dBm`).
    * An RSSI of `-80 dBm` to `-90 dBm` is likely to suffer packet loss or be dropped entirely.
    * The RSSI must exceed the **minimum receiver sensitivity** of the client adapter.
    * RSSI can also be an index value related to a scale of raw measurements (e.g., 0-60, 0-127, or 0-255). On a client, this index is often displayed as a number of "bars" on the adapter icon.

* **Signal-to-Noise Ratio (SNR):** The comparative strength of the data signal to the background noise.
    * Noise is also measured in dBm, but here, values closer to zero are less desirable as they represent higher noise levels.
    * RSSI and SNR can be measured using a **Wi-Fi analyzer** installed on an adapter or a dedicated spectrum analyzer.

### Antennas

* Antennas determine the propagation pattern (shape of radio waves transmitted/received).
* **Omnidirectional Antennas:**
    * Send and receive signals in all directions (radiate more equally).
    * The propagation pattern is shaped like a donut, radiating more powerfully in the horizontal plane than in the vertical plane.
    * Generally used for broader coverage areas.
* **Unidirectional (Directional) Antennas:**
    * Focus the signal in a particular direction.
    * Increase in signal strength obtained by focusing the signal is referred to as **Gain**, measured in **dBi (decibels isotropic)**.
    * Both sender and receiver must use directional antennas for point-to-point wireless links.
    * Examples: Yagi, parabolic grid (very highly directional for long connections).
    * **Beamwidth:** Measured in degrees, representing the angle of the main lobe of radiation. Omni-directional antennas have a wider beamwidth (e.g., 360° horizontal), while directional antennas have narrower beamwidths (e.g., 10°, 90°).

* **Polarization:** Refers to the orientation of the wave propagating from the antenna (e.g., vertical, horizontal).
    * To maximize signal strength, the transmitting (Tx) antenna and receiving (Rx) antenna should normally use the same polarization. This is particularly important when deploying unidirectional antennas for point-to-point links.
    * Some antennas are **dual-polarized**, meaning they can be installed in either orientation or support both simultaneously. Dual-polarized antennas are often best to support mobile devices, as these can be held by their user in a variety of orientations.

* **Insufficient Wireless Coverage (Dead Spots):**
    * Refers to spots within a building with no or weak Wi-Fi signal.
    * If sufficient signal strength cannot be obtained or interference cannot be mitigated, the only solution is to install additional APs to cover the gap.
    * If you cannot extend the cabled distribution network system to support additional APs, you will need to configure a wireless bridge or use a **range extender** (which extends two separate cabled segments wirelessly).

* **Antenna Placement:**
    * Incorrect antenna placement can cause or worsen attenuation and interference problems.
    * Use a **site survey** and **heat map** to determine the optimum position for APs and the direction in which to point adjustable antennas.
    * Using an incorrect antenna type can adversely affect signal strength (e.g., an AP designed for ceiling mounting produces a stronger signal directed downwards, whereas a wall-mounted AP's signal is angled outwards).

* **Antenna Cable Attenuation:**
    * Signal loss occurs when an antenna is connected at some distance from the access point via coaxial cabling.
    * Higher quality cable (e.g., LMR/HDF/CFD 400 series at approx. 0.22 dB/meter) has less attenuation than lower quality (e.g., LMR/HDF/CFD 200 series at approx. 0.6 dB/meter).
    * Connector loss (e.g., 0.15 dB per connector) is also calculated.
    * For devices with removable antennas, a loose or disconnected antenna will significantly reduce range and connectivity.

* **Effective Isotropic Radiated Power (EIRP) & Power Settings:**
    * **EIRP** is the total power radiated from the antenna, accounting for transmission power, antenna gain, and cable/connector losses.
    * `EIRP = Transmit Power (dBm) + Antenna Gain (dBi) - Cable/Connector Losses (dB)`
    * This value for each radio is reported through the AP or controller management software.
    * **Regulatory Limits:** Power limits must not exceed regulatory limits, which differ for 2.4 GHz and 5 GHz bands and for point-to-point versus point-to-multipoint operation modes.
    * **Ineffectiveness of High Power:** Increasing transmit power is not usually an effective solution to improve wireless coverage. If the client station detects a strong signal, it will set a high data rate. However, because the EIRP of the client radio is typically much lower, it fails to transmit a strong signal back to the AP, resulting in excessive packet errors (the "AP can hear the client, but the client can't hear the AP" problem).
    * **Rule of Thumb:** AP power should be roughly 4/3rds of the weakest client radio power. For example, if the weakest client can output 12 dBm, the AP should transmit at 9-10 dBm.

### Channel Utilization and Overlap Issues

* **Channel Overlap:** Refers to interference resulting from multiple access points that are all in range of one another and are configured to use similar RF wavelengths (channels).
* **Co-Channel Interference (CCI):**
    * Accurately described as contention for an RF channel when multiple access points use the same channel. Opportunities to transmit are reduced.
    * Wireless stations must then use **CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)** to find transmit opportunities.
    * CCI is measured as a percentage referred to as **channel utilization** using a Wi-Fi analyzer.
    * **Design Goal:** A channel should exhibit no more than 50% utilization for optimal performance.
* **Adjacent Channel Interference (ACI):**
    * Occurs when access points are configured to different but **overlapping channels**, such as channels 1 and 3 in the 2.4 GHz band.
    * ACI slows down the CSMA/CA process and raises noise levels.

**Channel Planning:**

* One of the design goals for a multi-AP site is to create "clean cells" so that clients can select an AP with the strongest signal easily and the Wi-Fi operates with a minimum of co-channel interference.
* In the 2.4 GHz band, there are only 3 non-overlapping channels (1, 6, 11). For example, select channel 1 for APx, channel 6 for APy, and channel 11 for APz.
* In the 5 GHz band (for 802.11a/n/ac/ax), more non-overlapping channels are available, and channels are generally wider (e.g., 20MHz, 40MHz, 80MHz, 160MHz). At least 25 MHz channel spans should be allowed to avoid channel overlap in the 5 GHz band.
* **Power Level Adjustment:** Adjusting the power level used by an AP on a given channel is advantageous. Using the maximum available power on an AP can result in interfering with other cells and situations where a client can "hear" the AP but cannot "talk" to it because it lacks sufficient power (as discussed in EIRP).
* **Roaming:** In order to enable seamless roaming for mobile clients, the cells or Basic Service Areas (BSAs) served by each AP need to overlap to some extent. Issues with roaming can be identified by analyzing access point association times for clients. A WLAN Controller will track client mobility, showing each AP and the time the client associated with it. A large number of clients "flapping" (repeatedly associating and disassociating) between two APs indicates a roaming issue.

### Overload Capacity / Client Saturation

* **Client Saturation:** Occurs when too many client stations connect to an AP, causing performance degradation.
* The maximum number of clients an AP can support varies depending on the Wi-Fi standard used and the type of network traffic generated. A maximum of 30 clients per AP is a generally accepted rule of thumb.
* **Design Goal:** Enough APs should be provided in appropriate locations to support the expected client density at this ratio.
* APs can be configured to enforce a maximum number of connections; additional clients will then connect to the nearest available AP.
* Even with a low number of clients, wireless networks can suffer from bandwidth saturation because it's a broadcast medium, meaning the available bandwidth is shared among all clients.
* A **Wireless LAN Controller** will normally provide reporting tools to manage and diagnose bandwidth issues, report on wireless channel utilization, and configure APs and clients to reassign channels dynamically to reduce over-utilization.
* If a **Traffic Shaper** is deployed, it may work automatically to throttle bandwidth to over-utilized clients.

### Environmental Factors Causing Weak Signal / No Connection

If a device is within the supported range but the signal is weak or there's no connection, interference or physical obstructions are likely.

1.  **Reflection / Bounce (Multipath Interference):**
    * Mirrors, metal surfaces, and other solid objects cause signals to reflect, meaning that a variable delay is introduced, causing packet loss and data rate decrease.
    * However, Wi-Fi 4/5/6 (802.11n/ac/ax) standards use multipath (via **MIMO**) as a means of optimizing throughput and range.
2.  **Refraction:** Glass or water (e.g., fish tanks) can cause radio waves to bend and take a different path to the receiver radio, causing signal distortion.
3.  **Absorption:** The degree to which solid materials reduce signal strength as the wave's energy is lost as heat when passing through construction materials.
    * The 2.4 GHz band generally has better penetration through objects than the 5 GHz band.
    * Ceiling-mounted APs are often favored to minimize absorption from office furniture.
    * An internal wall might cause 3-7 dBm of absorption.
4.  **Electromagnetic Interference (EMI):**
    * Interference from other powerful radio or electromagnetic sources working in the same frequency band (e.g., microwaves, cordless phones, Bluetooth devices, industrial equipment).
    * Detected using a **Spectrum Analyzer**. This specialized radio receiver filters out anything that isn't a Wi-Fi signal.
    * Usually supplied as handheld units with a directional antenna, so the exact location of the interference can be pinpointed.
    * A 6 dBm change in the level of a particular source reflects a halving/doubling of the distance between the analyzer and the source of the RF interference.

---

## 2. Wi-Fi Security Configuration Issues

### Wrong SSID and Incorrect Passphrase Issues

* **SSID (Service Set Identifier):** The network name. If the SSID is suppressed (hidden), clients must connect to the AP/WLAN by entering the network name manually.
* **Troubleshooting:**
    * Ensure clients are configured to transmit the correct SSID. Remember that the value is case-sensitive.
    * Check authentication settings are the same on all devices (client and AP).
    * If a passphrase is used (e.g., WPA2-Personal), ensure it is entered correctly.
    * Unless the WLAN is meant to provide public, unrestricted access, **do not set the authentication type to "Open"**.
    * It's possible that two APs are operating with the same SSID. If authentication is wrong, connection to the wrong SSID will fail.
    * If a user is joining the WLAN for the first time, there might be SSIDs from overlapping WLANs with very similar default names, leading to user confusion about which to choose.

### Encryption Protocol Mismatch Issues

* If the user is definitely supplying the correct key or credentials, check that the client can support the encryption and authentication standards configured on the AP.
* A device update or OS patch may be required for the client.
* Even if the credentials are supplied correctly, a connection will fail if the encryption protocol (e.g., WPA2 AES vs. WPA3) is mismatched.

### Client Disassociation Issues

* Access points and client stations normally use management frames to control connections.
* Using **beacon frames**, clients can choose to authenticate if they are in range of an AP's Basic Service Area (BSA).
* The client or AP can use **Disassociation** or **Deauthentication** frames to notify the other party about a connection ending.
* A legitimate client might disassociate but not deauthenticate because it's roaming to another wireless AP within an Extended Service Area (ESA).
* **Troubleshooting:** Investigate the AP or WLAN Controller event log to identify the cause of disassociations, especially if clients are found "flapping" between access points (indicating a roaming issue).
* If clients are disassociated unexpectedly and there is no roaming involved, consider interference or driver issues.
* **Malicious Attacks:** Also consider the possibility of a malicious attack.
    * **Disassociation Attack:** Exploits the lack of encryption on management frame traffic to send spoofed frames.
        * One type rejects management frames that spoof the MAC address of a single victim station in a disassociation notification, causing it to be disconnected from the network.
        * Another variant broadcasts spoofed frames to disconnect all client stations.
    * Disassociation and Deauthentication attacks are used to perform Denial of Service (DoS) against the wireless infrastructure or to exploit disconnected stations to try to force reconnection to a rogue AP ("Evil Twin"). They are also used in conjunction with a replay attack aimed at recovering the network key (e.g., cracking WPA/WPA2-Personal PSK).

### Open Authentication and Captive Portal Issues

* **Open Authentication** may be combined with a secondary authentication mechanism managed by a browser.
* When a client station associates with an Open AP (e.g., a hotspot) and launches the browser, the client is redirected to a **Captive Portal** (a "splash page"). This portal allows the client to authenticate to the hotspot provider's network (often over HTTPS, so the login is secure). Such portals may enforce terms and conditions or take payment.
* **Common Issues:** Most captive portal issues arise because the redirect does not work.
    * Modern browsers will block redirection to sites that do not use TLS/SSL. This means the portal itself needs to be installed with a digital certificate issued by a CA that is trusted by the client's browser.
* **Security Concern:** When using open wireless, data sent over the link is unencrypted. Users must ensure they:
    * Send confidential web data only over HTTPS connections.
    * Only use email, VoIP, and file transfer services with SSH/TLS enabled.
    * Another option for users is to force a VPN connection. The VPN must use certificate-based tunneling to set up the inner authenticated method for encrypting traffic over the untrusted network.

### Wireless Security Protocols (Evolution and Vulnerabilities)

* **WEP (Wired Equivalent Privacy):**
    * **Weaknesses:** Uses an RC4 cipher and a static key. Vulnerable to various replay attacks (e.g., IV attacks). Easy to crack. **Deprecated.**
* **WPA (Wi-Fi Protected Access) 1:**
    * **Improvements:** Uses RC4 cipher but introduces **TKIP (Temporal Key Integrity Protocol)** to mitigate replay attacks by dynamically changing session keys. Still vulnerable to some attacks.
* **WPA2 (Wi-Fi Protected Access) (Current Standard for most deployments):**
    * **Improvements:** Uses **AES-CCMP (Advanced Encryption Standard - Counter Mode with Cipher Block Chaining Message Authentication Code Protocol)** for stronger encryption. Offers two modes:
        * **WPA2-Personal (PSK - Pre-Shared Key):** Uses a passphrase for authentication. Suitable for home/small office. Vulnerable to dictionary attacks if the PSK is weak.
        * **WPA2-Enterprise:** Uses **EAP (Extensible Authentication Protocol)** to authenticate users via an **AAA (Authentication, Authorization, Accounting) server** (e.g., RADIUS, TACACS+). A unique Pairwise Master Key (PMK) is derived after authentication. Provides much stronger security, suitable for corporate environments.
* **WPA3 (Wi-Fi Protected Access 3) (Latest Standard):**
    * **Improvements:** Uses **AES-GCMP** (GCM-based encryption). Introduces **SAE (Simultaneous Authentication of Equals)** handshake to mitigate dictionary attacks against the pre-shared key. Provides **Protected Management Frames (PMF)** to protect management traffic from spoofing/disassociation attacks.
    * **WPA3-Personal:** Stronger than WPA2-Personal.
    * **WPA3-Enterprise:** Adds 192-bit encryption for sensitive data.

---
## 3. Configuring and Troubleshooting Wireless Security

Wireless connections pose considerable risks unless properly secured with access controls. Identifying different wireless security methods, their configuration requirements, and troubleshooting common issues is crucial.

**General Considerations:**

* **Signal Strength vs. Security:** Strong signal does not equate to strong security.
* **Interference:** Other wireless devices or even physical objects can interfere with Wi-Fi signals, impacting performance and potentially security.
* **Rogue APs:** Unauthorized APs on the network can pose a significant security threat.
* **Client Compatibility:** Ensure that all client devices support the chosen security standard (e.g., WPA3-only networks will not allow WPA2-only clients).

**Troubleshooting Common Wireless Issues:**

* **Connectivity Issues:**
    * Incorrect SSID.
    * Incorrect passphrase/security key.
    * Outdated wireless adapter drivers.
    * Channel interference (check channel settings on AP and surrounding networks).
    * AP too far away (weak signal).
    * Client device not supporting the chosen Wi-Fi standard or security protocol.
* **Authentication Failures:**
    * Incorrect username/password (for Enterprise modes).
    * Misconfigured RADIUS server.
    * Client certificates expired or misconfigured (for EAP-TLS).
    * Time synchronization issues between client, AP, and authentication server.
* **Performance Issues:**
    * Co-channel interference (multiple APs on the same channel in proximity).
    * Adjacent channel interference (overlapping channels, especially in 2.4 GHz).
    * Legacy devices forcing the network into backward compatibility modes.
    * Too many clients on one AP.
    * Weak signal requiring lower data rates (DRS).
    * Firmware issues on AP or client.


## Guidelines for Deploying and Troubleshooting Wireless Networks

Following these guidelines will lead to more robust and easily manageable wireless networks.

1.  **Define Requirements:** Create a clear list of requirements (e.g., number of users, physical service area to cover, external connectivity needs).
2.  **Consider Client Compatibility:** Consider the client devices you need to support and their compatibility requirements in terms of Wi-Fi standards (e.g., 802.11a/b/g, Wi-Fi 4/5/6).
3.  **Site Survey and Heat Maps:**
    * Obtain a blueprint or layout of the building.
    * Use a **Wi-Fi Analyzer** to perform a **site survey** and generate **heat maps** of signal strength and channel utilization. This helps to mitigate dead zones and co-channel/adjacent channel interference.
4.  **Determine AP Range:** Based on the chosen Wi-Fi technology, determine the effective range of the AP. This will help you better determine how many APs you will need to ensure adequate coverage for the space.
5.  **Balance Client Density:** Balance the number of users who will have access to each AP. Ensure that the APs cover all required employees within their range, while also considering client capacity limits.
6.  **Interference Check:** Tour the area within the range of the AP and check for any devices that will interfere with the wireless network (e.g., microwaves, cordless phones).
7.  **Obstacle Clearance:** Ensure that there are no significant obstacles (e.g., metal, water, thick walls) in the path of the AP that could obstruct the wireless signal.
8.  **AP Installation Steps (Vendor Specific but Common):**
    * Connect the AP to the cabled network / distribution network (via a switch, often with PoE).
    * Set the **SSID/ESSID** and an `802.11` beacon.
    * Configure frequency bands (2.4 GHz, 5 GHz) and channel layout within each frequency band (e.g., 1, 6, 11 for 2.4 GHz).
    * Adjust transmit power to reduce channel overlap and excessive packet loss errors (find the right balance for cell size).
    * Configure the appropriate **encryption and authentication scheme** (e.g., WPA2/WPA3 Personal vs. WPA2/WPA3 Enterprise).
    * If appropriate (for Enterprise mode), configure RADIUS and/or TACACS+ support for enterprise authentication.
9.  **Real-World Testing:** Test the installation under real-world conditions to confirm it is appropriately sized, secure, and operational.
10. **Periodic Site Surveys and Documentation:**
    * Perform periodic site surveys to check RSSI at key locations and compare to previous performance levels.
    * **Document every step** and establish a baseline for future installations and troubleshooting.


Let's break down network types, characteristics, topology, and how they relate to performance, cabling, switching, and routing within the OSI model.

---

# CHAPTER 19: SOFTWARE DEFINED NETWORKING

## SOFTWARE-DEFINED WIDE AREA NETWORKING (SD-WAN)

Traditional hub-and-spoke WAN designs with on-premises data centers often suffer from performance and reliability drawbacks. While moving services to cloud data centers or using colocation mitigates some issues by separating service integrity and availability from site accessibility, a new approach is needed for modern connectivity demands.

**SD-WAN replaces the traditional hub-and-spoke design with more efficient, secure connectivity to corporate clouds, often at a lower expense compared to provisioning MPLS services to every remote location.**

### Key Characteristics of SD-WAN

* **Overlay Network:** An SD-WAN is a type of overlay network. This means it creates a logical network on top of existing physical "underlay" networks.
* **Multi-Location Access:** It provisions corporate WAN access across multiple locations (branch offices, remote worker locations, data centers).
* **Direct Cloud Access:** Facilitates secure, direct access to cloud services from a branch office or other remote location, bypassing the need to backhaul traffic through a central hub.
* **Automation & Orchestration:** SD-WAN uses automation and orchestration to dynamically provision links based on application requirements and network congestion.
* **Secure Tunnels:** It typically uses **IPsec** (Internet Protocol Security) to ensure that traffic is tunneled securely through the underlying transport networks.
* **Micro-segmentation & Zero Trust:** An SD-WAN solution should apply micro-segmentation and zero-trust policies to ensure all requests and responses are authenticated and authorized, even for internal traffic.

### SD-WAN Architecture and Operation

The SD-WAN is managed by a **Controller and management software**, which can be located in the corporate data center or a public cloud.

* **SD-WAN Capable Devices:** Each site (branch, data center) has an SD-WAN capable router, gateway, or VPN application.
* **Controller Orchestration:** The SD-WAN Controller orchestrates connections to networks and clouds enrolled in the SD-WAN.
* **Underlay Network Agnostic:** It utilizes *any available IP underlay network*, such as broadband Internet, 4G/5G cellular, or private MPLS VPNs, to provision the fastest or most reliable available transport.
* **Authentication and Authorization:** The Controller also ensures that access requests are authenticated and authorized, reinforcing the security posture.

---

## DATA CENTER NETWORK DESIGN

A data center is a site dedicated to provisioning server resources. It hosts network services (authentication, addressing, name resolution), application servers, and storage area networks (SANs). While many are purpose-built facilities, some concepts apply to on-premises server rooms.

### Evolution of Data Center Design

* **No Client PCs:** Unlike a corporate network, a data center contains no client PCs, other than hardened, secure administrative workstations (SAWs) used solely to manage servers.
* **Traditional Three-Tiered Design (Legacy):** Historically, data centers were designed using the same three-tiered model as an enterprise campus network, with core, distribution, and access layer switches.
* **Shift to East-West Traffic:** The changing way applications are designed (as services, using virtualization and on-demand instances) has dramatically changed the nature of traffic flows.
    * **North-South Traffic:** Traditional traffic flow between clients and servers, often passing through a central firewall.
    * **East-West Traffic:** Predominant traffic flow **between servers** within the data center (e.g., microservices communicating, virtual machines talking to each other).
* **Security Challenges with East-West Traffic:** The preponderance of East-West traffic complicates security design. If each of these cascading transactions were to pass through a central firewall/security appliance, it would create a severe security bottleneck.
* **Virtualized Security & Zero Trust:** These requirements drive the creation of **virtualized security appliances** that can monitor traffic flowing between servers. Simultaneously, security implementations are moving towards a **Zero Trust design**, implying a highly segmented network where each link between servers must be authenticated and authorized.

### Overlay Networks in Data Centers

* An **overlay network** is used to implement this type of point-to-point logical link between nodes or networks, abstracting the complexity of the underlying physical topology.
* It uses **encapsulation protocols** and **Software-Defined Networking (SDN)** to create a logical tunnel between nodes or networks.
* When used inside a data center, overlay networks are commonly implemented using **Virtual eXtensible LANs (VXLANs)**.

---

## INFRASTRUCTURE AS CODE (IaC)

Cloud services require the rapid provisioning and de-provisioning of server instances and networks, relying heavily on automation, orchestration, and the use of overlay networks to establish point-to-point links quickly and reliably.

This means that these infrastructure components must be fully accessible to scripting, representing the idea of **Infrastructure as Code (IaC)**. Software-Defined Networking (SDN) serves as a model for these processes.

### Automation

* **Automation** via scripting means that each configuration or build task is performed by a block of code.
* The script takes standard arguments as data, reducing uncertainty over configuration choices and leading to fewer errors.
* **Two principal types of automation tools** focus on making a single, discrete task repeatable:
    * **Imperative Tools:** Require the precise steps to follow to achieve the desired configuration as input. This approach is most similar to automating traditional scripting languages such as PowerShell and Bash.
    * **Declarative Tools:** Take the desired configuration as input and leave the details of how that configuration should be achieved to the implementation platform. For example, a declarative configuration file specifies the *desired state*, leaving the specific implementation to the automation platform. Imperative tools specify *each step required*.

### Orchestration

* Where automation focuses on making a single discrete task easily repeatable, **orchestration performs a sequence of automated tasks via scripts or API service calls.**
* For orchestration to work properly, automated steps must occur in the correct sequence, taking dependencies into account. It must provide the right security credentials at every step and have the necessary rights and permissions to perform the defined tasks.
* Orchestration automates complex processes that might otherwise require dozens or hundreds of manual steps.
* Automation and Orchestration platforms connect to provide administration, management, and orchestration for many cloud platforms and services. Industry leaders include **Chef, Puppet, Ansible, and Kubernetes.**

### Infrastructure as Code (IaC) Defined

* Rather than manually installing operating systems and applications, making configuration changes, or installing patches, cloud technology encourages the use of **scripted approaches to provisioning and infrastructure management**.
* This is where automation and orchestration fully replace manual configuration, referred to as **IaC**.
* One of IaC's goals is to **eliminate "Snowflake Systems."** A Snowflake is a configuration or build that is different from others. The lack of consistency (or drift) in the platform environment leads to security and stability issues.
* **IaC tools for provisioning and management:**
    * **Terraform:** Primarily for **immutable infrastructure provisioning** (creating, modifying, deleting infrastructure resources like VMs, networks, storage).
    * **Ansible:** **Mutable**. Uses Playbooks, Inventory, Templates. Communication via SSH (port 22). Agentless (Push mechanism).
    * **Puppet:** **Mutable**. Uses Manifests, Templates. Communication via HTTPS (REST API) (port 8140 TCP). Agent-based (Pull mechanism).
    * **Chef:** **Mutable**. Uses Recipes, Run-lists. Communication via HTTPS (REST API) (port 10002 TCP). Agent-based (Pull mechanism).

---

## SOFTWARE-DEFINED NETWORKING (SDN)

SDN is a model for how these IaC processes are used for provisioning and de-provisioning networks.

### SDN Architecture (Three Layers)

SDN architectures are typically divided into three logical layers, from top to bottom: Application, Control (or Management), and Infrastructure (or Data).

1.  **Application Layer (Top):**
    * Applies business logic to make decisions about how traffic should be prioritized, secured, and switched.
    * This layer defines policies such as segmentation, Access Control Lists (ACLs), Security Groups, traffic prioritization, policing/shaping, and QoS.
    * It defines the *desired configuration and network behavior*.

2.  **Control / Management Plane Layer (Middle):**
    * The principal innovation of SDN is to **insert a control layer between the application layer and the infrastructure layer.**
    * The functions of the control plane are implemented by a virtual device known as the **SDN Controller**.
    * The controller interacts programmatically with network devices.
    * **Northbound API (NBI):** The interface between SDN applications and the SDN controller. It allows applications to interact with the controllers, access the data it gathers about the network, program it, and make changes in the network via the Southbound API. Data is often sent in structured/serialized formats like JSON/YAML. It supports CRUD (Create, Read, Update, Delete) operations.
    * **Southbound API (SBI):** The interface between the SDN Controller and the infrastructure devices. It allows the controller to communicate with and control the network devices (e.g., modify their data plane tables like IP, ACL, MAC, NAT). OpenFlow is a common Southbound API protocol.
    * A separate **Management Plane** sits at the same level as the Control Plane to interface with the operational layer (e.g., device state, CPU/memory utilization). This is used for adding traffic conditions based on network status.

3.  **Infrastructure / Data Plane Layer (Bottom):**
    * These are the physical or virtual network appliances (switches, routers, firewalls, etc.) that handle the actual **forwarding (data) and operational planes** of traffic.
    * They perform the important tasks of switching and routing traffic.

---

# CHAPTER 20: INFRASTRUCTURE AS CODE (IAC): AUTOMATION & ORCHESTRATION 

## NETWORK AUTOMATION

Network automation provides many key benefits by using tools and methods to automate tasks.

### Key Benefits of Network Automation

* **Scalability:** Networks become much more scalable as configurations can be deployed rapidly and consistently across many devices.
* **Network-Wide Policy Compliance:** Automated systems ensure that policies are consistently applied across the entire network, reducing configuration drift.
* **Improved Efficiency:** Automating network operations leads to reduced operating expenses (OpEx) by minimizing manual effort and human error.
* **Consistency:** Reduces "Snowflake Systems" and configuration drift, leading to greater stability and security.

### Tools and Methods for Network Automation

* **Ansible, Puppet, Python scripts, Chef:** Common tools used for network automation.
* **REST API:** A common interface used on controllers and network devices for programmatic interaction.
* **SDN Solutions:** Software-Defined Networking greatly facilitates the automation of various tasks via the SDN Controller.
* **Traditional Network Architectures:** Networking tasks can also be automated in traditional network architectures, but SDN tools can provide greater benefits by centralizing control.

---

## CISCO SD-ACCESS

Cisco SD-Access is Cisco's enterprise-level SDN solution for campus and branch networks.

### Underlay and Overlay in SD-Access

* **Underlay Network:** The underlying physical network of devices and connections (including wired and wireless) providing Layer 3 IP connectivity. Its purpose is to support the VXLAN tunnels of the Overlay.
* **Overlay Network:** The virtual network built on top of the physical underlay. SD-Access uses **VXLAN (Virtual eXtensible LAN)** to build tunnels over the underlay, providing Layer 2 connectivity over a Layer 3 underlay.
* **Fabric:** The combination of the Underlay and Overlay forms the network fabric.

### Three Different Roles for Switches in SD-Access

1.  **Edge Nodes:**
    * Connect to end-hosts (clients).
    * Access Switches act as the default gateway for end-hosts (implementing a **Routed Access Layer**).
2.  **Border Nodes:**
    * Connect to devices outside of the SD-Access domain (e.g., WAN routers, external data centers, the Internet).
3.  **Control Nodes:**
    * Use **LISP (Locator/ID Separation Protocol)** to perform various control plane functions.
    * Maintain a list of mappings of **EID (Endpoint Identifiers)** to **RLOCs (Routing Locators)**, effectively separating identity from location.

### SD-Access Deployment Models

* **Brownfield Deployment:** SD-Access can be added to an existing network if your hardware and software support it.
* **Greenfield Deployment:** A new deployment will be configured by **Cisco DNA Center** to ensure an optimal SD-Access underlay.
    * In a Greenfield deployment, all links between switches are **routed ports**.
    * **No Spanning Tree Protocol (STP)** is needed in the underlay due to the routed links.
    * Access Switches act as the default gateway for end-hosts.
    * Cisco's **TrustSec (CTS)** provides policy control (QoS, security policy, etc.) within SD-Access.

## Cisco DNA Center

Cisco DNA Center is the SDN Controller for SD-Access and has two main roles:

1.  **Network Manager:** For traditional (non-SD-Access) networks, it provides centralized management, monitoring, and automation capabilities.
2.  **SDN Controller:** For SD-Access deployments.

* **REST API:** DNA Center exposes a REST API that can be used to interact with it programmatically. The Southbound Interface (SBI) supports Netconf and Restconf.
* **Intent-Based Networking:** DNA Center enables "Intent-Based Networking." This allows engineers to communicate their *intent* for network behavior (e.g., "Guest users should not access corporate resources"). DNA Center then translates this intent into the actual configurations and policies on the network devices, centrally managing and monitoring them.
* **Configuration Drift:** DNA Center helps to prevent **configuration drift**, which occurs when individual changes made over time cause a device's configuration to deviate from the standardized or correct configurations defined by the company. It facilitates **Configuration Provisioning**, referring to how configuration changes are applied to devices.
