# website-building-workflow

A repeatable workflow for building and deploying websites, published as a docs site via MkDocs Material on GitHub Pages.

## Docs site

Published at: <https://jojo275.github.io/website-building-workflow/>

## Local development

```bash
uv sync
uv run mkdocs serve
```

## Structure

```text
docs/        # MkDocs source — published content
project/     # Internal design/planning docs (not published)
.github/     # GitHub Actions deploy workflow
```

## Pre-commit

```bash
uv run pre-commit install
```
