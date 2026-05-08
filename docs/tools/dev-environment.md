# Dev Environment

Editors, version control, package managers, linters, formatters, and testing tools.

## Code Editors

### VS Code

The most widely used editor for web development. Free, open source, and highly extensible.

Recommended extensions for web development:

- **Prettier** — automatic code formatting
- **ESLint** — JavaScript/TypeScript linting
- **Tailwind CSS IntelliSense** — class name autocomplete
- **Prisma** — schema syntax highlighting
- **GitHub Copilot** — AI code completion
- **GitLens** — enhanced Git history and blame

<https://code.visualstudio.com>

### Cursor

A fork of VS Code with deeper AI integration. Supports agent mode, multi-file edits, and codebase-wide context.

**Good for:** AI-assisted development, rapid prototyping, large codebases.

<https://cursor.sh>

### Zed

A fast, collaborative editor written in Rust. Lightweight with built-in multiplayer and AI features.

<https://zed.dev>

## Version Control

### Git

The standard version control system. All web development workflows depend on it.

Essential commands:

```bash
git init
git add .
git commit -m "message"
git push origin main
git pull
git checkout -b feature/name
```

<https://git-scm.com>

### GitHub

The standard platform for hosting Git repositories, pull requests, code review, and CI/CD.

- Pull requests and code review
- GitHub Actions for CI/CD
- GitHub Pages for static site hosting
- Issues and project boards

<https://github.com>

### GitLab

An alternative to GitHub with built-in CI/CD pipelines and self-hosting options.

<https://gitlab.com>

## Package Managers

### npm

The default Node.js package manager. Installed with Node.js.

```bash
npm install
npm run dev
npm run build
```

### pnpm

A faster, more disk-efficient alternative to npm. Recommended for most new projects.

```bash
pnpm install
pnpm dev
pnpm build
```

<https://pnpm.io>

### Bun

A fast all-in-one JavaScript runtime, package manager, and bundler.

<https://bun.sh>

### uv (Python)

A fast Python package and project manager that replaces pip and virtualenv.

```bash
uv sync
uv run python script.py
uv add fastapi
```

<https://docs.astral.sh/uv>

## Linting and Formatting

### ESLint

The standard JavaScript/TypeScript linter. Catches errors, style issues, and potential bugs.

```bash
npx eslint .
```

<https://eslint.org>

### Prettier

An opinionated code formatter for JavaScript, TypeScript, CSS, HTML, Markdown, and JSON.

```bash
npx prettier --write .
```

<https://prettier.io>

### Ruff (Python)

An extremely fast Python linter and formatter. Replaces flake8, black, isort, and more.

```bash
ruff check .
ruff format .
```

<https://docs.astral.sh/ruff>

### markdownlint

A linter for Markdown files. Enforces consistent style and catches common errors.

<https://github.com/DavidAnson/markdownlint>

## Testing Tools

### Vitest

A fast unit and component testing framework built on Vite. The modern replacement for Jest in Vite-based projects.

```bash
npx vitest
```

<https://vitest.dev>

### Jest

The most widely used JavaScript testing framework.

<https://jestjs.io>

### Playwright

End-to-end browser testing. Runs real browser interactions across Chromium, Firefox, and WebKit.

```bash
npx playwright test
```

<https://playwright.dev>

### Cypress

An end-to-end testing framework with a visual test runner.

<https://cypress.io>

## Terminal

### Windows Terminal

A modern terminal for Windows supporting multiple tabs, panes, and shell profiles (PowerShell, WSL, Git Bash).

<https://apps.microsoft.com/store/detail/windows-terminal>

### WSL2

Windows Subsystem for Linux 2. Runs a full Linux environment inside Windows, useful for Node.js and Python development.

<https://learn.microsoft.com/windows/wsl>
