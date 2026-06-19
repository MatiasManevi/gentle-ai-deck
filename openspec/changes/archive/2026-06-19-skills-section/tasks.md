# Tasks: Skills Section

## Review Workload Forecast

| Field | Value |
|-------|-------|
| Estimated changed lines | ~410 (after removing Slide 10) |
| 400-line budget risk | Low |
| Chained PRs recommended | No (size:exception approved by maintainer) |
| Suggested split | Single PR: rail fixes + speech reorg + slides 8-10 |
| Delivery strategy | exception-ok |
| Chain strategy | size-exception |

Decision needed before apply: No (size:exception approved by maintainer)
Chained PRs recommended: No
Chain strategy: size-exception
400-line budget risk: Low

### Work Units

| Unit | Goal | PR | Notes |
|------|------|----|-------|
| 1 | Rail fixes, speech reorg, slides 8-10 | Single PR | base=main; ~410 lines, size:exception approved. All 3 slides in one PR. |

## Phase 1: Rail Fix

- [x] 1.1 `index.html`: change `data-first="13"` → `"8"` on module 3 rail title
- [x] 1.2 `index.html`: change `id="dots-7"` → `"dots-3"` on module 3 rail dots container

## Phase 2: Slide 8 — Why Skills?

- [x] 2.1 Add `<article>` slide at index 8, `data-module="3"`, `data-tone="orange"`, kicker `09 · Skills`, title "Why Skills?"
- [x] 2.2 Write figure HTML: two-column comparison (Monolithic Agents.md vs Modular Skills) using flex layout with `--red`/`--orange` cards

## Phase 3: Slide 9 — Trigger System

- [x] 3.1 Add `<article>` slide at index 9, `data-module="3"`, `data-tone="orange"`, kicker `10 · Skills`, title referencing triggers
- [x] 3.2 Write figure HTML: three-stage flow (Trigger → Skill Loaded → Context Injected) with arrow separators and `--orange` borders

## Phase 4: Slide 10 — Divide & Conquer (REMOVED)

- [x] 4.1 Slide 10 (Divide & Conquer) was removed mid-apply per user request
- [x] 4.2 Remaining skills slides reindexed: old Slide 11 (Ecosystem) → new Slide 10

## Phase 5: Slide 10 (formerly 11) — Ecosystem Curated Skills

- [x] 5.1 Article slide at index 10, `data-module="3"`, `data-tone="orange"`, kicker `11 · Skills`, title "Ecosystem Curated Skills"
- [x] 5.2 Figure HTML: 3-column grid of categorized skill cards (SDD Workflow, Code Quality, Knowledge) with `--orange` borders

## Phase 6: Speech Reorganization

- [x] 6.1 `speech.md`: insert `## Skills` section header between "Agents.md grow" (line 21) and "Skills" notes (line 22)
- [x] 6.2 `speech.md`: add `### Slide 8`, `### Slide 9`, `### Slide 10` anchors within the new Skills section

## Phase 7: Manual Verification

- [ ] 7.1 Rail: click "4. Skills" navigates to slide 8 — confirm counter shows `09 / 11`
- [ ] 7.2 Dots: 3 pips under Module 3, each pip navigates to correct slide (8, 9, 10)
- [ ] 7.3 Counter: shows `11 / 11` on last slide, `01 / 11` on first
- [ ] 7.4 Slides 0-7: unchanged behavior, no regressions
- [ ] 7.5 Focus mode: all 3 new slides render correctly
