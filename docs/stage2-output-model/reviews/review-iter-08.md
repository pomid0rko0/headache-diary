# Review — iteration 08
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v07
Date: 2026-10-21

## Summary

v07 fixes R07-01, R07-02 and R07-03 correctly, and the fix sweep added nothing that needs a change.

- **R07-01.** The rule list of E-041 has 17 rules. Every offset, anchor, timing and population matches the guidance text. The six new rules are `ruleIhsQ2Oral`, `ruleAan14B`, `ruleRu33Bta`, `ruleRuChildren`, `ruleTrBox8` and `ruleTr3639`.
- **R07-02.** The `excludes` mechanism is well typed. It removes onabotulinumtoxinA from AAN/AHS 14A, from Russian section 7.1 and from Turkish Box 8, and each of these guidelines names its own later time point for that treatment. The R01-02 guarantee is kept: only a listed type excludes a rule.
- **R07-03.** Both [S-011] quotes now carry their own paragraph locations, and both locations are correct.

The citation base is sound:

- all 294 quoted source strings were found verbatim at their stated locations;
- the bibliographic details of S-101 to S-105 are correct;
- none of the guidance used by the new rules has a newer version.

The mechanical checks, the scope sweep and the fidelity check of all 39 requirements are clean. Section 8 is founded, and no Stage 1 issue is worked around silently. No oscillation watch point is touched.

## Verification coverage

**Method**

- **Downloads.** Every source was downloaded with `curl` into the fresh directory `/tmp/r08-dl-pjiN`, outside the repository. All 22 downloads returned HTTP 200.
- **Extraction.**
  - PDFs were extracted page by page with `pdftotext -raw` and `-layout`.
  - HTML pages and Europe PMC full-text XML were tag-stripped and HTML-unescaped.
  - The image-only title page of [S-034] was rendered with `pdftoppm` and read.
- **Scripts.** All scripts are in the session scratchpad (`quotes.py`, `nf2.py`, `pages.py`, `classify.py`, `mech.py`, `names.py`) and were run with `python3 -I`.
- **Quote extraction.** Every double-quoted string outside the `omn` blocks was extracted (575 occurrences), split at `[...]`, and searched in three passes:
  1. after collapsing whitespace;
  2. after normalising quotes, dashes, ligatures and line-end hyphens, and removing the ICHD-3 glyphs that have no text mapping;
  3. comparing letters and digits only.
- **Unmatched strings.** Every string not found in the source tagged before it was searched in all downloaded sources and in Stage 1 v18. For every PDF hit, the page was compared with the stated location.
- **Distinct strings.** Of the distinct quoted strings:
  - 294 are source text, and all were found;
  - 114 are verbatim Stage 1 v18 text reused by reference;
  - 11 or more are translations;
  - the rest are the model's own terms and search-log query strings.

### Citations

| Source (URL as listed; HTTP status) | Quoted strings checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (Stage 1 URL; 200; 211 pages) | 74, at these locations:<br>• code labels, pp. 8, 9, 12;<br>• 8.2 Descriptions and criteria B, the 8.2.3 comment and 8.2.6 note 2, pp. 122–125;<br>• A1.1.1/A1.1.2 window and note 2, p. 190;<br>• remission, p. 209;<br>• "simple analgesics", p. 139 | 74. The two A1.1 window strings were checked by hand: "±", "−" and "+" are unmapped glyphs, and the text layer shows "+3" as "þ3". | 0 | 0 |
| S-002 IHS episodic trial guideline (Stage 1 URL; 200) | 4 (short Stage 1 strings) | 4 | 0 | 0 |
| S-007 (UCL accepted manuscript; 200; 39 pp.) | 8 (pp. 10, 22, 25) | 8 | 0 | 0 |
| S-008 IHS 2024 (univaq PDF; 200; 31 pp.) | 26 | 26 | 0 | 0 |
| S-010 IHS 2025 (univaq PDF; 200) | 24 (p. 6) | 24 | 0 | 0 |
| S-011 EHF 2022 (Europe PMC XML and PMC page; 200) | 7 | 7 | 0 | 0 |
| S-014 (Europe PMC XML; 200) | 24 | 24 | 0 | 0 |
| S-015 NICE CG150 (Recommendations page and Overview page; 200) | 21 | 21 | 0 | 0 |
| S-016 SIGN 155 (64-page PDF; 200) | 7 | 7 | 0 | 0 |
| S-018 AAN/AHS Clinician Summary (12-page PDF; 200) | 15 | 15 | 0 | 0 |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML; 200) | 5 | 5 | 0 | 0 |
| S-028 NVN module (web page; 200) | 9 | 9 | 0 | 0 |
| S-033 Russian adult recommendations (92-page PDF; 200) | 18 | 18 | 0 | 0 |
| S-034 Russian paediatric recommendations (53-page PDF; 200) | 8 | 8. "Возрастная группа" … "дети" was read on the rendered image of p. 1. | 0 | 0 |
| S-035 Turkish protocol (92-page PDF; 200) | 10 | 10 | 0 | 0 |
| S-101 (Europe PMC XML; 200) | 6 | 6 | 0 | 0 |
| S-102 (Europe PMC XML; 200) | 6 | 6 | 0 | 0 |
| S-103 PedMIDAS page (200; footer "2026 Cincinnati Children's Hospital Medical Center") | 14 | 14 | 0 | 0 |
| S-104 (Europe PMC XML; 200) | 2 | 2 | 0 | 0 |
| S-105 PHQ/GAD-7 instructions (9-page PDF; 200; author Kurt Kroenke; created 2010-06-22, modified 2014-04-16) | 6 (P. 6/9, P. 8/9) | 6 | 0 | 0 |
| **Total** | **294** | **294** | **0** | **0** |

**New v07 quotes, checked in context**

- **[S-008] Q2, p. 9.**
  - The Optimal recommendation opens with the oral-preventive sentence, directly before the injectable sentence.
  - The Essential sentence and the footnote "*See Q6 …" are on the same page.
  - Q13 (pp. 17–18) names no time point for children.
- **[S-018] p. 7.**
  - 14A, 14B (with the repeated phrase "before assessing efficacy") and 14C are on this page, each marked "Level B".
  - 14H is on p. 8, with "Level B" in the margin.
- **[S-033].**
  - Section 3.3 comments, p. 39: "эффективность БТА – минимум через 6 месяцев терапии".
  - p. 40: the BTA recommendation with "[85]".
  - p. 41: the anti-CGRP sentence, which gives the same date as `ruleRu71`.
  - p. 4: "М – мигрень". "БТА" is absent from pp. 4–5.
- **[S-034].**
  - p. 52: the flowchart box ending "Контроль эффективности терапии через 3мес.".
  - p. 17: "Диагностика мигрени у детей и подростков …".
- **[S-035].**
  - p. 48: Kutu 8; the "Yeterli süre" item is the seventh.
  - p. 57: section 3.6.3.9 "Hastalar 3 enjeksiyon siklusu sonra değerlendirilmeli …".
  - p. 77: the heading of section 6; it is also in the table of contents on p. 7.
- **[S-016] p. 7.** The sentence on children is "two sentences later", as stated.
- **[S-011] Europe PMC.** The body "Background" begins with paragraph Par12, and Par13 is the one-sentence second paragraph.

**Further checks**

- **Translations** of the new non-English quotes (Russian, Turkish, Dutch) are faithful.
- **Bibliographic details (PubMed esummary).** All correct:
  - S-101: Cephalalgia 2011;31(3):357–67, PMC3057423, DOI 10.1177/0333102410379890;
  - S-102: J Headache Pain 2015;16:24, the seven authors as cited, PMC4406925;
  - S-104: Health Qual Life Outcomes 2003;1:29, PMC183845;
  - the S-103 developer paper: Neurology 2001;57(11):2034–9.
- **Newer versions.** None that changes an element:
  - NICE CG150: "last updated" 2025-06-03 (page metadata);
  - AAN/AHS Clinician Summary: PDF of 21 August 2026;
  - Turkish protocol: the August 2025 revision is current, and no 2026 revision was found;
  - Russian paediatric recommendations: 2024, with revision due "не позднее 2026", and no newer version was found by web search. The apicr server returns the same file for every version suffix, so probing suffixes proves nothing.

### Per-OUT fidelity check (Statement, Caveats, strength, traceability row)

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
| 011 | OK | 030 | OK (watch points untouched) |
| 012 | OK | 031 | OK |
| 013 | OK (MAY) | 032 | OK |
| 014 | OK (ISS-02) | 033 | OK |
| 015 | OK | 034 | OK (watch point INV-104 untouched) |
| 016 | OK (ISS-01, ISS-09) | 035 | OK |
| 017 | OK (ISS-11) | 036 | OK. (d) is realised with time points restricted to the guidance populations, including `ruleRuChildren` (ISS-10). |
| 018 | OK. R07-01 and R07-02 fixes verified; all 17 rules checked against their quotes. | 037 | OK |
| 019 | OK (ISS-05) | 038 | OK |
| 020 | OK (ISS-08) | | |

**Conformance levels** of the invariants:

- MUST 19;
- MUST NOT 2 (INV-048, INV-106);
- SHOULD 47;
- SHOULD NOT 8 (INV-013, 021, 043, 065, 084, 091, 101, 107);
- definitional 32.

No level differs from the strength of the Stage 1 statement part it realises. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`.

### Mechanical checks

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001 to E-067) and 108 invariants (INV-001 to INV-108); none missing, no duplicates |
| References | No dangling E- or INV- reference.<br>S references lie within S-001–S-046 and S-101–S-105; OUT references within 001–039.<br>ISS headings are ISS-01–06 and ISS-08–11; ISS-07 occurs only as the withdrawn ID. |
| Realises and traceability | Each element and invariant has exactly one Realises field.<br>39 rows, in Stage 1 order (OUT-039 after OUT-025).<br>0 differences between the rows and the union of the Realises fields.<br>No coverage text names an ID outside its row. |
| Names in `omn` blocks | 514 declared names (types, enumeration constants, variant tags, constants, functions, predicates); none declared twice.<br>Every attribute selection is declared on some type.<br>The only unresolved identifiers are bound variables, the parameter `Ks` and `refs` (defined in section 2.5). |
| `EvaluationRule` constants (by hand) | All 17 constants list the nine components in declaration order, with the correct types.<br>`evaluationRules` contains exactly the 17 constants.<br>`allPreventiveTypes` contains all nine `PreventiveTreatmentType` values. |
| Typing rule for levels | 172 level-annotated attribute declarations. No SHOULD, MAY or MUST-with-`when` attribute lacks an `opt`, `set` or `seq` type, and none uses `set1` or `seq1`. |
| Scope sweep (enter, entry, record, input, capture, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, reminder, obtained, calculated, computed, algorithm, "diary information", "diary data") | 56 hits in sections 1–7. All are exclusion statements, out-of-scope notes, omitted-word notes, text inside quotes, or wording accepted in earlier reviews.<br>The new rule components and predicates take only context properties (`preventiveTypes`, `preventiveFor`, `ageGroup`, `aged12OrOlder`, course events) and rule constants. |
| Thresholds and formulas that are part of the output data | All present and quoted: the evaluation time points (17 rules), the responder thresholds, the ICHD-3 8.2 levels and time span, the A1.1 window, the remission duration, score ranges and bands, the completeness proportion, the change formulas, the cluster rate and the totals relation. |
| Stale text after v07 | No leftover counts or descriptions of the earlier rule list ("eleven" now refers only to the rules whose offsets are in Stage 1 quotes, which is correct). |
| Snapshot | `cmp OUTPUT_MODEL.md history/v07.md`: identical. The working tree was clean before and after this review. |

## Remarks

None.

## Checked and not raised

- **New rules: readings and anchors.**
  - `ruleIhsQ2Oral` ("after three months at the target dose") is `atOffset` from the target dose.
  - `ruleAan14B` ("wait 24 weeks at the recommended dose before assessing efficacy") and `ruleRu33Bta` ("минимум через 6 месяцев терапии") are minimum times.
  - `ruleRuChildren` ("через 3мес.") is `atOffset` from the start.
  - `ruleTr3639` is anchored at the end of the third cycle, as `ruleNice1329` is anchored at the second.
  - `ruleTrBox8` ("etkinlik için en az 2-3 ay") is read as a window from the start, the same reading as the settled AAN 14A and NVN window readings.

  These readings follow the wording of each source and the model's settled conventions.
- **Populations of the new rules.**
  - **Turkish protocol (`anyAge`).** Section 3 addresses all ages; for example, the drug table on p. 52 gives adult and child doses. Section 6 adds paediatric specifics but names no evaluation time point ("Tedavi süresi en az 4 ay" is a treatment duration).
  - **IHS 2024 Q13 (children)** names no time point, so reading Q2 as `anyAge` stands.
  - **Russian paediatric recommendations.** The title page reads "дети", and p. 17 speaks of "детей и подростков", which supports `childrenAndAdolescentsOnly`.
- **Completeness of the `excludes` sweep.**
  - The Turkish protocol (pp. 47–58, and every page searched) names no type-specific time point other than 3.6.3.9.
  - SIGN 155 names none for botulinum toxin or CGRP antibodies; every page was searched, and the time statements outside section 4.1 concern trials, washout or phasing out.
  - The Russian time point for anti-CGRP antibodies (p. 41) is the date of `ruleRu71`.
- **`excludes` wording and NICE 1.3.27.**
  - The E-041 Meaning glosses `excludes` as "the types for which the same guidance names another time point". NICE also names 1.3.28 (CGRP inhibitors) and 1.3.29 (botulinum toxin type A), yet `ruleNice1327` excludes nothing.
  - The axiom values fix the semantics; comments have no formal force (section 2.2). The E-041 Notes state why NICE 1.3.27 applies to every type: NICE names no exception, and 12 weeks and the end of the second cycle are compatible with a review at 3–6 months.
  - Review 07 settled this point, so it is not a remark.
- **Boundary of the rule list.**
  - [S-023], the source of `critDmkg`, mentions "2 Monaten nach Erreichen der tolerierten Höchstdosis" and "innerhalb von 3 Monaten nach Behandlungsbeginn". Both are reports of the German guideline and of product information (SmPCs). They fall under the E-041 exclusion of "statements that report other guidelines", and [S-023] is not cited for OUT-018.
  - The model's boundary is the guidance cited for OUT-018 plus [S-034] for OUT-036 (d). It is stated, it applies the R07-01 required change, and ISS-10 records [S-034] for the human.
- **Turkish Box 8 criterion.** The Box 8 item "Ölçüt atak sıklığında en az %50 azalma olması" (a ≥ 50 % reduction in attack frequency) is not among `namedCriteria`. This is not a gap: OUT-020 requires a label to name the criterion it applies, not a fixed list, and `ResponderLabel.criterion` may hold any `ResponderCriterion` value. `namedCriteria` constrains nothing (it appears in no invariant).
- **Anchors that need a course event.**
  - The target-dose rules apply only where the context lists the date the target dose was reached. Review 07 accepted this ("it also needs the context to list the date the recommended dose was reached").
  - Every admissible context, including the context that lists the event, carries the obligation. So no obligation is lost for a subject described correctly.
- **Satisfiability with the new rules.**
  - Every rule except the two cycle-end rules puts its time point at least 8 weeks after the start. For NVN and Turkish Box 8, the 2-month minimum is at least 59 days.
  - So a 28-day on-treatment period can end at each time point, and a 28-day baseline gives equal lengths. INV-055, INV-056, INV-058, INV-059 and INV-097 hold together.
  - The `fitsMonthlyPeriod` guard covers `ruleTr3639`, as it covers `ruleNice1329`.
- **INV-055 Notes and ISS-10 on the rules that apply to children:**
  - NVN, IHS Q2, Turkish protocol, Russian paediatric;
  - from 12 years also NICE 1.3.27 (`aged12OrOlder`; INV-001 makes every adult aged 12 or older).

  The list is correct against the `ages` values.
- **Stage 1 example "8–12 weeks at target dose for most oral preventives".** `ruleAan14A` follows the AAN wording "most medications" (all types except onabotulinumtoxinA). The Stage 1 parenthesis is an example and is not contradicted, so this is not a Stage 1 issue.
- **Section 8.**
  - ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded, and each is pointed to from the elements it affects.
  - The ISS-10 update (the [S-034] rule is modelled and the human is asked to confirm it) is founded and not silent.
  - No Stage 1 issue is worked around silently.
- **Oscillation watch points** (the INV-087 start and lead-in; E-060, E-061, INV-105; INV-104): unchanged in v07, and not touched here.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the AAN/AHS 14A and NVN window readings;
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
  - NICE 1.3.27 applying to onabotulinumtoxinA.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and the oscillation check after iteration 04 froze nothing.
