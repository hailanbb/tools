# LocalSend · 跨平台局域网文件传输

> 🔗 **原项目 GitHub 地址**：[localsend/localsend](https://github.com/localsend/localsend)

在同一本地网络中，让电脑和手机互传文件及文字消息，无需互联网连接。适合把手机照片传到 Windows 电脑、在不同系统间传文档，以及没有外网时交换资料。跨互联网远程传输不属于这里的使用场景。

**[官方下载](https://localsend.org/download) · [正式版发行页](https://github.com/localsend/localsend/releases/tag/v1.18.2) · [来源与快照](UPSTREAM.md) · [返回工具索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 文件传输 |
| 平台 | Windows、macOS、Linux、Android、iOS、Fire OS |
| 收藏版本 | v1.18.2（2026-08-21 发布；2026-09-09 核验） |
| 授权 | 上游 Apache-2.0，见[原始许可证](source/LICENSE) |
| 保存方式 | 固定提交源码快照；Flutter 子模块未展开 |
| 验证程度 | 已核验官方文档、版本及源码文件；未安装实测、未编译 |

## 第一阶段：环境自检与首次使用

### 1. 选择安装方式

两端都安装 LocalSend。普通使用不需要 Flutter、Rust 或 Git，也不需要注册账户或配置 Token。

| 设备 | 建议入口 |
| :--- | :--- |
| Windows | [官方发行页](https://github.com/localsend/localsend/releases/tag/v1.18.2)中的 EXE 安装版或 Portable ZIP；也可从官网进入 Winget 等渠道 |
| macOS / iOS | 从[官网](https://localsend.org/download)进入 App Store；macOS 也有 DMG |
| Android | 官网列出的 Google Play、F-Droid，或官方发行页的 APK |
| Linux | 官网列出的发行渠道；按系统选择对应包格式 |
| Fire OS | 官网列出的 Amazon 应用商店入口 |

下载页会随上游更新；想使用本次收藏版本请打开固定的 v1.18.2 发行页。上游建议通过商店或包管理器获取更新，因为应用本身没有自动更新功能。平台兼容性以[该版本英文说明](https://github.com/localsend/localsend/blob/af0416be50770a97760f7070684bc667b759a15c/README.md#download)为依据：Windows 10+、Android 5.0+、iOS 12.0+、macOS 11+；具体安装包仍需匹配设备架构。

### 2. 检查网络与设备

1. 两端连接同一可互通的本地网络，并打开 LocalSend。
2. 查看接收端显示的设备名称，确认发送端能发现它。
3. 如果系统提示访问本地网络，理解用途后授予相应权限。
4. 先传一个小文件，核对接收文件是否可打开，再传大批量资料。

这个桌面应用没有需要套用的 `doctor` 初始化流程。以下排障只在发现异常时使用，收藏技能不会替你改变防火墙或路由器设置。

## 第二阶段：核心工作流

### 发送文件或文字

1. 在发送端打开“发送”，选择文件、文件夹或文字等对应内容。
2. 在附近设备列表中选择接收端，核对设备名。
3. 在接收端确认接收，等待传输完成。
4. 在接收端查看保存位置并打开文件，确认结果。

界面文字可能因平台与语言略有不同；以当前安装版本为准。传输使用 HTTPS；此处不建议为提速关闭加密。

### 找不到设备或速度慢

| 现象 | 检查方式 |
| :--- | :--- |
| 两端无法互相发现 | 检查是否处于同一网络，访客 Wi-Fi 或 AP 隔离可能阻止设备互通 |
| Windows 无法接收 | 核对当前网络可信程度和 LocalSend 的防火墙许可；官方说明使用 TCP/UDP 53317 入站通信 |
| iPhone / Mac 无法发现 | 检查系统隐私设置中的“本地网络”权限 |
| 大文件速度慢 | 优先尝试信号更好、较少拥塞的 5 GHz 网络，并保持设备唤醒 |

只有在了解影响后再调整网络权限；公司或公共网络应先联系管理员。更多信息见[固定版本排障说明](https://github.com/localsend/localsend/blob/af0416be50770a97760f7070684bc667b759a15c/README.md#troubleshooting)。

### 便携模式与托盘启动（Windows，可选）

在可执行文件旁创建空的 `settings.json` 可启用便携配置。已有同名文件时保留内容，不覆盖。

```text
localsend_app.exe --hidden
```

这会隐藏主窗口，仅保留托盘图标。该参数属于图形应用，不代表此版本提供完整文件传输 CLI。依据：[v1.18.2 设置说明](https://github.com/localsend/localsend/blob/af0416be50770a97760f7070684bc667b759a15c/README.md#setup)。

### 更新与卸载

- 商店或包管理器安装：通过原渠道更新；手动安装：从官方发行页下载匹配平台的新版本。
- Windows 安装版：通过系统“已安装的应用”卸载；其他平台通过各自系统或原包管理器卸载。
- 便携版：退出后可移除应用所在文件夹；先确认其中没有要保留的接收文件或配置。
- 收藏库更新是独立动作：要求“更新 tools 中的 LocalSend”才会刷新源码及指南，不会更新你设备上的应用。

## 开发者：源码快照与构建

[source/](source/) 保存了固定提交的普通 Git 跟踪文件，保留原文及许可。`support/submodules/flutter` 未展开，因此不是完整离线构建包；详见[子模块记录](UPSTREAM.md)。普通用户直接使用安装包即可。

源码构建建议从[上游固定提交](https://github.com/localsend/localsend/tree/af0416be50770a97760f7070684bc667b759a15c)开始，按[原始构建指南](source/README.md)准备 Flutter 和 Rust。该版本 [.fvmrc](source/.fvmrc) 指定 Flutter `3.41.9`；从上游源码根目录进入 app 后：

```shell
cd app
flutter pub get
flutter run
```

依赖下载仍需网络，平台构建环境还需满足 Flutter 的要求。本收藏未运行这些构建命令。

## 来源

中文指南整理参考[上游中文原文](source/support/readme/README_ZH.md)，并与[同版本英文原文](source/README.md)核对。原文文件保持原样，因此其中以 `/` 开头的链接仍按上游仓库布局编写；在线阅读原始文档可打开[固定版本中文页](https://github.com/localsend/localsend/blob/af0416be50770a97760f7070684bc667b759a15c/support/readme/README_ZH.md)。
