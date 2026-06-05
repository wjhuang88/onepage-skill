# Presentation HTML Design System

## Source Experience

This pattern was distilled from a Harness roadmap and inventory page that needed to combine deployment status, architecture diagrams, completed work, future work, and milestones for leadership review.

The pattern generalizes to presentation HTML: a shareable, self-contained page that turns structured material into a readable visual artifact. It can be used for leadership reports, technical explainers, product briefs, project inventories, research digests, roadmaps, and long-form chaptered summaries.

The strongest pattern is not visual decoration. It is the combination of:

- a compact hero with the page purpose and status metrics;
- sticky section navigation for long material;
- dense but readable cards;
- architecture diagrams implemented directly in HTML/CSS;
- consistent color semantics across sections;
- section patterns that stay balanced and action-oriented.

## Page Structure

Treat section order as a design decision, not a rigid template. Start from the reader's task and the source material's natural shape, then choose a narrative structure:

- summary-to-detail: best for decision briefs, inventories, and broad status pages;
- chronological: best for roadmaps, incident reviews, migrations, and implementation histories;
- problem-to-solution: best for proposals, transformation plans, and capability upgrades;
- capability map: best for platform, product, and architecture overviews;
- comparison: best for options, vendors, designs, teams, or before/after states;
- layered architecture: best for systems where physical, logical, and operational views differ.

This order works well for many project inventory, roadmap, or status reports, but adapt it freely:

1. Hero: title, short subtitle, metadata pills, and 4-6 numeric status metrics.
2. Navigation: sticky horizontal anchor list.
3. Overall status: 4-5 summary cards with similar text volume.
4. Architecture: one or two diagrams, split physical and logical views when needed.
5. Completed work: grouped by platform, apps, support services, operations, or governance.
6. In-progress work: focus on capabilities and constraints, not team ownership.
7. Gaps or focus areas: short problem statements with priority tags.
8. Medium/long-term plan: describe capability evolution without overclaiming current deployment.
9. Milestones: 4-6 balanced cards with action verbs and concrete outcomes.

For other display pages, adapt the section order to the source:

- Technical explainer: summary, concept map, architecture, flow, interfaces, constraints, rollout, open questions.
- Product brief: proposition, audience, scenarios, feature map, differentiation, roadmap, risks, launch plan.
- Research digest: key findings, evidence map, themes, comparisons, implications, recommendations, appendix.
- Operating plan: goals, workstreams, dependencies, decisions, timeline, risk controls, next actions.
- Chaptered long-form showcase: executive summary, chapter anchors, one section per theme, cross-cutting synthesis, next steps.

The model may merge, split, rename, or reorder chapters when it improves comprehension. Preserve layout discipline while doing so: each top-level section should have a clear purpose, a scannable title, a compact note, and one dominant visual pattern.

## Visual Language

Use a neutral operational palette:

- background: `#f7f8fb`
- panel: `#ffffff`
- text: `#172033`
- muted text: `#647086`
- border: `#dfe5ee`
- blue: deployed apps, runtime, primary status
- green: common support, MCP, shared capabilities
- orange: in-progress work, async flows, pending capabilities
- purple: external systems or independently hosted services
- yellow: storage or persistence
- pink/red: risk, governance, audit, operations alerts

Do not use one color family for everything. If two blocks share a color, they should share a semantic category.

## Layout Patterns

Use `max-width: 1360px` for wide presentation reports. Keep body font at `14px/1.65` for dense Chinese and English mixed content.

Recommended top layout:

- `.hero`: two-column grid, main narrative on the left and metrics on the right.
- `.hero-side`: two-column metric grid.
- `.nav`: sticky, horizontally scrollable anchors.
- `.section`: white panel with 8px radius and a subtle shadow.
- `.summary-grid`: 4-5 equal cards.

Architecture diagrams:

- Use `.architecture-set` to stack multiple diagrams.
- Use the same `.architecture-flow` grid across related diagrams:
  `grid-template-columns: minmax(220px, 0.85fr) minmax(0, 2fr) minmax(240px, 0.95fr);`
- Use `.diagram-card.wide` for center columns or full-width layers.
- Keep app cards compact. If a card no longer needs technical IDs, reduce padding and min-height.

Mobile rules:

- Collapse hero and architecture grids to one column below 900px.
- Collapse summary, matrix, and milestone grids to one or two columns depending on available width.
- Avoid fixed heights except for compact status labels or visual chips.

## Architecture Diagram Guidance

When representing a platform:

- Split infrastructure from application organization if physical deployment and logical app composition are mixed.
- Put direct external service entry points in their own layer.
- Put runtime as a wrapper around apps when all apps share the same runtime.
- Put common capabilities outside apps and connect them conceptually through copy or layout.
- Put MCP or integration services outside apps as support services; app cards should not repeat every MCP binding.
- For in-progress capabilities that are not deployed apps, use a pipeline strip or capability band rather than a fake app card.

For presentation-facing diagrams:

- Use Chinese or business names in primary labels.
- Hide internal deployment names unless the page is explicitly technical.
- Replace environment variable names with business descriptions.
- Avoid showing unclear implementation guesses. Use neutral wording like "independent environment" when the exact hosting form is unknown.

## Large Content Chaptering

When the input is too large to fit naturally into the template, plan the page before writing final copy. The goal is not to force a standard chapter count; the goal is to make a large body of material feel intentionally organized.

1. Inventory the source material into themes, decisions, systems, timelines, risks, and evidence.
2. Select a chapter count that fits the reader's task. Five to nine top-level anchors is a useful default for broad pages, but shorter pages may need three or four sections, and reference-heavy pages may need more with grouped navigation.
3. Choose the ordering logic deliberately: urgency, chronology, dependency, business domain, user journey, system layer, maturity level, or decision sequence.
4. Write one takeaway per chapter. If a chapter has no takeaway, merge it or turn it into supporting detail.
5. Choose one dominant visual pattern per chapter:
   - metric cards for status snapshots;
   - comparison matrix for alternatives, teams, systems, or capabilities;
   - architecture diagram for structural explanation;
   - timeline or roadmap for sequence;
   - risk register for uncertainty and mitigation;
   - detail table for dense facts that must remain visible.
6. Keep the top of the page as a compression layer: hero metrics, summary cards, and navigation should help the reader choose a path through the material.
7. Use progressive disclosure inside the single page: summary first, then grouped evidence, then implementation or appendix detail.
8. Balance chapter density. Avoid one chapter with twenty cards and another with one thin note unless the imbalance is intentional.
9. Keep the visual system consistent even when the story structure is custom: repeated section rhythm, aligned grids, predictable card sizes, consistent tag placement, and restrained color use.

Use these layout guardrails to preserve polish:

- Navigation labels should be short and parallel, ideally 2-6 words each.
- Top-level sections should use similar vertical spacing and heading treatment.
- Card grids should usually contain 3-6 cards; if there are more, group them into sub-sections or tables.
- A chapter should not mix too many patterns. Prefer one main pattern plus a short note or secondary detail block.
- Dense tables should have clear headers, small text only where necessary, and enough column width to avoid cramped wrapping.
- If a chapter is intentionally long, add subheadings or internal grouping so it does not become a wall of cards.

For very large source sets, generate in passes:

1. Outline and chapter map.
2. Section-by-section content extraction.
3. HTML composition with anchors and reusable card patterns.
4. Visual QA for overflow, repeated content, color consistency, and chapter flow.

## Wording Guidance

Use concrete, bounded language:

- "已具备生产运行底座雏形"
- "已完成部署"
- "推进中"
- "待统一配置"
- "待治理"
- "独立环境发布"
- "公共支撑能力"
- "对外服务入口"

Avoid:

- over-specific claims that were not verified;
- team ownership language unless explicitly requested;
- repeated "leadership version" wording in visible sections;
- unexplained internal codenames;
- long paragraphs inside cards.

## Review Checklist

Before finishing:

- Check whether section card text volume is balanced.
- Check whether architecture columns align across diagrams.
- Check whether bottom milestone cards are visually aligned.
- Check whether color categories are consistent.
- Check whether common capabilities appear once, not repeatedly.
- Check whether in-progress items are visually distinct from deployed apps.
- Check whether any app or service description overclaims current deployment.
- Check whether long materials have clear chapter anchors and one main takeaway per chapter.
