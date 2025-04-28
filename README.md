# Static NAT and Static Routing Project - Packet Tracer Simulation 🚀

## 📚 Project Objective

This project simulates a real-world enterprise network where private LAN devices communicate with external public devices using **Static NAT** (Network Address Translation) and **Static Routing**.  
The simulation is performed using Cisco Packet Tracer.

---

## 🧠 Topology Overview

- **LAN Side:**
  - 3 PCs (Private IPs)
  - 1 Switch
  - 1 Router (LAN Router - handling NAT)

- **ISP Side:**
  - 1 Router (ISP Router - simulating Internet provider)
  - 1 Switch
  - 2 PCs (Public IPs)

---

## 📋 IP Addressing Plan

| Device        | Interface | IP Address       | Subnet Mask    | Default Gateway |
|:--------------|:----------|:-----------------|:---------------|:----------------|
| PC0           | NIC        | 192.168.1.10/24   | 255.255.255.0  | 192.168.1.1     |
| PC1           | NIC        | 192.168.1.11/24   | 255.255.255.0  | 192.168.1.1     |
| PC2           | NIC        | 192.168.1.12/24   | 255.255.255.0  | 192.168.1.1     |
| LAN Router G0/0 | -        | 192.168.1.1/24    | 255.255.255.0  | -               |
| LAN Router G0/1 | -        | 200.0.0.2/24      | 255.255.255.0  | -               |
| ISP Router G0/0 | -        | 200.0.0.1/24      | 255.255.255.0  | -               |
| ISP Router G0/1 | -        | 150.1.1.1/24      | 255.255.255.0  | -               |
| ISP-PC0        | NIC        | 150.1.1.2/24      | 255.255.255.0  | 150.1.1.1       |
| ISP-PC1        | NIC        | 150.1.1.3/24      | 255.255.255.0  | 150.1.1.1       |

---

## ⚙️ Configuration Highlights

- **LAN Router:**
  - Configured Static NAT:
    - 192.168.1.10 ↔ 200.0.0.10
    - 192.168.1.11 ↔ 200.0.0.11
    - 192.168.1.12 ↔ 200.0.0.12
  - Static Default Route to ISP Router (0.0.0.0/0 → 200.0.0.1)

- **ISP Router:**
  - Static Route to reach LAN Network (192.168.1.0/24 → 200.0.0.2)

- **NAT Inside/Outside Configuration:**
  - G0/0 = NAT Inside (LAN Side)
  - G0/1 = NAT Outside (Public Side)

---

## 🔍 Testing and Verification

- ✅ Ping from LAN PCs to ISP PCs (150.1.1.2, 150.1.1.3).
- ✅ Ping from ISP PCs to mapped Public IPs (200.0.0.10, 200.0.0.11, 200.0.0.12).
- ✅ Verified NAT translations using:

```bash
show ip nat translations
