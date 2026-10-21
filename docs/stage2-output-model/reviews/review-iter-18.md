# Review — iteration 18
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v17
Date: 2026-10-21

## Summary

This is the main review of iteration 18: an independent fact-check and review of v17. `OUTPUT_MODEL.md` is byte-identical to `history/v17.md` (checked with `cmp`). The working tree was clean at the start.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 after OUT-025), and the source table of section 5;
- v17: sections 1–12, every element and every invariant;
- review 17 and fix 17;
- the oscillation check after iteration 16, with its eight watch points;
- the watch points of the check after iteration 12;
- the parts of earlier reviews and fixes that touch my topic: fix 05 (the start tie of INV-064) and review 15 ("Several stop events in one course").

**Earlier decisions.**
- FROZEN_ITEMS.md does not exist, and no item of v17 carries a FROZEN marker.
- My remark re-raises nothing a fixer declined, and it reverses no earlier fix. A `grep` of `reviews/`, `fixes/` and `oscillation/` finds no discussion of evaluation time points, or of responder labels, for a preventive course that stopped before the evaluated period.
- How the remark relates to the watch points is stated in the remark.

**Result.**
- **Citations.** No defect. 475 quoted fragments were extracted by script, and every fragment is verbatim at its stated location.
  - [S-028] (richtlijnendatabase.nl), unreachable in reviews 16 and 17, returned the module page today. All its fragments, and the section "Zoeken en selecteren" of the PICO sentence, were verified.
- **Value sets, codes, labels, thresholds, metadata.** No defect.
- **Mechanical checks.** All pass.
- **Scope sweep.** No input, storage or derivation-from-input content.
- **One remark:**
  - **R18-01** (OUT-018 MUST, OUT-020): the model does not bound "on treatment" by the stop or pause of the course. As a result:
    - INV-055 and INV-059 (MUST) require guidance evaluation time points, and comparisons "at" them, for a preventive course that was stopped or paused before the treatment interval those time points close. For example, they require the "3 consecutive months on treatment" time point of a monoclonal antibody stopped after 6 weeks, compared on a month in which no treatment was taken.
    - INV-063 and INV-064 let a responder or control-level label classify months after the stop as the treatment's response.

## Verification coverage

### Method

- **Downloads.** All downloads were made with `curl` (through the configured proxy) into the fresh directory `/tmp/r18-dl-rUTh`, outside the repository.
  - **Stage 1 URLs, all HTTP 200:**
    - PDFs: S-001 (211 pp.), S-002 (19), S-003 (18), S-005 (14), S-006 (16), S-007 (39, UCL Discovery), S-008 (31), S-010 (11), S-016 (64), S-018 (12), S-030 (86), S-033 (92; the first attempt was reset by the peer, the retry succeeded), S-034 (53), S-035 (92);
    - S-015: the CG150 Recommendations page and the Overview page;
    - S-028: the NVN module page.
  - **Europe PMC full-text XML, all HTTP 200:** S-004, S-011, S-012, S-013, S-014, S-023, S-042, S-043, S-101 (PMC3057423), S-102 (PMC4406925), S-104 (PMC183845).
  - **New-source pages, all HTTP 200:**
    - S-103: the Cincinnati Children's PedMIDAS page;
    - S-105: the 9-page manual PDF;
    - S-106: TA260 overview, chapter 1 and chapter 2.
- **Extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML and XML were stripped of scripts and markup, and entities were unescaped.
- **Read by eye after rendering with `pdftoppm`:**
  - ICHD-3 p. 190: the A1.1.1 and A1.1.2 windows "day 1 ± 2 (i.e. days −2 to +3)", whose "±" and "−" glyphs have no text mapping, and note 2;
  - the S-034 title page, an image that reads "Возрастная группа" followed by "дети".
- **Scripts.** All are in the session scratchpad, `r18/`, and were run with `python3 -I`:
  - `totext.py`: per-page text;
  - `quotes.py`: extracts every double-quoted string outside `omn` blocks on a line with an `[S-NNN]` tag, split at `[...]` and "…", keeping fragments of at least 6 letters. It searches each fragment with three normalisations: NFKC, quotes and dashes; line-end hyphens; letters and digits only. The search order is the source of the nearest preceding tag, then the other sources tagged on the line, then Stage 1 v18;
  - `where.py`: every page on which a fragment occurs, to check the stated pages;
  - `mech.py`, `names.py`: the mechanical checks;
  - `stopped.py`: the date arithmetic of R18-01.
- **Metadata.**
  - PubMed esummary confirms the citations of S-101 (PMID 20819842), S-102 (PMID 25902814), S-104 (PMID 12914662) and the PedMIDAS developer paper (PMID 11739822): authors, journal, year, volume, pages, DOI and PMCID as in section 10.
  - S-105 PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
  - S-106: "Published: 27 June 2012", "Last reviewed: 11 January 2016"; recommendation 1.2 and paragraph 2.1 read as quoted.
- **Newer versions.**
  - **ICHD-3.** A web search finds no published ICHD-4. The IHS pages still call ICHD-4 work in progress.
  - **NICE CG150.** The page still shows "Last updated: 03 June 2025". The Overview also shows "Last reviewed: 23 September 2026", with links to technology appraisals added. Recommendations 1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39 and 1.3.48 read as quoted.
  - Nothing newer changes an element.

### Citations

"Source" means found verbatim in the downloaded source of the nearest tag. "Other tag" means found in another source tagged on the same line, in the multi-source lines of E-041, E-045, E-057 and the logs; each was read in context and is attributed there to the source in which it was found. "Stage 1" means a fragment of a Stage 1 quote, checked against Stage 1 v18.

| Source (nearest tag) | Fragments | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 | 65 | 64. Source 57: labels on pp. 8, 9 and 12; 8.2–8.2.8 on pp. 122–125; the 8.2.3 comment on p. 123; the remission on p. 209; Definitions of terms on pp. 209–210. Stage 1 4. By eye on the rendered p. 190, 3. The other 1 is a search-log row label. "Simple analgesics" occurs only on p. 139 (10.1.1 comments). | 0 | 0 |
| S-002, S-005, S-007 | 30 | 30: source 17, other tag 7, Stage 1 6. S-005: "the final 28 days of the treatment period" on PDF p. 8 (printed p. 810). S-007: "≥ 14 attacks per week on average" on p. 10. | 0 | 0 |
| S-008 IHS 2024 | 26 | 26: source 20 (Q2 p. 9; Q6 p. 12; Q6 Evidence p. 13; Q13 p. 17), other tag 6. Two further S-008 phrases, counted under the S-014 and S-015 tags of their lines ("acceptable for treatment continuation beyond three months", "for treatment continuation beyond three months"), were found by hand on p. 12 (also p. 6). | 0 | 0 |
| S-010 IHS 2025 | 44 | 44: source 36 (p. 6: the four control levels, the migraine-day paragraph, the "proxy" sentence, the insufficient-control sentence in its two parts), Stage 1 8 | 0 | 0 |
| S-011, S-012, S-014, S-016, S-018, S-023, S-029, S-030, S-032, S-042 | 84 | 84: source 60 (S-011 Background and question 3; S-014 HALT recall, units and Table 18 with its "≥20" row; S-016 PDF p. 7; S-018 pp. 1, 7, 8; S-023; S-030 PDF p. 19; S-042), other tag 10, Stage 1 13, and 1 by hand (the S-008 phrase above) | 0 | 0 |
| S-015 NICE CG150 | 51 | 51: source 36 (1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48, the "Prophylactic treatment review" heading and the Overview population sentence), other tag 2, Stage 1 12, and 1 by hand (the S-008 phrase above) | 0 | 0 |
| S-028 NVN | 12 | 11: source 10, including the PICO sentence under "Zoeken en selecteren" and the Aanbeveling, which has titration schedules "BIJ KINDEREN" and "BIJ VOLWASSENEN"; other tag 1. The other 1 is a translation. | 0 | 0 (reachable again today) |
| S-033 Russian adults | 45 | 41: source 20 (p. 1 title; p. 4 "М – мигрень"; pp. 39, 40, 41, 53; the en dash of "БТА – минимум" is in the text layer), other tag 21. The other 4 are translations. | 0 | 0 |
| S-034 Russian children | 20 | 16: source 8 (p. 17; p. 52 flowchart), other tag 2, Stage 1 4. By eye on the rendered title page, 2 more. The other 4 are translations. | 0 | 0 |
| S-035 Turkish protocol | 50 | 37: source 33 (Kutu 8, p. 48, second and seventh items; 3.3 b, p. 23; 3.6.3.9, p. 57; section 6 heading, p. 77; chapter 7 heading, p. 82; 7.1, p. 83; 7.3, p. 86, "2 k ez" as printed), other tag 4. The other 13 are translations. | 0 | 0 |
| S-101 to S-106 | 48 | 33: S-101 "Data sources", 4; S-102 "Migraine-related disability", 7, plus other tag 2; S-103 grading table, 8; S-104, 3, plus Stage 1 1; S-105 P. 6/9 and P. 8/9, 3; S-106 paragraph 2.1 and overview, 3, plus other tag 1. By hand, TA260 recommendation 1.2 ("less than a 30% reduction in headache days per month after 2 treatment cycles"), cited in the change log, verbatim in chapter 1: 1 more. The remaining 15 are search-log queries, and labels of other MIDAS papers named in the E-057 Notes. | 0 | 0 |
| **Total** | **475** | **437 verified**: 325 in the source of the nearest tag; 56 in another source tagged on the line; 48 as Stage 1 v18 fragments; 8 by hand (3 on the rendered ICHD-3 p. 190, 2 on the rendered S-034 title page, 2 S-008 phrases, 1 TA260). The remaining 38 are 22 translations and 16 search-log or row-label texts. | **0** | **0** |

**Translations.** Every translation was read against the original in context: the [S-033], [S-034] and [S-035] translations of E-041 and E-045, the [S-028] PICO sentence, and the [S-034] flowchart box in ISS-10. All are faithful.

### Value sets, codes, units, labels and thresholds

All were checked against the downloaded sources, and all are correct:
- ICHD-3 code labels (E-009; pp. 8, 9, 12);
- the 8.2 reference levels 10 and 15 with "for more than three months" (E-032; pp. 122–125);
- 8.2.6 criterion B (p. 124) and note 2 (p. 125);
- the A1.1 window and "there is no day 0" (E-060; rendered p. 190);
- remission "must exceed three months" (E-063; p. 209);
- HIT-6: 36–78, the bands ≤49 / 50–55 / 56–59 / 60–78 and their four labels;
- MIDAS: grades I–IV with the [S-102] labels, the bands 0–5 / 6–10 / 11–20 / ≥21, and the three-month recall;
- PedMIDAS: the bands 0–10 / 11–30 / 31–50 / >50 with their four labels;
- HALT-90: the bands 0–5 / 6–10 / 11–20 / ≥20 with the Table 18 labels; HALT-30: one-month recall and no grading;
- HADS: 0–21 per subscale; PHQ-9: 0–27; GAD-7: 0–21;
- IHS Q6: the 50 % criterion, the 30 % chronic alternative, MIDAS ≥5 points for baseline 11–20 and ≥30 % for baseline ≥20, HIT-6 ≥5 points;
- DMKG/ÖKSG/SKG: 50 %, 5 points, 30 %;
- NICE 1.3.28 (50 % / 30 %) and 1.3.29 (30 %, two cycles); the Russian section 7.1 criterion (50 %);
- the IHS 2025 control levels;
- NICE 1.3.48: 4–8 weeks; TA260: re-treatment every 12 weeks.

The 18 rule constants of E-041 and the 6 criterion constants of E-045 match their quotes. R18-01 does not concern these values.

**Date examples of the v17 text, recomputed:**
- **E-042 and INV-055.** For a start on 1 January 2026:
  - the 3-month time point is 1 April, and March ends on 31 March;
  - 1 January + 84 days is 26 March;
  - 26 February to 25 March is 28 days, and 4 to 31 December 2025 is 28 days.
- **INV-049 Notes.** 10 March + 27 days is 6 April. 21 April is day 43, within the NICE window of 7 April to 5 May.
- **E-007.** 15 August to 20 October is 67 days.

All are correct.

### Fidelity to Stage 1 (all 39 requirements)

| OUT | Result |
|---|---|
| 001 | Periods with dates and length at MUST (E-005, INV-002, INV-003); frequency outputs per month or 28-day period (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); the Caveat through `lengthDays`. OK. |
| 002 | SHOULD definition labels in every reporting form (INV-008); ICHD-3 for headache days (INV-009). OK. |
| 003 | SHOULD indicator for every summarised period (INV-011, INV-012); SHOULD NOT cut-off (INV-013). OK. |
| 004–008 | Levels and conditions match (INV-014 to INV-017, INV-108; OUT-008 at MAY). OK. |
| 009 | Time course with markers in the view; weekly values where relevant (INV-034 to INV-036, INV-001). OK. |
| 010–013 | Intensity on a stated scale and compared between periods; duration with its label, and the Caveat as SHOULD NOT; symptoms and the most bothersome symptom across periods and per attack; aura at MAY. OK. |
| 014–016 | Total, classes and drugs; the weekly view; the indicator with code, level, span and basis, the prompt at MUST and "not a diagnosis" at MUST NOT. OK. |
| 017 | Follow-up view with the review window, the year (v17 bound checked) and the worsening label. OK. |
| 018 | Comparison, changes, 18 rules, the v17 day convention, and the Caveat at MUST NOT. **R18-01**: the time points, and the MUST comparisons at them, are required for a course stopped or paused before the treatment interval that the guidance names. |
| 019 | Residual burden next to percentage changes (INV-060, INV-061). OK. |
| 020 | Label, criterion, values, decidable components, not the sole indicator, no continuation decision. **R18-01**: a label may classify months after the stop of its course as the treatment's response. |
| 021 | MUST/SHOULD split; acute effectiveness per medication and period. OK. |
| 022 | Post-stop view: v17 `firstChangedDay`; on-treatment period and baseline. OK. |
| 023 | All named outcomes, timing, formulation (v17 ties in INV-074, INV-075), the baseline/on-treatment split, 15 minutes, the Caveat. OK. |
| 024 | History with dates, dose changes, duration, response, adverse effects, stop reason, adherence, and formulation tied to used formulations (INV-079). OK. |
| 025 | MAY scheme windows. OK. |
| 039 | Adherence next to the comparison, in the history and in the clinician summary (`adherenceFor`). OK. |
| 026, 027 | Instrument results with value sets and change; functional impact with the baseline comparison. OK. |
| 028–030 | Three-month view; per-type outputs; menstrual-relation view. OK. |
| 031 | Bouts, remissions, rates, and 15-minute effectiveness per medication of the covered period. OK. |
| 032, 033 | Trigger view with its caveats and its dates in its period; screening results next to headache outputs. OK. |
| 034, 035 | All components; INV-104 and INV-105 unchanged since v16. OK. |
| 036–038 | Paediatric outputs; composite index; caveats. OK. |

### Mechanical checks (scripts, on v17)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), with no gaps and no duplicates. Every E- and INV- reference resolves. Issues: ISS-01 to ISS-06 and ISS-08 to ISS-11 have headings; ISS-07 is referenced only as withdrawn (section 9). Every S reference lies in S-001–S-046 or S-101–S-106. Every OUT reference exists in Stage 1, and all 39 are referenced. |
| Fields | Exactly one Realises and one Conformance field in each of the 177 elements and invariants. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every OUT, the row's element and invariant sets equal the sets derived from the Realises fields. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Scopes: output 77, repertoire 32, context 1. All 10 MUST NOT and SHOULD NOT predicates begin with `¬`. |
| Attribute levels | core 94, MUST 29, SHOULD 47, MAY 2. The typing rule holds: every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. |
| Declarations | 41 `fun` declarations, all in one of the two forms of section 2.3 (`outputOf` and `viewOf` are now given functions; R17-03 is fixed). No name is declared twice. No used name is undeclared, apart from bound variables and the infix marker `_` of `_⊑_`. |
| v16 → v17 | 18 items changed: E-002, E-003, E-008, E-039, E-041 to E-043, E-049, E-051, E-053, E-055, INV-049, INV-055, INV-070, INV-074, INV-075, INV-079 and INV-097. These are byte-identical to v16: the watch-point items INV-105, E-067, E-062, E-045, E-046, INV-062 to INV-064, INV-098, INV-086, INV-087, E-060, E-061, INV-050, INV-051, INV-003, INV-054, INV-056, INV-078, E-040, INV-071, INV-072, INV-088, INV-104, INV-109 and E-047. |
| v17 constructs, by hand | Every date comparison was checked under the new day convention of section 2.8: `atTimePoint` and `fitsMonthlyPeriod`; INV-045 and INV-089 (> 3 months); INV-049 (the year); INV-051 (review dates); INV-070 with `firstChangedDay`; INV-079 and INV-109 (the course span); `courseOverlaps` and `courseNotOutside`; INV-056, INV-064, INV-067. All are consistent. `firstChangedDay` is well typed and has one member for the event kinds INV-070 admits. The new conjuncts of INV-074, INV-075 and INV-079 are well typed and guarded. |

### Scope sweep

- **Grep.** I searched for record, enter/entry, input, captur-, logged, stor-, persist-, database, JSON/XML/CSV/FHIR/HL7, serial-, encod-, retention, reminder, answer, data field, algorithm, obtained/computed/calculated from, and questionnaire. The hits are:
  - the scope statements of sections 1, 2.1, 2.7 and 3.5;
  - the "obtained from diary information; how is out of scope" notes;
  - the [S-014] HALT-30 quote ("records days affected");
  - the E-057 notes that scoring from answers is out of scope;
  - search-log tool names.

  All are legitimate.
- **Relations.** Every relation takes only output elements, constants and context properties as arguments. The change proposed in R18-01 does as well: it compares course-event dates of the context with output periods and with rule offsets.
- **Thresholds and formulas.** Every threshold, reference level, score band and offset that is part of the output data is present with its quote. No missing threshold or formula was found.

## Remarks

### R18-01 Infidelity to Stage 1 and formal defect: "on treatment" is not bounded by the stop of the course. Evaluation time points, and the MUST comparisons at them, are required for a preventive course stopped or paused before the treatment interval they close, and responder and control-level labels may classify months after the stop

- Item(s):
  - E-041 (`applicable`, Meaning, Notes); E-042 (Meaning); E-043 (Notes);
  - INV-055, INV-058, INV-059 (Predicate, Reading, Notes);
  - INV-063, INV-064 (Predicate, Reading, Notes); E-046 (Definition or Notes);
  - section 7, rows OUT-018 and OUT-020.
- Problem:
  - **(a) Time points.**
    - `applicable(c, t, r)` (E-041) and every invariant built on it look only at:
      - the treatment's type;
      - its population;
      - the existence of an anchor event.

      They never look at whether the course was still taken during the interval that the time point closes.
    - The preventive courses of the context include stopped ones ("every preventive treatment course of the subject up to the as-of date, ongoing or stopped", E-008).
    - So for a course stopped or paused shortly after its start, two MUST invariants still apply:
      - **INV-059** requires every response comparison of the course to show, as evaluation time points of the guidance, the dates "after 12 weeks of treatment", "after a minimum of 3 consecutive months on treatment" and so on;
      - **INV-055** requires, for each such time point that has been reached, a comparison whose "on-treatment" period ends at it.

      That period then lies wholly after the stop.
    - **These time points are not named by the guidance for such a course.** Every rule's guidance words its time point as a duration of treatment:
      - "after a minimum of 3 consecutive months on treatment" (EHF);
      - "after 12 weeks of treatment" and "Review the need for continuing migraine prophylaxis 3 to 6 months after starting" (NICE);
      - "at least 8–12 weeks at the recommended tolerated dose" (AAN/AHS 14A);
      - "eight weeks at the target dose" (SIGN 155);
      - "after three months at the target dose" (IHS Q2);
      - "через 3 месяца терапии", after 3 months of therapy (Russian section 7.1);
      - "niet eerder dan na 2-3 maanden behandeling", no earlier than after 2–3 months of treatment (NVN);
      - "etkinlik için en az 2-3 ay", at least 2–3 months for efficacy (Turkish Box 8).
    - The model's own day convention reads the time point as "the date after the interval (for example 'after 12 weeks of treatment' …)" (section 2.8). For a course stopped after 6 weeks, there is no 12-week interval of treatment.
    - **OUT-018 is broadened.** It requires (MUST) the comparison "at the evaluation time points named in current guidance". The model requires, at MUST, comparisons and displayed time points at dates that the guidance does not name for that course.
    - **The model is inconsistent with itself.** A rule anchored at the end of a treatment cycle (NICE 1.3.29, Turkish 3.6.3.9 and 7.3) applies only if that cycle took place, because its anchor event exists only then. Start-anchored rules ignore the stop. An onabotulinumtoxinA course stopped after one injection therefore:
      - gets no NICE 1.3.29 time point;
      - but still gets the 3–6-month NICE 1.3.27 window, the 6-month IHS Q2 (quarterly) and Russian section 3.3 time points, and the 24-week AAN/AHS 14B time point.
  - **(b) Labels.** The same gap lets an optional label classify off-treatment months as the treatment's response.
    - **INV-064 (definitional).** It ties the months of a control-level label to the start of its treatment, "Without the tie, a control-level label could classify months before the treatment as the response to it" (INV-064 Notes; added in fix 05). It does not tie them to the end of the course.
      - Yet E-046 Notes base the start tie on the levels being "goals for the migraine burden while on treatment".
      - So "optimal control" over three months after a stop is admitted.
    - **INV-063 (definitional).** It forces the category of a responder/non-responder label from the changes of its evaluated period, and `evaluated` (E-046) is not bounded by the stop. For a course of a CGRP inhibitor for episodic migraine stopped at 6 weeks, a label under NICE 1.3.28 on the month after the stop must be:
      - "non-responder" if that month shows less than a 50 % reduction;
      - "responder" if it shows at least 50 %.
    - Both outputs present a classification that the named criterion does not give.
  - **Why it matters for the reader.** In the treatment history (INV-109) and the clinician-facing summary (INV-104), each past preventive course is shown with its comparison and these time points. A course stopped early, for example for adverse effects, is thus presented as evaluated at the guidance time point, as an adequate trial.

    Stage 1 itself warns, through the EHF consensus on drug failure, that "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed" ([S-013], OUT-024).
  - **Relation to earlier loop files and watch points.**
    - No loop file discusses this, so no declined remark is re-raised.
    - **Watch point 5 (E-041).** The required change touches no `excludes`, `timing`, `ages`, `AgeCoverage`, anchor or offset value, and keeps `ruleTr73` and the age read on the treatment start.
    - **Iteration-08 watch point 2.** The three applicability dimensions (fallback type, population, exclusion) are kept. The change adds a condition on the course, on evidence that no earlier remark considered: the duration wording of every rule, the cycle-anchor asymmetry and [S-013].
    - **Watch point 4.** The change keeps every responder-label tie and relaxes none. It tightens INV-064 in the direction of fix 05.
    - **Watch point 1.** INV-105 and E-067 are untouched.
    - **Kept as Stage 1 states it.** The comparison's own periods stay "periods after treatment start" (OUT-018, INV-056). A comparison of a stopped course is still required (INV-055, first conjunct), and OUT-022's post-stop view is unaffected.
- Evidence:
  - **Model text.**
    - E-041: `pred applicable(c, t, r) ≙ t ∈ c.subject.preventiveTreatments ∧ inPopulation(c, t, r) ∧ (∃ ty ∈ r.appliesTo • (t, ty) ∈ c.subject.preventiveTypes) ∧ (¬ ∃ ty ∈ r.excludes • (t, ty) ∈ c.subject.preventiveTypes) ∧ anchorDates(c, t, r.anchor) ≠ ∅`.
    - INV-055, second conjunct: `∀ r ∈ evaluationRules; a ∈ anchorDates(c, t, r.anchor); s ∈ startOf(c, t) • applicable(c, t, r) ∧ shift(a, r.minOffset) ≤ c.asOf ∧ fitsMonthlyPeriod(s, a, r) ⇒ ∃ o … ∃ tp ∈ x.timePoints; p ∈ ran x.onTreatment • tp.rule = r ∧ tp.anchorDate = a ∧ atTimePoint(p, tp)` (MUST).
    - INV-059: `∀ r ∈ evaluationRules; a ∈ anchorDates(ctx, rc.treatment, r.anchor) • applicable(ctx, rc.treatment, r) ⇒ ∃ tp ∈ rc.timePoints • tp.rule = r ∧ tp.anchorDate = a` (MUST).
    - E-042 Meaning: "An evaluation time point of a guidance rule for one preventive treatment, shown with the response comparison: […] the date (or window) on which the evaluation falls, the first day after the interval that the guidance names".
    - Section 2.8: "The date *after* the interval (for example 'after 12 weeks of treatment', '3 to 6 months after starting', …) is the first day after it".
    - INV-064: `(∀ s ∈ startOf(ctx, L.treatment); p ∈ ran L.evaluated • s ≤ p.start)`, with no bound by a stop.
    - E-046 Notes: "The control levels are goals for the migraine burden while on treatment ([S-010] section 'Setting goals of migraine burden while on treatment'), so the months a control-level label evaluates begin on or after the start of the label's treatment (INV-064)."
  - **Stage 1 and guidance wording** (Stage 1 quotes of OUT-018, and E-041 quotes):
    - [S-011] "we suggest evaluating efficacy after a minimum of 3 consecutive months on treatment";
    - [S-015] "Stop CGRP inhibitors after 12 weeks of treatment if the frequency of migraines does not reduce by: [...]" and "Review the need for continuing migraine prophylaxis 3 to 6 months after starting prophylactic treatment.";
    - [S-018] "14A. Clinicians should wait at least 8–12 weeks at the recommended tolerated dose of most medications for migraine prevention before assessing efficacy.";
    - [S-016] "Prophylactic treatment should be used for eight weeks at the target dose or maximum tolerated dose (for those with a titration schedule) before deciding if it is effective or not.";
    - [S-008] "In individuals initiating a new migraine oral preventive treatment, we suggest evaluating effectiveness* after three months at the target dose." (Q2, p. 9);
    - [S-033] "если число дней с ГБ сокращается через 3 месяца терапии на 50% и более" (section 7.1, p. 53);
    - [S-028] "evalueer het effect niet eerder dan na 2-3 maanden behandeling";
    - [S-035] "Yeterli süre, etkinlik için en az 2-3 ay" (Kutu 8, p. 48).
  - **Stage 1 OUT-024, [S-013]:** "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed."
  - **Computed (`stopped.py`).** An adult with episodic migraine and an anti-CGRP monoclonal antibody (types `antiCGRPMonoclonalAntibody`, `monthlyInjectable`, `cgrpInhibitor`). Course start on 1 January 2026; `stop(discontinued)` dated 10 February 2026, the last day on treatment; as-of date 20 October 2026. The applicable rules, the time points INV-059 requires with every comparison of the course, and the period INV-055 requires:

    | Rule | Time point | INV-055 requires an "on-treatment" period ending on | Days on treatment in a 28-day such period |
    |---|---|---|---|
    | NICE 1.3.28 | 26 March | 25 March | 0 |
    | EHF 2022 question 3 | 1 April | 31 March | 0 |
    | IHS 2024 Q2 (monthly injectables) | 1 April | 31 March | 0 |
    | Russian section 7.1 | 1 April | 31 March | 0 |
    | NICE 1.3.27 | 1 April – 1 July | a day from 31 March to 30 June | 0 |
    | Turkish Box 8 | 1 March – 1 April | a day from 28 February to 31 March | at most 10 |

    All these time points have been reached, and `fitsMonthlyPeriod` holds. So a MUST-conformant diary must show these guidance time points for a course that was taken for 6 weeks, and compare December with March "at" them.

    With such a comparison, a NICE 1.3.28 label on March is forced by INV-063 to "non-responder" or "responder" by March's values. A control-level label over March to May with fewer than four days each month may be "optimal control".
- Required change: bound "on treatment" by the course's stop or pause wherever the model evaluates a treatment, keeping every rule value and the comparison's own periods as Stage 1 states them.
  - **(a) Time points.** Require and admit a rule's time point only for an anchor whose interval the course completes, without a stop or pause in it. For example, with a new predicate (E-041 or E-042):

    ```
    pred withoutStopIn(c : OutputContext, t : Treatment, a : Date, r : EvaluationRule) ≙
      ¬ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is stop ∧ a ≤ e.date ∧ next(e.date) < shift(a, r.minOffset)
    ```

    Here the stop or pause is dated on the last day of the course (section 2.8), and for a window the reference is its earliest date.
    - Add it to the antecedents of INV-055 (second conjunct) and INV-059. Add it either to INV-058, so that no `EvaluationTimePoint` of the rule is shown for such an anchor (a diary may still show a note on the stop as an `OtherItem`), or only to the two requirements.
    - Where a course stops within a window, INV-055 should ask for an on-treatment period that ends on or before the stop date.
    - Alternatively, add the condition to `applicable` itself, if the fixer prefers one place.
  - **(b) Labels.**
    - In INV-064, add that the evaluated months end on or before the date of every stop or pause of the label's treatment: `∀ e ∈ ctx.subject.courseEvents; p ∈ ran L.evaluated • e.treatment = L.treatment ∧ e.kind is stop ⇒ p.end ≤ e.date`. These are the months "while on treatment" of [S-010], as the start tie already reads them.
    - For responder and non-responder labels, either:
      - state the same bound for every label (E-046 `evaluated`, definitional, with the start bound that INV-064 states for control levels); or
      - let the reduction, attack-reduction and score components (`…Met`, `…Decided`, E-046) decide nothing for a label that evaluates a period ending after a stop or pause of its treatment.
  - **Align the text:**
    - E-041 Meaning and Notes (`applicable`, the sentence "applicable holds for the rules of all preventive types whenever …");
    - E-042 Meaning; E-043 Notes;
    - INV-055, INV-058 and INV-059 Readings and Notes; INV-063 and INV-064 Readings and Notes; E-046 Notes;
    - rows OUT-018 and OUT-020.
  - **Satisfiability.**
    - (a) only removes requirements: where it applies, the course is on treatment through the interval, so the v17 INV-055 construction (a 28-day period whose last day is the day before the time point, or for a window before the later of its earliest date and the 28th day after the start) lies within the course.
    - (b) constrains only optional labels (E-046, MAY). INV-062's `ran L.evaluated ⊆ ran rc.onTreatment` can be met by on-treatment periods before the stop.

## Checked and not raised

- **The v17 changes (R17-01 to R17-03 and the fixer's date sweep).**
  - The day convention is applied consistently in every place where a date is compared with a period (Mechanical checks).
  - INV-049 now bounds the year at `plusMonths(ws, 12)` exclusive; INV-070 starts the post-event periods on `firstChangedDay`.
  - The formulation ties of INV-074, INV-075 and INV-079 are well typed, definitional, and exclude only statements of a drug or formulation the subject never used.
  - `outputOf` and `viewOf` are given functions.
  - The examples in E-042, INV-049 and INV-055 are arithmetically correct.
- **Watch points.**
  - Every watch-point item of the iteration-16 check is byte-identical to v16, except those that fix 17 changed for R17-01 to R17-03 (E-041 Meaning and Notes, with no value changed; INV-049's `≤` → `<`).
  - E-062 `acute` and E-045 `valueAvailable` still use `acuteMedications ≠ ∅`; I raise nothing on them.
- **HALT-90 total score and its unit.** [S-014] states that question 5 "gives rise to a simple count for which the unit is not whole days" and is "included in the total summed score (sum of all five questions), which gives rise to grading". E-058 gives the HALT unit as days. Not raised:
  - Table 18 itself heads the graded score "Days lost in last 3 months";
  - the score remains a whole number (a count), so `wholeNumberScores` and INV-082 hold.
- **Periods that reach beyond the as-of date.** No invariant bounds a shown period by the as-of date. A comparison for a treatment started on the as-of date, or the periods after a stop dated on it, can only be met by a period that is not yet over, with its completeness shown (INV-011). This is a partially covered reporting period, not a false value. Not raised.
- **S-102 author "Pavlovic"** (PubMed "Pavlović"): a transliteration, not wrong metadata.
- **[S-028] reachable again.** All its fragments verify, and the NVN reading `anyAge` is confirmed by the Aanbeveling's schedules "BIJ KINDEREN" and "BIJ VOLWASSENEN".
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded. I re-verified:
  - 8.2.6 criterion B (p. 124) and note 2 (p. 125);
  - "simple analgesics" only on p. 139 (10.1.1, high-altitude headache);
  - NICE 1.3.9 and 1.3.39 without a review time point, 1.3.48, and the CG150 population sentence;
  - the [S-034] flowchart box (p. 52).

  No Stage 1 issue is silently worked around. R18-01 concerns the model, not Stage 1.
- **Settled points, not reopened (no new evidence):**
  - the 24-hour outcomes for cluster summaries;
  - "the history of previous bouts";
  - the lead-in;
  - HADS subscales only;
  - the review window of OUT-017 shown as a period;
  - INV-060 with INV-061 for compared periods shorter than 28 days;
  - the monthly baseline;
  - INV-023 at any granularity;
  - the "> 3 months" readings of INV-045 and INV-089;
  - the MIDAS labels;
  - the "baseline administration";
  - INV-091 to INV-093 with `concerns`;
  - "treatment effect" by one item;
  - the E-041 window readings, timings, ages and `excludes` values;
  - the E-008 time frames;
  - one adherence window per comparison;
  - the result completed on the start day read as the pre-treatment baseline (E-046, fix 17);
  - `namedCriteria` unused, and the Turkish Box 8 criterion without a constant.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and no item of v17 carries a FROZEN marker.
