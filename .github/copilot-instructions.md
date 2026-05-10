# Copilot Instructions

Guidelines for GitHub Copilot when working in this repository.

---

## What This Repo Is

**Website Building Workflow** is a personal knowledge base and reference guide for planning, designing, building, testing, and deploying websites. It is published as a static documentation site using MkDocs Material.

There is no application code, no database, no API, and no backend. The only output is the documentation site.

---

## Project Structure

```text
docs/                  ← all documentation source files (markdown)
  workflow/            ← numbered workflow pages (01–12)
  checklists/          ← launch, QA, accessibility, responsive checklists
  starters/            ← reusable templates (screen spec, component spec, etc.)
  conventions/         ← HTML, CSS, and design system conventions
  tools/               ← tool reference pages
site/                  ← built output (generated, do not edit manually)
mkdocs.yml             ← site configuration and nav
mkdocs.local.yml       ← local dev overrides (no GA, etc.)
pyproject.toml         ← dependencies (mkdocs, mkdocs-material)
Taskfile.yml           ← task runner shortcuts
.markdownlint.json     ← markdownlint rules
cspell.json            ← spell checker word list
```

---

## Key Tasks

| Task           | What it does                                      |
| -------------- | ------------------------------------------------- |
| `task serve`   | Start local dev server at `http://127.0.0.1:8001` |
| `task build`   | Build site to `site/` with strict mode            |
| `task lint`    | Run all pre-commit hooks against every file       |
| `task lint:md` | Run markdownlint only                             |
| `task setup`   | Install dependencies and git hooks                |
| `task upgrade` | Upgrade all dependencies                          |

---

## Pre-commit Hooks

- **markdownlint** — enforces `.markdownlint.json` rules
- **cspell** — spell checking against `cspell.json` word list
- **check-yaml** — validates YAML files
- **trailing-whitespace**, **end-of-file-fixer**, **mixed-line-ending** — whitespace hygiene

Validate before committing: `task lint` or `uv run pre-commit run --all-files`

---

## Conventions

### Markdown

- One `#` H1 per file — the page title
- Heading levels are sequential, no skipping
- Duplicate heading names are allowed across different parent sections (`siblings_only: true` in `.markdownlint.json`)
- No bare URLs — use `[text](url)` links
- Code blocks use fenced triple backticks with a language tag (` ```text `, ` ```yaml `, etc.)

### Nav

All pages must be listed in `mkdocs.yml` under `nav:`. New pages are not auto-discovered.

### Spell checking

Unknown words go in `cspell.json` under `words`. Add the word, not a suppression comment.

### Content style

- Direct and practical — this is a reference, not a tutorial
- No filler, no padding
- Examples over abstract explanations
- Tables for comparisons, code blocks for commands and directory trees
- Directory trees use `├──`, `│`, `└──` with `#` inline comments

---

## Working Style

- **Don't add pages without being asked.** Adding content to existing pages is fine; creating new files should be deliberate.
- **Keep the nav in sync.** Any new file added to `docs/` must be added to `mkdocs.yml`.
- **Run lint before finishing.** `task lint` catches markdownlint, cspell, and YAML issues before they hit pre-commit.
- **Don't churn.** Avoid restructuring, renaming, or reformatting content that isn't broken.
- **Flag stale content.** If existing content contradicts something being added, flag it rather than silently ignoring it.

---

## Common Issues

1. **New word flagged by cspell** — add it to `cspell.json` under `words`, not as an inline suppression.
2. **Duplicate heading lint error** — check that `.markdownlint.json` has `"MD024": { "siblings_only": true }`. If headings are genuinely siblings, rename them; if they're under different parents, the rule should pass.
3. **Page not appearing in nav** — add it to `mkdocs.yml` under `nav:`.
4. **Site not updating** — run `task serve` (not `task build`) for live reload during editing.
5. **Lockfile drift** — after editing `pyproject.toml`, run `uv lock` and commit `uv.lock` in the same change.
