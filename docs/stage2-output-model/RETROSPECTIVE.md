# Stage 2 — retrospective of the first attempt and brief for a restart

Date: 2026-10-23. The human stopped the first attempt after iteration 41 and decided to restart the formal output model in a new conversation, without letting it take days again. This file explains what went wrong and how to run the restart. It is input for the restart, not a rule for it.

## 1. Outcome in numbers

| Measure | Value |
|---|---|
| Wall-clock time | about 47 hours (2026-10-21 02:14 to 2026-10-23 01:16 UTC) |
| Iterations | 40 complete; review 41 done; the fix of 41 not started |
| Reviews / fixes / commits | 49 reviews (incl. re-checks), 41 fix logs, 111 commits |
| Remarks per main review | 12, 7, 7, 4, 3, 1, 3, 0 (iteration 8), then 0–3 for 33 iterations |
| Main reviews with NO_REMARKS | iterations 8, 10, 19, 21, 22, 25, 32. Each time a re-check then found a narrow new case |
| Model size | v00 268 KB, v10 476 KB, v20 647 KB, v34 822 KB; after the restructuring v35 421 KB, plus `RATIONALE.md` 319 KB |
| Content at v40 | 67 elements, 87 invariants (117 before merging), 160 formal blocks, 13 source-data tables (94 rows), 113 quote entries |
| Open at the stop | R41-01 and 14 findings of the `RATIONALE.md` audit (`audits/rationale-audit-v40-part*.md`), all about prose, not about values or coverage |

The model was substantively complete by about iteration 8–10, when the first main review found nothing. The remaining 30 iterations each removed one or two narrow defects.

## 2. What went wrong, most important first

1. **The stop rule could not be met on an artifact this large.**
   - The loop ended only when a main review and two independent re-checks *in a row* all found nothing. There was no severity threshold: any defect counted, whether a misread edge case, a page number or a sentence of prose.
   - Each fresh reviewer is a new sample of attention over about 1 MB of text: the model, `RATIONALE.md` and Stage 1. In practice, three clean samples in a row never happened. The main review was clean seven times and was beaten by a re-check every time.
2. **The model was formalised more deeply than the task needed.** It became a full first-order theory with:
   - contexts;
   - the lifecycle of treatment courses: stops, restarts, resumptions, unstated starts;
   - levels attached to individual conjuncts;
   - satisfiability arguments;
   - prose readings of every predicate.

   Every predicate became a surface for script-found counterexamples, and every prose sentence a surface for "prose says more than the predicate" remarks. Treatment-course semantics alone took iterations 25–28.
3. **Fixes only added.**
   - The minimal-fix rule made each fix add a clause or a special case. Nothing was merged or removed until the restructuring at iteration 35. By then the model was 822 KB, and an audit found 19 internal inconsistencies.
   - The orchestrator did not flag the growth until the human asked. It should have done so by iteration 10–12 (v12 was already 546 KB).
4. **Each iteration was serial and expensive.**
   - One reviewer read everything and re-verified all ~300 quotes by downloading 28 sources, every time, for about 25–30 minutes. One fixer followed.
   - That came to about one hour per iteration, so 40 iterations took about two days. The quotes did not change after v35, and six full verifications in a row found no misquote.
5. **Stage 1 ambiguities were carried into Stage 2.** Twelve Stage 1 issues (ISS-01–ISS-06, ISS-08–ISS-13) were found and recorded during Stage 2, but never decided. The model had to encode one reading of each, and reviewers kept probing those readings.
6. **Orchestration errors.**
   - The scope rule was first written stricter than the human intended; the human corrected it.
   - One re-check (19c) was steered toward particular points, which caused an extra iteration.
   - The orchestrator kept running the loop toward the iteration limit instead of proposing a change of approach once remarks had plateaued at one or two per iteration (from about iteration 12).

## 3. What worked and is worth keeping

- **The scope rule** as finally written: no input data, no storage format, no derivation from input; thresholds, formulas and computed fields that are part of the output data are required (PROCESS.md section 2).
- **Separating the model from its rationale**, with quotes, reasons and examples in a companion file.
- **Generality rules**: state a rule once; fix the class, not the case (PROCESS.md section 6a).
- **An output catalogue** (one row per kind of output) and **source-data tables** for values that sources fix.
- **Script checks** of IDs, traceability, brace balance and snapshot identity, and small-model witnesses.
- **Oscillation checks.** None of 10 found oscillation; they were useful mostly as trend reports.
- **Verified evidence that can be reused** (section 6).

## 4. How to run the restart

### 4.1 Before writing anything
1. **The human decides the Stage 1 issues** listed in section 5, or accepts the readings that v40 chose. The new model then encodes decisions, not open readings.
2. **Fix the form and the size of the deliverable in advance.**
   - **Depth.** A typed information model: records, enumerations, value sets, units, multiplicities, conformance levels and applicability conditions. Add a short list of constraints, and only those Stage 1 states as relations between shown values: co-presence, bounds, equal-length comparisons, a percentage change against its absolute change, the overuse indicator against its reference levels.
   - **What stays out.** No modelling of the lifecycle of context facts, such as treatment-course events. An applicability condition names a property of the subject or the context and is not defined further.
   - **Edge cases** that Stage 1 does not decide go to an issues list, not into predicates.
   - **A size budget**, for example a model of 150 KB or less, plus a rationale file. Every fix reports its size delta, and growth past the budget needs the human's approval.
3. **Reuse the verified evidence** (section 6) instead of researching it again. Add a new source only for a value that no existing entry supports.

### 4.2 The loop
- **Rounds, not single reviews.** One round is:
  1. **Parallel review.** Four to six reviewers work at the same time, each on one slice of the Stage 1 requirements, together with one cross-cutting checker for formal soundness and scope.
  2. **Fix.** One fixer then handles every remark of the round.
- **Classify each remark.**
  - *Blocking* means: a factual error against a source; a value, level or applicability condition that contradicts, narrows or broadens Stage 1; a scope violation; or contradictory or unsatisfiable constraints.
  - *Non-blocking* is everything else, including prose that is wrong but changes no value or level, citation locations, and edge cases Stage 1 does not decide.
- **Stop rule.**
  - Stop when one full round finds no blocking remark.
  - The non-blocking remarks are then fixed once, in a batch, and checked by script only.
  - There is a hard cap of four rounds. After that, the open remarks go to the human.
- **Quote verification** happens once, by a dedicated agent, at the start. After that, only quotes that were added or changed are verified.
- **Fixers** fix the class, keep rationale out of the model, report the size delta, and must not add a special case where a general rule exists.
- **After each round**, the orchestrator reports to the human: remarks by severity, size, and time used. If a round still has blocking remarks of a kind that keeps recurring, the orchestrator proposes a change of approach instead of running another round.

### 4.3 Time estimate
- First draft: about 1–1.5 hours.
- One round: about 1 hour (parallel review 30–40 minutes, fix 20–30 minutes).
- Three or four rounds: about 5–6 hours in total.

The hard cap of rounds is what keeps the restart from turning into days again.

## 5. Stage 1 issues the human should decide first

Recorded in section 8 of `OUTPUT_MODEL.md` v40, with evidence:

| ID | Issue |
|---|---|
| ISS-01 | The basis of the ICHD-3 8.2.6 indicator is not the total across all classes |
| ISS-02 | "Simple analgesics" is not the ICHD-3 name of the class |
| ISS-03 | Migraine days without the "patients with migraine" condition |
| ISS-04 | The clinician-facing summary includes MAY measures at SHOULD level, and the frequency outputs of OUT-001 |
| ISS-05 | OUT-019 and the single count of the IHS position statement 2025 |
| ISS-06 | "Total score" for instruments that have none |
| ISS-08 | Control levels under "responder or non-responder label" |
| ISS-09 | Which "acute medication outputs" OUT-029 breaks down by headache type |
| ISS-10 | Evaluation time points for preventive treatments outside the populations of the guidance quoted in OUT-018 |
| ISS-11 | The NICE CG150 1.3.48 review window for children under 12 |
| ISS-12 | Cluster remission duration in ICHD-3 |
| ISS-13 | Residual burden next to a percentage change over a period shorter than a month |

## 6. Reusable assets from the first attempt

All paths are in `docs/stage2-output-model/`. They were checked repeatedly; the counts are from reviews 36–41.

- **`RATIONALE.md` (v39), its Q entries:** 113 entries with about 300 quoted fragments.
  - Each fragment was verified verbatim at its URL and location in six full reviews, with no misquote.
  - Sources S-101 to S-106 have verified metadata.
- **`OUTPUT_MODEL.md` (v40), section 11:** 13 source-data tables with 94 rows, matched against their sources in every review since v35:
  - ICHD-3 codes and 8.2 reference levels;
  - fixed definitions;
  - evaluation rules of guidance;
  - responder criteria;
  - control levels;
  - instrument value sets and grade bands;
  - screening cut-offs;
  - early time points.
- **`OUTPUT_MODEL.md` (v40), section 4:** the output catalogue (45 rows), which is a usable skeleton for the new model.
- **`restructure/plan-v35.md`:** the families of rules that turned out to be generic.
- **`PROCESS.md`:** section 2 (scope rule) and section 6a (generality rules).

The first attempt itself (v00–v40, its reviews, fixes, audits and oscillation checks) stays in place as a record. The restart should work in a new folder, so that the two attempts do not mix.
