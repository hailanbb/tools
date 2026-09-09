# LocalSend 来源与快照

| 字段 | 记录 |
| :--- | :--- |
| 原项目 | [localsend/localsend](https://github.com/localsend/localsend) |
| 固定版本 | [v1.18.2](https://github.com/localsend/localsend/releases/tag/v1.18.2) |
| 发布日期 | 2026-08-21 |
| 精确提交 | [af0416be50770a97760f7070684bc667b759a15c](https://github.com/localsend/localsend/tree/af0416be50770a97760f7070684bc667b759a15c) |
| 取得时间 | 2026-09-09T11:45:19+08:00 |
| 许可证 | [Apache-2.0 原文](source/LICENSE) |
| 普通源文件 | 1029 个，逐个对照固定提交的 Git blob，并保存 SHA-256 |
| 源文件改动 | 无；中文指南和本记录位于 source 之外 |

## 保存范围

保存该提交的全部普通 Git 跟踪文件，包含隐藏文件、原 README、中文说明、许可证与嵌套 `.github`。不保存 `.git` 历史，不下载发行安装包。源文件中的绝对仓库链接可能仍指向上游布局，原文不作改写。

发现一个 Git 子模块，未展开：

| 路径 | 上游 | 固定提交 |
| :--- | :--- | :--- |
| `support/submodules/flutter` | [flutter/flutter](https://github.com/flutter/flutter) | `00b0c91f06209d9e4a41f71b7a512d6eb3b9c694` |

子模块声明保留在 [source/.gitmodules](source/.gitmodules)。本目录不是独立 Git 仓库，不能在这里直接用 `git submodule update` 还原上游子模块；需要完整开发环境时请克隆上游、检出上述提交后按上游说明初始化依赖。

## 验证记录

- 已对照选中提交的 Git blob 检查每个源文件的原始字节，未发现 LFS 指针。
- `CHANGELOG.md` 是指向 `app/assets/CHANGELOG.md` 的符号链接；Git 中保留 120000 类型。Windows 工作副本可能显示为包含目标路径的文本文件，实际内容请打开 [app/assets/CHANGELOG.md](source/app/assets/CHANGELOG.md)。
- 已记录 [SHA-256 文件清单](snapshot-manifest.json)，用于检测缺失、额外文件与内容变化。
- 已核对官方中文及英文 README、发行版本、许可证、Flutter 版本和子模块信息。
- 未安装运行 LocalSend、未执行两台设备间传输、未编译源码；不表示软件运行或安全审计通过。

## 更新方法

明确要求更新后，先检查现有摘要和上游正式版差异，再生成新快照、指南及摘要；保留首次收录时间。存在个人源码改动时停止覆盖。最新版本入口：[上游 Releases](https://github.com/localsend/localsend/releases)。
