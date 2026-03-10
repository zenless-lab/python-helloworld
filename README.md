<div align="center">

# 📦 Python Library Template

**A modern, opinionated foundation for high-performance Python packages.**

[![Python](https://img.shields.io/badge/python-3.10%2B-3776AB?logo=python&logoColor=white&style=flat-square)](https://www.python.org/)
[![Package manager](https://img.shields.io/badge/package%20manager-uv-DE5FE9?style=flat-square)](https://docs.astral.sh/uv/)
[![Lint](https://img.shields.io/badge/lint-ruff-D7FF64?logo=ruff&logoColor=111111&style=flat-square)](https://docs.astral.sh/ruff/)
[![Tests](https://img.shields.io/badge/tests-pytest-0A9EDC?logo=pytest&logoColor=white&style=flat-square)](https://docs.pytest.org/)
<br />
[![Types](https://img.shields.io/badge/types-ty-1F6FEB?style=flat-square)](https://github.com/astral-sh/ty)
[![Docs](https://img.shields.io/badge/docs-zensical-16A085?style=flat-square)](https://pypi.org/project/zensical/)
[![Pre-commit](https://img.shields.io/badge/pre--commit-enabled-FE602F?logo=pre-commit&logoColor=white&style=flat-square)](https://pre-commit.com/)
[![Package layout](https://img.shields.io/badge/layout-src-0F172A?style=flat-square)](#project-layout)

---

[Quick Start](#-quick-start) • [Features](#-features) • [Configuration](#-configuration) • [Contributing](#-contributing)

</div>

## 🚀 Overview

Stop wasting time on boilerplate. **Python Library Template** provides a clean, pre-configured starting point using the latest industry-standard tooling. Focus on writing your code while we handle the ecosystem.

> [!TIP]
> This template is optimized for small-to-medium libraries requiring high reliability and developer velocity.

## ✨ Features

| Category | Tool | Description |
| :---: | :---: | :--- |
| **Workflow** | [**uv**](https://docs.astral.sh/uv/) | Blazing fast Python package and project manager. |
| **Quality** | [**ruff**](https://docs.astral.sh/ruff/) | An extremely fast Python linter and code formatter. |
| **Automation** | [**pre-commit**](https://pre-commit.com/) | Managing and maintaining multi-language pre-commit hooks. |
| **Testing** | [**pytest**](https://docs.pytest.org/) | Simple and powerful testing framework. |
| **Typing** | [**ty**](https://github.com/astral-sh/ty) | Modern type-checking utilities. |
| **Docs** | [**zensical**](https://pypi.org/project/zensical/) | Minimalist, documentation-driven development. |
| **Structure** | [**src layout**](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/) | Prevents common import issues and ensures clean packaging. |

## Start From This Repository

Choose the workflow that matches how you want to adopt the template.

### Option 1: Use GitHub's template flow

1. Open this repository on GitHub.
2. Click **Use this template**.
3. Create a new repository from it.

### Option 2: Import the repository

Use this when you want a new repository without the generated-from-template badge.

1. Open GitHub's **Import repository** page.
2. Paste the source URL below.
3. Choose the new owner, name, and visibility.
4. Start the import.

```text
https://github.com/zenless-lab/python-library.git
```

### Option 3: Clone and reinitialize locally

Use this when you want full control from the command line.

```bash
git clone https://github.com/zenless-lab/python-library.git your-library
cd your-library
```

If you want a fresh Git history:

```bash
rm -rf .git
git init
git add .
git commit -m "Initial commit"
```

## Updating dev dependencies

If you want to remove items from the `dev-dependencies` section in `pyproject.toml`, delete the corresponding entries under the appropriate table (for example `[tool.uv.dev-dependencies]`). After removing unwanted entries, re-run the following to add or update the minimal development dependencies:

```bash
uv add --dev zensical pre-commit ruff ty pytest pytest-cov pytest-mock
```

This command will add or update the listed development packages and record minimal version constraints where applicable.

## First 5 Minutes

Install the environment, confirm the template works, then start replacing the placeholders.

```bash
uv sync
uv run pytest
uv run ruff check .
uv run ruff format .
uv run ty check
uv run pre-commit install
```

To preview the documentation site locally:

```bash
uv run zensical serve
```

To build the static documentation output:

```bash
uv run zensical build --clean
```

## Current Placeholder API

The repository intentionally ships with a tiny public example so the template is executable on day one.

```python
from python_library import hello

message = hello()
assert message == "Hello from python-library!"
```

This implementation is only a smoke-test placeholder. Replace it early with your actual package surface.

## What To Rename Before Shipping

These are the minimum edits to turn the template into a real project.

| Area | What to update |
| ---: | :--- |
| Package metadata | Update `name`, `description`, authors, and Python version support in `pyproject.toml`. |
| Import package | Rename `src/python_library/` to your actual import name. |
| Sample implementation | Replace `hello()` in `src/python_library/__init__.py`. |
| Tests | Replace the placeholder assertion in `tests/test_example.py`. |
| Documentation metadata | Update `site_name`, `site_description`, `site_author`, `site_url`, `repo_name`, and `repo_url` in `zensical.toml`. |
| Repository references | Replace `python-library`, `python_library`, and `zenless-lab/python-library` across the project. |
| Optional directories | Remove `scripts/` or `notebooks/` if they do not fit your project. |

## Recommended Customization Order

1. Rename the package directory in `src/`.
2. Update project metadata in `pyproject.toml`.
3. Replace the placeholder code and tests.
4. Update the documentation metadata in `zensical.toml`.
5. Rewrite the docs in `docs/` to match your API.
6. Rewrite this README for your real library once the public interface is stable.

## Everyday Commands

```bash
uv sync
uv run pytest
uv run ruff check .
uv run ruff format .
uv run ty check
uv run pre-commit run --all-files
uv run zensical serve
uv run zensical build --clean
```

## Project Layout

```text
.
├── docs/                    # Documentation source files
├── notebooks/               # Optional notebooks
├── scripts/                 # Optional utility scripts
├── src/
│   └── python_library/      # Rename this package for your project
├── tests/                   # Test suite
├── pyproject.toml           # Packaging and tool configuration
└── zensical.toml            # Documentation configuration
```

## Template Notes

- Documentation is configured through `zensical.toml`, not `mkdocs.yml`.
- The generated site output lives in `site/`.
- The template currently has no runtime dependencies in `pyproject.toml`.
- The sample package exports a single function, `hello()`.

## A Good First Pass

If you want a practical starting sequence after creating your own repository, use this:

```text
create repository
-> uv sync
-> rename src/python_library
-> update pyproject.toml
-> replace hello()
-> replace tests
-> update zensical.toml
-> rewrite docs/
```

The documentation under `docs/` expands on setup and customization if you want a slower, guided pass through the template.
