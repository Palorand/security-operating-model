# Evaluate This Operating Model in 10 Minutes

This guide is for reviewers who want to quickly assess whether this security operating model demonstrates real-world governance capability.

---

## The 10-Minute Path

### Minutes 1-3: Strategic Foundation

Start with [01-north-star-and-principles.md](01-north-star-and-principles.md):

- Is there a clear security mission tied to business outcomes?
- Are the principles actionable, not generic platitudes?
- Are there explicit "we will not" statements showing trade-off awareness?

**What to look for:** Specificity. Generic principles like "protect customer data" mean nothing. Look for statements that would actually guide decisions.

### Minutes 4-6: Risk Thinking

Review [03-risk-prioritization.md](03-risk-prioritization.md):

- Is the risk framework simple enough to actually use?
- Are the example risks specific to a realistic context?
- Is there clear ownership and treatment status?

**What to look for:** Evidence of prioritization. A risk register with everything marked "High" shows no thinking. Look for differentiation and rationale.

### Minutes 7-8: Execution Discipline

Skim [06-kpis-and-metrics.md](06-kpis-and-metrics.md):

- Are there fewer than 15 metrics? (More = vanity metrics)
- Does each metric have a clear measurement method?
- Are there anti-gaming notes showing awareness of Goodhart's Law?

**What to look for:** Metrics that would actually change behavior. "Number of vulnerabilities found" is vanity. "P1 vulnerabilities open beyond SLA" drives action.

### Minutes 9-10: Governance Reality

Check [08-exceptions-and-risk-acceptance.md](08-exceptions-and-risk-acceptance.md):

- Is there a process for when controls can't be followed?
- Are exceptions timeboxed with expiration?
- Is there business ownership of accepted risks?

**What to look for:** Acknowledgment that security isn't absolute. Organizations that claim 100% compliance are either lying or blocking business entirely.

---

## Red Flags to Watch For

| Red Flag | Why It Matters |
|----------|----------------|
| No exceptions process | Either blocking business or controls aren't enforced |
| Generic threat list | Copy-pasted from frameworks, not contextualized |
| 50+ KPIs | Measuring everything means prioritizing nothing |
| No ownership column | Risks without owners don't get treated |
| Compliance-only focus | Checking boxes vs. actually reducing risk |
| No trade-offs documented | Unrealistic or not battle-tested |

---

## Green Flags That Show Depth

| Green Flag | What It Demonstrates |
|------------|---------------------|
| Explicit refusals | Knows what NOT to do |
| Compensating controls | Understands defense in depth |
| Anti-gaming notes on metrics | Experienced with metric dysfunction |
| Business context in risks | Translates technical to business impact |
| RACI with real roles | Actually thought about organizational fit |
| Evidence requirements | Thinks about audit and verification |

---

## Questions This Model Should Answer

If you're evaluating someone's security leadership capability, this model should demonstrate they can answer:

1. **"What are your top 3 security priorities and why?"**
   - See: Risk prioritization, 90-day plan

2. **"How do you handle exceptions to security policy?"**
   - See: Exceptions and risk acceptance

3. **"What metrics do you report to leadership?"**
   - See: KPIs and metrics

4. **"How does security work with engineering?"**
   - See: Operating model and RACI, security review process

5. **"How do you handle incidents?"**
   - See: Incident operating loop

6. **"How do you approach compliance?"**
   - See: ISO 27001 in practice, mapping directory

---

## What This Model Intentionally Excludes

This is a governance framework, not:

- A security awareness training program
- Tool-specific configuration guides
- Penetration testing methodology
- Detailed incident playbooks
- Vendor selection criteria

Those are implementation details that vary by organization. This model provides the structure within which those details fit.

---

## Next Steps After Quick Evaluation

If the 10-minute review looks solid, go deeper on:

1. **[02-threat-landscape.md](02-threat-landscape.md)** - Is the threat model realistic for the stated context?
2. **[07-operating-model-and-raci.md](07-operating-model-and-raci.md)** - Does the org model make sense?
3. **[mapping/iso27001-annexA-to-controls.md](../mapping/iso27001-annexA-to-controls.md)** - Is compliance actually mapped to controls?
4. **[decision-memos/](../decision-memos/)** - Do the example decisions show good judgment?
