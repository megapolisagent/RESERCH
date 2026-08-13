# Investigation Brief — AI Engineer / Agent Builder

**Target type** (per `MISSION.md` Input): professional domain.
**Date**: 2026-08-11.
**Status**: Stage 1–5 complete: `02-evidence.md` (28 sources, hierarchy + Stage 1.5 abstraction tags) → `03-full-report.md` (6 claims directly re-verified; profession model + full Intelligence Report) → `04-profession-model.md` (owner-facing rewrite, model-first). Knowledge Growth applied: `knowledge/MY_AGENTS.md` (Engineering Agent entry), `knowledge/CAPABILITY_MAP.md` (new Capability 11 — Restraint/Scope Discipline, plus refinements to Capabilities 8 and 9), `knowledge/EVIDENCE_INDEX.md` (Batch AIENG). **Open, not yet done**: a second, narrower design pass — which part of the broad AI Engineering profession becomes the actual profession of this project's own Engineering Agent (see owner's 2026-08-11 follow-up: profession vs. sub-specialization scoping, an Engineer-Skills gap table, and repository-authoring mechanics research).

## Framing

The question is not "how do people build an AI agent." It is:

> What knowledge must an AI Engineer hold who professionally assembles other AI agents, repeatedly, as a craft?

The end consumer of this investigation is a future **Engineering Agent** — an AI_OS agent whose job is to compose specialized agents from a Foundation + a Skills library + a task. This report is the evidence base that agent will be built from, not a one-off explainer.

## Channels (per Stage 1 source-type checklist, `skills/reverse-engineering/METHODOLOGY.md`)

1. **GitHub** (primary channel) — best open-source AI agents, frameworks, agent templates, production agent repos, prompt-engineering repos, skill repos, agent operating systems. Focus on structure: repo layout, memory structure, knowledge organization, routing, instructions, installer, skills architecture, update mechanism, documentation.
2. **Exa** — surfaces engineering practice not yet popular on GitHub: agent architecture, agent memory, skills, agent templates, foundation design, reusable agent architecture, agent operating systems.
3. **Web** — Anthropic, OpenAI, Google, Letta, LangChain, CrewAI, OpenAI Agents SDK, Claude Code, MCP, A2A. Real engineering decisions, not overview articles.
4. **YouTube** — author talks, architecture walkthroughs, live demos, deep dives only. Priority: product authors > conference talks > bloggers. Metadata-first (title, description, chapters); full transcript only once a video's unique value is confirmed — consistent with this skill's existing Stage 1 rule that video sources are a known weak point and should default to a written companion artifact where one exists.

## Explicit exclusions

"Best 100 AI agents" listicles, marketing overviews, "what is an AI agent" explainers, beginner tutorials, SEO content, LLM news.

## Investigation questions

1. What knowledge does an engineer who builds professional AI agents actually hold?
2. What responsibilities does such an engineer always carry out?
3. Which engineering decisions repeat across nearly all strong projects?
4. Which repository structures recur most, and why?
5. Which folders are genuinely necessary for an agent, and which exist only because of a specific platform?
6. How do strong projects organize: memory, knowledge, routing, workspace, instructions, updates, profile, communication?
7. How is a Skills system built — not the file format, but the full lifecycle from idea to an agent actually using it?
8. What makes a good Skill? What's mandatory in one? What checks does it pass? How is it documented?
9. How does an engineer recognize that existing Skills are insufficient? What are the signals, and what happens next?
10. How is a new agent designed — from idea to a finished repository?
11. What does good documentation for an AI repository look like (README, VISION, ARCHITECTURE, CONTRIBUTING, DECISIONS, etc.)? What's industry norm vs. what actually helps?
12. Which mistakes recur most often?
13. **Agent Composition.** Does world practice already have a settled, named engineering mechanism that solves: *Foundation + Skills library + task → minimal specialized agent*? If it exists: what is it called, where is it used, how is it implemented, what alternative approaches exist, and is it a Capability, a Skill, a Framework, or some other kind of entity? Do not invent terminology before the investigation is done — the point of this question is to check whether "Agent Composition" is a real, already-named mechanism or a genuine gap, not to confirm an idea already chosen.

## Token-economy strategy

1. Wide scan first, no deep reading.
2. From the wide scan, shortlist ~20–30 genuinely strong sources.
3. Deep-read only the shortlist.
4. When three or more sources say the same thing, record it once as consensus — do not re-log repeated information.
5. YouTube: never transcribe a video in full until its value is confirmed via metadata/chapters.

## Stage 1.5 — Abstraction tagging (mandatory, runs before Stage 2 Verification proper)

**Why this exists**: a shortlist collected across GitHub/Exa/Web/YouTube naturally organizes itself by vendor/product (Anthropic, OpenAI, Letta, Claude Code, MCP, OpenHands) because that's how the sources are structured — but the target of this investigation is a *profession*, not a set of platforms. Left uncorrected, the report drifts into "what Anthropic/OpenAI/Letta do" instead of "what an AI Engineer needs to know." A vivid, well-sourced fact like "Boris Cherny deletes Claude Code's system prompt on every model release" is evidence *for* a professional principle, not the principle itself — the transferable knowledge one level up is "instructions tend to decay as models evolve and need periodic, deliberate re-pruning, not indefinite accumulation." Both are true; only the second belongs in the profession model.

**The test, applied per finding**: would this still be true/useful if the specific vendor/product disappeared tomorrow? If yes, it's profession-level knowledge. If no, it's platform/implementation evidence — keep it as a citation supporting a higher-level claim, not as a finding in its own right.

**Tag every item in the consolidated shortlist with one of five levels**:
1. **Platform/vendor practice** — true of one team's current implementation only (e.g. the system-prompt-deletion ritual).
2. **Architectural mechanism** — a named, transferable technical pattern still tied to one stack (e.g. MCP lazy-loading via filesystem-style server navigation).
3. **Industry/format standard** — adopted as shared convention across independent vendors (e.g. SKILL.md becoming cross-vendor).
4. **Universal engineering principle** — survives the disappearance test (e.g. "instructions decay as models evolve").
5. **Professional/craft principle** — judgment about when *not* to act (when not to build an agent, not to write a Skill, not to add memory, not to reach for MCP, not to add orchestration) — the single most valuable category, because it is engineering judgment, not technology, and generalizes past any stack.

Level 5 findings ("design restraint") get first billing in the eventual profession model — noted as the strongest category found in Stage 1 precisely because it wasn't about a technology at all.

**Explicitly deferred, not acted on now**: the future Engineering Agent is a *systems engineer who works with AI*, not only an *AI engineer* — general software-engineering practice (build systems, package managers, plugin systems, dependency management, non-AI software architecture) is a legitimate source domain not yet searched (Installer Skills sit closer to npm/pip/apt/brew than to prompt engineering; repo structure sits closer to Linux/Kubernetes/Rust/Go conventions than to AI specifically). No new search is launched for this now — flagged as a candidate future channel, to revisit after this investigation's Stage 2–5 are done, not before.

## Deliverable

**Lead with a profession model, not a checklist.** The synthesis pass (Stage 5, Judgment) must first produce a coherent model of AI Engineering as a profession — what this craft actually is, as a whole — before descending into the itemized questions. Questions 1–13 are verification/detail against that model (knowledge required, Skills required, decisions the practitioner makes, documents produced, checks performed, recurring mechanisms), not a parallel, unordered list of findings standing next to it. A disconnected set of facts about the domain is worth less than a model of the craft; the model is the primary product, the checklist answers are what it's built and checked against.

Within that frame: one Intelligence Report in the `MISSION.md` Output order (best representatives → repeating mechanisms → rare-but-strong → marketing vs. real → what didn't work → industry standard → contradicting approaches with their trade-offs → what transfers to the future Engineering Agent and what explicitly doesn't, with reason → where sources genuinely disagree → what changed recently → sources).

## Knowledge Growth (mandatory — part of Definition of Done for this investigation, not optional follow-up)

Per `MISSION.md`'s Knowledge Growth section, this investigation is not complete when the report is written. It is complete only once:

- **`knowledge/MY_AGENTS.md`** gets a new entry for the future **Engineering Agent** (domain, known mechanisms found to transfer, investigated date, source).
- **`knowledge/CAPABILITY_MAP.md`** / **`knowledge/EVIDENCE_INDEX.md`** are updated with any new, stable capability this investigation surfaces (e.g. a Skills-lifecycle capability, a repo-structure capability, an Agent Composition capability if question 13 confirms one exists).
- A explicit list of findings meant to become permanent knowledge for the future Engineering Agent is produced — distinct from the report itself.

The goal of this investigation is not only to answer the question, but to increase the system's accumulated intellectual capital.

## Operating instruction (owner-stated, verbatim, governs the whole investigation)

> Не ищи подтверждение нашим идеям. Ищи лучшие инженерные практики мира. Если они противоречат нашей архитектуре — именно это и является самым ценным результатом исследования.

This is the standing check against confirmation-seeking for the entire investigation: a finding that contradicts the current Foundation architecture is not a failure of the search, it is the most valuable possible outcome of it.

**Research-economy addition, added once all three Stage 1 channels had returned.** Once a fact is genuinely established — including an absence, e.g. two independent hierarchy-1/2 sources agreeing a named mechanism doesn't exist (this happened for Q13: Exa/Web and GitHub channels independently found no settled name for "Foundation + Skills library + task → minimal agent") — record it and move on. Do not keep spending search budget re-confirming or further disproving an already-settled point across every remaining channel. The biggest value of this investigation is not the fate of any one mechanism, it is the coherent profession model above. Redirect any further research effort toward breadth (covering more of the checklist, deepening the profession model) rather than depth on a question that already has two-source agreement.
