# RUC Survival Guide Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build an initial MkDocs Material repository for a non-official RUC student survival guide and course resource archive.

**Architecture:** The site uses `docs/` for readable guide pages and `materials/` for course resources. Course discovery has two entrances: alphabetical course-name index and school/course archive.

**Tech Stack:** MkDocs Material, GitHub Pages, GitHub Discussions + giscus, Git LFS.

---

### Task 1: Initialize Site Skeleton

**Files:**
- Create: `mkdocs.yml`
- Create: `requirements.txt`
- Create: `README.md`
- Create: `.github/workflows/deploy.yml`

- [x] Create MkDocs Material configuration with Chinese search, navigation tabs, and GitHub edit links.
- [x] Add Python requirements for `mkdocs-material` and revision date plugin.
- [x] Add GitHub Pages workflow using `mkdocs build --strict`.
- [x] Add README explaining project identity, structure, preview, deployment, and authorization model.

### Task 2: Create Content Architecture

**Files:**
- Create: `docs/index.md`
- Create: `docs/guide/*.md`
- Create: `docs/courses/**/*.md`
- Create: `docs/survival/*.md`
- Create: `docs/life/*.md`
- Create: `docs/resources/*.md`

- [x] Add homepage with project positioning and start points.
- [x] Add learning guide pages for freshmen, course selection, and GPA strategy.
- [x] Add course double entrance: alphabetical and school/course.
- [x] Add survival reference pages for baoyan, abroad, career, research, and transfer/second major.
- [x] Add lightweight campus life and resource index pages.

### Task 3: Create Maintenance Infrastructure

**Files:**
- Create: `CONTRIBUTING.md`
- Create: `CONTENT_LICENSE.md`
- Create: `TAKEDOWN.md`
- Create: `.gitattributes`
- Create: `.github/ISSUE_TEMPLATE/*.md`
- Create: `docs/contribute/*.md`

- [x] Add contribution rules for course pages, resources, and experience comments.
- [x] Add layered license statement.
- [x] Add takedown and correction process.
- [x] Add Git LFS tracking rules for large binary files.
- [x] Add issue templates for resource submissions and takedown requests.

### Task 4: Configure Course Comments

**Files:**
- Create: `overrides/partials/comments.html`
- Modify: course pages with `comments: true`

- [x] Add giscus comments partial.
- [x] Add comment disclaimer.
- [x] Enable comments on example course pages.
- [ ] After creating the GitHub repository, replace `data-repo`, `data-repo-id`, and `data-category-id`.

### Task 5: Publish First Public Version

**Files:**
- Modify: `mkdocs.yml`
- Modify: `README.md`
- Modify: `docs/resources/links.md`

- [ ] Replace placeholder GitHub URLs with the real repository URL.
- [ ] Enable GitHub Discussions and create the `课程讨论` category.
- [ ] Configure giscus and update `overrides/partials/comments.html`.
- [ ] Install Git LFS locally before adding large files.
- [ ] Push to GitHub and enable Pages from GitHub Actions.

