# Review — iteration 41
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v40
Date: 2026-10-22

## Summary

I reviewed v40 (`OUTPUT_MODEL.md` v40 with its companion `RATIONALE.md` v39, unchanged in v40) on its own merits against Stage 1 v18 and the sources. I did not redo the v34 → v35 equivalence check or fix 39's sweep of v34 prose. I read PROCESS.md, Stage 1 sections 1–3 in full, the whole model, the whole of `RATIONALE.md`, review 40, fix 40, the oscillation checks after iterations 36 and 40 (with their watch points) and the earlier reviews and fixes where a candidate point touched them.

**Citations and source values hold.**
- Every quoted fragment of the 113 Q entries is verbatim at the URL its entry names, at its stated page or section. The only differences are white space, line-end hyphens, glyphs without a text mapping (ICHD-3 "≥", "±", "−"), the EMA margin line numbers and the image-only title page of [S-034], which I read on the rendered page.
- The 17 translations are faithful.
- Every value of the source data tables (SD-IC, SD-DF, SD-CLS, SD-CMB, SD-FX, SD-ER, SD-RC, SD-CL, SD-IN, SD-GB, SD-SC, SD-SR, SD-ET) agrees with its quote.
- The metadata of S-101 to S-106 is correct, and no newer version of a source changes an element.

**The v40 change holds.** The INV-061 and INV-075 Readings now state their predicates; the diff from v39 is the two Readings, the header and the change-log entry only.

**Stage 1 fidelity, formal soundness and scope** check out: every OUT requirement is represented at its Stage 1 levels, the mechanical checks are clean, and no relation takes input data.

**One remark (R41-01, prose overclaim: `RATIONALE.md` disagrees with the model).** INV-076/D01 justifies INV-076 by stating that treated-attack lines "are not assigned to headache types, because such an assignment would be a derivation from input". The model contradicts both halves. Type scope is an output property of every per-period value, an acute-treatment summary included. The cluster view's required 15-minute summaries are, by the model's own Readings, summaries of the subject's cluster-headache attacks only, and they list those attacks as their lines. So, for a subject with migraine and cluster headache, INV-076 asks the migraine-associated symptoms of lines that the output itself presents as cluster-headache attacks, a consequence the entry neither states nor justifies. The remark asks for the entry to be corrected (preferred, no formal change); it touches no watch point.

## Verification coverage

### Method

All downloads, texts and scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r41/` (`dl/<source>/`, `out/`, `img/`, `scripts/`). Every script was run with `python3 -I`.
- **Fetching.** Every Source URL of `RATIONALE.md` (28 distinct documents) was fetched with `curl` through the proxy, all HTTP 200; the brainmed.com page reset the connection once and returned 200 on the retry. The nine PMC sources were also fetched as Europe PMC `fullTextXML`. The NICE TA260 Overview page was fetched for its dates.
- **Text.** `totext.py` produced page-by-page `pdftotext -raw` and `-layout` texts of every PDF and markup-stripped texts of every HTML and XML page.
- **`verify.py`** took the `Quote` field and every double-quoted string of the `Text` field of each Q entry, split them at `[...]`, and searched each fragment in the texts behind the entry's own Source lines in three passes (exact with white space and ligatures normalised; with quotes, dashes, line-end hyphens and the three unmapped glyphs normalised; letters and digits only), recording the page. Fragments not found at the source were searched in Stage 1 v18.
- **`verify_all.py`** searched every `[S-NNN] "…"` quote in all entries and in the model; **`allquotes.py`** searched every double-quoted string of 20 or more letters and digits in both files against all downloaded sources and Stage 1.
- **`ctx.py`** printed the source context of every match below the exact pass; **`jats_loc.py`** located the JATS quotes in their section paths.
- The title page of [S-034] was rendered with `pdftoppm` and read: "Возрастная группа" "дети", "Год утверждения 2024".

### Sources

| Source | URL used | Q entries | Fragments verified at the URL | Not found by script | Unreachable / notes |
|---|---|---|---|---|---|
| S-001 ICHD-3 | ichd-3.org PDF, 211 pp. | 28 | 61 (pp. 8, 9, 12, 42, 105, 122–125, 139, 190, 209, 210) | 0 | 14 matched on letters and digits only: the "≥", "±", "−" glyphs and line-end breaks that the entries state. Classification labels confirmed on pp. 8, 9 and 12 (the first hits on pp. 4–6 are the table of contents) |
| S-002 | ihs-headache.org PDF, 19 pp. | 2 | 2 (p. 12) | 0 | — |
| S-005 | ihs-headache.org PDF, 14 pp. | 2 | 2 (p. 9) | 0 | — |
| S-007 | UCL Discovery PDF, 39 pp. | 3 | 3 (pp. 10, 22, 25) | 0 | — |
| S-008 | univaq PDF, 31 pp. | 10 | 17 (pp. 1, 4, 5, 6, 9, 12, 13, 17, 24, 26) | 0 | "≥ 50%" and "a≥30%" spacing differs in the text layer only |
| S-010 | univaq PDF, 11 pp. | 13 | 18 (p. 6) | 0 | The Insufficient Control sentence is split by the running header, as E-046/Q04 states |
| S-011 | Europe PMC XML, PMC9188162 | 8 | 9 | 0 | Background paragraphs and the question 3 clinical guidance located by section path |
| S-012 | Europe PMC XML, PMC9555163 | 1 | 1 | 0 | Results > Consensus > Definition of triptan failure |
| S-013 | Europe PMC XML, PMC7296705 | 2 | 2 | 0 | Discussion > Drug failure; Discussion > Assessment of patients |
| S-014 | Europe PMC XML, PMC6734476 | 10 | 23 | 0 | Table 18 and "Scoring HALT" read in context |
| S-015 | NICE CG150 Recommendations and Overview pages | 15 | 27 | 0 | Recommendations "Last updated: 03 June 2025"; Overview "Last reviewed: 23 September 2026" (links to technology appraisals added; no quoted recommendation changed) |
| S-016 | SIGN 155 PDF, 64 pp. | 3 | 5 (PDF p. 7 = printed p. 1; p. 20) | 0 | Whole text searched for further time points: none |
| S-018 | AAN Clinician Summary PDF, 12 pp. | 4 | 5 (pp. 1, 7, 8) | 0 | Recommendations 14A–14H read in full |
| S-022 | EMA draft PDF, 17 pp. | 3 | Stage 1 wording; the rebound sentence is on p. 11, interleaved with margin line numbers 383–384 | 0 | — |
| S-023 | Europe PMC XML, PMC9607711 | 1 | 4 | 0 | — |
| S-028 | NVN module page | 2 | 5 | 0 | — |
| S-030 | DHOS PDF, 86 pp. | 3 | 2 (p. 19) | 0 | — |
| S-032 | brainmed.com page | 1 | the three Stage 1 Chinese strings found on the page | 0 | Connection reset once; retry OK |
| S-033 | Minzdrav PDF 295_4, 92 pp. | 6 | 11 (pp. 1, 4, 5, 18, 39, 40, 53) | 0 | — |
| S-034 | Minzdrav PDF 169_3, 53 pp. | 6 | 5 (pp. 17, 52) | 1 ("Возрастная группа", image) | Read on the rendered title page |
| S-035 | noroloji.org.tr PDF, 92 pp. | 11 | 18 (pp. 2, 6, 7, 22, 23, 48, 57, 86) | 0 | — |
| S-042 | Europe PMC XML, PMC12279330 | 1 | 1 | 0 | — |
| S-101 | Europe PMC XML, PMC3057423 | 4 | 2 (Methods > Data sources) | 0 | — |
| S-102 | Europe PMC XML, PMC4406925 | 4 | 3 (Methods > Migraine-related disability) | 0 | — |
| S-103 | cincinnatichildrens.org PedMIDAS page | 3 | 11 (grading table) | 0 | Title "PedMIDAS Tool \| Headache Center", heading "PedMIDAS Tool for Assessing Migraine Disability", footer © 2026 |
| S-104 | Europe PMC XML, PMC183845 | 3 | 2 (Discussion > Construction of the HADS) | 0 | — |
| S-105 | Joint Commission PDF, 9 pp. | 3 | 2 (P.6/9; the PHQ-9 sentence also on P. 5/9) | 0 | PDF metadata: author Kurt Kroenke, created 2010-06-22, modified 2014-04-16; developers sentence on P.8/9 |
| S-106 | NICE TA260 chapter 2 and Overview | 2 | 1 (para 2.1) | 0 | Published 27 June 2012; last reviewed 11 January 2016 |

**Totals.**
- **Q-entry fragments: 301.**
  - Verified at the URL by script: **241** (211 exact, 11 after normalising quotes, dashes, hyphens and glyphs, 19 on letters and digits only, each read in context).
  - Stage 1 wording, verbatim in Stage 1 v18: **51** (those attributed to S-022 and S-032 also found at their URLs).
  - Not found by script: **9**. One is verified on the rendered [S-034] title page; four are English translations inside `Text` fields (E-041/Q00, E-045/Q03, E-045/Q04, ISS-10/Q00), whose originals are verified; three are script artefacts (text between two quotes); one is the Stage 1 OUT-009 phrase quoted in INV-001/Q00 with a lower-case initial "where" (see Checked and not raised).
- **`[S-NNN] "…"` quotes in all entries and the model, and every long quoted string:** all found at their source or in Stage 1, apart from translations, the image case and script artefacts.
- **No misquote, no quote unreadable at its URL, no wrong location.**

**Translations (17), all faithful:** E-041/Q15 (Dutch); E-041/Q16 to Q21 (Russian); E-041/Q22 to Q28, E-045/Q03 and Q04 (Turkish); ISS-10/Q00 (Russian); the three Turkish and one Russian quotes of E-041/N01.

**Metadata.** Europe PMC metadata confirms authors, title, journal, year, volume, pages, DOI, PMID and PMCID of S-101 (20819842), S-102 (25902814) and S-104 (12914662), and of the PedMIDAS developer paper cited in S-103 (11739822, 10.1212/wnl.57.11.2034).

**Evidence pointers.** All 370 entry IDs that the model names exist; every `[S-NNN] <entry>` pair in an Evidence field names an entry whose Source lines include that source; every Rationale cell of a source-data row names entries that list the row under Concerns and hold its quote.

### Source data tables against their sources

- **SD-IC:** the 15 labels as printed on ICHD-3 pp. 8, 9 and 12.
- **SD-CLS, SD-CMB, SD-FX-06:** 10 days/month for ergotamine, triptans, opioids, combination analgesics and other medication (8.2.8), 15 for non-opioid analgesics, 10 for 8.2.6 over the four classes of its criterion B, "> 3 months"; `classesOf821to825` is 8.2.6 note 2.
- **SD-FX:** day 1 ± 2 (days −2 to +3, no day 0); a remission must "exceed three months"; review window 4–8 weeks; 12 months; 28 days.
- **SD-ER-01 to SD-ER-18:** each guidance, population, type, exclusion, anchor, timing and offset against E-041/Q00 to Q30 and the AAN, SIGN, IHS, NVN, Russian and Turkish texts.
- **SD-RC-01 to SD-RC-06:** NICE 1.3.28 50 %/30 %; NICE 1.3.29 30 % of headache days; IHS Q6 50 %, the 30 % chronic alternative, MIDAS ≥ 5 points for baseline 11–20 and ≥ 30 % for baseline ≥ 20, HIT-6 ≥ 5 points (p. 13); DMKG/ÖKSG/SKG; Russian section 7.1 50 % of headache days.
- **SD-CL:** 0; < 4 for three months; 4–6; > 6, insufficient control also admitted below six.
- **SD-IN, SD-GB:** HIT-6 36–78 with bands ≤ 49, 50–55, 56–59, 60–78; MIDAS grades I–IV with the [S-102] labels, 0–5, 6–10, 11–20, ≥ 21, recall 3 months; PedMIDAS 0–10, 11–30, 31–50, > 50 with the page's labels; HALT-90 Table 18 with its labels, grades and the "≥20" overlap; HALT-30 1 month (30 days), no grading.
- **SD-SR:** HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
- **SD-ET, SD-DF:** as Stage 1 states.

### Fidelity to Stage 1, requirement by requirement

| OUT | Parts and strength | Realised by (main items) | Result |
|---|---|---|---|
| 001 | period stated MUST; frequency per month or 28 days MUST; equal-length comparison MUST; Caveat (days visible) | E-003, E-005, INV-002, INV-003; C1-01, -02, -04, -06; INV-037, INV-038; `lengthDays` | ok |
| 002 | label SHOULD | INV-008 (`reports`), INV-111 | ok |
| 003 | SHOULD; SHOULD NOT | INV-011, INV-012, INV-121; C2-02 | ok |
| 004 | MUST; ICHD-3 definition MUST | C1-01 (+ per type); INV-125 (SD-DF-01) | ok |
| 005 | MUST for patients with migraine; label SHOULD | C1-02; INV-008 | ok |
| 006 | SHOULD; MUST per month where provided | C1-03, C1-04; INV-008, INV-122 | ok |
| 007 | SHOULD; ICHD-3 definition | C1-05, C1-06; INV-125 (SD-DF-02) | ok |
| 008 | MAY | E-020 to E-022; C3-02; INV-104 (ISS-04) | ok |
| 009 | SHOULD series with markers; weekly where relevant | INV-034, INV-035, E-035 W2, INV-001 | ok |
| 010 | SHOULD on a stated scale; comparison | C1-07, E-023 `scale`, INV-032, INV-039 | ok |
| 011 | SHOULD; label; Caveat | C1-08, C3-03, C2-03 | ok |
| 012 | SHOULD across periods and per treated attack, for migraine | C1-09, INV-033, `requiredOutcomes`, INV-072, INV-076 | ok formally; **R41-01** concerns the rationale entry of INV-076 |
| 013 | MAY | E-019, E-024, E-027 | ok |
| 014 | MUST total, class, drug | C1-10 (`medicationKinds`), INV-024, INV-122, SD-CLS | ok |
| 015 | SHOULD weekly | C1-11 | ok |
| 016 | MUST indicator; MUST prompt; MUST NOT diagnosis | INV-044 to INV-046, SD-CLS, SD-CMB, SD-FX-06; C3-04; C2-04 | ok |
| 017 | SHOULD | INV-049 to INV-051, E-039, C3-06 | ok |
| 018 | MUST; Caveat | INV-053, INV-055 to INV-059, E-040 and E-043 W2, SD-ER; C2-05 | ok |
| 019 | SHOULD | INV-060, INV-061; ISS-13 | ok |
| 020 | MAY; SHOULD; SHOULD NOT | E-045, E-046, INV-062 to INV-064, INV-114, INV-116; C2-06, C3-07 | ok |
| 021 | MUST; SHOULD | INV-102, INV-068, INV-069 | ok |
| 022 | SHOULD | INV-103, INV-070, INV-112, E-049 | ok |
| 023 | SHOULD; Caveat | INV-071 to INV-075, SD-ET, E-050 to E-053; C2-07 | ok |
| 024 | SHOULD | INV-077 to INV-079, INV-109, E-054 and E-055 W2 | ok |
| 025 | MAY | E-007 `schemeSelection`, E-056, INV-080 | ok |
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

Every Statement part and every Caveat that constrains what an output shows is represented at the level of its Stage 1 part, including each case of the level-indexed INV-118, INV-119, INV-120 and INV-125 (tables C1, C2, C3, SD-DF).

### Mechanical checks (scripts in `scripts/`)

| Check | Result |
|---|---|
| Headings and IDs (`mech.py`) | 67 E, 87 INV, 12 ISS; no duplicate. INV-001 to INV-125 each either live or listed in section 9 (38 merged invariants, ISS-07, C1-13). 0 dangling E/INV/ISS/OC/C1–C3/SD references. Withdrawn IDs occur before section 9 only in the "Replaces" Notes of the generic invariants. |
| `RATIONALE.md` entries (`mech.py`) | 440 entries, none duplicated; all 370 entry IDs that the model names exist; 0 internal references unresolved; every Concerns ID resolves. The 35 entries the model does not name are the C1–C3 origin entries, which section 4.4 names collectively ("C1-NN/D01 …"). |
| Traceability (`trace.py`) | 39 rows in Stage 1 order (OUT-039 after OUT-025). The Elements and Invariants columns equal the reverse index of the Realises fields (0 differences). The Catalogue rows column equals the rows whose Realises cell names the requirement (0 differences). Every catalogue Realises entry is in the Realises field of an item named in the row (0 exceptions). Two coverage lines name an item outside the row's columns (OUT-008: INV-104; OUT-012: INV-069); see Checked and not raised. |
| Audience column | 44 "OUT-NNN: …" cells equal the Stage 1 Audience lines verbatim (0 differences). |
| Level typing | 175 attributes with a level; every SHOULD, MAY and MUST-with-`when` attribute has an `opt`, `set` or `seq` type (0 violations). |
| W2 markers | 23 markers declared, equal to the section 6.0 table; each on a `→R` attribute. |
| Declared names (`names.py`) | 833 declarations; identifiers used in `omn` blocks and case-table code cells are declared, bound variables or table IDs. Repeated names are attribute names of different element types (section 2.5) and bound variables. |
| Case tables | Keys pairwise distinct in C1, C2, C3 and every SD table; every component of `EvaluationRule`, `ResponderCriterion` and `GradeBand` has its column; every header of form C is a declared function or predicate. |
| Definedness | Every `÷`, `days`, `first`/`last`, `s(i+1)`, `max`/`min`, `periodEndFrom`, `classOf` and `opt` use read: guarded as section 2.6 requires. |
| Catalogue "def." and "Shown with it" cells | Each "def." list equals the definitional invariants that name an element of the row, apart from the seven stated once in section 4.2; no row restates those seven (only INV-003, INV-008, INV-011 for their own kinds). |
| Worked examples | The dates and day counts of E-007/D01, E-042/W01, W02, E-063/W01, INV-049/W01, INV-055/W01, INV-079/W01 and INV-105/D02 recomputed: all correct. |
| v39 → v40 diff | Header, the INV-061 and INV-075 Readings, the change-log entry; `history/v40.md` and `history/v40-rationale.md` equal the live files. |
| Scope sweep | input, enter, record, answer, store, database, JSON, XML, CSV, FHIR, algorithm, comput, calculat, obtained, reminder, captur, persist, serializ, encod, retention, "diary information": only exclusion statements, notation prose, out-of-scope notes, source names, the HALT-30 quote, Stage 1 wording and the settled E-060 lead-in Meaning. Every threshold, formula and computed field shown with an output is present with its source, and every relation takes output elements (and context properties) only. |

## Remarks

### R41-01 Prose overclaim (`RATIONALE.md` disagrees with the model): INV-076/D01 says treated-attack lines are not assigned to headache types, while the model scopes acute-treatment summaries, and so their lines, to one headache type
- Item(s): `RATIONALE.md` INV-076/D01 (moved v34 INV-076 Notes). Related: INV-076; E-053 `symptomStatus`; E-051 `sequence`; E-012; INV-073; INV-088; E-012/D01; INV-073/D01.
- Problem:
  - **What the entry says.** INV-076/D01 justifies why INV-076 quantifies over every treated-attack line: "A subject with migraine may also have another headache type (OUT-029); the treated-attack lines are not assigned to headache types, because such an assignment would be a derivation from input (section 1, item 3), so every treated-attack line of a subject with migraine shows the three statuses."
  - **Type scope is an output property in the model, not a derivation from input.**
    - Every per-period value has a type scope: E-012 `typeScope : TypeScope core -- all headache types combined, or one headache type`; section 4.1: "A `PeriodValue` is a value shown for one period and one type scope (all headache types combined, or one type)".
    - An acute-treatment summary is a per-period value (`element AcuteTreatmentSummary extends PeriodValue`, E-051). OUT-029's values per type are model content (INV-118, `byTypeCases`), and section 1 does not treat them as derivation from input.
  - **The model relates treated-attack lines to one headache type.**
    - A summary lists the attacks it summarises: E-051 `sequence : seq →TreatedAttackLine … -- the treated attacks it summarises, earliest first`; INV-072 Reading: "It lists every treated attack it summarises, in order"; INV-074 Reading: "A summary lists at most the attacks it covers".
    - A summary scoped to cluster headache consists of cluster-headache attacks only:
      - INV-073 Reading: "Summaries of treated attacks of cluster headache only use the 15-minute time point";
      - INV-088 Reading: "The rates and the acute-treatment summaries it is required to show are those of all the subject's attacks of cluster headache";
      - E-012/D01: "`onlyOfType` and `scopeFor` are used where a value is taken to consist of the headaches of one type only: … of an acute-treatment summary with the 15-minute time point (INV-073), the rates and acute-treatment summaries that the cluster view shows for the subject's cluster headache (INV-088)";
      - INV-073/D01: "The 15-minute summaries of such a subject's cluster view (INV-088) are scoped to cluster headache."
    - So the lines of these summaries are, in the model's own terms, attacks of cluster headache.
  - **The consequence the entry misdescribes.** Take a subject with migraine and cluster headache (`possibleHeadacheTypes` = {c1, c3_1}).
    - INV-088 (SHOULD) asks for a cluster view whose summaries are in the scope `ofType(c3_1)` (`scopeFor`) with the 15-minute time point.
    - Their sequences (E-051, SHOULD, W2) list the treated cluster-headache attacks.
    - INV-076 (SHOULD) and E-053 `symptomStatus … SHOULD when hasType(ctx, c1)` then ask every one of these lines to show whether nausea/vomiting, photophobia and phonophobia were present at 15 minutes.
    - The entry gives as the reason for this that lines cannot be related to a headache type. The model does relate them, so the reason is false. Whether the model intends the consequence, under its subject-level reading of "For migraine" (the entry's first sentence), the entry does not say.
  - **Rule.** PROCESS.md section 6a: "`RATIONALE.md` must agree with the model; where they differ, the model governs and the difference is a defect." Section 9: "Prose overclaim: a … `RATIONALE.md` statement that claims more than, or other than, what the formal text guarantees."
  - **History and watch points.**
    - The sentence was written by fix 02 (R02-06) and moved verbatim in v35. Already in v02, INV-073 spoke of "Summaries of treated cluster-headache attacks", and since v13 INV-088 requires summaries scoped to cluster headache.
    - Review 13 noted that "INV-076 applies to every treated-attack line of a subject with migraine whatever the summary's scope (the R02-06 fix is kept)", as part of the satisfiability of its own remark; it did not examine the entry's reason.
    - No review, fix or oscillation check has raised or declined the sentence, and no watch point names INV-076 or E-053 `symptomStatus`.
    - This is not the declined "stale moved text" of watch point 8 (INV-075/D01, INV-085/D01, INV-110/S01): those became outdated when v35 moved conjuncts, while this reason has disagreed with the type-scoped summaries since it was written.
    - Option (a) below changes no formal text and keeps fix 02's decision. Option (b) would not restore R02-06's declined alternative (migraine-scoped summaries).
- Evidence:
  - `RATIONALE.md` INV-076/D01 (quoted above).
  - Model: E-012 Definition and Meaning; section 4.1, layer 3; E-051 Definition (`extends PeriodValue`, `sequence` comment) and Meaning ("the outcomes across the attacks treated with it … the sequence of per-attack lines"); INV-072, INV-073, INV-074 and INV-088 Readings (quoted above); INV-076 Predicate `∀ l : TreatedAttackLine • hasType(ctx, c1) ⇒ ∀ a : AssociatedSymptom • ∃ st ∈ l.symptomStatus • st.symptom = a`; E-053 `symptomStatus : set SymptomStatus SHOULD when hasType(ctx, c1)`.
  - `RATIONALE.md` E-012/D01 and INV-073/D01 (quoted above).
  - Stage 1 OUT-012: "For migraine, the diary output SHOULD report the presence of migraine-associated symptoms (nausea/vomiting, photophobia, phonophobia) and the patient's most bothersome symptom, both across periods and in the response of individual treated attacks (see OUT-023)." OUT-031: "for acute treatments, effectiveness at 15 minutes and the need for rescue treatment (see OUT-023)".
  - `history/v02.md` INV-073 Reading; `history/v13.md` INV-088 Predicate (`scopeFor(c, s.typeScope, c3_1)`).
- Required change:
  - **(a) Preferred: correct INV-076/D01; no formal change.** Remove the claims that treated-attack lines are not assigned to headache types and that such an assignment would be a derivation from input. State the actual reason and its scope:
    - INV-076 reads "For migraine" as a subject condition for both parts of OUT-012, as C1-09 and E-053 do.
    - A line of a summary over all headache types combined may show an attack of any type.
    - INV-076 therefore also applies to lines that the output presents as attacks of another headache type, for example the lines of the cluster view's 15-minute summaries of a subject who also has cluster headache (INV-088, INV-073).
  - **(b) Alternative, only with a Stage 1 reason.** If the fixer judges that OUT-012's per-attack part does not extend to attacks that the output itself presents as attacks of another headache type, then:
    - exempt from INV-076, and from E-053's `when` clause, the lines that a summary scoped to a headache type outside migraine lists, for example by adding to INV-076's antecedent `¬ ∃ s : AcuteTreatmentSummary; h : HeadacheType • l ∈ ran s.sequence ∧ s.typeScope = ofType(h) ∧ ¬ h ⊑ c1`;
    - keep every line of a summary over all headache types combined, which fix 02's decision requires;
    - correct INV-076/D01 accordingly, and update the OUT-012 traceability row.
  - **Class (PROCESS.md section 6a):** rationale entries that justify a rule by "the model does not relate X to a headache type". I searched `RATIONALE.md` and the model for such claims ("assign", "derivation from input", "not assigned"); INV-076/D01 is the only member. E-012/D01, E-064/D03, INV-073/D01, INV-089/D01 and INV-109/D02 agree with the type scopes of the model.

## Checked and not raised

- **The v40 change (R40-01).** The new INV-061 and INV-075 Readings state their predicates clause by clause; no other text changed (diff checked). The INV-061 heading keeps OUT-019's words, as fix 40 explained.
- **Traceability coverage lines naming items outside their row's columns.**
  - OUT-008 names INV-104 "in the clinician-facing summary (SHOULD, OUT-034) … (ISS-04)": an explicit cross-reference to OUT-034.
  - OUT-012's per-attack line names "in the treatment review view: INV-069", whose Realises field (OUT-021, OUT-023) does not include OUT-012, and does not name INV-072, which realises the per-attack most-bothersome-symptom part. E-053 is named there, and its Conformance field points to INV-072; INV-072 is in the row's Invariants column; INV-069 does show OUT-012's outputs in the review view (OUT-021 refers to OUT-012).
  - The columns are complete and exact. These are informative cross-references, not wrong entries. Not raised.
- **INV-096's PedMIDAS conjunct** is implied, at the same SHOULD level, by INV-081, E-058 `recallPeriod` and INV-082 (`publishedRecall(pedmidas) = recallMonths(3)`). It restates no rule differently and traces OUT-036 (a). Not raised.
- **Section 3.4** names `reportedPerPeriod` as the predicate of INV-118, which uses `reportedTogether`; for one kind the two are the same (INV-118/D03). Not raised.
- **Units.** `completeCycles` ("the number of complete cycles") and the Duration-typed attributes (rule U1 in section 2.8) state their units; the numeric components of value types `ScalePoint`, `GradeBand` and `ScoreRange` carry no "unit:" comment, but section 2.7 speaks of attributes, and their units are evident (scale points, score points). Not raised.
- **Per-period series without one scale, form or domain** (C1-07 intensity; C1-12 severe-impairment domain): deliberate, stated in E-023/D02 and INV-027/D01; the comparisons Stage 1 asks for are INV-039, INV-069, INV-105 and INV-027. Not raised.
- **INV-001/Q00** quotes OUT-009 as "where weekly granularity is clinically relevant (…)" with a lower-case initial; Stage 1 begins the sentence with "Where". A capitalisation change at the start of an embedded fragment. Not raised.
- **R-MCF (section 3.8) against its uses.** Rules (1) to (4) checked at every place SEC-3.8/D01 lists, and at E-047/INV-067, E-048/INV-068, E-055/INV-079, E-049/INV-112, INV-104, INV-105 and E-056/INV-080. The responder-label periods are the point settled in review 37. Not raised.
- **Satisfiability of the MUST layer.** INV-003 with INV-044 to INV-046 (spans before the selected time range), INV-037, INV-040 with INV-041, INV-055 to INV-059, INV-068 with INV-102 (including a one-day course), INV-086 with INV-087 and INV-124, C1-01 to C1-10 with `byTypeCases`, C3-04 and SD-DF-01: no combination is unsatisfiable for an admissible context.
- **Stage 1 issues ISS-01 to ISS-06 and ISS-08 to ISS-13.** Founded; every Stage 1 passage they cite is quoted and located correctly (ISS-03's list of Statements checked against every Stage 1 Statement). I found no other Stage 1 issue that the model works around silently.
- **Settled points, no new evidence:** the E-060 lead-in Meaning (review 05; checks 04 and 12); ISS-09's Group D without OUT-017 (reviews 25b, 31); the HADS total excluded (reviews 05, 19b); the HIT-6 one-month recall; the MIDAS labels and the HALT-90 overlap at 20; control-level labels over mixed months; MUST NOT for the OUT-018 Caveat (C2-05); `concerns` for mixed-type indices (reviews 01, 10); the overuse indicator's `basis` and `span` at MUST (review 19b); the stop bound of the comparison's periods and of INV-071 (fix 18); "the history of previous bouts" (review 01); the search languages of the Stage 2 searches (review 05).
- **Watch point 8, bookkeeping.** INV-075/D01, INV-085/D01 and INV-110/S01 (stale moved text) and the seven definitional cross-link asymmetries: declined earlier; no new evidence. Not raised.
- **Oscillation watch points of the checks after iterations 36 and 40.** R41-01 touches none of them: INV-076 and E-053 `symptomStatus` are named by no watch point, option (a) changes no formal text, and option (b) leaves every line of an all-types summary under INV-076 and does not restore R02-06's declined alternative.

## Notes on frozen items (for the human)

None. No item is frozen: `FROZEN_ITEMS.md` does not exist, and the model has no "Status: FROZEN" marker.
