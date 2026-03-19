# Getting Started

This page covers the intended setup flow for creating a new project from the template.

## Choose a Creation Method

Use one of these three approaches:

1. Use GitHub's **Use this template** button.
2. Use GitHub's import-repository flow with `https://github.com/zenless-lab/python-helloworld.git` if you do not want the generated-from marker.
3. Clone the repository, remove `.git/`, and initialize a new Git repository yourself.

## Reinitialize the Project

After the new repository exists, remove the template package and project metadata so `uv` can generate the project shape you actually want:

``` bash
rm -rf src uv.lock pyproject.toml
uv init --lib
```

Replace `--lib` with `--package` or `--app` if that better matches your target.

## Restore the Template Tooling

Install the development dependencies that this template expects:

``` bash
uv add --dev pre-commit pytest pytest-cov pytest-mock ruff ty zensical
```

Then append the template configuration and remove the template file:

```bash
cat pyproject.template.toml >> pyproject.toml
rm pyproject.template.toml
```

## Install Dependencies and Hooks

Once the project metadata is in place, install the environment and Git hooks:

```bash
uv sync
uv run pre-commit install
```

These steps align the local environment with the repository configuration and enable automated checks before commits.

## Install Default Skills

This template no longer stores preset skills directly in the repository. On first setup, install the default skill set with:

```bash
pnpm dlx skills add zenless-lab/skills --skill python-docstring-expert --skill python-comment-expert --skill google-docstring-crafter --skill secret-scanner --skill skill-crafter --skill agents-md-crafter --skill readme-crafter --skill conventional-commits
```

This command means:

- `pnpm dlx` downloads and runs the `skills` CLI without a permanent global install.
- `skills add` installs skills into the current repository's agent workspace.
- `zenless-lab/skills` is the source repository for the published skills.
- Each `--skill ...` flag picks one default skill to install.

The development environment includes Node.js so this command can run directly in the dev container. For more skills beyond the default set, check the `zenless-lab/skills` repository and install the ones that fit your workflow.

## Replace Placeholder Content

This repository intentionally keeps the example implementation very small. Before starting real work, review and replace:

- `src/` with your real package or app modules
- `tests/` with tests that match the new behavior
- `docs/` with project-specific documentation
- `zensical.toml` with your actual documentation site metadata

## Recommended First Checks

After setup, run the standard local checks once:

```bash
uv run ruff format
uv run ruff check --fix
uv run ty check
uv run pytest
```

If these commands pass, the template has been reinitialized correctly for normal development.
