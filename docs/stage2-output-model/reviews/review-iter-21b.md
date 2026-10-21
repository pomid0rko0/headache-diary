# Review — iteration 21 (re-check b)
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v20
Date: 2026-10-21

## Summary

This is the first independent re-check of iteration 21. The main review (review-iter-21.md) found no remarks on v20. I verified the sources, the Stage 1 text and the model myself, and reached my own verdict.

**State of the files.**
- The working tree was clean at HEAD 25c1da4. `OUTPUT_MODEL.md` is byte-identical to `history/v20.md`.
- `FROZEN_ITEMS.md` does not exist, and no item of v20 carries a FROZEN marker.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5;
- v20, all sections: every element, every invariant, the traceability table, section 8, the sources, the search log and the change log;
- review 21, review 20, re-checks 19b and 19c, and fix 20;
- the oscillation check after iteration 16, with its watch points and its list of settled points.

I searched the other reviews and fixes for settled and declined points. No earlier fixer declined a remark on the topic I raise.

**My own work.**
- Downloads: all with `curl` through the proxy, into a fresh directory outside the repository (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r21b/dl`).
- Text, page by page: `pdftotext -raw` and `-layout`, and markup removed from HTML and XML (`…/r21b/txt`).
- Scripts, run with `python3 -I`: `match.py`, `onpage.py`, `mech.py` and `decl.py` (`…/r21b/scripts`).
- Rendered and read: ICHD-3 pp. 42 and 190, and the image-only title page of [S-034].

**Result.**
- **Citations.** Every quote is verbatim at its URL and stated location, and every translation is faithful. The metadata of S-101 to S-106 is correct, and no newer version of a source changes an element.
- **Values.** All values, codes, labels, ranges, thresholds and offsets are correct against their sources.
- **Mechanical and fidelity checks.** The mechanical checks pass. Every OUT requirement is represented at its Stage 1 strength, and the scope sweep finds nothing.
- **One remark (R21b-01).** It concerns the cluster remission period.
  - OUT-031 asks for cluster remission periods "using the ICHD-3 definitions".
  - ICHD-3 itself words the duration of a remission in three different ways:
    - "must exceed three months" (Definitions of terms);
    - "≥3 months" (3.1.1 Episodic cluster headache);
    - "remissions lasting <3 months" (3.1.2 Chronic cluster headache).
  - The model follows the Definitions-of-terms wording as a definitional invariant (INV-089). As a result, the remissions that ICHD-3 describes for chronic cluster headache can never be shown as remission periods.
  - Neither E-063 nor section 8 records this choice or the conflict. E-063 also states that a remission item is "an attack-free period that ICHD-3 considers a remission".
  - The required change is text only: a new section 8 entry, pointers to it, and a corrected E-063 Meaning.

## Verification coverage

### Downloads

All 32 downloads returned HTTP 200.

**PDFs** (extracted page by page):
- [S-001] ICHD-3, 211 pp.; [S-002], 19 pp.; [S-005], 14 pp.; [S-007] UCL accepted manuscript, 39 pp.;
- [S-008], 31 pp.; [S-010], 11 pp.; [S-016] SIGN 155, 64 pp.; [S-018] AAN/AHS Clinician Summary, 12 pp.;
- [S-030], 86 pp.; [S-033], 92 pp.; [S-034], 53 pp.; [S-035], 92 pp. (PDF created 28 August 2025); [S-105], 9 pp.

**Web pages:**
- [S-015]: the CG150 Recommendations page ("Last updated: 03 June 2025") and the Overview page;
- [S-028]: the NVN module;
- [S-103]: the Cincinnati Children's PedMIDAS page (footer "© 2026");
- [S-106]: TA260, the Overview page, chapter 1 and chapter 2.

**Europe PMC full-text XML:**
- [S-004] PMC6501455, [S-011] PMC9188162, [S-012] PMC9555163, [S-013] PMC7296705, [S-014] PMC6734476, [S-023] PMC9607711;
- [S-101] PMC3057423, [S-102] PMC4406925, [S-104] PMC183845;
- PMC8684566 and PMC6537129, the MIDAS label variants named in the search log.

### Quotes per source

**Method of `match.py`.**
1. For every line outside the `omn` blocks that carries an `[S-NNN]` tag, it pairs the double quotes in sequence and attributes each quoted string to the nearest preceding tag.
2. It splits each string at "[...]" and keeps fragments with at least 6 letters or digits.
3. It searches each fragment, after normalisation (NFKC, soft hyphens removed, case folded, letters and digits only), in this order:
   - the tagged source, page by page;
   - the other sources tagged on the line;
   - the Stage 1 v18 text.

**Method of `onpage.py`.** It checked 86 Stage 2 quotes separately on their stated page, and all 86 were found there:
- [S-001] pp. 8, 9, 12, 105, 122–125, 139, 190, 209;
- [S-008] pp. 9, 12, 13, 17;
- [S-010] p. 6;
- [S-016] PDF p. 7;
- [S-018] pp. 1, 7, 8;
- [S-033] pp. 1, 4, 39, 40, 41, 53;
- [S-034] pp. 17, 52;
- [S-035] PDF pp. 23, 48, 57, 77, 82, 83, 86;
- [S-007] pp. 10, 22, 25;
- [S-105] P.6/9 and P.8/9.

**Counts.** "By hand" covers the 10 fragments the script did not place in a source text. All 10 were confirmed by rendering, by reading the page, or by a further download; the other 22 unplaced strings are translations.

| Source (nearest tag) | Fragments | In tagged source | Other tag on line | Stage 1 text | By hand | Translations (not source text) | Not found | Unreachable (tried) |
|---|---|---|---|---|---|---|---|---|
| S-001 ICHD-3 | 65 | 60 | 0 | 1 | 4: three quotes with the unmapped "±" and "−" glyphs (p. 190, rendered), and one search-log row label (not source text) | 0 | 0 | 0 |
| S-002, S-005, S-007 | 24 | 12 | 7 | 5 | 0 | 0 | 0 | 0 |
| S-008 IHS 2024 | 27 | 19 | 8 | 0 | 0 | 0 | 0 | 0 |
| S-010 IHS 2025 | 38 | 33 | 1 | 4 | 0 | 0 | 0 | 0 |
| S-011, S-012, S-013, S-016, S-018, S-023, S-029, S-030, S-032, S-042 | 48 | 34 | 12 | 2 | 0 | 0 | 0 | 0 |
| S-014 Lifting The Burden | 37 | 31 | 1 | 4 | 1: an [S-008] phrase on a line tagged S-014, found on [S-008] p. 12 | 0 | 0 | 0 |
| S-015 NICE CG150 | 42 | 35 | 4 | 2 | 1: the same [S-008] phrase, p. 12 | 0 | 0 | 0 |
| S-028 NVN | 13 | 10 | 2 | 0 | 0 | 1 | 0 | 0 |
| S-033 Russian adults | 47 | 21 | 22 | 0 | 0 | 4 | 0 | 0 |
| S-034 Russian children | 17 | 8 | 2 | 1 | 2: the title page, an image, rendered ("Возрастная группа" "дети") | 4 | 0 | 0 |
| S-035 Turkish protocol | 50 | 33 | 4 | 0 | 0 | 13 | 0 | 0 |
| S-101 to S-106 | 34 | 30 | 2 | 0 | 2: the search-log label variants, found in PMC8684566 ("little or none") and PMC6537129 ("minimal or infrequent disability", grade IVa) | 0 | 0 | 0 |
| **Total** | **442** | **326** | **65** | **19** | **10** | **22** | **0** | **0** |

**Translations.** I read every Stage 2 translation against its original, and all are faithful:
- [S-028]: the PICO line;
- [S-033]: the title page, the section 3.3 comment (p. 39), the PREEMPT recommendation (p. 40) and the p. 41 comment;
- [S-034]: the flowchart box (p. 52), the title page and section 2 (p. 17);
- [S-035]: Kutu 8 items 2 and 7 (item order checked on p. 48), 3.3 b, the three 3.6.3.9 sentences, the section 6 and chapter 7 headings, and the 7.1 and 7.3 items (third, fourth and fifth items, checked on p. 86).

### Citation metadata and versions

- **Europe PMC records** agree with section 10:
  - S-101: Cephalalgia 2011;31(3):357–367; 10.1177/0333102410379890; PMID 20819842; "Validation Study";
  - S-102: J Headache Pain 2015;16:24; 10.1186/s10194-015-0503-y; PMID 25902814; Stewart and Lipton among the authors;
  - S-104: Health Qual Life Outcomes 2003;1:29; 10.1186/1477-7525-1-29; PMID 12914662;
  - the S-103 developer paper: Neurology 2001;57(11):2034–2039; 10.1212/wnl.57.11.2034; PMID 11739822.
- **S-105.** PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
- **S-106.**
  - TA260 reads "Published: 27 June 2012" and "Last reviewed: 11 January 2016".
  - Paragraph 2.1 gives "every 12 weeks".
  - Recommendation 1.2 reads "less than a 30% reduction in headache days per month after 2 treatment cycles".
- **NICE CG150.**
  - The Overview page reads "Last reviewed: 23 September 2026" (links to technology appraisals added). It also announces a future update of the management section.
  - The Recommendations page still reads "Last updated: 03 June 2025". Recommendations 1.2.6, 1.3.9, 1.3.21, 1.3.24 to 1.3.29, 1.3.37, 1.3.39 and 1.3.48 read as quoted.
  - No newer version changes an element.

### Value sets, codes, units, labels and thresholds (category B)

All of these are correct against the downloaded sources:
- **ICHD-3 code labels** (pp. 8, 9, 12).
- **8.2 reference levels and span** (pp. 122–125):
  - 15 days per month for 8.2.3;
  - 10 days per month for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8;
  - more than three months for all.
- **`classesOf826`** against 8.2.6 criterion B, note 2, and the 8.2.5 note on combination-analgesics (p. 124).
- **The A1.1 window**, day 1 ± 2 (days −2 to +3, no day 0; p. 190, rendered).
- **The remission sentence** of the Definitions of terms (p. 209). See R21b-01 for the other ICHD-3 wordings.
- **Instruments:**
  - HIT-6: range 36–78 and the four bands; one-month recall ([S-101]: "a one-month recall of the HIT-6");
  - MIDAS: grades I–IV, labels and bands, three-month recall ([S-102]);
  - PedMIDAS: four grades, with "Greater than 50" as `strictLow` ([S-103]);
  - HALT-90: Table 18, overlapping at 20 ([S-014]);
  - HADS: 0–21 per subscale; PHQ-9: 0–27; GAD-7: 0–21.
- **Named responder criteria:** NICE 1.3.28 and 1.3.29, IHS Q6 (list on p. 12; MIDAS and HIT-6 thresholds on p. 13), DMKG/ÖKSG/SKG, Russian section 7.1, and the four IHS 2025 control levels (p. 6, read in full).
- **The 18 evaluation rules.** Offsets, anchors, timings, ages and exclusions agree with their quotes.
- **SIGN 155 (2026 update).** I searched every page for weeks, months and cycles. It names no further evaluation time point beyond the two SIGN rules; the six-to-12-month and 12-month continuation statements are classified correctly in the E-041 Notes.
- **Date examples, recomputed by script.** All the stated dates are correct:
  - 12 weeks from 1 January 2026 gives 26 March, with its final 28 days from 26 February to 25 March, and the 3-month point is 1 April;
  - the interval ends are 28 February (Turkish Box 8), 25 March (NICE 1.3.28) and 31 March (the 3-month time points);
  - 6 months after the start is 1 July (181 days), and 24 weeks is 18 June;
  - 4 to 31 December is 28 days;
  - 10 March to 21 April is 43 days; the first 28-day period ends on 6 April, and the review window runs from 7 April to 5 May;
  - 15 August to 20 October is 67 days.

### Fidelity to Stage 1 (category C), requirement by requirement

| OUT | Result |
|---|---|
| 001 | OK. Each view states its period, with start, end and length at MUST (E-003, E-005, INV-002, INV-003). Monthly frequency outputs are MUST (INV-014, INV-015, INV-108). Equal-length comparison (INV-037, INV-055). The Caveat is met by the stated length. |
| 002 | OK. INV-008 (SHOULD), over every form of the four measures (`reports`). |
| 003 | OK. INV-011 and INV-012; no cut-off presented as validated (INV-013, SHOULD NOT). |
| 004, 005 | OK. INV-014 and INV-015 (MUST); ICHD-3 definition (INV-009, MUST); migraine-day label SHOULD (INV-008). |
| 006, 007 | OK. Provision at SHOULD (INV-016, INV-017) and monthly availability where provided at MUST (INV-108). Attacks are a separate element with the ICHD-3 label (E-019, INV-010). |
| 008 | OK. MAY elements (E-020 to E-022); see ISS-03 and ISS-04. |
| 009 | OK. Time course with start, dose-change and stop markers in the view (INV-034 to INV-036); weekly values where relevant (INV-001, INV-034). |
| 010 | OK. Stated scale (INV-018); comparison between periods (INV-039). |
| 011 | OK. INV-019; label for treated attacks (INV-020); the Caveat as SHOULD NOT (INV-021). |
| 012 | OK. Across periods (INV-022) and per treated attack (INV-072, INV-076). |
| 013 | OK. MAY (E-027), separate from headache measures. |
| 014, 015 | OK. Total, class and drug together (INV-023, INV-024); weekly view (E-036, INV-025). |
| 016 | OK. Per period, class and combined use, with code, level, span and basis (INV-044 to INV-046); prompt at MUST (INV-047); not a diagnosis at MUST NOT (INV-048); see ISS-01. |
| 017 | OK. INV-049 to INV-052; see ISS-11. |
| 018 | OK. INV-053 to INV-059; no continuation decision at MUST NOT (INV-106); see ISS-03 and ISS-10. |
| 019 | OK. E-044, INV-060 and INV-061 (SHOULD); see ISS-03 and ISS-05. |
| 020 | OK. INV-062 to INV-065; see ISS-08. |
| 021 | OK. MUST components (INV-068, INV-102); SHOULD components where provided (INV-069, INV-071, INV-072). |
| 022 | OK. INV-070, INV-103. |
| 023 | OK. INV-071 to INV-075; no decision on the definition of response at SHOULD NOT (INV-107). |
| 024 | OK. INV-077 to INV-079, INV-109; the Caveats are stated in the E-054 Meaning. |
| 025 | OK. MAY (E-056, INV-080). |
| 039 | OK. INV-066, INV-067, INV-104, INV-109. |
| 026 | OK. INV-081, INV-082, INV-100; see ISS-06. |
| 027 | OK. INV-026, INV-027, INV-033. |
| 028 | OK. INV-040 to INV-043 (MUST, SHOULD and SHOULD NOT, as in Stage 1). Following Stage 1 section 1, the view names codes 1.3 and 2.3 and restates no criterion, so no threshold is shown and none is missing. |
| 029 | OK. INV-028 (MUST), INV-029 (SHOULD), INV-030; see ISS-09. |
| 030 | OK. MUST (E-060, E-061, INV-086, INV-087); see ISS-03. |
| 031 | Represented (E-062 to E-064, INV-088, INV-089). The remission duration is the subject of R21b-01. |
| 032 | OK. MAY, with the caveats at SHOULD (INV-090, INV-100, INV-110). |
| 033 | OK. INV-083 to INV-085, INV-100. |
| 034 | OK. INV-094, INV-104; see ISS-04. |
| 035 | OK. INV-095, INV-105; see ISS-03. |
| 036 | OK. INV-096 to INV-098; `ruleRuChildren`; INV-055. |
| 037 | OK. INV-091 to INV-093. |
| 038 | OK. INV-099 to INV-101. |

**Conformance levels.** Every invariant level matches the strength of the Stage 1 statement part it realises:
- MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33.
- Every SHOULD NOT and MUST NOT predicate begins with `¬`.
- No positive-level predicate is a bare prohibition.

I also spot-checked the attribute levels of the MUST, SHOULD and MAY elements against section 3.3, item 3.

### Mechanical checks (category E)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), with no gaps and no duplicates. No dangling E- or INV- reference. Every S reference lies in S-001–S-046 or S-101–S-106. Exactly the 39 Stage 1 OUT IDs are referenced. |
| Fields | Every item has exactly one Realises, Conformance and Evidence field. Every element has one Definition and one Meaning; every invariant has one Predicate and one Reading. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025). For every requirement, the row's E and INV sets equal the reverse index of the Realises fields: 0 mismatches. |
| Declarations (`decl.py`) | 555 declared names in the `omn` blocks, none declared twice. The only used name not declared in a block is `refs`, which section 2.5 defines. |
| Precedence and guards | Read by hand: INV-003, INV-046, INV-062 to INV-064, INV-087, INV-089 and INV-098. Every partial term is guarded, including `÷`, `days`, `first`, `last`, `min`, `max`, `periodEndFrom` and `s(i)`. |

### Scope sweep (category F)

I searched the model for:
- enter/entry, record, input, captur…, logged, store/storage, persist…, database;
- JSON, XML, CSV, FHIR, HL7, serializ/serialis, encod…, retention, reminder;
- answer…, algorithm…, data entry, data field, calculat…, comput… and "decision logic".

I read every hit in context. Each one is one of these:
- an exclusion statement (sections 1, 2.1, 2.7 and 3.5);
- an out-of-scope note (E-033, E-057, INV-076);
- the [S-014] HALT-30 quote ("records days affected"), quoted for the recall period;
- "can be answered with" (INV-014 Reading);
- a search-log or change-log entry.

Every relation and threshold takes as arguments only output elements, context properties stated as Stage 1 states them, and cited constants. The thresholds, formulas and computed fields that are part of the output data are present, each with its relation:
- change: INV-053;
- totals: INV-024;
- overuse indicator: INV-045, INV-046;
- instrument category and change: INV-082;
- criteria: E-045, INV-063, INV-064;
- completeness: INV-012;
- durations: INV-079, INV-089;
- rates: INV-089;
- time points and review window: INV-058, INV-051;
- perimenstrual window: INV-087;
- outcome proportions: INV-074.

### Section 8 (category G)

ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded, and the passages they cite read as described:
- ISS-01: pp. 124–125;
- ISS-02: pp. 12, 105, 123 and 139;
- ISS-03: Stage 1 Statements and Rationales, and p. 190;
- ISS-09: p. 122;
- ISS-10: NICE 1.3.9 and 1.3.39, and [S-034] p. 52;
- ISS-11: the CG150 Overview and 1.3.48.

Every issue is pointed to from the elements it affects. One Stage 1 issue is resolved without being recorded: R21b-01.

## Remarks

### R21b-01 Stage 1 issue handling: the cluster remission duration conflicts within ICHD-3, and the model resolves it silently
- **Item(s):** E-063 (Meaning, Evidence, Notes); INV-089 (remission conjunct); E-062; section 8; traceability row OUT-031.
- **Problem:**
  - OUT-031 asks, for patients with cluster headache, for "cluster periods (bouts) and cluster remission periods with their start dates, end dates and durations, using the ICHD-3 definitions [S-001]". Stage 1 quotes the first sentence of the Definitions-of-terms entry and leaves out its duration sentence.
  - ICHD-3 gives the duration of a remission in three different ways:
    - Definitions of terms: a remission must exceed three months;
    - 3.1.1 Episodic cluster headache: remission periods of at least three months;
    - 3.1.2 Chronic cluster headache: remission periods lasting less than three months, which its Description and its diagnostic criterion B both name.
  - The model takes the Definitions-of-terms sentence and makes it definitional. INV-089 states "a remission period shown lasts more than three months" (`plusMonths(s, remissionMoreThanMonths) ≤ e`). So an output that shows a remission of three months or less is not a valid output.
  - Two consequences follow:
    - **Chronic cluster headache.** A subject with 3.1.2, by its criterion B, has no remission or only "remissions lasting <3 months" within a year. The model therefore never admits a remission period for such a subject, although ICHD-3 calls these attack-free periods remissions and uses them to define the subtype. The E-062 `remissions` (SHOULD) cannot be met; fix 02 (item 14) treats this as a deviation.
    - **Episodic cluster headache.** A remission of exactly three months meets 3.1.1 criterion B ("≥3 months") but cannot be shown.
  - E-063 Meaning describes the item as "an attack-free period that ICHD-3 considers a remission". Given 3.1.1 and 3.1.2, this describes the model's choice inaccurately.
  - The choice is recorded nowhere. E-063 Evidence quotes only p. 209, E-063 Notes do not mention 3.1.1 or 3.1.2, and section 8 has no entry.
  - By contrast, the model discloses its other readings of ICHD-3 thresholds, for example the "> 3 months" reading of 8.2 in the E-032 Notes, and records Stage 1 reading questions in section 8 (ISS-01, ISS-09).
  - PROCESS.md section 4 requires a contradiction found in Stage 1 to be recorded in section 8, with a pointer from the affected element, not resolved silently (section 9, "Stage 1 issue handling").
- **Evidence:**
  - Stage 1 OUT-031 Statement: "cluster periods (bouts) and cluster remission periods with their start dates, end dates and durations, using the ICHD-3 definitions [S-001]".
  - Stage 1 OUT-031 Evidence: "[S-001] "Cluster remission period: The time during which attacks cease to occur spontaneously and cannot be induced with alcohol or nitroglycerine." (Definitions of terms, p. 209; the next sentence of the definition, a duration criterion, is not quoted)".
  - [S-001] (https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf). I verified each quote below in the text layer and on the page rendered with `pdftoppm`:
    - "To be considered a remission, the attack-free period must exceed three months." (Definitions of terms, Cluster remission period, p. 209; quoted in E-063.)
    - "Cluster headache attacks occurring in periods lasting from seven days to one year, separated by pain-free periods lasting at least three months." (3.1.1 Episodic cluster headache, Description, p. 42; the text layer breaks "periods" at a line end.)
    - "At least two cluster periods lasting from seven days to one year (when untreated) and separated by pain-free remission periods of ≥3 months." (3.1.1, diagnostic criterion B, p. 42; "≥" is a glyph without a text mapping, read on the rendered page.)
    - "Cluster headache attacks occurring for one year or longer without remission, or with remission periods lasting less than three months." (3.1.2 Chronic cluster headache, Description, p. 42.)
    - "Occurring without a remission period, or with remissions lasting <3 months, for at least one year." (3.1.2, diagnostic criterion B, p. 42.)
  - Model text:
    - E-063 Meaning: "a cluster remission period (an attack-free period that ICHD-3 considers a remission)";
    - E-063 Evidence quotes p. 209 only;
    - INV-089: `(x ∈ RemissionPeriodItem ⇒ ∀ s ∈ x.start; e ∈ lastDay(x) • plusMonths(s, remissionMoreThanMonths) ≤ e)`, Conformance "definitional (E-063, E-064)", with the Reading "a remission period lasts more than three months".
  - **Why this is new evidence.**
    - Review 02 ("Checked and not raised") compared only p. 209 with 3.1.1 criterion B ("≥3 months"), a one-day boundary, and called it "an inconsistency inside ICHD-3, not a model defect". Later reviews repeated this as settled, and review 19b justified INV-089 with "This matches ICHD-3".
    - None of them cited the 3.1.2 Description or criterion B, where ICHD-3 calls attack-free periods shorter than three months remissions. That wording turns the conflict into a substantive one for a subgroup that OUT-031 covers. None of them weighed PROCESS.md section 4 on recording a contradiction.
  - **Oscillation.** No fix ever changed this point, and no fixer declined a remark on it. The oscillation check after iteration 16 lists "the '> 3 months' readings of INV-045 and INV-089" among the settled points. Option (a) below changes no predicate or value, so it reverses nothing.
- **Required change:**
  - **(a) Text only; preferred.**
    1. Add a Stage 1 issue to section 8 (a new ID, for example ISS-12), "Cluster remission duration in ICHD-3".
       - It states that OUT-031 refers to "the ICHD-3 definitions", and quotes verbatim, with locations, the Definitions-of-terms sentence (p. 209), the 3.1.1 Description and criterion B (p. 42), and the 3.1.2 Description and criterion B (p. 42).
       - It states the effect on the model: E-063 and INV-089 follow the Definitions of terms. So a remission of three months or less, including every remission of chronic cluster headache that 3.1.2 describes, cannot be shown as a remission period, and the attack-free intervals between bouts appear only through the bouts' dates.
       - It asks the human which ICHD-3 usage OUT-031 means: in particular, whether attack-free periods of less than three months in chronic cluster headache, and remissions of exactly three months, should be shown as remission periods.
    2. Add a pointer to that issue in the E-063 Notes, the INV-089 Notes and the OUT-031 coverage reason.
    3. Reword E-063 Meaning so that it names the source of the duration accurately, for example "an attack-free period that exceeds three months, as ICHD-3 Definitions of terms requires".
  - **(b) Alternative.** If the fixer concludes that "the ICHD-3 definitions" of OUT-031 include the 3.1.1 and 3.1.2 usage, change E-063 and INV-089 so that they no longer exclude remissions of three months or less. Possible ways:
    - drop the lower bound;
    - make it conditional on the subject not having or possibly having 3.1.2;
    - add a stated kind of attack-free period.

    The new evidence must be cited verbatim (p. 42). The choice must still be recorded in section 8 as in (a), because it departs from the Definitions-of-terms sentence that E-063 now quotes.

## Checked and not raised

- **Labels under a criterion whose conditions do not hold.** For example, the DMKG/ÖKSG/SKG criterion applied to a chronic-migraine treatment: INV-063 forces "non-responder".
  - Review 02 judged this not a remark, because the criterion's name states its condition. Labels are optional (OUT-020, "If the output displays").
  - No new evidence. Not raised.
- **Treated attacks outside `reports`** (E-011). The counts of treated attacks and of attacks with a symptom are not read as reports of the attacks measure. Fix 12 decided this (R12-02), and I have no new evidence.
- **Untranslated non-English fragments in the E-041 Evidence.** These are headings and fragments quoted only to show that they name migraine: "3. MİGREN BAŞ AĞRISI TEDAVİSİ", "Migren Profilaktik Tedavi-Yönetim-6", «Мигрень», "Migren Klinik Protokolü" and "Profylactische behandeling migraine".
  - The surrounding English text states what each shows.
  - The longer fragments are parts of quotes that are translated nearby.
  - A translation would add no evidence. Not a remark, as review 21 also judged.
- **OUT-024 Caveats** ("supports, but does not by itself establish, eligibility"). This is descriptive, and the E-054 Meaning states it. Stage 1 words it as no prohibition. Not raised.
- **`refs` and `⊑` for codes the model does not name** (for example 1.1 or 3.1.2).
  - `refs` is defined in section 2.5.
  - `⊑` is a given function whose meaning, the ICHD-3 code hierarchy, is stated in its declaration comment and in the E-009 Meaning. Its axioms tabulate the named codes, as given functions are used throughout.
  - Not a defect.
- **Units of variant payloads** (for example `daysWithSymptom ⟨ℕ⟩`, `completeCycles`). The tag names state the unit, and rule U1 requires units on display. Not a remark (style).
- **HIT-6 one-month recall** ([S-101], "a one-month recall of the HIT-6"); **HADS subscales only**; **MIDAS labels and the Grade IV subdivision**. Settled, with no new evidence.
- **The IHS 2024 Q2 comment on onabotulinumtoxinA** (dose increase after the first cycle; later responders). E-041 classifies it as a dose-optimisation check, not an evaluation time point (watch point 5). Not reopened.
- **OUT-028 thresholds.** Stage 1 section 1 names standards "instead of restating their criteria", and OUT-028's "source definitions (see OUT-002)" are the measure definitions. So no 1.3 or 2.3 threshold is shown, and none is missing.
- **E-008 and E-041 typing of onabotulinumtoxinA as a quarterly injectable.** It is consistent with IHS 2024 Q2 ("injectable drugs administered quarterly") and with the 12-week re-treatment of [S-106]. Not raised.
- **NICE 1.3.25 (rimegepant).** It is a CGRP inhibitor recommended for adults, so it is covered by `cgrpInhibitor`, `ruleNice1328` (`adultsOnly`) and `critNice1328`. Consistent.
- **The v20 text changes** (ISS-03, the section 3.5 list, the Notes pointers, the three coverage reasons). They are consistent with the Stage 1 Statements and the unchanged predicates, and the new p. 190 quote is verbatim (rendered).
- **The main review's "not raised" items.** I re-examined these and agree that none requires a change:
  - INV-031, the marks conjunct;
  - the E-041 rule list against the IHS Q6 Background and the Q2 comment;
  - HALT versions;
  - name reuse in OMN;
  - "early onset of effect";
  - instrument results in the clinician-facing summary.
- **Oscillation watch points.** R21b-01 touches none of watch points 1 to 7. Its option (a) leaves INV-089's settled "> 3 months" reading unchanged.

## Notes on frozen items (for the human)

None. `FROZEN_ITEMS.md` does not exist, and no item of v20 carries a FROZEN marker.
