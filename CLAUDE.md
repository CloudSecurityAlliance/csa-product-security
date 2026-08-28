# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

The authoritative home of the Cloud Security Alliance (CSA) product security /
PSIRT program. It is **documentation only** — there is no application code, no
build system, no test suite, and no CI. Every Markdown file is source, and the
published documents are the product.

`AGENTS.md` is the contributor guide (structure, prose style, commit and PR
expectations) and applies to Claude too. Read it before editing; this file
covers only what `AGENTS.md` does not.

## Verification

There is no compiler to catch mistakes, so lint and link checks are the tests:

```bash
npx markdownlint-cli2 "**/*.md"                     # run before every commit
npx markdown-link-check README.md docs/*.md         # or just the touched files
npx markdown-link-check docs/sla-commitments.md     # single-file check
```

Two things to know before you act on the output:

- **The baseline is not clean.** As of 2026-08-27 a whole-repo run reports ~859
  issues, nearly all of them pre-existing: `MD013` line-length in the
  intentionally unwrapped `SECURITY.md`, `SECURITY-internal.md`, and `AGENTS.md`,
  plus a large pile in gitignored `tmp/`. Lint the files you touched and compare
  against that baseline; do not treat a nonzero exit as your regression, and do
  not "fix" the unwrapped root files.
- **The glob reaches into `tmp/`.** `"**/*.md"` ignores `.gitignore`, so scratch
  drafts dominate the report. Filter them out (`| grep -v '^tmp/'`) or lint
  explicit paths.

No markdownlint config is committed, so CLI defaults apply.
`docs/decision-log.md` wraps itself in `<!-- markdownlint-disable MD013 -->` /
`enable` because its decision entries are single long lines by design; prefer
wrapping to ~80 columns over adding new disables.

## Document authority map

Facts are deliberately restated across reporter-facing and internal documents,
which means most edits are multi-file edits. One document owns each fact:

| Fact | Authoritative source | Restated in (must be updated together) |
| --- | --- | --- |
| SLA targets (5 business days / 30 days / 90 days) | `docs/sla-commitments.md` | `README.md`, `SECURITY.md`, `docs/governance-framework.md`, `docs/vulnerability-disclosure-policy.md`, `docs/vulnerability-handling-process.md`, `docs/decision-log.md` |
| Scope and asset categories (websites/services, software, AI prompts) | `docs/governance-framework.md` | `README.md`, `SECURITY.md`, `docs/vulnerability-disclosure-policy.md` |
| Eight-step lifecycle | `docs/governance-framework.md` | `README.md`, `docs/vulnerability-handling-process.md` |
| Severity model (CVSS v3.1 / OWASP AIVSS) | `docs/severity-classification.md` | `docs/governance-framework.md`, `docs/vulnerability-handling-process.md` |
| CVE assignment policy and CNA scope | `docs/vulnerability-disclosure-policy.md` | `README.md`, `SECURITY.md`, `docs/governance-framework.md`, `docs/vulnerability-handling-process.md` |
| Why a choice was made | `docs/decision-log.md` | — |
| Work that must happen outside this repo | `docs/pending-actions.md` | `TODO.md` (index line per item) |

Split by audience, not by topic: `docs/vulnerability-disclosure-policy.md` is
reporter-facing, `docs/vulnerability-handling-process.md` is the internal
execution of the same lifecycle, and `docs/governance-framework.md` is the
umbrella both implement.

**Known drift to be careful of:** `SECURITY.md` lists five CSA GitHub orgs
(`CloudSecurityAlliance`, `-Chatbots`, `-DataSets`, `modelcontextprotocol-security`,
`RiskRubric`); `README.md` and `docs/governance-framework.md` still name only
`CloudSecurityAlliance`. Treat the five-org list as current and reconcile the
others when touching scope text.

## Conventions specific to this repo

- **Versioned docs.** Every file in `docs/` opens with `Version: N.N (YYYY-MM-DD)`
  under the `# H1`. Bump it when the substance changes; root files
  (`README.md`, `SECURITY.md`) carry no version header.
- **Decision log is append-only.** Never rewrite or delete an entry. Add a new
  dated decision and mark the old one
  `**Superseded by**: [Title](#anchor) on YYYY-MM-DD`. Entries keep the shape
  Decision / Alternatives considered / Rationale, newest last, separated by `---`.
- **`TODO.md` is an index, not content.** One line per open item pointing at the
  real detail (usually a `docs/pending-actions.md` anchor). New follow-up work
  goes in `pending-actions.md` with a `**Status**:` line, plus a `TODO.md` line.
  Keep anchors in sync — the index is only useful if its links resolve.
- **Line width.** Files in `docs/` wrap at ~80 columns. `SECURITY.md` and
  `AGENTS.md` are intentionally unwrapped; leave them that way.
- **Relative links inside the repo, absolute GitHub URLs in `SECURITY.md`** —
  that file is meant to be copied into the `.github` org repo, where relative
  links would break.

## Directories that are not documentation

- `tmp/` — gitignored scratch space (drafts, plans, CNA reference material). Never
  link to it from a tracked file and never assume a reader can see it.
- `website-cloudsecurityalliance.org/` — read-only reference copies of
  `/.well-known/security.txt` (managed in Cloudflare) and `/security/` (managed in
  CSA's CMS). Editing files here changes nothing live; real changes go through
  those platforms and belong in `docs/pending-actions.md`.

## Environment note

`/Volumes/MacMiniData/Users/kurt/GitHub/CloudSecurityAlliance/csa-product-security`
and `/Users/kurt/GitHub/CloudSecurityAlliance/csa-product-security` are the same
checkout reached through two paths. There is nothing to keep in sync between them.

## Content boundaries

This repo is intentionally public. Never commit reporter identities, embargoed
advisory details, unpublished vulnerability specifics, or exploit material.
Advisories themselves are never stored here. CSA is a CNA (`CSAI`,
`CNA-2026-0025`) and assigns CVE IDs directly for software in its CNA scope; the
CVE Record on the CVE List is authoritative, GHSA is cross-referenced, and
published advisories are listed at `labs.cloudsecurityalliance.org/advisories/`.

Two things to keep straight when touching CVE language:

- **CNA scope is narrower than PSIRT scope.** The registered scope is
  `github.com/CloudSecurityAlliance/*` only. Other CSA GitHub orgs, websites,
  and services are handled by the program but get no CSA-assigned CVE ID. Do not
  widen the scope wording in the docs to match `SECURITY.md`'s five-org list —
  that would overclaim against the cve.org record.
- **`docs/vulnerability-disclosure-policy.md` is externally referenced.** cve.org
  links to it as CSA's public CNA policy of record. Do not rename or move it
  without updating the CNA record first.
