# Review — iteration 30
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v29
Date: 2026-10-22

## Summary

This is the main review of iteration 30, by a new, independent reviewer. I checked v29 against its sources and against Stage 1 v18.

**State of the files.**
- `OUTPUT_MODEL.md` is v29 ("Version: v29 · Iteration: 29"). It is byte-identical to `history/v29.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line.
- The v28 → v29 diff, sentence by sentence, changes only the Notes of E-055, INV-064 and INV-067, plus bookkeeping (header, sections 9, 11 and 12). No `omn` block changed.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18: sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026), and the source table of section 5.
- v29: sections 1–10 in full (notation, conformance, all 67 elements and 111 invariants, traceability, section 8, sources), the search-log rows on new sources, and the v29 change-log entry.
- Loop files:
  - review 29 and fix 29;
  - the oscillation check after iteration 28, with its seven watch points;
  - R25b-01 (review 25b);
  - R02-05 and item 14 of fix 02 (derived attributes);
  - row 39 of fix 28's table;
  - every earlier passage on "previous bouts", and on INV-079 and the duration.

**Result.**
- **Citations.** I downloaded every source that carries a Stage 2 quote. Every quoted fragment is verbatim at its stated location. Translations, metadata and versions are correct.
- **Values.** All value sets, ranges, bands, code labels, reference levels, offsets, thresholds and control levels match their sources.
- **Scope.** The model has no input, storage or input-derivation content.
- **Mechanical checks.** All pass.
- **Fidelity.** All 39 requirements are represented at their Stage 1 strengths.
- **Text changed in v29.** The INV-064, INV-067 and E-055 Notes that fix 29 reworded state exactly what their predicates guarantee.
- **The remark.** **R30-01** concerns the derived `duration` of a treatment line (E-055, INV-079).
  - INV-079 ties the duration to the start and stop dates only where the line shows them. A line that omits a date can show any duration. With the predicate as written, 399 of 399 candidate values are admitted for a course of 41 days.
  - The INV-079 Reading states the equality without that condition, and INV-109 calls the acute course span "the span of the line's duration".
  - Both arguments of the relation are course events of the context, which INV-079 and INV-109 already use as relation arguments. So the relation can be stated in every valid output.
  - The case dates from v02. It is not a consequence of fixes 25–29, and the required change reverses no watch-point item.

## Verification coverage

### Downloads and tools

- **Where.**
  - Sources: fresh `curl` downloads through the proxy into the session scratchpad folder `r30/src`, outside the repository.
  - Text: per-page `pdftotext -raw` for PDFs; HTML and XML with the markup stripped. Output in `r30/txt`.
  - Rendered pages: `r30/img`.
- **HTTP.** All 25 requests returned HTTP 200 on the first try, including apicr.minzdrav.gov.ru (S-033, S-034) and noroloji.org.tr (S-035).
- **Scripts.** All are in `r30/scripts` and were run with `python3 -I`:
  - `extract.py` and `quotes.py` for the quote checks;
  - `mech.py` and `names.py` for the mechanical checks;
  - `inv079.py` for R30-01.
- **Matching.**
  - Normalisation: NFKD, combining marks and soft hyphens removed, case folded, letters and digits only.
  - This joins line-end hyphens and drops the ICHD-3 glyphs that have no text mapping.
- **Fragments.**
  - Every double-quoted string in sections 1–10 outside the `omn` blocks was split at "[...]". Fragments of at least 6 letters or digits were kept.
  - Each fragment was attributed to the nearest source tag on its line (before it, else after it) and searched page by page.
  - Fragments not found there were searched in Stage 1 v18 and then in every downloaded source.
  - For every PDF hit, I compared the page against the location stated in the model.
- **Rendered and read:**
  - [S-001] p. 190: A1.1.1 criterion B "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)" and A1.1.2 criterion B "Occurring on day 1 ± 2 (i.e. days −2 to +3)". In the text layer "+" is "þ", so these two were confirmed on the image.
  - [S-034] p. 1 (an image): "Возрастная группа" followed by "дети".
  - [S-035] PDF p. 48: Kutu 8 has eight items, with "Ölçüt …" second and "Yeterli süre …" seventh. The "Profilaktik tedavinin başarısı …" item stands below the box, as Stage 1 OUT-011 locates it.

### Quote check per source

| Source | Fragments attributed | Verbatim at stated location | Not found | Unreachable (tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (PDF, 211 pp.) | 69 + 2 glyph quotes | 69 in the text layer (pp. 8, 9, 12, 42, 105, 122–125, 139, 190, 209, 210); 2 on rendered p. 190 | 0 | — |
| S-007 IHS cluster (UCL accepted manuscript) | 5 | 5 (pp. 10, 22, 25) | 0 | — |
| S-008 IHS 2024 preventive (univaq PDF) | 20 | 20 (pp. 9, 12, 13, 17; p. 5 is the summary table) | 0 | — |
| S-010 IHS 2025 position statement (univaq PDF) | 31 | 31 (p. 6 and headings) | 0 | — |
| S-011, S-012, S-013 (Europe PMC XML) | 12 + 1 + 2 | 15 | 0 | — |
| S-014 EHF/LTB aids (Europe PMC XML) | 31 | 31; the HALT paragraph is in section "The Headache-Attributed Lost Time (HALT) Indices", as stated | 0 | — |
| S-015 NICE CG150 (Recommendations and Overview pages) | 33 | 33, including recs 1.3.9, 1.3.24, 1.3.26 (with the TA260 sentence), 1.3.27–1.3.29, 1.3.39 and 1.3.48 under these numbers, and the headings "Migraine with or without aura" and "Prophylactic treatment review" | 0 | — |
| S-016 SIGN 155 (PDF, 64 pp.; PDF page = printed page + 6) | 8 | 8 (PDF pp. 7, 20). The children sentence is two sentences after the objectives sentence | 0 | — |
| S-018 AAN/AHS clinician summary (PDF, 12 pp.) | 10 | 10 (pp. 1, 7, 8) | 0 | — |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML) | 5 | 5 | 0 | — |
| S-028 NVN module (web page) | 8 | 8, including the PICO under "Zoeken en selecteren" | 0 | — |
| S-033 Russian adults (official PDF, 92 pp.) | 23 | Every Russian fragment at its page: p. 1 (title), p. 4 ("М – мигрень"), p. 39 (section 3.3 comment and recommendation), p. 40 (BTA recommendation), p. 41 (anti-CGRP comment), p. 53 (section 7.1). The rest are English attribution artefacts of neighbouring sources | 0 | — |
| S-034 Russian children (official PDF, 53 pp.) | 8 + 1 image | 8 (pp. 17, 52) + rendered p. 1 | 0 | — |
| S-035 Turkish protocol (PDF, 92 pp.) | 30 | 30 (PDF pp. 23, 48, 57, 77, 82, 83, 86); item positions in Kutu 8 and section 7.3 as stated | 0 | — |
| S-101 HIT-6 validation (Europe PMC XML) | 4 | 4 (Methods, "Data sources"); the omitted words describe the summation | 0 | — |
| S-102 AMPP menses / MIDAS (Europe PMC XML) | 5 | 5 (subsection "Migraine-related disability") | 0 | — |
| S-103 PedMIDAS page (Cincinnati Children's) | 10 | 10 ("PedMIDAS Grading Scale"; footer © 2026) | 0 | — |
| S-104 HADS (Europe PMC XML) | 3 | 3; the omitted words describe how the scores are obtained | 0 | — |
| S-105 PHQ/GAD-7 manual (PDF, 9 pp.) | 3 + 2 in section 10 | 5 (P. 6/9; the development sentence on P. 8/9) | 0 | — |
| S-106 NICE TA260 (chapter 2) | 2 | 2 (paragraph 2.1, last sentence) | 0 | — |
| Stage 1 quotes reused by reference (S-002, S-005, S-022, S-030, S-042 and others; tagged and untagged) | 357 | 357 verbatim in Stage 1 v18 (the evidence carries over) | 0 | not re-downloaded |
| Translations and model-internal phrases | 22 + 16 | Not source quotes. I read every translation of a Stage 2 quote against its original (S-028 PICO; S-033 pp. 1, 39, 40, 41; S-034 pp. 1, 17, 52; S-035 Kutu 8, sections 3.3 b, 3.6.3.9, 6, 7, 7.1 and 7.3). All are faithful | — | — |
| Attribution artefacts (fragment tagged by a neighbouring source) | 29 | All 29 found in the source that the sentence actually names (for example the IHS Q6 "beyond three months" in S-008 p. 12) | 0 | — |

**Totals.** 750 fragments: 323 verified in their own source at the stated location, plus 2 glyph quotes and 1 image quote on rendered pages; 357 verified in Stage 1 v18; 29 artefacts verified in the named source; 38 translations and model phrases. None not found, and no source unreachable.

### Metadata and versions

- **PubMed esummary.**
  - S-101: PMID 20819842, Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMC3057423; Yang, Rendas-Baum, Varon, Kosinski.
  - S-102: PMID 25902814, J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMC4406925; seven authors as cited (PubMed spells "Pavlović").
  - S-104: PMID 12914662, Health Qual Life Outcomes 2003;1:29, DOI 10.1186/1477-7525-1-29, PMC183845; Snaith.
  - S-103 developer paper: PMID 11739822, Neurology 2001;57(11):2034–9, DOI 10.1212/wnl.57.11.2034.
- **S-105.** PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
- **S-106.** "Published: 27 June 2012", "Last reviewed: 11 January 2016".
- **S-015.** "Published: 19 September 2012", "Last updated: 03 June 2025", "Last reviewed: 23 September 2026" (overview). Every quoted recommendation reads as quoted.
- **Newer versions.** A web search finds no published ICHD-4, only the "Work in Progress" papers and the 2025 workshop, so [S-001] is current. No other source has a newer version that changes an element.

### Values checked against sources

- **E-009 and E-028.** The code labels are verbatim (pp. 8, 9, 12), and so are `classesOf826` (8.2.6 criterion B, p. 124) and the 8.2.3 single-class comment (p. 123).
- **E-032.** The reference levels are 15 for 8.2.3 and 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8. The span is "more than three months" (pp. 122–125). By recomputation, INV-045 gives four calendar months or four 28-day periods.
- **E-041.** All 18 rules match their sources: offsets, anchors, timings, ages and `excludes`.
- **E-045 and E-046.**
  - NICE 1.3.28: 50 % / 30 %. NICE 1.3.29: 30 %.
  - IHS Q6: ≥ 50 %; the ≥ 30 % chronic alternative; MIDAS ≥ 5 points (baseline 11–20) or ≥ 30 % (baseline ≥ 20); HIT-6 ≥ 5.
  - DMKG/ÖKSG/SKG (episodic part): 50 %, 5 points, 30 %.
  - Russian section 7.1: 50 %. Turkish Kutu 8: 50 %.
  - The four [S-010] control levels.
- **E-057.**
  - HIT-6: 36–78 and its four categories.
  - MIDAS: grades I–IV and their labels, as [S-102] prints them.
  - PedMIDAS: four bands, "Greater than 50" severe.
  - HALT-90: the table, with its overlap at 20. HALT-30: no grading.
  - Recall periods: 3 / 1 / 3 / 3 / 1 months.
- **E-059.** HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
- **E-039, E-060, E-063.**
  - NICE 1.3.48: 4–8 weeks.
  - ICHD-3 A1.1: day 1 ± 2 with no day 0, so `windowDaysBefore` = `windowDaysAfter` = 2.
  - A remission "must exceed three months".
- **Date examples, recomputed:**
  - 26 March, and 26 February – 25 March (28 days);
  - 4–31 December (28 days);
  - 1 April;
  - the interval ends of 28 February, 25 March and 31 March;
  - the stop on 30 March (NICE 1.3.28 and Box 8 required, the 3-month time points not);
  - 6 April and day 43;
  - 15 August – 20 October (67 days); 10 March – 21 April (43 days);
  - the bout of 42 days and the remission of 143 days.

### Fidelity check per Stage 1 requirement

| OUT | Statement parts and Caveats checked | Result |
|---|---|---|
| 001 | Every view states its period with start, end and length (E-003, E-005, INV-002, INV-003, MUST); frequency outputs per calendar month or 28-day period (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); Caveat (stated length) | OK |
| 002 | Label for every form in which a view reports a measure (INV-008, `reports`); one definition per measure in a view (INV-111) | OK |
| 003 | Indicator for the period of every summary measure (INV-011, INV-012); SHOULD NOT a validated cut-off (INV-013); Caveat | OK |
| 004–007 | Every period of the selected range; ICHD-3 definitions (INV-009 MUST, INV-010 SHOULD); attacks shown separately; levels MUST, MUST, SHOULD, SHOULD, with the OUT-001 MUST where provided (INV-014 to INV-017, INV-108) | OK |
| 008 | MAY measures; exploratory annotation MAY (E-020 to E-022) | OK |
| 009 | Series with start, dose-change and stop markers in the view; weekly values where relevant (INV-034 to INV-036, INV-001) | OK |
| 010, 011 | Intensity on a stated scale, compared between periods (INV-018, INV-032, INV-039); duration, with the treated-attack label SHOULD and the Caveat as SHOULD NOT (INV-019 to INV-021) | OK |
| 012, 013 | Symptoms across periods and per treated attack (INV-022, INV-072, INV-076); aura MAY (E-027) | OK |
| 014–016 | Total, class and drug (INV-023, INV-024); weekly view (INV-025); indicator per period, per class and for 8.2.6, with code, level and span (INV-044 to INV-046); prompt MUST (INV-047); not a diagnosis, MUST NOT (INV-048); interpretation caveat (INV-100) | OK |
| 017 | From the start of withdrawal; review window; the following year; worsening label (INV-049 to INV-052) | OK |
| 018 | Comparison per preventive treatment with the values and both changes (INV-053 to INV-057); time points by type and population (E-041, INV-055, INV-058, INV-059); Caveat at MUST NOT (INV-106) | OK |
| 019, 020 | Residual burden (INV-060, INV-061); labels with criterion, values and other values, not the sole indicator (INV-062 to INV-065) | OK |
| 021 | MUST and SHOULD components for the same periods (INV-068, INV-069, INV-102) | OK |
| 022 | View after every stop, pause or reduction (INV-103); on-treatment period and original baseline (INV-070) | OK |
| 023 | Outcomes, consistency, timing, formulation, phases, 15 minutes for cluster headache, Caveat (INV-071 to INV-075, INV-107) | OK |
| 024 | History with dates, dose changes, duration, response, adverse effects, stop reason, formulation, grouping and order (INV-077 to INV-079, INV-109) | **R30-01** (duration) |
| 025, 039 | Scheme windows MAY (E-056, INV-080); adherence next to the comparison, in the history and in the clinician summary (INV-066, INV-067, INV-104, INV-109) | OK |
| 026, 027 | Instrument results with name, date, recall, score, grading and change (INV-081, INV-082); functional impact and its comparison with the baseline (INV-026, INV-027) | OK |
| 028–031 | Three-month view with its MUST, SHOULD and SHOULD NOT parts (INV-040 to INV-043); per headache type (INV-028 to INV-030); menstrual view MUST (INV-086, INV-087); cluster view (INV-088, INV-089) | OK |
| 032–038 | Trigger caveats; screening; clinician and patient views; paediatric (a)–(d) and Caveat; composite index; interpretive caveats (INV-083 to INV-101, INV-104, INV-105, INV-110) | OK |

Every conformance level matches the strength of the Stage 1 statement part it realises. MUST NOT is used for OUT-016 and the OUT-018 Caveat, and SHOULD NOT for SHOULD parts and Caveats.

### Mechanical checks (`mech.py`, `names.py`, `inv079.py`)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111): none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn, section 9). |
| References | No dangling E-, INV- or ISS- reference. Every OUT reference exists in Stage 1 (39 requirements). The 37 cited source tags are within S-001–S-046 or S-101–S-106, and S-101 to S-106 are all cited. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field. Every invariant has exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`, and every invariant states its scope. |
| Typing rule for levels | No SHOULD or MAY attribute, and no MUST attribute with a `when` clause, lacks an `opt`, `set` or `seq` type. Only `Output.views` and `View.content` are composition attributes (section 2.5). |
| Names | 182 `omn` blocks. The only token the script left unresolved is `c`, the free context variable of INV-001 (section 2.9). One apparent double declaration was a text literal. |
| INV-079 duration (R30-01) | For a course of 41 days, INV-079 admits 1 of 399 candidate durations when the line shows both dates, and 399 of 399 when it omits the stop date, the start date or both. For an ongoing course whose line omits the start date, it admits a duration of 30 days, although the course has run 294 days. |
| Scope sweep | I read in context every occurrence of enter, record, input, store, persist, database, serializ, encod, retention, reminder, algorithm, "computed from", "derived from", "obtained from", answers, questionnaire, data-entry, JSON, XML, CSV, FHIR, HL7, capture and log. Each is one of: an exclusion statement; "obtained from diary information; how is out of scope"; the notation's "records"; an instrument or document name; the [S-014] HALT-30 sentence (settled); or the INV-076 statement that assigning attack lines to types would be a derivation from input. |

## Remarks

### R30-01 Formal defect (derived attribute without its relation; Reading claims more than the predicate): the duration of a treatment line is constrained only where the line also shows its start date and, for a stopped course, its stop date

- **Item(s):**
  - INV-079 (Predicate, Reading, Notes);
  - E-055 `duration` (declaration comment; Notes, "Relations");
  - INV-109 Reading ("the span of the line's duration, INV-079");
  - row OUT-024.
- **Problem:**
  - **The definition.** E-055 declares `duration : opt Duration derived SHOULD when startOf(ctx, self.treatment) ≠ ∅ -- to the stop date or, if not stopped, to the as-of date`.
  - **What the predicate ties.** INV-079 relates the duration to the line's *shown* dates only:
    - `∀ s ∈ l.startDate; e ∈ l.stopDate • s ≤ e ∧ ∀ d ∈ l.duration • d = daysLong(days(s, e))`;
    - `¬ stopped(ctx, l.treatment) ⇒ ∀ s ∈ l.startDate; d ∈ l.duration • … d = daysLong(days(s, ctx.asOf))`.

    Fix 28 added `∀ d ∈ l.duration • startOf(ctx, l.treatment) ≠ ∅`, which ties nothing to the value.
  - **The cases left open.** `startDate` and `stopDate` are SHOULD attributes (E-055). A line that shows its duration but omits its stop date, its start date or both can therefore show any duration. A line of an ongoing treatment that omits its start date can do the same. No other invariant constrains the value.
  - **Why this contradicts the definitional status.** INV-079 is definitional, and section 3.3 (5) says that a definitional invariant "holds wherever the element is shown" and excludes "outputs that show a value contradicting the definition of the element". A MUST-conformant diary may deviate from the SHOULD of a date, but that deviation does not license a false derived value.
  - **The texts claim the unconditional relation.**
    - INV-079 Reading: "a duration equal to the days from start to stop or, for a treatment that has not stopped, from start to the as-of date of the output".
    - INV-109 Reading equates an acute line's course summary with "the span of the line's duration, INV-079".
    - INV-109 ties that summary span to the context's course events whatever dates the line shows. A line could therefore show "200 days" next to a course summary of 41 days, and both are presented as the same span.
- **Evidence:**
  - **Script (`inv079.py`, INV-079 as written in v29).**
    - Context: a preventive course started on 1 January 2026 and discontinued on 10 February 2026, its last day on treatment (41 days); as-of date 21 October 2026.
    - Line with start and stop date shown: only 41 days is admitted.
    - Line with the start date shown and no stop date, or the stop date and no start date, or neither: every duration from 1 to 399 days is admitted, among them 200 days.
    - A course started on 1 January 2026 and not stopped, whose line omits the start date, admits 30 days, although the course has run 294 days.
  - **The relation can be stated over output elements and context properties.**
    - Both arguments are course events of the context (`startOf`, and the one stop or pause that INV-001 admits per course) or the as-of date.
    - INV-079 already uses exactly these as relation arguments (`eventOn`, `ctx.asOf`, `startOf`).
    - INV-109 ties the same course's span to them without condition on the shown dates: `(∀ b ∈ startOf(ctx, l.treatment) • s.period.start = b)`, `eventOn(ctx, l.treatment, stop(k), s.period.end)` and `s.period.end = ctx.asOf`.
    - INV-075 Notes state the model's rule: "The relation takes only an output element and a context property as arguments, as INV-036 and INV-079 do."
  - **Stage 1 makes a wrong duration matter.** OUT-024 asks for "start and stop dates, dose changes, treatment duration" and quotes:
    - [S-013] "It is not reasonable to test again preventive medications used in the past with no efficacy or with intolerable side effects provided that information on duration, dose and adverse events is sufficient and reliable.";
    - [S-013] "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed."

    R25b-01, accepted by fix 25, used the same evidence: "89 days shown for a course taken for 41 days presents an inadequate trial as adequate".
  - **Not considered before.**
    - R02-05 asked only for the duration of an ongoing treatment, and fix 02 related it to the shown start date.
    - Fix 02 item 14 ("Derived attributes outside the R02-05 pattern") accepted E-063 `duration` and E-058 `changeFromBaseline` as "defined in every fully conformant output". Their arguments are values obtained from diary information, for which no context relation exists. That reasoning was not applied to E-055.
    - Fix 28, row 39, already treated "any duration is admitted" as a defect of INV-079 and fixed it for unstated starts only.
    - R25b-01 and fix 25 concerned several stop events, not omitted dates.
- **Required change** (one of):
  - **(a) Tie the duration to the course in INV-079** (preferred: it keeps the value correct in every valid output). Add, for example:

    `(∀ d ∈ l.duration; s ∈ startOf(ctx, l.treatment) • (∀ e ∈ ctx.subject.courseEvents • e.treatment = l.treatment ∧ e.kind is stop ⇒ d = daysLong(days(s, e.date))) ∧ (¬ stopped(ctx, l.treatment) ⇒ d = daysLong(days(s, ctx.asOf))))`.

    The partial `days` is guarded by INV-001: no course event precedes the start, and every course event and the start lie on or before the as-of date.
  - **(b) Admit a duration only together with the dates it is computed from:** `∀ d ∈ l.duration • l.startDate ≠ ∅ ∧ (stopped(ctx, l.treatment) ⇒ l.stopDate ≠ ∅)`.
  - **In either case:**
    - align the INV-079 Reading and Notes, the E-055 Notes ("Relations") and the INV-109 Reading with the predicate;
    - keep every existing INV-079 conjunct, including fix 28's `∀ d ∈ l.duration • startOf(ctx, l.treatment) ≠ ∅` (oscillation watch point 4: no conjunct is dropped);
    - change no course-event date or other watch-point item.

## Checked and not raised

- **The v29 changes.**
  - INV-067 Notes. The window begins on or after a dated course event, and INV-067 does not bound it by the stop or pause. Evaluation windows end with on-treatment periods (`adherenceFor`), which INV-056 does not bound by a stop.
  - INV-064 Notes. The months lie within the days placed on a course without a stated start only where the course has stopped or paused, by `courseBegunBy` together with `evaluatedOnTreatment`.
  - E-055 Notes. The `adherence` clause rests on the evaluation window of the response comparison (`adherenceFor`, INV-109), which needs a stated start (INV-056).

  Each sentence states exactly what its predicate guarantees.
- **The analogous E-063 and E-058 cases.**
  - E-063 `duration`: unconstrained where the item omits its start date.
  - E-058 `changeFromBaseline`: unconstrained where a score is omitted.
  - Fix 02 item 14 decided both. Their arguments are values obtained from diary information, so no context relation exists. I have no new evidence. Not raised.
- **Residual burden for a change outside a response comparison** (for example a change in the post-stop view, whose compared period is off treatment). OUT-019 asks for the residual burden "Wherever the output shows a relative (percentage) change". The model follows that wording (INV-060, INV-061). Not raised.
- **DMKG/ÖKSG/SKG chronic-migraine sentence.** [S-023] continues after the episodic criterion with a chronic-migraine passage ("eine Reduktion um mindestens 50 % der Migränetage als Wirksamkeitsnachweis … mindestens 30 % als Therapieerfolg"). Stage 1 quotes only the episodic part, the named criterion says "(episodic migraine)", and `ResponderCriterion` is an open value type. Not raised.
- **Turkish section 3.6.3.9, the stopping rule after success** ("Hastanın başağrıları 3 ay boyunca ayda 10 günün altında seyrediyorsa tedavi kesilmesi önerilmektedir"). E-041 Notes list it among the times that are not evaluation time points. Correct.
- **Section 8.**
  - ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded, and their quotes are verbatim at the stated locations. "Simple analgesics" occurs exactly once in ICHD-3, on p. 139.
  - Their descriptions of the Stage 1 passages are accurate.
  - No Stage 1 issue is worked around silently. R30-01 is a model defect.
  - The Stage 1 OUT-011 location of the [S-035] success sentence ("directly below Kutu 8") is correct on the rendered page.
- **Satisfiability and definedness claims spot-checked:**
  - the INV-012 pairwise argument (1-D Helly property of the admitted intervals);
  - the INV-055 window construction (every window begins at least 8 weeks after the start);
  - `scopeFor` ⇒ `onlyOfType` (INV-088 Notes);
  - the "two directions agree" of INV-046 in outputs whose class values are consistent with the context.
- **Settled points, not reopened (no new evidence):**
  - "history of previous bouts" (since review 01);
  - E-039 `reviewWindow` without a `when` clause;
  - INV-060 with INV-061 for short compared periods;
  - adherence windows reaching past the stop (fix 18);
  - periods beyond the as-of date (watch point 10);
  - caregiver lost productive days bounded by the period length;
  - the "> 3 months" readings of INV-045 and INV-089;
  - INV-106 at MUST NOT;
  - the E-041 readings, ages and `excludes`;
  - the MIDAS labels and Grade IV undivided; the HIT-6 one-month recall; HADS subscales only;
  - the [S-014] HALT-30 sentence with "records";
  - the E-060 lead-in wording;
  - empty `remissions` in chronic cluster headache (ISS-12);
  - the acute part of optimal control.
- **Oscillation watch points (check after iteration 28).**
  - R30-01 concerns INV-079, an item named in watch point 4.
  - It reverses nothing listed there. It adds a relation and keeps the duration conjunct of fix 28, `courseBegunBy`, the INV-078 order, the INV-109 end ties and every course-event date.
  - It is a genuinely new case, a gap present since v02. It is not a consequence of fixes 25–29, and it does not take a side between the start-aligned and event-aligned positions of watch point 1.

## Notes on frozen items (for the human)

None.
