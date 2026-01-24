# Decision Memo: Deny Public Exposure by Default

## Document Information

| Field | Value |
|-------|-------|
| Decision ID | DM-001 |
| Title | Deny Public Exposure by Default |
| Author | Security Lead |
| Date | 2025-10-15 |
| Status | Approved |

---

## Executive Summary

All internal services, databases, storage buckets, and infrastructure components are denied public internet exposure by default. Any public exposure requires explicit security review and approval, with compensating controls documented and monitored.

---

## Context

### Background

As the organization has grown, we've seen multiple instances of accidental public exposure:
- Development databases temporarily exposed during testing
- S3 buckets made public for "quick" file sharing
- Internal APIs exposed without authentication for partner integrations
- Debug endpoints left enabled in production

Each incident required emergency response and created unnecessary risk.

### Current State

Before this decision:
- No consistent policy on public exposure
- Teams made case-by-case decisions
- Cloud security posture monitoring flagged issues after the fact
- No formal approval process for intentional public exposure

### Trigger

A staging database containing customer PII was exposed to the internet for 72 hours before detection. While no unauthorized access was confirmed, this incident highlighted the need for a clear policy and preventive controls.

---

## Decision

### Statement

**All services, APIs, databases, storage, and infrastructure are denied public internet exposure by default.** Public exposure is permitted only after completing a security review and implementing required controls.

### Scope

| Attribute | Value |
|-----------|-------|
| Applies to | All environments (production, staging, development) |
| Effective date | 2025-11-01 |
| Review date | 2025-11-01 |

---

## Options Considered

### Option 1: Documentation and Training Only

**Description:** Publish guidelines on secure exposure and rely on training.

| Pros | Cons |
|------|------|
| Low implementation effort | Relies on human compliance |
| No workflow changes | Doesn't prevent mistakes |
| | Reactive rather than preventive |

**Estimated effort:** Low

### Option 2: Monitoring and Alerting Only

**Description:** Implement CSPM alerts for public exposure, respond reactively.

| Pros | Cons |
|------|------|
| Catches issues quickly | Still allows exposure to occur |
| Visibility into current state | Response time creates risk window |
| | Alert fatigue risk |

**Estimated effort:** Medium

### Option 3: Policy-as-Code with Preventive Controls (Selected)

**Description:** Implement guardrails that block public exposure by default, with a formal exception process for legitimate needs.

| Pros | Cons |
|------|------|
| Prevents accidental exposure | Requires workflow change |
| Clear process for legitimate needs | Initial implementation effort |
| Auditable and consistent | May slow down some legitimate work |
| Defense in depth with monitoring |  |

**Estimated effort:** Medium

---

## Rationale

### Why This Option?

Preventive controls are more effective than detective controls for high-impact risks. The potential damage from accidental public exposure (data breach, regulatory fines, reputation damage) far outweighs the friction of a review process.

This approach:
1. Makes the secure path the default path
2. Creates a clear process for legitimate exceptions
3. Provides audit trail for compliance
4. Reduces incident response burden

### Key Factors

| Factor | Weight | How Selected Option Performs |
|--------|--------|------------------------------|
| Risk reduction | High | Prevents exposure vs. detecting it |
| Operational impact | Medium | Manageable with clear process |
| Compliance alignment | High | Supports ISO 27001, SOC 2 requirements |
| Implementation feasibility | Medium | Achievable with existing tools |

### Trade-offs Accepted

- Legitimate public exposure takes longer (requires review)
- Some developer friction for edge cases
- Maintenance burden for policy-as-code rules

---

## Implementation

### Requirements

1. **Cloud guardrails** - Implement SCPs/Organization Policies blocking:
   - Public S3 buckets
   - Security groups allowing 0.0.0.0/0 ingress
   - Public RDS/database instances
   - Public EKS/GKE endpoints

2. **Network architecture** - Establish patterns for:
   - Public-facing services (load balancers, CDN)
   - Private services (everything else)
   - Approved ingress points only

3. **Exception process** - Security review required for:
   - Any intentional public exposure
   - Minimum controls documented
   - Time-limited approval where possible

4. **Monitoring** - CSPM scanning for:
   - Policy violations
   - Drift from approved state
   - Alerting on any public exposure

### Timeline

| Milestone | Target Date | Owner |
|-----------|-------------|-------|
| Policy published | 2025-10-20 | Security Lead |
| Cloud guardrails deployed | 2025-11-01 | Cloud Platform |
| Exception process operational | 2025-11-01 | Security |
| CSPM alerting configured | 2025-11-15 | Security Engineering |
| Existing exceptions reviewed | 2025-12-01 | Security + Teams |

### Dependencies

| Dependency | Status | Impact if Delayed |
|------------|--------|-------------------|
| Cloud Platform team capacity | Confirmed | Guardrails delayed |
| CSPM tool deployed | Complete | Monitoring delayed |

---

## Impact Assessment

### Affected Stakeholders

| Stakeholder | Impact | Communication Needed |
|-------------|--------|---------------------|
| Engineering teams | New process for public exposure | Yes - all-hands + documentation |
| Platform team | Implement and maintain guardrails | Yes - direct coordination |
| Product teams | May affect some feature timelines | Yes - advance notice |

### Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Blocks legitimate work | Medium | Medium | Clear exception process, fast-track for urgent needs |
| Guardrails have gaps | Low | High | Defense in depth with monitoring |
| Teams bypass controls | Low | High | Audit logging, culture building |

### Resource Requirements

| Resource | Amount | Source |
|----------|--------|--------|
| Platform engineering | 2 weeks | Platform team |
| Security engineering | 1 week | Security team |
| Documentation | 3 days | Security team |

---

## Exceptions

### Exception Process

1. Submit security review request with business justification
2. Security assesses risk and required controls
3. If approved, document compensating controls:
   - WAF/DDoS protection
   - Authentication requirements
   - Monitoring and alerting
   - Data exposure minimization
4. Implement controls before exposure
5. Security verifies and approves
6. Ongoing monitoring and annual review

### Pre-Approved Exceptions

| Exception | Conditions | Approval |
|-----------|------------|----------|
| Public website/marketing | Static content only, no customer data, CDN/WAF required | Standing approval |
| Public API (documented) | Authentication required, rate limiting, WAF, security review complete | Per-service approval |

---

## Success Criteria

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Accidental public exposure incidents | 0 | Incident tracking |
| Policy violation alerts | Trending to 0 | CSPM dashboard |
| Exception review completion time | <5 business days | Review tracker |
| Compliant public services | 100% | Quarterly audit |

---

## Enforcement

### Technical Controls

- SCPs block public S3 bucket creation
- Organization policies block public IP assignment without approval tag
- Network policies deny internet ingress by default
- CI/CD scanning blocks infrastructure with public exposure

### Governance Controls

- Quarterly review of all public-facing services
- Annual re-certification of exceptions
- Violation tracking and escalation

### Consequences of Violation

1. First violation: Immediate remediation, incident review
2. Repeat violations: Escalation to engineering leadership
3. Pattern of violations: Process review and additional controls

---

## Review and Governance

### Review Schedule

| Review Type | Frequency | Next Review |
|-------------|-----------|-------------|
| Policy effectiveness | Quarterly | 2025-01-15 |
| Exception review | Annually | 2025-10-15 |
| Technical controls audit | Semi-annually | 2025-04-15 |

### Change Process

Changes to this policy require:
1. Security Lead proposal
2. Engineering leadership review
3. Documented rationale
4. Updated technical controls

---

## Approvals

### Consulted

| Name | Role | Date | Feedback |
|------|------|------|----------|
| [CTO] | CTO | 2025-10-10 | Supportive, requested clear exception process |
| [Eng Director] | Engineering Director | 2025-10-12 | Concerns addressed re: developer experience |
| [Platform Lead] | Platform Lead | 2025-10-12 | Implementation plan confirmed |

### Approved By

| Name | Role | Date |
|------|------|------|
| [CTO] | CTO | 2025-10-15 |
| [Security Lead] | Security Lead | 2025-10-15 |

---

## References

- Cloud security posture management runbook
- Security review process documentation
- Incident report: Staging database exposure (2025-09)
