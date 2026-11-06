# PowerToys · Windows 系统效率工具集

> 🔗 **原项目 GitHub 地址**：[microsoft/powertoys](https://github.com/microsoft/powertoys)

微软官方维护的 Windows 系统级效率与自定义增强工具集，集成窗口高级分屏管理（FancyZones）、快捷键重映射（Keyboard Manager）、快速启动器（PowerToys Run）、批量重命名（PowerRename）、全局屏幕取色（Color Picker）、屏幕文本识别（Text Extractor / OCR）等 30 余项开箱即用的系统辅助功能。

**[官方发行页](https://github.com/microsoft/PowerToys/releases/tag/v0.102.3101) · [上游说明](source/README.md) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 系统工具 |
| 收藏版本 | v0.102.3101（2026-11-06 发布） |
| 运行环境 | Windows 11 或 Windows 10（v2004 / 内部版本 19041 及以上），支持 x64 与 ARM64 架构 |
| 典型组件 | FancyZones、PowerToys Run、Text Extractor、PowerRename、Keyboard Manager、Color Picker、Awake 等 30+ 实用工具 |
| 许可证 | [MIT 原文](source/LICENSE)（Microsoft 开源许可） |
| 验证程度 | 文档与源码快照核验；未安装实测 |

## 第一阶段：环境自检与首次使用

### 1. 系统版本与架构自检

在 PowerShell 或命令提示符中检查系统版本与 CPU 架构：

```powershell
[System.Environment]::OSVersion.Version
[System.Environment]::Is64BitOperatingSystem
$env:PROCESSOR_ARCHITECTURE
```

要求 Windows 10 19041+ 或 Windows 11，支持 AMD64 (x64) 或 ARM64。

### 2. 官方推荐安装方式

PowerToys 属于桌面图形化实用程序，优先推荐通过 Windows 官方包管理器或官方 Release 安装包安装：

- **通过 WinGet 安装（推荐当前用户作用域）**：

  ```powershell
  winget install Microsoft.PowerToys -s winget
  ```

- **全系统（所有用户）安装**：

  ```powershell
  winget install --scope machine Microsoft.PowerToys -s winget
  ```

- **官方 GitHub Releases 安装包**：
  前往 [v0.102.3101 发行说明页](https://github.com/microsoft/PowerToys/releases/tag/v0.102.3101) 的 Assets 列表下载：
  - x64 架构：`PowerToysUserSetup-0.102.3101.0-x64.exe`
  - ARM64 架构：`PowerToysUserSetup-0.102.3101.0-arm64.exe`

### 3. 首次启动与界面自检

PowerToys 是系统后台托盘应用，不包含类似 CLI 工具的 `doctor` 诊断命令：

1. 安装完成后，在“开始”菜单搜索并启动 **PowerToys**。
2. 检查任务栏右下角系统通知区域（托盘），应出现 PowerToys 图标。
3. 双击托盘图标打开“常规”设置面板，在“常规”选项卡中可查看当前运行版本号（如 `v0.102.3101.0`）、开机自启动设置以及管理员权限运行模式（以管理员身份运行可使热键作用于特权窗口）。

## 第二阶段：核心工作流

### 常用组件最短上手路径

各功能均有默认全局快捷键，可直接在日常办公中使用：

| 功能模块 | 默认快捷键 / 操作 | 核心用途 |
| :--- | :--- | :--- |
| **PowerToys Run** | `Alt + 空格` | 全局快速启动器，支持算式运算、应用检索、单位换算、系统命令等 |
| **FancyZones** | 按住 `Shift` 拖拽窗口 / `Win + Shift + \`` | 多显示器/超宽屏窗口高级分区排布 |
| **Text Extractor** | `Win + Shift + T` | 屏幕任意区域文字即时框选与 OCR 识别（自动复制到剪贴板） |
| **Color Picker** | `Win + Shift + C` | 全局屏幕取色，显示 HEX/RGB 代码并进入调色历史板 |
| **PowerRename** | 选中文件右键菜单 -> **PowerRename** | 正则/批量文件智能重命名与即时预览 |
| **Always on Top** | `Win + Ctrl + T` | 将当前窗口锁定置顶（再次按下取消置顶） |
| **Awake** | 托盘图标控制 | 临时阻止计算机进入睡眠，保持屏幕常亮 |
| **Paste as Plain Text** | `Win + Ctrl + Alt + V` | 无格式纯文本粘贴（高级粘贴组件内可选） |

### 组件开关与资源控制

- 在 PowerToys 设置主界面左侧列表中，所有 30 余项工具均支持单独开启或禁用。
- 对于不需要的辅助功能，建议在设置中将其关闭，以节省系统后台钩子开销与内存占用。

### 可选：从源码编译（开发者）

日常使用无需编译源码；若需基于本次收录的快照源码二次开发：

1. **构建依赖**：
   - Visual Studio 2022（需安装“使用 C++ 的桌面开发”、“通用 Windows 平台开发”和“.NET 桌面开发”工作负载）
   - Windows 11 SDK (10.0.22621.0 或更新)
   - .NET 8.0+ SDK
2. **构建工程**：
   在源码目录执行 `PowerToys.slnx` 或：
   ```powershell
   msbuild PowerToys.sln /p:Configuration=Release /p:Platform=x64
   ```
   详细开发说明请参考 [doc/devdocs](source/doc/devdocs)。

### 常见故障、更新与卸载

| 现象 | 排查与解决方法 |
| :--- | :--- |
| 快捷键在某些软件（如任务管理器）中无效 | 需在 PowerToys 设置中开启“以管理员身份运行”或启用“在启动时始终以管理员身份运行” |
| 快捷键被其他软件占用 | 在各模块设置面板中将快捷键修改为其他组合键 |
| PowerToys Run 搜索卡顿或异常 | 在 PowerToys Run 设置中检查已启用的插件，禁用不需要的第三方插件或索引项 |
| 生成诊断日志排查故障 | 在“常规”设置面板点击“报告错误”或“导出诊断日志”，将打包日志用于故障分析 |

- **软件更新**：
  若通过 WinGet 安装，在终端运行：
  ```powershell
  winget upgrade Microsoft.PowerToys
  ```
  亦可在设置面板中点击“检查更新”。更新操作离开固定快照版本，收藏库记录保持独立。
- **软件卸载**：
  在 Windows“设置” -> “应用” -> “安装的应用”中找到 Microsoft PowerToys 选择“卸载”；或通过 WinGet 执行：
  ```powershell
  winget uninstall Microsoft.PowerToys
  ```

## 源码与依据

[source/](source/) 完整归档了项目上游 `v0.102.3101` 对应提交（`e84973c4f3724eeedd34d836559dac32734c3e22`）的代码与配置；中文指南依据官方英文文档与发布说明提炼整理。

依据来源：
- [上游 v0.102.3101 提交 README](https://github.com/microsoft/PowerToys/blob/e84973c4f3724eeedd34d836559dac32734c3e22/README.md)
- [PowerToys 官方 Microsoft Learn 文档](https://learn.microsoft.com/windows/powertoys/)
- [v0.102.3101 Release Notes](https://github.com/microsoft/PowerToys/releases/tag/v0.102.3101)
