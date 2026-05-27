# CCNA Lab 1

> This lab was built as part of my learning process and progress  towards my CCNA journey with the resources learnt from Jeremy IT  Lab CCNA v1 (200-301) Videos Day 1 - Day 24

---

## Scenario
Two branch offices of a WAN are connecting and communicating with each other i.e. (Branch 1 and Branch 2)

- **(Main) Branch 1** — Hosts the IT, Maintenance, Development Team
- **(Clients) Branch 2** — Hosts the Clients 1, Clients 2

## Assumption
The main provides services to the two clients in a B2B  connectivity, hosting X services for the clients. All of the  devices connecting in a network can communicate with each other.

---
## Network Diagrams

### Connections and Interfaces (Layer 2)

![](LAYER2-LAYER3-LAB1.drawio.svg)

### IP Addressing (Layer 3)

![](IP%20DIAGRAM.drawio.svg)

---

## Abbreviations

| Abbreviation | Full Name                  |
| ------------ | -------------------------- |
| ER1          | Edge Router 1              |
| IMR1         | Internal Main Router 1     |
| IMR2         | Internal Main Router 2     |
| CS1          | Core Switch 1              |
| DS1          | Distribution Switch 1      |
| DS2          | Distribution Switch 2      |
| AS1          | Access Switch 1            |
| CR1          | Client Router 1            |
| NID          | Network ID                 |
| DG           | Default Gateway            |
| SVI          | Switched Virtual Interface |
| VLAN         | Virtual Local Area Network |
| CAN          | Campus Area Network        |
| SI           | Sub Interfaces             |

---

## Configuration Details Overview

The configuration details are given in the following file 
 [Configuration Details](Configuration%20Details.md)

---
## Design Decisions

### Internal Network 1

- A partial mesh topology is implemented between DS1, DS2, AS1, and AS2 to improve redundancy and ensure alternate paths are available in case of link failure
- DS1 is configured as the **primary root bridge for VLANs 10, 20, and 30** so that most traffic is centrally forwarded through the main distribution layer
- DS2 is configured as the **secondary root bridge for VLANs 10, 20, and 30** to provide failover support if DS1 becomes unavailable
- Inter-VLAN routing is handled using **SVIs** on the core switch to allow communication between VLANs within the internal network
- Edge ports are configured to allow immediate connectivity for end devices using **PortFast**
    - **BPDU Guard** is enabled to prevent accidental or unauthorized switch connections
    - **Root Guard** is applied on distribution downlinks to ensure access switches do not influence the STP root election
    - **Loop Guard** is used on uplinks to protect against unidirectional link failures and potential loops

---

### Internal Network 2

- Edge ports are configured with PortFast to allow fast network access for connected devices
    - **BPDU Guard is enabled** to prevent unauthorized switches from being introduced into the network
- AS3 and AS4 are connected using **EtherChannel** with multiple physical links to improve redundancy and bandwidth efficiency
- AS4 is configured as a trunk switch to carry VLAN traffic between CR1 and AS3
- CR1 is configured using **Router-on-a-Stick** to enable inter-VLAN routing for the client network

---

### External Network

- CR1 and CR2 routers are responsible for routing between the **internal networks and external connectivity**
- **Static routing** is used across the WAN to ensure all networks can communicate with each other reliably

---
## Challenges Observed

- STP configuration was initially challenging, especially when setting DS1 as the primary root bridge and DS2 as the secondary root bridge while maintaining consistent VLAN behavior across the network
- EtherChannel did not form correctly at first due to inconsistencies in channel configuration across member interfaces, requiring correction and alignment of settings on both ends
- Managing static routing became complex due to the number of networks involved, and required careful verification of next-hop addresses to ensure full end-to-end connectivity across all sites

---

## Key Takeaways

- Understood how enterprise networks are structured using a hierarchical design with core, distribution, and access layers
- Gained practical experience in configuring and verifying VLANs, trunk links, and inter-VLAN routing using SVIs and Router-on-a-Stick
- Improved understanding of STP behavior, especially root bridge selection and how it affects traffic flow in redundant topologies
- Learned how EtherChannel works in real scenarios and how small configuration mismatches can prevent link bundling
- Developed better understanding of static routing across multiple routers and how important consistent next-hop planning is in larger topologies
- Strengthened troubleshooting skills by identifying and fixing configuration issues across Layer 2 and Layer 3

---

## Improvements

- If I were to improve the design, I would replace static routing with a dynamic routing protocol such as OSPF, using multiple areas to improve scalability and routing efficiency
- Increase redundancy in the external network by adding additional links and alternative routing paths between WAN routers
- Improve the overall network design by introducing additional enterprise services such as DHCP and DNS to support automated address assignment and name resolution as the network scales
- Add more EtherChannel links where appropriate, including both Layer 2 trunk links and Layer 3 routed EtherChannels, to improve redundancy and bandwidth between key devices