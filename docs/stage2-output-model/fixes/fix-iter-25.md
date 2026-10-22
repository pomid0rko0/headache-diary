# Fix log — iteration 25
Input review: reviews/review-iter-25b.md · Input version: v24 · Output version: v25
Date: 2026-10-22

## What was read and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039), with OUT-018, OUT-021, OUT-022 and OUT-024 and their evidence read closely (OUT-022: "After a preventive treatment is stopped, paused or reduced"; [S-011] "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal.");
- v24 (`OUTPUT_MODEL.md`, byte-identical to `history/v24.md`), sections 1–12;
- re-check 25b (one remark, R25b-01) and review 25 (no remarks).

**Earlier loop files read, so that no fix is undone:**
- the oscillation check after iteration 24, with its ten watch points, in particular watch point 4 (day convention and stop bounds) and watch point 1 (by-dates relations);
- review 15 ("Several stop events in one course", not raised);
- fix 17 (the day convention; `firstChangedDay`; the E-049 `when` clause);
- fix 18 (`notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`; the INV-068 tie; the dropped `a ≤ e.date`);
- fix 11, context-restriction table, which already reads course events as "at most one start; nothing before the start […] a restart is a new course";
- fix 07, whose E-041 sweep lists IHS 2024 Q7 ("waiting at least one month before considering restarting treatment") as "a restart (OUT-022)", not a time point.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. No earlier fixer declined a remark on several stops of one course; review 15 set the case aside without a remark, and fix 18 referred back to it.

**No download and no web search.** Every quoted fragment of the new text is verbatim in Stage 1 v18 (`quotes25.py`).

**Scripts.** All are in the session scratchpad, `r25bfix/` (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r25bfix/`), and were run with `python3 -I`:
- `stops25.py`: INV-001 in its v24 and v25 forms, and, as written in v24 (unchanged in v25), `startOf`, `stopped`, `notStoppedBefore`, `intervalOnTreatment`, `courseOverlaps`, `courseNotOutside`, the stop dates and durations INV-079 admits, the course-span ends of INV-109, the events of INV-103, `firstChangedDay`, the E-049 `when` clause, the on-treatment bounds of INV-068 and INV-070, the INV-055 time-point requirement for six start-anchored rules, and the markers of INV-035; the review's example, the dose change after a stop, a pause followed by a restart, the earlier watch-point examples, and 40,000 random contexts;
- `breakdown.py`: the kinds of the random contexts that v24 admits and v25 does not;
- `sat25.py`: the constructions of INV-055, INV-068, INV-070, INV-103 and INV-109 on 30,000 random v25 contexts;
- `omndiff.py`, `quotes25.py`, `newtok.py`: the changed `omn` blocks, the new quoted fragments, and the names and tags of the new conjuncts;
- the mechanical checks of PROCESS.md section 11 were run with the fix-24 scripts `mech24.py` and `names24.py` (scratchpad `fix24/`, read before use) on v24 and v25.

### Verification of the remark

**R25b-01 holds.** `stops25.py` on the review's example (a preventive course started on 1 January 2026, `stop(paused)` on 10 February, `stop(discontinued)` on 30 March, as-of 21 October 2026), with the predicates as written in v24:
- INV-001 (v24) admits the context.
- INV-079 admits two lines: stop 10 February, 41 days; and stop 30 March, 89 days.
- INV-103 requires a post-stop view for both events. For the 30 March event, E-049 requires the on-treatment period (1 January < 31 March), and INV-070 admits 1–28 March, which lies after the course ended.
- INV-068 excludes 1–28 March as an on-treatment period (`notStoppedBefore` is false), and `courseOverlaps(…, March 2026)` is false.

So two parts of the model read two different ends of one course, as the review states. The same holds for a dose change dated after a stop (stop 10 February, reduction 1 March): INV-001 (v24) admits it, INV-103 requires a view for the reduction, and INV-070 admits 11–28 February, after the end of the course, as its on-treatment period.

### Choice between the review's options

**Option (a): at most one stop or pause per course; a restart is a new course.** Chosen, on these grounds:
1. **The day convention fixes one stop date per course.** Section 2.8 (v17) dates a stop or pause "on the last day of the course", and a course has one last day. A second stop event of a course has no date under the convention. Option (b) would therefore need either a dating rule of its own for a later stop, which changes the course-event dates (oscillation watch point 4), or stop events dated after the course has ended. INV-035 and INV-104 would show those as stop markers, and INV-103 would ask for a monitoring view of each. Those are the further special cases that the review's option (b) lists.
2. **A restart is a new course under either option.** INV-001 already admits at most one start per course, and no course-event kind is a restart. So v24 cannot represent a restart within one course either. Option (b) would represent nothing that option (a) does not. Fix 11 already read the context this way ("a restart is a new course").
3. **Size.** Option (a) changes one `omn` block (INV-001), and it makes exact the "every stop or pause" wordings that E-042, E-043, E-046, INV-055, INV-064 and INV-068 already use. Option (b) would change the predicates of INV-070, INV-079, INV-103 and INV-109 and add an earliest-stop function.

**Option (a) does not narrow Stage 1.**
- **OUT-022.** "Stopped, paused or reduced": all three remain events of a course (`stop(discontinued)`, `stop(paused)`, `doseChange(reduction)`). OUT-022's [S-011] "restarting the treatment" is the start of a new course. "The original pre-treatment baseline" stays admissible after a restart, because INV-056, INV-068 and INV-070 bound a baseline only by the start of its own course.
- **OUT-024.** "Start and stop dates, dose changes, treatment duration": each course has one start, one stop and one duration, and a resumed treatment is a second line.
- **OUT-009.** The restart is a start marker.
- **OUT-018 and OUT-021.** A restarted treatment has its own comparison, time points and review view, aligned to its own start.
- **Contexts excluded.** v25 excludes only contexts with two stops of one course, or with a dose change or target-dose date after the stop. Under section 2.8 these are not states of a course: a dose change and the reaching of the target dose are dated on a day at the new dose, which is a day of the course.

**How the two cases are shown in v25** (`stops25.py`):
- **Pause followed by a restart** (course t1: start 1 January 2026, `stop(paused)` 10 February; restart as course t2 of the same drug: start 1 May, stop 30 September):
  - t1 has a line with stop 10 February and 41 days; a post-stop view whose on-treatment period ends on or before 10 February and whose periods after the event begin on 11 February; no time point, because the course is taken through no interval.
  - t2 has a line with stop 30 September and 153 days. It has its own response comparison with the time points of its own start: 1 July (Turkish Box 8), 24 July (NICE CG150 1.3.28), and 1 August (EHF 2022 question 3, IHS 2024 Q2 monthly injectables, the Russian section 7.1, and the first date of the NICE CG150 1.3.27 window). It has its own treatment review view and a post-stop view from 1 October. Its baseline may be December 2025, the original one.
  - The time course shows four markers: start t1, stop t1 (paused), start t2 and stop t2.
- **Pause later made definitive, without a restart** (the review's history):
  - One stop event, dated 10 February, the last day on treatment. The decision of 30 March adds no course event. The context states the stop as a pause or as a discontinuation. No relation distinguishes the two kinds; the markers and the post-stop view show the kind stated.
  - One line: stop 10 February, 41 days, with the stop reason.
  - One post-stop view: its on-treatment period ends on or before 10 February, and its periods after the event begin on 11 February and continue onward, so they also cover the time after 30 March.
  - INV-068's on-treatment periods end on or before 10 February. `courseOverlaps` is true for February and false for March. No time point is required.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R25b-01 | fixed: the review's option (a) | INV-001 (Predicate, Reading, Realises, Evidence, Notes); E-008 (Meaning, Evidence, Notes); section 2.8 (**Day convention**, course events); Notes of E-049 and INV-079; rows OUT-022 (Invariants column, coverage reason) and OUT-024 (coverage reason) | **INV-001, new conjuncts:**<br>• `#{e ∈ c.subject.courseEvents \| e.treatment = t ∧ e.kind is stop} ≤ 1` for every preventive and acute treatment t. This is the review's formula, placed in the existing one-start conjunct.<br>• `∀ e, f ∈ c.subject.courseEvents • e.treatment = f.treatment ∧ f.kind is stop ∧ (e.kind is doseChange ∨ e.kind = targetDoseReached) ⇒ e.date ≤ f.date`: no dose change after the stop or pause, as the review asks. The reaching of the target or tolerated dose is included because section 2.8 dates it, like a dose change, "on the first day at the new dose", a day of the course.<br>**Cycle ends are not bounded.** `cycleEnd(n)` is dated on the first day after the cycle. For a course stopped on the last day of its last cycle (NICE CG150 1.3.29: stop after 2 treatment cycles), that is the day after the stop. A bound would exclude this case, which `intervalOnTreatment` already handles: the time point is kept (`stops25.py`). INV-001 Notes say so.<br>**E-008:**<br>• a course ends with its one stop or pause, dated on its last day on treatment;<br>• a treatment resumed after a stop or pause is a new course of the same drug (`drugOf`), with its own start, course events, guidance types and headache types;<br>• a pause made definitive without a restart adds no course event, and the course keeps its one stop;<br>• the context states that stop as a pause or a discontinuation; every relation treats the two kinds alike (`e.kind is stop`), except that markers and the post-stop view show the kind stated (INV-036, INV-070; checked by script: no `omn` formula names `paused` or `discontinued` outside the `StopKind` declaration, and only two comments, of E-034 `event` and E-049 `event`, mention them);<br>• Evidence: the OUT-022 statement and its [S-011] quote.<br>**INV-001 text:**<br>• the Reading states both new bounds;<br>• Realises gains OUT-022, whose "paused" and restart the new bound reads, and row OUT-022 gains INV-001;<br>• Evidence: OUT-022 and its [S-011] quote; OUT-024 ("start and stop dates, dose changes, treatment duration"), with its [S-013] fragment on duration;<br>• Notes, new paragraph **One stop or pause per course**: every predicate that reads the end of the course refers to the same last day; the restart reading; the original baseline after a restart; the monitoring of a pause made definitive; the cycle-end exception.<br>**Section 2.8.** "A stop or a pause, of which a course has at most one (INV-001), is dated on the last day of the course […]. A treatment resumed after a stop or pause is a new course, with its own start (E-008)." No date changes.<br>**Pointers.** E-049 Notes: the on-treatment period ends on or before the course's one stop or pause, or before a reduction that does not follow it, so it lies within the course. INV-079 Notes: a stopped treatment's line has one stop date and one duration.<br>**Not needed under (a), and not changed.**<br>• INV-070, INV-079, INV-103 and INV-109 Predicates;<br>• the Readings and Notes of INV-070 and INV-109, and E-055: they already speak of "the" stop, the last day of the course;<br>• the "every stop or pause" wordings of E-042, E-043, E-046, INV-055, INV-064 and INV-068.<br>The dose-change markers (INV-035, INV-104) and the dose changes of INV-109 now always lie on or before the stop, by the new conjunct. |

## Other changes

1. **The same defect in prose.** The satisfiability sentences of the INV-068 Notes and the INV-097 Notes spoke of "its first stop or pause", which presupposes several stops. Both now read "its stop or pause" (INV-068 adds "(a course has one, INV-001)"). No other sentence of the model presupposes several stops of one course (grep for "first stop", "earliest stop", "later stop", "second stop", "several stop", "each stop", "any stop", "stops or pauses").
2. **Housekeeping:**
   - header (v25, iteration 25);
   - section 9 ("as of v25");
   - section 11 (iteration 25 entry: no web search, no download, no new source);
   - section 12 (v25 entry).

**Items changed (diff v24 → v25).**
- **9 content items:**
  - 2 elements: E-008 (Meaning, Evidence, Notes) and E-049 (Notes);
  - 4 invariants: INV-001 (Predicate, Reading, Realises, Evidence, Notes), and the Notes of INV-068, INV-079 and INV-097;
  - section 2.8;
  - rows OUT-022 and OUT-024.
- **Bookkeeping:** the header and sections 9, 11 and 12.
- **Formal blocks:** one `omn` block changed, INV-001, with 4 lines added and 1 line edited (`omndiff.py`: 182 blocks in each version, every other block byte-identical).
- **Not changed:**
  - no element or invariant added, withdrawn or renumbered;
  - no level, value, axiom or attribute declaration;
  - no defined predicate or function;
  - no source.

## Checks

| Check | Result |
|---|---|
| The review's example (i) | v24: INV-001 admits it; INV-079 admits stop 10 February with 41 days and stop 30 March with 89 days; INV-103 requires a view of the 30 March event, and INV-070 admits 1–28 March as its on-treatment period; INV-068 excludes that period. v25: the two-stop context is not admissible. The same history, one stop dated 10 February (stated as a pause or as a discontinuation), has one line (41 days) and one post-stop view, with its on-treatment period on or before 10 February and its periods after the event from 11 February. INV-068 admits 1 January – 10 February and excludes 1–28 March. `courseOverlaps` is true for February and false for March. One duration and one on-treatment period. |
| Dose change after a stop | v24 admits stop 10 February with a reduction on 1 March, and INV-070 admits 11–28 February as the reduction view's on-treatment period. v25 excludes the context. A reduction on 1 March followed by a pause on 30 June is admitted, and both views lie within the course. So is a reduction on the stop day. |
| Single-stop courses behave as in v24 (ii) | 40,000 random contexts, with two courses, 0–2 stops, dose changes, target dates and cycle ends. v25 INV-001 holds if and only if v24 INV-001 holds, each course has at most one stop or pause, and no dose change or target date follows it: 40,000 of 40,000. Every context with at most one stop and no such event has the same INV-001 verdict under v24 and v25 (15,769 of 15,769). All other predicates are byte-identical, so their verdicts on these contexts are the same. In every v25-admissible context, each started course has one INV-079 line and one INV-109 span end, and `notStoppedBefore(t, d)` holds exactly when d is on or before that end. `courseOverlaps` equals overlap with the span from the start to the stop (or the as-of date) for every 28-day period tested. Every INV-070 on-treatment bound lies within the course. Every dose change lies in the span. 15,769 of 15,769. Each of the 24,231 contexts that v24 admits and v25 does not has a course with two stops (73 such courses with both stops on one date) or a dose change or target date after the stop (`breakdown.py`, same 40,000 contexts). 21,284 of them fail at least one of the consistency checks above. The other 2,947 fail none, because those checks cover only started courses and only the end readings named; they are excluded all the same. |
| Watch-point examples (iii) | Unchanged from v24 (fix 17, fix 18, check 24):<br>• Review-18 antibody (start 1 January 2026): stopped on 10 February, no time point; on 30 March, NICE CG150 1.3.28 and Turkish Box 8; on 31 March, all six; uninterrupted, the six time points 1 April ×4, 26 March and 1 March.<br>• Stop on the start day: the on-treatment period is required, and a 1-day period meets INV-070; the line shows 1 day.<br>• Reduction on the start day: not required, and no period exists (E-049, fix 02 item 5 and fix 17 kept).<br>• NICE 1.3.29 with the stop on the last day of cycle 2 (`cycleEnd(2)` = the next day): admitted by v25 INV-001, and `intervalOnTreatment` holds.<br>• E-042: March ends at 1 April; 26 February – 25 March ends at 26 March; 4–31 December is 28 days.<br>• INV-049: day 43, window 7 April – 5 May, first 28-day range ends 6 April. |
| Satisfiability pass | **Method.** By script (`sat25.py`) and by hand, in every admissible v25 context. Restricting `Ctx` only removes contexts, so no repertoire obligation is added.<br>**INV-001.** Satisfiable: a context without treatments, and every history of the two cases above.<br>**INV-055 with E-042 and E-043.** The fix-18 construction is a 28-day on-treatment period ending on the day before the time point (for a window, before the later of its first date and day 28). It begins on or after the start, meets `atTimePoint`, and lies within the course: 197,471 of 197,471 required time points (8 rules, start and target-dose anchors).<br>**INV-068, INV-102.** A period from the start to the stop date (or 28 days) is admitted: 30,000 of 30,000.<br>**INV-070, E-049, INV-103.** For every INV-103 event, the E-049 `when` clause holds exactly when a period exists, and a period from the start to the day before the first changed day is admitted and lies within the course: 29,798 of 29,798.<br>**INV-079, INV-109, E-055.** One stop date and one span end, not before the start: 30,000 of 30,000.<br>**E-067, INV-105.** `courseOverlaps` and `courseNotOutside` are unchanged. With one stop they agree with the line's span (above), so the treatment-effect conjunct is satisfiable as in fix 16.<br>**E-046, INV-063, INV-064.** `evaluatedOnTreatment` is unchanged, and labels are optional.<br>**INV-035, INV-104.** Markers take start, dose change and stop events, now all within the course.<br>**INV-097.** Periods of a common length no longer than the days on treatment before the changed regimen.<br>**Result.** No MUST or SHOULD combination of the invariants named in the review becomes unsatisfiable, and no derived attribute is required where its relation is undefined. |
| Headings and IDs (`mech24.py`) | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn). No dangling E-, INV- or ISS- reference. 36 source IDs cited, all within S-001–S-046 or S-101–S-106. Every OUT reference exists in Stage 1. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field; no item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches (INV-001 now realises OUT-022, and row OUT-022 lists it). |
| Types and names (`names24.py`, `newtok.py`) | 746 declared names, none declared twice, the same as in v24. The token report is identical for v24 and v25. The new conjuncts use only the declared attributes `subject`, `courseEvents`, `preventiveTreatments`, `acuteTreatments`, `treatment`, `kind` and `date`, the `CourseEventKind` tags `stop`, `doseChange` and `targetDoseReached`, and the bound variables c, t, e and f. `e is t` applies to variant values and tags (section 2.6), `#` to a finite comprehension, and `≤` to dates. Brackets are balanced, and no partial term is used. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34, unchanged. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged, with no typing-rule violation. INV-001 stays definitional (context scope); its new conjuncts exclude only contexts that are not states of a course under section 2.8. |
| Diff of formal blocks | Only the INV-001 `omn` block changed. Watch point 4 is kept: the course-event dates of section 2.8, `atTimePoint`, `fitsMonthlyPeriod`, the INV-049 `<`, `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, `firstChangedDay` and the E-049 `when` clause are byte-identical, and `a ≤ e.date` is not re-added. INV-105 (`courseOverlaps`, `courseNotOutside`) and the INV-079 and INV-109 Predicates are byte-identical. Watch point 1 is kept: every v24 by-dates relation is byte-identical. Guarantee-term counts v24 → v25: `notStoppedBefore(` 8 → 8, `intervalOnTreatment(` 8 → 8, `evaluatedOnTreatment(` 6 → 6, `courseOverlaps(` 6 → 6, `courseNotOutside(` 8 → 8, `firstChangedDay(` 5 → 5, `next(p.end)` 6 → 6, `sameSpan(` 30 → 30, `sameIndicatedPeriod(` 7 → 7, `summarisesMedication(` 14 → 14. |
| Quotes (`quotes25.py`) | 30 quoted fragments on changed lines. 21 are verbatim in Stage 1 v18, including the OUT-022 statement and [S-011] quote and the OUT-024 statement and [S-013] fragment. 9 were already in v24. None is unmatched, and no source quote was added or changed. |
| Scope sweep | Term counts v24 → v25 for record, enter, entry, input, captur, logged, stor, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, questionnaire, data-entry, "derived from", "diary information", intake, "decision logic", taken and took: all equal except two. "stor" (61 → 62) is the path `history/v24.md` in the section 11 entry. "taken" (55 → 56) is "the course is taken through its interval" (INV-001 Notes), the existing phrase for a context property. "Restarted", "resumed" and "made definitive" describe the subject's treatment courses in the output context (E-008), whose becoming known is outside the model. The new conjuncts take only context properties as arguments. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v25.md`: identical. `history/v24.md` is unchanged (equal to HEAD). |
