# Lap · 本地私有照片管理器

> 🔗 **原项目 GitHub 地址**：[julyx10/lap](https://github.com/julyx10/lap)

一款开源、离线优先的现代化桌面照片管理工具（基于 Tauri + Vite + Rust）。面向拥有海量本地照片（10万+级别）的个人与摄影爱好者，提供完全私密、不强制上云、不锁定数据库的相册浏览、智能整理与本地 AI 搜索能力。

**[官方发行页](https://github.com/julyx10/lap/releases/tag/v0.3.1) · [官方网站](https://julyx10.github.io/lap/) · [上游中文说明](source/i18n/README.zh-CN.md) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 媒体处理 |
| 收藏版本 | v0.3.1，2026-08-18 发布 |
| 运行环境 | 桌面端支持 Windows 10/11 (x64 / ARM64)、macOS (Apple Silicon / Intel)、Linux (x64 / ARM64) |
| 核心特性 | 本地优先无强制上云、直接管理已有文件夹、本地 AI 搜图/人脸聚类、实况照片/RAW配对支持、四图对比选片 |
| 许可证 | [GPL-3.0 原文](source/LICENSE) |
| 验证程度 | 文档与源码核验；未安装桌面端实测 |

---

## 第一阶段：环境自检与首次使用

### 1. 官方安装包获取

官方推荐直接下载预编译安装包使用：

| 平台 / 架构 | 安装包类型 | 下载入口 | 验证与签名说明 |
| :--- | :--- | :--- | :--- |
| **Windows x64** | MSI 安装包 | [Lap_0.3.1_x64_en-US.msi](https://github.com/julyx10/lap/releases/download/v0.3.1/Lap_0.3.1_x64_en-US.msi) | 未签名，如遇 SmartScreen 拦截请选择“仍要保留”并核对校验和 |
| **Windows ARM64** | MSI 安装包 | [Lap_0.3.1_arm64_en-US.msi](https://github.com/julyx10/lap/releases/download/v0.3.1/Lap_0.3.1_arm64_en-US.msi) | 同上 |
| **macOS Apple Silicon** | DMG 镜像 | [Lap_0.3.1_aarch64.dmg](https://github.com/julyx10/lap/releases/download/v0.3.1/Lap_0.3.1_aarch64.dmg) | 已通过 Apple 官方公证 |
| **macOS Intel** | DMG 镜像 | [Lap_0.3.1_x64.dmg](https://github.com/julyx10/lap/releases/download/v0.3.1/Lap_0.3.1_x64.dmg) | 已通过 Apple 官方公证 |
| **Linux (Debian/Ubuntu)** | DEB 包 | [Lap_0.3.1_amd64.deb](https://github.com/julyx10/lap/releases/download/v0.3.1/Lap_0.3.1_amd64.deb) | 适用于 Ubuntu、Debian 等 |
| **Linux 通用** | AppImage | [Lap_0.3.1_amd64.AppImage](https://github.com/julyx10/lap/releases/download/v0.3.1/Lap_0.3.1_amd64.AppImage) | 添加执行权限后直接运行 |

> **macOS Homebrew 安装方式**：
> ```bash
> brew tap julyx10/lap
> brew install --cask lap
> ```

### 2. 首次启动与相册接入

1. **安装并打开 Lap**：遵循向导启动应用。
2. **选择已有照片文件夹**：Lap 采用**文件夹优先（Folder-first）**原则，直接选择存放照片与视频的磁盘目录，Lap 会进行后台只读扫描与索引，不会强行修改或移动原始目录结构。
3. **安全提示**：文件已嵌入的 EXIF（拍摄日期、相机、镜头、GPS 等）会自动读取；而 Lap 中创建的“合集”、“标签”、“评分”与“智能相册规则”保存在本地数据库中，不会污染原始照片文件。

---

## 第二阶段：核心工作流

### 1. 海量照片浏览与智能筛选

* **多维度过滤**：支持按时间线（日历热力图）、文件夹树、拍摄地点、相机型号、镜头参数、标签、星级评分与主体筛选。
* **智能相册 (Smart Albums)**：设定特定过滤规则（如“2025年 + 5星 + 佳能相机”），自动动态聚合符合条件的照片。
* **RAW + JPEG 配对与实况照片**：自动配对同一文件夹下的同名 RAW 与 JPG/HEIC 文件，在查看器中合成展示；完美支持 Apple Live Photo 动图与音频播放。

### 2. 本地 AI 搜索与相似照片排重

* **自然语言搜索**：在搜索栏输入“猫”、“海滩日落”、“生日蛋糕”等关键词，借助本地轻量 CLIP/多模态模型离线语义搜图（支持 50+ 语言）。
* **人脸识别与聚类**：本地计算人脸特征，按人物分组归纳照片。
* **重复与相似照片排重**：
  - 自动扫描视觉相似或完全一致的重复项。
  - 支持快捷保留/排除与批量移入回收站。
* **专业四窗格对比选片**：支持多张连拍照片同屏对比、缩放与对齐，挑出对焦与表情最佳成片。

---

## 排障与日常维护

* **关于文件管理习惯**：
  - 建议优先在 Lap 内部进行重命名、移动和删除操作，Lap 会同时保持关联附属文件（如 `.aae`、实况视频 `.mov`）及内部标签数据同步。
  - 若在操作系统资源管理器或 Finder 中直接修改了文件，可在相册界面点击“刷新扫描”重新对齐索引。
* **数据库备份**：在 **设置 → 存储** 中可自定义数据库存放路径并导出备份。
* **彻底卸载与数据清理**：
  - Lap 卸载不会删除你的任何原始照片。
  - Windows 完全清理缓存与配置：
    ```powershell
    Remove-Item -Recurse -Force -ErrorAction SilentlyContinue "$env:LOCALAPPDATA\com.julyx10.lap"
    Remove-Item -Recurse -Force -ErrorAction SilentlyContinue "$env:APPDATA\com.julyx10.lap"
    ```
  - macOS 完全清理：
    ```bash
    rm -rf "$HOME/Library/Application Support/com.julyx10.lap" "$HOME/Library/Caches/com.julyx10.lap"
    ```
