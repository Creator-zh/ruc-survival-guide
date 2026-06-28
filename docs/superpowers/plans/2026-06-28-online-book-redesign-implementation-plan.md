# Online Book Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Turn the existing MkDocs Material site into a clean GitBook-like online book for `RUC Survival Guide`, ready for GitHub Pages deployment under `Creator-zh/ruc-survival-guide`.

**Architecture:** Keep the existing Markdown content and MkDocs Material stack. Implement the redesign through focused changes to `mkdocs.yml`, a small stylesheet, the homepage, dependency list, and the existing GitHub Pages workflow.

**Tech Stack:** MkDocs, MkDocs Material, `mkdocs-git-revision-date-localized-plugin`, GitHub Actions, GitHub Pages.

---

## File Structure

- Modify `mkdocs.yml`: update site metadata, repository link, theme features, palette, plugins, extra CSS, edit/view actions, and Chinese navigation.
- Modify `requirements.txt`: add the Git revision date plugin used by MkDocs to display per-page update dates.
- Modify `docs/index.md`: make the homepage minimal and leave room for the future project-origin article.
- Create `docs/assets/stylesheets/book.css`: add restrained online-book styling and neutral color accents.
- Modify `.github/workflows/deploy.yml`: ensure Git history is available for the date plugin and GitHub Pages deployment still builds strictly.
- Optionally modify `.gitignore`: ignore local brainstorming artifacts if they are still present.
- Do not modify `overrides/partials/comments.html` in this pass; comments remain present but inactive unless page metadata enables them.

## Task 1: Prepare Dependencies for Page Update Dates

**Files:**
- Modify: `requirements.txt`

- [ ] **Step 1: Add the Git revision date plugin dependency**

Replace `requirements.txt` with:

```text
mkdocs-material>=9.5
mkdocs-git-revision-date-localized-plugin>=1.2
```

- [ ] **Step 2: Verify dependency file content**

Run:

```powershell
Get-Content -LiteralPath requirements.txt -Encoding UTF8
```

Expected output includes both lines:

```text
mkdocs-material>=9.5
mkdocs-git-revision-date-localized-plugin>=1.2
```

- [ ] **Step 3: Commit dependency update**

Run:

```powershell
git add -- requirements.txt
git commit -m "build: add page revision date plugin"
```

Expected: a commit is created containing only `requirements.txt`.

## Task 2: Reconfigure MkDocs as an Online Book

**Files:**
- Modify: `mkdocs.yml`

- [ ] **Step 1: Replace site metadata, theme settings, plugins, and navigation**

Rewrite `mkdocs.yml` to this content:

```yaml
site_name: RUC Survival Guide
site_description: 非官方、学生维护的中国人民大学学习与生存指南
site_url: https://creator-zh.github.io/ruc-survival-guide/
repo_name: Creator-zh/ruc-survival-guide
repo_url: https://github.com/Creator-zh/ruc-survival-guide
edit_uri: ""

theme:
  name: material
  language: zh
  custom_dir: overrides
  features:
    - navigation.tabs
    - navigation.sections
    - navigation.indexes
    - navigation.top
    - navigation.footer
    - navigation.tracking
    - search.suggest
    - search.highlight
    - content.tabs.link
  palette:
    - scheme: default
      primary: white
      accent: red
      toggle:
        icon: material/weather-night
        name: 切换到深色模式
    - scheme: slate
      primary: black
      accent: red
      toggle:
        icon: material/weather-sunny
        name: 切换到浅色模式

plugins:
  - search:
      lang:
        - zh
        - en
  - git-revision-date-localized:
      enable_creation_date: false
      type: date
      timezone: Asia/Shanghai
      locale: zh
      fallback_to_build_date: true

extra_css:
  - assets/stylesheets/book.css

markdown_extensions:
  - admonition
  - attr_list
  - def_list
  - footnotes
  - md_in_html
  - tables
  - toc:
      permalink: true
  - pymdownx.details
  - pymdownx.superfences
  - pymdownx.tasklist:
      custom_checkbox: true
  - pymdownx.tabbed:
      alternate_style: true

extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/Creator-zh/ruc-survival-guide
      name: GitHub

nav:
  - 首页: index.md
  - 学习指南:
      - guide/index.md
      - 新生入门: guide/freshman.md
      - 选课指南: guide/course-selection.md
      - GPA 与成绩: guide/gpa.md
  - 路径选择:
      - survival/index.md
      - 保研: survival/baoyan.md
      - 出国: survival/abroad.md
      - 就业: survival/career.md
      - 科研: survival/research.md
      - 转专业与辅修: survival/transfer-major.md
  - 校园生活:
      - life/index.md
      - 校园服务: life/campus-services.md
      - 宿舍: life/dorm.md
      - 食堂: life/canteen.md
      - 图书馆: life/library.md
  - 资源索引:
      - resources/index.md
      - 政策索引: resources/policies.md
      - 常用链接: resources/links.md
  - 课程资料库 ↗:
      - courses/index.md
      - 按首字母:
          - courses/alphabetical/index.md
          - A: courses/alphabetical/a.md
          - B: courses/alphabetical/b.md
          - C: courses/alphabetical/c.md
          - D: courses/alphabetical/d.md
          - E: courses/alphabetical/e.md
          - F: courses/alphabetical/f.md
          - G: courses/alphabetical/g.md
          - H: courses/alphabetical/h.md
          - I: courses/alphabetical/i.md
          - J: courses/alphabetical/j.md
          - K: courses/alphabetical/k.md
          - L: courses/alphabetical/l.md
          - M: courses/alphabetical/m.md
          - N: courses/alphabetical/n.md
          - O: courses/alphabetical/o.md
          - P: courses/alphabetical/p.md
          - Q: courses/alphabetical/q.md
          - R: courses/alphabetical/r.md
          - S: courses/alphabetical/s.md
          - T: courses/alphabetical/t.md
          - W: courses/alphabetical/w.md
          - X: courses/alphabetical/x.md
          - Y: courses/alphabetical/y.md
          - Z: courses/alphabetical/z.md
      - 按学院:
          - courses/schools/index.md
          - 信息学院:
              - 程序设计基础: courses/schools/信息学院/程序设计基础.md
          - 财政金融学院:
              - 金融学: courses/schools/财政金融学院/金融学.md
          - 高瓴人工智能学院:
              - 机器学习: courses/schools/高瓴人工智能学院/机器学习.md
      - 模板:
          - 课程页面模板: courses/templates/course-page.md
  - 参与贡献:
      - contribute/index.md
      - 课程资料模板: contribute/course-template.md
      - 资源模板: contribute/resource-template.md
      - 评论规则: contribute/comments.md
      - 授权说明: contribute/license.md
      - 下架请求: contribute/takedown.md
      - 路线图: contribute/roadmap.md
```

- [ ] **Step 2: Verify removed edit/view actions**

Run:

```powershell
rg -n "content.action.edit|content.action.view|edit_uri: edit" mkdocs.yml
```

Expected: no matches. This confirms that page-level edit/view buttons are not configured.

- [ ] **Step 3: Verify Chinese navigation and target URLs**

Run:

```powershell
rg -n "site_url|repo_url|学习指南|路径选择|校园生活|资源索引|课程资料库|参与贡献" mkdocs.yml
```

Expected: matches for the production site URL, the `Creator-zh` repository URL, and all Chinese top-level navigation labels.

- [ ] **Step 4: Commit MkDocs configuration**

Run:

```powershell
git add -- mkdocs.yml
git commit -m "config: reshape mkdocs navigation for online book"
```

Expected: a commit is created containing only `mkdocs.yml`.

## Task 3: Add Minimal Online Book Styling

**Files:**
- Create: `docs/assets/stylesheets/book.css`

- [ ] **Step 1: Create the stylesheet**

Create `docs/assets/stylesheets/book.css` with:

```css
:root {
  --ruc-book-accent: #9f1d2f;
}

[data-md-color-scheme="default"] {
  --md-primary-fg-color: #ffffff;
  --md-primary-bg-color: #1f2328;
  --md-accent-fg-color: var(--ruc-book-accent);
  --md-typeset-a-color: var(--ruc-book-accent);
}

[data-md-color-scheme="slate"] {
  --md-accent-fg-color: #ff8a9a;
  --md-typeset-a-color: #ff8a9a;
}

.md-header {
  border-bottom: 1px solid var(--md-default-fg-color--lightest);
  box-shadow: none;
}

.md-tabs {
  border-bottom: 1px solid var(--md-default-fg-color--lightest);
}

.md-typeset {
  font-size: 0.78rem;
  line-height: 1.8;
}

.md-typeset h1 {
  font-weight: 650;
  letter-spacing: 0;
}

.md-typeset h2 {
  border-top: 1px solid var(--md-default-fg-color--lightest);
  padding-top: 1.6rem;
}

.md-typeset a {
  text-decoration-thickness: 0.06em;
  text-underline-offset: 0.18em;
}

.md-typeset blockquote {
  border-left-color: var(--ruc-book-accent);
}

.md-nav__link--active,
.md-nav__link:focus,
.md-nav__link:hover {
  color: var(--md-accent-fg-color);
}

.md-source {
  font-weight: 500;
}

.md-footer-meta {
  background-color: var(--md-default-bg-color);
}
```

- [ ] **Step 2: Verify stylesheet is referenced**

Run:

```powershell
rg -n "assets/stylesheets/book.css" mkdocs.yml
```

Expected: one match under `extra_css`.

- [ ] **Step 3: Verify stylesheet avoids official branding**

Run:

```powershell
rg -n "logo|seal|emblem|校徽|人大标志|Renmin University logo" docs\\assets\\stylesheets\\book.css
```

Expected: no matches.

- [ ] **Step 4: Commit styling**

Run:

```powershell
git add -- docs/assets/stylesheets/book.css
git commit -m "style: add restrained online book theme"
```

Expected: a commit is created containing only `docs/assets/stylesheets/book.css`.

## Task 4: Simplify the Homepage

**Files:**
- Modify: `docs/index.md`

- [ ] **Step 1: Replace homepage content**

Replace `docs/index.md` with:

```markdown
# 人大学生生存指南

这是一份非官方、学生维护的中国人民大学学习与生活参考。

我会在这里写一篇文章，说明为什么要做这个项目。
```

- [ ] **Step 2: Verify homepage stays minimal**

Run:

```powershell
(Get-Content -LiteralPath docs\\index.md -Encoding UTF8 | Measure-Object -Line).Lines
```

Expected: `5` or fewer lines.

- [ ] **Step 3: Commit homepage update**

Run:

```powershell
git add -- docs/index.md
git commit -m "docs: simplify homepage for project origin essay"
```

Expected: a commit is created containing only `docs/index.md`.

## Task 5: Make GitHub Pages Workflow Compatible with Git Dates

**Files:**
- Modify: `.github/workflows/deploy.yml`

- [ ] **Step 1: Update checkout history and Python version**

Replace `.github/workflows/deploy.yml` with:

```yaml
name: Deploy MkDocs site

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: actions/setup-python@v5
        with:
          python-version: "3.x"
      - run: pip install -r requirements.txt
      - run: mkdocs build --strict
      - uses: actions/upload-pages-artifact@v3
        with:
          path: site

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```

- [ ] **Step 2: Verify full Git history checkout**

Run:

```powershell
rg -n "fetch-depth: 0|mkdocs build --strict|actions/deploy-pages@v4" .github\\workflows\\deploy.yml
```

Expected: matches for all three strings.

- [ ] **Step 3: Commit workflow update**

Run:

```powershell
git add -- .github/workflows/deploy.yml
git commit -m "ci: preserve git history for page dates"
```

Expected: a commit is created containing only `.github/workflows/deploy.yml`.

## Task 6: Ignore Local Brainstorming Artifacts

**Files:**
- Modify: `.gitignore`

- [ ] **Step 1: Add local artifact ignores**

Append these lines to `.gitignore` if they are not already present:

```gitignore
.superpowers/
%SystemDrive%/
```

- [ ] **Step 2: Verify ignore entries**

Run:

```powershell
rg -n "^\\.superpowers/|^%SystemDrive%/" .gitignore
```

Expected: matches for both ignore entries.

- [ ] **Step 3: Confirm the artifacts are not tracked**

Run:

```powershell
git status --short
```

Expected: `.superpowers/` and `%SystemDrive%/` do not appear in the untracked file list.

- [ ] **Step 4: Commit ignore update**

Run:

```powershell
git add -- .gitignore
git commit -m "chore: ignore local brainstorming artifacts"
```

Expected: a commit is created containing only `.gitignore`.

## Task 7: Build and Inspect the Static Site

**Files:**
- No source edits expected.

- [ ] **Step 1: Install dependencies if needed**

Run:

```powershell
pip install -r requirements.txt
```

Expected: `mkdocs-material` and `mkdocs-git-revision-date-localized-plugin` install successfully. If this fails with a network or sandbox error, rerun with escalated permissions.

- [ ] **Step 2: Build strictly**

Run:

```powershell
mkdocs build --strict
```

Expected: build completes with no warnings or errors.

- [ ] **Step 3: Verify repository link appears in built HTML**

Run:

```powershell
rg -n "https://github.com/Creator-zh/ruc-survival-guide|Creator-zh/ruc-survival-guide" site
```

Expected: matches in generated HTML.

- [ ] **Step 4: Verify homepage content is minimal in built HTML**

Run:

```powershell
rg -n "为什么要做这个项目|非官方、学生维护" site\\index.html
```

Expected: matches for both strings.

- [ ] **Step 5: Verify edit buttons are absent**

Run:

```powershell
rg -n "Edit this page|编辑此页|content.action.edit" site
```

Expected: no matches.

- [ ] **Step 6: Commit no files**

Run:

```powershell
git status --short
```

Expected: no new tracked source changes from the build. The `site/` directory remains ignored.

## Task 8: Prepare and Publish to GitHub

**Files:**
- No source edits expected.

- [ ] **Step 1: Check GitHub CLI authentication**

Run:

```powershell
gh auth status
```

Expected: authenticated as the `Creator-zh` GitHub account. If not authenticated, stop and ask the user to log in with `gh auth login`.

- [ ] **Step 2: Check whether the target repository already exists**

Run:

```powershell
gh repo view Creator-zh/ruc-survival-guide
```

Expected: either repository details appear, or GitHub reports it does not exist.

- [ ] **Step 3: Create the public repository if it does not exist**

Run:

```powershell
gh repo create Creator-zh/ruc-survival-guide --public --source . --remote origin --description "非官方、学生维护的中国人民大学学习与生存指南"
```

Expected: GitHub creates the public repository and configures `origin`. If `origin` already exists, inspect it with `git remote -v` and update only if it does not point to `https://github.com/Creator-zh/ruc-survival-guide.git`.

- [ ] **Step 4: Push main**

Run:

```powershell
git push -u origin main
```

Expected: local `main` is pushed to `origin/main`.

- [ ] **Step 5: Verify the GitHub Actions workflow starts**

Run:

```powershell
gh run list --repo Creator-zh/ruc-survival-guide --limit 5
```

Expected: a recent `Deploy MkDocs site` run is listed.

- [ ] **Step 6: Watch the latest deployment run**

Run:

```powershell
gh run watch --repo Creator-zh/ruc-survival-guide
```

Expected: workflow completes successfully.

- [ ] **Step 7: Report final URLs**

Report these URLs to the user:

```text
Repository: https://github.com/Creator-zh/ruc-survival-guide
Site: https://creator-zh.github.io/ruc-survival-guide/
```

## Self-Review

Spec coverage:

- Online book structure is covered by Task 2.
- Chinese navigation is covered by Task 2.
- Minimal homepage is covered by Task 4.
- Neutral GitBook-like styling is covered by Task 3.
- Repository link in the header is covered by Task 2 and verified by Task 7.
- No edit button is covered by Task 2 and verified by Task 7.
- Per-page Git update dates are covered by Tasks 1, 2, and 5.
- GitHub Pages deployment is covered by Tasks 5 and 8.
- Comments remain inactive by default because no task enables `page.meta.comments` or edits the giscus partial.

Placeholder scan:

- The plan uses exact file paths, exact config blocks, exact commands, and expected outputs.
- The plan contains no placeholder markers or unspecified implementation steps.

Type and naming consistency:

- The repository name is consistently `Creator-zh/ruc-survival-guide`.
- The site URL is consistently `https://creator-zh.github.io/ruc-survival-guide/`.
- The stylesheet path is consistently `docs/assets/stylesheets/book.css` and `assets/stylesheets/book.css` in MkDocs config.

