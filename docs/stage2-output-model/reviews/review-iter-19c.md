# Review — iteration 19 (re-check c)
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v18
Date: 2026-10-21

## Summary

This is the second independent re-check of iteration 19, after the main review (`review-iter-19.md`) and the first re-check (`review-iter-19b.md`) both returned NO_REMARKS on v18.

**State of the files.**
- The working tree was clean at the start.
- `OUTPUT_MODEL.md` is v18.
- `FROZEN_ITEMS.md` does not exist, and no item carries a FROZEN marker.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026), and the source table of section 5;
- v18: sections 1–11, every element and every invariant, and the change-log entries for v15–v18;
- the oscillation check after iteration 16, with its eight watch points;
- reviews 19 and 19b;
- the earlier reviews and fixes that touch the points I examined (listed under "Checked and not raised").

I read reviews 19 and 19b only to see what they had examined. Every check below I ran again myself:
- my own downloads into the fresh directory `/tmp/r19c-dl-iR8DrV`, outside the repository;
- my own text extraction into `/tmp/r19c-txt-0IgMKx`;
- my own scripts in the session scratchpad folder `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r19c-scripts/` (`extract.py`, `match.py`, `pages.py`, `mech.py`, `strip.py`), run with `python3 -I`.

**Result.**
- **Substance.** All values, codes, labels, thresholds, offsets, predicates and conformance levels are correct.
  - Every one of the 39 requirements is represented at its Stage 1 strength.
  - The mechanical checks pass.
  - The scope sweep finds nothing.
  - 498 quoted fragments were checked against freshly downloaded sources, and none is misquoted.
- **The two remarks.** Each is a text error about a source, and neither changes any value, predicate or level. Both points were also examined by earlier reviewers (reviews 05, 10b, 16, 19, 19b) and judged "imprecise" or "close enough". As the orchestrator asked, I decided this question myself.
  - **R19c-01.** The E-057 Notes state that the lower bound 0 of HALT-30 "follows from [its] lowest band". HALT-30 has no band, by the source ("Grading is not used by HALT-30") and by E-057's own definition. So the model gives a false basis for a number it takes from a source, and the element contradicts itself.
  - **R19c-02.** ISS-02 describes the only ICHD-3 passage that uses "simple analgesics" as "an unrelated passage (on acute mountain sickness, section 10)". The passage is the comment on 10.1.1 High-altitude headache (p. 139). There ICHD-3 names "simple analgesics such as paracetamol (acetaminophen) or ibuprofen", which are drugs of the class that it names non-opioid analgesics (8.2.3). The topic is misdescribed. The passage is also relevant to the decision that ISS-02 asks of the human.
- **Why these are remarks.**
  - Each is a statement of fact about a source that the source contradicts. Neither is a matter of style, naming, an equivalent wording or an optional addition (PROCESS.md section 9).
  - Task G asks for correct locations and descriptions of the passages that section 8 cites.
  - PROCESS.md section 2 asks that every number taken from a source be supported by its quote; R19c-01 gives a false basis for one.
  - Neither point was ever raised as a remark, so no fixer declined it, and neither touches a watch-point item of the iteration-16 oscillation check.
- **Required changes.** Both are confined to one sentence each.

## Verification coverage

### Downloads and method

All downloads used `curl` through the configured proxy. Every request returned HTTP 200, except one: the [S-033] PDF was reset by the peer once and returned HTTP 200 on the retry.

**Stage 1 PDFs**, extracted page by page with `pdftotext -raw` and `-layout`:
- [S-001] ICHD-3 (211 pp.); [S-002] (19 pp.); [S-005] (14 pp.); [S-007] UCL accepted manuscript (39 pp.);
- [S-008] (31 pp.); [S-010] (11 pp.); [S-016] SIGN 155 (64 pp.); [S-018] AAN/AHS Clinician Summary (12 pp.);
- [S-030] (86 pp.); [S-033] (92 pp.); [S-034] (53 pp.); [S-035] (92 pp.).

**Stage 1 web pages:**
- [S-015], the NICE CG150 Recommendations and Overview pages;
- [S-028] and [S-029], the NVN modules.

**Europe PMC full-text XML:**
- Stage 1 sources: [S-004] PMC6501455, [S-011] PMC9188162, [S-012] PMC9555163, [S-013] PMC7296705, [S-014] PMC6734476, [S-023] PMC9607711, [S-042] PMC12279330;
- new sources: [S-101] PMC3057423, [S-102] PMC4406925, [S-104] PMC183845;
- papers named in the search log or Notes: PMC8684566, PMC6537129, PMC5796955 (HALT 2018) and PMC5812954 (HURT 2018).

**New-source pages:**
- [S-103], the Cincinnati Children's PedMIDAS page;
- [S-105], the 9-page manual PDF;
- [S-106], the TA260 overview and chapters 1 and 2.

**Rendered with `pdftoppm` and read by eye:**
- ICHD-3 p. 190. A1.1.1 B reads "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)", and A1.1.2 B reads "Occurring on day 1 ± 2 (i.e. days −2 to +3)". Note 2 of each reads "there is no day 0".
- The [S-034] title page, an image without a text layer: "Возрастная группа" "дети".

**Scripts.**
- `extract.py` takes every double-quoted string outside `omn` blocks on a line with an `[S-NNN]` tag, and attributes it to the nearest preceding tag.
- `match.py` splits each string at "[...]" and "…" and keeps fragments of at least 6 letters. It searches the tagged source first, then the other sources tagged on the line, with two normalisations:
  - NFKC, with quotes and dashes unified, ligatures and line-end hyphens joined and whitespace collapsed;
  - letters and digits only, which covers ICHD-3's unmapped "≥", "±" and "−".

  A fragment not found in any source is checked against Stage 1 v18.
- `pages.py` lists every PDF page on which a fragment occurs, so that the stated page can be compared.

### Quotes per source

**Column definitions:**
- **In source:** found verbatim in the downloaded text of the tagged source.
- **Other tag on line:** found in another source tagged on the same line, in the multi-source lines of E-041, E-045, E-057 and the logs. Each was read in context.
- **Stage 1:** a fragment of a Stage 1 Statement, Caveat or quote, found verbatim in Stage 1 v18.
- **By eye or hand:** verified on a rendered page, or by hand in the source that the context names.
- **Not source text:** translations, row labels and search-log query strings.

| Source (nearest tag) | Fragments | In source | Other tag on line | Stage 1 | By eye or hand | Not source text | Not found | Unreachable (tried) |
|---|---|---|---|---|---|---|---|---|
| S-001 ICHD-3 | 65 | 57: labels pp. 8, 9, 12; 8.2–8.2.8 pp. 122–125; 8.2.3 comment p. 123; Definitions of terms pp. 209–210; remission p. 209; A1.1 note 2 p. 190; "simple analgesics" p. 139 | 0 | 4 | 3 (p. 190 windows, rendered) | 1 (search-log row label) | 0 | 0 |
| S-002, S-005, S-007 | 30 | 17 (S-005 "the final 28 days of the treatment period should be assessed" p. 8; S-007 p. 10 item a, pp. 22, 25) | 7 | 6 | 0 | 0 | 0 | 0 |
| S-008 IHS 2024 | 29 | 21 (Q2 p. 9; Q4 p. 11; Q6 p. 12; Q6 Evidence p. 13; Q13 p. 17) | 8 | 0 | 0 | 0 | 0 | 0 |
| S-010 IHS 2025 | 48 | 39 (all on p. 6, among them the four control levels, the migraine-day paragraph and the "proxy" sentence) | 1 | 8 | 0 | 0 | 0 | 0 |
| S-011, S-012, S-013, S-016, S-018, S-023, S-028, S-029, S-030, S-032, S-042 | 65 | 47 (S-016 PDF p. 7 = printed p. 1, "two sentences later" confirmed; S-018 pp. 1, 7, 8; S-011 body Background paragraphs 1 and 2; S-028 "Zoeken en selecteren"; S-030 PDF p. 19) | 14 | 3 | 0 | 1 (translation) | 0 | 0 |
| S-014 Lifting The Burden | 38 | 27 (HALT versions, "Scoring HALT", Table 18 with "≥20", "Grading is not used by HALT-30", HURT areas) | 1 | 9 | 1 (the [S-008] phrase "acceptable for treatment continuation beyond three months", p. 12) | 0 | 0 | 0 |
| S-015 NICE CG150 | 56 | 39 (1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48, the headings, the Overview population sentence) | 4 | 12 | 1 (the same [S-008] phrase, p. 12) | 0 | 0 | 0 |
| S-033 Russian adults | 49 | 21 (title page p. 1; abbreviations p. 4; section 3.3 pp. 39–41; section 7.1 p. 53) | 24 | 0 | 0 | 4 (translations) | 0 | 0 |
| S-034 Russian children | 20 | 8 (section 2 p. 17; flowchart p. 52) | 2 | 4 | 2 (title page, rendered) | 4 (translations) | 0 | 0 |
| S-035 Turkish protocol | 50 | 33 (3.3 b p. 23; Kutu 8 p. 48, items 2 and 7; 3.6.3.9 p. 57, sentence order confirmed; headings pp. 7, 77, 82; 7.1 p. 83; 7.3 p. 86, items 3–5, "2 k ez" as printed) | 4 | 0 | 0 | 13 (translations) | 0 | 0 |
| S-101 to S-106 | 48 | 29 (S-101 "Data sources"; S-102 "Migraine-related disability"; S-103 grading table; S-104 HADS construction section; S-105 P. 6/9 and P. 8/9; S-106 paragraph 2.1) | 3 | 1 | 0 | 15 (13 search-log queries; 2 label strings of PMC8684566 and PMC6537129, verified there) | 0 | 0 |
| **Total** | **498** | **338** | **68** | **47** | **7** | **38** | **0** | **0** |

**Translations.** I read all 22 Stage 2 translations against their originals in context, and all are faithful:
- [S-028]: the PICO line;
- [S-033]: the title page, the section 3.3 comment, the PREEMPT recommendation and the p. 41 comment;
- [S-034]: the flowchart box, the title page and section 2;
- [S-035]: Kutu 8 items 2 and 7; 3.3 b; three 3.6.3.9 sentences; the section 6 and chapter 7 headings; two 7.1 sentences; three 7.3 items.

### Citation metadata and versions

- **Europe PMC records** (authors, title, journal, year, volume, issue, pages, DOI, PMID, PMCID) agree with section 10 for:
  - S-101: Cephalalgia 2011;31(3):357–367; 10.1177/0333102410379890; PMID 20819842; PMC3057423;
  - S-102: J Headache Pain 2015;16:24; PMID 25902814 (PubMed spells the first author "Pavlović");
  - S-104: Health Qual Life Outcomes 2003;1:29; PMID 12914662; PMC183845; the article subject is "Commentary";
  - the PedMIDAS developer paper: Neurology 2001;57(11):2034–2039; PMID 11739822;
  - ICHD-3: Cephalalgia 2018;38(1):1–211; PMID 29368949.
- **S-105.** The title on P. 1/9 and the developers sentence on P. 8/9 are as cited. The PDF metadata are as cited: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014.
- **S-106.** "Published: 27 June 2012"; "Last reviewed: 11 January 2016"; "We checked this guidance and found nothing new". Paragraph 2.1 reads as quoted.
- **S-103.** The footer reads "© 2026 Cincinnati Children's Hospital Medical Center".
- **Search-log claims checked at their sources:**
  - PMC8684566 (Stewart, Lipton) uses "little or none"; PMC6537129 (Lipton, Stewart) uses "minimal or infrequent disability" and grades IVa/IVb;
  - PMC5796955 prints the same HALT-90 table, with "≥20";
  - PMC5812954 describes the HURT areas.
- **Newer versions.** A web search finds no published ICHD-4, only the "Work in Progress" papers of the classification committee. TA260 is current. I found no newer version that changes an element.

### Value sets, codes, units, labels and thresholds (category B)

All of these are correct against the downloaded sources:
- **ICHD-3 code labels** (E-009), pp. 8, 9 and 12.
- **8.2 reference levels and span** (E-032): the Descriptions of 8.2, 8.2.1, 8.2.2 and 8.2.3 (p. 123), and criterion B of 8.2.4, 8.2.5, 8.2.6 (p. 124) and 8.2.8 (p. 125). That gives 15 days per month for non-opioid analgesics, 10 for the other classes and for combined use, and more than three months for all.
- **8.2.6 basis:** the classes of criterion B and note 2 (`classesOf826`, `classesOf821to825`).
- **A1.1 window:** day 1 ± 2, that is, days −2 to +3, with no day 0.
- **Remission:** "must exceed three months".
- **HIT-6:** range 36–78 and four bands.
- **MIDAS:** grades I–IV with the [S-102] labels and bands, and 3-month recall.
- **PedMIDAS:** four grades, with "Greater than 50" shown as `strictLow`.
- **HALT-90:** Table 18 with the overlap at 20; HALT-30 and HALT-90 recall periods.
- **HADS, PHQ-9 and GAD-7:** 0–21 per HADS subscale, 0–27 and 0–21.
- **Responder thresholds:** IHS Q6 (with MIDAS 11–20 and ≥ 20), NICE 1.3.28 and 1.3.29, DMKG/ÖKSG/SKG and the Russian section 7.1.
- **Control levels** of [S-010].
- **The 18 evaluation rules:** offsets, anchors, timings, ages and exclusions.

**Date examples.** I recomputed the date examples of E-007, E-042, INV-049, INV-055 and INV-105, and all are correct. For example:
- 26 February to 25 March is 28 days, and 4 to 31 December is 28 days;
- the stop-on-30-March case keeps NICE 1.3.28 and Box 8 only.

### Fidelity to Stage 1 (category C), from a different angle

For each Statement I tried to construct two outputs:
- **(P) permitted but rejected:** an output that Stage 1 permits but the model rejects;
- **(F) forbidden but admitted:** an output that Stage 1 forbids but the model admits.

| OUT | Constructions tried, and result |
|---|---|
| 001 | **(P)** A treatment-history view with a covered period: always constructible, so no rejection. **(F)** A view with no stated period is excluded by INV-003; headache days only per week, by INV-014. OK. |
| 002 | **(F)** A view showing headache days by peak intensity, or cycle lines, without a label is a SHOULD deviation (`reports`, INV-008). **(P)** A label naming a non-ICHD-3 headache-day definition is excluded, which OUT-004's MUST requires (INV-009). OK. |
| 003 | **(F)** "≥ 80 % completeness = reliable" is a `clinicallyValidatedCutoff` claim (INV-013). **(P)** Completeness as days without data is admitted (`otherCompletenessExpression`). OK. |
| 004–007 | Monthly MUST availability (INV-014, INV-015, INV-108) and SHOULD provision (INV-016, INV-017). Attacks are never merged with days. OK. |
| 008, 013 | MAY; nothing is forced, and nothing is excluded but definitional bounds. OK. |
| 009 | **(F)** A time course without the dose-change marker of a paused course is a SHOULD deviation (`markedKind` covers start, dose change and stop). Weekly values are required for tension-type and cluster headache (INV-001, INV-034). OK. |
| 010, 011 | **(F)** Duration over all attacks without the treated-attack label (INV-020), and the duration of treated attacks as a stand-alone efficacy measure (INV-021). **(P)** A patient with no treated attacks can use `untreatedAttacks`. OK. |
| 012 | Associated symptoms across periods and per treated attack, for migraine (INV-022, INV-072, INV-076). OK. |
| 014–016 | **(F)** An indicator shown as "MOH" is excluded at MUST NOT (INV-048), and one without the prompt at MUST (INV-047). Combined use with a single class is forced to "not reached", as the 8.2.3 comment requires (INV-046). OK. |
| 017 | **(P)** A running follow-up on day 43 is required with its own values (INV-049). The review window is SHOULD in every view (E-039 attribute); it is not excluded. OK. |
| 018 | **(P)** A comparison that only uses 3-month means is not a `ResponseComparison`. It is settled by R01-03 option (a), and it is not excluded either (open world). **(F)** A stopped course shown with an "adequate trial" time point is excluded (INV-058). Continuation decisions are excluded (INV-106). OK. |
| 019 | A percentage change without residual burden is a SHOULD deviation (INV-060). OK. |
| 020 | **(F)** "Non-responder" at a 60 % reduction under NICE 1.3.28 for episodic migraine is excluded; a label without its criterion is a SHOULD deviation. **(P)** Months 3, 5 and 6 cannot carry "modest control" (see "Checked and not raised"). OK. |
| 021, 022 | MUST components for the same periods (INV-068); post-stop comparison with the baseline (INV-070). OK. |
| 023 | **(F)** Pain freedom shown without relief, a label "the response definition that applies", or a summary of the oral form standing in for the subcutaneous form: excluded at SHOULD or SHOULD NOT (INV-071, INV-072, INV-107, `summarisesMedication`). OK. |
| 024, 039 | Every dose change, the response and adherence with each line (INV-109); grouping and order (INV-078). OK. |
| 025 | MAY, labelled with the scheme (INV-080). OK. |
| 026, 027 | **(F)** A MIDAS score of 12 shown as "mild disability", or HIT-6 = 30: excluded (INV-082). Functional impact per domain and severe impairment, compared with baseline (INV-026, INV-027). OK. |
| 028–030 | **(F)** A three-month view stating "chronic migraine": excluded at SHOULD NOT (INV-043). **(F)** An attack on day −2 of a menstruation that the view does not show, marked "outside": excluded (INV-087, `nextWindowDays`). OK. |
| 031–033 | **(F)** A 10-week attack-free period shown as a remission: excluded (INV-089). **(F)** A HADS result shown as "depression": excluded at SHOULD NOT (INV-084). The trigger view's caveats are required (INV-090). OK. |
| 034–038 | All named components (INV-104, INV-105); paediatric (a)–(d) and the caveat (INV-096 to INV-098). A primary migraine index is excluded at SHOULD NOT (INV-091). Caveats on every view (INV-099). OK. |

Every requirement is represented at its Stage 1 strength. The traceability table is correct and complete (mechanical checks below).

### Mechanical checks (category E)

| Check | Result |
|---|---|
| IDs | 67 elements and 110 invariants, with no gaps and no duplicates; no dangling E- or INV- reference. |
| Traceability | 39 rows, in Stage 1 order (OUT-039 after OUT-025), all "full". For every requirement, the Elements and Invariants columns equal the reverse index of the Realises fields: 0 mismatches. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Declarations | 557 names, none declared twice. Every identifier in the `omn` blocks is declared, except bound variables and `refs`, which section 2.5 defines. |
| Typing rule for levels | Checked for every SHOULD, MAY and MUST-with-`when` attribute (`opt`, `set` or `seq`); no violation. |

### Scope sweep (category F)

- **Grep.** I searched for record, enter/entry, input, captur-, logged, stor-, persist-, database, JSON, XML, CSV, FHIR, HL7, serial-, encod-, retention, reminder, answer, data field and algorithm, and read every hit in context.
- **Hits.** Every hit is one of these: the exclusions of section 1; the notation disclaimer; "obtained from diary information; how is out of scope"; the [S-014] HALT-30 quote ("records days affected"); the INV-076 Note that assigning attack lines to headache types would be a derivation; search-log tool names; and "history".
- **Relations.** Every relation takes only output elements, context properties or cited constants as arguments.
- **Thresholds and formulas.** None that is part of the output data is missing.

### Section 8 (category G)

- **ISS-01 and ISS-03 to ISS-11.** Each is founded, and its quotes and locations are correct:
  - 8.2.6 criterion B (p. 124) and note 2 (p. 125);
  - NICE 1.3.9 and 1.3.39, with no review time point;
  - the CG150 population sentence and 1.3.48;
  - the [S-034] flowchart box (p. 52);
  - the [S-010] "Modest Control" sentence;
  - the HURT areas sentence.
- **ISS-02.** It is founded, but its description of the ICHD-3 passage is wrong (R19c-02).
- **No silent workarounds.** No Stage 1 issue is silently worked around.

## Remarks

### R19c-01 Factual error: E-057 Notes give HALT-30 a "lowest band" from which its lower bound would follow, although HALT-30 has no grading
- Item(s): E-057 (Notes); consequential to INV-082 Reading ("at least 0 for MIDAS, PedMIDAS and HALT").
- Problem:
  - **What the Notes say.** "The lower bound 0 of MIDAS, PedMIDAS and HALT follows from their lowest band."
  - **Which instruments "HALT" covers.** It covers HALT-30 as well, since the E-057 axiom sets `scoreRange(halt30) = ScoreRange(low ↦ 0, high ↦ ∅)`.
  - **What the source says.** HALT-30 has no band: [S-014] states that grading is not used by HALT-30.
  - **What the model itself says.** E-057 contains no `GradeBand` for `halt30`, so `banded(halt30)` is false, and it fixes `¬ publishedGrading(halt30)`.
  - **Effect.** The model therefore states a false basis for a number that it takes from a source. Its Notes also contradict its own Definition and Evidence.
  - **The value is still right.** A correct basis is already quoted in E-057 Evidence: HALT counts days, "the unit of each being whole days per one or 3 months" [S-014], and a number of days is not negative. The error is in the statement of the evidence, not in the value.
  - **Why this is a remark.** It is not a wording preference: the sentence asserts something about [S-014] that [S-014] contradicts. PROCESS.md section 2 requires every number taken from a source to rest on its cited quote.
- Evidence:
  - [S-014] "Grading has value in indicating the level of a patient’s personal need and, perhaps, priority for treatment. [...] Grading is not used by HALT-30." (section "The Headache-Attributed Lost Time (HALT) Indices" > "Scoring HALT", the paragraph after Table 18; Europe PMC full text of PMC6734476; quoted in Stage 1 OUT-026 and in E-057 Evidence).
  - [S-014] "HALT (30 or 90) can generate three summed scores from the first four questions (Figs. 3 and 4 ), the unit of each being whole days per one or 3 months" (same subsection, first sentence).
  - Model, E-057: `axiom publishedGrading(midas) ∧ … ∧ ¬ publishedGrading(halt30)`; `gradeBands` has bands for midas, hit6, pedmidas and halt90 only; Notes: "The lower bound 0 of MIDAS, PedMIDAS and HALT follows from their lowest band."
- Required change: correct the sentence in the E-057 Notes so that it states the actual basis of each lower bound. For example: "The lower bound 0 of MIDAS, PedMIDAS and HALT-90 follows from their lowest band; HALT-30 has no grading ("Grading is not used by HALT-30", [S-014]), and its lower bound 0 follows from its unit, "whole days per one or 3 months" [S-014]." No value, axiom or invariant changes.

### R19c-02 Stage 1 issue handling / citation defect: ISS-02 misdescribes the only ICHD-3 passage that uses "simple analgesics"
- Item(s): section 8, ISS-02 (Evidence). The search-log row ""Simple analgesics" occurs only in section 10 (ISS-02)" is correct and needs no change.
- Problem:
  - **What ISS-02 says.** "In the downloaded ICHD-3 text, "simple analgesics" occurs only once, in an unrelated passage (on acute mountain sickness, section 10)."
  - **The topic is wrong.** The phrase occurs once, on p. 139, in the Comments on 10.1.1 High-altitude headache, in a sentence about the treatment of high-altitude headache. Acute mountain sickness is introduced only in the next sentence ("However, acute mountain sickness (AMS) consists of …").
  - **"Unrelated" omits evidence.** The sentence uses "simple analgesics" for "paracetamol (acetaminophen) or ibuprofen". These are drugs of the class that ICHD-3 names "non-opioid analgesics": 8.2.3.1 Paracetamol (acetaminophen)-overuse headache and 8.2.3.2 Non-steroidal anti-inflammatory drug (NSAID)-overuse headache. So ICHD-3 does use the Stage 1 wording, informally, for drugs of 8.2.3, though never as the name of an 8.2 class.
  - **Why this matters.** That is exactly the evidence the human needs for the decision that ISS-02 asks for ("consider correcting the example label in Stage 1"). The conclusion of ISS-02 stands, but its evidence misdescribes the passage it cites and gives no page.
  - **Why this is a remark.** Section 8 entries must be founded and evidenced (PROCESS.md section 4: "the location in the source"; section 9: Stage 1 issue handling). A wrong description of a cited passage is a factual error about the source, not a wording preference.
- Evidence:
  - [S-001] "Most cases of 10.1.1 High-altitude headache respond to simple analgesics such as paracetamol (acetaminophen) or ibuprofen. However, acute mountain sickness (AMS) consists of at least moderate headache combined with one or more of nausea, anorexia, fatigue, photophobia, dizziness and sleep disturbances." (10.1.1 High-altitude headache, Comments, p. 139; the only occurrence of "simple analgesic" in the 211-page text layer, searched page by page in the PDF at the Stage 1 URL of S-001).
  - [S-001] "8.2.3.1 Paracetamol (acetaminophen)-overuse headache" and "8.2.3.2 Non-steroidal anti-inflammatory drug (NSAID)-overuse headache" (classification list, p. 12).
  - Model, ISS-02 Evidence: "In the downloaded ICHD-3 text, "simple analgesics" occurs only once, in an unrelated passage (on acute mountain sickness, section 10)."
- Required change: correct the description and location in ISS-02. For example: ""Simple analgesics" occurs only once in ICHD-3, in the Comments on 10.1.1 High-altitude headache (p. 139), where it names drugs of the 8.2.3 class: "simple analgesics such as paracetamol (acetaminophen) or ibuprofen"; ICHD-3 does not use it as the name of an 8.2 class." Optionally, add one clause to "For the human" saying that this usage shows which ICHD-3 class the Stage 1 example means. The effect on the model and the rest of ISS-02 are unchanged.

## Checked and not raised

- **E-057 Evidence: "the HALT unit is "whole days per one or 3 months"".**
  - [S-014] (and the HALT developers' 2018 paper, PMC5796955) states that unit for the three summed scores of the first four questions. It says that question 5 is "a simple count for which the unit is not whole days", which HALT-90's graded total includes.
  - The whole-number property of the HALT-90 total still holds, because question 5 is a count. The E-057 Evidence also rests it on the whole-number band limits of Table 18.
  - The unit "days" (E-058) matches Table 18's column "Days lost in last 3 months".
  - No change is required. A fixer editing the sentence of R19c-01 may state this precisely.
- **HALT upper bound.** PMC5796955 (not a cited source) says the total lost productive time "should not exceed the number of days in the period of enquiry". The model states no upper bound and says that `high = ∅` means "the model states no upper bound". This would be an optional addition. Not raised.
- **Control levels over mixed months** (INV-064). Over months of 3, 5 and 6 days, "modest control" is excluded and only "insufficient control" is admitted, which [S-010] permits.
  - [S-010] does not say how several months combine.
  - The per-month reading is disclosed (E-046 Notes).
  - Review 10 judged the same pattern (5 and 7 days).
  - I have no new evidence. Not raised.
- **Response comparisons on multi-month means** (OUT-018 "monthly migraine days"; [S-022] "mean number of monthly migraine days"). Fix 01 chose R01-03 option (a), monthly periods, with evidence. Means can be shown as further content (section 3.7). No new evidence. Not raised.
- **Treated-attack lines with an outcome not reported.** INV-072 (SHOULD) asks for a result for every measure on every line, as fixed in R01-07. Missing information is a valid reason for a SHOULD deviation (section 3.2). Not raised; raising it would partly reverse R01-07.
- **OUT-024 Caveat "does not by itself establish eligibility"** has no prohibition invariant. Fix 01 ("Considered and not changed") judged that it states what the list cannot show. INV-101 (SHOULD NOT `replacesClinicalAssessment`) covers an output that claims to establish eligibility. No new evidence. Not raised.
- **E-039 `reviewWindow` SHOULD without a `when` clause, and the conditional last conjunct of INV-050.** The attribute already asks for the window in every follow-up view. A window that reaches beyond a short covered period is shown as a period of the view (INV-003). The two constraints are consistent, so the overlap is redundancy, not contradiction. Not raised.
- **Conditions of responder criteria for a treatment given for "1. Migraine" without a subtype** (`episodicMigraineOnly`). INV-001 keeps the subject's types at one level of the hierarchy, and the reading on the treatment is settled (fix 12; watch point 4). Not raised.
- **Settled in earlier iterations, not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the "> 3 months" readings (INV-045, INV-089);
  - the E-041 window readings, `excludes`, ages and timings;
  - INV-060 with INV-061 for short periods (fix 02);
  - "every view is a summary output";
  - the 24-hour outcomes of cluster summaries;
  - the HIT-6 1-month recall;
  - HADS subscales only;
  - the MIDAS labels of [S-102];
  - `concerns` for mixed subjects (OUT-037);
  - "one item suffices" for the overview's treatment effect (watch point 1).
- **Oscillation watch points.** Neither remark touches an item named in the eight watch points of the iteration-16 check, and neither reverses an earlier fix:
  - R19c-01 changes one explanatory sentence of E-057, which no earlier remark or fix changed in substance;
  - R19c-02 changes the evidence wording of ISS-02, which no earlier remark addressed.

## Notes on frozen items (for the human)

None. `FROZEN_ITEMS.md` does not exist, and no item of v18 carries a FROZEN marker.
