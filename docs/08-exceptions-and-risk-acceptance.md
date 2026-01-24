# Exceptions and Risk Acceptance

This document defines the processes for handling security exceptions and formal risk acceptance.

---

## Core Principles

1. **Exceptions are not failures** - They're evidence that governance works with business reality
2. **All exceptions are temporary** - Permanent exceptions become policy changes
3. **Business owns the risk** - Security advises, business decides and accepts
4. **Compensating controls required** - Exceptions without mitigation are just ignored risks
5. **Transparency over avoidance** - A documented exception is better than an unknown gap

---

## Exception vs. Risk Acceptance

| Concept | Definition | Duration | Approval |
|---------|------------|----------|----------|
| **Exception** | Temporary deviation from a security control | Max 90 days, renewable | Security Lead |
| **Risk Acceptance** | Formal acknowledgment of residual risk | Until risk changes | Business Owner + Security |

**When to use which:**

- **Exception:** "We can't implement MFA on this legacy system yet, but will in Q2"
- **Risk Acceptance:** "We understand this legacy system has limited security controls and accept the residual risk given its isolation and planned retirement"

---

## Exception Process

### Eligibility

Exceptions may be requested when:

- A security control cannot be implemented due to technical constraints
- Business urgency requires temporary deviation
- A control is in progress but not yet complete
- Third-party limitations prevent compliance

Exceptions are **not appropriate** for:

- Convenience or cost savings alone
- Permanent gaps (use risk acceptance instead)
- Controls that are fundamental and non-negotiable
- Situations where compensating controls are impossible

### Exception Request Flow

```
Requestor                    Security                    Business Owner
    |                            |                            |
    |-- Submit request --------->|                            |
    |                            |-- Review & assess risk --->|
    |                            |                            |
    |                            |<-- (If >30 days) Approval -|
    |                            |                            |
    |<-- Approve/Deny/Modify ----|                            |
    |                            |                            |
    |-- Implement compensating --|                            |
    |   controls                 |                            |
    |                            |                            |
    |<-- Monitor until expiry ---|                            |
```

### Exception Request Template

See [templates/exception-request.md](../templates/exception-request.md) for the full template.

Required information:

1. **What control is being excepted?**
2. **Why can't the control be implemented?**
3. **What is the business impact of not granting the exception?**
4. **What compensating controls will be in place?**
5. **What is the remediation plan and timeline?**
6. **Who is the business owner accepting this risk?**

### Approval Authority

| Exception Duration | Approver | Additional Requirements |
|--------------------|----------|------------------------|
| Up to 30 days | Security Lead | Compensating controls documented |
| 31-90 days | Security Lead + Business Owner | Remediation plan with milestones |
| Renewal (any) | Original approvers + GRC review | Progress report on remediation |

### Exception Conditions

All approved exceptions must include:

1. **Expiration date** - Maximum 90 days from approval
2. **Compensating controls** - Alternative protections in place
3. **Monitoring requirements** - How we'll detect if risk materializes
4. **Remediation plan** - Steps to eliminate the exception
5. **Business owner** - Named individual accountable for the risk

### Exception Renewal

To renew an expiring exception:

1. Submit renewal request 14 days before expiration
2. Document progress on remediation plan
3. Explain why remediation is not yet complete
4. Update compensating controls if needed
5. Obtain re-approval from original approvers

**Renewal limits:**

- Maximum 3 renewals (total 360 days)
- After 3 renewals, must convert to formal risk acceptance or remediate

---

## Risk Acceptance Process

### When Risk Acceptance Is Required

- Residual risk remains after all reasonable controls
- Business decides to operate a system despite known vulnerabilities
- Compliance gaps that cannot be closed in reasonable timeframe
- Third-party risks outside our direct control

### Risk Acceptance Requirements

1. **Risk assessment** - Documented analysis of the risk
2. **Control evaluation** - Evidence that reasonable controls were considered
3. **Business justification** - Why accepting the risk is appropriate
4. **Compensating controls** - What mitigations are in place
5. **Review trigger** - Conditions that would require re-evaluation
6. **Business owner signature** - Named executive accepting the risk

### Risk Acceptance Template

See [templates/risk-acceptance.md](../templates/risk-acceptance.md) for the full template.

### Approval Authority

| Risk Level | Approver |
|------------|----------|
| Low | Department Director |
| Medium | VP / Senior Director |
| High | C-level (CTO, CFO, CEO depending on domain) |
| Critical | CEO + Board notification |

### Risk Acceptance Review

All accepted risks are reviewed:

- **Quarterly** - Verify conditions haven't changed
- **Annually** - Full re-evaluation and re-approval
- **On trigger** - When predefined conditions occur

---

## Compensating Controls

### What Makes a Good Compensating Control

| Criterion | Description |
|-----------|-------------|
| **Addresses the risk** | Directly mitigates the threat the original control addressed |
| **Proportionate** | Effort matches the risk level |
| **Verifiable** | Can confirm it's working |
| **Sustainable** | Can maintain for exception duration |
| **Independent** | Doesn't rely on the failed control |

### Examples of Compensating Controls

| Missing Control | Compensating Control |
|-----------------|---------------------|
| MFA not available | IP restriction + enhanced monitoring + shorter session timeout |
| Encryption at rest not supported | Network isolation + access logging + data minimization |
| Automated scanning not possible | Manual security review + enhanced monitoring |
| Patch cannot be applied | Virtual patching via WAF + network segmentation |
| Full audit logging not available | Additional application-level logging + file integrity monitoring |

### Compensating Controls Are Not

- "We'll be careful"
- "Users are trained"
- "It's on the internal network"
- "We haven't been breached yet"
- Documentation without enforcement

---

## Tracking and Reporting

### Exception Register

All exceptions tracked with:

| Field | Description |
|-------|-------------|
| Exception ID | Unique identifier |
| Control excepted | Reference to control/policy |
| System/scope | What's affected |
| Business owner | Accountable person |
| Approval date | When approved |
| Expiration date | When it expires |
| Compensating controls | What's in place |
| Remediation plan | Steps to close |
| Status | Open / Renewed / Closed / Expired |

### Metrics

Track and report monthly:

- Total open exceptions
- Exceptions by age bucket (0-30, 31-60, 61-90, expired)
- Exceptions by system/team
- Exception-to-remediation conversion rate
- Average exception duration
- Expired exceptions (compliance failures)

### Escalation

Escalate to leadership when:

- Exception expires without renewal or remediation
- Same system has 3+ concurrent exceptions
- Exception renewal count exceeds 2
- High/Critical risk exception requested
- Pattern of exceptions suggests systemic issue

---

## Non-Negotiable Controls

Some controls cannot be excepted under any circumstances:

| Control | Rationale |
|---------|-----------|
| Production secrets in source code | No compensating control is sufficient |
| Anonymous access to customer data | Fundamental privacy requirement |
| Disabled audit logging in production | Essential for incident response |
| Shared credentials for production access | Attribution is non-negotiable |

For these, the only path is remediation or system decommissioning.

---

## Governance

### Roles

| Role | Responsibility |
|------|----------------|
| Requestor | Submit complete request, implement compensating controls |
| Security | Assess risk, recommend approval/denial, monitor compliance |
| Business Owner | Accept risk, ensure remediation resources |
| GRC | Track exceptions, report metrics, manage renewal process |

### Process Review

This process is reviewed annually or when:

- Exception volume indicates process problems
- Incidents result from excepted controls
- Feedback suggests process is too burdensome or too lax
