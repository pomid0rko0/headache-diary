# Review — iteration 09
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v08
Date: 2026-10-21

## Summary

This is an independent fact-check and review of v08. I read PROCESS.md, Stage 1 v18 sections 1–3 in full (OUT-001 to OUT-039) and sections 5–7 as needed, v08 in full, reviews 07, 08 and 08b, fix log 08 and the oscillation check after iteration 08. I verified every quote from freshly downloaded sources and re-ran the mechanical checks with my own scripts. I did not rely on the conclusions of earlier reviews.

**What is sound**

- **Citations.** All 277 source-quote fragments checked were found at their stated locations: 253 by the first script pass and 24 by a second pass. The 24 were fragments whose nearest source tag was another source, or whose link text has a space before the full stop. The metadata of S-101 to S-106 is correct. No source used has a newer version that changes an element.
- **Value sets and thresholds.** These agree with their sources:
  - the ICHD-3 code labels, the 8.2 reference levels and "> 3 months" span, the A1.1 window and the cluster-remission duration;
  - the HIT-6, MIDAS, PedMIDAS and HALT-90 ranges and bands, and the HADS, PHQ-9 and GAD-7 ranges;
  - the six named responder criteria and the IHS 2025 control levels;
  - the offsets and populations of the 17 evaluation rules, and the v08 timing arithmetic behind `excludes`.
- **Mechanical checks.** IDs, references, traceability, declarations, the typing rule for levels and the form of the prohibitions are all clean.
- **Scope.** The scope sweep is clean.
- **Section 8.** Every entry is founded.

**Remark**

- **R09-01 (formal defect; infidelity to OUT-020).** The relations that decide a responder label (E-046, INV-063) accept a change, or a pair of attack counts, of any type scope. The output may show values for a single headache type, for example tension-type headache in a subject who also has migraine. A value for a single headache type can then force the label to "responder" or "non-responder" even when the named criterion, applied to the measure it names (the person's headache days, migraine days, moderate/severe headache days or attacks), gives the opposite result.
  - The model's own control-level relation (`levelDays`) and the comparison's required values (INV-056, INV-057) use all types combined.
  - The v08 attack-reduction component and INV-062 (a) ("∃ sc : TypeScope") carry the same gap.
  - No earlier review or fix considered the type scope of the deciding values. The remark adds a tie of the same kind as R05-02 and relaxes none.

## Verification coverage

**Method.**

- **Downloads.** Every source was downloaded with `curl` into the fresh directory `/tmp/r09-dl`, outside the repository. All 24 downloads returned HTTP 200, plus TA260 section 1 (200) and two Russian version probes.
- **Extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML pages and Europe PMC full-text XML were tag-stripped and HTML-unescaped. The image-only title page of S-034 was rendered with `pdftoppm` and read ("Возрастная группа дети", "2024").
- **Scripts.** `quotes.py`, `findall.py`, `mech.py`, `names.py` and `strip.py` are in the session scratchpad and were run with `python3 -I`.
- **Quote search.** `quotes.py` extracted every double-quoted string outside the `omn` blocks (600 fragments after splitting at `[...]`) with its nearest source tag and searched it in that source in three passes:
  1. whitespace, quotes and dashes normalised;
  2. also glyphs without a text mapping (≥, ±, þ) and line-end hyphens removed;
  3. letters and digits only.

  `findall.py` searched the remaining substantive fragments across all sources. Page numbers were listed for every PDF quote and compared with the stated location.

**Citations**

| Source (URL as listed; HTTP) | Quote fragments checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (Stage 1 URL; 200; 211 pp.) | 53: labels pp. 8, 9, 12; 8.2 to 8.2.8 pp. 122–125; A1.1 p. 190; remission p. 209; "simple analgesics" only on p. 139 | 53. Of these, 16 matched only after the unmapped "≥", "±" and "−" glyphs, footnote markers and line-end hyphens were removed; I read pp. 123–125, 190 and 209 by hand. | 0 | 0 |
| S-007 (UCL manuscript; 200; 39 pp.) | 8 | 8 (pp. 10, 22, 25) | 0 | 0 |
| S-008 IHS 2024 (univaq; 200; 31 pp.) | 18 | 18 (Q2 p. 9, Q6 pp. 12–13, Q13 p. 17) | 0 | 0 |
| S-010 IHS 2025 (univaq; 200; 11 pp.) | 25 | 25 (p. 6; one sentence interrupted by a running header, as stated) | 0 | 0 |
| S-011 EHF 2022 (Europe PMC XML; 200) | 6 | 6 | 0 | 0 |
| S-014 (Europe PMC XML; 200) | 24 | 24 | 0 | 0 |
| S-015 NICE CG150 (Recommendations and Overview pages; 200; "Last updated 03 June 2025") | 27 | 27 (acupuncture 1.3.9 and the 1.3.26 TA260 link differ only by a space before the full stop at link text) | 0 | 0 |
| S-016 SIGN 155 (200; 64 pp.) | 8 | 8 (PDF p. 7 = printed p. 1; PDF p. 20; headings in capitals) | 0 | 0 |
| S-018 AAN/AHS Clinician Summary (200; 12 pp.) | 10 | 10 (pp. 1, 7, 8) | 0 | 0 |
| S-023 (Europe PMC XML; 200) | 3 | 3 | 0 | 0 |
| S-028 NVN module (200) | 13 | 13 | 0 | 0 |
| S-033 Russian adult (200; 92 pp.) | 20 | 20 (pp. 1, 4, 39, 40, 41, 53) | 0 | 0 |
| S-034 Russian paediatric (200; 53 pp.) | 10 | 10 (p. 17; p. 52; title page read as image) | 0 | 0 |
| S-035 Turkish protocol (200; 92 pp.) | 18 | 18 (pp. 7, 47, 48, 52, 57, 77). Kutu 8: the "Ölçüt …" item is the second item and "Yeterli süre …" the seventh, as stated. The 3.6.3.9 "3 ayda bir" sentence is two sentences before "Hastalar 3 enjeksiyon siklusu …", as stated. | 0 | 0 |
| S-101 (Europe PMC XML; 200) | 4 | 4 (Methods, "Data sources") | 0 | 0 |
| S-102 (Europe PMC XML; 200) | 7 | 7 ("Headache impact on functioning" > "Migraine-related disability") | 0 | 0 |
| S-103 PedMIDAS page (200) | 12 | 12 | 0 | 0 |
| S-104 (Europe PMC XML; 200) | 2 | 2 (section "Construction of the HADS") | 0 | 0 |
| S-105 PHQ/GAD-7 manual (200; 9 pp.) | 5 | 5 (P. 6/9, P. 8/9) | 0 | 0 |
| S-106 NICE TA260 (section 2, overview and section 1 pages; 200) | 4 | 4 (§2.1 last sentence; published 27 June 2012, last reviewed 11 January 2016; the §1 phrase in the search log) | 0 | 0 |
| **Total** | **277** | **277** | **0** | **0** |

**Further checks**

- **Other quoted strings.** 235 further strings are verbatim Stage 1 v18 text reused by reference. The remaining strings are:
  - English translations;
  - the model's own terms;
  - PubMed and web query strings;
  - fragments created where the script paired quote marks across text.
- **Translations.** The two Turkish translations new in v08 are faithful:
  - "Ölçüt atak sıklığında en az %50 azalma olması" = "The criterion is a reduction of at least 50% in attack frequency";
  - "Hasta fayda görüyorsa enjeksiyonlar 3 ayda bir …" = "If the patient benefits, the injections should be continued every 3 months …".
- **Metadata.** Checked with PubMed esummary; all correct:
  - S-101: Cephalalgia 2011;31(3):357–67, PMID 20819842, PMC3057423;
  - S-102: J Headache Pain 2015;16:24, PMID 25902814, seven authors;
  - S-104: HQLO 2003;1:29, PMID 12914662;
  - S-103 developer paper: Neurology 2001;57(11):2034–9, PMID 11739822;
  - S-106: TA260 dates as listed.
- **Newer versions.** None found that changes an element:
  - ICHD-3 is still current; only "ICHD-4 – Work in Progress 1" (Cephalalgia 2024) exists ([fis.uke.de record](https://fis.uke.de/portal/en/publications/international-classification-of-headache-disorders4--work-in-progress-1(b2e76945-6b60-4911-9c1f-583c088a2d4c)/export.html); [IHS classification committee](https://ihs-headache.org/en/about-ihs/standing-committees/classification/));
  - NICE CG150 still reads "Last updated 03 June 2025";
  - the Russian API returns byte-identical files for the version ids 295_4/295_5/295_9 and 169_3/169_4, so the cited 2024 versions are current.

**Per-OUT fidelity check** (Statement parts, Caveats, strength and traceability row, for each of the 39 requirements)

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK | 021 | OK |
| 002 | OK | 022 | OK (ISS-03) |
| 003 | OK (SHOULD; SHOULD NOT INV-013; open form E-013) | 023 | OK (INV-107) |
| 004 | OK | 024 | OK |
| 005 | OK | 025 | OK (MAY) |
| 006 | OK (INV-016 SHOULD; INV-108 MUST where provided) | 039 | OK |
| 007 | OK | 026 | OK (ISS-06) |
| 008 | OK (MAY; ISS-04) | 027 | OK |
| 009 | OK | 028 | OK (ISS-03) |
| 010 | OK | 029 | OK (ISS-09) |
| 011 | OK (INV-020, INV-021) | 030 | OK (watch points; unchanged since v04) |
| 012 | OK | 031 | OK |
| 013 | OK (MAY) | 032 | OK (MAY; caveats SHOULD) |
| 014 | OK (ISS-02) | 033 | OK |
| 015 | OK | 034 | OK (ISS-04; unchanged since v03) |
| 016 | OK (ISS-01, ISS-09) | 035 | OK (ISS-03) |
| 017 | OK (ISS-11) | 036 | OK (ISS-10) |
| 018 | OK: 17 rules agree with their texts. The v08 `excludes` criterion reproduces the values: 168 days lies between ≤ 92 and ≥ 181 days for NICE; about 9 months lies after 2–3 months for Turkish Box 8. | 037 | OK |
| 019 | OK (ISS-05) | 038 | OK |
| 020 | **R09-01**: the label relations decide on values of any type scope. Otherwise OK, including the v08 open `UnderlyingKind`, the `where` clause (met by all 6 named criteria) and the attack-reduction arithmetic. | | |

**Mechanical checks**

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108), none missing and no duplicates. |
| References | No dangling E- or INV- reference.<br>S references lie within S-001–S-046 and S-101–S-106, and every S-1NN used has a row in section 10.<br>OUT references lie within 001–039.<br>ISS headings are ISS-01–06 and ISS-08–11; ISS-07 occurs only as the withdrawn ID. |
| Realises and traceability | Each item has exactly one Realises field.<br>39 rows, in Stage 1 order (OUT-039 after OUT-025).<br>0 differences between the rows and the union of the Realises fields.<br>No coverage text names an ID outside its row.<br>All 39 rows read "full". |
| Names in `omn` blocks | 539 declared names, enumeration constants and tags, none declared twice.<br>Every attribute selection is declared on a type.<br>Every remaining undeclared identifier is a bound variable or parameter, except `refs`, which section 2.5 defines. |
| Typing rule for levels | 0 violations: no SHOULD, MAY or MUST-with-`when` attribute lacks an `opt`, `set` or `seq` type, and none uses `set1` or `seq1`. |
| Invariant levels | MUST 19; MUST NOT 2; SHOULD 47; SHOULD NOT 8; definitional 32.<br>Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Scope sweep | Terms searched: enter, entry, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serial, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, "diary data", "diary information".<br>All hits in sections 1–9 were read. They are:<br>• exclusion statements;<br>• out-of-scope notes;<br>• Stage 1 wording ("covered by diary information", OUT-003);<br>• a verbatim source quote ("records days affected", [S-014], for the HALT-30 recall).<br>No relation takes input data. The v08 relations take shown counts, periods, changes, items and `provides`. |
| Thresholds and formulas that are part of the output data | All present and quoted (8.2 levels and span; A1.1 window; remission; instrument bands and ranges; responder thresholds; control levels; evaluation offsets; percentage change; totals; covered-day proportion; cluster rates). |
| Earlier remarks | The type scope of the values that decide a label is mentioned in no review or fix log, checked with `grep`. |

## Remarks

### R09-01 Formal defect (and infidelity to OUT-020): a responder label is decided by values of any type scope, so a value for one headache type can force a category that the named criterion does not give
- Item(s):
  - E-046 (`reductionMet`, `reductionDecided`, `attackReductionMet`, `attackReductionDecided`, Notes);
  - E-045 (`ReductionComponent`, `AttackReductionComponent`, Meaning and Notes);
  - INV-062 (conjuncts on `periodValuesOf` and on the changes of reduction measures);
  - INV-063 (Reading);
  - section 7 row OUT-020.
- Problem:
  - **Per-type values can appear with a label.**
    - The response comparison may show changes for one headache type. INV-053 requires only that a change compares two values of the same scope. INV-056 requires the all-types values but admits others. INV-061 explicitly gives a residual burden the scope of its change (`rb.migraineDays.typeScope = rb.change.compared.typeScope`).
    - A label may show attack counts of one type scope only. INV-062 requires them "∃ sc : TypeScope • …", and the scope may be `ofType(h)`.
  - **The deciding relations do not tie the scope.**
    - `reductionMet` is `∃ … ch ∈ rc.changes • … ch.reference.measure ∈ r.measures ∧ … 100 × (ch.reference.days − ch.compared.days) ≥ r.atLeastPercent × ch.reference.days`, with no condition on `ch.reference.typeScope`. `reductionDecided` likewise accepts a change of any scope.
    - `attackReductionMet` and `attackReductionDecided` (new in v08) require only `b.typeScope = f.typeScope`.
    - INV-063 (definitional) then forces "responder" when any shown scope meets a component, and "non-responder" when the shown scopes decide every component and meet none.
  - **Consequence.** In a subject who has migraine and another headache type (OUT-029), a value for that other type alone decides a criterion whose measure is the person's frequency.
  - **Example (all values admitted by v08).** Adult with migraine and tension-type headache. Preventive treatment with a start. Label naming `critRu71` (headache days, ≥ 50 %), with one evaluated month.
    - The response comparison shows headache days for all types, 20 at baseline and 14 in month 3 (a 30 % reduction).
    - It also shows headache days for `ofType(c2)`, 10 and 4 (60 %), and for `ofType(c1)`, 10 and 10. INV-030 holds.
    - `reductionMet` holds through the `ofType(c2)` change (100 × 6 = 600 ≥ 50 × 10 = 500), so INV-063 makes "responder" the only valid category.
    - The criterion, which concerns "число дней с ГБ" (the number of headache days) of the person, gives "not effective" for a 30 % reduction.
    - The same happens with an attack-reduction component (for example the Turkish Box 8 criterion) when the label shows tension-type attacks 6 → 2 next to all attacks 12 → 10.
    - The reverse also happens: when the label shows only `ofType(c2)` attack counts 6 → 5, it is forced to "non-responder" even if the person's attacks fell by 75 %.
  - **Why this is a defect.**
    - A definitional invariant excludes the label that OUT-020 permits (the named criterion applied to the values it names) and admits one that contradicts it.
    - The model is inconsistent with itself. The control levels are read on all types combined (`levelDays(L, p) ≙ daysOf(viewOf(L), migraineOrModerateSevereHeadacheDays, p, allTypes)`). The comparison's own required values (INV-056, INV-057) are all-types values.
    - The E-046 Notes state "Every component is evaluated on values of the label's own treatment and of the periods the label refers to", but the type scope is not tied.
  - **Not a reversal, and not considered before.**
    - R01-04 (`#L.evaluated = 1`) and R05-02 (`rc.treatment = L.treatment`; the `evaluationResult` / `pretreatmentBaseline` pair) tied the deciding values to the label's period and treatment. This remark asks for the missing tie of the same kind and relaxes neither.
    - It does not touch `UnderlyingKind`, `PeriodValueKind` or `otherValueNamed` (R08b-01), nor the fix-08 decision to keep intensity and duration thresholds as `judgement` components (oscillation watch point 5).
    - No review or fix log discusses the type scope of these relations.
- Evidence:
  - **Stage 1.**
    - OUT-020 Statement: "If the output displays a responder or non-responder label, it SHOULD name the criterion applied (…) and SHOULD always show the underlying values (OUT-018, OUT-019) …".
    - OUT-018 Caveats: "the output shows the change and names the criterion a reader chooses to apply (OUT-020), but does not itself decide on continuation".
    - OUT-029: "present frequency and acute medication outputs separately for each headache type (for example migraine and tension-type headache), as well as combined".
  - **The criteria's measures are the person's frequency, not a subset by headache type.**
    - [S-015] "Stop botulinum toxin type A if the frequency of headache days per month does not reduce by at least 30% after 2 treatment cycles, …" (rec. 1.3.29; https://www.nice.org.uk/guidance/cg150/chapter/Recommendations).
    - [S-033] "Рекомендуется считать профилактическое лечение М эффективным, если число дней с ГБ сокращается через 3 месяца терапии на 50% и более от исходного" (section 7.1, p. 53; https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=295_4).
    - [S-008] "a ≥ 50% decrease in monthly migraine days or moderate-to-severe headache days, optimally based on the use of a headache diary;" (Q6, p. 12).
    - [S-035] "Ölçüt atak sıklığında en az %50 azalma olması" (Kutu 8, second item, PDF p. 48; https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon)%20(92%20Sayfa).pdf).
  - **Model text.**
    - E-046 `reductionMet` and `reductionDecided`, as quoted under Problem.
    - `attackReductionMet`: "`∃ rc ∈ L.comparison; b, f ∈ L.otherValues ∩ AttackCount • … b.typeScope = f.typeScope ∧ b.count > 0 ∧ 100 × (b.count − f.count) ≥ a.atLeastPercent × b.count`".
    - `levelDays` (E-046), INV-056 and INV-057 (all `m.typeScope = allTypes`).
    - INV-061.
    - INV-062: "`∃ sc : TypeScope • ∀ p ∈ ran L.evaluated ∪ {rc ∈ L.comparison • rc.baseline} • ∃ m ∈ L.otherValues ∩ PeriodValue • m.period = p ∧ m.typeScope = sc ∧ valueOfKind(m, k)`".
- Required change:
  - **Tie the scope.** A reduction or attack-reduction component must be decided only on values of the type scope to which the criterion's measure refers. Values for a single headache type of a subject who also has another type must not force or exclude a category; the reader applies the named criterion to them (INV-062). Either option is acceptable:
    - **(a) All types combined.** Add `ch.reference.typeScope = allTypes` to `reductionMet` and `reductionDecided`, and `b.typeScope = allTypes` to `attackReductionMet` and `attackReductionDecided`. This is the scope at which INV-056 and INV-057 show the comparison's own values and at which `levelDays` reads the control levels.
      - In INV-062, require the per-period values of a `periodValuesOf` kind for the baseline and evaluated periods at `allTypes`, either instead of "∃ sc" or in addition to it.
      - Likewise require the changes of each reduction measure at `allTypes`.
      - Both are satisfiable wherever the diary provides the kind, as the fix-08 satisfiability pass shows for any scope.
    - **(b) A scope component.** Give `ReductionComponent` and `AttackReductionComponent` a component that states the scope of their measure, for example all types, or values that concern the criterion's headache type (`concerns`, E-012). State it for each named criterion with support from its text. Decide each component only on values of that scope, and let INV-062 require values of that scope.
  - **Text.** Update:
    - the E-045 Meaning and Notes, and the E-046 Notes ("Every component is evaluated on values of the label's own treatment, of the periods the label refers to and of …");
    - the INV-062 Reading and Notes, and the INV-063 Reading;
    - the section 7 row OUT-020.

    Every relation keeps taking output elements only. Keep the R01-04 and R05-02 ties.

## Checked and not raised

- **v08 changes to responder labels, apart from R09-01.**
  - `UnderlyingKind` with `periodValuesOf` and `otherValueNamed`, `PeriodValueKind`, `valueOfKind`, `valueAvailable` (with `provides`) and the `where` clause are well typed. All six named criteria satisfy the `where` clause.
  - The attack-reduction test uses shown counts only and is guarded (`b.count > 0`, no division).
  - The three per-period value types left out of `PeriodValueKind` are justified in the Notes: completeness indicators, marks of periods without migraine days, and cluster rates.
- **v08 `excludes` criterion (E-041).**
  - The arithmetic holds: 3 months ≤ 92 days, 6 months ≥ 181 days, and the end of the second 12-week cycle at 168 days.
  - TA260 §2.1 and the [S-035] "3 ayda bir" sentence read as quoted.
  - The short Readings of INV-001, INV-055 and INV-059 ("a later time point of its own (E-041 `excludes`)") point to the full criterion in E-041, and the axiom values fix the semantics. Not a remark (oscillation watch point 1; no value change asked).
- **INV-100 extended to instrument grades and screening results.** This follows OUT-038 "such as" and the [S-014] "indicating" wording, at SHOULD.
  - The model's definition of an indicator might also be read on cluster bouts and remissions. Stage 1 gives no evidence that these need the caveat, so requiring it would be an optional addition.
  - Narrowing INV-100 back would reverse fix-08 (watch point 6).
- **HALT unit "days" (E-058 `totalScore` comment) and `wholeNumberScores`.**
  - [S-014] says that question 5 "gives rise to a simple count for which the unit is not whole days" and is "included in the total summed score". The developers' Table 18 nevertheless labels the graded score "Days lost in last 3 months".
  - The model's unit follows the developers' table, and the total remains a whole number. Not a factual error.
- **ICHD-3 values.**
  - The 8.2.1–8.2.5 and 8.2.8 levels (10 or 15) and the 8.2.6 total of 10 read as quoted on pp. 122–125.
  - "Without overuse … 8.2.1–8.2.5" (note 2) matches `classesOf821to825`.
  - The A1.1 window and "there is no day 0" (p. 190) match `windowDaysBefore` and `windowDaysAfter`.
  - "must exceed three months" (p. 209) matches INV-089.
- **Instrument value sets.**
  - HIT-6: 36–78, with bands ≤ 49, 50–55, 56–59 and 60–78.
  - MIDAS: grades I–IV with bands 0–5, 6–10, 11–20 and ≥ 21, and a three-month recall.
  - PedMIDAS: bands 0–10, 11–30, 31–50 and > 50.
  - HALT-90: Table 18, including the overlap at 20.
  - HADS: subscales 0–21. PHQ-9: 0–27. GAD-7: 0–21.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the AAN/AHS 14A, NVN and Turkish Box 8 window readings;
  - INV-023 at any granularity;
  - the "> 3 months" reading of INV-045;
  - the MIDAS label choice;
  - the 24-hour outcomes for cluster summaries;
  - "history of previous bouts";
  - the OUT-031 end-of-bout Caveat;
  - the context as subject properties;
  - the HIT-6 one-month recall;
  - the cluster remission "> 3 months";
  - labels under a criterion that does not apply (review 02; this concerns unmet conditions, not type scope);
  - the E-060 lead-in wording;
  - NICE 1.3.27 applying to onabotulinumtoxinA;
  - "baseline administration" as any earlier administration;
  - "per month" read per evaluated month for control levels (INV-064).
- **Oscillation watch points.**
  - Untouched by R09-01: INV-087, E-060, E-061 and INV-105; INV-104; INV-050 and E-039; the E-041 dimensions; `ruleRuChildren`; the timing readings.
  - R09-01 concerns E-046 and INV-062 (watch point 5). It adds a tie and reverses none.
- **Section 8.**
  - ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded. I re-verified:
    - 8.2.6 criterion B;
    - "simple analgesics" only on p. 139;
    - NICE 1.3.9 and 1.3.39 without a review time point;
    - 1.3.48 in the medication-overuse section;
    - the [S-034] flowchart on p. 52.
  - Each issue is pointed to from the elements it affects. R09-01 is a defect of the model, not a Stage 1 issue.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist; the oscillation checks after iterations 04 and 08 froze nothing.
