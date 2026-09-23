# pfSense-homelab

## Overview

This project is a virtualized networking and security homelab built using
VMware Workstation and pfSense.

The purpose of the lab is to gain hands-on experience with routing,
firewall configuration, VLAN segmentation, Windows Active Directory,
Linux administration, and security monitoring.

## Lab Environment

- VMware Workstation Pro
- pfSense CE
- Windows Server 2022
- Windows 11
- Ubuntu Server
- Kali Linux
- Splunk

## Network Topology

[Beginning Network Topology](images/phase1/Network-Topology1.png)

## Network Addressing

| Device | IP Address | Purpose |
|---|---|---|
| pfSense LAN | 192.168.10.1 | Default Gateway |
| Windows Server | 192.168.10.10 | AD/DNS Server |
| Ubuntu Server | 192.168.10.20 | Linux Server |
| Windows 11 | DHCP | Domain Client |

## Skills Demonstrated

- Firewall configuration
- NAT
- DHCP
- DNS
- Routing
- VLAN segmentation
- Active Directory
- Group Policy
- Linux administration
- Network troubleshooting
- Log analysis

## Documentation
- [pfSense Setup](docs/setup/pfsense-setup.md)
- [Windows Server Setup](docs/setup/windows-server-setup.md) 

## Phase 1 - pfSense Setup

pfSense was configured as both the firewall and router for this homelab.

- WAN: em0 (DHCP via VMware NAT)
- LAN: em1
- LAN Subnet: 192.168.10.0/24

[View Detailed pfSense Configuration](docs/setup/pfsense-setup)
