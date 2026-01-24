# Postmortem: Staging Database Public Exposure

**Incident ID:** INC-2024-047
**Date:** September 2024
**Severity:** High (P2)
**Status:** Closed

---

## Executive Summary

A staging database containing customer PII was publicly accessible for approximately 72 hours due to a misconfigured security group. The exposure was detected by our CSPM tooling. Investigation confirmed no unauthorized access occurred during the exposure window. This incident led to the implementation of our "deny public exposure by default" policy.

---

## Timeline (All times UTC)

| Time | Event |
|------|-------|
| Sep 12, 14:32 | Engineer creates new staging environment for load testing |
| Sep 12, 14:45 | Security group modified to allow external load testing tool access |
| Sep 12, 14:47 | Database security group inadvertently set to 0.0.0.0/0 (copy-paste error) |
| Sep 12, 15:00 | Load testing begins, completes successfully |
| Sep 12, 16:00 | Engineer moves to other work, forgets to revert security group |
| Sep 15, 09:14 | CSPM alert fires: "RDS instance publicly accessible" |
| Sep 15, 09:18 | Security on-call acknowledges alert |
| Sep 15, 09:23 | Security group reverted, exposure closed |
| Sep 15, 09:30 | Incident declared, investigation begins |
| Sep 15, 11:00 | Database access logs reviewed - no unauthorized connections found |
| Sep 15, 14:00 | VPC flow logs analyzed - no suspicious traffic patterns |
| Sep 15, 16:00 | Incident downgraded, monitoring continues |
| Sep 16, 10:00 | Final analysis complete, no evidence of unauthorized access |
| Sep 18 | Postmortem meeting held |

**Total exposure window:** ~72 hours
**Time to detect:** 67 hours (CSPM scan interval was 24h at the time)
**Time to contain:** 9 minutes from alert

---

## Impact Assessment

### Data at Risk

| Data Type | Records | Classification |
|-----------|---------|----------------|
| Customer emails | ~15,000 | PII |
| Customer names | ~15,000 | PII |
| Usage metadata | ~50,000 | Internal |
| Test credentials | ~100 | Confidential |

Note: Staging contained a 6-month-old snapshot of production data that had NOT been masked. This is itself a policy violation.

### Actual Impact

- **Unauthorized access:** None confirmed
- **Data exfiltration:** None confirmed
- **Customer notification:** Not required (no confirmed breach)
- **Regulatory impact:** None (no confirmed breach)
- **Reputational impact:** None (not disclosed)

### Near-Miss Assessment

This was a significant near-miss. If an attacker had discovered the exposure:
- Direct database access with no authentication required
- Full read access to customer PII
- Would have required customer notification under GDPR
- Estimated cost of breach: $500K - $2M (notification, investigation, regulatory)

---

## Root Cause Analysis

### Immediate Cause

Engineer copy-pasted security group configuration and inadvertently set inbound rule to 0.0.0.0/0 instead of the specific IP of the load testing tool.

### Contributing Factors

1. **No guardrails preventing public database exposure**
   - SCPs did not block public RDS configurations
   - CSPM alerting existed but with 24-hour scan interval

2. **Production-like data in staging without masking**
   - Staging refresh process copied production data
   - No data masking pipeline implemented
   - "It's just staging" mentality

3. **No peer review for infrastructure changes**
   - Security group change made directly, no PR
   - No Terraform/IaC for this environment
   - Click-ops in console

4. **No automated reversion of temporary changes**
   - Temporary access had no expiration
   - No reminder to revert
   - Relied on human memory

### 5 Whys Analysis

1. **Why was the database exposed?** Security group allowed 0.0.0.0/0.
2. **Why was 0.0.0.0/0 allowed?** Copy-paste error during manual configuration.
3. **Why was it configured manually?** Staging environment not managed via IaC.
4. **Why isn't staging managed via IaC?** "Move fast" culture, staging seen as less critical.
5. **Why is staging seen as less critical?** Lack of understanding that staging contains sensitive data.

---

## What Went Well

- CSPM tooling detected the exposure (eventually)
- On-call response was fast once alerted (9 minutes to contain)
- Investigation was thorough and well-documented
- No evidence of actual breach
- Team was transparent about the incident internally

---

## What Went Poorly

- 72-hour exposure window is unacceptable
- 24-hour CSPM scan interval too slow for this risk
- Production data in staging without masking
- Manual infrastructure changes without review
- No preventive controls, only detective

---

## Action Items

| ID | Action | Owner | Due Date | Status |
|----|--------|-------|----------|--------|
| 1 | Implement SCP blocking public RDS | Platform | Oct 15 | Complete |
| 2 | Reduce CSPM scan interval to 1 hour | Security | Oct 1 | Complete |
| 3 | Implement real-time alerting for public exposure | Security | Oct 15 | Complete |
| 4 | Create data masking pipeline for staging | Data Eng | Dec 1 | Complete |
| 5 | Mandate IaC for all environments including staging | Platform | Nov 1 | Complete |
| 6 | Publish "deny public exposure by default" policy | Security | Oct 20 | Complete |
| 7 | Implement security group change alerting | Security | Oct 15 | Complete |
| 8 | Training on staging security requirements | Security | Nov 1 | Complete |
| 9 | Audit all staging environments for similar issues | Security | Oct 30 | Complete |

---

## Lessons Learned

### For Engineering

1. **"Just staging" is a dangerous mindset.** Staging often contains production-like data and should be treated with similar care.

2. **Temporary changes need expiration dates.** If you make a temporary change, set a calendar reminder or use automation to revert it.

3. **IaC isn't just for production.** Manual console changes are how misconfigurations happen.

### For Security

1. **Detective controls aren't enough.** 72 hours of exposure before detection is too long. We need preventive controls.

2. **Scan intervals matter.** 24-hour intervals leave significant windows. High-risk misconfigurations need real-time or near-real-time detection.

3. **Assume staging has sensitive data.** Design controls assuming staging is as sensitive as production.

### For the Organization

1. **Near-misses are gifts.** This could have been a major breach. We got lucky. The right response is to fix it, not to minimize it because "nothing happened."

2. **Speed vs. security is a false tradeoff.** The "move fast" approach that skipped IaC for staging created risk that could have cost far more time than it saved.

---

## Policy Changes Resulting from This Incident

1. **Decision Memo DM-001:** Deny public exposure by default
2. **Updated staging requirements:** Production-equivalent security controls
3. **Data masking mandate:** Non-production environments must use masked data
4. **IaC requirement:** All environments managed via Terraform, no console changes

---

## Follow-Up Review

**30-day review (October 2024):**
- All immediate actions complete
- No recurrence of similar issues
- CSPM detecting and blocking attempted public exposures

**90-day review (December 2024):**
- Data masking pipeline operational
- Zero public exposure incidents since policy implementation
- Staging security posture significantly improved

---

## Appendix: Detection Gap Analysis

### Why Did Detection Take 67 Hours?

| Control | Expected | Actual | Gap |
|---------|----------|--------|-----|
| CSPM scanning | 24h interval | 24h interval | Interval too long |
| GuardDuty | Real-time | No finding | RDS public exposure not a GuardDuty finding type |
| CloudTrail | Real-time | Event logged | No alert configured for SG changes |
| VPC Flow Logs | Real-time | Traffic logged | No alerting on external DB connections |

### Detection Improvements Implemented

1. CSPM interval reduced to 1 hour
2. Real-time alerting via EventBridge for security group changes
3. Custom CloudWatch alert for any 0.0.0.0/0 inbound rules
4. VPC Flow Log alerting for external connections to database ports
