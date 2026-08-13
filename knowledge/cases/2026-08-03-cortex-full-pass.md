# Case — Jmeg8r/cortex (was As-The-Geek-Learns/cortex), full workflow pass

Researched by a background subagent (States 1–4, 13 documents fully read, verified via the full 172-file repository tree — repo ownership change confirmed via GitHub API), integrated here (States 5–7).

## State 1 — Selected

**Category**: maturity + unique architecture. **Fact**: a research paper, a failure-analysis document, a paired external-evaluation-plus-response, and a MASTER-PLAN — an unusually complete first-person documentation trail for a personal project, including two contradiction findings the project surfaced about itself.

## State 4 — Analyzed (selected mechanisms)

1. **Mechanism**: tiered-permanence memory — every decision event is kept permanently at the storage layer (decay_rate = 1.0), while its *default-view inclusion* is tiered active/aging/archived, with automatic promotion back to active on access. **Why it works**: resolves "never lose a decision" vs. "never overflow the token budget" by treating storage permanence and default-view inclusion as two independent knobs rather than one. **Trade-off**: requires a promotion/demotion mechanism that must itself be kept correct.

2. **Mechanism**: adoption/UX friction scored with the same Likelihood×Impact rubric as technical risk — "setup complexity deters adoption" was tied for the single highest score across a 19-mode risk analysis. **Why it works**: treats a soft, often-unscored risk category with the same rigor as a hard, technical one, surfacing it as a top priority instead of an afterthought.

3. **Mechanism**: the project's own "external evaluation" document, on inspection, discloses no reviewer identity or organization distinguishing it from a same-author, same-tool adversarial re-prompt — the label claims more independence than the artifact substantiates. The critique's actual content was genuinely useful despite this.

### Contradiction question — mandatory

Two things: (1) `CAPABILITY_MAP.md`'s Learning section previously cited this project's "blameless post-mortem culture applied to the method itself" as confirming an already-established pattern — this pass confirms that framing still holds. (2) the paired "external evaluation" + "evaluation response" documents are a real-world instance of this project's own Double-Loop Review mechanism (`REVIEW_LOOP.md`) — and a direct, concrete confirmation of that section's own stated limitation: the "external" evaluator's independence from the author/tooling is asserted, not verifiable from the repository, which is exactly the "single-agent self-review lacks diversity-of-perspective" caveat already written into that section.

## State 6 — Extracted

**Transfer**: tiered-permanence memory as a named pattern (permanence and default-view inclusion as independent knobs). **Transfer**: adoption-risk-scored-like-technical-risk, as a general research-quality principle. **Transfer, most important**: a sharpened anti-pattern under Review — verify a claimed review's actual independence (reviewer identity, tooling separation) before crediting it as strong corroborating evidence, rather than accepting the project's own label of "external."

**Do not transfer**: the specific three-tier complexity rollout (Tier 0–3) — a good idea for this project's own adoption curve, not a universal principle; the specific git/package-manifest reality-check implementation — the technique (structured-data cross-check) transfers, the specific manifest-parsing code does not.

**Confidence**: High (13 fully-read documents, verified file tree, cross-checked repository identity change).

## State 7 — Capability Map update

Confirmations filed: Jmeg8r/cortex added as a source for patterns E, F, N in `CAPABILITY_MAP.md`, and explicitly cited as real-world validation of `REVIEW_LOOP.md`'s Double-Loop Review limitation clause. Candidates merged directly into `CAPABILITY_MAP.md` as single-source findings: tiered-permanence memory (immortal event + projection tiering, Capability 1), adoption-risk-scored-like-technical-risk (Capability 10), and — most important — a sharpened anti-pattern under Capability 5 requiring verification of claimed review independence before crediting it as corroborating evidence.
