# 🧰 工具精选（Tools Selection）

个人 GitHub 好工具收藏库。用中文说明解决什么问题、怎么开始使用，并保存可追溯的源码快照，让收藏变成真正用得上的工具箱。

**[🛠️ 工具索引](#catalog) · [📥 收藏方法](#collect) · [🤖 收藏技能](skills/github-tools-collect/README.md)**

## 📂 仓库结构

```text
tools/
├── README.md                       # 中文分类索引
├── imported_sources.json           # 来源、版本与防重清单（事实主表）
├── docs/collection-policy.md        # 收录、更新与验证规范
├── skills/github-tools-collect/    # 可反复使用的收藏技能
│   ├── SKILL.md                    # Agent 工作流
│   ├── README.md                   # 安装与使用
│   ├── agents/openai.yaml          # 技能展示信息
│   └── scripts/catalog.py          # 索引生成与完整性校验
└── tools/
    └── localsend/
        ├── README.md               # 中文上手指南
        ├── UPSTREAM.md             # 版本、许可、子模块与验证记录
        ├── snapshot-manifest.json  # 源文件 SHA-256 清单
        └── source/                 # 上游源码与原始文档
```

<a id="catalog"></a>

## 🛠️ 收藏工具索引

<!-- catalog:start -->

已收藏 **1** 个工具。版本为收录时快照，实际使用请查看官方发行页。

| 分类 | 工具 | 核心功能 | 使用场景 | 平台 | 收藏版本 | 详细说明 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 文件传输 | LocalSend · 局域网互传 | 电脑与手机在局域网内互传文件和文字 | 跨系统传照片、文档；无外网时交换资料 | Windows / macOS / Linux / Android / iOS / Fire OS | v1.18.2 | [👉 使用指南](tools/localsend/README.md) |

<!-- catalog:end -->

分类按用途增长：文件传输、效率办公、知识管理、开发辅助、媒体处理、系统维护、AI 工具。工具统一放在 `tools/<slug>/`，分类变化不移动目录；不为尚未收藏的分类创建空文件夹。

<a id="collect"></a>

## 📥 如何继续收藏

安装[收藏技能](skills/github-tools-collect/README.md)后，可以直接说：

> 把这个 GitHub 工具收藏到 hailanbb/tools：仓库链接。

也支持“更新 LocalSend 到最新正式版”“只收藏链接和中文指南，不保存源码”“检查工具索引是否一致”。同一来源再次收藏会返回已有条目；只有明确要求更新才替换快照。

## 📌 收录约定

- 中文指南放在工具目录，原始 README、许可证和源码放在 `source/`，不重写原作。
- 默认优先正式版，记录精确提交；没有正式版时说明采用的分支快照。
- 源码是时间点备份，不包含 Git 历史、安装包或自动更新承诺。子模块与 LFS 的完整性单独说明。
- 没有运行过的软件标注“文档核验”，不会把收藏等同于测试通过。
- 第三方文件沿用各自许可证；本仓库不以一个顶层许可证覆盖所有工具。详见[收录规范](docs/collection-policy.md)。

## 🔎 维护

需要 Python 3.10+，使用标准库，无额外依赖。在仓库根目录运行：

```shell
python skills/github-tools-collect/scripts/catalog.py check .
python skills/github-tools-collect/scripts/catalog.py render .
```

`check` 只读检查；`render` 仅更新首页的自动索引区域。新增或更新时同步维护来源主表、工具指南、来源说明与文件摘要。

组织与呈现参考 [skill-selection](https://github.com/hailanbb/skill-selection) 及其[转存至github](https://github.com/hailanbb/skill-selection/tree/master/skills/%E8%BD%AC%E5%AD%98%E8%87%B3github)；在此基础上增加版本固定、原文保留和一致性检查。
