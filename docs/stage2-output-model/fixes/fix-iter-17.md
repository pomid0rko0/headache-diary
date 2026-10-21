# Fix log — iteration 17
Input review: reviews/review-iter-17.md · Input version: v16 · Output version: v17
Date: 2026-10-21

## What was read, downloaded and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039), and the source rows of section 5 that I needed (S-005, S-011, S-015);
- v16 (`OUTPUT_MODEL.md`, byte-identical to `history/v16.md`, checked with `cmp`), sections 1–12;
- review 17.

**Earlier loop files read, so that no fix is undone:**
- the oscillation check after iteration 16, with its eight watch points, and the watch points of the check after iteration 12;
- review 02 (R02-01, the `fitsMonthlyPeriod` guard) and fix 02 (R02-01; item 5, the `when` clause of E-049 `onTreatmentPeriod`);
- review 05 ("Time points as period ends", checked and not raised);
- review 15 (R15-01; "Several stop events in one course"; the post-stop baseline) and fix 15 (identifying-property table);
- fix 16 (format and checks).

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. No earlier fixer declined a remark on the topics of review 17.

**Downloads.** With `curl` into the fresh directory `/tmp/r17fix-dl-IMOw`, outside the repository:
- [S-015] NICE CG150 Recommendations page (Stage 1 URL, HTTP 200, "Last updated: 03 June 2025"): recommendations 1.3.27 ("3 to 6 months after starting"), 1.3.28 ("Stop CGRP inhibitors after 12 weeks of treatment if the frequency of migraines does not reduce by:"), 1.3.29 ("after 2 treatment cycles") and 1.3.48 ("4 to 8 weeks after the start of withdrawal of overused medication") read as Stage 1 quotes them;
- [S-005] IHS paediatric trial guideline (Stage 1 URL, ihs-headache.org PDF, HTTP 200): "Thus, if a baseline period is 28 days, the final 28 days of the treatment period should be assessed." is verbatim in the `pdftotext -raw` text (the `-layout` text interleaves the two columns).

No web search and no new source. The new text quotes only fragments of Stage 1 quotes.

**Scripts.** All are in the session scratchpad, `r17fix/` (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r17fix/`), and were run with `python3 -I`:
- `tp.py`: the date arithmetic of the 18 rules (values copied from E-041) under the v16 and the v17 relation: the review's examples; whether `fitsMonthlyPeriod` is exact (it holds if and only if some calendar month or 28-day period that begins on or after the start satisfies `atTimePoint`) in 53 680 cases (starts every third day of 2025–2026, the rule's anchor kinds, cycle ends from 0 to 252 days after the start); the INV-055 construction; the course-event ordering; and the other day boundaries (INV-049, INV-051, INV-045 / INV-089, INV-087, INV-070);
- `inst.py`: R17-02 on the review's example and on witnesses, and the INV-070 and INV-049 changes, each in its v16 and v17 form;
- `mech.py`, `names.py`: the mechanical checks of PROCESS.md section 11 on v16 and v17;
- `watch.py`: byte-identity of the watch-point items, and counts of the guarantee terms;
- `changed.py`: the items and fields changed from v16;
- `quotes.py`: every quoted fragment added in v17 against Stage 1 v18 and the downloaded texts;
- `scope.py`: scope-term counts in v16 and v17, and the hits on changed lines.

### Verification of the remarks

**R17-01 holds.** The model counts the start day as a day on treatment: INV-056 lets an on-treatment period begin on the start, and INV-079 counts both the first and the last day of a course (`days`). So n weeks of treatment are the days s to `plusDays(s, 7n − 1)`. INV-058 puts the time point at `shift(anchor, offset)`, the first day after the interval, and v16 `atTimePoint` required `p.end = tp.earliest`, so the required period always contained one day after the interval. `tp.py`, for an anti-CGRP monoclonal antibody started on 1 January 2026 (adult, migraine), with December 2025 and March 2026 as baseline and on-treatment months:

| Rule | Time point (earliest; latest) | March meets it: v16 | v17 |
|---|---|---|---|
| `ruleEhf2022Q3`, `ruleIhsQ2Monthly`, `ruleRu71` | 1 April 2026 | no | yes |
| `ruleNice1327` | 1 April; 1 July 2026 | no | yes |
| `ruleTrBox8` | 1 March; 1 April 2026 | yes | yes |
| `ruleNice1328` | 26 March 2026 | no | no (a calendar month cannot end on 25 March) |

The final 28 days of the 12 weeks of NICE 1.3.28, 26 February to 25 March 2026, meet it under v17 and not under v16; the 28-day baseline 4–31 December 2025 has the same length. The 28-day period that begins on the start covers exactly the first 4 weeks and meets a 4-week time point under v17, not under v16. The cycle-end anchors had no stated date convention (E-008).

**R17-02 holds.** E-055 `formulations` (SHOULD for acute lines) was tied to nothing: no conjunct of INV-079 or any other invariant constrains it. INV-074 tied a treated-attack line's formulation to its summary only for single-formulation summaries. The review's example (an oral-only sumatriptan user whose acute line shows `{subcutaneous}`, with subcutaneous attack lines in a summary of all formulations naming `{oral, subcutaneous}`) satisfies every v16 invariant (`inst.py`). OUT-024 asks for the formulation so that the EHF triptan-refractoriness definition, which turns on the subcutaneous formulation, can be applied, so a formulation the patient never took is a false statement on exactly the point Stage 1 names. The context holds the needed fact (`acuteMedications`, drug and formulation, history-wide, E-008).

**R17-03 holds.** Section 2.3 defines `fun f : T₁ × … × Tₙ → T` (given) and `fun f(x₁ : T₁, …) : T ≙ e` (defined). `mech.py` on v16: of 40 `fun` declarations, exactly two are in neither form, `fun outputOf(x : Element) : Output` and `fun viewOf(x : Item) : View`.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R17-01 | fixed: the review's option (a) | Section 2.8 (new item **Day convention**); E-008 (Meaning); E-041 (Meaning, Notes); E-042 (Definition: `atTimePoint`, `fitsMonthlyPeriod`, comments of `earliest` and `latest`; Meaning; Evidence); E-043 (Notes); INV-055 (Reading, Notes); row OUT-018 | **Convention (section 2.8, stated once).** Periods, spans and windows include both end days. A course includes its start day; a dose change and the reaching of the target or tolerated dose are dated on the first day at the new dose; the end of treatment cycle n (`cycleEnd(n)`) on the first day after the cycle, the day by which it is complete; a stop or pause on the last day of the course (as INV-079, INV-109 and `courseOverlaps` already treat it). An interval of n weeks or months from a day a runs from a to the day before `shift(a, …)`, and `shift(a, …)` is the date after it, on which an evaluation or review falls. A period ends with the interval when `next(p.end)` is that date.<br>**Relations (E-042).** `atTimePoint`: `next(p.end) = tp.earliest` for `atOffset` and `atLeastOffset`; `tp.earliest ≤ next(p.end) ∧ ∀ l ∈ tp.latest • next(p.end) ≤ l` for `withinWindow`. `fitsMonthlyPeriod`: `plusDays(s, shortestMonthlyDays) ≤ …` instead of `plusDays(s, shortestMonthlyDays − 1) ≤ …`.<br>**Unchanged (watch point 5; the orchestrator's instruction):** `shift`, INV-058, the INV-055 predicate text, and every `excludes`, `timing`, `ages`, `AgeCoverage`, anchor and offset value of the 18 rules (`watch.py`: the E-041 `omn` block is byte-identical). Time-point dates are unchanged, so the `excludes` criterion gives the same values, and the E-041 statement that the NICE 1.3.29 time point is "24 weeks after the first injection" now follows from the stated `cycleEnd` date.<br>**Why (a), not (b).** (a) keeps `earliest` as the date on which the evaluation falls, as INV-051 does for the review window, and treats all anchors alike; (b) would have needed a case split of INV-058 by anchor kind (one day before `shift(…)` for start and dose anchors, the cycle-end date itself for cycle anchors).<br>**R02-01.** The guard is kept and re-expressed: `tp.py` finds it exact in all 53 680 cases under v17 (and under v16 for the v16 relation), and the INV-055 construction (a 28-day period whose last day is the day before the time point, or before the later of the window's earliest date and the 28th day after the start) works in every case where it holds. Course-event ordering (INV-001): every rule except the three cycle-end rules fits for every anchor on or after the start; the cycle-end rules fit exactly when the cycle-end date is at least 28 days after the start, the case the E-041, E-043 and INV-055 Notes describe.<br>**Text aligned:** E-041 Meaning (a time point is the date on which the evaluation falls; the evaluated period ends on the day before) and Notes (cycle-end time points less than 28 days after the start); E-042 Meaning (with the review's two examples) and Evidence (Stage 1 [S-005] "the final 28 days of the treatment period should be assessed", [S-011] "after a minimum of 3 consecutive months on treatment", [S-015] "after 12 weeks of treatment"); E-043 Notes; INV-055 Reading, Notes and satisfiability argument (with the examples); row OUT-018. |
| R17-02 | fixed; the review's optional tie of a summary's own formulations declined | INV-079 (Predicate, Reading, Evidence, Notes); INV-075 (Predicate, Reading, Evidence, new Notes); INV-074 (Predicate, Reading, Evidence, new Notes); E-051, E-053, E-055 (Notes); rows OUT-023, OUT-024 | **INV-079** (definitional), new conjunct: `l.role = acute ⇒ ∀ f ∈ l.formulations • AcuteMedication(drug ↦ l.drug, formulation ↦ f) ∈ ctx.subject.acuteMedications` (the review's formula).<br>**INV-075** (definitional, all treated-attack lines), new conjunct: `∃ m ∈ ctx.subject.acuteMedications • m.drug = l.drug ∧ ∀ f ∈ l.formulation • m.formulation = f`. It is the review's tie for the formulation and also ties the line's drug (Other changes, item 3). I put it in INV-075, which constrains every line, rather than INV-074, which constrains only the lines of a summary's sequence; the review allows either.<br>**INV-074**: `(s.formulationScope = singleFormulation ⇒ ∀ f ∈ l.formulation • f ∈ s.formulations)` becomes `(s.formulationScope = singleFormulation ∨ s.formulations ≠ ∅ ⇒ …)`. So the requirement now holds for every summary that names its formulations, and is unchanged for single-formulation summaries. For a summary of all formulations that names none (a deviation from the SHOULD of E-051 `formulations`), an unconditional `f ∈ s.formulations` would forbid every line from stating its formulation, a constraint no Stage 1 part asks for. INV-072 together with the new INV-075 tie already gives the review's result in every fully conformant output (INV-074 Notes).<br>**Optional summary tie declined.** A summary's formulation states the scope of what it summarises, not a use. A 0-attack summary of a formulation the subject never used is a correct value (E-008 Meaning). It can show that a formulation was not tried, for example subcutaneous sumatriptan, which is the point of the EHF refractoriness definition, and E-051 Notes already say that it "stands in for none". Requiring every named formulation to be a used one would exclude that output, which Stage 1 permits. E-051 Notes now say so.<br>**Kept (watch point 3):** `summarisesMedication`, and the type-scope, period and `adherenceFor` ties of R13-01, R14-02 and R15-02 (`watch.py`: E-051 Definition, INV-062, INV-069, INV-071, INV-072, INV-088, INV-104, INV-105 and INV-109 byte-identical; `summarisesMedication(` 14 occurrences in v16 and in v17). The OUT-023 reading is not decided. |
| R17-03 | fixed: the review's option (a) | E-002 (Definition); E-003 (Definition); section 2.5 | `fun outputOf : Element → Output` and `fun viewOf : Item → View`, given total functions (section 2.3). The comments state their meaning by composition: an output belongs to itself, a view to the output of which it is a part, an item to the output of its view. Section 2.5 now says that both are given total functions declared in E-002 and E-003, whose values the composition fixes; the old cross-reference "(section 5, E-003, E-004)" pointed to E-004, where neither is declared. Both functions are total, because every `Element` atom is an `Output`, a `View` or an `Item`, every view is part of exactly one output and every item of exactly one view (section 2.5). Every use applies `viewOf` to an `Item` and `outputOf` to an `Element` (checked by hand: INV-007, INV-032, INV-033, INV-054, INV-059, INV-060, INV-062, INV-066, INV-072, INV-087, INV-092, INV-093, INV-109, E-032, E-046, E-063, E-066). |

## Other changes

The orchestrator asked me to check, as the same defect nearby, every place where a date is compared with the first or last day of a period, and to fix only genuine off-by-one inconsistencies with the convention I settled on. With the convention stated (section 2.8), I checked each place:

| Place | Comparison | Result under the convention |
|---|---|---|
| `shift` (E-041), INV-058 | the time point is the date after the interval | consistent; unchanged |
| `atTimePoint`, `fitsMonthlyPeriod` (E-042) | the period's last day against the time point | **off by one**: R17-01 |
| INV-055 | `shift(a, r.minOffset) ≤ c.asOf`: the evaluation date has been reached | consistent (the evaluated period ends on the day before); unchanged |
| INV-051, INV-050 | review window `plusDays(ws, 28)` to `plusDays(ws, 56)`: dates of review "4 to 8 weeks after the start of withdrawal" | consistent (review 17 checked it as dates of review); unchanged |
| **INV-049** | `c.timeRange.to ≤ plusMonths(ws, 12)` and `c.asOf ≤ plusMonths(ws, 12)`, "within the following year" | **off by one**: `plusMonths(ws, 12)` is the first day after the year. Fixed (item 1) |
| INV-045 | span "> 3 months": `plusMonths(first.start, 3) ≤ last.end`, shortest-span conjunct | consistent (`tp.py`); unchanged |
| INV-089 | remission "must exceed three months": `plusMonths(s, 3) ≤ e` | consistent (`tp.py`); unchanged |
| INV-079, INV-109, E-055 | duration `days(s, e)` and course span from start to stop, both days included | consistent, and they fix the stop date as the last day of the course; unchanged |
| `courseOverlaps`, `courseNotOutside` (E-067) | `e.date < p.start`: stopped before the period | consistent (a stop on the first day of p means its last day lies in p); unchanged (watch point 1) |
| **INV-070, E-049** | after-periods begin on the event date; the on-treatment period ends before it | **off by one for a stop or pause** (dated on the last day of the course): the first period after a stop contained its last day on treatment, and the period that ends on the last day of treatment (for example the final 28 days before a stop) could not be the on-treatment period. Fixed (item 2). For a dose reduction (dated on the first day at the reduced dose) consistent. |
| INV-056, INV-068 | baseline ends before the start; on-treatment periods begin on or after it | consistent; unchanged |
| INV-064, INV-067, `adherenceFor` (E-047) | evaluated months and adherence window begin on or after the start | consistent; unchanged |
| E-046 `evaluationResult` and `pretreatmentBaseline`, INV-062 | an instrument result completed on the start day is the pre-treatment baseline | not a period boundary: a reading of result dates that the E-046 Notes state and justify (the recall of a result completed on the start day covers the time before treatment); unchanged |
| INV-087 | A1.1 window day 1 ± 2 (days −2 to +3, no day 0); `nextWindowDays` | consistent (`tp.py`); unchanged |
| E-005 `ofKind`, `periodEndFrom`, INV-004 `consecutive`, E-038 `mostRecent`, INV-035 and INV-104 markers (`inPeriod`), INV-096 to INV-098 (`childOn` on the first day of a period) | inclusive days | consistent; unchanged |

1. **INV-049, the following year** (E-039 Conformance and Notes; INV-049 Predicate and Reading). In both conjuncts `≤ plusMonths(ws, followUpMonths)` becomes `<`, and the Reading and E-039 now state the year as the days from the start of withdrawal to the day before `plusMonths(ws, 12)`. The first conjunct requires no fewer ranges in practice: no whole-period time range from a start of withdrawal ends on `plusMonths(ws, 12)` (`tp.py`, every start in 2025–2027). The second no longer asks, on the anniversary itself, for a running view of 366 or 367 days. Review 17 called the difference immaterial; under the convention it is a one-day deviation from the invariant's own Reading ("while the as-of date lies within that year"), so it is fixed. The running-follow-up conjunct is kept (iteration-12 watch point 5).
2. **INV-070, the periods after a stop or pause** (E-049 Definition, Meaning, Conformance and Notes; INV-070 Predicate, Reading and new Notes; INV-097 Notes; row OUT-022). New defined function in E-049: `fun firstChangedDay(k : CourseEventKind, d : Date) : set Date ≙ {x : Date | (k is stop ∧ x = next(d)) ∨ (k is doseChange ∧ x = d)}`. It gives the first day of the changed regimen: the first day off treatment after a stop or pause, or the first day at the reduced dose. INV-070 begins the periods after the event on that day and ends the on-treatment period before it. The `when` clause of `onTreatmentPeriod` reads `∃ s ∈ startOf(ctx, self.treatment); x ∈ firstChangedDay(self.event, self.eventDate) • s < x`, so the on-treatment period is required for every stop or pause and, as fix 02 (item 5) set it, for a reduction later than the start day. Fix 02's reason ("impossible for a stop, pause or reduction on the start day") still holds for a reduction. For a stop it no longer holds, because the stop date is a day on treatment: a course that stops on its start day has a one-day on-treatment period. The alternative, dating a stop on the first day off treatment, would have changed INV-079, INV-109, `courseOverlaps` and `courseNotOutside` (watch point 1), so I did not take it.
3. **INV-075, the drug of a treated-attack line.** The new conjunct also ties the line's drug to an acute medication the subject has used, which v16 left free when the line shows no formulation (`inst.py`: a line of ibuprofen, never used, met v16). This is the same defect, a stated fact of use tied to nothing. Treatment lines need no such tie, because INV-079 and INV-001 already tie their drug.
4. **Housekeeping:** header (v17, iteration 17); section 9 ("as of v17"); section 11 (iteration 17 entry: no web search, two downloads, no new source); section 12 (v17 entry).

**Items changed (script, v16 → v17).**
- 18 model items: E-002, E-003, E-008, E-039, E-041, E-042, E-043, E-049, E-051, E-053, E-055 (11 elements) and INV-049, INV-055, INV-070, INV-074, INV-075, INV-079, INV-097 (7 invariants).
- Sections 2.5 and 2.8, and rows OUT-018, OUT-022, OUT-023 and OUT-024.
- The header and sections 9, 11 and 12.

Formal changes: the declarations of `outputOf` and `viewOf`, `atTimePoint` and `fitsMonthlyPeriod`, E-049 `onTreatmentPeriod` with the new `firstChangedDay`, and the predicates of INV-049, INV-070, INV-074, INV-075 and INV-079. No element or invariant was added, withdrawn or renumbered, no level changed, and no source was added.

### Satisfiability pass

I checked the changed relations and invariants together with the invariants that constrain the same elements and views.
- **Response comparison** (INV-055 with INV-003, INV-011, INV-054 to INV-061, INV-066, INV-067, INV-097, INV-104, INV-105, INV-109).
  - For every applicable rule and anchor whose time point fits and has been reached, take a 28-day on-treatment period whose last day is the day before the time point (for a window, the day before the later of the earliest date and the 28th day after the start). It begins on or after the start (`tp.py`, every case where the guard holds). A 28-day baseline period ends before the start.
  - Equal lengths hold (INV-055, INV-097). The adherence window equal to the on-treatment period meets `adherenceFor` and INV-067.
  - The time points are those of INV-058, whose dates are unchanged, so INV-059 is unaffected.
  - Where the guard fails, nothing is required, and `tp.py` confirms that then no monthly period can end at the time point.
  - INV-055 asks for each rule and anchor in some output, so several time points never have to share one period.
- **Withdrawal follow-up** (INV-049 with INV-050 to INV-052, INV-003, INV-011). INV-049 now requires less, by one day, and INV-050 and INV-051 are byte-identical, so the v16 satisfiability argument of the INV-049 Notes carries over.
- **Post-stop monitoring** (INV-070 with E-049, INV-003, INV-011, INV-097, INV-098, INV-103).
  - Let x be the first day of the changed regimen and L ≤ the number of days on treatment before it. The on-treatment period of L days ending on the day before x, a baseline of L days ending before the start, and consecutive after-periods of L days from x meet INV-070 and INV-097 together (`inst.py`, for a stop, a reduction and a stop on the start day).
  - For a reduction on the start day, the `when` clause asks for no on-treatment period, and none is possible.
  - The `when` clause holds exactly when such a period can exist, so the SHOULD attribute is never required where INV-070 forbids it.
- **Formulation ties** (INV-074, INV-075, INV-079 with INV-001, INV-062, INV-069, INV-071, INV-072, INV-073, INV-088, INV-104, INV-105, INV-109, E-053, E-055).
  - The drug of every acute treatment is the drug of an acute medication (INV-001), so a non-empty `formulations` of an acute line can be chosen (E-055 SHOULD).
  - Every required summary is of a used medication's drug, of all formulations or of `{m.formulation}` (`summarisesMedication`, INV-071).
  - A summary of all formulations names every used formulation of its drug (INV-072), so every line of a truthful output (an attack treated with a used medication) meets INV-074 and INV-075.
  - Summaries with 0 treated attacks have no lines. No invariant requires a summary that names only some of the used formulations.
  - `inst.py` confirms the witnesses: an oral line in an all-formulation summary naming `{oral}`, a line without formulation, a summary naming no formulation, and a single-formulation summary.
- **Definedness.**
  - `next` and `plusDays` are total. `firstChangedDay` is a defined, set-valued function with one member for the event kinds INV-070 admits.
  - `first(v.after)` is guarded by `v.after ≠ ∅`.
  - `l.formulation`, `l.formulations` and `tp.latest` are used only inside quantifiers (section 2.6).
  - No derived attribute was added. The relation of `earliest` and `latest` (INV-058) is unchanged and defined for every rule.
- **Levels.**
  - INV-049 (SHOULD), INV-055 (MUST) and INV-070 (SHOULD) keep their levels.
  - INV-074, INV-075 and INV-079 stay definitional. The new conjuncts exclude only outputs that state a formulation or drug the subject never used, or a line formulation that contradicts the formulations its summary names as those it summarises (section 3.3, item 5).

**Result.** No admissible context makes the MUST and SHOULD invariants that constrain these elements and views jointly unsatisfiable, and no derived attribute is required where its relation is undefined.

### Watch points (oscillation/check-after-iter-16.md)

1. **INV-105 and E-067** are byte-identical: `courseOverlaps`, `courseNotOutside`, `within`, `allTypes` and `summarisesMedication` are unchanged.
2. **E-062 `acute` and E-045 `valueAvailable`** are byte-identical. E-008's Definition and Notes are byte-identical; only its Meaning gained the dates of the course events.
3. **Acute summaries and adherence.** INV-062, INV-066, INV-069, INV-071, INV-072, INV-088, INV-104 and INV-109, and the E-047 and E-051 Definitions, are byte-identical. `summarisesMedication` is kept, and the OUT-023 reading is not decided. The new INV-074 conjunct only tightens.
4. **Responder labels.** E-012, E-045, E-046, INV-062, INV-063 and INV-064 are byte-identical.
5. **E-041.** The `omn` block is byte-identical: every `excludes`, `timing`, `ages`, `AgeCoverage`, anchor and offset value is unchanged, `ruleTr73` is kept, and the age is still read on the treatment start. Only the Meaning and the last sentence of the Notes changed (the date convention).
6. **INV-098** is byte-identical.
7. **Earlier watch points.**
   - Co-presence: INV-003, INV-054, INV-056, INV-078 and E-040 are byte-identical.
   - Menstrual-relation view: INV-086, INV-087, E-060 and E-061 are byte-identical.
   - Withdrawal follow-up: INV-050, INV-051 and the E-039 Definition are byte-identical. INV-049 keeps both conjuncts and changes only `≤` to `<`.
   - The E-008 time-frame components are byte-identical.
8. **Change volume.** 18 model items and 4 rows, with no sweep. The extra items beyond the remarks come from the date-boundary check the orchestrator asked for (INV-049, INV-070 and their elements) and from aligning paraphrases. Guarantee-term counts are equal in v16 and v17: `summarisesMedication(` 14, `courseOverlaps(` 6, `courseNotOutside(` 8, `s.typeScope = allTypes` 9, `adherenceFor(` 7, `scopeFor(` 8, `#L.evaluated = 1` 7, `rc.treatment = L.treatment` 13, `fillsPeriod` 15, `menstruatesDuring` 9, "a later time point of its own" 4, `acuteMedications ≠ ∅` 3.

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-11; ISS-07 appears only as withdrawn (section 8 note, section 9, change log). |
| References | No dangling E- or INV- reference. S references lie in S-001–S-046 and S-101–S-106, and every S-1NN has a row in section 10. Every OUT reference exists in Stage 1, and all 39 requirements are referenced. |
| Fields | Exactly one Realises and one Conformance field in each of the 177 elements and invariants. No Realises field changed. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every OUT, the row's E and INV sets equal the sets derived from the Realises fields. |
| Types and names | The only capitalised names in `omn` blocks (text literals aside) that are not declared are the bound variables A, C, D, K, Ks and L (`names.py`). No name is declared twice (337 declared names). The only applied names without a `pred` or `fun` declaration are `refs` (section 2.5), `first` and `last` (section 2.6), and sequence applications (`s(i)`, `basis(j)`, `periods(i)`, …), as in v16. `firstChangedDay` is declared once (E-049) and used in E-049 and INV-070. All 181 `omn` blocks have balanced brackets. |
| Declaration forms | 41 `fun` declarations, all in one of the two forms of section 2.3 (v16: 2 of 40 in neither form, R17-03). |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33; total 110, unchanged. Scopes: output 77, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Date arithmetic (`tp.py`) | The review's examples as tabulated above. `fitsMonthlyPeriod` is exact in 53 680 cases under v17 (0 mismatches) and the INV-055 construction never fails. Cycle-end rules fit exactly from 28 days after the start; every other rule fits for every anchor on or after the start. |
| Instance checks (`inst.py`) | R17-02: the review's example holds under v16 and fails under v17 (INV-079, INV-074 and INV-075); the conformant witnesses hold. INV-070: March before a stop dated 31 March with periods after from 1 April holds under v17 only; a reduction dated 1 April holds under both. INV-049: the running view on the anniversary is no longer required. |
| Quotes | Seven new quoted fragments, all verbatim in Stage 1 v18 (`quotes.py`). No source quote was added or changed. The S-005 sentence and the NICE wording were also confirmed in the downloaded texts. |
| Scope sweep | Searched the whole document for enter, entry, record, input, captur, logged, store/storage, persist, database, JSON, XML, CSV, FHIR, HL7, serializ/serialis, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field, questionnaire, data-entry, "derived from", "diary information", intake, "decision logic", took and taken. Every count equals v16 except "took" (0 → 2): the INV-079 Notes and row OUT-024 say that a line's formulation states in which formulation the patient took the drug. This is the clinical meaning of a shown value, as E-053's "the medication and formulation taken" already is, not input data. The other hits on changed lines ("taken effect" in the E-041 Notes, "timing of intake" in row OUT-023) are unchanged phrases. Every relation added takes only output elements, context properties and constants as arguments. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v17.md`: identical. `history/v16.md` is unchanged. |
