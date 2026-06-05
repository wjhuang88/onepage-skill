---
name: onepage
description: Create polished, self-contained presentation HTML pages from roadmaps, inventories, architecture notes, research summaries, project status lists, implementation plans, product briefs, or other structured materials. Use when the user explicitly asks for a shareable single-page or chaptered HTML artifact, presentation page, visual report, roadmap display, architecture showcase, executive review page, capability inventory page, milestone/status dashboard, or large-content synthesis page with clear visual hierarchy and embedded diagrams. Do not use for ordinary text-only summaries, Markdown reports, or analysis unless the user wants an HTML/page artifact. Chinese triggers include HTML报告, 单页报告, 展示页面, 路线图页面, 架构展示, 汇报页面, 领导汇报页面, 项目状态看板, 产品简报页面, 研究摘要页面.
license: MIT
metadata:
  author: wjhuang88
  version: "0.2.1"
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
5. **[Visual pattern]** For very large inputs, build a chapter plan before drafting HTML. Keep the detailed planning workflow in `references/advanced-guide.md`.
6. **[Color mapping]** Before writing content, lock the semantic color assignments for the whole page so the same color means the same thing everywhere. Detailed palette and semantics live in `references/design-system.md`.
7. **[Template & layout]** Use `assets/report-template.html` as the base when creating a new page. Preserve the responsive layout, print support, compact cards, sticky navigation, and color semantics unless the target repo already has a stronger design system. Read references progressively:
   - `references/design-system.md` — always (principles, pattern selection, visual language, wording, checklist).
   - `references/layout-reference.md` — when building or tuning layout, diagrams, or component details.
   - `references/advanced-guide.md` — when the source is very large, iterating on an existing page, or hitting edge cases.
8. **[Content fill]** Write content into the locked structure. Apply the Content Rules below as you go. Keep the output self-contained by default; if the user explicitly requests external assets, call out that the result will no longer be fully offline/shareable.
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
- Keep three-column architecture cards equal height while keeping card titles single-line, top-aligned, and visually aligned across columns. Title-to-content spacing must be uniform in left, center, and right columns.
- Show direct service entry points as a separate outward-facing layer when the page needs to explain what business systems can call.
- Distinguish deployed, independently hosted, in-progress, and support capabilities with color and small text, not by overcrowding app cards with technical labels.
- Avoid standalone legends when the card labels and color semantics are obvious.

## Large Content Planning

- Start with an outline before drafting HTML when the source material is long, fragmented, or covers multiple systems, teams, periods, or decisions.
- Give each chapter one job and one dominant visual pattern.
- Use the hero and first overview section as a compression layer: what changed, what matters now, and where to look next.
- Put low-level details near the chapter they support, not in a detached dump at the end unless they are true appendix material.
- For chapter counts, pass-based generation, and edge cases, read `references/advanced-guide.md`.

## Output Checklist

- The page works as a single `.html` file.
- Desktop layout is dense but readable; mobile layout collapses to one column.
- Section headings, notes, and cards align cleanly.
- No text overlaps later content.
- Architecture diagrams use consistent widths, equal-height outer cards, top-aligned single-line card titles, uniform title-to-content spacing, and stable color meaning.
- The final page can be printed or shared as a static artifact.
