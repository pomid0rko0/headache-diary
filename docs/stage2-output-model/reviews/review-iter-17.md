# Review — iteration 17
VERDICT: REMARKS
REMARK_COUNT: 3
Reviewed version: v16
Date: 2026-10-21

## Summary

This is the main review of iteration 17: an independent fact-check and review of v16. `OUTPUT_MODEL.md` is byte-identical to `history/v16.md` (checked with `cmp`), and the working tree was clean at the start of this review.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 after OUT-025), and the source table of section 5;
- v16: sections 1–12, every element and every invariant;
- review 16, fix 16, and the oscillation check after iteration 16 with its eight watch points;
- the parts of earlier reviews and fixes that touch my topics: review 02 (R02-01, `fitsMonthlyPeriod`), review 05 ("Time points as period ends", checked and not raised), review 15 (R15-01, formulations), fix 15 (identifying-property table), and the searches for "previous bouts", the cluster 24-hour outcomes, the lead-in wording, the HADS total and the review window.

**Earlier decisions.** FROZEN_ITEMS.md does not exist, and no item of v16 carries a FROZEN marker. None of my remarks reverses an earlier fix or re-raises a remark a fixer declined. R17-01 concerns a point that review 05 examined and did not raise; the remark states what that examination did not consider. The relation of each remark to the watch points is stated in the remark.

**Result.**
- **Citations.** No defect. 465 quoted fragments were extracted by script. Every reachable fragment is verbatim at its stated location. [S-028] (richtlijnendatabase.nl) is still unreachable (maintenance page), as in review 16: 5 fragments, unchanged since v06.
- **Value sets, codes, labels, thresholds, metadata.** No defect.
- **Mechanical checks.** All pass.
- **Scope sweep.** No input, storage or derivation-from-input content.
- **Three remarks:**
  - **R17-01** (OUT-018, MUST): the relation `atTimePoint` places the end of the required on-treatment period one day after the treatment interval that the guidance names. This contradicts the model's own convention that the start date is a day on treatment. As a result, the comparison that Stage 1 itself describes does not meet INV-055 at most time points: the third consecutive month on treatment for "a minimum of 3 consecutive months", or the final 28 days of a 12-week treatment.
  - **R17-02** (OUT-023, OUT-024): the formulation that a treatment line or a treated-attack line states is tied to nothing. An output can state a formulation the subject never used, for example subcutaneous sumatriptan for an oral-only user, on which the EHF triptan-refractoriness definition turns.
  - **R17-03** (section 2): `outputOf` and `viewOf` are declared in a form that the notation does not define.

## Verification coverage

### Method

- **Downloads.** All were made with `curl` (through the configured proxy) into the fresh directory `/tmp/r17-dl-9ipL`, outside the repository.
  - **Stage 1 URLs, HTTP 200:**
    - PDFs: S-001 (211 pp.), S-002 (19), S-003 (18), S-005 (14), S-007 (39, UCL Discovery), S-008 (31), S-010 (11), S-016 (64), S-018 (12), S-030 (86), S-033 (92), S-034 (53; the first attempt was reset by the peer, the second succeeded), S-035 (92);
    - S-015: the Recommendations page and the Overview page.
  - **Europe PMC full-text XML (HTTP 200):** S-004 (PMC6501455), S-011 (PMC9188162), S-012 (PMC9555163), S-013 (PMC7296705), S-014 (PMC6734476), S-023 (PMC9607711), S-042 (PMC12279330), S-043 (PMC13169912), S-101 (PMC3057423), S-102 (PMC4406925), S-104 (PMC183845).
  - **New-source pages (HTTP 200):**
    - S-103 (the PedMIDAS grading table);
    - S-105 (9 pp.; metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014);
    - S-106: chapter 2, chapter 1 and the overview page.
  - **Unreachable:** S-028. Two direct requests returned HTTP 200 with the page "Deze pagina is tijdelijk niet bereikbaar". The Wayback availability API returned HTTP 429, and two Wayback fetches were reset by the peer.
- **Extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML and XML were stripped of scripts and markup, and entities were unescaped.
- **Read by eye after rendering with `pdftoppm`:**
  - ICHD-3 p. 190: the A1.1.1 and A1.1.2 windows "day 1 ± 2 (i.e. days −2 to +3)", whose "±", "−" and "+" have no text mapping, and note 2;
  - the S-034 title page, an image that reads "Возрастная группа" followed by "дети".
- **Scripts.** All are in the session scratchpad, `r17/`, and were run with `python3 -I`:
  - `quotes.py`: every double-quoted string outside `omn` blocks on a line with an `[S-NNN]` tag, split at `[...]` and "…", giving 465 fragments of at least 6 letters. Each fragment is searched in three normalisation passes (NFKC, quotes, dashes and whitespace; line-end hyphens; letters and digits only). The search goes first to the source of the nearest preceding tag, page by page, then to the other sources tagged on the line, then to Stage 1 v18. Every fragment not found was read in context;
  - `mech.py`: headings, references, traceability against the Realises fields, field counts, invariant levels and scopes, the prohibition form, attribute levels and the typing rule;
  - `names.py`: declarations and uses of names in `omn` blocks;
  - `tp.py`: the date arithmetic of R17-01;
  - `html2txt.py`.
- **Metadata.** PubMed esummary confirms:
  - S-101: Yang M, Rendas-Baum R, Varon SF, Kosinski M; Cephalalgia 2011;31(3):357–67; 10.1177/0333102410379890; PMC3057423;
  - S-102: Pavlović JM, Stewart WF, Bruce CA, Gorman JA, Sun H, Buse DC, Lipton RB; J Headache Pain 2015;16:24; 10.1186/s10194-015-0503-y; PMC4406925;
  - S-104: Snaith RP; HQLO 2003;1:29; 10.1186/1477-7525-1-29; PMC183845;
  - the PedMIDAS developer paper: PMID 11739822; 10.1212/wnl.57.11.2034;
  - S-106: "Published 27 June 2012", "Last reviewed: 11 January 2016".
- **Newer versions.**
  - **ICHD-3.** A web search finds no published ICHD-4, only work-in-progress papers and a September 2025 workshop report.
  - **NICE CG150.** The pages still show "Last updated: 03 June 2025". The Overview page now also shows "Last reviewed: 23 September 2026", with the note "We added links to relevant technology appraisal guidance in the section on treating and preventing migraine with or without aura". No recommendation text changed: 1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39 and 1.3.48 read as quoted.
  - **TA260.** Last reviewed 11 January 2016.
  - Nothing newer changes an element.

### Citations

"Source" means found verbatim in the downloaded source of the nearest tag. "Other tag" means found verbatim in another source tagged on the same line: these are fragments of that source in lines that cite several sources (E-041 Evidence and Notes, E-045 Evidence and Notes), and each was checked to be attributed to that source in the text. "Stage 1" means a fragment of a Stage 1 quote, checked against Stage 1 v18.

| Source (nearest tag) | Fragments | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 | 65 | 63. Source 56: labels pp. 8, 9, 12; 8.2–8.2.8 pp. 122–125; the 8.2.3 comment p. 123; Definitions of terms pp. 209–210; remission p. 209; A1.1 note 2 p. 190. Stage 1 4. By hand on the rendered p. 190, 3 (the A1.1.1 and A1.1.2 windows). The other 2 are search-log text. "Simple analgesics" occurs only on p. 139 (10.1.1 comments). | 0 | 0 |
| S-002, S-005 | 14 | 14: source 7, other tag 3, Stage 1 4 | 0 | 0 |
| S-007 IHS cluster | 10 | 10: source 8 (p. 10, section 2.2 item a; p. 22; p. 25), Stage 1 2 | 0 | 0 |
| S-008 IHS 2024 | 26 | 26: source 20 (Q2 pp. 5, 9; Q6 pp. 6, 12; Q6 Evidence p. 13; Q13 p. 17), other tag 5, Stage 1 1. By hand, 2 more fragments tagged S-014 and S-015 on their lines: "acceptable for treatment continuation beyond three months" and "for treatment continuation beyond three months", on p. 12, where a line break splits the phrase | 0 | 0 |
| S-010 IHS 2025 | 44 | 44: source 36 (p. 6: the four control levels, the migraine-day paragraph, the "proxy" sentence, the insufficient-control sentence, checked in its two parts around the running header), Stage 1 8 | 0 | 0 |
| S-011, S-014, S-016, S-018, S-023, S-030, S-032, S-042 | 84 | 83: source 58 (S-011 Background and question 3; S-014 HALT recall, units and Table 18 with its "≥20" row; S-016 PDF pp. 7, 20; S-018 pp. 1, 7, 8; S-023 "mindestens 50 %", "um mindestens 5 Punkte", "um mindestens 30 %", "sinkt"; S-030 PDF p. 19; S-042), other tag 12, Stage 1 13. The other 1 is the S-008 phrase above | 0 | 0 |
| S-015 NICE CG150 | 49 | 48: source 34 (1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48 and the Overview population sentence), other tag 2, Stage 1 12. The other 1 is the S-008 phrase above | 0 | 0 |
| S-028 NVN, S-029 | 13 | 8: Stage 1 7 (including the [S-028] Aanbeveling fragments of E-041), other tag 1. 1 is a translation | 0 | 4: the PICO sentence and the section name "Zoeken en selecteren", in E-041 and in the search log. 1 more echo, "kinderen en volwassenen", is counted under S-033. Tried as above |
| S-033 Russian adults | 45 | 40: source 20 (p. 1 title; p. 4 "М – мигрень"; pp. 39, 40, 41, 53), other tag 18, Stage 1 2. The remaining 4 are translations | 0 | 1 (the S-028 echo above) |
| S-034 Russian children | 20 | 16: source 8 (p. 17; p. 52 flowchart), other tag 2, Stage 1 4, and by hand on the rendered title page 2. The remaining 4 are translations | 0 | 0 |
| S-035 Turkish protocol | 50 | 37: source 33 (Kutu 8 p. 48, second and seventh items; 3.3 b p. 23; 3.6.3.9 p. 57; section 6 heading p. 77; chapter 7 heading; 7.1 p. 83; 7.3 p. 86, "2 k ez" as printed), other tag 4. The other 13 are translations | 0 | 0 |
| S-101 to S-106 | 49 | 32: S-101 "Data sources" 4; S-102 "Migraine-related disability" 7, plus 2 other tag; S-103 grading table 10; S-104 3, plus 1 Stage 1 fragment; S-105 P. 5/9–6/9 3; S-106 chapter 2 para. 2.1 and chapter 1, 4, plus 1 other tag. The remaining 17 are search-log queries and labels, and the labels of other MIDAS papers named in the E-057 Notes | 0 | 0 |
| **Total** | **465** | **421 verified**: 311 in the source of the nearest tag; 48 in another source tagged on the line; 55 as Stage 1 v18 fragments; 7 by hand (3 on the rendered ICHD-3 p. 190, 2 on the rendered S-034 title page, 2 S-008 phrases split by a line break). 22 more are translations and 17 search-log or note text | **0** | **5** (S-028) |

**Translations.** Every translation was read against the source text: the [S-033], [S-034] and [S-035] translations of E-041 and E-045, and the [S-028] PICO sentence. All are faithful. "uygulama süreleri uzatılabilir" ("the application intervals may be extended") is free but fits the context, and it supports no element (as review 16 noted).

### Value sets, codes, units, labels and thresholds

All were checked against the downloaded sources, and all are correct:
- ICHD-3 code labels (E-009; pp. 8, 9, 12);
- the 8.2 reference levels 10 and 15 with "for more than three months" (E-032; pp. 122–125);
- 8.2.6 criterion B (p. 124) and note 2 (p. 125); the 8.2.3 comment (p. 123);
- the A1.1 window and "there is no day 0" (E-060; rendered p. 190);
- remission "must exceed three months" (E-063, p. 209);
- HIT-6: 36–78, ≤49/50–55/56–59/60–78 and the four category labels;
- MIDAS: grades I–IV with the [S-102] labels, 0–5/6–10/11–20/≥21, three-month recall;
- PedMIDAS: 0–10/11–30/31–50/>50 with the labels "Little to none", "Mild", "Moderate", "Severe";
- HALT-90: 0–5/6–10/11–20/≥20 with the Table 18 labels; HALT-30 one month, no grading;
- HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21 (S-105 P. 5/9 and P.6/9, section "USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES");
- IHS Q6: 50 %, the 30 % chronic alternative, MIDAS ≥5 points for baseline 11–20 and ≥30 % for ≥20, HIT-6 ≥5;
- DMKG/ÖKSG/SKG: 50 %, 5 points, 30 %;
- NICE 1.3.28 (50/30 %), 1.3.29 (30 %, two cycles), the Russian 7.1 criterion (50 %);
- the IHS 2025 control levels;
- NICE 1.3.48: 4–8 weeks; TA260 re-treatment every 12 weeks.

The 18 rule constants of E-041 were checked against their quotes for offset, anchor, timing, headache type and ages, and the 6 criterion constants of E-045 for measure, threshold and condition. No value differs from its source. R17-01 concerns how a time point relates to a period's end date, not these values.

The day conventions of the other relations were checked as well: INV-045 (a span "more than three months", the shortest one being 4 calendar months or 4 × 28 days) and INV-089 (a remission that exceeds three months) are correct with `plusMonths` and inclusive `days`.

### Fidelity to Stage 1 (all 39 requirements)

| OUT | Result |
|---|---|
| 001 | Periods with dates and length at MUST (E-005, INV-002, INV-003); monthly frequency outputs (INV-014, INV-015, INV-108); comparisons of equal-length periods (INV-037); the Caveat by `lengthDays`. OK. For the comparison at evaluation time points (INV-055), see R17-01. |
| 002 | SHOULD labels in every reporting form (INV-008); ICHD-3 for headache days (INV-009). OK. |
| 003 | SHOULD indicator for every summarised period (INV-011, INV-012); SHOULD NOT cut-off (INV-013). OK. |
| 004–008 | Levels and conditions match (INV-014 to INV-017, INV-108; OUT-008 at MAY). OK. |
| 009 | Time course with markers in the view; weekly values where relevant (INV-034 to INV-036, INV-001). OK. |
| 010–013 | Intensity on a stated scale and compared between periods; duration with its label and the Caveat as SHOULD NOT; symptoms and the most bothersome symptom across periods and per attack; aura at MAY. OK. |
| 014–016 | Total, classes and drugs; the weekly view; the indicator with code, level, span and basis, the prompt at MUST and "not a diagnosis" at MUST NOT. OK. |
| 017 | Follow-up view with the review window, the year and the worsening label. OK. |
| 018 | Comparison, changes, 18 rules, and the Caveat at MUST NOT. **R17-01**: the required on-treatment period ends one day after the guidance interval, and the period that ends with the interval does not count. |
| 019 | Residual burden next to percentage changes (INV-060, INV-061). OK. |
| 020 | Label, criterion, values, decidable components, not the sole indicator, no continuation decision. OK. |
| 021 | MUST/SHOULD split; acute effectiveness per medication and period. OK. |
| 022 | Post-stop view with on-treatment and baseline periods. OK. |
| 023 | All named outcomes, timing, formulation, the baseline/on-treatment split, 15 minutes, the Caveat. **R17-02**: the formulation a treated-attack line states is not tied to a medication the subject has used, nor, outside single-formulation summaries, to the summary's formulations. |
| 024 | History with dates, dose changes, duration, response, adverse effects, stop reason and adherence. **R17-02**: the formulation of an acute line is tied to nothing. |
| 025 | MAY scheme windows. OK. |
| 039 | Adherence next to the comparison, in the history and in the clinician summary (`adherenceFor`). OK. |
| 026, 027 | Instrument results with value sets and change; functional impact with the baseline comparison. OK. |
| 028–030 | Three-month view; per-type outputs; menstrual-relation view. OK. |
| 031 | Bouts, remissions, rates, and 15-minute effectiveness per medication of the covered period. OK. |
| 032, 033 | Trigger view with caveats and dates in its period; screening results next to headache outputs. OK. |
| 034, 035 | All components; the v16 `courseNotOutside` tie of the overview's acute treatment effect is well typed and realises the fix-16 reading. OK. |
| 036–038 | Paediatric outputs; composite index; caveats. OK. |

### Mechanical checks (scripts, on v16)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), with no gaps and no duplicates. Every E- and INV- reference resolves. Issues ISS-01 to ISS-06 and ISS-08 to ISS-11; ISS-07 is referenced only as withdrawn (section 9). Every S reference lies in S-001–S-046 or S-101–S-106. Every OUT reference exists in Stage 1 (39 requirements). |
| Fields | Exactly one Realises and one Conformance field in every element and invariant. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025). For every OUT, the row's element and invariant sets equal the sets derived from the Realises fields. All rows say "full". |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Scopes: output 77, repertoire 32, context 1. All 10 MUST NOT / SHOULD NOT predicates begin with `¬`. |
| Attribute levels | 172 level-annotated declarations (core 94, MUST 29, SHOULD 47, MAY 2). The typing rule holds: every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. |
| Names in `omn` blocks | No duplicate declaration. Every capitalised name is declared, except the bound parameter `Ks`. Every applied lower-case name is a declared predicate, function or tag, a sequence application, `first`/`last`, or `refs` (section 2.5). **Declaration forms:** `outputOf` and `viewOf` use a form section 2.3 does not define (R17-03). |
| v16 change (by hand) | `courseNotOutside(c : OutputContext, t : Treatment, p : Period)` is applied to `ctx`, a member of `acuteTreatments : set Treatment`, and `v.covers` or `s.period : →Period`. `drugOf(t) = m.drug` is well typed. Precedence in INV-105 is as the Reading states: the antecedent disjunction is parenthesised, and the consequent closes before `∧ (menstruatesDuring …)`. No partial term. |

### Scope sweep

- **Grep.** I searched for enter/entry, record, input, captur-, logged, stor-, persist-, database, JSON/XML/CSV/FHIR/HL7, serializ-, encod-, retention, reminder, answer, data field, algorithm, "obtained from", "computed from" and "calculated from". The hits are:
  - the scope statements of sections 1, 2.1, 2.7 and 3.5;
  - the "obtained from diary information; how is out of scope" notes of E-014, E-019 and E-033;
  - the [S-014] HALT-30 quote ("records days affected");
  - the E-057 notes that scoring from answers is out of scope;
  - the INV-014 Reading ("can be answered");
  - the INV-076 note.

  All are legitimate.
- **Relations.** Every relation takes only output elements, constants and context properties as arguments. The changes proposed in R17-01 and R17-02 do as well.
- **Thresholds and formulas.** Every threshold, reference level, score band and offset that is part of the output data is present with its quote. No missing threshold or formula was found.

## Remarks

### R17-01 Formal defect: an evaluation time point is related to the end of an on-treatment period one day late, so INV-055 (MUST) does not accept the comparison that ends with the treatment interval the guidance names

- Item(s):
  - E-042 (`atTimePoint`, `fitsMonthlyPeriod`, Meaning);
  - INV-055 (Reading, Notes and satisfiability argument);
  - INV-058 (only if option (b) is chosen);
  - E-041 Meaning (the sentences on `atOffset`, `atLeastOffset` and `withinWindow`) and the E-041 Notes sentence on time points less than 28 days after the start;
  - E-043 Notes (the same sentence);
  - E-008 (`cycleEnd`: the meaning of its date);
  - section 7, row OUT-018.
- Problem:
  - **The model counts the start date as a day on treatment.**
    - An on-treatment period may begin on the treatment start (INV-056: `rc.treatmentStart ≤ p.start`).
    - A course's duration counts both its first and its last day (INV-079: `d = daysLong(days(s, e))`; INV-079 Notes).
    - So n weeks of treatment are the days s to `plusDays(s, 7n − 1)`, and n months of treatment end on the day before `plusMonths(s, n)`. For example, a course from 1 January to 25 March 2026 has a duration of 84 days, 12 weeks.
  - **The time point falls on the day after that interval, and the period must end on it.**
    - `earliest = shift(anchorDate, minOffset)` (INV-058) is `plusDays(s, 7n)` or `plusMonths(s, n)`: the first day after the interval.
    - `atTimePoint` then requires `p.end = tp.earliest` (for `atOffset` and `atLeastOffset`) or `tp.earliest ≤ p.end` (for `withinWindow`).
    - So the on-treatment period that INV-055 requires always contains one day outside the treatment interval that the guidance names ("after 12 weeks of treatment", "a minimum of 3 consecutive months on treatment", "через 3 месяца терапии", "3 to 6 months after starting").
  - **The period that ends with the interval never meets a time point of an `atOffset` or `atLeastOffset` rule, nor the earliest date of a window rule.** This is the comparison Stage 1 itself describes:
    - **Calendar months.** For an anti-CGRP monoclonal antibody started on 1 January, the third consecutive month on treatment, March, is the comparison of OUT-018's own example ("after a minimum of 3 consecutive months for anti-CGRP monoclonal antibodies"). It meets none of the 3-month time points: EHF question 3, IHS Q2 for monthly injectables, the Russian section 7.1 and NICE 1.3.27. INV-055 instead requires an on-treatment period that ends on 1 April, which no calendar month can do. A diary that reports response comparisons per calendar month, as OUT-001 permits ("per calendar month or per 28-day (4-week) period"), therefore fails the MUST of INV-055 for such a treatment, although it shows exactly the comparison that the guidance names.
    - **28-day periods.** The period that the Stage 1 evidence names, "the final 28 days of the treatment period" ([S-005], Stage 1 OUT-001 and OUT-036), never meets the time point. For NICE 1.3.28 ("after 12 weeks of treatment"), with a start on 1 January, the final 28 days of the 12 weeks are 26 February to 25 March. INV-055 requires 27 February to 26 March.
    - **The model's own guard.** `fitsMonthlyPeriod` states that a 28-day period beginning on the start "ends no earlier than 27 days after s". That period covers exactly the first 4 weeks of treatment, but it would not meet a 4-week time point (`plusDays(s, 28)`).
  - **The cycle-end anchors use the other convention, or an unstated one.**
    - E-042 calls the anchor date of NICE 1.3.29 and Turkish 3.6.3.9 and 7.3 "the end of a treatment cycle". E-008 does not say whether a `cycleEnd(n)` event is dated on the last day of the cycle or on the day after it.
    - On the natural reading (the last day of the cycle), the required period for "after 2 treatment cycles" ends with the interval, while the period for "after 12 weeks of treatment" ends one day after it. The two kinds of rule then follow opposite conventions.
  - **Relation to earlier loop files.**
    - Review 05 noted ("Time points as period ends") that `atTimePoint` makes a period end on `shift(anchor, offset)`. It did not raise this, because "Stage 1 fixes no day convention, and INV-055 remains satisfiable with 28-day periods".
    - That examination checked only satisfiability. It did not consider:
      - that the model does fix a convention (INV-056, INV-079), with which the time-point relation disagrees;
      - that INV-055 then rejects the comparisons that Stage 1 and its evidence name (the third consecutive month on treatment; the final 28 days of the treatment period);
      - the cycle-end anchors.
    - No fixer declined a remark on this, and no earlier fix is reversed.
    - **Watch point 5 (E-041).** The required change touches no `excludes` value, `timing`, `ages`, `AgeCoverage` value or anchor of any rule. A uniform one-day shift changes no comparison between time points of one guidance, so the `excludes` criterion gives the same values.
    - **R02-01.** The `fitsMonthlyPeriod` guard is kept and only re-expressed in the same convention.
- Evidence:
  - E-042: `pred atTimePoint(p : Period, tp : EvaluationTimePoint) ≙ (tp.rule.timing ∈ {atOffset, atLeastOffset} ⇒ p.end = tp.earliest) ∧ (tp.rule.timing = withinWindow ⇒ tp.earliest ≤ p.end ∧ ∀ l ∈ tp.latest • p.end ≤ l)`.
  - INV-058: `tp.earliest = shift(tp.anchorDate, tp.rule.minOffset)`. E-041: `shift(d, weeks(n)) = plusDays(d, 7 × n) ∧ shift(d, months(n)) = plusMonths(d, n)`. Section 2.8: `plusMonths` gives "the date with the same day of the month n calendar months later".
  - INV-056: `(∀ p ∈ ran rc.onTreatment • rc.treatmentStart ≤ p.start)`. INV-079: `d = daysLong(days(s, e))`, with `days` counting "both the first and the last day" (INV-079 Notes; section 2.8).
  - E-042 Meaning: "`fitsMonthlyPeriod(s, a, r)` holds when a calendar month or 28-day period that begins on or after the treatment start s can end at the time point of rule r anchored at a [...]: such a period has at least 28 days (E-005), so it ends no earlier than 27 days after s."
  - Stage 1 OUT-018: "after a minimum of 3 consecutive months for anti-CGRP monoclonal antibodies"; [S-011] "we suggest evaluating efficacy after a minimum of 3 consecutive months on treatment"; [S-015] "Stop CGRP inhibitors after 12 weeks of treatment"; [S-015] "Review the need for continuing migraine prophylaxis 3 to 6 months after starting prophylactic treatment."
  - Stage 1 OUT-001 and OUT-036, [S-005]: "The time periods for analyses of efficacy should be equivalent. Thus, if a baseline period is 28 days, the final 28 days of the treatment period should be assessed."
  - **Computed (`tp.py`).** An adult with migraine, an anti-CGRP monoclonal antibody (types `antiCGRPMonoclonalAntibody`, `monthlyInjectable`, `cgrpInhibitor`), start event on 1 January 2026, as-of date 15 April 2026. Baseline December 2025 and on-treatment March 2026, both calendar months of 31 days, so the lengths are equal. Whether March meets `atTimePoint`:
    - `ruleEhf2022Q3`: earliest 1 April; March ends 31 March; **no**. The required period is 5 March – 1 April.
    - `ruleIhsQ2Monthly`, `ruleRu71`: the same, **no**.
    - `ruleNice1327`: window 1 April – 1 July; **no**.
    - `ruleNice1328`: 26 March; **no**. The final 28 days of 12 weeks are 26 February – 25 March; the required period is 27 February – 26 March.
    - `ruleTrBox8`: window 1 March – 1 April; yes.
- Required change: make the relation between a time point and the end of the on-treatment period agree with the model's own counting of treatment days, so that a period that ends on the last day of the interval the guidance names (n weeks or n months of treatment from the anchor day, or the named treatment cycles) meets the time point. Use one convention for all anchors. Options:
  - **(a)** Keep the time point as the date on which the evaluation falls, the first day after the interval (as now for start and dose anchors, and as INV-051 does for the NICE 1.3.48 review window). Relate the period to it by its last day:
    - `next(p.end) = tp.earliest` for `atOffset` and `atLeastOffset`;
    - `tp.earliest ≤ next(p.end) ∧ ∀ l ∈ tp.latest • next(p.end) ≤ l` for `withinWindow`;
    - `fitsMonthlyPeriod` correspondingly with `plusDays(s, shortestMonthlyDays) ≤ …`;
    - state that the date of a `cycleEnd(n)` event is the first day after cycle n, the day by which the cycle is complete.
  - **(b)** Make the time point the last day of the interval: `earliest` (and `latest`) one day before `shift(…)` for the start and dose anchors (INV-058, E-042), keep `atTimePoint`, and state that a `cycleEnd(n)` event is dated on the last day of cycle n.

  In either case:
  - align the E-041 Meaning, the E-042 Meaning, the INV-055 Reading, Notes and satisfiability argument, the E-043 Notes and row OUT-018;
  - keep every E-041 value.

  Satisfiability is unchanged in substance: for a time point that fits, a 28-day on-treatment period ending on the last day of the interval begins on or after the start, and a 28-day baseline ending before the start has the same length.

### R17-02 Formal defect: the formulation that a treatment line or a treated-attack line states is not tied to a formulation the subject has used, so an output can state a formulation the subject never took

- Item(s):
  - E-055 `formulations` with INV-079 (and INV-109);
  - E-053 `formulation` with INV-074 (or INV-075);
  - optionally E-051 `formulations` with INV-074;
  - the Notes of E-051 and E-055;
  - section 7, rows OUT-023 and OUT-024.
- Problem:
  - Every other fact a treatment line shows is tied to the subject's treatment course (INV-079): its start, stop, dose changes, drug, response and adherence. The formulation of an acute line, which OUT-024 asks for, is tied to nothing: `formulations : set FormulationOrRoute SHOULD when self.role = acute` is met by any non-empty set.
  - The formulation of a treated-attack line (E-053) is tied to the summary's formulation only inside a single-formulation summary (INV-074: `s.formulationScope = singleFormulation ⇒ ∀ f ∈ l.formulation • f ∈ s.formulations`). In a summary of all formulations, a line may state any formulation, including one that the summary itself does not name.
  - The context holds exactly the fact needed: `acuteMedications` is "every acute medication (drug and formulation) the subject has used at any time up to the as-of date" (E-008). Every acute course and every treated attack lies on or before that date, so any formulation it was taken in is a formulation of its drug in that set. The tie is a relation over output elements and context properties only, like INV-036 and INV-079.
  - This is not the R15-01 question.
    - R15-01 and `summarisesMedication` concern which summaries are required: every used formulation is covered by a summary shown. R15-01's examples were 0-attack summaries, which the model treats as correct values (E-008 Meaning).
    - This remark concerns the truth of a stated fact: that the patient took the drug in a given formulation.
    - It decides neither reading of OUT-023 (watch point 3: "It must keep a condition that implies `summarisesMedication`"). It keeps `summarisesMedication`, and it loosens no tie of R13-01, R14-02, R15-01 or R16-01.
  - The stated formulation matters for the purpose Stage 1 gives. OUT-024 asks for the formulation "so that different formulations of the same drug can be told apart and the EHF definition of triptan refractoriness [S-012] can be applied", and that definition turns on the subcutaneous formulation.
- Evidence:
  - E-055: `formulations : set FormulationOrRoute  SHOULD when self.role = acute`. INV-079 has no conjunct on `l.formulations`, and nor does any other invariant (`grep` of the `omn` blocks: the only formulation constraints are `summarisesMedication`, INV-071, INV-072 for summaries of all formulations, and INV-074 for single-formulation summaries).
  - INV-074: `(∀ l ∈ ran s.sequence • l.drug = s.drug ∧ inPeriod(l.onset, s.period) ∧ (s.formulationScope = singleFormulation ⇒ ∀ f ∈ l.formulation • f ∈ s.formulations))`.
  - Stage 1 OUT-024: "For acute treatments, the list SHOULD also show the formulation of each treatment (see OUT-023), so that different formulations of the same drug can be told apart and the EHF definition of triptan refractoriness [S-012] can be applied."
  - Stage 1 OUT-024, [S-012]: "failure to subcutaneous triptans was considered mandatory for the definition of triptan refractoriness as subcutaneous formulations have the fastest absorption".
  - Stage 1 OUT-023: "The output SHOULD also state the formulation or route of administration (for example oral or subcutaneous) of each acute medication it summarises".
  - **Example admitted by v16.**
    - Setting:
      - a subject with migraine; one acute course, sumatriptan, started 10 January 2025 and ongoing;
      - `acuteMedications = {(sumatriptan, oral)}`, which satisfies the INV-001 link;
      - as-of date 20 October 2026.
    - Its treatment history view shows one acute class group ("triptans") with one line:
      - drug sumatriptan, start date 10 January 2025, duration to date;
      - `formulations = {subcutaneous}`;
      - as its response summary, a summary of all formulations of sumatriptan over all headache types, of 10 January 2025 – 20 October 2026, with `formulations = {oral, subcutaneous}`;
      - treated-attack lines that state the formulation `subcutaneous`.
    - These all hold: INV-072 (oral is named), INV-074 (drug and period; the formulation conjunct does not apply to a summary of all formulations), INV-078, INV-079, INV-109 (`summarisesMedication(s, (sumatriptan, oral))` holds through `allFormulations`; the course span), INV-073, INV-003 and INV-011.
    - The history tells the reader that this patient used subcutaneous sumatriptan, which the patient never used.
- Required change: tie each stated formulation to the subject's acute medications of the same drug, and a treated-attack line's formulation to the formulations its summary states.
  - **INV-079**, for acute lines: `l.role = acute ⇒ ∀ f ∈ l.formulations • AcuteMedication(drug ↦ l.drug, formulation ↦ f) ∈ ctx.subject.acuteMedications`.
  - **INV-074 (or INV-075)**, for treated-attack lines: `∀ f ∈ l.formulation • AcuteMedication(drug ↦ l.drug, formulation ↦ f) ∈ ctx.subject.acuteMedications`. Also require `f ∈ s.formulations` for the lines of every summary, not only single-formulation ones. With INV-072, the context tie already implies this for a summary of all formulations.
  - **Optionally**, for summaries: `∀ f ∈ s.formulations • AcuteMedication(drug ↦ s.drug, formulation ↦ f) ∈ ctx.subject.acuteMedications`. With INV-072, a summary of all formulations then names exactly the formulations of its drug that the subject has used.
  - Align the E-051 and E-055 Notes and rows OUT-023 and OUT-024.
  - **Satisfiability.**
    - The drug of every acute course is the drug of an acute medication (INV-001), so a non-empty `formulations` of an acute line can always be chosen.
    - The single-formulation summaries required by INV-071 and through `summarisesMedication` name `{m.formulation}`, with m an acute medication.
    - A summary of all formulations names the used formulations, as INV-072 already requires.
    - A treated attack was treated with a medication the subject has used.

### R17-03 Formal defect: `outputOf` and `viewOf` are declared in a form that the notation does not define

- Item(s): E-002 (`fun outputOf(x : Element) : Output`); E-003 (`fun viewOf(x : Item) : View`); section 2.3.
- Problem:
  - Section 2.3 defines two forms of function declaration:
    - `fun f : T₁ × … × Tₙ → T`, a given function;
    - `fun f(x₁ : T₁, …, xₙ : Tₙ) : T ≙ e`, a defined function.
  - The two declarations use the parameter-list form without `≙ e`, which is neither. Section 2.10 makes well-typedness depend on every name being declared, and these are the only two declarations of the model in an undefined form (checked over all 40 `fun` declarations).
  - Their meaning is stated only in the prose of section 2.5 ("`outputOf(x)` is the output an atom belongs to [...] and `viewOf(x)` is the view an item is part of").
  - Both functions are used in many invariants, for example INV-007, INV-054, INV-059, INV-060, INV-062, INV-072 and E-032 `classUseExcluded`.
- Evidence:
  - E-002: `fun outputOf(x : Element) : Output   -- the output an element belongs to (an output belongs to itself)`.
  - E-003: `fun viewOf(x : Item) : View`.
  - Section 2.3: "`fun f : T₁ × … × Tₙ → T` declares a **given total function** [...]. `fun f(x₁ : T₁, …, xₙ : Tₙ) : T ≙ e` declares a **defined function**."
  - Every other `fun` declaration of the model uses one of the two forms.
- Required change: declare both in a defined form. Options:
  - (a) Declare them as given functions, `fun outputOf : Element → Output` and `fun viewOf : Item → View`, with their meaning (the composition of section 2.5) in the comment, as the model does for the given functions `ctx` and `parts` (section 3.2). An `axiom` is not suitable, because section 2.3 lets an axiom refer to no output element.
  - (b) Define them with `≙` in terms of `views` and `content`. This needs a definite-description term ("the v with x ∈ v.content") that section 2.6 would have to add.
  - (c) Add the parameter-list form without body to section 2.3 as a given function with named parameters.

## Checked and not raised

- **The v16 change (R16-01).** `courseNotOutside` is well typed, takes only context properties and output periods, and equals `courseOverlaps` for a course with a stated start. The INV-105 antecedent narrows and its consequent strengthens relative to v15, as fix 16 states. Watch points 1 and 2 hold: `allTypes`, `within`, `summarisesMedication`, `courseOverlaps` and `courseNotOutside` are all present; E-008 is unchanged; E-062 `acute` and E-045 `valueAvailable` still use `acuteMedications ≠ ∅`, and I raise nothing on them.
- **The follow-up year of INV-049** (`c.timeRange.to ≤ plusMonths(ws, followUpMonths)`). This bound admits a time range one day longer than the year after the start of withdrawal. It only widens an availability requirement by one day and excludes no output, so it is immaterial. The NICE 1.3.48 window of INV-051 (the review falls 4 to 8 weeks after the start) is correct as dates of review.
- **`namedCriteria`** is declared but used by no invariant, and the Turkish Box 8 criterion is described in the E-045 Notes but has no constant. A responder label may name any criterion (OUT-020 "for example"), so nothing is missing.
- **`isWeekSpan`** is one given function, while its comment speaks of "the week convention of the output". Within one repertoire the convention is fixed, and no Stage 1 property depends on it.
- **HURT recall.** [S-014] gives HURT item recalls of 1 or 3 months. The model tabulates no HURT recall and shows recall as published. Correct.
- **Value sets** of HIT-6, MIDAS, PedMIDAS, HALT, HADS, PHQ-9 and GAD-7, and the PubMed metadata of S-101 to S-104: all correct (Verification coverage).
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded. I re-verified:
  - 8.2.6 criterion B (p. 124);
  - "simple analgesics" only on p. 139, in the 10.1.1 comments, next to the acute mountain sickness passage;
  - NICE 1.3.9 and 1.3.39 without a review time point;
  - 1.3.48 and the CG150 population sentence;
  - the [S-034] flowchart (p. 52).

  No Stage 1 issue is silently worked around. R17-01 to R17-03 concern the model, not Stage 1.
- **Settled points, not reopened (no new evidence):**
  - the 24-hour outcomes for cluster summaries (reviews 01–14);
  - "the history of previous bouts" (review 01, fix 11);
  - the E-060 lead-in wording on diary information (review 05);
  - HADS subscales only (review 05);
  - the review window of OUT-017 shown as a period (reviews 06, 11, 12);
  - INV-060 with INV-061 for compared periods shorter than 28 days;
  - the monthly baseline;
  - INV-023 at any granularity;
  - the "> 3 months" readings of INV-045 and INV-089;
  - the MIDAS labels and the HIT-6 recall;
  - the "baseline administration";
  - INV-091 to INV-093 with `concerns`;
  - "treatment effect" by one item;
  - the E-041 window readings, timings, ages and `excludes` values;
  - INV-087 and the lead-in;
  - INV-049 and INV-050;
  - the E-008 time frames;
  - one adherence window per comparison;
  - the periods of the overview's response comparison;
  - INV-068's periods.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and no item of v16 carries a FROZEN marker.
