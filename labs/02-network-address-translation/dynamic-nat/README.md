# Dynamic NAT Lab

This lab demonstrates **Dynamic Network Address Translation (Dynamic NAT)** using Cisco Packet Tracer.

## Objective
- Configure a single router to translate inside private IPs to public IPs.

## Topology 
- 1 Router
- 2 Switches
- 2 Servers (outside)
- 2 Laptops + 3 Desktops (inside)

## Topology Overview
![Topology](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/02-network-address-translation/screenshots/NAT-Topology-Static.png)

## IP Addressing Plan
### Inside Network
| Device | IP Address | Gateway |
| --- | --- | --- |
| Laptop 1 | 192.168.10.11 | 192.168.10.1 |
| PC 1 | 192.168.10.12 | 192.168.10.1 |
| PC 2 | 192.168.10.13 | 192.168.10.1 |
| PC 3 | 192.168.10.14 | 192.168.10.1 |
| Laptop 2 | 192.168.10.15 | 192.168.10.1 |
| Router | 192.168.10.1 | - |

## Router Configuration 
---
### Step 1: Create the NAT Pool
```bash
Router(config)# ip nat pool NAT_POOL 203.203.203.2 203.203.203.254 netmask 255.255.255.0
```

### Step 2: Create an ACL for the Inside Network
```bash
Router(config)# access-list 1 permit 192.168.10.0 0.0.0.255
```

### Step 3: Enable Dynamic NAT
Link the ACL to the NAT pool:
```bash
Router(config)# ip nat inside source list 1 pool NAT_POOL
```
