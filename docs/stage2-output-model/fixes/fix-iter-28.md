# Fix log — iteration 28
Input review: reviews/review-iter-28.md · Input version: v27 · Output version: v28
Date: 2026-10-22

## What was read and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039). OUT-018, OUT-020, OUT-021, OUT-022, OUT-024 and OUT-039 and their evidence were read closely. The key wordings:
  - OUT-022: "After a preventive treatment is stopped, paused or reduced, the diary output SHOULD continue to show headache and migraine frequency and compare it with both the on-treatment period and the original pre-treatment baseline";
  - OUT-021: "for the same pre-treatment baseline and on-treatment periods"; "The purpose is that efficacy can be judged across these dimensions";
  - OUT-024: "a chronological list of preventive (and, separately, acute) treatments with start and stop dates, dose changes, treatment duration, the response summary from OUT-018 or OUT-023 for each treatment";
  - OUT-039: "over the evaluation window, next to the response comparison of OUT-018";
- v27 (`OUTPUT_MODEL.md`, byte-identical to `history/v27.md`), sections 1–12 in full. E-008, E-034, E-039 to E-049, E-051, E-054, E-055, E-066, E-067, INV-001, INV-027, INV-035, INV-036, INV-049 to INV-079, INV-097 and INV-102 to INV-109 were read closely, and every `omn` block was searched by script for start-, stop-, anchor- and date-tied terms (`occ28.py`);
- review 28 (two remarks, R28-01 and R28-02), with its "Checked and not raised" list.

**Earlier loop files read, so that no fix is undone:**
- fix 27 (`originalStart` without the fallback; the E-049 `when` clause of `baseline`), fix 26 (`resumes`, `resumesFrom`, the INV-001 chain conjuncts, its consequences table) and fix 25 (one stop or pause per course; a restart is a new course);
- fix 02 (the `when` clauses of E-055 and E-049), fix 05 (the start tie of INV-064, added because the tie "existed only in INV-062, at SHOULD") and fix 14 (R14-02: the span of an acute line's summary, left unconstrained for a course without a stated start because it has "no stated span");
- the oscillation check after iteration 24 and its ten watch points, in particular watch point 4 (section 2.8, `atTimePoint`, `fitsMonthlyPeriod`, `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, `firstChangedDay`, and the E-049 `when` clause of `onTreatmentPeriod`: required for a stop on the start day, not for a reduction on the start day), watch point 8 (INV-105, E-067) and watch point 9 (change volume; the items aligned in v22–v24).

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. No earlier fixer declined a remark on courses whose start the context does not state; review 27 set the case aside, and fix 27 decided it for the E-049 baseline only.

**No download and no web search.** Every quoted fragment on a changed line is verbatim in Stage 1 v18 or already in v27 (`quotes28.py`).

**Scripts.** All are in a fresh scratchpad folder, `fix28b/` (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix28b/`), and were run with `python3 -I`:
- `p28.py` transcribes, as written in v27 and as written in v28, every predicate this fix changes (INV-064, INV-067, INV-068, INV-070, INV-078, INV-079, INV-103, INV-109, the new `courseBegunBy`) and the unchanged ones they read (INV-001, `startOf`, `resumesFrom`, `originalStart`, `notStoppedBefore`, `firstChangedDay`, the E-049 `when` clauses, INV-102).
- `ex28.py` (output `ex28.out`) runs them on the review's example B, on the same course with a stated start, on the watch-point examples and on examples for INV-078, INV-079 and INV-109.
- `rand28.py` (output `rand28.out`; reproducible, two runs byte-identical; a second seed in `rand28_seed2.out` gives the same conclusions) runs 20,000 random admissible contexts: chains of one to three resumed preventive courses whose first start is stated or not, unrelated preventive courses with and without a stated start, stops and reductions on the start day, target-dose dates, cycle ends (also on the day after the stop) and acute courses with and without a stated start.
- `apply28.py` builds v28 from `history/v27.md` by 55 exact replacements, each asserted to occur exactly once.
- `mech27.py`, `names27.py`, `tokcheck27.py`, `omndiff27.py`, `itemdiff27.py` and `scope27.py` are copies of the fix-27 scripts, and `quotes28.py` of `quotes27.py`, read before use; `watch28.py` checks the watch-point items.
- A scratch folder `fix28/` from the lost earlier attempt exists. I read its predicate script and its example output for orientation only; no script, result or text of it was used.

### Verification of the remarks

Both remarks hold (`ex28.out`, predicates as written in v27). Example B: course t1 with no stated start, `doseChange(reduction)` on 15 March 2026 and `stop(paused)` on 30 June 2026; t2 starts on 1 September 2026, resumes t1 and is reduced on 1 October; as of 21 October 2026. INV-001 admits it.

| Check | t1 without a stated start (v27) | t1 started on 1 January 2026 (v27) |
|---|---|---|
| INV-103 requires a view of | t2's reduction only | t1's reduction, t1's pause and t2's reduction |
| INV-070: calendar months January 2025 – October 2026 admitted as the on-treatment period of t1's pause | all 22, among them August 2026 (after the pause) and February 2026 (before t1's first dated event) | January – June 2026 (6) |
| INV-068: months admitted as the pre-treatment baseline of a t1 review view with on-treatment June 2026 | all 22, among them April 2026 (on treatment) | January – December 2025 (12) |

So R28-01 (1) and (2) and R28-02 are confirmed as the review states them.

### Choice between the options

**R28-01, part 1 (INV-103).** The conjunct `startOf(c, e.treatment) ≠ ∅` is removed, as the review requires. OUT-022 conditions on nothing about a known start, and the view is aligned to its event: its periods after the event begin on `firstChangedDay`, which the event's kind and date fix.

**R28-01, part 2 (INV-070): the review's option (b).**
- **Option (a)** (no on-treatment period where the start is not stated) would exclude correct outputs. Every course event is dated on a day by which its course has begun (section 2.8), and a course is taken from that day to its stop or pause. For t1, every day from 15 March to 30 June 2026 is therefore on treatment, and June 2026 is an on-treatment period of the pause that OUT-022 asks to compare with. Option (a) would forbid it. Fix 27's ground ("no period can be placed") holds for the original baseline, but not for the on-treatment period.
- **Option (b)** bounds the first day of the period by the dated course events. It uses one new predicate, `courseBegunBy(c, t, d) ≙ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.date ≤ d` (E-008).
  - **Stated start.** Where the start is stated, `courseBegunBy(c, t, d)` ⇔ `s ≤ d`, because the start is a course event and no course event precedes it (INV-001). So every stated-start verdict is unchanged (397,956 of 397,956 checks in `rand28.out`).
  - **Unstated start.** Where none is stated, the period must begin on or after a dated course event and end before the first changed day.
  - **Cycle ends.** A cycle end dated after the stop never qualifies, because the period ends on or before the stop (or before a reduction, which INV-001 dates on or before the stop).
- **The on-treatment period is also asked for** where the context states no start, the extension that option (b) allows.
  - **Why.** The view is now required for such a course, and OUT-022 asks it to "compare it with both the on-treatment period and the original pre-treatment baseline". Asking for the period exactly where one can be shown keeps fix 02's principle (required = possible, oscillation check 24, Findings B) for every course. The orchestrator's systematic-check rule asks the same: a requirement that does not depend on the start must not be dropped.
  - **Where.** The E-049 `when` clauses stay byte-identical, as the orchestrator and the review require. The ask is a conjunct of INV-070, the SHOULD content invariant of the view, for unstated starts only: `startOf(ctx, v.treatment) = ∅ ∧ courseBegunBy(ctx, v.treatment, plusDays(x, −1)) ⇒ v.onTreatmentPeriod ≠ ∅`.
  - **When it applies.** After every stop or pause, whose own date is the last day of the course, and after a reduction that another dated course event precedes. It never applies where the start is stated, so the watch-point cases (a stop on the start day: asked; a reduction on the start day: not asked) are unchanged.
  - **Why the baseline is not affected.** Fix 27's original-baseline decision is kept: where the original start is not stated, no baseline is asked for or admitted.

**R28-02 (INV-068): the review's main option.** The start conjunct becomes existential: `(∃ s ∈ startOf(ctx, v.treatment) • v.baseline.end < s ∧ ∀ p ∈ ran v.onTreatment • s ≤ p.start)`.
- The treatment review view's baseline is a MUST attribute that must be a pre-treatment baseline (OUT-021, MUST). Where the start is not stated, no period can be placed before it.
- The view is therefore admitted only where INV-102 requires it and INV-056 admits the response comparison of the same treatment.
- The `notStoppedBefore` conjunct is kept (watch point 4).
- The equivalent alternative (a definitional conjunct in E-048) was not taken, because it would add a conjunct where changing one quantifier suffices.

**No Stage 1 issue.** OUT-021 and OUT-022 are clear. The model asks for what can be placed and excludes only what would misstate a baseline or an on-treatment period.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R28-01 | fixed: INV-103 as required; INV-070 by the review's option (b), with the on-treatment period also asked for where the context places one (E-049 `when` clauses byte-identical) | E-008 (Definition, Meaning, Notes); E-049 (Conformance, Notes); INV-070 (Predicate, Reading, Notes); INV-103 (Predicate, Reading, Notes added); INV-097 (Notes); row OUT-022 | **INV-103, Predicate:** `startOf(c, e.treatment) ≠ ∅ ∧` removed. **Reading:** "After each stop, pause or dose reduction of a preventive treatment, whether or not the context states the start of its course, the post-stop monitoring view is available." **New Notes:** OUT-022 "is stopped, paused or reduced" with no condition on the start; what the view asks for without a stated start; satisfiability.<br>**E-008, Definition:** new `pred courseBegunBy(c, t, d) ≙ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.date ≤ d`, with its comment. `startOf`, `resumesFrom`, `originalStart` and `eventOn` are byte-identical. **Meaning:** the predicate and its equivalence to `s ≤ d` for a stated start. **Notes:** new paragraph **Course start not stated**: the days the context places on a course whose start it does not state; the periods tied to the time on treatment that begin on or after a dated course event (INV-070, INV-064, INV-067); the acute summary that covers these days (INV-109); the start-aligned content not shown for such a course (INV-079, E-041, INV-056, INV-068, E-049).<br>**INV-070, Predicate:** `(∀ q ∈ v.onTreatmentPeriod • courseBegunBy(ctx, v.treatment, q.start) ∧ q.end < x) ∧ (startOf(ctx, v.treatment) = ∅ ∧ courseBegunBy(ctx, v.treatment, plusDays(x, −1)) ⇒ v.onTreatmentPeriod ≠ ∅)` replaces `(∀ q ∈ v.onTreatmentPeriod; s ∈ startOf(ctx, v.treatment) • s ≤ q.start ∧ q.end < x)`. The baseline conjunct (fix 27), the after-event conjunct and the values conjunct are unchanged. **Reading:** the on-treatment period begins on or after the start or, where none is stated, on or after a dated course event; when it is shown without a stated start. **Notes:** new paragraph **Course start not stated**; the satisfiability sentence covers the first dated course event and the reduction that no other dated event precedes.<br>**E-049, Conformance:** the view for each event "whether or not the context states the start of the course"; the on-treatment period asked for by the `when` clause where the start is stated and by INV-070 where it is not. **Notes:** the first paragraph (the bound and the existence of the period without a stated start); in **Original start not stated**, the sentence "whose view INV-103 does not require" removed, and the list "the on-treatment period here; INV-055, INV-056, INV-102, INV-103" corrected to "INV-055, INV-056, INV-068, INV-102", as the review asks; new paragraph **Course start not stated** with the review's example (June 2026 admitted; August 2026 and February 2026 not; no on-treatment period for the reduction of 15 March; no baseline).<br>**INV-097, Notes:** the post-stop satisfiability clause (from the first dated course event; no period for a reduction that no other dated event precedes).<br>**Row OUT-022:** the view after every stop, pause or reduction whether or not the start is stated; the on-treatment bound. Elements and Invariants columns unchanged.<br>**Not changed:** E-049's `omn` block (both `when` clauses, `firstChangedDay`), `originalStart`, INV-001, section 2.8 and every other watch-point-4 item. |
| R28-02 | fixed: the review's main option | INV-068 (Predicate, Reading, Notes); E-048 (Conformance, Notes); row OUT-021 | **INV-068, Predicate:** `(∃ s ∈ startOf(ctx, v.treatment) • v.baseline.end < s ∧ ∀ p ∈ ran v.onTreatment • s ≤ p.start)` replaces the `∀ s` form. The `notStoppedBefore` conjunct and the values conjuncts are unchanged. **Reading:** the view of a treatment "whose start the context states"; "No treatment review view is shown for a preventive treatment whose start the context does not state, because no period can be placed before that start." **Notes:** new paragraph **Start not stated**, with the review's example (April 2026 on treatment, presented as the baseline next to June 2026, would hide the treatment effect by which "efficacy can be judged"), and the verdicts unchanged where the start is stated.<br>**E-048, Conformance:** "MUST be available for each preventive treatment whose start the context states (INV-102)", matching INV-102; no view without a stated start (INV-068). **Notes:** the view is shown only where the start is stated, as a response comparison is (INV-056).<br>**Row OUT-021:** the MUST components for each treatment whose start the context states; no view where it states none. Elements and Invariants columns unchanged.<br>**Not changed:** INV-069, INV-102, INV-056. |

## Start-tied bounds check

**Scope.**
- **What was listed.** Every formal occurrence, in the `omn` blocks of v27, of a start-tied bound or condition (`∀ s ∈ startOf(…)`, `startOf(…) ≠ ∅`, `∃ s ∈ startOf(…)`, `originalStart`, `rc.treatmentStart`) and of every other optional-date quantifier on the treatment course or the context: stop dates, anchors, the start and stop dates a line shows, the as-of date, the previous consultation and the chosen period. Found with `occ28.py` (132 `omn` lines), then read item by item.
- **What each row decides, from the Stage 1 text:**
  - **(1) start-dependent:** whether the item's content needs the start, or should be required even where the context does not state it;
  - **(2) vacuous risk:** whether the bound becomes vacuous where the date is not stated and so admits a wrong output, or whether an `∃` makes the item unsatisfiable or not required.

| # | Item | Form (v27) | Start-dependent | Vacuous risk | Change |
|---|---|---|---|---|---|
| 1 | E-008 `startOf` | `{e ∈ courseEvents \| e.treatment = t ∧ e.kind = start • e.date}`, at most one member | — (definition) | — | none |
| 2 | E-008 `originalStart` | first course of the chain, `d ∈ startOf(c, u)`; ∅ where not stated | y (OUT-022 "original") | n: an admission set, read by `∃` (INV-070) | none (fix 27) |
| 3 | E-041 `inPopulation` | `∃ s ∈ startOf(c, t) • ageCovered(c, r.ages, s)` | y: the guidance population is read at the age on the start, and the comparison needs the start (INV-056) | n (∃: no rule applies, E-041 Notes) | none |
| 4 | E-041 `applicable` | `anchorDates(c, t, r.anchor) ≠ ∅` (with `inPopulation`) | y | n | none |
| 5 | E-042 `notStoppedBefore`, `intervalOnTreatment`; E-046 `evaluatedOnTreatment` | `¬ ∃ e • e.kind is stop ∧ e.date < d` | n | n: the context lists every stop (E-008), so no stop stated means not stopped | none (watch point 4) |
| 6 | E-043 `timePoints` (`when`) | `∃ r; a ∈ anchorDates • applicable ∧ intervalOnTreatment` | y | n | none |
| 7 | E-046 `evaluationResult`, `pretreatmentBaseline`; INV-062 | `rc.treatmentStart` (`∈ startOf`, INV-056); `d ∈ r.completionDate` | y | n: a comparison exists only with a stated start | none |
| 8 | E-047 `adherenceFor` | `rc.treatmentStart ≤ a.window.start` | y | n | none |
| 9 | E-049 `baseline` (`when`) | `originalStart(ctx, self.treatment) ≠ ∅` | y | n | none (fix 27) |
| 10 | E-049 `onTreatmentPeriod` (`when`) | `∃ s ∈ startOf; x ∈ firstChangedDay • s < x` | partly: without a stated start, a day on treatment is placed before every stop or pause (its own date) and before a reduction that another dated event precedes | n (∃: not asked); the ask for unstated starts was missing | clause byte-identical (watch point 4; the review; the orchestrator); presence for unstated starts added in INV-070 |
| 11 | E-049 `firstChangedDay` | from the event's kind and date | n | n | none |
| 12 | E-055 `startDate` (`when`) | `startOf ≠ ∅` | y | n | none |
| 13 | E-055 `duration` (`when`) | `startOf ≠ ∅` | y | see row 39 | none |
| 14 | E-055 `preventiveResponse` (`when`) | `role = preventive ∧ startOf ≠ ∅` | y (OUT-018 "aligned to the treatment start date") | n | none |
| 15 | E-055 `adherence` (`when`) | `role = preventive ∧ startOf ≠ ∅` | y (OUT-039 "over the evaluation window, next to the response comparison") | n | none |
| 16 | E-055 `stopDate`, `stopReason`; `stopped` | `∃ e • e.kind is stop` | n | n | none |
| 17 | E-067 `courseOverlaps` (INV-105) | `∃ s ∈ startOf • s ≤ p.end` | y: the preventive treatment effect is a response comparison | n (∃) | none (watch point 8) |
| 18 | E-067 `courseNotOutside` (INV-105) | `∀ s ∈ startOf • s ≤ p.end` | n | vacuous by design: an acute course without a stated start counts as started, and that admits no wrong output (INV-105 Notes) | none (watch point 8) |
| 19 | INV-001 | `∀ e; s ∈ startOf(c, e.treatment) • s ≤ e.date` | y | n: nothing to order without a start | none |
| 20 | INV-001 | `∃ e; s ∈ startOf(c, p.2) • … e.date < s` (`resumes`) | y | n (∃: a resuming course states its start) | none (fix 26) |
| 21 | INV-001 | `≤ c.asOf` bounds; `∀ d ∈ c.previousConsultation`, `∀ r ∈ c.chosenPeriod` | n | n: an absent date has nothing to bound | none |
| 22 | INV-027 | `startOf(c, t) ≠ ∅ ⇒` functional impact next to the comparison | y (the comparison's baseline, OUT-027) | n | none |
| 23 | INV-035, INV-036, INV-104 (markers) | `∀ e ∈ courseEvents • markedKind(e.kind) ∧ …`; `eventOn` | n | n: dose-change and stop markers for every course; a start marker only where stated | none |
| 24 | INV-041 | `mostRecent(v.series, ctx.asOf)` | n | n (the as-of date is always stated) | none |
| 25 | INV-049 to INV-051 | `∀ ws ∈ c.subject.withdrawalStart` | — (each start is a stated date) | n | none |
| 26 | INV-055 | `startOf(c, t) ≠ ∅ ⇒ ∃ comparison` | y | n | none |
| 27 | INV-055 | `∀ r; a ∈ anchorDates; s ∈ startOf • applicable ∧ … ∧ fitsMonthlyPeriod(s, a, r) ⇒ …` | y | n: `applicable` needs a start anyway | none |
| 28 | INV-056 | `rc.treatmentStart ∈ startOf(ctx, rc.treatment)` | y | n (membership: no comparison without a start) | none |
| 29 | INV-058, INV-059 | `anchorDates`, `applicable` | y | n | none |
| 30 | INV-064 | `∀ s ∈ startOf(ctx, L.treatment); p ∈ ran L.evaluated • s ≤ p.start` | n: control levels are absolute months "while on treatment" ([S-010]); a label is optional and may be shown without a comparison | **y**: months before the course admitted (`rand28.out`: 65,746 accepted labels with a month before the first dated course event) | **fixed:** `∀ p ∈ ran L.evaluated • courseBegunBy(ctx, L.treatment, p.start)` |
| 31 | INV-067 | `∀ s ∈ startOf(ctx, a.treatment) • s ≤ a.window.start` | n: adherence to the regimen refers to time on treatment (OUT-039) | **y**: windows before the course admitted (227,096) | **fixed:** `courseBegunBy(ctx, a.treatment, a.window.start)` |
| 32 | INV-068 | `∀ s ∈ startOf • v.baseline.end < s ∧ ∀ p • s ≤ p.start` | y: the pre-treatment baseline needs the start | **y**: any baseline admitted (172,309 views) | **fixed (R28-02):** `∃ s ∈ startOf • …` |
| 33 | INV-068 | `∀ p ∈ ran v.onTreatment • notStoppedBefore(…)` | n | n | none (watch point 4) |
| 34 | INV-070 | `∀ b ∈ v.baseline • ∃ s ∈ originalStart • b.end < s` | y | n (∃) | none (fix 27) |
| 35 | INV-070 | `∀ q; s ∈ startOf • s ≤ q.start ∧ q.end < x` | n for `q.end < x`; the lower bound needs a day of the course | **y**: periods after the stop, or before the course, admitted (440,029 accepted periods outside the days placed on treatment) | **fixed (R28-01):** `courseBegunBy(…, q.start) ∧ q.end < x`, and the presence conjunct of row 10 |
| 36 | INV-071 | `startOf(c, t) ≠ ∅ ⇒` per-phase summaries next to the comparison | y | n | none |
| 37 | INV-078 | `∀ i ∈ dom g.lines • i < #g.lines ⇒ ∀ a ∈ lines(i).startDate; b ∈ lines(i + 1).startDate • a ≤ b` | n: the chronological order of the dated lines (OUT-024 "a chronological list") | **y**: a line without a start date, the line of a course whose start is not stated, between two lines suspends their order (7,880 non-chronological groups admitted) | **fixed:** every pair `i < j` |
| 38 | INV-079 | `∀ s ∈ l.startDate • eventOn(ctx, l.treatment, start, s)` | y | n | none |
| 39 | INV-079 | the duration conjuncts, over `l.startDate` and `l.stopDate` | y: the duration runs from the start | **y**: where the start is not stated no start date can be shown, so any duration is admitted (60,170 lines), although E-055 Notes say a duration exists only for a treatment that has a start | **fixed:** `∀ d ∈ l.duration • startOf(ctx, l.treatment) ≠ ∅` |
| 40 | INV-079 | `∀ e ∈ l.stopDate • ∃ k • eventOn(…, stop(k), e)` | n | n | none |
| 41 | INV-094 | `∀ r ∈ c.chosenPeriod`, `∀ d ∈ c.previousConsultation` | n | n: a summary for each period that the context has | none |
| 42 | INV-102 | `startOf(c, t) ≠ ∅ ⇒ ∃ review view` | y | n | none (consistent with row 32) |
| 43 | INV-103 | `… ∧ startOf(c, e.treatment) ≠ ∅ ∧ (stop ∨ reduction) ⇒ …` | **n**: the view is aligned to the event | requirement dropped for unstated starts (21,948 events now required) | **fixed (R28-01):** conjunct removed |
| 44 | INV-104 | `startOf(ctx, t) ≠ ∅ ⇒ ∃ rc … adherenceFor` | y | n | none |
| 45 | INV-109 | `∀ b ∈ startOf • s.period.start = b ∧ (stopped ⇒ end tie) ∧ (¬ stopped ⇒ end = asOf)` | the start tie y; the end ties **n** | **y**: the end ties were dropped with the start, so any period was admitted as an acute line's response summary (217,374 accepted periods that do not end with the course or leave out a dated course day) | **fixed:** the end ties outside the `∀ b`, and the period begins on or before every dated course event |
| 46 | INV-109 | `∀ e ∈ l.stopDate • s.period.end = e` | n | n | none |

**Outside this class (listed so that every optional date was considered):**
- **Instrument completion dates** (E-046, E-058, INV-062, INV-069, INV-081, INV-082, INV-096, INV-098, INV-104) are dates of results, not of the treatment course, and the context states the date of every available result (INV-082).
- **Cluster-phase dates** and the as-of end of an ongoing phase (E-063, INV-089) are settled (fix 23, watch point 3).

**Result:**
- **Genuine gaps in eight items:**
  - R28-01, in INV-103 and INV-070 (INV-070 also takes the ask that row 10 lacks);
  - R28-02, in INV-068;
  - five that the review did not raise, in INV-064, INV-067, INV-078, INV-079 and INV-109.
- **Every fix leaves the stated-start verdicts unchanged,** with one exception: INV-078 can now also reject a group in which a line with a stated start does not show it (a deviation from the SHOULD of E-055) and the dated lines around it are out of order. That group is not chronological, so rejecting it is correct.
- **Review 28 on INV-064, INV-067 and INV-109.** Review 28 did not raise them, because "a SHOULD invariant already needs a response comparison".
  - **INV-064.** That holds at SHOULD level only (INV-062), while INV-064 itself is definitional and admitted the months. Fix 05 added INV-064's start tie for exactly this reason, because the tie "existed only in INV-062, at SHOULD"; v28 extends that tie to courses whose start is not stated.
  - **INV-067.** The argument does not hold: its wrong windows broke no invariant.
  - **INV-109.** The argument does not hold either, because the acute summary needs no response comparison. Fix 14 left that summary's period unconstrained for a course without a stated start because such a course has "no stated span". The end of the span (the stop date or the as-of date) does not depend on the start, so v28 completes R14-02 for that case, with no verdict changed where the start is stated.
- **No reversal.** None of these changes returns an item to an earlier state. Fix 02's `when` clauses (E-055 `startDate`, `duration`, `preventiveResponse`, `adherence`; E-049) are byte-identical.
- **The other 37 rows** are start-dependent content correctly asked for only with a stated start, or bounds that are not vacuous. They are unchanged.

## Other changes

Bookkeeping only:
- header (v28, iteration 28);
- section 9 ("as of v28");
- section 11 (iteration 28 entry: no web search, no download, no new source);
- section 12 (v28 entry).

The text changes that the class fixes need are listed in the table above and in the v28 change-log entry:
- E-008 Notes, **Course start not stated**;
- E-046 and E-047 Notes;
- E-051 Conformance;
- E-055 Conformance and Notes;
- the Readings and Notes of INV-064, INV-067 (Notes added), INV-078, INV-079 and INV-109;
- rows OUT-020 and OUT-024.

**Items changed (diff v27 → v28, `itemdiff27.py`).**
- **20 content items:**
  - 7 elements:
    - E-008 (Definition, Meaning, Notes);
    - E-046 (Notes), E-047 (Notes);
    - E-048 (Conformance, Notes), E-049 (Conformance, Notes);
    - E-051 (Conformance);
    - E-055 (Conformance, Notes);
  - 9 invariants:
    - INV-064, INV-067, INV-068 and INV-070 (Predicate, Reading, Notes);
    - INV-078, INV-079, INV-103 and INV-109 (Predicate, Reading, Notes);
    - INV-097 (Notes);
  - 4 traceability rows: OUT-020, OUT-021, OUT-022, OUT-024 (coverage reason only).
- **4 bookkeeping items:** the header and sections 9, 11 and 12.
- **Formal blocks:** 9 of 182 `omn` blocks changed (`omndiff27.py`); every other block is byte-identical:

| Block | Change |
|---|---|
| E-008 | +3 lines: `courseBegunBy` and its two-line comment; no line removed |
| INV-064 | the start conjunct → `∀ p ∈ ran L.evaluated • courseBegunBy(ctx, L.treatment, p.start)` |
| INV-067 | `∀ s ∈ startOf(…) • s ≤ a.window.start` → `courseBegunBy(ctx, a.treatment, a.window.start)` |
| INV-068 | `∀ s ∈ startOf(…)` → `∃ s ∈ startOf(…)` |
| INV-070 | the on-treatment conjunct rewritten; one conjunct added (presence where no start is stated) |
| INV-078 | `∀ i ∈ dom g.lines • i < #g.lines ⇒ … (i + 1) …` → `∀ i, j ∈ dom g.lines • i < j ⇒ … j …` |
| INV-079 | one conjunct added: `(∀ d ∈ l.duration • startOf(ctx, l.treatment) ≠ ∅)` |
| INV-103 | `startOf(c, e.treatment) ≠ ∅ ∧` removed |
| INV-109 | the acute summary conjunct restructured: the start tie on its own, a coverage conjunct added, the end ties outside the `∀ b` |

- **Not changed:**
  - no element or invariant added, withdrawn or renumbered;
  - no level, value, axiom, Realises field or level-annotated attribute declaration;
  - no Elements or Invariants column of the traceability table;
  - no source.
  - One declared name was added (`courseBegunBy`).

## Checks

| Check | Result |
|---|---|
| (i) The review's examples (`ex28.out`) | **Example B, t1 without a stated start:**<br>• **INV-103.** v28 requires the views of t1's reduction (15 March), t1's pause (30 June) and t2's reduction (1 October). v27 required only the last.<br>• **INV-070, the view of t1's pause.** Of the 22 calendar months from January 2025 to October 2026, v28 admits April, May and June 2026 as the on-treatment period, and none other; v27 admitted all 22. August 2026 and February 2026 are rejected. A 1-day period on 30 June and 15 March – 11 April are admitted. The view without an on-treatment period is now rejected, because one can be shown and is asked for.<br>• **INV-070, the view of t1's reduction.** No on-treatment period is asked for or admitted (no course event before 15 March); the view with periods after the event only is admitted.<br>• **INV-068.** v28 admits no baseline for a review view of t1; v27 admitted all 22 months, among them April 2026. INV-102 still requires a view of t2 only.<br>• **INV-064.** Control-level months November 2025 – January 2026 are now rejected; April – June 2026 are still admitted.<br>• **INV-067.** An adherence window in November 2025 is now rejected; June 2026 is still admitted.<br>**INV-078.** The group [2022, –, 2020] was admitted by v27 and is rejected by v28. Every ordered group gives the same verdict in both versions.<br>**INV-079.** For an acute course without a stated start, durations of 900 and of 3 days were admitted by v27 and are rejected by v28; a line without a duration is admitted by both.<br>**INV-109.** For the same course (a dose change on 1 March 2025, stopped on 30 June 2026), August 2026 and 30 June alone were admitted by v27 and are rejected by v28. Periods from on or before 1 March 2025 to 30 June 2026 are admitted. |
| (ii) Stated starts behave as in v27 | **Example B with t1 started on 1 January 2026:** every verdict above is the v27 verdict: INV-103 (three views); INV-070 (January – June 2026 for the pause; January and February 2026 for the reduction); INV-068 (12 baseline months, January – December 2025); INV-064; INV-067.<br>**Watch-point examples** (seven cases): a stop on the start day with and without a 1-day period; a reduction on the start day with and without a period before it; a reduction on 1 March before a pause on 30 June; the pause with a June period; the pause with an August period. v27 and v28 agree on INV-001, the on-treatment ask, INV-103 and INV-070 in every case.<br>**Random contexts** (`rand28.out`, 20,000 admissible contexts). Wherever the context states the start, v28 gives the v27 verdict:<br>• 8,108,430 of 8,108,430 post-stop views;<br>• 43,700 of 43,700 on-treatment asks;<br>• 477,528 of 477,528 treatment review views;<br>• 238,764 of 238,764 control-level labels;<br>• 1,322,661 of 1,322,661 adherence windows;<br>• 198,948 of 198,948 treatment lines;<br>• 338,062 of 338,062 acute summaries;<br>• `courseBegunBy` = `s ≤ d` in 397,956 of 397,956 checks.<br>**INV-078** gives the v27 verdict for every group whose lines all show a start date (6,399 of 6,399). All 7,880 differences are groups that v27 admitted with their dated lines out of order. |
| (iii) Satisfiability and the unstated starts | **INV-103.** v28 requires a superset of v27's events in 20,000 of 20,000 contexts, the added events being exactly those of courses without a stated start (21,948).<br>**Required = possible.** The on-treatment period is asked for exactly where the context places a day on treatment before the changed regimen: 21,948 of 21,948 unstated and 43,700 of 43,700 stated events. It is asked for exactly where some on-treatment period is admitted: 65,648 of 65,648.<br>**INV-070 differences.** All 447,053 differences from v27 on unstated starts are rejections of an on-treatment period outside the days the context places on the course, or of a view without one where one is asked for. Every on-treatment period that v28 admits lies within those days (72,158 of 72,158).<br>**Constructions:**<br>• every v28 INV-103 view with every asked SHOULD attribute (baseline where E-049 asks for it, on-treatment period where asked, periods after the event) and a common length meets v28 INV-070 and INV-097: 65,648 of 65,648;<br>• every INV-102 view (baseline 28 days, or the days of a shorter course, before the start, on-treatment from the start) meets v28 INV-068 and INV-097: 39,794 of 39,794;<br>• every acute line has a summary period that meets v28 INV-109 (and v27 where the start is stated): 19,935 of 19,935;<br>• a line without a duration meets v28 INV-079 for every course (29,910 without and 49,737 with a stated start);<br>• lines sorted by their shown start dates meet v28 INV-078: 60,000 of 60,000.<br>**Unstated starts, what v28 still admits:**<br>• INV-068 admits no view (0 of 239,016; v27 admitted 172,309);<br>• INV-079 admits no duration (0; v27 60,170);<br>• every month (10,604), window (256,093) and acute summary period (32,426) that v28 admits begins on or after, or covers, the first dated course event, and every summary period ends with the course.<br>**The invariants that constrain the same views:**<br>• INV-066 with INV-067: a window of a response comparison begins on or after its stated start, so `courseBegunBy` holds;<br>• INV-062 and INV-063 with INV-064: unchanged where the start is stated, and the label is optional;<br>• INV-003, INV-011 and INV-098 add only periods, indicators and annotations, which can always be shown;<br>• INV-001, and so `Ctx`, are byte-identical.<br>**Result.** No MUST or SHOULD combination becomes unsatisfiable, and no attribute is required where it cannot exist. |
| Second seed (`rand28_seed2.out`, 20,000 contexts) | Same conclusions: every stated-start verdict equal; every construction met; INV-068 0 and INV-079 0 for unstated starts. |
| Headings and IDs (`mech27.py`) | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn). No dangling E-, INV-, ISS- or source reference. 37 source IDs cited, all within S-001–S-046 or S-101–S-106. Every OUT reference exists in Stage 1. The output is identical to the v27 run. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields (INV-067 and INV-103 have gained one each). |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Types and names (`names27.py`, `tokcheck27.py`) | 750 declared names, none declared twice: v27's 749 plus `courseBegunBy`.<br>The token report is identical to v27's (106 flagged tokens, each a declared attribute).<br>The new text is well typed:<br>• `courseBegunBy` is a defined predicate with parameters `OutputContext`, `Treatment` and `Date`; `e.date ≤ d` on dates;<br>• `startOf(…) = ∅` on a `set Date`;<br>• `plusDays(x, −1)` as in `intervalOnTreatment`;<br>• `v.onTreatmentPeriod ≠ ∅` on an `opt` attribute;<br>• `∀ i, j ∈ dom g.lines • i < j ⇒ …` as in INV-078's own `∀ g₁, g₂`;<br>• `∀ d ∈ l.duration • startOf(…) ≠ ∅`;<br>• `∀ f ∈ ctx.subject.courseEvents • f.treatment = l.treatment ⇒ s.period.start ≤ f.date`.<br>Brackets are balanced in every block. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34, unchanged. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged, with no typing-rule violation.<br>Each changed invariant keeps its level:<br>• INV-068 MUST (OUT-021);<br>• INV-070 and INV-103 SHOULD (OUT-022);<br>• INV-109 SHOULD and INV-078 SHOULD (OUT-024);<br>• INV-064, INV-067 and INV-079 definitional.<br>The ask added to INV-070 is SHOULD, the level of OUT-022 and of the `when` clause it complements. |
| Diff of formal blocks (`omndiff27.py`, `watch28.py`) | Only the nine blocks of the table above changed.<br>Byte-identical:<br>• section 2.8;<br>• E-041, E-042 (`atTimePoint`, `fitsMonthlyPeriod`, `notStoppedBefore`, `intervalOnTreatment`) and E-043;<br>• the `omn` blocks of E-046 (`evaluatedOnTreatment`), E-047, E-048, E-049 (both `when` clauses, `firstChangedDay`) and E-055;<br>• E-067 and INV-105 (watch point 8);<br>• INV-001, INV-027, INV-035, INV-036, INV-049, INV-055, INV-056, INV-058, INV-059, INV-062, INV-063, INV-066, INV-071, INV-102 and INV-104;<br>• rows OUT-009, OUT-018, OUT-034 and OUT-039.<br>In E-008, `startOf`, `resumesFrom`, `originalStart` and `eventOn` are byte-identical.<br>Term counts v27 → v28 are unchanged for `notStoppedBefore(` 8, `intervalOnTreatment(` 8, `evaluatedOnTreatment(` 6, `firstChangedDay(` 5, `originalStart(` 10, `courseOverlaps(` 6, `courseNotOutside(` 8, `atTimePoint(` 4 and `fitsMonthlyPeriod(` 3. |
| Quotes (`quotes28.py`) | 41 quoted fragments on changed lines: 20 verbatim in Stage 1 v18, among them the new "is stopped, paused or reduced" (OUT-022) and "efficacy can be judged" (OUT-021); 19 already in v27. The 2 fragments flagged "not found" are the text between two separate quotations on one line, not quotes (checked in context). No source quote was added or changed. |
| Scope sweep (`scope27.py`) | Term counts v27 → v28 are equal except four:<br>• "stor" (67 → 68) is the path `history/v27.md`;<br>• "taken" (60 → 63) is "the course is taken from that day to its stop or pause", "a treatment already being taken" (section 11) and "Not taken" (section 12);<br>• "states" and "stated" are "the context states", the model's phrase for a context property.<br>No element is described as entered or recorded. `courseBegunBy` and the changed conjuncts take only context properties (`courseEvents`) and output elements as arguments. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v28.md`: identical. `history/v27.md` is unchanged (equal to HEAD). |
