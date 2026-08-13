# Evidence log — Stage 0A, second object: real AI agent/system internal organization (batch 1, known systems)

Date: 2026-08-03. Object: how mature, known AI agent systems actually organize memory, planning, reasoning, permissions, review, learning, context, and skills — not world tradecraft practices (that was the first object, logged separately). Sources below are lettered A–L; letters are referenced from `CAPABILITY_MAP.md` and `EVIDENCE_INDEX.md`.

## A — AGENTS.md / CLAUDE.md standard
The AGENTS.md standard (agents.md, agentsmd, sno-ai/mda, indisoluble/AGENTS-spec) is a cross-tool, repo-wide static instructions file, distinct from a Skill, now adopted by 30+ tools under a shared, Linux-Foundation-adjacent governance model. CLAUDE.md sources examined include a real production file (`ThalesGroup/fred/CLAUDE.md`, quoted near-full across two commits) plus multiple guide articles on CLAUDE.md hierarchy practice (parent/child inheritance, length budgets, single-source-of-truth discipline). **Transferable to AI_OS?** The static/dynamic split this file represents (always-loaded repo-wide instructions vs. on-demand Skill bodies) is directly relevant to how this skill's own documents should be organized and loaded.

## B — Anthropic Claude Skills
The official `anthropics/skills` repository and `template/SKILL.md` (fetched in full) define the packaged-directory format: YAML frontmatter (`name`, `description`) plus a markdown body, optionally bundling reference files and scripts. Three-level progressive disclosure: name+description always loaded → full body loaded only on task match → linked files loaded only as needed. **Transferable to AI_OS?** Directly the template this project's own `skills/reverse-engineering/` follows.

## C — OpenHands memory/context architecture
Four SDK/architecture doc pages plus `memory.py` source examined. OpenHands draws its own static/dynamic distinction as "repo skill vs. knowledge skill" — the same underlying split as A and B, independently arrived at. Also documents context compaction/condensing to manage token budget across long sessions. **Transferable to AI_OS?** A third independent confirmation of the static/dynamic context split — this pattern is not vendor-specific, it recurs because the underlying constraint (a finite context window holding content of wildly different relevance-persistence) is identical everywhere.

## D — SWE-bench / SWE-agent
Harness reference, evaluation guide, and Docker migration documentation. A containerized, reproducible evaluation harness — layered base/environment/instance images, fixed prediction format, tunable cache levels (100–2000GB disk / 16GB+ RAM depending on level), a numeric resolution-rate metric. The project's own documented lesson: conda environments were "underspecified" and were replaced by Docker for reproducibility. **Transferable to AI_OS?** The general lesson that reproducibility requires eliminating ambient, underspecified environment state — directly relevant to why this skill's own Definition of Done requires a second analyst be able to reach the same conclusion.

## E — Memory architectures across multiple independent agent-memory projects
Cortex (README), Codemem (`docs/architecture.md`), jcode (`docs/MEMORY_ARCHITECTURE.md`), agent-memory/inosx (`docs/memory-system.md`), and the AWS sample-autonomous-cloud-coding-agents repo (`docs/design/MEMORY.md`) were each examined at varying depth (mostly Low-Medium confidence — README/single-doc snippets, not full source). Event sourcing (append-only log, deterministic projection, never edited in place) recurs across Cortex, ostk.ai, genesis-ssmp, and agent6 independently — the single strongest convergence found across this whole batch. Vector/semantic memory (embeddings + similarity search) appears in Codemem and jcode; graph-based memory (typed nodes/edges, contradiction/supersession edges) also in jcode and Codemem; multi-layer hybrid (ephemeral session + durable cross-session, explicitly separate tiers) in the AWS sample agent and agent-memory/inosx's five-layer stack.

## F — Memory-as-Governance (AWS sample agent)
A deterministic pre-action check against prior recorded failures, not just passive recall — the agent is blocked from repeating an action already known to fail, rather than merely being able to recall that it failed if it happens to look.

## G — Recency + explicit supersession (not deletion)
A recurring discipline across the memory-architecture sources: a stale fact is not deleted when superseded, it is marked superseded with a link to the newer fact — preserving the audit trail while still surfacing the current-truth view by default.

## H — OWASP ASI06, memory poisoning
Untrusted external content entering an agent's memory unfiltered is a named, catalogued risk class (OWASP's Agentic Security Initiative, ASI06) — relevant as a recurring anti-pattern for Capability 1 (Memory).

## I — Self-critique / reflection pattern catalogs
Six independent blog/pattern-catalog sources examined. A consistent family of patterns: Generator-Critic split (two distinct roles), single-agent self-reflection (one role, two passes), multi-perspective parallel critics with an explicit arbitration "Resolver" role, and a confidence-gated critic (only escalates when its own confidence in the critique is high enough). **Transferable to AI_OS?** Directly relevant to this skill's own Evidence Review / Double-Loop Review design.

## J — Combined stopping conditions for self-critique loops
Three independent sources converge on the same combination: an iteration cap, a cumulative token budget, and stagnation detection (identical critique output twice in a row is treated as a structural blind spot, not a hard problem worth another pass).

## K — Confidence calibration against real outcomes (Antigravity Lab)
A rolling log of (self-reported confidence, actual outcome) pairs with a learned correction factor — because raw self-reported model confidence is measurably uncalibrated by default and needs an external check against real outcomes to be trusted.

## L — Frozen/fixed critique rubric
Multiple sources converge on applying an identical rubric every critique pass, specifically to keep results comparable across iterations — free-form review measurably drifts because the model invents new criteria each pass.

## Summary
This batch is the second of Stage 0A's two objects (world tradecraft practices was the first, logged separately and folded directly into `PRINCIPLES.md`/`METHODOLOGY.md`). Synthesized into `CAPABILITY_MAP.md` as Capabilities 1 (Memory), 5 (Review), and contributes to 6 (Learning) and 10 (Evaluation). Reading depth for most sources here is Medium-to-Low (see `EVIDENCE_INDEX.md`) — citations should be read as "at least one signal of this pattern," not fully verified accounts of each project's actual practice.
