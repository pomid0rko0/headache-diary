# Review — iteration 36
VERDICT: REMARKS
REMARK_COUNT: 3
Reviewed version: v35
Date: 2026-10-22

## Summary

v35 is the restructured model: the output catalogue, case tables C1–C3, generic invariants INV-118 to INV-125, placement markers (rule W2), R-MCF, the source data tables, and `RATIONALE.md`, corrected after the equivalence check. I reviewed it on its own merits against Stage 1 v18 and the sources. I did not redo the equivalence check.

The formal content holds up:
- every quote in `RATIONALE.md` is verbatim at its source;
- every value of the source data tables matches its source;
- every level of the catalogue cases and of the invariants follows the strength of its Stage 1 statement part;
- the generic invariants and case tables are well formed;
- the scope sweep is clean.

The three remarks concern bookkeeping and text that the restructuring left wrong:

- **R36-01 (citation defect).** Thirteen `RATIONALE.md` entries give the PubMed abstract page as the URL of [S-010]. Their quotes come from the full text, p. 6, which Stage 1 lists under a second URL. Three [S-015] entries have the same problem: they quote the NICE Overview page but give the Recommendations URL.
- **R36-02 (traceability).** Two kept invariants lost conjuncts in v35, but their Conformance element lists and Realises fields still describe the moved conjuncts:
  - INV-033 still cites OUT-011, OUT-027 and OUT-036, and E-024, E-030 and E-031;
  - INV-031 still cites OUT-006, and E-017 and E-021.
  
  So four traceability rows are wrong, and the invariants contradict the Conformance fields of the elements. Related leftovers in the same class: the Evidence of INV-031, INV-075 and INV-079; the section 9 row of INV-036; and catalogue row OC-08.
- **R36-03 (prose overclaim).** Two sentences misstate the formal text:
  - Section 2.5 says that every placement of a non-period reference is a W2 marker. INV-060, INV-078 and INV-087 state placements that are not markers, and section 6.0 itself lists two of them.
  - Section 4.2 calls `DayCount` abstract, but it is a concrete element type.

## Verification coverage

### Method

Downloads and scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r36/` (`dl/` holds one folder per source; `scripts/` holds the scripts, all run with `python3 -I`). Every source was fetched with `curl`:
- PDFs were extracted with `pdftotext` (`-layout` and `-raw`, page by page);
- PMC articles were read in their Europe PMC `fullTextXML` form, the place model section 10 names;
- web pages had their markup removed.

`parse_rat.py` split `RATIONALE.md` into 432 entries (111 Q). `check_quotes.py` then took every `Quote` field and every double-quoted string in a Q entry's Text field (310 quoted items), split each at `[...]`, and searched for every fragment in each source that the entry names, in three passes:
1. exact, with only whitespace, ligatures, quote marks and dashes normalised;
2. with line-end hyphens joined;
3. letters and digits only, for glyphs without a text mapping.

Every fragment found only by pass 3 was read on the page. Every fragment not found was classified by hand. Stated locations (page, section, item order) were compared with the page or section where each fragment was found.

### Sources

| Source | URL used (as in the entry) | Q entries | Fragments checked | Verified verbatim | Not found | Unreachable / notes |
|---|---|---|---|---|---|---|
| S-001 ICHD-3 | ichd-3.org PDF (211 pp.) | 28 | 62 | 62: 40 exact, 7 after line-end joins, 12 with glyph or line-break normalisation, 3 on the rendered p. 190 (`pdftoppm`; "±", "−" and "+" have no text mapping) | 0 | — |
| S-002 | ihs-headache.org PDF | 2 | 3 | 3 | 0 | — |
| S-005 | ihs-headache.org PDF | 2 | 2 | 2 | 0 | — |
| S-007 | UCL Discovery PDF (39 pp.) | 3 | 3 | 3 | 0 | — |
| S-008 | univaq PDF (31 pp.) | 9 | 18 | 18 (E-045/Q01 differs only in spacing around "≥"; the E-008/Q00 fragment is the S-008 Q6 sentence, p. 12) | 0 | The first download timed out; the retry succeeded |
| S-010 | **entries give `https://pubmed.ncbi.nlm.nih.gov/39980456/`**; checked against Stage 1's full-text URL (univaq PDF, 11 pp.) and against the PubMed abstract (E-utilities `efetch`) | 13 | 18 | 18 on PDF p. 6; **0 of them in the PubMed abstract** (R36-01) | 0 | The PubMed HTML page returned a cookie wall (HTTP 203); the abstract was read through E-utilities |
| S-011 | PMC9188162 (Europe PMC XML, PMC page) | 8 | 8 | 8 | 0 | — |
| S-012 | PMC9555163 | 1 | 1 | 1 | 0 | The PMC HTML returned a bot-check page; Europe PMC XML used |
| S-013 | PMC7296705 | 2 | 2 | 2 | 0 | as S-012 |
| S-014 | PMC6734476 | 10 | 24 + 5 short table cells | all; Table 18 rows read in the XML (0-5 I, 6-10 II, 11-20 III, ≥20 IV) | 0 | as S-012 |
| S-015 | NICE CG150 Recommendations page and Overview page | 15 | 28 | 28 (the 1.3.26 and 1.3.9 sentences differ only by an HTML space before ".") | 0 | The population phrase is on the Overview page only (R36-01). The Overview page now reads "Last reviewed: 23 September 2026 – We added links to relevant technology appraisal guidance"; recommendations 1.3.24–1.3.29 and 1.3.48 are unchanged ("Last updated: 03 June 2025") |
| S-016 | SIGN 155 PDF (64 pp.) | 3 | 5 | 5 (section 1.2.1 on PDF p. 7 = printed p. 1) | 0 | — |
| S-018 | AAN clinician summary PDF (12 pp.) | 4 | 5 | 5 (14B p. 7 and 14H p. 8, level B) | 0 | — |
| S-022 | EMA draft PDF | 3 | 1 | 1 (lines 383–384, p. 11, with the margin line numbers removed) | 0 | — |
| S-023 | PMC9607711 | 1 | 4 | 4 | 0 | — |
| S-028 | NVN module page | 2 | 6 | 6 | 0 | — |
| S-030 | DHOS PDF | 3 | 2 | 2 | 0 | — |
| S-032 | brainmed.com reprint | 1 | 3 Stage 1 strings | 3 | 0 | The first two attempts reset the connection (curl 35); the third succeeded |
| S-033 | Minzdrav PDF 295_4 (92 pp.) | 6 | 11 | 11 (pp. 1, 39, 40, 53) | 0 | — |
| S-034 | Minzdrav PDF 169_3 (53 pp.) | 6 | 7 | 7: pp. 17 and 52 in the text layer; title page p. 1 rendered and read ("Возрастная группа дети") | 0 | — |
| S-035 | noroloji.org.tr PDF (92 pp.), full URL | 11 | 18 | 18 (PDF pp. 7, 23, 48, 57, 77, 82–86; Kutu 8 item order checked: criterion = 2nd, "Yeterli süre" = 7th) | 0 | — |
| S-042 | PMC12279330 | 1 | 1 | 1 | 0 | — |
| S-101 | PMC3057423 | 4 | 2 | 2 (Methods > Data sources) | 0 | — |
| S-102 | PMC4406925 | 4 | 3 | 3 (Methods > Migraine-related disability) | 0 | — |
| S-103 | cincinnatichildrens.org PedMIDAS page | 3 | 12 | 12 (footer © 2026) | 0 | — |
| S-104 | PMC183845 | 3 | 2 | 2 (section "Construction of the HADS") | 0 | — |
| S-105 | Joint Commission PDF (9 pp.) | 3 | 2 | 2 (P.6/9, "Use of some screeners…"; also on P.5/9); developers sentence on P.8/9; PDF metadata: created 2010, modified 2014, author Kurt Kroenke | 0 | — |
| S-106 | NICE TA260 chapter 2 and overview | 2 | 1 | 1 (para 2.1, last sentence); published 27 June 2012, last reviewed 11 January 2016 | 0 | — |
| Stage 1 wording | `OUTPUT_REQUIREMENTS.md` v18 | — | 53 | 53 (Statement, Rationale or Evidence-basis fragments that the entries attribute to Stage 1) | 0 | — |

Totals: 111 Q entries; 310 quoted items; 244 source fragments found by script, plus 6 more read by hand (3 glyph fragments on the rendered p. 190, the S-034 title page, the S-022 lines with margin numbers, and the S-008 fragment of E-008/Q00); 53 Stage 1 fragments; 7 translation strings. No misquote. The only URL defects are those of R36-01.

**Translations.** All checked against the original: E-041/Q15 (Dutch), Q16–Q21 (Russian), Q22–Q28, E-045/Q03 and Q04 (Turkish), ISS-10/Q00 (Russian). All are faithful. The short heading fragments in E-041/Q00 are not translated, but the entry's own English text says what they show (Checked and not raised).

**Metadata.**
- PubMed E-utilities `esummary` confirms the citation, DOI and PMC ID of each journal source:
  - S-101: PMID 20819842, DOI 10.1177/0333102410379890, PMC3057423;
  - S-102: PMID 25902814, DOI 10.1186/s10194-015-0503-y, PMC4406925;
  - S-104: PMID 12914662, DOI 10.1186/1477-7525-1-29, PMC183845;
  - the S-103 developer paper: PMID 11739822, DOI 10.1212/wnl.57.11.2034.
- Types and gradings are as stated.
- Newer versions: no ICHD-4 has been published (web search: ICHD-4 alpha 2020, "Work in Progress 1" 2024, an IHS workshop in 2025); TA260 has not been superseded; the review note on CG150 changes no recommendation that the model uses.

**Source data tables against their sources.** Every formal cell was compared with its quote:
- SD-IC: the ICHD-3 code labels on pp. 8, 9 and 12;
- SD-CLS and SD-CMB: 10 or 15 days/month and > 3 months, 8.2.1–8.2.8 (pp. 122–125);
- SD-FX: the A1.1 window (day 1 ± 2, days −2 to +3, p. 190), the remission of more than 3 months (p. 209), 4–8 weeks (NICE 1.3.48), 12 months and 28 days;
- SD-ER-01 to SD-ER-18: offsets, anchors, timing, ages, types and exclusions against E-041/Q00–Q30;
- SD-RC-01 to SD-RC-06: thresholds 50/30 % (NICE 1.3.28), 30 % (1.3.29), IHS Q6 (50 %; 30 % for the chronic alternative; MIDAS ≥5 points for baseline 11–20 and ≥30 % for baseline ≥20; HIT-6 ≥5 points), DMKG (50 %, HIT-6 5 points, MIDAS 30 %), Russian 7.1 (50 %);
- SD-CL: 0; < 4 for three months; 4–6; > 6, which can also hold below 6;
- SD-IN, SD-GB: HIT-6 36–78 with bands ≤49, 50–55, 56–59, 60–78; MIDAS bands 0–5, 6–10, 11–20, ≥21 with the [S-102] labels; PedMIDAS 0–10, 11–30, 31–50, > 50; HALT-90 0–5, 6–10, 11–20, ≥20 (overlap at 20 as printed); recall periods 3/1/3/1/3 months for MIDAS, HIT-6, HALT-90, HALT-30 and PedMIDAS; HALT-30 ungraded;
- SD-SC, SD-SR: HADS 0–21 per subscale, PHQ-9 0–27, GAD-7 0–21;
- SD-ET: 15 minutes for cluster headache;
- SD-DF: ICHD-3 "headache days" at MUST (OUT-004) and "frequency of attacks" at SHOULD (OUT-007).

All agree.

### Fidelity to Stage 1, requirement by requirement

Each row was checked against the Statement and its constraining Caveats, with levels against the strength of each statement part (PROCESS.md section 4), and against the catalogue row(s), case-table rows and invariants.

| OUT | Parts and strength | Realised by (main items) | Result |
|---|---|---|---|
| 001 | period stated MUST; per month or 28 days MUST; equal-length comparison MUST; Caveat (lengths visible) | E-003 `covers`, E-005, INV-002, INV-003; C1-01, -02, -04, -06; INV-037, INV-038; `lengthDays` | ok |
| 002 | label SHOULD | INV-008 (`reports`), INV-111 | ok |
| 003 | indicator SHOULD; validated cut-off SHOULD NOT | INV-011, INV-012, INV-121; C2-02 | ok |
| 004 | per period MUST; ICHD-3 definition MUST | C1-01; INV-125 (SD-DF-01 must) | ok |
| 005 | MUST for patients with migraine; label SHOULD | C1-02; INV-008 | ok |
| 006 | SHOULD; definition named | C1-03 (should), C1-04 (must, OUT-001); INV-008 | ok in substance; the trace lists INV-031, which no longer relates these days (R36-02) |
| 007 | SHOULD, separately from days; ICHD-3 definition | C1-05, C1-06; E-019; INV-125 (SD-DF-02 should) | ok |
| 008 | MAY, exploratory | E-020–E-022, C3-02 (may); INV-104 (ISS-04) | ok |
| 009 | SHOULD series with start, dose-change and stop markers; weekly where relevant | INV-034, INV-035, E-035 W2, INV-123, INV-001 | ok |
| 010 | SHOULD on a stated scale; comparison between periods | C1-07, INV-032, INV-039 | ok |
| 011 | SHOULD summary and label; Caveat SHOULD NOT stand-alone | C1-08, C3-03, C2-03 | ok in substance; the trace lists INV-033 (R36-02) |
| 012 | SHOULD across periods and per treated attack, for migraine | C1-09, INV-076, E-053, `requiredOutcomes` | ok |
| 013 | MAY auras and duration | E-019, E-024, E-027 | ok |
| 014 | MUST total, per 8.2 class, per drug | C1-10, `medicationKinds`, INV-024, INV-122, SD-CLS | ok |
| 015 | SHOULD weekly | C1-11 | ok |
| 016 | MUST indicator per period, per class and combined, levels and span; prompt MUST; diagnosis MUST NOT | INV-044–INV-046, SD-CLS, SD-CMB, SD-FX-06; C3-04 (must); C2-04 (mustNot) | ok |
| 017 | SHOULD from withdrawal, review window, a year, label | INV-049–INV-051, E-039 `reviewWindow`, C3-06 | ok |
| 018 | MUST comparison, values, both changes, MSHD where reported, guidance time points; Caveat MUST NOT continuation decision | INV-053, INV-055–INV-059, E-040/E-043 W2, SD-ER; C2-05 | ok |
| 019 | SHOULD residual burden wherever a % change is shown | INV-060, INV-061; ISS-13 for periods < 28 days | ok (see Checked and not raised) |
| 020 | MAY label; SHOULD criterion and values; SHOULD NOT sole indicator | E-045, E-046, INV-062–INV-064, INV-114, INV-116, SD-RC, SD-CL; C2-06; C3-07 | ok |
| 021 | MUST HD/MD/AMD for same periods; SHOULD further components where provided | INV-102, INV-068; INV-069 | ok |
| 022 | SHOULD after stop/pause/reduction vs on-treatment and original baseline | INV-103, INV-070, INV-112, E-049 | ok |
| 023 | SHOULD outcomes, consistency, relief, non-pain, AEs, timing, formulation, per phase, 15 min for cluster; Caveat | INV-071–INV-075, SD-ET; C2-07 | ok |
| 024 | SHOULD chronological list grouped by class with all named details | INV-077–INV-079, INV-109, E-054 and E-055 W2 | ok |
| 025 | MAY scheme windows labelled | E-056, INV-080 | ok |
| 039 | SHOULD adherence next to the comparison, in the history and in the clinician summary | INV-066, INV-067, INV-109, INV-104 | ok |
| 026 | SHOULD results with name, date, recall, score, grading, change | INV-081, INV-082, E-058, SD-IN, SD-GB | ok |
| 027 | SHOULD per period incl. severe; comparison with baseline | C1-12, INV-027 | ok in substance; the trace lists INV-033 (R36-02) |
| 028 | MUST view; SHOULD definitions; SHOULD NOT diagnosis | INV-040–INV-042; C2-08 | ok |
| 029 | MUST per type and combined; SHOULD intensity per type | C1-13, C1-14, INV-122 | ok |
| 030 | MUST relation to menstruation, A1.1 window, complete cycles | INV-086, INV-087, INV-124, SD-FX-01/02 | ok |
| 031 | SHOULD bouts, remissions, rates, 15 min, rescue, previous bouts | INV-088, INV-089, INV-124, SD-FX-07 | ok |
| 032 | MAY view; caveats SHOULD | E-065, INV-110, C3-09 | ok |
| 033 | SHOULD screening results next to headache outputs; Caveat | INV-083, INV-085, SD-SR; C2-09; C3-10 | ok |
| 034 | SHOULD concise clinician summary with listed outputs | INV-094, INV-104 | ok |
| 035 | SHOULD plain-language overview with listed components | INV-095, INV-105 | ok |
| 036 | SHOULD (a)–(d); Caveat supportive | INV-096, INV-097, SD-ER-15, INV-055; C3-11 | ok in substance; the trace lists INV-033 (R36-02) |
| 037 | SHOULD NOT primary (migraine); SHOULD exploratory + components; SHOULD headache days with AUC (TTH) | INV-091; C3-12, E-033 W2, INV-092, INV-115; INV-093 | ok |
| 038 | SHOULD caveats and interpretation | C3-01, C3-05, C3-07–C3-10; C2-01 | ok |

### Mechanical checks (scripts in `scripts/`)

| Check | Result |
|---|---|
| Headings and IDs | 67 E, 87 INV and 12 ISS headings; no duplicates; 0 unresolved E-/INV-/ISS- references in the model and `RATIONALE.md`; 174 table-row IDs (OC, C1–C3, SD) with no duplicates and 0 unresolved references; 432 entries with no duplicates and 0 unresolved entry references (including ranges such as "E-046/Q01 to E-046/Q05") |
| Evidence pointers | every `[S-NNN] <entry>` pair in a model Evidence field names an entry whose Source lines include S-NNN (0 mismatches); every entry except the case-row, section and search-log entries is referenced from the model; three shared entries do not list every citing item under Concerns (informative only) |
| Traceability | 39 rows in Stage 1 order. The Elements and Invariants columns equal the union of the Realises fields (0 differences). The Realises fields of INV-031 and INV-033 are themselves stale (R36-02) |
| Catalogue | 45 rows = `CatalogueRow` (oc01–oc45); every OUT appears in some row's Realises; every element is in a row or in the section 4.2 "no row" list; for every OUT named in Realises, an item named in the row realises it; 42 Audience cells verbatim against Stage 1 (0 mismatches; OC-02, OC-44 and OC-45 have no Stage 1 Audience by design); OC-08 lists OUT-013 against the column's definition (R36-02) |
| Definitional cross-links | element "Definitional:" lists against invariant "definitional (E-…)" lists: genuine mismatches only for INV-031 (E-017, E-021) and INV-033 (E-024, E-030, E-031) (R36-02); the others are indirections through `daysWithin`, `nestedIn`, `factsShown` or `gradeBands` |
| Declared names | 645 declared names; no duplicate declaration. The only identifiers used in `omn` blocks and formal table cells that are not declared are the table names in `table N` (syntax) and `refs` (defined in section 2.5 prose). Every attribute selection `.a` is a declared attribute or component |
| Placement markers | 20 marked attributes, each on a `→R` type, each listed in the section 6.0 index |
| Case tables | keys distinct in C1 (14 rows), C2 (9), C3 (12) and SD-*; every component of `EvaluationRule`, `ResponderCriterion` and `GradeBand` has a column; form-C headers apply declared functions |
| Levels | C1 must cases (C1-01, -02, -04, -06, -10, -13) all realise MUST parts; should cases realise SHOULD parts; C2-04 and C2-05 mustNot (OUT-016 MUST NOT; OUT-018 Caveat MUST); C3-04 must (OUT-016); SD-DF-01 must and -02 should; the 11 MUST invariants realise MUST parts; INV-091 SHOULD NOT (OUT-037) |
| Scope | the terms enter/record/input/answer/storage/database/JSON/XML/FHIR/algorithm/calculated occur in the model and `RATIONALE.md` only in exclusion statements, the HALT-30 quote ("records days affected"), the [S-010] note on definitions not quoted, and the INV-076/D01 exclusion |

## Remarks

### R36-01 Citation defect: [S-010] and [S-015] quote entries give a URL at which their quoted text cannot be read
- Item(s): `RATIONALE.md` entries E-018/Q01, E-018/Q02, E-018/Q03, E-046/Q01 to E-046/Q05, INV-031/Q00, INV-062/Q00, INV-064/Q00, ISS-05/Q00, ISS-08/Q00 (all [S-010]); E-008/Q00, INV-001/Q00, ISS-11/Q00 (the [S-015] population phrase); the model Evidence fields that point to them (E-018, E-046, E-045, INV-031, INV-062, INV-064, ISS-05, ISS-08, E-008, INV-001, ISS-11).
- Problem:
  - From v35 on, the URL of a quote is given once, in its `RATIONALE.md` entry. PROCESS.md section 6 says: "The verbatim quote, its translation, its location and its URL are given once, in that `RATIONALE.md` entry". `RATIONALE.md` section 1 defines the Q entry as "the source ID and the URL where it can be read".
  - Stage 1 lists two URLs for [S-010]: "Abstract quotes: https://pubmed.ncbi.nlm.nih.gov/39980456/ ; full-text quotes: https://ricerca.univaq.it/bitstream/11697/264025/1/sacco-et-al-2025-setting-higher-standards-for-migraine-prevention-a-position-statement-of-the-international-headache.pdf".
  - All 13 [S-010] entries give only the PubMed abstract URL (`- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/`). Every quote they hold is from the full text, section "Setting goals of migraine burden while on treatment", p. 6.
  - Some entries even state that their text is from the PDF. E-018/Q02: "in the PDF text layer line ends break 'definition' and 'following'". E-046/Q04: "in the PDF text layer the running header 'Cephalalgia 45(2)' interrupts the sentence".
  - Same class, for [S-015]: E-008/Q00, INV-001/Q00 and ISS-11/Q00 quote "young people (aged 12 years and older) and adults". That phrase is on the CG150 Overview page only, but the Source line of each entry gives the Recommendations page. E-041/Q01 does it right: its Location names `https://www.nice.org.uk/guidance/cg150`.
  - The equivalence fix's URL sweep (EQ35-02 class sweep) did not catch this. It checked only that each Source URL belongs to the source's row, not that the entry's quote can be read at it.
- Evidence:
  - **The abstract has none of the quotes.** The PubMed abstract (`efetch.fcgi?db=pubmed&id=39980456&rettype=abstract`) contains none of the 18 quoted [S-010] fragments of these entries (script check). For example, it has "modest control (four to six days with migraine or moderate-to-severe headache)", but not "Modest Control. This is defined as four to six days with migraine or moderate-to-severe headache per month." (E-018/Q01, E-046/Q03, ISS-05/Q00). It also does not have "In some cases, insufficient control may be present when there are less than six MMDs" (E-046/Q05), "for three months" (INV-062/Q00), "The assessment of the above goals requires a clear definition of migraine day." (E-018/Q02) or "We included in our definitions of treatment goals also moderate-to-severe headache days as a proxy of migraine days" (E-018/Q03).
  - **The full text has all of them.** All 18 fragments are on p. 6 of the univaq PDF (`pdftotext -raw`, page 6).
  - **The NICE pages.** The phrase "young people (aged 12 years and older) and adults" occurs on `https://www.nice.org.uk/guidance/cg150` and not on `https://www.nice.org.uk/guidance/cg150/chapter/Recommendations` (both fetched 2026-10-22; 0 occurrences of "12 years" on the Recommendations page).
- Required change:
  - **[S-010] entries.** In the Source line of the 13 entries, give the full-text URL from Stage 1 section 5 (`https://ricerca.univaq.it/bitstream/11697/264025/1/sacco-et-al-2025-setting-higher-standards-for-migraine-prevention-a-position-statement-of-the-international-headache.pdf`). The PubMed URL may stay only beside it, for an entry that also quotes the abstract (none does now).
  - **[S-015] entries.** In E-008/Q00, INV-001/Q00 and ISS-11/Q00, add the Overview page URL for the population phrase, as E-041/Q01 does in its Location.
  - **Class.** For every Source line whose Stage 1 or section 10 row lists more than one URL (S-010, S-015 Overview/Recommendations, S-106 chapter/overview, S-024, S-025, S-045, S-046 if ever quoted), check that the named URL is the one where that entry's quoted text can be read. My check found no other case.

### R36-02 Coverage gap (traceability) and contradiction: kept invariants that lost conjuncts in v35 still carry the Conformance, Realises and Evidence of the moved conjuncts
- Item(s):
  - INV-033 (Conformance, Realises);
  - INV-031 (Conformance, Realises, Evidence, and entry INV-031/Q00);
  - INV-075 (Evidence) and INV-079 (Evidence, and entry INV-079/Q00);
  - section 7 rows OUT-006, OUT-011, OUT-027 and OUT-036;
  - section 9 row INV-036;
  - catalogue row OC-08 (Realises).
- Problem:
  - **INV-033.** v35 moved the pain-time, symptom-days and caregiver-days bounds to INV-121 and the functional-impact bounds to INV-122 (fix-iter-35 mapping: "pain time, symptom days, caregiver days → INV-121; functional-impact bounds → INV-122; keeps attacks-with-symptom bound"). The v35 predicate is only `∀ a : AssociatedSymptomSummary • ∀ n : ℕ; e ∈ viewOf(a).content ∩ AttackCount • a.presence = attacksWithSymptom(n) ∧ … ⇒ n ≤ e.count`. Yet:
    - its Conformance still reads "definitional (E-024, E-025, E-030, E-031)";
    - its Realises still reads "OUT-011, OUT-012, OUT-027, OUT-036".
    
    The predicate mentions no duration (E-024, OUT-011), functional-impact (E-030, OUT-027) or caregiver (E-031, OUT-036 (b)) value. It does use E-019 `AttackCount`, which the field does not list.
  - **INV-031.** Its nesting bounds (moderate/severe ≤ headache days; symptom-free ≤ headache-free) moved to INV-122. The v35 predicate concerns only headache-free + headache days, the E-018 count against migraine days, and the mark of a migraine-free period. Yet:
    - its Conformance still lists E-017 and E-021;
    - its Realises still lists OUT-006;
    - its Evidence still cites "OUT-006" and "[S-002]" through INV-031/Q00, whose [S-002] text is the symptom-free-day definition that supports the moved bound.
  - **The traceability table carries the error.** Section 7 is built from the Realises fields, so row OUT-006 lists INV-031, and rows OUT-011, OUT-027 and OUT-036 list INV-033, although neither invariant realises any part of those requirements.
  - **The model contradicts itself.** The elements were updated, the invariants were not:
    - E-017 Conformance: "Definitional: INV-122";
    - E-021: "Definitional: INV-122";
    - E-024: "Definitional: INV-121";
    - E-030: "Definitional: INV-121, INV-122";
    - E-031: "Definitional: INV-121".
    
    INV-033 says it is definitional for E-024, E-030 and E-031, and INV-031 for E-017 and E-021, while those elements do not list them.
  - **Same class, Evidence only.**
    - INV-075's Evidence quotes OUT-023 "The output SHOULD also state the formulation or route … separately for each formulation of the same drug". That supported the medication and formulation tie that v35 moved to INV-123 (`usedMedication`); v35 INV-075 has no formulation conjunct.
    - INV-079's Evidence and INV-079/Q00 cite OUT-023 and the OUT-024 formulation and "reason for stopping" wording, with the [S-012] triptan-refractoriness quote. Those supported the formulation and stop-reason ties, now in INV-123 (`usedMedication`, `stoppedCourse`).
  - **Section 9, INV-036.** "Went into" names INV-123 only. Its `markedKind(mk.event)` conjunct went into the type of E-034 `event`, as fix-iter-35's mapping states ("INV-123 + E-034 attribute type"). PROCESS.md section 7 asks for "the item(s) it went into".
  - **Catalogue row OC-08.** "Number of attacks (E-019 `AttackCount`)" lists OUT-013 in Realises. Section 4.2 defines that column as "the requirements whose statements name this kind of output". OUT-013 names auras ("the number of auras per reporting period and their duration"), which are row OC-14 (and OC-12 for durations), not attack counts.
- Evidence:
  - The v34 INV-033 (`history/v34.md`, "Further bounds of per-period values") had the four conjuncts that justified these fields. The v35 predicate is quoted above.
  - Script check of every definitional invariant: element types and measures used in the predicate against the elements its Conformance lists. Listed but unused, and not reached through a defined function: INV-031 {E-017, E-021} and INV-033 {E-024, E-030, E-031}. A cross-check of element "Definitional:" lists against invariant lists gives the same five pairs.
  - The equivalence check reported "Realises unchanged for all 146 kept items" as a pass. For these two items, unchanged Realises with fewer conjuncts is the defect.
- Required change:
  - **Class.** Every kept invariant whose conjuncts v35 moved out (the 29 edited invariants of fix-iter-35 section 4) keeps in Conformance, Realises and Evidence only the elements, requirements and citations its v35 predicate uses. In the fix log, check each of the 29 and name the class.
  - **INV-033.** Conformance "definitional (E-019, E-025)" (or E-025 alone if E-019 is held to be only a referenced value); Realises "OUT-012" (OUT-007 may be added as the attacks it bounds against).
  - **INV-031.** Conformance without E-017 and E-021 (adding E-015 and E-016, which the predicate uses); Realises "OUT-008, OUT-020"; Evidence without OUT-006, and INV-031/Q00 without the [S-002] symptom-free definition. Alternatively, keep INV-031/Q00 and note that it serves INV-122.
  - **INV-075 and INV-079.** Remove from their Evidence (and from INV-079/Q00) the citations that support only the moved ties, or move them to INV-123.
  - **Section 7.** Drop INV-031 from row OUT-006, and INV-033 from rows OUT-011, OUT-027 and OUT-036.
  - **Section 9.** In the INV-036 row: "INV-123; E-034 `event` (attribute type)".
  - **Catalogue.** Remove OUT-013 from OC-08 Realises.

### R36-03 Prose overclaim: two notation and overview sentences misstate the formal text
- Item(s): section 2.5 ("References" bullet); section 4.2 (last paragraph).
- Problem:
  - **Section 2.5.** It states: "Where a referenced atom must be shown in the holder's view, an invariant states it: for periods, INV-003, …; for the other references, a placement marker (rule W2)." That is not so in v35. Three non-period references are placed by invariants, not markers:
    - `ClassGroup.lines` by INV-078 (`∀ l ∈ ran g.lines • l ∈ v.content`, SHOULD);
    - `MenstrualRelationView.cycles` by INV-087 (`v.content ∩ CycleLine = ran v.cycles`, definitional);
    - the day counts of a residual burden by INV-060 (`rb.migraineDays ∈ viewOf(ch).content ∧ rb.moderateSevereHeadacheDays ∈ viewOf(ch).content`, SHOULD).
    
    Section 6.0 itself says "Not marked: `ClassGroup.lines` (INV-078 places the lines in the history view), `MenstrualRelationView.cycles` (INV-087 states an equality)". So the notation section contradicts the model's own index. A reader or fixer who relies on section 2.5 would conclude that these references need not be in the view.
  - **Section 4.2.** It lists among the elements without a catalogue row "E-014 (abstract `DayCount`; nesting in INV-122)". E-014 declares `element DayCount extends PeriodValue { … }`, which is not abstract. In OMN, `abstract` has a formal meaning (section 2.5: "An `abstract` type has no atoms except those of its subtypes"). DayCount has no subtypes, only type abbreviations (E-015 to E-021, E-029, E-030), so an abstract `DayCount` would have no atoms and no day count could be shown.
  - PROCESS.md section 6a: "Prose claims nothing beyond the formal text."
- Evidence: section 2.5 and section 6.0 as quoted; the predicates of INV-060, INV-078 and INV-087; the E-014 Definition.
- Required change:
  - **Section 2.5.** For example: "for the other references, a placement marker (rule W2) or an invariant named in section 6.0 (INV-060, INV-078, INV-087)". Add INV-060 to the "Not marked" sentence of section 6.0 if that sentence is meant to list all such placements.
  - **Section 4.2.** Delete "abstract": "E-014 (`DayCount`, whose kinds have rows of their own; nesting in INV-122)".

## Checked and not raised

- **CHG-03, INV-060 and ISS-13.** INV-060 now asks for the residual burden only next to percentage changes over compared periods of at least 28 days. That narrows OUT-019's "Wherever". It rests on INV-061's reading that the month lies within the compared period (R01-03; fix 02, item 14). It is an intended change decided for the restructuring and recorded for the human in ISS-13, which asks which month applies. ISS-13 is founded: "per month" next to a weekly change is not fixed by Stage 1. No new evidence shows fix 02's reading wrong.
- **Generic invariants.** INV-118 to INV-125 and the C1–C3/SD-DF cases: well typed, keys distinct, every level as its Stage 1 part. The vacuous instances (for example INV-118 at `shouldNot`) are not literally of the form ¬F as section 3.3 item 7 says, but they impose nothing.
- **INV-119 Notes.** The claim that C2-08 and C2-09 are implied by C2-01 holds.
- **INV-119/D04.** The claim that annotations qualifying the three-month view or its items are in its content follows from W2 and the one-view rule (checked).
- **INV-125's guard** is `dom fixedDefinition`, while it applies `fixedDefinitionLevel`. Both domains are exactly the two SD-DF keys.
- **R-MCF (section 3.8).** Clauses (1)–(4) agree with the formal tests:
  - (1): INV-123 `courseEvent`/start, INV-068 (MUST), INV-079, INV-112, E-041 `inPopulation`;
  - (2): `courseBegunBy` and `courseNotOutside`;
  - (3): INV-080 and INV-094;
  - (4): INV-123 `availableResult` and `availableScreening`.
- **INV-123.** `factsShown`/`stated` are well typed. `usedScope` (CHG-05) makes INV-046/S01 true (re-derived for a single 8.2.6 class and for no acute medication). The attribute table of INV-123/D01 matches the members. No widening of the class is raised (check 32, watch point 1).
- **E-061/D02, INV-087/D01 and INV-124/D01.** The window-mark claims, with their stated exception, follow from INV-087 and INV-124 (argued for consecutive and non-consecutive lines, lead-ins and one-day lines).
- **Section 3.3 item 2 and the `set … MUST` attributes of `CycleLine`.** Settled in review 14; no new evidence.
- **"History of previous bouts" (OUT-031).** Settled since review 01.
- **Missing English for short heading fragments in E-041/Q00.** "3. MİGREN BAŞ AĞRISI TEDAVİSİ", "Migren Profilaktik Tedavi-Yönetim-6", "для профилактики хронической М", "профилактической терапии мигрени" have no translation, but the entry states their point in English ("name migraine as well"), and the full sentences are translated in Q18, Q19 and Q22. Moved verbatim from v34 and reviewed (review 34).
- **E-008/Q00** quotes the [S-008] Q6 fragment "acceptable for treatment continuation beyond three months" without an [S-008] Source line. The entry says "quoted in E-045", whose E-045/Q01 has the source; verified verbatim (p. 12).
- **SD-ER-04's Rationale cell** names E-041/Q07 (14H) but not Q06 (14B) for `excludes ↦ {onabotulinumtoxinA}`. The cell is informative, and E-041/D04 gives the ground.
- **SD-GB-15 and SD-GB-16** show HALT-90 grades "III" and "IV" without the parenthetical "(indicates high need for care)". The parenthetical annotates the grade in [S-014] Table 18; the labels are as printed.
- **Catalogue OC-33 Audience** names OUT-010 and OUT-027 by ID only. The column is informative, and the other 42 cells are verbatim.
- **Coverage lines.** Rows OUT-008 and OUT-012 name INV-104 and INV-069, which do not list those requirements in Realises. These are coverage remarks consistent with ISS-04 and OUT-021, not the Elements and Invariants columns.
- **Concerns fields.** E-009/Q03, E-028/Q02 and E-046/Q01 do not name every item that cites them. The field is informative.
- **`refs`** (INV-003) is defined in the section 2.5 prose, as since v00.
- **Watch points of the oscillation check after iteration 32.** None is touched by these remarks:
  - INV-112 to INV-116, INV-079's duration conjuncts, `E-046.comparison` and the comparability ties are unchanged;
  - INV-123's members and the "not in the class" rows are not widened;
  - R36-02 only corrects the bookkeeping fields of INV-031 and INV-033 to their v35 predicates. It reverses no decision.
- **Scope.** No input, storage or derivation-from-input content in the model or `RATIONALE.md`. Every relation of the source data tables (MOI status, control levels, responder components, rates, windows, completeness proportion, changes) takes output elements and context properties as arguments, as in v34.

## Notes on frozen items (for the human)

None. No item is frozen (`FROZEN_ITEMS.md` does not exist; no "Status: FROZEN" marker in the model).
