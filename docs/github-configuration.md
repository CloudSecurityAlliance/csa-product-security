# GitHub Configuration

This document describes what CSA has configured in GitHub to support the product security program, and how to reproduce or verify the configuration.

## Organization-Level Security Configuration

CSA uses the **GitHub-recommended security configuration** applied to all repositories in the `CloudSecurityAlliance` organization.

### How It Was Configured

1. Go to **github.com/CloudSecurityAlliance** → **Settings**
2. In the sidebar: **Security** → **Advanced Security** → **Configurations**
3. Select the **GitHub-recommended** security configuration
4. Apply to: **All repositories**
5. Use as default for newly created repositories: **All repositories**
6. Enforce configuration: **Enabled**

### What This Enables

| Feature | Public Repos | Private Repos |
|---|---|---|
| Private Vulnerability Reporting | Enabled (free) | Not available (GitHub limitation) |
| Security Advisories | Enabled (free) | Not available (GitHub limitation) |
| Dependabot Alerts | Enabled (free) | Enabled (free) |
| Dependency Graph | Enabled (free) | Enabled (free) |
| Dependabot Security Updates | Enabled (free) | Enabled (free) |
| Code Scanning (CodeQL) | Enabled (free) | Requires GitHub Advanced Security (paid) |
| Secret Scanning | Enabled (free) | Requires GitHub Advanced Security (paid) |
| Push Protection | Enabled (free) | Requires GitHub Advanced Security (paid) |

Private repos will show as "failed" for features that require GitHub Advanced Security. This is expected and correct — the free features (Dependabot, dependency graph) still apply.

### GitHub Advanced Security

CSA does not currently use GitHub Advanced Security (GHAS) for private repositories. GHAS is free for public repos and billed per active committer for private repos. The free public-repo coverage is sufficient for CSA's current needs since CSA's software products are primarily open source.

## Organization-Wide SECURITY.md

A default `SECURITY.md` is maintained in the [`CloudSecurityAlliance/.github`](https://github.com/CloudSecurityAlliance/.github) repository. This file automatically applies to every repo in the organization that does not have its own `SECURITY.md`.

The SECURITY.md directs reporters to use GitHub's Private Vulnerability Reporting and links to this repository for full policy details.

Individual repos can override this with their own SECURITY.md if they have specific requirements, but the organization default covers the standard case.

## Private Vulnerability Reporting Workflow

When PVR is enabled, each public repo gets a "Report a vulnerability" button in its Security tab. The workflow:

1. Reporter clicks "Report a vulnerability" → fills out form → submits
2. Report is private — visible only to repo maintainers and the reporter
3. GitHub automatically adds the reporter as a collaborator and credited user
4. Maintainers can: comment privately, accept as draft advisory, create a temporary private fork, or close
5. When ready, maintainers publish the advisory — it becomes public
6. Published advisories can be edited/updated at any time (URL stays the same, edit history stays private)
7. GitHub reviews published advisories and may add them to the GitHub Advisory Database and trigger Dependabot alerts

### API Access

All advisory operations are available through the GitHub REST API:

| Operation | Method | Endpoint |
|---|---|---|
| List org advisories | GET | `/orgs/{org}/security-advisories` |
| List repo advisories | GET | `/repos/{owner}/{repo}/security-advisories` |
| Create advisory | POST | `/repos/{owner}/{repo}/security-advisories` |
| Submit PVR report | POST | `/repos/{owner}/{repo}/security-advisories/reports` |
| Get advisory | GET | `/repos/{owner}/{repo}/security-advisories/{ghsa_id}` |
| Update advisory | PATCH | `/repos/{owner}/{repo}/security-advisories/{ghsa_id}` |

The `gh` CLI can access these via `gh api`. There are no dedicated `gh` subcommands for security advisories, but the API endpoints are fully functional.

## What About Private Repos?

PVR and security advisories are only available on public repos. This is a GitHub platform limitation, not a configuration choice. Private repositories do not have access to PVR or security advisories. The organization-wide default SECURITY.md directs reporters to PVR, which will not work for private repos. Each private repository should have its own SECURITY.md with reporting instructions appropriate to that repo. Since only users with repository access can view private repos, this is handled on a per-repo basis.

When a private repo is made public, the enforced org-wide security configuration should automatically enable PVR. Delete the repo's custom SECURITY.md at that point so the organization default takes over. Verify that the "Report a vulnerability" button appears in the Security tab after the transition.

## Verification

To verify the current configuration:

```bash
# Check org-level security advisories
gh api /orgs/CloudSecurityAlliance/security-advisories

# Check a specific repo's advisory status
gh api /repos/CloudSecurityAlliance/{repo}/security-advisories

# Verify SECURITY.md exists in .github
gh api /repos/CloudSecurityAlliance/.github/contents/SECURITY.md
```
