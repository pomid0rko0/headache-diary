# Oscillation check — after iteration 24
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: versions v00 to v24 (history/v00.md to history/v24.md; OUTPUT_MODEL.md is byte-identical to v24); reviews review-iter-01 to review-iter-24 with the re-checks 08b, 10b, 19b, 19c, 21b and 22b (30 files, 68 remarks: 12, 7, 7, 4, 3, 1, 3, 0 + 2, 1, 0 + 2, 3, 2, 3, 2, 3, 1, 3, 1, 0 + 0 + 2, 1, 0 + 1, 0 + 1, 1 and 2); fixes fix-iter-01 to fix-iter-24; the earlier oscillation checks after iterations 04, 08, 12 and 16, with all watch points of check-after-iter-16.md. Reviews 17 to 24 with their re-checks, and fixes 17 to 24, were read in full. Earlier reviews and fixes were read where they concern an item that changed in v17–v24 or a watch point: R02-01 and fix 02 item 5, R03-04, R05-01 to R05-03, R09-01, R10b-01, R11-01 with fix 11, R12-01, and the fix-04 sweeps of R04-03 and R04-04.
Date: 2026-10-22

## Method

1. **Git history.**
   - Checks:
     - each snapshot was added in exactly one commit and never changed afterwards (v17 396f418, v18 9a9587c, v19 5308800, v20 c4f0d1e, v21 06d41ff, v22 2096923, v23 ac1e28a, v24 cf8d10f; v00–v16 as in the iteration-16 check);
     - at each fix commit, OUTPUT_MODEL.md is byte-identical to that commit's snapshot;
     - the committed snapshots equal the working-tree snapshots;
     - every review, re-check and fix log was added in its own commit, in loop order, from c6719f2 (check 16) to cf8d10f (fix 24);
     - each fix commit touches only OUTPUT_MODEL.md, its snapshot and its fix log, and each review commit touches only its review;
     - Stage 1 is unchanged since bfec74f.
   - All checks passed. The working tree was clean, OUTPUT_MODEL.md equals v24, FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.
2. **Item split.** The splitter of the earlier checks, extended to 25 versions, gives 2,489 distinct items. These are:
   - the header, the sections and subsections;
   - every element, invariant and Stage 1 issue, and each of their fields;
   - every attribute and declaration of the `omn` blocks, and every E-041 rule and E-045 criterion constant;
   - the traceability rows, with their element, invariant and coverage columns;
   - the source rows, the withdrawn row, the search-log lines and the change-log entries.
3. **State trajectories** (`analyse.py`). Each item was hashed per version. The script flags every item that returns to the state of a non-adjacent earlier version after a different state in between (A → B → A, including add → remove → add).
4. **Near-return detector** (`nearret.py`, new). For every change vᵢ₋₁ → vᵢ with i in 17–24, the script tests whether vᵢ is closer, by word-level similarity, to some earlier state vⱼ (j < i − 1) than to vᵢ₋₁. This catches partial reversals that a hash cannot.
5. **Word-level diffs** (`show.py`, `show3.py`, `optypes.py`, `dels24.py`, `omn.py`).
   - Every item changed in v17–v24 was diffed word by word and classified as new, additive (no word deleted or replaced) or edited.
   - Every predicate and `omn` change was read.
   - Every deleted span of four or more words in a prose or formal field was listed and read.
   - `omn.py` counts the changed formal blocks per version.
6. **Insert/delete n-grams** (`ngram.py`, `docwide.py`).
   - Per item, and for every pair of versions vⱼ < vᵢ, the script compares 6-word n-grams in both directions: deleted at vⱼ and re-inserted at vᵢ, and inserted at vⱼ and deleted at vᵢ.
   - The same comparison was run over sections 1–9 as a whole, to catch text moved between items.
7. **Conformance** (`conf.py`, `attrtypes.py`). Tracked across all 25 versions:
   - every attribute declaration (type, level, `when` clause, `derived` mark);
   - every invariant's level;
   - the level-keyword counts of every element Conformance field.
8. **Guarantee terms** (`guar24.py`). The occurrences in v08 to v24 of 79 terms:
   - the 39 terms of the iteration-16 check;
   - the ties of v17–v24 (`next(p.end)`, `firstChangedDay(`, `notStoppedBefore(`, `intervalOnTreatment(`, `evaluatedOnTreatment(`, the formulation conjuncts of INV-074, INV-075 and INV-079, the 28-day anchor of `fillsPeriod`, `(∀ e ∈ x.end • e ≤ ctx.asOf)`, `ctx(outputOf(x)).asOf`, `sameSpan(`, `sameIndicatedPeriod(`, INV-111, ISS-03, ISS-12);
   - the conjuncts that carry R05-03, R09-01, R21b-01 and the v12 INV-003 period requirement.
9. **Watch-point items** (`wp24.py`). The trajectory of every item named in the watch points of check-after-iter-16.md.
10. **Remark topics** (`remarks24.py`).
    - The `Item(s)` of all 68 remarks were mapped to E-, INV-, ISS- and OUT- IDs.
    - The script lists the IDs named in remarks of two or more iterations, at least one of them in 17–24, and the earlier remarks each remark cites.
    - It lists every sentence of remarks 17–24 that uses revert, undo, reverse, restore, remove, drop, loosen, relax, re-raise or reopen.
    - Each remark of iterations 17–24 was read together with the earlier fixes it touches. The "Checked and not raised" lists of reviews 17–24 were compared with earlier ones.
11. **Scenario checks.**
    - `fills24.py` evaluates the series conjunct of INV-105 and INV-050 under the `tiles` form of v00–v04, the `fillsPeriod` of v05–v21 and the `fillsPeriod` of v22. It runs 1,500 random covered periods of 1 to 419 days (with extra weight on exact runs of 28-day periods and weeks), against calendar months, 28-day periods and calendar weeks (Monday first). That gives 4,276 cases with at least one whole period, every consecutive series within each, and 15,691 series that begin on the first day of the covered period, as INV-050's series must.
    - `poststop.py` evaluates the E-049 `onTreatmentPeriod` requirement, and whether a period meeting INV-070 can exist, under the forms of v00–v01, v02–v16 and v17–v24. It covers stops and reductions on the start day and later.
12. **Judgement.** Each item changed in two or more versions, at least once in v17–v24, was read against the remark or fixer change that drove each change. It was classified as convergent (one direction, earlier guarantees kept) or oscillating (back and forth on the same point).

**Results of the mechanical steps**

- **Step 3.** One item returns to a non-adjacent earlier state: `E-008.attr.SubjectProfile.aged12OrOlder` (`------AAAAAA-------------`), added in v06 and removed in v12. The iteration-12 check assessed it. Nothing new in v17–v24.
  - 1,025 items changed at least once, and 422 in two or more versions.
  - 198 items (excluding header, sections and logs) changed in two or more versions with at least one change in v17–v24. They fall into the 12 topics of the next section.
  - No item was removed after v12, and no removed item was re-added.
  - The change log is append-only (25 entries, none changed after its version). S-101 to S-106 are unchanged since v08, and no source was added in v17–v24. The withdrawn row is unchanged, and the search log is append-only.
  - `ISS-11.For the human` appears as changed in v21. This is a split artefact: the closing paragraph of section 8 ("ISS-07 was withdrawn …") now follows ISS-12 and is byte-identical there.
- **Step 4.** No change in v17–v24 moves an item closer to an earlier state than to its previous state. 0 hits.
- **Step 5.**
  - **Change types.**
    - v17: 39 edited, 15 additive, 6 new.
    - v18: 17 edited, 25 additive, 4 new.
    - v19: 3 edited.
    - v20: 6 edited, 6 additive, 2 new.
    - v21: 4 edited, 2 additive, 4 new.
    - v22: 8 edited, 3 additive.
    - v23: 8 edited, 3 additive.
    - v24: 49 edited, 18 additive, 10 new.
  - **Deleted spans of four or more words.** There are 11 in v17–v24. Each is replaced by text that keeps its content in a corrected form:
    - INV-055 Notes, INV-097 Notes and row OUT-022 (v17): the one-day re-expression under the day convention;
    - ISS-02 Evidence (v19): R19c-02;
    - ISS-03 "that are all 0." (v20): reworded as "(counts of 0) and no migraine attacks";
    - ISS-11 (v21): the artefact above;
    - E-063 Definition (two spans) and INV-089 Reading (v23): "the end of the covered period" becomes "the as-of date", R23-01;
    - INV-006 Predicate (v24, two spans): `m.period = n.period ∧` moves from the antecedent into the consequent (`… ⇒ m.days = n.days ∧ (m.period = n.period ⇒ m = n)`), so the v23 identity is kept.
  - **Formal blocks changed per version, v17–v24:** 9, 9, 0, 0, 0, 1, 2, 12.
- **Step 6.**
  - **Re-insertions within an item.** 12 hits in all; one has its re-insertion in v17–v24. In E-041 Notes, "end of a treatment cycle itself," was deleted in v14 and re-inserted in v17. This is an n-gram artefact: v17 inserts "the first day after the cycle (E-008;" inside the v14 parenthesis.
  - **Insert-then-delete.** 146 hits with the deletion in v17–v24. The 24 formal hits are all of one kind: a v17, v18, v22 or v24 edit inside a predicate that an earlier fix created, for example:
    - INV-055, INV-058, INV-059, INV-063, INV-064, INV-068: an added conjunct (v18);
    - INV-049: `≤` → `<` (v17);
    - E-042 `fitsMonthlyPeriod`: `shortestMonthlyDays − 1` → `shortestMonthlyDays` (v17);
    - E-049 `onTreatmentPeriod`: the `when` clause rewritten with `firstChangedDay` (v17);
    - `fillsPeriod`: an added conjunct (v22);
    - E-032, E-046, INV-053, INV-089: atom equality replaced by `sameSpan` or `sameIndicatedPeriod` (v24).

    Each was read: none removes a condition that an earlier fix inserted (Findings, D, for v24). The other hits are bookkeeping, or prose re-worded together with these predicates.
  - **Document-wide.** 65 n-grams were deleted from sections 1–9 and later re-inserted; 6 of them were re-inserted in v17–v24. All are generic phrases in unrelated items ("days and moderate/severe headache days of", "the same baseline and on-treatment periods,", "or before the as-of date; a"), structural boundaries (a new INV-070 Notes field after "Evidence: Stage 1 OUT-022."), or the E-041 artefact above.
- **Step 7.** No conformance level returned and none changed more than once.
  - **Attribute declarations.** In v17–v24 only two attribute `when` clauses changed:
    - E-049 `onTreatmentPeriod` (v17), its second change after v02 (Findings, B);
    - E-043 `timePoints` (v18), its first change.
  - **Invariant levels.** No invariant level ever changed. In v24 the totals are MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34 (INV-111 is new and definitional).
  - **Element Conformance fields.** No keyword count dropped.
- **Step 8.** No guarantee term occurs less often in any later version, from v08 to v24. For example:
  - `summarisesMedication(`: 14 from v15;
  - `courseNotOutside(`: 8 from v16;
  - `#L.evaluated = 1`: 7, then 8 from v18;
  - `notStoppedBefore(`: 8 from v18;
  - `plusMonths(s, remissionMoreThanMonths) ≤ e`, `onlyOfType(`, `ch.reference.period = rc.baseline` and `rc.treatmentStart ≤ p.start`: constant;
  - `v.covers.start = v.withdrawalStart`: 1, then 2 from v22 (E-006 Notes);
  - `sameSpan(`: 13, then 30 in v24.

  The atom equalities that v24 replaced in relations (for example `i₂.period = i.period`, `e.period = p`) are not guarantee terms. Each was replaced by a date comparison that every same-atom pair also satisfies (Findings, D).
- **Step 9.** These items are byte-identical since the iteration-16 check, or changed only in text:
  - **INV-105 and E-067.** INV-105 Predicate unchanged since v16; Reading and Notes changed only in v22, for `fillsPeriod`.
  - **E-008 time frames.** E-008 Definition and `acuteMedications` unchanged since v12; E-008 Meaning changed in v17 (the dates of course events).
  - **E-062 and E-045.** E-062 `acute` unchanged since v02, and E-045 Definition since v12.
  - **Acute and adherence ties.** INV-062, INV-066, INV-067, INV-069, INV-071, INV-072, INV-088, INV-104 and INV-109 Predicates, and the E-047, E-051 and E-055 Definitions, unchanged since v15.
  - **E-041.** Every `omn` declaration, rule constant and criterion unchanged since v14.
  - **INV-098.** Unchanged since v13.
  - **Co-presence.** INV-003 Predicate unchanged since v12, INV-054 since v10, INV-056 since v01, INV-078 since v11, INV-038 since v00 and the E-040 Definition since v10.
  - **Menstrual-relation view.** INV-086 Predicate unchanged since v12, INV-087 since v04, the E-060 Definition since v04 and E-061 since v00.
  - **Withdrawal follow-up.** INV-050 Predicate unchanged since v05, INV-051 and INV-052 since v00.

  The changed watch-point items are assessed below.
- **Step 10.**
  - **IDs in remarks of several iterations.** 46 IDs are named in remarks of two or more iterations, at least one in 17–24. They are led by:
    - OUT-018 (12 remarks);
    - E-041, INV-055 and INV-105 (11 each);
    - OUT-035 (11) and INV-104 (10).
  - **Reversal language.** No remark of iterations 17–24 asks to revert an earlier fix. The flagged sentences say the opposite, for example:
    - R17-02: "it loosens no tie of R13-01, R14-02, R15-01 or R16-01";
    - R21b-01: "Option (a) below changes no predicate or value, so it reverses nothing";
    - R22b-01: "Neither option reverses an earlier fix";
    - R24-01: "INV-006 and `daysOf` have been unchanged since v00, so the change below reverses no fix".
  - **Declined options.** These were not taken, and none was raised again:
    - fix 17: R17-02's optional tie of a summary's formulations;
    - fix 18: R18-01 (b), its first option;
    - fix 22: R22b-01 (a2) and (b);
    - fix 23: R23-01 (b);
    - fix 24: R24-01 (b) and the output-wide form, R24-02 (b), and the replacement of INV-008's consequent.

    No earlier declined remark was raised again. R11-01 (a)/(b), declined in fix 11, is explicitly kept by R24-01 and fix 24.
- **Step 11.** See Findings, A and B.

## Change history of items changed in two or more versions

Listed: items that changed in two or more versions, at least once in v17–v24. Items whose changes all lie in v00–v16 and that are unchanged since were assessed in the earlier checks (last row). "Fields" names the fields that changed.

| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| **Day convention and evaluation time points.**<br>Section 2.8 (v01, v17).<br>**E-042**:<br>• Definition, Meaning and Evidence (v02, v17, v18);<br>• Notes (v02, v06, v07, v18);<br>• Conformance (v18);<br>• `atTimePoint` (v17, its first change);<br>• `fitsMonthlyPeriod` (v02, v17);<br>• new `notStoppedBefore` and `intervalOnTreatment` (v18).<br>**E-041**: Meaning and Notes (v01, v02, v06, v07, v08, v12, v14, v17, v18).<br>**E-043**: Conformance (v01, v02, v11, v18); `timePoints` `when` (v18); Notes (v01 … v14, v17, v18).<br>**INV-055**: Predicate (v02, v18); Reading and Notes (v02, v06, v07, v08, v12, v14, v17, v18).<br>**INV-058**: Predicate (v18); Reading (v06, v07, v12, v18).<br>**INV-059**: Predicate (v18); Reading (v06, v07, v08, v12, v14, v18).<br>**E-008** Meaning (v06, v07, v12, v17); row **OUT-018** (v01 … v14, v17, v18) | v17, v18 (and earlier) | **v17 (R17-01, option (a)).**<br>• Section 2.8 states one day convention: a course includes its start day; a stop or pause is dated on the last day of the course; a dose change on the first day at the new dose; `cycleEnd(n)` on the first day after the cycle.<br>• A time point is the date after the interval. `atTimePoint` relates it to the period's last day (`next(p.end) = tp.earliest`), and `fitsMonthlyPeriod` is shifted by the same day.<br>**v18 (R18-01 (a)).** A time point is shown and required only where the course is taken through the interval that the time point closes (`intervalOnTreatment` in INV-058, INV-059, E-043 and INV-055). The comparison at a time point ends on or before every stop (`notStoppedBefore`). | R02-01, R06-01, R07-01 to R07-03, R08b-02, R14-01 (earlier); R17-01; R18-01 | **Convergent.**<br>• `atTimePoint` changed once in 25 versions, and section 2.8 is unchanged since v17.<br>• `shift`, the INV-058 relation of `earliest` and `latest`, and the E-041 `omn` block (every `excludes`, `timing`, `ages`, `AgeCoverage`, anchor and offset) are byte-identical since v14, so no time-point date changed.<br>• The R02-01 guard is kept: fix 17 found it exact in 53,680 cases under v17.<br>• v18 only narrows where a time point applies. Fix 18 found v18 ⊆ v17 in 40,000 random courses, equal for every course without a stop. |
| **Post-stop monitoring view.**<br>**E-049**: Definition, Notes and `onTreatmentPeriod` (v02, v17); Conformance (v02, v03, v12, v17).<br>**INV-070** (v17 only: Predicate, Reading, new Notes).<br>**INV-097** Notes (v03, v12, v17, v18); row **OUT-022** (v02, v17) | v02, v17 | **v02 (fix 02, item 5).** `onTreatmentPeriod` is SHOULD only `when ∃ s • s < self.eventDate`: "impossible for a stop, pause or reduction on the start day".<br>**v17 (fix 17's date-boundary check, the R17-01 defect elsewhere).** `firstChangedDay` (the day after a stop or pause; the day of a reduction). The on-treatment period may end on the stop date, the periods after the event begin on the first changed day, and the `when` clause reads `s < x`. | fix 02, item 5; R17-01 (the orchestrator's same-defect check) | **Convergent** (Findings, B). The requirement equals its possibility in every case from v02 on. The one outcome that returns, for a stop on the start day, follows from the v17 day convention, under which that period exists. The INV-070 baseline conjunct is unchanged since v00. |
| **Withdrawal follow-up.**<br>**INV-049**: Predicate (v05, v11, v17); Reading (v05, v11, v12, v17).<br>**E-039**: Conformance (v05, v11, v12, v17); Notes (v05, v06, v12, v17).<br>**INV-050**: Predicate (v03, v05); Notes (v05, v22) | v17, v22 (and earlier) | **v17.** "The following year" ends on the day before `plusMonths(ws, 12)`: `≤` → `<` in both conjuncts. Review 17 had called the one-day difference immaterial; fix 17 aligned it with the invariant's own Reading.<br>**v22.** INV-050 Notes: the "shrink" phrase made precise. | fix-03, fix-05, fix-11 and fix-12 sweeps (earlier); fix 17 date-boundary check; R22b-01 | **Convergent.**<br>• The v11 running-follow-up conjunct is kept.<br>• INV-050's start ties are unchanged since v05, and no end tie was re-added (iteration-08 watch point 4).<br>• INV-050's verdicts are unchanged by v22 (Findings, A). |
| **Series of whole periods.**<br>**E-006**: Definition and Meaning (v02, v03, v22); Notes (v02, v03, v05, v22); `fillsPeriod` (v03, v22).<br>**INV-104**: Reading and Notes (v01, v02, v03, v10, v13, v14, v15, v22).<br>**INV-105**: Reading and Notes (v02 … v16, v22).<br>Rows **OUT-034** and **OUT-035** (v22 and earlier) | v03, v05, v22 | **v03 (R03-04 (i)).** `fillsPeriod`: "all whole periods of its granularity within the covered period".<br>**v05 (R05-01).** INV-105's exact tiling replaced by `containsPeriodOf` ⇒ `fillsPeriod`. Fix 05 states that a run of whole periods "still spans it exactly".<br>**v22 (R22b-01, option (a1)).** 28-day series are counted from the first day of the covered period. | R03-04, R05-01, R22b-01 | **Convergent** (Findings, A).<br>• v04 ⊆ v22 ⊆ v21 in all 4,276 cases.<br>• v22 equals v04 on every exact run (768 of 768), and admits exactly one series wherever a whole period fits (4,276 of 4,276).<br>• Months and weeks are unchanged. |
| **Responder and control-level labels, treatment review view.**<br>**E-046**:<br>• Definition (v01, v02, v05, v08, v09, v12, v18, v24);<br>• Meaning (v05, v09, v18);<br>• Notes (v01, v05, v08, v09, v18, v24);<br>• `reductionMet` and `reductionDecided` (v01, v05, v09, v12, v24);<br>• `attackReductionMet` and `attackReductionDecided` (v08, v09, v12, v24).<br>**INV-063**: Predicate (v18); Reading (v01 … v12, v18).<br>**INV-064** (v05, v18).<br>**INV-068**: Predicate (v02, v18); Reading (v02, v10, v18).<br>**E-048** (v02, v03, v12, v18); rows **OUT-020** and **OUT-021** (v18 and earlier) | v18, v24 (and earlier) | **v18 (R18-01 (b)).**<br>• `evaluatedOnTreatment`: INV-064 gains it as a conjunct next to the fix-05 start tie.<br>• INV-063 forces "responder" or "non-responder" only where the evaluated period ends within the course.<br>• INV-068's on-treatment periods end on or before every stop.<br>**v24 (fix 24, other change 2).** The four component predicates match the label's evaluated periods and the comparison's baseline by dates (`sameSpan`) instead of by period atom. | R01-04, R05-02, R08b-01, R09-01, R10b-02, R11-02 (earlier); R18-01; R24-01 | **Convergent.** Every tie of iteration-12 watch point 2 is verbatim in v24 (step 8): `#L.evaluated = 1`, `conditionHolds`, `rc.treatment = L.treatment`, `ch.reference.typeScope = allTypes`, `attackScope`, the `evaluationResult` / `pretreatmentBaseline` pair and `otherValueNamed`.<br>• v18 removes forcing only past a stop.<br>• v24 extends matching only to atoms with the same dates.<br>• The v18 guard is verbatim in v24. |
| **Formulation ties.**<br>**INV-074**: Reading (v10, v17); Predicate (v17).<br>**INV-075** and **INV-079**: Predicate (v02, v17).<br>Notes of **E-051** (v05, v11, v15, v17), **E-053** (v02, v17) and **E-055** (v02, v11, v17).<br>Rows **OUT-023** and **OUT-024** (v17 and earlier) | v17 (and earlier) | **v17 (R17-02).** New conjuncts:<br>• the formulation of an acute treatment line is one of the subject's acute medications (INV-079);<br>• the drug and formulation of a treated-attack line are those of an acute medication of the subject (INV-075);<br>• INV-074's tie to the summary's formulations extends to every summary that names its formulations. | R17-02; the optional summary tie was declined | **Convergent.** Additive conjuncts only. `summarisesMedication` is unchanged (14 occurrences since v15), and the OUT-023 reading is not decided. The declined option was not raised again (review 18: the fix is correct). |
| **Instrument note and Stage 1 issue entries.**<br>**E-057** Notes (v01, v03, v19); **ISS-02** (v19); **ISS-03** (v20); section 3.5 (v12, v20).<br>Notes of **E-022** (v01, v10, v12, v20, v24), **E-044** (v01, v10, v12, v20), **E-060** (v01–v04, v12, v20), **E-061** (v02–v04, v20), **INV-060** (new in v20) and **INV-086** (v12, v20).<br>Rows **OUT-008**, **OUT-019** (v10, v20) and **OUT-030** (v01–v04, v12, v20) | v19, v20 | **v19.** The basis of the HALT-30 lower bound (R19c-01); the location and topic of the one ICHD-3 use of "simple analgesics" (R19c-02).<br>**v20 (R20-01).** ISS-03 and the section 3.5 list add OUT-008, OUT-019 and OUT-030, with Notes pointers and coverage reasons. | R19c-01, R19c-02, R20-01 | **Convergent.** Text only: no formal block changed in v19 or v20. Each sentence changed once; the corrected sentences had been unchanged since v00. |
| **Cluster view.**<br>**E-062**: Notes (v21, v23); in all v02, v12, v14, v21, v23.<br>**E-063**: Meaning and Notes (v21, v23); Definition (v23: `ongoing` comment and `lastDay`, their first change since v00).<br>**INV-089**: Predicate and Reading (v05, v09, v23, v24); Notes (v05, v09, v21, v23, v24).<br>**E-064** Notes (v05, v09, v24); new **ISS-12** (v21); row **OUT-031** (v05, v09, v12–v15, v21, v23) | v21, v23, v24 (and earlier) | **v05 (R05-03).** The rate relation; `concerns`.<br>**v09 (R09-01).** `onlyOfType`.<br>**v21 (R21b-01).** ISS-12. E-063 Meaning names the Definitions-of-terms bound. Text only.<br>**v23 (R23-01, option (a)).** `ongoing` means "not ended by the as-of date", and `lastDay` of an ongoing phase is the as-of date. New conjunct `(∀ e ∈ x.end • e ≤ ctx.asOf)`.<br>**v24 (R24-01).** The rate–count conjunct compares periods by dates. | R05-03, R09-01, R13-01, R14-02 (earlier); R21b-01; R23-01; R24-01 | **Convergent** (Findings, C). Kept verbatim: the remission bound (`plusMonths(s, remissionMoreThanMonths) ≤ e`), the constant, ISS-12, `onlyOfType` and the rate-within-bout conjunct. The rate relation only became stricter. |
| **Per-period relations compared by dates.**<br>Changed only in v24: **INV-006**, **E-014** `daysOf`, **INV-030**, **INV-033**.<br>Changed in v24 and earlier:<br>• **INV-012** (Predicate v24; Reading v08, v10, v24);<br>• **INV-031** (v04, v24);<br>• **INV-046** (Predicate v03, v24; Reading v03, v12, v24);<br>• **INV-053** (v10, v24);<br>• **E-032** (Definition v03, v12, v24; new `sameIndicatedPeriod`);<br>• **INV-024** Reading (v10, v12, v24); **INV-011** Notes (v12, v24); **INV-003** Notes (v11, v12, v24);<br>• Notes of **E-013** (v08, v12, v24), **E-019** (v05, v24) and **E-022** (v24);<br>• rows **OUT-003** (v08, v12, v24), **OUT-004**, **OUT-014** (v12, v24), **OUT-016** (v03, v12, v24) and **OUT-029** (v01, v24) | v24 (and earlier) | **v24 (R24-01, option (a), within one view).**<br>• Counts of the same measure, scope and dates agree (INV-006). The v23 identity per atom is kept in the consequent.<br>• `daysOf` and the EventCount, mark and rate comparisons match periods with the same dates.<br>• Completeness indicators with the same dates agree (INV-012).<br>• Overuse indicators are matched by view, dates and kind (`sameIndicatedPeriod`). Combined-use indicators of one view and period give the same indication (INV-046).<br>• A change compares periods with different dates (INV-053). | R03-01, R04-03, R10b-01, R11-01, R12-01, R12-02 (earlier); R24-01 | **Convergent** (Findings, D).<br>• Every relation now covers each pair it covered in v23, and the INV-006 identity is kept.<br>• Membership ties (INV-038, INV-054, INV-056) and the INV-003 placement are unchanged, so the R10b-01 and R11-01 decisions and the v12 INV-003 period requirement stand. |
| **Definition labels.**<br>**E-011**: Meaning and Notes (v04, v12, v24); Conformance (v12, v24).<br>**E-016** and **E-017** Meaning (v04, v24).<br>**INV-008**: Reading and Notes (v12, v24); Predicate (v12 only).<br>**E-040**: Conformance and Notes (v03, v10, v12, v24).<br>New **INV-111** (v24); row **OUT-002** (v12, v24) | v24 (and earlier) | **v24 (R24-02, option (a)).** INV-111 (definitional):<br>• one definition per measure in a view;<br>• where a change, residual burden or composite index refers to values shown in another view, and both views state a definition for the measure, the two definitions are the same.<br>The Meanings of E-016 and E-017 refer to that one definition. | R04-02, R04-03, R12-02 (earlier); R24-02 | **Convergent.** Additive.<br>• INV-008's predicate and SHOULD level are unchanged.<br>• `labelledAs` (R04-03) is unchanged since v12.<br>• R12-02's `reports` and `referencedValues` are unchanged.<br>• R10b-01's permission for a change's values to be shown in another view is untouched: INV-111 constrains only the labels. |
| **Notation.** Section 2.5 (v11, v12, v17); E-002 and E-003 Definitions (v17) | v17 | **v17 (R17-03, option (a)).** `outputOf` and `viewOf` are declared as given total functions. | R11-01 (section 2.5 references); R17-03 | **Convergent.** A form correction; no use changed. |
| Header; sections 9, 11 and 12; ISS-11 (artefact) | every version | Version line, "as of vNN", one search-log paragraph and one change-log entry per version. | — | Bookkeeping, not applicable. |
| Items whose changes all lie in v00–v16 and that are unchanged since. Examples: INV-105 Predicate and E-067 (v16); INV-062, INV-066, INV-069, INV-071, INV-072, INV-088, INV-104 and INV-109 Predicates, and E-047 and E-051 (v15); INV-098 (v13); E-008 Definition (v12); INV-003 Predicate (v12); INV-054, INV-056, INV-078, E-040 Definition; INV-086, INV-087, E-060, E-061 Definitions; E-041 `omn` block (v14); INV-050 Predicate (v05) | within v00–v16 | See check-after-iter-04, -08, -12 and -16. | as there | Convergent (earlier checks). Unchanged in v17–v24. |

## Recurring remark topics

| Topic (IDs) | Remarks | Pattern | Assessment |
|---|---|---|---|
| **Dates of course events and open ends against periods** (E-042, E-049, INV-049, INV-055, INV-058, INV-059, INV-063, INV-064, INV-068, INV-070; E-063, INV-089) | R17-01, R18-01, R23-01; fix 17's date-boundary check. Earlier: R02-05 (fix 02: the open end of a treatment line is the as-of date), R12-01, R16-01 | Each remark ties a different relation, under one convention:<br>• time point against the period's last day (v17);<br>• on-treatment against the stop of the course (v18);<br>• the open end of a cluster phase against the as-of date (v23).<br>Section 2.8 is unchanged since v17, and v18 and v23 build on it. R23-01's option (a) carries fix 02's choice for treatment lines (the as-of date, not the end of the covered period) over to cluster phases. | **Converging.** No relation was tied twice, and no convention changed after v17. |
| **Truth of a shown fact tied to the context** (INV-074, INV-075, INV-079; INV-063, INV-064; INV-089) | R17-02 (formulation), R18-01 (b) (labels after a stop), R23-01 (end date not after the as-of date) | Each adds a definitional conjunct that excludes only outputs stating something false, a formulation never used or a classification past the stop. R17-02 explicitly separates its point from R15-01's (which summaries are required). | Convergent. Additive. The iteration-16 "identifying property" class (type scope, period, formulation of required summaries, adherence window, comparison course, acute course) was not reopened on any of its dimensions. |
| **Text that claims more than the predicate** (E-006, INV-104, INV-105; E-063, INV-089; INV-006, INV-024, INV-030, INV-031, INV-089; E-011, E-016, E-017) | R22b-01, R23-01, R24-01, R24-02. Earlier of the same kind: R10b-02, R11-01 | Each finds that a statement of an earlier fix (fix 03 and fix 05 on `fillsPeriod`; the fix-04 sweeps of R04-04 and R04-03) is not secured by its predicate. Each time the predicate was brought up to the text:<br>• R22b-01 (b), R23-01 (b) and R24-01 (b) were not taken;<br>• no text was weakened in a way that undoes a fix. | **Converging, but not exhausted.** It occurred in three successive iterations (22b, 23, 24), each time on a different object: series alignment, the meaning of `ongoing`, period identity, definitions per view. A further remark of this class on an item aligned in v22–v24 would be cycling (watch point 9). |
| **Stage 1 issue entries and notes** (E-057, ISS-02, ISS-03, ISS-12) | R19c-01, R19c-02, R20-01, R21b-01 | Four text-only remarks, with no predicate changed, each on a different entry. R19c-01 and R19c-02 had been examined and not raised in reviews 05, 10b, 16, 19 and 19b. R21b-01 brought new evidence (ICHD-3 3.1.2, p. 42) against review 02's "not a model defect". Each corrected sentence had been unchanged since v00 and changed once. | Convergent. A threshold shift in the reviews (points once judged "close enough" were later raised), but one-directional. No later remark asks to restore an earlier wording. |
| **Cluster view** (E-062, E-063, INV-088, INV-089, OUT-031) | R05-03, R09-01, R13-01, R14-02 (earlier); R21b-01, R23-01, R24-01 | Three remarks in three of the last four iterations, each on a different conjunct: the source of the remission bound (text), the last day of an open phase, the rate–count matching. The bound, its constant, ISS-12, `onlyOfType` and the rate relation are kept (Findings, C). | Convergent. The most active item of iterations 21–24 (watch point 3). |
| **Series and `fillsPeriod`** (E-006, INV-050, INV-104, INV-105) | R03-04, R05-01, R22b-01 | R22b-01 completes R03-04 (i) for 28-day series, on a case that no loop file had examined (offset series). | Convergent (Findings, A). |
| **INV-105** (watch point 1) | R22b-01 only (its series conjunct) | No remark on the treatment-effect conjunct since R16-01. The predicate is byte-identical since v16. | Stable. |

**Settled points.** Reviews 17 to 24 list these as "not reopened (no new evidence)", and every item behind them is unchanged in v17–v24, or changed only on another dimension (marked):
- INV-106 at MUST NOT; INV-023 at any granularity; INV-027 tied to preventive treatments;
- the "> 3 months" readings of INV-045 and INV-089. For INV-089 the bound is verbatim; v23 changed only the last day against which it is tested, Findings C;
- the E-041 window readings, timings, ages and `excludes` values;
- "one item suffices" and the ties of INV-105; INV-098 read on period starts; the history-wide `acuteMedications`;
- the HIT-6 one-month recall; HADS subscales only; the MIDAS labels and Grade IV undivided; "baseline administration";
- INV-060 with INV-061 for compared periods shorter than 28 days; one adherence window per comparison; the periods of the overview's response comparison;
- `mostRecent` with 28-day periods (R22b-01 distinguished it; INV-041 is unchanged);
- empty `remissions` in chronic cluster headache (fix 02 item 14; ISS-12);
- the 24-hour outcomes of 15-minute summaries; the history of previous bouts; the cluster-view references without co-presence (fix 11);
- E-039 `reviewWindow` against INV-050; the CycleLine lead-in; the MUST cycle-line attributes in the overview;
- new in iterations 17–24:
  - the result completed on the start day read as the pre-treatment baseline (E-046, fix 17);
  - `namedCriteria` unused;
  - INV-071 per-phase summaries kept on the comparison's periods after a stop;
  - the window time point kept after a stop inside the window;
  - the HALT-90 total and question 5, and no HALT upper bound;
  - control levels over mixed months;
  - the INV-031 marks conjunct (reviews 21, 22, 22b). v24 changed it only to match by dates;
  - periods after the as-of date for comparisons (reviews 18, 19b, 22).

**Remark counts per iteration:** 12, 7, 7, 4, 3, 1, 3, 0 + 2, 1, 0 + 2, 3, 2, 3, 2, 3, 1, **3, 1, 0 + 0 + 2, 1, 0 + 1, 0 + 1, 1, 2**.

## Convergence assessment

**Numbers, v17–v24** (v13–v16 in brackets, from the iteration-16 check):

| Version | v17 | v18 | v19 | v20 | v21 | v22 | v23 | v24 |
|---|---|---|---|---|---|---|---|---|
| Remarks of the iteration | 3 | 1 | 0 + 0 + 2 | 1 | 0 + 1 | 0 + 1 | 1 | 2 |
| Items changed (iteration-12/16 granularity) | 96 | 74 | 18 | 39 | 31 | 30 | 25 | 122 |
| Top-level elements, invariants and issues | 18 | 12 | 2 | 7 | 4 (+ ISS-11 artefact) | 4 | 3 | 25 |
| Traceability rows | 4 | 3 | 0 | 3 | 1 | 2 | 1 | 6 |
| Invariant predicates / element definitions | 5 / 4 | 6 / 3 | 0 / 0 | 0 / 0 | 0 / 0 | 0 / 1 | 1 / 1 | 9 / 3 |
| Formal (`omn`) blocks changed | 9 | 9 | 0 | 0 | 0 | 1 | 2 | 12 |

(v13–v16: remarks 3, 2, 3, 1; items 110, 73, 90, 28; top-level 21, 12, 12, 3.) These counts agree with fix logs 17 to 24.

**Reading.**
- **Remark rate.**
  - The remark rate fell to about one per iteration: 12 remarks in iterations 17–24, against 9 in 13–16 (four iterations) and 56 in 01–16.
  - Three main reviews (19, 21, 22) returned NO_REMARKS, and iteration 19 had two NO_REMARKS in a row.
  - Every NO_REMARKS review was followed by a re-check that found at least one remark (19c, 21b, 22b), so the loop has not yet reached three consecutive NO_REMARKS.
- **Kinds of remark.** They narrowed through iteration 23, then widened again:
  - v17 and v18: Stage 1 fidelity and formal relations, with 9 changed blocks each;
  - v19–v21: text only;
  - v22 and v23: one or two conjuncts;
  - v24: two model-wide formal remarks (period identity in relations, one definition per view). With the fixer's same-defect sweep they changed 12 blocks and 122 items, the largest volume since v12.
- **The v24 spike is a new dimension, not a cycle.**
  - No earlier remark or fix concerned whether two period atoms with the same dates are the same reporting period, or whether a view may state two definitions for one measure.
  - The sweep went in one direction only: relations compare dates, membership ties stay on atoms.
  - It reverted nothing. The near-return detector, the n-gram checks and the term counts find no return.
- **No class on an already-tied dimension.**
  - No remark class recurs on a dimension already tied. The iteration-16 "identifying property" class was not reopened.
  - The day-boundary class tied three different relations under one convention.
  - The "text claims more than the predicate" class moves to a new object each time.

**Judgement.** The loop is converging. No item went back and forth, and every change of v17–v24 either added a conjunct or a pointer, or replaced a relation by one that covers every case the old one covered (Findings, D). But it has not converged. The remarks are no longer narrowing in size: iteration 24 opened the deepest formal question since iteration 12, with the most new surface (by-dates relations, INV-111). The next check should see whether iterations 25–28 return to small, text-level remarks, or whether the v24 semantics draw follow-up remarks that reopen it.

## Findings

None.

No item oscillates, so nothing is frozen, FROZEN_ITEMS.md is not written and OUTPUT_MODEL.md is not changed. Four points come closest to a back-and-forth pattern; each is assessed below.

### A. Offset 28-day series in the overview (INV-105) and `fillsPeriod` (v00–v04 → v05–v21 → v22)

**Trace of the series conjunct for 28-day periods:**
- **v00–v04.** INV-105 required `tiles(sr, spanOf(v.covers), sr.granularity)`, an exact tiling. A series offset within the covered period was not admitted. Neither was any series of a covered period that is not a run of whole periods; R05-01 found this defect.
- **v05–v21 (R05-01).** `containsPeriodOf ⇒ fillsPeriod`. Fix 05 stated: "Where the covered period is a run of whole periods, a series of that granularity still spans it exactly". For 28-day periods `fillsPeriod` admitted offset series, and series one period short, also on exact runs (R22b-01).
- **v22 (R22b-01, option (a1)).** `sr.granularity = fourWeekPeriod ⇒ first(sr.periods).start = p.start`. The offset series is excluded again.

**Script (`fills24.py`; 4,276 covered-period and granularity cases):**
- **Nesting.** The admitted sets are nested in every case: v04 ⊆ v22 ⊆ v21.
- **Exact runs.** On the 768 cases that are exact runs, v22 admits exactly the v04 tiling series. v21 admitted further series in 573 of them.
- **Satisfiability.** v22 admits exactly one series in every case where a whole period fits, so INV-105's v05 satisfiability, the defect R05-01 fixed, is kept. No case fails.
- **Granularities.** v21 and v22 differ only for 28-day periods (1,394 cases), never for calendar months or weeks.
- **INV-050.** Of the 15,691 series that begin on the first day of the covered period, as INV-050's series must (`v.covers.start = v.withdrawalStart`, `first(sr.periods).start = v.withdrawalStart`), none has a different verdict under v21 and v22. INV-050's own start ties imply the new conjunct, so v22 did not change INV-050's verdicts.

**Why it is not an oscillation:**
1. **One position throughout, no competing one.**
   - Fix 03 ("all whole periods of its granularity"), fix 05 ("still spans it exactly"), the INV-104 and INV-105 Notes of v05–v21 and fix 22 all state the same intent.
   - No remark or fix ever argued for admitting an offset 28-day series. The v05–v21 admission was an unintended effect of a predicate that did not say what its text said.
2. **The item did not return to an earlier state.** The v22 predicate keeps the v05 form (`containsPeriodOf`, `fillsPeriod`) and its satisfiability for every covered period, and adds no end tie (iteration-08 watch point 4). It equals v04 only where v04 was satisfiable.
3. **R05-01 is kept.** A 43-day covered period, R05-01's example, still has a series under v22.

**Judgement:** convergent. The nearest approach to A → B → A in iterations 17–24, at the level of one kind of admitted output, without competing positions.

### B. The on-treatment period of the post-stop view for a stop on the start day (E-049, INV-070; v00–v01 → v02–v16 → v17)

**Trace** (`poststop.py`):

| Event | v00–v01 | v02–v16 | v17–v24 |
|---|---|---|---|
| Stop on the start day | required, impossible (unsatisfiable) | not required, impossible | required, possible (a 1-day period) |
| Reduction on the start day | required, impossible | not required, impossible | not required, impossible |
| Stop or reduction 1 or 30 days after the start | required, possible | required, possible | required, possible |

**Why it is not an oscillation:**
1. **The rule never changed.** Fix 02 (item 5) made the SHOULD apply exactly where the period can exist ("impossible for a stop, pause or reduction on the start day"). From v02 on, required = possible in every case.
2. **What changed is the possibility.** The v17 day convention (R17-01; section 2.8) dates a stop on the last day of the course, so a course stopped on its start day has one day on treatment. Fix 17 states this explicitly: "Fix 02's reason … still holds for a reduction. For a stop it no longer holds, because the stop date is a day on treatment".
3. **The v00–v01 state was a defect.** It required a period that no output could contain. v17 does not restore it, because the v17 requirement is satisfiable.
4. **No competing positions.** No remark argued that the period should not be shown where it exists. The alternative, dating a stop on the first day off treatment, would have changed INV-079, INV-109, `courseOverlaps` and `courseNotOutside` (watch point 1), and fix 17 did not take it.

**Judgement:** convergent. A change of a shared convention on its own ground, with the principle of fix 02 kept.

### C. The cluster view: INV-089 and E-063 in v21, v23 and v24

**Trace:**
- **v21 (R21b-01, option (a)).** Text only. ISS-12 sets out the three ICHD-3 wordings of the remission duration. The E-063 Meaning names the Definitions-of-terms bound. No `omn` block changed.
- **v23 (R23-01, option (a)).**
  - `ongoing` means "not ended by the as-of date", and `lastDay` of an ongoing phase is the as-of date (it was the end of the covered period, unchanged since v00).
  - New conjunct `(∀ e ∈ x.end • e ≤ ctx.asOf)`.
- **v24 (R24-01).** The rate–count conjunct compares the periods of counts and rates by dates. Its antecedent (`r.period = p`) is unchanged, so p still ranges over the rates' own atoms.

**Did v23 or v24 reverse R05-03, R09-01 or R21b-01 / ISS-12? No.**
- **R05-03 (rate relation).** Its form is kept. In v24 its universally quantified consequents range over a superset (every count and rate with the dates of p), so every v23 constraint still holds and more are added.
- **R09-01.** `onlyOfType(ctx, r.typeScope, c3_1)` is verbatim since v09.
- **R21b-01 / ISS-12.**
  - `plusMonths(s, remissionMoreThanMonths) ≤ e`, the constant and ISS-12 are verbatim since v21.
  - v23 changed only the day the bound is tested against for an ongoing phase. An attack-free period is now tested on its own length (to its end, or to the as-of date), not on its part within the covered period.
  - ISS-12's "an attack-free period of three months or less … is not shown as a remission period" remains true. The E-062 Notes sentence of v21 is kept in v23, with one sentence added.
- **The settled "> 3 months" reading** is unchanged.
- **Rate within bout.** The rate-within-bout conjunct keeps its form. Its reach follows the bout's own extent, as review 15 settled ("a rate over any period within the bout").
- **Fix 02.** R23-01 extends to cluster phases fix 02's choice of the as-of date for an open end (R02-05). This is not a reversal of anything: `ongoing` and `lastDay` had never changed before v23.

**Judgement:** convergent. Three changes in four iterations on three different conjuncts, none in the opposite direction to an earlier one. This is the most active item of iterations 21–24 (watch point 3).

### D. The v24 move from period atoms to dates (R24-01, R24-02 and the fix-24 sweep)

**What changed.** Relations "for the same period" now compare dates:
- INV-006 and `daysOf`;
- INV-024 and INV-030 to INV-033 through `daysOf`;
- the EventCount conjuncts of INV-030 and INV-033;
- the rate conjunct of INV-089;
- the marks conjunct of INV-031;
- INV-012 (completeness);
- E-032 and INV-046, through `sameIndicatedPeriod`;
- INV-053;
- the E-046 components.

INV-111 is new.

**Direction of each change:**
- **Universally quantified relations.** INV-006, `daysOf` in INV-024 and INV-030 to INV-033, the EventCount and rate conjuncts, and INV-012 now range over a superset of the pairs they ranged over in v23. INV-006 keeps `m.period = n.period ⇒ m = n` in its consequent. So each implies its v23 form.
- **Stricter.** INV-053 (`¬ sameSpan` instead of `≠`) and INV-046's new combined-use conjunct are stricter.
- **The INV-031 marks conjunct.** It became existential by dates (`sameSpan(mk.period, spanOf(p))`) instead of by atom. With `daysOf` by dates, the atom form would be unsatisfiable as soon as another view of the output has an atom of the same month (fix 24, by script).
  - The conjunct is unchanged in substance since v00, and no remark ever fixed it.
  - Reviews 21, 22 and 22b examined it and did not raise it.
  - Its requirement, that every 0-count period is marked where the view marks such periods, is kept.
- **E-046 components.** They decide in more cases, so INV-063 forces in more cases. The v18 guard `evaluatedOnTreatment(L)` and every iteration-12 watch-point-2 tie are verbatim.

**Did the v24 by-dates comparisons alter what R10b-01, R11-01 or the v12 INV-003 period requirement established? No.**
- **The v12 INV-003 requirement.** The INV-003 predicate is byte-identical since v12, including the v12 conjunct `∀ m ∈ referencedValues(x) • ∃ p ∈ v.content ∩ Period • sameSpan(p, spanOf(m.period))`. That conjunct already compared by dates.
- **R11-01.** Membership of values in a comparison stays on atoms: INV-038 is unchanged since v00, and INV-056 since v01. The R11-01 derived property `p ∈ refs(x) ∩ refs(y) ⇒ viewOf(x) = viewOf(y)` is still stated in the INV-003 Notes (1 occurrence in v11, v12, v23 and v24). So the (a)/(b) derivation by which fix 11 declined R11-01 (a)/(b) stands. The v24 INV-003 Notes say so ("Membership of a value in a comparison stays tied to the comparison's own period atoms").
- **R10b-01.**
  - INV-054 is unchanged since v10.
  - The sentence "a value shown in another view with a period of the same dates … is not a value of that comparison" is verbatim in v23 and v24.
  - Agreement by dates is stated within one view only, not output-wide (fix 24), so a change may still have its values in another view.
  - INV-111 (2) constrains only the labels of the two views, where both state one.
- **R04-03.** `labelledAs` and the INV-031 IHS-2025 conjunct are unchanged since v12 and v04. INV-111 secures the "one measure, one definition" premise that fix 04 assumed.

**Judgement:** convergent. A model-wide strengthening in one direction, on a dimension that no earlier remark or fix had touched. Its size is the main convergence concern (watch points 1 and 9), not a reversal.

## Things the next checker should watch

1. **The v24 by-dates relations** (INV-006, E-014 `daysOf`, INV-012, INV-024, INV-030 to INV-033, INV-046, INV-053, the INV-089 rate conjunct, E-032 `sameIndicatedPeriod`, the E-046 components). Treat as oscillation, unless it rests on evidence that R24-01 and fix 24 did not consider:
   - a return to atom identity in any of these relations (`m.period = p`, `e.period = f.period`, `i₂.period = i.period`);
   - dropping `(m.period = n.period ⇒ m = n)` from INV-006;
   - returning the INV-031 marks conjunct to `mk.period = p`, which fix 24 found unsatisfiable with date-based `daysOf`.

   **Not a reversal, but a new decision:** making the agreement output-wide. It would have to address per-view definitions (INV-111). Moving membership or placement ties (INV-038, INV-054, INV-056, the INV-003 placement) to dates would undo the R11-01 derivation and the R10b-01 permission, and should be frozen.
2. **INV-111 and INV-008.**
   - INV-008's predicate is unchanged since v12 (fix 24: with INV-111 it is equivalent to `∃ d • labelledAs(v, lm, d)`).
   - Replacing its consequent would duplicate INV-111 (1).
   - Per-value definitions (R24-02 (b)) were not taken. Re-raising them needs new evidence.
3. **The cluster view** (E-062, E-063, INV-088, INV-089; ISS-12), changed in v21, v23 and v24. Treat as oscillation, unless it rests on evidence that R21b-01, R23-01 and R24-01 did not consider:
   - `ongoing` or `lastDay` relative to the covered period again (R23-01 (b));
   - removing `(∀ e ∈ x.end • e ≤ ctx.asOf)`;
   - any change of `remissionMoreThanMonths` or of the `plusMonths(s, …) ≤ e` form (settled; ISS-12 belongs to the human);
   - dropping `onlyOfType` (R09-01) or the rate relation (R05-03);
   - rate matching back to atoms.

   A fourth remark on INV-089 in a row should be checked against these.
4. **The day convention and the stop bounds** (section 2.8, v17; `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, v18). Unchanged since. Treat as oscillation:
   - any change of the course-event dates (stop or pause on the last day of the course; `cycleEnd(n)` on the first day after the cycle; dose change on the first day at the new dose);
   - `atTimePoint` back to `p.end = tp.earliest`, or `fitsMonthlyPeriod` back to `− 1`;
   - dropping one of the three predicates, or INV-049 back to `≤`;
   - re-adding R18-01's sketch condition `a ≤ e.date`, which fix 18 dropped and review 19 confirmed.

   In E-049 `onTreatmentPeriod`, the period is required for a stop on the start day and not for a reduction on the start day (Findings, B). A change of either case would reverse fix 17 or fix 02 item 5.
5. **`fillsPeriod`** (v22). Treat as oscillation:
   - dropping the 28-day anchor (R22b-01 (a2) or (b));
   - adding an end tie, or loosening INV-050's start ties (iteration-08 watch point 4).

   `mostRecent` (INV-041) stays without a grid (review 06; R22b-01).
6. **Formulation ties** (v17).
   - **Reversals:** dropping the INV-079 or INV-075 formulation conjuncts, or restricting INV-074 back to single-formulation summaries.
   - **Declined tie:** the summary-formulation tie that fix 17 declined (a 0-attack summary of a formulation never used is a correct value). Re-raising it needs new evidence.
7. **Text-only entries** (E-057 Notes, ISS-02, ISS-03 with the section 3.5 list, ISS-12).
   - Restoring an earlier wording would be a reversal.
   - Fix 20 found the seven-statement ISS-03 list complete.
   - Several of these points were judged "not raised" by earlier reviewers and later raised (R19c-01, R19c-02). A remark that now argues the earlier wording was right would be cycling.
8. **Earlier watch points, all unchanged in v17–v24 in their formal text:**
   - INV-105's treatment-effect conjunct and E-067 (iteration-16 watch point 1);
   - the history-wide `acuteMedications`, E-062 `acute` and E-045 `valueAvailable` (watch point 2);
   - the acute and adherence identity ties (watch point 3);
   - responder labels (watch point 4; v18 and v24 added only a guard, a conjunct and date matching);
   - E-041 (watch point 5);
   - INV-098 (watch point 6);
   - co-presence, the menstrual-relation view, withdrawal follow-up and the E-008 time frames (watch point 7).

   Their reversal triggers still apply.
9. **Change volume and remark pattern.**
   - Items changed: 96, 74, 18, 39, 31, 30, 25 and 122 in v17–v24; formal blocks: 9, 9, 0, 0, 0, 1, 2 and 12.
   - Check that volume falls again after v24.
   - A remark whose fix reverts part of the v24 sweep, or a further "text claims more than the predicate" remark on an item aligned in v22–v24, would be cycling. The aligned items are E-006, the INV-104 and INV-105 Readings, E-063, INV-089, INV-006, INV-024, INV-030 to INV-033, E-011, E-016 and E-017.
10. **Periods beyond the as-of date.**
    - v23 bounds the end dates of cluster phases by the as-of date.
    - Reviews 18, 19b and 22 settled that comparison periods may reach beyond it.
    - A remark that extends the as-of bound to comparison periods would contradict that settled point and needs new evidence.

## Conclusion

No item of the model oscillates after twenty-four iterations, and nothing is frozen.

- **Returns.** The only item that returns to an earlier state is `aged12OrOlder` (added in v06, removed in v12), which the iteration-12 check assessed. No element, attribute, field, invariant, rule or criterion constant, source, section, value set, conformance level, Realises field or traceability row returns to an earlier state in v17–v24, and no change moves an item closer to an older state.
- **Point-level returns.** Two outputs return to an earlier verdict, each without competing positions:
  - the offset 28-day series of the overview (Findings, A);
  - the post-stop on-treatment period for a stop on the start day (Findings, B).
- **Questions asked of this check:**
  - v22's anchor did not change INV-050's verdicts (0 of 15,691 series).
  - v23 and v24 kept R05-03, R09-01 and R21b-01 / ISS-12 (Findings, C).
  - v24's date comparisons left the R10b-01 and R11-01 co-presence decisions and the v12 INV-003 period requirement intact (Findings, D).
- **Change volume:** 96, 74, 18, 39, 31, 30, 25 and 122 items in v17–v24.
- **Remark counts:** 3, 1, 0 + 0 + 2, 1, 0 + 1, 0 + 1, 1 and 2. The loop is converging: no reversals, and a new dimension each time. It has not converged: re-checks keep finding remarks, and v24 was the largest change since v12.

The scripts are in the session scratchpad (`osc24/`): `split.py`, `analyse.py`, `volume.py`, `multi24.py`, `nearret.py`, `show.py`, `show3.py`, `optypes.py`, `dels24.py`, `omn.py`, `ngram.py`, `docwide.py`, `conf.py`, `attrtypes.py`, `guar24.py`, `wp24.py`, `remarks24.py`, `fills24.py` and `poststop.py`. FROZEN_ITEMS.md was not written, and OUTPUT_MODEL.md and the history snapshots were not changed.
