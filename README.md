# 🦞 OpenClaw Intelligence Hub

> **The design system for an 8-agent AI intelligence colony.**  
> Architecture decisions, agent specifications, configuration schemas, and a living user guide — all in one place.

---

## What This Is

This repository is the **design system and operational brain** of the OpenClaw Intelligence Hub — a colony of 8 specialized AI agents that collect, verify, narrate, remember, forecast, optimize, teach, and maintain an ongoing intelligence feed.

This is **not** the runtime. The deployed agents live in [clawroman-fortress](https://github.com/YOUR_USERNAME/clawroman-fortress). This repository is what tells them how to think, what to monitor, and how to talk to each other.

---

## The Eight Agents

| Icon | Agent | Primary Role |
|------|-------|-------------|
| 📡 | **Scout** | Sense — finds signals across the intelligence network |
| 😈 | **Critic** | Verify — trust-scores all incoming content |
| 📰 | **Scribe** | Narrate — produces the daily intelligence briefing |
| 📚 | **Librarian** | Remember — manages the vector store and memory |
| 🌊 | **Weatherman** | Forecast — makes and tracks falsifiable predictions |
| 🪙 | **Token Miser** | Optimize — governs model routing and inference costs |
| 🎓 | **Teacher** | Explain — makes complex concepts accessible |
| 📖 | **Editor** | Maintain — keeps the Living User Guide current |

---

## Repository Structure

```
openclaw-intelligence-hub/
│
├── docs/                          # Architecture documentation
│   ├── 01-lobster-anatomy.md      # THE ROSETTA STONE — all terminology defined here
│   ├── 02-scout-keywords.md       # Scout keyword configuration (121 terms, 3 layers)
│   ├── 03-influencer-registry.md  # Human intelligence network (7 tiers)
│   └── architecture/
│       └── decisions.md           # All Architecture Decision Records (ADR-001–010)
│
├── prompts/                       # Agent specifications
│   ├── agents/                    # System prompts for all 8 agents
│   │   ├── scout.md
│   │   ├── critic.md
│   │   ├── scribe.md
│   │   ├── librarian.md
│   │   ├── weatherman.md
│   │   ├── token-miser.md
│   │   ├── teacher.md
│   │   └── editor.md
│   └── config/                    # Agent configuration (domain-specific, separate from prompts)
│       ├── weatherman-bellwether.md   # Bellwether Framework + prediction ledger
│       └── librarian-vectorstore.md  # Vector store schema + retrieval patterns
│
├── guide/                         # Living User Guide
│   ├── README.md                  # Guide navigation and compass paths
│   └── chapters/                  # Ten chapter skeletons (content added by colony)
│       ├── ch01-what-is-an-agent.md
│       ├── ch02-lobster-explained.md
│       ├── ch03-first-agent-build.md
│       ├── ch04-daily-briefing.md
│       ├── ch05-ai-in-finance.md
│       ├── ch06-cost-optimization.md
│       ├── ch07-building-a-colony.md
│       ├── ch08-living-guide.md
│       ├── ch09-security-and-trust.md
│       └── ch10-the-forecast.md
│
├── assets/
│   └── diagrams/                  # Mermaid diagrams (colony structure, flows)
│
├── .github/
│   └── ISSUE_TEMPLATE/
│       └── stale-content.md       # Reader feedback template
│
├── CHANGELOG.md
└── README.md                      # This file
```

---

## The Lobster Metaphor

The entire system uses lobster biology as its architecture metaphor. This is not decoration — it is load-bearing. Every concept maps to a specific anatomical structure, and the mapping holds under technical scrutiny.

**Start here:** [`docs/01-lobster-anatomy.md`](docs/01-lobster-anatomy.md) — the authoritative Rosetta Stone. When any term is ambiguous anywhere in this repository, the anatomy document resolves it.

---

## Configuration Portability

This system enforces strict separation between **framework logic** (agent prompts) and **domain configuration** (keywords, influencers, categories). The agents are domain-agnostic. The config files are user-specific.

This means the entire framework can be deployed for any domain — finance, research, sports analytics, anything — by replacing the config files without modifying agent prompts.

See [`docs/architecture/decisions.md`](docs/architecture/decisions.md) → ADR-006 for the full rationale.

---

## Key Decisions

All architectural decisions are permanently recorded in [`docs/architecture/decisions.md`](docs/architecture/decisions.md).

| ADR | Decision | Status |
|-----|----------|--------|
| ADR-001 | Lobster biology as system metaphor | ✅ Accepted |
| ADR-002 | Eight-agent colony structure | ✅ Accepted |
| ADR-003 | OpenRouter as model routing layer | ✅ Accepted |
| ADR-004 | Librarian as dedicated memory agent | ✅ Accepted |
| ADR-005 | Librarian icon: 🧠 → 📚 | ✅ Accepted |
| ADR-006 | Configuration portability | ✅ Accepted |
| ADR-007 | Four-category content routing | ✅ Accepted |
| ADR-008 | Two-repo strategy | ✅ Accepted |
| ADR-009 | Drone Factory (future system) | 🅿️ Parked |
| ADR-010 | UX Wrapper (future build) | 🅿️ Parked |

---

## Related Repository

**[clawroman-fortress](https://github.com/YOUR_USERNAME/clawroman-fortress)** — the runtime. Deployed agent instances, VPS configuration, and operational runbooks for the Hostinger VPS deployment (Ubuntu 24.04, IP 187.77.102.162).

This repository = **what the agents know and how they think.**  
clawroman-fortress = **where the agents live and run.**

---

## Molt Cycle (Versioning)

| Type | Format | Cadence |
|------|--------|---------|
| Major | X.0.0 | ~Monthly — structural changes |
| Minor | X.Y.0 | ~Biweekly — new content or agent updates |
| Patch | X.Y.Z | 1-3 days — corrections |
| Security | !X.Y.Z | Hours — immediate |

Current version: **v1.0.0** — Foundation complete. All design documents locked. Deployment pending.

---

*Built on the OpenClaw framework. Architecture by the colony. Maintained by the Editor.*
