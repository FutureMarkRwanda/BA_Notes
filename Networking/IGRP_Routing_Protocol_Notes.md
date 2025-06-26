# Configuring the IGRP Routing Protocol

## Summary

This topic covers the Interior Gateway Routing Protocol (IGRP), a Cisco-proprietary distance-vector protocol used in older networks. It includes:

* **IGRP Operations**: Understanding IGRP’s characteristics and composite metric.
* **IGRP Configuration and Verification**: Setting up IGRP on Cisco routers and checking its functionality.
* **IGRP Troubleshooting**: Resolving common issues in IGRP deployments.

---

## IGRP Operations

IGRP (Interior Gateway Routing Protocol) is a Cisco-proprietary distance-vector protocol designed for routing within an autonomous system (AS). It uses a composite metric based on bandwidth, delay, reliability, load, and MTU, making it more sophisticated than RIP’s hop-count metric. IGRP sends updates every 90 seconds, with a hold-down timer of 280 seconds to stabilize routing after changes. Triggered updates accelerate convergence when network topology changes occur. Routers must share the same AS number to exchange routing information. IGRP supports up to 255 hops (default 100, often reduced to 50 or less) and has an administrative distance of 100.

The composite metric is calculated as:
```
Metric = [K1 * Bandwidth + (K2 * Bandwidth)/(256 - Load) + K3 * Delay] * [K5 / (Reliability + K4)]
```
Default constants: K1 = K3 = 1, K2 = K4 = K5 = 0, simplifying to `Metric = Bandwidth + Delay`. Note that IGRP is obsolete in modern Cisco equipment, replaced by EIGRP.

Key characteristics:
- Distance-vector protocol.
- Uses bandwidth, delay, reliability, load, and MTU for metrics.
- Updates every 90 seconds, hold-down 280 seconds.
- Maximum 255 hops, default 100.
- Administrative distance: 100.
- Requires same AS number for routers to share routes.

Example scenario: A legacy network uses IGRP to route between two LANs, prioritizing paths with higher bandwidth and lower delay for efficient data transfer.

---

## IGRP Configuration and Verification

Configuring IGRP involves enabling the protocol, specifying an AS number, and advertising connected networks. Verification ensures routes are correctly learned and advertised.

**Configuration Example** for two routers (R1 and R2) connecting LAN 1 (192.168.1.0/24), LAN 2 (192.168.2.0/24), and a link (10.10.0.0/30):
```bash
! On R1
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# interface g0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface g0/1
R1(config-if)# ip address 10.10.0.1 255.255.255.252
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# router igrp 100
R1(config-router)# network 192.168.1.0
R1(config-router)# network 10.10.0.0
R1(config-router)# exit
R1# copy running-config startup-config

! On R2
R2> enable
R2# configure terminal
R2(config)# hostname R2
R2(config)# interface g0/0
R2(config-if)# ip address 192.168.2.1 255.255.255.0
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# interface g0/1
R2(config-if)# ip address 10.10.0.2 255.255.255.252
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# router igrp 100
R2(config-router)# network 192.168.2.0
R2(config-router)# network 10.10.0.0
R2(config-router)# exit
R2# copy running-config startup-config
```

**Verification Commands**:
- `show ip route`: Displays IGRP routes (marked with “I”).
- `show ip protocols`: Shows IGRP configuration details (e.g., AS number, networks, timers).

Example output for `show ip route` on R1:
```
I 192.168.2.0/24 [100/8576] via 10.10.0.2, 00:01:30, GigabitEthernet0/1
```

A small business with legacy Cisco routers configures IGRP with AS 100 to connect two office LANs, ensuring routes are dynamically shared based on bandwidth and delay metrics._

---

## IGRP Troubleshooting

Troubleshooting IGRP focuses on resolving issues that prevent route advertisement or learning, often related to configuration errors or network issues.

Common issues and solutions:
- **Mismatched AS Numbers**: Routers must use the same AS number to exchange routes. Verify with `show ip protocols` and correct with `router igrp <AS>`.
- **Wrong Network Commands**: Missing or incorrect `network` statements prevent route advertisement. Check `show running-config` and ensure all relevant networks are included.
- **Interface Shutdown**: A shut interface stops route advertisements. Use `show ip interface brief` to confirm interfaces are up and issue `no shutdown` if needed.
- **Passive Interface**: If configured, a passive interface suppresses updates. Verify with `show ip protocols` and remove with `no passive-interface <interface>`.
- **Metric Issues**: Incorrect K-values or unreachable routes (metric too high) can disrupt routing. Reset to default K-values with `metric weights 0 1 0 1 0 0`.
- **Timers Mismatch**: Inconsistent update or hold-down timers between routers can cause instability. Align timers using `timers basic <update> <invalid> <holddown> <flush>`.

Example troubleshooting scenario: R1 does not see 192.168.2.0/24 in its routing table. The admin runs `show ip protocols` and finds R1 uses AS 100, but R2 uses AS 200. Reconfiguring R2 with `router igrp 100` resolves the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Mismatched AS        | No routes exchanged           | Set same AS with `router igrp <AS>`  |
| Wrong Network        | Missing routes                | Correct `network` statements          |
| Interface Shutdown   | No updates sent               | Use `no shutdown` on interface        |
| Passive Interface    | Updates suppressed            | Remove with `no passive-interface`    |

An admin notices R2’s routes are missing on R1. Using `show ip interface brief`, they find R2’s g0/1 interface is down. Issuing `no shutdown` restores route advertisements.