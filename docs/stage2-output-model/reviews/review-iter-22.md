# Review — iteration 22
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v21
Date: 2026-10-21

## Summary

This is the main review of iteration 22: an independent fact-check and review of v21.

**State of the files.**
- The working tree was clean at HEAD 06d41ff ("Stage 2 / iter 21: fix (v21)"). `OUTPUT_MODEL.md` is byte-identical to `history/v21.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item of v21 carries a `Status: FROZEN` line (checked by script).
- v21 differs from v20 in text only. I read the word diff in full. No `omn` block changed. The changes are:
  - the new Stage 1 issue ISS-12;
  - the E-063 Meaning;
  - the Notes of E-062, E-063 and INV-089;
  - the coverage reason of row OUT-031;
  - bookkeeping (header, section 9, search log, change log).

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026), the source table of section 5 and the search log of section 6;
- v21, all sections: every element and invariant, the traceability table, section 8, the sources, the search log and the v21 change-log entry;
- review 21, re-check 21b and fix 21;
- the oscillation check after iteration 16, with its watch points and its list of settled points.

I searched the other reviews and fixes for settled and declined points ("remission", "previous bouts", cycle-line MUST attributes in the overview, INV-031).

**My own work.**
- Downloads: all with `curl` through the proxy, into the fresh directory `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r22/dl`, outside the repository.
- Text: extracted page by page into `…/r22/txt`, with `pdftotext -raw` and `-layout`; for HTML and Europe PMC XML, the markup was removed.
- Scripts, in `…/r22/scripts` and run with `python3 -I`: `strip.py`, `match.py`, `onpage.py`, `bullets.py`, `s1quotes.py`, `mech.py` and `decl.py`, plus inline checks.
- Rendered with `pdftoppm` and read: ICHD-3 pp. 42 and 190, and the image-only title page of [S-034].

**Result.**
- **Citations.** Every quote is verbatim at its URL and stated location, and every Stage 2 translation is faithful. The citation metadata of S-101 to S-106 is correct, and I found no newer version of a source that changes an element.
- **Values.** All values, codes, labels, ranges, thresholds and offsets are correct against their sources.
- **Mechanical checks.** They all pass.
- **Scope sweep.** It finds no input, storage or derivation content.
- **Fidelity.** Every OUT requirement is represented at its Stage 1 strength.
- **Section 8.** Every entry, including the new ISS-12, is founded and correctly located, and no Stage 1 issue is silently worked around.
- **Remarks.** I found no issue that requires a change under PROCESS.md section 9.

## Verification coverage

### Downloads

All 36 downloads returned HTTP 200. The two Russian PDFs were reset by the peer on the first attempt and loaded on the retry.

**PDFs** (page counts from `pdfinfo`):

| Source | Pages |
|---|---|
| [S-001] ICHD-3 | 211 |
| [S-002] | 19 |
| [S-003] | 18 |
| [S-005] | 14 |
| [S-006] | 16 |
| [S-007] UCL accepted manuscript | 39 |
| [S-008] | 31 |
| [S-010] | 11 |
| [S-016] SIGN 155 (2026 update) | 64 |
| [S-018] AAN/AHS Clinician Summary | 12 |
| [S-030] | 86 |
| [S-033] | 92 |
| [S-034] | 53 |
| [S-035] (created 28 August 2025) | 92 |
| [S-105] (author Kurt Kroenke; created 22 June 2010, modified 16 April 2014) | 9 |

**Web pages:**
- [S-015] CG150: the Recommendations page ("Last updated: 03 June 2025") and the Overview page ("Last reviewed: 23 September 2026"; an update of the management section is in development, not published);
- [S-028]: the NVN module;
- [S-103]: the Cincinnati Children's PedMIDAS page ("© 2026");
- [S-106]: TA260, the Overview page ("Published: 27 June 2012", "Last reviewed: 11 January 2016"), chapter 1 and chapter 2.

**Europe PMC full-text XML:**
- PMC6501455 [S-004], PMC9188162 [S-011], PMC9555163 [S-012], PMC7296705 [S-013], PMC6734476 [S-014], PMC9607711 [S-023], PMC12279330 [S-042], PMC13169912 [S-043];
- PMC3057423 [S-101], PMC4406925 [S-102], PMC183845 [S-104];
- PMC8684566 and PMC6537129, the MIDAS label variants named in the search log.

### Method

**`match.py`.**
1. For every line outside the `omn` blocks that carries an `[S-NNN]` tag, it pairs the double quotes in sequence and attributes each quoted string to the nearest preceding tag.
2. It splits each string at "[...]" and keeps fragments with at least 6 letters or digits.
3. It searches each fragment, after normalisation (NFKC, soft hyphens removed, line-end hyphens joined, case folded, letters and digits only), in this order:
   - the tagged source, page by page;
   - the other sources tagged on the same line;
   - Stage 1 v18.

**`onpage.py` and `bullets.py`.** They compare each placed fragment of a paged source with the page stated after the quote. Every Stage 2 quote of the Evidence sub-bullets and of section 8 was found on its stated page, for example:
- [S-001] pp. 8, 9, 12, 105, 122–125, 139, 190, 209, and p. 42 for the five new ISS-12 quotes;
- [S-008] pp. 9 and 12–13;
- [S-010] p. 6;
- [S-016] PDF p. 7 = printed p. 1;
- [S-018] pp. 1, 7, 8;
- [S-033] pp. 1, 4, 39, 40, 41, 53;
- [S-034] pp. 17, 52;
- [S-035] PDF pp. 23, 48, 57, 77, 82, 83, 86;
- [S-105] P.6/9 and P.8/9.

The only "mismatches" reported are parsing artefacts of the long E-041 and search-log paragraphs, where the stated page belongs to a neighbouring parenthesis. I read each one by hand; each quote is on the page its own parenthesis states.

**`s1quotes.py`.** It checks the 289 quoted fragments on lines without a source tag against Stage 1 v18. The 26 it did not place are one of:
- the model's own terms or paraphrases, for example "definitional" or "K is available when C";
- source strings that I found in their sources: "минимум" ([S-033] p. 39), "en az 2-3 ay" ([S-035] p. 48), "in at least two out of three menstrual cycles" ([S-001] p. 190), the [S-103] page heading and the [S-105] developers sentence (P.8/9).

### Quotes per source

The source column is the nearest preceding tag on the line. "Other tag" means the fragment was found in another source tagged on the same line; this is mostly the many-tag paragraphs of the E-041 and E-045 Notes, where the tag follows its quote.

| Source (nearest tag) | Fragments | In tagged source | Other tag on line | Stage 1 text | By hand / rendered | Translations, not source text | Search-log query or row text, not source text | Not found | Unreachable (tried) |
|---|---|---|---|---|---|---|---|---|---|
| S-001 ICHD-3 | 88 | 78 | 0 | 6 | 3 (p. 190 rendered: the A1.1.1 and A1.1.2 windows in E-060 and INV-087, with the unmapped "±" and "−") | 0 | 1 | 0 | 0 |
| S-002, S-005, S-007 | 30 | 17 | 7 | 6 | 0 | 0 | 0 | 0 | 0 |
| S-008 IHS 2024 | 29 | 21 | 8 | 0 | 0 | 0 | 0 | 0 | 0 |
| S-010 IHS 2025 | 48 | 39 | 1 | 8 | 0 | 0 | 0 | 0 | 0 |
| S-011, S-012, S-013, S-016, S-018, S-023, S-029, S-030, S-032, S-042 | 52 | 36 | 12 | 4 | 0 | 0 | 0 | 0 | 0 |
| S-014 Lifting The Burden | 45 | 34 | 1 | 9 | 1 ("acceptable for treatment continuation beyond three months", an [S-008] phrase on a line tagged S-014: [S-008] p. 12) | 0 | 0 | 0 | 0 |
| S-015 NICE CG150 | 56 | 39 | 4 | 12 | 1 (the same [S-008] phrase, p. 12) | 0 | 0 | 0 | 0 |
| S-028 NVN | 13 | 10 | 2 | 0 | 0 | 1 | 0 | 0 | 0 |
| S-033 Russian adults | 49 | 21 | 24 | 0 | 0 | 4 | 0 | 0 | 0 |
| S-034 Russian children | 20 | 8 | 2 | 4 | 2 (title page, an image, rendered: "Возрастная группа" "дети") | 4 | 0 | 0 | 0 |
| S-035 Turkish protocol | 50 | 33 | 4 | 0 | 0 | 13 | 0 | 0 | 0 |
| S-101 to S-106 | 50 | 31 | 3 | 1 | 2 (search log: "little or none" in PMC8684566; "minimal or infrequent disability" in PMC6537129, with grades IVa and IVb) | 0 | 13 | 0 | 0 |
| **Total** | **530** | **367** | **68** | **50** | **9** | **22** | **14** | **0** | **0** |

**Translations.** I read every Stage 2 translation against its original, and all are faithful:
- [S-028]: the PICO line;
- [S-033]: the title page, the section 3.3 comment (p. 39), the PREEMPT recommendation (p. 40) and the p. 41 comment;
- [S-034]: the flowchart box (p. 52), the title page and section 2 (p. 17);
- [S-035]:
  - Kutu 8, items 2 and 7, and section 3.3 b;
  - the three 3.6.3.9 sentences;
  - the section 6 and chapter 7 headings;
  - the section 7.1 and 7.3 items.

### Citation metadata and versions

- **Europe PMC records** agree with section 10:
  - S-101: Cephalalgia 2011;31(3):357–367; 10.1177/0333102410379890; PMID 20819842; "Validation Study";
  - S-102: J Headache Pain 2015;16:24; 10.1186/s10194-015-0503-y; PMID 25902814; Stewart and Lipton among the authors;
  - S-104: Health Qual Life Outcomes 2003;1:29; 10.1186/1477-7525-1-29; PMID 12914662;
  - the S-103 developer paper: Neurology 2001;57(11):2034–2039; 10.1212/wnl.57.11.2034; PMID 11739822.
- **S-105.** The developers sentence is on P.8/9, under the heading "QUESTIONS REGARDING DEVELOPMENT, ACKNOWLEDGMENTS AND USE".
- **S-106.** Paragraph 2.1 gives "every 12 weeks".
- **Newer versions.**
  - A web search finds only "ICHD-4 – Work in Progress 1" (Cephalalgia 2024), so ICHD-3 is current.
  - A web search finds no EHF update after the 2022 CGRP-mAb guideline.
  - CG150 has an update in development, not published.
  - TA260 is unchanged since its 2016 review.
  - No newer version changes an element.

### Value sets, codes, units, labels and thresholds (category B)

All of these are correct against the downloaded sources:
- **ICHD-3 code labels** (E-009). All 15 match the classification list exactly, character for character (`pdftotext -layout`, pp. 8, 9, 12).
- **8.2 reference levels and span** (E-032, pp. 122–125):
  - 15 days per month for 8.2.3;
  - 10 days per month for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8;
  - more than three months for all.
- **`classesOf826` and `classesOf821to825`**, against 8.2.6 criterion B and note 2.
- **The A1.1 window**, day 1 ± 2 (days −2 to +3, no day 0), read on the rendered p. 190.
- **The remission duration**, p. 209, and the ISS-12 wordings on p. 42, read on the rendered page.
- **Instruments:**
  - HIT-6: range 36–78 and the four bands ([S-101]);
  - MIDAS: grades I–IV with the [S-102] labels and bands, and a 3-month recall;
  - PedMIDAS: four grades, with "Greater than 50" ([S-103]);
  - HALT-90: Table 18, overlapping at 20; HALT-30 and HALT-90 recall ([S-014]);
  - HADS: 0–21 per subscale; PHQ-9: 0–27; GAD-7: 0–21.
- **Named responder criteria:**
  - NICE 1.3.28: 50 % in episodic and 30 % in chronic migraine;
  - NICE 1.3.29: 30 % of headache days;
  - IHS Q6: 50 %, the 30 % chronic alternative, MIDAS ≥ 5 points for baseline 11–20 and ≥ 30 % for baseline ≥ 20, and HIT-6 ≥ 5 points;
  - DMKG/ÖKSG/SKG: 50 %, HIT-6 5 points and MIDAS 30 %;
  - Russian section 7.1: 50 % of headache days;
  - the four IHS 2025 control levels (p. 6).
- **The 18 evaluation rules.** Offsets, anchors, timings, ages and exclusions agree with their quotes.
- **Non-quote claims in the E-041 Notes.** I spot-checked these in the sources, and they hold:
  - AAN/AHS 14C ("by 8 weeks") and 17B (tapering after 6 months);
  - the IHS Q6 Background "two- to three-month evaluation period";
  - NICE 1.3.21 (acupuncture over 5 to 8 weeks);
  - the SIGN checklist, after 2–8 and 6–8 weeks (PDF pp. 40–41);
  - the Russian 12-week interval of botulinum toxin (pp. 41, 43) and the 6–12 months (p. 39);
  - the NVN placebo response that stabilises after 16 weeks;
  - the Turkish onset of 2–3 months and maximum within six months (p. 48), and "Tedavi süresi en az 4 ay" (p. 80);
  - the EHF 2022 sentence "In selected cases decision on treatment maintenance can be readdressed after an additional period of 3 months."
- **ISS-02.** A page-by-page search of the ICHD-3 text layer finds "simple analgesics" only on p. 139, and "ibuprofen or other NSAIDS" on p. 105.

### Fidelity to Stage 1 (category C), requirement by requirement

| OUT | Result |
|---|---|
| 001 | OK. Every view states its period, with start, end and length at MUST (E-003, E-005, INV-002, INV-003). Monthly frequency outputs at MUST (INV-014, INV-015, INV-108). Equal-length comparison (INV-037, INV-055). The Caveat is met by `lengthDays`. |
| 002 | OK. INV-008 (SHOULD), over every form of the four measures (`reports`). |
| 003 | OK. INV-011 and INV-012; no cut-off presented as validated (INV-013, SHOULD NOT). |
| 004, 005 | OK. INV-014 and INV-015 (MUST); ICHD-3 definition (INV-009, MUST); migraine-day label SHOULD (INV-008). |
| 006, 007 | OK. Provision at SHOULD (INV-016, INV-017); monthly availability where provided at MUST (INV-108). Attacks are a separate element with the ICHD-3 label (E-019, INV-010). |
| 008 | OK. MAY elements (E-020 to E-022); see ISS-03 and ISS-04. |
| 009 | OK. Series with start, dose-change and stop markers in the view (INV-034 to INV-036); weekly values where relevant (INV-001, INV-034). |
| 010 | OK. Stated scale (INV-018); comparison between periods (INV-039). |
| 011 | OK. INV-019; label for treated attacks (INV-020); the Caveat as SHOULD NOT (INV-021). |
| 012 | OK. Across periods (INV-022) and per treated attack (INV-072, INV-076), for migraine. |
| 013 | OK. MAY (E-027), separate from headache measures. |
| 014, 015 | OK. Total, class and drug together (INV-023, INV-024); weekly view (E-036, INV-025). |
| 016 | OK. Per period, per class and for combined use, with code, level, span and basis (INV-044 to INV-046); prompt at MUST (INV-047); not a diagnosis at MUST NOT (INV-048); see ISS-01. |
| 017 | OK. INV-049 to INV-052; see ISS-11. |
| 018 | OK. INV-053 to INV-059; no continuation decision at MUST NOT (INV-106); see ISS-03 and ISS-10. |
| 019 | OK. E-044, INV-060, INV-061 (SHOULD); see ISS-03 and ISS-05. |
| 020 | OK. INV-062 to INV-065; see ISS-08. |
| 021 | OK. MUST components (INV-068, INV-102); SHOULD components where provided (INV-069, INV-071, INV-072). |
| 022 | OK. INV-070, INV-103. |
| 023 | OK. INV-071 to INV-075; no decision on the definition of response at SHOULD NOT (INV-107). |
| 024 | OK. INV-077 to INV-079, INV-109; the Caveats are in the E-054 Meaning. |
| 025 | OK. MAY (E-056, INV-080). |
| 039 | OK. INV-066, INV-067, INV-104, INV-109. |
| 026 | OK. INV-081, INV-082, INV-100; see ISS-06. |
| 027 | OK. INV-026, INV-027, INV-033. |
| 028 | OK. INV-040 to INV-043 (MUST, SHOULD and SHOULD NOT, as in Stage 1); see ISS-03. |
| 029 | OK. INV-028 (MUST), INV-029 (SHOULD), INV-030; see ISS-09. |
| 030 | OK. MUST (E-060, E-061, INV-086, INV-087); see ISS-03. |
| 031 | OK. E-062 to E-064, INV-088, INV-089. The remission bound follows the Definitions-of-terms sentence of the definition that Stage 1 quotes, and is now recorded in ISS-12 with pointers from E-062, E-063, INV-089 and row OUT-031. The reading of the Caveat's "each attack-free period" as the remission periods shown is stated in ISS-12 and in the E-063 Notes. |
| 032 | OK. MAY, with the caveats at SHOULD (INV-090, INV-100, INV-110). |
| 033 | OK. INV-083 to INV-085, INV-100. |
| 034 | OK. INV-094, INV-104; see ISS-04. |
| 035 | OK. INV-095, INV-105; see ISS-03. |
| 036 | OK. INV-096 to INV-098; `ruleRuChildren`; INV-055. |
| 037 | OK. INV-091 to INV-093. |
| 038 | OK. INV-099 to INV-101. |

**Conformance levels.** Every invariant level matches the strength of the Stage 1 statement part it realises. Every SHOULD NOT or MUST NOT part, or negative form of a Caveat, is a `¬` invariant at that level:
- INV-013, INV-021, INV-043, INV-065, INV-084, INV-091, INV-101 and INV-107 at SHOULD NOT;
- INV-048 and INV-106 at MUST NOT.

Every MUST attribute realises a MUST statement part:
- `covers`; `start`, `end` and `lengthDays` of a period (OUT-001);
- the overuse-indicator `code`, `referenceLevel`, `span` and `basis` (OUT-016);
- the change, time-point and comparison attributes (OUT-018);
- the review-view periods (OUT-021);
- the cycle-line attributes and `completeCycles` (OUT-030).

### Mechanical checks (category E)

| Check | Result |
|---|---|
| IDs (`mech.py`) | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), with no gaps and no duplicates. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12; ISS-07 appears only as withdrawn. No dangling E-, INV- or ISS- reference. 36 distinct S references, all within S-001–S-046 or S-101–S-106. Exactly the 39 Stage 1 OUT IDs are referenced. |
| Fields | 177 items, each with exactly one Realises, Conformance and Evidence field and at most one Notes field. Every element has one Definition and one Meaning; every invariant has one Predicate and one Reading. No `Status` line. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every requirement, the row's E and INV sets equal the reverse index of the Realises fields: 0 mismatches. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Every MUST NOT and SHOULD NOT predicate begins with `¬`, and no MUST or SHOULD predicate is a bare negation. |
| Declarations (`decl.py`) | 181 `omn` blocks and 556 declared names, none declared twice. With attribute and component names and text literals removed, the only undeclared identifiers are bound variables and `refs` (defined in section 2.5). Every attribute selection `e.a` names a declared attribute or component. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2). Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type: 0 violations. |
| Partial terms (read by hand) | `÷`, `days`, `first`, `last`, `max`, `min`, `s(i)`, `periodEndFrom`, `classOf`, `scoreRange` and `publishedRecall` are guarded where used. These include INV-012, INV-024, INV-041, INV-045, INV-046, INV-053, INV-069, INV-074, INV-079, INV-082, INV-087, INV-089 and E-046 `scoreMet`. Every `opt` attribute used as a single value is quantified over or compared with a set display. |
| Date arithmetic (recomputed) | The 8.2 span has four periods with calendar months and with 28-day periods: `plusMonths(first.start, 3) ≤ last.end`, and the minimality conjunct holds. The review window is days 28 to 56 after the start of withdrawal. The remission bound excludes 1 January – 31 March (exactly three months) and admits 1 January – 1 April. Every window rule begins at least 8 weeks after the start, which INV-055's satisfiability argument uses. |

### Scope sweep (category F)

- **Grep.** I searched the model for enter/entry, record, input, captur…, logged, store/storage, persist…, database, JSON, XML, CSV, FHIR, HL7, serializ/serialis, encod…, retention, reminder, answer…, algorithm…, data entry, data field, calculat…, comput… and "decision logic", and read every hit in context.
- **Hits.** Every hit is one of these:
  - an exclusion statement (sections 1, 2.1, 2.7 and 3.5);
  - an out-of-scope note (E-033, E-057, INV-076);
  - the [S-014] HALT-30 quote "records days affected", quoted for the recall period;
  - "persistent high attack frequency" in an [S-007] quote;
  - "can be answered with" (INV-014 Reading);
  - a search-log or change-log entry.
- **Relations.** Every relation and threshold takes as arguments only output elements, context properties stated as Stage 1 states them, and cited constants.
- **Required content.** The thresholds, formulas and computed fields that are part of the output data are present, each with its relation:
  - change from baseline: INV-053;
  - totals and classes: INV-024;
  - overuse indicator: INV-045, INV-046;
  - instrument category and change: INV-082;
  - responder thresholds: E-045, INV-063, INV-064;
  - completeness proportion: INV-012;
  - durations: INV-079, INV-089;
  - rates: INV-089;
  - outcome proportions: INV-074;
  - evaluation dates: INV-058;
  - review window: INV-051;
  - perimenstrual window and complete cycles: INV-087;
  - remission bound: INV-089.
- **The cluster-period definition.** "Attacks ... at least once every other day" is not turned into an invariant on attack rates within a bout. This is correct: ICHD-3 3.1 note 2 allows less frequent attacks during part of the active time-course, so such an invariant would exclude valid outputs.

### Section 8 (category G)

ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded, and the passages they cite read as described:
- ISS-01: pp. 124–125;
- ISS-02: pp. 12, 105, 123 and 139;
- ISS-03: the Stage 1 Statements and Rationales, and p. 190;
- ISS-05 and ISS-08: [S-010] p. 6;
- ISS-06: [S-014] and [S-008] p. 12;
- ISS-09: p. 122;
- ISS-10: NICE 1.3.9 and 1.3.39, and [S-034] p. 52;
- ISS-11: the CG150 Overview and 1.3.48;
- ISS-12, new in v21:
  - the OUT-031 Statement, Evidence note and Caveat are quoted correctly;
  - the seven [S-001] quotes are verbatim on p. 209 (Definitions of terms: "Cluster remission period" and "Chronic") and p. 42 (3.1 Comments; 3.1.1 Description and criterion B; 3.1.2 Description and criterion B), checked on the rendered pages;
  - its "Effect on the model" agrees with the unchanged INV-089 and E-063.

Every issue is pointed to from the elements it affects. I found no Stage 1 issue that the model works around without recording it.

## Remarks

None.

## Checked and not raised

- **The v21 changes.**
  - The E-063 Meaning now names the Definitions-of-terms duration.
  - The Notes of E-062, E-063 and INV-089 and row OUT-031 point to ISS-12 and are consistent with the unchanged predicate.
  - The change-log count of "six new [S-001] quotes (five on p. 42, one on p. 209)" is correct.
- **Empty `remissions` in chronic cluster headache.** ISS-12 states this as a SHOULD deviation, as fix 02 (item 14) decided. Fix 02 and fix 21 considered it; I have no new evidence. Not raised.
- **"History of previous bouts" (OUT-031).** It is represented by the chronological bout list over a selectable time range. Completeness against the true bout history would need input data. Settled since review 01; not raised.
- **Cluster-view bouts, remissions and rates as references without a co-presence conjunct.** Fix 11 decided this (OUT-031 asks for no single view). Not raised.
- **MUST attributes of a `CycleLine` shown in the patient-facing overview.** Reviews 03 and 10b examined this: a diary that shows the relationship to menstruation otherwise deviates only from the SHOULD of INV-105. Not raised.
- **INV-031, the conjunct "a view that marks such periods marks every period whose migraine-day count is 0".** It keeps the marking of one view consistent with "periods without migraine days" as a per-period measure. Review 21 examined it; I have no new evidence. Not raised.
- **OUT-019 "migraine or headache days".** INV-060 triggers on changes in migraine days and headache days, not on changes in moderate/severe headache days. OUT-019 itself distinguishes "headache days" from "moderate/severe headache days" in the same sentence, so the literal reading is correct.
- **Periods after the as-of date.** No invariant forbids a comparison period after the as-of date, and none is needed. Stage 1 states no such requirement, every MUST that the model places on dated content is reachable with periods on or before the as-of date (INV-055 asks only for time points reached by the as-of date), and section 3.7 admits other content.
- **The S-102 author name.** "Pavlovic" in section 10 is printed "Pavlović" in Europe PMC. This is a diacritic only; the record is unambiguous through its DOI and PMID. Not a citation defect.
- **The S-105 section heading.** It is quoted in title case ("Questions regarding development, acknowledgments and use"); the PDF prints it in capitals. The wording is identical. Not a misquote.
- **Settled points, not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the "> 3 months" readings (INV-045, INV-089);
  - the HIT-6 one-month recall; HADS subscales only; the MIDAS labels of [S-102];
  - "baseline administration" as any earlier administration;
  - INV-027 tied to preventive treatments;
  - the E-041 rule list and the `excludes` values and criterion (watch point 5);
  - "one item suffices" for the overview's treatment effect (watch point 1);
  - INV-098 read on period starts (watch point 6);
  - the history-wide `acuteMedications` (watch point 2).
- **Oscillation watch points.** I raise nothing, so no watch-point item is changed or reversed.

## Notes on frozen items (for the human)

None. `FROZEN_ITEMS.md` does not exist, and no item of v21 carries a FROZEN marker.
