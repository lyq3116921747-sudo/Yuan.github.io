# GitHub Pages + baseurl 图片路径问题解决方案

## 🚨 问题根源

你的博客配置了 `baseurl: "/Yuan.github.io"`，这导致图片路径解析错误。

### 当前配置
```yaml
url: "https://lyq3116921747-sudo.github.io"
baseurl: "/Yuan.github.io"
```

### 问题表现
- ❌ 使用 `/img/posts/image.png` → 解析为 `https://lyq3116921747-sudo.github.io/img/posts/...`
- ✅ 应该解析为 → `https://lyq3116921747-sudo.github.io/Yuan.github.io/img/posts/...`

## ✅ 正确的图片引用方法

### 方法一：使用 `relative_url` 过滤器（推荐）

```markdown
![图片描述]({{ '/img/posts/image.png' | relative_url }})
```

**优点：**
- ✅ 自动适配 baseurl
- ✅ 本地开发和 GitHub Pages 都能正常显示
- ✅ Jekyll 官方推荐方法

### 方法二：使用 `site.baseurl` 变量

```markdown
![图片描述]({{ site.baseurl }}/img/posts/image.png)
```

### 方法三：HTML + `relative_url`

```html
<img src="{{ '/img/posts/image.png' | relative_url }}" alt="图片描述">
```

## 📝 实际示例对比

### ❌ 错误写法
```markdown
![图片](/img/posts/image.png)
```
- 本地开发：可以显示 ✅
- GitHub Pages：无法显示 ❌

### ✅ 正确写法
```markdown
![图片]({{ '/img/posts/image.png' | relative_url }})
```
- 本地开发：可以显示 ✅
- GitHub Pages：可以显示 ✅

## 🔧 批量修复现有文章

如果你的文章中已经使用了错误的路径，需要批量替换：

### 替换规则
**查找：** `](/img/posts/`
**替换为：** `]({{ '/img/posts/` **，然后在图片路径后添加** ` | relative_url }})`

### 示例
**修改前：**
```markdown
![图片](/img/posts/2026-05-05/image.png)
```

**修改后：**
```markdown
![图片]({{ '/img/posts/2026-05-05/image.png' | relative_url }})
```

## 🎯 完整的工作流程

### 1. 准备图片
```bash
# 将图片放到正确的目录
cp your-image.jpg img/posts/your-image.jpg
```

### 2. 在文章中引用
```markdown
---
title: 文章标题
date: 2026-05-06
---

# 文章内容

![图片描述]({{ '/img/posts/your-image.jpg' | relative_url }})
```

### 3. 本地测试
```bash
bundle exec jekyll serve
# 访问 http://localhost:4000
```

### 4. 部署到 GitHub
```bash
git add .
git commit -m "Add article with images"
git push
```

## 📋 快速参考卡片

### Markdown 图片语法
```markdown
<!-- 标准语法 -->
![alt text]({{ '/img/posts/image.jpg' | relative_url }})

<!-- 带标题 -->
![alt text]({{ '/img/posts/image.jpg' | relative_url }})
*图片标题*

<!-- HTML 语法 -->
<img src="{{ '/img/posts/image.jpg' | relative_url }}" alt="描述">
```

### 需要记住的要点
1. ✅ **始终使用** `{{ 'path' | relative_url }}`
2. ✅ **路径必须以** `/` **开头**
3. ✅ **图片放在** `img/posts/` **目录**
4. ✅ **使用英文文件名**

## 🧪 验证图片显示

部署后检查图片是否正常显示：

1. **打开浏览器开发者工具** (F12)
2. **查看 Network 面板**
3. **寻找图片加载错误** (红色标记)
4. **检查图片 URL 是否正确**

正确的图片 URL 格式：
```
https://lyq3116921747-sudo.github.io/Yuan.github.io/img/posts/image.jpg
```

错误的图片 URL 格式：
```
https://lyq3116921747-sudo.github.io/img/posts/image.jpg  # 缺少 baseurl
```

## 💡 为什么需要 baseurl？

`baseurl` 用于：
- GitHub Pages 项目站点（非用户页面）
- 子目录部署
- 多项目共存

你的站点部署在：
```
https://username.github.io/repo-name/
```

所以需要设置：
```yaml
baseurl: "/repo-name"
```

## 🔄 如果想简化配置

如果你有自己的域名，或者想使用 GitHub Pages 用户页面，可以简化配置：

### 方案一：使用用户页面
1. 将仓库名改为 `username.github.io`
2. 设置 `baseurl: ""`
3. 就可以直接使用 `/img/posts/image.png`

### 方案二：使用自定义域名
1. 在 `CNAME` 文件中设置自定义域名
2. 可以简化 `baseurl` 设置

## 📞 常见错误排查

### 错误 1：图片显示为破碎图标
**原因：** 路径错误或文件不存在
**解决：** 检查图片路径和文件是否存在

### 错误 2：本地显示正常，GitHub Pages 不显示
**原因：** 没有使用 `relative_url`
**解决：** 添加 `{{ 'path' | relative_url }}`

### 错误 3：图片路径包含 baseurl 重复
**原因：** 同时使用了 `baseurl` 和绝对路径
**解决：** 使用 `relative_url` 过滤器

---

**更新时间：** 2026-05-06
**适用版本：** Jekyll 3.x, 4.x
