# Workflow Commands

Reference for all commands used in day-to-day work on this repo.

---

## Setup

Install dependencies and activate the virtual environment:

```bash
uv sync
```

Install git hooks (run once after cloning):

```bash
uv run pre-commit install
```

---

## Local Development

Start the MkDocs dev server with live reload:

```bash
uv run mkdocs serve
```

Preview at <http://127.0.0.1:8000/website-building-workflow/>

Build the site locally (outputs to `site/`):

```bash
uv run mkdocs build
```

Build with strict mode (fails on warnings — same as CI):

```bash
uv run mkdocs build --strict
```

---

## Linting and Checks

Run all pre-commit hooks against every file:

```bash
uv run pre-commit run --all-files
```

Run a single hook by ID:

```bash
uv run pre-commit run markdownlint --all-files
uv run pre-commit run check-yaml --all-files
uv run pre-commit run trailing-whitespace --all-files
```

---

## Dependency Management

Add a runtime dependency:

```bash
uv add <package>
```

Add a dev dependency:

```bash
uv add --dev <package>
```

Update all dependencies to latest compatible versions:

```bash
uv lock --upgrade
uv sync
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
