# Huawei-eNSP-Firewall-Security-HRP-HA-Cluster
Designed a multi-zone network architecture (Untrust/DMZ/Trust) with dual firewalls (Master/Standby) in Hot Standby mode via HRP for service continuity. Implemented Security Zones and Security Policies to control traffic between zones, isolating DMZ servers (Web/FTP) from the internal Trust network (VLAN10/VLAN20).
# Huawei eNSP Firewall Security – HRP HA Cluster

## Description
Designed a multi-zone network architecture (Untrust/DMZ/Trust) with dual firewalls (Master/Standby) in Hot Standby mode via HRP for service continuity. Implemented Security Zones and Security Policies to control traffic between zones, isolating DMZ servers (Web/FTP) from the internal Trust network (VLAN10/VLAN20).

## Project Structure
- **Topology & Configuration.zip** – Full eNSP project file (topology + device configurations)
- **Screenshots/** – Visual references of the network design and configuration

## Zones
| Zone | Contents |
|------|----------|
| Untrust | ISP Router, external Client, Attacker |
| DMZ | Web Server, FTP Server |
| Trust | PC-IT (VLAN10), PC-HR (VLAN20) |

## Technologies
- Huawei eNSP
- USG Firewalls (Active/Standby)
- HRP (Huawei Redundancy Protocol)
- Security Zones & Security Policies
- VLANs & Static Routing

## Author
Final project – Huawei HCIA-Security certification course.
