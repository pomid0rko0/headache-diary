# Review — iteration 12
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v11
Date: 2026-10-21

## Summary

This is the main review of iteration 12. It is an independent review of v11. `OUTPUT_MODEL.md` is byte-identical to `history/v11.md`.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 after OUT-025) and section 5;
- v11, every element, every invariant, and sections 7 to 12;
- review 11 and fix 11, including the fix-11 sweeps;
- the oscillation check after iteration 08 and its eight watch points;
- the "Checked and not raised" lists of reviews 01, 03 and 11.

**Earlier decisions.** FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**The R11-01 (a)/(b) decline.** Fix 11 declined these two parts with a derivation through INV-003 and period atoms. I checked the derivation independently, and it holds:
- every item is part of exactly one view (section 2.5);
- INV-003 (MUST) puts every period that an item refers to into that item's view;
- so two items that refer to the same period atom lie in one view;
- the values of a response comparison refer to its own period atoms (INV-056, MUST), and those of a period comparison likewise (INV-038, definitional);
- so the values lie in the comparison's view, and so do its changes, through INV-054.

I do not re-raise R11-01 (a) or (b).

**Result.**
- **Citations.** No defects. 351 source fragments are verbatim at their stated locations: 346 by script, and 5 by hand on rendered pages.
- **Value sets.** No defects. Every threshold, band, range, recall period, code label, evaluation offset and responder threshold agrees with its source.
- **Mechanical checks.** All pass.
- **Scope sweep.** No input, storage or derivation-from-input content.
- **The NVN site (S-028)** was in maintenance during this review, so its fragments could not be re-checked. They are unchanged since v06 and were verified by reviews 06 to 11.
- **Two remarks:**
  - **R12-01 (formal defect: ambiguous semantics, with infidelity as its consequence).** `SubjectProfile.acuteMedications` ("the acute medications … the subject uses") has no stated time frame. The fix-11 log reads it as the current medications ("An acute line whose drug is no longer among `acuteMedications`"). Under that reading, three things go wrong for a period in which a medication the subject no longer uses was taken:
    - INV-023 (MUST) together with INV-024 (definitional) admits only wrong totals;
    - INV-044 and INV-046 force the ICHD-3 8.2.6 indicator to "not reached" where its levels were reached;
    - per-class, per-drug and per-medication outputs of OUT-014, OUT-016 and OUT-023 are no longer required.
  - **R12-02 (coverage gap).** The definition labels of OUT-002 (INV-008) and the completeness indicator of OUT-003 (INV-011) are triggered only by `PeriodValue` counts. Some outputs report migraine days, attacks or headache days as dated items or rates instead, and they escape both requirements:
    - the menstrual-relation view (OUT-030, MUST): its cycle lines and attack marks;
    - the trigger co-occurrence view: its attack onsets;
    - cluster attack rates;
    - the peak-intensity distribution, for the definition label only.

## Verification coverage

### Method

- **Downloads.** All with `curl` into the fresh directory `/tmp/r12-dl`, outside the repository.
  - Stage 1 URLs (HTTP 200): S-001, S-002, S-005, S-007, S-008, S-010, S-015 (Recommendations and Overview pages), S-016, S-018, S-030, S-033 (after two connection resets), S-034 and S-035.
  - Europe PMC full-text XML (HTTP 200): S-011 (PMC9188162), S-014 (PMC6734476), S-023 (PMC9607711), S-042 (PMC12279330), S-101 (PMC3057423), S-102 (PMC4406925) and S-104 (PMC183845). Also, for the E-057 Notes and the search log: PMC6537129 and PMC8684566.
  - Other pages (HTTP 200): the S-103 page; the S-105 PDF; and the S-106 overview, section 1 and section 2 pages.
  - S-028 (NVN): not available.
    - Four attempts returned HTTP 200 with the page "Deze pagina is tijdelijk niet bereikbaar" ("This page is temporarily unavailable").
    - WebFetch reported a 307 redirect to `maintenance.html`.
    - web.archive.org reset the connection twice.
- **Extraction.**
  - PDFs were extracted page by page with `pdftotext -raw` and `-layout`.
  - HTML and XML had their scripts and markup removed and entities unescaped.
  - ICHD-3 p. 190 and the S-034 title page were rendered with `pdftoppm` and read as images.
- **Scripts.** All are in the session scratchpad (`r12/`) and were run with `python3 -I`: `quotes.py`, `nf.py`, `mech.py`, `names.py` and `html2txt.py`.
- **Quote search.**
  - **Fragments.** Every double-quoted string outside the `omn` blocks on a line that carries an `[S-NNN]` tag was split at `[...]`. That gave 442 fragments.
  - **Search.** Each fragment was searched in its preceding tag's source, then in the other sources tagged on the line, in three passes:
    1. NFKC, whitespace, quotes and dashes normalised;
    2. line-end hyphens and unmapped glyphs removed;
    3. letters and digits only.
  - **Locations.** The script recorded the page or pages of every hit, and I compared them with the stated location.

### Citations

| Source | Fragments | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (211 pp.) | 61 | 61: 58 by script, and 3 by hand on rendered p. 190. In the text layer, ± is `\x05`, − is `\x06` and + is "þ".<br>Labels on pp. 8, 9 and 12.<br>8.2 to 8.2.8 on pp. 122–125.<br>The 8.2.3 comment on p. 123.<br>A1.1.1 and A1.1.2 on p. 190.<br>The remission duration on p. 209.<br>"simple analgesics" only on p. 139. | 0 | 0 |
| S-002, S-005, S-007 | 9 | 9: S-007 on pp. 10, 22 and 25; S-002 "50% responder rate" on pp. 10–11 | 0 | 0 |
| S-008 IHS 2024 (31 pp.) | 29 | 29: Q2 on p. 9 (and in the summary, p. 5); Q6 on p. 12; Q6 Evidence on p. 13; the Q13 heading on p. 17 | 0 | 0 |
| S-010 IHS 2025 (11 pp.) | 38 | 38, all on p. 6 (control levels, "requires a clear definition of migraine day", "as a proxy of migraine days") | 0 | 0 |
| S-011, S-014, S-023, S-042 (Europe PMC) | 48 | 48. S-014 includes Table 18 "Grading of HALT-90", "whole days per one or 3 months", HALT-90 and HALT-30 recall, and HURT. | 0 | 0 |
| S-015 NICE CG150 ("Last updated: 03 June 2025") | 35 | 35: 1.3.24, 1.3.26 to 1.3.29, 1.3.9, 1.3.39, 1.3.48 and the population sentence of the Overview | 0 | 0 |
| S-016 SIGN 155, S-018 AAN/AHS | 22 | 22: S-016 on PDF p. 7 (printed p. 1) and PDF p. 20; S-018 on pp. 1, 7 and 8 | 0 | 0 |
| S-028 NVN module | 15 | — | 0 | 15 (see Method). 11 of them are fragments or the title of the Stage 1 OUT-018 quote, which Stage 1 already verified. The 4 new ones are the PICO sentence of "Zoeken en selecteren", its location and "kinderen en volwassenen". They are unchanged since v06, and reviews 06–11 verified them. |
| S-030 | 3 | 3 (PDF p. 19) | 0 | 0 |
| S-033 Russian adult (92 pp.) | 22 | 22: title on p. 1; "М – мигрень" on p. 4; pp. 39, 40, 41 and 53 | 0 | 0 |
| S-034 Russian paediatric (53 pp.) | 13 | 13: 11 by script; "Возрастная группа" and "дети" by hand on the rendered title page. The flowchart is on p. 52, section 2 on p. 17. | 0 | 0 |
| S-035 Turkish protocol (92 pp.) | 28 | 28: Kutu 8 on PDF p. 48; 3.6.3.9 on p. 57; 3.3 b on p. 23; the section 6 heading on p. 77; "12 haftada bir" on p. 52 | 0 | 0 |
| S-101 HIT-6 | 5 | 5 ("Data sources", HIT-6 paragraph: 36–78 and the four categories) | 0 | 0 |
| S-102 MIDAS | 8 | 8 ("Migraine-related disability": the four grades, "with an option of dividing Grade IV into IVA and IVB", and the three-month recall) | 0 | 0 |
| S-103 PedMIDAS page | 12 | 12 (0 to 10, 11 to 30, 31 to 50 and "Greater than 50", with their labels) | 0 | 0 |
| S-104 HADS | 3 | 3 (section "Construction of the HADS", 0–21 per subscale) | 0 | 0 |
| S-105 PHQ/GAD-7 manual | 4 | 4: P.6/9 (0–27 and 0–21) and P.8/9 (developers) | 0 | 0 |
| S-106 NICE TA260 | 4 | 4: §2.1 re-treatment every 12 weeks; "Published 27 June 2012"; "Last reviewed: 11 January 2016" | 0 | 0 |
| **Total** | **366 source fragments** | **351** (346 by script, 5 by hand) | **0** | **15** (S-028, temporarily unreachable) |

**The other 76 tagged strings are not source quotes.**
- 46 are Stage 1 text, reused by reference. All occur in Stage 1 v18. One is a lower-case variant: "where weekly granularity…" in the INV-001 Evidence.
- 14 are English translations. I read them against the originals, and they are faithful: Russian (E-041), Turkish (E-041, E-045) and the S-034 flowchart (ISS-10).
- 16 are search-log query strings or labels. The search-log claims about other developer papers were checked:
  - PMC6537129 reads "grade I = 0–5 (minimal or infrequent disability)" and uses "very severe (≥41)";
  - PMC8684566 reads "little or none (score of 0–5, Grade I)".

**Metadata.**
- **PubMed esummary.** It confirms S-101 (PMID 20819842, Cephalalgia 2011;31(3):357–67, PMC3057423), S-102 (25902814, J Headache Pain 2015;16:24, PMC4406925), S-104 (12914662, Health Qual Life Outcomes 2003;1:29, PMC183845) and the S-103 developer paper (11739822, Neurology 2001;57(11):2034–9). Authors and DOIs match section 10. PubMed spells the S-102 first author "Pavlović".
- **S-105 PDF metadata.** Author Kurt Kroenke; created 2010-06-22; modified 2014-04-16.

**Newer versions.** A web search found no published ICHD-4, only "Work in Progress 1" (2024) and committee activity in 2025. Nothing found supersedes a source in a way that changes an element.

### Value sets and standard references (B)

Re-checked against the downloaded texts:
- **ICHD-3:**
  - the code labels;
  - levels 15 (8.2.3) and 10 (8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6, 8.2.8);
  - "> 3 months";
  - the 8.2.6 classes, and note 2 (8.2.1–8.2.5);
  - the A1.1 window, day 1 ± 2 (days −2 to +3, no day 0), giving `windowDaysBefore = windowDaysAfter = 2`;
  - remission "must exceed three months".
- **Instruments:**
  - HIT-6: 36–78 and the four bands;
  - MIDAS: grades I–IV, 0–5, 6–10, 11–20 and ≥21, with 3-month recall;
  - PedMIDAS: four grades, "Severe" > 50 (`strictLow`);
  - HALT-90: Table 18, including the overlap at 20; HALT-30: 1-month recall, no grading;
  - HADS: 0–21 per subscale; PHQ-9: 0–27; GAD-7: 0–21.
- **The 17 evaluation rules** against their texts: offsets, anchors, timing, populations and the three `excludes` values. The ordering argument for `excludes` holds: TA260 gives re-treatment every 12 weeks, so the end of the second cycle falls at 24 weeks, which lies within NICE 1.3.27's 3–6 months; and Turkish section 3.6.3.9 gives "3 ayda bir" (every 3 months).
- **The six named criteria:**
  - NICE 1.3.28: 50 % (episodic) and 30 % (chronic);
  - NICE 1.3.29: 30 % headache days;
  - IHS Q6: 50 %; the 30 % chronic alternative; MIDAS 5 points for baseline 11–20 and 30 % for baseline ≥20; HIT-6 5 points; and PGIC;
  - DMKG/ÖKSG/SKG: 50 %, 5 points and 30 %;
  - Russian section 7.1: 50 % headache days;
  - the IHS 2025 control levels.

### Per-OUT fidelity check (C)

For each requirement I compared every Statement part and every constraining Caveat with the items that realise it. I also compared the strength of each part with the level of the item, and checked the traceability row.

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK (INV-002, INV-003, INV-014, INV-015, INV-037, INV-038, INV-108) | 021 | OK in structure (INV-068 MUST, INV-069, INV-102). The acute-medication days of a medication no longer used: R12-01 |
| 002 | **Gap** for outputs that report the measures other than as `PeriodValue` counts (R12-02 (a)) | 022 | OK (INV-070, INV-103; ISS-03) |
| 003 | **Gap** for the menstrual-relation and trigger views (R12-02 (b)) | 023 | OK in content (INV-071 to INV-075, INV-107). Per-medication summaries depend on the reading of `acuteMedications` (R12-01) |
| 004 | OK (INV-014, INV-009) | 024 | OK (INV-077 to INV-079, INV-109) |
| 005 | OK (INV-015; label SHOULD) | 025 | OK (MAY; INV-080) |
| 006 | OK (INV-016, INV-108) | 039 | OK (INV-066, INV-067, INV-104, INV-109) |
| 007 | OK (E-019, INV-010, INV-017, INV-108) | 026 | OK (INV-081, INV-082, INV-100; ISS-06) |
| 008 | OK (MAY) | 027 | OK (INV-026, INV-027) |
| 009 | OK (INV-034 to INV-036; markers in the view since v11) | 028 | OK (INV-040 to INV-043) |
| 010 | OK (INV-018, INV-032, INV-039) | 029 | OK (INV-028 to INV-030; ISS-09) |
| 011 | OK (INV-019 to INV-021) | 030 | OK as content (INV-086, INV-087). Its labels and completeness: R12-02 |
| 012 | OK (INV-022, INV-072, INV-076) | 031 | OK (INV-088, INV-089). Attack-rate labels: R12-02 (a) |
| 013 | OK (MAY, E-027) | 032 | OK (MAY, INV-090, INV-100). Labels and completeness: R12-02 |
| 014 | OK only under one reading of `acuteMedications` (R12-01); ISS-02 | 033 | OK (INV-083 to INV-085) |
| 015 | OK (INV-025) | 034 | OK (INV-094 with `chosenPeriod`, INV-104) |
| 016 | OK in levels, span and wording (INV-044 to INV-048; ISS-01). The 8.2.6 status for a past span: R12-01 | 035 | OK (INV-095, INV-105; ISS-03) |
| 017 | OK (INV-049 to INV-052; ISS-11) | 036 | OK (INV-055, INV-096 to INV-098; ISS-10) |
| 018 | OK (INV-053 to INV-059, INV-106) | 037 | OK (INV-091 to INV-093) |
| 019 | OK (INV-060, INV-061; ISS-05) | 038 | OK (INV-099 to INV-101) |
| 020 | OK (INV-062 to INV-065, INV-106; the R11-02 change is per drug and per period, as asked) | | |

### Mechanical checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001–E-067) and 109 invariants (INV-001–INV-109): none missing, none duplicated. |
| References | No dangling E- or INV- reference.<br>S references lie in S-001–S-046 and S-101–S-106.<br>OUT references lie in 001–039.<br>ISS headings are 01–06 and 08–11; ISS-07 appears only as withdrawn. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025).<br>Exactly one Realises field per item.<br>Every row's E and INV columns equal the union of the Realises fields.<br>No coverage text names an ID outside its row. |
| `omn` names | No name declared twice. Every identifier is declared, or bound by a quantifier, comprehension, `let` or parameter list.<br>Every attribute selection names a declared attribute or component. The two parser hits, `combines` and `index` of E-033, are declared on a line with a nested brace. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), as the change log states.<br>Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 32, as the change log states.<br>Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Snapshot | `diff -q OUTPUT_MODEL.md history/v11.md`: identical. |
| Scope sweep (F) | Sections 1–8 were searched for: enter, entry, record, input, captur, logged, stor, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field, "diary information", "diary data".<br>Every hit was read in context. The hits are exclusion statements, out-of-scope notes, verbatim quotes (for example the S-014 HALT-30 recall sentence) and explanatory text.<br>No input entity, no storage term, and no relation or threshold with an input argument. |
| Thresholds and formulas that are part of the output data | All present and quoted:<br>• the 8.2 levels and span;<br>• the A1.1 window;<br>• the remission duration;<br>• the instrument ranges, bands and recalls;<br>• the six criteria and the control levels;<br>• the 17 evaluation offsets;<br>• the NICE review window.<br>The relations of all derived fields are stated: percentage and absolute change, covered-day proportion, outcome proportion, cluster rates, change from the baseline instrument result, treatment duration, totals across classes and drugs, and the 8.2 indicator status. No missing one was found. |

## Remarks

### R12-01 Formal defect (ambiguous semantics), with infidelity as its consequence: the time frame of `SubjectProfile.acuteMedications` is not stated, and under the reading the fix-11 log uses, invariants exclude correct outputs and narrow OUT-014, OUT-016 and OUT-023 for past periods
- Item(s):
  - E-008 (`acuteMedications` and its comment, Meaning);
  - INV-024 (the two upper-bound conjuncts);
  - INV-023, INV-028, INV-068 and INV-104 (per-class and per-drug days);
  - INV-044, and INV-046 with `classUseExcluded` (E-032);
  - INV-062, INV-069, INV-071 and INV-088 (per-medication summaries);
  - E-029 and E-032 Conformance ("the subject's acute medications");
  - section 7 rows OUT-014, OUT-016, OUT-021 and OUT-023.
- Problem:
  - **The declaration.** E-008 declares `acuteMedications : set AcuteMedication -- the acute medications (drug and formulation) the subject uses`. It does not say whether this means the medications in use as of the as-of date, or every acute medication the subject has used.
  - **A second set exists.** The model separately has `acuteTreatments`, acute treatment courses with start and stop events (E-008, E-055). Nothing ties the two sets together.
  - **The model's own fixer reads it as current.** The fix-11 log (satisfiability pass for INV-109) says: "An acute line whose drug is no longer among `acuteMedications` can refer to a summary with 0 attacks." So a medication that the subject stopped is taken to leave `acuteMedications`.
  - **The invariants quantify over this set for every period, past periods included.** Under the current-medication reading:
    - **(i) INV-024 (definitional) contradicts INV-023 (MUST) for correct values.**
      - **Example.** An adult with migraine; as-of date 20 October 2026; time range January to September 2026 in calendar months. Rizatriptan was used from November 2025 to 30 April 2026 and then stopped; since then only ibuprofen. In January 2026 the subject took rizatriptan on 6 days and ibuprofen on 6 other days. `acuteMedications` = {ibuprofen}.
      - **What INV-023 requires.** For January, the total, the non-opioid-analgesic class and ibuprofen, with the correct values 12, 6 and 6.
      - **What INV-024 then demands.** Its conjunct `let K == {m ∈ ctx.subject.acuteMedications • classOf(m.drug)} • (∀ k ∈ K • … ≠ ∅) ⇒ ∀ t ∈ daysOf(v, acuteMedicationDays(allAcuteMedication), p, sc) • t ≤ Σ k ∈ K • …` requires 12 ≤ 6.
      - **Result.** The only outputs that satisfy INV-023 and INV-024 show a wrong January total. The class-to-drug conjunct fails in the same way for a class whose old drug is no longer listed. (Example: a switch from rizatriptan to sumatriptan gives triptans 6 ≤ sumatriptan 0.)
      - INV-023 never requires the triptan class or rizatriptan days for January at all, although OUT-014 asks for the breakdown "by drug class [...] and by individual drug, together with the total across classes".
    - **(ii) The 8.2.6 indicator is forced to "not reached" where ICHD-3's levels were reached.**
      - Same subject, span January to April 2026: rizatriptan on 6 days and ibuprofen on 6 other days in each month, so 12 combined days per month and no class at its own level.
      - ICHD-3 8.2.6 criterion B is met ("any combination of ergotamine, triptans, non-opioid analgesics and/or opioids […] on a total of ≥10 days/month for >3 months without overuse of any single drug or drug class alone").
      - INV-044 requires indicators only for the classes of `acuteMedications` (here only non-opioid analgesics) and for combined use. So no triptan indicator is required.
      - `classUseExcluded(i, triptans)` then holds: no triptan indicator shows days, and "the subject uses no medication of class k".
      - The first conjunct of INV-046 needs two non-excluded classes of 8.2.6 for "reached", so the combined indicator for April 2026 must read "not reached".
      - OUT-016 (MUST) asks the output to indicate "whether acute medication use reached the levels of regular use that ICHD-3 code 8.2 and its subtypes 8.2.1–8.2.6 and 8.2.8 [S-001] describe".
    - **(iii) Per-medication outputs of OUT-023 and OUT-021 are not required for a medication no longer used.** This affects INV-071 (summaries per medication and per formulation, and for the baseline and on-treatment periods of each preventive treatment), INV-069 (treatment review view), INV-062 and INV-088.
      - This is exactly the case of a switch of acute medication around the start of a preventive treatment, where OUT-023 wants "a change in the response to acute treatment after the start of prevention" to be visible.
      - OUT-023 states "For each acute medication".
  - **The other reading.** Under the reading "every acute medication (drug and formulation) that the subject has used, up to the as-of date", all of these invariants are correct. In example (i), K = {triptans, non-opioid analgesics} and 12 ≤ 6 + 6. In example (ii), a triptan indicator is required and shows 6 days in each month.
  - **So the model's meaning depends on an unstated time frame.** The natural present-tense reading, which the model's own fixer uses, makes a MUST invariant satisfiable only with wrong values, and narrows MUST and SHOULD statement parts.
- Evidence:
  - Model:
    - E-008, `acuteMedications : set AcuteMedication -- the acute medications (drug and formulation) the subject uses`;
    - INV-024 predicate (the `let K` and `let D` conjuncts) and Reading ("when every class of the subject's acute medications is shown, the total does not exceed the sum of the class values");
    - INV-023 predicate (`{m ∈ c.subject.acuteMedications • …}`);
    - INV-044 predicate (`{m ∈ c.subject.acuteMedications • ofClassUse(classOf(m.drug))}`);
    - E-032, `classUseExcluded` (`¬ ∃ m ∈ ctx(outputOf(i)).subject.acuteMedications • classOf(m.drug) = k`), and INV-046;
    - INV-071 (`∀ c ∈ Ctx; m ∈ c.subject.acuteMedications`).
  - Fix log: fixes/fix-iter-11.md, section 4 (Satisfiability pass), the INV-078/INV-109 item: "An acute line whose drug is no longer among `acuteMedications` can refer to a summary with 0 attacks."
  - Stage 1:
    - OUT-014: "the number of days with acute (symptomatic) headache medication, broken down by drug class [...] and by individual drug, together with the total across classes";
    - OUT-016: "per reporting period, per acute medication class and, for ICHD-3 subtype 8.2.6, for the combined use of acute medication across classes";
    - OUT-023: "For each acute medication, the diary output SHOULD report, across the attacks treated with it, …"; "so that a change in the response to acute treatment after the start of prevention is visible".
  - Source: [S-001] 8.2.6 criterion B, quoted in E-028 and verified (p. 124).
  - Earlier loop files: no review or fix discusses the time frame of `acuteMedications`. INV-024, INV-044 and INV-046 are not watch points.
- Required change:
  - **(a) Preferred.** State in E-008 (the comment of `acuteMedications` and the Meaning) that the set holds every acute medication, drug and formulation, that the subject has used up to the as-of date, and that it keeps a medication after its use has stopped.
    - Optionally, add to INV-001 that the drug of every acute treatment course is the drug of one of these medications.
    - Then align the wording "the subject's acute medications" in E-029, E-032 and E-051, and the Readings of INV-023, INV-024, INV-044, INV-046 and INV-071.
    - No predicate needs to change.
  - **(b) Alternative.** If a current-medication set is intended, add a separate context component for the acute medications used up to the as-of date, and use it in place of `acuteMedications` wherever per-period content is required or bounded: INV-023, INV-024, INV-028, INV-044, `classUseExcluded`/INV-046, INV-062, INV-068, INV-069, INV-071, INV-072, INV-088 and INV-104.
  - **Satisfiability.** Under (a), every per-drug requirement can show 0 days, or a summary with 0 treated attacks, for a medication not used in the period (INV-072, INV-074). The bounds of INV-024 then hold for correct values.
  - **Oscillation.** None of the affected items is a watch point. E-041 applicability (watch point 2) and the responder machinery (watch point 5) are untouched.

### R12-02 Coverage gap: the definition labels of OUT-002 and the completeness indicator of OUT-003 are required only where a view shows `PeriodValue` counts; outputs that report migraine days, attacks or headache days as cycle lines, attack marks, attack onsets, rates or a distribution are not covered
- Item(s):
  - INV-008 (with `isMeasure`, E-011) and INV-011;
  - E-011 and E-013 Conformance;
  - E-060, E-061 (menstrual-relation view, cycle lines, attack marks);
  - E-064 (cluster attack rate);
  - E-065 (trigger co-occurrence view);
  - E-023 (`peakIntensityDistribution`);
  - section 7 rows OUT-002, OUT-003, OUT-030 and OUT-032.
- Problem:
  - **What triggers INV-008.**
    - INV-008 reads `∀ v : View; lm : LabelledMeasure • (∃ m ∈ v.content ∩ PeriodValue • isMeasure(m, lm)) ⇒ ∃ l ∈ v.content ∩ DefinitionLabel • l.measure = lm`.
    - `isMeasure` holds only for the day counts `HeadacheDays`, `MigraineDays` and `ModerateSevereHeadacheDays`, and for `AttackCount`.
  - **What triggers INV-011.** INV-011 asks for a completeness indicator only for the period of a `PeriodValue` that a view shows.
  - **Elements that escape both.** The model reports the same measures in other forms:
    - **The menstrual-relation view (E-060, MUST by INV-086).** It shows migraine days as dates (`CycleLine.migraineDays : set Date MUST`) and migraine attacks as attack marks (`CycleLine.attacks`, E-061).
      - INV-086 and INV-087 require no `PeriodValue` in this view.
      - A fully conformant output can therefore consist of a menstrual-relation view of, say, 1 July to 30 September 2026, with three cycle lines, 5 migraine days and 4 attack marks, and nothing else.
      - INV-008 and INV-011 are then satisfied vacuously. The reader cannot tell which definition of a migraine day selected the 5 days. Different definitions select different days (OUT-002 Rationale), and so different days fall inside the A1.1 window. Nor can the reader tell whether a cycle that shows no migraine day had diary days missing.
    - **The trigger co-occurrence view (E-065).** It shows attacks as attack onsets (`attackOnsets : set Date`), and no `PeriodValue` is required in it.
    - **The cluster view (E-062).** It shows attacks per day and per week (`ClusterAttackRate`, E-064). These are `PeriodValue`s, so completeness is required, but they are not `AttackCount`, and the view is not required to show an attack count (INV-089 relates the rate to one only "where the view shows one"). So no attack definition label is required.
    - **The intensity summary (E-023).** In its `peakIntensityDistribution` form it reports headache days by peak intensity level, which can be shown without a `HeadacheDays` count. No label is then required, although the label that INV-009 constrains (ICHD-3 headache days, MUST) is exactly the one this distribution depends on.
  - **What Stage 1 asks.**
    - OUT-002 (SHOULD) applies to "Outputs that report migraine days, headache days, moderate/severe headache days or attacks", in whatever form.
    - OUT-003 (SHOULD) applies to "Each reporting period", and every view is a summary output with a stated reporting period (section 3.6). The menstrual-relation view and the trigger view summarise diary information over their covered period.
    - The model's own text assumes broader coverage than its predicates give:
      - the E-045 Notes say that INV-011 shows completeness "with every period";
      - the OUT-002 row says "full — a definition label for each defined measure shown in a view".
  - **Consequence.** Two observable properties of OUT-002 and OUT-003 are missing for these outputs. One of them is the MUST view of OUT-030, whose subject matter, migraine attacks and migraine days in relation to menstruation, depends directly on the migraine-day and attack definitions and on diary coverage.
- Evidence:
  - Stage 1:
    - OUT-002: "Outputs that report migraine days, headache days, moderate/severe headache days or attacks SHOULD state which published definition of each measure they follow"; Rationale: "There is no single universally adopted definition of a migraine day; different definitions give different numbers. A reader can compare a diary value with guideline or trial values only if the definition used is visible";
    - OUT-003: "Each reporting period SHOULD be accompanied by an indicator of how completely the period is covered by diary information [...], shown next to the summary measures so that readers can judge their reliability"; Rationale: "Missing diary days bias frequency measures";
    - OUT-030: "the diary output MUST be able to show migraine attacks and migraine days in relation to the days of menstruation across consecutive cycles";
    - OUT-031: "attacks per day and per week during active periods";
    - OUT-032: "the co-occurrence over time of attacks with potential trigger factors".
  - Source, on why the definition matters for OUT-030: [S-001] A1.1.1 criterion A, "Attacks, in a menstruating woman, fulfilling criteria for 1.1 Migraine without aura and criterion B below" (p. 190; read on the rendered page).
  - Model:
    - INV-008 and INV-011 predicates as quoted;
    - `isMeasure` (E-011);
    - E-060 `migraineDays : set Date MUST` and `attacks : set →AttackMark MUST`;
    - E-065 `attackOnsets : set Date core`;
    - E-064 and INV-089 ("where the same view shows the attack count");
    - E-023 `peakIntensityDistribution ⟨set1 LevelDays⟩ -- headache days by peak intensity level`;
    - section 3.6;
    - E-045 Notes ("Completeness indicators (E-013), which INV-011 shows with every period");
    - section 7 row OUT-002.
  - Earlier loop files: no review or fix has discussed definition labels or completeness for these views. INV-008 and INV-011 are not watch points.
- Required change:
  - **(a) OUT-002.** Extend the antecedent of INV-008 (SHOULD) to every view that reports one of the four measures in any form the model shows it. For example, replace `isMeasure(m, lm)` by a predicate `reports(v, lm)` that also holds for:
    - `migraineDaysMeasure` when the view shows a cycle line;
    - `attacksMeasure` when it shows an attack mark, a cluster attack rate, or is a trigger co-occurrence view;
    - `headacheDaysMeasure` when it shows an intensity summary in its peak-intensity-distribution form.

    INV-009 and INV-010 then constrain these labels as they stand.
  - **(b) OUT-003.** Extend INV-011 (SHOULD) so that a menstrual-relation view and a trigger co-occurrence view show a completeness indicator for the period they cover: `∃ ci ∈ v.content ∩ CompletenessIndicator • ci.period = v.covers`.
    - Alternatively, apply INV-011 to every view whose content summarises diary information over its covered period.
    - Do not require it for views without diary-based content, for example the treatment history view.
  - **Then align:**
    - the Conformance fields of E-011, E-013, E-060, E-064 and E-065;
    - the Readings of INV-008 and INV-011;
    - the E-045 Notes;
    - section 7 rows OUT-002, OUT-003, OUT-030 and OUT-032.
  - **Satisfiability.** A definition label, and a completeness indicator for the covered period (`typeScope = allTypes`, INV-012), can be added to any view. INV-003 already shows the covered period in the view.
  - **Oscillation.** E-060, E-061 and INV-087 (watch point 7) need no change, because the label and the indicator are items of the view, not of the cycle lines. INV-104 and INV-105 are unchanged; they already show day counts that trigger both invariants.

## Checked and not raised

- **Fix 11 changes (v11).** Each is well typed, matches its Reading, and follows the Stage 1 part it cites:
  - INV-035 places the markers in the view;
  - INV-072 places the outcome summaries and the lines in the view, and requires every formulation for a summary of all formulations;
  - INV-062 requires per-drug and per-period acute summaries, and the evaluation result of each instrument;
  - `chosenPeriod` (E-007, INV-001, INV-094);
  - INV-049 covers the running follow-up;
  - INV-078 places the history groups and lines in the view;
  - INV-109 requires every dose change, and the response summary and adherence with the line;
  - INV-083 requires both HADS subscales.

  None of these changes reverses an earlier fix or changes a value at a watch point.
- **The R11-01 (a)/(b) derivation** (fix 11). It is verified as stated in the Summary. The derived property in the INV-003 Notes follows from section 2.5 and INV-003.
- **MIDAS grade IV subdivision.** [S-102] states "with an option of dividing Grade IV into IVA and IVB", and a developer-co-authored paper uses "very severe (≥41)".
  - INV-082 admits only the four tabulated bands as the MIDAS category.
  - Showing grade IV is the developers' grading. The optional subdivision can be shown as further content (`OtherItem`, section 3.7).
  - So no output that Stage 1 asks for is excluded. Not raised. The settled MIDAS label choice (review 01) is not reopened.
- **The week convention in `isWeekSpan`** ("under the week convention of the output"). It is a fixed given function, so the consistent reading is one week convention for the diary, which INV-001 and the outputs share. Stage 1 fixes no convention and requires no mix. Not a defect under that reading. Not raised.
- **E-039 `reviewWindow` SHOULD without `when`, against INV-050's conditional conjunct.** The attribute is stronger than the conjunct, but the two are consistent. A view of a running follow-up can show the coming review window, since no invariant confines a period to the covered period. Not raised.
- **E-062 `remissions` non-empty at SHOULD for chronic cluster headache.** Fix 02 (item 14) settled this: whether a remission exists depends on diary information. No new evidence. Not raised.
- **HALT-90 total score and whole numbers.** [S-014] says that question 5 "gives rise to a simple count for which the unit is not whole days" and is included in the total summed score. The total is still a sum of counts, so `wholeNumberScores` holds. Table 18 labels the score "Days lost in last 3 months", which matches the unit comment of E-058.
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded, and each is pointed to from the elements it affects. Re-verified:
  - 8.2.6 criterion B;
  - "simple analgesics" only on p. 139;
  - NICE 1.3.9 and 1.3.39 without a review time point;
  - 1.3.48 and the CG150 population;
  - the [S-034] flowchart on p. 52.

  No Stage 1 issue is silently worked around. R12-01 and R12-02 are defects of the model, not of Stage 1.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - INV-023 at any granularity (R12-01 concerns its medication set, not its granularity);
  - the "> 3 months" readings of INV-045 and INV-089;
  - the E-041 window readings and `excludes` values (watch points 1 and 8);
  - `ruleRuChildren` (watch point 3);
  - INV-050 and E-039 (watch point 4);
  - INV-091 to INV-093 with `concerns`;
  - labels under a criterion that does not apply;
  - "history of previous bouts" and the OUT-031 end-of-bout Caveat;
  - the E-060 lead-in wording;
  - the HIT-6 one-month recall;
  - the MIDAS label choice;
  - "baseline administration" as any earlier administration;
  - INV-060 with INV-061 for compared periods shorter than 28 days;
  - a response comparison right after the treatment start;
  - the context as subject properties;
  - the treatment-history co-presence ruling of review 03, which fix 11 superseded in the direction review 03 left open.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and no item of v11 carries a FROZEN marker.
