# Enterprise WAN Architecture: Dual-Branch Inter-VLAN Routing

## 1. Project Executive Summary
This project demonstrates the design and implementation of a robust **Wide Area Network (WAN)** infrastructure connecting two geographically separated branch offices. The primary objective was to establish seamless connectivity between sites while maintaining strict logical separation of departments using **VLAN segmentation**.

In this simulation, I emulated a corporate expansion scenario where a primary headquarters (Site A) requires a stable link to a new remote branch (Site B). Instead of a flat network, I architected a hierarchical design that ensures broadcast containment, security, and efficient address management.

**Key Technologies:** Cisco Packet Tracer, VLANs (802.1Q), Router-on-a-Stick (ROAS), Static Routing, DHCP, Serial WAN.

---

## 2. IP Addressing Schema
The following table outlines the IP allocation for the network devices and their respective interfaces.

| Device | Interface | IP Address | Subnet Mask | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Router0 (Site A)** | G0/0.10 | 10.0.0.1 | 255.0.0.0 | VLAN 10 Gateway (Sales/Admin) |
| | G0/0.20 | 20.0.0.1 | 255.0.0.0 | VLAN 20 Gateway (IT/Support) |
| | S0/1/0 | 25.0.0.1 | 255.0.0.0 | WAN Link to Site B |
| **Router3 (Site B)** | G0/0.10 | 30.0.0.1 | 255.0.0.0 | VLAN 10 Gateway |
| | G0/0.20 | 40.0.0.1 | 255.0.0.0 | VLAN 20 Gateway |
| | S0/0/0 | 25.0.0.2 | 255.0.0.0 | WAN Link (DCE Side) |
| **PC0 (Site A)** | NIC | *DHCP* | 255.0.0.0 | Assigned via Router0 Pool |
| **PC3 (Site B)** | NIC | *DHCP* | 255.0.0.0 | Assigned via Router3 Pool |

---

## 3. Technical Implementation Details

My implementation focused on manually configuring the end-to-end network infrastructure for two distinct sites.

### A. Layer 2 Segmentation (Switching)
* **VLAN Configuration:** Created **VLAN 10** and **VLAN 20** on both site switches to segregate user traffic at the data link layer.
* **Trunking:** Configured `GigabitEthernet0/1` uplinks as **802.1Q Trunk ports** to allow multiple VLANs to traverse the single physical link to the router.
* **Access Control:** Assigned specific FastEthernet ports to their respective VLANs (e.g., `switchport access vlan 10`) to enforce security boundaries.

### B. Router-on-a-Stick (Inter-VLAN Routing)
To enable communication between the isolated VLANs without using expensive Layer 3 switches, I deployed a **Router-on-a-Stick** design on the local routers.
* **Sub-Interfaces:** Divided the physical `GigabitEthernet0/0` interface into logical sub-interfaces.
* **Encapsulation:** Applied `encapsulation dot1Q` tags to match the VLAN IDs.
* **Gateway Services:** Assigned distinct IP subnets to serve as default gateways for each VLAN.

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 20.0.0.1 255.0.0.0
