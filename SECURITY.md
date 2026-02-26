# Security Policy

The Cloud Security Alliance (CSA) documents its full product security program in the [`csa-product-security`](https://github.com/CloudSecurityAlliance/csa-product-security) repository. The guidance below summarizes how to report potential vulnerabilities.

## Scope

- **Websites and services** such as `cloudsecurityalliance.org`, `csachapter.io`, `star.watch`, `webfinger.io`, hosted portals, and first-party APIs.
- **Software** in the `CloudSecurityAlliance` GitHub organization, including MCP servers/clients, SDKs, and extensions.
- **AI prompts and instructions** published by CSA, whether embedded in MCP artifacts or distributed separately.

General model-behavior research without a CSA artifact, third-party platforms, or upstream dependencies we do not control are out of scope. See the [Vulnerability Disclosure Policy](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/vulnerability-disclosure-policy.md#out-of-scope) for details.

## How to report

- **GitHub Private Vulnerability Reporting (preferred for software or repo-hosted AI artifacts):** Open the repository’s **Security** tab, select **Report a vulnerability**, and provide reproduction steps, impact, and affected versions. Reports stay private until we publish an advisory, and GitHub credits the reporter automatically. GitHub login required.
- **Email `security@cloudsecurityalliance.org`** (for websites/services, AI content published outside GitHub, or if you prefer not to use PVR). Include reproduction steps, impact, affected assets, and credit preference. Anonymous or pseudonymous reports and PGP-encrypted messages are accepted.

## Service levels and disclosure

CSA follows coordinated disclosure with explicit timelines:

- Acknowledge every report within **5 business days**.
- Provide substantive status updates at least every **30 days** while a case is open.
- Target remediation or public disclosure within **90 days** of acknowledgment unless we mutually agree on a different schedule.

We default to publishing advisories openly through GitHub as soon as practical, even if a fix is still in progress. See the [SLA commitments](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/sla-commitments.md) and [governance framework](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/governance-framework.md) for the canonical definitions.

## Safe harbor

CSA supports good-faith security research. If you respect this policy, avoid unnecessary service disruption, and give us a reasonable chance to remediate before disclosure, we will not pursue legal action. Keep exploitation to the minimum required to demonstrate impact and do not access, modify, or exfiltrate data beyond what is necessary to prove the issue.

## Need more detail?

The complete governance model, handling process, and severity expectations live in `csa-product-security/docs/`. Start with:

- [Vulnerability Disclosure Policy](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/vulnerability-disclosure-policy.md)
- [Vulnerability Handling Process](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/vulnerability-handling-process.md)
- [Severity Classification](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/severity-classification.md)

Copy this SECURITY.md into the `.github` repository to apply it organization-wide; individual repos can override it if they have unique requirements.
