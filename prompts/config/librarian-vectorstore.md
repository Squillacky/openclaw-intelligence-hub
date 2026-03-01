# 📚 Librarian Agent — Vector Store Specification

> `prompts/config/librarian-vectorstore.md` | Version 1.0  
> **Purpose:** Defines the five vector store collections, universal metadata schema, retrieval patterns, write operations, and freshness policy for the Librarian Agent.  
> **ADR reference:** ADR-004 (Librarian as dedicated memory agent) | ADR-012 (vector database technology selection — PENDING)

> ⚠️ **Technology-agnostic.** This specification defines schemas and behavior, not implementation. The specific vector database is selected in ADR-012 (not yet decided). Current frontrunner: Chroma for simplicity, pgvector if PostgreSQL already deployed.

---

## Section 1 — Collections

Five collections. Each has a distinct purpose, retrieval pattern, and lifecycle.

### Collection 1: `scout_findings`

**Purpose:** All Scout-discovered content. Raw intelligence before narrative synthesis.

| Field | Value |
|---|---|
| Chunk strategy | One chunk per source item |
| Max tokens | 512 tokens, 50-token overlap |
| Primary retrieval | Hybrid: semantic similarity + metadata filters |
| Key filters | `date_found`, `signal_class`, `category` |
| Active window | 90 days |
| Archive | Indefinitely |
| Estimated volume | 500-2000 new vectors/week |

### Collection 2: `scribe_narratives`

**Purpose:** Daily briefing outputs produced by the Scribe Agent.

| Field | Value |
|---|---|
| Chunk strategy | One chunk per category section per briefing |
| Max tokens | 800 tokens |
| Primary retrieval | Date-range filter + category filter |
| Active window | 180 days |
| Archive | Indefinitely |
| Estimated volume | ~4 vectors/day (one per category) |

### Collection 3: `weatherman_predictions`

**Purpose:** All predictions and watch items — the Bellwether ledger in vector form.

| Field | Value |
|---|---|
| Chunk strategy | One chunk per prediction |
| Max tokens | 600 tokens fixed structure |
| Primary retrieval | Exact match on `prediction_id` + semantic for topic queries + filter on `status` |
| Lifecycle | Persistent — never deleted, only status-updated |
| Estimated volume | 50-200 vectors total |

### Collection 4: `semantic_knowledge`

**Purpose:** Long-term knowledge base. Vectorized blog posts, transcripts, research papers, influencer profiles, framework documents.

| Field | Value |
|---|---|
| Chunk strategy | Paragraph-level: 256-512 tokens, 64-token overlap |
| Primary retrieval | Semantic similarity primary, filter on `source_type`, `author`, `domain`, `freshness_status` |
| Lifecycle | Persistent with quarterly freshness updates |
| Estimated volume | 2,000-10,000 vectors at full load |

### Collection 5: `critic_verdicts`

**Purpose:** All Critic trust assessments. Source reputation tracking.

| Field | Value |
|---|---|
| Chunk strategy | One chunk per verdict |
| Max tokens | 400 tokens fixed structure |
| Primary retrieval | Exact match on `source_url` or `source_name` for trust lookups; semantic for claim verification |
| Lifecycle | Persistent — source reputation is cumulative |
| Estimated volume | 100-500 vectors |

---

## Section 2 — Universal Metadata Schema

Every chunk across all five collections carries these 18 fields. No exceptions.

| Field | Type | Description | Example |
|---|---|---|---|
| `chunk_id` | string | UUID — unique per chunk | `"ck_7f3a..."` |
| `collection` | enum | Which collection this lives in | `"scout_findings"` |
| `content` | string | The actual text content | `"LangChain released..."` |
| `created_at` | ISO datetime | When this chunk was created | `"2026-02-26T14:32:00Z"` |
| `source_type` | enum | Content origin type | `"blog_post"`, `"github_commit"`, `"podcast_transcript"` |
| `source_url` | string | Canonical URL of origin | `"https://..."` |
| `source_name` | string | Human-readable source name | `"Lilian Weng Blog"` |
| `author` | string | Primary author name | `"Lilian Weng"` |
| `content_date` | ISO date | When the content was published | `"2024-11-15"` |
| `category` | enum | Intelligence category | `"A"`, `"B"`, `"C"`, `"D"` |
| `domain` | enum | Subject domain | `"agentic_ai"`, `"corporate_finance"`, `"cost_accounting"` |
| `signal_class` | int | 1-5 signal quality class | `2` |
| `influencer_tier` | int or null | Tier 1-7 if from registry, null if not | `1` |
| `freshness_status` | enum | Current freshness state | `"CURRENT"`, `"FRESH"`, `"AGING"`, `"STALE"`, `"EVERGREEN"`, `"HISTORICAL"` |
| `freshness_verified_at` | ISO datetime | Last freshness check | `"2026-02-26T00:00:00Z"` |
| `critic_verified` | boolean | Has Critic Agent reviewed? | `true` |
| `critic_trust_score` | float or null | 0.0-1.0 trust score if verified | `0.85` |
| `version` | string | Schema version | `"1.0"` |

---

## Section 3 — Collection-Specific Additional Fields

Fields added on top of the universal schema for specific collections.

### `scout_findings` additional fields

| Field | Description |
|---|---|
| `scan_keyword` | Which keyword triggered discovery |
| `scan_session_id` | Which scan session found this |
| `influencer_match` | Boolean — did this come from a registry influencer? |
| `ocean_layer` | Surface Currents / Mid-Ocean / Deep Ocean / Reef |
| `bellwether_triggered` | Boolean — does this relate to an active Bellwether prediction? |

### `weatherman_predictions` additional fields

| Field | Description |
|---|---|
| `prediction_id` | BW-NNN — matches Bellwether ledger |
| `confidence_pct` | Numeric confidence 0-100 |
| `confidence_label` | CONFIDENT / MODERATE / POSSIBLE / SPECULATIVE |
| `horizon_date` | ISO date — when the prediction expires |
| `status` | PENDING / CONFIRMED / REFUTED / PARTIAL / EXPIRED / SUPERSEDED |
| `current_type` | Technical / Professional / Opportunity / Risk |
| `resolution_date` | ISO date — when prediction was resolved (null if PENDING) |
| `calibration_score` | Float — contribution to calibration score when resolved |

### `critic_verdicts` additional fields

| Field | Description |
|---|---|
| `verdict_id` | CV-NNN — sequential verdict identifier |
| `trust_score` | 0.0-1.0 numeric trust score |
| `trust_label` | Authoritative / Credible / Plausible / Questionable / Unreliable |
| `flags` | Array of flags: ["hype", "unverified_claim", "conflict_of_interest"] |
| `verdict_reasoning` | Text — why this trust score was assigned |
| `chunk_ids_reviewed` | Array of chunk_ids this verdict was based on |

### `semantic_knowledge` additional fields

| Field | Description |
|---|---|
| `document_title` | Full title of the source document |
| `chunk_index` | Position within the document (0-indexed) |
| `total_chunks` | Total chunks from this document |
| `vectorization_priority` | HIGH / STANDARD / ARCHIVE |
| `lobster_layer` | Which anatomy element this relates to |

---

## Section 4 — Retrieval Patterns

Nine named retrieval patterns. Each is used by specific agents for specific purposes.

| Pattern ID | Name | Used By | Query Method | Filters |
|---|---|---|---|---|
| RP-01 | `CONTEXT_LOOKUP` | All agents | Semantic similarity | None |
| RP-02 | `RECENT_SCOUT` | Scribe | Semantic + date | `created_at > 24h ago`, `collection = scout_findings` |
| RP-03 | `CATEGORY_FEED` | Scribe | Metadata filter | `category = [A/B/C/D]`, `freshness != STALE` |
| RP-04 | `PREDICTION_STATUS` | Weatherman | Exact match | `prediction_id = BW-NNN` |
| RP-05 | `SOURCE_TRUST` | Critic | Exact match | `source_url` or `source_name` in `critic_verdicts` |
| RP-06 | `INFLUENCER_HISTORY` | Scout, Critic | Exact + semantic | `author = [name]`, sorted by `content_date` desc |
| RP-07 | `SEMANTIC_DEEP` | Teacher, Editor | Semantic similarity | `collection = semantic_knowledge`, `vectorization_priority IN [HIGH, STANDARD]` |
| RP-08 | `BELLWETHER_EVIDENCE` | Weatherman | Semantic + filter | `bellwether_triggered = true` + `prediction_id` reference |
| RP-09 | `FRESHNESS_AUDIT` | Editor, Librarian | Metadata filter | `freshness_status IN [AGING, STALE]`, sorted by `freshness_verified_at` asc |

---

## Section 5 — Write Operations

Seven write operations. All writes go through the Librarian — no direct vector store access from other agents.

| Operation | Triggered By | Collection | Deduplication |
|---|---|---|---|
| `INGEST_SCOUT_FINDING` | Scout completes a record | `scout_findings` | Hash on `source_url` + `content_date` — reject if duplicate within 30 days |
| `INGEST_NARRATIVE` | Scribe completes a briefing section | `scribe_narratives` | Hash on `briefing_date` + `category` — reject if exact duplicate |
| `RECORD_PREDICTION` | Weatherman creates a new prediction | `weatherman_predictions` | Exact match on `prediction_id` — reject if ID already exists |
| `UPDATE_PREDICTION` | Weatherman resolves a prediction | `weatherman_predictions` | Update in-place by `prediction_id` — never creates duplicate |
| `RECORD_VERDICT` | Critic completes a trust verdict | `critic_verdicts` | Upsert by `source_url` — update trust score, append to history |
| `VECTORIZE_DOCUMENT` | Librarian processes a document for `semantic_knowledge` | `semantic_knowledge` | Hash on `source_url` + `chunk_index` — skip if already vectorized |
| `FRESHNESS_UPDATE` | Editor triggers quarterly audit | All collections | Updates `freshness_status` and `freshness_verified_at` in-place |

---

## Section 6 — Freshness Policy

| Status | Icon | Definition | Retrieval Behavior |
|---|---|---|---|
| CURRENT | 🟢 | Verified within 7 days | Full retrieval — highest confidence |
| FRESH | 🟡 | Verified within 30 days | Full retrieval |
| AGING | 🟠 | 31-90 days | Retrieve with freshness warning attached |
| STALE | 🔴 | 91+ days | Blocked from high-confidence retrieval; available for historical queries |
| EVERGREEN | ⚪ | Not time-sensitive | No freshness checks — foundational content |
| HISTORICAL | 📅 | Intentionally past-tense | Retrieval allowed with explicit historical context flag |

**Collection-specific TTLs:**

| Collection | Active Window | Archive |
|---|---|---|
| `scout_findings` | 90 days | Indefinite |
| `scribe_narratives` | 180 days | Indefinite |
| `weatherman_predictions` | Persistent | Never expires |
| `semantic_knowledge` | Persistent | Quarterly freshness check |
| `critic_verdicts` | Persistent | Never expires |

---

## Section 7 — Vectorization Priority List

Content to vectorize immediately when found.

### HIGH Priority — Immediate vectorization

| Content | Author/Source | Why |
|---|---|---|
| "LLM Powered Autonomous Agents" | Lilian Weng | Canonical agent architecture reference |
| "4 Agentic Design Patterns" | Andrew Ng | Foundational design patterns |
| Agent security research | Simon Willison | Critic Agent threat model foundation |
| All essays | Nate B. Jones | Best professional impact content |
| All agent architecture posts | Latent Space (Swyx) | Practitioner synthesis |
| All posts | LangChain Blog (Harrison Chase) | Orchestration framework developments |
| OpenClaw documentation | openclaw.github.io | Primary reference — all versions |
| Internal documents | Bellwether ledger, ADR document, this spec | Colony self-knowledge |

### STANDARD Priority — Vectorize within 24 hours of discovery

- Tier 1-4 influencer content (registry)
- Podcast transcripts from priority shows
- Stratechery posts
- Ben's Bites daily digests
- ArXiv papers on agent architecture

### ARCHIVE Priority — Vectorize for completeness

- Conference talks older than 6 months
- Pre-2024 historical content
- Low-tier forum discussions

---

## Section 8 — Technology Selection (Pending ADR-012)

**Decision pending.** Candidates evaluated below. Selection criteria: named collections with distinct schemas, rich metadata filtering, local/self-hosted option, Python client, persistence across restarts, free/low-cost tier, batch upsert support.

| Database | Pros | Cons | Recommendation |
|---|---|---|---|
| **Chroma** | Simplest VPS setup, free, native self-hosted, good metadata filtering, Python-native | Less mature filtering at scale | ⭐ Start here |
| **pgvector** | Best if already running PostgreSQL, excellent SQL-based filtering, battle-tested | Requires PostgreSQL operational overhead | Use if PostgreSQL already deployed |
| **Qdrant** | Strong filtering, good Ubuntu compatibility, Rust-based performance | More complex setup than Chroma | Upgrade path from Chroma |
| **Weaviate** | Production-scale, enterprise features | Complex setup, overkill for initial deployment | Phase 2+ consideration |
| **Pinecone** | Managed, excellent tooling | Cloud-only — violates VPS-first principle | Not recommended |

**Preliminary recommendation:** Start with Chroma, migrate to pgvector if filtering complexity demands it. Decision locked when ADR-012 is written.

---

## Registry Summary

| Element | Count |
|---|---|
| Collections | 5 |
| Universal metadata fields | 18 |
| Retrieval patterns | 9 |
| Write operations | 7 |
| Freshness status levels | 6 |
| High-priority vectorization items | 8+ |
| Technology decision | Pending ADR-012 |

*Version 1.0 — technology selection pending ADR-012. Schema is locked and technology-agnostic.*
