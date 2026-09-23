# Windows 11 VM Setup

## VM Configuration

- OS: Windows 11 x64
- CPU: 2 cores
- RAM: 4096 MB
- Storage: 64 GB
- Version : 25H2 or later
- Network Adapter: LAB-LAN / Host-only

![Windows 11 Virtual Machine](../../images/phase1/Windows-VM-Setup.png)

 After connecting the Windows 11 VM to the `LAB-LAN` segment, I checked the network settings to make sure it was getting its information from pfSense.

The VM received:

- IP Address: `192.168.10.100`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.10.1`

I then tested the connection by pinging the pfSense gateway, pinging `8.8.8.8` to confirm Internet access, and using `nslookup google.com` to make sure DNS was working.

Everything worked successfully with no packet loss.

![Windows 11 Connectivity Test](../../images/phase1/windows11-connectivity-test.png)

