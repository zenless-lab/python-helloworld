# AGENTS.md

## Project Context

- This repository is a Python library template built around a minimal package in `src/python_helloworld`.
- The active toolchain is `uv` for environment and dependency management, `ruff` for formatting and linting, `ty` for type checking, `pytest` for tests, `pre-commit` for local hooks, and `zensical` for documentation builds.
- The repository already contains agent-specific files under `.github/agents/`, but this file is the root execution guide for coding agents.

## Source Of Truth

- Treat `src/`, `tests/`, `docs/`, `.github/workflows/`, `pyproject.toml`, `.pre-commit-config.yaml`, `.gitleaks.toml`, and `zensical.toml` as authoritative project inputs.
- Treat `site/` as generated documentation output. Do not hand-edit files under `site/` unless the user explicitly asks for generated artifact changes.
- `requirements.txt` is exported output from `uv export --frozen --output-file=requirements.txt`. Update it through the configured workflow, not by manual package edits.
- `uv.lock` is managed by `uv` and the pre-commit hooks.

## Setup And Core Commands

- Sync the environment with `uv sync`.
- Install local hooks with `uv run pre-commit install`.
- Format Python code with `uv run ruff format`.
- Run lint fixes with `uv run ruff check --fix`.
- Run type checks with `uv run ty check` locally. CI uses `uv run ty check --output-format=github`.
- Run tests with `uv run pytest`.
- Build distributions with `uv build`.
- Build documentation with `uv run zensical build --clean`.

## Repository Layout

- `src/python_helloworld/`: example typed package.
- `tests/`: pytest suite for package behavior.
- `docs/`: documentation sources.
- `site/`: generated documentation site.
- `scripts/`: project automation scripts.
- `notebooks/`: notebook workspace.

## Implementation Guidance

- Keep changes focused and minimal. This repository is a template, so avoid introducing project-specific complexity unless the user asks for it.
- Prefer English for code, comments, docstrings, and commit messages.
- Prefer Google-style Python docstrings when a docstring is needed.
- Follow the existing Ruff configuration in `pyproject.toml`: line length is 120, relative imports are banned, and `print` is generally disallowed outside configured exceptions.
- `ty` is configured for `src/` and `tests/`, while `scripts/` and `notebooks/` are excluded by default. Do not assume those excluded directories are type-checked.
- Keep package changes aligned with the `src/` layout and update tests together with behavior changes.

## Testing And Validation

- For Python code changes, run `uv run ruff format`, `uv run ruff check --fix`, `uv run ty check`, and `uv run pytest` when the affected area warrants it.
- If packaging behavior changes, also run `uv build`.
- If documentation sources or `zensical.toml` change, rebuild docs with `zensical build --clean` instead of editing generated files.
- Pre-commit also runs trailing whitespace fixes, YAML validation, merge-conflict checks, lockfile export checks, and gitleaks scanning.

## CI Expectations

- `.github/workflows/quality.yaml` runs Ruff and Ty.
- `.github/workflows/test.yaml` runs pytest across Python 3.10 through 3.13, builds distributions, tests built artifacts, and scans build outputs for secrets.
- `.github/workflows/docs.yml` builds the documentation site from `docs/` and deploys the generated `site/` directory.
- `.github/workflows/secret-scan.yaml` exists for repository secret scanning. Respect `.gitleaks.toml` when adding examples or fixture data.

## Git Guidance

- Use Conventional Commits by default, for example `feat: add package module` or `docs: update setup guide`.
- Do not revert unrelated user changes.
- Avoid destructive git operations unless the user explicitly asks for them.

## Agent Notes

- Verify commands and paths from repository files before documenting or automating them.
- Prefer editing source files over generated outputs.
- Update this file when repository structure, commands, or quality gates change in a way that would affect future agents.
