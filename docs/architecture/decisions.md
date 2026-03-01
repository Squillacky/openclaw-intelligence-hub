# Architecture Decision Records

> All architectural decisions are permanently on the record. A decision is never deleted — it is SUPERSEDED by a later ADR. This preserves the reasoning chain across the project's lifetime.

**Status key:** ✅ Accepted | 🔵 Proposed | 🅿️ Parked | ⬛ Superseded | 🚫 Deprecated

---

## Decision Index

| ADR | Title | Status | Domain |
|-----|-------|--------|--------|
| [ADR-001](#adr-001) | Lobster Biology as System Metaphor | ✅ | Architecture / Documentation |
| [ADR-002](#adr-002) | Eight-Agent Colony Structure | ✅ | Agent Architecture |
| [ADR-003](#adr-003) | OpenRouter as Model Routing Layer | ✅ | Infrastructure / Cost |
| [ADR-004](#adr-004) | Librarian as Dedicated Memory Agent | ✅ | Agent Architecture |
| [ADR-005](#adr-005) | Librarian Icon Change — 🧠 to 📚 | ✅ | Documentation / Standards |
| [ADR-006](#adr-006) | Configuration Portability | ✅ | Architecture / Portability |
| [ADR-007](#adr-007) | Four-Category Content Routing | ✅ | Agent Behavior / Output |
| [ADR-008](#adr-008) | Two-Repo Strategy | ✅ | Repository / Infrastructure |
| [ADR-009](#adr-009) | Drone Factory as Separate System | 🅿️ | Future Architecture |
| [ADR-010](#adr-010) | UX Wrapper for Configuration Portability | 🅿️ | Future / Product |
| [ADR-012](#adr-012) | Vector Store Technology Selection | ✅ | Infrastructure / Database |

---

## ADR-001

**Lobster Biology as System Metaphor** | ✅ Accepted | February 2026

### Context
- AI agent architectures lack intuitive mental models for non-engineers
- Standard computing metaphors don't capture emergent, adaptive agent behavior
- Documentation without a unifying metaphor fractures into inconsistent terminology

### Decision
The entire system uses lobster biology as its primary explanatory metaphor. Every architectural concept maps to a specific anatomical structure. `docs/01-lobster-anatomy.md` is the single authoritative reference. All other documents cite this one — they do not redefine terms independently.

### Rationale
- Lobster biology is genuinely isomorphic to agent architecture — distributed nervous system maps to distributed cognition, gastric mill maps to RAG, molt cycle maps to versioning
- A single metaphor forces consistency — when a writer reaches for a term, there is one correct term
- The metaphor is memorable and distinctive
- Biological systems encode genuine wisdom about resilience, adaptation, and failure modes

### Consequences
- **REQUIRES:** `docs/01-lobster-anatomy.md` maintained as authoritative reference
- **REQUIRES:** All 8 agent system prompts use anatomy vocabulary consistently
- **ENABLES:** Single explanation path for all audiences
- **PREVENTS:** Independent terminology drift across documents

### Alternatives Rejected
- *Factory/manufacturing metaphor* — doesn't encode adaptation or emergent behavior
- *Ecosystem/forest metaphor* — too passive; forests don't have orchestration loops
- *Military/unit metaphor* — implies conflict inconsistent with collaborative agent design

---

## ADR-002

**Eight-Agent Colony Structure** | ✅ Accepted | February 2026

### Context
- A single general-purpose agent creates an impossible design problem — the more capable at everything, the harder to reason about, test, and improve
- Different tasks have fundamentally different requirements — finding signals requires different models and tools than narrating findings
- Cost optimization requires routing different task types to appropriately-priced models

### Decision
The system uses exactly eight specialized agents, each with a single primary responsibility: Scout (sensing), Critic (verification), Scribe (narration), Librarian (memory), Weatherman (forecasting), Token Miser (cost governance), Teacher (accessibility), Editor (structure and maintenance).

### Rationale
- Single-responsibility principle applied to agents: one thing done well is testable independently
- Specialization enables model optimization — Token Miser routes simple tasks to Haiku, Scout routes complex synthesis to Sonnet
- Eight agents matches the cognitive load the system was designed to monitor

### Consequences
- **REQUIRES:** Each agent has a formally documented system prompt before deployment
- **REQUIRES:** Inter-agent communication protocol
- **ENABLES:** Independent model upgrades per agent
- **PREVENTS:** Adding a 9th agent without a formal ADR

### Alternatives Rejected
- *Single orchestrator agent* — becomes a god-object that is untestable at scale
- *Four agents* — insufficient specialization
- *Twelve agents* — diminishing returns beyond 8 for current scope

---

## ADR-003

**OpenRouter as Model Routing Layer** | ✅ Accepted | February 2026

### Context
- Different agent tasks have different model requirements
- Hardcoding a single API provider creates vendor lock-in and prevents cost optimization
- The AI model market evolves rapidly — new models ship monthly

### Decision
OpenRouter serves as the unified model routing layer. All agent LLM calls route through OpenRouter. The Token Miser governs the cost escalation ladder: tasks assigned to lowest-cost model capable of completing them to required quality.

### Rationale
- OpenRouter provides single API surface abstracting across Claude, GPT, Gemini, Mistral, DeepSeek, Llama, and others
- Model switching requires config change, not code change
- Avoids single-provider dependency risk

### Consequences
- **REQUIRES:** OpenRouter account and API key in environment config
- **REQUIRES:** Token Miser to maintain current model registry with cost tiers — quarterly review
- **ENABLES:** Any OpenRouter-supported model to serve any agent role without code changes
- **PREVENTS:** Hardcoding model names in agent prompts — model assignment lives in config

---

## ADR-004

**Librarian as Dedicated Memory Agent** | ✅ Accepted | February 2026

### Context
- LLMs have no persistent memory between sessions
- The colony generates significant content that, without organized storage, is lost
- Vector stores require ongoing maintenance — a dedicated function, not a side task
- Different agents need different memory access patterns

### Decision
Memory management is a dedicated agent responsibility assigned to the Librarian (📚). The Librarian manages the vector store, handles all embed/retrieve operations for other agents, maintains memory freshness, and enforces the three-tier memory architecture (working, episodic, semantic).

### Rationale
- Memory management is complex enough to warrant full agent status
- Centralizing memory prevents multiple agents writing with inconsistent chunking strategies
- The Librarian is the institutional memory of the colony

### Consequences
- **REQUIRES:** Defined vector store schema before any agent begins embedding content
- **REQUIRES:** All agents request memory retrieval through the Librarian — no direct vector store access
- **ENABLES:** Consistent memory hygiene across the entire colony
- **PREVENTS:** Multiple agents embedding the same content with different strategies

---

## ADR-005

**Librarian Icon Change — 🧠 to 📚** | ✅ Accepted | February 2026

### Context
- Librarian was originally assigned 🧠
- `docs/01-lobster-anatomy.md` uses 🧠 for the Brain/LLM concept
- Using 🧠 for both creates direct ambiguity in any document discussing both levels

### Decision
Librarian icon changes permanently from 🧠 to 📚. The anatomy document retains 🧠 as the exclusive icon for the Brain/LLM concept.

### Rationale
- The anatomy document is the authoritative reference — agent icons are subordinate
- 📚 is semantically appropriate for the Librarian
- The conflict was caught before deployment — fixing now costs a find-and-replace; fixing after costs a migration

### Consequences
- **REQUIRES:** Find-and-replace across all documents — 🧠 → 📚 wherever it refers to the Librarian
- **ENABLES:** Unambiguous icon usage across the entire system
- **PREVENTS:** Any future document using 🧠 to mean the Librarian

---

## ADR-006

**Configuration Portability — Framework vs. Domain Separation** | ✅ Accepted | February 2026

### Context
- The system was designed around one user's domain: AI agents, corporate finance, FP&A, OpenClaw ecosystem
- The underlying architecture is domain-agnostic — nothing in it depends on keywords, influencers, or categories
- Future users with different domains should run the same framework with a different configuration package

### Decision
The system enforces strict separation between framework logic and domain configuration at every level. Agent prompts contain behavior, personality, and inter-agent protocols. Agent prompts do NOT contain keywords, influencer names, categories, or any domain-specific content. All domain-specific content lives in configuration files that agents reference but do not embed.

### Rationale
- The value of the framework is multiplicative when portable — a personal tool serves one user, a portable framework serves any user
- Separation of concerns is foundational software engineering
- The Drone Factory (ADR-009) depends entirely on this separation

### Consequences
- **REQUIRES:** Formal configuration schema for each configurable element
- **REQUIRES:** Agent prompts reference configuration locations rather than contain configuration content
- **ENABLES:** Any user to deploy for any domain by replacing config files
- **ENABLES:** Drone Factory (ADR-009) to function as designed
- **PREVENTS:** Domain content embedded in agent prompts — this is a hard rule

---

## ADR-007

**Four-Category Content Routing Framework** | ✅ Accepted | February 2026

### Context
- The Scout collects content from many sources across many domains — without routing, all content enters the same queue
- The user operates in multiple distinct contexts: building AI projects, performing as FP&A Manager, making long-horizon decisions, staying current on technical AI
- Equal monitoring is correct. Equal routing is not.

### Decision
All Scout-collected content is routed into one of four categories before reaching the Scribe:

- **Category A — Opportunity Intelligence:** What can I build or monetize with AI?
- **Category B — Professional Leverage:** How do I become more valuable in my finance role using AI?
- **Category C — Strategic Intelligence:** Where is the AI economy going?
- **Category D — Technical Developments:** What is actually being built and what capabilities are arriving?

### Rationale
- Four categories match the four distinct contexts the user operates in
- The Scribe narrates differently for each category — one style for all four produces incoherent output
- The category framework is domain-agnostic (ADR-006) — a different user would have different category names but the same routing architecture

### Consequences
- **REQUIRES:** Scribe maintains four distinct narration templates
- **REQUIRES:** Priority weighting configuration — updatable as context shifts
- **REQUIRES:** Category definitions in Scribe config, not embedded in Scribe prompt
- **ENABLES:** Time-sensitive priority adjustment without architectural changes

---

## ADR-008

**Two-Repo Strategy — Design System vs. Runtime Separation** | ✅ Accepted | February 2026

### Context
- Two distinct projects exist: openclaw-intelligence-hub (design system) and clawroman-fortress (runtime on Hostinger VPS)
- Combining them creates confusion about what is documentation versus what is operational infrastructure
- Both need to evolve independently

### Decision
Two separate GitHub repositories with no code dependency between them. Cross-references use documentation links, not code imports.

- **openclaw-intelligence-hub:** Architecture, system prompts, lobster metaphor framework, living user guide, configuration schemas
- **clawroman-fortress:** VPS deployment configuration, deployed agent instances, operational runbooks

### Rationale
- Separation of concerns — design decisions and operational decisions are different kinds at different cadences
- Each repo tells a clean story independently
- Future portability (ADR-006) requires the design system decoupled from any specific runtime

### Consequences
- **REQUIRES:** Each repo has a README stating its role relative to the other
- **ENABLES:** Independent versioning and independent visibility decisions
- **PREVENTS:** Design system documentation co-mingled with VPS credentials or infrastructure-specific config

---

## ADR-009

**Drone Factory as Separate System** | 🅿️ Parked | February 2026

### Context
- The Intelligence Hub uses artisan-crafted specialized agents — not scalable to mass production
- A separate pattern is needed for producing many agents of similar type but different domain configuration
- Vehicle class taxonomy proposed: SUV (heavy information processing), HD Truck (bulk pipeline), Luxury Crossover (high-capability reasoning), Hybrid (multi-modal), Autonomous (self-directing)

### Decision
The Drone Factory is a separate system — distinct repo — built AFTER Phase 1 (Hub completion) and Phase 2 (Transfer Workflow) are fully tested. It depends entirely on ADR-006 being proven at the hub level first.

### 🅿️ PARKED — DO NOT IMPLEMENT UNTIL:
1. All 8 Intelligence Hub agents documented and tested
2. Transfer Workflow (Phase 2) functional and tested
3. A new ADR supersedes this one with explicit start decision

---

## ADR-010

**UX Wrapper for Configuration Portability** | 🅿️ Parked | February 2026

### Context
- ADR-006 enables portability but requires editing YAML/Markdown files directly — inaccessible to non-technical users
- For genuine universal adoption, configuration must be accessible without technical knowledge

### Decision
A UX wrapper for configuration generation is a Phase 3 build — after Hub complete, Transfer Workflow functional, and Drone Factory initiated. Generates configuration files conforming to schemas defined in ADR-006.

### 🅿️ PARKED — DO NOT IMPLEMENT UNTIL:
1. All configuration schemas stable and documented
2. Transfer Workflow built and tested
3. Drone Factory phase initiated and data package format stable

## ADR-012

**Vector Store Technology Selection** | ✅ Accepted | February 2026

### Context
- The Librarian Agent requires a vector database to persist the colony's memory (ADR-004).
- The vector store specification (`prompts/config/librarian-vectorstore.md`) defines 5 collections, 18 metadata fields, and 9 retrieval patterns.
- The schema is technology-agnostic, but deployment requires locking in a specific engine.
- Options evaluated included Chroma, pgvector, Qdrant, Weaviate, and Pinecone.
- The system prioritizes VPS-friendly deployment, low operational overhead for Phase 1, and strong metadata filtering.

### Decision
**Chroma** is selected as the initial vector database for the OpenClaw colony. **pgvector** is designated as the explicit upgrade path if and when filtering complexity or dataset size exceeds Chroma's comfortable limits.

### Rationale
- **Simplest VPS setup:** Chroma runs natively on Ubuntu 24.04 with minimal configuration compared to Qdrant or enterprise solutions.
- **Python-native:** Integrates seamlessly with the Python-based Intelligence Hub without requiring a separate network service architecture immediately.
- **Self-hosted & Free:** Adheres strictly to the VPS-first principle; avoids cloud lock-in (ruling out Pinecone).
- **Sufficient for Phase 1:** The estimated volume (under 15,000 vectors at full load across 5 collections) is well within Chroma's performance envelope.
- **Clear Upgrade Path:** The universal metadata schema is strictly defined. If Chroma's metadata filtering becomes a bottleneck at scale, migrating the well-structured data to pgvector (or Qdrant) is a straightforward ETL process, not a structural redesign.

### Consequences
- **REQUIRES:** Python/Chroma environment setup in `clawroman-fortress`.
- **REQUIRES:** Implementation of Librarian write operations using Chroma SDK.
- **ENABLES:** Immediate, low-friction deployment of the Librarian's memory architecture.
- **PREVENTS:** Premature optimization into heavy database administration before the ecosystem generates sufficient data volume to justify it.

---

## Future ADR Register

Ideas captured. Not yet decided. Each becomes a formal ADR when the decision is made.

| Future ID | Question | Decide When |
|-----------|----------|-------------|
| ADR-011 | Scribe category configuration — formal config doc for four-category routing | Before Scribe deployment |
| ADR-013 | Finance + AI Influencer Tier 7 — which voices enter the registry | After Lane B research |
| ADR-014 | CEO-level influencer additions (Lütke, Altman, Nadella, Huang) | Next influencer registry revision |
| ADR-015 | Drone Factory vehicle class taxonomy | When Drone Factory phase begins |
| ADR-016 | Transfer Workflow technology — how Chat-to-GitHub transfer works | Phase 2 completion |
| ADR-017 | Colony expansion — if/when to add a 9th agent | When genuine capability gap identified |
| ADR-018 | Configurator Agent — UX wrapper as colony member vs. traditional interface | Phase 3 UX design |
