# Evolution and Lessons Learned

This document captures how this operating model evolved over time, what failed, and what we learned along the way. Security frameworks that only show successes aren't credible - the real learning comes from failures.

---

## Framework Evolution Timeline

### Phase 1: The Checklist Era (Year 1)

**What we tried:**
- Started with a comprehensive 200+ control checklist based on ISO 27001 and CIS
- Attempted to implement everything at once
- Created detailed policies that nobody read

**What failed:**
- Engineering teams ignored the checklist - too long, not actionable
- Policies sat in Confluence gathering dust
- Security became the "department of no"
- We had 100% policy coverage and maybe 20% actual implementation

**Key lesson:** Comprehensive doesn't mean effective. A shorter list of enforced controls beats a longer list of documented-but-ignored controls.

### Phase 2: The Automation Obsession (Year 2)

**What we tried:**
- Automated everything - scanning, alerting, blocking
- Implemented 15+ security tools
- Created dashboards with 50+ metrics
- Set up alerts for every possible violation

**What failed:**
- Alert fatigue became crippling - 500+ alerts/day, most ignored
- Tools overlapped, creating duplicate findings
- Engineers started working around automated blocks
- We measured everything but improved nothing

**Key lesson:** Automation without prioritization creates noise. Fewer tools, configured well, beat many tools configured poorly.

### Phase 3: Risk-Based Pragmatism (Current)

**What changed:**
- Reduced to 10 KPIs that actually drive behavior
- Implemented exception process to work WITH the business
- Focused on high-impact controls first
- Built relationships instead of walls

**What's working:**
- Engineering teams actually engage with security
- Exception process surfaces real problems
- Metrics show improvement, not just activity
- Security is invited to design discussions, not just audits

---

## Failed Initiatives

### The "Security Champions" Program v1

**What we tried:** Mandatory security champion in every team, required to attend weekly 2-hour training sessions.

**Why it failed:**
- Champions were voluntold, not volunteers
- 2 hours/week was too much commitment
- No recognition or career benefit
- Champions became resentful liaisons, not advocates

**What we learned:** Security champions must be volunteers with genuine interest. Keep time commitment under 2 hours/month. Provide real career benefits (training, certifications, recognition).

**Current approach:** Optional program, 1 hour/month sync, champions get priority access to security training budget and conference attendance.

---

### The "Shift Everything Left" Initiative

**What we tried:** Block all deployments with any security finding. Mandatory security sign-off on every PR.

**Why it failed:**
- Deployment velocity dropped 60%
- Security team became bottleneck (2-day PR review backlog)
- Engineers started batching changes to avoid reviews
- Low-severity findings blocked critical hotfixes
- Relationship with engineering cratered

**What we learned:** Shift left doesn't mean block everything left. Severity matters. Trust but verify. Async tooling beats synchronous gates for most cases.

**Current approach:** Automated scanning with severity-based blocking (only Critical/High block merge). Security review for architecture changes, not every PR. SLA-based remediation instead of deployment blocking.

---

### The Comprehensive Vendor Assessment Program

**What we tried:** 200-question security questionnaire for every vendor. Required SOC 2 Type II for all tools. 6-week assessment process.

**Why it failed:**
- Teams started using shadow IT to avoid the process
- Small but critical vendors couldn't provide SOC 2
- 6 weeks was too slow for business needs
- We assessed vendors nobody actually selected

**What we learned:** Risk-based vendor assessment. Tier vendors by data access and criticality. Fast-track for low-risk tools. Focus assessment effort where data exposure is highest.

**Current approach:** 3-tier system. Tier 1 (critical data): full assessment. Tier 2 (internal data): abbreviated questionnaire. Tier 3 (no sensitive data): self-attestation only.

---

## Metrics We Abandoned

### "Number of Vulnerabilities Found"

**Why we tracked it:** Seemed like a good measure of security tooling effectiveness.

**Why we stopped:** Teams gamed it by running more scans on the same code. High numbers looked bad even when we were improving. Created perverse incentive to not look for issues.

**Replaced with:** Vulnerabilities open beyond SLA (measures remediation, not discovery).

---

### "Security Training Completion Rate"

**Why we tracked it:** Compliance requirement, seemed important.

**Why we stopped:** 95% completion, 5% retention. People clicked through to complete, learned nothing. Completion != competence.

**Replaced with:** Phishing simulation resilience + role-specific practical assessments. Still track completion for compliance, but don't pretend it measures security awareness.

---

### "Mean Time to Detect" (as a primary metric)

**Why we tracked it:** Industry standard metric, shows detection capability.

**Why we deprioritized:** Survivorship bias - only measures detected incidents. Improved MTTD might mean we're missing less, or might mean attackers are noisier. Can't tell the difference.

**Current approach:** Still track MTTD but supplement with red team exercises to measure actual detection coverage. MTTD is a secondary metric, not a KPI.

---

### "Percentage of Systems Compliant"

**Why we tracked it:** Executive dashboard staple.

**Why we stopped:** Binary compliant/non-compliant hides nuance. A system 95% compliant with one critical gap looks the same as a system 95% compliant with minor issues. Led to focusing on easy wins to improve percentage while ignoring hard problems.

**Replaced with:** Risk-weighted compliance score + explicit tracking of critical control gaps.

---

## Processes That Didn't Scale

### Manual Access Reviews

**At 50 employees:** Quarterly manual review of all access, manageable.

**At 200 employees:** Quarterly review became a 3-week project. Reviewers rubber-stamped to finish. Quality degraded as volume increased.

**Current approach:** Automated access review reminders with manager self-service. Quarterly review only for privileged access. Annual review for standard access. Automated detection of unused permissions.

---

### Security Review for All Changes

**At 5 services:** Security reviewed every significant change. High quality, no bottleneck.

**At 30 services:** Security became a 2-week bottleneck. Reviews rushed. Engineers frustrated. Quality actually decreased despite more process.

**Current approach:** Self-service security checklist for standard changes. Security review only for: new services, auth changes, data classification changes, public exposure. Trust teams for the rest, verify with automated scanning.

---

## Incidents That Shaped This Framework

### The "Temporary" Admin Credentials Incident

**What happened:** Developer created admin credentials for debugging. "Temporary" credentials stayed active for 8 months. Used in a breach.

**Impact:** 3-week incident response, customer notification, regulatory inquiry.

**What we changed:**
- All credentials must have expiration (max 90 days)
- Automated scanning for long-lived credentials
- Decision memo DM-002 (Secrets Management Standard)

---

### The Public S3 Bucket Incident

**What happened:** Engineer made bucket public for quick file sharing with external partner. Forgot to revert. Contained customer data exports.

**Impact:** 72-hour exposure window, customer notification, near-miss on major breach.

**What we changed:**
- Deny public exposure by default (Decision memo DM-001)
- SCPs blocking public bucket creation
- CSPM alerting on any public exposure
- Exception process for legitimate public resources

---

### The "It's Just Staging" Incident

**What happened:** Staging environment had production-like data (for realistic testing). Lower security controls because "it's just staging." Staging credentials leaked. Attackers pivoted to production.

**Impact:** Full incident response, unclear initially whether production was compromised, significant investigation effort.

**What we changed:**
- Same security controls in staging as production
- Data masking for non-production environments
- Network segmentation between environments
- "Staging is production" mindset in risk prioritization

---

### The Exception That Wasn't

**What happened:** Exception granted for legacy system. 90-day timeline. No follow-up process. Exception "renewed" via email for 18 months. System eventually breached via the excepted control gap.

**Impact:** Breach through known gap, audit finding, loss of credibility.

**What we changed:**
- All exceptions in tracking system with automated expiration
- Maximum 3 renewals (Decision memo DM-003)
- Convert to formal risk acceptance or remediate
- No more email-based exception renewals

---

## Cultural Lessons

### What Changed Our Relationship with Engineering

**Before:** Security as gatekeeper. Engineering sees us as blockers. Adversarial relationship.

**Turning point:** Started saying "yes, and here's how to do it securely" instead of "no." Provided secure-by-default templates. Made the secure path the easy path.

**After:** Security invited to design discussions. Engineers ask for advice, not just sign-off. Collaborative relationship.

**Key insight:** Every "no" should come with an alternative. If you can't offer an alternative, question whether the "no" is justified.

---

### On Metrics and Goodhart's Law

> "When a measure becomes a target, it ceases to be a good measure."

Every metric we've set as a target has been gamed. Not maliciously - people optimize for what's measured.

**Our approach now:**
- Anti-gaming notes on every KPI
- Rotate focus metrics to prevent over-optimization
- Qualitative review alongside quantitative metrics
- Celebrate risk reduction, not metric improvement

---

### On Compliance vs. Security

**Hard-learned truth:** You can be compliant and insecure. You can be secure and non-compliant. The overlap is smaller than auditors suggest.

**Our approach:** Use compliance as a floor, not a ceiling. Pass audits, but don't confuse audit readiness with actual security posture. Compliance is evidence of process. Security is evidence of outcomes.

---

## What We're Still Getting Wrong

Intellectual honesty requires acknowledging current gaps:

1. **Third-party risk is still reactive** - We assess vendors at onboarding but ongoing monitoring is weak
2. **Detection coverage has gaps** - Red team consistently finds blind spots we haven't addressed
3. **Data classification is inconsistent** - Policy exists, enforcement is spotty
4. **Security debt accumulates** - We're better at finding issues than fixing them
5. **Metrics don't capture everything** - Some important things aren't measurable

This framework is a work in progress. It will continue to evolve as we learn more about what works and what doesn't in our context.

---

## Advice for Others

If you're building a security program:

1. **Start with relationships, not policies** - Trust enables everything else
2. **Fewer controls, actually enforced** - beats comprehensive controls on paper
3. **Make the secure path the easy path** - Friction creates workarounds
4. **Measure outcomes, not activities** - What changed, not what you did
5. **Document your failures** - They're more valuable than your successes
6. **Context matters** - Copy frameworks critically, not blindly
7. **Security is a journey** - There's no "done" state
