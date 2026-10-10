# pfSense-homelab

## Overview

This project is a virtualized networking and security homelab built using
VMware Workstation and pfSense.

The purpose of the lab is to gain hands-on experience with routing,
firewall configuration, VLAN segmentation, Windows Active Directory,
Linux administration, and security monitoring.

## Lab Environment

***Current:***
- VMware Workstation Pro
- pfSense CE
- Windows Server 2025
- Windows 11
- Ubuntu Server
- Kali Linux
- Splunk Enterprise

## Current Network Topology

![Current Network Topology](images/phase4/NetworkTopology-Phase4.png)


## Network Addressing

- pfSense LAN: 192.168.10.1
  - Default gateway for 'LAB-LAN'

- pfSense SERVER: 192.168.20.1
  - Default gateway for 'SERVER-LAN'

- pfSense SECURITY: 192.168.30.1
  - Default gateway for 'SECURITY-LAN'

- pfSense GUEST: 192.168.40.1
  - Default gateway for 'GUEST-LAN'

- Windows 11 Client: 192.168.10.100 via DHCP
  - Connected to 'LAB-LAN'
  - Joined to the 'lab.local' domain
  - Uses Windows Server 2025 at '192.168.20.10' for DNS

- Windows Server 2025: 192.168.20.10
  - Connected to 'SERVER-LAN'
  - Static IP
  - Active Directory Domain Services and DNS

- Ubuntu Server: 192.168.20.20
  - Connected to 'SERVER-LAN'
  - Static IP
  - OpenSSH and Nginx

- Kali Linux: 192.168.30.10
  - Connected to 'SECURITY-LAN'
  - Static IP
  - Security testing client

- Ubuntu Server (Splunk): 192.168.30.20
  - Planned for 'SECURITY-LAN'
  - Splunk Enterprise / SIEM

## Planned Skills and Technologies

As I continue building the lab, I plan to focus more on security monitoring, centralized logging, and cloud networking.

Future phases will include Splunk and centralized logging, security monitoring and log analysis, network traffic analysis, Kali Linux testing, additional pfSense firewall tuning, guest network isolation, and eventually working with 802.1Q VLANs and cloud networking/security concepts.

## Documentation

### Setup

- [pfSense Setup](docs/setup/pfSense.md)
- [Windows 11 Pro Setup](docs/setup/Windows11Pro-VM.md)
- [Windows Server 2025 Setup](docs/setup/Windows-Server2025.md)
- [Kali Linux Setup](docs/setup/kali-linux-setup.md)
- [Splunk Enterprise Setup](docs/setup/splunk.md)

### Active Directory

- [Users, Groups, and OUs](docs/active-directory/users-groups.md)
- [Windows 11 Domain Join](docs/active-directory/domain-join.md)
- [Group Policy](docs/active-directory/group-policy.md)
- [Shared Folder Permissions](docs/active-directory/shared-folder-permissions.md)

### Linux

- [Ubuntu Server Setup & Integration](docs/linux/ubuntu-server.md)

### Network Segmentation

- [Network Segmentation and Server Network Changes](docs/network-segmentation/network-change.md)
- [LAN Firewall Rules](docs/network-segmentation/firewall-rules/lan.md)
- [SERVER Firewall Rules](docs/network-segmentation/firewall-rules/server.md)
- [SECURITY Firewall Rules](docs/network-segmentation/firewall-rules/security.md)
- [GUEST Firewall Rules](docs/network-segmentation/firewall-rules/guest.md)

### Security Monitoring 
- [pfSense Logging](docs/security-monitoring/pfSense-logging.md)

### Troubleshooting

- [Windows 11 Network Connectivity Issue](troubleshooting/windows11-network.md)
- [Domain Controller Promotion Issue](troubleshooting/domain-controller-promotion.md)
- [pfSense Interface Mapping Issue](troubleshooting/pfsense-interface-mapping.md)
- [SERVER Interface ICMP Rule Issue](troubleshooting/server-interface-icmp-rule.md)
- [Ubuntu DNS Resolution Issue](troubleshooting/ubuntu-dns-resolution.md)
- [Windows 11 DNS Update Issue](troubleshooting/Windows11-DNS-Update.md)
- [Windows Server Shared Folder Access Issue](troubleshooting/windows-server-share-access.md)
- [Windows Server DNS Forwarding Issue](troubleshooting/server-dns-forwarding.md)

<br><br>

## Phase 1 - Network Foundation

For Phase 1, I focused on getting the basic network working and making sure the devices in the lab could actually communicate through pfSense.

I set up pfSense as the firewall and router for the lab, using VMware NAT for the WAN connection and a separate LAB-LAN segment for the internal network.

- WAN: em0
- LAN: em1
- LAN Subnet: 192.168.10.0/24
- DHCP Range: 192.168.10.100 - 192.168.10.199

I connected a Windows 11 VM to the LAB-LAN and confirmed that it received an IP address from pfSense. I also added a Windows Server 2025 VM and gave it the static IP address 192.168.10.10.

After everything was connected, I tested both Windows machines to make sure they could reach the pfSense gateway, access the Internet, and resolve DNS successfully.

### Phase 1 Results:

- pfSense is working as the lab firewall and router
- Windows 11 is receiving an IP through DHCP
- Windows Server 2025 is using a static IP
- Both systems can reach the pfSense gateway
- Both systems have Internet access
- DNS resolution is working

[View Detailed pfSense Configuration](docs/setup/pfSense.md)

**Phase 1 Status: Complete**

<br><br>

## Phase 2 - Active Directory and Domain Services

For Phase 2, I focused on building out the Active Directory side of the lab using Windows Server 2025.

I installed Active Directory Domain Services and DNS, promoted the server to a domain controller, and created the 'lab.local' domain.

I created users and Global Security groups for IT, HR, and Marketing. I also created Organizational Units for each department and moved the users into the OU that matched their department.

[View Active Directory Users and Groups Documentation](docs/active-directory/users-groups.md)

After Active Directory was set up, I changed the Windows 11 client to use '192.168.10.10' for DNS and joined it to the 'lab.local' domain.

I tested the domain connection using "nslookup lab.local" and logged into Windows 11 using one of the domain accounts. I also used "whoami" to confirm that the account was being authenticated through the domain.

[View Windows 11 Domain Join Documentation](docs/active-directory/domain-join.md)

### Group Policy

I created and linked a Group Policy to the Marketing OU that blocked access to Control Panel and Windows Settings.

After applying the policy, I logged into the Windows 11 client using a Marketing account and confirmed that Windows blocked access as expected.

[View Group Policy Documentation](docs/active-directory/group-policy.md)

### Shared Folder Permissions

I created separate shared folders for IT, HR, and Marketing on Windows Server 2025 and used the department security groups to control access.

I tested the permissions from the Windows 11 client and confirmed that users could access and modify files in their own department folder while being blocked from folders they did not have permission to use.

[View Shared Folder Permissions Documentation](docs/active-directory/shared-folder-permissions.md)

### Phase 2 Results

- Windows Server 2025 promoted to a domain controller
- 'lab.local' domain created
- Active Directory Domain Services and DNS configured
- Department-based OUs created for IT, HR, and Marketing
- Users and Global Security groups created
- Windows 11 successfully joined to 'lab.local'
- Domain login and DNS resolution verified
- Group Policy created, linked, and successfully tested
- Department shared folders created
- Share and NTFS permissions configured using security groups
- Allowed and denied folder access successfully tested

**Phase 2 Status: Complete**

<br><br>

## Phase 3 - Linux Server Integration

For Phase 3, I added an Ubuntu Server VM to the existing 'LAB-LAN' and gave it the static IP address '192.168.10.20'.

I configured the server to use pfSense at '192.168.10.1' as the gateway and Windows Server 2025 at '192.168.10.10' for DNS. After setting up the network, I tested connectivity and confirmed that Ubuntu could resolve the 'lab.local' domain.

I installed OpenSSH and tested remote access from the Windows 11 client using "ssh zamir@192.168.10.20".

I also worked with Linux users, groups, and file permissions by creating a second user named 'alex', a 'webadmins' group, and a shared directory at '/srv/linux-share'. I tested the folder using both accounts to make sure the group permissions were working correctly.

After that, I installed Nginx and tested the web server locally and from the Windows 11 client.

On Windows Server 2025, I created a DNS record for 'ubuntu-server.lab.local' that points to '192.168.10.20'. From Windows 11, I tested the new hostname using 'nslookup', 'ping', SSH, and a web browser.

I was able to connect to the Ubuntu server and open the Nginx page using 'ubuntu-server.lab.local' instead of the IP address.

[View Ubuntu Server Documentation](docs/linux/ubuntu-server.md)

Phase 3 Status: Complete

<br><br>


## Phase 4 - Network Segmentation and Firewall Rules

For Phase 4, I separated the lab into different networks instead of keeping every device on the same 'LAB-LAN'.

I created separate VMware LAN Segments for the lab, server, security, and guest networks and added additional network adapters to pfSense.

The networks are currently set up as:

- LAB-LAN - 192.168.10.0/24
- SERVER-LAN - 192.168.20.0/24
- SECURITY-LAN - 192.168.30.0/24
- GUEST-LAN - 192.168.40.0/24

I moved Windows Server 2025 and Ubuntu Server to 'SERVER-LAN' and updated their IP addresses, gateways, and DNS settings.

I installed Kali Linux on 'SECURITY-LAN' and created firewall rules for the LAN, SERVER, SECURITY, and GUEST interfaces.

I configured the firewall rules to allow required services such as DNS, SSH, HTTP, HTTPS, and Active Directory traffic while blocking unauthorized communication between the networks.

I tested the firewall rules from Windows 11, Ubuntu Server, Kali Linux, and the Windows 11 Guest VM. I also checked the pfSense firewall logs to confirm that blocked traffic was being handled by the rules I created.

For the Guest network, I configured a Windows 11 VM at '192.168.40.100'. The Guest VM can access the internet but is blocked from accessing the internal LAB, SERVER, and SECURITY networks.

[View Network Segmentation Documentation](docs/network-segmentation/network-change.md)

[View LAN Firewall Rules](docs/network-segmentation/firewall-rules/lan.md)

[View SERVER Firewall Rules](docs/network-segmentation/firewall-rules/server.md)

[View SECURITY Firewall Rules](docs/network-segmentation/firewall-rules/security.md)

[View GUEST Firewall Rules](docs/network-segmentation/firewall-rules/guest.md)

**Phase 4 Status: Complete**

## Phase 5 - Security Monitoring and Centralized Logging

For Phase 5, I started adding centralized logging and security monitoring to the lab using Splunk Enterprise.

I created a separate Ubuntu Server on 'SECURITY-LAN' at '192.168.30.20' and installed Splunk Enterprise. I configured the server with a static IP address, DNS through Windows Server 2025, SSH access, and automatic startup using systemd.

I then configured Splunk to receive pfSense firewall and system logs over UDP port '5514'. I created a separate 'pfsense' index in Splunk to keep the firewall events organized.

To test the setup, I generated blocked traffic from Kali Linux at '192.168.30.10' to Windows Server 2025 at '192.168.20.10'.

The pfSense firewall blocked the traffic as expected and forwarded the event to Splunk. I searched the 'pfsense' index and confirmed that the blocked ICMP traffic from Kali was being recorded.

This gave me a working centralized logging setup where network activity can be generated, blocked by pfSense, and reviewed through Splunk.

[View Splunk Server Setup](docs/setup/splunk-server.md)

[View pfSense Logging with Splunk](docs/security-monitoring/pfsense-logging.md)

**Phase 5 Status: In Progress**
