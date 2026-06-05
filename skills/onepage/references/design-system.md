# Presentation HTML — Core Methodology

Always read this file when generating a presentation HTML report. It contains the design principles, pattern selection rules, visual language, wording guidance, and review checklist — the minimum context needed for every generation task.

For layout details and component specs, read [layout-reference.md](layout-reference.md) when building or tuning the page structure. For large-content chaptering, iteration guidance, and known limitations, read [advanced-guide.md](advanced-guide.md) when the task is complex.

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

## Design Principles

These principles explain why the visual language and layout rules exist. When you encounter a scenario not covered by a specific rule, fall back to these principles rather than inventing a new pattern.

1. **Density serves scanning.** This system targets leadership audiences who need to grasp status in seconds. 14px body text, compact cards, and tight spacing are deliberate — they maximize information per viewport. If a layout feels "spacious enough to relax in," it is probably too loose for a presentation report.

2. **Color is classification, not decoration.** Every color in this system carries a fixed semantic meaning. Blue = deployed/runtime. Green = shared support. Orange = in-progress. Purple = external. Yellow = storage. Red = risk/governance. Using color for visual variety (e.g., making every card a different color "to look nice") breaks the system. If two things share a color, the reader will assume they share a category.

3. **One card, one idea.** Each card should answer a single question for the reader. If you find yourself writing "and also" inside a card, split it. Dense evidence, multi-point comparisons, and implementation details belong in dedicated blocks — not inside a card that also carries a headline.

4. **Hierarchy through structure, not font size.** The system uses a limited type scale (14px body, 15px card title, 17px h3, 23px h2, 34px h1). Visual hierarchy comes from position (hero → nav → sections), container weight (white panel with shadow), and structural role (summary card vs detail card) — not from introducing new font sizes or weights.

5. **Content drives structure, not the reverse.** Start from the source material's natural shape, then choose a narrative structure. Forcing content into a fixed section template (always: overview → architecture → done → plan → milestones) produces mechanical pages. The page modes (executive report, roadmap, technical explainer, etc.) exist precisely to avoid this trap.

6. **Self-contained means no excuses.** Every output must work as a single `.html` file — no CDN calls, no external fonts, no image references. This constraint is non-negotiable because the primary distribution channel is email attachment or chat file-share, where network conditions are unknown.

## Do's and Don'ts

### Do

- Do decide the page mode before writing any HTML. The mode determines which sections exist and which visual patterns apply.
- Do assign semantic colors at the page level before filling content. Map categories (deployed, shared, in-progress, external, storage, risk) to colors once, then use consistently.
- Do use business-readable names as primary labels. "订单服务" not "order-service-v2-prod". Internal identifiers belong in secondary text only.
- Do keep card text under 3 lines. If you need more words, the card is trying to do too much — split or move detail to a dedicated section.
- Do give each chapter a single takeaway. If a chapter has no clear point, merge it with an adjacent one or convert it to supporting detail.
- Do return to white background between major sections. The white panel + shadow rhythm creates visual separation without relying on color variation.
- Do check architecture diagram column widths against each other. Related diagrams that use different column widths feel like they belong to different pages.

### Don't

- Don't use color to indicate priority. Priority is communicated by P0/P1 tags and card ordering. Color is reserved for semantic categories.
- Don't place internal system IDs, environment variable names, or deployment hostnames as primary labels. These are implementation details that break readability for the target audience.
- Don't mix more than two visual patterns in one chapter. If a chapter has metric cards AND a comparison table AND an architecture diagram, restructure it into sub-sections or separate chapters.
- Don't create a legend for architecture diagrams when the card labels and color semantics already make categories obvious. Legends add clutter without adding information.
- Don't repeat the same capability in multiple cards. Establish it once in its canonical location, then reference by name elsewhere.
- Don't use rounded pill buttons, gradient backgrounds, or drop shadows on individual cards. The system uses flat white panels with 8px radius and subtle shadow — adding stronger visual treatments breaks the consistent rhythm.
- Don't flatten large material into a single long list. If you have more than 6 cards of the same type, group them into sub-sections or switch to a table format.

## Visual Pattern Selection

Use this decision table when assigning a dominant visual pattern to each chapter. Every chapter should have one primary pattern; a short note or secondary detail block may accompany it.

| Pattern | When to use | When NOT to use |
|---|---|---|
| **Metric cards** (summary-grid) | Status snapshots, KPI overviews, count-based summaries where each card answers "how many" or "what status" | When cards would need paragraphs to explain — use a detail section instead |
| **Architecture diagram** (architecture-flow) | Explaining system structure, platform composition, service relationships, deployment topology | When the material is sequential (use timeline) or comparative (use matrix) |
| **Comparison matrix** (matrix-grid) | Comparing alternatives, teams, systems, options, or before/after states side by side | When items have no shared comparison dimensions — use separate cards |
| **Timeline / Roadmap** | Sequential events, version plans, migration phases, milestone sequences | When order doesn't matter — use thematic grouping instead |
| **Milestone cards** (next-grid with P0/P1 tags) | Action-oriented next steps with priority, owner, and concrete outcome | For historical accomplishments — use regular cards without priority tags |
| **Detail table** | Dense facts that must stay visible: feature lists, configuration tables, dependency matrices | When the reader needs a quick takeaway — use cards instead |
| **Risk register** | Uncertainty tracking with likelihood, impact, and mitigation | When all items are confirmed facts with no uncertainty |
| **Chaptered long-form** (multiple section blocks) | Very large inputs (>5000 words) covering multiple themes, systems, or time periods | When the material fits naturally into 3-5 sections without forced grouping |

### Pattern Combination Rules

- A chapter may combine its primary pattern with one secondary element: a short note block, a diagram-note annotation, or a small inline table.
- If two patterns feel equally important, split the chapter into two sub-sections.
- The hero section always uses metric cards. Do not place architecture diagrams or long text in the hero.
- Navigation anchors should reflect chapter purpose, not pattern type. "Current Status" not "Card Grid".

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
