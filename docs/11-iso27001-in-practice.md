# ISO 27001 in Practice

This document describes how we implement ISO 27001 as a practical security management system, not a compliance checkbox exercise.

---

## Philosophy

ISO 27001 is a framework for managing information security, not a list of controls to implement. The goal is:

1. **Risk-driven:** Controls address identified risks, not just Annex A checkboxes
2. **Evidence-based:** Claims are backed by verifiable evidence
3. **Continuously improving:** Regular review and improvement cycles
4. **Integrated:** Security management embedded in business processes

We use ISO 27001 as a structure for good security practice, not as an end in itself.

---

## Information Security Management System (ISMS)

### Scope

The ISMS covers:

- Production systems and infrastructure
- Customer data processing
- Corporate IT systems
- Employee access and devices
- Third-party services processing company data

**Out of scope:**
- Personal devices not accessing company data
- Publicly available information
- Physical office security (covered separately if applicable)

### ISMS Documentation Structure

```
Policies (What we commit to)
    |
    v
Standards (Specific requirements)
    |
    v
Procedures (How to do it)
    |
    v
Evidence (Proof it's done)
```

---

## Key ISO 27001 Clauses

### Clause 4: Context of the Organization

**Requirement:** Understand the organization and its context.

**Our implementation:**
- Business context documented in [01-north-star-and-principles.md](01-north-star-and-principles.md)
- Interested parties: customers, employees, regulators, partners
- Scope statement maintained and reviewed annually

**Evidence:**
- ISMS scope document
- Interested parties register
- Annual context review records

### Clause 5: Leadership

**Requirement:** Top management commitment and security policy.

**Our implementation:**
- Security principles endorsed by leadership
- Security Lead has direct access to executive team
- Security discussed in leadership meetings quarterly
- Resources allocated for security program

**Evidence:**
- Leadership meeting minutes
- Budget allocation records
- Security policy signed by CEO

### Clause 6: Planning

**Requirement:** Risk assessment and treatment planning.

**Our implementation:**
- Risk framework defined in [03-risk-prioritization.md](03-risk-prioritization.md)
- Risk register maintained with regular reviews
- Treatment plans tracked to completion
- Security objectives aligned with business objectives

**Evidence:**
- Risk register
- Risk assessment records
- Treatment plan status reports
- Security roadmap

### Clause 7: Support

**Requirement:** Resources, competence, awareness, communication, documented information.

**Our implementation:**
- Security team resourced per roadmap
- Security training for all employees
- Security awareness program
- Documentation maintained in version control
- Communication channels established

**Evidence:**
- Training completion records
- Awareness campaign materials
- Document control logs
- Communication records

### Clause 8: Operation

**Requirement:** Operational planning and control, risk assessment, risk treatment.

**Our implementation:**
- Security review process for changes
- Vulnerability management program
- Incident response procedures
- Third-party risk management

**Evidence:**
- Security review records
- Vulnerability scan reports
- Incident records
- Vendor assessment records

### Clause 9: Performance Evaluation

**Requirement:** Monitoring, measurement, analysis, evaluation, internal audit, management review.

**Our implementation:**
- Security KPIs defined in [06-kpis-and-metrics.md](06-kpis-and-metrics.md)
- Monthly security reporting
- Annual internal audit
- Quarterly management review

**Evidence:**
- Security dashboards and reports
- Internal audit reports
- Management review minutes

### Clause 10: Improvement

**Requirement:** Nonconformity, corrective action, continual improvement.

**Our implementation:**
- Incident postmortems drive improvements
- Audit findings tracked to closure
- Continuous improvement backlog maintained
- Annual program retrospective

**Evidence:**
- Postmortem records
- Corrective action tracker
- Improvement initiative records

---

## Annex A Control Mapping

Annex A provides a reference set of controls. We map these to our actual implementations.

See [mapping/iso27001-annexA-to-controls.md](../mapping/iso27001-annexA-to-controls.md) for the complete mapping.

### Mapping Approach

For each Annex A control:

| Field | Description |
|-------|-------------|
| Control ID | ISO 27001:2022 reference |
| Control Name | Control description |
| Applicability | Applicable / Not Applicable (with justification) |
| Implementation | How we implement this control |
| Evidence | Where to find proof |
| Owner | Who is responsible |
| Automation Level | Automated / Semi-automated / Manual |

### Sample Mappings

**A.5.15 - Access Control**

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Role-based access control via Okta, least privilege enforced, quarterly access reviews |
| Evidence | Okta configuration, access review records, IAM policies |
| Owner | IT / Security |
| Automation | Semi-automated (provisioning automated, reviews manual) |

**A.8.9 - Configuration Management**

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Infrastructure as Code (Terraform), CSPM scanning, baseline configurations |
| Evidence | Terraform repos, CSPM scan reports, baseline documents |
| Owner | Platform Engineering |
| Automation | Automated (IaC with policy-as-code gates) |

**A.8.16 - Monitoring Activities**

| Field | Value |
|-------|-------|
| Applicability | Applicable |
| Implementation | Centralized logging (SIEM), security alerts, CloudTrail for AWS |
| Evidence | SIEM dashboards, alert configurations, log retention policies |
| Owner | Security Engineering |
| Automation | Automated (real-time monitoring and alerting) |

---

## Statement of Applicability (SoA)

The Statement of Applicability documents:

1. All Annex A controls considered
2. Which controls are applicable and why
3. Which controls are not applicable and justification
4. Implementation status for applicable controls

The SoA is:
- Reviewed annually
- Updated when scope or controls change
- Approved by Security Lead
- Available for audit

---

## Evidence Management

### Types of Evidence

| Type | Examples | Retention |
|------|----------|-----------|
| Policies | Approved policy documents | Current + 1 version |
| Procedures | How-to documents, runbooks | Current + 1 version |
| Records | Logs, reports, meeting minutes | Per retention schedule |
| Configurations | System settings, IaC code | Version controlled |
| Assessments | Risk assessments, audits | 3 years |

### Evidence Collection

**Automated evidence** (preferred):
- System configurations exported automatically
- Scan reports generated on schedule
- Logs aggregated continuously
- Metrics dashboards always current

**Manual evidence:**
- Meeting minutes documented within 48 hours
- Reviews recorded when completed
- Training tracked in LMS
- Exceptions logged when processed

### Evidence Repository

Evidence stored in:
- Version-controlled documentation (policies, procedures)
- GRC platform (assessments, exceptions, audits)
- Log aggregation system (operational records)
- Ticketing system (incidents, changes, reviews)

---

## Audit Preparation

### Internal Audit

**Frequency:** Annual, plus ad-hoc as needed

**Scope:** Full ISMS or focused on specific areas

**Process:**
1. Audit plan developed
2. Evidence requests sent to owners
3. Control testing performed
4. Findings documented
5. Corrective actions assigned
6. Follow-up on remediation

**Output:** Internal audit report with findings and recommendations

### External Audit (Certification)

**Stage 1 (Documentation Review):**
- ISMS documentation review
- Scope confirmation
- Readiness assessment

**Stage 2 (Implementation Audit):**
- Evidence review
- Interviews with personnel
- Control testing
- Finding issuance

**Surveillance Audits (Annual):**
- Subset of controls reviewed
- Verify continued compliance
- Review changes since last audit

### Audit Readiness Checklist

- [ ] SoA current and approved
- [ ] Risk register updated within last 6 months
- [ ] Management review conducted within last 12 months
- [ ] Internal audit completed
- [ ] Corrective actions from previous audits closed
- [ ] Evidence accessible and organized
- [ ] Key personnel available for interviews

---

## Continuous Compliance

### Monthly Activities

- Review security metrics
- Process exceptions and risk acceptances
- Update risk register as needed
- Verify evidence collection is working

### Quarterly Activities

- Management review of security program
- Access reviews
- Third-party risk reviews
- Update SoA if needed

### Annual Activities

- Full risk assessment
- Internal audit
- Policy review and update
- Security objectives setting
- External audit (certification/surveillance)

---

## Common Pitfalls

| Pitfall | How We Avoid It |
|---------|-----------------|
| Paper compliance | Map controls to real implementations with evidence |
| Audit scramble | Continuous evidence collection, not annual gathering |
| Scope creep | Clear scope definition, change control |
| Control bloat | Risk-based control selection, remove unused controls |
| Documentation rot | Regular reviews, version control |
| Lack of ownership | Clear RACI, named control owners |

---

## ISO 27001:2022 Updates

The 2022 revision restructured Annex A controls:

| Category | Control Count | Focus Areas |
|----------|---------------|-------------|
| Organizational (5) | 37 | Policies, roles, responsibilities |
| People (6) | 8 | HR security, awareness |
| Physical (7) | 14 | Physical security |
| Technological (8) | 34 | Technical controls |

New controls added in 2022:
- A.5.7 Threat intelligence
- A.5.23 Information security for cloud services
- A.5.30 ICT readiness for business continuity
- A.7.4 Physical security monitoring
- A.8.9 Configuration management
- A.8.10 Information deletion
- A.8.11 Data masking
- A.8.12 Data leakage prevention
- A.8.16 Monitoring activities
- A.8.23 Web filtering
- A.8.28 Secure coding

Our control mapping addresses all 2022 requirements.
