# Fix log — iteration 29
Input review: reviews/review-iter-29.md · Input version: v28 · Output version: v29
Date: 2026-10-22

## What was read and checked

**Read:**
- PROCESS.md, in full.
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039), in full. I read OUT-018, OUT-020, OUT-021, OUT-022, OUT-024 and OUT-039 and their evidence closely. The key wordings:
  - OUT-039: "over the evaluation window, next to the response comparison of OUT-018";
  - OUT-018: "periods after treatment start, aligned to the treatment start date".
- v28 (`OUTPUT_MODEL.md`, byte-identical to `history/v28.md`):
  - sections 1–5 in full;
  - in section 6, INV-001, INV-055 to INV-059, INV-064, INV-066 to INV-070, INV-077 to INV-079, INV-097, INV-102 to INV-105 and INV-109 in full, plus the headings of all other invariants;
  - every formal line that constrains an adherence window, found by script (E-047 `adherenceFor`, E-055 `adherence`, INV-011, INV-066, INV-067, INV-079, INV-104, INV-109);
  - section 7, rows OUT-018 to OUT-024 and OUT-039;
  - sections 9, 11 and 12 (the v18 and v28 entries).
- Review 29 (one remark, R29-01), with its "Checked and not raised" list and its optional candidates (the INV-067 name, and the E-055 Notes phrase "adherence refers to the time on treatment (INV-067)").
- Fix 18: its decision row on `adherenceFor`, INV-066 and INV-067: "a window that reaches past it states nothing false. Bounding it would make INV-066 (SHOULD) unsatisfiable with INV-067 for every comparison of a course shorter than 28 days".
- Fix 28, in full: its start-tied bounds table, in particular row 15 (E-055 `adherence`, start-dependent by OUT-039) and row 31 (INV-067).
- Fix 02, the E-055 `when` clauses. Its ground for `adherence`: "Adherence refers to the time on treatment (INV-067) and, by OUT-039, to 'the evaluation window' of the response comparison. Neither exists without a start."
- The oscillation check after iteration 28, watch points 1–7.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**No download and no web search.** The fix adds no fact, value, source or quote.

**Scripts.**
- **Location.** All scripts are in a fresh scratchpad folder, `fix29/` (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix29/`), and were run with `python3 -I`.
- `sent28.py` (output `sent28.out`) lists, item by item and field by field, every prose sentence of v28 that is not in v27. These are the sentences that fix 28 added or changed.
- `claims29.py` (output `claims29.out`) transcribes the v28 predicates as written:
  - `courseBegunBy`, `startOf`, `notStoppedBefore`, `evaluatedOnTreatment` and `firstChangedDay`;
  - the E-049 `when` clauses;
  - INV-064, INV-067, INV-068 (with its v27 form for comparison), INV-070, INV-078, INV-079, INV-103 and INV-109.
  - It evaluates them on 14,709 admissible one-course contexts:
    - these are all contexts over days 0–6 with or without a stated start, a stop or pause, a dose reduction, a dose increase and a cycle end, under the INV-001 order;
    - periods may reach beyond the as-of date, which no invariant forbids (review 18);
    - 28-day periods are scaled to 3 days, because none of the claims depends on the length.
  - It also runs calendar examples:
    - the review's example B;
    - a course started on 1 January 2026 and stopped on 10 February 2026.
- `newtext29.py` (output `newtext29.out`) checks the claims of the v29 text on the evaluation windows of response comparisons, for courses with a stated start.
- `apply29.py` builds v29 from `history/v28.md` by six exact replacements, each asserted to occur exactly once, and appends the change-log entry.
- `mech27.py`, `names27.py`, `tokcheck27.py`, `omndiff27.py`, `itemdiff27.py`, `scope27.py` and `quotes27.py` are copies of fix 28's scripts. I read each one before use.

### Verification of R29-01

The remark holds (`claims29.out`, predicates as written in v28).

**Example B.** A course t1 has no stated start, `doseChange(reduction)` on 15 March 2026 and `stop(paused)` on 30 June 2026; the as-of date is 21 October 2026.
- INV-067 admits an adherence window of 1–31 August 2026, because `courseBegunBy(ctx, t1, 1 August)` holds through the events of 15 March and 30 June.
- None of its days lies in 15 March – 30 June 2026, the days that E-008 Notes place on the course.
- Of the calendar months January 2025 to October 2026, INV-067 admits April to October 2026 as windows, four of them after the pause.

**Enumeration.** For stopped courses without a stated start, INV-067 admits 160,701 windows.
- 63,972 of them contain no day placed on the course.
- Only 35,111 lie within these days.

So "still refers to days that the context places on the course" does not hold. No other invariant closes the gap:
- INV-066, INV-104 and INV-109 constrain a window only through `adherenceFor`, which needs a response comparison;
- INV-056 admits a response comparison only with a stated start;
- INV-011 adds a completeness indicator.

**The predicate is right.** INV-067 guarantees exactly a lower bound:
- every admitted window of a course without a stated start (215,446 of 215,446) begins on or after a dated course event, so not before the days placed on the course;
- no admitted window is bounded by the stop or pause. Without a stated start, 125,590 windows reach past the stop and 63,972 begin after it; with a stated start, 248,096 reach past it and 114,990 begin after it.

This is fix 18's settled reading, which the review does not reopen.

### Choice of the fix

- **The predicate.** I reworded the sentence and did not delete it. The INV-067 predicate, `courseBegunBy` and every other formal block are byte-identical (watch points 1 and 4; fix 18).
- **What is kept.** The first half of the sentence is correct and stays: "no response comparison and no evaluation window of one exists (INV-056)".
- **What replaces the false clause.** The false clause is replaced by what INV-067 guarantees, as the review proposes:
  - the window begins on or after a dated course event, so not before the days that the context places on the course;
  - INV-067 bounds only the first day of the window;
  - whether or not the context states the start, it does not bound the window by the stop or pause, so a window may reach past the stop or pause, or begin after it.
- **The ground, stated without citing fix 18.** For a stated start, the reason is the model's own: an evaluation window ends with an on-treatment period of the response comparison (`adherenceFor`, E-047), and these periods are not bounded by a stop (INV-056; E-043 Notes). Model Notes cite model items, not fix logs, so the review's parenthesis "(fix 18)" is not copied.
- **Why the explicit statement helps.** It removes any reading of the invariant's name "Adherence refers to the time on treatment" as an upper bound.

### Fix-28 prose check

Every prose sentence that fix 28 added or changed (`sent28.out`) was checked against the predicate it describes. The check covers the sentences of:
- E-008, E-046, E-047, E-048, E-049, E-051 and E-055;
- INV-064, INV-067, INV-068, INV-070, INV-078, INV-079, INV-097, INV-103 and INV-109;
- rows OUT-020, OUT-021, OUT-022 and OUT-024;
- the v28 change-log entry.

The check IDs refer to `claims29.out`. "Holds" means that the formal text guarantees exactly what the sentence states.

| # | Item, field | Claim (abridged) | Check | Result | Decision |
|---|---|---|---|---|---|
| 1 | E-008 Meaning | where the start is stated, `courseBegunBy(c, t, d)` holds exactly for the days on or after it | C1: 109,186 of 109,186 | holds | none |
| 2 | E-008 Notes, **Course start not stated**, sentences 1–2 | without a stated start, the course began on or before its first dated course event; the days placed on the course run from that event to the stop or pause, or to the as-of date | definition, under the day convention of section 2.8 | holds | none |
| 3 | E-008 Notes, sentence 3 | the on-treatment period (INV-070), the control-level months (INV-064) and an adherence window (INV-067) "begin on or after such an event"; the acute line's summary "covers these days" (INV-109) | C2: 215,446 of 215,446 windows; C5: 0 months before; C6: 156,438 of 156,438 periods; C12: 19,852 of 19,852 summaries cover | holds: it states only the lower bound for the three periods | none (see row 21) |
| 4 | E-008 Notes, sentence 4 | no start date, duration, response comparison, time point, review view or original baseline for such a course | C11: 0 start dates, 0 durations; INV-056; INV-058 (`inPopulation` needs `startOf`); C10: 0 views; baselines admitted: 0 | holds | none |
| 5 | E-046 Notes; INV-064 Reading; row OUT-020 | control-level months begin on or after the start (or a dated course event) and end on or before every stop or pause | C5: 97,178 labels; 0 months before; 0 months after a stop | holds | none |
| 6 | E-047 Notes, Relations | INV-067: the window begins on or after the start or, without one, on or after a dated course event | C2; definition | holds | none |
| 7 | E-048 Conformance and Notes; INV-068 Reading and Notes; row OUT-021 | a review view only for a treatment whose start is stated; the existential form gives the universal verdicts where the start is stated; April 2026 lies on treatment in example B | C10: 0 views without a stated start; 30,026,150 of 30,026,150 equal verdicts; calendar: April 2026 within 15 March – 30 June | holds | none |
| 8 | E-049 Conformance, sentence 1; E-049 Notes, sentences 3, 4 and 6; INV-103 Reading and Notes; row OUT-022 | the view is available after every stop, pause or reduction, whatever the start; a baseline only where the original start is stated, and none admitted otherwise | C8: 22,344 views required, 7,421 of them for courses without a stated start; 0 baselines admitted without one | holds | none |
| 9 | E-049 Conformance, sentence 2; E-049 Notes, sentence 8; INV-070 Reading, sentence 2; INV-070 Notes, sentence 3 | the on-treatment period is asked for exactly where the context places a day on treatment before the changed regimen | C7: asked ⇔ admitted, 22,344 of 22,344; asked ⇔ a day placed before it, 22,344 of 22,344; the view without the period is rejected exactly where it is asked for, 7,421 of 7,421 | holds | none |
| 10 | E-049 Notes, sentences 1, 2, 5 and 7; INV-070 Reading, sentence 1; INV-070 Notes, sentences 1–2; row OUT-022 | the on-treatment period begins on or after the start (or a dated course event) and ends before the first changed day, so it lies within the course; it exists for every stop or pause (also on the start day), for a reduction only after the start day (without a stated start, only after another dated event), and never for a reduction on the start day | C6: 156,438 of 156,438 within the placed days; 10,608 of 10,608 stops; 7,838 of 7,838 and 3,898 of 3,898 reductions; 0 of 2,088 reductions on the start day | holds | none |
| 11 | E-049 Notes, the example (sentences 9–12) | for the pause: periods from 1 July and an on-treatment period within 15 March – 30 June (June); August and February not admitted. For the reduction: no on-treatment period, and none asked for. Neither view shows a baseline | calendar: admitted months for the pause are April, May and June 2026; for the reduction, none; asked for the pause, not for the reduction; 0 baselines | holds | none |
| 12 | E-051 Conformance; E-055 Conformance; INV-109 Reading and Notes; row OUT-024 | the acute line's summary runs from the start (without one, from on or before the first dated event) to the stop or the as-of date, covers every placed day and ends with the course; the construction is in order | C12: all 19,852 cover and end with the course; construction 14,709 of 14,709 | holds | none |
| 13 | E-055 Notes, Relations; INV-079 Reading and Notes; row OUT-024 | no start date and no duration for a course whose start is not stated; otherwise the duration runs from the start to the stop or the as-of date | C11: 0 and 0; 2,060 of 2,060 | holds | none |
| 14 | INV-078 Reading and Notes; row OUT-024 | every two dated lines are in order; an undated line may stand anywhere | C13: 64 of 64 | holds | none |
| 15 | INV-097 Notes; INV-070 Notes, satisfiability; INV-103 Notes, satisfiability | periods of a common length, no longer than the days on treatment before the changed regimen, meet INV-070 and equal lengths | C14: 64,294 of 64,294 | holds | none |
| 16 | INV-067 Reading | the window begins on or after the start or a dated course event, "so that the window does not begin before the course" | C2 | holds | none |
| 17 | INV-067 Notes, sentence 1 | where the start is stated, the two bounds coincide | C1 | holds | none |
| 18 | INV-067 Notes, sentence 2 (**R29-01**) | an adherence summary of a course without a stated start "still refers to days that the context places on the course" | C3: 63,972 of 160,701 windows of stopped courses contain no such day; example B, August 2026 | **fails** | **reworded** (remark table) |
| 19 | **INV-064 Notes**, the start-tie sentence | without a stated start, the months begin on or after a dated course event, "within the days that the context places on the course, not before it" | C4: stopped courses, 0 of 7,018 labels have a month outside these days; courses not stopped, 17,767 of 21,712 labels have a month that ends after the as-of date, outside these days. Calendar: the same treatment, reduced on 15 March 2026 and not stopped, as of 21 October 2026, admits the month October 2026 | **fails for a course that has not stopped** | **reworded:** "so not before the days that the context places on the course, and end on or before every stop or pause of it (`evaluatedOnTreatment`), so that the months of a course that has stopped or paused lie within those days" |
| 20 | **E-055 Notes**, the `when`-clause sentence | "The `when` clauses state when the content can exist: a start date and a duration (INV-079) and a response comparison aligned to the start (INV-056) exist only for a treatment that has a start, and adherence refers to the time on treatment (INV-067)." | Parts 1–3 hold (C11; INV-056). Part 4 is given as the ground of the `adherence` clause `role = preventive ∧ startOf(…) ≠ ∅`. Since v28 the context places days on a course without a stated start (E-008 Notes), and INV-067, INV-079 and INV-109 admit an adherence summary on such a course's line (C15: 4,778 of 4,778 courses with a dated event). So INV-067 no longer grounds the condition, and "refers to the time on treatment" reads as the confinement that INV-067 does not have (row 18). The content the clause asks for, the adherence over an evaluation window of the response comparison (E-055 Conformance, INV-109), exists only with a stated start, because `adherenceFor` needs a comparison and INV-056 needs the start (`newtext29.out`). | **claims more** | **reworded:** "and so does an evaluation window of that comparison, the window over which the line's adherence is asked for (OUT-039; `adherenceFor`, E-047; INV-109)". This is the OUT-039 ground of fix 02 and of fix 28's table row 15. The `when` clause is byte-identical. |
| 21 | INV-067 name; E-008 Notes, sentence 3 ("periods that the model ties to the time on treatment") | the review's optional candidates | The name predates v28 (v00) and fix 28 did not change it. A name is a label, not a claim (PROCESS section 9: naming is not a remark). The Reading states the guarantee, and the v29 Notes say that the window is not bounded by the stop. E-008, sentence 3, states only the lower bound, which holds (row 3). | not a defect | none |
| 22 | v28 change-log entry, Checks | without a stated start, "every on-treatment period, month, window and summary period that v28 admits lies within the days that the context places on the course" | Periods: hold (C6). Months: begin on or after a dated event (C5) and lie within these days only for stopped courses (C4). Windows: begin on or after a dated event, but are not within these days (C3). Summary periods: cover these days and end with the course, but may begin before them (C12). | **claims more** (a summary of fix 28's checks, whose own log states them correctly: "begins on or after, or covers") | The v28 entry is a record of v28 and is left as written. The v29 change-log entry states the correct results. |

**Result.**
- Of the fix-28 prose, three statements claim more than their predicates guarantee: INV-067 Notes (R29-01), INV-064 Notes and E-055 Notes. All three are reworded, text only.
- A fourth, the summary in the v28 change-log entry, is corrected in the v29 entry.
- Every other fix-28 sentence states exactly what the formal text guarantees.
- No sentence was found that claims less.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R29-01 | fixed: reworded, as the review requires; text only | INV-067 (Notes) | **Before (v28):** "Where it states none, no response comparison and no evaluation window of one exists (INV-056), and an adherence summary that is shown still refers to days that the context places on the course (E-008 Notes, **Course start not stated**)."<br>**After (v29):** "Where it states none, no response comparison and no evaluation window of one exists (INV-056), and the window of an adherence summary that is shown begins on or after a dated course event of the treatment, so not before the days that the context places on the course (E-008 Notes, **Course start not stated**). INV-067 bounds only the first day of the window. Whether or not the context states the start, it does not bound the window by the stop or pause of the course: a window may reach past the stop or pause, or begin after it. Where the context states the start, this holds for the evaluation windows of the response comparison as well: each ends with an on-treatment period of the comparison (`adherenceFor`, E-047), and these periods are not bounded by a stop (INV-056)."<br>**Justification:** the remark is verified (example B: the August 2026 window is admitted and contains no day placed on the course; 63,972 of 160,701 windows). Each new claim holds by script:<br>• lower bound: C2, 215,446 of 215,446;<br>• not bounded by the stop: C3, windows that reach past the stop or begin after it, with and without a stated start;<br>• evaluation windows: 72,044 and 39,753 of the 76,132 evaluation windows of stopped courses with a stated start reach past the stop or begin after it (`newtext29.out`); calendar example: a course stopped on 10 February 2026, the comparison's on-treatment month March 2026, and the window March 2026 meets `adherenceFor` and INV-067.<br>**Not changed:** the INV-067 predicate, `courseBegunBy`, the Reading, the name (row 21) and every other formal block. Fix 18's decision (no stop bound) is restated, not reopened. |

## Other changes

**Two further sentences of the fix-28 prose** (rows 19 and 20 above), text only, same defect class as R29-01:
- **INV-064 Notes.**
  - **Before:** "… and the months still begin on or after a dated course event of the treatment, within the days that the context places on the course, not before it (E-008 Notes, **Course start not stated**)."
  - **After:** "… and the months still begin on or after a dated course event of the treatment, so not before the days that the context places on the course, and end on or before every stop or pause of it (`evaluatedOnTreatment`), so that the months of a course that has stopped or paused lie within those days (E-008 Notes, **Course start not stated**)."
  - **Why:** "within" holds only where the course has stopped or paused. For a course that has not stopped, a month may end after the as-of date, which no invariant forbids (review 18). The predicate is unchanged.
- **E-055 Notes.**
  - **Before:** "… exist only for a treatment that has a start, and adherence refers to the time on treatment (INV-067)."
  - **After:** "… exist only for a treatment that has a start, and so does an evaluation window of that comparison, the window over which the line's adherence is asked for (OUT-039; `adherenceFor`, E-047; INV-109)."
  - **Why:** v28's INV-067 admits the adherence window of a course whose start the context does not state, so it no longer grounds the start condition of the `adherence` clause. That condition rests on OUT-039's evaluation window of the response comparison. The `when` clause and fix 02's decision are unchanged, and fix 28's table row 15 classifies the clause in the same way.
- **Watch points.** INV-064 and INV-067 (watch point 4) and E-055 `adherence` (row 15 of fix 28's table, which watch point 4 covers) are items of the oscillation check after iteration 28. The reversals listed there concern their formal text: `courseBegunBy` back to `∀ s ∈ startOf`, a contested row classification, and the `when` clauses. All of that formal text is byte-identical. The v29 changes are Notes text only. They move the text toward the predicates and toward fix 18's and row 15's readings, so they reverse nothing listed there.

**The v28 change-log summary** (row 22). It is left as written; the v29 entry records the correct results.

**Bookkeeping:**
- header: "Version: v29 · Iteration: 29 · Status: under review";
- section 9: "(as of v29)";
- section 11: an iteration-29 entry (no web search, no download, no new source; the scripts and examples);
- section 12: the v29 entry.

**Items changed (diff v28 → v29, `itemdiff27.py`): 7.**
- **3 content items**, each in its Notes only:
  - E-055 (Notes);
  - INV-064 (Notes);
  - INV-067 (Notes).
- **4 bookkeeping items:** the header and sections 9, 11 and 12.
- **Formal blocks:** 0 of 182 changed.
- **Not changed:**
  - no Definition, Predicate, Meaning, Reading, Conformance, Realises or Evidence field;
  - no heading;
  - no traceability row;
  - no source, value, axiom or level.

## Checks

| Check | Result |
|---|---|
| (i) R29-01 and the review's example (`claims29.out`) | Example B under the v28 predicates: INV-067 admits the window 1–31 August 2026, which contains no day of 15 March – 30 June 2026. Stopped courses without a stated start: 63,972 of 160,701 admitted windows contain no day placed on the course. The remark holds. |
| (ii) The new text (`claims29.out`, `newtext29.out`) | INV-067 Notes: C2 and C3, and the evaluation windows of stated-start comparisons (16,436 comparisons, 92,960 evaluation windows, all of which meet INV-067). INV-064 Notes: C4 and C5. E-055 Notes: C11, C15, and `adherenceFor` with INV-056. The v29 change-log entry: C3, C4, C5, C6 and C12. Every claim of the new text holds. |
| (iii) Fix-28 prose check | 22 rows above. 3 statements reworded, 1 change-log summary corrected in the v29 entry, the others hold. |
| Headings and IDs (`mech27.py`) | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn). No dangling E-, INV-, ISS- or source reference; 37 source IDs cited, all within S-001–S-046 or S-101–S-106. Every OUT reference exists in Stage 1. The output is identical to the run on v28. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. All 39 rows are byte-identical to v28. |
| Types and names (`names27.py`, `tokcheck27.py`) | 750 declared names, none declared twice. The token report is identical for v28 and v29: 106 flagged tokens, each a declared attribute. Nothing added or removed. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34, unchanged. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`, and every invariant states its scope. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), with no typing-rule violation. |
| Diff of formal blocks (`omndiff27.py`, plus an ordered comparison) | 182 `omn` blocks in v28 and in v29. All are byte-identical, in order (equal SHA-256 of the concatenation). All 183 fenced blocks are identical. In the three changed items, only the Notes field differs; the headings are identical. |
| Quotes (`quotes27.py`) | 2 quoted fragments on changed lines: "while on treatment" (Stage 1 v18, OUT-020's [S-010] section title, already on that INV-064 line in v28) and "optimal control" (already in v28). No quote added or changed. |
| Scope sweep (`scope27.py`) | Term counts v28 → v29 are equal except four, each read in context:<br>• "entry" (3 → 4): the v28 change-log entry;<br>• "stor" (68 → 69): the path `history/v28.md`;<br>• "taken" (63 → 64): "a treatment already being taken", as in the entries of iterations 27 and 28;<br>• "states" (221 → 226): "the context states".<br>The new text has no input, storage or input-derivation content. |
| Snapshot and files | `cmp OUTPUT_MODEL.md history/v29.md`: identical. `history/v28.md` and everything under `docs/stage1-output-requirements/` are unchanged (equal to HEAD). Only `OUTPUT_MODEL.md`, `history/v29.md` and this log were written. |
