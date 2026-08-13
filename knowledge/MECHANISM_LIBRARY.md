# Mechanism Library — Obsidian Builder handoff

Not a project catalogue — an atomic registry of individual mechanisms, extracted from the Obsidian-agent/Obsidian-Builder investigation (2026-08-05), for consumption by the **Obsidian Builder** agent. One mechanism = one section, addressable by its `slug`, so a consuming agent can check "do I already have this" before adding a new entry (its own stated rule 4: update, don't duplicate) — same discipline this project already applies to its own memory and to `CAPABILITY_MAP.md`.

Distinct from `CAPABILITY_MAP.md`: that file is general AI-agent-system capabilities. This file is specifically Obsidian-vault-generation mechanisms, scoped to what a Builder can actually assemble from.

**Schema per entry**: `slug` / `layer` / `source` (+ hierarchy level, 1=primary artifact…5=marketing) / `maturity` / `reusable` (yes/partial/uncertain + reason) / `input` / `output` / `depends_on` / `last_verified`.

---

## Structure generation

### `para-folder-gen-vaulttoml`
**Source**: obsidian-forge (github.com/epicsagas/obsidian-forge), README — level 1. **Maturity**: medium — published crate, single maintainer. **Reusable**: yes, standalone CLI binary. **Input**: `vault.toml` (PARA-style config). **Output**: PARA folder layout + bundled templates + running daemon (inbox processing, backlink strengthening, git auto-commit). **Depends_on**: nothing external — self-contained Rust binary. **Last verified**: 2026-08-05.

### `entity-schema-folder-gen-templatesyml`
**Source**: obsd (github.com/nicolaygerold/obsd), README — level 1. **Maturity**: low-medium — personal/opinionated tool. **Reusable**: yes — `templates.yml` format itself is extractable as a spec even independent of the CLI. **Input**: `templates.yml` (renameable entity types, per-entity templates with variables). **Output**: entity folders + templates + status-workflow automation (backlog→active→review→done). **Depends_on**: Node.js CLI runtime. **Last verified**: 2026-08-05.

### `profile-folder-gen-autovault`
**Source**: AutoVault (github.com/Spifuth/AutoVault), README — level 1. **Maturity**: medium — real, domain-locked to SOC/pentest. **Reusable**: partial — the config→profile→folder-set *pattern* is portable, the shipped profiles (pentest/audit/bugbounty) are not. **Input**: profile selection (minimal/pentest/audit/bugbounty). **Output**: folder layout + auto-applied templates + Dataview-powered dashboard + Templater/Nmap/Burp automations. **Depends_on**: Bash, Templater plugin, Dataview plugin. **Last verified**: 2026-08-05.

### `preset-folder-gen-bootstrap-vault`
**Source**: obsidian-second-brain (github.com/eugeniughelbur/obsidian-second-brain), `scripts/bootstrap_vault.py` — level 1 (raw file fetched directly). **Maturity**: high — part of an active, 3699★ repo. **Reusable**: yes — standalone Python script, invocable independent of the rest of the repo (`uv run python scripts/bootstrap_vault.py --preset builder`). **Input**: `--preset` (default/executive/builder/creator/researcher) + name. **Output**: `wiki/`, `boards/`, `templates/`, `raw/` folders, Kanban boards, `.base` files. **Depends_on**: `uv`/Python. **Last verified**: 2026-08-05.

### `plan-apply-safety-gate`
**Source**: claude-obsidian (github.com/AgriciDaniel/claude-obsidian), README — level 1. **Maturity**: medium — most rigorously engineered of all candidates found, no external adoption evidence. **Reusable**: yes, and general-purpose — not coupled to this project's specific vault schema, could gate any generation step. **Input**: target path + generation params. **Output**: a plan file + `approved_plan_sha256`; nothing is written until re-invoked with `--approved-plan-sha256 <hash> --apply`. **Depends_on**: Python 3. **Last verified**: 2026-08-05.

---

## Frontmatter / typed properties

### `native-bases-typed-entities`
**Source**: obsidian-second-brain, claude-obsidian (both use it in place of Dataview) — level 1 (confirmed in both READMEs). **Maturity**: high — first-party Obsidian feature, not a plugin. **Reusable**: yes, trivially — built into Obsidian itself. **Input**: `.base` file definitions. **Output**: typed, queryable entity views (Projects.base, People.base, Tasks.base, Daily.base pattern observed). **Depends_on**: Obsidian ≥ version supporting Bases. **Last verified**: 2026-08-05.

### `zod-typed-frontmatter-validation`
**Source**: Zodsidian (github.com/conorluddy/Zodsidian), README — level 1. **Maturity**: low — 0★, author-labeled "Experimental, W.I.P." **Reusable**: yes in principle, unproven in practice. **Input**: Zod schema per document type (project/decision/idea/plan/documentation/session/backlog/hub). **Output**: `zodsidian new <type>` scaffolds one document; validate/fix/index/query as ongoing commands; live-validation Obsidian plugin. **Depends_on**: Node.js, Zod. **Last verified**: 2026-08-05. **Note**: generates one document, not a vault — narrower scope than the other structure-generation mechanisms.

---

## Query / dashboard

### `dataview-query-engine`
**Source**: Dataview (github.com/blacksmithgu/obsidian-dataview) — level 1. **Maturity**: very high — one of the most widely adopted Obsidian plugins. **Reusable**: yes, completely, zero coupling to any Builder project. **Input**: DQL/DataviewJS queries authored against YAML/inline metadata. **Output**: live-rendered query results, re-evaluated on file change. **Depends_on**: nothing beyond the plugin itself. **Last verified**: 2026-08-05. **Note**: purely mechanical — no decision logic, confirmed by design.

### `homepage-launcher`
**Source**: obsidian-homepage (github.com/mirnovov/obsidian-homepage) — level 1. **Maturity**: high — established community plugin. **Reusable**: yes, fully decoupled. **Input**: designated note/canvas/workspace + optional startup command. **Output**: that view opens automatically on launch, replacing default "reopen last file." **Depends_on**: nothing. **Last verified**: 2026-08-05. **Note**: launcher only — does not generate dashboard *content*; that gap is currently unfilled by anything found (see Gaps in the report).

---

## Calendar

### `gcal-bidirectional-oauth-sync`
**Source**: Full Calendar Remastered (obsidian-full-calendar-remastered.github.io) — level 2, official docs. **Maturity**: high — active fork, documented, production use. **Reusable**: yes, fully, standalone plugin. **Input**: OAuth login + calendar source selection. **Output**: two-way sync (create/edit/delete in Obsidian ↔ Google), auto-refresh every 5 min, title-parsed color categories, event-linked notes. **Depends_on**: Google OAuth app/credentials. **Last verified**: 2026-08-05. **Note**: purely mechanical matching (event ID/title parsing), no judgment.

### `gcal-tasks-asymmetric-sync`
**Source**: "Google Calendar and Tasks Sync" (community.obsidian.md/plugins/google-sync) — level 2, official listing. **Maturity**: medium-high — documented, but manual-trigger only, requires self-hosted OAuth redirect bridge. **Reusable**: yes, fully decoupled. **Input**: Google OAuth + manual "Import"/"Sync now" trigger. **Output**: events/tasks imported into `events/`/`tasks/` folders with `googleId` frontmatter; local edits diffed and pushed back; cannot create/delete on Google's side. **Depends_on**: Google Cloud project + self-hosted redirect page. **Last verified**: 2026-08-05.

### `gcal-oneway-sync-unbuilt-dedup` *(low confidence — included for completeness, not recommended-grade)*
**Source**: Septikai/obsidian-google-calendar-sync, README — level 1. **Maturity**: low — author states "not intended for installation." **Reusable**: technically yes, practically no. **Input/Output**: one-way (Obsidian→Google, full-day events only); a note-vs-ICS dedup feature is described but never shipped. **Depends_on**: n/a. **Last verified**: 2026-08-05.

---

## Tasks

### `periodic-note-task-carryforward`
**Source**: Auto Tasks (github.com/jamiefdhurst/obsidian-auto-tasks) — level 1. **Maturity**: high — documented, rule-based. **Reusable**: yes, fully. **Input**: creation of a new periodic note. **Output**: incomplete tasks from the prior note carried forward (optionally preserving due dates), optional Kanban sync. **Depends_on**: Periodic Notes plugin, Tasks plugin. **Last verified**: 2026-08-05. **Note**: explicitly rule-based per its own docs, no AI.

### `event-triggered-task-workflows`
**Source**: TaskNotes Workflows (community.obsidian.md/plugins/tasknotes-workflows) — level 2, official docs. **Maturity**: high — official docs, ships as example workflows. **Reusable**: yes, requires TaskNotes core plugin as dependency. **Input**: YAML/Markdown workflow definitions (triggers: status change, date proximity, manual, cross-app). **Output**: time-tracking control, date rollover, priority escalation, metadata inheritance, Canvas card creation. **Depends_on**: TaskNotes core plugin. **Last verified**: 2026-08-05. **Note**: docs explicitly self-describe as "purely mechanical rule-based automation."

---

## Decision logic (the one genuinely agent-driven mechanism found)

### `conditional-llm-workflow-nodes`
**Source**: LLM Hub / Workflow Builder (github.com/takeshy/obsidian-llm-hub), README — level 1. **Maturity**: low-medium — single source, README-level verification only, no adoption data found. **Reusable**: yes architecturally, but the least externally validated mechanism in this library — flag confidence explicitly before relying on it. **Input**: natural-language-described workflow + LLM API key + workspace folder. **Output**: compiled pipeline with LLM nodes and conditional (if/while) branching based on note content evaluation. **Depends_on**: an LLM API key. **Last verified**: 2026-08-05.

---

## Write primitives

### `mcp-write-primitives`
**Source**: obsidian-mcp-server (github.com/Vasallo94/obsidian-mcp-server) and 5+ independently-implemented siblings (newtype-01, otaviosoaresp, StevenStavrakis, aleksakarac, cyanheads — noted, not individually opened). **Maturity**: high as a pattern — convergent across multiple independent implementations. **Reusable**: yes, maximally — explicitly designed to be driven by an external decision-maker, the most decoupled mechanism in this whole library. **Input**: MCP tool calls (create/patch/move/delete). **Output**: raw vault mutations, zero decision logic of its own. **Depends_on**: MCP-capable client (an agent). **Last verified**: 2026-08-05.

---

## Maintenance (post-bootstrap — relevant to Builder's future/handoff boundary, not to generation itself)

### `nightly-orphan-relink-moc` *(Unverified — flagged, not silently upgraded)*
**Source**: agent-second-brain "doctor" job — README only, level 2; the actual implementing skill file 404'd on direct check. **Maturity**: unverified. **Reusable**: uncertain — cannot be extracted with confidence, the logic itself was never directly read. **Last verified**: 2026-08-05 (attempt made, failed).

### `reconcile-consolidate-5phase`
**Source**: obsidian-second-brain, `/obsidian-reconcile` + nightly 5-phase consolidation — level 1/2 mixed (folder/command existence confirmed level 1, mechanism detail from README level 2). **Maturity**: high — part of the same active repo. **Reusable**: partial — implemented as slash-commands inside a larger Claude-Code-skill framework, not a standalone library call. **Last verified**: 2026-08-05.

---

## Reference / pattern-only (not executable mechanisms)

### `obsidian-syntax-agent-skill`
**Source**: kepano/obsidian-skills — level 1. **Maturity**: high, credible maintainer. **Reusable**: yes, fully — designed explicitly to be installed as a skill into any agent. **Input**: n/a (it's the skill itself). **Output**: agent gains correct Obsidian Markdown/Bases/JSON Canvas syntax knowledge. **Depends_on**: an agent capable of loading skills. **Last verified**: 2026-08-05.

### `llm-wiki-architecture-pattern`
**Source**: Andrej Karpathy's LLM Wiki gist (gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — level 1, fetched and read directly, not from secondary summary. **Maturity**: very high as an influential pattern (16M+ views, 5000+★ on the gist), zero as shipped code — the gist itself states "intentionally abstract... describes the idea, not a specific implementation." **Reusable**: not as code — as a spec to reimplement (which is exactly what obsidian-second-brain and claude-obsidian both did). **Architecture**: `raw/` (immutable sources) + `wiki/` (LLM-generated pages) + schema file + `index.md` + `log.md`. **Last verified**: 2026-08-05.

---

## Known gaps (nothing found implementing these, across every candidate examined)

- No mechanism generates a **general entity-relation schema** (arbitrary types + typed relations) — every schema found is a fixed vocabulary (PARA categories or persona presets).
- No mechanism **auto-designs a dashboard** from a schema — dashboards are always a manual Dataview-query + Homepage-pointer assembly.
- No mechanism wires **calendar or Tasks-plugin setup into the generation/init step** — both exist as mature standalone plugins, always requiring separate manual OAuth/config after vault creation, in every project examined.
- No structure-generation mechanism produces **typed relations between entities at build time** — link/graph maintenance is something the *maintenance*-layer mechanisms do after the fact, not something any `init` step produces upfront.
