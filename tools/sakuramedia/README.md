# SakuraMedia · 面向 NAS 的私人媒体库管理平台

> 🔗 **原项目 GitHub 地址**：[tinypinglite/sakuramedia](https://github.com/tinypinglite/sakuramedia)

**SakuraMedia** 是专为 NAS 与私人影视收藏用户打造的一站式媒体库管理与观影系统。系统采用多端跨平台客户端（Flutter 开发，支持 Windows、macOS、Android、iOS）与独立后端服务协同架构，集成了影片与女优订阅追踪、自动化寻找资源与入库、缩略图时间轴预览与沉浸播放、以图搜图、切片与时刻收藏、采样指纹排重以及 115 网盘与 qBittorrent 存储与下载集成能力。

**[官方发行页](https://github.com/tinypinglite/sakuramedia/releases/tag/v0.8.2) · [官方文档/Wiki](https://tinypinglite.github.io/sakuramedia/) · [后端项目](https://github.com/tinypinglite/sakuramediabe) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 媒体处理 |
| 收藏版本 | v0.8.2，2026-09-22 发布 |
| 运行环境 | 客户端支持 Windows / macOS / Android / iOS；服务端支持 Docker / Linux / 各类 NAS 系统 |
| 核心能力 | 影片与女优追踪订阅、资源检索与自动入库、内置缩略图时间轴播放器、以图搜图、文件采样指纹排重、115网盘挂载、插件化扩展 |
| 许可证 | [GPL-3.0](UPSTREAM.md) |
| 验证程度 | 文档与源码核验；未部署后端实测、未连接网盘 |

---

## 第一阶段：环境自检与首次使用

### 1. 架构说明

SakuraMedia 采用前后端分离设计：
* **服务端（Backend）**：运行在 NAS、家用服务器或软路由上（Docker 部署），负责影视资料刮削、资源搜索、下载调度（对接 qBittorrent 或 115 离线）以及媒体库元数据维护。
* **客户端（Client）**：运行在电脑（Windows / macOS）或移动设备（Android / iOS）上，提供原生级流畅的浏览、管理、缩略图时间轴观影与切片整理体验。

### 2. 服务端 Docker 部署与环境自检

在 NAS 或服务器上，请首先确认容器环境就绪：

```bash
# 验证 Docker 与 Compose 就绪状态
docker --version
docker compose version
```

编写并启动后端服务（参考官方推荐的 `docker-compose.yml` 配置）：

```yaml
services:
  sakuramediabe:
    image: tinyping/sakuramediabe:latest
    container_name: sakuramediabe
    restart: unless-stopped
    ports:
      - "8080:8080"
    volumes:
      - /path/to/config:/app/config
      - /path/to/media:/media
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Shanghai
```

启动命令：
```bash
docker compose up -d
```

### 3. 客户端获取与配对连接

1. 前往 [SakuraMedia Releases 发行页](https://github.com/tinypinglite/sakuramedia/releases/tag/v0.8.2) 下载对应系统的安装包：
   - **Windows**：`sakuramedia-windows-x64.zip` / 安装程序
   - **macOS**：`sakuramedia-macos-arm64.dmg` / `x64.dmg`
   - **Android**：`sakuramedia-android.apk`
2. 打开客户端，在首次引导界面填入 NAS 后端服务的内网或穿透访问地址（如 `http://192.168.1.100:8080`），点击连接即完成配对。

---

## 第二阶段：核心工作流

### 1. 发现、订阅与全自动入库

* **女优与影片订阅**：按番号检索影片或按姓名关注女优，将其加入订阅清单，系统持续追踪发布动态与新作。
* **自动化寻找资源与下载**：服务端根据配置的规则定时寻找最佳可用资源，自动推送至绑定的 qBittorrent 客户端或 115 网盘离线任务。
* **自动导入与重试**：下载完成后服务端自动识别文件并刮削元数据入库；若遇解析跳过或异常，可在「下载任务中心」一键触发「重新导入」。

### 2. 缩略图时间轴与沉浸观影

* **快照时间轴**：客户端内置播放器自动将视频按时间线展开生成高清缩略图，拖动进度条即可即时预览精彩画面。
* **时刻与切片收藏**：观影过程中支持一键打点保存精彩时刻（Moment）或截取片段（Clip），生成专属合集与播放列表。
* **调用外部播放器**：除内置播放器外，也支持调用 PotPlayer、IINA、VLC 等本地第三方播放器。

### 3. 媒体库健康与采样指纹排重

* **文件指纹算法**：采用针对大文件的局部特征采样算法，无需扫描整部影片体积即可秒级计算出媒体指纹，快速识别跨目录、跨存储的重复或多版本文件。
* **存储迁移**：支持在本地硬盘与 115 等远程存储之间平滑迁移媒体文件，并完整保留观看记录与切片收藏。

### 4. 插件化生态扩展

* 支持按需安装第三方数据源插件、字幕检索插件与第三方存储适配插件，保持核心系统的精简与高度可扩展性。

---

## 排障与日常维护

* **前后端版本兼容性**：v0.8.2 引入的「重新导入」等高级功能需要后端服务保持在 `v0.8.1` 及以上版本；若提示接口异常，请优先拉取最新的后端 Docker 镜像更新。
* **网络与代理问题**：刮削外部影片资料时，请确保服务端网络环境能正常连通元数据提供源。
* **卸载与清理**：
  - 客户端：直接卸载对应应用，并清理系统应用数据目录即可。
  - 服务端：执行 `docker compose down -v` 清理容器与配置卷。