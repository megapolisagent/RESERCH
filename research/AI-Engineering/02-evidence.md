# Consolidated Shortlist — AI Engineer / Agent Builder investigation

Merges the three Stage 1 channel shortlists (GitHub, Exa/Web, YouTube — raw counts 10+12+8=30) into one deduplicated list, grouped by theme rather than by channel, as prep for Stage 2 (Verification). Per the research-economy rule ([[feedback_profession_model_and_research_economy]] / brief operating instructions), duplicate/converging citations are collapsed once, not re-argued.

**Dedup performed**: "12-Factor Agents" (GitHub repo + YouTube conference talk, same author Dex Horthy) → one entry. "Building Effective Agents" (Anthropic essay + Barry Zhang's AI Engineer Summit talk, explicitly noted by the YouTube agent as content-overlapping) → one entry, talk cited as corroboration not a separate source. Net: 27 distinct citable sources.

---

## A. Design restraint / when NOT to reach for an agent (Q1, Q2, Q3, Q12)

1. **Anthropic — "Building Effective Agents"** (essay + Barry Zhang's AI Engineer Summit 2025 talk as corroborating oral source) — T1. Augmented-LLM → workflows → agents only when needed; explicit warning against defaulting to agents/frameworks.
2. **`humanlayer/12-factor-agents`** (repo + Dex Horthy's AI Engineer Aug-2025 talk) — T1. "Own your control flow," "stateless reducer," "small focused agents" — argues against outsourcing control flow to a framework's agent loop. Per Horthy's ~100 founder interviews: highest-revenue production agents are conventional deterministic code with narrow LLM insertion points, not "prompt + bag of tools" loops.
3. **Simon Willison — agentic engineering patterns / "lethal trifecta"** (Pragmatic Summit talk, written companion used) — T2/T3 (independent practitioner, lowest priority tier, included only to fill a security/testing gap no product-author source covered). Prompt injection is not a fixable bug but the mechanism of instruction-following itself — sandboxing is the only real check; TDD reframed as mandatory since tests are now cheap to generate.
4. **Anthropic — "How we built our multi-agent research system"** — T1. Orchestrator-worker pattern; production hardening specifics (durable checkpoint/resume, rainbow deployments for stateful agents, lightweight references instead of full transcripts between agents); a named real failure mode (50 subagents spawned for simple queries before constrained).

## B. Skills — lifecycle, spec, authoring, recognition signal (Q7, Q8, Q9, Q13)

5. **`anthropics/skills` + Anthropic Skills docs/spec/best-practices cluster** — T1. Reference implementation; three-level progressive disclosure (metadata always-on → SKILL.md body on trigger → bundled files on demand); concrete validation rules (naming, length, no self-referential product names).
6. **`agentskills/agentskills`** — T1/T2 (docs-level, not raw spec read directly — flagged weaker). Vendor-neutral governance body for the same SKILL.md contract, decoupled from any one platform.
7. **Barry Zhang & Mahesh Murag — "Don't Build Agents, Build Skills Instead"** (AI Engineer conference talk, aggregated-transcript sources) — T1 (authors of the mechanism). MCP=connectivity vs. Skills=expertise split. Concrete recognition trigger for Q9: Claude regenerating the same procedural script from scratch every session is the observable signal a Skill is missing — the single most concrete answer to Q9 found across all three channels.
8. **`obra/superpowers`** — T1. Skills treated as tested code, not prose — changes require before/after eval results; a dedicated meta-skill (`writing-skills`) is the designated authoring tool, i.e. the answer to "Skill insufficient → what happens next" is "invoke the meta-skill," not hand-editing.
9. **OpenHands migration: `.openhands/microagents/` → `.agents/skills/`** — T1 (docs quoting own deprecation). A real production project abandoning a bespoke skill mechanism for the cross-vendor standard — direct evidence of migration cost when a local convention diverges from where the field converges.

## C. Memory architecture (Q1, Q6)

10. **Letta — context-engineering / agent-memory / memory-blocks cluster + `letta-ai/skills` agent-development skill** — T2 (vendor blog) / T1 (GitHub artifact). "LLM OS" framing: kernel context (system prompt, tools, memory blocks — mutated only via controlled tool calls) vs. user context (message buffer). Concrete antipatterns documented (too few / too many memory blocks).
11. **`letta-ai/letta` (MemGPT) three-tier memory** — T2/T3 (docs + secondary sources for exact tool names, weakest-verified item in the shortlist). Core (in-context, pinned) / archival (unbounded, searched) / recall (full history, searchable) — structured, agent-writable, queryable memory as a distinct paradigm from flat markdown files.
12. **Letta — "Rearchitecting Letta's Agent Loop"** — T2. Letta's own authors deprecating their MemGPT-style heartbeat/tool-reasoning architecture in favor of native model reasoning — a live instance of a framework's own creators reversing what was "best practice," because architectures need to stay in-distribution with how models are trained. **Contradiction/dating flag**, not a settled fact.
13. **Cline memory bank** — T2 (docs-page level, raw source 404'd — flagged for re-verification if this claim becomes load-bearing). Six typed markdown files (brief→context/patterns/tech→active/progress) read in full every task; designed around the assumption of zero persistent memory between sessions.

## D. Capability/tool loading at scale (Q5, Q6, Q7)

14. **`anthropics/skills` `shared/agent-design.md`** — T1 (primary artifact). Decision table: Tool search (cache-preserving dynamic tool-schema loading) vs. Skills (on-demand task instructions) vs. context editing/compaction/memory (files surviving restarts) — a rare source that names when each context-management primitive is correct, not just what it is.
15. **Anthropic — "Code execution with MCP"** — T1. Filesystem-navigable MCP servers (agent lists then reads only the specific tool file needed) cut token use 150,000 → 2,000 (98.7%) vs. loading all tool definitions upfront on a real case.
16. **MCP official architecture spec + "Introducing MCP"** — T1. Design principles: servers trivially easy to build, composable, isolated from each other and from full conversation history, capabilities negotiated progressively.
17. **Google — "Scaling AI Agent Infrastructure with MCP Stateless updates"** — T1/T2. Aug-2026 MCP spec change removing session/handshake state from the protocol core because statefulness broke horizontal scaling (sticky routing, no fault tolerance on pod restart) — a dated reversal of an earlier protocol assumption.

## E. Agent-composition primitives across vendors — direct evidence for Q13 (settled: no named cross-industry mechanism)

18. **Anthropic — "Building Agents with Skills" (Jan 2026)** — T1/T2. Names a 4-layer architecture (agent loop / agent runtime / MCP servers / skills library) — the closest conceptual match to "Foundation + Skills → specialized agent," but deliberately left unnamed ("the complete architecture," not a proper noun).
19. **OpenAI — Agents SDK + "A practical guide to building agents"** — T1. Composition primitives are named but structurally different: **Handoffs** (one-way ownership transfer) and **Agents-as-tools** (bounded delegated calls) compose *agents*, not a skills library into one agent.
20. **`wshobson/agents`** — T1 (file-level). 94 plugins, one Markdown source generating harness-native artifacts for 6 different platforms (Claude Code, Codex CLI, Cursor, OpenCode, Gemini CLI, Copilot) — strongest real composition/generation mechanics found, but the actual request→agent routing/selection algorithm is undocumented anywhere in the repo — an honest gap, not a guess.
21. **Claude Code — subagent `context: fork` vs. subagent `skills` field** — T1. Two distinct, easily-conflated composition primitives within one product: spawning a Skill into a subagent vs. force-injecting full skill content at subagent startup.

**Consolidated verdict on Q13** (established after two independent channels — Exa/Web and GitHub — converged on the same absence, per the research-economy rule this is now recorded and not being re-chased further): no settled, named, cross-industry mechanism exists for "Foundation + Skills library + task → minimal specialized agent." The underlying capability is real and multiple vendors implement some version of it; no vendor or independent source has named or standardized it as a single pattern.

## F. Repository / documentation structure (Q4, Q5, Q11)

22. **`github/spec-kit`** — T1. `.specify/memory/constitution.md` (versioned governing principles) separated from `.specify/templates/` (spec/plan/task with compliance checklists) and `.github/prompts/` (agent-facing prompts); unresolved items flagged inline as `[NEEDS CLARIFICATION]` rather than silently guessed.
23. **`block/goose`** — T1. Three-layer architecture (runtime / MCP extensions / recipes); `recipe.yaml` bundles instructions+tools+params as a portable unit; sub-recipes run in full isolation (no shared state, no nesting) as a deliberate contamination boundary; `AGENTS.md` (rules for building the system) kept distinct from recipes (what the system executes).
24. **ADR cluster** (`adr.github.io` + `microsoft/agent-framework/docs/decisions` + `vercel/ai` `adr-skill`) — T1. ADRs are the one documentation format shown to be load-bearing rather than decorative across independent projects; the Vercel artifact is notable as documentation practice itself packaged as a Skill.

## G. Production/process discipline from platform-team practitioners (Q2, Q10, Q11, Q12)

25. **Boris Cherny (Head of Claude Code) — prompt-deletion discipline** (YC Startup School talk) — T1. Deletes the entire system prompt on every new model release, rebuilds only for behaviors the model repeatedly stumbles on — direct counter-evidence to instruction-accumulation as a default.
26. **Boris Cherny — Co-Work architecture** (@Scale fireside chat) — T1. Platform-specific hardening (VM sandboxing, OS-level hooks, prompt-injection classifier) sits outside the core agent loop, not inside it; "output styles" as a first-class instruction-shaping mechanism distinct from system prompt or memory files.
27. **Cat Wu (Head of Product, Claude Code) — "ship demos, not docs"** — T1. Docs explicitly not treated as source of truth; ~10-minute build-to-live-feedback loop; engineers own idea-to-launch rather than handing off.
28. **Lance Martin (LangChain) — context engineering for agents** — T2 (practitioner at an infra vendor, written companion used). Cites Manus's finding of ~50 tool calls per typical agent task driving unavoidable context growth; recommends offloading large tool outputs to disk/state, returning compact references; frames context pruning as an ongoing operational responsibility, not a one-time design choice.

---

## Cross-cutting convergences already flagged by the channel agents (recorded once, not re-derived)

- **Governing/stable memory kept separate from session/task memory**: OpenHands `repo.md`, spec-kit `constitution.md`, Cline `projectbrief.md` all independently split this — matches the consuming project's own `MEMORY.md`/`DECISIONS.md`/`SOUL.md` vs. `workspace/` split.
- **Instruction/context accumulation actively resisted, not embraced, by three independent practitioner sources**: Cherny (deletes system prompt per release), Horthy (minimizes what's delegated to the LLM loop at all), Zhang/Murag (moves procedural knowledge out of the prompt into loadable Skills).
- **SKILL.md has become a cross-vendor standard in 2025–2026**, strong enough that an existing production project (OpenHands) migrated its own bespoke mechanism to it.

## Open questions carried into Stage 2 (not resolved at Stage 1)

- wshobson/agents' actual request→agent routing algorithm — undocumented anywhere found.
- OpenAI's (Handoffs/Agents-as-tools) vs. Anthropic's (Skills-in-context) composition philosophies — a genuine industry fork, not yet reconciled by any source.
- Letta's own reversal on agent-loop architecture — treat any "best practice" claim about agent-loop design as potentially dated, not load-bearing on its own.

## Discarded (noted once, not re-litigated)

Low-confidence/unverifiable-authorship vendor and hobby content (Taskade, V12Labs/CrewKit, Effective AI Labs, Diffco, Turion.ai, SkillTrace/CARG academic single-paper claims) — plausible but T3-T4, kept out of the shortlist unless independently corroborated during Stage 2.

---

## Stage 1.5 — Abstraction-level tags

**Correction**: the intro above says "27 distinct sources" — actual count after dedup is **28** (arithmetic slip, not re-derived, just corrected here per the research-economy rule: fix and move on).

Levels: **1** Platform/vendor practice · **2** Architectural mechanism · **3** Industry/format standard · **4** Universal engineering principle · **5** Professional/craft principle (the "when NOT to" category). Test applied throughout: does this survive the specific vendor/product disappearing tomorrow? Where a source's raw fact sits at level 1–3, the generalization is what actually carries into the profession model — the vendor fact stays behind as its supporting citation, not as a finding in its own right.

| # | Source | Level | Profession-level generalization (or standard/mechanism, if that's the ceiling) |
|---|---|---|---|
| 1 | Anthropic — Building Effective Agents | 5 | Earn agentic complexity only when the task genuinely needs open-ended flexibility; a workflow is simpler and more predictable and should be the default. |
| 2 | 12-Factor Agents | 4/5 | (4) Across ~100 founder interviews, the highest-revenue production agent systems keep the LLM's surface area narrow — deterministic code owns control flow. (5) "Own your control flow" as a standing design rule, not a framework default. |
| 3 | Simon Willison — lethal trifecta / TDD reframe | 4/5 | (4) Prompt injection is the mechanism of instruction-following itself, not a patchable bug — sandboxing, not prompt-level defense, is the only real boundary. (5) Since tests are now cheap to generate, treat TDD as a default discipline for agent-touching code, not an optional practice. |
| 4 | Anthropic — multi-agent research system | 4/5 | (4) Stateful, long-running agents need durable checkpoint/resume and gradual-rollout deployment, not atomic restarts — a general distributed-systems requirement, not an AI-specific one. (5) Constrain agent fan-out to actual task complexity; unconstrained spawning is a real, named failure mode. |
| 5 | anthropics/skills spec cluster | 3 | SKILL.md's progressive-disclosure contract (metadata always-on → body on trigger → files on demand) is the closest thing to a settled *format* standard found in this investigation. |
| 6 | agentskills/agentskills | 3 | Confirms #5's standard-ness — governance now sits outside any single vendor. |
| 7 | Zhang & Murag — "Don't Build Agents, Build Skills" | 4/5 | (4) Separate "how to connect" (MCP) from "how to do the task" (Skills) as a standing design axis, not a Claude-specific convention. (5) Recognize the need for a reusable capability by watching for repeated regeneration of the same procedural work — a concrete, observable trigger, not a vague heuristic. |
| 8 | obra/superpowers | 4/5 | Treat reusable agent instructions as tested artifacts requiring before/after eval evidence to change — not documentation that can be hand-edited on a hunch. |
| 9 | OpenHands microagents → Skills migration | 1→4 | (1) One project's migration. (4) A bespoke local convention carries real, paid-later migration cost once the field converges on an external standard — a generic build vs. buy/adopt lesson, not agent-specific. |
| 10 | Letta — context-engineering / memory-blocks cluster | 2/5 | (2) Kernel context (mutated only via controlled tool calls) vs. user context (free-flowing) as a structural split. (5) Start with the fewest memory blocks that work; both too-few and too-many are named, observed antipatterns — restraint applies to memory design too. |
| 11 | letta-ai/letta (MemGPT) three-tier memory | 2/4 | (4) Once memory needs to scale past what fits in context, it needs tiering and querying, not just a bigger flat file — a real alternative paradigm to markdown-file memory, weakest-verified item in the set. |
| 12 | Letta — agent-loop rearchitecture | 4 | Agent architecture should track the model's own training distribution; a mechanism that was correct for one model generation can become an anti-pattern for the next. This is a caution against treating *any* single architecture claim in this investigation (including this one) as permanent. |
| 13 | Cline memory bank | 2/4 | Once one memory file is doing multiple jobs (brief/context/patterns/tech/active/progress), splitting it into typed files by role is the generalizable move — doc-level source, flagged weaker. |
| 14 | Claude API — agent-design.md decision table | 4 | Tool search, Skills, and memory/compaction solve three different problems (cache-preserving tool access, on-demand task instructions, cross-restart persistence respectively) — choose per problem, not by reaching for one primitive by default. |
| 15 | Anthropic — code execution with MCP | 2/4 | Once a capability surface is large, expose it as navigable (list-then-read) rather than preloaded — a specific, measured instance (150k→2k tokens) of a general "lazy loading beats eager loading at scale" principle. |
| 16 | MCP architecture spec | 2/3 | MCP itself is becoming a protocol-level standard (composable, isolated, progressively-negotiated capabilities) — same standardization dynamic as SKILL.md, one layer lower in the stack. |
| 17 | Google — MCP stateless scaling change | 4 | Protocol-level statefulness is a horizontal-scaling liability (sticky routing, no fault tolerance on restart) — a classic distributed-systems/backend-engineering principle, independently rediscovered inside an AI-agent protocol, not an AI-specific insight at all. |
| 18 | Anthropic — 4-layer architecture (Jan 2026) | 2 | Names the shape (agent loop / runtime / MCP / skills library) but Anthropic itself declines to name it as a proper mechanism — stays at architectural-mechanism level, does not reach industry-standard. |
| 19 | OpenAI — Handoffs / Agents-as-tools | 2/4 | (4) "Delegate fully vs. retain control and call as a bounded tool" is a general composition-of-responsibility choice; OpenAI's naming of it is vendor-specific, the underlying choice is not. |
| 20 | wshobson/agents | 2/4 | Author once in a single source of truth, generate platform-native artifacts per target harness — this is build-system thinking (compile-once, target-many) applied to agent definitions, not a novel AI concept. |
| 21 | Claude Code — `context: fork` vs. `skills` field | 1 | Stays vendor-specific; no generalization extracted — kept as a concrete illustration of how easily two similar-looking composition primitives can be conflated. |
| 22 | github/spec-kit | 4/5 | (4) Separate governing principles, task templates, and agent-facing prompts into distinct artifacts rather than one blended document. (5) Flag genuine uncertainty inline (`[NEEDS CLARIFICATION]`) instead of silently guessing — a discipline, not a file format. |
| 23 | block/goose | 4 | Isolate sub-tasks from the parent's context/state as a deliberate contamination boundary; keep "rules for building the system" (AGENTS.md) separate from "what the system executes" (recipes) — both are general system-design separations, not goose-specific. |
| 24 | ADR cluster | 3/5 | (3) ADRs are the one documentation format shown load-bearing rather than decorative across independent, unrelated projects. (5) Document the *context and consequences* of a decision, not just the decision — this is what makes it useful later. |
| 25 | Cherny — prompt-deletion discipline | 1→4 | Instructions decay as the underlying model evolves; periodic, deliberate re-pruning beats indefinite accumulation. (This is the canonical example that prompted Stage 1.5 in the first place.) |
| 26 | Cherny — Co-Work architecture | 1→4 | Platform-specific hardening (sandboxing, injection defense) belongs outside the core reasoning loop, as a wrapping layer — not baked into it. |
| 27 | Cat Wu — "ship demos, not docs" | 1→5 | For a fast-moving agent product, a working prototype is a more reliable spec than written documentation; keep the build→feedback loop short and let engineers own idea-to-launch. |
| 28 | Lance Martin — context engineering | 2/4 | Don't return full payloads through the context window when a compact reference will do — offload bulk data to disk/state. A direct, independent rediscovery of pass-by-reference-over-pass-by-value inside agent design. |

**What this pass actually surfaced, unprompted by any new search** — direct, evidence-based support for the "Systems Engineer, not just AI Engineer" framing raised earlier: items 4, 17, 20, and 28 are, at their generalized level, classical distributed-systems / build-systems / software-engineering principles (durable checkpointing, protocol statelessness at scale, compile-once-target-many, pass-by-reference) that separate teams independently rediscovered while building AI agents. None of them are AI-specific at the level-4 generalization — the AI-specific part was only ever the vendor-level implementation (level 1–2). This is itself a finding worth carrying into the profession model, not just a methodological side-effect.

**Level-5 findings, gathered in one place** (the "design restraint" / "when NOT to" category, flagged as the strongest theme): earn agentic complexity only when needed (#1); own your control flow (#2); TDD as default once tests are cheap (#3); constrain agent fan-out to task complexity (#4); recognize a missing Skill by watching for repeated regeneration of the same work (#7); treat reusable instructions as tested artifacts (#8); start with the fewest memory blocks that work (#10); surface uncertainty inline instead of guessing (#22); document context and consequences, not just decisions (#24); let a working prototype be the spec (#27).
