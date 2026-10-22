# Oscillation check — after iteration 40
VERDICT: NO_OSCILLATION
Date: 2026-10-22
Versions examined: v00 to v40 (`history/v00.md` … `history/v40.md`), together with:
- the first committed v35 (commit 3b67179, called **v35a** below, as in the check after iteration 36);
- `history/v35-rationale.md` to `history/v40-rationale.md` and the RATIONALE of 3b67179.

`OUTPUT_MODEL.md` is byte-identical to v40. `RATIONALE.md` is byte-identical to `history/v40-rationale.md`, which equals `history/v39-rationale.md`: fix 40 did not change it.

## Summary

No item oscillates across iterations 37–40. Nothing is frozen: `FROZEN_ITEMS.md` was not written, and `OUTPUT_MODEL.md` was not changed.

**What changed in the formal content.**
- **v37.** No `omn` block and no case or source-data row changed. The catalogue's Availability, Shown with it and Prohibited cells (38 cells in 34 rows) stopped restating the seven output-wide invariants. Section 4.2 now states them once (R37-01).
- **v38.** Five `omn` blocks changed and one case row was withdrawn:
  - section 4.4: new constant `byTypeCases`;
  - INV-118: a second conjunct;
  - case C1-13 withdrawn (R38-01);
  - INV-049: its series is no longer tied to the selected granularity;
  - INV-096: one granularity of the diary's choice, `∃ g` (R38-02);
  - E-029: comment only.

  ISS-10 now counts five adult-only sources (R38-03).
- **v39.** Two `omn` blocks changed (R39-01):
  - E-056: three MAY content attributes with definitional W2 markers;
  - INV-080: a second conjunct.

  Responder labels were declared not content of the scheme-window view, so E-046 no longer realises OUT-025, and the frequency kinds and E-055 now do.
- **v40.** No formal change. The Readings of INV-061 and INV-075 were brought to their predicates (R40-01).

**No reversals.**
- No `omn` line, case row, catalogue cell, field or 6-word sequence of v37–v40 restores an earlier state that a fix had changed.
- Every watch point of the checks after iterations 04 to 36 is intact.
- 92 of the 98 watched blocks are byte-identical from v36 to v40. So are the section 2.8 and 3.4 blocks, all 94 source-data rows and all C2 and C3 rows.

**The closest approaches.** Each is a single change, backed by a reason that the earlier decision did not consider, and none has flipped back.
- **INV-049 (v38): the third change on the follow-up series.** Check 08's watch point 4 had a tightening (v03) and a qualification (v05) on record. The v38 change rests on Stage 1's granularity statements, which neither sweep considered.
- **C1-13 withdrawn (v38).** This is set against R01-06 and fix 01. The per-class and per-drug kinds are kept.
- **Responder labels and the scheme-window view (v39).** v39 decides against a sentence of the v00 draft. v35 had dropped that sentence without deciding anything, and no fix had ever decided the point.
- **The catalogue stated once (v37).** v37 changes the plan's informative column definitions for the first time.
- **The INV-061 and INV-075 Readings (v40).** The predicates were kept, and the predicate-strengthening alternatives were declined. This is consistent with fix 01 (R01-03), review 11, fix 02 item 14, and CHG-04.

One reversal was avoided: fix 38 declined R38-03's second option, which would have restored ISS-10's v06 scope.

**Direction.**
- v38 makes three deliberate widenings of availability requirements that Stage 1 does not make:
  - the MUST repertoire of OUT-029 (C1-13 → `byTypeCases`);
  - the SHOULD repertoire of INV-049;
  - the SHOULD repertoire of INV-096.

  No earlier version admitted these repertoires, so nothing re-widens.
- v39 narrows only through a new MAY attribute.
- v37 and v40 change no admitted or conformant set.

**Trend.**
- The bookkeeping cascade that followed the restructuring ended:
  - its last rewrite artefact was R37-01;
  - R39-01, whose v00 gap the v35 drop made total, was the last remark tied to the restructuring;
  - fix 39 audited all 1,536 v34 prose sentences, and review 40 found nothing of the kind.
- Since iteration 38, the remarks concern defects present since v00 to v07 that no earlier review raised (5 remarks in 3 iterations). None is caused by a fix.
- The rate is flat: 1, 3, 1, 1. No main review has returned NO_REMARKS since iteration 32.
- The loop converges in direction. Its tail is driven by the size of the model, not by fixes.

## Method

All scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/osc40/` and were run with `python3 -I`. The splitter and the helpers were taken from `osc36/`.
- One change to the splitter: the field pattern now allows digits, so that "Stage 1" fields of section 8 are split as fields. It still reproduces check 36's v35a → v35 and v35 → v36 volumes (top-level items 9 and 11; `omn` blocks 1 and 0; rows 0 and 7).
- v35a and its RATIONALE were copied from `osc36/`.

1. **Git and files.**
   - From ebb2c0c (check 36) to HEAD there are 8 commits in loop order: review 37 (c3f13d9), fix 37 (382f1ed), review 38 (856a965), fix 38 (a15f870), review 39 (5271df0), fix 39 (76cfc3b), review 40 (83cffc8), fix 40 (aa075d3).
   - Each fix commit touches only the model, RATIONALE (fixes 38 and 39 only), their snapshots and its log.
   - At each fix commit `OUTPUT_MODEL.md` equals its snapshot, and `RATIONALE.md` equals its snapshot.
   - No snapshot up to v36 changed after check 36.
   - PROCESS.md and Stage 1 are unchanged since ebb2c0c.
   - The working tree is clean, `FROZEN_ITEMS.md` does not exist, and the model has no FROZEN marker.
2. **Item split and returns** (`split.py`, `versions.py`, `analyse.py`).
   - 42 snapshots (v00–v34, v35a, v35–v40) give 1,894 distinct items: elements, invariants and issues with each field and `omn` text; the sections; and the table rows.
   - Each item was hashed per version after white space was normalised. Every change in v37–v40 was tested for a return to a non-adjacent earlier state.
3. **Formal text, line by line** (`linehist.py`, `omndiff.py`, `hist.py`).
   - Every `omn` line and every case or source-data row removed in v37–v40 was traced to the version that introduced it.
   - Every line added in v37–v40 was tested for presence in an earlier version.
   - The full history of each changed predicate was printed and read: INV-028/C1-13 → INV-118, INV-049, INV-096, INV-080, E-056, E-029, and also INV-061, INV-075, E-044 and E-053 for R40-01.
4. **Prose re-insertion** (`ngram40.py`). The 6-word sequences of sections 1 to 11 were compared:
   - each sequence removed in v37–v40, by the version in which it first appeared;
   - each sequence added in v37–v40 that had been present in an earlier version and absent in the one before.
5. **Near returns** (`nearret.py`). 123 changed fields, rows, sections, blocks and items of v37–v40: is the new text closer, by word-level similarity, to an earlier state than to its predecessor?
6. **Catalogue cells** (`cells.py`). The cell-level history of every catalogue row that changed between v35a and v40.
7. **RATIONALE** (`ratsplit.py`). Entries were split per version, v35a to v40, and the changed, new and removed entries were listed. All decision-carrying entries of v38 and v39 were read in full, and the six re-pointed entries were word-diffed.
8. **Watch-point blocks and tables** (`blocks40.py`):
   - 98 blocks that the checks after iterations 04 to 36 name, compared between v36 and v40;
   - the `omn` blocks of sections 2 to 4;
   - all C1, C2, C3 and SD rows.
9. **Protected terms** (`guar.py`).
   - 65 terms were counted in v34 to v40: the terms of the watch points, together with the new terms `byTypeCases`, `frequencyValues`, `tiles(`, `c.granularity`, `reportedTogether(`, `usedScope`, `usedMedication(`, `shortestMonthlyDays`, `shownDayOnes` and `presents(`.
   - The text counted is the comment-free `omn` blocks and the backticked cells of the catalogue, case and source-data tables.
   - Every drop was traced to its cause.
10. **Levels** (`levels.py`). Invariant levels per version, v35–v40, and attribute declarations in v36 and v40.
11. **Loop files.**
    - Read in full:
      - PROCESS.md;
      - the checks after iterations 32 and 36;
      - reviews 37 to 40 and fixes 37 to 40;
      - the watch points of the checks after iterations 04, 08, 12, 16, 24 and 28.
    - Read at the passages that bear on the changed points:
      - R01-03, R01-06 and fix 01;
      - fix 02 item 14; fix 03 (INV-050 and INV-049); fix 05 (the R05-01 sweep, INV-049);
      - review 04 (R04-02, the INV-050 note) and fix 04; fix 10 (INV-028 rows); fix 11 (context sweep, INV-049); review 11 (OUT-019);
      - fix 36 (catalogue sweep, R36-03 class); the fix-35 mapping for E-056 and INV-080.
    - Every review and fix was searched by script for INV-028, INV-049, scheme or E-056, residual burden, adverse events and ISS-10.

**Results of the mechanical steps.**
- **Returns (step 2).**
  - One hit: row C1-13 is absent before v35 and absent again from v38. This is the withdrawal of the v35 row that carried v34 INV-028, not a return of content (Items, row 2).
  - No other item returns to a non-adjacent earlier state.
- **Formal lines (step 3).**
  - v36 → v37: 0 removed, 0 added.
  - v37 → v38: 4 removed:
    - INV-049's series conjunct, present since v05 as the rewording of v00;
    - row C1-13 (since v35a);
    - two INV-096 lines, re-bracketed.

    8 added, none present in any earlier version.
  - v38 → v39: 1 removed (INV-080's first line, re-bracketed); 6 added, none earlier.
  - v39 → v40: 0 removed, 0 added.
- **Prose re-insertion (step 4).**
  - 0 re-inserted sequences in v37 and v40, and 2 in v39, both artefacts:
    - the INV-080 title reuses the v00 Reading phrase "windows are the selected windows, and";
    - OC-08's Realises ends "OUT-007, OUT-025", and OUT-013 is not re-added.
  - 37 in v38, all phrasing:
    - INV-118's new conjunct reuses v34 INV-028's quantifier text;
    - the INV-096 Reading reuses "are reported for every period of the selected time range" (v00–v09) while keeping the v12 time frame;
    - ISS-10 quotes E-041/D01.

    None restores an earlier meaning.
- **Near returns (step 5).** 0 hits in 123 changes.
- **Catalogue cells (step 6).**
  - Rows changed: OC-08 in v36, v37 and v39, each time in a different column (Realises −OUT-013; Shown with it; Realises +OUT-025). OC-35 in v37 and v38. OC-23 and OC-29 in v37 and v39. All other rows once.
  - No cell returns to an earlier state.
- **RATIONALE (step 7).**
  - Entries per version: v36 → v37 0 changed; v37 → v38 12 (3 new); v38 → v39 3 new; v39 → v40 0.
  - The six re-pointed entries change only "INV-118 (C1-13)" to "INV-118 (`byTypeCases`)", and each sentence stays true of the new place.
- **Watch-point blocks and tables (step 8).**
  - 92 of the 98 blocks are byte-identical from v36 to v40. The 6 that changed are E-029, E-056, INV-049, INV-080, INV-096 and INV-118.
  - The section 2.8 and 3.4 blocks are identical. Of the 160 `omn` blocks, 153 are identical; the 7th changed block is section 4.4.
  - C1: only C1-13 (withdrawn). C2, C3 and all 94 SD rows: identical.
- **Protected terms (step 9).**
  - Unchanged from v36 to v40, among others: `notStoppedBefore(` 5, `fillsPeriod(` 6, `courseBegunBy(` 5, `originalStart(` 3, `#L.evaluated = 1` 4, `rc.treatment = L.treatment` 10, `onSameScale(` 4, `inSameForm(` 2, `publishedGrading(` 2, `usedScope` 3, `usedMedication(` 3, `shownDayOnes` 2, `presents(` 2, `menstruatesDuring(` 4, `consecutive(v.after)` 1, `shortestMonthlyDays` 4, `set1` 26.
  - The drops, each explained:
    - `allTypes` 106 → 105: the C1-13 cell;
    - `tiles(` 8 → 7: the INV-049 series conjunct.
  - The increases: `sameSpan(` 29 → 30 (INV-080), `reportedTogether(` 2 → 3 and `byTypeCases` 0 → 4 (INV-118), `c.granularity` 10 → 11 (INV-096 and INV-118 add one each; INV-049 loses one), and `frequencyValues` 0 → 2.
- **Levels (step 10).**
  - v35 to v40: MUST 11, SHOULD 33, SHOULD NOT 1, definitional 38, level-indexed 4. No invariant changed level.
  - Attribute declarations: 172 → 175, the three new E-056 attributes, all MAY.

## Items examined

"Convergent" means a change in one direction that keeps every earlier guarantee, or an equivalent move. Versions are those in which the item changed.

| Item | Versions where it changed | Nature of each change | Verdict |
|---|---|---|---|
| **Catalogue, section 4.2 (column definitions; "Stated once for all rows") and section 4.3 cells** | 4.2: v35a (new), v36, v37, v38. Cells: v35a (new); v36 (OC-08 Realises); v37 (38 cells in 34 rows); v38 (OC-35); v39 (OC-05 to OC-08, OC-23, OC-29 Realises; OC-30) | **v36 (R36-03):** the 4.2 prose says the cells "repeat the OMN predicates of applicability conditions"; OC-08 loses OUT-013.<br>**v37 (R37-01, option (a)):**<br>• the seven output-wide invariants (INV-003, INV-006, INV-008, INV-011, INV-121, INV-122, INV-123) are stated once;<br>• "label", "completeness", the generic "def." entries and the per-row INV-123 mentions are removed;<br>• OC-14 "(no invariant)" (false) is removed;<br>• OC-45 Prohibited → "—";<br>• placements by INV-060 (OC-22) and INV-087 (OC-36) are named.<br>**v38:** OC-35 per measure (`byTypeCases`).<br>**v39:** Realises follow E-056's content (OUT-025). | **Convergent.**<br>• First change of these cells. v36 had changed only OC-08's Realises and the 4.2 prose.<br>• No cell returns to an earlier state.<br>• Review 37's option (b), adding the 91 missing pairs per row, was not taken. Taking it now would be A → B → A.<br>• The column layout of plan-v35 is kept; only what three informative columns hold changed, under PROCESS.md section 6a.<br>• No formal force (section 4.2). |
| **C1-13 withdrawn; `byTypeCases`; INV-118 second conjunct** (v34 INV-028) | INV-028: v00, v01 (`omn`), v10 (Reading). C1-13: v35a (row) → withdrawn v38. INV-118: v35a, v38 | **v00 (author):** `∃ g ∈ MonthlyKind`, one `reportedTogether` for headache days, total acute-medication days and, where provided, moderate/severe headache days and attacks, for every type scope.<br>**v01 (R01-06):** per-class and per-drug kinds added, "as in INV-023".<br>**v10:** the Reading states the monthly granularity and "together" (prose sweep, "match").<br>**v38 (R38-01):** the per-type values are asked through the combined-scope cases C1-01, C1-04, C1-06 and C1-10, each with its own `∃ g` and its own granularities: monthly for the frequency measures, `Granularity` for acute-medication days. No joint view. | **Not a reversal; a first change.**<br>• R01-06's per-class and per-drug kinds are kept, through `medicationKinds(c)` in C1-10.<br>• The per-type medication days now have INV-023's (C1-10's) granularity, which is literally R01-06's "as in INV-023" and review 01's settled "INV-023 at any granularity".<br>• R04-02 and fix 04 (monthly MUST for moderate/severe headache days and attacks where provided) are kept, per type, through C1-04 and C1-06.<br>• Review 14's "no migraine days per headache type" and ISS-09 (weekly view and overuse indicator combined only) are kept.<br>• The joint view and monthly granularity had never been decided: fix 10's "match" and fix 11's "one view" checked the Reading against the predicate, not against Stage 1.<br>• v38 extends INV-118/D03's principle ("one existential quantifier over both would strengthen the rule") to the per-type instances.<br>• The MUST repertoire widens. No earlier version admitted it.<br>• Check 12's presence-quantifier pattern: no ∀ over drugs or classes returns to ∃. |
| **INV-049** (follow-up view) | `omn` v00, v05, v11, v12, v17, v38. Reading v00, v05, v11, v12, v17, v38. Notes v11, v35a, v38 | **v00:** `tiles(v.series, c.timeRange, c.granularity)`.<br>**v05 (fix-05 sweep):** `sameSpan(v.covers, c.timeRange) ∧ ∃ sr ∈ v.series • tiles(sr, c.timeRange, c.granularity)`, "keeps … what INV-049 and INV-050 required together in v04".<br>**v11:** running follow-up. **v12:** every start of withdrawal. **v17:** `<`.<br>**v38 (R38-02):** the `∃ sr … tiles(…, c.granularity)` conjunct is removed. The series is left to E-039 (`series`, SHOULD `when wholePeriodFrom`) and INV-050 (start tie, `fillsPeriod`), both byte-identical. `∀ c ∈ Ctx` is kept: fix 38 rejected `∃ g`, because it would leave starts without views (R11-03, fix 12). | **Not oscillation; the closest approach.** This is the third change touching the follow-up view's covered period against its series: v03 tightened INV-050, v05 qualified it, and v38 loosens INV-049. Check 08's watch point 4 asks that a third change rest on new evidence. It does:<br>• Stage 1 OUT-017 names no granularity, and weekly values are asked only by OUT-009 (where relevant) and OUT-015;<br>• section 3.4's generic rule is `∃ g`;<br>• the per-case difference from INV-118, INV-034 and INV-044.<br>Fix 03's sweep (a stated covered period not tied to its series) and fix 05's sweep (series that must tile arbitrary covered periods; it listed INV-049 as "unchanged") did not consider which granularity Stage 1 permits.<br>What v38 does not do:<br>• restore any earlier state: every version from v00 to v37 had the tie;<br>• touch the objects of the watch point (INV-050 and E-039: start tie, `fillsPeriod`, no end tie);<br>• touch the 28-day anchor (E-006), the running conjunct (v11), "every start" (v12), `<` (v17) or `sameSpan` (v05).<br>Review 04's coverage note still holds: views are still required for every context. |
| **INV-096** | `omn` v00, v12, v38 | **v12 (sweep):** age read per date and period (`childOn`).<br>**v38 (R38-02):** `∃ g ∈ Granularity` before the series conjunct; both bodies verbatim. | **Convergent; a first change on the granularity dimension.** The v12 age reading (check 12) is verbatim. Not moved into table C1 (INV-096/D02). |
| **Section 3.4** (generic per-period rule) | v00, v04, v35a, v38 | **v38:** the `∃ g` rule also covers values for which Stage 1 names no period (OUT-036 (b), INV-096); per-type instances by `byTypeCases`. | Convergent. It extends the rule that INV-118, INV-034 and INV-044 already apply, and review 01's settled reading. |
| E-029 (comment, Conformance), INV-068 Evidence, ISS-09 Effect, OUT-029 row, section 9 (C1-13 row, INV-028 row) | E-029 Conformance v00, v01, v12, v35a, v38; INV-068 Evidence v00, v02, v35a, v38; ISS-09 Effect v01, v35a, v38; OUT-029 row v00, v01, v24, v35a, v38 | References to C1-13 → C1-10 and `byTypeCases`. | Consequential bookkeeping. No earlier text is restored. |
| **ISS-10, "Stage 1" field** | v06, v07, v38 | **v07 (R07-01):** "that OUT-018 quotes for these time points" → "that Stage 1 cites for OUT-018"; the count was left at four.<br>**v38 (R38-03):** "five", adding [S-002]. | **Convergent.** R38-03's second option would have restored the v06 scope that fix 07 deliberately widened, and fix 38 declined it. Effect and For the human are unchanged, and so are `ruleRuChildren` and the rule-list boundary (check 08, watch point 3). |
| **E-056 content; INV-080 second conjunct; Realises of E-046, E-015, E-016, E-017, E-019, E-055; row OUT-025; ISS-04** | E-056 Conformance v00, v35a, v39; `omn` v00, v39. INV-080 `omn` v00, v39. E-046 Realises v00, v39. Row OUT-025 v00, v35a, v39. ISS-04 v00, v01, v04, v39 | **v00 (author):** "Its content (headache days and migraine days per window, instrument results, treatment lines, responder labels) is MAY", in prose only. E-046 lists OUT-025.<br>**v35a:** the sentence is dropped by the Conformance template; the fix-35 mapping says "kept; formal text unchanged".<br>**v39 (R39-01):**<br>• `frequencyValues`, `instrumentResults` and `treatmentLines` (MAY, `shown`);<br>• INV-080 ties each frequency value to a window by `sameSpan`;<br>• responder labels are not content (E-056/X01 (3)), and E-046 loses OUT-025;<br>• ISS-04 also covers OUT-025's frequency outputs. | **Not a reversal.**<br>• The v35 drop was no intended change, so v39 restores unintentionally lost content, now formally, and adds nothing to the model's prose.<br>• Excluding responder labels decides, for the first time, against a sentence of the v00 draft that no fix had decided, as CHG-04 did for a v00 conjunct (check 36). The reason is new: a label under a scheme rule applies a scheme criterion (E-045/N02), and "month-by-month responder views" is an example of a window.<br>• The admitted views are unchanged, because the attributes are MAY and new.<br>• INV-080's v00 conjunct is verbatim. |
| **INV-061 Reading** (residual burden) | `omn` v00, v01. Reading v00, v01, v40 | **v01 (R01-03):** the compared period itself where monthly. The general "monthly period within the compared period" is kept for changes outside response comparisons.<br>**v40 (R40-01):** "each count for a calendar month or 28-day period … which may differ between the two counts"; "on-treatment" dropped. | **Convergent: text brought to the predicate.**<br>• The predicate has quantified the two counts separately since v00. Fix 01 did not decide whether they share a month.<br>• Review 11 settled that "per month that remain on treatment" is read on the compared period, which v40 now says.<br>• Fix 02 item 14 (compared periods shorter than 28 days) and ISS-13 are untouched.<br>• Fix 40 declined the reviewer's alternative, a `sameSpan` tie, because Stage 1 does not ask for it. Fix 32's table also treats each count as a true value of its own period. |
| **INV-075 Reading** (treated-attack line) | `omn` v00, v02, v17, v35a (a move). Reading v00, v02, v17, v35a, v40 | **v02:** symptom status. **v17:** formulation tie. **v35a:** the formulation tie moved to INV-123, so the Reading equals v02 (check 36).<br>**v40 (R40-01):** the adverse-event clause is stated as the conjunct, "at most one" result per measure, and clauses 3 and 4 name their results. | **Convergent.**<br>• The adverse-event conjunct and E-053 are unchanged since v00.<br>• No earlier Reading wording is restored: 0 re-inserted 6-word sequences in v40.<br>• Fix 40 declined the reviewer's alternative (`adverseEvents ≠ ∅ ⇒ (drugRelatedAdverseEvent, true) ∈ results`). That would be a definitional presence tie, which section 3.3 item 5 and CHG-04 exclude (watch point 2).<br>• INV-072 (fix 01, R01-07) still asks every required outcome at SHOULD. |
| RATIONALE: INV-118/D04, INV-049/D02, INV-096/D02 (new v38); E-056/D02, S01, X01 (new v39); C1-13/D01, INV-118/D03, INV-096/D01 (qualified v38); SEC-3.4/D01, E-012/D01, E-064/D03, INV-073/D01, INV-089/D01, INV-118/D01 (re-pointed v38) | v38, v39 | Decision records of the v38 and v39 changes, and re-pointing of moved text from C1-13 to `byTypeCases`. | **Consistent with the model's decisions.**<br>• Each decision entry names the rejected options: `∃ g` for INV-049, the C1 move for INV-096, one shared `∃ g` for the per-type cases, `within` ties, date ties and responder labels for E-056.<br>• The re-pointed sentences stay true: the per-type attack and medication counts of OUT-029 are still asked.<br>• No entry restores a v34 text. |

## Watch points from earlier checks

| Source | Watch point | State in v40 |
|---|---|---|
| Check 36, wp 1 | INV-060 antecedent / ISS-13 (CHG-03) | **Intact.**<br>• INV-060, INV-061 (predicate) and ISS-13 are byte-identical to v36.<br>• R40-01 concerns compared periods of 28 days or more that are not monthly. No per-month residual was added for shorter periods.<br>• OC-22 names INV-060's placement, not its antecedent. |
| Check 36, wp 2 | INV-031 completeness conjunct (CHG-04) | **Intact.** INV-031 and INV-104 are byte-identical; "a mark implies 0" is kept. Fix 40 relied on the same principle to decline a definitional presence tie in INV-075. |
| Check 36, wp 3 | Class of INV-123 | **Intact.**<br>• INV-123 is byte-identical: `usedScope`, `usedMedication`, CHG-R1 at definitional level.<br>• No member was added, removed or lowered, and no count of 0 was tied.<br>• v37 removed only the per-row catalogue mentions.<br>• The INV-080 conjunct ties output elements to each other (dates of a window), not to a context fact.<br>• Fix 40 declined two further ties. |
| Check 36, wp 4 | INV-124 (CHG-01, CHG-02) | **Intact.** INV-124, INV-087, E-060, E-061, E-063 (`lastDay`) and INV-089 are byte-identical. |
| Check 36, wp 5 | CHG-06, CHG-07 | **Intact.** INV-111 is byte-identical. The C2 rows are byte-identical, so the `presents` annotation disjunct of C2-03 and C2-06 is kept (`presents(` 2). Per-value definitions were not taken. |
| Check 36, wp 6 | E-049 `onTreatmentPeriod` `when` clause | **Intact.** E-049, INV-070, INV-112 and section 3.8 are byte-identical. |
| Check 36, wp 7 | E-039 `reviewWindow` (CA-05) | **Intact.** E-039 and INV-050 are byte-identical, with no `when` clause. "Required once the covered period reaches its end" occurs in neither file. |
| Check 36, wp 8 | INV-105 Reading lead-in (CA-16) | **Intact.** INV-105 and E-067 are byte-identical. |
| Check 36, wp 9 | Source-data cells as axioms | **Intact.** All 94 SD rows are byte-identical to v36. Reviews 37 to 40 each re-verified the values against the sources. |
| Check 36, wp 10 | v33 comparability and value-set conjuncts | **Intact.** E-023, E-025, E-033 and INV-082 are byte-identical. `publishedGrading` is not fixed for MSQ, M-TOQ or PGIC, and no scale or form tie was extended to INV-062. |
| Check 36, wp 11 | Earlier triggers at the v35 places | **Intact.**<br>• INV-123 members, E-034 and E-049 attribute types, INV-121 and INV-122 are byte-identical.<br>• The W2 index gained one definitional row (E-056); no marker was removed or lowered.<br>• Case rows: only C1-13 withdrawn. No watch point named it or v34 INV-028 (checks 04, 12 and 16 mention INV-028 only for R01-06 and R12-01, both kept). |
| Check 36, wp 12 | Bookkeeping cascade after the restructuring; INV-078 Evidence | **Ended.**<br>• Round 3, R37-01: catalogue cells against their column definitions, the adjacent class that check 36 foresaw. Fix 37 swept all 9 columns of all 45 rows.<br>• Round 4, R39-01: a statement part whose only representation, a prose sentence, v35 dropped. Fix 39 audited all 1,536 Meaning, Conformance, Reading and Notes sentences of the v34 items, plus sections 1–4 and the coverage reasons, against v38, and found no other case.<br>• Review 40 found no restructuring artefact.<br>• No dedicated RATIONALE-to-model agreement audit was made. Three stale moved entries were declined by reviews 37, 39 and 40 (INV-075/D01, INV-085/D01, INV-110/S01).<br>• INV-078 Evidence is byte-identical, so the OUT-024 sentence was not re-added. |
| Check 36, wp 13 | Volume by formal blocks and rows | `omn` blocks changed: 0, 5, 2, 0 in v37–v40. Case and SD rows: 0, 1 (withdrawn), 0, 0. Remarks: 1, 3, 1, 1. Eight iterations without a NO_REMARKS main review. The check's premise ("while the remarks stay in bookkeeping") no longer holds after iteration 37. Examined below: not cycling. |
| Checks 08, 12, 16, 24: E-041 | Rule values, `excludes`, ages, timings, `ruleTr73`, `ruleRuChildren` | **Intact.** E-041 is byte-identical. The 18 SD-ER rows are byte-identical to v36, which check 36 rebuilt verbatim against v34. |
| Checks 08, 12, 16, 32: responder labels | Open kinds, `#L.evaluated = 1`, `evaluationResult`/`pretreatmentBaseline`, `rc.treatment = L.treatment`, `scopeFor`, `attackScope`, INV-116, forced "non-responder" | **Intact.** E-045, E-046 (`omn`), INV-062, INV-063, INV-064, INV-114, INV-116 and SD-RC are byte-identical, and the protected counts are unchanged. E-046 Realises lost OUT-025 (v39), which is none of these triggers. |
| Check 24, wp 4: day convention 2.8 | Course-event dates; stop bounds | **Intact.** The 2.8 block is byte-identical. `notStoppedBefore(` 5, `intervalOnTreatment(` 5, `evaluatedOnTreatment(` 3. INV-049 keeps `<`. |
| Checks 28, 32: treatment-course decisions | Unstated starts; original baseline; one stop per course; start-tied bounds | **Intact.** E-008, E-049, INV-001, INV-064, INV-067, INV-070, INV-078, INV-079, INV-103, INV-109 and INV-112 are byte-identical. INV-068 changed in Evidence only. |
| Checks 08, 12, 24: `fillsPeriod`, 28-day anchor | E-006; INV-050 start ties | **Intact.** E-006 and INV-050 are byte-identical; `fillsPeriod(` 6. |
| Checks 24, 28: `sameSpan` | By-dates relations | **Intact.** `sameSpan(` 29 → 30 (new INV-080 conjunct); none dropped. INV-049 keeps `sameSpan(v.covers, c.timeRange)`. INV-006 is byte-identical. |
| Check 32, wp 1: INV-111 to INV-117 | Identity ties | **Intact.** INV-111, INV-112, INV-114, INV-115 and INV-116 are byte-identical. INV-113 and INV-117 live in INV-123, byte-identical. `E-046.comparison` stays `opt`. |
| Check 32, wp 3: `onSameScale` / `inSameForm` | Comparability | **Intact.** 4 and 2 occurrences; INV-027, INV-039, INV-069 and INV-105 are byte-identical. |
| Checks 08, 12, 16, 24: INV-049/INV-050 ties | End tie, `fillsPeriod`, start ties; running follow-up (v11); every start (v12); `<` (v17) | **Intact, with one change in INV-049.**<br>• INV-050 and E-039 are byte-identical.<br>• INV-049 keeps the running conjunct, every start, `<` and `sameSpan`.<br>• INV-049's series tie to the selected granularity was removed in v38 (Items, row 3). |
| Checks 04, 08, 12: menstrual-relation view and INV-104 | Lead-in, start of view, `menstruatesDuring` | **Intact.** INV-086, INV-087, E-060, E-061, INV-104 and INV-105 are byte-identical. |
| Check 24, wp 3: cluster view | `ongoing`, `lastDay`, as-of bound, `remissionMoreThanMonths`, `onlyOfType` | **Intact.** E-062, E-063, INV-088 and INV-089 are byte-identical; `onlyOfType(` 6. |
| Checks 12, 16, 24: co-presence, formulation ties, INV-098, E-008 time frames, text-only ISS items, periods beyond the as-of date | — | **Intact.**<br>• INV-003, INV-074, INV-123 (`usedMedication`), C3-11, E-008, E-057 Notes, ISS-02, ISS-03 and ISS-12 are byte-identical.<br>• The v37 "stated once" paragraph describes INV-003 placement for comparison values, not for the values of a change outside a response comparison (R10b-01 kept).<br>• Scheme windows (INV-080) stay unbounded by the as-of date, which is the settled point. |

## Findings

None. No item oscillates, so no OSC finding is raised, nothing is frozen, `FROZEN_ITEMS.md` is not written and `OUTPUT_MODEL.md` is not changed.

The closest approaches are assessed in the table above:
- **INV-049 (v38)** against fixes 03 and 05 and check 08's watch point 4. It is the third change on the follow-up series, with new Stage 1 evidence, and the watched ties are intact.
- **C1-13 (v38)** against R01-06 and fix 01. The kinds are kept, and the granularity is now literally "as in INV-023".
- **E-056 and E-046 (v39)** against the v00 prose. It is a first decision; the v35 drop had not been one.
- **The catalogue (v37)** against the plan-v35 column definitions. It is a first change, and per-row restatement (option (b)) was not taken.
- **The INV-061 and INV-075 Readings (v40)** against R01-03, review 11, fix 02 item 14 and fix 01 (R01-07). The Readings were brought to predicates unchanged since v01 and v00, and the predicate alternatives were declined.

Each is one change, with a reason that the earlier decision did not consider. None has been reversed, and none restores a state that an earlier fix deliberately set.

## Trend and looping assessment

**Remark counts per iteration, 30–40:**

| Iteration | 30 | 31 | 32 | 33 | 34 | 35 | 36 | 37 | 38 | 39 | 40 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Remarks | 1 | 1 | 0 + 3 | 2 | 1 | 1 (+ 19 audit, + 5 EQ) | 3 | 1 | 3 | 1 | 1 |

- The last NO_REMARKS main review was iteration 32's. Iterations 33–40 are eight in a row with remarks.
- The mean is 1.75 per iteration for 33–36 and 1.5 for 37–40.

**Formal-block changes per version** (`omn` blocks; case and source-data rows; informative tables listed separately):

| Version | v35a | v35 | v36 | v37 | v38 | v39 | v40 |
|---|---|---|---|---|---|---|---|
| `omn` blocks changed or new | 105 (restructuring) | 1 (a brace) | 0 | 0 | 5 (E-029 comment, INV-049, INV-096, INV-118, section 4.4) | 2 (E-056, INV-080) | 0 |
| Case and SD rows | new layout | 0 | 0 | 0 | 1 (C1-13 withdrawn) | 0 | 0 |
| Catalogue rows (informative) | new | 0 | 1 | 34 | 1 | 7 | 0 |
| Traceability rows | new | 0 | 5 | 0 | 1 | 1 | 0 |
| Element, invariant and issue fields | 634 | 9 | 15 | 0 | 16 | 15 (+ 1 W2 marker row) | 2 |
| RATIONALE entries changed (new) | 432 new | 32 | 21 (2) | 0 | 12 (3) | 3 (3) | 0 |
| Model size (bytes) | 421,294 | 421,294 | 421,917 | 423,296 | 427,204 | 430,136 | 431,035 |
| `omn` text (bytes) | 128,038 | 128,038 | 128,038 | 128,038 | 128,625 | 129,129 | 129,129 |

- Over four iterations the model grew by 2.2 % and its formal text by 0.85 %. RATIONALE grew from 322,333 to 332,923 bytes.
- No special case was added. Each formal change either states a rule once (`byTypeCases`, `∃ g` in INV-096) or removes a per-case deviation (C1-13, the INV-049 tie).

**Kinds of remarks since the restructuring (iterations 36–40, 9 remarks):**

| Kind | Remarks | Defect introduced in |
|---|---|---|
| Bookkeeping and prose introduced by the rewrite | R36-01 (URLs), R36-02 (fields of trimmed invariants), R36-03 (notation prose), R37-01 (catalogue cells restating generic invariants) | v35 |
| Statement part lost in the rewrite, never formalised | R39-01 (E-056 content) | v00 (prose only); its only representation was dropped in v35 |
| Rule stated per case / infidelity | R38-01 (C1-13 = INV-028), R38-02 (INV-049, INV-096) | v00 |
| Stage 1 issue description | R38-03 (ISS-10 count) | v07 |
| Prose overclaim | R40-01 (INV-061, INV-075 Readings) | v00, v01 |
| Caused by a fix of iterations 36–39 | none | — |

**The post-restructuring cascade (watch point 12) has ended.**
- Its rounds were EQ35-02 to EQ35-05, then R36-01 to R36-03, then R37-01, then R39-01. Each was in a class adjacent to the last, and each sweep was wider than the one before.
- Fix 37 closed the catalogue class by construction (stated once). Fix 39 audited every v34 prose sentence against v38. Review 40 found no artefact of the rewrite.
- One adjacent class remains unaudited as a whole: stale moved text in RATIONALE D, S and W entries. Three instances were seen and declined.

**Old defects at a steady rate.**
- Iterations 38–40 produced 5 remarks, all on content present since v00 to v07. None was raised or declined before, and none arises from a fix.
- Each came from a reviewer applying a new lens:
  - granularity quantifiers against the generic rule;
  - whether each view's Stage 1 content is formal;
  - Readings against predicates.
- Each fixer's class sweep then found the class to have only the members raised:
  - fix 38: INV-049 and INV-096 are the only unrestricted `tiles(…, c.granularity)`, and C1-13 the only joint case;
  - fix 39: E-056 is the only view without formal content;
  - fix 40: two Readings.
- Fixes 37 to 40 generated no follow-up remark. Reviews 38, 39 and 40 each checked the previous change and found it sound.
- This is the pattern of a tail driven by the size of the model: 67 elements, 87 invariants, 174 table rows and 440 RATIONALE entries. Each fresh reviewer finds roughly one untried lens and one old defect.

**Judgement.**
- **No looping in content.** Since iteration 33, no change has reversed a fix, and no remark has argued for an earlier state. The cascades of the earlier checks have not resumed: treatment courses, truth of a shown fact, comparability, value sets and restructuring bookkeeping.
- **Converging in direction.**
  - The v38 widenings and v35's CHG-03 and CHG-04 all remove requirements that Stage 1 does not make. The narrowings of v32–v33 and v39 add ties that Stage 1 or the element's definition supports.
  - No admitted set has re-widened and none has re-narrowed.
- **Not converged in rate.**
  - About 1.5 remarks per iteration and eight iterations without a NO_REMARKS main review. Convergence needs three NO_REMARKS reviews in a row.
  - At the current rate this is not in sight before the 64-iteration limit. The limiting factor is the number of review lenses not yet applied to a large model, not fix-induced churn.
  - A one-off audit along the lenses not yet swept would shorten the tail more than remark-by-remark fixing. Examples: RATIONALE D, S and W entries against the model, and element Meanings that describe roles (listed by fix 40). Whether to order one is a matter for the orchestrator or the human.

## Watch points for the next check

1. **INV-049 and the follow-up series** (v38).
   - **Oscillation, to be frozen:** re-adding a tie of the follow-up series to the selected granularity (`tiles(…, c.granularity)`). That would be A → B → A.
   - **A fourth change on check 08's watch point 4, also oscillation unless it rests on evidence beyond R38-02, fix 38 and fixes 03 and 05:** changing E-039 `series` or its `when` clause, or INV-050 (start tie, `fillsPeriod`), on R38-02's granularity ground. An example is removing E-039's weekly series in follow-up views of 7 to 27 days, which review 39 checked and did not raise, and which INV-049/D02 states.
   - **Reversal of R11-03 and fix 12 in substance:** applying `∃ g` to INV-049 (fix 38 declined it).
   - **INV-096:** returning to every granularity is A → B → A; the v12 age reading must stay.
2. **`byTypeCases` and INV-118** (v38).
   - **A → B → A:** re-adding a joint per-type view, or monthly acute-medication days per type (the C1-13 form).
   - **Reversals:**
     - dropping the per-class or per-drug kinds per type (R01-06);
     - one shared `∃ g` for a case and its per-type instance, or across measures (INV-118/D03, D04).
   - **New decisions needing Stage 1 evidence, not reversals:** migraine days per type (INV-118/D02; review 14), or the weekly view and the overuse indicator per type (ISS-09).
3. **The catalogue** (v37).
   - **A → B → A:** re-adding per-row restatements of the seven invariants that section 4.2 states once (R37-01 option (b)).
   - A remark on a catalogue cell should be fixed under the 4.2 column definitions. A fix that re-adds "label", "completeness", INV-121, INV-122 or INV-123 per row is the reversal.
4. **E-056 and INV-080** (v39).
   - **A → B → A:** responder labels as content of the scheme-window view, or OUT-025 back in E-046 Realises (E-056/X01 (3)).
   - **New decisions against E-056/D02:** date ties of instrument results or treatment lines to windows, or `within` in place of `sameSpan` (X01 (1), (2)). They would carry scheme criteria into the model (OUT-025 Caveats).
   - ISS-04 now also decides OUT-025's frequency outputs. A change of the four kinds without the human's ISS-04 decision would be a silent deviation.
5. **The INV-061 and INV-075 Readings** (v40).
   - **A → B → A:** restoring "for one calendar month or 28-day period" or "only when it shows a drug-related adverse event".
   - **New decisions that fix 40 declined with reasons; they need Stage 1 evidence:**
     - a shared month for the two residual counts (`sameSpan`);
     - a definitional presence tie of adverse events to a shown result. That tie would also contradict CHG-04's principle (watch point 7).
   - The element Meanings that describe roles (E-013, E-042, E-044, E-046, E-047, E-059) were judged outside R40-01's class by fix 40. A remark that raises them contests that judgement.
6. **ISS-10.** Restoring the v06 scope ("that OUT-018 quotes for these time points") would reverse fix 07 (R07-01). The count must stay at five while the scope is "Stage 1 cites".
7. **Check 36, watch points 1 to 11, carried forward unchanged**, all intact in v40:
   - INV-060 antecedent and ISS-13;
   - CHG-04 (INV-031);
   - the class of INV-123;
   - INV-124;
   - CHG-06 and CHG-07;
   - the E-049 `when` clause;
   - `reviewWindow` without `when`;
   - the INV-105 Reading lead-in;
   - source-data cells as axioms;
   - the v33 comparability and value-set conjuncts;
   - the earlier triggers at their v35 places.
8. **Bookkeeping, the remaining adjacent class.**
   - Stale moved text in RATIONALE: INV-075/D01, INV-085/D01 and INV-110/S01, declined in reviews 37, 39 and 40. The seven Definitional cross-link asymmetries were examined by fix 36 and not raised by reviews 37 and 40. Review 39 did not raise the E-015, E-017 and E-019 Conformance fields, which do not name their `byTypeCases` instances.
   - A remark there would continue the post-restructuring cascade (a fifth round). It needs new evidence against those declines.
   - INV-078 Evidence: re-adding the OUT-024 formulation sentence would complete A → B → A → B.
9. **Rate and source of remarks.**
   - Count, per iteration, the remarks whose defect a fix introduced, against those present since v00 to v07.
   - **A fix-induced remark is the first sign of a new cascade.** Candidate sources are `byTypeCases`, the INV-080 conjunct, the 4.2 "stated once" paragraph and the v40 Readings.
   - **A further iteration of old-defect remarks at about one per iteration confirms a size-driven tail,** not oscillation. Report it as a convergence-rate question for the human.
   - Count `omn` changes and case and source-data rows, as here. Expect 0–few.

The scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/osc40/`:
- `versions.py`, `split.py`, `analyse.py`, `hist.py`, `fld.py`, `omndiff.py`, `wdiff.py`, `nearret.py`, `guar.py`, `levels.py`, `volume.py`;
- `linehist.py`, `ngram40.py`, `cells.py`, `ratsplit.py`, `blocks40.py`.

`FROZEN_ITEMS.md` was not written, and `OUTPUT_MODEL.md`, `RATIONALE.md` and the history snapshots were not changed.
