# Lap 来源与快照

| 字段 | 记录 |
| :--- | :--- |
| 原项目 | [julyx10/lap](https://github.com/julyx10/lap) |
| 正式版本 | [v0.3.1](https://github.com/julyx10/lap/releases/tag/v0.3.1) |
| 发布日期 | 2026-08-18 |
| 固定提交 | [d6cad080d2a5e59206ec062b83ef8e92b37ee896](https://github.com/julyx10/lap/tree/d6cad080d2a5e59206ec062b83ef8e92b37ee896) |
| 收录及核验时间 | 2026-09-09T20:58:00+08:00 |
| 许可证 | [GPL-3.0](source/LICENSE) |
| 源文件 | 403 个 Git 跟踪文件 |

版本标签 `v0.3.1` 对应提交 SHA `d6cad080d2a5e59206ec062b83ef8e92b37ee896`。源文件原始字节与 Git 提交逐一核对；[SHA-256 清单](snapshot-manifest.json)用于后续完整性核验。

### 子模块记录

源项目在 `.gitmodules` 中声明了 4 个 C/C++ 图像底层解码依赖子模块（默认保持 GitLink 未展开状态，未递归拉取源码）：
* `src-tauri/third_party/LibRaw`: `https://github.com/LibRaw/LibRaw.git`（分支 `0.22-stable`，commit `b860248a89d9082b8e0a1e202e516f46af9adb29`，未展开）
* `src-tauri/third_party/libjpeg-turbo`: `https://github.com/libjpeg-turbo/libjpeg-turbo.git`（分支 `3.1.x`，commit `9217719d3a58633923b096af4c1d50d304768a64`，未展开）
* `src-tauri/third_party/libheif`: `https://github.com/strukturag/libheif.git`（分支 `v1.21.x-releases`，commit `62f1b8c76ed4d8305071fdacbe74ef9717bacac5`，未展开）
* `src-tauri/third_party/libde265`: `https://github.com/strukturag/libde265.git`（commit `3cd9fbf15ae30edafa22a29fdd8a89355ad52ad0`，未展开）

未发现符号链接或 LFS 指针。不包含 `.git` 版本历史、预编译桌面安装包或本地数据库缓存；嵌套的 `source/.github` 仅作配置归档。

已核验同版本中英文 README、发布日志及官方安装包发布状态。未在本地安装桌面客户端实测，未建立本地实际相册索引或执行 AI 搜索推理。本收藏不代表所有图像格式、平台硬件加速及超大图库性能均已实测。
