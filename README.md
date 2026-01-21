# Small Office Network Simulation

## 📌 Project Overview
This project simulates a segmented network infrastructure for a Small-to-Medium Enterprise (SME) designed in **Cisco Packet Tracer**. The topology utilizes a **Router-on-a-Stick** architecture to manage traffic between three distinct departments (HR, IT, and Sales) while implementing Layer 2 security measures at the access level.

## 🏗 Network Architecture
* **Core/Routing Layer:** A Cisco 2901 Router handles Inter-VLAN routing using sub-interfaces and acts as the central DHCP server.
* **Distribution Layer:** A Cisco 3650 Multilayer Switch aggregates traffic from the access layer switches.
* **Access Layer:** Two Cisco 2960 switches provide end-user connectivity with Port Security enabled to prevent unauthorized access.

## 🔧 Key Features & Technologies
* **VLAN Segmentation:** Traffic is logically separated into three VLANs to isolate departmental data.
* **Inter-VLAN Routing:** Configured via **802.1Q trunking** (Router-on-a-Stick) on the central router.
* **Dynamic Addressing (DHCP):** The router manages three separate DHCP pools to automatically assign IP addresses to devices in each VLAN.
* **Layer 2 Security:**
  * **Port Security:** Enabled on access ports with `violation restrict` mode.
  * **Sticky MAC:** Dynamically learns and saves MAC addresses to the running configuration to prevent MAC spoofing.
* **EtherChannel:** Link aggregation (LACP/PAgP) is configured to bundle physical links for increased bandwidth and redundancy between switches.

## 📊 VLAN Configuration Table
| Department | VLAN ID | Network Subnet | Gateway IP |
| :--- | :--- | :--- | :--- |
| **HR** | 10 | `10.0.0.0/8` | `10.0.0.1` |
| **IT** | 20 | `20.0.0.0/8` | `20.0.0.1` |
| **Sales** | 30 | `30.0.0.0/8` | `30.0.0.1` |

## 🚀 Usage
1. Open the `.pkt` file in **Cisco Packet Tracer** (Version 7.0 or newer recommended).
2. Wait for the network to converge (spanning tree) or press the "Fast Forward Time" button.
3. **Verify Connectivity:** Open a Command Prompt on any PC and ping a PC in a different VLAN (e.g., Ping from HR PC12 to Sales PC16).
4. **Test Security:** Attempt to connect an unauthorized device to ports `Fa0/1 - Fa0/6` to observe the Port Security violation.
