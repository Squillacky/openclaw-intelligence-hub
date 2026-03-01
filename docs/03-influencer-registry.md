# 📡 Scout Agent — Influencer Registry

> `docs/03-influencer-registry.md` | Version 1.0  
> **Type:** Human Intelligence Network — companion to `docs/02-scout-keywords.md`  
> **Purpose:** Named individuals whose output carries disproportionate signal weight. When keyword scans surface content from a registered influencer, Scout elevates signal priority automatically.  
> **ADR reference:** ADR-006 — this file is configuration, not agent logic.

**Status flags:** ✅ Verified — active and monitored | ⚠️ Verify — handle believed correct, confirm before monitoring | ❓ Discover — handle unknown, active discovery required

---

> 🚨 **ACTIVE BELLWETHER WATCH — READ FIRST**  
> Peter Steinberger, creator of OpenClaw, joined OpenAI on **February 14, 2026**. This is the most significant event in the OpenClaw ecosystem to date. Implications are actively unfolding.  
> **Monitor:** His public output frequency | What he stops discussing | OpenAI's stance on OpenClaw | Community reaction | Fork activity  
> **Route to:** 🌊 Weatherman (Bellwether) + 😈 Critic (trust recalibration) + 📖 Editor (Ch 04 Daily Intelligence)

---

> ⚠️ **Known Gap — Tier 7:** Finance + AI professional voices are absent from this registry. The keyword config has heavy finance orientation; the influencer network does not match. Tier 7 is a deliberate placeholder. Populate when Lane B research is complete.

---

## Tier 1 — Core (Maximum Priority)

*The people closest to OpenClaw itself. Primary source of truth.*

### Peter Steinberger — MAXIMUM

> Creator of OpenClaw. Joined OpenAI February 14, 2026.

Built the thing. Knows it better than anyone. His perspective is the authoritative primary source on OpenClaw architecture, design decisions, and roadmap. Post-OpenAI transition is the most critical monitoring task in this registry.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Twitter/X | steipete | ⚠️ | All posts, replies, quote tweets |
| GitHub | steipete | ⚠️ | All repos, commits, issues, stars |
| Website | steipete.me | ✅ | Blog posts, about page updates |
| YouTube | (not found) | ❓ | Conference talks, interviews — discover |
| LinkedIn | (not found) | ❓ | Career updates — discover |

**Monitor:** Track what he STOPS talking about as much as what he starts.

### Matt Schlicht — HIGH

> Founder of Moltbook. Entrepreneur.

Built the adjacent viral platform. Moltbook had serious security issues (404 Media exposed database). His response to security disclosures reveals ecosystem leadership maturity.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Twitter/X | (not found) | ❓ | Moltbook updates, AI agent commentary |
| LinkedIn | (not found) | ❓ | Professional updates |
| Website | (not found) | ❓ | Discover |

### Shadow (Core Maintainer) — HIGH

> Anonymous core maintainer of OpenClaw. Identity: unknown.

Quoted saying: *"If you can't understand how to run a command line, this is far too dangerous of a project for you to use safely."* This is the single most important safety statement in the OpenClaw ecosystem. Track all public statements.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| GitHub | shadow (username unknown) | ❓ | All commits, issue responses, PR reviews |
| Discord | (not found) | ❓ | OpenClaw Discord — active discovery required |

**Note:** Identity discovery is active priority. This person's technical judgment is critical for Critic Agent calibration.

---

## Tier 2 — Security & Critical Voices (High Priority)

*People whose work directly informs the Critic Agent's threat model.*

### Simon Willison — HIGH

> Developer, writer. Creator of Datasette and LLM CLI tool.

Primary authority on LLM security, prompt injection, and AI agent risk. His blog is the most rigorous ongoing source on AI security in the practitioner community. Every post is relevant to the Critic Agent's threat model.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Blog | simonwillison.net | ✅ | Every post — especially LLM security |
| Twitter/X | simonw | ⚠️ | Security threads, tool releases |
| GitHub | simonw | ⚠️ | LLM CLI, Datasette, security tools |

**Priority content:** Prompt injection research, AI agent security, tool use vulnerabilities.

### Amy Chang + Vineeth Sai Narajala — HIGH

> Cisco security researchers.

Demonstrated real data exfiltration via OpenClaw skills. Their research is the most concrete evidence of OpenClaw-specific attack vectors. The Critic Agent's exoskeleton assessment depends on their findings.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Cisco Blog | blogs.cisco.com | ✅ | AI security research posts |
| Research papers | (discover) | ❓ | Academic publications on AI agent security |

---

## Tier 3 — Tech Journalists Covering OpenClaw

*Journalists who have produced verified, high-quality coverage.*

| Name | Publication | Beat | Status | Priority |
|---|---|---|---|---|
| Anna Heim | TechCrunch | AI agent ecosystem | ✅ | HIGH |
| Anthony Ha | TechCrunch | AI tools and products | ✅ | HIGH |
| Casey Newton | Platformer | Big tech + AI culture | ✅ | HIGH |
| Butts & Chin | CNBC | Enterprise AI | ⚠️ | MEDIUM |
| Emily Forlini | PCMag | Consumer AI products | ⚠️ | MEDIUM |
| 404 Media reporters | 404 Media | AI security incidents | ✅ | HIGH — broke the Moltbook database story |

**Monitoring rule:** Tier 3 journalists are tracked for OpenClaw-specific coverage only, not general beat coverage. Alert on new bylines mentioning OpenClaw, Moltbot, or Clawdbot.

---

## Tier 4 — Agentic AI Thought Leaders

*Technical authorities on agent architecture. Not OpenClaw-specific — broader field.*

### Harrison Chase — HIGH

> CEO of LangChain. Creator of the LangChain framework.

Primary authority on agent orchestration patterns. LangGraph is a direct architectural influence. Every post on agent design patterns is relevant.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Twitter/X | hwchase17 | ⚠️ | Agent architecture, LangChain releases |
| LinkedIn | (discover) | ❓ | Enterprise AI strategy |
| Blog | blog.langchain.dev | ✅ | Technical architecture posts |

### Swyx (Shawn Wang) — HIGH

> Co-host of Latent Space podcast. AI Engineer.

Best aggregator and synthesizer in the AI practitioner community. Latent Space podcast is the highest-value audio source in the registry. His essays define how practitioners think about AI engineering.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Twitter/X | swyx | ⚠️ | AI engineer discourse, weekly synthesis |
| Podcast | latent.space | ✅ | All episodes — especially agent architecture |
| GitHub | sw-yx | ⚠️ | AI engineering repos |

### Andrew Ng — HIGH

> Founder of DeepLearning.AI and Landing AI. Former Baidu Chief Scientist.

Most credible popularizer of AI concepts. His "4 Agentic Design Patterns" framework is the foundational reference for this system's architecture.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Twitter/X | AndrewYNg | ⚠️ | AI education, agentic AI developments |
| Newsletter | deeplearning.ai/the-batch | ✅ | Weekly — framework updates |
| LinkedIn | andrewng | ⚠️ | Business AI strategy posts |

### Lilian Weng — HIGH

> Head of Safety at OpenAI. Author of "LLM Powered Autonomous Agents."

Her blog post "LLM Powered Autonomous Agents" is the canonical agent architecture reference — the textbook this system was built against. Every new post is immediate high-priority vectorization.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Blog | lilianweng.github.io | ✅ | Every post — IMMEDIATE vectorization |
| Twitter/X | lilianweng | ⚠️ | Research updates, OpenAI safety |

**Note:** Now at OpenAI, same company as Steinberger. This creates a potential upstream architectural influence on OpenClaw's future direction.

### Nate B. Jones — HIGH

> Substack writer. AI strategy + business intersection.

Best writer on Category B and C content — professional leverage and strategic intelligence. His essays are the closest thing to an FP&A-adjacent AI voice currently in the registry.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Substack | natesnewsletter.substack.com | ✅ | Every post |
| Twitter/X | (discover) | ❓ | Commentary and threads |

### Nathan Labenz — MEDIUM

> Host of The Cognitive Revolution podcast.

Strong signal on AI capability timelines and enterprise AI strategy. Less technical depth than Swyx/Chase, more strategic/business framing.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Podcast | cognitiverevolution.ai | ⚠️ | Episodes on agent capabilities, enterprise AI |
| Twitter/X | nlabenz | ⚠️ | AI commentary |

---

## Tier 4b — Business Strategy Voices

*Frameworks for understanding AI's economic and business impact.*

| Name | Platform | Signal | Priority | Notes |
|---|---|---|---|---|
| Ben Thompson | Stratechery (stratechery.com) | ✅ | HIGH | Aggregation Theory frameworks essential for agent business model analysis |
| David Sacks | Twitter/X + All-In Podcast | ⚠️ | MEDIUM | Enterprise AI adoption, VC perspective |
| Marc Andreessen | Twitter/X + a16z | ⚠️ | MEDIUM | AI techno-optimism — useful as counterweight |
| Ben Gilbert + David Rosenthal | Acquired Podcast (acquired.fm) | ✅ | MEDIUM | Deep business history — AI company strategy context |
| Brad Gerstner | Twitter/X (Altimeter Capital) | ⚠️ | MEDIUM | AI investment thesis, capital allocation signal |

---

## Tier 5 — Ocean Voices

*Human impact, workforce transformation, AI safety. Category C and D content.*

### Ethan Mollick — MEDIUM

> Associate Professor, Wharton. Author of "Co-Intelligence."

Most rigorous researcher on AI + knowledge work. His experiments with AI-augmented professionals are direct evidence for Category B content. The closest proxy for finance professional impact content until Tier 7 is populated.

| Platform | Handle / URL | Status | Track |
|---|---|---|---|
| Substack | oneusefulthing.org | ⚠️ | Every post — especially knowledge worker impact |
| Twitter/X | emollick | ⚠️ | Real-time experiments and findings |
| Book | Co-Intelligence | ✅ | Vectorize key chapters |

### Additional Tier 5 Voices

| Name | Focus | Platform | Priority |
|---|---|---|---|
| Gary Marcus | AI skepticism, limits of LLMs | Twitter/X | MEDIUM — useful Critic calibration |
| Yoshua Bengio | AI safety, existential risk | Research papers | LOW — long-horizon signals only |

---

## Tier 6 — Auto-Discovery Sources

*Scanned for new influencer discovery, not direct content.*

| Source | URL | Status | Frequency | Discovery Target |
|---|---|---|---|---|
| OpenClaw GitHub contributors | github.com/[REPO]/contributors | ⚠️ | Weekly | Profile top 20. Promote active ones to Tier 4. |
| OpenClaw Discord | (discover) | ❓ | Daily if found | If it exists, becomes Tier 1 source immediately |
| r/LocalLLaMA | reddit.com/r/localllama | ✅ | Weekly | Agent architecture practitioners |
| r/MachineLearning | reddit.com/r/MachineLearning | ✅ | Weekly | Research-to-practitioner bridge |
| Hacker News | news.ycombinator.com | ✅ | Daily | Search "OpenClaw" and related terms |
| AI Twitter lists | (build from Tier 1-4 follows) | ❓ | Daily | New voices citing Tier 1-4 content |

**Promotion criteria — move a discovered voice to Tier 4 when they meet ANY THREE:**
- Cited or retweeted by any existing Tier 1-4 influencer
- Demonstrable GitHub contribution to OpenClaw or related project
- Original research, not just amplification
- 1000+ engaged followers in the AI practitioner community
- Published in credible venues (Substack, peer-reviewed, major publication)

---

## Tier 7 — Finance + AI Voices (PLACEHOLDER — Lane B)

> ⚠️ **This tier is intentionally empty.** The keyword config has heavy finance orientation. This registry has zero finance-specific voices. The mismatch must be corrected.

**The gap:** The system is designed to serve a finance professional navigating AI transformation. The influencer network currently tracks the OpenClaw ecosystem and the general AI agent field excellently. It does not yet track finance professionals, FP&A practitioners, or CFO-level AI strategy voices.

**Ethan Mollick (Tier 5) and Nate B. Jones (Tier 4) are the closest current proxies.** Neither is finance-specific. This is a coverage gap, not a coverage solution.

**Candidates to research for Tier 7:**

| Category | Examples to Research | Why |
|---|---|---|
| Finance + AI practitioners | Paul Barnhurst (FP&A Guy), Glenn Hopper (Deep Finance) | FP&A practitioners already building with AI |
| Finance AI researchers | Academic or industry researchers studying AI impact on finance | Evidence-based rather than opinion-based signal |
| Finance AI content creators | YouTube/LinkedIn creators teaching AI tools to finance professionals | Teacher Agent content pipeline — curriculum signal |
| CFO-level voices | Finance executives publicly discussing AI adoption | Executive adoption signal |

**Populate using:** Lane B research from professional network + LinkedIn search + FP&A community forums + finance AI newsletters (CFO Dive, Accounting Today, FT Alphaville AI coverage).

---

## Newsletter & Podcast Feed

| Name | Author/Host | URL | Status | Priority | Cadence |
|---|---|---|---|---|---|
| Stratechery | Ben Thompson | stratechery.com | ✅ | HIGH | Daily/weekly |
| One Useful Thing | Ethan Mollick | oneusefulthing.org | ⚠️ | MEDIUM | ~Weekly |
| Ben's Bites | Ben Tossell | bensbites.com | ⚠️ | MEDIUM | Daily — pulse check |
| The Batch | Andrew Ng | deeplearning.ai/the-batch | ✅ | MEDIUM | Weekly |
| Latent Space | Swyx + Alessio | latent.space | ✅ | HIGH | ~Biweekly |
| The Cognitive Revolution | Nathan Labenz | cognitiverevolution.ai | ⚠️ | MEDIUM | ~Weekly |
| Acquired | Gilbert + Rosenthal | acquired.fm | ✅ | MEDIUM | Biweekly |
| All-In Podcast | Sacks, Friedberg, et al | allinpodcast.co | ⚠️ | MEDIUM | Weekly |
| ThursdAI | Alex Volkov | (discover) | ❓ | MEDIUM | Weekly |

---

## Action Backlog

| Priority | Action | Status |
|---|---|---|
| 🔴 HIGH | Verify all Twitter/X handles marked ⚠️ (Steinberger, Chase, Swyx, Ng, Weng, Newton, Mollick, Thompson) | TODO |
| 🔴 HIGH | Discover Shadow's GitHub identity | TODO |
| 🔴 HIGH | Find Matt Schlicht's platforms | TODO |
| 🔴 HIGH | Monitor Steinberger post-OpenAI activity weekly | ACTIVE |
| 🟡 MEDIUM | Begin Tier 7 research — Finance + AI voices (Lane B) | TODO |
| 🟡 MEDIUM | Vectorize: Lilian Weng, Stratechery, Simon Willison priority posts | TODO |
| 🟡 MEDIUM | Set up Google Alerts: primary keywords × Tier 1 influencer names | TODO |
| 🟡 MEDIUM | Discover OpenClaw Discord — confirm it exists, get access | TODO |
| 🟢 STEADY | Weekly GitHub contributor scan for new Tier 4 candidates | ONGOING |

---

## Registry Summary

| Tier | Focus | Count | Priority |
|---|---|---|---|
| Tier 1 | Core OpenClaw ecosystem | 3 profiles | Maximum |
| Tier 2 | Security & critical voices | 2 profiles | High |
| Tier 3 | Tech journalists | 6 names | High — OpenClaw coverage only |
| Tier 4 | Agentic AI thought leaders | 5 profiles | High |
| Tier 4b | Business strategy | 5 names | Medium |
| Tier 5 | Ocean voices | 3 profiles | Medium |
| Tier 6 | Auto-discovery sources | 6 sources | Discovery only |
| Tier 7 | Finance + AI voices | **0 — GAP** | HIGH to populate |

*Version 1.0 — Tier 7 gap documented. Lane B research required.*
