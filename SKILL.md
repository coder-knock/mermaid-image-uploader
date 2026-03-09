# Mermaid 图片生成与图床上传技能

将 Mermaid 图表转换为图片并上传到免费图床，专为公众号文章、技术博客和自媒体内容创作设计。

## 功能特性

- 🎨 将 Mermaid 代码转换为高质量图片
- ☁️ 支持多个免费图床上传，无需复杂配置
- 🔗 自动返回图片 URL，直接用于 Markdown 文档
- 📝 批量处理 Markdown 文件中的 Mermaid 图表
- 🖼️ 支持多种图片格式 (PNG, SVG, JPG, HTML)
- 💡 **三种处理模式**，满足不同场景需求：
  - 🔄 **替换模式**：Mermaid代码完全替换为图片链接（默认）
  - 📝 **保留模式**：保留原始Mermaid代码，在下方添加图片链接（`--keep-mermaid`）
  - 📦 **双文件模式**：同时生成两个独立文件（`--output-two-files`）
    - `*_images_only.md`：仅包含上传后的图片链接（无Mermaid代码）
    - `*_code_only.md`：仅保留原始Mermaid代码（无图片链接）

## 快速开始

### 安装依赖

```bash
pip install mermaid-cli requests
```

或者安装 Node.js 的 mermaid-cli：

```bash
npm install -g @mermaid-js/mermaid-cli
```

### 使用方法

```bash
# 1. 转换单个 Mermaid 文件
python mermaid_uploader.py --input diagram.mmd --output diagram.png

# 2. 转换 Markdown 文件中的所有 Mermaid 图表（替换为图片，默认模式）
python mermaid_uploader.py --markdown article.md --upload

# 3. 转换 Markdown 文件，保留原始 Mermaid 代码并在下方添加图片
python mermaid_uploader.py --markdown article.md --upload --keep-mermaid

# 4. 双文件输出模式：同时生成图片版本和代码版本两个独立文件
python mermaid_uploader.py --markdown article.md --upload --output-two-files

# 5. 指定图床（默认使用 freeimage，国内访问速度快）
python mermaid_uploader.py --input diagram.mmd --image-host imgur

# 6. 直接输入 Mermaid 代码生成图片
python mermaid_uploader.py --code "graph LR A-->B" --upload
```

## 支持的图床

| 图床 | 需要API Key | 特点 |
|------|------------|------|
| Imgur | ✅ | 稳定，国外 |
| FreeImage.host | ❌ | 免费，国内访问快 |
| Postimages | ❌ | 简单易用 |
| Cloudinary | ✅ | 功能强大 |

## 文件结构

```
skills/mermaid-image-uploader/
├── SKILL.md                    # 本文件
├── package.json                # 技能配置
├── README.md                   # 详细说明
├── mermaid_uploader.py         # 主程序
├── mermaid_converter.py        # Mermaid 转换器
├── image_host_uploader.py      # 图床上传器
└── examples/                   # 示例
    ├── sample_diagram.mmd
    └── sample_article.md
```

## 使用示例

### 1. 转换单个 Mermaid 图表

```python
from mermaid_uploader import MermaidUploader

uploader = MermaidUploader()

# 转换并上传
url = uploader.convert_and_upload(
    mermaid_code="""
    graph LR
        A[开始] --> B[处理]
        B --> C[结束]
    """,
    image_host="freeimage"
)

print(f"图片URL: {url}")
```

### 2. 处理 Markdown 文件

```python
from mermaid_uploader import MarkdownProcessor

processor = MarkdownProcessor()

# 处理文件，替换所有 Mermaid 为图片链接
processor.process_file("article.md", "article_with_images.md")
```

## 命令行参数

```
--input, -i              输入的 Mermaid 文件
--output, -o             输出的图片文件
--markdown, -m           处理的 Markdown 文件
--output-markdown        输出的 Markdown 文件路径（可选）
--upload, -u             是否上传到图床
--image-host             指定图床 (imgur, freeimage, postimages, cloudinary)
--format, -f             输出格式 (png, svg, jpg, html)
--api-key                图床 API Key
--code, -c               直接输入 Mermaid 代码
--keep-mermaid           保留原始 Mermaid 代码，在下方添加图片链接
--output-two-files       输出两个独立文件：一个仅含图片，一个仅含代码
--test                   运行测试
```

## 最佳实践与使用场景

### 公众号文章发布
使用 **双文件模式** 生成两个版本：
- 图片版本：直接复制到公众号编辑器，完美显示图表
- 代码版本：保留原始Mermaid代码，用于后续编辑和版本管理

### 技术博客写作
- 使用 **保留模式**：在文章中同时展示Mermaid代码和渲染后的图片，方便读者学习和复制使用
- 或者使用 **替换模式**：只显示图片，保持文章整洁

### 文档管理
- 技术文档：使用替换模式，生成适合网页展示的版本
- 源码文档：保留Mermaid代码，便于团队协作和修改

### 团队协作
- 设计人员：使用图片版本，直观查看架构图和流程图
- 开发人员：使用代码版本，直接修改和更新图表

## 常见问题

**Q: 转换失败怎么办？**
A: 可以尝试使用 `--format html` 参数查看生成的HTML文件，检查Mermaid语法是否正确。

**Q: 上传到哪个图床比较好？**
A: 国内用户推荐使用默认的 `freeimage`，无需API Key，上传速度快，稳定性好。

**Q: 生成的图片有水印吗？**
A: 所有免费图床生成的图片都没有水印，可以放心使用。

## 欢迎关注

欢迎关注微信公众号：**拿客**

获取更多技术干货和开源工具分享！

## 许可证

MIT License
