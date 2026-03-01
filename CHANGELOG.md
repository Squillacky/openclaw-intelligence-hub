# Changelog

All notable changes to openclaw-intelligence-hub are documented here.

Format: `[VERSION] YYYY-MM-DD — Description`  
Security patches prefixed with `!` (e.g., `!1.0.1`)

---

## [1.0.0] 2026-02-26 — Foundation Complete

### Added
- `docs/01-lobster-anatomy.md` — The Rosetta Stone. All terminology defined. Locked v1.0.
- `docs/02-scout-keywords.md` — Scout keyword configuration. 121 terms across 3 layers.
- `docs/03-influencer-registry.md` — Human intelligence network. 7 tiers. Tier 7 gap documented.
- `docs/architecture/decisions.md` — Architecture Decision Records ADR-001 through ADR-010.
- `prompts/config/weatherman-bellwether.md` — Bellwether Framework. 8 active predictions. BW-001 confirmed.
- `prompts/config/librarian-vectorstore.md` — Vector store specification. 5 collections. 18 universal metadata fields.
- `guide/README.md` — Guide navigation and compass paths.
- `guide/chapters/ch01` through `ch10` — All ten chapter skeletons.
- `README.md` — Repository root documentation.
- `CHANGELOG.md` — This file.

### Architecture Decisions Locked
- ADR-001: Lobster biology as system metaphor ✅
- ADR-002: Eight-agent colony structure ✅
- ADR-003: OpenRouter as model routing layer ✅
- ADR-004: Librarian as dedicated memory agent ✅
- ADR-005: Librarian icon change 🧠→📚 ✅
- ADR-006: Configuration portability ✅
- ADR-007: Four-category content routing ✅
- ADR-008: Two-repo strategy ✅
- ADR-009: Drone Factory — 🅿️ Parked
- ADR-010: UX Wrapper — 🅿️ Parked
- ADR-012: Vector store technology selection (Chroma) ✅

### Known Gaps (documented)
- Agent system prompts (8 files in `prompts/agents/`) — pending extraction from session transcripts
- `docs/02-scout-keywords.md` and `docs/03-influencer-registry.md` — pending Markdown extraction
- Influencer Tier 7 (Finance + AI voices) — Lane B research required
- Colony deployment — pending Phase 2 completion

---

## Upcoming

### [1.1.0] — Agent System Prompts
- Add all 8 agent system prompts to `prompts/agents/`
- Extract Scout keywords and influencer registry to Markdown
- First colony deployment test

### [1.2.0] — Living Guide Phase 1
- Populate Chapter 01 (What Is an AI Agent?)
- Populate Chapter 02 (The Lobster Explained)
- Populate Chapter 05 (AI in the Finance Profession)

---

*Maintained by the 📖 Editor Agent.*
