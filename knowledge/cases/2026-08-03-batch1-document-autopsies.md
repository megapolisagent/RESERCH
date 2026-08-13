# Case — Batch 1 document autopsies (OpenCode Swarm, hermes-multi-agent-workflow, Kimi-code, Anthropic Skills template)

Four projects read at full-document depth (State 3), with mechanism/why/trade-off recorded (State 4 partial) — predates the stricter `RESEARCH_WORKFLOW.md`-style discipline used in later batches; retroactively placed at State 3–4, incomplete by the fuller workflow's own rules.

## Project 1 — OpenCode Swarm (`docs/architecture.md`, full)

**Mechanisms**: single-owner planning discipline (one Architect owns all decisions); reality-check gate before planning (four-way status: NOT STARTED/PARTIALLY DONE/ALREADY COMPLETE/ASSUMPTION INCORRECT), built specifically because the team had been burned planning against a stale assumption; one task executes at a time, every task QA'd before the next starts.

**Why it works**: "multi-agent systems fail when they're unstructured" — the project's own stated motivation for centralizing planning authority in one role rather than distributing it.

**Trade-off**: trades parallelism for coherence — this is a deliberate, named choice, not an oversight.

## Project 2 — hermes-multi-agent-workflow (`AGENTS.md`, full)

**Mechanisms**: "fat engine, thin skill" — the orchestrator/engine stays domain-agnostic; all domain-specific behavior is pushed into one config file a Skill (or template) wraps.

**Why it works**: keeps the reusable engine reusable — domain logic leaking into the engine layer defeats the point of building a shared engine at all.

**Trade-off**: requires real authoring discipline to keep the boundary intact; the project names this as an explicit, actively-defended discipline, not a passive default.

## Project 3 — Kimi-code (`permission.md`, full)

**Mechanisms**: chain-of-responsibility microkernel permission architecture (policies self-register, first hit wins); the "harness constraint" vs. true-permission distinction — a mechanism that limits the agent for its own correctness (e.g. a plan-mode write guard) is a hard deny with no user-override channel, categorically different from a risk-policy ask/deny, which is always user-overridable.

**Race semantics of the veto event are documented precisely**: an immediate veto suppresses every pending `waitUntil` factory, so a deny can never be preceded by someone else's approval prompt. Very few documents anywhere in this research treat interaction ordering this exactly.

**Transferable to AI_OS:**
- The harness-constraint vs. true-permission distinction, now confirmed (not just inferred from a search snippet) to be architecturally enforced, not merely documented — this deepens what was already flagged in the Capability Map.
- Embedding "why not the obvious alternative" reasoning directly in living architecture docs rather than a separate RFC file that can be forgotten — worth citing specifically the next time this skill's own architecture decisions get written up.
- The two-path (data/code) contribution model as a way to bound complexity growth over time — a direct analog for how this skill's own findings should be thought about: strengthen an existing entry in `CAPABILITY_MAP.md`/`PRINCIPLES.md`/`METHODOLOGY.md` (cheap, "data path") before creating a new stage, principle, or file (expensive, "code path").

**Not transferable:** the specific TypeScript interfaces (`PermissionPolicyEntry`, `ToolAccesses.*` builders) are implementation, not principle.

---

## Project 4 — Anthropic Skills template (`template/SKILL.md`, full — trivially, the file is nearly empty)

**Mechanism**: the official template itself is minimal by design — frontmatter (`name`, `description`) plus a body, no imposed internal structure. **Why it works**: the standard's own progressive-disclosure design puts almost no constraint on body content, only on the metadata that governs discovery. **Trade-off**: a Skill's entire discoverability rests on the precision of one field (`description`).
