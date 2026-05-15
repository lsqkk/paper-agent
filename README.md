<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://capsule-render.vercel.app/api?type=waving&height=200&color=0:1a1a2e,50:16213e,100:0f3460&text=Paper%20Agent&fontAlignY=35&fontSize=60&desc=Academic%20Writing%20Workflow%20Template&descAlignY=55&descSize=18&fontColor=e0e0e0">
  <img alt="Paper Agent banner" src="https://capsule-render.vercel.app/api?type=waving&height=200&color=0:1a1a2e,50:16213e,100:0f3460&text=Paper%20Agent&fontAlignY=35&fontSize=60&desc=Academic%20Writing%20Workflow%20Template&descAlignY=55&descSize=18&fontColor=1a1a2e">
</picture>

<p align="center">
  <b>🤖 AI驱动的全自动学术写作工作流模板</b><br>
  <i>专为 Claude Code 设计，6 阶段管线：任务解析 → 深度搜索 → 规范写作 → 自动配图 → 审校迭代 → 导出 Word</i>
</p>

<p align="center">
  <a href="README.en.md"><img alt="English version" src="https://img.shields.io/badge/Read%20in-English-blue?style=flat-square"></a>
  <img alt="GitHub" src="https://img.shields.io/badge/license-MIT-blue?style=flat-square">
  <img alt="Claude Code" src="https://img.shields.io/badge/Claude%20Code-Ready-8A2BE2?style=flat-square">
  <img alt="Workflow" src="https://img.shields.io/badge/workflow-6%20stages-success?style=flat-square">
  <img alt="Language" src="https://img.shields.io/badge/language-%E4%B8%AD%E6%96%87%20%7C%20English-orange?style=flat-square">
  <img alt="Platform" src="https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey?style=flat-square">
</p>

---

## 📋 项目简介

**Paper Agent** 是一个面向 Claude Code 的结构化学术写作工作流模板。它将一份简单的作业要求自动转化为格式规范的学术报告，涵盖从需求分析到最终文档导出的全流程。

只需编写 `任务要求.md`，启动 Claude，即可获得包含完整逻辑链条、参考文献、技术示意图和格式排版的最终报告。

### ✨ 核心能力

| 能力 | 说明 |
|------|------|
| 🧠 **全自动管线** | 6 阶段流水线，从需求解析到 Word 导出无需人工干预 |
| 🔍 **深度信息搜集** | 自动执行 20+ 条高质量联网搜索，覆盖学术数据库与技术文档 |
| ✍️ **规范写作引擎** | 6 项严格文风规范，杜绝"AI腔"——禁用分点标题、比喻说教、单调句式 |
| 🎨 **SVG 智能配图** | 自动识别插图位置，生成统一色系的技术示意图（流程图、架构图、时间线等） |
| 🔬 **审稿迭代机制** | 扮演严厉审稿人进行逻辑/文风/事实三方面审查，支持多轮修订 |
| 📄 **一键 Word 导出** | 内置学术模板导出 `.docx`，支持自定义主题和模板 |

---

## 🏗️ 工作流架构

```
┌─────────────────────────────────────────────────────────────────────┐
│                     Paper Agent 6阶段流水线                            │
└─────────────────────────────────────────────────────────────────────┘

  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
  │  阶段一  │───▶│  阶段二  │───▶│  阶段三  │───▶│  阶段四  │───▶│  阶段五  │───▶│  阶段六  │
  │  任务解析│    │  深度信息│    │  规范写作│    │  图片规划│    │  审稿与  │    │  导出    │
  │  与方案  │    │  搜集    │    │          │    │  与处理  │    │  修改    │    │  Word    │
  └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘
       │               │               │               │               │               │
       │  用户确认     │  自动执行     │  自动执行     │  自动绘制     │  用户反馈     │  一键导出    │
       │  大纲后继续   │  无需等待     │  无需等待     │  /用户提供    │  循环迭代     │  最终输出    │
       ▼               ▼               ▼               ▼               ▼               ▼
    ✅ 人工检查点    🤖 Agent      ✍️ Agent        🎨 Agent/用户   🔬 Agent        📄 md2word
```

---

## 🔬 各阶段详解

### 阶段一：任务解析与方案确认

读取 `任务要求.md`，提取全部作业参数（主题、字数、格式、参考文献等）。进行 3-5 次初步联网搜索，设计包含核心论点、目录结构（二级标题）、展开策略和资料搜需清单的完整写作方案。输出 `初步大纲.md`。

> ⏸️ **检查点：** 必须等待用户确认后方可进入下一阶段。

### 阶段二：深度信息搜集

基于大纲关键词，执行 20+ 条高质量联网搜索，优先来自 arXiv、Google Scholar、IEEE Xplore 等学术数据库和官方技术文档。每条结果标注来源链接、发布日期、核心内容摘录及对应大纲章节。输出 `collected_info.md`。

> ▶️ **自动进入** 阶段三。

### 阶段三：正式写作

撰写完整报告 `report.md`，长度为任务要求字数的 1.5 倍。写作过程严格遵循 6 项文风规范：

- 🚫 **禁用分点小标题** —— 全部采用连贯自然段落
- 🌊 **细致全面** —— 阐释概念来龙去脉，杜绝强行拔高句式
- 📖 **首注英文** —— 关键概念首次出现标注原文与缩写
- 🚫 **拒绝说教** —— 禁止比喻修辞与"不是……而是……"式否定论证
- 📏 **标题简洁** —— 禁止冒号和破折号
- 🎵 **句式错落** —— 主动混合短、中、长句，打破"AI腔"单调节奏

> ▶️ **自动进入** 阶段四。

### 阶段四：图片规划与处理

通读报告，标记 3-5 处需要配图的位置，按类型分别处理：
- **技术示意图**（流程图、架构图、时间线）—— 自动绘制 SVG，存放至 `img/` 目录
- **真实影像**（照片、截图）—— 在 `img.md` 中描述需求，由用户提供

每张 SVG 使用统一色系，宽度 800-1000px，全中文标注。

> ▶️ 全为 SVG 则**自动进入**阶段五；如需用户提供图片则等待。

### 阶段五：苛刻审稿与修改

扮演严厉的毕业论文评审老师，对报告进行三方面批判性审查：

1. **逻辑缺陷** —— 论点跳跃、因果关系弱、概念偷换
2. **文风违规** —— 检查是否残留禁止格式、说教句、标题冒号
3. **事实与引用错误** —— 数据过时、引用张冠李戴、结论过度夸大

输出 `review.md`（含每条意见的修改标记）和 `report_revised.md`。

> 🔄 **迭代循环：** 用户反馈 → 再审 → 再改 → 直至回复"定稿"。

### 阶段六：导出 Word 文档

使用内置的 [md2word](https://github.com/lsqkk/md2word) 工具，以学术论文主题导出最终 `.docx` 文件。输出路径默认为项目根目录。导出后总结总字数、图片数量和参考文献条数。

> ⚠️ `md2word` 需单独安装：`git clone https://github.com/lsqkk/md2word`，详情见其项目说明。

> ✅ **完成。**

---

## 🚀 快速开始

### 前置条件

- 安装 [Claude Code](https://claude.ai/code)
- （选装）[md2word](https://github.com/lsqkk/md2word) —— 阶段六 Word 导出需要

### 一键启动

```bash
# 克隆模板
git clone https://github.com/lsqkk/paper-agent.git 我的论文

# 进入目录
cd 我的论文

# 编辑作业要求（打开 任务要求.md 填写作业参数）
# 然后启动 Claude Code
claude

# 接下来 Claude 会自动读取工作流，引导你进入阶段一
```

### 编辑 `任务要求.md`

```markdown
《课程名称》课程总结报告
主题：课程学习心得体会、读书报告（可自行拟定标题）

基本要求：
1. 格式：10% （条目清楚、重点突出）
2. 规范性：20% （科技论文/技术报告全要素）
3. 字数：10% （8000字左右）
...

【给AGENT的附加信息】
课程背景、教材信息、教授信息、内容侧重点等...
```

### 使用 /plan 技能

```bash
claude
> /plan "写一篇关于机器学习的8000字课程报告"
```

Agent 会自动进行需求分析、生成大纲，并请求你的确认。

---

## 📁 模板文件结构

```
paper-agent/
├── CLAUDE.md              # ← 核心：6 阶段工作流定义（引擎）
├── 任务要求.md            # ← 输入：作业要求模板，填写后启动
├── README.md              # ← 本文件（中文说明）
├── README.en.md           # ← 英文说明
├── .gitignore             # ← 自动生成的产物过滤规则
├── .gitattributes         # ← 换行符标准化
│
├── .claude/               # ← Claude 本地配置（已 gitignore）
│   └── settings.local.json
│
├── img/                   # ← 阶段四生成的 SVG 示意图（已 gitignore）
│   └── img_01_*.svg
│
├── 初步大纲.md            # ← 阶段一产出（已 gitignore）
├── collected_info.md      # ← 阶段二产出（已 gitignore）
├── report.md              # ← 阶段三产出（已 gitignore）
├── report_revised.md      # ← 阶段五产出（已 gitignore）
├── review.md              # ← 阶段五产出（已 gitignore）
└── *.docx                 # ← 阶段六导出（已 gitignore）
```

---

## 🎯 最佳实践

| ✅ 推荐做法 | ❌ 避免 |
|-----------|--------|
| 在 `任务要求.md` 中详细描述作业参数 | 留一行话，模糊不清 |
| 明确指定字数和格式要求 | 让 Agent 猜你想要什么格式 |
| 在"附加信息"中提供课程/教材背景 | 跳过上下文，导致内容偏题 |
| 仔细审阅阶段一的大纲 | 急于确认，大纲方向偏了后面全白写 |
| 在阶段五审稿循环中如实反馈 | 不看报告就批准定稿 |
| 确保参考文献真实可查 | 让 Agent 编造文献 |

### 会话恢复

如果对话因技术问题中断，发送：

> "恢复状态"

Claude 会自动识别最后完成的阶段并从该处重新开始。

### 自定义工作流

如需修改文风规范或图片参数，直接编辑 `CLAUDE.md` 中对应阶段（阶段三 / 阶段四）的规则描述即可。

---

## 🔧 高级用法

### 多论文并行

```
paper-agent/
├── 作业1/
│   ├── 任务要求.md
│   └── ...（自动生成）
├── 作业2/
│   └── ...
└── CLAUDE.md  （共享工作流）
```

### 自定义 Word 模板

`md2word` 支持自定义 `.docx` 模板。将模板文件放入项目根目录后引用：

```bash
md2word report_revised.md -o output.docx -t 我的模板.docx
```

内置主题：`official`（公文）、`academic`（学术论文）、`tech`（技术文档）、`media`（自媒体排版）。

---

## 🧩 技术栈

| 组件 | 技术 |
|------|------|
| AI 引擎 | Claude Code（Opus / Sonnet 模型） |
| 工作流 | `CLAUDE.md` 定义的 Markdown 管线 |
| 插图 | SVG（内联手写矢量图） |
| Word 导出 | [md2word](https://github.com/lsqkk/md2word)（Markdown → docx 转换器） |
| 图床（可选） | Cloudflare R2 |

---

## 📜 开源协议

MIT —— 自由使用、修改、分享。

---

<p align="center">
  Made with ❤️ for students who'd rather spend time thinking than formatting<br>
  <sub>欢迎提交 Issue 和 PR</sub>
</p>
