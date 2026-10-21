# Fix log — iteration 18
Input review: reviews/review-iter-18.md · Input version: v17 · Output version: v18
Date: 2026-10-21

## What was read, downloaded and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039), and the source rows of section 5 that I needed (S-011, S-013, S-015, S-018, S-033);
- v17 (`OUTPUT_MODEL.md`, byte-identical to `history/v17.md`), sections 1–12;
- review 18.

**Earlier loop files read, so that no fix is undone:**
- the oscillation check after iteration 16, with its eight watch points, and the watch points of the checks after iterations 08 and 12;
- fix 17 (the day convention; the date-boundary table; format and checks);
- fix 05 (the start tie of INV-064 and the R05-02 sweep of the responder components);
- review 15 ("Several stop events in one course", not raised), review 11 ("INV-060 for a percentage change after a stop", not raised), and reviews 16 and 17 on INV-068's periods (the monthly kind, not raised).

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. No earlier fixer declined a remark on a course stopped or paused before an evaluated period.

**Downloads.** With `curl` into the fresh directory `/tmp/r18fix-dl-sbZR`, outside the repository (all HTTP 200), checked by script (`srccheck.py`, markup removed, NFKC):
- [S-015] NICE CG150 Recommendations page (Stage 1 URL; "Last updated: 03 June 2025"): 1.3.27 ("Review the need for continuing migraine prophylaxis 3 to 6 months after starting prophylactic treatment."), 1.3.28 ("Stop CGRP inhibitors after 12 weeks of treatment if the frequency of migraines does not reduce by") and 1.3.29 ("after 2 treatment cycles") read as Stage 1 quotes them;
- [S-011] Europe PMC full text of PMC9188162: question 3 ("we suggest evaluating efficacy after a minimum of 3 consecutive months on treatment") and question 4 ("In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal");
- [S-013] Europe PMC full text of PMC7296705: "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed."

No web search and no new source. Every quoted fragment of the new text is verbatim in Stage 1 v18, except "after three months at the target dose" ([S-008] Q2) and "etkinlik için en az 2-3 ay" ([S-035] Kutu 8), which are fragments of quotes that E-041 Evidence already gives and review 18 verified at the source (`myquotes.py`).

**Scripts.** All are in the session scratchpad, `r18fix/` (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r18fix/`), and were run with `python3 -I`:
- `stop18.py`: the 18 rules (values copied from E-041) under the v17 and the v18 requirements of INV-055, INV-058 and INV-059; the review's example; stops at the boundaries of the intervals; 40 000 random courses (types, ages, target-dose and cycle-end anchors, one or two stops); the INV-055 construction; the label and treatment-review-view cases;
- `srccheck.py`: the source wording above;
- `mech.py`, `names.py`: the mechanical checks of PROCESS.md section 11;
- `changed.py`: the items and fields changed from v17;
- `watch18.py`: byte-identity of the watch-point items, the lines added to and removed from each changed `omn` block, and counts of the guarantee terms;
- `myquotes.py`, `quotes.py`: the new quoted fragments;
- `scope.py`: scope-term counts in v17 and v18, and the hits on changed lines.

### Verification of the remark

**R18-01 holds.**
- **(a) Time points.** `applicable` (E-041) looks at type, population, exclusion and the existence of an anchor, and INV-055 (MUST) and INV-059 (MUST) quantify over every anchor date. No conjunct looks at a stop or pause of the course. `stop18.py`, for the review's example (adult, migraine; types `antiCGRPMonoclonalAntibody`, `monthlyInjectable`, `cgrpInhibitor`; start 1 January 2026; `stop(discontinued)` dated 10 February 2026; as-of 20 October 2026): v17 requires the six time points of NICE CG150 1.3.27 and 1.3.28, EHF 2022 question 3, IHS 2024 Q2 (monthly injectables), the Russian section 7.1 and Turkish Box 8 with every comparison of the course, and a comparison at each of them whose on-treatment period ends on 25 March, 31 March or 28 February, all after the course ended. The review's table is reproduced exactly.
  - Every rule's guidance names its time point after an interval of treatment (Stage 1 OUT-018 quotes and E-041 quotes), and section 2.8 reads the time point as the date after that interval. For a 6-week course there is no 12-week interval of treatment, so OUT-018 ("at the evaluation time points named in current guidance") does not name these time points for it. Requiring them at MUST broadens OUT-018, and showing them presents the course as evaluated after the interval the guidance names.
  - The cycle-anchored rules (NICE 1.3.29, Turkish 3.6.3.9 and 7.3) already apply only where the cycle took place, so the model was inconsistent with itself, as the review says.
- **(b) Labels.** INV-064 bounds the evaluated months of a control-level label by the start only; "optimal control" over March to May after a stop on 10 February meets it. INV-063 forces "responder" or "non-responder" from a single evaluated month, and `reductionMet` and `reductionDecided` look at the comparison's on-treatment periods, which INV-056 bounds by the start only (Stage 1: "periods after treatment start"). So a NICE 1.3.28 label on March is forced by March's values (`stop18.py`, section 2).

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R18-01 | fixed; (a) as the review proposes, with the condition also in INV-058 and E-043; (b) INV-064 as proposed, and for responder and non-responder labels the review's second option (no component decides) | E-041 (Meaning; Notes, new paragraph **Stop or pause**); E-042 (Definition: `notStoppedBefore`, `intervalOnTreatment`; Meaning; Conformance; Evidence; Notes); E-043 (Definition: `timePoints` `when`; Conformance; Notes); INV-055 (Predicate, Reading, Notes); INV-058 (Predicate, Reading); INV-059 (Predicate, Reading); E-046 (Definition: `evaluatedOnTreatment`; Meaning; Notes, **After a stop or pause**); INV-063 (Predicate, Reading, Evidence); INV-064 (Predicate, Reading, Notes); rows OUT-018, OUT-020 | **(a) New predicates (E-042):**<br>• `notStoppedBefore(c, t, d) ≙ ¬ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is stop ∧ e.date < d`: the course has not ended before d, since a stop or pause is dated on the last day of the course (section 2.8);<br>• `intervalOnTreatment(c, t, a, r) ≙ notStoppedBefore(c, t, plusDays(shift(a, r.minOffset), −1))`: the course is taken through the last day of the interval from the anchor date (for a window, of the minimum interval, the reference the review names).<br>**Uses:** INV-059 requires, and INV-058 (definitional) admits, a time point only where `applicable ∧ intervalOnTreatment` holds. E-043 `timePoints` is MUST when such an anchor date exists; without this change the v17 `when` clause would have required a non-empty set that INV-058 now forbids. INV-055 adds `intervalOnTreatment(c, t, a, r)` to the antecedent and `notStoppedBefore(c, t, p.end)` to the witness, so a comparison at a window whose course stops inside the window ends on or before the stop, as the review asks.<br>**INV-058 as well, not only the requirements.** A time point shown for a 6-week course would itself present the course as evaluated after 12 weeks of treatment. This is consistent with INV-058's treatment of the population (no time point outside it); a diary may state the stop as an `OtherItem`.<br>**Departure from the review's sketch.** The sketch has `a ≤ e.date`. I dropped it: a stop or pause dated before the anchor date (for example before the target dose was reached) also means the course ended before the interval, under the v17 convention, and `courseOverlaps` likewise lets any earlier stop end the course. For cycle-end anchors with `weeks(0)` the two forms agree.<br>**Kept (watch point 5):** `applicable` and the whole E-041 `omn` block are byte-identical: every `excludes`, `timing`, `ages`, `AgeCoverage`, anchor and offset value, `ruleTr73`, and the age read on the start. Section 2.8 is byte-identical. The comparison is still required for every started treatment (INV-055 first conjunct), and its periods stay "periods after treatment start" (INV-056 byte-identical).<br>**Results (`stop18.py`):**<br>• the review's example: v17 requires 6 time points and 6 comparisons, v18 none;<br>• stopped on 31 March, all 6 apply; on 30 March, NICE 1.3.28 and Box 8 only; on 27 February, none;<br>• uninterrupted course: v18 requires exactly the v17 set;<br>• 40 000 random courses: v18 = v17 in all 40 000 without a stop; with a stop, v18 ⊆ v17 in all, and a pair is dropped exactly when a stop precedes the last day of its interval.<br>**(b) New predicate (E-046):** `evaluatedOnTreatment(L) ≙ ∀ p ∈ ran L.evaluated • notStoppedBefore(ctx(outputOf(L)), L.treatment, p.end)`.<br>• INV-064 (definitional) gains the conjunct `evaluatedOnTreatment(L)` next to the fix-05 start tie, which is kept. The [S-010] levels are goals "while on treatment".<br>• INV-063: the forcing of "responder" and "non-responder" applies only where `evaluatedOnTreatment(L)` holds. This is the review's second option ("decide nothing"), in one place: `componentMet` and `componentDecided` are used only in INV-063, so the guard has exactly that effect.<br>**Why not the first option for these labels.** A definitional bound on every label would exclude an optional label that Stage 1 does not forbid. It would also need the start bound for every label, which then duplicates INV-064's start tie (a duplication remark) unless that tie is moved, against fix 05. The second option removes the forcing on which the defect rests and cannot exclude a permitted output. The model already treats a label over several periods the same way: the reader applies the named criterion to the values shown (INV-062).<br>**Kept (watch point 4):** `#L.evaluated = 1`, the `evaluationResult` / `pretreatmentBaseline` pair, `rc.treatment = L.treatment`, the R09-01 scope ties, the open kinds and the v13/v15 acute ties. E-012, E-045, INV-062 and every E-046 predicate except the new one are byte-identical (`watch18.py`; counts equal).<br>**Text aligned:** E-041 Meaning and Notes (the sentence "`applicable` holds for the rules of all preventive types whenever …" is followed by the anchor-date condition); E-042 Meaning (with the review's example), Conformance, Evidence and Notes (with the [S-013] quote of Stage 1 OUT-024); E-043 Conformance and Notes; Readings of INV-055, INV-058, INV-059, INV-063 and INV-064; Notes of INV-055 and INV-064; E-046 Meaning and Notes; rows OUT-018 and OUT-020. |

## Other changes

The orchestrator asked me to check, as the same defect nearby, every place where "on treatment", "on-treatment" or the evaluated period of a treatment is used without the stop or pause of the course. I fixed only genuine gaps under the v17 convention (a stop or pause is dated on the last day of the course).

| Place | Stage 1 wording | Result |
|---|---|---|
| **INV-068, E-048** (treatment review view) | OUT-021 "for the same pre-treatment baseline and on-treatment periods", so that "efficacy can be judged" | **Gap: fixed** (item 1). The on-treatment periods were bounded by the start only, so the MUST view of a course stopped after 6 weeks could present March to May as its on-treatment periods. |
| INV-055, INV-056, E-043 `onTreatment` (response comparison) | OUT-018 "periods after treatment start" | Not a gap. Kept as Stage 1 states it, as the review requires. Only the period required at a time point now ends within the course. |
| `adherenceFor` (E-047), INV-066, INV-067 | OUT-039 "over the evaluation window, next to the response comparison of OUT-018" | Not a gap. The window is that of the comparison, whose periods OUT-018 places after the start. Adherence to the prescribed regimen counts no intake after the stop as missed, so a window that reaches past it states nothing false. Bounding it would make INV-066 (SHOULD) unsatisfiable with INV-067 for every comparison of a course shorter than 28 days, which INV-055 (MUST) still requires. Not changed. |
| INV-109, E-055 (course spans of acute lines; duration) | OUT-024 "start and stop dates [...] treatment duration" | Already end on the stop date (v17). Not changed. |
| INV-070, E-049 (post-stop view's on-treatment period) | OUT-022 "the on-treatment period" | Already ends before `firstChangedDay`, on or before the stop or pause date (v17). A course with several stop events is the review-15 case, which was not raised, and INV-070 changed in v17. Not changed. |
| INV-071 per-phase summaries; INV-027 | OUT-023 "the on-treatment periods of that preventive treatment" (of OUT-018's comparison); OUT-027 | Follow the comparison's periods. Not changed. |
| INV-060, INV-061, E-044 ("per month that remain on treatment") | OUT-019 | Settled in review 11 ("INV-060 for a percentage change after a stop […] Not raised"). No new evidence. Not changed. |
| `courseOverlaps`, `courseNotOutside` (E-067), INV-105 | OUT-035 | Already exclude a course stopped before the period (watch point 1). Byte-identical. |

1. **INV-068** (MUST) gains the conjunct `(∀ p ∈ ran v.onTreatment • notStoppedBefore(ctx, v.treatment, p.end))`, with its Reading and new Notes. E-048 Notes and row OUT-021 are aligned.
   - **Stage 1 basis.** OUT-021 names its periods "on-treatment periods", unlike OUT-018's "periods after treatment start". The periods after a stop are OUT-022's.
   - **Not a reopening.** Reviews 16 and 17 settled the monthly kind of these periods, not their end.
   - **INV-097 Notes.** The satisfiability sentence named INV-068 among the invariants that 28-day periods meet. That is no longer true for a course shorter than 28 days, so the sentence now gives periods of a common length no longer than the course up to its first stop.
2. **Housekeeping:** header (v18, iteration 18); section 9 ("as of v18"); section 11 (iteration 18 entry: no web search, three downloads, no new source); section 12 (v18 entry).

**Items changed (script, v17 → v18).**
- 12 model items:
  - 5 elements: E-041, E-042, E-043, E-046, E-048;
  - 7 invariants: INV-055, INV-058, INV-059, INV-063, INV-064, INV-068, INV-097.
- Rows OUT-018, OUT-020 and OUT-021.
- The header and sections 9, 11 and 12.

**Formal changes:**
- three new defined predicates: `notStoppedBefore` and `intervalOnTreatment` (E-042), and `evaluatedOnTreatment` (E-046);
- the `when` clause of E-043 `timePoints`;
- the predicates of INV-055, INV-058, INV-059, INV-063, INV-064 and INV-068. Each change only adds a conjunct or a guard; no line of an earlier predicate was removed other than to append to it (`watch18.py`).

No element or invariant was added, withdrawn or renumbered. No level changed, and no source was added.

### Satisfiability pass

I checked the changed relations together with the invariants that constrain the same elements and views, in every admissible context (INV-001: stops on or after the start, several stops, anchors after a stop, as-of date after every event).

- **Response comparison and time points** (INV-055 with E-042, E-043, INV-003, INV-011, INV-054, INV-056 to INV-061, INV-066, INV-067, INV-097, INV-104, INV-105, INV-109).
  - INV-058 and INV-059 now carry the same condition, `applicable ∧ intervalOnTreatment`. So every required time point is admitted, and the E-043 `when` clause asks for a non-empty set exactly where INV-059 does.
  - The INV-055 construction works for every required pair: 116 685 of 116 685 in `stop18.py`. The construction is a 28-day period whose last day is the day before the time point, or for a window before the later of its first date and the 28th day after the start. It begins on or after the start, meets `atTimePoint`, and ends on or before every stop or pause. Every window of the list begins at least 8 weeks after the start, so its last day is the last day of the interval, which `intervalOnTreatment` places on or before every stop.
  - A 28-day baseline ending before the start has the same length (INV-097). The adherence window equal to the on-treatment period meets `adherenceFor` and INV-067.
  - For a course that has not stopped, every requirement equals v17's (40 000 random courses).
  - The first conjunct of INV-055 is unchanged, so a stopped course still has a comparison, and INV-104, INV-105 and INV-109 can show it.
- **Labels** (INV-063, INV-064 with E-045, E-046, INV-062, INV-065, INV-100, INV-106).
  - INV-063 only became weaker: it forces less, and its two forcing antecedents stay mutually exclusive.
  - INV-064's new conjunct constrains only optional control-level labels. INV-062 (SHOULD) can be met with on-treatment periods of the label's comparison that lie within the course, and INV-056 leaves those periods free. Where no consecutive monthly periods lie within the course, no control-level label is shown, and none is required.
- **Treatment review view** (INV-068 with INV-002, INV-003, INV-011, INV-069, INV-097, INV-102).
  - The view's periods are of any kind. For a stopped or paused course, a period from the start to its first stop or pause date lies within the course, because the start precedes every course event (INV-001). A shorter one does as well, and a baseline of the same length ends before the start.
  - For a course without a stop the conjunct is void. INV-102 (MUST) stays satisfiable for every started treatment, including one stopped on its start day (a 1-day period).
- **Definedness.**
  - `plusDays` and `shift` are total, `−1 ∈ ℤ`, and `ctx(outputOf(L))` is total.
  - The new predicates use no partial term.
  - No derived attribute was added, and the relations of `earliest` and `latest` (INV-058) hold wherever a time point exists.
- **Levels.**
  - INV-055 and INV-059 stay MUST, INV-068 MUST, and INV-058, INV-063 and INV-064 definitional.
  - The MUST changes only narrow INV-055 and INV-059. INV-068 now excludes only outputs that present periods after the end of the course as on-treatment periods, which OUT-021 does not permit.

**Result.** No admissible context makes the MUST and SHOULD invariants that constrain these elements and views jointly unsatisfiable. No derived attribute is required where its relation is undefined.

### Watch points (oscillation/check-after-iter-16.md)

1. **INV-105 and E-067** are byte-identical.
2. **E-062 `acute`, E-045 `valueAvailable` and E-008** are byte-identical.
3. **Acute summaries and adherence.** INV-062, INV-066, INV-067, INV-069, INV-071, INV-072, INV-088, INV-104 and INV-109, and E-047 and E-051, are byte-identical.
4. **Responder labels.** E-012, E-045 and INV-062 are byte-identical. E-046 gained one predicate, INV-063 one guard, and INV-064 one conjunct; every tie listed in the watch point is kept. Term counts are equal in v17 and v18: `#L.evaluated = 1` 7, `rc.treatment = L.treatment` 13, `evaluationResult(` 7, `pretreatmentBaseline(` 6, `scopeFor(` 8, `otherValueNamed` 6, `summarisesMedication(` 14, `s.typeScope = allTypes` 9.
5. **E-041.** The `omn` block is byte-identical. No `excludes`, `timing`, `ages`, `AgeCoverage`, anchor or offset value changed, `ruleTr73` is kept, and the age is read on the start. The section 2.8 day convention is byte-identical. The stop condition is a separate, anchor-level predicate that only narrows where a time point applies.
6. **INV-098** is byte-identical.
7. **Earlier watch points.**
   - Co-presence: INV-003, INV-054, INV-056, INV-078 and E-040 are byte-identical.
   - Menstrual-relation view: INV-086, INV-087, E-060 and E-061 are byte-identical.
   - Withdrawal follow-up: INV-049, INV-050, INV-051 and E-039 are byte-identical.
   - The E-008 time frames are byte-identical.
8. **Change volume.** 12 model items and 3 rows, with no sweep. Beyond the remark's own items, the extra items are INV-068 and E-048 (the same defect) and INV-097 (its satisfiability note).

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-11; ISS-07 appears only as withdrawn (section 8 note, section 9, change log). |
| References | No dangling E- or INV- reference. Every S reference lies in S-001–S-046 or S-101–S-106, and every S-1NN has a row in section 10. Every OUT reference exists in Stage 1, and all 39 requirements are referenced. |
| Fields | Exactly one Realises and one Conformance field in each of the 177 elements and invariants. No Realises field changed. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every OUT, the row's E and INV sets equal the sets derived from the Realises fields. |
| Types and names | 340 declared names (v17: 337; new `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`), none declared twice. The only capitalised names in `omn` blocks (text literals aside) that are not declared are the bound variables A, C, D, K, Ks and L. The applied names without a `pred` or `fun` declaration are the same as in v17: `refs` (section 2.5), `first` and `last` (section 2.6), and sequence applications. Every argument of the new predicates has its parameter's type. All 181 `omn` blocks have balanced brackets. |
| Declaration forms | 41 `fun` declarations, all in one of the two forms of section 2.3. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type (E-043 `timePoints`: `set`). |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33; total 110, unchanged. Scopes: output 77, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Date arithmetic (`stop18.py`) | The review's example: v17 requires 6 time points and 6 comparisons, v18 none. The same course uninterrupted: v18 = v17. Boundary stops: 31 March, all 6 apply; 30 March and 25 March, 2; 24 March and 28 February, 1; 27 February, 0. Random courses: 40 000 of 40 000 equal without a stop; with a stop, v18 ⊆ v17 and the exclusion is exact in 40 000 of 40 000. INV-055 construction: 116 685 of 116 685. |
| Instance checks (`stop18.py`) | Control-level label "optimal control", March to May after a stop on 10 February: admitted by v17 INV-064, excluded by v18. NICE 1.3.28 label on March: forced by v17 INV-063, not by v18. The same label on January (within the course): forced under both. Treatment review view with March as its on-treatment period: admitted by v17 INV-068, excluded by v18. 1 January to 10 February, or January: admitted under both. |
| Quotes | 16 quoted fragments in the new text: 14 verbatim in Stage 1 v18, and 2 fragments of quotes already in E-041 Evidence. No source quote was added or changed. The [S-011], [S-013] and [S-015] wording was also confirmed in the downloaded texts. |
| Scope sweep | Searched the whole document for enter, entry, record, input, captur, logged, store/storage, persist, database, JSON, XML, CSV, FHIR, HL7, serializ/serialis, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field, questionnaire, data-entry, "derived from", "diary information", intake, "decision logic", took and taken. Every count equals v17 except "taken" (37 → 54). Every new occurrence is "the course is taken through the interval" or "a treatment taken over an interval": a property of the subject's treatment course in the output context, defined by the dated stop and pause course events (E-008), as `courseOverlaps` already says "taken during p". None is input data. Every relation added takes only context properties (course events), output elements (periods, labels, time points) and rule constants as arguments. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v18.md`: identical. `history/v17.md` is unchanged (equal to HEAD). |
