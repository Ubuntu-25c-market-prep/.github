# .github

Organisation-level configuration: the public profile, issue and pull request
templates, and reusable workflows every repository calls.

**Owner:** `@cto`

## Contents

| Path | What it does |
|---|---|
| `profile/README.md` | The organisation landing page at github.com/Ubuntu-25c-market-prep |
| `.github/ISSUE_TEMPLATE/` | Issue forms, including the workstream dropdown |
| `.github/PULL_REQUEST_TEMPLATE.md` | Applies to every repository without one of its own |
| `.github/workflows/security-scan.yml` | Reusable security scan called by all code repositories |

## The security scan

Every code repository calls this rather than copying it, so a fix lands
everywhere at once.

```yaml
# .github/workflows/security.yml in a consuming repository
jobs:
  scan:
    uses: Ubuntu-25c-market-prep/.github/.github/workflows/security-scan.yml@main
```

Three jobs:

| Job | Catches |
|---|---|
| **Secrets** | gitleaks across full history, results to code scanning |
| **Forbidden files** | `.tfvars`, state, kubeconfig, `.pem`, `.env` — things a credential scanner will not flag |
| **IaC misconfiguration** | Trivy config scan, HIGH and CRITICAL |

This is defence in depth behind GitHub's native secret scanning and push
protection, which are enabled on every repository. Native scanning catches
credential *patterns*; it does not catch a committed state file or a bare account
id, which leak just as much.

## Changing the reusable workflow

It runs on every repository, so a mistake blocks all of them.

- A reusable workflow's `permissions` block **defines** the token — it is not
  merged with the caller's. `security-events: write` must stay, or SARIF upload
  fails while the scan itself appears to pass.
- Pin scanner versions. `:latest` means the same commit scans differently on
  different days.
- Test on one repository before merging.

## Standards

[Engineering Handbook](https://github.com/Ubuntu-25c-market-prep/ops-program/blob/main/docs/engineering-handbook.md)
