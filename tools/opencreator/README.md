# OpenCreator · AI 创作工作台

> 🔗 **原项目 GitHub 地址**：[krillinai/OpenCreator](https://github.com/krillinai/OpenCreator)

开源的面向创作者与开发者的本地 AI 工作台（原名 KrillinAI）。它以 Codex CLI 为执行引擎，在其上构建了本地 Runtime、可视化创作工作区与桌面客户端，集成了视频翻译、视频下载、封面生成与图像生成等专用创作工具，同时支持多项目、后台 Run 与技能扩展。

**[官方发行页](https://github.com/krillinai/OpenCreator/releases/tag/v3.1.0) · [官方文档](https://github.com/krillinai/OpenCreator/blob/v3.1.0/docs/zh/README.md) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 媒体处理 |
| 收藏版本 | v3.1.0，2026-09-07 发布 |
| 运行环境 | 桌面端支持 Windows (x64)、macOS (Apple Silicon / Intel)；服务端与 CLI 亦支持 Linux |
| 核心能力 | 视频翻译（双语字幕/配音）、视频下载（yt-dlp 集成）、封面图生成、GPT 图像生成、通用 Agent 对话 |
| 许可证 | [Apache-2.0 / GPL-3.0](UPSTREAM.md) |
| 验证程度 | 文档与源码核验；未安装桌面端实测 |

---

## 第一阶段：环境自检与首次使用

### 1. 官方安装包获取

官方推荐直接使用预构建桌面应用（开箱即用，已内置必要运行时）：

| 操作系统 / 架构 | 推荐安装包下载入口 |
| :--- | :--- |
| **Windows x64** | [OpenCreator-3.1.0-win-x64.exe](https://github.com/krillinai/OpenCreator/releases/download/v3.1.0/OpenCreator-3.1.0-win-x64.exe) |
| **macOS Apple Silicon** | [OpenCreator-3.1.0-mac-arm64.dmg](https://github.com/krillinai/OpenCreator/releases/download/v3.1.0/OpenCreator-3.1.0-mac-arm64.dmg) |
| **macOS Intel** | [OpenCreator-3.1.0-mac-x64.dmg](https://github.com/krillinai/OpenCreator/releases/download/v3.1.0/OpenCreator-3.1.0-mac-x64.dmg) |

> 校验提示：官方在 Release 页面提供了 [SHA256SUMS.txt](https://github.com/krillinai/OpenCreator/releases/download/v3.1.0/SHA256SUMS.txt)。Windows 安装包暂未附带 Authenticode 签名，下载后建议核对 SHA-256 校验和。

### 2. 首次启动与配置

1. **启动应用**：双击运行安装包或挂载 DMG 并拖入 Applications 目录打开。
2. **Runtime 自动拉起**：客户端首次启动时会自动启动本地 Runtime，并初始化默认创作工程。
3. **AI 模型接入**：
   - 依赖 Codex 环境与大模型 API（如 OpenAI 兼容接口）。
   - 在应用设置界面填入所需的 API Key 与 Endpoint 即可启用对话及智能翻译能力。

---

## 第二阶段：核心工作流

### 1. 创作工具面板使用

在主界面左侧或控制台进入对应创作工具：

* **视频翻译 (Video Translation)**：
  - 导入本地视频或输入在线视频链接。
  - 支持 Whisper 语音转录（本地或云端服务）。
  - LLM 上下文感知断句、术语对齐与字幕翻译，可导出 SRT 字幕文件或渲染带双语字幕与配音的成品视频。
* **视频下载 (Video Downloader)**：
  - 支持解析 YouTube、Bilibili 等主流视频平台的公开视频链接。
  - 内置 yt-dlp 组件，可查看不同画质与音频格式并一键下载到本地工作区。
* **封面生成 (Thumbnail Generator)**：
  - 输入视频主题、链接或上传参考图，批量生成并对比多款内容封面图。
* **图像生成 (Image Generation)**：
  - 输入提示词，设定纵横比（16:9、9:16、1:1 等）与数量，生成并保存图片素材。

### 2. 通用 Agent 会话与工作台协同

除了固定工具面板外，可直接在主对话框中用自然语言向 Agent 发出创作指令。工作台的可视化状态机与 Agent 对话双向联动，执行进度与中间产出实时呈现。

---

## 排障与日常维护

* **yt-dlp 版本与更新**：OpenCreator 内置对 yt-dlp 组件的版本管理，如遇视频解析失败，可在设置面板中手动检查并更新 yt-dlp。更新若遇异常会自动回滚至先前可用版本。
* **网络与代理问题**：下载外部视频或调用海外 API 时，请确保系统代理配置正确，且端口未被占用。
* **更新与升级**：桌面端支持自动检查更新；也可直接前往[官方 Release 页面](https://github.com/krillinai/OpenCreator/releases)下载最新安装包覆盖安装。
* **卸载方式**：
  - Windows：在“控制面板”或“设置 -> 已安装的应用”中找到 OpenCreator 并执行卸载。
  - macOS：直接将 Applications 中的 OpenCreator.app 移至废纸篓，并清理 `~/Library/Application Support/OpenCreator` 缓存目录（如有需要）。
