# Security Design Review

## Project Information

| Field | Value |
|-------|-------|
| Project Name | |
| Review ID | SDR-YYYY-NNN |
| Project Lead | |
| Engineering Team | |
| Review Type | [ ] Lightweight [ ] Standard [ ] Deep Dive |
| Review Date | |
| Reviewer(s) | |

---

## Project Overview

### Description

[Brief description of the project, feature, or change]

### Business Context

[Why is this being built? What business problem does it solve?]

### Timeline

| Milestone | Date |
|-----------|------|
| Design complete | |
| Development start | |
| Target launch | |

---

## Architecture Overview

### System Diagram

[Include or reference architecture diagram]

### Components

| Component | Description | New/Existing | Technology |
|-----------|-------------|--------------|------------|
| | | | |

### External Dependencies

| Dependency | Purpose | Data Exchanged |
|------------|---------|----------------|
| | | |

---

## Data Assessment

### Data Inventory

| Data Element | Classification | Source | Storage | Retention |
|--------------|----------------|--------|---------|-----------|
| | [Public/Internal/Confidential/Restricted] | | | |

### Data Flow

[Describe or diagram how data flows through the system]

**Data at Rest:**
- Where is data stored?
- Is it encrypted? (Algorithm, key management)
- Who has access to storage?

**Data in Transit:**
- What protocols are used?
- Is TLS enforced?
- Are there any unencrypted channels?

### Data Handling

- [ ] PII is minimized (only collect what's needed)
- [ ] Retention periods defined
- [ ] Deletion/anonymization process exists
- [ ] Data residency requirements addressed

---

## Authentication and Authorization

### Authentication

| Question | Answer |
|----------|--------|
| How are users authenticated? | |
| Is MFA required? | |
| How are sessions managed? | |
| Session timeout configured? | |

### Authorization

| Question | Answer |
|----------|--------|
| What authorization model is used? | [RBAC/ABAC/ACL/etc.] |
| How are permissions assigned? | |
| Are there different privilege levels? | |
| How is access revoked? | |

### Service-to-Service Authentication

| Question | Answer |
|----------|--------|
| How do services authenticate to each other? | |
| Are credentials short-lived? | |
| How are secrets managed? | |

---

## Input Handling

### Input Sources

| Input | Source | Validation Method |
|-------|--------|-------------------|
| | | |

### Input Validation

- [ ] All inputs validated on server side
- [ ] Input length limits enforced
- [ ] Allowlists used where possible
- [ ] Encoding/escaping applied to outputs

### File Handling (if applicable)

- [ ] File types restricted
- [ ] File size limits enforced
- [ ] Files scanned for malware
- [ ] Files stored outside web root

---

## Security Controls Checklist

### Infrastructure

| Control | Status | Notes |
|---------|--------|-------|
| Network segmentation appropriate | [ ] Yes [ ] No [ ] N/A | |
| Security groups/firewalls configured | [ ] Yes [ ] No [ ] N/A | |
| No public exposure of internal services | [ ] Yes [ ] No [ ] N/A | |
| Infrastructure as Code used | [ ] Yes [ ] No [ ] N/A | |

### Application

| Control | Status | Notes |
|---------|--------|-------|
| HTTPS enforced | [ ] Yes [ ] No [ ] N/A | |
| Security headers configured | [ ] Yes [ ] No [ ] N/A | |
| CSRF protection enabled | [ ] Yes [ ] No [ ] N/A | |
| Rate limiting implemented | [ ] Yes [ ] No [ ] N/A | |
| Error handling doesn't leak info | [ ] Yes [ ] No [ ] N/A | |

### Secrets Management

| Control | Status | Notes |
|---------|--------|-------|
| No hardcoded secrets | [ ] Yes [ ] No [ ] N/A | |
| Secrets in vault/secrets manager | [ ] Yes [ ] No [ ] N/A | |
| Secrets rotatable | [ ] Yes [ ] No [ ] N/A | |
| Least privilege for secret access | [ ] Yes [ ] No [ ] N/A | |

### Logging and Monitoring

| Control | Status | Notes |
|---------|--------|-------|
| Security events logged | [ ] Yes [ ] No [ ] N/A | |
| PII excluded/masked in logs | [ ] Yes [ ] No [ ] N/A | |
| Logs sent to central system | [ ] Yes [ ] No [ ] N/A | |
| Alerts configured for security events | [ ] Yes [ ] No [ ] N/A | |

---

## Threat Model

### Assets

| Asset | Value | Why It Matters |
|-------|-------|----------------|
| | | |

### Threat Analysis (STRIDE)

| Threat | Applicable? | Scenario | Mitigation |
|--------|-------------|----------|------------|
| **Spoofing** | [ ] Yes [ ] No | | |
| **Tampering** | [ ] Yes [ ] No | | |
| **Repudiation** | [ ] Yes [ ] No | | |
| **Information Disclosure** | [ ] Yes [ ] No | | |
| **Denial of Service** | [ ] Yes [ ] No | | |
| **Elevation of Privilege** | [ ] Yes [ ] No | | |

### Abuse Cases

| Abuse Case | Likelihood | Impact | Mitigation |
|------------|------------|--------|------------|
| | | | |

---

## Third-Party Assessment

### Third-Party Services

| Service | Data Shared | Security Assessment | Contract Terms |
|---------|-------------|---------------------|----------------|
| | | [ ] Complete [ ] Pending [ ] N/A | [ ] Reviewed [ ] Pending |

### Open Source Dependencies

- [ ] Dependencies scanned for vulnerabilities
- [ ] Licenses reviewed for compliance
- [ ] Update process defined

---

## Compliance Considerations

| Requirement | Applicable? | How Addressed |
|-------------|-------------|---------------|
| GDPR | [ ] Yes [ ] No | |
| SOC 2 | [ ] Yes [ ] No | |
| ISO 27001 | [ ] Yes [ ] No | |
| PCI DSS | [ ] Yes [ ] No | |
| HIPAA | [ ] Yes [ ] No | |
| Other: | [ ] Yes [ ] No | |

---

## Findings

### Critical Findings

| ID | Finding | Risk | Recommendation | Owner | Due Date |
|----|---------|------|----------------|-------|----------|
| | | | | | |

### High Findings

| ID | Finding | Risk | Recommendation | Owner | Due Date |
|----|---------|------|----------------|-------|----------|
| | | | | | |

### Medium Findings

| ID | Finding | Risk | Recommendation | Owner | Due Date |
|----|---------|------|----------------|-------|----------|
| | | | | | |

### Low Findings / Recommendations

| ID | Finding | Recommendation |
|----|---------|----------------|
| | | |

---

## Review Outcome

### Decision

- [ ] **Approved** - Proceed with implementation
- [ ] **Approved with Conditions** - Proceed after addressing specified items
- [ ] **Not Approved** - Significant concerns must be resolved
- [ ] **Deferred** - More information needed

### Conditions for Approval

[List any conditions that must be met before or during implementation]

1.
2.
3.

### Required Before Launch

- [ ] All Critical findings remediated
- [ ] All High findings remediated or risk-accepted
- [ ] Medium findings have remediation plan
- [ ] Security sign-off obtained

---

## Sign-off

### Security Reviewer

| Field | Value |
|-------|-------|
| Reviewer | |
| Date | |
| Outcome | |

**Signature:** _________________________

### Project Lead Acknowledgment

I acknowledge the findings in this review and commit to addressing them per the agreed timeline.

| Field | Value |
|-------|-------|
| Project Lead | |
| Date | |

**Signature:** _________________________

---

## Follow-up

| Action | Owner | Due Date | Status |
|--------|-------|----------|--------|
| | | | |

### Post-Launch Review

- [ ] Required (for high-risk projects)
- [ ] Not required

If required, scheduled for: [Date]
