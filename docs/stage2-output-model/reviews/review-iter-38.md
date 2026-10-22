# Review — iteration 38
VERDICT: REMARKS
REMARK_COUNT: 3
Reviewed version: v37
Date: 2026-10-22

## Summary

I reviewed v37 (`OUTPUT_MODEL.md` v37 with `RATIONALE.md` v36, unchanged in v37) on its own merits against Stage 1 v18 and the sources. I did not redo the v34 → v35 equivalence check.

The citations and source values hold:
- **Quotes.** Every quoted fragment of the 113 Q entries of `RATIONALE.md` is verbatim at the URL that its entry names and at its stated location. The only differences are white space and glyphs without a text mapping. No misquote was found.
- **Source data tables.** Every value matches its source: codes and labels, reference levels and spans, windows, evaluation rules, named criteria, control levels, ranges, bands and recall periods.
- **Metadata.** The citation metadata of S-101 to S-106 is correct. No newer version of a source changes an element; for example, no ICHD-4 has been published.
- **Evidence pointers.** Every pointer resolves to an entry whose sources support the value it is cited for.

The v37 change also holds: the catalogue's "Stated once for all rows" paragraph and the revised cells are consistent with their column definitions (checked by script).

The three remarks concern long-standing content that no earlier review raised: since v00 for R38-01 and R38-02, and since v07 for R38-03.
- **R38-01 (infidelity / rule stated per case).** Case C1-13 (OUT-029) requires acute-medication days per calendar month or 28-day period. It also requires them in one view with the frequency measures, for each headache type and for all types combined. Stage 1 asks for neither, and for the same measures over all types combined, C1-01, C1-04, C1-06 and C1-10 ask for neither. The model's own granularity rule (section 3.4) gives acute-medication days at any granularity.
- **R38-02 (rule stated per case / infidelity).** INV-049 (OUT-017) and INV-096 (OUT-036 (b)) require their series at every granularity a reader can select, weekly included. INV-118, INV-034, INV-044 and section 3.4 require one granularity of the diary's choice. Stage 1 asks for weekly values only where weekly granularity is clinically relevant (OUT-009) and for acute-medication days (OUT-015).
- **R38-03 (Stage 1 issue description).** ISS-10 counts four adult-only sources among the guidance that Stage 1 cites for OUT-018 and leaves out [S-002]. [S-002] is cited there and is a guideline for adults.

R38-01 and R38-02 are one class: the granularity, and the joint view, in which per-period content must be available is stated differently case by case. A fix that states the rule once and applies it to C1-13, INV-049 and INV-096 closes both.

## Verification coverage

### Method

All downloads, extracted texts and scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r38/`. Each source has its own folder under `dl/`, the extracted texts are in `txt/`, and the scripts are in `scripts/`, all run with `python3 -I`.

How the sources were fetched and read:
- Every Source URL of `RATIONALE.md` was fetched with `curl`.
- PDFs were extracted page by page with `pdftotext` (`-raw` and `-layout`).
- HTML pages had their markup stripped.
- PMC articles were read in their Europe PMC `fullTextXML` form, which model section 10 names. The PMC HTML pages returned a reCAPTCHA page for 7 of the 9 articles; for S-014 and S-023 the PMC HTML page was read as well.
- ICHD-3 p. 190 and the S-034 title page were rendered with `pdftoppm` and read.

The scripts:
- `parse_rat.py` split `RATIONALE.md` into 434 entries (113 Q, 228 D, 36 S, 12 W, 8 N, 2 X; no duplicate ID).
- `check_quotes.py` took every `Quote` field and every double-quoted string in the Text fields of the Q entries, split at `[...]`. It searched each fragment in the texts behind the entry's own URLs in three passes:
  1. exact, with white space, quote marks, dashes and ligatures normalised;
  2. with line-end hyphens joined;
  3. letters and digits only.

  It recorded the page or section of each hit and compared it with the stated location. Fragments not found in a listed source were searched in Stage 1 v18.

### Sources

| Source | URL used (as the entries give it) | Q entries | Fragments verified at the URL | Not found | Unreachable / notes |
|---|---|---|---|---|---|
| S-001 ICHD-3 | ichd-3.org PDF, 211 pp. (PDF page = printed page) | 28 | ~60 by script (pp. 8, 9, 12, 42, 105, 122–125, 139, 190, 209, 210)<br>+ 3 window fragments with "±"/"−" read on rendered p. 190: E-060/Q01 for A1.1.1 and A1.1.2, and INV-087/Q00 | 0 | "≥", "±", "−" are unmapped glyphs, as the entries state |
| S-002 | ihs-headache.org PDF | 2 | 3 (p. 12 = journal p. 1037) | 0 | — |
| S-005 | ihs-headache.org PDF | 2 | 2 (pp. 8–9) | 0 | — |
| S-007 | UCL Discovery PDF, 39 pp. | 3 | 3 (pp. 10, 22, 25) | 0 | — |
| S-008 | univaq PDF, 31 pp. | 10 | 18 (pp. 5–6, 9, 12, 13, 17); the "a ≥ 50%" / "a ≥ 30%" spacing matches the `-layout` text | 0 | — |
| S-010 | univaq PDF, 11 pp. | 13 | 18, all on p. 6 | 0 | — |
| S-011 | Europe PMC XML of PMC9188162 | 8 | 9; E-041/Q10 and Q11 are paragraphs 1 and 2 of the main Background | 0 | PMC HTML: reCAPTCHA |
| S-012 | Europe PMC XML of PMC9555163 | 1 | 1 | 0 | PMC HTML: reCAPTCHA |
| S-013 | Europe PMC XML of PMC7296705 | 2 | 2 | 0 | PMC HTML: reCAPTCHA |
| S-014 | Europe PMC XML and PMC HTML of PMC6734476 | 10 | 28 (Table 18 cells; "Scoring HALT"; HURT paragraph) | 0 | E-057/Q06–Q07 give "Additional file 18 ))" with a space; the XML has "18))". This is white space only, and the location note states it |
| S-015 | NICE CG150 Recommendations page and Overview page | 15 | 28 (1.3.9, 1.3.24–1.3.29, 1.3.39, 1.3.48; Overview population sentence) | 0 | "Last updated: 03 June 2025"; Overview "Last reviewed: 23 September 2026" |
| S-016 | SIGN 155 PDF, 64 pp. | 3 | 7 (PDF p. 7 = printed p. 1; PDF p. 20) | 0 | — |
| S-018 | AAN Clinician Summary PDF, 12 pp. | 4 | 5 (pp. 1, 7, 8; heading "When to Assess Treatment Efficacy" on p. 7) | 0 | — |
| S-022 | EMA draft PDF | 3 | 1 sentence (p. 11, after the margin line numbers were removed) | 0 | Stage 1 wording |
| S-023 | Europe PMC XML and PMC HTML of PMC9607711 | 1 | 4 | 0 | — |
| S-028 | NVN module page | 2 | 5 | 0 | — |
| S-030 | DHOS PDF, 86 pp. | 3 | 2 (p. 19) | 0 | — |
| S-032 | brainmed.com page | 1 | the 2 Stage 1 strings found on the page | 0 | the first attempt reset the connection (curl 35); the retry succeeded |
| S-033 | Minzdrav PDF 295_4, 92 pp. | 6 | 11 (pp. 1, 4, 39, 40, 53) | 0 | — |
| S-034 | Minzdrav PDF 169_3, 53 pp. | 6 | 8 in the text layer (pp. 3, 17, 32, 52)<br>+ "Возрастная группа" / "дети" read on the rendered title page (year 2024) | 0 | — |
| S-035 | noroloji.org.tr PDF, 92 pp. | 11 | 18 (pp. 2, 6, 7, 22, 23, 48, 57, 77, 82, 86) | 0 | — |
| S-042 | Europe PMC XML of PMC12279330 | 1 | 1 | 0 | PMC HTML: reCAPTCHA |
| S-101 | Europe PMC XML of PMC3057423 | 4 | 2 | 0 | PMC HTML: reCAPTCHA |
| S-102 | Europe PMC XML of PMC4406925 | 4 | 3 | 0 | PMC HTML: reCAPTCHA |
| S-103 | cincinnatichildrens.org PedMIDAS page | 3 | 12 (grading table and headings) | 0 | — |
| S-104 | Europe PMC XML of PMC183845 | 3 | 2 | 0 | PMC HTML: reCAPTCHA |
| S-105 | Joint Commission PDF, 9 pp. | 3 | 2 (P. 6/9; also P. 5/9)<br>The developers sentence is on P. 8/9; PDF metadata: created 2010-06-22, modified 2014-04-16, author Kurt Kroenke | 0 | — |
| S-106 | NICE TA260 chapter 2 and overview | 2 | 1 (para 2.1); published 27 June 2012, last reviewed 11 January 2016 | 0 | — |

**Totals.**
- 312 quoted fragments (2 further strings matched by the parser are not quotes).
- 248 verified in a listed source by script, and 3 more on rendered pages (2 ICHD-3 window fragments, 1 S-034 title-page fragment).
- 56 are Stage 1 wording, found verbatim in Stage 1 v18. Those of S-022 and S-032 were also found at their URLs.
- 5 are English translations, checked against their originals.
- No misquote; no quote that cannot be read at its URL.

**Translations.** All checked against the originals and faithful:
- E-041/Q15 (Dutch);
- E-041/Q16 to Q21 (Russian);
- E-041/Q22 to Q28, E-045/Q03 and Q04 (Turkish), and the E-041/Q00 heading "7. MİGRENDE GİRİŞİMSEL İŞLEMLER";
- ISS-10/Q00 (Russian).

**Metadata and versions.**
- PubMed `esummary` confirms authors, journal, volume, pages, DOI and PMC ID for S-101 (PMID 20819842), S-102 (25902814), S-104 (12914662) and the S-103 developer paper (11739822, 10.1212/wnl.57.11.2034).
- S-033 and S-034 are dated 2024 (Год утверждения), and S-035 August 2025.
- No ICHD-4 has been published. A web search finds only the ICHD-4 "Work in Progress 1" (Cephalalgia 2024) and an IHS workshop in September 2025 ([fis.uke.de](https://fis.uke.de/portal/en/publications/international-classification-of-headache-disorders4--work-in-progress-1(b2e76945-6b60-4911-9c1f-583c088a2d4c)/export.html), [ihs-headache.org](https://ihs-headache.org/en/about-ihs/standing-committees/classification/)).
- TA260 is not superseded. The CG150 recommendations used by the model are unchanged.

**Evidence pointers.**
- `evid.py`: all 122 `[S-NNN] <entry>` pairs in model Evidence fields resolve to an entry whose Source lines include that source.
- Every Rationale cell of the SD tables names entries whose Concerns list the row.

### Source data tables against their sources

Every formal cell agrees with its quote:
- **SD-IC.** The code labels on pp. 8, 9 and 12.
- **SD-CLS, SD-CMB and SD-FX-06.**
  - Levels: 10 days/month for every class, 15 for non-opioid analgesics, 10 for 8.2.6.
  - Span: "> 3 months".
  - `classesOf826` as in 8.2.6 criterion B.
- **SD-FX.**
  - Window: day 1 ± 2, days −2 to +3, no day 0, which gives 2 days before and 2 after. The `nextWindowDays` arithmetic gives days −2 and −1.
  - Remission: "must exceed three months".
  - Review window: 4–8 weeks. Follow-up: 12 months. Shortest monthly period: 28 days.
- **SD-ER-01 to SD-ER-18.** Every offset, anchor, timing, age, type and exclusion matches E-041/Q00 to Q30. I re-read NICE 1.3.24–1.3.29, AAN 14A/14B/14H, SIGN 4.1, EHF Q3, IHS Q2, NVN, Russian 3.3/7.1, the Russian paediatric flowchart, and Turkish Box 8, 3.6.3.9 and 7.3.
- **SD-RC-01 to SD-RC-06.**
  - NICE 1.3.28: 50 / 30 %. NICE 1.3.29: 30 %.
  - IHS Q6: the list items on p. 12 and the AHS MIDAS and HIT-6 thresholds on p. 13.
  - DMKG: eM 50 %, HIT-6 5 points, MIDAS 30 %.
  - Russian 7.1: 50 %.
- **SD-CL.** 0; < 4 for three months; 4–6; > 6, with insufficient control also below six days.
- **SD-IN and SD-GB.**
  - HIT-6: 36–78 with the four [S-101] bands.
  - MIDAS: grades I–IV with the [S-102] labels.
  - PedMIDAS: 0–10 / 11–30 / 31–50 / > 50.
  - HALT-90: 0–5 / 6–10 / 11–20 / ≥ 20.
  - Recall periods: 3 months for MIDAS, PedMIDAS and HALT-90; 1 month for HIT-6 and HALT-30. HALT-30 is ungraded; HURT has graded areas.
- **SD-SC and SD-SR.** HADS 0–21 per subscale, PHQ-9 0–27, GAD-7 0–21.
- **SD-ET.** 15 minutes for cluster headache.
- **SD-DF.** MUST for OUT-004 and SHOULD for OUT-007.

### Fidelity to Stage 1, requirement by requirement

For each requirement, I checked the Statement and its constraining Caveats against the catalogue row(s), case rows, elements and invariants that realise it, and each level against the Stage 1 part.

| OUT | Parts and strength | Realised by (main items) | Result |
|---|---|---|---|
| 001 | period stated MUST; frequency per month / 28 days MUST; equal-length comparison MUST; Caveat | E-003, E-005, INV-002, INV-003; C1-01, -02, -04, -06; INV-037, INV-038; `lengthDays` | ok |
| 002 | label SHOULD | INV-008 (`reports`), INV-111 | ok |
| 003 | SHOULD; SHOULD NOT | INV-011, INV-012, INV-121; C2-02 | ok |
| 004 | MUST; ICHD-3 definition MUST | C1-01; INV-125 (SD-DF-01) | ok |
| 005 | MUST for patients with migraine; label SHOULD | C1-02; INV-008 | ok |
| 006 | SHOULD; label | C1-03, C1-04; INV-008, INV-122 | ok |
| 007 | SHOULD; ICHD-3 definition | C1-05, C1-06; INV-125 (SD-DF-02) | ok |
| 008 | MAY | E-020 to E-022; C3-02; INV-104 (ISS-04) | ok |
| 009 | SHOULD series with markers; weekly where relevant | INV-034, INV-035, E-035 W2, INV-001 | ok; see R38-02 for weekly series asked elsewhere |
| 010 | SHOULD on a stated scale; comparison | C1-07, INV-032, INV-039 | ok |
| 011 | SHOULD, label; Caveat SHOULD NOT | C1-08, C3-03, C2-03 | ok |
| 012 | SHOULD across periods and per treated attack | C1-09, INV-076, `requiredOutcomes` | ok |
| 013 | MAY | E-019, E-024, E-027 | ok |
| 014 | MUST total, class, drug | C1-10, INV-024, INV-122, SD-CLS | ok; see R38-01 (C1-13 gives the same kinds another granularity) |
| 015 | SHOULD weekly | C1-11 | ok |
| 016 | MUST indicator; MUST prompt; MUST NOT diagnosis | INV-044 to INV-046, SD-CLS, SD-CMB; C3-04; C2-04 | ok |
| 017 | SHOULD | INV-049 to INV-051, E-039, C3-06 | **R38-02** (INV-049 at every granularity) |
| 018 | MUST; Caveat MUST NOT | INV-053, INV-055 to INV-059, E-040/E-043 W2, SD-ER; C2-05 | ok; see R38-03 (ISS-10 description) |
| 019 | SHOULD | INV-060, INV-061; ISS-13 | ok |
| 020 | MAY; SHOULD; SHOULD NOT | E-045, E-046, INV-062 to INV-064, INV-114, INV-116; C2-06, C3-07 | ok |
| 021 | MUST; SHOULD | INV-102, INV-068, INV-069 | ok |
| 022 | SHOULD | INV-103, INV-070, INV-112, E-049 | ok |
| 023 | SHOULD; Caveat | INV-071 to INV-076, SD-ET; C2-07 | ok |
| 024 | SHOULD | INV-077 to INV-079, INV-109, E-054/E-055 W2 | ok |
| 025 | MAY | E-056, INV-080 | ok |
| 039 | SHOULD | INV-066, INV-067, INV-109, INV-104 | ok |
| 026 | SHOULD | INV-081, INV-082, E-058, SD-IN, SD-GB | ok |
| 027 | SHOULD; comparison SHOULD | C1-12, INV-027 | ok |
| 028 | MUST; SHOULD; SHOULD NOT | INV-040 to INV-042; C2-08 | ok |
| 029 | MUST; SHOULD intensity | C1-13, C1-14, INV-122 | **R38-01** |
| 030 | MUST | INV-086, INV-087, INV-124, SD-FX-01/02 | ok |
| 031 | SHOULD | INV-088, INV-089, INV-124, SD-FX-07 | ok |
| 032 | MAY; caveats SHOULD | E-065, INV-110, C3-09 | ok |
| 033 | SHOULD; Caveat | INV-083, INV-085, SD-SR; C2-09, C3-10 | ok |
| 034 | SHOULD | INV-094, INV-104 | ok |
| 035 | SHOULD | INV-095, INV-105 | ok |
| 036 | SHOULD (a)–(d); Caveat | INV-096, INV-097, SD-ER-15, INV-055; C3-11 | **R38-02** (INV-096 at every granularity) |
| 037 | SHOULD NOT; SHOULD; SHOULD | INV-091; C3-12, E-033 W2, INV-092, INV-115; INV-093 | ok |
| 038 | SHOULD | C3-01, C3-05, C3-07 to C3-10; C2-01 | ok |

### Mechanical checks (scripts in `scripts/`)

| Check | Result |
|---|---|
| Headings and IDs (`model_ids.py`) | 67 E, 87 INV and 12 ISS headings; no duplicate. 0 unresolved E-, INV- or ISS- references in the model or `RATIONALE.md`. A withdrawn ID is referenced only in "Replaces" notes, section 9 and the ISS-07 sentence. 174 table rows (OC, C1–C3, SD-*): no duplicate, 0 unresolved row references. 364 model → RATIONALE entry references, all resolve. The only entries not cited by ID are the C1/C2/C3 D01 entries, which section 4.4 cites generically. |
| Evidence pointers (`evid.py`) | 122 pairs; 0 bad. Every SD-row Rationale entry names the row under Concerns. |
| Traceability and catalogue (`trace.py`) | 39 rows in Stage 1 order. The Elements and Invariants columns equal the union of the Realises fields (0 differences). The catalogue-rows column equals the rows whose Realises name the requirement. Every OUT in a row's Realises is realised by an item named in the row. The elements without a row are exactly those that section 4.2 lists. The coverage lines naming INV-104 (OUT-008) and INV-069 (OUT-012) outside the columns are known (reviews 36, 37). |
| Catalogue cells after v37 (by hand against the column definitions) | For every row, "def." equals the definitional invariants whose Conformance field names an element of the row, minus INV-006, INV-121, INV-122 and INV-123. W2 markers, C3 cases, C2 cases, SD-DF rows and INV-060, INV-078 and INV-087 are each named in their own row. The rows named in the section 4.2 paragraph (INV-003 in OC-01, INV-008 in OC-03, INV-011 in OC-04) are the only ones that name a stated-once invariant. |
| Audience column (`audience.py`) | Every "OUT-NNN: …" cell equals the Stage 1 Audience line verbatim. |
| Declared names (`names.py`) | Every identifier used in `omn` blocks and formal cells is declared, a primitive, a bound variable or a text literal. `refs` is defined in section 2.5. No bare `ctx` inside a defined predicate or function. |
| Attribute typing and composition | Every SHOULD or MAY attribute, and every MUST attribute with `when`, has an `opt`, `set` or `seq` type. Element types are mentioned without `→` only in `Output.views` and `View.content`. Placement markers are on `→R` types only, and the 6.0 index matches the declarations. |
| Case tables | Keys pairwise distinct: C1 (14), C2 (9), C3 (12) and every SD table. Every component of `EvaluationRule`, `ResponderCriterion` and `GradeBand` has a column. Every `table N` reference resolves. |
| Levels | 11 MUST invariants (INV-003, INV-037, INV-040, INV-044, INV-055 to INV-057, INV-059, INV-068, INV-086, INV-102), each realising a MUST part. C1 `must` cases cite MUST parts, `should` cases SHOULD parts. C2-04 and C2-05 are `mustNot`, the other C2 cases `shouldNot`. C3-04 is `must`, C3-02 `may`. SD-DF-01 is `must`, SD-DF-02 `should`. INV-091 is SHOULD NOT. Exceptions in substance: R38-01 and R38-02 (strength in granularity and co-presence, not level). |
| Use of the selected granularity (`grep c.granularity`) | `tiles(…, c.granularity)` under an unrestricted `∀ c ∈ Ctx` occurs only in INV-049 and INV-096. INV-034, INV-044 and INV-118 quantify `∃ g` first (R38-02). |
| Scope sweep | The terms enter/record/input/answer/stored/storage/database/JSON/XML/FHIR/algorithm/computed/derive/obtained from/questionnaire/entry/persist/file occur only in these places: exclusion statements, notation prose, derived-attribute notes that leave the derivation out, source titles and search-log entries, the HALT-30 quote ("records days affected"), and E-018/Q02's note that the [S-010] day definitions "classify a day from what the patient reports and are not quoted". No formula, threshold or relation takes input data. Every threshold and formula shown with an output (overuse levels, span, windows, offsets, criteria, control levels, bands, ranges) is present. |
| Date arithmetic of worked examples | E-042/W01–W02, INV-055/W01, INV-049/W01, INV-079/W01 (41 and 294 days), E-063/W01 (42 and 143 days), E-007/D01 (67 days), INV-105/D02 (43 days): all correct. |

## Remarks

### R38-01 Infidelity to Stage 1 / rule stated per case: case C1-13 asks acute-medication days per calendar month or 28-day period, and in one view with the frequency measures, which neither Stage 1 nor the combined-scope cases ask
- Item(s): C1-13 (table C1, section 4.4; INV-118); OC-35; E-029 Conformance ("per headache type MUST (INV-118, C1-13)"); `RATIONALE.md` INV-118/D02 and C1-13/D01; section 3.4. Related: C1-01, C1-04, C1-06, C1-10; ISS-04; ISS-09.
- Problem:
  - **What C1-13 requires.** For a subject who has or may have two or more headache types, each pair (scope, kinds) must be shown for every period of the selected time range: `ppGranularities(oc35, must) = MonthlyKind` and `q.2 = {HeadacheDays} ∪ medicationKinds(c) ∪ {K ∈ {ModerateSevereHeadacheDays, AttackCount} | provides(K)}`. `reportedTogether` (section 3.4) means one view, one series and one granularity g ∈ MonthlyKind for all these kinds. The scopes are every possible type and `allTypes`. So, at MUST:
    - (i) acute-medication days (total, per class, per drug) per calendar month or 28-day period, for each type and combined;
    - (ii) these in the same view and series as headache days, and, where provided, moderate/severe headache days and attacks;
    - (iii) one existential granularity shared by all these kinds.
  - **What Stage 1 asks.**
    - OUT-029 (MUST): "present frequency and acute medication outputs separately for each headache type (for example migraine and tension-type headache), as well as combined". It names no granularity and no co-presence of frequency with medication outputs.
    - The granularity of the frequency outputs comes from OUT-001, which section 3.4 reads as "the frequency measures of OUT-004 to OUT-007".
    - Acute-medication days are OUT-014 outputs, "per reporting period". For these, section 3.4 states the model's own rule: "Where Stage 1 says 'per reporting period' without naming a granularity, the availability invariant requires reportedPerPeriod for contexts of at least one granularity".
    - No Stage 1 part asks for frequency and acute-medication outputs per headache type in one presentation. Contrast OUT-021: "present together".
  - **The same measures are stated differently per case.**
    - C1-10 (OUT-014, MUST) gives acute-medication days over all headache types combined with `ppGranularities = Granularity`. A diary may provide them per calendar week only.
    - C1-01, C1-04 and C1-06 give headache days, moderate/severe headache days and attacks over all types combined, each as its own case, with its own existential granularity and its own view. INV-118/D03 explains why: "one existential quantifier over both would strengthen the rule".
    - C1-13 repeats these combined-scope kinds (`q.1 = allTypes`) jointly, in one view, monthly. It does so only for subjects with two or more possible types.
    - So the same outputs (for example combined acute-medication days) are MUST per calendar month or 28-day period, together with headache days, when the subject has or may have two headache types. For a subject with one type they are MUST at any granularity and in any view. Nothing in Stage 1 makes the number of headache types bear on the granularity or co-presence of acute-medication days.
  - **The consequence: a narrowing.** Take a subject with migraine and tension-type headache who uses one triptan. A diary shows:
    - headache days per calendar month for each type and combined, in a chart;
    - acute-medication days (total, triptans, sumatriptan) for each type and combined per calendar week, in a table.

    It meets OUT-029, OUT-014 and OUT-001. It fails C1-13 at MUST: no view shows a monthly series with both. For a migraine-only subject, the same diary is MUST-conformant under C1-01 and C1-10. PROCESS.md section 4: "A model element may be marked stronger than one Stage 1 statement part only when another Stage 1 statement part of at least that strength directly requires it". Section 9: "an invariant that excludes an output Stage 1 permits".
  - **Not a reversal.**
    - C1-13 is v34 INV-028 verbatim, and v00 already had `MonthlyKind` and `reportedTogether`. R01-06 / fix 01 added the per-class and per-drug kinds (the "total-only" reading); the fix below keeps them.
    - No review, fix or oscillation check discussed the granularity or co-presence of these kinds. I searched every loop file for INV-028 and C1-13. Fix 10's level sweep ("INV-028 | … | match") and fix 11's co-presence sweep ("Each places its items in one view") checked that the predicate does what its Reading says, not whether Stage 1 asks for it.
    - No watch point names INV-028 or C1-13.
- Evidence:
  - Stage 1 OUT-029 Statement and Strength ("MUST for frequency and acute medication outputs per headache type"); OUT-014 Statement ("per reporting period"); OUT-001 Statement; OUT-009 ("frequency measures (OUT-004 to OUT-007)"); OUT-021 ("MUST present together").
  - Model:
    - section 3.4, paragraph after the `reportedTogether` block;
    - table C1 rows C1-01, C1-04, C1-06 and C1-10 (`Granularity`) against C1-13 (`MonthlyKind`, one pair per scope with all kinds);
    - INV-118 Notes ("Each case has its own existential granularity: the two measures of C1-04 and C1-06 … are separate cases");
    - `RATIONALE.md` INV-118/D03 ("one existential quantifier over both would strengthen the rule") and INV-118/D02.
- Required change (state the per-period rule once for every type scope):
  - **(a) Preferred.** Restate C1-13 as the per-type extension of the combined-scope cases.
    - The frequency measures per headache type: headache days, and, where provided, moderate/severe headache days and attacks. They stay per calendar month or 28-day period (OUT-001), each with its own existential granularity, as C1-01, C1-04 and C1-06 have.
    - The acute-medication days per headache type (total, per class and per drug, together, as OUT-014 says "together with the total") go in a case with `ppGranularities = Granularity`, as C1-10 has.
    - No co-presence of frequency with medication outputs is asked.
    - The combined scope is already covered by C1-01 to C1-06 and C1-10, so the new cases need only the per-type scopes.
    - Update OC-35, E-029 Conformance and INV-118/D02. INV-122 is unaffected, since it binds only values shown in one view.
  - **(b) Alternative.** If the fixer reads OUT-029 as asking for one presentation per headache type in which frequency and acute-medication outputs are shown together, per calendar month or 28-day period, this reading is not stated by Stage 1:
    - record it in section 8, as a new issue or by extending ISS-09, which already concerns "which acute medication outputs" OUT-029 means, and point to it from C1-13;
    - and state in section 3.4, with ISS-04, why acute-medication days are monthly MUST for these subjects only, or make them monthly in C1-10 as well. ISS-04's "For the human" names only the OUT-008 measures and the aura counts of OUT-013 as candidate frequency outputs.
  - Either way, apply the result together with R38-02, which concerns the same class (the granularity of per-period availability).

### R38-02 Rule stated per case / infidelity to Stage 1: INV-049 and INV-096 require their series at every granularity a reader can select, while the generic per-period rule requires one granularity of the diary's choice
- Item(s): INV-049 (first conjunct), INV-096 (second conjunct); section 3.4; INV-118, INV-034, INV-044 (for comparison); C1-12. Related: E-039, INV-050 (unchanged by this remark).
- Problem:
  - **Two forms of the same rule.** "Values for every period of the selected time range" is written in two ways:
    - **One granularity of the diary's choice.** INV-118 (all of table C1), INV-034 and INV-044 quantify `∃ g ∈ … • ∀ c ∈ Ctx • c.granularity = g ⇒ … tiles(sr, c.timeRange, c.granularity) …`. Section 3.4 states this as the model's reading: "the availability invariant requires reportedPerPeriod for contexts of at least one granularity".
    - **Every granularity.** INV-049 and INV-096 quantify `∀ c ∈ Ctx` with no granularity restriction and require `tiles(sr, c.timeRange, c.granularity)`. Every admissible context of every granularity (calendar month, 28-day period, calendar week; INV-001 admits all three) needs a series of that granularity. These are the only two places where a series is tied to the selected granularity without a preceding `∃ g`.
  - **The per-case statements differ for the same values.**
    - C1-12 (OUT-027, SHOULD) asks for `fiDays(paidWorkOrSchool, affected)` per period at one granularity: `ppGranularities(oc32, should) = Granularity`.
    - INV-096 (OUT-036 (b), SHOULD) asks for the same day counts, or missed and impaired school days, and caregiver impact, for children at every granularity. That includes per calendar week for every child, whatever the clinical relevance of weekly values.
    - INV-049 (OUT-017, SHOULD) asks the follow-up series of headache days and acute-medication days at every granularity, including weekly series for every subject withdrawing from overused medication.
  - **Stage 1 asks for less.**
    - OUT-036 (b): "report school days missed or impaired and the impact on parents or caregivers".
    - OUT-017: "show headache days and acute medication days from the start of withdrawal onward … and SHOULD allow continued monitoring of acute medication use over the following year".
    - Neither names a granularity.
    - Stage 1 asks for weekly values only "Where weekly granularity is clinically relevant (tension-type headache, cluster headache, early onset of effect)" (OUT-009; the model's `weeklyGranularityRelevant`, INV-034 second conjunct) and for acute-medication days (OUT-015, C1-11).
  - **Examples.**
    - A child with migraine. A diary reports school days and caregiver impact per calendar month and per 28-day period, not per calendar week. It meets OUT-036 (b), but fails INV-096 for every weekly context.
    - A withdrawal started on the first day of a calendar week. A diary offers the follow-up series in 28-day periods only. It meets OUT-017, but fails INV-049 for the weekly contexts whose time range starts on that day.

    Both breaches are deviations from SHOULD constraints that Stage 1 does not make. The same diary meets C1-12 for the functional-impact days of an adult.
  - **Watch points.**
    - INV-049 is a watched block: check 08 wp 4, check 12 wp 5, check 24 wp 5, check 16. The watched content is INV-050's start tie and `fillsPeriod`, the removed end tie, the running-follow-up conjunct (v11) and "every start of withdrawal" (v12).
    - This remark touches none of them. It concerns only the quantification of the series granularity in INV-049's first conjunct, unchanged since v00 and never discussed. Review 04 noted that "the 28-day and weekly contexts cover OUT-017" as coverage, not as a requirement to support every granularity.
    - INV-096's age reading (check 12) is not touched.
    - Fix 11's per-period sweep listed OUT-036 (b) among the "per reporting period" outputs, together with INV-026 (now C1-12), without noting the different quantifier.
- Evidence:
  - INV-049 first conjunct: `∀ c ∈ Ctx; ws ∈ c.subject.withdrawalStart • (c.timeRange.from = ws ∧ … ⇒ ∃ o … ∃ v … • … sameSpan(v.covers, c.timeRange) ∧ ∃ sr ∈ v.series • tiles(sr, c.timeRange, c.granularity))`.
  - INV-096 second conjunct: `∀ c ∈ Ctx • … (childOn(c, c.timeRange.from) ⇒ ∃ o … ∃ v ∈ o.views; sr ∈ v.content ∩ Series • tiles(sr, c.timeRange, c.granularity) ∧ …)`.
  - INV-118: `∃ g ∈ ppGranularities(r, l) • ∀ c ∈ Ctx • c.granularity = g ⇒ …`; INV-034 and INV-044 likewise; section 3.4 (quoted above); C1-12.
  - Stage 1 OUT-009, OUT-015, OUT-017 and OUT-036 Statements (quoted above).
- Required change (fix the class with R38-01: state once how the granularity of per-period availability is chosen, and apply it):
  - **INV-096.** Quantify the series conjunct as INV-118 does: `∃ g ∈ Granularity • ∀ c ∈ Ctx • c.granularity = g ∧ childOn(c, c.timeRange.from) ⇒ …`. Alternatively, move school days and caregiver impact for children into table C1 as cases of OC-42 with an age condition in `ppRequired`, as C1-02 carries `hasType`. The PedMIDAS conjunct is unaffected.
  - **INV-049.** Keep a follow-up view for every time range that begins on a start of withdrawal (R11-03's guarantee, which needs time ranges that can begin on any day), and drop the tie of its series to the selected granularity. Two ways:
    - require only `v.withdrawalStart = ws ∧ sameSpan(v.covers, c.timeRange)` in the first conjunct, and leave the series to E-039 (`series` SHOULD when `wholePeriodFrom`) and INV-050 (start tie and `fillsPeriod`, unchanged);
    - or quantify `∃ g` over a granularity whose periods can begin on every start of withdrawal.
  - Leave unchanged the second (running-follow-up) conjunct, INV-050, E-039 and every start of withdrawal.
  - Update the Readings of INV-049 and INV-096, and `RATIONALE.md` INV-049/D01 and INV-096/D01.

### R38-03 Stage 1 issue handling: ISS-10 misdescribes the guidance that Stage 1 cites for OUT-018 (four adult-only sources; [S-002] omitted)
- Item(s): ISS-10 (section 8, "Stage 1" paragraph).
- Problem:
  - **What ISS-10 says.** "Every guidance that Stage 1 cites for OUT-018 concerns preventive treatment of migraine, and four of them concern adults only (AAN/AHS 2026, SIGN 155, the EHF 2022 guideline and the Russian clinical recommendations for adults). NICE CG150 covers people aged 12 years and older …; the IHS 2024 recommendations, the NVN module and the Turkish protocol also address children (E-041)."
  - **What Stage 1 cites.** OUT-018's Evidence cites nine sources: [S-015], [S-002] (twice), [S-018], [S-016], [S-011], [S-008], [S-033], [S-028] and [S-035]. Its Evidence basis names [S-002] as "international trial-methodology guideline (IHS)".
  - **The omission.** ISS-10 accounts for eight of the nine and leaves out [S-002]. [S-002] is "Guidelines of the International Headache Society for controlled trials of preventive treatment of migraine attacks in episodic migraine in adults" (Stage 1 section 5). It also concerns preventive treatment of migraine, and it concerns adults only. So "four of them concern adults only" is wrong as stated.
  - **Why it matters.** The human decides ISS-10 on this description of the population coverage of OUT-018's sources. PROCESS.md section 9 lists Stage 1 issue handling among the remarks, and section 8 entries must describe correctly the passages they cite.
  - **How it arose; not raised before.**
    - v06 read "Every guidance that OUT-018 quotes *for these time points* …". That scope excludes [S-002], which names no time point, so the count was right.
    - Fix 07 (R07-01, ISS-10 rewrite) widened it to "Every guidance that Stage 1 cites for OUT-018" without changing the count and without stating a reason.
    - The sentence has been unchanged since v07, and no review commented on it.
    - No watch point names ISS-10's text.
- Evidence:
  - Stage 1 OUT-018 Evidence ([S-002] "The primary endpoint in controlled trials of preventive treatment of episodic migraine should be the change from baseline in migraine days per unit time." and the recommendation b quote), Evidence basis ("international trial-methodology guideline (IHS)"); Stage 1 section 5, S-002 citation.
  - `RATIONALE.md` E-041/D01 itself lists [S-002] among the sources: "The IHS trial guideline [S-002], also cited in OUT-018, names durations and analysis periods of controlled trials, not time points for evaluating a person's treatment."
- Required change: correct the ISS-10 sentence. Either:
  - count [S-002] ("five of them concern adults only (…, and the IHS trial guideline for episodic migraine in adults [S-002], which names no evaluation time point for a person's treatment, E-041/D01)"); or
  - restrict the sentence again to the guidance that names the time points ("that OUT-018 quotes for these time points", the v06 scope), and say so.

  No formal change.

## Checked and not raised

- **Section 4.2 "Stated once for all rows" (v37).** Every claim checked against the predicates:
  - INV-003, INV-006, INV-008, INV-011 and INV-122 quantify over every view, INV-121 over every per-period value, and INV-123 over every element.
  - The examples of placement through shared period atoms hold: INV-038 and INV-056 values, the INV-045 basis, and the INV-115 components.
  - The bearers of C2-01, C2-02, C2-05, C2-07 and C3-01 are as stated.
- **Section 6.0 "Not marked" list.** It does not name `OutcomeSummary.summary`, `MedicationOveruseIndicator.basis`, the values and changes of comparisons, or `ClusterAttackRate.bout`.
  - Their placement follows from INV-003 through shared period atoms (section 2.5), or from E-051 `outcomes` (W2) with INV-074 (`os ∈ os.summary.outcomes`).
  - The cluster references are excluded on purpose (E-062/X01).
  - The list does not claim to be exhaustive. Review 37 checked the basis and the comparison values.
- **R-MCF clause 3, "admitted only where the context makes the selection".** A `PeriodComparison` or `ClinicianSummary` that matches no selection is admitted, but it is not content *for* a selection: `matchesSelection` and the previous-consultation span presuppose the selection. Read so, the clause holds; INV-080 ties scheme windows formally. Not raised.
- **DMKG/ÖKSG/SKG.** S-023 also gives a chronic-migraine statement: 50 % in trials, "in der Praxis" 30 %.
  - The model names only "DMKG/ÖKSG/SKG consensus statement (episodic migraine)", the criterion Stage 1 quotes.
  - OUT-020 names criteria as examples.
  - A label under this name for a treatment of chronic migraine is forced "non-responder". This is the settled `set1` behaviour (check 32, wp 2).
- **IHS Q6.** The "Essential" level (continue with meaningful subjective improvement) and Q5's stopping rule (fewer than four monthly migraine days over three months) are not modelled as named criteria. The named criterion is the Q6 "Optimal" list, which matches p. 12 item by item.
- **NICE CG150 1.3.25** (rimegepant) is a CGRP inhibitor, which `ruleNice1328`/`critNice1328` (`cgrpInhibitor`) cover. Consistent.
- **Single-month control-level labels.** With 1–3 days in one evaluated month, only "insufficient control" is admitted, because optimal control needs three months (SD-CL). This follows [S-010] (E-046/D06), and labels are optional. Not raised.
- **Cluster 24-hour outcomes with the 15-minute time point** (review 01, review 14) and **"baseline administration" as any earlier administration** (since review 01). Settled; no new evidence.
- **Whitespace and glyph differences in quotes:**
  - "Additional file 18 ))" (E-057/Q06–Q07), where Europe PMC XML has "18))" and the location note states the rendering;
  - "≥" spacing in the [S-008] quotes, which matches the `-layout` text;
  - the ICHD-3 "≥"/"±"/"−", verified on rendered p. 190.

  None changes a word or a number.
- **Prose claims checked against their predicates:**
  - E-012 (`scopeFor` picks exactly one scope);
  - E-067 (`courseOverlaps` and `courseNotOutside` agree under a stated start);
  - section 3.8 clause 2 (`courseBegunBy` equals "on or after the start" under INV-001);
  - E-043/D01 (the changes of a comparison lie in its view, by W2 and the one-view rule);
  - INV-045/D01 (four monthly periods: plusMonths(first.start, 3) ≤ last.end, and not from the second);
  - INV-087 and INV-124 Readings;
  - INV-088 with INV-073 (`scopeFor` implies `onlyOfType`);
  - INV-003/D02 (the agreeing values).

  All hold.
- **Stage 1 issues ISS-01 to ISS-09, ISS-11 to ISS-13.** Founded, with correct locations and descriptions:
  - ISS-03's list, checked against every Stage 1 Statement that mentions migraine;
  - ISS-02: "simple analgesics" occurs only on ICHD-3 p. 139;
  - ISS-12: pp. 42 and 209;
  - ISS-13: no monthly period lies within a compared period shorter than 28 days.

  ISS-09's Group D description without OUT-017 is settled (reviews 25b, 31).
- **Watch points of the check after iteration 36.**
  - R38-01: C1-13 is not named by any watch point.
  - R38-02: see the remark. It keeps every watched INV-049/INV-050 tie.
  - R38-03: ISS-10 is not a watched text item.

  No remark reverses an earlier fix or touches watch points 1 to 8, 10 or 12.

## Notes on frozen items (for the human)

None. No item is frozen: `FROZEN_ITEMS.md` does not exist, and the model has no "Status: FROZEN" marker.
