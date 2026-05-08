# Website Building Workflow — Design Document (v1)

## Overview

This repository documents a repeatable workflow for building and deploying websites. The workflow is published as a living documentation site using MkDocs Material, hosted via GitHub Pages.

## Goals

- Provide a clear, step-by-step guide for building websites from scratch to deployment
- Serve as a personal/team reference that evolves over time (versioned via `project/vN/`)
- Keep the workflow tool-agnostic where possible, with specific tool recommendations called out explicitly

## Non-Goals

- This repo is not a website builder itself — it documents the *process*
- Not intended to cover every possible tech stack; focuses on the recommended workflow

## Repo Structure

```text
website-building-workflow/
├── docs/                   # MkDocs source — published to GitHub Pages
│   ├── index.md            # Home page
│   ├── workflow/           # Core workflow steps
│   └── reference/          # Reference material, checklists, snippets
├── project/                # Internal design/planning docs (not published)
│   └── v1/
│       └── design.md       # This file
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions — build & deploy MkDocs site
├── .pre-commit-config.yaml # Pre-commit hooks
├── .markdownlint.json      # Markdown lint rules
├── mkdocs.yml              # MkDocs configuration
├── requirements.txt        # Python dependencies (mkdocs + plugins)
└── README.md
```

## Technology Choices

| Concern | Choice | Rationale |
|---|---|---|
| Docs framework | MkDocs Material | Great defaults, search, versioning support, widely used |
| Hosting | GitHub Pages | Free, integrates with GitHub Actions |
| Linting | markdownlint | Keeps markdown consistent; lightweight |
| Pre-commit | pre-commit | Automates lint checks before every commit |
| CI/CD | GitHub Actions | Native to GitHub, no extra tooling |

## Versioning Strategy

Design documents live in `project/vN/design.md`. When a significant revision to the workflow approach is made, a new version folder is created so prior reasoning is preserved.

The *published* docs site does not version-gate content at this stage — the `docs/` tree always reflects the current recommended workflow.

## Open Questions

- [ ] Add `mike` for MkDocs versioned docs deployment in a future version?
- [ ] Add a contributing guide once the workflow stabilises?
