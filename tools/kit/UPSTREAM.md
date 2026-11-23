# KiT 上游来源记录

| 字段 | 记录 |
| :--- | :--- |
| 原项目 | [Luciferbobo/KiT](https://github.com/Luciferbobo/KiT) |
| 正式版本 | main 分支最新提交快照（上游未发布正式 Release 标签） |
| 发布日期 | 2026-11-20 |
| 固定提交 | [a9bf4a30e37076c4fb59a1461a5d5dfbd51a3294](https://github.com/Luciferbobo/KiT/tree/a9bf4a30e37076c4fb59a1461a5d5dfbd51a3294) |
| 记录时间 | 2026-11-23T08:50:00+08:00 |
| 许可证 | [AGPL-3.0](source/LICENSE) |
| 源码文件 | 58 个 Git 跟踪文件 |

上游仓库暂未创建 Release 标签，本次收录采用 `main` 分支最新稳定提交（Commit SHA: `a9bf4a30e37076c4fb59a1461a5d5dfbd51a3294`）。源码文件原始字节已与 Git blob 逐一比对核对，[SHA-256 清单](snapshot-manifest.json)通过契约校验。文件模式与原始内容完整保留，未修改源码。

未发现 gitlink 子模块、未发现符号链接或 Git LFS 指针。无超过 100 MiB 的单文件（最大文件为评测回测图表 `results/backtest_results/backtest_top10.png`，约 385 KiB）。模型权重文件（如 `step_market_284M.pt`）依上游设计存放在外部存储（Google Drive / Baidu Pan），不包含在 Git 快照内。

已核验同版本 README、LICENSE、论文设计架构（arXiv:2609.34507）与 Python 源码实现。未下载预训练模型权重实测，未执行实际行情推理或量化回测；本次仅作为文档规范与源码快照收录。
