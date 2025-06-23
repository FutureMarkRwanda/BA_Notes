# Ethical Hacking Concepts

## Summary

This topic covers ethical hacking, the practice of legally testing systems to identify vulnerabilities. It includes terminologies, compliance requirements, hacking phases, and hacker classifications.

* **Terminologies**: Key concepts like penetration testing, vulnerabilities, and exploits.
* **Compliances**: Legal and ethical guidelines for hacking.
* **Phases**: Structured process of ethical hacking.
* **Hacker Classifications**: Types of hackers by intent and actions.

---

## Ethical Hacking Terminologies

Ethical hacking involves legally penetrating systems to find and fix vulnerabilities before malicious exploitation.

**Key Terms**:
- **Penetration Testing (Pen Testing)**: Simulating attacks to identify weaknesses.
- **Footprinting**: Gathering target information (e.g., IP addresses, employee data).
- **Vulnerability**: System flaw exploitable by attackers.
- **Exploit**: Code or method to leverage vulnerabilities.
- **Payload**: Malicious action post-exploit (e.g., ransomware installation).

**Examples**:
- Pen testing reveals SQL injection flaws in a web app.
- Footprinting uses Whois to find domain details.
- Tools: Metasploit (exploits), Nmap (scanning).

Scenario: A company hires a pen tester to footprint its network and exploit vulnerabilities, improving defenses.

---

## Ethical Hacking Compliances

Ethical hacking requires adherence to legal and ethical standards to ensure responsible practices.

**Key Aspects**:
- **Permission-Based**: Explicit consent from system owners required.
- **Goal-Oriented**: Focus on identifying and mitigating vulnerabilities.
- **Methodology**: Follows standards like PTES or OWASP.
- **Reporting**: Provides detailed vulnerability reports with remediation advice.

**Examples**:
- A signed contract authorizes a pen test for a bank’s systems.
- A report details XSS vulnerabilities with fixes.
- Standards: PTES, OWASP Top Ten, NIST SP 800-115.

Scenario: An ethical hacker obtains permission to test a retailer’s e-commerce site, reporting findings per OWASP guidelines.

---

## Ethical Hacking Phases

Ethical hacking follows a structured process to simulate cyberattacks and identify vulnerabilities.

**Phases**:
1. **Reconnaissance**: Gather target info.
   - Passive: Public data (e.g., Whois, Google Dorks).
   - Active: Direct interaction (e.g., port scanning).
   - Tools: Maltego, Recon-ng, Shodan.
2. **Scanning/Enumeration**: Detect live hosts, ports, and services.
   - Types: Port, network, vulnerability, application, wireless scanning.
   - Tools: Nmap, Nessus, OWASP ZAP, Wireshark.
3. **Gaining Access**: Exploit vulnerabilities to access systems.
   - Techniques: SQL injection, password cracking, social engineering.
   - Tools: Metasploit, SQLMap, Hydra.
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

Scenario: An ethical hacker scans a university’s network, exploits a weak password, and recommends MFA implementation.

---

## Hacker Classifications

Hackers are classified by intent, skills, and legality, impacting their actions and motivations.

**Types**:
- **White Hat (Ethical)**: Improve security legally (e.g., pen testers).
- **Black Hat**: Malicious, illegal activities (e.g., data theft).
- **Gray Hat**: Mixed intent, often unauthorized but non-malicious.
- **Red Hat**: Vigilante hackers targeting threats illegally.
- **Script Kiddies**: Inexperienced, using pre-made tools.
- **Hacktivists**: Ideological attacks (e.g., Anonymous).
- **Cybercriminals**: Financial gain via crimes (e.g., ransomware).
- **State-Sponsored**: Government-backed espionage.
- **Insider Threats**: Malicious internal actors.

**Examples**:
- A white hat tests a bank’s defenses with Nmap.
- A black hat deploys ransomware like WannaCry.
- A hacktivist defaces a government site for protest.

Scenario: A company faces a gray hat exposing a flaw without permission, prompting a white hat hire to secure systems.