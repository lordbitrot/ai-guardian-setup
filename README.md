# ai-guardian-setup

This repository is a draft one-click bundle for an AI watchdog setup.

It includes:
- Dependabot for dependency updates
- semgrep for security/static checks
- GitHub Actions to block high-risk PRs
- a PR approval gate requiring explicit owner review
- CODEOWNERS to enforce sensitive-path owner approval

Use it as a starting point for a repo where a Claude-based assistant or other AI can help with maintenance, but must not do irreversible things without your approval.

## Included files

- `.github/workflows/ai-guardian.yml` — blocks risky/irreversible PRs
- `.github/workflows/owner-approval-check.yml` — requires owner approval
- `.github/workflows/semgrep.yml` — runs Semgrep on push/PR
- `.github/semgrep-rules.yml` — custom prompt/safety guard rules
- `.github/dependabot.yml` — weekly dependency update PRs
- `.github/CODEOWNERS` — marks sensitive files as owner-only
- `scripts/check_irreversible.py` — scans PR patches for unsafe changes
- `docs/branch-protection.md` — setup instructions

## Quick start

1. Copy the files into your project repo.
2. Update the owner username in the workflow files.
3. In GitHub, enable branch protection on your default branch.
4. Require the status checks:
   - `ai-guardian`
   - `owner-approval`
   - `semgrep-scan`
   - your CI checks
5. Merge the PR after approval.

## Important note

This is a guardrail system, not a replacement for review. It is designed to help you say: “AI can act, but not with destructive or irreversible changes unless I approve.”
