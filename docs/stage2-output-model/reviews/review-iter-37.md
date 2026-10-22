# Review — iteration 37
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v36
Date: 2026-10-22

## Summary

I reviewed v36 (`OUTPUT_MODEL.md` and `RATIONALE.md` v36) on its own merits against Stage 1 v18 and the sources. I did not redo the v34 → v35 equivalence check.

The formal content holds up:
- **Quotes.** Every quoted fragment in the 113 Q entries of `RATIONALE.md` is verbatim at the URL its entry names and at its stated location. That includes the [S-010] and [S-015] URLs that fix 36 corrected.
- **Values.** Every value of the source data tables matches its source: codes and labels, reference levels and spans, windows, evaluation rules, named criteria, control levels, ranges, bands, recall periods.
- **Levels.** Every level, including each case of the level-indexed invariants INV-118 to INV-120 and INV-125, follows the strength of its Stage 1 statement part.
- **Mechanical checks.** IDs, references, Evidence pointers, the traceability table and the catalogue's Realises column all pass. So do declared names, case-table forms and keys, and the attribute typing rule.
- **Scope.** The scope sweep is clean.
- **Stage 1 issues.** The issues of section 8, ISS-13 included, are founded.

One remark (R37-01, rule stated per case). The output catalogue of section 4.3, new in v35, is meant to be an index. Two of its columns restate generic invariants row by row: the definitional invariants INV-006, INV-121 and INV-122 in "Availability", and the companions INV-008 and INV-011 in "Shown with it". The restatements differ between rows of the same kind and miss cases. Five rows say "—" where INV-011 asks for a completeness indicator. PROCESS.md section 6a requires a rule to be stated once. The preferred fix shrinks the catalogue: state the generic invariants once in section 4.2.

## Verification coverage

### Method

Downloads, extracted texts and scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r37/`:
- `dl/` holds one fresh folder per source;
- `txt/` holds the extracted texts;
- `scripts/` holds the scripts, all run with `python3 -I`.

How the sources were fetched and read:
- Every URL that a Source line of `RATIONALE.md` names was fetched with `curl`.
- PDFs were extracted page by page with `pdftotext` (`-raw` and `-layout`).
- PMC articles were read in their Europe PMC `fullTextXML` form, which model section 10 names. For S-101 and S-102 the PMC HTML page was read as well.
- Web pages had their markup removed.
- ICHD-3 p. 190 and the title page of S-034 were rendered with `pdftoppm` and read.

The scripts:
- `parse_rat.py` split `RATIONALE.md` into 434 entries (113 Q; no duplicate IDs).
- `check_quotes.py` took every `Quote` field and every double-quoted string in the Text fields of the Q entries, 309 fragments after splitting at `[...]`. It searched each fragment in the text behind each URL of its entry, in three passes:
  1. exact, with only white space, quote marks, dashes and ligatures normalised;
  2. with line-end hyphens joined;
  3. letters and digits only.
  
  Fragments not found in a listed source were looked up in Stage 1 v18. The stated page or section was compared with the place of each hit.

### Sources

| Source | URL used (as in the entries) | Q entries | Fragments verified at the URL | Not found | Unreachable / notes |
|---|---|---|---|---|---|
| S-001 ICHD-3 | ichd-3.org PDF, 211 pp. | 28 | 59 (40 exact, 7 after line-end joins, 12 letters/digits for unmapped "≥"); plus 3 "±"/"−" window fragments (E-060/Q01, INV-087/Q00) read on rendered p. 190 | 0 | — |
| S-002 | ihs-headache.org PDF | 2 | 3 (p. 12 = journal p. 1037) | 0 | — |
| S-005 | ihs-headache.org PDF | 2 | 2 (pp. 8–9 = 810–811) | 0 | — |
| S-007 | UCL Discovery PDF, 39 pp. | 3 | 3 (pp. 10, 22, 25) | 0 | — |
| S-008 | univaq PDF, 31 pp. | 10 | 18 (pp. 6, 9, 12, 13, 17) | 0 | — |
| S-010 | univaq full-text PDF, 11 pp. | 13 | 18, all on p. 6 | 0 | No entry gives the PubMed URL any more (fix 36) |
| S-011 | Europe PMC XML of PMC9188162 | 8 | 10 | 0 | — |
| S-012 | PMC9555163 | 1 | 1 | 0 | — |
| S-013 | PMC7296705 | 2 | 2 | 0 | — |
| S-014 | PMC6734476 | 10 | 26 (Table 18 cells read in the XML; paragraph "There are three versions of HALT" and "Scoring HALT" first sentence confirmed) | 0 | — |
| S-015 | NICE CG150 Recommendations page and Overview page | 15 | 30 (the population phrase on the Overview page only, as the corrected Source lines say; 1.3.27–1.3.29 under "Prophylactic treatment review", within "Migraine with or without aura") | 0 | Recommendations page "Last updated: 03 June 2025"; Overview "Last reviewed: 23 September 2026" |
| S-016 | SIGN 155 PDF, 64 pp. | 3 | 8 (PDF p. 7 = printed p. 1; PDF p. 20 = printed p. 14) | 0 | — |
| S-018 | AAN Clinician Summary PDF, 12 pp. | 4 | 7 (pp. 1, 7, 8) | 0 | — |
| S-022 | EMA draft PDF | 3 | 1 sentence (p. 11), found after removing the margin line numbers | 0 | — |
| S-023 | PMC9607711 | 1 | 4 | 0 | — |
| S-028 | NVN module page | 2 | 7 | 0 | — |
| S-030 | DHOS PDF, 86 pp. | 3 | 2 (p. 19) | 0 | — |
| S-032 | brainmed.com page | 1 | the 2 Stage 1 strings found on the page | 0 | first attempt reset the connection (curl 35); the retry succeeded |
| S-033 | Minzdrav PDF 295_4, 92 pp. | 6 | 12 (pp. 1, 4, 18, 39, 40, 53) | 0 | — |
| S-034 | Minzdrav PDF 169_3, 53 pp. | 6 | 10 in the text layer (pp. 3, 17, 32, 52); title page p. 1 rendered: "Возрастная группа" / "дети" | 0 | first attempt reset the connection; the retry succeeded |
| S-035 | noroloji.org.tr PDF, 92 pp. | 11 | 20 (pp. 2, 6, 7, 22, 23, 48, 57, 77, 86) | 0 | — |
| S-042 | PMC12279330 | 1 | 1 | 0 | — |
| S-101 | PMC3057423 | 4 | 2 (Methods > Data sources) | 0 | — |
| S-102 | PMC4406925 | 4 | 3 (Methods > Migraine-related disability) | 0 | — |
| S-103 | cincinnatichildrens.org PedMIDAS page | 3 | 12 (title "PedMIDAS Tool \| Headache Center"; heading "PedMIDAS Tool for Assessing Migraine Disability"; footer © 2026) | 0 | — |
| S-104 | PMC183845 (Europe PMC XML) | 3 | 2 | 0 | the PMC HTML returned a bot-check page |
| S-105 | Joint Commission PDF, 9 pp. | 3 | 2 (P. 6/9; PHQ-9 sentence also on P. 5/9); PDF metadata: created 2010-06-22, modified 2014-04-16, author Kurt Kroenke | 0 | — |
| S-106 | NICE TA260 chapter 2 and overview | 2 | 1 (para 2.1); published 27 June 2012, last reviewed 11 January 2016 | 0 | — |

**Totals.**
- 309 fragments: 246 verified in a listed source by script, plus 4 more by reading:
  - the 3 window fragments on rendered ICHD-3 p. 190;
  - "Возрастная группа" on the rendered S-034 title page.
- 54 fragments are Stage 1 wording, found verbatim in Stage 1 v18.
- 5 are English translations, checked against their originals.
- No misquote. No quote that cannot be read at its URL.

**Translations.** Checked against the originals and faithful:
- E-041/Q15 (Dutch);
- E-041/Q16 to Q21 (Russian);
- E-041/Q22 to Q28 (Turkish);
- E-045/Q03 and Q04 (Turkish);
- ISS-10/Q00 (Russian).

**Metadata and versions.**
- PubMed `esummary` confirms citation, DOI and PMC ID for S-101 (PMID 20819842), S-102 (25902814), S-104 (12914662) and the S-103 developer paper (11739822, 10.1212/wnl.57.11.2034).
- Types and gradings are as stated.
- No ICHD-4 has been published: a web search finds only the 2020 alpha, "Work in Progress 1" (Cephalalgia 2024) and an IHS workshop in 2025.
- TA260 is not superseded.
- The CG150 recommendations that the model uses are unchanged ("Last updated: 03 June 2025").

**Evidence pointers.** All 122 `[S-NNN] <entry>` pairs in model Evidence fields resolve to an entry whose Source lines include that source (script `evid.py`; ranges such as "E-046/Q01 to E-046/Q05" expanded). Every Q entry is referenced from the model. For the source data tables, each row's Rationale cell names an entry that holds the quote supporting the cell's value. I checked each row of SD-IC, SD-CLS, SD-CMB, SD-FX, SD-ER, SD-RC, SD-CL, SD-IN, SD-GB, SD-SR and SD-ET.

### Source data tables against their sources

Every formal cell agrees with its quote:
- **SD-IC.** The ICHD-3 code labels on pp. 8, 9 and 12.
- **SD-CLS and SD-CMB.** 10 days/month for every class except 15 for non-opioid analgesics; 10 for 8.2.6; span "> 3 months" (pp. 122–125); `classesOf826` as in 8.2.6 criterion B.
- **SD-FX.**
  - The A1.1 window "day 1 ± 2 (i.e. days −2 to +3)" with "no day 0" gives 2 days before and 2 after (p. 190).
  - Remission "must exceed three months" (p. 209).
  - Review window 4–8 weeks; 12 months; 28 days.
- **SD-ER-01 to SD-ER-18.** Offsets, anchors, timings, ages, types and exclusions against E-041/Q00 to Q30.
- **SD-RC-01 to SD-RC-06.** NICE 1.3.28 50/30 %, 1.3.29 30 %; IHS Q6 50 %, 30 % in the chronic alternative, MIDAS ≥ 5 points for baseline 11–20 and ≥ 30 % for ≥ 20, HIT-6 ≥ 5 points; DMKG 50 %, 5 points, 30 %; Russian 7.1 50 %.
- **SD-CL.** 0; < 4 for three months; 4–6; > 6, which can also hold below six days.
- **SD-IN and SD-GB.**
  - HIT-6: 36–78; bands ≤ 49, 50–55, 56–59, 60–78; recall 1 month ([S-002]).
  - MIDAS: grades 0–5, 6–10, 11–20, ≥ 21 with the [S-102] labels; recall 3 months.
  - PedMIDAS: 0–10, 11–30, 31–50, > 50 (`strictLow`); recall 3 months ([S-005]).
  - HALT-90: 0–5, 6–10, 11–20, ≥ 20; HALT-30: 1 month, ungraded.
  - HURT: graded areas.
- **SD-SC and SD-SR.** HADS 0–21 per subscale, PHQ-9 0–27, GAD-7 0–21.
- **SD-ET.** 15 minutes for cluster headache.
- **SD-DF.** "headache days" at MUST (OUT-004), "frequency of attacks" at SHOULD (OUT-007).

### Fidelity to Stage 1, requirement by requirement

Each requirement was checked as follows:
- its Statement and constraining Caveats against the catalogue row(s), case-table rows, elements and invariants that realise it;
- the level of each part against the strength of the Stage 1 part (PROCESS.md section 4).

| OUT | Parts and strength | Realised by (main items) | Result |
|---|---|---|---|
| 001 | period stated MUST; per month or 28 days MUST; equal-length comparison MUST; Caveat (lengths visible) | E-003 `covers`, E-005, INV-002, INV-003; C1-01, -02, -04, -06; INV-037, INV-038; `lengthDays` | ok |
| 002 | label SHOULD | INV-008 (`reports`), INV-111 | ok |
| 003 | indicator SHOULD; validated cut-off SHOULD NOT | INV-011, INV-012, INV-121; C2-02 | ok |
| 004 | per period MUST; ICHD-3 definition MUST | C1-01; INV-125 (SD-DF-01) | ok |
| 005 | MUST for patients with migraine; label SHOULD | C1-02; INV-008 | ok |
| 006 | SHOULD; definition named | C1-03; C1-04 (OUT-001); INV-008; INV-122 | ok |
| 007 | SHOULD, separately; ICHD-3 definition | C1-05, C1-06; E-019; INV-125 (SD-DF-02) | ok |
| 008 | MAY, exploratory | E-020 to E-022; C3-02 (may); INV-104 (ISS-04) | ok |
| 009 | SHOULD series with start, dose-change and stop markers; weekly where relevant | INV-034, INV-035, E-035 W2, INV-123, INV-001 | ok |
| 010 | SHOULD, stated scale; comparison between periods | C1-07, INV-032, INV-039 | ok |
| 011 | SHOULD summary and label; Caveat SHOULD NOT | C1-08, C3-03, C2-03 | ok |
| 012 | SHOULD across periods and per treated attack, for migraine | C1-09, INV-076, `requiredOutcomes` | ok |
| 013 | MAY auras and duration | E-019, E-024, E-027 | ok |
| 014 | MUST total, per 8.2 class, per drug | C1-10, `medicationKinds`, INV-024, INV-122, SD-CLS | ok |
| 015 | SHOULD weekly | C1-11 | ok |
| 016 | MUST indicator per period, class and combined, with levels and span; MUST prompt; MUST NOT diagnosis | INV-044 to INV-046, SD-CLS, SD-CMB, SD-FX-06; C3-04; C2-04 | ok |
| 017 | SHOULD from withdrawal, review window, following year, label | INV-049 to INV-051, E-039, C3-06 | ok |
| 018 | MUST comparison with values, both changes, MSHD where reported, guidance time points; Caveat MUST NOT | INV-053, INV-055 to INV-059, E-040/E-043 W2, SD-ER; C2-05 | ok |
| 019 | SHOULD residual burden | INV-060, INV-061; ISS-13 | ok |
| 020 | MAY label; SHOULD criterion and values; SHOULD NOT sole indicator | E-045, E-046, INV-062 to INV-064, INV-114, INV-116; C2-06; C3-07 | ok |
| 021 | MUST HD, MD and AMD for the same periods; SHOULD further components where provided | INV-102, INV-068; INV-069 | ok |
| 022 | SHOULD after stop, pause or reduction | INV-103, INV-070, INV-112, E-049 | ok |
| 023 | SHOULD outcomes, consistency, relief, non-pain, AEs, timing, formulation, per phase, 15 min; Caveat | INV-071 to INV-075, SD-ET; C2-07 | ok |
| 024 | SHOULD chronological grouped list with the named details | INV-077 to INV-079, INV-109, E-054/E-055 W2 | ok |
| 025 | MAY scheme windows, labelled | E-056, INV-080 | ok |
| 039 | SHOULD adherence with the comparison, in the history and in the clinician summary | INV-066, INV-067, INV-109, INV-104 | ok |
| 026 | SHOULD name, date, recall, score, grading, change | INV-081, INV-082, E-058, SD-IN, SD-GB | ok |
| 027 | SHOULD per period incl. severe; comparison with baseline | C1-12, INV-027 | ok |
| 028 | MUST view; SHOULD definitions; SHOULD NOT diagnosis | INV-040 to INV-042; C2-08 | ok |
| 029 | MUST per type and combined; SHOULD intensity per type | C1-13, C1-14, INV-122 | ok |
| 030 | MUST relation to menstruation, A1.1 window, complete cycles | INV-086, INV-087, INV-124, SD-FX-01/02 | ok |
| 031 | SHOULD bouts, remissions, rates, 15 min, rescue | INV-088, INV-089, INV-124, SD-FX-07 | ok |
| 032 | MAY view; caveats SHOULD | E-065, INV-110, C3-09 | ok |
| 033 | SHOULD next to headache outputs; Caveat | INV-083, INV-085, SD-SR; C2-09; C3-10 | ok |
| 034 | SHOULD concise clinician summary with the listed outputs | INV-094, INV-104 | ok |
| 035 | SHOULD plain-language overview | INV-095, INV-105 | ok |
| 036 | SHOULD (a)–(d); Caveat | INV-096, INV-097, SD-ER-15, INV-055; C3-11 | ok |
| 037 | SHOULD NOT primary (migraine); SHOULD exploratory and components; SHOULD HD with AUC (TTH) | INV-091; C3-12, E-033 W2, INV-092, INV-115; INV-093 | ok |
| 038 | SHOULD caveats and interpretation | C3-01, C3-05, C3-07 to C3-10; C2-01 | ok |

### Mechanical checks (scripts in `scripts/`)

| Check | Result |
|---|---|
| Headings and IDs (`model.py`) | 67 E, 87 INV and 12 ISS headings, no duplicate. 0 unresolved E-, INV- or ISS- references in the model or `RATIONALE.md`. References to withdrawn IDs occur only in "Replaces …" notes and section 9. 174 table-row IDs (OC, C1–C3, SD-*): no duplicate, 0 unresolved row references. |
| `RATIONALE.md` (`parse_rat.py`, `evid.py`) | 434 entries, no duplicate. All 122 Evidence pairs resolve with matching sources. No `pubmed` URL remains in a Source line. |
| Traceability (`trace.py`) | 39 rows in Stage 1 order. The Elements and Invariants columns equal the union of the Realises fields (0 differences). The Catalogue-rows column equals the rows whose Realises name the requirement. Coverage lines name INV-104 (OUT-008) and INV-069 (OUT-012) outside the columns; this is known (review 36). |
| Catalogue Realises (`trace.py`) | Every requirement in a row's Realises is in the Realises of an item named in the row. Every element is in a row or in the section 4.2 list. Every OUT appears in some row. |
| Catalogue "def." and "Shown with it" (`catdef.py`) | Inconsistent across rows of the same kind: R37-01. |
| Definitional cross-links | Element "Definitional:" lists against invariant "definitional (E-…)" lists differ in 7 pairs: E-001/INV-123, E-029/INV-045, E-030/INV-121, E-040/INV-111, E-053/INV-074, INV-123/E-014 and INV-082/E-057. Fix 36 examined all seven (section 3, "Examined and not changed"); not raised. |
| Declared names (`names.py`) | Every identifier used in `omn` blocks and formal table cells is declared, a primitive or a bound variable. The exceptions are the table names after `table` and `<br>` in cells. |
| Case tables | 16 captions in the form "Case table <ID> — <form>"; every `table N` reference resolves. Keys are pairwise distinct in C1 (14), C2 (9), C3 (12) and every SD table; SD-GB members are distinct. Every component of `EvaluationRule`, `ResponderCriterion` and `GradeBand` has a column. |
| Typing rule for levels | Every SHOULD or MAY attribute, and every MUST attribute with `when`, has an `opt`, `set` or `seq` type. Placement markers only on `→R` types; the 6.0 index matches the declarations. |
| Levels | C1 must cases realise MUST parts and should cases SHOULD parts. C2-04 and C2-05 are mustNot; the other C2 cases are shouldNot from SHOULD parts or Caveats. C3-04 is must; C3-02 is may (OUT-008). SD-DF-01 is must and SD-DF-02 should. INV-091 is SHOULD NOT. Every MUST invariant (INV-003, INV-037, INV-040, INV-044, INV-055 to INV-057, INV-059, INV-068, INV-086, INV-102) realises a MUST part. |
| Scope | The terms enter/record/input/answer/stored/storage/database/JSON/XML/FHIR/algorithm/calculated/derive occur only in exclusion statements, notation prose, the HALT-30 quote ("records days affected") and INV-076/D01. Every relation of the source data tables takes only output elements and context properties as arguments. |

## Remarks

### R37-01 Rule stated per case: the catalogue restates generic invariants row by row, and the restatements differ and miss cases
- Item(s): section 4.2 (column definitions "Availability" and "Shown with it"); section 4.3, catalogue rows:
  - "Availability" ("def."): OC-06, OC-07, OC-08, OC-09, OC-14, OC-15, OC-24, OC-32, OC-35, OC-42, against OC-05;
  - "Shown with it": OC-11, OC-12, OC-13, OC-14, OC-22, OC-24, OC-28, OC-32, OC-35, OC-42, OC-43, and the view rows OC-10, OC-18, OC-21, OC-26, OC-34, OC-40, OC-41, against OC-05 to OC-09, OC-15, OC-16, OC-19, OC-36 and OC-38.
- Problem:
  - **What the columns promise.** Section 4.2 defines:
    - Availability as "the level and the item that states it (`INV-NNN`, `C1-NN`), and the definitional invariants of the kind";
    - Shown with it as "companions, by ID: periods (INV-003), definition labels (INV-008, "label"), completeness (INV-011, "completeness"), …".
  - **What the rows do.** The rows restate the generic invariants INV-006, INV-121, INV-122, INV-008 and INV-011 one row at a time, and the restatements are not the same for rows of the same kind.
  - **Availability, "def." (the definitional invariants of the kind).** INV-006, INV-121 and INV-122 apply to every per-period day count (E-014 and its kinds), and INV-006 and INV-122 to every event count (E-019).
    - OC-05 (headache days, E-015; E-014) lists "def. INV-006, INV-121, INV-122".
    - OC-06 (migraine days, E-016), OC-07 (E-017) and OC-08 (E-019) list no definitional invariant at all. Yet INV-122's own Conformance field names E-017 and E-019, E-017's Conformance reads "Definitional: INV-122", and E-019's reads "Definitional: INV-006, INV-122".
    - OC-14 (aura counts are E-019 event counts) says "MAY (no invariant)".
    - OC-09, OC-15, OC-24, OC-32 and OC-35 list some of the three and omit others. For example, OC-24 (the E-018 day count) lists only INV-031, and OC-15 lists INV-024 and INV-122 but not INV-006 or INV-121.
    - OC-42 lists INV-121 for E-031 and E-030 but not INV-122, whose Conformance names E-030.
  - **Shown with it, completeness (INV-011).** INV-011 asks for a completeness indicator with every per-period value in a view (first conjunct) and with every value that a change, residual burden or composite index refers to (second conjunct).
    - OC-05 to OC-09, OC-15 and OC-16 list "completeness".
    - The other per-period-value rows do not: OC-11 (E-023), OC-12 (E-024), OC-13 (E-025, E-026), OC-14 (E-027), OC-24 (E-018), OC-28 (E-051), OC-32 (E-030), OC-35, OC-42 (E-031) and OC-43 (E-033).
    - OC-13, OC-14, OC-24, OC-32 and OC-35 show "—", that is, nothing shown with them.
    - OC-19 (change) lists "label; completeness" for its referenced values. OC-22 (residual burden, E-044) has "—", although the same mechanism (`referencedValues`, E-011) brings INV-008 and INV-011 to it. OC-43 (composite index, whose components are `referencedValues`) lists neither.
  - **Shown with it, labels (INV-008, `reports`).** Listed for OC-05 to OC-09, OC-11, OC-19, OC-36 and OC-38. Missing for OC-22 (its migraine days and moderate/severe headache days), OC-35 (per-type headache days, migraine days, moderate/severe headache days and attacks) and OC-43 (frequency components).
  - **View rows.** OC-01, OC-36 and OC-38 list completeness. The view rows whose content is per-period values do not list completeness or labels: OC-10, OC-18, OC-21, OC-26, OC-34, OC-40 and OC-41.
  - **Why it is a remark.** PROCESS.md section 6a was written against exactly this ("about half of them in prose that restated other items"). It reads: "State a rule once. A rule that applies to several outputs is stated once, as a generic invariant over the output catalogue or over a common supertype." Section 9 makes "Rule stated per case" a remark "when the per-case statements differ in content or one case is missing". Both hold here.
  - **The effect.** A reader who uses the catalogue as the index of section 4.2 is told, for example, that nothing is shown with associated-symptom summaries, functional-impact days or residual burden. INV-011 (SHOULD) asks for their completeness, and INV-008 (SHOULD) asks for the residual burden's definition labels.
  - **Not a reversal.**
    - The catalogue is new in v35.
    - No earlier review or fix raised these two columns (searched: reviews, fixes, audits, `restructure/`, `oscillation/`).
    - Fix 36's catalogue sweep covered the Realises column and cells that assert too much, not cells that omit a generic invariant.
    - The class touches watch point 12 of the check after iteration 36 (bookkeeping after the restructuring). Option (a) below removes the per-row restatement instead of extending it, so it closes the class rather than widening it.
- Evidence:
  - Section 4.2, the column table: "Availability | the level and the item that states it (`INV-NNN`, `C1-NN`), and the definitional invariants of the kind" and "Shown with it | companions, by ID: periods (INV-003), definition labels (INV-008, "label"), completeness (INV-011, "completeness"), …".
  - Rows as printed:
    - OC-05 "MUST (C1-01); def. INV-006, INV-121, INV-122 | label (fixed: SD-DF-01); completeness";
    - OC-07 "SHOULD (C1-03); MUST where provided (C1-04) | label; completeness";
    - OC-08 "SHOULD (C1-05); MUST where provided (C1-06) | label (fixed: SD-DF-02); completeness";
    - OC-13 "SHOULD (C1-09); def. INV-033, INV-121 | —";
    - OC-14 "MAY (no invariant) | —";
    - OC-22 "SHOULD (INV-060); def. INV-061 | —";
    - OC-24 "…; def. INV-031 (…) | —";
    - OC-32 "…; def. INV-121, INV-122 | —";
    - OC-35 "…; def. INV-122 | —".
  - Invariants:
    - INV-006 Conformance "definitional (E-014, E-019)";
    - INV-121 "definitional (E-012, E-013, E-014, E-023, E-024, E-025, E-031)";
    - INV-122 "definitional (E-012, E-014, E-017, E-019, E-021, E-029, E-030)";
    - INV-011 first conjunct `∀ m ∈ v.content ∩ PeriodValue • m ∉ CompletenessIndicator ⇒ ∃ ci ∈ v.content ∩ CompletenessIndicator • ci.period = m.period`, and second conjunct over `referencedValues(x)`;
    - INV-008 with `reports` (E-011), which covers `referencedValues`.
  - Script `catdef.py` lists, per row, the elements named, the "def." list, the definitional invariants that the named elements' own Conformance fields give, and whether "label" and "completeness" appear (output in the scratch folder).
- Required change (fix the class: every catalogue cell that restates a generic invariant):
  - **(a), preferred under section 6a.** In section 4.2, state once which generic invariants apply to every row as their predicates state:
    - INV-003 (periods);
    - INV-006, INV-121 and INV-122 (definitional, for the per-period values they quantify over);
    - INV-008 (labels, wherever `reports` holds);
    - INV-011 (completeness);
    - INV-123 (facts shown).
    
    Then keep in each row's "def." only the definitional invariants specific to the kind (for example INV-002, INV-004, INV-031, INV-045, INV-046, INV-087), and in "Shown with it" only row-specific companions: W2 markers, C3 cases, INV-060, INV-066, INV-071, INV-078, fixed-definition rows of SD-DF. Remove "label", "completeness" and "def. INV-006, INV-121, INV-122" from the rows that now carry them, and adjust the column definitions to match.
  - **(b), alternative.** Complete every row by the column definitions: add the missing definitional invariants and the label and completeness companions to the rows listed under Item(s), and replace the "—" cells of OC-13, OC-14, OC-22, OC-24, OC-32 and OC-35.
  - Either way, no `omn` block, level, Realises field or traceability row changes.

## Checked and not raised

- **R-MCF (1) and responder-label periods.** Section 3.8 says content aligned to a stated fact "is admitted only where the context states it". A responder or non-responder label whose treatment has no stated start is admitted, with any `evaluated` periods.
  - R-MCF (1) defines aligned content as a period placed before or after the fact, a date or duration counted from it, or values compared at a time point counted from it.
  - The model places no label period relative to the start. Fix 18 declined that bound with a reason, and INV-123/D01 lists `evaluated` as "not in the class".
  - The values a label compares are those of its response comparison, which INV-123 admits only with a stated start.
  - So the rule's wording holds for what it defines. Not raised (no new evidence against fix 18).
- **The 7 element/invariant definitional cross-link pairs** (Mechanical checks). Fix 36 examined them as uses through another element's function or type. The R37-01 fix (a) leaves them alone. Not raised.
- **INV-075/D01** speaks of a relation that "takes only an output element and a context property as arguments, as INV-123 and INV-079 do". INV-075 no longer has that relation. The equivalence fix examined it and kept it at its plan-fixed anchor ("as INV-123 and INV-079 do" is true). No new evidence. Not raised.
- **INV-110/S01** lists C3 cases (C3-05, C3-07, C3-08, C3-10, and C3-09 twice) whose bearers are not trigger views. These are mechanical renamings of the v34 IDs; the satisfiability claim stays true. Not raised.
- **Dangling colons** at the end of E-041/Q00, E-045/Q00, E-057/Q00, E-064/Q00 and INV-046/Q00 ("not stated in Stage 1:"). This is verbatim moved text, and the following Q entries hold the quotes. Not raised.
- **INV-079 Evidence** cites OUT-024 only, while its Realises also lists OUT-039 (the adherence tie). Stage 1 evidence carries over by reference (PROCESS.md section 4); fix 36's class concerns stale citations, not missing ones. Not raised.
- **E-057 Meaning**, "results show the instrument's own published scores and categories by name (`recallAsPublished`, `publishedCategory`)", for untabulated instruments.
  - INV-082 forces a published category for them.
  - The recall shown cannot be fixed without a value set, which E-057/D07 states.
  - The sentence names the constructs available, consistently with E-057/D07. Not raised.
- **Caregiver lost productive days bounded by the period length (INV-121).** Settled in reviews 16, 24 and 29 (other figures go to `otherCaregiverImpact`). Not raised.
- **HIT-6 recall of one month.** This is [S-002]'s wording. S-101 states no recall period: its "four weeks" phrases concern study eligibility. Settled (reviews 29 and 30). Not raised.
- **ISS-09's description of Group D** without OUT-017. Settled (reviews 25b and 31; check after iteration 28). Not raised.
- **ISS-03's list** of statements that name migraine days without the OUT-005 condition. Checked against every Stage 1 Statement by script: complete.
- **ISS-02.** "Simple analgesics" occurs in the ICHD-3 text layer only on p. 139. Confirmed.
- **ISS-13.** Founded. No calendar month or 28-day period lies within a compared period of fewer than 28 days. This is an intended change recorded for the human (CHG-03); oscillation watch point 1 applies.
- **Stage 1 issues ISS-01 to ISS-12.** Founded, with correct locations and descriptions of the passages they cite (quotes verified above).
- **Prose claims checked against their predicates:**
  - INV-119 Notes (C2-08 and C2-09 implied by C2-01);
  - E-067 (`courseNotOutside` and `courseOverlaps` agree under a stated start);
  - E-012 (`scopeFor` picks exactly one scope and implies `onlyOfType`);
  - INV-073 and INV-089 Readings on cluster scope;
  - section 3.8 clause 2 (`courseBegunBy` equals "on or after the start" where the start is stated, by INV-001);
  - E-043/D01 (a change of a response comparison lies in the comparison's view, by W2 on `reference` and the one-view rule);
  - INV-045/D01 (a span of four monthly periods);
  - the date arithmetic of E-042/W01, W02, INV-055/W01, INV-079/W01, INV-049/W01 and E-063/W01.
  
  All hold.
- **Section 2.5 and the 6.0 "Not marked" list** after fix 36. The placement of `MedicationOveruseIndicator.basis` and of the values of comparisons follows from INV-003, through shared period atoms, which section 2.5 names. Holds.
- **Watch points of the check after iteration 36.** No remark touches watch points 1 to 11. R37-01 falls under watch point 12 and reverses nothing (see the remark).

## Notes on frozen items (for the human)

None. No item is frozen: `FROZEN_ITEMS.md` does not exist, and the model has no "Status: FROZEN" marker.
