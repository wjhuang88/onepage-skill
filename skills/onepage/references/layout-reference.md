# Presentation HTML — Layout & Component Reference

Read this file when building or tuning the page layout, working with architecture diagrams, or applying component-level rules. For core methodology (principles, pattern selection, wording), see [design-system.md](design-system.md).

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
- Use `align-items: stretch` on `.architecture-flow` so the three outer cards stay equal height. Keep content top-aligned inside each card with the `.diagram-card` rules below.
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

## Component Guardrails

### Hero
- Hero must contain: eyebrow label, h1 title, subtitle, metadata pills, and 2-6 metric cards.
- Hero must NOT contain: architecture diagrams, long-form text (>2 sentences in subtitle), or interactive elements.
- Metric cards should show different measures. Avoid two cards showing the same metric in different units.

### Navigation (.nav)
- Navigation is required when the page has 4 or more top-level sections.
- Navigation may be omitted for short pages (3 or fewer sections).
- Navigation labels: 2-6 characters in Chinese, 2-6 words in English. Parallel construction (all nouns, or all verb phrases). Do not mix styles.
- Navigation must be sticky and horizontally scrollable. Never use vertical sidebar navigation in a presentation report.

### Section (.section)
- Every section must have: a section-title (h2 + optional section-note), and at least one content block.
- section-note should be concise supplementary context, not a second paragraph of content.
- Vertical spacing between sections must be consistent (20px margin-top). Do not tighten or widen spacing for individual sections.

### Summary Cards (.summary-card / .summary-grid)
- Use 4-5 cards per grid. Fewer than 3 suggests the overview is too thin; more than 6 suggests it needs sub-sections.
- Each card: one strong title + one short paragraph. If a card needs a list, bullet points, or multiple paragraphs, it is not a summary — move the detail elsewhere.
- Card text volume should be visually balanced. If one card has 3 lines and another has 10 words, redistribute.

### Architecture Diagram (.architecture-flow)
- Always use the three-column grid: left context → center detail → right context.
- Column widths must use the same `grid-template-columns` across all architecture diagrams on the page.
- Use `align-items: stretch` on `.architecture-flow` so the three outer cards stay equal height. The misalignment bug is fixed inside `.diagram-card`, not by making the outer cards different heights.
- Every `.diagram-card` must use the same internal layout:

  ```css
  .architecture-flow {
    align-items: stretch;
  }

  .diagram-card {
    display: grid;
    grid-template-rows: auto 1fr;
    gap: 10px;
  }

  .diagram-card h3 {
    margin: 0;
    line-height: 1.5;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .diagram-card > :not(h3) {
    align-self: start;
  }
  ```

- Diagram card titles must be single-line and top-aligned. If a title wraps, shorten the label before changing card height.
- The first content block inside every `.diagram-card` must rely on the card's `gap`; do not add inline `margin-top` to side columns or center columns.
- Use the same body gap and node padding across side and center columns. A center `.node-grid` should not have a different title-to-first-node rhythm than side-column content.
- App nodes (.node) should be compact. If a node needs more than 2 lines of description, use a separate detail section.
- Split physical deployment from logical application architecture into separate diagrams when a single diagram becomes too dense to scan.

### Milestone Cards (.next-step)
- Always include a priority tag: P0 (critical, near-term) or P1 (important, medium-term).
- Each card should start with or prominently feature an action verb: "完成", "上线", "迁移", "建立".
- Milestone cards are forward-looking. Do not use them for completed work — use matrix cards instead.
- 4-6 cards per grid. Fewer than 3 suggests combining with the plan section.

### Tags (.tag)
- P0 tags must use red styling. P1 tags must use orange styling.
- Do not introduce new tag levels (P2, P3, P-legacy). The system supports exactly two priority tiers.
- Tags are for milestone cards only. Do not add tags to summary cards or architecture nodes.
