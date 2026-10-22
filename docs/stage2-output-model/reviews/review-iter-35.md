# Review — iteration 35
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v34
Date: 2026-10-22

## Summary

This is the main review of iteration 35, by a new and independent reviewer. It checks v34 against its sources, against Stage 1 v18 and against itself. Every result below comes from my own downloads, scripts and reading.

**State of the files.**
- `OUTPUT_MODEL.md` is v34 and byte-identical to `history/v34.md`.
- `FROZEN_ITEMS.md` does not exist, and no item carries a FROZEN marker.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18: sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5.
- v34: sections 1–10 (all 67 elements, 117 invariants, the traceability table, ISS-01 to ISS-12, sections 9 and 10), and the iteration-34 entries of sections 11 and 12.
- Loop files:
  - review 34 and fix 34;
  - the oscillation check after iteration 32, with its findings, settled points and watch points, and the watch points of the checks after iterations 12 and 16 that it carries forward.

  For each point I considered raising, I searched all reviews, fixes and oscillation reports (see "Checked and not raised").

**Result.**
- **Quotes.** Every quote is verbatim in its source, on its stated page or section. Every translation is faithful.
- **Values.** Every value set, range, band, code, label, reference level, offset and threshold matches its source.
- **Sources.** All were reachable. No newer version changes an element: ICHD-4 exists only as "Work in Progress 1", and I found no EHF update after the 2022 CGRP guideline.
- **Fidelity.** All 39 Stage 1 requirements are represented at the right strength.
- **Scope.** The model contains no input, storage or input-derivation content.
- **Mechanical checks.** All pass.
- **The v34 changes** are correct. These are the two [S-102] locations of E-057 and the [S-001] location of ISS-03. I checked them in the JATS full text and on the ICHD-3 web edition.
- **One remark (R35-01), a formal defect.** INV-087 holds for every cycle line in every view, but outside the menstrual-relation view it does not stop two cycle lines from overlapping.
  - As a result, a patient-facing overview can mark an attack as outside the ICHD-3 A1.1 perimenstrual window even though the attack falls on day +2 of a menstruation that the same view shows.
  - So the claims in INV-087 Notes, E-061 Notes, INV-105 Notes and row OUT-035 that every attack mark is correct are not guaranteed by the predicate. A script confirms this.
  - No earlier remark or fix considered two overlapping lines. The required change hits none of the reversal triggers of the menstrual-relation-view watch point.

## Verification coverage

### Downloads and tools

- **Where.** Every source was downloaded with `curl` through the proxy into its own folder under `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r35/dl/`.
  - Extracted text is in `…/r35/txt`, scripts in `…/r35/scripts` and outputs in `…/r35/out`.
  - Every script ran with `python3 -I`.
- **HTTP.** Every download returned HTTP 200:
  - **PDFs:** S-001, S-007, S-008, S-010, S-016, S-018, S-033, S-034, S-035 and S-105. The first two attempts at S-033 and S-034 (apicr.minzdrav.gov.ru) ended in a proxy "connection reset", which the proxy status logged as `ws_closed_mid_exchange`. The retry returned 200.
  - **Europe PMC full-text XML:** S-011, S-012, S-013, S-014, S-023, S-042, S-101, S-102 and S-104. For S-102 I also fetched PMC's own JATS copy through efetch.
  - **Web pages:**
    - S-015: the Recommendations and Overview pages;
    - S-028;
    - S-103;
    - S-106: chapter 2 and the Overview page;
    - the ichd-3.org pages of A1.1 and A1.1.3.
  - **PubMed esummary:** PMIDs 20819842, 25902814, 12914662 and 11739822.
- **Extraction.**
  - PDFs: per page, with `pdftotext -raw` and `-layout`.
  - XML and HTML: text with `lxml`.
  - The image-only title page of S-034 was rendered with `pdftoppm` and read: "Возрастная группа дети", "Год утверждения 2024".
- **Quote matching** (`quotes.py`).
  - **Extraction.** Every double-quoted string in sections 1–10 outside `omn` blocks was split at "[...]". This gave 799 fragments of at least 6 letters or digits.
  - **Normalisation.** Text was normalised to NFKD, with marks, soft hyphens and the ICHD-3 "þ" removed, case-folded, and only letters and digits kept.
  - **Search order.** Each fragment was searched page by page, and across adjacent pages, in its tagged source, then in Stage 1 v18, then in every downloaded source.
  - **Locations.** Pages were compared with the stated locations:
    - PDF page = printed page for S-001, S-007, S-008, S-010, S-018, S-033 and S-034;
    - S-016: printed page = PDF page − 6;
    - S-035: stated as "PDF p.";
    - S-105: "P. n/9" = PDF page n.
  - **Section paths.** `secpath.py` extracted the section path of each quote in the Europe PMC JATS sources.
  - **Item numbers.** I read the item numbers of S-035 Kutu 8 (PDF p. 48; items 2 and 7) and section 7.3 (PDF p. 86; items 3, 4 and 5) on the page.

### Quote check per source

| Source | Fragments | Verified verbatim at the stated location | Not found | Unreachable (what I tried) |
|---|---|---|---|---|
| S-001 ICHD-3 PDF | 69 | 69 (pp. 8, 9, 12, 42, 105, 122–125, 139, 190, 209). "Simple analgesics" occurs once in the whole text, p. 139. The A1.1.3 comment is on p. 190; the ichd-3.org web edition shows it on the A1.1.3 page. | 0 | — |
| S-007 IHS cluster (UCL manuscript) | 5 | 5 (pp. 10, 22, 25) | 0 | — |
| S-008 IHS 2024 | 20 | 20 (pp. 9, 12, 13, 17; Q6 list read in full) | 0 | — |
| S-010 IHS 2025 | 31 | 31 (p. 6, including the sentence interrupted by "Cephalalgia 45(2)") | 0 | — |
| S-011 EHF 2022 (Europe PMC) | 11 | 11 (Background, paragraphs 1–2; Results > Expert consensus statements, questions 3 and 4) | 0 | — |
| S-012, S-013 (Europe PMC) | 1 + 4 | 5 (Results > Consensus > Definition of triptan failure; Discussion > Drug failure; Discussion > Assessment of patients) | 0 | — |
| S-014 EHF/LTB (Europe PMC) | 30 | 30 (the HALT Indices paragraph; "Scoring HALT" first sentence; Table 18; the HURT paragraph) | 0 | — |
| S-015 NICE CG150 | 29 | 29 (1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48; the headings "Migraine with or without aura" and "Prophylactic treatment review"; Overview: "young people (aged 12 years and older) and adults"; "Last reviewed: 23 September 2026") | 0 | — |
| S-016 SIGN 155 (2026) | 7 | 7 (PDF pp. 7, 20) | 0 | — |
| S-018 AAN/AHS clinician summary | 10 | 10 (pp. 1, 7, 8) | 0 | — |
| S-023 DMKG (Europe PMC) | 4 | 4 (Hintergrund) | 0 | — |
| S-028 NVN | 7 (+1 translation) | 7 (Aanbeveling; PICO under "Zoeken en selecteren") | 0 | — |
| S-033 Russian adults | 21 (+4 translations) | 21 (pp. 1, 4, 39, 40, 41, 53) | 0 | — |
| S-034 Russian children | 9 (+3 translations) | 8 (pp. 17, 52) + 1 on the rendered image of p. 1 | 0 | — |
| S-035 Turkish protocol | 34 (+13 translations) | 34 (PDF pp. 6–7, 23, 47–48, 57, 77, 82–83, 86) | 0 | — |
| S-042 Saudi consensus | 1 | 1 (Results > Table 2) | 0 | — |
| S-101 HIT-6 | 5 | 5 (Methods > Data sources) | 0 | — |
| S-102 MIDAS / AMPP | 4 | 4 (Methods > Migraine-related disability, as corrected in v34; both JATS copies agree) | 0 | — |
| S-103 PedMIDAS page | 12 | 12 ("PedMIDAS Grading Scale"; footer "© 2026 Cincinnati Children's Hospital Medical Center") | 0 | — |
| S-104 HADS | 3 | 3 (Discussion > "Construction of the Hospital Anxiety And Depression Scale (HADS)") | 0 | — |
| S-105 PHQ/GAD-7 manual | 5 | 5 (P. 6/9 under "USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES"; the same sentence also stands on P. 5/9; developers' sentence on P. 8/9) | 0 | — |
| S-106 NICE TA260 | 2 | 2 (paragraph 2.1, last sentence; Overview "Last reviewed: 11 January 2016") | 0 | — |
| Stage 1 text (quotes carried over, Stage 1 statement and source wording) | 431 | 431 verbatim in Stage 1 v18 | 0 | not re-downloaded |

**Totals.** 799 fragments:
- 324 verbatim in a downloaded source at the stated location;
- 431 verbatim in Stage 1 v18;
- 22 English translations, read against their originals (S-028, S-033, S-034, S-035) and all faithful;
- 18 model phrases or proposed wordings ("definitional", "the subject has migraine", "total score, where the instrument defines one", …);
- 3 regex artefacts spanning two quotes on one line (their parts are verified);
- 1 image-only text (S-034 title page), read on the rendered page.

No quote was not found, and no source was unreachable.

**Metadata** (PubMed esummary):
- S-101: Cephalalgia 2011;31(3):357–67, PMC3057423, DOI 10.1177/0333102410379890, four authors as cited.
- S-102: J Headache Pain 2015;16:24, PMC4406925, DOI 10.1186/s10194-015-0503-y, seven authors as cited. PubMed spells the first author "Pavlović".
- S-104: Health Qual Life Outcomes 2003;1:29, PMC183845.
- The PedMIDAS developer paper: Neurology 2001;57(11):2034–9, PMID 11739822.

**Versions.**
- Web search: ICHD-4 exists only as "Work in Progress 1" (Cephalalgia 2024), so [S-001] is current.
- No EHF guideline update after 2022 was found.
- NICE CG150 1.3.24 now lists atogepant and the other technology appraisals. This changes no element: the quoted part of 1.3.24 is verbatim.

### Values checked against sources

- **Codes and classes.**
  - The code labels are verbatim on pp. 8, 9 and 12.
  - `classesOf826` matches 8.2.6 criterion B, and `classesOf821to825` matches 8.2.6 note 2.
- **Overuse levels.**
  - The levels are 15 days for 8.2.3 and 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8, over "more than three months" (pp. 122–125).
  - The span reading (shortest run of monthly periods that lasts more than 3 months) gives 4 periods for both calendar months and 28-day periods. I checked this by hand from the minimal and maximal month lengths.
- **Evaluation rules (E-041).** I read all 18 rules against their quotes: offset, anchor, timing, ages and `excludes`. The sources are:
  - NICE 1.3.27–1.3.29;
  - AAN/AHS 14A, 14B and 14H;
  - SIGN 155 section 4.1 and 1.2.1;
  - EHF 2022 question 3;
  - IHS 2024 Q2 and Q13;
  - the NVN PICO;
  - the Russian sections 3.3 and 7.1 (pp. 39–41) and the paediatric flowchart (p. 52);
  - Turkish Kutu 8 (items 2 and 7), 3.6.3.9 and 7.3 (items 3–5);
  - TA260 2.1 "every 12 weeks".
- **Named criteria and control levels.**
  - NICE 1.3.28: 50 % / 30 %. NICE 1.3.29: 30 %.
  - IHS Q6: ≥ 50 %, the chronic 30 % alternative, MIDAS ≥ 5 points for a baseline of 11–20 or ≥ 30 % for a baseline of ≥ 20, and HIT-6 ≥ 5 points (pp. 12–13).
  - DMKG: 50 %, 5 points and 30 %. Russian 7.1: 50 % of headache days.
  - [S-010]: n = 0; n < 4 for three months; 4–6; and > 6, with insufficient control also possible below six.
- **Instruments.**
  - HIT-6: 36–78, bands ≤ 49, 50–55, 56–59 and 60–78.
  - MIDAS: grades I–IV with the [S-102] labels and bands, and three-month recall.
  - PedMIDAS: 0–10, 11–30, 31–50 and "Greater than 50".
  - HALT-90: the Table 18 bands, with the overlap at 20. HALT-30: "Grading is not used by HALT-30". HALT recall: 3 and 1 months.
  - HADS: 0–21 per subscale. PHQ-9: 0–27. GAD-7: 0–21.
- **Windows.**
  - NICE 1.3.48: 4–8 weeks.
  - A1.1: day 1 ± 2 (days −2 to +3), with no day 0 (p. 190).
  - Cluster remission "must exceed three months" (p. 209).
- **Date examples recomputed:**
  - 67 days (E-007);
  - 41 and 294 days (INV-079);
  - 42 and 143 days (E-063);
  - day 43, 6 April and the window 7 April – 5 May (INV-049);
  - 26 March and 26 February – 25 March, the intervals ending 28 February, 25 March and 31 March, and the stops on 10 February, 30 and 31 March (E-042, INV-055).

### Fidelity check per Stage 1 requirement

| OUT | Statement parts and Caveats checked | Result |
|---|---|---|
| 001 | Period stated with start, end and length (MUST, INV-003); frequency outputs per calendar month or 28-day period (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); Caveat (`lengthDays`) | OK |
| 002 | Labels for every form of report (SHOULD, INV-008); one definition per measure (INV-111) | OK |
| 003 | Indicator for each period of a summary measure (SHOULD); no validated cut-off (SHOULD NOT, INV-013); Caveat | OK |
| 004–007 | Headache days (MUST, ICHD-3 at MUST); migraine days for patients with migraine (MUST, label SHOULD); moderate/severe days and attacks (SHOULD, per month MUST where provided); attacks separate | OK |
| 008, 009 | MAY measures; time series with start, dose-change and stop markers in the view; weekly values where relevant | OK |
| 010, 011 | Intensity per period on a stated scale, comparison on one scale and in one form; duration, treated-attack label and the Caveat as SHOULD NOT | OK |
| 012, 013 | Symptoms and most bothersome symptom across periods and per treated attack, for migraine; aura (MAY) | OK |
| 014–017 | Total, class and drug days (MUST); weekly view; indicator with code, level, span and basis, prompt (MUST), not a diagnosis (MUST NOT); withdrawal follow-up, review window, the following year and the worsening label | OK |
| 018, 019 | Comparison per preventive treatment, values and both changes (MUST), time points by type and population, `where reported` (INV-057); the Caveat as MUST NOT; residual burden | OK |
| 020 | Named criterion, underlying and other values, not the sole indicator, no verdict on continuation | OK |
| 021, 022 | MUST components for the same periods; SHOULD components where provided; post-stop monitoring against the on-treatment period and the original baseline | OK |
| 023 | All named outcomes, consistency, timing, formulation, separate baseline and on-treatment summaries, 15 minutes for cluster headache, the Caveat as SHOULD NOT | OK |
| 024, 025, 039 | History lists, dates, dose changes, duration, response, adverse effects, stop reason, formulation, grouping and order; scheme windows (MAY); adherence next to the comparison, in the history and in the clinician summary | OK |
| 026, 027 | Results where available with name, date, recall, score, own grading and change; functional impact and its comparison | OK |
| 028, 029 | Three-month view (MUST), definitions (SHOULD), no diagnosis (SHOULD NOT); per-type presentation (MUST) and intensity per type (SHOULD) | OK |
| 030 | View for every time range during which the subject menstruates; A1.1 window distinguished; complete cycles stated | OK in the menstrual-relation view. For cycle lines of other views, see **R35-01**. |
| 031–033 | Bouts, remissions, rates, 15-minute effectiveness and rescue, previous bouts; trigger view with caveats; screening results next to headache outputs, not diagnoses | OK |
| 034 | Clinician summary with all named components, period chosen by the clinician or since the previous consultation | OK |
| 035 | Overview in plain language with the named components | Components OK. The window marks of its cycle lines are not guaranteed correct: **R35-01**. |
| 036–038 | Paediatric (a)–(d) and Caveat; composite index (SHOULD NOT, SHOULD, SHOULD); interpretive caveats | OK |

**Conformance levels** match the Stage 1 strength of each statement part:
- MUST: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054, 055, 056, 057, 059, 068, 086, 102 and 108.
- MUST NOT: INV-048 and INV-106.
- SHOULD NOT: INV-013, 021, 043, 065, 084, 091, 101 and 107.
- Each MUST attribute of a SHOULD or MAY element cites a MUST part.

### Mechanical checks (`mech.py`, `names.py`, `cex87.py`)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 117 invariants (INV-001 to INV-117), none missing or duplicated. Issues: ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn, section 9). |
| References | No dangling E-, INV- or ISS- reference. Every OUT reference is one of the 39 Stage 1 requirements. 35 source IDs are cited, each in Stage 1 section 5 or in section 10. Every S-101 to S-106 is cited outside the table. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. No FROZEN marker. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names each requirement: 0 mismatches. |
| Levels and scope | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 40. Scopes: output 84, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Names | 188 `omn` blocks; 347 declared names, none declared twice. Every identifier is declared, bound, an attribute, a parameter or an enumeration or variant constant, except `_` (from `_⊑_`) and `refs` (section 2.5). Every attribute selection names a declared attribute or component. |
| Definedness (by reading) | `days`, `first`, `last`, `s(i)`, `min`, `max`, `÷`, `classOf` and `periodEndFrom` are guarded where they are used, including `min cl.menstruationDays`, `max A` (INV-069) and every `days(…)` in INV-037, INV-079 and INV-089. |
| Prose claims of predicates | Checked by hand: the INV-046 "two directions agree" claim, the INV-012 pairwise claim (1-D Helly), `scopeFor` uniqueness, `courseOverlaps` = `courseNotOutside` for a stated start, `fitsMonthlyPeriod`, and the INV-055 satisfiability construction. All hold.<br>The INV-087 claim that every attack mark is correct under ICHD-3 A1.1 fails in a view other than the menstrual-relation view (`cex87.py`, **R35-01**). |
| Scope sweep | I read in context every occurrence of enter, record, input, store, persist, database, serializ, encod, retention, reminder, answer, capture, algorithm, JSON, XML, CSV, FHIR, HL7, data-entry and entry in sections 1–10. Each is one of:<br>• an exclusion statement;<br>• the notation's "records";<br>• the [S-014] quote "records days affected";<br>• "can be answered";<br>• the out-of-scope notes of E-057 and INV-076.<br>Every threshold, formula and derived relation takes only output elements, cited constants or context properties as arguments. |

## Remarks

### R35-01 Formal defect: cycle lines shown outside the menstrual-relation view may overlap, so an attack can be marked outside the A1.1 window on a window day of a menstruation the same view shows
- Item(s): INV-087 (Predicate, Reading, Notes); E-060 (Notes); E-061 (Notes); INV-105 (Notes); section 7 rows OUT-030 and OUT-035.
- Problem:
  - **What INV-087 constrains.** It holds for every cycle line and every attack mark in every view. That is the R02 pattern (fix 02, other change 8), and E-060 Notes, E-067 Notes and INV-105 Notes rely on it for the patient-facing overview.
    - It ties a line's day 1, window and `nextWindowDays` to the line's own `cycle` span.
    - It attaches each attack mark to exactly one line of its view.
    - It tests the mark only against that line's own window and `nextWindowDays`.
  - **What it does not constrain.** The non-overlap of lines is a consequence of the sequence structure, which binds only `MenstrualRelationView` (`v.content ∩ CycleLine = ran v.cycles`, consecutive lines).
    - For any other view that shows cycle lines, and for lines of different views of one output, nothing stops a day 1 shown by one line from lying inside another line's span. Such a view is the overview of INV-105, which requires "a cycle line that overlaps that period" and so may show several.
    - The only output-wide rule is for lead-ins: `∀ cl₂ : CycleLine • ∀ d ∈ cl₂.firstDayOfMenstruation • cl.cycle.to < d`. It does not cover lines that show their day 1.
  - **Two consequences.**
    - **The outputs it admits contradict E-060's definition of `cycle`.** A line that has ended runs "to the day before the next first day of menstruation" (E-060), yet another line of the same view or output shows a first day of menstruation inside it.
    - **A derived MUST value can be wrong under ICHD-3 A1.1.** `inPerimenstrualWindow` (E-061) is set from the attack's own line only, so an attack on a window day of a menstruation shown by another line is marked "outside". OUT-030 (MUST) requires the window "as defined in ICHD-3 appendix A1.1" to be distinguished from the other days of the cycle. OUT-035 (SHOULD) asks the overview for "the relationship to menstruation".
  - **The model's prose claims more than the predicate gives.**
    - INV-087 Notes (line 3357): "the mark of every attack shown is correct under ICHD-3 A1.1".
    - INV-105 Notes (line 3666): "so that the window marks of the overview are correct for every attack it marks".
    - E-060 Notes (line 1814): "So every day of a line that lies in the window of a menstruation the view shows is shown as a window day".
    - E-061 Notes (line 1828): a mark can say nothing about a shown menstruation's window "only for an attack in a lead-in, or one after the last day of a line that has not ended".
    - Row OUT-035: "every attack mark shown attached to a cycle line and correctly marked".
- Evidence:
  - **Case 1: one patient-facing overview** of 1–31 March 2026 (`cex87.py`, which encodes every conjunct of INV-087).
    - Line A: `cycle` 1–28 March, `dayOneShown`, `complete`, `menstruationDays` 1–5 March, window 27 February – 3 March, `nextWindowDays` 27–28 March, `migraineDays` {16 March}, attacks {a}.
    - Line B: `cycle` 15–31 March, `dayOneShown`, not complete (it ends on the last covered day), `menstruationDays` 15–19 March, window 13–17 March.
    - Attack mark a: onset 16 March, `inPerimenstrualWindow = false`.
    - INV-087 holds: each line's own conjuncts hold, a is an attack of exactly one line of the view (A), and "outside" matches A's window and `nextWindowDays`. The menstrual-relation-view conjuncts do not apply.
    - INV-105's cycle-line conjunct holds.
    - Yet the overview shows a menstruation with day 1 on 15 March, so 16 March is its day +2, inside "day 1 ± 2 (i.e. days −2 to +3)" ([S-001] A1.1.1 and A1.1.2 criterion B, p. 190). The attack is shown as outside the window.
    - Line A also says that no menstruation began between 2 and 28 March (E-060: "to the day before the next first day of menstruation"), which line B contradicts.
  - **Case 2: one output with a menstrual-relation view and an overview.**
    - The menstrual-relation view shows the cycles 1–28 March and 29–31 March.
    - The overview shows a line with day 1 on 15 March, ending 10 April.
    - INV-087 holds. The output states both that no day 1 fell between 2 and 28 March and that one fell on 15 March.
  - **Why this is new.** No earlier remark or fix considered two lines that overlap.
    - Fix 02 (other change 8) extended the per-line and attack-mark relations to every view and kept "the sequence structure, the overlap with the covered period and `completeCycles`" in the menstrual-relation view.
    - R03-03 concerned attack marks without a shown cycle; R04-01 the lead-in; R04-04 `nextWindowDays`.
    - Reviews 03, 10b, 19b, 22, 24, 25b and 32b examined only the MUST attributes of a cycle line in the overview.
    - Fix 04 already gave the reason that makes the required tie satisfiable: "all views of one output summarise the same diary information as of one as-of date". It used that reason for the lead-in rule only.
  - **Watch points.** The remark touches the menstrual-relation view and overview watch point (check after iteration 12, item 4; carried by the check after iteration 32, watch point 5). It hits none of its reversal triggers:
    - it does not restore a subject-level `menstruates`;
    - it requires no view or line for a period without menstruation;
    - it neither removes nor restricts the lead-in, whose rule is already stronger than the tie below;
    - it does not relax the start of the view;
    - it does not move the sequence structure of fix 02 into the overview.

    It is not a "truth of a shown fact" tie to the context (watch point 1): its arguments are output elements only.
- Required change:
  - **(a) Preferred.** Add a definitional conjunct to INV-087 so that no first day of menstruation shown in the output lies after the first day of another cycle line and within that line, for example:

    `∀ cl, cl₂ : CycleLine • ∀ d ∈ cl₂.firstDayOfMenstruation • ¬ (cl.cycle.from < d ∧ d ≤ cl.cycle.to)`

    This is output-wide, as the lead-in rule is.
    - It is satisfiable, because the true cycles of the summarised diary information never overlap. Lines of one consecutive sequence meet it, and so does the same cycle shown in two views.
    - It does not narrow the menstrual-relation view, whose consecutive lines already meet it.
    - With it, a menstruation shown in the view whose window contains an attack's onset is that of the attack's own line (day 1 to day 1 + 2) or the next one (`nextWindowDays`), so the mark is correct.
  - **(b) Alternative.** The same conjunct restricted to two lines of one view (`viewOf(cl₂) = viewOf(cl)`). This suffices for the attack marks and the window days of one view. It leaves different views of one output free to state contradictory cycles, so the Notes would have to say so.
  - **In either case:**
    - update the INV-087 Reading and Notes, E-060 Notes, E-061 Notes and INV-105 Notes;
    - update rows OUT-030 and OUT-035, so that their claims match the predicate.

    Aligning only the prose, without the conjunct, would not suffice: the overview would still mark an attack on a window day of a menstruation it shows as outside the A1.1 window.

## Checked and not raised

- **The v34 changes.**
  - E-057: the two [S-102] quotes now stand at "(Methods, section "Migraine-related disability")" and "(same section, the sentence after the grades)". Both JATS copies place Sec6 "Migraine-related disability" as a sibling of Sec5 under Methods, and both quotes are in its single paragraph.
  - ISS-03: the A1.1.3 location. On p. 190, "Comments: This subclassification of 1.1 Migraine without aura …" follows A1.1.3's criteria and note. The ichd-3.org web edition shows it on the A1.1.3 page and not on the A1.1 page.
  - No `omn` block changed between v33 and v34.
- **Cycle-line migraine dates against migraine-day counts of the same view** (and attack marks against attack counts).
  - The model states no relation between the dated migraine days or attack marks of cycle lines and the counts shown for a period with the same dates. An overview could therefore list more migraine dates in a month than its migraine-day count.
  - Neither value is computed from the other: both are obtained from diary information. Stage 1 asks for no such relation, and PROCESS section 2 requires the relations of computed fields only.
  - An optional addition, not raised.
- **INV-076 for cluster-scoped summaries of a subject who also has migraine.** INV-076 asks every treated-attack line of a subject with migraine for the three symptom statuses, also in the 15-minute summaries of the cluster view. Its `hasType(ctx, c1)` condition is fix 02's answer to R02-06 (the review's first option). Changing it would reverse that fix without evidence that OUT-012's "For migraine" means the attack's type. Not raised.
- **DMKG/ÖKSG/SKG chronic-migraine sentence** (the [S-023] passage after the episodic criterion). Settled in reviews 11 and 30. `critDmkg` is named "(episodic migraine)", and the criterion list is open. No new evidence.
- **OUT-024 "does not by itself establish eligibility" and OUT-031 "should not be read as treatment effect"** have no prohibition invariant. Fix 01 classed them as descriptive and reading instructions, and reviews 19c and 21b kept that. No new evidence.
- **Cluster-view bouts, remissions and rates as references not placed in the view.** Fix 11 declined this (OUT-031 asks for no co-presence); review 24 kept it. No new evidence.
- **Context course events as arguments of relations** (INV-036, INV-079, INV-109, INV-112 and others). The context is the semantic parameter of section 3.2, whose components "become known" outside the model (section 3.5). This is the settled "truth of a shown fact" class (check after iteration 32, watch point 1). No new evidence.
- **IHS 2024 Q6 Essential level** ("continue treatment in all persons with migraine that report a meaningful subjective improvement"). Stage 1 quotes the Optimal list, which `critIhsQ6` models in full (p. 12: three list items and the chronic 30 % alternative).
- **Turkish Kutu 8** also states that the onset of efficacy may take 2–3 months and that the maximum comes within six months, and that treatment should be re-evaluated in remission. E-041 Notes list onset and maximum as not evaluation time points. Remission re-evaluation is a continuation decision. Not raised.
- **Instruments.**
  - The MIDAS labels and the undivided Grade IV, the HIT-6 one-month recall, the HALT-90 overlap at 20, HURT's per-response areas (ISS-06), and HADS subscales only are settled points. No new evidence.
  - `publishedGrading` left open for MSQ v2.1, M-TOQ and PGIC follows E-057 Notes.
- **Formal points, settled:**
  - `refs` (section 2.5);
  - 𝔹-valued functions used as formulas;
  - INV-060 with INV-061 for short compared periods;
  - INV-106 at MUST NOT;
  - the "> 3 months" readings of INV-045 and INV-089;
  - `excludes` and the rule-list boundary;
  - the evaluated periods of a responder label (fix 18);
  - the formulation of an acute summary (fix 17);
  - E-063 `duration` and E-058 `changeFromBaseline`;
  - INV-078 grouping and INV-035 at SHOULD;
  - adherence windows past the stop;
  - empty `remissions` in chronic cluster headache (ISS-12);
  - "baseline administration" as any earlier administration;
  - INV-027 tied to preventive treatments.

  None reopened (no new evidence).
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded, and their quotes and locations are verbatim:
  - 8.2.6 criterion B and note 2;
  - "simple analgesics" only on p. 139;
  - 7.3.2 "ibuprofen or other NSAIDS" on p. 105;
  - A1.1.3 comments on p. 190;
  - NICE 1.3.9, 1.3.39 and 1.3.48;
  - S-034 p. 52;
  - 3.1, 3.1.1 and 3.1.2 on p. 42, and the Definitions of terms on p. 209.

  The Stage 1 passages are described correctly (OUT-005, 008, 009, 014, 016–022, 026, 028, 030, 031, 034, 035). No Stage 1 issue is worked around silently.

## Notes on frozen items (for the human)

None. `FROZEN_ITEMS.md` does not exist, and no item carries a FROZEN marker.
