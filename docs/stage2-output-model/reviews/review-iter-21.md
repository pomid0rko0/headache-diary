# Review — iteration 21
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v20
Date: 2026-10-21

## Summary

This is the main review of iteration 21: an independent fact-check and review of v20.

**State of the files.**
- `OUTPUT_MODEL.md` is byte-identical to `history/v20.md` (`cmp`). The working tree was clean at HEAD c4f0d1e ("Stage 2 / iter 20: fix (v20)").
- `FROZEN_ITEMS.md` does not exist, and no item of v20 carries a FROZEN marker.
- v20 differs from v19 only in text (word diff read in full): the section 3.5 reference-rule list, one Notes sentence each in E-022, E-044, E-060, E-061 and INV-086, a new Notes field in INV-060, ISS-03, three traceability coverage reasons (OUT-008, OUT-019, OUT-030), section 9, the search log and the change log. No `omn` block changed.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5;
- v20, all sections: every element and invariant, the traceability table, section 8, the sources, the search log, and the change log in outline;
- review 20 and fix 20;
- the oscillation check after iteration 16, with its eight watch points.

I consulted the other reviews and fixes by search, to see which points were settled or declined.

**My own work.**
- Downloads: all with `curl` into the fresh directory `/tmp/r21-dl-EOMU`, outside the repository.
- Text: extracted into `/tmp/r21-txt-0L6e`.
- Scripts: in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r21/` (`strip.py`, `match2.py`, `onpage.py`, `mech.py`, `decl2.py`), run with `python3 -I`.

**Result.**
- **Values and citations.** All quotes are verbatim at the stated URLs and locations. All values, codes, labels, ranges, thresholds and offsets are correct against their sources.
- **Mechanical checks.** They pass.
- **Scope sweep.** It finds no input, storage or derivation content.
- **Fidelity.** Every OUT requirement is represented at its Stage 1 strength.
- **Section 8.** Every entry is founded, and no Stage 1 issue is silently worked around.
- **Remarks.** I found no issue that requires a change under PROCESS.md section 9.

## Verification coverage

### Downloads and method

All 32 downloads returned HTTP 200.

**PDFs** (page by page with `pdftotext -raw` and `-layout`):
- [S-001] ICHD-3, 211 pp.; [S-002], 19 pp.; [S-005], 14 pp.; [S-007] UCL accepted manuscript, 39 pp.;
- [S-008], 31 pp.; [S-010], 11 pp.; [S-016] SIGN 155, 64 pp.; [S-018] AAN/AHS Clinician Summary, 12 pp.;
- [S-030]; [S-033], 92 pp.; [S-034], 53 pp.; [S-035], 92 pp. (PDF created 28 August 2025); [S-105], 9 pp.

**Web pages** (markup removed):
- [S-015]: the CG150 Recommendations page ("Last updated: 03 June 2025") and its Overview page;
- [S-028]: the NVN module;
- [S-103]: the Cincinnati Children's PedMIDAS page;
- [S-106]: TA260, the Overview page ("Published: 27 June 2012", "Last reviewed: 11 January 2016"), chapter 1 and chapter 2.

**Europe PMC full-text XML:**
- [S-011] PMC9188162, [S-012] PMC9555163, [S-013] PMC7296705, [S-014] PMC6734476, [S-023] PMC9607711;
- [S-101] PMC3057423, [S-102] PMC4406925, [S-104] PMC183845;
- PMC8684566 and PMC6537129 (the MIDAS label variants named in the search log).

**Rendered and read by eye:**
- ICHD-3 p. 190. It shows A1.1.1 B "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)", A1.1.2 B "Occurring on day 1 ± 2 (i.e. days −2 to +3)", note 2 "The first day of menstruation is day 1 and the preceding day is day −1; there is no day 0.", and the A1.1 comment "This subclassification of 1.1 Migraine without aura is clearly applicable only to menstruating women as defined above." In the text layer the "±" and "−" glyphs are unmapped.
- The [S-034] title page, an image: "Возрастная группа" "дети".

**Matching script.** `match2.py` works on every line outside `omn` blocks that carries an `[S-NNN]` tag:
1. It pairs the line's double-quote marks in sequence and attributes each quoted string to the nearest preceding tag.
2. It splits the string at "[...]" and keeps fragments with at least 6 letters or digits.
3. It searches each fragment, after normalisation (NFKC, soft hyphens removed, line-end hyphens joined, case folded, letters and digits only), in this order:
   - the tagged source, page by page;
   - the other sources tagged on the line;
   - Stage 1 v18.

`onpage.py` then confirmed each stated page separately for the Stage 2 quotes. For example:
- [S-001] pp. 8, 9, 12, 104, 105, 122–125, 139, 190, 209;
- [S-008] pp. 9, 11, 12, 13, 17;
- [S-010] p. 6;
- [S-016] PDF pp. 7, 20;
- [S-018] pp. 1, 7, 8, 9;
- [S-033] pp. 1, 4, 39, 40, 41, 53;
- [S-034] pp. 17, 52;
- [S-035] PDF pp. 7, 23, 48 (Kutu 8, items 2 and 7, counted on the page), 52, 57, 77, 80, 82, 83, 86;
- [S-105] P.6/9 and P.8/9 (page footers in the PDF).

Every fragment that the script did not place was read by hand.

### Quotes per source

The source column is the nearest preceding tag on the line. "Other tag" means the fragment was found in another source tagged on the same line; this mostly concerns the many-tag paragraphs of the E-041 and E-045 Notes.

| Source (nearest tag) | Fragments | In tagged source | Other tag on line | Stage 1 text | By hand / rendered | Translations, not source text | Not found | Unreachable (tried) |
|---|---|---|---|---|---|---|---|---|
| S-001 ICHD-3 | 65 | 60 | 0 | 1 | 3 (p. 190 rendered: the two A1.1 windows, as quoted in E-060 and INV-087) | 1 (search-log row label) | 0 | 0 |
| S-002, S-005, S-007 | 24 | 12 | 7 | 5 | 0 | 0 | 0 | 0 |
| S-008 IHS 2024 | 27 | 19 | 8 | 0 | 0 | 0 | 0 | 0 |
| S-010 IHS 2025 | 38 | 33 | 1 | 4 | 0 | 0 | 0 | 0 |
| S-011, S-012, S-013, S-016, S-018, S-023, S-029, S-030, S-032, S-042 | 48 | 34 | 12 | 2 | 0 (plus the EHF 2022 "In selected cases …" sentence, checked directly in PMC9188162) | 0 | 0 | 0 |
| S-014 Lifting The Burden | 37 | 31 | 1 | 4 | 1 ("acceptable for treatment continuation beyond three months", on a line tagged S-014: [S-008] p. 12) | 0 | 0 | 0 |
| S-015 NICE CG150 | 42 | 35 | 4 | 2 | 1 (the same [S-008] phrase, p. 12) | 0 | 0 | 0 |
| S-028 NVN | 13 | 10 | 2 | 0 | 0 | 1 translation | 0 | 0 |
| S-033 Russian adults | 47 | 21 | 22 | 0 | 0 | 4 translations | 0 | 0 |
| S-034 Russian children | 17 | 8 | 2 | 1 | 2 (title page, rendered) | 4 translations | 0 | 0 |
| S-035 Turkish protocol | 50 | 33 | 4 | 0 | 0 | 13 translations | 0 | 0 |
| S-101 to S-106 | 34 | 30 | 2 | 0 | 2 (search log: "little or none" in PMC8684566, 2021; "minimal or infrequent disability" with grade IVa in PMC6537129, 2019) | 0 | 0 | 0 |
| **Total** | **442** | **326** | **65** | **19** | **9** | **23** | **0** | **0** |

**Translations.** I read every Stage 2 translation against its original, and all are faithful:
- [S-028]: the PICO line;
- [S-033]: the title page, the section 3.3 comment and the PREEMPT recommendation (pp. 39–40), and the p. 41 comment;
- [S-034]: the flowchart box (p. 52), the title page and section 2 (p. 17);
- [S-035]: Kutu 8 items 2 and 7; 3.3 b; the three 3.6.3.9 sentences; the section 6 and chapter 7 headings; the 7.1 and 7.3 items.

### Citation metadata and versions

- **Europe PMC records** agree with section 10:
  - S-101: Cephalalgia 2011;31(3):357–367; 10.1177/0333102410379890; PMID 20819842; "Validation Study";
  - S-102: J Headache Pain 2015;16:24; 10.1186/s10194-015-0503-y; PMID 25902814; Stewart and Lipton among the authors;
  - S-104: HQLO 2003;1:29; 10.1186/1477-7525-1-29; PMID 12914662;
  - the S-103 developer paper: Neurology 2001;57(11):2034–2039; 10.1212/wnl.57.11.2034; PMID 11739822.
- **S-105.** PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014. The developers sentence is on P.8/9.
- **S-106.** Paragraph 2.1 ends "The recommended re-treatment schedule is every 12 weeks (see the summary of product characteristics)." Recommendation 1.2 reads "less than a 30% reduction in headache days per month after 2 treatment cycles".
- **NICE CG150 recommendation numbers.** Each matches its text on the downloaded page: 1.2.6, 1.3.9, 1.3.21, 1.3.24, 1.3.26, 1.3.27 (under "Prophylactic treatment review"), 1.3.28, 1.3.29, 1.3.37, 1.3.39 and 1.3.48. The Overview population sentence reads as quoted.
- **Newer versions.**
  - A web search finds no published ICHD-4, only "ICHD-4 – Work in Progress 1" (Cephalalgia 2024), so ICHD-3 is current.
  - CG150 is current (last updated 3 June 2025), and so is TA260.
  - I found no newer version of any cited source that changes an element.

### Value sets, codes, units, labels and thresholds (category B)

All of these are correct against the downloaded sources:
- **ICHD-3 code labels** (E-009), pp. 8, 9 and 12.
- **8.2 reference levels and span** (E-032):
  - 15 days per month for non-opioid analgesics;
  - 10 days per month for ergotamine, triptans, opioids, combination analgesics, other medication and 8.2.6 combined use;
  - more than three months for all (pp. 122–125).
  - The 8.2.6 classes (`classesOf826`) match criterion B and notes 1–2 (pp. 124–125), and the 8.2.3 comment on cumulative non-opioid use (p. 123).
- **The span by script logic.** With calendar months or 28-day periods, the shortest span "lasting more than three months" has four periods.
- **The A1.1 window.** Day 1 ± 2, days −2 to +3, no day 0. The derived offsets of INV-087 (`nextWindowDays`, the window) agree with it.
- **Cluster remission.** It "must exceed three months".
- **Instruments:**
  - HIT-6: range 36–78 and the four bands;
  - MIDAS: grades I–IV with the [S-102] labels and bands, and a 3-month recall;
  - PedMIDAS: four grades, with "Greater than 50" shown as `strictLow`;
  - HALT-90: Table 18 bands, labels and grades (overlap at 20); HALT-30 and HALT-90 recall;
  - HADS: 0–21 per subscale; PHQ-9: 0–27; GAD-7: 0–21.
- **Named responder criteria:**
  - NICE 1.3.28: 50 % episodic, 30 % chronic;
  - NICE 1.3.29: 30 % of headache days;
  - IHS Q6: 50 %; 30 % in its chronic alternative; MIDAS ≥ 5 points for baseline 11–20 and ≥ 30 % for baseline ≥ 20; HIT-6 ≥ 5 points;
  - DMKG/ÖKSG/SKG: 50 %, HIT-6 5 points, MIDAS 30 %;
  - Russian section 7.1: 50 % of headache days;
  - the IHS 2025 control levels.
- **The 18 evaluation rules.** I checked offsets, anchors, timings, ages and exclusions against their quotes.
- **Non-quote location claims in the E-041 Notes.** I spot-checked these, and they hold:
  - AAN/AHS 14C and 17B;
  - the IHS Q2 comment on onabotulinumtoxinA after the first cycle;
  - the IHS Q6 Background "two- to three-month evaluation period … (82)";
  - the Russian 12-week botulinum interval;
  - the NVN placebo response that stabilises after 16 weeks;
  - the Turkish onset of 2–3 months and maximum within six months (p. 48), and "Tedavi süresi en az 4 ay" (p. 80);
  - the Russian paediatric courses of at least 3 months.
- **Date examples, recomputed:**
  - 15 August to 20 October is 67 days;
  - 10 March to 21 April is 43 days, and the longest 28-day time range ends on 6 April, with the review window from 7 April to 5 May;
  - for 1 January 2026: the 12-week time point is 26 March, its final 28 days are 26 February to 25 March, and the 3-month time point is 1 April;
  - stops on 10 February, 30 March and 31 March give the stated time points;
  - 4 to 31 December is 28 days.

### Fidelity to Stage 1 (category C), requirement by requirement

| OUT | Result |
|---|---|
| 001 | OK. A period with start, end and length (E-003, E-005, INV-002, INV-003). Monthly frequency outputs at MUST (INV-014, INV-015, INV-108). Equal-length comparison (INV-037, INV-055). Caveat met by `lengthDays`. |
| 002 | OK. INV-008 (SHOULD) over every form of the four measures (`reports`). |
| 003 | OK. INV-011, INV-012; no cut-off presented as validated (INV-013, SHOULD NOT). |
| 004 | OK. Every period of the selected time range (INV-014, MUST); ICHD-3 definition (INV-009, MUST). |
| 005 | OK. For patients with migraine (INV-015, MUST); label SHOULD (INV-008). |
| 006, 007 | OK. Provision at SHOULD (INV-016, INV-017); monthly availability at MUST where provided (INV-108); attacks are a separate element (E-019) with the ICHD-3 label (INV-010). |
| 008 | OK. MAY elements (E-020 to E-022) with an optional exploratory label; see ISS-03 and ISS-04. |
| 009 | OK. Time course with start, dose-change and stop markers in the view (INV-034 to INV-036); weekly values where relevant (INV-001, INV-034). |
| 010 | OK. Stated scale (INV-018); comparison between periods (INV-039). |
| 011 | OK. INV-019; label for treated attacks (INV-020); the Caveat as SHOULD NOT (INV-021). |
| 012 | OK. Across periods (INV-022) and per treated attack (INV-072, INV-076), for migraine. |
| 013 | OK. MAY (E-027), separate from headache measures. |
| 014 | OK. Total, class and drug together (INV-023); relations (INV-024). |
| 015 | OK. Calendar-week view (E-036, INV-025). |
| 016 | OK. Per period, per class and for combined use, with code, level, span and basis (INV-044 to INV-046); prompt at MUST (INV-047); not a diagnosis at MUST NOT (INV-048); see ISS-01. |
| 017 | OK. INV-049 to INV-052; see ISS-11. |
| 018 | OK. INV-053 to INV-059; no continuation decision at MUST NOT (INV-106); see ISS-03 and ISS-10. |
| 019 | OK. SHOULD (E-044, INV-060, INV-061); since v20, ISS-03 covers the residual migraine days, and ISS-05 the single count. |
| 020 | OK. INV-062 to INV-065; see ISS-08. |
| 021 | OK. MUST components (INV-068, INV-102); SHOULD components where provided (INV-069, INV-071, INV-072). |
| 022 | OK. INV-070, INV-103. |
| 023 | OK. INV-071 to INV-075; no decision on the definition of response at SHOULD NOT (INV-107). |
| 024 | OK. INV-077 to INV-079, INV-109. |
| 025 | OK. MAY (E-056, INV-080). |
| 039 | OK. INV-066, INV-067, INV-104, INV-109. |
| 026 | OK. INV-081, INV-082, INV-100; see ISS-06. |
| 027 | OK. INV-026, INV-027, INV-033. |
| 028 | OK. INV-040 to INV-043 (MUST, SHOULD, SHOULD NOT as in Stage 1); see ISS-03. |
| 029 | OK. INV-028 (MUST), INV-029 (SHOULD), INV-030; see ISS-09. |
| 030 | OK. MUST (E-060, E-061, INV-086, INV-087); since v20, ISS-03 records the missing migraine condition. |
| 031 | OK. INV-088, INV-089. |
| 032 | OK. MAY, with caveats at SHOULD (INV-090, INV-100, INV-110). |
| 033 | OK. INV-083 to INV-085, INV-100. |
| 034 | OK. INV-094, INV-104; see ISS-04. |
| 035 | OK. INV-095, INV-105; see ISS-03. |
| 036 | OK. INV-096 to INV-098; E-041 `ruleRuChildren`; INV-055. |
| 037 | OK. INV-091 to INV-093. |
| 038 | OK. INV-099 to INV-101. |

Every conformance level matches the strength of the Stage 1 statement part it realises. Every SHOULD NOT or MUST NOT part, or negative form of a Caveat, is a `¬` invariant at that level:
- INV-013, INV-021, INV-043, INV-065, INV-084, INV-091, INV-101 and INV-107 at SHOULD NOT;
- INV-048 and INV-106 at MUST NOT.

I also checked that no SHOULD or MAY element carries a MUST attribute without a MUST statement part that requires it (section 3.3, item 3).

### Mechanical checks (category E)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), with no gaps and no duplicates. No dangling E- or INV- reference. Every S reference lies in S-001–S-046 or S-101–S-106. Exactly the 39 Stage 1 OUT IDs are referenced. |
| Fields | 177 items, each with exactly one Realises, Conformance and Evidence field and at most one Notes field. Every invariant has one Predicate and one Reading, and every element one Definition and one Meaning. |
| Traceability | 39 rows, in Stage 1 order (OUT-039 after OUT-025), all "full". For every requirement, the row's E and INV sets equal the reverse index of the Realises fields: 0 mismatches. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Every MUST NOT and SHOULD NOT predicate begins with `¬`, and no positive-level predicate is a bare prohibition. |
| Declarations | 181 `omn` blocks; 555 declared names by my script's count (types, enum constants, variant tags, constants, functions, predicates), none declared twice. With text literals removed, the only undeclared identifiers are the bound variables A, C, D, K, Ks and L, and `refs` (defined in section 2.5). Every attribute selection `e.a` names a declared attribute or component. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2). Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type: 0 violations. |
| `opt` used as a single value | I read every use of every `opt` attribute in the predicates (for example `completionDate`, `totalScore`, `latest`, `series`, `reviewWindow`, `baseline`, `start`, `formulation`, `maxOffset`, `baselineAtLeast`, `headacheType`, `schemeSelection`). Each is used as a set, compared with a set display, or quantified over (section 2.6). |
| Partial terms | `days`, `÷`, `first`, `last`, `min`, `max`, `periodEndFrom` and `classOf` are guarded where used: INV-012, INV-024, INV-037, INV-041, INV-053, INV-069, INV-074, INV-079, INV-087, INV-089 and E-046 `scoreMet`. |

### Scope sweep (category F)

- **Grep.** I searched the model for enter/entry, record, input, captur, logged, stor(e/age), persist, database, JSON, XML, CSV, FHIR, HL7, serializ/serialis, encod, retention, reminder, answer, algorithm, data-entry, data field, obtained from, calculat, comput and "decision logic", and read every hit in context.
- **Hits.** Every hit is one of these:
  - an exclusion statement (sections 1, 2.1, 2.7);
  - an out-of-scope note (E-014, E-019, E-057, INV-076);
  - the instrument-recall quote of [S-014] ("records days affected during the preceding 1 month"), quoted for the HALT-30 recall period;
  - "can be answered with" (INV-014 Reading);
  - a search-log tool name.
- **Relations.** Every relation and threshold takes as arguments only output elements, context properties stated as Stage 1 states them, and cited constants.
- **Required content.** The thresholds, formulas and computed fields that are part of the output data are present, each with its relation where it has one over output elements:
  - change from baseline: INV-053;
  - total and classes: INV-024;
  - overuse indicator: INV-045, INV-046;
  - instrument category and change: INV-082;
  - responder thresholds: E-045, INV-063, INV-064;
  - completeness proportion: INV-012;
  - durations: INV-079, INV-089;
  - rates: INV-089;
  - evaluation dates and review window: INV-058, INV-051;
  - perimenstrual window and complete cycles: INV-087;
  - outcome proportions: INV-074.

### Section 8 (category G)

- **ISS-01 to ISS-06 and ISS-08 to ISS-11.** Each is founded, and its quotes and locations are correct:
  - ISS-01: 8.2.6 criterion B and its notes 1–2 do not name combination analgesics (pp. 124–125);
  - ISS-02: pp. 12, 105, 123 and 139;
  - ISS-03 (v20): the [S-001] A1.1 comment (p. 190), the OUT-019 and OUT-030 Rationales, and the list of seven statements against the Stage 1 Statements;
  - ISS-06: [S-008] "Patient Global Impression scales";
  - ISS-09: [S-001] p. 122;
  - ISS-10: NICE 1.3.9 and 1.3.39, and [S-034] p. 52;
  - ISS-11: the CG150 population sentence and 1.3.48.
- **Silent workarounds.** I found no Stage 1 issue that the model works around without recording it.

## Remarks

None.

## Checked and not raised

- **The v20 changes.**
  - ISS-03 now lists OUT-008, OUT-018, OUT-019, OUT-022, OUT-028, OUT-030 and OUT-035, and this matches the Stage 1 Statements.
  - Its claims about OUT-002, OUT-007, OUT-009, OUT-020, OUT-021 and OUT-034 are correct.
  - The new [S-001] quote is verbatim (p. 190, rendered).
  - "Stage 1 groups [OUT-028 and OUT-030] among the outputs that support diagnosis and classification" is correct (Group G).
  - The new Notes pointers and coverage reasons are consistent with the unchanged predicates.
- **Settled points, not reopened (no new evidence):**
  - INV-060 with INV-061 for compared periods shorter than 28 days (declined in fix 02, item 14);
  - `concerns` for all-types indices of mixed subjects (INV-091 to INV-093; review 01);
  - the cluster-view bouts, remissions and rates as references without co-presence (fix 11: OUT-031 asks for no single view);
  - the OUT-023 outcome set kept for cluster-headache and non-migraine summaries (review 14: the model follows Stage 1 and works nothing around);
  - INV-106 at MUST NOT;
  - the "> 3 months" readings (INV-045, INV-089);
  - the HIT-6 1-month recall;
  - HADS subscales only;
  - the MIDAS labels of [S-102];
  - "baseline administration" as any earlier administration;
  - INV-027 tied to preventive treatments;
  - "one item suffices" for the overview's treatment effect (watch point 1).
- **INV-031, the conjunct "a view that marks such periods marks every period whose migraine-day count is 0".**
  - It is unchanged since v00 and has been reviewed in every iteration.
  - It is satisfiable, because a mark (E-022, MAY) can always be added, and it keeps the marking of one view consistent.
  - I have no evidence that it excludes an output Stage 1 permits in substance. Not raised.
- **E-041 rule list (watch point 5).**
  - The IHS 2024 Q6 Background "two- to three-month evaluation period (starting once the maximally tolerated dose has been reached)" cites other expert recommendations (its reference 82). The E-041 Notes classify it as a report of other guidelines.
  - The IHS Q2 comment observes later responders "after the second or third cycle" and asks for a dose increase after the first cycle. Neither is a recommended evaluation time point.
  - The classification is consistent with the settled criterion, and changing it would touch watch point 5. Not raised.
- **Untranslated heading.**
  - E-041 Evidence quotes the [S-035] heading "3. MİGREN BAŞ AĞRISI TEDAVİSİ" without a translation (since v07).
  - It is quoted only to show that the heading names migraine, which the surrounding English text states ("name migraine as well").
  - A translation ("3. Treatment of migraine headache") would add nothing to the evidence. Not a remark.
- **HALT versions.** [S-014] says there are three versions of HALT and includes two. A third version can be shown as `otherInstrument`, so the open instrument set covers it.
- **Name reuse in OMN.** Some names serve both as a function and as an attribute or component (`days`, `label`), and `value` is used as an attribute name. Application `f(…)` and selection `e.a` are syntactically distinct, and section 2.5 allows attribute names to recur, so the semantics are not ambiguous. Not a defect.
- **"Early onset of effect" (OUT-009).** It is left to the context flag `weeklyGranularityRelevant`, while tension-type and cluster headache force the flag (INV-001). Stage 1 names no criterion for it that a shown value could be tested against. Not raised.
- **Instrument results in the clinician-facing summary.** INV-104 asks for the results completed within the covered period, which follows OUT-034's period wording. Not raised.
- **Oscillation watch points.** I raise nothing, so no watch-point item is changed or reversed.

## Notes on frozen items (for the human)

None. `FROZEN_ITEMS.md` does not exist, and no item of v20 carries a FROZEN marker.
