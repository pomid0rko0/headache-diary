# Review — iteration 28
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v27
Date: 2026-10-22

## Summary

This is the main review of iteration 28, by a new, independent reviewer. I checked v27 against its sources and against Stage 1 v18.

**State of the files.**
- `OUTPUT_MODEL.md` is v27 ("Version: v27 · Iteration: 27") and is byte-identical to `history/v27.md`.
- `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026), and the source table of section 5.
- v27, every section: notation, conformance, all 67 elements and 111 invariants, traceability, section 8, sources and search log; from the change log, the v26 and v27 entries.
- Review 27 and fixes 26 and 27 in full, the oscillation check after iteration 24 with its ten watch points, and the earlier loop passages on each point I considered raising: the INV-103 history from v00, fix 10, and the M-TOQ, PGIC and MSQ discussion of reviews 03, 04 and 19b.

**Result.**
- **Citations.** I downloaded every source that carries a Stage 2 quote and found every quoted fragment verbatim at its stated location. Translations, metadata and versions are correct. ICHD-3 is still the current edition.
- **Values.** All value sets, ranges, bands, code labels, reference levels, offsets, thresholds and control levels match their sources.
- **Scope.** The model has no input, storage or input-derivation content. Every threshold, formula and computed field that is part of the output data is present and cited.
- **Mechanical checks.** All pass.
- **Fidelity.** 37 of the 39 requirements are fully represented at their Stage 1 strengths. Two remarks concern **preventive courses whose start the context does not state**, a case the model admits (INV-001: "at most one start"; for example a treatment the subject was already taking). Fix 27 decided this case for one item only: E-049's original baseline is not admitted where the start is not stated. The neighbouring items still treat the case in a way that does not fit Stage 1:
  - **R28-01 (OUT-022).** INV-103 drops the whole post-stop view for such a course, including the parts that do not depend on the start. When the view is shown anyway, INV-070 leaves its "on-treatment period" unbounded, so a month after the stop can be shown as the on-treatment period.
  - **R28-02 (OUT-021).** INV-068 (MUST) admits any period, including a month on treatment, as the "pre-treatment baseline" of a treatment review view of such a treatment.

Neither remark reverses an earlier fix or touches an item of watch points 1 to 10 toward an earlier state (see "Checked and not raised").

## Verification coverage

### Downloads and tools

- **Where.** Every source was downloaded fresh with `curl` through the proxy into the session scratchpad folder `r28/src` (under `/tmp`, outside the repository). Texts went to `r28/txt` and rendered pages to `r28/img`.
- **HTTP.** All requests returned HTTP 200, with two exceptions, each resolved:
  - [S-007] (discovery.ucl.ac.uk) returned HTTP 520 twice, and the alternate URLs returned 403 and 520. The third attempt at the Stage 1 URL returned HTTP 200 (39-page PDF).
  - [S-033] (apicr.minzdrav.gov.ru): the connection was reset by the peer once; the second attempt returned the official 92-page PDF.
- **Scripts.** All are in `r28/scripts` and were run with `python3 -I`:
  - `html2txt.py`, `quotes.py`, `pages.py` and `others.py` for the quote checks;
  - `mech.py` and `names.py` for the mechanical checks;
  - `unstated.py` for the predicate checks of R28-01 and R28-02.
- **Extraction.** PDFs page by page with `pdftotext -raw` and `-layout`. HTML pages and Europe PMC full-text XML with the markup stripped.
- **Matching.** NFKC normalisation; soft hyphens removed; case folded; letters and digits only, which joins line-end hyphens.
- **Rendered and read:**
  - [S-001] p. 190: A1.1.1 criterion B, "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)", and note 2. The text layer maps "±" and "−" to control glyphs and "+" to "þ".
  - [S-034] p. 1, an image: "Возрастная группа" followed by "дети".

### Quote check per source

**Method.**
1. Every double-quoted string outside the `omn` blocks and before the search log was taken: 748 fragments, after splitting at "[...]" and keeping fragments of at least 6 letters or digits.
2. Each fragment was attributed to the nearest preceding source tag on its line and searched page by page in that source.
3. Fragments not found there were searched in Stage 1 v18 and then in every downloaded source.
4. The page of every hit was compared with the location the model states (`pages.py`). Each of the 39 fragments found in another source than the nearest preceding tag was read in its line (`others.py`). All are cited to the source in which they were found (the tag follows the quote), or they repeat a fragment already verified.

| Source | Fragments checked | Verbatim at stated location | Not found | Unreachable (tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (PDF, 211 pp.) | 66 | 66 (64 in the text layer; 2 with ± and − read on rendered p. 190) | 0 | — |
| S-007 IHS cluster (UCL accepted manuscript, 39 pp.) | 5 | 5 (the ≥ 14 attacks fragment, section 2.2, p. 10) | 0 | HTTP 520 twice, alternate URLs 403/520; third attempt HTTP 200 |
| S-008 IHS 2024 preventive (univaq PDF, 31 pp.) | 14 | 14 | 0 | — |
| S-010 IHS 2025 position statement (univaq PDF, 11 pp.) | 29 | 29 | 0 | — |
| S-011 EHF 2022 (Europe PMC XML) | 9 | 9 | 0 | — |
| S-012, S-013 (Europe PMC XML) | 1 + 1 | 2 | 0 | — |
| S-014 EHF/LTB aids (Europe PMC XML) | 27 | 27 | 0 | — |
| S-015 NICE CG150 (Recommendations and Overview pages) | 25 | 25 | 0 | — |
| S-016 SIGN 155 (PDF, 64 pp.) | 6 | 6 (PDF p. = printed p. + 6) | 0 | — |
| S-018 AAN/AHS clinician summary (PDF, 12 pp.) | 8 | 8 | 0 | — |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML) | 4 | 4 | 0 | — |
| S-028 NVN module (web page) | 7 | 6 + 1 English translation | 0 | — |
| S-033 Russian adults (official PDF, 92 pp.) | 22 | 18 + 4 English translations | 0 | connection reset once; second attempt HTTP 200 |
| S-034 Russian children (official PDF, 53 pp.) | 13 | 8 + 4 English translations + 1 on the rendered title page | 0 | — |
| S-035 Turkish protocol (PDF, 92 pp.) | 40 | 27 + 13 English translations | 0 | — |
| S-101 HIT-6 validation (Europe PMC XML) | 4 | 4 | 0 | — |
| S-102 AMPP menses / MIDAS (Europe PMC XML) | 4 | 4 | 0 | — |
| S-103 PedMIDAS page (Cincinnati Children's) | 10 | 10 | 0 | — |
| S-104 HADS (Europe PMC XML) | 3 | 3 | 0 | — |
| S-105 PHQ/GAD-7 manual (PDF, 9 pp.) | 3 | 3 (P. 6/9) | 0 | — |
| S-106 NICE TA260 (chapters 1 and 2, overview) | 2 | 2 | 0 | — |
| Fragments cited to the source in which they were found, behind a following tag (`others.py`) | 39 | 39 | 0 | — |
| Stage 1 quotes reused by reference (S-002, S-005, S-022, S-030, S-032, S-042 and others) | 390 | 390 verbatim in Stage 1 v18 (evidence carries over) | 0 | not re-downloaded; no Stage 2 quote depends on them |
| Model-internal phrases (for example "output model notation", "K is available when C", ISS-06's proposed wording) | 16 | not source quotes | — | — |

**Translations.** I read all 22 English translations against their originals ([S-028] PICO; [S-033] title page, section 3.3 comment, BTA recommendation and the p. 41 sentence; [S-034] flowchart, title page and section 2; [S-035] Kutu 8 items, sections 3.3 b, 3.6.3.9, 6, 7.1 and 7.3, and the chapter 7 heading). All are faithful.

### Metadata and versions

- **PubMed esummary.**
  - S-101: PMID 20819842, Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMC3057423; authors Yang, Rendas-Baum, Varon, Kosinski.
  - S-102: PMID 25902814, J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMC4406925; seven authors, including Stewart and Lipton.
  - S-104: PMID 12914662, Health Qual Life Outcomes 2003;1:29, DOI 10.1186/1477-7525-1-29, PMC183845; Snaith.
  - S-103 developer paper: PMID 11739822, Neurology 2001;57(11):2034–9, DOI 10.1212/wnl.57.11.2034.
- **S-103.** Page footer "© 2026 Cincinnati Children's Hospital Medical Center".
- **S-105.** PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
- **S-106.** "Published: 27 June 2012", "Last reviewed: 11 January 2016". Chapter 1 has "less than a 30% reduction in headache days per month after 2 treatment cycles"; chapter 2 has the re-treatment "every 12 weeks" sentence.
- **S-015.** "Published 19 September 2012", "Last updated 03 June 2025". The overview page also shows "Last reviewed: 23 September 2026" (links to technology appraisal guidance added). Every quoted recommendation is unchanged.
- **Newer versions.** A web search finds no published ICHD-4, only "Work in Progress" papers and a September 2025 IHS workshop; [S-001] is current. No other source has a newer version that changes an element.

### Values checked against sources

- **E-009 and E-028.** The code labels are verbatim on pp. 8, 9 and 12; 8.2.6 criterion B is the source of `classesOf826`.
- **E-032.** Reference levels: 15 days per month for 8.2.3, and 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8. The time span is more than three months (pp. 122–125).
- **E-041.** All 18 rules match their sources: offsets, anchors, timings, ages and `excludes`.
- **E-045, E-046.** The thresholds of NICE 1.3.28 and 1.3.29, IHS Q6 (including the MIDAS and HIT-6 improvements and the ≥ 30 % chronic alternative), DMKG/ÖKSG/SKG, the Russian section 7.1 and Turkish Kutu 8, and the four control levels of [S-010].
- **E-057.** HIT-6 36–78 and its four categories; MIDAS grades I–IV with a three-month recall; PedMIDAS bands; the HALT-90 table, with its overlap at 20; HALT-30 without grading.
- **E-059.** HADS, PHQ-9 and GAD-7 ranges.
- **E-039, E-060, E-063.** NICE 1.3.48 (4–8 weeks), ICHD-3 A1.1 (day 1 ± 2, no day 0), and the remission period that "must exceed three months".
- **ISS-02.** Page-by-page search of the ICHD-3 text layer: "simple analgesic" occurs only on p. 139.
- **Date examples in the prose.** Recomputed by script, all correct: 67 days (E-007); 26 March, and 26 February – 25 March as 28 days (E-042, INV-055); 4–31 December as 28 days; 6 April and day 43 (INV-049); 42 and 143 days (E-063).

### Fidelity check per Stage 1 requirement

| OUT | Statement parts and Caveats checked | Result |
|---|---|---|
| 001 | Period with start, end and length (E-003, E-005, INV-002, INV-003, MUST); monthly frequency outputs (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); Caveat (stated length) | OK |
| 002 | Definition label for every form in which a view reports a measure (INV-008, `reports`); one definition per view (INV-111) | OK |
| 003 | Indicator next to every summary measure (INV-011, INV-012); SHOULD NOT a validated cut-off (INV-013); Caveat | OK |
| 004–007 | Per period over the selected range, ICHD-3 definitions, attacks separate; MUST, MUST, SHOULD and SHOULD, with the OUT-001 MUST where provided (INV-009, INV-010, INV-014 to INV-017, INV-108) | OK |
| 008 | MAY measures; exploratory annotation MAY (E-020 to E-022) | OK |
| 009 | Series with start, dose-change and stop markers in the view; weekly values where relevant (INV-034 to INV-036) | OK |
| 010, 011 | Intensity on a stated scale, compared between periods (INV-018, INV-032, INV-039); duration, with the treated-attack label SHOULD and the Caveat as SHOULD NOT (INV-019 to INV-021) | OK |
| 012, 013 | Across periods and per treated attack (INV-022, INV-072, INV-076); aura MAY (E-027) | OK |
| 014–016 | Total, class and drug (INV-023, INV-024); weekly view (INV-025); indicator per period, class and 8.2.6 with code, level and span, prompt MUST, diagnosis MUST NOT, interpretation caveat (INV-044 to INV-048, INV-100) | OK |
| 017 | From the start of withdrawal, review window, the following year, worsening label (INV-049 to INV-052) | OK |
| 018 | Comparison per preventive treatment with values and both changes (INV-053 to INV-057); time points by type and population (E-041, INV-055, INV-058, INV-059); Caveat (INV-106) | OK |
| 019, 020 | Residual burden (INV-060, INV-061); labels with criterion, values and other values, not the sole indicator (INV-062 to INV-065) | OK |
| 021 | MUST and SHOULD components for the same periods (INV-068, INV-069, INV-102) | **R28-02**: the "pre-treatment baseline" of a view of a treatment whose start is not stated is unbounded |
| 022 | Post-stop view: the frequency after the event, the on-treatment period and the original pre-treatment baseline (E-049, INV-070, INV-103) | **R28-01**: no view is required for a course whose start is not stated, and the on-treatment period of such a view is unbounded |
| 023, 024 | Acute outcomes, consistency, timing, formulation, phases, 15 minutes for cluster headache, Caveat (INV-071 to INV-075, INV-107); treatment history (INV-077 to INV-079, INV-109) | OK |
| 025, 039 | Scheme windows MAY (E-056, INV-080); adherence next to the comparison, in the history and in the clinician summary (INV-066, INV-067, INV-104, INV-109) | OK |
| 026, 027 | Instrument results with name, date, recall, score, grading and change (INV-081, INV-082); functional impact and its comparison with the baseline (INV-026, INV-027) | OK |
| 028–031 | Three-month view: its MUST, SHOULD and SHOULD NOT parts (INV-040 to INV-043); values per headache type (INV-028 to INV-030); menstrual view MUST (INV-086, INV-087); cluster view (INV-088, INV-089) | OK |
| 032–038 | Trigger caveats; screening; clinician and patient views; paediatric (a)–(d) and Caveat; composite index; interpretive caveats (INV-083 to INV-101, INV-104, INV-105, INV-110) | OK |

Every conformance level matches the strength of the Stage 1 statement part it realises. MUST NOT is used for OUT-016 and the OUT-018 Caveat, and SHOULD NOT for the SHOULD parts and Caveats.

### Mechanical checks (`mech.py`, `names.py`, `unstated.py`)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn, section 9). |
| References | No dangling E-, INV- or ISS- reference. All OUT references exist in Stage 1 (39). The 37 cited source IDs are within S-001–S-046 or S-101–S-106, and S-101 to S-106 are all cited. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`, and every invariant states its scope. |
| Names | 182 `omn` blocks; 554 declared names, none declared twice. Every identifier in the blocks is declared, is an attribute, a primitive or a semantic constant, or is bound by a quantifier, comprehension, parameter list or `let`: 0 unresolved tokens. |
| Scope sweep | I read in context every occurrence of record, enter, entry, input, captur, persist, database, XML, serializ, encod, retention, reminder, algorithm, answers, data-entry, storage and stored. Each is an exclusion statement, an out-of-scope statement about scoring, the notation's "records", a search-log tool name, or the [S-014] HALT-30 sentence quoted for the recall period. |
| v27 claims (`originalStart`) | The v27 E-008, E-049 and INV-070 claims hold for resumed chains. `originalStart` has at most one member; it equals `startOf` for a course that resumes no course; and chains are acyclic, by the INV-001 conjuncts (start ≤ stop < next start). |
| Courses without a stated start (`unstated.py`) | The predicates were evaluated as written in v27 on course t1 of fix 27's example B (no stated start, `doseChange(reduction)` 15 March 2026, `stop(paused)` 30 June 2026, as of 21 October 2026), and on the same course with a start on 1 January 2026.<br>• **No stated start.** INV-103 requires no view of either event. INV-070 admits a view of the pause whose "on-treatment period" is August 2026. INV-068 admits a treatment review view whose "pre-treatment baseline" is April 2026.<br>• **Stated start.** INV-103 requires both views. INV-070 rejects August 2026 and accepts June 2026. INV-068 rejects April 2026.<br>Result: R28-01, R28-02. |

## Remarks

### R28-01 Infidelity to Stage 1 / formal defect: post-stop monitoring (OUT-022) of a preventive course whose start the context does not state is not required, and when shown, its "on-treatment period" is unbounded

- **Item(s):**
  - INV-103: Predicate and Reading.
  - INV-070: Predicate (the on-treatment conjunct), Reading and Notes.
  - E-049: Conformance; Notes, the paragraph on the on-treatment period and **Original start not stated**.
  - Row OUT-022.
- **Problem:**
  1. **INV-103 drops the whole view, not only what depends on the start.**
     - **What INV-103 requires.** A post-stop view, but only where `startOf(c, e.treatment) ≠ ∅`.
     - **What OUT-022 conditions on.** Nothing about a known start. Of what it asks, only "the original pre-treatment baseline" depends on the start.
     - **Fix 27 already handles that part.** E-049 `baseline` is SHOULD `when originalStart(ctx, self.treatment) ≠ ∅`, and INV-070 admits no baseline otherwise.
     - **The rest does not depend on the start:**
       - "continue to show headache and migraine frequency" is shown by the periods from `firstChangedDay`, which is computed from the event alone (E-049 `after`);
       - the comparison with "the on-treatment period" is a comparison with a period before the changed regimen, within the course.
     - **The justification does not fit.** E-049 Notes justify the gap by counting INV-103 among "the other content aligned to a start". But the post-stop view is aligned to its event (`eventOn`, `firstChangedDay`), not to the start.
     - **The case is the core case of OUT-022.** It is a patient already on a preventive whose start the context does not state, and who stops, pauses or reduces it. Two examples:
       - **Fix 27's own example B.** t1 is already being taken, reduced on 15 March 2026 and paused on 30 June 2026. The subject restarts as t2 on 1 September, the [S-011] situation "restarting the treatment if migraine worsens after treatment withdrawal". v27 requires no post-stop view of t1's pause, so the months after it (July and August), in which the worsening occurs, are compared with the on-treatment period in no required view. The views of t2 begin on 1 October (its reduction).
       - **Discontinuation trials.** The trials of OUT-022's evidence, [S-030] and [S-023], are made on a prophylaxis that is already running.
  2. **When the view is shown, INV-070 does not bound its on-treatment period.**
     - **The conjunct.** It is `(∀ q ∈ v.onTreatmentPeriod; s ∈ startOf(ctx, v.treatment) • s ≤ q.start ∧ q.end < x)`. Where `startOf` is empty, both bounds are vacuous, including `q.end < x`.
     - **The effect.** A view of such a course may show a period after the stop as "the on-treatment period" and still satisfy INV-070 (`unstated.py`: August 2026 is accepted for t1's 30 June pause).
     - **Why this matters for OUT-022.** A comparison of the months after the stop with a month after the stop labelled "on treatment" hides the worsening or rebound that OUT-022 exists to show. This is the same reasoning by which fix 27 excluded an unplaceable original baseline.
     - **The model claims the opposite.** E-049 Notes say that an on-treatment period "ends before the first day of the changed regimen (INV-070) [...] So it lies within the course". The predicate does not guarantee this where the start is not stated.
- **Evidence:**
  - **Stage 1 OUT-022.**
    - Statement: "After a preventive treatment is stopped, paused or reduced, the diary output SHOULD continue to show headache and migraine frequency and compare it with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible."
    - [S-011] "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal."
    - [S-030] "Ved effekt bør medicinen forsøges seponeret hver 6-12 måneder for at sikre, at der fortsat er behov for og effekt af medicinen." Translation: "If effective, discontinuation of the medication should be attempted every 6–12 months to ensure that there is still a need for, and an effect of, the medication."
    - [S-023] "Es hat sich bewährt, im Verlauf einer Therapie die fortbestehende Indikation für eine wirksame Prophylaxe durch einen Absetzversuch oder die Reduktion der Dosis, oder die Verlängerung des Dosierungsintervalls zu überprüfen." Translation: "It has proved useful, in the course of therapy, to check whether an effective prophylaxis is still indicated by a discontinuation trial, a dose reduction or an extension of the dosing interval."
  - **Model text (v27).**
    - INV-103 Predicate: `∀ c ∈ Ctx; e ∈ c.subject.courseEvents • e.treatment ∈ c.subject.preventiveTreatments ∧ startOf(c, e.treatment) ≠ ∅ ∧ (e.kind is stop ∨ e.kind = doseChange(reduction)) ⇒ …`.
    - E-049 Notes: "The same holds for the view of a stop, pause or reduction of a course whose own start the context does not state, which resumes no course (INV-001) and whose view INV-103 does not require. So the model asks for the original pre-treatment baseline where the context states the original start, as it asks for the other content aligned to a start where the context states that start (the on-treatment period here; INV-055, INV-056, INV-102, INV-103; E-055 Notes)."
    - E-049 `after : seq →Period SHOULD -- consecutive periods from the first day of the changed regimen onward`, and `firstChangedDay(k, d)`, which reads only the event's kind and date.
    - INV-070 Predicate: `(∀ x ∈ firstChangedDay(v.event, v.eventDate) • (∀ q ∈ v.onTreatmentPeriod; s ∈ startOf(ctx, v.treatment) • s ≤ q.start ∧ q.end < x) ∧ …)`.
    - E-049 Notes: "An on-treatment period before the event begins on or after the treatment start and ends before the first day of the changed regimen (INV-070) [...] So it lies within the course".
    - Fix 27 ("Everything else OUT-022 asks for stays required for this patient"): "the post-stop view of each stop, pause or reduction of every course with a stated start". For the course whose start is not stated, which is the patient's first course, nothing is required.
  - **Script (`unstated.py`), predicates as written in v27.**
    - **t1 without a stated start.** INV-103 requires no view of its 15 March reduction or its 30 June pause. INV-070 accepts a pause view whose on-treatment period is 1–31 August 2026, with periods after the pause from 1 July.
    - **The same course started on 1 January 2026.** INV-103 requires both views. INV-070 rejects August and accepts June 2026.
  - **Partial cover only.** The time-course view marks the pause (INV-035), but it asks for no comparison with the on-treatment period, and E-049 is the model's realisation of OUT-022.
  - **Not earlier settled.** The `startOf` conjunct of INV-103 is unchanged since v00. No remark or fix argued for it; fix 10 changed only its Reading.
    - **Review 27** set the case aside as "the model's general treatment of unstated starts".
    - **Fix 27 has since changed that treatment for this view.** Where the start is not stated it now excludes the unplaceable baseline but keeps the placeable content, and it argued only about the baseline.
    - **No reversal.** The change below keeps fix 25, fix 26 and fix 27, section 2.8, `firstChangedDay` and the E-049 `when` clauses (watch point 4).
- **Required change:**
  1. **INV-103.** Remove the conjunct `startOf(c, e.treatment) ≠ ∅`, so that the view is available for every stop, pause or dose reduction of every preventive course.
     - **The `when` clauses of E-049 stay as they are.** For a course whose start is not stated, the view then asks (SHOULD) for the periods from the first changed day, and for no original baseline (fix 27) and no on-treatment period (the unchanged `when` clause).
     - **Satisfiable.** A view with periods after the event only meets INV-070, INV-097, INV-003 and INV-011.
  2. **INV-070.** Make the on-treatment period end before the first changed day whatever the start, and bound its first day. Either option meets this.
     - **Option (a): admit an on-treatment period only where a start is stated**, in the form fix 27 gave the baseline conjunct:
       `(∀ q ∈ v.onTreatmentPeriod • (∃ s ∈ startOf(ctx, v.treatment) • s ≤ q.start) ∧ ∀ x ∈ firstChangedDay(v.event, v.eventDate) • q.end < x)`.
       Verdicts are identical wherever a start is stated.
     - **Option (b): bound the period by the dated course events.** Where no start is stated, bound `q.start` below by the earliest course event of the course that is dated on a day of the course: a dose change, the date the target or tolerated dose was reached, or the stop or pause (section 2.8); a cycle end is excluded, because it can fall after the stop.
       - If the fixer also wants that period asked for, add to the `when` clause of `onTreatmentPeriod` a disjunct for courses without a stated start only.
       - The stated-start cases of watch point 4 (a stop or a reduction on the start day) must stay unchanged.
  3. **Text.** Correct, so that none claims more than the predicate:
     - the INV-103 Reading;
     - the E-049 Conformance and Notes, in particular the sentence that INV-103 does not require the view of a course whose own start is not stated, and the list "INV-102, INV-103";
     - the INV-070 Reading and Notes;
     - row OUT-022.

### R28-02 Formal defect / infidelity to Stage 1: INV-068 admits any period, including a month on treatment, as the "pre-treatment baseline" (OUT-021) of a treatment review view of a treatment whose start the context does not state

- **Item(s):**
  - INV-068: Predicate (the start conjunct), Reading and Notes.
  - E-048: Notes.
  - Row OUT-021, if its coverage text is affected.
- **Problem:**
  - **The conjunct.** INV-068 (MUST) ties the periods to the start by `(∀ s ∈ startOf(ctx, v.treatment) • v.baseline.end < s ∧ ∀ p ∈ ran v.onTreatment • s ≤ p.start)`. Where the context states no start, it is vacuous.
  - **The effect.** INV-102 does not require a view for such a treatment, but nothing excludes one, and INV-068 accepts it with any baseline. In `unstated.py`, course t1 of example B has a dated dose reduction on 15 March 2026, which places it on treatment from that day (section 2.8: "a dose change [...] dated on the first day at the new dose"). A view of it with April 2026 as the "pre-treatment baseline" and June 2026 as the on-treatment period satisfies INV-068. Its on-treatment periods may likewise begin before the course began.
  - **Why this matters for OUT-021.** Comparing an on-treatment month, presented as the pre-treatment baseline, with an on-treatment month hides the treatment effect that OUT-021 presents "so that efficacy can be judged".
  - **The model claims the opposite.**
    - The INV-068 Reading states "a baseline period that ends before the treatment start, and on-treatment periods that begin on or after it".
    - The E-048 Notes state "The on-treatment periods lie within the course: they begin on or after the treatment start".
    - The predicate guarantees neither where the start is not stated.
- **Evidence:**
  - **Stage 1 OUT-021 (MUST).** "For treatment review, the diary output MUST present together, for the same pre-treatment baseline and on-treatment periods, headache days (OUT-004), migraine days (OUT-005) and acute medication days (OUT-014). [...] The purpose is that efficacy can be judged across these dimensions and against the patient's own goals."
  - **Model text (v27).** The INV-068 Predicate and Reading and the E-048 Notes, quoted above.
  - **New evidence since review 27, which set the case aside** ("INV-070's baseline and on-treatment bounds are vacuous for such a course, as INV-068's are [...] This is the model's general treatment of unstated starts"):
    - **Fix 27 changed that treatment for the E-049 baseline.** It now admits none where the start is not stated, on the ground that "No period can be placed before the original start. Every month before a restart or before the first dated event may lie in the pause or on the first course", and that "v27 excludes only outputs that present such a period as the original baseline" (fixes/fix-iter-27.md).
    - **The model now treats one situation in two opposite ways.** v27 excludes an unplaceable baseline in E-049 and INV-070, but keeps admitting it in INV-068. Here the baseline is a "pre-treatment" one rather than an "original" one, and it is required at MUST rather than SHOULD.
    - **The rest of the model agrees with the exclusion.** INV-056 already admits no response comparison for a treatment without a stated start (`rc.treatmentStart ∈ startOf(ctx, rc.treatment)`), and INV-102 requires no review view for one.
  - **Script (`unstated.py`).**
    - **No stated start.** INV-068 accepts April 2026 as the baseline.
    - **Start stated on 1 January 2026.** It rejects April 2026.
- **Required change:**
  - **INV-068.** Replace the start conjunct by the form fix 27 gave the INV-070 baseline conjunct:
    `(∃ s ∈ startOf(ctx, v.treatment) • v.baseline.end < s ∧ ∀ p ∈ ran v.onTreatment • s ≤ p.start)`.
    - **What it admits.** A treatment review view only for a treatment whose start is stated. That is exactly where INV-102 requires one and where INV-056 admits the response comparison of the same treatment.
    - **Unchanged verdicts.** Wherever a start is stated, so INV-069, INV-097 and INV-102 stay satisfiable (fix 18's construction).
    - **An equivalent alternative.** A definitional conjunct in E-048 stating that a treatment review view exists only for a treatment with a stated start.
  - **Keep** the `notStoppedBefore` conjunct (watch point 4).
  - **Text.** Correct the INV-068 Reading and Notes and the E-048 Notes. State that no treatment review view is shown for a treatment whose start the context does not state, because no period can be placed before that start.

## Checked and not raised

- **Other start ties that are vacuous without a stated start.** They are not raised. In each case a SHOULD invariant already needs a response comparison, which INV-056 admits only with a stated start, so such content cannot meet the model's own SHOULD:
  - INV-064, the control-level months;
  - INV-067, the adherence window;
  - INV-109, an acute line's summary period (stated in its Notes).
- **M-TOQ, PGIC and MSQ v2.1 categories untabulated (E-057).** Settled in review 19b (the developer papers use different versions; Stage 1 names none). No new evidence.
- **INV-060 with INV-061 for compared periods shorter than a month**, for example weekly percentage changes. Settled (review 27 list). Not reopened.
- **The [S-014] HALT-30 sentence with "records".** It is quoted for the instrument's recall period, an output element, not for data collection. Not a scope violation.
- **The NICE CG150 overview** shows "Last reviewed: 23 September 2026". The recommendations page is still "Last updated 03 June 2025", and every quoted recommendation reads as quoted. No newer content changes an element.
- **v27 `originalStart` (fix 27).**
  - The definition matches its comment and the Notes.
  - E-049's `when` clause for `baseline` coincides with the condition under which INV-070 admits a baseline.
  - The INV-070 Notes claim, that every baseline shown ends before the start of the view's own course, holds.
- **Section 8.**
  - ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded.
  - Their quotes are verbatim at the stated locations: [S-001] pp. 12, 42, 105, 122–125, 139, 190 and 209; NICE 1.3.9, 1.3.39 and 1.3.48; [S-034] p. 52.
  - Their descriptions of the Stage 1 passages are accurate.
  - R28-01 and R28-02 are model defects, not Stage 1 issues: OUT-021 and OUT-022 are clear, and the model can meet them.
- **Settled points, not reopened (no new evidence):**
  - the HIT-6 one-month recall; HADS subscales only; the MIDAS labels and Grade IV undivided;
  - the "> 3 months" readings of INV-045 and INV-089; INV-106 at MUST NOT;
  - the E-041 readings, timings, ages and `excludes`;
  - empty `remissions` in chronic cluster headache (ISS-12);
  - `mostRecent` with 28-day periods; comparison periods beyond the as-of date;
  - the by-dates relations and INV-111 (watch points 1 and 2); the cluster view (3); `fillsPeriod` (5); the formulation ties (6); ISS-03 (7).
- **Oscillation watch points.**
  - **R28-01** keeps every watch-point-4 item byte-identical in its option (a): the course-event dates, `atTimePoint`, `fitsMonthlyPeriod`, `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, `firstChangedDay` and the `when` clause of `onTreatmentPeriod`. Option (b) would extend that clause only for courses without a stated start, a case that fixes 02 and 17 did not concern.
  - **R28-02** keeps `notStoppedBefore` in INV-068.
  - **Neither remark** touches the items aligned in v22–v24 (watch point 9), and neither returns any item to an earlier state. Both extend fix 27's decision on unstated starts to the two neighbouring items that it did not examine.

## Notes on frozen items (for the human)

None.
