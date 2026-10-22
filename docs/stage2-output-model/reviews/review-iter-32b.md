# Review — iteration 32 (re-check b)
VERDICT: REMARKS
REMARK_COUNT: 3
Reviewed version: v31
Date: 2026-10-22

## Summary

This is the first independent re-check of iteration 32. I checked v31 against the sources, Stage 1 v18 and the model itself. I read the main review 32 to see what it covered, but every result below comes from my own downloads, scripts and reading.

**State of the files.**
- `OUTPUT_MODEL.md` is v31 and byte-identical to `history/v31.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a FROZEN marker.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5.
- v31, sections 1–10 (all 67 elements and 115 invariants), with the search-log and change-log entries for v29 to v31.
- Loop files: review 32; fix 31; the "Checked and not raised" list of review 31; the watch points of the oscillation checks after iterations 12, 16, 24 and 28; fix 02 item 14. I also searched every review and fix for each point I considered raising (see "Checked and not raised").

**Result.**
- **Citations and values.** I re-downloaded every source that carries a Stage 2 quote. All 912 quoted fragments are accounted for, and none was not found. Every Stage 2 quote is verbatim at its stated location, and the translations are faithful. All value sets, ranges, bands, code labels, reference levels, offsets and thresholds match their sources. No source has a newer version that changes an element.
- **Scope.** The model has no input, storage or input-derivation content.
- **Mechanical checks.** All pass.
- **Remarks.** I found three issues that require a change. None was raised or declined before, and none reverses an earlier fix or crosses an oscillation watch point.
  1. **R32b-01.** The thresholds of the named responder criteria are tied to nothing. A label can name "NICE CG150 rec. 1.3.28" with a threshold that is not NICE's. INV-063 then forces the category that the false threshold gives, at every conformance level.
  2. **R32b-02.** Four facts that the context holds are tied at no level: the treatment of a responder label; a stop reason on a treatment that has not stopped; and the instrument of an instrument or screening result shown without its date. This is the defect class of R30-01 and R31-01. The fix-31 identity-tie sweep could not find these cases, because none of these ties was a conjunct of any SHOULD invariant.
  3. **R32b-03.** The intensity summaries compared between periods (INV-039, INV-069) need not share a scale. So a "comparison" can put a 0–10 mean next to a four-level distribution, which does not "allow comparison between periods" (OUT-010).

## Verification coverage

### Downloads and tools

- **Where.** Every source was downloaded with `curl` through the proxy into the fresh folder `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r32b/src`, outside the repository. Scripts are in `…/r32b/scripts`, outputs in `…/r32b/out`, and every script was run with `python3 -I`.
- **Extraction.**
  - PDFs: per-page `pdftotext` text, in both `-raw` and `-layout` mode.
  - Europe PMC full-text XML and HTML pages: stripped to text by `strip.py`.
  - The S-034 title page, an image without a text layer, was rendered with `pdftoppm` and read: "Клинические рекомендации Мигрень", "Возрастная группа дети", "Год утверждения 2024".
- **HTTP.** All requests returned HTTP 200. The only exception was S-034 (apicr.minzdrav.gov.ru): "Connection reset by peer" on the first attempt, then HTTP 200 on the retry (53 pages). No source was unreachable.
- **Quote matching (`quotes.py`).**
  - Fragments: every double-quoted string outside the `omn` blocks, split at "[...]", keeping fragments of at least 6 letters or digits.
  - Normalisation: NFKD, combining marks, soft hyphens and the ICHD-3 "þ" glyph removed, case folded, letters and digits only. This joins line-end hyphens and drops glyphs without a text mapping.
  - Search order: the source tagged nearest before the fragment on its line (PDFs page by page, and across adjacent pages); then Stage 1 v18; then every downloaded source.
  - Locations: a script compared the stated "p. N" of every Stage 2-only PDF quote with the pages on which it was found. All match; S-016's printed p. 1 is PDF p. 7, as Stage 1 states (PDF page = printed page + 6).
  - In context, by hand: Kutu 8 items 2 and 7 (S-035, PDF p. 48); sections 3.6.3.9 (p. 57) and 7.3, items 3–5 (p. 86); S-033 pp. 39 and 41; the S-034 flowchart (p. 52); AAN/AHS 14A, 14B and 14H (S-018, pp. 7–8); NICE 1.3.24–1.3.29 and 1.3.48; TA260 paragraph 2.1; the S-014 HALT table; the S-101 "Data sources" and S-102 "Migraine-related disability" sections; ICHD-3 pp. 122–125, 190 and 209.

### Quote check per source

| Source | Fragments attributed | Verbatim at stated location | Not found | Unreachable (tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (PDF, 211 pp.) | 76 | 71 in the PDF (49 Stage 2-only; pp. 8, 9, 12, 42, 105, 122–125, 139, 190, 209), and 1 in Stage 1 only. The other 4 are model or log phrases. One of them is a parsing artefact of line 1798, whose two A1.1 window quotes I verified separately on p. 190. | 0 | — |
| S-007 IHS cluster (UCL accepted manuscript) | 9 | 8 (the Stage 2 quote on p. 10, section 2.2); 1 Stage 1 | 0 | — |
| S-008 IHS 2024 (univaq PDF) | 27 | 19 (pp. 9, 12, 13, 17); 6 Stage 1; 2 artefacts, each found in the source its sentence names | 0 | — |
| S-010 IHS 2025 (univaq PDF) | 38 | 33 (p. 6); 5 Stage 1 | 0 | — |
| S-011 EHF 2022 (Europe PMC XML) | 22 | 13; 8 Stage 1; 1 artefact | 0 | — |
| S-012, S-013 (Europe PMC XML) | 1 + 4 | 1 + 3; 1 artefact | 0 | — |
| S-014 EHF/LTB aids (Europe PMC XML) | 37 | 31 (HALT paragraphs, "Scoring HALT", Table 18); 6 Stage 1 | 0 | — |
| S-015 NICE CG150 (Recommendations and Overview pages) | 42 | 35; 6 Stage 1; 1 artefact. "Last updated: 03 June 2025"; Overview "Last reviewed: 23 September 2026". | 0 | — |
| S-016 SIGN 155 (PDF, "Revised May 2026") | 9 | 7 (PDF p. 7 = printed p. 1); 1 Stage 1; 1 artefact | 0 | — |
| S-018 AAN/AHS clinician summary (PDF) | 13 | 10 (pp. 1, 7, 8); 2 Stage 1; 1 artefact | 0 | — |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML) | 6 | 5; 1 Stage 1 | 0 | — |
| S-028 NVN module (web page) | 13 | 10 (including the PICO under "Zoeken en selecteren"); 1 Stage 1; 1 translation; 1 artefact | 0 | — |
| S-033 Russian adults (official PDF, 92 pp.) | 47 | 21 (pp. 1, 4, 39, 40, 41); 12 Stage 1; 4 translations; 10 artefacts | 0 | — |
| S-034 Russian children (official PDF, 53 pp.) | 17 | 8 (pp. 17, 52); 3 Stage 1; 4 translations; 2 title-page fragments, read on the rendered p. 1 | 0 | first attempt reset, retry HTTP 200 |
| S-035 Turkish protocol (PDF, 92 pp.) | 50 | 33 (PDF pp. 7, 23, 48, 57, 77, 82, 83, 86); 1 Stage 1; 13 translations; 3 artefacts | 0 | — |
| S-101 HIT-6 (Europe PMC XML) | 4 | 4 (Methods > "Data sources") | 0 | — |
| S-102 MIDAS / AMPP (Europe PMC XML) | 9 | 6; 2 artefacts; 1 label of another paper, quoted in the search log | 0 | — |
| S-103 PedMIDAS page | 10 | 10 ("PedMIDAS Grading Scale") | 0 | — |
| S-104 HADS (Europe PMC XML) | 3 | 3 | 0 | — |
| S-105 PHQ/GAD-7 manual (PDF, 9 pp.) | 3 (+2 in section 10) | 5 (P. 6/9; the development sentence on P. 8/9) | 0 | — |
| S-106 NICE TA260 (chapters 1 and 2, overview) | 5 | 4 (paragraph 2.1, last sentence); 1 artefact. "Last reviewed: 11 January 2016". | 0 | — |
| Stage 1 sources reused only by their Stage 1 quotes (S-002, S-005, S-022, S-029, S-030, S-032, S-042) | 27 | 26 verbatim in Stage 1 v18; 1 artefact found in S-035 | 0 | not re-downloaded |
| Untagged fragments | 440 | 364 verbatim in Stage 1 v18; 19 found in a downloaded source | 0. The other 57 are model, search-log and change-log phrases. | — |

**Totals:** 912 fragments, none not found, no source unreachable.
- **Translations.** I read every translation of a Stage 2 quote against its original, and all are faithful: S-028 PICO; S-033 pp. 1, 39, 40, 41; S-034 pp. 1, 17, 52; S-035 pp. 7, 23, 48, 57, 77, 82, 83, 86.
- **Metadata.**
  - PubMed esummary confirms S-101 (PMID 20819842, Cephalalgia 2011;31(3):357–67, PMC3057423, DOI as cited), S-102 (PMID 25902814, PMC4406925), S-104 (PMID 12914662, PMC183845) and the PedMIDAS developer paper (PMID 11739822, Neurology 2001;57(11):2034–9).
  - S-105 PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
- **Versions.** A web search finds no published ICHD-4, only "International Classification of Headache Disorders-4 – Work in Progress 1" (2024; e.g. https://scientiasalut.gencat.cat/handle/11351/11121), so [S-001] is current. TA260 was last reviewed in 2016 and is still the guidance that CG150 1.3.26 cites.

### Values checked against sources

- **Codes and classes (E-009, E-028).** Code labels verbatim on pp. 8, 9 and 12. `classesOf826` matches 8.2.6 criterion B (p. 124), and `classesOf821to825` matches 8.2.6 note 2 (p. 125).
- **Overuse levels (E-032).** 15 days for 8.2.3; 10 days for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8; "more than three months" (pp. 122–125).
- **Evaluation rules (E-041).** All 18 rules match their sources in offset, anchor, timing, ages and `excludes`.
- **Thresholds (E-045, E-046).**
  - NICE 1.3.28: 50 % in episodic, 30 % in chronic migraine. NICE 1.3.29: 30 %.
  - IHS Q6: ≥ 50 %, and ≥ 30 % in the chronic alternative; MIDAS ≥ 5 points (baseline 11–20) or ≥ 30 % (baseline ≥ 20); HIT-6 ≥ 5 points.
  - DMKG/ÖKSG/SKG: 50 %, 5 points, 30 %. Russian 7.1: 50 %.
  - IHS 2025 control levels: 0; < 4 for three months; 4–6; > 6.
- **Instruments (E-057, E-059).**
  - HIT-6: 36–78, bands ≤ 49, 50–55, 56–59 and 60–78.
  - MIDAS: grades I–IV with the [S-102] labels, bands 0–5, 6–10, 11–20 and ≥ 21, three-month recall.
  - PedMIDAS: 0–10, 11–30, 31–50 and "Greater than 50".
  - HALT-90: Table 18 bands, including the overlap at 20. HALT-30: "Grading is not used by HALT-30".
  - HADS: 0–21 per subscale. PHQ-9: 0–27. GAD-7: 0–21.
- **Windows and remission (E-039, E-060, E-063).** The NICE 1.3.48 window, 4–8 weeks. The A1.1 window, day 1 ± 2 with no day 0. A cluster remission "must exceed three months".
- **Date examples recomputed.**
  - E-042 and INV-055: 26 March for NICE 1.3.28, with 26 February – 25 March as its 28 days. The interval ends of 28 February, 25 March and 31 March, and the verdicts for stops on 10 February, 30 March and 31 March.
  - The other examples: 41 days and 294 days (INV-079); 42 days and 143 days (E-063); 67 days (E-007); day 43 and 6 April (INV-049).

### Fidelity check per Stage 1 requirement

| OUT | Statement parts and Caveats checked | Result |
|---|---|---|
| 001 | Every view states its period (start, end, length) at MUST; frequency outputs per calendar month or 28-day period; equal-length comparisons; Caveat (lengths shown) | OK |
| 002–007 | Definition labels (SHOULD) for every form of report; ICHD-3 for headache days (MUST) and attacks (SHOULD); MUST, MUST, SHOULD and SHOULD availability, with the OUT-001 MUST where provided | OK |
| 008, 009 | MAY measures; time series with start, dose-change and stop markers in the view; weekly values where relevant | OK |
| 010 | Per period on a stated scale (INV-018). Comparison between periods (INV-039) admits incomparable scales. | **R32b-03** |
| 011–013 | Duration, its treated-attack label and the Caveat (SHOULD NOT); symptoms and most bothersome symptom across periods and per treated attack; aura (MAY) | OK |
| 014–017 | Total, class and drug days; weekly view; overuse indicator with code, level, span and basis, the prompt (MUST) and no diagnosis (MUST NOT); withdrawal follow-up, review window, following year, worsening label | OK |
| 018, 019 | Comparison per preventive treatment with values and both changes at MUST; time points by type and population; residual burden; Caveat (MUST NOT) | OK |
| 020 | Label names its criterion, with underlying and other values; not the sole indicator. The criterion's thresholds are not tied to its name, and the label's treatment is not tied to the subject. | **R32b-01, R32b-02 (a)** |
| 021 | MUST and SHOULD components for the same baseline and on-treatment periods. Intensity in the view has no common scale. | **R32b-03** (intensity part) |
| 022, 023 | Post-stop monitoring; acute outcomes, consistency, timing, formulation, phases, 15 minutes for cluster headache, Caveat (SHOULD NOT) | OK |
| 024 | History with dates, dose changes, duration, response, adverse effects, stop reason, formulation, grouping and order. A stop reason may be shown for a treatment that has not stopped. | **R32b-02 (b)** |
| 025, 039 | Scheme windows (MAY); adherence next to the comparison, in the history and in the clinician summary | OK |
| 026, 033 | Results with name, date, recall, score, grading and change; screening results with name, date and score. A result shown without its date is not tied to an available result. | **R32b-02 (c), (d)** |
| 027–032 | Functional impact and its comparison with the baseline period; three-month view (MUST, SHOULD, SHOULD NOT); per-type presentation; menstrual view (MUST); cluster view; trigger view with its caveats | OK |
| 034–038 | Clinician summary; patient overview; paediatric (a)–(d) and the Caveat; composite index (SHOULD NOT, SHOULD); interpretive caveats | OK |

The conformance levels match the strength of each Stage 1 statement part.
- MUST invariants: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054, 055, 056, 057, 059, 068, 086, 102 and 108.
- MUST NOT: INV-048 and INV-106.
- SHOULD NOT: INV-013, 021, 043, 065, 084, 091, 101 and 107.

### Mechanical checks (`mech.py`, `names.py`, inline scripts)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 115 invariants (INV-001 to INV-115), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12; ISS-07 is withdrawn (section 9). |
| References | No dangling E-, INV- or ISS- reference. Every OUT reference exists in Stage 1. 37 source IDs are used, all within S-001–S-046 or S-101–S-106. |
| Fields | Every element and every invariant has exactly one of each required field and at most one Notes field. |
| Traceability | 39 rows in Stage 1 order, all "full". The Elements and Invariants columns equal the sets of items whose Realises field names each requirement: 0 mismatches. |
| Levels and scope | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 38. Scopes: output 82, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. No repertoire or context invariant uses a bare `ctx`. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2). No violation, and no `set1` or `seq1` on a SHOULD or MAY attribute. MUST attributes occur only in MUST-available elements, or under a `when` clause tied to a MUST part (E-040, E-042). |
| Names | 559 declared names in the `omn` blocks, none declared twice. Every attribute selection resolves. The only unresolved tokens are `refs` (section 2.5), keywords and bound variables (`A`, `C`, `D`, `K`, `Ks`, `L`). |
| Uses of constants (for R32b-01) | `evaluationRules` is used in E-043, INV-055, INV-058 and INV-059, and `gradeBands` in INV-082. `namedCriteria` and the six `crit…` constants occur only in their own declaration, axiom and set (3 occurrences each). |
| Attributes per invariant (for R32b-02) | `ResponderLabel.treatment`: no invariant requires it to be one of the subject's preventive treatments. INV-114 ties it only to a comparison that is shown, and INV-064 only to a course event, and only for control-level labels. `TreatmentLine.stopReason`: only the E-055 `when` clause. `InstrumentResult.instrument` and `ScreeningResult.instrument`: tied to the context only through a shown date (INV-082, INV-085). |
| INV-063 transcription (`crit.py`, `out/crit.out`) | A label of a CGRP monoclonal antibody given for episodic migraine, with a 30 % fall in migraine days. Under `critNice1328`, INV-063 forces "non-responder". Under a criterion with the same name and a 30 % threshold, it forces "responder". |
| Scope sweep | I read in context every occurrence of enter, record, input, store, persist, database, serializ, encod, retention, reminder, answer, capture, algorithm, JSON, XML, CSV, FHIR, HL7 and data-entry in sections 1–10. Each is an exclusion statement, the notation's "records", the settled [S-014] HALT-30 sentence, the INV-076 remark on derivation from input, or "persistent" in an [S-007] quote. Every threshold and formula has output-element arguments only. Apart from the remarks below, every computed field that is part of the output data has its relation. |

## Remarks

### R32b-01 Formal defect: the thresholds of the named responder criteria are tied to no label that names them
- **Item(s):** E-045 (`critNice1328` … `critRu71`, `namedCriteria`), E-046 (`criterion`), INV-062, INV-063; traceability row OUT-020.
- **Problem.**
  - E-045 states the six named criteria with their thresholds, cited verbatim: NICE 1.3.28 and 1.3.29, IHS Q6, the IHS 2025 control levels, DMKG/ÖKSG/SKG and the Russian section 7.1. But these constants are used by no invariant.
  - `ResponderLabel.criterion` may be any `ResponderCriterion` value, so the `name` a label shows is unrelated to the components (thresholds and conditions) and the `alsoRestsOn` it shows. INV-063 decides the category from the components the label shows.
  - So the model admits, at every conformance level, a label that names a criterion of a source with a threshold that the source does not state. It then forces the category that this misstated threshold gives.
  - The model's other source value sets are tied where they are shown:
    - evaluation time points belong to `evaluationRules` (INV-058);
    - grade bands belong to `gradeBands` and to their instrument (INV-082);
    - an instrument outside the nine named ones cannot bear their names (`OtherInstrumentName`, E-057).

  For responder criteria the constants constrain nothing.
- **Evidence.**
  - **PROCESS.md section 2** names "a named responder criterion with its threshold (OUT-020)" as the first example of a threshold that is part of the output data: "When a cut-off, reference level or formula is part of the output data, the model states it in full."
  - **Stage 1 OUT-020:** "it SHOULD name the criterion applied (for example "NICE CG150 rec. 1.3.28", "IHS global practice recommendations Q6", "IHS position statement 2025 control levels")". A label that names NICE 1.3.28 but applies another threshold does not name the criterion it applies.
  - **[S-015], recommendation 1.3.28** (verified on https://www.nice.org.uk/guidance/cg150/chapter/Recommendations): "Stop CGRP inhibitors after 12 weeks of treatment if the frequency of migraines does not reduce by: at least 50% in episodic migraine; at least 30% in chronic migraine".
  - **Counter-example** (transcribed predicates; `crit.py`, `out/crit.out`):
    - Context: a CGRP monoclonal antibody, given for episodic migraine (`givenFor(c1)`, not `c1_3`), started on 1 January 2026.
    - Response comparison: baseline December 2025 with 10 migraine days; March 2026 with 7 (−30 %).
    - Label 1, evaluated ⟨March 2026⟩, with `criterion = critNice1328`. INV-063 forces "non-responder": the episodic component is decided and not met, and the chronic component is decided by its condition.
    - Label 2, the same label with `criterion = ResponderCriterion(name ↦ "NICE CG150 rec. 1.3.28", components ↦ {reductionFromBaseline(ReductionComponent(measures ↦ {migraineDays}, atLeastPercent ↦ 30, condition ↦ anySubject))}, alsoRestsOn ↦ ∅)`. It meets INV-062, INV-063, INV-065, INV-100, INV-106 and INV-114 with category "responder", and INV-063 even forces "responder".
    - So the reader is shown "responder under NICE CG150 rec. 1.3.28 (≥ 30 %)", a NICE threshold that [S-015] does not state.
  - **The same holds for every named criterion.** For example, a criterion named "IHS position statement 2025 control levels" whose components are a reduction threshold, not `controlLevels`, then decides a responder or non-responder label (INV-063, first conjunct).
  - **Not raised before in this form.** Reviews 08, 08b and 17 noted that `namedCriteria` is unused only in order to confirm that a label may name criteria outside the list, which this remark keeps. No review or fix considered the tie between a criterion's name and its thresholds.
- **Required change.**
  - **Option (a), preferred.** Tie every criterion shown under the name of a named criterion to that criterion, in a definitional invariant of E-045/E-046:

    `∀ L : ResponderLabel; K ∈ L.criterion; n ∈ namedCriteria • K.name = n.name ⇒ K = n`

    This is definitional because it states which criterion the label shows, as INV-058 and INV-082 do for rules and bands. A criterion whose name is that of a cited source but whose thresholds are not that source's contradicts the source wherever it is shown (section 3.3, item 5). It makes nothing more required: labels stay optional (MAY), and labels under other criteria stay open, as OUT-020's "for example" requires.
  - **Option (b).** State the same restriction as for instruments: a label's criterion is either a member of `namedCriteria`, or a value whose name is none of theirs. State it outside the `where` clause of `ResponderCriterion`, because the constants are values of that type.
  - **Either way:**
    - say in the E-045 Meaning and Notes, and in the E-046 Conformance and Notes, that the thresholds of the named criteria are those a label shows under their names;
    - list the new invariant in E-045/E-046 Notes ("Relations") and in the OUT-020 traceability row.
  - **Satisfiability.** The constants satisfy the `where` clause of `ResponderCriterion` (the score components of `critIhsQ6` and `critDmkg` list their instruments in `alsoRestsOn`), and every label that v31 admits under an exact named criterion is unchanged.

### R32b-02 Formal defect: four facts that the context holds are tied to the output at no level (the R30-01 / R31-01 class)
- **Item(s):** E-046 (`treatment`) and INV-114; E-055 (`stopReason`) and INV-079; E-058 (`instrument`) and INV-082; E-059 (`instrument`) and INV-085.
- **Problem.**
  - Fix 30 tied a treatment line's duration to the course "whatever dates the line shows". Fix 31 moved to definitional invariants the conjuncts of SHOULD invariants that state what an element is: "A SHOULD-level statement of them lets a MUST-conformant output [...] state an event, a withdrawal, a treatment or a period that is false" (fix-iter-31.md, R31-01).
  - The fix-31 sweep classified the conjuncts of the SHOULD invariants only. The four ties below are conjuncts of no invariant at any level, so the sweep could not find them. Each lets an output state a fact about the subject that the context contradicts, at every conformance level.
  - **(a) The treatment of a responder label.**
    - E-046 describes a label that "classifies the response to a preventive treatment", and `treatment` is `core`.
    - No invariant requires `L.treatment ∈ ctx.subject.preventiveTreatments`:
      - INV-114 ties `L.treatment` only to a response comparison that the label shows, and showing one is SHOULD (INV-062);
      - INV-064 requires a course event of the treatment only for control-level labels, and that course event may be an acute treatment's.
    - Every other element with a `treatment` attribute is tied:
      - INV-036 (markers), INV-056 (response comparison, MUST), INV-058 (time points), INV-067 (adherence), INV-068 (treatment review, MUST), INV-079 (treatment lines) and INV-112 (post-stop monitoring).
  - **(b) A stop reason on a treatment that has not stopped.**
    - E-055 declares `stopReason : opt StopReason SHOULD when stopped(ctx, self.treatment)`. The `when` clause states only when the reason is asked for.
    - INV-079 ties the stop date to the course (`∀ e ∈ l.stopDate • ∃ k : StopKind • eventOn(ctx, l.treatment, stop(k), e)`), but no invariant ties the stop reason to a stop.
    - So the line of an ongoing treatment may show "reason for stopping: lack of efficacy" without a stop date.
  - **(c) An instrument result without its date.**
    - INV-082 ties a result to an available result only through a date that it shows: `(∀ d ∈ r.completionDate • InstrumentAdministration(instrument ↦ r.instrument, date ↦ d) ∈ ctx.subject.instrumentAdministrations)`. `completionDate` is SHOULD.
    - So a result of, for example, MIDAS shown without its date is admitted for a subject with no available MIDAS result.
  - **(d) A screening result without its date.** The same holds for `ScreeningResult` (INV-085, last conjunct; `date` SHOULD).
- **Evidence.**
  - **Mechanical scan** (inline script in my verification; see the "Attributes per invariant" row). The only constraints on these attributes are the ones quoted above.
  - **Counter-examples.** Context: an adult with migraine; a preventive treatment t started on 1 January 2026, not stopped; an acute treatment course u of sumatriptan; no instrument or screening result available; as of 21 October 2026.
    - (a) A "responder" label with `treatment = u` (or a treatment that is not in the context), evaluated ⟨March 2026⟩, criterion `critIhsQ6`, and no comparison. INV-114 is vacuous, and INV-063 forces nothing: no reduction component is decided without a comparison, and Q6 has a judgement component. Only INV-062 (SHOULD) fails, so the output is MUST-conformant.
    - (b) A treatment line of t with `stopReason = {lackOfEfficacy}` and no stop date. INV-079 and INV-109 hold, so the line is admitted at every level.
    - (c) A MIDAS result with total score 14 and no date. Every INV-082 conjunct holds.
    - (d) A HADS result with subscale scores 9 and 11 and no date. Every INV-085 conjunct holds.
  - **Section 3.3, item 5:** an invariant that states "the structure of an element" or "a bound that follows from an element's definition" "holds wherever the element is shown".
  - **Stage 1.**
    - OUT-020 concerns labels of the response to the preventive treatment of OUT-018 ("the underlying values (OUT-018, OUT-019)"; OUT-018: "For each preventive treatment").
    - OUT-024 lists "the reason for stopping" of a treatment "with start and stop dates".
    - OUT-026 and OUT-033 report results "Where results of validated instruments are available" and "Where results of depression or anxiety screening instruments [...] are available".
  - **Not a reversal.** The oscillation watch points on responder labels (iteration 12, point 2; iteration 16, point 4), on the treatment line (iteration 28, point 4) and on the instruments list no such tie. Each change below only adds a conjunct, and it changes no level, `when` clause or date.
- **Required change.** Add these definitional conjuncts:
  - (a) `∀ L : ResponderLabel • L.treatment ∈ ctx.subject.preventiveTreatments`, for example in INV-114;
  - (b) `∀ l : TreatmentLine • l.stopReason ≠ ∅ ⇒ stopped(ctx, l.treatment)`, in INV-079;
  - (c) `∀ r : InstrumentResult • ∃ a ∈ ctx.subject.instrumentAdministrations • a.instrument = r.instrument`, in INV-082;
  - (d) `∀ r : ScreeningResult • ∃ a ∈ ctx.subject.screeningAdministrations • a.instrument = r.instrument`, in INV-085.

  Update the Readings, the Relations notes of E-046, E-055, E-058 and E-059, and the coverage reasons of rows OUT-020, OUT-024, OUT-026 and OUT-033.
- **Satisfiability.** Each conjunct holds for every element that the model asks for:
  - INV-062 shows the comparison of a preventive treatment (INV-056, INV-114);
  - INV-077 and INV-079 build lines from the context, and a stop reason is asked for only when the treatment has stopped;
  - INV-062, INV-069, INV-081, INV-096 and INV-104 ask only for results of available administrations, and INV-083 only for available screening results.

  Labels stay optional, and nothing becomes more required.

### R32b-03 Coverage gap: intensity "compared between periods" need not be on one scale
- **Item(s):** INV-039 (OUT-010) and INV-069 (OUT-021); E-023 (Conformance, Notes); traceability rows OUT-010 and OUT-021.
- **Problem.**
  - **INV-039** requires, for each selected period, an intensity summary with a scale (`m.scale ≠ ∅`). It does not require the compared periods to share a scale.
  - **INV-069** requires an intensity summary for the baseline and each on-treatment period of the treatment review view, also with no common scale.
  - No invariant relates the scales, or the summary forms, of the summaries that one comparison shows. So both predicates are met by a comparison that shows, for example, a mean peak intensity of 6.0 on a 0–10 numerical scale for the baseline period and a distribution of headache days over a four-level verbal scale (none, mild, moderate, severe) for the compared period. That output does not allow intensity to be compared between the periods.
  - This is a realistic output, for example for a diary that changed its intensity scale between the baseline and the treatment period.
  - The model takes care of commensurability for day counts: INV-053 compares one measure and type scope, and INV-111 states one definition per measure in a view, because "different definitions give different numbers" (OUT-002). It has no counterpart for intensity.
- **Evidence.**
  - **Stage 1 OUT-010 Statement:** "The diary output SHOULD summarise headache intensity per reporting period [...], on a stated scale, and allow comparison between periods."
  - **Its Evidence basis:** "the element "on a stated scale" is supported only indirectly, because a change in intensity between periods (for example the halving of intensity in [S-030]) can only be read when the scale is known". A halving can be read only on one scale.
  - **Stage 1 OUT-021:** "present together, for the same pre-treatment baseline and on-treatment periods, [...] intensity (OUT-010) [...]. The purpose is that efficacy can be judged across these dimensions".
  - **The model's own wording:**
    - the INV-039 Reading: "Intensity summaries over all headache types combined, with their scale, can be compared between selected periods";
    - the OUT-010 row: "comparison between periods over all headache types combined, as per period".
  - **Not raised before.** Every earlier review lists OUT-010 as "intensity on a stated scale and compared between periods". None examined whether the compared summaries share a scale (searched reviews and fixes for "same scale", "different scales" and scale near "compar").
- **Required change.**
  - **INV-039:** inside the existential, at SHOULD (the level of OUT-010), require the intensity summaries of the compared periods to be on one scale:

    `∀ m₁, m₂ ∈ pc.values ∩ IntensitySummary • m₁.scale = m₂.scale`

    Preferably, also require one summary form: both distributions, both means, or both of another form, so that the change can be read directly.
  - **INV-069:** the same, for the intensity summaries of the baseline and on-treatment periods over all headache types combined (SHOULD, OUT-021).
  - **Text:** update the E-023 Conformance and Notes, the INV-039 and INV-069 Readings, and rows OUT-010 and OUT-021.
  - **Further check.** The fixer should check, for the same reason, the other places where the model shows intensity for several periods so that change can be followed: the series of INV-018, and the time course of the patient-facing overview (INV-105).
  - **Satisfiability.** The constraint holds wherever the diary shows the compared periods on one scale. A diary that cannot do so deviates from a SHOULD for a reason in particular circumstances (section 3.1).

## Checked and not raised

- **INV-060 with INV-061 for compared periods shorter than a month.** OUT-019's "per month that remain on treatment" next to "Wherever the output shows a relative (percentage) change" could also be read as a Stage 1 issue for section 8. Fix 02 (item 14) declined the point with a justification, and later reviews kept it. I have no new evidence against that justification, only a different reading of the same Stage 1 text. Not raised.
- **Composite index over all types for subjects with migraine and another type** (`concerns`, INV-091 to INV-093). Settled in reviews 01, 19b, 21 and 25b; no new evidence.
- **The "baseline administration" of OUT-026** read as any earlier administration (settled since review 01), and the baseline month of a response comparison not adjacent to the start (review 02). No new evidence.
- **Rules anchored at the tolerated or target dose** (AAN/AHS 14A, 14B, SIGN titrated, IHS Q2 oral). They apply only where the context states a `targetDoseReached` event. This is consistent with the model's rule that content is aligned only to dates the context states. Not a defect.
- **Associated-symptom presence in different forms across the periods of the treatment review view** (INV-069; `daysWithSymptom` against `attacksWithSymptom`). This is related to R32b-03. But Stage 1 fixes no form of "presence", and OUT-012 asks for no comparison of it, so the basis is weaker than for intensity. Not raised; the fixer may consider it under R32b-03.
- **`isWeekSpan` "under the week convention of the output"** is used in the context invariant INV-001. It is one given total function, so the convention is the diary's. No effect on any verdict.
- **Cycle lines in the patient-facing overview** carry the MUST attributes of E-060. These are the derived content of a cycle line (its day 1, window and next-window days), not a level raised above OUT-035.
- **A responder label of a treatment whose start is not stated** cannot show its comparison. This is the deviation Stage 1 describes (review 32). R32b-02 (a) does not change it.
- **Watch points.** None of the three remarks reverses an earlier fix or touches a watch-point item (oscillation checks after iterations 12, 16, 24 and 28). R32b-01 keeps the open criterion list, R32b-02 adds ties in the direction of fixes 30 and 31, and R32b-03 adds a co-presence condition at SHOULD.
- **Section 8.**
  - ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded, and their quotes are verbatim at the stated locations:
    - "simple analgesics" occurs once in ICHD-3, on p. 139;
    - "ibuprofen or other NSAIDS" is on p. 105;
    - the 3.1.1 and 3.1.2 passages are on p. 42;
    - NICE 1.3.9 and 1.3.39 read as quoted.
  - The descriptions of the Stage 1 passages are accurate (ISS-03's list of statements, ISS-04, ISS-09's settled Group D description, ISS-12's account of the OUT-031 Evidence note).
  - No Stage 1 issue is worked around silently, apart from the settled INV-060/INV-061 point above.
- **Citation metadata.**
  - S-102: "Pavlovic JM" for PubMed "Pavlović JM", as review 32 noted. The identifiers are unambiguous; not a defect.
  - SIGN 155: the PDF's internal title metadata reads "2023 update", while the cover page reads "Revised May 2026". That is Stage 1 metadata, and the cover matches Stage 1.

## Notes on frozen items (for the human)

None.
