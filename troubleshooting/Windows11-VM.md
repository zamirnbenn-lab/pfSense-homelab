# Windows 11 Network Connectivity Issue

## Problem

While setting up the Windows 11 VM, it was not getting a working network connection when connected to VMware's Host-only network.

## What I Changed

I decided to move the lab network to a dedicated VMware LAN Segment instead. This kept the Windows 11 client and pfSense LAN on the same isolated network and allowed pfSense to handle the network connection.

## Resolution

- Changed the pfSense LAN adapter from Host-only to a LAN Segment
- Created a LAN Segment called `LAB-LAN`
- Connected the Windows 11 VM to `LAB-LAN`
- Left the pfSense WAN adapter connected to VMware NAT
- Restarted pfSense before starting the Windows 11 VM

After making these changes, the Windows 11 VM was able to connect successfully through pfSense.
