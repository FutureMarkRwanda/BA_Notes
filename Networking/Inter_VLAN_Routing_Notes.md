# Implementing Inter-VLAN Routing

## Summary

This topic covers inter-VLAN routing, enabling communication between hosts in different VLANs using a router or Layer 3 switch. It includes:

* **Inter-VLAN Routing Concepts**: Understanding traditional and router-on-a-stick methods.
* **Traditional Inter-VLAN Routing Configuration**: Using multiple physical router interfaces.
* **Router-on-a-Stick Configuration**: Using a single router interface with sub-interfaces.
* **Verification and Troubleshooting**: Confirming connectivity and resolving issues.

---

## Inter-VLAN Routing Concepts

Inter-VLAN routing allows hosts in different VLANs (broadcast domains) to communicate via a routing device, such as a router or Layer 3 switch. VLANs isolate traffic for security and performance, but inter-VLAN communication requires routing to forward packets between VLANs. Two common methods are:

- **Traditional Inter-VLAN Routing**: Uses one physical router interface per VLAN, each connected to an access port on a switch. Each interface acts as the default gateway for its VLAN.
- **Router-on-a-Stick**: Uses a single router interface with sub-interfaces, each assigned to a VLAN using 802.1Q tagging. The switch port connected to the router is configured as a trunk to carry multiple VLANs.

**Key Considerations**:
- Traditional routing requires more physical interfaces, limiting scalability.
- Router-on-a-stick is more scalable but may introduce latency due to single-link bottlenecks.
- 802.1Q encapsulation tags frames to identify VLANs on trunk links.

A company needs Admin (VLAN 10) and Finance (VLAN 20) departments to communicate. A router facilitates inter-VLAN routing, ensuring secure and efficient data exchange.

---

## Traditional Inter-VLAN Routing Configuration

Traditional inter-VLAN routing uses separate physical router interfaces, each connected to a switch access port assigned to a specific VLAN. Each interface’s IP address serves as the default gateway for its VLAN’s hosts.

**Example Configuration** (VLAN 10: Admin-dept, VLAN 20: Finance-dept):
![Image](https://cdn.comparitech.com/wp-content/uploads/2020/10/Traditional-inter-VLAN-routing.jpg.webp)
```bash
! On Switch
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW1
SW1(config)# vlan 10
SW1(config-vlan)# name Admin-dept
SW1(config-vlan)# exit
SW1(config)# vlan 20
SW1(config-vlan)# name Finance-dept
SW1(config-vlan)# exit
SW1(config)# interface fa0/2
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1(config)# interface fa0/3
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 20
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1(config)# interface fa0/1
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1(config)# interface fa0/4
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 20
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1# copy running-config startup-config

! On Router
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# interface fa0/0
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface fa0/1
R1(config-if)# ip address 192.168.20.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1# copy running-config startup-config

! Host Configurations
! Host A (VLAN 10): IP 192.168.10.10, Subnet Mask 255.255.255.0, Gateway 192.168.10.1
! Host B (VLAN 20): IP 192.168.20.20, Subnet Mask 255.255.255.0, Gateway 192.168.20.1
```

**Notes**:
- Switch ports fa0/1 (VLAN 10) and fa0/4 (VLAN 20) connect to the router’s fa0/0 and fa0/1, respectively.
- Pinging from Host A to Host B succeeds after routing is configured.

A small office configures traditional inter-VLAN routing to connect Admin and Finance VLANs, using two router interfaces for direct connectivity.

---

## Router-on-a-Stick Configuration

Router-on-a-stick uses a single router interface with sub-interfaces, each assigned to a VLAN with 802.1Q encapsulation. The switch port connected to the router is set as a trunk to carry multiple VLANs, making this method more scalable than traditional routing.

**Example Configuration** (VLAN 10: Admin-dept, VLAN 20: Finance-dept):
![Diagram](https://cdn.comparitech.com/wp-content/uploads/2020/10/Router-on-a-stick-inter-VLAN-routing.jpg.webp)
```bash
! On Switch
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW1
SW1(config)# vlan 10
SW1(config-vlan)# name Admin-dept
SW1(config-vlan)# exit
SW1(config)# vlan 20
SW1(config-vlan)# name Finance-dept
SW1(config-vlan)# exit
SW1(config)# interface fa0/2
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1(config)# interface fa0/3
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 20
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1(config)# interface fa0/1
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk allowed vlan 10,20
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1# copy running-config startup-config

! On Router
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# interface fa0/1.10
R1(config-subif)# encapsulation dot1Q 10
R1(config-subif)# ip address 192.168.10.1 255.255.255.0
R1(config-subif)# exit
R1(config)# interface fa0/1.20
R1(config-subif)# encapsulation dot1Q 20
R1(config-subif)# ip address 192.168.20.1 255.255.255.0
R1(config-subif)# exit
R1(config)# interface fa0/1
R1(config-if)# no shutdown
R1(config-if)# exit
R1# copy running-config startup-config

! Host Configurations
! Host A (VLAN 10): IP 192.168.10.10, Subnet Mask 255.255.255.0, Gateway 192.168.10.1
! Host B (VLAN 20): IP 192.168.20.20, Subnet Mask 255.255.255.0, Gateway 192.168.20.1
```

**Notes**:
- The switch’s fa0/1 is a trunk port, carrying VLAN 10 and 20 traffic.
- Router sub-interfaces fa0/1.10 and fa0/1.20 handle VLAN 10 and 20, respectively, with 802.1Q tagging.
- Pinging from Host A to Host B succeeds after configuration.

A medium-sized enterprise uses router-on-a-stick to route traffic between Admin and Finance VLANs, leveraging a single router interface for cost efficiency.

---

## Verification and Troubleshooting

Verifying inter-VLAN routing confirms VLAN assignments, interface configurations, and connectivity. Troubleshooting resolves issues like failed pings or misconfigured interfaces.

**Verification Commands**:
- `show vlan brief` (Switch): Displays VLANs and associated ports.
- `show interfaces switchport` (Switch): Shows port modes and VLANs.
- `show interfaces trunk` (Switch): Confirms trunk status and allowed VLANs.
- `show ip route` (Router): Verifies routing table.
- `show running-config` (Both): Checks configurations.
- `ping <destination>` (Both): Tests connectivity between hosts.

Example output for `show ip route` on R1 (Router-on-a-Stick):
```bash
C    192.168.10.0/24 is directly connected, FastEthernet0/1.10
C    192.168.20.0/24 is directly connected, FastEthernet0/1.20
```

**Troubleshooting Common Issues**:
- **VLAN Not Created**: Missing VLANs on switch. Verify with `show vlan brief` and create with `vlan <ID>`.
- **Incorrect Port Mode**: Access port set as trunk or vice versa. Check with `show interfaces switchport` and correct with `switchport mode <access|trunk>`.
- **Sub-Interface Misconfiguration**: Missing or incorrect encapsulation. Verify with `show running-config` and set with `encapsulation dot1Q <VLAN>`.
- **Interface Down**: Port or sub-interface not active. Check with `show ip interface brief` and enable with `no shutdown`.
- **Incorrect Gateway**: Hosts cannot reach other VLANs. Verify host configurations and ensure gateways match router interface IPs.
- **Trunk VLAN Mismatch**: VLANs not passing. Confirm with `show interfaces trunk` and adjust with `switchport trunk allowed vlan <list>`.

Example troubleshooting scenario: Host A cannot ping Host B. `show interfaces switchport` on SW1 shows fa0/1 is in access mode, not trunk. Setting `switchport mode trunk` resolves the issue for router-on-a-stick.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| VLAN Not Created     | No VLAN connectivity          | Create with `vlan <ID>`              |
| Incorrect Port Mode  | Traffic not routed            | Set `switchport mode <access|trunk>` |
| Sub-Interface Error  | VLAN routing fails            | Configure `encapsulation dot1Q <VLAN>`|
| Interface Down       | No connectivity               | Enable with `no shutdown`            |

An admin finds no connectivity between VLANs 10 and 20. `show running-config` on R1 reveals fa0/1.20 lacks `encapsulation dot1Q 20`. Adding it restores inter-VLAN routing.