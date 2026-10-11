# TTPlayer · 千千静听社区复刻版

> 🔗 **原项目 GitHub 地址**：[Sonic853/TTPlayer](https://github.com/Sonic853/TTPlayer)

**TTPlayer**（Thousand Tunes Player）是基于经典无损音乐播放器“千千静听”（TTPlayer 5.7.9）行为和 ABI 边界深度复刻的现代开源重写项目。它不仅完整还原了经典的九宫格位图皮肤、动感逐字歌词、十段图形均衡器与插件扩展体系，还针对现代 Windows 10/11 系统进行了全方位升级，支持系统媒体控件（SMTC）、任务栏缩略图播控、Winamp 皮肤支持、Discord 状态同步、独立工作进程插件沙盒与丰富的高清无损编解码器扩展。

**[官方发行页](https://github.com/Sonic853/TTPlayer/releases/tag/2026.10.09) · [中文文档](source/README_chs.md) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 媒体处理 |
| 收藏版本 | 2026.10.09，2026-10-09 发布 |
| 运行环境 | Windows XP SP3 / Windows 7 / Windows 10 / Windows 11 (x86/Win32) |
| 核心能力 | 经典千千静听复刻、逐字动感歌词、SMTC 系统媒体控件、Winamp 皮肤支持、无损音频解码、独立工作进程沙盒、HTTPS 歌词源 |
| 许可证 | [MIT](UPSTREAM.md) |
| 验证程度 | 文档与源码核验；未编译、未在 Windows 实机运行 |

---

## 第一阶段：环境自检与首次使用

### 1. 运行前提与版本说明

* **核心依赖**：TTPlayer 重建版需要与原版 5.7.9 的资源文件协同运行（依赖 `ttpcomm.dll`、`ttpres.dll`、`Skin` 等目录）。
* **架构要求**：程序为 32 位（x86/Win32）架构构建，完美兼容 32 位与 64 位 Windows 系统。
* **独立配置**：重建版配置独立写入 `TTPlayerRebuild.xml`，首次运行可导入原版配置且不覆盖原版数据，支持与原版千千静听安全共存。

### 2. 官方发行包获取与安装步骤

1. 前往 [TTPlayer Releases 页面](https://github.com/Sonic853/TTPlayer/releases/tag/2026.10.09) 下载主程序包：
   - `TTPlayerRebuild-2026.10.09.zip`
2. 解压并将压缩包内的 `TTPlayerRebuild.exe`、`TTPUpdater.exe`、`ttpcomm.dll` 及 `AddIn` 目录复制到千千静听所在目录（与 `TTPlayer.exe` 处于同级路径，合并 `AddIn` 目录）。
3. **可选插件包（按需安装）**：
   - **音视频解码增强包**（`CodecAddIn-Rebuild-*.zip`）：包含 WebM、APE、FLAC、MP3/WMA 编码、OGG/Opus、AAC 插件，解压并合并至 `AddIn` 目录。
   - **扩展功能包**（`ExtraAddIn-*.zip`）：包含 Winamp 皮肤支持、MAKI 虚拟机与多语言包，解压合并 `AddIn`，并将 `i18n` 目录放置在主程序同级。
4. 双击运行 `TTPlayerRebuild.exe` 即可启动。

### 3. 源码构建（面向开发者）

若需从源代码自行编译：

* **构建依赖**：
  - Visual Studio 2026（包含“使用 C++ 的桌面开发”组件）
  - CMake 4.2 及以上版本
* **构建指令**：
  ```powershell
  # 必须使用 Win32/x86 架构生成项目配置
  cmake -S . -B build -G "Visual Studio 18 2026" -A Win32 -DBUILD_TESTING=OFF -DTTPLAYER_STAGE_RUNTIME=OFF
  cmake --build build --config Release --target ttplayer_rebuild --parallel 4
  ```
  生成产物位于 `build/Release/TTPlayerRebuild.exe`。

---

## 第二阶段：核心工作流

### 1. 经典界面与皮肤体验

* **多代千千皮肤兼容**：全面兼容经典位图 `.skn` 皮肤以及 6.x 以上版本采用的 BMP/PNG 混合透明皮肤，呈现原汁原味的四态按钮与光影过渡。
* **Winamp 皮肤无缝运行**：启用 `ttp_waskin.dll` 插件后，可直接载入 Winamp 经典现代皮肤与配色方案。

### 2. 动感歌词与全屏交互

* **高精度动感歌词**：支持本地 LRC 文件载入与逐字变色高亮。
* **拖拽进度定位**：在歌词文字或显示区域空白处按住鼠标拖动，即可精准拖拽跳转歌曲播放进度。
* **增强在线歌词服务**：内置 HTTPS 传输支持与可扩展的自定义歌词服务器配置（默认提供稳定版在线歌词搜索插件）。
* **多屏全屏与封面显示**：全屏模式支持指定显示器、桌面透明置顶显示以及高清专辑大图呈现。

### 3. 现代 Windows 深度集成

* **SMTC 媒体面板与任务栏控制**：在 Windows 10/11 的锁屏与音量浮窗中展示曲目元数据与封面图，支持通过系统媒体按键及任务栏缩略图直接切歌与暂停。
* **独立工作进程与故障隔离**：音频标签元数据解析、DSP 音效插件探测与音频输出设备枚举均在隔离子进程中运行，彻底避免因单个问题插件崩溃连带导致播放器主界面闪退。
* **Discord 音乐状态同步**：实时在 Discord 个人资料展示当前歌曲名称、艺术家及播放进度。

---

## 排障与日常维护

* **启动报错或提示缺少 DLL**：请确保不要仅替换单独的 EXE，必须退出播放器后将主程序包中的 `ttpcomm.dll` 和 `AddIn` 目录整包覆盖，避免混用不同版本的核心库。
* **歌词无法在线搜索**：检查 `AddIn/ttp_lrcsh.dll` 与 `AddIn/ttp_https.dll` 是否已正确定位，并确认网络防火墙未拦截播放器访问。
* **卸载与还原**：
  - 重建版所有独立配置均保存在 `TTPlayerRebuild.xml`。
  - 直接删除 `TTPlayerRebuild.exe`、`TTPlayerRebuild.xml` 及新增的插件 DLL 即可恢复到原版状态，不影响原有千千静听的数据。