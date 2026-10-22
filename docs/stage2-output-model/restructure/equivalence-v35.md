# Equivalence check — v34 -> v35 (iteration 35, step 3)
VERDICT: DEFECTS
DEFECT_COUNT: 5
Date: 2026-10-22

## Summary

v35 (`OUTPUT_MODEL.md` = `history/v35.md`, with `RATIONALE.md` = `history/v35-rationale.md`) is v34 plus the listed intended changes CHG-01 to CHG-07 and CHG-R1, as far as the formal content goes, with one exception: a syntax error in E-045 (EQ35-01).

- **Accounting.** Every v34 element and invariant is accounted for, every new ID is one that the plan and the fix log list, and every Stage 1 issue and source is still present.
- **Generic rules and moves.** I unfolded every generic invariant (INV-118 to INV-125), placement marker (rule W2), source data table and reformulated invariant. Each one is equivalent to the v34 text it replaces, apart from the listed CHGs. Levels and traceability are unchanged.
- **Watch points.** No watch point is reversed.
- **Remark R35-01** is resolved as the fix log states. My own enumeration confirms the remaining exception and nothing more.

The other four defects are in text and links, not in formal content:

- EQ35-02: a truncated source URL in 11 `RATIONALE.md` quote entries.
- EQ35-03: two prose places that CHG-03 made false.
- EQ35-04: references in moved or kept prose that still name the v34 home of moved conjuncts. Two of them now contradict the model: a level that CHG-R1 changed, and an ask that now sits in E-049.
- EQ35-05: the Reading of INV-118 claims more than its predicate.

## Method and coverage

All checks were run by my own scripts, not by the author's or the architect's. They read `history/v34.md`, `history/v35.md`, `history/v35-rationale.md`, the plan, the fix log and Stage 1. The scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/eq-v35/`, which is outside the repository. All were run with `python3 -I`.

| Script | What it checks | Result |
|---|---|---|
| `parse.py`, `accounting.py`, `mapcmp.py` | split both versions into items and fields; ID accounting; model section 9 against the fix-log and plan mappings | E 67/67 kept, none new; INV 117 → 79 kept + 38 withdrawn as merged (each with a section 9 row); new INV exactly INV-118 to INV-125; ISS-01 to ISS-12 (ISS-07 withdrawn) kept, ISS-13 new; OC-01 to OC-45; C1 14, C2 9, C3 12; 94 SD rows in 13 tables; section 10 (sources) byte-identical; plan and fix-log mappings agree (8 rows differ only in explanatory wording) |
| `formal.py` | `omn` blocks per item, v34 against v35, with diffs | byte-identical: 37 elements, 50 invariants; changed: 30 elements, 29 invariants. I read all 59 diffs against plan section 8 and the fix log: 58 are exactly the stated edits (D-6, D-7 and the plan 3.4 comment deletions included); E-045 is not (EQ35-01) |
| `secs.py` | sections 1–3, blocks outside items | section 1 identical; blocks of 2.8 and 3.4 identical; 3.2 block changed only in comments, with the conditions as normative sentences (CA-11), same content; new `enum Level`, `CatalogueRow` block |
| `levels.py` | conformance level and scope of every invariant | v34 {def 40, MUST 19, SHOULD 48, SHOULD NOT 8, MUST NOT 2}; withdrawn {MUST 8, SHOULD 15, SHOULD NOT 7, MUST NOT 2, def 6}; v35 {def 38, MUST 11, SHOULD 33, SHOULD NOT 1, level-indexed 4}. No kept invariant changed level. Every merged case, marker and moved conjunct keeps its v34 level, except the two CHG-R1 conjuncts (MUST → definitional) |
| `sdcheck.py` | source data tables: rebuild the v34 OMN text from the v35 cells (forms V, M, C, D) and compare it, white space aside, with the v34 axioms and constants | 13 tables, 94 rows, 383 formal values; 0 mismatches. `AcuteDrugClass` has exactly 6 constants (so the v34 `∀ k ≠ …` form equals the 6 SD-CLS rows); every component of `EvaluationRule`, `ResponderCriterion` and `GradeBand` has a column |
| `eq_c1.py` | INV-118 with case table C1 (cells as written) against v34 INV-014–019, 022, 023, 025, 026, 028, 029, 108, per level, on random repertoires (series per view, granularity, tiling, kinds per type scope, `provides`); with a mutation test | 100,000 repertoires: MUST 0, SHOULD 0 mismatches; mutation (C1-07 and C1-14 under one `∃ g`) detected 40 times |
| `eq_c2c3.py` (+ a sparse-claims variant) | INV-119 with C2 and INV-120 with C3 against the 9 + 8 replaced invariants, per level, with annotations constrained by W2 / INV-007 | 2 × 200,000 outputs: MUST NOT 0; SHOULD NOT 102 + 827 differences, all an annotation that carries `standAloneEfficacyMeasure` or `soleIndicatorOfIndividualBenefit` (CHG-07), 0 unexplained; required annotations 0 mismatches at MUST and SHOULD |
| `eq_small.py` | exhaustive small domains | INV-064 with SD-CL: 18,724 cases, 0; INV-073 with SD-ET: 4, 0; INV-085 with SD-SR: 964, 0; E-049 `when` merged with the INV-070 ask: 32, 0; INV-079 role conjuncts against INV-123 under INV-001 disjointness: 6, 0; INV-125 with SD-DF against INV-009/010 per level: 1,024, 0 |
| `eq_nest.py` | INV-122 (`nestedIn`, first conjunct) against the removed bounds of INV-024, 031, 033; INV-121 (`daysWithin`) against INV-005 and the removed conjuncts of INV-012, 032, 033 | 30,000 views (36 nested pairs): 0; 50,000 atoms: 0 |
| `r3501_check.py` | R35-01: INV-087 (per line, lead-in, marks, MRV sequence) with INV-124's first conjunct, on random one-view and two-view outputs | 2 × 400,000 trials. Admitted by v35: 28,895 one-view and 775 two-view outputs. Wrong marks on a line that has ended: 0. Wrong marks on a line that has not ended, against the day 1s up to its last day: 0. v34 admitted 34,219 and 2,800, of which 756 and 126 had a wrong mark |
| `witness.py` | satisfiability witness: one context (migraine, TTH and cluster history; triptan and NSAID; a preventive course with a stated start) and five views; INV-118 on a two-context repertoire | holds: INV-118 (must, should), INV-119, INV-120, INV-121–INV-125, INV-087, INV-089 (phases), INV-111 (with CHG-06), INV-060/061, INV-031. Negative controls: an overlapping cycle line and a bout that overlaps a remission in another view are both rejected by INV-124 |
| `quotes.py`, `urls.py` | quote preservation, Evidence pointers, Source lines | 588 quote occurrences (451 distinct) on v34 lines with an [S-] tag: all present verbatim except 3 control-level label names (not source quotes; the [S-010] quotes are in E-046/Q01–Q05). Of all 906 quoted strings, 23 are absent: Stage 1 fragments in the Evidence of merged invariants (Stage 1 quotes are cited, not repeated) and those label names. 70 structured `[S] "quote" (location)[. Translation]` bullets: all found with the same source, location, quote and translation. 114 model Evidence pointers and 362 entry IDs resolve, each Q entry carrying its source. 153 Source lines: 142 match the source tables, 11 do not (EQ35-02) |
| `trace.py` | Realises mapped through section 9 and moved conjuncts; section 7; catalogue column Realises | 384 v34 (item, OUT) pairs, 0 lost. Of 391 v35 pairs, 1 has no v34 source: INV-120/OUT-008 through C3-02, which is MAY and imposes nothing. Realises unchanged for all 146 kept items. Section 7: 39 rows, and the Elements and Invariants columns equal the union of Realises. Every catalogue Realises OUT is realised by an item named in its row |
| `withdrawn_refs.py`, `edited_refs.py`, `moved_claims.py`, `stale.py` | prose and RATIONALE references to withdrawn IDs and to kept invariants that lost conjuncts | references to withdrawn IDs are all provenance ("v34 INV-…", C-row origins, "Replaces"). Stale attributions are listed in EQ35-04 |
| other | bracket balance of all `omn` blocks and 567 case-table cells; C1–C3 rows and the generic blocks against the plan; the search log; resolution of IDs and entry references | only E-045 is unbalanced. 35/35 C rows equal the plan's (Stage 1 part column included). All 20 `omn` blocks of the plan appear verbatim, plus INV-111's third conjunct. Search log: 97/97 lines verbatim. Model: 379 IDs referenced, RATIONALE: 310, all resolve. RATIONALE has 432 entries, no duplicates, no unknown anchors, 397 entry references resolved |

**Read by hand:**
- PROCESS.md in full;
- the plan, sections 0–15;
- the fix log in full;
- v35 sections 1–4, 6.0, 9–11, every edited invariant (predicate, Reading and Notes against v34), all 67 element Conformance fields against v34, and the Meanings of the edited elements;
- the RATIONALE entries for R35-01, CA-05, CA-06, CA-07, CA-12, CA-14, CA-15 and CA-16, SEC-2.11/W01, SEC-3.4/D01, SEC-3.8/D01, and the moved entries named in EQ35-03 and EQ35-04;
- the watch-point lists of checks 12, 16, 24, 28 and 32;
- the audit findings CA-01 to CA-19;
- Stage 1 OUT-002, 008, 011, 019, 020, 030 and 031, and the source table entry of S-035.

## Defects

### EQ35-01 Formal defect (syntax): stray `}` in the definition of `namedCriteria`
- **Location (v34 / v35 / RATIONALE):**
  - v34 E-045 Definition: `const namedCriteria : set1 ResponderCriterion ≙ {critNice1328, …, critRu71}`.
  - v35 E-045 Definition, last line (model line 1469): `const namedCriteria : set1 ResponderCriterion ≙ table SD-RC}`.
- **Problem:**
  - The edit replaced the set display but left its closing brace. The paragraph is not of the form `const S : set1 T ≙ table N` (sections 2.3 and 2.11), so the defined constant that SD-RC's form V depends on is ill-formed.
  - INV-116 and E-045 `alsoRestsOn` use this constant.
  - The plan section 8 text is `≙ table SD-RC`. The fix log's check C2 ("edited exactly by the scripted plan section 8 edits") does not hold for this block.
- **Evidence:**
  - Bracket count: the E-045 `omn` block has 12 `{` and 13 `}`.
  - It is the only unbalanced block of the 160 v35 blocks; all 188 v34 blocks are balanced.
- **Required change:** delete the trailing `}` (and in `history/v35.md`).

### EQ35-02 Citation defect (lost value): the S-035 URL is truncated in 11 RATIONALE quote entries
- **Location (v34 / v35 / RATIONALE):** RATIONALE entries E-041/Q00, E-041/Q22 to Q28, E-045/Q00, E-045/Q03 and E-045/Q04, in the line `- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon`.
- **Problem:**
  - From v35 on, the URL of a quote is given once, in its RATIONALE entry (PROCESS.md section 6).
  - The URL is cut at the first `)`. The Stage 1 source table (S-035) gives `https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon)%20(92%20Sayfa).pdf`.
  - The truncated link is not a URL where the eleven Turkish quotes can be read (PROCESS.md section 4).
- **Evidence:**
  - `urls.py` compared all 153 Source lines with Stage 1 section 5 and model section 10.
  - 142 match; the 11 that do not are exactly the S-035 lines.
  - The quotes, locations and translations in these entries are verbatim (`quotes.py`).
- **Required change:** give the full Stage 1 URL in the 11 Source lines.

### EQ35-03 Contradiction / prose overclaim: CHG-03 not carried into ISS-03 and E-044/D01
- **Location (v34 / v35 / RATIONALE):**
  - v35 section 8, ISS-03 "Effect on the model", OUT-019 bullet: "residual migraine days next to every percentage change in migraine or headache days, whatever the subject's headache types (E-044, INV-060, INV-061)".
  - RATIONALE E-044/D01: "The residual migraine days are shown next to every percentage change in migraine or headache days without the condition …".
  - Related, weaker: E-040/D01, "OUT-019 asks, wherever a percentage change … is shown, for the residual burden next to it (INV-060)"; and INV-060/D01, "a percentage change in the headache days of a subject without migraine SHOULD also be shown with its residual migraine days".
- **Problem:**
  - Under CHG-03, INV-060 asks for the residual burden only where `ch.compared.period.lengthDays ≥ shortestMonthlyDays`.
  - ISS-13 says it "is not asked for next to a change over a shorter compared period".
  - So section 8 now contradicts itself (ISS-03 against ISS-13), and E-044/D01 contradicts INV-060 (PROCESS.md section 6a: a difference between RATIONALE and the model is a defect).
  - These sentences were true of the v34 predicate and were not qualified when CHG-03 was applied. The plan qualified only the E-040 Conformance field and row OUT-019.
- **Evidence:**
  - The v34 and v35 ISS-03 fields are identical (the ISS diff shows no change to ISS-03).
  - INV-060 v35 predicate and Reading ("… whose compared period has at least 28 days …").
- **Required change:**
  - Qualify the OUT-019 bullet of ISS-03 and E-044/D01: "next to every percentage change in migraine or headache days whose compared period has at least 28 days (INV-060; ISS-13)". In E-040/D01 and INV-060/D01, make the same qualification or cite ISS-13.
  - This is a qualification required by an intended change, not a restoration of earlier wording, so the text-only watch point (check 24, watch point 7) is not touched.

### EQ35-04 Contradiction (RATIONALE and model prose against the model): references to conjuncts that v35 moved
- **Location (v34 / v35 / RATIONALE):**
  - **Substantive** (the sentence states what the model no longer states):
    - RATIONALE INV-123/D02 (moved from v34 INV-117 Notes): "an adherence summary (INV-067), a treatment line (INV-079) and a post-stop monitoring view (INV-112) show a treatment of the subject wherever they are shown, and a response comparison (INV-056) and a treatment review view (INV-068) do so at MUST"; and "one of the subject's preventive treatments (INV-056)".
    - RATIONALE INV-112/D01: "… and the on-treatment period where the context states no start, are asked for by INV-070 at the level of OUT-022".
    - RATIONALE INV-103/D01: "… and INV-070 for an on-treatment period wherever a course event of the course is dated before the changed regimen".
  - **Misattribution** (same constraint, now in another item):
    - RATIONALE INV-074/D01: "only through INV-075" and "(INV-075)", for the formulation of a line; now INV-123 (`usedMedication`).
    - RATIONALE INV-109/D01: "INV-079 makes every shown dose change one of them"; now INV-123 (`courseEvent`).
    - RATIONALE E-046/D03: "as in INV-081 and INV-082", for available results; the availability is now INV-123.
    - RATIONALE INV-049/D01 ("Its content is that of INV-050: … and the review window") and INV-123/D06 ("… and the review window … stay at its level (INV-050)"); the review window is now asked by E-039 `reviewWindow` alone (CA-05).
    - Model INV-069 Reading ("whose outcome summaries and treated-attack lines INV-072 shows in the same view") and INV-071 Reading ("in the same view (INV-072)"); this placement is now the W2 markers on E-051 `outcomes`, `sequence`.
    - Model ISS-11 Effect "(E-039, INV-050, INV-051)".
- **Problem:**
  - Moved prose must describe v35: plan 9.1, rule P0; D-14 updated 15 such entries, but these were missed.
  - Under CHG-R1, the ties of INV-056 and INV-068 are definitional members of INV-123, so "do so at MUST" now states a level the model does not have.
  - Since the merge into E-049's `when` clause, INV-070 contains no ask at all, so INV-112/D01 and INV-103/D01 name the wrong item for that ask.
  - The other places cite an item that no longer holds the constraint they describe. The constraint itself still holds, elsewhere and at the same level.
- **Evidence:**
  - The v35 predicates of INV-056, INV-067, INV-068, INV-070, INV-072, INV-075, INV-079, INV-082, INV-112 and INV-050, as diffed in `formal_diffs.txt`.
  - INV-123's `factsShown`; the E-049 `onTreatmentPeriod` `when` clause; the W2 index of section 6.0.
  - `stale.py` lists the sentences.
- **Required change:**
  - Replace the cited items by their v35 places (INV-123; E-049 `onTreatmentPeriod` `when`, E-049/D04; E-051 `outcomes`, `sequence` (W2); E-039 `reviewWindow`).
  - In INV-123/D02, state that the response comparison and the treatment review view show a treatment of the subject definitionally (INV-123; CHG-R1).

### EQ35-05 Prose overclaim: the Reading of INV-118 asks for all kinds of a case in one view and series
- **Location (v34 / v35 / RATIONALE):** v35 INV-118 Reading: "… the diary can produce an output in which one view and one series that spans the selected time range show, for every period of the series, values of each kind that the case asks for, with the type scope it names".
- **Problem:**
  - The predicate asks `reportedTogether(c, q.2, q.1)` separately for each pair `q ∈ ppRequired(r, l, c)`. Each pair may be met by another output, view and series.
  - C1-09 has four pairs (the most bothersome symptom, and each associated symptom), as v34 INV-022 had separate `reportedPerPeriod` calls. C1-13 has one pair per type scope, as v34 INV-028 had `∀ sc • reportedTogether`.
  - The Reading therefore asks for these values together in one view and series, which neither v35 nor v34 requires.
  - "The type scope it names" is also undefined for C1-13, whose case names several scopes.
  - RATIONALE INV-118/D03 and SEC-2.11/W01 state the unfolding correctly.
- **Evidence:** the INV-118 predicate and table C1 (rows C1-09, C1-13); v34 INV-022 and INV-028. `eq_c1.py` confirms that the predicate as written equals v34.
- **Required change:** paraphrase the per-pair quantifier, for example: "… for every pair of a type scope and kinds of per-period value that the case asks for, the diary can produce an output in which one view and one series that spans the selected time range show, for every period of the series, values of each of these kinds with that type scope".

## Checked and equivalent

**Generic invariants (families F1–F9 of the plan):**
- **INV-118 + C1.** Each of the 14 cases unfolds to its v34 invariant, with its own `∃ g` and the same level:
  - an applicability condition moved into `ppRequired` empties the set outside the condition, the same as the v34 antecedent;
  - INV-108 is two cases;
  - C1-11 equals INV-025, because E-036 `WeeklyMedicationView` is the type of views with a weekly series showing `TotalAcuteMedicationDays`;
  - `medicationKinds` is INV-023's term verbatim;
  - checked by script and by symbolic unfolding.
- **INV-119 + C2.** MUST NOT is equal. SHOULD NOT differs only by CHG-07: for every-element bearers and for C2-08 (with W2 on `qualifies`), the annotation disjunct of `presents` adds nothing.
- **INV-120 + C3.** Equal at MUST and SHOULD. C3-02 (`may`) imposes nothing, as the v34 E-010 MAY did. `ctx(outputOf(·))` equals `ctx` in output scope.
- **INV-121 and INV-122.** One union member or disjunct per replaced conjunct, with the same quantifier ranges and definitional level. The last two conjuncts of INV-122 are INV-030 verbatim.
- **INV-123.** Each member of `factsShown`/`stated` equals the v34 conjunct it replaces:
  - `startOf` and `eventOn` reduce to course-event membership;
  - `AcuteMedication` has exactly the components `drug` and `formulation`;
  - the role conjuncts are equal under INV-001 disjointness and `TreatmentRole ::= preventive | acute`;
  - `markedKind` and the E-049 event kinds became attribute types, which are definitional as INV-036 and INV-112 were.
  - The only new member is `usedScope` (CHG-05).
- **INV-124.** Its third conjunct implies the removed INV-089 conjunct, since the bouts and remissions of a view are atoms of its output (W1).
- **INV-125 + SD-DF.** Equals INV-009 (MUST) and INV-010 (SHOULD). The domains of both partial functions are the two keys.

**Rule W2.** All 19 marked attributes equal the placement conjuncts they replace, with the same atoms, condition and level:
- `y = h` is impossible for item-typed references, and matches INV-007's `e = viewOf(a)` for `qualifies`;
- D-5's reading, that a marker without its own `when` applies to every atom, is the one needed. Every replaced conjunct was unconditional, and E-033's `when` equals INV-092's antecedent;
- E-046 `comparison` is `opt`, so ∃ splits into ∀ ∧ ∃.

The unmarked references (`ClassGroup.lines`, `cycles`, cluster view, periods) are as v34.

**New constructs.**
- Section 2.11 forms V, M, C and D; `Level`; `CatalogueRow`; the level-indexed semantics (3.3, item 7); and markers (2.5 W2, 3.3 item 8) are defined precisely enough for an unambiguous unfolding. I did not need any choice beyond the text. Every key set is distinct, and every default matches its v34 "otherwise".
- The ⇸ domains of `publishedRecall`, `scoreRange` and `screeningMax` are exactly the v34-commented domains. The v34 comments had no formal force; CA-11 made them formal, as the fix log states.

**Source data tables.** Every value, code, threshold, label, range, rule, criterion, band, name and constant equals v34 (383 values). INV-064, INV-073 and INV-085 reformulated with SD-CL, SD-ET and SD-SR are equivalent (exhaustive).

**R-MCF.**
- The 16 places of plan 7.2 / SEC-3.8/D01 keep their v34 formal tests, so each verdict is v34's.
- The one formal move, the E-049 `when` clause merged with the INV-070 ask, is equivalent. The stated-start disjunct is verbatim: a stop on the start day asks for the period; a reduction on the start day does not.
- The v34 per-item prose treatments ("Course start not stated", "Start not stated", "Original start not stated") agree with clauses (1)–(4). E-049's sentence "aligned to the event, not to the start" is kept in E-049/D03.

**Intended changes.** Each is implemented as described, is no broader, and is consistent with Stage 1:
- **CHG-01** (OUT-030, OUT-035): INV-124 first conjunct and `shownDayOnes`. The R35-01 claim holds in my enumeration, including the exception for lines that have not ended.
- **CHG-02** (OUT-031: a remission is attack-free and a bout has attacks).
- **CHG-03:** exactly the 28-day threshold at which INV-061 can be met (`ofKind` fourWeekPeriod is any 28-day span). ISS-13 records the open question; but see EQ35-03.
- **CHG-04** (OUT-008 is MAY; section 3.3 item 5).
- **CHG-05:** any acute-medication day count > 0, for every scope kind, tied by `inMedicationScope`, which is guarded by INV-001.
- **CHG-06:** the verbatim plan conjunct. The fully conformant repertoire is unchanged, because INV-008 could not be met.
- **CHG-07** (OUT-011 Caveat, OUT-020).
- **CHG-R1:** MUST-conformant and fully conformant repertoires are unchanged.

**R35-01 and CA-01 to CA-19.** Resolved as the fix log says:
- CA-01 → CHG-03 + ISS-13; CA-02 → CHG-04; CA-03 → CHG-05 (the 8.2.6 single-class guarantee now holds, because class indicators rest on DayCount bases); CA-07 → CHG-06.
- CA-05: INV-050's review-window conjunct is implied by E-039 `reviewWindow` (SHOULD, no `when`) at the same level.
- CA-11: the 3.2 sentences equal the old comments.
- CA-04, CA-06, CA-08, CA-09, CA-10, CA-12, CA-14, CA-15, CA-16: the prose is corrected as stated.
- CA-13: kept, as stated.
- CA-17, CA-18, CA-19: section text corrected.

**Deviations D-1 to D-18.** None changes a formal meaning:
- D-4 (forms C and D) and D-5 are needed for the unfoldings to equal v34.
- D-6 and D-7 (constants and tables stated once) are equivalent.
- D-8 (catalogue column, informative) and D-9 (INV-122 Realises OUT-036, needed for traceability) are bookkeeping.
- D-10 to D-18 are prose and layout. I checked them: quotes are intact, and D-12 keeps v34's purpose clause.

**Levels and traceability.**
- Per Stage 1 statement part, the levels are unchanged except CHG-R1.
- No (item, OUT) pair is lost, and the Realises of kept items are unchanged.
- Section 7 agrees with the items. The coverage lines name C, SD and W2 places at the right levels (sampled OUT-016, 017, 018, 020, 023, 030, 031, 038).

**Watch points (checks 12, 16, 24, 28, 32).** None is reversed. The following are byte-identical or verbatim:
- E-041 values (SD-ER) and responder labels: INV-063, INV-114 and INV-116 byte-identical; `namedCriteria` `set1`; `E-046.comparison` stays `opt`; `#L.evaluated = 1` and the `evaluationResult`/`pretreatmentBaseline` pair unchanged;
- section 2.8, `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`;
- the treatment-course decisions: INV-001 (one stop per course; a restart is a new course), `resumes`, `originalStart` without fallback, `courseBegunBy`, and INV-112's bounds;
- `fillsPeriod` with its 28-day anchor (E-006), and INV-050's start ties;
- the by-dates relations: `daysOf`, INV-006, INV-030 inside INV-122, the INV-031 "mark implies 0" conjunct;
- INV-111 to INV-117: kept, merged verbatim into INV-123, or extended by CHG-06 only;
- `onSameScale` and `inSameForm`: E-023, E-025, INV-027, INV-039, INV-069 and INV-105 are byte-identical;
- the formulation ties (INV-123 members, INV-074 unchanged);
- the cluster view: INV-089 keeps `ongoing`, `lastDay`, `e ≤ ctx.asOf`, the `plusMonths` form with SD-FX-07 = 3, `onlyOfType` and the rate relation; there is no placement, so fix 11 stands;
- INV-087's lead-in; INV-098 as C3-11; co-presence (INV-054 as an E-040 marker with `when ofResponseComparison`);
- the text-only items: E-057 Notes, ISS-02 and ISS-12 moved as planned; ISS-03 is unchanged (see EQ35-03).

CHG-04 deletes the conjunct that check 24, watch point 1 lists among the by-dates relations. Deletion is not one of its reversal triggers, which concern atom identity. It is a listed intended change with a stated reason (section 3.3, item 5).

**Quotes.** Every source-attributed quote is present verbatim, with its source and location, as listed in the method table. Every Evidence pointer resolves to a Q entry holding its source. The search log is verbatim.

**Scope.** I found no input data, storage format or derivation from input in the new text. The counts of scope terms do not rise from v34 to v35 + RATIONALE. Case tables hold output values and the cases of generic invariants; their context terms are subject properties, as in v34.

**Satisfiability.** The generic invariants are jointly satisfiable with the kept invariants they interact with (`witness.py`; `r3501_check.py`: 28,895 admitted one-view outputs). The new exclusions are only outputs that state contradictory dated phases (CHG-01, CHG-02), false medication facts (CHG-05) or a change across two definitions (CHG-06). Stage 1 permits none of these.
