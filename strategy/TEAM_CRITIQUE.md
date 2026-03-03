# Team Critique — Honest Assessment

*Last updated: 2026-02-10*

## Current Team

| Role | Person | Background |
|------|--------|------------|
| Technical lead | Luka Lortkipanidze | ML/Data Engineering, Ex-Tether, Co-founded Bitpulse |
| Business lead | Otar Donadze | Business major, 1.5 years at Bitpulse with Luka |
| Domain expert | Nikoloz Lortkipanidze | Civil Engineering, Constructor, CTO of Georgian Precast Association |

---

## Critical Gaps

### 1. ~~No CAD/Graphics Software Engineer~~ — RESOLVED

*Previously the biggest gap when Buildable was a FreeCAD fork (C++ codebase with 45K+ commits on Qt6, Coin3D, OpenCASCADE). Moving to a web-based stack (Flask + ezdxf + Claude CLI) eliminated this dependency entirely. The product is now Python all the way through, which matches Luka's strengths. No C++/CAD expertise needed.*

### 2. No Designer/UX Person

Still a gap but less critical now. Moving to a web-based product means full control over UX (no FreeCAD "quirks all the way down"). The chat interface, SVG viewport, layer controls, and approval modal are all custom-built. But nobody on the team is thinking about product design full-time — and Cursor won partly on polish.

### 3. Domain Expertise is Narrow

Nikoloz brings construction/precast — one vertical within one country. CAD serves:
- Mechanical engineering (the biggest CAD market)
- Product design / consumer electronics
- Automotive / aerospace
- Architecture (broader than precast)
- Robotics / manufacturing

Having a precast CTO in Georgia is great for a first beachhead, but it's a very small niche. The risk: building something that works for Georgian precast workflows but doesn't generalize. Adam and Zoo are targeting the massive mechanical engineering market.

### 4. Geographic Disadvantage

All three founders are in Georgia (the country). The AI-CAD startup ecosystem is concentrated in:
- SF/Bay Area (Zoo, Adam, Hestus, Cursor — all YC companies)
- Israel (Leo AI — $9.7M, strong defense/engineering talent pipeline)
- Europe (Backflip)

This means: harder to fundraise (most AI VCs want US-based teams), harder to recruit, harder to get warm intros to enterprise CAD customers at Boeing/Ford/Siemens. Ondsel's team had better geographic positioning and still failed commercially.

### 5. No Previous Exits or Brand Recognition

VCs backing AI-CAD startups are writing checks because of pedigree:
- **Backflip** ($30M) — founder previously built Markforged ($1.8B company)
- **Zoo** ($10M) — Jessie Frazelle is well-known infra engineer, backed by Nat Friedman (GitHub CEO)
- **Adam** ($4.1M) — YC W25, UC Berkeley design program
- **Leo AI** ($9.7M) — Israeli military elite engineering program, former SolidWorks CEO as angel

Bitpulse and tinydot.ai are not household names. Doesn't mean you can't succeed, but the fundraising story has to be 10x stronger on traction and product.

### 6. Bus Factor of One

Still one technical contributor (Luka). But the risk profile has changed: the stack is now Python/Flask/ezdxf — standard web dev, not a 45K-commit C++ fork. If Luka gets stuck, another Python developer could realistically pick up the codebase. Still a real gap — Otar and Nikoloz cannot contribute to code.

### 7. Claude Code Dependency

The entire AI layer is built on Claude Code CLI. If Anthropic:
- Changes Claude Code pricing
- Rate-limits CLI usage
- Deprecates the `--allowedTools` interface
- Gets outperformed by a competitor model for CAD code generation

...there's a single point of failure with zero fallback. Cursor supports 33 models. Buildable's architecture is coupled to one.

### 8. Business Founder Without SaaS/Dev-Tools Experience

Otar's background is in business, but building a developer/engineering tools company is a very specific kind of go-to-market. The sales cycle for CAD software is long, enterprise procurement is painful, and the community-to-commercial pipeline (open source → paid) is a playbook most business founders haven't run before. This is exactly what killed Ondsel.

---

## What's Missing — Hires, Advisors, or Partners Needed

| Gap | What's Needed | Priority |
|-----|---------------|----------|
| ~~C++/CAD engineering~~ | ~~Co-founder or senior hire who knows OpenCASCADE, Qt, computational geometry~~ | ~~Critical~~ — Resolved by moving to web stack |
| Product/UX design | Designer who can make the AI interaction feel magical, not bolted-on | High |
| Mechanical engineering domain | Advisor from mainstream mech-E (not just construction) to validate PMF | High |
| Community building | Someone to build contributor community (FreeCAD forum, YouTube, Discord) | Medium |
| Enterprise sales | Someone who has sold $10K+/yr software to engineering teams | Medium |
| Model-agnostic AI layer | Architecture supporting multiple LLM backends, not just Claude — revisit after revenue | Low |

---

## Counterarguments — What's Working

These are real, not just copium:

1. **The thesis is strong** — code-as-source-of-truth for CAD is genuinely differentiated and currently unoccupied
2. **Timing is right** — post-FreeCAD 1.0, AI models are finally good enough, VC appetite for AI-CAD is proven ($58M+ deployed)
3. **Nikoloz = distribution** — having a co-founder who runs an industry association is a warmer go-to-market than any cold outreach
4. **Luka ships fast** — from first commit to working AI assistant with plan mode, preview, self-review, and agentic learning in under 2 months (solo)
5. **Open source moat** — if a community forms, it becomes a flywheel that funded competitors can't replicate
6. **Georgia = low burn** — the same funding buys 5-10x more runway than a SF-based team

---

## Recommendations

1. **Immediately**: Ship with Claude Code — it works, don't abstract prematurely. Revisit model-agnostic architecture once there's revenue and a clear need.
2. **Within 1 month**: Ship a public demo video — traction > pedigree for early fundraising
3. ~~**Within 3 months**: Find a C++/CAD technical co-founder or contractor~~ — No longer needed after move to web-based stack
4. **For fundraising**: Lead with Nikoloz's precast association as proof of commercial demand, not just the technology
5. **First revenue**: Deploy Buildable at Georgian Precast Association member companies — real users, real feedback, real case studies
