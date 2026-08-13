# Observability / execution record for independently-living (non-child) agents

Brief: 5th direct call from Engineer, 2026-08-12. Question registered in `ENGINEER/OPEN_QUESTIONS.md`
(2026-08-12, "Как production-системы обеспечивают observability/execution record для самостоятельно
живущих (не дочерних) агентов"). Criterion fixed before search: 2-3 real production systems, each
checked against most of the 8 sub-questions, with source; honest "not found" where absent; explicit
applicability to the real case (Claude Code, separate Engineer/Researcher repos, no shared server).
No design proposal — Craft/Engineering boundary respected.

## System 1 — Anthropic Managed Agents (Claude Developer Platform) — Confirmed, official docs fetched directly

Fetched directly this session: `platform.claude.com/docs/en/managed-agents/observability`,
`platform.claude.com/docs/en/managed-agents/session-operations`.

1. **Where stored**: platform-side, Anthropic's own infrastructure — not the client, not the agent's own process.
2. **Who creates it**: the platform, automatically, on `POST /v1/sessions` (`client.beta.sessions.create()`). The developer does not build a record; every session event is persisted by the platform as it happens.
3. **How the creator/orchestrator retrieves it**: by `session_id` — `GET /v1/sessions/{session_id}` (retrieve status), `GET /v1/sessions/{session_id}/events` (full event history), `GET /v1/sessions/{session_id}/events/stream` (live SSE), `GET /v1/sessions?agent_id=...` (paginated list across an agent's sessions).
4. **Retention**: session history "persisted until deleted" (no default TTL) — quoted directly. Sandbox state (files/tools inside the container) has a separate, harder 30-day TTL regardless of activity, after which a resumed session gets a fresh sandbox.
5. **Link to task spec/contract**: not a formal contract object. Task intent travels as a `user.message` event; a `system.message` event can append operator-level context mid-session. No dedicated "spec" field found.
6. **Minimum data per event**: `id`, `type`, `processed_at` (server timestamp), `content` (event-specific payload) — every tool call and its result carries timestamps and duration.
7. **Retrievable without a human**: yes, fully — every retrieval/list/resume call above is a plain authenticated API call, scriptable end to end.
8. **Works for a long-lived, independently-run agent, not parent→child in one session**: yes, explicitly — a session is created once, its ID stored anywhere durable (a database, a config file), and resumed at any later time by any process holding that ID and the API key; nothing in the mechanism assumes a parent session.

## System 2 — OpenAI Responses + Conversations API (successor to Assistants/Threads) — Confirmed (direct fetch), Medium depth

**Important, time-sensitive correction to the brief's own suggested reference**: OpenAI's Assistants/Threads
API — named in the brief as the likely closest analog — is being deprecated **2026-08-26**, i.e. two weeks
after this investigation (`learn.microsoft.com` Azure OpenAI Q&A thread; `developers.openai.com/api/docs/assistants/migration`,
both surfaced via WebSearch). The load-bearing current system is its replacement: the **Responses API** (runs
a request) + **Conversations API** (stores the exchange), fetched directly at
`developers.openai.com/api/docs/guides/conversation-state`.

1. **Where stored**: server-side, OpenAI's infrastructure.
2. **Who creates it**: the developer explicitly creates a conversation object (`openai.conversations.create()`); response objects are created per call, with persistence opt-out via `store: false`. Not fully automatic the way Anthropic's session creation is — the developer must choose to persist.
3. **How retrieved**: pass the stored `conversation_id` into a later `responses.create(conversation=conversation.id)` call, or chain via `previous_response_id`. A direct "fetch this response/conversation and read its history" retrieve endpoint exists per the API reference but its exact call shape was not confirmed to source-hierarchy-1 depth in this pass (the page summarizing it did not show the literal call).
4. **Retention**: quoted directly — "Response objects are saved for 30 days by default"; "conversation objects and items in them are not subject to the 30 day TTL" (i.e. two different retention policies for two different object types).
5. **Link to task spec**: not found in what was fetched — no metadata/contract field documented.
6. **Minimum data**: not explicitly specified in the fetched guide beyond role/content message items.
7. **Retrievable without a human**: yes, plain API calls.
8. **Works for independent, long-lived agents**: yes, confirmed directly quoted — "you can keep using it across sessions, devices, or jobs," explicitly not conditioned on a parent/child relationship.

## System 3 — OpenTelemetry GenAI Semantic Conventions (+ LangSmith as one real backend it feeds) — Established/Medium

Fetched directly (partial — the canonical page had moved) plus WebSearch aggregation, cross-checked against
one further search specifically for span/attribute names.

**Structural finding, load-bearing for the applicability question below**: OTel GenAI conventions are **not
themselves a storage or retrieval system** — they define a vendor-neutral *data shape* (`invoke_agent` span,
`gen_ai.operation.name`, `gen_ai.agent.id`/`.name`, `chat`/`execute_tool` child spans, a single `trace_id`
linking the whole agent run) that something else — a collector/backend — must ingest, store, and serve. As of
mid-2026 every `gen_ai.*` signal in the official registry is still tagged "Development," not "Stable" (per
`dev.to/azena-ai` and `greptime.com` summaries, WebSearch-aggregated, Medium confidence — not independently
re-fetched from the raw spec repo this session, one fetch attempt to the moved canonical URL succeeded for a
generic confirmation only).

**LangSmith**, as one concrete backend a self-instrumented agent can send traces to (`docs.langchain.com/langsmith/trace-with-api`,
WebSearch-aggregated, Medium): a genuinely separate service from the agent's own runtime — `POST /runs` /
`PATCH /runs` (basic tracing) or `POST /runs/multipart` (batch), with a caller-supplied or server-issued
`run_id`/`trace_id` used for later retrieval; base retention 14 days, extended retention 400 days (both
explicit, quoted). This is the "tracing as a decoupled service" family the brief pointed at, distinct from
Systems 1-2 where the same platform that runs the agent also stores its record.

**Honest gap**: none of the OTel/LangSmith material found this session states how a creator would *discover*
which `trace_id` belongs to a specific independently-launched agent without already being told it out of
band — same limitation Systems 1-2 have (an ID must travel through some other channel), just made more
explicit here because there is no single owning platform to ask.

## System 4 — Claude Code's own native session mechanism (not Managed Agents) — Confirmed, official docs fetched directly

Fetched directly: `code.claude.com/docs/en/sessions`. Included because it is the actual runtime Engineer and
Researcher already run on — most directly comparable to "our real case," not a hypothetical migration target.

1. **Where stored**: locally, on disk — `~/.claude/projects/<project>/<session-id>.jsonl`, one file per session, **for every session, not only subagents** (the same class of file Engineer already parsed by hand for a *child* subagent turns out to be the general mechanism, not a subagent-specific one).
2. **Who creates it**: the harness, automatically — "Claude Code stores it locally as you work," no developer action needed to start persistence.
3. **How retrieved by another process**: **directly confirmed to work across independently-launched sessions, not only parent→child**: `claude --resume <session-id>` "looks for the ID in the current project directory and its git worktrees first, then **in every other project on this machine**" — i.e. any session anywhere on the same machine is resumable by ID regardless of how it was started. Scriptable form for exactly this use case, quoted directly: `claude -p --resume <session-id> --output-format json "summarize what we changed" | jq -r '.result'`.
4. **Retention**: 30-day default, configurable via `cleanupPeriodDays` in `settings.json`; storage location itself movable via `CLAUDE_CONFIG_DIR`.
5. **Link to task spec**: none built in as a formal object; the closest mechanism is a `SessionEnd` hook receiving a `transcript_path` field, which "can archive the transcript when a session ends" — an event hook, not a spec/contract linkage.
6. **Minimum data**: not documented as a stable public schema — explicitly the opposite: "the entry format is internal to Claude Code and changes between versions, so scripts that parse these files directly can break on any release." The documented, stable interfaces are `/export` (human-readable), `claude -p --output-format json/stream-json` (structured, scriptable), and hook `transcript_path` fields — not the raw JSONL.
7. **Retrievable without a human**: yes, via `claude -p --resume <id> --output-format json`.
8. **Works for independently-launched, non-child sessions**: **yes, confirmed** — this directly closes the specific gap the brief opened with (Engineer's own subagent-only JSONL-parsing case). The mechanism is not scoped to a subagent tree at all; it is a machine-wide session registry keyed by session ID.

## Direct answer to applicability (per the brief's explicit requirement, not a design proposal)

- **Systems 1-3 do not apply to the real case as-is**: each requires either migrating Engineer/Researcher onto
  a different vendor platform (OpenAI), a different Anthropic product surface (Managed Agents — a session/
  sandbox runtime, not plain Claude Code CLI), or standing up observability infrastructure that doesn't exist
  today (an OTel collector, a LangSmith account) — real infrastructure investment, not a fact already true of
  the two repos.
- **System 4 (Claude Code's own native session mechanism) is the one piece of evidence that is already true
  of the actual environment, no new infrastructure needed**: `claude -p --resume <session-id> --output-format
  json` is a real, documented, scriptable way for one process to retrieve another, independently-launched
  session's structured output by ID — and it is explicitly not limited to parent→child. The real constraint it
  carries, not solved by anything found this session: it works **only on the same machine** (the lookup is
  described as scanning "every other project on this machine," nothing beyond it), and the session ID itself
  still has to travel between Engineer and Researcher through some other channel (there is no cross-repo
  registry) — the same "ID must arrive out of band" gap every other system in this batch also has, just
  without a platform account to look it up against.
- Whether Engineer and Researcher in fact run on the same machine/user account today, and whether that
  constraint is acceptable long-term, is a fact about the current setup and a design question respectively —
  both left to Engineer, not decided here.

**Evidence level**: Confirmed (Anthropic Managed Agents observability/session-operations docs — official,
fetched directly, exact API methods and quoted retention language) · Confirmed (Claude Code sessions docs —
official, fetched directly, exact CLI/API syntax and quoted retention/format-stability language) · Confirmed/
Medium (OpenAI conversation-state guide — official, fetched directly, but the assistant summarizing it could
not confirm the exact retrieve-endpoint call shape) · Established/Medium (OpenTelemetry GenAI conventions —
one direct fetch confirmed only that content had moved; span/attribute names confirmed via a second, targeted
WebSearch; stability-status and LangSmith retention numbers are WebSearch-aggregated, not independently
re-fetched from a primary page this session).
