# Security Policy

The Cloud Security Alliance (CSA) documents its full product security program in the [`csa-product-security`](https://github.com/CloudSecurityAlliance/csa-product-security) repository. The guidance below summarizes how to report potential vulnerabilities.

## Scope

- **Websites and services** such as `cloudsecurityalliance.org`, `csachapter.io`, `star.watch`, `webfinger.io`, hosted portals, and first-party APIs.
- **Software** in CSA-managed GitHub organizations, including MCP servers/clients, SDKs, and extensions:
  - `CloudSecurityAlliance`
  - `CloudSecurityAlliance-Chatbots`
  - `CloudSecurityAlliance-DataSets`
  - `modelcontextprotocol-security`
  - `RiskRubric`
- **AI prompts and instructions** published by CSA, whether embedded in MCP artifacts or distributed separately.

General model-behavior research without a CSA artifact, third-party platforms, or upstream dependencies we do not control are out of scope. See the [Vulnerability Disclosure Policy](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/vulnerability-disclosure-policy.md#out-of-scope) for details.

## How to report

- **GitHub Private Vulnerability Reporting (preferred for software or repo-hosted AI artifacts):** Open the repository’s **Security** tab, select **Report a vulnerability**, and provide reproduction steps, impact, and affected versions. Reports stay private until we publish an advisory, and GitHub credits the reporter automatically. GitHub login required.
- **Email `security@cloudsecurityalliance.org`** (for websites/services, AI content published outside GitHub, or if you prefer not to use PVR). Include reproduction steps, impact, affected assets, and credit preference. Anonymous or pseudonymous reports and PGP-encrypted messages are accepted.

## CVE identifiers

CSA is an authorized [CVE Numbering Authority](https://www.cve.org/PartnerInformation/ListofPartners/partner/CSAI) (CNA short name `CSAI`, CNA ID `CNA-2026-0025`) and assigns CVE IDs for its own software directly. The registered CNA scope is *"vulnerabilities in software developed and maintained by the Cloud Security Alliance (`github.com/CloudSecurityAlliance/*`)"*, which is narrower than the reporting scope above — reports for other CSA repositories, websites, and services are still accepted and remediated, but do not receive a CSA-assigned CVE ID. CSA also does not assign CVE IDs for pre-1.0 releases; those issues are still fixed and may receive a GitHub advisory. See the [disclosure policy](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/vulnerability-disclosure-policy.md#cve-identifiers-and-csas-role-as-a-cna) for the full assignment policy, and email [cve-mgmt@cloudsecurityalliance.org](mailto:cve-mgmt@cloudsecurityalliance.org) for CVE-specific questions such as scope deconfliction or record corrections.

## Service levels and disclosure

CSA follows coordinated disclosure with explicit timelines:

- Acknowledge every report within **5 business days**.
- Provide substantive status updates at least every **30 days** while a case is open.
- Target remediation or public disclosure within **90 days** of acknowledgment unless we mutually agree on a different schedule.

We default to publishing advisories openly as soon as practical, even if a fix is still in progress. Where CSA assigns a CVE ID, the CVE Record is published to the CVE List within 72 hours of public disclosure. Published advisories are listed at [labs.cloudsecurityalliance.org/advisories](https://labs.cloudsecurityalliance.org/advisories/). See the [SLA commitments](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/sla-commitments.md) and [governance framework](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/governance-framework.md) for the canonical definitions.

## Safe harbor

CSA supports good-faith security research. If you respect this policy, avoid unnecessary service disruption, and give us a reasonable chance to remediate before disclosure, we will not pursue legal action. Keep exploitation to the minimum required to demonstrate impact and do not access, modify, or exfiltrate data beyond what is necessary to prove the issue.

## Need more detail?

The complete governance model, handling process, and severity expectations live in `csa-product-security/docs/`. Start with:

- [Vulnerability Disclosure Policy](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/vulnerability-disclosure-policy.md)
- [Vulnerability Handling Process](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/vulnerability-handling-process.md)
- [Severity Classification](https://github.com/CloudSecurityAlliance/csa-product-security/blob/main/docs/severity-classification.md)

Copy this SECURITY.md into the `.github` repository to apply it organization-wide; individual repos can override it if they have unique requirements.
