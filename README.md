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
  <img alt="Architecture" src="https://img.shields.io/badge/architecture-modular-green?style=flat-square">
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
| 🔍 **深度信息搜集** | 按大纲章节分配搜索配额，配合引用链扩展策略，全面覆盖学术数据库与技术文档 |
| ✍️ **规范写作引擎** | 6 项严格文风规范，杜绝"AI腔"——禁用分点标题、比喻说教、单调句式 |
| 🎨 **SVG 智能配图** | 自动识别插图位置，基于标准化模板（3套学术色系）生成技术示意图，附带质量自动校验 |
| 🔬 **独立 Agent 审稿** | 五维度批判性审稿（逻辑/文风/事实/结构/一致性），独立 Agent 避免自我审稿偏误 |
| 📄 **一键 Word 导出** | 内置学术模板导出 `.docx`，导出前自动字数裁剪至目标范围 |
| ♻️ **会话恢复** | 基于 `_checkpoint.json` 的断点续写，对话中断无缝恢复 |

---

## 🏗️ 工作流架构

```
┌─────────────────────────────────────────────────────────────────────┐
│                     Paper Agent 6阶段流水线                            │
└─────────────────────────────────────────────────────────────────────┘

  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
  │  阶段一  │───▶│  阶段二  │───▶│  阶段三  │───▶│  阶段四  │───▶│  阶段五  │───▶│  阶段六  │
  │  任务解析│    │  深度信息│    │  规范写作│    │  图片规划│    │  独立审稿│    │  导出    │
  │  与方案  │    │  搜集    │    │  (分段)  │    │  +模板SVG│    │  五维度  │    │  Word    │
  └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘
       │               │               │               │               │               │
       │  用户确认     │  自动执行     │  分节写作     │  模板约束     │  独立Agent    │  字数裁剪    │
       │  大纲后继续   │  无需等待     │  上下文压缩   │  +自动校验    │  靶向修改     │  一键导出    │
       ▼               ▼               ▼               ▼               ▼               ▼
    ✅ 人工检查点    🤖 Agent      ✍️ Agent        🎨 Agent       🔬 Agent        📄 md2word
```

| 架构特性 | 说明 |
|---------|------|
| **轻量路由** | `CLAUDE.md` 仅含阶段路由与恢复逻辑（39行），按需加载独立阶段文件 |
| **按需加载** | 每个阶段对应 `docs/phase_N_*.md`，仅当前阶段读取，前后阶段不占上下文 |
| **共用规则** | 六项文风规范独立为 `docs/workflow_rules.md`，阶段三和阶段五共享引用 |
| **SVG 标准化** | `docs/svg_template.md`（3套色板模板）+ `docs/svg_checklist.md`（22项校验） |

---

## 🔬 各阶段详解

### 阶段一：任务解析与方案确认

读取 `任务要求.md`，提取全部作业参数。自动识别任务类型（课程论文/文献综述/实验报告/读书报告）并匹配对应结构模板。进行 3-5 次初步联网搜索（结果记入 `pre_search.md` 供后续复用）。设计包含字数预算表（每节预期字数及占比）的完整写作方案。输出 `初步大纲.md`。

> ⏸️ **检查点：** 必须等待用户确认后方可进入下一阶段。

### 阶段二：深度信息搜集

基于大纲关键词，按**每个二级板块 3-5 条**的配额执行高质量搜索，替代固定总量指标。采用**引用链扩展策略**——找到高质量综述后追踪其参考文献。每条信息标注质量评分（高/中/参考）和**唯一引用编号 `[N]`**，写作阶段直接使用该编号。输出 `collected_info.md`。

> ▶️ **自动进入** 阶段三。

### 阶段三：正式写作

采用**分段写作 + 上下文压缩**策略：

1. **写作规划**——将章节分为"核心论述章"和"包装章"，先写核心章节后写引言/结论
2. **逐节写作**——每章独立写到 `report_章节关键词.md`，写完后生成 200 字内压缩摘要记入 `_writing_log.md`
3. **上下文压缩**——后续章节携带此前所有章节的摘要而非全文，大幅降低上下文压力
4. **全文组装**——按序拼接所有章节文件为 `report.md`
5. **结构化自检**——表格逐条检查六项规范 + 术语一致性 + 跨章重复 + 引用完整性

全文长度为任务要求字数的 1.5 倍，确保内容充实。

> ▶️ **自动进入** 阶段四。

### 阶段四：图片规划与处理

通读报告，标记 3-5 处需要配图的位置，按类型处理：

- **技术示意图**（流程图、架构图、时间线）—— 绘制前读取 `docs/svg_template.md` 选择模板（学术单色/双色对比/三色分层），严格遵循色板、字体层级、元素样式
- **改编图** —— 根据数据重绘的统一风格图表
- **真实影像**（照片、截图）—— 在 `img.md` 中描述需求，由用户提供

每张 SVG 生成后，按 `docs/svg_checklist.md` 执行 22 项质量校验（文字溢出检测、字体后备链、配色合规、图-文一致性等），全部通过后方可插入。

> ▶️ 全为 SVG 则**自动进入**阶段五；如需用户提供图片则等待。

### 阶段五：苛刻审稿与修改

启动**独立的 Agent 实例**（脱离当前上下文）扮演评审老师，避免自我审稿的认知偏误。从五个维度进行批判性审查：

1. **逻辑与论证**—— 论点跳跃、因果关系弱、概念偷换
2. **文风规范**—— 逐条检查六项规则
3. **事实与引用**—— 数据过时、引用错误、结论夸大
4. **结构均衡性**—— 各章节字数是否合理
5. **跨章一致性**—— 术语统一、论点不自相矛盾

采用**靶向修改**原则（仅重写被评审意见涉及的具体段落），输出 `review.md`（含修改标记）和 `report_revised.md`。

> 🔄 **迭代循环：** 用户反馈 → 再审 → 再改 → 直至回复"定稿"。

### 阶段六：导出 Word 文档

导出前自动检查字数——超过任务要求 110% 则裁剪至目标范围。使用内置的 [md2word](https://github.com/lsqkk/md2word) 工具，以学术论文主题导出最终 `.docx` 文件。输出后总结总字数、图片数量和参考文献条数。

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

---

## 📁 模板文件结构

```
paper-agent/
├── CLAUDE.md                 # ← 路由引擎：按需加载阶段文件，断点恢复
│
├── docs/                     # ← 模块化阶段定义与制品模板
│   ├── workflow_rules.md     #   六项文风规范（阶段3/5共享）
│   ├── phase_1_task_analysis.md
│   ├── phase_2_deep_search.md
│   ├── phase_3_writing.md    #   分段写作+上下文压缩
│   ├── phase_4_image_planning.md
│   ├── phase_5_review.md     #   独立Agent审稿+五维度
│   ├── phase_6_export.md
│   ├── svg_template.md       #   3套学术SVG风格模板
│   └── svg_checklist.md      #   22项SVG质量校验清单
│
├── 任务要求.md               # ← 输入：作业要求模板，填写后启动
├── README.md                 # ← 本文件（中文说明）
├── README.en.md              # ← 英文说明
├── _checkpoint.json          # ← 断点文件，自动管理
│
├── img/                      # ← 阶段四生成的 SVG 示意图
│   └── img_01_*.svg
│
├── 初步大纲.md               # ← 阶段一产出
├── collected_info.md         # ← 阶段二产出
├── report.md                 # ← 阶段三产出
├── report_revised.md         # ← 阶段五产出
├── review.md                 # ← 阶段五产出
└── *.docx                    # ← 阶段六导出
```

> 运行时产出的中间文件（`_writing_log.md`、`report_segment_*.md`、`self_check.md` 等）已自动加入 `.gitignore`。

---

## 🎯 最佳实践

| ✅ 推荐做法 | ❌ 避免 |
|-----------|--------|
| 在 `任务要求.md` 中详细描述作业参数 | 留一行话，模糊不清 |
| 明确指定字数和格式要求 | 让 Agent 猜你想要什么格式 |
| 在"附加信息"中提供课程/教材背景 | 跳过上下文，导致内容偏题 |
| 仔细审阅阶段一的大纲和字数预算表 | 急于确认，大纲方向偏了后面全白写 |
| 在阶段五审稿循环中如实反馈 | 不看报告就批准定稿 |
| 确保参考文献真实可查 | 让 Agent 编造文献 |

### 会话恢复

如果对话因技术问题中断，重新启动后 Claude 会自动检测 `_checkpoint.json`，询问是否从断点继续。确认后即恢复上下文。

### 自定义工作流

各阶段逻辑独立存放在 `docs/` 目录中，可直接按需修改：

| 要改什么 | 改哪个文件 |
|---------|-----------|
| 文风规范 | `docs/workflow_rules.md` |
| SVG 色板/字体 | `docs/svg_template.md` |
| SVG 校验规则 | `docs/svg_checklist.md` |
| 写作策略参数 | `docs/phase_3_writing.md` |
| 审稿维度 | `docs/phase_5_review.md` |

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
└── CLAUDE.md  （共享路由引擎）
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
| 工作流 | 模块化 Markdown 管线：`CLAUDE.md` 路由 + `docs/` 独立阶段文件 |
| 插图 | SVG（标准化模板 + 质量自动校验） |
| Word 导出 | [md2word](https://github.com/lsqkk/md2word)（Markdown → docx 转换器） |
| 图床（可选） | Cloudflare R2 |
| 断点恢复 | `_checkpoint.json` 持久化 |

---

## 📜 开源协议

MIT —— 自由使用、修改、分享。

---

<p align="center">
  Made with ❤️ for students who'd rather spend time thinking than formatting<br>
  <sub>欢迎提交 Issue 和 PR</sub>
</p>
