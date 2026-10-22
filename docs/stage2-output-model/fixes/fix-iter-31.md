# Fix log — iteration 31
Input review: reviews/review-iter-31.md · Input version: v30 · Output version: v31
Date: 2026-10-22

## What was read and checked

**Read:**
- PROCESS.md, in full: the scope exclusions of section 2, the notation of section 3, fidelity and evidence of section 4, the structure of section 6, identifiers of section 7, frozen items of section 10 and the practical notes of section 11.
- Stage 1 v18, sections 1–3 in full (OUT-001 to OUT-039). Read closely:
  - OUT-017 ("For patients withdrawing from overused medication, the diary output SHOULD show headache days and acute medication days from the start of withdrawal onward, including the review window …");
  - OUT-020 ("If the output displays a responder or non-responder label, it SHOULD name the criterion applied […] and SHOULD always show the underlying values (OUT-018, OUT-019)");
  - OUT-022 ("After a preventive treatment is stopped, paused or reduced, the diary output SHOULD continue to show headache and migraine frequency and compare it with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible");
  - OUT-037 ("If such an index is shown for migraine, it SHOULD be labelled as exploratory and shown together with its component measures").
- v30 (`OUTPUT_MODEL.md`, byte-identical to `history/v30.md`), in full: sections 1–10, and the iteration-30 entries of sections 11 and 12. Read closely: section 3.3 (items 2 and 5), E-033, E-039, E-046, E-049, INV-036, INV-050, INV-051, INV-058, INV-061, INV-062, INV-063, INV-064, INV-067, INV-070, INV-079, INV-092, INV-097, INV-103, INV-109 and INV-110.
- Review 31 (one remark, R31-01), with its "Checked and not raised" list.
- Earlier loop files:
  - fix 30 (format and checks);
  - fix 26 ("INV-070 keeps its level. It stays SHOULD, the strength of OUT-022");
  - fix 05 (the INV-064 start tie, added because "the tie existed only in INV-062, at SHOULD");
  - fix 18 (R18-01: why no definitional bound was put on the periods of every responder label);
  - the oscillation checks after iterations 8, 12, 16, 24 and 28, with their watch points. The check after iteration 28 names INV-070 in watch points 1, 2 and 5; the check after iteration 24 names the class "Truth of a shown fact tied to the context"; iteration-08 watch point 4 and iteration-12 watch point 5 protect INV-050's start ties; iteration-12 watch point 2 and iteration-16 watch point 4 protect the responder-label ties.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**No download and no web search.** The fix adds no fact, value or source. The quotes added are fragments of Stage 1 statements (OUT-017, OUT-018, OUT-020, OUT-022, OUT-037), checked by script against Stage 1 v18.

**Scripts.** All are in a fresh scratchpad folder, `fix31/` (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix31/`), and were run with `python3 -I`.
- `attrscan31.py` (`attrscan31.out`): which invariants and element predicates constrain the attributes concerned, by level, in v30 and v31; and every occurrence of the three ties with its role (constraint or condition).
- `common31.py`, `false31.py` (`false31.out`): the library of section 2.8, the context predicates of E-008, and transcriptions of every invariant that ranges over the atoms of the review's four outputs. The transcribed predicate texts of INV-050, INV-062, INV-070, INV-092 and INV-112 to INV-115 are asserted to equal the `omn` text of v30 and v31. The other invariants used are asserted to be byte-identical in the two versions.
- `equiv31.py` (`equiv31.out`): checks (ii) and (iii): v30 against v31 on random and enumerated views, labels and indices, with targeted variants of the review's output 1, and the construction of the views that INV-103 asks for.
- `conjuncts31.py` (`conjuncts31_v30.out`, `conjuncts31_v31.out`): every SHOULD and SHOULD NOT invariant split into its top-level conjuncts, for the identity-tie check.
- `apply31.py` builds v31 from `history/v30.md` by exact replacements, each asserted to occur once. The INV-070 predicate and Notes are split by asserted line and paragraph boundaries. `entry31.md` is the change-log entry.
- `blockcheck31.py` (`blockcheck31.out`): which `omn` blocks changed, whether each moved conjunct is verbatim and in one place, and the counts of the protected tie terms.
- `mech31.py`, `names27.py`, `tokcheck27.py`, `omndiff27.py`, `itemdiff27.py`, `scope27.py` and `quotes31.py` are copies of fix 29's check scripts, which I read before use.
  - In `mech31.py` the highest invariant number is a command-line argument (111 for v30, 115 for v31) instead of the fixed 111.
  - In `quotes31.py` the label "already in v28" reads "already in v30".

### Verification of R31-01

**The remark holds.**
- **Which invariants constrain the attributes** (`attrscan31.out`, v30).
  - E-049 `treatment`, `event`, `eventDate`, `baseline`, `onTreatmentPeriod` and `after`: INV-070, INV-097 and INV-103 only, all SHOULD.
  - E-039 `withdrawalStart`: INV-049 and INV-050 (SHOULD). INV-051 is definitional but relates the review window to the date only.
  - E-046 `comparison`: INV-062 (SHOULD) and the predicates of E-046. `rc.treatment = L.treatment` occurs ten times: once as a constraint, inside INV-062's existential, and nine times as a condition (an antecedent or a witness selector) in INV-062 and E-046.
  - E-033 `components`: INV-092 (SHOULD) only.
  - So the four ties held only at SHOULD, as the review says.
- **The review's four outputs** (`false31.out`). Context: an adult subject; a preventive treatment t, given for migraine, started on 1 January 2026 and discontinued on 30 June 2026; a second preventive treatment u started on 1 August 2026; no start of withdrawal; as of 21 October 2026. Each output was built with all the presentation that the SHOULD invariants ask for (definition labels, completeness indicators, caveats, adherence, residual burden, time points, attribute presence), so that only the tie under test can fail. Every invariant that ranges over its atoms was evaluated.

| Output | v30: failing invariants | v30 MUST-conformant | v31: failing invariants | v31 MUST-conformant |
|---|---|---|---|---|
| 1. Post-stop view of t, `stop(paused)` on 31 March 2026 (an event the context does not have); baseline May 2026; on-treatment August 2026; after February and April 2026 | INV-070 (SHOULD) | yes | INV-112 (definitional) | no |
| 2. Withdrawal follow-up view with start of withdrawal 1 February 2026 (the context states none); review window 1–29 March 2026 by INV-051 | INV-050 (SHOULD) | yes | INV-113 (definitional) | no |
| 3. "Responder" label of t (evaluated March 2026, NICE CG150 1.3.28) whose comparison is u's response comparison (itself MUST-conformant: INV-053, INV-054, INV-056, INV-057, INV-058 and INV-059 hold, with the time points of NICE 1.3.27, Russian 7.1 and Turkish Box 8) | INV-062 (SHOULD) | yes | INV-062 (SHOULD), INV-114 (definitional) | no |
| 4. Composite index for migraine of January 2026 whose components are the headache days and intensity of June 2026 | INV-092 (SHOULD) | yes | INV-115 (definitional) | no |

In output 3, INV-063 holds in v30 because the label's comparison is not of its treatment: no component is met or decided, so "responder" is unconstrained. Under v31, INV-062 still fails as well, because March is not among u's on-treatment periods.

- **Why this is a defect.** Section 3.3 (5) calls definitional "a bound that follows from an element's definition [...] or the structure of an element (for example that a series is consecutive)". Such an invariant "holds wherever the element is shown" and "excludes only outputs that show a value contradicting the definition of the element". The four ties are of that kind:
  - E-049 declares `baseline` as "the original pre-treatment baseline period, before the treatment was first started", `onTreatmentPeriod` as "an on-treatment period before the changed regimen" and `after` as "consecutive periods from the first day of the changed regimen onward";
  - E-039 is the follow-up of a withdrawal of the subject;
  - E-046 declares `comparison` as "the underlying values (OUT-018)" of a label that classifies the response to its treatment;
  - E-033 declares `components` as "the component measures shown with it".

  A SHOULD-level statement of them lets a MUST-conformant output, or one that deviates from a SHOULD for a valid reason, state an event, a withdrawal, a treatment or a period that is false. Fix 30 applied the same reading to INV-079.

### Separation of the conjuncts (section 3.3)

"Identity" marks a conjunct that states what the element or one of its attributes is (which treatment, event, withdrawal or period), or the declared structure of an attribute. "Content" marks a conjunct that states what Stage 1 asks the element to show (presence, co-presence, coverage, alignment, values), at the strength of its statement part.

**INV-070 (E-049).**

| Conjunct | What it states | Class | Moved |
|---|---|---|---|
| `v.treatment ∈ ctx.subject.preventiveTreatments` | which treatment: one of the subject's preventive treatments | identity | yes, to INV-112 |
| `(v.event is stop ∨ v.event = doseChange(reduction))` | which kind of event (the E-049 comment: stop(discontinued), stop(paused) or doseChange(reduction)) | identity | yes |
| `eventOn(ctx, v.treatment, v.event, v.eventDate)` | which stop, pause or reduction: one of the course, on its date (as INV-036 for markers) | identity | yes |
| `(∀ b ∈ v.baseline • ∃ s ∈ originalStart(ctx, v.treatment) • b.end < s)` | which period is the original pre-treatment baseline | identity (a bound that follows from the declaration of `baseline`) | yes |
| `consecutive(v.after)` | the structure of `after` ("consecutive periods") | identity (structure, the example of section 3.3 (5)) | yes |
| `(∀ q ∈ v.onTreatmentPeriod • courseBegunBy(ctx, v.treatment, q.start) ∧ q.end < x)` | which period is the on-treatment period: one of the course, before the changed regimen | identity | yes |
| `(v.after ≠ ∅ ⇒ first(v.after).start = x)` | the periods after the event run from the first day of the changed regimen | identity (a bound that follows from the declaration of `after`) | yes |
| `(startOf(ctx, v.treatment) = ∅ ∧ courseBegunBy(ctx, v.treatment, plusDays(x, −1)) ⇒ v.onTreatmentPeriod ≠ ∅)` | that the on-treatment period is shown where the context states no start | content: presence (OUT-022 "compare it with both the on-treatment period …") | no; stays SHOULD (watch points 1 and 5) |
| `∀ p ∈ v.baseline ∪ v.onTreatmentPeriod ∪ ran v.after • shownDay(v, headacheDays, …) ∧ shownDay(v, migraineDays, …)` | that the values of the periods are shown | content (OUT-022 "continue to show headache and migraine frequency") | no |

**INV-050 (E-039).**

| Conjunct | What it states | Class | Moved |
|---|---|---|---|
| `v.withdrawalStart ∈ ctx.subject.withdrawalStart` | which withdrawal: one of the subject's | identity | yes, to INV-113 |
| `v.covers.start = v.withdrawalStart` | the view covers the time from the start of withdrawal onward | content (OUT-017 "from the start of withdrawal onward"). A deviating view states its covered period truly (INV-003); protected by iteration-08 watch point 4 | no |
| `shownDay(v, headacheDays, v.covers, allTypes)`, `shownDay(v, acuteMedicationDays(allAcuteMedication), v.covers, allTypes)` | values | content | no |
| `∀ sr ∈ v.series • sr ∈ v.content ∧ first(sr.periods).start = v.withdrawalStart ∧ fillsPeriod(sr, v.covers) ∧ perPeriod(…) ∧ perPeriod(…)` | co-presence, alignment and coverage of the series, values | content (OUT-017; iteration-08 watch point 4, iteration-12 watch point 5). The series' own structure is already definitional (INV-004) | no |
| `(plusDays(v.withdrawalStart, 7 × reviewWindowToWeeks) ≤ v.covers.end ⇒ v.reviewWindow ≠ ∅)` | presence of the review window | content | no |

**INV-062 (E-046).**

| Conjunct | What it states | Class | Moved |
|---|---|---|---|
| `L.criterion ≠ ∅` | presence of the criterion | content (OUT-020 "SHOULD name the criterion applied") | no |
| `rc.treatment = L.treatment` (inside `∃ rc ∈ L.comparison • …`) | which comparison is the label's underlying values: one of its treatment | identity | yes, to INV-114 |
| `rc ∈ viewOf(L).content` | co-presence | content (OUT-020 "SHOULD always show the underlying values") | no |
| `ran L.evaluated ⊆ ran rc.onTreatment` | the comparison shows the label's periods | content: coverage of the underlying values. It is the counterpart of INV-092's dimension coverage, which the review keeps at SHOULD; see the identity-tie check | no |
| the residual burden of each percentage change of the evaluated periods; `∀ x ∈ L.otherValues • x ∈ viewOf(L).content`; `∀ rb ∈ L.residual • rb ∈ viewOf(L).content` | coverage and co-presence | content (OUT-019, OUT-020) | no |
| the `valueAvailable`, reduction-component, score-component and control-level conjuncts | witnesses (coverage); `rc.treatment = L.treatment` is a condition in three of their antecedents | content; the three conditions are kept verbatim, because they constrain nothing | no |

**INV-092 (E-033).**

| Conjunct | What it states | Class | Moved |
|---|---|---|---|
| `annotated(x, exploratoryMeasure)` | label | content (OUT-037 "SHOULD be labelled as exploratory") | no |
| `m ∈ viewOf(x).content` | co-presence of each component | content ("shown together with its component measures") | no |
| `m.period = x.period ∧ m.typeScope = x.typeScope` | which values are the index's components | identity | yes, to INV-115 |
| `∀ d ∈ x.combines • ∃ m ∈ x.components • dimensionOf(m, d)` | a component for each dimension | content (coverage) | no |

### Choice between the review's options

**Option (a) taken.** The identity conjuncts were moved, verbatim, to four new definitional invariants, and every content conjunct stays at its level in its invariant. New invariants were chosen over conjuncts of INV-051 or INV-063: both quantify over a shown attribute (`∀ v; w ∈ v.reviewWindow`, `∀ L; K ∈ L.criterion`). A tie added inside those quantifiers would hold only where a review window or a criterion is shown, and adding it outside would rewrite their predicates.

- **INV-112** (E-049) = v30 INV-070 lines 1–5 and 7, with the same `∀ x ∈ firstChangedDay(v.event, v.eventDate)` binder. INV-070 keeps the binder with the presence conjunct, and the `shownDay` conjunct.
- **INV-113** (E-039): `∀ v : WithdrawalFollowUpView • v.withdrawalStart ∈ ctx.subject.withdrawalStart`.
- **INV-114** (E-046): `∀ L : ResponderLabel; rc ∈ L.comparison • rc.treatment = L.treatment`. INV-062's existential keeps the presence of the comparison, its place in the label's view and its periods.
- **INV-115** (E-033): `∀ x : CompositeIndex • concerns(ctx, x.typeScope, c1) ⇒ ∀ m ∈ x.components • m.period = x.period ∧ m.typeScope = x.typeScope`. This keeps the scope of INV-092 (indices for migraine), as the review allows. An unrestricted tie would also exclude outputs that v30 admits as fully conformant: an index for another headache type, for which Stage 1 asks for no components. So it would add a constraint rather than move one, and the set of fully conformant outputs would change.

**`consecutive(v.after)` and the first start moved, not the review's variant.** The review also allows a variant: keep these two at SHOULD and make only `∀ p ∈ ran v.after • x ≤ p.start` definitional. It was not taken:
1. The two conjuncts are the structure that E-049 declares for `after` ("consecutive periods from the first day of the changed regimen onward"). Section 3.3 (5) names such structure definitional ("the structure of an element (for example that a series is consecutive)"). The model states the structure of period sequences definitionally elsewhere:
   - a series is consecutive (INV-004);
   - the span of a medication-overuse indicator is a run of consecutive periods that ends with the indicated period (INV-045);
   - the months of a control-level label are consecutive (INV-064).
2. Moving them makes nothing more required:
   - `after` stays SHOULD and may be empty;
   - the values of its periods stay SHOULD (INV-070);
   - a run from the first changed day can always be shown (check (iii) below);
   - any other period can be shown in the view (section 3.7).
3. The variant would add a conjunct the model did not state, and the task is to move the ties verbatim.

The difference is small and is measured in `equiv31.out`. Of the 1,176,539 random views that v31 rejects at the definitional level, 21,124 are rejected only because their periods after the event are not the consecutive run from the first changed day (each such period lies on or after it). The variant would have kept these at SHOULD. Each of them is also outside v30's full conformance.

**Option (b) not taken** (INV-070, INV-050, INV-062 and INV-092 made definitional, with their presence conjuncts moved to new SHOULD invariants). It gives the same verdicts. It would move more text, and the watch points of the check after iteration 28 name INV-070 as the place of the presence conjunct.

**Watch points kept** (oscillation checks after iterations 8, 12, 16, 24 and 28):
- **Watch point 1 (iteration 28).**
  - The INV-070 presence conjunct is kept verbatim, at SHOULD.
  - `courseBegunBy` and the on-treatment bound are kept verbatim; the bound is now definitional.
  - No ask is dropped, and INV-103 is byte-identical.
  - The E-049 Notes keep the classification of the view as aligned to the event.
- **Watch point 2.** `originalStart`, `resumes`, `resumesFrom`, the E-049 `baseline` `when` clause and the baseline conjunct are byte-identical. The baseline conjunct is now definitional, so no baseline is admitted where `originalStart = ∅` at any level.
- **Watch point 5.** The two places that ask for the on-treatment period (the E-049 `when` clause, and INV-070 where the start is not stated) are unchanged.
- **Watch point 4 and section 2.8.** No course-event date changed. Section 2.8, E-008's `omn` block and INV-001's predicate are byte-identical. Section 2.8 still cites INV-070 for "the first day off treatment is the day after it"; INV-070 still binds that day (`firstChangedDay`, `plusDays(x, −1)`), so the reference was left as it is.
- **INV-050** (iteration-08 watch point 4, iteration-12 watch point 5). The start ties, `fillsPeriod` and the running follow-up view are unchanged and at their level. Only the withdrawal tie moved.
- **Responder labels** (iteration-12 watch point 2, iteration-16 watch points 3 and 4). `rc.treatment = L.treatment` is not relaxed but made definitional. `#L.evaluated = 1`, the `evaluationResult` / `pretreatmentBaseline` pair, `allTypes`, `summarisesMedication`, `attackScope` and `conditionHolds` are byte-identical.
- **Direction.** Every admitted set narrows or stays equal: the fully conformant sets are equal, and the MUST-conformant sets narrow. No fix is reversed.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R31-01 | fixed: the review's preferred option (a) | **New:** INV-112, INV-113, INV-114, INV-115.<br>**Changed:**<br>• INV-050, INV-062, INV-070, INV-092 (Predicate, Reading, Notes);<br>• E-033, E-039, E-046, E-049 (Conformance, Notes);<br>• E-008, E-012, INV-001, INV-097, INV-103 (Notes: references);<br>• rows OUT-017, OUT-020, OUT-022, OUT-037 (Invariants column, coverage reason) | **Predicates.** The identity conjuncts of the four invariants were moved verbatim to four new definitional invariants (tables above). No conjunct, `when` clause or date was changed. INV-062's existential loses only the conjunct `rc.treatment = L.treatment ∧`.<br>**INV-112** "Post-stop monitoring shows the subject's event and its periods":<br>• definitional (E-049), Realises OUT-022;<br>• Evidence: the Stage 1 OUT-022 statement and the [S-011] and [S-022] quotes of INV-070;<br>• Notes: why the conjuncts are definitional, with INV-036, INV-004, INV-045 and INV-064 as precedents; why they make nothing more required; INV-070's v30 Notes on the day convention, **Original baseline** and the on-treatment bound, moved verbatim; satisfiability with INV-103.<br>**INV-113** "A withdrawal follow-up view shows a start of withdrawal of the subject": definitional (E-039), Realises OUT-017.<br>**INV-114** "A responder label's response comparison is one of the label's treatment": definitional (E-046), Realises OUT-020; Notes give the counterpart INV-079 (`∀ r ∈ l.preventiveResponse • r.treatment = l.treatment`) and state that no decision of INV-063 changes.<br>**INV-115** "The components of a composite index for migraine are of its period and type scope": definitional (E-033), Realises OUT-037; Notes give the counterpart INV-061 and the scope of INV-092.<br>**INV-070.** Reading: the values of the periods, and the on-treatment period where the context states no start; what the periods are is stated by INV-112. Notes: the presence conjunct and satisfiability (now "meet this invariant, INV-112 and INV-097").<br>**INV-050, INV-062, INV-092.** Reading and Notes point to the new invariant. INV-092's Reading drops "and for the same period" and adds the INV-115 clause.<br>**Elements.**<br>• E-033: the components are "of its period and type scope wherever it shows them (definitional, INV-115)"; Notes, Relations: INV-115.<br>• E-039: "The start of withdrawal it shows is one of the subject's, wherever it is shown (definitional, INV-113)"; Notes, Relations: INV-113.<br>• E-046: "Wherever it shows a response comparison as its underlying values, that comparison is one of the label's treatment (definitional, INV-114)"; Notes, Relations: INV-114.<br>• E-049: "INV-070 admits none" becomes "INV-112 admits none", and a new sentence lists what INV-112 fixes. In the Notes, the references to the bounds go to INV-112; the references to the asks stay with INV-070.<br>**References.** E-008 Notes (4), E-012 Notes (`concerns` also in INV-115), INV-001 Notes (2), INV-097 Notes, INV-103 Notes.<br>**Rows.** OUT-017 (+INV-113), OUT-020 (+INV-114), OUT-022 (+INV-112), OUT-037 (+INV-115): Invariants column, and a clause on the definitional tie in the coverage reason. The Elements columns are unchanged.<br>**Justification:**<br>• the remark is verified (tables above);<br>• levels: the content conjuncts keep the levels of their Stage 1 statement parts, and the moved ones have none of their own (section 3.3 (5));<br>• Realises of the new invariants = those of their source invariants (OUT-017, OUT-020, OUT-022, OUT-037);<br>• checks (i)–(iii) below. |

## Identity-tie check

**Question.** Does any other SHOULD, SHOULD NOT or MAY invariant state, at that level only, what its element is? The review's precedents are INV-036 (marker), INV-058 (time point), INV-061 (residual burden), INV-067 (adherence window), INV-079 (treatment line) and INV-110 (trigger view).

**Method.** Every conjunct (`conjuncts31_v30.out`) was read against the declarations of its element. There is no MAY invariant.
- **Identity** means that the conjunct states which atom, event, period or value an attribute holds, or an attribute's declared structure, so that a violation shows something false.
- **Content** means that the conjunct asks for presence, co-presence, coverage, alignment, annotations or values, or for the choice of a definition, a window or a time point that Stage 1 asks for at SHOULD.
- **Repertoire-scope invariants** state availability. Their conjuncts are existence requirements and witness selectors (for example `v.withdrawalStart = ws` in INV-049, or `v.event = e.kind` in INV-103), which choose which output must exist and constrain no shown element.

| Invariant | Conjunct(s) | Identity or content | Moved |
|---|---|---|---|
| INV-008 | a definition label for each measure that the view reports | content (presence); the label's identity is INV-111 (definitional) | no |
| INV-010 | the label for attacks names ICHD-3 "frequency of attacks" | content (which definition the view follows, OUT-007 SHOULD); that a label names the definition its values follow is INV-111 | no |
| INV-011 | a completeness indicator for each period of a summary measure, each referenced value, each adherence window and the special views | content (presence) | no |
| INV-020 | the treated-attack duration label | content (annotation) | no |
| INV-035 | series in the view; covered period = span of the series; the four measures per period; markers in the view; a marker for every event | content (co-presence, alignment, coverage; the review: OUT-009); the identity of a marker is INV-036 | no |
| INV-042 | definition labels and referenced codes of the three-month view | content | no |
| INV-050 | (above) | the withdrawal tie is identity; the rest is content | tie: yes, to INV-113 |
| INV-052 | worsening label | content (annotation) | no |
| INV-060 | a residual burden next to each percentage change, with its two values in the view | content (presence, co-presence; `rb.change = ch` selects the witness); the identity of a residual burden is INV-061 | no |
| INV-062 | (above) | the treatment tie is identity; the rest is content | tie: yes, to INV-114 |
| INV-066 | adherence next to the comparison, over an evaluation window (`adherenceFor`) | content (presence; which window, OUT-039 "over the evaluation window"); the identity of an adherence summary is INV-067 | no |
| INV-069 | the further dimensions for the same periods, where provided | content (presence) | no |
| INV-070 | (above) | seven identity conjuncts; presence and values are content | identity: yes, to INV-112 |
| INV-072 | outcomes for the time point; all treated attacks listed (`#s.sequence = s.treatedAttacks`); intake timing and results per line; outcomes and lines in the view; every formulation of the drug named | content (presence, coverage, co-presence); the identity bounds of the lines and outcomes are INV-074 (`#s.sequence ≤ s.treatedAttacks`, drug, period, formulation) | no |
| INV-073 | 15 minutes for summaries of cluster attacks only, 2 hours otherwise | content (which time point is reported, OUT-023 SHOULD); the outcome time point equals the summary's by INV-074 (definitional), so no shown value is false | no |
| INV-076 | symptom status in each line, for migraine | content (presence) | no |
| INV-078 | group roles, one group per class, groups and lines in the view, line role and class equal to the group's, chronological order, each line in one group | content. The review set this aside: these realise "(and, separately, acute)", "grouped by drug class" and "chronological" (OUT-024 SHOULD), and lines can only be placed in `ClassGroup`s, so a definitional form would make the grouping required of every history | no |
| INV-109 | every dose change shown; response summaries and adherence in the line's view; an acute summary over the span of the course; adherence over an evaluation window of the comparison | content (coverage, co-presence, which period, which window); the identity ties of the line's references (treatment, drug) are INV-079, and the start bound of the adherence window is INV-067 | no |
| INV-090 | the two trigger caveats | content (annotation) | no |
| INV-092 | (above) | the component ties are identity; the rest is content | ties: yes, to INV-115 |
| INV-093 | headache days of the same period with an AUC that is a primary measure for tension-type headache | content (presence) | no |
| INV-097 | equal lengths in every comparison that reaches into childhood | content (OUT-036 (c) SHOULD) | no |
| INV-098, INV-099, INV-100 | supportive-information caveat; interpretive caveats; clinical-interpretation caveat | content (annotation) | no |
| INV-104 | the components of the clinician-facing summary (`concise`, frequency measures, time course with `fillsPeriod`, markers, medication days, overuse indicators, comparisons with adherence, acute summaries, lines, instruments, functional impact) | content (presence, coverage, alignment; witnesses only) | no |
| INV-105 | the components of the patient-facing overview (`plainLanguage`, the four measures, the series, the treatment effect, a cycle line) | content (presence; witnesses only) | no |
| INV-016, INV-017, INV-018, INV-019, INV-022, INV-025, INV-026, INV-027, INV-029, INV-034, INV-039, INV-049, INV-071, INV-077, INV-081, INV-083, INV-088, INV-094, INV-095, INV-096, INV-103 (21 SHOULD, repertoire) | availability of outputs, with witness selectors | content (availability) | no |
| INV-013, INV-021, INV-043, INV-065, INV-084, INV-091, INV-101, INV-107 (8 SHOULD NOT) | `¬` a claim (or, for INV-091, a primary role for migraine) | content (negative forms of SHOULD parts and Caveats); no identity conjunct | no |

**Result.** The four invariants of the remark are the only SHOULD invariants with conjuncts that state what their element is. For every other kind of element whose ties the review lists, those ties are already definitional:
- E-034: INV-036;
- E-042: INV-058;
- E-044: INV-061;
- E-047: INV-067;
- E-051 and E-052: INV-074;
- E-053: INV-075;
- E-055: INV-079;
- E-065: INV-110.

**Noted, not changed:**
1. **The periods of a responder or non-responder label.** They are bound by no definitional invariant. In a MUST-conformant output, a label may refer to a month before its treatment started, as it may refer to one after a stop. This is not a conjunct of a SHOULD invariant: in a fully conformant output it follows from INV-062's coverage conjunct together with INV-056 (MUST). Fix 18 decided it with reasons when it chose the second option of R18-01 for these labels: "A definitional bound on every label would exclude an optional label that Stage 1 does not forbid. It would also need the start bound for every label, which then duplicates INV-064's start tie". The oscillation check after iteration 24 assesses that change as convergent, and the responder-label ties stay under watch (iteration-16 watch point 4, carried into the watch lists of the checks after iterations 24 and 28). INV-063 decides no component for such a label, so the label states no classification that the values force. It is not reopened here; it would be a new decision on a point that fix 18 argued, not a move of a SHOULD conjunct.
2. **The components of an index that does not concern migraine.** E-033 asks for no components there: OUT-037 asks for them only for migraine, and for tension-type headache only for the headache days next to AUC (INV-093). No invariant states their tie at any level, so stating it would add a constraint, not move one, and would change the fully conformant outputs. INV-115 keeps the scope of INV-092, as the review allows.

## Other changes

**Bookkeeping:**
- header: "Version: v31 · Iteration: 31 · Status: under review";
- section 9: "(as of v31)";
- section 11: an iteration-31 entry (no web search, no download, no new source; the scripts and the review's context; the Stage 1 fragments added);
- section 12: the v31 entry (2026-10-22).

**Items changed (diff v30 → v31, `itemdiff27.py`): 25.**
- **4 new invariants:** INV-112, INV-113, INV-114, INV-115.
- **17 content items changed:**
  - E-008, E-012, E-033, E-039, E-046, E-049;
  - INV-001, INV-050, INV-062, INV-070, INV-092, INV-097, INV-103;
  - rows OUT-017, OUT-020, OUT-022, OUT-037.
- **4 bookkeeping items:** the header and sections 9, 11 and 12.
- **Not changed:**
  - no element added, withdrawn or renumbered, and no invariant withdrawn or renumbered;
  - no element Definition, no Meaning, and no Realises field of an existing item;
  - no Elements column of the traceability table;
  - no source, value, axiom, conformance level of an existing invariant, attribute level or `when` clause.
- `git diff --stat` of OUTPUT_MODEL.md: 93 insertions, 34 deletions.

## Checks

| Check | Result |
|---|---|
| (i) The review's four outputs are rejected at every level (`false31.out`) | Under v30 each is MUST-conformant: every definitional, MUST and MUST NOT invariant over its atoms holds, and only INV-070, INV-050, INV-062 or INV-092 (SHOULD) fails. Under v31 each fails INV-112, INV-113, INV-114 or INV-115 (definitional), so it is neither MUST-conformant nor fully conformant.<br>**Each tie alone** (`equiv31.out`). Eight variants of output 1, each violating one tie of a view that meets every conjunct, fail INV-070 in v30 and INV-112 in v31, while v31's INV-070 holds:<br>• an event the context does not have;<br>• a treatment never stopped;<br>• a dose increase;<br>• a baseline on treatment;<br>• an on-treatment period after the stop;<br>• a period after the event that contains a day on treatment;<br>• periods after the event that are not consecutive;<br>• periods after the event that begin after the first day off treatment. |
| (ii) The fully conformant outputs are unchanged (`equiv31.out`, `blockcheck31.out`) | **INV-070 (v30) ⇔ INV-070 ∧ INV-112 (v31):** 1,200,000 random post-stop views in 30,000 admissible contexts (chains of resumed courses, starts stated or not, stops, pauses, reductions, increases, target-dose dates), 0 mismatches; 17,605 views are fully conformant in both.<br>**INV-050 ⇔ INV-050 ∧ INV-113:** 54 enumerated cases, 0 mismatches.<br>**INV-062 ⇔ INV-062 ∧ INV-114:** 208 enumerated cases, 0 mismatches. The equivalence rests on `comparison : opt`: with two comparisons, outside the typing, 36 cases differ.<br>**INV-092 ⇔ INV-092 ∧ INV-115:** 4,932 enumerated cases, 0 mismatches, 2,192 of them for indices that concern migraine.<br>**Formally:** every moved conjunct is verbatim and in one place, and every kept one is verbatim in its source (`blockcheck31.out`). ∀ distributes over ∧, and for INV-062 an `opt` attribute has at most one member. Every other invariant is byte-identical, so the conjunction of all invariants, and with it the set of fully conformant outputs, is unchanged. The MUST-conformant outputs narrow by exactly the outputs that violate a moved tie; v30 had no definitional invariant on these four ties. |
| (iii) Nothing becomes unsatisfiable (`equiv31.out`) | **Full conformance.** By (ii), every repertoire that was fully conformant in v30 is fully conformant in v31, so no requirement becomes unsatisfiable.<br>**INV-103.** In 20,000 random admissible contexts (30 % with a subject who is a child on some dates), each of the 37,063 views that INV-103 asks for was constructed as the INV-070 Notes describe: periods after the event from the first changed day, an on-treatment period where asked, and a baseline before the original start where stated, all of one length. All 37,063 meet INV-070, INV-112 and INV-097 (equal lengths) together. The on-treatment period was asked for and shown in 33,888 views, and the baseline in 25,832.<br>**INV-049.** Every view that INV-049 asks for has `v.withdrawalStart = ws` for a start `ws` of the subject, so it meets INV-113.<br>**Labels and indices** are optional. A label of a treatment can show that treatment's response comparison, which INV-055 requires wherever the start is stated (INV-114). An index can show components of its own period and scope (INV-115). |
| Headings and IDs (`mech31.py`) | 67 elements (E-001 to E-067) and 115 invariants (INV-001 to INV-115), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn). No dangling E-, INV-, ISS- or source reference; 37 source IDs cited, all within S-001–S-046 or S-101–S-106. Every OUT reference exists in Stage 1. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full", covering all 39 Stage 1 requirements. The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. INV-113 is in row OUT-017, INV-114 in OUT-020, INV-112 in OUT-022 and INV-115 in OUT-037. |
| Types and names (`names27.py`, `tokcheck27.py`) | 750 declared names, none declared twice; no new name. The token report is identical for v30 and v31: 106 flagged tokens, each a declared attribute. Every type used is defined. The new invariants use only declared types, attributes, predicates and functions: `PostStopMonitoringView`, `WithdrawalFollowUpView`, `ResponderLabel`, `CompositeIndex`, `eventOn`, `originalStart`, `courseBegunBy`, `firstChangedDay`, `consecutive`, `concerns`. The partial term `first(v.after)` stays guarded by `v.after ≠ ∅ ⇒`. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 38 (34 + 4). Every MUST NOT and SHOULD NOT predicate has the form `¬ F`, and every invariant states its scope (output for the four new ones). 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged, with no typing-rule violation. Each new invariant is definitional for its element (E-049, E-039, E-046, E-033), as section 3.3 (5) requires. |
| Diff of formal blocks (`omndiff27.py`, `blockcheck31.py`) | 182 `omn` blocks in v30, 186 in v31.<br>• Changed: INV-050, INV-062, INV-070, INV-092. New: INV-112, INV-113, INV-114, INV-115.<br>• The other 178 blocks are equal in order (SHA-256). Among them, byte-identical: section 2.8, E-008, E-033, E-039, E-046, E-049, INV-001, INV-036, INV-049, INV-051, INV-063, INV-064, INV-097 and INV-103.<br>• Line-level, the changed blocks differ from v30 only by the moved conjuncts, the copied `∀ v` / `∀ x ∈ firstChangedDay(…)` binders and the trailing `∧` / `)`.<br>• Protected-tie counts in the formal text, v30 → v31, unchanged: `notStoppedBefore(` 6, `intervalOnTreatment(` 6, `evaluatedOnTreatment(` 4, `courseBegunBy(` 6, `originalStart(` 4, `resumesFrom(` 3, `courseOverlaps(` 4, `courseNotOutside(` 4, `summarisesMedication(` 11, `sameSpan(` 30, `sameIndicatedPeriod(` 7, `onlyOfType(` 6, `next(p.end)` 3, `eventOn(` 7, `∃ s ∈ startOf(` 4, `∀ s ∈ startOf(` 1, `consecutive(` 5, `rc.treatment = L.treatment` 10, `plusDays(x, −1)` 1, `first(v.after).start = x` 1.<br>• `firstChangedDay(` grows from 4 to 5, because INV-070 and INV-112 both bind it. |
| Quotes (`quotes31.py`) | 45 quoted fragments on changed lines. Every source quote is verbatim in Stage 1 v18 or already in v30. The OUT-020 quote of INV-114 has an omission `[...]`; its two fragments ("If the output displays a responder or non-responder label, it SHOULD name the criterion applied" and "and SHOULD always show the underlying values (OUT-018, OUT-019)") are each verbatim in OUT-020, the omitted text being the parenthesis of example criteria. No source quote was changed. |
| Scope sweep (`scope27.py`) | Term counts v30 → v31 are equal except four, each read in context:<br>• "stor" (+1): `history/v30.md` in the search-log entry;<br>• "taken" (+1): "Not taken.";<br>• "states" and "stated": "the context states".<br>The E-033 sentence "computed from diary information and is out of scope" is on a changed line but is unchanged. No new text describes input, storage or a derivation from input. The new invariants take as arguments only output elements and context properties that the model already uses as such (`ctx.subject.preventiveTreatments`, course events, `originalStart`, `ctx.subject.withdrawalStart`, `concerns`). |
| Snapshot and files | `cmp OUTPUT_MODEL.md history/v31.md`: identical. `history/v30.md` and everything under `docs/stage1-output-requirements/` are unchanged (equal to HEAD). Only `OUTPUT_MODEL.md`, `history/v31.md` and this log were written. |
