# Review — iteration 07
VERDICT: REMARKS
REMARK_COUNT: 3
Reviewed version: v06
Date: 2026-10-21

## Summary

v06 fixes R06-01 correctly. Each evaluation rule now carries the population of its guidance (`headacheType`, `ages`), and `applicable` requires it. Every population value matches the downloaded guidance text:

- NICE CG150: the Overview, the headings above 1.3.27–1.3.29, and "in adults" in 1.3.24 and 1.3.26;
- AAN/AHS 2026: the title of the Clinician Summary;
- SIGN 155: section 1.2.1;
- the EHF 2022 guideline: its Background;
- IHS 2024: the Q2 and Q13 headings;
- the NVN module: its PICO, and an Aanbeveling with titration schedules "BIJ KINDEREN" and "BIJ VOLWASSENEN";
- the Russian adult recommendations: the title page.

The new subject properties take no input data, INV-001 stays satisfiable, and ISS-10 and ISS-11 are founded.

The citation base is sound. All 131 quoted strings that are not Stage 1 text were found verbatim in the downloaded sources. The metadata of S-101 to S-105 is correct, and no newer version of ICHD-3, NICE CG150 or IHS 2024 exists. The mechanical checks and the scope sweep are clean.

Three defects remain. All are in E-041 and none touches an oscillation watch point.

- **R07-01 (coverage gap).** The rule list holds only the time points that appear inside the Stage 1 quotes. Two time points are missing, although OUT-018 cites their sources for "the evaluation time points named in current guidance":
  - IHS 2024 Q2, oral preventives: three months at the target dose. It is the sentence directly before the one Stage 1 quotes.
  - AAN/AHS 2026 rec. 14B, onabotulinumtoxinA: 24 weeks at the recommended dose.
- **R07-02 (applicability).** `ruleAan14A` and `ruleRu71` apply to every preventive type. So at MUST they require "AAN/AHS 2026 rec. 14A" and "Russian … section 7.1" time points for onabotulinumtoxinA. Both guidelines name a later time point for this treatment: 24 weeks (AAN 14B) and a minimum of 6 months (Russian section 3.3 comments).
- **R07-03 (citation defect).** One [S-011] quote in E-041 has the wrong paragraph location.

## Verification coverage

**Method**

- **Downloads.** Everything was downloaded with `curl` into a fresh directory outside the repository (`/tmp/r07-dl-OmPD`). Scripts were kept in the session scratchpad (`srctext.py`, `quotes.py`, `mech.py`, `names.py`) and run with `python3 -I`.
- **Extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML pages and Europe PMC full-text XML were tag-stripped and HTML-unescaped.
- **Quote extraction.** Every double-quoted string outside the `omn` blocks (407 distinct strings) was extracted, together with the source tag that precedes it. Each string was split at `[...]`.
- **Search passes.** Each fragment was searched in its attributed source in three passes:
  1. after whitespace collapse;
  2. after normalising quotes, dashes, ligatures and line-end hyphens, and removing the unmapped ICHD-3 glyphs "≥" and "±";
  3. alphanumeric only.
- **Unmatched strings.** Strings not found in their attributed source were searched in every downloaded source and in Stage 1 v18, and then read in context.

### Citations

| Source (URL as listed; HTTP status) | Quoted strings checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (Stage 1 URL; 200; 211 pages) | 35:<br>• code labels, pp. 8, 9, 12;<br>• 8.2 Descriptions and criteria B, 8.2.6 note 2, the 8.2.3 comment (short and full), pp. 122–125;<br>• A1.1.1 and A1.1.2 window, A1.1.1 note 2, "in at least two out of three menstrual cycles", p. 190;<br>• cluster remission, p. 209;<br>• "simple analgesics", p. 139 | 35 | 0 | 0 |
| S-007 (Stage 1 URL, UCL Discovery; 200; 39 pages) | 4 (pp. 10, 22, 25) | 4 | 0 | 0 |
| S-008 IHS 2024 (Stage 1 URL, univaq; 200; 31 pages) | 5:<br>• the Q6 30 % alternative, p. 12;<br>• the AHS MIDAS/HIT-6 definition, p. 13;<br>• "baseline score";<br>• the Q2 heading, p. 9, and the Q13 heading, p. 17 | 5 | 0 | 0 |
| S-010 IHS 2025 (Stage 1 URL, univaq; 200) | 17 (p. 6: the control levels, the definition sentence, the "proxy" sentence, section names) | 17 | 0 | 0 |
| S-011 EHF 2022 (Europe PMC XML of PMC9188162 and the listed PMC page; 200) | 2 (Background) | 2 (location defect: R07-03) | 0 | 0 |
| S-014 (Europe PMC XML of PMC6734476 and the listed PMC page; 200) | 13 (HALT recall, unit, Table 18, the HURT sentence) | 13 | 0 | 0 |
| S-015 NICE CG150 (Recommendations page and Overview page; 200; "Last updated: 03 June 2025") | 9:<br>• the Overview population sentence;<br>• the headings above 1.3.27;<br>• 1.3.24, 1.3.26, 1.3.9, 1.3.39 and 1.3.48 | 9 | 0 | 0 |
| S-016 SIGN 155 (Stage 1 URL; 200; 64 pages) | 4 (section 1.2.1, PDF p. 7 = printed p. 1; the heading is printed in upper case) | 4 | 0 | 0 |
| S-018 AAN/AHS Clinician Summary (Stage 1 URL; 200; 12-page PDF) | 2 (p. 1) | 2 | 0 | 0 |
| S-028 NVN module (Stage 1 URL; 200) | 4 (PICO in "Zoeken en selecteren", module name, Aanbeveling fragments) | 4 | 0 | 0 |
| S-033 Russian adult recommendations (Stage 1 URL; 200, first attempt; 92 pages) | 4 ("Возрастная категория: взрослые", p. 1; "М - мигрень", p. 4; section 7.1, p. 53) | 4 | 0 | 0 |
| S-034 Russian paediatric recommendations (Stage 1 URL; 200; 53 pages) | 3 (Приложение Б, p. 52) | 3 | 0 | 0 |
| S-101 Yang 2011 (Europe PMC XML; listed PMC page 200) | 4 | 4 | 0 | 0 |
| S-102 Pavlović 2015 (Europe PMC XML; listed PMC page) | 4 | 4 | 0 | 0 (the PMC page first returned a reCAPTCHA page; it returned 200 with the quote on retry) |
| S-103 PedMIDAS page (listed URL; 200; footer "2026 Cincinnati Children's Hospital Medical Center") | 13 (title, lead sentence, section heading, table headings and rows) | 13 | 0 | 0 |
| S-104 Snaith 2003 (Europe PMC XML; listed PMC page) | 2 | 2 | 0 | 0 (reCAPTCHA on the first try; 200 with the quote on retry) |
| S-105 PHQ/GAD-7 instructions (listed PDF; 200; 9 pages; author Kurt Kroenke, created 2010-06-22, modified 2014-04-16) | 6 (P. 6/9 ranges; the P. 8/9 developers sentence and its heading) | 6 | 0 | 0 |
| **Total** | **131** | **131** | **0** | **0** |

**Further checks**

- **Stage 1 text.** 228 further quoted strings are verbatim Stage 1 v18 text: fragments of Stage 1 statements and quotes reused by reference.
- **Remaining strings.** The other 48 strings are of three kinds, and none is presented as a source quote:
  - the model's own terms and wordings of Stage 1, for example "K is available when C" and "not reached";
  - translations;
  - search-log query strings.
- **Translations of the new non-English quotes**, all faithful:
  - [S-028] PICO: "P: Patients (children and adults) with migraine in whom preventive treatment is indicated";
  - [S-033] "Age category: adults";
  - [S-034] flowchart box: "prescription of medicines for the preventive therapy of migraine taking comorbidity into account. Monitoring of the efficacy of therapy after 3 months."
- **Metadata (PubMed esummary).** All correct:
  - S-101: Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMID 20819842, PMC3057423;
  - S-102: J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMID 25902814, PMC4406925, the seven authors as cited;
  - S-104: Health Qual Life Outcomes 2003;1:29, PMID 12914662, PMC183845;
  - the S-103 developer paper: Neurology 2001;57(11):2034–9, PMID 11739822.
- **Newer versions.** None changes an element:
  - ICHD-4 exists only as "Work in Progress 1" (2024);
  - NICE CG150 was last updated on 3 June 2025;
  - no update of the IHS 2024 preventive recommendations was found.
- **Value sets re-checked against the downloaded texts**, all correct:
  - the ICHD-3 labels, the 8.2 levels (15 / 10) and the "> 3 months" span; the A1.1 window; the remission duration;
  - the HIT-6 range and bands; the MIDAS, PedMIDAS and HALT-90 bands and labels; the recall periods;
  - the HADS, PHQ-9 and GAD-7 ranges;
  - the IHS Q6, NICE, DMKG and Russian thresholds; the IHS 2025 control levels;
  - the offsets, anchors and populations of the eleven rules of E-041.
- **Sources read for the first time in Stage 2.** The time-point recommendations of the sources cited in the OUT-018 Statement were read in full:
  - S-008 Q2, Q4–Q6 and Q13;
  - S-011 questions 3 and 4;
  - S-015 1.3.17–1.3.29 and 1.3.39–1.3.41;
  - S-016 section 4.1 and the onabotulinumtoxinA text;
  - S-018 recommendations 14A–14H and 17;
  - S-033 sections 3.3 and 7.1.

  This found the omissions of R07-01 and the evidence of R07-02.

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
| 011 | OK | 030 | OK |
| 012 | OK | 031 | OK |
| 013 | OK (MAY) | 032 | OK |
| 014 | OK (ISS-02) | 033 | OK |
| 015 | OK | 034 | OK |
| 016 | OK (ISS-01, ISS-09) | 035 | OK |
| 017 | OK (ISS-11 founded) | 036 | OK (R06-01 fix verified; ISS-10) |
| 018 | **R07-01, R07-02**; otherwise OK, including the R06-01 fix | 037 | OK |
| 019 | OK (ISS-05) | 038 | OK |
| 020 | OK (ISS-08) | | |

**Conformance levels.** Compared for all 108 invariants and every attribute level:

- MUST 19;
- MUST NOT 2 (INV-048, INV-106);
- SHOULD 47;
- SHOULD NOT 8 (INV-013, 021, 043, 065, 084, 091, 101, 107);
- definitional 32.

No mismatch with the Stage 1 strength was found. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`.

### Mechanical checks

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108); none missing, no duplicates |
| References | no dangling E- or INV- reference<br>ISS-07 occurs only as the withdrawn ID (sections 8, 9 and 12)<br>S references lie within S-001–S-046 and S-101–S-105; OUT references within 001–039 |
| Realises and traceability | each element and invariant has exactly one Realises field<br>39 rows, in Stage 1 order (OUT-039 after OUT-025)<br>0 differences between the rows and the union of the Realises fields<br>no coverage text names an ID outside its row<br>39 × "full" (but see R07-01, R07-02) |
| Names in `omn` blocks | 508 declared names, enumeration constants and variant tags; none declared twice<br>every attribute selection is declared on some type<br>the only unresolved token is `Ks`, the parameter of `reportedTogether`, which the script's parameter regex misses<br>only `Output.views` and `View.content` are composition attributes |
| Typing rule for levels | 172 level-annotated attribute declarations; no SHOULD, MAY or MUST-with-`when` attribute lacks an `opt`, `set` or `seq` type, and none uses `set1` or `seq1` |
| v06 constructs, checked by hand | `AgeCoverage`, `ageCovered`, `inPopulation`, `preventiveFor` and `aged12OrOlder` are well typed<br>every rule constant lists all eight components<br>the new INV-001 conjuncts are satisfiable together with the others |
| Scope sweep (enter, entry, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, reminder, obtained, calculated, computed, algorithm, "diary information", "diary data") | 48 hits, all of them:<br>• exclusion statements;<br>• out-of-scope notes;<br>• omitted-word notes;<br>• text inside quotes;<br>• the meaning statements already accepted in earlier reviews.<br>None is new input, storage or derivation-from-input content. Every relation takes only output elements, context properties or cited constants. |
| Thresholds and formulas that are part of the output data | all present and quoted, except two evaluation time points (R07-01) |
| Snapshot | `cmp OUTPUT_MODEL.md history/v06.md`: identical; working tree clean before this review |

## Remarks

### R07-01 Coverage gap: two evaluation time points named in recommendations that OUT-018 cites for its time points are missing (IHS 2024 Q2 for oral preventives; AAN/AHS 2026 rec. 14B for onabotulinumtoxinA)
- Item(s): E-041 (`evaluationRules`, Meaning, Evidence, Notes); E-008 (`PreventiveTreatmentType`); INV-055 and INV-059 (through `evaluationRules`); section 7 row OUT-018; section 11.
- Problem:
  - **What Stage 1 requires.**
    - OUT-018 (MUST) requires the comparison "at the evaluation time points named in current guidance, which differ by treatment type", and cites [S-008][S-011][S-015][S-016][S-018] for them.
    - The parenthesis "(for example … after onabotulinumtoxinA cycles)" lists examples of these time points. The requirement itself is "the evaluation time points named in current guidance".
    - PROCESS section 2 lists "the evaluation time points shown with a response comparison (OUT-018)" among the thresholds that are part of the output data and that the model must contain. It adds: "When a cut-off, reference level or formula is part of the output data, the model states it in full."
  - **What the model contains.** The E-041 Notes restrict the list to "the set of evaluation time points named in the Stage 1 evidence of OUT-018". So the list holds only time points that appear inside the Stage 1 quotes. Two time points named in two of the five cited sources are missing. Both stand in the same recommendations from which the model already takes rules:
    1. **IHS 2024 Q2, oral preventives: three months at the target dose.**
       - This is the first sentence of the Q2 Optimal recommendation, directly before the injectable sentence that Stage 1 quotes and that `ruleIhsQ2Monthly` and `ruleIhsQ2Quarterly` model. The Essential level names the same time point.
       - It is not equivalent to any rule of the list:
         - AAN 14A: a window of 8 to 12 weeks after the tolerated dose;
         - SIGN 155, titrated treatment: at least 8 weeks after the target dose;
         - NVN: 2 to 3 months after the start;
         - Russian section 7.1: 3 months after the start;
         - NICE 1.3.27: a window of 3 to 6 months after the start, in which INV-055 requires only one comparison.
    2. **AAN/AHS 2026 rec. 14B (level B), onabotulinumtoxinA: 24 weeks at the recommended dose.**
       - It stands between 14A and 14C, which Stage 1 quotes from the same page.
       - OUT-018 names onabotulinumtoxinA among its examples. The model's onabotulinumtoxinA time points are only NICE 1.3.29 (the end of the second cycle) and IHS Q2 for quarterly injectables.
  - **Example 1 (oral preventive).**
    - An adult with episodic migraine starts topiramate (`doseTitratedPreventive`) on 1 February 2026 and reaches the target dose on 1 March 2026. The as-of date is 15 August 2026.
    - INV-059 requires the time points of NICE 1.3.27, AAN 14A, SIGN 155 (titrated), NVN and Russian section 7.1, and INV-055 requires comparisons at them.
    - Neither requires a comparison ending at the IHS Q2 time point (1 June 2026), nor any time point labelled with IHS Q2.
    - For a child under 12, NVN is the only applicable rule, although the model reads IHS Q2 as guidance for any age (E-041 Notes).
  - **Example 2 (onabotulinumtoxinA).** For onabotulinumtoxinA started at the recommended dose on 5 January 2026, no "AAN/AHS 2026 rec. 14B" time point (22 June 2026) is required. A 14A window (2 to 30 March 2026) is required instead; see R07-02.
  - **Why the stated reason does not hold.** The E-041 Notes justify the restriction with "Stage 1 gives them as examples ('for example')". But "for example" qualifies the parenthetical list, not the MUST, and the bracketed sources are where Stage 1 says the time points are named.
  - **The model's own practice elsewhere.** Where Stage 1 names a source's criterion, E-045 states that criterion in full, beyond the Stage 1 quote. The IHS Q6 chronic-migraine 30 % alternative and the AHS MIDAS/HIT-6 thresholds appear there under "Thresholds not quoted in Stage 1".
  - **Not considered before; not a reversal.**
    - R01-01 compared the list only with the Stage 1 quotes.
    - In iteration 06 the fixer quoted the Q2 heading (E-041 Evidence) but not the first Q2 recommendation sentence.
    - No Stage 2 file mentions AAN 14B (checked by `grep`).
    - Adding rules continues R01-01 in the same direction.
- Evidence:
  - Stage 1 OUT-018 Statement: "The output MUST allow this comparison at the evaluation time points named in current guidance, which differ by treatment type (for example after about 8–12 weeks at target dose for most oral preventives, after a minimum of 3 consecutive months for anti-CGRP monoclonal antibodies, and after onabotulinumtoxinA cycles) [S-008][S-011][S-015][S-016][S-018]."
  - Stage 1 OUT-018 Evidence quotes only the second Q2 sentence: [S-008] "We recommend a minimum of three months for injectable drugs taken on a monthly basis, and a minimum of six months for injectable drugs administered quarterly." (Q2, Optimal-level recommendation, p. 9).
  - [S-008] "In individuals initiating a new migraine oral preventive treatment, we suggest evaluating effectiveness* after three months at the target dose." (Q2 "When should the effectiveness of a migraine preventive treatment be assessed?", Recommendations, Optimal, p. 9; the asterisk refers to the footnote "See Q6 for the criteria for assessing the effectiveness of a preventive therapy"). https://ricerca.univaq.it/retrieve/b7f186a9-06ec-4e9c-b132-4f785bbeb121/puledda-et-al-2024-international-headache-society-global-practice-recommendations-for-preventive-pharmacological.pdf
  - [S-008] "In individuals initiating a new oral preventive treatment, we suggest evaluating effectiveness* after three months of treatment at target dose." (Q2, Recommendations, Essential, p. 9; same URL)
  - [S-018] "14B. Clinicians should wait 24 weeks at the recommended dose before assessing efficacy of onabotulinumtoxinA injections for migraine prevention before assessing efficacy." (Recommendation 14 "When to Assess Treatment Efficacy", level B, p. 7; the repeated phrase "before assessing efficacy" is in the source). https://www.aan.com/Guidelines/Home/GetGuidelineContent/1180
  - [S-018] "14H. If suboptimal response is observed after 12–24 weeks (see 14A and 14B), and other options are available and not contraindicated, clinicians should engage in shared decision making with the patient to initiate an alternate medication for migraine prevention." (Recommendation 14, level B, p. 8; same URL)
  - E-041 Notes (model): "The rule list is the set of evaluation time points named in the Stage 1 evidence of OUT-018 ([S-015], [S-018], [S-016], [S-011], [S-008], [S-028], [S-033]). Stage 1 gives them as examples ("for example"), so a diary may show further guidance time points as `OtherItem`s."
  - E-045 Evidence (model): "Thresholds not quoted in Stage 1: [S-008] "For patients with chronic migraine who have not achieved a ≥ 50% decrease […]"" and the AHS MIDAS/HIT-6 definition.
- Required change:
  - **Add two rules** to `evaluationRules`. Each takes a verbatim quote with its location from S-008 or S-018, cited by Stage 1 ID.
    - (a) **IHS Q2, oral preventives.** `guidance` "IHS global practice recommendations Q2 (oral preventives)", `headacheType` `c1`, `ages` `anyAge` (as the model reads Q2 for the injectable rules), `anchor` `toleratedOrTargetDoseAnchor`, `timing` `atOffset`, `minOffset` `months(3)`. Its `appliesTo` needs a new `PreventiveTreatmentType` value for oral preventive treatments (for example `oralPreventive`), explained in the E-008 Notes. INV-001's fallback type stays.
    - (b) **AAN/AHS 2026 rec. 14B.** `headacheType` `c1`, `ages` `adultsOnly`, `appliesTo` `{onabotulinumtoxinA}`, `anchor` `toleratedOrTargetDoseAnchor` ("at the recommended dose"), `timing` `atLeastOffset` ("wait 24 weeks … before assessing efficacy"), `minOffset` `weeks(24)`.
  - **Satisfiability.** Check `fitsMonthlyPeriod` and INV-055 with INV-056 and INV-097. Both time points lie at least 13 weeks after the start, so the R02-01 argument carries over.
  - **Text.** Update:
    - the E-041 Meaning, Evidence and Notes: the rule list is the set of time points named in the cited guidance recommendations, not only the Stage 1 quotes;
    - section 7 row OUT-018;
    - the search log.
  - **If the author holds that time points outside the Stage 1 quotes are not required**, state that with a reason grounded in Stage 1 text. "for example" is not such a reason (see Problem).

### R07-02 Infidelity (applicability condition): the AAN/AHS 14A and Russian section 7.1 time points are required for onabotulinumtoxinA, for which both guidelines name a later time point
- Item(s): E-041 (`ruleAan14A` and `ruleRu71` with `appliesTo ↦ allPreventiveTypes`; `applicable`; Meaning; Notes); INV-055, INV-058, INV-059; section 7 row OUT-018.
- Problem:
  - **What the model requires.**
    - Through `appliesTo ↦ allPreventiveTypes`, both rules apply to a preventive treatment of type `onabotulinumtoxinA`. This holds for an adult with migraine; for 14A, it also needs the context to list the date the recommended dose was reached.
    - INV-059 (MUST) then requires the comparison to show two time points for that treatment:
      - one labelled "AAN/AHS 2026 rec. 14A", 8 to 12 weeks after that date;
      - one labelled "Russian clinical recommendations «Мигрень» (adults) 2024, section 7.1", 3 months after the start.
    - INV-055 (MUST) requires comparisons that end at these time points.
  - **What the guidance says.**
    - AAN/AHS 2026 gives onabotulinumtoxinA its own time point, 24 weeks (14B). Its 14H refers to "12–24 weeks (see 14A and 14B)". So "most medications" in 14A does not include onabotulinumtoxinA.
    - The Russian recommendations repeat the 3-month recommendation in section 3.3. Its comments name a minimum of 6 months for botulinum toxin type A.
    - The model therefore attributes to both guidelines time points that they do not give for this treatment. This is the R06-01 defect for a treatment type instead of a population. PROCESS section 2: "A relation must be correct under the definitions the output names."
  - **Internal inconsistency.** The E-041 Meaning itself describes the AAN time point as "about 8–12 weeks at the tolerated or target dose for most oral preventives (AAN/AHS, adults)", as the Stage 1 example does. The rule nevertheless applies it to every type.
  - **Example.**
    - An adult with chronic migraine receives onabotulinumtoxinA from 5 January 2026, at the recommended dose from the start. The as-of date is 15 August 2026.
    - The model requires an "AAN/AHS 2026 rec. 14A" window from 2 to 30 March 2026, and a "Russian … section 7.1" time point on 5 April 2026, each with a comparison ending there.
    - AAN names no assessment before 22 June 2026 (24 weeks), and the Russian guideline none before 5 July 2026 (6 months).
  - **New evidence against earlier decisions.**
    - Review 01 judged "AAN 14A ('most medications') applied to all preventive types" to be "a defensible reading". The R01-01 fixer applied `ruleRu71` "for every preventive type".
    - Neither considered 14B or the section 3.3 comment, and no Stage 2 file mentions them.
  - **What this remark does not touch.**
    - The settled "AAN/AHS 14A window reading" (8 to 12 weeks as a window from the tolerated dose) is unchanged.
    - R01-02's guarantee (the INV-001 fallback type) and R06-01's population condition are kept.
    - This is not a reversal of an earlier fix, and E-041 is not an oscillation watch point.
- Evidence:
  - E-041 (model): `ruleAan14A = EvaluationRule(guidance ↦ "AAN/AHS 2026 rec. 14A", …, appliesTo ↦ allPreventiveTypes, anchor ↦ toleratedOrTargetDoseAnchor, timing ↦ withinWindow, minOffset ↦ weeks(8), maxOffset ↦ {weeks(12)})`.
  - E-041 (model): `ruleRu71 = EvaluationRule(…, appliesTo ↦ allPreventiveTypes, anchor ↦ treatmentStartAnchor, timing ↦ atOffset, minOffset ↦ months(3), …)`.
  - `allPreventiveTypes` contains `onabotulinumtoxinA`.
  - E-041 Notes (model): ""most medications" is modelled as applying to every preventive treatment type within its population"; and, for the Russian rule, "so it applies to every preventive treatment type within its population".
  - [S-018] 14B and 14H, quoted in R07-01 (pp. 7–8).
  - [S-033] "при отсутствии эффекта в течение 3 месяцев следует заменить выбранное профилактическое средство на другой препарат; эффективность БТА – минимум через 6 месяцев терапии." Translation: "if there is no effect within 3 months, the chosen preventive agent should be replaced by another drug; efficacy of BTA – after a minimum of 6 months of therapy."
    - Location: section 3.3 "Профилактическая терапия", Комментарии to the recommendation "Рекомендуется считать профилактическое лечение эффективным, если частота дней с ГБ сокращается через 3 месяца терапии на 50% и более от исходной", PDF p. 39. Stage 1 quotes the section 7.1 version of that recommendation (p. 53). https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=295_4
    - "БТА" is not expanded in the list of abbreviations. The next recommendation (p. 40) concerns "ботулинический токсин типа А" (botulinum toxin type A).
- Required change:
  - **Exclude onabotulinumtoxinA from `ruleAan14A` and from `ruleRu71`.**
    - Removing a value from `appliesTo` does not suffice. A treatment may have several types: an onabotulinumtoxinA course is also a `quarterlyInjectable`, and a quarterly anti-CGRP antibody must keep 14A.
    - For example, add an `excludes : set PreventiveTreatmentType` component to `EvaluationRule`: `{onabotulinumtoxinA}` for these two rules and ∅ for the others. `applicable` then also requires that the treatment has none of the excluded types. An equivalent mechanism is also acceptable.
  - **The time points for onabotulinumtoxinA.**
    - The AAN time point is then that of 14B (R07-01).
    - For the Russian guideline, either add a rule for "минимум через 6 месяцев" (`atLeastOffset`, `months(6)`, from the treatment start, `adultsOnly`, migraine), with the quote, its translation and the note on "БТА"; or state why it is not added. In neither case may the 3-month rule remain applicable to onabotulinumtoxinA.
  - **Text.** Update:
    - the E-041 Meaning and Notes (replace "applying to every preventive treatment type");
    - the INV-055, INV-058 and INV-059 Readings where they describe the rules;
    - section 7 row OUT-018.

### R07-03 Citation defect: wrong location of the second [S-011] quote in E-041
- Item(s): E-041 Evidence.
- Problem: E-041 cites two [S-011] quotes with the single location "(Background, first paragraph; the omitted text is a reference number)". Only the first quote is in the first paragraph of the Background. The second quote, "Considering the new knowledge on the topic, the EHF council decided to update the 2019 guideline.", is the whole second paragraph.
- Evidence:
  - Europe PMC full text of PMC9188162: the Background section opens with `<p id="Par12">The landscape of migraine prevention […] In 2019 the European Headache Federation (EHF) issued the first guideline for the use of CGRP-mAbs for migraine prevention in adults [1]. […]</p>`, followed by `<p id="Par13">Considering the new knowledge on the topic, the EHF council decided to update the 2019 guideline.</p>`.
  - The listed URL https://pmc.ncbi.nlm.nih.gov/articles/PMC9188162/ shows the same two paragraphs.
- Required change: give each quote its own location: "(Background, first paragraph; the omitted text is a reference number)" for the first quote and "(Background, second paragraph)" for the second.

## Checked and not raised

- **R06-01 fix.**
  - The populations of the eleven rules match the guidance texts (see Summary).
  - The NVN PICO that E-041 quotes belongs to the module's add-on sub-question ("I: Combinatie van preventieve behandeling"). The Aanbeveling, which contains the 2–3-month time point, has schedules for children and for adults, so `anyAge` is correct.
  - NICE 1.3.28 states no age itself. Reading it as `adultsOnly`, because NICE recommends CGRP inhibitors only for adults (1.3.24, 1.3.25), is defensible.
  - SIGN 155 for adolescents is read as permitted rather than named. The time point can still be shown as an `OtherItem`, so no output that Stage 1 permits is excluded.
- **ISS-10 and ISS-11 are founded.**
  - NICE 1.3.9 and 1.3.39–1.3.41 recommend prophylaxis with no review time point.
  - The [S-034] flowchart (p. 52) reads as quoted.
  - The [S-034] paediatric time point is cited for OUT-036 (d), which names no time points. Recording it as a Stage 1 issue is therefore acceptable and not a silent work-around.
- **Other time-point statements in the OUT-018 sources** are not evaluation time points of OUT-018:
  - S-008 Q4 Evidence ("at least eight weeks at the target dose", a review of partial effect) and Q5 (continuation for 6 or 12 months);
  - S-011 question 4 (a pause after 12–18 months);
  - S-016's "Follow-up review with GP (after 6–8 weeks)";
  - S-018 14C, 14D and 17B.
- **NICE 1.3.27** applies to onabotulinumtoxinA as to every preventive treatment. NICE names no exception, and 1.3.29 adds a stopping rule.
- **INV-001.** The new conjuncts (`preventiveFor`, an adult is aged 12 or older) are satisfiable and exclude only incoherent contexts.
- **Watch points of the oscillation check** (the INV-087 start and lead-in; E-060, E-061 and INV-105; INV-104): unchanged in v06, and not touched by any remark here.
- **S-105 location.** The PHQ-9 range sentence occurs on P. 5/9 and on P. 6/9. The cited P. 6/9 location, under the heading of the quote, is correct.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the AAN/AHS 14A and NVN window readings (R07-02 concerns only which types 14A applies to);
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
  - the E-060 lead-in wording.
- **Section 8.** Every entry is founded and is pointed to from the elements it affects:
  - ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded;
  - ISS-02 was re-verified: "simple analgesics" occurs only on p. 139 of ICHD-3.

  R07-01 and R07-02 are defects of the model, not Stage 1 issues: the OUT-018 Statement already asks for the time points named in the guidance it cites.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and the oscillation check after iteration 04 froze nothing.
