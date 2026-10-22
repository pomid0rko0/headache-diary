# Review — iteration 31
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v30
Date: 2026-10-22

## Summary

This is the main review of iteration 31, by a new, independent reviewer. I checked v30 against its sources and against Stage 1 v18.

**State of the files.**
- `OUTPUT_MODEL.md` is v30 ("Version: v30 · Iteration: 30"). It is byte-identical to `history/v30.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line.
- The v29 → v30 diff changes one `omn` block (INV-079, one conjunct inserted), the INV-079 Reading, Evidence and Notes, the E-055 Notes, the INV-109 Reading, the OUT-024 coverage reason, and bookkeeping.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18: sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5.
- v30: sections 1–10 in full (notation, conformance, all 67 elements and 111 invariants, traceability, section 8, sources), the search log and the v30 change-log entry.
- Loop files: review 30 and fix 30; the oscillation check after iteration 28 with its seven watch points; fix 26 (the level of INV-070); the iteration-24 check's topic "Truth of a shown fact tied to the context"; R27-01 and R28-01 (INV-070).

**Result.**
- **Citations.** I downloaded every source that carries a Stage 2 quote. Every quoted fragment is verbatim at its stated location. Translations, metadata and versions are correct. ICHD-3 is still the current edition.
- **Values.** All value sets, ranges, bands, code labels, reference levels, offsets, thresholds and control levels match their sources.
- **Scope.** The model has no input, storage or input-derivation content.
- **Mechanical checks.** All pass.
- **The v30 change.** The new INV-079 conjunct does what its Reading, its Notes and the INV-109 Reading say (script below).
- **Fidelity.** All 39 requirements are represented, and every level matches its Stage 1 statement part.
- **The remark.** **R31-01** concerns four content invariants of SHOULD or MAY elements: INV-070 (E-049), INV-050 (E-039), INV-062 (E-046) and INV-092 (E-033).
  - Each of them contains, besides the SHOULD content that Stage 1 asks for, conjuncts that state what the element *is*: the course event or the start of withdrawal it shows, the periods it labels as the original pre-treatment baseline, the on-treatment period or the periods after the event, the treatment of a label's underlying values, the period of an index's component measures.
  - Because these conjuncts carry only the SHOULD level of their invariant, a MUST-conformant diary may show, for example, a post-stop monitoring view of a stop that never happened, with a month on treatment as its "original pre-treatment baseline". Every definitional and MUST invariant still holds.
  - Section 3.3 (5) classifies such conjuncts as definitional. The model states the same kind of tie definitionally for markers (INV-036), time points (INV-058), treatment lines (INV-079), residual burdens (INV-061) and trigger views (INV-110).
  - The required change moves these conjuncts verbatim to definitional status. It changes no conjunct and no `when` clause, and it narrows only what MUST-conformant diaries admit. So it reverses none of the watch-point items on INV-070.

## Verification coverage

### Downloads and tools

- **Where.** Every source was downloaded with `curl` through the proxy into the session scratchpad folder `r31/src`, outside the repository.
  - PDFs were split into per-page text with `pdftotext -raw`.
  - HTML and the Europe PMC full-text XML were stripped to text (`r31/scripts/strip.py`).
  - Pages were rendered with `pdftoppm` where a quote is in an image.
- **HTTP.** Every request returned HTTP 200, except two attempts on apicr.minzdrav.gov.ru (S-033: connection reset by peer). The second retry returned the 92-page PDF.
- **Scripts.** All are in `r31/scripts` and were run with `python3 -I`:
  - `quotes.py` (quote extraction and matching);
  - `mech.py` (IDs, references, fields, traceability, levels);
  - `names.py` (declared names and token resolution in the 182 `omn` blocks);
  - `inv079.py` (the v30 INV-079 conjunct).
- **Matching.**
  - Normalisation: NFKD, combining marks, soft hyphens and the ICHD-3 "þ" glyph removed, case folded, letters and digits only. This joins line-end hyphens and drops glyphs that have no text mapping ("≥", "±", "−").
  - Fragments: every double-quoted string outside the `omn` blocks, split at "[...]", keeping fragments of at least 6 letters or digits.
  - Attribution: each fragment was attributed to the nearest source tag on its line and searched page by page in that source.
  - Fallback: a fragment not found there was searched in Stage 1 v18, then in every downloaded source.
  - Location: for every PDF hit, I compared the page against the location stated in the model; for web and XML sources, the section heading.
- **Rendered and read:**
  - [S-034] p. 1 (an image): "Клинические рекомендации Мигрень", "Возрастная группа" followed by "дети", "Год утверждения 2024".
  - [S-035] PDF p. 48: Kutu 8, with "Ölçüt atak sıklığında en az %50 azalma olması" as the second item and "Yeterli süre, etkinlik için en az 2-3 ay …" as the seventh. "Profilaktik tedavinin başarısı …" stands below the box, as Stage 1 OUT-011 says.
  - [S-035] PDF pp. 82–83: the nerve-block sentences quoted in E-041 Notes stand above the heading "7.2", so in section 7.1, as stated.

### Quote check per source

| Source | Fragments attributed | Verbatim at stated location | Not found | Unreachable (tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (PDF, 211 pp.) | 81 | 81 (pp. 4–15 classification list, 42, 105, 122–125, 139, 190, 209, 210) | 0 | — |
| S-007 IHS cluster (UCL accepted manuscript, 39 pp.) | 8 | 8 (pp. 10, 22, 25) | 0 | — |
| S-008 IHS 2024 preventive (univaq PDF, 31 pp.) | 21 | 21 (pp. 9, 12, 13, 17) | 0 | — |
| S-010 IHS 2025 position statement (univaq PDF, 11 pp.) | 39 | 39 (p. 6; headings) | 0 | — |
| S-011 EHF 2022 (Europe PMC XML) | 13 | 13 (Background; question 3 and 4 statements) | 0 | — |
| S-012, S-013 (Europe PMC XML) | 1 + 4 | 5 | 0 | — |
| S-014 EHF/LTB aids (Europe PMC XML) | 34 | 34; the HALT and HURT passages and Table 18 are in the sections stated | 0 | — |
| S-015 NICE CG150 (Recommendations and Overview pages) | 38 | 38, including recs 1.3.9, 1.3.24, 1.3.26 (with the TA260 sentence), 1.3.27–1.3.29, 1.3.39 and 1.3.48; "Last updated: 03 June 2025", "Last reviewed: 23 September 2026" | 0 | — |
| S-016 SIGN 155 (PDF, 64 pp.; PDF page = printed page + 6) | 7 | 7 (PDF pp. 7, 20) | 0 | — |
| S-018 AAN/AHS clinician summary (PDF, 12 pp.) | 10 | 10 (pp. 1, 7, 8) | 0 | — |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML) | 5 | 5 | 0 | — |
| S-028 NVN module (web page) | 10 | 10, including the PICO under "Zoeken en selecteren" | 0 | — |
| S-033 Russian adults (official PDF, 92 pp.) | 21 | 21 (pp. 1, 4, 39, 40, 41, 53); the p. 41 sentence follows the anti-CGRP paragraph, as stated | 0 | — (two connection resets, then HTTP 200) |
| S-034 Russian children (official PDF, 53 pp.) | 8 + 2 image fragments | 8 (pp. 17, 52) + rendered p. 1 | 0 | — |
| S-035 Turkish protocol (PDF, 92 pp.) | 33 | 33 (PDF pp. 6–7, 23, 48, 57, 77, 82, 83, 86) | 0 | — |
| S-101 HIT-6 validation (Europe PMC XML) | 4 | 4 (Methods, "Data sources") | 0 | — |
| S-102 AMPP menses / MIDAS (Europe PMC XML) | 7 | 7 ("Headache impact on functioning" > "Migraine-related disability") | 0 | — |
| S-103 PedMIDAS page (Cincinnati Children's) | 10 | 10 ("PedMIDAS Grading Scale"; footer "2026 Cincinnati Children's Hospital Medical Center") | 0 | — |
| S-104 HADS (Europe PMC XML) | 3 | 3 ("Construction of the Hospital Anxiety And Depression Scale (HADS)") | 0 | — |
| S-105 PHQ/GAD-7 manual (PDF, 9 pp.) | 3 (+2 in section 10) | 5 (P. 6/9 under "USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES"; the development sentence on P. 8/9) | 0 | — |
| S-106 NICE TA260 (chapter 2; overview; chapter 1) | 3 (+1 in the search log) | 4 (paragraph 2.1, last sentence; the search-log phrase "less than a 30% reduction in headache days per month after 2 treatment cycles" is in recommendation 1.2 of chapter 1) | 0 | — |
| Stage 1 quotes reused by reference (S-002, S-005, S-022, S-030, S-042 and others, tagged and untagged) | 415 | 415 verbatim in Stage 1 v18 (the evidence carries over) | 0 | not re-downloaded |
| Attribution artefacts (fragment tagged by a neighbouring source) | 40 | All 40 found in the source that the sentence actually names (for example "beyond three months" in S-008 p. 12) | 0 | — |
| Translations, search-log query strings and model-internal phrases | 22 + 21 + 35 | Not source quotes. I read every translation of a Stage 2 quote against its original (S-028 PICO; S-033 pp. 1, 39, 40, 41; S-034 pp. 1, 17, 52; S-035 pp. 23, 48, 57, 77, 82, 83, 86). All are faithful | — | — |

**Totals.** 899 fragments:
- 363 verified in their own source at the stated location, plus the 2 image fragments on the rendered S-034 p. 1 and the TA260 search-log phrase;
- 415 verified in Stage 1 v18;
- 40 attribution artefacts verified in the named source;
- 78 translations, query strings and model phrases.

None was not found, and no source was unreachable.

### Metadata and versions

- **PubMed esummary.**
  - S-101: PMID 20819842, Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMC3057423; Yang M, Rendas-Baum R, Varon SF, Kosinski M.
  - S-102: PMID 25902814, J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMC4406925; seven authors as cited.
  - S-104: PMID 12914662, Health Qual Life Outcomes 2003;1:29, DOI 10.1186/1477-7525-1-29, PMC183845; Snaith RP.
  - S-103 developer paper: PMID 11739822, Neurology 2001;57(11):2034–9, DOI 10.1212/wnl.57.11.2034.
- **S-105.** PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
- **S-106.** Title "Botulinum toxin type A for the prevention of headaches in adults with chronic migraine", TA260, "Published: 27 June 2012", "Last reviewed: 11 January 2016".
- **Newer versions.** A web search finds no published ICHD-4, only "Work in Progress 1" (2024) and the 2025 workshop, so [S-001] is current. No other source has a newer version that changes an element.

### Values checked against sources

- **E-009 and E-028.** Code labels verbatim (pp. 8, 9, 12); `classesOf826` (8.2.6 criterion B, p. 124); the 8.2.3 single-class comment (p. 123).
- **E-032.** Reference levels: 15 for 8.2.3, and 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8. Span: "more than three months" (pp. 122–125).
- **E-041.** All 18 rules match their sources: offsets, anchors, timings, ages and `excludes`.
- **E-045 and E-046.**
  - NICE 1.3.28: 50 % / 30 %. NICE 1.3.29: 30 %.
  - IHS Q6: ≥ 50 %; the ≥ 30 % chronic alternative; MIDAS ≥ 5 points (baseline 11–20) or ≥ 30 % (baseline ≥ 20); HIT-6 ≥ 5.
  - DMKG/ÖKSG/SKG: 50 %, 5 points, 30 %. Russian section 7.1: 50 %.
  - The four [S-010] control levels.
- **E-057.**
  - HIT-6: 36–78, and "little or no impact (49 or less), some impact (50–55), substantial impact (56–59), and severe impact (60–78)".
  - MIDAS: grades I–IV with the [S-102] labels and bands 0–5, 6–10, 11–20, ≥ 21.
  - PedMIDAS: 0–10, 11–30, 31–50, "Greater than 50".
  - HALT-90: Table 18 with its overlap at 20. HALT-30: no grading.
  - Recall periods: 3 / 1 / 3 / 3 / 1 months.
- **E-059.** HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
- **E-039, E-060, E-063.**
  - NICE 1.3.48: 4–8 weeks.
  - ICHD-3 A1.1: day 1 ± 2 with no day 0, so `windowDaysBefore` = `windowDaysAfter` = 2.
  - A remission "must exceed three months".
- **Dates recomputed:**
  - 41 days for 1 January – 10 February 2026; 294 days for 1 January – 21 October 2026;
  - 26 February – 25 March (28 days) and 26 March (NICE 1.3.28);
  - 1 April (3-month time point);
  - the bout of 42 days (10 July – 20 August) and the remission of 143 days (1 June – 21 October).

### Fidelity check per Stage 1 requirement

| OUT | Statement parts and Caveats checked | Result |
|---|---|---|
| 001 | Start, end and length of every view's period (E-003, E-005, INV-002, INV-003, MUST); frequency outputs per calendar month or 28-day period (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); Caveat (stated length) | OK |
| 002 | Label for every form in which a view reports a measure (INV-008); one definition per measure in a view (INV-111) | OK |
| 003 | Indicator for the period of every summary measure (INV-011, INV-012); SHOULD NOT a validated cut-off (INV-013) | OK |
| 004–007 | Every period of the selected range; ICHD-3 definitions (INV-009 MUST, INV-010 SHOULD); attacks shown separately; MUST, MUST, SHOULD, SHOULD, with the OUT-001 MUST where provided | OK |
| 008 | MAY measures; exploratory annotation MAY (E-020 to E-022) | OK |
| 009 | Series with start, dose-change and stop markers in the view; weekly values where relevant (INV-034 to INV-036, INV-001) | OK |
| 010, 011 | Intensity on a stated scale, compared between periods (INV-018, INV-032, INV-039); duration, with the treated-attack label (SHOULD) and the Caveat (SHOULD NOT) (INV-019 to INV-021) | OK |
| 012, 013 | Symptoms across periods and per treated attack (INV-022, INV-072, INV-076); aura MAY (E-027) | OK |
| 014–016 | Total, class and drug (INV-023, INV-024); weekly view (INV-025); indicator per period, per class and for 8.2.6, with code, level and span (INV-044 to INV-046); prompt MUST (INV-047); not a diagnosis, MUST NOT (INV-048) | OK |
| 017 | From the start of withdrawal; review window; the following year; worsening label (INV-049 to INV-052) | Represented. The tie of the view to a real start of withdrawal holds only at SHOULD: **R31-01** |
| 018 | Comparison per preventive treatment with the values and both changes (INV-053 to INV-057); time points by type and population (E-041, INV-055, INV-058, INV-059); Caveat at MUST NOT (INV-106) | OK |
| 019, 020 | Residual burden (INV-060, INV-061); labels with criterion, values and other values, not the sole indicator (INV-062 to INV-065) | Represented. The identity of a label's underlying values holds only at SHOULD: **R31-01** |
| 021 | MUST and SHOULD components for the same periods (INV-068, INV-069, INV-102) | OK |
| 022 | View after every stop, pause or reduction (INV-103); on-treatment period and original baseline (INV-070) | Represented. The event and the periods' defining bounds hold only at SHOULD: **R31-01** |
| 023 | Outcomes, consistency, timing, formulation, phases, 15 minutes for cluster headache, Caveat (INV-071 to INV-075, INV-107) | OK |
| 024 | History with dates, dose changes, duration (v30: tied to the course), response, adverse effects, stop reason, formulation, grouping and order (INV-077 to INV-079, INV-109) | OK |
| 025, 039 | Scheme windows MAY (E-056, INV-080); adherence next to the comparison, in the history and in the clinician summary (INV-066, INV-067, INV-104, INV-109) | OK |
| 026, 027 | Instrument results with name, date, recall, score, grading and change (INV-081, INV-082); functional impact and its comparison with the baseline period (INV-026, INV-027) | OK |
| 028–031 | Three-month view with its MUST, SHOULD and SHOULD NOT parts (INV-040 to INV-043); per headache type (INV-028 to INV-030); menstrual view MUST (INV-086, INV-087); cluster view (INV-088, INV-089) | OK |
| 032–036, 038 | Trigger caveats; screening; clinician and patient views; paediatric (a)–(d) and Caveat; interpretive caveats (INV-083 to INV-101, INV-104, INV-105, INV-110) | OK |
| 037 | No primary index for migraine (SHOULD NOT); exploratory label and components (SHOULD); AUC with headache days (INV-091 to INV-093) | Represented. The period and scope of the components hold only at SHOULD: **R31-01** |

Every conformance level matches the strength of the Stage 1 statement part it realises. MUST NOT is used for OUT-016 and the OUT-018 Caveat, and SHOULD NOT for SHOULD parts and Caveats. R31-01 does not dispute the level of any Stage 1 statement part. It concerns conjuncts that state what an element is, which section 3.3 (5) gives no level.

### Mechanical checks (`mech.py`, `names.py`, `inv079.py`)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111): none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn, section 9). |
| References | No dangling E-, INV- or ISS- reference. Every OUT reference exists in Stage 1 (39 requirements). The 37 cited source IDs are all within S-001–S-046 or S-101–S-106. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`, and every invariant states its scope. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2). No SHOULD or MAY attribute, and no MUST attribute with a `when` clause, lacks an `opt`, `set` or `seq` type. |
| Names | 182 `omn` blocks; 554 declared names, none declared twice; every constructor argument name is a declared component. The only unresolved tokens are `c`, the free context variable of INV-001 (section 2.9), and the operator `Σ`. Every attribute selection names a declared attribute. |
| Definedness | Every partial term in the v30 conjunct is guarded (`s ≤ e.date ∧ …`, `s ≤ ctx.asOf ∧ …`). I spot-checked `÷`, `min`, `max`, `first`, `last` and `s(i)` in INV-012, INV-045, INV-053, INV-069, INV-074, INV-087 and INV-089. |
| INV-079 (v30) | 147 one-course contexts with integer days (every start, stop and as-of date up to 7, under the INV-001 order) and 94,080 lines (every shown start date, stop date and duration of 1–9 days, or none). Results: 0 admitted lines show a wrong duration; 0 admit a duration without a stated start; 0 reject the true duration with correct or omitted dates; every v30-admitted line is v29-admitted. The Reading ("whether or not the line shows its start and stop dates") and the Notes hold. |
| R31-01 | Which invariants constrain the attributes in question, by level (script over every predicate). E-049 `treatment`, `event`, `eventDate`, `baseline`, `onTreatmentPeriod`, `after`: only INV-070, INV-097 and INV-103, all SHOULD. E-039 `withdrawalStart`: INV-049 and INV-050 (SHOULD) and INV-051 (definitional, but only relative to `withdrawalStart`). E-046 `comparison` (treatment): INV-062 (SHOULD); INV-063 and INV-064 only condition on it. E-033 `components`: INV-092 (SHOULD) only. |
| Scope sweep | I read in context every occurrence of enter, record, input, store, persist, database, serializ, encod, retention, reminder, algorithm, "computed from", "obtained from", answer, questionnaire, data-entry, JSON, XML, CSV, FHIR, HL7 and capture. Each is one of: an exclusion statement; "obtained from diary information; how is out of scope"; the notation's "records"; an instrument name or a search-log string; the [S-014] HALT-30 sentence (settled); or the INV-076 statement that assigning attack lines to types would be a derivation from input. |

## Remarks

### R31-01 Formal defect (definitional content stated at SHOULD; contradiction with section 3.3 (5) and with INV-036, INV-058, INV-061, INV-079, INV-110): four content invariants let a MUST-conformant output show a stop that did not happen, an "original pre-treatment baseline" on treatment, a withdrawal that did not start, another treatment's values as a label's underlying values, or another month's values as an index's components

- **Item(s):**
  - INV-070 (E-049): the conjuncts on the treatment, the event, its date and the periods;
  - INV-050 (E-039): `v.withdrawalStart ∈ ctx.subject.withdrawalStart`;
  - INV-062 (E-046): `rc.treatment = L.treatment`;
  - INV-092 (E-033): `m.period = x.period ∧ m.typeScope = x.typeScope`;
  - Conformance and Notes of E-033, E-039, E-046 and E-049; rows OUT-017, OUT-020, OUT-022 and OUT-037.
- **Problem:**
  - **The model's rule.** Section 3.3 (5) says that an invariant stating "a bound that follows from an element's definition [...] or the structure of an element (for example that a series is consecutive) is *definitional*". It "holds wherever the element is shown", and "the level of the element or attribute decides whether the element is shown at all". It "excludes only outputs that show a value contradicting the definition of the element, which no Stage 1 requirement permits". Section 3.2 makes a diary MUST-conformant when its repertoire satisfies "every definitional invariant [...] and every MUST and MUST NOT constraint". So a SHOULD constraint binds only full conformance, and even there it is waivable "where a valid reason in particular circumstances justifies a deviation".
  - **Four content invariants mix the two kinds.** Each states, at its own level SHOULD, both the content that Stage 1 asks for at SHOULD and conjuncts that only say what the element is:
    1. **INV-070 (E-049, post-stop monitoring).**
       - The shown facts: `v.treatment ∈ ctx.subject.preventiveTreatments`; `(v.event is stop ∨ v.event = doseChange(reduction))`; `eventOn(ctx, v.treatment, v.event, v.eventDate)`.
       - The bounds that E-049's own declarations define:
         - `baseline`: "the original pre-treatment baseline period, before the treatment was first started";
         - `onTreatmentPeriod`: "an on-treatment period before the changed regimen";
         - `after`: "consecutive periods from the first day of the changed regimen onward".
       - The conjuncts that state these bounds: `(∀ b ∈ v.baseline • ∃ s ∈ originalStart(ctx, v.treatment) • b.end < s)`; `consecutive(v.after)`; `(∀ q ∈ v.onTreatmentPeriod • courseBegunBy(ctx, v.treatment, q.start) ∧ q.end < x)`; `(v.after ≠ ∅ ⇒ first(v.after).start = x)`.
    2. **INV-050 (E-039, withdrawal follow-up).** `v.withdrawalStart ∈ ctx.subject.withdrawalStart`. The view is defined "For a patient withdrawing from overused medication [...] from the start of withdrawal onward" (E-039 Meaning). INV-051, which is definitional, derives the NICE review window from this date.
    3. **INV-062 (E-046, responder label).** `rc.treatment = L.treatment` for the comparison the label shows. E-046 declares `comparison` as "the underlying values (OUT-018)" of a label that "classifies the response to a preventive treatment".
    4. **INV-092 (E-033, composite index).** `m.period = x.period ∧ m.typeScope = x.typeScope` for the components. E-033 declares `components` as "the component measures shown with it".
  - **No definitional or MUST invariant states these ties** (mechanical check above). They therefore hold only at SHOULD, while their elements are SHOULD (E-039, E-049) or optional (E-046, E-033). This is a different matter from the SHOULD of showing the element or its content.
  - **The model states the same kind of tie definitionally everywhere else:**
    - a marker's event and date, `eventOn(ctx, mk.treatment, mk.event, mk.date)` (INV-036, the same predicate as in INV-070);
    - a time point's anchor date (INV-058);
    - a treatment line's dates and response (INV-079, including `∀ r ∈ l.preventiveResponse • r.treatment = l.treatment`, the counterpart of the INV-062 tie);
    - the measures, scope and period of a residual burden's values relative to its change (INV-061, the counterpart of the INV-092 tie);
    - the dates a trigger view shows (INV-110), whose Notes give the reason: "Without the relation, a view could state one reporting period and show the dates of another";
    - an adherence summary's treatment and window (INV-067);
    - an attack line's drug (INV-075).

    The SHOULD or MAY elements E-034, E-044, E-055, E-062 and E-065 all have such definitional invariants. E-049, E-039, E-046 and E-033 are the only element kinds whose ties to the context, or to the item they belong to, are not definitional.
- **Evidence:**
  - **Admitted outputs (v30), all checked against the invariants that mention the attributes concerned.** Context: an adult subject; a preventive treatment t, given for migraine, started on 1 January 2026 and discontinued on 30 June 2026, its last day on treatment; a second preventive treatment u started on 1 August 2026; no start of withdrawal; as of 21 October 2026. A repertoire that satisfies every definitional, MUST and MUST NOT invariant may contain:
    1. A post-stop monitoring view of t with `event = stop(paused)` and `eventDate` = 31 March 2026, an event the context does not have. Its periods:
       - "original pre-treatment baseline": May 2026, a month on treatment;
       - "on-treatment period": August 2026, a month after the stop;
       - "periods after the event": February 2026 and April 2026, months on treatment, not consecutive.

       Only INV-070 (SHOULD) fails; INV-097 does not apply, because the subject is an adult. The output presents a pause that did not happen and hides the rebound "above baseline" that OUT-022 is to make visible.
    2. A withdrawal follow-up view with `withdrawalStart` = 1 February 2026, a withdrawal that did not happen. By INV-051 (definitional) it shows the "NICE CG150 1.3.48 review window" from 1 to 29 March 2026. Only INV-050 (SHOULD) fails.
    3. A responder label of t whose `comparison` is the response comparison of u. Only INV-062 (SHOULD) fails. INV-063 decides nothing, because no comparison of t is shown, so the label "responder" stands next to the values of another treatment.
    4. A composite index for migraine of January 2026 whose `components` are the headache days and intensity of June 2026. Only INV-092 (SHOULD) fails.
  - **The principle was applied in iteration 30.** Fix 30 accepted R30-01 on it: "INV-079 is definitional. Section 3.3 (5) says that a definitional invariant 'holds wherever the element is shown' [...]. A deviation from the SHOULD of a date does not make a false duration valid." No valid reason can justify showing an event the subject did not have, so these conjuncts are not SHOULD content.
  - **Stage 1 has no statement part that the conjuncts realise at SHOULD.**
    - OUT-022 asks the output to "continue to show headache and migraine frequency and compare it with both the on-treatment period and the original pre-treatment baseline" "After a preventive treatment is stopped, paused or reduced".
    - OUT-017 asks for the view "For patients withdrawing from overused medication".
    - OUT-020 asks the output to "show the underlying values (OUT-018, OUT-019)".
    - OUT-037 asks for an index to be "shown together with its component measures".

    The SHOULD of each concerns whether the content is shown. Moving the ties to definitional status makes no content more required (section 3.3 (5)).
  - **Not considered before.**
    - Fix 26 wrote "INV-070 keeps its level. It stays SHOULD, the strength of OUT-022". It weighed the level of the invariant's content against OUT-022, not the definitional character of its bounds.
    - R27-01 and R28-01 (and fixes 27 and 28) changed what INV-070 admits as the original baseline and the on-treatment period. None of them examined the level at which these bounds hold.
    - The iteration-24 oscillation check records the class "Truth of a shown fact tied to the context", where each remark "adds a definitional conjunct that excludes only outputs stating something false". These four invariants were never reached by it.
    - The level of INV-050, INV-062, INV-070 and INV-092 has been SHOULD since v00, so this is not a consequence of fixes 25–30.
- **Required change:**
  - **(a) Preferred: state the ties as definitional invariants, verbatim, and keep each invariant's presence content at SHOULD.**
    - **E-049.** A new definitional invariant for E-049, for example INV-112, with these conjuncts of INV-070, removed from INV-070:
      - `v.treatment ∈ ctx.subject.preventiveTreatments`;
      - `(v.event is stop ∨ v.event = doseChange(reduction))`;
      - `eventOn(ctx, v.treatment, v.event, v.eventDate)`;
      - `(∀ b ∈ v.baseline • ∃ s ∈ originalStart(ctx, v.treatment) • b.end < s)`;
      - `consecutive(v.after)`;
      - within `∀ x ∈ firstChangedDay(v.event, v.eventDate)`: `(∀ q ∈ v.onTreatmentPeriod • courseBegunBy(ctx, v.treatment, q.start) ∧ q.end < x)` and `(v.after ≠ ∅ ⇒ first(v.after).start = x)`.

      INV-070 keeps, at SHOULD, the presence conjunct `startOf(ctx, v.treatment) = ∅ ∧ courseBegunBy(ctx, v.treatment, plusDays(x, −1)) ⇒ v.onTreatmentPeriod ≠ ∅` and the `shownDay` conjunct.

      Acceptable variant: keep `consecutive(v.after)` and `first(v.after).start = x` at SHOULD and state definitionally only `∀ p ∈ ran v.after • x ≤ p.start`. No period shown as after the event may contain a day of the earlier regimen.
    - **E-039.** `∀ v : WithdrawalFollowUpView • v.withdrawalStart ∈ ctx.subject.withdrawalStart`: as a conjunct of INV-051, which is already definitional for E-039, or in a new definitional invariant. Remove it from INV-050.
    - **E-046.** `∀ L : ResponderLabel; rc ∈ L.comparison • rc.treatment = L.treatment`: as a conjunct of INV-063, which is definitional for E-046, or in a new invariant. INV-062 keeps its existential at SHOULD.
    - **E-033.** A definitional invariant `∀ x : CompositeIndex; m ∈ x.components • m.period = x.period ∧ m.typeScope = x.typeScope`. Restricting it to `concerns(ctx, x.typeScope, c1)`, as in INV-092, is acceptable. Remove the two equalities from INV-092, which keeps the annotation, the co-presence `m ∈ viewOf(x).content` and the dimension coverage at SHOULD.
  - **(b) Alternatively,** mark INV-070, INV-050, INV-062 and INV-092 as definitional, and move their presence conjuncts into new SHOULD invariants. The result is the same.
  - **In either case:**
    - change no conjunct's text, no `when` clause of E-049, and no course-event date;
    - update the Conformance and Notes of E-033, E-039, E-046 and E-049, the Realises fields, and rows OUT-017, OUT-020, OUT-022 and OUT-037 (and section 7's columns if new IDs are added).
  - **Effect.** What a fully conformant diary may show is unchanged. Only outputs that state a false fact are excluded, at every conformance level.
  - **Watch points (oscillation check after iteration 28).** This is not a reversal:
    - watch point 1: the INV-070 presence conjunct stays, `courseBegunBy` stays, no on-treatment ask is dropped, and the start-aligned versus event-aligned classification is untouched;
    - watch point 2: `originalStart`, `resumes`, the E-049 `baseline` `when` clause and the baseline conjunct are kept verbatim;
    - watch point 5: the two places that ask for the on-treatment period are unchanged.

    Every admitted set narrows or stays equal.

## Checked and not raised

- **The v30 change.** The INV-079 conjunct is well typed and guarded. It admits only the true duration, whatever dates the line shows, and admits none without a stated start (script above). The INV-079 Reading and Notes, the E-055 Notes, the INV-109 Reading and the OUT-024 coverage reason state exactly that. The [S-013] quote added to the INV-079 Evidence is verbatim in Stage 1 OUT-024.
- **Scope of the v30 conjunct.** Its arguments are the course start and the one stop or pause of the context, and the as-of date. These are properties of the subject's treatment course that the line itself shows (the start and stop dates of OUT-024). The model states them as facts of the subject, not as recorded data, and says "How these properties become known is outside the model" (E-008, section 3.5). INV-036, INV-058, INV-075 and INV-079 use the same arguments. No counting procedure over diary records is stated, so this is not a derivation from input (precedent: R30-01 and fix 30).
- **INV-078 at SHOULD.** Its role and class conjuncts realise the SHOULD statement parts "(and, separately, acute)" and "grouped by drug class" of OUT-024. A diary that deviates from the grouping has no other way to place lines in `ClassGroup`s, so these conjuncts keep the level of OUT-024. They are not ties of the kind in R31-01.
- **INV-035, and INV-050's other conjuncts.** The time-course view covering exactly its series, the withdrawal view beginning on the start of withdrawal, and its series starting there realise the SHOULD parts of OUT-009 and OUT-017 ("from the start of withdrawal onward"). A view that deviates still states its covered period truly (INV-003). Not raised.
- **One-month baseline of the response comparison (INV-056).** OUT-018 compares "monthly migraine days and monthly headache days [...] in a pre-treatment baseline period". The model's per-period counts (OUT-005) and [S-005]'s "if a baseline period is 28 days" support a monthly baseline. Other baselines may be shown as `OtherItem`s, so no output Stage 1 permits is excluded. Not raised.
- **Section 8.**
  - ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded, and their quotes are verbatim at the stated locations. "Simple analgesics" occurs once in ICHD-3, on p. 139. "ibuprofen or other NSAIDS" is on p. 105, and the 3.1.1 and 3.1.2 passages are on p. 42.
  - The descriptions of the Stage 1 passages are accurate. ISS-09's description of Group D without OUT-017 is a settled point (check after iteration 28).
  - No Stage 1 issue is worked around silently. R31-01 is a model defect.
- **Locations re-checked on the page:** the Turkish section 7.1 sentences (above "7.2" on PDF p. 83); the Russian p. 41 sentence on anti-CGRP antibodies; Kutu 8 items 2 and 7; the PHQ-9 and GAD-7 ranges under "USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES" (P. 6/9).
- **S-104 categories.** Snaith also describes four HADS ranges (normal, mild, moderate, severe). Stage 1 OUT-033 asks for "instrument name, date and score" only, so the model correctly states no categories.
- **Settled points, not reopened (no new evidence):**
  - INV-106 at MUST NOT; the "> 3 months" readings of INV-045 and INV-089; INV-023 at any granularity; INV-027 tied to preventive treatments;
  - the E-041 readings, ages and `excludes`; the MIDAS labels and Grade IV undivided; the HIT-6 one-month recall; HADS subscales only; the HALT-90 overlap at 20;
  - the E-063 and E-058 derived attributes (fix 02 item 14); empty `remissions` in chronic cluster headache (ISS-12); "history of previous bouts";
  - INV-060 with INV-061 for short compared periods; comparison periods beyond the as-of date; E-039 `reviewWindow` without a `when` clause;
  - the acute part of optimal control; the 24-hour outcomes of 15-minute summaries; the [S-014] HALT-30 sentence with "records".
- **Oscillation watch points.** R31-01 touches INV-070, which watch points 1, 2 and 5 name. As stated in the remark, it changes no conjunct, no `when` clause and no date. It only lifts the level of conjuncts that state what the element is, so it reverses no fix and widens nothing. INV-050, INV-062 and INV-092 are in no watch point.

## Notes on frozen items (for the human)

None.
