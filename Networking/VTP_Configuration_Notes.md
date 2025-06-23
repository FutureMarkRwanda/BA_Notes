# Configuring VLAN Trunk Protocol (VTP)

## Summary

This topic covers the VLAN Trunk Protocol (VTP), a Cisco-proprietary protocol for managing VLAN configurations across a network. It includes:

* **VTP Benefits and Operations**: Understanding VTP’s role, modes, and components.
* **VTP Configuration**: Setting up VTP server, client, and transparent modes with VLANs and trunks.
* **Verification and Troubleshooting**: Checking VTP status and resolving configuration issues.
* **VTP Versions and Frame Structure**: Exploring VTP versions, advertisements, and frame components.

---

## VTP Benefits and Operations

VTP (VLAN Trunk Protocol) simplifies VLAN management in large networks by synchronizing VLAN configurations across switches in the same VTP domain. It eliminates manual VLAN configuration on each switch, reducing errors and ensuring consistency. VTP operates in three modes:
- **Server**: Creates, modifies, and deletes VLANs, propagating changes via trunk ports.
- **Client**: Receives and applies VLAN updates from the server but cannot modify VLANs.
- **Transparent**: Maintains local VLAN configurations, forwarding VTP messages without applying them.

**Key Components**:
- **VTP Domain**: A group of switches sharing the same VLAN database, identified by a unique domain name (e.g., rca.ac.rw). Switches with mismatched domains do not share VTP updates.
- **VTP Advertisements**: Messages carrying VLAN information:
  - **Summary Advertisement**: Sent every 5 minutes or after a change, containing domain name and revision number.
  - **Subset Advertisement**: Details specific VLAN changes (e.g., add/delete).
  - **Advertisement Request**: Sent when a switch needs VLAN information (e.g., after reset or domain change).
- **VTP Pruning**: Reduces unnecessary broadcast traffic by restricting VLAN traffic on trunk links to only active VLANs. Enabled with `vtp pruning` or per-interface with `switchport trunk pruning vlan <list>`.

**Benefits**:
- Ensures VLAN consistency across switches.
- Simplifies VLAN additions, deletions, and renaming.
- Reduces configuration errors and management overhead.
- Supports dynamic VLAN reporting and tracking.

Scenario: A university with 50 switches uses VTP to propagate VLAN 10 (Student), VLAN 20 (Teacher), and VLAN 30 (Staff) from a server switch, ensuring uniform VLAN configurations.

---

## VTP Configuration

Configuring VTP involves setting the VTP mode, domain, and password on switches, creating VLANs on the server, and establishing trunk links. Pruning can be enabled to optimize traffic. The example configures three switches (S1 as server, S2 as client, S3 as transparent) with VLANs 10, 20, and 30.

**Example Configuration**:
```
! On S1 (VTP Server)
S1> enable
S1# configure terminal
S1(config)# hostname S1
S1(config)# vtp mode server
S1(config)# vtp domain rca.ac.rw
S1(config)# vtp password rca@123
S1(config)# vlan 10
S1(config-vlan)# name student
S1(config-vlan)# exit
S1(config)# vlan 20
S1(config-vlan)# name teacher
S1(config-vlan)# exit
S1(config)# vlan 30
S1(config-vlan)# name staff
S1(config-vlan)# exit
S1(config)# vtp pruning
S1(config)# interface fa0/1
S1(config-if)# switchport mode trunk
S1(config-if)# switchport trunk allowed vlan 1,10,20,30
S1(config-if)# exit
S1# copy running-config startup-config

! On S2 (VTP Client)
S2> enable
S2# configure terminal
S2(config)# hostname S2
S2(config)# vtp mode client
S2(config)# vtp domain rca.ac.rw
S2(config)# vtp password rca@123
S2(config)# interface fa0/1
S2(config-if)# switchport mode trunk
S2(config-if)# switchport trunk allowed vlan 1,10,20,30
S2(config-if)# exit
S2# copy running-config startup-config

! On S3 (VTP Transparent)
S3> enable
S3# configure terminal
S3(config)# hostname S3
S3(config)# vtp mode transparent
S3(config)# vtp domain rca.ac.rw
S3(config)# vtp password rca@123
S3(config)# vlan 10
S3(config-vlan)# name student
S3(config-vlan)# exit
S3(config)# vlan 20
S3(config-vlan)# name teacher
S3(config-vlan)# exit
S3(config)# vlan 30
S3(config-vlan)# name staff
S3(config-vlan)# exit
S3(config)# interface fa0/2
S3(config-if)# switchport mode trunk
S3(config-if)# switchport trunk allowed vlan 1,10,20,30
S3(config-if)# exit
S3# copy running-config startup-config
```

**Notes**:
- S1 propagates VLANs 10, 20, and 30 to S2 (client) but not S3 (transparent).
- VTP pruning reduces unnecessary VLAN traffic on trunks.
- The same domain name and password ensure VTP communication.

Scenario: A corporate network configures S1 as a VTP server to manage VLANs for departments, with S2 as a client to receive updates and S3 as transparent for local VLAN control.

---

## Verification and Troubleshooting

Verifying VTP confirms domain settings, mode, VLAN propagation, and pruning status. Troubleshooting addresses issues like missing VLANs or synchronization failures.

**Verification Commands**:
- `show vtp status`: Displays VTP mode, domain, revision number, and version.
- `show vtp password`: Shows the VTP password (if set).
- `show vtp counters`: Details VTP message statistics.
- `show vlan brief`: Verifies VLANs on the switch.

Example output for `show vtp status` on S1:
```
VTP Version                     : 2
Configuration Revision          : 3
Maximum VLANs supported locally : 1005
Number of existing VLANs        : 8
VTP Operating Mode              : Server
VTP Domain Name                 : rca.ac.rw
VTP Pruning Mode                : Enabled
VTP V2 Mode                     : Enabled
VTP Traps Generation            : Disabled
MD5 digest                      : 0x7D 0x5A ...
```

**Troubleshooting Common Issues**:
- **Mismatched VTP Domain**: Prevents VLAN synchronization. Verify with `show vtp status` and correct with `vtp domain <name>`.
- **Incorrect VTP Mode**: All switches set to client mode cause no VLAN updates. Ensure at least one server with `vtp mode server`.
- **Password Mismatch**: Blocks VTP updates. Check with `show vtp password` and align with `vtp password <password>`.
- **Revision Number Conflict**: Higher revision on a client overwrites server VLANs. Reset client with `vtp mode transparent` then `vtp mode client`.
- **Trunk Misconfiguration**: Prevents VTP messages. Verify with `show interfaces trunk` and correct with `switchport mode trunk`.
- **VTP Version Mismatch**: Incompatible versions (e.g., V1 vs. V2). Align with `vtp version <1|2|3>`.

Example troubleshooting scenario: S2 lacks VLAN 10. `show vtp status` shows a mismatched domain name (rca vs. rca.ac.rw). Setting `vtp domain rca.ac.rw` on S2 resolves the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Mismatched VTP Domain| VLANs not synchronized        | Set `vtp domain <name>`              |
| All Client Modes     | No VLAN updates               | Configure `vtp mode server` on one switch |
| Password Mismatch    | VTP updates ignored           | Align `vtp password <password>`       |
| Revision Number Conflict | VLAN database overwritten  | Reset client mode and revision       |

Scenario: An admin finds VLAN 20 missing on S2. `show vtp status` reveals a password mismatch. Setting `vtp password rca@123` on S2 restores VLAN propagation.

---

## VTP Versions and Frame Structure

**VTP Versions**:
- **V1**: Basic VLAN propagation, limited to Ethernet VLANs.
- **V2**: Adds Token Ring support, backward-compatible with V1.
- **V3**: Supports extended VLANs (1006–4094), enhanced security, and MSTP integration.

**VTP Frame Structure**:
- **Header**: Includes message type (summary, subset, request), domain name, and length.
- **Management Domain Name**: Identifies the VTP domain.
- **Configuration Revision Number**: Tracks VLAN changes; higher numbers override lower ones.
- **VLAN Information**: Lists VLAN IDs, names, and types in TLV format.

**VTP Traps**: Notify administrators of VLAN changes via SNMP, enabled with `vtp traps`.

Scenario: A network upgrades to VTP v3 to support extended VLANs and improved security, ensuring compatibility with modern Cisco switches.