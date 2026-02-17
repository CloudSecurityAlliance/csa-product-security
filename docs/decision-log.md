# Decision Log

Key decisions made in establishing CSA's product security program, including alternatives considered and rationale.

## 2026-02-17: Use GitHub Private Vulnerability Reporting as the sole GitHub reporting channel

**Decision**: All vulnerability reports for CSA software on GitHub go through GitHub's Private Vulnerability Reporting (PVR). No other GitHub-based reporting mechanism (issues, discussions) is used for security vulnerabilities.

**Alternatives considered**:

- **GitHub Issues**: Public by default, which risks accidental disclosure of vulnerability details. Research shows only ~1% of open source projects use issues for security reporting, and reporters frequently disclose publicly by mistake. Rejected.
- **GitHub Discussions**: Also public by default. No structured workflow for triage, fix development, or advisory publication. Rejected.
- **GitHub Issues with a vulnerability template**: Slightly better than plain issues, but still public. The PVR form provides the same structured input with privacy by default. Rejected.
- **PVR + Issues as a secondary channel**: Adds complexity with no benefit. PVR covers the use case completely. Rejected.

**Rationale**: PVR is purpose-built for this. It is private by default, has a structured submission form, automatically credits reporters, integrates with GitHub's advisory publication system, and supports the full lifecycle (report → triage → fix → publish → update). It requires no external tools.

---

## 2026-02-17: Publish advisories openly and quickly by default

**Decision**: CSA's default is to publish security advisories publicly as soon as possible, even before a fix is available. Private advisories are the exception, not the rule.

**Alternatives considered**:

- **Standard coordinated disclosure (private until fix)**: The traditional model where advisories are only published after a fix is available. This is reasonable for commercial software, but CSA's software is open source. The code is already public, so keeping the advisory private while the vulnerable code is visible provides limited additional protection. Rejected as the default, but retained as an option for exceptional cases.
- **Strict 90-day embargo**: A fixed private window before disclosure. Overly rigid and not aligned with CSA's transparency goals. Rejected.

**Rationale**: CSA's software is largely open source. Openness and transparency are simpler to operate, consistent with open source norms, and honest about the realities of public code. The 90-day timeline exists as a maximum, not a target. GitHub's advisory system supports publishing early and updating later — the URL stays the same and the edit history stays private.

---

## 2026-02-17: Use GitHub-recommended security configuration with no customizations

**Decision**: Apply GitHub's recommended security configuration across the entire `CloudSecurityAlliance` organization with enforcement enabled and no customizations.

**Alternatives considered**:

- **Custom security configuration**: GitHub allows creating custom configurations with different feature toggles. CSA has no reason to deviate from the defaults — the recommended configuration enables all relevant free features. Rejected.
- **Per-repo configuration**: Configuring security features individually per repository. Does not scale — CSA has many repos and will have more. Rejected.

**Rationale**: The GitHub-recommended configuration enables PVR, Dependabot, code scanning, secret scanning, and push protection for all public repos at no cost. There is nothing to customize. Using the standard configuration is simpler to maintain, easier to document, and reduces the chance of misconfiguration.

---

## 2026-02-17: No bug bounties

**Decision**: CSA does not offer monetary rewards for vulnerability reports.

**Alternatives considered**:

- **Paid bug bounty program**: CSA is a nonprofit. The budget does not support it. Rejected.
- **Swag/merchandise rewards**: Adds procurement and shipping overhead for minimal benefit. Rejected.

**Rationale**: CSA is a nonprofit. GitHub's automatic credit on published advisories provides recognition. Researchers who report vulnerabilities to CSA are contributing to the security of a public-good organization.

---

## 2026-02-17: No separate acknowledgements page

**Decision**: CSA does not maintain a separate "hall of fame" or acknowledgements page for security researchers. Credit is handled through GitHub's native advisory credit mechanism.

**Alternatives considered**:

- **ACKNOWLEDGEMENTS.md in the repo**: A manually maintained list of researchers. Creates a maintenance burden and duplicates information already captured by GitHub's advisory system. Rejected.
- **Dedicated webpage**: Same issues as above, plus requires web team involvement to update. Rejected.

**Rationale**: When a PVR is submitted, GitHub automatically adds the reporter as a credited user on the advisory. When the advisory is published, the credit is public and permanent. This is the record. There is no need to maintain a separate list.

---

## 2026-02-17: SLAs to be defined later

**Decision**: CSA does not commit to specific response time SLAs at launch. The SLA document is a stub acknowledging this is being defined.

**Alternatives considered**:

- **Define SLAs immediately**: Risk committing to targets CSA cannot reliably meet without operational experience. Rejected.

**Rationale**: It is better to establish the program, gain operational experience, and then define commitments based on actual capacity. The SLA document will be updated when CSA is ready to make those commitments.

---

## 2026-02-17: Separate programs for GitHub software vs. web properties

**Decision**: CSA's product security program (this repo) covers software on GitHub. CSA web properties (cloudsecurityalliance.org, etc.) are covered by a separate process documented at [security.txt](https://cloudsecurityalliance.org/.well-known/security.txt) and [cloudsecurityalliance.org/security](https://cloudsecurityalliance.org/security).

**Alternatives considered**:

- **Single unified program**: Combining web property security and software product security into one process. The web properties are managed by different teams with different tooling (not GitHub-native). Forcing everything through one process would be awkward for both sides. Rejected.

**Rationale**: The two programs have different tooling, different teams, and different workflows. Keeping them separate is cleaner. The SECURITY.md and this repo's documentation cross-reference the web property security program so researchers can find the right channel regardless of where they start.

---

## 2026-02-17: Reference security.txt for non-GitHub security concerns

**Decision**: All references to CSA's non-GitHub security program point to the [security.txt](https://cloudsecurityalliance.org/.well-known/security.txt) file rather than directly to the website security page.

**Alternatives considered**:

- **Link directly to cloudsecurityalliance.org/security**: The security.txt already links to this page via its `Policy:` field. Linking to security.txt is more standards-compliant and the security.txt is the canonical entry point per RFC 9116. Rejected as the primary link.

**Rationale**: security.txt (RFC 9116) is the standard machine-readable mechanism for security contact discovery. It is the canonical reference point. Humans who click the link will find the contact information and policy URL in the security.txt content. Consistently referencing security.txt reinforces standards compliance.

---

## 2026-02-17: Use GHSA as primary identifier, request CVE IDs through GitHub

**Decision**: CSA uses GitHub's native GHSA identifiers (e.g., `GHSA-xxxx-xxxx-xxxx`) as the primary advisory identifier. CSA also requests CVE IDs through GitHub's advisory workflow for published advisories where appropriate. Both identifiers are included in published advisories.

**Alternatives considered**:

- **CSA-YYYY-NNN identifiers**: A CSA-specific advisory numbering scheme (e.g., `CSA-2026-001`). This would require manual assignment, tracking of sequential numbers, and maintaining a mapping between CSA IDs, GHSA IDs, and CVE IDs. Rejected.
- **CVE IDs as primary, no GHSA**: GitHub assigns GHSA IDs automatically and they are tightly integrated with the GitHub Advisory Database, Dependabot, and the advisory workflow. Ignoring them in favor of CVE-only would work against the tooling. Rejected.
- **GHSA only, no CVE**: CVE is the global standard for vulnerability identification. Not requesting CVE IDs would limit the reach and interoperability of CSA's advisories. Rejected.

**Rationale**: GHSA identifiers are assigned automatically, globally unique, and integrated with GitHub's ecosystem (Advisory Database, Dependabot, API). CVE IDs are the global standard recognized across all vulnerability databases and security tooling. Using both provides maximum reach — GHSA for the GitHub ecosystem, CVE for everything else. GitHub is a CNA Root and handles CVE assignment through the advisory workflow, so there is no operational overhead for CSA to request CVE IDs.

---

## 2026-02-17: No separate advisory files in the repository

**Decision**: CSA does not maintain advisory files (markdown or JSON) in this repository. Advisories are published through GitHub's native security advisory system.

**Alternatives considered**:

- **OSV-format JSON files per advisory**: Machine-readable advisory files in the Open Source Vulnerability (OSV) format, stored in an `advisories/` directory. This duplicates what GitHub's advisory system already provides through its web UI and REST API. Rejected.
- **CSAF 2.0 format files**: A more complex advisory format. Significant overhead for CSA's scale with no clear consumer. Rejected.
- **Markdown advisory files**: Human-readable versions of each advisory in the repo. GitHub's published advisories are already human-readable on the web. Rejected.

**Rationale**: GitHub's advisory system is the authoritative source. Advisories are accessible via the web UI, REST API, and the GitHub Advisory Database. Maintaining a parallel set of files in the repo creates duplication and synchronization overhead with no additional value. The API provides machine-readable access for any tooling that needs it.
