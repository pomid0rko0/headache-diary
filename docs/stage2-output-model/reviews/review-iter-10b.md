# Review — iteration 10 (re-check b)
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v09
Date: 2026-10-21

## Summary

This is the first independent re-check of v09, after the main review of iteration 10 (`reviews/review-iter-10.md`) returned NO_REMARKS.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 after OUT-025), and section 5;
- v09 (`OUTPUT_MODEL.md`, byte-identical to `history/v09.md`): every element, every invariant, and sections 7 to 12;
- the oscillation check after iteration 08 and its eight watch points;
- review 09, fix 09 and review 10.

**Earlier decisions.** I searched every earlier review and fix log for the items I examined. FROZEN_ITEMS.md does not exist. I downloaded every source myself and checked every quote by script and by hand. I reached my own verdict.

**Result.**
- **Citations, value sets, scope, traceability and section 8.** All are clean. Every evidence quote is verbatim at its stated location, and every threshold and value set agrees with its source.
- **Two remarks.** Both need a change.
  - **R10b-01 (conformance level).** INV-054 makes it MUST that *every* change is shown with the two values it compares. Stage 1 requires this at MUST only for the changes of the OUT-018 response comparison. For the other changes the model itself admits (R03-05, INV-097), Stage 1 is at most SHOULD (OUT-019, OUT-020, OUT-022). The main review dismissed this point on the premise that "changes are the changes of response comparisons". That premise is contradicted by R03-05, fix 02 and INV-097.
  - **R10b-02 (formal).** The INV-063 Reading and the E-045 Notes paraphrase `scopeFor` with a condition that differs from its predicate. A subject who may have migraine but has no confirmed headache type is admissible (INV-001). For that subject the Reading gives the all-types scope, and the predicate gives `ofType(c1)`.
- **Earlier fixes.** Neither remark reverses an earlier fix or changes a value at an oscillation watch point (details in each remark).

## Verification coverage

**Method**
- **Downloads.** Every source was downloaded with `curl` into the fresh directory `/tmp/r10b-dl`, outside the repository. All 32 downloads returned HTTP 200:
  - the Stage 1 URLs of S-001, S-002, S-005, S-007, S-008, S-010, S-015 (Recommendations and Overview), S-016, S-018, S-028, S-029, S-030, S-033, S-034 and S-035;
  - the Europe PMC full-text XML of S-004, S-011, S-012, S-013, S-014, S-023, S-042, S-043, S-101, S-102 and S-104;
  - the S-103 page, the S-105 PDF and the S-106 pages (overview, section 1, section 2).
- **Extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML and XML had their markup stripped and entities unescaped. ICHD-3 p. 190 and S-034 p. 1 were rendered with `pdftoppm` and read as images.
- **Scripts.** `quotes.py`, `tally.py`, `mech.py`, `names.py` and `html2txt.py`, in the session scratchpad (`r10b/`), run with `python3 -I`.
- **Quote search.** Every double-quoted string on a line that carries an `[S-NNN]` tag, outside the `omn` blocks, was split at `[...]`. That gave 433 fragments. Each fragment was searched in the sources tagged on the same line, in three passes:
  1. whitespace, quotes and dashes normalised;
  2. also line-end hyphens and unmapped glyphs (`≥`, `±`, `+`) removed;
  3. letters and digits only.

  Hits were reported with their PDF page and compared with the stated location.

**Citations**

| Source (URL as listed; HTTP) | Fragments checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (ichd-3.org PDF; 200; 211 pp.) | 59 | 59 (57 by script, 2 by hand). Code labels pp. 8, 9, 12; 8.2–8.2.8 pp. 122–125; the 8.2.3 comment p. 123; Definitions of terms p. 209. The A1.1.1/A1.1.2 window "day 1 ± 2 (i.e. days −2 to +3)" and note 2 were read on the rendered p. 190, because the text layer has no mapping for "±", "−" and "+". | 0 | 0 |
| S-002, S-005, S-042 (Stage 1 quotes reused) | 9 | 9 | 0 | 0 |
| S-007 (UCL manuscript; 200; 39 pp.) | 8 | 8 (pp. 10, 22, 25) | 0 | 0 |
| S-008 IHS 2024 (univaq PDF; 200; 31 pp.) | 27 | 27 (Q2 p. 9, Optimal and Essential; Q6 p. 12, chronic 30 % alternative; Q6 Evidence p. 13: "reduction of ≥5 points for baseline score 11–20 or ii) reduction of ≥30% for baseline score ≥20", so the overlap at 20 is as printed; Q13 heading p. 17) | 0 | 0 |
| S-010 IHS 2025 (univaq PDF; 200; 11 pp.) | 34 | 34 (p. 6: the four control levels, "requires a clear definition of migraine day", "as a proxy of migraine days") | 0 | 0 |
| S-011 EHF 2022 (Europe PMC XML; 200) | 8 | 8 (main-text Background, paragraph 1 "In 2019 …", paragraph 2 "Considering the new knowledge …", as stated) | 0 | 0 |
| S-014 (Europe PMC XML; 200) | 32 | 32 (HALT-90 and HALT-30 recall; "whole days per one or 3 months"; Table 18 with "≥20 Severe IV"; HURT; "Grading is not used by HALT-30") | 0 | 0 |
| S-015 NICE CG150 (200; "Last updated: 03 June 2025") | 35 | 35 (Overview population; 1.3.9, 1.3.24, 1.3.26 with "For full details … (TA260, 2012)", 1.3.27–1.3.29, 1.3.39, 1.3.48; the two headings) | 0 | 0 |
| S-016 SIGN 155 (200; 64 pp.) | 10 | 10 (section 1.2.1, PDF p. 7 = printed p. 1, with "two sentences later" correct; section 4.1, PDF p. 20) | 0 | 0 |
| S-018 AAN/AHS Clinician Summary (200; 12 pp.) | 15 | 15 (p. 1 summary sentence; 14A–14C and 14B with the repeated phrase p. 7; 14H p. 8) | 0 | 0 |
| S-023, S-028, S-029, S-030 (200) | 25 | 25 (the NVN PICO "P: Patiënten (kinderen en volwassenen) …" under "Zoeken en selecteren"; the S-029 module title by a separate download; "hyppigheden eller styrken af migræne", PDF p. 19) | 0 | 0 |
| S-033 Russian adult (200; 92 pp.) | 17 | 17 ("Возрастная категория: взрослые" p. 1; "М – мигрень" p. 4; section 3.3 comments p. 39 "эффективность БТА – минимум через 6 месяцев терапии"; PREEMPT p. 40; "через 3 мес. после ее начала" p. 41; section 7.1 p. 53) | 0 | 0 |
| S-034 Russian paediatric (200; 53 pp.) | 17 | 17 (15 by script, 2 by hand: "Возрастная группа" "дети" read on the rendered title page; p. 17; flowchart p. 52) | 0 | 0 |
| S-035 Turkish protocol (200; 92 pp.) | 28 | 28. Kutu 8 p. 48: "Ölçüt …" is item 2 and "Yeterli süre …" item 7, counted. Section 3.3 b, p. 23. Section 3.6.3.9 p. 57: "3 ayda bir" two sentences before "Hastalar 3 enjeksiyon siklusu sonra …". Heading of section 6, p. 77. | 0 | 0 |
| S-101 HIT-6 (Europe PMC XML; 200) | 5 | 5 (Methods > Data sources: "ranges between 36 and 78"; the four categories) | 0 | 0 |
| S-102 MIDAS (Europe PMC XML; 200) | 8 | 8 (Headache impact on functioning > Migraine-related disability: grades I–IV and bands; three-month recall) | 0 | 0 |
| S-103 PedMIDAS page (200; "© 2026") | 12 | 12 (grading table: 0 to 10, 11 to 30, 31 to 50, Greater than 50, with labels) | 0 | 0 |
| S-104 HADS (Europe PMC XML; 200) | 2 | 2 ("possible scores ranged from 0 to 21 for anxiety and 0 to 21 for depression", in the section "Construction of the Hospital Anxiety And Depression Scale (HADS)") | 0 | 0 |
| S-105 PHQ/GAD-7 manual (200; 9 pp.) | 4 | 4 (P.6/9 under "USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES"; developers sentence P.8/9) | 0 | 0 |
| S-106 NICE TA260 (200) | 5 | 5 (§2.1 "The recommended re-treatment schedule is every 12 weeks …"; published 27 June 2012, last reviewed 11 January 2016; the search-log fragment of §1 by a separate download) | 0 | 0 |
| **Total** | **360** | **360** (354 by script, 6 by hand or by a separate download) | **0** | **0** |

**Other quoted strings and metadata**
- **The other 73 strings on tagged lines** are not source quotes:
  - 15 English translations. All are faithful: the Russian and Turkish ones of E-041 and E-045, including the v09 "Migraine preventive treatment aims to reduce …", and the Dutch PICO.
  - 40 strings of Stage 1 text reused by reference.
  - 17 PubMed and web query strings or model terms.
  - One search-log label, "little or none" (PMC8684566). It is not an evidence quote and was not checked.
- **Metadata.** I checked S-101, S-102 and S-104, and the S-103 developer paper (PMID 11739822), with PubMed esummary. Journal, year, volume, pages, authors, DOI and PMCID agree with section 10.
- **Newer versions.** ICHD-3 is still the current edition: web search found only ICHD-4 "Work in Progress 1" (2024) and committee activity in 2025. NICE CG150 still reads "Last updated: 03 June 2025". No newer version that changes an element was found.

**Per-OUT fidelity check.** For each requirement I compared every Statement part and every constraining Caveat with the items that realise it, the strength of each part with the item's level, and the traceability row.

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK (E-003/E-005 MUST, INV-003, INV-014/015/108, INV-037; Caveat by `lengthDays`) | 021 | OK (INV-068 MUST, INV-069 SHOULD, INV-102) |
| 002 | OK (INV-008) | 022 | OK (INV-070, INV-103; ISS-03) |
| 003 | OK (INV-011, INV-012, INV-013 SHOULD NOT) | 023 | OK (INV-071 to INV-075, INV-107) |
| 004 | OK (INV-014, INV-009) | 024 | OK (INV-077 to INV-079) |
| 005 | OK (INV-015, label SHOULD) | 025 | OK (MAY; INV-080) |
| 006 | OK (INV-016, INV-108) | 039 | OK (INV-066, INV-067, E-055, INV-104) |
| 007 | OK (E-019, INV-010, INV-017, INV-108) | 026 | OK (INV-081, INV-082, INV-100; ISS-06) |
| 008 | OK (MAY) | 027 | OK (INV-026, INV-027) |
| 009 | OK (INV-034 to INV-036) | 028 | OK (INV-040 to INV-043) |
| 010 | OK (INV-018, INV-032, INV-039) | 029 | OK (INV-028 to INV-030; ISS-09) |
| 011 | OK (INV-019 to INV-021) | 030 | OK (INV-086, INV-087) |
| 012 | OK (INV-022, INV-072, INV-076) | 031 | OK (INV-088, INV-089) |
| 013 | OK (MAY, E-027) | 032 | OK (MAY; INV-090) |
| 014 | OK (INV-023, INV-024; ISS-02) | 033 | OK (INV-083 to INV-085) |
| 015 | OK (INV-025) | 034 | OK (INV-094, INV-104; ISS-04) |
| 016 | OK (INV-044 to INV-048; ISS-01) | 035 | OK (INV-095, INV-105; ISS-03) |
| 017 | OK (INV-049 to INV-052; ISS-11) | 036 | OK (INV-055, INV-096 to INV-098; ISS-10) |
| 018 | OK for its own content (INV-053 to INV-059, INV-106); see R10b-01 for INV-054 outside the response comparison | 037 | OK (INV-091 to INV-093) |
| 019 | OK (INV-060, INV-061; ISS-05) | 038 | OK (INV-099 to INV-101) |
| 020 | OK in substance (INV-062 to INV-065); see R10b-02 for the INV-063 Reading | | |

**Mechanical checks**

| Check | Result |
|---|---|
| Headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108); none missing, none duplicated. |
| References | No dangling E- or INV- reference.<br>S references lie in S-001–S-046 and S-101–S-106, and every S-1NN has a row in section 10.<br>OUT references lie in 001–039.<br>ISS headings are 01–06 and 08–11; ISS-07 appears only as withdrawn. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025).<br>Exactly one Realises field per item.<br>Each row equals the union of the Realises fields.<br>No coverage text names an ID outside its row. |
| `omn` names | No name declared twice.<br>Every attribute selection `e.a` names a declared attribute or component.<br>The only undeclared-looking identifier was `OtherItem`, a regex artefact: it is declared in E-004. |
| Levels | Attribute declarations: 172 (core 94, MUST 29, SHOULD 47, MAY 2). Typing rule of section 2.5: 0 violations.<br>Invariants: MUST 19, MUST NOT 2, SHOULD 47, SHOULD NOT 8, definitional 32. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Partial terms | Read in every invariant: every `÷`, `days`, `first`/`last`, `max`/`min`, `s(i)`, `classOf` and `periodEndFrom` is guarded, or covered by INV-001, INV-002 or INV-004. |
| Scope sweep | Searched in sections 1–8: enter, entry, record, input, captur, logged, store, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answers, reminder, algorithm, obtained, calculat, comput, field, "diary data", "diary information".<br>Every hit was read in context. They are exclusion statements, out-of-scope notes, Stage 1 wording, verbatim quotes, or the E-060 lead-in wording, which reviews 05 to 10 settled.<br>No input entity, storage term or derivation from input. Every threshold and formula takes output elements or context properties only. |
| Thresholds and formulas that are part of the output data | All present and quoted:<br>• the ICHD-3 8.2 levels and span, the A1.1 window and the remission duration;<br>• the instrument ranges and bands, the responder thresholds, the control levels and the 17 evaluation offsets;<br>• the percentage change, the covered-day proportion, the outcome proportion, the cluster rates and the change from the baseline instrument result. |

## Remarks

### R10b-01 Infidelity (conformance level): INV-054 requires at MUST that every change is shown with the two values it compares, but Stage 1 requires this at MUST only for the changes of the OUT-018 response comparison
- Item(s): INV-054; E-040 Conformance; section 7 rows OUT-018, OUT-019 and OUT-020.
- Problem:
  - **What INV-054 says.** It quantifies over every `Change`: `∀ ch : Change • ch.reference ∈ viewOf(ch).content ∧ ch.compared ∈ viewOf(ch).content`, at MUST. It realises OUT-018 and OUT-020.
  - **Changes outside response comparisons exist in the model.** The model permits them and constrains them elsewhere:
    - INV-097 (v03, fix of R03-05) requires equal lengths for "the reference and compared periods of every change";
    - E-037 Conformance lists the "change from a reference period" beside the response comparison;
    - R03-05 named "every `Change` (E-040) outside a response comparison … (for example in a scheme-window view)";
    - the iteration-02 fixer noted that no invariant *requires* such a change, which concedes that such changes are *permitted*.
  - **Where such a change can appear.** For example:
    - the post-stop monitoring view (OUT-022, SHOULD), comparing with the original baseline;
    - the scheme-window view (OUT-025, MAY), for month-by-month responder views;
    - the patient-facing overview (OUT-035, SHOULD), showing "treatment effect".
  - **What Stage 1 requires for these changes.** Nothing at MUST:
    - OUT-018's MUST part concerns the comparison "For each preventive treatment … showing both the values of each period and the absolute and percentage change from baseline";
    - OUT-019 sets SHOULD for exactly the absolute values to be shown next to a relative change "wherever" it is shown;
    - OUT-020 sets SHOULD for showing the underlying values with a label.
  - **The level mismatch.** Section 3.3 item 6 allows a constraint to be stronger than a statement part only "where another part of at least that strength directly requires it". No MUST part requires it for these changes. INV-054 also cites OUT-020, a SHOULD requirement, for a MUST invariant.
  - **Example of an output Stage 1 permits that the model excludes at MUST.** An adult with migraine starts erenumab. The output has two views:
    - a patient-facing overview that states "migraine days −4 (−40 %) since the start of erenumab" as a `Change`;
    - a response-comparison view that shows the two monthly migraine-day values.

    Stage 1 asks only at SHOULD (OUT-019) for the values next to the percentage. Under INV-054 the diary is not MUST-conformant (section 3.2).
  - **Why the main review's reason does not hold.** Review 10 did not raise this, on the premise that "In the model, changes are the changes of response comparisons (E-040 Conformance, INV-056)". INV-056 only constrains the changes *of* a response comparison. Nothing restricts `Change` atoms to response comparisons, and INV-097, E-037 and R03-05 above show that the model itself treats other changes as possible. No fixer has declined this point; it was never raised.
- Evidence:
  - Model text:
    - INV-054 Predicate as quoted above; Conformance "MUST"; Realises "OUT-018, OUT-020".
    - E-040 Conformance: "MUST wherever a response comparison shows a change (E-043); shown together with the two values it compares (INV-054)."
    - INV-097 Predicate: `(∀ ch : Change • equalLengths({ch.reference.period, ch.compared.period}))`; Reading: "… and the reference and compared periods of every change".
    - E-037 Conformance: "(response comparison, treatment review view, post-stop monitoring view and change from a reference period)".
    - Section 3.3 item 6 as quoted above.
  - Stage 1 text:
    - OUT-018: "For each preventive treatment, the diary output MUST compare monthly migraine days and monthly headache days […] showing both the values of each period and the absolute and percentage change from baseline."
    - OUT-019 (SHOULD): "Wherever the output shows a relative (percentage) change in migraine or headache days, it SHOULD show next to it the absolute number of migraine days and moderate/severe headache days per month that remain on treatment."
    - OUT-020 (SHOULD): "SHOULD always show the underlying values (OUT-018, OUT-019)".
    - OUT-022 (SHOULD): "compare it with both the on-treatment period and the original pre-treatment baseline".
  - Earlier loop files:
    - `reviews/review-iter-03.md` R03-05 ("every `Change` (E-040) outside a response comparison");
    - `fixes/fix-iter-02.md` item 14 ("No invariant requires such a change: response comparisons are monthly (INV-056), and the scheme windows of the OUT-025 examples are at least 4 weeks").
- Required change (one of):
  - **(a)** Restrict the MUST of INV-054 to the changes of a response comparison, for example `∀ rc : ResponseComparison; ch ∈ rc.changes • ch.reference ∈ viewOf(ch).content ∧ ch.compared ∈ viewOf(ch).content`, realising OUT-018 only. State the same co-presence for every other change in a new SHOULD invariant (a new ID, for example INV-109) that realises OUT-019 and OUT-020. Alternatively, state that other changes are constrained only by INV-060.
  - **(b)** Lower INV-054 to SHOULD for every change, citing OUT-019 and OUT-020, and add the MUST co-presence for response-comparison changes as a conjunct of INV-056 (MUST, OUT-018).
  - **Either way**, update E-040 Conformance, the INV-054 Realises, Reading and Evidence, the section 7 rows OUT-018 to OUT-020, and the level totals in the change log.
  - **Alternative to both:** if the fixer holds that MUST is right for every change, cite the Stage 1 MUST statement part that requires it outside the OUT-018 response comparison.
  - **Oscillation check.** INV-054 is not a watch point, and its level has never changed. The responder-label ties of watch point 5 rest on changes of the label's response comparison, which keep the MUST under both options.

### R10b-02 Formal defect (contradiction between predicate and Reading): the INV-063 Reading and the E-045 Notes state `scopeFor` with a condition that its predicate does not have
- Item(s): INV-063 Reading; E-045 Notes (**Type scope**); `scopeFor` and `onlyOfType` (E-012). Consequential: INV-062 and `attackScope` (E-046).
- Problem:
  - **The predicate.** `onlyOfType(c, allTypes, t)` requires `concerns(c, allTypes, t)`, which requires `c.subject.headacheTypes ≠ ∅`. So `scopeFor(c, sc, t)` gives `allTypes` only when the subject *has* at least one headache type and every type it has or may have falls under t; otherwise it gives `ofType(t)`. The E-012 Meaning states this correctly ("where the subject has a headache type and every headache type it has or may have falls under t").
  - **The paraphrases.** The two paraphrases introduced in v09 drop the first condition and state an explicit "where … and otherwise …" rule:
    - E-045 Notes: "The values of one headache type are those in the scope `scopeFor` (E-012): over all types combined where every headache type the subject has or may have falls under that type, and otherwise in the scope of the type itself."
    - INV-063 Reading: "(over all types combined where every headache type the subject has or may have falls under that type, and otherwise in the scope of that type)".
  - **They disagree in an admissible context.** INV-001 requires only `headacheTypes ⊆ possibleHeadacheTypes`, so `headacheTypes = ∅` is admissible. Take a subject with suspected but unconfirmed migraine: `headacheTypes = ∅`, `possibleHeadacheTypes = {c1}`.
    - The Readings give the all-types scope; the predicate gives `ofType(c1)`.
    - The vacuous case `possibleHeadacheTypes = ∅` differs in the same way.
  - **Consequence.** Take a label under a criterion with an attack-reduction component for migraine attacks (the Turkish Box 8 form, `headacheType = {c1}`).
    - `valueAvailable` holds (`mayHaveType(c, c1)`), so INV-062 requires attack counts in scope `ofType(c1)`, and `attackScope` decides the component only on those.
    - A diary built from the Reading would show all-types counts. INV-062 would then fail, and the component would stay undecided.
    - So the Reading and the predicate prescribe different outputs.
  - **Why the main review's reason does not hold.** Review 10 did not raise this. It gave three reasons, and none applies:
    - the E-045 sentence names `scopeFor`;
    - text outside `omn` blocks is explanatory (section 2.1);
    - review 09 accepted short Readings that point to the formal definition (watch point 1).

    The watch-point-1 Readings ("a later time point of its own") abbreviate a criterion and add no contrary condition. Here, both paraphrases state a complete, explicit condition that yields the opposite scope in an admissible context. PROCESS section 6 makes "Reading" the plain-English reading of the predicate, and PROCESS section 9 lists contradictions between elements or invariants and ambiguous semantics as remarks. The human who decides the Stage 1 issues reads these sentences.
- Evidence:
  - E-012: `pred concerns(c, sc, t) ≙ (∃ h : HeadacheType • sc = ofType(h) ∧ h ⊑ t) ∨ (sc = allTypes ∧ c.subject.headacheTypes ≠ ∅ ∧ ∀ h ∈ c.subject.headacheTypes • h ⊑ t)`; `onlyOfType`; `scopeFor`; and the Meaning quoted above.
  - INV-001: `c.subject.headacheTypes ⊆ c.subject.possibleHeadacheTypes` and no non-emptiness condition.
  - OUT-029: "When the patient has, or may have, more than one headache type". Stage 1 itself distinguishes "has" from "may have".
  - The two paraphrases as quoted (E-045 Notes, line 1276; INV-063 Reading, line 2674 of v09). The v09 change-log entry repeats the same wording ("only where every type the subject has or may have falls under it, and otherwise those of the type itself").
- Required change (one of):
  - **(a) Preferred; no semantic change.** Add the missing condition to both paraphrases, for example "over all types combined where the subject has a headache type and every headache type it has or may have falls under that type, and otherwise in the scope of the type itself".
  - **(b)** If the Readings state the intended rule, change `scopeFor`, or the all-types case of `onlyOfType`, so that it does not require `headacheTypes ≠ ∅`. Then re-check INV-073 and INV-089, which share `onlyOfType`, and the E-012 Meaning.
  - **Optional, under either option:** align the INV-062 Evidence phrase "The values of one headache type are those of the separate presentation of OUT-029". When `scopeFor` gives `allTypes`, these values are not those of the OUT-029 per-type presentation.
  - **Oscillation check.** Option (a) touches only explanatory text of the R09-01 fix. It does not change `#L.evaluated = 1`, the `evaluationResult` / `pretreatmentBaseline` pair, `rc.treatment = L.treatment`, or the open `UnderlyingKind` / `PeriodValueKind` (watch point 5). It reverses nothing.

## Checked and not raised

- **INV-088: a 15-minute summary for every acute medication of a subject with cluster headache.** This includes a drug never used for cluster attacks. With INV-073, such a summary is scoped `ofType(c3_1)` and is satisfiable with 0 treated attacks. It reads OUT-031 "for acute treatments" over all of the subject's acute treatments, which is defensible. It requires no content that contradicts Stage 1.
- **INV-096: `affected` as an alternative to `missed` and `impaired`.** Days on which headache affected school are the days on which school was missed or impaired, shown as one count. Within a domain, INV-033 bounds `missed` and `impaired` by `affected`. Not a narrowing.
- **INV-048 scope.** E-001 defines `claims` as what an element puts to the reader "by its wording or presentation". So a presentation of the indicator as a diagnosis, by its surroundings, is a claim of the indicator. INV-101 covers other elements at SHOULD NOT. Not a gap.
- **INV-060 and INV-061 for compared periods shorter than 28 days.** INV-061 makes a residual burden impossible for a weekly percentage change. The iteration-02 fixer declined this with a justification. I have no new evidence, so I do not raise it.
- **MUST attributes of `CycleLine` when it is shown in the patient-facing overview** (E-060, INV-105). This is the same pattern as R10b-01, but the cycle-line attributes (the ICHD-3 window, `nextWindowDays`) are what a cycle line is. The line's availability is MUST through OUT-030. Its use in the overview has been a watch point unchanged since v02 and v04. Not raised.
- **E-040 `absolute` and `relative` at MUST without a `when` clause.** These attributes are part of what a `Change` is. Content that shows only one form is not an instance of E-040 and falls under `OtherItem` (section 3.7). INV-054, by contrast, is a non-definitional MUST on instances. Not raised.
- **HURT category and recall.** S-014 grades each HURT response and uses 1- or 3-month recall periods. `publishedCategory ⟨Text⟩` and `recallAsPublished ⟨Text⟩` can show these as published, and ISS-06 records the total-score question. Not raised.
- **ISS-02 wording.** "simple analgesics" occurs once in ICHD-3, on p. 139, in the comments on 10.1.1 High-altitude headache. That passage mentions acute mountain sickness in the next sentence. ISS-02 describes it as a passage "on acute mountain sickness, section 10". The point of the issue (the one occurrence is unrelated to 8.2) stands, so this is not a remark.
- **Values re-verified in the sources.**
  - ICHD-3: 8.2 Description "10 or more or 15 or more days/month … for more than three months"; 8.2.1, 8.2.2 and 8.2.3 Descriptions; 8.2.4, 8.2.5, 8.2.6 and 8.2.8 criterion B; 8.2.6 note 2; the A1.1 window (p. 190, image); the remission "must exceed three months" (p. 209); the code labels.
  - IHS 2024: Q6 thresholds, including MIDAS "≥20".
  - IHS 2025: the control levels.
  - HIT-6: 36–78; ≤ 49, 50–55, 56–59, 60–78.
  - MIDAS: grades I–IV with 0–5, 6–10, 11–20 and ≥ 21; 3-month recall.
  - PedMIDAS: 0–10, 11–30, 31–50, > 50.
  - HALT-90: Table 18, including the overlap at 20; HALT-30 is not graded.
  - HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
  - The 17 evaluation rules against their texts: NICE 1.3.27–1.3.29, AAN/AHS 14A and 14B, SIGN 4.1, EHF Q3, IHS Q2, NVN, Russian sections 3.3 and 7.1, the Russian paediatric flowchart, Turkish Kutu 8 and 3.6.3.9.
  - The six named criteria: NICE 1.3.28 and 1.3.29, IHS Q6, IHS 2025, DMKG, Russian 7.1.
- **v09 formal changes.** `scopeFor` picks exactly one scope. `attackScope`, `typeValuesOf`, the `where` clause and `valueAvailable` are well typed and guarded. The `allTypes` ties in `reductionMet` and `reductionDecided` only add conjuncts. INV-073 and INV-089 under `onlyOfType` are consistent with INV-028, INV-071 and INV-088.
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded, and each is pointed to from the elements it affects. Re-verified: 8.2.6 criterion B, NICE 1.3.9 and 1.3.39 without a review time point, 1.3.48 and the CG150 population, and the S-034 flowchart. No Stage 1 issue is silently worked around.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - INV-023 at any granularity;
  - the "> 3 months" readings of INV-045 and INV-089;
  - the window readings and `excludes` values of E-041 (watch points 1 and 8);
  - `ruleRuChildren` (watch point 3);
  - INV-091 to INV-093 with `concerns`;
  - labels under a criterion that does not apply;
  - "history of previous bouts";
  - the E-060 lead-in wording;
  - the HIT-6 recall;
  - the MIDAS label choice.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and no item of v09 carries a FROZEN marker.
