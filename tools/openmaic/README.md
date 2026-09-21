# OpenMAIC · 多智能体互动课堂

> 🔗 **原项目 GitHub 地址**：[THU-MAIC/OpenMAIC](https://github.com/THU-MAIC/OpenMAIC)

**OpenMAIC**（Open Multi-Agent Interactive Classroom）是由清华大学 THU-MAIC 团队开源的多智能体沉浸式互动教学与自学平台。它能将任意主题、知识大纲或课件文档（PDF、Office、Markdown）一键转化为包含演示幻灯片、即时测验、3D 模拟实验和项目制学习（PBL）活动的沉浸式课堂。课堂内由 AI 教师、助教与 AI 同学共同协同授课、板书绘图，并支持学生通过自然语言语音/文字展开即时研讨。

**[官方发行页](https://github.com/THU-MAIC/OpenMAIC/releases/tag/v1.0.3) · [在线体验 Demo](https://open.maic.chat/) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 教育学习 |
| 收藏版本 | v1.0.3，2026-09-15 发布 |
| 运行环境 | Node.js 20+ (pnpm)、Docker / Docker Compose；支持 Windows / macOS / Linux |
| 核心能力 | 文档一键转课、多智能体协作授课、白板与3D交互实验、PBL项目制探究、课程MP4导出、Agent 工作台集成 |
| 许可证 | [MIT](UPSTREAM.md) |
| 验证程度 | 文档与源码核验；未部署实测、未启动服务 |

---

## 第一阶段：环境自检与首次使用

### 1. 运行环境自检

在部署或本地启动 OpenMAIC 前，请在终端中执行以下命令检查底层环境状态：

```powershell
# 1. 验证 Node.js 版本 (推荐 Node.js 20+)
node -v

# 2. 验证 pnpm 包管理器
pnpm -v

# 3. 验证 Docker 与 Docker Compose (若采用容器化部署)
docker --version
docker compose version
```

### 2. 快速部署方式

官方支持两种主流运行路径：

#### 路径 A：Docker Compose 容器化部署（推荐）

1. 克隆代码并进入项目目录：
   ```bash
   git clone https://github.com/THU-MAIC/OpenMAIC.git
   cd OpenMAIC
   ```
2. 复制环境配置模板：
   ```bash
   cp .env.example .env
   ```
3. 在 `.env` 中配置至少一个大模型 API Key（支持 OpenAI、DeepSeek、Anthropic、智谱 GLM、通义千问等）。
4. 启动容器集群：
   ```bash
   docker compose up -d
   ```
5. 启动完成后，在浏览器访问 `http://localhost:3000` 即可进入课堂主页。

#### 路径 B：本地 Node.js 源码启动

1. 安装依赖：
   ```bash
   pnpm install
   ```
2. 配置环境变量：
   ```bash
   cp .env.example .env.local
   # 编辑 .env.local 填入模型 API Key
   ```
3. 运行开发服务器：
   ```bash
   pnpm dev
   ```

---

## 第二阶段：核心工作流

### 1. 课堂创建与内容解析

* **主题输入**：在首页输入想要学习或备课的知识点主题（如“量子纠缠的基本原理”），设定目标学段与教学风格。
* **文档驱动生成**：上传 PDF 讲义、Word 讲稿或 Markdown 论文，系统自动解析核心知识点并抽取结构化教学大纲。
* **大纲微调**：在生成完整课件前，可手动增删章节、调整授课节奏与测验重点。

### 2. 沉浸式多智能体协同授课

* **分角色多智能体**：
  - **AI 讲师**：负责核心知识框架梳理、步进式推演与白板板书绘制。
  - **AI 同学**：模拟课堂发问、提出典型易错点与补充思考，带动研讨氛围。
  - **真人参与**：支持通过麦克风语音输入或即时文字打字插话提问，智能体即时暂停并解答。
* **深度交互模式**：支持 3D 几何与物理可视化、代码在线调试运行、动态思维导图互动。

### 3. 编辑、导出与生态集成

* **MAIC Editor 专业编辑器**：课程生成后，可在图形化编辑器中自由拖拽、旋转、框选幻灯片元素，或通过自然语言指令（“Edit with AI”）由模型批量应用 JSON Patch 调整版式。
* **多样化导出**：
  - **离线 HTML 包**：全量保留交互能力的单文件/离线包。
  - **MP4 课程视频**：内置无头 Chromium 渲染服务，将整堂课的演示、板书与多角色语音直接合成为高清视频。
* **Agent 工作台插件**：内置 OpenMAIC 专属 Skill，支持在 [OpenClaw](https://github.com/openclaw/openclaw)、Codex 等智能体工作流中调用，直接在 Slack、飞书或 Telegram 频道中一键触发课程生成。

---

## 排障与日常维护

* **模型 API 与网络连接**：若出现生成超时或错误，请检查 `.env` 中的 `OPENAI_API_BASE` / `DEEPSEEK_API_BASE` 等端点是否可直连，网络代理端口是否畅通。
* **渲染服务资源配置**：导出 MP4 视频需要依赖 Chromium 无头渲染服务，建议为主机预留足够的内存与 CPU 资源（建议 4 核 8GB 以上）。
* **更新与升级**：
  ```bash
  git pull origin main
  pnpm install
  pnpm build
  ```
* **卸载与清理**：
  - Docker 模式：运行 `docker compose down -v` 清理容器与数据卷。
  - 源码模式：直接删除项目根目录及关联的 `.env` 配置文件即可。