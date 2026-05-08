# Workflow Commands

Reference for all commands used in day-to-day work on this repo.

This repo uses [Task](https://taskfile.dev) as a task runner (`Taskfile.yml` in root).
All tasks wrap `uv` commands — you can always run the underlying `uv` command directly
if preferred.

---

## Task Runner Quick Reference

```bash
task           # list all tasks
task setup     # install deps + git hooks
task serve     # local dev server
task build     # build site (strict mode)
task lint      # run all pre-commit hooks
task lint:md   # markdownlint only
task lint:yaml # check-yaml only
task upgrade   # upgrade all dependencies
```

---

## Setup

Install dependencies and activate the virtual environment:

```bash
task setup
# or: uv sync
```

Install git hooks (run once after cloning):

```bash
task setup
# or: uv run pre-commit install
```

---

## Local Development

Start the MkDocs dev server with live reload:

```bash
task serve
# or: uv run mkdocs serve
```

Preview at <http://127.0.0.1:8000/website-building-workflow/>

Build the site locally (outputs to `site/`):

```bash
task build
# or: uv run mkdocs build --strict
```

---

## Linting and Checks

Run all pre-commit hooks against every file:

```bash
task lint
# or: uv run pre-commit run --all-files
```

Run a single hook:

```bash
task lint:md
task lint:yaml
# or: uv run pre-commit run markdownlint --all-files
# or: uv run pre-commit run check-yaml --all-files
```

---

## Dependency Management

Upgrade all dependencies to latest compatible versions:

```bash
task upgrade
# or: uv lock --upgrade && uv sync
```

Add a runtime dependency:

```bash
uv add <package>
```

Add a dev dependency:

```bash
uv add --dev <package>
```

---

## Deployment

Deployment is automatic via GitHub Actions on push to `main`.

To trigger a manual deploy without a push:

1. Go to **Actions → Deploy MkDocs to GitHub Pages**
2. Click **Run workflow**

---

## Hooks Reference

Hooks configured in `.pre-commit-config.yaml`:

| Hook | What it does |
|---|---|
| `trailing-whitespace` | Removes trailing whitespace |
| `end-of-file-fixer` | Ensures files end with a newline |
| `mixed-line-ending` | Normalises line endings to LF |
| `check-yaml` | Validates YAML syntax |
| `check-merge-conflict` | Catches unresolved conflict markers |
| `check-added-large-files` | Prevents large binary commits |
| `markdownlint` | Lints Markdown against `.markdownlint.json` |
