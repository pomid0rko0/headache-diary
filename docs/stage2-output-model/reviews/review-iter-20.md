# Review — iteration 20
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v19
Date: 2026-10-21

## Summary

This is the main review of iteration 20. It is an independent fact-check and review of v19.

**State of the files.**
- `OUTPUT_MODEL.md` is byte-identical to `history/v19.md` (checked with `cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a FROZEN marker.
- v19 differs from v18 only in the E-057 Notes (the basis of the HALT-30 lower bound), ISS-02, section 9, the search log and the change log (fix 19, R19c-01 and R19c-02).

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5;
- v19, all sections, every element and every invariant;
- the oscillation check after iteration 16, with its eight watch points, and the watch points of the check after iteration 12;
- review 19c and fix 19.

I consulted the earlier reviews and fixes by search, to see which points were settled or declined.

**My own work.**
- Downloads: into the fresh directory `/tmp/r20-dl-2LW0jf`, outside the repository.
- Text extraction: into `/tmp/r20-txt-dqT4Sb`.
- Scripts: in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r20/scripts/` (`strip.py`, `match.py`, `mech.py`, `decl.py`), run with `python3 -I`.

**Result.**
- **Values and citations.** All values, codes, labels, ranges, thresholds, offsets and conformance levels are correct against their sources. 512 quoted fragments were checked, and none is misquoted.
- **Mechanical checks.** They pass.
- **Scope sweep.** It finds nothing.
- **Fidelity.** Every OUT requirement is represented at its Stage 1 strength.
- **One remark (R20-01).** It concerns section 8 and the reference rule of section 3.5:
  - ISS-03 records that some Stage 1 statements name migraine days without the "for patients with migraine" condition of OUT-005. It also asks the human to decide whether those components apply only to patients with migraine.
  - ISS-03 lists four such statements (OUT-018, OUT-022, OUT-028, OUT-035). OUT-019 (SHOULD) and OUT-030 (MUST) are of the same kind, and ISS-03 omits them.
  - The model applies the same no-condition reading to OUT-019 and OUT-030 (E-044, INV-060; E-060, INV-086). It does so without recording the issue for them, without pointers from these elements, and without asking the human about them.
  - The required change concerns text only: section 8, section 3.5, Notes pointers and two traceability reasons. It changes no predicate or level.

## Verification coverage

### Downloads and method

All downloads used `curl` through the configured proxy, and every request returned HTTP 200.

**PDFs** (extracted page by page with `pdftotext -raw` and `-layout`):
- [S-001] ICHD-3 (211 pp.), [S-002] (19 pp.), [S-005] (14 pp.), [S-007] UCL manuscript (39 pp.);
- [S-008] (31 pp.), [S-010] (11 pp.), [S-016] SIGN 155 (64 pp.), [S-018] AAN/AHS Clinician Summary (12 pp.);
- [S-030] (86 pp.), [S-033] (92 pp.), [S-034] (53 pp.), [S-035] (92 pp.), [S-105] (9 pp.).

**Web pages** (markup removed):
- [S-015]: the NICE CG150 Recommendations page ("Last updated: 03 June 2025") and its Overview page;
- [S-028]: the NVN module;
- [S-103]: the Cincinnati Children's PedMIDAS page (footer "© 2026");
- [S-106]: TA260, the Overview page ("Last reviewed: 11 January 2016"), chapter 1 and chapter 2.

**Europe PMC full-text XML:**
- [S-004], [S-011], [S-012], [S-013], [S-014], [S-023];
- [S-101] PMC3057423, [S-102] PMC4406925, [S-104] PMC183845;
- PMC8684566 and PMC6537129 (MIDAS label variants named in the search log).

**Rendered and read by eye:**
- ICHD-3 p. 190: A1.1.1 B "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)", A1.1.2 B "Occurring on day 1 ± 2 (i.e. days −2 to +3)" and note 2 "there is no day 0". In the text layer the "±" and "−" glyphs are unmapped.
- The [S-034] title page, which is an image: "Возрастная группа" "дети".

**Scripts.**
- `match.py` takes every double-quoted string outside `omn` blocks on a line with an `[S-NNN]` tag and attributes it to the nearest preceding tag. It splits the string at "[...]" and keeps fragments with at least 6 word characters.
- Each fragment is searched in three places, in this order:
  - the tagged source, page by page (NFKC, quotes and dashes unified, line-end hyphens joined, whitespace collapsed; then letters and digits only);
  - the other sources tagged on the line;
  - Stage 1 v18.

  Fragments still unmatched were read by hand.

### Quotes per source

| Source (nearest tag) | Fragments | In tagged source | Other tag on line | Stage 1 | By eye / by hand | Not source text | Not found | Unreachable (tried) |
|---|---|---|---|---|---|---|---|---|
| S-001 ICHD-3 | 72 | 63 (labels pp. 8, 9, 12; 8.2–8.2.8 pp. 122–125; 8.2.3 comment p. 123; Definitions of terms pp. 209–210; remission p. 209; A1.1 note 2 p. 190; "simple analgesics" p. 139; "ibuprofen or other NSAIDS" p. 105, comment on 7.3.2, heading p. 104) | 0 | 4 | 2 (A1.1.1/A1.1.2 windows, p. 190 rendered) | 3 (search-log row label; explanatory text caught by the regex) | 0 | 0 |
| S-002, S-005, S-007 | 30 | 17 (S-007 p. 10 item a of section 2.2, pp. 22, 25; S-005 p. 8) | 7 | 6 | 0 | 0 | 0 | 0 |
| S-008 IHS 2024 | 29 | 21 (Q2 p. 9, footnote p. 9; Q4 p. 11; Q6 Recommendations p. 12; Q6 Evidence p. 13; Q13 p. 17) | 7 | 0 | 0 | 1 | 0 | 0 |
| S-010 IHS 2025 | 48 | 39 (all four control levels, the migraine-day paragraph and the "proxy" sentence, p. 6) | 1 | 8 | 0 | 0 | 0 | 0 |
| S-011, S-012, S-013, S-016, S-018, S-023, S-029, S-030, S-032, S-042 | 51 | 34 (S-016 PDF p. 7 and p. 20; S-018 pp. 1, 7, 8; S-011 Background paragraphs 1–2; S-030 PDF p. 19; S-013 "If therapy was inadequate …") | 9 | 6 | 0 | 2 | 0 | 0 |
| S-014 Lifting The Burden | 45 | 31 (HALT versions, "Scoring HALT", Table 18, "Grading is not used by HALT-30", HURT areas, "Grading has value …") | 2 | 9 | 0 | 3 | 0 | 0 |
| S-015 NICE CG150 | 55 | 38 (1.3.9, 1.3.21, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48, the headings, the Overview population sentence) | 4 | 12 | 0 | 1 | 0 | 0 |
| S-028 NVN | 12 | 10 (Aanbeveling; PICO of "Zoeken en selecteren") | 1 | 0 | 0 | 1 | 0 | 0 |
| S-033 Russian adults | 49 | 19 (title p. 1; abbreviations p. 4; section 3.3 pp. 39–41; section 7.1 p. 53) | 10 | 0 | 0 | 20 (4 translations; 16 regex fragments of explanatory text) | 0 | 0 |
| S-034 Russian children | 20 | 8 (section 2 p. 17; flowchart p. 52) | 2 | 4 | 2 (title page, rendered) | 4 (translations) | 0 | 0 |
| S-035 Turkish protocol | 50 | 33 (3.3 b p. 23; Kutu 8 p. 48; 3.6.3.9 p. 57; headings pp. 7, 77, 82; 7.1 p. 83; 7.3 p. 86, "2 k ez" as printed) | 4 | 0 | 0 | 13 (translations and regex fragments) | 0 | 0 |
| S-101 to S-106 | 51 | 30 (S-101 "Data sources"; S-102 "Migraine-related disability"; S-103 grading table; S-104 HADS construction; S-105 P.6/9 and P.8/9; S-106 paragraph 2.1) | 3 | 1 | 2 (TA260 chapter 1 "less than a 30% reduction in headache days per month after 2 treatment cycles"; PMC8684566 "little or none") | 15 (13 search-log query strings; 2 regex fragments) | 0 | 0 |
| **Total** | **512** | **343** | **50** | **50** | **6** | **63** | **0** | **0** |

**Translations.** I read every Stage 2 translation against its original, and all are faithful:
- [S-028]: the PICO line;
- [S-033]: the title page, the section 3.3 comment, the PREEMPT recommendation and the p. 41 comment;
- [S-034]: the flowchart box, the title page and section 2;
- [S-035]: Kutu 8 items 2 and 7; 3.3 b; the 3.6.3.9 sentences; the section 6 and chapter 7 headings; the 7.1 and 7.3 items.

### Citation metadata and versions

- **Europe PMC records** agree with section 10 for:
  - S-101: Cephalalgia 2011;31(3):357–367; 10.1177/0333102410379890; PMID 20819842;
  - S-102: J Headache Pain 2015;16:24; 10.1186/s10194-015-0503-y; PMID 25902814;
  - S-104: HQLO 2003;1:29; 10.1186/1477-7525-1-29; PMID 12914662; subject "Commentary".
- **S-105.** The PDF metadata agree with section 10: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014. The developers sentence is on P.8/9.
- **S-106.** "Published: 27 June 2012"; "Last reviewed: 11 January 2016"; paragraph 2.1 reads as quoted.
- **Location claims of the E-041 Notes** that are not quotes all hold:
  - NICE 1.3.21 (acupuncture over 5 to 8 weeks, migraine);
  - AAN/AHS 17B (tapering after 6 months);
  - the SIGN patient checklist "after 2–8" and "after 6–8" weeks (PDF pp. 40–41);
  - the IHS Q2 comment on raising the onabotulinumtoxinA dose after the first cycle (p. 9);
  - Turkish 6.2.2, "Tedavi süresi en az 4 ay" (PDF p. 80);
  - the Russian 12-week botulinum interval (p. 41);
  - the NVN placebo response that stabilises after 16 weeks.
- **Newer versions.**
  - A web search finds no EHF guideline on anti-CGRP antibodies after the 2022 update.
  - CG150 is current (last updated 3 June 2025), and TA260 is current.
  - Earlier reviews found no ICHD-4. I found no newer version that changes an element.

### Value sets, codes, units, labels and thresholds (category B)

All of these are correct against the downloaded sources:
- **ICHD-3 code labels** (E-009), pp. 8, 9 and 12.
- **8.2 reference levels and span** (E-032): 15 days per month for non-opioid analgesics; 10 for ergotamine, triptans, opioids, combination analgesics, other medication and combined use; more than three months for all (pp. 122–125).
- **8.2.6 classes** (`classesOf826`) and note 2.
- **A1.1 window:** day 1 ± 2, that is, days −2 to +3, with no day 0.
- **Cluster remission:** "must exceed three months".
- **HIT-6:** range 36–78 and the four impact bands.
- **MIDAS:** grades I–IV with the [S-102] labels and bands, and 3-month recall.
- **PedMIDAS:** the four grades, with "Greater than 50" shown as `strictLow`.
- **HALT-90:** Table 18, with the overlap at 20; HALT-30 and HALT-90 recall periods.
- **HADS, PHQ-9 and GAD-7:** 0–21 per HADS subscale, 0–27 and 0–21.
- **Named responder criteria:**
  - NICE 1.3.28: 50 % episodic, 30 % chronic;
  - NICE 1.3.29: 30 % headache days;
  - IHS Q6: 50 % and 30 %, MIDAS ≥ 5 points for baseline 11–20 and ≥ 30 % for baseline ≥ 20, HIT-6 ≥ 5 points;
  - DMKG/ÖKSG/SKG and Russian section 7.1.
- **IHS 2025 control levels.**
- **The 18 evaluation rules:** offsets, anchors, timings, ages and exclusions, each against its quote.
- **Date examples:** I recomputed those of E-007, E-042, INV-049, INV-055 and INV-105, and all are correct. Examples: 67 and 43 days; 26 February to 25 March, 28 days; the stops on 10 February and 30 March; the 10 March withdrawal with day 43 and 6 April.
- **Span length (INV-045):** four monthly periods both for calendar months and for 28-day periods.

### Fidelity to Stage 1 (category C), requirement by requirement

| OUT | Result |
|---|---|
| 001 | OK. Period with start, end and length (E-003, E-005, INV-002, INV-003). Monthly frequency outputs at MUST (INV-014, INV-015, INV-108). Equal-length comparison (INV-037, INV-055). Caveat met by `lengthDays`. |
| 002 | OK. INV-008 (SHOULD) over every form of the four measures (`reports`). |
| 003 | OK. INV-011, INV-012; no validated cut-off (INV-013, SHOULD NOT). |
| 004 | OK. Every period of the selected time range (INV-014, MUST); ICHD-3 definition (INV-009). |
| 005 | OK. For patients with migraine (INV-015, MUST); label SHOULD. |
| 006, 007 | OK. Provision SHOULD (INV-016, INV-017); monthly availability MUST where provided (INV-108). Attacks are a separate element (E-019). |
| 008 | OK. MAY elements (E-020 to E-022), with optional exploratory label. |
| 009 | OK. Time course with start, dose-change and stop markers (INV-034 to INV-036); weekly values where relevant (INV-001, INV-034). |
| 010 | OK. Stated scale (INV-018); comparison between periods (INV-039). |
| 011 | OK. INV-019; label for treated attacks (INV-020); Caveat as SHOULD NOT (INV-021). |
| 012 | OK. Across periods (INV-022) and per treated attack (INV-072, INV-076). |
| 013 | OK. MAY (E-027). |
| 014 | OK. Total, class and drug together (INV-023); relations (INV-024). |
| 015 | OK. INV-025. |
| 016 | OK. Per period, class and combined use, with code, level, span and basis (INV-044 to INV-046); prompt at MUST (INV-047); not a diagnosis at MUST NOT (INV-048). |
| 017 | OK. INV-049 to INV-052. |
| 018 | OK. INV-053 to INV-059; continuation decision at MUST NOT (INV-106). The migraine-day components follow ISS-03. |
| 019 | **Represented** at SHOULD (E-044, INV-060, INV-061). The migraine-day component carries no "patients with migraine" condition, and ISS-03 does not record this (R20-01). |
| 020 | OK. INV-062 to INV-065. |
| 021 | OK. INV-068, INV-069, INV-071, INV-102. |
| 022 | OK. INV-070, INV-103. |
| 023 | OK. INV-071 to INV-075; INV-107 at SHOULD NOT. |
| 024 | OK. INV-077 to INV-079, INV-109. |
| 025 | OK. MAY (E-056, INV-080). |
| 039 | OK. INV-066, INV-067, INV-104, INV-109. |
| 026 | OK. INV-081, INV-082; ISS-06. |
| 027 | OK. INV-026, INV-027. |
| 028 | OK. INV-040 to INV-043. |
| 029 | OK. INV-028 to INV-030; ISS-09. |
| 030 | **Represented** at MUST (E-060, E-061, INV-086, INV-087). The view is required for every subject who menstruates, also without migraine, and ISS-03 does not record this (R20-01). |
| 031 | OK. INV-088, INV-089. |
| 032 | OK. MAY, with caveats at SHOULD (INV-090, INV-100, INV-110). |
| 033 | OK. INV-083 to INV-085. |
| 034 | OK. INV-094, INV-104; ISS-04. |
| 035 | OK. INV-095, INV-105; ISS-03. |
| 036 | OK. INV-096 to INV-098; E-041 `ruleRuChildren`. |
| 037 | OK. INV-091 to INV-093. |
| 038 | OK. INV-099 to INV-101. |

Every conformance level matches the strength of the Stage 1 statement part it realises. Every SHOULD NOT and MUST NOT part is a `¬` invariant at that level.

### Mechanical checks (category E)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), with no gaps and no duplicates. No dangling E- or INV- reference. Every S reference lies in S-001–S-046 or S-101–S-106, and exactly the 39 Stage 1 OUT IDs are referenced. |
| Fields | 177 items, each with one Realises and one Conformance field. Each invariant has one Predicate and one Reading. |
| Traceability | 39 rows, in Stage 1 order (OUT-039 after OUT-025). For every requirement, the row's E and INV sets equal the reverse index of the Realises fields: 0 mismatches. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Declarations | 181 `omn` blocks; 551 declared names by my script's count, none declared twice. Every identifier used is declared, bound, an attribute, or a keyword or primitive. The exceptions are the `let`-bound A, C and D, `refs` (section 2.5) and the `_⊑_` infix form. Every attribute selection `e.a` names a declared attribute or component. |
| Typing rule for levels | No SHOULD, MAY or MUST-with-`when` attribute has a type other than `opt`, `set` or `seq`. |
| Partial terms | Spot-checked: `days`, `first`, `last`, `min`, `÷`, `periodEndFrom` and `opt` values used as single values. All are guarded, as section 2.6 requires. |

### Scope sweep (category F)

- **Grep.** I searched for enter, entry, record, input, captur, logged, stor, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, reminder, answer, algorithm, obtained, calculat, comput, field, questionnaire, data-entry, "diary data" and "decision logic", and read every hit in context.
- **Hits.** Every hit is one of these:
  - an exclusion statement (sections 1, 2.1, 2.7);
  - an out-of-scope note (E-014, E-019, E-033, E-057, INV-076);
  - Stage 1 wording ("efficacy of treatment from diary data");
  - the notation's "records with named attributes";
  - a search-log tool name;
  - "history".
- **Relations.** Every relation takes only output elements, context properties or cited constants as arguments.
- **Thresholds and formulas.** None that is part of the output data is missing.

### Section 8 (category G)

- **ISS-01, ISS-02, ISS-04 to ISS-06 and ISS-08 to ISS-11.** Each is founded, and its quotes and locations are correct:
  - ISS-02 after fix 19: p. 139, p. 12 and p. 105 verified;
  - ISS-10: 1.3.9, 1.3.39 and the [S-034] box (p. 52);
  - ISS-11: the CG150 population sentence and 1.3.48.
- **ISS-03.** It is founded, but its description of Stage 1 is incomplete (R20-01).

## Remarks

### R20-01 Stage 1 issue handling: ISS-03 and the reference rule omit OUT-019 and OUT-030, which also name migraine days without the "patients with migraine" condition
- Item(s): section 8, ISS-03 ("Stage 1", "Effect on the model" and "For the human"); section 3.5 (reference rule, the list "(OUT-018, OUT-022, OUT-028, OUT-035)"); E-044 Notes and E-060 Notes (no pointer to ISS-03); section 7, the coverage reasons of rows OUT-019 and OUT-030.
- Problem:
  - **What ISS-03 records.** Stage 1 OUT-005 reports migraine days only "For patients with migraine". ISS-03 lists the Stage 1 statements that name migraine days without that condition and without a reference to OUT-005: "OUT-018 (...), OUT-022 (...), OUT-028 (...) and OUT-035 (...)". The model "modelled [these] as stated, without the condition", so that "For a subject without migraine [...] these outputs show migraine days that are all 0". The human is asked to "decide whether migraine-day components of OUT-018, OUT-022, OUT-028 and OUT-035 apply only to patients who have (or, for OUT-028, may have) migraine". Section 3.5 states the same rule with the same list of four.
  - **Two more Stage 1 statements are of the same kind.** I searched every Stage 1 Statement for migraine-specific measures. Two more name migraine days without the OUT-005 condition and without a reference to OUT-005:
    - **OUT-019 (SHOULD):** "Wherever the output shows a relative (percentage) change in migraine or headache days, it SHOULD show next to it the absolute number of migraine days and moderate/severe headache days per month that remain on treatment."
    - **OUT-030 (MUST):** "For patients who menstruate, the diary output MUST be able to show migraine attacks and migraine days in relation to the days of menstruation across consecutive cycles [...]". Its only stated condition is menstruation.
    - OUT-008 (MAY) also names "periods without migraine days" without the condition. It is MAY, so no requirement depends on it.
  - **The model applies the no-condition reading to both, without recording it.**
    - **OUT-019.** E-044 declares `migraineDays : →DayCount core`, and INV-060 applies to every change with `ch.reference.measure ∈ {migraineDays, headacheDays}` and a percentage form, with no subject condition; INV-061 fixes `rb.migraineDays.measure = migraineDays`. Example: a preventive treatment of tension-type headache. Its response comparison shows headache-day changes in percentage form at MUST (INV-056, E-040), and each of these changes then SHOULD be shown with "migraine days per month that remain on treatment" (always 0).
    - **OUT-030.** INV-086 (MUST) requires the menstrual-relation view for every context with `menstruatesDuring(c, c.timeRange)`, and E-060 makes `migraineDays` and `attacks` MUST in every cycle line. A subject who menstruates and has only tension-type headache must therefore be offered, at MUST, a view of migraine attacks and migraine days (all empty) against the A1.1 perimenstrual window, with its count of complete cycles. The cycle lines of the overview (INV-105, OUT-035 "where relevant, the relationship to menstruation") carry the same migraine-day and attack content.
    - **What is missing.** Neither E-044 nor E-060 (nor INV-060 or INV-086) points to ISS-03. The traceability rows OUT-019 ("see ISS-05") and OUT-030 (no issue named) mention none. ISS-03 does not ask the human about these two requirements.
  - **Why this matters.** ISS-03 asks the human to decide the migraine-day condition for four requirements. Whatever the human decides there, OUT-019 and OUT-030 would keep the opposite treatment unless the human is told about them. OUT-030 is the stronger case, because its whole output is migraine-specific and it is MUST:
    - its Rationale reads "Distinguishing pure menstrual from menstrually related migraine matters for treatment";
    - the window it names belongs to a subclassification of migraine in ICHD-3 (Evidence).
  - **Why this is a remark** (PROCESS.md sections 4 and 9):
    - section 4 requires each Stage 1 issue to be recorded in section 8 and pointed to from the Notes of every element it directly affects ("The model keeps following Stage 1 and does not deviate silently");
    - section 9 lists "Stage 1 issue handling" as a remark category;
    - the "Stage 1" field of ISS-03 states which requirements are concerned, and that statement is incomplete about Stage 1;
    - the point was never raised as a remark, so no fixer declined it. ISS-03 and the section 3.5 list are unchanged since v00 (checked in `history/v00.md`, `v05.md`, `v10.md`, `v15.md` and `v19.md`).
- Evidence:
  - Stage 1 OUT-005 Statement: "For patients with migraine, the diary output MUST report the number of migraine days per reporting period (monthly migraine days)."
  - Stage 1 OUT-019 Statement, quoted above. Its Rationale and Evidence are migraine-specific, for example [S-017] "The aim of preventer treatment is to reduce migraine days to 4 or less a month." (quoted in OUT-019).
  - Stage 1 OUT-030 Statement, quoted above. Its Rationale is "Distinguishing pure menstrual from menstrually related migraine matters for treatment". Its Evidence includes [S-015] "Diagnose menstrual‑related migraine using a headache diary [...] for at least 2 menstrual cycles." and [S-001] "The importance of distinguishing between A1.1.1 Pure menstrual migraine without aura and A1.1.2 Menstrually related migraine without aura is that hormone prophylaxis is more likely to be effective for the former." (A1.1 comments, p. 190).
  - [S-001] "This subclassification of 1.1 Migraine without aura is clearly applicable only to menstruating women as defined above." (A1.1, Comments, first sentence, p. 190; at the Stage 1 URL of S-001; in the text layer the word is broken as "with-/out" and "subclassification" carries the "ﬁ" ligature), and A1.1.1 criterion A: "Attacks, in a menstruating woman, fulfilling criteria for 1.1 Migraine without aura and criterion B below" (p. 190). These show that the window of OUT-030 is defined for migraine.
  - Model, section 3.5: "Where a statement names a measure without such a reference (OUT-018, OUT-022, OUT-028, OUT-035), the model adds no condition that the statement does not state (see ISS-03 in section 8)."
  - Model, ISS-03, "For the human": "decide whether migraine-day components of OUT-018, OUT-022, OUT-028 and OUT-035 apply only to patients who have (or, for OUT-028, may have) migraine."
  - Model, E-044 Notes: "... See ISS-05." E-060 Notes and INV-086 Notes: no pointer to ISS-03.
- Required change: record the issue for OUT-019 and OUT-030. Do not change any predicate, condition or level.
  - **What stays unchanged.** The model keeps following Stage 1, as it does now. In particular, no migraine condition is added to INV-086, INV-060 or INV-105. Adding one would deviate from Stage 1, and it would also touch the menstrual-relation watch point (iteration-12 watch point 4; iteration-16 watch point 7).
  - **(a) Preferred: extend ISS-03.**
    1. In "Stage 1", add OUT-019 ("the absolute number of migraine days and moderate/severe headache days per month that remain on treatment") and OUT-030 ("For patients who menstruate, the diary output MUST be able to show migraine attacks and migraine days in relation to the days of menstruation"). Optionally add OUT-008 ("periods without migraine days", MAY).
    2. In "Effect on the model", add that these are also modelled as stated, without the condition:
       - E-044, INV-060 and INV-061: a residual migraine-day count next to every percentage change in migraine or headache days, whatever the subject's headache types;
       - E-060, E-061, INV-086 and INV-087, with the cycle-line conjunct of INV-105: the menstrual-relation view at MUST for every time range during which the subject menstruates, whether or not the subject has migraine.
    3. In "For the human", extend the decision to OUT-019 and OUT-030, and say that OUT-030 is MUST.
    4. Add OUT-019 and OUT-030 to the list in the reference rule of section 3.5.
    5. Add a pointer to ISS-03 in the Notes of E-044 and E-060 (optionally also INV-060 and INV-086), and "see ISS-03" in the coverage reasons of section 7 rows OUT-019 and OUT-030.
  - **(b) Alternative: a new section 8 entry** (for example ISS-12) for OUT-019 and OUT-030, with the same evidence, effect and question, and the same pointers. In that case, add a cross-reference between ISS-03 and the new entry, so that the human decides the migraine-day condition consistently.

## Checked and not raised

- **The v19 changes.**
  - E-057 Notes (HALT-30): the basis of the lower bound now matches [S-014].
  - ISS-02: all four new [S-001] quotes verified (p. 139; p. 12; p. 105, under the 7.3.2 heading on p. 104).
  - Search-log and change-log entries: consistent with the files.
- **HALT-30 "total score".** [S-014] gives HALT-30 three summed scores (lost paid work time, lost household work time, total lost productive time), and question 5 is "retained in HALT-90" only. The model calls the HALT-30 value a total score, without naming the summed score. The third summed score is itself a total, so there is no evidence of a wrong value or unit. Not raised.
- **HALT-90 total unit.** Question 5 is a count whose unit "is not whole days", and E-058 states the HALT unit as days. Table 18 heads the graded score "Days lost in last 3 months", and review 18 judged this. No new evidence. Not raised.
- **OUT-019 trigger.** INV-060 is not triggered by a percentage change in moderate/severe headache days. Stage 1 names "migraine or headache days", which are the measures of OUT-004 and OUT-005. This is a reading of Stage 1, not a defect. Not raised.
- **Periods that reach beyond the as-of date** (a comparison of a treatment started on the as-of date). Review 18 settled this as a partially covered period with its completeness shown, and review 19b concurred. Not raised.
- **The E-060 lead-in wording on diary information.** Review 05 settled it, and it is a watch-point item. Not raised.
- **Settled points, not reopened (no new evidence):**
  - the HIT-6 1-month recall (reviews 01, 03);
  - HADS subscales only;
  - the MIDAS labels of [S-102];
  - "baseline administration" as any earlier administration;
  - INV-106 at MUST NOT;
  - the "> 3 months" readings;
  - the E-041 readings, timings, ages and `excludes` (watch point 5);
  - "one item suffices" for the overview's treatment effect (watch point 1);
  - INV-027 tied to preventive treatments (OUT-027 Rationale: "the baseline against which treatment is evaluated");
  - the redundancy between E-039 `reviewWindow` and INV-050.
- **Section 4 relation diagram.** It omits `AcuteTreatmentSummary → OutcomeSummary`. The diagram is an informal overview, and the reference is declared formally in E-051. Not a remark.
- **Multilingual search for the Stage 2 value sets.** The search log covers German, French, Italian and Spanish searches and states why other languages were not searched: the developers' value sets are in English. I found no evidence of a non-English source that would change a value set. Not raised.
- **Oscillation watch points.** R20-01 changes only text: section 8, the section 3.5 list, Notes pointers and two traceability reasons. It changes no predicate, condition or level of any watch-point item. In particular, it does not touch INV-086, INV-087, INV-105, E-060 or E-061 in substance (iteration-12 watch point 4; iteration-16 watch point 7), and it reverses no earlier fix.

## Notes on frozen items (for the human)

None. `FROZEN_ITEMS.md` does not exist, and no item of v19 carries a FROZEN marker.
