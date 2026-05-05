# 博客图片插入解决方案

## 问题分析

Jekyll 博客无法插入图片的常见原因：
1. 图片路径不正确
2. 缺少专门的图片目录
3. 相对路径 vs 绝对路径混淆
4. 图片文件命名不规范

## 解决步骤总结

### ✅ 第一步：创建图片目录
```bash
mkdir -p img/posts
```

### ✅ 第二步：准备图片文件
- 将图片复制到 `img/posts/` 目录
- 推荐格式：JPG、PNG、WebP
- 建议最大宽度：1200px
- 使用英文文件名和连字符

### ✅ 第三步：在文章中引用图片
在 Markdown 文件中使用绝对路径：
```markdown
![图片描述](/img/posts/your-image.jpg)
```

### ✅ 第四步：配置 Jekyll
更新 `_config.yml` 添加图片支持：
```yaml
defaults:
  - scope:
      path: "img/posts"
    values:
      image: true
```

### ✅ 第五步：添加图片样式
在 CSS 中添加图片显示样式（已完成）：
```css
.post-content img {
  max-width: 100%;
  height: auto;
  border-radius: 6px;
  margin: 20px 0;
}
```

## 快速参考

### 标准图片插入
```markdown
![描述](/img/posts/screenshot-2024-05-06.png)
```

### 带尺寸的图片
```html
<img src="/img/posts/image.jpg" alt="描述" style="width: 80%;">
```

### 居中图片带标题
```html
<div style="text-align: center;">
  <img src="/img/posts/image.jpg" alt="描述" style="max-width: 100%;">
  <p style="color: #888; font-size: 0.9em;">图片标题</p>
</div>
```

## 目录结构
```
Yuan.github.io/
├── img/
│   ├── posts/           # 文章图片存放处
│   │   ├── README.md
│   │   └── *.jpg
│   ├── background1.webp
│   └── icon/
├── _posts/
│   └── 2026-05-06-*.md
└── assets/
```

## 注意事项

### ✅ 正确做法
- ✅ 使用绝对路径：`/img/posts/image.jpg`
- ✅ 英文文件名：`screenshot-2024-05-06.png`
- ✅ 添加 alt 属性：`![描述](路径)`
- ✅ 压缩图片优化加载速度

### ❌ 错误做法
- ❌ 相对路径：`../img/posts/image.jpg`
- ❌ 中文文件名：`图片.jpg`
- ❌ 特殊字符：`image@#$.jpg`
- ❌ 忘记 alt 属性

## 测试图片

创建测试文章验证图片显示：
```bash
# 1. 复制测试图片到 img/posts/
cp test.jpg img/posts/test-image.jpg

# 2. 在文章中添加
![测试图片](/img/posts/test-image.jpg)

# 3. 本地预览
bundle exec jekyll serve
```

## 常见问题解决

### 图片不显示
1. 检查路径是否以 `/` 开头
2. 确认文件在 `img/posts/` 目录
3. 清除浏览器缓存
4. 检查文件扩展名大小写

### 图片过大
1. 压缩图片文件
2. 使用 HTML 设置宽度：`style="max-width: 800px;"`
3. 使用响应式图片

### 移动端显示问题
CSS 已添加响应式支持：
```css
max-width: 100%;
height: auto;
```

## 成功标志

当你看到以下情况，说明图片配置成功：
- ✅ 本地预览图片正常显示
- ✅ GitHub Pages 构建成功
- ✅ 图片在各种设备上正常显示
- ✅ 图片加载速度合理

## 下一步

1. 将图片整理到 `img/posts/` 目录
2. 更新现有文章中的图片路径
3. 优化图片大小和格式
4. 测试各种设备和浏览器

---

**创建日期**: 2026-05-06
**最后更新**: 2026-05-06
