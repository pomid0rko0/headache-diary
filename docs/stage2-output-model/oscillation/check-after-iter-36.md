# Oscillation check — after iteration 36
VERDICT: NO_OSCILLATION
Date: 2026-10-22
Versions examined: v00 to v36 (`history/v00.md` … `history/v36.md`), together with:
- the first committed v35 (commit 3b67179, called **v35a** below) and the corrected v35 (49c5ade);
- `history/v35-rationale.md`, `history/v36-rationale.md` and the RATIONALE of 3b67179.

`OUTPUT_MODEL.md` is byte-identical to v36, and `RATIONALE.md` to `history/v36-rationale.md`.

## Summary

No item oscillates across iterations 33–36, including across the restructuring. Nothing is frozen: `FROZEN_ITEMS.md` was not written, and `OUTPUT_MODEL.md` was not changed.

**What changed in the formal content.**
- **v33.** Four `omn` blocks changed, each in the direction of an earlier fix:
  - E-023 and E-025: one form per summary, now also among the "other" forms (R33-01, extending R32b-03);
  - E-033: `otherHeadacheIndex ⟨Text⟩` (fix-33 sweep);
  - INV-082: the `publishedGrading` conjunct (R33-02).
- **v34 and v36.** No `omn` block changed. v34 corrected two quote locations; v36 corrected bookkeeping fields, URLs and notation prose.
- **v35, the restructuring.** I compared it with v34 by meaning, using the mapping of `fixes/fix-iter-35.md`:
  - all 184 v34 elements and invariants are accounted for (146 kept, 38 withdrawn as merged, each with its target in section 9), and no ID is reused;
  - every edited block is a move (to a generic invariant, a W2 marker, an attribute type or a source-data table) or one of the listed intended changes CHG-01 to CHG-07 and CHG-R1;
  - all source-data values reproduce v34 verbatim;
  - no kept invariant changed level.

**No reversals.** No intended change and no audit-driven change restores a state that an earlier fix deliberately changed. No change removes a tie that an earlier fix added, except by an equivalent move. No watch point of the checks after iterations 04 to 32 is reversed.

**Five closest approaches.** Each is a single change backed by a reason that the earlier decision did not consider, and none has flipped back:
- **CHG-05** places positive acute-medication day counts inside the "truth of a shown fact" class. Fix 32's attribute table had listed them outside it.
- **CHG-03** changes the settled point "INV-060 with INV-061 for short compared periods" (fix 02, item 14) for the first time, and hands the question to the human as ISS-13.
- **CHG-04** removes a v00 conjunct of INV-031 that reviews 21, 21b and 22 had let stand.
- **INV-078 Evidence** returns in v36 to its v00 text: fix 36 drops a citation that fix 11 added. Text only; meaning unchanged.
- **CA-16** removes a v04 clause from the INV-105 Reading. That Reading is on check 24's list of items aligned in v22–v24, but the clause itself was never aligned.

**Direction.**
- v35 contains the first deliberate widenings since check 24: CHG-03 widens the fully conformant repertoire, and CHG-04 widens the admitted outputs. Neither returns to a set that an earlier version admitted.
- Every other change narrows, or moves equivalently.

**Trend.**
- Remark counts for iterations 25–36: 0 + 1, 1, 1, 2, 1, 1, 1, 0 + 3, 2, 1, 1, 3. Iteration 35 also had 19 audit findings and 5 equivalence defects.
- The content cascades of the earlier checks have stopped producing reviewer remarks: treatment courses, truth of a shown fact, comparability, and value-set facts that constrain nothing.
- The restructuring did not lower the remark count in its first iteration. It changed what the remarks are about: all three remarks of iteration 36 concern bookkeeping and prose that the rewrite introduced, none concerns formal content.
- These defects form a short, self-widening cascade: EQ35-02/03/04/05 → R36-01/02/03. Fix 36's sweeps are the broadest so far.

## Method

All scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/osc36/` and were run with `python3 -I`. The first committed v35 and its RATIONALE were extracted with `git show 3b67179:…` into the same folder as `v35a.md` and `v35a-rationale.md`.

1. **Git and files.**
   - From ae665ea (check 32) to HEAD there are 13 commits in loop order:
     - review 33 (6e02a16), fix 33 (ff41cc8);
     - review 34 (ffbce05), fix 34 (b2ce671);
     - review 35 (424584a), the audit (ffe3464), the PROCESS.md change (d80fc34), the plan (1cb4d31);
     - the restructured v35 (3b67179), the equivalence check (7b8af9e), the corrected v35 (49c5ade);
     - review 36 (888b6ef), fix 36 (3a6a2c1).
   - Each fix commit touches only the model, RATIONALE, their snapshots and its log. At each fix commit `OUTPUT_MODEL.md` equals its snapshot.
   - The 3b67179 snapshot equals the first v35. Of the history snapshots, only `v35.md` and `v35-rationale.md` were rewritten after their first commit, by the equivalence fix, as PROCESS.md section 8 provides. No snapshot up to v34 changed after check 32.
   - The working tree is clean, `FROZEN_ITEMS.md` does not exist, and no snapshot carries a FROZEN marker. Stage 1 is unchanged since bfec74f.
2. **Item split** (`split.py`, `versions.py`, `analyse.py`).
   - The splitter covers 38 snapshots (v00–v34, v35a, v35, v36) and gives 1,881 distinct items: every element, invariant and Stage 1 issue with each field and its `omn` text; the sections; and the table rows (traceability, catalogue, case-table, source-data, source and withdrawn rows).
   - Check: it reproduces check 32's counts for v29–v32 (top-level items 3, 3, 17, 18; `omn` blocks 0, 1, 8, 11; rows 0, 1, 4, 8).
   - Each item was hashed per version, after normalising white space.
   - Every change in v33–v36 was tested for a return to a non-adjacent earlier state.
3. **Formal blocks** (`omndiff.py`, `hist.py`).
   - Every `omn` block that changed between v32 and v33, v33 and v34, v34 and v35a, v35a and v35, and v35 and v36 was diffed line by line.
   - The full history of each changed predicate was printed and read: INV-031, INV-050, INV-060, INV-061, INV-075, INV-078, INV-082, INV-087 and E-033; also INV-021, INV-065, INV-048, INV-084, INV-013, INV-101 and INV-043, for CHG-07.
4. **Restructuring by meaning.**
   - **Accounting** (`mapcheck.py`): every v34 element and invariant against the v36 headings, v36 section 9 and the fix-35 mapping.
   - **Watch-point blocks** (`blocks.py`): 78 blocks that the checks after iterations 16 to 32 name, compared between v32 and v36.
   - **Source-data values** (`sdcheck.py`): the v34 constants and axioms were rebuilt from the v36 cells of SD-ER, SD-RC, SD-GB and SD-IN, and searched in v34. SD-CLS, SD-CMB, SD-FX, SD-CL, SD-SR, SD-ET and SD-DF were read against v34.
   - **Equivalences.** Each was read and argued from the definitions: the INV-123 members, the E-049/INV-070 merge, CA-05, INV-064 with SD-CL, INV-073 with SD-ET, INV-085 with SD-SR, INV-089 with INV-124, and C3-11 with INV-098.
5. **Protected terms** (`guar.py`).
   - 55 terms of the earlier watch points (for example `notStoppedBefore(`, `sameSpan(`, `courseBegunBy(`, `originalStart(`, `fillsPeriod(`, `rc.treatment = L.treatment`, `#L.evaluated = 1`, `onSameScale(`, `inSameForm(`, `publishedGrading(`, `consecutive(v.after)`) were counted in v28 and v32–v36.
   - The formal text counted is the comment-free `omn` blocks plus the backticked cells of the catalogue, case and source-data tables.
   - Every drop was traced to its cause.
6. **Near-return detector** (`nearret.py`, `nearret35.py`). For every changed field or row, I asked whether the new text is closer, by word-level similarity, to an earlier state than to its predecessor:
   - v33, v34, v35a → v35 and v36: 74 changes;
   - v34 → v35a: 176 changed Meaning, Reading, Conformance and Realises fields.
7. **Word diffs** (`wdiff.py`). Read for every hit of steps 2 and 6, and for every prose change named by an audit finding or CHG.
8. **Levels** (`levels.py`). Invariant levels per version; level changes of kept invariants between v34 and v36; the levels of the case rows C1–C3 against the merged invariants.
9. **Loop files.**
   - Read in full: PROCESS.md, the checks after iterations 28 and 32, reviews 33 to 36, fixes 33, 34, 35, 35-equivalence and 36, the audit, the equivalence check.
   - Read at the sections used: the plan (sections 12, 13 and 15, and the mapping); the watch points of the checks after iterations 04, 08, 12, 16 and 24.
   - Read at the passages that bear on the changed points: fix 02 (items 8 and 14), R01-03, R04-01 and fix 04, R05-01 and fix 05, fix 11 (table), fix 17, R24-02 and fix 24, reviews 21, 21b, 22 and 27, fixes 31 and 32 (the attribute table), and review 34 on HALT-30.
   - Every review and fix was searched by script for earlier positions on each changed point.
10. **Volume** (`volume.py`): changed items per version, v24–v36, with RATIONALE entries counted separately.

**Results of the mechanical steps.**
- **Returns (step 2).** Besides the withdrawal of the 38 merged invariants and the Notes fields that moved to RATIONALE, eight fields return to an earlier text:
  - the Readings of INV-008, INV-037 and INV-038 (v35a equals v12, v10 and v00);
  - INV-075 Predicate, Reading and Evidence (v35a, v35a and v36 equal v02);
  - INV-078 Evidence (v36 equals v00).

  All are examined in the table below. No `omn` block returns to an earlier state, except INV-075 by the move of its v17 conjunct to INV-123.
- **Formal blocks (step 3).**
  - v32 → v33: 4 changed (E-023, E-025, E-033, INV-082).
  - v33 → v34: 0.
  - v34 → v35a: 105 (30 elements and 29 invariants edited, 38 removed, 8 new).
  - v35a → v35: 1 (E-045: a stray `}` deleted).
  - v35 → v36: 0.
- **Accounting (step 4).** 184 v34 IDs: 146 kept, 38 withdrawn with a section 9 row whose target agrees with the fix-35 mapping, 0 unaccounted. The new IDs INV-118 to INV-125, ISS-13 and the OC, C and SD rows occur in no snapshot before v35.
- **Watch-point blocks (step 4).**
  - Of the 78 blocks, 32 are byte-identical from v32 to v36, among them INV-001, INV-003, INV-006, INV-008, INV-027, INV-039, INV-049, INV-055, INV-058, INV-063, INV-069, INV-074, INV-088, INV-103, INV-104, INV-105, INV-114, INV-115, INV-116, E-006 and E-067.
  - The other 46 changed only by the v33 changes or by the moves of fix-35 section 8, each read.
  - The section 2.8 and 3.4 blocks are byte-identical from v32 to v36.
- **Source data (step 4).**
  - 65 rebuilt values and rows match v34 verbatim, 0 mismatches: SD-ER 18 rules, SD-RC 6 criteria, SD-GB 16 bands, and 25 checks over the 9 SD-IN rows (`publishedGrading(halt30)` false).
  - The read tables also match v34: the overuse levels 15 and 10 and the 8.2.6 basis; SD-FX 2, 2, 4, 8, 12, 3, 3, 28; and the control levels with `insufficientControl` unbounded and forced above 6.
- **Protected terms (step 5).**
  - Unchanged from v34 to v36: `notStoppedBefore(` 5, `evaluatedOnTreatment(` 3, `intervalOnTreatment(` 5, `summarisesMedication(` 10, `courseOverlaps(` 3, `courseNotOutside(` 3, `#L.evaluated = 1` 4, `rc.treatment = L.treatment` 10, `fillsPeriod(` 6, `v.covers.start = v.withdrawalStart` 1, `originalStart(` 3, `courseBegunBy(` 5, `conditionHolds(` 12, `evaluationResult(` 5, `pretreatmentBaseline(` 4, `attackScope(` 3, `firstChangedDay(` 4, `stopped(` 8, `onSameScale(` 4, `inSameForm(` 2, `resumes` 7, `consecutive(v.after)` 1, `first(v.after).start = x` 1, `onlyOfType(` 6, `remissionMoreThanMonths` 2, `menstruatesDuring(` 4.
  - The drops, each explained:
    - `sameSpan(` 30 → 29: the CHG-04 conjunct;
    - `daysOf(` 34 → 23: the nesting bounds stated once in INV-122;
    - `publishedGrading(` 8 → 2, `excludes` 20 → 2, `ruleTr73` 3 → 1: values moved into source-data cells, rebuilt verbatim;
    - `eventOn(` 7 → 3, `startOf(` 24 → 23, `preventiveTreatments` 32 → 26, `acuteMedications` 30 → 28: fact conjuncts moved into one `stated` clause each (INV-123).
- **Near returns (step 6).**
  - v33, v34, v35a → v35 and v36: 2 hits, the INV-075 and INV-078 Evidence fields.
  - v34 → v35a: 58 hits. All are shortenings under rule 6a: templated Conformance fields, and Readings that lost consequences drawn with other items. The formal-content-bearing ones were read: E-049 Meaning; the Readings of INV-008, INV-037, INV-038, INV-055, INV-068, INV-070 and INV-105; E-019 Meaning. None drops a statement of its own predicate (table below).
- **Levels (step 8).**
  - v32–v34: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 40.
  - v35 and v36: MUST 11, SHOULD 33, SHOULD NOT 1, definitional 38, level-indexed 4.
  - No kept invariant changed level. Every case row keeps the level of the invariant it replaces (C2-04 and C2-05 `mustNot` for INV-048 and INV-106). The only level change is CHG-R1, upward.

## Items examined

"Convergent" means a change in one direction that keeps every earlier guarantee, or an equivalent move. Versions are those in which the field or block changed.

| Item | Versions where it changed | Nature of each change | Verdict |
|---|---|---|---|
| **E-023 `onSameScale`, `OtherSummary`; E-025 `inSameForm`** | v32 (new), v33; moved prose v35 | v32: one scale and one form for compared intensity and symptom summaries (R32b-03).<br>v33: the "other" forms state their form, and two other forms are one form only when their forms are equal (R33-01). | Convergent. One conjunct added in the v32 direction, and the v32 conjuncts are verbatim. INV-027, INV-039, INV-069 and INV-105 are byte-identical since v32. `otherIntensitySummary ⟨Text⟩` and `otherPresenceSummary ⟨Text⟩` were unchanged from v00 to v32. |
| **E-033 `HeadacheIndexKind`** | v00, v33 | `enum … \| otherHeadacheIndex` → `variant … \| otherHeadacheIndex ⟨Text⟩` (fix-33 sweep). A label resting on another index must show that index, not any other. | Convergent; first change. It is not the extension to INV-062's values that fix 32 declined: fix 32 declined a *scale or form* tie, and this concerns the *kind* of value that E-045 already claimed ("composite indices of each kind"). `PeriodValueKind` stays open (R08b-01; check 12, watch point 2). |
| **INV-082** | v00, v01, v32, v33, v35 | v33: `∀ cat ∈ r.category • publishedGrading(r.instrument)` (R33-02).<br>v35: the two availability conjuncts (v00 and v32) move to INV-123 `availableResult`, whose `stated` clause has the same two conjuncts with `ds = r.completionDate`. | Convergent. No earlier state had or rejected the grading tie. R03-07's decision (PGIC and others unfixed) is kept, and SD-IN keeps the same six fixed values: MIDAS, HIT-6, PedMIDAS, HALT-90 and HURT true, HALT-30 false. |
| E-057 Notes, E-058 Conformance and Notes, INV-039 and INV-069 Notes, rows OUT-010, OUT-021, OUT-026, OUT-035 | v33 (rows reset by the v35 template) | Text brought to the v33 predicates. | Convergent; text only. E-057 Notes (check 24, watch point 7) gained a reference and lost no wording. |
| **E-057 Evidence, [S-102] location** | v00…v33, v34; moved to E-057/Q03 and Q04 in v35 | "subsection 'Migraine-related disability'" → "section 'Migraine-related disability'" (R34-01, both JATS copies). | Convergent; first change, new evidence. The v34 wording is in v36 RATIONALE. |
| **ISS-03 Evidence, [S-001] location** | v20, v34; moved to RATIONALE in v35 | "A1.1 comments" → "A1.1.3 Non-menstrual migraine without aura, comments" (fix-34 sweep: ICHD-3 prints a code's comments before its subcodes; the ichd-3.org pages). | Convergent. Text-only watch item (check 24, watch point 7): no earlier wording restored. Fix 20 had not examined which code the comments belong to. The quote and the ISS-03 argument are unchanged. |
| **INV-075** | `omn` v00, v02, v17, v35; Evidence v02, v17, v36 | v35: the v17 conjunct `∃ m ∈ ctx.subject.acuteMedications • m.drug = l.drug ∧ ∀ f ∈ l.formulation • m.formulation = f` moves to INV-123 `usedMedication((l.drug, l.formulation))`, whose `stated` clause is the same formula. Both are definitional.<br>v36: the OUT-023 formulation quote follows it to INV-123/Q01. | Not a reversal. The return to the v02 text is a move; the formulation tie of check 24, watch point 6 holds verbatim in INV-123. |
| **INV-078 Evidence** | v00, v11, v36 | v11 (fix-11 sweep, R11 co-presence): added the OUT-024 sentence "For acute treatments, the list SHOULD also show the formulation of each treatment", citing it for the placement of the history's groups and lines.<br>v36 (fix-36 sweep): dropped as supporting "no conjunct". The sentence stays in INV-123/Q01, inside the longer OUT-024 quote. | **Text return, not oscillation.** One return in a bookkeeping field, with no effect on meaning, Realises (OUT-024) or level. The citation now sits with the item that ties formulations (INV-123, the formulation ties of fix 17, which post-date fix 11). Fix 36's reason is imprecise: the citation dates from v11, not v15, and fix 11 had cited it for the line placement that INV-078 still states. Watch point 12. |
| **INV-031** | `omn` v00, v04, v24, v35; Conformance, Realises, Evidence v36 | v35: the two nesting bounds go to INV-122 (by dates, `daysOf`), and the mark-completeness conjunct is removed (CHG-04).<br>v36: Conformance, Realises and Evidence follow the predicate (R36-02). | CHG-04: see the next section. The bookkeeping is consequential. "A mark implies 0" stays verbatim (check 24, watch point 1). |
| **INV-033** | v00 … v24, v35, v36 | v35: the bounds go to INV-121 and INV-122.<br>v36: Conformance and Realises follow (R36-02). | Consequential; not a reversal. |
| **INV-050** | v00, v03, v05, v31, v35 | v35: the series placement goes to a W2 marker (E-039 `series` `shown SHOULD`), and the conditional review-window conjunct is removed as implied (CA-05). | No admitted or conformant set changes (next section). The start ties and `fillsPeriod` are verbatim (check 08, watch point 4; check 12, watch point 5). |
| **INV-060** | v00, v10, v35 | v35: antecedent `∧ ch.compared.period.lengthDays ≥ shortestMonthlyDays` (CHG-03). | First change of a settled point; next section. |
| **E-049 `onTreatmentPeriod` `when`; INV-070** | E-049 v35; INV-070 v17, v26, v27, v28, v31, v35 | The INV-070 presence ask moves into the `when` clause as a second disjunct. | Equivalent move, allowed by check 28 (next section). |
| **INV-087, INV-124, E-060 `shownDayOnes`** | INV-087 v00–v04, v35; INV-124 and `shownDayOnes` new in v35 | INV-087 loses only the attack placement (now a W2 marker on `attacks`). INV-124's first conjunct is new (CHG-01). | Next section. INV-087's lead-in conjunct and view rules are verbatim since v04. |
| **INV-089** | … v21, v23, v24, v35 | The bout–remission conjunct (within a view) is removed; INV-124's third conjunct states it for the whole output (CHG-02). | Next section. `ongoing`, `lastDay` (as-of date), `e ≤ ctx.asOf`, the `plusMonths` form with SD-FX-07 = 3, `onlyOfType` and the rate relation are verbatim. |
| **INV-111** | v24, v35 | Third conjunct (CHG-06). | Next section. |
| **INV-021, INV-065 → INV-119 (C2-03, C2-06)** | v00; merged v35 | Annotation disjunct of `presents` (CHG-07). | Next section. |
| **INV-056, INV-068** | … v35 | The treatment and start facts move from MUST to definitional in INV-123 (CHG-R1). | Next section. |
| **INV-123 `usedScope`** | new v35 | Positive acute-medication day counts tied to the context (CHG-05). | Next section. |
| **INV-064, INV-073, INV-085** | v35 | Reformulated with SD-CL, SD-ET and SD-SR. | Equivalent. The four control-level ranges, the minimum of 3 months for optimal control and the forcing of "insufficient" above 6 days are as in v34, with `insufficientControl` unbounded (the settled point "no more than six days required"). Early time points: 15 minutes exactly for cluster-only scopes, otherwise 2 hours. Screening ranges: HADS 21 + 21, PHQ-9 27, GAD-7 21. |
| **E-009, E-028, E-032, E-041, E-045, E-057, E-059 values** | v35 | Values moved to source-data tables. | Verbatim (method, step 4). The E-041 rule values, `ages`, `timing`, anchors and `excludes` are those of v34 (checks 08, 12 and 16). The E-045 constants likewise. |
| **Readings of INV-008, INV-037, INV-038** | INV-008 v00, v12, v24, v35; INV-037 v00, v10, v11, v35; INV-038 v00, v11, v35 | v35 drops the consequence clauses written by fix 11 ("in the comparison's view …", "Together with INV-003, this places every value of a comparison in the comparison's view") and fix 24 ("with INV-111, it states one definition for each"). | Not a reversal. Prose that restates other items is dropped under PROCESS.md section 6a. The predicates are byte-identical, and the derivations remain stated in RATIONALE (E-037/D01, E-043/D01, INV-111/D01) and in the INV-008 Notes. Co-presence (check 12, watch point 3) is formally unchanged. |
| **E-049 Meaning** | v26, v27, v35 | v35 drops fix 27's sentence ("where the context states no start for the course as it was first started, … the view shows no period as the original pre-treatment baseline"). | Not a reversal. R-MCF clause (1) (section 3.8) states it for every unstated fact, `originalStart` included (PROCESS.md section 6a, "one general treatment"). The decision is verbatim in the formal text: E-049 `baseline` `SHOULD when originalStart(ctx, self.treatment) ≠ ∅`, and INV-112 `∀ b ∈ v.baseline • ∃ s ∈ originalStart(…) • b.end < s` (check 28, watch point 2). |
| **INV-105 Reading** | v00, v02, v04, v05, v12, v13–v16, v22, v32, v35 | v35 drops "which is a lead-in (E-060) where the overview shows no first day of menstruation on or before the first day of that period" (CA-16). | Not a reversal (next section). |
| **Readings of INV-027, INV-055, INV-071, INV-102, INV-104, INV-105; E-067 Meaning** | v35 (CA-08) | "that has started" → "whose start the context states", and `courseOverlaps` worded the same way. | Not a reversal. The wording changes only the start-aligned preventive parts. The acute part of INV-105 and `courseNotOutside` keep fix 16's "a course whose start the context does not state counting as started" (check 16, watch point 1). The `omn` blocks are byte-identical. |
| **E-019 Meaning** | v00, v35 | The ICHD-3 definition of attacks is no longer part of the Meaning. Attacks are counted under the view's one definition, and INV-125 (SD-DF-02) asks at SHOULD for the ICHD-3 label (CA-10). | First change. It aligns E-019 with the E-016 and E-017 wording that fix 24 chose. INV-010's level (SHOULD) is kept as SD-DF-02. |
| **ISS-12 Effect; INV-089 Reading; E-062 and E-063 entries** | ISS-12 v21, v35 | "A remission period shown lasts more than three months" → "… that shows its start date …; every fully conformant output shows that date" (CA-06). | First change. Text-only watch item (check 24, watch point 7) with an added qualification; no earlier wording restored (the phrase occurs in no snapshot before v35). E-063 is not re-tied (fix 02, item 14). |
| **INV-003 Notes, "Period atoms with the same dates"** | v24, v35 (now INV-003/D02) | The agreement is limited to counts, completeness, the combined indication and cluster rates (CA-12). | Not a reversal: fix 24's sentence is qualified toward its predicates. No output-wide agreement is added (check 24, watch point 1). |
| Section 2.8 prose | v35 (CA-18; one reference in the equivalence fix) | "the week convention of the output" → "of the diary (one convention for all its outputs)". | Text only. The 2.8 block is byte-identical since v17 (check 24, watch point 4). |
| v35a → v35 (equivalence fix) | v35 | E-045 brace (EQ35-01); S-035 URLs (EQ35-02); ISS-03 and E-044/D01 qualified by CHG-03 (EQ35-03); references to the new places of moved conjuncts in 32 RATIONALE entries, the INV-069 and INV-071 Readings and ISS-11 (EQ35-04); the INV-118 to INV-120 and INV-124 Readings (EQ35-05). | Corrections of the rewrite. The ISS-03 qualification is required by an intended change and restores no earlier wording. E-049/D03 keeps "aligned to the event, not to the start". |
| **RATIONALE Source URLs** ([S-010] 13 entries; [S-015] E-008/Q00, INV-001/Q00, ISS-11/Q00, E-041/Q01; [S-008] in E-008/Q00) | v35 (introduced), v36 | v35 gave the PubMed abstract URL for [S-010] full-text quotes. v36 gives the univaq full-text PDF, and the CG150 Overview page for the population phrase (R36-01). | Not a reversal. v34 stated no URL for these quotes; its search log records the univaq PDF as the text used. v36 follows that basis, and v35's URL was an error of the rewrite. |
| INV-082 and INV-085 Notes "R-MCF (4)."; INV-122 and INV-123 Evidence and Notes; INV-079 Evidence and Q00; INV-122/Q01, INV-123/Q01 | v35 (added), v36 | Evidence and R-MCF pointers follow the conjuncts moved in v35 (R36-02 class). | Consequential. INV-079 keeps fix 28's `∀ d ∈ l.duration • startOf(…) ≠ ∅` and fix 30's duration conjunct verbatim. |
| Rows OUT-006, OUT-011, OUT-013, OUT-027, OUT-036; OC-08 Realises; section 9 row INV-036 | v35, v36 | Recomputed from the Realises fields; OUT-013 removed from OC-08; E-034 `event` added as a destination of INV-036. | Consequential; no requirement loses coverage (fix 36). |
| Section 2.5 References; section 3.3 item 5; section 4.1 (layer 3 and two sketch lines); section 4.2; section 6.0 "Not marked" | 2.5, 4.2, 6.0 new in v35; 3.3 item 5 and the sketch lines unchanged v00–v35; all changed v36 | Prose brought to the formal text (R36-03 and its sweep). | Single changes. The sketch line `TreatmentHistoryView ⊃ ClassGroup`, unchanged since v00, became `→`; the audit had noted it as "notationally mixed, not counted". |

## Watch points from earlier checks

| Source | Watch point | State in v36 |
|---|---|---|
| Check 32, wp 1 | Identity ties and "truth of a shown fact": INV-112 to INV-117; the INV-079 conjuncts of v30 and v32; INV-082 and INV-085 availability; fix 32's attribute table; the ties declined | **Intact, with one boundary change.**<br>• INV-112 bounds verbatim; INV-114, INV-115 and INV-116 byte-identical; INV-113 and INV-117 merged verbatim into INV-123 (definitional); availability in INV-123.<br>• INV-079 keeps fix 30's duration conjunct and fix 28's `∀ d ∈ l.duration • startOf(…) ≠ ∅`; option (b) of R30-01 not taken.<br>• No tie moved down. CHG-R1 moves two MUST conjuncts up.<br>• Declined ties still untied: fix 18 (evaluated periods), fix 17 (summary formulation), E-063 and E-058, INV-078 grouping and INV-035 at SHOULD (W2 markers `shown SHOULD`), and adherence windows not bounded by the stop.<br>• `E-046.comparison` stays `opt`.<br>• **Changed:** CHG-05 moves "acute-medication days of a drug or class" (count above 0) from fix 32's "not in the class" row into the class (next section). |
| Check 32, wp 2 | Named criteria: INV-116, `K = n` not taken, forced "non-responder" (`set1`), open list | Intact. INV-116 and INV-063 byte-identical; `namedCriteria : set1 … ≙ table SD-RC` with the six constants verbatim; `ResponderCriterion` open. |
| Check 32, wp 3 | Comparability | Intact and tightened (v33, R33-01). INV-027, INV-039, INV-069 and INV-105 byte-identical. INV-018 and INV-029 became C1-07 and C1-14, availability only. |
| Check 32, wp 4; check 28, wps 1–5 | Treatment-course cluster | Intact.<br>• INV-001, INV-103 and section 2.8 byte-identical.<br>• E-008 changed only by additions (`ShownFact`, `inMedicationScope`, `stated`), so `resumes`, `resumesFrom`, `originalStart` (no fallback) and `courseBegunBy` are verbatim.<br>• INV-112 bounds verbatim.<br>• The start-tied bounds of fix 28 are verbatim (INV-078 all pairs; INV-068 `∃ s`; `courseBegunBy` counts unchanged).<br>• The INV-070 presence ask is now a disjunct of E-049's `when` clause, for unstated starts only, at SHOULD. Check 28 wp 1 names this move "not a reversal", and wp 5 allows the merge.<br>• The three fix-28 sentences that fix 29 corrected occur in neither file. |
| Check 32, wp 5 | Earlier watch points | See the rows below. |
| Check 32, wp 6 | Volume and fixer sweeps | Formal volume fell: 4, 0, (restructuring), 0 blocks. Sweeps: fix 33 (E-033), fix 34 (ISS-03), fix 36 (INV-078, INV-082 and INV-085 Notes, E-041/Q01, E-008/Q00, sections 3.3 and 4). None reverses a fix's stated reason. Fix 36 changed E-008/Q00, which review 36 had listed as "checked and not raised", by adding a Source line, with a stated reason. |
| Check 28, wp 6; check 24, wp 1 | By-dates relations | Intact. `daysOf` by dates; INV-006 byte-identical; INV-122 quantifies over `daysOf` and keeps INV-030's `sameSpan` verbatim. The INV-031 "mark implies 0" conjunct is verbatim. The INV-031 *completeness* conjunct was removed (CHG-04): deletion is not one of this watch point's triggers (atom identity), but see the next section. No output-wide agreement of counts. |
| Check 24, wp 2 | INV-111 and INV-008 | Intact. INV-008 byte-identical. INV-111 gains a third conjunct (CHG-06), which is option (a) of R24-02, not the per-value definitions of option (b). |
| Check 24, wp 3 | Cluster view | Intact. INV-089 differs from v34 only by the bout–remission conjunct, now in INV-124. `lastDay` uses the as-of date, which keeps INV-124 consistent across views. No placement of the cluster view's references (fix 11; CA-09 kept). |
| Check 24, wp 4 | Day convention and stop bounds | Intact. Section 2.8 block byte-identical; `notStoppedBefore`, `intervalOnTreatment` and `evaluatedOnTreatment` unchanged. The stated-start disjunct of E-049 is v34's verbatim: a stop on the start day asks for the period, and a reduction on the start day does not. |
| Check 24, wp 5; check 12, wp 5; check 08, wp 4 | `fillsPeriod` and INV-050 | Intact. E-006 byte-identical (28-day anchor). INV-050 keeps the start ties and `fillsPeriod`. Its review-window conjunct is removed as implied, which changes no admitted or conformant set, so it is not a "third change in either direction". |
| Check 24, wp 6 | Formulation ties | Intact. The INV-075 and INV-079 formulation conjuncts are the `usedMedication` members of INV-123, definitional as before; INV-074 byte-identical; fix 17's declined tie not added. |
| Check 24, wp 7 | Text-only entries | Intact. E-057 Notes moved verbatim. ISS-02 unchanged. ISS-03 changed its location (v34, new evidence) and its OUT-019 bullet (CHG-03 qualification). ISS-12 qualified (CA-06). No earlier wording restored. |
| Check 24, wp 8; check 16, wps 1–7 | INV-105 with E-067; history-wide `acuteMedications`; E-062 `acute`; E-045 `valueAvailable`; acute and adherence identity ties; responder labels; E-041; INV-098; co-presence; menstrual-relation view; withdrawal follow-up; E-008 time frames | Intact.<br>• INV-105, E-067, E-062, INV-066, INV-069, INV-071, INV-088 and INV-104 byte-identical.<br>• INV-062 and INV-109 lost only placements (W2).<br>• E-041 values verbatim in SD-ER; `applicable` and `AgeCoverage` unchanged.<br>• INV-098 = C3-11, the same bearers, with `ctx(outputOf(v))`.<br>• INV-049 byte-identical. E-008 time frames unchanged.<br>• Fix 16's acute "counting as started" kept in prose (CA-08). |
| Check 24, wp 9 | Volume; "text claims more than predicate" on items aligned in v22–v24 | CA-16 is such a finding on the INV-105 Reading. It concerns a v04 clause that the v22 alignment did not touch (the v22 change was the 28-day phrase). Not cycling (next section). CA-06 concerns E-063 and INV-089 prose that was qualified, not re-aligned. |
| Check 24, wp 10 | Periods beyond the as-of date | Intact. INV-124 constrains phases only. The CA-05 prose states that the review window may lie after the as-of date, consistent with the settled point. |
| Check 12, wp 1; check 08, wps 1–3, 8 | E-041 `excludes`, ages, timings, rule-list boundary, `ruleRuChildren`, Turkish rules | Intact: all 18 SD-ER rows equal the v34 constants (ISS-10 unchanged). |
| Check 12, wp 2; check 08, wp 5 | Responder labels | Intact. `UnderlyingKind` and `PeriodValueKind` open; `otherValueNamed` 2; `#L.evaluated = 1`; the `evaluationResult`/`pretreatmentBaseline` pair; `rc.treatment = L.treatment`; `allTypes`; `attackScope`. The `scopeFor` paraphrase of R10b-02 is intact in the INV-063 Reading (byte-identical) and in E-045's "Type scope" entry (moved verbatim). |
| Check 12, wp 3 | Co-presence | Intact. INV-003 byte-identical. INV-054 → W2 marker `shown MUST when ofResponseComparison(self)`, so values of changes outside response comparisons are still not required in the view (R10b-01). INV-078 keeps the line placement; the group placement → W2 at SHOULD. |
| Check 12, wp 4; check 08, wp 7; check 04, wp 1 | Menstrual-relation view: start of the view, lead-in, no subject-level `menstruates`, no line without menstruation, the sequence in the view | Intact. INV-087 differs from v04 only by the W2 move. CHG-01 adds output-wide non-contradiction of shown day 1s, extending the lead-in rule's own ground (fix 04). It does not move the sequence into other views, and does not restrict the lead-in beyond "no shown day 1 inside it", which E-060's Meaning already states. |
| Check 12, wp 6 | E-008 time frames | Intact (E-008 changed by additions only). |
| Check 08, wp 6 | v08 sweep items | Intact. INV-100's indicators are C3-05, C3-07, C3-08 and C3-10 (OUT-026, OUT-033); E-013 `otherCompletenessExpression` unchanged. The `namedCriteria` gloss is superseded by INV-116 (check 32). |

## Restructuring and intended changes

**CHG-01** (INV-124 conjunct 1, E-060 `shownDayOnes`; R35-01).
- **Not a reversal.** No earlier remark or fix considered overlapping cycle lines. Review 35 states this, and my search of the menstrual-view remarks and fixes of iterations 02 to 05 found none either.
- Fix 02 (item 8) kept "the sequence structure, the overlap with the covered period and `completeCycles`" in the menstrual-relation view. CHG-01 keeps that: it forbids contradictions between lines, not non-consecutive lines.
- It applies fix 04's own ground for the output-wide lead-in rule ("all views of one output summarise the same diary information as of one as-of date").
- The remaining exception (lines that have not ended) is stated. Closing it by restricting lead-ins was rejected because it would reverse check 12, watch point 4 (plan, section 15.3).

**CHG-02** (INV-124 conjuncts 2–3; the INV-089 bout–remission conjunct).
- **Not a reversal.** INV-124's third conjunct is the removed INV-089 conjunct, with the same body, over all items of the output, so it implies it.
- Every term of check 24, watch point 3 is verbatim.
- It depends on `lastDay` being the as-of date (the v23/v24 decision), which it therefore reinforces.

**CHG-03** (INV-060 antecedent `≥ 28` days; ISS-13). **Not a reversal; a first change of a settled point.**
- **Trace.**
  - INV-060 asked for the residual burden next to every percentage change from v00 to v34. INV-061 made that impossible for compared periods under 28 days.
  - Fix 02, item 14 ("Considered and not changed") kept both, on three grounds: no invariant requires such a change; a residual "per month" within a shorter period does not exist; INV-061's design came from R01-03.
  - About twenty reviews between iterations 03 and 30 listed the point as settled (03, 10b, 11, 12, 15 to 19c, 21, 22b to 25b, 27 to 30).
- **The change.** CA-01 (audit) classed the unmeetable SHOULD as a contradiction, because E-040 Conformance and row OUT-019 claimed the burden "next to every such change" with "full" coverage. v35 narrows INV-060's antecedent instead of the prose.
- **Why not oscillation.**
  - The state changed once. No earlier version had the restriction, so nothing is restored.
  - Fix 02's second ground (no per-month value within a shorter period) is the premise of the change, and INV-061 is byte-identical.
  - The new element is that the model's own text claimed what the predicate excludes. Fix 02 did not consider this, because those claims were written later.
  - The decision was taken under the human's instruction to restructure (plan, section 15.1), and the open question is in section 8 as ISS-13.
- **Effect.** Widens the fully conformant repertoire only; MUST is unchanged.
- The point is now argued both ways (fix 02 against CA-01): watch point 1.

**CHG-04** (INV-031: the mark-completeness conjunct removed). **Not a reversal.**
- **Trace.**
  - The conjunct was in v00 (the author's draft). No remark asked for it.
  - Fix 24 rewrote it by dates (`sameSpan`) so that it stayed satisfiable with date-based `daysOf`; it did not argue for keeping it.
  - Reviews 21, 21b and 22 let it stand: "satisfiable", "keeps the marking of one view consistent".
- **New reason.** Section 3.3, item 5 (in the model since v00) says that a definitional invariant "cannot make an element more or less required". The audit showed the conjunct does exactly that for the MAY element E-022. No earlier review weighed it against that rule.
- **What stays.**
  - "A mark implies a count of 0" is verbatim.
  - INV-104 (SHOULD), unchanged, still asks for the marks of the clinician summary; fix 01's R01-09 (b) placed this requirement there.
- The admitted set widens. No earlier version admitted these outputs, so this is not a re-widening.
- Re-adding the conjunct at definitional level would be A → B → A (watch point 2).

**CHG-05** (INV-123 `usedScope`: a shown acute-medication day count above 0 implies the context lists a medication of that scope). **Not oscillation; the closest approach of this check.**
- **Trace.**
  - Review 27 saw the case: an indicator for a class never used makes INV-046 unsatisfiable. It wrote: "the output states false medication days anyway. Excluding it is harmless … Not raised".
  - Fix 32's attribute table (R32b-02 sweep) listed "acute-medication days of a drug or class" among "derived counts … values obtained from diary information", "not attributes that name or presuppose a context fact", with "A count of 0 … is a correct value … no remark has asked it to. No change".
  - CA-03 showed that two guarantees that INV-046's Reading and Notes state fail without this tie: the ICHD-3 single-class rule, and "the two directions agree". INV-046 then becomes unsatisfiable for an admitted output.
- **Why not oscillation.**
  - The model changed once: no tie in v00–v34, a tie in v35. Nothing was removed and nothing restored.
  - The new reason is the dependence of INV-046's stated guarantee on these counts, which fix 32's table did not consider; its premise "no remark has asked" no longer holds.
  - Fix 32's own ground is kept: a count of 0 stays admitted (`m.days > 0`), as do fix 17's declined summary-formulation tie and the 0-attack summaries of E-051.
  - INV-123/D01 states the new boundary: positive acute-medication day counts in the class; treated attacks, overuse basis, cycle-line menstruation days and values of one type scope out.
- **Check 32's criterion.** Check 32, watch point 1 asked that a new member found among the attributes that fix 32's table lists outside the class be treated as a sign that the sweeps cycle. Formally that happened. In substance, the class boundary moved once, for a reason specific to INV-046, and the plan put the membership policy to the human (section 15.8). Watch point 3.

**CHG-06** (INV-111 conjunct 3; CA-07). **Not a reversal.**
- R24-02 option (a) asked: "where both views state a definition for the measure, the two are the same". Fix 24 implemented this as conjunct 2, for the view of the change against the view of its values.
- CA-07 found the case of two values in two views, which fix 24's satisfiability sentence assumed away. CHG-06 extends the same option to it.
- INV-008 is byte-identical. Per-value definitions (R24-02 (b)) are still not taken.
- The fully conformant repertoire is unchanged, because INV-008 could not be met by those outputs.

**CHG-07** (annotation disjunct `presents` for C2-03 and C2-06). **Not a reversal.**
- INV-021 and INV-065 were unchanged from v00 to v34, without the annotation disjunct that INV-048 and INV-084 had from v00.
- No loop file discussed the difference.
- First change; it narrows full conformance at SHOULD NOT only.

**CHG-R1** (the INV-056 and INV-068 treatment and start facts: MUST → definitional). **Not a reversal.**
- Fix 31 moved only conjuncts of SHOULD invariants. Fix 32's table records these two facts as "tied" at MUST and argues nothing for keeping MUST. No level had changed before v35 (check 32).
- Check 32, watch point 1 names only moves *down* as reversals.
- The MUST-conformant and fully conformant repertoires are unchanged: an output with a false fact failed MUST in v34 and is not admitted in v35.

**The E-049/INV-070 merge.** **Allowed by check 28 and equivalent.**
- v34 at SHOULD: the attribute constraint `φ₁ ⇒ P` together with INV-070's `∀ x ∈ firstChangedDay(…) • φ₂(x) ⇒ P`.
- v35: `(φ₁ ∨ ∃ x ∈ firstChangedDay(…) • φ₂(x)) ⇒ P`.
- These are logically equal for any `firstChangedDay`, since `(∀ x • φ₂(x) ⇒ P) ≡ ((∃ x • φ₂(x)) ⇒ P)`, at the same level (SHOULD, fix 26).
- The stated-start disjunct is v34's verbatim.
- Check 28, watch point 1 names exactly this move "not a reversal", and watch point 5 allows the merge.
- E-049/D03 keeps "aligned to the event, not to the start". INV-070 keeps its baseline and `shownDay` conjunct at SHOULD.

**Audit-driven changes.**
- **CA-05 (kept as settled).**
  - E-039 `reviewWindow` has been `SHOULD` without `when` since v00. Fix 02, item 14 called it consistent with INV-050's conditional conjunct, and later reviews list it as settled.
  - v35 removes the implied conjunct and states the attribute's reading in prose. The audit's suggested `when` clause was not added, which would have reversed the settled point.
  - The v05 change-log wording "required once the covered period reaches its end" described the redundant conjunct. No formal state changes.
- **CA-06 (prose only).** E-063 and E-058 are not re-tied (fix 02, item 14). The ISS-12 qualification is new text.
- **CA-09 (kept).** No placement of the cluster view's references; the INV-088 Reading now says "refers to". This is fix 11's decision ("no change": OUT-031 asks for no one view).
- **CA-13 (kept).** INV-035's ties stay at SHOULD (E-035 `shown SHOULD`) and INV-041's definitional (E-038 `shown`), as reviews 31 and 32 and check 32 settled.
- **CA-08.** Applies only to start-aligned content (R-MCF (1)); fix 16's acute reading is kept.
- **CA-10.** First change of the E-019 Meaning, in fix 24's wording.
- **CA-11.** The comments of sections 2.3 and 3.2 become normative sentences; same content.
- **CA-12.** Qualifies fix 24's sentence.
- **CA-14, CA-15.** Satisfiability and Notes sentences corrected to their predicates.
- **CA-16** (INV-105 Reading).
  - Fix 04 wrote, for R04-01: "the per-line rules apply in every view, so a lead-in *satisfies* INV-105 for an overview of a week before menarche". The Reading's "which is a lead-in where …" stated it as a requirement that no version's predicate had.
  - v35 moves the remark to INV-105/D04 as one way to meet the conjunct, which is fix 04's own statement.
  - The clause was outside the v22 alignment of check 24, watch point 9. So this is a first correction of a v04 overclaim, not cycling.
- **CA-17, CA-18, CA-19, CA-04.** Text corrections; single changes.
- **CA-01, CA-02, CA-03, CA-07.** These are CHG-03, CHG-04, CHG-05 and CHG-06.

**Equivalence-check defects (EQ35-01 to EQ35-05).** All are corrections of the rewrite: a brace, URLs, prose made false by CHG-03, references to the new homes of moved conjuncts, and Reading overclaims. None changes an `omn` block other than the brace, and none restores an earlier state.

**Deviations D-1 to D-18 of fix 35.** Layout and prose. D-11 and D-12 kept the sentences that the watch points quote.

## Findings

None. No item oscillates, so no OSC finding is raised, nothing is frozen, `FROZEN_ITEMS.md` is not written and `OUTPUT_MODEL.md` is not changed.

The closest approaches are assessed above:
- CHG-05, against fix 32's attribute table;
- CHG-03, against fix 02, item 14;
- CHG-04, against reviews 21, 21b and 22 and fix 24;
- INV-078 Evidence, against fix 11;
- CA-16, against check 24, watch point 9.

Each is one change, with a reason that the earlier decision did not consider. None has been reversed, and none restores a state that an earlier fix deliberately set.

## Trend and looping assessment

**Remark counts per iteration, 25–36:** 0 + 1, 1, 1, 2, 1, 1, 1, 0 + 3, **2, 1, 1, 3**.
- Iteration 35 also had the audit (19 findings) and the equivalence check (5 defects), both handled as remarks.
- The last NO_REMARKS main review was iteration 32's; its re-check found 3 remarks.

**Change volume** (`volume.py`; same granularity as check 32):

| Version | v29 | v30 | v31 | v32 | **v33** | **v34** | **v35** (restructuring) | **v35 corrected** | **v36** |
|---|---|---|---|---|---|---|---|---|---|
| Top-level items changed | 3 | 3 | 17 | 18 | **8** | **2** | 190 (38 withdrawn, 8 new) | **9** | **11** |
| `omn` blocks changed | 0 | 1 | 8 | 11 | **4** | **0** | 105 (59 edited, 38 removed, 8 new) | **1** (a brace) | **0** |
| Traceability, catalogue and table rows | 0 | 1 | 4 | 8 | **4** | **0** | 252 (new layout) | 0 | **7** |
| RATIONALE entries changed | — | — | — | — | — | — | 432 new | **32** | **21** (2 new) |

**Topics.**

| Area | Remarks 33–36 (and audit/EQ) | Pattern | Assessment |
|---|---|---|---|
| Treatment courses (INV-001, E-049, INV-064 to INV-070, INV-079, INV-103, INV-109, INV-112) | none from reviewers. Audit: CA-08 (wording), CA-14 (a satisfiability sentence); the E-049/INV-070 merge; CHG-R1 | No predicate of the cluster changed except by equivalent moves. | Converged (the cascade ended at v28, as check 32 found). |
| Truth of a shown fact (INV-123) | none from reviewers (review 34 declined to widen it to cycle-line days). Audit: CA-03 → CHG-05 | The reviewer cascade R30-01 → R31-01 → R32b-02 stopped. The class now has one rule and an explicit member list. One member was added from the "not in class" side (CHG-05). | Converging; boundary to watch (watch point 3). |
| Comparability | R33-01 (after R32b-03); fix-33 sweep E-033 | Two remarks in a row, each tightening in one direction; none since iteration 33. | Converged for now. |
| Value-set facts that constrain nothing | R33-02 (after R32b-01) | Fix 33's sweep of 102 names and 15 axioms found no other case; none since. | Converged for now. |
| Citations (locations, URLs) | R34-01 (location); fix-34 sweep (ISS-03); EQ35-02 (truncated URL); R36-01 (wrong page) | Different defects. The first two predate the restructuring; the URL defects come from the rewrite. Fix 34 checked all 142 locations; fix 36 checked all 303 fragments of the 113 Q entries against their URLs (18 unreadable in v35, 0 in v36). | Not circling one point; the sweeps are now exhaustive for their classes. |
| Bookkeeping and prose after the restructuring | EQ35-01 to EQ35-05 → R36-01, R36-02, R36-03 | **Self-widening by one step.** Each equivalence-fix sweep was scoped to its defect's narrow class: URL in the source row, prose references, generic Readings. Review 36 found the adjacent class: URL readable, Conformance/Realises/Evidence of trimmed invariants, notation prose. Fix 36's sweeps cover all Q entries, all 29 edited invariants (a table) and sections 2–4. | The one live cascade. It concerns no formal content. Watch point 12. |
| Menstrual relation | R35-01 (first remark on the area since iteration 04) | New case (cross-view consistency); resolved by CHG-01 on fix 04's ground. | New; one direction. |

**Did the restructuring change the trend?**
- **Remark count.** Not yet: 3 remarks in iteration 36, against 1–2 before it. All three are defects introduced by the rewrite. None concerns the formal content, a source value or Stage 1 fidelity.
- **Formal stability.** It improved. Neither v34 nor v36 changes an `omn` block; the last versions without a formal change were v19, v20 and v29. The restructuring's formal changes are the eight listed CHGs plus moves.
- **Accretion.** The model shrank from 822 KB (v34) to 422 KB (v36), with 322 KB in `RATIONALE.md`. Prose that restated other items, which the audit found was the main site of contradictions, was dropped (139 sentences, 31 KB) or moved to `RATIONALE.md`.
- **Monotonicity.** Check 32 found every change monotone narrowing. v35 adds two deliberate widenings (CHG-03 at full conformance; CHG-04 in the admitted outputs), each with a stated reason. Neither returns to a set an earlier version admitted, so no admitted set *re*-widens.

**Judgement.**
- **No looping in content.** The areas that drew earlier cascades (treatment courses, shown facts, comparability, value sets) have produced no reviewer remark since iteration 33. Every change of v33–v36 aligns text, adds a constraint, moves a constraint equivalently, or is a listed intended change with a stated reason.
- **Not converged in rate.** The loop has not had a NO_REMARKS main review since iteration 32, and iteration 36 rose to 3 remarks.
- **The question for iterations 37–40** is whether the post-restructuring bookkeeping cascade ends with fix 36's sweeps. If iteration 37 again finds bookkeeping or RATIONALE-agreement defects in classes that fix 36 swept, the transcription defects are not exhausted; a one-off agreement audit of RATIONALE against the model (PROCESS.md section 6a) would end the cascade faster than remark-by-remark fixes.

## Watch points for the next check

1. **CHG-03 / ISS-13** (INV-060 antecedent `ch.compared.period.lengthDays ≥ shortestMonthlyDays`).
   - The point is now argued both ways: fix 02, item 14 against CA-01. It belongs to the human (ISS-13).
   - **Oscillation, to be frozen:** restoring INV-060's unrestricted antecedent, or adding a per-month residual for shorter periods, before the human decides ISS-13.
   - **Not a reversal:** a change made by the human's decision on ISS-13.
2. **CHG-04** (INV-031 completeness conjunct removed).
   - **Oscillation (A → B → A):** re-adding it at definitional level.
   - **A new decision needing a Stage 1 SHOULD basis** (plan, section 15.4): adding it at SHOULD for every view that marks such periods.
   - "A mark implies 0" and INV-104's marks must stay.
3. **The class of INV-123** ("truth of a shown fact"; INV-123/D01).
   - **Reversals:** removing `usedScope`, or moving any member below definitional (including the CHG-R1 facts back to MUST).
   - **Widening the class again:** tying another derived count that INV-123/D01 lists "not in the class" (treated attacks, overuse basis, cycle-line menstruation days against `menstruationSpans` (declined in review 34), values of one type scope). That is the second redraw of fix 32's boundary. Ask whether the class has an end, and treat it as cycling unless it rests, like CHG-05, on a stated guarantee that fails.
   - **Cycling:** any tie of a count of 0, or of a summary with 0 treated attacks (fix 17, fix 32).
   - The plan (section 15.8) put the membership policy to the human.
4. **INV-124 (CHG-01, CHG-02).**
   - **Reversals:** restricting it to one view (option (b)); moving the menstrual sequence structure into the overview; closing R35-01's remaining exception by restricting lead-ins (check 12, wp 4); making `lastDay` relative to the covered period again (check 24, wp 3), which would also break INV-124 across views.
5. **CHG-06 and CHG-07.**
   - **Reversals:** lowering INV-111 conjunct 3 to SHOULD or dropping it; removing the annotation disjunct of `presents` for C2-03 and C2-06.
   - **Still not taken:** per-value definitions (R24-02 (b)).
6. **The E-049 `onTreatmentPeriod` `when` clause.** Check 28's watch points 1, 2 and 4 now apply to it.
   - The stated-start disjunct must stay verbatim.
   - The unstated-start disjunct must stay at SHOULD.
   - Splitting it back into an invariant is not a reversal if equivalent.
   - Fix 27's decision is now carried by E-049 `baseline` `when`, INV-112 and R-MCF (1). Removing any of them would admit a baseline without an original start (check 28, wp 2).
7. **CA-05** (E-039 `reviewWindow`).
   - **Reversal:** adding a `when` clause, or restating "required once the covered period reaches its end" as a requirement (fix 02, item 14; settled).
8. **CA-16 / INV-105.**
   - **Cycling (check 24, wp 9):** re-adding the lead-in clause to the Reading as a requirement.
   - **A new decision, not supported by fix 04:** a predicate that requires the overview's first line to be a lead-in.
9. **Source data tables** (SD-ER, SD-RC, SD-GB, SD-IN, SD-CL, SD-CLS, SD-CMB, SD-FX, SD-SR, SD-ET, SD-DF). They now carry every watched value (E-041 rules, named criteria, bands, recalls and ranges, control levels, overuse levels).
   - Any cell change is a change of a source value. Check it against checks 08, 12 and 16 (E-041) and check 32 (named criteria) as if it were an axiom change.
10. **Comparability and value sets** (E-023, E-025 `OtherSummary`; E-033 `otherHeadacheIndex ⟨Text⟩`; INV-082 `publishedGrading`).
    - **Reversals:** dropping the v33 conjuncts or the payload; fixing `publishedGrading` for MSQ v2.1, M-TOQ or PGIC (R03-07).
    - **A new decision:** extending a scale or form tie to INV-062's values.
11. **All earlier watch points** (checks 04 to 32), as listed in the previous section. Their triggers now apply to the v35 places of the moved conjuncts: INV-123 members, W2 markers, case rows C1–C3, E-034 and E-049 attribute types, INV-121 and INV-122.
12. **Bookkeeping after the restructuring** (R36-01 to R36-03; EQ35-02 to EQ35-05).
    - Read a further remark of this kind against fix 36's sweeps: all Q-entry fragments against their URLs; the table of the 29 edited invariants; sections 2 to 4 and the 6.0 index.
    - If it finds a case those sweeps list as checked, they missed it. If it finds a new adjacent class, for example RATIONALE D entries that no longer agree with the model, it is the third round of a widening cascade: consider a one-off agreement audit.
    - **INV-078 Evidence:** re-adding the OUT-024 formulation sentence would complete an A → B → A → B cycle.
13. **Volume and remarks.**
    - Count changes in `omn` blocks and table rows against the plan's section 11 mapping, not raw prose items.
    - Expect 0–few formal changes and falling remarks.
    - A rise in formal changes driven by sweeps, or a fourth iteration without a NO_REMARKS main review while the remarks stay in bookkeeping, should be examined for cycling.

The scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/osc36/`: `versions.py`, `split.py`, `analyse.py`, `hist.py`, `fld.py`, `omndiff.py`, `wdiff.py`, `nearret.py`, `nearret35.py`, `guar.py`, `sdcheck.py`, `blocks.py`, `levels.py`, `mapcheck.py` and `volume.py`. `FROZEN_ITEMS.md` was not written, and `OUTPUT_MODEL.md`, `RATIONALE.md` and the history snapshots were not changed.
