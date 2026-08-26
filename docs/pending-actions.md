# Pending Actions

Version: 1.0 (2026-02-25)

Actions that need to be completed outside this repository to fully integrate the
product security program.

## Update cloudsecurityalliance.org/security page

**Status**: Completed (2026-02-25)

The page now presents the three asset categories (Websites and Services,
Software, AI Prompts and Instructions), updated out-of-scope text, and routing
guidance consistent with this repository. Future edits should keep the page and
the governance framework in sync.

## Reflect CSA's CNA status in the disclosure documentation

**Status**: Pending

CSA operates as a CVE Numbering Authority, but nothing in this repository says
so. `docs/vulnerability-disclosure-policy.md` states that an advisory may
"include a CVE ID requested via GitHub", and `README.md` mentions CNA only as a
research program informing this practice. A reporter reading the current policy
would reasonably conclude CSA depends on GitHub as its CNA.

Decide whether CSA assigns CVE IDs for its own products directly, and if so
update the disclosure policy, `docs/vulnerability-handling-process.md`, and the
root `SECURITY.md` so the identifier path matches what actually happens. The
governance framework and SLA commitments should be checked for the same
assumption.

This surfaced while auditing `CloudSecurityAlliance/csa-skilljar` against this
program on 2026-08-26. That repository's `SECURITY.md` deliberately delegates all
process to this one and does not restate the CVE mechanism, so it needs no change
either way.

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
