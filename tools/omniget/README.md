# OmniGet · 全能课程与媒体下载工具箱

> 🔗 **原项目 GitHub 地址**：[tonhowtf/omniget](https://github.com/tonhowtf/omniget)

一款免费开源、免终端的桌面全能媒体与课程下载器及学习工具箱（基于 Tauri + Rust + Svelte）。基于 yt-dlp 与自研下载引擎，支持下载 Udemy/Hotmart 课程、YouTube、Bilibili、Instagram、TikTok 以及 1,800 多个站点的音视频与电子书，并内置课程播放器、PDF/EPUB 阅读器与音频库。

**[官方发行页](https://github.com/tonhowtf/omniget/releases/tag/v0.9.2) · [上游中文说明](source/README_zh_CN.md) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 媒体处理 |
| 收藏版本 | v0.9.2，2026-09-11 发布 |
| 运行环境 | 桌面端支持 Windows (x64 / Portable)、macOS (Apple Silicon / Intel)、Linux (AppImage / DEB / RPM) |
| 核心特性 | 课程下载（Udemy/Hotmart 等）、1800+ 站点视频解析、种子/磁力下载、Whisper 转写、内置播放器与电子书阅读 |
| 许可证 | [GPL-3.0 原文](source/LICENSE) |
| 验证程度 | 文档与源码核验；未安装桌面端实测 |

---

## 第一阶段：环境自检与首次使用

### 1. 官方安装包获取

官方推荐直接下载预编译安装包使用：

| 平台 / 架构 | 安装包类型 | 下载入口 | 验证与运行说明 |
| :--- | :--- | :--- | :--- |
| **Windows x64** | 安装包 (.exe) | [omniget_0.9.2_x64-setup.exe](https://github.com/tonhowtf/omniget/releases/download/v0.9.2/omniget_0.9.2_x64-setup.exe) | 推荐安装版 |
| **Windows x64 (便携版)** | 免安装 (.exe) | [omniget_0.9.2_x64-portable.exe](https://github.com/tonhowtf/omniget/releases/download/v0.9.2/omniget_0.9.2_x64-portable.exe) | 解压即用，不写注册表 |
| **macOS Apple Silicon** | DMG 镜像 | [omniget_0.9.2_aarch64.dmg](https://github.com/tonhowtf/omniget/releases/download/v0.9.2/omniget_0.9.2_aarch64.dmg) | 首次打开若提示损坏需移除隔离属性（见下文） |
| **macOS Intel** | DMG 镜像 | [omniget_0.9.2_x64.dmg](https://github.com/tonhowtf/omniget/releases/download/v0.9.2/omniget_0.9.2_x64.dmg) | 同上 |
| **Linux (Debian/Ubuntu)** | DEB 包 | [omniget_0.9.2_amd64.deb](https://github.com/tonhowtf/omniget/releases/download/v0.9.2/omniget_0.9.2_amd64.deb) | 适用于 Ubuntu 22.04+、Debian 12+ 等 |
| **Linux 通用** | AppImage | [omniget_0.9.2_amd64.AppImage](https://github.com/tonhowtf/omniget/releases/download/v0.9.2/omniget_0.9.2_amd64.AppImage) | Debian 12+ 需安装 `libfuse2` |

> **macOS 首次打开提示“已损坏”解决方法**：
> ```bash
> xattr -cr /Applications/omniget.app
> ```

### 2. 首次启动与基础配置

1. **启动应用**：打开应用后直接进入简洁的主界面。
2. **下载目录设置**：在设置中选择你的媒体或课程保存路径，文件直接保存在本地硬盘中，无需账号登录，无云端中转。
3. **Cookie / 凭据管理（可选）**：如需下载已购买的 Udemy/Hotmart 课程或受限内容，可在设置中配置浏览器 Cookie。

---

## 第二阶段：核心工作流

### 1. 媒体与课程下载

* **链接粘贴即下**：直接在输入框粘贴网页链接（YouTube、B站、Instagram、X、TikTok、Udemy 等）、磁力链接或拖入 `.torrent` 种子文件。
* **清晰度与格式选择**：支持选择视频清晰度、音频提取（MP3/M4A/FLAC）或整集/播放列表批量下载。
* **课程完整打包**：支持 Udemy 与 Hotmart 课程的章节结构化下载（附带课件文档、练习题与中英字幕）。

### 2. 内置学习与媒体工具箱

* **课程专属播放器**：保留课程章节目录树、支持记忆播放进度、双语字幕展示与倍速播放。
* **文档与图书阅读**：内置 PDF 与 EPUB 阅读器，直接在应用内阅读下载的配套课件与电子书。
* **离线转写与语音**：内置轻量 Whisper 语音识别与文字转语音工具，可为无字幕视频生成本地字幕。

---

## 排障与日常维护

* **下载解析失败或站点变动**：底层依赖 yt-dlp 等解析器，可在应用设置中手动检查并更新内置 yt-dlp 组件。
* **网络与代理设置**：访问海外平台（如 YouTube、Udemy）时，请在应用设置内配置 HTTP/SOCKS5 代理。
* **更新与升级**：桌面端支持自动检查更新；也可前往[官方 Release 页面](https://github.com/tonhowtf/omniget/releases)下载最新安装包覆盖安装。
* **卸载与清理**：
  - Windows：在“控制面板”或“设置 > 已安装的应用”中卸载 OmniGet。
  - macOS：将 Applications 中的 `omniget.app` 移到废纸篓。
  - 配置文件目录：`%APPDATA%\com.tonhowtf.omniget` (Windows) 或 `~/Library/Application Support/com.tonhowtf.omniget` (macOS)。
