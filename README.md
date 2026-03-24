# course-common-docs

Shared course information content repository for metyatech course sites.

This repo is **content-only** (not a Next.js app). The shared site runtime lives in `metyatech/course-docs-site`.

## Overview

This repository contains lesson-independent, course-common documentation:

- **はじめに** — Landing page linking to the two key sections
- **受講ルール** — Attendance, quiz participation, and self-study guidance
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

```bash
# Requires markdownlint installed globally: npm install -g markdownlint-cli
markdownlint "**/*.md" --ignore node_modules --ignore AGENTS.md --ignore agent-rules-private/**
```

Integration check against the shared site runtime:

```sh
cd ../course-docs-site
COURSE_CONTENT_SOURCE=../course-common-docs npm run build
```

## Local preview

Use `course-docs-site` and point it at this content repo:

```sh
# In course-docs-site/.env.course.local
COURSE_CONTENT_SOURCE=../course-common-docs
```

Then run:

```sh
cd course-docs-site
npm run dev
```

## Deploy (Vercel)

Deployment is done via GitHub Actions using the Vercel CLI.
See `.github/workflows/deploy-vercel.yml`.
The workflow checks out `metyatech/course-docs-site`, points `COURSE_CONTENT_SOURCE` at this repository, and deploys the resulting build.

Required GitHub Actions secrets:

- `VERCEL_TOKEN`
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
    grading/
      index.mdx                   # 成績評価 page
public/
  img/
    favicon.ico                   # Site favicon
site.config.ts                    # Site metadata consumed by course-docs-site
```

## Project files

- `content/` — course pages (MDX)
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
