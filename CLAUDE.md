# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

@AGENTS.md

## Commands

```bash
npm run dev      # Start dev server (Turbopack, default)
npm run build    # Production build
npm run start    # Start production server
npm run lint     # Run ESLint (note: build no longer runs lint automatically)
```

To use Webpack instead of Turbopack: `next dev --webpack` or `next build --webpack`.

## Architecture

This is a **Next.js 16** app using the **App Router** (`app/` directory), React 19, TypeScript, and Tailwind CSS v4.

- `app/layout.tsx` — root layout with Geist fonts and global CSS
- `app/page.tsx` — home page (currently the default scaffold)
- `app/globals.css` — global styles (Tailwind CSS v4 via PostCSS)
- `eslint.config.mjs` — flat ESLint config (ESLint v9 format)

## Key Next.js 16 Differences

- **Turbopack** is the default bundler (not Webpack)
- **`next build` does not run the linter** — run `npm run lint` separately
- **`cookies()` is async** — must `await cookies()` before use
- **`refresh()`** from `next/cache` refreshes the current page; use `revalidatePath`/`revalidateTag` for cache invalidation
- **Server Functions** use the `'use server'` directive; they are reachable via direct POST requests — always verify auth inside them
- **Linting**: use `eslint` CLI directly, not `next lint`

Before writing code for any feature, read the relevant guide in `node_modules/next/dist/docs/`.

## Git Workflow

After completing any meaningful unit of work, commit and push to GitHub immediately:

```bash
git add <files>
git commit -m "concise description of what changed and why"
git push
```

- Commit after each feature, fix, or logical change — never accumulate large batches of unrelated changes
- Write commit messages in the imperative mood (e.g. "add feedback form component", not "added" or "adding")
- Always push after committing so the remote is never behind local
- The remote is `origin/main` at `https://github.com/acee-at-the-squad/client-feedback-form`
