# Skills Presentation Specification

## Purpose

Three-slide module (indices 8–10) explaining why Gentle AI Skills exist, how trigger-based lazy loading works, and cataloguing the curated skills shipped with Gentle AI. Replaces the broken Module 3 rail entry with working navigation and dots.

## Requirements

### Requirement: Rail Navigation Fix

The rail module for "4. Skills" MUST have `data-first="8"` (not `"13"`) and `id="dots-3"` (not `"dots-7"`).

#### Scenario: Clicking the skills rail title navigates to correct slide

- GIVEN the user is on any slide
- WHEN they click the "4. Skills" rail title
- THEN the deck navigates to slide index 8
- AND rail module 3 is marked as the active module

#### Scenario: Dots render under the skills module

- GIVEN `buildDots()` executes
- WHEN it processes slides with `data-module="3"`
- THEN three pips appear inside `#dots-3`
- AND each pip navigates to the correct slide (8, 9, 10)

### Requirement: "Why Skills?" Slide (index 8)

The slide at index 8 MUST present the motivation for skills: Agents.md grows with the project, consuming more tokens and causing hallucinations. Skills modularize conventions and load on demand.

#### Scenario: Slide 8 content renders correctly

- GIVEN the user navigates to slide index 8
- THEN the slide MUST show kicker "09 · Skills", title "Why Skills?", and module 3 tone (`tone-yellow`)
- AND the content MUST explain that Agents.md scales linearly with project complexity, increasing token usage and hallucination risk
- AND the figure MUST use an HTML/CSS layout (keyword boxes, flow arrows — no SVG, no images)

### Requirement: "Trigger System" Slide (index 9)

The slide at index 9 MUST explain that each skill declares trigger conditions (file patterns, task descriptions), and the agent loads only matching skills via lazy loading.

#### Scenario: Slide 9 content renders correctly

- GIVEN the user navigates to slide index 9
- THEN the slide MUST show kicker "10 · Skills" and a title referencing triggers
- AND the content MUST describe how triggers filter which skills enter context
- AND the figure MUST diagram the trigger → skill-load flow with HTML/CSS elements

### Requirement: "Ecosystem Curated Skills" Slide (index 10)

The slide at index 10 MUST present the curated skills that ship with Gentle AI, organized by category (SDD workflow, code quality, documentation, project management).

#### Scenario: Slide 10 content renders correctly

- GIVEN the user navigates to slide index 10
- THEN the slide MUST show kicker "11 · Skills" and a title referencing ecosystem skills
- AND the content MUST list the curated skills grouped by category (SDD, code review, testing, docs, workflow)
- AND the figure MUST display skill cards arranged in a grid using HTML/CSS

### Requirement: Counter Auto-Update

The counter MUST reflect the total number of slides after adding the three new slides.

#### Scenario: Counter shows 11 total slides

- GIVEN the three Skills slides exist in the DOM
- WHEN `slides.length` evaluates during `updateChrome()`
- THEN the counter SHALL display "11 / 11" on the last slide
- AND the counter SHALL display "01 / 11" on the first slide
- AND the progress bar width SHALL be proportional to `(current + 1) / 11`

### Requirement: Speech Reorganization

The speech document MUST group all Skills module notes under a `## Skills` section header.

#### Scenario: Skills notes are grouped

- GIVEN the `speech.md` file
- WHEN a reader scans for Skills content
- THEN existing notes for "Skills" and "God agent" SHALL appear under a `## Skills` header
- AND each slide anchor (8, 9, 10) SHALL be present in the section
