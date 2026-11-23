# BilldDesk · 跨平台 WebRTC 远程桌面控制系统

> 🔗 **原项目 GitHub 地址**：[galaxy-s10/billd-desk](https://github.com/galaxy-s10/billd-desk)

基于 Vue 3 + WebRTC + Node.js + Electron / Flutter 构建的现代化跨平台开源远程桌面与游戏串流系统。实现了类似 ToDesk、向日葵、RustDesk 等桌面控制软件的功能架构，支持 Web 浏览器、桌面客户端（Windows/macOS/Linux）与移动端（Android）之间的低延迟画面串流与键鼠交互，实测支持最高 2K 120FPS 硬件加速流畅串流。

**[项目主页](https://github.com/galaxy-s10/billd-desk) · [在线演示](https://desk.hsslive.cn) · [开源版说明](source/README_OpenSource.md) · [上游说明](source/README.md) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 系统工具 |
| 收藏版本 | main 分支快照（Commit: `9212de860f0d`，2026-11-22 提交） |
| 运行环境 | Node.js 18+、pnpm；客户端支持 Windows、macOS、Linux、Android 与主流 Chromium/Firefox 浏览器 |
| 核心架构 | Vue 3 + Vite + TypeScript + WebRTC + Electron |
| 串流特性 | 支持 1080P/2K 60~120 FPS 串流、GPU 硬件编解码加速、P2P 直连与中继穿透 |
| 许可证 | [MIT 原文](source/LICENSE.txt) |
| 验证程度 | 文档与源码快照核验；未部署信令服务器与客户端实测远程连接 |

## 第一阶段：环境自检与首次使用

### 1. 开发与构建环境自检

确保开发机已安装推荐版本的 Node.js 与 pnpm：

```bash
node -v   # 要求 >= 18.0.0
pnpm -v   # 建议 >= 8.0.0
```

### 2. 依赖安装

进入本次收录的快照源码目录：

```bash
cd tools/billd-desk/source
pnpm install
```

### 3. 本地启动与调试

- **启动 Web 网页端**：
  ```bash
  pnpm dev
  ```
  控制台将输出本地开发服务器地址（默认 `http://localhost:3300/`），可通过现代浏览器直接访问 Web 控制端。
- **启动 Electron 桌面客户端**：
  ```bash
  pnpm dev:electron
  ```
  将同时启动 Vite 开发服务器与 Electron 主进程窗口。

## 第二阶段：核心工作流

### 1. 跨端远程控制模式

BilldDesk 支持灵活的多端互控拓扑：

| 控制端（主控） | 被控端 | 交互模式 |
| :--- | :--- | :--- |
| **Web 浏览器** | 电脑桌面端 (Windows/Mac) | 完整画面查看 + 鼠标点击/键盘映射控制 |
| **电脑客户端** | 电脑桌面端 (Windows/Mac) | 低延迟全屏游戏串流 + 快捷键穿透 |
| **Web / 电脑端** | Android 安卓端 | 画面查看与无障碍权限远程触控 |
| **Android 客户端** | 电脑桌面端 | 触屏手势模拟鼠标/虚拟键盘输入 |

### 2. 画质与硬件加速配置

- **画质档位**：支持 1080P 60FPS、2K 60FPS 及 2K 120FPS 动态切换。
- **硬件加速**：在设置界面中可开启 GPU 硬件加速编解码（支持 NVENC / QuickSync 等硬件加速方案），降低 CPU 占用并压缩端到端传输延迟至毫秒级。

### 3. 自建信令与 NAT 穿透支持

WebRTC 通信依赖信令交换与 STUN/TURN 穿透：
1. **信令服务**：前端默认连接官方演示或自定义 Node.js WebSocket 信令服务。
2. **NAT 穿透**：局域网内自动建立 P2P 直连；跨公网环境若对称型 NAT 无法直接穿透打洞，需配置自建的 TURN 中继服务器以保障连通率。

### 4. 客户端打包与构建

针对目标操作系统打包分发安装包：

```bash
# 构建 Windows 安装包 (.exe)
pnpm build:win

# 构建 macOS 安装包 (.dmg)
pnpm build:mac

# 构建 Linux 安装包 (.AppImage / .deb)
pnpm build:linux
```

输出文件将保存在 `dist_electron/` 目录下。

### 5. 常见故障排查

| 现象 | 排查与解决办法 |
| :--- | :--- |
| 被控端无法分享屏幕 | 检查操作系统屏幕录制权限（macOS 需在“系统偏好设置 -> 隐私与安全性 -> 屏幕录制”中授权应用） |
| WebRTC 状态一直停在 connecting | 检查信令服务器 WebSocket 是否可达，确认公网 STUN/TURN 配置是否正常生效 |
| 鼠标点击位置发生偏移 | 检查被控端系统缩放倍率（DPI Scaling，如 125%/150%），确保客户端已正确同步画布比例 |

## 源码与依据

[source/](source/) 完整归档了项目上游 `main` 分支最新提交（`9212de860f0d8edba6b8bd0e60c564b037e3ab35`）的全部代码与配置。中文指南基于官方说明与前端工程代码提炼整理。

依据来源：
- [上游 commit README](https://github.com/galaxy-s10/billd-desk/blob/9212de860f0d8edba6b8bd0e60c564b037e3ab35/README.md)
- [开源版使用说明 README_OpenSource.md](source/README_OpenSource.md)
- [前端工程配置 package.json](source/package.json)
