# Review — iteration 13
VERDICT: REMARKS
REMARK_COUNT: 3
Reviewed version: v12
Date: 2026-10-21

## Summary

This is the main review of iteration 13: an independent fact-check and review of v12. `OUTPUT_MODEL.md` is byte-identical to `history/v12.md`.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, OUT-039 after OUT-025), section 5, and section 6 as needed;
- v12: every element, every invariant, and sections 7 to 12;
- review 12 and fix 12 (including the fix-12 time-frame and trigger sweeps), the v11 → v12 diff;
- the oscillation check after iteration 12 and its seven watch points;
- the parts of earlier reviews and fixes that concern the items of my remarks (review 02 R02-06; review 10 and fixes 09 and 10 on the type scope of acute-treatment summaries; fix 11 quantifier sweep on OUT-035).

**Earlier decisions.** FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. None of my remarks reverses an earlier fix (each remark states its relation to the watch points).

**Result.**
- **Citations.** No defects. 352 source fragments are verbatim at their stated locations (348 by script, 4 by hand). 9 fragments could not be re-checked because two sites were unreachable (S-028 in maintenance; S-007 behind a Cloudflare block); all 9 are unchanged since v06/v05 and were verified by earlier reviews.
- **Value sets, codes, labels, thresholds, offsets.** No defects.
- **Mechanical checks.** All pass.
- **Scope sweep.** No input, storage or derivation-from-input content.
- **Three remarks**, all on constraints that are weaker than the Stage 1 statement part or caveat they realise:
  - **R13-01 (coverage gap).** The headache-type scope of the intensity, associated-symptom, most-bothersome-symptom and acute-treatment values required by INV-039, INV-069, INV-071, INV-104 and the `acuteTreatmentEffectiveness` branch of INV-062 is unconstrained. These requirements are met by values scoped to a headache type that the subject does not have (or to only one of its types), which report none (or part) of the attacks and headaches that OUT-010, OUT-021 and OUT-023 ask for.
  - **R13-02 (coverage gap).** INV-098, the paediatric "supportive information" caveat (OUT-036 Caveat), is triggered only by the first day of a view's covered period (v12). A view that covers a later period but shows paediatric outputs of childhood periods (a comparison whose baseline lies in adolescence, which INV-097 itself treats as paediatric; a PedMIDAS result completed in childhood) escapes it.
  - **R13-03 (formal defect: missing definitional relation).** The factor dates and attack onsets of a trigger co-occurrence view (E-065) are not tied to the period the view covers. A view can state one reporting period and show dates of another, with the completeness indicator of the wrong period (OUT-001, OUT-003).

## Verification coverage

### Method

- **Downloads.** All with `curl` (through the configured proxy) into the fresh directory `r13dl/` of the session scratchpad under `/tmp`, outside the repository.
  - Stage 1 URLs (HTTP 200): S-001 (211 pp.), S-002, S-003, S-005, S-006, S-008 (31 pp.), S-010 (11 pp.), S-015 (Recommendations page, "Last updated" datetime 2025-06-03, and Overview page), S-016 (64 pp.), S-018 (12 pp.), S-030 (86 pp.), S-033 (92 pp.), S-034 (53 pp.), S-035 (92 pp.).
  - Europe PMC full-text XML (HTTP 200): S-011 (PMC9188162), S-014 (PMC6734476), S-023 (PMC9607711), S-042 (PMC12279330), S-101 (PMC3057423), S-102 (PMC4406925), S-104 (PMC183845); for the search-log claims: PMC6537129, PMC8684566, PMC5796955, PMC5812954.
  - Other pages (HTTP 200): S-103 (Cincinnati Children's PedMIDAS page), S-105 (PHQ/GAD-7 manual PDF, 9 pp.), S-106 (TA260 overview, chapter 1 and chapter 2 pages); the PMC page of S-101.
  - **Unreachable:**
    - S-028 (richtlijnendatabase.nl): three attempts returned HTTP 200 (once 307) with the page "Deze pagina is tijdelijk niet bereikbaar"; web.archive.org and archive.org reset the connection.
    - S-007 (UCL Discovery accepted manuscript): HTTP 403 Cloudflare "Attention Required" from both UCL URL forms, also without a browser user agent; the SAGE PDF returned 403; Europe PMC lists the article as not open access; web.archive.org reset the connection.
- **Extraction.** PDFs page by page with `pdftotext -raw` and `-layout`; HTML/XML with scripts and markup removed and entities unescaped. ICHD-3 p. 190: the window glyphs read as `\x05` (±), `\x06` (−) and "þ" (+). The S-034 title page (an image) was rendered with `pdftoppm` and read.
- **Scripts** (session scratchpad, `r13/`, run with `python3 -I`): `quotes.py` (fragment search), `nf.py` (classification of misses), `mech.py` (IDs, references, traceability, levels, typing rule), `names.py` (names and attribute selections in `omn` blocks), `html2txt.py`.
- **Quote search.** Every double-quoted string outside the `omn` blocks on a line that carries an `[S-NNN]` tag was split at `[...]`: 452 fragments. Each was searched in the source of the preceding tag, then in the other sources tagged on the line, in three passes (NFKC/whitespace/quotes/dashes; line-end hyphens; letters and digits only), and the page of each hit was compared with the stated location. Misses were then searched in Stage 1 v18 and, for search-log claims, in the papers named.

### Citations

| Source | Fragments | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 | 59 | 59: 57 by script (labels pp. 8, 9, 12; 8.2–8.2.8 pp. 122–125; 8.2.3 comment p. 123; remission p. 209; "simple analgesics" only p. 139); 2 by hand (A1.1.1/A1.1.2 window, p. 190, glyph mapping) | 0 | 0 |
| S-002, S-005 | 8 | 8 (S-002 pp. 10–12 PDF; S-005 p. 9 PDF) | 0 | 0 |
| S-008 IHS 2024 | 29 | 29 (Q2 p. 9 and summary p. 5; Q4 p. 11; Q6 p. 12; Q6 Evidence p. 13; Q13 p. 17), 2 of them tagged under another source on their line | 0 | 0 |
| S-010 IHS 2025 | 37 | 37, all control levels and the migraine-day definition sentences on p. 6 | 0 | 0 |
| S-011, S-014, S-023, S-042 | 49 | 49 (S-014 incl. Table 18 "Grading of HALT-90", HALT recall sentences, "whole days per one or 3 months") | 0 | 0 |
| S-015 NICE CG150 | 44 | 44 (1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48; Overview population sentence) | 0 | 0 |
| S-016 SIGN 155, S-018 AAN/AHS | 24 | 24 (S-016 PDF p. 7 = printed p. 1, PDF p. 20; S-018 pp. 1, 7, 8) | 0 | 0 |
| S-030 | 3 | 3 (PDF p. 19) | 0 | 0 |
| S-033 Russian adults | 23 | 23 (p. 1 title; p. 4 "М – мигрень"; pp. 39, 40, 41, 53) | 0 | 0 |
| S-034 Russian children | 13 | 13: 11 by script (p. 17, p. 52 flowchart); 2 by hand ("Возрастная группа" … "дети" on the rendered title page) | 0 | 0 |
| S-035 Turkish protocol | 28 | 28 (Kutu 8 PDF p. 48; 3.6.3.9 p. 57; 3.3 b p. 23; section 6 heading p. 77; "12 haftada bir" p. 52) | 0 | 0 |
| S-101 HIT-6 | 5 | 5 (range 36–78 and the four categories) | 0 | 0 |
| S-102 MIDAS | 8 | 8 (grades I–IV with bands; "three months" recall) | 0 | 0 |
| S-103 PedMIDAS | 12 | 12 (0 to 10, 11 to 30, 31 to 50, "Greater than 50", with labels) | 0 | 0 |
| S-104 HADS | 3 | 3 | 0 | 0 |
| S-105 PHQ/GAD-7 manual | 3 | 3 (P.6/9: 0–27, 0–21; P.8/9 developers) | 0 | 0 |
| S-106 NICE TA260 | 4 | 4 (re-treatment every 12 weeks; published datetime 2012-06-27; "Last reviewed: 11 January 2016") | 0 | 0 |
| S-028 NVN module | 5 (Stage 2 fragments: the "Zoeken en selecteren" PICO sentence, its location, "kinderen en volwassenen") | — | 0 | 5 (see Method). Unchanged since v06; verified by reviews 06–11. The Stage 1 OUT-018 fragments of S-028 are counted under "Stage 1 text" below. |
| S-007 IHS cluster guideline | 4 (E-064 "≥ 14 attacks per week on average", section title) | — | 0 | 4 (see Method). Unchanged since v05; verified by reviews 05–12. |
| **Total source fragments** | **361** | **352** (348 by script, 4 by hand) | **0** | **9** |

**The other 91 tagged strings are not source quotes:**
- 58 are Stage 1 text reused by reference; all occur verbatim in Stage 1 v18.
- 15 are English translations (Russian S-033, S-034; Turkish S-035; Dutch S-028). I read each against its original: faithful.
- 14 are search-log query strings or labels; 2 search-log claims were checked in the papers named: PMC6537129 "grade I = 0–5 (minimal or infrequent disability)" and PMC8684566 "little or none (score of 0–5, Grade I)". PMC5796955 prints the same HALT-90 table with "≥20 severe IV".
- 2 are parser artifacts (text between two quotes).

**Metadata.**
- PubMed esummary confirms S-101 (PMID 20819842; Cephalalgia 2011;31(3):357–67; PMC3057423; DOI 10.1177/0333102410379890), S-102 (25902814; J Headache Pain 2015;16:24; PMC4406925), S-104 (12914662; Health Qual Life Outcomes 2003;1:29; PMC183845) and the S-103 developer paper (11739822; Neurology 2001;57(11):2034–9). Authors and DOIs match section 10.
- S-105 PDF metadata: author Kurt Kroenke, created 2010-06-22, modified 2014-04-16, as stated.
- **Newer versions.** A web search found no published ICHD-4 (only "Work in Progress 1", 2024, and committee activity in 2025). NICE CG150 still shows last update 3 June 2025. No newer version that changes an element.

### Value sets and standard references (B)

Re-checked against the downloaded texts, no defect:
- ICHD-3 code labels; 8.2 reference levels (15 for 8.2.3; 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6, 8.2.8), "> 3 months"; 8.2.6 classes and note 2; 8.2.3 comment; A1.1 window day 1 ± 2 (days −2 to +3, no day 0), so `windowDaysBefore = windowDaysAfter = 2`; remission "must exceed three months".
- HIT-6 36–78 and four bands; MIDAS grades I–IV (0–5, 6–10, 11–20, ≥21) and 3-month recall; PedMIDAS four grades with "Severe" > 50; HALT-90 Table 18 (overlap at 20) and recalls; HALT-30 no grading; HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
- The 17 evaluation rules (offsets, anchors, timings, ages, the three `excludes`) and the six named criteria (thresholds and conditions) against their source texts.

### Per-OUT fidelity check (C)

For each requirement I compared every Statement part and constraining Caveat with the realising items, their levels, and the traceability row.

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK (INV-002, INV-003 incl. the v12 conjunct, INV-014, INV-015, INV-037, INV-038, INV-108); the trigger view: R13-03 | 021 | MUST part OK (INV-068, INV-102); SHOULD components: type scope open (R13-01) |
| 002 | OK (INV-008 with `reports`, v12) | 022 | OK (INV-070, INV-103; ISS-03) |
| 003 | OK (INV-011, INV-012, INV-013); the trigger view's dates: R13-03 | 023 | Content OK (INV-071 to INV-075, INV-107); "across the attacks treated with it": R13-01 |
| 004 | OK (INV-014, INV-009) | 024 | OK (INV-077 to INV-079, INV-109) |
| 005 | OK (INV-015; label SHOULD) | 025 | OK (MAY; INV-080) |
| 006 | OK (INV-016, INV-108) | 039 | OK (INV-066, INV-067, INV-104, INV-109) |
| 007 | OK (E-019, INV-010, INV-017, INV-108) | 026 | OK (INV-081, INV-082, INV-100; ISS-06) |
| 008 | OK (MAY) | 027 | OK (INV-026, INV-027) |
| 009 | OK (INV-034 to INV-036) | 028 | OK (INV-040 to INV-043) |
| 010 | Per-period summary OK (INV-018, allTypes); comparison between periods: R13-01 (INV-039) | 029 | OK (INV-028 to INV-030; ISS-09) |
| 011 | OK (INV-019 to INV-021) | 030 | OK (INV-086 with `menstruatesDuring`, INV-087) |
| 012 | OK (INV-022, INV-072, INV-076) | 031 | OK (INV-088, INV-089) |
| 013 | OK (MAY, E-027) | 032 | OK (MAY; INV-090, INV-100); dates vs covered period: R13-03 |
| 014 | OK (INV-023, INV-024 with the v12 time frame of `acuteMedications`; ISS-02) | 033 | OK (INV-083 to INV-085) |
| 015 | OK (INV-025) | 034 | OK (INV-094, INV-104) except the scope of its acute summaries (R13-01) |
| 016 | OK (INV-044 to INV-048; ISS-01) | 035 | OK (INV-095, INV-105; ISS-03) |
| 017 | OK (INV-049 to INV-052, every start of withdrawal; ISS-11) | 036 | (a)–(d) OK (INV-055, INV-096, INV-097; ISS-10); Caveat: R13-02 (INV-098) |
| 018 | OK (INV-053 to INV-059, INV-106) | 037 | OK (INV-091 to INV-093) |
| 019 | OK (INV-060, INV-061; ISS-05) | 038 | OK (INV-099 to INV-101) |
| 020 | OK (INV-062 to INV-065, INV-106); acute effectiveness scope: R13-01 | | |

### Mechanical checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001–E-067), 109 invariants (INV-001–INV-109); none missing, none duplicated. ISS-01–06 and 08–11; ISS-07 only as withdrawn. |
| References | No dangling E- or INV- reference; S references in S-001–S-046 and S-101–S-106, each S-1NN with a row in section 10; OUT references in 001–039. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025); one Realises field per item; every row's E and INV columns equal the union of the Realises fields; no coverage text names an ID outside its row (ranges expanded); all rows "full". |
| `omn` names | 546 declared names; none declared twice (one parser double count of `Item`, caused by the empty brace of E-004, checked by hand). Every attribute selection names a declared attribute or component. Every identifier is declared or bound (the residual parser hits are multi-declaration bindings such as `; x ∈`, `Σ x ∈`, and the free context variable `c` of INV-001, section 2.9). `refs` is defined in section 2.5. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2); every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 32, as the change log states; every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Definedness | Every partial term in the v12 constructs (`referencedValues`, `reports`, INV-003 last conjunct, INV-011, `ageCovered`, `inPopulation`, `childIn`, `menstruatesDuring`, `conditionHolds`, INV-087 `max`/`min`) and in the earlier invariants spot-checked (`÷`, `days`, `first`/`last`, `classOf`, `periodEndFrom`, `publishedRecall`, `scoreRange`, `i.span(2)`) is guarded. |
| Snapshot | `diff -q OUTPUT_MODEL.md history/v12.md`: identical. |
| Scope sweep (F) | Sections 1–8 searched for enter/entry, record, input, captur, logged, stor, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field, "diary information", "diary data". Every hit read in context: exclusion statements, out-of-scope notes ("The value is obtained from diary information; how is out of scope"), verbatim quotes (S-014 "records days affected") and "history". No input entity, storage term, or relation or threshold with an input argument. |
| Thresholds and formulas that are part of the output data | All present and quoted: 8.2 levels and span; A1.1 window; remission duration; instrument ranges, bands and recalls; six criteria and control levels; 17 evaluation offsets; NICE review window. Relations of all derived fields stated (changes, covered-day proportion, outcome proportion, cluster rates, change from baseline instrument result, treatment duration, totals across classes and drugs, 8.2 indicator status). No missing one. |

## Remarks

### R13-01 Coverage gap: the headache-type scope of the intensity, symptom and acute-treatment values required by INV-039, INV-069, INV-071, INV-104 and INV-062 is unconstrained, so these requirements are met by values that cover none, or only part, of the subject's attacks and headaches
- Item(s):
  - INV-039 (intensity in comparisons);
  - INV-069 (the intensity, associated-symptom, most-bothersome-symptom and acute-treatment-summary conjuncts);
  - INV-071 (both conjuncts: per drug and formulation for the selected time range; per drug for the baseline and on-treatment periods);
  - INV-104 (acute-treatment summary conjunct);
  - INV-062 (the `u = acuteTreatmentEffectiveness` branch);
  - optionally, for the same reason: INV-105 (an acute-treatment summary as the treatment effect) and E-055 `acuteResponse`;
  - E-023, E-025, E-026, E-051 Conformance; section 7 rows OUT-010, OUT-020, OUT-021, OUT-023, OUT-034.
- Problem:
  - **Every per-period value has a type scope.** `PeriodValue.typeScope : TypeScope core`, with `variant TypeScope ::= allTypes | ofType ⟨HeadacheType⟩` and `HeadacheType == ICHD3Code` (E-012). No invariant restricts `ofType(h)` to a headache type the subject has or may have, and nothing reads an unscoped requirement as "all types". Fix 10 says so explicitly: "A blanket convention sentence was considered and rejected, because some content invariants (for example INV-069, INV-071) leave the scope open." Review 10 and fix 09 noted, in satisfiability passes only, that "INV-071, INV-069 and INV-104 do not constrain the scope"; no review or fix has checked this against Stage 1.
  - **The base requirements fix the scope; the listed conjuncts do not.**
    - Fixed: INV-018 (intensity) and INV-022 (symptoms, most bothersome symptom) use `reportedPerPeriod(…, allTypes)`; INV-037, INV-068, and the moderate/severe-headache-day and attack conjuncts of INV-069 use `typeScope = allTypes`; the `periodValuesOf(acuteTreatmentSummaries)` branch of INV-062 uses `s.typeScope = allTypes`.
    - Open: INV-039 `∃ m ∈ pc.values ∩ IntensitySummary • m.period = p ∧ m.scale ≠ ∅`; INV-069 `∃ m ∈ v.content ∩ IntensitySummary • m.period = p`, `∃ m ∈ v.content ∩ AssociatedSymptomSummary • m.period = p ∧ m.symptom = s`, `∃ m ∈ v.content ∩ MostBothersomeSymptomItem • m.period = p`, `∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.drug = am.drug ∧ s.period = p`; INV-071 `s.drug = m.drug ∧ s.formulationScope = allFormulations ∧ sameSpan(s.period, c.timeRange)` (and the single-formulation and per-phase conjuncts); INV-104 `∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.drug = m.drug`; INV-062 `∃ s ∈ L.otherValues ∩ AcuteTreatmentSummary • s.period = p ∧ s.drug = am.drug`.
  - **Example 1 (nothing reported).** A subject with migraine only (`headacheTypes = possibleHeadacheTypes` = {1.1 Migraine without aura}); sumatriptan treated 20 attacks in the selected time range. INV-071 is satisfied by a summary of sumatriptan for the time range with `typeScope = ofType(c2)` (tension-type headache): 0 treated attacks, every outcome summary 0 of 0, no attack lines. INV-072 (`#s.sequence = s.treatedAttacks = 0`, all outcome measures present), INV-073 (not cluster headache, so 2 hours), INV-074 and INV-011 all hold. The output reports the effectiveness of sumatriptan across none of the 20 attacks treated with it. The same construction satisfies INV-069, INV-104 and INV-062 for acute treatment, and INV-039 and INV-069 for intensity (an intensity summary of tension-type headache, `otherIntensitySummary`, or a distribution with 0 days at each level, which INV-032 bounds only by the headache days of the same scope).
  - **Example 2 (part reported).** A subject with migraine and tension-type headache (the situation of OUT-029), ibuprofen used for both. The treatment review view (INV-069) and the per-phase summaries next to the response comparison (INV-071) can show ibuprofen's effectiveness for tension-type attacks only, and the intensity of tension-type headache only. The change in the response of migraine attacks after the start of prevention, which OUT-021 and OUT-023 want visible, is then not shown, and the intensity comparison of selected periods (INV-039) is not the headache-intensity summary of OUT-010 that INV-018 gives over all types.
  - **Consequence.** These are SHOULD statement parts whose observable property ("across the attacks treated with it"; "headache intensity"; "for the attacks treated in each of these periods") is not represented, because the required value need not concern the attacks or headaches that the statement names.
- Evidence:
  - Stage 1:
    - OUT-023: "For each acute medication, the diary output SHOULD report, across the attacks treated with it, the outcome measures …"; "When a preventive treatment is started (OUT-018), the output SHOULD allow these per-drug outcomes to be shown separately for the pre-treatment baseline period and for the on-treatment periods of that preventive treatment, so that a change in the response to acute treatment after the start of prevention is visible";
    - OUT-010: "The diary output SHOULD summarise headache intensity per reporting period […] on a stated scale, and allow comparison between periods";
    - OUT-021: "the same view SHOULD also include […] intensity (OUT-010), migraine-associated symptoms and the most bothersome symptom (OUT-012), the effectiveness of acute treatment for the attacks treated in each of these periods (OUT-023)";
    - OUT-020: "the effectiveness of acute treatment in OUT-023"; OUT-034: "current and past treatments with response (OUT-018, OUT-023, OUT-024)".
  - Model: E-012 (`TypeScope`); the predicates quoted above; INV-018, INV-022, INV-062 (`periodValuesOf` branch) for the fixed scope; fix-iter-10.md (sweep of explanatory text, "All types" flag); review-iter-10.md and fix-iter-09.md ("INV-071, INV-069 and INV-104 do not constrain the scope").
- Required change:
  - **(a) Preferred.** Add `typeScope = allTypes` (for summaries: `s.typeScope = allTypes`) to each listed conjunct, as INV-018, INV-022, INV-037, INV-068 and the `periodValuesOf` branch of INV-062 already do for the same kinds of value. Then align the Readings and the Conformance texts of E-023, E-025, E-026 and E-051, and the rows listed.
  - **(b) Alternative.** Where a per-type presentation is intended, require, for every headache type t that the subject has or may have, the value in the scope `scopeFor(ctx, sc, t)` (E-012), so that together the values cover every attack treated with the drug and every headache of the period.
  - Either way, a value scoped to a type that covers none or only part of the attacks or headaches that the statement concerns must not meet the requirement.
  - **Satisfiability.** A value over all types can be shown for any period, and a summary may have 0 treated attacks (INV-072, INV-074). INV-073 then gives such summaries 2 hours unless the subject has only cluster headache (`onlyOfType`); the cluster view keeps its own cluster-scoped 15-minute summaries (INV-088, INV-073). INV-076 applies to every treated-attack line of a subject with migraine whatever the summary's scope (the R02-06 fix is kept). INV-032 bounds a distribution by the headache days of the same scope, which INV-068 shows over all types in the treatment review view.
  - **Oscillation.** No earlier remark or fix argued for an open scope: fix 10 rejected only a blanket prose convention. For INV-062 (watch point 2) the change adds a scope conjunct to the per-drug, per-period requirement of R11-02 without reducing it; the R09-01 deciding values, `#L.evaluated = 1`, the `evaluationResult`/`pretreatmentBaseline` pair and the open kinds are untouched, and acute summaries decide no category.

### R13-02 Coverage gap: the paediatric "supportive information" caveat (INV-098) is triggered only by the first day of a view's covered period, so views that show paediatric outputs of childhood periods but cover a later period escape it
- Item(s): INV-098 (Predicate, Reading, Notes); E-008 Notes ("for the paediatric outputs for the periods in which the subject is a child or adolescent (INV-039, INV-096 to INV-098)"); section 7 row OUT-036.
- Problem:
  - **The v12 predicate.** The fix-12 time-frame sweep changed INV-098 from `ctx.subject.ageGroup = childOrAdolescent ⇒ ∀ v : View • annotated(v, supportiveInformation)` (v11) to `∀ v : View • childOn(ctx, v.covers.start) ⇒ annotated(v, supportiveInformation)`. No review has examined the new trigger.
  - **A view's content is not confined to its covered period.** INV-003 shows in a view every period its items use, wherever it lies. The clinician-facing summary shows the response comparison of every started preventive treatment (INV-104), whose baseline lies before the treatment start (INV-056), whatever period the summary covers. INV-096 places PedMIDAS results in `parts(o)` with no condition on the view or its covered period.
  - **Example.** `adultFrom` = 1 July 2026; as-of date 20 October 2026; topiramate started 1 May 2026 (the subject is 17); previous consultation 1 August 2026.
    - INV-094 and INV-104 require a clinician-facing summary covering 1 August – 20 October 2026, with the topiramate response comparison: a 28-day baseline 3–30 April 2026 (INV-056) and 28-day on-treatment periods. INV-003 places the April period in the summary.
    - The model itself treats this comparison as a paediatric comparison: INV-097 applies to it, because `childIn(ctx, {rc.baseline} ∪ ran rc.onTreatment)` holds (OUT-036 (c)).
    - INV-098 does not apply, because `childOn(ctx, 1 August 2026)` is false. The same holds for the subject's PedMIDAS result of 15 May 2026 (OUT-036 (a), INV-096) shown in this summary or in any view whose covered period begins after 30 June 2026.
  - **The model's own reading is broader than its predicate.** INV-098 Notes: "The paediatric outputs of the OUT-036 Caveat are read as the views of periods that begin while the subject is a child or adolescent"; E-008 Notes: "for the paediatric outputs for the periods in which the subject is a child or adolescent". The summary above is a view of a period (April 2026) that begins while the subject is a child. INV-096 reads the age on the result dates and INV-097 on every compared period, but INV-098 only on the first day of the covered period.
  - **Consequence.** The OUT-036 Caveat, at SHOULD, is not represented for paediatric outputs (a), (c) and (d) of childhood periods that are shown in a view whose covered period begins in adulthood.
- Evidence:
  - Stage 1 OUT-036: Statement (a)–(d); Caveats "[S-034] 'Дневник головной боли не является общепринятым валидизированным методом' […] Paediatric outputs should therefore be presented as supportive information."
  - Model: INV-098 Predicate and Notes; E-008 Notes; INV-096 (`childOn(c, a.date)`), INV-097 (`childIn` over the compared periods); INV-003; INV-056; INV-104; v11 INV-098 (`history/v11.md`).
- Required change:
  - **(a) Preferred.** Extend the antecedent of INV-098 to every view that shows a period that begins, or a result completed, while the subject is a child or adolescent, for example: `∀ v : View • childIn(ctx, v.content ∩ Period) ∨ (∃ r ∈ v.content ∩ InstrumentResult; d ∈ r.completionDate • childOn(ctx, d)) ⇒ annotated(v, supportiveInformation)`. Because INV-003 places `v.covers` in `v.content`, this includes the present antecedent.
  - **(b) Alternative.** Name the paediatric output kinds of OUT-036 in the antecedent: a view that shows a PedMIDAS result completed in childhood or adolescence, school-day or caregiver-impact values of a period that begins then, or a comparison or change to which INV-097 applies.
  - Then align the INV-098 Reading and Notes, the E-008 Notes and row OUT-036.
  - **Satisfiability.** An annotation can be added to any view (INV-007); INV-099 already annotates every view.
  - **Oscillation.** Watch point 6 (v12 time-frame components): the change keeps the dated reading of v12 (age read on dates of the output, `childOn`/`childIn`) and does not restore `ageGroup` or the as-of-date reading of v11.

### R13-03 Formal defect (missing definitional relation): the dates shown by a trigger co-occurrence view are not tied to the period the view covers
- Item(s): E-065 (Definition, Meaning, Notes); INV-011 (fourth conjunct and its Reading); section 7 row OUT-032 (and OUT-001, OUT-003).
- Problem:
  - E-065 declares `factorDates : set Date core` and `attackOnsets : set Date core`. No invariant relates these dates to `v.covers`, the reporting period the view states (E-003). INV-003 places periods in a view, not dates. The attributes appear in no invariant at all.
  - Fix 12 added to INV-011 a completeness indicator for the covered period of a trigger co-occurrence view, and the INV-011 Reading justifies it by "whose summaries concern the diary information of that period". That premise is not formalised.
  - **Admitted output.** A trigger co-occurrence view that covers 1–31 March 2026 (stated with its dates and length, INV-003), with a completeness indicator for March (INV-011), a definition label for attacks (INV-008), the caveats of INV-090 and INV-100, and `attackOnsets` = {5 June 2026, 12 June 2026}, `factorDates` = {4 June 2026}. Every invariant holds.
  - The view states a reporting period that its content does not cover, and the dates it shows are not accompanied by any completeness indicator. Elsewhere the model ties dated content to its period: attack marks lie in cycle lines that overlap the covered period (INV-087), treated-attack lines lie in their summary's period (INV-074), and the markers required in a time-course view are those within its covered period (INV-035).
- Evidence:
  - Stage 1: OUT-001 "Every summary output MUST state the reporting period it covers (start date, end date and length)"; OUT-003 "Each reporting period SHOULD be accompanied by an indicator of how completely the period is covered by diary information"; OUT-032 "The diary output MAY show the co-occurrence over time of attacks with potential trigger factors".
  - Model: E-065 Definition; E-003 `covers` ("the reporting period the view covers"); section 3.6 ("each view summarises diary information for a stated period"); INV-011 fourth conjunct and Reading; INV-003.
- Required change:
  - **(a) Preferred.** Add a definitional invariant for E-065 (Realises OUT-001, OUT-032): `∀ v : TriggerCooccurrenceView • ∀ d ∈ v.factorDates ∪ v.attackOnsets • inPeriod(d, v.covers)`. Then state the relation in the E-065 Notes and row OUT-032.
  - **(b) Alternative.** Require the view to show, with their dates and length, a period that contains its dates, and the completeness indicator of that period (INV-003 and INV-011).
  - **Satisfiability.** The covered period of a trigger view is constrained only by INV-003 and INV-011, so it can be chosen to contain the dates shown; the annotations and the label are unaffected.
  - **Oscillation.** E-065 is not a watch point; INV-011 is only given a premise that its v12 Reading already states.

## Checked and not raised

- **The v12 changes, each well typed and satisfiable, none reversing an earlier fix:**
  - `acuteMedications` as every acute medication used up to the as-of date, with the two INV-001 links to the acute treatment courses: the R12-01 examples now give 12 ≤ 6 + 6 (INV-024) and a triptan indicator with 6 days (INV-044, INV-046).
  - `reports`, `referencedValues`, the INV-008 and INV-011 extensions, and the new INV-003 conjunct (MUST, the OUT-001 reading of "state the reporting period").
  - `menstruationSpans` with `menstruatesDuring` (INV-086, INV-105); `adultFrom`, `aged12From`, `childOn`, `childIn`; `ageCovered` and `inPopulation` on the treatment start (E-041); `withdrawalStart : set Date`; `ihsQ6ChronicAlternative : set Treatment`; `conditionHolds` on the label's treatment through `givenFor`.
- **OUT-002 labels not required for the attacks with an associated symptom, the treated attacks of acute summaries, and headache-free and symptom-free days** (E-011 Notes, fix 12). OUT-002 names four measures; counting a part or the complement of their days or attacks is another measure. A defensible reading; not raised.
- **Headache types as the subject's history and OUT-029.** A subject whose migraine was chronic (1.3) and later episodic (1.1), or who had tension-type headache before chronic migraine (ICHD-3 1.3 note 3: 1.3 "excludes the diagnosis of 2. Tension-type headache"), gets per-type values for both codes for every period (INV-028). The values remain correct (0 days where a type did not occur, E-008), so no output Stage 1 forbids is required. Not raised.
- **`previousConsultation` "on or before the as-of date".** On a consultation day the "period since the previous consultation" of that context would be one day, but `Ctx` contains the context that names the earlier consultation, for which INV-094 requires the summary. Not a defect.
- **INV-105 "treatment effect" by one item.** Settled by the fix-11 quantifier sweep (OUT-035 does not say "for each"); no new evidence. R13-01 lists INV-105 only for the scope of an acute summary, optionally.
- **A view's covered period is not, in general, tied to all its content.** This is by design (baselines of response comparisons in the clinician-facing summary; "the history of previous bouts" in the cluster view; the first cycle line, which may begin before the covered period), and INV-003 states every period used. Only the two consequences in R13-02 and R13-03 need a change. The previous bouts of the cluster view are shown with their own dates (OUT-031 "history of previous bouts"); their lack of a completeness indicator is not raised.
- **HALT-90 total.** [S-014] grades "the total summed score (sum of all five questions)", in which question 5 is a count of lost social events; the total is still a whole number, so `wholeNumberScores` holds, and the unit comment "days" follows the Table 18 heading "Days lost in last 3 months".
- **Type checking.** `refs` is defined in section 2.5 (notation), not in 2.8 or 3.2; section 2.10's "declared" list does not name section 2.5, but the notation section defines it. Not a defect.
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded and pointed to from the elements they affect. Re-verified: 8.2.6 criterion B (p. 124); "simple analgesics" only on p. 139; NICE 1.3.9 and 1.3.39 without a review time point; 1.3.48 and the CG150 population; the [S-034] flowchart (p. 52). No Stage 1 issue is silently worked around; R13-01 to R13-03 are defects of the model, not of Stage 1.
- **Earlier decisions not reopened (no new evidence):** INV-106 at MUST NOT; INV-023 at any granularity; the "> 3 months" readings; the E-041 window readings, timings and `excludes` values (watch point 1); `ruleRuChildren`; INV-050 and E-039 (watch point 5); INV-087 and the lead-in (watch point 4); INV-091 to INV-093 with `concerns`; labels under a criterion that does not apply; the MIDAS label choice and the Grade IV subdivision; the HIT-6 one-month recall; "baseline administration" as any earlier administration; the R10b-01 restriction of INV-054 and the R11-01 (a)/(b) derivation (watch point 3).

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and no item of v12 carries a FROZEN marker.
