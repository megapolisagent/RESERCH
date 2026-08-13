# Evidence — Capability layering: available / belongs / permitted / recommended (2026-08-12)

Brief from Engineer, relayed from `ENGINEER/OPEN_QUESTIONS.md` (2026-08-12 entry, "Как зрелые системы различают «доступно среде» / «принадлежит агенту» / «разрешено агенту» / «рекомендовано для задачи»"). Synthesis lives in `knowledge/CAPABILITY_MAP.md` under "Refinement to Capability 4 (Permissions) — Capability Layering." This file is the raw source-level material behind that synthesis.

**Internal context read before external search** (per `METHODOLOGY.md`'s Internal-context-first rule): `ENGINEER/skills/tool-selection/SKILL.md`, `ENGINEER/skills/tool-selection/evidence.json`, `ENGINEER/OPEN_QUESTIONS.md` (2026-08-12 entry, fixed answer criterion), `knowledge/CAPABILITY_MAP.md` Capability 4 (Permissions, already documents deny>ask>allow, MCP-adjacent findings from prior sessions).

## Source 1 — Claude Code `code.claude.com/docs/en/mcp` (fetched directly)

MCP installation scopes table, quoted verbatim:

| Scope | Loads in | Shared with team | Stored in |
|---|---|---|---|
| Local | Current project only | No | `~/.claude.json` |
| Project | Current project only | Yes, via version control | `.mcp.json` in project root |
| User | All your projects | No | `~/.claude.json` |

"Local scope is the default. A local-scoped server loads only in the project where you added it and stays private to you... Use local scope for personal development servers, experimental configurations, or servers with credentials you don't want in version control."

"Project-scoped servers enable team collaboration by storing configurations in a `.mcp.json` file at your project's root directory... Check `.mcp.json` into version control so everyone on your team gets the same MCP tools and services."

"User-scoped servers are stored in `~/.claude.json` and provide cross-project accessibility, making them available across all projects on your machine while remaining private to your user account."

`claude mcp list` shows a health status "regardless of scope" — `✔ Connected`, `! Needs authentication`, `✘ Failed to connect`; project-scoped servers awaiting approval show `⏸ Pending approval`. This confirms availability-in-session (what `claude mcp list` reports) is orthogonal to ownership scope — a local- or user-scoped connection reports exactly the same "Connected" status as a project-owned one.

## Source 2 — Claude Code `code.claude.com/docs/en/sub-agents` (fetched directly, full page read across two pages of persisted output)

Frontmatter fields table (excerpt): `tools` — "Tools the subagent can use. Inherits every tool available to subagents if omitted... If no entry in the list resolves to a tool, the subagent usually fails to launch." `disallowedTools` — "Tools to deny, removed from inherited or specified list." `mcpServers` — "MCP servers available to this subagent. Each entry is either a server name referencing an already-configured server... or an inline definition... Ignored for plugin subagents."

"To keep an MCP server out of the main conversation entirely and avoid its tool descriptions consuming context there, define it inline here rather than in `.mcp.json`. The subagent gets the tools; the parent conversation doesn't." — direct confirmation that ownership can be scoped narrower than session-wide availability, in the opposite direction from the project/local-scope case (a tool can belong to a subagent and be *invisible* to the very session that spawned it).

"Subagents inherit the built-in tools and MCP tools available in the main conversation, narrowed by two filters..." — the baseline is session availability; ownership (the `tools`/`mcpServers` fields) narrows from there, never widens beyond what the session itself has connected (except for the inline-`mcpServers` case above, which is the documented exception).

`permissionMode` field: `default`/`acceptEdits`/`auto`/`dontAsk`/`bypassPermissions`/`plan` — a subagent-level permission layer, separate from and layered on top of tool ownership.

## Source 3 — Claude Code `code.claude.com/docs/en/permissions` (fetched directly)

"Rules are evaluated in order: deny, then ask, then allow. The first match in that order determines the outcome, and rule specificity doesn't change the order." (Already corroborates prior Capability 4 finding — this is the 6th independent implementation of the same precedence rule, now including Claude Code confirmed at the primary-doc level for the current version rather than a prior secondary reference.)

MCP-specific rule syntax: `mcp__puppeteer` (any tool from that server), `mcp__puppeteer__*` (wildcard, same effect), `mcp__puppeteer__puppeteer_navigate` (one named tool). Deny-only, unanchored wildcard `mcp__*` removes every MCP tool; allow rules require a literal, glob-free server segment.

Managed-settings keys, quoted: `allowedMcpServers`/`deniedMcpServers` ("`allowManagedMcpServersOnly`: When true, only `allowedMcpServers` from managed settings are respected. `deniedMcpServers` still merges from all sources"); `allowManagedPermissionRulesOnly` ("prevents user and project settings from defining allow/ask/deny rules... Doesn't affect the MCP server allowlist; for that, set `allowManagedMcpServersOnly`") — the doc itself explicitly separates the "which servers may connect at all" policy surface from the "which already-connected tools are allowed" policy surface, i.e. institutionally treats availability-gating and permission-gating as two different settings even at the managed/enterprise layer.

## Source 4 — Claude Code `code.claude.com/docs/en/skills` (fetched directly)

Frontmatter: `allowed-tools` — "Pre-approve tools for a skill... This skill lets Claude run git commands without per-use approval whenever you invoke it: `allowed-tools: Bash(git add *) Bash(git commit *) Bash(git status *)`." "This persistence applies to the skill's instructions, not its permissions: an `allowed-tools` grant clears when you send your next message." — a permission grant explicitly scoped to one task/invocation window, not the session.

`disable-model-invocation: true` / `user-invocable: false` table — controls *who* can invoke a skill (you vs. Claude), a distinct axis from tool ownership/permission, closer to a recommendation/routing control (does this capability surface itself as an option for the model to pick at all).

Description-based delegation: "Claude uses skill descriptions to decide when to use it" (implicit throughout the page; explicit parallel statement for subagents on the sub-agents page: "Claude uses each subagent's description to decide when to delegate tasks").

## Source 5 — MCP spec `modelcontextprotocol.io/specification/2025-06-18/server/tools` (fetched directly)

Tool annotations: "clients **MUST** consider tool annotations to be untrusted unless they come from trusted servers." Annotations (`readOnlyHint`, `destructiveHint`, etc.) are explicitly advisory metadata about tool behavior — the spec's own security section separately requires "Prompt for user confirmation on sensitive operations" as the actual control, keeping the hint (recommendation-shaped) and the confirmation gate (permission-shaped) as two different mechanisms in the same document.

## Source 6 — MCP spec `modelcontextprotocol.io/specification/2025-06-18/basic/authorization` (fetched directly)

OAuth 2.1-based flow: a 401 with `WWW-Authenticate` triggers Protected Resource Metadata discovery, then an authorization-server-issued, audience-bound access token (RFC 8707 `resource` parameter) before any `tools/call` succeeds. This is a genuinely separate permission layer at the protocol level, independent of whether `tools/list` already reported the tool as available — a server can list a tool via `tools/list` (schema is public) while every actual `tools/call` still requires a valid, audience-bound token. Notably, this spec-level authorization is explicitly scoped to HTTP-based transports only; **STDIO transports "SHOULD NOT" follow this spec and instead read credentials from the environment** — meaning for a large share of real local MCP setups (stdio servers, which is what `claude mcp add --transport stdio` produces), the permission layer is *not* MCP-protocol-level at all, it's whatever the local harness (Claude Code's own `settings.json` rules, above) provides. This is an honest, spec-stated limit on how far "the protocol itself" answers the permission question.

## Source 7 — LangChain `docs.langchain.com/oss/python/langchain/human-in-the-loop` (fetched directly, verbatim code returned)

```python
middleware=[
    HumanInTheLoopMiddleware(
        interrupt_on={
            "write_file": True,  # All decisions allowed
            "execute_sql": {"allowed_decisions": ["approve", "reject"]},
            "read_data": False,  # Auto-approve (no review)
        },
    ),
]
```
Quoted: "`interrupt_on`... Mapping of tool names to approval configs. Values can be `True` (interrupt with default config), `False` (auto-approve), or an `InterruptOnConfig` object." The agent's own `tools=[write_file, execute_sql, read_data]` list is the separate, prior ownership declaration — `interrupt_on` is confirmed as a second, independent configuration surface keyed by the same tool names.

No structured field for "recommended for this specific task" was found on this page or in the toolkit/`bind_tools()` reference material gathered via search — reported as an honest gap for this system, not assumed to exist by analogy to Claude Code.

## Source 8 — OpenAI Agents SDK `openai.github.io/openai-agents-python/tools/` and `/guardrails/` (fetched directly)

`Agent(tools=[fetch_weather, read_file])` — ownership declaration, same shape as LangChain's.

`allowed_callers` (tool-level field): "controls how a tool may be invoked. Omitting it allows direct model calls only." Values: `["programmatic"]`, `["direct", "programmatic"]`, omitted (direct-only default). Explicitly scoped to `FunctionTool`, `CustomTool`, `ShellTool`, `ApplyPatchTool`, `HostedMCPTool`, `CodeInterpreterTool`.

`Agent.as_tool(..., needs_approval=...)`: "If approval is required, the run pauses and pending items appear in `result.interruptions`; then use `result.to_state()` and resume after calling `state.approve(...)` or `state.reject(...)`." Confirmed as distinct from `allowed_callers`: "`allowed_callers` is about access method; approval is about gating execution."

Hosted tools (`WebSearchTool`, `FileSearchTool`, etc.) require the same explicit `tools=[...]` declaration as a user-defined function — no session-level "platform tool is connected but not yet claimed by an agent" state was found, unlike Claude Code's MCP-server-scope case above. This is the concrete basis for reporting "available vs. belongs does not separate cleanly" for this system.

Guardrails (input/output/tool) confirmed as a *third*, separate mechanism again: detection-and-block ("immediately raises an `InputGuardrailTripwireTriggered`...") rather than a pre-invocation allow/deny/ask gate — closer in spirit to a runtime validation layer than to either "belongs" or "permitted" as defined in this brief. Noted but not counted toward any of the four layers, to avoid stretching a fit.

## Source 9 — AWS `docs.aws.amazon.com/bedrock/latest/userguide/agents-permissions.html` and `agents-action-create.html` (fetched directly)

Note at top of `agents-action-create.html`: "Amazon Bedrock Agents (now Amazon Bedrock Agents Classic) is no longer open to new customers... Existing customers can continue to use the service as normal." — flagged plainly; real and checkable, but legacy.

Action group → agent ownership, via the Lambda resource-based policy's condition key, quoted from the JSON template: `"ArnLike": {"AWS:SourceArn": "arn:aws:bedrock:{{region}}:{{account}}:agent/{{agent-id}}"}` — the Lambda function itself is only invokable on behalf of the one named `agent-id`, not any Bedrock agent in the account. This is ownership enforced at the resource-policy level, not merely declared in a UI.

Separately, the agent's own identity-based service-role policy statements (`AgentModelInvocationPermissions`, `AgentActionGroupS3`, `AgentKnowledgeBaseQuery`, `ApplyGuardrail`, etc.) govern what the *agent's role* may call — a second, independently-configured IAM surface. Two-sided enforcement (identity-based on the caller + resource-based on the callee) is the concrete mechanism, not a single list.

## Source 10 — Salesforce Agentforce (fetch attempted, not credited)

`help.salesforce.com/s/articleView?id=sf.copilot_topics_actions.htm` returned a 404 page when fetched directly this session. `help.salesforce.com/s/articleView?id=ai.agent_user.htm` returned an unrenderable/loading-only page. A third page (`ai.copilot_actions.htm`) did load and gave a qualitative description of an org-wide action library vs. per-agent action assignment, but explicitly could not confirm the specific runtime permission mechanism ("the documentation excerpt does not explicitly detail whether execution permissions are enforced through permission sets... object/field-level security... sharing rules... or a combination"). Per `METHODOLOGY.md` Stage 2's explicit-report rule, this is logged as **not verified at mechanism level** — reported honestly rather than either counted as a third confirmed system or silently dropped from the record.

## Confidence summary

Confirmed (Claude Code `mcp`/`sub-agents`/`permissions`/`skills`, MCP spec `server/tools`/`basic/authorization`, LangChain `human-in-the-loop`, OpenAI Agents SDK `tools`/`guardrails` — all official docs, all fetched directly this session) · Established/Medium (AWS Bedrock Agents Classic — official docs fetched directly, but the product itself is legacy) · Unverified (Salesforce Agentforce — primary pages unreachable this session, not used as evidence for any claim).
