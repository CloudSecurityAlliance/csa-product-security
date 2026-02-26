# Repository Guidelines

## Project Structure & Module Organization
Root-level `README.md` maps the full program scope and links to `docs/governance-framework.md`. All live policies, playbooks, and references live in `docs/`, grouped by severity, SLA, configuration, and pending actions (for example, add new disclosure content beside `docs/vulnerability-handling-process.md`). Use `website-cloudsecurityalliance.org/` only for historical context and keep experimental work inside `tmp/`. There is no compiled code today, so treat every Markdown file as source and ensure new assets stay under the closest policy directory with relative links.

## Build, Test, and Development Commands
Run `npx markdownlint-cli2 "**/*.md"` before every commit to catch heading, spacing, and table issues. Validate links with `npx markdown-link-check README.md docs/*.md` or target only touched files to keep reviews fast. Preview long tables or flows using `gh pr view --web` or your editor’s Markdown preview to confirm column alignment and list formatting.

## Coding Style & Naming Conventions
Prefer ATX headings in sentence case and keep paragraphs under four sentences. Narrate processes with numbered lists, reserve bullets for principles, and mirror the README table style (`| column | column |`). Use descriptive kebab-case filenames such as `docs/reporting-workflow.md`, wrap commands like `npx markdownlint-cli2` in backticks, and stick to US English spelling. Add brief comments only when a policy step needs clarification.

## Testing Guidelines
Proofread like testing: re-run every referenced command in a fresh shell, open each new link, and confirm SLA terminology matches `docs/governance-framework.md`, `docs/severity-classification.md`, and `docs/sla-commitments.md`. When editing sequences or SLAs, cross-check dates and versions, then document assumptions inline instead of leaving TODOs.

## Commit & Pull Request Guidelines
Write imperative commit subjects near 60 characters (for example, `docs: refine disclosure flow`) and explain why the change matters in the body. Pull requests must call out scope impact (web/service/software/AI), link CSA actions or issues, and include screenshots or command output when formatting or tooling behavior is relevant. Request review for any policy, severity, SLA, or governance change and reference `docs/pending-actions.md` for tasks that need coordination outside GitHub.

## Security & Configuration Tips
Never include sensitive reporter details; this repo is intentionally public. Reference GitHub-native workflows (PVRs, advisories, Dependabot) when discussing software fixes, and log cross-team follow-ups in `docs/pending-actions.md`. Flag inconsistencies immediately so downstream guidance stays aligned.
