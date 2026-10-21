# Review — iteration 22 (re-check b)
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v21
Date: 2026-10-21

## Summary

This is the first independent re-check of iteration 22. The main review (review-iter-22.md) found no remarks on v21. I verified the sources, the Stage 1 text and the model myself and reached my own verdict. I read the main review only after my own checks, to compare coverage.

**State of the files.**
- The working tree was clean at HEAD 9501557. `OUTPUT_MODEL.md` is byte-identical to `history/v21.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item of v21 carries a `Status: FROZEN` line.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5;
- v21, all sections: every element, every invariant, the traceability table, section 8, the sources, the search log and the change log (entries v14 to v21 in full, earlier entries where they concern an item I examined);
- the v20 → v21 word diff;
- review 22, re-check 21b, fix 21, and the R03-04 entries of review 03 and fix 03;
- the oscillation check after iteration 16, with its watch points and its list of settled points.

I searched all reviews and fixes for declined remarks (only R11-01 (a)/(b) and the optional part of R17-02 were declined) and listed the "Checked and not raised" topics of every review, so that I raise nothing that is settled without new evidence.

**My own work.**
- Downloads: all with `curl` through the proxy, into the fresh directory `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r22b/dl`, outside the repository.
- Text: PDFs extracted page by page with `pdftotext -raw` and `-layout`; markup removed from HTML and Europe PMC XML.
- Scripts in `…/r22b/scripts`, run with `python3 -I`: `strip.py`, `match.py`, `onpage.py`, `mech.py` and `fills.py`, plus inline checks.
- Rendered with `pdftoppm` and read: ICHD-3 pp. 190 and 209, and the image-only title page of [S-034].

**Result.**
- **Citations.** Every quote is verbatim at its URL and on its stated page, and every Stage 2 translation I read is faithful. The metadata of S-101 to S-106 is correct, and I found no newer version of a source that changes an element.
- **Values, mechanical checks, scope.** All values are correct against their sources, the mechanical checks pass, and the scope sweep finds no input, storage or derivation content.
- **Fidelity and section 8.** Every OUT requirement is represented at its Stage 1 strength, and section 8 is founded.
- **One remark (R22b-01), a formal defect.**
  - For 28-day periods, the predicate `fillsPeriod` (E-006) admits a series that is offset within the covered period and has one 28-day period fewer than fit.
  - This also holds when the covered period is an exact run of 28-day periods, for example the selected time range that INV-094 and INV-095 make the clinician-facing summary and the patient-facing overview cover.
  - E-006, INV-104, INV-105 and rows OUT-034 and OUT-035 state the opposite: the series "consists of all whole periods of its granularity", "cannot shrink to a single period of a longer covered period" and, for a run of whole periods, "spans it exactly".
  - No earlier review or fix examined offset 28-day series. They checked only the anchored construction, which shows that the predicate can be met, not what else it admits.

## Verification coverage

### Downloads

All downloads used by the checks returned HTTP 200. The two Russian PDFs and brainmed.com were reset by the peer on the first attempt; the Russian PDFs loaded on the retry. PubMed returned a bot-check page (HTTP 203) for S-044. Neither S-032 nor S-044 carries a Stage 2 quote: their fragments in the model are Stage 1 quotes, found in the Stage 1 text.

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
| [S-009] | 45 |
| [S-010] | 11 |
| [S-016] SIGN 155, 2026 update | 64 |
| [S-018] | 12 |
| [S-020] | 12 |
| [S-030] | 86 |
| [S-033] | 92 |
| [S-034] | 53 |
| [S-035] | 92 |
| [S-046] | 12 |
| [S-105] | 9 |

**Web pages:**
- [S-015]: the CG150 Recommendations page and the Overview page ("Last reviewed: 23 September 2026");
- [S-028] and [S-029]: the NVN modules;
- [S-103]: the Cincinnati Children's PedMIDAS page ("© 2026 Cincinnati Children's");
- [S-106]: TA260, the Overview page ("Last reviewed: 11 January 2016"), chapter 1 and chapter 2.

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
   - Stage 1 v18;
   - all other downloaded texts.

**`onpage.py`.** It compares the pages on which each fragment was found with the page stated in the next parenthesis. Every Evidence sub-bullet of sections 5 and 6 and every quote of section 8 is on its stated page. Examples:
- [S-001] pp. 8, 9, 12, 42, 105, 122–125, 139, 190, 209;
- [S-008] pp. 9, 12, 13, 17;
- [S-010] p. 6;
- [S-016] PDF p. 7 = printed p. 1;
- [S-018] pp. 1, 7, 8;
- [S-033] pp. 1, 39, 40, 41, 53;
- [S-034] pp. 17, 52;
- [S-035] PDF pp. 23, 48, 57, 77, 83, 86;
- [S-007] p. 10;
- [S-105] P. 6/9.

The other mismatches the script reports come from the long E-041 Notes and search-log paragraphs, where the parenthesis that follows a quote belongs to a neighbouring item. I read each by hand; each quote is on the page that its own parenthesis states.

**Untagged quotes.** A second script checked the 256 quoted fragments of at least 12 letters or digits on lines without a source tag against Stage 1 v18 and all downloaded texts. The 14 it did not place are the model's own terms or paraphrases, for example "definitional", "K is available when C", "where results are available" and "total score, where the instrument defines one".

### Quotes per source

The source column is the nearest preceding tag on the line. Notes on the columns:
- **Stage 1 wording.** The fragment is a Stage 1 Statement or quote reused on a line tagged with another source, found verbatim in Stage 1 v18.
- **Confirmed otherwise.** The fragment was confirmed on a rendered page or in another downloaded copy:
  - S-001: the A1.1.1 and A1.1.2 windows, whose "±", "−" and "+" are glyphs without a text mapping (p. 190, rendered); the same window on a line where the parser found it next to S-102;
  - S-014 and S-015: the [S-008] phrase "acceptable for treatment continuation beyond three months" ([S-008] p. 12);
  - S-034: "Возрастная группа" "дети" (title page, an image, rendered);
  - S-101 to S-106: the search-log label variants "little or none" (PMC8684566) and "minimal or infrequent disability" (PMC6537129).

| Source (nearest tag) | Fragments | In tagged source | Other tag on line | Stage 1 wording | Confirmed otherwise | Translations (not source text) | Search-log query or row text | Not found | Unreachable (tried) |
|---|---|---|---|---|---|---|---|---|---|
| S-001 ICHD-3 | 88 | 78 | 0 | 6 | 3 | 0 | 1 | 0 | 0 |
| S-002, S-003, S-005, S-006, S-007 | 30 | 17 | 7 | 6 | 0 | 0 | 0 | 0 | 0 |
| S-008 IHS 2024 | 29 | 21 | 8 | 0 | 0 | 0 | 0 | 0 | 0 |
| S-010 IHS 2025 | 48 | 39 | 1 | 8 | 0 | 0 | 0 | 0 | 0 |
| S-011, S-012, S-013, S-016, S-018, S-023, S-029, S-030, S-032, S-042, S-043 | 52 | 37 | 12 | 3 | 0 | 0 | 0 | 0 | 0 |
| S-014 Lifting The Burden | 45 | 34 | 1 | 9 | 1 | 0 | 0 | 0 | 0 |
| S-015 NICE CG150 | 56 | 39 | 4 | 12 | 1 | 0 | 0 | 0 | 0 |
| S-028 NVN | 13 | 10 | 2 | 0 | 0 | 1 | 0 | 0 | 0 |
| S-033 Russian adults | 49 | 21 | 24 | 0 | 0 | 4 | 0 | 0 | 0 |
| S-034 Russian children | 20 | 8 | 2 | 4 | 2 | 4 | 0 | 0 | 0 |
| S-035 Turkish protocol | 50 | 33 | 4 | 0 | 0 | 13 | 0 | 0 | 0 |
| S-101 to S-106 | 50 | 31 | 3 | 1 | 2 | 0 | 13 | 0 | 0 |
| **Total** | **530** | **368** | **68** | **49** | **9** | **22** | **14** | **0** | **0** |

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
  - S-101: Cephalalgia 2011;31(3):357–367; 10.1177/0333102410379890; PMID 20819842; PMC3057423; "Validation Study";
  - S-102: J Headache Pain 2015;16:24; 10.1186/s10194-015-0503-y; PMID 25902814; PMC4406925; Stewart and Lipton among the authors;
  - S-104: Health Qual Life Outcomes 2003;1:29; 10.1186/1477-7525-1-29; PMID 12914662; PMC183845;
  - the S-103 developer paper: Neurology 2001;57(11):2034–2039; 10.1212/wnl.57.11.2034; PMID 11739822.
- **S-105.** PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
- **S-106.** TA260 reads "Last reviewed: 11 January 2016"; paragraph 2.1 gives "every 12 weeks".
- **Newer versions.**
  - Web searches find no new ICHD edition and no EHF update of the CGRP-mAb guideline after 2022.
  - The CG150 Overview page reads "Last reviewed: 23 September 2026", and the Recommendations page still reads "Last updated: 03 June 2025"; the recommendations quoted read as quoted.
  - No newer version changes an element.

### Value sets, codes, units, labels and thresholds (category B)

All of these are correct against the downloaded sources:
- **ICHD-3:**
  - the 15 code labels (pp. 8, 9, 12);
  - the 8.2 reference levels: 15 days per month for 8.2.3, and 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8; more than three months for all (pp. 122–125);
  - `classesOf826` and `classesOf821to825`, against 8.2.6 criterion B and note 2;
  - the A1.1 window, day 1 ± 2 (days −2 to +3, no day 0), read on the rendered p. 190;
  - the remission sentence (p. 209) and the ISS-12 wordings (p. 42).
- **Instruments:**
  - HIT-6: 36–78 and the four bands ([S-101]);
  - MIDAS: grades I–IV with the [S-102] labels and bands, and a three-month recall;
  - PedMIDAS: "0 to 10" "Little to none" … "Greater than 50" "Severe" ([S-103]);
  - HALT-90: Table 18, with "≥20" for grade IV, overlapping at 20; HALT-30 and HALT-90 recall ([S-014]);
  - HADS: 0–21 per subscale ([S-104]); PHQ-9: 0–27; GAD-7: 0–21 ([S-105], P. 6/9).
- **Named responder criteria:**
  - NICE 1.3.28 and 1.3.29;
  - IHS Q6, with the 30 % chronic alternative and the MIDAS and HIT-6 thresholds (pp. 12–13);
  - DMKG/ÖKSG/SKG; Russian section 7.1;
  - the four IHS 2025 control levels (p. 6).
- **The 18 evaluation rules.** Offsets, anchors, timings, ages and exclusions agree with their quotes.
- **Completeness of the rule list.** A scan of the CG150 Recommendations page for weeks, months, cycles and "review" finds no evaluation time point that the list lacks.
- **E-041 Notes claims** spot-checked in the sources, and they hold:
  - the IHS Q2 comment on a dose increase of onabotulinumtoxinA after the first cycle (p. 9);
  - AAN/AHS 17B (p. 9);
  - the NVN placebo response that "na 16 weken weer stabiliseert";
  - the Russian paediatric minimum courses of 3 months (pp. 29–31).

### Fidelity to Stage 1 (category C), requirement by requirement

| OUT | Result |
|---|---|
| 001 | OK. Every view states its period, with start, end and length at MUST (E-003, E-005, INV-002, INV-003). Monthly frequency outputs at MUST (INV-014, INV-015, INV-108). Equal-length comparison (INV-037, INV-055). The Caveat is met by `lengthDays`. |
| 002 | OK. INV-008 (SHOULD) over every form of the four measures (`reports`). |
| 003 | OK. INV-011, INV-012; no cut-off presented as validated (INV-013, SHOULD NOT). |
| 004, 005 | OK. INV-014, INV-015 (MUST); ICHD-3 headache days (INV-009, MUST); migraine-day label (INV-008, SHOULD). |
| 006, 007 | OK. Provision at SHOULD (INV-016, INV-017); monthly availability where provided at MUST (INV-108). Attacks are a separate element (E-019) with the ICHD-3 label (INV-010). |
| 008 | OK. MAY elements (E-020 to E-022); ISS-03, ISS-04. |
| 009 | OK. INV-034 to INV-036; weekly values where relevant (INV-001, INV-034). |
| 010 | OK. INV-018, INV-032, INV-039. |
| 011 | OK. INV-019; label for treated attacks (INV-020); the Caveat at SHOULD NOT (INV-021). |
| 012 | OK. Across periods (INV-022) and per treated attack (INV-072, INV-076). |
| 013 | OK. MAY (E-027), separate from headache measures. |
| 014, 015 | OK. INV-023, INV-024; weekly view (E-036, INV-025). |
| 016 | OK. INV-044 to INV-046; prompt at MUST (INV-047); not a diagnosis at MUST NOT (INV-048); ISS-01. |
| 017 | OK. INV-049 to INV-052; ISS-11. |
| 018 | OK. INV-053 to INV-059; no continuation decision at MUST NOT (INV-106); ISS-03, ISS-10. |
| 019 | OK. E-044, INV-060, INV-061 (SHOULD); ISS-03, ISS-05. |
| 020 | OK. INV-062 to INV-065; ISS-08. |
| 021 | OK. MUST components (INV-068, INV-102); SHOULD components where provided (INV-069, INV-071, INV-072). |
| 022 | OK. INV-070, INV-103. |
| 023 | OK. INV-071 to INV-075; no decision on the definition of response at SHOULD NOT (INV-107). |
| 024 | OK. INV-077 to INV-079, INV-109; the Caveats are in the E-054 Meaning. |
| 025 | OK. MAY (E-056, INV-080). |
| 039 | OK. INV-066, INV-067, INV-104, INV-109. |
| 026 | OK. INV-081, INV-082, INV-100; ISS-06. |
| 027 | OK. INV-026, INV-027, INV-033. |
| 028 | OK. INV-040 to INV-043 at MUST, SHOULD and SHOULD NOT, as in Stage 1; ISS-03. |
| 029 | OK. INV-028 (MUST), INV-029 (SHOULD), INV-030; ISS-09. |
| 030 | OK. MUST (E-060, E-061, INV-086, INV-087); ISS-03. |
| 031 | OK. E-062 to E-064, INV-088, INV-089; ISS-12. |
| 032 | OK. MAY, with the caveats at SHOULD (INV-090, INV-100, INV-110). |
| 033 | OK. INV-083 to INV-085, INV-100. |
| 034 | Represented (INV-094, INV-104; ISS-04). The time course of the summary is the subject of R22b-01. |
| 035 | Represented (INV-095, INV-105; ISS-03). The time course of the overview is the subject of R22b-01. |
| 036 | OK. INV-096 to INV-098; `ruleRuChildren`; INV-055. |
| 037 | OK. INV-091 to INV-093. |
| 038 | OK. INV-099 to INV-101. |

**Conformance levels.** Every invariant level matches the strength of the Stage 1 statement part it realises. Every SHOULD NOT or MUST NOT part, or negative form of a Caveat, is a `¬` invariant at that level:
- INV-013, INV-021, INV-043, INV-065, INV-084, INV-091, INV-101 and INV-107 at SHOULD NOT;
- INV-048 and INV-106 at MUST NOT.

Every MUST attribute realises a MUST statement part:
- `covers` and the period attributes (OUT-001);
- the overuse-indicator attributes (OUT-016);
- the change, time-point and comparison attributes (OUT-018);
- the review-view periods (OUT-021);
- the cycle-line attributes and `completeCycles` (OUT-030).

### Mechanical checks (category E)

| Check (`mech.py`) | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), with no gaps and no duplicates. No dangling E-, INV- or ISS- reference; ISS-07 appears only as withdrawn. 36 distinct S references, all within S-001–S-046 or S-101–S-106. Exactly the 39 Stage 1 OUT IDs are referenced. |
| Fields | Every element and invariant has exactly one Realises, Conformance and Evidence field and at most one Notes field. Every element has one Definition and one Meaning; every invariant has one Predicate and one Reading. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every requirement, the row's E and INV sets equal the reverse index of the Realises fields: 0 mismatches. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Every MUST NOT and SHOULD NOT predicate begins with `¬`, and no MUST or SHOULD predicate is a bare negation. |
| Declarations | No name declared twice; the one duplicate the parser reported comes from the text literal "Tension-type headache". |
| Typing rule for levels | 172 level-annotated attribute declarations, as the change log states. Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type: 0 violations. |
| Partial terms and `opt` use (read by hand) | `÷`, `days`, `first`, `last`, `max`, `min`, `s(i)`, `periodEndFrom`, `classOf`, `scoreRange` and `publishedRecall` are guarded where used. Every `opt` attribute used as a single value is quantified over or compared with a set display. |
| Date arithmetic | Recomputed: the four-period 8.2 span with calendar months and with 28-day periods; the review window, days 28 to 56; the remission bound; the 12-week and 3-month examples of E-042 and INV-055; the 43-day and 67-day examples. |
| `fills.py` | It evaluates `fillsPeriod` for 28-day series literally as written. For every covered length from 56 to 399 days except those of 27 mod 28 (332 of the 344 lengths), it admits a series with one period fewer than fit. This includes every exact multiple of 28. See R22b-01. |

### Scope sweep (category F)

- **Grep.** I searched the model for enter/entry, record, input, captur…, logged, stor…, persist…, database, JSON, XML, CSV, FHIR, HL7, serializ/serialis, encod…, retention, reminder, answer…, algorithm…, data entry, data field, calculat…, comput… and "decision logic", and read every hit in context.
- **Hits.** Every hit is one of these:
  - an exclusion statement (sections 1, 2.1, 2.7 and 3.5);
  - an out-of-scope note (E-033, E-057, INV-076);
  - the [S-014] HALT-30 quote "records days affected", quoted for the recall period;
  - "persistent high attack frequency" in an [S-007] quote;
  - "can be answered with" (INV-014 Reading).
- **Relations.** Every relation and threshold takes as arguments only output elements, context properties stated as Stage 1 states them, and cited constants.
- **Required content.** The thresholds, formulas and computed fields that are part of the output data are present, each with its relation:
  - change from baseline: INV-053;
  - totals and classes: INV-024;
  - overuse indicator: INV-045, INV-046;
  - instrument category and change: INV-082;
  - responder thresholds and control levels: E-045, INV-063, INV-064;
  - completeness proportion: INV-012;
  - durations: INV-079, INV-089;
  - rates: INV-089;
  - outcome proportions: INV-074;
  - evaluation dates: INV-058;
  - review window: INV-051;
  - perimenstrual window and complete cycles: INV-087.

### Section 8 (category G)

ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded, and the passages they cite read as described:
- ISS-01: pp. 124–125;
- ISS-02: pp. 12, 105, 123 and 139;
- ISS-03: the Stage 1 Statements and Rationales, and p. 190;
- ISS-05 and ISS-08: [S-010] p. 6;
- ISS-06: [S-014] and [S-008];
- ISS-09: p. 122;
- ISS-10: NICE 1.3.9 and 1.3.39, and [S-034] p. 52;
- ISS-11: the CG150 Overview and 1.3.48;
- ISS-12: pp. 42 and 209, and the OUT-031 Statement, Evidence note and Caveat as quoted.

I found no Stage 1 issue that the model works around without recording it.

## Remarks

### R22b-01 Formal defect: for 28-day periods, `fillsPeriod` admits a shorter, offset series, while E-006, INV-104 and INV-105 state that it gives all whole periods of the covered period
- Item(s):
  - E-006 (`fillsPeriod`, Meaning, Notes);
  - INV-104 (Reading, Notes) and INV-105 (Reading, Notes);
  - INV-050 Notes; E-067 Notes;
  - section 7 rows OUT-034 and OUT-035.
- Problem:
  - **What the predicate admits.** `fillsPeriod(sr, p)` requires only that no whole period of the series' granularity fits in p before the first or after the last period of the series.
    - Calendar months and calendar weeks lie on a fixed grid, so for them the series is the set of whole months or weeks within p.
    - 28-day periods have no grid. A 28-day series may therefore leave up to 27 days uncovered at each end. So it may be offset within p and hold one period fewer than fit.
  - **When this happens.** By script (`fills.py`), it happens for every covered length of at least 56 days except those of 27 mod 28. This includes every exact multiple of 28.
  - **What the model states.** The model says the opposite in its definition text and in the Readings and Notes of the two invariants that use the predicate for unanchored series:
    - INV-104, clinician-facing summary, SHOULD;
    - INV-105, patient-facing overview, SHOULD.
  - **Consequence.** These invariants admit outputs that their Readings exclude.
    - The covered periods include the selected time range: INV-094 and INV-095 require a summary and an overview of it (`sameSpan(v.covers, c.timeRange)`).
    - INV-001 tiles the selected time range with whole periods of the selected granularity from its first day.
    - For a selected time range of 28-day periods, the summary's time course and its medication-overuse indicators (INV-104) may be shown for periods that are not the selected periods, and for one fewer of them.
  - **Not affected.** INV-050 (withdrawal follow-up) is not affected, because it also ties the first period to the start of withdrawal.
- Evidence:
  - **The predicate.**
    - E-006: `pred fillsPeriod(sr : Series, p : Period) ≙ within(first(sr.periods), p) ∧ within(last(sr.periods), p) ∧ ¬ ∃ d₁, d₂ : Date • p.start ≤ d₁ ∧ d₁ ≤ d₂ ∧ d₂ ≤ p.end ∧ ofKind(d₁, d₂, sr.granularity) ∧ (d₂ < first(sr.periods).start ∨ last(sr.periods).end < d₁)`.
    - E-005: `ofKind` for `fourWeekPeriod` is `days(d₁, d₂) = 28`, with no anchor.
  - **What the model claims.**
    - E-006 Meaning: "`fillsPeriod(sr, p)` holds when the series lies within the period p and leaves no whole period of its granularity within p before its first or after its last period, so that it consists of the whole periods of its granularity within p."
    - E-006 Notes: "the series of the clinician-facing summary, of the patient-facing overview and of the withdrawal follow-up view consists of all whole periods of its granularity within the period the view covers."
    - INV-104 Reading: "for every period of a series that consists of all whole periods of its granularity within the covered period".
    - INV-104 Notes: "it consists of all whole periods of its granularity within it (`fillsPeriod`, E-006), so it spans the covered period up to fewer days than one period at either end, and it cannot shrink to a single period of a longer covered period."
    - INV-105 Notes: "it spans it up to fewer days than one period at either end, and it cannot shrink to a single period of a longer covered period. Where the covered period is a run of whole periods, a series of their granularity spans it exactly."
    - The INV-105 Reading, the E-067 Notes ("over all whole periods within it") and rows OUT-034 ("over all whole periods within the covered period") and OUT-035 ("for every period of a series of all whole periods of its granularity within it") repeat this.
  - **Counterexamples** (checked by script against the predicate as written):
    - **(A) An exact run of 28-day periods.**
      - Context: granularity `fourWeekPeriod`, selected time range 5 January – 29 March 2026. That is 84 days, the three 28-day periods 5 Jan–1 Feb, 2 Feb–1 Mar and 2 Mar–29 Mar (INV-001).
      - The series 19 Jan–15 Feb, 16 Feb–15 Mar satisfies `fillsPeriod`:
        - no 28-day span within the covered period ends before 19 January (the earliest ends on 1 February);
        - none begins after 15 March and ends by 29 March (the earliest such ends on 12 April).
      - So the clinician-facing summary of this time range (INV-094) meets INV-104 with a time course and medication-overuse indicators for two offset periods. None of the three selected periods is in its time course.
      - The overview of the same time range (INV-095, INV-105) is in the same position. Yet INV-105 states that such a series "spans it exactly".
    - **(B) One period of a longer covered period.**
      - Covered period 1 March – 9 May 2026 (70 days; for example the period since a consultation on 1 March).
      - The single period 22 Mar–18 Apr satisfies `fillsPeriod`, although two whole 28-day periods fit (1–28 Mar and 29 Mar–25 Apr).
      - This contradicts "cannot shrink to a single period of a longer covered period".
    - **(C) A six-month summary.** For 1 January – 1 July 2026 (182 days), five periods from 28 January to 16 June are admitted, where six fit.
  - **Why this is new evidence, not a settled point.**
    - R03-04 (review 03) required "(i) Require the series to consist of all whole periods of its granularity within the covered period".
    - Fix 03 adopted the review's formula and verified it only by construction: "consecutive 28-day periods from the first covered day fill any period of at least 28 days" (fix-iter-03.md, R03-04; "checked on a six-month summary (calendar months or six 28-day periods with a 13-day remainder)").
    - Fix 05 (R05-01) replaced INV-105's exact tiling of v00–v04 by `containsPeriodOf` and `fillsPeriod` and verified it the same way. Its Notes claim that a run of whole periods is still spanned exactly.
    - Review 06 states "`fillsPeriod` still excludes a one-period series of a long covered period (the R03-04 guarantee)", and review 05 says the same.
    - No loop file examined an offset 28-day series.
    - Review 06 accepted, for `mostRecent` (INV-041), that "Stage 1 fixes no grid for 28-day periods". That argument does not dispose of this defect, for two reasons:
      - here the model's own text claims exactness and maximality;
      - the selected time range does have a grid, the one INV-001 gives it.
  - **Stage 1 context.**
    - OUT-034 brings together "frequency measures and their time course (OUT-004 to OUT-009)" and "any medication-overuse indicator (OUT-014 to OUT-016)" for the period the summary covers.
    - OUT-004 asks for values "for every period in the selected time range".
- Required change. Either option removes the contradiction:
  - **(a) Make the predicate do what the text says** (preferred, as it completes R03-04 (i)). In E-006, add to `fillsPeriod` a conjunct for 28-day series. Two forms are possible:
    - **(a1) An anchor.** `sr.granularity = fourWeekPeriod ⇒ first(sr.periods).start = p.start`.
      - This is the construction that the satisfiability arguments of fix 03, fix 05 and the INV-104 and INV-105 Notes already use, and that INV-050 already imposes through its start tie.
      - With it, a 28-day series consists of the consecutive 28-day periods from the first day of the covered period up to fewer than 28 days before its end. A covered period that is a run of 28-day periods, such as the selected time range, is spanned exactly.
    - **(a2) A maximality condition.** For example `sr.granularity = fourWeekPeriod ⇒ p.lengthDays < 28 × (#sr.periods + 1)`.
      - It gives the most periods that fit and spans a run of 28-day periods exactly.
      - It still lets the series be offset when the covered period is not a multiple of 28 days. The text would then have to say so.

    Calendar months, calendar weeks and INV-050 are unchanged in effect, and satisfiability is unchanged. Check the INV-104 and INV-105 satisfiability Notes and rows OUT-034 and OUT-035 against the new conjunct.
  - **(b) Keep the predicate and correct the text.** State what `fillsPeriod` guarantees for 28-day series: fewer than 28 days uncovered at each end, so the series may be offset and hold one period fewer than fit, also for a run of whole 28-day periods. Remove "consists of all whole periods", "cannot shrink to a single period of a longer covered period" and "spans it exactly" for 28-day series from these places:
    - E-006 Meaning and Notes;
    - INV-104 Reading and Notes;
    - INV-105 Reading and Notes;
    - the E-067 Notes;
    - the reference "as INV-104 and INV-105 do" in the INV-050 Notes;
    - rows OUT-034 and OUT-035.
  - **Oscillation.** Neither option reverses an earlier fix.
    - Watch point 4 of the iteration-08 check, repeated after iteration 12, names re-adding the exact end tie and loosening `fillsPeriod` or the start tie as oscillation.
    - Option (a) tightens `fillsPeriod` in the direction of R03-04 (i) and of INV-105's v00–v04 tiling, and adds no exact end tie: the series may still end up to 27 days before the covered period ends.
    - Option (b) changes no predicate.
    - The INV-105 watch points of the iteration-16 check (the treatment-effect conjunct) are untouched.

## Checked and not raised

- **The v21 changes.** ISS-12, the E-063 Meaning and the Notes of E-062, E-063 and INV-089 are consistent with the unchanged INV-089. The six new [S-001] quotes are verbatim on pp. 42 and 209, and the Stage 1 OUT-031 passages that ISS-12 cites are quoted correctly.
- **`mostRecent` (INV-041) with 28-day periods.** It admits a triple that ends up to 27 days before the as-of date. Review 06 settled this ("Stage 1 fixes no grid for 28-day periods"), and the three-month view is not tied to the selected time range. No new evidence. Not raised. Unlike R22b-01, no text of the model claims more than the predicate gives there, beyond "most recent" itself.
- **`fillsPeriod` for calendar months and weeks.** These have a grid, so the predicate gives exactly the whole months or weeks within the covered period. No defect.
- **𝔹-valued given functions used as formulas** (`isMonthSpan`, `isWeekSpan`, `_⊑_`, `showsValueNamed`, `publishedGrading`, `banded`). Section 2.6 admits "application of a defined or given predicate", and section 2.3 has no separate "given predicate" form. Reading `f(x)` as `f(x) = true` is the only possible meaning, so the semantics are not ambiguous. Not raised.
- **24-hour outcomes in cluster-headache summaries** (INV-072 with `fifteenMinutes`). The model follows Stage 1 OUT-023, which replaces only "the corresponding time point". Review 01 settled this; no work-around and no new evidence.
- **MIDAS Grade IVA/IVB** (INV-082 admits the four tabulated bands only). Settled by review 12 (shown as `OtherItem`). No new evidence.
- **No relation between the three functional-impact domains and `anyActivity`, or between a distribution and a mean peak intensity.**
  - The first is an optional bound, like `treatedAttacks ≤ AttackCount`, which review 05 did not raise.
  - For the second, Stage 1 does not fix whether "an average peak intensity" is over days or attacks, so no relation is part of the output data.
- **The INV-055 Notes example of a course stopped on 30 March.** It names the NICE 1.3.28 and Turkish Box 8 time points but not AAN/AHS 14A. Whether 14A applies depends on a `targetDoseReached` event that the example does not state. For the same antibody stopped on 10 February, the v18 change log counts six time points, which do not include 14A; under that typing the text is correct. The example is illustrative. Not raised.
- **Quoted paraphrases in sections 1 and 3** ("where results are available", "the subject has migraine"). These present Stage 1 conditions in shortened form; no source quote is altered. Style. Not raised.
- **The main review's "not raised" items.** I re-examined each and agree:
  - empty `remissions` in chronic cluster headache;
  - the history of previous bouts;
  - the cluster-view references;
  - the MUST cycle-line attributes in the overview;
  - INV-031;
  - OUT-019 "migraine or headache days";
  - periods after the as-of date;
  - the S-102 diacritic and the S-105 heading case.
- **Settled points, not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the "> 3 months" readings (INV-045, INV-089);
  - ISS-01's basis of the 8.2.6 indicator;
  - the HIT-6 one-month recall; HADS subscales only; the MIDAS labels;
  - "baseline administration" as any earlier administration;
  - INV-023 at any granularity;
  - INV-027 tied to preventive treatments;
  - INV-060 with INV-061 for compared periods shorter than 28 days;
  - the E-041 rule list, `excludes` values and criterion (watch point 5);
  - "one item suffices" and the other ties of INV-105's treatment effect (watch point 1);
  - INV-098 read on period starts (watch point 6);
  - the history-wide `acuteMedications` (watch point 2).
- **Oscillation watch points.** R22b-01 concerns `fillsPeriod`. Under iteration-08 watch point 4, only loosening it or the start tie, or re-adding the exact end tie, would be a reversal. Neither option of R22b-01 does any of these (see the remark).

## Notes on frozen items (for the human)

None. `FROZEN_ITEMS.md` does not exist, and no item of v21 carries a FROZEN marker.
