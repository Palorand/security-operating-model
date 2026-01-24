# Risk Acceptance Form

## Instructions

Complete this form when formally accepting a security risk that cannot be fully mitigated. This creates a record of informed risk acceptance by the appropriate business owner.

---

## Risk Identification

| Field | Value |
|-------|-------|
| Risk Acceptance ID | RA-YYYY-NNN |
| Date | YYYY-MM-DD |
| Requestor | [Name, Title] |
| Business Owner | [Name, Title] |
| Security Reviewer | [Name] |

---

## Risk Description

### Summary

[One paragraph describing the risk in business terms]

### Technical Details

[Technical description of the vulnerability, gap, or exposure]

### Affected Systems/Data

| System/Asset | Data Classification | Business Function |
|--------------|--------------------|--------------------|
| [System name] | [Public/Internal/Confidential/Restricted] | [What it does] |

---

## Risk Assessment

### Impact Analysis

| Impact Category | Severity (1-5) | Description |
|-----------------|----------------|-------------|
| Financial | | [Potential financial loss] |
| Operational | | [Business disruption impact] |
| Reputational | | [Customer/market perception] |
| Regulatory | | [Compliance implications] |
| Legal | | [Liability exposure] |

**Overall Impact Score:** [1-5]

### Likelihood Assessment

| Factor | Assessment |
|--------|------------|
| Threat actor motivation | [Low/Medium/High] |
| Attack complexity | [Low/Medium/High] |
| Current exposure | [Internal only/Limited external/Broadly exposed] |
| Historical incidents | [None/Rare/Occasional/Frequent] |

**Overall Likelihood Score:** [1-5]

### Risk Score

| Metric | Value |
|--------|-------|
| Impact | [1-5] |
| Likelihood | [1-5] |
| Detectability Modifier | [-2 to +2] |
| **Final Risk Score** | [Calculated] |
| **Risk Level** | [Low/Medium/High/Critical] |

---

## Control Analysis

### Existing Controls

| Control | Effectiveness | Notes |
|---------|---------------|-------|
| [Control 1] | [Partial/Full] | [How it helps] |
| [Control 2] | [Partial/Full] | [How it helps] |

### Controls Considered But Not Implemented

| Control | Reason Not Implemented |
|---------|----------------------|
| [Control option] | [Cost/Technical limitation/Timeline/etc.] |

### Compensating Controls

| Compensating Control | Implementation Status | Effectiveness |
|---------------------|----------------------|---------------|
| [Control 1] | [In place/Planned] | [How it reduces risk] |
| [Control 2] | [In place/Planned] | [How it reduces risk] |

---

## Business Justification

### Why Accept This Risk?

[Explain why the business chooses to accept this risk rather than mitigate it fully]

### Business Value Protected

[What business capability or value does accepting this risk enable?]

### Alternatives Considered

| Alternative | Pros | Cons | Why Rejected |
|-------------|------|------|--------------|
| [Option 1] | | | |
| [Option 2] | | | |

---

## Conditions and Monitoring

### Conditions of Acceptance

This risk acceptance is valid only while the following conditions remain true:

1. [Condition 1 - e.g., "System remains isolated from production network"]
2. [Condition 2 - e.g., "Data volume does not exceed X records"]
3. [Condition 3 - e.g., "Compensating controls remain in place"]

### Monitoring Requirements

| Monitoring Activity | Frequency | Owner |
|--------------------|-----------|-------|
| [Activity 1] | [Daily/Weekly/Monthly] | [Name/Role] |
| [Activity 2] | [Daily/Weekly/Monthly] | [Name/Role] |

### Review Triggers

This risk acceptance must be re-evaluated if:

- [ ] Threat landscape changes materially
- [ ] System scope or data classification changes
- [ ] Compensating controls are degraded
- [ ] Security incident related to this risk occurs
- [ ] Regulatory requirements change

---

## Review Schedule

| Review Type | Date | Reviewer |
|-------------|------|----------|
| Initial Acceptance | [Date] | [Name] |
| 6-Month Review | [Date] | [Name] |
| Annual Review | [Date] | [Name] |

---

## Approvals

### Security Review

| Field | Value |
|-------|-------|
| Security Reviewer | [Name] |
| Review Date | [Date] |
| Recommendation | [Accept / Accept with conditions / Do not accept] |
| Comments | [Security perspective on this acceptance] |

**Security Signature:** _________________________ **Date:** _____________

### Business Owner Acceptance

By signing below, I acknowledge that:

1. I understand the risk described in this document
2. I accept this risk on behalf of [Department/Business Unit]
3. I commit to maintaining the compensating controls described
4. I will ensure this risk is reviewed per the schedule above
5. I will notify Security if conditions change

| Field | Value |
|-------|-------|
| Business Owner | [Name] |
| Title | [Title] |
| Department | [Department] |

**Business Owner Signature:** _________________________ **Date:** _____________

### Executive Approval (if required)

Required for High or Critical risk levels.

| Field | Value |
|-------|-------|
| Executive Approver | [Name] |
| Title | [Title] |

**Executive Signature:** _________________________ **Date:** _____________

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | [Date] | [Name] | Initial acceptance |
| | | | |
