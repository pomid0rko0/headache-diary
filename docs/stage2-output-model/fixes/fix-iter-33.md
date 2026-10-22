# Fix log — iteration 33
Input review: reviews/review-iter-33.md · Input version: v32 · Output version: v33
Date: 2026-10-22

## What was read and checked

**Read:**
- PROCESS.md, in full (scope exclusions of section 2, notation of section 3, fidelity and evidence of section 4, structure of section 6, identifiers of section 7, frozen items of section 10, practical notes of section 11).
- Stage 1 v18: sections 1 and 2, and the Statement of every requirement OUT-001 to OUT-039. Read in full, with Evidence basis, quotes and Caveats: OUT-001, OUT-010, OUT-011, OUT-012, OUT-021, OUT-026, OUT-033, OUT-034 and OUT-035.
- v32 (`OUTPUT_MODEL.md`, byte-identical to `history/v32.md`):
  - sections 1 to 4 in full;
  - every formal (`omn`) block of sections 2, 3, 5 and 6, that is, all 67 elements and all 117 invariants;
  - the prose fields of E-006, E-012 to E-014, E-023 to E-026, E-030 to E-033, E-045, E-047, E-050, E-051, E-057 to E-059, INV-006, INV-012, INV-018 to INV-022, INV-029, INV-031 to INV-033, INV-037 to INV-039, INV-069, INV-081 to INV-085, INV-096, INV-097, INV-100 and INV-105;
  - traceability rows OUT-010, OUT-012, OUT-020, OUT-021, OUT-022, OUT-026, OUT-033 and OUT-035; ISS-06; section 9; the iteration-32 entries of sections 11 and 12.
- Review 33 (two remarks) and fix 32 (where `onSameScale` and `inSameForm` were introduced, with its same-defect tables).
- The oscillation check after iteration 32, with its watch points: 1 (identity ties, INV-082 availability), 2 (named criteria) and 3 (comparability: dropping the conjuncts would be a reversal). The watch-point block lists of the checks after iterations 16, 24 and 28, and iteration-12 watch point 2 (responder labels).
- Earlier positions on the points changed, found by searching all reviews, fixes and oscillation checks:
  - `publishedGrading`: R03-07 and fix 03 (PGIC left unfixed), R19c-01 and fix 19 (the basis of the HALT-30 lower bound), and fix 32's sweep, which counted it as "used";
  - `OtherInstrumentName`: fix 03 and review 04 ("the Meaning fixes the semantics");
  - `compositeIndicesOf`: fix 08, which introduced `PeriodValueKind`.

  No loop file discusses `otherIntensitySummary`, `otherPresenceSummary` or `otherHeadacheIndex` with two different other forms or indices.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**No download and no web search.** The fix adds no fact, value or source. The only quotes added are fragments of the Stage 1 text of OUT-026, checked by script.

**Scripts.** All are in a fresh scratchpad folder, `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix33r/`, and were run with `python3 -I`. A previous, lost attempt at this fix had left three scripts in `…/scratchpad/fix33/`; they were read and not used.
- `lib33.py`: the library.
  - It extracts the `omn` blocks by item.
  - It transcribes, in their v32 and v33 forms: `onSameScale` and `inSameForm`; INV-032; the symptom conjuncts of INV-033; the comparison witness of INV-039; the intensity and symptom conjuncts of INV-069; the series-intensity conjunct of INV-105 (with `perPeriod` of E-006); INV-082; the `category` presence constraint of E-058; and, for composite indices, `valueOfKind` of E-045 with INV-062's per-period ask.
- `verify33.py` (`verify33_v32.out`): asserts 24 fragments of the transcribed predicates verbatim in their v32 blocks and reproduces the review's examples under v32.
- `sweep33.py` (`sweep33_v32.out`, `sweep33_v33.out`): the R33-02 sweep. It traces every constant and function to the invariants, `where` clauses and comprehension types that use it, directly or through other declared names, and lists those that only `when` clauses use.
- `check33.py` (`check33.out`): checks (i) to (iii) on v33.
  - It asserts the v33 transcriptions verbatim.
  - It asserts that the blocks using the changed predicates are byte-identical.
  - It asserts that INV-082 differs from v32 by exactly one added line.
- `apply33.py` builds the v33 body from `history/v32.md` by 24 exact replacements, each asserted to occur once. `entry33.py` adds the section 11 and 12 entries.
- `blockcheck33.py` (`blockcheck33.out`): a line-level diff of every changed `omn` block, the byte-identity of the watch-point blocks, and counts of protected and tie terms.
- `quotes33.py` (`quotes33.out`): every quoted string on a changed line, checked against Stage 1 v18 or found unchanged in v32.
- Copies of fix 32's check scripts, read before use: `mech31.py`, `mech_r32b.py`, `names27.py`, `tokcheck27.py`, `omndiff27.py`, `itemdiff27.py` and `scope27.py`.

### Verification of the remarks under v32 (`verify33_v32.out`)

**R33-01 holds.**
- **The example.** A comparison of January and March 2026 (31 days each), both on the 0–10 numerical rating scale. January shows `otherIntensitySummary("median peak intensity 6")`, and March shows `otherIntensitySummary("severe pain on 30 % of headache days")`.
  - `onSameScale` holds, and INV-032 holds for both summaries.
  - The comparison meets the witness of INV-039, the intensity conjunct of INV-069 (the two months as baseline and on-treatment periods) and the series conjunct of INV-105.
- **The control.** R32b-03's mean of 6.0 on the numerical scale against a distribution over a four-level verbal scale is rejected by INV-039.
- **Symptoms.** "nausea on 40 % of headache days" against "nausea in 3 of 5 attacks" meets `inSameForm` and the symptom conjunct of INV-069. Days against attacks, the control, is rejected.

**R33-02 holds.**
- **The example.** A HALT-30 result with total score 12, recall `recallMonths(1)`, an available administration and `category = {publishedCategory("Moderate")}` meets every conjunct of INV-082. E-058 places no constraint on it, because its `when` clause `publishedGrading(halt30)` is false.
- **The contrast.** The same result showing the HALT-90 band "Moderate" (11–20) is rejected. The same result with `publishedCategory("Grade III")` is admitted.
- **Uses.** `publishedGrading` occurs only in the `when` clause of `E-058.category` (`sweep33_v32.out`).

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R33-01 | fixed: the review's option (a) | **Changed:**<br>• E-023 (Definition, Meaning, Notes);<br>• E-025 (Definition, Meaning, Notes);<br>• INV-039 (Notes), INV-069 (Notes);<br>• rows OUT-010, OUT-021, OUT-035 | **Definitions.**<br>• New value type (E-023): `value OtherSummary { form : Text; value : Text }`, where `form` is the kind of summary as the output names it.<br>• `otherIntensitySummary ⟨OtherSummary⟩` (E-023) and `otherPresenceSummary ⟨OtherSummary⟩` (E-025).<br>• `onSameScale` gains `(∀ x₁, x₂ : OtherSummary • i₁.summary = otherIntensitySummary(x₁) ∧ i₂.summary = otherIntensitySummary(x₂) ⇒ x₁.form = x₂.form)`.<br>• `inSameForm` gains the same conjunct, for `presence` and `otherPresenceSummary`.<br>• Both predicates now hold only for summaries in one form, among the other forms too, and stay equivalence relations (reflexive, symmetric and transitive by script). The "and so with each other" of INV-039 therefore still holds.<br>• Forms are compared by equality, as texts are (section 2.8). This is the convention by which the model identifies instruments and criteria by the names it states for them (E-045 Notes).<br>**Invariants.** INV-039, INV-069 and INV-105 are byte-identical. Through the predicates, they now admit compared summaries only in one form, as their Readings already state ("on one scale and in one form").<br>**Text.**<br>• E-023 and E-025: the comments and Meanings read "or both of the same other form", and a sentence introduces `OtherSummary`.<br>• E-023 Notes: other forms state their form, and two other forms are not one form.<br>• E-025 Notes: two other forms cannot be compared either, for example the share of headache days and the share of attacks with the symptom.<br>• Notes of INV-039 and INV-069; rows OUT-010, OUT-021 and OUT-035: "summaries in other forms only where they state the same form".<br>• The Readings of INV-039, INV-069 and INV-105 were already true of the tightened predicates and are unchanged. So are the INV-105 Notes ("share the scale and the form of one intensity summary").<br>**Level:** SHOULD, unchanged (OUT-010, OUT-021 and OUT-035 are SHOULD). No form is fixed; the form remains the diary's choice.<br>**Not a reversal** (watch point 3 of the check after iteration 32): the conjuncts of fix 32 are verbatim, and one conjunct is added in the same direction. INV-018, INV-029 and the values of INV-062, which fix 32 declined to tie, are unchanged. |
| R33-02 | fixed: the review's conjunct (the general form, not the HALT-30-only variant) | **Changed:**<br>• INV-082 (Predicate, Reading, Evidence, Notes);<br>• E-057 (Notes);<br>• E-058 (Conformance, Notes);<br>• row OUT-026 | **INV-082** gains `(∀ cat ∈ r.category • publishedGrading(r.instrument))`. A grade or category is shown only for an instrument whose developer publishes a grading or categories, so never for HALT-30, whatever the form of the category. INV-082 is definitional, like its band ties: the category is "the instrument's own published grading or categories" (OUT-026; E-058 Meaning), and HALT-30 has none ([S-014] "Grading is not used by HALT-30.", quoted in Stage 1 OUT-026).<br>**Why the general form.** It ties every fixed value of `publishedGrading`, not only HALT-30's. For the instruments where the model leaves `publishedGrading` unfixed (MSQ v2.1, M-TOQ, PGIC and other instruments), it reads as "a category only where the instrument's own publication has one". That follows the existing E-057 Notes ("it follows those instruments' own publications") and R03-07's decision for PGIC, and it changes no axiom.<br>**Text.**<br>• INV-082 Reading: no category for an instrument without a published grading, such as HALT-30.<br>• INV-082 Evidence: Stage 1 OUT-026 "the instrument's own published grading or categories" and the [S-014] sentence.<br>• INV-082 Notes: a paragraph **Grading**, with the satisfiability argument.<br>• E-057 Notes: `publishedGrading` decides both whether a category is asked for (E-058) and whether one may be shown (INV-082). The sentence "INV-082 constrains the results of other instruments only by …" now names this tie, so that the paraphrase stays true.<br>• E-058 Conformance and Notes ("Relations").<br>• Row OUT-026.<br>**Unchanged:** the E-057 and E-058 blocks (no axiom, value, `when` clause or level), and the availability conjuncts of INV-082 added by fix 32 (watch point 1 of the check after iteration 32). |

## Same-defect checks

### R33-01: open-ended "other" variants treated as one case by a comparison, equality or same-kind test

Every variant tag or enumeration constant of the model whose name begins with `other` was listed from the `omn` blocks, together with `OtherItem`, `recallAsPublished`, `publishedCategory`, `judgement` and `otherValueNamed`. Each was read against every predicate that compares or classifies its values. The blocks that use each element kind were also listed: for example IntensitySummary in E-011, E-023, E-033, E-045, INV-018, INV-029, INV-032, INV-039, INV-069 and INV-105.

| Variant | Test that could lump it | v32 | Result |
|---|---|---|---|
| `otherIntensitySummary ⟨Text⟩` (E-023) | `onSameScale` (INV-039, INV-069, INV-105) | every other form is one form | **the remark; fixed** |
| `otherPresenceSummary ⟨Text⟩` (E-025) | `inSameForm` (INV-069) | every other form is one form | **the remark; fixed** |
| `otherHeadacheIndex` (E-033, a constant with no payload) | `valueOfKind(m, compositeIndicesOf(ik))` (E-045, through `x.index = ik`), used by INV-062's per-period ask and by `valueAvailable` | Every index other than the AUC is one kind. A label whose criterion rests on `periodValuesOf(compositeIndicesOf(otherHeadacheIndex))` meets INV-062 with index Y for the baseline and index Z for the evaluated period (`verify33_v32.out`). Yet E-045 says that `PeriodValueKind` names "composite indices of each kind (E-033)" | **Genuine instance; fixed.** `variant HeadacheIndexKind ::= areaUnderHeadacheCurve \| otherHeadacheIndex ⟨Text⟩`, the index by the name the output shows for it (E-033 Definition and Meaning). E-045's block and text are byte-identical, and its claim "of each kind" is now true. INV-093 (`x.index = areaUnderHeadacheCurve`) and INV-091, INV-092 and INV-115 do not depend on which other index is shown. Unlike R33-01's forms, these are different measures, not forms of one measure. So this is not the extension to INV-062's values that fix 32 declined (a form or scale tie on intensity), and `PeriodValueKind` stays open (R08b-01) |
| `otherInstrument ⟨OtherInstrumentName⟩` (E-057), `otherScreeningInstrument ⟨OtherScreeningName⟩` (E-059) | instrument equality in INV-062, INV-069, INV-081, INV-082, INV-085, `scoreMet`, `evaluationResult` and `valueAvailable` | the name payload tells instruments apart | not an instance. Review 04 settled that a named instrument shown under another name, and likewise a screening instrument shown as an `Instrument`, is excluded by the Meaning |
| `otherCompletenessExpression ⟨Text⟩` (E-013) | INV-012 | INV-012 compares only the numeric forms: "An `otherCompletenessExpression` is worded text and is not compared" | not an instance: left out of the comparison, not lumped |
| `otherStatistic` (E-024, a constant) | `statistic` is tested only for `total` (INV-033); `durationSummariesOf ⟨DurationKind⟩` is by kind, not statistic | no test equates two other statistics; no requirement compares durations across periods (OUT-011 is per period, and OUT-021 does not list duration) | not an instance |
| `otherCaregiverImpact ⟨Text⟩` (E-031) | INV-033 tests `caregiverLostProductiveDays` only; INV-096 asks per period; `caregiverImpacts` is a kind | no comparison across periods (OUT-036 (b) asks for reporting) | not an instance |
| `otherAdherenceStatement ⟨Text⟩` (E-047) | INV-066, INV-067, INV-104, INV-109 (presence and window only) | no comparison of values | not an instance |
| `otherNonPainSymptom ⟨Text⟩` (E-026) | INV-022, INV-069 (presence per period) | the payload names the symptom; no comparison | not an instance |
| `otherStopReason ⟨Text⟩` (E-055), `judgement ⟨Text⟩`, `otherValueNamed ⟨Text⟩` (E-045), `recallAsPublished ⟨Text⟩`, `publishedCategory ⟨Text⟩` | INV-079 (a stop reason only where stopped); `showsValueNamed`; INV-082 (recall for the tabulated instruments; band versus published category) | each carries its text, and no test equates two different texts | not an instance |
| `otherMedication` (E-028) | `ofClassUse(otherMedication)`, `classCode` | one class by definition: ICHD-3 8.2.8, "one or more medications other than those described above" | not an instance |
| `otherPreventive` (E-008) | `appliesTo` of the evaluation rules (E-041) | one guidance type by definition: "a preventive treatment that none of the other values describes" (E-008 Notes). Only rules for all preventive types name it | not an instance |
| `otherSpan` (E-005) | `sameIndicatedPeriod` (E-032) compares `kind` only together with the dates (and INV-045 makes indicator periods monthly) | two other spans with the same dates are the same span | not an instance |
| `OtherItem` (E-004) | none (open world, section 3.7) | — | not an instance |

### R33-02: value-set facts of axioms and comments that no invariant enforces (`sweep33_v32.out`)

Every `const` and `fun` of the model was traced, directly or through other declared names, to the invariants, `where` clauses and comprehension types that use it (102 names, 15 axioms, 32 `when` clauses):

| Name(s) | Use | Result |
|---|---|---|
| `publishedGrading` | the E-058 `when` clause only | **the remark; fixed (INV-082)**. It is the only fixed value-set fact that only a `when` clause uses. In v33 it is enforced by INV-082 (`sweep33_v33.out`) |
| `scoreRange` (HIT-6 36–78; MIDAS, PedMIDAS, HALT-90 and HALT-30 from 0), `wholeNumberScores`, `publishedRecall` (3 months, or 1 month for HIT-6 and HALT-30), `gradeBands`, `banded`, `inBand` | INV-082 | enforced |
| the HADS, PHQ-9 and GAD-7 subscales and ranges (stated in INV-085 and E-059 Evidence; `Subscale`) | INV-085; INV-083 asks for both HADS subscales | enforced |
| `instrumentName`, `screeningName`, `label` (E-009) | display functions: the attribute holds the instrument or code, and its shown name is a function of that value (fix 32). The script reaches `label` only through the axiom that also fixes the code constants | not a value set that a shown value can contradict |
| `minutes`, `hours` | library constructors of `Duration` (section 2.8) | not a source value set |
| every other `const` and `fun` (evaluation rules, overuse codes and levels, `overuseSpanMonths`, the review-window weeks, `followUpMonths`, the window days of A1.1, `remissionMoreThanMonths`, `shortestMonthlyDays`, `requiredOutcomes`, the named criteria, the code hierarchy `⊑`, `classCode`, `classesOf826`, `classesOf821to825`) | reached from invariants (INV-009, INV-010, INV-045, INV-046, INV-049, INV-051, INV-055, INV-058, INV-072, INV-087, INV-089, INV-116, …) | enforced |

**Comments of the `omn` blocks that state a value-set or structural fact** were read one by one. Each is enforced:
- the indicator period, a calendar month or 28-day period (E-032): INV-045;
- the baseline month (E-043): INV-056;
- the three most recent monthly periods (E-038): INV-041;
- day 1 ± 2 (E-060): INV-087;
- 15 minutes and rescue (E-062): INV-088;
- the NICE 1.3.48 window (E-039): INV-051;
- the event kinds of post-stop monitoring (E-049): INV-112;
- "at most one member" (E-008, E-014): INV-001, INV-006.

The unit comments ("unit: days", "score points") fall under rule U1 (section 2.7), not a value set.

**Facts stated only in prose, checked:**
- **HURT's areas.** The model describes them ("no concern" or one of three flagged areas, E-057 Notes; ISS-06) and does not tabulate them. HURT is among the instruments whose categories are shown "as published" (E-057 Meaning), and the model states no labels against which a shown category could be tested. `publishedGrading(hurt)` is enforced by the new conjunct in the direction that matters: a category may be shown. Not an instance.
- **MSQ v2.1, M-TOQ and PGIC.** `publishedGrading` is unfixed for them by design (R03-07). The new conjunct ties them to their own publications without fixing a value.
- **"A depression or anxiety screening instrument is a `ScreeningInstrument` (E-059), not an `Instrument`"** (E-057 Meaning). Review 04 settled that the Meaning fixes this semantics for an instrument shown under another name, and the E-057 value sets are long settled. Not reopened.

## Other changes

**Bookkeeping:**
- header: "Version: v33 · Iteration: 33 · Status: under review";
- section 9: "(as of v33)";
- section 11: the iteration-33 entry (no web search, no download, no new source);
- section 12: the v33 entry (2026-10-22).

**Items changed (diff v32 → v33, `itemdiff27.py`): 16.**
- **12 content items:**
  - 5 elements: E-023, E-025, E-033, E-057, E-058;
  - 3 invariants: INV-039, INV-069, INV-082;
  - 4 rows: OUT-010, OUT-021, OUT-026, OUT-035.
- **4 bookkeeping items:** the header and sections 9, 11 and 12.
- **Not changed:**
  - no element or invariant added, withdrawn or renumbered;
  - no Realises field, and no Elements or Invariants column of the traceability table;
  - no source, value, axiom, `when` clause, level-annotated attribute declaration, or level of an invariant.
- `git diff --stat` of OUTPUT_MODEL.md: 39 insertions, 26 deletions.

**Watch points kept** (oscillation checks after iterations 12, 16, 24, 28 and 32; `blockcheck33.out`):
- **Checks 16 and 24.** All 50 watch-point blocks are byte-identical, among them E-045, E-046, INV-062, INV-063, INV-069 and INV-105.
- **Check 28.** All 12 treatment-course blocks are byte-identical.
- **Check 32.** The blocks named in watch points 1 to 3 are byte-identical except E-023 and E-025 (watch point 3, one conjunct added in the direction of the v32 tie) and INV-082 (watch point 1, one conjunct added; the availability conjuncts are verbatim). The 14 blocks checked are INV-027, INV-039, INV-069, INV-105, INV-112 to INV-117, INV-085, E-057, E-058 and E-059.
- **Protected terms.** The counts are unchanged except `publishedGrading(` 7 → 8. For example: `onSameScale(` 5, `inSameForm(` 3, `rc.treatment = L.treatment` 10, `#L.evaluated = 1` 4, `conditionHolds(` 12, `instrumentAdministrations` 16, `allTypes` 105.
- Row OUT-021 is listed among the watched rows of `itemdiff27.py`. Its only change is the comparability phrase of R33-01, the same clause that fix 32 added.
- **Direction.** Every admitted set narrows or stays equal. No fix is reversed.

## Checks

| Check | Result |
|---|---|
| (i) The review's examples (`check33.out`) | Under v33, each is rejected:<br>• the January–March comparison (median peak intensity against the share of headache days with severe pain), by INV-039, by the intensity conjunct of INV-069 and by the series conjunct of INV-105;<br>• nausea as a share of headache days and as a count of attacks, by the symptom conjunct of INV-069;<br>• the HALT-30 result with `publishedCategory("Moderate")`, by INV-082 (definitional, so at every level).<br>The same HALT-30 result without a category meets INV-082. The same comparison with a median peak intensity in both months (6 and 5) meets INV-039 and INV-032.<br>**Further instance:** the label showing index Y and index Z for a criterion that rests on index X fails INV-062's ask; showing X for both periods meets it. |
| (ii) Truthful, fully conformant v32 outputs stay fully conformant (`check33.out`) | **R33-01.** 30,000 random configurations: 2 to 4 periods; intensity summaries as distributions, means and three other forms; scales NRS, VRS or none; symptom summaries as days, attacks and two other forms.<br>• The v33 conjuncts (INV-039 witness, INV-069 intensity and symptoms, INV-105 series) admit only what v32 admits: 0 exceptions.<br>• 908 conjunct verdicts change. Every one comes from a configuration with two or more different other forms.<br>• On all 16,267 configurations whose other-form summaries state one form per dimension, the verdicts are equal: 0 differences.<br>• A v32 output whose `otherIntensitySummary` or `otherPresenceSummary` shows a form maps to v33 by stating that form. Only outputs that compare two different forms lose conformance, and these are what the remark rejects.<br>**R33-02.** 153,600 enumerated results: 10 instruments; scores, categories (none, three published categories and all 16 tabulated bands) and recalls; 16 assignments of `publishedGrading` to MSQ v2.1, M-TOQ, PGIC and another instrument.<br>• v33 admits only what v32 admits.<br>• 5,664 results are rejected by v33 alone, each showing a category for an instrument without a published grading. Among them, for each assignment, are the 66 HALT-30 results that show a category and meet v32.<br>• No result that shows a category only where the instrument publishes one is lost.<br>**Composite indices.** A label that shows the index its criterion rests on, for every period, meets INV-062 as in v32. |
| (iii) Nothing becomes unsatisfiable (`check33.out`) | **Intensity and symptoms.** One summary per period in any one form, whether distribution, mean or a single other form, on either scale, meets INV-032 together with the conjuncts of INV-039, INV-069 and INV-105. Symptom summaries all as days, all as attacks or all in one other form meet INV-033 and INV-069. The two predicates are equivalence relations.<br>**Instrument results.** For every instrument and every assignment of `publishedGrading`, there is a result that meets INV-082 (v33) and the category ask of E-058: a band containing the score, a published category, or no category where there is no grading.<br>• E-058 asks for a category exactly where `publishedGrading` holds, and the new conjunct then holds.<br>• INV-100 mentions `r.category` only as an antecedent, and no other invariant mentions it, so none asks for a category elsewhere.<br>• The results that INV-062, INV-069, INV-081, INV-096 and INV-104 ask for need no category.<br>**Composite indices.** Labels and indices are optional. A criterion that rests on another index X can be met by showing X for every period, where the diary provides X (`valueAvailable`). |
| Headings and IDs (`mech31.py`, `mech_r32b.py`) | 67 elements (E-001 to E-067) and 117 invariants (INV-001 to INV-117), none missing, none duplicated.<br>Issues: ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn).<br>References: no dangling E-, INV-, ISS- or source reference. 37 source IDs are cited, all within S-001–S-046 or S-101–S-106. Every OUT reference exists in Stage 1. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field. Every invariant has exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full", covering all 39 Stage 1 requirements.<br>The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Types and names (`names27.py`, `tokcheck27.py`) | 754 declared names (752 in v32). The new names are the value type `OtherSummary` and its component `form`; `value` was already an attribute name. None is declared twice.<br>The token report is identical for v32 and v33: 106 flagged tokens, each a declared attribute.<br>Every type used is defined.<br>• `OtherSummary` is declared in E-023 and used in E-025.<br>• `otherHeadacheIndex ⟨Text⟩` is a tag of the variant `HeadacheIndexKind`; INV-093's `areaUnderHeadacheCurve` stays a constant tag.<br>• `x₁` and `x₂` are bound variables; `₁` and `₂` are listed subscript digits (section 2.2).<br>No partial term is added. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 40, all unchanged. Scopes: output 84, repertoire 32, context 1.<br>Every MUST NOT and SHOULD NOT predicate has the form `¬ F`, and no repertoire or context invariant uses a bare `ctx`.<br>172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged, with no typing-rule violation.<br>INV-082 stays definitional (E-057, E-058). INV-039, INV-069 and INV-105 stay SHOULD, the strength of OUT-010, OUT-021 and OUT-035. |
| Diff of formal blocks (`omndiff27.py`, `blockcheck33.py`, and an inline script for the order) | 188 `omn` blocks in v32 and in v33.<br>• Changed: E-023, E-025, E-033 and INV-082.<br>• New: none.<br>• The other 184 blocks are byte-identical, in the same order (checked by position).<br>**Line-level changes:**<br>• E-023: the `otherIntensitySummary` tag; the new `OtherSummary` declaration (two lines with its comment); the comment "or both of the same other form"; one added conjunct of `onSameScale`.<br>• E-025: the `otherPresenceSummary` tag; the comment; one added conjunct of `inSameForm`.<br>• E-033: `enum` → `variant`, with `otherHeadacheIndex ⟨Text⟩`.<br>• INV-082: one added line. |
| Quotes (`quotes33.py`) | 19 quoted strings on changed lines.<br>• 15 are found verbatim in Stage 1 v18, including the new OUT-026 fragments "the instrument's own published grading or categories" and "Grading is not used by HALT-30.". Two of the 15 are words of the change-log entry, not quotations.<br>• The other 4 are unchanged v32 quotes on lines that changed elsewhere (E-057 Notes: "minimal or infrequent disability", "11–20", "≥20", "whole days per one or 3 months").<br>No source quote was changed. |
| Scope sweep (`scope27.py`) | Term counts v32 → v33 are equal except two, each read in context:<br>• "stor" +1: `history/v32.md` in the search-log entry;<br>• "states" +5: "states that form", "state the same form".<br>The other hits on changed lines are unchanged text of those lines: the E-057 Notes on derivation from answers being out of scope, and "taken during" in row OUT-035.<br>No new text describes input, storage or a derivation from input. The new relations take as arguments only output elements (the shown forms of summaries, the shown category and instrument of a result, the shown index) and the fixed value-set function `publishedGrading`. |
| Snapshot and files | `cmp OUTPUT_MODEL.md history/v33.md`: identical.<br>`history/v32.md`, PROCESS.md and everything under `docs/stage1-output-requirements/` are unchanged (equal to HEAD).<br>Only `OUTPUT_MODEL.md`, `history/v33.md` and this log were written. |
