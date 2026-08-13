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

## Summary

- **Total distinct projects/sources touched**: ~113 (104 prior + ~9 new source-groups from Batch KIMI).
- **High confidence (full file/primary-artifact read, incl. Stage 2 direct re-verification)**: 16 — Anthropic Skills template, OpenCode Swarm, Kimi-code, Hermes, dsifry/metaswarm, agentic-ceo, plus 10 from Batch AIENG (Building Effective Agents, 12-Factor Agents, anthropics/skills spec, obra/superpowers, Letta v1 agent post, Claude API agent-design.md, Google MCP stateless post, Anthropic Building-Agents-with-Skills post, wshobson/agents, spec-kit).
- **Medium**: ~47 — substantial structured excerpts or official docs, no full primary-artifact fetch.
- **Low**: ~19 — single short snippet or secondary-sourced claim, not cross-checked.
- **Unverified**: 1 category (system-prompt leak repositories — catalogued as a source class, not analyzed).

**Honest reading of this table**: the ratio of High to Medium/Low is small — 6 out of ~56. Most of the Capability Map (`CAPABILITY_MAP.md`) was built from Medium/Low-depth sources, which is exactly the gap flagged in the prior correction. The document-autopsy batch (`CASE`) is the first deliberate push toward High-confidence, full-document reading, and is explicitly a first installment, not a completed pass across the full evidence base. Where the Capability Map cites a Low-confidence project as an example of a mechanism, that citation should be read as "at least one signal of this pattern," not as a fully verified account of that project's actual practice.
