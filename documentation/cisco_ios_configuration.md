# Cisco IOS Configuration Guide

This document contains the exact Cisco IOS commands required to configure the **Cisco 2911 Router** (`R1-Core`) and the **Cisco 2960-24TT Switches** for inter-subnet routing, local user authentication, Telnet access, and secure SSH v2 configuration.

---

## 1. Cisco 2911 Core Router Configuration (`R1-Core`)

### 1.1 Basic Hostname and Interface Configuration
```ios
enable
configure terminal

! Set System Hostname
hostname R1-Core

! Configure GigabitEthernet0/0 (LAN 1 Gateway)
interface GigabitEthernet0/0
 description Gateway for LAN 1 (Finance)
 ip address 192.168.10.1 255.255.255.0
 no shutdown
exit

! Configure GigabitEthernet0/1 (LAN 2 Gateway)
interface GigabitEthernet0/1
 description Gateway for LAN 2 (Engineering)
 ip address 192.168.20.1 255.255.255.0
 no shutdown
exit

! Configure GigabitEthernet0/2 (LAN 3 Gateway)
interface GigabitEthernet0/2
 description Gateway for LAN 3 (Management)
 ip address 192.168.30.1 255.255.255.0
 no shutdown
exit
```

---

### 1.2 Local User Credentials & Security Settings
```ios
! Enable Encrypted Privilege Password
enable secret CiscoSecret123!

! Create Local Admin Credentials for SSH/Telnet Authentication
username admin privilege 15 secret AdminSSH2026!
username nettech privilege 1 secret TelnetPass123!

! Set Domain Name (Mandatory for RSA Key Generation)
ip domain-name enterprise.local
```

---

### 1.3 SSH v2 RSA Cryptographic Key Generation
```ios
! Generate 2048-bit RSA Cryptographic Key Pair
crypto key generate rsa modulus 2048

! Force SSH Version 2
ip ssh version 2

! Optional: Configure SSH Authentication Timeout & Retries
ip ssh timeout 60
ip ssh authentication-retries 3
```

---

### 1.4 Virtual Terminal (VTY) Line Configuration (SSH & Telnet)
```ios
! Configure VTY lines 0 through 4 to allow both Telnet and SSH for comparative testing
line vty 0 4
 login local
 transport input ssh telnet
 exec-timeout 15 0
exit

! Configure VTY lines 5 through 15 to enforce SSH ONLY (Hardened Configuration)
line vty 5 15
 login local
 transport input ssh
 exec-timeout 10 0
exit
```

---

## 2. Cisco 2960-24TT Switch Management Configuration

### 2.1 Management Interface & Gateway (`SW-LAN1`)
```ios
enable
configure terminal
hostname SW-LAN1

! Configure Management SVI (VLAN 1)
interface vlan 1
 description Management SVI for SW-LAN1
 ip address 192.168.10.2 255.255.255.0
 no shutdown
exit

! Set Default Gateway pointing to Router R1
ip default-gateway 192.168.10.1

! Local Credentials & VTY Config
username admin secret SwitchAdminPass!
line vty 0 15
 login local
 transport input ssh
exit
```

---

## 3. Configuration Verification Commands

Verify configuration status on the Cisco IOS CLI:
```ios
! Verify Interface IP Status
show ip interface brief

! Verify SSH Status & RSA Key
show ip ssh
show crypto key mypubkey rsa

! Verify Active VTY Connections
show users
show line vty 0 4
```
