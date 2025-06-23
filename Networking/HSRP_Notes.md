# Configuring HSRP (Hot Standby Router Protocol)

## Summary

This topic covers the Hot Standby Router Protocol (HSRP), a Cisco-proprietary First Hop Redundancy Protocol (FHRP) that ensures high availability by providing transparent failover for the default gateway. It includes:

* **HSRP Operations**: Understanding HSRP’s role, states, and versions.
* **HSRP Configuration**: Setting up HSRP on Cisco routers with RIP for routing.
* **Verification and Troubleshooting**: Checking HSRP functionality and resolving issues.

---

## HSRP Operations

HSRP (Hot Standby Router Protocol) is a Cisco-proprietary FHRP that provides redundancy for the default gateway by allowing multiple routers to share a virtual IP and MAC address. Hosts use this virtual IP as their gateway, ensuring connectivity even if the active router fails. HSRP is part of the FHRP family, alongside VRRP (Virtual Router Redundancy Protocol) and GLBP (Gateway Load Balancing Protocol). HSRP operates by electing one router as the active router, which forwards traffic, and another as the standby router, which takes over if the active router fails.

HSRP has six states:
- **Initial**: HSRP is not running (e.g., during interface startup).
- **Learn**: Router awaits the virtual IP and active router’s hello messages.
- **Listen**: Router knows the virtual IP/MAC but is neither active nor standby.
- **Speak**: Router sends hellos and participates in active/standby election.
- **Standby**: Router monitors the active router, ready to take over if it fails.
- **Active**: Router forwards traffic and sends periodic hellos.

HSRP versions:
- **Version 1**: Uses multicast 224.0.0.2, UDP port 1985, group numbers 0–255.
- **Version 2**: Uses multicast 224.0.0.102, UDP port 1985, group numbers 0–4095, with improved timers and IPv6 support.

Key features:
- Transparent failover for high availability.
- Priority-based election (default 100, higher is preferred).
- Preemption allows a higher-priority router to reclaim the active role.
- Authentication (e.g., MD5) secures HSRP communication.

Scenario: A company uses HSRP to ensure PCs on a LAN (10.0.0.0/24) maintain connectivity to other networks via a virtual gateway, even if one router fails.

---

## HSRP Configuration

Configuring HSRP involves assigning a virtual IP address to a group of routers, setting priorities, enabling preemption, and optionally adding authentication. The provided topology includes three routers (R1, R2, R3) with RIPv2 for routing, where R1 and R2 form an HSRP group for LAN 10.0.0.0/24, using virtual IP 10.0.0.254.

**Configuration Example**:
```
! On R1
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# interface s0/2/0
R1(config-if)# ip address 20.0.0.1 255.255.255.252
R1(config-if)# clock rate 64000
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface g0/0
R1(config-if)# ip address 10.0.0.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# standby 10 ip 10.0.0.254
R1(config-if)# standby 10 priority 110
R1(config-if)# standby 10 preempt
R1(config-if)# standby 10 authentication md5 key-string mypassword
R1(config-if)# exit
R1(config)# router rip
R1(config-router)# version 2
R1(config-router)# network 10.0.0.0
R1(config-router)# network 20.0.0.0
R1(config-router)# exit
R1# copy running-config startup-config

! On R2
R2> enable
R2# configure terminal
R2(config)# hostname R2
R2(config)# interface s0/2/0
R2(config-if)# ip address 30.0.0.1 255.255.255.252
R2(config-if)# clock rate 64000
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface g0/0
R2(config-if)# ip address 10.0.0.2 255.255.255.0
R2(config-if)# no shutdown
R2(config-if)# standby 10 ip 10.0.0.254
R2(config-if)# standby 10 preempt
R2(config-if)# standby 10 authentication md5 key-string mypassword
R2(config-if)# exit
R2(config)# router rip
R2(config-router)# version 2
R2(config-router)# network 10.0.0.0
R2(config-router)# network 30.0.0.0
R2(config-router)# exit
R2# copy running-config startup-config

! On R3
R3> enable
R3# configure terminal
R3(config)# hostname R3
R3(config)# interface s0/2/0
R3(config-if)# ip address 20.0.0.2 255.255.255.252
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# interface s0/2/1
R3(config-if)# ip address 30.0.0.2 255.255.255.252
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# interface g0/0
R3(config-if)# ip address 40.0.0.1 255.255.255.0
R3(config-if)# no shutdown
R3(config-if)# exit
R3(config)# router rip
R3(config-router)# version 2
R3(config-router)# network 20.0.0.0
R3(config-router)# network 30.0.0.0
R3(config-router)# network 40.0.0.0
R3(config-router)# exit
R3# copy running-config startup-config
```

**PC Configuration**:
- Configure PCs on the 10.0.0.0/24 LAN with default gateway 10.0.0.254 (virtual IP).

Scenario: A small office configures HSRP on R1 and R2 for LAN 10.0.0.0/24, with R1 as the active router (higher priority) and R2 as standby, ensuring seamless gateway failover.

---

## Verification and Troubleshooting

Verifying HSRP confirms the active/standby roles and virtual IP functionality. Troubleshooting addresses issues like misconfigurations or connectivity failures.

**Verification Commands**:
- `show standby`: Displays HSRP details (e.g., state, virtual IP, priority).
- `show standby brief`: Summarizes HSRP group status.

Example output for `show standby brief` on R1:
```
Interface   Grp  Pri P State   Active          Standby         Virtual IP
Gi0/0       10   110 P Active  local           10.0.0.2        10.0.0.254
```

**Troubleshooting Common Issues**:
- **Mismatched Virtual IP**: Routers must use the same virtual IP. Verify with `show standby` and correct with `standby <group> ip <IP>`.
- **Priority Misconfiguration**: Incorrect priorities prevent desired active router election. Check `show standby` and adjust with `standby <group> priority <value>`.
- **Authentication Mismatch**: Different passwords or algorithms block HSRP communication. Verify with `show running-config` and align with `standby <group> authentication md5 key-string <password>`.
- **Preemption Disabled**: A higher-priority router doesn’t take over. Enable with `standby <group> preempt`.
- **Interface Issues**: Shut or misconfigured interfaces prevent HSRP operation. Use `show ip interface brief` and issue `no shutdown`.
- **Version Mismatch**: HSRP v1 and v2 are incompatible. Verify with `show standby` and set with `standby version <1|2>`.

Example troubleshooting scenario: R1 is not active despite higher priority. `show standby` shows preemption is disabled. Adding `standby 10 preempt` on R1 makes it active.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Mismatched Virtual IP| No HSRP adjacency             | Set same `standby <group> ip <IP>`    |
| Authentication Mismatch | HSRP not forming            | Align `standby <group> authentication`|
| Preemption Disabled  | Higher-priority router not active | Enable `standby <group> preempt`   |
| Version Mismatch     | Incompatible HSRP messages    | Set same `standby version <1|2>`      |

Scenario: An admin notices PCs lose connectivity when R1 fails. `show standby` on R2 reveals a mismatched authentication password. Correcting it with `standby 10 authentication md5 key-string mypassword` restores failover.