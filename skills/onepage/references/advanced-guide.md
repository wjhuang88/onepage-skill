# Presentation HTML — Advanced Guide

Read this file when the source material is very large (>5000 words), when iterating on an existing report, or when encountering edge cases not covered by the core methodology. For core methodology, see [design-system.md](design-system.md). For layout and component specs, see [layout-reference.md](layout-reference.md).

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

## Known Limitations

These are documented gaps where the system's constraints produce known imperfections. Do not try to "fix" these with ad-hoc workarounds — they are accepted tradeoffs.

- **Three-column architecture grids look hollow when content is asymmetric.** If the left column has one item and the center has six, the grid will have visible white space. This is preferable to breaking the column alignment. Accept the imbalance or split into separate diagrams.

- **Print mode breaks long tables across pages.** Tables exceeding the printable page height will split mid-row. Mitigation: keep tables under ~15 rows, or place dense tables in a downloadable attachment rather than the printed page.

- **Color semantics conflict when a page covers both technical deployment AND business status.** Blue means "deployed app" in the technical view and "primary status" in the business view. If a page mixes both perspectives, add a small inline color key at the first diagram and keep usage consistent within each section.

- **14px body text is uncomfortable for extended reading.** This is intentional — presentation reports are scanning artifacts, not reading documents. If a section needs more than 3 paragraphs of continuous prose, the material may be better served as a separate document with the report linking to it.

- **No dark mode.** The system is optimized for light-background presentation (projectors, screens, printed paper). Dark mode would require inverting all color semantics and is explicitly out of scope.

- **Chinese and English text alignment is imperfect in architecture nodes.** Mixed-language labels with very different character widths may cause slight misalignment in node grids. This is a limitation of CSS Grid with mixed content — accept it rather than adding alignment hacks.

## Iteration Guide

When modifying an existing report or iterating on a draft, follow these rules to avoid cascading inconsistencies.

1. **Change one chapter at a time.** Read the chapter's current state, decide what to change, update it, then verify that adjacent chapters still flow correctly. Do not edit 5 chapters simultaneously.

2. **When adding a new chapter, decide its visual pattern first.** Look at the existing chapters' patterns and choose one that is NOT already over-represented. A page with 4 card-grid chapters and 0 diagrams probably needs a diagram chapter, not a 5th card grid.

3. **When changing colors, re-verify the entire page.** Color mapping is a page-level decision. Changing "blue = deployed" to "blue = in-progress" in one section breaks the system for every other section that uses blue.

4. **When adjusting a chapter's content, check card balance afterwards.** Adding 3 cards to one chapter while leaving adjacent chapters at 2 cards each creates visual imbalance. Either redistribute content or accept the asymmetry intentionally.

5. **Default to `{typography.body}` (14px/1.65) for all text.** Reach for larger sizes only for section titles and hero elements. Do not introduce 15px, 16px, or 18px body text to "make something stand out" — use card position and structural role instead.

6. **When the source material changes significantly (new sections, removed sections, restructured narrative), start from the Decision Priorities in SKILL.md.** Do not patch the existing HTML structure — rebuild the chapter plan first, then regenerate.

7. **Run the Review Checklist after every iteration**, not just at the end. Catching color inconsistency or card imbalance early prevents compounding errors.
