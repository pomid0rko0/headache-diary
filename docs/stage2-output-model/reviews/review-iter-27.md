# Review — iteration 27
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v26
Date: 2026-10-22

## Summary

This is the main review of iteration 27, by a new, independent reviewer. I checked v26 against its sources and against Stage 1 v18. I read the earlier loop files only to avoid reopening settled points or reversing earlier fixes.

**State of the files.**
- `OUTPUT_MODEL.md` is v26 (header "Version: v26 · Iteration: 26") and is byte-identical to `history/v26.md`.
- `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18: sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5.
- v26, every section: notation, conformance, all 67 elements and 111 invariants, traceability, section 8, sources, search log (the change log was read for v24–v26).
- Review 26 and fix 26 in full; the "Checked and not raised" lists of reviews 24, 25 and 25b; the oscillation check after iteration 24 with its ten watch points; the earlier loop passages on each point I considered raising (review 03 on the acute part of optimal control; fix 10 and the INV-103 rows of reviews 10–26).

**Result.**
- **Citations.** I downloaded every source that carries a quote in the model and found every quoted fragment verbatim at its stated location. Translations, metadata and versions are correct; ICHD-3 is still the current edition.
- **Values.** All value sets, ranges, bands, code labels, reference levels, offsets, thresholds and control levels match their sources.
- **Scope.** No input, storage or input-derivation content. Every threshold, formula and computed field that is part of the output data is present and cited.
- **Mechanical checks.** All pass.
- **Fidelity.** 38 of the 39 requirements are fully represented at their Stage 1 strengths. One case of OUT-022 is not (R27-01).

**One remark (R27-01).**
- Fix 26 (R26-01) introduced `originalStart` so that the post-stop view of a resumed treatment compares with the baseline from before the treatment was first started.
- Where the first course of the chain of resumed courses has no stated start, `originalStart` falls back to "the earliest start that the context states", which is the start of a later course of the chain, that is, a restart.
- INV-070 then again admits a month of the interval off treatment (and a month on the first course) as "the original pre-treatment baseline". This is the R26-01 defect, in a case that fix 26 did not examine against OUT-022. The model's own Notes claim that this cannot happen.

## Verification coverage

### Downloads and tools

- **Where.** Every source was downloaded fresh with `curl` through the proxy into `/tmp/r27_src`, outside the repository. Page texts went to `/tmp/r27_txt` and rendered pages to `/tmp/r27_img`.
- **HTTP.** All requests returned HTTP 200. The one exception was [S-033] (apicr.minzdrav.gov.ru): the connection was reset by the peer twice, and the official 92-page PDF downloaded on the third attempt.
- **Scripts.** All are in the session scratchpad folder `r27/` and were run with `python3 -I`:
  - `norm.py`, `quotes.py`, `global.py` and `tally.py` for quote extraction and matching;
  - `onpage.py` for location checks;
  - `mech.py` and `names.py` for the mechanical checks;
  - `chain.py` and `chain2.py` for predicate behaviour.
- **Extraction.** PDFs page by page with `pdftotext -raw` and `-layout`. HTML pages and Europe PMC full-text XML with the markup stripped.
- **Matching.** NFKC normalisation; soft hyphens removed; line-end hyphens joined; case folded; letters and digits only.
- **Rendered and read** (no usable text layer):
  - [S-001] p. 190: A1.1.1 criterion B "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)", A1.1.2 criterion B "Occurring on day 1 ± 2 (i.e. days −2 to +3)", and note 2. The text layer drops "±" and "−".
  - [S-034] p. 1, an image: "Возрастная группа" followed by "дети".

### Quote check per source

**Method.**
1. Every double-quoted string outside the `omn` blocks and before the search log was taken: 883 fragments, after splitting at "[...]" and keeping fragments of at least 6 letters or digits.
2. Each fragment was attributed to the source tag in its line and searched page by page. Unmatched fragments were then searched in every downloaded source and in Stage 1 v18.
3. Where the first hit was a table of contents, an abstract or a summary page, the fragment was re-checked on the stated page (`onpage.py`). Pages re-checked:
   - [S-001]: classification list pp. 8, 9 and 12; pp. 122–125; p. 139.
   - [S-008]: Q2 sentences on p. 9.
   - [S-105]: P. 6/9.
   - [S-035]: PDF pp. 23, 77, 82 and 86.
   - [S-033]: pp. 4, 41 and 53.
   - [S-016]: PDF pp. 7 and 20 (printed pp. 1 and 14).
   - [S-010]: p. 6.
   - [S-007]: p. 21.

   All matched.

| Source | Unique fragments checked | Verbatim at stated location | Not found | Unreachable (tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (PDF, 211 pp.) | 60 (58 in the text layer + 2 with ± and − read on rendered p. 190) | 60 | 0 | — |
| S-007 IHS cluster (UCL PDF, 39 pp.) | 6 | 6 | 0 | — |
| S-008 IHS 2024 preventive (univaq PDF, 31 pp.) | 27 | 27 | 0 | — |
| S-010 IHS 2025 position statement (univaq PDF, 11 pp.) | 20 | 20 | 0 | — |
| S-011 EHF 2022 (Europe PMC XML) | 9 | 9 | 0 | — |
| S-012, S-013 (Europe PMC XML) | 1 + 2 | 3 | 0 | — |
| S-014 EHF/LTB aids (Europe PMC XML) | 25 | 25 | 0 | — |
| S-015 NICE CG150 (Recommendations and Overview pages) | 24 | 24 | 0 | — |
| S-016 SIGN 155 (PDF, 64 pp.) | 7 | 7 | 0 | — |
| S-018 AAN/AHS clinician summary (PDF, 12 pp.) | 14 | 14 | 0 | — |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML) | 6 | 6 | 0 | — |
| S-028 NVN module (web page) | 7 | 7 | 0 | — |
| S-033 Russian adults (official PDF, 92 pp.) | 19 | 19 | 0 | connection reset twice, third attempt HTTP 200 |
| S-034 Russian children (official PDF, 53 pp.) | 7 (6 + 1 on the rendered title page) | 7 | 0 | — |
| S-035 Turkish protocol (PDF, 92 pp.) | 30 | 30 | 0 | — |
| S-101 HIT-6 validation (Europe PMC XML) | 4 | 4 | 0 | — |
| S-102 AMPP menses / MIDAS (Europe PMC XML) | 6 | 6 | 0 | — |
| S-103 PedMIDAS page (Cincinnati Children's) | 12 (table rows and headings) | 12 | 0 | — |
| S-104 HADS (Europe PMC XML) | 3 | 3 | 0 | — |
| S-105 PHQ/GAD-7 manual (PDF, 9 pp.) | 5 | 5 | 0 | — |
| S-106 NICE TA260 (chapters 1 and 2, overview) | 2 | 2 | 0 | — |
| Other Stage 1 sources (S-002 to S-006, S-020 to S-022, S-029 to S-032, S-042 to S-046), reused through their Stage 1 quotes | 351 fragment occurrences, all verbatim in Stage 1 v18 (evidence carries over by reference) | 351 | 0 | not re-downloaded; no Stage 2 quote depends on them |

**Fragments not found in a source, all accounted for:**
- **22 English translations.** I read each against its original: [S-028] PICO; [S-033] title page, section 3.3 comments, the BTA recommendation, and the anti-CGRP sentence of p. 41; [S-034] flowchart, title page and section 2; [S-035] Kutu 8 items, sections 3.3 b, 3.6.3.9, 6, 7.1 and 7.3, and the chapter 7 heading. All are faithful.
- **16 model-internal phrases**, not source quotes. Examples: "output model notation", "K is available when C", "the subject has migraine", "of the same period", "total score, where the instrument defines one" (ISS-06's proposal).

### Metadata and versions

- **PubMed esummary.**
  - S-101: PMID 20819842, Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMC3057423; authors Yang, Rendas-Baum, Varon, Kosinski.
  - S-102: PMID 25902814, J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMC4406925; seven authors including Stewart and Lipton.
  - S-104: PMID 12914662, Health Qual Life Outcomes 2003;1:29, DOI 10.1186/1477-7525-1-29, PMC183845; Snaith.
  - The S-103 developer paper: PMID 11739822, Neurology 2001;57(11):2034–9, DOI 10.1212/wnl.57.11.2034.
- **S-103.** Footer "© 2026 Cincinnati Children's Hospital Medical Center".
- **S-105.** PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014. The developers' sentence is on P. 8/9 and the score ranges on P. 6/9.
- **S-106.** "Published: 27 June 2012", "Last reviewed: 11 January 2016". Chapter 1 has "less than a 30% reduction in headache days per month after 2 treatment cycles"; chapter 2 has "every 12 weeks".
- **S-015.** "Published: 19 September 2012 Last updated: 03 June 2025"; the overview page now also shows "Last reviewed: 23 September 2026". No change of content.
- **Newer versions.** A web search finds no published ICHD-4, only "Work in Progress" papers and an IHS committee workshop (September 2025). [S-001] is current.

### Values checked against sources

- **E-009.** Code labels verbatim on pp. 8, 9 and 12.
- **E-028 and E-032.** Reference levels 15 (8.2.3) and 10 (8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6, 8.2.8) days per month, for more than three months (pp. 122–125). `classesOf826` is the class list of 8.2.6 criterion B; the note 2 exclusion of 8.2.1–8.2.5 holds; the 8.2.3 comment is verbatim (p. 123).
- **E-041.** All 18 rules match their sources: offsets, anchors, timings, ages and `excludes`. This covers [S-015] 1.3.27–1.3.29, [S-018] 14A, 14B and 14H, [S-016] section 4.1, [S-011] question 3, [S-008] Q2, [S-028], [S-033] pp. 39–41 and 53, [S-034] p. 52, and [S-035] PDF pp. 48, 57 and 86. The re-treatment every 12 weeks ([S-106]) places the end of NICE cycle 2 at 24 weeks, within the 1.3.27 window.
- **E-045 and E-046.**
  - NICE 1.3.28 (50 % / 30 %) and 1.3.29 (30 %, headache days).
  - IHS Q6: ≥ 50 %; the ≥ 30 % chronic alternative; MIDAS ≥ 5 points for baseline 11–20 and ≥ 30 % for ≥ 20; HIT-6 ≥ 5 points (pp. 12–13).
  - DMKG/ÖKSG/SKG; Russian section 7.1 (50 %); Turkish Kutu 8 (≥ 50 % attack frequency).
  - The four control levels of [S-010] p. 6.
- **E-057.** HIT-6 36–78 and its four categories [S-101]. MIDAS grades I–IV with 0–5, 6–10, 11–20 and ≥ 21, and a three-month recall [S-102]. PedMIDAS 0–10, 11–30, 31–50 and > 50 [S-103]. HALT-90 Table 18 including the overlap at 20, and HALT-30 without grading [S-014].
- **E-059.** HADS 0–21 per subscale [S-104]; PHQ-9 0–27 and GAD-7 0–21 [S-105].
- **E-039, E-060, E-063.** NICE 1.3.48: 4–8 weeks. ICHD-3 A1.1: day 1 ± 2, no day 0. Remission "must exceed three months" (p. 209).
- **Date examples in the Notes, all correct:**
  - 67 days (E-007);
  - 26 March, and 26 February – 25 March as 28 days (E-042, INV-055);
  - 28 February, 25 March and 31 March as interval ends;
  - day 43 and 6 April (INV-049), and 43 days (INV-105);
  - 42 and 143 days (E-063);
  - the v26 E-049 example (December 2025 admitted, August 2026 not).

### Fidelity check per Stage 1 requirement

| OUT | Statement parts and Caveats checked | Result |
|---|---|---|
| 001 | Period with start, end and length (E-003, E-005, INV-002, INV-003, MUST); monthly frequency outputs (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); Caveat (stated length) | OK |
| 002 | Definition label for every reported form (INV-008, `reports`); one definition per view (INV-111) | OK |
| 003 | Indicator next to every summary measure (INV-011, INV-012); SHOULD NOT validated cut-off (INV-013); Caveat | OK |
| 004–007 | Per period over the selected range, ICHD-3 definitions, attacks separate; levels MUST/MUST/SHOULD/SHOULD with the OUT-001 MUST where provided (INV-014 to INV-017, INV-108, INV-009, INV-010) | OK |
| 008 | MAY measures, exploratory annotation MAY (E-020 to E-022) | OK |
| 009 | Series with start, dose-change and stop markers in the view; weekly where relevant (INV-034 to INV-036) | OK |
| 010, 011 | Intensity on a stated scale, compared (INV-018, INV-032, INV-039); duration, treated-attack label SHOULD, Caveat as SHOULD NOT (INV-019 to INV-021) | OK |
| 012, 013 | Across periods and per treated attack (INV-022, INV-072, INV-076); aura MAY (E-027) | OK |
| 014–016 | Total, class, drug (INV-023, INV-024); weekly view (INV-025); indicator per period, class and 8.2.6 with code, level and span, prompt MUST, diagnosis MUST NOT, interpretation caveat (INV-044 to INV-048, INV-100) | OK |
| 017 | From the start of withdrawal, review window, following year, worsening label (INV-049 to INV-052) | OK |
| 018 | Comparison per preventive treatment with values and both changes (INV-053 to INV-057), time points by type and population (E-041, INV-055, INV-058, INV-059), Caveat (INV-106) | OK |
| 019, 020 | Residual burden (INV-060, INV-061); labels with criterion, values, other values, not sole indicator (INV-062 to INV-065) | OK |
| 021 | MUST and SHOULD components for the same periods (INV-068, INV-069, INV-102) | OK |
| 022 | Post-stop view, on-treatment period and **original** pre-treatment baseline (INV-070, INV-103) | **Partial: R27-01** (resumed treatment whose first course has no stated start) |
| 023, 024 | Acute outcomes, consistency, timing, formulation, phases, 15 minutes for cluster, Caveat (INV-071 to INV-075, INV-107); history (INV-077 to INV-079, INV-109) | OK |
| 025, 039 | Scheme windows MAY (E-056, INV-080); adherence next to the comparison, in the history and in the clinician summary (INV-066, INV-067, INV-104, INV-109) | OK |
| 026, 027 | Instrument results with name, date, recall, score, grading and change (INV-081, INV-082); functional impact and baseline comparison (INV-026, INV-027) | OK |
| 028–031 | Three-month view: MUST, SHOULD and SHOULD NOT parts (INV-040 to INV-043); per type (INV-028 to INV-030); menstrual view MUST (INV-086, INV-087); cluster view (INV-088, INV-089) | OK |
| 032–038 | Trigger caveats; screening; clinician and patient views; paediatric (a)–(d) and Caveat; composite index; interpretive caveats (INV-083 to INV-101, INV-104, INV-105, INV-110) | OK |

Every conformance level matches the strength of the Stage 1 statement part it realises. MUST NOT is used for OUT-016 and the OUT-018 Caveat; SHOULD NOT for the SHOULD parts and Caveats.

### Mechanical checks (`mech.py`, `names.py`)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111): none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn, section 9). |
| References | No dangling E-, INV- or ISS- reference. All OUT references exist in Stage 1 (39). The 37 cited source IDs are within S-001–S-046 or S-101–S-106, and S-101 to S-106 are all cited. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. |
| Names | 182 `omn` blocks. Every identifier is declared, an attribute, a primitive or semantic constant, or bound by a quantifier, comprehension, parameter list or `let`. The only free variable is `c` of the context-scope INV-001. The v26 additions are well typed and guarded: `resumes`, `resumesFrom` (with `s(i + 1)` guarded by `i < #s`) and `originalStart` (a finite set of start dates). |
| Scope sweep | I read in context every occurrence of record, enter, entry, input, persist, database, XML, serializ, encod, retention, answer, reminder, algorithm, obtained, comput, questionnaire, data-entry and "reported by". Each is an exclusion statement, a statement that a value comes from diary information without saying how, an instrument name, or a citation. `resumes` is a context property, like `preventiveFor`. |
| Predicate behaviour (`chain.py`, `chain2.py`) | The full v26 INV-001, INV-103 and INV-070 were evaluated on the R26-01 example, on fix 26's chain a → b → k, and on both with the first course's start unstated. Result: R27-01. |

## Remarks

### R27-01 Infidelity to Stage 1 / formal defect: for a resumed treatment whose first course has no stated start, INV-070 still admits a month off treatment as "the original pre-treatment baseline"
- **Item(s):**
  - E-008: the `originalStart` definition and its comment; the Notes paragraph **Resumed courses**.
  - INV-070: Predicate (baseline conjunct), Reading, Notes **Original baseline**.
  - E-049: Meaning; Notes **Resumed treatment**.
  - INV-001 Notes (**One stop or pause per course**, **Resumed courses**).
  - Traceability row OUT-022.
- **Problem:**
  - **What OUT-022 asks.** It asks (SHOULD) for the frequency after a stop, pause or reduction to be compared "with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible".
  - **What v26 does.** Fix 26 (R26-01) bounds the post-stop baseline by `originalStart(ctx, v.treatment)` and defines it as "the earliest start that the context states for t or for a course that t resumes".
  - **Where it fails.** The model admits preventive courses without a stated start (INV-001: "at most one start"; E-041 and E-055 Notes treat such courses). If the first course of a chain has no stated start, `originalStart` is the start of the next course of the chain, that is, the restart.
  - **The effect.** INV-070 then admits as "the original pre-treatment baseline" a month of the interval off treatment between the courses, or a month on the first course. These are exactly the outputs that R26-01 found contrary to OUT-022.
  - **The setting is realistic.** A patient who is already taking a preventive when the diary begins, pauses it and restarts it is this case. INV-103 requires the post-stop view of the restarted course, because that course has a start.
  - **The model claims the opposite.** Its own Notes state that the original baseline lies "before the start of the first course of that chain" and that "no month of an interval off treatment between the courses … stands for the original pre-treatment baseline". The predicate does not guarantee this.
- **Evidence:**
  - **Stage 1 OUT-022.**
    - Statement: "After a preventive treatment is stopped, paused or reduced, the diary output SHOULD continue to show headache and migraine frequency and compare it with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible."
    - Evidence [S-011]: "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal." The interval off treatment is the time of worsening.
    - Evidence [S-022]: "to detect possible rebound phenomena (i.e. frequency of migraine days per month going above its baseline)".
  - **The model text.**
    - E-008 `omn`: "originalStart(c, t): the start of the treatment of course t as it was first started: the earliest start that the context states for t or for a course that t resumes (resumesFrom)".
    - E-008 Notes: "`originalStart(c, t)` is the start of that first course or, where the context states no start for it, the earliest start that it states for a course of the chain".
    - INV-070 Predicate: `(∀ b ∈ v.baseline; s ∈ originalStart(ctx, v.treatment) • b.end < s)`.
    - INV-070 Notes: "for a course that resumes the treatment of an earlier course after its stop or pause (`resumes`), the start of the first course of that chain, so that no month of an interval off treatment between the courses, in which migraine may have worsened after the withdrawal ([S-011]), stands for the original pre-treatment baseline".
    - E-049 Notes: "the original pre-treatment baseline lies before the start of the first course of the chain (`originalStart`), not before the restart".
    - Row OUT-022: "a period that ends before the start of the first course of the chain (`originalStart`, E-008; INV-070), not with a period of the interval off treatment".
  - **Instances.** Evaluated with the v26 predicates as written (`chain2.py`; every INV-001 conjunct is checked).
    - **B: the R26-01 example with the first start unstated.**
      - Course t1 of topiramate has `doseChange(reduction)` on 15 March 2026 and `stop(paused)` on 30 June 2026, with no stated start: the patient was already taking it.
      - Course t2 of the same drug starts on 1 September 2026, with `doseChange(reduction)` on 1 October 2026. (t1, t2) ∈ `resumes`. The as-of date is 21 October 2026.
      - INV-001 admits the context. INV-103 requires the post-stop view of t2's reduction. `originalStart(t2) = {1 September 2026}`.
      - INV-070 admits August 2026 (the pause interval) and May 2026 (t1 on treatment, after its dated reduction) as the baseline.
    - **B2.** The same as B with t1's only event its pause. INV-070 again admits August 2026.
    - **Kn: fix 26's own chain a → b → k without a's start.**
      - Fix 26 used starts on 1 March 2025, 1 December 2025 and 1 September 2026. Here a has no stated start and has `stop(paused)` on 31 October 2025; b stops on 30 June 2026; k pauses on 15 October 2026.
      - INV-001 admits it, and INV-103 requires k's post-stop view. `originalStart(k) = {1 December 2025}`.
      - INV-070 admits November 2025, the pause month between a and b, as the original baseline. With a's start stated (fix 26's case), it is rejected.
    - **Contrast.** With the first start stated (the R26-01 example, and K), v26 rejects these months, as fix 26 reports.
  - **The defect is new to the loop, and the fix does not reverse an earlier one.**
    - R26-01's required change defined the original start as "the start of the first course of its chain of resumptions". It did not provide a fallback.
    - Fix 26 added the fallback and checked only that it is "never after the course's own start" (fixes/fix-iter-26.md, Checks). That is: it is not weaker than v25. It did not check the fallback against OUT-022's "original", nor against the INV-070 Notes sentence quoted above.
    - The change below keeps fix 26's link `resumes`, `resumesFrom`, the INV-001 conjuncts and the original-start bound for every chain whose first course states its start.
    - It touches none of the watch-point-4 items: the course-event dates, `atTimePoint`, `fitsMonthlyPeriod`, `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, `firstChangedDay` and the E-049 `when` clause of `onTreatmentPeriod`.
    - It touches none of the aligned items of watch point 9.
- **Required change:** make INV-070 exclude, as the original pre-treatment baseline of a resumed course, every period that the context places on or after the treatment was first started, also where the first course's start is not stated. Correct the texts that claim this. Either option meets this.
  - **Option (a): bound the baseline by every dated course event of the chain.**
    - Replace (or add to) the INV-070 baseline conjunct:
      `(∀ b ∈ v.baseline; u : Treatment; e ∈ ctx.subject.courseEvents • resumesFrom(ctx, u, v.treatment) ∧ e.treatment = u ⇒ b.end < e.date)`.
    - **Same result where the first start is stated.** Under INV-001 a stated start is not after any event of its course, and every later course of a chain states its start. So this bound equals the v26 bound wherever the first course states its start (the R26-01 example and K: identical verdicts in `chain2.py`).
    - **Where it is not stated.** The bound excludes every period that ends on or after a dated event of the treatment's history, in particular every interval off treatment between courses (B, B2 and Kn: August 2026 and November 2025 rejected).
    - **Text.** Correct the `originalStart` comment ("as it was first started") or replace its fallback. State in the Notes that, where the first start is not stated, the bound is the earliest dated event of the chain.
  - **Option (b): no fallback.**
    - Define `originalStart` as the start of the first course of the chain only, ∅ where that course states none.
    - Make E-049 `baseline` SHOULD `when originalStart(ctx, self.treatment) ≠ ∅`.
    - In INV-070, admit a baseline only where the original start is known (or, where it is not, apply option (a)'s bound).
    - State in the Notes that the original pre-treatment baseline of a treatment whose first start is not stated cannot be placed.
  - **Either way:**
    - Correct the E-008 Notes, the INV-070 Reading and Notes, the E-049 Meaning and Notes, the INV-001 Notes and row OUT-022, so that none claims more than the predicate.
    - Check satisfiability with INV-097. A baseline of the common length that ends before the bound always exists.
    - INV-056 and INV-068 need no change: OUT-018 and OUT-021 say "pre-treatment baseline", not "original".

## Checked and not raised

- **A course that is not resumed and has no stated start.**
  - INV-070's baseline and on-treatment bounds are vacuous for such a course, as INV-068's are. INV-103 does not require its post-stop view.
  - This is the model's general treatment of unstated starts: E-041 Notes, INV-064 Notes, E-055 `when` clauses. It is not raised.
  - Option (a) of R27-01 would also bound such a view's baseline by the course's dated events, if the fixer wishes.
- **The acute-treatment part of optimal control** ("with a satisfactory response to acute treatment, defined as pain-freedom within two hours from the intake"). It is not decided in INV-064, because [S-010] gives no share of attacks. Settled in review 03; INV-062 shows the values.
- **IHS 2024 Q5.** The stop rule ("less than four monthly migraine days over a period of three consecutive months", p. 12) is a reason to stop after success, not an evaluation time point or a response criterion. E-041 Notes list Q5 among the continuation periods. Not raised.
- **INV-046 Notes, "The two directions agree".** An output could show an indicator for a class the subject never used, with ≥ its level of days. INV-046 would then be unsatisfiable for that output, but the output states false medication days anyway. Excluding it is harmless, and no requirement is affected. Not raised.
- **Translations.** All 22 are faithful, including the five inline translations of E-041 Notes ([S-035] PDF pp. 82, 83 and 86; [S-033] p. 41).
- **Section 8.**
  - ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded, and their quotes are verbatim at the stated locations: [S-001] pp. 12, 42, 105, 122–125, 139, 190 and 209; NICE 1.3.9, 1.3.39 and 1.3.48; [S-034] p. 52.
  - Their descriptions of the passages are accurate.
  - No Stage 1 issue is worked around silently. R27-01 is a model defect, not a Stage 1 issue: OUT-022 states "original".
- **Search log.**
  - It has no entry for iteration 23; fix 23 made no search, so this is not a remark category (reviews 25 and 26).
  - The access dates and the URLs where quotes can be read are correct.
- **Settled points, not reopened (no new evidence):**
  - the HIT-6 one-month recall, HADS subscales only, the MIDAS labels and Grade IV undivided, "baseline administration", the HALT-90 total;
  - the "> 3 months" readings of INV-045 and INV-089; INV-106 at MUST NOT;
  - the E-041 readings, timings, ages and `excludes`;
  - "history of previous bouts"; empty `remissions` in chronic cluster headache (ISS-12);
  - INV-060 with INV-061 for short compared periods; `mostRecent` with 28-day periods;
  - comparison periods beyond the as-of date;
  - the by-dates relations and output-wide agreement (watch point 1); INV-008 and INV-111 (watch point 2);
  - the cluster view (watch point 3); `fillsPeriod` (watch point 5); the formulation ties (watch point 6); ISS-03 (watch point 7);
  - the two illustrative paraphrases in sections 1 and 3.3.
- **Oscillation watch points.**
  - R27-01 changes no item named in watch points 1 to 10 toward an earlier state. It keeps fix 25 (one stop per course; a restart is a new course) and fix 26 (the `resumes` link and the original-start bound).
  - It closes the one case in which the fix-26 fallback re-admits the R26-01 output.

## Notes on frozen items (for the human)

None.
