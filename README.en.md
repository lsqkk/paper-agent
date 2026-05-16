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
  <img alt="Architecture" src="https://img.shields.io/badge/architecture-modular-green?style=flat-square">
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
| 🔍 **Deep Research** | Per-section search quotas (3-5 per section) with citation chain expansion strategy |
| ✍️ **Rigorous Writing** | Section-by-section writing with context compression; strict style enforcement against common "AI writing" pitfalls |
| 🎨 **Standardized SVG Diagrams** | 3 academic color templates with 22-point quality auto-verification checklist |
| 🔬 **Independent Agent Review** | 5-dimension critical review (logic/style/facts/structure/consistency) by a separate Agent instance |
| 📄 **One-Click Export** | Direct export to formatted Word document with automatic word count trimming |
| ♻️ **Session Resume** | `_checkpoint.json` persistence — pick up where you left off after interruptions |

---

## 🏗️ Workflow Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                     Paper Agent 6-Stage Pipeline                      │
└─────────────────────────────────────────────────────────────────────┘

  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
  │  STAGE 1 │───▶│  STAGE 2 │───▶│  STAGE 3 │───▶│  STAGE 4 │───▶│  STAGE 5 │───▶│  STAGE 6 │
  │  Task    │    │  Deep    │    │  Formal  │    │  Figure  │    │  Indep.  │    │  Export  │
  │  Parse & │    │  Info    │    │  Writing │    │  Design  │    │  Agent   │    │  Word    │
  │  Outline │    │  Search  │    │  (segmented) │  + SVG   │    │  Review  │    │  Doc     │
  └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘
       │               │               │               │               │               │
       │  User         │  Automatic    │  Section-by-  │  Template    │  Independent   │  Word count  │
       │  Approves     │  Execution    │  Section w/   │  Constrained │  Agent Review  │  trim before │
       │  Outline      │               │  Context      │  + Validation│  + Targeted    │  export      │
       │               │               │  Compression  │               │  Revision      │              │
       ▼               ▼               ▼               ▼               ▼               ▼
    ✅ Human       🤖 Agent        ✍️ Agent        🎨 Agent       🔬 Agent        📄 md2word
    Checkpoint     Auto            Segmented       Template +     Fresh Instance   Final Output
                                   Writing         Verification   (No Self-bias)
```

| Architecture Feature | Detail |
|----------------------|--------|
| **Lightweight Router** | `CLAUDE.md` is only 39 lines — routing table + session recovery |
| **On-Demand Loading** | Each stage lives in `docs/phase_N_*.md`, loaded only when that stage is active |
| **Shared Rules** | Six writing rules in `docs/workflow_rules.md`, shared by Stage 3 and Stage 5 |
| **SVG Standardization** | `docs/svg_template.md` (3 color schemes) + `docs/svg_checklist.md` (22 verification items) |

---

## 🔬 Detailed Stage Breakdown

### Stage 1 — Task Parsing & Outline Design

Reads `任务要求.md`, classifies task type (course paper / literature review / lab report / book report), and matches a structural template. Performs 3-5 targeted web searches (results saved to `pre_search.md` for later reuse). Designs a writing strategy with a **word count budget table** (expected word count per section). Outputs `初步大纲.md` for user approval.

> ⏸️ **Checkpoint:** Waits for user confirmation before proceeding.

### Stage 2 — Deep Information Gathering

Executes high-quality searches with a **per-section quota of 3-5 items** (replacing the flat 20-item target). Uses **citation chain expansion** — tracing references from high-quality surveys. Each item gets a **quality score** (high/medium/reference) and a **unique citation number `[N]`** for direct use in writing. Outputs `collected_info.md`.

> ▶️ **Auto-proceeds** to Stage 3.

### Stage 3 — Formal Writing (Segmented + Context Compression)

1. **Writing plan** — classifies sections into "core" and "wrapper" chapters; writes core chapters first
2. **Per-section writing** — each chapter written to its own `report_*.md` file; a 200-character compressed summary goes into `_writing_log.md`
3. **Context compression** — subsequent sections carry only compressed summaries of prior sections, drastically reducing context pressure
4. **Assembly** — concatenates all segment files into `report.md`
5. **Structured self-check** — table-based verification of 6 style rules + terminology consistency + cross-section deduplication + citation integrity

Target length: 1.5x the required word count to ensure rich content (trimmed at export).

> ▶️ **Auto-proceeds** to Stage 4.

### Stage 4 — Figure Design & Processing (Templated + Validated)

Identifies 3-5 positions needing illustrations:

- **Technical diagrams** (flowcharts, architecture, timelines) — reads `docs/svg_template.md` to select a color scheme template, strictly follows its palette, typography, and element styles
- **Adapted charts** — data-driven charts redrawn in unified style
- **Real images** (photos, screenshots) — user-provided via `img.md`

Each SVG is validated against the 22-point `docs/svg_checklist.md` (text overflow, font fallback chain, color compliance, content alignment, text-consistency) before insertion.

> ▶️ **Auto-proceeds** if all SVGs; ⏸️ **Checkpoint** if user images needed.

### Stage 5 — Rigorous Review & Revision (Independent Agent)

Launches a **separate Agent instance** (fresh context, no self-bias) as a stern thesis advisor reviewing five dimensions:

1. **Logic & Argumentation** — gaps, weak causality, concept substitution
2. **Style Compliance** — point-by-point against the six writing rules
3. **Facts & Citations** — outdated data, mismatched references, overclaimed conclusions
4. **Structural Balance** — reasonable length distribution across sections
5. **Cross-Chapter Consistency** — unified terminology, no self-contradiction

Uses **targeted revision** — rewrites only sections affected by review findings. Outputs `review.md` with resolution notes and `report_revised.md`.

> 🔄 **Iteration loop:** User feedback → re-review → re-revise → until "定稿" (final approval).

### Stage 6 — Word Export

Auto-trims the report to target word count if it exceeds 110% of the requirement. Exports using an academic paper template via [md2word](https://github.com/lsqkk/md2word). Summarizes total word count, figure count, and references.

> ⚠️ `md2word` requires separate installation: `git clone https://github.com/lsqkk/md2word`

> ✅ **Complete.**

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

---

## 📁 Template File Structure

```
paper-agent/
├── CLAUDE.md                 # ← Router engine: on-demand stage loading, session resume
│
├── docs/                     # ← Modular stage definitions & asset templates
│   ├── workflow_rules.md     #   Six writing rules (shared by Stage 3 & 5)
│   ├── phase_1_task_analysis.md
│   ├── phase_2_deep_search.md
│   ├── phase_3_writing.md    #   Segmented writing + context compression
│   ├── phase_4_image_planning.md
│   ├── phase_5_review.md     #   Independent agent review + 5 dimensions
│   ├── phase_6_export.md
│   ├── svg_template.md       #   3 academic SVG style templates
│   └── svg_checklist.md      #   22-point SVG quality checklist
│
├── 任务要求.md               # ← Input: assignment specification template
├── README.md                 # ← Chinese documentation
├── README.en.md              # ← This file
├── _checkpoint.json          # ← Auto-managed session checkpoint
│
├── img/                      # ← Stage 4 generated SVGs
│   └── img_01_*.svg
│
├── 初步大纲.md               # Stage 1 output
├── collected_info.md         # Stage 2 output
├── report.md                 # Stage 3 output
├── report_revised.md         # Stage 5 output
├── review.md                 # Stage 5 output
└── *.docx                    # Stage 6 export
```

Intermediate artifacts (`_writing_log.md`, `report_segment_*.md`, `self_check.md`, etc.) are auto-gitignored.

---

## 🎯 Best Practices

| Do | Don't |
|----|-------|
| ✅ Write detailed task requirements in `任务要求.md` | ❌ Leave requirements vague or one-line |
| ✅ Specify exact word count and formatting rules | ❌ Expect the agent to guess the format |
| ✅ Include course/department context in "附加信息" | ❌ Skip background context |
| ✅ Review and approve the outline + word budget carefully | ❌ Rush through Stage 1 — it sets the direction |
| ✅ Provide honest feedback in Stage 5 iteration loop | ❌ Approve a report without reviewing |
| ✅ Keep reference sources real and verifiable | ❌ Let the agent fabricate citations |

### Session Recovery

If your session is interrupted, Claude will detect `_checkpoint.json` on restart and ask whether to resume from the breakpoint.

### Customization

Each stage's logic lives in its own `docs/` file:

| Want to change | Edit this file |
|---------------|---------------|
| Writing style rules | `docs/workflow_rules.md` |
| SVG color palettes / fonts | `docs/svg_template.md` |
| SVG verification criteria | `docs/svg_checklist.md` |
| Writing strategy parameters | `docs/phase_3_writing.md` |
| Review dimensions | `docs/phase_5_review.md` |

---

## 🔧 Advanced Usage

### Multi-Paper Batch

```
paper-agent/
├── assignment-1/
│   ├── 任务要求.md
│   └── ... (auto-generated)
├── assignment-2/
│   └── ...
└── CLAUDE.md  (shared router engine)
```

### Custom Export Templates

The `md2word` tool supports custom `.docx` templates:

```bash
md2word report_revised.md -o output.docx -t my-template.docx
```

Built-in themes: `official` (government document), `academic` (thesis), `tech` (technical report), `media` (editorial).

---

## 🧩 Tech Stack

| Component | Technology |
|-----------|-----------|
| AI Engine | Claude Code (Opus / Sonnet models) |
| Workflow | Modular Markdown pipeline: `CLAUDE.md` router + `docs/` stage files |
| Figures | SVG (standardized templates + auto verification) |
| Export | [md2word](https://github.com/lsqkk/md2word) (Markdown → docx converter) |
| Image Upload | Cloudflare R2 (optional, for blog hosting) |
| Session Recovery | `_checkpoint.json` persistence |

---

## 📜 License

MIT — use freely, modify freely, share freely.

---

<p align="center">
  Made with ❤️ for students who'd rather spend time thinking than formatting<br>
  <sub>Contributions, issues, and feature requests are welcome!</sub>
</p>
