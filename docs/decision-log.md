# Decision Log

Version: 1.0 (2026-02-25)

<!-- markdownlint-disable MD013 -->

Key decisions made in establishing CSA's product security program, including alternatives considered and rationale.

## 2026-02-17: Use GitHub Private Vulnerability Reporting as the primary software reporting channel

**Decision**: Vulnerability reports for CSA software on GitHub are submitted through GitHub's Private Vulnerability Reporting (PVR). Other GitHub-based mechanisms (issues, discussions) are not used for security vulnerabilities.

**Alternatives considered**:

- **GitHub Issues**: Public by default, creating a risk of accidental disclosure. Not selected.
- **GitHub Discussions**: Also public by default and lacks structured triage or advisory workflows. Not selected.
- **GitHub Issues with a vulnerability template**: Provides structure but remains public. PVR offers equivalent input fields with privacy by default. Not selected.
- **PVR with Issues as a secondary channel**: Adds operational complexity without a clear benefit since PVR covers the full workflow. Not selected.

**Rationale**: PVR is purpose-built for vulnerability coordination. It is private by default, provides a structured submission form, automatically credits reporters, integrates with GitHub's advisory publication system, and supports the full lifecycle from report through publication. No external tooling is required.

---

## 2026-02-17: Publish advisories openly and promptly by default

**Decision**: CSA publishes security advisories as soon as practical, even before a fix is available. Embargoed or private advisories are reserved for exceptional circumstances.

**Alternatives considered**:

- **Standard coordinated disclosure (private until fix)**: Appropriate for commercial software, but CSA's repositories are predominantly open source. Keeping an advisory private while the vulnerable code is publicly visible offers limited additional protection. Retained as an option for exceptional cases but not selected as the default.
- **Fixed 90-day embargo**: A rigid private window before any disclosure. Not aligned with CSA's transparency commitments. Not selected.

**Rationale**: CSA's open source posture favors early transparency. GitHub's advisory system supports publishing and updating advisories incrementally — the URL remains stable and the edit history stays private. The 90-day timeline serves as a maximum coordination window rather than a publication target.

---

## 2026-02-17: Apply GitHub-recommended security configuration org-wide

**Decision**: Apply GitHub's recommended security configuration across the entire `CloudSecurityAlliance` organization with enforcement enabled and no customizations.

**Alternatives considered**:

- **Custom security configuration**: GitHub supports bespoke feature toggles, but the recommended configuration already enables all relevant free features. No customization was needed. Not selected.
- **Per-repository configuration**: Configuring features individually does not scale across CSA's growing number of repositories. Not selected.

**Rationale**: The recommended configuration enables PVR, Dependabot, code scanning, secret scanning, and push protection for all public repositories at no cost. Applying it uniformly with enforcement reduces the risk of misconfiguration and simplifies ongoing maintenance.

---

## 2026-02-17: No bug bounty program

**Decision**: CSA does not offer monetary rewards for vulnerability reports.

**Alternatives considered**:

- **Paid bug bounty program**: As a nonprofit, CSA does not have the budget to sustain monetary rewards. Not selected.
- **Swag or merchandise rewards**: Introduces procurement and logistics overhead with limited incentive value. Not selected.

**Rationale**: CSA is a nonprofit organization. GitHub's automatic credit on published advisories provides meaningful public recognition. Researchers who report vulnerabilities to CSA contribute to the security of a public-good organization, and CSA values those contributions.

---

## 2026-02-17: No separate acknowledgements page

**Decision**: CSA does not maintain a standalone acknowledgements or "hall of fame" page. Reporter credit is handled through GitHub's native advisory credit mechanism.

**Alternatives considered**:

- **ACKNOWLEDGEMENTS.md in the repository**: A manually maintained list that duplicates information already captured by GitHub's advisory system. Not selected.
- **Dedicated webpage**: Introduces the same duplication and requires web team involvement for updates. Not selected.

**Rationale**: GitHub automatically credits the reporter when a PVR-originated advisory is published. This credit is public, permanent, and requires no additional maintenance.

---

## 2026-02-17: Defer SLA commitments until operational experience is established

**Decision**: CSA did not commit to specific response-time SLAs at program launch.

**Superseded by**: [Establish service level commitments (5/30/90)](#2026-02-25-establish-service-level-commitments-53090) on 2026-02-25.

**Alternatives considered**:

- **Define SLAs immediately**: Risked committing to targets CSA could not reliably meet without operational experience. Not selected at the time.

**Rationale**: Establishing the program first and defining commitments based on demonstrated capacity was the more responsible approach.

---

## 2026-02-17: Separate programs for GitHub software and web properties

**Decision**: CSA's product security program (this repository) initially covered only software on GitHub. Web properties were covered by a separate process documented at [security.txt](https://cloudsecurityalliance.org/.well-known/security.txt) and [cloudsecurityalliance.org/security](https://cloudsecurityalliance.org/security).

**Superseded by**: [Expand PSIRT scope to include websites/services and AI instructions](#2026-02-25-expand-psirt-scope-to-include-websitesservices-and-ai-instructions) on 2026-02-25.

**Alternatives considered**:

- **Single unified program**: Web properties are managed by different teams with different tooling. Combining both into one process at launch would have added unnecessary complexity. Not selected at the time.

**Rationale**: The two programs had different tooling, teams, and workflows. Keeping them separate at launch allowed each to operate effectively while cross-references ensured reporters could find the appropriate channel.

---

## 2026-02-17: Reference security.txt as the canonical security contact entry point

**Decision**: References to CSA's security contact information use the [security.txt](https://cloudsecurityalliance.org/.well-known/security.txt) file as the primary link rather than linking directly to the website security page.

**Alternatives considered**:

- **Link directly to cloudsecurityalliance.org/security**: The security.txt file already references this page via its `Policy:` field. Using security.txt as the primary link is more standards-compliant. Not selected as the primary reference.

**Rationale**: security.txt (RFC 9116) is the standard machine-readable mechanism for security contact discovery. Consistently referencing it reinforces standards compliance and provides a stable entry point for both automated tools and human researchers.

---

## 2026-02-17: Use GHSA as primary identifier and request CVE IDs through GitHub

**Decision**: CSA uses GitHub's native GHSA identifiers as the primary advisory identifier and requests CVE IDs through GitHub's advisory workflow where appropriate. Both identifiers appear in published advisories.

**Alternatives considered**:

- **CSA-specific identifiers (e.g., CSA-2026-001)**: Would require manual assignment, sequential tracking, and a mapping layer between CSA IDs, GHSA IDs, and CVE IDs. Not selected.
- **CVE IDs as primary, without GHSA**: GHSA identifiers are tightly integrated with the GitHub Advisory Database, Dependabot, and the advisory workflow. Disregarding them would work against the tooling. Not selected.
- **GHSA only, without CVE**: CVE is the global standard for vulnerability identification. Omitting CVE IDs would limit the reach and interoperability of CSA's advisories. Not selected.

**Rationale**: GHSA identifiers are assigned automatically, are globally unique, and integrate with GitHub's ecosystem. CVE IDs are recognized across all major vulnerability databases and security tooling. Using both provides maximum reach. GitHub serves as a CNA Root and handles CVE assignment through its advisory workflow, so there is no additional operational overhead for CSA.

---

## 2026-02-17: No separate advisory files in the repository

**Decision**: CSA does not maintain advisory files (markdown, JSON, or other formats) in this repository. Advisories are published through GitHub's native security advisory system.

**Alternatives considered**:

- **OSV-format JSON files**: Machine-readable advisory files stored in an `advisories/` directory. Duplicates what GitHub's advisory system already provides through its web UI and REST API. Not selected.
- **CSAF 2.0 format files**: A comprehensive advisory format with significant overhead relative to CSA's current scale. Not selected.
- **Markdown advisory files**: Human-readable versions of each advisory. GitHub's published advisories are already accessible on the web. Not selected.

**Rationale**: GitHub's advisory system is the authoritative source. Advisories are accessible via the web UI, REST API, and the GitHub Advisory Database. Maintaining a parallel set of files would create synchronization overhead without additional value.

---

## 2026-02-25: Publish a unified governance framework for all CSA assets

**Decision**: Release a public governance framework describing scope, lifecycle, transparency posture, maturity roadmap, and tooling commitments across websites/services, software, and AI instructions.

**Alternatives considered**:

- **Maintain GitHub-only scope**: Continue the "software only" framing while referencing web properties separately. Not selected because reporters and internal teams need a single reference for all CSA assets.
- **Internal-only governance**: Keep the framework private. Not selected; transparency and community feedback are core CSA values, and public documentation builds trust with reporters and partners.

**Rationale**: CSA receives reports across multiple asset types and benefits from a shared playbook. Publishing the governance framework aligns with CSA's transparency goals, keeps the public security page authoritative, and demonstrates disciplined vulnerability management practices.

---

## 2026-02-25: Expand PSIRT scope to include websites/services and AI instructions

**Decision**: Treat CSA websites, operated services, and AI prompts/instructions as first-class assets within this repository, each with a defined reporting channel (email or GitHub PVR).

**Alternatives considered**:

- **Continue separate programs**: Maintain web properties and AI instructions outside the repository per the original 2026-02-17 decision. Not selected because the unified governance framework requires a consolidated intake view.
- **Route all assets through GitHub**: Require GitHub PVR for everything. Not selected because some assets (websites, CMS-managed instructions) are not represented in GitHub repositories.

**Rationale**: The public security page now presents three categories, and the internal program mirrors that structure. Email remains the appropriate channel for websites and non-repository artifacts, while GitHub PVR stays the authoritative system for code and repository-hosted AI artifacts.

---

## 2026-02-25: Establish service level commitments (5/30/90)

**Decision**: Commit to acknowledging reports within 5 business days, providing status updates at least every 30 days, and targeting remediation or publication within 90 days unless both parties agree to a different timeline.

**Alternatives considered**:

- **Continue without SLAs**: Defer commitments until later maturity. Not selected because reporters and partners expect explicit timelines now that governance is published.
- **Adopt stricter timelines immediately**: Commit to faster response targets such as 24-hour acknowledgments. Not selected; CSA's current operational capacity does not yet support shorter commitments reliably.

**Rationale**: The 5/30/90 targets balance operational realism with industry expectations. Publishing them sets clear expectations for reporters and partners without overcommitting.

---

## 2026-02-25: Use CVSS and AIVSS as supporting severity signals

**Decision**: Supplement GitHub's Critical/High/Medium/Low ratings with CVSS v3.1 for software and services and OWASP AIVSS for AI prompts and instructions.

**Alternatives considered**:

- **GitHub ratings only**: Qualitative labels alone lack the machine-readable data useful for tooling and interoperability. Not selected.
- **Custom CSA severity model**: A proprietary scoring system would be harder to explain to reporters and less interoperable with existing tooling. Not selected.

**Rationale**: CVSS is widely adopted for software and services. AIVSS is designed for AI artifacts. Using both provides consistent, machine-readable severity data aligned with the governance framework across all asset categories.

<!-- markdownlint-enable MD013 -->
