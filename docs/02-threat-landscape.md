# Threat Landscape

This document identifies the primary threats relevant to our context and maps them to detection capabilities and controls.

---

## Context

This threat model assumes a B2B SaaS company with:

- Cloud-native infrastructure (AWS/GCP/Azure)
- Customer data including PII and business-sensitive information
- Engineering-driven culture with CI/CD deployment
- 50-500 employees, Series B to post-IPO stage
- SOC 2 and/or ISO 27001 compliance requirements

Adjust threat priorities based on your actual context.

---

## Top 10 Threats

### 1. Compromised Developer Credentials

**Description:** Attacker obtains valid credentials for a developer account through phishing, credential stuffing, or malware.

| Attribute | Assessment |
|-----------|------------|
| Likelihood | High |
| Impact | Critical |
| Attack Vector | Phishing, credential reuse, infostealer malware |
| Business Impact | Code tampering, data exfiltration, supply chain compromise |

**Detection Signals:**
- Login from unusual location or device
- Access outside normal working hours
- Unusual repository access patterns
- MFA bypass attempts

**Key Controls:**
- Mandatory MFA on all developer accounts
- Hardware security keys for privileged access
- Session monitoring and anomaly detection
- Regular access reviews

---

### 2. Supply Chain Attack

**Description:** Malicious code introduced through a dependency, build tool, or third-party integration.

| Attribute | Assessment |
|-----------|------------|
| Likelihood | Medium |
| Impact | Critical |
| Attack Vector | Compromised package, typosquatting, CI/CD poisoning |
| Business Impact | Malware distribution to customers, data theft, reputation damage |

**Detection Signals:**
- New or updated dependencies with suspicious characteristics
- Build process anomalies
- Unexpected network connections from build systems

**Key Controls:**
- Dependency scanning (SCA) in CI/CD
- Lock files and hash verification
- Private artifact registry
- Build system isolation and monitoring

---

### 3. Insider Threat

**Description:** Malicious or negligent actions by employees, contractors, or partners with legitimate access.

| Attribute | Assessment |
|-----------|------------|
| Likelihood | Medium |
| Impact | High |
| Attack Vector | Data exfiltration, sabotage, policy violations |
| Business Impact | Data breach, IP theft, operational disruption |

**Detection Signals:**
- Bulk data downloads
- Access to resources outside job function
- Activity during notice period
- Attempts to bypass DLP controls

**Key Controls:**
- Least privilege access
- Data Loss Prevention (DLP)
- User behavior analytics
- Offboarding procedures with immediate access revocation

---

### 4. Cloud Misconfiguration

**Description:** Security settings in cloud infrastructure left in insecure states, exposing data or systems.

| Attribute | Assessment |
|-----------|------------|
| Likelihood | High |
| Impact | High |
| Attack Vector | Public S3 buckets, overly permissive IAM, exposed databases |
| Business Impact | Data exposure, compliance violations, unauthorized access |

**Detection Signals:**
- Cloud security posture alerts
- Public exposure of resources
- IAM policy changes
- Configuration drift from baselines

**Key Controls:**
- Cloud Security Posture Management (CSPM)
- Infrastructure as Code with security scanning
- Automated remediation for critical misconfigs
- Regular configuration audits

---

### 5. Ransomware

**Description:** Malware that encrypts systems and data, demanding payment for decryption.

| Attribute | Assessment |
|-----------|------------|
| Likelihood | Medium |
| Impact | Critical |
| Attack Vector | Phishing, RDP exposure, vulnerability exploitation |
| Business Impact | Operational shutdown, data loss, extortion costs |

**Detection Signals:**
- Mass file encryption activity
- Unusual process execution
- Network scanning from internal hosts
- Backup deletion attempts

**Key Controls:**
- Endpoint Detection and Response (EDR)
- Immutable backups with tested restoration
- Network segmentation
- Email security and phishing protection

---

### 6. API Abuse

**Description:** Exploitation of API vulnerabilities or misuse of legitimate API access.

| Attribute | Assessment |
|-----------|------------|
| Likelihood | High |
| Impact | Medium-High |
| Attack Vector | BOLA, injection, broken authentication, rate limit bypass |
| Business Impact | Data theft, service abuse, resource exhaustion |

**Detection Signals:**
- Unusual API call patterns
- Authentication failures
- Parameter tampering attempts
- Rate limit violations

**Key Controls:**
- API gateway with rate limiting
- Input validation and output encoding
- Authentication and authorization checks
- API-specific WAF rules

---

### 7. Business Email Compromise (BEC)

**Description:** Attacker impersonates executives or vendors to trick employees into transferring funds or data.

| Attribute | Assessment |
|-----------|------------|
| Likelihood | High |
| Impact | Medium-High |
| Attack Vector | Email spoofing, account takeover, domain impersonation |
| Business Impact | Financial loss, data disclosure, reputation damage |

**Detection Signals:**
- Emails from lookalike domains
- Unusual payment or data requests
- Executive impersonation patterns

**Key Controls:**
- DMARC/DKIM/SPF enforcement
- Email security gateway
- Security awareness training
- Out-of-band verification for sensitive requests

---

### 8. Third-Party Breach

**Description:** Security incident at a vendor, partner, or service provider that affects our data or operations.

| Attribute | Assessment |
|-----------|------------|
| Likelihood | Medium |
| Impact | Medium-High |
| Attack Vector | Vendor compromise, shared infrastructure breach |
| Business Impact | Data exposure, service disruption, compliance violations |

**Detection Signals:**
- Vendor security notifications
- Unusual activity from third-party integrations
- Public breach disclosures

**Key Controls:**
- Vendor security assessments
- Data minimization with third parties
- Contractual security requirements
- Third-party access monitoring

---

### 9. Vulnerability Exploitation

**Description:** Attacker exploits known or zero-day vulnerabilities in applications or infrastructure.

| Attribute | Assessment |
|-----------|------------|
| Likelihood | Medium |
| Impact | High |
| Attack Vector | Unpatched systems, zero-days, public exploits |
| Business Impact | System compromise, data theft, lateral movement |

**Detection Signals:**
- Exploitation attempt patterns in logs
- Unexpected system behavior
- Network anomalies

**Key Controls:**
- Vulnerability scanning and management
- Patch management with SLAs
- Virtual patching via WAF
- Bug bounty program

---

### 10. Data Exfiltration

**Description:** Unauthorized extraction of sensitive data from the organization.

| Attribute | Assessment |
|-----------|------------|
| Likelihood | Medium |
| Impact | High |
| Attack Vector | Compromised accounts, insider threat, malware |
| Business Impact | Regulatory fines, customer trust loss, competitive harm |

**Detection Signals:**
- Large data transfers
- Uploads to unauthorized destinations
- Database query anomalies
- Email attachments with sensitive content

**Key Controls:**
- Data Loss Prevention (DLP)
- Network monitoring and egress controls
- Database activity monitoring
- Data classification and access controls

---

## Threat Matrix Summary

| Threat | Likelihood | Impact | Risk Score | Priority |
|--------|------------|--------|------------|----------|
| Compromised Developer Credentials | High | Critical | 20 | P1 |
| Cloud Misconfiguration | High | High | 16 | P1 |
| API Abuse | High | Medium-High | 12 | P2 |
| Business Email Compromise | High | Medium-High | 12 | P2 |
| Supply Chain Attack | Medium | Critical | 15 | P1 |
| Ransomware | Medium | Critical | 15 | P1 |
| Insider Threat | Medium | High | 12 | P2 |
| Vulnerability Exploitation | Medium | High | 12 | P2 |
| Third-Party Breach | Medium | Medium-High | 9 | P2 |
| Data Exfiltration | Medium | High | 12 | P2 |

---

## Annual Review

This threat landscape should be reviewed:

- Annually as part of risk assessment cycle
- After any significant security incident
- When business context changes (new products, markets, regulations)
- When emerging threats warrant re-evaluation
