# Review — iteration 32
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v31
Date: 2026-10-22

## Summary

This is the main review of iteration 32, by a new, independent reviewer. I checked v31 against its sources and against Stage 1 v18.

**State of the files.**
- `OUTPUT_MODEL.md` is v31 ("Version: v31 · Iteration: 31 · Status: under review"). It is byte-identical to `history/v31.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line.
- The v30 → v31 `omn` diff is the one the change log states:
  - four blocks changed (INV-050, INV-062, INV-070, INV-092);
  - four blocks added (INV-112 to INV-115).
  - Each moved conjunct is verbatim. No other formal block changed.
  - The IDs INV-112 to INV-115 occur in no earlier snapshot (v00–v30), so no ID is reused.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5.
- v31, sections 1–10: notation, conformance, all 67 elements and 115 invariants, traceability, section 8 and sources. Also the v31 entries of sections 11 and 12, and the search-log rows used for the source checks.
- Loop files:
  - review 31 and fix 31;
  - the "Checked and not raised" lists of reviews 29 and 30;
  - the oscillation check after iteration 28, with its seven watch points;
  - the earlier review and fix passages on the points listed under "Checked and not raised" below (reviews 02, 19b, 21b, 23, 27; fixes 03, 12).

**Result.** I found no issue that requires a change under PROCESS.md section 9.
- **Citations.** I downloaded every source that carries a Stage 2 quote. Every quoted fragment is verbatim at its stated location, and the translations are faithful. Metadata and versions are correct. ICHD-3 is still the current edition: only ICHD-4 "Work in Progress 1" (2024) has been published.
- **Values.** All value sets, ranges, bands, code labels, reference levels, offsets, thresholds and control levels match their sources.
- **Scope.** The model contains no input, storage or input-derivation content. Every threshold, formula and computed field that is part of the output data is present.
- **Fidelity.** All 39 requirements are fully represented, and every conformance level matches the strength of its Stage 1 statement part.
- **Mechanical checks.** All pass: IDs, references, fields, traceability, levels, the typing rule for levels, and name resolution.
- **The v31 change.** It moves each identity tie verbatim into a definitional invariant, as R31-01 asked, and it reverses no watch-point item. Every text that refers to the split invariants is still correct.

## Verification coverage

### Downloads and tools

- **Where.** Every source was downloaded with `curl` through the proxy into the fresh folder `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r32/src`, outside the repository. Scripts are in `.../scratchpad/r32/scripts`, outputs in `.../scratchpad/r32/out`, and every script was run with `python3 -I`.
- **Text extraction.**
  - PDFs: per-page text with `pdftotext`, in both `-raw` and default mode.
  - HTML and Europe PMC full-text XML: stripped to text (`strip.py`).
  - The S-034 title page, an image without a text layer, was rendered with `pdftoppm` and read: "Клинические рекомендации Мигрень", "Возрастная группа дети", "Год утверждения 2024".
- **HTTP.** Every request returned HTTP 200 on the first attempt, including apicr.minzdrav.gov.ru for S-033 and S-034. No source was unreachable.
- **Quote matching (`quotes.py`).**
  - Fragments: every double-quoted string outside the `omn` blocks, split at "[...]", keeping fragments of at least 6 letters or digits.
  - Normalisation: NFKD, combining marks, soft hyphens and the ICHD-3 "þ" glyph removed, case folded, letters and digits only. This joins line-end hyphens and drops glyphs without a text mapping ("≥", "±", "−").
  - Search order: the source tagged nearest before the fragment on its line, page by page; then Stage 1 v18; then every downloaded source.
  - Locations: for every Stage 2-only hit in a PDF, I compared the page against the stated location by hand. For web and XML sources, I checked the enclosing section heading by script.

### Quote check per source

| Source | Fragments attributed | Verbatim at stated location | Not found | Unreachable (tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (PDF, 211 pp.) | 75 | 73 in the PDF; 1 in Stage 1 only. Pages: 8, 9 and 12 (classification list), 42, 105, 122–125, 139, 190 and 209. | 0 (1 model phrase in the search log) | — |
| S-007 IHS cluster (UCL accepted manuscript, 39 pp.) | 9 | 9 (p. 10, section 2.2; the rest in Stage 1) | 0 | — |
| S-008 IHS 2024 preventive (univaq PDF) | 27 | 25 (pp. 9, 12, 13, 17); 2 attribution artefacts found in S-008 | 0 | — |
| S-010 IHS 2025 position statement (univaq PDF) | 38 | 38 (p. 6) | 0 | — |
| S-011 EHF 2022 (Europe PMC XML) | 22 | 21; 1 artefact. Background; question 3, "Clinical guidance". | 0 | — |
| S-012, S-013 (Europe PMC XML) | 1 + 4 | 4; 1 artefact | 0 | — |
| S-014 EHF/LTB aids (Europe PMC XML) | 37 | 37. HALT paragraphs; "Scoring HALT"; Table 18 with its rows 0–5, 6–10, 11–20 and ≥20. | 0 | — |
| S-015 NICE CG150 (Recommendations and Overview pages) | 42 | 41; 1 artefact. Recs 1.3.9, 1.3.24, 1.3.26 (with the TA260 sentence), 1.3.27–1.3.29, 1.3.39 and 1.3.48. "Last updated: 03 June 2025"; Overview "Last reviewed: 23 September 2026". | 0 | — |
| S-016 SIGN 155 (PDF; PDF page = printed page + 6) | 9 | 8 (PDF p. 7 = printed p. 1); 1 artefact | 0 | — |
| S-018 AAN/AHS clinician summary (PDF) | 13 | 12 (pp. 1, 7, 8); 1 artefact | 0 | — |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML) | 6 | 6 | 0 | — |
| S-028 NVN module (web page) | 13 | 11, including the PICO under "Zoeken en selecteren"; 1 artefact | 0 (1 translation) | — |
| S-033 Russian adults (official PDF, 92 pp.) | 47 | 33. Pages 1, 4, 39, 40 and 41; the p. 41 anti-CGRP sentence, as stated. | 0. Of the other 14: 10 artefacts found in the source the sentence names, and 4 translations. | — |
| S-034 Russian children (official PDF, 53 pp.) | 17 | 11 (pp. 17, 52) | 0. The title-page fragment was checked on the rendered p. 1. The other 5 are translations. | — |
| S-035 Turkish protocol (PDF, 92 pp.) | 50 | 34. PDF pp. 7, 23, 48 (Kutu 8, items 2 and 7), 57 (3.6.3.9), 77, 82–83 (7.1, above the heading "7.2") and 86 (7.3). | 0. Of the other 16: 3 artefacts and 13 translations. | — |
| S-101 HIT-6 validation (Europe PMC XML) | 4 | 4 (Methods > "Data sources") | 0 | — |
| S-102 AMPP menses / MIDAS (Europe PMC XML) | 9 | 6 (Methods > "Headache impact on functioning" > "Migraine-related disability"); 2 artefacts | 0 (1 label of another paper, quoted in the search log) | — |
| S-103 PedMIDAS page (Cincinnati Children's) | 10 | 10 ("PedMIDAS Grading Scale"; footer "© 2026 Cincinnati Children's Hospital Medical Center") | 0 | — |
| S-104 HADS (Europe PMC XML) | 3 | 3 ("Construction of the Hospital Anxiety And Depression Scale (HADS)") | 0 | — |
| S-105 PHQ/GAD-7 manual (PDF, 9 pp.) | 3 (+2 in section 10) | 5 (P. 6/9; the development sentence on P. 8/9) | 0 | — |
| S-106 NICE TA260 (chapters 1 and 2, overview) | 5 | 4 (paragraph 2.1; the search-log phrase is in recommendation 1.2); 1 artefact | 0 | — |
| Stage 1 quotes reused by reference (S-002, S-005, S-022, S-029, S-030, S-032, S-042 and untagged) | 368 untagged + Stage 1 tags | 448 fragments verbatim in Stage 1 v18 (the evidence carries over) | 0 | not re-downloaded |
| Translations, query strings, change-log and model phrases | 84 | Not source quotes. I read all 22 translations of Stage 2 quotes against their originals (S-028; S-033 pp. 1, 39, 40, 41; S-034 pp. 17, 52; S-035 pp. 23, 48, 57, 77, 82, 83, 86), and all are faithful. The other 62 are 22 search-log strings, 21 change-log phrases and 18 model-internal phrases. | — | — |

The "verbatim" counts per source add two groups: fragments found in the downloaded source itself, and fragments tagged with that source that are Stage 1 quotes, found in Stage 1 v18. The second group is: S-001 1, S-007 1, S-008 6, S-010 5, S-011 8, S-014 6, S-015 6, S-016 1, S-018 2, S-023 1, S-028 1, S-033 12, S-034 3 and S-035 1.

**Totals.** 916 fragments, all accounted for:
- 340 were found in their own attributed source; 197 of them are Stage 2-only quotes, each at its stated location;
- 448 were found in Stage 1 v18;
- 44 are attribution artefacts, each found in the source that its sentence names;
- 84 are translations, query strings or model phrases, plus the image fragment checked on the rendered page.

None was not found, and no source was unreachable.

### Metadata and versions

- **PubMed esummary.**
  - S-101: PMID 20819842; Cephalalgia 2011;31(3):357–67; DOI 10.1177/0333102410379890; PMC3057423; Yang M, Rendas-Baum R, Varon SF, Kosinski M.
  - S-102: PMID 25902814; J Headache Pain 2015;16:24; DOI 10.1186/s10194-015-0503-y; PMC4406925; seven authors as cited.
  - S-104: PMID 12914662; Health Qual Life Outcomes 2003;1:29; DOI 10.1186/1477-7525-1-29; PMC183845; Snaith RP.
  - S-103 developer paper: PMID 11739822; Neurology 2001;57(11):2034–9; DOI 10.1212/wnl.57.11.2034.
- **S-105.** PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
- **S-106.** TA260, "Published: 27 June 2012", "Last reviewed: 11 January 2016"; the title is as cited.
- **Newer versions.**
  - A web search (Cephalalgia "International Classification of Headache Disorders-4 – Work in Progress 1", 2024; IHS classification committee page, ICHD-IV workshop 2025) finds no published ICHD-4, so [S-001] is current.
  - No other S-1xx source has a newer version that changes an element.

### Values checked against sources

- **E-009 and E-028.**
  - Code labels verbatim on pp. 8, 9 and 12.
  - `classesOf826` matches 8.2.6 criterion B (p. 124); `classesOf821to825` matches 8.2.6 note 2 (p. 125).
  - The 8.2.3 single-class comment is on p. 123.
- **E-032.** Reference levels: 15 for 8.2.3; 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8. Span "more than three months" (pp. 122–125).
- **E-041.**
  - All 18 rules match their sources: offsets, anchors, timings, ages and `excludes`.
  - Re-read on the page: IHS 2024 Q2 Optimal and Essential (p. 9; the onabotulinumtoxinA dose comment is not a time point); AAN/AHS 14A and 14B (p. 7) and 14H (p. 8); SIGN section 4.1; Russian sections 3.3 and 7.1; Turkish Kutu 8 and sections 3.6.3.9 and 7.3.
- **E-045 and E-046.**
  - NICE 1.3.28: 50 % / 30 %. NICE 1.3.29: 30 %.
  - IHS Q6: ≥ 50 %; the ≥ 30 % chronic alternative; MIDAS ≥ 5 points (baseline 11–20) or ≥ 30 % (baseline ≥ 20); HIT-6 ≥ 5.
  - DMKG/ÖKSG/SKG: 50 %, 5 points, 30 %. Russian section 7.1: 50 %. Turkish Kutu 8: 50 % attack frequency.
  - The four [S-010] control levels: 0; < 4 for three months; 4–6; > 6, with insufficient control also possible at fewer days.
- **E-057.**
  - HIT-6: 36–78, with bands ≤ 49, 50–55, 56–59 and 60–78.
  - MIDAS: I–IV with the [S-102] labels and bands 0–5, 6–10, 11–20 and ≥ 21.
  - PedMIDAS: 0–10, 11–30, 31–50 and "Greater than 50" (`strictLow`).
  - HALT-90: Table 18, with its overlap at 20. HALT-30: no grading.
  - Recall periods: 3, 1, 3, 3 and 1 months.
- **E-059.** HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
- **E-039, E-060, E-063, E-064.**
  - NICE 1.3.48: 4–8 weeks.
  - ICHD-3 A1.1: day 1 ± 2, with no day 0.
  - A remission "must exceed three months".
  - IHS cluster: "≥ 14 attacks per week on average" is quoted only for the meaning of an average weekly rate.
- **Dates recomputed:**
  - 41 days for 1 January – 10 February 2026, and 294 days for 1 January – 21 October 2026;
  - 26 February – 25 March (28 days) and 26 March (NICE 1.3.28);
  - 28 February and 31 March as the ends of the Turkish Box 8 and 3-month intervals;
  - 4–31 December 2025 (28 days);
  - the bout of 42 days (10 July – 20 August) and the remission of 143 days (1 June – 21 October).

### Fidelity check per Stage 1 requirement

| OUT | Statement parts and Caveats checked | Result |
|---|---|---|
| 001 | Start, end and length of every view's period (E-003, E-005, INV-002, INV-003, MUST). Frequency outputs per calendar month or 28-day period (INV-014, INV-015, INV-108). Equal-length comparisons (INV-037, INV-055). Caveat: the stated length. | OK |
| 002 | A label for every form in which a view reports a measure (INV-008, SHOULD); one definition per measure in a view (INV-111) | OK |
| 003 | Indicator for the period of every summary measure (INV-011, INV-012); no cut-off presented as validated, SHOULD NOT (INV-013) | OK |
| 004–007 | Every period of the selected range. ICHD-3 definitions (INV-009 MUST, INV-010 SHOULD). Attacks shown separately. Levels MUST, MUST, SHOULD and SHOULD, with the OUT-001 MUST wherever provided. | OK |
| 008 | MAY measures; the exploratory annotation MAY (E-020 to E-022) | OK |
| 009 | Series with start, dose-change and stop markers in the view; weekly values where relevant (INV-034 to INV-036, INV-001) | OK |
| 010, 011 | Intensity on a stated scale, compared between periods (INV-018, INV-032, INV-039). Duration, with the treated-attack label at SHOULD and the Caveat at SHOULD NOT (INV-019 to INV-021). | OK |
| 012, 013 | Symptoms across periods and per treated attack (INV-022, INV-072, INV-076); aura at MAY (E-027) | OK |
| 014–016 | Total, class and drug (INV-023, INV-024). Weekly view (INV-025). Indicator per period, per class and for 8.2.6, with code, level, span and basis (INV-044 to INV-046). Prompt at MUST (INV-047); not a diagnosis at MUST NOT (INV-048). | OK |
| 017 | From the start of withdrawal; the review window; the following year; the worsening label (INV-049 to INV-052). The start of withdrawal is the subject's at every level (INV-113, v31). | OK |
| 018 | Comparison per preventive treatment, with the values and both changes (INV-053 to INV-057). Time points by type and population (E-041, INV-055, INV-058, INV-059). Caveat at MUST NOT (INV-106). | OK |
| 019, 020 | Residual burden (INV-060, INV-061). Labels with criterion, underlying and other values, not the sole indicator (INV-062 to INV-065). The comparison is of the label's treatment at every level (INV-114, v31). | OK |
| 021 | MUST and SHOULD components for the same periods (INV-068, INV-069, INV-102) | OK |
| 022 | View after every stop, pause or reduction (INV-103). Content (INV-070). The event and periods of the subject's course at every level (INV-112, v31). | OK |
| 023 | Outcomes, consistency, timing, formulation, phases, 15 minutes for cluster headache, Caveat (INV-071 to INV-075, INV-107) | OK |
| 024 | History with dates, dose changes, duration, response, adverse effects, stop reason, formulation, grouping and order (INV-077 to INV-079, INV-109) | OK |
| 025, 039 | Scheme windows at MAY (E-056, INV-080). Adherence next to the comparison, in the history and in the clinician summary (INV-066, INV-067, INV-104, INV-109). | OK |
| 026, 027 | Instrument results with name, date, recall, score, grading and change (INV-081, INV-082). Functional impact and its comparison with the baseline period (INV-026, INV-027). | OK |
| 028–031 | Three-month view with its MUST, SHOULD and SHOULD NOT parts (INV-040 to INV-043). Per headache type (INV-028 to INV-030). Menstrual view at MUST (INV-086, INV-087). Cluster view (INV-088, INV-089). | OK |
| 032–036, 038 | Trigger caveats; screening; clinician and patient views; paediatric (a)–(d) and the Caveat; interpretive caveats (INV-083 to INV-101, INV-104, INV-105, INV-110) | OK |
| 037 | No primary index for migraine, SHOULD NOT. Exploratory label and components, SHOULD. Components of the index's period and scope at every level (INV-115, v31). AUC with headache days (INV-091 to INV-093). | OK |

**Levels.**
- MUST NOT is used for OUT-016 and for the OUT-018 Caveat. SHOULD NOT is used for the SHOULD statement parts and Caveats of OUT-003, OUT-011, OUT-020, OUT-023, OUT-028, OUT-033, OUT-037 and OUT-038.
- Every MUST invariant realises a MUST part: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054, 055, 056, 057, 059, 068, 086, 102 and 108.
- MUST attributes of elements that are available only at SHOULD or MAY each cite a MUST part (section 3.3, item 3).

### Mechanical checks (`mech.py`, `names.py`, `claims.py`, `claims_c.py`, `quotes.py`)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 115 invariants (INV-001 to INV-115), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12; ISS-07 is withdrawn (section 9). INV-112 to INV-115 appear in no earlier snapshot. |
| References | No dangling E-, INV- or ISS- reference. Every OUT reference exists in Stage 1 (39 requirements). The 37 cited source IDs all lie within S-001–S-046 or S-101–S-106. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field. Every invariant has exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the sets of items whose Realises field names the requirement: 0 mismatches. |
| Levels and scope | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 38. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. Every invariant states its scope (output 82, repertoire 32, context 1). No repertoire or context invariant uses a bare `ctx`. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2). No SHOULD or MAY attribute, and no MUST attribute with a `when` clause, lacks an `opt`, `set` or `seq` type. |
| Names | 186 `omn` blocks and 531 declared names, none declared twice. Every attribute selection names a declared attribute. Only `Output.views` and `View.content` mention an element type without `→`, so they are the only composition attributes, as section 2.5 states. The other tokens that a crude resolver leaves open are enumeration constants of multi-line declarations, bound parameters, `refs` (section 2.5) and the infix `_⊑_`; I checked each by hand. |
| Definedness | Spot-checked guards: `min` in INV-087; `max A` in INV-069; `i.span(2)` in INV-045; `first(v.after)` in INV-112; `÷` in INV-012, INV-053, INV-074 and INV-089; `days` in INV-002, INV-037, INV-079 and INV-089. All are guarded. |
| Prose claims about predicates (`claims.py`, `claims_c.py`) | INV-045 Notes, "with calendar months or 28-day periods it has four periods": 1,466 cases, 0 violations. INV-087, the window days −2 to +3 and `nextWindowDays` as days −2 and −1: 800 checks, 0 violations. INV-012 Notes, pairwise agreement implies one number of covered days: 6,787 pairwise-agreeing triples, 0 violations. E-006 `fillsPeriod` for 28-day periods, one series of ⌊length/28⌋ periods leaving fewer than 28 days: 172 cases, 0 violations. |
| v31 split | The v30 INV-070, INV-050, INV-062 and INV-092 are each the conjunction of their v31 parts: verbatim conjuncts under the same binders, and for INV-062 because `comparison` is `opt`. Every text that refers to the split invariants still states what they contain: section 2.8, the INV-001 Notes, the E-033, E-039, E-046 and E-049 Conformance and Notes, the INV-068 Notes, ISS-03 and rows OUT-017, OUT-020, OUT-022 and OUT-037. |
| Scope sweep | I read in context every occurrence of enter, record, input, store, persist, database, serializ, encod, retention, reminder, algorithm, capture, JSON, XML, CSV, FHIR, HL7, data-entry, answer, "obtained from", "computed from" and "counted from" in sections 1–10. Each is one of these: an exclusion statement; "obtained from diary information; how is out of scope"; the notation's "records"; the [S-014] HALT-30 sentence (settled); the INV-076 statement that assigning attack lines to types would be a derivation from input; or "28-day periods counted from the first day of p", which concerns output periods. |
| Computed fields present | Each derived field has its relation, or is stated as obtained from diary information. Relations checked: percentage and absolute change against the baseline; total, class and drug days; the 8.2 indicator against its code, level, span and basis; instrument category against score; responder thresholds; control levels; complete cycles; the window mark; the cluster rate against the attack count; remission and line durations against their dates; covered days against the proportion; outcome proportions; change from the baseline instrument score; and the review window and time points against their anchors. No missing threshold or formula found. |

## Remarks

None.

## Checked and not raised

- **The v31 change (R31-01).**
  - INV-112 to INV-115 are well typed and definitional. Each states only what its element is.
  - The presence and co-presence conjuncts stay at SHOULD.
  - No `when` clause, course-event date, `originalStart`, `resumes` or `courseBegunBy` changed, so watch points 1, 2 and 5 of the check after iteration 28 are not crossed.
  - INV-115 keeps INV-092's scope (indices for migraine), so no constraint was added for other indices.
- **Atom equality in INV-115** (`m.period = x.period`). It ties components to the index's period atom, not to the period's dates. This is the model's membership-by-atom principle (INV-003 Notes; INV-038, INV-056, INV-061). It has no effect the reader can see: by INV-006, a component can always be shown on the index's own period atom with the same number. Not a defect.
- **Other SHOULD conjuncts that state what an element is**, after fix 31. I split every SHOULD invariant into its conjuncts and looked for further identity ties.
  - The only candidates are the INV-078 grouping conjuncts and INV-035's covered period. Review 31 kept both at SHOULD with reasons I accept.
  - INV-073's time point and INV-072's formulation list are content choices: each is stated truthfully on the item.
- **Labels of a treatment whose start is not stated.** The `comparison` and `residual` attributes are SHOULD without a `when` clause. For such a label they cannot be met, because no response comparison exists without a stated start (INV-056, INV-114). Such a label lacks the underlying values of OUT-018, which OUT-020 asks it to "always show" at SHOULD, so the deviation is the one Stage 1 itself describes. Not a defect.
- **Subtypes as headache types (INV-028).** A subject whose listed types are two migraine subtypes gets the MUST presentation per type. Stage 1 OUT-029 quotes [S-001] "two or more different headache types or subtypes". Consistent; not raised.
- **Settled points, not reopened (no new evidence):**
  - a label under a criterion whose conditions do not hold is forced to "non-responder" (reviews 02 and 21b);
  - INV-046 "the two directions agree", which fails only for class values inconsistent with the context (reviews 23, 27 and 30);
  - the indicator's `basis` and `span` at MUST (review 19b);
  - INV-106 at MUST NOT; the "> 3 months" readings of INV-045 and INV-089; INV-023 at any granularity; INV-027 tied to preventive treatments;
  - the E-041 readings, ages and `excludes`; the MIDAS labels and Grade IV undivided; the HIT-6 one-month recall; HADS subscales only; the HALT-90 overlap at 20;
  - E-039 `reviewWindow` without a `when` clause; periods beyond the as-of date; INV-060 with INV-061 for short compared periods;
  - "history of previous bouts"; empty `remissions` in chronic cluster headache (ISS-12); the 24-hour outcomes of 15-minute summaries;
  - the E-060 lead-in wording; the [S-014] HALT-30 sentence with "records"; the one-month baseline of the response comparison.
- **Section 8.**
  - ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded, and their quotes are verbatim at the stated locations.
  - "Simple analgesics" occurs exactly once in ICHD-3, on p. 139. "ibuprofen or other NSAIDS" is on p. 105, and the 3.1.1 and 3.1.2 passages are on p. 42.
  - The descriptions of the Stage 1 passages are accurate, for example that OUT-009, OUT-021 and OUT-034 refer to OUT-005 by ID, and the OUT-031 Evidence note on the unquoted duration sentence.
  - No Stage 1 issue is worked around silently.
- **Citation metadata.** S-102 gives the first author as "Pavlovic JM", where PubMed has "Pavlović". The DOI, PMID, PMCID and the text at the URL identify the paper unambiguously. Not a citation defect.
- **Oscillation watch points (check after iteration 28).** This review raises no remark, so it reverses nothing. The one change since the check, v31, narrows only what MUST-conformant diaries admit and keeps every item that the watch points name.

## Notes on frozen items (for the human)

None.
