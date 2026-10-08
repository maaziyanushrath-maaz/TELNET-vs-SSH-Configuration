# Comprehensive IP Addressing Table

## 1. Complete Network Addressing Matrix

The table below outlines the IP address assignments, subnet masks, interface configurations, and default gateways for all networking devices and end stations in the topology.

| Device Name | Interface | IP Address | Subnet Mask | Default Gateway | VLAN / Role |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **R1-Core** | `GigabitEthernet0/0` | `192.168.10.1` | `255.255.255.0` | N/A | LAN 1 Gateway |
| **R1-Core** | `GigabitEthernet0/1` | `192.168.20.1` | `255.255.255.0` | N/A | LAN 2 Gateway |
| **R1-Core** | `GigabitEthernet0/2` | `192.168.30.1` | `255.255.255.0` | N/A | LAN 3 Gateway |
| **SW-LAN1** | `VLAN 1 (SVI)` | `192.168.10.2` | `255.255.255.0` | `192.168.10.1` | Switch Mgmt LAN 1 |
| **SW-LAN2** | `VLAN 1 (SVI)` | `192.168.20.2` | `255.255.255.0` | `192.168.20.1` | Switch Mgmt LAN 2 |
| **SW-LAN3** | `VLAN 1 (SVI)` | `192.168.30.2` | `255.255.255.0` | `192.168.30.1` | Switch Mgmt LAN 3 |
| **PC-1** | `FastEthernet0` | `192.168.10.10` | `255.255.255.0` | `192.168.10.1` | LAN 1 Workstation |
| **PC-2** | `FastEthernet0` | `192.168.10.11` | `255.255.255.0` | `192.168.10.1` | LAN 1 Workstation |
| **PC-3** | `FastEthernet0` | `192.168.10.12` | `255.255.255.0` | `192.168.10.1` | LAN 1 Workstation |
| **PC-4** | `FastEthernet0` | `192.168.20.10` | `255.255.255.0` | `192.168.20.1` | LAN 2 Workstation |
| **PC-5** | `FastEthernet0` | `192.168.20.11` | `255.255.255.0` | `192.168.20.1` | LAN 2 Workstation |
| **PC-6** | `FastEthernet0` | `192.168.30.10` | `255.255.255.0` | `192.168.30.1` | LAN 3 Workstation |
| **PC-7** | `FastEthernet0` | `192.168.30.11` | `255.255.255.0` | `192.168.30.1` | LAN 3 Workstation |

---

## 2. Subnet Summary Table

| Subnet Identifier | Subnet Network ID | Subnet Mask | Usable Host Range | Broadcast Address | Assigned Devices |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Subnet 1 (LAN 1)** | `192.168.10.0/24` | `255.255.255.0` | `192.168.10.1` – `192.168.10.254` | `192.168.10.255` | R1 Gi0/0, SW-LAN1, PC-1, PC-2, PC-3 |
| **Subnet 2 (LAN 2)** | `192.168.20.0/24` | `255.255.255.0` | `192.168.20.1` – `192.168.20.254` | `192.168.20.255` | R1 Gi0/1, SW-LAN2, PC-4, PC-5 |
| **Subnet 3 (LAN 3)** | `192.168.30.0/24` | `255.255.255.0` | `192.168.30.1` – `192.168.30.254` | `192.168.30.255` | R1 Gi0/2, SW-LAN3, PC-6, PC-7 |
