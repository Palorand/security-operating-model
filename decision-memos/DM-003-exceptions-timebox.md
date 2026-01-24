# Decision Memo: All Exceptions Are Timeboxed

## Document Information

| Field | Value |
|-------|-------|
| Decision ID | DM-003 |
| Title | All Security Exceptions Are Timeboxed |
| Author | Security Lead |
| Date | 2024-11-15 |
| Status | Approved |

---

## Executive Summary

All security exceptions are limited to a maximum of 90 days, with a maximum of 3 renewals (360 days total). Exceptions that cannot be remediated within this timeframe must be converted to formal risk acceptances with business owner sign-off. This prevents exception debt accumulation and ensures accountability for security deviations.

---

## Context

### Background

Security exceptions allow temporary deviations from controls when business needs require flexibility. However, without governance, exceptions become permanent:

- "Temporary" exceptions from 2+ years ago still active
- No tracking of exception age or renewal history
- Business owners change, accountability lost
- Compensating controls degrade over time
- Audit findings cite unmanaged exceptions

### Current State

Analysis of existing exceptions revealed:

| Age | Count | Percentage |
|-----|-------|------------|
| < 90 days | 8 | 25% |
| 90-180 days | 6 | 19% |
| 180-365 days | 7 | 22% |
| > 365 days | 11 | 34% |

**34% of exceptions are over a year old** with no formal review or renewal.

### Trigger

- ISO 27001 audit finding: "Exception management process lacks defined timeframes and review requirements"
- SOC 2 auditor questions about perpetual exceptions
- New Security Lead review of exception backlog

---

## Decision

### Statement

**All security exceptions are limited to 90 days maximum duration. Exceptions may be renewed up to 3 times (360 days total) with documented progress. After 360 days, the exception must be either remediated or converted to a formal risk acceptance.**

### Key Rules

| Rule | Requirement |
|------|-------------|
| Maximum initial duration | 90 days |
| Maximum renewals | 3 |
| Maximum total duration | 360 days |
| Renewal requirement | Progress report on remediation |
| Post-360-day path | Remediate OR formal risk acceptance |

### Scope

| Attribute | Value |
|-----------|-------|
| Applies to | All security exceptions, all systems |
| Effective date | 2024-12-01 (new), 2025-02-01 (existing) |
| Review date | 2025-11-15 |

---

## Options Considered

### Option 1: No Time Limits (Status Quo)

**Description:** Continue allowing indefinite exceptions with periodic review.

| Pros | Cons |
|------|------|
| No process change | Exception debt continues to grow |
| Flexibility for teams | No accountability |
| | Compliance risk |
| | Audit findings |

**Estimated effort:** None

### Option 2: Strict 90-Day Limit, No Renewals

**Description:** All exceptions must be remediated within 90 days, no extensions.

| Pros | Cons |
|------|------|
| Forces remediation | Unrealistic for complex issues |
| Simple to administer | Would create compliance theater |
| | Teams would work around it |

**Estimated effort:** Low

### Option 3: Tiered Timeboxing with Renewal Limits (Selected)

**Description:** 90-day periods with up to 3 renewals, then formal risk acceptance required.

| Pros | Cons |
|------|------|
| Balances flexibility and accountability | More complex than binary approach |
| Forces progress visibility | Requires tracking infrastructure |
| Clear escalation path | |
| Aligns with audit expectations | |

**Estimated effort:** Medium

---

## Rationale

### Why This Option?

The tiered approach acknowledges reality while enforcing accountability:

1. **90 days is achievable** for most remediations with proper prioritization
2. **Renewals require progress** - no "set and forget" exceptions
3. **360-day limit** forces a decision: fix it or formally own the risk
4. **Risk acceptance escalation** ensures business ownership of long-term risks

### Key Factors

| Factor | Weight | How Selected Option Performs |
|--------|--------|------------------------------|
| Audit compliance | High | Meets ISO 27001 / SOC 2 requirements |
| Operational feasibility | High | Achievable timelines |
| Accountability | High | Clear ownership at each stage |
| Flexibility | Medium | Renewals provide buffer |

### Trade-offs Accepted

- Administrative overhead for tracking and renewals
- Some exceptions will convert to risk acceptances (this is intended)
- Teams may need to prioritize security work they previously deferred

---

## Implementation

### Exception Lifecycle

```
Exception Requested
        |
        v
Security Review (Approve/Deny)
        |
        v
Exception Active (Day 1-90)
        |
        v
Day 75: Renewal reminder sent
        |
        +---> Remediated? ---> Exception Closed
        |
        v
Renewal Requested (with progress report)
        |
        v
Renewal 1 Approved (Day 91-180)
        |
        v
[Repeat for Renewal 2, 3]
        |
        v
Day 360: Final deadline
        |
        +---> Remediated? ---> Exception Closed
        |
        v
Convert to Risk Acceptance
        |
        v
Business Owner Sign-off Required
        |
        v
Risk Acceptance Active (Annual Review)
```

### Renewal Requirements

To renew an exception, the requestor must provide:

1. **Progress report** - What remediation work was completed?
2. **Blockers** - What prevented full remediation?
3. **Updated timeline** - Realistic completion date
4. **Compensating controls** - Still in place and effective?
5. **Business justification** - Why is more time needed?

Renewals are **not automatic**. Security reviews each renewal request.

### Risk Acceptance Conversion

When an exception reaches 360 days:

1. Exception owner notified at day 300
2. Options presented: remediate or convert to risk acceptance
3. Risk acceptance requires:
   - Formal risk assessment
   - Business owner (director+) sign-off
   - Documented compensating controls
   - Annual review commitment
4. Risk acceptance tracked separately from exceptions

### Existing Exceptions Migration

| Current Age | Action | Deadline |
|-------------|--------|----------|
| < 90 days | Continue with new rules | Current expiration |
| 90-180 days | Counts as 1 renewal used | 90 days from effective date |
| 180-270 days | Counts as 2 renewals used | 90 days from effective date |
| 270-360 days | Counts as 3 renewals used | 90 days from effective date |
| > 360 days | Immediate conversion to risk acceptance | 2025-02-01 |

### Timeline

| Milestone | Target Date | Owner |
|-----------|-------------|-------|
| Policy published | 2024-11-20 | Security Lead |
| Tracking system updated | 2024-11-30 | GRC |
| New exceptions follow policy | 2024-12-01 | All |
| Existing exception inventory | 2024-12-15 | GRC |
| Migration plan per exception | 2025-01-15 | Exception owners |
| All exceptions compliant | 2025-02-01 | All |

---

## Impact Assessment

### Affected Stakeholders

| Stakeholder | Impact | Communication Needed |
|-------------|--------|---------------------|
| Exception owners | Must remediate or escalate | Yes - direct notification |
| Business owners | May need to sign risk acceptances | Yes - leadership briefing |
| Engineering teams | Prioritize remediation work | Yes - planning input |
| GRC team | Tracking and administration | Yes - process training |

### Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Teams miss deadlines | Medium | Medium | Automated reminders, escalation |
| Risk acceptances proliferate | Low | Medium | Leadership visibility, limit total |
| Remediation deprioritized | Medium | Medium | Security in sprint planning |

### Resource Requirements

| Resource | Amount | Source |
|----------|--------|--------|
| GRC administration | 4 hours/week ongoing | GRC team |
| Exception remediation | Varies by exception | Engineering teams |
| Risk acceptance reviews | 2-3 hours each | Security + Business |

---

## Exceptions to This Policy

### Can This Policy Have Exceptions?

Yes, but only for:

| Scenario | Approval Required | Maximum Duration |
|----------|-------------------|------------------|
| Vendor dependency (documented) | Security Lead + CTO | Until vendor resolves |
| Regulatory constraint | Security Lead + Legal | Until regulation changes |
| System decommission planned | Security Lead | Until decommission (max 6 months) |

All meta-exceptions require quarterly review.

---

## Success Criteria

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Exceptions > 90 days old | < 10 | Exception tracker |
| Exceptions > 360 days old | 0 | Exception tracker |
| Average exception age | < 60 days | Exception tracker |
| Renewal-to-remediation ratio | > 50% remediated | Exception tracker |
| Risk acceptances from exceptions | < 5 per year | GRC tracking |

---

## Enforcement

### Automated Controls

1. **Reminder at day 75** - Email to exception owner
2. **Reminder at day 85** - Email to owner + manager
3. **Day 90** - Exception expires, escalation to Security Lead
4. **Expired exceptions** - Flagged in compliance dashboard

### Governance Controls

1. **Weekly exception review** - Security team reviews expiring exceptions
2. **Monthly report** - Exception metrics to leadership
3. **Quarterly audit** - Verify all exceptions compliant

### Consequences

| Situation | Consequence |
|-----------|-------------|
| Exception expires without renewal | System flagged non-compliant, escalation |
| Renewal without progress | Renewal denied, escalation |
| Repeated renewals without progress | Mandatory risk acceptance or remediation |

---

## Review and Governance

### Review Schedule

| Review Type | Frequency | Next Review |
|-------------|-----------|-------------|
| Policy effectiveness | Quarterly | 2025-02-15 |
| Exception metrics | Monthly | Ongoing |
| Policy update | Annually | 2025-11-15 |

### Change Process

Changes require Security Lead approval. Significant changes (timeline adjustments) require CTO approval.

---

## Approvals

### Consulted

| Name | Role | Date | Feedback |
|------|------|------|----------|
| [GRC Lead] | GRC Lead | 2024-11-10 | Process confirmed feasible |
| [Eng Directors] | Engineering Directors | 2024-11-12 | Timelines agreed with input |
| [Legal] | Legal Counsel | 2024-11-13 | Risk acceptance language approved |

### Approved By

| Name | Role | Date |
|------|------|------|
| [CTO] | CTO | 2024-11-15 |
| [Security Lead] | Security Lead | 2024-11-15 |

---

## References

- Exception request template
- Risk acceptance template
- ISO 27001 clause 6.1.3 (Risk treatment)
- SOC 2 CC3.2 (Risk management)
