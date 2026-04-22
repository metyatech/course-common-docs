# course-common-docs

Shared course information content repository for metyatech course sites.

This repo is **content-only** (not a Next.js app). The shared site runtime lives in `metyatech/course-docs-site`.

## Overview

This repository contains lesson-independent, course-common documentation:

- **はじめに** — Landing page linking to the key sections
- **受講ルール** — Attendance, quiz participation, and self-study guidance
- **生成AIの利用** — Classroom and exam guidance for acceptable AI use
- **成績評価** — Grade composition and exam policy

It follows the same content-repo contract used by `javascript-course-docs` and `programming-course-docs` so that `course-docs-site` can consume it via `COURSE_CONTENT_SOURCE`.

## Setup after cloning

```bash
git clone https://github.com/metyatech/course-common-docs.git
cd course-common-docs

# Initialize the agent-rules-private submodule
git submodule update --init --recursive

# Install compose-agentsmd if not already installed
npm install -g compose-agentsmd

# Regenerate AGENTS.md from the ruleset
compose-agentsmd

# Enable the pre-commit hook
git config core.hooksPath .githooks
```

## Verify

Run the canonical verification command from this repository:

```sh
node scripts/verify.mjs
```

What it does:

- runs `markdownlint` for this repository
- locates a local `course-docs-site` checkout automatically when the repos live in the same workspace
- runs `course-docs-site` lint and `build:verified` with `COURSE_CONTENT_SOURCE` set to this repository

If `course-docs-site` is not in the same workspace, set `COURSE_DOCS_SITE_DIR` in your shell or terminal session to that checkout before running `node scripts/verify.mjs`.

Automatic discovery looks for a local checkout named `course-docs-site` while walking up parent directories from this repository.

## Local preview

```sh
git clone https://github.com/metyatech/course-docs-site.git
cd course-docs-site
npm install
```

Then point `course-docs-site` at this repository through `.env.course.local`:

```sh
# In course-docs-site/.env.course.local
COURSE_CONTENT_SOURCE=../path-to-course-common-docs
```

Use any local path that is valid from the `course-docs-site` checkout. If the two repositories are siblings, that can be `../course-common-docs`.

## Deploy (Vercel)

Deployment is done via GitHub Actions using the Vercel CLI.
See `.github/workflows/deploy-vercel.yml`.
The workflow checks out `metyatech/course-docs-site`, points `COURSE_CONTENT_SOURCE` at this repository, and deploys the resulting build.

Required GitHub Actions secrets:

- `VERCEL_TOKEN` (a Vercel access token with access to the target project/team)
- `VERCEL_ORG_ID`
- `VERCEL_PROJECT_ID`

## Repository structure

````text
content/
  _meta.ts                        # Top-level navigation
  docs/
    _meta.ts                      # Docs section ordering
    intro/
      index.mdx                   # はじめに page (landing / index)
    course-rules/
      index.mdx                   # 受講ルール page
    ai-usage/
      index.mdx                   # 生成AIの利用 page
    grading/
      index.mdx                   # 成績評価 page
public/
  img/
    favicon.ico                   # Site favicon
site.config.ts                    # Site metadata consumed by course-docs-site
```

## Project files

- `content/` — course pages (MDX)
- `scripts/verify.mjs` — canonical verification entrypoint for local delivery checks
- `public/` — static files (e.g. `public/img/**`)
- `site.config.ts` — per-course site configuration consumed by `course-docs-site`

## Agent rules

This repo includes `agent-rules-private` as a git submodule. Initialize it after cloning:

```bash
git submodule update --init --recursive
```

Regenerate `AGENTS.md` after editing `agent-ruleset.json`:

```bash
compose-agentsmd
```

## Content contract

- `content/` — MDX page content
- `content/**/_meta.ts` — Nextra sidebar ordering
- `public/img/` — Static assets (favicon, images)
- `site.config.ts` — Site metadata (`logoText`, `description`, `projectLink`, `faviconHref`)

Do not add Next.js app runtime files (`next.config.js`, `src/app/`, `package.json`) to this repository.
````
