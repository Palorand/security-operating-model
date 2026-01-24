# Security Operating Model and RACI

This document defines how the security function operates and interfaces with the rest of the organization.

---

## Operating Model Overview

Security operates as an **enabling function** that:

1. **Sets standards** - Defines security requirements and acceptable risk levels
2. **Provides tools** - Builds or procures security capabilities for teams to use
3. **Reviews and advises** - Evaluates designs and provides guidance
4. **Monitors and responds** - Detects threats and coordinates incident response
5. **Reports and governs** - Measures security posture and enforces accountability

Security does **not**:

- Own application security for every team (teams own their security)
- Block deployments indefinitely (we find solutions)
- Make business decisions (we inform, business decides)

---

## Team Structure

### Security Engineering

**Mission:** Build and operate security technical capabilities.

**Responsibilities:**
- Security tooling (SAST, DAST, SCA, secrets scanning)
- Detection engineering and SIEM management
- Vulnerability management operations
- Security architecture guidance
- Incident response (technical)

**Interfaces with:** Engineering teams, Platform/SRE, IT

### Governance, Risk, and Compliance (GRC)

**Mission:** Manage security risk and compliance obligations.

**Responsibilities:**
- Risk assessment and register management
- Policy and standards development
- Compliance program management (SOC 2, ISO 27001, etc.)
- Vendor security assessments
- Exception and risk acceptance processing
- Audit coordination

**Interfaces with:** Legal, Finance, Procurement, External auditors

### Security Operations (if separate)

**Mission:** Monitor, detect, and respond to security threats.

**Responsibilities:**
- Alert triage and investigation
- Incident response coordination
- Threat intelligence integration
- Security monitoring 24/7 (or on-call)

**Interfaces with:** Engineering teams, IT, SRE

---

## RACI Matrix

### Legend

- **R** = Responsible (does the work)
- **A** = Accountable (final decision authority)
- **C** = Consulted (provides input)
- **I** = Informed (kept updated)

### Security Activities

| Activity | Product | Engineering | SRE/Platform | Security Eng | GRC | IT |
|----------|---------|-------------|--------------|--------------|-----|-----|
| Define security requirements | C | C | C | R | A | I |
| Threat modeling | C | R | C | A | I | I |
| Secure code development | I | R/A | I | C | I | I |
| Security code review | I | R | I | A | I | I |
| Vulnerability remediation | I | R/A | R | C | I | I |
| Security testing (SAST/DAST) | I | C | C | R/A | I | I |
| Infrastructure hardening | I | C | R/A | C | I | I |
| Access management | C | C | R | C | A | R |
| Incident response | I | R | R | A | C | R |
| Risk assessment | C | C | C | C | R/A | C |
| Compliance evidence | I | R | R | R | A | R |
| Vendor security assessment | C | I | I | C | R/A | C |
| Security awareness training | I | I | I | C | R/A | R |
| Policy approval | I | C | C | C | R | C |

### Security Processes

| Process | Owner (A) | Executor (R) | Consulted | Informed |
|---------|-----------|--------------|-----------|----------|
| Security review for new projects | Security Lead | Security Eng | Engineering | Product |
| Exception requests | GRC | Requestor | Security Eng | Leadership |
| Risk acceptance | Business Owner | GRC | Security | Leadership |
| Vulnerability triage | Security Eng | Security Eng | Engineering | GRC |
| Incident declaration | Security Lead | Security Ops | SRE | Leadership |
| Postmortem review | Security Lead | Incident team | All involved | Leadership |
| Access review | GRC | System owners | Security | Compliance |
| Penetration test | Security Lead | External vendor | Engineering | Leadership |

---

## Interaction Model

### With Engineering Teams

```
Engineering Team                    Security
      |                                |
      |-- New project kickoff -------->|
      |<-- Security review scheduled --|
      |                                |
      |-- Design doc shared ---------->|
      |<-- Security feedback ----------|
      |                                |
      |-- Implementation begins -------|
      |<-- Automated scanning runs ----|
      |                                |
      |-- Findings addressed ----------|
      |<-- Review sign-off ------------|
      |                                |
      |-- Deploy to production --------|
      |<-- Monitoring active ----------|
```

### With Product Teams

| Touchpoint | Purpose | Timing |
|------------|---------|--------|
| Roadmap planning | Identify security implications of new features | Quarterly |
| Feature kickoff | Security requirements for specific features | Per feature |
| Launch review | Verify security readiness | Pre-launch |
| Incident communication | Coordinate customer-facing response | As needed |

### With Leadership

| Touchpoint | Purpose | Frequency |
|------------|---------|-----------|
| Security metrics review | Report on KPIs and trends | Monthly |
| Risk review | Discuss top risks and treatment | Quarterly |
| Incident briefings | Report on significant incidents | As needed |
| Budget planning | Resource and tool requests | Annually |

---

## Operating Rhythms

### Daily

| Activity | Participants | Purpose |
|----------|--------------|---------|
| Security standup | Security team | Coordinate daily work |
| Alert triage | Security Ops | Review overnight alerts |
| Vulnerability review | Security Eng | Triage new findings |

### Weekly

| Activity | Participants | Purpose |
|----------|--------------|---------|
| Security-Engineering sync | Security Lead + Eng Leads | Discuss current issues, upcoming work |
| Threat intel review | Security team | Review relevant threat intelligence |
| Metrics review | Security team | Check KPI trends |

### Monthly

| Activity | Participants | Purpose |
|----------|--------------|---------|
| Security report | Security Lead -> Leadership | Report on security posture |
| Risk register review | Security + GRC | Update risk status |
| Security champions sync | Security + Champions | Knowledge sharing, feedback |

### Quarterly

| Activity | Participants | Purpose |
|----------|--------------|---------|
| Roadmap review | Security + Leadership | Review progress, adjust priorities |
| Access review | GRC + System owners | Verify access appropriateness |
| Tabletop exercise | Security + stakeholders | Test incident response |
| Vendor review | GRC | Assess third-party risks |

### Annually

| Activity | Participants | Purpose |
|----------|--------------|---------|
| Risk assessment | All stakeholders | Comprehensive risk evaluation |
| Policy review | Security + Legal | Update security policies |
| Penetration test | External + Security | External validation |
| Security strategy | Security + Leadership | Set annual direction |

---

## Escalation Paths

### Technical Escalation

```
Security Analyst
      |
      v
Security Engineer (on-call)
      |
      v
Security Lead
      |
      v
CISO / CTO
```

### Business Escalation

```
Security finding/request
      |
      v
Team Lead discussion
      |
      v
Engineering Director (if cross-team)
      |
      v
CTO (if company-wide impact)
      |
      v
CEO (if customer/regulatory impact)
```

### Incident Escalation

See [10-incident-operating-loop.md](10-incident-operating-loop.md) for incident-specific escalation.

---

## Decision Rights

| Decision | Authority | Input Required |
|----------|-----------|----------------|
| Security tool selection | Security Lead | Engineering feedback |
| Vulnerability severity override | Security Eng Lead | Risk assessment |
| Exception approval (< 30 days) | Security Lead | Risk assessment |
| Exception approval (> 30 days) | Business Owner + Security | GRC review |
| Risk acceptance | Business Owner | Security recommendation |
| Policy creation/update | Security Lead | Legal review |
| Incident severity declaration | Security Lead | Incident team input |
| Breach notification | Legal + Security Lead | Executive approval |

---

## Service Level Expectations

### From Security to Organization

| Service | SLA |
|---------|-----|
| Security review for new projects | Scheduled within 5 business days |
| Security review completion | 10 business days (standard), 2 days (expedited) |
| Exception request response | 3 business days |
| Vulnerability triage | 1 business day |
| Incident response (P1) | 1 hour |
| Security questions/consultations | 2 business days |

### From Organization to Security

| Expectation | Standard |
|-------------|----------|
| Security review lead time | Request 10+ days before needed |
| Vulnerability remediation | Per SLA by severity |
| Incident participation | Immediate when requested |
| Access review completion | Within 5 business days of request |
| Evidence provision for audits | Within 10 business days |
