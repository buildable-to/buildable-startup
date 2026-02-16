# Buildable — Startup Operations

This is the operational hub for Buildable — managed entirely through Claude Code. We use Claude Code as our startup ops tool: writing strategy docs, managing the project board, doing competitive research, drafting pitch materials, and keeping the team aligned.

**Product repo:** [buildable-to/Buildable](https://github.com/buildable-to/Buildable)
**Project board:** [Buildable Roadmap](https://github.com/orgs/buildable-to/projects/1)

## What is Buildable?

AI-powered structural engineering tool that generates construction-ready 2D drawings from natural language. Describe a foundation element — dimensions, rebar, concrete class — and get complete drawings with plan views, sections, rebar details, and bar bending schedules.

Built on FreeCAD (open-source parametric CAD) with a proprietary AI layer.

**Target vertical:** Precast concrete structural engineering

## How We Use Claude Code

This repo is operated through Claude Code (Anthropic's CLI tool). Instead of manually editing docs and managing tasks, we tell Claude Code what needs to happen and it:

- **Writes and updates docs** — strategy, competitive teardowns, pitch materials, interview notes
- **Manages the project board** — creates GitHub issues, assigns owners, sets milestones, tracks status via `gh` CLI
- **Does competitive research** — signs up for competitors, documents findings, writes teardowns
- **Drafts content** — LinkedIn posts, pitch deck outlines, grant applications
- **Keeps everything consistent** — follows the conventions in `CLAUDE.md` so docs stay structured

### Workflow

1. Open Claude Code in this repo
2. Describe what you need ("create a task for X", "update the competitive teardown for Y", "draft a LinkedIn post about Z")
3. Claude Code reads `CLAUDE.md` for context, edits the right files, and manages the board

No Jira, no Notion, no context-switching. The repo _is_ the project management tool, and Claude Code _is_ the operator.

## Team

- **Luka** — Technical lead. Builds the product.
- **Otar** — Business lead. Strategy, GTM, sales, fundraising. Primary operator of this repo.
- **Nikoloz** — Domain expert. Civil engineer, upcoming CTO of Georgian Precast Association.

## Repo Structure

```
buildable-startup/
├── CLAUDE.md              # Instructions for Claude Code (read on every session)
├── README.md              # This file
├── strategy/              # Strategic planning docs
├── customers/             # Customer discovery interviews and tracking
├── pitch/                 # Fundraising materials
├── competitive/           # One file per competitor teardown
└── content/               # Marketing content (LinkedIn, etc.)
```

## Key Milestones

| Milestone | Deadline | Status |
|-----------|----------|--------|
| M1-3: Prove the Wedge | March 1, 2026 | **Active** |
| M4-6: First Revenue | June 1, 2026 | Upcoming |
| M7-9: Validate PMF | September 1, 2026 | Planned |
| M10-12: Scale Signal | December 1, 2026 | Planned |
