# Fix log — iteration 13
Input review: reviews/review-iter-13.md · Input version: v12 · Output version: v13
Date: 2026-10-21

## What was read and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3;
- v12 (`OUTPUT_MODEL.md`, byte-identical to `history/v12.md`);
- review 13.

**Earlier loop files read, so that no fix is undone:**
- fix logs 09 (satisfiability note "INV-071, INV-069 and INV-104 do not constrain the scope"), 10 (the "All types" flag of the prose sweep) and 12 (all sweeps);
- review 02, R02-06 (associated symptoms on every treated-attack line of a subject with migraine);
- the oscillation checks after iterations 08 and 12, with their watch points.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**Downloads.** None. All three remarks concern the formal model and are verified against the Stage 1 v18 text in the repository and against v12. No quote was added or changed. Every quoted fragment of the new text was checked by script and occurs verbatim in Stage 1 v18:
- OUT-001 "Every summary output MUST state the reporting period it covers (start date, end date and length)";
- OUT-023 "across the attacks treated with it";
- OUT-024 "the response summary from OUT-018 or OUT-023 for each treatment";
- OUT-029 "When the patient has, or may have, more than one headache type";
- OUT-032 "the co-occurrence over time of attacks with potential trigger factors".

**Scripts.** All are in the session scratchpad (`fix13/`) and were run with `python3 -I`:
- `mech.py`: headings, references, traceability, invariant levels, attribute declarations and the typing rule (run on v12 and v13);
- `scope.py`: `concerns`, `onlyOfType`, `scopeFor` and INV-073 on six subject profiles, for the R13-01 examples and the cluster view (INV-088).

There are also inline checks: the diff of the `omn` text v12 → v13, the quote fragments, the scope words, the item diff, and the counts of the guarantee terms of earlier fixes.

### Verification of the remarks

**R13-01 holds.**
- **The defect.** In v12, eight presence requirements on per-period values state no type scope:
  - INV-039 (intensity);
  - INV-069 (intensity, each associated symptom, most bothersome symptom, acute-treatment summaries);
  - INV-071 (all three conjuncts);
  - INV-104 (acute-treatment summaries);
  - INV-062, the `acuteTreatmentEffectiveness` branch.

  The base requirements of the same kinds fix the scope: INV-018 and INV-022 use `allTypes`, and so do the `periodValuesOf` branch of INV-062, INV-037 and INV-068.
- **Example 1, reproduced.** A subject with migraine only: INV-071 is met by a sumatriptan summary scoped `ofType(c2)` with 0 treated attacks. INV-072, INV-073 (not cluster, so 2 hours), INV-074 and INV-011 hold. `scope.py` confirms that v13 excludes this scope.
- **Example 2.** A subject with migraine and tension-type headache can be shown the tension-type values only. INV-076 does not prevent this, because it only adds symptom statuses to lines.
- **Stage 1.** The statement parts name all the attacks or headaches concerned:
  - OUT-023 "across the attacks treated with it";
  - OUT-021 "for the attacks treated in each of these periods";
  - OUT-010 "headache intensity per reporting period".

  So the defect is a coverage gap at SHOULD, as the review states.
- **The same defect nearby** (Other changes, 1 and 2):
  - INV-104 asks for its functional-impact days with no scope;
  - INV-088 admits a cluster subtype the subject does not have, or one of two subtypes.

**R13-02 holds.**
- **The v12 trigger.** INV-098 fires only on `childOn(ctx, v.covers.start)`.
- **The review's example, checked.** `adultFrom` 1 July 2026, topiramate started 1 May 2026, clinician-facing summary 1 August – 20 October 2026.
  - INV-104 places the response comparison in the summary.
  - Its 28-day baseline (3–30 April) is placed there by INV-056 and INV-003.
  - INV-097 applies to it (`childIn` holds), but INV-098 does not.
- **Results.** A PedMIDAS result of 15 May 2026, required with its recall by INV-096, escapes the caveat in any view whose covered period begins after 30 June 2026.
- **Model's own reading.** The v12 Notes ("the views of periods that begin while the subject is a child or adolescent") are broader than the predicate.

**R13-03 holds.**
- **The defect.** `factorDates` and `attackOnsets` (E-065) occur in no invariant. A view covering March can show June dates next to the March completeness indicator; INV-003, INV-008, INV-011, INV-090 and INV-100 all hold.
- **The model's own pattern.** Elsewhere dated content is tied to its period: treated-attack lines to the summary's period (INV-074), and cycle lines to the covered period (INV-087).

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R13-01 | fixed: the review's option (a), including the two items it names as optional | INV-039, INV-062, INV-069, INV-071, INV-104, INV-105, INV-109 (Predicates and Readings); Notes of INV-062 and INV-109; Conformance of E-023, E-025, E-026, E-046, E-051 and E-055; E-045 Meaning and Notes; rows OUT-010, OUT-020, OUT-021, OUT-023, OUT-024, OUT-034 and OUT-035 | **Predicates.** Each listed conjunct now requires the value over all headache types combined:<br>• INV-039: `m.typeScope = allTypes` for the intensity summaries of the compared periods;<br>• INV-069: the same for intensity, each associated symptom and the most bothersome symptom, and `s.typeScope = allTypes` for the acute-treatment summaries;<br>• INV-071: `s.typeScope = allTypes` in all three conjuncts (all formulations and single formulation for the time range; baseline and on-treatment periods);<br>• INV-104: the same for the acute-treatment summaries;<br>• INV-062, `acuteTreatmentEffectiveness` branch: the same.<br>**Optional items of the review:**<br>• INV-105: the treatment effect is a response comparison or an acute-treatment summary over all headache types combined;<br>• INV-109: an acute treatment line's response summaries include one over all headache types combined (E-055 `acuteResponse`).<br>The scope goes into the SHOULD invariant INV-109 as an existence requirement, not into the definitional INV-079. A `∀` there would exclude a line that also references a summary of one type, which Stage 1 permits.<br>**Basis.** This is the scope that INV-018, INV-022 and the other two branches of INV-062 already use for the same kinds of value. It matches the Stage 1 wording: OUT-023 "across the attacks treated with it", OUT-021 "for the attacks treated in each of these periods", OUT-010 "headache intensity".<br>**Text aligned:** Readings; E-045, E-046 and E-051 for the acute branch; E-023, E-025 and E-026 Conformance (which also now name INV-069); the rows.<br>**Watch point 2 (responder labels).** INV-062 gains a scope conjunct only. These are unchanged: `#L.evaluated = 1`, the `evaluationResult` / `pretreatmentBaseline` pair, `rc.treatment = L.treatment`, the open `UnderlyingKind` and `PeriodValueKind`, `otherValueNamed`, `attackScope`, `conditionHolds`, and the per-drug, per-period summaries of R11-02. Their counts are equal (Checks). No category is decided on acute summaries (INV-063 unchanged).<br>**Kept:** R02-06 (INV-076 unchanged) and R09-01. |
| R13-02 | fixed: the review's option (a) | INV-098 (Predicate, Reading, Notes); E-008 Notes; row OUT-036 | **Predicate.** `∀ v : View • childIn(ctx, {v.covers} ∪ (v.content ∩ Period)) ∨ (∃ r ∈ v.content ∩ InstrumentResult; d ∈ r.completionDate • childOn(ctx, d)) ⇒ annotated(v, supportiveInformation)`.<br>The covered period is named explicitly, so the v12 antecedent is included without relying on INV-003.<br>**What it now covers.** All four outputs of OUT-036 wherever they are shown:<br>• (a) a PedMIDAS result completed in childhood;<br>• (b) school-day and caregiver values of childhood periods;<br>• (c) and (d) comparisons and changes that reach into childhood, including the response comparison of a treatment started then, in a summary of a later period.<br>The Notes say so.<br>**Option (a) rather than (b).** It is the direct generalisation of the model's own reading (views of childhood periods), and it does not need a list of paediatric output kinds.<br>**Watch point 6.** The age stays read on the dates of the output (`childIn`, `childOn`). Neither `ageGroup` nor an as-of-date reading is restored. |
| R13-03 | fixed: the review's option (a) | new INV-110 (definitional); E-065 (new Notes); INV-011 Reading; rows OUT-001 and OUT-032 | **New INV-110:** `∀ v : TriggerCooccurrenceView • ∀ d ∈ v.factorDates ∪ v.attackOnsets • inPeriod(d, v.covers)`. Realises OUT-001 and OUT-032; definitional (E-065). It states a property of the view's own covered period, as INV-074 does for treated-attack lines.<br>**Text.**<br>• INV-011 Reading: the premise "whose summaries concern the diary information of that period" now points to INV-110.<br>• E-065 Notes give the relation.<br>• Rows OUT-001 and OUT-032 list INV-110, as the union of the Realises fields requires.<br>**Not changed:** E-065 itself, which is not a watch point. |

## Other changes

**1. INV-104, functional impact (the R13-01 defect in the same invariant).**
- **The defect.** The two functional-impact conjuncts of INV-104 (days affected in each of the three domains; days with severe functional impairment) stated no type scope. A migraine-only subject's summary could show the tension-type values, 0 days.
- **The fix.** `m.typeScope = allTypes` in both, as INV-026 and INV-027 require for the same values (OUT-027; OUT-034 "functional impact (OUT-027)").
- **Text:** INV-104 Reading; row OUT-034.

**2. INV-088, the cluster view (the R13-01 defect, through cluster subtypes).**
- **The defect in v12.** v12 required "∃ r ∈ v.rates • r.bout = b ∧ r.basis = k" and an acute summary with `s.earlyTimePoint = fifteenMinutes`. Through INV-073 and INV-089 these must have a scope of cluster headache only (`onlyOfType`), but that scope admits every subtype of 3.1. So, as `scope.py` shows:
  - a subject with cluster headache 3.1 had its requirements met by rates and summaries scoped to 3.1.1 or 3.1.2, a type it does not have;
  - a subject with 3.1.1 and 3.1.2 had them met by values of one subtype only.
- **The fix.** Both conjuncts now require `scopeFor(c, …, c3_1)` (E-012): over all types combined where every type the subject has or may have is cluster headache or a subtype of it, otherwise `ofType(c3_1)`. Exactly one scope satisfies `scopeFor`.
- **No conflict.** It implies `onlyOfType(c, …, c3_1)`, so INV-073 still gives 15 minutes and INV-089 holds. The review's satisfiability note ("the cluster view keeps its own cluster-scoped 15-minute summaries") still holds.
- **Text:** INV-088 Reading and Evidence (OUT-029 for the type scope, as in INV-089); E-012 Evidence and Notes (INV-088 among the users of `scopeFor`); row OUT-031.

**3. Noted, not changed: the formulation scope of per-drug acute summaries.**
- **What is open.** The per-drug summaries required by INV-062 (three acute branches), INV-069, the per-phase conjunct of INV-071, INV-088, INV-104 and INV-105 do not fix `formulationScope`. For a drug used in two formulations, a single-formulation summary can therefore meet a per-drug requirement.
- **Why it is not changed here.** This is a different attribute from the headache-type scope that R13-01 names. Its reading also needs a decision of its own: in the model an "acute medication" is a drug-and-formulation pair (E-008 `AcuteMedication`), while OUT-023 speaks of "per-drug outcomes" and of their separate presentation "for each formulation of the same drug".
- Under the minimal-change rule of this iteration it is noted here, not changed. The new prose claims nothing about formulations.

**No other change.**
- No element or invariant was withdrawn, and no level changed.
- No watch-point item changed: E-039, E-041, E-060, E-061, INV-003, INV-050, INV-054, INV-063, INV-064, INV-078, INV-086, INV-087 and INV-097 are byte-identical to v12.
- No whole-model sweep was run.

### Satisfiability pass

For every changed or new invariant, together with the invariants that constrain the same elements and views, I built a construction by hand and, for the scope predicates, checked it with `scope.py`. No admissible context (INV-001) makes the MUST and SHOULD constraints jointly unsatisfiable. No derived attribute was added or changed.

- **Values over all headache types combined** (INV-039, INV-069, INV-071, INV-104, INV-105, INV-062):
  - **Showable for any period.** A value of the person over all types can be shown for any period. Counts and summaries may be 0, and an acute-treatment summary may have 0 treated attacks (INV-072, INV-074).
  - **INV-032.** It bounds a peak-intensity distribution by the headache days of the same scope, where the view shows them. INV-068 (MUST) shows them over all types in the treatment review view, and INV-037 in a comparison of selected periods of equal length. The true values satisfy the bound.
  - **INV-033.** It bounds attacks with a symptom by the attack count of the same scope, which INV-069 shows over all types.
  - **INV-073.** It gives an all-types summary 2 hours unless the subject has, and may have, only cluster headache; then it gives 15 minutes, OUT-023's time point for cluster headache (`scope.py`: profiles "cluster only" and "3.1.1 + 3.1.2").
  - **Other invariants on the same summaries.** INV-071, INV-069, INV-104, INV-105, INV-109 and INV-062 fix no time point. INV-072 (content in the summary's view; all formulations named for an all-formulations summary) and INV-074 hold for any scope. INV-076 adds symptom statuses to every line of a subject with migraine, whatever the scope (R02-06).
  - **INV-011 and INV-012.** The completeness indicator is over all types anyway.
- **INV-109 with INV-079 (definitional), INV-072 and INV-104.**
  - The all-types summary has the line's drug (INV-079) and is shown in the line's view with its outcomes and lines (INV-072).
  - In the clinician-facing summary, the line can reference the all-types summary that INV-104 requires.
- **INV-088 with INV-073 and INV-089.**
  - `scopeFor(c, sc, c3_1)` implies `onlyOfType(c, sc, c3_1)`. So INV-073 gives 15 minutes, which INV-088 requires, and INV-089 admits the rate.
  - The count relation of INV-089 holds with the attack count of the same scope wherever the view shows one.
  - For a subject with cluster headache only, the all-types summaries of INV-071 and INV-104 also have 15 minutes, so the cluster view and the other views agree.
- **INV-098 with INV-007 and INV-099.** An annotation can qualify any view, and INV-099 already annotates every view. The antecedent only widens, so no other invariant is affected.
- **INV-110 with INV-003, INV-008, INV-011, INV-090, INV-098, INV-099 and INV-100.**
  - E-065 is MAY, and no invariant requires a trigger view with a given covered period, so the covered period can be chosen to contain every date shown.
  - INV-003 shows that period, INV-011 asks for its completeness, and the label and annotations can be added whatever the period is.

### Levels and paraphrases

**Levels.**
- **Unchanged.** Every changed invariant keeps its level, which is that of the Stage 1 part it realises over its whole range:
  - INV-039 SHOULD (OUT-010);
  - INV-062 SHOULD (OUT-020);
  - INV-069 SHOULD (OUT-021, OUT-023);
  - INV-071 SHOULD (OUT-023);
  - INV-088 SHOULD (OUT-031);
  - INV-098 SHOULD (OUT-036 Caveat);
  - INV-104 SHOULD (OUT-034);
  - INV-105 SHOULD (OUT-035);
  - INV-109 SHOULD (OUT-024).
- **New.** INV-110 is definitional (E-065): it is a bound that follows from the meaning of `covers` (section 3.3, item 5), as INV-074 is.
- **Attribute declarations.** 172, unchanged.

**Paraphrases.** Every changed Reading, Notes, Conformance and Meaning text and every changed row was compared with its predicate.
- **Overclaim avoided.** Two draft phrases claimed that a required summary "covers every attack treated with the medication". They were removed before the final version, because the formulation scope stays open (Other changes, 3).
- **R10b-02 class.** The INV-088 paraphrase of `scopeFor` keeps the condition "the subject has a headache type".
- **INV-110 Reading.** It refers to the completeness that INV-011 asks for, and does not state it as a fact.

### Watch points (oscillation/check-after-iter-12.md)

1. **E-041.** Unchanged.
2. **Responder labels.** INV-062 gains one scope conjunct, a tightening. The counts of the guarantee terms are equal to v12:
   - `#L.evaluated = 1`: 7;
   - `rc.treatment = L.treatment`: 13;
   - `evaluationResult(L`: 7;
   - `pretreatmentBaseline(L`: 6;
   - `otherValueNamed`: 6;
   - `ch.reference.typeScope = allTypes`: 7;
   - `attackScope(`: 5;
   - `conditionHolds(`: 10.

   `scopeFor(` rises from 5 to 8 (INV-088). INV-063 and INV-064 are unchanged.
3. **Co-presence.** INV-003, INV-054, INV-056 and INV-078 are unchanged. R10b-01 is kept: no value is placed next to a change.
4. **Menstrual-relation view and overview.** INV-086, INV-087, E-060 and E-061 are unchanged. INV-105 changed only in its treatment-effect conjunct; the cycle-line conjunct and the series are unchanged.
5. **Withdrawal follow-up.** INV-049, INV-050 and E-039 are unchanged.
6. **Time-frame components.** Unchanged. INV-098 keeps the dated reading.
7. **Change volume.** No sweep was run. This version changes:
   - 10 elements;
   - 10 invariants, and adds 1;
   - 11 traceability rows;
   - the header and sections 9, 11 and 12.

   The iteration-12 check counted 264 changed items in v12 at its finer split, which counts fields and declarations separately.

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-11; ISS-07 appears only as withdrawn. |
| References | No dangling E-, INV- or ISS- reference. S references lie in S-001–S-046 and S-101–S-106, and each S-1NN has a row in section 10. OUT references lie in 001–039. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025). Exactly one Realises field per item. Each row's E and INV columns equal the union of the Realises fields: INV-110 is in rows OUT-001 and OUT-032. No coverage text names an ID outside its row (ranges expanded). All rows say "full". |
| Types and names | Every name in the changed `omn` text is declared: `scopeFor`, `childIn`, `childOn`, `inPeriod`, `annotated`. Every attribute selection is declared on its type: `typeScope` on `IntensitySummary`, `AssociatedSymptomSummary`, `MostBothersomeSymptomItem`, `AcuteTreatmentSummary`, `DayCount` and `ClusterAttackRate` (all extend `PeriodValue`); `factorDates`, `attackOnsets` and `covers` on `TriggerCooccurrenceView`; `completionDate` on `InstrumentResult`; `role` and `acuteResponse` on `TreatmentLine`.<br>Type-checked by hand:<br>• `{v.covers} ∪ (v.content ∩ Period)` is a finite set of `Period` atoms, the parameter type of `childIn`;<br>• `r.completionDate` (`opt Date`) is used only inside a quantifier;<br>• `v.content ∩ ResponseComparison ≠ ∅`;<br>• the precedence of the new INV-098 and INV-105 formulas is as intended (`∨` before `⇒`; the parenthesised `∃` bodies end at their parentheses). |
| Typing rule for levels | Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33 (INV-110 new); total 110. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Scope sweep | The whole document was searched for enter, entry, record, input, captur, logged, store/storage, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field and questionnaire: 65 occurrences in v12 and v13, with the same count per term. The added lines contain only "history" (the subject's treatment history) and "diary information" (the INV-011 Reading, and the new INV-110 Notes, in the wording of section 3.6 and Stage 1 OUT-003). No input entity, no storage term, and no relation or threshold with an input argument. Every new relation takes output elements and context properties only: type scopes, dates shown, covered periods and completion dates. |
| Quotes | No quote added or changed. The five Stage 1 fragments of the new text were checked by script against Stage 1 v18 (verbatim). |
| Snapshot | `cmp OUTPUT_MODEL.md history/v13.md`: identical. |
