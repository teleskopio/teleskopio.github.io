# AGENTS.md for teleskopio.github.io

## Overview

This project is a blog for application teleskopio, the kubernetes web ui dashboard.
Project build with Eleventy. Eleventy is a simpler static site generator.
Project hosted as github pages and deployed with simple push to the master.

## Directory layout

- `_data/` – configuration for eleventy.
- `_includes/` – main js files to build index.html.
- `content/` – files in markdown format with actual content.
- `css/` – styles for blog.
- `docs` – directory with compiled static site.

## Dev environment tips

- Use `pnpm run start` to start project.
- Run `pnpm run build-ghpages` to build project.

## Commit Messages

Follow Conventional Commits:

- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation only changes
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `coauth`: Co-authored changes (e.g., "Co-authored-by: LLM <basename of LLM>")
- Example: `fix(core): format New function to pass gofumpt (coauth: Qwen3)`
