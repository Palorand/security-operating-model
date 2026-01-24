# KPI Dashboard Specification

## Overview

This document specifies the security KPI dashboard requirements, data sources, and visualization standards.

---

## Dashboard Objectives

1. Provide real-time visibility into security posture
2. Enable data-driven decision making
3. Track progress against security objectives
4. Identify trends and emerging issues
5. Support reporting to leadership and stakeholders

---

## Dashboard Views

### Executive Dashboard

**Audience:** C-level, Board, Senior Leadership

**Refresh:** Weekly

**Content:**

| Widget | Type | Description |
|--------|------|-------------|
| Security Score | Gauge | Overall security posture (0-100) |
| Risk Heatmap | Matrix | Top risks by impact and likelihood |
| KPI Stoplight | Table | Red/Yellow/Green status for primary KPIs |
| Incident Summary | Counter | Incidents this month by severity |
| Trend Indicator | Sparklines | 6-month trend for key metrics |
| Open Exceptions | Counter | Total exceptions with expiration status |

**Design Principles:**
- Single page, no scrolling
- Focus on status and trends, not details
- Clear visual indicators (red/yellow/green)
- Comparison to previous period

### Operational Dashboard

**Audience:** Security Team, Engineering Leads

**Refresh:** Real-time / Daily

**Content:**

| Widget | Type | Description |
|--------|------|-------------|
| Vulnerability Burndown | Line chart | Open vulnerabilities over time by severity |
| SLA Compliance | Bar chart | Remediation within SLA by severity |
| MTTR Trend | Line chart | Mean time to remediate over time |
| Active Alerts | Table | Current security alerts requiring attention |
| Exception Tracker | Table | Open exceptions with days until expiration |
| Deployment Security | Bar chart | Deployments blocked vs. passed security gates |
| Coverage Metrics | Gauges | SAST/SCA/EDR coverage percentages |

**Design Principles:**
- Actionable information
- Drill-down capability
- Real-time where possible
- Filter by team/system/severity

### Compliance Dashboard

**Audience:** GRC Team, Auditors

**Refresh:** Daily

**Content:**

| Widget | Type | Description |
|--------|------|-------------|
| Control Status | Matrix | ISO 27001 / SOC 2 control implementation status |
| Evidence Freshness | Table | Last evidence collection date by control |
| Policy Review Status | Table | Policies and last review date |
| Training Compliance | Bar chart | Training completion by department |
| Access Review Status | Progress bar | Access reviews completed vs. due |
| Vendor Assessment Status | Table | Vendors and assessment status |

---

## KPI Definitions

### Primary KPIs

#### 1. Vulnerability SLA Compliance

```yaml
name: Vulnerability SLA Compliance
description: Percentage of vulnerabilities remediated within SLA
formula: (Vulnerabilities closed within SLA / Total vulnerabilities closed) * 100
unit: Percentage
target:
  critical: ">95%"
  high: ">90%"
  medium: ">80%"
data_source: Vulnerability Scanner API
refresh: Daily
dimensions:
  - severity
  - team
  - system
visualization: Stacked bar chart with SLA line
```

#### 2. Mean Time to Remediate (Critical)

```yaml
name: MTTR Critical Vulnerabilities
description: Average days from discovery to remediation for critical vulns
formula: Sum(remediation_date - discovery_date) / Count(critical_vulns)
unit: Days
target: "<7 days"
data_source: Vulnerability Scanner API
refresh: Daily
dimensions:
  - team
  - vulnerability_type
visualization: Line chart with target line
```

#### 3. Secret Exposure Incidents

```yaml
name: Secret Exposure Incidents
description: Count of secret exposure events
formula: Count(secret_alerts) grouped by environment
unit: Count
target:
  production: "0"
  pre_production: "<5/month"
data_source: Secret Scanner API + Incident System
refresh: Real-time
dimensions:
  - environment
  - secret_type
  - repository
visualization: Counter with trend sparkline
```

#### 4. Security Review Coverage

```yaml
name: Security Review Coverage
description: Percentage of eligible projects that received security review
formula: (Projects reviewed / Projects requiring review) * 100
unit: Percentage
target: "100%"
data_source: Security Review Tracker
refresh: Daily
dimensions:
  - team
  - review_type
visualization: Progress bar with list of pending reviews
```

#### 5. Exception Backlog Health

```yaml
name: Exception Backlog Health
description: Open exceptions count and age distribution
formula: Count(open_exceptions) grouped by age_bucket
unit: Count
target:
  total: "<15"
  over_90_days: "0"
data_source: GRC Platform
refresh: Daily
dimensions:
  - age_bucket (0-30, 31-60, 61-90, >90)
  - system
  - owner
visualization: Stacked bar chart by age
```

#### 6. MFA Coverage

```yaml
name: MFA Coverage
description: Percentage of accounts with MFA enabled
formula: (Accounts with MFA / Total accounts) * 100
unit: Percentage
target:
  privileged: "100%"
  all_users: ">95%"
data_source: Identity Provider API
refresh: Weekly
dimensions:
  - account_type
  - system
visualization: Gauge with breakdown table
```

#### 7. Phishing Resilience

```yaml
name: Phishing Resilience Rate
description: Percentage passing simulated phishing tests
formula: ((No click + Click and report) / Total recipients) * 100
unit: Percentage
target: ">90%"
data_source: Phishing Simulation Platform
refresh: Per campaign
dimensions:
  - department
  - campaign_difficulty
visualization: Bar chart by department with trend
```

#### 8. MTTD (Mean Time to Detect)

```yaml
name: Mean Time to Detect
description: Average time from incident occurrence to detection
formula: Sum(detection_time - incident_start_time) / Count(incidents)
unit: Hours
target: "<24 hours"
data_source: SIEM + Incident System
refresh: Weekly
dimensions:
  - incident_type
  - detection_source
visualization: Line chart with target line
note: Only measurable for detected incidents
```

#### 9. Incident Response Time

```yaml
name: Incident Response Time
description: Time from alert to initial response action
formula: Sum(response_time - alert_time) / Count(incidents)
unit: Minutes (P1) / Hours (P2+)
target:
  P1: "<60 minutes"
  P2: "<4 hours"
data_source: Incident Management System
refresh: Real-time
dimensions:
  - severity
  - time_of_day
visualization: Box plot showing distribution
```

#### 10. Security Training Completion

```yaml
name: Security Training Completion
description: Percentage of employees completed required training
formula: (Employees completed / Employees required) * 100
unit: Percentage
target: ">95%"
data_source: LMS API
refresh: Weekly
dimensions:
  - department
  - training_type
  - days_overdue
visualization: Progress bar with overdue list
```

---

## Data Sources

| Source | Type | Refresh | Authentication |
|--------|------|---------|----------------|
| Vulnerability Scanner | API | Every 4 hours | API Key |
| Secret Scanner | Webhook | Real-time | OAuth |
| Identity Provider | API | Daily | OAuth |
| SIEM | API | Real-time | API Key |
| Incident System | API | Real-time | OAuth |
| GRC Platform | API | Daily | API Key |
| LMS | API | Daily | API Key |
| Phishing Platform | API | Per campaign | API Key |
| CI/CD System | Webhook | Real-time | Token |

---

## Alerting Thresholds

| KPI | Yellow Threshold | Red Threshold | Alert Channel |
|-----|------------------|---------------|---------------|
| Vuln SLA Compliance | <90% | <80% | Slack + Email |
| MTTR Critical | >7 days | >14 days | Slack |
| Secret Incidents (Prod) | 1 | >1 | PagerDuty |
| Review Coverage | <95% | <90% | Slack |
| Exceptions >90 days | 1 | >3 | Email |
| MFA Coverage | <98% | <95% | Weekly report |
| MTTD | >24 hours | >48 hours | Weekly report |
| IR Response Time (P1) | >30 min | >60 min | PagerDuty |

---

## Implementation Notes

### Technology Stack

| Component | Recommended Options |
|-----------|---------------------|
| Dashboard Platform | Grafana, Datadog, Tableau, PowerBI |
| Data Aggregation | Custom ETL, Airflow, dbt |
| Data Storage | PostgreSQL, Snowflake, BigQuery |
| Alerting | PagerDuty, Opsgenie, native platform |

### Data Quality

- Validate data on ingestion
- Track data freshness per source
- Alert on missing or stale data
- Document data lineage

### Access Control

| Dashboard | Access |
|-----------|--------|
| Executive | Leadership, Security Lead |
| Operational | Security Team, Engineering Leads |
| Compliance | GRC, Security, Auditors (read-only) |

### Maintenance

- Review dashboard relevance quarterly
- Update thresholds based on maturity
- Archive unused widgets
- Document all calculated metrics

---

## Rollout Plan

| Phase | Scope | Timeline |
|-------|-------|----------|
| 1 | Core vulnerability metrics | Week 1-2 |
| 2 | Incident and detection metrics | Week 3-4 |
| 3 | Compliance and governance metrics | Week 5-6 |
| 4 | Executive dashboard | Week 7-8 |
| 5 | Alerting and automation | Week 9-10 |
