# Contributing

Thank you for your interest in contributing to `course-common-docs`.

## Development setup

```bash
git clone https://github.com/metyatech/course-common-docs.git
cd course-common-docs
git submodule update --init --recursive
```

## Submitting changes

1. Fork the repository and create a feature branch.
2. Open a pull request with a clear description of the change.

## Scope

This repository is **content-only** and contains shared course information (受講ルール, 成績評価, etc.) consumed by multiple course sites. Please keep PRs scoped to course content (MDX pages, metadata). Runtime/site changes belong in the shared `course-docs-site` or `course-docs-platform` repositories.
