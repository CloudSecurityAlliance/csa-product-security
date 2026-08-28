# Pending Actions

Version: 1.1 (2026-08-27)

Actions that need to be completed outside this repository to fully integrate the
product security program.

## Update cloudsecurityalliance.org/security page

**Status**: Completed (2026-02-25)

The page now presents the three asset categories (Websites and Services,
Software, AI Prompts and Instructions), updated out-of-scope text, and routing
guidance consistent with this repository. Future edits should keep the page and
the governance framework in sync.

## Reflect CSA's CNA status in the disclosure documentation

**Status**: Completed (2026-08-27)

CSA was authorized as a CNA on 2026-04-28 (short name `CSAI`, CNA ID
`CNA-2026-0025`, MITRE Top-Level Root). The documentation now states this
directly: `docs/vulnerability-disclosure-policy.md` carries the assignment
policy CNA Rules 3.2.6.1 requires CSA to publish, and the CVE-via-GitHub
framing has been removed from the disclosure policy, README, and `SECURITY.md`.
CVE is now the identifier of record with GHSA cross-referenced, pre-1.0
releases are an explicit assignment exclusion, and the 72-hour CVE Record
publication requirement is recorded in `docs/sla-commitments.md`. Both
decisions are logged in `docs/decision-log.md`.

Note for future edits: cve.org links to
`docs/vulnerability-disclosure-policy.md` as CSA's public CNA policy, so that
file is externally referenced and should not be renamed or moved without
updating the CNA record.

## Update security.txt

**Status**: Pending

The [security.txt](https://cloudsecurityalliance.org/.well-known/security.txt)
entry should link directly to this repository (governance framework and
disclosure policy) so automated clients can discover the program details. This
file is maintained in CSA’s CMS.

## Announce governance framework

**Status**: Pending

CSA communications should publish a short update (blog, newsletter, or member
mailing) summarizing the new governance framework and AI scope additions. This
helps reporters and partners discover the changes outside of GitHub.

## Link governance framework from security page

**Status**: Pending

Add a prominent link on
[cloudsecurityalliance.org/security](https://cloudsecurityalliance.org/security)
to `docs/governance-framework.md` (or a rendered copy) so reporters can access
the full lifecycle without browsing the repository.
