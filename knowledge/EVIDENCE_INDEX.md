# Evidence Index — AI Agent Systems Research

Registry of every project/source touched during Stage 0A's second object (real AI agent/system internal organization), across all four evidence files plus the document-autopsy batch. Built in response to a direct question about depth: this index makes reading depth explicit and auditable per project, rather than leaving "how well was this actually looked at" implicit.

**Confidence here is about reading depth, not mechanism validity** (that's the separate Confirmed/Established/Inferred/Unverified scale in `METHODOLOGY.md`). Four tiers:
- **High** — the actual file was fetched and read end-to-end.
- **Medium** — no full fetch, but the search tool returned a substantial, structured, likely near-complete excerpt.
- **Low** — a single short snippet only, not cross-checked, almost certainly a partial view of the source.
- **Unverified** — catalogued as an available resource but not actually analyzed for mechanism content this session.

Source file abbreviations: `AGT` = `...-ai-agent-systems.md`, `OBS` = `...-obscure-repos-experimental-systems.md`, `WFL` = `...-workflows-issues-rfc-prompts.md`, `CASE` = `cases/2026-08-03-batch1-document-autopsies.md`.

## Batch AGT — known AI agent systems

| Project | Documents analyzed | Artifact type | Mechanisms extracted | Confidence |
|---|---|---|---|---|
| AGENTS.md standard (agents.md, agentsmd, sno-ai/mda, indisoluble/AGENTS-spec) | Homepage, READMEs, MDA spec section | Official spec + community specs | A | Medium |
| Anthropic Claude Skills | Docs pages, engineering blog, `anthropics/skills` README, **`template/SKILL.md` (full)** | Official docs + official repo | B, C | High |
| OpenHands | 4 SDK/arch doc pages, `memory.py` source | Official docs + source | C | Medium |
| SWE-bench / SWE-agent | Harness reference, eval guide, Docker migration doc | Official docs | D | Medium |
| Cortex | README | Repo README | E | Low |
| Codemem | `docs/architecture.md` | Repo doc | E | Low |
| jcode | `docs/MEMORY_ARCHITECTURE.md` | Repo doc | E, G | Low |
| agent-memory (inosx) | `docs/memory-system.md` | Repo doc | E | Low |
| AWS sample-autonomous-cloud-coding-agents | `docs/design/MEMORY.md` | Repo doc | E, F, G, H | Medium |
| Self-critique pattern catalogs (6 sources) | 6 articles | Blog / pattern catalog | I, J, K, L | Medium |

## Batch OBS — obscure repos and experimental systems

| Project | Documents analyzed | Artifact type | Mechanisms extracted | Confidence |
|---|---|---|---|---|
| ostk.ai | README | Repo README | M | Low |
| OpenSwarm (openswarm-os) | README | Repo README | R | Low |
| **OpenCode Swarm** | README (snippet) + **`docs/architecture.md` (full, CASE)** | Repo doc | P, N, plus full autopsy | High |
| deepelement-mind/openos | README | Repo README | Q | Low |
| justEstif/openswarm | `docs/ARCHITECTURE.md` | Repo doc | (design-principle findings, unlettered) | Low |
| genesis-ssmp | README (full `architecture.md` fetch failed) | Repo README | M | Low |
| Deterministic-agent-execution-engine (Asirwad) | README | Repo README | N (early instance) | Low |
| agent6 (elesiuta) | `STATE_MACHINES.md` | Repo doc | M, N, O | Medium |
| agentFlow (Yupoer) | README | Repo README | N | Low |
| ai-runtime-lab (Ali-hey-0) | README | Repo README | N, O | Medium |
| AgentFlow (AleSaiani) | README | Repo README | N | Low |
| **Kimi-code** | README (snippet) + **`permission.md` (full, CASE)** | Repo doc | Z, plus full autopsy | High |
| agentscope | `_engine.py` source | Source code | Z | Medium |
| agent-perms (rgharris) | README | Repo README | Z | Low |
| intus-permission-rule-gate | README | Repo README | Z | Low |
| cleveragents-core | `escalation-architecture-proposal.md` (Gitea) | Repo doc | (escalation-tier findings, unlettered) | Low |
| Claude Code permissions | Official docs page | Official docs | Z | Medium |
| Sieve postmortem | Blog post (Martin Beauvais) | First-person blog | X | Medium |
| Grinta-Coding-Agent | `docs/journey/README.md` | Repo doc | Y | Medium |
| AgentHub retrospective | Blog post (Hashnode) | First-person blog | X | Medium |
| Katherine Cass retrospective | Blog post | First-person blog | U | Medium |
| agentic-ceo | `docs/DEEP_DIVE.md` (snippet-depth, superseded — see full pass below) | First-person technical blog | S, T, V, W | **Revised from High to Medium (2026-08-03)** — a full-document, source-code-verified pass (`knowledge/cases/2026-08-03-agentic-ceo-full-pass.md`) found the project's headline quantitative claim (Critic's "23% downgrade," 0.9 confidence threshold) does not exist anywhere in `critic.py`'s source, and 5 of the project's own documented agents were never implemented. Narrative depth was mistaken for verification depth. Pattern W's citation of this project now carries an explicit caveat. |

## Batch WFL — workflows, issues, RFC, prompt version control

| Project | Documents analyzed | Artifact type | Mechanisms extracted | Confidence |
|---|---|---|---|---|
| ryofuu/agentflow | README | Repo README | AA | Low |
| zeyad-azima/agentsbear | README | Repo README | AA | Low |
| craftsman-labs/simpleagents | README | Repo README | AA | Low |
| hexdag | PyPI page | Package page | AA | Low |
| **hermes-multi-agent-workflow** | README (snippet) + **`AGENTS.md` (full, CASE)** | Repo doc | BB, plus full autopsy | High |
| GittieLabs/agentflow | README (archived commit) | Repo README | AA | Low |
| terrylica/claude-code-skills-github-issues | README | Repo README | CC | Medium |
| mindmorass/reflex | `github-harvester/SKILL.md` | Repo skill file | CC | Medium |
| FacuM/yolo-agent | `knowledge-base-generator/SKILL.md` | Repo skill file (near-full) | CC, F | Medium |
| github/gh-aw | `discussion-task-miner.md` + PR #9428 | Repo doc + PR description | CC | Medium |
| dsifry/metaswarm | `knowledge-curator-agent.md` | Repo doc (near-full) | CC | High |
| kieranpotts/rfc | README | Repo README | DD | Medium |
| bwnodak/eng-rfc | README | Repo README | DD | Medium |
| bytecodealliance/rfcs | `template-full.md` | Full template file | DD | Medium |
| pandev-metrics.com | Blog article | Blog | DD | Medium |
| tech.attentive.com | Blog article | Blog | DD | Medium |
| openclaw/rfcs | README | Repo README | DD | Medium |
| prompt-version-control (saurabhghatnekar) | README | Repo README | EE | Low |
| PromptTree (yedhuk) | README | Repo README | EE | Medium |
| promptrepo (+ duplicate) | PyPI page | Package page | EE | Medium |
| prompt-template-version (MukundaKatta) | README | Repo README | EE | Low |
| reaatech/prompt-version-control | README | Repo README | EE | Medium |
| System prompt leak repos (6 repos) | Index pages only | Repo catalogs | (source class noted only) | Unverified |
| CLAUDE.md sources (fred, ayautomate, claude.com, proportione, sdd.sh) | **`ThalesGroup/fred/CLAUDE.md` (quoted near-full, 2 commits)** + 4 guide articles | Real production file + guides | A | Medium/High |

## Batch CASE — parallel full-workflow passes (hierarchical team: 3 background subagents + centralized synthesis)

| Project | Documents analyzed | Artifact type | Mechanisms extracted | Confidence |
|---|---|---|---|---|
| dsifry/metaswarm | `README.md`, `adversarial-review-rubric.md`, `issue-orchestrator.md` (all full) | Repo docs | 7 mechanisms, 2 candidate new patterns | High |
| Jmeg8r/cortex (was As-The-Geek-Learns/cortex) | 13 documents full (research paper, failure-analysis, external-evaluation + response, MASTER-PLAN, etc.) | Repo docs, verified via full 172-file tree | 7 mechanisms, 2 candidate new patterns, 2 contradiction findings | High |
| brcrusoe72/agentic-ceo | 9 documents full + 2 source files exhaustively verified | Repo docs + source code | 6 mechanisms, 1 candidate new pattern, **3 contradiction findings including a falsified headline mechanism** | High |
| os-tack/ostk.ai | 10 documents full (repo + companion site), verified via tree + org API + 404 check on referenced private repo | Repo docs + site + API calls | 10 mechanisms, several candidate new patterns, **2 contradiction findings including a self-contradicting license** | High |

## Batch AIENG — AI Engineering profession investigation, 2026-08-11

Full source-level detail, source-hierarchy tags (T1–T4), and Stage 1.5 abstraction-level tags: `research/AI-Engineering/02-evidence.md`. Report: `research/AI-Engineering/03-full-report.md`; owner-facing profession model: `research/AI-Engineering/04-profession-model.md`. Confidence below folds in six Stage-2 direct re-verifications performed during synthesis (marked "verified directly" in the report), not just the original three parallel channel agents' Stage 1 reads.

| Project / source | Documents analyzed | Artifact type | Confidence |
|---|---|---|---|
| Anthropic — Building Effective Agents (+ Zhang AI Eng Summit talk) | Essay read directly | Official essay | High |
| `humanlayer/12-factor-agents` (+ Horthy AI Engineer talk) | Raw `README.md` | Repo doc | High |
| Simon Willison — agentic engineering patterns | Written companion (simonwillison.net) | Independent practitioner blog | Medium |
| Anthropic — multi-agent research system | Official post | Official blog | Medium |
| `anthropics/skills` + Skills docs/spec/best-practices cluster | README + spec folder (Stage 1); `agentskills.io/specification` **re-fetched directly, Stage 2** | Official repo + spec | High |
| `agentskills/agentskills` | Docs-page level | Governance repo docs | Medium |
| Zhang & Murag — "Don't Build Agents, Build Skills Instead" | Aggregated transcript sources | Conference talk | Medium |
| `obra/superpowers` | Raw `CLAUDE.md` | Repo doc | High |
| OpenHands microagents → Skills migration | Doc page (Stage 1, claim not found on page cited) + independent web search corroboration **(Stage 2)** | Official docs + search corroboration | Medium |
| Letta — context-engineering / memory-blocks cluster | Vendor blog posts + `letta-ai/skills` GitHub artifact | Vendor blog + repo | Medium |
| `letta-ai/letta` (MemGPT) three-tier memory | Docs + secondary/community sources for tool names | Docs + secondary | Low |
| Letta — "Rearchitecting Letta's Agent Loop" | `letta.com/blog/letta-v1-agent` **re-fetched directly, Stage 2** | Official blog | High |
| Cline memory bank | Docs-page (raw `.mdx` 404'd) | Docs page | Medium |
| Claude API — `shared/agent-design.md` | Raw primary artifact | Repo skill file | High |
| Anthropic — code execution with MCP | Official post | Official blog | Medium |
| MCP official architecture spec + "Introducing MCP" | Official spec/announcement | Official docs | Medium |
| Google — MCP stateless scaling post | `developers.googleblog.com/...` **re-fetched directly, Stage 2** | Official eng blog | High |
| Anthropic — "Building Agents with Skills" (Jan 2026) | `claude.com/blog/...` **re-fetched directly, Stage 2** | Official blog | High |
| OpenAI — Agents SDK + practical guide | Official docs | Official docs | Medium |
| `wshobson/agents` | Raw `README.md` + `docs/architecture.md`; routing-gap claim **re-confirmed directly, Stage 2** | Repo docs | High |
| Claude Code docs — subagents + skills preload | Official docs | Official docs | Medium |
| `github/spec-kit` | Raw `spec-driven.md` | Repo doc | High |
| `block/goose` | Raw `AGENTS.md` (`recipe.yaml` 404'd, structure summarized from docs) | Repo doc + docs | Medium |
| ADR cluster (`adr.github.io`, `microsoft/agent-framework`, `vercel/ai` adr-skill) | Official/docs level | Docs + repo | Medium |
| Boris Cherny — prompt-deletion discipline (YC Startup School) | Third-party transcript writeup (sozai.app) | Conference talk | Medium |
| Boris Cherny — Co-Work architecture (@Scale) | Third-party transcript writeup (sozai.app) | Conference talk | Medium |
| Cat Wu — "ship demos, not docs" | Interview, transcript-derived | Podcast/interview | Medium |
| Lance Martin (LangChain) — context engineering | Written companion (latent.space) | Independent practitioner blog | Medium |

## Batch ORCH — Orchestrator↔Specialist invocation contract, 2026-08-12

Brief from Engineer (sibling Foundation repo). Full source-level detail: `knowledge/evidence/2026-08-12-orchestrator-specialist-invocation.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement — Orchestrator↔Specialist Invocation Contract". Closed question record: `OPEN_QUESTIONS.md`, 2026-08-12 entry.

| Project / source | Documents analyzed | Artifact type | Confidence |
|---|---|---|---|
| Claude Code — sub-agents, agent-teams, cross-session-messaging | 3 full doc pages, fetched directly | Official docs | High |
| Anthropic — multi-agent research system | Official engineering post, fetched directly, asked directly about all 5 brief questions | Official blog | High |
| OpenAI Agents SDK — Handoffs | `handoffs/` doc page + raw `handoffs.md`, fetched directly | Official docs | High (confident negative finding: no return channel described) |
| LangGraph Supervisor (`langgraph-supervisor-py`) | Reference page + `handoff.py` reached via search, function-level detail only (no verbatim source confirmed) | Repo docs/source | Medium |
| CrewAI — Collaboration | Official docs page, fetched directly | Official docs | Medium (tool signature High; return/sufficiency mechanism explicitly unreached) |

## Batch SELF — External validation of this project's own reverse-engineering methodology, 2026-08-12

Brief from Engineer, relayed from `ENGINEER/OPEN_QUESTIONS.md`. This project's own methodology (`skills/reverse-engineering/references/`) is the investigation target; the table below is the external reference set it was checked against — deliberately not this project's own prior documents. Full synthesis: `knowledge/CAPABILITY_MAP.md`, "External Validation" section. Correction applied: `skills/reverse-engineering/references/METHODOLOGY.md`, Definition of Done provenance note.

| Project / source | Documents analyzed | Artifact type | Confidence |
|---|---|---|---|
| Anthropic — multi-agent research system | Official post, re-fetched directly, asked specifically about sufficiency-judgment, source hierarchy, disagreement-handling, per-claim confidence | Official blog | High |
| Deep Research: A Survey of Autonomous Research Agents (`arxiv.org/html/2508.12752v1`) | Fetched directly, asked specifically about source verification/ranking and sufficiency/confidence mechanisms | Academic survey | High |
| Deep Research Agents: A Systematic Examination And Roadmap (`arxiv.org/abs/2506.18096`) | Abstract-level fetch only, full text not reached | Academic survey | Medium |
| OpenAI — Deep Research system card | Search-corroborated summary, not a full direct fetch of the PDF | Official system card | Medium |
| "Why Your Deep Research Agent Fails" / DeepHalluBench (`arxiv.org/html/2601.22984v1`) | Search-corroborated summary | Academic benchmark paper | Medium |
| ICD 203 — Analytic Standards | Primary PDF (`dni.gov`) returned HTTP 403 this session, not reached; two independent secondary summaries (`legalclarity.org`, `factually.co`) cross-checked against each other | Secondary summaries of an unreached primary | Medium (primary unreachable, flagged per Stage 2's "explicit report when a primary artifact is unreachable") |
| NATO/Admiralty Code (source reliability × information credibility) | Search-corroborated, multiple independent secondary sources agreeing | Secondary (SANS, threat-intel practitioner sources) | Medium |
| National Intelligence Estimate — dissent-preservation practice | Search-corroborated (CFR, Wilson Center, GAO) | Secondary/institutional | Medium |
| Bellingcat — Online Investigation Toolkit / Verification Handbook | Search-corroborated, not a full fetch of the toolkit itself | Official toolkit (secondary description) | Medium |
| IFCN Code of Principles | Fetched directly | Official code of principles | High |
| Xerox / Rank Xerox-Fuji benchmarking methodology, "adapt not adopt" | Search-corroborated across multiple academic sources | Academic/secondary | Medium |
| Nygard ADR template (Context/Decision/Consequences) | Search-corroborated, well-documented public standard | Secondary, high-consensus | Medium |
| Google SRE — postmortem "contributing factors" doctrine | Search-corroborated; official `sre.google` pages identified but not directly fetched this session | Official book/site (secondary access) | Medium |

## Batch LAYERS — Capability layering (available/belongs/permitted/recommended), 2026-08-12

Brief from Engineer, relayed from `ENGINEER/OPEN_QUESTIONS.md`. Full source-level detail: `knowledge/evidence/2026-08-12-capability-layering-tool-permissions.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement to Capability 4 (Permissions) — Capability Layering" section.

| Project / source | Documents analyzed | Artifact type | Confidence |
|---|---|---|---|
| Claude Code — mcp, sub-agents, permissions, skills | 4 full doc pages, fetched directly, version-numbered | Official docs | High |
| Model Context Protocol spec — server/tools, basic/authorization | 2 full spec pages, fetched directly | Official spec | High |
| LangChain — human-in-the-loop (`HumanInTheLoopMiddleware`) | Official doc, fetched directly, verbatim code example returned | Official docs | High |
| OpenAI Agents SDK — tools, guardrails | 2 official doc pages, fetched directly | Official docs | High |
| Amazon Bedrock Agents (Classic) — agents-permissions, agents-action-create | 2 official doc pages, fetched directly | Official docs | Medium (product itself flagged legacy/maintenance-mode by AWS's own page) |
| Salesforce Agentforce — Topics/Actions, agent user permissions | 2 Help Center pages, fetch attempted, both 404'd/unrenderable this session | Official docs (unreached) | Unverified — not credited as evidence |

## Batch ROUTE — Automatic capability/model selection, tool selection, cost optimization, verification, update, 2026-08-12

Brief from Engineer (second direct question, same day as Batch ORCH), re: a 4-layer "Capability System" (Skills/Tools-MCP-Plugins/Models/Routing), reinforced mid-session on fan-out cost (sub-question 5) and periodic capability retirement (sub-question 7). Full source-level detail: `knowledge/evidence/2026-08-12-capability-model-routing-selection.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement — Automatic Capability/Model Selection" section. Closed question record: `OPEN_QUESTIONS.md`, 2026-08-12 entry.

| Project / source | Documents analyzed | Artifact type | Confidence |
|---|---|---|---|
| Anthropic — tool search tool, programmatic tool calling, Claude Code cost management | 3 full doc pages, fetched directly, version-numbered | Official docs | High |
| Systima — "The Subagent Tax" | Full blog post, fetched directly, methodology and caveats extracted | Independent practitioner benchmark | High |
| `rohitg00/pro-workflow` — `mcp-audit` SKILL.md | Full file, fetched directly | Repo skill file | High |
| Red Hat Developer — LLM Semantic Router | Full article, fetched directly | Official vendor engineering blog | High |
| Arize AI — "How cheap models changed multi-agent economics" | Full blog post, fetched directly | Vendor engineering blog | Medium-High |
| joost.blog — self-updating agent skills | Full post, fetched directly | Independent practitioner blog | Medium (single practitioner) |
| bigprompthub.com — Deadskills vs Skillreaper | Full comparison article, fetched directly (both tools' own READMEs as its stated source) | Independent secondary write-up | Medium |
| `vllm-project/semantic-router` | README, fetched directly, thin on mechanism detail | Repo README | Low |
| RouteLLM (ICLR 2025), FrugalGPT (Stanford), GPT-5 router (OpenAI) | WebSearch-aggregated only; OpenAI's own post fetch blocked (HTTP 403) | Papers/official post (search-corroborated) | Medium |
| Langfuse/LangSmith agent evaluation | WebSearch-aggregated only, not fetched directly | Official product docs (search-corroborated) | Medium |
| `anthropics/claude-code` issues #44968, #26179 | Referenced via WebSearch aggregation; direct `gh`/API fetch attempted and failed (`gh` not present in this environment) | Real filed GitHub issues (unreached primary) | Medium |
| MCP Registry, Anthropic model-deprecations docs, Dependabot/Renovate | WebSearch-aggregated only | Official docs / well-known product (search-corroborated) | Medium |
| YouTube — "The Real Cost of AI Agents in 2026" | `WebFetch` attempted, returned page chrome only, no transcript | Video (not directly accessed) | Unverified — not credited as evidence, logged per Stage 1's video-source rule |

## Batch ENGCAP (2026-08-12) — Engineer's ENGINEERING-category capability-map audit

| Source | Depth | Type | Confidence |
|---|---|---|---|
| `Skill System/registry.json` (ENGINEERING category, 17 entries) + `ENGINEER/skills/` directory listing | Full read of all 17 `SKILL.md` files + direct `ls` of installed skills | Primary artifact, this project's own sibling repo | High |
| `find`/`grep` for `idea-calibration.md`/`PROJECT_DNA.md`/`Bootstrap Sequence` across ENGINEER | Direct search, zero hits | Primary artifact (absence proof) | High |
| Anthropic — "Demystifying evals for AI agents" | Full post, fetched directly, asked explicitly about builder/grader independence | Official engineering blog | High |
| WebSearch — LLM-as-judge builder-bias / independent agent evaluation | Aggregated snippets (Microsoft/Azure AI Foundry blog, arXiv 2601.05111, arXiv 2605.24134) | Search-aggregated (not individually fetched) | Medium |
| WebSearch — agent eval/drift/regression production practice 2026 | Aggregated snippets (FutureAGI blog, arXiv 2601.04170, arXiv 2605.01604) | Search-aggregated (not individually fetched) | Medium |
| `knowledge/CAPABILITY_MAP.md` (Capabilities 2/4/5/8/9/10/11 + three 2026-08-12 Refinement sections) | Reused, previously fetched fresh the same day | This project's own prior-verified synthesis | Inherits prior per-claim confidence |

## Batch EXECREC (2026-08-12) — observability/execution record for independently-living agents

Full findings: `knowledge/evidence/2026-08-12-independent-agent-execution-record.md`.

| Source | Depth | Type | Confidence |
|---|---|---|---|
| `platform.claude.com/docs/en/managed-agents/observability` + `/session-operations` | Full page, fetched directly, exact API methods extracted | Official Anthropic docs | High |
| `code.claude.com/docs/en/sessions` | Full page, fetched directly | Official Anthropic docs | High |
| `developers.openai.com/api/docs/guides/conversation-state` | Full page, fetched directly, one endpoint's exact call shape not confirmed | Official OpenAI docs | Medium-High |
| WebSearch — OpenAI Assistants API deprecation date | Aggregated (Microsoft Q&A, OpenAI migration guide) | Official + secondary (search-corroborated) | High (specific date, cross-corroborated) |
| OpenTelemetry GenAI semantic conventions (moved page + targeted WebSearch) | One direct fetch (generic confirmation only) + one targeted WebSearch for span/attribute names | Official spec (partially reached) | Medium |
| LangSmith trace API (`docs.langchain.com/langsmith/trace-with-api`) | WebSearch-aggregated only | Official docs (search-corroborated) | Medium |

## Batch MAINENG (2026-08-13) — verification of three mechanisms from old MAIN_ENGINEER (predecessor repo)

Brief from Engineer, relayed via `ENGINEER/OPEN_QUESTIONS.md`, 2026-08-13 entry. Full source-level detail and per-mechanism verdicts: `knowledge/evidence/2026-08-13-main-engineer-mechanisms-verification.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement — instruction-file governance mechanisms checked against old MAIN_ENGINEER" section.

| Source | Depth | Type | Confidence |
|---|---|---|---|
| `megapolisagent/MAIN_ENGINEER` — `MAIN_ENGINEER_CORE.md`, `AGENT_PROTOCOL.md`, `OBSIDIAN_PROTOCOL.md`, `ai_engineering_operating_system_master.md`, `SKILLS_REGISTRY.md`, `Claude.md` | Full text, fetched directly this session (`raw.githubusercontent.com`) | Primary artifact (predecessor repo) | High |
| `.../ENGINEERING_LOG/external_review_MAIN_ASSISTANT_v1.7.1_2026-06-16.md`, `.../v1.7.3_2026-06-19.md`, `.../v1.7.4_2026-06-19.md` | Full text, fetched directly | Primary artifact (real exercised instances of the mechanism) | High |
| `anthropics/skills` `README.md` + `platform.claude.com/.../agent-skills/best-practices` | Full text, fetched directly | Official docs | High |
| Arthur.ai, Latitude.so, Agenta, aiquinta, tianpan.co — prompt/agent-config SemVer practice | WebSearch-aggregated, not individually fetched in full | Vendor/practitioner (search-corroborated) | Medium |
| a16z retention-benchmarks post, Sequoia "Retention" article | WebSearch-aggregated | VC/investor practice writeup (search-corroborated) | Medium |
| arXiv 2605.10223 (tiered AgentRunner), `Gamferno/agent-constitution`, MetaGPT/CAMEL writeups | WebSearch-aggregated | Framework/paper/repo (search-corroborated, checked and found not a full match) | Medium |
| `.../ENGINEERING_LOG/registry.md`, `.../v1.7.2_2026-06-16.md`, `ARCHIVE/`, `PROJECT_SUMMARIES/`, `AI_Projects/*` | Not fetched this session | Primary artifact (unreached) | Unverified — not credited as evidence, honest gap on the Karpathy-citation premise |

## Batch KIMI (2026-08-13) — Kimi/Moonshot AI: real strength/price, data policy, integration with Claude Code

Brief from Engineer, relayed via `ENGINEER/OPEN_QUESTIONS.md`, 2026-08-13 entry. Full source-level detail and per-sub-question verdicts: `knowledge/evidence/2026-08-13-kimi-moonshot-verification.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement — Kimi (Moonshot AI)" section.

| Source | Depth | Type | Confidence |
|---|---|---|---|
| `platform.kimi.ai/docs/agreement/userprivacy` | Full page, fetched directly | Official privacy policy | High |
| `platform.kimi.ai/docs/pricing`, `platform.kimi.ai/docs/guide/claude-code-kimi` | Full pages, fetched directly | Official docs | High |
| `forum.moonshot.ai/t/kimi-k3-is-here-our-most-capable-model/480` | Full page, fetched directly | Official vendor announcement | High |
| `openrouter.ai/moonshotai/kimi-k3`, `artificialanalysis.ai/models/comparisons/kimi-k2-6-vs-gemini-2-5-pro` | Full pages, fetched directly | Independent aggregator/benchmark | High |
| `aihackers.net/risks/kimi/` + `/verify/kimi-claims/` | Full pages, fetched directly, checked for own cited evidence | Independent secondary (found to self-flag its own key claim as unverified) | Medium (useful as a negative check, not as confirming evidence) |
| Wikipedia `Moonshot_AI` + SCMP profile of Yang Zhilin | Search-aggregated, cross-corroborating | Independent journalism/tertiary | Medium-High (two independent sources agree) |
| `github.com/x51xxx/kimi-mcp-server` (README) | Full README, fetched directly | Repo doc (independent third-party MCP bridge) | High |
| Gemini long-context pricing (apidog.com, devtk.ai, pricepertoken.com); SWE-Bench Pro comparative figures; K2.5/K2.6 pricing (DeepInfra, NxCode) | WebSearch-aggregated only | Secondary (search-corroborated) | Medium |
| `techtimes.com` Moonshot funding/data-risk article | Fetch attempted, HTTP 403, not read | Unreached | Unverified — not credited as evidence |

## Batch SYNC (2026-08-17) — cross-repo markdown/git status-sync patterns, no CI/no shared backend

Brief from Engineer, direct call (narrow question, criterion pre-fixed per brief, relayed above the tool boundary rather than written to `OPEN_QUESTIONS.md` first). Prompted by a real found-and-fixed rassinhron between `ENGINEER`'s and this project's own decision-status records on the same question. Full source-level detail: `knowledge/evidence/2026-08-17-cross-repo-status-sync-patterns.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement — Cross-Repo Status Sync (git/markdown, no CI)" section. Closed question record: `OPEN_QUESTIONS.md`, 2026-08-17 entry.

| Source | Depth | Type | Confidence |
|---|---|---|---|
| Git submodule mechanism (`git-scm.com` general primitive) + `opensource.com`, `martinuke0.github.io` write-ups | WebSearch-aggregated, well-established primitive, not individually full-fetched | Official concept + secondary write-ups | Medium |
| Michael Nygard's ADR pattern (status field, supersession) | Already logged Medium in Batch ORCH/SELF; reused, not re-fetched this session | Well-documented public standard | Medium |
| Richards & Ford, *Fundamentals of Software Architecture* (cross-repo ADR centralization) | Quoted directly via `synchronium.github.io/software-architecture-wiki`, fetched directly this session | Secondary source quoting a named book | Medium (secondary quoting primary; book itself not directly read) |
| shields.io official docs — dynamic endpoint badges | WebSearch-aggregated, official docs, not individually full-page-fetched | Official docs | Medium |
| TC39 `proposals` repo central stage registry | Fetched directly (`README.md`, `how-we-work/README.md`) — sync mechanism between central registry and individual proposal repos **not confirmed**, dropped from findings | Official repo (mechanism unconfirmed) | Unverified — not credited as evidence |
| `embeddedartistry.com` ADR-in-repo article | Fetched directly — did not address multi-repo scenario, dropped from findings | Independent blog (off-topic for this question) | Unverified — not credited as evidence |

## Batch BIZPROD (2026-08-17) — "AI Business Producer" category: real business-analysis + specialist-agent-coordination systems

task_id `ENG-2026-08-17-BIZPRODUCER-001`, World Research step inside Engineer's `idea-calibration` (Confidence Low). Full source-level detail: `knowledge/evidence/2026-08-17-ai-business-producer-systems.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement — 'AI Business Producer' category" section.

| Source | Depth | Type | Confidence |
|---|---|---|---|
| `api.github.com/repos/foundationagents/metagpt`, `.../OpenBMB/ChatDev` | Full API response, fetched directly | Primary (stars/activity/archived-status) | High |
| `api.github.com/repos/ES7/AI-Software-Company-Simulator`, `.../vedanta/the-system`, `.../msoedov/mesa`, `.../Caoquyen1913/ai-outsourcing-studio` | Full API response, fetched directly | Primary (stars/activity) | High |
| MetaGPT, ChatDev READMEs | Substantial excerpt via search, not individually full-fetched | Official repo README | Medium |
| `goodhelp.ai` | Full page, fetched directly (`WebFetch`) | Official product page | High |
| `aqen.ai`, `aqen.ai/product` | Substantial excerpt via search | Official product page | Medium |
| `itsmeduncan.com/2026/05/05/the-builders-bet`, `linkedin.com/in/itsmeduncan` | Substantial excerpt via search | Founder's own blog/profile (level 4, self-report) | Medium |
| `voraiq.com`, `/pricing`, `/agents`, `/live-metrics`, `/reviews` | Substantial excerpts via search, multiple pages | Official product pages | Medium |
| `apprecs.com/ios/6736479518/vora-iq` | Substantial excerpt via search | Independent third-party App Store review aggregator | Medium |
| `cofounder.co`, `cofounder.co/resources/introducing-cofounder-2` | Substantial excerpts via search | Official product page + founder blog post | Medium |
| `usecarly.com/blog/cofounder-ai` | Substantial excerpt via search | Independent product teardown | Medium |
| `currlyai.com/tool/cofounder-agentic-company-os`, `aitoolsclub.com/meet-cofounder...` | Substantial excerpts via search | Independent write-ups | Medium |
| rootentity.com, startcaas.com, soleur.ai/agents, capibot.io, agentcorp.work, gforce.cloud, uuple.com, opscale.io, syzygia.io, incagent.ai, preplix.ai | Search-aggregated snippets only, not individually full-fetched | Official product pages (Tier 4/5 — mechanism claims recorded, usage not independently corroborated) | Low |
| Academic venues for MetaGPT (ICLR 2024) / ChatDev (ACL 2024) | Claimed by each repo's own README, not independently re-verified via arXiv this session | Repo self-report of publication venue | Unverified — not credited beyond "claimed by the project itself" |
| Reddit/Hacker News/Discord/YouTube for any candidate | Not investigated this session (time-boxed to fixed criterion) | — | Unverified — explicitly not investigated |

## Summary

- **Total distinct projects/sources touched**: ~132 (113 prior + ~19 new source-groups from Batch BIZPROD).
- **High confidence (full file/primary-artifact read, incl. Stage 2 direct re-verification)**: 19 — Anthropic Skills template, OpenCode Swarm, Kimi-code, Hermes, dsifry/metaswarm, agentic-ceo, plus 10 from Batch AIENG (Building Effective Agents, 12-Factor Agents, anthropics/skills spec, obra/superpowers, Letta v1 agent post, Claude API agent-design.md, Google MCP stateless post, Anthropic Building-Agents-with-Skills post, wshobson/agents, spec-kit), plus 3 from Batch BIZPROD (MetaGPT/ChatDev GitHub API, 4-clone GitHub API, goodhelp.ai full fetch).
- **Medium**: ~55 — substantial structured excerpts or official docs, no full primary-artifact fetch (+8 from Batch BIZPROD).
- **Low**: ~30 — single short snippet or secondary-sourced claim, not cross-checked (+11 from Batch BIZPROD, the unfetched Tier 4/5 landing pages).
- **Unverified**: 3 categories (system-prompt leak repositories; Batch BIZPROD's claimed academic venues for MetaGPT/ChatDev; Batch BIZPROD's not-investigated Reddit/HN/Discord/YouTube — each catalogued as a source class, not analyzed or credited as evidence).

**Honest reading of this table**: the ratio of High to Medium/Low is small — 6 out of ~56. Most of the Capability Map (`CAPABILITY_MAP.md`) was built from Medium/Low-depth sources, which is exactly the gap flagged in the prior correction. The document-autopsy batch (`CASE`) is the first deliberate push toward High-confidence, full-document reading, and is explicitly a first installment, not a completed pass across the full evidence base. Where the Capability Map cites a Low-confidence project as an example of a mechanism, that citation should be read as "at least one signal of this pattern," not as a fully verified account of that project's actual practice.

## Batch REALESTATE (2026-08-17) — "Agency-first, productize internal tooling second" in real estate/proptech

task_id `ENG-2026-08-17-BIZPRODUCER-002`, direct call from Engineer, criterion fixed before search. Full source-level detail: `knowledge/evidence/2026-08-17-real-estate-agency-to-saas-pattern.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement — 'Agency-first, productize internal tooling second' in real estate/proptech" section.

| Source | Depth | Type | Confidence |
|---|---|---|---|
| Practical Founders podcast + article (MoxiWorks/York Baur) | Substantial excerpts via search | Independent podcast/case study | Medium |
| GeekWire (MoxiWorks/Vector Capital funding) | Substantial excerpt via search | Independent tech press | Medium |
| Vector Capital, MoxiWorks own site | Substantial excerpts via search | Company/investor self-report (level 4) | Medium |
| Inman — Avenue 8/Sidekick (2024-06-10), Compass (2018-07-27, 2019-01-03), Anywhere retrospective (2025-10-02), Sequel (2018-10-03), Riley (2019-03-14), StackWrap, Rechat (2026-06-11), indie-brokerage panel (2022-04-21) | Substantial excerpts via search across 8 separate articles | Independent real-estate trade press | Medium |
| Sidekick's own site, Michael Martin LinkedIn posts | Substantial excerpts via search | Company/founder self-report (level 4) | Medium |
| RealTrends — Mainframe/ABE (2023-03-14), Bailey vs. Duffy build-vs-buy (2023-07-10) | Substantial excerpts via search | Independent real-estate trade press | Medium |
| The Nassau Guardian — Rodland/RoRo (2026-04-17, 2026-07-27) | Substantial excerpts via search, 2 articles | Independent regional business press | Medium |
| HousingWire — Rodland/RoRo interview (2026-05-22), The Real Brokerage/Leo 2.0 (2026-08-12) | Substantial excerpts via search | Independent real-estate trade press | Medium |
| Jason Fried (Medium 2015, 37signals podcast, Basecamp About page, Signal v. Noise 2009, Inc. magazine) | Substantial excerpts via search, 5 independent venues | Primary/first-person, multi-venue | Medium-High (not individually full-fetched, but converging across 5 independent publications over a decade) |
| NPR, Globe and Mail, Ottawa Business Journal, Shopify's own blog, rubyonrails.org 2005 (Shopify/Snowdevil) | Substantial excerpts via search, 5 sources | Independent press + primary contemporary post | Medium-High (same convergence logic as Basecamp) |
| Crawlux/TG3 own blog and About pages | Substantial excerpts via search, 2 pages | Company self-report (level 4), no independent corroboration found | Medium |
| Side Inc — TechCrunch, The Real Deal (2x), Camber Creek interview | Substantial excerpts via search, 4 sources | Independent tech/real-estate press | Medium |
| Small 2025-2026 agency-ops-tool cluster (AgencyFlo, Rofinery, Supervisible, Wisdom, Tikr/Konabos, Hero Projects/Shape) | Substantial excerpts via search, 6 sources | Company self-report (level 4), no independent corroboration | Low |
| Job postings — Kirpa Properties, P3 Properties, properti, ON Real Estate, Hogar Properties, Zenant, FutureStack AI, Areezo, TEO, Outcome/Sid Jain, Ledora | Substantial excerpts via search, ~11 postings/LinkedIn profiles | Primary hiring documents / founder self-report | Medium (primary for role-content claims; self-report for company-traction claims within the same postings) |
| Vitally.io, Nobel Recruitment (generic SaaS CS-hiring benchmarks) | Substantial excerpts via search | Independent SaaS-industry research | Medium — explicitly flagged as not real-estate-specific |

**Honest note on this batch**: no source above was a full primary-artifact fetch (no company's internal financials, cap table, or source code was reached — none was expected to be reachable for this class of target). Depth is capped at Medium by design: real-estate trade press (Inman, HousingWire, RealTrends) is treated as independent level-3 practitioner journalism per `METHODOLOGY.md`'s source hierarchy, not as a primary artifact, and is the highest tier actually reachable for this target. Two claims reached Confirmed only because 2+ independent outlets covered the same underlying fact independently (MoxiWorks' spin-out; Compass's and Riley's founder admissions, each reported by Inman and consistent with the companies' own subsequent public conduct).

## Batch BIZCHAR (2026-08-17) — What separates professional from superficial business diagnosis: behavior, not knowledge

task_id `ENG-2026-08-17-BIZPRODUCER-003`, direct call from Engineer, criterion fixed before search. Different layer from Batch BIZPROD/REALESTATE — not "what systems/companies exist" but "what character of work makes a business diagnosis professional," for `SOUL.md`/core Skill design. Full source-level detail: `knowledge/evidence/2026-08-17-professional-vs-superficial-business-diagnosis-character.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement — Professional vs. superficial business diagnosis: behavioral character" section.

| Source | Depth | Type | Confidence |
|---|---|---|---|
| McKinsey Podcast transcript, "How to master the seven-step problem-solving process" (Charles Conn, Hugo Sarrazin) | Full transcript fetched directly (Firecrawl, after 2 blocked `WebFetch` attempts) | Official first-party technical content | High |
| Y Combinator Startup Playbook (`playbook.samaltman.com`) | Fetched and read directly | Official primary artifact | High |
| The Mom Test (Rob Fitzpatrick) — via `sachinrekhi.com` full fetch + `mtlynch.io`/`blog.uxtweak.com` search-snippet corroboration | 1 full secondary fetch + 2 converging independent snippets; book itself not fetched | Independent practitioner summaries, 3-way convergent | Medium (Established mechanism, not primary-verified) |
| The Trusted Advisor (Maister/Green/Galford) — via `trustedadvisor.com`, `nateliason.com`, `success-stacks.com` search snippets | Search snippets only, converging across 3 independent write-ups; book not fetched | Independent practitioner summaries, 3-way convergent | Low-Medium (Established mechanism, not primary-verified) |
| AI-specific business-diagnosis-quality critique (searched, not credited) | Search only | Generic AI-hallucination content-marketing pages | Not used as evidence — explicitly named gap, see evidence file |

**Honest note on this batch**: this is the first batch in this project where the two highest-confidence sources (McKinsey, YC) were both reached as full primary-artifact fetches on the first or second attempt — a rarer outcome than the Medium/Low-depth norm the "honest reading" note above this section already flags project-wide. The two supporting sources (Mom Test, Trusted Advisor) stayed at Established rather than Confirmed specifically because the primary books were not reached this session — flagged, not smoothed over. No AI-tool-specific source met the bar for use; the search category is recorded as investigated-but-not-credited, not silently skipped.

## Batch AUTONOMY (2026-08-18) — Unattended/headless AI agent autonomy: sandboxing, non-interactive config, post-hoc audit

Brief from Engineer, registered in `ENGINEER/OPEN_QUESTIONS.md` (2026-08-18 entry), criterion fixed before search. Three sub-questions, ≥2 real systems each. Full source-level detail: `knowledge/evidence/2026-08-18-unattended-headless-agent-autonomy.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement — Unattended/headless agent autonomy" section.

| Source | Depth | Type | Confidence |
|---|---|---|---|
| `code.claude.com/docs/en/sandbox-environments` | Full page, fetched directly | Official vendor docs | High |
| `code.claude.com/docs/en/headless` | Full page, fetched directly | Official vendor docs | High |
| `code.claude.com/docs/en/permission-modes` | Full page, fetched directly (persisted to file, read in full) | Official vendor docs | High |
| `learn.chatgpt.com/docs/agent-approvals-security` (OpenAI Codex CLI, redirected from `developers.openai.com`) | Full page, fetched directly | Official vendor docs | High |
| `microsoft.github.io/autogen/0.2/docs/topics/code-execution/cli-code-executor/` | Full page, fetched directly | Official vendor docs (Microsoft) | High |
| `docs.github.com/en/copilot/concepts/agents/cloud-agent/risks-and-mitigations` | Full page, fetched directly | Official vendor docs | High |
| `docs.aws.amazon.com/bedrock-agentcore/latest/devguide/registry-cloudtrail.html` + sibling AgentCore CloudTrail pages | WebSearch-aggregated across several official pages, not one single full-fetch | Official vendor docs | Medium |
| `docs.openhands.dev/openhands/usage/architecture/runtime` | WebSearch-aggregated substantial excerpt | Official vendor docs | Medium |
| `raw.githubusercontent.com/openai/codex/main/docs/sandbox.md` | Fetched directly — page itself only pointed onward to the `learn.chatgpt.com` page above, contained no independent content; not credited beyond confirming the pointer | Official repo doc (redirect stub) | Unverified — not credited as independent evidence |
| gVisor in an AI-agent-specific context | Searched, no primary source found tying gVisor specifically to agentic tooling | — | Unverified — explicitly not found, not forced into the report |
| Cursor, CrewAI, Devin | Not investigated this session — saturation reached (P6) before these were needed to clear the fixed criterion | — | Unverified — explicitly not investigated, named as a gap |

**Honest note on this batch**: unusually high ratio of full primary-artifact fetches (6 of 9 credited sources at High confidence) — the official Claude Code, OpenAI Codex, GitHub, and AutoGen documentation pages were each substantial and directly on-topic on first fetch, so the search did not need to fall back to secondary blog aggregation to clear the criterion. The two Medium-confidence sources (AWS AgentCore, OpenHands) were left at WebSearch-aggregated depth once saturation was reached for their respective sub-questions (P6) — flagged, not silently promoted to High.

## Batch PRODROLE (2026-08-19) — Producer role (human/managerial practice): sequence, delegation, financial accountability without control

task_id `ENG-2026-08-19-PRODUCERROLE-001`, direct call from Engineer, criterion fixed before search (`ENGINEER/OPEN_QUESTIONS.md`, 2026-08-19 entry). Human/managerial practice only — no AI product investigated in this batch, distinct from Batch BIZPROD/REALESTATE/BIZCHAR above. Full source-level detail: `knowledge/evidence/2026-08-19-producer-role-human-practice.md`. Synthesis: `knowledge/CAPABILITY_MAP.md`, "Refinement — Producer role (human/managerial practice)" section.

| Source | Depth | Type | Confidence |
|---|---|---|---|
| `eosworldwide.com` (14 pages: Integrator, Accountability Chart, Scorecard, IDS, GWC, Level 10 Meeting, People Analyzer, FAQ, etc.) | Substantial excerpts via search, multiple pages, not individually full-fetched | Official methodology source (level 4 — subject describing its own product) | Medium |
| `markcwinters.com` (2 pages, Rocket Fuel co-author) | Substantial excerpts via search | Official methodology source (co-author's own site) | Medium |
| `integratorimpact.com` | Substantial excerpt via search | Independent EOS coach/implementer, not EOS Worldwide itself | Medium |
| `coaches.scalingup.com`, `scalingup.com`, `therainmakergroupinc.com` (FACe PDF, Barriers chapter PDF) | Substantial excerpts via search, including a full PDF chapter | Official methodology source, independent company from EOS | Medium |
| `sup.org` (Stanford University Press, *Riding Shotgun*) | Publisher page + excerpted preface, via search | Academic book, independent of both business-coaching methodologies | Medium |
| `operationscouncil.org`, `robinson.gsu.edu`, `degruyterbrill.com` | Substantial excerpts via search | Independent summary + author's own faculty page (citation cross-check) + publisher TOC | Medium |
| `producersguild.org/code-of-credits-feature-films` | Substantial excerpt via search | Industry-authority primary (Producers Guild of America's own credit definitions) | Medium-High |
| `studiobinder.com`, `torontofilmschool.ca`, `indeed.com`, `geldards.com` | Substantial excerpts via search | Independent film-industry trade education / practitioner explainers | Medium |
| `ipa.co.uk/knowledge/careers-in-advertising/...` | Substantial excerpt via search | Industry-authority primary (UK Institute of Practitioners in Advertising) | Medium-High |
| `creedconsultingservices.com`, `wrapbook.com`, `storyflowe.com`, `a-p-a.net`, `creativeprojectmanagement.org` | Substantial excerpts via search | Independent practitioner accounts + a real posted job description | Medium |
| `scholarship.law.vanderbilt.edu` (JETLaw), `digitalcommons.lmu.edu` (Loyola ELR), `troygould.com`, `iftn.ie` | Substantial excerpts via search | Legal scholarship / entertainment-law-firm practice notes | Medium |
| `beta.bailii.org` — *Film Finance Inc v RBS* [2007] EWHC 195 | Substantial excerpt via search, quoting the actual completion-guaranty contract's operative text | Primary legal artifact (a real court judgment quoting a real contract) | High |
| `21hats.com` (2 episodes), `friedmanpartners.com` | Substantial excerpts via search | Independent podcast/consultancy, named real business owners' first-person accounts | Medium |
| `profit-strategies.com`, `calcalistech.com`, `monsterops.io` | Substantial excerpts via search | Independent critical book reviews / practitioner review (monsterops flagged as having a commercial interest in its own narrative, read with that in mind) | Medium |
| Chief of Staff role, management-consulting engagement-manager/partner role | Not pursued once the criterion was already cleared with margin | — | Unverified — explicitly not investigated to depth, not "checked and rejected" |
| Reddit/Hacker News/Discord/YouTube for any candidate | Not investigated this session (time-boxed to fixed criterion) | — | Unverified — explicitly not investigated |

**Honest note on this batch**: no source reached full-page-fetch depth via `WebFetch` — every source was read through the search tool's own substantial page excerpts, capped at Medium confidence by design per this project's own confidence-vs-depth distinction, except the one primary legal judgment (bailii.org), which quoted enough of the actual contract text directly in the search excerpt to warrant High. This is a human-practice/management-literature target, not a codebase or product with a GitHub repository — the source-type mix (methodology sites, industry bodies, academic press, legal scholarship, independent podcasts) reflects the target, not a shortfall in method.
