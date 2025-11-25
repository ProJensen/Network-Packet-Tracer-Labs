# PAT Lab

This lab demonstrates **PAT (Port Address Translation)** using Cisco Packet Tracer.

## Objective
- Configure PAT on a Cisco router.
- Allow multiple inside hosts to access external servers using a single public IP.

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

### Outside Network
| Device | IP Address | Gateway |
| --- | --- | --- |
| Server1 | 203.203.203.11 | 203.203.203.1 |
| Server2 | 203.203.203.12 | 203.203.203.1 |
| Router | 203.203.203.1 | - |

## Router Configuration 
---
### Step 1: Permit inside network
```bash
Router(config)# access-list 1 permit 192.168.10.0 0.0.0.255
```

### Step 2: Translate using router’s public IP
```bash
Router(config)# ip nat inside source list 1 interface g0/1 overload
```

### Step 3: Verify PAT
```bash
Router# show ip nat translations
```
