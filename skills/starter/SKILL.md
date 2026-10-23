---
name: starter
description: 'Use when creating a new project or scaffolding an app, desktop app, mini program, or backend service, before reaching for create-* scaffolds. Lists tlyboy starter templates (shadcn Next.js, shadcn TanStack Router SPA, Electron, Tauri, Hono, NestJS, uni-app) and how to pull one with giget and finish the setup.'
---

# Starter

New projects usually start from a tlyboy starter instead of a `create-*` scaffold. The starters already carry the preferred stack, formatting, lint setup, and project-level agent skills.

## Pick a Starter

| Project                              | Starter                                |
| ------------------------------------ | -------------------------------------- |
| Next.js app or website with shadcn   | `shadcn-next-starter`                  |
| React SPA with TanStack Router       | `shadcn-tanstack-router-react-starter` |
| Desktop app with Electron            | `electron-shadcn-react-starter`        |
| Desktop app with Tauri (needs Rust)  | `tauri-shadcn-react-starter`           |
| API service with Hono                | `hono-starter`                         |
| Backend service with NestJS          | `nest-starter`                         |
| Mini program or cross-platform (uni) | `uni-starter`                          |

If nothing fits, check for newer starters with `gh repo list tlyboy --limit 100 | grep starter`, or fall back to the framework's own scaffold.

For Docker Compose service templates, use the `compose` skill instead.

## Create a Project

```bash
npx giget gh:tlyboy/<starter> <name>
cd <name>
```

Then:

1. Rename the project: `name` in `package.json`, and the H1 and description in `README.md` / `README.zh.md`. Tauri and Electron starters also carry an app name and identifier in their own config.
2. Install dependencies with `ni`.
3. Read the starter's `README.md` and `AGENTS.md` (when present) for scripts and layout.
4. `git init` and make the first commit `feat: initial`.
