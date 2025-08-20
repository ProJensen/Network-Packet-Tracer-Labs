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
