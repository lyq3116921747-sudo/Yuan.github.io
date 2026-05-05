---
title: Markdown 图片插入指南
date: 2026-05-06 10:00:00 +0800
categories: [教程]
tags: [Markdown, Jekyll, 图片]
description: 详细介绍在 Jekyll 博客中插入图片的各种方法。
---

本文介绍如何在 Yuan Blog 中正确插入和使用图片。

## 方法一：本地图片（推荐）

### 1. 准备图片
将图片文件放到 `img/posts/` 目录下。

### 2. 在文章中引用
```markdown
![图片描述](/img/posts/your-image.jpg)
```

### 3. 示例代码块
```markdown
![风景图片](/img/posts/screenshot-2024-05-06.png)
```

## 方法二：外部图片链接

直接使用图床或外部链接：

```markdown
![图片描述](https://example.com/image.jpg)
```

## 方法三：HTML 标签（更灵活）

使用 HTML 可以设置更多属性：

```html
<img src="/img/posts/your-image.jpg"
     alt="图片描述"
     style="width: 100%; max-width: 800px; border-radius: 8px;">
```

## 图片排版技巧

### 居中显示
```html
<div style="text-align: center;">
  <img src="/img/posts/your-image.jpg" alt="图片描述" style="max-width: 100%;">
  <p style="color: #888; font-size: 0.9em;">图片标题</p>
</div>
```

### 并排显示
```html
<div style="display: flex; gap: 16px;">
  <img src="/img/posts/image1.jpg" alt="图片1" style="flex: 1;">
  <img src="/img/posts/image2.jpg" alt="图片2" style="flex: 1;">
</div>
```

## 图片优化建议

1. **压缩图片**：使用 TinyPNG 等工具压缩
2. **合适尺寸**：最大宽度 1200px 即可
3. **格式选择**：
   - 照片：JPG
   - 截图/图表：PNG
   - 现代浏览器：WebP

## 注意事项

- 路径必须以 `/` 开头（绝对路径）
- 图片文件名避免中文和特殊字符
- 使用有意义的 alt 文本便于 SEO
- 定期检查图片链接是否有效

## 总结

推荐使用 **方法一**：将图片放到 `img/posts/` 目录，然后使用 `/img/posts/` 路径引用。这样稳定可靠，加载速度快。
