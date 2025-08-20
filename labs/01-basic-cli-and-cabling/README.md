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

Verify:

```bash
show startup-config
```
![Verify S1](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/01-basic-cli-and-cabling/screenshots/Verify_S1.png)

---

## Step 3 — Configure the router (R1)

Open R1 → CLI:

```bash
enable
configure terminal
interface g0/0
  ip address 192.168.10.1 255.255.255.0
  no shutdown
end
copy run start
```

![Configure R1](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/01-basic-cli-and-cabling/screenshots/Configure_R1.png)

![Device & Cabling 2](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/01-basic-cli-and-cabling/screenshots/Place_Devices_Cable_2.png)

---

## Step 4 — Configure the PCs

On each PC: Desktop → IP Configuration

PC1: `IP 192.168.10.10`, `Mask 255.255.255.0`, `GW 192.168.10.1`

PC2: `IP 192.168.10.11`, `Mask 255.255.255.0`, `GW 192.168.10.1`

### PC1
![PC1 IP Config](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/01-basic-cli-and-cabling/screenshots/PC1_IP.%20Config.png)

### PC2
![PC2 IP Config](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/01-basic-cli-and-cabling/screenshots/PC2_IP%20Config.png)

---

## Step 5 — Verify

   - S1: `show ip interface brief` → `Vlan1` is `up/up` with `192.168.10.2`

![S1 Vlan1](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/01-basic-cli-and-cabling/screenshots/S1_Vlan1.png)

   - R1: `show ip interface brief` → `Gi0/0` is `up/up` with `192.168.10.1`

![R1 G0/0](https://github.com/ProJensen/Network-Packet-Tracer-Labs/blob/main/labs/01-basic-cli-and-cabling/screenshots/R1_G0%3A0.png)

   - PC1: Command Prompt → `ping 192.168.10.11` (PC2) → success

![PC1 ping PC2](https://raw.githubusercontent.com/ProJensen/Network-Packet-Tracer-Labs/refs/heads/main/labs/01-basic-cli-and-cabling/screenshots/PC1_ping_PC2.png)

   - PC1: `ping 192.168.10.1` (R1) → success

