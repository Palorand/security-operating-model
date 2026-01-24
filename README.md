# Security Operating Model

[![ISO 27001](https://img.shields.io/badge/ISO_27001-Aligned-0052CC.svg?logo=iso)](https://www.iso.org/isoiec-27001-information-security.html)
[![NIST CSF](https://img.shields.io/badge/NIST_CSF-Referenced-003366.svg)](https://www.nist.gov/cyberframework)
[![Risk-Based](https://img.shields.io/badge/Approach-Risk_Based-critical.svg)]()
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

This repository contains the security operating model I've developed and refined over several years leading security programs at scale-ups and mid-size companies. It started as internal documentation that I kept copying between roles, so I decided to consolidate it into something reusable.

The goal is pragmatic security governance that actually works in engineering-driven organizations, not compliance theater.

---

## TL;DR

**What this demonstrates:**
- Strategic thinking: threat landscape tied to business context, not generic risk lists
- Prioritization discipline: risk scoring that drives resource allocation
- Execution focus: 90-day plans and 12-month roadmaps with measurable outcomes
- Governance that scales: exception handling, risk acceptance, security reviews
- Engineering alignment: security integrated into SDLC, not bolted on
- Honest retrospection: what failed, what we abandoned, and what we learned

**Quick evaluation path:**

```
Start here:
  docs/01-north-star-and-principles.md    # What we optimize for
  docs/03-risk-prioritization.md          # How we decide what matters

Then validate execution:
  docs/06-kpis-and-metrics.md             # How we measure progress
  docs/08-exceptions-and-risk-acceptance.md  # How we handle reality

Check what we learned the hard way:
  docs/12-evolution-and-lessons-learned.md   # Failures and abandoned approaches
  docs/postmortems/                          # Real incidents, anonymized

Finally, check compliance linkage:
  mapping/iso27001-annexA-to-controls.md  # ISO 27001 mapped to concrete controls
  mapping/controls-to-repos.md            # Controls mapped to implementation
```

---

## Security Highlights

<table>
<tr>
<td width="50%" valign="top">

### Strategic Foundation

| Element | Coverage |
|---------|----------|
| North Star | Clear security mission tied to business objectives |
| Principles | 8 non-negotiable security principles |
| Threat Model | Top 10 threats contextualized to organization type |
| Risk Framework | Impact x Likelihood with detectability factor |

</td>
<td width="50%" valign="top">

### Execution Model

| Element | Coverage |
|---------|----------|
| 90-Day Plan | Quick wins and foundational work |
| 12-Month Roadmap | Quarterly objectives with success criteria |
| KPIs | 10 actionable metrics with anti-gaming notes |
| Operating Rhythm | Weekly/monthly/quarterly ceremonies |

</td>
</tr>
<tr>
<td width="50%" valign="top">

### Governance

| Process | Purpose |
|---------|---------|
| Security Reviews | Design review gates in SDLC |
| Exception Handling | Timeboxed deviations with compensating controls |
| Risk Acceptance | Formal sign-off with business ownership |
| Incident Response | Triage through postmortem loop |

</td>
<td width="50%" valign="top">

### Compliance

| Standard | Approach |
|----------|----------|
| ISO 27001 | Annex A mapped with implementation gaps noted |
| Evidence | Automated where possible, governed otherwise |
| Audits | Continuous compliance, not annual scramble |
| Suppliers | Security questionnaire and assessment process |

</td>
</tr>
<tr>
<td width="50%" valign="top">

### Supply Chain

| Element | Coverage |
|---------|----------|
| Dependency Scanning | SCA with remediation SLAs |
| SBOM | Software bill of materials for each release |
| Artifact Signing | Container and release signature verification |
| Build Security | CI/CD hardening and secrets management |

</td>
<td width="50%" valign="top">

### Learning Culture

| Element | Coverage |
|---------|----------|
| Postmortems | Blameless incident retrospectives |
| Failed Initiatives | What we tried and abandoned |
| Metric Evolution | KPIs that didn't work and why |
| Framework Changes | How our approach evolved over time |

</td>
</tr>
</table>

---

## Why This Exists

I built this for a few reasons:

| Audience | What they get |
|----------|---------------|
| **Security leaders** | A starting point that's faster than building from scratch |
| **Engineering teams** | Clear expectations and processes they can actually follow |
| **Executives** | Visibility into security priorities and progress |
| **Auditors** | Evidence of a functioning security management system |

This isn't meant to be deployed as-is. Every organization has different threats, risk appetite, and constraints. The value is in the structure and the thinking behind it, which you adapt to your context.

---

## Repository Structure

```
security-operating-model/
├── README.md                           # You are here
├── docs/                               # Core strategic documents
│   ├── 00-evaluate-in-10min.md        # Quick assessment guide
│   ├── 01-north-star-and-principles.md
│   ├── 02-threat-landscape.md
│   ├── 03-risk-prioritization.md
│   ├── 04-90-day-plan.md
│   ├── 05-12-month-roadmap.md
│   ├── 06-kpis-and-metrics.md
│   ├── 07-operating-model-and-raci.md
│   ├── 08-exceptions-and-risk-acceptance.md
│   ├── 09-security-review-process.md
│   ├── 10-incident-operating-loop.md
│   ├── 11-iso27001-in-practice.md
│   ├── 12-evolution-and-lessons-learned.md
│   ├── 13-supply-chain-security.md
│   └── postmortems/                   # Anonymized incident learnings
│       └── PM-001-staging-database-exposure.md
├── templates/                          # Reusable governance artifacts
│   ├── risk-register.csv
│   ├── risk-acceptance.md
│   ├── exception-request.md
│   ├── security-design-review.md
│   ├── supplier-security-questionnaire.md
│   ├── kpi-dashboard-spec.md
│   ├── decision-memo.md
│   └── executive-security-report.md
├── decision-memos/                     # Example arbitration decisions
│   ├── DM-001-deny-public-exposure.md
│   ├── DM-002-secrets-management-standard.md
│   └── DM-003-exceptions-timebox.md
├── mapping/                            # Compliance and implementation linkage
│   ├── iso27001-annexA-to-controls.md
│   └── controls-to-repos.md
└── LICENSE
```

---

## Documentation Overview

| Document | Purpose |
|----------|---------|
| [00-evaluate-in-10min.md](docs/00-evaluate-in-10min.md) | Quick walkthrough for evaluators |
| [01-north-star-and-principles.md](docs/01-north-star-and-principles.md) | Security mission and non-negotiables |
| [02-threat-landscape.md](docs/02-threat-landscape.md) | Contextualized threat analysis |
| [03-risk-prioritization.md](docs/03-risk-prioritization.md) | Risk scoring methodology and register |
| [04-90-day-plan.md](docs/04-90-day-plan.md) | Initial execution roadmap |
| [05-12-month-roadmap.md](docs/05-12-month-roadmap.md) | Annual strategic objectives |
| [06-kpis-and-metrics.md](docs/06-kpis-and-metrics.md) | Security metrics that matter |
| [07-operating-model-and-raci.md](docs/07-operating-model-and-raci.md) | Organizational model and responsibilities |
| [08-exceptions-and-risk-acceptance.md](docs/08-exceptions-and-risk-acceptance.md) | Governance for deviations |
| [09-security-review-process.md](docs/09-security-review-process.md) | Design review methodology |
| [10-incident-operating-loop.md](docs/10-incident-operating-loop.md) | Incident response procedures |
| [11-iso27001-in-practice.md](docs/11-iso27001-in-practice.md) | Practical ISO 27001 implementation |
| [12-evolution-and-lessons-learned.md](docs/12-evolution-and-lessons-learned.md) | Framework evolution, failures, and what we learned |
| [13-supply-chain-security.md](docs/13-supply-chain-security.md) | Dependency and build pipeline security |

---

## Decision Memos

These document real arbitration decisions with full context on trade-offs:

| Decision | Summary |
|----------|---------|
| [DM-001](decision-memos/DM-001-deny-public-exposure.md) | Deny public exposure by default - policy-as-code enforcement |
| [DM-002](decision-memos/DM-002-secrets-management-standard.md) | Secrets management standard - short-lived credentials, no long-lived keys |
| [DM-003](decision-memos/DM-003-exceptions-timebox.md) | All exceptions are timeboxed - 90-day maximum with renewal process |

---

## Postmortems

Anonymized incident postmortems that shaped our current practices:

| Incident | Key Lesson |
|----------|------------|
| [PM-001](docs/postmortems/PM-001-staging-database-exposure.md) | Staging database exposed to internet - led to environment parity controls |

These are sanitized versions of real incidents. Names, dates, and identifying details have been changed, but the lessons are genuine.

---

## Standards Alignment

| Standard | Coverage |
|----------|----------|
| **ISO 27001:2022** | Annex A controls mapped to implementation |
| **NIST CSF** | Identify, Protect, Detect, Respond, Recover addressed |
| **SOC 2** | Trust Service Criteria alignment for SaaS contexts |
| **CIS Controls** | Implementation Groups 1-2 covered |

The [mapping/](mapping/) directory contains detailed control mappings.

---

## What This Doesn't Cover

This is a governance framework, not a complete security program:

- **Tool-specific configurations** - Adapt to your stack (AWS/GCP/Azure, specific SIEM, etc.)
- **Detailed runbooks** - Incident playbooks need to match your infrastructure
- **Penetration testing** - Scope and methodology depend on your architecture
- **Security awareness content** - Training materials are organization-specific
- **Vendor-specific integrations** - SSO, MDM, EDR configs vary by product

The operating model tells you *what* to do and *why*. The *how* depends on your technology choices.

---

## License

MIT. See [LICENSE](LICENSE).
