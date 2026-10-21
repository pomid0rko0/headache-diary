# Fix log — iteration 11
Input review: reviews/review-iter-11.md · Input version: v10 · Output version: v11
Date: 2026-10-21

## What was downloaded and checked

**Nothing was downloaded, and no quote was added or changed.** The three remarks concern the formal model: co-presence in a view, the quantifier of a presence requirement, and the range of a context component. They were verified against the Stage 1 v18 text in the repository and against v10 itself (`history/v10.md`, byte-identical to the input OUTPUT_MODEL.md). Two new Evidence lines reuse fragments of quotes that the model already gives and that review 11 verified (370 of 370 fragments):
- [S-010] "for three months, with a satisfactory response to acute treatment", from the optimal-control quote in E-046 (INV-062, E-045);
- [S-104] "ranged from 0 to 21 for anxiety and 0 to 21 for depression", from the quote in E-059 (INV-083).

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3;
- v10;
- review 11.

**Earlier loop files read so that no fix is undone:**
- review 03 "Checked and not raised" ("Co-presence of response-comparison values", "Treatment-history groups");
- review 04 (INV-050 note on INV-049);
- review 06 ("Co-presence through INV-003");
- fix logs 05 (the R05-01 sweep, INV-049 and INV-050) and 10 (level sweep; the E-032 basis wording);
- the oscillation check after iteration 08 and its eight watch points.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**Scripts.** All are in the session scratchpad (`fix11/`) and were run with `python3 -I`:
- `refs.py` lists every reference attribute (53);
- `scen11.py` is an instance check of the four R11-01 scenarios;
- `mech.py`, `names.py` and `scope.py` are the mechanical checks;
- `diffitems.py` lists the changed items and the watch-point status against v10.

### Verification of the remarks

**R11-01 holds for (c) and (d), but not for (a) and (b).**
- **(a) and (b) are already required at MUST.** `scen11.py` rejects the review's (a) scenario in both possible forms:
  - The values in view B refer to the comparison's own period atoms. Then INV-003 fails, because "MMD Mar in B refers to period Mar(A) shown in A".
  - The values in view B have their own period atoms with the same dates. Then INV-056 fails, because `m.period ∈ {rc.baseline} ∪ ran rc.onTreatment` is false.
- **Why this follows.** A period is an item, and every item is part of exactly one view (section 2.5). By INV-003, the period that an item refers to is in that item's view. So two items that refer to the same period atom are in one view.
  - The values of a response comparison refer to its period atoms (INV-056, MUST), so they are in its view. Each of its changes is shown with its two values (INV-054, MUST), so the changes are in that view too.
  - The (b) scenario fails in the same way, through INV-038 (definitional) with INV-003.
  - The consequences that the review lists also hold. A responder label's comparison (INV-062) and the overview's treatment effect (INV-105) bring their values with them, and the residual day counts follow through INV-061.
- **Earlier reviews.** Review 03 ("Co-presence of response-comparison values ... necessarily in the comparison's view ... No gap") and review 06 ("Co-presence through INV-003 ... This confirms review 03") stated the same.
- **The real point in (a) and (b).** The model did not say this anywhere. So a reader of the model, the reviewer included, could take the Readings "side by side" and "showing the values" as unsupported by the predicates.
- **(c) and (d) hold.**
  - A treatment marker refers to no period.
  - Outcome summaries and treated-attack lines refer to no period.
  - No v10 invariant places them in the holder's view. `scen11.py` admits both scenarios.

**R11-02 holds.** In the review's example (sumatriptan and ibuprofen, an "optimal control" label over three months), one ibuprofen summary for the first month satisfies the v10 conjunct (`scen11` evaluation). `periodValuesOf(acuteTreatmentSummaries)` and `typeValuesOf` have the same ∃-per-period gap.

**R11-03 holds.** 15 August 2026 (a Saturday) to 20 October 2026 (a Tuesday) is 67 days.
- It is not a run of calendar months.
- 67 is not a multiple of 28 or of 7.
- So no admissible context has it as its time range, and v10 INV-094 never requires a summary for it.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R11-01 | partly fixed: (c) and (d) fixed as the review proposes; (a) and (b) declined as formal changes, because the co-presence is already required at MUST, and the consequence is now stated explicitly | (c) INV-035 (Predicate, Reading, new Notes); E-034 and E-035 Conformance; row OUT-009.<br>(d) INV-072 (Predicate, Reading, Realises +OUT-021, Evidence, new Notes); E-051 (Conformance, Notes); E-052 and E-053 Conformance; INV-069 and INV-071 Readings; rows OUT-021 and OUT-023.<br>(a)/(b) INV-003 (new Notes); section 2.5 (References); INV-037, INV-038 and INV-056 Readings; INV-054 Notes; INV-056 Evidence and new Notes; E-037 and E-043 Conformance and Notes; rows OUT-001, OUT-010, OUT-018, OUT-020 and OUT-035 | **(c)** New conjunct `(∀ mk ∈ v.markers • mk ∈ v.content)` in INV-035 (SHOULD, the level of OUT-009: "as a time series [...] with dated markers").<br>**(d)** New conjuncts `(∀ os ∈ s.outcomes • os ∈ viewOf(s).content) ∧ (∀ l ∈ ran s.sequence • l ∈ viewOf(s).content)` in INV-072 (SHOULD). The review's first option was chosen:<br>• The co-presence holds for every summary. The outcome measures and per-attack lines are what a summary reports (OUT-023: "report, across the attacks treated with it, the outcome measures"; "show how consistently ...").<br>• Every view that shows a summary therefore shows its effectiveness. This covers the treatment review view (INV-069, OUT-021: "the same view SHOULD also include [...] the effectiveness of acute treatment"), INV-071, INV-104, INV-105, INV-062 and INV-109.<br>• OUT-021 is added to INV-072's Realises.<br>**(a) and (b): why no formal change.**<br>• The values of a response comparison or period comparison refer to its period atoms (INV-056 MUST, INV-038 definitional). INV-003 (MUST) places those atoms in the comparison's view, and every item is part of exactly one view.<br>• So the values are in the comparison's view, at MUST, the level of OUT-018 and OUT-001. The changes follow by INV-054 (MUST).<br>• The review's counter-example fails INV-003 or INV-056 (verification above). Reviews 03 and 06 reached the same conclusion.<br>• Adding the review's conjuncts would duplicate a consequence of INV-003 with INV-038, INV-054 and INV-056.<br>**What was added instead.** The consequence is now written down:<br>• the INV-003 Notes state the derived property `∀ x, y : Item; p : Period • p ∈ refs(x) ∩ refs(y) ⇒ viewOf(x) = viewOf(y)` and its uses;<br>• section 2.5 points to it;<br>• the Readings and Notes of INV-037, INV-038, INV-054 and INV-056, and of E-037 and E-043, state the co-presence and its basis.<br>So the "side by side" of E-037 and the INV-037 Reading, and "showing the values" in E-043, are visibly backed by predicates. No predicate of INV-037, INV-038, INV-054 or INV-056 changed.<br>**Oscillation.** INV-104 and INV-105 are untouched (watch point 7). The R10b-01 restriction of INV-054 is unchanged. |
| R11-02 | fixed: the review's option (a) | INV-062 (Predicate, Reading, Evidence, Notes); E-045 (Meaning, Notes); E-046 Conformance; row OUT-020 | **Predicate.**<br>• `u = acuteTreatmentEffectiveness` now requires `∀ p ∈ ran L.evaluated; am ∈ ctx.subject.acuteMedications • ∃ s ∈ L.otherValues ∩ AcuteTreatmentSummary • s.period = p ∧ s.drug = am.drug`.<br>• For `periodValuesOf(k)` and `typeValuesOf((k, h))`, the case `k = acuteTreatmentSummaries` requires a summary of each acute medication for the baseline and each evaluated period, with the same type scope as before (`allTypes`, or `scopeFor(ctx, s.typeScope, h)`). Every other kind keeps its v10 conjunct, guarded by `k ≠ acuteTreatmentSummaries`.<br>**Basis.**<br>• OUT-020 refers to "the effectiveness of acute treatment in OUT-023", which OUT-023 reports "For each acute medication".<br>• The optimal-control level of [S-010] holds "for three months, with a satisfactory response to acute treatment" (fragment of the E-046 quote).<br>• INV-069 and INV-071 already treat the same values per drug and per period.<br>**Satisfiability.**<br>• The summaries refer to the evaluated periods and the baseline. INV-003 already places these in the label's view, through the label and its comparison.<br>• A summary may have 0 treated attacks (INV-072, INV-074).<br>• INV-011 and INV-073 hold.<br>**Oscillation (watch point 5).** The fix only tightens presence:<br>• `#L.evaluated = 1` (4 occurrences) is unchanged;<br>• the `evaluationResult` / `pretreatmentBaseline` pair is unchanged;<br>• `rc.treatment = L.treatment` is unchanged, and gains one further occurrence (see Other changes 2);<br>• the open `UnderlyingKind` and `PeriodValueKind`, with `otherValueNamed`, are unchanged;<br>• INV-063 decides nothing on acute values (fix 09), so no category is forced or excluded. |
| R11-03 | fixed: the review's option (a) | E-007 (Definition: new component `chosenPeriod : opt DateSpan`; Meaning); INV-001 (Predicate, Reading, Realises +OUT-034, Evidence, Notes); INV-094 (Predicate, Reading, Evidence, new Notes); E-066 (Meaning, Conformance); section 4 (item 1); row OUT-034 | **Context.** `chosenPeriod` is a period chosen by the clinician for the clinician-facing summary. INV-001 bounds only its end, by the as-of date. It is not subject to the whole-period condition of the selected time range, because OUT-034 places no condition on "a period chosen by the clinician".<br>**INV-094** gains the conjunct `(∀ r ∈ c.chosenPeriod • ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ ClinicianSummary • sameSpan(v.covers, r))`.<br>**Kept.** The v10 conjunct for the selected time range stays, read as a time range that the clinician reader selects. Removing it would change v10 without need.<br>**Why option (a) rather than (b).** The chosen period belongs to the context, as the compared periods, the previous consultation and the scheme windows do. Option (b) would make every span a requirement of every context, without recording which period the clinician chose.<br>**INV-104** is unchanged (watch point 7; its v02 condition and v03 tie are kept). It applies to any covered period, as its Notes show: 15 August – 20 October gives two 28-day periods with 11 days left over, and nine whole Monday-weeks; checked by script.<br>**Text.** E-007 states which context components are subject to the whole-period condition. The INV-001 Notes list the components that are not. |

## Other changes

### 1. Same-view sweep (R11-01 class)

**Method.**
- `refs.py` listed every element attribute whose type mentions `→`: 53 reference attributes.
- For each, I read the Stage 1 statement of the output it belongs to and looked for a co-presence word ("side by side", "next to", "together", "in the same view", "alongside", "with", "in", "the list ... show").
- Where Stage 1 asks for co-presence, I checked that an invariant at the level of that Stage 1 part places the referenced item in the holder's view, directly or through the shared-period consequence of INV-003.
- I also re-read the invariants that place non-reference items together (INV-011, INV-027, INV-028, INV-066, INV-068 to INV-071, INV-083, INV-093, INV-104, INV-105). Each places its items in one view.

**Result.** Three gaps beyond R11-01 (c) and (d), all fixed:
- the groups and lines of the treatment history;
- the response summaries of a treatment line;
- the adherence of a treatment line.

| Reference attribute(s) | Co-presence asked by Stage 1 | Invariant (level) | Result |
|---|---|---|---|
| The 17 period references: `View.covers`, `Series.periods`, `PeriodValue.period`, `MedicationOveruseIndicator.period`, `.span`, `PeriodComparison.periods`, `WithdrawalFollowUpView.reviewWindow`, `ResponseComparison.baseline`, `.onTreatment`, `ResponderLabel.evaluated`, `AdherenceSummary.window`, `TreatmentReviewView.baseline`, `.onTreatment`, `PostStopMonitoringView.baseline`, `.onTreatmentPeriod`, `.after`, `SchemeWindowView.windows` | OUT-001 "Every summary output MUST state the reporting period it covers" | INV-003 (MUST) | already required |
| `Annotation.qualifies` | the labels and caveats of OUT-011, OUT-016, OUT-017, OUT-032, OUT-036, OUT-037 and OUT-038, shown with what they qualify | INV-007 (definitional) | already required |
| `CompositeIndex.components` | OUT-037 "shown together with its component measures" | INV-092 (SHOULD) | already required |
| `TimeCourseView.series` | OUT-009 "as a time series" | INV-035 (SHOULD) | already required |
| `TimeCourseView.markers` | OUT-009 "with dated markers" | none in v10 → INV-035 (SHOULD) | **fixed (R11-01 (c))** |
| `PeriodComparison.values` | OUT-001 "comparison of periods"; OUT-010 "comparison between periods"; side by side (E-037) | INV-038 with INV-003 (MUST) | already required; now stated (R11-01 (b)) |
| `ThreeMonthPatternView.series` | OUT-028 "a view of headache days and migraine days for each of the most recent three" | INV-041 (definitional) | already required |
| `WithdrawalFollowUpView.series` | OUT-017 "show headache days and acute medication days from the start of withdrawal onward" | INV-050 (SHOULD) | already required |
| `MedicationOveruseIndicator.basis` | none: OUT-016 asks for the indication with the levels and the span, which the indicator shows (fix 10) | — | no change. The basis is in the indicator's view anyway, because `basis(j).period = span(j)` (INV-045) and INV-003 apply. |
| `Change.reference`, `.compared` | OUT-018, for the changes of a response comparison (MUST). OUT-019 asks only for the residual burden next to other percentage changes (fix 10). | INV-054 (MUST) | already required |
| `ResponseComparison.values`, `.changes` | OUT-018 "showing both the values of each period and the absolute and percentage change from baseline" | INV-056 with INV-003; INV-054 (MUST) | already required; now stated (R11-01 (a)) |
| `ResponseComparison.timePoints` | OUT-018 "at the evaluation time points" | INV-059 (MUST) | already required |
| `ResidualBurden.change`, `.migraineDays`, `.moderateSevereHeadacheDays` | OUT-019 "next to it" | INV-060 (SHOULD); the day counts also through INV-061 with INV-003 | already required |
| `ResponderLabel.comparison`, `.residual`, `.otherValues` | OUT-020 "show the underlying values [...] and [...] those values as well" | INV-062 (SHOULD) | already required |
| `AcuteTreatmentSummary.outcomes`, `.sequence`; `OutcomeSummary.summary` | OUT-023 (the summary reports the outcome measures and the consistency across consecutive treated attacks); OUT-021 "the same view SHOULD also include [...] the effectiveness of acute treatment" | none in v10 → INV-072 (SHOULD). `OutcomeSummary.summary` follows from INV-074 with INV-072. | **fixed (R11-01 (d))** |
| `TreatmentHistoryView.preventiveGroups`, `.acuteGroups`; `ClassGroup.lines` | OUT-024 "a chronological list of preventive (and, separately, acute) treatments [...] grouped by drug class"; "the list SHOULD also show the formulation" | none in v10 → INV-078 (SHOULD) | **fixed (sweep)** |
| `TreatmentLine.preventiveResponse`, `.acuteResponse` | OUT-024 "treatments with [...] the response summary from OUT-018 or OUT-023 for each treatment"; OUT-034 "current and past treatments with response" | none in v10 → new INV-109 (SHOULD) | **fixed (sweep)** |
| `TreatmentLine.adherence` | OUT-039 "The adherence output SHOULD also be available in the treatment history (OUT-024) and in the clinician-facing summary (OUT-034)" | none in v10 for the history → INV-109 (SHOULD); the clinician-facing summary already had it (INV-104) | **fixed (sweep)** |
| `InstrumentResult.baselineResult` | none: OUT-026 asks for "the change from the baseline administration", an attribute of the result (review 11, not raised) | — | no change |
| `MenstrualRelationView.cycles`; `CycleLine.attacks` | OUT-030 "show migraine attacks and migraine days in relation to the days of menstruation across consecutive cycles" | INV-087 (definitional) | already required |
| `ClusterView.bouts`, `.remissions`, `.rates`, `.acute`; `ClusterAttackRate.bout` | none: OUT-031 lists what to report ("report: [...]; [...]; and [...]") without asking for one view, and the rate is "during active periods" (review 11, not raised) | — | no change |

**About the treatment history.** Review 03 noted that the groups and lines "may be shown in another view of the same output", and that "OUT-024 requires no co-presence with other content". That note was not raised as a remark, and fixed nothing.
- The sweep reads OUT-024 itself: the history is "a chronological list" which "SHOULD also show" the details of each treatment, "with [...] the response summary [...] for each treatment". Its groups and lines are therefore the content of the history view, as the cycle lines are the content of the menstrual-relation view (INV-087).
- Co-presence with other content, which review 03 addressed, is still not required.

**New INV-109 (SHOULD; OUT-024, OUT-034, OUT-039).** A new invariant was added because the conjuncts concern every treatment line, wherever it is shown: in the history, the clinician-facing summary and a scheme-window view. The history view and its structure are the subject of INV-078.

### 2. Presence-quantifier sweep (R11-02 class)

**Method.**
- I took every Stage 1 statement part with "for each", "each", "every", "per", "where available", "where provided", "where reported", "Wherever" or "in each of these periods", together with the model's own phrase "in the evaluated periods".
- For each, I checked that the model requires the content for every relevant item (each drug, period, type, instrument, event, symptom, domain, subscale), and not for some one item.

**Result.** Four gaps beyond R11-02, all fixed:
- the instrument result at the evaluation;
- the formulations of a summary of all formulations;
- every dose change;
- the HADS subscales.

| Stage 1 part | Required for | Model (v10) | Result |
|---|---|---|---|
| OUT-001 "Every summary output" | each view | INV-003 ∀ v | ok |
| OUT-003 "Each reporting period" | each period with a measure | INV-011 ∀ m | ok |
| OUT-004 to OUT-008, OUT-010, OUT-011, OUT-015, OUT-027, OUT-028, OUT-036 (b) "per reporting period", "for every period in the selected time range" | each period | `perPeriod` ∀ p (INV-014 to INV-019, INV-022, INV-023, INV-025, INV-026, INV-040, INV-096, INV-108) | ok |
| OUT-009 markers "for the start, dose change and stop" | each event | INV-035 ∀ e | ok |
| OUT-012 the three symptoms; "in the response of individual treated attacks" | each symptom; each line | INV-022 ∀ s; INV-076 ∀ l ∀ a | ok |
| OUT-014 "by drug class [...] and by individual drug" | each class and drug | INV-023 ∀ m | ok |
| OUT-016 "per reporting period, per acute medication class" | each period and class, and combined use | INV-044 ∀ p ∀ s | ok |
| OUT-018 "For each preventive treatment"; "the values of each period"; "evaluation time points"; "where reported" | each treatment, period, measure and applicable time point | INV-055 ∀ t ∀ r ∀ a; INV-056 ∀ k ∀ p; INV-057; INV-059 ∀ r ∀ a | ok |
| OUT-019 "Wherever the output shows a relative (percentage) change" | each such change | INV-060 ∀ ch | ok |
| OUT-020 effectiveness of acute treatment | each acute medication, in each evaluated period | ∃ one summary | **fixed (R11-02)** |
| OUT-020 per-period values: acute-treatment summaries | each acute medication, for the baseline and each evaluated period | ∃ one summary per period | **fixed (R11-02)** |
| OUT-020 results of instruments and of PGIC | each instrument, with its result at the evaluation ("in the evaluated periods") | ∀ instrument, but any result of it; the evaluation result was required only for score components (R05-02) | **fixed (sweep).** Where a result completed after the treatment start within the last evaluated period is available, INV-062 requires the latest such result (`evaluationResult`) for every instrument the criterion rests on, for example PGIC under IHS Q6. |
| OUT-020 changes of reduction measures; score pairs; control-level counts | each measure and evaluated period; each component; each evaluated month | INV-062 ∀ | ok |
| OUT-021 "for the same [...] periods"; "the most recent results"; "in each of these periods" | each period, instrument and acute medication | INV-068, INV-069 ∀ p ∀ i ∀ am | ok |
| OUT-022 "stopped, paused or reduced" | each event | INV-103 ∀ e | ok |
| OUT-023 "For each acute medication"; the outcome measures; "for the same attacks"; "For the treated attacks it summarises"; "for each formulation"; baseline and on-treatment periods | each medication, measure, attack, formulation and period | INV-071 ∀ m ∀ p; INV-072 ∀ k ∀ l | ok |
| OUT-023 "state the formulation or route of administration [...] of each acute medication it summarises" | each formulation that a summary of all formulations covers | `formulations` only non-empty | **fixed (sweep).** INV-072 now requires, for `allFormulations`, every formulation of the drug in `acuteMedications`. |
| OUT-024 the treatments listed | each treatment | INV-077 ∀ t | ok |
| OUT-024 "dose changes" | every dose change of each treatment | `doseChanges` only non-empty | **fixed (sweep).** INV-109 adds the first conjunct; INV-079 already made every shown change a real course event. |
| OUT-024 "the response summary [...] for each treatment"; "the formulation of each treatment" | each treatment | E-055 attributes | ok |
| OUT-026 "Where results of validated instruments are available" | each available result | INV-081 ∀ a | ok |
| OUT-027 three domains, severe impairment | each domain | INV-026, INV-027 ∀ d | ok |
| OUT-029 "separately for each headache type"; intensity "where provided" | each type | INV-028 ∀ sc; INV-029 ∀ t | ok |
| OUT-031 "for acute treatments, effectiveness at 15 minutes and the need for rescue"; "attacks per day and per week during active periods" | each acute medication; each bout and rate basis | INV-088 ∀ m; ∀ b ∀ k | ok |
| OUT-031 bouts and remissions; "the history of previous bouts" | each bout | `bouts` non-empty | no change. Which bouts exist is not a context property, and requiring all of them would be a derivation from input (section 1, item 3). |
| OUT-033 "Where results [...] are available [...] with instrument name, date and score" | each available result, with its score: for HADS, its two subscale scores ([S-104] in E-059) | `scores` only non-empty | **fixed (sweep, INV-083)** |
| OUT-034 the components | each started preventive treatment, acute medication, treatment, result and monthly period | INV-104 ∀ | ok |
| OUT-035 "treatment effect" | not stated per treatment ("an understandable overview [...] treatment effect"; contrast OUT-018 "For each preventive treatment" and OUT-023 "For each acute medication") | INV-105 ∃ one item | no change. The per-treatment outputs are required by INV-055 and INV-071, and INV-105 is watch point 7. |
| OUT-036 (a) PedMIDAS | each available result | INV-096 ∀ a | ok |
| OUT-037 "together with its component measures" | each dimension | INV-092 ∀ d | ok |
| OUT-038 "Summary outputs"; the indicators | each view; each indicator | INV-099, INV-100 ∀ | ok |
| OUT-039 "For each preventive treatment [...] next to the response comparison" | each comparison | INV-066 ∀ rc | ok |

### 3. Context-range sweep (R11-03 class)

**Method.** I checked every component of `OutputContext` and `SubjectProfile` (E-007, E-008), and every conjunct of INV-001. For each, I asked whether it keeps an output that Stage 1 asks for or permits out of the required (or admitted) outputs.

**Result.** One gap beyond R11-03: the running withdrawal follow-up. It is fixed.

| Context restriction | Outputs that depend on it | Result |
|---|---|---|
| `timeRange`: whole periods of `granularity`, ending on or before `asOf` (INV-001) | (1) The outputs given "for every period in the selected time range" (OUT-004 and the INV-014 family), whose series tile the range: ok.<br>(2) OUT-034, "a period chosen by the clinician": **R11-03**.<br>(3) OUT-017, "from the start of withdrawal onward": **gap**. INV-049 required views only for whole-period ranges from the start of withdrawal. With 28-day periods from 10 March and an as-of date of 21 April (day 43, inside the NICE 1.3.48 window of 7 April to 5 May), the longest required view ended on 6 April. With calendar months and a mid-month start, no view was required at all. E-039 already admitted a covered period ending on the as-of date. **Fixed:** INV-049 also requires the view from the start of withdrawal to the as-of date, while the as-of date lies within the following year.<br>(4) OUT-035 (INV-095) and OUT-030, OUT-031, OUT-023 (INV-071): these name no period, and their views admit any covered period: ok.<br>(5) OUT-026 and OUT-033 (INV-081, INV-083): every result date d ≤ asOf lies in the admissible 28-day range ending on d: ok. |
| `granularity` ∈ {calendar month, 28-day period, calendar week} | the periods Stage 1 names (OUT-001, OUT-009, OUT-015) | ok |
| `comparedSpans`: any spans up to `asOf` | OUT-001, OUT-010 (INV-037, INV-039) | ok |
| `previousConsultation`: one date up to `asOf` | OUT-034 "the period since the previous consultation" (the latest one) | ok |
| `chosenPeriod` (new): any span up to `asOf` | OUT-034 | new (R11-03) |
| `schemeSelection`: one scheme with any windows | OUT-025 (MAY) | ok |
| `audience`: one per output | OUT-034, OUT-035 | ok |
| `weeklyGranularityRelevant` forced for tension-type and cluster headache | OUT-009 | it only adds requirements: ok |
| `headacheTypes` ⊆ `possibleHeadacheTypes`; no listed type a subtype of another | OUT-029; `hasType` uses ⊑ | a subject is described by its most specific types: ok |
| preventive and acute treatments disjoint | a course is one or the other; one drug may appear in two courses | ok |
| every preventive treatment has a guidance type and is given for a type the subject has or may have; adult ⇒ aged 12 or older | E-041 applicability (watch point 2) | unchanged |
| course events up to `asOf`; at most one start; nothing before the start | OUT-009, OUT-018, OUT-022, OUT-024; a restart is a new course | ok |
| every acute medication has an ICHD-3 8.2 class | `otherMedication` covers the rest | ok |
| `withdrawalStart`: at most one date, up to `asOf` | OUT-017 speaks of "the start of withdrawal" of a patient who is withdrawing | ok |
| instrument and screening results up to `asOf`; `menstruates`; `ageGroup` | OUT-026, OUT-030, OUT-033, OUT-036 | ok |

### 4. Satisfiability pass

**Method.** For every changed or added invariant and attribute, I built a construction by hand (dates checked by script) together with the invariants that constrain the same elements and views. No MUST or SHOULD combination is unsatisfiable in an admissible context, and no derived attribute is required where its relation is undefined. No new derived attribute was added.

- **INV-035 with INV-003, INV-011, INV-034 and INV-036.**
  - Markers refer to no period, so they add no period or completeness obligation.
- **INV-072 with INV-069, INV-071, INV-073, INV-074, INV-062, INV-088, INV-104, INV-105 and INV-109.**
  - Outcome summaries and lines refer to no period. INV-074 already keeps the lines within the summary's period.
  - A summary with 0 attacks shows its outcome summaries with 0 assessed and no lines.
  - The formulation conjunct applies only to `allFormulations`. INV-071 sets no formulation for those summaries, and INV-074 limits only `singleFormulation`.
- **INV-062 with INV-003, INV-011, INV-072, E-058 and INV-082.**
  - The per-drug summaries refer to the evaluated and baseline period atoms, which are already in the label's view, through `L.evaluated` and `rc ∈ viewOf(L).content`.
  - The evaluation result is an available result with that completion date.
  - INV-063 is unaffected.
- **INV-078, INV-109 and E-055 with INV-077, INV-079, INV-003, INV-011, INV-055 to INV-057, INV-059, INV-060, INV-066, INV-067, INV-097, INV-104 and the scheme-window view.**
  - A response comparison with 28-day periods meets its MUST content in any view, including the history view.
  - The line's adherence summary can be the one that INV-066 asks for, with a window that ends with an on-treatment period.
  - In the clinician-facing summary, the lines refer to the comparisons, summaries and adherence that INV-104 already shows there. An acute line whose drug is no longer among `acuteMedications` can refer to a summary with 0 attacks.
  - Every shown dose change is a course event (INV-079), and every course event is shown (INV-109). Course events form a set, so there is at most one per date and kind.
- **INV-083 with INV-085.** HADS shows two subscale scores, each once and each ≤ 21.
- **INV-094 and INV-001 with INV-104, INV-003 and INV-011.**
  - The chosen period of 15 August – 20 October has two 28-day periods with 11 days left over, and nine whole Monday-weeks.
  - INV-104's construction covers any covered period.
- **INV-049 with INV-050, INV-051, INV-052 and INV-003.**
  - The start of withdrawal lies on or before the as-of date (INV-001).
  - For the view of 10 March – 21 April: a 28-day series of 10 March – 6 April fills it, and no review window is required yet (5 May > 21 April).
  - Review 06 checked follow-up views of 10, 40 and 70 days.

### 5. Levels and paraphrases

- **No MUST was added.** Every new or changed constraint is SHOULD, like the Stage 1 parts it realises:
  - INV-035 (OUT-009);
  - INV-049 (OUT-017);
  - INV-062 (OUT-020);
  - INV-072 (OUT-021 SHOULD component; OUT-023);
  - INV-078 (OUT-024);
  - INV-083 (OUT-033);
  - INV-094 (OUT-034);
  - INV-109 (OUT-024, OUT-034, OUT-039).

  INV-001 stays definitional for contexts.
- **The co-presence stated for (a) and (b)** is that of INV-003 (MUST, OUT-001), together with INV-056 and INV-054 (MUST, OUT-018) and INV-038 (definitional). For an intensity comparison (OUT-010, SHOULD), the comparison itself stays SHOULD (INV-039). The MUST is the structural one of a period shown in the view of every item that refers to it (section 3.3, items 3 and 5).
- **Prose against formal text.** Every Reading, Meaning, Conformance, Notes and row text that I changed was compared with its predicate or declaration. Two drafting errors were corrected before the final version:
  - a parenthesis in the E-046 Conformance;
  - a claim in the INV-003 Notes that response summaries "refer to no period". The text now says that they share no period with the treatment line.
- **Coverage texts.** No coverage text names an ID outside its row. Four draft references to INV-003, INV-038 and INV-072 in rows OUT-010, OUT-018, OUT-020 and OUT-035 were replaced by element references within the rows, or by plain text.

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 109 invariants (INV-001 to INV-109). None missing, none duplicated. |
| References | No dangling E-, INV- or ISS- reference (ISS-07 appears only as withdrawn). S references lie in S-001–S-046 and S-101–S-106, each S-1NN with a row in section 10. OUT references lie in 001–039. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025). Exactly one Realises field per item. Each row's element and invariant columns equal the union of the Realises fields: INV-001 +OUT-034; INV-072 +OUT-021; INV-109 → OUT-024, OUT-034 and OUT-039. No coverage text names an ID outside its row. All rows say "full". |
| `omn` names | Every capitalised name is declared or primitive, except bound variables (`A`, `D`, `K`, `Ks`, `L`) and the level keywords. Every selection `e.a` names a declared attribute or component, including the new `chosenPeriod`. The new terms were type-checked by hand: `sameSpan(Period, DateSpan)`, `viewOf(Item)`, `evaluationResult(L, r)`, `doseChange(k)` with `k : DoseChangeDirection`, and `{anxietySubscale, depressionSubscale}`. `last(L.evaluated)` is guarded by `seq1`. |
| Levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48 (v10: 47; +INV-109), SHOULD NOT 8, definitional 32; total 109. Every MUST NOT and SHOULD NOT predicate begins with `¬`. Attribute declarations: 172 (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. |
| Scope sweep | Whole document searched for enter, entry, record, input, captur, logged, store, storage, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field, "diary data" and questionnaire. Every occurrence was read in context. They are exclusion statements, out-of-scope notes, Stage 1 wording, verbatim quotes, instrument names, document-structure words ("Conformance field", "change-log entry") and the search-log tool description ("full-text XML"). The counts equal those of v10, and no changed line contains any of these words. |
| Watch points (oscillation/check-after-iter-08.md) | **Byte-identical to v10:** E-008, E-013, E-041, E-042, E-060, E-061, INV-050, INV-055, INV-058, INV-059, INV-063, INV-064, INV-087, INV-100, INV-104 and INV-105.<br>**Explanatory text only:** E-039 (Conformance; the covered-period and series tie is unchanged), E-043, E-045 and E-046.<br>**Formal additions only:**<br>• INV-001: the `chosenPeriod` bound. The R01-02 fallback type, R06-01 population and R02-01 event order are unchanged.<br>• INV-062: the per-drug acute conjuncts and the evaluation result. `#L.evaluated = 1` 4 → 4; `rc.treatment = L.treatment` 9 → 10; `evaluationResult(L, r)` 4 → 5; `pretreatmentBaseline(L, b)` 4 → 4; `otherValueNamed` unchanged.<br>**Unchanged values:** `excludes` (17 values), rule timings, `fillsPeriod` and `containsPeriodOf`. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v11.md`: identical. |
