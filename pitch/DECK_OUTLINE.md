# Pitch Deck v1 — Outline

*Target: 10 slides. Lead with pain, not technology.*

## Slide 1: The Problem
**"2 months of drawings for 15 days of construction"**

One of Georgia's biggest precast companies told us their design/drawing phase takes 2 months. Actual construction takes 15 days. They spend 4x longer on paper than on concrete.

This isn't unique — it's the industry norm.

## Slide 2: Who Has This Problem
- Precast concrete manufacturers globally ($143-155B market)
- Every precast plant has 2-5 structural engineers doing drawings
- Average cost: $30K+/year on drawing production (Georgia), $100K+ internationally
- Tools: AutoCAD (manual, slow), Tekla ($10-20K/seat/year, overkill)

## Slide 3: The Solution
**Describe your element. Get construction-ready drawings in minutes.**

Buildable generates complete 2D construction drawings — plan views, sections, rebar details, bar bending schedules — from a natural language description.

[Screenshot / video of the flow]

## Slide 4: Demo
Live demo or embedded video showing:
- Engineer types: "Foundation 3000x1500x400, C30/37, 8Ø16 bottom, 6Ø12 top, stirrups Ø8@200"
- Buildable generates: complete drawing sheet with all views + BBS
- One parameter change → everything regenerates

## Slide 5: How It Works
- Built on FreeCAD + OpenCASCADE (same geometry engine as SolidWorks)
- AI edits Python code that defines the design (code-as-source-of-truth)
- Version controllable, reproducible, git-friendly
- Open-source base, proprietary AI layer

## Slide 6: Market
- CAD software: $12-23B (6.2% CAGR)
- Precast concrete: $143-155B globally, growing 4.5-5.7%
- No dominant "precast AI" exists
- Expansion: precast → structural steel → general structural → full CAD

## Slide 7: Competition
| | Tekla | AutoCAD | Adam | Zoo | Buildable |
|--|-------|---------|------|-----|-----------|
| Precast-specific | ✓ | ✗ | ✗ | ✗ | ✓ |
| AI-powered | ✗ | ✗ | ✓ | ✓ | ✓ |
| Affordable | ✗ ($10-20K/yr) | ~✓ ($2K/yr) | ? | Free tier | ✓ |
| 2D drawing output | ✓ | ✓ | ✗ | ✗ | ✓ |
| Open source | ✗ | ✗ | ✗ | Partial | ✓ |

## Slide 8: Traction
- Working product: AI assistant generating 2D drawings
- [X] customer conversations completed
- [X] design partners signed / in pipeline
- Georgian Precast Association (umbrella org) as launch partner
- [Any metrics: drawings generated, time saved, etc.]

## Slide 9: Team
- **Luka Lortkipanidze** — Technical lead. ML/Data Engineering, Ex-Tether, Co-founded Bitpulse. Builds the AI layer.
- **Otar Donadze** — Business lead. 1.5 years working with Luka at Bitpulse. Strategy and GTM.
- **Nikoloz Lortkipanidze** — Domain expert. Civil engineer, CTO of Georgian Precast Association. Built-in distribution to commercial customers.

## Slide 10: The Ask
- **Raising:** $[amount] pre-seed
- **Use of funds:** Expand element library, hire C++/CAD engineer, enter Turkish market
- **Goal:** [X] paying customers, $[X]K MRR by [date]

---

## Notes
- Keep slides visual, not text-heavy
- The "2 months vs 15 days" stat should be the first thing anyone remembers
- Have a live demo ready as backup — if the video doesn't land, show it live
