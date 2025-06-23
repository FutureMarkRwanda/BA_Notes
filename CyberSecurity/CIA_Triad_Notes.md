# Security Goals (CIA Triad)

## Summary

This topic covers the CIA Triad, the foundational framework for cybersecurity, consisting of Confidentiality, Integrity, and Availability. It outlines how these principles protect systems, networks, and data from unauthorized access, tampering, and disruptions.

* **Confidentiality**: Ensuring data is accessible only to authorized parties.
* **Integrity**: Maintaining data accuracy and trustworthiness.
* **Availability**: Guaranteeing resources are accessible when needed.

---

## Confidentiality

Confidentiality protects sensitive information from unauthorized access, ensuring privacy for personal, financial, or proprietary data. It restricts access to authorized users through various controls and techniques.

**Key Mechanisms**:
- **Access Control**: Restricts data access using authentication (e.g., passwords, biometrics, multi-factor authentication).
- **Encryption**: Converts data into unreadable ciphertext (e.g., AES-256 for secure transmission).
- **Data Masking**: Obscures sensitive data (e.g., showing only XXXX-XXXX-XXXX-1234 for credit cards).
- **Least Privilege Principle**: Grants minimal access needed for tasks (e.g., employees access only relevant databases).
- **Network Segmentation**: Isolates sensitive data in separate network zones (e.g., DMZ for public-facing servers).

**Examples**:
- A hospital encrypts patient records to prevent unauthorized access.
- A bank uses multi-factor authentication (MFA) to secure online accounts.
- Violation: A hacker intercepts unencrypted emails (eavesdropping) or an employee leaks customer data (insider threat).

Scenario: A company implements encryption and MFA to protect client financial data, preventing breaches during data transmission.

---

## Integrity

Integrity ensures data remains accurate, consistent, and unaltered by unauthorized parties. It verifies that information is trustworthy during storage, transmission, or processing.

**Key Mechanisms**:
- **Hashing**: Generates unique hash values to detect changes (e.g., SHA-256 for file verification).
- **Checksums/Message Digests**: Validates data integrity (e.g., MD5 for software downloads).
- **Digital Signatures**: Ensures data authenticity and integrity using public/private keys.
- **Access Controls**: Limits who can modify data (e.g., write permissions for authorized users only).
- **Version Control**: Tracks changes to revert unauthorized modifications (e.g., Git for code).

**Examples**:
- A bank uses digital signatures to verify transaction integrity.
- A website checks file hashes to ensure downloads are untampered.
- Violation: A man-in-the-middle (MitM) attack alters payment details, or malware corrupts database records.

Scenario: An e-commerce platform uses hashing to verify product listings, preventing unauthorized price changes.

---

## Availability

Availability ensures systems, applications, and data are accessible to authorized users when needed, minimizing downtime and disruptions.

**Key Mechanisms**:
- **System Uptime**: Maintains operational servers (e.g., 99.99% uptime SLAs).
- **Redundancy**: Deploys backup systems (e.g., RAID for storage, failover servers).
- **Disaster Recovery**: Restores operations post-incident (e.g., backups for ransomware recovery).
- **Load Balancing**: Distributes traffic to prevent overload (e.g., AWS Elastic Load Balancer).
- **DDoS Protection**: Mitigates traffic floods (e.g., Cloudflare for web servers).

**Examples**:
- A cloud provider uses redundant servers to ensure constant access.
- A retailer implements backups to recover from ransomware.
- Threats: Denial of Service (DoS) attacks overwhelm servers, or hardware failures cause outages.

Scenario: A university uses load balancing and backups to keep its e-learning platform accessible during peak usage.