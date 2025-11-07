# Static NAT Lab

This lab demonstrates **Static Network Address Translation (Static NAT)** using Cisco Packet Tracer.

## Objective
- Configure a single router to translate inside private IPs to public IPs.

## Topology
- 1 Router
- 2 Switches
- 2 Servers (outside)
- 2 Laptops + 3 Desktops (inside)

## Topology Overview
![Static-NAT](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/02-network-address-translation/screenshots/NAT-Topology.png)

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

### Laptop 1
![Laptop1](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/02-network-address-translation/screenshots/Laptop%201.png)

### Outside Network
| Device | IP Address | Gateway |
| --- | --- | --- |
| Server1 | 203.203.203.11 | 203.203.203.1 |
| Server2 | 203.203.203.12 | 203.203.203.1 |
| Router | 203.203.203.1 | - |

### Server 1
![Server1](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/02-network-address-translation/screenshots/Server%201.png)

## Router Configuration (Static NAT)
---
### Step 1: Configure Interfaces

```bash
Router> enable
Router# configure terminal

! Inside interface
Router(config)# interface g0/0
Router(config-if)# ip address 192.168.10.1 255.255.255.0
Router(config-if)# ip nat inside
Router(config-if)# no shutdown
Router(config-if)# exit

! Outside interface
Router(config)# interface g0/1
Router(config-if)# ip address 203.0.113.1 255.255.255.0
Router(config-if)# ip nat outside
Router(config-if)# no shutdown
Router(config-if)# exit
```
