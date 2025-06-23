# Security Services

## Summary

This topic explores security services that protect systems and data, including Authentication, Authorization, Accounting, and Non-repudiation. These services ensure user identity verification, access control, activity tracking, and undeniable proof of actions.

* **Authentication**: Verifying user or system identity.
* **Authorization**: Determining access permissions.
* **Accounting**: Tracking user activities.
* **Non-repudiation**: Ensuring actions cannot be denied.

---

## Authentication

Authentication verifies the identity of users, devices, or systems to ensure they are legitimate before granting access.

**Methods**:
- **Something You Know**: Passwords, PINs.
- **Something You Have**: Smart cards, tokens.
- **Something You Are**: Biometrics (e.g., fingerprints, facial recognition).

**Examples**:
- A user logs into a banking app with a password and SMS code (MFA).
- A company uses fingerprint scanners for employee access.
- Tools: Kerberos, OAuth, SAML.

Scenario: An organization implements MFA with passwords and biometrics to secure remote access to its VPN.

---

## Authorization

Authorization determines what authenticated users or systems can access or perform, based on predefined permissions.

**Mechanisms**:
- **Role-Based Access Control (RBAC)**: Permissions by role (e.g., admin vs. user).
- **Attribute-Based Access Control (ABAC)**: Permissions by attributes (e.g., location, time).
- **Access Control Lists (ACLs)**: Specific permissions per user/group (e.g., read/write).

**Examples**:
- An HR manager accesses employee records but not financial data (RBAC).
- A contractor accesses systems only during work hours (ABAC).
- Tools: Active Directory, AWS IAM.

Scenario: A university restricts student access to grades but allows faculty full access using RBAC.

---

## Accounting

Accounting tracks user actions via logging and auditing, providing records for security monitoring and compliance.

**Key Aspects**:
- Logs events like logins, file access, and configuration changes.
- Enables forensic analysis and compliance audits (e.g., GDPR, HIPAA).

**Examples**:
- A server logs all SSH login attempts for review.
- A company audits database access to detect unauthorized queries.
- Tools: Splunk, ELK Stack, Syslog.

Scenario: A bank logs all transactions to trace suspicious activities, ensuring compliance with regulations.

---

## Non-repudiation

Non-repudiation ensures users or systems cannot deny their actions, providing proof of data origin and integrity.

**Mechanisms**:
- **Digital Signatures**: Verify sender and data integrity using public/private keys.
- **Timestamping**: Records action timing (e.g., document signing).
- **Hashing**: Ensures data hasn’t been altered (e.g., SHA-256).

**Examples**:
- A contract is digitally signed to prove agreement.
- An email with a timestamp confirms sending time.
- Tools: PGP, DocuSign, OpenSSL.

Scenario: A law firm uses digital signatures to ensure clients cannot deny signing contracts.