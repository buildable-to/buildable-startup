# CLAUDE.md — Buildable Startup Operations

## What This Repo Is

This is the internal operations repo for Buildable — an AI-native structural engineering tool built on FreeCAD. It contains strategy docs, customer research, pitch materials, competitive intel, and business planning.

**The product codebase lives at:** github.com/buildable-to/Buildable

## Team

- **Luka Lortkipanidze** — Technical lead. Builds the product. Works in the Buildable repo.
- **Otar Donadze** — Business lead. Strategy, GTM, sales, fundraising. Primary user of this repo.
- **Nikoloz Lortkipanidze** — Domain expert. Civil engineer, CTO of Georgian Precast Association. Validates engineering output and opens doors to customers.

## Context

- **Product:** AI assistant that generates construction-ready 2D drawings (plan views, sections, rebar details, bar bending schedules) from natural language descriptions
- **Target vertical:** Precast concrete structural engineering
- **Key insight:** One of Georgia's biggest precast companies spends 2 months on design/drawings but only 15 days on actual construction. The bottleneck is paperwork, not building.
- **Base:** Fork of FreeCAD (open-source parametric CAD on OpenCASCADE kernel)
- **AI approach:** Code-as-source-of-truth — Claude Code edits a Python source.py that defines the design

## How to Help

When editing files in this repo:

1. **Be direct and critical.** This is an internal repo — no sugarcoating. If an idea is bad, say so.
2. **Use data over opinion.** Reference market data, competitor numbers, customer quotes.
3. **Follow YC principles.** Launch fast, talk to users, build what they want, don't die.
4. **Keep docs actionable.** Every doc should have clear next steps, owners, and deadlines.
5. **Update, don't duplicate.** Edit existing docs rather than creating new ones when possible.

## Repo Structure

```
buildable-startup/
├── CLAUDE.md              # This file
├── strategy/              # Strategic planning docs
│   ├── RESEARCH.md        # Competitive landscape, market research
│   ├── STRATEGY.md        # Vertical strategy, YC lessons, execution plan
│   └── TEAM_CRITIQUE.md   # Honest team assessment and gaps
├── customers/             # Customer discovery
│   ├── interviews/        # Individual interview notes
│   ├── INTERVIEW_SCRIPT.md # Standard questions (Mom Test)
│   └── TRACKER.md         # Summary tracker across all interviews
├── pitch/                 # Fundraising materials
│   ├── DECK_OUTLINE.md    # Pitch deck structure and content
│   └── GRANT_TRACKER.md   # Accelerators, grants, deadlines
├── competitive/           # Competitive intelligence
│   └── {competitor}.md    # One file per competitor teardown
└── content/               # Marketing content
    └── linkedin/          # LinkedIn post drafts and ideas
```

## Key Milestones

| Milestone | Deadline | Status |
|-----------|----------|--------|
| M1-3: Prove the Wedge | March 1, 2026 | **Active** — deadline approaching |
| M4-6: First Revenue | June 1, 2026 | Upcoming |
| M7-9: Validate PMF | September 1, 2026 | Planned |
| M10-12: Scale Signal | December 1, 2026 | Planned |

## Project Board

Track all tasks at: https://github.com/orgs/buildable-to/projects/1
