# Decision Memo: Secrets Management Standard

## Document Information

| Field | Value |
|-------|-------|
| Decision ID | DM-002 |
| Title | Secrets Management Standard |
| Author | Security Lead |
| Date | 2025-11-01 |
| Status | Approved |

---

## Executive Summary

All secrets (credentials, API keys, certificates, tokens) must be managed through approved secrets management solutions with short-lived credentials preferred. Long-lived credentials in code, configuration files, or environment variables are prohibited. This standard establishes the approved patterns and migration timeline.

---

## Context

### Background

Secrets management has been inconsistent across teams:
- Some teams use HashiCorp Vault
- Others use cloud-native solutions (AWS Secrets Manager, GCP Secret Manager)
- Some still use environment variables or config files
- Historical secrets exist in git history

Secret scanning has identified 150+ historical secrets in repositories, and we've had three incidents in the past year involving exposed credentials.

### Current State

| Pattern | Usage | Risk Level |
|---------|-------|------------|
| HashiCorp Vault | 40% of services | Low |
| Cloud Secrets Manager | 25% of services | Low |
| Environment variables | 20% of services | Medium |
| Config files / hardcoded | 15% of services | High |

### Trigger

- Increased secret scanning findings
- Compliance requirements (SOC 2, ISO 27001) for secrets management
- Need for standardization as team scales

---

## Decision

### Statement

**All secrets must be stored in approved secrets management solutions and retrieved at runtime. Short-lived credentials (workload identity, OIDC) are the preferred pattern. Long-lived secrets in code, config files, or environment variables are prohibited.**

### Approved Solutions

| Solution | Use Case | Preference |
|----------|----------|------------|
| Workload Identity / OIDC | Cloud resource access | Preferred |
| HashiCorp Vault | Application secrets, dynamic credentials | Preferred |
| AWS Secrets Manager | AWS-native applications | Acceptable |
| GCP Secret Manager | GCP-native applications | Acceptable |

### Prohibited Patterns

- Secrets in source code (any file in repository)
- Secrets in CI/CD configuration files
- Long-lived credentials where short-lived alternatives exist
- Shared credentials across services
- Secrets in environment variables at rest (deployment configs)

### Scope

| Attribute | Value |
|-----------|-------|
| Applies to | All services, all environments |
| Effective date | 2025-12-01 (new services), 2025-03-01 (existing services) |
| Review date | 2025-11-01 |

---

## Options Considered

### Option 1: Standardize on Single Solution (Vault Only)

**Description:** Mandate HashiCorp Vault for all secrets management.

| Pros | Cons |
|------|------|
| Single solution to manage | Migration effort for cloud-native teams |
| Consistent patterns | Additional infrastructure to maintain |
| Advanced features (dynamic secrets) | Potential vendor lock-in |

**Estimated effort:** High

### Option 2: Allow Any Secrets Manager

**Description:** Permit any secrets management solution that meets baseline requirements.

| Pros | Cons |
|------|------|
| Maximum flexibility | Inconsistent patterns |
| Lower migration effort | Harder to audit and support |
| Teams choose best fit | Training burden |

**Estimated effort:** Low

### Option 3: Tiered Approach with Preferred Solutions (Selected)

**Description:** Define preferred and acceptable solutions with clear migration path.

| Pros | Cons |
|------|------|
| Balance of standardization and flexibility | Still some variation |
| Pragmatic migration path | Need to support multiple solutions |
| Prioritizes short-lived credentials | |

**Estimated effort:** Medium

---

## Rationale

### Why This Option?

A tiered approach balances security improvement with operational pragmatism:

1. **Short-lived credentials eliminate entire risk categories** - No rotation needed, no exposure window
2. **Multiple approved solutions** reduce migration friction while maintaining security baseline
3. **Clear prohibition on bad patterns** draws a firm line
4. **Phased timeline** allows teams to plan migrations

### Key Factors

| Factor | Weight | How Selected Option Performs |
|--------|--------|------------------------------|
| Risk reduction | High | Eliminates hardcoded secrets |
| Migration feasibility | High | Phased approach is achievable |
| Operational complexity | Medium | Limited set of solutions |
| Developer experience | Medium | Good tooling available |

### Trade-offs Accepted

- Supporting multiple solutions increases operational overhead
- Some legacy systems may need longer migration timelines
- Short-lived credentials require infrastructure changes

---

## Implementation

### Requirements

#### 1. Short-Lived Credentials (Workload Identity)

**For cloud resources:**
- AWS: IAM Roles for Service Accounts, OIDC federation
- GCP: Workload Identity Federation
- Azure: Managed Identities

**For CI/CD:**
- GitHub Actions: OIDC to cloud providers
- GitLab: OIDC integration
- No long-lived cloud credentials in CI/CD

#### 2. Application Secrets (Vault / Cloud Secrets Manager)

**Pattern:**
```
Application starts
    -> Authenticates to secrets manager (using workload identity)
    -> Retrieves secrets at runtime
    -> Secrets never written to disk or logs
```

**Requirements:**
- Secrets retrieved at runtime, not build time
- Application authenticates using workload identity where possible
- Secrets have defined rotation schedule
- Access audited

#### 3. Secret Scanning

**Pre-commit:**
- Gitleaks or similar running on developer machines
- Blocks commits containing secrets

**CI/CD:**
- Secret scanning on all PRs
- Blocks merge if secrets detected
- Historical scanning for new patterns

**Monitoring:**
- Alerts on any secret detection
- 24-hour rotation SLA for any exposed secret

### Timeline

| Milestone | Target Date | Owner |
|-----------|-------------|-------|
| Standard published | 2025-11-15 | Security |
| Pre-commit hooks available | 2025-11-15 | Security Engineering |
| CI/CD scanning mandatory | 2025-12-01 | Security Engineering |
| New services must comply | 2025-12-01 | All teams |
| Existing services migrated | 2025-03-01 | All teams |
| Historical secrets rotated | 2025-03-01 | All teams |

### Migration Guide

For each service:

1. **Inventory current secrets**
   - List all secrets used by the service
   - Identify storage location (env var, config, vault)

2. **Determine target pattern**
   - Cloud resources: workload identity
   - Application secrets: Vault or cloud secrets manager
   - Third-party API keys: secrets manager with rotation plan

3. **Implement retrieval**
   - Add secrets manager SDK/integration
   - Remove hardcoded values
   - Test in non-production

4. **Rotate and deploy**
   - Generate new credentials in secrets manager
   - Deploy updated application
   - Revoke old credentials
   - Verify no references to old credentials

5. **Document and verify**
   - Update service documentation
   - Security verification

---

## Impact Assessment

### Affected Stakeholders

| Stakeholder | Impact | Communication Needed |
|-------------|--------|---------------------|
| All engineering teams | Migration work required | Yes - all-hands, documentation |
| Platform team | Vault/identity infrastructure | Yes - capacity planning |
| DevOps/SRE | CI/CD changes | Yes - coordination |

### Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Migration breaks services | Medium | High | Non-prod testing, rollback plan |
| Timeline not met | Medium | Medium | Prioritize high-risk services |
| Developer friction | Low | Low | Good tooling and documentation |

### Resource Requirements

| Resource | Amount | Source |
|----------|--------|--------|
| Security engineering | 4 weeks | Security team |
| Platform engineering | 2 weeks | Platform team |
| Per-team migration | 1-3 days per service | Each team |

---

## Exceptions

### Exception Process

Exceptions require:
1. Technical justification for why approved pattern cannot be used
2. Compensating controls documented
3. Time-boxed exception (max 90 days)
4. Security Lead approval

### Pre-Approved Exceptions

| Exception | Conditions | Duration |
|-----------|------------|----------|
| Legacy system pending retirement | System decommission planned within 6 months, enhanced monitoring in place | Until decommission |
| Third-party constraint | Vendor requires specific credential format, documented vendor limitation | Until vendor supports alternative |

---

## Success Criteria

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Services using approved solution | 100% | Quarterly audit |
| Secret scanning coverage | 100% of repos | Scanner dashboard |
| Secrets in code (new) | 0 | Pre-commit + CI blocking |
| Mean time to rotate exposed secret | <24 hours | Incident tracking |
| Long-lived cloud credentials | 0 | IAM audit |

---

## Enforcement

### Technical Controls

1. **Pre-commit hooks** - Block commits with secrets
2. **CI/CD gates** - Block PRs with secrets
3. **Cloud policies** - Alert on long-lived credential creation
4. **Vault policies** - Enforce access controls and audit

### Governance Controls

1. **Quarterly compliance review** - Audit all services
2. **New service checklist** - Secrets management verified before production
3. **Incident review** - Any secret exposure triggers process review

---

## Review and Governance

### Review Schedule

| Review Type | Frequency | Next Review |
|-------------|-----------|-------------|
| Compliance audit | Quarterly | 2025-02-01 |
| Standard review | Annually | 2025-11-01 |
| Tool evaluation | Annually | 2025-11-01 |

### Change Process

Changes require Security Lead approval with documentation of rationale.

---

## Approvals

### Consulted

| Name | Role | Date | Feedback |
|------|------|------|----------|
| [Platform Lead] | Platform Lead | 2025-10-25 | Infrastructure support confirmed |
| [Eng Directors] | Engineering Directors | 2025-10-28 | Timeline agreed |

### Approved By

| Name | Role | Date |
|------|------|------|
| [CTO] | CTO | 2025-11-01 |
| [Security Lead] | Security Lead | 2025-11-01 |

---

## References

- HashiCorp Vault documentation
- AWS Secrets Manager best practices
- OWASP Secrets Management Cheat Sheet
- Internal: Secret scanning runbook
