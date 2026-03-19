<!-- markdownlint-disable MD041 -->
<!-- markdownlint-disable MD033 -->
<div align="center">

<h1>Python HelloWorld Template</h1>

<strong>A modern Python starter for libraries, packages, and small applications</strong>

Fast setup, opinionated tooling, documentation, CI workflows, and AI-assisted development out of the box.

[Quick Nav](#quick-nav) · [Why This Template](#why-this-template) · [Quick Start](#quick-start) · [Tooling](#what-is-included) · [Structure](#repository-layout) · [Full Docs](docs/index.md)

</div>
<!-- markdownlint-enable MD033 -->

## Quick Nav

- [Why This Template](#why-this-template)
- [Quick Start](#quick-start)
- [What Is Included](#what-is-included)
- [Repository Layout](#repository-layout)
- [AI-Assisted Development](#ai-assisted-development)
- [CI, Docs, and Security](#ci-docs-and-security)

## Why This Template

This repository is a reusable Python project template built for fast project bootstrap without sacrificing engineering discipline. It combines a minimal codebase with an opinionated development workflow: fast dependency management through `uv`, linting and formatting with `ruff`, type checking with `ty`, testing with `pytest`, documentation with `zensical`, and CI workflows for quality, tests, docs, publishing, and secret scanning.

It is also designed for AI-assisted development from the start. The repository already contains agent-oriented structure under `.agents/`, and this project now includes an `AGENTS.md` file so coding agents can work with accurate repository context and conventions.

## Quick Start

There are three practical ways to create a new project from this template:

1. Use GitHub's **Use this template** button.
2. Use GitHub's repository import flow with `https://github.com/zenless-lab/python-helloworld.git` if you want to avoid the generated-from badge.
3. Clone the repository locally, remove `.git`, and initialize a fresh Git history.

After creating the new repository, reinitialize it for your actual project type:

```bash
rm -rf src uv.lock pyproject.toml
uv init --lib
uv add --dev pre-commit pytest pytest-cov pytest-mock ruff ty zensical
cat pyproject.template.toml >> pyproject.toml
rm pyproject.template.toml
```

Then review and replace the placeholder content in `tests/` and `docs/`.

To set up the development environment in this repository layout:

```bash
uv sync
uv run pre-commit install
```

## What Is Included

- **Dependency and environment management:** `uv`
- **Formatter and linter:** `uv run ruff format` and `uv run ruff check --fix`
- **Type checking:** `uv run ty check`
- **Tests:** `uv run pytest`
- **Documentation site generation:** `zensical`
- **Git hooks:** `uv run pre-commit install`
- **Node.js in the development environment:** available for running the `skills` CLI via `pnpm dlx`

Why these choices:

- `uv` keeps setup and dependency operations fast.
- `ruff` replaces several older tools with one consistent workflow.
- `ty` adds a dedicated type-checking pass without bloating the stack.
- `pytest` remains the most flexible and widely understood testing framework in Python.
- `zensical` gives the template a documentation pipeline with a modern output site.

## Repository Layout

The following structure is based on the current repository contents, not a hypothetical layout:

```text
.
├── .agents/                 # Agent resources and installed skill workspace
├── .devcontainer/           # Dev container configuration
├── .github/workflows/       # CI workflows for docs, publish, quality, secrets, and tests
├── docs/                    # Documentation source files for the site
├── notebooks/               # Notebook workspace placeholder
├── scripts/                 # Project scripts
├── site/                    # Generated documentation output
├── src/python_helloworld/   # Template Python package
├── tests/                   # Pytest-based tests
├── .gitleaks.toml           # Secret and PII scanning rules
├── .pre-commit-config.yaml  # Local quality and safety hooks
├── pyproject.toml           # Active project configuration
├── pyproject.template.toml  # Template config to append after `uv init`
├── requirements.txt         # Exported requirements snapshot
├── uv.lock                  # Locked dependency resolution
└── zensical.toml            # Documentation site configuration
```

## AI-Assisted Development

This template is intentionally structured for AI-assisted programming. The repository ships with an `AGENTS.md` guide that explains the repository at a useful level for coding agents.

Default skills are no longer stored directly in the template repository. Instead, install them on first setup with the `skills` command:

```bash
pnpm dlx skills add zenless-lab/skills --skill python-docstring-expert --skill python-comment-expert --skill google-docstring-crafter --skill secret-scanner --skill skill-crafter --skill agents-md-crafter --skill readme-crafter --skill conventional-commits
```

What this command does:

- `pnpm dlx` downloads and runs the `skills` CLI without requiring a permanent global install.
- `skills add` tells the CLI to install skills into the current repository's agent workspace.
- `zenless-lab/skills` is the source repository that provides the published skills.
- Each `--skill ...` flag selects one default skill to install, such as docstring, commenting, README, commit-message, and secret-scanning helpers.

The development environment includes Node.js so this command can run directly in the dev container. If you want additional skills beyond the default set above, browse the available catalog in the `zenless-lab/skills` repository and install the ones you need.

Agents may update `AGENTS.md` when they make structural changes, but that should not be treated as self-maintaining truth. When the repository changes in meaningful ways, review and update `AGENTS.md` so it continues to match reality. That extra maintenance step materially improves agent output quality, especially with lighter models.

## CI, Docs, and Security

The workflow set in `.github/workflows/` currently covers:

- `quality.yaml` for quality gates
- `test.yaml` for automated testing
- `docs.yml` for documentation generation
- `publish.yaml` for publishing workflows
- `secret-scan.yaml` for secret scanning

The local gitleaks rules are intentionally strict. In addition to generic secret scanning, `.gitleaks.toml` blocks non-anonymous email addresses and public IPs, while allowing GitHub and GitLab noreply addresses. This is meant to reduce the chance of pushing personal information into the repository or downstream package releases. If your project intentionally needs an address that would otherwise be blocked, update the allowlist in `.gitleaks.toml`.

## Read More

Detailed guidance is available in the docs site source:

- [Documentation home](docs/index.md)
- [Getting started](docs/getting-started.md)
- [Repository structure](docs/repository-structure.md)
- [Development workflow](docs/development-workflow.md)
