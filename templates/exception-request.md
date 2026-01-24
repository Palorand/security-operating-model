# Security Exception Request

## Instructions

Complete this form to request a temporary exception to a security control or policy. Exceptions are time-limited deviations that require compensating controls and a remediation plan.

---

## Request Information

| Field | Value |
|-------|-------|
| Exception ID | EX-YYYY-NNN |
| Request Date | YYYY-MM-DD |
| Requestor | [Name, Title, Team] |
| Business Owner | [Name, Title] |

---

## Exception Details

### Control/Policy Being Excepted

| Field | Value |
|-------|-------|
| Control Reference | [Policy section, standard, or control ID] |
| Control Description | [What the control requires] |

### Scope of Exception

| Field | Value |
|-------|-------|
| Affected Systems | [List systems, applications, or services] |
| Affected Data | [Data types and classification] |
| Affected Users/Services | [Who/what is affected] |
| Environment | [Production / Staging / Development / All] |

### Exception Description

[Describe specifically what deviation from the control is being requested]

---

## Justification

### Why Is the Exception Needed?

[Explain why the control cannot be fully implemented at this time]

### Technical Constraints

| Constraint | Description |
|------------|-------------|
| [Constraint type] | [Details] |

### Business Impact if Exception Not Granted

[What business impact would occur if this exception is denied?]

### Alternatives Considered

| Alternative | Why Not Feasible |
|-------------|------------------|
| [Option 1] | [Reason] |
| [Option 2] | [Reason] |

---

## Risk Assessment

### Risk Without the Control

| Risk Factor | Assessment |
|-------------|------------|
| What could go wrong? | [Describe potential security impact] |
| Likelihood (1-5) | [Score with rationale] |
| Impact (1-5) | [Score with rationale] |
| Risk Score | [Calculated] |

### Threat Scenarios

| Scenario | Likelihood | Impact |
|----------|------------|--------|
| [Attack scenario 1] | [Low/Medium/High] | [Description] |
| [Attack scenario 2] | [Low/Medium/High] | [Description] |

---

## Compensating Controls

Compensating controls are required for all exceptions. These controls should address the risk created by the exception.

### Proposed Compensating Controls

| Control | How It Addresses Risk | Implementation Status |
|---------|----------------------|----------------------|
| [Control 1] | [Explanation] | [In place / Will implement by date] |
| [Control 2] | [Explanation] | [In place / Will implement by date] |
| [Control 3] | [Explanation] | [In place / Will implement by date] |

### Monitoring During Exception Period

| Monitoring Activity | Frequency | Owner | Alert Threshold |
|--------------------|-----------|-------|-----------------|
| [Activity 1] | [Frequency] | [Name] | [When to alert] |
| [Activity 2] | [Frequency] | [Name] | [When to alert] |

---

## Remediation Plan

Exceptions must include a plan to eliminate the need for the exception.

### Remediation Approach

[Describe how the control will eventually be implemented]

### Remediation Timeline

| Milestone | Target Date | Owner | Dependencies |
|-----------|-------------|-------|--------------|
| [Milestone 1] | [Date] | [Name] | [Dependencies] |
| [Milestone 2] | [Date] | [Name] | [Dependencies] |
| [Final remediation] | [Date] | [Name] | [Dependencies] |

### Remediation Blockers

| Blocker | Mitigation | Expected Resolution |
|---------|------------|---------------------|
| [Blocker 1] | [How to address] | [Date] |

---

## Exception Duration

| Field | Value |
|-------|-------|
| Requested Start Date | [Date] |
| Requested End Date | [Date - max 90 days from start] |
| Duration | [X days] |

**Note:** Exceptions are limited to 90 days maximum. Extensions require renewal with progress report.

---

## Acknowledgments

### Requestor Acknowledgment

By submitting this request, I confirm that:

- [ ] The information provided is accurate and complete
- [ ] I understand the security risk created by this exception
- [ ] I commit to implementing the compensating controls described
- [ ] I commit to the remediation timeline provided
- [ ] I will notify Security immediately if circumstances change

**Requestor:** _________________________ **Date:** _____________

### Business Owner Acknowledgment

By approving this request, I accept responsibility for:

- [ ] The risk during the exception period
- [ ] Ensuring compensating controls are maintained
- [ ] Providing resources for remediation
- [ ] Escalating if remediation is blocked

**Business Owner:** _________________________ **Date:** _____________

---

## Security Review

### Risk Assessment

| Field | Value |
|-------|-------|
| Reviewer | [Name] |
| Review Date | [Date] |
| Residual Risk Level | [Low / Medium / High / Critical] |

### Compensating Controls Assessment

| Control | Adequate? | Comments |
|---------|-----------|----------|
| [Control 1] | [Yes/No/Partial] | [Feedback] |
| [Control 2] | [Yes/No/Partial] | [Feedback] |

### Additional Requirements

[Any additional compensating controls or conditions required by Security]

### Recommendation

- [ ] **Approve** - Risk is acceptable with proposed controls
- [ ] **Approve with Conditions** - Approve if additional requirements met
- [ ] **Deny** - Risk is not acceptable
- [ ] **Defer** - Need more information

**Security Reviewer:** _________________________ **Date:** _____________

---

## Approval

### Approval Decision

| Field | Value |
|-------|-------|
| Decision | [Approved / Approved with Conditions / Denied] |
| Approver | [Name, Title] |
| Approval Date | [Date] |
| Expiration Date | [Date] |

### Conditions of Approval

[List any conditions that must be maintained for this exception to remain valid]

1. [Condition 1]
2. [Condition 2]
3. [Condition 3]

**Approver Signature:** _________________________ **Date:** _____________

---

## Exception Lifecycle

| Event | Date | Notes |
|-------|------|-------|
| Requested | [Date] | |
| Reviewed | [Date] | |
| Approved/Denied | [Date] | |
| Compensating controls verified | [Date] | |
| Remediation checkpoint 1 | [Date] | |
| Remediation checkpoint 2 | [Date] | |
| Exception closed | [Date] | [Remediated / Renewed / Converted to Risk Acceptance] |
