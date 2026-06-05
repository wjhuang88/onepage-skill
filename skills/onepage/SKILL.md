---
name: onepage
description: Create polished, self-contained presentation HTML pages from roadmaps, inventories, architecture notes, research summaries, project status lists, implementation plans, product briefs, or other structured materials. Use when the user asks to generate or refine a shareable single-page or chaptered HTML artifact for executive review, technical presentation, roadmap display, capability inventory, milestone tracking, status summary, or large-content synthesis with clear visual hierarchy and embedded diagrams. Chinese triggers include 生成报告, HTML报告, 路线图页面, 架构展示, 汇报页面, 领导汇报, 项目状态总结, 产品简报, 研究摘要.
license: MIT
metadata:
  author: wjhuang88
  version: "0.1.0"
---

# Presentation HTML Report

## Decision Priorities

Decisions are not equally weighted. Making them out of order produces inconsistent pages. Follow this priority:

1. **Page mode** (most important) — determines the narrative structure and all subsequent visual choices. Decide this before writing any HTML.
2. **Chapter flow** — group source material into sections with a clear narrative arc. Each chapter gets one job.
3. **Visual pattern per chapter** — assign each chapter a dominant visual pattern (metric cards, architecture diagram, comparison matrix, timeline, risk register, detail table).
4. **Color mapping** — assign semantic colors at the page level, once. The same color must mean the same thing everywhere.
5. **Content fill** — write and place content only after the above decisions are locked.

Reversing this order (writing content first, then choosing visuals) is the most common cause of inconsistent output.

## Workflow

Steps follow the Decision Priorities above. Each step is tagged with its priority band.

1. **[Page mode]** Identify the audience, viewing context, source-material type, and desired action from the source material.
2. **[Page mode]** Choose the page mode before writing any HTML: executive report, technical explainer, roadmap, product brief, research digest, project inventory, operating plan, or chaptered long-form showcase.
3. **[Chapter flow]** Design the chapter flow around the material instead of forcing a fixed report structure. Choose, merge, split, or reorder sections so the page has a clear narrative arc for the intended reader.
4. **[Chapter flow]** Convert raw notes into balanced sections that match the chosen flow. Common building blocks include overview, architecture or operating model, current state, evidence, completed work, in-progress work, gaps, plan, risks, milestones, and appendix-style details.
5. **[Visual pattern]** For very large inputs, first build a flexible chapter plan: group source material by theme, define the main takeaway or question for each chapter, assign each chapter a dominant visual pattern (metric cards, comparison matrix, architecture diagram, timeline, roadmap, risk register, capability map, detail table), and decide what belongs in summary cards versus detail sections.
6. **[Color mapping]** Before writing content, lock the semantic color assignments for the whole page so the same color means the same thing everywhere. Detailed palette and semantics live in `references/design-system.md`.
7. **[Template & layout]** Use `assets/report-template.html` as the base when creating a new page. Preserve the responsive layout, print support, compact cards, sticky navigation, and color semantics unless the target repo already has a stronger design system. Read references progressively:
   - `references/design-system.md` — always (principles, pattern selection, visual language, wording, checklist).
   - `references/layout-reference.md` — when building or tuning layout, diagrams, or component details.
   - `references/advanced-guide.md` — when the source is very large, iterating on an existing page, or hitting edge cases.
8. **[Content fill]** Write content into the locked structure. Apply the Content Rules below as you go. Keep the output self-contained unless the user requests external assets; inline CSS is preferred for standalone presentation HTML.
9. **[Verify]** Verify the page by opening or inspecting the generated HTML for overlapping text, inconsistent grid widths, cramped cards, weak chapter flow, and mismatched color semantics.

## Content Rules

- Lead with the clearest outcome, current state, or reader decision, not background narrative.
- Use business-readable names in visible labels. Keep internal IDs, environment variable names, and implementation details in secondary text only when they are necessary.
- Avoid repeating the same capability in multiple cards. Use one canonical location, then refer to it by category.
- Separate physical deployment architecture from logical application or capability architecture when one diagram becomes too dense.
- Put shared capabilities in a common support area instead of duplicating them inside every app or workstream.
- Use color consistently: the same color must mean the same kind of thing across the page.
- Keep milestone content balanced. A section with only one or two thin cards usually needs consolidation or a clearer phase model.
- For large materials, do not flatten everything into one long list. Build a visible chapter structure with section anchors, compact summaries, and progressive detail.
- Let chapters follow the natural logic of the source material. A polished page may be chronological, thematic, layered from summary to detail, problem-to-solution, capability-based, or decision-oriented.
- Keep each card scoped to one idea. Move dense evidence, examples, tables, or implementation notes into dedicated detail blocks.

## Diagram Rules

- Prefer HTML/CSS diagrams for presentation pages when the diagram needs to live in the report itself.
- Use aligned three-column architecture grids for comparable diagrams. Keep column widths consistent across related diagrams.
- Show direct service entry points as a separate outward-facing layer when the page needs to explain what business systems can call.
- Distinguish deployed, independently hosted, in-progress, and support capabilities with color and small text, not by overcrowding app cards with technical labels.
- Avoid standalone legends when the card labels and color semantics are obvious.

## Large Content Planning

- Start with an outline before drafting HTML when the source material is long, fragmented, or covers multiple systems, teams, periods, or decisions.
- Choose the number of chapters based on the material and reading task. As a practical default, broad materials often work well with 5-9 top-level anchors, but clarity is more important than hitting that range.
- Give each chapter a job: orient, compare, explain, prove, decide, sequence, track risk, teach a concept, or show evidence.
- Assign each chapter a primary visual pattern: metric cards, comparison matrix, architecture diagram, timeline, roadmap, risk register, capability map, or detail table.
- Use the hero and first overview section as a compression layer. They should tell the reader what changed, what matters now, and where to look next.
- Put low-level details near the chapter they support, not in a detached dump at the end unless they are true appendix material.
- Preserve visual order even when the chapter order is custom: consistent heading hierarchy, stable section spacing, aligned grids, restrained card counts, and navigation labels that scan cleanly.

## Output Checklist

- The page works as a single `.html` file.
- Desktop layout is dense but readable; mobile layout collapses to one column.
- Section headings, notes, and cards align cleanly.
- No text overlaps later content.
- Architecture diagrams use consistent widths and color meaning.
- The final page can be printed or shared as a static artifact.
