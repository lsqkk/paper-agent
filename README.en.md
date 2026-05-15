<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://capsule-render.vercel.app/api?type=waving&height=200&color=0:1a1a2e,50:16213e,100:0f3460&text=Paper%20Agent&fontAlignY=35&fontSize=60&desc=Academic%20Writing%20Workflow%20Template&descAlignY=55&descSize=18&fontColor=e0e0e0">
  <img alt="Paper Agent banner" src="https://capsule-render.vercel.app/api?type=waving&height=200&color=0:1a1a2e,50:16213e,100:0f3460&text=Paper%20Agent&fontAlignY=35&fontSize=60&desc=Academic%20Writing%20Workflow%20Template&descAlignY=55&descSize=18&fontColor=1a1a2e">
</picture>

<p align="center">
  <b>🤖 AI-Powered End-to-End Academic Writing Workflow Template</b><br>
  <i>For Claude Code — 6-stage pipeline: Task Parsing → Deep Research → Formal Writing → Auto Diagramming → Peer Review → Word Export</i>
</p>

<p align="center">
  <a href="README.md"><img alt="中文版" src="https://img.shields.io/badge/%E4%B8%AD%E6%96%87%E7%89%88%E6%9C%AC-blue?style=flat-square"></a>
  <img alt="GitHub" src="https://img.shields.io/badge/license-MIT-blue?style=flat-square">
  <img alt="Claude Code" src="https://img.shields.io/badge/Claude%20Code-Ready-8A2BE2?style=flat-square">
  <img alt="Workflow" src="https://img.shields.io/badge/workflow-6%20stages-success?style=flat-square">
  <img alt="Language" src="https://img.shields.io/badge/language-English%20%7C%20%E4%B8%AD%E6%96%87-orange?style=flat-square">
  <img alt="Platform" src="https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey?style=flat-square">
</p>

---

## 📋 Overview

**Paper Agent** is a structured, six-stage academic writing workflow template for [Claude Code](https://claude.ai/code). It transforms a simple task description into a polished academic report with automatic research collection, rigorous writing, diagram generation, peer review, and Word export.

Designed for university students, researchers, and professionals who need to produce high-quality academic papers, reports, or assignments with minimal manual effort.

### ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🧠 **AI-Driven Pipeline** | Fully automated 6-stage workflow from task analysis to final export |
| 🔍 **Deep Research** | Automatic 20+ source information gathering before writing |
| ✍️ **Rigorous Writing** | Strict style enforcement avoiding common "AI writing" pitfalls |
| 🎨 **Auto Diagramming** | SVG diagrams generated programmatically to illustrate key concepts |
| 🔬 **Critical Review** | AI-powered peer review with iterative revision loop |
| 📄 **One-Click Export** | Direct export to formatted Word document with academic templates |

---

## 🏗️ Workflow Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                     Paper Agent 6-Stage Pipeline                      │
└─────────────────────────────────────────────────────────────────────┘

  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
  │  STAGE 1 │───▶│  STAGE 2 │───▶│  STAGE 3 │───▶│  STAGE 4 │───▶│  STAGE 5 │───▶│  STAGE 6 │
  │  Task    │    │  Deep    │    │  Formal  │    │  Figure  │    │  Review  │    │  Export  │
  │  Parse & │    │  Info    │    │  Writing │    │  Design  │    │  & Revi- │    │  Word    │
  │  Outline │    │  Search  │    │          │    │  & Draw  │    │  sion    │    │  Doc     │
  └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘
       │               │               │               │               │               │
       │  User         │  Automatic    │  Automatic    │  Automatic    │  User         │  One-click   │
       │  Confirms     │  Execution    │  Execution    │  (or user     │  Feedback     │  Final       │
       │  Outline      │               │               │   provides    │  Loop         │  Output      │
       │               │               │               │   photos)     │               │              │
       ▼               ▼               ▼               ▼               ▼               ▼
    ✅ Human       🤖 Agent        ✍️ Agent        🎨 Agent/User   🔬 Agent        📄 md2word
    Checkpoint     Auto-run        Auto-run        Auto-run        Iterative       Export
```

---

## 🔬 Detailed Stage Breakdown

### Stage 1 — Task Parsing & Outline Design
**Input:** `任务要求.md` (task specification file)

Reads the task requirements, performs targeted web research (3-5 queries), designs a writing strategy with thesis statement, outline structure, and argumentation logic. Outputs `初步大纲.md` for user approval.

> ⏸️ **Checkpoint:** Waits for user confirmation before proceeding.

### Stage 2 — Deep Information Gathering
**Input:** Approved outline

Conducts 20+ high-quality web searches targeting academic databases (arXiv, Google Scholar), official documentation, and industry reports. All findings are annotated with source links, publication dates, and mapped to specific outline sections. Outputs `collected_info.md`.

> ▶️ **Auto-proceeds** to Stage 3 after completion.

### Stage 3 — Formal Writing
**Input:** Outline + collected info

Writes the full report (`report.md`) at 1.5× the target word count, strictly following six writing style rules:
- 🚫 No bullet-point mini-headings — continuous prose only
- 🌊 Natural paragraph flow with smooth transitions
- 📖 First-occurrence English glossing for key terms (e.g., "生成对抗网络（Generative Adversarial Network, GAN）")
- 🚫 No flowery metaphors or "not A but B" didactic constructions
- 📏 Concise headings without colons or dashes
- 🎵 Varied sentence rhythm mixing short, medium, and long sentences

> ▶️ **Auto-proceeds** to Stage 4 after completion.

### Stage 4 — Figure Design & Processing
**Input:** Completed report

Identifies 3-5 positions where diagrams would enhance understanding. Classifies each into:
- **Technical diagrams** (flowcharts, architecture diagrams, timelines) → auto-generated as SVG
- **Real images** (photos, screenshots) → user-provided via `img/` directory

Outputs SVG files to `img/` folder with consistent color schemes.

> ▶️ **Auto-proceeds** if all figures are SVGs; ⏸️ **Checkpoint** if user images needed.

### Stage 5 — Rigorous Review & Revision
**Input:** Report with figures

Acts as an unforgiving thesis advisor, scrutinizing:
1. **Logic flaws** — argument gaps, weak causality, concept substitution
2. **Style violations** — forbidden patterns, didactic tone, formatting errors
3. **Factual errors** — outdated data, citation mismatches, overclaimed conclusions

Outputs `review.md` with line-level critique and produces `report_revised.md` with all issues addressed.

> 🔄 **Iteration loop:** User provides feedback → re-review → re-revise → until "定稿" (final approval).

### Stage 6 — Word Export
**Input:** Final approved report

Exports the final document using an academic paper template via the [md2word](https://github.com/lsqkk/md2word) converter (requires separate installation). Default output: `{Title}_最终报告.docx`.

> ✅ **Complete:** Summary of total word count, figure count, and references.

---

## 🚀 Getting Started

### Prerequisites

- [Claude Code](https://claude.ai/code) installed and authenticated
- (Optional) [md2word](https://github.com/lsqkk/md2word) for Word export in Stage 6

### One-Click Start

```bash
# Clone the template
git clone https://github.com/your-username/paper-agent.git my-paper

# Navigate in
cd my-paper

# Edit the task requirements
# (Open 任务要求.md and fill in your assignment details)

# Launch Claude Code
claude

# That's it! Claude will read the workflow and walk you through Stage 1.
```

### Edit `任务要求.md`

```markdown
《Course Name》Summary Report
Topic: Course learning reflection, book report (title can be customized)

Requirements:
1. Format: 10%
2. Standardization: 20%
3. Word count: 10% (~8000 words)
...

【Additional info for AGENT】
Course background, textbook info, professor info, content focus...
```

### Manual: Use the /plan Skill

```bash
claude
> /plan "Write an 8000-word report about machine learning"
```

The agent will analyze requirements, generate an outline, and request your approval before proceeding.

---

## 📁 Template File Structure

```
paper-agent/
├── CLAUDE.md              # ← Core: 6-stage workflow definition (the engine)
├── 任务要求.md            # ← Input: your assignment requirements (template)
├── README.md              # ← Chinese documentation
├── README.en.md           # ← This file
├── .gitignore             # ← Auto-generated artifact exclusion rules
├── .gitattributes         # ← Line-ending normalization
│
├── .claude/               # ← Claude local configuration (gitignored)
│   └── settings.local.json
│
├── img/                   # ← Generated SVG diagrams (gitignored)
│   └── img_01_*.svg
│
├── 初步大纲.md            # ← Stage 1 output (gitignored)
├── collected_info.md      # ← Stage 2 output (gitignored)
├── report.md              # ← Stage 3 output (gitignored)
├── report_revised.md      # ← Stage 5 output (gitignored)
├── review.md              # ← Stage 5 output (gitignored)
└── *.docx                 # ← Stage 6 export (gitignored)
```

---

## 🎯 Best Practices

| Do | Don't |
|----|-------|
| ✅ Write detailed task requirements in `任务要求.md` | ❌ Leave requirements vague or one-line |
| ✅ Specify exact word count and formatting rules | ❌ Expect the agent to guess the format |
| ✅ Include course/department context in "附加信息" | ❌ Skip background context |
| ✅ Review and approve the outline carefully | ❌ Rush through Stage 1 — it sets the direction |
| ✅ Provide honest feedback in Stage 5 iteration loop | ❌ Approve a report without reviewing |
| ✅ Keep reference sources real and verifiable | ❌ Let the agent fabricate citations |

### Workflow State Management

If your session is interrupted, send:

> "恢复状态"

Claude will recall which stage was last completed and restart from there.

### Customization

To modify writing style requirements, edit the six writing rules in `CLAUDE.md` Stage 3 section. To change figure generation parameters, update the SVG specifications in Stage 4.

---

## 🔧 Advanced Usage

### Multi-Paper Batch

For multiple assignments, create per-assignment directories:

```
paper-agent/
├── assignment-1/
│   ├── 任务要求.md
│   └── ... (auto-generated)
├── assignment-2/
│   └── ...
└── CLAUDE.md  (shared workflow)
```

### Custom Export Templates

The `md2word` tool supports custom `.docx` templates. Place your template in the project root and reference it:

```bash
md2word report_revised.md -o output.docx -t my-template.docx
```

Built-in themes: `official` (government document), `academic` (thesis), `tech` (technical report), `media` (editorial).

---

## 🧩 Tech Stack

| Component | Technology |
|-----------|-----------|
| AI Engine | Claude Code (Opus / Sonnet models) |
| Workflow | Markdown-defined pipeline in `CLAUDE.md` |
| Figures | SVG (inline hand-coded vector graphics) |
| Export | [md2word](https://github.com/lsqkk/md2word) (Markdown → docx converter) |
| Image Upload | Cloudflare R2 (optional, for blog hosting) |

---

## 📜 License

MIT — use freely, modify freely, share freely.

---

<p align="center">
  Made with ❤️ for students who'd rather spend time thinking than formatting<br>
  <sub>Contributions, issues, and feature requests are welcome!</sub>
</p>
