# RATIONALE audit — part 2 (lines 854–1403), model v40
Date: 2026-10-23
FINDINGS: 6 (CONTRADICTION 1, OVERCLAIM 5, STALE 0, WRONG-REFERENCE 0)
Entries audited: 97 entries anchored E-042 … E-067 (lines 854–1403 of `RATIONALE.md` v39): D 52, S 1, W 7, N 5, X 2 (67 entries audited in full), and Q 30 (non-quote prose only: claims about what a quote supports in the model; the quotes themselves were not re-verified).

## Method

**What I read.**
- PROCESS.md, in full.
- `RATIONALE.md`: section 1 (rules), and lines 854–1403 entry by entry. Other entries were read where an entry in the range refers to them: E-008/D01 to D04, E-032/D03, E-041/D05, D06, N01.
- `OUTPUT_MODEL.md` v40, all of it: sections 1–4 (notation, conformance, R-MCF, catalogue and case tables), every element E-001 to E-067, every invariant, sections 7–12. I compared each entry against the current formal text.
- `reviews/review-iter-41.md` (R41-01 and its class search).
- `oscillation/check-after-iter-40.md`, with its watch points. Watch point 8's declined entries are not in my range.
- "Checked and not raised" in reviews 36–41.
- `fixes/fix-iter-35.md`, `fix-iter-35-equivalence.md` and fixes 36–40, searched for every entry ID in my range.
- `fixes/fix-iter-06.md` (the E-045 population note) and `fixes/fix-iter-24.md` (the `sameSpan` matching of E-046).
- `audits/consistency-audit-v34.md`: CA-06, CA-08 and CA-09.
- Stage 1 v18: OUT-018 and OUT-020 (Statement and Evidence), and the OUT-031 Caveat.

**Settled points.** An entry that a review, fix or check already examined is listed as settled under "Checked and consistent". It is raised only where I found evidence those examinations did not consider. Each finding states that evidence.

**Scripts.** All scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/ra2/`. They were run with `python3 -I`.
- `inventory.py`: lists the entries in the range by kind (97: Q 30, D 52, W 7, N 5, S 1, X 2). It checks that every entry is named by the model (0 missing). It also checks that each of the 220 item, row and entry IDs cited in the range resolves in the model or in `RATIONALE.md` (0 unresolved).
- `omnlib.py`: an executable reading of the library and rule predicates used here (`plusDays`, `plusMonths`, `days`, `shift`, `notStoppedBefore`, `intervalOnTreatment`, `atTimePoint`), with the 18 SD-ER rows.
- `dates_check.py`: recomputes every date and day count of E-042/W01, W02, E-049/W01, W03 and E-063/W01 under those predicates.
- `claims_check.py`: small enumerations over the predicates as written. It covers:
  - the PeriodValue subtypes against `valueOfKind` (E-045/D07);
  - dropping a never-met, always-decided component under INV-063 (E-045/D05);
  - which E-046 predicates carry `#L.evaluated = 1` (E-046/D05);
  - ∀ against ∃ over `firstChangedDay` (E-049/D04);
  - `scopeFor` over 166 small subject profiles (E-045/D09);
  - grade-band coverage of whole and half-point scores (E-057/Q10);
  - an unstated start against INV-055 and INV-123 (E-042/D01);
  - the INV-074 line conjunct for a line that shows no formulation (E-051/D01);
  - which predicates mention `remissions` (E-062/D01);
  - INV-089's `ongoing` conjunct (E-063/N01);
  - `adherenceFor` (E-047/D02).
- `remission_check.py`: evaluates the first conjunct of INV-089 for four remission periods (E-062/D01, E-063/D01).
- `asks_check.py`: lists the invariants that ask for a `ResponderLabel` (none) or use `namedCriteria` (INV-116 only).

## Findings

### RA-2-01 OVERCLAIM: E-042/D01 says the response comparison is required "for every started treatment"
- Entry: E-042/D01 (moved v34 E-042 Notes, **Stop or pause**).
- Entry text: "The comparison itself is still required for every started treatment (INV-055), with its periods after the treatment start as OUT-018 states them (INV-056), and a diary may state the stop next to it as an `OtherItem` (section 3.7)."
- Model text:
  - INV-055, first conjunct: `(startOf(c, t) ≠ ∅ ⇒ ∃ o : Output • (c, o) ∈ Rep ∧ ∃ x ∈ parts(o) ∩ ResponseComparison • x.treatment = t)`.
  - INV-055 Reading: "For each preventive treatment whose start the context states, a response comparison is available."
  - INV-123 (definitional), with E-001 `factsShown`: `{rc ∈ {x} ∩ ResponseComparison • courseEvent(CourseEvent(treatment ↦ rc.treatment, kind ↦ start, date ↦ rc.treatmentStart))}`, which `stated` (E-008) requires to be in `c.subject.courseEvents`.
  - Section 3.8: "In the model, "a treatment whose start the context states" replaces "a treatment that has started"."
  - E-008 Meaning: where the context states no start, the course has still begun (`courseBegunBy`), for example for a treatment the subject was already taking (E-049/W02, W03).
- Why they conflict:
  - In its plain sense, a started treatment includes a course whose start the context does not state, for example a preventive treatment the subject was already taking.
  - For such a course, INV-055 asks for no comparison. INV-123 admits none, because a comparison must show a start date that the context states.
  - Script (`claims_check.py` (f)): with no start event, INV-055 asks nothing, and INV-123 admits no comparison of the treatment.
  - This is the v34 wording that CA-08 found in the model prose and that v35 replaced by section 3.8's wording rule there. The moved entry kept it.
  - New evidence: the equivalence fix examined this sentence only for its INV-056 citation ("periods 'after the treatment start'"), not for "every started treatment". No review raised it.
- Correction (entry only): "The comparison itself is still required for every preventive treatment whose start the context states (INV-055; R-MCF (1)), with its periods after the treatment start as OUT-018 states them (INV-056), …". No watch point is touched: the predicates of the treatment-course watch points of checks 28 and 32 are unchanged.

### RA-2-02 OVERCLAIM: E-046/D05 says a label over several periods is, like a label past a stop, decided by no component
- Entry: E-046/D05 (moved v34 E-046 Notes, **After a stop or pause**).
- Entry text: "A responder or non-responder label that refers to a period ending after a stop or pause of its treatment (`evaluatedOnTreatment` false) is therefore decided by no component (INV-063): the values of such a period neither force nor exclude a category, and the reader applies the named criterion to the values shown (INV-062), as for a label over several periods."
- Model text:
  - `reductionMet`, `reductionDecided`, `attackReductionMet` and `attackReductionDecided` contain `#L.evaluated = 1`. `scoreMet` and `scoreDecided` do not (E-046).
  - INV-063 Reading: "A reduction or attack-reduction component is decided only for a label that refers to one on-treatment period …; a label over several periods is not decided by these components. A score component is decided only by the pair of results it compares".
- Why they conflict:
  - The trailing comparison attaches to the whole elaboration: decided by no component, its values neither forcing nor excluding a category. Read so, it says a label over several periods is likewise decided by no component.
  - The model decides a label over several periods by its score components. Example: three evaluated months, critIhsQ6, a MIDAS baseline of 15 and a score of 8 at the evaluation within the last month. Then `scoreMet` holds, and INV-063 forces "responder".
  - Script (`claims_check.py` (b)): the four reduction and attack predicates require `#L.evaluated = 1`, the two score predicates do not, and the witness gives `scoreMet` = true.
  - The past-the-stop case is correct, because INV-063's antecedent requires `evaluatedOnTreatment(L)`. Only the analogy claims too much.
  - New evidence: the analogy has not been examined. Fix 18 wrote the sentence; no review of iterations 19–41 mentions it.
- Correction (entry only): replace "as for a label over several periods" by "as for the reduction and attack-reduction components of a label over several periods (E-046/D01)". The responder-label watch points of checks 08, 12, 16 and 32 are untouched.

### RA-2-03 OVERCLAIM: E-051/D01 says a single-formulation summary "lists only attacks treated with it" and that every attack line shows a formulation
- Entry: E-051/D01 (moved v34 E-051 Notes, **Formulation of a required summary**).
- Entry text: "A summary of all formulations names every formulation of the drug that the subject has used (INV-072), and one of a single formulation lists only attacks treated with it (INV-074). Every attack line shows a drug, and a formulation, in which the subject has used it (INV-123), as the formulations of an acute treatment line do (INV-123); …"
- Model text:
  - E-053: `formulation : opt FormulationOrRoute  SHOULD`.
  - INV-074: `∀ l ∈ ran s.sequence • l.drug = s.drug ∧ inPeriod(l.onset, s.period) ∧ (s.formulationScope = singleFormulation ∨ s.formulations ≠ ∅ ⇒ ∀ f ∈ l.formulation • f ∈ s.formulations)`.
  - INV-074 Reading: "all of its drug and period and, where a line shows its formulation, of a formulation that the summary names: always for a single formulation".
  - INV-123 with `factsShown` `usedMedication((l.drug, l.formulation))`: `stated` requires `∃ m ∈ c.subject.acuteMedications • m.drug = dr ∧ ∀ x ∈ fs • m.formulation = x`, a condition on the formulation only where the line shows one.
- Why they conflict:
  - A line's formulation is optional (SHOULD). INV-074 constrains only a line that shows its formulation; a line of a single-formulation summary that shows none is admitted.
  - So INV-074 guarantees that the summary lists no line that shows another formulation, not that every attack it lists was treated with its formulation. The model's own INV-074 Reading carries the qualification.
  - Likewise, INV-123 makes the drug of every line, and the formulation it shows where it shows one, those of a used medication. It does not make every line show a formulation.
  - Script (`claims_check.py` (h)): INV-074's line conjunct holds for a single-formulation summary {oral} with a line that shows no formulation, and fails for a line that shows another formulation.
  - New evidence: the v34 text had the same sentences. Fix 35 (D-14) re-pointed only their citations to INV-123. No review examined the claims.
- Correction (entry only): "…, and one of a single formulation lists no attack line that shows another formulation (INV-074). The drug that an attack line shows, and the formulation it shows where it shows one (E-053 `formulation`, SHOULD), are those of an acute medication the subject has used (INV-123), as the formulations of an acute treatment line are (INV-123); …". No tie should be added: the class of INV-123 is watch point 3 of check 36.

### RA-2-04 OVERCLAIM: E-062/D01 says a view of a past period "shows" an overlapping remission period
- Entry: E-062/D01 (moved v34 E-062 Notes, as corrected for CA-06).
- Entry text: "The length is that of the whole attack-free period, to its end or, while it has not ended by the as-of date, to the as-of date, not that of its part within the period the view covers (E-063/D01); so a view of a past period shows a remission period that overlaps it and has exceeded three months by the as-of date."
- Model text:
  - E-062: `remissions : seq →RemissionPeriodItem  SHOULD`. Its presence constraint is only "not empty" (section 3.3, item 2).
  - INV-088 has no conjunct on `remissions`. Its Reading says the view "refers to … its remission periods as E-062 states".
  - INV-089 only orders a view's remissions. INV-124 only excludes overlaps.
  - E-063/D01: "a remission period that the ICHD-3 Definitions of terms recognise as of the as-of date **can be shown** in a view of any covered period that it overlaps".
- Why they conflict:
  - No invariant relates the remission periods of a cluster view to its covered period, or requires any particular remission period in it.
  - The model only admits an overlapping remission period whose whole length exceeds three months: INV-089 tests the bound on `lastDay`, not on the part within the covered period.
  - "shows" states as a fact what the model only permits. It also disagrees with E-063/D01's "can be shown", which states the same consequence.
  - Script (`claims_check.py` (i)): the only predicate that mentions `remissions` is INV-089 (the ordering conjunct); E-062 declares it SHOULD.
  - New evidence: CA-06 corrected only the start-date sentence of this entry; this sentence was not examined.
- Correction (entry only): "…; so a view of a past period may show a remission period that overlaps it and has exceeded three months by the as-of date (E-063/D01)."

### RA-2-05 OVERCLAIM: E-062/D01 and E-063/D01 say a remission period that shows its start date lasts more than three months; the bound also needs a shown last day
- Entries: E-062/D01 and E-063/D01 (both corrected for CA-06 in v35).
- Entry text:
  - E-062/D01: "A remission period that shows its start date is an attack-free period of more than three months, as the ICHD-3 Definitions of terms require (E-063, INV-089); every fully conformant output shows the start date (E-063 `start`, SHOULD)." Also: "Attack-free periods of three months or less, among them those that ICHD-3 3.1.2 Chronic cluster headache calls remissions, are not shown as remission periods that show their start date; see ISS-12."
  - E-063/D01: "… so an attack-free period of three months or less is not shown as a remission period that shows its start date, also where 3.1.2 calls it a remission; …"
- Model text:
  - INV-089: `(x ∈ RemissionPeriodItem ⇒ ∀ s ∈ x.start; e ∈ lastDay(x) • plusMonths(s, remissionMoreThanMonths) ≤ e)`. The duration conjunct is `∀ s ∈ x.start; e ∈ lastDay(x) • s ≤ e ∧ ∀ d ∈ x.duration • d = daysLong(days(s, e))`.
  - E-063: `fun lastDay(x) ≙ {d : Date | (x.ongoing ∧ d = ctx(outputOf(x)).asOf) ∨ (¬ x.ongoing ∧ d ∈ x.end)}` and `end : opt Date  SHOULD when ¬ self.ongoing`.
- Why they conflict:
  - A remission period that has ended (`ongoing` false) but shows no end date has an empty `lastDay`. Both conjuncts are then vacuous.
  - So it may show its start date and, for example, a duration of 30 days in a MUST-conformant output; INV-124 is vacuous for it too. Its only deviation is from the SHOULD on `end`.
  - The bound holds only where the period shows its start date and its last day: its end date, or the as-of date while ongoing.
  - "Every fully conformant output shows the start date" names only one of the two SHOULD attributes the bound needs.
  - Script (`remission_check.py`):
    - ended, start and end shown, 30 days: rejected;
    - ended, start shown, no end, duration 30 days: admitted;
    - ongoing from 1 June, 143 days to the as-of date: admitted;
    - ongoing with an end date: rejected.
  - New evidence: CA-06 raised only the missing start date ("holds only where the remission period shows its start date"). Fix 35 qualified these sentences for it. The missing end date of an ended period was not considered.
- Correction (entries; prose only):
  - E-062/D01: "A remission period that shows its start date and its last day (its end date or, while it is ongoing, the as-of date; `lastDay`, E-063) is an attack-free period of more than three months, as the ICHD-3 Definitions of terms require (INV-089); every fully conformant output shows both (E-063 `start`, SHOULD; `end`, SHOULD once the period has ended)."
  - In the last sentence of E-062/D01 and in E-063/D01: "… not shown as a remission period that shows its start date and its last day …".
  - The class (PROCESS.md section 6a): the model prose states the same bound with the same gap: the INV-089 Reading ("a remission period that shows its start date lasts more than three months …") and ISS-12 Effect. The fixer should qualify them in the same way.
  - A formal alternative would test the bound on a shown duration. CA-06 offered it; fix 35 did not take it, keeping "no re-tying of E-063" (check 32, watch point 1). It is not needed.

### RA-2-06 CONTRADICTION: E-063/N01 says the output shows the end of each remission period it shows
- Entry: E-063/N01 (moved v34 E-063 Notes).
- Entry text: "The output shows the start, end and duration of each remission period it shows, but not the ICHD-3 element "cannot be induced with alcohol or nitroglycerine" (OUT-031 Caveats)."
- Model text:
  - INV-089: `(x.ongoing ⇒ x.end = ∅)`.
  - E-063 Meaning: "An ongoing period is one that has not ended by the as-of date of the output: it shows no end date, and its duration runs from its start to the as-of date (its duration to date)."
  - E-063: `start : opt Date SHOULD`, `end : opt Date SHOULD when ¬ self.ongoing`, `duration : opt Duration derived SHOULD`.
  - E-063/W01 itself shows "an ongoing remission period".
- Why they conflict: for an ongoing remission period, the model forbids an end date. For the others, start, end and duration are SHOULD, not guaranteed. The sentence repeats the wording of the Stage 1 OUT-031 Caveat as if it were what the model guarantees. Script (`claims_check.py` (j)): the conjunct `(x.ongoing ⇒ x.end = ∅)` is in INV-089. The entry's point, that the alcohol/nitroglycerine element is not modelled, is correct.
- Correction (entry only): "The output shows the start date, the end date once the period has ended, and the duration (to date, while it is ongoing) of each remission period it shows (E-063, SHOULD; INV-089), but not the ICHD-3 element "cannot be induced with alcohol or nitroglycerine" (OUT-031 Caveats)."

## Checked and consistent

- **E-042/Q00 (prose):** the two "That …" claims match `atTimePoint` (`next(p.end) = tp.earliest`: the evaluated period ends with the interval) and `intervalOnTreatment`. "E-041 (Notes, **Stop or pause**)" is E-041/D06.
- **E-042/D01, apart from RA-2-01:**
  - "stopped or paused before the last day of the interval" is `¬ intervalOnTreatment` (`notStoppedBefore(…, plusDays(shift(a, minOffset), −1))`). INV-058 then admits, and INV-059 and the E-043 `when` clause ask for, no time point at that anchor.
  - INV-056 places the periods after the start. Section 3.7 permits an `OtherItem`. E-049 `after` holds the periods after the stop.
- **E-042/W01, W02:** recomputed (`dates_check.py`). Settled as well: reviews 37–41 recomputed them.
  - W01: the 3-month time point is 1 April = `next`(31 March); NICE 1.3.28 falls on 26 March; 26 February–25 March is 28 days.
  - W02: the last days of the intervals are 28 February (Box 8), 25 March (NICE 1.3.28) and 31 March (the 3-month rules; for the types the script assumes for a monthly antibody, NICE 1.3.27, SIGN fixed-dose, EHF Q3, IHS Q2 monthly and Russian 7.1).
  - A stop on 10 February loses every time point, and a stop on 31 March keeps them all.
- **E-043/D01:** settled (reviews 37, 38). The chain holds at MUST:
  - INV-056 (`m.period ∈ {rc.baseline} ∪ ran rc.onTreatment`, `ch.reference ∈ rc.values`);
  - INV-003 and its Notes (one view per period atom);
  - W2 `shown MUST` on `timePoints` and on E-040 `reference` and `compared`.
- **E-044/D01:** INV-060's antecedent (percent form, compared period of at least `shortestMonthlyDays`, no subject condition) and INV-061's monthly periods. Corrected in v35 (EQ35-03).
- **E-045/Q00–Q04 (prose):**
  - The day measures over all types match the `ReductionComponent` comment and `ch.reference.typeScope = allTypes`.
  - The Box 8 threshold matches `attackReduction` with type `c1` (E-045/D08, D09).
- **E-045/D01:** the six SD-RC criteria are exactly those that the Stage 1 v18 evidence of OUT-018 and OUT-020 names: NICE 1.3.28 and 1.3.29, IHS Q6, IHS 2025, DMKG/ÖKSG/SKG and Russian 7.1. The [S-002] "50% responder rate" is not among them.
- **E-045/D02, D03:**
  - SD-RC-01 has `measures ↦ {migraineDays}`.
  - In SD-RC-03 both MIDAS ranges (11–20, ≥ 20) contain 20, and components are alternatives. The overlap is settled (R01-12; model section 9, ISS-07 row).
- **E-045/D04:** written by fix 06, on review 02's settled ground that a label under a criterion that does not apply is no defect. It claims no formal population restriction; D06 states that no criterion is required. No new evidence.
- **E-045/D05:**
  - A left-out component whose condition fails is never met, always decided and asks for no value; INV-116 keeps `alsoRestsOn` equal.
  - Dropping such a component changes no category that INV-063 forces (`claims_check.py` (a): 84 combinations, 0 differences).
  - "A criterion shown under any other name is not constrained" is read in its INV-116 context: no equality to a named criterion. Its value type's `where` clause and INV-062 and INV-063 still apply, as the next sentence implies.
- **E-045/D06:**
  - The `conditionHolds` cases match.
  - INV-001's antichain rule still admits a treatment given for an episodic migraine type of a subject who has had `c1_3`. The type is then a migraine type other than `c1` itself, because `c1` and `c1_3` cannot both be listed.
  - No invariant asks for a `ResponderLabel`; `namedCriteria` is used only by INV-116 (`asks_check.py`).
- **E-045/D07:**
  - The PeriodValue subtypes that `valueOfKind` does not name are exactly CompletenessIndicator, MigraineFreePeriodMark and ClusterAttackRate, the three the entry lists (`claims_check.py` (k)).
  - The INV-062 conjuncts match: for `acuteTreatmentEffectiveness` (evaluated periods, `allTypes`, every acute medication) and for `periodValuesOf(acuteTreatmentSummaries)` (baseline included).
  - So does the `evaluationResult` clause.
- **E-045/D08:**
  - `attackReduction` is decided on `L.otherValues ∩ AttackCount` in `attackScope`.
  - The components are alternatives, and INV-062 reads `alsoRestsOn`.
- **E-045/D09:**
  - The reduction predicates use `allTypes`, as INV-056, INV-057 and `levelDays` do.
  - `scopeFor` over 166 small profiles (`claims_check.py` (d)): exactly one scope each time. Values over all types never decide a one-type attack component for a subject who has or may have another type.
  - "An attack count has no headache type of its own" refers to the counted event: `CountedEvent` names no type, unlike `migraineDays`. The type lies in the scope, as the entry goes on to say (`attackScope`, `scopeFor`). It does not deny type scopes (cf. R41-01); not raised.
- **E-045/N01, N02:** SD-RC-02 has only the 30 % clause. SD-RC has no scheme criterion (review 39).
- **E-046/D01:** `#L.evaluated = 1` is in `reductionMet` and in the decided branch of `reductionDecided`.
- **E-046/D02:**
  - Evaluated periods and attack-count periods are matched by `sameSpan`.
  - For reduction components, the reference is matched as the baseline atom (`ch.reference.period = rc.baseline`). INV-056 requires that of every change of a comparison, and fix 24 kept it for that reason. So the dates claim holds in every MUST-conformant output; not raised.
  - The type-scope and example sentences match `reductionMet`.
- **E-046/D03:**
  - The `evaluationResult` and `pretreatmentBaseline` readings match their predicates, and `b ∈ r.baselineResult` (E-058).
  - "available" refers to the subject's available results (section 3.5), as in INV-081 and INV-123. Corrected in v35 (EQ35-04).
- **E-046/D04:**
  - `ControlLevel` has four values.
  - INV-064 uses `courseBegunBy`, which equals "on or after the start" where the start is stated (INV-001), and `evaluatedOnTreatment`.
- **E-046/D05, apart from RA-2-02:** INV-063's antecedent requires `evaluatedOnTreatment(L)`.
- **E-046/D06:** SD-CL-04 is `true`; settled (review 38).
- **E-047/D01, D02:**
  - `AdherenceValue` matches.
  - `adherenceFor` admits a window equal to the evaluated period and a window from the start, and rejects a window of the last 5 days and one that begins before the start (`claims_check.py` (l)).
  - INV-066 asks for one window.
- **E-048/D01:** INV-068 (MUST) requires a stated start and `notStoppedBefore`. INV-123 ties the comparison's start fact.
- **E-049/D01–D03:**
  - `originalStart` and `resumesFrom` are as stated, the own start for a course that resumes none.
  - INV-001 forces a stated start for a course that resumes another, hence "(INV-001)" in D02.
  - The `when` clauses of `baseline` and `onTreatmentPeriod`, INV-103 and INV-112 match.
  - D03 keeps "aligned to the event, not to the start" (check 36, watch point 6).
- **E-049/D04:** v34 INV-070 had `∀ x ∈ firstChangedDay(…) • (startOf(…) = ∅ ∧ courseBegunBy(…) ⇒ v.onTreatmentPeriod ≠ ∅)`; v40's `when` disjunct has `∃ x`. The two forms are equivalent (`claims_check.py` (c)). The first disjunct is verbatim v34.
- **E-049/W01–W03:** recomputed (`dates_check.py`).
  - W01: September is admitted as the on-treatment period and December 2025 as the baseline; August 2026 is not.
  - W03: June is admitted; August and February are not. The reduction view's `when` clause is false, and INV-112 admits no on-treatment period.
  - W02: `originalStart` is ∅, so no baseline is shown.
- **E-050/D01:** `requiredOutcomes` holds both pain freedom and headache relief; C2-07 applies.
- **E-051/D01, apart from RA-2-03:**
  - The two readings of `summarisesMedication` match its definition.
  - INV-072 states the formulations, and INV-071 asks for both presentations.
  - `AcuteTreatmentSummary` is not in `factsShown`, so a summary may name an unused formulation.
- **E-054/D01, E-055/D01, D02:**
  - `DrugClass` is a given set.
  - Course events lie on or before the as-of date (INV-001).
  - INV-079 sets the duration to the as-of date when there is no stop.
  - INV-077 places no constraint on `covers`.
  - `StopReason` matches.
- **E-056/D01, D02, S01, X01:** settled (reviews 39, 40). Rechecked: the Realises fields of E-015, E-016, E-017, E-019, E-055, E-058 and E-046, INV-080, the W2 index, and INV-001's silence on `schemeSelection`.
- **E-057/Q00–Q10 (prose), D01–D07, N01:**
  - SD-IN and SD-GB match.
  - Q10's whole-number claim: no whole score is uncovered, and half-point gaps exist (`claims_check.py` (e)).
  - D02's HALT-90 overlap at 20 is settled.
  - D05 matches the SD-IN `publishedGrading` cells, E-058 `category` `when`, and INV-082.
  - D07 (review 37) matches the INV-082 conjuncts for instruments outside `dom scoreRange`, `dom publishedRecall` and `banded`.
- **E-058/D01:** critIhsQ6 and critDmkg use MIDAS and HIT-6.
- **E-059/Q01–Q03 (prose), D01:**
  - `OtherScreeningName` excludes the three names.
  - INV-085 applies.
  - `ScreeningResult` has no category.
- **E-060/Q01, Q02 (prose), D01–D03, N01:**
  - `completeCycles` in INV-087.
  - The lead-in conjuncts: it starts at `covers.start`, ends before every shown day 1, and every later line shows its day 1. E-032/D03 is the cited analogy.
  - The lead-in Meaning is settled (review 05; checks 04, 12).
- **E-061/D01, D02:** `nextWindowDays` of an ended lead-in, and the earliest shown day 1 (INV-087, INV-124). D02 is settled (review 36).
- **E-062/X01:**
  - CA-09, kept by fix 11.
  - INV-088's Reading says "refers to"; INV-011's fourth conjunct asks for completeness.
  - Section 6.0 lists the cluster references as not marked.
- **E-062/D01, rest:** the annotation sentence; "every fully conformant output shows the start date" (E-063 `start`, SHOULD).
- **E-063/Q01; E-063/D01, rest; E-063/W01:**
  - Phases are dated without clipping; `lastDay` applies; complete cycle lines may extend beyond the covered period (INV-087).
  - W01 recomputed: 42 days and 143 days, and the 1 June remission exceeds three months by 21 October.
- **E-064/Q00, Q01 (prose), D01–D03:**
  - INV-003 and `lengthDays` (MUST); INV-089's rate–count relation in one view; INV-011.
  - D03 is settled (review 41 class search).
- **E-066/D01:** `summaryTimeCourse` as stated (INV-104); INV-094 (`Clinicians`); ISS-04.
- **E-067/W01:** INV-105's covered-period values, and its series of all whole periods of one granularity (`fillsPeriod`) wherever the covered period contains one. INV-095 does not restrict `covers` otherwise.
