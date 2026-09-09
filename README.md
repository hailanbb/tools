# 🧰 Tools · 实用工具收藏

收藏 GitHub 上值得使用的软件和实用工具，覆盖文件传输、效率办公、媒体处理、系统维护与开发辅助等场景。每个工具都配有中文介绍、官方获取入口和上手指南，按需要保存源码快照。

**[🛠️ 工具索引](#catalog) · [📂 仓库结构](#structure) · [📥 收录方式](#collect)**

<a id="catalog"></a>

## 🛠️ 收藏工具索引

<!-- catalog:start -->

已收藏 **1** 个工具。版本为收录时快照，实际使用请查看官方发行页。

| 分类 | 工具 | 核心功能 | 使用场景 | 平台 | 收藏版本 | 详细说明 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 文件传输 | LocalSend · 局域网互传 | 电脑与手机在局域网内互传文件和文字 | 跨系统传照片、文档；无外网时交换资料 | Windows / macOS / Linux / Android / iOS / Fire OS | v1.18.2 | [👉 使用指南](tools/localsend/README.md) |

<!-- catalog:end -->

### 如何选择

- **电脑与手机互传文件** → [LocalSend 使用指南](tools/localsend/README.md)：支持多种系统，在本地网络内传照片、文档和文字。
- 更多类别随实际收藏增加，不设置空目录，也不把安装工具的流程套成 Agent 技能调用。

<a id="structure"></a>

## 📂 仓库结构

```text
tools/
├── README.md                     # 工具分类索引
├── tools/                        # 收藏的软件与实用工具
│   └── localsend/
│       ├── README.md             # 中文介绍、安装与使用指南
│       ├── UPSTREAM.md           # 原项目、版本与许可记录
│       ├── snapshot-manifest.json # 源文件完整性清单
│       └── source/               # 上游源码与原始说明
├── imported_sources.json         # 来源与版本清单，避免重复收藏
├── docs/collection-policy.md      # 收录与维护约定
└── scripts/                      # 本仓库的索引维护脚本
    ├── catalog.py
    └── test_catalog.py
```

工具统一放入 `tools/<工具名>/`，首页按用途分类；改变分类不改变工具地址。`scripts/` 仅维护本仓库，不是收藏条目。

<a id="collect"></a>

## 📥 收录方式

提供 GitHub 项目链接即可整理收录。每个条目包含：

1. **是什么、适合谁**：中文用途介绍、平台和使用场景。
2. **怎么获取和使用**：官方安装入口、最短操作步骤、常见问题、更新和卸载说明。
3. **来自哪里**：原项目地址、核验日期、版本与许可证。
4. **可选源码快照**：固定提交保存；体积或许可不适合复制时只保留介绍与链接。

同一来源重复提交不会新增重复条目；明确要求更新时才刷新既有快照。源码备份不包含 Git 历史或安装包，子模块与未实测部分在各条目中说明。

## 📌 维护约定

第三方源码和原始文档保持原样，保留各自许可证；中文指南独立编写。分类、版本、来源与目录由[来源清单](imported_sources.json)统一记录，详见[收录规范](docs/collection-policy.md)。

<details>
<summary>维护者：索引校验与自动化</summary>

Python 3.10+，不需要额外依赖。在仓库根目录运行：

```shell
python scripts/catalog.py check .
python scripts/catalog.py render .
python scripts/test_catalog.py
```

`check` 只读核验；`render` 仅刷新首页索引区域。

用于自动整理收藏的 [github-tools-collect 技能](https://github.com/hailanbb/skill-selection/tree/master/skills/github-tools-collect) 单独维护在 `skill-selection`，不属于本库收藏的软件。浏览、下载和使用本库工具无需安装该技能。

</details>
