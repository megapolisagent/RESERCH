# Engineer capability-map audit — ENGINEERING category (Skill System), 17 Skills

Brief: 4th direct call from Engineer, 2026-08-12. Task: don't accept "17 Skills = Engineer's own capabilities"
as given — reassess the decomposition itself (MERGE/SPLIT candidates), build a real capability map, compare
each capability to external reference practice, verdict KEEP/STRENGTHEN/MERGE/REPLACE/REMOVE, name MISSING
capabilities (owner-suspected: independent post-build evaluation of an agent's own result), and answer
whether Engineer's Locked role is achievable with this set. Full report delivered inline to Engineer — this
file is the supporting evidence record per `MISSION.md` Knowledge Growth.

## FACT — the premise needed correction before anything else

`Skill System/registry.json` filtered by `category: "ENGINEERING"` returns 17 entries (verified by direct
`python -c "json.load(...)"` count, 2026-08-12): architecture-review, capability-creation-methodology,
claude-api, decision-documentation, dispatching-parallel-agents, executing-plans, mcp-builder,
repository-design, skill-creator, subagent-driven-development, systematic-debugging,
test-driven-development, tool-selection, verification-before-completion, webapp-testing, writing-plans,
writing-skills.

`ls "ENGINEER/skills/"` (direct, 2026-08-12) shows only 4 entries: `decision-documentation`, `installer`,
`repository-design`, `tool-selection`. Cross-checked against `ENGINEER/HOME.md`'s own "Мои скиллы" table
(3 rows, matching). **Only 3 of the 17 ENGINEERING-category Skills in the shared Skill System registry are
actually installed on Engineer.** The other 14 are catalog entries in the shared warehouse — available for
`installer` to pull in, never pulled. This matches Engineer's own Locked decision-log entry (2026-08-12,
"Приведение собственной сборки Engineer в порядок") which already states this explicitly for the
Skills-status column. The task's framing ("17 Skills — собственные профессиональные способности Engineer")
is therefore not literally accurate as a fact about the installed system; it is accurate as "the ENGINEERING
candidate pool Engineer could draw from." All capability-table verdicts below distinguish installed vs.
candidate-only status.

## Decomposition reassessment (Step 1 of the brief — before building the map)

Read every one of the 17 `SKILL.md` files in full (`Skill System/skills/<name>/SKILL.md`,
`ENGINEER/skills/tool-selection/SKILL.md` for the locally-modified copy).

### MERGE candidates found

1. **dispatching-parallel-agents + executing-plans + subagent-driven-development** — all three obra/superpowers
   origin, all three explicitly cross-reference each other as branches of one decision tree in their own text
   (`executing-plans`: "if subagents available, use subagent-driven-development instead"; `subagent-driven-
   development`'s own `dot` graph contrasts itself against `executing-plans` on "same session?"). One real
   capability — *delegated/multi-agent execution of implementation work* — with three selectable modes
   (independent-parallel / sequential-plan-cross-session / sequential-plan-same-session-with-review-loop), not
   three independent capabilities.
2. **skill-creator + writing-skills** — different origins (anthropics/skills vs. obra/superpowers)
   independently reinvent the same core idea: "RED-GREEN-REFACTOR applied to Skill authoring" (writing-skills'
   own explicit TDD-mapping table; skill-creator's baseline/with-skill eval runs are the same red/green
   check via a different tool chain). Convergent independent invention from two unrelated sources is itself
   corroborating evidence this is one real capability (*Skill authoring, testing & validation*) with two
   complementary halves (craft/bulletproofing vs. tooling/benchmarking), not two competing skills.

### SPLIT candidates found

1. **claude-api** bundles three separable things: (a) a live reference for current API/model/pricing usage,
   (b) a `migrate` subcommand — model-migration procedure, which is really a *maintenance/drift* capability,
   not a build-time reference; (c) Managed Agents onboarding — building a specific deployment shape. (b) is
   the one place in all 17 Skills that even partially touches ongoing maintenance after a model changes —
   worth carrying forward separately rather than leaving buried in a reference doc's subcommand table.
2. **subagent-driven-development**'s "Model Selection" section (cheap/standard/most-capable model per role,
   explicit-always, escalate-on-repeated-failure) is a reusable, generalizable decision a composing Engineer
   needs any time it assigns models to subagent roles — not only when executing one specific plan format.
   Worth extracting as its own referenced capability rather than leaving it embedded in one execution mode.

### Foreign-dependency finding (verified, not inferred)

`architecture-review` and `capability-creation-methodology` are both tagged `"source": "AI_OS (Мария)"` in
`registry.json` — i.e. authored for a *different* agent's own framework, not Foundation/Engineer's. Both
reference artifacts that do not exist in this project: `idea-calibration.md` (both skills route through it
for Steps 0/1/3-7) and a "Bootstrap Sequence" producing `PROJECT_DNA.md`, `CLAUDE.md`, `ROADMAP.md`,
`START.md`. Verified by direct search: `find "ENGINEER" -iname "*idea-calibration*"` and
`grep -ril "idea-calibration|PROJECT_DNA|Bootstrap Sequence" ENGINEER` both return **zero hits**. Foundation's
actual file model (per `repository-design/SKILL.md`'s own Implementation table, which Engineer already
uses) is `VISION.md`/`HOME.md`/`AGENTS.md`/`SOUL.md`/`PROFILE.md`/`MEMORY.md`/`ROUTING.md`/`DECISIONS.md`/
`OPEN_QUESTIONS.md`/`instructions/`/`workspace/`/`skills/` — none of which match. Installing either Skill
verbatim on Engineer would reference dead files. The underlying *ideas* in both (a closing checklist with a
reliability/AI-reasoning-boundary section; a disciplined domain-research phase sequence with a mandatory
Open-Source-Research step and a "take/reject + one-line why" extraction log) are sound and have no current
equivalent anywhere in Engineer's installed capabilities — hence REPLACE, not REMOVE, in the verdict table.

## Reassessed capability map (13 capabilities, replacing the 17-file view)

1. Repository/Agent Structure Design & Build-Readiness Audit — `repository-design` (installed, VERIFIED·LIVE).
2. Decision Documentation & Governance — `decision-documentation` (installed, VERIFIED·LIVE).
3. Tool/Capability Selection & Layering — `tool-selection` (installed, DRAFT).
4. Capability/Domain Discovery for a new agent build — `capability-creation-methodology` (candidate only,
   foreign dependency).
5. Architecture/Reliability/Reasoning-Boundary Gate — `architecture-review` (candidate only, foreign
   dependency).
6. Skill Authoring, Testing & Validation — `skill-creator` + `writing-skills` (MERGED; candidate only,
   neither installed).
7. Delegated/Multi-Agent Execution Orchestration — `dispatching-parallel-agents` + `executing-plans` +
   `subagent-driven-development` (MERGED; candidate only, none installed).
8. Model/Cost Tiering Decision — extracted (SPLIT) from `subagent-driven-development`; candidate only.
9. Build Quality Discipline (three complementary, not merged) — `test-driven-development`,
   `systematic-debugging`, `verification-before-completion` (candidate only, none installed).
10. Platform/API Currency Reference — `claude-api` minus the migration piece (candidate only).
11. Model-Migration / Platform-Drift Maintenance — `claude-api`'s `migrate` subcommand (SPLIT out of #10);
    candidate only, and only a partial answer to Missing capability M2 below (covers raw API code, not
    Skills/agent-loop architecture as a whole).
12. MCP Server Building — `mcp-builder` (candidate only).
13. Web Frontend Testing — `webapp-testing` (candidate only, professional-fit questioned — see verdict table).

## Point-fix, 2026-08-12 (same day, later) — `VISION.md` checked for the `webapp-testing` (capability 13) verdict

Requested by Engineer, closing the specific gap named in this audit's own Technical Execution Record answer:
the `webapp-testing` → **REMOVE** verdict ("не соответствует профессии Engineer") was reasoned from `HOME.md`'s
"Кто ты" section, never checked against `ENGINEER/VISION.md` — the one file whose stated job is "зачем этот
агент существует." Read in full now.

**Finding: `ENGINEER/VISION.md` is the generic Foundation-level file, not an Engineer-specific one, and it
does not speak to this question either way.** Its entire content is about why *Foundation* (the shared base
every agent is built on) exists, not why *Engineer the specialization* exists or what its professional scope
is: "Foundation — это дом, а не жилец... он не умеет писать код, не умеет искать источники, не умеет вести
соцсети — и не должен... Профессию приносит специализация, которую подключают поверх, уже после установки"
— quoted directly. Engineer's own specific profession/scope (composing Claude-Code-style agents vs. web
products) is deliberately not this file's job by Foundation's own stated design — it lives in `HOME.md`'s
"Кто ты" section instead, which is the file the original REMOVE verdict was actually reasoned from.

**Verdict: unchanged. `webapp-testing` stays REMOVE.** Not because `VISION.md` confirms the original reasoning
— it doesn't address agent-specific professional scope at all, by design — but because it also contains
nothing that contradicts it. The named gap (verdict reasoned without checking this specific file) is now
closed as a completed, neutral check, not as new support for the verdict: `VISION.md` was silent on the
question, and the original basis (`HOME.md`) stands un-revisited by this check.

## External reference set used

Reused, already-fresh (fetched directly earlier the same day, per this project's own P0/independence rules —
not re-derived from memory): `knowledge/CAPABILITY_MAP.md` Capabilities 2, 4, 5, 8, 9, 10, 11; "Refinement —
Orchestrator↔Specialist Invocation Contract"; "Refinement to Capability 4 — Capability Layering"; "Refinement
— Automatic Capability/Model Selection." Sources underlying those sections: Anthropic multi-agent research
system post, Claude Code `sub-agents`/`agent-teams`/`cross-session-messaging`/`permissions`/`mcp`/`skills`
docs, LangGraph supervisor + `human-in-the-loop` docs, OpenAI Agents SDK `tools`/`guardrails`/`handoffs` docs,
Systima "The Subagent Tax" benchmark, Arize AI role-tiering benchmark, `mcp-audit`/`deadskills`/`skillreaper`.

Fresh this session (2026-08-12), for the MISSING-capability question specifically:
- `WebSearch`: "independent evaluation of AI agent output quality after deployment LLM-as-judge builder bias
  2026" — surfaced self-bias/conflict-of-interest concern for same-family judge models (Microsoft Community
  Hub, Azure AI Foundry blog); "Agent-as-a-Judge" (arXiv 2601.05111); "ProofAgent Harness" adversarial
  evaluation infra (arXiv 2605.24134).
- `WebSearch`: "agent evaluation framework production monitoring drift regression Claude Skills 2026" —
  surfaced regression-set/drift-cluster practice for Claude Skill stacks (FutureAGI), scheduled trace-report
  tooling (Halo), and academic drift-quantification work (arXiv 2601.04170, arXiv 2605.01604).
- `WebFetch` direct, `anthropic.com/engineering/demystifying-evals-for-ai-agents` (official, Confirmed tier):
  asked explicitly whether the post recommends separating the building process from the grading process.
  **It does not.** It recommends distributed eval-authorship (PMs/CSMs/salespeople contribute eval tasks) and
  LLM-judge calibration against human graders — governance and calibration, not builder-independence. This
  is a real, checked negative finding, not an assumption: even the most current official first-party guidance
  on agent evals does not establish independent-of-builder evaluation as a governing norm.

## MISSING capabilities (none of the 17 covers these; separate from the KEEP/MERGE/REPLACE table)

**M1 — Independent post-build evaluation of an agent's actual professional output over time.** The
owner-suspected gap, confirmed. Distinct from Capability 5 (code review during build) and Capability 10
(benchmark/eval mechanics in general) and from `skill-creator`'s eval loop (which evaluates one Skill's test
prompts, always with the Skill's own author present, not a deployed agent's real ongoing output). Confirmed
absent from all 17. Confirmed, via the fresh Anthropic fetch above, that this gap is not unique to Engineer —
current first-party AI-agent-engineering practice does not treat builder-independence as solved either. Real,
but partial, external mechanisms exist (LLM-as-judge with human calibration, "Agent-as-a-Judge" adversarial
harnesses, regression-set/drift-cluster monitoring for Claude Skill stacks) — none of them is installed or
adapted anywhere in Engineer's current or candidate set.

**M2 — Maintenance/drift: periodic Skill/agent-loop revalidation after a model change, and capability
retirement.** Already partially named in this project's own earlier research today (`Refinement — Automatic
Capability/Model Selection`): no scheduled, calendar-driven mechanism was found anywhere in the world for
this; only manual/symptom-triggered tooling (`mcp-audit`, `deadskills`) exists as a real precedent. Engineer's
own Locked decision (2026-08-11, "архитектурные решения про agent loop — временные, не окончательные")
already commits Engineer to revisiting agent-loop architecture on model change, but no installed or
candidate Skill among the 17 operationalizes that commitment — `claude-api`'s `migrate` subcommand is the
closest partial match, and it only covers raw API-call code, not Skills or agent-loop design.

**M3 — Full-spectrum (Skills + MCP + Models) discovery at build time, not Skills alone.** Engineer's own
Locked "Эталон обязанностей" item 1 (2026-08-12) explicitly requires finding what exists across all three —
"не только Skills." `capability-creation-methodology`, the one candidate that does systematic domain
discovery, only reaches Skills/market/open-source/methodology research for a whole profession — it does not
mention MCP servers or model selection anywhere in its 9 phases. No other candidate fills this.

**M4 — Permissions/least-privilege security audit as its own discipline.** Not newly discovered by this
audit — already logged by Engineer itself (`ENGINEER/DECISIONS.md`, 2026-08-12, "Три observations от внешней
сверки Researcher: не вносить в repository-design сейчас" — least-privilege/`allowed-tools` was one of three
named observations, explicitly deferred, not assigned a home). Reconfirmed here as still missing in practice
across all 17 ENGINEERING Skills — cross-referenced, not re-claimed as a new finding.

## Locked-role verdict — evidence trail

Engineer's Locked role (`ENGINEER/DECISIONS.md`, 2026-08-12): "устойчиво достигал требуемого профессионального
результата," with Foundation/Skills/tools/permissions/memory/interfaces/validation named as means, not the
boundary of the responsibility.

Concrete, evidenced gaps against that role (each tied to a real incident already in `ENGINEER/DECISIONS.md`,
not a hypothetical):
- Capability 6 (Skill authoring/testing) not installed, yet Engineer already authored/evaluated 3 Skills by
  improvising each time (`skillctl.py evaluate` run ad hoc, `installer` end-to-end run found and fixed
  reactively, no pressure-test/eval-loop backing any of the three).
- Capability 7 (execution orchestration) not installed; Engineer's only real orchestration to date
  (Engineer→Researcher direct call, 2026-08-12) used raw `Agent`/`SendMessage` with no named methodology, and
  its own governing rule is still explicitly `Proposal`, not `Locked`.
- Capability 9 (build-quality discipline) not installed; Engineer's one real code-level fix to date
  (`update.sh`, 2026-08-12) was verified by an improvised "run it twice on isolated copies" test, not a named,
  reusable discipline.
- M1 (independent post-build evaluation) fully missing — directly undermines "устойчиво достигал" as a
  standing, checkable property rather than a one-time build-completeness checklist result.
- M2 (maintenance/drift) fully missing — directly undermines "устойчиво" over time as models change, despite
  Engineer's own Locked commitment to revisit agent-loop architecture on model change.
- M3 (Skills+MCP+Models discovery) fully missing — directly contradicts Engineer's own Locked 6-point
  Эталон, item 1, written the same day as this audit.

What Engineer *can* currently do reliably, evidenced by real completed work: repository structure design/
audit against Foundation (repository-design, VERIFIED·LIVE, used on Researcher's own remediation), decision
recording (decision-documentation, VERIFIED·LIVE, used consistently across the entire `DECISIONS.md` log),
category-level tool routing (tool-selection, DRAFT but in active, correct use).
