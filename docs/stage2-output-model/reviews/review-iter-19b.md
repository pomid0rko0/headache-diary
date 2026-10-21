# Review — iteration 19 (re-check b)
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v18
Date: 2026-10-21

## Summary

This is the first independent re-check of iteration 19. The main review, `review-iter-19.md`, returned NO_REMARKS on v18. I read only its summary and method list, to see what it had examined. Every check below I ran again myself:
- my own downloads, into a fresh directory `/tmp/r19b-dl-uxTbWo`, outside the repository;
- my own scripts, in the session scratchpad folder `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r19b-scripts/`, all run with `python3 -I`.

**State of the files.**
- `OUTPUT_MODEL.md` is byte-identical to `history/v18.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a FROZEN marker.
- The working tree was clean when I started.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5;
- v18: every element (E-001 to E-067), every invariant (INV-001 to INV-110), and sections 1–4 and 7–11, with the change log skimmed;
- the oscillation check after iteration 16 with its eight watch points;
- the parts of earlier reviews and fixes that concern the topics I examined. The section "Checked and not raised" lists them.

As asked, I spent most of my effort on the parts that recent iterations did not touch:
- the instrument value sets (E-057, E-058, E-059, INV-081 to INV-085);
- the medication-overuse indicator (E-028, E-029, E-032, INV-024, INV-044 to INV-048);
- the cluster view (E-062 to E-064, INV-088, INV-089);
- the composite-index prohibition (E-033, INV-091 to INV-093);
- the reimbursement windows (E-056, INV-080);
- the caveat and decision invariants (INV-099 to INV-107).

**Result.**
- **Citations.** 413 quoted source fragments were checked against freshly downloaded text. All 413 are verbatim at their stated location: 406 by script and 7 by hand or by rendering the page. Every new source has correct metadata.
- **Value sets.** Every value set, score range, unit, code, label, threshold and offset matches its source.
- **Fidelity.** All 39 Stage 1 requirements are represented, at the right strength.
- **Mechanical checks.** All pass.
- **Scope sweep.** It found no input, storage or derivation-from-input content. No threshold, formula or computed field of the output data is missing.
- **Section 8.** Every Stage 1 issue in section 8 is founded, and none is silently worked around.

Several points looked like possible remarks. Each turned out to be one of these:
- a decision that an earlier fixer declined, or an earlier reviewer judged, with a justification, for which I have no new evidence;
- or not a defect.

They are listed under "Checked and not raised". I raise nothing, so no earlier fix is reversed and no watch point of the iteration-16 check is touched.

## Verification coverage

### Downloads and method

All downloads were made with `curl` through the configured proxy into `/tmp/r19b-dl-uxTbWo`.
- **PDFs** were extracted page by page with `pdftotext -layout` and `-raw`.
- **HTML and Europe PMC XML** were extracted with scripts and markup removed, then entities unescaped.
- **Rendered with `pdftoppm` and read by eye:**
  - ICHD-3 p. 190 and p. 209;
  - the [S-034] title page, which is an image.
- **How `quotes.py` works.** It extracts every double-quoted string outside `omn` blocks on a line that carries an `[S-NNN]` tag. It splits each string at `[...]` and `…`. It searches each fragment in the text of the nearest preceding tagged source, then in the other sources tagged on the line, using two normalisations:
  - NFKC, with quotes and dashes unified, line-end hyphens joined and whitespace collapsed;
  - letters and digits only, which covers the ICHD-3 glyphs without a text mapping ("≥", "±", "−").

  Fragments that are not found in a source are checked against the Stage 1 v18 text.
- **Page numbers.** For PDF sources, the script lists every page on which a fragment occurs, so that the stated page can be compared.
- **Retries.** Two sites failed once:
  - brainmed.com ([S-032]) reset the connection; the retry returned HTTP 200.
  - The PMC pages of [S-102] and [S-104] first returned a reCAPTCHA page; the retry returned the article.

  Every other request returned HTTP 200 on the first attempt.

### Quotes per source

| Source (file checked) | Fragments checked | Verified verbatim at stated location | Not found | Unreachable |
|---|---|---|---|---|
| S-001 ICHD-3 PDF, 211 pp. | 59 | 59 (57 by script; the A1.1.1 and A1.1.2 window "day 1 ± 2 (i.e. days −2 to +3)" on rendered p. 190) | 0 | — |
| S-002 IHS episodic prevention PDF | 7 | 7 | 0 | — |
| S-005 IHS paediatric PDF | 3 | 3 | 0 | — |
| S-007 UCL accepted manuscript, 39 pp. | 8 | 8 (pp. 10, 22, 25) | 0 | — |
| S-008 IHS 2024 PDF (univaq), 31 pp. | 31 | 31 (Q2 p. 9, Q6 p. 12, Q6 Evidence p. 13, Q13 p. 17); 2 attached by the script to a neighbouring tag, checked by hand on p. 12 | 0 | — |
| S-010 IHS 2025 PDF (univaq), 11 pp. | 40 | 40 (control levels and migraine-day paragraphs, p. 6) | 0 | — |
| S-011 Europe PMC PMC9188162 | 11 | 11 | 0 | — |
| S-012 PMC9555163 / S-013 PMC7296705 | 1 / 1 | 1 / 1 | 0 | — |
| S-014 Europe PMC PMC6734476 | 30 | 30 (HALT versions, scoring, Table 18 rows and pairing, HURT areas) | 0 | — |
| S-015 NICE CG150 Recommendations and Overview pages | 57 | 57 (1.3.9, 1.3.24, 1.3.26 to 1.3.29, 1.3.39, 1.3.48, headings, population sentence, "Last updated: 03 June 2025") | 0 | — |
| S-016 SIGN 155 PDF, 64 pp. | 10 | 10 (1.2.1 on PDF p. 7, printed p. 1; 4.1 on PDF p. 20, printed p. 14) | 0 | — |
| S-018 AAN/AHS Clinician Summary PDF, 12 pp. | 17 | 17 (title and first sentence p. 1, 14A and 14B p. 7, 14H p. 8) | 0 | — |
| S-023 Europe PMC PMC9607711 | 7 | 7 | 0 | — |
| S-028 NVN module page | 15 | 15 (Aanbeveling, PICO "Patiënten (kinderen en volwassenen)") | 0 | — |
| S-029 NVN page / S-030 Danish PDF / S-042 PMC12279330 | 1 / 3 / 1 | 1 / 3 (PDF p. 19) / 1 | 0 | — |
| S-033 Russian adult PDF, 92 pp. | 26 | 26 (title page p. 1, abbreviations p. 4, section 3.3 pp. 39–41, section 7.1 p. 53) | 0 | — |
| S-034 Russian paediatric PDF, 53 pp. | 11 | 11 (flowchart p. 52, section 2 p. 17); the title page is an image without a text layer, rendered: "Возрастная группа" / "дети" | 0 | — |
| S-035 Turkish protocol PDF, 92 pp. | 42 | 42 (p. 23; Kutu 8 p. 48; 3.6.3.9 p. 57; section 6 heading p. 77, contents p. 7; chapter 7 pp. 82, 83, 86) | 0 | — |
| S-101 PMC3057423 (Europe PMC XML and PMC page) | 5 | 5 (HIT-6 range 36–78 and four categories, "Data sources") | 0 | — |
| S-102 PMC4406925 (XML and PMC page) | 7 | 7 (four MIDAS grades with bands, "option of dividing Grade IV into IVA and IVB", three-month recall) | 0 | — |
| S-103 Cincinnati Children's PedMIDAS page | 10 | 10 (table rows 0–10 / 11–30 / 31–50 / > 50 paired with Little to none / Mild / Moderate / Severe) | 0 | — |
| S-104 PMC183845 (XML and PMC page) | 3 | 3 (HADS 0–21 per subscale) | 0 | — |
| S-105 PHQ/GAD-7 manual PDF, 9 pp. | 3 | 3 (heading "Use of some screeners as severity and outcome measures" and both ranges on P. 6/9; the developers sentence on P. 8/9) | 0 | — |
| S-106 NICE TA260 overview, chapters 1 and 2 | 4 | 4 (2.1, last sentence: re-treatment every 12 weeks) | 0 | — |
| **Total** | **413** | **413** | **0** | **0** |

The other quoted strings fall into three groups:
- **Stage 1 fragments (47).** These are Statement and Caveat wording of Stage 1, for example "for example a pre-treatment baseline period against a later period of the same length". All 47 were found verbatim in Stage 1 v18.
- **Translations (22).** These are the English translations of the new Russian, Turkish and Dutch quotes. I checked each against the original for meaning, and all are faithful (for example "Контроль эффективности терапии через 3мес." → "Monitoring of the efficacy of therapy after 3 months"; "Etkisini değerlendirmek için en az 2 k ez uygulanmalıdır" → "To evaluate its effect, it should be administered at least 2 times").
- **Not source quotes (19).** These are 16 search-log query strings and 3 strings of model prose.

### Citation metadata

**S-101, S-102, S-104 and the developer paper of S-103.** Checked against the Europe PMC records:
- authors, title, journal, volume, issue, pages and year;
- DOI, PMID and PMCID.

All are correct. "Pavlovic" for "Pavlović" is a transliteration.

**S-105.**
- The manual title on P. 1/9 is as cited.
- The developers sentence is on P. 8/9.
- The PDF metadata match the citation: author Kurt Kroenke, created 2010-06-22, modified 2014-04-16.

**S-106.**
- Published 27 June 2012, last reviewed 11 January 2016 (overview page).
- CG150 1.3.26 refers to it: "For full details, see NICE's technology appraisal guidance on botulinum toxin type A (TA260, 2012)."

**S-103.** The page footer reads "© 2026 Cincinnati Children's Hospital Med…", as cited.

**Types and grading.** All are stated correctly:
- the developer co-authorship of S-101 (Kosinski) and S-102 (Stewart, Lipton);
- S-104 by a co-developer (Snaith);
- S-105 by the developers.

**Newer versions.** No newer version of any new source that would change an element was found. TA260 is current ("We checked this guidance and found nothing new").

### Value sets, codes, labels and thresholds (category B)

**ICHD-3 codes and labels** (E-009, E-028). The labels of 1., 1.2, 1.3, 2., 2.3, 3.1, 8.2 and 8.2.1 to 8.2.8 are exactly as printed in the classification list (pp. 8, 9, 12).

**ICHD-3 8.2 reference levels** (E-032), each matching its description or criterion B:
- 15 days per month for 8.2.3;
- 10 days per month for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8;
- more than three months for every subtype.

Further details checked:
- The "≥" glyph in the text layer is `^B`, so "on ≥10 days/month for >3 months" reads as quoted.
- 8.2.6 criterion B names only ergotamine, triptans, non-opioid analgesics and/or opioids (`classesOf826`).
- Note 2 ("criterion B has not been fulfilled for any of the specific subtypes 8.2.1–8.2.5") supports `classesOf821to825`, so 8.2.8 does not block 8.2.6.

**Other ICHD-3 values.**
- The A1.1 window is day 1 − 2 to day 1 + 2, that is, days −2 to +3, with no day 0 (rendered p. 190).
- A remission "must exceed three months" (rendered p. 209).

**Instrument value sets.**
- HIT-6: range 36–78, with bands ≤ 49, 50–55, 56–59 and 60–78 and the four labels.
- MIDAS: grades I to IV, with bands 0–5, 6–10, 11–20 and ≥ 21 and the labels of [S-102]; 3-month recall.
- PedMIDAS: four grades, the top one "Greater than 50", hence `strictLow` at 50.
- HALT-90: Table 18 with bands 0–5, 6–10, 11–20 and ≥ 20, grades I to IV and their labels; the overlap at 20 is in the source.
- HALT-30 and HALT-90 recall: 1 and 3 months.
- HADS: 0–21 per subscale.
- PHQ-9: 0–27.
- GAD-7: 0–21.

**Responder thresholds** (E-045), each as its source states it:
- NICE 1.3.28 (50 % episodic, 30 % chronic) and 1.3.29 (30 % of headache days);
- IHS Q6: ≥ 50 %; the ≥ 30 % chronic alternative; MIDAS ≥ 5 points for baseline 11–20 and ≥ 30 % for baseline ≥ 20; HIT-6 ≥ 5 points;
- DMKG/ÖKSG/SKG (episodic migraine): 50 %, 5 points and 30 %;
- Russian section 7.1: 50 % of headache days.

**Control levels** (E-046, INV-064). The four levels and the "less than six MMDs" allowance match the [S-010] wording.

**Evaluation rules** (E-041). All 18 offsets, anchors, timings, ages and exclusions match their quotes.

**Other thresholds** match Stage 1 or their quotes:
- the 4–8-week review window and the 12-month follow-up (E-039, INV-051);
- 15 minutes and 2 hours (INV-073);
- the 28-day period (E-042).

### Fidelity to Stage 1, requirement by requirement (category C)

The table checks every observable property of each Statement and every Caveat that constrains the output. It also checks each conformance level against the Stage 1 statement part it realises.

| OUT | Result |
|---|---|
| 001 | Every view states its period with start, end and length (E-003, E-005, INV-002, INV-003). Frequency measures are MUST per calendar month or 28-day period (INV-014, INV-015, INV-108; reading of "frequency outputs" in ISS-04). Equal-length comparisons: INV-037, INV-055. The lengths of calendar months are visible (Caveat). OK. |
| 002 | Definition labels at SHOULD for every form in which a view reports the four measures (E-011 `reports`, INV-008). OK. |
| 003 | Completeness for every summarised period at SHOULD (INV-011, INV-012). Its forms are open, with the proportion as an example. The SHOULD NOT on a validated cut-off is INV-013. OK. |
| 004 / 005 / 006 / 007 | MUST / MUST (for migraine) + label SHOULD / SHOULD / SHOULD, each with its ICHD-3 or published definition (INV-009, INV-010, INV-014 to INV-017, INV-108). Attacks are a separate element type. OK. |
| 008 | MAY elements, with an optional exploratory label (E-020 to E-022). OK. |
| 009 | SHOULD time series with dated markers for start, dose change and stop (INV-034 to INV-036). Weekly values where relevant (INV-001, INV-034). OK. |
| 010 / 011 | Intensity on a stated scale, comparable between periods (INV-018, INV-032, INV-039). Duration (INV-019), with the treated-attack label (INV-020) and the Caveat as SHOULD NOT (INV-021). OK. |
| 012 / 013 | Symptoms and the most bothersome symptom across periods and per treated attack (INV-022, INV-072, INV-076). Aura measures MAY (E-027). OK. |
| 014 / 015 | Total, per ICHD-3 8.2 class and per drug, MUST (INV-023, INV-024). Weekly view SHOULD (INV-025). OK. |
| 016 | Indicator per period, per class and for 8.2.6 combined use, MUST (INV-044). The code, level, span and basis are shown, and the status relation is over output elements only (INV-045, INV-046). Prompt wording MUST (INV-047). Not a diagnosis, MUST NOT (INV-048). 8.2.7 is excluded, as in Stage 1. OK. |
| 017 | Follow-up from the start of withdrawal, with the NICE window, over the following year, with the worsening label (INV-049 to INV-052; ISS-11). OK. |
| 018 | Monthly comparison aligned to the start, with values, absolute and percentage changes, time points and moderate/severe days where reported, all MUST (INV-053 to INV-059). Continuation is not decided (INV-106). OK. |
| 019 / 020 | Residual burden SHOULD (INV-060, INV-061). Labels: criterion, values, other values (SHOULD, INV-062), consistency (INV-063, INV-064), not the sole indicator SHOULD NOT (INV-065). OK. |
| 021 / 022 | MUST components for the same periods (INV-068, INV-102), the others SHOULD where provided (INV-069). Post-stop monitoring SHOULD (INV-070, INV-103). OK. |
| 023 | All named outcomes, consistency, timing, formulation, 15 minutes for cluster headache, and baseline and on-treatment phases (INV-071 to INV-075). The choice of definition is left to the reader (INV-107). OK. |
| 024 / 039 | History grouped by class and chronological, with every listed attribute (INV-077 to INV-079, INV-109). Adherence next to the comparison, in the history and in the clinician summary (INV-066, INV-067, INV-104, INV-109). OK. |
| 025 | MAY view of the selected windows, labelled with the scheme name (E-056, INV-080). OK. |
| 026 / 027 | Instrument results with name, date, recall, total score, published grading and change (INV-081, INV-082; ISS-06). Functional impact per domain and severe impairment, compared with baseline (INV-026, INV-027). OK. |
| 028 / 029 | Three-month view MUST, definitions SHOULD, no diagnosis SHOULD NOT (INV-040 to INV-043). Per-type outputs MUST, intensity SHOULD (INV-028 to INV-030; ISS-09). OK. |
| 030 / 031 | Menstrual view MUST, with the A1.1 window and the number of complete cycles (INV-086, INV-087). Cluster bouts, remissions, rates, 15-minute effectiveness and rescue need, and earlier bouts as the bout list (INV-088, INV-089). OK. |
| 032 / 033 | Trigger view MAY, with its caveats SHOULD (INV-090, INV-110). Screening results next to headache outputs, not presented as diagnoses (INV-083 to INV-085). OK. |
| 034 / 035 / 036 | Clinician summary (INV-094, INV-104; ISS-04). Patient overview (INV-095, INV-105; ISS-03). Paediatric outputs (a)–(d) and the supportive-information Caveat (INV-055, INV-096 to INV-098). OK. |
| 037 / 038 | For migraine: SHOULD NOT as a primary measure, and labelled exploratory with its components. AUC for tension-type headache shown with headache days (INV-091 to INV-093). Caveats, interpretation and no diagnosis (INV-099 to INV-101). OK. |

### Mechanical checks (category E) and their results

**IDs** (`ids.py`):
- 67 elements, E-001 to E-067, with no gaps;
- 110 invariants, INV-001 to INV-110, with no gaps;
- 10 Stage 1 issues; ISS-07 is withdrawn and listed in section 9;
- no duplicate headings;
- no dangling reference to an E, INV or ISS ID;
- S-101 to S-106 are defined in section 10, and every S-0NN cited is a Stage 1 source.

**Fields.** Every element has Definition, Meaning, Conformance, Realises and Evidence. Every invariant has Predicate, Reading, Conformance, Realises and Evidence.

**Traceability.**
- 39 rows, in Stage 1 order, with OUT-039 after OUT-025.
- For every requirement, the Elements and Invariants columns equal exactly the reverse index of the Realises fields.
- Every row states its coverage as "full".

**Symbols** (`symbols.py`, with comments and text literals removed).
- Every identifier used in the `omn` blocks is declared, apart from the infix `_⊑_`.
- No name is declared twice.
- Every attribute selection `e.a` names a declared attribute.

**Typing rule for levels.** All 172 attribute declarations were checked. Every SHOULD, MAY and MUST-with-`when` attribute has an `opt`, `set` or `seq` type, and none has `set1` or `seq1`.

**Definedness.** I read every partial term (`first`, `last`, `min`, `max`, `÷`, `s(i)`, `classOf`, `periodEndFrom`) and found each guarded as section 2.6 requires.

**Satisfiability.** I hand-checked the pairs that constrain the same elements:
- INV-044 to INV-046 with INV-024 and INV-003;
- INV-088 with INV-073, INV-089 and INV-011;
- INV-062 to INV-064 with INV-055, INV-056 and INV-097;
- INV-091 to INV-093 with INV-008 and INV-011;
- INV-080 with E-056.

None of them conflicts.

**Conformance levels.** Each of the 110 invariant levels was listed against the Stage 1 strength of every requirement it realises. All match section 3.3 of the model and PROCESS.md section 4. INV-106 is MUST NOT as the negative form of a Caveat of OUT-018 (MUST), a choice settled in fix 01.

**Date arithmetic** (script):
- The shortest span of INV-045 has 4 periods for every calendar month from 2020 to 2029, and for every 28-day period starting on each of 3,000 consecutive days. Minimality holds in all cases.
- The worked examples of E-042 and INV-055 are correct: 12 weeks from 1 January 2026 end at 26 March; the final 28 days run from 26 February to 25 March; 3 months end at 1 April; the last day of the Turkish Box 8 interval is 28 February.
- The NICE CG150 1.3.27 window runs from 1 April to 1 July, and 24 weeks after the start (18 June) lies within it, as the E-041 Notes state.

### Scope sweep (category F)

**Wording.** I grepped the model for "enter", "record", "input", "capture", "answer", "data field", "reminder", "store", "database", "serialization", "JSON", "XML", "CSV", "FHIR", "HL7", "encoding", "persist" and "retention", and read every hit in context. The only hits are:
- the exclusion statements of section 1;
- the notation disclaimer of section 2.1;
- the quoted [S-014] sentence "HALT-30 [...] records days affected during the preceding 1 month", quoted for the recall period;
- statements that a derivation is out of scope (E-057 Notes, INV-076 Notes);
- the Europe PMC "full-text XML" endpoint in the search log.

**Formulas and relations.** Every formula, threshold and derived relation has only output elements, context properties or cited constants as arguments. Each such relation is listed with its element:
- E-005: length;
- E-013 / INV-012: completeness;
- E-032 / INV-045 / INV-046: status from the shown basis and level;
- E-040 / INV-053: the change;
- E-042 / INV-058: time points;
- E-046 / INV-063 / INV-064: labels from the shown changes, counts and results;
- E-058 / INV-082: category and change;
- E-060 / E-061 / INV-087: window and attack marks;
- E-064 / INV-089: rates.

Derived values that are obtained from diary information are given only their type, unit and meaning.

**Required content.** No threshold, formula or computed field that is part of the output data is missing. One case was considered: the untabulated categories of M-TOQ, PGIC and MSQ v2.1 (see "Checked and not raised").

### Stage 1 issues (category G)

**ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded.** I re-verified:
- 8.2.6 criterion B (p. 124) and note 2 (p. 125);
- "simple analgesics" occurs only on p. 139, in 10.1.1 High-altitude headache;
- NICE 1.3.9 and 1.3.39 name no review time point;
- the CG150 population sentence and 1.3.48;
- the [S-034] flowchart box (p. 52);
- the [S-010] "Modest Control" sentence;
- the HURT areas sentence.

**Pointers.** Each issue is pointed to from the elements it affects.

**No silent workarounds.** No Stage 1 issue is silently worked around. Two points follow Stage 1 literally and work nothing around, so they are not omissions from section 8:
- the HIT-6 recall period;
- the 24-hour outcomes of the cluster-headache summaries.

## Remarks

None.

## Checked and not raised

- **MIDAS grade labels and the Grade IV subdivision** (E-057, INV-082).
  - [S-102] gives "little or no disability" and so on, with "an option of dividing Grade IV into IVA and IVB". Other developer-co-authored papers use "minimal or infrequent disability".
  - Review 01 (labels) and review 12 (subdivision) settled both points. The subdivision can be shown as further content (`OtherItem`).
  - I fetched the abstract of the MIDAS development paper (Stage 1 S-044, PubMed 11294956), which is the developers' own publication. It states no grade labels, so it is no new evidence.
- **HIT-6 recall "1 month".** The HIT-6 form words three of its items "in the past 4 weeks". The model follows [S-002], as review 03 settled. No new evidence.
- **HADS total score excluded** (INV-085). [S-104] confirms that "the two subscales, anxiety and depression, were independent measures" (review 05).
- **M-TOQ, PGIC and MSQ v2.1 categories not tabulated** (E-057).
  - Europe PMC has open-access papers co-authored by the M-TOQ developer.
  - They use different versions with different items, for example mTOQ-5 in PMC10090340, while other papers use mTOQ-4.
  - Stage 1 names "mTOQ/M-TOQ" without a version.
  - So "the instrument's own published grading or categories" depends on the version used. The model's `publishedCategory` and its E-057 Notes handle this. No change is required.
- **HALT-30 lower bound 0.**
  - The E-057 Notes say that the lower bound 0 of HALT "follows from their lowest band", but HALT-30 has no grading.
  - The value is still supported by the quoted unit, "whole days per one or 3 months" [S-014]: a number of days is not negative.
  - The value is correct, so this is not a factual error.
- **ISS-02 wording.**
  - The section 8 entry describes the only other occurrence of "simple analgesics" as a passage "on acute mountain sickness, section 10".
  - The passage is in fact the comment on 10.1.1 High-altitude headache, and it mentions acute mountain sickness in the next sentence.
  - The section and the point of the issue (an unrelated passage) are correct, so the entry is founded.
- **Medication-overuse indicator** (E-032, INV-044 to INV-048).
  - The levels and span are verified above, and the 4-period span is confirmed by script.
  - INV-046 matches 8.2.6 criterion B, note 2 and the 8.2.3 comment on cumulative non-opioid analgesics.
  - 8.2.8 does not block 8.2.6, consistent with note 2.
  - `basis` and `span` at MUST are needed for the status to be a relation over output elements (PROCESS.md section 2), and the basis is placed in the indicator's view through its period atoms (INV-003).
  - The reading of "for more than three months" as "in every month of a span longer than three months" is disclosed as the model's.
- **Cluster view** (E-062 to E-064).
  - A current attack-free period shorter than three months cannot be shown as a remission (INV-089). This matches ICHD-3, under which the attack-free period "must exceed three months".
  - Fix 11 settled "history of previous bouts", and reviews 01 and 14 settled the 24-hour outcomes of the 15-minute summaries.
  - The rate relation (INV-089) and the type scope (`scopeFor` implies `onlyOfType`) are consistent with INV-073 and INV-088.
- **Composite index** (E-033, INV-091 to INV-093). An index over all headache types of a subject with migraine and tension-type headache concerns neither type under `concerns`. Review 01 judged this a defensible reading of the OUT-037 Caveat, and I have no new evidence.
- **Reimbursement windows** (E-056, INV-080).
  - The view and its content are MAY, labelled with the selected scheme.
  - No audience condition is needed, because MAY imposes nothing.
  - The windows are not checked against the scheme's own definitions, which is a matter of scheme criteria that OUT-025 Caveats exclude.
- **Decision and caveat invariants.**
  - INV-106 is MUST NOT by section 3.3(6) of the model, from the OUT-018 Caveat (fix 01; reviews 02 to 19).
  - INV-107 is SHOULD NOT from the OUT-023 Caveat.
  - INV-099 to INV-101 are SHOULD and SHOULD NOT (OUT-038).
  - INV-048 (MUST NOT) is consistent with INV-101.
- **INV-060 with INV-061 for compared periods shorter than 28 days.** Fix 02 (item 14) declined this with a justification, and I have no new evidence.
- **Window time points and the as-of date** (INV-055).
  - For a window rule whose first date has been reached, the existential can also be met by an on-treatment period that ends at a later date within the window, possibly after the as-of date.
  - A period that ends before the as-of date always also satisfies it.
  - Review 18 judged a period that is not yet over to be a partially covered period with its completeness shown, not a false value.
  - So no output that Stage 1 forbids is admitted, and no change is required.
- **The patient overview's cycle line** (INV-105 with INV-087). The window and day-1 relations are definitional for every cycle line. This is a watch-point item (iteration-16 watch point 7), and it is unchanged.
- **Oscillation watch points.** I raise nothing, so no watch-point item is changed or reversed.

## Notes on frozen items (for the human)

None. No item is frozen, and `FROZEN_ITEMS.md` does not exist.
