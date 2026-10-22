# Review — iteration 40
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v39
Date: 2026-10-22

## Summary

I reviewed v39 (`OUTPUT_MODEL.md` v39 with `RATIONALE.md` v39) on its own merits against Stage 1 v18 and the sources. I did not redo the v34 → v35 equivalence check or fix 39's sweep of v34 prose.

**Citations and source values hold.**
- Every quoted fragment of the 113 Q entries is verbatim at the URL its entry names and at its stated location. So is every `[S-NNN] "…"` quote in the D, N, S, W and X entries and in the model. The only differences are white space, line-end hyphens, glyphs without a text mapping, the image-only title page of [S-034] and the EMA margin line numbers. The entries state each of these.
- Every value of the source data tables matches its source.
- The metadata of S-101 to S-106 is correct, and no newer version of a source changes an element.
- Every Evidence pointer of the model leads to an entry that holds the cited source.

**The v39 change holds.**
- E-056 `frequencyValues`, `instrumentResults` and `treatmentLines` are well typed, MAY, and carry definitional W2 markers.
- The new INV-080 conjunct relates output elements only.
- The OUT-025 row, the catalogue rows, the Realises fields and ISS-04 are consistent with them.

**Stage 1 fidelity.** Every OUT requirement checks out. Each Statement part and constraining Caveat is represented at its Stage 1 level.

**Mechanical checks** are clean: IDs, references, traceability against the Realises fields, the catalogue, declared names, level typing, W2 markers, Audience cells, Evidence pointers and the scope sweep.

**One remark (R40-01, prose overclaim).** It covers one class, Readings that state a relation the predicate does not have, with two members:
- **INV-061.** The Reading says the residual burden shows its two counts "for one calendar month or 28-day period". Where the compared period is not itself monthly, the predicate lets the two counts refer to different months.
- **INV-075.** The Reading says a treated-attack line "lists adverse events only when it shows a drug-related adverse event". The predicate excludes adverse events only where the line shows that no drug-related adverse event occurred. A line that shows no result for that outcome may still list adverse events.

A script confirms both cases. Neither Reading has been raised before; both have been unchanged since v00/v01.

## Verification coverage

### Method

All downloads, texts and scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r40/`: `dl/<source>/`, `txt/<source>/` (page-by-page `pdftotext -raw` and `-layout`, and markup-stripped HTML/XML), `img/`, `scripts/` and `out/`. Every script was run with `python3 -I`.

**Fetching.**
- Every Source URL of `RATIONALE.md` (29 distinct URLs), the NICE TA260 Overview page and the nine Europe PMC `fullTextXML` texts were fetched with `curl`.
- The PMC HTML pages of S-014 and S-101 served real content this time (no reCAPTCHA) and were used as well.
- The Russian PDF 295_4 reset the connection once; the retry returned HTTP 200.
- ICHD-3 p. 190 and the S-034 title page were rendered with `pdftoppm` and read.

**Scripts.**
- **`parse_rat.py`** split `RATIONALE.md` into 440 entries: 113 Q, 232 D, 37 S, 12 W, 8 N, 3 X and 35 search-log entries. No ID is duplicated.
- **`check_quotes.py`** took the `Quote` field and every double-quoted string in the `Text` field of each Q entry, excluding translations, and split them at `[...]`. It searched each fragment in the texts behind the entry's own URLs in three passes:
  1. exact, with white space, quotes, dashes and ligatures normalised;
  2. with line-end hyphens joined;
  3. letters and digits only.

  It recorded the page of each hit. Fragments not found at the source were searched in Stage 1 v18.
- **`check_all.py`** ran the same search for every `[S-NNN] "…"` quote in all entries and in the model.

### Sources

| Source | URL used | Q entries | Fragments verified at the URL | Not found by script | Unreachable / notes |
|---|---|---|---|---|---|
| S-001 ICHD-3 | ichd-3.org PDF (211 pp.) | 28 | 59 (pp. 8, 9, 12, 42, 105, 122–125, 139, 190, 209, 210) | 3 | The A1.1 window fragments with "±" and "−" are glyphs without a text mapping. Read on the rendered p. 190: A1.1.1 B "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)", A1.1.2 B "Occurring on day 1 ± 2 (i.e. days −2 to +3)", note 2 of A1.1.1 |
| S-002 | ihs-headache.org PDF (19 pp.) | 2 | 3 (p. 12) | 0 | — |
| S-005 | ihs-headache.org PDF (14 pp.) | 2 | 2 (pp. 8, 9) | 0 | — |
| S-007 | UCL Discovery PDF (39 pp.) | 3 | 3 (pp. 10, 22, 25) | 0 | — |
| S-008 | univaq PDF (31 pp.) | 10 | 17 (pp. 5, 6, 9, 12, 13, 17) | 0 | — |
| S-010 | univaq PDF (11 pp.) | 13 | 18 (p. 6) | 0 | — |
| S-011 | Europe PMC XML, PMC9188162 | 8 | 9 | 0 | — |
| S-012 | Europe PMC XML, PMC9555163 | 1 | 1 | 0 | — |
| S-013 | Europe PMC XML, PMC7296705 | 2 | 2 | 0 | — |
| S-014 | Europe PMC XML and PMC page, PMC6734476 | 10 | 24 | 0 | Table 18 and "Scoring HALT" read in context |
| S-015 | NICE CG150 Recommendations and Overview pages | 15 | 28 | 0 | "Last updated: 03 June 2025"; Overview "Last reviewed: 23 September 2026" |
| S-016 | SIGN 155 PDF (64 pp.) | 3 | 5 (PDF p. 7 = printed p. 1; p. 20) | 0 | — |
| S-018 | AAN Clinician Summary PDF (12 pp.) | 4 | 5 (pp. 1, 7, 8) | 0 | — |
| S-022 | EMA draft PDF (17 pp.) | 3 | Stage 1 wording. The rebound sentence was found on p. 11 once the margin line numbers were stripped | 0 | — |
| S-023 | Europe PMC XML, PMC9607711 | 1 | 4 | 0 | — |
| S-028 | NVN module page | 2 | 5 | 0 | — |
| S-030 | DHOS PDF (86 pp.) | 3 | 2 (p. 19) | 0 | — |
| S-032 | brainmed.com page | 1 | the two Stage 1 Chinese strings found on the page | 0 | — |
| S-033 | Minzdrav PDF 295_4 (92 pp.) | 6 | 11 (pp. 1, 4, 18, 39, 40, 41, 53) | 0 | Connection reset once; retry OK. The section 3.3 recommendation that E-041/Q17 names is on p. 39 |
| S-034 | Minzdrav PDF 169_3 (53 pp.) | 6 | 6 (pp. 17, 52) | 1 | "Возрастная группа" + "дети" read on the rendered title page, which also shows "Год утверждения 2024" |
| S-035 | noroloji.org.tr PDF (92 pp.) | 11 | 18 (pp. 2, 6, 7, 22, 23, 48, 57, 77, 83, 86) | 0 | — |
| S-042 | Europe PMC XML, PMC12279330 | 1 | 1 | 0 | — |
| S-101 | Europe PMC XML and PMC page, PMC3057423 | 4 | 2 | 0 | — |
| S-102 | Europe PMC XML, PMC4406925 | 4 | 3 | 0 | — |
| S-103 | cincinnatichildrens.org PedMIDAS page | 3 | 12 (grading table) | 0 | Title "PedMIDAS Tool for Assessing Migraine Disability"; footer © 2026 |
| S-104 | Europe PMC XML, PMC183845 | 3 | 2 | 0 | — |
| S-105 | Joint Commission PDF (9 pp.) | 3 | 2 (P.6/9; the PHQ-9 sentence also on P. 5/9) | 0 | PDF metadata: created 2010-06-22, modified 2014-04-16, author Kurt Kroenke |
| S-106 | NICE TA260 chapter 2 and Overview | 2 | 1 (para 2.1) | 0 | Published 27 June 2012; last reviewed 11 January 2016 |

**Totals.**
- **Q-entry fragments:** 304 in all.
  - **Verified at the URL by script: 245.** Of these, 218 matched exactly, 12 after joining line-end hyphens and 15 on letters and digits only.
  - **Stage 1 wording, verbatim in Stage 1 v18: 54.** Those attributed to S-022 and S-032 were also found at their URLs.
  - **Not found by script: 5.**
    - 4 were verified on rendered pages (ICHD-3 p. 190, three fragments; S-034 title page).
    - 1 is an English translation inside a `Text` field: "7. Interventional procedures in migraine". Its original, "7. MİGRENDE GİRİŞİMSEL İŞLEMLER", is verified on p. 7.
- **`[S-NNN] "…"` quotes in all entries and in the model:** 130 fragments.
  - 97 were verified at the source and 25 are Stage 1 wording.
  - 8 were not found by script:
    - 3 are the same glyph and image cases;
    - 5 are pairings in which the script attached a quote to the source cited just before it. Each of the 5 is verified at its own source: S-008 pp. 5 and 9, S-035 p. 48, S-014, S-015 and S-033 p. 40.
- **No misquote, and no quote that cannot be read at its URL.** Every stated page or section matches the hit, or a later hit where the first is the table of contents (ICHD-3 pp. 4–6 against classification list pp. 8, 9 and 12).

**Translations.** Each was checked against the original and is faithful:
- E-041/Q15 (Dutch);
- E-041/Q16 to Q21 (Russian);
- E-041/Q22 to Q28, E-045/Q03 and Q04 (Turkish);
- ISS-10/Q00 (Russian);
- the Turkish and Russian quotes of E-041/N01.

**Metadata and versions.**
- **PubMed `esummary`.** It confirms authors, journal, year, volume, pages, DOI and PMC ID for S-101 (20819842), S-102 (25902814) and S-104 (12914662), and for the PedMIDAS developer paper (11739822, 10.1212/wnl.57.11.2034).
- **ICHD-3.** It is still current: only "ICHD-4 – Work in Progress 1" (2024) has been published ([fis.uke.de](https://fis.uke.de/portal/en/publications/international-classification-of-headache-disorders4--work-in-progress-1(b2e76945-6b60-4911-9c1f-583c088a2d4c)/export.html); [ihs-headache.org](https://ihs-headache.org/en/about-ihs/standing-committees/classification/)).
- **NICE.** CG150 was last updated on 3 June 2025, and TA260 is not superseded.

**Evidence pointers.**
- All 119 `[S-NNN] <entry>` pairs in the model's Evidence fields resolve to an entry whose Source lines include that source.
- All 370 entry IDs that the model names resolve.
- The Rationale cell of every source-data row names only entries that list that row under Concerns.

### Source data tables against their sources

Every formal cell agrees with its quote:
- **SD-IC.** The labels on ICHD-3 pp. 8, 9 and 12, including "2. Tension-type headache (TTH)" and "8.2 Medication-overuse headache (MOH)".
- **SD-CLS, SD-CMB, SD-FX-06.** 10 days/month for every class, 15 for non-opioid analgesics, 10 for 8.2.6, "> 3 months". `classesOf826` is 8.2.6 criterion B.
- **SD-FX.** Day 1 ± 2 (days −2 to +3, no day 0); a remission must "exceed three months"; review window 4–8 weeks; follow-up 12 months; shortest monthly period 28 days.
- **SD-ER-01 to SD-ER-18.** Each against E-041/Q00 to Q30.
- **SD-RC-01 to SD-RC-06.** NICE 1.3.28: 50 % and 30 %. NICE 1.3.29: 30 %. IHS Q6: 50 %, the 30 % chronic alternative, and the MIDAS and HIT-6 thresholds on p. 13. DMKG/ÖKSG/SKG. Russian section 7.1: 50 %.
- **SD-CL.** 0; < 4 for three months; 4–6; > 6, with insufficient control also admitted below six days.
- **SD-IN and SD-GB.**
  - HIT-6: 36–78, with bands ≤ 49, 50–55, 56–59 and 60–78.
  - MIDAS: grades I–IV with the [S-102] labels and bands 0–5, 6–10, 11–20 and ≥ 21; recall 3 months.
  - PedMIDAS: 0–10, 11–30, 31–50 and > 50.
  - HALT-90: Table 18, 0–5, 6–10, 11–20 and ≥ 20, with labels and grades as printed.
  - HALT-30: no grading.
- **SD-SR.** HADS 0–21 per subscale, PHQ-9 0–27, GAD-7 0–21.
- **SD-ET and SD-DF.** As Stage 1 states.

### Fidelity to Stage 1, requirement by requirement

| OUT | Parts and strength | Realised by (main items) | Result |
|---|---|---|---|
| 001 | period stated MUST; frequency per month or 28 days MUST; equal-length comparison MUST; Caveat (days visible) | E-003, E-005, INV-002, INV-003; C1-01, -02, -04, -06; INV-037, INV-038; `lengthDays` | ok |
| 002 | label SHOULD | INV-008 (`reports`), INV-111 | ok |
| 003 | SHOULD; SHOULD NOT | INV-011, INV-012, INV-121; C2-02 | ok |
| 004 | MUST; ICHD-3 definition | C1-01 (+ per type); INV-125 (SD-DF-01) | ok |
| 005 | MUST for patients with migraine; label SHOULD | C1-02; INV-008 | ok |
| 006 | SHOULD; MUST per month where provided | C1-03, C1-04; INV-008, INV-122 | ok |
| 007 | SHOULD; ICHD-3 definition | C1-05, C1-06; INV-125 (SD-DF-02) | ok |
| 008 | MAY | E-020 to E-022; C3-02; INV-104 (ISS-04) | ok |
| 009 | SHOULD series with markers; weekly where relevant | INV-034, INV-035, E-035 W2, INV-001 | ok |
| 010 | SHOULD on a stated scale; comparison | C1-07, E-023 `scale`, INV-032, INV-039 | ok |
| 011 | SHOULD; label; Caveat | C1-08, C3-03, C2-03 | ok |
| 012 | SHOULD across periods and per treated attack | C1-09, INV-076, `requiredOutcomes`, INV-069 | ok |
| 013 | MAY | E-019, E-024, E-027 | ok |
| 014 | MUST total, class, drug | C1-10 (`medicationKinds`), INV-024, INV-122, SD-CLS | ok |
| 015 | SHOULD weekly | C1-11 | ok |
| 016 | MUST indicator; MUST prompt; MUST NOT diagnosis | INV-044 to INV-046, SD-CLS, SD-CMB, SD-FX-06; C3-04; C2-04 | ok |
| 017 | SHOULD | INV-049 to INV-051, E-039, C3-06 | ok |
| 018 | MUST; Caveat | INV-053, INV-055 to INV-059, E-040/E-043 W2, SD-ER; C2-05 | ok |
| 019 | SHOULD | INV-060, INV-061; ISS-13 | ok in content. **R40-01 (a)**: INV-061 Reading |
| 020 | MAY; SHOULD; SHOULD NOT | E-045, E-046, INV-062 to INV-064, INV-114, INV-116; C2-06, C3-07 | ok |
| 021 | MUST; SHOULD | INV-102, INV-068, INV-069 | ok |
| 022 | SHOULD | INV-103, INV-070, INV-112, E-049 | ok |
| 023 | SHOULD; Caveat | INV-071 to INV-076, SD-ET; C2-07 | ok in content. **R40-01 (b)**: INV-075 Reading |
| 024 | SHOULD | INV-077 to INV-079, INV-109, E-054/E-055 W2 | ok |
| 025 | MAY | E-007 `schemeSelection`, E-056 (three content attributes, W2 definitional), INV-080 | ok (v39 change checked) |
| 039 | SHOULD | INV-066, INV-067, INV-109, INV-104 | ok |
| 026 | SHOULD | INV-081, INV-082, E-058, SD-IN, SD-GB; C3-08 | ok |
| 027 | SHOULD; comparison SHOULD | C1-12, INV-027 | ok |
| 028 | MUST; SHOULD; SHOULD NOT | INV-040 to INV-042; C2-08 | ok |
| 029 | MUST; SHOULD intensity | INV-118 (C1-01, -04, -06, -10 and their per-type instances by `byTypeCases`), C1-14, INV-122 | ok |
| 030 | MUST | INV-086, INV-087, INV-124, SD-FX-01/02 | ok |
| 031 | SHOULD | INV-088, INV-089, INV-124, SD-FX-07, SD-ET-01 | ok |
| 032 | MAY; caveats SHOULD | E-065, INV-110, C3-09 | ok |
| 033 | SHOULD; Caveat | INV-083, INV-085, SD-SR; C2-09, C3-10 | ok |
| 034 | SHOULD | INV-094, INV-104 | ok |
| 035 | SHOULD | INV-095, INV-105 | ok |
| 036 | SHOULD (a)–(d); Caveat | INV-096, INV-097, SD-ER-15, INV-055; C3-11 | ok |
| 037 | SHOULD NOT; SHOULD; SHOULD | INV-091; C3-12, E-033 W2, INV-092, INV-115; INV-093 | ok |
| 038 | SHOULD | C3-01, C3-05, C3-07 to C3-10; C2-01 | ok |

The ISS-03 list of statements that name migraine days without the OUT-005 condition matches a script search of all Stage 1 Statements: OUT-008, 018, 019, 022, 028, 030 and 035, plus OUT-002, 005, 007 and 021 as ISS-03 describes them.

### Mechanical checks (scripts in `scripts/`)

| Check | Result |
|---|---|
| Headings and IDs (`ids_trace.py`) | 67 E, 87 INV and 12 ISS headings; no duplicate. 0 E-, INV- or ISS- references are unresolved in the model or `RATIONALE.md`. There are 174 table rows (OC, C1–C3, SD-*), none duplicated, and 0 row references are unresolved. Section 9 holds 40 withdrawn IDs. |
| Traceability (`ids_trace.py`) | 39 rows, in Stage 1 order (OUT-039 after OUT-025). Elements and Invariants equal the reverse index of the Realises fields (0 differences). Catalogue rows equal the rows whose Realises cell names the requirement (0 differences). |
| Catalogue Realises (`ids_trace.py`) | Every requirement in a row's Realises cell is in the Realises field of an item, case row or source-data row named in the row (0 exceptions). |
| Audience column | Every "OUT-NNN: …" cell equals the Stage 1 Audience line verbatim (0 differences). |
| Declared names (`names.py`) | 830 declared names, none declared twice. Every identifier outside string literals is declared, a bound variable, or a table ID in `axiom table`. The three "undeclared" attribute selections (`after`, `eventDate`, `onTreatmentPeriod`) are an artefact of brace matching on E-049; they are declared there. |
| Level typing, composition, W2 (`attrs.py`) | 54 element types. Every SHOULD, MAY or conditional-MUST attribute has an `opt`, `set` or `seq` type. The only composition attributes are `Output.views` and `View.content`, as section 2.5 states. The 23 placement markers equal the section 6.0 marker table, and each is on a `→R` attribute. |
| Element Conformance "Definitional:" against invariant Conformance (`catdef.py`) | Seven asymmetries in index prose (see Checked and not raised). No level differs. |
| Scope sweep | input, record, answer, questionnaire, storage, database, JSON, XML, FHIR, algorithm, computed from, calculated, captured and reminder occur only in the exclusion statements, notation prose, instrument titles, the search log, the HALT-30 quote ("records days affected"), E-033/D01, E-057/D04 and N01, and INV-076/D01. No relation takes input data. Every threshold, formula and computed field shown with an output is present, with its source. |
| Witness (`witness40.py`, `out/witness40.txt`) | INV-061 holds for a residual burden whose migraine days are of January and whose moderate/severe days are of March, within a compared period of 1 January – 31 March 2026. INV-075 holds for a line that lists an adverse event and shows no drug-related-adverse-event result. The control line, which shows (drugRelatedAdverseEvent, false) and lists an adverse event, is rejected. |

## Remarks

### R40-01 Prose overclaim: the Readings of INV-061 and INV-075 state relations that their predicates do not have
- **Item(s):** INV-061 (Reading); INV-075 (Reading). Related: E-044, E-053.
- **Problem:** Both are definitional invariants. In each, the Reading states a relation that the predicate does not guarantee (PROCESS.md sections 6a and 9, "Prose overclaim").
  - **(a) INV-061.**
    - **What the Reading says.** "The residual burden shows migraine days and moderate/severe headache days, with the scope of the change, for one calendar month or 28-day period: the compared on-treatment period itself when that is a calendar month or 28-day period (as in every response comparison, INV-056), and otherwise one such period within the compared period."
    - **What the predicate says.** It quantifies separately over the two counts: `∀ m ∈ {rb.migraineDays, rb.moderateSevereHeadacheDays} • m.period.kind ∈ MonthlyKind ∧ within(m.period, rb.change.compared.period) ∧ (rb.change.compared.period.kind ∈ MonthlyKind ⇒ m.period = rb.change.compared.period)`. Where the compared period is not itself a calendar month or 28-day period, each count may refer to a different month within it.
    - **No other invariant ties the two periods.**
      - INV-060 places the two counts in the view of the change.
      - INV-003 places their periods there.
      - INV-062 concerns labels, whose comparisons are monthly.
    - **The case is reachable.** INV-060 (SHOULD) asks for a residual burden next to every percentage change in migraine or headache days whose compared period has at least 28 days, including changes outside response comparisons. An example is a change between two selected 90-day spans of an adult (INV-037, INV-053). The script admits, for a compared period of 1 January – 31 March 2026, a burden that shows the migraine days of January and the moderate/severe headache days of March. The Reading describes one month.
  - **(b) INV-075.**
    - **What the Reading says.** "it lists adverse events only when it shows a drug-related adverse event".
    - **What the predicate says.** Its conjunct is `AttackOutcomeResult(measure ↦ drugRelatedAdverseEvent, achieved ↦ false) ∈ l.results ⇒ l.adverseEvents = ∅`. It excludes adverse events only where the line shows that no drug-related adverse event occurred.
    - **The gap.** `results` is a set and may hold no result for `drugRelatedAdverseEvent`. A line that shows no such result may then list adverse events. The script admits such a line, and INV-075 holds for it.
    - **No other constraint closes the gap at the definitional level.**
      - INV-072 asks the lines of a summary's sequence to show every required outcome, but only at SHOULD.
      - E-053 `adverseEvents` constrains presence only, at SHOULD `when (drugRelatedAdverseEvent, true) ∈ self.results`.

      So under the definitional and MUST constraints, the line is admitted.
    - **The Reading fits neither reading.** Read with "shows" referring to the line's results, it claims more than the predicate. Read with the listed items themselves counting as "showing" an adverse event, it is vacuous, and it does not state the exclusion the predicate makes. Either way it does not say what the predicate says.
  - **History.**
    - The INV-075 Reading has been unchanged since v00 and the INV-061 Reading since v01 (R01-03).
    - A search of every review, fix, audit and oscillation file finds no remark or declined point on either sentence ("lists adverse events", "one calendar month", "one such period").
    - The INV-075 items discussed earlier are other matters: its formulation conjunct (moved to INV-123) and INV-075/D01 (declined in review 37).
  - **Watch points.**
    - The INV-061 point is distinct from watch point 1 (CHG-03 / ISS-13). That point concerns INV-060's antecedent and a per-month residual for compared periods shorter than 28 days. This remark concerns compared periods of at least 28 days that are not monthly.
    - Fix 01 (R01-03) kept "a monthly period within the compared period" for changes outside response comparisons and did not decide whether the two counts share that period.
    - No watch point names the INV-075 adverse-event conjunct. Check 24, watch point 6 and check 36's row on INV-075 concern its formulation tie.
    - So neither part reverses an earlier fix.
- **Evidence:**
  - The model text quoted above: INV-061 Predicate and Reading; INV-075 Predicate and Reading; E-053 `results : set AttackOutcomeResult core` and `adverseEvents … SHOULD when …`; INV-060; INV-072.
  - Stage 1 OUT-019: "the absolute number of migraine days and moderate/severe headache days per month that remain on treatment".
  - Stage 1 OUT-023: "drug-related adverse events after intake and whether the patient regarded them as meaningful".
  - The script output in `out/witness40.txt`.
- **Required change:**
  - **(a) INV-061. Preferred:** reword the Reading to what the predicate states, and leave the predicate byte-identical (watch point 1). For example: each of the two counts is of a calendar month or 28-day period with the scope of the change; it is the compared period itself where that is a calendar month or 28-day period, as in every response comparison (INV-056), and otherwise a period within the compared period, so the two counts may refer to different months.
    - **Alternative.** The fixer may hold that a residual burden "per month that remain on treatment" (OUT-019) is, by definition of E-044, the burden of one month. Then the fixer may instead add the definitional conjunct `sameSpan(rb.migraineDays.period, spanOf(rb.moderateSevereHeadacheDays.period))`.
    - It changes nothing where the compared period is monthly, and it touches neither INV-060 nor the ISS-13 question.
    - The fixer must argue that it excludes only outputs that contradict the element's definition (section 3.3, item 5).
  - **(b) INV-075. Preferred:** reword that clause of the Reading to what the conjunct states, for example "it lists no adverse event where it shows that no drug-related adverse event occurred".
    - **Alternative.** Replace the conjunct by `l.adverseEvents ≠ ∅ ⇒ AttackOutcomeResult(measure ↦ drugRelatedAdverseEvent, achieved ↦ true) ∈ l.results`. With the first conjunct (one result per measure), it implies the current one.
    - It would also exclude lines that list adverse events without showing that outcome, which no Stage 1 part forbids.
    - The fixer must argue that it is part of the definition of E-053.
  - **Class (PROCESS.md section 6a):** Readings that state a relation other than their predicate.
    - I read all 87 invariant Readings against their predicates, including every "only", "exactly", "one", "the same" and "never" phrase. These two are the only members I found. The fix should confirm this.
    - `RATIONALE.md` restates neither relation, so no entry needs to follow.

## Checked and not raised

- **The v39 change (R39-01).**
  - The three E-056 attributes are `set →…` at MAY with definitional placement.
  - INV-080's second conjunct is well typed (`m.period : →Period`, `spanOf(w)` for `w ∈ ran v.windows`). It is satisfiable with INV-003, INV-006, INV-121 and INV-122, and every v38 view is still admitted.
  - E-056 Meaning and Conformance, INV-080 Reading, the marker row, OC-30, the Realises fields and the OUT-025 row match the formal text.
  - E-056/D02, S01 and X01 agree with the model.
  - "INV-001 states no condition on [scheme windows]" is true, and consistent with INV-001/D01.
  - Windows beyond the as-of date fall under the settled point of check 24, watch point 10.
- **The "disability outputs" of OUT-025 read as instrument results (E-056/D02).** OUT-026's title names "disability", and OUT-027 is titled "Functional impact and lost productive time". The reading is stated in `RATIONALE.md`, functional-impact days may still be shown in the view (section 3.7), and the content is MAY. This is not a silent deviation, and no ISS is needed.
- **Element Conformance "Definitional:" lists against the invariants' Conformance fields.** There are seven asymmetries:
  - E-001 and E-030 name INV-123 and INV-121 respectively, which do not name them back;
  - E-014 does not name INV-123;
  - E-029 names INV-045;
  - E-040 names INV-111;
  - E-053 names INV-074;
  - E-057 does not name INV-082.

  Each named invariant does constrain the element, or the element defines a term the invariant uses. No level or constraint differs, and the fields are an index (section 3.3, item 5 attaches "definitional" to the invariant's field). Not raised.
- **Section 6.0 "Not marked:" list.** It omits E-032 `basis`, E-037 `values`, E-043 `values` and `changes`, E-052 `summary` and E-064 `bout`. The first four are placed through INV-003 (same period atom) or by E-040 W2. The last two carry no placement requirement. Section 2.5's claim ("Where a referenced atom must be shown in the holder's view, the model states it") holds.
- **HALT-90 total score.** "Scoring HALT" ([S-014]) says the graded total includes question 5, "a simple count for which the unit is not whole days". Table 18 heads the graded score "Days lost in last 3 months", and the total is still a whole number, so `wholeNumberScores` and the unit comment of E-058 agree with the source.
- **INV-075/D01 and INV-085/D01** explain conjuncts that v35 moved to INV-123. This was declined in review 37 after fix 35 (equivalence) kept their anchors; I have no new evidence.
- **Settled points, no new evidence:**
  - the monthly baseline of a response comparison (R01-03; review 19c);
  - control-level labels over mixed months (reviews 10, 19c, 33, 38);
  - 𝔹-valued functions and attributes used as formulas (review 22b);
  - periods beyond the as-of date (check 24, watch point 10);
  - no migraine days per headache type (INV-118/D02, D04);
  - the E-060 lead-in Meaning (checks 04 and 12);
  - MUST NOT for the OUT-018 Caveat (C2-05, since v00).
- **Satisfiability of the MUST layer.** I checked INV-003, INV-037, INV-040, INV-044 with INV-045 and INV-046, INV-055 to INV-059, INV-068, INV-086 with INV-087 and INV-124, INV-102, C1-01 to C1-10 with `byTypeCases`, C3-04 and SD-DF-01, together with the definitional invariants. No combination is unsatisfiable for an admissible context.
- **Stage 1 issues ISS-01 to ISS-06 and ISS-08 to ISS-13.** All are founded, and their Stage 1 passages are quoted and located correctly. ISS-04 now covers OUT-025's frequency outputs as well. I found no other Stage 1 issue that the model works around silently.
- **Watch points of the check after iteration 36.** R40-01 touches none of watch points 1 to 13 (see the remark).

## Notes on frozen items (for the human)

None. No item is frozen: `FROZEN_ITEMS.md` does not exist, and the model has no "Status: FROZEN" marker.
