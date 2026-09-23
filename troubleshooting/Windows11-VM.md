# Windows 11 Network Connectivity Issue

## Problem

While setting up the Windows 11 VM, it was not getting a working network connection through VMware's Host-only network.

## Resolution

I switched the pfSense LAN and Windows 11 VM over to a dedicated LAB-LAN segment while keeping the pfSense WAN connected through VMware NAT. After restarting pfSense and the Windows 11 VM, the client was able to connect successfully through pfSense.

This fixed the issue and gave me a cleaner isolated network for the lab.
