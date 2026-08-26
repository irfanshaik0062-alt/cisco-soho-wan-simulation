# Cisco-SOHO-WAN-Simulation
A Packet Tracer network simulation demonstrating local LAN DHCP dynamic client configuration routing through a Cable Modem and WAN ISP Cloud bridge to a hosted remote HTTP Web Server environment.

A complete **Small Office/Home Office (SOHO)** network simulation featuring local LAN client allocation, standard physical edge infrastructure bridging, and functional public domain routing model via **Cisco Packet Tracer**.

## 📌 Project Overview
This repository provides a configuration blueprint demonstrating secure LAN client machines automatically obtaining local network metrics and seamlessly communicating across an ISP infrastructure bridge to reach an internet-accessible host server providing HTTP web services and DNS domain lookups.

┌───────────────┐
│    myserver   │ = (HTTP / DNS Server)│ 208.67.220.220│
└───────┬───────┘
│ (Ethernet6)   |
┌───────┴───────┐
│    Cloud0     │ = (ISP WAN Bridge)
└───────┬───────┘
│ (Coaxial7)    |
┌───────┴───────┐
│ Cable Modem0  │
└───────┬───────┘
        |
┌──────────┴──────────┐
│  Wireless Router0   │ = (Edge NAT Gateway)│ WAN: 208.67.220.221 ││ LAN: 192.168.0.1    │
└──────────┬──────────┘
        │
┌───────┴───────┐
│ Switch0       │
└───────┬───────┘
┌────────────────┼────────────────┐┌────┴────┐     
│   PC0         │   PC1   │       │ Laptop0  |
|  (DHCP)       | (DHCP)  │       │  (DHCP)  |
└─────────┘     └─────────┘       └─────────┘

## 🛠️ Network Architecture Design

### 1. Local Area Network (LAN) Configuration
* **Gateway Interface:** `192.168.0.1` (Wireless Router0 LAN Interface)
* **Subnet Mapping Range:** `192.168.0.100` to `192.168.0.102`
* **Allocation Subnet Mask:** `255.255.255.0 (/24)`
* **Assigned Local Clients:** `PC0`, `PC1`, and `Laptop0` managed dynamically via DHCP leasing.

### 2. Wide Area Network (WAN) & Internet Configuration
* **Router Public WAN Interface:** `208.67.220.221`
* **Network Mask Configuration:** `255.255.255.0`
* **Upstream Default Gateway:** `208.67.220.1`
* **Target HTTP/DNS Server Location:** `208.67.220.220`

---

## ⚙️ Step-by-Step Device Setup Guide

### Phase 1: ISP Core Infrastructure Bridge (`Cloud0`)
To map local subscriber physical termination over to public server segments:
1. Open the configuration interface for **Cloud0** and access the **Config** tab.
2. Select **Cable** under the *Connections* menu options panel on the left.
3. Establish a static port association with the following assignments:
   * **Drop-down 1 (Coaxial Input Interface):** Choose `Coaxial7`
   * **Drop-down 2 (Ethernet Output Port):** Choose `Ethernet6`
4. Click **Add** to register the bridging interface mapping rules.

### Phase 2: Host Application Node Provisioning (`myserver`)
Configure the targeted remote web deployment platform:
1. Open **myserver** and navigate to **Desktop** > **IP Configuration**.
2. Check **Static** assignment mode and apply the network metrics:
   * **IP Address:** `208.67.220.220`
   * **Subnet Mask:** `255.255.255.0`
   * **Default Gateway:** `208.67.220.1`
   * **DNS Server Configuration:** `208.67.220.220`
3. Swap over to the **Services** tab, select **HTTP**, and toggle both **HTTP** and **HTTPS** markers to **On**.
4. Select **DNS** under the *Services* panel to link the domain string:
   * **Name:** `myserver`
   * **Type:** `A Record`
   * **Address:** `208.67.220.220`
   * Click **Add** and ensure DNS Service is toggled **On**.

### Phase 3: Central Perimeter Node Routing (`Wireless Router0`)
Provisions network perimeter boundaries and edge network address translation (NAT):
1. Access the **Home Router** interface and open the **GUI** configuration utility tab.
2. Locate the **Internet Setup** parameter cluster under **Setup** > **Basic Setup**:
   * **Internet Connection Type Selection:** Change to `Static IP`
   * **Internet IP Address:** `208.67.220.221`
   * **Subnet Mask Allocation:** `255.255.255.0`
   * **Default Gateway Metric:** `208.67.220.1`
   * **Primary DNS Target:** `208.67.220.220`
3. Scroll downwards on the same menu panel to configure **Network Setup** (LAN Parameter blocks):
   * **Router IP Address Assignment:** `192.168.0.1`
   * **Subnet Mask Selection:** `255.255.255.0`
   * **DHCP Address Server:** Marked to `Enabled`
   * **Static DNS 1 Variable:** Input `208.67.220.220` to update domain queries for local clients automatically.
4. Scroll to the lower edge margin of the utility panel and choose **Save Settings**.

---

## 🔍 Validation & Interoperability Testing

### Verification Procedure 1: Dynamic Leasing Check
Open the **IP Configuration** screen on **PC0**, **PC1**, and **Laptop0**. Toggle the assignment mode selector button from `Static` to `DHCP` to verify automatic host provisioning.

### Verification Procedure 2: Low-Level Connectivity Verification
Open a local terminal prompt (**PC0** > **Desktop** > **Command Prompt**) and execute a test transmission against your target server node:
```bash
ping 208.67.220.220
```
*Successful replies indicate functioning LAN encapsulation, edge translation (NAT), and downstream routing protocols are working correctly.*

### Verification Procedure 3: Top-Level HTTP Service Verification
Open the **Web Browser** application dashboard on **PC0** or **Laptop0**. Inside the primary URL routing address bar field, type either the static server IP or the DNS mapping word link, then click **Go**:
* `208.67.220.220`
* `http://myserver`

The application framework should successfully look up the node hostname, cross the internet architecture boundary, and render the underlying landing page document.

---

## 📸 Project Success Demonstration

When configuration is complete, pointing the built-in Packet Tracer Web Browser application to the host network address or domain successfully fetches and displays the following index template page:

![Web Server Verification Success] git add images/Cisco-SOHO-WAN-Simulation.png



