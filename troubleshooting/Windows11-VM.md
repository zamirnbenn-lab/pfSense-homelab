# Windows 11 Network Connectivity Issue

## Problem

While setting up the Windows 11 VM, it was not getting a working network connection when connected to VMware's Host-only network.

## What I Changed

I decided to move the lab network to a dedicated VMware LAN Segment instead. This kept the Windows 11 client and pfSense LAN on the same isolated network and allowed pfSense to handle the network connection.

## Resolution

I changed the pfSense LAN adapter from Host-only to a dedicated LAB-LAN segment, connected the Windows 11 VM to that same segment, kept the pfSense WAN on VMware NAT, and restarted pfSense before starting the Windows 11 VM.

After making these changes, the Windows 11 VM was able to connect successfully through pfSense.
