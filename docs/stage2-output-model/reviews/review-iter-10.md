# Review — iteration 10
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v09
Date: 2026-10-21

## Summary

This is an independent fact-check and review of v09. I read the following in full:
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 after OUT-025), and section 5 for the source list;
- v09 in full (`OUTPUT_MODEL.md`, byte-identical to `history/v09.md`);
- review 09, fix log 09 and the oscillation check after iteration 08, with its eight watch points.

For earlier decisions I searched the other reviews and fix logs. FROZEN_ITEMS.md does not exist. I downloaded every source again myself, verified the quotes by script and by hand, and ran my own mechanical checks. I did not rely on the conclusions of earlier reviews.

**What changed in v09.** The v08 → v09 diff touches only these items:
- E-012: new `onlyOfType` and `scopeFor`;
- E-045: `AttackReductionComponent.headacheType`, the new tag `typeValuesOf`, the `where` clause, `valueAvailable`, one new [S-035] quote;
- E-046: the `allTypes` tie in `reductionMet` and `reductionDecided`; `attackScope`;
- INV-062, INV-063;
- INV-073 and INV-089: `onlyOfType` in place of `concerns`;
- E-064;
- rows OUT-020, OUT-023 and OUT-031; sections 9, 11 and 12.

E-041, E-039, E-060, E-061, INV-001, INV-050, INV-055, INV-058, INV-059, INV-087, INV-100, INV-104 and INV-105 are byte-identical to v08 (checked by script).

**Result.**
- **Citations.** 400 source-quote fragments were checked. 397 were found by script in their source; the other 3 source-language fragments were verified by hand:
  - the ICHD-3 A1.1 window, whose "±", "−" and "+" glyphs have no text mapping;
  - the [S-034] title page, which is an image (I rendered and read it).
  - The page or section location stated in the model was confirmed for every PDF quote.
  - The new v09 quote ([S-035] section 3.3 b, PDF p. 23, printed p. 13) is verbatim, its location is correct, and its translation is faithful.
- **Value sets and thresholds.** ICHD-3 labels, the 8.2 levels and span, the A1.1 window and the remission duration agree with their sources. So do the instrument ranges and bands, the six named responder criteria, the IHS 2025 control levels and the 17 evaluation rules.
- **v09 changes.**
  - The R09-01 fix is formally sound. `scopeFor` picks exactly one scope.
  - Every new term is well typed and guarded.
  - The tightened relations only add conjuncts, so INV-063 stays satisfiable.
  - INV-062 remains satisfiable in every admissible context.
  - The `onlyOfType` sweep of INV-073 and INV-089 is consistent with INV-088, INV-071 and INV-028.
- **Other checks.** Mechanical checks, traceability, conformance levels, the scope sweep and section 8 are clean.
- **Earlier work.** No remark would reverse an earlier fix or touch an oscillation watch point.

## Verification coverage

**Method**
- **Downloads.** Every source was downloaded with `curl` into the fresh directory `/tmp/r10-dl`, outside the repository. All 35 downloads returned HTTP 200:
  - the Stage 1 URLs of S-001 to S-011 (except S-010's PubMed page), S-014 to S-016, S-018, S-020, S-023, S-028 to S-030 and S-033 to S-035;
  - the Europe PMC full-text XML of S-004, S-011, S-012, S-014, S-023, S-042, S-043, S-101, S-102 and S-104;
  - the NICE CG150 Recommendations and Overview pages;
  - the S-103 page, the S-105 PDF and the S-106 pages (overview, section 1, section 2).
- **Extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`; HTML and XML had their markup stripped and entities unescaped. Page 1 of S-034 was rendered with `pdftoppm` and read as an image.
- **Scripts.** `extract.py`, `quotes.py`, `tally.py`, `grep.py`, `mech.py` and `names.py`, kept in the session scratchpad (`r10/`) and run with `python3 -I`.
- **Quote search.** Every double-quoted string outside the `omn` blocks was split at `[...]` (631 fragments). Each fragment was searched in the source of its nearest preceding tag, then in every source, in three passes:
  1. whitespace, quotes and dashes normalised;
  2. also line-end hyphens and glyphs without a text mapping removed;
  3. letters and digits only.

  Hits were reported with their PDF page and compared with the stated location.

**Citations**

| Source (URL as listed; HTTP) | Fragments checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (ichd-3.org PDF; 200; 211 pp.) | 107 | 107 (106 by script, 1 by hand). Code labels pp. 8, 9, 12; 8.2–8.2.8 pp. 122–125; the 8.2.3 comment p. 123; A1.1.1 criterion B and note 2 p. 190; Definitions of terms pp. 209–210; "simple analgesics" only on p. 139 (10.1.1, high-altitude headache). The window quote was read by hand: the text layer gives "day 1  2 (i.e. days 2 to þ3)". | 0 | 0 |
| S-007 (UCL manuscript; 200; 39 pp.) | 9 | 9 (pp. 10, 22, 25) | 0 | 0 |
| S-008 IHS 2024 (univaq PDF; 200; 31 pp.) | 27 | 27 (Q2 p. 9 with footnote; Q6 p. 12, Optimal, chronic 30 % alternative; Q6 Evidence p. 13; Q13 p. 17; Q4 p. 11) | 0 | 0 |
| S-010 IHS 2025 (univaq PDF; 200; 11 pp.) | 29 | 29 (p. 6; the "Insufficient Control" sentence is interrupted by the running header, as stated) | 0 | 0 |
| S-011 EHF 2022 (Europe PMC XML; 200) | 8 | 8 | 0 | 0 |
| S-014 (Europe PMC XML; 200) | 26 | 26 (HALT-90 and HALT-30 recall, "whole days per one or 3 months", Table 18 rows and labels) | 0 | 0 |
| S-015 NICE CG150 (Recommendations and Overview; 200; "Last updated: 03 June 2025") | 36 | 36 (1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48; the headings "Migraine with or without aura" and "Prophylactic treatment review"; the Overview population) | 0 | 0 |
| S-016 SIGN 155 (200; 64 pp.) | 9 | 9 (section 1.2.1, PDF p. 7; section 4.1, PDF p. 20) | 0 | 0 |
| S-018 AAN/AHS Clinician Summary (200; 12 pp.) | 13 | 13 (p. 1 title sentence; 14A, 14B, 14C p. 7; 14H p. 8) | 0 | 0 |
| S-023, S-028, S-029, S-030 (200) | 24 | 24 ("die Migränetage"; NVN PICO "Patiënten (kinderen en volwassenen)", "Publicatiedatum: 11-01-2018", the Aanbeveling; "hyppigheden eller styrken af migræne", PDF p. 19) | 0 | 0 |
| S-033 Russian adult (200; 92 pp.) | 21 | 21 (title p. 1 "Возрастная категория: взрослые", "Год утверждения: 2024"; "М – мигрень" p. 4; section 3.3 pp. 39–41; section 7.1 p. 53) | 0 | 0 |
| S-034 Russian paediatric (200; 53 pp.) | 10 | 10 (8 by script, 2 by hand; p. 17; flowchart p. 52; the title page image reads "Возрастная группа дети", "Год утверждения 2024") | 0 | 0 |
| S-035 Turkish protocol (200; 92 pp.) | 28 | 28. Kutu 8 p. 48: "Ölçüt …" is the second item and "Yeterli süre …" the seventh. Section 3.6.3.9 p. 57: "3 ayda bir" two sentences before "Hastalar 3 enjeksiyon siklusu …". Table 6 p. 52 "12 haftada bir". Heading of section 6, p. 77. **New v09 quote**: section 3.3 "Farmakolojik Tedavi", item "b. Profilaksi", PDF p. 23, printed p. 13, verbatim. | 0 | 0 |
| S-101 HIT-6 (Europe PMC XML; 200) | 6 | 6 (Methods > Data sources) | 0 | 0 |
| S-102 MIDAS (Europe PMC XML; 200) | 8 | 8 (Headache impact on functioning > Migraine-related disability) | 0 | 0 |
| S-103 PedMIDAS page (200; footer "© 2026") | 13 | 13 (grading table rows and headings) | 0 | 0 |
| S-104 HADS (Europe PMC XML; 200) | 2 | 2 (section "Construction of the HADS") | 0 | 0 |
| S-105 PHQ/GAD-7 manual (200; 9 pp.) | 5 | 5 (P.6/9 under "Use of some screeners as severity and outcome measures"; the PHQ-9 sentence also appears on P.5/9; developers sentence P.8/9) | 0 | 0 |
| S-106 NICE TA260 (200) | 4 | 4 (§2.1 last sentence; "Published: 27 June 2012"; "Last reviewed: 11 January 2016") | 0 | 0 |
| Stage 1 quotes reused (S-002, S-004, S-005, S-012, S-042, S-043) | 15 | 15 | 0 | 0 |
| **Total** | **400** | **400** (397 by script, 3 by hand) | **0** | **0** |

**Other quoted strings**
- **Stage 1 text.** 156 strings are Stage 1 v18 text reused by reference.
- **Translations.** 14 strings are English translations. All are faithful:
  - the eight Russian and Turkish translations of E-041;
  - the two Turkish translations of E-045, including the new v09 one: "Migraine preventive treatment aims to reduce the frequency, severity and duration of migraine attacks and to improve the patient's overall quality of life";
  - the Dutch PICO translation.
- **Not checked.** The rest are model terms, PubMed and web query strings, and fragments that the script created by pairing quote marks across text. The search-log mention "little or none" (PMC8684566) is not an evidence quote and was not checked.
- **Metadata** (PubMed esummary). S-101, S-102 and S-104, and the S-103 developer paper (PMID 11739822), agree with section 10: journal, year, volume, pages, authors, DOI and PMCID.
- **Newer versions.** None found that changes an element:
  - ICHD-3 is still the current edition; only "ICHD-4 – Work in Progress 1" (Cephalalgia 2024) exists ([fis.uke.de record](https://fis.uke.de/portal/en/publications/international-classification-of-headache-disorders4--work-in-progress-1(b2e76945-6b60-4911-9c1f-583c088a2d4c)/export.html); [IHS classification committee](https://ihs-headache.org/en/about-ihs/standing-committees/classification/));
  - no EHF CGRP-mAb guideline later than the 2022 update was found by web search;
  - NICE CG150 still reads "Last updated: 03 June 2025";
  - the NVN module still reads "Publicatiedatum: 11-01-2018";
  - the Russian adult PDF reads "Год утверждения: 2024";
  - the Turkish protocol is Revizyon 01 (2025).

**Per-OUT fidelity check.** For each requirement I compared the Statement parts, the constraining Caveats, the strength of each part against the level of the item that realises it, and the traceability row.

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK (E-003/E-005 MUST, INV-003, INV-014/015/108, INV-037; Caveat by `lengthDays`) | 021 | OK (INV-068 MUST, INV-069 SHOULD where provided, INV-102) |
| 002 | OK (INV-008 SHOULD) | 022 | OK (INV-070, INV-103; ISS-03) |
| 003 | OK (INV-011, INV-012; INV-013 SHOULD NOT; open form) | 023 | OK (INV-071 to INV-075, INV-107 SHOULD NOT; 15 min for cluster-only summaries, INV-073) |
| 004 | OK (INV-014 MUST, INV-009) | 024 | OK (INV-077 to INV-079; Caveats in Meaning) |
| 005 | OK (INV-015 for `hasType(c, c1)`; label SHOULD) | 025 | OK (MAY; INV-080) |
| 006 | OK (INV-016 SHOULD; INV-108 MUST where provided) | 039 | OK (INV-066, INV-067, E-055, INV-104) |
| 007 | OK (separate type E-019; INV-010, INV-017, INV-108) | 026 | OK (INV-081, INV-082, INV-100; ISS-06) |
| 008 | OK (MAY; ISS-04) | 027 | OK (INV-026, INV-027) |
| 009 | OK (INV-034 to INV-036; INV-001 forces weekly relevance for TTH and cluster) | 028 | OK (INV-040 MUST, INV-042 SHOULD, INV-043 SHOULD NOT; ISS-03) |
| 010 | OK (INV-018, INV-032, INV-039) | 029 | OK (INV-028 MUST, INV-029 SHOULD, INV-030; ISS-09) |
| 011 | OK (INV-019, INV-020; INV-021 SHOULD NOT) | 030 | OK (INV-086 MUST, INV-087; unchanged since v04) |
| 012 | OK (INV-022, INV-072, INV-076) | 031 | OK (INV-088, INV-089; rate scope `onlyOfType`) |
| 013 | OK (MAY, E-027) | 032 | OK (MAY; caveats SHOULD, INV-090) |
| 014 | OK (INV-023 MUST, INV-024; ISS-02) | 033 | OK (INV-083, INV-085; INV-084 SHOULD NOT) |
| 015 | OK (INV-025) | 034 | OK (INV-094, INV-104; ISS-04; unchanged since v03) |
| 016 | OK (INV-044, INV-045, INV-046; INV-047 MUST; INV-048 MUST NOT; ISS-01, ISS-09) | 035 | OK (INV-095, INV-105; ISS-03) |
| 017 | OK (INV-049 to INV-052; ISS-11) | 036 | OK ((a)–(c) INV-096 to INV-098; (d) INV-055 with `ruleRuChildren`; ISS-10) |
| 018 | OK (INV-053 to INV-059; INV-106 MUST NOT; the 17 rules agree with their texts) | 037 | OK (INV-091 SHOULD NOT, INV-092, INV-093) |
| 019 | OK (INV-060, INV-061; ISS-05) | 038 | OK (INV-099, INV-100; INV-101 SHOULD NOT) |
| 020 | OK. Scenario check of v09: a reduction component is decided on all-types changes only, an attack component on counts of `attackScope`, and the review-09 example no longer forces "responder". The six criterion constants are unchanged, and the named measures are the person's (NICE 1.3.28/1.3.29, IHS Q6, DMKG, Russian 7.1; Stage 1 quotes). | | |

**Mechanical checks**

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108); none missing, no duplicates. |
| References | No dangling E- or INV- reference.<br>S references lie within S-001–S-046 and S-101–S-106, and every S-1NN cited has a row in section 10.<br>OUT references lie within 001–039.<br>ISS headings are ISS-01–06 and ISS-08–11; ISS-07 occurs only as the withdrawn ID in section 9. |
| Realises and traceability | Exactly one Realises field per item.<br>39 rows in Stage 1 order (OUT-039 after OUT-025).<br>0 differences between each row and the union of the Realises fields.<br>No coverage text names an ID outside its row.<br>All rows read "full". |
| Names in `omn` blocks | 319 declared names, none declared twice.<br>218 enumeration constants and variant tags, with no clash with declared names.<br>Every attribute selection `e.a` names a declared attribute or component.<br>Every remaining undeclared identifier is a bound variable or parameter (after string literals and comments were stripped). |
| v09 terms | `onlyOfType`, `scopeFor`, `attackScope`, `typeValuesOf`, `AttackReductionComponent.headacheType`, the `where` clause and `valueAvailable` are well typed. Optional values are used only inside quantifiers (`∃ t ∈ a.headacheType`). No partial term was added. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2); 0 violations. |
| Invariant levels | MUST 19; MUST NOT 2 (INV-048, INV-106); SHOULD 47; SHOULD NOT 8; definitional 32.<br>Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Partial terms | Every `÷`, `days`, `first`/`last`, `max`/`min`, `classOf`, `publishedRecall`, `scoreRange` and `periodEndFrom` use is guarded, or covered by INV-001, INV-002 or INV-004 (section 2.6). |
| Scope sweep | Terms searched in sections 1–9: enter, entry, record, input, capture, logged, store/storage, persist, database, JSON, XML, CSV, FHIR, HL7, serialis, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field, "diary data", "diary information".<br>55 hits, all read in context. They are exclusion statements, out-of-scope notes, Stage 1 wording, or verbatim source quotes ([S-014] "records days affected").<br>No input entity, storage term or derivation from input. The v09 relations take shown changes, counts, periods and type scopes, the subject's headache types (a context property) and `provides`. |
| Thresholds and formulas that are part of the output data | All present and quoted:<br>• the 8.2 levels and span, the A1.1 window and the remission duration;<br>• the instrument bands and ranges;<br>• the responder thresholds, the control levels and the evaluation offsets;<br>• the percentage change, the covered-day proportion and the outcome proportion;<br>• totals against classes and drugs, the cluster rates, and the change from the baseline instrument result. |
| Watch-point items | E-041, E-039, E-060, E-061, INV-001, INV-050, INV-055, INV-058, INV-059, INV-087, INV-104 and INV-105 are byte-identical in v08 and v09. |

## Remarks

None.

## Checked and not raised

- **R09-01 fix and its sweep.**
  - **Reduction components.** They are decided on all-types changes only. INV-056 and INV-057 always show these changes (MSHD where provided), so no decidable case is lost. Each named criterion's measure is a measure of the person in its Stage 1 quote, which I re-verified in the sources.
  - **Attack components.** They are decided in `attackScope`. The Box 8 reading (migraine attacks) is supported by the new verbatim [S-035] quote.
  - **`scopeFor`.** Exactly one scope satisfies it.
  - **INV-062.** The `periodValuesOf` values at `allTypes` and the `typeValuesOf` values at `scopeFor` are satisfiable with:
    - INV-006, INV-030, INV-031 and INV-032;
    - INV-091 and INV-092, with a non-primary, exploratory index;
    - INV-073 and INV-011.
  - **Watch point 5.** The fix keeps `#L.evaluated = 1`, the `evaluationResult` / `pretreatmentBaseline` pair, `rc.treatment = L.treatment` and the open `UnderlyingKind`, so watch point 5 is respected.
  - **Reader-named criteria restricted to one headache type.** A reduction criterion restricted to one type becomes a `judgement` component and is not decided. OUT-020 does not require the output to decide labels, so this is not a defect.
- **Readings of `scopeFor` for a subject without a confirmed headache type.** The E-045 Notes ("Type scope") and the INV-063 Reading paraphrase `scopeFor` as "over all types combined where every headache type the subject has or may have falls under that type". They omit the condition, stated in the E-012 Meaning and predicate, that the subject has at least one headache type. For a subject with `headacheTypes = ∅` and `possibleHeadacheTypes = {c1}`, the predicate gives `ofType(c1)`.
  - The E-045 sentence refers explicitly to "`scopeFor` (E-012)".
  - Section 2.1 makes text outside the `omn` blocks explanatory.
  - Review 09 judged short Readings that point to the formal definition not a remark (watch point 1).
  - So this is not a remark. A fixer touching these Readings in a later iteration could add "where the subject has a headache type" at no cost.
- **`onlyOfType` in INV-073 and INV-089.** In the cluster view of a subject who has cluster headache and may have another type, INV-088 is met by summaries and rates scoped to `ofType(c3_1)`. INV-071, INV-069 and INV-104 do not constrain the scope.
  - INV-088 asks for a 15-minute summary for every acute medication, including one never used for cluster attacks. This is satisfiable with 0 treated attacks and unchanged from v08 in substance.
- **INV-091 to INV-093 keep `concerns`.** The fixer considered this and justified it in the E-012 Notes. It errs towards applying the OUT-037 restriction, and review 01 found the reading defensible.
- **INV-048 (MUST NOT).** It covers the indicator's own claims and those of annotations qualifying it. `claims` are defined as what an element puts to the reader "by its wording or presentation" (E-001), so a presentation of the indicator as a diagnosis by its surroundings is a claim of the indicator. The general SHOULD NOT of INV-101 covers other elements. Not a gap.
- **INV-054 at MUST for every change.** In the model, changes are the changes of response comparisons (E-040 Conformance, INV-056). The invariant is also the kind PROCESS section 2 lists ("a relative change is shown together with the absolute values it compares"). Not a broadening.
- **INV-096, `affected` as an alternative to `missed` and `impaired`.** Days on which headache affected school are the days on which school was missed or impaired, shown as one count. This is a reading of "school days missed or impaired", not a narrowing.
- **ICHD-3 values re-verified in the PDF.**
  - 8.2.1–8.2.5 and 8.2.8 at 10 or 15 days per month; 8.2.6 "on a total of ≥10 days/month for >3 months"; note 2 on 8.2.1–8.2.5;
  - the A1.1 window and "there is no day 0" (p. 190);
  - "must exceed three months" (p. 209);
  - the cluster-period definition (p. 209).
- **Instrument value sets re-verified.**
  - HIT-6: 36–78; ≤ 49, 50–55, 56–59, 60–78.
  - MIDAS: grades I–IV, 0–5, 6–10, 11–20, ≥ 21; three-month recall.
  - PedMIDAS: 0–10, 11–30, 31–50, > 50.
  - HALT-90: Table 18, including the overlap at 20. "Grading is not used by HALT-30".
  - HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
- **IHS 2025 control levels (INV-064).** The levels exclude every inconsistent category. A month pattern of mixed values (for example 5 and 7) admits only "insufficient control", which [S-010] permits.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - INV-023 at any granularity;
  - the "> 3 months" reading of INV-045 and of the cluster remission;
  - the AAN/AHS 14A, NVN and Turkish Box 8 window readings, and NICE 1.3.27 for onabotulinumtoxinA (watch points 1 and 8);
  - labels under a criterion that does not apply (review 02);
  - OUT-028 and ICHD-3 1.3 "> 3 months" (Stage 1 review 18);
  - the 24-hour outcomes for cluster summaries;
  - "history of previous bouts";
  - the HIT-6 one-month recall;
  - the MIDAS label choice;
  - "baseline administration" as any earlier administration;
  - the co-presence of treatment-history groups (review 03);
  - the E-060 lead-in wording.
- **Oscillation watch points.** No observation above asks for a change to any watched item:
  - `excludes` and the rule values;
  - the E-041 applicability dimensions;
  - `ruleRuChildren`;
  - INV-050 and E-039;
  - the responder-label ties;
  - the v08 sweep items;
  - INV-087, INV-104 and INV-105;
  - the timing readings.
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded and each is pointed to from the elements it affects. I re-verified:
  - 8.2.6 criterion B;
  - "simple analgesics" only on p. 139 (high-altitude headache);
  - NICE 1.3.9 and 1.3.39 without a review time point;
  - 1.3.48 in the medication-overuse section, and the CG150 population;
  - the [S-034] flowchart on p. 52.

  No Stage 1 issue is silently worked around. The R09-01 fix rests on the criteria's own wording, which Stage 1 quotes, and is not a Stage 1 issue.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist; the oscillation checks after iterations 04 and 08 froze nothing.
