# Fix log — iteration 08
Input review: reviews/review-iter-08b.md · Input version: v07 · Output version: v08
Date: 2026-10-21

## What was downloaded and checked

**Frozen items and watch points.** FROZEN_ITEMS.md does not exist, and the oscillation check after iteration 04 froze nothing, so no item is frozen. Its watch points (the start of the menstrual-relation view and the lead-in in INV-087; E-060, E-061 and INV-105; INV-104) are not touched: an item-level diff of v07 and v08 shows them unchanged.

**Earlier work read so that no fix is undone.** PROCESS.md; Stage 1 v18 (sections 1–3 in full); v07 in full; reviews 08 (NO_REMARKS) and 08b, and reviews 06 and 07 on E-041; the fix logs of iterations 01, 05 and 07; oscillation/check-after-iter-04.md. The guarantees of the earlier fixes are kept:
- **E-041 (R01-01, R01-02, R02-01, R06-01, R07-01, R07-02).** The 17 rule constants are byte-identical to v07 (checked by script), including every `excludes` value. Only a listed type excludes a rule, so the R01-02 guarantee holds. `fitsMonthlyPeriod`, the INV-055 guard and the INV-001 order of course events are unchanged (R02-01). Populations are unchanged (R06-01). The rule list is unchanged (R07-01). R07-02's exclusions of onabotulinumtoxinA are unchanged. NICE 1.3.27 still applies to onabotulinumtoxinA, the point that review 07 settled.
- **E-045, E-046 and INV-062 (R01-04, R05-02 and its sweep).**
  - Reduction components still decide only labels with a single evaluated period (`#L.evaluated = 1`), and only on the label's own comparison (`rc.treatment = L.treatment`).
  - Score components are still decided only on the `evaluationResult` / `pretreatmentBaseline` pair.
  - Control-level months still begin on or after the treatment start (INV-064 unchanged).
  - The 6 named criteria are byte-identical to v07.
  - The new attack-reduction component follows the same rules: one evaluated period, the label's own comparison, and counts that the label shows.

**Downloads.** All downloads went with `curl` into the fresh directory `/tmp/fix08-dl-7xav`, outside the repository, and all returned HTTP 200. PDFs were extracted with `pdftotext -raw` and `-layout`; web pages had their markup removed. Scripts were kept in the session scratchpad and run with `python3 -I`.
- **[S-035] Turkish Ministry of Health Migraine Clinical Protocol** (92-page PDF):
  - Kutu 8 (PDF p. 48): the second item is "Ölçüt atak sıklığında en az %50 azalma olması,"; the seventh item is the "Yeterli süre…" sentence.
  - Section 3.6.3.9 (PDF p. 57): "Hasta fayda görüyorsa enjeksiyonlar 3 ayda bir, hasta epizodik forma dönüşünceye dek devam edilmelidir.", two sentences before "Hastalar 3 enjeksiyon siklusu sonra değerlendirilmeli …".
  - Table 6 (PDF p. 52): "12 haftada bir".
- **[S-015] NICE CG150 Recommendations page** ("Last updated: 03 June 2025"):
  - 1.3.26 ends "For full details, see NICE's technology appraisal guidance on botulinum toxin type A (TA260, 2012)." The link goes to TA260.
  - 1.3.27–1.3.29 read as quoted.
- **NICE TA260** (new source **S-106**): the overview page ("Published: 27 June 2012"; "Last reviewed: 11 January 2016"), section 1 and section 2.
  - Section 1, recommendation 1.2: "less than a 30% reduction in headache days per month after 2 treatment cycles", which CG150 1.3.29 restates.
  - Section 2.1: "The recommended re-treatment schedule is every 12 weeks (see the summary of product characteristics)."
- **[S-018] AAN/AHS 2026 Clinician Summary** (12-page PDF): 14A, 14B and 14H read as quoted in Stage 1 and in E-041.

**Quote check.** All 30 double-quoted strings that are new in v08, outside the `omn` blocks, were checked by script after normalising whitespace, non-breaking spaces, quotes and dashes:
- 28 were found verbatim in the downloaded texts, in Stage 1 v18 or in v07;
- the other 2 are English translations.

**Verification of the remarks before fixing.** Both remarks hold.
- **R08b-01.**
  - OUT-020 gives the other values a criterion rests on as examples: "(for example the results of instruments and of patient global impression of change in OUT-026, or the effectiveness of acute treatment in OUT-023)".
  - In v07, `UnderlyingKind` had only the tags `instrumentResultOf` and `acuteTreatmentEffectiveness`, and `ReductionComponent.measures` could name only a `DayMeasure`.
  - So the Turkish Box 8 criterion could only be a `judgement` with `alsoRestsOn = ∅`, and INV-062 required no attack counts with it.
  - Stage 1 itself quotes criteria that rest on further values:
    - [S-035] section 3.6.2: attack frequency and duration, and the acute response;
    - [S-030]: frequency or intensity, and side effects;
    - [S-042]: attack duration;
    - [S-032]: attack frequency, duration, severity, functional impairment and the acute response.
- **R08b-02.**
  - The v07 criterion was "the types for which the same guidance names another time point". It contradicts `ruleNice1327.excludes = ∅`, because NICE names 1.3.28 and 1.3.29.
  - Read literally, it would also make every type-specific rule exclude its own type. For example, NICE 1.3.27 names a time point for CGRP inhibitors too, so `ruleNice1328` would exclude `cgrpInhibitor`.
  - The reason given for NICE ("names no exception") applies equally to Turkish Box 8, which v07 treats the other way.
  - The criterion that does produce the values was stated only in fix-iter-07.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R08b-01 | fixed: both parts of the review's required change (the set of other values is opened, and attack-frequency thresholds become a decidable component) | E-045 (Definition, Meaning, Evidence, Notes); E-046 (Definition, Conformance, Notes); INV-062 (Predicate, Reading, Evidence, Notes); INV-063 Reading; section 7 row OUT-020 | **Open set of other values (E-045).** `UnderlyingKind` gains two tags:<br>• `periodValuesOf ⟨PeriodValueKind⟩`. `PeriodValueKind` names the kinds of per-period value of the model on which a criterion can rest: `dayCountsOf ⟨DayMeasure⟩` (every day count, including acute-medication and functional-impact days), `eventCountsOf ⟨CountedEvent⟩` (attacks, auras), `intensitySummaries`, `durationSummariesOf ⟨DurationKind⟩`, `symptomPresenceOf ⟨AssociatedSymptom⟩`, `mostBothersomeSymptoms`, `caregiverImpacts`, `compositeIndicesOf ⟨HeadacheIndexKind⟩` and `acuteTreatmentSummaries`. The new predicate `valueOfKind(m, k)` relates a shown value to its kind. Three kinds are left out, with reasons in the Notes: completeness indicators, which every period shows anyway; marks of periods without migraine days, which restate a count of 0; and cluster attack rates, which restate an attack count within a bout.<br>• `otherValueNamed ⟨Text⟩`, for a value of any other kind, as the output names it. The given relation `showsValueNamed : Item × Text → 𝔹` says which item shows it, for example the treatment line with the adverse effects that [S-030] names.<br>The review's `ℙ PeriodValue` payload was not used: section 2.4 admits `ℙ` only for predicate parameters and semantic constants. An enumeration of kinds is typed in OMN and has the same reach.<br>**`valueAvailable`** gains `provides({m : PeriodValue \| valueOfKind(m, k)})` for per-period kinds and `provides({x : Item \| showsValueNamed(x, t)})` for other kinds, as the review proposed. Acute-treatment summaries also need a subject who uses acute medication.<br>**Comment of `alsoRestsOn`.** It now reads "the kinds of value on which the criterion also rests, besides the day counts and changes of the response comparison, the residual burden and the control-level count". The v07 wording ("values other than frequency") would now contradict the attack-count kinds.<br>**Attack-frequency thresholds.** The review's first option was taken: a new component `attackReduction ⟨AttackReductionComponent⟩` (`atLeastPercent`, `condition`). Its threshold is quoted from [S-035] Box 8 (E-045 Evidence).<br>• New predicates `attackReductionMet` and `attackReductionDecided` (E-046) test the attack counts that the label shows among its other values. The baseline count is that of the response comparison's baseline period; the evaluated count is that of the single evaluated period; both have one type scope. The test is `100 × (b − f) ≥ p × b`, with b > 0, on the shown counts.<br>• `componentMet` and `componentDecided` include the new component. The INV-063 predicate is unchanged; its Reading describes the component.<br>• The model still decides only what the shown values decide (R01-04 rule: one evaluated period only).<br>**`where` clause on `ResponderCriterion`.** A criterion lists the instrument of each score component, and the attack counts if it has an attack-reduction component. All 6 named criteria already satisfy it (checked).<br>**INV-062 (SHOULD), new conjuncts.**<br>(a) For each `periodValuesOf(k)` that the diary provides, the label shows values of kind k, of one type scope, for the baseline period of its comparison and for each evaluated period.<br>(b) For each `otherValueNamed(t)` that the diary provides, the label shows an item that shows it.<br>(c) Sweep, same element: for each reduction component that applies to the subject, the comparison shows, for each measure the diary provides, the change from the baseline for each evaluated period. In v07 nothing required a reduction measure other than headache, migraine and moderate/severe headache days (for example acute-medication days) to be shown.<br>**Intensity and duration thresholds** stay `judgement` components, and the E-045 Notes say why. The quoted criteria name no statistic, scale or form of summary on which a shown value could be tested: a halving of intensity ([S-030]); a 50 % reduction in duration ([S-035]); a significant decrease ([S-042]). Their values are declared with `periodValuesOf`, so INV-062 requires them with the label.<br>**Conjunctive criteria.** The Notes also state that a criterion whose parts must all be met is one `judgement` component, because components are alternatives. Examples are [S-035] 3.6.2 and [S-030].<br>**Example of the review (Turkish Box 8).** The criterion is now `attackReduction(50, anySubject)`, and its `alsoRestsOn` includes `periodValuesOf(eventCountsOf(attacks))`. INV-062 requires the attack counts of the baseline and evaluated months. INV-063 gives "responder" for 6 → 3 attacks and "non-responder" for 6 → 4 when Box 8 is the only component, and decides nothing for a 0 baseline or two evaluated periods (script `scen.py`).<br>**Scope.** Every new relation takes output elements only (shown counts, periods, changes, items) and `provides`, which is the "where provided" of section 3.5. |
| R08b-02 | fixed: the stated criterion was corrected so that it matches the formal values of all 17 rules. The values are unchanged, as the orchestrator asked and as the review's option (a) allows; no evidence was found that any value is wrong. | E-041 (`excludes` comment, Meaning, Evidence with three new quotes, Evidence intro, Notes "Types and exclusions"); E-008 Notes; E-043 Notes; INV-001 Reading; INV-055 Reading and Notes; INV-059 Reading; section 7 row OUT-018; section 10 (new S-106) | **Criterion now stated** (component comment, Meaning, Notes): among the types a rule is named for (`appliesTo`), a type is excluded when the same guidance gives it, in another rule of the list that names that type and not all preventive treatment, a time point after this rule's time point or, for a window, after its latest date. Both time points are taken as the guidance states them, or as a guidance it refers to for details states them. Excluded: time points for all preventive treatment, time points that do not lie after this rule's, and times that are not evaluation time points of the list.<br>**Check of every rule (E-041 Notes):**<br>• `ruleAan14A` (8–12 weeks after the dose is reached) vs 14B (24 weeks): after the window → `{onabotulinumtoxinA}` ✓.<br>• `ruleRu71` (3 months) vs section 3.3 BTA (minimum 6 months): after → `{onabotulinumtoxinA}` ✓. The 3.3 anti-CGRP comment gives the same 3 months, not later.<br>• `ruleTrBox8` (2–3 months) vs 3.6.3.9 (after 3 injection cycles, injections "3 ayda bir", about 9 months): after → `{onabotulinumtoxinA}` ✓.<br>• `ruleNice1327` (3–6 months) vs 1.3.28 (12 weeks, before the window) and 1.3.29 (end of the 2nd cycle). TA260, to which CG150 1.3.26 refers "For full details", gives re-treatment every 12 weeks, so the 2nd cycle ends 24 weeks (168 days) after the first injection. That lies within the window: 3 months is at most 92 days and 6 months at least 181 days, checked for every start date 2024–2028. → `∅` ✓.<br>• `ruleRuChildren`: no other time point in [S-034] → `∅` ✓.<br>• The 12 type-specific rules: their guidance gives their types no later time point of their own → `∅` ✓. SIGN's titrated and fixed-dose rules, and IHS Q2's oral, monthly and quarterly rules, concern different types. The IHS dose increase after the first onabotulinumtoxinA cycle and the EHF re-evaluation in selected cases are not evaluation time points of the list.<br>**The NICE rationale "names no exception"** is replaced by the timing argument. That argument is what separates NICE 1.3.27 from Turkish Box 8, as the review noted.<br>**New evidence (E-041 Evidence):**<br>• [S-015] the 1.3.26 cross-reference to TA260;<br>• [S-106] TA260 §2.1, re-treatment every 12 weeks;<br>• [S-035] §3.6.3.9, injections every 3 months.<br>**Readings and rows.** The Readings of INV-001, INV-055 and INV-059, the E-008 and E-043 Notes, the INV-055 Notes and the OUT-018 row now state the criterion, or point to `excludes`, instead of "names another time point". The INV-058 Reading states no criterion ("of no type the rule excludes") and needed no change. The v07 entry of the change log is a record of v07 and was left as it was. |

## Other changes

1. **Sweep for the R08b-01 kind** (a Stage 1 list introduced by "for example", "such as" or "include" that the model closes). Every Stage 1 Statement and Caveat was searched by script; 23 occurrences were found. The occurrences in the Caveats of OUT-018, OUT-025, OUT-026 and OUT-033 give examples of sources, criteria or facts, not of output content that the model could close; the criteria of the OUT-018 Caveats are open through any `ResponderCriterion`.
   - **OUT-003, fixed.** The completeness indicator is given "for example expressed as the proportion of days". `CompletenessExpression` was closed to covered days and the proportion. It gains the tag `otherCompletenessExpression ⟨Text⟩` (E-013). INV-012 still relates only the two numeric forms. Also updated: the E-013 comment ("in one or more forms") and Notes; the INV-011 and INV-012 Readings, which said "or both" and "at most once in each form"; the OUT-003 row.
   - **OUT-038, fixed.** "indicators such as possible medication overuse (OUT-016), responder labels (OUT-020) and trigger associations (OUT-032) require clinical interpretation". INV-100 was closed to these three.
     - New INV-100 Notes define an indicator: an element that points to a possible clinical condition, or classifies the subject's state under a criterion or a published grading.
     - INV-100 now also covers an instrument result that shows a grade or category. [S-014] says grading is "indicating" the patient's need (Stage 1 OUT-026), and HURT areas are "indicating increasingly important treatment deficiencies".
     - It also covers a depression or anxiety screening result, which OUT-033 reports "as screening results" with "(see OUT-038)", and of which it says "A high HAD score is not specific".
     - The Notes say why other elements are not indicators: the completeness indicator states diary coverage, not a clinical finding; attack marks place a date against a window; the three-month view assigns no diagnosis.
     - Also changed: INV-100 Realises (+OUT-026, +OUT-033), Reading and Evidence; E-058 Conformance and Realises (+OUT-038); E-059 Conformance; rows OUT-026, OUT-033 and OUT-038.
     - Level SHOULD, as OUT-038.
   - **Checked and not changed:**
     - OUT-001: any selection.
     - OUT-002: `PublishedDefinition` is a given set.
     - OUT-009: other granularities are not excluded; monthly series are needed for OUT-001.
     - OUT-010: `otherIntensitySummary`.
     - OUT-011: `otherStatistic`. The duration kinds are those of the Statement ("attack or headache duration"), not its examples.
     - OUT-014: the ICHD-3 8.2 classes are complete.
     - OUT-018: the rule list (R07-01) and `OtherItem`.
     - OUT-020: the criterion names, through any `ResponderCriterion`.
     - OUT-021: an enumeration, not an example list.
     - OUT-023: `FormulationOrRoute` is a given set.
     - OUT-025: any windows.
     - OUT-026: `otherInstrument`.
     - OUT-029: any ICHD-3 code.
     - OUT-033: `otherScreeningInstrument`.
     - OUT-036: `otherCaregiverImpact`.
     - OUT-037 Caveats: a scope statement.
2. **Sweep for the R08b-02 kind** (a prose definition of a component that disagrees with its formal values). All 187 `omn` lines that carry a comment after a declaration (attributes, components, constants, functions, predicates, variant tags) were listed by script and compared with the values they describe; the related Meaning texts were read.
   - **E-041 Meaning, fixed.** It glossed `atLeastOffset` with the wordings "a minimum of", "at least" and "wait". Yet "at least 8–12 weeks" (`ruleAan14A`) and "en az 2-3 ay" (`ruleTrBox8`) are `withinWindow`, as is "niet eerder dan na 2-3 maanden". The Meaning now states the rule that the values follow: `atLeastOffset` for a single offset worded as a minimum; `withinWindow` for a range, also where the range is worded as a minimum. This matches the settled window readings, which are not reopened.
   - **E-045 Meaning (`namedCriteria`), fixed.** The definition "the criteria named in the Stage 1 evidence of OUT-018 and OUT-020" also reads on the trial endpoint "50% responder rate" of [S-002] (OUT-018), which is not in the set. It now says criteria for judging an individual's response, and that [S-003] and [S-005] (OUT-020) exclude responder rates from that use. `namedCriteria` is used in no invariant.
   - **E-045 `alsoRestsOn`:** fixed under R08b-01.
   - **E-013 `expressions`:** "in one or both forms" became "in one or more forms" after the new tag (item 1).
   - No other disagreement was found. The other component comments match their values, for example `wholeNumberScores`, `publishedRecall`, `scoreRange`, `overuseLevel`, `classesOf826`, the window and remission constants, and the `GradeBand` table.
3. **Satisfiability pass** over every changed invariant and attribute and those that constrain the same elements and views (against INV-001 and the context definitions).
   - **INV-062 with the other invariants on the same values.**
     - The values required by (a) can be shown for the baseline and evaluated months. These periods are already in the label's view (INV-003), and a value the view already shows is referenced, not repeated (INV-006).
     - Attack counts are available per calendar month or 28-day period wherever provided (INV-108).
     - Each kind admits a value for any period: a count of 0, a `total` duration of 0, `daysWithSymptom(0)`, `caregiverLostProductiveDays(0)`, a composite index in a secondary or exploratory role with its components (INV-091, INV-092), and acute summaries with 0 treated attacks (E-051 `sequence` SHOULD only when > 0; INV-072, INV-074).
     - The relations INV-005, INV-024, INV-030, INV-031, INV-032 and INV-033 hold with consistent values.
     - The changes of (c) compare the comparison's own periods. INV-053 and INV-054 are met, INV-056 admits them, INV-097 holds with equal-length periods, and INV-060 concerns only migraine and headache days.
     - (b) needs an item that shows the named value in the label's view; no item kind is confined to a view type in a way that prevents this (cycle lines and attack marks can be shown in any view).
   - **INV-063.** The two forcing antecedents remain mutually exclusive. The new component only adds a disjunct to `componentMet` and `componentDecided`, so for any shown values a consistent category exists. The `where` clause is met by every named criterion and can be met by any criterion a reader names.
   - **INV-100.** The new annotations are shown in the same view (INV-007, definitional). There is no conflict with INV-084 or INV-099.
   - **E-013 and INV-011/INV-012.** The new form is unconstrained text; the numeric relations are unchanged.
   - **E-041.** Values unchanged, so INV-055, INV-058, INV-059 and E-043 `timePoints` are as in v07.
   - **Derived attributes.** None is required where its relation is undefined. No new derived attribute was added. The attack test has a guard `b.count > 0` and no division.
   - **Result.** No MUST or SHOULD invariants are jointly unsatisfiable in any admissible context, so no conflict needed fixing.
4. **Bookkeeping.**
   - Header "Version: v08 · Iteration: 08 · Status: under review".
   - Section 9 "as of v08".
   - Section 10: new S-106 (NICE TA260), access date 2026-10-21.
   - Section 11: iteration 08 paragraph (no web search; S-106 reached through the CG150 link).
   - Section 12: v08 entry.

## Checks

Scripts in the session scratchpad (`mech.py`, `names.py`, `quotes.py`, `scope.py`, `scen.py`) were run on the final OUTPUT_MODEL.md.

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108). None missing, no duplicates, none withdrawn. |
| References | No dangling E- or INV- reference.<br>S references lie within S-001–S-046 and S-101–S-106, and every S-1NN used has a row in section 10.<br>OUT references lie within 001–039.<br>ISS headings are ISS-01–06 and ISS-08–11; ISS-07 occurs only as the withdrawn ID. |
| Realises and traceability | Every element and invariant has exactly one Realises field.<br>39 rows, in Stage 1 order (OUT-039 after OUT-025).<br>0 differences between the rows and the union of the Realises fields. The new links are INV-100 → OUT-026 and OUT-033, and E-058 → OUT-038, all in their rows.<br>No coverage text names an ID outside its row.<br>39 × "full". |
| Names and types in `omn` blocks | 322 declared names (v07: 316). New: `AttackReductionComponent`, `PeriodValueKind`, `showsValueNamed`, `valueOfKind`, `attackReductionMet`, `attackReductionDecided`. None is declared twice.<br>217 enumeration constants and variant tags (v07: 204; 13 new), with no clash with declared names.<br>Every attribute selection is declared on some type.<br>Every remaining identifier is a bound variable or parameter.<br>Every type used in the new text is declared: `DayMeasure`, `CountedEvent`, `DurationKind`, `AssociatedSymptom`, `HeadacheIndexKind`, `PeriodValue`, `DayCount`, `EventCount`, `AttackCount`, `IntensitySummary`, `DurationSummary`, `AssociatedSymptomSummary`, `MostBothersomeSymptomItem`, `CaregiverImpact`, `CompositeIndex`, `AcuteTreatmentSummary`, `InstrumentResult`, `ScreeningResult`, `Item`, `TypeScope`, `Text`. |
| Typing rule for levels | 172 level-annotated attribute declarations, as in v07; 0 violations. |
| Conformance levels | MUST 19 (INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054–057, 059, 068, 086, 102, 108).<br>MUST NOT 2 (INV-048, 106).<br>SHOULD 47.<br>SHOULD NOT 8 (INV-013, 021, 043, 065, 084, 091, 101, 107).<br>Definitional 32.<br>No invariant changed level or scope; INV-100 stays SHOULD, the level of OUT-038. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. |
| Unchanged values | The 17 rule constants of E-041 and the 6 criterion constants of E-045 are byte-identical to v07. |
| Quotes | 30 new quoted strings: 28 found verbatim, 2 are translations (see above). |
| Scope sweep (enter, entry, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, reminder, field, obtained, calculated, computed, algorithm, "diary information", "diary data") | 85 occurrences (v07: 83). The two new ones are "diary information" in the E-013 Notes and the INV-100 Notes. Both describe the coverage that the completeness indicator states, in the wording of Stage 1 OUT-003 ("covered by diary information"). The other differences are unchanged occurrences with changed surrounding text and the section headings "Search log" and "Change log".<br>No input entity, storage term or derivation from input was added. The new relations take output elements (shown counts, periods, changes, items) and `provides`. |
| Satisfiability | See Other changes 3: no conflict. Scenario script: the exclusion arithmetic holds for every start date 2024–2028, and the attack-reduction decisions are as intended. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v08.md`: identical. |
| Files written | Only OUTPUT_MODEL.md, history/v08.md and this fix log. Nothing under docs/stage1-output-requirements/ was changed, and nothing was committed or pushed. |
