# 90-Day Security Plan

This document outlines the initial 90-day execution plan for establishing or improving a security program.

---

## Objectives

By day 90, we will have:

1. Visibility into current security posture
2. Critical gaps identified and prioritized
3. Quick wins delivered to build momentum
4. Foundation laid for longer-term initiatives
5. Relationships established with key stakeholders

---

## Days 1-30: Discovery and Quick Wins

### Week 1: Orientation

| Task | Outcome | Owner |
|------|---------|-------|
| Meet with engineering leadership | Understand priorities, pain points, and culture | Security Lead |
| Review existing security documentation | Identify what exists vs. gaps | Security Lead |
| Get access to security tools and dashboards | Baseline visibility established | Security Lead |
| Identify key stakeholders across teams | Stakeholder map created | Security Lead |
| Review recent incidents and postmortems | Understand historical issues | Security Lead |

### Week 2: Assessment

| Task | Outcome | Owner |
|------|---------|-------|
| Inventory production systems and data flows | Asset inventory draft | Security Eng |
| Review IAM configuration and access patterns | IAM findings documented | Security Eng |
| Assess CI/CD pipeline security | Pipeline security gaps identified | Security Eng |
| Review cloud security posture (CSPM) | Top misconfigurations listed | Security Eng |
| Evaluate logging and monitoring coverage | Visibility gaps documented | Security Eng |

### Week 3-4: Quick Wins

| Quick Win | Impact | Effort | Status |
|-----------|--------|--------|--------|
| Enable MFA on all admin accounts | High | Low | |
| Enable secret scanning on repositories | High | Low | |
| Block public S3 bucket creation | High | Low | |
| Enable CloudTrail in all regions | High | Low | |
| Deploy default security group with no rules | Medium | Low | |
| Enable GuardDuty | High | Low | |
| Set password policy to industry standard | Medium | Low | |
| Enable audit logging on critical SaaS apps | Medium | Low | |

### Day 30 Deliverables

- [ ] Security posture assessment report
- [ ] Prioritized risk register (initial)
- [ ] Quick wins status report
- [ ] 60-day plan refinement
- [ ] Stakeholder communication sent

---

## Days 31-60: Foundation Building

### Weeks 5-6: Process Establishment

| Task | Outcome | Owner |
|------|---------|-------|
| Define security review process for new projects | Process documented, first reviews scheduled | Security Lead |
| Establish vulnerability management SLAs | SLAs agreed with engineering | Security Lead |
| Create exception request process | Template and workflow in place | Security Lead |
| Set up security metrics dashboard | Initial KPIs visible | Security Eng |
| Define incident response roles | RACI documented | Security Lead |

### Weeks 7-8: Technical Foundation

| Task | Outcome | Owner |
|------|---------|-------|
| Implement SAST in CI/CD pipeline | Scanning enabled, baseline established | Security Eng |
| Deploy dependency scanning (SCA) | Known vulnerable dependencies identified | Security Eng |
| Establish secrets management approach | Vault or equivalent configured | Security Eng |
| Implement centralized logging | Security logs aggregated | Security Eng |
| Create security alerting baseline | Critical alerts configured | Security Eng |

### Day 60 Deliverables

- [ ] Security review process operational
- [ ] Vulnerability management SLAs documented
- [ ] CI/CD security gates implemented
- [ ] Centralized logging operational
- [ ] Security dashboard with initial metrics
- [ ] 90-day plan refinement

---

## Days 61-90: Operationalization

### Weeks 9-10: Governance

| Task | Outcome | Owner |
|------|---------|-------|
| Conduct first security reviews | 3+ reviews completed | Security Lead |
| Process first exception requests | Workflow validated | Security Lead |
| Run tabletop incident response exercise | Gaps identified, runbooks updated | Security Lead |
| Establish regular security sync with engineering | Recurring meeting scheduled | Security Lead |
| Draft security principles document | Principles documented | Security Lead |

### Weeks 11-12: Measurement and Reporting

| Task | Outcome | Owner |
|------|---------|-------|
| Generate first monthly security report | Report delivered to leadership | Security Lead |
| Review and refine KPIs | Metrics validated as useful | Security Lead |
| Document security architecture | Architecture diagrams created | Security Eng |
| Create security onboarding for new engineers | Onboarding content ready | Security Lead |
| Plan Q2 roadmap | Quarterly objectives defined | Security Lead |

### Day 90 Deliverables

- [ ] Monthly security report (first edition)
- [ ] Security principles document
- [ ] Incident response runbooks (critical scenarios)
- [ ] Security architecture documentation
- [ ] Q2 roadmap with prioritized initiatives
- [ ] 90-day retrospective

---

## Success Criteria

| Criterion | Target | Measurement |
|-----------|--------|-------------|
| Critical vulnerabilities | < 10 open beyond SLA | Vulnerability scanner |
| Secret scanning coverage | 100% of active repos | GitHub/GitLab metrics |
| MFA adoption | 100% of privileged accounts | IAM audit |
| Security review completion | 100% of new projects | Review tracker |
| Incident response test | 1 tabletop completed | Exercise record |
| Stakeholder satisfaction | No major complaints | Informal feedback |

---

## Risk and Dependencies

### Risks to Plan

| Risk | Mitigation |
|------|------------|
| Engineering pushback on new processes | Early engagement, demonstrate value, start with high-risk areas |
| Tool procurement delays | Start with open source or existing tools; defer advanced tooling |
| Resource constraints | Prioritize ruthlessly; defer nice-to-haves |
| Major incident during ramp-up | Have basic IR process ready by day 14 |

### Dependencies

| Dependency | Impact if Delayed |
|------------|-------------------|
| Access to production systems | Assessment delayed |
| Engineering cooperation | Process adoption blocked |
| Budget approval for tools | Technical improvements limited |
| Leadership support | Governance authority undermined |

---

## Communication Plan

| Audience | Frequency | Content |
|----------|-----------|---------|
| Security team | Daily standup | Task progress, blockers |
| Engineering leads | Weekly | Security review queue, findings trends |
| Leadership | Bi-weekly | Progress against plan, escalations |
| All engineering | Day 30, 60, 90 | Summary of changes and expectations |

---

## Post-90 Day Transition

At day 90, transition from "establishment mode" to "operating mode":

- Shift from discovery to continuous improvement
- Move from ad-hoc to scheduled security activities
- Transition from individual heroics to team processes
- Begin measuring against established baselines

The [12-month roadmap](05-12-month-roadmap.md) picks up from here.
