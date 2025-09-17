# CCNA Networking Lab – VLANs, Inter-VLAN Routing, Static Routing, and ACLs  

This project demonstrates a small enterprise-style network using **Cisco Packet Tracer**. It includes multiple VLANs, Router-on-a-Stick inter-VLAN routing, static routing over a WAN link, switch trunking, and access control lists (ACLs) for traffic restriction.  

---

## 🖧 Topology Overview  

- 4 VLANs: HR (10), IT (20), Sales (30), Branch (40)  
- 2 Routers (Cisco 2911) with static WAN link  
- Multilayer switches (Cisco 3560) with trunk ports  
- 8 PCs (2 per VLAN)  
- Router-on-a-Stick configuration for inter-VLAN routing  
- ACL restricting traffic between VLAN 10 (HR) and VLAN 30 (Sales)  
  

## 📷 Topology
Topology.png

---

## 🧱 Devices & IP Addressing

| Device | Interface | IP Address | Subnet Mask | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **R1** | G0/0.10 | 192.168.10.1 | 255.255.255.0 | VLAN 10 GW |
| | G0/0.20 | 192.168.20.1 | 255.255.255.0 | VLAN 20 GW |
| | G0/0.30 | 192.168.30.1 | 255.255.255.0 | VLAN 30 GW |
| | S0/3/0 | 10.0.0.1 | 255.255.255.252 | WAN to R2 |
| **R2** | G0/0 | 192.168.40.1 | 255.255.255.0 | VLAN 40 GW |
| | S0/3/0 | 10.0.0.2 | 255.255.255.252 | WAN to R1 |
| **S1** | VLAN 10 | 192.168.10.2 | 255.255.255.0 | Optional Mgmt. |
| **S1** | VLAN 20 | 192.168.20.2 | 255.255.255.0 | Optional Mgmt. |
| **S2** | VLAN 30 | 192.168.30.2 | 255.255.255.0 | Optional Mgmt. |
| **S3** | VLAN 40 | 192.168.40.2 | 255.255.255.0 | Optional Mgmt. |
| **PC1-2** | Fa0 | 192.168.10.x | 255.255.255.0 | VLAN 10 HR |
| **PC3-4** | Fa0 | 192.168.20.x | 255.255.255.0 | VLAN 20 IT |
| **PC5-6** | Fa0 | 192.168.30.x | 255.255.255.0 | VLAN 30 Sales |
| **PC7-8** | Fa0 | 192.168.40.x | 255.255.255.0 | VLAN 40 Branch |



---

## ⚙️ Configurations Included  

- VLAN creation and port assignments  
- Trunk configuration between Cisco 3560 switches  
- Router-on-a-Stick inter-VLAN routing on Cisco 2911 routers  
- Static WAN routing between HQ (R1) and Branch (R2)  
- IP addressing and default gateways for PCs  
- **ACL restricting communication between HR (VLAN 10) and Sales (VLAN 30)**  

---

## 🔒 ACL Implementation  

An **Access Control List (ACL)** was configured on Router R1 to block HR (192.168.10.0/24) from communicating with Sales (192.168.30.0/24).  

---

✅ Result:

HR ↔ Sales = Blocked

HR ↔ IT / Branch = Allowed

Sales ↔ IT / Branch = Allowed

---

Example configuration:  

R1(config)# access-list 100 deny ip 192.168.10.0 0.0.0.255 192.168.30.0 0.0.0.255
R1(config)# access-list 100 permit ip any any
R1(config)# interface g0/0.30
R1(config-if)# ip access-group 100 in

---

## ✅ Testing & Results

- Pings within the same VLAN ✅  
- Pings across VLANs via Router-on-a-Stick ✅  
- Pings across HQ–Branch WAN ✅  
- ACL blocking Sales → HR traffic (expected) ✅  
- ACL allowing Sales → IT/Branch traffic ✅  

---

## 🧠 What I Learned

- VLAN segmentation and inter-VLAN communication  
- Trunk ports for VLAN propagation  
- Router-on-a-Stick for routing between VLANs  
- Static routing across a WAN link  
- Using ACLs for basic security and traffic filtering  
- End-to-end network connectivity testing  

---

## 💼 Built With

- Cisco Packet Tracer 8.x (or latest)  
- Cisco 3560 Switches  
- Cisco 2911 Routers  

---

## 📁 Folder Structure

- `PacketTracerFiles/` — `.pkt` file for Cisco Packet Tracer  
- `Configurations/` — Router and switch configs  
- `Diagrams/` — Network topology images  

---

## Author


Created by Abdulmohaimen – part of CCNA hands-on learning.

