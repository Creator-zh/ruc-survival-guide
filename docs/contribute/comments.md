# 评论与课程体验

课程页面可以开启 GitHub Discussions + giscus 评论区。

## 评论原则

- 使用 GitHub 账号署名。
- 可以写具体任课教师、课程体验、给分感受、点名、作业压力和考试风格。
- 请标注学期、任课教师和个人背景，例如专业、年级、是否跨专业。
- 不发布人身攻击、隐私信息、未经核实的严重指控。

## 推荐格式

```text
2025 秋，A 老师，本专业大二：
作业约每两周一次，期末闭卷，课堂节奏较快。
个人建议提前复习课后题，往年题参考价值较高。
```

## giscus 配置

1. 在 GitHub 仓库开启 Discussions。
2. 创建“课程讨论”分类。
3. 到 https://giscus.app/zh-CN 生成配置。
4. 替换 `overrides/partials/comments.html` 中的 `data-repo-id` 和 `data-category-id`。
5. 在需要评论的课程页 front matter 中设置 `comments: true`。

