# Implementing Layer 3 Switching Inter-VLAN Routing

## Summary

This topic covers inter-VLAN routing using a multilayer switch, which combines Layer 2 switching and Layer 3 routing capabilities. It includes:

* **Layer 3 Switching Concepts**: Understanding multilayer switches and Switch Virtual Interfaces (SVIs).
* **Layer 3 Switch Configuration**: Configuring VLANs, SVIs, and routed ports for inter-VLAN routing.
* **Verification and Troubleshooting**: Confirming routing functionality and resolving issues.
* **Comparison with Other Methods**: Contrasting with traditional and router-on-a-stick routing.

---

## Layer 3 Switching Concepts

Layer 3 (multilayer) switches perform both switching and routing, enabling inter-VLAN routing without an external router. Unlike traditional inter-VLAN routing (multiple router interfaces) or router-on-a-stick (single router interface with sub-interfaces), multilayer switch routing uses **Switch Virtual Interfaces (SVIs)**—logical interfaces tied to VLANs—for routing. Each SVI is assigned an IP address in its VLAN’s subnet, acting as the default gateway for hosts. This method is scalable, reduces latency, and eliminates the need for a separate router.

**How It Works** (e.g., Host A in VLAN 10 to Host B in VLAN 20):
1. Host A sends unicast traffic to a Layer 2 (L2) switch.
2. The L2 switch tags the traffic with VLAN 10 and forwards it via a trunk to the Layer 3 (L3) switch.
3. The L3 switch removes the VLAN 10 tag, routes the traffic internally to the VLAN 20 SVI, and retags it.
4. The L3 switch sends the tagged traffic back to the L2 switch via the trunk.
5. The L2 switch removes the VLAN 20 tag and forwards the frame to Host B.

**Benefits**:
- Faster routing within the switch, reducing external link bottlenecks.
- Scalable for large networks with many VLANs.
- Simplifies topology by eliminating external routers.

Scenario: A corporate network uses a multilayer switch to route traffic between Admin (VLAN 10) and Finance (VLAN 20) departments, ensuring efficient communication without a dedicated router.

---

## Layer 3 Switch Configuration

Configuring inter-VLAN routing on a multilayer switch involves creating VLANs, assigning switch ports, enabling IP routing, configuring SVIs with IP addresses, and setting up a routed port for external connectivity (e.g., to a firewall). The example configures an L2 switch and an L3 switch for VLANs 10 and 20, with a routed port to a firewall.

**Example Configuration** (VLAN 10: Admin-dept, VLAN 20: Finance-dept):
```
! On L2 Switch
L2-Switch> enable
L2-Switch# configure terminal
L2-Switch(config)# hostname SW1-L2
SW1-L2(config)# vlan 10
SW1-L2(config-vlan)# name Admin-dept
SW1-L2(config-vlan)# exit
SW1-L2(config)# vlan 20
SW1-L2(config-vlan)# name Finance-dept
SW1-L2(config-vlan)# exit
SW1-L2(config)# interface fa0/2
SW1-L2(config-if)# switchport mode access
SW1-L2(config-if)# switchport access vlan 10
SW1-L2(config-if)# no shutdown
SW1-L2(config-if)# exit
SW1-L2(config)# interface fa0/3
SW1-L2(config-if)# switchport mode access
SW1-L2(config-if)# switchport access vlan 20
SW1-L2(config-if)# no shutdown
SW1-L2(config-if)# exit
SW1-L2(config)# interface fa0/1
SW1-L2(config-if)# switchport mode trunk
SW1-L2(config-if)# switchport trunk allowed vlan 10,20
SW1-L2(config-if)# no shutdown
SW1-L2(config-if)# exit
SW1-L2# copy running-config startup-config

! On L3 Switch
L3-Switch> enable
L3-Switch# configure terminal
L3-Switch(config)# hostname SW2-L3
SW2-L3(config)# ip routing
SW2-L3(config)# vlan 10
SW2-L3(config-vlan)# name Admin-dept
SW2-L3(config-vlan)# exit
SW2-L3(config)# vlan 20
SW2-L3(config-vlan)# name Finance-dept
SW2-L3(config-vlan)# exit
SW2-L3(config)# interface vlan 10
SW2-L3(config-if)# ip address 192.168.10.1 255.255.255.0
SW2-L3(config-if)# no shutdown
SW2-L3(config-if)# exit
SW2-L3(config)# interface vlan 20
SW2-L3(config-if)# ip address 192.168.20.1 255.255.255.0
SW2-L3(config-if)# no shutdown
SW2-L3(config-if)# exit
SW2-L3(config)# interface fa0/1
SW2-L3(config-if)# switchport trunk encapsulation dot1q
SW2-L3(config-if)# switchport mode trunk
SW2-L3(config-if)# switchport trunk allowed vlan 10,20
SW2-L3(config-if)# no shutdown
SW2-L3(config-if)# exit
SW2-L3(config)# interface fa0/0
SW2-L3(config-if)# description to Internet Firewall
SW2-L3(config-if)# no switchport
SW2-L3(config-if)# ip address 192.0.0.1 255.255.255.252
SW2-L3(config-if)# no shutdown
SW2-L3(config-if)# exit
SW2-L3(config)# ip route 0.0.0.0 0.0.0.0 192.0.0.2
SW2-L3# copy running-config startup-config

! Host Configurations
! Host A (VLAN 10): IP 192.168.10.10, Subnet Mask 255.255.255.0, Gateway 192.168.10.1
! Host B (VLAN 20): IP 192.168.20.20, Subnet Mask 255.255.255.0, Gateway 192.168.20.1
```

**Notes**:
- `ip routing` enables Layer 3 routing on the multilayer switch.
- SVIs (interface vlan 10, 20) act as default gateways for their respective VLANs.
- The routed port (fa0/0) connects to a firewall, with a default route for external traffic.
- Pinging from Host A to Host B succeeds after configuration.

Scenario: A university configures a multilayer switch to route traffic between Admin and Finance VLANs internally, with a routed port to a firewall for Internet access, simplifying the network topology.

---

## Verification and Troubleshooting

Verifying Layer 3 switching inter-VLAN routing confirms VLAN assignments, SVI configurations, routing tables, and connectivity. Troubleshooting resolves issues like failed pings or misconfigured SVIs.

**Verification Commands**:
- `show vlan brief` (Both switches): Displays VLANs and associated ports.
- `show interfaces switchport` (Both): Shows port modes and VLANs.
- `show interfaces trunk` (Both): Confirms trunk status and allowed VLANs.
- `show ip route` (L3 Switch): Verifies routing table.
- `show ip interface brief` (L3 Switch): Checks interface status.
- `show running-config` (Both): Displays configurations.
- `ping <destination>` (Both): Tests connectivity.

Example output for `show ip route` on SW2-L3:
```
      0.0.0.0/0 [120/1] via 192.0.0.2, 00:00:05, FastEthernet0/0
C     192.0.0.0/30 is directly connected, FastEthernet0/0
C     192.168.10.0/24 is directly connected, Vlan10
C     192.168.20.0/24 is directly connected, Vlan20
```

**Troubleshooting Common Issues**:
- **VLAN Not Created**: Missing VLANs on switches. Verify with `show vlan brief` and create with `vlan <ID>`.
- **SVI Not Active**: SVI down due to no active ports in VLAN. Check with `show ip interface brief` and ensure at least one port is up in the VLAN or manually enable with `no shutdown`.
- **IP Routing Disabled**: No inter-VLAN routing. Verify with `show running-config` and enable with `ip routing`.
- **Trunk Misconfiguration**: VLANs not passing. Confirm with `show interfaces trunk` and correct with `switchport trunk allowed vlan <list>`.
- **Incorrect Gateway**: Hosts cannot reach other VLANs. Verify host configurations match SVI IPs.
- **Routed Port Issue**: No external connectivity. Check with `show ip route` and ensure `no switchport` and correct IP on fa0/0.

Example troubleshooting scenario: Host A cannot ping Host B. `show ip interface brief` on SW2-L3 shows Vlan10 is down. Adding an active port to VLAN 10 with `interface fa0/4; switchport access vlan 10; no shutdown` brings the SVI up, restoring connectivity.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| VLAN Not Created     | No VLAN connectivity          | Create with `vlan <ID>`              |
| SVI Not Active       | No routing for VLAN           | Ensure active port or `no shutdown`   |
| IP Routing Disabled  | No inter-VLAN routing         | Enable `ip routing`                  |
| Trunk Misconfiguration | VLAN traffic not passing     | Set `switchport trunk allowed vlan`   |

Scenario: An admin finds no external connectivity from VLAN 10. `show ip route` on SW2-L3 lacks a default route. Adding `ip route 0.0.0.0 0.0.0.0 192.0.0.2` resolves the issue.

---

## Comparison with Other Methods

Layer 3 switching inter-VLAN routing offers advantages over traditional and router-on-a-stick methods:
- **Traditional Inter-VLAN Routing**:
  - Uses multiple physical router interfaces, one per VLAN.
  - Less scalable due to interface limitations.
  - Simpler configuration but requires more hardware.
- **Router-on-a-Stick**:
  - Uses a single router interface with sub-interfaces and 802.1Q tagging.
  - Scalable but limited by single-link bandwidth, causing potential bottlenecks.
  - Requires external router, adding complexity.
- **Layer 3 Switching**:
  - Routes internally using SVIs, no external router needed.
  - High scalability and performance due to internal routing.
  - Ideal for large networks but requires a multilayer switch.

Scenario: A growing enterprise switches from router-on-a-stick to Layer 3 switching to handle increased VLAN traffic, leveraging a multilayer switch for faster, scalable routing.