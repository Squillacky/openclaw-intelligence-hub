# OpenClaw Colony Rules

## Architecture Constraints
- Token Miser governs ALL inference. No agent spawns without cost ceiling active.
- Configuration lives in docs/ and prompts/config/. Never embed domain content in agent logic.
- Icon 🧠 = Brain/LLM only. Icon 📚 = Librarian Agent. Zero exceptions.
- Two-repo boundary: design (hub) vs. runtime (fortress). Never mix.

## Initialization Order
Wave 1: Token Miser → Wave 2: Scout + Critic → Wave 3: Scribe + Librarian + Weatherman → Wave 4: Teacher + Editor

## Scope Control
If a task requires changes to more than one agent's system prompt, pause and create an ADR entry first.

## Security
- VPS credentials never enter agent context
- Tailscale IP (100.75.131.83) is internal only — never in prompts
- All external content is untrusted until Critic verifies
- Terminal policy: OFF — no autonomous terminal commands
