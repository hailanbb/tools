# KiT · 基于 Diffusion Transformer 的金融 K 线时序预测大模型

> 🔗 **原项目 GitHub 地址**：[Luciferbobo/KiT](https://github.com/Luciferbobo/KiT)

KiT（K-line Diffusion Transformer）是针对金融 K 线（Candlestick / OHLCV）多周期走势预测的基础大模型（Foundation Model）。基于扩散 Transformer（DiT）与流匹配（Flow Matching）架构构建，预训练数据涵盖美股、A 股、加密货币等多市场数十亿根 K 线，原生覆盖从 1 分钟到 1 天（1m、5m、15m、30m、1h、2h、1d）共 7 种时间粒度。模型将多周期 K 线编码为 5 维对数比率状态序列，通过条件路径生成实现收益率与波动率预测，并配备了完整的离线评测与量化回测系统。

> ⚠️ **合规提示**：本项目属于学术研究与量化技术探索成果，预测输出不构成任何投资建议与财务指导。

**[项目主页](https://github.com/Luciferbobo/KiT) · [在线演示](https://trading.etfnav.org/?lang=en) · [论文 (arXiv:2609.34507)](https://arxiv.org/abs/2609.34507) · [上游说明](source/README.md) · [来源记录](UPSTREAM.md) · [返回索引](../../README.md)**

| 项目 | 内容 |
| :--- | :--- |
| 分类 | 量化金融 |
| 收藏版本 | main 分支快照（Commit: `a9bf4a30e370`，2026-11-20 提交） |
| 运行环境 | Python 3.10+、PyTorch 2.1+、CUDA 12+；支持 Linux 与 Windows |
| 核心架构 | Diffusion Transformer (DiT) + AdaLN 调制 + Flow Matching 条件路径生成 |
| 模型规格 | 包含 30M (`dit_30m.yaml`)、100M (`dit_100m.yaml`) 与 300M / 284M (`dit_300m.yaml`) 架构 |
| 许可证 | [AGPL-3.0 原文](source/LICENSE) |
| 验证程度 | 文档与源码快照核验；未下载模型权重实测、未执行量化回测 |

## 第一阶段：环境自检与首次使用

### 1. 环境自检

推荐在拥有 NVIDIA GPU（显存建议 ≥ 16GB）的独立 Python 虚拟环境中运行：

```bash
# 确认 Python 版本 (>=3.10) 与 CUDA 支持
python -c "import torch; print('CUDA available:', torch.cuda.is_available(), 'Version:', torch.version.cuda)"
```

### 2. 安装项目依赖

克隆或进入本次收录的快照源码目录安装依赖：

```bash
cd tools/kit/source
pip install -r requirements.txt
```

### 3. 获取权重与演示数据

1. **模型权重**：
   按上游 [ckpt/README.md](source/ckpt/README.md) 说明从官方 Google Drive 或百度网盘链接下载 `step_market_284M.pt`，并放置于 `ckpt/` 目录。
2. **测试数据**：
   从官方共享盘下载 100 只股票演示数据集（或按 [data/README.md](source/data/README.md) 准备股票历史 OHLCV 字典与基本面日历信息），解压后放置于 `data/` 目录。

## 第二阶段：核心工作流

### 1. 单股单周期预测与可视化

指定股票代码、时间粒度以及历史窗口截止时间锚点（Anchor），模型将读取历史 $L_c$ 根 K 线并预测未来 $L_h$ 根走势：

```bash
# 默认配置预测
python eval/infer_for_pred.py

# 指定标的与周期（如紫金矿业 5 分钟级别、宁德时代 30 分钟级别）
python eval/infer_for_pred.py --case 601899.SH,5m,2026-03-04 --case 300750.SZ,30m,"2026-03-10 11:30"
```

各粒度固定窗口对照：

| 时间粒度 | 1m | 5m | 15m | 30m | 1h | 2h | 1d |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 输入历史 $L_c$ (根) | 1200 | 960 | 800 | 640 | 400 | 360 | 250 |
| 预测步长 $L_h$ (根) | 120 | 96 | 64 | 40 | 20 | 20 | 20 |

输出将自动绘制走势图并保存于 `results/infer_for_pred/`，包含历史末端蜡烛图、真实未来走势与多条生成路径置信区间（q05~q95 / q25~q75）。

### 2. 验证集批量推理与指标评测

对验证区间全部 100 只标的与 7 种周期执行全量推断并计算统计指标（收益率 return、波动率 vol、累计价格收益 price）：

```bash
python eval/infer_for_eval.py
python eval/cal_metrics.py
```

评测细节请参考同版本文档 [docs/EVALUATION.md](source/docs/EVALUATION.md)。

### 3. 量化策略回测

在全量验证集推断完成后，可调用内置的多周期量化回测模块：

```bash
python eval/backtest.py --top 20 --slip 5 --scales 5m,15m,1h
```

- **选股规则**：各时间锚点根据生成路径收益率均值进行全市场截面排序，等权持有 Top N 股票。
- **交易风控**：内置 A 股涨跌停限制（首日/常规涨跌停不可买卖处理）、T+1 交易制度、双边印花税与佣金滑点模拟。
- **基准比对**：自动计算等权均值、中位数及 CSI500 中证 500 指数基准走势，结果图表与汇总数据写入 `results/backtest_results/`。

### 4. 常见问题排障

| 现象 | 排查与解决办法 |
| :--- | :--- |
| `FileNotFoundError: ckpt/step_market_284M.pt` | 确认权重文件已正确下载并放置于 `ckpt/` 目录，路径大小写保持一致 |
| CUDA Out of Memory (OOM) | 在 `configs/dit_*.yaml` 中调小批处理大小（Batch Size）或采样路径数 $K$ |
| 日历数据或股票代码格式报错 | 标的代码需包含交易所后缀（如 `.SH`、`.SZ`），且交易日历须覆盖历史到预测期 |

## 源码与依据

[source/](source/) 完整归档了项目上游 `main` 分支最新提交（`a9bf4a30e37076c4fb59a1461a5d5dfbd51a3294`）的全部代码、模型结构定义与评测回测脚本。中文指南基于官方说明与源码逻辑整理。

依据来源：
- [上游 commit README](https://github.com/Luciferbobo/KiT/blob/a9bf4a30e37076c4fb59a1461a5d5dfbd51a3294/README.md)
- [KiT 预印本论文 (arXiv:2609.34507)](https://arxiv.org/abs/2609.34507)
- [模型定义 kit_v1/model/](source/kit_v1/model/) 与 [回测评测 eval/](source/eval/)
