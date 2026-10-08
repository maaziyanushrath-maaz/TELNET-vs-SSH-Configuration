# Network Topology & Architecture Specification

## 1. Executive Summary

This document details the topology and hardware interconnectivity for the **TELNET-vs-SSH-Configuration** project designed in Cisco Packet Tracer. The network infrastructure demonstrates a multi-subnet enterprise environment linked by a central Cisco 2911 router, providing inter-VLAN routing, subnet gateway services, and remote management access via Telnet and SSH v2.

---

## 2. Hardware Inventory

| Device Name | Device Model | Quantity | Interfaces Used | Role / Description |
| :--- | :--- | :---: | :--- | :--- |
| **R1-Core** | Cisco 2911 Integrated Services Router | 1 | `Gi0/0`, `Gi0/1`, `Gi0/2` | Core Inter-Subnet Router & SSH/Telnet Server |
| **SW-LAN1** | Cisco Catalyst 2960-24TT Switch | 1 | `Gi0/1`, `Fa0/1` – `Fa0/3` | Access Switch for LAN Subnet 1 (Finance) |
| **SW-LAN2** | Cisco Catalyst 2960-24TT Switch | 1 | `Gi0/1`, `Fa0/1` – `Fa0/2` | Access Switch for LAN Subnet 2 (Engineering) |
| **SW-LAN3** | Cisco Catalyst 2960-24TT Switch | 1 | `Gi0/1`, `Fa0/1` – `Fa0/2` | Access Switch for LAN Subnet 3 (Management) |
| **PC-1 to PC-7** | Generic Desktop PC | 7 | `FastEthernet0` | End-user workstations for remote access testing |

---

## 3. Physical & Logical Interconnections

### 3.1 Router Interface Connectivity Matrix

| Central Router Interface | Connected Switch | Switch Port | Target Subnet | Subnet Network ID |
| :--- | :--- | :--- | :--- | :--- |
| **R1 GigabitEthernet0/0** | `SW-LAN1` | `GigabitEthernet0/1` | LAN 1 (Finance) | `192.168.10.0/24` |
| **R1 GigabitEthernet0/1** | `SW-LAN2` | `GigabitEthernet0/1` | LAN 2 (Engineering) | `192.168.20.0/24` |
| **R1 GigabitEthernet0/2** | `SW-LAN3` | `GigabitEthernet0/1` | LAN 3 (Management) | `192.168.30.0/24` |

---

### 3.2 End Device Port Mapping

#### Subnet 1: `192.168.10.0/24` (Finance Department)
* **SW-LAN1 Port `Fa0/1`** $\rightarrow$ **PC-1** (`192.168.10.10`)
* **SW-LAN1 Port `Fa0/2`** $\rightarrow$ **PC-2** (`192.168.10.11`)
* **SW-LAN1 Port `Fa0/3`** $\rightarrow$ **PC-3** (`192.168.10.12`)

#### Subnet 2: `192.168.20.0/24` (Engineering Department)
* **SW-LAN2 Port `Fa0/1`** $\rightarrow$ **PC-4** (`192.168.20.10`)
* **SW-LAN2 Port `Fa0/2`** $\rightarrow$ **PC-5** (`192.168.20.11`)

#### Subnet 3: `192.168.30.0/24` (Management Department)
* **SW-LAN3 Port `Fa0/1`** $\rightarrow$ **PC-6** (`192.168.30.10`)
* **SW-LAN3 Port `Fa0/2`** $\rightarrow$ **PC-7** (`192.168.30.11`)

---

## 4. Visual Topology Diagram

```
                        +----------------------------+
                        |       Cisco 2911           |
                        |      R1-Core Router        |
                        +--------------+-------------+
                                       |
           +---------------------------+---------------------------+
           | Gi0/0                     | Gi0/1                     | Gi0/2
           v                           v                           v
+----------------------+    +----------------------+    +----------------------+
|   SW-LAN1 (2960)     |    |   SW-LAN2 (2960)     |    |   SW-LAN3 (2960)     |
|   192.168.10.0/24    |    |   192.168.20.0/24    |    |   192.168.30.0/24    |
+---+------+------+----+    +---+------+-----------+    +---+------+-----------+
    |      |      |             |      |                    |      |
    v      v      v             v      v                    v      v
  PC-1   PC-2   PC-3          PC-4   PC-5                 PC-6   PC-7
```

---

## 5. Architectural Notes

1. **Routing Layer**: The Cisco 2911 router operates as the default gateway across all 3 subnets, facilitating inter-subnet IP routing.
2. **Access Layer**: Three Cisco 2960-24TT layer-2 switches aggregate traffic from end workstations into dedicated collision domains.
3. **Management Boundaries**: Remote administration (Telnet / SSH v2) is initiated from any workstation PC across subnets targeting the Gateway router interfaces or switch management IPs.
