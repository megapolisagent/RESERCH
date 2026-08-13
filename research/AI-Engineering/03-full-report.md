# Intelligence Report — AI Engineering as a Profession (the Agent Builder)

**Target** (per `MISSION.md` Input): a professional domain — the AI Engineer who professionally assembles other AI agents, repeatedly, as a craft.
**Scope documents**: `01-brief.md` (brief, incl. the 13 investigation questions and the two process amendments made mid-investigation), `02-evidence.md` (28 sources, hierarchy tags, Stage 1.5 abstraction tags). Owner-facing rewrite of this report: `04-profession-model.md`.
**Method**: `skills/reverse-engineering/METHODOLOGY.md` Stages 1–5, plus a project-specific Stage 1.5 (abstraction-level tagging) added mid-investigation specifically to stop a profession-domain investigation from drifting into a platform-comparison exercise.
**Stage 2 verification note**: 6 of the most load-bearing claims below were independently re-fetched from primary sources during this synthesis pass (not reused from the channel agents' earlier reads) — see inline citations marked "verified directly." The remainder rely on the channel agents' Stage 1 reads at the hierarchy level recorded in the consolidated shortlist; per the research-economy rule agreed mid-investigation, once two independent sources converged on a claim it was not re-chased for a third confirmation.
**Integration note (added 2026-08-11, retroactively, per Definition of Done condition 5a)**: this report originally shipped without a structured Integration section — the old §8 stated what transfers in prose, which left "so what do we actually do with each finding, and with which specific part of it" unanswered per finding. Section 1 below (moved up from its original position at the end, per the same 2026-08-11 revision) closes that gap using only material already in `02-evidence.md` — no new research, no new design.

---

## 0. Profession model (lead section — per the brief's Deliverable requirement, this precedes the standard checklist rather than sitting beside it)

AI Engineering, as practiced by the strongest observed sources, is not "prompt engineering" and not "building one agent." It is closer to **systems engineering applied to a probabilistic component** — the craft of deciding, for a given task, how much of the work to hand to an LLM versus how much to keep in deterministic code, memory, or tooling, and of packaging whatever *is* handed to the LLM as a minimal, reusable, inspectable unit. Four things are true of every strong source in this investigation at once:

1. **The default posture is restraint, not construction.** Every strong source treats "build an agent," "write a Skill," "add memory," "reach for MCP," "add orchestration" as a cost to be justified by the task, not a default to reach for. This is the single most consistent, most vendor-independent finding in the whole investigation (§3, §9.4 in `consolidated-shortlist.md`'s Level-5 list).
2. **The craft is largely about locating the deterministic/probabilistic boundary correctly** — deciding what the LLM proposes versus what code enforces — and re-drawing that boundary as models change, not once at design time.
3. **A meaningful share of what this profession needs is not AI-specific at all.** Durable checkpointing, protocol statelessness at scale, compile-once/target-many generation, and pass-by-reference over pass-by-value all appear in this investigation as *rediscovered* classical systems-engineering and build-systems principles, arrived at independently by teams building AI agents (`consolidated-shortlist.md` items 4, 17, 20, 28). The AI-specific part of the craft sits on top of ordinary software engineering, it does not replace it.
4. **Packaging reusable expertise (Skills) is converging on a shared, portable, cross-vendor format**, which changes what "knowing how to write a Skill" means: it is closer to knowing how to write a well-formed package for an ecosystem (npm/pip-shaped judgment) than to prompt-writing.

### 0.1 Knowledge the practitioner holds

- **The determinism boundary**: which decisions the LLM is allowed to make versus which a scheduler/state machine/validator enforces (`consolidated-shortlist.md` #2, #4; corroborated independently by `CAPABILITY_MAP.md` Capability 3, evidence N — four unrelated projects state the identical rule).
- **The three-primitive context toolbox and when each applies**: tool search (cache-preserving, dynamic tool-schema loading) vs. Skills (on-demand task instructions) vs. memory/compaction (cross-restart persistence) — a decision table, not an either/or (#14, verified against `anthropics/skills/shared/agent-design.md` by the GitHub channel agent at file level).
- **Skill packaging mechanics**: the `SKILL.md` contract — required `name`/`description` frontmatter, optional `license`/`compatibility`/`metadata`/`allowed-tools`, three-level progressive disclosure (metadata ~100 tokens always-on → body <5000 tokens on activation → bundled `scripts/`/`references/`/`assets/` on demand). **Verified directly** against `agentskills.io/specification` during this synthesis pass — the earlier GitHub-channel read is now corroborated by a fresh, independent fetch, satisfying Stage 2's independence-of-check rule.
- **Memory-tiering judgment**: when a flat markdown file suffices (Cline, spec-kit, OpenHands) versus when memory needs to become structured/queryable (Letta's tiered core/archival/recall model) — a real, unresolved fork, not a settled answer (#10–13).
- **When an architecture claim is likely to be dated**: Letta's own authors deprecated their MemGPT-style heartbeat/tool-reasoning loop in favor of native model reasoning, explicitly to stay "in-distribution" with how newer models are post-trained (**verified directly** against `letta.com/blog/letta-v1-agent`, quote: *"as models become more heavily post-trained on new agentic patterns, agent architectures benefit from converging to match these patterns — in other words, staying 'in-distribution'"*). A competent practitioner treats today's "best" agent-loop design as provisional, not load-bearing.

### 0.2 Responsibilities always carried out

- Deciding, for every new task, whether it needs an agent at all, or whether a workflow/deterministic pipeline is sufficient and preferable (#1).
- Authoring and periodically *pruning* instructions rather than only ever adding to them — Cherny's practice of deleting Claude Code's entire system prompt on every model release and rebuilding only for behaviors the model still stumbles on is the platform-level fact; the professional generalization is that instructions decay as models evolve (#25).
- Recognizing when a reusable capability (a Skill) is missing via an observable signal — the agent regenerating the same procedural work from scratch repeatedly — rather than a vague sense that "we should have a Skill for this" (#7, Zhang & Murag).
- Keeping platform-specific hardening (sandboxing, prompt-injection defense) outside the core reasoning loop as a wrapping layer, not baked into it (#26).
- Treating a Skill or reusable instruction set as a tested artifact requiring before/after evaluation evidence when changed, not documentation edited on a hunch (#8, `obra/superpowers`).
- Documenting decisions with context and consequences (ADR discipline), not just the decision itself, and flagging genuine uncertainty inline rather than silently guessing (`[NEEDS CLARIFICATION]` pattern, `github/spec-kit`) (#22, #24).

### 0.3 Decisions routinely made

Agent vs. workflow · how much control to delegate vs. retain (Anthropic's Skills-in-context posture vs. OpenAI's Handoffs/Agents-as-tools posture — a genuine, unresolved industry fork, §8 below) · flat-file vs. tiered/structured memory · eager vs. lazy capability loading · when a local convention is safe to keep bespoke vs. when to adopt an external standard before the migration cost compounds (OpenHands's own migration, §6).

### 0.4 Documents produced

ADRs (context + decision + consequences, not decision alone) · a constitution/governing-memory document distinct from task/session memory · SKILL.md packages for reusable expertise · architecture documents that separate "rules for building the system" from "what the system executes" (`block/goose`'s `AGENTS.md` vs. `recipe.yaml` split, #23).

### 0.5 Checks performed

Skill changes gated on before/after eval results, not shipped on inspection alone (#8) · uncertainty flagged inline during spec/plan authoring rather than resolved by guessing (#22) · architecture claims re-examined against current model training patterns rather than assumed permanent (#12).

### 0.6 The restraint layer — the strongest, most transferable category found

Ten level-5 findings converged independently across unrelated sources on a single theme: **professional judgment about when *not* to act is the load-bearing skill, not any specific technology.** Earn agentic complexity only when the task needs it; own your control flow rather than delegating it to a framework's loop; default to TDD once tests are cheap to generate; constrain agent fan-out to actual task complexity; recognize a missing Skill from a concrete behavioral signal, not a hunch; treat reusable instructions as tested code; start with the fewest memory blocks that work; surface uncertainty instead of guessing; document consequences, not just decisions; let a working prototype be the spec. None of these are AI-specific in their generalized form — the full list is reproduced in `consolidated-shortlist.md`'s Stage 1.5 section.

---

## 1. Integration

Per Definition of Done condition 5a (`METHODOLOGY.md`): one card per significant, **reusable** finding — a true fact about one object is not itself a card; the generalized lesson it supports is. Built only from what's already in `02-evidence.md` — no new research, no new design invented here. Decision options: **использовать полностью / адаптировать / объединить / отложить / не использовать**. Placed here, right after the profession model, because this is what the report is opened to act on — not left for the end of the document.

---

**Skill Creator (Anthropic) — SKILL.md format**
Назначение: формат упаковки переиспользуемого знания — `name`/`description` frontmatter, три уровня прогрессивного раскрытия.
Почему интересен: единственный формат, ставший подтверждённым кросс-вендорным стандартом, с реальным кейсом цены отказа от него (OpenHands).
Наш вывод: ☑ Адаптировано — материализовано 2026-08-11
Если адаптировать — с чем: с уже существующей конвенцией `skills/` в Foundation (`skills/installer/SKILL.md` уже использует `name`/`description`/`allowed-tools` — совместимость подтверждена напрямую, не предположена).
Куда идёт: Skill-System (`Skill-System/skills/repository-design/SKILL.md` — первый реальный Skill Engineer)
Приоритет: High
Почему именно так: собственная конвенция уже работает и обоснована тремя источниками собственной архитектуры Foundation; сверка показала совместимость с внешним спеком без переделки.
Что конкретно переносим: ✔ progressive disclosure (метаданные → тело → файлы); ✔ контракт `name`/`description` как обязательных полей — уже используется, подтверждено. ✘ конкретный directory layout примеров Anthropic; поле `allowed-tools` уже используется в Foundation независимо, не как заимствование.

**Progressive disclosure (3-уровневая загрузка: метаданные → тело → файлы)**
Назначение: экономия контекста — грузить только то, что реально нужно под задачу.
Почему интересен: подтверждён и на уровне спецификации, и отдельным измеренным кейсом (code-execution-with-MCP: 150k→2k токенов).
Наш вывод: ☑ Использовать полностью
Куда идёт: Skill System
Приоритет: High
Почему именно так: уже совместим с тем, как Foundation описывает `skills/` (загрузка по требованию) — требуется только дисциплина соблюдения при написании новых Skills, не адаптация механизма.
Что конкретно переносим: ✔ сам принцип целиком — переносится без изменений, ничего не отбрасываем.

**Governing/session memory split**
Назначение: устойчивая память системы хранится отдельно от памяти текущей сессии/задачи.
Почему интересен: независимо подтверждён у трёх не связанных проектов (OpenHands, spec-kit, Cline).
Наш вывод: ☑ Использовать полностью (уже используется)
Куда идёт: Foundation
Приоритет: Low — действие не требуется
Почему именно так: `MEMORY.md`/`DECISIONS.md` против `workspace/` в Foundation — это уже тот же паттерн; карточка фиксирует подтверждение, не создаёт задачу.
Что конкретно переносим: — уже реализовано, переносить нечего.

**Skills-as-tested-code (obra/superpowers)**
Назначение: изменение Skill требует before/after eval-доказательств, а не правки на глазок.
Почему интересен: редкая, но сильная дисциплина — единственный источник, где это явное требование.
Наш вывод: ☐ Отложить
Куда идёт: Skill System (будущее правило)
Приоритет: Medium
Почему именно так: у нас пока нет ни одного реального Skill, на котором можно проверить эту дисциплину — вводить правило раньше первой реальной правки было бы преждевременным проектированием.
Что конкретно переносим: пока ничего. Когда станет актуально: ✔ требование before/after проверки при правке Skill; ✘ конкретный формат eval из `obra/superpowers` — не видели его напрямую, только описание механизма.

**ADR discipline (context + decision + consequences)**
Назначение: решения документируются с причиной и последствиями, не только фактом.
Почему интересен: единственный формат документации, подтверждённый как несущий, а не декоративный, у нескольких независимых проектов.
Наш вывод: ☑ Адаптировать частично — Proposal подан 2026-08-11, не Locked
Если адаптировать — с чем: с уже существующим `DECISIONS.md` в Foundation — при проверке выяснилось, что структура «Статус / Что решается / Обоснование / Отклонённые альтернативы / Источник» уже покрывает контекст и решение; не хватает только явного поля «Последствия».
Куда идёт: Foundation
Приоритет: High
Почему именно так: изменение формата `DECISIONS.md` — это изменение собственной методологии агента, а не разовая задача; по правилу самого файла («высокий радиус поражения — независимая проверка перед Locked») предложение внесено как Proposal, не применено сразу тем же ходом рассуждений, который его придумал.
Что конкретно переносим: ✔ предложено добавить поле «Последствия» (запись в `Foundation/04_REPOSITORY/DECISIONS.md`, статус Proposal). ✘ полный статус-цикл (proposed→accepted→deprecated→superseded) — избыточен для текущего масштаба.

**ADR-as-a-Skill (`vercel/ai` adr-skill)**
Назначение: сама практика документирования решений упакована как Skill.
Почему интересен: показывает, что дисциплину выше (ADR discipline) можно не просто декларировать, а упаковать как переносимый инструмент.
Наш вывод: ☑ Объединено и материализовано — 2026-08-11
Если объединять — с чем: с карточкой "ADR discipline" — один Skill, не отдельный принцип и отдельный артефакт.
Куда идёт: Skill-System/skills/decision-documentation/ → установлен в Engineer/agent
Приоритет: Medium
Почему именно так: вместо того чтобы Engineer просто "помнил" про ADR-дисциплину, дан инструмент, который её применяет — построен на уже существующем формате `DECISIONS.md`, а не на ожидании Foundation-Proposal.
Что конкретно переносим: ✔ саму идею "документирование решений — это Skill, не только принцип"; ✔ уже существующий формат Foundation (Статус/Что решается/Обоснование/Отклонённые альтернативы/Источник). ✘ конкретную реализацию `vercel/ai` — не читали её напрямую, только описание механизма на уровне документации. ✘ поле «Последствия» — остаётся Proposal в Foundation, не встроено в Skill до Locked.

**Cline six-file memory bank**
Назначение: память разбита на 6 типизированных файлов по роли, а не на один общий.
Почему интересен: другой ответ на "сколько задач решает один файл памяти", чем однофайловый дефолт у большинства источников.
Наш вывод: ☐ Не использовать
Куда идёт: — (остаётся находкой Research)
Приоритет: Low
Почему именно так: `MEMORY.md` пока не показывает признаков перегрузки несколькими ролями сразу — вводить сейчас было бы just-in-case усложнением; источник к тому же слабо верифицирован (уровень документации, не файла).
Что конкретно переносим: ничего сейчас.

**Letta MemGPT heartbeat/tool-reasoning loop (устарел по признанию собственных авторов)**
Назначение: архитектура reasoning-цикла на heartbeat/tool calls.
Почему интересен: единственный источник, пойманный на живом развороте собственной архитектуры — прямое предупреждение против фиксации любого agent loop как постоянного решения.
Наш вывод: ☑ Использовать как правило — материализовано 2026-08-11
Куда идёт: Engineer/agent/DECISIONS.md (Locked-запись, не Skill — это правило поведения, не переносимая процедура)
Приоритет: Medium
Почему именно так: сам источник от механизма отказался; переносится не механизм, а обязанность — не считать ни одно решение про agent loop окончательным, зафиксировано как явное правило, а не оставлено подразумеваемым.
Что конкретно переносим: ✔ само предостережение, как явное Locked-правило Engineer. ✘ ничего из механизма Letta — не копируется.

**Bespoke skill-механизм при существовании внешнего стандарта (урок OpenHands)**
Назначение: обобщённый урок, не механизм — локальная конвенция, разошедшаяся со стандартом, требует миграции позже, и это не бесплатно.
Почему интересен: реальный, не гипотетический пример цены такого решения (сам факт "OpenHands мигрировал" — не карточка сам по себе; карточка — это генерализуемый урок за ним).
Наш вывод: ☑ Использовать как довод
Куда идёт: обоснование приоритета карточки "Skill Creator / SKILL.md" выше
Приоритет: High
Почему именно так: это причина, по которой сверка с SKILL.md-спеком помечена High, а не просто "когда-нибудь".
Что конкретно переносим: ✔ сам аргумент ("расхождение со стандартом стоит дороже позже, чем раньше"); ✘ детали миграции OpenHands — они не переносимы, специфичны для их кодовой базы.

**Stateful MCP-сессии (устаревший паттерн, разворот Google)**
Назначение: сессионные рукопожатия в протоколе MCP.
Почему интересен: подтверждённый, датированный разворот архитектуры под реальной production-нагрузкой.
Наш вывод: ☐ Не использовать
Куда идёт: — (Research, на будущее, если появится собственная MCP-инфраструктура)
Приоритет: Low сейчас
Почему именно так: у нас пока нет собственных MCP-серверов, куда это могло бы попасть — фиксируем как готовое знание, не как задачу.
Что конкретно переносим: ничего сейчас; на будущее — ✔ принцип "не проектировать session state в протокол на пути к масштабу".

**Skills-in-context vs. Handoffs/Agents-as-tools (Anthropic vs. OpenAI)**
Назначение: два разных способа композиции агента — грузить экспертизу в контекст против делегирования управления другому агенту.
Почему интересен: реальный, неразрешённый архитектурный разрыв между двумя ключевыми игроками рынка.
Наш вывод: ☐ Отложить
Куда идёт: Engineer (решение при первой реальной многоагентной задаче)
Приоритет: Medium
Почему именно так: у нас пока нет ни одной задачи, требующей выбора между этими подходами — решать заранее означало бы проектировать то, что можно выяснить в работе.
Что конкретно переносим: ничего сейчас — оба варианта остаются открытыми до первой реальной задачи.

**spec-kit: разделение constitution / templates / prompts**
Назначение: правила системы, шаблоны с чек-листами и промпты агента — три разных файла, не один.
Почему интересен: третий независимый источник (наравне с Foundation и OpenHands), подтверждающий разделение, которое у нас уже есть.
Наш вывод: ☑ Уже используется — подтверждено при материализации 2026-08-11
Куда идёт: Foundation
Приоритет: — (действие не требуется)
Почему именно так: при попытке материализовать эту карточку (взять приём `[NEEDS CLARIFICATION]`) выяснилось, что он уже реализован — `HOME.md`: «Не выдумывай цифры и результаты. Нет реального факта — пометь `[УТОЧНИТЬ]` и спроси», и `ROUTING.md` явно ссылается на ту же дисциплину. Карточка меняет статус с «использовать частично» на «уже есть», не создаёт задачу.
Что конкретно переносим: ничего — уже перенесено раньше, чем появилась эта карточка; остальная структура `.specify/` (templates/scripts) не переносится — у нас уже есть собственный, не хуже подтверждённый аналог.

**goose: `recipe.yaml` (инструкции + инструменты + параметры единым целым) + изоляция под-рецептов**
Назначение: минимальная специализированная единица работы под задачу; под-рецепты работают в полной изоляции от родителя.
Почему интересен: конкретный, работающий пример "минимального специализированного агента под задачу" — ближе всего к тому, чем должен заниматься Engineer.
Наш вывод: ☑ Адаптировать
Если адаптировать — с чем: с процессом Repository Assembly у Engineer — не копировать формат `recipe.yaml` дословно, взять принцип изоляции под-агента от родителя.
Куда идёт: Engineer
Приоритет: Medium
Почему именно так: копировать чужой конкретный формат сейчас — преждевременная реализация; принцип изоляции универсален и дёшево держать в голове с первой сборки.
Что конкретно переносим: ✔ принцип изоляции под-агента от родительского контекста/состояния. ✘ формат `recipe.yaml` и его YAML-синтаксис — не копируем.

**wshobson/agents: один Markdown-источник → генерация под харнесс**
Назначение: генерация нативных артефактов под разные среды исполнения из одного источника.
Почему интересен: сильнейшее найденное доказательство механики композиции, с честно незакрытым вопросом (алгоритм роутинга не описан нигде).
Наш вывод: ☐ Не использовать сейчас
Куда идёт: — (Research — решает проблему, которой у нас пока нет)
Приоритет: Low
Почему именно так: у нас один харнесс, не шесть — использовать сейчас значило бы решать не свою задачу.
Что конкретно переносим: ничего сейчас.

---

## 2. Best real representatives found, and why

- **Anthropic's Applied AI / Skills team** (Barry Zhang, Mahesh Murag) — authors of the mechanism most of the field is now converging on; the only source with a concrete, observable trigger for "a Skill is missing."
- **Claude Code team** (Boris Cherny, Cat Wu) — three independent, non-overlapping, non-marketing process claims (prompt-deletion discipline, Co-Work's hardening-outside-the-loop design, "ship demos not docs") from people who ship a production agent product daily.
- **`humanlayer/12-factor-agents`** (Dex Horthy) — the sharpest and most economically-grounded restraint argument (~100 founder interviews), independently converging with Anthropic's own restraint framing from a completely different angle.
- **Letta** — the only source offering a structurally different memory paradigm (tiered, queryable, agent-writable) rather than a variation on flat markdown files, *and* the only source caught reversing its own prior architecture live, which is itself valuable evidence about how fast "best practice" moves.
- **`wshobson/agents`** — the strongest concrete evidence of cross-harness composition mechanics (one Markdown source generating harness-native artifacts for 6 different platforms), honestly documented as leaving the actual request-routing algorithm unsolved.
- **`github/spec-kit`** and **`block/goose`** — the clearest structural separations found between governing rules, task templates, and executable units.
- **Google's MCP infrastructure team** and **Anthropic's MCP protocol work** — primary, dated, technically detailed evidence of a real architecture reversal (stateful → stateless) under production load.

## 3. Mechanisms that repeat across nearly all of them

- **SKILL.md progressive disclosure** as the shared packaging contract (metadata always-on, body on trigger, bundled files on demand) — independently confirmed via a direct fetch of `agentskills.io/specification` during this pass.
- **Governing/stable memory kept separate from session/task memory** — OpenHands (`repo.md`), `spec-kit` (`constitution.md`), Cline (`projectbrief.md` root) all independently split this; the consuming project's own `MEMORY.md`/`DECISIONS.md`/`SOUL.md` vs. `workspace/` split already matches this pattern (§9).
- **Lazy, on-demand capability loading over eager preloading** at every layer examined — Skills (progressive disclosure), MCP (code-execution-with-MCP's 150k→2k token reduction), tool search (cache-preserving dynamic schema loading).
- **Instruction/context non-accumulation as an active discipline**, not a passive default — three unrelated sources (Cherny, Horthy, Zhang/Murag) each push against letting instructions/context grow monotonically, from three different angles (prompt deletion, control-flow minimization, moving procedural knowledge out of the prompt entirely).
- **Deterministic control-flow ownership / a narrow LLM surface** in the highest-revenue production systems, per Horthy's interview base and Anthropic's own restraint framing.

## 4. What's rare but looks strong

- **Skills treated as tested code** (`obra/superpowers`) — before/after eval evidence required to change a Skill, not just a documentation edit. Rare; only one source in the shortlist does this explicitly.
- **ADR-as-a-Skill** (`vercel/ai`'s `adr-skill`) — documentation *practice itself* packaged and taught as a Skill, rather than left as an unenforced convention.
- **Cline's six-file typed memory bank** (`projectbrief`/`productContext`/`systemPatterns`/`techContext`/`activeContext`/`progress`) — a genuinely different answer to "how many jobs should one memory file do" than the single-file default most sources use, though this claim is doc-level, not file-verified (flagged weaker in the consolidated shortlist).

## 5. What turned out to be marketing

No specific claim that survived into the Stage 1 shortlist turned out, on verification, to be marketing dressed as engineering — the shortlist's exclusion criteria (no listicles, no "top 10," no vendor webinars, no reaction content) filtered this out before it reached this stage. This is stated explicitly per Definition of Done condition 8 rather than silently omitted: **abstained**, not found empty by oversight. (One Anthropic Skills webinar and a "How Anthropic Skills Actually Work" livestream of unverifiable host authority were screened out at Stage 1 for exactly this reason — see the YouTube channel's discard notes.)

## 6. What turned out not to work

- **Letta's own MemGPT-style heartbeat/tool-reasoning loop** — deprecated by its own authors (**verified directly**, `letta.com/blog/letta-v1-agent`), with an explicit acknowledged trade-off: developers lose transparency/control over reasoning tokens (now encrypted, immutable by providers) in exchange for better alignment with how current models are trained.
- **Bespoke, locally-invented skill/memory mechanisms, once an external standard exists.** OpenHands built its own `microagents` mechanism, then migrated toward the cross-vendor `.agents/skills/` standard, keeping the legacy path only for backward compatibility (**corroborated via independent web search** during this pass, not just the original channel-agent read: three-tier legacy path — `.agents/skills/` new/recommended, `.openhands/skills/` "V1 standard," `.openhands/microagents/` "V0 legacy" — confirms the original claim's substance, though the original binary "deprecated" framing is slightly overstated; the more accurate framing is "superseded as the recommended path, retained for compatibility").
- **Stateful session handshakes in the MCP protocol core**, at production scale. **Verified directly** against Google's engineering blog: standard round-robin load balancers can't route to the container holding an in-memory session, forcing sticky-session affinity that defeats autoscaling; a pod restart silently drops session state; remote deployments needed shared Redis session stores or gateway-level packet inspection, adding latency and cost. The fix removed the `initialize`/`initialized` handshake and `Mcp-Session-Id` header entirely, making every request self-describing.
- **Unconstrained agent fan-out** — Anthropic's own multi-agent research system spawned up to 50 subagents for simple queries before this was deliberately constrained; a named, real failure mode, not a hypothetical one.

## 7. What has become an industry standard

- **SKILL.md** — the clearest finding in this category. Verified directly against the primary spec: mandatory `name` (kebab-case, ≤64 chars, must match directory) and `description` (≤1024 chars) frontmatter, optional `license`/`compatibility`/`metadata`/`allowed-tools`, three-level progressive disclosure. Governance now sits with a vendor-neutral body (`agentskills.io`/`agentskills/agentskills`), not solely with Anthropic, and a real production project (OpenHands) has migrated toward it from a bespoke mechanism — the single strongest standardization signal in the investigation.
- **ADRs** (Context/Decision/Consequences, status lifecycle) — the one documentation format shown load-bearing rather than decorative across independent, unrelated projects (`adr.github.io`, `microsoft/agent-framework`, `vercel/ai`).
- **MCP**, trending toward protocol-level standard status, itself now mid-transition (stateful → stateless) under the same standardization pressure that produced SKILL.md's convergence.

## 8. Approaches that contradict each other, and the trade-off each side accepts

1. **Anthropic's Skills-in-context posture vs. OpenAI's Handoffs/Agents-as-tools posture.** Anthropic composes by loading expertise into one agent's context (Skills); OpenAI composes by transferring or delegating control between agents (Handoffs = full one-way transfer; Agents-as-tools = bounded delegated calls). Trade-off: Anthropic's approach keeps one coherent reasoning context but risks context bloat as more expertise is loaded; OpenAI's approach keeps each agent's context narrow but pays a coordination/hand-off cost and gives up single-context coherence. Neither source frames the other as wrong — this is a genuine, unresolved architectural fork, not a solved question.
2. **Flat markdown-file memory (OpenHands, spec-kit, Cline) vs. Letta's tiered, structured, queryable memory.** Trade-off: markdown files are simple, portable, human-readable, and require no extra infrastructure; Letta's model scales past what fits in context and supports agent-initiated memory editing via tools, at the cost of real infrastructure and a fundamentally different mental model. No source in this investigation argues one is universally correct — the fork is contingent on scale, not resolved in principle.
3. **Stateful vs. stateless protocol design**, resolved *in one direction* by evidence (§6) but only for the specific failure mode observed (horizontal scaling under load) — the trade-off given up by going stateless is that every request must now be fully self-describing, which pushes complexity to the client/caller rather than the server.

## 9. What transfers to the future Engineering Agent (and the Foundation it will assemble agents from), and what explicitly doesn't

**Transfers**:
- The governing-memory vs. session-memory split — already present in the Foundation's own `MEMORY.md`/`DECISIONS.md`/`SOUL.md` vs. `workspace/` structure; this investigation corroborates rather than contradicts that existing choice.
- SKILL.md-compatibility as a design constraint worth checking the project's own `skills/` folder against, given how far cross-vendor standardization has gone and the real migration cost OpenHands paid for staying bespoke.
- The lazy/on-demand capability-loading pattern as a default, at every layer (Skills, tools, memory) — not specific to any one vendor's implementation of it.
- The full level-5 restraint checklist (§0.6) as literal, checkable design questions for any future agent the Engineering Agent assembles.
- ADR discipline (context + consequences, not just decisions) for any design decision the Engineering Agent itself makes.

**Does not transfer**:
- Any single vendor's exact implementation mechanics as a required pattern — Cherny's specific prompt-deletion cadence, Claude Code's exact `context: fork` vs. `skills` field distinction, Letta's specific tool names for self-editing memory. These are platform/vendor-practice level (Stage 1.5 level 1) and are evidence *for* the generalized principles above, not themselves requirements.
- Letta's full tiered-memory infrastructure, unless and until the Foundation's own memory needs genuinely exceed what a flat file supports — adopting it pre-emptively would be exactly the kind of unearned complexity §0.6's restraint principle argues against.
- A named "Agent Composition" mechanism — because, per §10 below, no such settled mechanism exists to transfer.

Full item-by-item take/adapt/merge/reject detail with reasoning: §1 (Integration), above.

## 10. Where sources genuinely disagree (not smoothed into a single view)

1. **Whether "Foundation + Skills library + task → minimal specialized agent" is a settled, named mechanism.** It is not, established twice independently: the Exa/Web channel and the GitHub channel each separately searched for a name (Agent Composition, capability routing, etc.) and found none. Anthropic's own closest description (`consolidated-shortlist.md` #18) is deliberately left unnamed — **verified directly** during this pass: *"Putting it all together, the emerging agent architecture looks like a combination of..."*, never elevated to a proper noun. The underlying *capability* is real (multiple vendors implement some version of it); the field has not converged on what to call it or on one reference implementation. Per the research-economy rule set mid-investigation, this is recorded as settled and not re-chased a third time.
2. **Delegate-control vs. retain-control composition philosophy** (§8.1) — a live, unresolved fork between the two labs most cited in this investigation.
3. **Whether agent-loop architecture (heartbeat/tool-based reasoning vs. native model reasoning) is currently "solved."** Letta's own reversal (§6) means any claim about correct agent-loop design found anywhere in this investigation — including in this report — should be treated as provisional against the model generation it was designed for, not as settled doctrine.

## 11. What changed recently

- **SKILL.md's cross-vendor consolidation**, concretely evidenced by OpenHands's migration (2025–2026 window) and the existence of a vendor-neutral governance body.
- **MCP's stateful → stateless protocol shift**, dated to the Aug-2026 spec update per Google's engineering post — recent enough that older MCP-based designs assuming session handshakes are now behind current guidance.
- **Letta's `letta_v1_agent` architecture change**, moving away from MemGPT-style reasoning — recent enough that any prior citation of Letta's heartbeat/tool-based loop as current practice would now be dated.
- **Anthropic's January 2026 "Building Agents with Skills" post** — the most current articulation of the field's leading composition architecture, and still, as of this post, declining to name it as a formal mechanism.

## 12. Sources

Full source list with hierarchy tags (T1 primary/official, T2 vendor blog, T3 independent practitioner, T4 low-confidence/discarded) and Stage 1.5 abstraction-level tags: `02-evidence.md` (28 sources). Six claims re-verified directly during this synthesis pass, marked inline above: the SKILL.md spec (`agentskills.io/specification`), Anthropic's unnamed 4-layer architecture (`claude.com/blog/building-agents-with-skills...`), OpenHands's skills migration (corroborated via independent search after the original doc page didn't surface it directly), the absence of a documented routing algorithm in `wshobson/agents`, Letta's agent-loop reversal (`letta.com/blog/letta-v1-agent`), and Google's MCP statelessness rationale (`developers.googleblog.com/scaling-ai-agent-infrastructure...`).
