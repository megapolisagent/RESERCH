# My Agents — Registry

Not market research. A map of the owner's own agents and what is already known about each — built as a byproduct whenever one of them is investigated as an Intelligence Report target, and consulted whenever a new external finding needs to be checked for fit against the existing portfolio.

Distinct from `CAPABILITY_MAP.md`: that file is generic evidence about how AI agent systems work in general, gathered from third parties. This file is specifically the owner's own agents and their already-known mechanisms — the thing a new finding gets matched against.

Per agent:

- **Domain** — what it's responsible for.
- **Known mechanisms** — what this agent already does, in enough detail to judge whether a new finding strengthens, duplicates, or is irrelevant to it.
- **Investigated** — when it was last the subject of an Intelligence Report (or when its mechanisms were otherwise confirmed).
- **Source** — which report/artifact the mechanisms were drawn from.

Matching a new finding against this registry is a separate act from producing an Intelligence Report: the input is a finding (an article, a mechanism, a tool), not a target; the output is a short relevance read per agent, with a reason — not a ten-section report, and not a recommendation to act.

---

## Chief Design Officer

**Domain**: product design judgment — an independent reviewer role, explicitly not a UI/implementation function ("Not a UI designer... Judge; don't implement").

**Known mechanisms**:
- Context Sufficiency Gate — a precondition before judgment starts: infer what the project already answers, ask only if the answer would change the verdict.
- Thinking Model — Observe → Interpret → Challenge → Judge, applied every time, in that order.
- Sources of Truth hierarchy — product's own internal logic (for character/tone) → Operating System → Knowledge → independent research (decision research vs. professional research, kept distinct).
- Doctrine Change Policy — three escalation levels (typo-fix / README-level / philosophy-level) tied to blast radius, each requiring Proposal → (Discussion) → LOCKED → Apply.
- Voice register — verdict first, three to four sentences, no narration of the underlying framework in output.

**Investigated**: yes — full Intelligence Report produced comparing these mechanisms against real design-review/creative-director AI systems (hive_studio, zdesign, designpowers, ds-architect, creative-director-skill, Amazon Bar Raiser, Claude's Constitution, ADR practice).

**Source**: that Intelligence Report (this project, current session).

---

## Obsidian Builder

**Domain**: collaborative design + one-time automated generation of an Obsidian vault from a user-approved architecture (entities, relations, templates, Properties, Dataview/Bases, Tasks, Calendar, dashboards, automations). Explicitly not an ongoing vault-maintenance agent — that is a distinct, currently unbuilt role.

**Known mechanisms**: none of its own yet — by its own stated rule ("не придумывай механизмы, если они уже существуют"), it is meant to assemble from `knowledge/MECHANISM_LIBRARY.md` rather than invent. That file is the live registry of what it has to build from (structure generation, typed frontmatter, query/dashboard, calendar sync, task automation, one decision-logic mechanism, write primitives) and the gaps nothing yet fills (general entity-relation schema, dashboard auto-generation, calendar/Tasks wired into init, build-time typed relations).

**Investigated**: 2026-08-05 — role received directly from the owner (not reverse-engineered from an external artifact); mechanism library built same day from a dedicated Obsidian-Builder investigation.

**Source**: this session's Obsidian-agent + Obsidian-Builder investigation; mechanism detail in `knowledge/MECHANISM_LIBRARY.md`.

---

## Engineering Agent

**Domain**: composes specialized AI agents from a Foundation + a Skills library + a task — the profession investigated is "AI Engineer who professionally assembles other AI agents, repeatedly, as a craft." Not yet built; this entry is the evidence base a future implementation should be checked against, not a description of an existing mechanism.

**Known mechanisms** (transferable findings from the profession-level investigation, not vendor-specific implementation detail — see the full report for what was explicitly excluded as non-transferable):
- Restraint as the default posture: earn agentic complexity, Skills, memory, MCP, and orchestration only when the task demonstrably needs them — not by default. The single most consistent finding across the whole investigation.
- The determinism-boundary judgment (what the LLM proposes vs. what code enforces) as core professional knowledge, to be re-drawn as models change, not fixed once.
- A three-primitive context toolbox (tool search / Skills / memory-compaction) chosen per problem, not by reaching for one by default.
- Lazy, on-demand capability loading as a default pattern at every layer (Skills progressive disclosure, MCP tool access, memory).
- Governing/stable memory kept separate from session/task memory — **confirms** the Foundation's own existing `MEMORY.md`/`DECISIONS.md`/`SOUL.md` vs. `workspace/` split rather than contradicting it.
- SKILL.md as an increasingly cross-vendor packaging standard — worth checking this project's own `skills/` folder against, given a real observed migration cost (OpenHands) when a bespoke mechanism diverges from where the field converges.
- **Explicitly not found**: a settled, named, industry-wide "Agent Composition" mechanism for "Foundation + Skills library + task → minimal specialized agent." The capability is real in practice; no vendor or independent source has named or standardized it. If the Engineering Agent's own design later invents a name for this, that name is original to this project, not adopted from observed practice.
- **Cross-reference, 2026-08-12**: `knowledge/CAPABILITY_MAP.md`'s "Refinement — Orchestrator↔Specialist Invocation Contract" section is the directly relevant evidence base once this agent's own design work reaches "how does the Engineering Agent hand a task to, and re-invoke, a specialist it composed" — the two real families found (call-and-return vs. baton-pass) and the unresolved fork (resume-with-history vs. fresh-re-ask) are exactly the choices that step would face. Not yet applied to a design decision here — this agent remains unbuilt.
- **Cross-reference, 2026-08-12 (second)**: `knowledge/CAPABILITY_MAP.md`'s "Refinement to Capability 4 (Permissions) — Capability Layering" section is directly relevant to this agent's eventual Skill/MCP catalog design — the real, checked distinction between "connected in the current session" (a live fact, e.g. Claude Code's `claude mcp list`), "owned by the project" (`.mcp.json` scope vs. `~/.claude.json`), "technically permitted" (`settings.json` allow/ask/deny, a separate surface from ownership in every system checked), and "recommended for this task" (Skill/subagent `description`-matching, MCP tool annotations — both explicitly advisory, not enforced) is exactly the four-way confusion a real sibling agent (Engineer, `ENGINEER` repo) hit when its `tool-selection` Skill conflated "connected" with "owned." Not a design decision here (Responsibility Boundary Gate: Research only) — the open question of whether a future Skill System catalog should itself be a live-state mirror or a static ownership record is named as unresolved, not answered.

- **Cross-reference, 2026-08-12 (third)**: `knowledge/evidence/2026-08-12-engineer-capability-map-audit.md` — direct audit of the ENGINEERING category (17 Skills) in the shared Skill System registry, requested by Engineer to check whether its own capability set can discharge its Locked role. Key facts: only 3 of the 17 are actually installed on Engineer (repository-design, decision-documentation, tool-selection); two candidates (architecture-review, capability-creation-methodology) reference files (`idea-calibration.md`, a Bootstrap Sequence) that don't exist anywhere in Foundation/ENGINEER — verified by direct search, zero hits — because both were authored for a different agent's own framework (AI_OS/Мария), not adapted. Real MERGE candidates found: dispatching-parallel-agents/executing-plans/subagent-driven-development (one execution-orchestration capability, three modes); skill-creator/writing-skills (one Skill-authoring-and-testing capability, two independently-converging implementations). Named missing capabilities not covered by any of the 17: independent post-build evaluation of an agent's own professional output (owner-suspected, confirmed — and confirmed not solved by current AI-agent industry practice either, via a direct fetch of Anthropic's own evals post); maintenance/drift revalidation after a model change; full Skills+MCP+Models discovery (Engineer's own capability-creation-methodology candidate only covers Skills); and a permissions/least-privilege audit discipline (already flagged by Engineer itself, not newly found here). Verdict on the Locked-role question: Engineer cannot yet fully discharge it with this set — three concrete, evidenced gaps (no installed Skill-authoring/testing, no installed execution-orchestration discipline, no installed build-quality discipline) each already surfaced once in real work logged in `ENGINEER/DECISIONS.md`, plus the missing capabilities above.

- **Cross-reference, 2026-08-13**: `knowledge/CAPABILITY_MAP.md`'s "Refinement — Kimi (Moonshot AI)" section is directly relevant to this agent's eventual per-subtask model-choice logic — a real, vendor-documented, non-hypothetical technical path to a non-Anthropic model (Moonshot's Anthropic-compatible endpoint, plus independent third-party MCP bridges to Moonshot's own REST API) now exists and is checked, which the prior Automatic Capability/Model Selection refinement's cross-vendor routing gap did not yet have a concrete single-vendor example of. Not a design decision here (Research only) — whether/when such a path should actually be used remains Engineer's/the owner's call, and the jurisdiction/data-policy question checked in the same batch (company is Chinese/Beijing-headquartered, independently confirmed; the specific infrastructure-routing claim is not) is exactly the kind of fact this future agent's model-choice policy would need to weigh, not something this project resolved on its behalf.

**Investigated**: 2026-08-11 — full Intelligence Report, three parallel Stage 1 channels (GitHub, Exa/Web, YouTube), 28-source consolidated shortlist, Stage 1.5 abstraction-level tagging pass, 6 claims independently re-verified at Stage 2.

**Source**: `research/AI-Engineering/` — `01-brief.md` (brief + process amendments), `02-evidence.md` (source-level evidence), `03-full-report.md` (full Intelligence Report), `04-profession-model.md` (owner-facing profession model, the version this entry's "Known mechanisms" above is drawn from). Open follow-up, not yet done: a second, narrower design pass scoping which part of the broad AI Engineering profession becomes this agent's own profession — see `01-brief.md`'s status note.

---

## Researcher (this project) / `skills/reverse-engineering`

**Domain**: this project's own investigation methodology — the five-stage pipeline, source hierarchy, Definition of Done, and Review Loop that every other entry in this file, and every Intelligence Report this project produces, is built with.

**Known mechanisms**: see `skills/reverse-engineering/references/PRINCIPLES.md`/`METHODOLOGY.md`/`REVIEW_LOOP.md` directly — not duplicated here.

**Investigated**: 2026-08-12 — this project's own methodology was the target of a self-audit, requested by Engineer via a registered `ENGINEER/OPEN_QUESTIONS.md` question, checked against an external reference set (real AI research-agent engineering practice + real human-intelligence tradecraft + OSINT/fact-checking + cross-organizational benchmarking), not against this project's own documents. Result, in short: the *principles* (P0–P6) hold up well against established, cited disciplines. The *five-stage pipeline shape* converges with both the classical Intelligence Cycle and 2025–2026 deep-research-agent surveys at the level of "gather → establish mechanism → judge," but this project's Verification stage (an explicit, graded source hierarchy) is confirmed only against human-intelligence/OSINT tradecraft — current AI-research-agent engineering practice, including Anthropic's own production system checked directly, was found to still lack this apparatus, using informal prompt heuristics instead. One real correction resulted: Definition of Done conditions 4/5 (identify what transfers / what doesn't) were self-tagged "original" and turned out to already exist as cross-organizational benchmarking methodology's "adapt, not adopt" principle (Xerox, 1979) — corrected inline in `METHODOLOGY.md` itself, not just noted here.

**Source**: `knowledge/CAPABILITY_MAP.md`, "External Validation" section; `knowledge/EVIDENCE_INDEX.md`, Batch SELF; correction inline in `skills/reverse-engineering/references/METHODOLOGY.md`.

---

## [Next agent]

**Domain**:

**Known mechanisms**:

**Investigated**:

**Source**:
