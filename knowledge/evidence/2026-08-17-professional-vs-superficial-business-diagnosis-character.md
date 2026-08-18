# Evidence — What makes business diagnosis/consulting professional vs superficial: behavior, not knowledge (2026-08-17)

task_id: `ENG-2026-08-17-BIZPRODUCER-003`. Direct call from Engineer, criterion fixed before search (see brief). Target: not *what systems exist* (already closed, BIZPRODUCER-001/002) but *what character/manner of work* separates a professional business diagnosis from a superficial/templated one — behavioral rules, not facts about the world, so Engineer can design `SOUL.md`/core Skill for "AI Business Producer" from external practice, not invention.

Source-hierarchy tier noted per claim. Confidence tiers per `METHODOLOGY.md`: Confirmed / Established single-source / Inferred / Unverified.

---

## 1. McKinsey — structured, hypothesis-driven problem solving (Confirmed, primary)

**Source**: official McKinsey Podcast transcript, "How to master the seven-step problem-solving process" (mckinsey.com/capabilities/strategy-and-corporate-finance/our-insights/how-to-master-the-seven-step-problem-solving-process), Charles Conn (co-author, *Bulletproof Problem Solving*, ex-McKinsey partner) and Hugo Sarrazin (McKinsey senior partner) — fetched and read in full directly (Firecrawl, after two direct `WebFetch` attempts on mckinsey.com were blocked by Cloudflare/ECONNRESET; the successful fetch is a full podcast transcript, not a secondary gloss). Level 1-2, official first-party technical content — treated as primary because it is the subject describing its own mechanism in its own words, not a third party's summary of it.

Concrete, quotable behavioral rules (not general advice):

- **Problem definition is checked, not assumed** — "It is surprising how often people jump past this step and make a bunch of assumptions." McKinsey spends disproportionate time writing a precise problem statement (down to "is it an 'or' or an 'and'") specifically because skipping this step is the most common failure they see, including in "especially bright young people [who] run off with half of the idea about what the problem is and start collecting data and start building models — only to discover that they've really gone off half-cocked... in the wrong direction."
- **Prioritize what's important AND movable, not just important** — Conn's Pacific salmon case: ocean conditions were a big lever but not adjustable, so the team deliberately focused on fish habitat and harvesting practices instead, even though ocean conditions "mattered" more in the abstract. Spending analysis time on a factor nobody can act on is named explicitly as a common failure ("people spend a lot of time arguing about branches that are either not important or that none of us can change").
- **Match the depth of the answer to the stakes, and treat an over-built plan as a red flag, not rigor** — "Every time you see a 50-page work plan that stretches out to three months, you know it's wrong. It will be outmoded very quickly." McKinsey explicitly practices a "one-day answer" / "one-hour answer" as a deliberate first pass, then iterates — the elaborate plan is the antipattern, not the goal.
- **Named, specific cognitive biases are checked for on every team, not treated as a personality problem**: *availability bias* (mistaking a familiar past pattern for actual evidence about the current situation — "you think you've seen the problem before, and therefore what's available is your previous conception of it"), and *sunflower/hierarchy bias* (junior team members' judgment suppressed by seniority — McKinsey's stated countermeasure is having the youngest team members speak first, and explicitly asking "this was true in what context?" before reusing a past conclusion in a new situation).
- **State the conclusion's confidence and conditions explicitly, never as flat certainty** — Sarrazin, verbatim: "Often, people lack humility in the way they make their recommendations: 'This is the answer.' They're very precise, and I think we would all be well-served to say, 'This is a likely answer under the following sets of conditions'... you can be explicit about the certainty of your answer when you make that recommendation." This is stated as the corrective to a named, common failure mode (false precision), not as an abstract ideal.
- **A model/algorithm/dataset is never a substitute for a correct problem definition** — explicit warning about applying machine learning without first doing "superb problem solving, starting with good problem definition," and a reminder that algorithms "can have biases built into them" just as earlier statistical models did — stated directly in the context of AI/ML tooling being used for business analysis, not humans only.
- **Analysis is not the answer** — "They've got their analysis, and they assume that's the answer, and of course it isn't the answer." The deliverable is a synthesized story that answers "what should I do," not the raw output of the analysis step; a recommendation that doesn't convert into an actionable decision is treated as an incomplete answer, not a finished one.

## 2. Y Combinator Startup Playbook — evidence over assumption (Confirmed, primary)

**Source**: `playbook.samaltman.com` (the canonical hosted text of YC's official Startup Playbook, linked directly from `ycombinator.com/blog/startup-playbook/`) — fetched and read directly. Level 1, primary artifact.

- **A claim about the business/idea is tested, not asserted** — "The way to test an idea is to either launch it and see what happens or try to sell it (e.g. try to get a letter of intent before you write a line of code.)" For B2B specifically: "one of the first questions we'll ask you is if you have a letter of intent from a customer saying they'll buy what you're building" — a concrete artifact standing in for a claim, not the claim itself.
- **What people say and what people do are tracked as two different signals, not merged** — "Value both what they tell you and what they actually do" — stated together with an explicit caveat against over-trusting either alone (the "faster horses" caveat: people's stated wants are not a reliable guide to what to build, yet talking to users "works surprisingly often" if done right).
- **A forced, non-derivative-looking idea is flagged as a specific failure pattern, not a style choice** — YC's own retrospective on teams they funded without a real idea: "all of them failed" because, lacking genuine conviction, they produced "plausible sounding but derivative ideas." This is offered as evidence of a mechanism (fabricated-sounding diagnosis without real conviction fails), not opinion.

## 3. The Mom Test (Rob Fitzpatrick) — specific past behavior over hypothetical opinion (Established, single-source-type, converged across independent secondary summaries)

**Source**: not fetched from the book/author's own site directly this session (momtestbook.com was not reached); triangulated across three independently-written secondary sources that converge on identical, specific mechanism language — `sachinrekhi.com/p/the-mom-test-rob-fitzpatrick` (fetched in full directly, a named practitioner's own reading notes, not an SEO aggregator), plus corroborating WebSearch snippets from `mtlynch.io` and `blog.uxtweak.com`. Convergent, specific mechanism across 3 independent write-ups of the same primary text → treated as Established, not Confirmed (primary text itself unread this session), but strong enough to use.

- **Opinions and hypotheticals about the future are explicitly excluded as evidence** — "do you think it's a good product idea?" and "would you use this if it existed?" are named as unreliable by construction, because people are "overly optimistic" and want to protect the asker's feelings — not because they're lying maliciously, but because the question *format itself* produces false-positive validation.
- **The substitute is always a question about specific, already-happened behavior** — "Ask about specifics in the past instead of opinions about the future" ("How do you currently solve X?", "When's the last time you tried?", "How much time/money does it cost you now?") — because a person "certainly won't lie about" what they already did.
- **A stated intention is not counted until it costs the person something** — "It's not a real sales lead until you've given them such a concrete chance to reject you" — a letter of intent, a pre-order, a real referral, not a verbal "I'd definitely buy that."

## 4. The Trusted Advisor (Maister, Green, Galford) — honest disagreement over pleasing the client (Established, single-source-type, converged across independent secondary sources)

**Source**: not fetched from the book directly this session; triangulated across independent secondary write-ups converging on the same anecdote and mechanism (trustedadvisor.com/trustmatters, nateliason.com/notes, success-stacks.com). Established, not Confirmed.

- **The advisor's job is named explicitly as "useful," not "right" or "liked"** — the book's own origin anecdote: Maister was fired early in his career for a blunt, accurate diagnosis the client didn't want to hear; the lesson drawn is not "be less honest" but "an advisor's job is not to win the argument but to be useful" — i.e., accuracy alone, delivered without care for how it lands, is also a failure mode, not a virtue by itself.
- **Sometimes the correct diagnosis is "you don't need this"** — cited directly as a trust-building move: a consultant who says "I don't think you need my services right now" is reported as gaining more trust than one who pushes for a sale — an explicit, concrete instance of the diagnosis overriding the diagnoser's own interest.

---

## What was checked and not found (honest gap, not filled with impression)

- No primary-source-verified claim was found specifically about *AI tools* (not human consultants) doing business diagnosis well or badly, distinct from the general AI-hallucination literature. A search for "AI business strategy tool generic/hallucination/overconfident" returned only generic AI-hallucination content-marketing pages (level 4-5, SEO-style, not specific to business diagnosis) — explicitly **not used** as evidence for any claim above; this gap is named, not smoothed over. The behavioral principles above are therefore sourced from human consulting/accelerator/advisory practice, per the brief's explicit permission ("методология консалтинга/бизнес-акселераторов/YC-подобных программ, ИЛИ..." — either family was acceptable), not from AI-specific practice.
- Peter Block's *Flawless Consulting* ("consultant is not the expert who prescribes, but a partner in diagnosis," "authentic contracting") was found and is directionally consistent with the Maister material above, but was not pursued to the same depth — redundant with the Maister finding once found, per Principle P6 (stop collecting once a source stops adding new information).

---

## Decision-ready synthesis (also see final report to Engineer)

**3-5 behavioral principles, directly SOUL.md-shaped:**

1. Separate stated fact from working hypothesis visibly, at all times — an assumption is never silently promoted to a settled input. (McKinsey: hypothesis-driven method, explicit fact-base-building against a hypothesis.)
2. Every conclusion carries its own confidence and the conditions under which it holds — never a flat "this is the answer." (McKinsey, Sarrazin, verbatim quote above.)
3. Prioritize analysis effort on what is both important *and* changeable by the owner right now — not everything that matters is worth analyzing today. (McKinsey, Pacific salmon case.)
4. Validate a business claim (about the market, the owner's own past attempts, a customer's interest) against specific past behavior or a concrete costly commitment — never against a hypothetical opinion or a compliment. (The Mom Test; YC's letter-of-intent bar.)
5. Be willing to state the unwelcome diagnosis, including "you don't need this," rather than soften it to keep the owner comfortable — usefulness, not agreement, is the job. (Trusted Advisor.)

**2-3 named antipatterns, each with source:**

1. Skipping explicit problem definition and jumping straight to data-gathering/solutioning on an unexamined assumption — McKinsey names this as the most common failure they see, including in their own best people ("gone off half-cocked... in the wrong direction").
2. False precision — delivering a flat, unconditioned "this is the answer" instead of naming the conditions and confidence behind it — McKinsey, named directly as a lack of humility that recurs.
3. Treating hypothetical or opinion-based responses ("would you buy this," "sounds like a good idea") as if they were evidence, instead of demanding a costly commitment or a fact about specific past behavior — The Mom Test's central, named failure mode, with YC's letter-of-intent bar as the accelerator-world equivalent.

Not designed here: `SOUL.md` or Skill content itself — that decision and its wording stay with Engineer, per `MISSION.md`'s Craft/Engineering boundary.
