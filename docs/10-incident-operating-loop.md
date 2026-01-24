# Incident Response Operating Loop

This document defines the incident response process from detection through postmortem.

---

## Incident Definition

A security incident is any event that:

- Compromises confidentiality, integrity, or availability of systems or data
- Violates security policy
- Indicates malicious activity or unauthorized access
- Requires coordinated response beyond normal operations

**Not incidents** (handled through normal processes):
- Vulnerability discoveries without exploitation
- Policy violations without security impact
- System outages without security cause
- Phishing emails that were not clicked

---

## Severity Levels

| Severity | Definition | Examples | Response Time |
|----------|------------|----------|---------------|
| **P1 - Critical** | Active breach, significant data exposure, or major service impact | Data exfiltration confirmed, ransomware active, production compromise | Immediate (< 15 min) |
| **P2 - High** | Likely breach, limited exposure, or potential for escalation | Suspicious admin access, malware detected, credential compromise | < 1 hour |
| **P3 - Medium** | Suspicious activity requiring investigation, no confirmed impact | Failed attack attempts, policy violations, anomalous behavior | < 4 hours |
| **P4 - Low** | Minor security events, informational | Blocked attacks, minor policy deviations | Next business day |

---

## Roles and Responsibilities

### Incident Commander (IC)

**Who:** Security Lead or designated on-call

**Responsibilities:**
- Owns the incident end-to-end
- Makes decisions on response actions
- Coordinates resources and communication
- Escalates to leadership when needed
- Ensures postmortem is completed

### Technical Lead

**Who:** Senior engineer with relevant system expertise

**Responsibilities:**
- Leads technical investigation
- Directs containment and eradication
- Coordinates with system owners
- Documents technical timeline

### Communications Lead

**Who:** Security or designated communications person

**Responsibilities:**
- Manages internal communications
- Coordinates external communications (if needed)
- Keeps stakeholders updated
- Documents communications sent

### Scribe

**Who:** Any team member

**Responsibilities:**
- Documents timeline of events
- Records decisions made
- Tracks action items
- Maintains incident log

---

## Incident Response Phases

### 1. Detection

**Goal:** Identify that a security incident has occurred.

**Sources:**
- Security monitoring and alerts
- Employee reports
- Third-party notifications
- Customer reports
- Automated scanning findings

**Actions:**
- [ ] Acknowledge alert or report
- [ ] Perform initial assessment
- [ ] Determine if this is a security incident
- [ ] Assign initial severity
- [ ] Create incident ticket/channel

### 2. Triage

**Goal:** Understand scope and determine response level.

**Actions:**
- [ ] Gather initial facts (what, when, where, how)
- [ ] Identify affected systems and data
- [ ] Assess potential impact
- [ ] Confirm or adjust severity
- [ ] Activate appropriate response team
- [ ] Notify stakeholders per severity

**Triage Questions:**
- What systems are affected?
- What data may be exposed?
- Is the attack ongoing?
- What is the blast radius?
- Do we need external help?

### 3. Containment

**Goal:** Stop the incident from spreading or causing additional damage.

**Short-term containment:**
- [ ] Isolate affected systems
- [ ] Block malicious IPs/accounts
- [ ] Disable compromised credentials
- [ ] Preserve evidence before changes

**Long-term containment:**
- [ ] Implement temporary controls
- [ ] Apply emergency patches if available
- [ ] Enhance monitoring on affected areas
- [ ] Prepare for eradication

**Decision Point:** Is the situation stable enough to proceed to eradication?

### 4. Eradication

**Goal:** Remove the threat from the environment.

**Actions:**
- [ ] Identify root cause
- [ ] Remove malware/backdoors
- [ ] Close vulnerability exploited
- [ ] Reset compromised credentials
- [ ] Verify threat is eliminated
- [ ] Document what was removed

**Verification:**
- Scan systems for indicators of compromise
- Review logs for continued malicious activity
- Confirm all entry points are closed

### 5. Recovery

**Goal:** Restore normal operations safely.

**Actions:**
- [ ] Restore systems from clean backups (if needed)
- [ ] Bring systems back online gradually
- [ ] Verify systems function correctly
- [ ] Monitor closely for recurrence
- [ ] Confirm with system owners

**Recovery Criteria:**
- No signs of ongoing compromise
- Systems functioning normally
- Monitoring in place for related activity
- Stakeholders informed of restoration

### 6. Post-Incident

**Goal:** Learn from the incident and improve defenses.

**Actions:**
- [ ] Complete incident documentation
- [ ] Conduct postmortem meeting
- [ ] Identify lessons learned
- [ ] Create action items for improvements
- [ ] Update detection and response procedures
- [ ] Close incident ticket

---

## Communication

### Internal Communication

| Severity | Notify Immediately | Update Frequency |
|----------|-------------------|------------------|
| P1 | CEO, CTO, Legal, affected VPs | Every 30 minutes until stable |
| P2 | CTO, Security Lead, affected directors | Every 2 hours until stable |
| P3 | Security Lead, affected managers | Daily until resolved |
| P4 | Security team | As needed |

### Communication Templates

**Initial notification:**
```
SECURITY INCIDENT - [Severity]

Summary: [One sentence description]
Status: [Investigating / Containing / Recovering]
Impact: [Known or potential impact]
Actions: [What we're doing]
Next update: [Time]

Please direct questions to [IC name].
```

**Status update:**
```
INCIDENT UPDATE - [Incident ID]

Status: [Current phase]
Progress: [What's been done]
Findings: [What we've learned]
Next steps: [What's happening next]
Next update: [Time]
```

### External Communication

External communication (customers, regulators, public) requires:

1. Legal review before any external statement
2. Executive approval
3. Coordination with PR/Communications
4. Documented approval chain

**Do not** communicate externally without explicit approval.

---

## Evidence Handling

### Preservation Priorities

1. Volatile data (memory, running processes)
2. Logs (before rotation)
3. Disk images (before remediation)
4. Network captures (if available)
5. Configuration files

### Evidence Rules

- **Do not** modify evidence systems unnecessarily
- **Document** all actions taken on evidence systems
- **Preserve** original data; work from copies
- **Maintain** chain of custody documentation
- **Secure** evidence from unauthorized access

### Chain of Custody

For each piece of evidence, document:
- What it is
- Where it was collected from
- When it was collected
- Who collected it
- How it was stored
- Who has accessed it

---

## Escalation Criteria

### Escalate to Leadership

- Confirmed data breach involving customer data
- Regulatory notification may be required
- Incident requires public statement
- Significant financial impact
- Law enforcement involvement needed
- Attack attributed to nation-state or organized crime

### Escalate to Legal

- Any confirmed data breach
- Potential regulatory implications
- Law enforcement contact
- Third-party involvement (vendors, partners)
- Litigation risk

### Escalate to External Resources

- Incident beyond internal capabilities
- Forensic analysis required
- Legal hold or e-discovery needs
- Specialized threat intelligence needed

---

## Postmortem Process

### Timeline

- **P1/P2:** Postmortem within 5 business days of resolution
- **P3/P4:** Postmortem within 10 business days (if warranted)

### Postmortem Meeting

**Duration:** 60-90 minutes

**Attendees:** IC, Technical Lead, affected system owners, Security

**Agenda:**
1. Incident timeline review (15 min)
2. Root cause analysis (20 min)
3. What went well (10 min)
4. What could be improved (20 min)
5. Action items (15 min)

### Postmortem Document

Include:
- Incident summary
- Timeline of events
- Root cause analysis
- Impact assessment
- What went well
- What could be improved
- Action items with owners and due dates

### Blameless Culture

Postmortems focus on:
- Systems and processes, not individuals
- Understanding, not blame
- Improvement, not punishment

We assume people acted with best intentions given available information.

---

## On-Call and Availability

### On-Call Rotation

- Security maintains 24/7 on-call coverage
- On-call rotates weekly
- Primary and secondary on-call defined
- Escalation path documented

### Response Expectations

| Time | Expectation |
|------|-------------|
| Business hours | Immediate response |
| After hours (P1/P2) | Response within 15 minutes |
| After hours (P3/P4) | Response next business day |

### On-Call Tools

- PagerDuty (or equivalent) for alerting
- Slack incident channel for coordination
- Incident management system for tracking
- Runbooks for common scenarios

---

## Metrics

| Metric | Target |
|--------|--------|
| Mean time to detect (MTTD) | < 24 hours |
| Mean time to respond (MTTR) | P1: < 15 min, P2: < 1 hour |
| Mean time to contain | < 4 hours for P1/P2 |
| Postmortem completion rate | 100% for P1/P2 |
| Action item completion rate | > 90% within 30 days |

---

## Annual Testing

- **Tabletop exercise:** Quarterly, rotating scenarios
- **Technical drill:** Semi-annually, realistic simulation
- **Full exercise:** Annually, cross-functional with leadership

Each exercise produces findings that feed into process improvements.
