# website-building-workflow

A repeatable workflow for building and deploying websites, published as a docs site via MkDocs Material on GitHub Pages.

## Docs site

Published at: <https://jojo275.github.io/website-building-workflow/>

## Commands

```bash
uv sync                          # install dependencies
uv run pre-commit install        # install git hooks (once after clone)
uv run mkdocs serve              # local dev server → http://127.0.0.1:8000
uv run mkdocs build --strict     # build (mirrors CI)
uv run pre-commit run --all-files  # run all lint checks
```

See [project/v1/commands.md](project/v1/commands.md) for the full reference.

## Structure

```text
docs/           # MkDocs source — published content
design-source/  # Raw design files (not published)
project/        # Internal planning docs (not published)
.github/        # GitHub Actions deploy workflow
```
