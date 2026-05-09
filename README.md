# website-building-workflow

A repeatable workflow for building and deploying websites, published as a docs site via MkDocs Material on GitHub Pages.

The site is intentionally information-dense — each page covers a full topic with worked examples, reference tables, and code snippets, rather than light overviews. Browse the workflow pages in order for a first read; use the search or nav for reference afterwards.

## Docs site

Published at: <https://jojo275.github.io/website-building-workflow/>

## Commands

```bash
task setup    # install dependencies + git hooks (once after clone)
task serve    # local dev server → http://127.0.0.1:8001
task build    # build site (mirrors CI)
task lint     # run all lint checks
task upgrade  # upgrade dependencies
```

Run `task` with no arguments to list all available tasks.
See [project/v1/commands.md](project/v1/commands.md) for the full reference.

## Structure

```text
docs/           # MkDocs source — published content
design-source/  # Raw design files (not published)
project/        # Internal planning docs (not published)
.github/        # GitHub Actions deploy workflow
```
