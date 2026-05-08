# design-source

Raw and supporting design materials for the website-building-workflow project.

This folder is **not** published to the MkDocs site. It tracks design files
alongside the code so context is preserved in version history.

## Structure

```text
design-source/
  exports/      ← exported images and diagrams referenced in docs/
  diagrams/     ← source diagram files (.drawio, etc.)
  references/   ← competitor notes, visual references, research
```

## Guidelines

- Export images used in docs to `exports/` and reference them from `docs/assets/`
- Keep large binary files out of this repo — use Git LFS or link to external tools
- Figma files live in Figma; store the share link in `references/` instead
