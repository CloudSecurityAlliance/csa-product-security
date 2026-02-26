# Severity Classification

Version: 1.0 (2026-02-25)

CSA uses GitHub's security advisory ratings (Critical, High, Medium, Low) and
supplements them with structured scoring input:

- **[CVSS](https://www.first.org/cvss/) v3.1 Base Score** for software and operated services.
- **[OWASP AIVSS](https://aivss.owasp.org)** for AI prompts, skills, and other
  AI-facing instructions.

These inputs provide consistent, machine-readable severity data across all asset
categories.

## Severity ratings

- **Critical** — Typically CVSS ≥ 9.0 or AIVSS Level 4/5. Exploitation is
  straightforward and impact is severe.
- **High** — Usually CVSS 7.0–8.9 or AIVSS Level 3. Exploitation is practical
  and impact is significant.
- **Medium** — CVSS 4.0–6.9 or AIVSS Level 2. Exploitation requires specific
  conditions or the impact is limited.
- **Low** — CVSS < 4.0 or AIVSS Level 1. Exploitation is difficult or impact is
  minimal.

## How severity is used

Severity classification informs:

- **Priority of response** — Higher severity vulnerabilities are addressed first.
- **Disclosure urgency** — Critical and high issues receive accelerated
  publication and remediation.
- **SLA focus** — Elevated severities may require tighter targets than the
  baseline [SLA commitments](sla-commitments.md).
- **Advisory content** — Every published advisory includes the severity rating
  and the supporting CVSS or AIVSS details.

## Context matters

Severity ratings provide a baseline, but CSA also considers deployment context,
customer impact, and exploitability signals when prioritizing response.

## Related resources

- [Governance Framework](governance-framework.md)
- [Vulnerability Handling Process](vulnerability-handling-process.md)
- [SLA Commitments](sla-commitments.md)
