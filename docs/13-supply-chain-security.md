# Supply Chain Security

This document defines our approach to managing security risks in the software supply chain, including dependencies, build systems, and third-party code.

---

## Why Supply Chain Security Matters

Modern software is built on dependencies. A typical application might have:
- 50-200 direct dependencies
- 500-2000 transitive dependencies
- Build tools, CI/CD systems, container base images
- Third-party APIs and services

Each dependency is a potential attack vector. Supply chain attacks (SolarWinds, Log4j, Codecov, ua-parser-js) have shown that attackers increasingly target the software supply chain.

---

## Threat Model

### Attack Vectors

| Vector | Description | Example |
|--------|-------------|---------|
| Compromised package | Attacker gains control of legitimate package | ua-parser-js npm hijack |
| Typosquatting | Malicious package with similar name | `crossenv` vs `cross-env` |
| Dependency confusion | Private package name published publicly | Internal package overridden |
| Compromised maintainer | Maintainer account compromised | event-stream incident |
| Build system compromise | CI/CD system compromised | Codecov bash uploader |
| Malicious contribution | Malicious code in PR gets merged | Subtle backdoors |

### Risk Assessment

| Risk | Likelihood | Impact | Priority |
|------|------------|--------|----------|
| Known vulnerability in dependency | High | Medium-High | P1 |
| Compromised popular package | Low | Critical | P1 |
| Typosquatting attack | Medium | High | P2 |
| Dependency confusion | Medium | High | P2 |
| Build system compromise | Low | Critical | P2 |
| Malicious contribution | Low | Medium | P3 |

---

## Controls

### 1. Dependency Scanning (SCA)

**Objective:** Identify known vulnerabilities in dependencies.

**Implementation:**
- Scan all repositories for vulnerable dependencies
- Scan on every PR and on schedule (daily)
- Block merges for critical/high vulnerabilities in new dependencies
- Alert on new vulnerabilities in existing dependencies

**Tools:** Dependabot, Snyk, or similar

**SLA for remediation:**

| Severity | SLA | Action |
|----------|-----|--------|
| Critical | 7 days | Immediate upgrade or removal |
| High | 30 days | Planned upgrade |
| Medium | 90 days | Best effort |
| Low | Best effort | Track only |

**Current gaps:**
- Some legacy repositories not yet onboarded
- Transitive dependency visibility limited
- No automated PR creation for updates (planned)

---

### 2. Dependency Pinning and Lock Files

**Objective:** Ensure reproducible builds and prevent unexpected updates.

**Requirements:**
- All projects must use lock files (package-lock.json, yarn.lock, Pipfile.lock, go.sum)
- Lock files must be committed to version control
- CI must verify lock file integrity
- No floating version ranges in production dependencies

**Verification:**
- CI check fails if lock file is missing or out of sync
- Periodic audit of version pinning practices

---

### 3. Private Package Registry

**Objective:** Control what packages can be installed and prevent dependency confusion.

**Implementation:**
- Internal packages published to private registry
- Public packages mirrored/proxied through private registry
- Namespace reservation for internal package names on public registries
- Registry configured as the only allowed source

**Current state:** Partially implemented
- Private registry operational for npm
- Python and other ecosystems still using public directly
- Dependency confusion risk not fully mitigated

---

### 4. SBOM (Software Bill of Materials)

**Objective:** Know what's in our software for vulnerability response and compliance.

**Implementation:**
- Generate SBOM for every release
- SBOM includes direct and transitive dependencies
- SBOM stored alongside release artifacts
- SBOM format: CycloneDX or SPDX

**Use cases:**
- Rapid response to new vulnerabilities (Log4j-style)
- Customer security questionnaires
- Compliance requirements
- License compliance

**Current state:** Planned for Q2
- Tool selected (Syft)
- Integration into CI/CD pending

---

### 5. Artifact Signing

**Objective:** Verify integrity and provenance of build artifacts.

**Implementation:**
- Sign container images with Cosign
- Sign release artifacts with GPG
- Verify signatures before deployment
- Store signatures in transparency log (Rekor)

**Current state:** Partially implemented
- Container signing operational for production images
- Other artifacts not yet signed

---

### 6. Build System Security

**Objective:** Protect CI/CD systems from compromise.

**Controls:**

| Control | Status |
|---------|--------|
| CI/CD runs in isolated environments | Implemented |
| No long-lived credentials in CI/CD | In progress (OIDC migration) |
| Build logs reviewed for secrets | Implemented |
| Self-hosted runners hardened | Implemented |
| Third-party actions pinned to SHA | Partial |
| Workflow changes require approval | Implemented |

**Risks:**
- GitHub Actions from third parties (pinned to SHA, but still risk)
- Build environment shared across projects (isolation via containers)

---

### 7. Code Review for Dependencies

**Objective:** Human review of significant dependency changes.

**When required:**
- New direct dependencies
- Major version upgrades
- Dependencies with low reputation/maintainer trust
- Dependencies with sensitive access (crypto, network, filesystem)

**Review checklist:**
- [ ] Is this dependency necessary? Can we avoid it?
- [ ] Is the package actively maintained?
- [ ] How many maintainers? Bus factor?
- [ ] Any security history? Past vulnerabilities?
- [ ] What permissions/access does it require?
- [ ] Is the license compatible?
- [ ] How many downloads/stars? (popularity as weak signal)

---

### 8. Container Security

**Objective:** Secure container supply chain from base image to runtime.

**Controls:**

| Control | Implementation | Status |
|---------|----------------|--------|
| Approved base images only | Internal registry with curated images | Implemented |
| Base image scanning | Trivy scan of base images | Implemented |
| Minimal base images | Distroless or Alpine where possible | Partial |
| No root in containers | USER directive required | Implemented |
| Image scanning before deploy | Trivy in CI/CD | Planned Q1 |
| Runtime scanning | Falco or similar | Not implemented |

**Approved base images:**
- `gcr.io/distroless/base`
- `gcr.io/distroless/java`
- Internal hardened images based on Alpine

---

### 9. Third-Party Code Review

**Objective:** Review code from outside contributors before merge.

**Requirements:**
- All external contributions require maintainer review
- Commits from non-employees flagged for extra scrutiny
- No auto-merge for external PRs
- DCO or CLA for open source projects

---

## Incident Response for Supply Chain

### If a dependency is compromised:

1. **Identify exposure**
   - Check SBOM: Do we use this package?
   - Check versions: Are we on affected version?
   - Check deployment: Where is it running?

2. **Contain**
   - Block deployment of affected version
   - Identify all affected systems
   - Assess if compromise was exploited

3. **Remediate**
   - Upgrade to fixed version
   - If no fix, remove dependency or implement workaround
   - Verify fix deployed everywhere

4. **Communicate**
   - Internal notification to affected teams
   - Customer notification if data at risk
   - Postmortem and lessons learned

### Response time targets:

| Scenario | Detection | Containment | Remediation |
|----------|-----------|-------------|-------------|
| Critical CVE in direct dependency | < 4 hours | < 8 hours | < 24 hours |
| Critical CVE in transitive dependency | < 24 hours | < 48 hours | < 7 days |
| Compromised package (active exploit) | Immediate | < 4 hours | < 24 hours |

---

## Metrics

| Metric | Target | Current |
|--------|--------|---------|
| Dependencies with known critical/high CVE | 0 | 3 |
| Average age of dependency vulnerabilities | < 30 days | 45 days |
| Repositories with SCA enabled | 100% | 85% |
| Lock file compliance | 100% | 92% |
| SBOM generation coverage | 100% | 0% (planned) |
| Container image signing coverage | 100% | 60% |

---

## Vendor/Dependency Evaluation

### For new dependencies, evaluate:

**Maintenance health:**
- Last commit date
- Release frequency
- Open issue/PR count and response time
- Number of maintainers

**Security posture:**
- Security policy (SECURITY.md)
- Vulnerability disclosure process
- Past security issues and response
- Signed releases

**Trust signals:**
- Package age
- Download counts
- Corporate backing or foundation membership
- Used by other reputable projects

**Red flags:**
- Single maintainer with no succession plan
- No releases in > 1 year
- History of malicious versions
- Excessive permissions requested
- Obfuscated or suspicious code

---

## Responsibilities

| Role | Responsibility |
|------|----------------|
| Engineering teams | Choose and update dependencies, respond to vulnerability alerts |
| Security Engineering | Tooling, scanning, policy, incident response |
| Platform | Build system security, registry management |
| GRC | License compliance, vendor assessment for commercial components |

---

## Current Gaps and Roadmap

### Gaps

1. **SBOM not generated** - Can't quickly answer "do we use X?" during incidents
2. **Transitive dependency visibility limited** - Deep dependencies not fully tracked
3. **No dependency confusion protection** for Python ecosystem
4. **Container scanning not in deployment pipeline** - Only at build time
5. **No runtime supply chain monitoring** - Would not detect compromised dependency at runtime

### Roadmap

| Initiative | Quarter | Owner |
|------------|---------|-------|
| SBOM generation in CI/CD | Q1 | Security Eng |
| Container scanning in deployment | Q1 | Platform |
| Private registry for Python | Q2 | Platform |
| Dependency review automation | Q2 | Security Eng |
| Runtime monitoring evaluation | Q3 | Security Eng |

---

## References

- SLSA Framework (https://slsa.dev)
- NIST SSDF (Secure Software Development Framework)
- OpenSSF Scorecard
- Sigstore project
