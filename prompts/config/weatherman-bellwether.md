# 🌊 Weatherman Agent — Bellwether Framework

> `prompts/config/weatherman-bellwether.md` | Version 1.0  
> **Purpose:** Forecasting specification, signal classification system, active prediction ledger, watch list, and calibration protocol.  
> **ADR reference:** ADR-006 — configuration, not agent logic.

> ⚠️ **The Weatherman is not a news summarizer (that is the Scribe). Not a trend reporter (that is the Scout). It is a forecaster.** It makes specific, falsifiable predictions with explicit confidence levels and time horizons. Predictions that cannot be proven right or wrong are not Weatherman predictions — they are opinions, and they belong elsewhere.

---

## Section 1 — Signal Classification

Not all signals are equal. Every signal is classified before making a prediction. Signal class determines the confidence ceiling — no prediction can have higher confidence than its weakest input signal.

| Class | Type | Description | Confidence Ceiling |
|---|---|---|---|
| Class 1 | Direct Evidence | Authoritative primary source (GitHub commits, official announcements, peer-reviewed research) | CONFIDENT: 70-85% |
| Class 2 | Corroborated Reporting | Multiple independent credible sources confirming the same claim | MODERATE: 50-70% |
| Class 3 | Community Signal | Practitioner consensus, forum discussions, survey data | POSSIBLE: 30-50% |
| Class 4 | Weak Signal | Single non-authoritative source, speculative commentary, pattern-matching | SPECULATIVE: 15-30% |
| Class 5 | Historical Pattern | Long-run trend data, industry cycle analysis, base rates | CONFIDENT for long-horizon forecasts |

**Enforcement:** When input signals are mixed class, the prediction is capped at the lowest-class input's ceiling. Upgrade confidence only when you upgrade the evidence.

---

## Section 2 — Confidence Labels

| Label | Range | When to Use |
|---|---|---|
| HIGH CONVICTION | 85%+ | Overwhelming evidence. Use sparingly — overconfidence erodes trust. |
| CONFIDENT | 70-85% | Strong Class 1 + Class 5 evidence combined |
| MODERATE | 50-70% | Class 2 corroborated reporting |
| POSSIBLE | 30-50% | Class 3 community signal |
| SPECULATIVE | 15-30% | Class 4 weak signal — record for future value |
| UNCERTAIN | <15% | On record but insufficient signal to forecast |

---

## Section 3 — Prediction Protocol

Every prediction uses the following schema. All fields required.

```
PREDICTION ID:       [BW-NNN] — sequential, never reused
PREDICTION:          [Exact, falsifiable statement]
TYPE:                [Technical | Professional | Opportunity | Risk]
CURRENT STATUS:      [PENDING ⏳ | CONFIRMED ✅ | REFUTED ❌ | PARTIAL 🔄 | EXPIRED ⏰ | SUPERSEDED 🔀]
CONFIDENCE:          [Label + percentage]
HORIZON DATE:        [Specific date — not "Q4 2026" alone, use Dec 31, 2026]
PRIMARY SIGNAL:      [Class N — description of triggering evidence]
CONFIRMATION CRITERIA: [Exact evidence that marks this CONFIRMED]
REFUTATION CRITERIA:   [Exact evidence that marks this REFUTED]
COLONY ROUTING:      [Which agents this affects]
```

---

## Section 4 — Active Predictions Ledger

### BW-001 — Steinberger Joins OpenAI [CONFIRMED ✅]

> **Not a prediction — a confirmed triggering event. Every BW-002 through BW-006 cascades from this.**

**Event:** Peter Steinberger, creator of OpenClaw, accepted a position at OpenAI.  
**Date confirmed:** February 14, 2026  
**Signal class:** Class 1 — direct announcement from Steinberger  
**Implication:** This is the most significant event in the OpenClaw ecosystem to date. The project's center of gravity has shifted. Every downstream prediction below was triggered by this single event.

---

### BW-002 — Steinberger Commentary Decline [PENDING ⏳]

**Prediction:** Steinberger's public OpenClaw commentary will decrease in frequency within 60 days of joining OpenAI.  
**Type:** Technical  
**Confidence:** MODERATE — 55%  
**Horizon:** April 15, 2026  
**Primary signal:** Class 3 — historical pattern of executives going quiet after major transitions + corporate communication norms  
**Confirmation criteria:** Post frequency drops >50% from pre-OpenAI baseline across Twitter/X + GitHub combined  
**Refutation criteria:** Post frequency remains within 25% of baseline, OR he explicitly states continued involvement  
**Colony routing:** Critic (recalibrate trust scores for OpenClaw source attribution), Editor (Ch 04 update)

---

### BW-003 — OpenAI Public Statement on OpenClaw [PENDING ⏳]

**Prediction:** OpenAI will make a public statement about OpenClaw's relationship to OpenAI products within 90 days.  
**Type:** Technical  
**Confidence:** MODERATE — 60%  
**Horizon:** May 14, 2026  
**Primary signal:** Class 2 — corroborated reporting on Steinberger hiring + historical OpenAI communication patterns around ecosystem acquisitions  
**Confirmation criteria:** Official OpenAI blog post, press release, or executive statement explicitly addressing OpenClaw  
**Refutation criteria:** 90 days pass with no statement (scores as REFUTED, not extended)  
**Colony routing:** All agents — this event triggers a full colony update cycle

---

### BW-004 — GitHub Contribution Velocity Change [PENDING ⏳]

**Prediction:** OpenClaw GitHub contribution velocity will change measurably within 120 days of Steinberger's OpenAI start.  
**Type:** Technical  
**Confidence:** POSSIBLE — 65% (direction uncertain: could increase or decrease)  
**Horizon:** June 14, 2026  
**Primary signal:** Class 3 — community signals about open-source project dynamics post-acquisition adjacent events  
**Confirmation criteria:** Commit frequency changes >30% from 30-day pre-announcement baseline (in either direction)  
**Refutation criteria:** Commit frequency remains within 15% of baseline through the 120-day window  
**Colony routing:** Scout (weekly GitHub monitoring), Librarian (version tracking)

---

### BW-005 — AI-Native FP&A Tooling from Major Vendors [PENDING ⏳]

**Prediction:** AI-native FP&A tooling (dedicated AI tools for financial planning and analysis) will be offered by at least 3 major enterprise vendors by Q4 2026.  
**Type:** Professional  
**Confidence:** MODERATE — 65%  
**Horizon:** December 31, 2026  
**Primary signal:** Class 2 — multiple vendor announcements already underway (Microsoft Copilot for Finance, Workday AI, SAP AI)  
**Confirmation criteria:** Three named enterprise vendors announce dedicated AI FP&A modules with specific feature sets (not just general AI features)  
**Refutation criteria:** Fewer than 3 vendors reach this threshold by Dec 31, 2026  
**Partial criteria:** 2 vendors meet threshold = PARTIAL (scored 0.5)  
**Colony routing:** Scribe (Category B + C), Teacher (Ch 05 update), Editor (Ch 05 freshness)

---

### BW-006 — "AI Analyst" Job Title in Fortune 1000 Finance [PENDING ⏳]

**Prediction:** The "AI analyst" job title (or functional equivalent) will appear in finance job postings at Fortune 1000 companies at materially higher frequency by Q3 2026 vs. Q1 2026.  
**Type:** Professional  
**Confidence:** POSSIBLE — 50%  
**Horizon:** September 30, 2026  
**Primary signal:** Class 3 — practitioner community signals + early job posting patterns  
**Confirmation criteria:** LinkedIn or Indeed data showing >100% increase in finance + AI analyst title postings at Fortune 1000 vs. Q1 2026 baseline  
**Refutation criteria:** <25% increase in same comparison  
**Colony routing:** Scout (job posting monitoring), Teacher (Ch 05 career impact section), Weatherman (Ch 10 update)

---

### BW-007 — Inference Cost Reduction via Model Routing [PENDING ⏳]

**Prediction:** OpenRouter or equivalent model routing services will reduce average enterprise AI inference costs by >30% by end of 2026 relative to direct API pricing.  
**Type:** Technical  
**Confidence:** MODERATE — 60%  
**Horizon:** December 31, 2026  
**Primary signal:** Class 2 — current OpenRouter pricing trends + model competition dynamics (DeepSeek, Llama, Mistral driving price pressure)  
**Confirmation criteria:** Published analysis from credible source showing >30% cost reduction achievable via routing vs. single-provider direct API  
**Refutation criteria:** No credible published evidence of this threshold being reached by Dec 31, 2026  
**Colony routing:** Token Miser (cost escalation ladder update), Editor (Ch 06 cost optimization)

---

### BW-008 — Major Vendor Acquisition of AI-Native FP&A Startup [PENDING ⏳]

**Prediction:** A major accounting software vendor (Workday, SAP, Oracle, or Microsoft) will acquire or partner with an AI-native FP&A startup by end of 2026.  
**Type:** Opportunity  
**Confidence:** MODERATE — 55%  
**Horizon:** December 31, 2026  
**Primary signal:** Class 2 — historical M&A patterns in enterprise software + current AI startup funding landscape  
**Confirmation criteria:** Announced acquisition or formal partnership between a named Big 4 vendor and an identifiable AI-native FP&A startup  
**Refutation criteria:** No such acquisition or partnership announced by Dec 31, 2026  
**Colony routing:** Scout (Category C), Scribe (Category C briefing), Weatherman (Ch 10)

---

## Section 5 — Resolution Criteria

| Status | Meaning | Scoring |
|---|---|---|
| CONFIRMED ✅ | Exact confirmation criteria met | 1.0 point |
| REFUTED ❌ | Exact refutation criteria met, OR time horizon expired | 0 points |
| PARTIAL 🔄 | Confirmation criteria partially met | 0.5 points |
| EXPIRED ⏰ | Time horizon passed with insufficient evidence to confirm or refute | 0 points |
| SUPERSEDED 🔀 | A more significant development made the original prediction irrelevant | Withdrawn |

> ⚠️ **No extensions.** Expired time horizons score as REFUTED or EXPIRED, never extended. Extension is a calibration evasion tactic.

---

## Section 6 — Bellwether Watch List

Items being monitored that have not yet crossed the threshold to become formal predictions.

| Watch Item | Current Signal | Class | Watching For | Prediction Threshold |
|---|---|---|---|---|
| OpenClaw Foundation Formation | Steinberger mentioned open-source foundation on Feb 14 | Class 2 | Formal legal entity announcement, governance structure | Formal nonprofit or foundation announcement with governance structure = BW-009 |
| AI in Audit Function | Big 4 AI audit pilot programs appearing | Class 3 | Regulatory guidance on AI in external audit | Formal PCAOB or AICPA guidance on AI audit use = new prediction |
| Finance Team Headcount Impact | Anecdotal reports of FP&A team size reductions post-AI | Class 3 | Verifiable headcount data from public companies | >5 S&P 500 companies report FP&A headcount reduction attributed to AI = new prediction |
| On-Premise LLM Adoption in Finance | Banks and regulated entities exploring private LLM deployment | Class 2 | Regulatory clarity on private AI in regulated finance | OCC or SEC guidance on private LLM use in regulated finance = new prediction |
| OpenRouter Pricing Floor | Model competition may force OpenRouter pricing below sustainable margins | Class 3 | OpenRouter pricing changes, competitor routing services | OpenRouter announces pricing restructuring = new prediction |
| Multi-Agent Coordination Standards | No industry standard exists for multi-agent communication | Class 3 | Early standards proposals from LangChain, Anthropic, OpenAI | Published interoperability standard from credible body = new prediction |

---

## Section 7 — Calibration Protocol

The Weatherman runs a calibration check quarterly. For each confidence band, compare stated confidence to actual confirmation rate.

**Target:** Overall calibration score of 55-70% confirmation rate across all resolved predictions.  
**A perfectly calibrated forecaster is right 65% of the time when they say "CONFIDENT" and 30% of the time when they say "POSSIBLE."**

| Confidence Band | Target Confirmation Rate | Calibration Action if Off |
|---|---|---|
| HIGH CONVICTION 85%+ | 80-90% | If <80%: raise evidence threshold |
| CONFIDENT 70-85% | 65-80% | If <65%: review signal class assignments |
| MODERATE 50-70% | 45-65% | If <45%: check for confirmation bias |
| POSSIBLE 30-50% | 25-45% | If <25%: review input signal quality |
| SPECULATIVE 15-30% | 10-25% | Low resolution expected — record only |

**Calibration output:** Quarterly scorecard showing predictions resolved in the quarter, accuracy by confidence band, calibration score, and adjustments to signal class criteria if needed.

---

## Section 8 — Anti-Patterns

Common Weatherman failure modes. The Editor monitors for these in colony output.

| Anti-Pattern | Description | Example | Fix |
|---|---|---|---|
| The Vague Hedge | Prediction so broad it cannot be falsified | "AI will continue to impact the finance profession" | Require specific measurable outcome with specific time horizon |
| Confidence Inflation | Assigning higher confidence than signal class ceiling allows | Class 3 signal assigned CONFIDENT (70%+) | Enforce signal class ceiling strictly. Find stronger evidence first. |
| Permanent Pending | Allowing predictions to remain PENDING past time horizon | Extending BW-003 window rather than scoring REFUTED | Expired = REFUTED or EXPIRED. Never extended. |
| Hindsight Reformulation | Changing confirmation criteria after events become clearer | Redefining "measurably" in BW-004 after the data arrives | Criteria are locked at prediction time |
| Correlation Forecasting | Predicting what has already happened | Predicting "AI will be adopted in finance" in 2026 | Predictions must be ahead of the current evidence curve |

---

## Registry Summary

| Metric | Current |
|---|---|
| Active predictions | 7 (BW-002 through BW-008) |
| Confirmed events | 1 (BW-001) |
| Watch list items | 6 |
| First bellwether event | BW-001 — Steinberger → OpenAI (Feb 14, 2026) |
| Calibration target | 55-70% overall |
| Next calibration check | May 2026 (Q1 close) |

*Version 1.0 — locked. Quarterly calibration review scheduled.*
