# Case — brcrusoe72/agentic-ceo, full workflow pass

Researched by a background subagent (States 1–4), integrated here (States 5–7).

## State 1 — Selected

**Category**: unusual idea + maturity signal. **Fact**: a "Wolf/Jackal" directed-then-undirected two-pass research pattern with a fixed phase budget (Stalk 15% → Test Bite 20% → Kill 50% → Feed 10%), a Critic/Observer/Evolver self-tuning loop, and a first-person retrospective naming specific real failures — not a marketing page.

## State 2 — Document Inventory

Full 14-category inventory completed by the background subagent; all categories marked. Notably: no ADR folder, no formal permission-system document, but an extensive `docs/DEEP_DIVE.md` and `docs/retrospective.md`.

## State 3 — Reading

9 documents fully read end-to-end, plus 2 source files (`critic.py`, `orchestrator.py`) exhaustively searched for specific claims (not just skimmed).

## State 4 — Analyzed

1. **Mechanism**: Wolf/Jackal two-pass research — a first "Wolf" pass with a fixed, directed research plan, followed by a second "Jackal" pass that explores undirected, opportunistic leads the Wolf pass didn't anticipate. **Why it works**: directed research alone misses adjacent, unplanned findings; undirected research alone lacks focus and burns budget. Splitting the passes gets both. **Trade-off**: doubles the number of passes required per research unit.

2. **Mechanism**: fixed phase-budget allocation (Stalk 15% / Test Bite 20% / Kill 50% / Feed 10%) forces the system into synthesis ("Feed") regardless of how tempting further collection remains. **Why it works**: without a forced transition, collection tends to expand to fill all available time/budget. **Trade-off**: the specific percentages are tuned to this project's own cost model, not universal.

3. **Mechanism (headline claim, verified against source)**: the project's own documentation and retrospective describe a Critic agent that downgrades "23%" of high-rated frameworks using a 0.9 confidence threshold. A full-text search of `critic.py` found no such figure, no confidence field, and no threshold check anywhere in the actual implementation. **Why this matters**: narrative depth (a detailed, technical-sounding retrospective) was mistaken for verification depth. The qualitative claim — a Critic role with an adversarially-framed prompt exists and runs — remains true; the specific number does not exist in code.

### Contradiction question — mandatory

Two things: (1) the project's own retrospective explicitly frames "almost cut the Critic to save cost" as a real, nearly-made decision — direct real-world evidence that a dedicated adversarial-review role is not self-evidently worth its cost even to the people who built it. (2) the 23% figure, once traced to source, turned out unverifiable — a direct instance of this project's own Stage 2 (Verification) requirement to check a primary implementation artifact, not just a description of it.

**Correction to prior citations (this is the important part)**: this project was previously logged in `CAPABILITY_MAP.md` (pattern W, Review/Learning) citing its Critic and Observer+Evolver loop as evidence that "a dedicated adversarial role pays for itself," based entirely on the project's own narrative. That qualitative claim (a critic role exists, with an adversarial-framed prompt) remains true — `critic.py` does exist and does implement a `critique()` function. But the specific, quantitative claim used to justify *why* it pays for itself (the 23% figure) is now known to be uncorroborated by the actual code. **`EVIDENCE_INDEX.md`'s "High" confidence rating for agentic-ceo is downgraded to Medium** for any claim not specifically re-verified in this pass — depth of narrative was previously mistaken for depth of verification, which is exactly the gap this whole re-run discipline exists to catch.

## State 6 — Extracted

**Transfer**: the Wolf/Jackal directed/undirected two-pass pattern, as a cheap addition to any single-pass research step. **Transfer, most important**: before crediting any documented mechanism as real, verify the corresponding source file actually exists and actually implements the claimed behavior — a documented "agent" or "threshold" is a claim, not a fact, until the code is checked. This directly sharpens this skill's own Reading (State 3) discipline: "fully read" should mean the primary *implementation*, not only the primary *description*, wherever an implementation exists to check against.

**Do not transfer**: the specific budget percentages (5/15/20/50/10) — tuned for this project's own cost model, not a universal ratio.

**Confidence**: High for the two source-code-verified findings (2, 3, and the central contradiction); Medium for the rest (real documents, not independently re-derived from code).

## State 7 — Capability Map update

`CAPABILITY_MAP.md`'s pattern-T entry: strengthened (Jackal addition, quantified test-bite-abandon rate). Pattern-W entry: **caveat added** — the specific "23% downgrade" claim is unverified-in-code, not evidence, only a narrated claim; the qualitative existence of an adversarial critic role stands. The generalized rule (verify code existence before crediting a documented mechanism as implemented) is promoted directly into `skills/reverse-engineering/METHODOLOGY.md`, Stage 2 — it had a second independent confirming instance in the same batch (os-tack/ostk.ai's self-contradicting license, see that project's case file), clearing this skill's own P3 bar for a permanent addition rather than a staged candidate.

**State: Done.**
