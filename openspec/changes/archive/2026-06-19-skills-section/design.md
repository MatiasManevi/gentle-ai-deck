# Design: Skills Section (Slides 8–11)

## Technical Approach

Four new HTML slides for Module 3 with pure HTML/CSS figure layouts (no SVGs, no images), two rail fixes to correct the broken Module 3 navigation, and a speech.md reorganization that groups existing notes under `## Skills`. The fourth slide catalogs the curated skills shipped with Gentle AI.

## Architecture Decisions

### Decision: HTML/CSS figures instead of SVGs

| Option | Tradeoff | Decision |
|--------|----------|----------|
| SVG (existing pattern) | Rich graphics, but ~150+ lines per figure, hard to author | ❌ Rejected — proposal explicitly bans it |
| Inline HTML/CSS with `--orange` vars | Simpler markup, reuses existing theme, no new tools needed | ✅ Chosen — figure divs use `class="fig-*"` scoped inside `.slide-figure` |
| External images | Network dependency, breaks offline | ❌ Rejected — violates "no images" constraint |

Figure HTML is placed directly inside `.slide-figure` as `<div>` elements styled via inline-oriented utility classes. The `.slide-figure` CSS already provides the container (`border-radius`, `padding`, `overflow: hidden`). A single CSS block in `<style>` per slide scopes figure-specific layout.

### Decision: Inline `<style>` per figure vs shared CSS

| Option | Tradeoff | Decision |
|--------|----------|----------|
| Shared styles.css classes | More maintainable, but these figures are one-off layouts | ✅ Chosen for class-level layout (flex, grid, colors via vars) |
| Inline `<style>` in each slide | Self-contained, avoids polluting styles.css | ✅ Chosen for figure-specific dimensions, gaps, and spacing |

Existing `.tone-orange` class and `--orange` / `--tone-glow` variables handle all color theming. Layout-specific rules go in `<style>` blocks within each slide (existing convention: app.js uses `data-tone` which auto-applies tone class). No changes to `styles.css` — validated by inspecting existing variable set.

### Decision: speech.md — section header + anchors only

| Option | Tradeoff | Decision |
|--------|----------|----------|
| Rewrite notes entirely | Richer content but scope creep | ❌ Rejected — notes are acceptable as-is |
| Add `## Skills` header + per-slide anchors | Minimal change, keeps existing phrasing | ✅ Chosen — insert `## Skills` between line 21 and 22, add `### Slide N` anchors |

## Data Flow

```
   Rail click: data-first="8" → render(8) → slide 8 active
   buildDots(): slides grouped by data-module → pips in dots-3
   counter: slides.length = 12 → "01 / 12" ... "12 / 12"
```

## File Changes

| File | Action | Description |
|------|--------|-------------|
| `index.html` | Modify | Fix rail: `data-first="13"`→`"8"`, `id="dots-7"`→`"dots-3"` |
| `index.html` | Modify | Add 4 `<article>` slide blocks (indices 8, 9, 10, 11) after slide 7 |
| `speech.md` | Modify | Insert `## Skills` section header + `### Slide N` anchors, group lines 22–40 |
| `assets/css/styles.css` | None | No changes needed — variables and tone classes already exist |

## Interfaces / Contracts

**Slide data contract** (same as existing):

```html
<article class="slide" data-index="8" data-module="3" data-tone="orange">
  <div class="slide-content">
    <p class="slide-kicker">09 · Skills</p>
    <h2>Why Skills?</h2>
    <p>...</p>
  </div>
  <figure class="slide-figure">
    <div class="fig-layout">  <!-- HTML/CSS instead of SVG -->
      ...
    </div>
  </figure>
</article>
```

**Kicker numbering**: slide 8 → `09 · Skills`, slide 9 → `10 · Skills`, slide 10 → `11 · Skills`, slide 11 → `12 · Skills`.

## Testing Strategy

Not applicable — no test framework. Manual verification checklist:

| Layer | What to Verify | Approach |
|-------|---------------|----------|
| Rail | Click Module 3 navigates to slide 8 | Visual + console no-errors |
| Dots | 4 pips under Module 3, clicking navigates correctly | Visual |
| Counter | Shows `12 / 12` on last slide | Visual |
| Animations | slide 8→9→10→11 transitions work | Visual |
| Focus mode | Slides render correctly in focus layout | Visual |
| Existing slides 0–7 | Unchanged behavior, no regressions | Visual diff |

## Migration / Rollout

No migration required. This is additive HTML content with two corrected attribute values. Deploy by replacing `index.html` and `speech.md` in one commit.

## Figure Layouts (Concrete HTML/CSS)

### Slide 8 — Why Skills?

A two-column comparison: **Monolithic Agents.md** (red-tinted, shows the problem) vs **Modular Skills** (orange-tinted, shows the solution). Each side is a bordered card with 3–4 line items. CSS: flex row with `gap`, each card using `--red`/`--orange` border on hover.

```
┌─────────────────────────────────┐
│  [❌ Monolithic Agents.md]       │
│  • Grows with project            │
│  • More tokens                    │
│  • More hallucinations            │
│  ────────────────                 │
│  [✅ Modular Skills]              │
│  • On-demand loading               │
│  • Lean context                   │
│  • Consistent output              │
└─────────────────────────────────┘
```

### Slide 9 — Trigger System

A flow diagram: **Trigger** (keyword/file pattern) → **Skill Loaded** → **Context Injected**. Three horizontal stages connected by arrow characters (`→`). Each stage is a styled `<div>` with border, background, and `--orange` accents.

```
┌──────────┐     ┌──────────┐     ┌──────────┐
│ Trigger  │ ──→ │ Skill    │ ──→ │ Context  │
│ "spec"   │     │ sdd-spec │     │ injected │
└──────────┘     └──────────┘     └──────────┘
```

### Slide 10 — Divide & Conquer

A hub-and-spoke diagram: **Orchestrator** (center, orange glow) with 3 sub-agents radiating (Explore, Implement, Verify). Each sub-agent is a smaller card with `--tone-glow` and a brief description. CSS: flex `row` with centered items, or a grid with the orchestator in the middle.

```
        ┌──────────┐
        │ Explorer │
        └────┬─────┘
             │
    ┌────────┴────────┐
    │  Orchestrator   │
    └────────┬────────┘
             │
        ┌────┴─────┐   ┌──────────┐
        │Implement │   │ Verifier │
        └──────────┘   └──────────┘
```

### Slide 11 — Ecosystem Curated Skills

A categorized grid of skill cards: **SDD Workflow** (init, explore, propose, spec, design, tasks, apply, verify, archive), **Code Quality** (judgment-day, go-testing, branch-pr, chained-pr, work-unit-commits), **Knowledge** (cognitive-doc-design, skill-creator, skill-improver, comment-writer, issue-creation). Each category is a titled card with 3–5 skill names as tags. CSS: 3-column grid using `--orange` borders on cards, `--subtext1` for skill names.

```
┌────────────────────────────────────────────────┐
│  ⚙️ SDD Workflow                   11 skills    │
│  init  explore  propose  spec  design  tasks    │
│  apply  verify  archive  onboard                │
├────────────────────────────────────────────────┤
│  🔍 Code Quality                   5 skills     │
│  judgment-day  go-testing  branch-pr            │
│  chained-pr  work-unit-commits                  │
├────────────────────────────────────────────────┤
│  📖 Knowledge                      5 skills     │
│  cognitive-doc-design  skill-creator            │
│  skill-improver  comment-writer                 │
│  issue-creation                                 │
└────────────────────────────────────────────────┘
```

## Open Questions

- None. All decisions are resolved by existing code patterns and the proposal constraints.
