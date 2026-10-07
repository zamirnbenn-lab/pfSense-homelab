
# Windows Server DNS Forwarding Issue

## Problem

While configuring the firewall rules for 'SERVER-LAN', I ran into an issue where Windows Server 2025 and Windows 11 could no longer resolve external domains.

The Ubuntu Server was also unable to resolve external websites, even though it could still reach the internet by pinging '8.8.8.8'.

I found that the issue started after enabling the rule blocking traffic from 'SERVER-LAN' to the other internal networks.

## Resolution

I temporarily disabled the 'Block SERVER Access to Internal Networks' rule in pfSense and tested DNS again.

After disabling the rule, external DNS resolution started working.

I checked the Windows Server DNS forwarding configuration and added a separate firewall rule allowing Windows Server at '192.168.20.10' to send DNS requests to pfSense at '192.168.10.1'.

The rule used:

- Action: Pass
- Protocol: TCP/UDP
- Source: 192.168.20.10
- Destination: 192.168.10.1
- Destination Port: 53 (DNS)

I placed the new rule above the internal network block rule and enabled the block rule again.

After applying the changes, I tested DNS and internet connectivity from both Windows Server 2025 and Ubuntu Server.

Windows Server was able to resolve external domains and connect to websites over HTTPS. Ubuntu was also able to access external websites and successfully completed a longer ping test with 0% packet loss.

This allowed me to keep the internal network restrictions in place without blocking the DNS requests needed by the lab.
