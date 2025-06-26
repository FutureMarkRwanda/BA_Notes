# Configuring VLANs

## Summary

This topic covers the configuration of Virtual Local Area Networks (VLANs) to segment networks logically, enhancing performance and security. It includes:

* **Hierarchical Network Model and Switching Concepts**: Understanding network design and switch operations.
* **VLAN Operations and Benefits**: Exploring VLAN types, ranges, and advantages.
* **VLAN Configuration**: Creating VLANs, assigning ports, and configuring trunk ports.
* **Verification and Troubleshooting**: Checking VLAN configurations and resolving issues.

---

## Hierarchical Network Model and Switching Concepts

The hierarchical network model organizes campus networks into three layers:
- **Access Layer**: Connects end devices (e.g., PCs, phones) to the network, providing user access.
- **Distribution Layer**: Aggregates access layer traffic, enforces policies, and connects to the core layer.
- **Core Layer**: Provides high-speed transport between distribution switches.

Benefits include scalability, redundancy, performance, security, manageability, and maintainability. Structured engineering principles like hierarchy, modularity, resiliency, and flexibility ensure reliable network design.

Switching involves forwarding frames based on the ingress port and destination MAC address. Switches maintain a **MAC address table** to map MAC addresses to ports, reducing flooding (broadcasting to all ports). Use `show mac-address-table` to view the table. A **collision domain** is a network segment where devices can collide when transmitting; switches reduce collisions by creating separate collision domains per port. Full-duplex communication and higher-bandwidth devices further minimize collisions.

A university uses a hierarchical network with access switches for student devices, distribution switches for policy enforcement, and core switches for fast inter-building connectivity.

---

## VLAN Operations and Benefits

A VLAN (Virtual Local Area Network) logically segments devices into separate broadcast domains, regardless of physical location, improving security and performance. Each VLAN acts as a distinct network with its own IP addressing and policies, requiring a Layer 3 device (e.g., router) for inter-VLAN communication.

**Benefits**:
- **Security**: Isolates sensitive traffic (e.g., management VLAN).
- **Performance**: Reduces broadcast domains, alleviating congestion.
- **Management**: Simplifies device grouping by function or department.
- **Scalability**: Supports network growth with smaller, manageable segments.

**VLAN Types**:
- **Default VLAN**: VLAN 1, non-deletable, carries all traffic initially.
- **Data VLAN**: Carries user data (e.g., PC traffic).
- **Voice VLAN**: Prioritizes VoIP traffic for quality (delay <150ms).
- **Management VLAN**: Dedicated for switch management (not VLAN 1 for security).
- **Native VLAN**: Handles untagged traffic on 802.1Q trunk ports, ideally unused.

**VLAN Ranges**:
- 0, 4095: Reserved for system use.
- 1: Default VLAN, non-deletable.
- 2–1001: Normal range, user-configurable.
- 1002–1005: Legacy FDDI/Token Ring, non-deletable.
- 1006–4094: Extended range, Ethernet only, not propagated by VTP.

A company uses VLAN 10 for employee data, VLAN 20 for VoIP, and VLAN 99 for management to isolate and prioritize traffic.

---

## VLAN Configuration

Configuring VLANs involves creating VLANs, naming them, assigning switch ports to VLANs, and setting up trunk ports for inter-switch connectivity. Access ports connect to end devices, carrying traffic for a single VLAN, while trunk ports carry multiple VLANs using 802.1Q tagging. Sub-interfaces on routers enable inter-VLAN routing.

**Example Configuration** for a switch and router, with VLAN 10 (Student) and VLAN 20 (Teacher):
![Diagram](https://res.cloudinary.com/ddsojj7zo/image/upload/v1750949794/Capture_d_%C3%A9cran_du_2025-06-26_16-56-14_lyn6rg.png)
```bash
! On Switch
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW1
Switch(config)# vlan 10
Switch(config-vlan)# name student
Switch(config-vlan)# state active
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# name teacher
Switch(config-vlan)# state active
Switch(config-vlan)# exit
Switch(config)# interface range fa0/1-3
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit
Switch(config)# interface range fa0/4-6
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20
Switch(config-if-range)# exit
Switch(config)# interface fa0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 1,10,20
Switch(config-if)# exit
Switch# copy running-config startup-config

! On Router (for inter-VLAN routing)
Router> enable
Router# configure terminal
Router(config)# hostname R1
Router(config)# interface g0/0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# interface g0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit
Router(config)# interface g0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit
Router# copy running-config startup-config
```

**PC Configuration**:
- PC1 (VLAN 10): IP 192.168.10.10/24, Gateway 192.168.10.1
- PC2 (VLAN 20): IP 192.168.20.10/24, Gateway 192.168.20.1

A school configures VLAN 10 for student devices and VLAN 20 for teacher devices, with a trunk to a router for inter-VLAN routing, ensuring isolated broadcast domains.

---

## Verification and Troubleshooting

Verifying VLAN configurations confirms VLAN creation, port assignments, and trunk functionality. Troubleshooting addresses issues like misconfigurations or connectivity problems.

**Verification Commands**:
- `show vlan brief`: Displays VLANs, names, and associated ports.
- `show interfaces switchport`: Shows port modes and VLAN assignments.
- `show mac-address-table`: Verifies MAC-to-port mappings.
- `show interfaces trunk`: Confirms trunk status and allowed VLANs.

Example output for `show vlan brief` on SW1:
```bash
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/7, Fa0/8, ...
10   student                          active    Fa0/1, Fa0/2, Fa0/3
20   teacher                          active    Fa0/4, Fa0/5, Fa0/6
```

**Troubleshooting Common Issues**:
- **VLAN Not Created**: Missing VLAN in database. Verify with `show vlan` and create with `vlan <ID>`.
- **Port Not in VLAN**: Incorrect port assignment. Check `show interfaces switchport` and correct with `switchport access vlan <ID>`.
- **Trunk Misconfiguration**: VLANs not passing. Verify with `show interfaces trunk` and ensure `switchport mode trunk` and `switchport trunk allowed vlan <list>`.
- **Inter-VLAN Routing Failure**: Missing sub-interfaces or incorrect encapsulation. Check router `show running-config` and configure `encapsulation dot1Q <VLAN>`.
- **Native VLAN Mismatch**: Causes trunk issues. Align native VLANs with `switchport trunk native vlan <ID>` on both switches.
- **Port Shutdown**: Interface down blocks traffic. Use `show ip interface brief` and issue `no shutdown`.

Example troubleshooting scenario: PCs in VLAN 10 cannot reach VLAN 20. `show running-config` on the router shows missing sub-interface for VLAN 20. Adding `interface g0/0.20` with `encapsulation dot1Q 20` resolves the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| VLAN Not Created     | VLAN missing in `show vlan`    | Create with `vlan <ID>`               |
| Port Not in VLAN     | No connectivity in VLAN        | Set `switchport access vlan <ID>`     |
| Trunk Misconfiguration | VLAN traffic not passing      | Configure `switchport mode trunk`     |
| Native VLAN Mismatch | Trunk errors                  | Align `switchport trunk native vlan`  |

An admin finds student PCs (VLAN 10) have no connectivity. `show interfaces switchport` reveals fa0/1 is in VLAN 1. Reassigning with `switchport access vlan 10` restores connectivity.