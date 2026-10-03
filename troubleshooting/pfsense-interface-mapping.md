# pfSense Interface Mapping Issue

## Problem

While setting up the new Phase 4 networks, Windows 11 lost access to pfSense at '192.168.10.1'.

The Windows 11 client still had the correct IP address, subnet mask, and default gateway, but pinging '192.168.10.1' returned a destination host unreachable message.

## Resolution

I checked the VMware network settings and confirmed that Windows 11 was still connected to 'LAB-LAN'. I then compared the MAC addresses of each pfSense network adapter in VMware with the interface MAC addresses shown in the pfSense console.

The issue was that the VMware adapter numbers did not match the pfSense interface names in the order I expected.

I corrected the pfSense interface assignments to:

- WAN - em0
- LAN - em4
- OPT1 - em1
- OPT2 - em2
- OPT3 - em3

After updating the interface assignments, Windows 11 was able to ping '192.168.10.1' again and access the pfSense web interface.
