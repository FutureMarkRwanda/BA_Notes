# Configuring Spanning Tree Protocol (STP)

## Summary

This topic covers the Spanning Tree Protocol (STP), a Layer 2 protocol that prevents loops in Ethernet networks by managing redundant paths. It includes:

* **STP Operations**: Understanding STP’s role, algorithm, and port states.
* **STP Configuration**: Setting up STP, including bridge IDs and modes.
* **Verification and Troubleshooting**: Checking STP status and resolving issues.
* **STP Variants**: Comparing STP, RSTP, PVST, RPVST, and MSTP.

---

## STP Operations

STP (Spanning Tree Protocol) ensures loop-free Layer 2 networks by selectively blocking redundant paths while maintaining connectivity. Redundant links between switches enhance reliability but risk creating loops, causing broadcast storms and network instability. STP uses the Spanning Tree Algorithm (STA) to build a loop-free topology by electing a root bridge, determining root and designated ports, and blocking non-designated ports.

**Key Components**:
- **Root Bridge**: The central reference point, elected based on the lowest Bridge ID (BID), which combines a 2-byte bridge priority (default 32768) and a 6-byte MAC address.
- **Root Port**: Each non-root switch selects one port with the lowest path cost to the root bridge.
- **Designated Port**: One port per network segment with the lowest path cost to the root bridge, used for forwarding.
- **Non-Designated Port**: Blocked to prevent loops, with higher path costs.
- **BPDUs (Bridge Protocol Data Units)**: Multicast frames (224.0.0.2) used to exchange information. Types include:
  - Configuration BPDU: Elects root bridge and determines roles.
  - Topology Change Notification (TCN) BPDU: Signals topology changes (e.g., link or switch failure).
  - Topology Change Acknowledgment (TCA) BPDU: Confirms TCN receipt.

**Port States**:
- **Disabled**: Port is shut down, no STP participation.
- **Blocking**: Receives BPDUs but discards frames, no forwarding (20 seconds default, max_age).
- **Listening**: Sends/receives BPDUs, computes loop-free topology, no frame forwarding (15 seconds, forward_delay).
- **Learning**: Learns MAC addresses, no frame forwarding (15 seconds, forward_delay).
- **Forwarding**: Forwards frames, learns MAC addresses, fully operational.

**Topology Changes**: Triggered by link failures, switch failures, or ports entering forwarding state, prompting STP to recalculate the topology.

Scenario: A campus network with redundant switch links uses STP to prevent loops, electing one switch as the root bridge and blocking redundant ports to ensure stable communication.

---

## STP Configuration

Configuring STP involves setting the bridge priority to influence root bridge election, changing STP modes (e.g., Rapid Per-VLAN Spanning Tree), and ensuring proper port roles. By default, Cisco switches run Per-VLAN Spanning Tree (PVST), creating a separate STP instance per VLAN.

**Example Configuration** for a network with two switches (SW1, SW2) and VLANs 10 and 20:
```
! On SW1 (desired root bridge for VLAN 10)
SW1> enable
SW1# configure terminal
SW1(config)# hostname SW1
SW1(config)# vlan 10
SW1(config-vlan)# name student
SW1(config-vlan)# exit
SW1(config)# vlan 20
SW1(config-vlan)# name teacher
SW1(config-vlan)# exit
SW1(config)# interface fa0/1
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1(config)# interface fa0/2
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 20
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1(config)# interface fa0/24
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk allowed vlan 10,20
SW1(config-if)# no shutdown
SW1(config-if)# exit
SW1(config)# spanning-tree mode rapid-pvst
SW1(config)# spanning-tree vlan 10 priority 4096
SW1(config)# spanning-tree vlan 20 priority 8192
SW1(config)# exit
SW1# copy running-config startup-config

! On SW2
SW2> enable
SW2# configure terminal
SW2(config)# hostname SW2
SW2(config)# vlan 10
SW2(config-vlan)# name student
SW2(config-vlan)# exit
SW2(config)# vlan 20
SW2(config-vlan)# name teacher
SW2(config-vlan)# exit
SW2(config)# interface fa0/1
SW2(config-if)# switchport mode access
SW2(config-if)# switchport access vlan 10
SW2(config-if)# no shutdown
SW2(config-if)# exit
SW2(config)# interface fa0/2
SW2(config-if)# switchport mode access
SW2(config-if)# switchport access vlan 20
SW2(config-if)# no shutdown
SW2(config-if)# exit
SW2(config)# interface fa0/24
SW2(config-if)# switchport mode trunk
SW2(config-if)# switchport trunk allowed vlan 10,20
SW2(config-if)# no shutdown
SW2(config-if)# exit
SW2(config)# spanning-tree mode rapid-pvst
SW2(config)# spanning-tree vlan 10 priority 8192
SW2(config)# spanning-tree vlan 20 priority 4096
SW2(config)# exit
SW2# copy running-config startup-config
```

**Notes**:
- SW1 is configured as the root bridge for VLAN 10 (priority 4096) and secondary for VLAN 20.
- SW2 is the root bridge for VLAN 20 (priority 4096) and secondary for VLAN 10.
- Rapid Per-VLAN Spanning Tree (RPVST) is enabled for faster convergence.
- Alternatively, use `spanning-tree vlan <ID> root primary` to set the root bridge dynamically.

Scenario: A school network configures SW1 as the root bridge for VLAN 10 (student devices) and SW2 for VLAN 20 (teacher devices), using RPVST to ensure fast recovery from link failures.

---

## Verification and Troubleshooting

Verifying STP confirms the root bridge, port roles, and topology status. Troubleshooting addresses issues like incorrect root bridge election or blocked ports.

**Verification Commands**:
- `show spanning-tree`: Displays root bridge, bridge IDs, port roles, and states.
- `show spanning-tree vlan <ID>`: Shows STP details for a specific VLAN.
- `show spanning-tree summary`: Summarizes STP mode and root bridge status.

Example output for `show spanning-tree vlan 10` on SW1:
```
VLAN0010
  Spanning tree enabled protocol rapid-pvst
  Root ID    Priority    4106
             Address     0019.569d.4a00
             This bridge is the root
  Bridge ID  Priority    4106  (priority 4096 sys-id-ext 10)
             Address     0019.569d.4a00
  Interface           Role Sts Cost      Prio.Nbr Type
  ------------------- ---- --- --------- -------- --------------------------------
  Fa0/24              Desg FWD 19        128.24   P2p
```

**Troubleshooting Common Issues**:
- **Incorrect Root Bridge**: Unexpected switch is root. Verify with `show spanning-tree` and set priority with `spanning-tree vlan <ID> priority <value>` or `root primary`.
- **Blocked Ports**: Desired port is blocked. Check path costs with `show spanning-tree` and adjust with `spanning-tree cost <value>` on the interface.
- **STP Mode Mismatch**: Switches run different modes (e.g., PVST vs. RSTP). Align with `spanning-tree mode <mode>`.
- **BPDU Not Received**: Root bridge failure suspected. Verify connectivity with `ping` and check BPDU timers with `show spanning-tree`.
- **Topology Change Loops**: Frequent changes cause instability. Identify failed links with `show spanning-tree` and stabilize with portfast or BPDU guard.
- **VLAN Misconfiguration**: VLAN not included in trunk. Verify with `show interfaces trunk` and correct with `switchport trunk allowed vlan <list>`.

Example troubleshooting scenario: SW2’s fa0/24 is blocked for VLAN 10, but it should be forwarding. `show spanning-tree vlan 10` shows SW2 has a higher priority (8192) than SW1 (4096). Setting `spanning-tree vlan 10 priority 4096` on SW2 makes it the root, resolving the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Incorrect Root Bridge| Wrong switch is root          | Set `spanning-tree vlan <ID> priority`|
| Blocked Port         | Desired port not forwarding   | Adjust `spanning-tree cost <value>`   |
| STP Mode Mismatch    | Inconsistent convergence      | Align `spanning-tree mode <mode>`     |
| BPDU Not Received    | No root bridge communication  | Check connectivity and timers         |

Scenario: An admin notices network instability. `show spanning-tree` reveals frequent topology changes due to a flapping link. Disabling the unstable port stabilizes the topology.

---

## STP Variants

STP has evolved to address convergence speed and scalability:
- **STP (802.1D)**: Original protocol, slow convergence (30–50 seconds).
- **RSTP (802.1w)**: Faster convergence (seconds), backward-compatible, uses all switches for BPDUs, and has three port states (Discarding, Learning, Forwarding).
- **PVST**: Cisco’s per-VLAN STP, separate instance per VLAN, resource-intensive.
- **RPVST**: Combines PVST with RSTP’s fast convergence.
- **MSTP (802.1s)**: Maps multiple VLANs to a single STP instance, ideal for large networks.

**STP vs. RSTP**:
| Feature              | STP (802.1D)                  | RSTP (802.1w)                |
|----------------------|-------------------------------|------------------------------|
| Standard             | 802.1D                        | 802.1w                       |
| BPDU Source          | Root bridge only              | All switches                 |
| Port Roles           | Root, Designated, Blocked     | Root, Designated, Alternate, Backup |
| Port States          | 5 (Disabled, Blocking, Listening, Learning, Forwarding) | 3 (Discarding, Learning, Forwarding) |
| Convergence          | 30–50 seconds                 | Seconds                      |
| Link Types           | None                          | Point-to-Point, Shared       |

Scenario: A large enterprise switches from PVST to MSTP to reduce CPU load by grouping VLANs into fewer STP instances, improving scalability.