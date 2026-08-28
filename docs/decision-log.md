# Decision Log

Version: 1.2 (2026-08-28)

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

**Superseded by**: [Assign CVE IDs directly as a CNA, with CVE as the identifier of record](#2026-08-27-assign-cve-ids-directly-as-a-cna-with-cve-as-the-identifier-of-record) on 2026-08-27.

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

---

## 2026-08-27: Assign CVE IDs directly as a CNA, with CVE as the identifier of record

**Decision**: CSA became an authorized CVE Numbering Authority on 2026-04-28 (CNA short name `CSAI`, CNA ID `CNA-2026-0025`, MITRE Top-Level Root, organization type Vendor). CSA assigns CVE IDs directly for software in its CNA scope. The CSA-assigned CVE ID is the identifier of record in published advisories; GHSA identifiers continue to be issued automatically for GitHub-hosted repositories and are cross-referenced rather than treated as primary. CVE-specific correspondence goes to `cve-mgmt@cloudsecurityalliance.org`.

**Registered CNA scope**: "Vulnerabilities in software developed and maintained by the Cloud Security Alliance (`github.com/CloudSecurityAlliance/*`)."

**Alternatives considered**:

- **Continue requesting CVE IDs through GitHub as a CNA Root**: Workable, but it makes CSA dependent on another organization for identifiers it is now authorized to assign itself, and it adds latency and a coordination step to every publication. Not selected.
- **Keep GHSA as the primary identifier with CSA-assigned CVE as secondary**: Preserves the existing tooling story (Dependabot, the GitHub Advisory Database) with a smaller documentation change. Not selected — GHSA is a platform-specific identifier, and CSA's CNA scope includes software whose advisories may be published outside GitHub. Leading with the identifier CSA itself controls is more durable.
- **Drop GHSA emphasis entirely and publish only CVE**: Would forfeit automatic Dependabot notification and GitHub Advisory Database inclusion for CSA's own repositories at no benefit, since GHSA identifiers are issued automatically whether or not CSA references them. Not selected.

**Rationale**: CSA is now the authority for identifiers covering its own software, and the documentation should say so plainly. A reporter reading the previous policy would reasonably have concluded CSA depended on GitHub as its CNA. Assigning directly removes that dependency, shortens the path to publication, and aligns the disclosure policy with the record registered at cve.org — which links to `docs/vulnerability-disclosure-policy.md` as CSA's public CNA policy. Note that the CNA scope is narrower than this program's overall reporting scope: websites, operated services, and repositories in other CSA GitHub organizations are handled under this program but do not receive CSA-assigned CVE IDs.

---

## 2026-08-27: Do not assign CVE IDs for pre-1.0 software

**Superseded by**: [Define CVE eligibility as a declared version of 1.0.0 or higher](#2026-08-28-define-cve-eligibility-as-a-declared-version-of-100-or-higher) on 2026-08-28. The exclusion itself stands; the superseding entry pins down what "reaches 1.0" means.

**Decision**: CSA does not assign CVE IDs for vulnerabilities in releases prior to a project's 1.0 (or equivalent general availability) release. Such reports are still triaged, remediated, and — where the repository supports it — documented in a GitHub advisory. Once a project reaches 1.0, subsequent vulnerabilities are eligible for CVE assignment.

**Alternatives considered**:

- **Assign regardless of version number**: CNA Rules 4.2.10 only directs CNAs not to assign for products that are "not and were never publicly available", and a public pre-1.0 repository is publicly available, so this would be permissible. Not selected; see rationale.
- **Case-by-case based on observed real-world use**: Assign for pre-1.0 software that is packaged, distributed, or known to be running in production. More faithful to actual risk, but it turns every pre-1.0 report into a judgment call, is difficult to state crisply in a public policy, and produces inconsistent outcomes across similar projects. Not selected.
- **Exclude only explicitly labelled alpha/beta/preview releases**: A narrower exclusion, but it depends on labelling discipline CSA does not enforce uniformly across repositories. Not selected.

**Rationale**: A CVE record carries an implicit representation that the affected software was offered as production-ready. CSA publishes pre-1.0 code for evaluation and community feedback and does not represent it as such, so assigning CVE IDs against it would misstate the maturity of the artifact and generate downstream noise in scanners and dependency tooling for software nobody was advised to deploy. Drawing the line at 1.0 is a bright-line rule that reporters and maintainers can both apply without negotiation. This is a discretionary CSA assignment policy, published as CNA Rules 3.2.6.1 requires, and not a rule imposed by the CVE Program.

---

## 2026-08-28: Define CVE eligibility as a declared version of 1.0.0 or higher

**Decision**: CVE eligibility turns on whether the software has declared a version of `1.0.0` or higher. The declaration counts if it appears as a release tag, a GitHub Release, or a published package version — any one is sufficient, and no formal release process is required. Software carrying no version at all has not declared readiness and is not eligible.

**Context**: The 2026-08-27 exclusion said "before a project's 1.0 (or equivalent general availability) release" without defining what established 1.0. Checking the CNA-scope organization against that wording showed the gap was not theoretical: of 26 public non-archived repositories, three sat at `v1.0.0` by git tag with no GitHub Release and no published package, two had releases below 1.0, and 21 had no release or tag at all. Applying the rule literally, no repository was unambiguously eligible.

**Alternatives considered**:

- **Require a GitHub Release or published package for 1.0.0 to count**: A stricter, more auditable signal. Not selected — it would contradict CSA's own release standard, which already treats the tag as the provenance anchor ("publish only from CI, off a tag"). A tag authoritative enough to build a release from is authoritative enough to mark readiness.
- **Treat software with no version as eligible**: Unversioned software is the least likely to be production-ready, so treating absence of a version as eligibility would invert the intent of the exclusion. Not selected.
- **Replace the version test with a general-availability judgment per report**: Avoids depending on version hygiene, but reintroduces the per-report judgment call the bright-line rule was chosen to remove. Not selected.

**Rationale**: A version of `1.0.0` is a statement by the project that the software is ready for consumption, and that statement is what the exclusion is really testing. Reading the declaration from a tag, a release, or a package version keeps the test applicable to repositories at different points of release maturity without requiring every project to adopt a publishing pipeline first. Deriving eligibility from the version label also keeps this policy independent of any future organization-wide versioning standard: if such a standard lands, this rule reads whatever it produces without amendment.

<!-- markdownlint-enable MD013 -->
