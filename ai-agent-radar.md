# AI Agent Radar

A running log of AI-agent-related repos and tools worth tracking, saved from things shared with me.

---

## 2026-09-06 — 5 fresh AI-agent repos

Source: shared post ("5 fresh AI-agent repos worth having on your radar"). Theme: tooling around agents is maturing — reusable coding-agent skills, time-aware knowledge systems, commerce agents, multi-agent workspaces, and isolated execution environments.

| Repo | Link | Category (from post) |
|---|---|---|
| `humanlayer/skills` | https://github.com/humanlayer/skills | Reusable coding-agent skills |
| `deeplethe/utopia` | https://github.com/deeplethe/utopia | Time-aware knowledge systems |
| `anthropics/commerce-agents` | https://github.com/anthropics/commerce-agents | Commerce agents |
| `stablyai/orca` | https://github.com/stablyai/orca | Multi-agent workspaces |
| `arcboxlabs/arcbox` | https://github.com/arcboxlabs/arcbox | Isolated execution environments |

### Verification — independent review (2026-09-06)

All five repos exist and match the post's categories on inspection. Notes below are from fetching each repo's GitHub page directly, not from the original post.

**`humanlayer/skills`** — Claude Code skills collection from HumanLayer (skill packs like `improve-claude-md`, `build-iterated-agentic-loop`, `show-me`). ~2.8k stars, 82 forks, MIT license, JS/TS, npm-installable. Multiple recent commits and open PRs/issues — looks actively maintained. [ESTABLISHED — repo content confirmed]

**`deeplethe/utopia`** — Bitemporal knowledge graph / "enterprise world model": document ingestion, semantic search, entity resolution, full temporal audit trail of how knowledge changes over time. ~4.8k stars, 442 forks, Apache-2.0, Rust core with TS/React frontend. Still v0.1 (schema can break between versions) but has 328+ commits, security policy, and contribution docs — early-stage but seriously maintained, not a toy. [ESTABLISHED — repo content confirmed; PLAUSIBLE that "time-aware knowledge systems" tag is accurate]

**`anthropics/commerce-agents`** — Official Anthropic reference blueprint for shopping and merchant agents (customer-facing shopping assistant + back-office merchant agent), with retail/travel/telecom/entertainment examples. Runs on the Messages API, Agent SDK, and Managed Agents. ~2.1k stars, 361 forks, Apache-2.0, Python + Node examples. Has CI, tests, docs, open PRs — this one I'd trust most by default since it's first-party Anthropic, not a third party's read of the product. [ESTABLISHED]

**`stablyai/orca`** — Orchestration tool / "ADE" (agent development environment) that runs a fleet of parallel coding agents (Claude Code, Codex, Grok, Cursor, Copilot, 20–30+ others), each in its own isolated git worktree so parallel edits never collide; desktop, mobile, and remote runtime, bring-your-own agent subscription, MIT license, TypeScript/pnpm. This is the outlier of the five: it's an order of magnitude more popular than the other four. A direct repo fetch read ~62.4k stars; a second cross-check (an ecosystem-tracking aggregator plus a blog post) put it at 6,063 stars in one place and "crossed 53,000 stars five months after first commit" in another. [UNCERTAIN] The sources disagree on the exact number, which suggests real, fast, viral growth (multiple independent sources put it in the tens of thousands) but I can't state a precise star count with confidence — check the repo page directly for the current figure before citing one.

**`arcboxlabs/arcbox`** — Container/VM runtime for macOS (Docker Desktop / OrbStack alternative), written from scratch in Rust with a custom hypervisor, VirtIO devices, and Docker CLI compatibility. Markets sub-100ms-boot disposable microVMs specifically as AI-agent sandboxes — matches the "isolated execution environments" tag well. ~3.1k stars, dual MIT/Apache-2.0 license, public beta but active (nearly 2k commits, open issues/PRs, roadmap). [ESTABLISHED]

**Overall confidence:** Moderate. Four of five check out cleanly against a direct repo fetch. One (`orca`) has a star-count figure that looks anomalous and should be treated as unverified until checked again. None of these were tested by installing or running the code — this is a metadata-level review (README, stars, commit/issue activity), not a functional or security audit.
