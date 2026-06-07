# BidTech Writer · AI-Assisted Bidding Technical Proposal Tool

[中文](#中文) | [English](#english)

---

<a id="english"></a>

## What Problem Does It Solve

When writing bidding technical proposals, do you face these challenges:

- **Evaluators can't find scoring points** — The proposal's table of contents doesn't align with the evaluation scorecard, forcing evaluators to hunt through the entire document
- **Technical requirements get missed** — Tender documents contain many parameters and dense tables; you only discover omissions after submission
- **Risk control content leaks into the proposal** — Scoring values and disqualification clauses end up in the main text, becoming grounds for point deductions
- **Endless rework cycles** — Each rejection means rewriting from scratch, with no structured process control

ZBID addresses this through a **9-step fixed workflow + 9 independent Skill files**, ensuring AI follows rules step by step, produces files for your review at each stage, guarantees complete response to every technical requirement, and physically isolates risk control content from the proposal text.

---

## Core Principle

**TOC Structure = Evaluation Scorecard Mirror, Every Technical Requirement Responded Item by Item**

- Chapters align with scoring items — evaluators find corresponding points by browsing the table of contents
- Every row in the Technical Response Table (T-001, T-002, ...) = one sub-chapter in the TOC = one prompt entry = one response section in the text
- Writing prompts and risk control ledgers are physically separated — risk control content never enters the proposal text

---

## 9-Step Workflow

```
Step 1 Tender Parsing        → Step 2 Three Base Tables     → Step 3 Score-Mapped TOC
Step 4 Prompts + Risk Ledger → Step 5 Chapter-by-Chapter    → Step 6 Full Merge
Step 7 Compliance Check      → Step 8 Formatting            → Step 9 Archive
```

Each step produces independent files. You review and confirm before proceeding. AI cannot skip steps or advance without your approval.

---

## Quick Start

### 1. Prepare Files

```
your-workspace/
├── 投标编制规范.md              ← Main specification (in Chinese)
└── skills/                      ← Skill files directory
    ├── Skill1_招标文件智能解析拆分.md
    ├── Skill2_生成三份基准文档.md
    ├── Skill3_标书分级目录搭建.md
    ├── Skill4_批量生成撰写提示词库与风控台账.md
    ├── Skill5_分章节文稿生成.md
    ├── Skill6_三重合规AI预检.md
    ├── Skill7_标准化排版.md
    ├── Skill8_项目全套资料归档.md
    └── Skill_补充招标文件追加解析.md
```

### 2. Launch

In your AI chat window (Claude Code / ChatGPT or any AI tool with file reading capability), send:

```
请阅读 投标编制规范.md，理解你的角色定位、作业流程和权限红线，然后告诉我你已准备好。
```

*(Translation: "Read 投标编制规范.md, understand your role, workflow rules, and permission red lines, then tell me you're ready.")*

### 3. Start Writing

```
调用技能1：招标文件智能解析拆分，项目名称：XX项目，招标文件路径：./tender/XX_tender.pdf
```

AI will automatically create a project folder, execute parsing, produce files, and prompt you for review.

---

## Project Folder Structure

Each project automatically creates an independent folder, organized by workflow stage:

```
projects/{project-name}/
├── 00_招标文件/              ← Original tender, supplementary files
├── 01_解析与基准/            ← Parsing results + three base tables
├── 02_目录与提示词/          ← TOC + writing prompts + risk control ledger
├── 03_章节初稿/              ← Per-chapter files
├── 04_合并与质检/            ← Merged draft + inspection/re-inspection reports
├── 05_排版终稿/              ← Formatted final version
└── 06_归档/                  ← Archive checklist
```

---

## Step-by-Step Guide

### Step 1: Tender Document Parsing

```
调用技能1：招标文件智能解析拆分，项目名称：XX项目，招标文件路径：XXX
```

AI cleans irrelevant content (announcements, payment info, contacts) and splits into three sections:
- **Technical Scoring Section** — Extracts scoring items, values, and scoring conditions item by item
- **Technical Requirements Section** — Extracts technical parameters, service standards, and delivery requirements
- **Disqualification Section** — Extracts disqualification conditions (filters out commercial/price items)

Output: `01_解析与基准/招标文件解析.md`

### Step 2: Three Base Tables

```
调用技能2：生成三份基准文档
```

| Table | Content | AI Fills |
|-------|---------|----------|
| Scoring Alignment Table | Technical scoring items listed item by item | First 3 columns (AI), last 3 left blank (human) |
| Technical Response Table | Each technical requirement on its own row, with T-number and ★ markers | First 3 columns (AI), last 3 left blank (human) |
| Disqualification Checklist | Technical disqualification clauses listed item by item | First 2 columns (AI), last 3 left blank (human) |

Output: Three independent files under `01_解析与基准/`

### Step 3: Score-Mapped TOC

```
调用技能3：标书分级目录搭建
```

TOC mirrors the evaluation scorecard. Nesting depth is unlimited (4-5 levels is normal):
- Chapter → Scoring category
- Section → Scoring item (name reflects scoring keywords)
- Subsection → Technical sub-domain
- Item → Each row in the Technical Response Table (T-001, T-002, ...) must have its own heading

Output: `02_目录与提示词/标书目录.md`

### Step 4: Writing Prompts + Risk Control Ledger

```
调用技能4：批量生成撰写提示词库+风控台账
```

Two documents, physically separated:

| Document | Content | Purpose |
|----------|---------|---------|
| Writing Prompts | Overview / Detailed Design / Item-by-Response types (bound to T-numbers) | Used in Step 5 for writing. **Contains NO** scoring values or disqualification clauses |
| Risk Control Ledger | Scoring items + values + Technical hard constraints + Disqualification risk alerts | Used ONLY in Step 7 for inspection. **Must NEVER** enter the proposal text |

Output: Two independent files under `02_目录与提示词/`

### Step 5: Chapter-by-Chapter Writing

```
调用技能5：分章节文稿生成
```

- Outputs one chapter at a time, each as a separate file
- Reads ONLY writing prompts — **loading the risk control ledger is strictly forbidden**
- Unverifiable information marked with 【【Manual Addition: XXX】】 placeholders
- After reviewing each chapter: reply `本章定稿` → next chapter / `本章驳回：reason` → rewrite

Output: `03_章节初稿/第XX章_章节名.md`

### Step 6: Full Merge

Executed automatically after all chapters are finalized. Concatenates chapters in TOC order, unifies numbering, handles transitions.

Output: `04_合并与质检/合并初稿.md`

### Step 7: Compliance Inspection

```
调用技能6：三重合规AI预检
```

Four-dimensional inspection with risk levels:

| Dimension | Risk Level |
|-----------|-----------|
| Disqualification gaps | High |
| Scoring omissions | Medium |
| Technical deviations | Medium |
| Placeholder remnants | High (unfilled 【【Manual Addition】】 marks) |

After corrections, reply `整改完成` to trigger re-inspection of corrected items only.

Output: `04_合并与质检/质检报告.md` + `复检报告.md` (if applicable)

### Step 8: Formatting

```
调用技能7：标准化排版
```

Annotates heading fonts, line spacing, indentation, signature positions, and other formatting per tender requirements.

Output: `05_排版终稿/排版终稿.md`

### Step 9: Archive

```
调用技能8：项目全套资料归档
```

Verifies completeness of all files, generates archive checklist, and closes the project.

Output: `06_归档/归档清单.md`

---

## Data Chain

The Technical Response Table is the anchor of the entire chain — every row maps one-to-one:

```
T-001  ──→  TOC Sub-chapter  ──→  Prompt (Item-by-Response)  ──→  Text Section
T-002  ──→  TOC Sub-chapter  ──→  Prompt (Item-by-Response)  ──→  Text Section
T-003  ──→  TOC Sub-chapter  ──→  Prompt (Item-by-Response)  ──→  Text Section
```

A break at any point in this chain = an unresponded technical requirement. Step 7 inspection checks this chain in reverse, but it's best to catch gaps at Steps 2-4.

---

## Command Reference

| Scenario | Command |
|----------|---------|
| Launch | `请阅读 投标编制规范.md，理解你的角色定位、作业流程和权限红线，然后告诉我你已准备好` |
| Step 1 | `调用技能1：招标文件智能解析拆分，项目名称：XX项目，招标文件路径：XXX` |
| Step 2 | `调用技能2：生成三份基准文档` |
| Step 3 | `调用技能3：标书分级目录搭建` |
| Step 4 | `调用技能4：批量生成撰写提示词库+风控台账` |
| Step 5 | `调用技能5：分章节文稿生成` |
| Step 7 | `调用技能6：三重合规AI预检` |
| Step 8 | `调用技能7：标准化排版` |
| Step 9 | `调用技能8：项目全套资料归档` |
| Confirm | `确认通过` |
| Confirm TOC | `目录确认通过` |
| Confirm chapter | `本章定稿` |
| Reject & redo | `驳回重做：specific issue` |
| Reject chapter | `本章驳回：specific issue` |
| Partial edit | `局部修改：XX content, change to XXX` |
| Corrections done | `整改完成` |
| Supplementary tender | `补充招标文件追加解析，补充文件路径：XXX` |

---

## Permission Red Lines

1. AI cannot modify the fixed column structure of base tables
2. AI cannot mark positive/negative deviations
3. AI cannot fabricate qualifications, case studies, or parameters
4. AI cannot skip user confirmation steps
5. Risk control ledger content must never enter the proposal text
6. Loading the risk control ledger during writing is strictly forbidden

---

## License

MIT
