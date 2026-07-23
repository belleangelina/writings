# writings

公开写作内容仓库，用于存放会发布到个人 GitHub Pages 网站的长篇、短篇、笔记和相关资源。

站点仓库：`belleangelina/belleangelina.github.io`  
发布地址：`https://belleangelina.github.io/`

本仓库只负责内容；网站构建、页面样式、路由和部署逻辑放在站点仓库中。

## 内容类型

V1 支持三类内容：

- `novels/`：长篇小说，按“作品 → 卷 → 章”组织。
- `shorts/`：短篇小说或独立短文。
- `notes/`：笔记，例如开发调试经验、部署记录、写作记录等。

V1 只支持 Markdown `.md`，暂不支持 MDX，也暂不使用 tags。

## 目录结构

```text
writings/
├─ README.md
├─ novels/
│  └─ <novel-slug>/
│     ├─ index.md                 # 长篇作品首页 / 元信息
│     ├─ cover.jpg                # 可选：作品封面
│     └─ <volume-slug>/
│        ├─ index.md              # 卷首页 / 卷元信息
│        ├─ <chapter-slug>.md     # 章节正文
│        └─ <chapter-slug>/       # 可选：该章相关资源
│           └─ images/
├─ shorts/
│  ├─ <short-slug>.md             # 短篇正文
│  └─ <short-slug>/               # 可选：短篇资源目录
│     ├─ cover.jpg
│     └─ images/
└─ notes/
   ├─ <note-slug>.md              # 笔记正文
   └─ <note-slug>/                # 可选：笔记资源目录
      └─ images/
```

## Slug 命名规则

slug 来自目录名或文件名，用于生成网页 URL。

建议规则：

- 使用英文小写。
- 单词之间使用短横线 `-`。
- 不使用空格。
- 尽量保持短而稳定。

示例：

```text
night-voyage
summer-rain
github-pages-debug
```

V1 不需要在 frontmatter 中额外写 `slug` 字段。

## 发布状态

所有会被网站读取的 Markdown 文件都需要写 `status` 字段。

```yaml
status: published  # 正式发布，会出现在网站
status: draft      # 草稿，不会出现在网站
```

V1 只支持 `published` 和 `draft`。

## 通用 frontmatter

```yaml
title: 标题
status: published
summary: 简介，可选
date: 2026-07-04
cover: ./relative/path/to/cover.jpg
```

字段说明：

- `title`：必填，页面标题。
- `status`：必填，`published` 或 `draft`。
- `summary`：可选，用于列表页、RSS 等摘要展示。
- `date`：推荐填写，用于列表排序和 RSS 时间。
- `cover`：可选，封面图路径，使用相对当前 Markdown 文件的路径。

## 长篇小说

长篇小说按“作品 → 卷 → 章”组织。

作品首页：

```text
novels/<novel-slug>/index.md
```

```yaml
title: 夜航
status: published
summary: 作品简介。
date: 2026-07-04
cover: ./cover.jpg
```

卷首页：

```text
novels/<novel-slug>/<volume-slug>/index.md
```

```yaml
title: 第一卷 海上的灯
status: published
volume: 1
summary: 第一卷简介。
```

章节正文：

```text
novels/<novel-slug>/<volume-slug>/<chapter-slug>.md
```

```yaml
title: 第一章 夜航
status: published
chapter: 1
date: 2026-07-04
summary: 第一章简介。
```

说明：

- 卷按 `volume` 从小到大排序。
- 章按 `chapter` 从小到大排序。
- 章节不需要写 `volume` 字段，所属卷由目录决定。

## 短篇

短篇使用单个 `.md` 文件。

```text
shorts/<short-slug>.md
```

```yaml
title: 夏雨
status: published
date: 2026-07-04
summary: 一个发生在雨天的故事。
cover: ./summer-rain/cover.jpg
```

如需封面或插图，放在同名资源目录：

```text
shorts/<short-slug>/
├─ cover.jpg
└─ images/
```

## 笔记

笔记使用单个 `.md` 文件。

```text
notes/<note-slug>.md
```

```yaml
title: GitHub Pages 部署踩坑
status: published
date: 2026-07-04
summary: 记录一次 GitHub Pages 部署失败的排查过程。
```

如需插图，放在同名资源目录：

```text
notes/<note-slug>/
└─ images/
```

## 图片和资源

规则：

- 图片尽量就近存放。
- 封面图通过 frontmatter 的 `cover` 字段指定。
- 正文插图使用 Markdown 图片语法。
- 图片路径使用相对当前 Markdown 文件的相对路径。

示例：

```md
---
title: 夏雨
status: published
cover: ./summer-rain/cover.jpg
---

![雨中的街道](./summer-rain/images/street.jpg)
```

## 排序规则

网站构建时采用以下默认排序：

- 文章总览、短篇、笔记：按 `date` 倒序，新内容在前。
- 长篇列表：按作品 `date` 倒序。
- 长篇内部：卷按 `volume` 升序，章按 `chapter` 升序。

## 自动发布

push 到 `main` 分支后，网站会自动重新构建并发布。站点仓库也保留手动触发入口，便于调试或重新部署。

## 注意事项

- V1 只支持 Markdown `.md`。
- V1 暂不支持 MDX `.mdx`。
- V1 暂不使用 tags。
- 草稿内容请设置 `status: draft`。
- 已发布内容请设置 `status: published`。
- 修改已经发布过的 slug 会改变文章 URL，应尽量避免。

© 2026 Manbo. All rights reserved.
