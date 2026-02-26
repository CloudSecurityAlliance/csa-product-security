# CSA Product Security

This repository is the authoritative home for the Cloud Security Alliance's (CSA)
product security program. It documents scope, reporting channels, governance, and
service levels for CSA websites, services, software, and AI prompts and
instructions.

## Program scope

- **Websites and services** — `cloudsecurityalliance.org`, `csachapter.io`,
  `star.watch`, `webfinger.io`, hosted portals, and first-party APIs. Report via
  `security@cloudsecurityalliance.org`.
- **Software** — Repositories under
  [`CloudSecurityAlliance`](https://github.com/CloudSecurityAlliance), MCP servers
  and clients, SDKs, and extensions. Report through GitHub's Private Vulnerability
  Reporting (PVR).
- **AI prompts and instructions** — CSA-published prompts, guardrails, skills, and
  system instructions, including those embedded in MCP servers and clients. Report
  through GitHub PVR if stored in a repository or via
  `security@cloudsecurityalliance.org` if published elsewhere.

The [governance framework](docs/governance-framework.md) explains how these
categories map to intake, handling, disclosure, and maturity goals.

## Reporting a vulnerability

Choose the channel based on where you found the issue:

- **GitHub PVR** (preferred for software and repo-hosted AI artifacts): open the
  repository’s **Security** tab, select **Report a vulnerability**, and provide
  details. GitHub requires a logged-in account and credits the reporter
  automatically on published advisories.
- **Email `security@cloudsecurityalliance.org`** (for websites, services, or
  non-repo AI artifacts): include reproduction details, impact, and any preferred
  credit instructions. This channel supports anonymous or pseudonymous
  submissions and PGP on request.

CSA does not run a bug bounty. Safe harbor applies to good-faith reporters who
follow the [disclosure policy](docs/vulnerability-disclosure-policy.md).

## How CSA handles reports

1. **Intake** — Receive the report, acknowledge, and log the case.
2. **Security qualification** — Validate the issue, remove accidental secrets, and
   quarantine abuse.
3. **Scope and routing** — Map to the correct asset category, ensure the proper
   channel, and redirect out-of-scope items.
4. **Confirmation** — Reproduce or clearly explain the issue, capture evidence,
   and gauge impact.
5. **Remediation planning** — Engage owners, track fixes, and define mitigations.
6. **Disclosure decision** — Coordinate timelines, embargoes, and advisory
   format.
7. **Publication** — Publish through GitHub advisories, website updates, or
   partner notices; credit when the platform supports it and both parties agree.
8. **Closure** — Verify fixes, update timelines, and archive correspondence.

CSA targets **acknowledgment within 5 business days**, **status updates every 30
days**, and **remediation or disclosure within 90 days** unless a different
timeline is mutually agreed. See [SLA commitments](docs/sla-commitments.md) for
details.

## Key documents

- [Governance Framework](docs/governance-framework.md) — Unified scope,
  lifecycle, maturity roadmap, and transparency commitments.
- [Vulnerability Disclosure Policy](docs/vulnerability-disclosure-policy.md) —
  Reporter-facing guidance on scope, channels, and safe harbor.
- [Vulnerability Handling Process](docs/vulnerability-handling-process.md) —
  Internal lifecycle execution and role definitions.
- [Severity Classification](docs/severity-classification.md) — Severity model
  ([CVSS](https://www.first.org/cvss/)/[AIVSS](https://aivss.owasp.org) inputs) across asset categories.
- [SLA Commitments](docs/sla-commitments.md) — Authoritative response-time
  targets.
- [Decision Log](docs/decision-log.md) — Key governance decisions and
  alternatives considered.
- [Pending Actions](docs/pending-actions.md) — Follow-up work tracked outside
  this document.
- [AGENTS Guide](AGENTS.md) — Contributor instructions for human and AI
  assistants.

## Design principles

- **Transparency with safeguards** — Publish governance, policies, and roadmaps
  while keeping embargoed data confidential until release.
- **Reporter-aligned scope** — Asset categories mirror the public security page
  so routing stays simple.
- **Standards-aligned** — RFC 9116, CVE-compatible practices, CVSS + AIVSS
  context.
- **Single source of truth** — GitHub remains the authoritative system for
  software advisories; email handles other assets without duplicating state.
- **Practical maturity** — Roadmap focuses on capabilities CSA can operate today
  while paving the way for consistent CVE assignment.
