# Evidence log — Stage 0A, second object: obscure repos and experimental agent systems

Date: 2026-08-03. Per explicit instruction not to limit this object to famous projects — deliberately obscure/small/experimental repos, evidence-only, letters M–Z continuing from the known-systems batch.

## M — Event sourcing (additional instances)
ostk.ai and genesis-ssmp READMEs (the latter's full `architecture.md` fetch failed, README-depth only) both describe an append-only event log as the memory substrate — independent instances adding to pattern E's convergence count.

## N — LLM proposes structured intent, deterministic code owns control flow
The single clearest, most repeated rule found in this entire research line — stated in near-identical language across four independent, otherwise-unrelated small projects: ai-runtime-lab, agent6, and two unrelated projects both named "AgentFlow" (Yupoer's and AleSaiani's). ai-runtime-lab additionally documents a Workflow/Activity split modeled on the Temporal/Restate durable-execution pattern: orchestration must be 100% deterministic (no `time.now()`, no `random()`); only an Activity may touch the outside world, and each Activity is independently retried/cached. agent6's `STATE_MACHINES.md` implements the same boundary as an explicit finite-state machine: the LLM cannot pick the next state, only populate variables a downstream deterministic branch reads.

## O — Three-way failure taxonomy
ai-runtime-lab and agent6 both classify failures as Retry (transient) / Fail (permanent) / Escalate (human-in-the-loop) rather than treating all failures identically.

## P — Reality-check gate before planning
OpenCode Swarm's `docs/architecture.md` (fetched in full as part of the document-autopsy batch) documents a four-way status check (NOT STARTED / PARTIALLY DONE / ALREADY COMPLETE / ASSUMPTION INCORRECT) run before committing to any plan — the project's own stated motivation was having been burned planning against a stale assumption.

## Q — Evidence-linked capability status
deepelement-mind/openos's README documents a three-lens fix for "documentation vs. verified progress" drift: Target / IterationScope / Implemented, where the last lens specifically requires evidence links, not just a written claim. **Transferable to AI_OS?** Directly and strongly relevant: this skill's own methodology version status (`v0.x` vs `v1.0`) already requires exactly this discipline — a rule isn't "confirmed" because it's written down, only when a real case's outcome is the evidence link (see Evidence Review in `REVIEW_LOOP.md`). Independent corroboration of a design choice already made here, not a new rule.

## R — OpenSwarm (openswarm-os): emergent coordination
Logged as the outlier against convergent patterns found elsewhere — a deliberately looser, emergent-coordination bet rather than the structured, single-owner or DAG-planned approaches dominant elsewhere in this research.

## S — Strategy/execution role separation
agentic-ceo's `docs/DEEP_DIVE.md` (snippet-depth at the time of this entry; superseded by the full-document, source-verified pass in `knowledge/cases/2026-08-03-agentic-ceo-full-pass.md`) describes a Director agent that decides *what* to do, with a separate agent executing it.

## T — Wolf/Jackal directed/undirected research pattern
Also from agentic-ceo: a first "Wolf" pass with a fixed, directed research plan, followed by a second "Jackal" pass exploring undirected, opportunistic leads — plus a fixed phase-budget allocation (Stalk 15% / Test Bite 20% / Kill 50% / Feed 10%) that forces a transition into synthesis regardless of how tempting further collection remains. **Transferable to AI_OS?** Directly relevant to this skill's own Stage 1 (Collection) and to the Stage 0A stopping rule (P6) — this is a sharper, more concrete version of "stop once a source adds nothing new," applied per-source within a single case rather than per-discipline across Stage 0A.

## U — Katherine Cass retrospective; the "Sophie" token-burn case
A first-person retrospective blog post documenting `AGENT_CULTURE.md` — a written culture document (not a rules file) that measurably shaped agent judgment on situations no rule enumerated in advance. The same retrospective documents a real production failure: an episodic/handoff-memory agent repeatedly re-derived and re-reported the same finding because it had no "have I already acted on/reported this" check before acting — a token-burn loop, not merely an inefficiency.

## V, W — agentic-ceo's Critic/Observer/Evolver loop
An automated, continuous review loop: an Observer grades every run; an Evolver adjusts configuration automatically based on Observer + Critic output — review as a standing system, not only a periodic manual checkpoint. The project's own retrospective states the Critic role was "almost cut to save cost... without it the knowledge base becomes an echo chamber" — real-world-validated qualitative evidence for a dedicated adversarial role. (A specific quantitative figure attributed to this system — a "23% downgrade" rate — was later checked directly against the project's own `critic.py` source in the full-document pass and found not to exist in code; see `knowledge/cases/2026-08-03-agentic-ceo-full-pass.md`. The qualitative finding above is unaffected; the specific number is not evidence.)

## X — Sieve and AgentHub retrospectives
Two independent first-person postmortems (Martin Beauvais's Sieve blog post; a Hashnode AgentHub retrospective) both document an architecture-level mistake: a premature microservices/multi-repo split, chosen at planning time to save token cost, which cost more in coordination overhead than it saved — a planning-level failure, not an execution one.

## Y — Three different senses of "done"
Grinta-Coding-Agent's `docs/journey/README.md` documents an explicit three-way distinction the project learned to make the hard way: a passing test suite, spec compliance, and correct runtime state are three different claims, not one — declaring "done" from any single one of these without checking the others separately is a named, recurring failure mode.

## Z — Permission systems (five independent implementations)
Kimi-code (`permission.md`, fetched in full), agentscope (`_engine.py` source), agent-perms (README), intus-permission-rule-gate (README), and Claude Code's own documented permission system all converge on identical precedence rules: deny > ask > allow, first match wins regardless of specificity, and a bare tool-name deny removes the tool from the model's context entirely (versus a scoped deny that leaves the tool visible but blocks matching calls) — the single strongest triangulation found in this entire research session. Kimi-code additionally contributes a distinct conceptual finding: a "harness constraint" (a mechanism that limits the agent for its own correctness, with no user-override channel) is categorically different from a risk-policy ask/deny (always user-overridable). agent-perms layers semantic command classification (read/read-sensitive/write/admin × local/remote) on top of pattern matching, built specifically because glob-based rules are "fragile" — an admission from Claude Code's own documentation, cited by agent-perms itself. intus contributes compound-command anti-injection: an allow rule for one command does not extend to that command chained with another via `&&`.

**Transferable to AI_OS?** Very strong, direct corroboration of two choices already made in this skill: (a) the non-destructive revision discipline (superseding a rule in place, inline, rather than deleting it), and (b) Definition of Done condition 1 (mechanism found, not just description) and condition 6 (reproducibility) both exist specifically because "looks done" and "is done" are different claims. Logged as strong confirming evidence, not a new rule.

## File-based, human-legible knowledge directory design
Several of the small/experimental repos examined in this batch structure their own accumulated knowledge as plain, version-controllable markdown files organized by type (evidence, cases, decisions, methodology) rather than a database or opaque store. **Transferable to AI_OS?** This skill's own `knowledge/` directory (evidence/, cases/, plus `CAPABILITY_MAP.md`/`EVIDENCE_INDEX.md`) already follows exactly this file-based, human-legible design for exactly the same stated reasons — direct, independent corroboration of a design choice already made in this project, not a new rule.

## Summary
This batch, combined with the known-systems batch, produced the bulk of `CAPABILITY_MAP.md`'s content across Capabilities 1–10. Reading depth is predominantly Low (single README snippet) with several Medium-confidence exceptions (agent6, ai-runtime-lab, Claude Code docs) and two High-confidence full-document autopsies (Kimi-code's `permission.md`, OpenCode Swarm's `docs/architecture.md`) — see `EVIDENCE_INDEX.md` for the full per-project breakdown.
