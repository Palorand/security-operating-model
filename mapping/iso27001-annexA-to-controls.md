# ISO 27001:2022 Annex A Control Mapping

This document maps ISO 27001:2022 Annex A controls to our specific implementations, evidence sources, and ownership.

---

## How to Use This Document

For each control:
- **Applicability**: Whether the control applies to our context
- **Implementation**: How we satisfy the control requirement
- **Evidence**: Where to find proof of implementation
- **Owner**: Who is responsible for maintaining the control
- **Automation**: Level of automation (Automated / Semi-automated / Manual)

---

## 5. Organizational Controls

### 5.1 Policies for Information Security

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Security policies documented in internal wiki, reviewed annually, approved by Security Lead |
| Evidence | Policy documents with version history, approval records |
| Owner | Security Lead |
| Automation | Manual (annual review cycle) |

### 5.2 Information Security Roles and Responsibilities

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | RACI matrix defined in operating model, job descriptions include security responsibilities |
| Evidence | [07-operating-model-and-raci.md](../docs/07-operating-model-and-raci.md), HR job descriptions |
| Owner | Security Lead / HR |
| Automation | Manual |

### 5.3 Segregation of Duties

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Separate roles for development, deployment, and production access; approval workflows for sensitive actions |
| Evidence | IAM role definitions, deployment pipeline configuration, approval logs |
| Owner | Platform Engineering |
| Automation | Automated (enforced by IAM and CI/CD) |

### 5.4 Management Responsibilities

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Leadership endorsement of security program, quarterly security reviews with executives |
| Evidence | Meeting minutes, security report distribution lists |
| Owner | Security Lead |
| Automation | Manual |

### 5.5 Contact with Authorities

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Incident response plan includes authority notification procedures, legal maintains regulatory contacts |
| Evidence | [10-incident-operating-loop.md](../docs/10-incident-operating-loop.md), legal contact registry |
| Owner | Legal / Security Lead |
| Automation | Manual |

### 5.6 Contact with Special Interest Groups

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Security team participates in ISACs, follows threat intelligence feeds, attends industry conferences |
| Evidence | Membership records, threat intel feed subscriptions |
| Owner | Security Engineering |
| Automation | Manual |

### 5.7 Threat Intelligence

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Threat intel feeds integrated into SIEM, regular threat landscape reviews, documented in [02-threat-landscape.md](../docs/02-threat-landscape.md) |
| Evidence | SIEM threat feed configuration, threat landscape document |
| Owner | Security Engineering |
| Automation | Semi-automated (feeds automated, analysis manual) |

### 5.8 Information Security in Project Management

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Security review process for new projects, security requirements in project templates |
| Evidence | [09-security-review-process.md](../docs/09-security-review-process.md), review records |
| Owner | Security Lead |
| Automation | Semi-automated (tracking automated, reviews manual) |

### 5.9 Inventory of Information and Other Associated Assets

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Asset inventory maintained via cloud resource tagging, CMDB for infrastructure, data catalog for data assets |
| Evidence | Cloud console asset lists, CMDB exports, data catalog |
| Owner | Platform Engineering / Data Engineering |
| Automation | Automated (cloud discovery) |

### 5.10 Acceptable Use of Information and Other Associated Assets

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Acceptable use policy, device management policy, acknowledged during onboarding |
| Evidence | Policy documents, signed acknowledgments in HR system |
| Owner | IT / HR |
| Automation | Semi-automated (acknowledgment tracking) |

### 5.11 Return of Assets

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Offboarding checklist includes asset return, MDM for remote wipe capability |
| Evidence | Offboarding records, MDM logs |
| Owner | IT / HR |
| Automation | Semi-automated |

### 5.12 Classification of Information

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Data classification scheme (Public, Internal, Confidential, Restricted), classification guidance documented |
| Evidence | Data classification policy, data catalog classifications |
| Owner | GRC |
| Automation | Semi-automated (some automated classification) |

### 5.13 Labelling of Information

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Document templates include classification labels, email classification options |
| Evidence | Document templates, email system configuration |
| Owner | IT |
| Automation | Semi-automated |

### 5.14 Information Transfer

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | TLS required for all transfers, approved file sharing tools, DLP monitoring |
| Evidence | TLS configuration, approved tools list, DLP reports |
| Owner | IT / Security Engineering |
| Automation | Automated (TLS enforcement) |

### 5.15 Access Control

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | RBAC via identity provider, least privilege principle, documented in access control policy |
| Evidence | IAM configurations, access control policy, access review records |
| Owner | IT / Security |
| Automation | Automated (provisioning), Semi-automated (reviews) |

### 5.16 Identity Management

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Centralized identity provider (Okta/Azure AD), unique identifiers, lifecycle management |
| Evidence | Identity provider configuration, provisioning workflows |
| Owner | IT |
| Automation | Automated |

### 5.17 Authentication Information

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | MFA required, password policy enforced, no shared credentials |
| Evidence | Identity provider MFA reports, password policy configuration |
| Owner | IT / Security |
| Automation | Automated (enforcement) |

### 5.18 Access Rights

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Role-based provisioning, quarterly access reviews, just-in-time access for privileged roles |
| Evidence | Access review records, JIT access logs |
| Owner | IT / System Owners |
| Automation | Semi-automated |

### 5.19 Information Security in Supplier Relationships

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Vendor security assessment process, contractual security requirements |
| Evidence | [supplier-security-questionnaire.md](../templates/supplier-security-questionnaire.md), vendor assessment records |
| Owner | GRC / Procurement |
| Automation | Manual |

### 5.20 Addressing Information Security Within Supplier Agreements

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Security addendum template, DPA requirements, right to audit clauses |
| Evidence | Contract templates, executed agreements |
| Owner | Legal / GRC |
| Automation | Manual |

### 5.21 Managing Information Security in the ICT Supply Chain

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Dependency scanning, SBOM generation, approved supplier list for critical components |
| Evidence | SCA scan reports, SBOM artifacts |
| Owner | Security Engineering |
| Automation | Automated (scanning) |

### 5.22 Monitoring, Review and Change Management of Supplier Services

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Annual vendor reviews, service level monitoring, change notification requirements |
| Evidence | Vendor review records, SLA reports |
| Owner | GRC / Vendor owners |
| Automation | Semi-automated |

### 5.23 Information Security for Use of Cloud Services

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Cloud security standards, CSPM monitoring, shared responsibility model documented |
| Evidence | Cloud security policy, CSPM reports |
| Owner | Security Engineering / Platform |
| Automation | Automated (CSPM) |

### 5.24 Information Security Incident Management Planning and Preparation

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Incident response plan documented, roles defined, communication templates prepared |
| Evidence | [10-incident-operating-loop.md](../docs/10-incident-operating-loop.md) |
| Owner | Security Lead |
| Automation | Manual |

### 5.25 Assessment and Decision on Information Security Events

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Triage process defined, severity classification criteria, escalation paths |
| Evidence | Incident records, triage decisions |
| Owner | Security Operations |
| Automation | Semi-automated (alerting automated, triage manual) |

### 5.26 Response to Information Security Incidents

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Containment, eradication, recovery procedures documented and tested |
| Evidence | Incident records, tabletop exercise records |
| Owner | Security Operations |
| Automation | Semi-automated |

### 5.27 Learning from Information Security Incidents

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Blameless postmortems, action items tracked to completion, lessons integrated |
| Evidence | Postmortem documents, action item tracker |
| Owner | Security Lead |
| Automation | Manual |

### 5.28 Collection of Evidence

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Evidence handling procedures, chain of custody documentation, forensic capability |
| Evidence | Evidence handling procedures, incident records |
| Owner | Security Operations |
| Automation | Manual |

### 5.29 Information Security During Disruption

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Business continuity plan includes security requirements, DR procedures maintain security controls |
| Evidence | BCP/DR plans, DR test records |
| Owner | SRE / Security |
| Automation | Manual |

### 5.30 ICT Readiness for Business Continuity

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | RTO/RPO defined, backup procedures, failover testing |
| Evidence | BCP documentation, backup reports, failover test records |
| Owner | SRE |
| Automation | Semi-automated (backups automated, testing manual) |

### 5.31 Legal, Statutory, Regulatory and Contractual Requirements

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Compliance register maintained, legal review process, regulatory monitoring |
| Evidence | Compliance register, legal review records |
| Owner | Legal / GRC |
| Automation | Manual |

### 5.32 Intellectual Property Rights

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | License compliance, open source policy, IP agreements with employees |
| Evidence | License inventory, employee agreements |
| Owner | Legal / Engineering |
| Automation | Semi-automated (license scanning) |

### 5.33 Protection of Records

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Retention schedules, secure storage, access controls on records |
| Evidence | Retention policy, storage configurations |
| Owner | GRC / IT |
| Automation | Semi-automated |

### 5.34 Privacy and Protection of PII

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Privacy policy, GDPR compliance, data minimization, consent management |
| Evidence | Privacy policy, DPA templates, consent records |
| Owner | Legal / GRC |
| Automation | Semi-automated |

### 5.35 Independent Review of Information Security

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Annual internal audit, external penetration tests, SOC 2 / ISO certification audits |
| Evidence | Audit reports, pentest reports, certification |
| Owner | GRC |
| Automation | Manual |

### 5.36 Compliance with Policies, Rules and Standards for Information Security

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Policy compliance monitoring, exception tracking, metrics reporting |
| Evidence | Compliance dashboard, exception register |
| Owner | GRC |
| Automation | Semi-automated |

### 5.37 Documented Operating Procedures

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Runbooks for security operations, procedures version controlled |
| Evidence | Runbook repository, version history |
| Owner | Security Operations |
| Automation | Manual (documentation), Automated (version control) |

---

## 6. People Controls

### 6.1 Screening

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Background checks for all employees, enhanced checks for sensitive roles |
| Evidence | HR screening records |
| Owner | HR |
| Automation | Manual |

### 6.2 Terms and Conditions of Employment

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Employment contracts include security responsibilities, confidentiality clauses |
| Evidence | Employment contract templates, signed contracts |
| Owner | HR / Legal |
| Automation | Manual |

### 6.3 Information Security Awareness, Education and Training

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Security awareness training on hire and annually, phishing simulations, role-based training |
| Evidence | LMS completion records, phishing simulation reports |
| Owner | Security / HR |
| Automation | Semi-automated (LMS tracking) |

### 6.4 Disciplinary Process

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Security violations included in disciplinary policy, escalation procedures |
| Evidence | HR policy, violation records |
| Owner | HR |
| Automation | Manual |

### 6.5 Responsibilities After Termination or Change of Employment

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | NDA remains in effect, offboarding includes security briefing on ongoing obligations |
| Evidence | NDA agreements, offboarding records |
| Owner | HR / Legal |
| Automation | Manual |

### 6.6 Confidentiality or Non-Disclosure Agreements

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | NDA required for employees, contractors, and third parties with access to confidential information |
| Evidence | Signed NDAs |
| Owner | Legal / HR |
| Automation | Manual |

### 6.7 Remote Working

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Remote work security policy, VPN/ZTNA required, endpoint protection mandatory |
| Evidence | Remote work policy, VPN/ZTNA configuration, endpoint compliance reports |
| Owner | IT / Security |
| Automation | Automated (endpoint compliance) |

### 6.8 Information Security Event Reporting

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Security incident reporting channel, awareness training on what to report |
| Evidence | Reporting channel configuration, training materials |
| Owner | Security |
| Automation | Semi-automated (ticketing) |

---

## 7. Physical Controls

### 7.1 - 7.14 Physical Security Controls

| Field | Value |
|-------|-------|
| Applicability | Limited - Cloud-first organization |
| Implementation | Cloud provider physical security relied upon for infrastructure; office security managed by facilities |
| Evidence | Cloud provider SOC 2 reports, office security procedures |
| Owner | Facilities / Cloud providers |
| Automation | N/A (outsourced) |

**Note:** As a cloud-first organization, physical security for infrastructure is delegated to cloud providers (AWS, GCP, Azure) whose compliance is verified through their SOC 2 Type II reports. Office physical security is managed separately.

---

## 8. Technological Controls

### 8.1 User Endpoint Devices

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | MDM enrollment required, disk encryption, EDR deployment, automatic updates |
| Evidence | MDM compliance reports, EDR dashboard |
| Owner | IT |
| Automation | Automated |

### 8.2 Privileged Access Rights

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Just-in-time access, separate admin accounts, MFA required, privileged access workstations for sensitive operations |
| Evidence | JIT access logs, admin account inventory |
| Owner | IT / Security |
| Automation | Semi-automated |

### 8.3 Information Access Restriction

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | RBAC, need-to-know principle, data access controls based on classification |
| Evidence | IAM policies, access control configurations |
| Owner | System Owners / IT |
| Automation | Automated |

### 8.4 Access to Source Code

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Repository access controls, branch protection, code review requirements |
| Evidence | Repository settings, access audit logs |
| Owner | Engineering |
| Automation | Automated |

### 8.5 Secure Authentication

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | MFA required, SSO integration, passwordless options available, session management |
| Evidence | Identity provider configuration, MFA enrollment reports |
| Owner | IT / Security |
| Automation | Automated |

### 8.6 Capacity Management

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Cloud auto-scaling, capacity monitoring and alerting, resource quotas |
| Evidence | Cloud configuration, monitoring dashboards |
| Owner | SRE / Platform |
| Automation | Automated |

### 8.7 Protection Against Malware

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | EDR on all endpoints, email security gateway, sandboxing for suspicious files |
| Evidence | EDR dashboard, email security reports |
| Owner | IT / Security |
| Automation | Automated |

### 8.8 Management of Technical Vulnerabilities

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Vulnerability scanning, patch management SLAs, remediation tracking per [06-kpis-and-metrics.md](../docs/06-kpis-and-metrics.md) |
| Evidence | Vulnerability scan reports, patch compliance reports |
| Owner | Security Engineering |
| Automation | Automated (scanning), Semi-automated (remediation) |

### 8.9 Configuration Management

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Infrastructure as Code, CSPM monitoring, baseline configurations, drift detection |
| Evidence | IaC repositories, CSPM reports |
| Owner | Platform Engineering |
| Automation | Automated |

### 8.10 Information Deletion

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Data retention policies, automated deletion, secure deletion procedures |
| Evidence | Retention policy, deletion logs |
| Owner | Data Engineering / GRC |
| Automation | Semi-automated |

### 8.11 Data Masking

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | PII masking in non-production environments, log sanitization |
| Evidence | Data masking configuration, environment policies |
| Owner | Data Engineering |
| Automation | Automated |

### 8.12 Data Leakage Prevention

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | DLP on email and endpoints, cloud DLP for storage, egress monitoring |
| Evidence | DLP policy configuration, DLP reports |
| Owner | Security Engineering |
| Automation | Automated |

### 8.13 Information Backup

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Automated backups, encrypted backup storage, offsite replication, restoration testing |
| Evidence | Backup job logs, restoration test records |
| Owner | SRE |
| Automation | Automated (backups), Manual (restoration tests) |

### 8.14 Redundancy of Information Processing Facilities

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Multi-AZ deployment, database replication, failover automation |
| Evidence | Architecture diagrams, failover test records |
| Owner | SRE / Platform |
| Automation | Automated |

### 8.15 Logging

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Centralized logging, security event logging, log integrity protection, retention per policy |
| Evidence | SIEM configuration, log retention settings |
| Owner | Security Engineering |
| Automation | Automated |

### 8.16 Monitoring Activities

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | SIEM with detection rules, alerting, 24/7 monitoring coverage |
| Evidence | SIEM dashboards, alert configurations, on-call schedules |
| Owner | Security Operations |
| Automation | Automated (detection), Semi-automated (response) |

### 8.17 Clock Synchronisation

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | NTP configuration on all systems, cloud provider time sync |
| Evidence | NTP configuration |
| Owner | Platform Engineering |
| Automation | Automated |

### 8.18 Use of Privileged Utility Programs

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Restricted access to system utilities, audit logging of privileged operations |
| Evidence | Access controls, audit logs |
| Owner | Platform Engineering |
| Automation | Automated |

### 8.19 Installation of Software on Operational Systems

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | CI/CD deployment only, no manual installations in production, change management process |
| Evidence | Deployment logs, change records |
| Owner | Platform Engineering |
| Automation | Automated |

### 8.20 Networks Security

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Network segmentation, firewall rules, VPC design, no default routes |
| Evidence | Network diagrams, security group configurations |
| Owner | Platform Engineering |
| Automation | Automated (IaC) |

### 8.21 Security of Network Services

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | TLS for all services, network service hardening, regular security assessments |
| Evidence | TLS configuration, network scan reports |
| Owner | Platform Engineering / Security |
| Automation | Automated |

### 8.22 Segregation of Networks

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Separate VPCs/networks for production, staging, development; no direct routing between |
| Evidence | Network architecture diagrams, routing tables |
| Owner | Platform Engineering |
| Automation | Automated (IaC) |

### 8.23 Web Filtering

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | DNS filtering, web proxy for corporate devices |
| Evidence | DNS filter configuration, proxy logs |
| Owner | IT |
| Automation | Automated |

### 8.24 Use of Cryptography

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Encryption standards defined, TLS 1.2+ required, approved algorithms only |
| Evidence | Cryptography policy, configuration audits |
| Owner | Security Engineering |
| Automation | Automated (enforcement via policy-as-code) |

### 8.25 Secure Development Life Cycle

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | SDLC includes security requirements, security review gates, security testing |
| Evidence | [09-security-review-process.md](../docs/09-security-review-process.md), CI/CD configuration |
| Owner | Security / Engineering |
| Automation | Semi-automated |

### 8.26 Application Security Requirements

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Security requirements in design process, OWASP guidelines, secure coding training |
| Evidence | Security review records, training completion |
| Owner | Security |
| Automation | Manual |

### 8.27 Secure System Architecture and Engineering Principles

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Security architecture principles documented, defense in depth, least privilege |
| Evidence | [01-north-star-and-principles.md](../docs/01-north-star-and-principles.md), architecture documents |
| Owner | Security / Platform |
| Automation | Manual |

### 8.28 Secure Coding

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | SAST in CI/CD, code review requirements, secure coding guidelines |
| Evidence | SAST reports, code review records |
| Owner | Engineering / Security |
| Automation | Automated (SAST) |

### 8.29 Security Testing in Development and Acceptance

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | SAST, DAST, dependency scanning in pipeline; security acceptance criteria |
| Evidence | CI/CD pipeline configuration, scan reports |
| Owner | Security Engineering |
| Automation | Automated |

### 8.30 Outsourced Development

| Field | Value |
|-------|-------|
| Applicability | Applicable where used |
| Implementation | Security requirements in contracts, code review for external contributions, same security standards |
| Evidence | Contract terms, review records |
| Owner | Engineering / Security |
| Automation | Manual |

### 8.31 Separation of Development, Test and Production Environments

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Separate environments with different credentials, no production data in lower environments (or masked) |
| Evidence | Environment configurations, data masking policies |
| Owner | Platform Engineering |
| Automation | Automated |

### 8.32 Change Management

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Change management process, approval workflows, rollback procedures |
| Evidence | Change records, deployment logs |
| Owner | Engineering / SRE |
| Automation | Semi-automated |

### 8.33 Test Information

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Production data not used in testing, synthetic or masked data for test environments |
| Evidence | Test data policies, data masking configuration |
| Owner | Data Engineering |
| Automation | Automated |

### 8.34 Protection of Information Systems During Audit Testing

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Audit activities scheduled, separate audit accounts, audit scope controls |
| Evidence | Audit plans, audit account configurations |
| Owner | GRC |
| Automation | Manual |

---

## Summary

| Category | Total Controls | Applicable | Automated | Semi-Automated | Manual |
|----------|---------------|------------|-----------|----------------|--------|
| 5. Organizational | 37 | 37 | 8 | 18 | 11 |
| 6. People | 8 | 8 | 1 | 2 | 5 |
| 7. Physical | 14 | Limited | N/A | N/A | Outsourced |
| 8. Technological | 34 | 34 | 22 | 9 | 3 |
| **Total** | 93 | 79+ | 31 | 29 | 19 |
