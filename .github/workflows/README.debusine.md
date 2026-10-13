# Debusine CI Workflows

This directory contains GitHub Actions workflows for Debian package building and releasing via Debusine.

## Workflows

### pkg-pr-hook.yml
Automatically triggered on pull requests to `qcom/**` and `qli/**` branches.
Also supports manual triggering via `workflow_dispatch`.

**Manual trigger**: Go to Actions → PR Build → Run workflow → enter branch name

### pkg-release.yml
Manual workflow for releasing packages to Staging or Production environments.

**Manual trigger**: Go to Actions → Release → Run workflow → select environment and branch

## Requirements

- Repository must have `is-pkg-repo` custom property set to `true`
- GHCR `pkg-builder` image access (for Ubuntu builds)
- Debusine credentials (for Debian builds)
