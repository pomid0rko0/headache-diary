# Review — iteration 39
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v38
Date: 2026-10-22

## Summary

I reviewed v38 (`OUTPUT_MODEL.md` v38 with `RATIONALE.md` v38) on its own merits against Stage 1 v18 and the sources. I did not redo the v34 → v35 equivalence check. The snapshots `history/v38.md` and `history/v38-rationale.md` are byte-identical to the two files.

**Citations and source values hold.**
- Every quoted fragment of the 113 Q entries, and every `[S-NNN] "…"` quote in the D, N and X entries and in the model, is verbatim at the URL its entry names and at its stated location. The only differences are white space, line-end hyphens, glyphs without a text mapping and omitted footnote markers, each stated in the entry.
- Every value of the source data tables matches its source.
- The metadata of S-101 to S-106 is correct, and no newer version of a source changes an element.
- Every model Evidence pointer leads to an entry that holds the source it is cited with.

**The v38 changes hold.**
- `byTypeCases` and the second conjunct of INV-118 are well typed, satisfiable and at the level of OUT-029 (MUST).
- INV-118/D04's monotonicity claim is correct: every repertoire that met v37 C1-13 meets v38.
- INV-049 and INV-096 now bind the series granularity as section 3.4 states.
- ISS-10 now counts the nine sources of OUT-018 correctly: five adult-only, NICE from age 12, and three that also address children.
- No text still treats C1-13 as an active case.

**One remark.**
- **R39-01 (coverage gap / traceability / prose overclaim).** OUT-025 says the scheme-window view shows "the frequency, disability and treatment-history outputs for those windows". This statement part has no formal representation:
  - E-056 declares only the scheme name and the windows;
  - the E-056 Meaning claims that content anyway;
  - the OUT-025 traceability row is marked "full" but has no line for this part;
  - the Realises fields are inconsistent: responder labels (E-046) and instrument results (E-058) realise OUT-025, while no frequency element and no treatment-history element does.

  The content has been prose only since v00. v35 also dropped the v34 Conformance sentence that listed it. No earlier review, fix or watch point discussed it.

## Verification coverage

### Method

All downloads, extracted texts and scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r39/`:
- `dl/<hash>/`: one folder per URL;
- `txt/<hash>/`: page-by-page `pdftotext -raw` and `-layout` for PDFs, and markup-stripped text for HTML and XML;
- `scripts/`: the scripts, all run with `python3 -I`;
- `out/`: the results.

How the sources were fetched:
- Every Source URL of `RATIONALE.md` (29 URLs) was fetched with `curl`. The PMC HTML pages returned a reCAPTCHA page, so the nine PMC articles were read in their Europe PMC `fullTextXML` form, which model section 10 names.
- The Russian 169_3 PDF reset the connection once; the retry succeeded.
- ICHD-3 p. 190 and the S-034 title page were rendered with `pdftoppm` and read.

What the scripts did:
- **`parse_rat.py`** split `RATIONALE.md` into 437 entries: 113 Q, 231 D, 36 S, 12 W, 8 N, 2 X and 35 search-log entries. No ID is duplicated.
- **`check_quotes.py`** took the `Quote` field and every double-quoted string in the `Text` field of each Q entry, with translations excluded, and split them at `[...]`. It searched each fragment in the texts behind the entry's own URLs in three passes:
  1. exact, with white space, quote marks, dashes and ligatures normalised;
  2. with line-end hyphens joined;
  3. letters and digits only.

  It recorded the page of each hit. Fragments not found in a source were searched in Stage 1 v18.
- **`check_all_quotes.py`** did the same for every `[S-NNN] "…"` quote in every entry, D, N and X included, and in the model.

### Sources

| Source | URL used | Q entries | Fragments verified at the URL | Not found by script | Unreachable / notes |
|---|---|---|---|---|---|
| S-001 ICHD-3 | ichd-3.org PDF (211 pp.) | 28 | 59 (pp. 8, 9, 12, 105, 122–125, 139, 190, 209, 42) | 3 | The 3 are the A1.1 window fragments with "±" and "−", glyphs without a text mapping. Read on the rendered p. 190: "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)" (A1.1.1 B) and "Occurring on day 1 ± 2 (i.e. days −2 to +3)" (A1.1.2 B) |
| S-002 | ihs-headache.org PDF | 2 | 2 (p. 12 = journal p. 1037) | 0 | — |
| S-005 | ihs-headache.org PDF | 2 | 2 | 0 | — |
| S-007 | UCL Discovery PDF (39 pp.) | 3 | 3 (pp. 10, 22, 25) | 0 | — |
| S-008 | univaq PDF (31 pp.) | 10 | 17 (pp. 9, 12, 13, 17) | 0 | The Q6 Optimal list on p. 12 has exactly the three items that SD-RC-03 models |
| S-010 | univaq PDF (11 pp.) | 13 | 18 (p. 6) | 0 | — |
| S-011 | Europe PMC XML, PMC9188162 | 8 | 9 | 0 | PMC HTML: reCAPTCHA |
| S-012 | Europe PMC XML, PMC9555163 | 1 | 1 (the "failure to subcutaneous triptans …" fragment; the rest is Stage 1 text) | 0 | PMC HTML: reCAPTCHA |
| S-013 | Europe PMC XML, PMC7296705 | 2 | 2 | 0 | PMC HTML: reCAPTCHA |
| S-014 | Europe PMC XML, PMC6734476 | 10 | 24 | 0 | "Additional file 18 ))" spacing as the entry states |
| S-015 | NICE CG150 Recommendations and Overview pages | 15 | 28 (1.3.9, 1.3.24–1.3.29, 1.3.39, 1.3.48; Overview population sentence) | 0 | "Last updated: 03 June 2025"; Overview "Last reviewed: 23 September 2026" |
| S-016 | SIGN 155 PDF (64 pp.) | 3 | 5 (PDF p. 7 = printed p. 1; p. 20) | 0 | — |
| S-018 | AAN Clinician Summary PDF (12 pp.) | 4 | 5 (pp. 1, 7, 8) | 0 | — |
| S-022 | EMA draft PDF (17 pp.) | 3 | Stage 1 wording; the rebound sentence was also found on p. 11 once the margin line numbers were removed | 0 | — |
| S-023 | Europe PMC XML, PMC9607711 | 1 | 4 | 0 | — |
| S-028 | NVN module page | 2 | 5 | 0 | — |
| S-030 | DHOS PDF (86 pp.) | 3 | 2 (p. 19) | 0 | — |
| S-032 | brainmed.com page | 1 | the two Stage 1 Chinese strings were found on the page | 0 | — |
| S-033 | Minzdrav PDF 295_4 (92 pp.) | 6 | 11 (pp. 1, 4, 39, 40, 41, 53) | 0 | — |
| S-034 | Minzdrav PDF 169_3 (53 pp.) | 6 | 6 (pp. 17, 52) | 1 | The 1 is "Возрастная группа" … "дети" (E-041/Q20), read on the rendered image title page, which also shows "Год утверждения 2024" |
| S-035 | noroloji.org.tr PDF (92 pp.) | 11 | 18 (pp. 6, 7, 22, 23, 48, 57, 77, 83, 86) | 0 | — |
| S-042 | Europe PMC XML, PMC12279330 | 1 | 1 | 0 | PMC HTML: reCAPTCHA |
| S-101 | Europe PMC XML, PMC3057423 | 4 | 2 | 0 | PMC HTML: reCAPTCHA |
| S-102 | Europe PMC XML, PMC4406925 | 4 | 3 | 0 | PMC HTML: reCAPTCHA |
| S-103 | cincinnatichildrens.org PedMIDAS page | 3 | 12 (grading table) | 0 | Footer © 2026 |
| S-104 | Europe PMC XML, PMC183845 | 3 | 2 | 0 | PMC HTML: reCAPTCHA |
| S-105 | Joint Commission PDF (9 pp.) | 3 | 2 (P. 6/9; also P. 5/9). The developers sentence is on P. 8/9 | 0 | PDF metadata: created 2010-06-22, modified 2014-04-16, author Kurt Kroenke |
| S-106 | NICE TA260 chapter 2 page | 2 | 1 (para 2.1, last sentence) | 0 | Overview: published 27 June 2012, last reviewed 11 January 2016 |

**Totals.**
- **Q-entry fragments.** 297 in all.
  - **Verified at the URL by script: 243.** 215 matched on exact text, 11 after joining line-end hyphens and 17 on letters and digits only. I inspected each of the 17 in context: the differences are the unmapped "≥", omitted footnote markers, the "a≥30%" spacing, and the space that NICE's link markup puts before a full stop. No word or number differs.
  - **Verified on rendered pages: 4.** These are the 4 that the script did not find.
  - **Stage 1 wording, found verbatim in Stage 1 v18: 50.** Those attributed to S-012, S-022 and S-032 were also found at their URLs.
- **`[S-NNN] "…"` quotes in all entries and in the model.** 56 in all; every one was verified. The exceptions are the same as above: the image page, the unmapped glyphs, and the EMA line numbers. This includes the quotes inside E-041/N01: [S-035] p. 83 (both), [S-033] p. 41, and [S-011] "In selected cases …".
- **No misquote, and no quote that cannot be read at its URL.** Every stated page or section matches the hit, or a hit on a later page where the first hit is the table of contents.

**Translations.** Each was checked against the original and is faithful:
- E-041/Q15 (Dutch);
- E-041/Q16 to Q21 (Russian);
- E-041/Q22 to Q28, E-045/Q03 and Q04 (Turkish);
- ISS-10/Q00 (Russian);
- the Turkish and Russian quotes of E-041/N01.

**Metadata and versions.**
- **PubMed `esummary`.** It confirms authors, journal, volume, pages, DOI and PMC ID for S-101 (PMID 20819842), S-102 (25902814) and S-104 (12914662), and for the PedMIDAS developer paper (11739822, 10.1212/wnl.57.11.2034).
- **ICHD-3.** No ICHD-4 has been published. The latest is "International Classification of Headache Disorders-4 – Work in Progress 1" (Cephalalgia 2024), and the IHS lists an ICHD-IV workshop in September 2025 ([fis.uke.de](https://fis.uke.de/portal/en/publications/international-classification-of-headache-disorders4--work-in-progress-1(b2e76945-6b60-4911-9c1f-583c088a2d4c)/export.html), [ihs-headache.org](https://ihs-headache.org/en/about-ihs/standing-committees/classification/)).
- **S-004.** No fifth edition of the IHS acute trial guideline was found; the fourth edition (2019) is current ([PubMed 30806518](https://pubmed.ncbi.nlm.nih.gov/30806518/)).
- **S-022 and TA260.** S-022 is still the 2026 consultation draft (PDF created September 2026). TA260 is not superseded.

**Evidence pointers** (`evid.py`).
- All 121 `[S-NNN] <entry>` pairs in the model's Evidence fields resolve to an entry whose Source lines include that source.
- All 370 entry IDs that the model names resolve. The only exceptions are the generic patterns C1-NN/D01, C2-NN/D01 and C3-NN/D01 of section 4.4.
- The Rationale cell of every one of the 94 source-data rows names only entries that list that row under Concerns.

### Source data tables against their sources

Every formal cell agrees with its quote.
- **SD-IC.** The labels on ICHD-3 pp. 8, 9 and 12, including "2. Tension-type headache (TTH)" and "8.2 Medication-overuse headache (MOH)".
- **SD-CLS, SD-CMB and SD-FX-06.**
  - Levels: 10 days/month for every class, 15 for non-opioid analgesics, 10 for 8.2.6.
  - Span: "> 3 months", which gives four monthly periods (INV-045/D01, checked).
  - `classesOf826` matches 8.2.6 criterion B.
- **SD-FX.**
  - Window: day 1 ± 2, days −2 to +3, no day 0.
  - Remission: "must exceed three months".
  - Review window: 4–8 weeks.
  - Follow-up: 12 months.
  - Shortest monthly period: 28 days.
- **SD-ER-01 to SD-ER-18.** Every offset, anchor, timing, age coverage, type list and exclusion agrees with E-041/Q00 to Q30. I re-read:
  - NICE 1.3.24 to 1.3.29;
  - AAN 14A, 14B and 14H;
  - SIGN 4.1;
  - EHF question 3;
  - IHS Q2 (p. 9, Optimal and Essential, and the onabotulinumtoxinA comment that E-041/N01 lists);
  - NVN;
  - the Russian sections 3.3 and 7.1 and the paediatric flowchart;
  - Turkish Box 8, 3.6.3.9 (p. 57; the order of sentences matches the Q25 location) and 7.3.
- **SD-RC-01 to SD-RC-06.**
  - NICE 1.3.28: 50 % and 30 %. NICE 1.3.29: 30 %.
  - IHS Q6: the three list items on p. 12, the 30 % chronic alternative, and the AHS MIDAS and HIT-6 thresholds on p. 13.
  - DMKG: 50 % in episodic migraine, HIT-6 5 points, MIDAS 30 %.
  - Russian 7.1: 50 %.
- **SD-CL.** Levels 0; < 4 for three months; 4–6; > 6, with insufficient control also admitted below six days.
- **SD-IN and SD-GB.**
  - HIT-6: 36–78, with bands 36–49, 50–55, 56–59 and 60–78.
  - MIDAS: grades I–IV with the [S-102] labels and bands 0–5, 6–10, 11–20 and ≥ 21.
  - PedMIDAS: 0–10, 11–30, 31–50 and > 50.
  - HALT-90: 0–5, 6–10, 11–20 and ≥ 20.
  - Recall periods: 3 months for MIDAS, PedMIDAS and HALT-90; 1 month for HIT-6 and HALT-30.
- **SD-SR.** HADS 0–21 per subscale, PHQ-9 0–27, GAD-7 0–21.
- **SD-ET and SD-DF.** SD-ET gives 15 minutes for cluster headache. SD-DF gives MUST for OUT-004 and SHOULD for OUT-007.

### Fidelity to Stage 1, requirement by requirement

For each requirement, I checked the Statement and its constraining Caveats against the catalogue rows, case rows, elements and invariants that realise it, and each level against its Stage 1 part.

| OUT | Parts and strength | Realised by (main items) | Result |
|---|---|---|---|
| 001 | period stated MUST; frequency per month / 28 days MUST; equal-length comparison MUST; Caveat | E-003, E-005, INV-002, INV-003; C1-01, -02, -04, -06; INV-037, INV-038; `lengthDays` | ok |
| 002 | label SHOULD | INV-008 (`reports`), INV-111 | ok |
| 003 | SHOULD; SHOULD NOT | INV-011, INV-012, INV-121; C2-02 | ok |
| 004 | MUST; ICHD-3 definition MUST | C1-01 (+ per type by `byTypeCases`); INV-125 (SD-DF-01) | ok |
| 005 | MUST for patients with migraine; label SHOULD | C1-02; INV-008 | ok |
| 006 | SHOULD; MUST per month where provided; label | C1-03, C1-04; INV-008, INV-122 | ok |
| 007 | SHOULD; ICHD-3 definition | C1-05, C1-06; INV-125 (SD-DF-02) | ok |
| 008 | MAY | E-020 to E-022; C3-02; INV-104 (ISS-04) | ok |
| 009 | SHOULD series with markers; weekly where relevant | INV-034, INV-035, E-035 W2, INV-001 | ok |
| 010 | SHOULD on a stated scale; comparison | C1-07, E-023 `scale`, INV-032, INV-039 | ok |
| 011 | SHOULD, label; Caveat SHOULD NOT | C1-08, C3-03, C2-03 | ok |
| 012 | SHOULD across periods and per treated attack | C1-09, INV-076, `requiredOutcomes`, INV-069 | ok |
| 013 | MAY | E-019, E-024, E-027 | ok |
| 014 | MUST total, class, drug | C1-10, INV-024, INV-122, SD-CLS | ok |
| 015 | SHOULD weekly | C1-11 | ok |
| 016 | MUST indicator; MUST prompt; MUST NOT diagnosis | INV-044 to INV-046, SD-CLS, SD-CMB, SD-FX-06; C3-04; C2-04 | ok |
| 017 | SHOULD | INV-049, INV-050, INV-051, E-039, C3-06 | ok (v38 INV-049 checked) |
| 018 | MUST; Caveat MUST NOT | INV-053, INV-055 to INV-059, E-040/E-043 W2, SD-ER; C2-05 | ok |
| 019 | SHOULD | INV-060, INV-061; ISS-13 | ok |
| 020 | MAY; SHOULD; SHOULD NOT | E-045, E-046, INV-062 to INV-064, INV-114, INV-116; C2-06, C3-07 | ok |
| 021 | MUST; SHOULD | INV-102, INV-068, INV-069 | ok |
| 022 | SHOULD | INV-103, INV-070, INV-112, E-049 | ok |
| 023 | SHOULD; Caveat | INV-071 to INV-076, SD-ET; C2-07 | ok |
| 024 | SHOULD | INV-077 to INV-079, INV-109, E-054/E-055 W2 | ok |
| 025 | MAY | E-056, INV-080 | **R39-01** (content for the windows not represented; row "full") |
| 039 | SHOULD | INV-066, INV-067, INV-109, INV-104 | ok |
| 026 | SHOULD | INV-081, INV-082, E-058, SD-IN, SD-GB | ok |
| 027 | SHOULD; comparison SHOULD | C1-12, INV-027 | ok |
| 028 | MUST; SHOULD; SHOULD NOT | INV-040 to INV-042; C2-08 | ok |
| 029 | MUST; SHOULD intensity | INV-118 (C1-01, -04, -06, -10 and their per-type instances by `byTypeCases`), C1-14, INV-122 | ok (v38 checked) |
| 030 | MUST | INV-086, INV-087, INV-124, SD-FX-01/02 | ok |
| 031 | SHOULD | INV-088, INV-089, INV-124, SD-FX-07 | ok |
| 032 | MAY; caveats SHOULD | E-065, INV-110, C3-09 | ok |
| 033 | SHOULD; Caveat | INV-083, INV-085, SD-SR; C2-09, C3-10 | ok |
| 034 | SHOULD | INV-094, INV-104 | ok |
| 035 | SHOULD | INV-095, INV-105 | ok |
| 036 | SHOULD (a)–(d); Caveat | INV-096, INV-097, SD-ER-15, INV-055; C3-11 | ok (v38 INV-096 checked) |
| 037 | SHOULD NOT; SHOULD; SHOULD | INV-091; C3-12, E-033 W2, INV-092, INV-115; INV-093 | ok |
| 038 | SHOULD | C3-01, C3-05, C3-07 to C3-10; C2-01 | ok |

### Mechanical checks (scripts in `scripts/`)

| Check | Result |
|---|---|
| Headings and IDs (`ids_trace.py`) | 67 E, 87 INV and 12 ISS headings; no duplicate. In the model and `RATIONALE.md`, 0 E-, INV- or ISS- references are unresolved. A withdrawn ID appears only in "Replaces" notes, section 9, the ISS-07 sentence, and "v34 …" or "Origin in v34" text in `RATIONALE.md`. There are 174 table rows (OC, C1–C3, SD-*), none duplicated, and 0 row references are unresolved. C1-13 appears only as withdrawn. |
| Traceability and catalogue (`ids_trace.py`) | 39 rows, in Stage 1 order (OUT-039 after OUT-025). The Elements and Invariants columns equal the union of the Realises fields (0 differences). The Catalogue-rows column equals the rows whose Realises name the requirement (0 differences). Two coverage lines name items outside their columns: INV-104 in OUT-008 and INV-069 in OUT-012. Both are known and were left by reviews 36 to 38. |
| Audience column | Every "OUT-NNN: …" cell equals the Stage 1 Audience line verbatim. |
| Declared names (`names.py`) | Every applied function or predicate, every capitalised identifier and every selected attribute in the `omn` blocks and formal cells is declared. The residue is sequence applications (`rc.onTreatment(i)`), bound variables and table IDs. |
| Levels | 11 MUST invariants; each realises a MUST part. INV-055 also cites OUT-036 (SHOULD), with OUT-018 as its MUST part. INV-091 is SHOULD NOT. The four level-indexed invariants' cases follow their Stage 1 parts. The `byTypeCases` instances are MUST, which is OUT-029's level for frequency and acute-medication outputs per type. |
| v37 → v38 diff | Five `omn` blocks changed: section 4.4, the E-029 comment, INV-049, INV-096 and INV-118. C1-13 is withdrawn. In `RATIONALE.md`, INV-118/D04, INV-049/D02 and INV-096/D02 are new, and six moved texts were re-pointed to `byTypeCases`. The change-log entry is accurate. |
| `byTypeCases` monotonicity (INV-118/D04) | Checked by hand. v37 C1-13 had one pair per scope, whose kinds were {HeadacheDays} ∪ `medicationKinds(c)` ∪ the provided moderate/severe and attack kinds, at a g₀ ∈ `MonthlyKind`. The v38 per-type instance of each case in `byTypeCases` is met at the same g₀ ∈ `ppGranularities`, because `reportedTogether` is monotone in its kinds. The claim holds. |
| Use of the selected granularity | `tiles(…, c.granularity)` occurs only under a preceding `∃ g` (INV-034, INV-044, INV-096, INV-118), under `calendarWeek ∧ weeklyGranularityRelevant` (INV-034), or in INV-001. |
| Scope sweep | The terms enter, record, input, answer, questionnaire, stored, storage, database, JSON, XML, FHIR, algorithm, computed from, derived from and calculated occur only in these places: exclusion statements, notation prose, instrument titles, the search log, the HALT-30 quote ("records days affected"), E-018/Q02's note that the [S-010] day definitions are not quoted, and INV-076/D01's reason for not assigning lines to types. No relation takes input data. Every threshold, formula and computed field that is shown with an output is present. |
| Date arithmetic of worked examples | All correct: E-042/W01–W02, INV-055/W01 (including the 30 March stop), INV-049/W01 (day 43, range ending 6 April), INV-079/W01 (41 and 294 days), E-063/W01 (42 and 143 days), E-007/D01 (67 days) and INV-105/D02 (43 days). |
| View content (for R39-01) | Each view subtype was checked for formal content behind its Meaning: E-035 (INV-035), E-038 (INV-040, INV-041), E-039 (INV-050), E-048 (INV-068, INV-069), E-049 (INV-070), E-054 (INV-078), E-060 (INV-087), E-062 (attributes), E-065 (attributes), E-066 (INV-104), E-067 (INV-105). E-056 is the only one with none. |

## Remarks

### R39-01 Coverage gap / traceability / prose overclaim: the outputs that OUT-025 asks for "for those windows" have no representation, while the OUT-025 row claims full coverage
- **Item(s):** E-056 (Definition, Meaning, Conformance); traceability row OUT-025; OC-30. Related: the Realises fields of E-046 and E-058 (OUT-025), and of the frequency and treatment-history elements (E-014 to E-019, E-054, E-055: no OUT-025).
- **Problem:**
  - **What Stage 1 states.** OUT-025 has these statement parts, at MAY:
    1. the clinician can select evaluation windows defined by a scheme;
    2. the diary can "show the frequency, disability and treatment-history outputs for those windows";
    3. they are "labelled with the name of the scheme".
  - **What the model represents.**
    - Part 1: the context's `schemeSelection`, and INV-080.
    - Part 3: `scheme` "shown as the label of the view", and INV-080.
    - Part 2 has no formal representation. `SchemeWindowView` declares only `scheme` and `windows`. No attribute, case or definitional invariant states that the view shows frequency values, disability results or treatment-history content, or that any value it shows refers to its windows. A view with these two attributes and no other content is an instance of E-056 as defined.
    - Every other view subtype states its content formally, through attributes or a content or definitional invariant (see the mechanical check "View content"). E-065, also MAY, declares its content as core attributes. E-056 is the only one with none.
  - **Prose overclaim** (PROCESS.md sections 6a and 9). The E-056 Meaning reads "Frequency, disability and treatment-history outputs for evaluation windows defined by a national reimbursement or monitoring scheme …, labelled with the name of the scheme". The formal text guarantees none of this content.
  - **Traceability is wrong and incomplete.**
    - The OUT-025 row reads "full", with the single line "evaluation windows of a scheme, labelled with the scheme (MAY): E-056, INV-080". Section 7 defines "full" as every observable property of the Statement represented, "with one line per statement part"; part 2 has no line.
    - The row's columns also list E-046 (responder labels) and E-058 (instrument results), and the catalogue rows OC-23 and OC-31. These kinds realise OUT-025 only through their Realises fields, and no item ties them to a scheme-window view or to its windows.
    - The frequency elements (E-014 to E-019) and the treatment-history elements (E-054, E-055), which part 2 names equally, do not list OUT-025 at all.
  - **History; not a reversal.**
    - From v00 to v34, E-056's Conformance said in prose: "Its content (headache days and migraine days per window, instrument results, treatment lines, responder labels) is MAY". This was never formalised.
    - v35 dropped that sentence. The v35 mapping records E-056 as "kept; formal text unchanged".
    - No review, fix, audit or oscillation check discussed what the view shows for its windows. A search of every loop file for E-056, SchemeWindowView, "scheme-window view" and OUT-025 found only availability checks ("MAY scheme-window view labelled with the scheme … OK") and the placement of `SchemeWindowView.windows` by INV-003 (fix 11).
    - No watch point names E-056, INV-080 or OUT-025.
- **Evidence:**
  - Stage 1 OUT-025 Statement: "The diary output MAY allow the clinician to select evaluation windows defined by national reimbursement or monitoring schemes (for example specified treatment weeks, the three months preceding an application, month-by-month responder views, or six-monthly reassessments) and to show the frequency, disability and treatment-history outputs for those windows, labelled with the name of the scheme." Its Evidence quotes scheme criteria that need exactly these outputs for the windows:
    - [S-039] "the number of migraine days in treatment weeks 9-12" and "information on previous migraine treatment and its results";
    - [S-040] "at least 8 days of disabling migraine per month [defined as a MIDAS questionnaire score ≥11]".
  - Model: E-056 (`element SchemeWindowView extends View { scheme : SchemeName core; windows : seq1 →Period core }` and its Meaning); INV-080 (windows and scheme only); section 7 heading text ("one line per statement part") and row OUT-025; the Realises fields of E-046 and E-058 against those of E-014 to E-019, E-054 and E-055.
  - PROCESS.md section 4 ("Every observable property in a Stage 1 Statement must be represented: what is reported, per what period …") and section 3.2 of the model ("MAY constraints impose nothing: they state that the content is permitted and fix its type and meaning").
- **Required change:**
  - **(a) Preferred.** Represent the content of the view formally, at MAY, so that its type and meaning are fixed without asking for anything.
    - **The content.** For example, add reference attributes of level MAY, each with a definitional `shown` marker or with placement by INV-003:
      - the frequency outputs for the windows: per-period values of the frequency measures, whose periods have the dates of one of the view's windows;
      - the disability outputs: instrument results;
      - the treatment-history outputs: treatment lines, class groups or a history view.
    - **The tie.** Extend the definitional INV-080 by the tie of each frequency value to a window (`∃ w ∈ ran v.windows • sameSpan(m.period, spanOf(w))`). Tie disability and history content to the windows only as far as OUT-025's "for those windows" can be read without inventing scheme rules.
    - **Prose and traceability.** Then:
      - align the E-056 Meaning and Conformance;
      - make the Realises fields consistent, so that the OUT-025 trace runs through E-056's content and not only through E-046 and E-058;
      - give the OUT-025 row a line for "frequency, disability and treatment-history outputs for those windows (MAY)".
    - **Constraints on the fix.** No scheme criterion may enter the model (OUT-025 Caveats; E-045/N02, E-056/D01).
  - **(b) Only if the fixer can show that the content cannot be represented without narrowing OUT-025.**
    - Reduce the E-056 Meaning to what the formal text states.
    - Mark the OUT-025 coverage "partial", with the reason in a `RATIONALE.md` entry.
    - Remove OUT-025 from the Realises fields of E-046 and E-058, or explain why those two kinds, and not the frequency and history kinds, realise it.
  - **Class (PROCESS.md section 6a).** The class is "a view kind whose Stage 1 content is stated only in prose". I checked every view subtype; E-056 is the only member. A fix should confirm this.

## Checked and not raised

- **The v38 changes.** The second conjunct of INV-118 and `byTypeCases` are well typed:
  - `const byTypeCases : set (CatalogueRow × Level)` is a defined constant (section 2.3);
  - `(r, l) ∈ byTypeCases` is guarded;
  - `ofType(t)` is applied to a `HeadacheType`;
  - the instances for l ≠ must are vacuous.

  The Conformance, Evidence and Notes fields, OC-35, E-029, section 3.4, section 4.2, the ISS-09 Effect, section 9 and the change log all match the predicate. C1-14 (intensity per type) differs from a per-type instance of C1-07 only by the scale filter and the "where provided" condition. At SHOULD, these ask the same thing, because E-023 `scale` is SHOULD and C1-07 makes intensity provided (INV-118/D04). This is not a "rule stated per case" with different content.
- **E-015, E-017 and E-019 Conformance fields.** They do not name the per-type MUST instances that `byTypeCases` adds, while E-029's does. No level differs, and INV-118 Conformance and OC-35 state these instances. The same asymmetry existed with C1-13 in v37. Not raised.
- **E-039 short follow-up views.** For a covered period shorter than 28 days that begins on a calendar week, E-039 still asks for a weekly series, and INV-104 and INV-105 do the same for short covered periods. This is the settled `fillsPeriod` design (checks 08, 12 and 24 watch points). INV-049/D02 states it, and fix 38 considered it explicitly. No new evidence; not raised.
- **Section 3.4, "Their availability per calendar month or 28-day period is stated by INV-118 (…), INV-037 and INV-057".** INV-037 asks for the frequency measures, MUST where provided, for any selected equal-length periods, which may be calendar months or 28-day periods. Read so, the sentence holds, and SEC-3.4/D01 states the reading precisely. Not raised.
- **INV-076/D01.** Treated-attack lines carry no type attribute. That INV-076 asks for migraine-associated symptom status on every line of a subject with migraine, including lines of a cluster-scoped summary, follows the settled reading of "For migraine" as a subject condition (C1-09) and of the outcome set with the 15-minute time point (reviews 01 and 14). Not raised.
- **OUT-024 Caveat ("does not by itself establish eligibility")** and **OUT-031 Caveat.** Settled as descriptive (fix 01; reviews 19c, 21b and 35). No new evidence.
- **R-MCF clause 3.** A `PeriodComparison` or `ClinicianSummary` that matches no selection is admitted. As review 38 found, it is not content for a selection. Not raised.
- **INV-110/S01.** It lists C3-09 twice and names cases (C3-05, C3-07, C3-08, C3-10) whose bearers a trigger view is not. The claim that the annotations "can be added whatever the covered period is" stays true. Not raised.
- **OC-33 Audience cell.** It lists "OUT-010, OUT-027" without their Audience text. The catalogue is an index without formal force (section 4.2), and other rows also list only the main requirement's Audience. Not raised.
- **Stage 1 issues ISS-01 to ISS-06 and ISS-08 to ISS-13.** All are founded, with correct locations and descriptions. In particular, ISS-10 now counts nine sources: AAN/AHS, SIGN, EHF 2022, the Russian adult guideline and [S-002] are adult-only; NICE covers age 12 and up; IHS 2024, NVN and the Turkish protocol also address children. No other Stage 1 issue is silently worked around.
- **Watch points of the check after iteration 36.** R39-01 touches no watched item: E-056, INV-080 and OUT-025 appear in none of watch points 1 to 13. It reverses no earlier fix, because the content of the scheme-window view was never decided.

## Notes on frozen items (for the human)

None. No item is frozen: `FROZEN_ITEMS.md` does not exist, and the model has no "Status: FROZEN" marker.
