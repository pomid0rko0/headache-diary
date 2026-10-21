# Review — iteration 19
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v18
Date: 2026-10-21

## Summary

This is the main review of iteration 19: an independent fact-check and review of v18. `OUTPUT_MODEL.md` is byte-identical to `history/v18.md` (checked with `cmp`). The working tree was clean at the start.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 after OUT-025) and the source table of section 5;
- v18: sections 1–10, every element and every invariant; sections 11 and 12 for the iteration 16–18 entries and the source rows;
- review 18 and fix 18;
- the oscillation check after iteration 16, with its eight watch points.

**Earlier decisions.**
- FROZEN_ITEMS.md does not exist, and no item of v18 carries a FROZEN marker.
- I raise nothing, so no declined remark is re-raised and no earlier fix is reversed.

**v17 → v18.** By script, 12 model items changed: E-041, E-042, E-043, E-046, E-048, INV-055, INV-058, INV-059, INV-063, INV-064, INV-068 and INV-097, plus rows OUT-018, OUT-020 and OUT-021 and the housekeeping sections. These match the items that fix 18 lists.
- The E-041 `omn` block and section 2.8 are byte-identical to v17.
- Every item named in the watch points of the iteration-16 check is byte-identical to v17: INV-105, E-067, E-062, E-045, E-012, INV-062, INV-098, INV-086, INV-087, E-060, E-061, INV-049 to INV-051, E-039, INV-003, INV-054, INV-056, E-040, E-008, INV-071, INV-088, INV-104, INV-109, E-047, E-051, INV-066, INV-069 and INV-072.

**Result.**
- **Citations.** No defect. Every quoted fragment is verbatim at its stated location.
- **Value sets, codes, labels, thresholds and metadata.** No defect.
- **Fidelity.** All 39 requirements are represented at the right strength.
- **Mechanical checks.** All pass.
- **Scope sweep.** No input, storage or derivation-from-input content. No threshold, formula or computed field of the output data is missing.
- **R18-01.** The fix is correct, complete and satisfiable. I re-checked it independently by script.
- **Section 8.** Every issue is founded.

## Verification coverage

### Method

- **Downloads.** All downloads were made with `curl` through the configured proxy, into the fresh directory `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r19dl-im5F`, outside the repository. Every request returned HTTP 200 on the first attempt.
  - **Stage 1 PDFs** (pages):
    - S-001 ICHD-3 (211); S-002 (19); S-005 (14); S-007, UCL Discovery (39);
    - S-008 (31); S-010 (11); S-016 SIGN 155 (64); S-018 AAN/AHS Clinician Summary (12);
    - S-030 (86); S-033 (92); S-034 (53); S-035 (92).
  - **Stage 1 web pages:** S-015, the NICE CG150 Recommendations and Overview pages; S-028, the NVN module page.
  - **Europe PMC full-text XML:**
    - S-004 (PMC6501455), S-011 (PMC9188162), S-012 (PMC9555163), S-013 (PMC7296705), S-014 (PMC6734476), S-023 (PMC9607711), S-042 (PMC12279330);
    - S-101 (PMC3057423), S-102 (PMC4406925), S-104 (PMC183845).
  - **New-source pages:**
    - S-103, the Cincinnati Children's PedMIDAS page;
    - S-105, the 9-page manual PDF;
    - S-106, the TA260 overview, chapter 1 and chapter 2.
- **Extraction.**
  - PDFs page by page with `pdftotext -raw` and `-layout`.
  - HTML and XML with scripts and markup removed and entities unescaped.
- **Rendered with `pdftoppm` and read by eye:**
  - ICHD-3 p. 190: the A1.1.1 and A1.1.2 window "day 1 ± 2 (i.e. days −2 to +3)" and note 2. The "±" and "−" glyphs and "+3" have no text mapping.
  - S-034 title page, an image without a text layer, which reads "Возрастная группа" / "дети".
- **Scripts.** All are in the scratchpad folder `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r19scripts/` and were run with `python3 -I`.
  - `quotes.py` extracts every double-quoted string outside `omn` blocks on a line with an `[S-NNN]` tag. It splits each at `[...]` and "…" and keeps fragments of at least 6 letters. It searches each fragment with three normalisations: NFKC with quotes and dashes unified; line-end hyphens removed; letters and digits only. The search order is the source of the nearest preceding tag, then the other sources tagged on the line, then Stage 1 v18.
  - `where.py` lists every page on which a fragment occurs, so that stated pages can be checked.
  - `mech.py` and `names.py` run the mechanical checks.
  - `stop19.py` is the instance check of the v18 constructs.
- **Metadata.**
  - PubMed esummary confirms S-101 (PMID 20819842), S-102 (PMID 25902814), S-104 (PMID 12914662) and the PedMIDAS developer paper (PMID 11739822): authors, journal, year, volume, pages, DOI and PMCID as in section 10. PubMed spells the S-102 author "Pavlović"; the model's "Pavlovic" is a transliteration.
  - S-105 PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014. The title "Instructions for Patient Health Questionnaire (PHQ) and GAD-7 Measures" and the developers sentence on P.8/9 read as cited.
  - S-106: "Published: 27 June 2012", "Last reviewed: 11 January 2016". Chapter 1 has "less than a 30% reduction in headache days per month after 2 treatment cycles", and paragraph 2.1 reads as quoted.
  - S-103 page footer: © 2026.
- **Newer versions.**
  - **ICHD-3.** A web search finds no published ICHD-4; only the "Work in Progress" papers of the classification committee exist.
  - **NICE CG150.** The Recommendations page shows "Published: 19 September 2012 Last updated: 03 June 2025". The Overview shows "Last reviewed: 23 September 2026". Recommendations 1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39 and 1.3.48 read as quoted.
  - **EHF CGRP guideline.** A web search finds no update after 2022.
  - Nothing newer changes an element.

### Citations

Column definitions:
- **Source:** found verbatim in the downloaded source of the nearest tag.
- **Other tag:** found in another source tagged on the same line. These occur in the multi-source lines of E-041, E-045, E-057 and the logs, and each was read in context.
- **Stage 1:** a fragment of a Stage 1 quote, checked against Stage 1 v18.
- **By hand or eye:** verified manually; see the notes in the row.
- **Not source text:** translations, prose that the extractor captured between two quotations, and search-log query strings.

| Source (nearest tag) | Fragments | Source | Other tag | Stage 1 | By hand or eye | Not source text | Not found | Unreachable (tried) |
|---|---|---|---|---|---|---|---|---|
| S-001 ICHD-3 | 65 | 56: labels pp. 8, 9, 12; 8.2–8.2.8 pp. 122–125; 8.2.3 comment p. 123; remission p. 209; Definitions of terms pp. 209–210; A1.1 note 2 p. 190 | 0 | 4 | 2 (p. 190 window, by eye) | 3 | 0 | 0 |
| S-002, S-004, S-005, S-007 | 30 | 17 (S-005 "the final 28 days of the treatment period" p. 8; S-007 "≥ 14 attacks per week on average" p. 10, rates pp. 22, 25) | 7 | 6 | 0 | 0 | 0 | 0 |
| S-008 IHS 2024 | 29 | 21 (Q2 p. 9; Q4 p. 11; Q6 p. 12; Q6 Evidence p. 13; Q13 p. 17) | 7 | 0 | 0 | 1 | 0 | 0 |
| S-010 IHS 2025 | 48 | 37 (p. 6: the four control levels, the migraine-day paragraph, the "proxy" sentence, insufficient control) | 0 | 8 | 0 | 3 | 0 | 0 |
| S-011, S-012, S-013, S-016, S-018, S-023, S-028, S-029, S-030, S-032, S-042 | 75 | 54 (S-016 PDF pp. 7, 20; S-018 pp. 1, 7, 8; S-028 PICO and Aanbeveling; S-030 PDF p. 19) | 16 | 2 | 0 | 3 | 0 | 0 |
| S-014 Lifting The Burden | 38 | 26 (HALT recall, units, Table 18 with the "≥20" row; HURT areas) | 1 | 9 | 1 (the S-008 Q6 phrase "acceptable for treatment continuation beyond three months", p. 12) | 1 | 0 | 0 |
| S-015 NICE CG150 | 56 | 39 (1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48, headings, Overview population sentence) | 3 | 12 | 1 (the S-008 phrase "for treatment continuation beyond three months", p. 12) | 1 | 0 | 0 |
| S-033 Russian adults | 49 | 19 (p. 1; p. 4 "М – мигрень"; pp. 39, 40, 41, 53) | 12 | 0 | 0 | 18 | 0 | 0 |
| S-034 Russian children | 20 | 8 (p. 17; p. 52 flowchart) | 2 | 4 | 2 (title page, by eye) | 4 | 0 | 0 |
| S-035 Turkish protocol | 50 | 33 (Kutu 8 p. 48; 3.3 b p. 23; 3.6.3.9 p. 57; section 6 p. 77; chapter 7 heading p. 82; 7.1 p. 83; 7.3 p. 86, "2 k ez" as printed) | 4 | 0 | 0 | 13 | 0 | 0 |
| S-101 to S-106 | 39 | 29 (S-101 "Data sources", HIT-6 range and four categories; S-102 grades and recall; S-103 grading table rows paired as quoted; S-104 HADS 0–21; S-105 P. 6/9; S-106 paragraph 2.1 and chapter 1) | 2 | 1 | 0 | 17 (mostly search-log queries) | 0 | 0 |
| **Total** | **499** | **329** | **52** | **48** | **6** | **64** | **0** | **0** |

**Translations.** I read every translation added in Stage 2 against its original in context, and all are faithful:
- [S-028]: the PICO sentence;
- [S-033], four sentences: section 3.3 comments; the PREEMPT recommendation; the anti-CGRP comment, p. 41; the title page;
- [S-034]: the flowchart box, section 2 and the title page;
- [S-035], 14 sentences: Kutu 8, items 2 and 7; 3.3 b; 3.6.3.9 (three sentences); section 6 and chapter 7 headings; 7.1 (two sentences); 7.3 (three items).

### Value sets, codes, units, labels and thresholds

All were checked against the downloaded sources, and all are correct:
- **ICHD-3 code labels** (E-009; pp. 8, 9, 12).
- **ICHD-3 8.2 reference levels** (E-032; pp. 122–125): 15 for non-opioid analgesics; 10 for ergotamine, triptans, opioids, combination analgesics, 8.2.8 and 8.2.6; "for more than three months". Also 8.2.6 criterion B (p. 124), note 2 (p. 125) and the 8.2.3 comment (p. 123).
- **A1.1 window** "day 1 ± 2 (i.e. days −2 to +3)" and "there is no day 0" (rendered p. 190).
- **Cluster remission** "must exceed three months" (p. 209).
- **Instrument value sets:**
  - HIT-6: 36–78; bands ≤49, 50–55, 56–59 and 60–78 with the four labels of [S-101].
  - MIDAS: grades I–IV with the [S-102] labels; bands 0–5, 6–10, 11–20 and ≥21; three-month recall.
  - PedMIDAS: 0 to 10 "Little to none", 11 to 30 "Mild", 31 to 50 "Moderate", "Greater than 50" "Severe".
  - HALT-90: 0–5, 6–10, 11–20 and ≥20 with the Table 18 labels and grades I–IV. HALT-30: one-month recall and "Grading is not used by HALT-30".
  - HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
- **Responder criteria:**
  - IHS Q6: ≥ 50 %; the ≥ 30 % chronic alternative; MIDAS ≥ 5 points for baseline 11–20 and ≥ 30 % for baseline ≥ 20; HIT-6 ≥ 5 points.
  - DMKG/ÖKSG/SKG: 50 %, 5 points, 30 %.
  - NICE 1.3.28 (50 % / 30 %) and 1.3.29 (30 %, after 2 cycles); Russian section 7.1 (50 %, 3 months).
  - IHS 2025 control levels.
- **Review intervals:** NICE 1.3.48, 4–8 weeks; TA260, re-treatment every 12 weeks.
- **Evaluation rules.** All 18 rule constants of E-041 match their quotes in offset, anchor, timing, ages, `appliesTo` and `excludes`. The same holds for the 6 criterion constants of E-045.

**Date examples of the v18 text, recomputed by script:**
- E-007: 15 August to 20 October is 67 days.
- E-042, INV-055: start on 1 January 2026.
  - The NICE 1.3.28 time point is 26 March, and 26 February to 25 March is 28 days.
  - The 3-month time point is 1 April. Box 8's earliest date is 1 March, so its interval ends on 28 February.
  - 4 to 31 December 2025 is 28 days.
  - Stopped on 10 February: no time point is required. Stopped on 30 March: NICE 1.3.28 and Box 8 only. Stopped on 31 March: all of them.
- INV-049: 10 March + 27 days is 6 April; 21 April is day 43; the NICE window is 7 April to 5 May.
- INV-105: 10 March to 21 April is 43 days.

All are correct.

### Fidelity to Stage 1 (all 39 requirements)

| OUT | Result |
|---|---|
| 001 | Periods with start, end and length at MUST (E-005, INV-002, INV-003); frequency outputs per month or 28-day period (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); the Caveat through `lengthDays`. OK. |
| 002 | SHOULD definition label in every reporting form (`reports`, INV-008). OK. |
| 003 | SHOULD indicator for every summarised period (INV-011, INV-012); SHOULD NOT cut-off (INV-013). OK. |
| 004–008 | Levels and conditions match: INV-009 MUST ICHD-3, INV-014 to INV-017, INV-108; OUT-008 at MAY. OK. |
| 009 | Time course with dated start, dose-change and stop markers in the view; weekly values where relevant (INV-034 to INV-036, INV-001). OK. |
| 010–013 | Intensity on a stated scale and compared between periods. Duration with its label, and the Caveat as SHOULD NOT. Symptoms and the most bothersome symptom across periods and per attack. Aura at MAY. OK. |
| 014–016 | Total, per class and per drug together (INV-023, INV-024). Weekly view (INV-025). Indicator with code, level, span and basis; prompt at MUST; "not a diagnosis" at MUST NOT (INV-044 to INV-048). OK. |
| 017 | Follow-up view with the 4–8-week window, the following year and the worsening label (INV-049 to INV-052). OK. |
| 018 | Comparison aligned to the start; values and both forms of change, co-present at MUST; time points of the 18 rules within their populations. v18: a rule's time point is shown and required only at anchors whose interval the course completes. The comparison at a time point ends within the course, and a comparison is still required for every started treatment, with "periods after treatment start" as Stage 1 states them. Caveat at MUST NOT (INV-106). OK. |
| 019 | Residual burden next to every percentage change in migraine or headache days (INV-060, INV-061). OK. |
| 020 | Optional label with criterion, values, other values and decidable components; not the sole indicator (SHOULD NOT); no continuation decision. v18: no component decides a responder or non-responder label over a period after a stop or pause (INV-063). Control-level months lie within the course (INV-064). OK. |
| 021 | MUST components for the same periods (INV-068, INV-102). v18: the on-treatment periods end on or before every stop or pause, as "on-treatment periods" reads. SHOULD components where provided (INV-069, INV-071). OK. |
| 022 | Post-stop view with `firstChangedDay`, the on-treatment period and the baseline (INV-070, INV-103). OK. |
| 023 | All named outcome measures, consistency (attack lines), timing of intake, formulation and per-formulation summaries, the baseline/on-treatment split, 15 minutes for cluster headache, Caveat at SHOULD NOT (INV-071 to INV-075, INV-107). OK. |
| 024 | History with dates, dose changes, duration, response, adverse effects, stop reason, formulation and adherence, grouped by class (INV-077 to INV-079, INV-109). OK. |
| 025 | MAY scheme-window view labelled with the scheme (E-056, INV-080). OK. |
| 039 | Adherence next to the comparison, in the history and in the clinician summary (`adherenceFor`, INV-066, INV-067, INV-104, INV-109). OK. |
| 026, 027 | Instrument results with value sets, grading and change (INV-081, INV-082). Functional impact per domain with severe impairment and the baseline comparison (INV-026, INV-027). OK. |
| 028–030 | Three-month view with labels and codes, no diagnosis (INV-040 to INV-043). Per-type outputs (INV-028 to INV-030). Menstrual-relation view with window and complete cycles (INV-086, INV-087). OK. |
| 031 | Bouts, remissions, rates, 15-minute effectiveness and rescue need, previous bouts (INV-088, INV-089). OK. |
| 032, 033 | Trigger view with its caveats, dates in its period (INV-090, INV-110). Screening results next to headache outputs, not diagnoses (INV-083 to INV-085). OK. |
| 034, 035 | All named components (INV-094, INV-104; INV-095, INV-105). OK. |
| 036–038 | Paediatric outputs (INV-096 to INV-098). Composite index (INV-091 to INV-093). Caveats and prohibitions (INV-099 to INV-101). OK. |

### Mechanical checks (scripts, on v18)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), with no gaps and no duplicates. Every E- and INV- reference resolves. ISS-01 to ISS-06 and ISS-08 to ISS-11 have headings; ISS-07 appears only as withdrawn (section 9). |
| Sources | Every S reference lies in S-001–S-046 or S-101–S-106. Every S-1NN has a row in section 10. |
| OUT references | Every OUT reference exists in Stage 1, and all 39 requirements are referenced. |
| Fields | Exactly one Realises and one Conformance field in each of the 177 elements and invariants. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every OUT, the row's E and INV sets equal the sets derived from the Realises fields. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Scopes: output 77, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Attribute levels | core 94, MUST 29, SHOULD 47, MAY 2. The typing rule of section 2.5 holds: every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type, never `set1` or `seq1`. |
| Declarations | No name is declared twice. The only identifiers in `omn` blocks that are not declared are bound variables (A, C, D, K, Ks, L and lower-case ones) and `refs`, which is defined in section 2.5. Every attribute selection names a declared attribute. |
| v18 predicates | All are well typed with no partial term: `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, and the `timePoints` `when` clause of E-043. `plusDays(shift(a, r.minOffset), −1)` is total, and `ctx(outputOf(L))` is total. The usage lists in the E-042 Notes match the `omn` usages (script). |
| Instance check (`stop19.py`) | 30 000 random courses over the 18 rules, with their types, target-dose anchors, cycle anchors, and zero, one or two stops. Wherever INV-055's v18 antecedent holds (156 780 rule–anchor pairs), the construction works in every case. The construction is a 28-day on-treatment period that ends the day before the time point (for a window, before the later of its earliest date and the 28th day after the start). It begins on or after the start, meets `atTimePoint`, and ends on or before every stop or pause. Failures: 0. 35 379 pairs were dropped by a stop before the end of their interval. |

### Scope sweep

- **Grep.** I searched for record, enter/entry, input, captur-, logged, stor-, persist-, database, JSON/XML/CSV/FHIR/HL7, serial-, encod-, retention, reminder, answer, data field, algorithm, calculat-, comput-, obtained and questionnaire.
  - Every count equals v17, except one new "stor-" hit, which is "history" in the iteration-18 search-log entry.
  - The hits are the scope statements of sections 1, 2.1, 2.7 and 3.5; the "obtained from diary information; how is out of scope" notes; the [S-014] HALT-30 quote ("records days affected"); the E-057 notes; and search-log tool names. All are legitimate.
- **Relations.** Every relation added in v18 takes only course events of the output context, which the treatment history also shows (INV-079), output periods, labels, time points and rule constants as arguments. No relation takes recorded data.
- **Thresholds and formulas.** Every threshold, reference level, score band, offset and formula that is part of the output data is present with its verbatim quote. None is missing.

## Remarks

None.

## Checked and not raised

- **R18-01 fix.**
  - **(a) Time points.** INV-058 (definitional), INV-059 (MUST) and the E-043 `when` clause carry the same condition, `applicable ∧ intervalOnTreatment`, so no required time point is excluded. INV-055 requires the comparison at a time point to end within the course, and the instance check confirms that this is always satisfiable. The first conjunct of INV-055 still requires a comparison for every started treatment.
  - **(b) Labels.** The INV-063 guard only weakens the forcing, and INV-064's conjunct constrains only optional control-level labels.
  - **(c) INV-068.** The bound follows OUT-021's wording "on-treatment periods", and INV-102 stays satisfiable, also for a course stopped on its start day.
  - **Fixer's departure from the review sketch.** Dropping `a ≤ e.date` is correct: a stop before the anchor date also ends the course before the interval.
  - **Watch points.** No watch-point item changed.
- **INV-071 per-phase summaries after a stop** (OUT-023 "the on-treatment periods of that preventive treatment"). Fix 18 kept them on the comparison's periods. OUT-023 introduces them with "When a preventive treatment is started (OUT-018)", and its Rationale speaks of "the periods before and after a preventive treatment is started". So the justification holds, and summaries within the course are required in the treatment review view (INV-069 with the v18 INV-068). Not raised.
- **Residual burden after a stop (INV-060)** and **adherence windows after a stop (INV-066, INV-067).** Settled in review 11 and fix 18 respectively. No new evidence. Not raised.
- **`courseOverlaps` and `notStoppedBefore`.** Their stop conjuncts state the same condition. This is equivalent structuring, not a contradiction. Not raised.
- **Window rules with a stop inside the window.** The window stays shown with its latest date, and the comparison ends on or before the stop. The guidance names the review for the window ("3 to 6 months after starting"), so showing it states nothing false. Not raised.
- **HALT-90 grades.** The grade column of Table 18 reads "III (indicates high need for care)" and "IV (indicates high need for care)". The model's grades are "III" and "IV". The parenthetical annotates the grade and is not part of its name. Not raised.
- **ISS-02 wording.** "simple analgesics" occurs once in ICHD-3, on p. 139 (10.1.1 High-altitude headache), in a passage that goes on to acute mountain sickness. The model's description of that passage ("on acute mountain sickness") is close enough, and the issue itself is founded. Not raised.
- **Section 8.** I re-verified ISS-01 to ISS-06 and ISS-08 to ISS-11 at their sources:
  - 8.2.6 criterion B (p. 124) and note 2 (p. 125);
  - NICE 1.3.9 and 1.3.39 without a review time point, 1.3.48, and the CG150 population sentence;
  - the [S-034] flowchart box (p. 52);
  - HURT with areas and no total score ([S-014]).

  No Stage 1 issue is silently worked around.
- **Settled points, not reopened (no new evidence):**
  - INV-091 to INV-093 with `concerns`;
  - INV-106 at MUST NOT;
  - the "> 3 months" readings of INV-045 and INV-089;
  - the E-041 window readings, timings, ages and `excludes` values;
  - the E-008 time frames;
  - one adherence window per comparison;
  - "treatment effect" by one item;
  - the 24-hour outcomes for cluster summaries;
  - the history of previous bouts;
  - the lead-in;
  - HADS subscales only;
  - the "baseline administration";
  - the MIDAS labels;
  - INV-023 at any granularity;
  - the OUT-031 end-of-bout Caveat without an annotation.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and no item of v18 carries a FROZEN marker.
