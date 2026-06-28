# RUC Survival Guide 在线书改造设计

## 背景

当前项目是一个基于 MkDocs Material 的非官方人大生存指南，内容以 Markdown 组织，覆盖学习入门、课程资料、路径选择、校园生活、资源索引和贡献说明。改造目标是把它整理成一本简洁、美观、可长期维护的 GitHub Pages 在线书，而不是迁移为新的技术栈或制作 PDF。

项目归属与目标地址：

- GitHub 账户：https://github.com/Creator-zh
- 目标仓库：https://github.com/Creator-zh/ruc-survival-guide
- 目标站点：https://creator-zh.github.io/ruc-survival-guide/

## 设计目标

1. 保留 `RUC Survival Guide` 作为项目名。
2. 使用中文主导航，让主要读者能快速理解章节含义。
3. 整体接近 GitBook/技术文档式在线书：清爽、克制、可检索、目录明确。
4. 首页暂时保持轻量，预留给作者后续撰写项目缘起文章。
5. 课程资料库不作为主线正文的一部分，而是作为醒目的资料入口保留。
6. 首版优先上线，不重写正文内容，仅调整外观、导航、配置和部署准备。

## 参考方向

- Material for MkDocs：https://squidfunk.github.io/mkdocs-material/
  - 参考点：现有技术栈、搜索、导航、浅色/深色模式、仓库入口。
- Material for MkDocs 仓库入口文档：https://squidfunk.github.io/mkdocs-material/setup/adding-a-git-repository/
  - 参考点：通过 `repo_url` 和 `repo_name` 在页眉提供 GitHub 仓库入口。
- CSDIY：https://csdiy.wiki/
  - 参考点：在线知识库式阅读体验，以及右上角可见但不打扰阅读的仓库入口。
- GitBook：https://www.gitbook.com/
  - 参考点：清爽的在线书气质、左侧目录、搜索优先的阅读方式。

## 信息架构

最终主导航使用中文标题：

- 首页：极简占位，后续承载作者关于项目缘起的文章。
- 学习指南：新生、选课、GPA 等学习入门内容。
- 路径选择：保研、出国、就业、科研、转专业等长期选择。
- 校园生活：宿舍、食堂、图书馆、校园服务。
- 资源索引：政策、链接、工具资源。
- 课程资料库 ↗：课程资料入口，视觉上作为资料库入口呈现，实际仍指向本站课程页。
- 参与贡献：投稿、版权、下架、路线图等项目维护内容。

正文文件原则上不移动，不进行大规模合并或拆分；主要通过 `mkdocs.yml` 导航重排表达新的阅读结构。

## 首页策略

首页不做封面式营销页，不放大图、章节卡片或长介绍。首版只保留少量文字和结构空间，让它成为后续项目缘起文章的位置。站点入口主要由顶部导航、左侧目录和搜索承担。

首页应避免以下内容：

- 大面积品牌视觉或校徽式设计。
- 过多说明性卡片。
- 与正文重复的章节介绍。
- 强引导按钮和营销式文案。

## 视觉风格

视觉目标是中性、简洁、适合长时间阅读。

- 主色：黑白灰为主。
- 强调色：少量深红色，用于链接、当前导航项、悬停状态和提示块。
- 品牌：不使用人大标志，不做强校园品牌化，避免被误解为官方项目。
- 模式：默认浅色，保留不抢眼的深色模式切换。
- 布局：保留 Material for MkDocs 的目录、搜索、页内标题导航和响应式布局。
- 阅读密度：正文宽度适中，减少装饰，优先保证中文长文可读性。

## 功能配置

首版功能范围：

- 使用 MkDocs Material，不迁移技术栈。
- 配置 `site_url` 为 `https://creator-zh.github.io/ruc-survival-guide/`。
- 配置 `repo_url` 为 `https://github.com/Creator-zh/ruc-survival-guide`。
- 右上角显示仓库入口，形式参考 CSDIY。
- 不显示“编辑此页”按钮。
- 每页显示 Git 最后更新日期。
- 保留中文和英文搜索。
- 保留深色模式切换。
- 评论系统首版不启用，但保留现有 `overrides/partials/comments.html` 扩展位，后续可接入 GitHub Discussions 或 Giscus。

为实现 Git 最后更新日期，预计需要引入 MkDocs 的 Git 日期相关插件，并在本地和 GitHub Actions 中保证构建时有 Git 历史可用。

## 课程资料库处理

课程相关页面继续保留在当前站点内，但从主线书籍导航中降级为“课程资料库 ↗”入口。这样读者能把它理解为资料库，而不是在线书的主线章节。

课程资料库入口应满足：

- 顶部导航可见。
- 文案明确是资料库。
- 不打断“学习指南 / 路径选择 / 校园生活”的主线阅读。
- 后续如果课程资料独立成仓库或单独站点，导航目标可以平滑替换。

## 上线流程

首版实现完成后应按以下顺序验证和上线：

1. 本地安装依赖。
2. 运行 `mkdocs build` 验证静态站点构建。
3. 配置 GitHub Actions 构建并发布到 GitHub Pages。
4. 检查本机 GitHub CLI 登录状态。
5. 如权限可用，创建公开仓库 `Creator-zh/ruc-survival-guide`。
6. 推送代码到远程仓库。
7. 等待 GitHub Actions 完成部署。
8. 验证 `https://creator-zh.github.io/ruc-survival-guide/` 可访问。

如果 GitHub CLI 未登录、网络受限或创建仓库失败，应保留本地可构建状态，并明确给出用户需要完成的下一步。

## 非目标

首版不做以下工作：

- 不迁移到 VitePress、Nextra、Docusaurus 或 GitBook。
- 不制作 PDF 或印刷版。
- 不重写正文。
- 不设计人大标志、校徽或强官方风格视觉。
- 不立即接入评论系统。
- 不把课程资料迁移到单独仓库。

## 验收标准

设计落地后应满足：

- 站点本地 `mkdocs build` 通过。
- 导航使用中文标题，结构与本设计一致。
- 首页保持极简，为后续项目缘起文章留出空间。
- 页面右上角能看到 GitHub 仓库入口。
- 页面不显示“编辑此页”按钮。
- 页面显示 Git 最后更新日期。
- 默认浅色模式，深色模式可切换。
- 课程资料库作为独立入口可访问。
- GitHub Pages 部署配置存在，目标站点地址正确。

