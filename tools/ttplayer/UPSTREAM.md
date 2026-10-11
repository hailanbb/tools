# TTPlayer 来源与快照

| 字段 | 记录 |
| :--- | :--- |
| 原项目 | [Sonic853/TTPlayer](https://github.com/Sonic853/TTPlayer) |
| 正式版本 | [2026.10.09](https://github.com/Sonic853/TTPlayer/releases/tag/2026.10.09) |
| 发布日期 | 2026-10-09 |
| 固定提交 | [383bbaa2de9f996ed970155152f98472ce9eeb2a](https://github.com/Sonic853/TTPlayer/tree/383bbaa2de9f996ed970155152f98472ce9eeb2a) |
| 收录及核验时间 | 2026-10-11T21:12:00+08:00 |
| 许可证 | [MIT](source/LICENSE) |
| 源文件 | 480 个 Git 跟踪文件 |

版本标签 `2026.10.09` 为轻量标签（Lightweight Tag），对应实际目标提交 SHA（`383bbaa2de9f996ed970155152f98472ce9eeb2a`）。源文件原始字节与 Git 提交逐一核对；[SHA-256 清单](snapshot-manifest.json)用于后续完整性核验。

项目包含 1 个外部 Git 子模块（默认未递归拉取，保持未展开状态）：
- **路径**：`tests`
- **上游仓库**：`git@github.com:Sonic853/TTPlayer_Tests.git`
- **固定提交**：`e00ee2be73f6241e4e5e21740554e776e79e627f`

未发现符号链接或 LFS 指针。不包含 `.git` 版本历史、外部下载的千千静听原版二进制资源（如原版 `ttpcomm.dll`、`ttpres.dll`）或构建产物；嵌套的 `source/.github` 仅作构建工作流配置归档。

已核验同版本中英文 README、发布日志及 CMake 构建系统。未在本地通过 Visual Studio 执行完整 Win32 编译，未在 Windows 物理机运行播放器实测。本收藏不代表所有 DSP 插件与音频格式解码均已端到端实测。