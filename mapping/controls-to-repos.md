# Controls to Implementation Mapping

This document maps security controls to their concrete implementations in code, configuration, and infrastructure.

---

## Purpose

This mapping provides:

1. **Traceability** - Connect controls to actual implementation
2. **Evidence location** - Where to find proof for audits
3. **Ownership clarity** - Who maintains each implementation
4. **Change impact** - Understand what's affected by changes

---

## Control Categories

### Identity and Access Management

| Control | Implementation | Repository/Location | Owner |
|---------|----------------|---------------------|-------|
| SSO/SAML Configuration | Okta tenant configuration | `infrastructure/okta-terraform/` | IT |
| MFA Enforcement | Okta authentication policies | `infrastructure/okta-terraform/policies/` | IT |
| Password Policy | Identity provider settings | `infrastructure/okta-terraform/policies/password.tf` | IT |
| Role Definitions | IAM roles and groups | `infrastructure/aws-iam/roles/` | Platform |
| Permission Boundaries | AWS IAM boundaries | `infrastructure/aws-iam/boundaries/` | Platform |
| Service Account Management | Workload identity configs | `infrastructure/gcp-workload-identity/` | Platform |
| Access Review Automation | Custom tooling | `tools/access-review/` | Security Eng |
| JIT Access System | Temporalize or similar | `infrastructure/jit-access/` | Security Eng |

### Network Security

| Control | Implementation | Repository/Location | Owner |
|---------|----------------|---------------------|-------|
| VPC Architecture | Terraform VPC modules | `infrastructure/terraform/modules/vpc/` | Platform |
| Security Groups | Terraform SG definitions | `infrastructure/terraform/modules/security-groups/` | Platform |
| Network ACLs | Terraform NACL configs | `infrastructure/terraform/modules/nacl/` | Platform |
| WAF Rules | AWS WAF / Cloudflare config | `infrastructure/waf/` | Security Eng |
| DDoS Protection | Cloud provider + Cloudflare | `infrastructure/cloudflare/` | Platform |
| VPN/ZTNA | Tailscale/Cloudflare Access | `infrastructure/zero-trust/` | IT |
| DNS Security | Route53 + filtering config | `infrastructure/dns/` | Platform |
| TLS Configuration | Certificate management | `infrastructure/certificates/` | Platform |

### Application Security

| Control | Implementation | Repository/Location | Owner |
|---------|----------------|---------------------|-------|
| SAST Scanning | Semgrep configuration | `.semgrep/` in each repo | Security Eng |
| Dependency Scanning | Dependabot / Snyk config | `.github/dependabot.yml` | Security Eng |
| Secret Scanning | Gitleaks + GitHub native | `.gitleaks.toml`, repo settings | Security Eng |
| Container Scanning | Trivy in CI/CD | `.github/workflows/security.yml` | Security Eng |
| DAST Scanning | OWASP ZAP config | `security/dast/` | Security Eng |
| Security Headers | Application middleware | `src/middleware/security-headers.ts` | Engineering |
| Input Validation | Application code | `src/validators/` | Engineering |
| CSRF Protection | Framework configuration | `src/config/security.ts` | Engineering |

### Infrastructure Security

| Control | Implementation | Repository/Location | Owner |
|---------|----------------|---------------------|-------|
| CSPM Policies | Prisma Cloud / native rules | `security/cspm-policies/` | Security Eng |
| Cloud Guardrails | SCPs / Org Policies | `infrastructure/organization/scps/` | Platform |
| Terraform Security | tfsec / Checkov config | `.tfsec.yml`, `.checkov.yml` | Security Eng |
| Baseline Configurations | CIS benchmark configs | `infrastructure/baselines/` | Platform |
| Patch Management | SSM / OS config management | `infrastructure/patch-management/` | Platform |
| Container Hardening | Dockerfile best practices | `docker/` in each repo | Engineering |
| Kubernetes Security | Pod security policies/standards | `kubernetes/policies/` | Platform |
| Secrets Management | Vault configuration | `infrastructure/vault/` | Platform |

### Data Protection

| Control | Implementation | Repository/Location | Owner |
|---------|----------------|---------------------|-------|
| Encryption at Rest | KMS key configurations | `infrastructure/kms/` | Platform |
| Encryption in Transit | TLS termination config | `infrastructure/load-balancers/` | Platform |
| Database Encryption | RDS/Cloud SQL settings | `infrastructure/databases/` | Platform |
| Backup Encryption | Backup service config | `infrastructure/backups/` | SRE |
| DLP Rules | Cloud DLP configuration | `security/dlp/` | Security Eng |
| Data Masking | Masking job configs | `data-platform/masking/` | Data Eng |
| Key Rotation | KMS rotation policies | `infrastructure/kms/rotation.tf` | Platform |

### Logging and Monitoring

| Control | Implementation | Repository/Location | Owner |
|---------|----------------|---------------------|-------|
| Centralized Logging | Log aggregation config | `infrastructure/logging/` | Platform |
| CloudTrail | AWS CloudTrail terraform | `infrastructure/cloudtrail/` | Platform |
| Application Logging | Logging library config | `src/lib/logger.ts` | Engineering |
| SIEM Integration | Splunk/Datadog forwarders | `infrastructure/siem/` | Security Eng |
| Detection Rules | SIEM detection content | `security/detections/` | Security Eng |
| Alerting Rules | PagerDuty/Opsgenie config | `infrastructure/alerting/` | SRE |
| Metrics Collection | Prometheus/Datadog config | `infrastructure/monitoring/` | SRE |
| Audit Logging | Application audit events | `src/lib/audit.ts` | Engineering |

### Incident Response

| Control | Implementation | Repository/Location | Owner |
|---------|----------------|---------------------|-------|
| Runbooks | Incident procedures | `docs/runbooks/` | Security Ops |
| Automation Playbooks | SOAR playbooks | `security/playbooks/` | Security Eng |
| Forensic Tooling | Forensic scripts | `security/forensics/` | Security Eng |
| Communication Templates | Incident comms | `docs/incident-templates/` | Security |
| On-Call Configuration | PagerDuty schedules | `infrastructure/pagerduty/` | SRE |

### CI/CD Security

| Control | Implementation | Repository/Location | Owner |
|---------|----------------|---------------------|-------|
| Pipeline Definition | GitHub Actions workflows | `.github/workflows/` | Engineering |
| Security Gates | Security job definitions | `.github/workflows/security.yml` | Security Eng |
| Artifact Signing | Cosign configuration | `.github/workflows/release.yml` | Security Eng |
| SBOM Generation | Syft configuration | `.github/workflows/sbom.yml` | Security Eng |
| Deployment Policies | Environment protection rules | Repo settings | Platform |
| Secrets in CI/CD | GitHub/GitLab secrets | Org/repo secret settings | Platform |
| OIDC Federation | Workload identity for CI | `.github/workflows/*.yml` | Platform |

---

## Evidence Collection Matrix

For audit purposes, this maps controls to evidence locations.

| Control Domain | Automated Evidence | Manual Evidence | Collection Frequency |
|----------------|-------------------|-----------------|---------------------|
| Access Control | IAM reports, IdP exports | Access review records | Weekly / Quarterly |
| Network Security | Security group exports, VPC configs | Architecture diagrams | On change / Annually |
| Vulnerability Management | Scanner exports | Remediation records | Daily / Monthly |
| Logging | Log retention reports | Log review records | Daily / Monthly |
| Encryption | KMS key reports, TLS scans | Encryption policy | Monthly / Annually |
| Change Management | Git history, deployment logs | Change tickets | On change |
| Incident Response | Incident tickets | Postmortem docs | Per incident |
| Training | LMS completion reports | Training materials | Quarterly |

---

## Repository Index

### Infrastructure Repositories

| Repository | Purpose | Primary Owner |
|------------|---------|---------------|
| `infrastructure/terraform` | Core infrastructure as code | Platform |
| `infrastructure/kubernetes` | Kubernetes configurations | Platform |
| `infrastructure/vault` | Secrets management | Platform |
| `infrastructure/okta-terraform` | Identity provider config | IT |
| `infrastructure/monitoring` | Observability stack | SRE |

### Security Repositories

| Repository | Purpose | Primary Owner |
|------------|---------|---------------|
| `security/detections` | SIEM detection rules | Security Eng |
| `security/policies` | Security policy as code | Security Eng |
| `security/tools` | Security automation tools | Security Eng |
| `security/forensics` | Forensic scripts and tools | Security Eng |
| `security-operating-model` | This documentation | Security |

### Application Repositories

| Repository | Purpose | Security Contact |
|------------|---------|------------------|
| `app/api` | Main API service | [Team lead] |
| `app/frontend` | Web application | [Team lead] |
| `app/worker` | Background jobs | [Team lead] |
| `shared/libraries` | Shared code libraries | [Team lead] |

---

## Change Impact Analysis

When modifying security controls, assess impact using this matrix.

| Change Type | Repositories Affected | Review Required | Testing Required |
|-------------|----------------------|-----------------|------------------|
| IAM policy change | `aws-iam/`, affected services | Security | Non-prod validation |
| Network rule change | `terraform/`, `security-groups/` | Security + Platform | Non-prod, connectivity test |
| Encryption change | `kms/`, affected services | Security | Key rotation test |
| Logging change | `logging/`, `siem/` | Security | Log flow validation |
| Scanner rule change | `.semgrep/`, CI workflows | Security | CI pipeline test |
| Detection rule change | `detections/` | Security | Detection validation |

---

## Automation and Tooling

### Policy-as-Code Tools

| Tool | Purpose | Configuration Location |
|------|---------|----------------------|
| Open Policy Agent | Infrastructure policies | `security/policies/opa/` |
| Sentinel | Terraform policies | `infrastructure/sentinel/` |
| Kyverno | Kubernetes policies | `kubernetes/kyverno/` |
| Checkov | IaC scanning | `.checkov.yml` |
| tfsec | Terraform security | `.tfsec.yml` |
| Semgrep | Code analysis | `.semgrep/` |

### Compliance Automation

| Tool | Purpose | Output Location |
|------|---------|-----------------|
| Prowler | AWS security audit | `security/reports/prowler/` |
| ScoutSuite | Cloud security audit | `security/reports/scoutsuite/` |
| Lynis | System hardening audit | `security/reports/lynis/` |
| Drata/Vanta | Compliance automation | SaaS platform |

---

## Maintenance

### Review Schedule

| Component | Review Frequency | Reviewer |
|-----------|------------------|----------|
| This mapping document | Quarterly | Security Eng |
| Repository access | Quarterly | Security + Engineering |
| Detection rules | Monthly | Security Eng |
| Policy-as-code rules | Monthly | Security Eng |
| Infrastructure configs | On change | Platform + Security |

### Update Process

1. Changes to security controls must update this mapping
2. Pull requests affecting security require security review
3. Major changes require architecture review
4. All changes tracked in version control
