# Evidence — "AI Business Producer" category: real systems that analyze a business and coordinate specialist AI agents by business function

task_id: ENG-2026-08-17-BIZPRODUCER-001. Requested by Engineer as the World Research step inside `idea-calibration` (gate result: Confidence Low) for a new agent concept, working name "AI Business Producer." Question is domain-specific: does this category of system exist in the real world (not concept/pitch-deck), what's the mechanism, what specializations recur, what's the real-production/demo ratio. The general orchestrator↔specialist mechanical pattern was already closed separately (`OPEN_QUESTIONS.md`, 2026-08-12) — not repeated here.

Pre-task check (per `instructions/pre-task-check.md`): criterion already fixed by Engineer before this search began (the 5-point brief itself is the criterion) — no question asked back, no new decision surfaced that needed the owner's word.

## Source-type checklist

- Web (semantic search, `mcp__exa__web_search_exa`) — found and read (16+ product landing pages, one independent product-analysis blog, one independent app-review aggregator, one independent tech-news write-up).
- GitHub (`gh`/raw API, stars/activity as an adoption proxy) — found and read for 7 repos (MetaGPT, ChatDev, Soleur, and 4 smaller "software company simulator" clones).
- Official documentation/product pages — found and read directly (`WebFetch` on goodhelp.ai; Exa full-page fetch on aqen.ai, voraiq.com, cofounder.co).
- Independent write-ups — found: usecarly.com (Cofounder.co teardown), currlyai.com + aitoolsclub.com (Cofounder.co), apprecs.com (Vora IQ App Store review aggregation, third-party).
- Academic papers — not fetched directly this session; MetaGPT (ICLR 2024) and ChatDev (ACL 2024) are referenced by their own repos as published, not independently re-verified via arXiv this session — flagged, not silently upgraded.
- Reddit/Hacker News/Discord/YouTube — not investigated this session (time-boxed to the fixed criterion; the source-type checklist records this honestly rather than omitting it).

## Candidates found, sorted by verification strength

### Tier 1 — real, independently corroborated production usage, mechanism read from the primary source

**Cofounder.co / "Cofounder 2"** (The General Intelligence Company, founder Andrew Pignanelli, New York)
- **Funding**: $8.7M seed, Union Square Ventures + Acrew Capital, announced Dec 2025 (independent tech-news source, aitoolsclub.com write-up) — a funding-round claim is still a claim, not a code artifact, so this stays at "reported by independent secondary source," not "Confirmed" in the strict source-hierarchy sense; no press-release/Crunchbase cross-check was done this session.
- **Reported usage**: "over 10,650 companies running on it" — stated by an independent teardown blog (usecarly.com), not the vendor's own copy. Single independent source, not cross-corroborated by a second one this session.
- **Input**: a founder's idea/goal; an onboarding "guide" conversation.
- **Mechanism**: Cofounder itself is a "superoptimizer" (manager agent) that delegates across departments — engineering, sales, marketing, design (confirmed in-product); ops/support/finance referenced in marketing copy but not independently confirmed as live department types. Each department has a manager + specialist agents sharing context ("marketing knows what engineering shipped" — usecarly.com's phrasing of the shared-context claim, not independently verified against actual multi-department output).
- **Output**: a company-specific roadmap; concrete shipped artifacts — live sites (domain purchase + hosting on paid tier), marketing campaigns, sales outreach/inbox warming, Stripe payment setup, customer support handling.
- **Task handoff**: user picks which work streams to hand off; departmental managers assign to specialist agents.
- **Verification/review**: explicit human-in-the-loop gate before "potentially dangerous actions"; agent-built previews/preview environments exist before anything goes live; an explicit data-export path ("graduate data from the platform") — independent teardown calls this out as meaningfully reducing lock-in risk, one of the few skeptical/critical independent assessments found in this whole search.
- **Decision-maker**: human founder approves risky actions; agent executes routine/lower-risk work autonomously.
- **What it is NOT**: not a business-structuring/legal-entity/company-formation analyzer — the "roadmap" step is closer to a project-execution plan (what to build/ship next) than to "разбор бизнеса до структуры компании" in the legal/financial-structure sense. That specific capability (entity formation, cap table, compliance calendar) was not found in Cofounder's own product copy — flagged as absent, not assumed.

**MetaGPT** (FoundationAgents/metagpt, GitHub) and **ChatDev** (OpenBMB/ChatDev, GitHub)
- **Adoption signal** (checked directly, `api.github.com`, this session): MetaGPT — 69,865 stars, 8,883 forks, last push 2026-01-21, not archived, 129 open issues (active maintenance signal). ChatDev — 34,011 stars, 4,246 forks, last push 2026-07-24, not archived, 67 open issues.
- **Mechanism** (read from each project's own README, source-hierarchy level 1): MetaGPT assigns LLM-based roles (product manager / architect / project manager / engineer) organized around explicit SOPs ("Code = SOP(Team)"), takes a one-line requirement, and outputs user stories / competitive analysis / requirements / data structures / APIs / documents. ChatDev (1.0, the original virtual-software-company mode) runs CEO/CTO/Programmer/Tester-style roles through "specialized functional seminars," covering design → code → test → document; ChatDev was also relaunched as a hosted SaaS (chatdev.modelbest.cn per its own changelog) and has since evolved into "ChatDev 2.0/DevAll," a general-purpose no-code multi-agent configuration platform, not only the original software-company simulation.
- **Real production signal**: both are open-source with sustained multi-year adoption at a scale (tens of thousands of stars, thousands of forks, recent commits) that is a strong, checkable proxy for "genuinely used," not a demo abandoned after launch. Both underpin published, peer-reviewed papers (MetaGPT — ICLR 2024; ChatDev — ACL 2024, per their own repos) — paper venues not independently re-verified via arXiv this session, flagged.
- **What this is NOT**: general business analysis. Both simulate a *software* company producing a *software* product from a one-line spec — the "specialization" is around the software delivery lifecycle (PM/architect/engineer/QA), not business functions like market research, finance, or legal structure. Relevant to this investigation only as the strongest evidence that "named business-role personas + SOP-defined handoffs + a review step" is a real, working, widely-adopted mechanism in a narrower domain — not evidence that the *general business* version of this idea is equally proven.

### Tier 2 — real, small-scale, independently corroborated but far smaller scale

**Vora IQ** (voraiq.com, Vora IQ Inc, West Hollywood, founded 2024, LinkedIn: 1–10 employees, distributed US/Pakistan)
- **Input**: an idea (text) or an existing plan document/pasted text.
- **Mechanism**: extracts business model/market/financials/goals into a "Business Context Layer" (BCL) shared by 13 named agents — 7 that execute ("doers") + 6 that judge/advise. Doers include: **Axis** (turns validated idea into a build plan tuned for Lovable/Replit/Claude Code — 10 sections, 4 build stages), **Ledger** (CFO — connects live to Stripe, models runway/unit economics, and **hard-refuses** to green-light scaling if LTV:CAC < 3:1 or runway < 6 months — a coded business-logic veto, not just an LLM opinion), **Scribe** (pulls real BCL numbers into investor decks/board memos, explicitly "not made up"), **Apollo** (Head of Growth — finds real organizations via web search, drafts outreach, **review-first: nothing sends until human approves**), **Insight** (Head of Research — biweekly market/competitor/legal/risk sweeps, every claim cited to a source). Advisors: Vibe (CMO), Shield (General Counsel), Pivot (CSO), Pulse (COO), Reflect (Executive Coach), Forge (CPO).
- **Output**: a 5-dimension viability score → a living, re-prioritized roadmap with daily tasks; investor decks; outreach campaigns; market-signal briefings.
- **Task handoff/coherence**: every agent reads/writes the same BCL, so one agent's finding propagates automatically (Ledger's runway flag → Scribe's board update, per the product's own worked example).
- **Verification**: hard-coded numeric gates (Ledger) + explicit human-approval-before-send (Apollo) + a stated 7-day output-rejection/refund window.
- **Decision-maker**: explicit in the product's own FAQ — "You stay the decision-maker while the system reduces operational drag."
- **Independent corroboration** (not the vendor's own copy): App Store reviews on a third-party aggregator (apprecs.com) — genuine user-voice reviews, not vendor testimonials; a live, self-published metrics page showing real (small) numbers — 240 total web users, –$13,432.02 YTD revenue, $0 CAC, explicitly "pre-profitable" (a company publishing its own weak numbers is a different, stronger evidentiary posture than a vendor only publishing wins — noted as a positive signal for honesty, not for scale); a "Cohort One — Founding 50" program (50 real founders, 60-day free access).
- **Verdict**: small scale, but genuinely operating with real users and a checkable (if modest) real-usage footprint — not a pitch-deck-only concept.

### Tier 3 — real but thin/self-referential evidence

**GoodHelp** (goodhelp.ai)
- **Mechanism** (read directly, `WebFetch`): pick a department template (CFO, CMO, CRO, CTO, Support, Ops); a standing orchestrator ("Hopper") is included per org; each agent has a per-agent allow-list of tools/data, a cost ceiling, an egress allow-list, and approval thresholds.
- **Verification**: financial actions explicitly stated as "private beta and human-approved — never on autopilot"; tamper-evident, timestamped action log described as "auditor-grade evidence"; outputs reviewable, 7-day reject/refund.
- **Decision-maker**: human approves above threshold; agent proposes.
- **Production evidence**: one concrete, falsifiable, named case — the vendor's own company, LMNTL, reportedly replaced a departing COO's role with agents covering "53 of 53" responsibilities in "~8 engineer-days," and runs "17 production agents" on its own operations (marketing, research, finance, ops). This is a real, specific, checkable-in-principle claim — but it is about the vendor's *own* company, not a third-party customer, and no independent corroboration or named external customer was found this session. Kept at "vendor-reported, self-referential" rather than promoted to independently-confirmed.

### Tier 4 — explicit pre-launch / not yet real users (self-declared by the product itself)

**Aqen** (aqen.ai) — solo-founder side project (Duncan Grazier, ex-BuildOps CAIO, "TideHelm"/"Grazier Ventures"), publicly and explicitly "in closed beta... join the waitlist to be considered" on its own homepage. Mechanism as described (not yet verifiable against real users): captures a founder's intent as a "Charter," decomposes into a "Blueprint" across nine business domains (formation & legal, finance & capital, GTM, marketing, product development & validation, branding, operations, people/hiring, compliance), sequences dependencies, runs each step as a "Work Order," specialist agents work in parallel per domain, coordinate through a shared "Brain." This is the single closest match in the entire search to "разбор бизнеса до структуры компании" in the legal/entity-formation sense (explicit "entity formation," "cap table," "compliance calendar," "EIN filing") — but by the product's own admission it has no proven users yet. Kept as a mechanism description with an explicit unproven-usage flag, not discarded — the domain-decomposition idea itself (nine business domains, dependency-sequenced) is a real, specific design even though the product behind it is pre-launch.

**GForce** (gforce.cloud) and **Syzygia** (syzygia.io) — both explicitly "waitlist"/"early access, onboarding in small groups" on their own homepages. Not investigated further.

### Tier 5 — landing pages found, mechanism-level claims present, no independent usage evidence found or sought this session (honest gap, not "proven fake")

RootEntity, StartCaaS, Soleur (13 GitHub stars — source-available but low adoption), CapiBot, AgentCorp, Uuple, Opscale, IncAgent, Preplix — each makes specific mechanism claims (named departments/agents, shared context, approval gates) matching the same pattern as Tiers 1–3, but no independent (non-vendor) usage evidence was found for any of them in this session's search depth. This is stated as an honest "not investigated to that depth," per Definition of Done condition 8 — not evidence they are fake, and not evidence they are real at scale.

### Abandoned/near-zero-adoption open-source clones (checked directly via GitHub API, confirms the demo-proliferation signal)

- `ES7/AI-Software-Company-Simulator` — 0 stars, single push 2026-04-24, not archived (never gained a user).
- `Caoquyen1913/ai-outsourcing-studio` — 2 stars.
- `vedanta/the-system` ("ASDO," 26 agents/6 departments claimed) — 9 stars.
- `msoedov/mesa` (Linear-style board, CEO agent, "zero-human company") — 68 stars.

Contrast with MetaGPT (69,865) / ChatDev (34,011): the ratio between the two established, paper-backed, actively-maintained projects and the four independent from-scratch clones is roughly three to four orders of magnitude in adoption — a direct, checkable signal that this specific idea ("simulate a company's roles as coordinated LLM agents") is easy to prototype and attracts many independent solo attempts, almost none of which gain real users, and the ones that did (MetaGPT, ChatDev) did so on the narrower software-company version of the idea, not the general-business version.

## Specializations/roles actually observed across all candidates (not invented)

Compiled from the mechanism-level read of every Tier 1–4 candidate plus the mechanism claims of Tier 5 (listed, not double-counted as verified):

**Converges in nearly every system found** (present in ≥8 of the ~16 named products): Marketing/Growth (CMO), Finance/Accounting (CFO), Sales/GTM/Revenue (CRO), Operations (COO), Legal/Compliance (General Counsel), Product/Engineering (CTO/CPO), Customer Support/Success.

**Recurs but less universally**: HR/People/Recruiting/Onboarding (Uuple, Preplix, IncAgent, Aqen's "people" domain); Strategy/"Chief Strategy Officer" as a distinct role from Finance or Ops (Vora IQ's Pivot, GoodHelp's "Ops/Strategy" bucket); Research/market-intelligence as its own standing role, distinct from a one-off "market analysis" step (Vora IQ's Insight — biweekly sweeps with cited sources; GoodHelp's competitor/audience profiling); Documentation/investor-relations as its own role (Vora IQ's Scribe — pulls real numbers into decks/memos); an "Executive Coach" role focused on the founder's own judgment rather than a business function (Vora IQ's Reflect — the one outlier that is not a business-function specialist at all, worth naming explicitly since it doesn't fit the rest of the pattern).

**Not found anywhere in this search**: a distinct "legal *structure*/entity-formation" specialist separate from general "Legal/Compliance" — only Aqen names entity formation, EIN, cap table, compliance calendar as explicit deliverables; everyone else's "Legal" role is compliance/contract-review-shaped, not company-formation-shaped. This is a real, specific gap worth naming rather than smoothing over: "company structure" in the literal legal-entity sense is the least-covered function among all specializations found.

## Overengineering / real-production signal (point 3 of the brief)

Of the ~16 named "business producer"-type products surfaced by search this session:
- **3 have independently-corroborated evidence of real usage** beyond the vendor's own marketing copy (Cofounder.co — funded + independent usage-count claim; Vora IQ — independent App Store reviews + self-published, unflattering-enough-to-be-credible metrics; GoodHelp — one specific, falsifiable but self-referential production case).
- **3 explicitly self-declare pre-launch/waitlist status** on their own homepage (Aqen, GForce, Syzygia) — not a judgment call, their own words.
- **9 remain unverified either way** in this session's depth — landing pages with specific mechanism claims, no corroborating or disconfirming evidence found.
- Separately, in the open-source/GitHub-verifiable segment: **2 established, paper-backed, actively-maintained projects** (MetaGPT, ChatDev) against **4 independent from-scratch clones with 0–68 stars** — a concrete, direct measurement (not an impression) of how much of this specific idea-space is prototype/demo relative to what actually gained traction, though note the two winners are scoped to software delivery, not general business.

Honest reading: this is a hot, actively-explored idea space right now (August 2026) with a wide spread of maturity — from a funded, seed-stage company reporting five-figure customer counts (Cofounder.co) down to solo-founder waitlist pages — but very little of it is old enough or independently audited enough to call "settled practice." No source found in this session claims a mature, multi-year-proven version of the *general business* case (as opposed to the *software-company* case, which is mature and proven).

## What transfers to Engineer's case vs. what requires infrastructure not currently held

Per the brief: Engineer already has one proven mechanism — a background agent invoked with a narrow brief and a fixed-before-search sufficiency criterion, where Engineer (not the worker) owns checking the result against that criterion (`ENGINEER/COMMUNICATION.md`).

- **Transfers, already structurally present**: the core coordination shape used by every Tier 1–3 candidate — a manager/coordinator delegates a scoped unit of work to a specialist, the specialist's output is checked against a standard before being accepted, a human (or in Cofounder.co's case, an approval gate) makes the call on anything risky — is the same shape as Engineer↔Researcher's already-verified call. Vora IQ's "shared context layer every specialist reads/writes so decisions don't conflict" is conceptually the same problem Engineer/Researcher already solve with shared markdown files (`DECISIONS.md`, `OPEN_QUESTIONS.md`) as the common reference — not a new capability, an existing one under a different name.
- **Does not transfer without new infrastructure**: (1) hard-coded, live-data-driven business-logic gates like Vora IQ's Ledger (an automated refusal tied to a real Stripe feed, not an LLM judgment call) — this requires an actual live financial-data integration Engineer does not have; (2) continuous/standing background execution across many specialist agents running in parallel with their own tool access (Cofounder.co's departments, GoodHelp's Hopper-orchestrated org) — a materially different infrastructure order than "call one background agent once with a brief and read back its answer," which is Engineer's current, single-shot pattern; (3) any live external tool/API integration (CRM, banking, Stripe, calendar) — none of the systems reviewed do meaningful business coordination without at least one such live integration, and Engineer/Researcher's proven channel today is file-based, not tool-integrated.
- Not assessed here (explicitly out of scope per the brief, Craft/Engineering boundary): whether Business Producer should be built, in what shape, or in what order relative to other work — that is Engineer's/the owner's decision, not this file's.

## Sources

- github.com/foundationagents/metagpt (README, fetched via search; stars/activity via `api.github.com`, fetched directly)
- github.com/OpenBMB/ChatDev (README, fetched via search; stars/activity via `api.github.com`, fetched directly)
- github.com/ES7/AI-Software-Company-Simulator, github.com/Caoquyen1913/ai-outsourcing-studio, github.com/vedanta/the-system, github.com/msoedov/mesa (stars/activity via `api.github.com`, fetched directly)
- aqen.ai, aqen.ai/product (homepage + product page, fetched via search)
- itsmeduncan.com/2026/05/05/the-builders-bet (founder's own blog, independent of the product page but same author — level 4, self-report)
- linkedin.com/in/itsmeduncan (founder's public profile, fetched via search)
- voraiq.com, voraiq.com/pricing, voraiq.com/agents, voraiq.com/live-metrics, voraiq.com/reviews (fetched via search)
- apprecs.com/ios/6736479518/vora-iq (independent third-party App Store review aggregator)
- goodhelp.ai (fetched directly, `WebFetch`)
- cofounder.co, cofounder.co/resources/introducing-cofounder-2 (fetched via search)
- usecarly.com/blog/cofounder-ai (independent product teardown, fetched via search)
- currlyai.com/tool/cofounder-agentic-company-os, aitoolsclub.com/meet-cofounder-a-platform-that-lets-you-run-an-entire-company-with-ai-agents (independent write-ups, fetched via search)
- rootentity.com, startcaas.com, soleur.ai/agents, capibot.io, agentcorp.work, gforce.cloud, uuple.com, opscale.io, syzygia.io, incagent.ai, preplix.ai (homepages, fetched via search — Tier 4/5, mechanism claims recorded, usage not independently corroborated)
