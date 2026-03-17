# course-common-docs

Shared course information content repository for metyatech course sites.

## Overview

This repository contains lesson-independent, course-common documentation:

- **受講ルール** — Attendance, quiz participation, and self-study guidance
- **成績評価** — Grade composition and exam policy

It follows the same content-repo contract used by `javascript-course-docs` and `programming-course-docs` so that `course-docs-site` can consume it via `COURSE_CONTENT_SOURCE`.

## Repository structure

```
content/
  _meta.ts                        # Top-level navigation
  docs/
    _meta.ts                      # Docs section ordering
    course-rules/
      index.mdx                   # 受講ルール page
    grading/
      index.mdx                   # 成績評価 page
public/
  img/
    favicon.ico                   # Site favicon
site.config.ts                    # Site metadata consumed by course-docs-site
```

## Local preview

This is a content-only repository with no build tooling. Preview via `course-docs-site`:

```sh
# In course-docs-site/.env.course.local
COURSE_CONTENT_SOURCE=../course-common-docs
```

Then run:

```sh
cd course-docs-site
npm run dev
```

## Content contract

- `content/` — MDX page content
- `content/**/_meta.ts` — Nextra sidebar ordering
- `public/img/` — Static assets (favicon, images)
- `site.config.ts` — Site metadata (`logoText`, `description`, `projectLink`, `faviconHref`)

Do not add Next.js app runtime files (`next.config.js`, `src/app/`, `package.json`) to this repository.
