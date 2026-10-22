# Review — iteration 26
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v25
Date: 2026-10-22

## Summary

This is the main review of iteration 26. I am a new, independent reviewer. I checked v25 against its sources and against Stage 1 v18. I read the earlier loop files only to avoid reopening settled points or reversing earlier fixes.

**State of the files.**
- `OUTPUT_MODEL.md` is v25 (header "Version: v25 · Iteration: 25").
- `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line (script).

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18: sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5.
- v25, every section: notation, conformance, all 67 elements and 111 invariants, traceability, section 8, sources, search log, and the change-log entry for v25.
- Fix 25, reviews 25 and 25b, and the oscillation check after iteration 24 with its ten watch points.
- The earlier review and fix passages on each point I considered raising: review 02 (baseline position), review 15 (several stops), reviews 01 to 24 on "history of previous bouts" and "baseline administration", and fix 15 (INV-070 row).

**Result.**
- **Citations.** I downloaded every source that has a quote in the model and found every quoted fragment verbatim on its stated page or section. Metadata, translations and versions are correct, and ICHD-3 is still the current edition.
- **Values.** All value sets, ranges, bands, code labels, reference levels, offsets, thresholds and control levels match their sources.
- **Scope.** The model contains no input, storage or input-derivation content. Every threshold, formula and computed field that is part of the output data is present and cited.
- **Mechanical checks.** All pass.
- **Fidelity.** 38 of the 39 Stage 1 requirements are represented at their Stage 1 strengths. One observable property of OUT-022 is not (R26-01).

**One remark (R26-01).**
- OUT-022 asks for the frequency after a stop, pause or reduction to be compared "with both the on-treatment period and the original pre-treatment baseline".
- v25 models a treatment resumed after a pause as a new course with its own start (E-008, INV-001). INV-070 bounds the baseline only by the start of the course the view concerns.
- So, for a resumed treatment, INV-070 accepts a month of the pause interval as "the original pre-treatment baseline". OUT-022's own evidence describes that interval as the time when "migraine worsens after treatment withdrawal" ([S-011]).
- The remark keeps fix 25 (one stop per course; a restart is a new course). It asks for the link between a resumed course and the course it resumes, so that the original baseline can be required.

## Verification coverage

### Downloads and tools

- **Where.** Every source was downloaded fresh with `curl` through the proxy into `/tmp/r26_src`, outside the repository. All requests returned HTTP 200.
- **Scripts.** Kept in the session scratchpad (`r26/`) and run with `python3 -I`: `quotes.py`, `pages.py`, `onpage.py`, `mech.py`, `names.py` and `restart.py`.
- **Extraction.**
  - PDFs: page by page, with `pdftotext -raw` and `-layout`.
  - HTML pages and Europe PMC full-text XML: markup stripped.
  - Matching: NFKC normalisation, soft hyphens removed, line-end hyphens joined, case folded, letters and digits only.
- **Rendered and read.** Two passages have no usable text layer, so I rendered them with `pdftoppm` and read them:
  - [S-001] p. 190: A1.1.1 criterion B "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)", A1.1.2 criterion B "Occurring on day 1 ± 2 (i.e. days −2 to +3)", and note 2. The text layer drops "±" and "−" and maps "+" to "þ".
  - [S-034] p. 1, an image: "Возрастная группа" followed by "дети".
- **Metadata.**
  - **PubMed esummary.**
    - S-101: PMID 20819842, Cephalalgia 2011 Feb;31(3):357–67, DOI 10.1177/0333102410379890, PMC3057423; authors Yang, Rendas-Baum, Varon, Kosinski (QualityMetric).
    - S-102: PMID 25902814, J Headache Pain 2015;16:24, PMC4406925; the seven authors as cited, with Stewart and Lipton.
    - S-104: PMID 12914662, Health Qual Life Outcomes 2003;1:29, PMC183845; Snaith.
    - The S-103 developer paper: PMID 11739822, Neurology 2001;57(11):2034–9.
  - **S-105 PDF metadata.** Author Kurt Kroenke; created 22 June 2010, modified 16 April 2014. The developers' sentence is on P. 8/9.
  - **S-103.** Page footer "© 2026 Cincinnati Children's Hospital Medical Center".
  - **S-106 (TA260).** "Published: 27 June 2012" and "Last reviewed: 11 January 2016". Chapter 1 has "less than a 30% reduction in headache days per month after 2 treatment cycles" (the search-log statement), and chapter 2 the re-treatment schedule "every 12 weeks".
  - **S-015 (NICE CG150).** "Published: 19 September 2012 Last updated: 03 June 2025". No newer update.
  - **Newer versions.** A web search finds no ICHD-4 publication: the IHS classification page lists ICHD-4 as work in progress. So [S-001] is current.

### Quote check per source

**Method (`quotes.py`).**
1. Take every double-quoted string outside the `omn` blocks: 883 fragments, after splitting at "[...]" and keeping fragments of at least 6 letters or digits.
2. Search each fragment in the downloaded sources page by page, then in Stage 1 v18.
3. Compare the page where each fragment was found with the location the model states (`pages.py`, `onpage.py`). Where the first hit was in a table of contents, an abstract or a summary table, I re-checked the stated page directly: the ICHD-3 classification list pp. 8, 9 and 12; [S-008] Q2 p. 9; [S-105] P. 6/9; [S-035] PDF pp. 77, 82 and 86. All matched.

| Source | Quotes or fragments checked (unique) | Verbatim on stated location | Not found | Unreachable (tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (PDF, 211 pp.) | 94 (+2 with ± and − read on the rendered p. 190) | 96 | 0 | — |
| S-007 IHS cluster (UCL PDF) | 9 | 9 | 0 | — |
| S-008 IHS 2024 preventive (univaq PDF) | 33 | 33 | 0 | — |
| S-010 IHS 2025 position statement (univaq PDF) | 27 | 27 | 0 | — |
| S-011 EHF 2022 (Europe PMC) | 10 | 10 | 0 | — |
| S-014 EHF/LTB aids (Europe PMC) | 27 | 27 | 0 | — |
| S-015 NICE CG150 (Recommendations and Overview pages) | 32 | 32 | 0 | — |
| S-016 SIGN 155 (PDF; printed page = PDF page − 6) | 8 | 8 | 0 | — |
| S-018 AAN/AHS clinician summary (PDF) | 17 | 17 | 0 | — |
| S-023 DMKG/ÖKSG/SKG (Europe PMC) | 6 | 6 | 0 | — |
| S-028 NVN module (web page) | 10 | 10 | 0 | — |
| S-033 Russian adults (official PDF, 92 pp.) | 20 | 20 | 0 | — |
| S-034 Russian children (official PDF, 53 pp.) | 7 (+1 on the rendered title page) | 8 | 0 | — |
| S-035 Turkish protocol (PDF, 92 pp.) | 35 | 35 | 0 | — |
| S-012, S-013 (Europe PMC; Stage 1 fragments reused) | 3 + 3 | 6 | 0 | — |
| S-101 HIT-6 validation (Europe PMC) | 5 | 5 | 0 | — |
| S-102 AMPP menses/MIDAS (Europe PMC) | 8 | 8 | 0 | — |
| S-103 PedMIDAS page | 12 (table rows and headings) | 12 | 0 | — |
| S-104 HADS (Europe PMC) | 3 | 3 | 0 | — |
| S-105 PHQ/GAD-7 manual (PDF) | 7 | 7 | 0 | — |
| S-106 NICE TA260 (chapters 1 and 2, overview) | 2 (+1 in the search log) | 3 | 0 | — |
| Other Stage 1 sources (S-002 to S-006, S-020 to S-022, S-024 to S-027, S-029 to S-032, S-036 to S-046), reused by their Stage 1 quotes | 204 unique fragments, matched verbatim in Stage 1 v18 (evidence carries over by reference) | 204 | 0 | not re-downloaded; no Stage 2 quote depends on them |

**The 82 fragments not found in a source**, each accounted for:
- 41 are search-log or change-log text (PubMed queries, model wording).
- 22 are English translations. I read each against its original:
  - [S-028]: P/PICO.
  - [S-033]: title page, section 3.3 comments, the BTA recommendation, section 3.3 on the anti-CGRP time point.
  - [S-034]: flowchart, title page, section 2.
  - [S-035]: Kutu 8 items, sections 3.3 b, 3.6.3.9, 6, 7.1 and 7.3.

  All are faithful.
- 16 are model-internal phrases or paraphrases in conformance text, not source quotes (for example "output model notation"; "where results are available", settled in review 25).
- 2 are ICHD-3 quotes with glyphs that have no text mapping; I verified them on the rendered page.
- 1 is the [S-034] title-page image; I verified it on the rendered page.

### Values checked against sources

- **E-009.** The ICHD-3 code labels are verbatim on pp. 8, 9 and 12.
- **E-028 and E-032.** Reference levels 10 and 15 days per month, more than three months, are on pp. 122–125. The 8.2.6 criterion B and note 2, and the 8.2.3 comment, are verbatim.
- **E-041.**
  - All 18 rules match their sources: offsets, anchors, timings, ages and `excludes`. This includes [S-008] Q2 (Optimal and Essential, p. 9), [S-018] 14A, 14B (with its repeated "before assessing efficacy", p. 7) and 14H (p. 8), [S-033] pp. 39–41, [S-034] p. 52 and [S-035] PDF pp. 48, 57 and 86.
  - The date arithmetic of the examples is correct:
    - 26 March for NICE CG150 1.3.28; 26 February to 25 March is 28 days;
    - 28 February, 25 March and 31 March as the ends of the intervals;
    - TA260's 12-week re-treatment places the end of the second cycle at 24 weeks, within the 1.3.27 window.
- **E-045 and E-046.**
  - NICE 1.3.28 (50 % / 30 %) and 1.3.29 (30 % headache days).
  - IHS Q6 (≥ 50 %; the ≥ 30 % chronic alternative; MIDAS ≥ 5 points for baseline 11–20 and ≥ 30 % for ≥ 20; HIT-6 ≥ 5 points; pp. 12–13).
  - DMKG/ÖKSG/SKG and the Russian section 7.1 (50 %).
  - Turkish Kutu 8 (≥ 50 % attack frequency).
  - The four control levels of [S-010] p. 6 (none, < 4 for three months, 4–6, > 6).
- **E-057.**
  - HIT-6: 36–78 and the four categories [S-101]. Its one-month recall is also stated in [S-101] itself: "a one-month recall of the HIT-6".
  - MIDAS: grades I–IV, 0–5, 6–10, 11–20, ≥ 21, and three months [S-102].
  - PedMIDAS: 0–10, 11–30, 31–50, > 50 [S-103].
  - HALT-90: table 18, including the overlap at 20; HALT-30: no grading [S-014].
- **E-059.** HADS 0–21 per subscale [S-104]; PHQ-9 0–27 and GAD-7 0–21 [S-105].
- **E-039 and E-060.** NICE CG150 1.3.48: 4–8 weeks. ICHD-3 A1.1 window: day 1 ± 2, no day 0.
- **E-063.** The ICHD-3 remission duration, "must exceed three months" (p. 209).
- **Other date examples in Notes:** 67 days (E-007), 43 days (INV-049, INV-105), 42 and 143 days (E-063), and day 43 within the review window. All correct.

### Fidelity check per Stage 1 requirement

| OUT | Result |
|---|---|
| 001 | Periods with start, end and length (INV-002, INV-003); monthly availability at MUST (INV-014, INV-015, INV-108); equal-length comparison (INV-037, INV-055); Caveat. OK. |
| 002 | Labels for every reported form (INV-008, `reports`); one definition per view (INV-111). OK. |
| 003 | Indicator next to every summary measure (INV-011, INV-012); SHOULD NOT cut-off (INV-013). OK. |
| 004–007 | Per period, definitions, separate attack counts, levels as in Stage 1 (INV-014 to INV-017, INV-108, INV-009, INV-010). OK. |
| 008 | MAY elements with relations (E-020 to E-022, INV-031). OK. |
| 009 | Series with start, dose-change and stop markers; weekly where relevant (INV-034 to INV-036). OK. |
| 010, 011 | Intensity on a stated scale and compared (INV-018, INV-032, INV-039); duration with the treated-attack label and the SHOULD NOT (INV-019 to INV-021). OK. |
| 012, 013 | Across periods and per treated attack (INV-022, INV-072, INV-076); aura counts MAY (E-027). OK. |
| 014–016 | Total, class and drug (INV-023, INV-024); weekly view (INV-025); indicator with code, level, span and basis, prompt MUST, MUST NOT diagnosis (INV-044 to INV-048). OK. |
| 017 | Follow-up, review window, worsening label (INV-049 to INV-052). OK. |
| 018–021 | Comparison, time points, residual burden, labels, review view (INV-053 to INV-069, INV-102, INV-106). OK. |
| 022 | Post-stop view at SHOULD (INV-070, INV-103). **Not fully represented: "the original pre-treatment baseline" for a resumed treatment (R26-01).** |
| 023, 024 | Acute summaries, outcomes, formulation, phases (INV-071 to INV-075, INV-107); history (INV-077 to INV-079, INV-109). OK. |
| 025, 039 | Scheme windows MAY (E-056, INV-080); adherence (INV-066, INV-067, INV-104, INV-109). OK. |
| 026–027 | Instrument results and value sets (INV-081, INV-082, INV-100); functional impact with baseline comparison (INV-026, INV-027). OK. |
| 028–031 | Three-month view MUST, SHOULD and SHOULD NOT parts (INV-040 to INV-043); per type (INV-028 to INV-030); menstrual view MUST (INV-086, INV-087); cluster view (INV-088, INV-089). OK. |
| 032–038 | Trigger caveats; screening; clinician and patient views; paediatric (a)–(d) and Caveat; composite index; interpretive caveats (INV-090 to INV-101, INV-104, INV-105, INV-110). OK. |

Every conformance level matches the Stage 1 strength of the part it realises. MUST NOT is used for OUT-016 and for the OUT-018 Caveat; SHOULD NOT for the SHOULD parts and Caveats.

### Mechanical checks (`mech.py`, `names.py`)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111): none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn, section 9). |
| References | No dangling E-, INV- or ISS- reference. Every OUT reference exists in Stage 1 (39 requirements). Every cited source ID is S-001 to S-046 or S-101 to S-106, and each of S-101 to S-106 is cited. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field. Every invariant has exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. |
| Names | 182 `omn` blocks. Every identifier used is declared, bound by a quantifier, comprehension, parameter list or `let`, or a primitive. `refs` is defined in section 2.5. The v25 INV-001 conjuncts are well typed: `#` on a finite comprehension, `is` on variant tags, `≤` on dates. |
| Scope sweep | Every occurrence of record, enter, input, store, database, XML, serializ, encod, retention, answer, reminder, algorithm, obtained, comput and questionnaire, read in context, is an exclusion statement, an explanation that a value derives from diary information without stating how, or search-log text. The v25 text ("restarted", "resumed", "made definitive") describes context properties. |
| Predicate behaviour (`restart.py`) | The case of R26-01 evaluated with the predicates as written: INV-001 (v25) admits the context; INV-103 requires the post-stop view; INV-070 admits a pause-interval baseline (Remark R26-01). |

## Remarks

### R26-01 Infidelity to Stage 1: the "original pre-treatment baseline" of OUT-022 is not required for a treatment resumed after a pause
- Item(s): INV-070 (Predicate, Reading); E-049 (`baseline`, Meaning, Notes); E-008 (Notes); INV-001 (Notes); traceability row OUT-022.
- Problem:
  - OUT-022 (SHOULD) asks the post-stop output to compare the frequency after a stop, pause or reduction "with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible".
  - Since v25, a treatment resumed after a pause is a new course with its own start (E-008, INV-001: at most one start and at most one stop or pause per course).
  - INV-070 bounds the post-stop baseline only by the start of the course the view concerns: `(∀ b ∈ v.baseline; s ∈ startOf(ctx, v.treatment) • b.end < s)`.
  - For the resumed course, that start is the restart date. So INV-070 accepts, as "the original pre-treatment baseline", any period before the restart, including a month of the pause interval. That month is not the original pre-treatment baseline of the treatment.
  - It is also, by OUT-022's own evidence, the time in which migraine worsened after withdrawal. Comparing with it can hide the "worsening or rebound above baseline" that OUT-022 exists to show.
  - The model's own text says only that the original baseline "may" be used. The model therefore admits outputs that OUT-022 excludes, and it does not represent the word "original" for this case.
- Evidence:
  - **Stage 1 OUT-022.**
    - Statement: "After a preventive treatment is stopped, paused or reduced, the diary output SHOULD continue to show headache and migraine frequency and compare it with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible."
    - Evidence quote [S-011]: "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal." The pause interval is the time of worsening that leads to the restart.
    - Evidence quote [S-022]: "Patients should be followed for at least 4 weeks after termination of the treatment period to detect possible rebound phenomena (i.e. frequency of migraine days per month going above its baseline)." The baseline is the one from before treatment.
  - **The model text.**
    - E-049: `baseline : opt →Period  SHOULD               -- the original pre-treatment baseline period`.
    - The INV-070 Reading says the view shows the values "for the original pre-treatment baseline period, so that worsening or rebound above baseline is visible". The predicate does not secure this for a resumed course.
    - INV-001 Notes: "its pre-treatment baseline may still be the original one, before the first course, because INV-056, INV-068 and INV-070 bound a baseline only by the start of its own course."
    - Row OUT-022: "a pause followed by a restart is the stop of one course and the start of a new one, whose monitoring after its own stop may compare with the original baseline before the first course".
  - **Instance** (`restart.py`, predicates as written in v25).
    - Course t1 of drug X starts on 1 January 2026, with `stop(paused)` on 30 June 2026. Migraine worsens.
    - Course t2 of the same drug starts on 1 September 2026, with `doseChange(reduction)` on 1 October 2026. The as-of date is 21 October 2026.
    - INV-001 admits the context, and INV-103 requires a post-stop view for t2's reduction.
    - INV-070 admits, as that view's baseline, August 2026, the pause interval (31 August < 1 September). It equally admits December 2025, the month before the treatment was first started.
    - So the model admits a post-stop view whose "original pre-treatment baseline" is a month of worsening during the pause.
  - **This does not reverse an earlier fix.**
    - Fix 25 chose option (a) of R25b-01 (one stop or pause per course; a resumed treatment is a new course). That choice is kept.
    - Fix 25 checked only that the original baseline "stays admissible after a restart, because INV-056, INV-068 and INV-070 bound a baseline only by the start of its own course" (fixes/fix-iter-25.md). It did not consider that the same bound also admits a non-original baseline, which OUT-022 excludes. Nor did it consider the [S-011] wording that places worsening in the pause interval.
    - Review 02 settled only that the baseline need not be the month directly before the start. No earlier review examined the baseline of a resumed course.
    - The change leaves every watch-point-4 item unchanged: the course-event dates of section 2.8, `atTimePoint`, `fitsMonthlyPeriod`, `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, `firstChangedDay` and E-049 `onTreatmentPeriod`.
    - The aligned items of watch point 9 are not touched. The remark concerns the fidelity of INV-070 to OUT-022, not a text-versus-predicate wording issue.
- Required change: make INV-070 require, for a resumed treatment, a baseline before the treatment was originally started. Either option below meets this.
  - **Option (a): a link in the context.**
    1. Add a component to the context (E-008) that states which course resumes which, for example `resumes : set (Treatment × Treatment)`.
       - (t₁, t₂) ∈ resumes: course t₂ resumes the preventive treatment of course t₁ after t₁'s stop or pause.
       - INV-001 conjuncts: both courses are preventive; `drugOf(t₁) = drugOf(t₂)`; t₁ has a stop dated before the start of t₂; each course resumes at most one course and is resumed by at most one.
    2. Define the original start of a course as the start of the first course of its chain of resumptions. The chain is finite, because each start follows the previous course's stop.
    3. In INV-070, bound the baseline by the original start instead of `startOf(ctx, v.treatment)`.
  - **Option (b): a reading of the existing context, without a new component.**
    1. State in E-008 that a course of the same drug that starts after a course ending with `stop(paused)` resumes that course. Name which such course, for example the first that starts after the pause.
    2. Define the original start from this reading.
    3. Use it in INV-070 as in option (a).
  - **Either way:**
    - Update the INV-070 Reading, E-049 (Meaning, Notes), E-008 Notes, the INV-001 Notes ("may still be the original one" becomes a requirement) and the OUT-022 traceability row.
    - Check satisfiability: a period that ends before the original start can always be shown, and periods of a common length meet INV-097 for children.
    - The response comparison (INV-056) and the treatment review view (INV-068) need no change: OUT-018 and OUT-021 say "pre-treatment baseline", not "original".
  - **If the fixer finds** that Stage 1 leaves open whether the "original" baseline of a resumed treatment is the one before its first course, record that question in section 8, with evidence and a pointer from E-049. Do not leave it as "may" in the model.

## Checked and not raised

- **Citations.** Every quoted fragment of the model is verbatim at its stated location.
  - Location claims checked: table of contents, abstract and summary-table first hits were re-checked on the stated page; the [S-016] printed-page offset of 6; [S-007] manuscript pages; [S-035] PDF pages; [S-105] "P. 6/9" and "P. 8/9".
  - The omissions marked "[...]" in the ICHD-3 8.2.4, 8.2.5, 8.2.6 and 8.2.8 criteria are footnote markers only. The 8.2 Description omission leaves the meaning intact.
  - All translations are faithful.
- **Search log.** It has no entry for iteration 23. Fix 23 made no search or download, so this is not a remark category; review 25 noted the same.
- **The HIT-6 recall of one month.** The HIT-6 items ask about "the past 4 weeks". The model's `recallMonths(1)` follows [S-002] (Stage 1) and [S-101], whose developer co-author writes "a one-month recall of the HIT-6". Settled, consistent with the cited sources.
- **ISS-02.** "Simple analgesics" occurs once in the ICHD-3 text layer, on p. 139, as ISS-02 states (page-by-page script).
- **Section 8.**
  - ISS-01, ISS-03, ISS-05, ISS-06 and ISS-08 to ISS-12 are founded.
  - Their quotes are verbatim at the stated locations (pp. 42, 122–125, 139, 190 and 209 of [S-001]; NICE 1.3.9, 1.3.39 and 1.3.48; [S-034] p. 52).
  - Their descriptions of the passages are accurate.
  - No Stage 1 issue is silently worked around, apart from the OUT-022 point of R26-01, which is a model defect rather than a Stage 1 issue.
- **v25 INV-001 conjuncts.**
  - They are well typed and satisfiable, and exclude only histories that are not states of one course under section 2.8.
  - Cycle ends after a stop remain admissible, and harmless: `intervalOnTreatment` then requires no time point.
  - A dose change on the stop date is admitted (`≤`), and its post-stop view is satisfiable.
- **Other effects of "a restart is a new course".**
  - Each course has its own line, duration, markers, response comparison and review view.
  - OUT-024 ("chronological list [...] with start and stop dates [...] treatment duration"), OUT-009 (start markers) and OUT-018 and OUT-021 ("pre-treatment baseline") are met. None of these statements says "original".
- **Settled points, not reopened (no new evidence):**
  - "history of previous bouts" (review 01 onward);
  - "baseline administration" as any earlier administration;
  - the "> 3 months" readings of INV-045 and INV-089;
  - INV-106 at MUST NOT;
  - the E-041 readings and `excludes`;
  - the cluster view (watch point 3);
  - `fillsPeriod` (watch point 5);
  - the formulation ties (watch point 6);
  - ISS-03 and its list (watch point 7);
  - by-dates relations and output-wide agreement (watch point 1);
  - INV-008 and INV-111 (watch point 2);
  - comparison periods beyond the as-of date (watch point 10);
  - the two illustrative paraphrases in sections 1 and 3.3 (review 25).
- **Oscillation watch points.**
  - R26-01 changes no item named in watch points 1 to 10 in the direction of an earlier state.
  - It keeps fix 25's option (a) and every stop bound and course-event date.

## Notes on frozen items (for the human)

None.
