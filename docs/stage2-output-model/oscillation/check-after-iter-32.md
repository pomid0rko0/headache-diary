# Oscillation check — after iteration 32
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: versions v00 to v32 (history/v00.md to history/v32.md; OUTPUT_MODEL.md is byte-identical to v32); reviews review-iter-01 to review-iter-32 with the re-checks 08b, 10b, 19b, 19c, 21b, 22b, 25b and 32b (40 files, 79 remarks; iterations 29–32: 1, 1, 1 and 0 + 3); fixes fix-iter-01 to fix-iter-32; the earlier oscillation checks after iterations 04, 08, 12, 16, 24 and 28, with all seven watch points of check-after-iter-28.md and the open watch points of the checks after iterations 12, 16 and 24. Read in full: PROCESS.md, check-after-iter-28.md, review 29, fixes 29 to 32. Read in full except their source-download and quote tables: reviews 30, 31, 32 and re-check 32b (summary, remarks, "Checked and not raised"). Read at the passages that bear on the items changed in v29–v32: the watch points and recurring-topic table of the checks after iterations 12, 16 and 24; review 02 and fix 02 on R02-04 and item 14; fix 18 on R18-01; fix 26 on the level of INV-070; reviews 08, 08b, 17 and 18 on `namedCriteria`; fix 10 on the INV-050 Reading. All 40 reviews and all 32 fix logs were also searched by script (remark items, reversal language, earlier positions on every point that v29–v32 changed). Every snapshot was split by script.
Date: 2026-10-22

## Method

1. **Git history.**
   - Checks:
     - each of v29 to v32 was added in exactly one commit and never changed afterwards (v29 a300ac2, v30 1ff0dd5, v31 d37b98f, v32 8764ec8);
     - at each of these fix commits, OUTPUT_MODEL.md is byte-identical to that commit's snapshot;
     - the committed snapshots v00 to v32 equal the working-tree snapshots;
     - from 59e06b7 (check 28) to 8764ec8 (fix 32), every review, re-check and fix log was added in its own commit, in loop order: review 29 (e1afc83), fix 29, review 30 (b6e836c), fix 30, review 31 (de06d47), the process change 806ed98 (iteration limit 32 → 64, PROCESS.md only, one line), fix 31, review 32 (b772a9b, NO_REMARKS), re-check 32b (0d0157d, 3 remarks), fix 32;
     - each fix commit touches only OUTPUT_MODEL.md, its snapshot and its fix log, and each review commit touches only its review;
     - Stage 1 is unchanged since bfec74f.
   - All checks passed. The working tree was clean, FROZEN_ITEMS.md does not exist, and no snapshot carries a FROZEN marker.
2. **Item split** (`split.py`). The granularity of the checks after iterations 12, 16, 24 and 28, extended to 33 versions. It gives 2,573 distinct items: the header and sections; every element, invariant and Stage 1 issue with each field; every attribute and declaration of the `omn` blocks; the traceability rows with their columns; the source rows, the withdrawn row, the search-log lines and the change-log paragraphs. The splitter reproduces the iteration-28 check's volumes for v25–v28 exactly (39, 41, 36, 84).
3. **State trajectories** (`analyse.py`). Each item was hashed per version; the script flags every item that returns to the state of a non-adjacent earlier version after a different state in between (A → B → A, including add → remove → add), and every removal or re-addition in v29–v32.
4. **Formal blocks** (`omn.py`, `omndiff.py`, `hist.py`).
   - The same trajectory test on every `omn` block, raw and with comments removed.
   - Every block changed in v29–v32 was diffed line by line.
   - Every distinct state since v00 of each changed predicate was printed and read: INV-027, INV-039, INV-050, INV-062, INV-069, INV-070, INV-079, INV-082, INV-085, INV-092 and INV-105, with the new INV-112 to INV-117.
5. **The v31 split** (`split31.py`).
   - Textual: the top-level conjuncts of v30 INV-070 and INV-050 were compared, as multisets, with those of v31 INV-070 + INV-112 and INV-050 + INV-113; v31 INV-062 and INV-092 were compared with v30 minus exactly the moved conjunct.
   - Semantic: the quantifier structure of each split was transcribed and the v30 form was compared with the conjunction of the two v31 invariants on 20,000 random finite models each.
6. **v32 direction and INV-116** (`narrow32.py`).
   - The v31 and v32 forms of the rewritten conjuncts (intensity in INV-039, INV-069 and INV-105; symptoms in INV-069; severe impairment in INV-027) were evaluated on 30,000 random finite models each, to test v32 ⇒ v31.
   - INV-116's omission rule was tested against INV-063's forced categories on every criterion of up to five components with up to three condition-failed components (3,636 cases).
7. **Near-return detector** (`nearret.py`). For every change from vᵢ₋₁ to vᵢ, with i from 29 to 32, whether vᵢ is closer by word-level similarity to an earlier state vⱼ (j < i − 1) than to vᵢ₋₁.
8. **Word-level diffs** (`dels.py`, `moved.py`, `wdiff.py`). Every item changed in v29–v32 was classified as new, additive or edited; every deleted span of four or more words was listed, and tested for whether it reappears verbatim elsewhere in the same version (a move). The text fields of the treatment-course cluster, the responder-label elements and every other item changed in v32 were diffed version by version.
9. **Insert/delete n-grams** (`ngram.py`, `docwide.py`). Per item and over sections 1–9 as a whole, 6-word n-grams deleted at some vⱼ and re-inserted in v29–v32, and inserted at some vⱼ and deleted in v29–v32.
10. **Conformance** (`conf.py`). Across all 33 versions: every invariant's level; every attribute declaration (level, `when` clause, `derived` mark); the level-keyword counts of every element Conformance field.
11. **Guarantee terms and watch-point blocks** (`guar.py`).
    - 65 protected terms counted in the comment-free formal text of v24 to v32: the ties of all earlier watch points (for example `notStoppedBefore(`, `evaluatedOnTreatment(`, `sameSpan(`, `summarisesMedication(`, `courseOverlaps(`, `#L.evaluated = 1`, `rc.treatment = L.treatment`, `fillsPeriod(`, `v.covers.start = v.withdrawalStart`, `originalStart(`, `courseBegunBy(`, the INV-070 presence conjunct, fix 28's duration conjunct, `conditionHolds(`, `evaluationResult(`, `attackScope(`, `allTypes`) and the new terms of v29–v32.
    - The 50 blocks named in the watch points of the checks after iterations 16 and 24 (listed there as 49), and the 12 treatment-course blocks of the check after iteration 28, compared between v28 and v32.
12. **Remark topics** (`remarks.py`). All 79 remarks were mapped to E-, INV-, ISS- and OUT- IDs; for each remark of iterations 29–32 the earlier remarks on the same IDs were listed, and every sentence with revert, undo, reverse, restore, remove, drop, loosen, relax, weaken, re-raise or reopen was read. All reviews and fix logs were searched for earlier positions on each point that v29–v32 changed (stop reasons, scales, results shown without their date, the treatment of a label, the components of an index, the start of withdrawal, `namedCriteria`, the level of INV-070, derived attributes with omitted arguments).
13. **Bookkeeping** (inline script). Change-log paragraphs, source rows, the withdrawn row, the ISS items, the search log and sections 1 to 4, 8 and 10, v28–v32.
14. **Judgement.** Each item that changed in two or more versions, at least once in v29–v32, was read against the remark or fixer decision behind each change and classified as convergent (one direction, earlier guarantees kept) or oscillating (back and forth on the same point).

**Results of the mechanical steps**

- **Step 3.**
  - 1,143 items changed at least once, and 460 in two or more versions.
  - One item returns to a non-adjacent earlier state: `E-008.attr.SubjectProfile.aged12OrOlder`, added in v06 and removed in v12, which the iteration-12 check assessed. Nothing new in v29–v32.
  - No item was removed in v29–v32, and no removed item was re-added. The IDs INV-112 to INV-117 occur in no snapshot before their version.
  - 84 leaf items changed in two or more versions with at least one change in v29–v32. They fall into the six topics of the next section.
- **Step 4.**
  - No `omn` block, raw or with comments removed, returns to an earlier state in v00–v32.
  - Blocks changed per version: v29 0; v30 1 (INV-079, three lines inserted); v31 8 (INV-050, INV-062, INV-070 and INV-092 changed; INV-112 to INV-115 new); v32 11 (E-023, E-025, INV-027, INV-039, INV-069, INV-079, INV-082, INV-085 and INV-105 changed; INV-116 and INV-117 new).
  - Every changed predicate's full history was read. INV-079 only gains conjuncts (v02, v17, v28, v30, v32), every earlier conjunct verbatim. INV-082 and INV-085 gain an availability conjunct that no earlier state had. INV-027, INV-039 and INV-069 reach a third or later state that no earlier version had (no earlier form tied the scale, form or impairment domain across periods). INV-105 changes only its series intensity term; the treatment-effect conjunct is verbatim.
- **Step 5 (the v31 split).**
  - The conjunct multisets are equal: INV-070 (10 = 10, with INV-112), INV-050 (6 = 6, with INV-113). INV-062 and INV-092 in v31 equal their v30 forms minus exactly the moved conjunct.
  - All eight invariants have scope "output"; the four sources stay SHOULD and the four new ones are definitional.
  - Finite models: 0 mismatches of 20,000 each for INV-070 ≡ INV-070′ ∧ INV-112, INV-092 ≡ INV-092′ ∧ INV-115 and, with `comparison : opt`, INV-062 ≡ INV-062′ ∧ INV-114. With two comparisons (outside the typing), 744 of 20,000 differ, as fix 31 notes for its own enumeration.
- **Step 6.**
  - In 30,000 models each, no v32 form holds where its v31 form fails. v32 rejects 2,380 intensity configurations, 79 symptom configurations and 638 severe-impairment configurations that v31 admitted.
  - INV-116's omission rule changes no category that INV-063 forces (0 mismatches of 3,636). Because `components` is `set1`, a criterion all of whose components fail their condition keeps at least one of them, so the label is still forced to "non-responder".
- **Step 7.** 217 changes examined, 1 hit: the INV-050 Reading of v31 is closer to its v09 form than to v30. v10 had added "the subject's" to the start of withdrawal (fix 10); v31 writes "its start of withdrawal, a start of withdrawal of the subject (INV-113)". The v10 content is kept; the hit is a metric artefact.
- **Step 8.**
  - **Change types** (leaf items, without sections, logs and aggregates): v29 3 edited; v30 6 edited, 3 additive; v31 31 edited, 9 additive, 33 new; v32 37 edited, 31 additive, 23 new.
  - **Deleted spans of four or more words:** v29 1, v30 1, v31 24, v32 4.
    - v29: E-055 Notes, "adherence refers to the time on treatment (INV-067)" (written in v02), replaced by the OUT-039 ground (Findings, E).
    - v30: E-055 Notes, "agrees with the start and the stop date, or with the start and the as-of date", replaced by the stricter relation of R30-01.
    - v31: every span is a conjunct or text moved from INV-050, INV-062, INV-070 and INV-092 to INV-112 to INV-115. Each one reappears verbatim in the new invariant (the INV-070 Notes and Reading text in INV-112's Notes and Reading), apart from bracket and `∧` boundaries.
    - v32: the INV-027 severe-impairment conjunct (rewritten with one domain) and the INV-069 intensity and symptom conjuncts (moved out of `∀ p` and anchored).
- **Step 9.**
  - **Re-insertions within items:** 3, all artefacts. In the INV-070 Reading at v31, "original pre-treatment baseline period, so that worsening or rebound above baseline is visible" rejoins once the v26 and v27 parentheticals moved to INV-112. In the INV-079 Reading at v30, "(its duration to date)," gains a following clause.
  - **Document-wide:** 14 n-grams. They are the same artefacts, the conjunct order inside INV-112 (as in INV-070 before v28's presence conjunct was inserted between them), two field boundaries, and a Stage 1 quote of OUT-026 cited again.
  - **Insert-then-delete:** 117 hits with the deletion in v29–v32. They are reference changes from INV-070 to INV-112, sentences of earlier fixes extended within the sentence, the v31 moves, and the three fix-28 sentences that fix 29 corrected (INV-064 and INV-067 Notes, E-055 Notes). None removes a condition that an earlier fix inserted.
- **Step 10.**
  - No invariant level has ever changed. v32 totals: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 40 (34 until v30, 38 in v31).
  - No attribute level, `when` clause or `derived` mark changed in v29–v32, and none ever returned to an earlier state.
  - Element Conformance keyword counts only grew: E-023 (SHOULD 4 → 5) and E-025 (SHOULD 1 → 2), both in v32.
- **Step 11.**
  - No protected term occurs less often in any of v29–v32 than in the version before. The only drops since v24 are the targeted v27 and v28 removals that check 28 assessed.
  - Unchanged from v28 to v32 include `notStoppedBefore(` 5, `evaluatedOnTreatment(` 3, `sameSpan(` 30, `summarisesMedication(` 10, `#L.evaluated = 1` 4, `rc.treatment = L.treatment` 10, `evaluationResult(` 5, `pretreatmentBaseline(` 4, `attackScope(` 3, `allTypes` 105, `fillsPeriod(` 6, `courseBegunBy(` 5, the INV-070 presence conjunct 1 and fix 28's duration conjunct 1.
  - The terms that grow are the new ties: `firstChangedDay(` 3 → 4 (INV-112), `stopped(` 6 → 8, `conditionHolds(` 9 → 12, `namedCriteria` 1 → 2, plus the availability terms, `onSameScale(` and `inSameForm(`.
  - Of the 50 watch-point blocks of the checks after iterations 16 and 24, 46 are byte-identical in v28 and v32. The 4 that changed are INV-050 and INV-062 (v31 moves) and INV-069 and INV-105 (v32 scale and form).
  - Of the 12 treatment-course blocks of the check after iteration 28 (section 2.8, E-008, E-049, INV-001, INV-064, INV-067, INV-068, INV-070, INV-078, INV-079, INV-103 and INV-109), 10 are byte-identical. INV-070 changed only by the v31 move, and INV-079 only by the v30 and v32 insertions.
- **Step 12.** See "Recurring remark topics".
  - No remark of iterations 29–32 asks to undo a fix. The flagged sentences are statements that the remark reverses nothing, and R31-01's "remove" instructions, which move conjuncts into new invariants.
  - No earlier loop file argued against any tie that v29–v32 added.
  - No remark that a fixer declined was raised again.
- **Step 13.**
  - The change log is append-only (33 paragraphs, none changed after its version).
  - S-101 to S-106, the withdrawn row and all ISS items are unchanged in v29–v32.
  - The search log is append-only (one line per version).
  - Sections 1 to 4 (including the notation and section 2.8), 8 and 10 are unchanged. Section 9 changed only in "as of vNN".

## Change history of items changed in two or more versions

Listed: items that changed in two or more versions, at least once in v29–v32. Items whose changes all lie in v00–v28 and that are unchanged since were assessed in the earlier checks (last row).

| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| **Fix-28 prose brought to its predicates.**<br>INV-067 Notes (v28, v29); INV-064 Notes (v05, v18, v28, v29); E-055 Notes (v02, v11, v17, v28, v29; also v30, v32, next rows) | v29 | **v29 (R29-01 and fix 29's check of all fix-28 prose).**<br>• INV-067 Notes: "still refers to days that the context places on the course" → the window begins on or after a dated course event, and INV-067 does not bound it by the stop or pause (fix 18's reading).<br>• INV-064 Notes: "within the days … not before it" → "so not before …, and end on or before every stop or pause …, so that the months of a course that has stopped or paused lie within those days".<br>• E-055 Notes: the ground "adherence refers to the time on treatment (INV-067)" → the evaluation window of the comparison (OUT-039; `adherenceFor`; INV-109).<br>No `omn` block changed. | R29-01; fix 28 (the sentences); fix 18 and fix 02 (the readings the new text follows) | **Convergent** (Findings, E).<br>• Text only, each time toward the predicate, which is byte-identical since v28.<br>• No sentence was weakened in a way that undoes a fix: fix 18's "no stop bound" and the E-055 `when` clause of fix 02 are kept, and the sentences deleted were written in v28, except E-055's v02 ground, which v28's INV-067 had made false. |
| **Duration and stop reason of a treatment line.**<br>INV-079: Predicate (v02, v17, v28, v30, v32), Reading (v02, v17, v28, v30, v32), Evidence (v02, v17, v30, v32), Notes (v02, v17, v25, v28, v30, v32).<br>E-055 Notes (v29, v30, v32); INV-109 Reading (v11, v13, v14, v15, v28, v30); row OUT-024 (v02 … v28, v30, v32) | v30, v32 | **v30 (R30-01, option (a)).** A shown duration equals the days from the course's start to its one stop or pause, or to the as-of date, whatever dates the line shows. Fix 28's `∀ d ∈ l.duration • startOf(…) ≠ ∅` is kept, and every earlier line is verbatim.<br>**v32 (R32b-02 (b)).** `l.stopReason ≠ ∅ ⇒ stopped(ctx, l.treatment)`.<br>Readings, Notes, the INV-109 Reading and row OUT-024 were aligned each time. | R02-05 and fix 02 (the shown-date relation); R17-02; R25b-01; fix 28 row 39; R30-01; R32b-02 | **Convergent.**<br>• Every state of INV-079 contains every conjunct of the state before it, verbatim.<br>• R30-01's option (b) was not taken; fix 30 argued that it is not definitional.<br>• Fix 02 item 14 (E-063, E-058) concerns other attributes and is kept: fix 30's sweep left both unchanged, as reviews 30 and 31 did. |
| **Identity ties moved to definitional status** (v31).<br>INV-070 (v17, v26, v27, v28, v31) → INV-112; INV-050 (v03, v05, v31) → INV-113; INV-062 (v02 … v15, v31) → INV-114; INV-092 (v31) → INV-115.<br>Conformance and Notes of E-033 (v12, v31), E-039 (v05 … v17, v31), E-046 (… v28, v31, v32) and E-049 (… v28, v31).<br>References in the Notes of E-008, E-012, INV-001, INV-097 and INV-103; rows OUT-017, OUT-020, OUT-022 and OUT-037 | v31 | **v31 (R31-01, option (a)).** The conjuncts that state what the element is were moved verbatim, at the same scope, into four definitional invariants:<br>• the post-stop view's treatment, event, date and periods;<br>• the start of withdrawal;<br>• the comparison's treatment;<br>• the components' period and scope.<br>The presence and value conjuncts stay at SHOULD. The INV-070 presence conjunct stays in INV-070. | Fix 26 (INV-070 stays SHOULD, which it does); iteration-24 topic "Truth of a shown fact"; R30-01's principle; R31-01 | **Convergent: a pure move** (Findings, A).<br>• The fully conformant outputs are unchanged.<br>• MUST-conformant outputs narrow by exactly the outputs that show a false event, withdrawal, treatment or period.<br>• No conjunct, level, `when` clause or date changed. |
| **Named criteria and the label's treatment** (v32).<br>E-045 Meaning and Notes (v01 … v13, v32); E-046 Conformance and Notes (… v31, v32); new INV-116 and INV-117; row OUT-020 (v01 … v28, v31, v32) | v32 (E-045 last changed in v13) | **v32 (R32b-01; R32b-02 (a)).**<br>• INV-116: a criterion shown under the name of a named criterion has the same `alsoRestsOn` and a subset of its components, omitting only components whose condition the label's treatment does not meet. The review asked for `K = n`.<br>• INV-117: the label's treatment is a preventive treatment of the subject.<br>The E-045, E-046, INV-062, INV-063 and INV-064 blocks are byte-identical. | Reviews 08, 08b, 17 and 18 (`namedCriteria` unused; settled); R08b-01 (open kinds); R32b-01; R32b-02 | **Convergent** (Findings, B and D).<br>• Two new invariants, so only narrowing.<br>• Every responder-label tie of iteration-12 watch point 2 and iteration-16 watch point 4 is verbatim.<br>• A settled "not raised" point is reopened for the first time, in one direction. |
| **Availability of instrument and screening results** (v32).<br>INV-082 Predicate (v01, v32), Reading (v01, v10, v32); INV-085 (v32); E-057 Notes (v01, v03, v19, v32); E-058 Conformance and Notes (… v12, v32); E-059 (v03, v08, v11, v32); rows OUT-026 (v01, v03, v08, v32) and OUT-033 (v08, v11, v32) | v32 | **v32 (R32b-02 (c), (d)).** A result shown without its date is still one of an instrument (or screening instrument) whose result is available. E-057 Notes gained "the availability of a result of the instrument" in a sentence written in v03, and nothing was deleted. | R32b-02 | **Convergent.**<br>• No earlier state had or rejected this tie.<br>• E-057 Notes is a text-only item of iteration-24 watch point 7, and v32 adds to it without restoring any earlier wording. |
| **Comparability across periods** (v32).<br>E-023 (Definition: `onSameScale`; Conformance v10, v12, v13, v32; Notes v10, v32); E-025 (`inSameForm`; Conformance v13, v32); E-030 Conformance (v02, v12, v32).<br>INV-027 (Predicate v02, v32; Reading v02, v10, v32); INV-039 (v02, v12, v13, v32); INV-069 (Predicate v13, v15, v32); INV-105 (… v16, v22, v32).<br>Rows OUT-010, OUT-021, OUT-027 and OUT-035 | v32 | **v32 (R32b-03, and the fixer's sweep).**<br>• Intensity summaries of compared periods on one scale and in one form (INV-039, INV-069, INV-105): anchored on one summary, less strict than the review's all-pairs form.<br>• The symptom presence of the treatment review view in one form (INV-069; the review left it to the fixer).<br>• Severe impairment counted in one domain across compared periods (INV-027; the fixer's own finding). Fix 02 had copied INV-026's per-period `∃ d` without arguing for differing domains. | R02-04 and fix 02 (INV-027); R11-01, R13-01 (INV-039, INV-069); R13-01 … R16-01 (INV-105); R32b-03 | **Convergent.**<br>• Each rewrite implies its v31 form (step 6), and no earlier state tied scale, form or domain.<br>• INV-105's treatment-effect conjunct (iteration-16 watch point 1) is verbatim.<br>• INV-018 and INV-029 (per-period values) and INV-062 were left unchanged with reasons. |
| Header; sections 7 (table), 9, 11 and 12 | every version | Version line, "as of vNN", one search-log line and one change-log paragraph per version, and the traceability rows above. | — | Bookkeeping, not applicable. |
| Items whose changes all lie in v00–v28 and that are unchanged since: among them section 2.8, E-008, E-049 (`omn`), INV-001, INV-064, INV-067, INV-068, INV-078, INV-103 and INV-109 (`omn`), and 46 of the 50 watch-point blocks of the checks after iterations 16 and 24 | within v00–v28 | See check-after-iter-04, -08, -12, -16, -24 and -28. | as there | Convergent (earlier checks). Unchanged in v29–v32. |

## Recurring remark topics

| Topic (IDs) | Remarks | Pattern | Assessment |
|---|---|---|---|
| **Treatment-course semantics** (INV-001, E-008, E-049, INV-064, INV-067, INV-070, INV-079, INV-103, INV-109; OUT-022, OUT-024) | R29-01 (sixth in a row on the cluster), R30-01. Earlier: R25b-01, R26-01, R27-01, R28-01, R28-02 | **The cascade of v25–v28 has ended.**<br>• R29-01 is text-only: a sentence of fix 28 that claimed more than its predicate. It is the last consequence of the cascade's own fixes.<br>• R30-01 concerns a gap present since v02 (a duration shown without its dates), not a consequence of fixes 25–29.<br>• Since v28, no predicate of the cluster has changed except the two additive INV-079 conjuncts and the verbatim v31 move of INV-070's bounds into INV-112. | **Converged as a cascade.** None of the cluster's v28 decisions was revisited. Check 28's question (a self-feeding cascade beyond iteration 32) does not arise. |
| **Truth of a shown fact tied to the context** (INV-079; INV-112 to INV-117; INV-082, INV-085) | R30-01, R31-01, R32b-02, and R32b-01 for named thresholds. Earlier of the same kind: R17-02, R18-01 (b), R23-01 (iteration-24 check) | **A new, self-widening cascade.** Each remark applies the previous fix's principle to a wider class:<br>• a derived value tied to the context whatever the item shows (R30-01);<br>• identity conjuncts that held only at SHOULD (R31-01, citing fix 30);<br>• facts with no tie at any level (R32b-02, citing fixes 30 and 31).<br>Each fix's sweep was scoped to its remark's class (fix 30: derived attributes; fix 31: conjuncts of SHOULD invariants), and the next reviewer found the wider class. Fix 32's sweep is the broadest yet: every attribute that names or presupposes an entity of the context. | **Converging in direction, not yet exhausted.**<br>• Every step only narrows (MUST-conformant outputs, and fully conformant outputs only where they state a false fact).<br>• Every tie that earlier fixes declined with reasons is kept: fix 18 (the periods of a label), fix 17 (a summary's formulation), fix 02 item 14 (E-063, E-058), review 31 (INV-078 grouping, INV-035), and E-051 with 0 attacks. |
| **Text that claims more than the predicate** (INV-064, INV-067, E-055; INV-079, INV-109 Readings) | R29-01; R30-01 (its Reading part); fix 29's check of all fix-28 prose. Earlier: R27-01, R28-01, R28-02; R22b-01 … R24-02 | One direction: text brought to the predicate, or the predicate brought up to the text (v30). None of these items was aligned in v22–v24 (iteration-24 watch point 9). | Convergent. |
| **"Not raised" points later raised** | Review 29 (optional E-055 phrase) → fix 29; review 32 (NO_REMARKS) → re-check 32b; reviews 08, 17 and 18 and the check-24 settled list ("`namedCriteria` unused") → R32b-01; review 32b (INV-069 symptom forms) → fix 32 | **Threshold differences between reviewers,** as checks 24 and 28 noted (R19c-01; review 15 → R25b-01).<br>• Review 32 classed "other SHOULD conjuncts that state what an element is" as exhausted; re-check 32b found ties at no level, a different sub-case.<br>• Reviews 08, 17 and 18 judged `namedCriteria` unused only in order to accept criteria outside the list, which INV-116 keeps. | One direction: each time a constraint is added, never loosened. No later remark argues that the earlier "not raised" state was right (Findings, D). |
| **Comparability of compared values** (E-023, E-025, INV-027, INV-039, INV-069, INV-105; OUT-010, OUT-021, OUT-027, OUT-035) | R32b-03. Earlier on the same IDs: R02-04, R11-01, R13-01, R15-01 | A new topic. Its earlier counterpart for day counts is INV-053 and INV-111 (R24-02), which v32 leaves unchanged. | New; one direction. |
| **Topics of the earlier checks:** by-dates relations, INV-111, the cluster view, `fillsPeriod`, formulation ties, text-only ISS items, E-041, INV-098, co-presence, the menstrual-relation view, withdrawal follow-up (other than the v31 move), the E-008 time frames | none in 29–32 | Reviews 29 to 32b list them as settled and not reopened. | Stable. |

**Settled points.** Reviews 29 to 32b list these as "not reopened (no new evidence)", and every item behind them is byte-identical in v29–v32, or changed only on another dimension (marked):
- adherence windows reaching past the stop (fix 18; restated, not changed, in fix 29);
- periods beyond the as-of date; INV-060 with INV-061 for short compared periods; caregiver lost productive days;
- the E-063 and E-058 derived attributes (fix 02 item 14);
- INV-106 at MUST NOT; the "> 3 months" readings of INV-045 and INV-089; INV-023 at any granularity;
- INV-027 tied to preventive treatments (v32 changed only the impairment domain);
- the E-041 readings, ages and `excludes`; the MIDAS labels and Grade IV undivided; the HIT-6 one-month recall; HADS subscales only; the HALT-90 overlap at 20;
- "history of previous bouts"; empty `remissions` in chronic cluster headache (ISS-12); E-039 `reviewWindow` without a `when` clause;
- a label under a criterion whose conditions do not hold is forced to "non-responder" (reviews 02 and 21b; kept under INV-116, step 6);
- INV-046 "the two directions agree"; the indicator's `basis` and `span` at MUST; the one-month baseline of the response comparison;
- unstated starts as a Stage 1 issue (fixes 27 and 28);
- the `when` clause of E-049 together with the INV-070 ask (check 28, watch point 5).

**Remark counts per iteration:** 12, 7, 7, 4, 3, 1, 3, 0 + 2, 1, 0 + 2, 3, 2, 3, 2, 3, 1, 3, 1, 0 + 0 + 2, 1, 0 + 1, 0 + 1, 1, 2, 0 + 1, 1, 1, 2, **1, 1, 1, 0 + 3**.

## Convergence assessment

**Numbers** (v24–v28 from the iteration-28 check, reproduced exactly by this check's splitter):

| Version | v24 | v25 | v26 | v27 | v28 | **v29** | **v30** | **v31** | **v32** |
|---|---|---|---|---|---|---|---|---|---|
| Remarks of the iteration | 2 | 0 + 1 | 1 | 1 | 2 | **1** | **1** | **1** | **0 + 3** |
| Items changed (iteration-12/16/24/28 granularity) | 122 | 39 | 41 | 36 | 84 | **17** | **25** | **103** | **122** |
| Top-level elements, invariants and issues | 25 | 6 | 4 | 5 | 16 | **3** | **3** | **17** (4 new) | **18** (2 new) |
| Traceability rows | 6 | 2 | 1 | 1 | 4 | **0** | **1** | **4** | **8** |
| Invariant predicates / element definitions | 9 / 3 | 1 / 0 | 2 / 2 | 1 / 2 | 8 / 1 | **0 / 0** | **1 / 0** | **8 / 0** | **9 / 2** |
| Formal (`omn`) blocks changed or new | 12 | 1 | 4 | 3 | 9 | **0** | **1** | **8** (4 + 4 new) | **11** (9 + 2 new) |

The content items that fixes 29 to 32 list (3, 4, 21 and 26) equal the top-level items plus rows above. The rest of each count is bookkeeping, the sections that contain the changed items, and the split of each changed field.

**Reading.**
- **Volume.**
  - v29 (17 items, no block) is the smallest change of any version from v17 on, and v30 (25 items, 1 block) equals v23.
  - v31 and v32 rose to 103 and 122 items, the v24 peak. v31 is a move of conjuncts plus four new invariants. v32 addresses three remarks and adds a fixer sweep of comparable places (INV-027, the INV-069 symptoms, INV-105).
- **Remarks.**
  - The rate is flat: 1, 1, 1, then 0 + 3.
  - Iteration 32 brought the first NO_REMARKS main review since review 25. Its re-check found three remarks, so the loop has still not had three NO_REMARKS in a row.
  - The remarks have left the treatment-course cluster. R31-01 and R32b-01 to R32b-03 concern identity ties, named thresholds and comparability; the responder-label elements had drawn no remark since R18-01, and comparability is a new topic.
- **Cascade or cycle.**
  - **Why it converges in direction.** No item returns to an earlier state, and no admitted set re-widens. Every change of v29–v32 is one of three kinds:
    - text aligned to a predicate (v29, and parts of v30);
    - an added conjunct or invariant (v30, v32);
    - a verbatim move that leaves the fully conformant outputs unchanged (v31).

    No remark asked to undo a fix, and every tie that earlier fixes had declined with reasons is still untied.
  - **Why it has not converged.**
    - A new self-widening cascade, "truth of a shown fact", has drawn three remarks in a row (R30-01, R31-01, R32b-02, plus R32b-01). Each fixer's sweep was scoped to its own remark's class.
    - Fixer sweeps beyond the remarks continue (fix 29: two further Notes; fix 32: INV-027, the INV-069 symptoms and INV-105). Each reverses nothing, but they keep the volume high.

**Judgement.**
- **Converging in direction.** v29–v32 is a monotone refinement:
  - the treatment-course cascade of v25–v28 has ended without a reversal;
  - the identity, named-criterion and comparability changes only narrow what the model admits, and only where an output states something false or not comparable.
- **Not converged in rate.** The remark count is flat, and the volume of v31–v32 equals the v24 peak.
- **What the next check should see.** With the limit now at 64, the question for iterations 33–36 is whether the "truth of a shown fact" class closes against fix 32's attribute table, and whether volume falls. If remarks keep widening that class, or a fix moves a tie back below definitional status, see watch points 1 and 2.

## Findings

None.

No item oscillates, so nothing is frozen, FROZEN_ITEMS.md is not written and OUTPUT_MODEL.md is not changed. Five points were examined as the closest approaches to a back-and-forth pattern; each is assessed below.

### A. The v31 split of INV-070, INV-050, INV-062 and INV-092 into INV-112 to INV-115: a pure move?

**What moved:**

| v30 invariant (SHOULD) | Moved verbatim to (definitional) | Left at SHOULD |
|---|---|---|
| INV-070 | INV-112: treatment, event kind, `eventOn`, the `originalStart` baseline bound, `consecutive(v.after)`, and, under the same `firstChangedDay` binder, the `courseBegunBy` on-treatment bound and `first(v.after).start = x` | the presence conjunct (`startOf … = ∅ ∧ courseBegunBy(…, plusDays(x, −1)) ⇒ v.onTreatmentPeriod ≠ ∅`) and the `shownDay` conjunct |
| INV-050 | INV-113: `v.withdrawalStart ∈ ctx.subject.withdrawalStart` | the start ties, `fillsPeriod`, values and review window |
| INV-062 | INV-114: `rc.treatment = L.treatment` for `rc ∈ L.comparison` | the existential with co-presence, coverage and residual burden; the nine `rc.treatment = L.treatment` conditions |
| INV-092 | INV-115: `m.period = x.period ∧ m.typeScope = x.typeScope`, under INV-092's own `concerns(ctx, x.typeScope, c1)` | annotation, co-presence, dimension coverage |

**Did any admitted set change?**
- **The fully conformant outputs did not change.**
  - The conjuncts are textually the same multiset (step 5), and all eight invariants have scope "output".
  - ∀ distributes over ∧, `c ⇒ X ∧ Y` splits into `(c ⇒ X) ∧ (c ⇒ Y)`, and, because `comparison : opt`, `∃ rc • T ∧ R` equals `(∃ rc • R) ∧ (∀ rc • T)`.
  - On 60,000 finite models there are 0 mismatches. They would differ only if `comparison` became a set (watch point 1).
- **The MUST-conformant outputs narrowed** by exactly those that show a false event, withdrawal, treatment or component period. v30 had no definitional invariant on these ties, so this is the remark's purpose, not a side effect.
- **Repertoire requirements.** INV-103 and INV-049 are byte-identical, and their witnesses meet the new ties (fix 31, check (iii)).

**Watch-point items kept:**
- check 28, watch points 1, 2 and 5: the presence conjunct stays in INV-070 at SHOULD, `courseBegunBy`, `originalStart` and the E-049 `when` clauses are verbatim, and E-049 Notes keep "aligned to the event, not to the start";
- iteration-08 watch point 4 and iteration-12 watch point 5: INV-050's start ties and `fillsPeriod`;
- iteration-12 watch point 2: `rc.treatment = L.treatment`, now definitional;
- fix 26: INV-070 stays SHOULD.

**Two options not taken, both stated in the loop files:**
- R31-01's variant: keep `consecutive(v.after)` and the first start at SHOULD, and state only `x ≤ p.start` definitionally;
- INV-115 for every index, not only indices for migraine.

**Judgement:** a pure move of text with the intended narrowing of MUST-conformance. Convergent.

### B. INV-116 and the responder-label guarantees (v32)

**Question.** INV-116 lets a criterion shown under a named criterion's name omit components whose condition the label's treatment does not meet. Does it contradict or loosen a responder-label guarantee (iteration-12 watch point 2, iteration-16 watch point 4)?

**It cannot loosen anything.**
- INV-116 and INV-117 are new definitional invariants.
- The E-045, E-046, INV-062, INV-063 and INV-064 blocks are byte-identical from v28 to v32.
- Every protected tie keeps its count: `#L.evaluated = 1` 4, `rc.treatment = L.treatment` 10, `evaluationResult(` 5, `pretreatmentBaseline(` 4, `attackScope(` 3, `otherValueNamed(` 2, `summarisesMedication(` 10, `allTypes` 105.
- `UnderlyingKind` and `PeriodValueKind` stay open, and conditions are still read on the treatment.

**It does not contradict a settled point.**
- INV-063 depends only on "some component is met" and "every component is decided and none is met". A component whose condition fails is never met and always decided, so omitting it changes neither (0 mismatches in 3,636 cases).
- `components : set1` keeps at least one component. So "a label under a criterion whose conditions do not hold is forced to non-responder" (reviews 02 and 21b; review 32's settled list) still holds.
- INV-062 asks nothing for a condition-failed component (its reduction and score conjuncts require `conditionHolds`).
- Criteria under other names stay unconstrained (R08b-01; OUT-020 "for example").

**Competing forms stated in the loop files:**
- review 32b's option (a), `K = n`;
- fix 32's subset form, which admits 53 truthful labels that `K = n` would reject in its enumeration.

Only one state exists so far.

**INV-117 and fix 18.** INV-117 ties the label's treatment, a different dimension from the evaluated periods that fix 18 declined to bound ("A definitional bound on every label would exclude an optional label that Stage 1 does not forbid"). Fixes 31 and 32 both list fix 18's decision as kept.

**Judgement:** convergent. No guarantee loosened; a new constraint added.

### C. The "truth of a shown fact" cascade R30-01 → R31-01 → R32b-02 (v30–v32)

**Trace:**
- **v30.** The duration is tied to the course whatever the line shows (INV-079).
- **v31.** The identity conjuncts of four SHOULD invariants become definitional.
- **v32.** Four facts with no tie at any level:
  - the treatment of a label (INV-117);
  - a stop reason only after a stop (INV-079);
  - the availability of an instrument result and of a screening result shown without its date (INV-082, INV-085).

**Why it is not an oscillation:**
- Each step adds a conjunct or invariant, or lifts a conjunct's level. None removes or lowers one.
- Each remark cites the previous fix as its principle. None argues against an earlier fix.
- The ties that earlier fixes declined with reasons stay declined, and fix 32's attribute table lists them:
  - the periods of a responder label (fix 18);
  - the formulation of an acute summary (fix 17);
  - E-063 `duration` and E-058 `changeFromBaseline` (fix 02 item 14; reviews 30 and 31);
  - INV-078's grouping and INV-035's covered period at SHOULD (reviews 31 and 32);
  - a 0-attack summary of a formulation never used (E-051).
- Fix 02 item 14 and fix 30 apply different standards to derived attributes, but on different objects. Fix 30 tied only the one derived attribute whose omitted arguments have counterparts in the context (fix 30's sweep, 33 attributes), and left E-063 and E-058 unchanged.

**Judgement:** convergent, a monotone narrowing. It is still producing remarks (watch point 1).

### D. `namedCriteria`: a settled "not raised" point reopened (v32)

**Trace:**
- Review 08: "`namedCriteria` constrains nothing (it appears in no invariant)".
- Reviews 08b, 17 and 18 say the same, and the iteration-24 check's settled list includes "`namedCriteria` unused".
- R32b-01 raised the tie between a criterion's name and its thresholds; v32 adds INV-116.

**Why it is not an oscillation:**
- The settled point answered another question: whether the Turkish Box 8 and Danish criteria must be among the constants. Each review concluded that a label may apply any criterion, and INV-116 keeps that.
- No review or fix argued that a criterion shown under a named criterion's name may carry other thresholds.
- The first change of this point adds a constraint. No later remark argues for the unconstrained state.
- PROCESS section 9's rule on re-raising concerns remarks that a fixer declined. No fixer declined this one.

**Judgement:** convergent, a reviewer threshold shift in one direction (as R19c-01 and R25b-01 were).

### E. E-055 Notes, changed in v29, v30 and v32, and the deletion of fix 02's adherence ground (v29)

**Trace:**
- **v29.** "and adherence refers to the time on treatment (INV-067)" (fix 02's first ground for the `adherence` `when` clause) → the evaluation window of the comparison (fix 02's second ground, OUT-039).
- **v30.** The Relations sentence on `duration`, stricter (R30-01).
- **v32.** A sentence on the stop reason (R32b-02).

**Why it is not an oscillation:**
- The three changes concern three different sentences, and no 6-word sequence deleted earlier was re-inserted.
- The v29 deletion follows from v28: INV-067 then admitted the adherence window of a course without a stated start, so INV-067 no longer grounds the start condition.
- The `when` clause of fix 02 is byte-identical, fix 28's table row 15 classifies it the same way, and INV-067's name is unchanged (fix 29, row 21).

**Judgement:** convergent.

## Things the next checker should watch

1. **Identity ties and "truth of a shown fact"** (INV-112 to INV-117; INV-079's v30 and v32 conjuncts; INV-082 and INV-085 availability; fix 32's attribute table). Treat as oscillation, unless it rests on evidence that R30-01, R31-01, R32b-02 and fixes 30 to 32 did not consider:
   - moving a tie back to SHOULD or into its v30 invariant (for example R31-01's variant for `consecutive(v.after)` and `first(v.after).start = x`), or dropping INV-112 to INV-117;
   - dropping fix 30's duration conjunct, or replacing it by R30-01's option (b);
   - dropping fix 28's `∀ d ∈ l.duration • startOf(…) ≠ ∅`;
   - re-tying what earlier fixes declined: the evaluated periods of every responder label (fix 18), the formulation of an acute summary (fix 17), E-063 and E-058 (fix 02 item 14), INV-078 grouping and INV-035 at definitional level (reviews 31 and 32), and adherence windows bounded by the stop (fix 18; fix 29).

   **Changing `E-046.comparison` from `opt` to a set** would break the equivalence of INV-062 ∧ INV-114 with v30 INV-062, and should be checked for that.

   **A fourth remark of this class in a row** should be checked against fix 32's attribute table. If it finds an attribute listed there as tied or outside the class, the sweeps are cycling. If it widens the class again, ask whether the class has an end.
2. **Named criteria** (INV-116, E-045, E-046; v32). Treat as oscillation, unless there is new evidence:
   - removing INV-116, or leaving named criteria unconstrained again;
   - switching to `K = n` (fix 32 found 53 truthful labels excluded);
   - widening the omission beyond components whose condition fails;
   - closing the list of criteria (R08b-01);
   - any change that ends the forced "non-responder" of a label whose criterion's conditions all fail (`set1`).

   All responder-label triggers of iteration-12 watch point 2 and iteration-16 watch point 4 still apply.
3. **Comparability** (`onSameScale`, `inSameForm`; INV-027, INV-039, INV-069, INV-105; v32).
   - **Reversals:** dropping these conjuncts, or moving INV-027's `∃ sd` back inside `∀ p`.
   - **New decisions, not reversals:** the review's all-pairs form, or extending the tie to INV-018, INV-029 or the values of INV-062, which fix 32 declined with reasons.
   - **INV-105:** its treatment-effect conjunct remains under iteration-16 watch point 1.
4. **The treatment-course cluster** (check 28, watch points 1 to 5). Unchanged in v29–v32 except the verbatim move of INV-070's bounds into INV-112 and the INV-079 additions. The reversal triggers now apply to INV-112 for the bounds (the baseline conjunct, `courseBegunBy`, the after-periods) and to INV-070 for the presence ask. Restoring any of the three fix-28 sentences that fix 29 corrected would be cycling:
   - "still refers to days that the context places on the course";
   - "within the days … not before it";
   - "adherence refers to the time on treatment (INV-067)" as the ground of the `when` clause.
5. **Earlier watch points** (checks 12, 16 and 24). 46 of the 50 named blocks are byte-identical v28 → v32. The other four are INV-050 and INV-062 (v31 moves) and INV-069 and INV-105 (v32 scale and form). Their reversal triggers still apply. "`namedCriteria` unused" is no longer a settled point: it is superseded by INV-116 (watch point 2).
6. **Change volume and remark pattern.**
   - Items changed: 17, 25, 103 and 122 in v29–v32; formal blocks: 0, 1, 8 and 11. Remarks: 1, 1, 1 and 0 + 3.
   - Check that volume falls after v32.
   - **Fixer sweeps beyond the remarks** (fix 29: INV-064 and E-055 Notes; fix 32: INV-027, the INV-069 symptoms, INV-105) should continue to be checked for reversals of the reviews' stated reasons. None is reversed so far.

## Conclusion

No item of the model oscillates after thirty-two iterations, and nothing is frozen.

- **Returns.** The only item that returns to an earlier state is `aged12OrOlder` (added in v06, removed in v12), assessed by the iteration-12 check. In v29–v32 no element, attribute, field, invariant, `omn` block, conformance level, `when` clause, source, section, value set, Realises field or traceability row returns to an earlier state, and no admitted set re-widens.
- **Questions asked of this check:**
  - **The v31 split** changed no fully conformant set. It is a verbatim move, confirmed textually and on 60,000 finite models, and it narrows MUST-conformance only by outputs that state a false fact (Findings, A).
  - **INV-116** loosens no responder-label guarantee. It is a new constraint; every label block and tie is verbatim; and its omission rule changes no category that INV-063 forces, including the settled forced "non-responder" (Findings, B).
  - **The treatment-course cluster of v25–v28.** No v29–v32 change touches it in a reversing direction: v29 aligned text to the v28 predicates, v30 and v32 added INV-079 conjuncts, and v31 moved INV-070's bounds verbatim into INV-112.
- **Change volume:** 17, 25, 103 and 122 items in v29–v32; formal blocks 0, 1, 8 and 11.
- **Remark counts:** 1, 1, 1 and 0 + 3.
- **Convergence.** The loop converges in direction: every change of v29–v32 aligns text, adds a constraint or moves one verbatim, and the treatment-course cascade has ended. It has not converged in rate: the remark count is flat, v31–v32 returned to the v24 volume, and a new, self-widening class of remarks (truth of a shown fact) is still producing remarks.

The scripts are in the session scratchpad (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/osc32/`): `split.py`, `analyse.py`, `volume.py`, `omn.py`, `omndiff.py`, `hist.py`, `split31.py`, `narrow32.py`, `nearret.py`, `dels.py`, `moved.py`, `wdiff.py`, `ngram.py`, `docwide.py`, `conf.py`, `guar.py`, `multi.py` and `remarks.py`. FROZEN_ITEMS.md was not written, and OUTPUT_MODEL.md and the history snapshots were not changed.
