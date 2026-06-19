# Proposal: Skills Section

## Intent

The deck's rail already has a broken Module 3 entry for Skills (`data-first="13"` → should be `8`, `id="dots-7"` → should be `dots-3`), but no slides exist. Skills are a core differentiator of Gentle AI — they solve the `Agents.md` scaling problem, introduce lazy-loading via triggers, and enable the orchestrator pattern. Adding a dedicated section completes the broken module and gives viewers the full chain: why skills exist → how they work → how they enable divide & conquer.

## Scope

### In Scope
- 3 new slides for module 3 (indices 8–10)
- Rail fixes: `data-first` and `dots-id` corrections
- Speech reorganization: group existing Skills/God-agent/Divide&Conquer notes under module 3
- HTML/CSS layouts for figure areas (no SVG, no images)

### Out of Scope
- Module 4 (MCP) — remains commented out
- Content changes to existing slides 0–7
- JavaScript/behavior changes (counter and dots auto-build work with correct attributes)

## Capabilities

### New Capabilities
- `skills-presentation`: Slide module explaining Gentle AI Skills — motivation (Agents.md limits), trigger-based lazy loading, and how skills enable the orchestrator's divide-and-conquer architecture

### Modified Capabilities
None — existing modules (ecosystem, SDD, Engram) are unchanged at the spec level

## Approach

1. **Rail fixes**: Change `data-first="13"` → `data-first="8"`, `id="dots-7"` → `id="dots-3"`
2. **Slide 8** — "Why Skills?": Agents.md grows with the project → more tokens → more hallucinations. Skills modularize conventions, load on demand.
3. **Slide 9** — "Trigger System": Each skill declares trigger conditions (file patterns, task descriptions). The agent loads matching skills only. Lazy loading keeps context lean.
4. **Slide 10** — "Divide & Conquer": Even with skills, one agent fills context. Solution: orchestrator delegates to sub-agents with fresh context + their own loaded skill.
5. **Speech**: Reorganize existing notes (Speech lines 22–40) under a `## Skills` section header
6. **Figures**: HTML/CSS layouts — keyword boxes, flow arrows, structured cards. No SVG, no images.

## Affected Areas

| Area | Impact | Description |
|------|--------|-------------|
| `index.html` | Modified | Fix rail attrs (2 lines), add 3 slide `<article>` blocks (~150 lines each) |
| `speech.md` | Modified | Add `## Skills` section header, group existing notes 22–40, add per-slide anchors |
| `assets/css/styles.css` | Unchanged | Existing slide + content styles handle new slides |

## Risks

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Slide count mismatch after adding 3 slides | Low | JS `slides.length` auto-computes counter — no manual updates needed |
| `buildDots()` fails if `dots-3` container doesn't exist | Low | Only fires if `container` not found (already has guard: `if (!container) return`) |
| Audio sync for slides 9–11 out of sync | Low | Rehearse after speech reorg |

## Rollback Plan

1. Revert `data-first` and `dots-id` values to originals
2. Remove 3 new `<article>` slide blocks from `index.html`
3. Restore `speech.md` from git: `git checkout -- speech.md`

## Dependencies

- None — pure HTML/CSS changes, no build step or package update

## Success Criteria

- [ ] Rail Module 3 (Skills) shows 3 dots, clicking navigates to slide 8
- [ ] All 3 slides render with correct content, kicker numbers, and tone class
- [ ] Counter shows `11 / 11` on last slide (was `08 / 08`)
- [ ] Speech notes flow logically: Skills → God Agent → Divide & Conquer → SDD
- [ ] Existing slides 0–7 unchanged in behavior, content, or animation
