# Evidence log — Skill anatomy: FACT map from Dmitry's skill-guide and the real Skills it makes visible

Date: 2026-08-08. Object: the actual internal structure of "Skill" as a unit — not Дмитрий's `skill-guide` itself (that is a catalog/observation tool over two Skill ecosystems, not a Skill implementation — established separately, see below), but the four independent Skill implementations reached through it. This is a Stage 1 (Collection) + Stage 2 (Verification) checkpoint, not Stage 3 (Decomposition) or Stage 5 (Judgment) — no mechanism-naming, no transfer/adoption judgment, no comparison to the owner's own agents. That is explicitly deferred to a later, separate stage (world practices, then the owner's old Skills).

## Sources (all primary artifacts, source-hierarchy level 1 — fetched and read directly)

- `github.com/Ntmib/skill-guide` — full repo clone, all scripts read (not a Skill implementation; a catalog tool over the two ecosystems below).
- `agentskills.io/specification` — the official Agent Skills format spec (fetched via WebFetch).
- `github.com/anthropics/skills` — full repo clone; `template/SKILL.md`, `skills/internal-comms/SKILL.md`, `skills/pdf/SKILL.md` + `forms.md`, `skills/docx/`, `skills/skill-creator/SKILL.md` (full, 486 lines) read directly.
- `github.com/obra/superpowers` — full repo clone; `skills/using-superpowers/SKILL.md`, `skills/systematic-debugging/SKILL.md` (full, 284 lines) read directly; folder trees of `test-driven-development`, `writing-skills` inspected.
- `github.com/garrytan/gstack` — full repo clone; `AGENTS.md`, `SKILL.md.tmpl` (router), `cso/SKILL.md` (first 130 of 1285 lines), `cso/sections/manifest.json` read directly; folder trees of `qa`, `review`, `office-hours` inspected.
- `~/.codex/skills/.system/` on this machine — local, not cloned: `imagegen`, `openai-docs`, `plugin-creator`, `skill-creator`, `skill-installer` folder trees inspected; `imagegen/agents/openai.yaml` and `skill-installer/SKILL.md` read directly.

Sampling caveat: not exhaustive. `anthropics/skills` has 17 skills, `superpowers` 14, `gstack` ~60 — 2-6 were opened per repo, picked for structural diversity (simple / complex / router / meta), not at random and not all. Any claim below about a repo's *internal* pattern is grounded in the files actually opened; claims about *frequency across the whole repo* are not supported and are marked UNKNOWN where relevant.

---

## 1. Minimal common contract of a Skill

- **FACT** — A directory whose name is the skill's identifier, containing a `SKILL.md` file with YAML frontmatter (`name`, `description`) followed by a Markdown body. Confirmed by the official spec and directly observed, independently, in all four implementations (Anthropic, superpowers, gstack, Codex).
- **FACT** — The spec requires `name` to match the parent directory name exactly, plus a specific character set (`a-z0-9-`, no leading/trailing/double hyphen).
- **INFERENCE** — Because this exact shape recurs across four vendor-independent implementations rather than being copied from one shared codebase, it functions as a de facto cross-platform convention, not an artifact of one specific product. (No source states this as a claim; it is an inference from convergence.)

## 2. Mandatory vs. optional

- **FACT** (per spec) — Mandatory: `SKILL.md` itself, and within it `name` + `description`. Optional: `license`, `compatibility`, `metadata`, `allowed-tools`, and any bundled files/directories.
- **FACT** — Real implementations do not stay inside this list. gstack's compiled `SKILL.md` carries top-level frontmatter keys the spec does not define at all (`preamble-tier`, `version`, `triggers`) rather than nesting them under the spec's own `metadata` escape hatch.
- **FACT** — The body has no required internal structure per spec ("no format restrictions... write whatever helps agents perform the task effectively").

## 3. What can exist around SKILL.md

- **FACT** — Spec-named optional directories: `scripts/`, `references/`, `assets/`.
- **FACT** — Structures observed in real skills that are outside this named trio: `agents/*.md` (Anthropic `skill-creator` — subagent prompts; conceptually different from) `agents/openai.yaml` (Codex — a per-skill catalog descriptor: display name, icons, default prompt); `examples/` (Anthropic `internal-comms`, superpowers `writing-skills`); `sections/` + `manifest.json` (gstack — declarative on-demand section registry with `id`/`file`/`title`/`trigger`); `specialists/` (gstack `review` — multiple named reviewer-perspective files bundled in one skill); `templates/` (`docx/scripts/templates`, `qa/templates`); repo-level `hooks/` sitting outside any individual skill folder (superpowers).
- **FACT** — superpowers does not use the `scripts/references/assets` convention at all; auxiliary files (`root-cause-tracing.md`, `defense-in-depth.md`, `condition-based-waiting.md`, `CREATION-LOG.md`, `test-pressure-*.md`) sit flat next to `SKILL.md`.
- **FACT** — In gstack, the checked-in `SKILL.md` is a generated artifact, not the source; the source is `SKILL.md.tmpl` (+ per-section `.tmpl` files), compiled by `bun run gen:skill-docs`, with an explicit "do not edit directly" comment in the output.

## 4. How a Skill is selected / triggered

- **FACT** (direct quote, Anthropic `skill-creator/SKILL.md`) — "Skills appear in Claude's `available_skills` list with their name + description, and Claude decides whether to consult a skill based on that description... Claude only consults skills for tasks it can't easily handle on its own — simple, one-step queries... may not trigger a skill even if the description matches perfectly."
- **FACT** — `skill-creator` explicitly instructs authors to write `description` in a deliberately "pushy" register, stated reason: to counteract the model's own tendency to under-trigger skills.
- **FACT** — Real skill bodies almost always restate "when to use" a second time, in human prose, as a distinct piece of text from `description` — observed in `internal-comms` ("## When to use this skill"), `pdf` (opening description line), gstack's `cso` ("Use when:"), gstack's router (a phrase→command dispatch table).
- **FACT** — gstack adds a third, separate frontmatter field, `triggers` (an explicit phrase list), not part of the official spec and not observed in any other source.
- **UNKNOWN** — The actual matching mechanism (how a natural-language task is scored against a `description` string) is not disclosed as code or algorithm in any of the four sources; it is only asserted declaratively ("Claude decides") and observed through its external effects and the tuning advice built around it.
- **UNKNOWN** — Whether the triggering mechanism differs between Claude Code and Codex; both use name+description, but neither source's internals were reachable to compare.

## 5. How a Skill executes

- **FACT** (spec) — Once a skill is activated, the agent loads the entire `SKILL.md` body into context ("the agent will load this entire file once it's decided to activate a skill").
- **FACT** — Beyond that load, execution is just the agent following the body as ordinary instructions; the spec defines no separate skill "runtime" or execution engine.
- **FACT** — Bundled `scripts/` are run through the agent's ordinary tools (e.g. Bash), not a dedicated skill runner — confirmed by direct invocation examples in the sources (`python scripts/check_bounding_boxes.py fields.json`, `python -m scripts.aggregate_benchmark`).
- **FACT** — gstack specialist skills open with a shared bash "preamble" block (self-update check, session dedup, reading multiple persisted config flags, session-kind detection, opt-in telemetry, per-project cross-session "learnings" retrieval). This is not part of the spec.
- **INFERENCE** — Since this preamble pattern appears in none of the spec, Anthropic's skills, superpowers, or Codex's system skills, and only in gstack, it reads as one implementation's own addition rather than a general property of the Skill format. (Inferred from absence in three sources plus presence in one, not stated as a rule anywhere.)

## 6. How Skills compose

- **FACT** — Explicit cross-reference by name: `systematic-debugging` invokes `superpowers:test-driven-development` and `superpowers:verification-before-completion` by name inside its own body text.
- **FACT** — Explicit priority ordering stated in prose: `using-superpowers` — "process skills come first... then implementation skills."
- **FACT** — Explicit bundling: gstack's `/guard` = `/careful` + `/freeze`.
- **FACT** — Explicit fixed pipeline: gstack's `/autoplan` runs CEO → design → eng → DX review skills in sequence.
- **FACT** — No source, including the official spec, defines a structural frontmatter field for composition (no `depends_on` / `calls` / `requires`). Every composition example found is expressed in body prose or in external routing logic, never in the format itself.
- **INFERENCE** — Because four independent implementations each solve composition differently (inline name-reference, a separate priority-setting meta-skill, a router with a dispatch table, a fixed pipeline skill) and none reaches for a shared format-level mechanism, composition currently appears to be left to the skill author/ecosystem, not resolved at the Skill-format level.

## 7. How result-checking is structured

- **FACT** — Not a required part of the format in the spec or in any of the four sources.
- **FACT** — Where present, at least four distinct mechanisms were observed: (a) a standalone executable gate script that must pass before continuing (`pdf/forms.md` → `check_bounding_boxes.py`); (b) a phased process with a hard "cannot proceed without completing the prior phase" rule and a numeric escalation threshold (`systematic-debugging` — "3+ failed fixes ⇒ stop, question the architecture"); (c) delegation to a separate, named skill for the check (`superpowers:verification-before-completion`); (d) a full separate measurement loop for the *skill's own* quality as an artifact — evals/grading/benchmark in `skill-creator` (this checks the skill, not a given run's output).
- **FACT** — Some real skills opened have no result-check at all (`internal-comms`; base `pdf` outside the forms path).
- **UNKNOWN** — Whether any one of these patterns dominates across the ecosystem at large; the sample (4 sources, a handful of skills each, non-random) cannot support a frequency claim.

## 8. What belongs to the Skill itself vs. to its delivery/update infrastructure

- **FACT** (spec) — The Skill itself is the directory + `SKILL.md` + optional bundled files. Nothing beyond that is part of the format.
- **FACT** — Delivery/update is handled by three structurally different mechanisms, one per ecosystem observed: Claude Code's plugin/marketplace system — an external registry (`marketplace.json` + `installed_plugins.json`) living outside the skill folder on disk; gstack — clone of one monorepo containing all skills, plus its own template→build step (`bun run gen:skill-docs`); Codex — installation implemented as just another Skill (`skill-installer`), using plain scripts and the GitHub API, with no separate subsystem at all.
- **FACT** — Codex keeps catalog metadata (icon, display name) *inside* the skill folder (`agents/openai.yaml`); Claude Code keeps the equivalent catalog metadata (source, deeplink) *outside* the skill, in `marketplace.json`. The boundary between "part of the skill" and "part of the delivery infrastructure" is drawn in different places by these two ecosystems.
- **FACT** — Dmitry's `skill-guide` is a third, optional layer sitting on top of both delivery infrastructures — not part of the Skill format and not part of either delivery mechanism, but an external observation/cataloging tool over them (established in the prior turn of this investigation, restated here for completeness).

## 9. What remains unknown at this checkpoint

- **UNKNOWN** — The actual trigger-matching implementation (how a task is scored against `description`) — not public in any of the four sources.
- **UNKNOWN** — Default system behavior when multiple applicable skills exist and the author has defined no router/priority — no source describes a default; only what specific authors chose to script themselves.
- **UNKNOWN** — Quantitative prevalence of any pattern above — the sample is small and hand-picked for diversity, not representative; every claim here is "observed at least once in named source X," never "most skills do Y."
- **UNKNOWN** — World practices outside the Claude/Codex-derived ecosystems (other agent frameworks, closed corporate systems) — deliberately untouched at this stage; next stage by plan.
- **UNKNOWN** — How this maps onto the owner's own existing Skills — deliberately deferred to its own later stage.

## Summary

Four independent Skill implementations converge on exactly one shared contract — a named folder with `SKILL.md` (YAML `name`+`description` frontmatter, freeform Markdown body) — and diverge on everything past it: which extra folders exist, whether frontmatter stays inside the spec's field list, how triggering is reinforced in prose, whether/how results are checked, how skills compose, and how they are delivered and updated. No source defines composition or result-verification as part of the format itself; both are consistently pushed into body prose or external tooling. This checkpoint stops here by design — no mechanism-naming (Stage 3), no transfer judgment (Stage 5), no comparison to world practices or the owner's own agents yet.
