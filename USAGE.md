# Mermaid 图片上传工具使用示例

## 快速开始

### 1. 基本使用（替换模式）
将Markdown文件中的Mermaid代码全部替换为图片链接：
```bash
python mermaid_uploader.py --markdown 我的文章.md --upload
```

输出文件：`我的文章_with_images.md`

### 2. 保留模式（代码+图片）
保留原始Mermaid代码，在每个图表下方添加图片链接：
```bash
python mermaid_uploader.py --markdown 我的文章.md --upload --keep-mermaid
```

### 3. 双文件模式（推荐公众号使用）
同时生成两个独立文件：
```bash
python mermaid_uploader.py --markdown 我的文章.md --upload --output-two-files
```

输出文件：
- `我的文章_images_only.md`：仅包含图片链接，可直接复制到公众号编辑器
- `我的文章_code_only.md`：仅保留Mermaid代码，用于后续编辑和版本管理

### 4. 单个图表转换
直接转换单个Mermaid代码：
```bash
python mermaid_uploader.py --code "graph LR A[开始] --> B[结束]" --upload
```

## 支持的图床

| 图床名称 | 命令参数 | 需要API Key | 特点 |
|---------|---------|------------|------|
| FreeImage.host | freeimage | ❌ | 国内访问快，免费无水印 |
| Postimages | postimages | ❌ | 稳定可靠，全球访问 |
| Imgur | imgur | ✅ | 国外知名图床，需要翻墙 |
| Cloudinary | cloudinary | ✅ | 功能强大，支持CDN |

## 最佳实践

### 公众号发布工作流
1. 写作时使用Mermaid代码绘制图表
2. 发布前使用双文件模式处理：
   ```bash
   python mermaid_uploader.py --markdown 公众号文章.md --upload --output-two-files
   ```
3. 将 `*_images_only.md` 的内容复制到公众号编辑器
4. 将 `*_code_only.md` 提交到Git仓库保存源码

### 技术博客写作
- 对于面向技术读者的博客，使用 `--keep-mermaid` 模式，同时展示代码和图片
- 对于普通用户阅读的博客，使用默认替换模式，只展示图片

## 常见问题

### Q: 转换失败怎么办？
A: 首先检查Mermaid语法是否正确，可以使用在线编辑器（https://mermaid.live/）验证。如果语法正确，尝试添加 `--format html` 参数查看生成的HTML页面，了解具体错误信息。

### Q: 图片上传后不显示？
A: 国内用户推荐使用默认的 `freeimage` 图床，其他图床可能被墙或访问速度慢。

### Q: 可以自定义输出文件名吗？
A: 可以使用 `--output-markdown` 参数指定输出文件路径：
```bash
python mermaid_uploader.py --markdown input.md --output-markdown output.md --upload
```
