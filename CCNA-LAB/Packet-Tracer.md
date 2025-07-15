# Network Engineering Lab Series: Architecture Transformation (Packet Tracer Edition)

## Project Overview

Welcome to my hands-on network engineering lab series! This repository documents my journey to solidify foundational networking skills using Cisco Packet Tracer. This approach prioritizes rapid prototyping and concept verification to maintain motivation and efficient study flow. The core idea is to progressively build and transform a network topology across three common architectural models:

1.  Three-Tier Architecture (Classic Enterprise)
2.  Two-Tier (Collapsed Core) Architecture
3.  Spine-Leaf Architecture (Modern Data Center/Enterprise)

For each architecture, I will configure, verify, and troubleshoot a comprehensive set of networking protocols and services. This approach allows me to not only learn the "how" but also the "why" – understanding which protocols are essential for each design.

### Why Packet Tracer for this approach?

* Speed & Simplicity: Rapid device setup and instant boot times mean more time configuring and less time waiting.
* Accessibility: Easily runnable on most laptops without high resource demands.
* Core Concept Mastery: Excellent for understanding VLANs, Trunking, EtherChannel, STP, HSRP, OSPF, EIGRP, ACLs, and basic NAT.
* Focus on Fundamentals: Allows direct focus on networking concepts without battling emulation quirks.

### Lab Environment

* Simulation Platform: Cisco Packet Tracer (Latest Version Recommended)
* Device Types: Standard Packet Tracer Routers, Multilayer Switches, and 2960 Switches.
* Client Devices: Standard Packet Tracer PCs and Server.


### Lab Series Objectives: A Comprehensive Packet Tracer Network Design

This comprehensive lab series aims for proficiency in designing, implementing, and troubleshooting a realistic enterprise network topology within Packet Tracer. Through hands-on configuration and verification, learners will achieve mastery in the following critical networking areas and technologies:

* Network Infrastructure Foundations:
    * LAN Switching Fundamentals: Implementing VLANs and configuring Trunking (802.1Q) for inter-VLAN communication.
    * Layer 3 Switching & Redundancy: Setting up Switched Virtual Interfaces (SVIs) for inter-VLAN routing, and ensuring high availability with Hot Standby Router Protocol (HSRP) for seamless gateway failover.
    * EtherChannel Resilience: Configuring robust EtherChannels using both LACP (Link Aggregation Control Protocol) and PAgP (Port Aggregation Protocol) for improved bandwidth and link redundancy.
    * Advanced Spanning Tree Protocol (STP): Enhancing Layer 2 stability and preventing loops with STP best practices, including PortFast for immediate port activation, BPDU Guard to prevent rogue switches, Root Guard to enforce root bridge placement, and Loop Guard for unidirectional link failure detection.

* Routing & Connectivity:
    * Dynamic Routing: Implementing OSPFv2 (Open Shortest Path First) for efficient IPv4 route advertisement and dynamic path determination across the network.
    * Internet Connectivity: Configuring Network Address Translation (NAT), specifically Dynamic PAT (Port Address Translation), to allow internal private IP addresses to access simulated external resources (e.g., the Internet).

* Network Security & Access Control:
    * Access Control Lists (ACLs): Deploying both Standard and Extended Access Control Lists for granular traffic filtering (e.g., inter-VLAN communication restrictions) and securing remote device management access (VTY lines).
    * Layer 2 Security Enhancements (Planned): Implementing crucial access layer security features such as Port Security to control MAC addresses, DHCP Snooping to mitigate rogue DHCP servers and build IP-MAC binding tables, and Dynamic ARP Inspection (DAI) to prevent ARP spoofing.

* Essential Network Services & Management (Planned):
    * Dynamic Host Configuration Protocol (DHCP): Configuring centralized DHCP services for automated IP address assignment to end devices.
    * Network Time Protocol (NTP): Synchronizing device clocks for accurate logging and troubleshooting.
    * Domain Name System (DNS): Ensuring proper name resolution capabilities within the network.
    * Simple Network Management Protocol (SNMP): Preparing devices for network monitoring.
    * Syslog: Centralizing log messages for efficient event monitoring and troubleshooting.

* Network Operations & Troubleshooting:
    * Developing proficiency in utilizing essential Cisco IOS Command Line Interface (CLI) `show` commands for real-time verification, monitoring, and effective troubleshooting of network operations.

* Wireless LAN (WLAN) (Optional - if desired):
    * Basic WLAN configuration with WPA2-PSK security using Packet Tracer's generic Wireless Router/Access Point functionality. *(Note: This section has not yet been detailed. Please confirm if you wish to include this in the lab series.)*

----

## Section 1: Three-Tier Architecture

This initial phase focuses on building a robust, traditional three-tier enterprise network. All the specified wired-network protocols and services will be implemented in this architecture, serving as our baseline. Wireless components and a dedicated WAN router are excluded for this initial build phase.

### 1.1 Architecture Overview

The classic three-tier design organizes network devices into distinct logical layers:

* Core Layer: The high-speed backbone, optimizing for fast packet forwarding and inter-network connectivity (e.g., Internet).
* Distribution Layer: Acts as an aggregation point for access layer devices. It's responsible for routing between VLANs, enforcing security policies (ACLs), and implementing redundancy (HSRP). Each access layer switch connects redundantly to *both* distribution layer switches.
* Access Layer: Connects end-user devices (PCs, servers). Its focus is on high port density, basic connectivity, and foundational security features like port security and VLAN assignment.

In this architecture, Layer 2 protocols like STP and EtherChannel are critical to prevent loops and provide redundancy. Redundancy at every layer, from access uplinks to core interconnects, is paramount for high availability.

### 1.2 Lab Topology Diagram

(Screenshot of your Packet Tracer Lab for Three-Tier Architecture will go here)

* Instruction to the User (You): Please replace this placeholder with a high-resolution screenshot of your complete Three-Tier topology from Packet Tracer. Label devices clearly (e.g., R1, SW1, PC1).

The interface names for the `PT-Router` with added modules typically follow a pattern like `GigabitEthernetX/Y` (e.g., `Gi0/0`, `Gi0/1` for default ports, and then `Gi1/0`, `Gi2/0`, etc., for ports on modules in different slots). For simplicity and consistency in the `README.md`, I will map the required ports to the `GiX/Y` format, assuming you arrange them logically when adding modules.


### 1.3 Detailed Topology Description

*(This section remains the same, confirming the device types you are using)*

Core Layer Devices (Use "PT-Router" or "Generic Router" in Packet Tracer):
* `Router 1 (R1)`: Primary Core Router
* `Router 2 (R2)`: Secondary/Redundant Core Router
* `ISP Router (ISP-R1)`: Simulates an Internet Service Provider

Distribution Layer Devices (Use "Multilayer Switch" or "3560 Switch" in Packet Tracer):
* `Router 3 (R3)`: Primary Distribution Switch
* `Router 4 (R4)`: Secondary Distribution Switch

Access Layer Devices (Use "2960 Switch" in Packet Tracer):
* `Switch 1 (SW1)`: Access Switch for PC1 and Server
* `Switch 2 (SW2)`: Access Switch for PC2
* `Switch 3 (SW3)`: Access Switch for PC3
* `Switch 4 (SW4)`: Access Switch for PC4

Specialized Devices & Clients (Standard Packet Tracer devices):

* `DNS/TFTP/NTP/Syslog Server (Server1)`: A "Server" device (will reside in VLAN 99 - Management)
* `Client PC 1 (PC1)`: A "PC" device (will reside in VLAN 10 - Sales)
* `Client PC 2 (PC2)`: A "PC" device (will reside in VLAN 10 - Sales)
* `Client PC 3 (PC3)`: A "PC" device (will reside in VLAN 20 - HR)
* `Client PC 4 (PC4)`: A "PC" device (will reside in VLAN 20 - HR)
* `Client PC 5 (PC5)`: A "PC" device (will reside in VLAN 99 - Management)
* `Client PC 6 (PC6)`: A "PC" device (will reside in VLAN 99 - Management)
* `Client PC 7 (PC7)`: A "PC" device (will reside in VLAN 99 - Management)
* `Cloud Object (Internet)`: Packet Tracer's "Cloud" device (for external connectivity simulation)

---

## Section 2: Detailed Connectivity (Interface:Device-Interface:Device - Packet Tracer Naming):

Important Note on Interface Naming & Packet Tracer Limitations:

For R1, R2, and ISP-R1 (PT-Routers), you will need to add PT-ROUTER-NM-1FGE modules to get enough Gigabit Ethernet ports. Their interfaces will typically be named GigabitEthernetX/Y.

For R3 and R4 (Cisco Catalyst 3560 Multilayer Switches), these switches have only two Gigabit Ethernet ports (Gi0/1, Gi0/2) and the rest are FastEthernet (Fa0/X). The GigE ports will be used for Core uplinks. All other Distribution Layer links (to Access and peer Distribution) will use FastEthernet.

For SW1-SW4 (2960 Switches), these also have only two Gigabit Ethernet uplinks (Gi0/1, Gi0/2) and the rest are FastEthernet. All links to the Distribution layer will use FastEthernet to match the 3560's ports.

A. Core Layer Connections (PT-Routers):

* `R1 Gi0/0` : `ISP-R1 Gi0/0` (Primary Internet Uplink)
* `R2 Gi0/0` : `ISP-R1 Gi0/1` (Secondary/Redundant Internet Uplink)
* `R1 Gi0/1` : `R2 Gi0/1` (Core Router Interconnect - Link 1)
* `R1 Gi0/2` : `R2 Gi0/2` (Core Router Interconnect - Link 2)

B. Core to Distribution Layer Connections (PT-Routers to Multilayer Switches):

* `R1 Gi0/3` : `R3 Gi0/1` (R1 to R3 - Primary Link)
* `R1 Gi0/4` : `R4 Gi0/1` (R1 to R4 - Primary Link)
* `R2 Gi0/3` : `R3 Gi0/2` (R2 to R3 - Secondary Link)
* `R2 Gi0/4` : `R4 Gi0/2` (R2 to R4 - Secondary Link)

C. Distribution to Access Layer Connections (3560 Multilayer Switches to 2960 Switches - EtherChannel Bundles / Routed Links):
    * Each Access Layer switch (SW1-SW4) will connect to *both* Distribution Layer switches (R3 and R4) with two redundant FastEthernet links each.
    * The Access Switch side will form an EtherChannel bundle (Port-Channel) using these FastEthernet ports. The Distribution Switch will use separate routed interfaces (e.g., SVIs) as peers to that Port-Channel.

* R3 (3560 Multilayer Switch) to Access Switches (2960 Switches):
    * `R3 Fa0/1` : `SW1 Fa0/1` (R3 to SW1 - Link 1 for Port-Channel)
    * `R3 Fa0/2` : `SW1 Fa0/2` (R3 to SW1 - Link 2 for Port-Channel)
    * `R3 Fa0/3` : `SW2 Fa0/1` (R3 to SW2 - Link 1 for Port-Channel)
    * `R3 Fa0/4` : `SW2 Fa0/2` (R3 to SW2 - Link 2 for Port-Channel)
    * `R3 Fa0/5` : `SW3 Fa0/1` (R3 to SW3 - Link 1 for Port-Channel)
    * `R3 Fa0/6` : `SW3 Fa0/2` (R3 to SW3 - Link 2 for Port-Channel)
    * `R3 Fa0/7` : `SW4 Fa0/1` (R3 to SW4 - Link 1 for Port-Channel)
    * `R3 Fa0/8` : `SW4 Fa0/2` (R3 to SW4 - Link 2 for Port-Channel)

* R4 (3560 Multilayer Switch) to Access Switches (2960 Switches):
    * `R4 Fa0/1` : `SW1 Fa0/3` (R4 to SW1 - Link 1 for Port-Channel)
    * `R4 Fa0/2` : `SW1 Fa0/4` (R4 to SW1 - Link 2 for Port-Channel)
    * `R4 Fa0/3` : `SW2 Fa0/3` (R4 to SW2 - Link 1 for Port-Channel)
    * `R4 Fa0/4` : `SW2 Fa0/4` (R4 to SW2 - Link 2 for Port-Channel)
    * `R4 Fa0/5` : `SW3 Fa0/3` (R4 to SW3 - Link 1 for Port-Channel)
    * `R4 Fa0/6` : `SW3 Fa0/4` (R4 to SW3 - Link 2 for Port-Channel)
    * `R4 Fa0/7` : `SW4 Fa0/3` (R4 to SW4 - Link 1 for Port-Channel)
    * `R4 Fa0/8` : `SW4 Fa0/4` (R4 to SW4 - Link 2 for Port-Channel)

D. Distribution Layer Interconnect (3560 Multilayer Switches):
    * These links will also utilize FastEthernet ports due to GigE port limitations on the 3560s.

* `R3 Fa0/9` : `R4 Fa0/9` (R3 to R4 - Link 1)
* `R3 Fa0/10` : `R4 Fa0/10` (R3 to R4 - Link 2)


E. Access Layer to Client/Service Connections (2960 Switches):

* `SW1 Fa0/5` : `PC1` (VLAN 10 - Sales)
* `SW1 Fa0/6` : `Server1` (VLAN 99 - Management)
* `SW1 Fa0/7` : `PC5` (VLAN 99 - Management)
* `SW2 Fa0/5` : `PC2` (VLAN 10 - Sales)
* `SW2 Fa0/6` : `PC6` (VLAN 99 - Management)
* `SW3 Fa0/5` : `PC3` (VLAN 20 - HR)
* `SW3 Fa0/6` : `PC7` (VLAN 99 - Management)
* `SW4 Fa0/5` : `PC4` (VLAN 20 - HR)

F. ISP-R1 to Internet Cloud (PT-Router to Cloud):

* `ISP-R1 Gi0/2` : `Cloud0` (Packet Tracer Cloud Object, connect via "DSL Modem" or "Cable Modem" if available in PT and desired for realism, then to Cloud's "Ethernet" port).

----

## Section 3: IP Addressing Scheme

This IP addressing plan is tailored to the Packet Tracer lab topology, meticulously mapping IP addresses to the specific GigabitEthernet and FastEthernet interfaces as per our finalized connectivity details.

Core Layer Subnets (PT-Routers):
* ISP Uplinks (Primary/Secondary):
    * `203.0.113.0/30`:
        * `203.0.113.1` on `R1 GigabitEthernet0/0`
        * `203.0.113.2` on `ISP-R1 GigabitEthernet1/0`
    * `203.0.113.4/30`:
        * `203.0.113.5` on `R2 GigabitEthernet0/0`
        * `203.0.113.6` on `ISP-R1 GigabitEthernet2/0`

* Core Interconnect (R1-R2):
    * `10.0.0.0/30` (Link 1):
        * `10.0.0.1` on `R1 GigabitEthernet1/0`
        * `10.0.0.2` on `R2 GigabitEthernet1/0`
    * `10.0.0.4/30` (Link 2):
        * `10.0.0.5` on `R1 GigabitEthernet2/0`
        * `10.0.0.6` on `R2 GigabitEthernet2/0`

Core to Distribution Subnets (PT-Routers to 3560 Multilayer Switches):
* R1 to Distribution:
    * `10.0.1.0/30` (R1-R3 Link):
        * `10.0.1.1` on `R1 GigabitEthernet3/0`
        * `10.0.1.2` on `R3 GigabitEthernet0/1`
    * `10.0.1.4/30` (R1-R4 Link):
        * `10.0.1.5` on `R1 GigabitEthernet4/0`
        * `10.0.1.6` on `R4 GigabitEthernet0/1`

* R2 to Distribution:
    * `10.0.1.8/30` (R2-R3 Link):
        * `10.0.1.9` on `R2 GigabitEthernet3/0`
        * `10.0.1.10` on `R3 GigabitEthernet0/2`
    * `10.0.1.12/30` (R2-R4 Link):
        * `10.0.1.13` on `R2 GigabitEthernet4/0`
        * `10.0.1.14` on `R4 GigabitEthernet0/2`

Distribution to Access Subnets (Routed FastEthernet EtherChannel Links):
* Each pair of links between a Distribution Switch (R3/R4) and an Access Switch (SW1-SW4) will form an EtherChannel bundle on *both* sides. The IP address for the routed link will be assigned to the Port-Channel interface on both the Distribution and Access switches.

* R3 (3560) to Access Switches (2960):
    * `10.0.2.0/30` (R3 Po30 to SW1 Po10):
        * `10.0.2.1` on `R3 Port-channel 30` (grouping `Fa0/1` and `Fa0/2`)
        * `10.0.2.2` on `SW1 Port-channel 10` (grouping `Fa0/1` and `Fa0/2`)
    * `10.0.2.4/30` (R3 Po31 to SW2 Po11):
        * `10.0.2.5` on `R3 Port-channel 31` (grouping `Fa0/3` and `Fa0/4`)
        * `10.0.2.6` on `SW2 Port-channel 11` (grouping `Fa0/1` and `Fa0/2`)
    * `10.0.2.8/30` (R3 Po32 to SW3 Po12):
        * `10.0.2.9` on `R3 Port-channel 32` (grouping `Fa0/5` and `Fa0/6`)
        * `10.0.2.10` on `SW3 Port-channel 12` (grouping `Fa0/1` and `Fa0/2`)
    * `10.0.2.12/30` (R3 Po33 to SW4 Po13):
        * `10.0.2.13` on `R3 Port-channel 33` (grouping `Fa0/7` and `Fa0/8`)
        * `10.0.2.14` on `SW4 Port-channel 13` (grouping `Fa0/1` and `Fa0/2`)

* R4 (3560) to Access Switches (2960):
    * `10.0.2.16/30` (R4 Po40 to SW1 Po20):
        * `10.0.2.17` on `R4 Port-channel 40` (grouping `Fa0/1` and `Fa0/2`)
        * `10.0.2.18` on `SW1 Port-channel 20` (grouping `Fa0/3` and `Fa0/4`)
    * `10.0.2.20/30` (R4 Po41 to SW2 Po21):
        * `10.0.2.21` on `R4 Port-channel 41` (grouping `Fa0/3` and `Fa0/4`)
        * `10.0.2.22` on `SW2 Port-channel 21` (grouping `Fa0/3` and `Fa0/4`)
    * `10.0.2.24/30` (R4 Po42 to SW3 Po22):
        * `10.0.2.25` on `R4 Port-channel 42` (grouping `Fa0/5` and `Fa0/6`)
        * `10.0.2.26` on `SW3 Port-channel 22` (grouping `Fa0/3` and `Fa0/4`)
    * `10.0.2.28/30` (R4 Po43 to SW4 Po23):
        * `10.0.2.29` on `R4 Port-channel 43` (grouping `Fa0/7` and `Fa0/8`)
        * `10.0.2.30` on `SW4 Port-channel 23` (grouping `Fa0/3` and `Fa0/4`)

Distribution Interconnect (R3-R4 - Separate FastEthernet Links):
* `10.0.3.0/30` (Link 1):
    * `10.0.3.1` on `R3 FastEthernet0/9`
    * `10.0.3.2` on `R4 FastEthernet0/9`
* `10.0.3.4/30` (Link 2):
    * `10.0.3.5` on `R3 FastEthernet0/10`
    * `10.0.3.6` on `R4 FastEthernet0/10`

VLAN Subnets (Managed at Distribution Layer via HSRP for First-Hop Redundancy):
* VLAN 10 (Sales): `192.168.10.0/24`
    * HSRP Virtual IP: `192.168.10.254`
    * `192.168.10.1` on `R3 Interface VLAN 10`
    * `192.168.10.2` on `R4 Interface VLAN 10`
* VLAN 20 (HR): `192.168.20.0/24`
    * HSRP Virtual IP: `192.168.20.254`
    * `192.168.20.1` on `R3 Interface VLAN 20`
    * `192.168.20.2` on `R4 Interface VLAN 20`
* VLAN 99 (Management): `192.168.99.0/24`
    * HSRP Virtual IP: `192.168.99.254`
    * `192.168.99.1` on `R3 Interface VLAN 99`
    * `192.168.99.2` on `R4 Interface VLAN 99`
    * For SW1-SW4, Server1 management IPs (e.g., `192.168.99.3` for SW1, `192.168.99.4` for SW2, etc., and `192.168.99.10` for Server1).

Loopback Interfaces (for Routing Protocol advertisement and Router IDs):
* `R1 Loopback0`: `172.16.1.1/32`
* `R2 Loopback0`: `172.16.2.1/32`
* `R3 Loopback0`: `172.16.3.1/32`
* `R4 Loopback0`: `172.16.4.1/32`
* `ISP-R1 Loopback0`: `172.16.6.1/32`


-----

## Section 4: Next Steps for Implementation:

#### \!\!\! IMPORTANT WARNING FOR ALL CONFIGURATION STEPS \!\!\!

Always be mindful of the specific capabilities of each device model.

This lab utilizes Cisco Catalyst 2960 switches at the Access Layer (ASW-1 to ASW-4). These are Layer 2-ONLY switches. They DO NOT SUPPORT Layer 3 routing features such as `ip routing`, `no switchport` on physical interfaces/Port-Channels, or direct IP addressing on data plane interfaces.

All configurations for ASWs in this document are tailored to their Layer 2 capabilities. Attempting to configure Layer 3 features on a 2960 will result in errors and a non-functional lab. A detailed explanation of this distinction and what *would* be configured on a multilayer switch is provided at the end of the configuration section for learning purposes.

1.  Open Cisco Packet Tracer.

2.  Drag and drop the necessary devices into your workspace as described in Section 1.3:

      * Core Layer: Select the `Generic Router (PT-Router)` for `R1 (core-r1)`, `R2 (core-r2)`, and `ISP-R1`.
      * Distribution Layer: Select the `Cisco Catalyst 3560 Multilayer Switch` for `R3 (DSW-R3)` and `R4 (DSW-R4)`.
      * Access Layer: Select the `2960 Switch` for `SW1 (ASW-1)`, `SW2 (ASW-2)`, `SW3 (ASW-3)`, `SW4 (ASW-4)`.
      * End Devices: Use standard `PC` devices for `PC1-PC4`, and a `Server` device for `Server1`.
      * Cloud: Use the `Cloud` object for Internet simulation.

3.  Add any required modules to the PT-Routers (core-r1, core-r2, ISP-R1):

      * For each `PT-Router` device, go to its Physical tab and drag and drop `PT-ROUTER-NM-1FGE` modules into their available slots. Ensure you add enough modules to get all the Gigabit Ethernet ports as specified in Section 1.3.
      * *Pointers:*
          * Remember that the `PT-Router`'s built-in Gigabit Ethernet ports are typically `GigabitEthernet0/0` and `GigabitEthernet0/1`. Modules added in slot 1 will be `GigabitEthernet1/0`, slot 2 will be `GigabitEthernet2/0`, and so on.
          * The 3560 and 2960 switches have fixed ports (2 x GigabitEthernet, 24 x FastEthernet), so no modules are needed or can be added to them.

4.  Connect all cables exactly as specified in the "Detailed Connectivity" (Section 1.3):

      * Crucial Pointer for PT-Router interfaces: Pay extremely close attention to the `GigabitEthernet0/0`, `GigabitEthernet1/0`, `GigabitEthernet2/0`, etc., interface names for `R1 (core-r1)`, `R2 (core-r2)`, and `ISP-R1`.
      * Crucial Pointer for 3560/2960 interfaces: Carefully match the `GigabitEthernet0/X` (e.g., `Gi0/1`, `Gi0/2`) and `FastEthernet0/X` (e.g., `Fa0/1`, `Fa0/2`, etc.) interface names.
      * Key Design Pointer for D-A and D-D links: Specifically, ensure that all Distribution-to-Access and Distribution-to-Distribution links utilize FastEthernet ports on *both* connecting devices (e.g., `DSW-R3 Fa0/1` to `ASW-1 Fa0/1`, etc.), as this was a critical correction to match Packet Tracer's device limitations.

5.  Take NEWEST, FINAL Screenshot for Phase 1: Capture a fresh, clear screenshot of your complete Three-Tier topology within Packet Tracer once all devices are placed and cabled. This will be your definitive topology diagram.

6.  Update `README.md`: Replace the placeholder text in Section 1.2 "Lab Topology Diagram" with your *newest* screenshot.

7.  Confirm Hostnames: Access the CLI of each device and configure its hostname (`core-r1`, `core-r2`, `DSW-R3`, `DSW-R4`, `ASW-1`, `ASW-2`, `ASW-3`, `ASW-4`, `ISP-R1`, `PC1`, `PC2`, `PC3`, `PC4`, `Server1`).

8.  Assign IP Addresses and Configure Basic Layer 2/3 Services (Step-by-Step Configuration):
    Proceed to configure the IP addresses on all relevant Layer 3 interfaces and set up Layer 2 elements precisely according to the FINALIZED Section 1.4 "IP Addressing Scheme" and the corrected design.

    A.  Enable IP Routing on Distribution Switches (DSW-R3, DSW-R4):
    \* Access global configuration mode (`conf t`).
    \* Enter the command: `ip routing`
    \* *Explanation for Learners:* This command is fundamental for Cisco multilayer switches. By default, they only perform Layer 2 switching. `ip routing` enables their Layer 3 forwarding capabilities, allowing them to route traffic between different IP subnets, which is essential for their role in the Distribution layer.

## Section 5: Configure Core Layer Routers (core-r1, core-r2, ISP-R1):
    \* For `core-r1`, `core-r2`, and `ISP-R1`, go to global configuration mode (`conf t`).
    \* For each active GigabitEthernet interface that connects to another router (Core-Core, Core-Distro, ISP-Uplinks), navigate to its interface configuration mode (e.g., `interface GigabitEthernet0/0`).
    \* Assign the IP address and subnet mask: `ip address <address> <subnet-mask>`
    \* Activate the interface: `no shutdown`
    \* For Loopback interfaces (e.g., `interface Loopback0`):
    \* Assign the IP address: `ip address <address> 255.255.255.255` (for a /32 mask).
    \* Activate the interface: `no shutdown`

    C.  Configure Distribution Layer Switches (DSW-R3, DSW-R4) - Loopback and Interconnect Links:
    \* For `DSW-R3` and `DSW-R4`, go to global configuration mode (`conf t`).
    \* For Loopback interfaces (e.g., `interface Loopback0`):
    \* Assign the IP address: `ip address <address> 255.255.255.255`
    \* Activate the interface: `no shutdown`
    \* For the DSW-R3 to DSW-R4 Interconnect FastEthernet links (`Fa0/9` and `Fa0/10` on both DSW-R3 and DSW-R4):
    \* Navigate to the interface configuration mode (e.g., `interface FastEthernet0/9`).
    \* Convert the Layer 2 switchport to a Layer 3 routed port: `no switchport`
    \* *Explanation for Learners:* Physical interfaces on multilayer switches are Layer 2 by default. The `no switchport` command changes the interface's mode, allowing it to directly participate in Layer 3 routing and accept an IP address, rather than just forwarding frames based on MAC addresses.
    \* Assign the IP address: `ip address <address> <subnet-mask>`
    \* Activate the interface: `no shutdown`

### Configure Distribution Layer Switches (DSW-R3, DSW-R4) - Layer 2 Trunk Port-Channels (to Access Switches):

    \* These will be `Port-channel 30` to `33` on `DSW-R3` and `Port-channel 40` to `43` on `DSW-R4`.
    \* *Explanation for Learners:* Since the Access Switches (2960s) are Layer 2 only, the uplinks from the DSWs to the ASWs must be Layer 2 Trunking EtherChannels. This means they will carry traffic for multiple VLANs without directly participating in Layer 3 routing on these specific Port-Channels. The `no switchport` command and IP address will NOT be applied to these Port-Channels.

    ```
    * For DSW-R3's Port-Channels (Po30-33) - Using PAgP (Cisco Proprietary):
        * *Explanation for Learners:* PAgP (Port Aggregation Protocol) is a Cisco-proprietary protocol used to negotiate EtherChannel formation. `mode desirable` actively attempts to form a channel, while `mode auto` passively waits.
        * For each Port-Channel bundle (e.g., for DSW-R3 to ASW-1 - Po30):
            1.  Configure Physical Member Interfaces (Layer 2 for Bundling):
                * Go to interface range configuration mode (e.g., `conf t` then `interface range FastEthernet0/1 - 2`).
                * Add the interfaces to the channel-group: `channel-group <ID> mode desirable` (replace `<ID>` with the correct Port-Channel ID like `30`).
                * Activate the interfaces: `no shutdown`
                * *Note:* These individual physical interfaces remain Layer 2 switchports and will NOT have `no switchport` or an IP address directly configured on them. They solely serve to aggregate into the logical Port-Channel.
            2.  Configure the Logical Port-Channel Interface (Layer 2 Trunking):
                * Exit interface range mode.
                * Navigate to the Port-Channel interface: `interface Port-channel <ID>` (e.g., `interface Port-channel 30`).
                * Set the Port-Channel to trunking mode: `switchport mode trunk`
                * Activate the Port-Channel: `no shutdown`
                * *Important:* No `no switchport` or `ip address` will be configured here.

    * For DSW-R4's Port-Channels (Po40-43) - Using LACP (IEEE Standard):
        * *Explanation for Learners:* LACP (Link Aggregation Control Protocol) is an open-standard protocol (IEEE 802.3ad) for negotiating EtherChannel formation. `mode active` actively attempts to form a channel, while `mode passive` passively waits.
        * For each Port-Channel bundle (e.g., for DSW-R4 to ASW-1 - Po40):
            1.  Configure Physical Member Interfaces (Layer 2 for Bundling):
                * Go to interface range configuration mode (e.g., `conf t` then `interface range FastEthernet0/1 - 2`).
                * Add the interfaces to the channel-group: `channel-group <ID> mode active` (replace `<ID>` with the correct Port-Channel ID like `40`).
                * Activate the interfaces: `no shutdown`
                * *Note:* These individual physical interfaces remain Layer 2 switchports and will NOT have `no switchport` or an IP address directly configured on them. They solely serve to aggregate into the logical Port-Channel.
            2.  Configure the Logical Port-Channel Interface (Layer 2 Trunking):
                * Exit interface range mode.
                * Navigate to the Port-Channel interface: `interface Port-channel <ID>` (e.g., `interface Port-channel 40`).
                * Set the Port-Channel to trunking mode: `switchport mode trunk`
                * Activate the Port-Channel: `no shutdown`
                * *Important:* No `no switchport` or `ip address` will be configured here.
    ```

### Configure Access Layer Switches (ASW-1 to ASW-4) - Layer 2 Trunk Port-Channels (Uplinks to Distribution):
    ```
    Explanation for Learners:* The Access Switches (2960s) operate purely at Layer 2. Their uplinks to the Distribution Layer must be configured as Layer 2 Trunking EtherChannels to carry VLAN traffic from end devices up to the DSWs for routing. `ip routing` will NOT be enabled on these switches.
    * Crucial Pointer for Channel-Group IDs on 2960s: In Packet Tracer, 2960 switches typically support channel-group IDs only within the range of 1-6. Therefore, we will use Port-channel 1 for the PAgP uplink and Port-channel 2 for the LACP uplink on each Access Switch. The channel-group ID does not need to match on both ends of the EtherChannel (DSW and ASW).
    * For ASW's Port-Channels connecting to DSW-R3 (using PAgP):
    * *This will be `Port-channel 1` on each ASW (ASW-1, ASW-2, ASW-3, ASW-4).*
    * *Explanation for Learners:* Since DSW-R3 is configured with `mode desirable` for PAgP, the ASW side should be configured with `mode auto` to passively respond and form the EtherChannel.
    * For each ASW (e.g., ASW-1 to DSW-R3):
        1.  Configure Physical Member Interfaces (Layer 2 for Bundling):
            * Go to interface range configuration mode (e.g., `conf t` then `interface range FastEthernet0/1 - 2` on `ASW-1`).
            * Add the interfaces to the channel-group: `channel-group 1 mode auto`
            * Activate the interfaces: `no shutdown`
            * *Note:* These individual physical interfaces remain Layer 2 switchports and will NOT have `no switchport` or an IP address directly configured on them. They aggregate into the logical Port-Channel.
        2.  Configure the Logical Port-Channel Interface (Layer 2 Trunking):
            * Exit interface range mode.
            * Navigate to the Port-Channel interface: `interface Port-channel 1`
            * Set the Port-Channel to trunking mode: `switchport mode trunk`
            * Activate the Port-Channel: `no shutdown`
            * *Important:* No `no switchport` or `ip address` will be configured here.

    * For ASW's Port-Channels connecting to DSW-R4 (using LACP):
    * *This will be `Port-channel 2` on each ASW (ASW-1, ASW-2, ASW-3, ASW-4).*
    * *Explanation for Learners:* Since DSW-R4 is configured with `mode active` for LACP, the ASW side should be configured with `mode passive` to passively respond and form the EtherChannel.
    * For each ASW (e.g., ASW-1 to DSW-R4):
        1.  Configure Physical Member Interfaces (Layer 2 for Bundling):
            * Go to interface range configuration mode (e.g., `conf t` then `interface range FastEthernet0/3 - 4` on `ASW-1`).
            * Add the interfaces to the channel-group: `channel-group 2 mode passive`
            * Activate the interfaces: `no shutdown`
            * *Note:* These individual physical interfaces remain Layer 2 switchports and will NOT have `no switchport` or an IP address directly configured on them. They aggregate into the logical Port-Channel.
        2.  Configure the Logical Port-Channel Interface (Layer 2 Trunking):
            * Exit interface range mode.
            * Navigate to the Port-Channel interface: `interface Port-channel 2`
            * Set the Port-Channel to trunking mode: `switchport mode trunk`
            * Activate the Port-Channel: `no shutdown`
            * *Important:* No `no switchport` or `ip address` will be configured here.
    ```       

### Important Note for Learners: Understanding Layer 2 vs. Layer 3 Switches in EtherChannels

It's crucial to distinguish between Layer 2-only switches (like the Catalyst 2960s used for our ASWs) and multilayer (Layer 3 capable) switches (like our Catalyst 3560s used for DSWs). This distinction fundamentally impacts how EtherChannels are configured and whether IP addresses can be assigned directly to bundled interfaces.

Scenario A: Layer 2 Access Switches (Our Current Lab Design with 2960s)

As configured in this lab (Steps 8.d and 8.f), when your Access Switches are Layer 2-only (2960s):

  * `ip routing` is NOT enabled on the ASWs.
  * EtherChannels (Port-Channels) on the ASWs (and their corresponding DSW ports) are configured as Layer 2 Trunks (`switchport mode trunk`).
  * NO IP ADDRESSES are assigned directly to these Port-Channel interfaces on the ASWs.
  * The default gateways for end devices are the VLAN SVIs on the Distribution Layer Switches (DSW-R3, DSW-R4).

Scenario B: Multilayer Access Switches (Hypothetical for Learning Contrast)

If the Access Switches (ASWs) in your topology were also multilayer switches (e.g., Cisco Catalyst 3560s or higher models capable of Layer 3 routing), you would configure their uplinks to the Distribution Layer as Layer 3 Routed EtherChannels. This would involve:

  * Enabling `ip routing` on the ASWs in global configuration mode:
    ```
    ASW(config)# ip routing
    ```
  * Configuring the logical Port-Channel interface to be a Layer 3 routed port:
    ```
    ASW(config)# interface Port-channel <ID>
    ASW(config-if)# no switchport
    ASW(config-if)# ip address <address> <subnet-mask>
    ASW(config-if)# no shutdown
    ```
  * In this hypothetical scenario, the DSW-to-ASW links would become point-to-point Layer 3 links, and IP addresses (like the `/30` networks we initially discussed for these links) would be assigned to both ends of the Port-Channel. The VLAN SVIs could then potentially be placed on the ASWs themselves (if they were routing locally), or routing would occur directly on the L3 EtherChannel.

This lab explicitly uses 2960s at the Access Layer to demonstrate the common Layer 2-only Access / Layer 3 Distribution design pattern, which relies on the DSWs for all inter-VLAN routing via SVIs.

If you did configure the the Distribution Switches Port-Channel interfaces with IP address.
Yes, you must remove the IP addresses from the Port-channel interfaces (Port-channel 30-33 on DSW-R3 and Port-channel 40-43 on DSW-R4) before converting them to Layer 2 trunks.
Leaving the IP addresses on a Port-channel that is intended to be a Layer 2 trunk would cause a conflict and prevent the trunk from forming correctly, as it would still be trying to act as a Layer 3 interface.
Here's how you would correct the configuration on DSW-R3 and DSW-R4 for those specific Port-Channels:
For DSW-R3's Port-Channels (Po30-33) and DSW-R4's Port-Channels (Po40-43):
 * Access the Port-Channel Interface:
   DSW-R3(config)# interface Port-channel 30

   (Repeat for Po31, Po32, Po33 on DSW-R3, and Po40, Po41, Po42, Po43 on DSW-R4)
 * Remove the IP Address:
   DSW-R3(config-if)# no ip address

   Explanation for Learners: This command removes any previously configured IP address from the interface, ensuring it no longer attempts to function as a Layer 3 routed port.
 * Ensure it's a switchport (if no switchport was applied):
   DSW-R3(config-if)# switchport

   Explanation for Learners: If you previously applied no switchport to the logical Port-Channel interface, this command reverts it to a Layer 2 switchport, which is necessary for it to operate as a trunk.
*  Set the Port-Channel to Trunking Encapsulation:
   DSW-R3(config-if)# switchport trunk encapsulation dot1q
 * Set the Port-Channel to Trunking Mode:
   DSW-R3(config-if)# switchport mode trunk

   Explanation for Learners: This command explicitly configures the Port-Channel to operate as a trunk, allowing it to carry traffic for multiple VLANs between the Distribution and Access layers.
 * Exit Interface Configuration:
   DSW-R3(config-if)# exit

You would perform these steps for all the Port-Channels connecting the DSWs to the ASWs. This ensures they are properly configured as Layer 2 trunks, aligning with the 2960's capabilities. 


## Section 6: Configure VLANs (Creation on all relevant switches):

  * Purpose: Before you can assign interfaces to a VLAN or create a Switched Virtual Interface (SVI) for a VLAN, the VLAN itself must exist in the switch's VLAN database.
  * Action: Go to global configuration mode (`conf t`) on ALL of your Distribution Switches (`DSW-R3`, `DSW-R4`) and ALL of your Access Switches (`ASW-1`, `ASW-2`, `ASW-3`, `ASW-4`). Create VLANs 10, 20, and 99 with their respective names:
    ```
    Switch# configure terminal
    Switch(config)# vlan 10
    Switch(config-vlan)# name Sales
    Switch(config-vlan)# exit
    Switch(config)# vlan 20
    Switch(config-vlan)# name HR
    Switch(config-vlan)# exit
    Switch(config)# vlan 99
    Switch(config-vlan)# name Management
    Switch(config-vlan)# exit
    ```

    G. Configure Access Layer Switches (ASW-1 to ASW-4) - Access Ports for End Devices:

  * Explanation for Learners: These ports connect directly to end-user devices (PCs, Servers) and are assigned to a specific VLAN. They do not carry traffic for multiple VLANs (unlike trunk ports). This step assigns the ports to the VLANs you just created.

  * Action: For each ASW, identify the FastEthernet ports connected to PCs and the Server. Go to interface configuration mode for each port (e.g., `interface FastEthernet0/5`). Set the port to access mode: `switchport mode access`. Assign the port to its respective VLAN: `switchport access vlan <VLAN_ID>`. Activate the interface: `no shutdown`.

      * On `ASW-1`:
          * `interface FastEthernet0/5`: `switchport access vlan 10` (for PC1)
          * `interface FastEthernet0/6`: `switchport access vlan 20` (for PC4)
      * On `ASW-2`:
          * `interface FastEthernet0/5`: `switchport access vlan 10` (for PC2)
          * `interface FastEthernet0/6`: `switchport access vlan 20` (for PC5)
      * On `ASW-3`:
          * `interface FastEthernet0/5`: `switchport access vlan 10` (for PC3)
          * `interface FastEthernet0/6`: `switchport access vlan 99` (for PC7)
      * On `ASW-4`:
          * `interface FastEthernet0/5`: `switchport access vlan 20` (for PC6)
          * `interface FastEthernet0/6`: `switchport access vlan 99` (for PC8)
          * `interface FastEthernet0/7`: `switchport access vlan 99` (for Server1)

## Section 7: Configure Distribution Layer Switches (DSW-R3, DSW-R4) - VLAN SVIs:

  * VLAN Subnets (Managed at Distribution Layer via HSRP for First-Hop Redundancy):
    Note for DSW-R3:

```
DSW-R3 VLAN SVIs & HSRP:
VLAN 10 (Sales): 192.168.10.1 (Active for 10)
    HSRP Virtual IP: 192.168.10.254
VLAN 20 (HR): 192.168.20.1 (Standby for 20)
    HSRP Virtual IP: 192.168.20.254
VLAN 99 (Management): 192.168.99.1 (Active for 99)
    HSRP Virtual IP: 192.168.99.254
```

Note for DSW-R4:

```
DSW-R4 VLAN SVIs & HSRP:
VLAN 10 (Sales): 192.168.10.2 (Standby for 10)
    HSRP Virtual IP: 192.168.10.254
VLAN 20 (HR): 192.168.20.2 (Active for 20)
    HSRP Virtual IP: 192.168.20.254
VLAN 99 (Management): 192.168.99.2 (Standby for 99)
    HSRP Virtual IP: 192.168.99.254
```
    * For SW1-SW4, Server1 management IPs (e.g., `192.168.99.3` for SW1, `192.168.99.4` for SW2, etc., and `192.168.99.10` for Server1).

  * Understanding Hot Standby Router Protocol (HSRP):

      * Purpose: HSRP is a Cisco-proprietary First-Hop Redundancy Protocol (FHRP) that provides network redundancy for IP networks without requiring a re-configuration of the end-user's default gateway. In a redundant setup like our Distribution Layer, you have two (or more) switches that can act as the default gateway for a VLAN. HSRP ensures that even if one switch fails, network connectivity for that VLAN remains uninterrupted.
      * How it Works:
          * Virtual IP Address & MAC Address: HSRP creates a "virtual" router with a single virtual IP address and a virtual MAC address. This virtual IP is configured as the default gateway on all end devices within the VLAN.
          * Active Router: One router (DSW) in the HSRP group becomes the "Active" router. It owns the virtual IP and virtual MAC address and is responsible for forwarding traffic.
          * Standby Router: Another router (DSW) in the group becomes the "Standby" router. It monitors the Active router and takes over its role if the Active router fails.
          * Hellos: Active and Standby routers exchange "hello" messages to monitor each other's status. If the Standby router doesn't receive hellos from the Active router for a certain period (hold timer), it assumes the Active router has failed and takes over.
          * Priority: Routers use a priority value (0-255, default 100) to determine which router becomes Active. The router with the highest priority becomes Active.
          * Preemption: If preemption is enabled, a router with a higher priority will take over the Active role if it comes online or its priority increases (e.g., due to a tracked interface recovering). Without preemption, a lower-priority router will remain Active even if a higher-priority one becomes available.
          * Tracking: This is crucial\! You can configure HSRP to "track" the state of other interfaces (e.g., uplink interfaces to the Core). If a tracked interface goes down, the HSRP priority of that router is *decremented*, potentially forcing a failover to the Standby router, even if the SVI interface itself is still up. This ensures the gateway is only active if it has a viable path to the rest of the network.
      * Why we use it here: In our design, `DSW-R3` and `DSW-R4` both have SVIs for VLANs 10, 20, and 99. HSRP will allow us to make `192.168.X.254` the default gateway for PCs and Server, providing seamless failover between `DSW-R3` and `DSW-R4` if one path or device becomes unavailable.

  * Action for VLAN SVIs and HSRP Configuration:
    For each VLAN (10, 20, 99):

    1.  Navigate to the SVI interface configuration mode (e.g., `interface Vlan 10`).
    2.  Assign the IP address: `ip address <address> <subnet-mask>`.
    3.  Activate the SVI: `no shutdown`.
    4.  Configure HSRP parameters. We will set `DSW-R3` as active for VLANs 10 and 99, and `DSW-R4` as active for VLAN 20, for basic load balancing. We'll use the VLAN ID as the HSRP group number for clarity.

    Configuration on `DSW-R3` (Active for VLANs 10 & 99, Standby for VLAN 20):

    ```
    DSW-R3(config)# interface Vlan10
    DSW-R3(config-if)# ip address 192.168.10.1 255.255.255.0
    DSW-R3(config-if)# standby 10 ip 192.168.10.254
    DSW-R3(config-if)# standby 10 priority 110
    DSW-R3(config-if)# standby 10 preempt
    DSW-R3(config-if)# standby 10 authentication text CiscoPW  ! Optional, but good practice
    DSW-R3(config-if)# no shutdown
    DSW-R3(config-if)# exit

    DSW-R3(config)# interface Vlan20
    DSW-R3(config-if)# ip address 192.168.20.1 255.255.255.0
    DSW-R3(config-if)# standby 20 ip 192.168.20.254
    DSW-R3(config-if)# standby 20 authentication text CiscoPW  ! Optional, but good practice
    DSW-R3(config-if)# no shutdown
    DSW-R3(config-if)# exit

    DSW-R3(config)# interface Vlan99
    DSW-R3(config-if)# ip address 192.168.99.1 255.255.255.0
    DSW-R3(config-if)# standby 99 ip 192.168.99.254
    DSW-R3(config-if)# standby 99 priority 110
    DSW-R3(config-if)# standby 99 preempt
    DSW-R3(config-if)# standby 99 authentication text CiscoPW  ! Optional, but good practice
    DSW-R3(config-if)# no shutdown
    DSW-R3(config-if)# exit
    ```

    Configuration on `DSW-R4` (Active for VLAN 20, Standby for VLANs 10 & 99):

    ```
    DSW-R4(config)# interface Vlan10
    DSW-R4(config-if)# ip address 192.168.10.2 255.255.255.0
    DSW-R4(config-if)# standby 10 ip 192.168.10.254
    DSW-R4(config-if)# standby 10 authentication text CiscoPW  ! Optional, but good practice
    DSW-R4(config-if)# no shutdown
    DSW-R4(config-if)# exit

    DSW-R4(config)# interface Vlan20
    DSW-R4(config-if)# ip address 192.168.20.2 255.255.255.0
    DSW-R4(config-if)# standby 20 ip 192.168.20.254
    DSW-R4(config-if)# standby 20 priority 110
    DSW-R4(config-if)# standby 20 preempt
    DSW-R4(config-if)# standby 20 authentication text CiscoPW  ! Optional, but good practice
    DSW-R4(config-if)# no shutdown
    DSW-R4(config-if)# exit

    DSW-R4(config)# interface Vlan99
    DSW-R4(config-if)# ip address 192.168.99.2 255.255.255.0
    DSW-R4(config-if)# standby 99 ip 192.168.99.254
    DSW-R4(config-if)# standby 99 authentication text CiscoPW  ! Optional, but good practice
    DSW-R4(config-if)# no shutdown
    DSW-R4(config-if)# exit
    ```

## Section 8: Configure End Devices (PC1-PC8, Server1):

  * Action: For each `PC` and the `Server`, go to its Desktop tab -\> IP Configuration.

  * Configure the Static IP Address, Subnet Mask (255.255.255.0 for /24), and Default Gateway according to the scheme below:

      * PC1: IP: `192.168.10.10`, DG: `192.168.10.254`
      * PC2: IP: `192.168.10.11`, DG: `192.168.10.254`
      * PC3: IP: `192.168.10.12`, DG: `192.168.10.254`
      * PC4: IP: `192.168.20.10`, DG: `192.168.20.254`
      * PC5: IP: `192.168.20.11`, DG: `192.168.20.254`
      * PC6: IP: `192.168.20.12`, DG: `192.168.20.254`
      * PC7: IP: `192.168.99.11`, DG: `192.168.99.254`
      * PC8: IP: `192.168.99.12`, DG: `192.168.99.254`
      * Server1: IP: `192.168.99.10`, DG: `192.168.99.254`

Important Note for Learners: Verify Layer 2 Connectivity!

Before proceeding to configure Layer 3 routing, it is crucial to verify that your Layer 2 VLAN segmentation is working as expected. This test confirms that devices within the same VLAN can communicate, and devices in different VLANs (on the same or different Access Switches) cannot yet communicate.

How to Test:

1.  Ping PCs within the SAME VLAN:
    * From `PC1` (VLAN 10), try to ping `PC2` (VLAN 10) and `PC3` (VLAN 10).
    * From `PC4` (VLAN 20), try to ping `PC5` (VLAN 20) and `PC6` (VLAN 20).
    * From `PC7` (VLAN 99), try to ping `PC8` (VLAN 99) and `Server1` (VLAN 99).
    * Expected Result: All these pings should be successful. This confirms that your VLAN creation, access port assignments, and EtherChannel trunks are correctly configured for Layer 2 forwarding within VLANs.

2.  Attempt to Ping PCs between DIFFERENT VLANs:
    * From `PC1` (VLAN 10), try to ping `PC4` (VLAN 20) or `PC7` (VLAN 99).
    * From `PC4` (VLAN 20), try to ping `PC1` (VLAN 10) or `PC7` (VLAN 99).
    * Expected Result: All these pings should fail. This is the desired outcome at this stage, as Layer 3 routing between VLANs has not yet been configured on your Distribution Layer switches.

If your tests match these expected results, you have successfully completed the Layer 2 configuration and are ready to move on to the next phase: configuring Layer 3 routing.

-----

## Section 9: Configuring Layer 3 Routing (OSPF)

This section will guide you through enabling IP routing on your Distribution Layer switches and configuring OSPF across all your Layer 3 devices (Core Routers and Distribution Switches). We will operate all internal OSPF routing within a single Area 0 for simplicity in this lab.

Goal: Allow all VLANs to communicate with each other and for all internal devices to learn routes to each other.

9.1 Enable IP Routing on Distribution Switches

By default, Cisco multilayer switches act primarily as Layer 2 devices. To enable their Layer 3 routing capabilities (which is necessary for SVIs to function as gateways and to participate in routing protocols), you must explicitly enable IP routing.

  * Action: Go to global configuration mode (`conf t`) on `DSW-R3` and `DSW-R4`.

    On `DSW-R3` and `DSW-R4`:

    ```
    Switch(config)# ip routing
    ```

### 9.2 Configure Routed Ports on Distribution Switches (Verification)

As per our finalized IP Addressing Scheme (Section 1.4), the physical interfaces between your Distribution Switches (`DSW-R3` and `DSW-R4`) and between the Distribution and Core Layers were already configured with their IP addresses and set as Layer 3 routed ports.

  * Action: For these interfaces, simply ensure they are in `no switchport` mode and are `no shutdown`. (You would have already applied the `ip address` commands during the initial setup in Section 1.4).

    On `DSW-R3`:

    ```
    DSW-R3(config)# interface FastEthernet0/9
    DSW-R3(config-if)# no switchport  ! Confirm no switchport is applied
    DSW-R3(config-if)# no shutdown
    DSW-R3(config-if)# exit

    DSW-R3(config)# interface FastEthernet0/10
    DSW-R3(config-if)# no switchport  ! Confirm no switchport is applied
    DSW-R3(config-if)# no shutdown
    DSW-R3(config-if)# exit

    DSW-R3(config)# interface GigabitEthernet0/1
    DSW-R3(config-if)# no switchport  ! Confirm no switchport is applied
    DSW-R3(config-if)# no shutdown
    DSW-R3(config-if)# exit

    DSW-R3(config)# interface GigabitEthernet0/2
    DSW-R3(config-if)# no switchport  ! Confirm no switchport is applied
    DSW-R3(config-if)# no shutdown
    DSW-R3(config-if)# exit
    ```

    On `DSW-R4`:

    ```
    DSW-R4(config)# interface FastEthernet0/9
    DSW-R4(config-if)# no switchport  ! Confirm no switchport is applied
    DSW-R4(config-if)# no shutdown
    DSW-R4(config-if)# exit

    DSW-R4(config)# interface FastEthernet0/10
    DSW-R4(config-if)# no switchport  ! Confirm no switchport is applied
    DSW-R4(config-if)# no shutdown
    DSW-R4(config-if)# exit

    DSW-R4(config)# interface GigabitEthernet0/1
    DSW-R4(config-if)# no switchport  ! Confirm no switchport is applied
    DSW-R4(config-if)# no shutdown
    DSW-R4(config-if)# exit

    DSW-R4(config)# interface GigabitEthernet0/2
    DSW-R4(config-if)# no switchport  ! Confirm no switchport is applied
    DSW-R4(config-if)# no shutdown
    DSW-R4(config-if)# exit
    ```

### 9.3 Configure OSPF Routing Protocol

Now, we will configure OSPF on all Layer 3 devices to allow them to dynamically learn routes to all connected networks, including your VLANs.

  * A. Global OSPF Configuration:

      * The `router ospf 1` command starts the OSPF routing process (where `1` is the process ID, arbitrary but unique per router).
      * The `router-id` command explicitly sets the OSPF Router ID. It's best practice to use the Loopback 0 IP address as defined in Section 1.4.
      * `auto-cost reference-bandwidth 1000` sets the reference bandwidth for OSPF cost calculation. For Gigabit Ethernet links, this should be set to `1000` (meaning 1000 Mbps). Ensure this is configured on *all* OSPF-enabled devices for consistent cost calculation.

    On `R1 (core-r1)`, `R2 (core-r2)`, `DSW-R3`, `DSW-R4`, and `ISP-R1`:

    ```
    Router(config)# router ospf 1
    Router(config-router)# router-id <Loopback0_IP_Address_from_Section_1.4>  ! e.g., 172.16.1.1 for R1
    Router(config-router)# auto-cost reference-bandwidth 1000
    Router(config-router)# exit
    ```

  * B. Configure OSPF Networks on Core Routers (`R1`, `R2`, `ISP-R1`):

      * You need to advertise all directly connected networks and loopback interfaces that OSPF should learn about and share with its neighbors. The `network` command specifies the networks to include in OSPF, along with their wildcard masks and the area ID. We are using `area 0` for all internal routing.

    On `R1 (core-r1)`:

    ```
    R1(config)# router ospf 1
    R1(config-router)# network 172.16.1.1 0.0.0.0 area 0       ! Loopback0
    R1(config-router)# network 10.0.0.0 0.0.0.3 area 0        ! R1-R2 Link 1
    R1(config-router)# network 10.0.0.4 0.0.0.3 area 0        ! R1-R2 Link 2
    R1(config-router)# network 10.0.1.0 0.0.0.3 area 0        ! R1-DSW-R3 link
    R1(config-router)# network 10.0.1.4 0.0.0.3 area 0        ! R1-DSW-R4 link
    R1(config-router)# network 203.0.113.0 0.0.0.3 area 0     ! R1-ISP-R1 link (Gi0/0)
    R1(config-router)# exit
    ```

    On `R2 (core-r2)`:

    ```
    R2(config)# router ospf 1
    R2(config-router)# network 172.16.2.1 0.0.0.0 area 0       ! Loopback0
    R2(config-router)# network 10.0.0.0 0.0.0.3 area 0        ! R2-R1 Link 1
    R2(config-router)# network 10.0.0.4 0.0.0.3 area 0        ! R2-R1 Link 2
    R2(config-router)# network 10.0.1.8 0.0.0.3 area 0        ! R2-DSW-R3 link
    R2(config-router)# network 10.0.1.12 0.0.0.3 area 0       ! R2-DSW-R4 link
    R2(config-router)# network 203.0.113.4 0.0.0.3 area 0     ! R2-ISP-R1 link (Gi0/0 on R2)
    R2(config-router)# exit
    ```

    On `ISP-R1`:

      * Note: For `ISP-R1`, we'll include its loopback and the links to `R1` and `R2`. If you later configure it to simulate an Internet gateway, you'd add default routes or external routing.

    <!-- end list -->

    ```
    ISP-R1(config)# router ospf 1
    ISP-R1(config-router)# network 172.16.6.1 0.0.0.0 area 0      ! Loopback0
    ISP-R1(config-router)# network 203.0.113.0 0.0.0.3 area 0     ! ISP-R1-R1 link (Gi1/0)
    ISP-R1(config-router)# network 203.0.113.4 0.0.0.3 area 0     ! ISP-R1-R2 link (Gi2/0)
    ISP-R1(config-router)# exit
    ```

  * C. Configure OSPF Networks on Distribution Switches (`DSW-R3`, `DSW-R4`):

      * Remember to advertise the SVI networks (VLANs), the routed physical links to the Core and between DSWs, and the loopback.
      * Important: Set your VLAN SVIs as `passive-interface`. This prevents OSPF hello packets from being sent into your end-user VLANs, which is a security and efficiency best practice.

    On `DSW-R3`:

    ```
    DSW-R3(config)# router ospf 1
    DSW-R3(config-router)# network 172.16.3.1 0.0.0.0 area 0       ! Loopback0
    DSW-R3(config-router)# network 10.0.1.0 0.0.0.3 area 0        ! DSW-R3 to R1 Core
    DSW-R3(config-router)# network 10.0.1.8 0.0.0.3 area 0        ! DSW-R3 to R2 Core
    DSW-R3(config-router)# network 10.0.3.0 0.0.0.3 area 0        ! DSW-DSW Interconnect (Fa0/9)
    DSW-R3(config-router)# network 10.0.3.4 0.0.0.3 area 0        ! DSW-DSW Backup (Fa0/10)
    DSW-R3(config-router)# network 192.168.10.0 0.0.0.255 area 0 ! VLAN 10 (Sales)
    DSW-R3(config-router)# network 192.168.20.0 0.0.0.255 area 0 ! VLAN 20 (HR)
    DSW-R3(config-router)# network 192.168.99.0 0.0.0.255 area 0 ! VLAN 99 (Management)
    DSW-R3(config-router)# passive-interface Vlan10
    DSW-R3(config-router)# passive-interface Vlan20
    DSW-R3(config-router)# passive-interface Vlan99
    DSW-R3(config-router)# exit
    ```

    On `DSW-R4`:

    ```
    DSW-R4(config)# router ospf 1
    DSW-R4(config-router)# network 172.16.4.1 0.0.0.0 area 0       ! Loopback0
    DSW-R4(config-router)# network 10.0.1.4 0.0.0.3 area 0        ! DSW-R4 to R1 Core
    DSW-R4(config-router)# network 10.0.1.12 0.0.0.3 area 0       ! DSW-R4 to R2 Core
    DSW-R4(config-router)# network 10.0.3.0 0.0.0.3 area 0        ! DSW-DSW Interconnect (Fa0/9)
    DSW-R4(config-router)# network 10.0.3.4 0.0.0.3 area 0        ! DSW-DSW Backup (Fa0/10)
    DSW-R4(config-router)# network 192.168.10.0 0.0.0.255 area 0 ! VLAN 10 (Sales)
    DSW-R4(config-router)# network 192.168.20.0 0.0.0.255 area 0 ! VLAN 20 (HR)
    DSW-R4(config-router)# network 192.168.99.0 0.0.0.255 area 0 ! VLAN 99 (Management)
    DSW-R4(config-router)# passive-interface Vlan10
    DSW-R4(config-router)# passive-interface Vlan20
    DSW-R4(config-router)# passive-interface Vlan99
    DSW-R4(config-router)# exit
    ```

### 9.4 Verification Steps for Layer 3 Routing:

After configuring OSPF, verify that adjacency is established and routes are learned.

1.  Check OSPF Neighbor Adjacencies:

      * On `R1`, `R2`, `DSW-R3`, `DSW-R4`, `ISP-R1`:
        ```
        Router# show ip ospf neighbor
        ```
          * Expected Output: You should see neighbors listed with a "FULL" state. If you see "INIT" or "EXSTART", there's an issue with adjacency.

2.  Check OSPF Database:

      * On any OSPF router (e.g., `R1` or `DSW-R3`):
        ```
        Router# show ip ospf database
        ```
          * Expected Output: You should see Link-State Advertisements (LSAs) for all advertised networks and routers in Area 0.

3.  Check Routing Table:

      * On any OSPF router (e.g., `R1` or `DSW-R3`):
        ```
        Router# show ip route ospf
        ```
          * Expected Output: You should see routes for all your VLAN subnets (192.168.10.0/24, 192.168.20.0/24, 192.168.99.0/24) and all 10.0.x.x /30 links learned via OSPF.

4.  Test End-to-End Connectivity:

      * From any PC (e.g., `PC1` in VLAN 10), try to ping a PC in a different VLAN (e.g., `PC4` in VLAN 20, or `PC7` in VLAN 99).
      * Try to ping the loopback addresses of your Core routers (e.g., `ping 172.16.1.1` from a PC).
      * Expected Output: All these pings should now be successful, as Layer 3 routing is enabled\!


-----

## Section 10: Verify and Test First-Hop Redundancy (HSRP)

Goal: Confirm that HSRP is providing resilient first-hop redundancy for your VLANs by verifying its initial state and then observing its failover capabilities.

10.1 Verify HSRP Initial State

First, let's check the current HSRP state on both `DSW-R3` and `DSW-R4` to confirm they are in their intended Active/Standby roles.

  * Action: On `DSW-R3` and `DSW-R4`, go to privileged EXEC mode and use the `show standby` or `show standby brief` command. The `brief` option provides a concise summary, which is often sufficient for a quick check.

    On `DSW-R3` and `DSW-R4`:

    ```
    Switch# show standby brief
    ```

  * Expected Output:

      * For VLANs 10 and 99:
          * `DSW-R3` should show its state as `Active`.
          * `DSW-R4` should show its state as `Standby`.
      * For VLAN 20:
          * `DSW-R4` should show its state as `Active`.
          * `DSW-R3` should show its state as `Standby`.
      * The "Active virtual IP address" for each group should be `192.168.X.254`.
      * Priorities should be `110` for the Active router and `100` for the Standby router.
      * Preempt should be implicitly active based on priority differences and the `standby preempt` command you configured.


10.2 Test HSRP Failover (Scenario 1: Primary Active SVI Failure)

This test simulates a failure on the currently Active HSRP router for a specific VLAN. Since your Packet Tracer does not support `standby track`, we'll simulate the most direct form of failure affecting HSRP: the SVI itself going down.

  * Scenario: We will test failover for VLAN 10, where `DSW-R3` is initially Active.

  * Action:

    1.  On a PC in VLAN 10 (e.g., `PC1`):

          * Before Failure: Perform a `traceroute` to a destination beyond your local VLAN, such as a Core router's Loopback IP (e.g., `traceroute 172.16.1.1`).
          * Expected Observation: The first hop in the `traceroute` output should be `192.168.10.1` (the IP address of `DSW-R3`'s VLAN 10 SVI). This confirms `DSW-R3` is the active gateway.

    2.  On `DSW-R3`: Go to interface configuration mode for `Vlan10` and shut it down. This simulates a critical failure of that SVI.

        ```
        DSW-R3(config)# interface Vlan10
        DSW-R3(config-if)# shutdown
        ```

    3.  Observe: Immediately check the console of `DSW-R4`. You should see syslog messages indicating HSRP state changes, specifically `DSW-R4` transitioning to the `Active` state for VLAN 10.

    4.  Verify New State:

          * On `DSW-R3`: Run `show standby brief` for `Vlan10`. It should now show `Vlan10` as `Init` or `Disabled`.
          * On `DSW-R4`: Run `show standby brief` for `Vlan10`. It should now clearly show `Vlan10` as `Active`.

    5.  Test Connectivity & Path Change:

          * From the same PC in VLAN 10 (e.g., `PC1`), try to ping a PC in a different VLAN (e.g., `PC4` in VLAN 20) or the Core router loopback (e.g., `172.16.1.1`).
          * Crucial Observation: Perform another `traceroute` to the same destination (e.g., `traceroute 172.16.1.1`).
          * Expected Result: Connectivity should continue without interruption (or with minimal, sub-second packet loss during the failover event). More importantly, the first hop in the `traceroute` output should now be `192.168.10.2` (the IP address of `DSW-R4`'s VLAN 10 SVI). This vividly demonstrates that `DSW-R4` has taken over the active gateway role.

  * Action (Restore Primary):

    1.  On `DSW-R3`: Re-enable `Vlan10` by bringing the interface back up.
        ```
        DSW-R3(config)# interface Vlan10
        DSW-R3(config-if)# no shutdown
        ```
    2.  Observe: Watch the consoles again. `DSW-R3` (due to its higher priority and the `preempt` command) should quickly regain the `Active` role for VLAN 10.
    3.  Verify Restored State & Path:
          * On `DSW-R3`: `show standby brief` for `Vlan10` should show `Active`.
          * On `DSW-R4`: `show standby brief` for `Vlan10` should show `Standby`.
          * From `PC1`, perform a final `traceroute` to `172.16.1.1`. The first hop should revert back to `192.168.10.1`.
    4.  Test Connectivity: Confirm connectivity from `PC1` to other VLANs/Core is still working.

10.3 Test HSRP Failover (Scenario 2: Primary Standby SVI Failure)

This test ensures that if the Standby router's SVI fails, it simply goes offline without affecting the Active router's role, and no unwanted failover occurs.

  * Scenario: We will test failover for VLAN 20, where `DSW-R4` is initially Active and `DSW-R3` is Standby.

  * Action:

    1.  On `DSW-R3`: Go to interface configuration mode for `Vlan20` and shut it down.
        ```
        DSW-R3(config)# interface Vlan20
        DSW-R3(config-if)# shutdown
        ```
    2.  Observe: Check the console of `DSW-R4`. There should be no change in `DSW-R4`'s HSRP state for VLAN 20 (it should remain `Active`).
    3.  Verify State:
          * On `DSW-R4`: `show standby brief` for `Vlan20` should still show `Active`.
          * On `DSW-R3`: `show standby brief` for `Vlan20` should show `Init` or `Disabled`.
    4.  Test Connectivity: From a PC in VLAN 20 (e.g., `PC4`), ping a PC in a different VLAN or a Core router loopback.
          * Expected Result: Connectivity should be uninterrupted.

  * Action (Restore Standby):

    1.  On `DSW-R3`: Re-enable `Vlan20`.
        ```
        DSW-R3(config)# interface Vlan20
        DSW-R3(config-if)# no shutdown
        ```
    2.  Observe: `DSW-R3` should quickly return to the `Standby` state for VLAN 20.

-----

## Section 11: Implement Access Control Lists (ACLs)

Goal: To enhance network security by controlling communication between VLANs and limiting management access to network devices.

11.1 Introduction to Access Control Lists (ACLs)

ACLs are ordered sets of rules that control network traffic. They work by filtering packets based on criteria such as source IP address, destination IP address, protocol, port numbers, and more.

  * Implicit Deny: Every ACL, by default, has an implicit `deny any` statement at the very end. This means if a packet does not match any `permit` statement in the ACL, it will be dropped. This is why it's crucial to explicitly `permit` any traffic you *do* want to allow, especially after `deny` statements.
  * Placement: ACLs are applied to interfaces (or VTY lines) in a specific direction (inbound or outbound).
      * Inbound: Filters traffic coming *into* the interface before the router processes it.
      * Outbound: Filters traffic leaving *out of* the interface after the router processes it.
      * General Rule for Extended ACLs: Place them as close to the source of the traffic you want to filter as possible.
      * General Rule for Standard ACLs: Place them as close to the destination of the traffic you want to filter as possible. (Though for VTY lines, they are applied directly to the VTY lines themselves).
  * Types used in this lab:
      * Named Extended ACLs: Offer flexible filtering based on source/destination IP, protocol, and port numbers. They are easier to read and modify than numbered ACLs.
      * Named Standard ACLs: Filter solely based on source IP address. Useful for simple source-based filtering or controlling VTY access.

### Section 11.2 Scenario 1: Restrict HR (VLAN 20) from Accessing Sales (VLAN 10) - *Enhanced with Port Filtering*

This is a common security requirement: preventing direct communication between specific departments while allowing others to function normally.

  * Goal: PCs in VLAN 20 (HR) should NOT be able to communicate with PCs in VLAN 10 (Sales) for common services like web (HTTP/HTTPS), FTP, Telnet, SSH, and basic ping (ICMP). All other inter-VLAN communication (e.g., HR to Management, Sales to Management, Sales to HR) should remain permitted.

  * ACL Type: Named Extended ACL.

  * Placement: We will apply this ACL inbound on the `Vlan20` interface of both `DSW-R3` and `DSW-R4`. Traffic originating from VLAN 20 attempting to reach other VLANs enters the DSWs via this SVI. Applying it here ensures filtering happens early.

  * ACL Name: `NO_HR_TO_SALES`

  * Action: Configure the named extended ACL on `DSW-R3` and `DSW-R4`.

    On `DSW-R3`:

    ```
    DSW-R3(config)# ip access-list extended NO_HR_TO_SALES
    DSW-R3(config-ext-nacl)# deny icmp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255     ! Deny Ping
    DSW-R3(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq www ! Deny HTTP (Port 80)
    DSW-R3(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq 443 ! Deny HTTPS (Port 443)
    DSW-R3(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq ftp ! Deny FTP Control (Port 21)
    DSW-R3(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq ftp-data ! Deny FTP Data (Port 20)
    DSW-R3(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq telnet ! Deny Telnet (Port 23)
    DSW-R3(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq ssh   ! Deny SSH (Port 22)
    DSW-R3(config-ext-nacl)# deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255         ! Deny any other IP traffic from HR to Sales
    DSW-R3(config-ext-nacl)# permit ip any any                                            ! Explicitly permit all other traffic
    DSW-R3(config-ext-nacl)# exit

    DSW-R3(config)# interface Vlan20
    DSW-R3(config-if)# ip access-group NO_HR_TO_SALES in                                  ! Apply the ACL inbound on Vlan20
    DSW-R3(config-if)# exit
    ```

    On `DSW-R4`:

    ```
    DSW-R4(config)# ip access-list extended NO_HR_TO_SALES
    DSW-R4(config-ext-nacl)# deny icmp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255     ! Deny Ping
    DSW-R4(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq www ! Deny HTTP (Port 80)
    DSW-R4(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq 443 ! Deny HTTPS (Port 443)
    DSW-R4(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq ftp ! Deny FTP Control (Port 21)
    DSW-R4(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq ftp-data ! Deny FTP Data (Port 20)
    DSW-R4(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq telnet ! Deny Telnet (Port 23)
    DSW-R4(config-ext-nacl)# deny tcp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 eq ssh   ! Deny SSH (Port 22)
    DSW-R4(config-ext-nacl)# deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255         ! Deny any other IP traffic from HR to Sales
    DSW-R4(config-ext-nacl)# permit ip any any                                            ! Explicitly permit all other traffic
    DSW-R4(config-ext-nacl)# exit

    DSW-R4(config)# interface Vlan20
    DSW-R4(config-if)# ip access-group NO_HR_TO_SALES in                                  ! Apply the ACL inbound on Vlan20
    DSW-R4(config-if)# exit
    ```

  * Verification for Scenario 1 (Revised):

    1.  From `PC4` (VLAN 20) to `PC1` (VLAN 10):
          * Try to `ping 192.168.10.10` (PC1).
          * Expected Result: Ping should fail (due to `deny icmp`).
          * *If you had a web server or FTP server on PC1:* Try to connect via HTTP, HTTPS, FTP, Telnet, or SSH. Expected Result: Connection attempts should fail for these specific services.
    2.  From `PC1` (VLAN 10) to `PC4` (VLAN 20):
          * Try to ping `192.168.20.10` (PC4).
          * Expected Result: Ping should succeed (traffic from Sales to HR is not denied).
    3.  From `PC4` (VLAN 20) to `PC7` (VLAN 99):
          * Try to ping `192.168.99.11` (PC7).
          * Expected Result: Ping should succeed (HR to Management is not denied).

Important Observation for Ping from Sales (VLAN 10) to HR (VLAN 20):
When `PC1` (VLAN 10) attempts to ping `PC4` (VLAN 20), you will observe a "Request timed out" message. Your suspicion is correct: this is because the ACL on `Vlan20` is blocking the ICMP Echo Reply packet from `PC4` back to `PC1`.

Even though the rule `deny icmp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255` is intended to prevent traffic *from HR to Sales*, it also matches the return traffic (source: VLAN 20, destination: VLAN 10, protocol: ICMP). This highlights a critical aspect of ACL placement: an `in` ACL on an interface filters *all* traffic entering that interface, including return traffic from hosts in that segment.


11.3 Scenario 2: Limit Telnet/SSH Access to Management VLAN (VLAN 99)

This scenario ensures that only authorized devices (those in the management VLAN) can remotely access your network devices for configuration.

  * Goal: Only devices in VLAN 99 (network `192.168.99.0/24`) should be able to Telnet or SSH to the Core Routers (`R1`, `R2`, `ISP-R1`) and Distribution Switches (`DSW-R3`, `DSW-R4`).

  * ACL Type: Named Standard ACL, as we only need to filter based on the source IP address.

  * Placement: Applied inbound to the `vty` (Virtual Terminal) lines on each device.

  * ACL Name: `MGMT_ACCESS`

  * Action: Configure the named standard ACL and apply it to the VTY lines on each specified device.

    On `DSW-R3`, `DSW-R4`, `R1`, `R2`, and `ISP-R1`:

    ```
    Router(config)# ip access-list standard MGMT_ACCESS
    Router(config-std-nacl)# permit 192.168.99.0 0.0.0.255   ! Permit devices from Management VLAN
    Router(config-std-nacl)# exit

    Router(config)# line vty 0 15                           ! Apply to all virtual terminal lines
    Router(config-line)# access-class MGMT_ACCESS in        ! Apply the ACL inbound
    Router(config-line)# login local                         ! Ensure local authentication is configured
    Router(config-line)# transport input telnet ssh         ! Allow both Telnet and SSH (or specific if preferred)
    Router(config-line)# exit
    ```

      * Note: If you haven't already, ensure you have local usernames and passwords configured on each device for `login local` to work (e.g., `username admin privilege 15 secret cisco`).

  * Verification for Scenario 2:

    1.  From `PC7` (VLAN 99):
          * Try to `telnet 172.16.1.1` (R1's Loopback0) or `telnet 172.16.3.1` (DSW-R3's Loopback0).
          * Expected Result: Telnet/SSH attempts should succeed, and you should be prompted for credentials.
    2.  From `PC1` (VLAN 10) or `PC4` (VLAN 20):
          * Try to `telnet 172.16.1.1` or `telnet 172.16.3.1`.
          * Expected Result: Telnet/SSH attempts should fail (connection refused or timeout).


11.4 General ACL Verification Commands:

Use these commands to inspect your ACLs and their application:

  * `show ip access-lists`: Shows all configured IP ACLs.
  * `show running-config | section access-list`: Shows ACLs from the running configuration.
  * `show running-config | include access-group`: Shows where `access-group` commands are applied on interfaces.
  * `show running-config | section line vty`: Shows ACL application on VTY lines.

-----

## Section 12: Configure Network Address Translation (NAT)

Goal: To allow hosts in your internal private VLANs (`192.168.10.0/24`, `192.168.20.0/24`, `192.168.99.0/24`) to communicate with the simulated external network (represented by `ISP-R1`'s Loopback0 `172.16.6.1`). We will use Dynamic NAT with Port Address Translation (PAT), also known as "overload," which allows many private IP addresses to share a single public IP address.

Mechanism:
When an internal host initiates traffic to an external destination, the NAT router (`R1` or `R2` in this case) will:

1.  Translate the internal private source IP address and port number to the router's public outside interface IP address and a unique port number.
2.  Forward the packet to the outside network.
3.  When the response comes back, it translates it back to the original internal IP and port.

Key Steps:

1.  Identify Inside and Outside Interfaces:

      * Outside Interfaces: These are the interfaces connected to the "Internet" or public network.
          * On `R1`: `GigabitEthernet0/0` (IP: `203.0.113.1`)
          * On `R2`: `GigabitEthernet0/0` (IP: `203.0.113.5`)
      * Inside Interfaces: These are the interfaces facing your internal private networks, where traffic originates from or is destined for private IP addresses.
          * On `R1`: `GigabitEthernet1/0` (to R2), `GigabitEthernet3/0` (to DSW-R3), `GigabitEthernet4/0` (to DSW-R4), `Loopback0`
          * On `R2`: `GigabitEthernet1/0` (to R1), `GigabitEthernet3/0` (to DSW-R3), `GigabitEthernet4/0` (to DSW-R4), `Loopback0`

2.  Define "Interesting" Traffic with a Standard ACL:

      * This ACL specifies which internal source IP addresses are allowed to be translated. We'll include all your user VLAN subnets.

3.  Configure Dynamic PAT (Overload):

      * This command links the ACL defining the "interesting" traffic to the outside interface and enables PAT using that interface's IP address.


12.1 Configure NAT on R1

  * Action: First, define the inside/outside interfaces, then create the ACL, and finally link them together for PAT.

    On `R1`:

    ```
    R1(config)# interface GigabitEthernet0/0
    R1(config-if)# ip nat outside
    R1(config-if)# exit

    R1(config)# interface GigabitEthernet1/0
    R1(config-if)# ip nat inside
    R1(config-if)# exit

    R1(config)# interface GigabitEthernet3/0
    R1(config-if)# ip nat inside
    R1(config-if)# exit

    R1(config)# interface GigabitEthernet4/0
    R1(config-if)# ip nat inside
    R1(config-if)# exit

    R1(config)# interface Loopback0
    R1(config-if)# ip nat inside
    R1(config-if)# exit

    R1(config)# ip access-list standard NAT_INTERNAL_TRAFFIC
    R1(config-std-nacl)# permit 192.168.10.0 0.0.0.255   ! Sales VLAN
    R1(config-std-nacl)# permit 192.168.20.0 0.0.0.255   ! HR VLAN
    R1(config-std-nacl)# permit 192.168.99.0 0.0.0.255   ! Management VLAN
    R1(config-std-nacl)# exit

    R1(config)# ip nat inside source list NAT_INTERNAL_TRAFFIC interface GigabitEthernet0/0 overload
    ```

12.2 Configure NAT on R2

  * Action: Repeat the configuration steps for `R2`.

    On `R2`:

    ```
    R2(config)# interface GigabitEthernet0/0
    R2(config-if)# ip nat outside
    R2(config-if)# exit

    R2(config)# interface GigabitEthernet1/0
    R2(config-if)# ip nat inside
    R2(config-if)# exit

    R2(config)# interface GigabitEthernet3/0
    R2(config-if)# ip nat inside
    R2(config-if)# exit

    R2(config)# interface GigabitEthernet4/0
    R2(config-if)# ip nat inside
    R2(config-if)# exit

    R2(config)# interface Loopback0
    R2(config-if)# ip nat inside
    R2(config-if)# exit

    R2(config)# ip access-list standard NAT_INTERNAL_TRAFFIC
    R2(config-std-nacl)# permit 192.168.10.0 0.0.0.255   ! Sales VLAN
    R2(config-std-nacl)# permit 192.168.20.0 0.0.0.255   ! HR VLAN
    R2(config-std-nacl)# permit 192.168.99.0 0.0.0.255   ! Management VLAN
    R2(config-std-nacl)# exit

    R2(config)# ip nat inside source list NAT_INTERNAL_TRAFFIC interface GigabitEthernet0/0 overload
    ```

12.3 Verify NAT Functionality

Now, let's confirm that NAT is correctly translating your private IP addresses. We'll use `ISP-R1`'s Loopback0 (`172.16.6.1`) as our "Internet" destination.

  * Action:
    1.  From a PC (e.g., `PC1` in VLAN 10):
          * Try to ping `172.16.6.1`.
          * Expected Result: Ping should succeed.
    2.  On `R1` or `R2` (the router that `PC1`'s traffic egresses through, which will depend on OSPF routing):
          * Use the following commands to view NAT translations and statistics.
        <!-- end list -->
        ```
        Router# show ip nat translations
        Router# show ip nat statistics
        ```
          * Expected Observation (`show ip nat translations`): You should see an entry showing your PC's private IP address (`192.168.10.10`) being translated to the public IP address of `R1`'s or `R2`'s `GigabitEthernet0/0` interface (e.g., `203.0.113.1` or `203.0.113.5`) with a unique port number.

          * Expected Observation (`show ip nat statistics`): This command will show the number of active translations, hits, misses, and other relevant NAT statistics.

-----

## Section 13: Implement Spanning Tree Protocol (STP) Enhancements

Goal: To improve the responsiveness, security, and stability of your access layer by configuring PortFast, BPDU Guard, Root Guard, and Loop Guard on your Access Switches (`SW1` to `SW4`).

13.1 Understanding Enhanced STP Features

To ensure your Layer 2 network is stable, secure, and responsive, it's essential to configure several enhancements to Spanning Tree Protocol (STP).

  * PortFast:

      * Purpose: By default, when a port comes up, STP goes through listening and learning states (taking about 30 seconds) before entering the forwarding state. This delay can cause issues for end devices (like PCs and IP Phones) that need immediate network access. PortFast immediately brings an access port to the forwarding state, bypassing these listening/learning states.
      * Crucial Note: PortFast must only be enabled on ports connected to end devices, never on ports connected to other switches (or hubs that could connect to switches). Enabling PortFast on a trunk or uplink port could create temporary switching loops.

  * BPDU Guard:

      * Purpose: BPDU Guard provides a layer of security by preventing unauthorized switches from being introduced into your network. If a port configured with BPDU Guard receives a Bridge Protocol Data Unit (BPDU) – which is a signal from another switch – the port will immediately shut down (go into an `err-disabled` state).
      * Benefit: This protects your STP domain from accidental or malicious loops and ensures your designated root bridge remains stable.
      * Usage: It's typically enabled on all access ports where PortFast is configured.

  * Root Guard:

      * Purpose: Prevents ports from becoming a root port, ensuring that your designated root bridge (typically your Distribution Layer switches in this design) always remains the root. If a port configured with Root Guard receives a superior BPDU (indicating a better root bridge), the port is put into a `root-inconsistent` (blocking) state.
      * Where to Apply: On ports that should never lead to the root bridge. In your topology, this is primarily on the access ports (`Fa0/5-24`) that connect to end devices, as you don't want a PC or a rogue hub/switch trying to become the STP root.

  * Loop Guard:

      * Purpose: Protects against unidirectional link failures that could create loops. If a non-designated (blocking) port stops receiving BPDUs but is still receiving other traffic, Loop Guard puts it into a `loop-inconsistent` (blocking) state, preventing it from transitioning to forwarding and creating a loop.
      * Where to Apply: On blocking ports where you expect to receive BPDUs, but which might unexpectedly stop receiving them (e.g., due to a unidirectional link issue). In this topology, this is most relevant on the EtherChannel uplinks (`Port-channel10`, `Port-channel20`, etc.) from your Access Switches to the Distribution Switches, where redundant paths exist.


13.2 Configure STP Enhancements on Access Switches (SW1 - SW4)

We will apply PortFast and BPDU Guard to your end-device facing ports, and Root Guard and Loop Guard where appropriate for stability.

  * Action: Go to global configuration mode on each Access Switch (`SW1`, `SW2`, `SW3`, `SW4`) and apply the commands.

    On `SW1`, `SW2`, `SW3`, and `SW4`:

    1.  Configure PortFast, BPDU Guard, and Root Guard (on End-Device Access Ports):

        ```
        Switch(config)# interface range FastEthernet0/5 - 24
        Switch(config-if-range)# spanning-tree portfast                  ! Enable PortFast
        Switch(config-if-range)# spanning-tree bpduguard enable         ! Enable BPDU Guard
        Switch(config-if-range)# spanning-tree guard root               ! Enable Root Guard
        Switch(config-if-range)# exit
        ```

          * Confirmation Prompt: If prompted for PortFast (e.g., "%Warning: Portfast should only be enabled on ports connected to a single host."), type `y` or hit `Enter`.

    2.  Configure Loop Guard (on Uplink Port-Channels):

          * Recall the Port-Channels from Access Switches to DSW-R3 and DSW-R4.
          * On `SW1`: `Port-channel1` (to DSW-R3) and `Port-channel2` (to DSW-R4)
          * On `SW2`: `Port-channel1` (to DSW-R3) and `Port-channel2` (to DSW-R4)
          * On `SW3`: `Port-channel1` (to DSW-R3) and `Port-channel2` (to DSW-R4)
          * On `SW4`: `Port-channel1` (to DSW-R3) and `Port-channel2` (to DSW-R4)

        <!-- end list -->

        ```
        Switch(config)# interface Port-channel1
        Switch(config-if)# spanning-tree guard loop
        Switch(config-if)# exit

        Switch(config)# interface Port-channel2
        Switch(config-if)# spanning-tree guard loop
        Switch(config-if)# exit

        ! Repeat for the respective Port-Channels on SW2, SW3, SW4:
        ! For SW2: Port-channel1, Port-channel2
        ! For SW3: Port-channel1, Port-channel2
        ! For SW4: Port-channel1, Port-channel2
        ```
        Unfortunately Packet tracer does not afford users room to enable loopGuard.

13.3 Verify STP Enhancements

  * Action: Use `show` commands to confirm that these features are enabled on your desired interfaces.

    On `SW1` (or any Access Switch):

    ```
    Switch# show spanning-tree interface FastEthernet0/5 detail
    ```

      * Expected Output: Look for "PortFast enable", "BPDU Guard is enabled", and "Root Guard is enabled" within the detailed output.


    ```
    Switch# show spanning-tree interface Port-channel10 detail
    ```

      * Expected Output: Look for "Loop Guard is enabled" within the detailed output.

    You can also see a summary with:

    ```
    Switch# show spanning-tree summary totals
    ```

      * This command provides a global overview, including how many ports have PortFast, BPDU Guard, and various STP guard features enabled.

  * Testing `err-disabled` states (Conceptual/Advanced for Packet Tracer):

      * To test `BPDU Guard`: Connect another switch (that sends BPDUs) to an `Fa0/5-24` port. The port should immediately go into an `err-disabled` state. Check with `show interface status err-disabled`. To recover, remove the rogue device, then use `shutdown` followed by `no shutdown` on the affected interface.
      * To test `Root Guard`: This is more complex in Packet Tracer, as it involves configuring another simulated switch with a very low STP priority and connecting it to an `Fa0/5-24` port. The port should then enter a `root-inconsistent` blocking state.
      * To test `Loop Guard`: This is very challenging to simulate directly in Packet Tracer as it requires a specific unidirectional link failure scenario. Conceptually, if a Port-channel stopped receiving BPDUs but the line protocol remained up, Loop Guard would prevent it from forwarding and creating a loop.

-----

## Section 14: Implement Dynamic Host Configuration Protocol (DHCP) Server

Goal: To configure `DSW-R3` and `DSW-R4` as DHCP servers for your internal VLANs (Sales, HR, Management), allowing client PCs and other devices to automatically obtain their IP addresses, default gateway, and DNS server information.

Key Concepts for DHCP Server:

  * DHCP Pool: A defined range of IP addresses that the DHCP server can assign.
  * Excluded Addresses: Specific IP addresses within a pool's range that the DHCP server should *not* assign (e.g., static IPs for routers, servers, printers).
  * Default Router: The IP address of the default gateway for clients in that pool (which will be your HSRP virtual IP for each VLAN).
  * DNS Server: The IP address of the DNS server that clients should use. We'll use `Server1` for this, so we'll assign it a static IP first.

We will configure identical DHCP pools on both `DSW-R3` and `DSW-R4` for redundancy.
Here's a breakdown of why this approach (DHCP on DSWs, other services on a dedicated server) is considered a good practice:

1.  DHCP Redundancy and Proximity (DSWs as DHCP Servers):
    * High Availability: By configuring DHCP pools on *both* `DSW-R3` and `DSW-R4`, you achieve DHCP redundancy. Since these are also your HSRP active/standby gateways for each VLAN, if one DSW fails, the other seamlessly takes over both the routing (HSRP) and DHCP server responsibilities. Clients will continue to receive IP addresses without interruption.
    * No `ip helper-address` Needed: Because the router acting as the VLAN's default gateway (the SVI on the DSW) is also the DHCP server for that VLAN, there's no need to configure `ip helper-address` (DHCP relay) on the SVI. This simplifies the configuration and reduces potential points of failure by not having to forward DHCP requests to another device.
    * Performance/Proximity: The Distribution Layer is typically physically and logically "close" to the access layer (where end devices reside). Having the DHCP server here means DHCP requests don't have to traverse deep into the core network or to a centralized server farm, leading to faster IP address assignment.

2.  Separation of Services and Specialization (DNS, TFTP, NTP, Syslog on Server1):
    * Resource Allocation: Dedicated server hardware (`Server1` in our case) is typically built with more CPU, RAM, and storage than a network device. These resources are better suited for running application-layer services like DNS, TFTP, NTP, and Syslog, which can consume significant resources, especially in larger networks.
    * Scalability: As your network grows and the demands on these services increase, it's much easier to scale up a dedicated server (by adding resources or deploying more servers) than it is to upgrade the capabilities of a router or switch.
    * Management Focus: Network devices are optimized for packet forwarding and routing. Servers are optimized for hosting applications and data. Keeping these roles separate allows administrators to specialize in managing each domain without one impacting the other.
    * Troubleshooting Simplicity: If you encounter a network performance issue, you can focus on the network devices without worrying that an overloaded DNS service running on a router might be the root cause. Conversely, if a service like DNS fails, it doesn't directly impact the core routing and switching functions.
    * Security Posture: Centralizing these services on a dedicated server allows for more focused security hardening and patching for server-specific vulnerabilities, rather than trying to apply server-level security to network hardware.
    * Backup & Recovery: Dedicated servers typically have more robust backup and disaster recovery mechanisms in place.

3.  Security through Segmentation (Management VLAN 99):
    * Placing `Server1` and other management-related devices (like `PC5`, `PC6`, `PC7` for admin access) within a dedicated `VLAN 99` (Management VLAN) is a strong security practice. This allows you to apply strict Access Control Lists (ACLs) to control who can access these sensitive management services, effectively isolating management traffic from general user traffic. (As we've done with ACLs already!)

In essence, this design balances the need for high availability and localized responsiveness for fundamental services (like DHCP) with the benefits of centralization, specialization, and robust management for other essential network services. It's a clean, efficient, and resilient architecture.


14.1 Configure Static IP for Server1 (DNS/TFTP/NTP/Syslog Server)

Before setting up DHCP, it's essential to assign a static IP address to your server so that clients can consistently find it. `Server1` will reside in VLAN 99 (Management).

  * Action: Go to `Server1` in Packet Tracer.
    1.  Click on `Server1`.
    2.  Go to the `Desktop` tab.
    3.  Click on `IP Configuration`.
    4.  Select `Static`.
    5.  Enter the following details:
          * IP Address: `192.168.99.10`
          * Subnet Mask: `255.255.255.0`
          * Default Gateway: `192.168.99.254` (HSRP Virtual IP for VLAN 99)
          * DNS Server: `192.168.99.10` (Server1 itself will act as the DNS server later)


14.2 Configure DHCP Server on DSW-R3

  * Action: Go to global configuration mode on `DSW-R3`.

      * First, exclude the addresses that are already statically assigned or reserved (HSRP virtual IPs and Server1's IP).
      * Then, create the DHCP pools for each VLAN.

    On `DSW-R3`:

    ```
    DSW-R3(config)# ip dhcp excluded-address 192.168.10.254   ! HSRP VIP for VLAN 10
    DSW-R3(config)# ip dhcp excluded-address 192.168.20.254   ! HSRP VIP for VLAN 20
    DSW-R3(config)# ip dhcp excluded-address 192.168.99.254   ! HSRP VIP for VLAN 99
    DSW-R3(config)# ip dhcp excluded-address 192.168.99.10    ! Server1's static IP

    DSW-R3(config)# ip dhcp pool SALES_VLAN_POOL
    DSW-R3(dhcp-config)# network 192.168.10.0 255.255.255.0
    DSW-R3(dhcp-config)# default-router 192.168.10.254
    DSW-R3(dhcp-config)# dns-server 192.168.99.10
    DSW-R3(dhcp-config)# domain-name MaverickAcademy.com                ! Optional: A local domain name
    DSW-R3(dhcp-config)# exit

    DSW-R3(config)# ip dhcp pool HR_VLAN_POOL
    DSW-R3(dhcp-config)# network 192.168.20.0 255.255.255.0
    DSW-R3(dhcp-config)# default-router 192.168.20.254
    DSW-R3(dhcp-config)# dns-server 192.168.99.10
    DSW-R3(dhcp-config)# domain-name MaverickAcademy.com
    DSW-R3(dhcp-config)# exit

    DSW-R3(config)# ip dhcp pool MANAGEMENT_VLAN_POOL
    DSW-R3(dhcp-config)# network 192.168.99.0 255.255.255.0
    DSW-R3(dhcp-config)# default-router 192.168.99.254
    DSW-R3(dhcp-config)# dns-server 192.168.99.10
    DSW-R3(dhcp-config)# domain-name MaverickAcademy.com
    DSW-R3(dhcp-config)# exit
    ```

14.3 Configure DHCP Server on DSW-R4

  * Action: Repeat the exact same DHCP configuration steps on `DSW-R4` for redundancy.

    On `DSW-R4`:

    ```
    DSW-R4(config)# ip dhcp excluded-address 192.168.10.254
    DSW-R4(config)# ip dhcp excluded-address 192.168.20.254
    DSW-R4(config)# ip dhcp excluded-address 192.168.99.254
    DSW-R4(config)# ip dhcp excluded-address 192.168.99.10

    DSW-R4(config)# ip dhcp pool SALES_VLAN_POOL
    DSW-R4(dhcp-config)# network 192.168.10.0 255.255.255.0
    DSW-R4(dhcp-config)# default-router 192.168.10.254
    DSW-R4(dhcp-config)# dns-server 192.168.99.10
    DSW-R4(dhcp-config)# domain-name MaverickAcademy.com
    DSW-R4(dhcp-config)# exit

    DSW-R4(config)# ip dhcp pool HR_VLAN_POOL
    DSW-R4(dhcp-config)# network 192.168.20.0 255.255.255.0
    DSW-R4(dhcp-config)# default-router 192.168.20.254
    DSW-R4(dhcp-config)# dns-server 192.168.99.10
    DSW-R4(dhcp-config)# domain-name MaverickAcademy.com
    DSW-R4(dhcp-config)# exit

    DSW-R4(config)# ip dhcp pool MANAGEMENT_VLAN_POOL
    DSW-R4(dhcp-config)# network 192.168.99.0 255.255.255.0
    DSW-R4(dhcp-config)# default-router 192.168.99.254
    DSW-R4(dhcp-config)# dns-server 192.168.99.10
    DSW-R4(dhcp-config)# domain-name MaverickAcademy.com
    DSW-R4(dhcp-config)# exit
    ```

14.4 Configure Client PCs for DHCP

  * Action: For each client PC (`PC1` through `PC7`), switch its IP configuration method to DHCP.
    1.  Click on the PC.
    2.  Go to the `Desktop` tab.
    3.  Click on `IP Configuration`.
    4.  Select `DHCP`.
    5.  The PC should automatically request and receive an IP address, subnet mask, default gateway, and DNS server. If it doesn't immediately, try clicking `Static` then `DHCP` again.


14.5 Verify DHCP Functionality

  * Action: Confirm that clients have received IP addresses from the correct pools and check DHCP server statistics.

    1.  On any Client PC (e.g., `PC1`):

          * Go to `Desktop` tab, then `Command Prompt`.
          * Type `ipconfig /all`
          * Expected Result: Verify that `PC1` has an IP address in the `192.168.10.0/24` range, with default gateway `192.168.10.254` and DNS server `192.168.99.10`. Repeat for other PCs (`PC3` in `192.168.20.0/24`, `PC5` in `192.168.99.0/24`).

    2.  On `DSW-R3` or `DSW-R4`:

          * Use the following commands in privileged EXEC mode:
            ```
            DSW-R3# show ip dhcp binding
            ```
              * Expected Result: This shows a list of IP addresses that have been leased to clients, along with their MAC addresses. You should see entries for your active PCs.
            <!-- end list -->
            ```
            DSW-R3# show ip dhcp pool
            ```
              * Expected Result: This command displays details about each configured DHCP pool, including the number of leased addresses and available addresses.

----

## Section 15: Configure DNS Service on Server

Goal: To enable the DNS service on `Server1` and create a record that resolves `maverickacademy.com` to `Server1`'s own IP address (`192.168.99.10`).

  * Action: Go to `Server1` in Packet Tracer and configure its DNS service.

    1.  Click on `Server1`.
    2.  Go to the `Services` tab.
    3.  In the left-hand pane, click on `DNS`.
    4.  Ensure the `DNS Service` is toggled `On`.
    5.  Under `DNS Records`, enter the following:
          * Name: `maverickacademy.com`
          * Type: Select `A Record` (This stands for "Address Record" and maps a domain name to an IPv4 address).
          * Address: `192.168.99.10` (This is Server1's static IP address)
    6.  Click the `Add` button.

15.1 Verify DNS Resolution

  * Action: From any of your client PCs (e.g., `PC1`, `PC3`, `PC5`), open the Command Prompt and test DNS resolution.

    1.  Click on any Client PC (e.g., `PC1`).
    2.  Go to the `Desktop` tab.
    3.  Click on `Command Prompt`.
    4.  Type:
        ```
        ping maverickacademy.com
        ```
          * Expected Result: You should see successful replies from `192.168.99.10`. This confirms that your PCs are correctly querying `Server1` for DNS, and `Server1` is resolving `maverickacademy.com` as expected.

    *(Optional verification)*: You can also use `nslookup` (if available on the Packet Tracer PC's command line, though `ping` usually uses DNS first).

    ```
    nslookup maverickacademy.com
    ```

      * Expected Result: It should show the DNS server (192.168.99.10) and then the address of `maverickacademy.com` as `192.168.99.10`.
