# Fix log — iteration 26
Input review: reviews/review-iter-26.md · Input version: v25 · Output version: v26
Date: 2026-10-22

## What was read and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039). OUT-022, OUT-018, OUT-021, OUT-023, OUT-024, OUT-027, OUT-035, OUT-009 and OUT-039 and their evidence were read closely. The key wordings:
  - OUT-022: "compare it with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible";
  - [S-011]: "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal.";
  - [S-022]: "to detect possible rebound phenomena (i.e. frequency of migraine days per month going above its baseline)";
  - OUT-018: "in a pre-treatment baseline period with periods after treatment start, aligned to the treatment start date";
- v25 (`OUTPUT_MODEL.md`, byte-identical to `history/v25.md`), sections 1–12;
- review 26 (one remark, R26-01).

**Earlier loop files read, so that no fix is undone:**
- fix 25, with the decision "one stop or pause per course; a restart is a new course" (option (a) of R25b-01), and review 25b (R25b-01);
- the oscillation check after iteration 24, with its ten watch points, in particular:
  - watch point 4: the course-event dates, `atTimePoint`, `fitsMonthlyPeriod`, `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, `firstChangedDay` and the E-049 `when` clause;
  - watch point 8: INV-105 and E-067, responder labels, E-041;
- review 02 ("Aligned to the treatment start date": the baseline need not be the month directly before the start; not raised);
- review 15 ("Several stop events in one course"; not raised) and fix 15 (the INV-070 row: "the position of the original baseline (settled in review 02)");
- fix 11 (context-restriction table: "a restart is a new course").

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. No earlier fixer declined a remark on the baseline of a resumed course.

**No download and no web search.** Every quoted fragment of the new text is verbatim in Stage 1 v18 (`quotes26.py`).

**Scripts.** All are in the session scratchpad, folder `fix26/` (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix26/`), and were run with `python3 -I`:
- `chain26.py` (output in `chain26.out`) evaluates these items in their v25 and v26 forms:
  - INV-001 (course-event conjuncts, and in v26 the `resumes` conjuncts);
  - `startOf`, and in v26 `resumesFrom` and `originalStart`;
  - INV-070, the E-049 `when` clause, `firstChangedDay`, INV-103 and the INV-097 post-stop conjunct;
  - for the watch-point examples, `notStoppedBefore`, `intervalOnTreatment` and the INV-055 time points.

  It runs them on the review's example, on chains of two and three courses, on a chain whose first course has no stated start, on ten kinds of malformed link, on the earlier watch-point examples and on 30,000 random contexts.
- `mech26.py` and `names26.py` are copies of the fix-24 scripts `mech24.py` and `names24.py`, read before use. `tokcheck.py` confirms that every name `names26.py` flags is a declared attribute.
- `omndiff.py` and `quotes26.py` are copies of the fix-25 scripts, read before use. `itemdiff.py` gives the item-level diff, and `scope26.py` the scope sweep.

### Verification of the remark

**R26-01 holds.** `chain26.py` ran the review's example with the predicates as written in v25. The example:
- course t1 of drug X starts on 1 January 2026 and has `stop(paused)` on 30 June 2026;
- course t2 of the same drug starts on 1 September 2026 and has `doseChange(reduction)` on 1 October 2026;
- the as-of date is 21 October 2026.

The results:
- INV-001 admits the context.
- INV-103 requires post-stop views for t1's pause and for t2's reduction.
- For the view of t2's reduction, INV-070 admits each of these baselines:
  - August 2026, in the interval off treatment;
  - June 2026, the last month of t1 on treatment;
  - December 2025.

The bound is `b.end < s` for `s ∈ startOf(ctx, t2) = {1 September 2026}`. So v25 accepts a month of the pause, and even a month on treatment, as "the original pre-treatment baseline".

### Choice between the review's options

**Option (a): a context link `resumes` from a resumed course to the course it resumes, and an original start defined over the chain.** Chosen, on these grounds:
1. **A resumption is a property of the course that dates and stop kinds cannot decide.**
   - A later course of the same drug may resume the treatment after a pause or a discontinuation trial (Stage 1 OUT-022: [S-011]; and [S-023] and [S-030], the discontinuation trial).
   - Or it may be the drug tried again as a new treatment, whose original baseline is its own.
   - Option (b) would have to choose among these from the existing context: "a course of the same drug that starts after a course ending with `stop(paused)`", "for example the first that starts after the pause". That reading has three problems:
     - It would be the first relation of the model that distinguishes `paused` from `discontinued`. Fix 25 established, and checked by script, that every relation treats the two kinds alike (`e.kind is stop`), because a pause that is later made definitive keeps the kind the context states.
     - It would miss a resumption after a discontinuation trial.
     - It would link a new trial years later.
2. **The link is a context property like the others.** It is stated as Stage 1 states the situation ("restarting the treatment", OUT-022), like `preventiveFor` and `preventiveTypes`, and how it becomes known is outside the model. It is not described as entered or recorded, and it takes no input data as argument.
3. **Size.**
   - One component of `SubjectProfile`.
   - Two defined names (`resumesFrom`, `originalStart`).
   - Two INV-001 conjuncts.
   - One token in INV-070 (`startOf` → `originalStart`).

   Option (b) would need the same original-start function plus a defined reading of the context.

**Option (a) neither narrows nor broadens Stage 1.**
- **The link is optional, and the conjuncts reject only malformed links.**
  - A context without links (`resumes = ∅`) is admissible exactly when it is admissible in v25.
  - The new INV-001 conjuncts exclude only links that do not describe a later course of the same drug resuming a preventive course after its stop or pause.
- **Courses that resume no course behave exactly as in v25.** For such a course, `originalStart(c, t) = startOf(c, t)`, so INV-070 is the v25 predicate. This covers every course of a treatment that was never resumed, and the first course of a chain.
- **For a course that resumes another, INV-070 only excludes baselines.** The excluded baselines end on or after the original start of the treatment, that is, after the treatment was first started. OUT-022's "original" excludes them.
- **INV-070 keeps its level.** It stays SHOULD, the strength of OUT-022.
- **Nothing else changes level or content.** No other invariant's level or content changes.

**Section 8.** No issue was recorded. The review asks for one only if Stage 1 leaves open whether the "original" baseline of a resumed treatment is the one before its first course. It does not:
- OUT-022 concerns a treatment that "is stopped, paused or reduced". Its evidence restarts "the treatment" after a pause ([S-011]).
- It qualifies the baseline as "original", which the response comparison of OUT-018 and the treatment review view of OUT-021 do not do ("pre-treatment baseline").
- Its rebound is "above its baseline" ([S-022]).

So the baseline of OUT-022 is the one from before the treatment was first started. It is not the time before a restart, which by [S-011] is the time in which migraine worsened after the withdrawal.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R26-01 | fixed: the review's option (a) | E-008 (Definition, Meaning, Evidence, Notes); INV-001 (Predicate, Reading, Notes); INV-070 (Predicate, Reading, Evidence, Notes); E-049 (Definition comment of `baseline`, Meaning, Conformance, Notes); row OUT-022 (coverage reason) | **E-008, Definition:**<br>• new component `resumes : set (Treatment × Treatment)`: (t₁, t₂) when the preventive course t₂ resumes the treatment of the course t₁ after the stop or pause of t₁;<br>• new `pred resumesFrom(c, u, t) ≙ ∃ s : seq1 Treatment • first(s) = u ∧ last(s) = t ∧ ∀ i ∈ dom s • i < #s ⇒ (s(i), s(i + 1)) ∈ c.subject.resumes`: t is u, or t resumes the treatment of u, directly or through intermediate courses;<br>• new `fun originalStart(c, t) : set Date`: the earliest start that the context states for t or a course that t resumes. This is the start of the first course of the chain, or, where the context states no start for that course, the earliest start it states in the chain. It has at most one member, and it is never after `startOf(c, t)`, so the INV-070 bound is never weaker than in v25.<br>**E-008, text:**<br>• Meaning: the history bullet adds `resumes`, and the OUT-022 paragraph adds the original start and `resumesFrom`;<br>• Evidence: the OUT-022 statement fragment and the [S-022] fragment;<br>• Notes, new paragraph **Resumed courses**: the link and its INV-001 constraints; the original start; what keeps its own course's start; a new trial is not linked; a link may follow a stop stated either way; the time frame.<br>**INV-001, new conjuncts:**<br>• `∀ p ∈ c.subject.resumes • p.1 ∈ preventiveTreatments ∧ p.2 ∈ preventiveTreatments ∧ drugOf(p.1) = drugOf(p.2) ∧ ∃ e ∈ courseEvents; s ∈ startOf(c, p.2) • e.treatment = p.1 ∧ e.kind is stop ∧ e.date < s`;<br>• `∀ p, q ∈ c.subject.resumes • p.1 = q.1 ∨ p.2 = q.2 ⇒ p = q`.<br>These are the review's conjuncts. Because no course event precedes a start and the stop of the resumed course is dated before the restart, a chain of resumptions is in chronological order, finite (at most as many courses as the subject has preventive courses) and without cycles. With at most one predecessor and one successor per course, the courses that a course resumes form one chain with a unique first course.<br>**INV-001, text:** the Reading states the conjuncts. In the Notes, "its pre-treatment baseline may still be the original one" is now split: the response comparison and the treatment review view keep a baseline before their own start, which may be the original one (OUT-018 and OUT-021 say "pre-treatment baseline"); post-stop monitoring compares with the original baseline (INV-070). New paragraph **Resumed courses**: well-foundedness, the scope of the link, and that a context without links is admissible as in v25.<br>**INV-070, Predicate:** `(∀ b ∈ v.baseline; s ∈ originalStart(ctx, v.treatment) • b.end < s)` replaces `s ∈ startOf(ctx, v.treatment)`. Nothing else in the predicate changed: the on-treatment period still begins on or after the start of the event's own course and ends before `firstChangedDay`, and the periods after the event begin on `firstChangedDay`.<br>**INV-070, text:**<br>• Reading: the original pre-treatment baseline ends before the treatment was first started;<br>• Evidence: the OUT-022 statement fragment, [S-011] and [S-022];<br>• Notes, new paragraph **Original baseline**, and the satisfiability sentence: the baseline is a period of the common length ending on the day before the original start, which exists for any length.<br>**E-049:**<br>• the `baseline` comment;<br>• Meaning: the original baseline;<br>• Conformance: the baseline ends before the original start;<br>• Notes, new paragraph **Resumed treatment**: the review's example (December 2025 admitted, August 2026 not), and why the on-treatment period stays within the event's course.<br>**Row OUT-022:** the restart sentence now states the link, the original baseline before the first course of the chain, and that the course's own comparison and review view keep a baseline before its own start. The Elements and Invariants columns are unchanged.<br>**Not changed:**<br>• E-049 `onTreatmentPeriod` and its `when` clause, `firstChangedDay`, and the on-treatment and after-event conjuncts of INV-070 (watch point 4; see the consequences check);<br>• INV-103, INV-097 and INV-056;<br>• INV-068 (the review: "need no change");<br>• section 2.8 (its sentence "A treatment resumed after a stop or pause is a new course, with its own start (E-008)" stays true). |

## Consequences of "restart = new course"

Every place where the model refers to the pre-treatment baseline, the original baseline, the treatment start, the treatment history, adherence over the evaluation window, the treatment duration or markers was checked. The candidates were found by a per-item term count:

| Term | Occurrences in v25 (before section 11) |
|---|---|
| "pre-treatment baseline" | 22 |
| "original" | 8 |
| "treatment start" | 63 |
| "treatment history" | 18 |
| "evaluation window" | 29 |
| "duration" | 141 |
| "marker" | 37 |
| "restart" | 13 |
| "resum" | 4 |

For each item, the decision follows the Stage 1 wording:
- **Course:** the start or period of the item's own course.
- **Chain:** the chain of resumed courses.

| # | Item | Stage 1 wording | Course or chain | Change |
|---|---|---|---|---|
| 1 | E-049 `baseline`; INV-070 baseline conjunct | OUT-022: "compare it with both the on-treatment period and the original pre-treatment baseline"; [S-022] "going above its baseline" | **chain**: before the treatment was first started (`originalStart`) | **y** (R26-01) |
| 2 | E-049 `onTreatmentPeriod` and its `when` clause; INV-070 on-treatment conjunct | OUT-022: "the on-treatment period" (not qualified as "original"); "continue to show" | course of the event: the period on treatment that the stop, pause or reduction ends | n. A chain reading would change the `when` clause for a reduction on a resumed course's start day, which watch point 4 freezes (fix 17, fix 02 item 5). It would also admit an on-treatment period separated from the event by an interval off treatment. |
| 3 | E-049 `after`; INV-070 after conjunct; `firstChangedDay` | OUT-022: "continue to show headache and migraine frequency" | course of the event (from its first changed day) | n. Stage 1 names no end. The periods after a pause may reach past a restart, which the restart's start marker (INV-035) and the resumed course's own views show; requiring an end would be a new tie with no Stage 1 wording. |
| 4 | INV-103 | OUT-022: "After a preventive treatment is stopped, paused or reduced" | course events: each stop, pause or reduction of each course | n. t1's pause and t2's reduction each have their view. |
| 5 | E-043, INV-056 (baseline before `treatmentStart`; on-treatment periods after it) | OUT-018: "in a pre-treatment baseline period with periods after treatment start, aligned to the treatment start date" | course (admits the original baseline too, since it ends before every later start) | n (the review: "need no change") |
| 6 | E-041 `inPopulation`, `anchorDates`; E-042; INV-055, INV-058, INV-059 (time points; age on the start) | OUT-018: "at the evaluation time points named in current guidance"; [S-015] "3 to 6 months after starting prophylactic treatment" | course: a restarted treatment has the time points of its own start (fix 25) | n (watch points 4 and 8) |
| 7 | E-048, INV-068, INV-102 | OUT-021: "for the same pre-treatment baseline and on-treatment periods" | course | n (the review: "need no change") |
| 8 | E-051, INV-071 (summaries per preventive phase) | OUT-023: "separately for the pre-treatment baseline period and for the on-treatment periods of that preventive treatment" | course: the periods of that treatment's response comparison | n |
| 9 | INV-027 | OUT-027: "allow comparison with the baseline period" | course: the response comparison's baseline | n |
| 10 | E-046 `pretreatmentBaseline`, `evaluationResult`, `evaluatedOnTreatment`; INV-062, INV-063, INV-064 | OUT-020 (criteria on the response to the treatment; [S-010] "while on treatment"); OUT-018 | course: the label's own response comparison and course | n (watch point 8) |
| 11 | E-047 `adherenceFor`; INV-066, INV-067; E-055 `adherence`; INV-104, INV-109 adherence | OUT-039: "over the evaluation window, next to the response comparison of OUT-018" | course: a window of that course's comparison, beginning on or after its start | n |
| 12 | E-054, E-055, INV-077, INV-078, INV-079, INV-109 (lines, start and stop dates, duration, response summary) | OUT-024: "a chronological list of preventive (and, separately, acute) treatments with start and stop dates, dose changes, treatment duration" | course: each course is a line with one start, one stop and one duration (fix 25) | n. OUT-024 does not ask for the link to be shown; the resumed course is the next line of the same class group. |
| 13 | E-034, E-035, INV-035, INV-036, INV-104 markers | OUT-009: "dated markers for the start, dose change and stop of preventive treatments" | course events: a restart is the start marker of the new course | n |
| 14 | E-067 `courseOverlaps`, `courseNotOutside`; INV-105 | OUT-035: "treatment effect", "so that patients can follow the effect of their treatment" | course: the treatment taken during the period | n (watch point 8). During an interval off treatment no course is taken. |
| 15 | INV-097, INV-098 | OUT-036 (c) and Caveat | applies to whatever periods a view shows | n: satisfiable with the original baseline (Checks) |
| 16 | E-008, INV-001 (the restart reading of fix 25) | OUT-022 "stopped, paused or reduced"; [S-011] "restarting the treatment" | introduces the chain (`resumes`, `resumesFrom`, `originalStart`) | **y** (R26-01) |
| 17 | Row OUT-022 | OUT-022 | chain for the baseline; course otherwise | **y** |
| 18 | Rows OUT-009, OUT-018, OUT-021, OUT-024, OUT-039 | as in items 5–13 | course | n (byte-identical, `itemdiff.py`) |
| 19 | Section 2.8 (day convention) | — | course-event dates | n (watch point 4; byte-identical) |

**Result.** One genuine gap (items 1, 16 and 17, that is, R26-01). Every other reference keeps its course, as the Stage 1 wording requires. No further change was made.

## Other changes

None besides the bookkeeping:
- header (v26, iteration 26);
- section 9 ("as of v26");
- section 11 (iteration 26 entry: no web search, no download, no new source);
- section 12 (v26 entry).

**Items changed (diff v25 → v26, `itemdiff.py`).**
- **5 content items:**
  - 2 elements: E-008 (Definition, Meaning, Evidence, Notes) and E-049 (Definition comment, Meaning, Conformance, Notes);
  - 2 invariants: INV-001 (Predicate, Reading, Notes) and INV-070 (Predicate, Reading, Evidence, Notes);
  - row OUT-022.
- **Bookkeeping:** the header and sections 9, 11 and 12.
- **Formal blocks:** 4 of 182 `omn` blocks changed (`omndiff.py`); every other block is byte-identical:

| Block | Change |
|---|---|
| E-008 | +11 lines: the `resumes` component (2 lines), `resumesFrom` and `originalStart` with their comments (9 lines) |
| INV-001 | +3 lines (two conjuncts) |
| INV-070 | 1 line edited (`startOf` → `originalStart`) |
| E-049 | 1 comment edited (no formal change) |

- **Not changed:**
  - no element or invariant added, withdrawn or renumbered;
  - no level, value, axiom or level-annotated attribute declaration;
  - no Realises field;
  - no Elements or Invariants column of the traceability table;
  - no source added.

## Checks

| Check | Result |
|---|---|
| The review's example (i) | **v25:** INV-001 admits the context; INV-070 admits August 2026, June 2026 and December 2025 as the baseline of the view of t2's reduction.<br>**v26 with (t1, t2) ∈ `resumes`:** INV-001 admits the context, and `originalStart(t2) = {1 January 2026}`. INV-070 rejects August 2026 (the pause) and June 2026 (on t1), and accepts December 2025.<br>**Further cases:**<br>• The view of t1's own pause is unchanged.<br>• If t2 also stops on 15 October, its stop view likewise rejects August 2026 and accepts December 2025.<br>• Chain a → b → k (starts 1 March 2025, 1 December 2025, 1 September 2026): `originalStart(k) = {1 March 2025}`. February 2025 is accepted. October 2025, a pause month of a, is rejected (v25 accepted it).<br>• A chain whose first course has no stated start: `originalStart` is the earliest stated start, never after the course's own start.<br>• Without the link (the drug tried again as a new treatment), v26 gives the v25 verdicts. |
| INV-001 v26 on links | Rejects all ten malformed kinds:<br>• different drug;<br>• acute course;<br>• resumed course without a stop;<br>• restart before the stop;<br>• restart on the stop day;<br>• resuming course without a start;<br>• self link;<br>• two successors;<br>• two predecessors;<br>• a two-course cycle.<br>Admits a chain of three, and a restart after a stop stated as a discontinuation. |
| A treatment never resumed behaves as in v25 (ii) | 30,000 random contexts (three courses, 0–1 stops, dose changes, random drugs; half with links), with 6 random post-stop views per INV-103 event:<br>• INV-001 v26 equals v25 on every context without links (15,000 of 15,000).<br>• INV-070 gives the v25 verdict on every view of a context without links (266,682 of 266,682).<br>• It also gives the v25 verdict on every view of a course that resumes no course in a linked context (18,792 of 18,792).<br>• For a course that resumes another: 6,218 of 7,122 views keep their verdict. The 904 others are admitted by v25 and rejected by v26, each with a baseline that ends on or after the original start. None is admitted by v26 and rejected by v25.<br>• `originalStart` has at most one member and is not after `startOf` (48,861 of 48,861 courses), and it equals `startOf` for every course that resumes none (47,840 of 47,840).<br>• Every linked admitted context is acyclic (878 of 878). |
| Watch-point examples (iii) | Unchanged from v25 (fix 17, fix 18, fix 25, check 24):<br>• Review-18 antibody (start 1 January 2026):<br>  – stopped on 10 February: no time point;<br>  – stopped on 30 March: NICE CG150 1.3.28 and Turkish Box 8;<br>  – stopped on 31 March: all six;<br>  – uninterrupted: 1 April ×4, 26 March and 1 March.<br>• Stop on the start day: the on-treatment period is required, and a 1-day period with a December 2025 baseline is admitted by v25 and v26.<br>• Reduction on the start day: no on-treatment period is required, and the view is admitted by both versions.<br>• Reduction 1 March, then pause 30 June: both views; the reduction view is admitted by both versions.<br>• A dose change after a stop: rejected by v25 and v26.<br>• NICE 1.3.29 with a stop on the last day of cycle 2: admitted; `intervalOnTreatment` holds.<br>• Fix-25 restart example, now with the link: t1 has no time point; t2 has 1 July, 24 July and 1 August ×4, as in fix 25; `originalStart(t2) = {1 January 2026}`.<br>• E-042 and INV-049 dates: 26 March; 28 days; day 43; 7 April – 5 May. |
| Satisfiability pass | **INV-001.** Satisfiable: every v25 context with `resumes = ∅`, and every linked context above. The new conjuncts constrain only `resumes`.<br>**`resumesFrom`, `originalStart`.** Total. `originalStart` is finite with at most one member: its members are start dates of a finite chain of courses, and the minimum of a set of dates is unique.<br>**INV-070 with E-049, INV-103 and INV-097.** For every INV-103 event of 20,000 random linked contexts, the following post-stop view was built, with L = 28, or for a required on-treatment period the smaller of 28 and the days on treatment before the changed regimen:<br>  – a baseline of L days ending on the day before the original start;<br>  – an on-treatment period of L days ending on the day before `firstChangedDay`, where the E-049 `when` clause requires it;<br>  – an after period of L days from `firstChangedDay`.<br>Each such view meets INV-070 (v26), the `when` clause and the equal lengths of INV-097: 6,215 of 6,215.<br>**INV-003, INV-011, INV-006.** The baseline is a period atom of the view, a completeness indicator can be added for it, and one value per measure, period and scope can be shown.<br>**INV-098.** An earlier baseline may begin in childhood, and the view then needs the supportive-information annotation, which can always be added.<br>**INV-056, INV-068, INV-055.** Unchanged, and they do not read `resumes`.<br>**Result.** No MUST or SHOULD combination of the invariants that constrain the post-stop view or the context becomes unsatisfiable, and no derived attribute is required where its relation is undefined. |
| Headings and IDs (`mech26.py`) | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn). No dangling E-, INV- or ISS- reference. 37 source IDs cited, all within S-001–S-046 or S-101–S-106; the one newly cited is the Stage 1 source S-022, by its Stage 1 quote. Every OUT reference exists in Stage 1. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Types and names (`names26.py`, `tokcheck.py`) | 749 declared names, none declared twice: v25's 746 plus `resumes`, `resumesFrom` and `originalStart`. Every name that the token report flags is a declared attribute, and the report differs from v25 only by `resumes`.<br>The new text is well typed:<br>• `p.1`, `p.2` on pairs (section 2.4);<br>• `(s(i), s(i + 1)) ∈ c.subject.resumes`, with `s(i + 1)` guarded by `i < #s`, as in `consecutive`;<br>• `first`, `last` on `seq1`;<br>• `∃ s : seq1 Treatment` as in INV-001's `∃ s : seq1 DateSpan`;<br>• `e is stop` on a variant tag;<br>• `<` and `≤` on dates;<br>• `{d : Date \| φ}` as a finite set.<br>Brackets are balanced. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34, unchanged. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged, with no typing-rule violation. `resumes` is a component of a value type, with no level. INV-070 stays SHOULD (OUT-022), and INV-001 stays definitional (context scope). |
| Diff of formal blocks (`omndiff.py`, `itemdiff.py`) | Only the E-008, INV-001, INV-070 and E-049 `omn` blocks changed (E-049 in a comment only).<br>Byte-identical:<br>• the watch-point-4 items: section 2.8, `atTimePoint`, `fitsMonthlyPeriod`, `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, `firstChangedDay`, the E-049 `when` clause;<br>• INV-105 and E-067 (`courseOverlaps`, `courseNotOutside`);<br>• INV-079 and INV-109;<br>• E-041 and its values;<br>• E-046 and the responder-label invariants INV-062 to INV-064;<br>• INV-055, INV-056, INV-058, INV-059, INV-066 to INV-068, INV-071, INV-097, INV-103 and INV-104;<br>• the rows OUT-009, OUT-018, OUT-021, OUT-024 and OUT-039.<br>Fix 25 is kept: at most one stop per course, and a restart is a new course. |
| Quotes (`quotes26.py`) | 24 quoted fragments on changed lines. All are verbatim in Stage 1 v18 or already in v25, among them:<br>• the OUT-022 statement fragment;<br>• the [S-011] quote;<br>• the [S-022] fragment;<br>• "aligned to the treatment start date" and "pre-treatment baseline".<br>None is unmatched, and no source quote was added or changed. |
| Scope sweep (`scope26.py`) | Term counts v25 → v26 for record, enter, entry, input, captur, logged, stor, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, questionnaire, data-entry, "derived from", "diary information", intake, "decision logic", taken and took are all equal except two:<br>• "stor" (63 → 66) is "history" ("the subject's history", "history/v25.md");<br>• "taken" (56 → 57) is "was not taken" (option (b), section 12).<br>The link is a context property ("the context also states which earlier course the new course resumes"). How it becomes known is outside the model, and no element is described as entered or recorded. The new conjuncts and functions take only context properties as arguments. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v26.md`: identical. `history/v25.md` is unchanged (equal to HEAD). |
