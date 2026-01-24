# Risk Prioritization Framework

This document defines how we assess, score, and prioritize security risks.

---

## Risk Scoring Methodology

We use a simplified Impact x Likelihood model with a Detectability modifier.

### Impact Scale (1-5)

| Score | Level | Definition | Examples |
|-------|-------|------------|----------|
| 5 | Critical | Existential threat to business | Major data breach, complete system compromise, regulatory shutdown |
| 4 | High | Significant financial or operational damage | Partial data breach, extended outage, major customer loss |
| 3 | Medium | Moderate damage requiring significant response | Limited data exposure, service degradation, compliance finding |
| 2 | Low | Minor damage with contained impact | Small data leak, brief outage, isolated incident |
| 1 | Minimal | Negligible business impact | Failed attack attempt, minor policy violation |

### Likelihood Scale (1-5)

| Score | Level | Definition | Timeframe |
|-------|-------|------------|-----------|
| 5 | Almost Certain | Expected to occur | Within 6 months |
| 4 | Likely | More likely than not | Within 1 year |
| 3 | Possible | Could occur | Within 2 years |
| 2 | Unlikely | Not expected but possible | Within 3 years |
| 1 | Rare | Highly improbable | Beyond 3 years |

### Detectability Modifier

Detectability adjusts the base risk score. Poor detection means higher effective risk.

| Detection Level | Modifier | Definition |
|----------------|----------|------------|
| Real-time automated | -2 | Detected immediately with automated response |
| Near real-time | -1 | Detected within hours through monitoring |
| Periodic | 0 | Detected through scheduled scans/audits |
| Reactive | +1 | Detected only after impact observed |
| None | +2 | No detection capability exists |

### Final Risk Score

```
Risk Score = (Impact x Likelihood) + Detectability Modifier
```

Maximum score: 27 (5 x 5 + 2)
Minimum score: -1 (1 x 1 - 2)

### Priority Mapping

| Score Range | Priority | Response Expectation |
|-------------|----------|---------------------|
| 20-27 | P1 - Critical | Immediate action, escalate to leadership |
| 13-19 | P2 - High | Address within current quarter |
| 7-12 | P3 - Medium | Plan for next quarter |
| 1-6 | P4 - Low | Address opportunistically |
| < 1 | P5 - Accepted | Monitor only |

---

## Risk Register

### Active Risks

| ID | Risk Description | Impact | Likelihood | Detect | Score | Priority | Owner | Status |
|----|------------------|--------|------------|--------|-------|----------|-------|--------|
| R-001 | Secrets in source code repositories | 5 | 4 | -1 | 19 | P2 | Security Eng | In Treatment |
| R-002 | Overly permissive IAM roles in production | 4 | 4 | 0 | 16 | P2 | Cloud Platform | In Treatment |
| R-003 | Unpatched critical vulnerabilities beyond SLA | 4 | 3 | -1 | 11 | P3 | Security Eng | In Treatment |
| R-004 | No MFA on third-party SaaS applications | 4 | 3 | +1 | 13 | P2 | IT | In Treatment |
| R-005 | Insufficient logging for forensic investigation | 3 | 3 | +2 | 11 | P3 | Security Eng | In Treatment |
| R-006 | Developer laptops without EDR | 4 | 3 | +1 | 13 | P2 | IT | In Treatment |
| R-007 | Lack of network segmentation between environments | 4 | 2 | 0 | 8 | P3 | Cloud Platform | Planned |
| R-008 | No formal vendor security assessment process | 3 | 4 | +1 | 13 | P2 | GRC | In Treatment |
| R-009 | Incomplete data classification and handling | 3 | 3 | +1 | 10 | P3 | GRC | Planned |
| R-010 | Backup restoration not regularly tested | 5 | 2 | +1 | 11 | P3 | SRE | In Treatment |

### Risk Treatment Status Definitions

| Status | Definition |
|--------|------------|
| Identified | Risk documented but no treatment started |
| In Treatment | Active remediation work underway |
| Planned | Treatment scheduled for future quarter |
| Accepted | Business has formally accepted the risk |
| Mitigated | Controls implemented, monitoring residual risk |
| Closed | Risk no longer applicable |

---

## Risk Detail: R-001 Secrets in Source Code

**Description:** Credentials, API keys, and other secrets committed to source code repositories, creating exposure risk if repositories are compromised or made public.

**Current State:**
- Secret scanning enabled on new commits
- Historical secrets not fully remediated
- Some teams using environment variables instead of vault

**Treatment Plan:**
1. Complete historical secret rotation (Q1)
2. Mandate HashiCorp Vault for all production secrets (Q1)
3. Block commits containing secrets via pre-commit hooks (Q2)
4. Implement secret rotation automation (Q2)

**Evidence of Progress:**
- Secret scanning alert backlog: 47 (down from 156)
- Teams onboarded to Vault: 8/12
- Pre-commit hooks deployed: 60% of repositories

**Compensating Controls:**
- All flagged secrets rotated within 24 hours of detection
- Repository access restricted to employees only
- Audit logging on all repository access

---

## Risk Detail: R-002 Overly Permissive IAM Roles

**Description:** Production IAM roles with broader permissions than required, increasing blast radius if credentials are compromised.

**Current State:**
- Legacy roles with admin-level permissions
- No systematic least-privilege review process
- IAM Access Analyzer enabled but findings not fully addressed

**Treatment Plan:**
1. Inventory all production IAM roles (Complete)
2. Prioritize roles by permission scope and usage (Q1)
3. Refactor top 20 overly permissive roles (Q1-Q2)
4. Implement permission boundaries for all new roles (Q1)
5. Establish quarterly IAM review process (Q2)

**Evidence of Progress:**
- Roles inventoried: 100%
- High-priority roles identified: 23
- Roles refactored: 8/23
- Permission boundaries template: Complete

**Compensating Controls:**
- CloudTrail logging of all IAM activity
- Alerts on sensitive API calls
- Monthly review of unused permissions

---

## Accepted Risks

Risks that have been formally accepted by business stakeholders.

| ID | Risk | Accepted By | Acceptance Date | Review Date | Rationale |
|----|------|-------------|-----------------|-------------|-----------|
| R-011 | Legacy app without WAF protection | VP Engineering | 2025-09-15 | 2025-03-15 | App scheduled for retirement Q2; WAF integration cost exceeds value |
| R-012 | Manual access reviews (not automated) | CISO | 2025-10-01 | 2025-04-01 | Automation project planned for Q2; compensating monthly manual review |

---

## Risk Appetite Statement

### What We Accept

- Residual risk after reasonable controls are implemented
- Temporary elevated risk during migrations with compensating controls
- Low-impact risks that would be costly to fully eliminate

### What We Do Not Accept

- Unmitigated critical risks to customer data
- Risks without identified owners
- Permanent exceptions without review dates
- Risks that violate legal or regulatory requirements

---

## Governance

### Risk Review Cadence

| Activity | Frequency | Participants |
|----------|-----------|--------------|
| Risk register review | Monthly | Security team |
| Priority risk deep-dive | Bi-weekly | Risk owners + Security |
| Leadership risk report | Quarterly | CISO, CTO, CEO |
| Full risk assessment | Annually | All stakeholders |

### Escalation Criteria

Escalate to leadership immediately when:

- New P1 risk identified
- Risk score increases by 5+ points
- Treatment plan misses milestone by 30+ days
- External threat intelligence indicates imminent threat

---

## Updating This Document

- Risk register updated as risks are identified or status changes
- Full methodology review annually
- Changes to scoring criteria require security leadership approval
