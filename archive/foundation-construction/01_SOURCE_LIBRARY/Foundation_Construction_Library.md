# FOUNDATION CONSTRUCTION LIBRARY

Прямое извлечение архитектурных блоков из первоисточников (не через посредника, не через отчёт Этапа 2). Каждый источник открыт и прочитан заново в рамках этого прохода — либо через прямой `curl` на сырой markdown/HTML (когда доступен), либо через ar5iv для arXiv-статей, либо через WebFetch там, где сайт требует JS-рендеринга (отмечено отдельно).

Формат блока: `Источник · Раздел · Тип блока · Foundation Section` + дословный фрагмент ниже. Foundation Section — механическая метка папки будущего дома (`memory` / `instructions` / `workspace` / `knowledge` / `profile` / `skills` / `routing` / `update` / `communication`), без обоснования, без анализа.

Без объединения повторов: один и тот же принцип, встреченный в нескольких источниках, зафиксирован отдельно от каждого.

---

## ИСТОЧНИК: Anthropic — Building Effective Agents

Способ получения: прямой `curl` на www.anthropic.com/research/building-effective-agents.

**Блок №001** — `Источник: Anthropic` · `Раздел: Building block — The augmented LLM` · `Тип блока: Agent Definition` · `Foundation Section: instructions`
```
The basic building block of agentic systems is an LLM enhanced with augmentations such as retrieval, tools, and memory. Our current models can actively use these capabilities—generating their own search queries, selecting appropriate tools, and determining what information to retain.
```

**Блок №002** — `Источник: Anthropic` · `Раздел: Workflows vs Agents` · `Тип блока: Architecture Pattern` · `Foundation Section: routing`
```
Workflows are systems where LLMs and tools are orchestrated through predefined code paths. Agents, on the other hand, are systems where LLMs dynamically direct their own processes and tool usage, maintaining control over how they accomplish tasks.
```

**Блок №003** — `Источник: Anthropic` · `Раздел: Workflow — Prompt chaining` · `Тип блока: Orchestration Pattern` · `Foundation Section: routing`
```
Prompt chaining decomposes a task into a sequence of steps, where each LLM call processes the output of the previous one. You can add programmatic checks (see "gate" in the diagram below) on any intermediate steps to ensure that the process is still on track.
```

**Блок №004** — `Источник: Anthropic` · `Раздел: Workflow — Routing` · `Тип блока: Orchestration Pattern` · `Foundation Section: routing`
```
Routing classifies an input and directs it to a specialized followup task. This workflow allows for separation of concerns, and building more specialized prompts. Without this workflow, optimizing for one kind of input can hurt performance on other inputs.
```

**Блок №005** — `Источник: Anthropic` · `Раздел: Workflow — Parallelization` · `Тип блока: Orchestration Pattern` · `Foundation Section: routing`
```
LLMs can sometimes work simultaneously on a task and have their outputs aggregated programmatically. This workflow, parallelization, manifests in two key variations: Sectioning: Breaking a task into independent subtasks run in parallel. Voting: Running the same task multiple times to get diverse outputs.
```

**Блок №006** — `Источник: Anthropic` · `Раздел: Workflow — Orchestrator-workers` · `Тип блока: Orchestration Pattern` · `Foundation Section: routing`
```
In the orchestrator-workers workflow, a central LLM dynamically breaks down tasks, delegates them to worker LLMs, and synthesizes their results. ... the key difference from parallelization is its flexibility—subtasks aren't pre-defined, but determined by the orchestrator based on the specific input.
```

**Блок №007** — `Источник: Anthropic` · `Раздел: Workflow — Evaluator-optimizer` · `Тип блока: Orchestration Pattern` · `Foundation Section: routing`
```
In the evaluator-optimizer workflow, one LLM call generates a response while another provides evaluation and feedback in a loop. This workflow is particularly effective when we have clear evaluation criteria, and when iterative refinement provides measurable value.
```

**Блок №008** — `Источник: Anthropic` · `Раздел: When and how to use frameworks` · `Тип блока: Design Principle` · `Foundation Section: instructions`
```
When building applications with LLMs, we recommend finding the simplest solution possible, and only increasing complexity when needed. This might mean not building agentic systems at all.
```

**Блок №009** — `Источник: Anthropic` · `Раздел: Summary` · `Тип блока: Design Principle` · `Foundation Section: instructions`
```
Success in the LLM space isn't about building the most sophisticated system. It's about building the right system for your needs. Start with simple prompts, optimize them with comprehensive evaluation, and add multi-step agentic systems only when simpler solutions fall short. When implementing agents, we try to follow three core principles: Maintain simplicity in your agent's design. Prioritize transparency by explicitly showing the agent's planning steps. Carefully craft your agent-computer interface (ACI) through thorough tool documentation and testing.
```

---

## ИСТОЧНИК: humanlayer/12-factor-agents (GitHub README, дословно)

Способ получения: прямой `curl` на raw.githubusercontent.com/humanlayer/12-factor-agents/main/README.md и файлы content/factor-*.md.

**Блок №010** — `Источник: 12-Factor Agents` · `Раздел: The 12 Factors (список названий)` · `Тип блока: Principles List` · `Foundation Section: instructions`
```
Factor 1: Natural Language to Tool Calls
Factor 2: Own your prompts
Factor 3: Own your context window
Factor 4: Tools are just structured outputs
Factor 5: Unify execution state and business state
Factor 6: Launch/Pause/Resume with simple APIs
Factor 7: Contact humans with tool calls
Factor 8: Own your control flow
Factor 9: Compact Errors into Context Window
Factor 10: Small, Focused Agents
Factor 11: Trigger from anywhere, meet users where they are
Factor 12: Make your agent a stateless reducer
```

**Блок №011** — `Источник: 12-Factor Agents` · `Раздел: Agents as loops` · `Тип блока: Control Flow Pattern` · `Foundation Section: routing`
```
1. LLM determines the next step in the workflow, outputting structured json ("tool calling")
2. Deterministic code executes the tool call
3. The result is appended to the context window
4. Repeat until the next step is determined to be "done"
```
```python
initial_event = {"message": "..."}
context = [initial_event]
while True:
  next_step = await llm.determine_next_step(context)
  context.append(next_step)
  if (next_step.intent === "done"):
    return next_step.final_answer
  result = await execute_step(next_step)
  context.append(result)
```

**Блок №012** — `Источник: 12-Factor Agents` · `Раздел: Factor 3 — Own your context window` · `Тип блока: Context Management` · `Foundation Section: memory`
```
At any given point, your input to an LLM in an agent is "here's what's happened so far, what's the next step". Everything is context engineering. LLMs are stateless functions that turn inputs into outputs. To get the best outputs, you need to give them the best inputs. Creating great context means: The prompt and instructions you give to the model; Any documents or external data you retrieve (e.g. RAG); Any past state, tool calls, results, or other history; Any past messages or events from related but separate histories/conversations (Memory); Instructions about what sorts of structured data to output.
```

**Блок №013** — `Источник: 12-Factor Agents` · `Раздел: Factor 5 — Unify execution state and business state` · `Тип блока: State Model` · `Foundation Section: memory`
```
Execution state: current step, next step, waiting status, retry counts, etc. Business state: What's happened in the agent workflow so far (e.g. list of OpenAI messages, list of tool calls and results, etc.) If possible, SIMPLIFY - unify these as much as possible. ... This approach has several benefits: 1. Simplicity: One source of truth for all state 2. Serialization: The thread is trivially serializable/deserializable 3. Debugging: The entire history is visible in one place 4. Flexibility: Easy to add new state by just adding new event types 5. Recovery: Can resume from any point by just loading the thread 6. Forking: Can fork the thread at any point by copying some subset of the thread into a new context / state ID 7. Human Interfaces and Observability: Trivial to convert a thread into a human-readable markdown or a rich Web app UI
```

**Блок №014** — `Источник: 12-Factor Agents` · `Раздел: Factor 8 — Own your control flow` · `Тип блока: Control Flow Pattern` · `Foundation Section: routing`
```
Build your own control structures that make sense for your specific use case. Specifically, certain types of tool calls may be reason to break out of the loop and wait for a response from a human or another long-running task like a training pipeline. You may also want to incorporate custom implementation of: summarization or caching of tool call results; LLM-as-judge on structured output; context window compaction or other memory management; logging, tracing, and metrics; client-side rate limiting; durable sleep / pause / "wait for event"
```

**Блок №015** — `Источник: 12-Factor Agents` · `Раздел: Factor 10 — Small, Focused Agents` · `Тип блока: Design Principle` · `Foundation Section: instructions`
```
Rather than building monolithic agents that try to do everything, build small, focused agents that do one thing well. Agents are just one building block in a larger, mostly deterministic system. The key insight here is about LLM limitations: the bigger and more complex a task is, the more steps it will take, which means a longer context window. As context grows, LLMs are more likely to get lost or lose focus. By keeping agents focused on specific domains with 3-10, maybe 20 steps max, we keep context windows manageable and LLM performance high.
```

---

## ИСТОЧНИК: AGENTS.md (agents.md, официальный сайт стандарта)

Способ получения: прямой `curl` на agents.md.

**Блок №016** — `Источник: AGENTS.md` · `Раздел: Why AGENTS.md?` · `Тип блока: Agent Manifest` · `Foundation Section: instructions`
```
README.md files are for humans: quick starts, project descriptions, and contribution guidelines. AGENTS.md complements this by containing the extra, sometimes detailed context coding agents need: build steps, tests, and conventions that might clutter a README or aren't relevant to human contributors. We intentionally kept it separate to: Give agents a clear, predictable place for instructions. Keep READMEs concise and focused on human contributors. Provide precise, agent-focused guidance that complements existing README and docs.
```

**Блок №017** — `Источник: AGENTS.md` · `Раздел: FAQ — Are there required fields?` · `Тип блока: Agent Manifest` · `Foundation Section: instructions`
```
No. AGENTS.md is just standard Markdown. Use any headings you like; the agent simply parses the text you provide.
```

**Блок №018** — `Источник: AGENTS.md` · `Раздел: FAQ — What if instructions conflict?` · `Тип блока: Routing Rule` · `Foundation Section: routing`
```
The closest AGENTS.md to the edited file wins; explicit user chat prompts override everything.
```

**Блок №019** — `Источник: AGENTS.md` · `Раздел: How to use AGENTS.md — nested files` · `Тип блока: Routing Rule` · `Foundation Section: routing`
```
Large monorepo? Use nested AGENTS.md files for subprojects. Place another AGENTS.md inside each package. Agents automatically read the nearest file in the directory tree, so the closest one takes precedence and every subproject can ship tailored instructions. For example, at time of writing the main OpenAI repo has 88 AGENTS.md files.
```

**Блок №020** — `Источник: AGENTS.md` · `Раздел: FAQ — Can I update it later?` · `Тип блока: Update Rule` · `Foundation Section: update`
```
Absolutely. Treat AGENTS.md as living documentation.
```

**Блок №021** — `Источник: AGENTS.md` · `Раздел: About` · `Тип блока: Governance` · `Foundation Section: update`
```
AGENTS.md is now stewarded by the Agentic AI Foundation under the Linux Foundation.
```

---

## ИСТОЧНИК: OpenAI Agents SDK (openai.github.io/openai-agents-python)

Способ получения: прямой `curl` (статический MkDocs-сайт).

**Блок №022** — `Источник: OpenAI Agents SDK` · `Раздел: Intro — primitives` · `Тип блока: Agent Definition` · `Foundation Section: instructions`
```
The OpenAI Agents SDK enables you to build agentic AI apps in a lightweight, easy-to-use package with very few abstractions. It's a production-ready upgrade of our previous experimentation for agents, Swarm. The Agents SDK has a very small set of primitives: Agents, which are LLMs equipped with instructions and tools; Agents as tools / Handoffs, which allow agents to delegate to other agents for specific tasks; Guardrails, which enable validation of agent inputs and outputs.
```

**Блок №023** — `Источник: OpenAI Agents SDK` · `Раздел: Why use the Agents SDK` · `Тип блока: Design Principle` · `Foundation Section: instructions`
```
The SDK has two driving design principles: Enough features to be worth using, but few enough primitives to make it quick to learn. Works great out of the box, but you can customize exactly what happens.
```

**Блок №024** — `Источник: OpenAI Agents SDK` · `Раздел: Main features list` · `Тип блока: Capability Inventory` · `Foundation Section: skills`
```
Sandbox agents: Run specialists inside real isolated workspaces with manifest-defined files, sandbox client choice, and resumable sandbox sessions. ... Function tools: Turn any Python function into a tool with automatic schema generation and Pydantic-powered validation. MCP server tool calling: Built-in MCP server tool integration that works the same way as function tools. Sessions: A persistent memory layer for maintaining working context within an agent loop. Human in the loop: Built-in mechanisms for involving humans across agent runs.
```

**Блок №025** — `Источник: OpenAI Agents SDK` · `Раздел: Start here — decision table` · `Тип блока: Design Principle` · `Foundation Section: routing`
```
Build your first text-based agent with the Quickstart. Then decide how you want to carry state across turns in Running agents. If the task depends on real files, repos, or isolated per-agent workspace state, read the Sandbox agents quickstart. If you are deciding between handoffs and manager-style orchestration, read Agent orchestration.
```

**Блок №026** — `Источник: OpenAI Agents SDK` · `Раздел: Sessions — Overview` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
The Agents SDK provides built-in session memory to automatically maintain conversation history across multiple agent runs, eliminating the need to manually handle .to_input_list() between turns. Sessions stores conversation history for a specific session, allowing agents to maintain context without requiring explicit manual memory management.
```

**Блок №027** — `Источник: OpenAI Agents SDK` · `Раздел: Sessions — Core session behavior` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
When session memory is enabled: Before each run: The runner automatically retrieves the conversation history for the session and prepends it to the input items. After each run: All new items generated during the run (user input, assistant responses, tool calls, etc.) are automatically stored in the session. Context preservation: Each subsequent run with the same session includes the full conversation history, allowing the agent to maintain context.
```

**Блок №028** — `Источник: OpenAI Agents SDK` · `Раздел: Sessions — Memory operations` · `Тип блока: Memory Model` · `Foundation Section: memory`
```python
from agents import SQLiteSession
session = SQLiteSession("user_123", "conversations.db")
# Get all items in a session
items = await session.get_items()
# Add new items to a session
new_items = [
    {"role": "user", "content": "Hello"},
    {"role": "assistant", "content": "Hi there!"}
]
await session.add_items(new_items)
# Remove and return the most recent item
last_item = await session.pop_item()
# Clear all items from a session
await session.clear_session()
```

**Блок №029** — `Источник: OpenAI Agents SDK` · `Раздел: Sessions — Limiting retrieved history` · `Тип блока: Context Management` · `Foundation Section: memory`
```
Use SessionSettings to control how much history is fetched before each run. SessionSettings(limit=None) (default): retrieve all available session items. SessionSettings(limit=N): retrieve only the most recent N items.
```

---

## ИСТОЧНИК: Anthropic — Claude Agent SDK (code.claude.com/docs)

Способ получения: прямой `curl` на markdown-экспорт документации (`.md`-суффикс).

**Блок №030** — `Источник: Claude Agent SDK` · `Раздел: Subagents — Overview` · `Тип блока: Agent Definition` · `Foundation Section: skills`
```
Subagents are separate agent instances that your main agent can spawn to handle focused subtasks. Use them to isolate context, run multiple analyses in parallel, and apply specialized instructions without adding to the main agent's prompt. You can create subagents in three ways: Programmatically: use the agents parameter in your query() options. Filesystem-based: define agents as markdown files in .claude/agents/ directories. Built-in general-purpose: Claude can invoke the built-in general-purpose subagent at any time via the Agent tool without you defining anything.
```

**Блок №031** — `Источник: Claude Agent SDK` · `Раздел: Subagents — Automatic invocation` · `Тип блока: Routing Rule` · `Foundation Section: routing`
```
When you define subagents, Claude determines whether to invoke them based on each subagent's description field. Write clear descriptions that explain when to use the subagent, and Claude automatically delegates appropriate tasks. You can also explicitly request a subagent by name in your prompt, for example "Use the code-reviewer agent to...".
```

**Блок №032** — `Источник: Claude Agent SDK` · `Раздел: Subagents — Context isolation` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
Each subagent runs in its own fresh conversation. Intermediate tool calls and results stay inside the subagent; only its final message returns to the parent. Example: a research-assistant subagent can explore dozens of files without any of that content accumulating in the main conversation. The parent receives a concise summary, not every file the subagent read.
```

**Блок №033** — `Источник: Claude Agent SDK` · `Раздел: Skills — SKILL.md инвокация` · `Тип блока: Capability Attachment` · `Foundation Section: skills`
```
Skills must be created as filesystem artifacts... The SDK does not provide a programmatic API for registering Skills
```

**Блок №034** — `Источник: Claude Agent SDK` · `Раздел: Sub-agents (файловые) — что происходит при отсутствии автосрабатывания` · `Тип блока: Fallback Rule` · `Foundation Section: routing`
```
the `/agents` command no longer opens the interactive creation wizard; running it prints a reminder to ask Claude or edit `.claude/agents/` directly.
```

**Блок №035** — `Источник: Claude Agent SDK` · `Раздел: How permissions are evaluated` · `Тип блока: Permission Model` · `Foundation Section: instructions`
```
When Claude requests a tool, the SDK checks permissions in this order: Hooks — Run hooks first. A hook can deny the call outright or pass it on. Deny rules — Check deny rules (from disallowed_tools and settings.json). If a deny rule matches, the tool is blocked, even in bypassPermissions mode. Bare-name deny rules like Bash remove the tool from Claude's context before this evaluation begins, so only scoped rules like Bash(rm *) are checked at this step. Ask rules — Check ask rules from settings.json. If an ask rule matches, the call falls through to your canUseTool callback for confirmation, even in bypassPermissions mode. Permission mode — Apply the active permission mode. Allow rules — Check allow rules (from allowed_tools and settings.json). If a rule matches, the tool is approved. canUseTool callback — If not resolved by any of the above, call your canUseTool callback for a decision.
```

**Блок №036** — `Источник: Claude Agent SDK` · `Раздел: Sessions — сессия и возобновление` · `Тип блока: Memory Model` · `Foundation Section: memory`
(файл получен: `code.claude.com/docs/en/agent-sdk/sessions.md`, 403 строки — управление сессиями, возобновление и форк; конкретные цитаты будут добавлены отдельным блоком при углублении в этот файл)

---

## ИСТОЧНИК: Model Context Protocol (спецификация, modelcontextprotocol.io / GitHub raw)

Способ получения: прямой `curl` на raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol (спецификация версии 2025-06-18).

**Блок №037** — `Источник: MCP` · `Раздел: Architecture — Core Components` · `Тип блока: Communication Protocol` · `Foundation Section: communication`
```
The Model Context Protocol (MCP) follows a client-host-server architecture where each host can run multiple client instances. This architecture enables users to integrate AI capabilities across applications while maintaining clear security boundaries and isolating concerns. Built on JSON-RPC, MCP provides a stateful session protocol focused on context exchange and sampling coordination between clients and servers.
```

**Блок №038** — `Источник: MCP` · `Раздел: Architecture — Host` · `Тип блока: Communication Protocol` · `Foundation Section: communication`
```
The host process acts as the container and coordinator: Creates and manages multiple client instances; Controls client connection permissions and lifecycle; Enforces security policies and consent requirements; Handles user authorization decisions; Coordinates AI/LLM integration and sampling; Manages context aggregation across clients.
```

**Блок №039** — `Источник: MCP` · `Раздел: Lifecycle — три фазы` · `Тип блока: Lifecycle Model` · `Foundation Section: update`
```
The Model Context Protocol (MCP) defines a rigorous lifecycle for client-server connections that ensures proper capability negotiation and state management. 1. Initialization: Capability negotiation and protocol version agreement. 2. Operation: Normal protocol communication. 3. Shutdown: Graceful termination of the connection.
```

**Блок №040** — `Источник: MCP` · `Раздел: Lifecycle — Initialization` · `Тип блока: Lifecycle Model` · `Foundation Section: update`
```
The initialization phase MUST be the first interaction between client and server. During this phase, the client and server: Establish protocol version compatibility; Exchange and negotiate capabilities; Share implementation details. The client MUST initiate this phase by sending an initialize request containing: Protocol version supported; Client capabilities; Client implementation information.
```

**Блок №041** — `Источник: MCP` · `Раздел: Lifecycle — Capability Negotiation` · `Тип блока: Capability Attachment` · `Foundation Section: skills`
```
Client and server capabilities establish which optional protocol features will be available during the session. Key capabilities include: Client: roots — Ability to provide filesystem roots; Client: sampling — Support for LLM sampling requests; Client: elicitation — Support for server elicitation requests; Server: prompts — Offers prompt templates; Server: resources — Provides readable resources; Server: tools — Exposes callable tools; Server: logging — Emits structured log messages.
```

**Блок №042** — `Источник: MCP` · `Раздел: Server features — Tools, User Interaction Model` · `Тип блока: Capability Attachment` · `Foundation Section: skills`
```
The Model Context Protocol (MCP) allows servers to expose tools that can be invoked by language models. Tools enable models to interact with external systems, such as querying databases, calling APIs, or performing computations. Each tool is uniquely identified by a name and includes metadata describing its schema. Tools in MCP are designed to be model-controlled, meaning that the language model can discover and invoke tools automatically based on its contextual understanding and the user's prompts.
```

**Блок №043** — `Источник: MCP` · `Раздел: Server features — Resources, User Interaction Model` · `Тип блока: Knowledge Attachment` · `Foundation Section: knowledge`
```
The Model Context Protocol (MCP) provides a standardized way for servers to expose resources to clients. Resources allow servers to share data that provides context to language models, such as files, database schemas, or application-specific information. Each resource is uniquely identified by a URI. Resources in MCP are designed to be application-driven, with host applications determining how to incorporate context based on their needs.
```

**Блок №044** — `Источник: MCP` · `Раздел: Server features — Prompts, User Interaction Model` · `Тип блока: Capability Attachment` · `Foundation Section: skills`
```
The Model Context Protocol (MCP) provides a standardized way for servers to expose prompt templates to clients. Prompts allow servers to provide structured messages and instructions for interacting with language models. Clients can discover available prompts, retrieve their contents, and provide arguments to customize them. Prompts are designed to be user-controlled, meaning they are exposed from servers to clients with the intention of the user being able to explicitly select them for use.
```

---

## ИСТОЧНИК: Agent2Agent Protocol Specification (a2a-protocol.org)

Способ получения: прямой `curl` (статическая часть спецификации, 4089 строк).

**Блок №045** — `Источник: A2A` · `Раздел: 1. Introduction` · `Тип блока: Communication Protocol` · `Foundation Section: communication`
```
The Agent2Agent (A2A) Protocol is an open standard designed to facilitate communication and interoperability between independent, potentially opaque AI agent systems. In an ecosystem where agents might be built using different frameworks, languages, or by different vendors, A2A provides a common language and interaction model. Its primary goal is to enable agents to: Discover each other's capabilities. Negotiate interaction modalities (text, files, structured data). Manage collaborative tasks. Securely exchange information to achieve user goals without needing access to each other's internal state, memory, or tools.
```

**Блок №046** — `Источник: A2A` · `Раздел: 1.2. Guiding Principles` · `Тип блока: Design Principle` · `Foundation Section: communication`
```
Simple: Reuse existing, well-understood standards (HTTP, JSON-RPC 2.0, Server-Sent Events). Enterprise Ready: Address authentication, authorization, security, privacy, tracing, and monitoring by aligning with established enterprise practices. Async First: Designed for (potentially very) long-running tasks and human-in-the-loop interactions. Modality Agnostic: Support exchange of diverse content types including text, audio/video (via file references), structured data/forms, and potentially embedded UI components. Opaque Execution: Agents collaborate based on declared capabilities and exchanged information, without needing to share their internal thoughts, plans, or tool implementations.
```

**Блок №047** — `Источник: A2A` · `Раздел: 1.3. Specification Structure — три слоя` · `Тип блока: Protocol Layering` · `Foundation Section: communication`
```
This specification is organized into three distinct layers that work together to provide a complete protocol definition: A2A Data Model (Task, Message, AgentCard, Part, Artifact, Extension) → A2A Operations (Send Message, Send Streaming Message, Get Task, List Tasks, Cancel Task, Get Agent Card) → Protocol Bindings (JSON-RPC Methods, gRPC RPCs, HTTP/REST Endpoints, Custom Bindings).
```

**Блок №048** — `Источник: A2A` · `Раздел: 4.1.3. TaskState — состояния жизненного цикла задачи` · `Тип блока: Lifecycle Model` · `Foundation Section: update`
```
TASK_STATE_UNSPECIFIED — The task is in an unknown or indeterminate state. TASK_STATE_SUBMITTED — Indicates that a task has been successfully submitted and acknowledged. TASK_STATE_WORKING — Indicates that a task is actively being processed by the agent. TASK_STATE_COMPLETED — Indicates that a task has finished successfully. This is a terminal state. TASK_STATE_FAILED — Indicates that a task has finished with an error. This is a terminal state. TASK_STATE_CANCELED — Indicates that a task was canceled before completion. This is a terminal state. TASK_STATE_INPUT_REQUIRED — Indicates that the agent requires additional user input to proceed. This is an interrupted state. TASK_STATE_REJECTED — Indicates that the agent has decided to not perform the task. This is a terminal state. TASK_STATE_AUTH_REQUIRED — Indicates that authentication is required to proceed. This is an interrupted state.
```

**Блок №049** — `Источник: A2A` · `Раздел: 4.1.4. Message` · `Тип блока: Communication Protocol` · `Foundation Section: communication`
```
Message is one unit of communication between client and server. It can be associated with a context and/or a task. For server messages, context_id must be provided, and task_id only if a task was created. For client messages, both fields are optional, with the caveat that if both are provided, they have to match (the context_id has to be the one that is set on the task). If only task_id is provided, the server will infer context_id from it.
```

---

## ИСТОЧНИК: LangGraph (docs.langchain.com)

Способ получения: прямой `curl` на markdown-экспорт (`.md`-суффикс).

**Блок №050** — `Источник: LangGraph` · `Раздел: Overview — назначение` · `Тип блока: Architecture Layering` · `Foundation Section: instructions`
```
LangGraph is a low-level orchestration framework and runtime for building, managing, and deploying long-running, stateful agents. LangGraph gives you fine-grained control to mix deterministic, hand-coded steps with LLM-driven agentic steps in the same graph, so you can build bespoke agents that behave exactly the way your application requires. LangGraph is very low-level, and focused entirely on agent orchestration.
```

**Блок №051** — `Источник: LangGraph` · `Раздел: Overview — как продукты LangChain соотносятся друг с другом` · `Тип блока: Architecture Layering` · `Foundation Section: instructions`
```
Deep Agents is an agent harness: planning, subagents, filesystem tools, and context management on top of LangGraph. LangChain is the agent framework: abstractions and integrations for models, tools, and agent loops. LangGraph is the orchestration runtime: durable execution, streaming, human-in-the-loop, and persistence. LangSmith is the platform for tracing, evaluation, prompts, and deployment across frameworks.
```

**Блок №052** — `Источник: LangGraph` · `Раздел: Persistence — два дополняющих слоя` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
LangGraph provides two complementary persistence systems: Checkpointers persist a thread's graph state as checkpoints. Use them for short-term, thread-scoped memory, including conversation continuity, human-in-the-loop workflows, time travel, and fault tolerance. Stores persist application-defined data outside the graph state. Use them for long-term, cross-thread memory, including user preferences, facts, and shared knowledge. Most applications can use both: a checkpointer tracks the current thread, and a store tracks durable information across threads.
```

**Блок №053** — `Источник: LangGraph` · `Раздел: Persistence — Checkpointer vs. store (таблица)` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
|                | Checkpointer                                                                 | Store                                               |
| -------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------- |
| Persists       | Graph state snapshots                                                        | Application-defined key-value data                  |
| Scope          | A single thread                                                              | Across threads                                      |
| Memory type    | Short-term, thread-scoped memory                                             | Long-term, cross-thread memory                      |
| Use for        | Conversation continuity, human-in-the-loop, time travel, and fault tolerance | User preferences, facts, and shared knowledge        |
| Access pattern | Pass a thread_id in graph config                                             | Read and write items from nodes or application code |
```

**Блок №054** — `Источник: LangGraph` · `Раздел: Persistence — Quickstart, разворачивание одной командой` · `Тип блока: Memory Model` · `Foundation Section: memory`
```python
from langgraph.checkpoint.memory import InMemorySaver
from langgraph.store.memory import InMemoryStore

checkpointer = InMemorySaver()
store = InMemoryStore()

graph = builder.compile(checkpointer=checkpointer, store=store)

result = graph.invoke(
    {"messages": [{"role": "user", "content": "Hi, my name is Bob."}]},
    {"configurable": {"thread_id": "thread-1"}},
)
```

**Блок №055** — `Источник: LangGraph` · `Раздел: Graph API — правило маршрутизации по узлам` · `Тип блока: Routing Rule` · `Foundation Section: routing`
```
For each node, choose one routing mechanism: use normal edges for static routing, or use conditional edges/Command for dynamic routing. Do not mix... because both paths can execute and make graph behavior harder to reason about.
```

---

## ИСТОЧНИК: CrewAI (docs.crewai.com)

Способ получения: прямой `curl -L` на markdown-экспорт (сайт редиректит на версионированный путь).

**Блок №056** — `Источник: CrewAI` · `Раздел: Memory — Overview` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
CrewAI provides a unified memory system -- a single Memory class that replaces separate short-term, long-term, entity, and external memory types with one intelligent API. Memory uses an LLM to analyze content when saving (inferring scope, categories, and importance) and supports adaptive-depth recall with composite scoring that blends semantic similarity, recency, and importance. You can use memory four ways: standalone (scripts, notebooks), with Crews, with Agents, or inside Flows.
```

**Блок №057** — `Источник: CrewAI` · `Раздел: Memory — Quick Start` · `Тип блока: Memory Model` · `Foundation Section: memory`
```python
from crewai import Memory

memory = Memory()

# Store -- the LLM infers scope, categories, and importance
memory.remember("We decided to use PostgreSQL for the user database.")

# Retrieve -- results ranked by composite score (semantic + recency + importance)
matches = memory.recall("What database did we choose?")
for m in matches:
    print(f"[{m.score:.2f}] {m.record.content}")

# Tune scoring for a fast-moving project
memory = Memory(recency_weight=0.5, recency_half_life_days=7)

# Forget
memory.forget(scope="/project/old")

# Explore the self-organized scope tree
print(memory.tree())
print(memory.info("/"))
```

**Блок №058** — `Источник: CrewAI` · `Раздел: CLI — Create crew (шаблон по умолчанию сменился на JSON)` · `Тип блока: Scaffolding` · `Foundation Section: skills`
```
By default, `crewai create crew` creates a JSON-first crew project with `crew.jsonc` and `agents/*.jsonc`. Use `crewai create crew my_new_crew --classic` only when you want the older Python/YAML scaffold with `crew.py`, `config/agents.yaml`, and `config/tasks.yaml`.
```

**Блок №059** — `Источник: CrewAI` · `Раздел: CLI — Create skill` · `Тип блока: Scaffolding` · `Foundation Section: skills`
```
Scaffold an agent skill. Inside a crew project (where pyproject.toml exists), the skill is created under ./skills/: `crewai create skill my-skill` / `crewai create skill my-skill --no-project`. Use --no-project to create the skill in the current directory instead of ./skills/.
```

**Блок №060** — `Источник: CrewAI` · `Раздел: Crafting Effective Agents — 80/20 Rule` · `Тип блока: Design Principle` · `Foundation Section: instructions`
```
80/20 Rule: 80% of your effort should go into designing tasks, and only 20% into defining agents.
```

---

## ИСТОЧНИК: AG2 (docs.ag2.ai, форк AutoGen)

Способ получения: прямой `curl` (MkDocs Material сайт, HTML очищен от тегов).

**Блок №061** — `Источник: AG2` · `Раздел: Overview — Why did we create AG2?` · `Тип блока: Design Principle` · `Foundation Section: update`
```
The original AutoGen project released with its first public preview in September 2023, and AG2 later diverged from that codebase in November 2024 to continue building on its core ideas. ... We have increasingly found that the original architecture inherited from AutoGen challenged the adoption of new ideas. Shipping modern capabilities inside the original design often requires introducing complexity, unnecessary migration effort, or compatibility compromises. ... Today's AG2 is our way to move forward with a future-focused foundation, applying the lessons we learned from building and operating hundreds of agent systems on the original framework.
```

**Блок №062** — `Источник: AG2` · `Раздел: Overview — What is AG2?` · `Тип блока: Agent Definition` · `Foundation Section: instructions`
```
AG2 is a protocol-driven, async agent framework built around a small, predictable core and a set of opt-in primitives. It rebuilds the framework around capabilities that were difficult or impractical to introduce on the original architecture. It is the foundation for AG2 agent development and production-ready multi-agent systems going forward, and forms the basis of AG2 v1.0.
```

**Блок №063** — `Источник: AG2` · `Раздел: Overview — A composable harness` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
AG2's harness layers on powerful primitives to the base Agent — assembly policies for context shaping, a knowledge store for persistent memory, sub-task delegation with isolated streams, and middleware for retries, logging, token limits, and history management. Build up the agent you need with the harness doing the heavy lifting for you.
```

**Блок №064** — `Источник: AG2` · `Раздел: Overview — State externalisation` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
State is externalised behind protocols — History, Storage, and Stream can be backed by Redis, a database, or anything you build — so agents stay effectively stateless and horizontal scaling is straightforward. Cross-cutting concerns like retries, rate limits, token budgets, and history compaction are middleware you compose onto an Agent.
```

**Блок №065** — `Источник: AG2` · `Раздел: Overview — Tools, toolkits, and built-in tools` · `Тип блока: Capability Attachment` · `Foundation Section: skills`
```
Define tools with a @tool decorator on plain functions. Use type hints, dependency injection (Context, Inject, Variable), and toolkits to organize related capabilities. Wire in built-in tools (web search, code execution, shell, memory) or expose any agent as a tool with Agent.as_tool(...).
```

**Блок №066** — `Источник: AG2` · `Раздел: Overview — Current Focus Areas` · `Тип блока: Roadmap` · `Foundation Section: update`
```
AG2 is actively focused on: improving the single-agent developer experience; providing stronger context and memory management primitives; simplifying integration with real applications, including Text UI, web, ambient, and background runtimes; enabling new multi-agent coordination patterns that are not feasible in the current AG2 architecture; supporting emerging standards and protocols across the AI agent ecosystem.
```

---

## ИСТОЧНИК: Semantic Kernel (learn.microsoft.com)

Способ получения: прямой `curl` (HTML очищен от тегов).

**Блок №067** — `Источник: Semantic Kernel` · `Раздел: Plugins — отличие от tools у других SDK` · `Тип блока: Capability Attachment` · `Foundation Section: skills`
```
Not all AI SDKs have an analogous concept to plugins (most just have functions or tools). In enterprise scenarios, however, plugins are valuable because they encapsulate a set of functionality that mirrors how enterprise developers already develop services and APIs. Plugins also play nicely with dependency injection. Within a plugin's constructor, you can inject services that are necessary to perform the work of the plugin (e.g., database connections, HTTP clients, etc.). This is difficult to accomplish with other SDKs that lack plugins.
```

**Блок №068** — `Источник: Semantic Kernel` · `Раздел: Agent Architecture — AgentThread` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
AgentThread class serves as the core abstraction for threads or conversation state. It abstracts away the different ways in which conversation state may be managed for different agents.
```

---

## ИСТОЧНИК: MemGPT — Towards LLMs as Operating Systems (Packer et al., arXiv 2310.08560)

Способ получения: полный текст статьи через ar5iv.labs.arxiv.org (HTML-рендеринг arXiv), HTML очищен от тегов.

**Блок №069** — `Источник: MemGPT` · `Раздел: Main context` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
main context, consist of the system instructions, working context, and a FIFO queue.
```

**Блок №070** — `Источник: MemGPT` · `Раздел: Virtual context management — метафора виртуальной памяти ОС` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
virtual context management, a technique drawing inspiration from hierarchical memory systems in traditional operating systems which provide the illusion of an extended virtual memory via paging between physical memory and disk.
```

**Блок №071** — `Источник: MemGPT` · `Раздел: FIFO Queue и system instructions` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
The system instructions are read-only (static) and contain information on the MemGPT control flow, the intended usage of the different memory levels, and instructions on how to use the MemGPT functions (e.g. how to retrieve out-of-context data). Working context is a fixed-size read/write block of unstructured text, writeable only via MemGPT function calls.
```

---

## ИСТОЧНИК: Letta (docs.letta.com, www.letta.com/constitution)

Способ получения: раздел Context Hierarchy — прямой `curl` на markdown-экспорт (docs.letta.com). Раздел Constitution — WebFetch (сайт не отдаёт статичный HTML/markdown напрямую через curl; текст возвращён с явным требованием дословности, оформлен как прямые цитаты в кавычках).

**Блок №072** — `Источник: Letta` · `Раздел: Context hierarchy — четыре уровня` · `Тип блока: Memory Model` · `Foundation Section: memory`
(файл получен: `docs.letta.com/guides/core-concepts/memory/context-hierarchy.md`, 160 строк — описывает Memory Blocks (in-context, редактируемые), Files (read-only, открываются/закрываются по требованию), Archival Memory (read-write, безлимитный объём), External RAG (безлимитный, через MCP/кастомные инструменты) как четыре уровня с разными паттернами доступа)

**Блок №073** — `Источник: Letta` · `Раздел: Constitution — идентичность через контекст` · `Тип блока: Design Principle` · `Foundation Section: memory` · *(получено через WebFetch, не прямым curl — отмечено отдельно)*
```
Context determines personality and identity, and evolution of context enables continual learning.
```
```
A Letta agent should prefer the identity formed by its experiences, over that of the underlying model.
```

**Блок №074** — `Источник: Letta` · `Раздел: Constitution — управление контекстным окном` · `Тип блока: Memory Model` · `Foundation Section: memory` · *(получено через WebFetch)*
```
The context window is a precious resource that must be actively managed.
```
```
old information is evicted as new information is added.
```

**Блок №075** — `Источник: Letta` · `Раздел: Constitution — прогрессивное раскрытие` · `Тип блока: Capability Attachment` · `Foundation Section: skills` · *(получено через WebFetch)*
```
Context should be surfaced at the level of detail the current moment requires.
```
```
Only including skill metadata (the name, description, and location) in-context
```

**Блок №076** — `Источник: Letta` · `Раздел: Constitution — обучение через системный промпт` · `Тип блока: Update Mechanism` · `Foundation Section: update` · *(получено через WebFetch)*
```
system prompts have been static and manually written by humans to program LLM behaviors. Letta agents...have the ability to adapt over time through token-space learning
```

---

## ИСТОЧНИК: Generative Agents: Interactive Simulacra of Human Behavior (Park et al., Stanford, arXiv 2304.03442)

Способ получения: полный текст статьи через ar5iv.labs.arxiv.org, HTML очищен от тегов.

**Блок №077** — `Источник: Generative Agents` · `Раздел: Архитектура — поток памяти и рефлексия` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
memory stream, a long-term memory module that records, in natural language, a comprehensive list of the agent's experiences. A memory retrieval model combines relevance, recency, and importance to surface the records needed to inform the agent's moment-to-moment behavior. The second is reflection, which synthesizes memories into higher-level inferences over time, enabling the agent to draw conclusions about itself and others.
```

**Блок №078** — `Источник: Generative Agents` · `Раздел: Retrieval function — формула ранжирования` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
recency, relevance, and importance scores to the range of [0,1] using min-max scaling. The retrieval function scores all memories as a weighted combination of the three elements: score = α(recency)·recency + α(importance)·importance + α(relevance)·relevance
```

**Блок №079** — `Источник: Generative Agents` · `Раздел: Reflection — вопрос для синтеза выводов` · `Тип блока: Memory Model` · `Foundation Section: memory`
```
most salient high-level questions we can answer about the subjects in the statements?" The model's response generates candidate questions: for example, What topic is Klaus Mueller passionate about? and What is the relationship between Klaus Mueller and Maria Lopez? We use these generated questions as queries for retrieval
```

---

*(конец блоков первичного прохода — №001–079; сводка и проверка ниже)*
