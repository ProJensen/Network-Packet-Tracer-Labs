[← Back to Index](../../README.md)

# Lab 01 — Basic CLI & Cabling (Packet Tracer)

Warm-up lab: small routed LAN + essential Cisco CLI.

> Tested with Cisco Packet Tracer 8.2+

---

## Before you start
- Save as `Lab01_Basic_CLI_CABLING.pkt`
- Devices: **1×2960 switch**, **1×2911 router**, **2×PC**

## Objectives
- Cable **PC1/PC2 ↔ S1 (2960) ↔ R1 (2911)**
- Secure basic access (hostname, console/VTY, enable secret)
- Configure **switch management SVI (VLAN 1)** + **default gateway**
- Configure **router LAN interface (G0/0)**
- Set PC IPs and verify **end-to-end connectivity**

## Topology
PC1 ──(Fa)── S1 ──(G0/1 ↔ G0/0)── R1

PC2 ──(Fa)── S1

---

## Step 1 — Place devices & cable
1. Add: **2960**, **2911**, **2×PC**
2. Cable:
   - `PC1 Fa0` → `S1 Fa0/1` (Copper Straight-Through)
   - `PC2 Fa0` → `S1 Fa0/2` (Copper Straight-Through)
   - `S1 Gi0/1` → `R1 Gi0/0` (Copper Straight-Through)
3. Wait for link LEDs to go green.

![Devices & Cabling](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/01-basic-cli-and-cabling/screenshots/Place_Devices_Cable.png)

---

## Step 2 — Configure the switch (S1)
Open **S1 → CLI**:

```bash
enable
configure terminal
interface vlan 1
  ip address 192.168.10.2 255.255.255.0
  no shutdown
exit
ip default-gateway 192.168.10.1
end
copy run start
```
![Configure S1](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/01-basic-cli-and-cabling/screenshots/Configure_S1.png)

