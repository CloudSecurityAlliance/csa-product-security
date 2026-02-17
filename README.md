# CSA Product Security

This repository is the authoritative home for the Cloud Security Alliance's (CSA) product security program. It documents how CSA handles security vulnerabilities in its own software and services hosted on GitHub.

## What This Covers

**CSA software on GitHub**: All software and services hosted under the [`CloudSecurityAlliance`](https://github.com/CloudSecurityAlliance) GitHub organization. Report vulnerabilities using GitHub's Private Vulnerability Reporting (PVR).

**CSA web properties**: Security issues related to CSA websites and services (cloudsecurityalliance.org, etc.) are handled through a separate process — see CSA's [security.txt](https://cloudsecurityalliance.org/.well-known/security.txt) (RFC 9116).

## Reporting a Vulnerability

Use **GitHub's Private Vulnerability Reporting (PVR)**:

1. Go to the **Security** tab of the affected repository
2. Click **"Report a vulnerability"**
3. Fill out the form

This is enabled across all public repositories in the `CloudSecurityAlliance` organization. Every repo inherits a default [SECURITY.md](https://github.com/CloudSecurityAlliance/.github/blob/main/SECURITY.md) that explains this.

## How CSA Handles Reports

1. **Receive** — PVR report comes in, visible only to CSA maintainers and the reporter
2. **Acknowledge** — CSA acknowledges receipt and begins triage
3. **Triage** — Assess severity, determine affected products/versions
4. **Assign Identifiers** — GHSA identifier is assigned automatically; CVE ID is requested where appropriate
5. **Publish** — CSA's default is to publish advisories openly and quickly. Public disclosure is the norm, not the exception. Advisories only remain private temporarily if there is a specific reason to delay. Maximum timeline from report to public disclosure is 90 days
6. **Fix** — Develop and release a fix
7. **Update** — Update the published advisory with fix details, affected versions, etc.

GitHub automatically credits the reporter on the published advisory.

## Documentation

| Document | Description |
|---|---|
| [Vulnerability Disclosure Policy](docs/vulnerability-disclosure-policy.md) | How vulnerabilities are reported and disclosed (aligned with ISO 29147) |
| [Vulnerability Handling Process](docs/vulnerability-handling-process.md) | How CSA handles vulnerabilities internally (aligned with ISO 30111) |
| [Severity Classification](docs/severity-classification.md) | How CSA classifies vulnerability severity |
| [SLA Commitments](docs/sla-commitments.md) | Response time commitments (currently being defined) |
| [GitHub Configuration](docs/github-configuration.md) | What CSA has configured in GitHub and why |
| [Decision Log](docs/decision-log.md) | Key decisions made and alternatives considered |
| [Pending Actions](docs/pending-actions.md) | Actions needed outside this repo (website updates, etc.) |

## Design Principles

- **GitHub-native**: Everything runs through GitHub's built-in security features — PVR, security advisories, Dependabot. No external tools
- **Open by default**: Advisories are published quickly and openly. CSA's software is largely open source and our security process reflects that
- **Machine-readable**: Structured data formats, consistent schemas, predictable naming conventions. This program is designed to be operated with AI assistance
- **Standards-aligned**: ISO 29147 (vulnerability disclosure), ISO 30111 (vulnerability handling), RFC 9116 (security.txt)
- **Simple**: Standard GitHub configuration, no customizations, minimal process overhead. CSA is a nonprofit with limited resources — the process must be sustainable
