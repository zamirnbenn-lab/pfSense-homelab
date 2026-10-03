# Ubuntu DNS Resolution Issue

## Problem

After moving the Ubuntu Server to the new 'SERVER-LAN' network, the server was able to reach pfSense, the Windows Server, and the internet, but DNS lookups using 'nslookup lab.local' returned a SERVFAIL error.

Running 'nslookup lab.local 192.168.10.10' worked correctly, which showed that the Windows DNS server was reachable and responding.

## Resolution

I checked the Ubuntu resolver settings using 'resolvectl status ens33' and found that the server was using '192.168.20.10' as its DNS server.

At this point, the Windows Server was still using '192.168.10.10', so the Ubuntu Server was pointing to the wrong DNS address.

I updated the Netplan configuration so the DNS server was set back to '192.168.10.10', then applied the changes and restarted 'systemd-resolved'.

After the change, 'resolvectl status ens33' showed the correct DNS server and 'nslookup lab.local' worked normally.
