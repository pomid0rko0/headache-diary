# Review — iteration 29
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v28
Date: 2026-10-22

## Summary

This is the main review of iteration 29, by a new, independent reviewer. I checked v28 against its sources and against Stage 1 v18.

**State of the files.**
- `OUTPUT_MODEL.md` is v28 ("Version: v28 · Iteration: 28") and is byte-identical to `history/v28.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026), and the source table of section 5.
- v28, sections 1–10 in full (notation, conformance, all 67 elements and 111 invariants, traceability, section 8, sources); sections 11 and 12 for the iteration-28 entries.
- Review 28, fix 28 and the oscillation check after iteration 28, with its seven watch points.
- The earlier loop passages on each point I considered raising: fix 18 (adherence windows after a stop), reviews 16 and 24 (caregiver days), reviews 18, 20 and 22 (periods beyond the as-of date), fixes 27 and 28 (Stage 1 issue for unstated starts).

**Result.**
- **Citations.** I downloaded every source that carries a Stage 2 quote. Every quoted fragment is verbatim at its stated location. Translations, metadata and versions are correct. ICHD-3 is still the current edition.
- **Values.** All value sets, ranges, bands, code labels, reference levels, offsets, thresholds and control levels match their sources.
- **Scope.** The model has no input, storage or input-derivation content. Every threshold, formula and computed field that is part of the output data is present and cited.
- **Mechanical checks.** All pass.
- **Fidelity.** All 39 requirements are represented at their Stage 1 strengths.
- **v28 changes.** I checked fix 28's predicates (`courseBegunBy`, INV-064, INV-067, INV-068, INV-070, INV-078, INV-079, INV-103, INV-109) by script against the prose that describes them. Every claim holds except one.
- **The remark.**
  - **R29-01** concerns a Notes sentence that fix 28 added to INV-067.
  - The sentence says that an adherence summary of a course without a stated start "still refers to days that the context places on the course".
  - The predicate bounds only the first day of the window from below. It admits a window that lies wholly after the stop or pause.
  - The required change is to the text only. It changes no predicate and reverses no fix (see the remark, and "Checked and not raised", oscillation watch points).

## Verification coverage

### Downloads and tools

- **Where.**
  - Sources: fresh `curl` downloads through the proxy into the session scratchpad folder `r29/src` (outside the repository).
  - Text: per-page `pdftotext -raw` and `-layout`, or HTML/XML with the markup stripped, in `r29/txt`.
  - Rendered pages: `r29/img`.
- **HTTP.** All requests returned HTTP 200, with one exception. [S-033] (apicr.minzdrav.gov.ru) reset the connection once; the retry returned the official 92-page PDF.
- **Scripts.** All are in `r29/scripts` and were run with `python3 -I`:
  - `extract.py`, `quotes.py`, `nf.py`, `loc.py` and `tally.py` for the quote checks;
  - `mech.py` and `names.py` for the mechanical checks;
  - `claims28.py` for the v28 prose claims.
- **Matching.** NFKC normalisation, soft hyphens removed, case folded, letters and digits only. This joins line-end hyphens and drops the ICHD-3 glyphs that have no text mapping ("≥", "±", "−").
- **Rendered and read:**
  - [S-001] p. 190: A1.1.1 and A1.1.2 criterion B, "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)" and "Occurring on day 1 ± 2 (i.e. days −2 to +3)"; note 2 "day −1; there is no day 0".
  - [S-001] p. 124: "≥10 days/month for >3 months" in 8.2.4, 8.2.5 and 8.2.6 criterion B, and "≥15" in 8.2.3.2.
  - [S-034] p. 1 (an image): "Возрастная группа" followed by "дети".

### Quote check per source

**Method.**
- Every double-quoted string in sections 1–10 outside the `omn` blocks: 750 fragments, after splitting at "[...]" and keeping fragments of at least 6 letters or digits.
- Each fragment was attributed to the nearest preceding source tag on its line and searched page by page in that source.
- Fragments not found there were searched in Stage 1 v18 and then in every downloaded source.
- For PDF sources, the page of every hit was compared with the location the model states (`loc.py`). There were no mismatches.

| Source | Fragments | Verbatim at stated location | Not found | Unreachable (tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (PDF, 211 pp.) | 68 | 64 in the text layer + 3 on rendered p. 190; 1 is Stage 1 text | 0 | — |
| S-007 IHS cluster (UCL accepted manuscript, 39 pp.) | 6 | 5 (pp. 10, 22, 25); 1 Stage 1 text | 0 | — |
| S-008 IHS 2024 preventive (univaq PDF, 31 pp.) | 18 | 14 (pp. 5, 6, 9, 12, 13); 4 Stage 1 text | 0 | — |
| S-010 IHS 2025 position statement (univaq PDF, 11 pp.) | 34 | 29 (p. 6 and headings); 5 Stage 1 text | 0 | — |
| S-011, S-012, S-013 (Europe PMC XML) | 18 + 1 + 2 | 11; the rest Stage 1 text or correctly attributed to a source named after the quote | 0 | — |
| S-014 EHF/LTB aids (Europe PMC XML) | 33 | 27; 6 Stage 1 text | 0 | — |
| S-015 NICE CG150 (Recommendations and Overview pages) | 32 | 25, including recs 1.3.9, 1.3.24, 1.3.26 (with the TA260 sentence), 1.3.27–1.3.29, 1.3.39 and 1.3.48 under these numbers; 6 Stage 1 text; 1 attributed after the quote | 0 | — |
| S-016 SIGN 155 (PDF, 64 pp.; PDF p. = printed p. + 6) | 8 | 6 (PDF pp. 7, 20) | 0 | — |
| S-018 AAN/AHS clinician summary (PDF, 12 pp.) | 11 | 8 (pp. 1, 7, 8) | 0 | — |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML) | 5 | 4; 1 Stage 1 text | 0 | — |
| S-028 NVN module (web page) | 9 | 6, including the PICO "P: Patiënten (kinderen en volwassenen) ..." under "Zoeken en selecteren"; 1 translation | 0 | — |
| S-033 Russian adults (official PDF, 92 pp.) | 44 | 18 (pp. 1, 4, 39, 40, 41, 53); 4 translations; the rest Stage 1 text or attributed after the quote | 0 | connection reset once; retry HTTP 200 |
| S-034 Russian children (official PDF, 53 pp.) | 16 | 8 (pp. 17, 52) + 1 on rendered p. 1; 4 translations | 0 | — |
| S-035 Turkish protocol (PDF, 92 pp.) | 44 | 27 (PDF pp. 23, 48, 57, 77, 82, 83, 86); 13 translations | 0 | — |
| S-101 HIT-6 validation (Europe PMC XML) | 4 | 4 | 0 | — |
| S-102 AMPP menses / MIDAS (Europe PMC XML) | 5 | 4; 1 is an [S-014] fragment cited behind its own tag | 0 | — |
| S-103 PedMIDAS page (Cincinnati Children's) | 10 | 10 | 0 | — |
| S-104 HADS (Europe PMC XML) | 3 | 3 | 0 | — |
| S-105 PHQ/GAD-7 manual (PDF, 9 pp.) | 3 | 3 (P. 6/9) | 0 | — |
| S-106 NICE TA260 (chapters 1 and 2, overview) | 3 | 2 (paragraph 2.1, last sentence); 1 attribution artefact (an [S-035] fragment) | 0 | — |
| Stage 1 quotes reused by reference (S-002, S-005, S-022, S-030, S-032, S-042 and others; tagged and untagged) | 392 | 392 verbatim in Stage 1 v18 (evidence carries over) | 0 | not re-downloaded |
| Model-internal phrases and English translations (for example "output model notation", ISS-06's proposed wording) | 38 | not source quotes; every translation read against its original | — | — |

**Translations.** I read every translation of a Stage 2 quote against the original:
- [S-028] the PICO;
- [S-033] the title page, the section 3.3 comment on "БТА", the BTA recommendation (p. 40) and the p. 41 sentence;
- [S-034] the flowchart box (p. 52), the title page and section 2 (p. 17);
- [S-035] Kutu 8 (items 2 and 7), section 3.3 b, section 3.6.3.9 (three sentences), the section 6 and chapter 7 headings, section 7.1 (two sentences) and section 7.3 (three items).

All are faithful.

### Metadata and versions

- **PubMed esummary.**
  - S-101: PMID 20819842, Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMC3057423; authors Yang, Rendas-Baum, Varon, Kosinski.
  - S-102: PMID 25902814, J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMC4406925; seven authors, including Stewart and Lipton.
  - S-104: PMID 12914662, Health Qual Life Outcomes 2003;1:29, DOI 10.1186/1477-7525-1-29, PMC183845; Snaith.
  - S-103 developer paper: PMID 11739822, Neurology 2001;57(11):2034–9, DOI 10.1212/wnl.57.11.2034.
- **S-103.** Footer "© 2026 Cincinnati Children's Hospital Medical Center". The grading table is as quoted ("Greater than 50" "Severe").
- **S-105.** PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
- **S-106.** "Published: 27 June 2012" and "Last reviewed: 11 January 2016".
- **S-015.** "Published: 19 September 2012" and "Last updated: 03 June 2025". The overview page shows "Last reviewed: 23 September 2026" (links added). Every quoted recommendation reads as quoted.
- **Newer versions.** A web search finds no published ICHD-4, only the "Work in Progress" papers and the 2025 IHS workshop, so [S-001] is current. No other source has a newer version that changes an element.

### Values checked against sources

- **E-009 and E-028.** The code labels are verbatim on pp. 8, 9 and 12. 8.2.6 criterion B (p. 124, rendered) gives `classesOf826`. The 8.2.3 single-class comment is on p. 123.
- **E-032.** Reference levels: 15 days per month for 8.2.3, and 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8. The time span is "more than three months" (pp. 122–125). The INV-045 span is four calendar months or four 28-day periods (recomputed).
- **E-041.** All 18 rules match their sources: offsets, anchors, timings, ages and `excludes`.
  - The 24-week second-cycle time point of NICE 1.3.29 (TA260, 12-week re-treatment) lies within the 3–6-month window of 1.3.27.
  - I also scanned SIGN 155 and the Turkish protocol for further time points and found none.
- **E-045, E-046.**
  - NICE 1.3.28: 50 % / 30 %. NICE 1.3.29: 30 %.
  - IHS Q6: ≥ 50 %, the ≥ 30 % chronic alternative, MIDAS ≥ 5 points (baseline 11–20) or ≥ 30 % (baseline ≥ 20), HIT-6 ≥ 5.
  - DMKG/ÖKSG/SKG: 50 %, 5 points, 30 %. Russian section 7.1: 50 %. Turkish Kutu 8: 50 %.
  - The four [S-010] control levels (< 4, 4–6, > 6, complete elimination).
- **E-057.** HIT-6 36–78 and its four categories; MIDAS grades I–IV; PedMIDAS bands; the HALT-90 table with its overlap at 20; HALT-30 without grading.
- **E-059.** HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
- **E-039, E-060, E-063.** NICE 1.3.48 (4–8 weeks); ICHD-3 A1.1 (day 1 ± 2, no day 0); a remission "must exceed three months".
- **Date examples in the prose, recomputed.**
  - 26 March and 26 February – 25 March (28 days).
  - 4–31 December (28 days).
  - 1 April as the 3-month time point.
  - The interval ends of 28 February, 25 March and 31 March.
  - 6 April and day 43.

### Fidelity check per Stage 1 requirement

| OUT | Statement parts and Caveats checked | Result |
|---|---|---|
| 001 | Period with start, end and length (E-003, E-005, INV-002, INV-003, MUST); monthly frequency outputs (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); Caveat (stated length) | OK |
| 002 | Label for every form in which a view reports a measure (INV-008, `reports`); one definition per measure in a view (INV-111) | OK |
| 003 | Indicator next to every summary measure (INV-011, INV-012); SHOULD NOT a validated cut-off (INV-013); Caveat | OK |
| 004–007 | Every period of the selected range; ICHD-3 definitions (INV-009 MUST, INV-010 SHOULD); attacks separate; MUST, MUST, SHOULD, SHOULD, with the OUT-001 MUST where provided (INV-014 to INV-017, INV-108) | OK |
| 008 | MAY measures; exploratory annotation MAY (E-020 to E-022) | OK |
| 009 | Series with start, dose-change and stop markers in the view; weekly values where relevant (INV-034 to INV-036, INV-001) | OK |
| 010, 011 | Intensity on a stated scale, compared between periods (INV-018, INV-032, INV-039); duration, with the treated-attack label SHOULD and the Caveat as SHOULD NOT (INV-019 to INV-021) | OK |
| 012, 013 | Across periods and per treated attack (INV-022, INV-072, INV-076); aura MAY (E-027) | OK |
| 014–016 | Total, class and drug (INV-023, INV-024); weekly view (INV-025); indicator per period, per class and for 8.2.6, with code, level and span; prompt MUST; diagnosis MUST NOT; interpretation caveat (INV-044 to INV-048, INV-100) | OK |
| 017 | From the start of withdrawal; review window; the following year; worsening label (INV-049 to INV-052) | OK |
| 018 | Comparison per preventive treatment with values and both changes (INV-053 to INV-057); time points by type and population (E-041, INV-055, INV-058, INV-059); Caveat at MUST NOT (INV-106) | OK |
| 019, 020 | Residual burden (INV-060, INV-061); labels with criterion, values and other values, not the sole indicator (INV-062 to INV-065); v28 `courseBegunBy` in INV-064 | OK |
| 021 | MUST and SHOULD components for the same periods (INV-068, INV-069, INV-102); v28: no view without a stated start | OK |
| 022 | v28: the view after every stop, pause or reduction (INV-103); on-treatment period within the placed days, asked for where one exists (INV-070); original baseline (fix 27) | OK |
| 023, 024 | Acute outcomes, consistency, timing, formulation, phases, 15 minutes for cluster headache, Caveat (INV-071 to INV-075, INV-107); history with the v28 order, duration and summary-span ties (INV-077 to INV-079, INV-109) | OK |
| 025, 039 | Scheme windows MAY (E-056, INV-080); adherence next to the comparison, in the history and in the clinician summary (INV-066, INV-067, INV-104, INV-109) | OK at the predicate level; **R29-01** concerns the INV-067 Notes text only |
| 026, 027 | Instrument results with name, date, recall, score, grading and change (INV-081, INV-082); functional impact and its comparison with the baseline (INV-026, INV-027) | OK |
| 028–031 | Three-month view with its MUST, SHOULD and SHOULD NOT parts (INV-040 to INV-043); per headache type (INV-028 to INV-030); menstrual view MUST (INV-086, INV-087); cluster view (INV-088, INV-089) | OK |
| 032–038 | Trigger caveats; screening; clinician and patient views; paediatric (a)–(d) and Caveat; composite index; interpretive caveats (INV-083 to INV-101, INV-104, INV-105, INV-110) | OK |

Every conformance level matches the strength of the Stage 1 statement part it realises. MUST NOT is used for OUT-016 and the OUT-018 Caveat, and SHOULD NOT for the SHOULD parts and Caveats.

### Mechanical checks (`mech.py`, `names.py`, `claims28.py`)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn, section 9). |
| References | No dangling E-, INV- or ISS- reference. Every OUT reference exists in Stage 1 (39 requirements). The 35 cited source tags are within S-001–S-046 or S-101–S-106, and S-101 to S-106 are all cited. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`, and every invariant states its scope. |
| Names | 182 `omn` blocks. The tokens left unresolved by the script are attribute declarations, record-construction keys, DateSpan components, the primitives of section 2.8 and `refs` (section 2.5). Each was read and is declared. The new `courseBegunBy` is well typed (`OutputContext`, `Treatment`, `Date`). |
| `courseBegunBy` = `s ≤ d` where the start is stated (E-008 Meaning, INV-064, INV-067, INV-070 Notes) | Holds in 220,891 of 220,891 checks on enumerated admissible courses. |
| INV-070: the presence conjunct ⇔ an admissible on-treatment period exists (INV-070 Notes) | Holds in 11,005 of 11,005 events. |
| INV-064: months within the days placed on a stopped course (INV-064 Notes) | 0 of 172,874 admitted months lie outside. |
| INV-109: the acute summary covers every placed day (INV-109 Notes) | 0 of 150,867 admitted periods fail. |
| INV-067: windows within the days placed on the course (INV-067 Notes) | **Fails.** For stopped courses without a stated start, 116,353 of 227,540 admitted 28-day windows contain no day placed on the course. Example B is admitted with an August 2026 window (R29-01). |
| Scope sweep | I read in context every occurrence of record, entry, input, persist, database, XML, serializ, encod, retention, reminder, algorithm, answers, data-entry, storage, stored, "computed from" and "obtained from". Each is one of: an exclusion statement, "obtained from diary information; how is out of scope", the notation's "records", the Europe PMC endpoint name, the [S-007] "persistent" quote, or the [S-014] HALT-30 recall sentence. |

## Remarks

### R29-01 Formal defect (a Notes claim that the predicate does not guarantee): INV-067 Notes state that an adherence summary of a course without a stated start "still refers to days that the context places on the course", but INV-067 admits a window that lies wholly after the stop or pause

- **Item(s):** INV-067 Notes, second sentence (added in v28). Related: E-008 Notes, **Course start not stated**, which defines the days that the context places on such a course.
- **Problem:**
  - **What the predicate bounds.** INV-067 (v28) bounds only the first day of an adherence window, from below, by a dated course event.
  - **What the Notes claim.** They say that, for a course whose start the context does not state, a shown adherence summary "still refers to days that the context places on the course".
  - **Why the claim is false.** E-008 defines those days as running "from that event to the stop or pause, or, for a course that has not stopped, to the as-of date". For a stopped or paused course, a window that begins after the stop satisfies INV-067 and contains none of these days.
  - **No other invariant closes the gap.** INV-066 and INV-109 concern adherence shown with a response comparison, which INV-056 admits only with a stated start. E-055 `adherence` and INV-104 ask for adherence only where the start is stated. So nothing else constrains such a summary.
  - **Consequence.** The Notes describe a bound that the model does not have, so the semantics of INV-067 are stated ambiguously. This is the class of R10b-02 and R22b-01: a Notes or Reading statement that contradicts its predicate.
- **Evidence:**
  - **Model text (v28).**
    - INV-067 Predicate: `∀ a : AdherenceSummary • a.treatment ∈ ctx.subject.preventiveTreatments ∧ courseBegunBy(ctx, a.treatment, a.window.start)`.
    - E-008: `pred courseBegunBy(c : OutputContext, t : Treatment, d : Date) ≙ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.date ≤ d`.
    - INV-067 Notes: "Where it states none, no response comparison and no evaluation window of one exists (INV-056), and an adherence summary that is shown still refers to days that the context places on the course (E-008 Notes, **Course start not stated**)."
    - E-008 Notes: "The days that the context places on the course then run from that event to the stop or pause, or, for a course that has not stopped, to the as-of date."
  - **Script (`claims28.py`), predicates as written in v28.**
    - Example B of reviews and fixes 28: a course without a stated start, `doseChange(reduction)` on 15 March 2026 and `stop(paused)` on 30 June 2026.
    - An adherence summary with the window 1–31 August 2026 satisfies INV-067, because `courseBegunBy(ctx, t1, 1 Aug)` holds through the 15 March and 30 June events.
    - None of its days lies in 15 March – 30 June, the days placed on the course.
    - Over enumerated admissible courses without a stated start that have stopped, 116,353 of 227,540 admitted 28-day windows contain no day placed on the course.
  - **The predicate is right; the sentence is not.** The model admits windows that reach past the stop by a settled decision. Fix 18 declined to bound them: "a window that reaches past it states nothing false. Bounding it would make INV-066 (SHOULD) unsatisfiable with INV-067 for every comparison of a course shorter than 28 days". The v28 sentence asserts the opposite for unstated starts.
  - **Not considered before.**
    - Fix 28 checked only the lower bound: "every month (10,604), window (256,093) and acute summary period (32,426) that v28 admits begins on or after, or covers, the first dated course event" (fix-iter-28.md, Checks (iii)).
    - Fix 28 did not check the "refers to days that the context places on the course" claim against the predicate.
- **Required change:**
  - **Text only.** In the INV-067 Notes, replace the clause "and an adherence summary that is shown still refers to days that the context places on the course" with what INV-067 guarantees, for example:
    - "and the window of an adherence summary that is shown begins on or after a dated course event of the treatment, so not before the days that the context places on the course; as for a course with a stated start, the window is not bounded by the stop or pause (fix 18)".
  - **Alternatively,** delete the clause.
  - **Do not change** the INV-067 predicate, `courseBegunBy` or any other formal text.
    - This remark does not reopen fix 18's decision not to bound windows by the stop.
    - It does not touch any item of oscillation watch points 1–4. The INV-067 conjunct stays `courseBegunBy(ctx, a.treatment, a.window.start)`.
  - **Optional, for consistency.** The fixer may check that no other sentence presents INV-067 as confining the window to the time on treatment. Candidates are the INV-067 name and the E-055 Notes phrase "adherence refers to the time on treatment (INV-067)". Both predate v28 and were read with fix 18's meaning, so this remark does not require their change.

## Checked and not raised

- **The v28 fixes of R28-01 and R28-02 and of the sweep** (INV-064, INV-068, INV-070, INV-078, INV-079, INV-103, INV-109). Each is well typed.
  - Where the start is stated, each gives the v27 verdict (`courseBegunBy` = `s ≤ d`).
  - Each prose claim about it holds by script (table above), except the INV-067 sentence of R29-01.
  - E-049 Conformance and Notes, the INV-068 and INV-103 Notes and rows OUT-020, OUT-021, OUT-022 and OUT-024 describe the predicates correctly.
- **The `when` clause of E-049 plus the INV-070 ask** (watch point 5). They are consistent under section 3.3 (2) and are not a duplication. Not raised.
- **An acute line's summary of a course without a stated start** (INV-109) may begin well before the first dated event, even over an earlier course of the same drug. This is a superset that the unknown start makes necessary, and Notes claim only coverage. Not raised.
- **The phrase "that has started"** in the Readings of INV-027, INV-055, INV-071, INV-102 and INV-104. It is the model's established phrase for `startOf(c, t) ≠ ∅` (fix 10). The predicates are unambiguous. Wording, not a remark.
- **Unstated starts as a Stage 1 issue** (OUT-018, OUT-021, OUT-022, OUT-024). Fixes 27 and 28 found Stage 1 clear and the model asking for what can be placed. No new evidence. Not raised.
- **Settled points, not reopened (no new evidence):**
  - adherence windows reaching past the stop (fix 18);
  - caregiver lost productive days bounded by the period length (reviews 16, 24);
  - periods beyond the as-of date (reviews 18, 20, 22; watch point 10);
  - INV-060 with INV-061 for short compared periods;
  - the "> 3 months" readings of INV-045 and INV-089; INV-106 at MUST NOT;
  - the E-041 readings, timings, ages and `excludes`;
  - empty `remissions` in chronic cluster headache (ISS-12);
  - the HIT-6 one-month recall; HADS subscales only; the MIDAS labels and Grade IV undivided;
  - the M-TOQ, PGIC and MSQ categories (review 19b);
  - the acute part of optimal control (review 03);
  - the [S-014] HALT-30 sentence with "records".
- **Section 8.**
  - ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded.
  - Their source quotes are verbatim at the stated locations: [S-001] pp. 12, 42, 105, 122–125, 139, 190 and 209; NICE 1.3.9, 1.3.39 and 1.3.48 under these numbers; [S-034] p. 52.
  - Their descriptions of the Stage 1 passages are accurate. For example, OUT-031 Evidence notes that "the next sentence of the definition, a duration criterion, is not quoted", and OUT-009, OUT-021 and OUT-034 refer to OUT-005 by ID.
  - No Stage 1 issue is worked around silently. R29-01 is a model defect.
- **Oscillation watch points (check after iteration 28).**
  - R29-01 is the sixth consecutive remark on the treatment-course cluster.
  - It finds a new case: a sentence of fix 28 that its checks did not cover.
  - It is text-only, and it moves the text toward the predicate and toward fix 18's settled reading.
  - It reverses nothing listed in watch points 1–4. `startOf` in INV-103, the INV-070 presence conjunct, `courseBegunBy`, the `when` clauses of E-049, `originalStart` and `resumes` are untouched.
  - It requires no predicate change, so it cannot widen or narrow any admitted set.

## Notes on frozen items (for the human)

None.
