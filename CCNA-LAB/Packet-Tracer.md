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

## Lab Environment

* Simulation Platform: Cisco Packet Tracer (Latest Version Recommended)
* Device Types: Standard Packet Tracer Routers, Multilayer Switches, and 2960 Switches.
* Client Devices: Standard Packet Tracer PCs and Server.

## Core Protocols & Services Covered (Overall Series - Packet Tracer Scope)

This lab series aims for proficiency in the following areas, focusing on Packet Tracer's capabilities:

* Infrastructure Services: DHCP, DNS, basic NAT (Static/Dynamic)
* LAN Switching: VLANs, Trunking (802.1Q), SVI (Switched Virtual Interfaces), EtherChannel (LACP/PAgP), STP (Spanning Tree Protocol)
* Routing Protocols: OSPFv2 (IPv4), EIGRP (IPv4)
* First-Hop Redundancy: HSRP (Hot Standby Router Protocol)
* Security: Standard Access Control Lists (ACLs), Port Security
* Basic WAN: Static Routes to ISP, Default Routes
* Monitoring & Management: Basic CLI commands (`show` commands)
* Wireless LAN: Basic WLAN configuration with WPA2 PSK (using Packet Tracer's generic Wireless Router/AP)

---

## Lab Phase 1: Three-Tier Architecture

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

---

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
* `DNS/TFTP/NTP Server (Server1)`: A "Server" device
* `Client PC 1 (PC1)`: A "PC" device
* `Client PC 2 (PC2)`: A "PC" device
* `Client PC 3 (PC3)`: A "PC" device
* `Client PC 4 (PC4)`: A "PC" device
* `Cloud Object (Internet)`: Packet Tracer's "Cloud" device

---

## Detailed Connectivity (Interface:Device-Interface:Device - Packet Tracer Naming):

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

* `SW1 Fa0/5` : `PC1`
* `SW1 Fa0/6` : `Server1` (DNS/TFTP/NTP Server)
* `SW2 Fa0/5` : `PC2`
* `SW3 Fa0/5` : `PC3`
* `SW4 Fa0/5` : `PC4`

F. ISP-R1 to Internet Cloud (PT-Router to Cloud):

* `ISP-R1 Gi0/2` : `Cloud0` (Packet Tracer Cloud Object, connect via "DSL Modem" or "Cable Modem" if available in PT and desired for realism, then to Cloud's "Ethernet" port).

---

### 1.4 IP Addressing Scheme

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

### Next Steps for Implementation:

## \!\!\! IMPORTANT WARNING FOR ALL CONFIGURATION STEPS \!\!\!

Always be mindful of the specific capabilities of each device model.

This lab utilizes Cisco Catalyst 2960 switches at the Access Layer (ASW-1 to ASW-4). These are Layer 2-ONLY switches. They DO NOT SUPPORT Layer 3 routing features such as `ip routing`, `no switchport` on physical interfaces/Port-Channels, or direct IP addressing on data plane interfaces.

All configurations for ASWs in this document are tailored to their Layer 2 capabilities. Attempting to configure Layer 3 features on a 2960 will result in errors and a non-functional lab. A detailed explanation of this distinction and what *would* be configured on a multilayer switch is provided at the end of the configuration section for learning purposes.

-----

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

    B.  Configure Core Layer Routers (core-r1, core-r2, ISP-R1):
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

    D.  Configure Distribution Layer Switches (DSW-R3, DSW-R4) - Layer 2 Trunk Port-Channels (to Access Switches):
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

    E.  Configure Access Layer Switches (ASW-1 to ASW-4) - Layer 2 Trunk Port-Channels (Uplinks to Distribution):
    \* *Explanation for Learners:* The Access Switches (2960s) operate purely at Layer 2. Their uplinks to the Distribution Layer must be configured as Layer 2 Trunking EtherChannels to carry VLAN traffic from end devices up to the DSWs for routing. `ip routing` will NOT be enabled on these switches.
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


    F. Configure VLANs (Creation on all relevant switches):

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

    H. Configure Distribution Layer Switches (DSW-R3, DSW-R4) - VLAN SVIs:

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

    I. Configure End Devices (PC1-PC8, Server1):

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

### Section 9: Configuring Layer 3 Routing (OSPF)

This section will guide you through enabling IP routing on your Distribution Layer switches and configuring OSPF across all your Layer 3 devices (Core Routers and Distribution Switches). We will operate all internal OSPF routing within a single Area 0 for simplicity in this lab.

Goal: Allow all VLANs to communicate with each other and for all internal devices to learn routes to each other.

-----

9.1 Enable IP Routing on Distribution Switches

By default, Cisco multilayer switches act primarily as Layer 2 devices. To enable their Layer 3 routing capabilities (which is necessary for SVIs to function as gateways and to participate in routing protocols), you must explicitly enable IP routing.

  * Action: Go to global configuration mode (`conf t`) on `DSW-R3` and `DSW-R4`.

    On `DSW-R3` and `DSW-R4`:

    ```
    Switch(config)# ip routing
    ```

-----

9.2 Configure Routed Ports on Distribution Switches (Verification)

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

-----

9.3 Configure OSPF Routing Protocol

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

-----

9.4 Verification Steps for Layer 3 Routing:

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
