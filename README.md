# Yuan Blog

这是一个基于 Jekyll 的个人技术博客，部署在 GitHub Pages。

Live site:
https://lyq3116921747-sudo.github.io/Yuan.github.io/

## 写文章

在 `_posts` 目录中新建 Markdown 文件，文件名格式为：

```text
YYYY-MM-DD-title.md
```

文章开头需要包含 front matter：

```yaml
---
title: 文章标题
date: 2026-05-05 12:00:00 +0800
categories: [技术]
tags: [Jekyll, Blog]
description: 一句话概括这篇文章。
---
```

提交到 `main` 分支后，GitHub Pages workflow 会自动构建并发布。

## 本地预览

如果本机已安装 Ruby 和 Bundler：

```powershell
bundle install
bundle exec jekyll serve
```

站点默认使用 `img/background1.webp` 作为全屏背景图，请不要重复复制这个大文件。
