# Windows 11 DNS Update Issue

## Problem

After moving Windows Server 2025 from '192.168.10.10' to '192.168.20.10', the Windows 11 client was still using the old DNS server address.

Even after updating the DNS server in pfSense DHCP settings, 'nslookup lab.local' continued trying to use '192.168.10.10' and timed out.

## Resolution

I checked the Windows 11 DNS settings and found that the old DNS server had been set manually on the network adapter.

I tried resetting the DNS settings with PowerShell, but the command required administrator permissions.

I opened PowerShell as an administrator using the local 'LabAdmin' account and ran:

'Set-DnsClientServerAddress -InterfaceAlias "Ethernet0" -ResetServerAddresses'

After that, I renewed the DHCP lease and flushed the DNS cache using: 'ipconfig /release' , 'ipconfig /renew' and 'ipconfig /flushdns'. After this, Windows 11 then received '192.168.20.10' as its DNS server from pfSense, and 'nslookup lab.local' worked correctly.
