# RATIONALE audit — part 3 (lines 1404–1798), model v40
Date: 2026-10-23
FINDINGS: 5 (CONTRADICTION 1, OVERCLAIM 2, STALE 2, WRONG-REFERENCE 0)
Entries audited: 70 — D 44, S 14, W 2, X 1, N 0, and the non-quote prose of Q 9

## Method

- **Scope.** `RATIONALE.md` (v39, companion of `OUTPUT_MODEL.md` v40), section 2.4, from `### 2.4 Invariants` (line 1404) to the end of INV-062/S02 (line 1797), the last entry before `#### INV-114/D01`. That is the generic invariants INV-118 to INV-125, then INV-001 to INV-062 in model order. Quotes were not re-verified against their sources.
- **Read in full:** PROCESS.md; `OUTPUT_MODEL.md` v40 (sections 1 to 12, including section 2 notation, section 3 conformance and R-MCF, the section 4 catalogue and case tables, and all elements, invariants, issues and source-data tables); `RATIONALE.md` section 1 and the range; review 41; the oscillation check after iteration 40.
- **Read for settled points:** the "Checked and not raised" lists of reviews 36 to 41; the fix logs of 35, 35-equivalence and 36 to 40; the oscillation check after iteration 36; `restructure/equivalence-v35.md`; and the passages of `restructure/plan-v35.md` and fix 32 that a candidate finding touched. Every review and fix log was searched by script for every entry ID in the range.
- **Origins.** Each candidate was traced in `history/v12.md`, `v24.md`, `v26.md`, `v31.md`, `v34.md` and `v35-rationale.md`, to tell a sentence that a later fix made false (STALE) from one that was never true of the formal text.
- **Checks.** For every statement that an entry makes about the model (what an item says, permits or forbids, its level, how items relate, which item holds a rule, reasons stated as facts about the model), I read the formal text the statement concerns. Where a statement could be enumerated, I checked it by script. Scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/ra3/`, run with `python3 -I`:
  - `dates.py` uses the section 2.8 library (`plusDays`, `plusMonths`, `days`, `shift`) and the 18 SD-ER rows. It checks:
    - the length of the INV-045 span, for every monthly period from 2020 to 2029;
    - the spans of February 2026 as a calendar month and as a 28-day period;
    - the dates of INV-049/W01 and INV-055/W01;
    - which rules can have a time point earlier than 28 days after the start (INV-055/D02);
    - the earliest start of every window (INV-055/S01).
  - `preds.py` encodes the predicates it needs literally from the model. It checks:
    - INV-012 rounding: whether the covered days that a shown proportion admits are consecutive, and whether pairwise agreement implies one common number;
    - INV-119 with bearer `Element`, with and without the annotation disjunct of `presents`;
    - INV-123 `factsShown`/`stated` on the basis count of an overuse indicator;
    - the three INV-111 conjuncts on a three-view output;
    - INV-003 with INV-115 on a composite index for migraine;
    - the INV-001 `resumes` conjuncts, over 3 same-drug courses on a small date grid.
- **R41-01.** INV-076/D01 is the subject of R41-01. It is at line 1953, in part 4, outside this range, and is not re-reported here. I looked for the same misreading in this range: claims that an output item is not related to a headache type, or that relating it would be a derivation from input. The entries that speak of type scopes are INV-118/D04, INV-055/D01, INV-062/Q00, D02 and D03, INV-122/D01 and D02, and the "values of one type scope" of INV-123/D01. All of them agree with E-012 (`allTypes`, `ofType`, `onlyOfType`, `scopeFor`), with INV-062 and with INV-118. None makes the R41-01 claim.

## Findings

### RA-3-01 STALE: INV-123/D01 puts the basis of a medication-overuse indicator outside the class of INV-123, which has contained it since v35 (CHG-05)
- Entry: `RATIONALE.md` INV-123/D01, attribute table, row "other derived counts" (line 1482). The same table's row "E-014 (E-029)" (line 1479) is also involved.
- Entry text:
  - "| other derived counts (treated attacks of a summary, **the basis of an overuse indicator**, cycle-line menstruation days, values of one type scope) | values obtained from diary information | not in the class; a count of 0 for a medication, type or treatment that did not occur is a correct value |"
  - Three rows above: "| E-014 (E-029) acute-medication day count above 0 | use of medication of the count's scope | INV-123 (`usedScope`; v35, CHG-05) |"
- Model text:
  - E-001 `factsShown`: `{f : ShownFact | ∃ m ∈ {x} ∩ DayCount; s : MedicationScope • m.measure = acuteMedicationDays(s) ∧ m.days > 0 ∧ f = usedScope(s)}`.
  - E-032: `basis : seq1 →DayCount  MUST   -- the acute-medication days of the scope, one for each period of the span`.
  - INV-045: `i.basis(j).measure = acuteMedicationDays(basisScope(i.scope))`.
  - INV-123: `∀ x : Element; f ∈ factsShown(x) • stated(ctx, f)`.
  - E-008 `stated`: `(∀ s : MedicationScope • f = usedScope(s) ⇒ ∃ m ∈ c.subject.acuteMedications • inMedicationScope(m, s))`.
- Why they conflict:
  - **The basis counts are in the class.** Every basis count of an indicator is a `DayCount` whose measure is `acuteMedicationDays(…)` (INV-045). Above 0 it shows `usedScope` of its scope, and INV-123 ties that fact to the context. So "the basis of an overuse indicator … not in the class" is false of v40.
  - **Script (`preds.py`).** A class indicator for triptans with a basis count of 3 days, for a subject whose only acute medication is ibuprofen, gives `factsShown` = {usedScope(ofClass(triptans))} with `stated` false. INV-123 excludes it. A combined-use basis count of 12 days for a subject without acute medication is excluded the same way.
  - **CHG-05 exists for this tie.**
    - Fix 35, CA-03: "INV-046 unchanged; its guarantees (INV-046/S01) now hold".
    - `restructure/equivalence-v35.md`: "the 8.2.6 single-class guarantee now holds, because class indicators rest on DayCount bases".
    - The plan, row INV-046: "S01 (true after CHG-05)".
    - In this same range, INV-046/S01 ("For a subject without acute medication, or with medication of one class of 8.2.6 only, the combined indicator that INV-044 requires is shown as 'not reached'") holds only because basis counts above 0 are tied. INV-123/D07 states the tie for every acute-medication day count.
  - **The entry contradicts itself.** Its own row "E-014 (E-029)" puts every acute-medication day count above 0 in the class. The basis counts are such counts.
  - **History.** Fix 32's table listed "acute-medication days of a drug or class, the treated attacks of a summary, the basis of an overuse indicator, …" as derived counts outside the class, which was true in v34. The v35 update moved positive acute-medication day counts into the class (the new row). It left the basis, which consists of those same counts, in the out-of-class row.
  - **New evidence against the earlier checks.**
    - Review 36 noted in general terms that "the attribute table of INV-123/D01 matches the members".
    - The check after iteration 36 restated the row ("treated attacks, overuse basis, cycle-line menstruation days and values of one type scope out"). Its watch point 3 lists "overuse basis" among counts "not in the class".
    - Neither compared the row with the `usedScope` member and INV-045. That comparison, together with CA-03's dependence on it, is the new evidence.
- Correction:
  - In the row "other derived counts", delete "the basis of an overuse indicator, ".
  - In the row "E-014 (E-029)", add after "acute-medication day count above 0": "(among them the basis counts of a medication-overuse indicator, E-032, INV-045, on which INV-046/S01 rests)".
  - This changes no formal text and does not widen the class: these counts have been members since v35. For the next oscillation check: the words "overuse basis" in watch point 3 of the check after iteration 36 come from this stale row. Correcting the row is not a redraw of the class boundary.

### RA-3-02 OVERCLAIM: INV-001/D03 says the `resumes` conjuncts exclude only links that are not resumptions; the uniqueness conjunct also excludes sets of genuine resumptions
- Entry: `RATIONALE.md` INV-001/D03 (line 1540).
- Entry text: "A context that states no link (`resumes = ∅`) is admissible whenever it is admissible without the component, so the conjuncts exclude only links that are not resumptions of a stopped or paused course by a later course of the same drug."
- Model text:
  - INV-001: `(∀ p ∈ c.subject.resumes • p.1 ∈ c.subject.preventiveTreatments ∧ p.2 ∈ c.subject.preventiveTreatments ∧ drugOf(p.1) = drugOf(p.2) ∧ ∃ e ∈ c.subject.courseEvents; s ∈ startOf(c, p.2) • e.treatment = p.1 ∧ e.kind is stop ∧ e.date < s) ∧ (∀ p, q ∈ c.subject.resumes • p.1 = q.1 ∨ p.2 = q.2 ⇒ p = q)`.
  - Reading: "each course resumes at most one course and is resumed by at most one".
- Why they conflict:
  - The second conjunct excludes sets of links in which every link is a resumption of a stopped or paused course by a later course of the same drug: a course that two courses resume, or a course that resumes two.
  - Script (`preds.py`): 396 such link sets on a small grid of three same-drug courses. Example: t1 and t2 stopped on day 2, t3 started on day 3, `resumes = {(t1, t3), (t2, t3)}`. Each link meets the first conjunct, and the set fails the second.
  - The entry states this uniqueness two sentences earlier ("Because each course resumes at most one course and is resumed by at most one, …"), so its "only" contradicts its own text.
  - The sentence was written by fix 26 together with the uniqueness conjunct (fix 26 calls the excluded links "malformed"). No review has examined it. The defect is minor.
- Correction: "… so the conjuncts exclude only links that are not resumptions of a stopped or paused course by a later course of the same drug, and sets of links in which a course resumes, or is resumed by, more than one course."

### RA-3-03 CONTRADICTION: INV-003/D01 says the referenced values of a composite index are not placed in its view; for a composite index for migraine, INV-003 with INV-115 places them there
- Entry: `RATIONALE.md` INV-003/D01, paragraph "Periods of referenced values" (line 1545).
- Entry text: "A change, a residual burden and a composite index refer to per-period values, not to periods (`referencedValues`, E-011), so the conjunct on `refs(x) ∩ Period` does not place the periods of these values in the item's view, and the values themselves may be shown in another view of the output (rule W1; E-040 `reference`, `compared` (W2) places them in the view only for the changes of a response comparison)."
- Model text:
  - E-033: `element CompositeIndex extends PeriodValue`, and E-012: `period : →Period  core`.
  - INV-115 (definitional): `∀ x : CompositeIndex • concerns(ctx, x.typeScope, c1) ⇒ ∀ m ∈ x.components • m.period = x.period ∧ m.typeScope = x.typeScope`.
  - INV-003 (MUST): `∀ v : View • … ∀ x ∈ v.content • refs(x) ∩ Period ⊆ v.content ∧ …`. Its Notes: "if two items x and y refer to the same period atom p, then viewOf(x) = viewOf(p) = viewOf(y)".
  - Section 4.2: "INV-003 also places in one view every two items that refer to the same period atom … and so places in the view of their holder, for example, … the components of a composite index for migraine (INV-115)".
- Why they conflict:
  - For a composite index for migraine, the period of every component is the index's own period atom.
  - That atom is in `refs(x) ∩ Period`, so INV-003 places it in the index's view. That contradicts "does not place the periods of these values in the item's view".
  - Each component refers to that atom, so INV-003 places the component in the same view. That contradicts "the values themselves may be shown in another view of the output".
  - Script (`preds.py`): an index in view V with `x.period = P`, P in V, and a component with `m.period = P` placed in view W. INV-003 fails in W. With the component moved to V, it holds.
  - Review 38 checked the section 4.2 example ("the INV-115 components") and found it true, so the model's prose and the entry say opposite things.
  - **History.** The sentence dates from v12. The period tie was then a SHOULD conjunct of INV-092 (`m ∈ viewOf(x).content ∧ m.period = x.period`). Fix 31 moved it, as INV-115, to definitional level. Since v31 the sentence is false of every output that meets INV-003, and since v37 section 4.2 states the opposite. No review or fix has examined the sentence.
- Correction: append to the sentence: "; the components of a composite index for migraine are the exception: they refer to the index's own period atom (INV-115), so INV-003 places them, with that period, in the index's view (INV-003 Notes; section 4.2)". No formal change.

### RA-3-04 OVERCLAIM: INV-003/D02 says that combined-use indications of periods with the same dates agree; INV-046 ties them only for the same dates and the same kind
- Entry: `RATIONALE.md` INV-003/D02 (line 1550).
- Entry text: "So these values that one view shows for periods with the same dates agree: counts (INV-006), completeness (INV-012), the combined medication-overuse indication (INV-046) and cluster attack rates (INV-089); other values, for example two intensity summaries, are not tied by any invariant."
- Model text:
  - INV-046, last conjunct: `(∀ i₂ : MedicationOveruseIndicator • sameIndicatedPeriod(i₂, i) ∧ i₂.scope = combinedUse ⇒ i₂.status = i.status)`.
  - E-032: `pred sameIndicatedPeriod(i₂, i) ≙ i₂ ∈ viewOf(i).content ∧ sameSpan(i₂.period, spanOf(i.period)) ∧ i₂.period.kind = i.period.kind`.
- Why they conflict:
  - INV-046 ties the combined-use indications of periods with the same dates and the same kind.
  - Periods with the same dates and different kinds exist. INV-006/D01 names them: "a calendar month and a 28-day period with the same dates (February of a common year)".
  - Their indicators have spans with different dates. `dates.py`: for February 2026 the calendar-month span is 1 Nov 2025 to 28 Feb 2026, and the 28-day span is 9 Nov 2025 to 28 Feb 2026. So the two indicators rest on different basis days, and INV-046 leaves their indications free to differ.
  - INV-046/D01 states exactly this: "the kind is part of the match because a calendar month and a 28-day period with the same dates have spans with different dates".
  - Counts, completeness and rates are tied by dates alone (`sameSpan`), so the rest of the list is right.
  - **New evidence.** Review 38 listed "INV-003/D02 (the agreeing values)" as checked. It did not consider the kind conjunct of `sameIndicatedPeriod` or INV-046/D01, which are the new evidence here. The defect is minor.
- Correction: replace "the combined medication-overuse indication (INV-046)" with "the combined medication-overuse indication for periods with the same dates and kind (INV-046; INV-046/D01)".

### RA-3-05 STALE: INV-111/D01 says the invariant excludes only outputs whose labels contradict the values they label; its third conjunct (v35) excludes more
- Entry: `RATIONALE.md` INV-111/D01 (line 1575, moved v34 Notes).
- Entry text: "A second label of the view naming another definition, or a label naming another definition than that of the view whose values a change, a residual burden or a composite index refers to, would state a definition that the values do not follow. So the invariant is definitional: it excludes only outputs whose labels contradict the values they label."
- Model text:
  - INV-111, third conjunct: `(∀ v : View; x ∈ v.content; m₁, m₂ ∈ referencedValues(x); lm : LabelledMeasure • isMeasure(m₁, lm) ∧ isMeasure(m₂, lm) ⇒ ∀ l₁ ∈ viewOf(m₁).content ∩ DefinitionLabel; l₂ ∈ viewOf(m₂).content ∩ DefinitionLabel • l₁.measure = lm ∧ l₂.measure = lm ⇒ l₁.definition = l₂.definition)`.
  - Reading: "The values that one change, residual burden or composite index refers to come from views that, where both state a definition for the measure, state the same one."
- Why they conflict:
  - The third conjunct excludes outputs in which every label states the definition that its own view's values follow.
  - Example: a change in view V, which shows no migraine-day label, refers to a value in view A (label d1) and a value in view B (label d2).
  - Script (`preds.py`) on that output: every label names the definition of its view's values (true); conjunct 1 true; conjunct 2 true; conjunct 3 false.
  - The entry is v34 text, and v34 INV-111 had only the first two conjuncts, for which the sentence was true. v35 added the third conjunct (CHG-06, CA-07, INV-111/D02: "A change between values under two definitions is not a change of one measure"). That made the "only" false.
  - Section 1 of `RATIONALE.md` asks that "a sentence that an intended change of meaning of v35 made false is qualified". This one was not.
  - No review or fix has examined it. Watch point 8 of the check after iteration 40 names only INV-075/D01, INV-085/D01 and INV-110/S01.
- Correction: "So the invariant is definitional: it excludes only outputs whose labels contradict the values they label, and, by its third conjunct (v35, INV-111/D02), outputs in which one change, residual burden or composite index refers to values whose views state different definitions for the measure."

## Checked and consistent

**Generic invariants**
- **INV-118/D03:**
  - `reportedTogether(c, {K}, sc)` equals `reportedPerPeriod`, checked against both definitions in section 3.4.
  - The conditions inside `ppRequired` of C1-02, C1-04, C1-06, C1-09 and C1-14 are as stated.
  - C1-11's series has granularity `calendarWeek`, through `tiles`, and so its view is a `WeeklyMedicationView` (E-036).
  - The C1-13 qualification matches section 9. The entry is settled in review 41.
- **INV-118/D04:**
  - The granularities and kinds of C1-01, C1-04, C1-06, C1-07, C1-10 and C1-14 are as stated.
  - `byTypeCases` has no SHOULD case.
  - The second conjunct has its own ∃ g, separate per case.
  - INV-122 is per view.
  - The monotonicity from C1-13 to v38 is settled in review 39.
- **INV-119/D04:** `preds.py` gives 0 differing verdicts over 32 outputs for the bearer `Element`. The C2-08 annotations are bearers by E-010 `qualifies` (W2) and the one-view rule. Settled in review 36.
- **INV-120/D03:** `ctx(outputOf(…))` equals `ctx` in output scope (sections 2.9 and 4.4).
- **INV-121/D01:** `daysWithin` has 5 members, one per replaced v34 conjunct (v34 INV-005, INV-012, INV-032 and INV-033). The pain-time conjunct is verbatim (compared with `history/v34.md`).
- **INV-122/Q01 (prose):** consistent.
- **INV-122/D01:** consistent; the moved reference to INV-125 (SD-DF-01) is correct.
- **INV-122/D02:** `nestedIn` has 7 disjuncts: the 4 bounds of v34 INV-024 with the same ranges, the 2 of v34 INV-031 and the 1 of v34 INV-033. The last two conjuncts are verbatim v34 INV-030.
- **INV-123/Q01 (prose):** consistent.
- **INV-123/D01, every row except RA-3-01:** each "Tie in v35" checked against the members of `factsShown`, the `stated` clauses, INV-058, INV-067, INV-068, INV-079, INV-080, INV-082, INV-089 and INV-112. The header's "a rule" as an entity of the context is loose wording, and the row itself says "a rule of the list"; not raised.
- **INV-123/D03:** `stoppedCourse` ⇒ `stopped`, and course events lie on or before the as-of date (INV-001). E-055 `stopReason` is SHOULD `when stopped`.
- **INV-123/D04:** `usedMedication((l.drug, {fo}))`. INV-001 gives every acute treatment an acute medication of its drug.
- **INV-123/D05:** `availableResult` holds without a completion date. Every result asked by INV-062, INV-069, INV-081, INV-096 and INV-104 can be an available one.
- **INV-123/D07:** checked against v34 INV-056, INV-068 and INV-079.
  - The `startOf` and `eventOn` memberships hold.
  - The `AcuteMedication` value equality holds.
  - v34's role conjuncts were biconditionals (⇔), and they equal v35's role facts under INV-001's disjointness.
  - The CHG-R1 and CHG-05 statements are true.
- **INV-124/D01:** consistent with the first conjunct and `shownDayOnes`, and with the cluster conjuncts over start and `lastDay`. The stated exception is settled in review 36.
- **INV-125/D01:** consistent with SD-DF and its levels.

**Contexts and frame (INV-001 to INV-006)**
- **INV-001/Q00 (prose):** consistent.
- **INV-001/D01:** the as-of bounds of the compared spans, the consultation, the chosen period and the withdrawal starts are as stated, and scheme windows are unbounded (settled in review 40). No course event precedes a start.
- **INV-001/D02:**
  - At most one stop per course.
  - Dose changes and the reached target dose lie on or before the stop; cycle ends are not bounded by it.
  - INV-112 gives no baseline without `originalStart`.
  - `intervalOnTreatment` holds for NICE 1.3.29 with a stop on the last day of cycle 2.
- **INV-001/D03, apart from RA-3-02:**
  - `preds.py` finds no cycle in 3,469 admissible `resumes` sets.
  - The chain is unique, `originalStart` has at most one member, and the population argument through `applicable` holds.
- **INV-003/S01:** consistent with INV-002 and the second conjunct of INV-011.
- **INV-006/D01:** INV-006 compares by `sameSpan` and ignores the kind. The relations listed are per view.
- **INV-006/S01:** consistent, read as "one count per measure, scope and dates".

**Definition labels and completeness (INV-008 to INV-012)**
- **INV-008/S01:** consistent. It was rewritten in v35 for the third conjunct of INV-111.
- **INV-111/D02:** without the third conjunct, INV-008 is unmeetable in the view of a change across two definitions (follows from the second conjunct).
- **INV-111/S01:** consistent.
- **INV-011/D01:**
  - The response summaries of a treatment history view bring their periods and indicators: acute summaries are per-period values (first conjunct).
  - A comparison's values share its period atoms, and its changes are placed by E-040 W2 MUST (second conjunct).
- **INV-011/S01:** consistent.
- **INV-012/D01:** `preds.py`: 1,581 admitted sets for lengths 1 to 31 and 0 to 2 decimals, all consecutive; no pairwise-agreeing triple without a common number.
- **INV-012/S01:** consistent. It does not name the `allTypes` conjunct, which INV-011/S01 states; not raised.

**Frequency, severity and comparisons (INV-027 to INV-039)**
- **INV-027/D01:** settled in review 41.
- **INV-027/S01:** consistent with the INV-122 nesting by domain.
- **INV-031/Q00 (prose):** consistent.
- **INV-031/D01:**
  - No migraine-day ≤ headache-day relation exists.
  - The relation to E-018 holds only under `labelledAs` with `ihs2025MigraineDay`.
  - E-018 is not related to moderate/severe headache days.
  - The mark of a period ties migraine days of periods with the same dates.
- **INV-031/X01:** INV-104 asks for the marks of the covered period and of the series periods with 0 migraine days at SHOULD. "A mark implies 0" stays.
- **INV-035/D01:** `markers` (W2 SHOULD); the values of the series come in through `perPeriod`, and their periods through INV-003.
- **INV-039/Q00 (prose):** consistent.
- **INV-039/D01:** consistent with the antecedent of INV-039 and the first conjunct of INV-097.
- **INV-039/D02:** `onSameScale` with `i₁` is transitive, so the summaries share a scale and form with each other.
- **INV-039/S01:** consistent.

**Medication overuse and withdrawal (INV-045 to INV-050)**
- **INV-045/D01:** `dates.py`: the span has 4 periods for every calendar month and every 28-day period from 2020 to 2029. Settled in reviews 37 to 39.
- **INV-046/Q00 and Q01 (prose):** consistent. The dangling colon is settled in review 37.
- **INV-046/D01:**
  - Spans of the same indicated period have the same dates.
  - `dates.py` confirms the different spans of February.
  - Same-period class indicators agree, by INV-045 and INV-006.
- **INV-046/S01:** both directions re-derived. It rests on the `usedScope` tie of the basis counts (see RA-3-01).
- **INV-049/D01:** consistent; the reading of v38 is settled in fix 38.
- **INV-049/D02:** consistent; settled in review 39 and fix 38.
- **INV-049/S01:** consistent.
- **INV-049/W01:** `dates.py`: day 43; review window 7 April to 5 May; time range ends 6 April.
- **INV-050/D01:** consistent with `fillsPeriod` and the `when` clause of E-039.
- **INV-050/D02:** E-039 `reviewWindow` is SHOULD without a `when` clause; the window period is in the view by INV-003 (`refs(v)`).
- **INV-050/S01:** consistent. "Needs only its own values" holds for INV-050 itself; the weekly series of short views is E-039's, considered by fix 38. Not raised.

**Preventive treatment response (INV-055 to INV-062)**
- **INV-055/Q00 (prose):** consistent with `inPopulation` (age on the start).
- **INV-055/D01:** consistent with the populations and ages of the SD-ER rows.
- **INV-055/D02:** `dates.py`: only `ruleNice1329`, `ruleTr3639` and `ruleTr73` can fail `fitsMonthlyPeriod`.
- **INV-055/D03:** consistent with the first conjunct of INV-055, `intervalOnTreatment` and `notStoppedBefore`.
- **INV-055/S01:** `dates.py`: the earliest windows begin 56 days (AAN 14A), 59 days (NVN, Turkish Box 8) and 89 days (NICE 1.3.27) after the start; the period construction holds.
- **INV-055/W01:** `dates.py`: every date and both stop scenarios as stated.
- **INV-056/D01:** co-presence at MUST, by INV-056, INV-003 and E-040 W2.
- **INV-060/D01:** consistent with INV-060 and ISS-03.
- **INV-060/D02:** a monthly period exists within a compared period exactly when it has at least 28 days (INV-061).
- **INV-062/Q00 (prose):** `valueAvailable` and `scopeFor` are as described.
- **INV-062/D01:** consistent with INV-123, `evaluationResult` and `pretreatmentBaseline`.
- **INV-062/D02:**
  - The evaluated periods are the on-treatment atoms of the comparison, so INV-003 places the label and its comparison in one view.
  - The scopes in which components are decided match INV-063 (`allTypes`, `attackScope`).
  - The moved reference "INV-118 (C1-04, C1-06)" for attack counts follows the section 9 place of v34 INV-108. C1-06 alone would be exact; not raised.
- **INV-062/D03:** consistent with the acute and instrument conjuncts of INV-062 and with INV-063.
- **INV-062/S01:** consistent with INV-082 (`d₁ < d₂`), E-058 and INV-123.
- **INV-062/S02:** consistent.
