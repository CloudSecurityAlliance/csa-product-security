# Cloud Security Alliance vulnerability governance framework

Version: 1.0 (2026-02-25)

## Purpose and openness

The Cloud Security Alliance (CSA) operates a unified product security incident
response team (PSIRT) for its websites, services, software, and AI-facing
prompts, skills, and system instructions. This framework documents how CSA
manages intake, analysis, remediation, and disclosure so reporters, partners,
and internal teams share the same playbook. CSA publishes its governance
materials publicly to invite feedback and demonstrate accountable practices
while still handling embargoed or sensitive reports confidentially. More than
sixty CSA members already function as CVE Numbering Authorities; their
experience informs this framework, and community members may suggest
improvements.

## Scope and asset categories

CSA handles three categories. Each determines the reporting channel, handling
steps, and disclosure path.

- **Websites and services** — `cloudsecurityalliance.org`, `csachapter.io`,
  `star.watch`, `webfinger.io`, hosted portals, and first-party APIs. Report via
  [security@cloudsecurityalliance.org](mailto:security@cloudsecurityalliance.org).
- **Software** — Repositories under `github.com/CloudSecurityAlliance/*`, MCP
  servers and clients, SDKs, and extensions. Report through GitHub Private
  Vulnerability Reporting (PVR) from the repository’s Security tab.
- **AI prompts and instructions** — Published prompts, guardrails, skills, and
  system instructions, including those embedded in MCP servers and clients. Use
  GitHub PVR if the artifact lives in a repository; otherwise report via email.

Reporters only need to answer “Where did I find the issue?” Internal workflows
handle classification and disclosure details.

## Reporting channels and safe harbor

- **Email** — [security@cloudsecurityalliance.org](mailto:security@cloudsecurityalliance.org)
  (PGP available) handles websites, services, and AI artifacts published
  outside GitHub. Anonymous or pseudonymous submissions are welcome.
- **GitHub PVR** — Handles code within the CloudSecurityAlliance organization
  and AI artifacts stored in repositories. GitHub requires reporters to be
  logged in; the linked GitHub account is visible to CSA. Researchers who
  prefer not to share their GitHub identity should use email instead.

CSA does not run a bug bounty program.

## Credit for reporting

- GitHub PVR submissions always include the reporter’s GitHub account. When the
  advisory is published, GitHub credits that account automatically.
- Email submissions for software advisories can include credit when both parties
  agree, using the reporter’s GitHub handle if provided. Website and service
  issues generally do not include public acknowledgments.

Safe harbor applies to good-faith reporters who demonstrate impact without
unnecessary exploitation and respect confidentiality requirements. Public
materials stay open for review, but supporting evidence, exploit details, and
embargoed advisories can remain confidential until publication if needed.

## Qualification criteria and record discipline

CSA treats a report as a security vulnerability when it is:

1. Attributable to a CSA-controlled asset within scope.
2. Reproducible with the information provided, or clearly explained so analysts
   can validate it.
3. A demonstrable (or clearly explained) violation of confidentiality,
   integrity, availability, or authorization boundaries.

Issues outside these criteria may route to policy or research channels. CSA
maintains CVE-compatible records: one independently fixable issue per record,
explicit split/merge rationale, structured data aligned with CVE JSON fields,
and auditable lifecycle states.

## Lifecycle overview

1. **Intake** — Receive the report, acknowledge receipt, capture reporter
   preferences, and assign a temporary tracking ID.
2. **Security qualification** — Validate the issue, redact accidental secrets,
   and quarantine abuse.
3. **Scope and routing** — Map to the published category, confirm the reporting
   channel, identify related records or duplicates, and help redirect out-of-
   scope issues to the responsible party.
4. **Confirmation** — Reproduce or explain the issue, document evidence, note
   affected versions or deployments, and assess impact.
5. **Remediation planning** — Engage engineering or service owners, define
   fixes, and track progress alongside interim mitigations.
6. **Disclosure decision** — Choose advisory format, coordinate timelines with
   reporters and partners, and set embargo terms when required.
7. **Publication** — Release advisories or updates through GitHub, the website,
   or coordinated partner notices, and provide credit only when the platform
   supports it and both parties agree.
8. **Closure** — Verify fixes in production, update timelines and references,
   and archive correspondence. Rejections, duplicates, or disputes capture
   rationale and reference the original report.

Embargo-sensitive information is handled through restricted systems during each
stage. Public transparency resumes once publication criteria are met.

## Service level commitments

CSA follows clear response targets:

- **Acknowledgment:** within five business days of receiving a report, via the
  same channel used for submission.
- **Status updates:** at least every 30 days while the issue is under
  investigation or remediation.
- **Remediation or disclosure target:** resolve or coordinate publication within
  90 days of acknowledgment unless CSA and the reporter mutually agree to a
  different timeline (documented in the case record).

Critical issues may move faster. Extensions beyond 90 days require explicit
agreement so every party knows the plan.

## AI-specific guidance

CSA accepts reports for AI artifacts it publishes when the issue:

- Bypasses an intended security control (for example, prompt injection that
  defeats guardrails).
- Enables unauthorized tool execution or access to restricted connectors.
- Circumvents authentication or authorization decisions encoded in the
  artifact.
- Exfiltrates data or system state governed by the artifact.

General model behavior observations without a CSA-attributable artifact are
outside this framework. Action-bound AI artifacts (those that invoke tools or
change system state) follow procedures similar to software, whereas purely
behavioral instructions may route through research or policy workflows if no
security boundary is involved.

## Records and transparency

Each validated vulnerability record includes at least: internal identifier,
asset category, affected assets or versions, severity, reproduction evidence,
disclosure status, and references. Records live in version-controlled systems
with audit trails. Publishing this framework—and related documents such as the
severity criteria and SLA commitments—helps reporters understand expectations
and gives other organizations a CVE-compatible reference they can adapt.

## Maturity roadmap

CSA tracks its progress through six phases. Each phase adds capabilities without
replacing the governance foundation.

1. **Foundation** — Governance published, scope aligned, intake channels
   operating.
2. **Structured operations** — Structured records, defined SLAs, and cross-asset
   coverage.
3. **Quality and consistency** — Accurate scope resolution, duplicate detection,
   and completeness checks reduce analyst rework.
4. **CVE-ready records** — CVE-format records, traceable decisions, and internal
   IDs mapped to public references enable quick CVE requests or assignments.
5. **Publication readiness** — Advisory workflows, rapid publication capability,
   and coordination playbooks deliver timely, consistent disclosures.
6. **CVE assignment operations** — Reliable acquisition of CVE identifiers
   (direct or coordinated) plus scope deconfliction for CSA assets and
   third-party software.

## Reporter and ecosystem support

Raising the entire vulnerability community is central to CSA’s mission. CSA
publishes guidance, templates, and tooling—such as scope decision helpers,
reporting checklists, and completeness tools—so reporters, vendors, and service
operators can produce high-quality submissions. Every inbound report is
processed through CSA’s own systems, but helper tools remain available to
anyone. Feedback on this framework or its supporting assets is welcome via
GitHub issues or
[security@cloudsecurityalliance.org](mailto:security@cloudsecurityalliance.org).
