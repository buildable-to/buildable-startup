# BUILDABLE

## Technical Architecture & Execution Plan

**Claude Code + FreeCAD — One System, One Pipeline**

February 2026 | Prepared for Luka, Otar & Nikoloz

---

## Executive Summary

Buildable generates construction-ready 2D structural engineering drawings from natural language descriptions, targeting the precast concrete vertical. Structural engineers spend 80% of their time drafting — Buildable eliminates that bottleneck.

This plan is built on one principle: prove the core hypothesis first, then scale. The core hypothesis is that Claude Code + FreeCAD can produce a drawing that a structural engineer would accept with minimal manual corrections.

### Key Decisions

**1. FreeCAD is the only engine.** One tool for 2D plans, 3D models, section cuts, and rebar detailing. One set of recipes, one API for Claude to learn, no integration headaches.

**2. Drawing correctness is the product.** Not calculations, not 3D visualization. Engineers spend 80% of time drafting. Making correct, dimensioned, annotated 2D drawings is what they'll pay for.

**3. Claude Code stays fully agentic.** Claude writes real FreeCAD Python code, guided by tested recipes and SKILL.md. No rigid JSON schema, no intermediate abstraction layer.

**4. Recipes over reference docs.** Claude fails when given "this is what it should look like." Claude succeeds when given "here is working code that produces it."

**5. Validate before scaling.** Before building 15 recipes and a vision loop, we need to prove that ONE FreeCAD script can produce a drawing Nikoloz rates 6+/10. Everything else is premature until that's confirmed.

**6. Leverage existing open source.** FreeCAD Reinforcement Workbench provides rebar generation with full Python API. Don't rebuild what exists.

---

## System Architecture

### The Problem Today

User describes a structure → Claude Code generates FreeCAD Python from scratch → Script executes → Output.

**Why it fails:** Claude guesses at FreeCAD's API every time. It doesn't reliably know method signatures, coordinate systems, or parameter formats. Most iteration time is spent fighting API errors, not working on drawing logic. Reference documents (showing what the output should look like) don't help because Claude still doesn't know HOW to produce that output in FreeCAD.

### The Solution: Recipe-Driven Generation

Give Claude working code it can adapt, not reference images it can't implement.

| Component | What It Does | Key Point |
|---|---|---|
| **SKILL.md** | Drawing conventions, FreeCAD API patterns, do/don't rules, Nikoloz's corrections | Updated after every review. This is how the system improves. |
| **Recipe Scripts** | Working, tested FreeCAD Python files. Each produces one correct drawing element. | Created manually by Luka. ~50-150 lines each. Created once, reused forever. |
| **Claude Code** | Reads SKILL.md + recipes. Writes adapted FreeCAD Python for the user's specific request. Runs it, debugs errors, iterates. | The agentic loop is the advantage. Claude writes code, runs it, fixes it. |
| **Nikoloz Review** | Quality gate. Reviews output against professional standards. Corrections feed back into SKILL.md. | No automated substitute for this. Don't try to automate it yet. |

**How recipes change Claude's workflow:** Without recipes, Claude writes FreeCAD code from memory → guesses API → errors → 20 minutes, bad result. With recipes, Claude reads working example → adapts coordinates and values → runs → 2-3 minutes, correct result.

### Why FreeCAD Only

FreeCAD's Draft module handles all 2D primitives needed for plan drawings: `Draft.makeLine()`, `Draft.makeRectangle()`, `Draft.makeCircle()`, `Draft.makeText()`, `Draft.makeDimension()`. The same tool also provides:

- **Arch workbench** for 3D structural elements (columns, beams, walls, slabs)
- **TechDraw workbench** for extracting 2D views from 3D models (section cuts)
- **Reinforcement Workbench** (addon) for rebar generation with Python API
- **DXF/DWG export** for interoperability with AutoCAD (future — not in scope for validation phase)

One tool, one set of recipes, one pipeline. Adding a second library would mean two APIs to learn, two sets of recipes to maintain, and integration headaches when plan drawings need to reference section drawings.

---

## The Recipe System

### What a Recipe Is

A recipe is a complete, tested FreeCAD Python script that produces one correct drawing element. It's not a snippet or a function — it's a standalone script that Claude can run, see the output, and adapt.

### Recipe Creation Process

**There is no shortcut.** Each recipe must be created manually by fighting FreeCAD's API firsthand:

- Nikoloz specifies what the correct output looks like (hand sketch or AutoCAD reference)
- Luka writes the FreeCAD Python script, debugging until it produces correct output
- The script is validated: runs headlessly, produces correct visual output
- The script becomes a recipe that Claude can read, adapt, and reuse

**Honest time estimate:** Each recipe will take 1-3 days, not hours. FreeCAD's Draft documentation is sparse, parameter behavior is sometimes surprising, and getting text placement, line weights, and dimension formatting right requires trial and error. This time investment is front-loaded — once a recipe works, Claude can reuse it indefinitely.

### Required Recipes (Priority Order)

#### Phase 1 — Minimum Viable Drawing (Proof of Concept)

| Recipe | What It Produces | Est. Time | Priority |
|---|---|---|---|
| `grid_system.py` | Labeled axes (A,B,C + 1,2,3), axis lines extending beyond grid, circle bubbles with labels | 1-3 days | Critical |
| `column_plan.py` | Columns in plan view as crossed rectangles at grid intersections, with labels (C-1, C-2) | 1-2 days | Critical |
| `dimension_chain.py` | Horizontal + vertical dimension chains between grid axes, proper text formatting and offset | 1-2 days | Critical |
| `title_block.py` | Drawing border, title block with project name, drawing title, scale, date, revision | 1-2 days | Critical |

**Phase 1 output:** A dimensioned column layout plan with grid system and title block. This is the proof of concept that everything else depends on.

#### Phase 2 — Complete Plan Drawing Set

| Recipe | What It Produces | Est. Time | Priority |
|---|---|---|---|
| `beam_plan.py` | Beams between columns with dashed centerlines and labels (B-1, B-2) | 1-2 days | High |
| `slab_plan.py` | Slab outlines with hatching in plan view, slab labels and thickness notation | 1-2 days | High |
| `wall_plan.py` | Walls in plan view with proper line weights and fill patterns | 1-2 days | High |
| `foundation_plan.py` | Foundation layout with footings at column locations, footing dimensions | 1-2 days | High |
| `section_cut_line.py` | Section cut reference lines on plan with arrows and labels (A-A, B-B) | 1 day | High |
| `sheet_orchestrator.py` | Combines elements into multi-sheet drawing set with cross-references | 2-3 days | High |

#### Phase 3 — Sections & Reinforcement Details

| Recipe | What It Produces | Est. Time | Priority |
|---|---|---|---|
| `beam_section.py` | Beam cross-section: outline, dimensions, material hatch | 2-3 days | Medium |
| `column_section.py` | Column cross-section: outline, dimensions, cover notation | 1-2 days | Medium |
| `beam_rebar.py` | Beam section with reinforcement using FreeCAD Reinforcement Workbench API | 2-3 days | Medium |
| `column_rebar.py` | Column section with reinforcement using Reinforcement Workbench API | 2-3 days | Medium |
| `connection_detail.py` | Precast beam-to-column connection: corbel, dowels, neoprene bearing | 3-5 days | Medium |

---

## SKILL.md Structure

SKILL.md is the knowledge base Claude reads before every drawing generation. It encodes drawing standards, API patterns, and lessons learned. It's not magic — it's documentation. But good documentation measurably improves Claude's output.

| Section | Content | Updated By |
|---|---|---|
| **FreeCAD API Patterns** | Working code snippets for `Draft.makeLine()`, `Draft.makeDimension()`, `Draft.makeText()`, etc. Parameter formats, coordinate system notes, common gotchas. | Luka |
| **Drawing Standards** | Line weights (cut=0.7mm, visible=0.35mm, dim=0.18mm), text heights, dimension formatting, hatch patterns, scale conventions. | Nikoloz + Luka |
| **Element Conventions** | Columns in plan = crossed rectangles. Beam labels = B-1 format. Grid bubbles = 10mm diameter circles. Section arrows = specific style. | Nikoloz |
| **Recipe Index** | "To draw a grid system, see recipes/grid_system.py" — pointers to every available recipe. | Luka |
| **Do / Don't Rules** | "NEVER place dimension text inside the element." "ALWAYS chain dimensions from grid to grid." Accumulated from every Nikoloz review. | Nikoloz (via Luka) |
| **Units & Tolerances** | FreeCAD stores everything in mm internally but display units vary. All recipes must use mm explicitly. Dimension precision rules: structural dims to nearest mm, rebar cover to nearest 5mm. Document every unit conversion gotcha here — one wrong unit and every dimension on the drawing is wrong. | Luka |
| **Known Issues** | FreeCAD API pitfalls discovered during recipe development. Workarounds for text placement, coordinate system traps. | Luka |
| **Precast Specifics** | Precast connection types, joint conventions, lifting point notation, embed plate standards. Added as Phase 3 develops. | Nikoloz |

**Key principle:** After every Nikoloz review, update SKILL.md with his corrections. The system improves through knowledge accumulation in this file, not through code changes.

---

## Open Source Leverage

Tools that already exist and should be integrated, not rebuilt:

| Tool | What It Gives You | Integration |
|---|---|---|
| **FreeCAD Draft** | 2D primitives: lines, rectangles, circles, text, dimensions, polygons. Layer management. All scriptable from Python. | Primary drawing engine for plan views. All Phase 1 + Phase 2 recipes use this. |
| **FreeCAD Arch** | 3D structural elements as parametric objects: `Arch.makeStructure()` for columns, beams, walls, slabs. Understands structural hierarchy. | Used in Phase 3 to build 3D model before extracting 2D sections. |
| **FreeCAD TechDraw** | Extract 2D views from 3D models. Section views, projection groups, dimension tools on projected views. | Used in Phase 3 for section cut generation from Arch model. |
| **FreeCAD Reinforcement WB** | Python API for all common rebar types: `makeStraightRebar()`, `makeUShapeRebar()`, `makeSlabReinforcement()`. Also generates rebar BOM and bending schedules. | Used in Phase 3 for rebar detailing. Clone repo, study API, add function signatures to SKILL.md. |

---

## Validation-First Approach

**The biggest risk is not technical architecture.** It's that Claude Code + FreeCAD produces output that's fundamentally not good enough for professional engineers. Structural engineers have extremely high standards. If Buildable's output requires 2+ hours of manual cleanup, the value proposition breaks — an engineer can draft a plan from scratch in 4 hours.

**The test:** Produce ONE correct drawing. Show it to Nikoloz. Ask: "How long would it take you to fix this to contractor-ready quality?"

| Nikoloz Rating | What It Means | Action |
|---|---|---|
| **2-3 / 10** | Fundamental problems. FreeCAD's 2D output doesn't meet basic professional standards. | Investigate whether Draft module is the right approach vs. TechDraw projections from 3D, or reconsider the rendering pipeline entirely. |
| **4-5 / 10** | Recognizable but many convention errors. Fixable with SKILL.md refinement and recipe iteration. | Expected result for first attempt. Catalog every issue, fix recipes, re-test. |
| **6-7 / 10** | Good foundation. Issues are mostly formatting/convention, not structural. | Strong signal. Invest in expanding recipe library. The approach works. |
| **8+ / 10** | Near production quality on first attempt. | Unlikely but ideal. Move fast to Phase 2. |

Do not proceed to Phase 2 until Phase 1 achieves at least 5/10 from Nikoloz. If Phase 1 scores below 4/10 after two iterations, reconsider the FreeCAD Draft approach before investing more time.

---

## Execution: What Actually Matters

No week-by-week timelines. The work is exploratory and the schedule depends on what we learn. What matters is the sequence and the gates.

### Step 1: Prove FreeCAD Output Quality

**Goal:** One correct column layout plan for a simple warehouse, validated by Nikoloz.

**Gate:** Nikoloz rates output ≥ 5/10. Nothing else matters until this is proven.

- Set up FreeCAD headless environment
- Write Phase 1 recipes by hand: grid system, column plan, dimension chains, title block
- First Nikoloz review — record every correction, write SKILL.md v1
- If score < 4/10 after two iterations, reconsider the FreeCAD Draft approach

### Step 2: Prove Claude Can Adapt Recipes

**Goal:** Claude Code generates a correct drawing from natural language by adapting recipes.

**Gate:** Claude-generated output scores within 1 point of hand-crafted recipe output.

- Give Claude the working recipes + SKILL.md, test if it adapts correctly
- Iterate on SKILL.md based on Claude's mistakes — add "NEVER/ALWAYS" rules
- Second Nikoloz review of Claude-generated output vs. hand-crafted

### Step 3: Expand Drawing Coverage

**Goal:** Multiple coordinated drawings from one description.

**Gate:** Complete drawing set that Nikoloz says requires < 1 hour of manual correction.

- Build Phase 2 recipes (beams, slabs, walls, foundations, section cut lines)
- Build sheet orchestrator for multi-sheet sets
- Test with 2-3 structure types (warehouse, multi-story frame, industrial)

### Step 4: Sections & Precast Details

**Goal:** Section cuts with reinforcement details. Precast-specific connection details.

- Set up FreeCAD Arch → TechDraw pipeline for 3D-to-2D sections
- Build Phase 3 recipes using Reinforcement Workbench API
- Precast connection details — the hardest recipe, the most differentiated
- Fourth Nikoloz review: full package. "Would you hand this to a contractor?"

---

## Repository Structure

```
buildable-to/Buildable/
├── SKILL.md                    — Master knowledge file Claude reads before every generation
├── recipes/
│   ├── plan/                   — 2D plan drawing recipes (grid, columns, beams, dims, title block)
│   ├── section/                — Section and detail recipes (beam section, column section)
│   └── rebar/                  — Reinforcement recipes (using Reinforcement Workbench API)
├── examples/
│   ├── warehouse_24x36.py      — Complete working example: full drawing set
│   ├── multi_story_frame.py    — Complete working example
│   └── expected_output/        — Reference DXF/PNG files for validation
├── utils/
│   ├── export.py               — FreeCAD to DXF/PNG export helper
│   └── validate.py             — Check drawing completeness (grids, dims, labels present)
├── src/                        — Core Buildable application code
└── tests/                      — Automated tests: run recipes, compare output to expected
```

---

## Success Metrics

| Metric | Phase 1 Target | Phase 3 Target | Phase 4 Target |
|---|---|---|---|
| Nikoloz rating | ≥ 5/10 | ≥ 7/10 | ≥ 8/10 |
| Manual correction time | < 2 hours | < 1 hour | < 30 minutes |
| Generation time | < 10 min (with Claude iteration) | < 5 min per drawing set | < 10 min for full package |
| Structure types supported | 1 (warehouse) | 3+ (warehouse, frame, industrial) | 4+ with precast details |
| Recipe library size | 4 tested recipes | 10+ recipes | 15+ recipes |
| Export quality | N/A — focus on FreeCAD output | DXF opens in AutoCAD correctly | Production-ready DXF |

---

## Risks & Mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| FreeCAD Draft 2D output quality is insufficient for professional standards | **Critical** — blocks entire approach | This is what Phase 1 validates. Test early, pivot early if needed. Alternative: use Arch 3D → TechDraw 2D pipeline even for plans. |
| Recipe creation takes much longer than estimated | **High** — delays all phases | Start with absolute minimum (grid + columns). One correct plan view is still a compelling demo. Accept 1-3 days per recipe, not hours. |
| DXF export from FreeCAD has compatibility issues with AutoCAD | **High** — engineers won't adopt | Not in scope for validation phase. FreeCAD's native output quality matters first. DXF export is a separate problem to solve later. |
| Claude's FreeCAD API knowledge is poor even with recipes | **Medium** — slower generation | Recipes compensate. The more recipes exist, the less Claude needs API knowledge. Also: SKILL.md with explicit code patterns helps. |
| Unit/tolerance errors in generated drawings | **High** — wrong dimensions destroy trust instantly | FreeCAD internal units are mm but display units can differ. All recipes must explicitly set units. Add unit validation to SKILL.md from day one. One wrong conversion = every dimension wrong. |
| FreeCAD headless mode is unstable on server | **Medium** — deployment issues | Doesn't block local development. Can run FreeCAD with virtual display (xvfb) on server. |
| Nikoloz's standards require too many edge cases | **Low** — scope creep | Focus on 80/20: conventions in every drawing. Edge cases later. |

---

## What To Do This Week

**Forget the 16-week plan.** All that matters right now is proving that FreeCAD can produce a professional-looking plan drawing. Here's what to do:

| Day | Task | What You'll Learn |
|---|---|---|
| **Day 1-2** | Write one FreeCAD Python script by hand. Just a grid system: 4 axes each direction, circle bubbles with labels, axis lines. Fight the Draft API. Document every pain point. | Whether FreeCAD's Draft module is practical for 2D structural drawings. What the real API behavior is vs. documentation. |
| **Day 3** | Add columns at grid intersections (crossed rectangles + labels) and basic dimension chains to the same script. You now have a minimal plan drawing. | Whether dimensions, text, and elements play nicely together. Whether the output looks professional. |
| **Day 4** | Show the FreeCAD output to Nikoloz. One question: "On a scale of 1-10, how close is this to what you'd produce?" Record every correction. | Whether the output gap is bridgeable. What "correct" means in concrete, fixable terms. |
| **Day 5** | Give your working script to Claude Code as a reference. Ask it to generate a similar drawing for different dimensions (e.g., 30x48m warehouse, 8m bays). Does Claude adapt it correctly? | Whether the recipe approach actually works. Whether Claude can modify a working script without breaking it. |

**After these 5 days you'll know three critical things:** (1) whether FreeCAD's 2D is good enough, (2) what Nikoloz specifically needs fixed, and (3) whether Claude can adapt recipes. That's worth more than any plan document. Everything else is speculation until you have this data.
