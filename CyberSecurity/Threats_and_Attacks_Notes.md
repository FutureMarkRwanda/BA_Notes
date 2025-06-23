# Threats and Attacks

## Summary

This topic covers cyber threats and attacks, potential dangers that exploit vulnerabilities to harm systems or data. It includes types of attacks and prioritization based on impact and likelihood.

* **Types of Threats and Attacks**: Categories like malware, phishing, and DoS.
* **Prioritization**: Ranking threats by impact and exploitability.

---

## Types of Threats and Attacks

Threats are potential risks, while attacks are deliberate attempts to exploit vulnerabilities, compromising confidentiality, integrity, or availability.

**Attack Types**:
1. **Malware**:
   - Virus: Attaches to files, spreads on execution (e.g., macro viruses).
   - Worm: Self-replicates over networks (e.g., Conficker).
   - Trojan: Disguises as legitimate software (e.g., fake antivirus).
   - Ransomware: Encrypts data, demands payment (e.g., WannaCry).
   - Spyware: Monitors user activity (e.g., keyloggers).
   - Adware: Displays unwanted ads.
   - Rootkit: Hides malicious activities (e.g., kernel-level rootkits).
   - Botnet: Compromised device network (e.g., Mirai).
   - Fileless Malware: Memory-based, no disk traces.
   - Cryptojacker: Mines cryptocurrency illicitly.
2. **Phishing**: Tricks users into revealing sensitive data.
   - Email Phishing: Fraudulent emails.
   - Spear Phishing: Targeted attacks.
3. **Cross-Site Scripting (XSS)**: Injects malicious scripts into web pages.
   - Stored/Reflected XSS: Server or browser-based attacks.
4. **Man-in-the-Middle (MitM)**: Intercepts communication (e.g., session hijacking).
5. **SQL Injection**: Executes unauthorized database queries.
6. **Denial of Service (DoS)**: Overwhelms systems (e.g., DDoS via botnets).
7. **Brute Force**: Tries all password combinations (e.g., password cracking).
8. **Social Engineering**: Manipulates users (e.g., pretexting, baiting).
9. **Zero-Day**: Exploits unpatched flaws.
10. **Insider Attacks**: Malicious internal actions (e.g., data theft).
11. **Rootkits**: Hides malware for persistent access.

**Examples**:
- WannaCry ransomware encrypts hospital data.
- A phishing email steals employee credentials.
- Tools: Metasploit (exploits), LOIC (DDoS).

Scenario: A retailer faces a DDoS attack and phishing attempts, deploying firewalls and user training to mitigate risks.

---

## Prioritization of Threats and Attacks

Prioritizing threats involves assessing their impact, likelihood, exploitability, and business criticality to focus mitigation efforts.

**Based on Impact**:
- **High**: Severe consequences (e.g., ransomware locking critical systems, insider data theft, zero-day exploits).
- **Medium**: Moderate damage (e.g., phishing stealing credentials, DoS causing temporary outages).
- **Low**: Minimal impact (e.g., adware, minor misconfigurations).

**Examples**:
- High: A zero-day exploit in a financial system is patched immediately.
- Medium: A phishing campaign prompts user awareness training.
- Low: Adware is removed with antivirus scans.
- Tools: Risk matrices, NIST SP 800-30.

Scenario: A company prioritizes ransomware over adware, allocating resources to backups and endpoint protection.