# Review — iteration 25
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v24
Date: 2026-10-22

## Summary

This is the main review of iteration 25, by a new, independent reviewer. I checked v24 against its sources and against Stage 1 v18 myself. I read the earlier loop files only so that I would not reopen settled points or reverse earlier fixes.

**State of the files.**
- The working tree was clean at HEAD 9340190 ("Stage 2 / iter 24: oscillation check (none)").
- `OUTPUT_MODEL.md` is byte-identical to `history/v24.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18: sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5.
- v24, every section: notation, conformance, all 67 elements and 111 invariants, the traceability table, section 8, sources, the search log and the v24 change-log entry.
- Review 24, fix 24, and the oscillation check after iteration 24 with its findings, settled points and watch points.

**Result.** I found nothing that requires a change.
- **Citations.** Every quote in the model is verbatim at its URL and on its stated page or section. I checked 874 quoted fragments; none is a misquote. The six Stage 2 sources (S-101 to S-106) have correct metadata. Translations are faithful. I found no newer version of a source that changes an element: there is still no published ICHD-4, only "Work in Progress" papers.
- **Values.** Every value set, range, band, code label, reference level, offset, threshold, criterion and control level matches its source.
- **Stage 1 fidelity.** All 39 requirements are fully represented at the right levels.
- **Scope.** The sweep finds no input, storage or input-derivation content. Every threshold, formula and computed field that is part of the output data is present and cited.
- **Formal checks.** All mechanical checks pass.
- **The v24 change** (by-dates relations, `sameIndicatedPeriod`, INV-111):
  - it is well typed and guarded;
  - every property that its prose claims holds (checked by script);
  - it still admits correct outputs that have several period atoms with the same dates, including a calendar month and a 28-day period with the same dates.

## Verification coverage

### Downloads and tools

**Where.** All sources were downloaded fresh with `curl` through the proxy into a new directory, `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r25/dl`, outside the repository. Scripts are in `…/r25/scripts` and were run with `python3 -I`: `extract.py`, `match.py`, `pages.py`, `mech.py`, `names.py`, `claims.py` and `instance.py`.

**Extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML pages and Europe PMC full-text XML were stripped of markup.

**HTTP status.** Every download returned HTTP 200, with one exception. The PubMed web page of [S-010] (Stage 1 abstract URL) returned HTTP 203 with a cookie check. The [S-010] quotes in the model come from the full-text PDF (Stage 1 URL, HTTP 200), and the abstract was read through PubMed E-utilities.

**Sources downloaded:**
- [S-001] (211 pp.), [S-002], [S-003], [S-005], [S-006], [S-007] (39 pp.), [S-008] (31 pp.), [S-009], [S-010] (11 pp.), [S-016] (64 pp.), [S-018] (12 pp.), [S-020], [S-030] (86 pp.), [S-033] (92 pp.), [S-034] (53 pp.), [S-035] (92 pp.) and [S-105] (9 pp.);
- Europe PMC full texts: [S-004], [S-011], [S-012], [S-013], [S-014], [S-023], [S-042], [S-043], [S-101], [S-102] and [S-104], plus PMC8684566 and PMC6537129, for the MIDAS label variants that the search log names;
- web pages:
  - [S-015]: the Recommendations and Overview pages;
  - [S-028] and [S-029];
  - [S-032];
  - [S-103];
  - [S-106]: the overview and chapters 1, 2 and 8.

**Rendered and read** (no usable text layer):
- [S-001] p. 190: the A1.1.1 and A1.1.2 windows "day 1 ± 2 (i.e. days −2 to +3)" and note 2;
- [S-034] p. 1, an image: "Возрастная группа" … "дети".

**Metadata.**
- PubMed esummary confirms the authors, journal, year, volume, issue, pages, DOI and PMCID of S-101 (PMID 20819842), S-102 (25902814), S-104 (12914662) and the S-103 developer paper (11739822).
- [S-105] PDF metadata: author Kurt Kroenke, created 2010, modified 2014.
- [S-106] overview: "Published: 27 June 2012" and "Last reviewed: 11 January 2016".
- [S-015] overview: "Last updated: 03 June 2025" and "Last reviewed: 23 September 2026".
- [S-103] footer: "© 2026".

### Quote check (`match.py`, `pages.py`)

**Method.**
1. For every line outside the `omn` blocks, the script takes each quoted string. It attributes the string to the nearest preceding `[S-NNN]` tag on the line and splits it at "[...]".
2. It normalises each fragment of at least 6 letters or digits (NFKC, soft hyphens removed, case folded, letters and digits only).
3. It searches the tagged source page by page, then all other downloaded texts, then Stage 1 v18.
4. `pages.py` compares the page on which each fragment was found with the "p." or "PDF p." given after the quote. Offsets: S-016 printed page + 6; S-002 printed page − 1025; S-005 printed page − 802.

**Results.**
- **Pages.** 115 fragments are on their stated page. Six apparent mismatches were script artefacts, each read by hand and found on the stated page:
  - a parenthesis that belongs to a later item: E-041 Evidence, the [S-034] and [S-035] heading fragments;
  - a page number taken from a later sentence of a search-log entry: [S-033] p. 53, [S-007] p. 10, [S-035] PDF pp. 48 and 23.
- **Rows without a fragment found.** The fragments in the "Not source text" column were each read in place. They are:
  - English translations;
  - prose caught between two quotation marks of different quotes;
  - model terms, search queries and row labels;
  - two illustrative paraphrases of Stage 1 wording (Checked and not raised).

Notes on the columns:
- "Verbatim elsewhere": found in another source tagged on the line, or as Stage 1 wording. Lines often cite a source after its quote, so the nearest preceding tag is not always the right one.
- [S-102] includes "little or none" from the search log, which is in PMC8684566 as the log states.

| Source (nearest tag) | Fragments | Verbatim in tagged source | Verbatim elsewhere | Confirmed on rendered page | Not source text | Not found | Unreachable |
|---|---|---|---|---|---|---|---|
| S-001 | 76 | 69 | 2 | 1 | 4 | 0 | 0 |
| S-002 | 6 | 2 | 4 | 0 | 0 | 0 | 0 |
| S-005 | 9 | 2 | 7 | 0 | 0 | 0 | 0 |
| S-007 | 9 | 8 | 1 | 0 | 0 | 0 | 0 |
| S-008 | 27 | 19 | 7 | 0 | 1 | 0 | 0 |
| S-010 | 38 | 31 | 4 | 0 | 3 | 0 | 0 |
| S-011 | 9 | 7 | 2 | 0 | 0 | 0 | 0 |
| S-012 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| S-013 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| S-014 | 37 | 28 | 6 | 0 | 3 | 0 | 0 |
| S-015 | 42 | 35 | 6 | 0 | 1 | 0 | 0 |
| S-016 | 9 | 7 | 2 | 0 | 0 | 0 | 0 |
| S-018 | 13 | 10 | 3 | 0 | 0 | 0 | 0 |
| S-023 | 6 | 4 | 1 | 0 | 1 | 0 | 0 |
| S-028 | 13 | 10 | 2 | 0 | 1 | 0 | 0 |
| S-029 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| S-030 | 4 | 3 | 1 | 0 | 0 | 0 | 0 |
| S-032 | 1 | 0 | 1 | 0 | 0 | 0 | 0 |
| S-033 | 47 | 19 | 10 | 0 | 18 | 0 | 0 |
| S-034 | 17 | 8 | 3 | 2 | 4 | 0 | 0 |
| S-035 | 50 | 33 | 4 | 0 | 13 | 0 | 0 |
| S-042 | 3 | 1 | 2 | 0 | 0 | 0 | 0 |
| S-101 | 4 | 4 | 0 | 0 | 0 | 0 | 0 |
| S-102 | 9 | 6 | 3 | 0 | 0 | 0 | 0 |
| S-103 | 10 | 10 | 0 | 0 | 0 | 0 | 0 |
| S-104 | 3 | 3 | 0 | 0 | 0 | 0 | 0 |
| S-105 | 3 | 3 | 0 | 0 | 0 | 0 | 0 |
| S-106 | 6 | 4 | 0 | 0 | 2 | 0 | 0 |
| No tag on the line (Stage 1 wording, model terms, search queries) | 420 | 0 | 363 | 0 | 57 | 0 | 0 |
| **Total** | **874** | **329** | **434** | **3** | **108** | **0** | **0** |

**Stage 2 sources, read in context:**
- **[S-101] PMC3057423, Methods, "Data sources".** "ranges between 36 and 78, with larger scores reflecting greater impact" and the four categories with their bands are verbatim.
- **[S-102] PMC4406925, "Migraine-related disability".** The four grades with labels and bands, the IVA/IVB option, and "The recall period for the MIDAS is three months" are verbatim.
- **[S-103] "PedMIDAS Grading Scale".** The table rows are verbatim: 0 to 10 Little to none; 11 to 30 Mild; 31 to 50 Moderate; Greater than 50 Severe.
- **[S-104].** "the possible scores ranged from 0 to 21 for anxiety and 0 to 21 for depression" is verbatim.
- **[S-105].** "PHQ-9 total score for the nine items ranges from 0 to 27." and "GAD-7 total score for the seven items ranges from 0 to 21." are on P.6/9; the developers sentence is on P.8/9.
- **[S-106] chapter 2.** "The recommended re-treatment schedule is every 12 weeks (see the summary of product characteristics)." is the last sentence of 2.1.

**Translations read in context and judged faithful:**
- **Russian.**
  - [S-033] p. 39: the comment that follows the recommendation quoted in E-041, with "эффективность БТА – минимум через 6 месяцев терапии";
  - [S-033] pp. 4, 40 and 41;
  - [S-034] pp. 1, 17 and 52.
- **Turkish.**
  - [S-035] PDF p. 48, Kutu 8: "Ölçüt…" is its second item and "Yeterli süre…" its seventh, as stated.
  - [S-035] PDF p. 57: "Hasta fayda görüyorsa…" is two sentences before "Hastalar 3 enjeksiyon siklusu…".
  - [S-035] PDF p. 86, section 7.3: the third, fourth and fifth items, as stated.
  - [S-035] PDF pp. 23, 77, 82 and 83.
- **Dutch.** The [S-028] PICO.

**Source headings and populations read on the page:**
- [S-015]:
  - recommendations 1.3.27 to 1.3.29 stand under "Migraine with or without aura" and "Prophylactic treatment review";
  - 1.3.24 and 1.3.26 say "in adults";
  - 1.3.9, 1.3.39 and 1.3.48 read as quoted;
  - the Overview gives the population "young people (aged 12 years and older) and adults".
- [S-016] p. 7: section 1.2.1.
- [S-018] p. 7: 14B, with the repeated phrase "before assessing efficacy"; p. 8: 14H.
- [S-008] p. 9: Q2 Optimal and Essential.

### Values

All of the following match their sources:
- **ICHD-3 code labels** of E-009, character for character, including "(TTH)" and "(MOH)": classification list, pp. 8, 9 and 12.
- **ICHD-3 8.2 reference levels**: 15 days for non-opioid analgesics, 10 for the other classes and for combined use; the span of "more than three months".
- **ICHD-3 classes**: `classesOf826` is criterion B of 8.2.6; 8.2.6 note 2 excludes 8.2.1–8.2.5.
- **A1.1 window**: `plusDays(d1, −2)` to `plusDays(d1, 2)`, with no day 0; this is days −2 to +3.
- **Remission duration**: "must exceed three months".
- **Instrument value sets**:
  - HIT-6: range 36–78; bands 36–49, 50–55, 56–59 and 60–78, with the source labels;
  - MIDAS: grades I–IV, with the [S-102] labels and bands;
  - PedMIDAS: four grades, the last with a strict lower bound of 50;
  - HALT-90: Table 18, including the overlap at 20;
  - HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21;
  - recall periods: 3 months for MIDAS, PedMIDAS and HALT-90; 1 month for HIT-6 and HALT-30.
- **The 18 evaluation rules**: for each, the offset, anchor, timing, ages and `excludes` were read against its quote.
- **The six named criteria**: their thresholds and conditions, including the IHS Q6 MIDAS baseline ranges and the HIT-6 5 points.
- **The four control levels of [S-010]**.

### Fidelity to Stage 1, requirement by requirement

For each OUT requirement I compared every observable property of the Statement, and every Caveat that constrains the output, with the elements and invariants that realise it. I also compared the level of each part with its Stage 1 strength.

| OUT | Parts and strength | Realised by | Result |
|---|---|---|---|
| 001 | MUST: period with start, end and length; monthly or 28-day; equal-length comparison. Caveat: days per month visible | E-003, E-005, INV-002, INV-003, INV-014, INV-015, INV-108, INV-037, INV-038 | ok |
| 002 | SHOULD: state the definition each measure follows | E-011, INV-008, INV-111 | ok (v24 checked) |
| 003 | SHOULD: indicator next to the measures. SHOULD NOT: cut-off presented as validated | E-013, INV-011 to INV-013 | ok (v24 INV-012 checked) |
| 004 | MUST: every period of the time range; ICHD-3 definition | INV-014, INV-009, INV-006 | ok |
| 005 | MUST for migraine; SHOULD: label | INV-015, INV-008 | ok |
| 006 / 007 | SHOULD; MUST per month or 28 days where provided; separate attack count | INV-016, INV-017, INV-108, INV-010, E-019 | ok |
| 008 | MAY | E-020 to E-022, INV-031 | ok |
| 009 | SHOULD: series, markers, weekly where relevant | INV-034 to INV-036, INV-001 | ok |
| 010 | SHOULD: per period, stated scale, comparison | INV-018, INV-039, INV-032 | ok |
| 011 | SHOULD: summary and label. Caveat as SHOULD NOT | INV-019 to INV-021 | ok |
| 012 | SHOULD: across periods and per treated attack | INV-022, INV-072, INV-076 | ok |
| 013 | MAY | E-027 | ok |
| 014 | MUST: total, class and drug per period, together | INV-023, INV-024 | ok |
| 015 | SHOULD: per calendar week | INV-025 | ok |
| 016 | MUST: per period, per class and combined; MUST: prompt. MUST NOT: diagnosis | E-032, INV-044 to INV-048 | ok (v24 `sameIndicatedPeriod` checked) |
| 017 | SHOULD: from the start of withdrawal; 4–8-week window; following year; worsening label | E-039, INV-049 to INV-052 | ok |
| 018 | MUST: comparison, values, absolute and percentage change, time points. Caveat: no decision (MUST NOT) | E-040 to E-043, INV-053 to INV-059, INV-106 | ok |
| 019 | SHOULD: residual burden next to a percentage change | INV-060, INV-061 | ok |
| 020 | SHOULD: criterion, values, other values. SHOULD NOT: sole indicator | E-045, E-046, INV-062 to INV-065 | ok (v24 E-046 checked) |
| 021 | MUST: three components for the same periods. SHOULD: the others where provided | INV-068, INV-069, INV-102 | ok |
| 022 | SHOULD: after a stop, pause or reduction, against the on-treatment period and the baseline | INV-070, INV-103 | ok |
| 023 | SHOULD: all outcomes, consistency, timing, formulation, phases, 15 min. Caveat as SHOULD NOT | E-050 to E-053, INV-071 to INV-075, INV-107 | ok |
| 024 | SHOULD: chronological, grouped by class, every detail, acute formulation | E-054, E-055, INV-077 to INV-079, INV-109 | ok |
| 025 | MAY | E-056, INV-080 | ok |
| 039 | SHOULD: next to the comparison, in the history, in the clinician summary | E-047, INV-066, INV-067, INV-104, INV-109 | ok |
| 026 | SHOULD: name, date, recall, total score, grading, change | E-057, E-058, INV-081, INV-082 | ok |
| 027 | SHOULD: three domains, severe impairment, comparison with the baseline | INV-026, INV-027, INV-033 | ok |
| 028 | MUST: three-month view. SHOULD: definitions. SHOULD NOT: diagnosis | INV-040 to INV-043 | ok |
| 029 | MUST: frequency and medication per type and combined. SHOULD: intensity per type | INV-028 to INV-030 | ok |
| 030 | MUST: cycles, the A1.1 window, the number of complete cycles | E-060, E-061, INV-086, INV-087 | ok |
| 031 | SHOULD: bouts and remissions, rates, 15 min, previous bouts | E-062 to E-064, INV-088, INV-089 | ok |
| 032 | MAY; caveats SHOULD | E-065, INV-090, INV-110 | ok |
| 033 | SHOULD: name, date and score next to headache outputs; SHOULD NOT: diagnoses | E-059, INV-083 to INV-085 | ok |
| 034 / 035 | SHOULD | E-066, E-067, INV-094, INV-095, INV-104, INV-105 | ok |
| 036 | SHOULD: (a) to (d) and the Caveat | INV-055, INV-096 to INV-098 | ok |
| 037 | SHOULD NOT and SHOULD as stated | INV-091 to INV-093 | ok |
| 038 | SHOULD; SHOULD NOT as the negative form | INV-099 to INV-101 | ok |

### Mechanical checks (scripts)

| Check | Result |
|---|---|
| IDs (`mech.py`) | <ul><li>67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111): none missing, none duplicated.</li><li>Issues ISS-01 to ISS-12 without ISS-07, which section 9 lists as withdrawn.</li><li>No dangling E-, INV- or ISS- reference.</li><li>Every OUT ID named exists in Stage 1.</li><li>36 source IDs cited, all within S-001 to S-046 or S-101 to S-106.</li></ul> |
| Fields | <ul><li>Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field.</li><li>Every invariant has exactly one Predicate, Reading, Conformance, Realises and Evidence field.</li><li>No item has two Notes fields.</li><li>Every invariant states its scope: output 78, repertoire 32, context 1.</li></ul> |
| Traceability | <ul><li>39 rows in Stage 1 order (OUT-039 after OUT-025), all "full".</li><li>For every row, the Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches.</li><li>INV-111 is in row OUT-002.</li></ul> |
| Invariant levels | <ul><li>MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34.</li><li>Every MUST NOT and SHOULD NOT predicate has the form `¬ F`.</li></ul> |
| Attribute levels | <ul><li>172 level-annotated attributes: core 94, MUST 29, SHOULD 47, MAY 2.</li><li>The typing rule of section 2.5 holds for all of them.</li></ul> |
| Names (`names.py`, string literals removed) | <ul><li>557 declarations, none declared twice.</li><li>Every identifier in the `omn` blocks is declared, a primitive, a keyword or a bound variable.</li><li>Every attribute selection `.a` names one of the 189 declared attributes.</li></ul> |
| v24 typing and definedness (by hand) | <ul><li>`sameSpan : Period × DateSpan` and `spanOf` (guarded by INV-002) in `daysOf`, INV-006, INV-012, INV-030, INV-031, INV-033, INV-053, INV-089, E-046 and `sameIndicatedPeriod`.</li><li>`viewOf` is total on items: `sameIndicatedPeriod` and INV-111 conjunct (2).</li><li>`÷` in INV-012 divides by `lengthDays : ℕ₁`.</li><li>`j ∈ dom i₂.basis` guards `i₂.basis(j)`.</li></ul> |
| Prose claims (`claims.py`) | <ul><li>**INV-012 Notes**, "indicators that agree pairwise rest on one number": no counter-example among 14,027 random sets of indicators that agree pairwise. The proportions were shown at 0–2 decimals; each set had 2–5 indicators, of periods of 1–92 days.</li><li>**INV-045 and the E-032 Notes**: the shortest span lasting more than three months always has four periods (every calendar month 2020–2030 and 4,000 end dates of 28-day periods), and its dates are fixed by the indicated period's dates and kind. February 2026 as a calendar month has the span 1 November – 28 February; 1–28 February as a 28-day period has 9 November – 28 February. They differ, as the E-032 Notes say.</li><li>**Worked dates**, all correct: E-042 and INV-055 (1 April; 26 March; 26 February – 25 March; interval ends 28 February and 31 March; 4–31 December = 28 days); INV-049 (day 43; window 7 April – 5 May; 6 April); E-007 (67 days); E-063 (42 and 143 days); INV-105 (43 days).</li></ul> |
| Correct outputs still admitted (`instance.py`) | <ul><li>One view, built from one set of underlying days, shows: a calendar-month series November 2025 – February 2026; a response comparison with its own December and February atoms; the 28-day period 1–28 February 2026; triptan, NSAID and combined-use overuse indicators for February on three atoms (series month, comparison month, 28-day period); February completeness stated as days, as a proportion at 1 decimal and at 0 decimals.</li><li>INV-006, INV-024, INV-031, the INV-045 span shape, the INV-046 agreement of combined indicators, the agreement of class indicators with `sameIndicatedPeriod`, INV-012 and INV-053 all hold.</li><li>The two February spans are not compared, because their kinds differ.</li></ul> |
| Scope sweep | <ul><li>I searched for record, enter, entry, input, captur*, stor*, database, seriali[sz]*, JSON, XML, CSV, FHIR, encod*, retention, persist*, reminder, data field, data-entry, logged and answer(s).</li><li>The only hits are: the section 1 exclusions and the section 2.1 disclaimer; the [S-014] HALT-30 sentence "accordingly records days affected" (an instrument's recall, settled since review 01); the E-057 Notes that leave scoring from answers out of scope; INV-076's statement that it avoids a derivation.</li><li>Every relation that v24 changed or added takes output elements only: counts, periods and their dates, indicators, labels, rates and changes.</li><li>Every threshold and formula that is part of the output data is present and cited.</li></ul> |
| Section 8 | <ul><li>Each of ISS-01 to ISS-06 and ISS-08 to ISS-12 is founded, and its quotes are verbatim on the stated pages.</li><li>ISS-02: a page-by-page search of [S-001] finds "simple analgesic" only on p. 139, as stated; the p. 105 "ibuprofen or other NSAIDS" is as quoted.</li><li>ISS-03: by script, the Statements of OUT-008, OUT-018, OUT-019, OUT-022, OUT-028, OUT-030 and OUT-035 name migraine days without "patients with migraine"; OUT-021 cites OUT-005, and OUT-009 and OUT-034 cite ranges that include it.</li><li>ISS-12: the Stage 1 OUT-031 Caveat and Evidence sentences it cites read as described.</li><li>No Stage 1 issue is worked around silently.</li></ul> |

## Remarks

None.

## Checked and not raised

- **Agreement of counts across the views of one output.**
  - Within one view, v24 makes counts of the same measure, scope and dates agree. Across the views of one output it does not. So one output may show March 2026 headache days as 5 in one view and 7 in another.
  - The INV-006 Notes give per-view definitions as the reason. That reason fits migraine days and moderate/severe headache days. It does not fit headache days, which follow ICHD-3 in every view (E-015, INV-009), or acute-medication days.
  - I did not raise it, for three reasons:
    1. R24-01 required the agreement "at least within one view as their Readings state" and left output-wide agreement to the fixer, who declined it with a reason.
    2. The Readings of the relations say "in one view", so no text claims more than its predicate.
    3. No Stage 1 statement part is unrepresented: each count is defined as the number of days of its period with the property (E-014).
  - Watch point 1 of the oscillation check calls this a new decision, not a defect. It is noted here for the human.
- **INV-111 excludes one view that shows migraine days under two definitions, each with its label.**
  - This follows from option (a) of R24-02, which fix 24 implemented. Watch point 2 says that re-raising per-value definitions needs new evidence.
  - Stage 1 OUT-002 asks only that the definition used be visible; it does not ask for two definitions in one view. Values under a second definition can be shown in another view, or as an `OtherItem` (section 3.7).
  - No new evidence. Not raised.
- **INV-008 Notes, "Satisfiable in every view".** For a view whose changes refer to migraine-day values shown in two other views with different definitions, INV-008 and INV-111 cannot both hold. But no invariant requires such a view: the changes of a response comparison, residual burdens and migraine indices have their values in their own view (INV-054, INV-060, INV-092). The INV-111 Notes state this. It does not affect the satisfiability of the repertoire. Not raised.
- **A side effect of the new INV-012 conjunct.** With `cj = ci`, a lone proportion must be a rounding of the covered days, a whole number, divided by the length (for example, "50 %" is impossible for a 31-day period). This is correct under the definition of `proportionCovered` and section 2.7. The INV-012 satisfiability statement remains true.
- **The rows of OUT-014 and OUT-016 cite INV-006 in their coverage reason**, while INV-006's Realises names only OUT-004 and OUT-007. The columns follow the Realises fields, as the table header states (0 mismatches), and the coverage of both rows is full through INV-023, INV-024 and INV-044 to INV-046. A bookkeeping matter, not a coverage gap.
- **[S-106] metadata.** Chapter 8 of TA260 records "June 2025: … minor editorial changes to the wording in section 1.1". This affects neither chapter 2, which the model quotes, nor the re-treatment schedule. The citation gives the dates that the overview page shows.
- **Two paraphrases of Stage 1 wording in quotation marks:**
  - section 3.3 item 6, "supports but does not replace clinical assessment and diagnosis" (OUT-038 reads "support");
  - section 1, "where results are available".
  These are illustrative wordings in the conformance text, not cited quotes. INV-101 and INV-081 cite the Stage 1 wording exactly. Not a citation defect.
- **MIDAS labels.** [S-101] itself uses "minimal or infrequent disability". The E-057 Notes already state that labels differ between publications of the developers, and that the model uses those of [S-102] with the same bands. Settled.
- **HALT-90 total and question 5.** Read again in [S-014] "Scoring HALT"; review 24 settled it. Not reopened.
- **The search log has no entry for iteration 23.** Fix 23 made no search, so this is not a remark category.
- **Settled points, not reopened (no new evidence):**
  - INV-106 at MUST NOT; the "> 3 months" readings of INV-045 and INV-089; INV-023 at any granularity; INV-027 tied to preventive treatments;
  - the E-041 window readings, timings, ages and `excludes`;
  - "one item suffices" and the ties of INV-105; INV-098 read on period starts; the history-wide `acuteMedications`;
  - the HIT-6 one-month recall; HADS subscales only; MIDAS Grade IV undivided; "baseline administration";
  - INV-060 with INV-061 for periods shorter than 28 days;
  - `mostRecent` with 28-day periods; empty `remissions` in chronic cluster headache (ISS-12); the 24-hour outcomes of 15-minute summaries;
  - E-039 `reviewWindow`; the CycleLine lead-in;
  - the INV-031 marks conjunct;
  - comparison periods beyond the as-of date.
- **Oscillation watch points.**
  - Nothing above returns a v24 relation to atom identity.
  - Nothing changes INV-008's predicate, the cluster view, the day convention, `fillsPeriod`, the formulation ties or the text-only entries.
  - No remark is raised, so nothing reverses an earlier fix.

## Notes on frozen items (for the human)

None. No item is frozen.
