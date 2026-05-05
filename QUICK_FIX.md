# 🚨 图片显示问题 - 紧急修复指南

## 问题诊断

你的博客图片无法显示的原因：**使用了错误的图片路径语法**

### 当前配置
```yaml
baseurl: "/Yuan.github.io"  # ← 这是问题根源
```

### 错误的路径写法
```markdown
![图片](/img/posts/image.png)  # ❌ 在 GitHub Pages 上失效
```

### 正确的路径写法
```markdown
![图片]({{ '/img/posts/image.png' | relative_url }})  # ✅
```

---

## 🔧 立即修复现有文章

### 需要修改的文件
1. `_posts/2026-05-05-welcome-to-yuan-blog.md` ← ✅ 已修复
2. 其他包含图片的文章

### 修复步骤

#### 方法一：手动修复（推荐）
在文章编辑器中：
1. **查找：** `](/img/posts/`
2. **替换为：** `]({{ '/img/posts/`

然后在每个图片路径的末尾添加 ` | relative_url }})`

**示例：**
```markdown
# 修改前
![图片](/img/posts/2026-05-05/image.png)

# 修改后
![图片]({{ '/img/posts/2026-05-05/image.png' | relative_url }})
```

#### 方法二：批量替换
使用 VSCode 或其他编辑器的批量替换功能：

1. **查找：** `](/img/posts/`
2. **替换为：** `]({{ '/img/posts/`
3. 然后手动在每个图片路径后添加 ` | relative_url }})`

---

## ✅ 验证修复

### 1. 本地测试
```bash
bundle exec jekyll serve
# 访问 http://localhost:4000
```

### 2. 检查生成的 HTML
查看生成的 HTML 文件中的图片路径：

**正确格式：**
```html
<img src="/Yuan.github.io/img/posts/image.png">
```

**错误格式：**
```html
<img src="/img/posts/image.png">  <!-- 缺少 baseurl -->
```

### 3. 部署后检查
```bash
git add .
git commit -m "Fix image paths"
git push
```

然后在浏览器中：
1. 访问文章页面
2. 按 F12 打开开发者工具
3. 查看 Network 面板
4. 确认图片加载成功（没有红色错误）

---

## 📝 未来的正确做法

### 创建新文章时的模板
```markdown
---
title: 文章标题
date: 2026-05-06 10:00:00 +0800
categories: [分类]
tags: [标签]
description: 描述
---

文章内容...

![图片]({{ '/img/posts/image.jpg' | relative_url }})

更多内容...
```

### 快速插入图片
1. 复制图片到 `img/posts/` 目录
2. 在文章中添加：
   ```markdown
   ![描述]({{ '/img/posts/your-image.jpg' | relative_url }})
   ```

---

## 🎯 核心要点（必记）

1. **永远使用** `{{ 'path' | relative_url }}`
2. **路径必须以** `/` **开头**
3. **图片必须放在** `img/posts/` **目录**
4. **不要直接使用** `/img/posts/...`

---

## 📚 相关文档

- `BASEURL_FIX.md` - 详细的 baseurl 问题说明
- `IMAGE_GUIDE.md` - 完整的图片插入指南
- `img/posts/README.md` - 图片目录说明

---

**最后更新：** 2026-05-06
**状态：** ✅ 第一篇文章已修复
**下一步：** 检查其他文章并修复
