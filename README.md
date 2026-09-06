# Huawei eNSP Firewall Security – HRP High Availability Cluster

## Overview
This project is a final capstone simulation for the **Huawei HCIA-Security** certification, built entirely using **eNSP (Enterprise Network Simulation Platform)**. It demonstrates the design and implementation of a secure, multi-zone enterprise network protected by a **redundant firewall cluster** running **HRP (Huawei Redundancy Protocol)** in Active/Standby (Hot Standby) mode.

The project goes beyond static design — it includes **live traffic testing with Wireshark** to validate that Security Zones, Security Policies, and the HRP failover mechanism all function correctly under real conditions.

## Objectives
- Design a segmented network using **Security Zones**: Untrust, DMZ, and Trust.
- Implement **Security Policies** to strictly control traffic flow between zones.
- Configure two **USG firewalls** (Master/Active and Standby) in a **Hot Standby (HRP)** cluster for high availability.
- Validate zone isolation and firewall failover using **live ping tests and Wireshark packet captures**.

## Network Topology
![Network Topology](Screenshots/Network%20Topology.png)

| Zone | Devices | Subnet(s) |
|------|---------|-----------|
| Untrust Zone | ISP Router, Client, Attacker | 200.1.x.x/24 |
| DMZ Zone | Web Server, FTP Server | 192.168.100.0/24 |
| Trust Zone | PC-IT (VLAN10), PC-HR (VLAN20) | 192.168.10.0/24, 192.168.20.0/24 |
| Firewall Cluster | Master & Standby Firewalls (HRP heartbeat link) | 10.0.0.0/30 |

## Security Zones
Interfaces were grouped into dedicated security zones on the firewall, each with a distinct priority level to enforce traffic direction rules.

![Security Zones](Screenshots/Security%20Zones.png)

## Security Policies
Explicit rules were configured to control inter-zone traffic — permitting legitimate business traffic (Trust → DMZ, Trust → Untrust, Untrust → DMZ services) while explicitly denying unauthorized access from Untrust into the Trust zone.

![Security Policy](Screenshots/Security%20Policy.png)

## High Availability – HRP Cluster
The two firewalls synchronize state over a dedicated heartbeat link (GE1/0/3) using HRP, ensuring the Standby firewall can take over instantly if the Master fails.

**Master Firewall — Active State**
![HRP State Master](Screenshots/HRP%20State%20(Master)%20.png)

**Standby Firewall — Standby State**
![HRP State Standby](Screenshots/HRP%20State%20(Standby).png)

**Failover Test — Master Firewall Powered Off**
When the Master firewall was shut down, the Standby detected the lost heartbeat and automatically promoted itself to Active, maintaining network availability.
![HRP Failover](Screenshots/HRP%20State%20when%20Firewall%20Master%20is%20Off.png)

## Testing & Validation (Wireshark)
Live traffic was captured with Wireshark on key links to verify that the security policies and HA cluster behaved as designed.

**✅ Allowed Traffic — PC-IT (Trust) to Web Server (DMZ)**
Ping requests from the Trust zone reached the DMZ server successfully, confirming the `trust_to_dmz` policy is working.
![PC-IT to Web Server](Screenshots/Ping%20from%20PC%20(IT)%20on%20Web%20Server%20(Master)%20-%20WireShark.png)

**🚫 Blocked Traffic — Attacker (Untrust) to Trust Zone**
Ping attempts from the Attacker in the Untrust zone toward internal Trust hosts received no response, confirming the `untrust_to_trust_deny` policy is enforced.
![Attacker Blocked](Screenshots/Ping%20from%20Attacker%20on%20PC%20(IT)%20(Standby)%20-%20WireShark.png)

**✅ Service Validation — FTP & HTTP**
Application-level connectivity to the DMZ servers was also verified using FTP and HTTP clients, confirming the DMZ services are reachable and correctly filtered by the firewall policies.

> Additional test screenshots (Master/Standby comparisons, extended ping sessions, and full packet captures) are available in the `Screenshots/` folder.

## Project Structure
- **Topology & Configuration.zip** – Full eNSP project file (topology + device configurations)
- **Screenshots/** – Complete set of test evidence (topology, zones, policies, HRP states, Wireshark captures)

## Technologies Used
- Huawei eNSP
- USG Firewalls (Active/Standby)
- HRP (Huawei Redundancy Protocol)
- Security Zones & Security Policies
- VLANs & Static Routing
- Wireshark (traffic analysis & validation)

## Author
**Youssuf Ahmed Mohamed Hafez** | HCIA-Security

* **LinkedIn:** [Youssuf Ahmed](https://www.linkedin.com/in/yussufhafezofficial)
