# Review — iteration 33
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v32
Date: 2026-10-22

## Summary

This is the main review of iteration 33. I checked v32 against its sources, Stage 1 v18 and the model itself. All results below come from my own downloads, scripts and reading.

**State of the files.**
- `OUTPUT_MODEL.md` is v32 and byte-identical to `history/v32.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a FROZEN marker.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18: sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5.
- v32: sections 1–10 (all 67 elements and 117 invariants, the traceability table, ISS-01 to ISS-12, the Sources table), and the iteration-31 and iteration-32 entries of sections 11 and 12.
- Loop files: the oscillation check after iteration 32, including its watch points; re-check 32b; fix 32. I searched all reviews, fixes and oscillation reports for each point I considered raising (see "Checked and not raised").

**Result.**
- **Citations and values.** Every Stage 2 quote is verbatim at its stated location, and every translation is faithful. All value sets, ranges, bands, codes, reference levels, offsets and thresholds match their sources. Every source was reachable. No source has a newer version that changes an element.
- **Scope.** The model contains no input, storage or input-derivation content.
- **Mechanical checks.** All pass.
- **Remarks.** I found two issues that require a change. Neither was raised or declined before, and neither reverses an earlier fix or crosses an oscillation watch point.
  1. **R33-01.** `onSameScale` (E-023) and `inSameForm` (E-025) treat every "other" summary as one form. A comparison can therefore show a median peak intensity for one period and a share of severe days for another, and INV-039, INV-069 and INV-105 still hold. The R32b-03 gap stays open for every form outside the two named ones, although the model's text says these predicates ensure "one form".
  2. **R33-02.** E-057 fixes `¬ publishedGrading(halt30)`, because [S-014] says "Grading is not used by HALT-30". Yet INV-082 lets a HALT-30 result show a `publishedCategory`, for example the HALT-90 label "Moderate". `publishedGrading` is used only in a `when` clause, so this fact of the value set constrains nothing.

## Verification coverage

### Downloads and tools

- **Where.** Every source was downloaded with `curl`, through the proxy, into the fresh folder `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r33/dl`, outside the repository.
  - Scripts are in `…/r33/scripts`, and extracted text is in `…/r33/txt`. Every script was run with `python3 -I`.
- **Extraction.**
  - PDFs: per-page `pdftotext` text, in both `-raw` and `-layout` mode.
  - Europe PMC full-text XML and HTML pages: stripped to text by `strip.py`.
  - The S-034 title page is an image without a text layer. I rendered it with `pdftoppm` and read "Клинические рекомендации Мигрень", "Возрастная группа дети" and "Год утверждения 2024".
- **HTTP.** All requests returned HTTP 200. The one exception was S-033 (apicr.minzdrav.gov.ru): "Connection reset by peer" on the first attempt, then HTTP 200 on the retry (92 pages).
- **Quote matching** (`extract.py`, `verify.py`, `strict.py`, `loc.py`).
  - **Extraction.** Every double-quoted string in sections 1–9 outside the `omn` blocks: 799 strings. Each was attributed to the nearest preceding source tag on its line and split at "[...]". 790 fragments have at least 6 letters or digits.
  - **Letters-only matching.** Text was normalised to NFKD, with combining marks, soft hyphens and the ICHD-3 "þ" glyph removed, case folded, and only letters and digits kept. The search order was: the tagged source, page by page (and across adjacent pages); then Stage 1 v18; then every downloaded source.
  - **Punctuation-preserving pass.** Each match was mapped back to its source span and compared with punctuation kept. All 53 differences were reviewed by hand. They are:
    - line-end hyphens ("def-inition", "con-sidered");
    - the ICHD-3 glyphs without a text mapping ("≥", "±", "−"), which the model notes at each quote;
    - heading case where the location names a heading;
    - one PDF spacing ("a≥30%" for "a ≥ 30%" in [S-008] p. 12).

    None alters wording, numbers or meaning. I read the [S-008] Q2 asterisks ("effectiveness*") and the [S-035] heading "3. MİGREN BAŞ AĞRISI TEDAVİSİ" on their stated pages (p. 9; PDF pp. 22–30).
  - **Locations.** A script compared every stated "p. N" with the pages on which the fragment was found. Every one matches, except [S-016] "p. 1" = PDF p. 7, which follows the Stage 1 offset (PDF page = printed page + 6).
  - **Section 10.** I checked the quotes in the Sources table by hand: the [S-105] development sentence (P. 8/9) and the [S-015] sentence of 1.3.26 that names TA260.

### Quote check per source

| Source | Fragments attributed | Verified verbatim at stated location | Not found | Unreachable (what I tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (PDF, 211 pp.) | 68 | 67 in the PDF (pp. 8, 9, 12, 42, 105, 122–125, 139, 190, 209); 1 in Stage 1 | 0 | — |
| S-007 IHS cluster (UCL accepted manuscript) | 6 | 5 (pp. 10, 22, 25); 1 Stage 1 | 0 | — |
| S-008 IHS 2024 (univaq PDF) | 18 | 14 (pp. 9, 12, 13, 17); 4 Stage 1 | 0 | — |
| S-010 IHS 2025 (univaq PDF) | 34 | 29 (p. 6, including the sentence interrupted by "Cephalalgia 45(2)"); 5 Stage 1 | 0 | — |
| S-011 EHF 2022 (Europe PMC XML) | 19 | 10; 8 Stage 1; 1 found in [S-008], the source its sentence names | 0 | — |
| S-012, S-013 (Europe PMC XML) | 1 + 3 | 1 + 2; 1 found in [S-015], the source its sentence names | 0 | — |
| S-014 EHF/LTB aids (Europe PMC XML) | 33 | 27 (HALT paragraphs, "Scoring HALT", Table 18); 6 Stage 1 | 0 | — |
| S-015 NICE CG150 (Recommendations and Overview pages) | 33 | 26; 6 Stage 1; 1 found in [S-008]. Pages read "Last updated: 03 June 2025" and, on the Overview, "Last reviewed: 23 September 2026". | 0 | — |
| S-016 SIGN 155 (PDF) | 8 | 6 (PDF pp. 7, 20); 1 Stage 1; 1 found in [S-008] | 0 | — |
| S-018 AAN/AHS clinician summary (PDF) | 11 | 8 (pp. 1, 7, 8); 2 Stage 1; 1 found in [S-033] | 0 | — |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML) | 5 | 4; 1 Stage 1 | 0 | — |
| S-028 NVN module (web page) | 8 + 1 translation | 6 (including the PICO under "Zoeken en selecteren"); 1 Stage 1; 1 found in [S-035] | 0 | — |
| S-033 Russian adults (official PDF, 92 pp.) | 42 + 4 translations | 19 (pp. 1, 4, 39, 40, 41); 13 Stage 1; 10 found in the other sources that their sentences name (E-041 Notes) | 0 | first attempt reset, retry HTTP 200 |
| S-034 Russian children (official PDF, 53 pp.) | 12 + 4 translations | 8 (pp. 17, 52); 3 Stage 1; 1 on the rendered title page (image, p. 1) | 0 | — |
| S-035 Turkish protocol (PDF, 92 pp.) | 31 + 13 translations | 27 (PDF pp. 6–7, 22–23, 48, 57, 77, 82, 83, 86); 1 Stage 1; 3 found in [S-008] or [S-011], the sources their sentences name | 0 | — |
| S-101 HIT-6 (Europe PMC XML) | 4 | 4 (Methods, "Data sources") | 0 | — |
| S-102 MIDAS / AMPP (Europe PMC XML) | 5 | 4 ("Headache impact on functioning" > "Migraine-related disability"); 1 found in [S-014] | 0 | — |
| S-103 PedMIDAS page | 10 | 10 ("PedMIDAS Grading Scale"); page footer © 2026 | 0 | — |
| S-104 HADS (Europe PMC XML) | 3 | 3 | 0 | — |
| S-105 PHQ/GAD-7 manual (PDF, 9 pp.) | 3 + 1 (section 10) | 4 (P. 6/9; the development sentence on P. 8/9) | 0 | — |
| S-106 NICE TA260 (chapter 2, Overview) | 3 | 2 (paragraph 2.1, last sentence); 1 found in [S-035]. Overview reads "Last reviewed: 11 January 2016". | 0 | — |
| Stage 1 sources reused only through their Stage 1 quotes (S-002, S-005, S-022, S-030, S-032, S-042) | 18 | 17 verbatim in Stage 1 v18; 1 found in [S-035] | 0 | not re-downloaded |
| Untagged strings | 390 | 360 verbatim in Stage 1 v18; 12 found in a downloaded source. The other 18 are model phrases ("definitional", "the subject has migraine", "in the same view"). | 0 | — |

**Totals:** 790 fragments (799 quoted strings, 22 of them translations). 285 were verified in the tagged source at the stated location, 430 in Stage 1 v18 and 34 in the source that the sentence names. 18 are model phrases, and 1 is the S-034 title page, verified on the rendered image. None was not found, and no source was unreachable.

- **Translations.** I read every translation of a Stage 2 quote against its original, and all are faithful:
  - S-028: the PICO;
  - S-033: pp. 1, 39, 40, 41;
  - S-034: pp. 1, 17, 52;
  - S-035: PDF pp. 7, 23, 48, 57, 77, 82, 83, 86.
- **Metadata.**
  - PubMed esummary confirms:
    - S-101: Cephalalgia 2011;31(3):357–67, PMID 20819842, PMC3057423, DOI 10.1177/0333102410379890;
    - S-102: J Headache Pain 2015;16:24, PMID 25902814, PMC4406925;
    - S-104: Health Qual Life Outcomes 2003;1:29, PMID 12914662, PMC183845;
    - the PedMIDAS developer paper: Neurology 2001;57(11):2034–9, PMID 11739822.
  - S-105 PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
  - S-106: published 27 June 2012, last reviewed 11 January 2016.
- **Versions.** A web search finds no published ICHD-4, only "International Classification of Headache Disorders-4 – Work in Progress 1" (Cephalalgia 2024; https://scientiasalut.gencat.cat/handle/11351/11121), so [S-001] is current.
  - NICE CG150 1.3.24 and 1.3.25 now name atogepant and rimegepant as CGRP inhibitors. This changes no element: `ruleNice1328` applies to `cgrpInhibitor` in adults, and the 1.3.24 quote in E-041 is verbatim.
  - TA260 is still the guidance that CG150 1.3.26 names.

### Values checked against sources

- **Codes and classes (E-009, E-028).**
  - The code labels are verbatim on pp. 8, 9 and 12.
  - `classesOf826` matches 8.2.6 criterion B (p. 124), and `classesOf821to825` matches 8.2.6 note 2 (p. 125).
  - "simple analgesics" occurs once in the text layer, on p. 139 (ISS-02); "ibuprofen or other NSAIDS" is on p. 105.
- **Overuse levels and span (E-032, INV-045).**
  - The levels are 15 days for 8.2.3, and 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8, over "more than three months" (pp. 122–125).
  - With calendar months or 28-day periods, the span INV-045 defines has 4 periods. I recomputed this, including the minimality conjunct.
- **Evaluation rules (E-041).** I read all 18 rules against their quotes, for offset, anchor, timing, ages and `excludes`.
  - The NICE 1.3.27–1.3.29 and 1.3.48 texts are on the Recommendations page.
  - AAN/AHS 14A, 14B and 14H are on pp. 7–8, SIGN section 1.2.1 on PDF p. 7, and IHS Q2 and Q13 on pp. 9 and 17.
  - The Russian adult p. 39, 40 and 41 passages and the paediatric flowchart (p. 52) are verbatim.
  - The Turkish passages are verbatim: Kutu 8 (PDF p. 48), section 3.6.3.9 (p. 57), section 7.1 (p. 83) and section 7.3 (p. 86).
  - TA260 2.1: "every 12 weeks".
- **Named criteria (E-045).**
  - NICE 1.3.28: 50 % in episodic and 30 % in chronic migraine. NICE 1.3.29: 30 %.
  - IHS Q6: ≥ 50 %, with the 30 % chronic alternative; MIDAS ≥ 5 points for a baseline of 11–20, or ≥ 30 % for a baseline of ≥ 20; HIT-6 ≥ 5 points.
  - DMKG/ÖKSG/SKG: 50 %, 5 points and 30 %. Russian section 7.1: 50 %.
- **Control levels (E-046, INV-064).** The four [S-010] definitions (p. 6) are verbatim, including the "less than six MMDs" sentence.
- **Instruments (E-057, E-059).**
  - HIT-6: 36–78, with bands ≤ 49, 50–55, 56–59 and 60–78 [S-101].
  - MIDAS: grades I–IV with the [S-102] labels, bands 0–5, 6–10, 11–20 and ≥ 21, and a three-month recall.
  - PedMIDAS: 0–10, 11–30, 31–50 and "Greater than 50" [S-103].
  - HALT-90: the Table 18 bands, including the overlap at 20. HALT-30: "Grading is not used by HALT-30" [S-014].
  - HADS: 0–21 per subscale [S-104]. PHQ-9: 0–27. GAD-7: 0–21 [S-105].
- **Windows and remission (E-039, E-060, E-063).** The NICE 1.3.48 window is 4–8 weeks. The A1.1 window is day 1 ± 2, with no day 0 (p. 190). A cluster remission "must exceed three months" (p. 209).
- **Date examples recomputed.**
  - 67 days (E-007); 41 and 294 days (INV-079); 42 and 143 days (E-063).
  - Day 43 and 6 April (INV-049).
  - The INV-055 / E-042 examples: 26 March for NICE 1.3.28, interval ends of 28 February, 25 March and 31 March, and the verdicts for stops on 10 February, 30 March and 31 March.
  - NICE 1.3.29's 24 weeks lie within the 1.3.27 window.

### Fidelity check per Stage 1 requirement

| OUT | Statement parts and Caveats checked | Result |
|---|---|---|
| 001 | Every view states its period (start, end, length) at MUST; frequency outputs per calendar month or 28-day period at MUST where provided; equal-length comparisons; Caveat (lengths visible) | OK |
| 002 | Definition label for every form of report (SHOULD); one definition per measure in a view | OK |
| 003 | Indicator next to every reporting period of a summary measure (SHOULD); no validated cut-off (SHOULD NOT); Caveat | OK |
| 004–007 | Availability: headache days (MUST); migraine days for patients with migraine (MUST, with the label at SHOULD); moderate/severe days and attacks (SHOULD, with MUST per month where provided); ICHD-3 definitions; attacks separate from days | OK |
| 008, 009 | MAY measures; time series with start, dose-change and stop markers in the view; weekly values where relevant | OK |
| 010 | Per period on a stated scale; comparison between periods (INV-039). Two summaries in different "other" forms count as one form. | **R33-01** |
| 011–013 | Duration and its treated-attack label; the Caveat as SHOULD NOT; symptoms and most bothersome symptom across periods and per treated attack; aura (MAY) | OK |
| 014–017 | Total, class and drug days; weekly view; overuse indicator with code, level, span and basis; the prompt (MUST); no diagnosis (MUST NOT); withdrawal follow-up with the review window, the following year and the worsening label | OK |
| 018, 019 | Comparison per preventive treatment, with values and both changes at MUST; time points by type and population; residual burden; the Caveat as MUST NOT | OK |
| 020 | Label names its criterion, a named criterion's thresholds tied by INV-116; underlying and other values; not the sole indicator; label's treatment preventive (INV-117) | OK |
| 021 | MUST components for the same baseline and on-treatment periods; SHOULD components where provided. The intensity and symptom forms carry the gap of R33-01. | **R33-01** (form part) |
| 022, 023 | Post-stop monitoring; acute outcomes, consistency, timing, formulation, phases, 15 minutes for cluster headache; the Caveat as SHOULD NOT | OK |
| 024, 025, 039 | History with dates, dose changes, duration, response, adverse effects, stop reason (only after a stop), formulation, grouping and order; scheme windows (MAY); adherence next to the comparison, in the history and in the clinician summary | OK |
| 026 | Results where available, with name, date, recall, score, the instrument's own published grading or categories, and change. A HALT-30 result may show a category that the source says does not exist. | **R33-02** |
| 027–034 | Functional impact and its comparison (one domain for severe impairment); three-month view (MUST, SHOULD, SHOULD NOT); per-type presentation; menstrual view (MUST); cluster view; trigger view with its caveats; screening results; clinician summary | OK |
| 035 | Overview, with the intensity of its time course on one scale and in one form. The "other" form part of R33-01 applies. | **R33-01** (form part) |
| 036–038 | Paediatric (a)–(d) and the Caveat; composite index (SHOULD NOT, SHOULD); interpretive caveats | OK |

The conformance levels match the strength of each Stage 1 statement part.
- MUST: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054, 055, 056, 057, 059, 068, 086, 102 and 108.
- MUST NOT: INV-048 and INV-106.
- SHOULD NOT: INV-013, 021, 043, 065, 084, 091, 101 and 107.
- Every element attribute at MUST in a SHOULD or MAY element cites a MUST part (section 3.3, item 3).

### Mechanical checks (`mech.py`, `names.py`, `cex.py`)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 117 invariants (INV-001 to INV-117), none missing, none duplicated. Issues: ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn, section 9). |
| References | No dangling E-, INV- or ISS- reference. Every OUT reference exists in Stage 1. 37 source IDs are cited, all within S-001–S-046 or S-101–S-106. |
| Fields | Every element and every invariant has exactly one of each required field and at most one Notes field. ISS-04 gives its evidence in its "Stage 1" field (Stage 1 text only). |
| Traceability | 39 rows in Stage 1 order, all "full". The Elements and Invariants columns equal the sets of items whose Realises field names each requirement: 0 mismatches. |
| Levels and scope | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 40. Scopes: output 84, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. |
| Names | 538 declared names in the `omn` blocks (my count, by declaration), none declared twice. Every attribute selection resolves to a declared attribute. The remaining tokens are bound variables, keywords, words inside text literals, and the constants of the multi-line `AnnotationKind`, `IntensitySummaryValue` and `AcuteOutcomeMeasure` declarations, which I checked by reading. |
| Definedness | `days`, `first`, `last`, `s(i)`, `min`, `max`, `÷` and `classOf` are guarded where used (INV-045, INV-069, INV-079, INV-087, INV-089, E-032, E-046). |
| Prose against predicates (`cex.py`) | Transcribed: `onSameScale`, `inSameForm`, the INV-039 comparison part, the INV-032 constraints, and INV-082.<br>• `onSameScale` holds for two `otherIntensitySummary` values in different forms. INV-039's witness and INV-032 hold for them (R33-01).<br>• `inSameForm` holds for two `otherPresenceSummary` values in different forms (R33-01).<br>• The control behaves as the model intends: R32b-03's mean against distribution is rejected.<br>• INV-082 admits a HALT-30 result with `publishedCategory("Moderate")`, while it rejects the same result showing the HALT-90 band (R33-02). |
| Scope sweep | I read in context every occurrence of enter, record, input, store, persist, database, serializ, encod, retention, reminder, answer, capture, algorithm, JSON, XML, CSV, FHIR, HL7 and data-entry in sections 1–10. Each is an exclusion statement, the notation's "records", an [S-014] quote ("records days affected"), a statement that a derivation from answers is out of scope (E-057 Notes), or the INV-076 Note on derivation from input. Every threshold, formula and derived relation has output elements, constants or context properties as arguments. |

## Remarks

### R33-01 Formal defect: `onSameScale` and `inSameForm` count every "other" summary as one form, so compared summaries in two different forms are admitted
- **Item(s):**
  - E-023 (`onSameScale`, Meaning, Conformance, Notes) and E-025 (`inSameForm`, Meaning, Conformance, Notes);
  - INV-039, INV-069 and INV-105 (Readings and Notes);
  - traceability rows OUT-010, OUT-021 and OUT-035.
- **Problem.**
  - Fix 32 (R32b-03) introduced `onSameScale` so that "wherever the model asks for intensity for several periods in order to compare them, the summaries of these periods are on one scale and in one form" (E-023 Notes). The reason it gives: "A change in intensity between two periods can be read only where their summaries are on the same scale and in the same form". `inSameForm` was introduced for the same purpose for symptom presence (E-025 Notes: "a number of days and a number of attacks have different units and cannot be compared").
  - The predicates distinguish only the two named forms:
    - `onSameScale(i₁, i₂) ≙ i₁.scale = i₂.scale ∧ (i₁.summary is peakIntensityDistribution ⇔ i₂.summary is peakIntensityDistribution) ∧ (i₁.summary is meanPeakIntensity ⇔ i₂.summary is meanPeakIntensity)`;
    - `inSameForm` tests only `daysWithSymptom` and `attacksWithSymptom`.

    Every `otherIntensitySummary ⟨Text⟩` is therefore "in the same form" as every other one, and likewise every `otherPresenceSummary ⟨Text⟩`. The `Text` payload is the value as worded, so the model has no way to tell two other forms apart.
  - The forms are open by design: Stage 1 gives the two forms only "for example" (OUT-010), and E-023 keeps the list open with `otherIntensitySummary`. So the gap concerns every form outside the two named ones. Examples:
    - a median peak intensity;
    - the share of headache days with severe pain;
    - the mean intensity of all headache days;
    - for symptoms, the share of headache days against the share of attacks with the symptom. These are the same days-against-attacks difference that E-025 Notes reject.
  - So INV-039, INV-069 and INV-105 admit comparisons that do not allow intensity, or symptom presence, to be compared. Yet their Readings state the opposite:
    - INV-039: "the summaries of the compared periods being on one scale and in one form [...], so that a change between them can be read";
    - INV-069: "the summaries of each symptom in one form for all these periods";
    - INV-105: "with the intensity of the periods of the series on one scale and in one form".
- **Evidence.**
  - **Stage 1.**
    - OUT-010 Statement: "on a stated scale, and allow comparison between periods". Evidence basis: "a change in intensity between periods (for example the halving of intensity in [S-030]) can only be read when the scale is known".
    - OUT-021: "The purpose is that efficacy can be judged across these dimensions".
    - OUT-035: "over time [...] so that patients can follow the effect of their treatment".
  - **Counter-example** (`cex.py`, transcribed predicates). A comparison of January and March 2026, both on the 0–10 numerical rating scale:
    - January shows `otherIntensitySummary("median peak intensity 6")`;
    - March shows `otherIntensitySummary("severe pain on 30 % of headache days")`.

    `onSameScale` holds, INV-032 holds for both, and the witness of INV-039 holds. The same comparison shown as a mean against a distribution, R32b-03's example, is rejected. For symptoms, `inSameForm` holds for "nausea on 40 % of headache days" against "nausea in 3 of 5 attacks".
  - **Model text.** The E-023 comment and Meaning define the predicate as holding for "both of another form". That wording came from R32b-03's suggestion ("both distributions, both means, or both of another form"). Neither R32b-03 nor fix 32 considered two different other forms (I searched all reviews and fixes for `otherIntensitySummary`, `otherPresenceSummary` and "other form").
  - **Not a reversal.** Oscillation watch point 3 names as reversals only dropping these conjuncts or moving INV-027's `∃ sd` back inside `∀ p`. The change below tightens the v32 tie in its own direction. It does not touch INV-018, INV-029 or INV-062, which fix 32 declined with reasons.
- **Required change.**
  - **Option (a), preferred.** Let an "other" summary state its form, and compare forms:
    - for example `otherIntensitySummary ⟨OtherSummary⟩` with `value OtherSummary { form : Text; value : Text }`, where `form` is the kind of summary as the output names it, for example "median peak intensity";
    - add to `onSameScale`: `∀ x₁, x₂ : OtherSummary • i₁.summary = otherIntensitySummary(x₁) ∧ i₂.summary = otherIntensitySummary(x₂) ⇒ x₁.form = x₂.form`;
    - do the same for `otherPresenceSummary` and `inSameForm`.
  - **Option (b).** Any equivalent structure (for example a separate form attribute) that makes `onSameScale` and `inSameForm` hold only for summaries of the same form, including among other forms.
  - **Either way:**
    - replace "or both of another form" in the E-023 and E-025 comments and Meanings with "or both of the same other form";
    - align the Notes of E-023, E-025, INV-039 and INV-069 and the coverage reasons of rows OUT-010, OUT-021 and OUT-035.
  - **Satisfiability.** INV-032 and INV-033 place no constraint on other forms, and periods summarised alike in one named form or one other form meet the tightened predicates. So fix 32's witnesses remain valid, and nothing becomes more required.

### R33-02 Factual error (value set): INV-082 lets a HALT-30 result show a category, although the model fixes, from [S-014], that HALT-30 has no grading
- **Item(s):** E-057 (`publishedGrading`, Notes), E-058 (`category`, Conformance, Notes), INV-082 (Predicate, Reading); traceability row OUT-026.
- **Problem.**
  - E-057 states `axiom … ∧ ¬ publishedGrading(halt30)`, with the Stage 1 quote of [S-014] "Grading is not used by HALT-30". `publishedGrading` is used only in the `when` clause of `E-058.category`, so it decides only whether a category is asked for. No invariant forbids a category where `publishedGrading` is false.
  - INV-082 constrains categories in two ways:
    - for banded instruments, the category must be a band of the instrument that contains the score;
    - for every instrument, a `band(b)` must be a band of that instrument.

    A `publishedCategory(Text)` is therefore admitted for every unbanded instrument, HALT-30 included. A HALT-30 result can show "Moderate" or "Grade III", the HALT-90 labels, as its "published category" at every conformance level. INV-100 then even qualifies it as an indicator.
  - INV-082 forbids showing a HALT-90 band on a HALT-30 result ("never a band of another instrument"). The same false grading worded as `publishedCategory` passes.
  - The INV-082 Reading says that for every unbanded instrument the category shown is "a category as published". For HALT-30 no category is published, so the Reading claims more than the predicate guarantees.
- **Evidence.**
  - **Source.** [S-014] "Grading has value in indicating the level of a patient’s personal need and, perhaps, priority for treatment. But for assessment as a prelude to planning management, or for establishing the baseline impact, the individual summed scores are more informative than overall grades. Grading is not used by HALT-30." I verified it on the Europe PMC full text of PMC6734476, section "Scoring HALT", the paragraph after Table 18. It is quoted in Stage 1 OUT-026, whose Evidence basis reads "(HALT-30 uses no grading)".
  - **Stage 1 OUT-026.** "the instrument's own published grading or categories". A HALT-30 category is no published grading of HALT-30.
  - **Counter-example** (`cex.py`). A HALT-30 result with total score 12, recall `recallMonths(1)`, the date of an available administration, and `category = {publishedCategory("Moderate")}`:
    - every INV-082 conjunct holds, and E-058 places no constraint, because its `when` clause is false;
    - the same result showing the HALT-90 band "Moderate" (11–20) is rejected.
  - **Not raised before.** R19c-01 corrected the basis of HALT-30's lower bound. Fix 32's sweep listed `publishedGrading` as "used" by the E-058 `when` clause. No review or fix examined a category shown for an instrument without grading.
  - **Not a reversal.** The change adds a conjunct in the direction of INV-082's band ties. It touches no item of the oscillation watch points.
- **Required change.**
  - Add a definitional conjunct to INV-082: `(∀ cat ∈ r.category • publishedGrading(r.instrument))`. Its narrower variant would be `r.instrument = halt30 ⇒ r.category = ∅`.
  - Update:
    - the INV-082 Reading: no category for an instrument without a published grading, such as HALT-30;
    - the E-057 Notes sentence "INV-082 constrains the results of other instruments only by …", so that it names this tie;
    - the E-058 Conformance and Notes ("Relations");
    - the coverage reason of row OUT-026.
  - **Satisfiability.** E-058 asks for `category` only `when publishedGrading(self.instrument)`, and no invariant asks for a category elsewhere. So every result that an invariant asks for still meets INV-082, and nothing becomes more required.

## Checked and not raised

- **INV-116 compares names by exact text.** A criterion named "NICE CG150 1.3.28" (without "rec.") is not tied. The model identifies criteria, like instruments (`OtherInstrumentName`), by the name it states for them, and states that convention (E-045 Notes). This is a modelling convention, not a defect.
- **INV-116 against INV-063 and INV-062.** Omitting only condition-failed reduction, attack or score components changes no forced or admitted category and no value asked for. `set1` keeps the forced "non-responder" of a label whose components all fail their conditions (a settled point). Judgement and control-level components cannot be omitted.
- **INV-069 symptom anchor.** `a₁` is not required to be of symptom `s`. Because the summary of `s` for any period can serve as `a₁`, the predicate is equivalent to an anchor of symptom `s`. Not a defect.
- **INV-117 and the new conjuncts of INV-079, INV-082 and INV-085.** Each holds for every element that another invariant asks for, so nothing becomes unsatisfiable.
- **HALT-90 question 5.** [S-014] says this question's unit "is not whole days", but it is a "simple count" included in the graded total. So the total is still a whole number, and `wholeNumberScores` is correct.
- **NICE CG150 1.3.24 and 1.3.25 now name gepants.** No element changes (see Versions).
- **Control-level label over one month with 1–3 days.** INV-064 admits only "insufficient control" for it (or migraine freedom at 0). This is the settled point "the model does not require more than six days for that level", with optional labels. Not reopened.
- **Settled points, not reopened (no new evidence):**
  - INV-060 with INV-061 for compared periods shorter than a month;
  - INV-027 tied to preventive treatments;
  - E-063 `duration` and E-058 `changeFromBaseline` (fix 02 item 14);
  - INV-106 at MUST NOT;
  - the "> 3 months" readings of INV-045 and INV-089;
  - the MIDAS labels and the undivided Grade IV;
  - the HIT-6 one-month recall;
  - the HALT-90 overlap at 20;
  - "history of previous bouts";
  - empty `remissions` in chronic cluster headache (ISS-12);
  - the evaluated periods of a responder label (fix 18);
  - the formulation of an acute summary (fix 17);
  - INV-078 grouping and INV-035 at SHOULD;
  - adherence windows reaching past the stop.
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded, and their quotes are verbatim at the stated locations:
  - "simple analgesics" occurs only on p. 139;
  - the 3.1.1 and 3.1.2 passages are on p. 42;
  - the Definitions of terms are on p. 209;
  - A1.1 is on p. 190;
  - NICE 1.3.9 and 1.3.39 read as quoted.

  The descriptions of the Stage 1 passages are accurate. No Stage 1 issue is worked around silently.
- **Oscillation watch points.** Neither remark reverses an earlier fix or touches a frozen or watched tie:
  - R33-01 tightens the v32 comparability tie (watch point 3);
  - R33-02 adds a value-set conjunct to INV-082, an attribute that fix 32's attribute table does not list.

## Notes on frozen items (for the human)

None.
