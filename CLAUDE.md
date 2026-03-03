# CLAUDE.md — Buildable Startup Operations

## What This Repo Is

This is the operational hub for Buildable, managed entirely through Claude Code. It contains strategy docs, customer research, pitch materials, competitive intel, and business planning.

Buildable is an AI-native structural engineering tool — a web-based drawing assistant that generates DXF files from natural language descriptions.

**The product codebase lives at:** github.com/buildable-to/ezdxf-flask (previously github.com/buildable-to/Buildable when we were FreeCAD-based)

## How This Repo Works

This repo replaces Jira/Notion/Google Docs. Claude Code is the primary operator:

- **Project management** — GitHub Issues + the [project board](https://github.com/orgs/buildable-to/projects/1) are the single source of truth. Create, update, and track tasks using `gh` CLI. All issues go in `buildable-to/buildable-startup` to keep everything on one board.
- **Documentation** — All docs live in this repo as markdown. Edit existing files, don't create duplicates.
- **Competitive intel** — One file per competitor in `competitive/`. Research, sign up, document.
- **Content** — LinkedIn posts, pitch materials, grant applications — all drafted here.

When a team member opens Claude Code in this repo, `CLAUDE.md` provides full context so Claude can operate autonomously — create tasks, update docs, draft content, manage the board.

## Team

- **Luka Lortkipanidze** — Technical lead. Builds the product. Works in the Buildable repo.
- **Otar Donadze** — Business lead. Strategy, GTM, sales, fundraising. Primary user of this repo.
- **Nikoloz Lortkipanidze** — Domain expert. Civil engineer, CTO of Georgian Precast Association. Validates engineering output and opens doors to customers.

## Context

- **Product:** AI assistant that generates construction-ready 2D drawings (plan views, sections, rebar details, bar bending schedules) from natural language descriptions
- **Target vertical:** Precast concrete structural engineering
- **Key insight:** One of Georgia's biggest precast companies spends 2 months on design/drawings but only 15 days on actual construction. The bottleneck is paperwork, not building.
- **Stack:** Web-based Flask app using ezdxf for DXF generation, Claude CLI as coding agent (previously built on FreeCAD fork, moved to web-based approach)
- **AI approach:** Code-as-source-of-truth — Claude Code writes/edits Python drawing.py scripts that generate DXF files. The script is the source of truth, the DXF is just the build output.

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
