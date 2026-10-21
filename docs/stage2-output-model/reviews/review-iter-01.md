# Review — iteration 01
VERDICT: REMARKS
REMARK_COUNT: 12
Reviewed version: v00
Date: 2026-10-21

## Summary

v00 is a careful, well-typed model. Every quote was found verbatim at its stated source. All five new sources have correct metadata. The notation is complete: every name used is declared, the typing rule for levels holds for all 165 attribute declarations, and the IDs and the traceability table are consistent. The scope sweep found no input, storage or derivation-from-input content. Every formula and threshold has only output elements, context properties or cited constants as arguments.

The remarks fall into five groups:

- **Fidelity and coverage in the treatment-response part:**
  - evaluation time points of Stage 1 evidence are missing (R01-01);
  - the type-independent rules depend on a type listing (R01-02);
  - "monthly" values are not represented in the response comparison (R01-03);
  - the aggregation of a responder label over several periods is unsupported (R01-04);
  - the OUT-018 Caveat on continuation decisions is missing (R01-05).
- **Narrowings and gaps in other requirements:** OUT-029 per-type acute-medication outputs (R01-06), per-attack outcomes for OUT-023 and OUT-012 (R01-07), and the clinician summary of OUT-034 (R01-09).
- **Formal defect:** the menstrual-cycle view (R01-08).
- **Value-set and citation details:** score ranges (R01-10) and one wrong location (R01-11).
- **Section 8 handling:** R01-12.

## Verification coverage

Downloads were made with `curl` into fresh directories under the session scratchpad, outside the repository. Text was extracted with `pdftotext` (raw and `-layout` modes), and HTML/XML tags were stripped with a script. A script checked every quote in three passes:

1. exact after collapsing whitespace;
2. after normalising typographic quotes, dashes and line-end hyphens, and removing the ICHD-3 glyphs "≥", "±", "−" that have no text mapping;
3. alphanumeric-only.

I inspected every quote that matched only at pass 2 or 3 in context. In each case the only differences were the documented glyph and line-break artefacts. Page locations were checked page by page (`pdftotext -f/-l`).

### Citations

| Source | Where checked | Quotes checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|---|
| S-001 ICHD-3 (Stage 1 URL) | ichd-3.org PDF; PDF page = printed page | 29 distinct:<br>• 15 code labels (pp. 8, 9, 12)<br>• 8.2.3 comment<br>• 8.2.6 criterion B and note 2<br>• 8.2, 8.2.1, 8.2.2, 8.2.3 Descriptions<br>• 8.2.4, 8.2.5, 8.2.8 criterion B<br>• A1.1.1 and A1.1.2 criterion B, note 2<br>• cluster remission.<br>Also the ISS-02 claim that "simple analgesics" occurs once (p. 139, 10.1.1). | 29; ISS-02 claim confirmed | 0 | 0 |
| S-008 IHS 2024 prevention (Stage 1 URL) | univaq PDF | 3 (Q6 30 % alternative, p. 12; MIDAS/HIT-6 AHS definition, Q6 Evidence, p. 13; PGIC judgement item, p. 12) | 3 | 0 | 0 |
| S-010 IHS position statement 2025 (Stage 1 URL) | univaq PDF | 5 (four control levels and the "In some cases" sentence, p. 6; the running-header break after "per" confirmed) | 5 | 0 | 0 |
| S-014 Lifting The Burden / EHF aids (Stage 1 source) | Europe PMC full-text XML of PMC6734476 | 5 (HALT-90 and HALT-30 recall sentences, "Scoring HALT" unit sentence, Table 18 headings and four rows, HURT sentence of ISS-06) | 5 | 0 | 0 |
| S-101 Yang et al. 2011 | Europe PMC XML; listed PMC URL returns HTTP 200 with the text | 2 (Methods, "Data sources") | 2 | 0 | 0 |
| S-102 Pavlović et al. 2015 | Europe PMC XML; PMC URL HTTP 200 with the text | 2 ("Migraine-related disability") | 2 | 0 | 0 |
| S-103 Cincinnati Children's PedMIDAS page | listed URL, HTTP 200 | 1 (heading and four table rows, "PedMIDAS Grading Scale"; page footer "© 2026") | 1 | 0 | 0 |
| S-104 Snaith 2003 | Europe PMC XML; PMC URL HTTP 200 with the text | 1 ("Construction of the Hospital Anxiety And Depression Scale (HADS)") | 1 | 0 | 0 |
| S-105 PHQ/GAD-7 instructions (Joint Commission copy) | listed PDF, HTTP 200 | 3 (PHQ-9 and GAD-7 ranges, P.6/9; developers sentence in the Sources entry) | 3 (wording) | 0 | 0 — but the developers sentence is on P.8/9, not P. 9/9 (R01-11) |
| **Total** | | **51** | **51** | **0** | **0** |

**Metadata.** Checked with PubMed efetch/esummary:

- S-101: DOI 10.1177/0333102410379890, PMID 20819842, PMC3057423, Cephalalgia 2011;31(3):357–67.
- S-102: DOI 10.1186/s10194-015-0503-y, PMID 25902814, PMC4406925, J Headache Pain 2015;16:24, authors as listed.
- S-104: DOI 10.1186/1477-7525-1-29, PMID 12914662, PMC183845.
- S-103 developer paper: PMID 11739822, DOI 10.1212/wnl.57.11.2034, Neurology 2001;57(11):2034–9.

All are correct. The S-105 PDF metadata (author Kurt Kroenke, created 2010-06-22, modified 2014-04-16) matches the entry. There are no non-English quotes new in Stage 2: the S-023 and S-033 fragments in E-045 are substrings of Stage 1 quotes, whose translations carry over.

**Newer versions.** ICHD-3 (2018) is still current: a web search found only "ICHD-4 – Work in Progress" (Cephalalgia 2024) and an IHS ICHD-IV workshop in 2025, and no published ICHD-4.

**Stage 1 fragments.** 24 Stage 1 fragments cited inside model Evidence fields were checked by script as exact substrings of Stage 1 v18; all 24 are present. They are the E-041 offsets, the E-045 thresholds, the E-057 recalls and the E-039 window.

### Per-OUT fidelity check (Statement, Caveats, strength, traceability row)

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK (periods, monthly/28-day, equal-length comparison, Caveat via `lengthDays`) | 021 | OK |
| 002 | OK | 022 | OK (ISS-03) |
| 003 | OK (SHOULD / SHOULD NOT) | 023 | R01-07 |
| 004 | OK | 024 | OK |
| 005 | OK | 025 | OK (MAY) |
| 006 | OK | 039 | OK |
| 007 | OK | 026 | OK (ISS-06); see R01-10 for value sets |
| 008 | OK (MAY) | 027 | OK |
| 009 | OK | 028 | OK (ISS-03) |
| 010 | OK | 029 | R01-06 |
| 011 | OK (Caveat as INV-021) | 030 | R01-08 |
| 012 | R01-07 (most bothersome symptom per treated attack) | 031 | OK (see "Checked and not raised") |
| 013 | OK (MAY) | 032 | OK |
| 014 | OK | 033 | OK |
| 015 | OK | 034 | R01-09 |
| 016 | OK (MUST / MUST NOT; ISS-01) | 035 | OK (ISS-03) |
| 017 | OK | 036 | OK |
| 018 | R01-01, R01-02, R01-03, R01-05 | 037 | OK |
| 019 | OK (ISS-05) | 038 | OK |
| 020 | R01-04 | | |

Conformance levels were compared with the Stage 1 strengths for all 105 invariants and for the attribute levels of every element. No mismatch was found:

- MUST: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054–057, 059, 068, 086, 102;
- MUST NOT: INV-048;
- SHOULD NOT: INV-013, 021, 043, 065, 084, 091, 101;
- the rest are SHOULD or definitional.

### Mechanical checks (scripts in the session scratchpad)

| Check | Result |
|---|---|
| E-/INV- headings: count, sequence, duplicates | 67 elements (E-001–E-067) and 105 invariants (INV-001–INV-105), consecutive, no duplicates |
| Dangling E-/INV-/ISS-/S- references | none; S-1xx refs ⊆ {S-101…S-105}; Stage 1 refs within S-001–S-046; OUT refs within 001–039 |
| Every item has a Realises field | yes |
| Traceability table vs Realises fields | all 39 OUT rows present, in Stage 1 order (OUT-039 after OUT-025); for every OUT the element and invariant sets of the row equal the union of the Realises fields (0 differences); 39 × "full" |
| Names in `omn` blocks declared exactly once | no name declared twice; every undeclared identifier left after the script is a bound variable, the free context variable `c` of INV-001, or `refs` (defined in section 2.5) |
| Attribute selections `e.a` | every selected attribute is declared in some record or element type |
| Typing rule for levels (section 2.5) | 165 attribute declarations (163 parsed by script; the 2 core attributes with refinement types, `CompositeIndex.combines` and `PeriodComparison.periods`, checked by hand): every SHOULD/MAY or MUST-with-`when` attribute has an `opt`/`set`/`seq` type; none has a `set1`/`seq1` type |
| Scope sweep (enter/record/input/capture/log/store/persist/database/JSON/XML/CSV/FHIR/serialise/encode/retention/answer/entry/reminder) | only the exclusion statements (section 1, section 2.1), "the scoring of every instrument from its answers is out of scope" (E-057), the S-014 recall quote ("records days affected during the preceding 1 month", used for the recall value) and the search-log tool name "full-text XML" |
| Thresholds, formulas and derived attributes: arguments | all relations take output elements, context properties (section 3.5) or cited constants only; no relation takes input data |

## Remarks

### R01-01 Coverage gap: evaluation time points named in the Stage 1 evidence of OUT-018 are missing, although the model says the list is complete

- **Item(s):** E-041 (`evaluationRules`, Notes), E-045 (`critRu71`), INV-055, INV-059, section 7 row OUT-018.
- **Problem:** OUT-018 makes it a MUST that the output allows the comparison "at the evaluation time points named in current guidance". E-041 Notes say "The rule list is the set of time points named in the Stage 1 evidence", and the OUT-018 traceability row says "The time points are those named in the Stage 1 evidence". That is not the case. Two time points quoted in the Stage 1 evidence of OUT-018 are missing from `evaluationRules`:
  - NVN (S-028): no earlier than 2–3 months of treatment.
  - Russian adult recommendations (S-033): after 3 months of therapy.

  The model does model the Russian criterion `critRu71` ("section 7.1"), but not the time point the same sentence attaches to it. INV-055 and INV-059 therefore impose no MUST for these two time points. The NICE 1.3.27 window (3–6 months) does not cover them: it requires only one comparison somewhere in the window.
- **Evidence:** Stage 1 OUT-018 Evidence quotes both time points:
  - [S-028]: "Titreer naar de ondergrens van de geadviseerde therapeutische breedte, evalueer het effect niet eerder dan na 2-3 maanden behandeling, primair op geleide van frequentie; dit kan gedocumenteerd worden in een dagboek of kalender." (Translation: "... evaluate the effect no earlier than after 2–3 months of treatment ...")
  - [S-033]: "Рекомендуется считать профилактическое лечение М эффективным, если число дней с ГБ сокращается через 3 месяца терапии на 50% и более от исходного" (Translation: "... if the number of headache days decreases after 3 months of therapy by 50% or more from baseline").

  A script confirmed that both fragments occur verbatim in Stage 1 v18 ("evalueer het effect niet eerder dan na 2-3 maanden behandeling"; "через 3 месяца терапии"). Model text: E-041 axiom lists exactly nine rules: NICE ×3, AAN 14A, SIGN ×2, EHF Q3, IHS Q2 ×2.
- **Required change:** do one of the following, and in either case correct the E-041 Notes and the OUT-018 traceability text so that they describe the list accurately.
  - Add `EvaluationRule` constants for NVN "Profylactische behandeling migraine" (2–3 months of treatment, "niet eerder dan", that is, an at-least offset) and for the Russian recommendations section 7.1 (3 months after the start of therapy), with their `appliesTo` and anchors, and include them in `evaluationRules`.
  - Or state, with a reason grounded in Stage 1, why these two current-guidance time points are excluded.

### R01-02 Infidelity (applicability condition): even the type-independent guidance time points apply only if the context lists a guidance type for the treatment

- **Item(s):** E-041 (`applicable`), E-008 (`preventiveTypes`), INV-001, INV-055, INV-058, INV-059.
- **Problem:** `applicable(c, t, r)` requires `∃ ty ∈ r.appliesTo • (t, ty) ∈ c.subject.preventiveTypes`. INV-001 requires only `p.1 ∈ c.subject.preventiveTreatments` for the listed pairs. It does not require every preventive treatment to have at least one type.
  - For a preventive treatment with no listed type, no rule is applicable, even NICE 1.3.27 and AAN 14A, which the model applies to `allPreventiveTypes`. The time-point part of INV-055 (MUST) and INV-059 (MUST) is then vacuously satisfied.
  - Stage 1 states no such condition: NICE 1.3.27 applies to any prophylactic treatment.
  - The model thus adds an applicability condition ("the treatment's guidance type is known") that narrows a MUST of OUT-018.
- **Evidence:** OUT-018: "The output MUST allow this comparison at the evaluation time points named in current guidance". [S-015] 1.3.27 (Stage 1 quote): "Review the need for continuing migraine prophylaxis 3 to 6 months after starting prophylactic treatment."
- **Required change:** one of the following.
  - Add to INV-001 the conjunct `∀ t ∈ c.subject.preventiveTreatments • ∃ ty : PreventiveTreatmentType • (t, ty) ∈ c.subject.preventiveTypes`, so that `otherPreventive` serves as the fallback.
  - Or redefine `applicable` so that rules whose `appliesTo` is `allPreventiveTypes` apply to every preventive treatment, whatever the type listing says.

### R01-03 Infidelity: the response comparison does not represent "monthly" migraine and headache days

- **Item(s):** E-043, INV-055, INV-056, INV-057, E-040, INV-053; consequential: INV-061.
- **Problem:** OUT-018 requires the comparison of monthly migraine days and monthly headache days. In the model:
  - `baseline` and `onTreatment` are periods of any kind; no invariant restricts them to `MonthlyKind`.
  - The values compared are `DayCount`s, the number of days in the period.
  - INV-061 explicitly expects compared periods longer than a month ("a calendar-month or 28-day period within the compared period").

  An output can therefore compare, for example, an 84-day baseline with an 84-day on-treatment period and show "days in 84 days" and their absolute change as the values of OUT-018. These are not monthly values: the absolute change is three times the monthly change. The period granularity ("per what period", Stage 2 PROCESS.md section 4) of the Statement is not represented.
- **Evidence:**
  - OUT-018 Statement: "the diary output MUST compare monthly migraine days and monthly headache days (and, where reported, moderate/severe headache days) in a pre-treatment baseline period with periods after treatment start [...] showing both the values of each period and the absolute and percentage change from baseline".
  - Stage 1 OUT-005 evidence [S-022]: "the change from baseline in the mean number of monthly migraine days (MMDs)".
  - [S-015] 1.3.29: "the frequency of headache days per month".
  - Model: E-043 `baseline : →Period MUST`, `onTreatment : seq1 →Period MUST` (no kind); INV-056 places no constraint on `p.kind`.
- **Required change:** make the compared values monthly, by either of these options.
  - (a) Restrict the baseline and on-treatment periods of a `ResponseComparison` to `MonthlyKind`, allowing several consecutive monthly on-treatment periods, and simplify INV-061 accordingly.
  - (b) Add a derived per-month value for multi-month periods, for example a mean of the monthly counts shown for the consecutive monthly periods that make up the period, with its relation to those shown counts, and define the `Change`s of a response comparison on it.

  The responder thresholds (E-045, INV-063) must then be tested on the monthly values.

### R01-04 Formal defect: a responder label over several periods is forced to "responder" when any single period meets the threshold

- **Item(s):** E-046 (`reductionMet`, `reductionDecided`, `evaluated`), INV-063.
- **Problem:** `reductionMet` holds when there exists one change whose compared period is in `ran L.evaluated` and meets the threshold, and INV-063 (definitional) then forces `L.category = responder`. For a label that refers to several on-treatment periods, a single month with a ≥ 50 % reduction therefore makes "non-responder" impossible, even when the named criterion applied to the evaluation as a whole is not met.
  - Example: under NICE 1.3.28 or IHS Q6, month 1 −55 %, months 2 and 3 −20 %, and evaluation at 12 weeks or over the mean of the three months.

  No source supports this "any one evaluated month" aggregation. The named criteria evaluate at a time point, against a baseline month, or over a share of months. INV-063 thus excludes outputs that Stage 1 permits, a correctly labelled "non-responder" under the named criterion. The meaning of a label with several `evaluated` periods is not defined.
- **Evidence:**
  - Model: `pred reductionMet(L, r) ≙ … ∃ rc ∈ L.comparison; ch ∈ rc.changes • … ch.compared.period ∈ ran L.evaluated ∧ … 100 × (ch.reference.days − ch.compared.days) ≥ r.atLeastPercent × ch.reference.days`; INV-063: `(∃ k ∈ K.components • componentMet(L, k)) ⇒ L.category = responder`.
  - Sources: [S-015] 1.3.28 "Stop CGRP inhibitors after 12 weeks of treatment if the frequency of migraines does not reduce by: [...]"; [S-038] "reduction in monthly headache/migraine days reaches at least 50%, relative to the pre-treatment baseline month"; [S-029] "als tenminste de helft van de maanden 30% reductie van MMD op is getreden" (all Stage 1 quotes).
- **Required change:** define how a reduction component is evaluated when `#L.evaluated > 1`, and make INV-063 follow that definition, by either of these options.
  - (a) Apply INV-063's reduction relations only to labels with a single evaluated period. With several periods the label is then not decided by the shown values, as for judgement components.
  - (b) Add to `ResponderCriterion` an explicit, cited evaluation mode (for example at the time point, on the mean of the evaluated monthly values, in every evaluated period, or in a stated share of them) and use it in `reductionMet` and `reductionDecided`.

  Whichever option is chosen, a single period must not decide a multi-period label unless a source supports that reading.

### R01-05 Coverage gap: the OUT-018 Caveat "does not itself decide on continuation" has no representation

- **Item(s):** E-001 (`Claim`), E-043 Notes, INV-101, section 7 row OUT-018.
- **Problem:**
  - Section 7 defines "full" coverage as including "every Caveat that constrains what an output shows".
  - The OUT-018 Caveat constrains what the output shows: it must not itself decide on continuation.
  - The model mentions this only in prose (E-043 Notes: "names no continuation decision"). No `Claim` value names a continuation decision, and no invariant prohibits it.

  The model represents other constraining Caveats formally: OUT-011 → INV-021, OUT-033 → INV-084, OUT-036 → INV-098. The OUT-018 row nevertheless says "full".
- **Evidence:** OUT-018 Caveats: "the output shows the change and names the criterion a reader chooses to apply (OUT-020), but does not itself decide on continuation." OUT-020 Rationale: "Showing the named criterion with the underlying values serves both positions without the output itself making the decision." E-001 `Claim` lists only `diagnosis`, `clinicallyValidatedCutoff`, `soleIndicatorOfIndividualBenefit`, `standAloneEfficacyMeasure` and `replacesClinicalAssessment`.
- **Required change:** do one of the following, and in either case make the OUT-018 traceability entry reflect it.
  - Add a claim, for example `continuationDecision` ("presents a decision to continue, stop or change a treatment"), and a prohibition invariant `¬ ∃ x : Element • continuationDecision ∈ x.claims` that realises OUT-018 (Caveat) and OUT-020. Set its level by section 3.3(6) of the model.
  - Or, if the author holds that `replacesClinicalAssessment` (INV-101) covers continuation decisions, say so explicitly in E-001 and INV-101 and add OUT-018 to INV-101's Realises field.

### R01-06 Infidelity (narrowing): per headache type, only the total of the acute-medication outputs is required

- **Item(s):** INV-028, E-029 Conformance, section 7 row OUT-029.
- **Problem:** OUT-029 makes it a MUST to present "frequency and acute medication outputs separately for each headache type ... as well as combined". The acute-medication output of OUT-014 is MUST and consists of the total across classes, the per-class days (ICHD-3 8.2 classes) and the per-drug days. INV-028 requires only `TotalAcuteMedicationDays` per type. Neither the class nor the drug breakdown is required per type, and the model gives no reason for this. The rationale of OUT-029 names the use of the diary "to detect medication overuse" across headache types, which is exactly what the class and drug breakdown per type shows.
- **Evidence:**
  - OUT-029 Statement and Strength: "MUST for frequency and acute medication outputs per headache type". OUT-014: "broken down by drug class [...] and by individual drug, together with the total across classes".
  - [S-033] (OUT-029 evidence): "для облегчения дифференциальной диагностики с ГБН и для выявления лекарственного абузуса".
  - INV-028: `reportedTogether(c, {HeadacheDays, TotalAcuteMedicationDays} ∪ {K ∈ {ModerateSevereHeadacheDays, AttackCount} | provides(K)}, sc)`.
- **Required change:** do one of the following.
  - Include, for each `sc` in INV-028, the per-class and per-drug acute-medication day kinds of the subject's acute medications, as in INV-023.
  - Or, if the author reads "acute medication outputs" in OUT-029 as the total only, record that reading as a Stage 1 ambiguity in section 8 with a pointer from INV-028. Do not narrow the requirement silently.

### R01-07 Coverage gap: per-attack outcomes, and hence consistency across consecutive treated attacks, are never required

- **Item(s):** E-051 (`sequence`), E-053 (`results`), INV-072, INV-074; OUT-012 (most bothersome symptom per treated attack).
- **Problem:** OUT-023 asks the output to "show how consistently the drug was effective across consecutive treated attacks", and OUT-012 asks for the most bothersome symptom "in the response of individual treated attacks". The model represents both only through the attack lines of `sequence`:
  - INV-072 requires a non-empty sequence and an `intakeTiming` on each line.
  - It requires no line to show any outcome: `results : set AttackOutcomeResult core` may be empty.
  - It requires the sequence to contain only one of the summarised attacks: `#s.sequence ≤ s.treatedAttacks`.

  An output whose lines carry no results (all `OutcomeSummary.attacksAssessed = 0`, which INV-074 then demands) satisfies every invariant, yet shows neither per-attack effectiveness, nor its consistency, nor the absence of the most bothersome symptom per attack. The model requires `intakeTiming` and, for migraine, `symptomStatus` on each line (INV-072, INV-076), but not the outcome results, which are the substance of "consistency".
- **Evidence:** OUT-023 Statement (quoted above); OUT-012 Statement: "both across periods and in the response of individual treated attacks (see OUT-023)"; INV-072 predicate as cited.
- **Required change:** extend INV-072 (SHOULD) so that:
  - (i) each line of `s.sequence` shows a result for each measure of `requiredOutcomes(s.earlyTimePoint)`, or at least for the early-time-point measures, including `mostBothersomeSymptomAbsent` for migraine;
  - (ii) the sequence lists the summarised treated attacks, for example `#s.sequence = s.treatedAttacks`, so that consistency across consecutive treated attacks is visible.

  Update the OUT-012 and OUT-023 traceability entries accordingly.

### R01-08 Formal defect: the last (incomplete) menstrual cycle has no defined span, and `completeCycles` is not tied to the cycles shown

- **Item(s):** E-060 (`CycleLine.cycle`, `completeCycles`), INV-087.
- **Problem:**
  - `cycle` is defined as running "from the first day of menstruation to the day before the next one". For the current cycle, the next menstruation does not exist, so `cycle.to` has no defined meaning. Yet `cycle` is `core` and every cycle line must have one.
  - `completeCycles` is a derived MUST field of OUT-030. Its only relation is `completeCycles ≤ #cycles`.
  - Under INV-087 an output that shows three cycles lying wholly inside the covered period can state "0 complete cycles", and an output can present an incomplete cycle as if it were complete.

  The number OUT-030 requires is a relation over shown elements (in scope: Stage 2 PROCESS.md section 2), but the model does not give it.
- **Evidence:** OUT-030: "MUST state how many complete cycles the view covers". E-060: `cycle : DateSpan core -- from the first day of menstruation to the day before the next one`; INV-087: `v.completeCycles ≤ #v.cycles`. Compare E-063, where `ongoing` and `lastDay` solve the same problem for cluster periods.
- **Required change:**
  - Add to `CycleLine` an explicit marker of completeness, for example `complete : 𝔹 core`, with `cycle.to` defined for an incomplete cycle (for example as the end of the covered period, as `lastDay` does in E-063). Require that only the last cycle can be incomplete.
  - Replace `completeCycles ≤ #cycles` by its defining relation over the shown cycles, for example `completeCycles = #{cl ∈ ran v.cycles | cl.complete ∧ v.covers.start ≤ cl.cycle.from ∧ cl.cycle.to ≤ v.covers.end}`, or by the author's equivalent reading of "complete cycles the view covers".

### R01-09 Coverage gap: the clinician-facing summary (INV-104) omits parts of the components OUT-034 names

- **Item(s):** INV-104, E-066, section 7 row OUT-034.
- **Problem:** OUT-034 brings together "frequency measures and their time course (OUT-004 to OUT-009)", "functional impact (OUT-027)" and the other outputs listed. INV-104 includes most of them, and by its own Note includes OUT-008 because it falls within "OUT-004 to OUT-009". It leaves out three parts:
  - (a) The time course (OUT-009) is required only for headache days. The series must show `HeadacheDays` per period, but not migraine days (for migraine), moderate/severe headache days or attacks. These are the frequency measures whose time course OUT-009 defines (INV-035 requires them in the time-course view).
  - (b) Of the three OUT-008 measures, headache-free days and symptom-free days are included, but "periods without migraine days" (E-022) is not. This is inconsistent with the stated reading (ISS-04).
  - (c) Functional impact includes only the "affected" days in the three domains, not the "days with severe functional impairment" that OUT-027 names.
- **Evidence:**
  - OUT-034 Statement (as quoted).
  - OUT-009: "frequency measures (OUT-004 to OUT-007) as a time series of consecutive reporting periods".
  - OUT-008: "headache-free days and symptom-free days per reporting period, and periods without migraine days".
  - OUT-027: "including days with severe functional impairment".
  - INV-104: `perPeriod(v, sr, HeadacheDays, allTypes)` is the only per-period content of the series; `∀ d ∈ {paidWorkOrSchool, householdWork, socialOrLeisure} • ∃ m ∈ v.content ∩ fiDays(d, affected) • …`.
- **Required change:** in INV-104:
  - require the series to show, per period, also migraine days (for migraine), moderate/severe headache days and attacks, as INV-035 does;
  - include `MigraineFreePeriodMark` consistently with ISS-04, or state in ISS-04 why it is excluded;
  - include the severe-impairment days of E-030 (as in INV-026).

### R01-10 Factual error (value set): MIDAS, PedMIDAS and HALT scores are stated as unbounded rationals

- **Item(s):** E-057 (`ScoreRange`, `scoreRange` axiom, Notes), E-058 (`totalScore : opt ℚ`), INV-082 Reading.
- **Problem:** The value type defines `high = ∅` as "no upper bound", and INV-082 reads "0 or more for MIDAS, PedMIDAS and HALT". These instruments are sums of day counts over a fixed recall period, in whole days, so their range is bounded and integer. The model's own Notes say only that "no upper bound is stated by the cited sources". The formal statement "no upper bound" (and a rational score such as 5.5, which lies between the MIDAS bands 0–5 and 6–10) misstates the value sets.
- **Evidence:**
  - [S-014] "the unit of each being whole days per one or 3 months" (quoted in E-057) and "HALT-90 [...] counts days affected by headache during the preceding 3 months (90 days)".
  - [S-101] "MIDAS included five questions, capturing information on missed days of work, household chores, non-work activity and days with substantially reduced productivity over a three-month period. A total score is calculated by adding the five headache-related disability items together." (Methods, "Data sources", MIDAS paragraph; verified in the Europe PMC XML of PMC3057423).
  - [S-103] "The score is a simple composite of the total of six questions." (section "About the PedMIDAS Questions").
- **Required change:**
  - Change the meaning of `high = ∅` to "the model states no upper bound" (not "the range has no upper bound"), and correct the INV-082 Reading. Alternatively, state cited maxima.
  - Restrict the total scores of the day-count instruments (MIDAS, PedMIDAS, HALT-90, HALT-30) to whole numbers, citing the quotes above.

### R01-11 Citation defect: wrong location of the S-105 developers statement

- **Item(s):** section 10, S-105 entry.
- **Problem:** The entry cites the developers sentence as "(manual, P. 9/9)". The sentence is on page "P.8/9", under the heading "QUESTIONS REGARDING DEVELOPMENT, ACKNOWLEDGMENTS AND USE". Page 9/9 is "SELECTED REFERENCES".
- **Evidence:** In the PDF at the listed URL (HTTP 200), PDF page 8, headed "PHQ and GAD-7 Instructions P.8/9", reads: "The PHQ family of measures (see Table 1, page 3), including abbreviated and alternative versions as well as the GAD-7, were developed by Drs. Robert L. Spitzer, Janet B.W. Williams, Kurt Kroenke and colleagues, with an educational grant from Pfizer Inc." PDF page 9 is headed "P.9/9" and contains "SELECTED REFERENCES".
- **Required change:** change the location to "P. 8/9, section 'Questions regarding development, acknowledgments and use'".

### R01-12 Stage 1 issue handling: ISS-07 is not a Stage 1 issue, and ISS-08 has no pointer from the element it affects

- **Item(s):** section 8 ISS-07 and ISS-08; E-045, E-046 and E-057 Notes.
- **Problem:**
  - ISS-07 states of itself "This is not a defect of Stage 1, which does not state the bands" and "no action needed". Section 8 is for gaps or defects found in Stage 1 (Stage 2 PROCESS.md sections 4 and 6), so an entry that is not one is unfounded there. The overlaps of the S-014 and S-008 bands are already described in the Notes of E-057 and E-045.
  - Section 8 says "Each issue is pointed to from the Notes of the elements it affects", and PROCESS.md section 4 requires such a pointer. But ISS-08, which determines the `ResponderCategory` variant of E-046, is referenced only from the traceability table. E-046 Notes contain no pointer to it.
- **Evidence:** ISS-07 text as quoted. A grep for "ISS-08" finds it only at the OUT-020 traceability row, the ISS-08 heading and the change log, not in E-046.
- **Required change:**
  - Withdraw ISS-07 from section 8, keeping the overlap descriptions in the E-045 and E-057 Notes. Alternatively, reformulate it as a genuine Stage 1 issue, if there is one.
  - Add "See ISS-08." to the Notes of E-046.

## Checked and not raised

- **The context (`OutputContext`, `SubjectProfile`) is not an input entity.**
  - Course events, available administrations and the start of withdrawal are stated as properties of the subject. Nothing is described as entered or recorded. "How these properties become known is outside the model."
  - They are needed to state the "for each preventive treatment" and "markers for every start, dose change and stop" parts of Stage 1.
  - The consistency invariants (INV-036, INV-079, INV-082 last conjunct, INV-085 last conjunct) relate shown values to subject properties, not to recorded data. I judged this within section 3.5 / PROCESS.md section 2. A future reviewer may wish to watch that these properties do not grow into a record model.
- **MIDAS grade labels.**
  - The labels of [S-102] ("little or no disability", …) are quoted exactly.
  - [S-101], also a source of the model, uses "minimal or infrequent disability" / "mild or infrequent disability" and attributes them to the MIDAS development paper (its ref. 30, Stewart et al. 2001 = S-044). [S-102] attributes its labels to Stewart et al. 2000 (Pain).
  - Both label sets are developer-attributed, the score bands agree, and E-057 Notes already disclose the divergence. No evidence makes one of them the sole correct label set.
- **Stage 1 issues.** ISS-01 (verified: ICHD-3 8.2.6 criterion B names only ergotamine, triptans, non-opioid analgesics and/or opioids), ISS-02 (verified: "simple analgesics" occurs only on p. 139, 10.1.1), ISS-03, ISS-04, ISS-05, ISS-06 and ISS-08 are founded, and the model follows Stage 1 with the deviation recorded. No Stage 1 issue was found that the model silently works around beyond R01-06.
- **ICHD-3 8.2 indicator.**
  - Correct: the reference levels (15 for 8.2.3; 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8) and the "> 3 months" span.
  - Checked by hand: the shortest-span relation of INV-045 yields 4 calendar months or 4 × 28 days.
  - The INV-046 combined-use relation matches 8.2.6 note 2.
  - The application of per-month levels to 28-day periods is disclosed in the E-032 Notes.
- **The perimenstrual window** (day 1 − 2 to day 1 + 2 = days −2 to +3, no day 0) is correct.
- **Remission:** `plusMonths(s, 3) ≤ e` correctly encodes "must exceed three months".
- **Control levels and thresholds:** the INV-064 control levels and the IHS Q6, NICE, DMKG and Russian thresholds match their quotes.
- **The AAN 14A rule** ("most medications") applied to all preventive types, anchored at the tolerated or target dose: a defensible reading of the guidance.
- **INV-091 / INV-093** (`concerns` for all-types values of mixed-type subjects): the scope reading is defensible given the OUT-037 Caveat, which limits the restriction to migraine and to AUC for tension-type headache.
- **INV-023** uses any granularity for acute-medication days. The monthly basis needed by INV-044 is guaranteed through `basis`, and OUT-001's monthly MUST concerns frequency outputs.
- **`acuteTreatments` and `acuteMedications`** are not linked by INV-001. This only adds admissible contexts (more obligations, no excluded outputs).
- **INV-081 / INV-082 "baseline administration"** is any earlier administration. Stage 1 does not define the baseline administration further.
- **OUT-031 "history of previous bouts":** represented by the chronological bout list over a selectable time range. Completeness against the true bout history would need input data and is out of scope.
- **The cluster summaries keep the 24-hour outcomes** (INV-072 with `fifteenMinutes`). This is a literal reading of OUT-023 ("the corresponding time point is 15 minutes").
- **INV-094** makes both the chosen period and the period since the previous consultation available. **INV-097** applies equal-length comparisons to every paediatric comparison. Both are faithful to the Stage 1 wording.
- **The HIT-6 recall of 1 month** agrees with [S-002] and with [S-101] ("a one-month recall of the HIT-6").
- **The S-014 quote "HALT-30 [...] records days affected during the preceding 1 month"** is used for the recall value, an output element, not for data collection.
- **Notation (section 2):** complete for every construct used (`is`, `≈`, `let`, `∃₁`, `Σ`, `min`/`max`, `first`/`last`, comprehensions, `→R`, `opt`/`set`/`seq`).
- **Partial terms:** all are guarded as section 2.6 states (checked for `days`, `periodEndFrom`, `÷`, `s(i)`, `first`/`last`, `max`, `classOf`, `spanOf`).
- **Satisfiability:** no unsatisfiable or contradictory invariant combination was found among INV-003 + INV-007, INV-055 + INV-056 + INV-097, INV-040 + INV-041, INV-044 + INV-045 + INV-003, or INV-086 + INV-087.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and there are no earlier review, fix or oscillation files for Stage 2.
