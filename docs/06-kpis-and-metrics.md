# Security KPIs and Metrics

This document defines the key performance indicators used to measure security program effectiveness.

---

## Principles for Security Metrics

1. **Actionable over interesting** - Every metric should drive a decision or behavior
2. **Outcome over activity** - Measure results, not effort
3. **Trend over snapshot** - Direction matters more than absolute numbers
4. **Few over many** - 10 metrics you act on beat 50 you ignore
5. **Anti-gaming considered** - Anticipate how metrics can be manipulated

---

## Primary KPIs

These are the metrics reported to leadership monthly.

### 1. Vulnerability SLA Compliance

**Definition:** Percentage of vulnerabilities remediated within SLA by severity.

| Severity | SLA | Target Compliance |
|----------|-----|-------------------|
| Critical | 7 days | > 95% |
| High | 30 days | > 90% |
| Medium | 90 days | > 80% |
| Low | Best effort | Not tracked |

**Measurement:** Vulnerability scanner data, calculated weekly.

**Anti-gaming notes:**
- Don't count risk-accepted vulns as "remediated"
- Track separately: remediated vs. risk-accepted vs. false-positive
- Watch for severity downgrading without justification

**Owner:** Security Engineering

---

### 2. Mean Time to Remediate (MTTR) - Critical Vulnerabilities

**Definition:** Average days from vulnerability discovery to remediation for critical severity.

**Target:** < 7 days

**Measurement:** Vulnerability scanner timestamps.

**Anti-gaming notes:**
- Exclude outliers only with documented justification
- Track median alongside mean to spot skew
- Don't count "mitigated" as "remediated" unless control is equivalent

**Owner:** Security Engineering

---

### 3. Secret Exposure Incidents

**Definition:** Number of incidents where secrets (credentials, API keys, certificates) were exposed.

**Target:** 0 production incidents; < 5 pre-production detections per month

**Measurement:** Secret scanning alerts + incident tracking.

**Anti-gaming notes:**
- Count all exposures, even if caught pre-commit
- Distinguish severity: production vs. development
- Track time-to-rotation after detection

**Owner:** Security Engineering

---

### 4. Security Review Coverage

**Definition:** Percentage of new projects/major changes that received security review before production.

**Target:** 100%

**Measurement:** Security review tracker vs. deployment records.

**Anti-gaming notes:**
- Define clear criteria for "requires review"
- Track reviews that happened post-deployment (failures)
- Measure review quality, not just completion

**Owner:** Security Lead

---

### 5. Exception Backlog Health

**Definition:** Number of open security exceptions and their age distribution.

**Target:**
- Total open exceptions < 15
- Zero exceptions > 90 days without renewal

**Measurement:** Exception tracking system.

**Anti-gaming notes:**
- Expired exceptions count as violations, not closures
- Track exception-to-remediation conversion rate
- Monitor repeat exceptions for same issue

**Owner:** GRC

---

### 6. Phishing Resilience Rate

**Definition:** Percentage of employees who correctly handle simulated phishing attempts.

**Target:** > 90% (no click, or click + report)

**Measurement:** Phishing simulation platform.

**Anti-gaming notes:**
- Vary difficulty across campaigns
- Don't count "warned" employees differently
- Track repeat offenders specifically

**Owner:** Security Awareness

---

### 7. MFA Coverage

**Definition:** Percentage of accounts with MFA enabled across critical systems.

**Target:** 100% for production access; > 95% for all corporate accounts

**Measurement:** IAM audit across systems.

**Anti-gaming notes:**
- Count service accounts separately (should use workload identity)
- Distinguish MFA types (SMS vs. TOTP vs. hardware key)
- Track exceptions and justifications

**Owner:** IT / Identity

---

### 8. Mean Time to Detect (MTTD)

**Definition:** Average time from attack/anomaly occurrence to detection alert.

**Target:** < 24 hours for critical threats

**Measurement:** SIEM timestamps, incident records.

**Anti-gaming notes:**
- Only measurable for detected incidents (survivorship bias)
- Supplement with red team exercises for ground truth
- Track by threat category, not just overall average

**Owner:** Security Operations

---

### 9. Incident Response Time

**Definition:** Time from alert to initial response action.

**Target:** < 1 hour for P1 incidents; < 4 hours for P2

**Measurement:** Incident management system timestamps.

**Anti-gaming notes:**
- "Response" means meaningful action, not just acknowledgment
- Track separately: detection-to-alert, alert-to-response, response-to-containment
- Include after-hours response times

**Owner:** Security Operations

---

### 10. Security Training Completion

**Definition:** Percentage of employees who completed required security training.

**Target:** > 95% within 30 days of due date

**Measurement:** LMS completion records.

**Anti-gaming notes:**
- Track comprehension (quiz scores), not just completion
- New hire training tracked separately
- Role-specific training tracked by role

**Owner:** Security Awareness

---

## Secondary Metrics

Tracked internally but not reported to leadership unless concerning.

| Metric | Target | Purpose |
|--------|--------|---------|
| SAST findings per build | Trending down | Code quality indicator |
| Dependency vulnerabilities | < 50 high/critical | Supply chain health |
| Cloud misconfigurations | < 20 high severity | Infrastructure hygiene |
| Access reviews completed | 100% on schedule | IAM governance |
| Backup restoration tests | 1 per quarter | Recovery readiness |
| Security champions engagement | > 80% attending monthly sync | Program health |

---

## Metrics Dashboard Specification

### Executive View

Single page showing:

1. **Stoplight summary** - Red/Yellow/Green for each primary KPI
2. **Trend arrows** - Direction vs. last month
3. **Top 3 risks** - From risk register
4. **Incidents this month** - Count and severity

### Operational View

Detailed view showing:

1. **All primary KPIs** with historical trend (6 months)
2. **Secondary metrics** current state
3. **Exception list** with expiration dates
4. **Vulnerability breakdown** by severity and age
5. **Upcoming deadlines** (reviews, renewals, audits)

### Data Sources

| Metric | Source System | Refresh Frequency |
|--------|---------------|-------------------|
| Vulnerability data | Qualys/Tenable/etc. | Daily |
| Secret scanning | GitHub/GitLab | Real-time |
| Security reviews | Jira/Asana/etc. | Real-time |
| Exceptions | GRC platform | Real-time |
| Phishing results | KnowBe4/etc. | Per campaign |
| MFA coverage | Okta/Azure AD/etc. | Weekly |
| SIEM metrics | Splunk/etc. | Real-time |
| Training | LMS | Weekly |

---

## Reporting Cadence

| Report | Audience | Frequency | Content |
|--------|----------|-----------|---------|
| Security Dashboard | Security team | Real-time | All metrics |
| Monthly Security Report | Leadership | Monthly | Primary KPIs + narrative |
| Quarterly Security Review | Executive team | Quarterly | KPIs + roadmap progress + risks |
| Board Security Summary | Board | Quarterly | High-level posture + incidents |

---

## Metric Review Process

### Monthly

- Review all KPI trends
- Investigate any metric crossing threshold
- Adjust targets if consistently over/under-performing
- Update anti-gaming controls if manipulation detected

### Quarterly

- Assess metric usefulness - drop metrics nobody acts on
- Consider new metrics for emerging risks
- Benchmark against industry where possible
- Calibrate targets based on maturity progression

### Annually

- Full metric framework review
- Align metrics with updated risk priorities
- Update targets for next year
- Retire metrics that served their purpose
