# North Star and Security Principles

This document defines the security mission and the non-negotiable principles that guide all security decisions.

---

## North Star Statement

> **Enable the business to move fast without creating unacceptable risk to customers, data, or operations.**

Security exists to protect value, not to block progress. Every control should tie back to a specific risk, and every risk should tie back to business impact.

---

## Security Mission

Protect the confidentiality, integrity, and availability of:

1. **Customer data** - The trust customers place in us by sharing their information
2. **Business operations** - The systems and processes that generate revenue
3. **Intellectual property** - The code, designs, and knowledge that differentiate us
4. **Employee safety** - The privacy and security of our workforce

In that order. When priorities conflict, this hierarchy guides decisions.

---

## Core Principles

### 1. Default Deny

Access to systems, data, and networks is denied by default. Every permission requires explicit justification and approval.

**In practice:**
- No public exposure of internal services without security review
- No broad IAM permissions; scope to minimum required
- Network segmentation with explicit allow rules only

**We will not:** Grant "just in case" access or convenience permissions.

### 2. Defense in Depth

No single control is sufficient. Multiple layers ensure that if one fails, others still protect.

**In practice:**
- Authentication AND authorization AND audit logging
- Network controls AND application controls AND data controls
- Prevention AND detection AND response capability

**We will not:** Rely on a single control, no matter how strong it appears.

### 3. Shift Left, But Not Exclusively

Security should be involved early in design, but production monitoring remains essential.

**In practice:**
- Security design reviews before implementation begins
- Automated scanning in CI/CD pipelines
- Runtime detection and monitoring in production

**We will not:** Assume that pre-production security eliminates the need for production monitoring.

### 4. Risk-Based Prioritization

Resources are finite. We address the highest risks first, not the easiest or most visible.

**In practice:**
- Risk scoring drives remediation priority
- Accept that some risks will remain temporarily open
- Focus on exploitability and impact, not just vulnerability counts

**We will not:** Chase low-risk findings while high-risk issues remain open.

### 5. Business Ownership of Risk

Security identifies and quantifies risk. The business decides acceptable risk levels.

**In practice:**
- Risk acceptance requires business stakeholder sign-off
- Security provides recommendations, not mandates
- Accountability for risk decisions sits with business owners

**We will not:** Make business decisions unilaterally or accept risk on behalf of the business.

### 6. Automate Enforcement

Manual processes fail. Policy should be enforced through automation wherever possible.

**In practice:**
- Policy-as-code in CI/CD pipelines
- Automated compliance scanning and alerting
- Infrastructure guardrails that prevent misconfiguration

**We will not:** Rely on documentation or training alone to enforce policy.

### 7. Assume Breach

Design systems assuming attackers will eventually get in. Focus on detection, containment, and limiting blast radius.

**In practice:**
- Comprehensive audit logging for forensics
- Network segmentation to contain lateral movement
- Incident response plans tested regularly

**We will not:** Assume perimeter defenses are sufficient or that prevention alone is enough.

### 8. Transparency Over Security Theater

Real security requires honest assessment, not impressive-looking but ineffective controls.

**In practice:**
- Report actual metrics, including failures
- Acknowledge gaps and track remediation
- Avoid checkbox compliance without real protection

**We will not:** Implement controls that look good but don't reduce risk.

---

## What We Will Not Do

Explicit refusals are as important as commitments. We will not:

| Refusal | Rationale |
|---------|-----------|
| Block deployments indefinitely | Security is not a veto; we find solutions |
| Accept compliance as sufficient | Passing audits doesn't mean being secure |
| Implement security by obscurity | Assume attackers know everything we know |
| Skip security for "urgent" releases | Urgency is not an excuse; we have fast-path processes |
| Store secrets in code or config | No exceptions, ever |
| Grant permanent elevated access | All privileged access is time-limited |

---

## Conditional Accepts

Some requests we'll approve with conditions:

| Request | Conditions |
|---------|------------|
| Public exposure of a service | Security review completed, WAF in place, monitoring enabled |
| Third-party integration | Vendor security assessment passed, data classification approved |
| Exception to a control | Compensating controls documented, time-boxed, business owner sign-off |
| Access to production data | Justified business need, audit logging, data minimization applied |
| Use of new technology | Threat model completed, secure defaults configured |

---

## How Principles Guide Decisions

When faced with a decision, apply principles in this order:

1. **Does this create unacceptable risk to customers?** If yes, stop.
2. **Can we implement defense in depth?** If not, what compensating controls exist?
3. **Can we automate enforcement?** If not, what's the manual process and how do we verify it?
4. **Is there business ownership?** Who is accountable for this risk?
5. **How do we detect failure?** What monitoring tells us if this breaks?

---

## Updating These Principles

Principles are not immutable. They should be reviewed annually or when:

- A significant incident reveals a gap
- Business context changes materially
- New threats emerge that aren't addressed

Changes require security leadership approval and communication to all stakeholders.
