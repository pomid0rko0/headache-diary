# Review — iteration 34
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v33
Date: 2026-10-22

## Summary

This is the main review of iteration 34, by a new and independent reviewer. It checks v33 against its sources, against Stage 1 v18 and against itself. Every result below comes from my own downloads, scripts and reading.

**State of the files.**
- `OUTPUT_MODEL.md` is v33 and byte-identical to `history/v33.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a FROZEN marker.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18: sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5.
- v33: sections 1–10 (all 67 elements and 117 invariants, the traceability table, ISS-01 to ISS-12, section 9 and the Sources table), and the iteration-33 entries of sections 11 and 12.
- Loop files:
  - review 33 and fix 33;
  - the oscillation check after iteration 32, with its watch points and settled points;
  - the `diff` of v32 and v33.

  For each point I considered raising, I also searched all reviews, fixes and oscillation reports (see "Checked and not raised").

**Result.**
- **Quotes.** Every Stage 2 quote is verbatim in its source and on its stated page, and every translation is faithful.
- **Values.** Every value set, range, band, code, reference level, offset and threshold matches its source.
- **Sources.** Every source was reachable. No source has a newer version that changes an element: a web search found no ICHD-4 and no EHF update after the 2022 CGRP guideline.
- **Fidelity.** Every observable property of the 39 Stage 1 requirements is represented at the right strength.
- **Scope.** The model contains no input, storage or input-derivation content.
- **Mechanical checks.** All pass.
- **The v33 changes** are sound and consistent with the prose around them:
  - `OtherSummary` with the tightened `onSameScale` and `inSameForm`;
  - `HeadacheIndexKind` as a variant;
  - the `publishedGrading` conjunct of INV-082.
- **One remark (R34-01).** It is a minor citation defect. E-057 places the two [S-102] MIDAS quotes in a "subsection 'Migraine-related disability'" of the section "Headache impact on functioning". In the source, both are sibling sections of Methods. Earlier reviews described the location the same way but did not check the nesting. The JATS full text, both the Europe PMC copy and PMC's own efetch copy, is new evidence. The remark touches no watch-point item and reverses no fix.

## Verification coverage

### Downloads and tools

- **Where.** Every source was downloaded with `curl`, through the proxy, into a fresh folder outside the repository: `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r34/dl`.
  - Extracted text is in `…/r34/txt` and scripts are in `…/r34/scripts`.
  - Every script was run with `python3 -I`.
- **Extraction.**
  - PDFs: per-page `pdftotext`, in both `-raw` and `-layout` mode.
  - Europe PMC full-text XML and HTML pages: stripped to text with `lxml` (`strip.py`).
  - The S-034 title page is an image without a text layer, so I rendered it with `pdftoppm` and read it.
- **HTTP.** Every download returned HTTP 200:
  - the PDFs of S-001, S-007, S-008, S-010, S-016, S-018, S-033, S-034, S-035 and S-105;
  - the web pages of S-015 (Recommendations and Overview), S-028, S-103 and S-106 (chapter 2 and Overview);
  - the Europe PMC XML of S-011, S-012, S-013, S-014, S-023, S-101, S-102 and S-104.

  The PMC HTML page and the publisher PDF of S-102 returned bot-challenge pages to `curl`. The PMC copy of the article was therefore taken from the PMC efetch API (HTTP 200), in addition to Europe PMC.
- **Quote matching** (`quotes.py`, `strict.py`, `secpath.py`).
  - **Extraction.** Every double-quoted string in sections 1–10 outside the `omn` blocks was split at "[...]": 798 fragments of at least 6 letters or digits.
  - **Letters-only matching.** Text was normalised to NFKD, with combining marks, soft hyphens and the ICHD-3 "þ" glyph removed, case folded, and only letters and digits kept.
    - Each fragment was searched first in its tagged source, page by page and across adjacent pages, then in Stage 1 v18, then in every downloaded source.
  - **Punctuation-preserving pass.** Each match was mapped back to its source span and compared with punctuation kept. All 26 differences were read by hand. They are:
    - line-end hyphens ("def-inition", "con-sidered", "acetamino-phen");
    - the ICHD-3 glyphs without a text mapping ("≥", "±", "−"), which the model notes at each quote;
    - the end of a span at the last letter;
    - heading case ("USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES");
    - PDF spacing in [S-008] p. 12 ("≥50%", "a≥30%").

    None alters wording, numbers or meaning.
  - **Pages.** The pages on which each fragment was found were compared with the stated "p." or "PDF p." locations. All match:
    - for ICHD-3, PDF page = printed page;
    - for [S-016], PDF page = printed page + 6, as stated in Stage 1.
  - **Section paths** (`secpath.py`). For the Europe PMC sources I extracted the section path of each quote from the XML and compared it with the stated location. All match except [S-102] (R34-01).
  - **Item numbers.** I read [S-035] PDF p. 48 (Kutu 8: items 2 and 7) and p. 86 (section 7.3: items 3, 4 and 5) to confirm the item numbers that the locations state.

### Quote check per source

| Source | Fragments | Verified verbatim at stated location | Not found | Unreachable (what I tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (PDF, 211 pp.) | 68 | 67 in the PDF (pp. 8, 9, 12, 42, 105, 122–125, 139, 190, 209); 1 in Stage 1 | 0 | — |
| S-007 IHS cluster (UCL accepted manuscript) | 6 | 5 (pp. 10, 22, 25); 1 Stage 1 | 0 | — |
| S-008 IHS 2024 (univaq PDF) | 18 | 14 (pp. 9, 12, 13, 17); 4 Stage 1 | 0 | — |
| S-010 IHS 2025 (univaq PDF) | 34 | 29 (p. 6, including the sentence interrupted by "Cephalalgia 45(2)"); 5 Stage 1 | 0 | — |
| S-011 EHF 2022 (Europe PMC XML) | 19 | 10 (Background, paragraphs 1 and 2; question 3 and 4 statements); 8 Stage 1; 1 in [S-008], the source its sentence names | 0 | — |
| S-012, S-013 (Europe PMC XML) | 1 + 3 | 1 + 2 (Results > Consensus > Definition of triptan failure; Discussion > Drug failure / Assessment of patients); 1 in [S-015], the source its sentence names | 0 | — |
| S-014 EHF/LTB aids (Europe PMC XML) | 35 | 29 (HALT Indices paragraph, "Scoring HALT", Table 18, HURT paragraph); 6 Stage 1 | 0 | — |
| S-015 NICE CG150 (Recommendations and Overview pages) | 34 | 27 (1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48; the Overview population sentence); 6 Stage 1; 1 in [S-008] | 0 | — |
| S-016 SIGN 155 (PDF, 64 pp.) | 8 | 6 (PDF pp. 7, 20); 1 Stage 1; 1 in [S-008] | 0 | — |
| S-018 AAN/AHS clinician summary (PDF, 12 pp.) | 11 | 8 (pp. 1, 7, 8); 2 Stage 1; 1 in [S-033] | 0 | — |
| S-023 DMKG/ÖKSG/SKG (Europe PMC XML) | 5 | 4; 1 Stage 1 | 0 | — |
| S-028 NVN module (web page) | 9 (1 translation) | 6 (including the PICO under "Zoeken en selecteren"); 1 Stage 1; 1 in [S-035] | 0 | — |
| S-033 Russian adults (official PDF, 92 pp.) | 46 (3 translations) | 19 (pp. 1, 4, 39, 40, 41); 13 Stage 1; 10 in the sources their sentences name (E-041 Notes) | 0 | — |
| S-034 Russian children (official PDF, 53 pp.) | 16 (4 translations) | 8 (pp. 17, 52); 3 Stage 1; 1 on the rendered title page (image, p. 1: "Возрастная группа дети") | 0 | — |
| S-035 Turkish protocol (PDF, 92 pp.) | 44 (13 translations) | 27 (PDF pp. 6–7, 22–23, 47–48, 57, 77, 82, 83, 86); 1 Stage 1; 3 in [S-008] or [S-011], the sources their sentences name | 0 | — |
| S-101 HIT-6 (Europe PMC XML) | 4 | 4 (Methods > Data sources) | 0 | — |
| S-102 MIDAS / AMPP (Europe PMC XML; PMC efetch JATS) | 5 | 4 verbatim, but under Methods > "Migraine-related disability", not a subsection of "Headache impact on functioning" (**R34-01**); 1 in [S-014] | 0 | PMC HTML page and publisher PDF: bot challenge to `curl`; PMC efetch JATS retrieved instead |
| S-103 PedMIDAS page | 10 | 10 ("PedMIDAS Grading Scale"; page footer © 2026) | 0 | — |
| S-104 HADS (Europe PMC XML) | 3 | 3 (Discussion > "Construction of the Hospital Anxiety And Depression Scale (HADS)") | 0 | — |
| S-105 PHQ/GAD-7 manual (PDF, 9 pp.) | 3 + 2 (section 10) | 5 (P. 6/9 under "USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES"; the developers sentence on P. 8/9) | 0 | — |
| S-106 NICE TA260 (chapter 2, Overview) | 3 | 2 (paragraph 2.1, last sentence); 1 in [S-035] | 0 | — |
| Stage 1 sources reused only through Stage 1 quotes (S-002, S-005, S-022, S-030, S-032, S-042) | 21 | 20 verbatim in Stage 1 v18; 1 in [S-035] | 0 | not re-downloaded |
| Untagged strings | 392 | 358 verbatim in Stage 1 v18; 16 in a downloaded source; 18 model phrases or proposed wordings ("definitional", "the subject has migraine", "in the same view", "total score, where the instrument defines one") | 0 | — |

**Totals.** 798 fragments:
- 288 verified in the tagged source at the stated location;
- 431 verbatim in Stage 1 v18;
- 38 in another downloaded source that the sentence names;
- 22 English translations, read against their originals;
- 18 model phrases;
- 1 on the rendered image of the S-034 title page.

No quote was not found, and no source was unreachable.

- **Translations.** I read every translation of a Stage 2 quote against its original, and all are faithful:
  - S-028: the PICO;
  - S-033: pp. 1, 39, 40, 41;
  - S-034: pp. 1, 17, 52;
  - S-035: Kutu 8, sections 3.3, 3.6.3.9, 6, 7.1 and 7.3.
- **Text literals in `omn` blocks.** All 71 were checked:
  - the ICHD-3 code labels and the grade and category labels are verbatim in their sources;
  - the criterion names "NICE CG150 rec. 1.3.28", "IHS global practice recommendations Q6" and "IHS position statement 2025 control levels" are verbatim in Stage 1 OUT-020;
  - the `judgement` text of `critIhsQ6` is verbatim in Stage 1 OUT-020.
- **Metadata.**
  - PubMed esummary confirms:
    - S-101: Cephalalgia 2011;31(3):357–67, PMID 20819842, PMC3057423, DOI 10.1177/0333102410379890, authors Yang, Rendas-Baum, Varon, Kosinski;
    - S-102: J Headache Pain 2015;16:24, PMID 25902814, PMC4406925, DOI 10.1186/s10194-015-0503-y, seven authors as cited;
    - S-104: Health Qual Life Outcomes 2003;1:29, PMID 12914662, PMC183845; the article subject is "Commentary";
    - the PedMIDAS developer paper: Neurology 2001;57(11):2034–9, PMID 11739822.
  - S-105 PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
  - S-106: published 27 June 2012, last reviewed 11 January 2016.
  - S-015: last updated 03 June 2025; the Overview reads "Last reviewed: 23 September 2026".
- **Versions.**
  - Web search: ICHD-4 exists only as "Work in Progress 1" (Cephalalgia 2024), so [S-001] is current.
  - No EHF update after the 2022 CGRP guideline was found.
  - NICE CG150 1.3.24–1.3.25 now name atogepant and rimegepant. This changes no element: `ruleNice1328` applies to `cgrpInhibitor` in adults, and the 1.3.24 quote in E-041 is verbatim.

### Values checked against sources

- **Codes and classes (E-009, E-028).**
  - The code labels are verbatim on pp. 8, 9 and 12.
  - `classesOf826` matches 8.2.6 criterion B (p. 124), and `classesOf821to825` matches 8.2.6 note 2 (p. 125).
  - "simple analgesics" occurs once in the whole text layer, on p. 139 (checked page by page, across line breaks).
- **Overuse levels and span (E-032, INV-045).**
  - The levels are 15 days for 8.2.3, and 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8, over "more than three months" (pp. 122–125).
  - `dates.py` recomputed the span for every calendar month from 2020 to 2030 and for 28-day runs over 4,000 days. The minimality conjunct admits exactly 4 periods every time.
- **Evaluation rules (E-041).** I read all 18 rules against their quotes, for offset, anchor, timing, ages and `excludes`.
  - The NICE 1.3.27–1.3.29 texts are on the Recommendations page; TA260 2.1 says "every 12 weeks".
  - AAN/AHS 14A, 14B and 14H are on pp. 7–8.
  - SIGN 155 section 4.1 is on PDF p. 20, and 1.2.1 on PDF p. 7.
  - IHS 2024 Q2 and Q13 are on pp. 9 and 17.
  - The NVN PICO is under "Zoeken en selecteren".
  - The Russian passages are on pp. 39, 40 and 41, and the paediatric flowchart on p. 52.
  - The Turkish passages are Kutu 8 (PDF p. 48), 3.6.3.9 (p. 57), 7.1 (p. 83) and 7.3 (p. 86).
- **Named criteria (E-045) and control levels (E-046, INV-064).**
  - NICE 1.3.28: 50 % in episodic and 30 % in chronic migraine. NICE 1.3.29: 30 %.
  - IHS Q6: ≥ 50 %, with the 30 % chronic alternative; MIDAS ≥ 5 points for a baseline of 11–20, or ≥ 30 % for a baseline of ≥ 20; HIT-6 ≥ 5 points.
  - DMKG/ÖKSG/SKG: 50 %, 5 points and 30 %. Russian section 7.1: 50 %.
  - The [S-010] control levels map to n = 0, n < 4 over at least 3 months, 4 ≤ n ≤ 6, and n > 6.
- **Instruments (E-057, E-059).**
  - HIT-6: 36–78, with bands ≤ 49, 50–55, 56–59 and 60–78.
  - MIDAS: grades I–IV with the [S-102] labels, bands 0–5, 6–10, 11–20 and ≥ 21, and a three-month recall.
  - PedMIDAS: 0–10, 11–30, 31–50 and "Greater than 50".
  - HALT-90: the Table 18 bands, including the overlap at 20. HALT-30: "Grading is not used by HALT-30".
  - HADS: 0–21 per subscale. PHQ-9: 0–27. GAD-7: 0–21.
- **Windows and remission.**
  - The NICE 1.3.48 window is 4–8 weeks.
  - The A1.1 window is day 1 ± 2, with no day 0 (p. 190).
  - A cluster remission "must exceed three months" (p. 209).
- **Date examples recomputed** (`dates.py`):
  - 67 days (E-007); 41 and 294 days (INV-079); 42 and 143 days (E-063);
  - day 43, 6 April and the review window 7 April – 5 May (INV-049);
  - 26 March and 26 February – 25 March (12 weeks; 28 days), 4–31 December (28 days), and 1 April and 1 March (3- and 2-month time points) (E-042, INV-055);
  - "more than three months" (INV-089): 1 January – 31 March fails and 1 January – 1 April holds.

### Fidelity check per Stage 1 requirement

| OUT | Statement parts and Caveats checked | Result |
|---|---|---|
| 001 | Every view states its period (start, end, length) at MUST; frequency outputs per calendar month or 28-day period at MUST where provided; equal-length comparisons; Caveat (lengths visible) | OK |
| 002 | Definition label for every form of report (SHOULD); one definition per measure in a view | OK |
| 003 | Indicator next to every reporting period of a summary measure (SHOULD); no validated cut-off (SHOULD NOT); Caveat | OK |
| 004–007 | Headache days (MUST); migraine days for patients with migraine (MUST, label SHOULD); moderate/severe days and attacks (SHOULD, with MUST per month where provided); ICHD-3 definitions; attacks separate from days | OK |
| 008, 009 | MAY measures; time series with start, dose-change and stop markers in the view; weekly values where relevant | OK |
| 010 | Per period on a stated scale; comparison between periods on one scale and in one form, now also among other forms (v33) | OK |
| 011–013 | Duration and its treated-attack label; the Caveat as SHOULD NOT; symptoms and most bothersome symptom across periods and per treated attack; aura (MAY) | OK |
| 014–017 | Total, class and drug days; weekly view; overuse indicator with code, level, span and basis; prompt (MUST); no diagnosis (MUST NOT); withdrawal follow-up with the review window, the following year and the worsening label | OK |
| 018, 019 | Comparison per preventive treatment, values and both changes at MUST; time points by type and population; residual burden; the Caveat as MUST NOT | OK |
| 020 | Label names its criterion; named criteria tied (INV-116); underlying and other values; not the sole indicator; label's treatment preventive (INV-117) | OK |
| 021 | MUST components for the same baseline and on-treatment periods; SHOULD components where provided, intensity and symptom forms comparable (v33) | OK |
| 022, 023 | Post-stop monitoring; acute outcomes, consistency, timing, formulation, phases, 15 minutes for cluster headache; the Caveat as SHOULD NOT | OK |
| 024, 025, 039 | History with dates, dose changes, duration, response, adverse effects, stop reason, formulation, grouping and order; scheme windows (MAY); adherence next to the comparison, in the history and in the clinician summary | OK |
| 026 | Results where available, with name, date, recall, score, own published grading (none for HALT-30, v33) and change | OK (citation location of S-102: R34-01) |
| 027–034 | Functional impact and its comparison; three-month view (MUST, SHOULD, SHOULD NOT); per-type presentation; menstrual view (MUST, complete cycles); cluster view; trigger view with caveats; screening results; clinician summary | OK |
| 035–038 | Patient overview (plain language, time course on one scale and form, treatment effect, menstruation); paediatric (a)–(d) and Caveat; composite index (SHOULD NOT, SHOULD); interpretive caveats | OK |

The conformance levels match the strength of each Stage 1 statement part.
- MUST: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054, 055, 056, 057, 059, 068, 086, 102 and 108.
- MUST NOT: INV-048 and INV-106.
- SHOULD NOT: INV-013, 021, 043, 065, 084, 091, 101 and 107.
- Every attribute at MUST in a SHOULD or MAY element cites a MUST part (section 3.3, item 3).

### Mechanical checks (`mech.py`, `names.py`, inline scripts)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 117 invariants (INV-001 to INV-117), none missing or duplicated. Issues: ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn, section 9). |
| References | No dangling E-, INV- or ISS- reference. Every OUT reference exists in Stage 1. 37 source IDs are cited, all within S-001–S-046 or S-101–S-106. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names each requirement: 0 mismatches. |
| Levels and scope | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 40. Scopes: output 84, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Typing rule for levels | Every SHOULD or MAY attribute, and every MUST attribute with a `when` clause, has an `opt`, `set` or `seq` type, and none has a `set1` or `seq1` type. |
| Names | 539 names declared in `omn` blocks, none twice. Every attribute selection resolves to a declared attribute or component. What remains after removing declared names, attributes and bound variables is:<br>• the constants of the three multi-line enumerations, checked by reading;<br>• `let` names;<br>• the parameter `sc`;<br>• `refs` (section 2.5, settled since review 13). |
| Definedness | `days`, `first`, `last`, `s(i)`, `min`, `max`, `÷` and `classOf` are guarded where they are used. |
| v33 changes | • `OtherSummary` is declared once (E-023) and used in E-025.<br>• `onSameScale` and `inSameForm` remain equivalence relations by inspection.<br>• `otherHeadacheIndex ⟨Text⟩` is used only through `compositeIndicesOf` and `valueOfKind`; INV-093 compares with the constant tag `areaUnderHeadacheCurve`.<br>• The new INV-082 conjunct uses only `r.category`, `r.instrument` and `publishedGrading`.<br>• No prose still says "both of another form". |
| Scope sweep | I read in context every occurrence of enter, record, input, store, persist, database, serializ, encod, retention, reminder, answer, capture, algorithm, JSON, XML, CSV, FHIR, HL7 and data-entry in sections 1–10. Each is:<br>• an exclusion statement;<br>• the notation's "records";<br>• the [S-014] quote "records days affected";<br>• "can be answered" (INV-014 Reading);<br>• the INV-076 note on derivation from input.<br>Every threshold, formula and derived relation takes as arguments only output elements, constants or context properties. Every derived attribute whose arguments are all output elements has its relation stated. |

## Remarks

### R34-01 Citation defect: wrong location of the two [S-102] MIDAS quotes in E-057
- Item(s): E-057 (Evidence, the two [S-102] bullets).
- Problem:
  - E-057 locates both [S-102] quotes inside the section "Headache impact on functioning":
    - "[...] four grades based on total days of impaired functioning [...]" is at "(Methods, "Headache impact on functioning", subsection "Migraine-related disability")";
    - "The recall period for the MIDAS is three months" is at "(same subsection, the sentence after the grades)".
  - In the source, "Migraine-related disability" is not a subsection of "Headache impact on functioning". The two are sibling sections of Methods:
    - "Headache impact on functioning" is a single sentence that lists the measures used;
    - both quotes are in the next section, "Migraine-related disability".

  The stated location therefore misdescribes where the quotes stand in the source. PROCESS.md section 4 requires "the location in the source". Review 07 raised a location error of the same size (R07-03, the paragraph of an [S-011] quote).
- Evidence:
  - **Europe PMC full text** of PMC4406925 (`https://www.ebi.ac.uk/europepmc/webservices/rest/PMC4406925/fullTextXML`, HTTP 200). Under `<sec id="Sec2" disp-level="1"><title>Methods</title>`:
    - `<sec id="Sec5" disp-level="2"><title>Headache impact on functioning</title><p>We used the following migraine/headache impact measures: MIDAS (scored by grade), a MIDAS measure of lost productive time (LPT) [22,23] and the HIT-6 [21].</p></sec>`;
    - then, as a sibling, `<sec id="Sec6" disp-level="2"><title>Migraine-related disability</title><p>The MIDAS is comprised of five questions [...] four grades based on total days of impaired functioning (i.e., Grade I or little or no disability, 0 to 5; [...] Grade IV or severe disability, ≥21, with an option of dividing Grade IV into IVA and IVB). The recall period for the MIDAS is three months, effectively covering three menstrual cycles.</p></sec>`.
  - **PMC's own JATS copy** (`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pmc&id=4406925`, HTTP 200), from which the PMC page listed in section 10 is rendered, has the same structure: Sec5 "Headache impact on functioning" and Sec6 "Migraine-related disability" are both children of Sec2 "Methods", followed by Sec7 "Lost productive time".
  - **Earlier reviews** (05, 09, 10, 10b, 14, 23, 25b, 31, 32, 33) reported the location as "Headache impact on functioning" > "Migraine-related disability" without checking the nesting. No review or fix examined it, so this is new evidence and not a re-raised remark. The remark touches no frozen or watch-point item.
- Required change: in E-057 Evidence, change the first location to "(Methods, section "Migraine-related disability")" and the second to "(same section, the sentence after the grades)". The quotes themselves are verbatim and unchanged. If any other text gives the location, align it as well; I found none in sections 1–11.

## Checked and not raised

- **The v33 fixes.**
  - R33-01: the review's option (a), with `OtherSummary`. `onSameScale` and `inSameForm` now separate two different other forms, and each remains an equivalence relation (two named forms, or two other forms with equal `form` texts). Satisfiability is unchanged: periods summarised alike satisfy every conjunct.
  - R33-02: the `publishedGrading` conjunct of INV-082. Every result that an invariant asks for still meets INV-082, because E-058 asks for a category only where `publishedGrading` holds.
  - The same-defect fix of E-033, `otherHeadacheIndex ⟨Text⟩`.

  None of these reverses a watch point of the check after iteration 32. Watch point 3 (comparability) is tightened in its own direction, and watch point 1 (INV-082) gains one conjunct.
- **`otherHeadacheIndex(x)` with x naming the AUC.** Its Meaning says it is "another index". Review 04 settled the parallel case for instruments: a named instrument shown under another name is excluded by the Meaning. No new evidence.
- **HURT's per-response areas against a single `category`.** Review 10b settled that `publishedCategory ⟨Text⟩` shows HURT's areas as published, and ISS-06 records the total-score question. Fix 33 re-examined HURT. No new evidence.
- **𝔹-valued given functions used as formulas** (`publishedGrading`, `banded`, `isMonthSpan`, `showsValueNamed`, `⊑`). Review 22b settled that their reading is unambiguous.
- **`refs`.** It is defined in the notation section (2.5); settled in review 13.
- **INV-048 scope.** Reviews 10 and 10b settled that a presentation of the indicator as a diagnosis by its surroundings is a claim of the indicator.
- **`concerns` for all-types indices of mixed-type subjects** (INV-091 to INV-093). Settled in reviews 01 and 10.
- **OUT-019 and moderate/severe headache days** (INV-060). Settled in reviews 14, 20 and 22: Stage 1 distinguishes "headache days" from "moderate/severe headache days" in the same sentence.
- **Cycle-line menstruation days and the context's `menstruationSpans`.** Fix 32's attribute table classifies these as values obtained from diary information, not attributes that presuppose a context fact. A remark here would widen the "truth of a shown fact" class (watch point 1) without new evidence. Not raised.
- **The optimal-control level and the acute-treatment part of [S-010].** The response to acute treatment is kept as a value the criterion rests on (`acuteTreatmentEffectiveness`, INV-062). No threshold of "satisfactory response" can be tested on the values shown. Consistent with the settled control-level points.
- **E-016's Conformance** omits "at calendar-month or 28-day granularity", which E-015 and E-017 state. It names INV-015, whose predicate and Reading state the granularity. This is a summary wording, not a defect.
- **S-101 and S-102 are studies, not the developers' instrument publications.** Each is co-authored by developers of the instrument (Kosinski for HIT-6; Stewart and Lipton for MIDAS), and the developers' own papers are not open access (search log). S-103 to S-105 come from the developers or their institution. The MIDAS labels are a settled point. No new evidence.
- **Settled points, not reopened (no new evidence):**
  - INV-060 with INV-061 for short compared periods;
  - INV-027 tied to preventive treatments;
  - E-063 `duration` and E-058 `changeFromBaseline`;
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
  - adherence windows reaching past the stop;
  - "baseline administration" as any earlier administration;
  - E-039 `reviewWindow` without a `when` clause.
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded, and their quotes are verbatim at the stated locations:
  - "simple analgesics" occurs only on p. 139, in the comments on 10.1.1;
  - "ibuprofen or other NSAIDS" is in the comment on 7.3.2 (p. 105);
  - the 3.1.1 and 3.1.2 passages are on p. 42;
  - the Definitions of terms are on p. 209;
  - A1.1 is on p. 190;
  - NICE 1.3.9, 1.3.39 and 1.3.48 read as quoted.

  The descriptions of the Stage 1 passages are accurate. No Stage 1 issue is worked around silently.

## Notes on frozen items (for the human)

None.
