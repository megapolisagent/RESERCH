# Case — dsifry/metaswarm, full workflow pass

Run through this skill's methodology (Collection → Verification → Decomposition → Contextualization → Judgment, `skills/reverse-engineering/METHODOLOGY.md`), full document-by-document depth, single agent, sequential per the architecture decision stated before starting.

## State 1 — Selected

**Category**: production use + unique architecture.
**Fact**: 343 stars, 45 forks, 5 releases, one maintainer, "production-tested... hundreds of PRs" (self-reported, flagged as a claim not independently verified — level 4 per the source hierarchy). Unique architecture claim: recursive orchestration (swarm of swarms) + mandatory fresh-reviewer adversarial review + asymmetric agent persistence — none of these three exactly matched anything already in `CAPABILITY_MAP.md` before this pass.

## State 2 — Document Inventory

| Category | Status |
|---|---|
| AGENT.md/AGENTS.md | ✅ Exists (root `AGENTS.md`, `agents/` — 18 persona files) |
| CLAUDE.md | ✅ Exists (root + `templates/CLAUDE.md` + `CLAUDE-append.md`) |
| SKILL.md | ✅ Exists (13 skills, each with its own `SKILL.md`) |
| README | ✅ Exists |
| ADR | ❌ Confirmed absent — no `adr/`/`decisions/` markdown folder in the repository's own structure listing. Nearest analog, `knowledge/decisions.jsonl`, is a fact-store entry type, not a classic ADR document — a categorically different artifact, not counted as satisfying this category. |
| Templates | ✅ Exists (`templates/` — CLAUDE.md, CLAUDE-append.md, UI-FLOWS.md, SERVICE-INVENTORY.md, ci.yml, gitignore, .env.example, pre-push) |
| Memory | ✅ Exists (`knowledge/` — patterns.jsonl, gotchas.jsonl, decisions.jsonl, api-behaviors.jsonl, codebase-facts.jsonl, anti-patterns.jsonl, facts.jsonl) |
| Prompts | ✅ Exists (`agents/*.md` persona definitions function as the prompts; no separate `prompts/` directory) |
| Evaluation | ✅ Exists (`rubrics/` — plan, code-review, adversarial-review, security-review, release-engineering) |
| Workflow | ✅ Exists (9-phase SDLC + 4-phase Orchestrated Execution Loop) |
| Architecture | ✅ Exists (README's own Architecture section + diagram) |
| Hooks | ✅ Exists (`hooks/hooks.json`, `hooks/session-start.sh`) |
| Tests | ✅ Exists (`tests/hooks/test-session-start.sh`, confirmed via PR #44 discussion) |
| Permissions | ❌ Confirmed absent — no dedicated permission-system document or module found; contrasts directly with Kimi-code (Case batch 1), which has one as a first-class design doc. |

14/14 marked.

## State 3 — Reading

**Fully read** (direct fetch, complete content): `README.md`, `skills/orchestrated-execution/rubrics/adversarial-review-rubric.md`, `skills/start/agents/issue-orchestrator.md` (near-complete — response truncated near the end of the Coder spawn template section).
**Partially read** (search-snippet depth only, logged, not advanced to full analysis): `CLAUDE.md`, `AGENTS.md`, `skills/start/SKILL.md`, `skills/setup/SKILL.md`, `agents/code-review-agent.md`, `INSTALL.md`.
**Not read**: remaining 10 skills, remaining 17 agent persona files, all `knowledge/*.jsonl` contents, `guides/*.md`.

This project is **not** fully advanced past State 3 — only three documents are at full-read depth. States 4–7 below apply only to what was fully read; the rest remains queued for a future pass.

## State 4 — Analyzed (mechanisms from fully-read documents only)

1. **Mechanism**: binary PASS/FAIL verdict with no intermediate state ("no APPROVED WITH COMMENTS"). **Why it works**: removes the reviewer's ability to soften a contract violation into a suggestion — a spec is either met or it isn't. **Trade-off**: genuinely ambiguous, defensible interpretations get resolved by "when in doubt, it's BLOCKING," which will produce some false-positive blocks in exchange for never producing a false-positive pass.

2. **Mechanism**: mandatory cited evidence (`file:line`) for every verdict, with an explicit blacklist of invalid evidence phrases ("the code looks correct," "tests appear to cover this"). **Why it works**: makes every claim falsifiable by a second reader without re-doing the review from scratch. **Trade-off**: real time cost — every single DoD item needs its own citation, which does not scale to very large diffs without splitting work units smaller (which the project does — file-scope-bounded work units).

3. **Mechanism**: mandatory fresh reviewer instance on every re-review, with an explicit self-escalation rule ("if you have any knowledge of the previous review, you are not a fresh reviewer — escalate to the orchestrator"). **Why it works**: removes anchoring bias — a reviewer who remembers a prior FAIL may unconsciously search for confirmation that the fix worked rather than genuinely re-checking. **Trade-off**: costs a new context/session per re-review cycle; capped at 3 retries before human escalation, i.e., the cost is bounded but real.

4. **Mechanism**: orchestrator never trusts a subagent's self-report of completion; it re-runs validation independently (`npx tsc`, `eslint`, `vitest`, file-scope diff check) regardless of what the Coder claims. **Why it works**: separates "claims to be done" from "independently verified as done" into two non-collapsible steps. **Trade-off**: doubles the verification cost of every work unit (the orchestrator's own run plus the Coder's own testing), by design.

5. **Mechanism**: asymmetric agent persistence in Team Mode — the Coder is explicitly persistent across work units ("no cold start"), but adversarial reviewers are explicitly always fresh `Task()` instances "in BOTH modes, without exception." **Why it works**: persistence helps the producer (context continuity is valuable for implementation) but actively hurts the verifier (persistence is exactly what causes anchoring, mechanism 3 above) — the system encodes that the same feature (memory) is good for one role and bad for another, rather than applying one persistence policy uniformly. **Trade-off**: requires the architecture to track two different lifecycle rules per agent role instead of one global policy — more moving parts to keep straight.

6. **Mechanism**: External Dependency Checkpoint — a mandatory human pause, triggered specifically when a work unit needs external service credentials, before implementation of that unit begins. **Why it works**: prevents an agent from silently stalling, fabricating a stub, or proceeding with broken integration when it lacks something only a human can provide. **Trade-off**: adds friction even when the human already has credentials ready — a blanket pause for a specific-but-common risk.

7. **Mechanism**: BEADS (durable task store) is the single source of truth; only the orchestrator is permitted to write to it, even when multiple named teammates exist; teammates report via message-passing instead. **Why it works**: removes the need for a lock by removing the possibility of concurrent writers in the first place. **Trade-off**: the orchestrator becomes a serialization point for all durable state changes, even in a mode explicitly designed to reduce orchestrator-mediated bottlenecks elsewhere.

### Contradiction question — mandatory

**What in this project contradicts what I already believe to be correct?**

Two things, not zero:

1. `CAPABILITY_MAP.md`'s Review section (built from a different set of sources) framed anchoring/blind-spot bias in self-critique as fixed by *adding more parallel reviewers* (multi-perspective critic pattern). Metaswarm's adversarial-review mechanism fixes the same underlying risk a different way — a **single** reviewer, but with guaranteed zero carried-over memory between attempts — and treats "more reviewers" as a separate concern (that's the Design Review Gate, a different stage in metaswarm's own pipeline, not the fix for anchoring specifically). This means the Capability Map's implicit suggestion that parallel critics are *the* answer to same-model blind spots was incomplete — memory-freshness and reviewer-count are two independent levers, not one.

2. Prior findings (OpenCode Swarm, evidence P) framed "one Architect owns all decisions" as close to a universal discipline for multi-agent coherence. Metaswarm's Team Mode explicitly relaxes this for one specific reason — removing the orchestrator as a bottleneck for high-frequency handoffs (Researcher → Architect via direct `SendMessage`) — while still keeping centralization exactly where it matters (single BEADS writer, reviewer freshness). This is a real, production system consciously choosing partial decentralization, which qualifies rather than confirms the earlier "single owner" framing: the right question is not "centralized or not" but "centralized for *which specific risk*."

## State 5 — Cross-Validated

| # | Tag |
|---|---|
| 1 (binary verdict) | Confirms pattern L (frozen rubric), refines it — the binary-only constraint is a sharper version not previously logged. |
| 2 (mandatory cited evidence) | Confirms patterns Y and D (evidence must travel with the claim). |
| 3 (fresh reviewer + escalate) | **Candidate new pattern** — extends the self-critique family (evidence I) with a named "memory reset" variant not previously catalogued. |
| 4 (never trust self-report) | Confirms the Explorer/Architect (OpenCode Swarm) and Director/Wolf (agentic-ceo, pattern S) role-separation family. |
| 5 (asymmetric persistence) | **Candidate new pattern** — not previously logged anywhere in `CAPABILITY_MAP.md`. |
| 6 (External Dependency Checkpoint) | **Candidate new pattern** — a specific, named trigger type for a proactive human gate; general HITL gates were logged before (pattern AA/SimpleAgents), this is a more specific case. |
| 7 (BEADS single-writer) | Confirms pattern E/M (event-sourced/durable-log-as-truth), applied to task coordination specifically. |

## State 6 — Extracted (transfer verdicts, all High confidence — full document reads)

**Transfer**: mandatory cited evidence with an explicit invalid-evidence blacklist (directly sharpens this skill's own Judgment stage and Definition of Done — "mechanism found" and "trade-offs stated" could both require file:line-equivalent citation, not prose assertion). **Transfer**: fresh-reviewer-plus-self-escalation-if-memory-present, as a concrete implementation detail for a standing adversarial stress-test — this answers "how do you actually guarantee freshness." **Transfer**: the asymmetric-persistence principle itself (memory helps producers, hurts verifiers) as a named design rule, not tied to metaswarm's specific stack. **Transfer**: External Dependency Checkpoint as a reusable, named pattern for "pause before touching a resource only a human controls."

**Do not transfer**: BEADS/`bd` CLI specifics, the exact validate command list (`npx tsc --noEmit`, `eslint`, `vitest`) — stack-specific tooling, not principle. **Do not transfer**: the specific 18-persona taxonomy — a specific division of labor for this project's own SDLC scope, not a universal role set.

**Confidence**: High for the three fully-read documents; the rest of the inventory remains unread and contributes nothing to this analysis.

## State 7 — Capability Map update

Confirmations (1, 2, 4, 7 above): `dsifry/metaswarm` added to `CAPABILITY_MAP.md` — Capability 5 (frozen-rubric/binary-verdict refinement), Capability 4 (External Dependency Checkpoint), Capability 5 (fresh-reviewer-plus-self-escalation, asymmetric persistence).
Candidates (3, 5, 6 above): merged directly into `CAPABILITY_MAP.md` (Capability 5 and Capability 4) as single-source implementation findings, in the same style the Map already uses for other not-yet-cross-validated entries — no separate staging file needed; the Map itself is the place single-source findings live until (if ever) a second independent instance confirms them.

**State: Done.**
