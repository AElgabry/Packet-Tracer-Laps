# Multi-Site Dynamic Routing (RIP) Simulation

## 📌 Project Overview
This project simulates a **Multi-Site Wide Area Network (WAN)** connecting three separate office locations in a linear topology. Unlike static routing scenarios, this simulation utilizes **RIP (Routing Information Protocol)** to demonstrate how routers can dynamically exchange network information and converge without manual route configuration.

## 🏗 Network Architecture
* **Topology:** A linear "Daisy Chain" connecting Site A ↔ Site B ↔ Site C.
* **Routing Protocol:** **RIPv1** is configured on all routers to automatically advertise and learn routes to remote subnets.
* **WAN Backbone:** Serial links connect the routers, establishing the path for inter-site communication.

## 🔧 Key Features & Technologies
* **Dynamic Routing (RIP):** Routers automatically discover the network topology. If a new network is added, RIP will propagate the route updates to neighbors automatically.
* **Serial WAN Links:**
  * **Link A-B:** Network `11.0.0.0/8` (Connects Router0 and Router1).
  * **Link B-C:** Network `13.0.0.0/8` (Connects Router1 and Router2).
* **DCE/DTE Clocking:**
  * Router0 acts as the DCE for the link to Router1.
  * Router1 acts as the DCE for the link to Router2.

## 📊 Configuration Table

| Site | Device | LAN Subnet | Gateway IP | Connected To |
| :--- | :--- | :--- | :--- | :--- |
| **Site A (Left)** | Router0 | `10.0.0.0/8` | `10.0.0.2` | Router1 (via `11.x`) |
| **Site B (Middle)**| Router1 | `20.0.0.0/8` | `20.0.0.2` | Router0 & Router2 |
| **Site C (Right)** | Router2 | `30.0.0.0/8` | `30.0.0.2` | Router1 (via `13.x`) |

## 🚀 Usage
1. Open the `.pkt` file in **Cisco Packet Tracer**.
2. **Verify Routing:** Open the CLI on **Router0** and type `show ip route`. You should see entries marked with **R** (RIP) for networks 20.0.0.0 and 30.0.0.0.
3. **Test Connectivity:**
   * Open **PC0** (Site A) and ping **PC2** (Site C) at `30.0.0.x` (assuming PCs are configured).
   * The ping should succeed as the traffic traverses the middle router (Router1) automatically.
