# Windows Server 2025 VM Setup

## VM Configuration

- OS: Windows Server 2025
- CPU: 2 cores
- RAM: 2048 MB
- Storage: 60 GB
- Version : 25H2 or later
- Network Adapter: LAB-LAN 

![Windows 11 Virtual Machine](../../images/phase1/Windows2025-Server.png)

## Network Configuration

- IP Address: 192.168.10.10
- Subnet Mask: 255.255.255.0
- Default Gateway: 192.168.10.1

![Windows Server IP Configuration](../../images/phase1/WinServer25-IpConfig.png)

## Connectivity Verification

The server was able to reach the pfSense gateway, access the Internet, and resolve DNS.

![Windows Server Connectivity Test](../../images/phase1/Win25Server-ConnectivityTest.png)
