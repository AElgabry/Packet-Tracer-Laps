# Site-to-Site WAN Network Simulation

## 📌 Project Overview
This project simulates a **Wide Area Network (WAN)** connecting two geographically separated office branches ("Site A" and "Site B"). The topology demonstrates how distinct Local Area Networks (LANs) communicate over a serial link using **Static Routing** and **Router-on-a-Stick** for internal segmentation.

## 🏗 Network Architecture
* **WAN Edge:** Two Cisco 2901 Routers connect via a Serial interface, simulating a leased line connection between offices.
* **LAN Core:** Each site utilizes a generic Router-on-a-Stick configuration to manage traffic between local VLANs.
* **Access Layer:** Cisco 2960 switches provide connectivity to end devices at each site.

## 🔧 Key Features & Technologies
* **WAN Connectivity:** Sites are linked via a Serial connection (Network `25.0.0.0/8`) using HDLC encapsulation.
* **Static Routing:** Manual routing entries guide traffic between the two remote sites.
* **Inter-VLAN Routing:** Local routing at each site is handled via sub-interfaces (802.1Q).
* **DHCP Services:** Each router acts as a DHCP server for its local VLANs, automatically assigning IPs to workstations.
* **DCE/DTE Configuration:** The WAN link is clocked at 2,000,000 bps on the DCE side (Router3) to synchronize the serial connection.

## 📊 Configuration Table

| Site | Department/Label | VLAN ID | Network Subnet | Gateway IP |
| :--- | :--- | :--- | :--- | :--- |
| **Site A (Left)** | VLAN 10 | 10 | `10.0.0.0/8` | `10.0.0.1` |
| **Site A (Left)** | VLAN 20 | 20 | `20.0.0.0/8` | `20.0.0.1` |
| **Site B (Right)** | VLAN 10* | 10 | `30.0.0.0/8` | `30.0.0.1` |
| **Site B (Right)** | VLAN 20* | 20 | `40.0.0.0/8` | `40.0.0.1` |
| **WAN Link** | Serial Link | N/A | `25.0.0.0/8` | N/A |

*\*Note: VLAN IDs 10 and 20 are reused at Site B but correspond to different IP subnets (30.x and 40.x).*

## 🚀 Usage
1. Open the `.pkt` file in **Cisco Packet Tracer**.
2. **Verify WAN Link:** Hover over the Serial cable (red zigzag) to ensure link lights are green.
3. **Test Local Routing:** Ping from PC0 (`10.x`) to PC1 (`20.x`) to test Router-on-a-Stick at Site A.
4. **Test WAN Routing:** Ping from PC0 (Site A) to PC2 (Site B).
   * *Example:* Ping from `10.0.0.x` to `30.0.0.x`.
   * *Note:* The first ping may fail due to ARP resolution; try twice.
