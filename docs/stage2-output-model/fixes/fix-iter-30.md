# Fix log — iteration 30
Input review: reviews/review-iter-30.md · Input version: v29 · Output version: v30
Date: 2026-10-22

## What was read and checked

**Read:**
- PROCESS.md, in full (scope exclusions of section 2, notation of section 3, fidelity and evidence of section 4, structure of section 6, identifiers of section 7, frozen items of section 10, practical notes of section 11).
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039), in full. I read OUT-024 and its evidence closely:
  - Statement: "a chronological list of preventive (and, separately, acute) treatments with start and stop dates, dose changes, treatment duration, the response summary from OUT-018 or OUT-023 for each treatment";
  - [S-013] "It is not reasonable to test again preventive medications used in the past with no efficacy or with intolerable side effects provided that information on duration, dose and adverse events is sufficient and reliable.";
  - [S-013] "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed."
- v29 (`OUTPUT_MODEL.md`, byte-identical to `history/v29.md`), in full: sections 1–4, every element and invariant of sections 5 and 6, sections 7–10, and the iteration-29 entries of sections 11 and 12. E-008, E-055, E-063, INV-001, INV-079, INV-089 and INV-109 were read closely.
- Review 30 (one remark, R30-01), with its "Checked and not raised" list.
- Earlier decisions on INV-079 and E-055:
  - fix 02: R02-05 (the duration of a treatment that has not stopped runs to the as-of date) and item 14 ("Derived attributes outside the R02-05 pattern": E-063 `duration` and E-058 `changeFromBaseline` accepted as defined in every fully conformant output);
  - fix 17: R17-02 (the formulation conjunct of INV-079) and the day-convention table row on INV-079 and INV-109;
  - fix 25: R25b-01 (one stop per course; the 41- and 89-day example);
  - fix 28: the start-tied-bounds table, rows 12–16 (the E-055 `when` clauses) and row 39 (INV-079: no duration without a stated start);
  - fix 29 (format and checks).
- The oscillation checks after iterations 24 and 28 with their watch points. INV-079 is in watch point 4 of the check after iteration 28: dropping its duration conjunct would be a reversal. E-063 and INV-089 are in watch points 3 and 9 of the check after iteration 24.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**No download and no web search.** The fix adds no new fact, value or source. The one quote added is a Stage 1 quote of OUT-024, checked by script against Stage 1 v18.

**Scripts.** All are in a fresh scratchpad folder, `fix30/` (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix30/`), and were run with `python3 -I`.
- `inv079_30.py` (outputs `inv079_v29only.out`, `inv079_30.out`, `inv079_30_final.out`):
  - It transcribes the date and duration conjuncts of INV-079 as written in v29 and the conjunct added in v30.
  - It first asserts that each transcribed conjunct occurs verbatim in the INV-079 `omn` block of the file it is given.
  - It evaluates the conjuncts on the review's examples, on courses without a stated start, and on every admissible one-course context over seven days. These contexts have every combination of start, stop or pause, dose change, target-dose date and as-of date, under the INV-001 order. Each context is tested with every line: every start date, every stop date, and every duration of 1 to 9 days or none.
  - It compares the duration with the course span of INV-109 in 20,000 random calendar contexts.
- `derived30.py` (outputs `derived30_v29.out`, `derived30_v30.out`) lists every derived attribute with its element, type, level and `when` clause. For each element it also lists the non-derived attributes that an instance may omit (SHOULD, MAY, or a `when` clause), and it lists the components of `SubjectProfile` and `OutputContext`.
- `apply30.py` builds v30 from `history/v29.md` by ten exact replacements, each asserted to occur exactly once. It then appends the change-log entry (`entry30.md`).
- `blockcheck30.py` diffs the INV-079 block line by line and compares the other `omn` blocks. It also counts the protected tie terms of the watch points in the formal text.
- `mech27.py`, `names27.py`, `tokcheck27.py`, `omndiff27.py`, `itemdiff27.py`, `scope27.py` and `quotes27.py` are copies of fix 29's check scripts. I read each one before use. In `quotes27.py` the label "already in v28" reads "already in v29".

### Verification of R30-01

The remark holds (`inv079_v29only.out`, INV-079 as written in v29).

**The review's example A.** A preventive course started on 1 January 2026 and discontinued on 10 February 2026, its last day on treatment; true duration 41 days; as of 21 October 2026. Candidate durations: 1 to 399 days.

| Line shows | v29 admits | v30 admits |
|---|---|---|
| start date and stop date | 1 of 399 (41) | 1 of 399 (41) |
| start date only | 399 of 399, among them 200 | 1 of 399 (41) |
| stop date only | 399 of 399, among them 200 | 1 of 399 (41) |
| neither date | 399 of 399, among them 200 | 1 of 399 (41) |

**Example B.** A course started on 1 January 2026 that has not stopped; 294 days as of 21 October 2026.

| Line shows | v29 admits | v30 admits |
|---|---|---|
| its start date | 1 of 399 (294) | 294 only |
| no start date | 399 of 399, among them 30 | 294 only |

**No other invariant closes the gap.** `l.duration` occurs only in INV-079 (search of every `omn` block). E-055 asks for the start and stop dates at SHOULD only. INV-109 ties the acute summary's span to the course events whatever dates the line shows, so in v29 a line could show "200 days" next to a course summary of 41 days.

**The texts claimed the unconditional relation:**
- the INV-079 Reading: "a duration equal to the days from start to stop or, for a treatment that has not stopped, from start to the as-of date";
- the INV-109 Reading: "the span of the line's duration, INV-079";
- the E-055 Notes and row OUT-024, in the same words.

**Why this is a defect, not a choice.** INV-079 is definitional. Section 3.3 (5) says that a definitional invariant "holds wherever the element is shown" and "excludes only outputs that show a value contradicting the definition of the element". A deviation from the SHOULD of a date does not make a false duration valid. The arguments of the relation are already in the context:
- `startOf` and the one stop or pause of the course (INV-001), or the as-of date;
- INV-079 already uses them (`eventOn`, `ctx.asOf`, `startOf`), and so does INV-109.

So the relation can be stated in every valid output (section 2.7; PROCESS section 2: a relation whose arguments are output elements or context properties already used as such).

### Choice between the review's options

**Option (a) taken: the duration is tied to the course whatever the line shows.** The new conjunct is the review's formula, with explicit definedness guards in the form of the existing duration conjuncts (`s ≤ e.date ∧ …`, `s ≤ ctx.asOf ∧ …`; section 2.6):

`(∀ d ∈ l.duration; s ∈ startOf(ctx, l.treatment) • (∀ e ∈ ctx.subject.courseEvents • e.treatment = l.treatment ∧ e.kind is stop ⇒ s ≤ e.date ∧ d = daysLong(days(s, e.date))) ∧ (¬ stopped(ctx, l.treatment) ⇒ s ≤ ctx.asOf ∧ d = daysLong(days(s, ctx.asOf))))`

**Why option (a), on the evidence:**
1. **It excludes exactly the wrong durations.** In the enumeration, every line that v29 admits and v30 rejects shows a duration other than the true one. The true duration is admitted with every combination of shown dates (1,483 of 1,483 contexts with a stated start).
2. **Option (b) is not definitional.** Option (b) admits a duration only together with the dates it rests on. It would therefore reject a line that shows a correct duration without its dates, a value that contradicts nothing. That turns the SHOULD dates of E-055 into a condition for showing the duration, and section 3.3 (5) says a definitional invariant "cannot make an element more or less required".
   - Stated at SHOULD level instead, option (b) would leave the value unconstrained in every MUST-conformant output that omits a date, which is the defect itself.
   - OUT-024 lists "start and stop dates, dose changes, treatment duration" as parts of one SHOULD statement, and PROCESS section 4 keeps each part at its own strength; option (b) would make one part depend on another.
3. **Stage 1 makes the value matter.** OUT-024 rests the dates, dose changes and duration on [S-013]: "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed." A wrong duration presents an inadequate trial as adequate, or the reverse (R25b-01, fix 25). This quote is now cited in the INV-079 Evidence.
4. **The review prefers it**, and it is the smaller change: one conjunct, with no change to E-055's `omn` block.

**The quantifier over `startOf` is not vacuous.** The new conjunct is universal over `startOf(ctx, l.treatment)`. Fix 28's conjunct `(∀ d ∈ l.duration • startOf(ctx, l.treatment) ≠ ∅)`, which is kept, excludes a duration where the context states no start. So wherever a duration is shown, `startOf` has exactly one member (INV-001), and the new conjunct fixes the value.

**Definedness.** `days(s, e.date)` and `days(s, ctx.asOf)` are guarded in the formula. INV-001 also ensures both guards in every admissible context: no course event precedes the start, every course event lies on or before the as-of date, and the start is a course event.

**Watch points kept** (oscillation check after iteration 28):
- **Watch point 4.** Every v29 conjunct of INV-079 is kept verbatim, including fix 28's duration conjunct. The change is a pure insertion of three lines (`blockcheck30.out`).
- **Day convention.** No course-event date changed. Section 2.8, E-008 and INV-001 are byte-identical.
- **Other watch-point items.** `courseBegunBy`, the INV-078 order, the INV-109 predicate (its end ties and its start tie), the E-055 `when` clauses of fix 02, and the E-049, INV-064, INV-067, INV-068, INV-070 and INV-103 blocks are byte-identical.
- **Watch point 1 (start-aligned against event-aligned content).** The duration was already classified as start-dependent (fix 28 row 13). It stays so: the new conjunct reads the start, and it takes no side on the post-stop view.
- **Direction.** The change only narrows what INV-079 admits (v30 admits a subset of the v29 lines), so it reverses no fix.

### Derived-attribute sweep (the same defect nearby)

**Question.** For every derived attribute: does its relation hold only where its arguments are shown in the same item, while the true value is determined by output elements or context properties that every valid output has? `derived30_v29.out` lists 33 derived attributes. "Omissible" means that the argument may be absent while the value is shown.

| # | Derived attribute | Relation | Arguments omissible? | Context counterpart of the omissible arguments | Same gap? |
|---|---|---|---|---|---|
| 1 | E-005 `lengthDays` | INV-002 | no (`start`, `end` MUST) | — | no |
| 2 | E-013 `expressions` | INV-012 | no (period length MUST); a proportion shown without covered days rests on a number obtained from diary information | none | no |
| 3–4 | E-014 `days`, E-019 `count` | INV-005, INV-006, INV-030, INV-031 (bounds and one value per view) | no | — | no (values obtained from diary information) |
| 5 | E-023 `summary` | INV-032: the levels lie on the scale, and the counts lie within the headache days shown | yes: `scale` (SHOULD), the headache days of the view | none: the scale is a presentation choice of the output, and the days are values obtained from diary information | no |
| 6–8 | E-024 `value`, E-025 `presence`, E-031 `impact` | INV-033 (bounds by the period length, always shown; attacks with a symptom by the attack count of the view) | the attack count only | none (diary information) | no |
| 9–11 | E-032 `code`, `referenceLevel`, `status` | INV-045, INV-046 | no (`scope` core, `basis` and `span` MUST) | — | no |
| 12 | E-033 `value` | none (its formula is computed from diary information, out of scope) | — | — | no |
| 13 | E-039 `reviewWindow` | INV-051 | no (`withdrawalStart` core) | — | no |
| 14–15 | E-040 `absolute`, `relative` | INV-053 | no (`reference`, `compared` core) | — | no |
| 16–17 | E-042 `earliest`, `latest` | INV-058 | no (`anchorDate` MUST, tied to the context by INV-058) | — | no |
| 18 | E-047 `adherence` | none (obtained from diary information) | — | — | no |
| 19 | E-051 `treatedAttacks` | INV-072, INV-074 (the number of attack lines) | yes: `sequence` (SHOULD) | none (the attacks are diary information) | no |
| 20–22 | E-052 `attacksWithOutcome`, `attacksAssessed`, `proportion` | INV-074 | no (core counts) | — | no |
| **23** | **E-055 `duration`** | **INV-079** | **yes: `startDate`, `stopDate` (SHOULD)** | **yes: `startOf`, the stop or pause course event, `ctx.asOf`** | **yes: R30-01, fixed** |
| 24 | E-058 `totalScore` | INV-082 (range) | — | — | no (obtained from diary information) |
| 25–26 | E-058 `category`, `changeFromBaseline` | INV-082 | yes: the total scores (SHOULD) | none: the context states the instrument and date of each available result, not its score | no; fix 02 item 14 decided this, and review 30 did not raise it |
| 27 | E-060 `completeCycles` | INV-087 | no (`cycles` core) | — | no |
| 28–30 | E-060 `firstDayOfMenstruation`, `perimenstrualWindow`, `nextWindowDays` | INV-087 | no (`cycle`, `dayOneShown`, `complete` core; `menstruationDays` MUST) | — | no |
| 31 | E-061 `inPerimenstrualWindow` | INV-087 | no (`onset` core; its cycle line is in the view) | — | no |
| 32 | E-063 `duration` | INV-089 | yes: `start` (SHOULD), `end` (SHOULD when not ongoing) | none: `SubjectProfile` and `OutputContext` have no component for cluster periods or remission periods, whose dates are obtained from diary information; only the as-of end of an ongoing period is a context property, and the start is still needed | no; fix 02 item 14; watch points 3 and 9 of the check after iteration 24 (E-063 and INV-089 were aligned in v23); review 30 did not raise it |
| 33 | E-064 `rate` | INV-089 (the attack count of the same view) | the attack count may be absent | none (diary information) | no |

**Result.**
- E-055 `duration` is the only derived attribute whose omissible arguments have counterparts in the context, and so the only one for which the relation can be stated in every valid output.
- The other derived attributes either take arguments that every instance shows, or take values obtained from diary information. For these, section 2.7 gives the relation only over shown output elements, because the context does not hold them and a relation to them would be a derivation from input.
- No other item was changed. E-063 and INV-089 are left as they are. Their text was aligned in v23, and changing it again on this ground would be the cycling of watch point 9 of the check after iteration 24. Review 30 brings no new evidence on them.
- The E-055 `duration` comment ("to the stop date or, if not stopped, to the as-of date") was not changed. It states the definition that the predicate now enforces, so the E-055 `omn` block stays byte-identical.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R30-01 | fixed: the review's option (a) | INV-079 (Predicate, Reading, Evidence, Notes); E-055 (Notes); INV-109 (Reading); row OUT-024 | **INV-079, Predicate.** New conjunct after fix 28's duration conjunct (formula above): where the context states the start, a duration shown is the number of days from the start to the one stop or pause of the course or, for a treatment that has not stopped, to the as-of date. Every v29 conjunct is kept verbatim.<br>**INV-079, Reading.** "a duration equal to the days from start to stop or, for a treatment that has not stopped, from start to the as-of date of the output (its duration to date) and no duration …" → "a duration equal to the days from the start of the course to its stop or, for a treatment that has not stopped, from its start to the as-of date of the output (its duration to date), whether or not the line shows its start and stop dates, and no duration …".<br>**INV-079, Evidence.** Adds the Stage 1 quote of OUT-024: "for the duration of the course, [S-013] "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed."".<br>**INV-079, Notes.** New paragraph **Duration and the course**:<br>• the line may omit its SHOULD dates, so the duration is tied to the course;<br>• the review's two examples (41 days; 294 days);<br>• with the dates shown, the shown-date conjuncts give the same value (`eventOn`);<br>• the arguments are course events and the as-of date, as in INV-109;<br>• `days` is defined (INV-001);<br>• the dates themselves are not required (section 3.3, item 5).<br>**E-055, Notes (Relations).** "duration agrees with the start and the stop date, or with the start and the as-of date …, and is not shown for a treatment whose start the context does not state" → "duration equal to the days from the start of the course to its stop or, for a treatment that has not stopped, to the as-of date, whether or not the line shows its start and stop dates, and so agreeing with the dates it shows; no duration for a treatment whose start the context does not state".<br>**INV-109, Reading.** "…, to the as-of date, the span of the line's duration, INV-079)" → "…, to the as-of date; where the context states the start, this is the span whose days the line's duration counts, whatever dates the line shows, INV-079)". The INV-109 predicate is byte-identical. Its Notes ("where the treatment has a start, … the span of the line's duration (INV-079)") are now exact and were not changed.<br>**Row OUT-024.** "duration (to the stop, or to date for a treatment that has not stopped)" → "duration (from the start of the course to its stop, or to date for a treatment that has not stopped, whatever dates the line shows)". The Elements and Invariants columns are unchanged.<br>**Justification:**<br>• the remark is verified (the tables above);<br>• option (a) is chosen on the evidence of the section above;<br>• levels: INV-079 stays definitional (E-055), and no conformance level, `when` clause or Realises field changed;<br>• no watch-point item is reversed. |

## Other changes

**Bookkeeping:**
- header: "Version: v30 · Iteration: 30 · Status: under review";
- section 9: "(as of v30)";
- section 11: an iteration-30 entry (no web search, no download, no new source; the scripts and examples; the one Stage 1 quote added);
- section 12: the v30 entry (date 2026-10-22).

**Items changed (diff v29 → v30, `itemdiff27.py`): 8.**
- **4 content items:**
  - E-055 (Notes);
  - INV-079 (Predicate, Reading, Evidence, Notes);
  - INV-109 (Reading);
  - row OUT-024 (coverage reason).
- **4 bookkeeping items:** the header and sections 9, 11 and 12.
- **Formal blocks:** 1 of 182 changed (INV-079, three lines inserted).
- **Not changed:**
  - no element or invariant added, withdrawn or renumbered;
  - no Definition, Meaning, Conformance or Realises field;
  - no heading, no traceability column other than the coverage reason of OUT-024;
  - no source, value, axiom, level or `when` clause.
- `git diff --stat` of OUTPUT_MODEL.md: 21 insertions, 8 deletions.

## Checks

| Check | Result |
|---|---|
| (i) The review's examples (`inv079_30.out`) | **Example A** (start 1 January 2026, discontinued 10 February 2026, as of 21 October 2026):<br>• v29 admits 399 of 399 durations for a line without its start date, its stop date or both (200 days included), and 1 (41) with both dates;<br>• v30 admits 41 days only in all four cases.<br>**Example B** (start 1 January 2026, not stopped):<br>• a line without its start date: v29 admits 399 of 399 (30 included), v30 only 294;<br>• with its start date: both admit only 294. |
| (ii) Lines that show both dates (`inv079_30.out`) | 2,064 admissible one-course contexts and 1,320,960 lines.<br>• Every line that shows every date its duration rests on (its start date, and its stop date where the course has stopped) has the v29 verdict: 1,052,030 of 1,052,030.<br>• v30 admits a subset of the v29 lines, and every line it rejects shows a duration other than the true one.<br>• No v30-admitted line shows a wrong duration, or a duration for a course without a stated start (0 and 0). |
| (iii) No required line becomes unsatisfiable (`inv079_30.out`) | • The fully conformant line (a start date and the duration where the start is stated, a stop date where the course has stopped) is admitted in 2,064 of 2,064 contexts, among them ongoing courses and courses without a stated start.<br>• The true duration is admitted with every combination of shown dates: 1,483 of 1,483 contexts with a stated start.<br>• Courses without a stated start (the script's examples C and D: reduced 15 March 2026, and paused 30 June 2026 or not stopped) admit the line without a duration and no duration, in v29 and in v30, as fix 28 set it. |
| Satisfiability pass (INV-079, INV-109, E-055 and the invariants that require lines) | • **INV-079.** Above. `l.duration` occurs in no other predicate (search of every `omn` block).<br>• **INV-109.** The predicate is unchanged. In 20,000 random calendar contexts with a stated start, the only duration that v30 admits for a line without dates equals the number of days of the course span of INV-109, from the start to the stop or the as-of date (20,000 of 20,000). So the new Reading's "the span whose days the line's duration counts" holds, and INV-109 and INV-079 are satisfied together.<br>• **E-055.** The `when` clauses are unchanged. The SHOULD of `duration` (where the start is stated) is met by the true value, which v30 admits in every context.<br>• **Lines required elsewhere.** INV-077 and INV-104 require lines and INV-078 orders them by start date. These are unchanged, and a line can always show the true duration or none, so they are satisfiable as in v29. |
| Headings and IDs (`mech27.py`) | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn). No dangling E-, INV-, ISS- or source reference; 37 source IDs cited, all within S-001–S-046 or S-101–S-106. Every OUT reference exists in Stage 1. The output is identical to the run on v29. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full", covering all 39 Stage 1 requirements. The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. Only the coverage reason of row OUT-024 changed. |
| Types and names (`names27.py`, `tokcheck27.py`) | • 750 declared names, none declared twice; no new name.<br>• The token report is identical for v29 and v30: 106 flagged tokens, each a declared attribute.<br>• The new conjunct is well typed:<br>&nbsp;&nbsp;– `d` ranges over `l.duration : opt Duration`, and `s` over `startOf(…) : set Date`;<br>&nbsp;&nbsp;– `e` ranges over `ctx.subject.courseEvents : set CourseEvent`;<br>&nbsp;&nbsp;– `e.kind is stop` uses the tag of `CourseEventKind`;<br>&nbsp;&nbsp;– `days : Date × Date ⇸ ℕ₁` is guarded by `s ≤ …`;<br>&nbsp;&nbsp;– `daysLong : ℕ → Duration`;<br>&nbsp;&nbsp;– `stopped` is the predicate of E-055.<br>• Brackets are balanced. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34, unchanged. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`, and every invariant states its scope. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged, with no typing-rule violation. INV-079 stays definitional (E-055), the level of the relation of a derived attribute (section 3.3, item 5). |
| Diff of formal blocks (`omndiff27.py`, `blockcheck30.py`) | 182 `omn` blocks in v29 and in v30.<br>• Only the INV-079 block differs: one insertion of three lines directly after fix 28's duration conjunct, with every v29 line kept in order.<br>• The SHA-256 of the other 181 blocks, in order, is equal.<br>• Byte-identical, among others: E-008, E-055, E-063, INV-001, INV-064, INV-067, INV-068, INV-070, INV-078, INV-089, INV-103, INV-109 and section 2.8.<br>• Formal counts of the protected ties, v29 → v30, unchanged: `notStoppedBefore(` 6, `intervalOnTreatment(` 6, `evaluatedOnTreatment(` 4, `firstChangedDay(` 4, `courseBegunBy(` 6, `originalStart(` 4, `resumesFrom(` 3, `courseOverlaps(` 4, `courseNotOutside(` 4, `summarisesMedication(` 11, `sameSpan(` 30, `sameIndicatedPeriod(` 7, `onlyOfType(` 6, `next(p.end)` 3, `eventOn(` 7, `∃ s ∈ startOf(` 4, `∀ s ∈ startOf(` 1, and fix 28's `∀ d ∈ l.duration • startOf(ctx, l.treatment) ≠ ∅` 1.<br>• The counts that grow are those of the new conjunct: `startOf(` 23 → 24, `stopped(` 6 → 7, `e.kind is stop` 7 → 8, `daysLong(days(` 3 → 5. |
| Quotes (`quotes27.py`) | 4 quoted fragments on changed lines, all verbatim in Stage 1 v18 (OUT-024 statement and evidence): "start and stop dates, dose changes, treatment duration", the OUT-024 formulation sentence, the [S-012] triptan-refractoriness fragment, and the new [S-013] "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed." No source quote was changed. |
| Scope sweep (`scope27.py`) | Term counts v29 → v30 are equal except six, each read in context:<br>• "stor" (69 → 70): `history/v29.md` in the iteration-30 search-log entry;<br>• "obtained" and "diary information" (+1 each): "values obtained from diary information" in the change-log entry, the model's own exclusion phrase of section 2.7;<br>• "taken" (+1): "Not taken.";<br>• "states" and "stated": "the context states the start".<br>The new text has no input, storage or input-derivation content. Every relation added takes only output elements and context properties already used as relation arguments. |
| Snapshot and files | `cmp OUTPUT_MODEL.md history/v30.md`: identical. `history/v29.md` and everything under `docs/stage1-output-requirements/` are unchanged (equal to HEAD). Only `OUTPUT_MODEL.md`, `history/v30.md` and this log were written. |
