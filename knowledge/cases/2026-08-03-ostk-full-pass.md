# Case — os-tack/ostk.ai, full workflow pass

Researched by a background subagent (States 1–4, extended to the companion `ostk-site` docs and org repos since the project ships docs off-repo). Integrated here (States 5–7).

## State 1 — Selected

**Category**: unique architecture + unusual idea — a POSIX kernel spec (RFC 2119, numbered invariants, formal conformance section) reimplementing process/ownership/signal semantics in userspace for AI-agent coordination; a Dual-CPU scheduler (human = Ring 0, LLM = Ring 3). **Sharpened fact**: the repo's own `LICENSE` file directly contradicts its own `README.md`'s license claim, independently confirmed by GitHub's SPDX detector siding with the LICENSE file — an unusually rare, directly-caught self-contradiction on a project's own primary artifact.

## State 2 — Document Inventory (verified against the repo tree + companion site + org repo list, not guessed)

| Category | Status |
|---|---|
| AGENT.md/AGENTS.md | ❌ Confirmed absent (nearest analog, `Agentfile`, is a per-process launch manifest, not a repo-wide instructions file — not counted) |
| CLAUDE.md | ❌ Confirmed absent |
| SKILL.md | ❌ Confirmed absent |
| README | ✅ Exists |
| ADR | ❌ Confirmed absent (`GENESIS.md` is a one-time ceremonial identity attestation, not a recurring decision-log format — not counted) |
| Templates | ✅ Exists (`HUMANFILE`/`ENTITYFILE`, shipped reference instances; authoring source lives in a private companion repo) |
| Memory | ✅ Exists (five append-only logs; registries as memoized projections) |
| Prompts | ❌ Confirmed absent |
| Evaluation | ❌ Confirmed absent in-project (a sibling public repo, `find-the-needle`, serves this role but is outside the assigned project boundary) |
| Workflow | ✅ Exists (Five Laws + seven-step approval chain + lifecycle states) |
| Architecture | ✅ Exists |
| Hooks | ✅ Exists (`ostk hook` CLI, near-exact taxonomy match to Claude Code's own hook events) |
| Tests | 📄 Not published (cited by specific line ranges in the spec; actual source tree confirmed private, 404 on direct query) |
| Permissions | ✅ Exists — the most thoroughly documented category in this project |

14/14 marked.

## State 3 — Reading

Ten documents fully read end-to-end (README, POSIX kernel spec, security/architecture/coordination-primitives docs, AUTHORIZATION.md, GENESIS.md, ENTITYFILE, HUMANFILE, LICENSE). Several large site pages logged as partially read or explicitly not read (one file, 326KB, explicitly skipped as too large for this pass's budget — a logged reason, not silently dropped).

## State 4 — Analyzed (10 mechanisms; full detail in the subagent's report)

1. Ownership-by-liveness double-check (`kill_zero` AND recorded start-time match) — defeats PID-reuse, fails closed when unverifiable.
2. Atomic reap-not-delete via same-filesystem `rename(2)` into a graveyard directory — cheap crash-safety, at the cost of a hard single-filesystem deployment constraint.
3. Closed, numbered coordination-signal table over a Unix domain socket, explicitly not OS signals — avoids async-signal-safety limits, at the cost of anything unanticipated needing a spec revision.
4. Per-response (not just per-handshake) anchor-epoch fencing token — closes a narrower race than handshake-only fencing; transparent reconnect explicitly not yet shipped.
5. Handle-generation counters generalizing the PID-reuse defense to every reusable identifier — nothing in the type system stops a caller from skipping the re-validation check.
6. Tier-floor capability pins that compose by **intersection, not override** — most-restrictive-wins across two independent policy sources, a materially different rule from an ordered first-match deny/ask/allow list.
7. Empirical permission bounding (`ostk learn`) — observes a real run, emits a minimal grant from what was actually exercised, at the cost of denying any rarely-taken path the observation window missed.
8. Three-tier CAS conflict resolution on kernel-mediated edits (auto-merge / suggest / reject) — applies only through the kernel's own file-op path; bypassing tools lose the guarantee silently.
9. `GENESIS.md`'s dual-signed "birth attestation" — flagged explicitly as an unverified, level-4/5 self-report despite its technical styling.
10. Signed-binary-only distribution as a substitute for source availability — a supply-chain trust model, not a read-the-code trust model; the project's own "auditable infrastructure" language is not exercisable by an outsider for the kernel itself.

### Contradiction findings

1. **`CAPABILITY_MAP.md` has no category for this project's actual center of gravity.** Event sourcing (already logged, Capability 1) is real but is one of seven co-equal invariants; the more differentiated content — ownership/reaping/fencing/signal-table discipline, i.e. a full userspace reimplementation of *process lifecycle*, not of *durable recall* — has no home in the current ten-capability taxonomy. Capability 3 (Reasoning/Determinism Boundary) is the nearest bucket and doesn't really cover it either.
2. **A previously-implicit generalization broke on this project's own primary document.** Every project fully analyzed so far in this research line ships inspectable source, with specific unverified *claims* being the exception. `ostk.ai`'s own `LICENSE` file states source is "not yet publicly available," directly contradicting its own `README`'s "AGPL-3.0" line — confirmed independently by GitHub's SPDX detector, and confirmed further by the referenced source repo (`os-tack/haystack`) returning 404. The project's own conformance section asks readers to verify claims against source lines that are not actually accessible to them — an unresolved seam between an open-governance narrative and a closed-kernel commercial reality, not an oversight.

## State 5 — Cross-Validated

| # | Tag |
|---|---|
| 1, 2, 5 (ownership/reap/handle-gen) | **Candidate new capability territory** — confirms pattern E (event sourcing, the log substrate) only partially; the differentiated content doesn't fit any existing pattern letter. Flagged in `CAPABILITY_MAP.md` as a possible 11th capability, not added to the Map's structure directly — needs a second project with a similar lifecycle-ownership mechanism first. |
| 3 (closed signal table) | Related to pattern N (determinism boundary) by spirit (bounded, auditable vocabulary) but a distinct mechanism — logged as a related-but-not-identical candidate. |
| 4 (epoch fencing) | No existing pattern match — candidate new, filed under the same lifecycle-ownership territory as 1/2/5. |
| 6 (tier-floor intersection composition) | **Directly contrasts with pattern Z** (deny>ask>allow, ordered, first-match-wins) — a second, independently-arrived-at composition rule (most-restrictive-wins-by-intersection) for the same general problem (combining multiple permission policies). Logged as a genuine alternative within Capability 4, not a confirmation. |
| 7 (empirical permission learning) | Candidate new pattern — not previously logged anywhere in the Map. |
| 8 (three-tier CAS) | Relates to pattern from evidence on OCC-guarded execution (ai-runtime-lab, Capability 3) but applied to file-edit conflict resolution specifically rather than workflow orchestration — candidate refinement. |
| 9 (GENESIS self-attestation) | Confirms the general discipline already established (P4 — evidence over marketing) applied to a governance document specifically. |
| 10 (signed-binary, no source) | No existing pattern — logged as a data point on the "different bet" side, same spirit as pattern R (OpenSwarm's emergent coordination) being the outlier against convergent patterns elsewhere. |

## State 6 — Extracted

**Transfer**: the tier-floor-as-intersection composition rule, as a named alternative to ordered deny/ask/allow — worth knowing both exist as legitimate answers to "how do multiple permission sources combine," not just one. **Transfer**: empirical permission-bounding via observed-run learning, as a concrete technique for the general "measure, don't guess" principle. **Transfer, most important procedurally**: this project is the clearest evidence yet that a project's own README is not a reliable source even for its own licensing — check the actual LICENSE file and, where possible, an independent third-party classifier (GitHub's SPDX detection), not the prose description, before treating a project's self-declared terms as fact.

**Do not transfer**: the specific POSIX syscall-naming choices, the GPG-ceremony ritual details (`bootstrap-ceremony.sh`) — implementation and branding, not principle.

**Confidence**: High (ten fully-read primary documents, two independent API checks confirming the license contradiction and the private-repo status).

## State 7 — Capability Map update

Confirmations filed: `os-tack/ostk.ai` added to pattern E's source list (with the caveat that it's a minor part of this project, not its center of gravity, per contradiction #1). Pattern Z gets a new "alternative composition rule" note (tier-floor-by-intersection vs. ordered-first-match), not a confirmation of Z itself — both merged directly into `CAPABILITY_MAP.md`, Capability 4.
Candidates merged directly into `CAPABILITY_MAP.md` as single-source findings: a possible 11th Capability Map category (process/resource lifecycle ownership) — flagged, not added to the Map's structure, pending its own validation cycle; empirical permission-bounding via observation (Capability 4).

**State: Done.**
