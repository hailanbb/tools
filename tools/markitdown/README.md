# MarkItDown · 文档转 Markdown

> 🔗 **原项目 GitHub 地址**：[microsoft/markitdown](https://github.com/microsoft/markitdown)

微软维护的 Python 文档转换工具，将文件中的文字及标题、列表、表格、链接等结构整理为 Markdown。适合知识库入库、检索和大模型文本预处理；它不以还原原文件的视觉排版为目标。

**[官方发行页](https://github.com/microsoft/markitdown/releases/tag/v0.1.7) · [上游说明](source/README.md) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 文档转换 |
| 收藏版本 | v0.1.7，2026-07-29 发布 |
| 运行环境 | Python 3.10+；可在相应 Python 环境支持的 Windows、macOS、Linux 上使用 |
| 典型格式 | PDF、DOCX、PPTX、XLSX/XLS、HTML、CSV、JSON、XML、EPUB 等；依赖按格式安装 |
| 许可证 | [MIT 原文](source/LICENSE) |
| 验证程度 | 文档与源码核验；未安装实测 |

## 第一阶段：环境自检与首次使用

### 1. 准备独立 Python 环境

先确认 `python --version` 为 3.10 或以上。Linux/macOS 可能需要使用 `python3`，Windows 也可使用 `py -3`。

```shell
python -m venv .venv
```

后续命令使用这个虚拟环境中的 Python：Windows 为 `.venv\Scripts\python.exe`，Linux/macOS 为 `.venv/bin/python`。也可以按本机习惯激活环境；不必为了激活而更改系统脚本执行策略。

### 2. 安装匹配用途的依赖

以下示例中的 `python` 应指向刚创建的环境。固定本次收藏版本：

```shell
python -m pip install "markitdown[all]==0.1.7"
```

只处理常用文档时，可选更精简的组合：

```shell
python -m pip install "markitdown[pdf,docx,pptx,xlsx]==0.1.7"
```

`[all]` 安装可选格式依赖，不等于自动配置云服务或所有第三方插件。安装步骤本次未执行。

## 第二阶段：核心工作流

### 命令行转换

在环境已激活、`markitdown` 命令可用时：

```shell
markitdown "input.pdf" -o "output.md"
markitdown "report.docx" -o "report.md"
markitdown "slides.pptx" -o "slides.md"
```

输入和输出路径含空格或中文时加引号；选择尚未使用的输出文件名，避免覆盖已有文件。未激活环境时，可使用其 Scripts/bin 目录下的命令入口。

转换后打开 Markdown，抽查标题、表格、链接和关键段落。复杂布局、公式或扫描件需人工检查，不能把“有输出”当作内容完整。

### Python 中使用

```python
from pathlib import Path
from markitdown import MarkItDown

converter = MarkItDown(enable_plugins=False)
result = converter.convert_local("input.docx")
with Path("output.md").open("x", encoding="utf-8") as output:
    output.write(result.text_content)
```

此示例仅接收本地文件，输出已存在时会报错而不覆盖。处理外部用户提供的路径或 URL 时，应限制可访问的文件与网络范围；上游通用 convert 方法会使用当前进程的访问权限。

### OCR、图片和云服务

- 基础文本及 Office 转换不要求提供模型 API Key。
- 扫描 PDF、嵌入图片的文字和图片描述，不能假定基础安装均可完整提取。按上游说明选择 OCR 插件、模型或 Azure 路径。
- 第三方插件默认关闭；`--list-plugins` 查看已安装插件，`--use-plugins` 才启用它们。
- Azure Document Intelligence、Azure Content Understanding 或模型视觉功能需要相应配置，可能把内容发送到外部服务并产生费用。先明确所选方式，再使用；本次未启用这些功能。

详细选项见[同版本完整 README](source/README.md)。

### 常见问题、更新与卸载

| 现象 | 检查方式 |
| :--- | :--- |
| 找不到 markitdown 命令 | 确认安装和运行使用同一虚拟环境 |
| 某种格式缺少依赖 | 安装对应 extra，例如 pdf、docx、pptx 或 xlsx |
| 扫描件没有文字 | 检查是否需要额外 OCR，不要只反复转换 |
| 表格或排版不理想 | 该工具面向结构化文本提取，复杂页面需抽查或改用适合的转换方案 |

更新前查看官方发行记录；需要升级时，在对应环境运行 `python -m pip install --upgrade "markitdown[all]"`。升级会离开本次固定版本，收藏快照不会自动改变。

卸载主包：`python -m pip uninstall markitdown`。这通常不移除全部依赖；若使用专门虚拟环境，可在确认不含资料或其他项目后移除该环境。转换输出单独保留。

## 源码与依据

[source/](source/) 保存原始项目；主要 Python 包位于 [packages/markitdown](source/packages/markitdown)。中文指南依据所选版本英文说明整理，未发现独立中文 README。

来源：[固定提交 README](https://github.com/microsoft/markitdown/blob/fd239d5d2be43d9b68329730206b9312c7d5a388/README.md)、[Python 包配置](source/packages/markitdown/pyproject.toml)、[v0.1.7 发行说明](https://github.com/microsoft/markitdown/releases/tag/v0.1.7)。
