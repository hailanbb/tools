# Google QR SMS Helper · 谷歌跨设备扫码转短信验证助手

> 🔗 **原项目 GitHub 地址**：[havenicec/google-qr-sms-helper](https://github.com/havenicec/google-qr-sms-helper)

基于 Chrome Extension Manifest V3 开发的浏览器扩展工具。针对在桌面浏览器上升级或验证 Google 账号时频繁出现的强制跨设备手机扫码限制（通常触发 Android GMS Constellation 硬件静默短信或国际外发短信 MO-SMS），本扩展利用官方跨设备降级机制（`idv_xdevice=1` 与非 Android 客户端状态 `[3, null, 4]`），并在整个验证链路中通过 `declarativeNetRequest` 保持一致的 `iPad Mini` 请求头与 Client Hints 伪装，一键将二维码强制验证降级回传统的“输入手机号接收 6 位短信验证码”流程。

**[官方发行页](https://github.com/havenicec/google-qr-sms-helper/releases/tag/v1.1.0) · [上游说明](source/README.md) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 系统工具 |
| 收藏版本 | v1.1.0（2026-10-26 发布） |
| 运行环境 | 支持 Manifest V3 的 Chromium 内核浏览器（Google Chrome、Microsoft Edge、Brave 等）；跨平台适用于 Windows、macOS、Linux |
| 典型功能 | DOM 原生二维码解码、全链路 iPadOS 标头伪装、MypxBd / YDtwf `[3, null, 4]` RPC 自动降级、悬浮一键触发 |
| 许可证 | [MIT 原文](source/LICENSE) |
| 验证程度 | 文档与源码快照核验；未加载至 Chrome 实测 Google 账号验证 |

## 第一阶段：环境自检与首次使用

### 1. 浏览器环境自检

确认当前使用的桌面浏览器基于 Chromium 内核且支持 Manifest V3：
- Google Chrome ≥ 88
- Microsoft Edge ≥ 88
- Brave 或其他现代 Chromium 衍生浏览器

### 2. 加载已解压扩展

1. 在浏览器地址栏输入并打开扩展管理页：
   - Chrome：`chrome://extensions/`
   - Edge：`edge://extensions/`
2. 打开页面右上角（或左下角）的 **“开发者模式”** 开关。
3. 点击 **“加载已解压的扩展程序”**（Load unpacked）。
4. 在文件选择窗口中，选择本次收录的快照目录 `tools/google-qr-sms-helper/source`。
5. 确认扩展列表中出现 **Google QR SMS Helper**，且状态为已启用。

### 3. 权限与状态检查

- 扩展依赖 `declarativeNetRequest` 权限用于修改请求头中的 User-Agent 及剥离桌面端 Client Hints（`Sec-CH-UA*`）。
- 点击“背景页 / Service Worker”查看控制台，确认后台 Service Worker 正常启动并处于激活状态。

## 第二阶段：核心工作流

### 1. 标准触发入口（推荐 Cloud Shell 路径）

根据开发者实测，从 Google Cloud Console 触发验证可生成无嵌套第三方 OAuth 跳转的标准流程令牌：

1. 登录需要验证的 Google 账号，访问 [Google Cloud Console](https://console.cloud.google.com/)。
2. 点击右上角导航栏的 **激活 Cloud Shell（`[>_]`）** 图标（或通过扩展在页面注入的辅助悬浮按钮触发）。
3. 在弹出的验证对话框中点击 **`Verify`**，系统将打开 `/v3/signin/challenge/iap/qrcode` 跨设备扫码页面。

### 2. 一键降级至短信验证

1. 在二维码页面右下角，找到扩展自动注入的悬浮控制面板。
2. 点击 **`⚡ 一键降级到短信选择框`** 按钮：
   - 扩展使用原生 `BarcodeDetector` 直接从页面 Canvas / 图像提取二维码绑定的 URL。
   - 后台 Service Worker 自动完成 MypxBd 与 YDtwf 请求交互，锁定非 Android 回退状态。
   - 页面自动刷新重定向至带有 `&idv_xdevice=1` 参数的 `uplevelingstep/selection` 路径。

### 3. 接收并填入 6 位验证码

1. 降级成功后，页面将展示单选方式列表。
2. 勾选 **Text message (SMS)** 选项，选择国家代码并输入手机号。
3. 手机接收到 Google 发送的 6 位验证码短信（形如 `G-xxxxxx`）后，填入页面输入框完成验证。

### 4. 常见故障排查与卸载

| 故障现象 | 排查与解决办法 |
| :--- | :--- |
| 点击降级无反应或提示未找到二维码 | 确保页面已完全加载完成；若处于 iframe 嵌套环境，尝试直接在新标签页打开验证 URL |
| 二维码失效或超时 | 重新刷新页面生成新二维码，再次点击降级按钮 |
| 短信接口提示不可用 | 确认代理 IP 纯净度与网络出口区域；部分高风控 IP 可能会被 Google 限制短信下发频次 |
| 无法加载扩展 | 检查是否开启了浏览器的“开发者模式”，核对 `manifest.json` 是否在所选文件夹根目录 |

- **扩展卸载**：
  在 `chrome://extensions/` 页面找到 Google QR SMS Helper，点击“移除”并确认即可完全删除扩展，DNR 请求头重写规则将随之立即失效。

## 源码与依据

[source/](source/) 完整归档了项目上游 `v1.1.0`（提交 `c91ce2afc73add167d312fb379d551c56c421b9d`）的全部代码与配置。中文指南基于官方说明与扩展实现代码提炼整理。

依据来源：
- [上游 v1.1.0 提交 README](https://github.com/havenicec/google-qr-sms-helper/blob/c91ce2afc73add167d312fb379d551c56c421b9d/README.md)
- [扩展配置文件 manifest.json](source/manifest.json)
- [核心后台脚本 background.js](source/background.js)
