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
- [pfSense Setup](docs/setup/pfSense.md)
- [Windows 11 Setup](docs/setup/Windows11Pro-VM.md)
- [Windows Server Setup](docs/setup/Windows-Server2025.md)

## Phase 1 - Network Foundation

Phase 1 focused on getting the basic lab network up and running and making sure devices could successfully connect through pfSense.

pfSense was configured as both the firewall and router for the homelab.

- WAN: em0 
- LAN: em1
- LAN Subnet: 192.168.10.0/24
- DHCP Range: 192.168.10.100 - 192.168.10.199
- LAN Segment: LAB-LAN

I connected a Windows 11 client to the LAB-LAN segment and confirmed that it received an IP address from pfSense through DHCP.

I also added a Windows Server 2025 VM and configured it with a static IP address of 192.168.10.10.

To make sure everything was working correctly, I tested connectivity from both Windows systems. Both machines were able to reach the pfSense gateway, connect to the Internet, and successfully resolve DNS queries.

### Phase 1 Completed

- pfSense firewall/router configured
- WAN connected through VMware NAT
- Isolated 'LAB-LAN' segment created
- DHCP configured for client devices
- Windows 11 client connected successfully
- Windows Server 2025 configured with a static IP
- Gateway connectivity verified
- Internet connectivity verified
- DNS resolution verified

**Phase 1 Status: Complete**

[View Detailed pfSense Configuration](docs/setup/pfSense.md)
