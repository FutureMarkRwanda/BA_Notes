# Implementing Router Security

## Summary

This topic covers securing Cisco routers to protect against unauthorized access and network threats. It includes:

* **Router Access Security**: Configuring console, auxiliary, VTY, SSH, and password protections.
* **Login Security and Monitoring**: Implementing login restrictions and logging for attack detection.
* **Standard Ports and Protocols**: Understanding key ports for secure network services.
* **Verification and Troubleshooting**: Checking configurations and resolving security issues.

---

## Router Access Security

Securing router access prevents unauthorized management and ensures only trusted users can configure or monitor the device. Key measures include setting passwords for console, auxiliary, and VTY ports, enabling SSH for secure remote access, encrypting passwords, configuring banners, and setting timeouts.

**Key Configurations**:
- **Console Port**: Protects physical access to the router.
- **Auxiliary (AUX) Port**: Secures modem or secondary access (less common today).
- **VTY Ports**: Controls Telnet/SSH access (0–4 or 0–15 depending on platform).
- **Privileged Mode**: Restricts access to configuration mode with `enable secret`.
- **Password Encryption**: Uses `service password-encryption` (weak, type 7) or `secret` (strong, MD5).
- **SSH**: Replaces insecure Telnet with encrypted remote access.
- **MOTD Banner**: Warns unauthorized users.
- **Exec Timeout**: Logs out inactive sessions.
- **Local User Database**: Uses usernames/passwords for authentication.

**Example Configuration**:
```
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)# security passwords min-length 9
R1(config)# enable secret Cisco12345
R1(config)# line console 0
R1(config-line)# password cisco12345
R1(config-line)# login
R1(config-line)# exec-timeout 5 0
R1(config-line)# exit
R1(config)# line aux 0
R1(config-line)# password cisco12345
R1(config-line)# login
R1(config-line)# exec-timeout 5 0
R1(config-line)# exit
R1(config)# line vty 0 4
R1(config-line)# password cisco12345
R1(config-line)# login
R1(config-line)# transport input telnet
R1(config-line)# exec-timeout 5 0
R1(config-line)# exit
R1(config)# service password-encryption
R1(config)# banner motd $Only Authorized Users Are Allowed!$
R1(config)# username admin privilege 15 secret Admin@123
R1(config)# ip domain-name rca.rw
R1(config)# crypto key generate rsa general-keys modulus 1024
R1(config)# ip ssh version 2
R1(config)# line vty 0 4
R1(config-line)# login local
R1(config-line)# transport input ssh
R1(config-line)# exit
R1# copy running-config startup-config
```

**Notes**:
- `secret` is preferred over `password` for stronger MD5 encryption.
- SSH requires a hostname, domain name, RSA keys, and `login local` for username-based authentication.
- `exec-timeout 5 0` sets a 5-minute idle timeout; `0 0` disables it.

Scenario: A corporate network secures a router with SSH access, encrypted passwords, and a MOTD banner to deter unauthorized access while allowing admin management.

---

## Login Security and Monitoring

Preventing and detecting login attacks enhances router security. Measures include blocking repeated failed login attempts, logging successful and failed logins, and restricting access to specific protocols or users.

**Key Features**:
- **Login Block**: Temporarily blocks logins after multiple failed attempts.
- **Logging**: Tracks login successes and failures for auditing.
- **Access Restrictions**: Limits protocols (e.g., SSH only) or source IPs (via ACLs).

**Example Configuration**:
```
R1> enable
R1# configure terminal
R1(config)# login block-for 180 attempts 5 within 120
R1(config)# login on-success log
R1(config)# login on-failure log every 2
R1(config)# ip access-list standard SSH-ACCESS
R1(config-std-nacl)# permit 192.168.10.100
R1(config-std-nacl)# permit 192.168.10.101
R1(config-std-nacl)# exit
R1(config)# line vty 0 4
R1(config-line)# access-class SSH-ACCESS in
R1(config-line)# exit
R1# copy running-config startup-config
```

**Notes**:
- `login block-for 180 attempts 5 within 120`: Blocks logins for 180 seconds after 5 failed attempts in 120 seconds.
- `login on-failure log every 2`: Logs every second failed attempt.
- ACL `SSH-ACCESS` restricts SSH to specific IPs, enhancing security.

Scenario: A university router logs login attempts and blocks access after 5 failed tries in 2 minutes, notifying admins of potential brute-force attacks via logs.

---

## Standard Ports and Protocols

Understanding key ports and protocols is essential for configuring secure router services and ACLs. Common ports include:

| Port | Protocol | Description                     |
|------|----------|---------------------------------|
| 20/21| FTP      | File Transfer Protocol (TCP)    |
| 22   | SSH      | Secure Shell (TCP)              |
| 23   | Telnet   | Insecure remote access (TCP)    |
| 25   | SMTP     | Simple Mail Transfer (TCP)      |
| 53   | DNS      | Domain Name System (UDP)        |
| 80   | HTTP     | Web traffic (TCP)               |
| 123  | NTP      | Network Time Protocol (UDP)     |
| 143  | IMAP     | Email management (TCP)          |
| 179  | BGP      | Border Gateway Protocol (TCP)   |
| 443  | HTTPS    | Secure web traffic (TCP)        |
| 500  | ISAKMP   | IPsec key management (UDP)      |
| 587  | SMTP     | Secure email (TCP)              |
| 3389 | RDP      | Remote Desktop Protocol (TCP)   |

**Use Case**: When configuring ACLs, specify ports (e.g., `eq 80` for HTTP) to allow/deny specific services while securing the router.

Scenario: An admin configures an ACL to permit HTTPS (port 443) traffic to a server while denying Telnet (port 23) to the router, ensuring secure access.

---

## Verification and Troubleshooting

Verifying router security confirms configurations for access, encryption, and login protections. Troubleshooting resolves issues like failed logins or SSH connectivity problems.

**Verification Commands**:
- `show running-config | section line`: Displays console, AUX, and VTY configurations.
- `show running-config | include password`: Shows password settings.
- `show ip ssh`: Verifies SSH configuration.
- `show login`: Checks login block settings and attempt history.
- `show access-lists`: Confirms ACLs for access restrictions.
- `show users`: Lists active sessions.
- `show logging`: Displays login success/failure logs.

Example output for `show ip ssh` on R1:
```
SSH Enabled - version 2.0
Authentication timeout: 120 secs; Authentication retries: 3
Minimum expected Diffie Hellman key size : 1024 bits
```

**Troubleshooting Common Issues**:
- **Console/VTY Login Failure**: Incorrect password or `login` setting. Verify with `show running-config | section line` and correct with `password` or `login local`.
- **SSH Connection Refused**: Missing RSA keys, domain name, or SSH version. Check with `show ip ssh` and configure with `ip domain-name`, `crypto key generate rsa`, and `ip ssh version 2`.
- **Login Block Triggered**: Legitimate user blocked after failed attempts. Verify with `show login` and clear with `clear login blocked`.
- **Weak Encryption Used**: Type 7 passwords in config. Replace `password` with `secret` for MD5 encryption and verify with `show running-config | include password`.
- **Telnet Enabled**: Insecure access allowed. Confirm with `show running-config | section vty` and set `transport input ssh` to disable Telnet.
- **No Logging**: Missing login attack logs. Check with `show logging` and enable with `login on-failure log`.

Example troubleshooting scenario: SSH access to R1 fails. `show ip ssh` shows no RSA keys. Generating keys with `crypto key generate rsa general-keys modulus 1024` resolves the issue.

| Issue                | Symptom                        | Solution                              |
|----------------------|--------------------------------|---------------------------------------|
| Login Failure        | Cannot access console/VTY     | Correct `password` or `login local`   |
| SSH Refused          | SSH connection fails          | Set `ip domain-name`, generate RSA keys|
| Login Block Triggered| User blocked after attempts   | Clear with `clear login blocked`      |
| Weak Encryption      | Type 7 passwords in config    | Use `secret` for MD5 encryption       |

Scenario: An admin cannot access R1 via SSH. `show running-config | section vty` shows `transport input telnet`. Setting `transport input ssh` and `login local` enables secure SSH access.