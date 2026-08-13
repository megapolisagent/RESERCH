# Evidence log — Stage 0A batch 2: OpenAI System Cards, Model Cards, Cloudflare, Microsoft Research, Anthropic

Date: 2026-08-03. Second batch of world-practices research (technical investigation disciplines), following the same stopping rule as batch 1 — closed once a source class stops yielding a mechanism not already captured.

## OpenAI System Cards
Structured, quantitative, comparative capability+risk reporting, explicitly benchmarked against the previous model version, with reported confidence intervals. **Transferable to AI_OS?** A named-template discipline for reporting capability + limitation together, benchmarked against a prior baseline rather than in isolation — relevant to how this skill's own Judgment stage should compare a new finding against the current state of the receiving system, not just describe it standalone.

## Mitchell et al., Model Cards (2019)
Standardized documentation template: Model Details / Intended Use / Factors / Metrics / Evaluation Data / Training Data / Quantitative Analyses / Ethical Considerations and Caveats and Recommendations.

Possible mechanism not seen in batch 1: a named, reusable documentation *template* (fixed sections) for capability + limitation + intended-use reporting, including a specific "Caveats and Recommendations" section. Partial overlap flagged, not resolved: this may be a partial existing analog to Definition-of-Done conditions 4/5 (transferable capability / what not to transfer) in `skills/reverse-engineering/METHODOLOGY.md`, which are currently tagged `original` there — Model Cards' "Intended Use" and "Caveats" sections address *where a model should/shouldn't be used*, which is related to but not identical to *whether a capability should be transplanted into a different system*. Needs a deliberate check before any tag is changed — not decided here.

## Cloudflare postmortems / Health Mediated Deployments
Controlled, metric-gated rollout with automatic revert, applied to configuration changes with the same discipline as software releases, after a real incident exposed the gap between the two. **Transferable to AI_OS?** The general discipline of applying the same rigor to configuration/process changes as to code changes — relevant to how this skill's own methodology changes should be gated, not just code.

## Microsoft Research — measurement validity
"Shared Standard for Valid Measurement": systematize → operationalize → apply. Checking whether a metric actually measures the claimed construct is a distinct question from checking where the evidence for the metric came from (source-hierarchy verification). **Observation 8**: a candidate addition to Stage 2 (Verification), distinct from source-hierarchy checking — does the metric/evidence actually measure the claimed thing, not just where it came from. Logged as a real, named discipline; not yet incorporated as a methodology rule.

## Anthropic — RSP, Alignment Stress Testing, "Reflections"
A standing, proactive adversarial function whose job is to actively try to break an organization's own safety/methodology rules before failures occur in the wild — distinct from a retrospective review that only runs after a batch of cases. Also: Anthropic's own "Reflections" document is a real instance of blameless post-mortem culture applied to a policy/methodology document itself, not only to an incident. **Observation 9**: a candidate for a standing (not only retrospective) adversarial stress-test function for this skill's own methodology — distinct from Evidence Review, which only runs after cases have already happened.

## Summary
Two candidate additions surfaced but not incorporated in this pass, per the stopping-rule discipline (log the observation, don't force it into a rule before it's actually needed): a measurement-validity check as a Verification sub-step (Observation 8), and a standing adversarial stress-test of the methodology itself, distinct from retrospective Evidence Review (Observation 9).
