# Review — iteration 08 (re-check b)
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v07
Date: 2026-10-21

## Summary

This is an independent re-check of v07. Review 08 found no remarks. I verified everything again from the downloaded sources, Stage 1 v18 and the model, and I did not rely on that review's conclusions.

**What is sound**

- **Citations.** All 236 quoted source strings were found verbatim at their stated locations, and the metadata of S-101 to S-105 is correct.
- **Value sets.** These agree with their sources: the ICHD-3 labels, the 8.2 levels and the "> 3 months" span, the A1.1 window, the remission duration, the instrument ranges and bands, the responder thresholds, the control levels and the offsets of all 17 evaluation rules.
- **Mechanical checks.** IDs, references, traceability, declared names, attribute selections, the typing rule for levels and the form of the prohibitions are all clean.
- **Scope.** The scope sweep is clean.
- **Section 8.** Every entry is founded.

**Remarks**

Two defects need a change. Neither touches an oscillation watch point, and neither reverses an earlier fix.

- **R08b-01 (coverage gap, narrowing of OUT-020).** OUT-020 asks a responder label to show the other values its named criterion rests on, and its list of such values is open ("for example"). The model closes that list to its two examples, instrument results and acute-treatment effectiveness (`UnderlyingKind`, E-045). As a result, some criteria cannot be represented with the values they rest on:
  - attack frequency: Turkish protocol Box 8; Russian paediatric flowchart;
  - attack duration: Turkish protocol Box 8; Saudi consensus;
  - intensity: Danish reference programme; Russian paediatric flowchart.

  Stage 1 itself quotes these criteria as criteria of preventive success, except the Russian paediatric one, which is in a Stage 1 source.
- **R08b-02 (formal defect).** The membership criterion of the new component `EvaluationRule.excludes` (E-041) is stated in a form that the axiom values contradict:
  - The Meaning, the component comment and the Readings of INV-001, INV-055, INV-058 and INV-059 define it as "the types for which the same guidance names another time point". Yet `ruleNice1327.excludes = ∅`, although NICE CG150 names other time points for CGRP inhibitors (1.3.28) and for botulinum toxin type A (1.3.29).
  - The Notes justify NICE with "which names no exception". That reason applies equally to Turkish Box 8, which nonetheless excludes onabotulinumtoxinA.

  This item does not reopen the settled point that NICE 1.3.27 applies to onabotulinumtoxinA. The new evidence is the Turkish case, which did not exist before v07.

## Verification coverage

**Method.**

- **Downloads.** Every source was downloaded with `curl` into the fresh directory `/tmp/r08b-dl-SOAR`, outside the repository. All downloads returned HTTP 200. S-034 returned "connection reset" once and HTTP 200 on retry.
- **Extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML pages and Europe PMC full-text XML were tag-stripped and HTML-unescaped. The image-only title page of S-034 was rendered with `pdftoppm` and read.
- **Scripts.** Scripts were kept in the session scratchpad (`quotes.py`, `where.py`, `mech.py`, `names.py`, `strip.py`) and run with `python3 -I`.
- **Quote search.** Every double-quoted string outside the `omn` blocks was extracted (560 occurrences) with its nearest source tag and split at `[...]`. Each fragment was searched in three passes:
  1. after normalising whitespace, quotes and dashes;
  2. after also removing the unmapped glyphs (`≥`, `±`, `−`, `þ`) and line-end hyphens;
  3. letters and digits only.
- **Pages.** Pages were then listed for each location-sensitive quote and compared with the stated location.
- **Hand checks.** Every string matched only in pass 2 or 3 (42 strings) was read in context. All differ only by:
  - unmapped glyphs;
  - an upper-case heading in the source;
  - line breaks;
  - a typographic space next to "≥".

**Citations**

| Source (URL as listed; HTTP) | Quoted strings checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (Stage 1 URL; 200; 211 pp.) | 42 at these locations:<br>• labels, pp. 8, 9, 12;<br>• 8.2 Descriptions and criteria B, the 8.2.3 comment, the 8.2.6 note 2, pp. 122–125;<br>• A1.1.1/A1.1.2, p. 190;<br>• remission, p. 209;<br>• "simple analgesics", p. 139 only | 42. The A1.1 window strings were checked by hand on p. 190: the layer shows "day 1  2 (i.e. days 2 to þ3)". | 0 | 0 |
| S-007 (UCL manuscript; 200; 39 pp.) | 6 | 6 | 0 | 0 |
| S-008 IHS 2024 (univaq; 200; 31 pp.) | 19 (Q2 p. 9, Q6 pp. 12–13, Q13 p. 17) | 19 | 0 | 0 |
| S-010 IHS 2025 (univaq; 200; 11 pp.) | 21 (p. 6) | 21 | 0 | 0 |
| S-011 EHF 2022 (Europe PMC XML and PMC page; 200) | 6 | 6 | 0 | 0 |
| S-014 (Europe PMC XML; 200) | 24 | 24 | 0 | 0 |
| S-015 NICE CG150 (Recommendations and Overview pages; 200) | 20 | 20 | 0 | 0 |
| S-016 SIGN 155 (64-page PDF; 200) | 6 (PDF p. 7 = printed p. 1; section 4.1 on PDF p. 20 = printed p. 14) | 6 | 0 | 0 |
| S-018 AAN/AHS Clinician Summary (12-page PDF; 200) | 11 (pp. 1, 7, 8) | 11 | 0 | 0 |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML; 200) | 5 | 5 | 0 | 0 |
| S-028 NVN module (page; 200) | 7 | 7 | 0 | 0 |
| S-033 Russian adult (92-page PDF; 200) | 17 (pp. 1, 4, 5, 39, 40, 41) | 17 | 0 | 0 |
| S-034 Russian paediatric (53-page PDF; 200 on retry) | 7 (pp. 17, 52; title page read as an image: "Возрастная группа дети") | 7 | 0 | 0 (one "connection reset", then 200) |
| S-035 Turkish protocol (92-page PDF; 200) | 9 (pp. 7, 47, 48, 57, 77) | 9 | 0 | 0 |
| S-101 (Europe PMC XML; 200) | 5 | 5 | 0 | 0 |
| S-102 (Europe PMC XML; 200) | 9 | 9 | 0 | 0 |
| S-103 PedMIDAS page (200; footer "© 2026") | 14 | 14 | 0 | 0 |
| S-104 (Europe PMC XML; 200) | 2 | 2 | 0 | 0 |
| S-105 PHQ/GAD-7 manual (200; 9 pp.) | 6 (P.6/9, P.8/9) | 6 | 0 | 0 |
| **Total** | **236** | **236** | **0** | **0** |

**Further checks**

- **Other quoted strings.** 191 further strings are verbatim Stage 1 v18 text reused by reference. The remaining 47 unmatched strings are:
  - English translations;
  - the model's own terms;
  - PubMed and web query strings;
  - the A1.1 glyph strings checked by hand.
- **Translations.** The new Russian, Turkish and Dutch translations are faithful. Among them:
  - "Контроль эффективности терапии через 3мес." = "monitoring of the efficacy of therapy after 3 months";
  - "Yeterli süre, etkinlik için en az 2-3 ay …" = "The adequate duration is at least 2–3 months for efficacy …".
- **Metadata (PubMed esummary).** All correct:
  - S-101: Cephalalgia 2011;31(3):357–67, PMID 20819842, PMC3057423, DOI 10.1177/0333102410379890;
  - S-102: J Headache Pain 2015;16:24, PMID 25902814, PMC4406925, seven authors;
  - S-104: Health Qual Life Outcomes 2003;1:29, PMID 12914662;
  - the S-103 developer paper: Neurology 2001;57(11):2034–9.
- **Newer versions.** None found:
  - Russian paediatric recommendations: still the 2024 version ("пересмотр не позднее 2026"), confirmed by web search;
  - Turkish protocol: no revision after August 2025 found by web search;
  - NICE CG150: 1.3.27 "[2012, amended 2025]".

**Per-OUT fidelity check (Statement, Caveats, strength, traceability row)**

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK | 021 | OK |
| 002 | OK | 022 | OK (ISS-03) |
| 003 | OK (SHOULD / SHOULD NOT) | 023 | OK (INV-107) |
| 004 | OK | 024 | OK |
| 005 | OK | 025 | OK (MAY) |
| 006 | OK | 039 | OK |
| 007 | OK | 026 | OK (ISS-06) |
| 008 | OK (MAY; ISS-04) | 027 | OK |
| 009 | OK | 028 | OK (ISS-03) |
| 010 | OK | 029 | OK (ISS-09) |
| 011 | OK | 030 | OK (watch points not examined for change) |
| 012 | OK | 031 | OK |
| 013 | OK (MAY) | 032 | OK |
| 014 | OK (ISS-02) | 033 | OK |
| 015 | OK | 034 | OK |
| 016 | OK (ISS-01, ISS-09) | 035 | OK |
| 017 | OK (ISS-11) | 036 | OK ((d) checked against S-005 primary endpoints and the S-034 flowchart; ISS-10) |
| 018 | All 17 rules agree with their texts. **R08b-02**: the stated criterion of `excludes` contradicts the values. | 037 | OK |
| 019 | OK (ISS-05) | 038 | OK |
| 020 | **R08b-01**: the "other values" are closed to two kinds. The row's "full" is therefore incorrect. | | |

**Mechanical checks**

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108); none missing, no duplicates |
| References | No dangling E- or INV- reference.<br>S references lie within S-001–S-046 and S-101–S-105; OUT references within 001–039.<br>ISS headings are ISS-01–06 and ISS-08–11; ISS-07 occurs only as the withdrawn ID. |
| Realises and traceability | Each item has exactly one Realises field.<br>39 rows, in Stage 1 order (OUT-039 after OUT-025).<br>0 differences between the rows and the union of the Realises fields.<br>No coverage text names an ID outside its row.<br>All rows read "full". |
| Names in `omn` blocks | 515 declared names, none declared twice.<br>Every attribute selection is declared on a type.<br>After string literals are removed, every remaining undeclared identifier is a bound variable or parameter (`Ks`, `K`, `L`, `A`, `D`, …). |
| Typing rule for levels | No SHOULD, MAY or MUST-with-`when` attribute lacks an `opt`, `set` or `seq` type, and none uses `set1` or `seq1`. |
| Invariant levels | MUST 19; MUST NOT 2 (INV-048, 106); SHOULD 47; SHOULD NOT 8 (INV-013, 021, 043, 065, 084, 091, 101, 107); definitional 32.<br>Every MUST NOT / SHOULD NOT predicate begins with `¬`. |
| Scope sweep (enter/entry/record/input/capture/store/persist/database/JSON/XML/CSV/FHIR/HL7/serialise/encode/retention/answer/reminder/obtained/calculated/computed/algorithm/logged, "diary information", "diary data") | 40 hits, all of them:<br>• exclusion statements;<br>• out-of-scope notes;<br>• omitted-word notes;<br>• text inside quotes;<br>• wording accepted in earlier reviews.<br>No relation takes input data. |
| Thresholds and formulas that are part of the output data | All present and quoted. The exception is the representational gap of R08b-01: the values that a named criterion rests on, when they are attack counts, durations or intensities. |
| Earlier remarks | `UnderlyingKind` is unchanged since v00, and no review or fix log mentions `UnderlyingKind` or `alsoRestsOn` (checked with `grep`). |

## Remarks

### R08b-01 Coverage gap (narrowing of OUT-020): the "other values" a named criterion rests on are closed to instrument results and acute-treatment effectiveness
- Item(s): E-045 (`UnderlyingKind`, `alsoRestsOn`, `valueAvailable`, `ReductionComponent.measures`); E-046 (`otherValues`); INV-062; section 7 row OUT-020.
- Problem:
  - **What Stage 1 requires.** OUT-020 (SHOULD) asks that a responder label show the underlying values of OUT-018 and OUT-019 "and, where the named criterion also rests on other values, those values as well (for example the results of instruments and of patient global impression of change in OUT-026, or the effectiveness of acute treatment in OUT-023)". The criterion itself is any criterion the reader applies (OUT-018 Caveats; OUT-020 "for example").
  - **What the model does.** `ResponderLabel.criterion` may hold any `ResponderCriterion`, but such a criterion can declare only two kinds of other values: `variant UnderlyingKind ::= instrumentResultOf ⟨Instrument⟩ | acuteTreatmentEffectiveness`.
    - E-046 `otherValues` is required only `when … ∃ u ∈ k.alsoRestsOn`.
    - INV-062 requires specific other values only for these two kinds.
    - A reduction component can only name a `DayMeasure`, so a threshold on attack frequency cannot be a decidable component either.
  - **Consequence.** For a criterion that rests on attack frequency, attack duration or intensity, no constraint requires those values to be shown with the label. The Stage 1 "for example" list is closed to its examples. This is the same kind of narrowing as R03-06, where the open list of instruments had been closed.
  - **Example.** A clinician applies the Turkish protocol criterion "Ölçüt atak sıklığında en az %50 azalma olması" (the criterion is a reduction of at least 50 % in attack frequency). The label's criterion must then be a `judgement` with `alsoRestsOn = ∅`. INV-062 requires only the response comparison, which shows headache and migraine days, and the residual burden. It does not require the attack counts of the baseline and evaluated periods on which the criterion rests.
  - **Not considered before; not a reversal.** `UnderlyingKind` has had the same two tags since v00. Review 08 noted that the Turkish criterion is absent from `namedCriteria` and judged that "`ResponderLabel.criterion` may hold any `ResponderCriterion` value". It did not consider that the type cannot express what such a criterion rests on. No earlier review or fix mentions `UnderlyingKind`.
- Evidence:
  - Stage 1 OUT-020 Statement, quoted above (line "If the output displays a responder or non-responder label, it SHOULD name the criterion applied (for example …) and SHOULD always show the underlying values (OUT-018, OUT-019) and, where the named criterion also rests on other values, those values as well (for example …)").
  - Model E-045: `variant UnderlyingKind ::= instrumentResultOf ⟨Instrument⟩ | acuteTreatmentEffectiveness`; `value ReductionComponent { measures : set1 DayMeasure; … }`. E-046: `otherValues : set →Item SHOULD when ∃ k ∈ self.criterion • ∃ u ∈ k.alsoRestsOn • valueAvailable(ctx, u)`.
  - [S-035] "► Ölçüt atak sıklığında en az %50 azalma olması," (Kutu 8 "Migren Profilaktik Tedavi-Yönetim-6", second item, PDF p. 48). Translation: "The criterion is a reduction of at least 50% in attack frequency."
    - The same box distinguishes attacks from days on p. 47: "Ayda 2'den fazla atağın veya ayda 4'ten fazla ağrılı günün olması" (more than 2 attacks or more than 4 painful days a month).
    - URL: https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon)%20(92%20Sayfa).pdf
  - Success criteria that rest on attack frequency, duration or intensity, quoted in Stage 1 itself:
    - [S-035] "Profilaktik tedavinin başarısı, atak sıklığında ve süresinde %50'lik bir azalma ve akut atakta ilaçlara artan yanıt ile değerlendirilir." (Stage 1 OUT-011, OUT-021, OUT-023; attack frequency, attack duration and acute response);
    - [S-030] "Profylaktisk behandling anses generelt for succesfuld, hvis hyppigheden eller styrken af migræne kan halveres […]" (Stage 1 OUT-010; frequency or intensity);
    - [S-042] "Significant decrease in attack duration based on patient’s headache diary" (Stage 1 OUT-011).
  - [S-034] "Отсутствие положительной динамики частоты и тяжести приступов в течение 3мес: коррекция профилактической терапии" (Приложение Б, flowchart "Алгоритм диагностики и ведения пациента с мигренью", p. 52; the same flowchart from which `ruleRuChildren` is taken). Translation: "Absence of positive dynamics in the frequency and severity of attacks within 3 months: correction of the preventive therapy." URL: https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=169_3
- Required change:
  - **Open the set of other values.**
    - Let a criterion declare that it rests on further per-period output values. Two forms are acceptable:
      - a tag such as `periodValuesOf ⟨ℙ PeriodValue⟩`;
      - tags for attack counts, intensity summaries, duration summaries and functional-impact days, plus an open tag.
    - Extend `valueAvailable`, for example with `provides(K)` for such a kind.
    - In INV-062 (SHOULD), require the label's view to show values of each such kind for the baseline period of the label's response comparison and for each evaluated period.
  - **Attack-frequency thresholds.** Either:
    - allow a reduction component over attack counts, so that a criterion such as Turkish Box 8 carries its threshold as a decidable component (INV-063 keeps deciding only what the shown values decide); or
    - state in the E-045 Notes why such thresholds are `judgement` components.
  - **Text.** Update the E-045 Meaning and Notes, the E-046 Notes and the section 7 row OUT-020. Every new relation must take output elements only.

### R08b-02 Formal defect: the stated membership criterion of `EvaluationRule.excludes` contradicts the rule values (NICE 1.3.27 vs Turkish Box 8)
- Item(s): E-041 (`excludes` component comment, Meaning, Notes "Types and exclusions"); E-008 Notes; Readings of INV-001, INV-055, INV-058 and INV-059; section 7 row OUT-018.
- Problem:
  - **The stated definition.** The model defines `excludes` as "the types for which the same guidance names another time point". The INV-059 Reading (MUST) says that the time points apply "to its type, unless the same guidance names another time point for a type the treatment has"; INV-001 and INV-055 say the same.
  - **The NICE value.** `ruleNice1327` has `excludes ↦ ∅`. Yet the same guidance, NICE CG150, names another time point for CGRP inhibitors (1.3.28, "after 12 weeks of treatment", `ruleNice1328`) and for botulinum toxin type A (1.3.29, "after 2 treatment cycles", `ruleNice1329`).
    - Read by its Reading, INV-059 would not require the NICE 1.3.27 time point for these treatments. Read by its predicate, it does.
    - So a MUST invariant's Reading contradicts its predicate, and the stated definition of the component contradicts one of its 17 values.
  - **The NICE rationale.** The E-041 Notes justify the NICE value with "NICE CG150 1.3.27, which names no exception, applies to it as to every preventive treatment (1.3.29 adds the stopping rule for botulinum toxin type A)". Turkish Box 8 also names no exception, yet `ruleTrBox8` excludes onabotulinumtoxinA.
    - Its section 3.6.3.9 has the same form as NICE 1.3.29: evaluate after N cycles, and stop when there is no benefit.
    - So the stated reason does not distinguish the two cases that the model treats oppositely.
  - **The criterion actually applied.** The criterion that does yield the values appears only in fix-iter-07: the end of the second cycle lies within the NICE 3–6-month window, while the Turkish 3-cycle time point lies after the 2–3-month window of Box 8. It is not stated in the model.
  - **Why this matters.** `excludes` decides which MUST time points INV-055 and INV-059 require. With the stated definition, a later fixer who extends the rule list, or who applies the definition literally to NICE, would change MUST obligations.
  - **Not a reversal.** This remark does not ask to change whether NICE 1.3.27 applies to onabotulinumtoxinA; review 07 settled that. It concerns the criterion added in v07. The Turkish rules, which are the new evidence, did not exist when review 07 judged NICE.
- Evidence:
  - E-041 (model): "`excludes : set PreventiveTreatmentType -- the types for which the same guidance names another time point`".
  - E-041 Meaning (model): "`excludes` lists the treatment types for which the same guidance names another time point: the rule does not apply to a treatment of such a type."
  - The `ruleNice1327` axiom: `excludes ↦ ∅`. The `ruleTrBox8` axiom: `excludes ↦ {onabotulinumtoxinA}`.
  - INV-059 Reading (model): "Every response comparison shows, in its view, the evaluation time points of all guidance rules that apply to the treatment: to its type, unless the same guidance names another time point for a type the treatment has, …".
  - [S-015] Under the heading "Prophylactic treatment review": "1.3.27 Review the need for continuing migraine prophylaxis 3 to 6 months after starting prophylactic treatment. [2012, amended 2025] 1.3.28 Stop CGRP inhibitors after 12 weeks of treatment if the frequency of migraines does not reduce by: […] 1.3.29 Stop botulinum toxin type A if the frequency of headache days per month does not reduce by at least 30% after 2 treatment cycles, […]". https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
  - [S-035] Kutu 8 (PDF p. 48): "► Yeterli süre, etkinlik için en az 2-3 ay ve tedavi için en az 6 aydır,". It is a general item with no exception.
  - [S-035] section 3.6.3.9 (PDF p. 57): "Hastalar 3 enjeksiyon siklusu sonra değerlendirilmeli ve fayda görmeyen hastalarda tedavi kesilmelidir." Translation (E-041): "Patients should be evaluated after 3 injection cycles, and treatment should be stopped in patients who do not benefit."
  - E-041 Notes (model): "the Turkish protocol evaluates onabotulinumtoxinA after 3 injection cycles against the at least 2–3 months of Box 8; so `ruleRu71` and `ruleTrBox8` also exclude onabotulinumtoxinA" and "NICE CG150 1.3.27, which names no exception, applies to it as to every preventive treatment (1.3.29 adds the stopping rule for botulinum toxin type A)".
  - fixes/fix-iter-07.md, Other changes 1: "NICE 1.3.27: no exception in NICE, and the end of the second botulinum cycle (about 24 weeks) lies within its 3–6-month window."
- Required change:
  - **State the criterion that decides membership of `excludes`, and apply it to every rule.** Update:
    - the component comment and the E-041 Meaning;
    - the E-041 Notes (replace the NICE rationale "names no exception");
    - the E-008 Notes;
    - the INV-001, INV-055, INV-058 and INV-059 Readings;
    - the OUT-018 row.
  - **Option (a).** "The types for which the same guidance names, for that type, a time point after this rule's time point or window, so that this rule would place an assessment before the guidance's own time point for that type."
    - This criterion gives the current values:
      - AAN 14A, Russian 7.1 and Turkish Box 8 exclude onabotulinumtoxinA;
      - NICE 1.3.27 excludes nothing, because 12 weeks comes before its window and the end of the second cycle lies within it.
    - Check every rule against it and state the result in the Notes.
  - **Option (b).** Another criterion, stated explicitly and supported by the guidance texts, with the values changed to follow it, for example treating NICE 1.3.27 and Turkish Box 8 alike.

## Checked and not raised

- **Russian paediatric rule (`ruleRuChildren`).**
  - The flowchart box (p. 52) is in the branch on preventive therapy and reads "… назначение препаратов для профилактической терапии мигрени с учетом коморбидности. Контроль эффективности терапии через 3мес."; `atOffset` 3 months from the start is correct.
  - The population is correct: title page "Возрастная группа дети" (read on the image), and p. 17 "детей и подростков".
  - The document mentions neither botulinum toxin nor monoclonal antibodies (no "ботулин", "БТА" or "моноклональн" on any page), so `excludes ↦ ∅` is consistent.
  - Including the rule under OUT-018 is recorded for the human in ISS-10, so it is not silent.
- **Age reading of the Turkish rules (`anyAge`).**
  - Section 3 is not limited to adults:
    - Table 6 (pp. 51–52) gives "Siproheptadin 0.25-1.5 mg/kg" and "B-C- erişkin, U-çocuk";
    - Box 8 lists "Yaş" among factors to consider.
  - Section 6 (children, pp. 77–80) names no evaluation time point. Its "Tedavi süresi en az 4 ay" is a treatment duration.
  - For 3.6.3.9 (onabotulinumtoxinA), the protocol states no age, and section 6 does not list the drug for children. Reading it as `anyAge` is the literal reading and is defensible.
- **Turkish Box 8 criterion vs `namedCriteria`.** `namedCriteria` is defined as the criteria named in the Stage 1 evidence of OUT-018 and OUT-020, and the Box 8 criterion is not among them. `namedCriteria` is used in no invariant. Its membership is therefore not a remark; the substantive gap is R08b-01.
- **Turkish Box 8 window reading** ("en az 2-3 ay" read as a window of 2 to 3 months). This is the same reading as the settled AAN 14A and NVN readings.
- **S-005 and OUT-036 (d).** The IHS paediatric primary endpoints are the "Change in headache frequency, as measured by headache days or migraine days" and the 50 % responder rate. These match the response comparison.
- **Completeness of the rule list.** I read the following independently: AAN 14A–14H (pp. 7–8); NICE 1.3.9, 1.3.24–1.3.29, 1.3.39 and 1.3.48; IHS Q2 (p. 9); Turkish sections 3.6.2–3.6.3.10 and 6. I found no time point that is missing.
  - NICE 1.3.25 calls rimegepant an oral "CGRP inhibitor", which `cgrpInhibitor` covers.
  - Turkish section 3.6.3.6 (anti-CGRP mAbs) names no time point.
- **INV-059 shows every applicable time point in every comparison.** This is consistent with PROCESS section 2, which lists "the evaluation time points shown with a response comparison (OUT-018)" as data shown to the reader.
- **HADS subscales only (INV-085).** This follows the developer [S-104]. Review 05 judged the same.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the AAN 14A and NVN window readings;
  - INV-023 at any granularity;
  - the "> 3 months" reading of INV-045;
  - the MIDAS label choice;
  - the 24-hour outcomes for cluster summaries;
  - "history of previous bouts";
  - the OUT-031 end-of-bout Caveat;
  - the context as subject properties;
  - the HIT-6 one-month recall;
  - the cluster remission "> 3 months";
  - labels under a criterion that does not apply;
  - the E-060 lead-in wording;
  - NICE 1.3.27 applying to onabotulinumtoxinA (R08b-02 does not change this);
  - "baseline administration" as any earlier administration (review 01).
- **Oscillation watch points.** The INV-087 start and lead-in, E-060, E-061, INV-105 and INV-104 are unchanged in v07 and are touched by no remark here.
- **Section 8.**
  - ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded. Re-verified: the 8.2.6 criterion B; "simple analgesics" only on p. 139; NICE 1.3.9 and 1.3.39 without review time points; the scope of 1.3.48.
  - Each issue is pointed to from the elements it affects.
  - R08b-01 and R08b-02 are model defects, not Stage 1 issues.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and the oscillation check after iteration 04 froze nothing.
