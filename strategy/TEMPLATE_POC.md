# Drawing Templates PoC Plan

## What We're Proving

One question: **Does inner Claude produce better shop drawings when it can read a validated template file, compared to writing from scratch?**

That's it. If yes, we expand the template library. If no, we rethink.

---

## What Is a Template

A template is a **complete, tested FreeCAD Python script** that produces one correct drawing. It lives on disk as a `.py` file. Inner Claude reads it with the Read tool when relevant, adapts the values (dimensions, rebar, spacing), and writes a new script based on it.

Templates are NOT executed directly. They're reference code — like copying from a working example instead of guessing.

---

## Architecture (Minimal for PoC)

```
src/Mod/DrawingAssistant/
├── templates/
│   ├── INDEX.md                    ← Short manifest: what's available, when to use it
│   ├── beam_shop_drawing.py        ← Complete beam shop drawing (elevation + section + BBS)
│   └── _engineering_helpers.py     ← Shared helper functions (stirrup drawing, BBS, etc.)
├── backends/
│   └── claude_code.py              ← Add ~5 lines: tell inner Claude about templates/
```

**System prompt addition** (appended to existing prompt, ~100 tokens):

```
## Templates
Validated drawing templates are available at: {templates_dir}
Read templates/INDEX.md to see what's available.
When creating a drawing that matches a template, read the template first and adapt it.
Do NOT copy templates verbatim — adapt dimensions, rebar, and layout to the user's request.
```

**Everything else stays the same.** Executor, review kit, sandbox, multi-page system — untouched.

---

## The First Template: Beam Shop Drawing

Written from scratch by hand. No copying from luka_52 or other test outputs — every line intentional, every API call understood. This is how you learn the real FreeCAD gotchas that become SKILL.md later.

### What a beam shop drawing must contain

A beam shop drawing is what the factory worker reads to build one concrete beam. It fits on a single A3 sheet and contains these views:

#### View 1: Longitudinal Elevation (side view of the beam)
The main view. Shows the beam from the side, full length.

Must show:
- **Beam outline** — rectangle: span length × depth
- **Support blocks** — small rectangles at each end (where the beam sits on columns)
- **Bottom reinforcement bars** — drawn as double lines running the full span, with hooks at each end bending up
- **Top reinforcement bars** — double lines running the full span, hooks bending down
- **Stirrups** — vertical double lines at regular spacing. Two or three zones with different spacing (closer together near supports where shear is highest, wider apart in the middle)
- **Section cut markers** — dashed line with "A-A" labels showing where the cross-section is cut
- **Dimensions** — overall span, depth, stirrup zone lengths
- **Labels** — bar position numbers (Pos 1, Pos 2, Pos 3), stirrup spacing per zone

Typical scale: **1:25 or 1:50** depending on beam length.

#### View 2: Cross-Section (cut through the beam, section A-A)
Shows what you'd see if you sliced the beam perpendicular to its length.

Must show:
- **Concrete outline** — rectangle: width × depth
- **Stirrup** — double-line rectangle inside the outline (offset by concrete cover)
- **Bottom bars** — filled circles at correct positions
- **Top bars** — filled circles at correct positions
- **Cover dimensions** — distance from concrete face to stirrup (typically 25-40mm)
- **Overall dimensions** — width and depth
- **Bar labels with leaders** — lines pointing from bar dots to labels (e.g. "4T20", "2T12")

Typical scale: **1:20** (larger than elevation because it's a smaller view).

#### View 3: Bar Shape Diagrams
Shows each rebar type flattened out so the factory knows what shape to bend.

Must show per bar position:
- **Shape outline** — the bar shape drawn flat (straight bar with hooks, stirrup rectangle, etc.)
- **Dimensions** — hook length, straight length, bend diameter
- **Label** — position number, diameter, shape code (e.g. "Pos 1 d20 SC-11"), cut length

#### View 4: Bar Bending Schedule (BBS)
A table listing every bar in the beam.

Columns: Position | Diameter | Shape | Cut Length | Quantity | Unit Weight | Total Weight

This uses FreeCAD's Spreadsheet workbench, embedded into TechDraw as a DrawViewSpreadsheet.

#### View 5: Notes
Standard text blocks:
- **Material specification** — concrete grade, steel grade, cover, exposure class
- **General notes** — construction notes (lap lengths, placing, vibration, etc.)

#### Sheet Layout (A3 Landscape)

```
┌────────────────────────────────────────────────────────────────────┐
│                                                                    │
│   ┌── Elevation (1:50) ──────────────────────────────────────┐    │
│   │                                                          │    │
│   │   [full beam side view with rebar and stirrups]          │    │
│   │                                                          │    │
│   └──────────────────────────────────────────────────────────┘    │
│                                                                    │
│   ┌── Section ──┐    ┌── Bar Shapes ─────────┐                    │
│   │             │    │                       │                    │
│   │  [A-A cut]  │    │  Pos 1: ──┐  ┐──     │                    │
│   │   (1:20)    │    │  Pos 2: ──┘  └──     │                    │
│   │             │    │  Pos 3: ┌──┐          │                    │
│   └─────────────┘    └───────────────────────┘                    │
│                                                                    │
│   ┌── Notes ────┐    ┌── Bar Schedule ───────────────────────┐    │
│   │ Material    │    │ Pos │ Ø │ Shape │ Length │ Qty │ Wt  │    │
│   │ General     │    │  1  │20 │ SC-11 │ 6330  │  4  │ ... │    │
│   └─────────────┘    └───────────────────────────────────────┘    │
│                                                            [title]│
└────────────────────────────────────────────────────────────────────┘
```

---

## Steps

### Step 1: Nikoloz review (BEFORE writing code)
**Effort:** 30 min conversation

Show Nikoloz:
1. The sheet layout diagram above — "Is this what goes on a beam shop drawing? What's missing?"
2. The luka_52 screenshot — "On 1-10, how close is this to what you'd produce?"
3. Ask: "What element do your engineers draw the most — beams, columns, slabs?"
4. Ask: "Do your clients also need GA drawings or just shop drawings?"

**Do NOT start coding until Nikoloz confirms the content is right.** He might say "you're missing lifting inserts" or "we don't do bar shape diagrams, we use a different format" — and that changes everything.

### Step 2: Write beam template from scratch
**Effort:** 1-3 days

Fight the FreeCAD API. Build one piece at a time:

1. **Day 1: Elevation view** — beam outline, support blocks, rebar lines with hooks, stirrups
2. **Day 2: Cross-section + bar shapes** — the simpler geometric views
3. **Day 3: BBS + notes + layout** — tables, text, and fitting everything on A3

**Document every API pain point as you go.** These become SKILL.md entries later.

### Step 3: Create template directory + INDEX.md
**Effort:** 30 minutes

### Step 4: Wire into system prompt
**Effort:** 30 minutes

### Step 5: A/B test
**Effort:** 1-2 hours

Same prompt, two runs:
- **Without template**: "Draw a beam shop drawing: 8000mm span, 400×600mm, 6T25 bottom, 2T16 top, T10@125/175 stirrups"
- **With template**: same prompt, template system enabled

### Step 6: Nikoloz review of outputs
**Effort:** 30 min meeting

---

## Success Criteria

| Criteria | How to Measure |
|---|---|
| Inner Claude reads the template | Check tool calls — does it Read beam_shop_drawing.py? |
| Output has all required elements | Elevation, section, BBS, dimensions, notes all present |
| Output adapts to different parameters | Different beam = different drawing, not a copy |
| Better than without template | Fewer API errors, fewer review iterations, cleaner layout |
| Nikoloz says it's recognizable | Rating >= 5/10 on template-assisted output |

---

## After PoC: If It Works

1. Ask Nikoloz: what's the next most common shop drawing? (probably column)
2. Create column shop drawing template
3. Build up template library one at a time, each validated by Nikoloz
4. Eventually refactor system prompt rules into readable SKILL.md file
5. Explore: can Claude help write new templates faster?

## After PoC: If It Doesn't Work

Possible failure modes:
- **Claude ignores the template** → Make template reading mandatory, not optional
- **Claude copies verbatim without adapting** → Stronger "ADAPT, don't copy" instructions
- **Template is too long** → Split into focused sub-templates (section-only, elevation-only)
- **Output quality still bad** → Problem is FreeCAD rendering, not templates. Investigate TechDraw pipeline
- **Nikoloz rates below 4/10 even with template** → Template itself needs iteration with Nikoloz
