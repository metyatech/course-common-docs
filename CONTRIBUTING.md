# Contributing

Thank you for your interest in contributing to `course-common-docs`.

## Development setup

```bash
git clone https://github.com/metyatech/course-common-docs.git
cd course-common-docs
git submodule update --init --recursive
```

## Local preview

1. Clone `metyatech/course-docs-site`.
2. Run `npm install` in that repo.
3. Create `course-docs-site/.env.course.local` with `COURSE_CONTENT_SOURCE` set to this repository.
4. Start the dev server with `npm run dev`.

Use any local path that is valid from the `course-docs-site` checkout. If the two repositories are siblings, `../course-common-docs` works.

## Verification

Run the full verification suite before each commit:

- `node scripts/verify.mjs`

If `course-docs-site` is not in the same workspace, set `COURSE_DOCS_SITE_DIR` to that checkout before running the verify script.

## Submitting changes

1. Fork the repository and create a feature branch.
2. Open a pull request with a clear description of the change.

## Scope

This repository is **content-only** and contains shared course information (受講ルール, 成績評価, etc.) consumed by multiple course sites. Please keep PRs scoped to course content (MDX pages, metadata). Runtime/site changes belong in the shared `course-docs-site` or `course-docs-platform` repositories.
