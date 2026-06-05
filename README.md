# Onepage

**Presentation HTML Report Skill** — Turn structured materials (roadmaps,
project inventories, architecture notes, implementation plans, product
briefs, research summaries, status reports) into polished, self-contained
**single-page or chaptered presentation HTML**.

Every output is a **self-contained `.html` file**: inline CSS, no external
dependencies, ready to share, print, or embed. Built for executive
readouts, technical showcases, and roadmap reviews.

[中文说明 / Chinese version →](README.zh-CN.md)

The shipped artifact is an [Agent Skills](https://agentskills.io)-compatible
skill named **`onepage`**, packaged under
[`skills/onepage/`](skills/onepage/). Releases are produced by the
workflow in [`.github/workflows/release.yml`](.github/workflows/release.yml):
a push of a tag matching `v*` builds a zip of the skill directory and
attaches it to a GitHub Release.

---

## The Problem

Structured materials — roadmaps, architecture notes, status reports,
research summaries — are usually shared as long Markdown documents or
scattered slides. Both fail in the same ways when reviewed by leadership
or cross-functional stakeholders:

- **No visual hierarchy** — wall-of-text dumps hide the headline
  outcome and force the reader to extract it themselves.
- **Inconsistent design** — every author reinvents layout, color, and
  typography, so reports never feel like part of the same program.
- **External dependencies** — CDN-loaded fonts, icons, and chart
  libraries break in restricted networks and make offline review
  impossible.
- **No print story** — most web layouts collapse when printed or
  exported to PDF for distribution.
- **No narrative scaffolding** — a 200-line inventory or a 50-page
  research dump is delivered in raw form, with no chaptering,
  prioritization, or visual rhythm.

`onepage` solves this by giving an agent an opinionated design system,
a reusable HTML template, and a set of page modes that map the
material's intent to the right narrative structure.

## Core Features

### 1. Adaptive Page Modes

The agent selects a narrative structure based on the material's type
and the intended audience:

| Mode | Best for |
| --- | --- |
| Executive Report | Decision briefs, project inventories, status overviews |
| Technical Explainer | Architecture, flows, interfaces, constraints, release plans |
| Roadmap | Timelines, version plans, migration schedules |
| Product Brief | Positioning, audience, scenarios, features, differentiators, launch |
| Research Digest | Findings, evidence, theme comparisons, recommendations |
| Project Inventory | Global catalog of platforms / apps / services / capabilities |
| Operating Plan | Goals, workflows, dependencies, decisions, risk controls |
| Chaptered Showcase | Large material organized into themed chapters |

### 2. Visual Components

- **Compact Hero** — title, subtitle, metadata tags, 4–6 headline
  metric cards.
- **Sticky Navigation** — horizontally scrollable anchor nav, essential
  for long pages.
- **Metric Cards** — summary information for overviews, status, and
  progress.
- **HTML/CSS Architecture Grids** — three-column architecture grids
  with multi-layer support.
- **Milestone Cards** — action cards with P0 / P1 priority labels.
- **Comparison Matrices** — side-by-side views of options, teams, or
  systems.

### 3. Responsive + Print-Friendly

- **Desktop** — max width `1360px`, multi-column grids, high
  information density.
- **Tablet (≤ 980px)** — two-column layout.
- **Mobile (≤ 640px)** — single-column stack.
- **Print** — navigation hidden, shadows removed, page-break
  controlled.

## Design System

### Color Semantics

Colors carry stable meaning across every report this skill produces.
**The same color must always represent the same category of thing on
a page.**

| Color | Hex | Semantic |
| --- | --- | --- |
| 🔵 Blue | `#1f6feb` | Deployed apps, runtime, primary status |
| 🟢 Green | `#1b8754` | Shared platform capabilities, common services |
| 🟠 Orange | `#b86600` | In-flight work, async flows, pending capabilities |
| 🟣 Purple | `#7657c8` | External systems, independently deployed services |
| 🟡 Yellow | `#8a6d1f` | Storage, persistence |
| 🔴 Red | `#c63d32` | Risk, governance, audit, alerts |

### Typography & Layout

- **Body text** — `14px / 1.65`, comfortable for mixed CJK and
  Latin content.
- **Panels** — white background, `8px` border radius, subtle shadow.
- **Max width** — `1360px`.
- **Spacing** — `14px` between cards, `20px` between sections.

## Directory Structure

The shipped skill lives at `skills/onepage/`. The repository also
contains authoring source, release tooling, and this README.

```text
.
├── skills/
│   └── onepage/                  # Shipped Agent Skill (release artifact)
│       ├── SKILL.md              # Workflow, content rules, output checklist
│       ├── references/
│       │   └── design-system.md  # Detailed design guidance
│       ├── assets/
│       │   └── report-template.html  # Reusable single-page HTML template
│       └── agents/
│           └── openai.yaml       # UI metadata and default prompt
├── .github/
│   └── workflows/
│       └── release.yml           # Tag-driven release workflow
├── AGENTS.md                     # Authoring rules for this repo
├── README.md                     # This file (English)
└── README.zh-CN.md               # Chinese version
```

| Path | Purpose |
| --- | --- |
| `skills/onepage/SKILL.md` | Agent entry point: workflow steps, content rules, diagram rules, large-content strategy, output checklist. |
| `skills/onepage/references/design-system.md` | Detailed design reference. Read when adjusting layout, color, architecture grids, milestone cards, chaptering, or wording. |
| `skills/onepage/assets/report-template.html` | Ready-to-copy HTML template. Includes full CSS variables, responsive breakpoints, print styles, and placeholder structure. |
| `skills/onepage/agents/openai.yaml` | UI metadata for OpenAI-compatible platforms. Defines display name, short description, and default trigger prompt. |

## Quick Start

### Install

Download the latest release zip from
[GitHub Releases](https://github.com/wjhuang88/onepage/releases) and
unpack it into your Agent Skills directory (typically
`~/.codex/skills/` or your platform's equivalent):

```bash
curl -L -o /tmp/onepage.zip \
  https://github.com/wjhuang88/onepage/releases/latest/download/onepage.zip
unzip /tmp/onepage.zip -d ~/.codex/skills/
```

The skill will then be available to your agent as `onepage`.

### Use

Describe what you want in natural language — the agent will load
`SKILL.md` automatically, read `references/design-system.md` on
demand, and generate HTML from `assets/report-template.html`.

Example triggers:

> "Generate a presentation HTML report from this roadmap."
>
> "Turn this architecture note into a single-page HTML I can send to
> leadership."
>
> "Build a project status HTML report with an architecture diagram
> and milestone cards."

Typical flow:

```text
User provides source material
    ↓
1. Agent identifies audience, context, and material type
    ↓
2. Agent selects a page mode and chapter structure
    ↓
3. Agent generates HTML from report-template.html
    ↓
4. Agent refines visual details against design-system.md
    ↓
5. Agent outputs a self-contained .html file
```

### Use the Template Directly

If you just want a clean HTML template to fill in by hand:

1. Copy `skills/onepage/assets/report-template.html`.
2. Replace every `{{PLACEHOLDER}}` with your content.
3. Add or remove sections, cards, and architecture nodes as needed.

Key placeholders:

| Placeholder | Content |
| --- | --- |
| `{{REPORT_TITLE}}` | Report main title |
| `{{REPORT_SUBTITLE}}` | Report subtitle |
| `{{METRIC_*_VALUE}}` / `{{METRIC_*_LABEL}}` | Hero metric cards |
| `{{SUMMARY_*_TITLE}}` / `{{SUMMARY_*_TEXT}}` | Summary cards |
| `{{APP_*}}` / `{{APP_*_TEXT}}` | Architecture-grid application nodes |
| `{{MILESTONE_*_TITLE}}` / `{{MILESTONE_*_TEXT}}` | Milestone cards |

## Content Principles

- **Lead with the outcome** — open with the clearest result, current
  state, or decision needed. Avoid background-first narratives.
- **Business names first** — visible labels use business names.
  Internal IDs and environment variables appear as secondary
  information only when necessary.
- **Single source of truth** — describe each capability in one place;
  reference it by category elsewhere.
- **One idea per card** — every card carries one core message. Dense
  evidence and tables go into dedicated sections.
- **Consistent color semantics** — the same color always represents
  the same category on a page.
- **Concrete wording** — prefer explicit status words
  (*deployed*, *in progress*, *pending governance*) over vague
  phrasing.

## Output Quality Checklist

Before delivering a report, verify:

- [ ] Output is a single `.html` file that opens directly in a browser
- [ ] Desktop layout is compact and readable; mobile collapses to a
  single column
- [ ] Section titles, cards, and notes are aligned
- [ ] No text overlap or overflow
- [ ] Architecture grid columns are equal width with consistent color
  semantics
- [ ] Renders correctly when printed to PDF
- [ ] Navigation anchors jump to the right sections
- [ ] Milestone cards have balanced content and visual weight

## Technical Constraints

- **No external dependencies** — all CSS is inline; no CDN, no
  external resources, fully offline.
- **Single-file output** — one `.html` file contains everything.
- **Browser compatibility** — standard CSS only (Grid, Flexbox, CSS
  Variables); works in all modern browsers.
- **Mixed CJK + Latin** — font stack prioritizes PingFang SC and
  Microsoft YaHei for comfortable Chinese display alongside Latin
  text.

## Validation

After modifying the skill, run the basic validator:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  /path/to/onepage
```

Manual checks:

- `SKILL.md` YAML frontmatter is valid
- `description` clearly covers the trigger scenarios
- `report-template.html` is still a complete HTML file
- Desktop and mobile layouts render without overlap or overflow
- Color semantics are consistent across the page
