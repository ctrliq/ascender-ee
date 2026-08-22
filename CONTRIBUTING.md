# Contributing to the Ascender Execution Environment

Thanks for your interest in contributing to the Ascender Execution Environment. This document covers the
development setup, testing, and pull request guidelines.

## Development setup

Fork and clone the repository:

```bash
git clone https://github.com/<your-user>/ascender-ee.git
cd ascender-ee
```

Install [ansible-builder](https://ansible-builder.readthedocs.io/en/stable/installation/),
then build the image:

```bash
ansible-builder build -v3 -t ghcr.io/ctrliq/ascender-ee
```

## Running tests

A successful build is the primary check. Linting runs through tox:

```bash
tox
```

Collections and Python packages baked into the image are pinned in
[`execution-environment.yml`](./execution-environment.yml). When adding one,
pin the version and say in the PR why the image needs it.


## Making changes

### Branching

Create a feature branch from `main`:

```bash
git checkout -b my-feature main
```

### Commit messages

Write clear, concise commit messages:

```
Short summary (under 72 characters)

Longer description of what changed and why, if needed.
```

## Submitting a PR

1. Make sure the checks above pass locally.
2. One logical change per PR. Do not bundle unrelated fixes.
3. Target the `main` branch.
4. Explain what changed and why in the PR description.

## Reporting issues

Open an issue at
[github.com/ctrliq/ascender-ee/issues](https://github.com/ctrliq/ascender-ee/issues).
Include the version you are running and the steps that reproduce the problem.

For security vulnerabilities, follow [SECURITY.md](./SECURITY.md) instead of
opening a public issue.
