# SERVER Interface ICMP Rule Issue

## Problem

After moving the Ubuntu Server to the new 'SERVER-LAN' network, the server was able to use the new IP address '192.168.20.20', but it could not ping the pfSense SERVER interface at '192.168.20.1'.

The VMware network settings and interface configuration were correct, and pfSense was able to ping the Ubuntu Server from its own console.

## Resolution

I created a new firewall rule on the SERVER interface to allow ICMP traffic from the 'SERVER' network to the pfSense SERVER address.

The rule used:

- Action: Pass
- Protocol: ICMP
- Source: SERVER subnets
- Destination: SERVER address

After saving and applying the rule, the Ubuntu Server was able to successfully ping '192.168.20.1'.
