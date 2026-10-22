# Oscillation check — after iteration 28
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: versions v00 to v28 (history/v00.md to history/v28.md; OUTPUT_MODEL.md is byte-identical to v28); reviews review-iter-01 to review-iter-28 with the re-checks 08b, 10b, 19b, 19c, 21b, 22b and 25b (35 files, 73 remarks; iterations 25–28: 0 + 1, 1, 1 and 2); fixes fix-iter-01 to fix-iter-28; the earlier oscillation checks after iterations 04, 08, 12, 16 and 24, with all ten watch points of check-after-iter-24.md. Read in full: check-after-iter-24.md, review 25, and fixes 25 to 28. Read in full except their source-download and quote tables: re-check 25b and reviews 26, 27 and 28 (summary, remarks, "Checked and not raised"). Earlier passages read for the items that changed in v25–v28: review 15 ("Several stop events in one course"), fix 02 item 5, fix 05 (the INV-064 start tie), fix 10 (the INV-103 Reading), fix 14 (R14-02), fix 16, fix 18 (INV-070 row), and the watch points of the checks after iterations 08, 12 and 16. Every snapshot was split by script, and every item of the treatment-course cluster was read in each of its states.
Date: 2026-10-22

## Method

1. **Git history.**
   - Checks:
     - each of v25 to v28 was added in exactly one commit and never changed afterwards (v25 bbd0562, v26 5624f52, v27 3fd47c2, v28 c541f8a);
     - at each of these fix commits, OUTPUT_MODEL.md is byte-identical to that commit's snapshot;
     - the committed snapshots v00 to v28 equal the working-tree snapshots;
     - from 9340190 (check 24) to c541f8a (fix 28), every review, re-check and fix log was added in its own commit, in loop order: review 25 (d6cd400), re-check 25b (02d8768), fix 25, review 26 (62ef926), fix 26, review 27 (a2a0a10), fix 27, review 28 (9b0bfc9), fix 28;
     - each fix commit touches only OUTPUT_MODEL.md, its snapshot and its fix log, and each review commit touches only its review;
     - Stage 1 is unchanged since bfec74f.
   - All checks passed. The working tree was clean, OUTPUT_MODEL.md equals v28, FROZEN_ITEMS.md does not exist, and no snapshot carries a FROZEN marker.
2. **Item split** (`split.py`). The same item granularity as the checks after iterations 12, 16 and 24, extended to 29 versions. It gives 2,503 distinct items:
   - the header, the sections and subsections;
   - every element, invariant and Stage 1 issue, and each of their fields;
   - every attribute and declaration of the `omn` blocks;
   - the traceability rows with their columns, the source rows, the withdrawn row, the search-log lines and the change-log paragraphs.

   The splitter attaches a comment line to the declaration before it. So when a declaration is inserted, comment lines move between items. The resulting apparent changes of `startOf` (v26, v28) and `resumesFrom` (v27) were checked by hand: their bodies are byte-identical.
3. **State trajectories** (`analyse.py`, `cluster.py`). Each item was hashed per version. The script flags every item that returns to the state of a non-adjacent earlier version after a different state in between (A → B → A, including add → remove → add).
4. **Formal blocks** (`omn.py`, `omntraj.py`, `omndiff.py`, `hist.py`).
   - The same trajectory test was run on every `omn` block with comments removed.
   - Every block changed in v25–v28 was diffed line by line.
   - Every distinct state since v00 of each changed predicate was printed and read: INV-001, INV-064, INV-067, INV-068, INV-070, INV-078, INV-079, INV-102, INV-103, INV-109, the E-008 declarations, and the E-049 `baseline` and `onTreatmentPeriod` attributes.
5. **Near-return detector** (`nearret.py`). For every change from vᵢ₋₁ to vᵢ, with i from 25 to 28, the script tests whether vᵢ is closer by word-level similarity to some earlier state vⱼ (j < i − 1) than to vᵢ₋₁.
6. **Word-level diffs** (`wdiff.py`, `dels.py`).
   - Every item changed in v25–v28 was classified as new, additive (no word deleted or replaced) or edited.
   - Every deleted span of four or more words was listed and read.
   - The text fields of the treatment-course cluster were diffed version by version from v24.
7. **Insert/delete n-grams** (`ngram.py`, `docwide.py`). Per item, and over sections 1–9 as a whole, the scripts compare 6-word n-grams:
   - deleted at some vⱼ and re-inserted in v25–v28;
   - inserted at some vⱼ and deleted in v25–v28.
8. **Conformance** (`conf.py`). Tracked across all 29 versions:
   - every invariant's level;
   - every attribute declaration (level, `when` clause, `derived` mark);
   - the level-keyword counts of every element Conformance field.
9. **Guarantee terms** (`guar.py`). The occurrences in the formal blocks of v08 to v28 of 36 terms:
   - the ties protected by the earlier watch points, for example `notStoppedBefore(`, `intervalOnTreatment(`, `evaluatedOnTreatment(`, `firstChangedDay(`, `next(p.end)`, `sameSpan(`, `sameIndicatedPeriod(`, `summarisesMedication(`, `courseOverlaps(`, `courseNotOutside(`, `onlyOfType(`, the remission bound, `(∀ e ∈ x.end • e ≤ ctx.asOf)`, `#L.evaluated = 1`, `(m.period = n.period ⇒ m = n)`, the 28-day anchor of `fillsPeriod`, `rc.treatmentStart ∈ startOf`, `labelledAs(`, `conditionHolds(` and `otherValueNamed(`;
   - the ties of v25–v28 (the one-stop and dose-order conjuncts, `resumes`, `resumesFrom(`, `originalStart(`, `p.2 ≠ u`, `∃ s ∈ originalStart`, `courseBegunBy(`, the INV-068 `∃ s` form);
   - the start-tied forms that v28 replaced (`startOf(c, e.treatment) ≠ ∅`, `∀ s ∈ startOf(`).

   In addition, the 49 `omn` blocks named in the watch points of the checks after iterations 16 and 24 were compared between v24 and v28.
10. **Semantic scenarios** (`course.py`).
    - Each treatment-course predicate was transcribed in every form it has had since v00: the INV-070 baseline conjunct (v00–v25, v26, v27–v28); the INV-070 on-treatment conjunct (v00–v16, v17–v27, v28); whether the on-treatment period is asked for (v00–v01, v02–v16, v17–v27, v28); INV-103 (v00–v27, v28); INV-068 (v00–v17, v18–v27, v28); INV-064 (v00–v04, v05–v17, v18–v27, v28); INV-067, INV-079 and INV-078 (v00–v27, v28); INV-109 (v11–v13, v14–v27, v28); and both forms of `originalStart`.
    - For nine contexts, the script lists per version what each item admits or requires: the calendar months January 2024 to October 2026 as baseline, on-treatment, control-level or adherence months, the required views, and the asks. It then flags every item whose set returns to an earlier set.
    - The nine contexts:
      - a course with a stated start (A);
      - review 27's example B (a first course without a stated start, resumed);
      - the R26-01 example (C);
      - a three-course chain without (D) and with (E) the first start;
      - an unlinked new trial of the same drug (F);
      - a stop and a reduction on the start day (G);
      - an acute course without a stated start, for INV-109 (H);
      - INV-078 groups with a line without a start date (I).
11. **Remark topics** (`remarks.py`).
    - The `Item(s)` of all 73 remarks were mapped to E-, INV-, ISS- and OUT- IDs, and for each remark of iterations 25–28 the earlier remarks on the same IDs were listed.
    - Every sentence of those remarks that uses revert, undo, reverse, restore, remove, drop, loosen, relax, weaken, re-raise or reopen was listed.
    - The "Checked and not raised" lists of reviews 25 to 28 were compared with earlier ones and with what fixes 25 to 28 then changed.
12. **Bookkeeping** (`book.py`). Change-log paragraphs, source rows, the withdrawn row, the ISS items, the search log, sections 1, 3 and 4, and the notation subsections, v25–v28.
13. **Judgement.** Each item that changed in two or more versions, at least once in v25–v28, was read against the remark or fixer change that drove each change. It was then classified as convergent (one direction, earlier guarantees kept) or oscillating (back and forth on the same point).

**Results of the mechanical steps**

- **Step 3.**
  - 1,049 items changed at least once, and 442 in two or more versions.
  - One item returns to a non-adjacent earlier state: `E-008.attr.SubjectProfile.aged12OrOlder`, added in v06 and removed in v12. The iteration-12 check assessed it. Nothing new in v25–v28.
  - No item was removed after v12, and no removed item was re-added.
  - 60 leaf items changed in two or more versions with at least one change in v25–v28. They fall into the four topics of the next section.
- **Step 4.**
  - No `omn` block, with comments removed, returns to an earlier state in v00–v28.
  - Blocks changed per version: v25 1 (INV-001); v26 4 (E-008, INV-001, INV-070, and E-049 in a comment only); v27 3 (E-008, E-049, INV-070); v28 9 (E-008, INV-064, INV-067, INV-068, INV-070, INV-078, INV-079, INV-103, INV-109).
  - Each changed line was read. Every condition replaced in v25–v28 is replaced by a form that gives the same verdict wherever the context states the start, or that is stricter. The one exception is INV-103 (Findings, A).
- **Step 5.** 147 changes were examined; there are 2 hits, INV-103 and its Reading. The v28 Reading ("After each stop, pause or dose reduction of a preventive treatment, whether or not the context states the start of its course, …") is closer to the v00 Reading than to the v10–v27 Reading ("… of a preventive treatment that has started, …"). Assessed in Findings, A.
- **Step 6.**
  - **Change types** (leaf items, without sections, logs and aggregates):
    - v25: 10 edited, 9 additive;
    - v26: 10 edited, 11 additive, 3 new;
    - v27: 11 edited, 7 additive;
    - v28: 36 edited, 16 additive, 3 new.
  - **Deleted spans of four or more words:**
    - **v26 (3).** INV-001 Notes and row OUT-022: "may compare with the original baseline" becomes a requirement for post-stop monitoring.
    - **v27 (11).** The `originalStart` fallback in E-008 (Definition, comment and Notes) and its mention in the INV-001 Notes; three INV-070 Notes phrases reworded with the same content ("so this bound implies the bound by that start" → "because the original start is not after it").
    - **v28 (19, of which 6 are duplicates of the Predicate/misc pair and 1 is a comment artefact).** These are:
      - the replaced start ties of INV-064, INV-067, INV-070 and INV-068;
      - the INV-103 conjunct and Reading;
      - "where the treatment has a start" in the E-051, E-055 and INV-109 texts and in row OUT-024;
      - the INV-064 Notes "the start tie then constrains nothing" (written in v05) and the INV-109 Notes "the period of its summary is not constrained" (written in v14);
      - two E-049 Notes phrases written in v27: "and whose view INV-103 does not require" and "(the on-treatment period here; INV-055, INV-056, INV-102, INV-103; …)".

      Each is replaced by text matching the new predicate (Findings, A and C).
- **Step 7.**
  - **Re-insertions.** 5 hits within items. Four are artefacts:
    - E-049 Conformance ("period SHOULD be shown whenever the"): a v17 insertion split again in v28;
    - E-049 Notes ("last day of the course, and");
    - row OUT-024, twice ("the treatment has a start, and"): list punctuation.

    One is real: INV-103 Reading, "dose reduction of a preventive treatment," deleted in v10 and re-inserted in v28 (Findings, A).

    Document-wide, 8 n-grams were deleted earlier and re-inserted in v25–v28. They are the same artefacts, a generic phrase, and a field boundary ("Evidence: Stage 1 OUT-022. - Notes:", the new INV-103 Notes field).
  - **Insert-then-delete.** 115 hits with the deletion in v25–v28. The formal hits are:
    - INV-001 (v02 → v25, v25 → v26): bracket boundaries of extended conjuncts;
    - INV-064 (v05, v18 → v28), INV-070 (v17 → v28, v26 → v27), INV-109 (v14, v15 → v28) and INV-079 (v02 → v28): the replaced start ties;
    - `originalStart` (v26 → v27): the fallback.

    None removes a condition that an earlier fix inserted without putting back a form that gives the same verdict wherever the start is stated (step 10). The text hits are sentences of an earlier fix that a later fix extended within the sentence. The one substantive reversal of an earlier sentence is the v27 E-049 Notes claim about INV-103 (Findings, A).
- **Step 8.**
  - No invariant level has ever changed. v28 totals: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34, the same as in v24.
  - No attribute level or `when` clause returned to an earlier state. The only attribute change in v25–v28 is E-049 `baseline`, which gains `when originalStart(ctx, self.treatment) ≠ ∅` in v27, its first change since v00.
  - No element Conformance keyword count dropped or returned.
- **Step 9.**
  - Every protected tie occurs as often in v28 as in v24, for example `notStoppedBefore(` 5, `intervalOnTreatment(` 5, `evaluatedOnTreatment(` 3, `firstChangedDay(` 3, `sameSpan(` 30, `sameIndicatedPeriod(` 6, `summarisesMedication(` 10, `courseNotOutside(` 3 and `onlyOfType(` 6. These are formal-text counts; the fix logs count prose too.
  - The new ties keep their counts after their version: the one-stop and dose-order conjuncts (1 from v25), `resumes` 7 from v26, `originalStart(` 3 from v27 and `∃ s ∈ originalStart` 1 from v27.
  - The drops are exactly the targeted removals:
    - `resumesFrom(` 3 → 2 in v27 (the fallback's second use);
    - `startOf(c, e.treatment) ≠ ∅` 1 → 0 in v28 (INV-103);
    - `∀ s ∈ startOf(` 4 → 1 in v28 (INV-064, INV-067 and INV-068, replaced by `courseBegunBy` or `∃ s`).
  - `a ≤ e.date` (R18-01's dropped sketch) is absent, and INV-049 keeps `<`.
  - All 49 watch-point blocks of the checks after iterations 16 and 24 are byte-identical in v24 and v28: E-006, E-014, E-032, E-041 to E-047, E-051, E-055, E-062, E-063, E-067, INV-003, INV-006, INV-008, INV-012, INV-024, INV-030, INV-031, INV-033, INV-038, INV-046, INV-049, INV-050, INV-053 to INV-056, INV-058, INV-059, INV-062, INV-063, INV-066, INV-069, INV-071, INV-072, INV-074, INV-075, INV-086 to INV-089, INV-098, INV-102, INV-104, INV-105 and INV-111.
- **Step 10.**
  - **Nesting.** In every context, every admitted set of v25–v28 is nested in the set of the version before it. A set widens in only one place, the known v17 day-convention widening of the on-treatment months; nothing widens in v25–v28. The required views of INV-103 grow in v28, for courses without a stated start.
  - **Stated starts.** Wherever the context states the start, every v28 verdict equals the v27 verdict (contexts A, C, E, F and G, every item).
  - **Two point-level returns.** Both concern whether the on-treatment period is asked for:
    - **For a stop or pause of a course whose start the context does not state** (contexts B and D): asked in v00–v01, not asked in v02–v27, asked in v28. Findings, A.
    - **For a stop on the start day** (context G): asked in v00–v01, not asked in v02–v16, asked from v17. This is Findings B of the iteration-24 check, unchanged since.
  - **The original baseline** for the view of a resumed course whose first course has no stated start: 32 months (v00–v25), 32 or 23 (v26), 0 (v27–v28). It never widens. Findings, B.
- **Step 11.** See "Recurring remark topics".
  - Every remark of iterations 25–28 states that it reverses no fix. The flagged words are "No reversal", "does not reverse", and R28-01's "Remove the conjunct `startOf(c, e.treatment) ≠ ∅`" (Findings, A).
  - No earlier remark named in their items is undone: R02-03, R02-05, R03-05, R12-01, R14-02, R15-02, R17-01, R18-01 and R20-01 were each checked against the v28 predicates.
  - No remark that a fixer declined was raised again.
- **Step 12.**
  - The change log is append-only (29 paragraphs, none changed after its version).
  - S-101 to S-106 are unchanged since v08; no source was added in v25–v28.
  - The withdrawn row and every ISS item are unchanged in v25–v28, and the search log is append-only (4 lines added).
  - Section 9 changed only in "as of vNN". Sections 1, 3 and 4 are unchanged. Of the notation, only section 2.8 changed, in v25, and only additively (Findings, D).

## Change history of items changed in two or more versions

Listed: items that changed in two or more versions, at least once in v25–v28. Items whose changes all lie in v00–v24 and that are unchanged since were assessed in the earlier checks (last row).

| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| **One stop per course; a restart is a new course.**<br>**INV-001**:<br>• Predicate (v01, v02, v06, v11, v12, v25, v26);<br>• Reading (v01 … v12, v25, v26);<br>• Realises and Evidence (v25 and earlier);<br>• Notes (v02 … v12, v25, v26, v27).<br>Section **2.8** (v01, v17, v25).<br>**E-008**: Meaning (v06, v07, v12, v17, v25 …); Evidence (v06, v12, v25, v26); Notes (v01 … v13, v25 …).<br>Notes of **E-049** (v02, v17, v25 …), **INV-068** (v18, v25, v28), **INV-079** (v02, v17, v25, v28) and **INV-097** (v03 … v18, v25, v27, v28).<br>Rows **OUT-022** and **OUT-024** (v25 and earlier) | v25 (and earlier, on other conjuncts) | **v25 (R25b-01, option (a)).**<br>• INV-001: at most one stop or pause per course (added to the one-start conjunct), and no dose change or target-dose date after the stop.<br>• Section 2.8 and E-008: a resumed treatment is a new course with its own start. No course-event date changed.<br>• INV-068 and INV-097 Notes: "its first stop or pause" → "its stop or pause". | Review 15 (not raised; listed as settled in check 16); R25b-01 | **Convergent** (Findings, D).<br>• Additive conjuncts in INV-001. The earlier INV-001 conjuncts are verbatim, and so is the iteration-08 fallback type.<br>• Section 2.8 gained two clauses, and its dates are verbatim (watch point 4).<br>• "A restart is a new course" was already fix 11's reading of INV-001 (one start per course). |
| **Original pre-treatment baseline of a resumed course.**<br>**E-008**:<br>• Definition: new `resumes`, `resumesFrom` and `originalStart` (v26); `originalStart` body (v27);<br>• Meaning and Notes (v26, v27).<br>**INV-001**: the `resumes` conjuncts (v26); Notes (v26, v27).<br>**INV-070**:<br>• the baseline conjunct: `∀ b; s ∈ startOf` (v00–v25), `∀ b; s ∈ originalStart` (v26), `∀ b • ∃ s ∈ originalStart` (v27);<br>• Reading and Notes (v17, v26, v27, v28); Evidence (v26).<br>**E-049**:<br>• `baseline`: comment (v26), `when` clause (v27);<br>• Meaning (v17, v26, v27); Conformance (v02, v03, v12, v17, v26, v27, v28); Notes (v26, v27).<br>**INV-097** Notes (v27); row **OUT-022** (v26, v27) | v26, v27 | **v26 (R26-01, option (a)).**<br>• The context link `resumes`, with INV-001 conjuncts: same drug, both preventive, the restart after the stop, one predecessor and one successor.<br>• `originalStart` is the earliest start that the context states in the chain (a fallback where the first course states none).<br>• INV-070 bounds the post-stop baseline by it.<br>**v27 (R27-01, option (b)).**<br>• `originalStart` is the start of the first course of the chain only, ∅ where the context states none.<br>• E-049 asks for a baseline only where it is not empty, and INV-070 admits none otherwise.<br>• Extended by the fixer to every course without a stated original start. | R26-01; R27-01 | **Convergent** (Findings, B).<br>• The admitted baselines are nested v25 ⊇ v26 ⊇ v27 = v28 in every context.<br>• The fallback was the fixer's own addition: R26-01's required change defined the original start as "the start of the first course of its chain of resumptions", without one. v27 is that definition.<br>• `resumes`, `resumesFrom` and the INV-001 conjuncts are verbatim from v26 to v28. |
| **Courses whose start the context does not state: post-stop view and treatment review view.**<br>**INV-103**:<br>• Predicate (v28; unchanged since v00 before that);<br>• Reading (v10, v28); Notes (new in v28).<br>**INV-070**:<br>• the on-treatment conjunct: `∀ q; s ∈ startOf • s ≤ q.start ∧ q.end < v.eventDate` (v00–v16), `… < x` (v17–v27), `courseBegunBy(…, q.start) ∧ q.end < x` (v28);<br>• new presence conjunct (v28).<br>**E-049** Conformance and Notes (v28).<br>**E-008**: new `courseBegunBy`, and Meaning and Notes (v28).<br>**INV-068**: the start conjunct `∀ s` (v00–v27) → `∃ s` (v28); Predicate also v02 and v18 on other conjuncts; Reading (v02, v10, v18, v28); Notes (v18, v25, v28).<br>**E-048** Conformance (v02, v03, v12, v28) and Notes (v18, v28).<br>**INV-097** Notes (v28); rows **OUT-021** and **OUT-022** (v28 and earlier) | v28 (and v10 for the INV-103 Reading) | **v28 (R28-01).**<br>• INV-103 requires the post-stop view whether or not the start is stated.<br>• The on-treatment period begins on or after a dated course event (`courseBegunBy`) and ends before the first changed day.<br>• It is asked for where the start is not stated and a course event is dated before the changed regimen. The E-049 `when` clauses are byte-identical.<br>**v28 (R28-02).** INV-068's start conjunct becomes existential, so no treatment review view is admitted without a stated start. | Fix 02 item 5 (side effect); fix 10 (Reading only); review 27 (not raised); fix 27 (precedent); R28-01; R28-02 | **Convergent, the closest approach of this window** (Findings, A).<br>• Every predicate changed once.<br>• Wherever the start is stated, every verdict is unchanged.<br>• At the level of one point, the on-treatment ask for such a course went T (v00–v01) → F (v02–v27) → T (v28). The v28 state did not exist before: it is asked only where a day on the course is placed, and the period is bounded.<br>• Fix 27 had cited INV-103 and the `when` clause as start-aligned content, and fix 28 reclassified both as aligned to the event. |
| **Start-tied bounds: the fixer's sweep.**<br>**INV-064**: Predicate, Reading and Notes (v05, v18, v28).<br>**INV-067** (v28, its first change).<br>**INV-078**: Predicate, Reading and Notes (v11, v28).<br>**INV-079**: Predicate and Reading (v02, v17, v28).<br>**INV-109**: Predicate, Reading and Notes (v11, v13, v14, v15, v28).<br>Notes of **E-046** (… v18, v24, v28), **E-047** (v15, v28) and **E-055** (v02, v11, v17, v28).<br>Conformance of **E-051** (v01 … v16, v28) and **E-055** (v02 … v15, v28).<br>Rows **OUT-020** and **OUT-024** (v28 and earlier) | v28 (and earlier) | **v28 (fix 28's start-tied-bounds table, 46 rows, 8 changed; five items not raised by review 28).**<br>• INV-064 and INV-067: `∀ s ∈ startOf • s ≤ …` → `courseBegunBy(…)`.<br>• INV-078: chronological order over every pair of lines, not only neighbours.<br>• INV-079: no duration where the start is not stated.<br>• INV-109: the end ties of an acute line's summary hold whatever the start, and the summary begins on or before every dated course event. | Fix 05; R14-02 with fix 14; R15-02; R17-02; R18-01 (earlier); fix 28 | **Convergent** (Findings, C).<br>• Each change gives the v27 verdict wherever the start is stated, and is stricter where it is not.<br>• The ties of fix 05 (INV-064), fix 14 (INV-109), R15-02 (adherence window), R17-02 (formulations), the INV-078 co-presence conjuncts and `notStoppedBefore` are verbatim, or replaced by an equivalent.<br>• The two deleted Notes sentences only described the vacuity of v05 and v14; no remark or fix had argued for it. |
| Header; sections 9, 11 and 12 | every version | Version line, "as of vNN", one search-log paragraph and one change-log paragraph per version. | — | Bookkeeping, not applicable. |
| Items whose changes all lie in v00–v24 and that are unchanged since. Examples: the 49 watch-point blocks of step 9, among them the v24 by-dates relations, INV-111, the cluster view, `fillsPeriod`, E-041, E-042, E-046 and INV-105 with E-067; the E-049 `onTreatmentPeriod` attribute (v17); the ISS items | within v00–v24 | See check-after-iter-04, -08, -12, -16 and -24. | as there | Convergent (earlier checks). Unchanged in v25–v28. |

## Recurring remark topics

| Topic (IDs) | Remarks | Pattern | Assessment |
|---|---|---|---|
| **Treatment-course semantics: stops, restarts, the original baseline, unstated starts** (INV-001, E-008, E-049, INV-070, INV-103; INV-068, E-048; OUT-021, OUT-022, OUT-024) | R25b-01, R26-01, R27-01, R28-01, R28-02. Earlier on the same items: review 15 (not raised), R17-01, R18-01, R02-05, R02-03 | **A cascade.** Each remark is a consequence of the previous fix:<br>• several stops → one stop per course, and a restart is a new course (v25);<br>• the original baseline of a restarted course → `resumes` and `originalStart` (v26);<br>• a chain whose first start is not stated → no fallback, no baseline (v27);<br>• the neighbouring items for unstated starts → INV-103, the INV-070 on-treatment bound, INV-068, and the fixer's sweep (v28).<br>Each remark names a different case. Each fix kept the previous fixes' formal text verbatim: the v25 INV-001 conjuncts in v26–v28; `resumes` and `resumesFrom` in v27–v28; `originalStart` and the E-049 `omn` block in v28. | **Converging, not exhausted.** Five remarks in four iterations on one cluster. None asks to undo an earlier fix, and no admitted set widens (step 10). The one competing pair of positions, on the alignment of the post-stop view (fix 27 against fix 28), changed one item once (Findings, A). |
| **"Not raised" points later raised** | Review 15 → R25b-01; review 27 → R28-01 and R28-02; review 28 (INV-064, INV-067, INV-109) → fix 28 | **The reasons given for raising them:**<br>• R25b-01 brought new evidence: the v17 day convention and the v18 stop bounds made the earliest stop the end of the course in part of the model only.<br>• R28-01 and R28-02 cite fix 27's change of the unstated-start treatment as new.<br>• **Inside iteration 28,** fix 28 rejected review 28's reason for not raising INV-064, INV-067 and INV-109 ("a SHOULD invariant already needs a response comparison"). It found that the definitional INV-064 and INV-067 admitted wrong months and windows, and that INV-109's acute summary needs no comparison. | **One direction** (each time a constraint is added, never loosened). A threshold shift between reviewers, of the kind the iteration-24 check noted for R19c-01. Not a cycle, because no later remark argues that the earlier "not raised" state was right. |
| **Text that claims more than the predicate** (E-049 Notes, INV-070 Notes, INV-068 Reading, E-048 Notes, INV-103 Reading) | R27-01, R28-01, R28-02 | Each found a Notes or Reading sentence written to describe the intended semantics (fixes 26 and 18), and the predicate was brought up to it. In v28 one sentence went the other way: fix 27's E-049 claim about INV-103 was deleted because the predicate changed (Findings, A). | Not on an item aligned in v22–v24, so not the cycling of iteration-24 watch point 9. |
| **Topics of the earlier checks:** by-dates relations, INV-111, the cluster view, `fillsPeriod`, formulation ties, text-only ISS items | none in 25–28 | Reviews 25 to 28 list them as settled and not reopened. Review 25 and re-checks 25b and 26 noted output-wide agreement of counts as a new decision, not a defect (watch point 1 of check 24). | Stable. |

**Settled points.** Reviews 25 to 28 list these as "not reopened (no new evidence)", and every item behind them is byte-identical in v25–v28:
- INV-106 at MUST NOT; the "> 3 months" readings of INV-045 and INV-089; INV-023 at any granularity; INV-027 tied to preventive treatments;
- the E-041 readings, timings, ages and `excludes`;
- the HIT-6 one-month recall; HADS subscales only; the MIDAS labels and Grade IV undivided; "baseline administration"; the HALT-90 total;
- INV-060 with INV-061 for short compared periods; `mostRecent` with 28-day periods; comparison periods beyond the as-of date;
- empty `remissions` in chronic cluster headache (ISS-12); "history of previous bouts"; the 24-hour outcomes of 15-minute summaries;
- E-039 `reviewWindow`; the CycleLine lead-in; the INV-031 marks conjunct;
- the `concerns` reading of all-types indices; 𝔹-valued given functions; the E-060 lead-in;
- the baseline month not tied to the month before the start (review 02);
- new in iterations 25–28:
  - output-wide agreement of counts across views (a new decision, watch point 1);
  - INV-111 excluding two labelled definitions in one view;
  - the INV-012 rounding side effect;
  - the M-TOQ, PGIC and MSQ categories (review 19b);
  - the acute part of optimal control (review 03);
  - IHS 2024 Q5 as a stop rule;
  - the INV-046 "two directions agree" Notes;
  - the ISS-09 Group D wording and the ISS-03 "by its ID" wording;
  - the two illustrative paraphrases in sections 1 and 3.3.

**Remark counts per iteration:** 12, 7, 7, 4, 3, 1, 3, 0 + 2, 1, 0 + 2, 3, 2, 3, 2, 3, 1, 3, 1, 0 + 0 + 2, 1, 0 + 1, 0 + 1, 1, 2, **0 + 1, 1, 1, 2**.

## Convergence assessment

**Numbers, v25–v28** (v17–v24 from the iteration-24 check, reproduced exactly by this check's splitter):

| Version | v17 | v18 | v19 | v20 | v21 | v22 | v23 | v24 | **v25** | **v26** | **v27** | **v28** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Remarks of the iteration | 3 | 1 | 0 + 0 + 2 | 1 | 0 + 1 | 0 + 1 | 1 | 2 | **0 + 1** | **1** | **1** | **2** |
| Items changed (iteration-12/16/24 granularity) | 96 | 74 | 18 | 39 | 31 | 30 | 25 | 122 | **39** | **41** | **36** | **84** |
| Top-level elements, invariants and issues | 18 | 12 | 2 | 7 | 4 | 4 | 3 | 25 | **6** | **4** | **5** | **16** |
| Traceability rows | 4 | 3 | 0 | 3 | 1 | 2 | 1 | 6 | **2** | **1** | **1** | **4** |
| Invariant predicates / element definitions | 5 / 4 | 6 / 3 | 0 / 0 | 0 / 0 | 0 / 0 | 0 / 1 | 1 / 1 | 9 / 3 | **1 / 0** | **2 / 2** | **1 / 2** | **8 / 1** |
| Formal (`omn`) blocks changed | 9 | 9 | 0 | 0 | 0 | 1 | 2 | 12 | **1** | **4** (1 comment only) | **3** | **9** |

The content items that fixes 25 to 28 list (9, 5, 6 and 20) agree with these counts. The rest of each count is bookkeeping, the sections that contain the changed items, and the split of each changed field.

**Reading.**
- **Volume.**
  - After the v24 peak (122 items, 12 blocks), v25–v27 returned to the level of v20–v23 (36–41 items, 1–4 blocks).
  - v28 rose again, to 84 items and 9 blocks, the largest change since v24. Of its 9 blocks, 4 address R28-01 and R28-02. The other 5 come from the fixer's start-tied-bounds sweep, on items that review 28 had set aside.
- **Remarks.**
  - The remark rate has not fallen: 0 + 1, 1, 1, 2.
  - Review 25 returned NO_REMARKS, and every later review found at least one remark. The loop has still not had three NO_REMARKS in a row.
  - All five remarks of iterations 25–28 concern one cluster, the treatment course (stops, restarts, the original baseline, unstated starts). Every other area of the model is byte-identical since v24.
- **Cascade or cycle.**
  - **The case for a converging cascade.** Each remark found a case that the previous fix created or left open: several stops → restart → original start → unstated first start → unstated start in neighbouring items. Each fix moved in one direction:
    - it narrowed what the model admits (nested sets in every scenario, step 10);
    - it extended requirements only to cases where they can be met (the INV-103 views; the on-treatment ask where a day on the course is placed);
    - it kept every earlier fix's formal text, and every verdict wherever the context states the start.
    No remark undid an earlier fix. The fallback that R27-01 removed was a fixer addition that no remark had asked for.
  - **Why it is not a cycle.** No item went back to an earlier state.
    - The two point-level returns (Findings, A, and the iteration-24 Findings B) end in states that did not exist before.
    - Fix 28 made the classification explicit for every start-tied bound of the model, in 46 rows. The cluster is therefore decided item by item: content placed before the start (the original baseline, the pre-treatment baseline of the review view, the response comparison, the start date and the duration) needs a stated start. Content placed by dated course events (the post-stop view, its after-periods and on-treatment period, control-level months, adherence windows, the end of an acute summary) does not.
  - **Why it is not yet converged.**
    - Iteration 28 had two competing positions on whether the post-stop view and its on-treatment period are aligned to the start (fix 27) or to the event (R28-01, fix 28). Both are stated in the E-049 Notes of v27 and v28.
    - The v28 ask for the on-treatment period lives in INV-070, beside the unchanged E-049 `when` clause, so two places now state when the period is asked for. Not a contradiction under section 3.3 (2), where a `when` clause imposes presence only where it holds.
    - The cluster has drawn five remarks in a row.

**Judgement.**
- **Converging.** The treatment-course cascade of iterations 25–28 is a monotone refinement towards one semantics:
  - one stop per course;
  - a restart is a new course, linked to the course it resumes;
  - the original baseline lies before the start of the first course of the chain, and only where the context states that start;
  - event-aligned content is placed by dated course events where no start is stated.
- **Not converged.** The remark count is flat (1, 1, 2), v28's volume is high, and the last step reversed one supporting argument of the step before.
- **What the next check should see.** A fifth remark on this cluster that reverses any of fixes 25 to 28 is oscillation (watch point 1). Iterations 29–32 should either reach three NO_REMARKS in a row, or produce remarks outside this cluster.

## Findings

None.

No item oscillates, so nothing is frozen, FROZEN_ITEMS.md is not written and OUTPUT_MODEL.md is not changed. Four points come closest to a back-and-forth pattern; each is assessed below.

### A. The post-stop view and its on-treatment period for a course whose start the context does not state (INV-103, INV-070, E-049; v00–v01 → v02–v27 → v28)

**Trace** (`course.py`, contexts B and D, and `hist.py`):

| Version | INV-103: view required for such a course | On-treatment period asked for (stop or pause) | On-treatment bound | What the text says |
|---|---|---|---|---|
| v00–v01 | no (`startOf(c, e.treatment) ≠ ∅`) | yes (E-049 SHOULD, no `when`) | none (vacuous `∀ s ∈ startOf`) | INV-103 Reading has no start condition (a description defect) |
| v02–v09 | no | no: fix 02 item 5, `when ∃ s ∈ startOf • s < self.eventDate` | none | as v00 |
| v10–v26 | no | no (v17: `… s < x`) | none | INV-103 Reading: "of a preventive treatment that has started" (fix 10) |
| v27 | no | no | none | E-049 Notes (fix 27): the view of a course "whose view INV-103 does not require"; the original baseline asked for "as it asks for the other content aligned to a start where the context states that start (the on-treatment period here; INV-055, INV-056, INV-102, INV-103; E-055 Notes)" |
| v28 | **yes** (conjunct removed) | **yes, where a course event is dated before the changed regimen** (INV-070 presence conjunct; the E-049 `when` clause byte-identical) | `courseBegunBy(ctx, v.treatment, q.start) ∧ q.end < x` | INV-103 Reading "whether or not the context states the start of its course"; E-049 Notes: the view and its on-treatment period "are aligned to the event, not to the start"; the v27 clause and INV-103 in the list deleted |

**The competing positions, with their evidence:**
- **Start-aligned (fix 27; review 27).**
  - Review 27, "Checked and not raised": "INV-070's baseline and on-treatment bounds are vacuous for such a course, as INV-068's are. INV-103 does not require its post-stop view. This is the model's general treatment of unstated starts".
  - Fix 27, choice of option (b), point 3: "The model asks for content aligned to a treatment start only where the context states that start: […] the treatment review view (INV-102) and the post-stop view itself (INV-103); the on-treatment period of this very view (E-049 `when` clause of `onTreatmentPeriod`)".
- **Event-aligned (R28-01; fix 28).**
  - R28-01: OUT-022 "conditions on nothing about a known start"; "the post-stop view is aligned to its event (`eventOn`, `firstChangedDay`), not to the start". Stage 1 OUT-022: "After a preventive treatment is stopped, paused or reduced, the diary output SHOULD continue to show headache and migraine frequency and compare it with both the on-treatment period and the original pre-treatment baseline".
  - Fix 28: "Fix 27's ground ('no period can be placed') holds for the original baseline, but not for the on-treatment period". Its reason: every course event is dated on a day by which the course has begun (section 2.8), so a period after the first dated event and before the changed regimen lies on the course.

**Why it is not an oscillation:**
1. **Every predicate changed once.**
   - INV-103's conjunct was unchanged from v00 to v27 and was removed in v28.
   - The INV-070 on-treatment conjunct changed in v17 (the day convention) and in v28.
   - The E-049 `when` clause is byte-identical since v17.
   - The return at the level of one point (asked → not asked → asked) does not restore v00–v01. That state asked for the period unconditionally and with no bound, so it admitted months after the stop. It also left the view itself unrequired. The v28 state asks for the period only where a day on the course is placed, bounds it, and requires the view. It did not exist before.
2. **The first change was not a decision on this point.**
   - Fix 02 item 5 gave one reason only: the period is "impossible for a stop, pause or reduction on the start day, which INV-001 admits". The exclusion of courses without a stated start was a side effect of `∃ s ∈ startOf`. Under v01, such a period was not impossible, because the bound was vacuous.
   - Fix 10 changed only the INV-103 Reading, to describe the predicate (the R10b-02 class: "dropped `startOf(…) ≠ ∅`" → "that has started").
   - Before fix 27, no remark or fix argued for the INV-103 condition, as review 28 states ("The `startOf` conjunct of INV-103 is unchanged since v00. No remark or fix argued for it").
3. **One argued position replaced by another, once.**
   - Fix 27 used the start-aligned reading as a supporting precedent for the baseline decision. It did not use it as a decision on INV-103 or on the on-treatment period, and neither item changed in v27.
   - Fix 28 replaced the precedent with the event-aligned reading and kept fix 27's decision itself. In v28, `originalStart`, the E-049 `baseline` `when` clause and the INV-070 baseline conjunct are byte-identical, and the E-049 Notes keep "Neither view shows a baseline".
   - So v27's decision, "no original baseline without a stated original start", was neither reversed nor contradicted in v28. Fix 27's arguments (1) and (2) still stand: option (a) still admitted on-treatment months, and no period can be placed before an unstated start. Only argument (3), the analogy, was withdrawn.
4. **Fix 02's principle is kept** (required = possible; iteration-24 Findings B).
   - The stated-start cases of watch point 4 are unchanged in v28: a stop on the start day still asks for its 1-day period, and a reduction on the start day asks for none (context G). The new presence conjunct applies only where `startOf(ctx, v.treatment) = ∅`.
   - For a course without a stated start, the period is asked for exactly where one can be shown: after every stop or pause, and after a reduction that another dated event precedes. This matches fix 28's check, 65,648 of 65,648 events.

**Judgement:** convergent, and the closest approach of iterations 25–28. The point is now argued both ways in the loop files, so a further change in either direction on it is oscillation (watch point 1).

### B. `originalStart` with and without the fallback (v26 → v27)

**Trace:**
- **v25.** No `originalStart`. The post-stop baseline is bounded by the start of the view's own course (`∀ s ∈ startOf`).
- **v26 (fix 26).** `originalStart(c, t)` is "the earliest start that the context states for t or for a course that t resumes": the first course's start, or, where that course states none, the earliest start stated in the chain.
- **v27 (fix 27).** The start of the first course of the chain only: `{d | ∃ u • resumesFrom(c, u, t) ∧ (∀ p ∈ c.subject.resumes • p.2 ≠ u) ∧ d ∈ startOf(c, u)}`, ∅ where the context states none. INV-070 changes from `∀ s ∈` to `∃ s ∈`, and E-049 `baseline` gains `when originalStart(…) ≠ ∅`.
- **v28.** Unchanged.

**Is the fallback an A → B → A? No.**
1. **The item never returned.** `originalStart` went from absent, to the form with the fallback, to the first-course form: three different states. The v27 form is not v25's bound, because v25 had none of the chain.
2. **The admitted baselines are nested, never re-widened** (`course.py`). Three contexts:
   - **Example B,** the view of t2's reduction: 32 months before t2's start (v25), the same 32 months (v26, where the fallback is t2's own start), 0 (v27–v28).
   - **Chain D,** the view of k's stop: 32 months (v25), 23 months, those before b's start (v26), 0 (v27–v28).
   - **Every chain whose first start is stated** (contexts C and E): v26 = v27 = v28.

   So v25 ⊇ v26 ⊇ v27 = v28 in every case.
3. **One position throughout.**
   - R26-01's required change: "Define the original start of a course as the start of the first course of its chain of resumptions".
   - Fix 26's own Notes: "the start of the first course of that chain".
   - R27-01 and fix 27 say the same.
   - The fallback was the fixer's addition. It was checked only for being "never after the course's own start", and no remark or fix argued for it. R27-01's option (a), a bound by the dated course events of the chain, was not taken. Fix 27 gave evidence that option (a) still admits on-treatment months (115,321 of 249,051 accepted baselines in chains of 2–4 courses).
4. **No earlier fix reversed.**
   - Fix 25 ("the original pre-treatment baseline stays admissible after a restart") is kept: it is admissible wherever the first start is stated.
   - Fix 26's link `resumes`, `resumesFrom` and the INV-001 conjuncts are verbatim in v27 and v28.

**Judgement:** convergent. A fixer's over-reach, corrected one iteration later to the reviewer's original specification.

### C. The v28 start-tied bounds and fixes 05 and 14 (INV-064, INV-109; also INV-067, INV-068, INV-078, INV-079)

**Did v28 reverse fix 05 or fix 14? No.**
- **INV-064 (fix 05).**
  - **What changed.** Fix 05 added `(∀ s ∈ startOf(ctx, L.treatment); p ∈ ran L.evaluated • s ≤ p.start)`, because the tie "existed only in INV-062, at SHOULD". v28 replaces it with `(∀ p ∈ ran L.evaluated • courseBegunBy(ctx, L.treatment, p.start))`.
  - **Same verdict where the start is stated.** `courseBegunBy(c, t, d)` holds exactly when `s ≤ d`, because the start is a course event and INV-001 dates no course event before it. Contexts A, C, E and F give the same months in v27 and v28.
  - **Stricter where it is not stated.** Months before the first dated event are no longer admitted (context B: 30 → 3 months).
  - **Kept.** `evaluatedOnTreatment(L)` (v18) is verbatim.
  - **The deleted sentence.** The v05 Notes sentence "the start tie then constrains nothing" described the vacuity, with the reason that no response comparison exists. No remark or fix argued that the months should stay unconstrained. Review 28 set the point aside for that reason, and fix 28 replied that INV-064 is definitional and admitted wrong months.
- **INV-109 (fix 14, R14-02).**
  - **What fix 14 decided.** Fix 14 tied an acute line's summary to "the span of its course" and wrote: "For a course without a stated start (no stated span, start date or duration, E-055), the period stays unconstrained, as the review's 'for an acute line of a treatment that has a start' provides". That followed the scope of the remark; it is not a position against tying the end.
  - **What v28 changes.** It moves the end ties (the stop date, or the as-of date) outside `∀ b ∈ startOf` and adds that the summary begins on or before every dated course event.
  - **Same verdict where the start is stated.** The start equals b, and INV-001 puts every event after it.
  - **Where it is not stated.** The tie runs in R14-02's own direction: in context H, 5 → 2 admitted periods.
  - **Kept.** `allTypes`, `summarisesMedication` and `adherenceFor` are verbatim, so iteration-16 watch point 3 is not crossed.
- **INV-068 (R28-02).**
  - **What changed.** `∀ s` → `∃ s`, the first change of this conjunct since v00.
  - **Same verdict where the start is stated.**
  - **Where it is not stated.** No review view is admitted, which matches INV-102 (unchanged since v00) and INV-056 (`rc.treatmentStart ∈ startOf`).
  - **Kept.** `notStoppedBefore` (v18) is verbatim. No remark ever argued for admitting a review view without a stated start.
- **INV-067, INV-078 and INV-079.** First changes of their conjuncts since v00 or v02. Each gives the same verdict where every line or treatment has a stated start, and each is stricter otherwise:
  - INV-067: `courseBegunBy` for the adherence window;
  - INV-078: every pair of lines, so a line without a start date no longer suspends the order (context I);
  - INV-079: no duration without a start, as E-055's `when` clause already said since fix 02.

  INV-078's placement conjuncts (iteration-12 watch point 3) are verbatim.

**Judgement:** convergent. One rule applied model-wide in one direction. Its size (5 of the 9 blocks of v28, from a fixer sweep beyond the review) is a volume concern, not a reversal.

### D. One stop per course: review 15's settled point reopened (v25)

**Trace:**
- **Review 15** set the case aside: "Several stop events in one course. […] Stage 1 does not say whether a resumed or later-discontinued pause is one course. The model's ordering requirements hold either way. Not raised."
- **Fix 18** referred back to it, and the iteration-16 check listed it as settled.
- **R25b-01** raised it. Its new evidence: the v17 day convention and the v18 stop bounds made "the earliest stop the end of the course in E-042, INV-055, INV-068, E-046 and E-067, while INV-070, INV-079 and INV-109 still take any stop". Its instance gave two durations (41 and 89 days) for one course.
- **Fix 25** added the bound to INV-001.

**Why it is not an oscillation:**
- The settled state was "no change". Reopening it produced the first change of this point, and only additive conjuncts.
- No course-event date of section 2.8 changed (watch point 4).
- "A restart is a new course" had been the model's reading since fix 11 (INV-001 allows one start per course).
- No later remark argues for several stops.

**Judgement:** convergent. A settled point reopened on evidence that postdates it, in one direction.

## Things the next checker should watch

1. **Courses whose start the context does not state** (INV-103, INV-070, E-049, E-008 `courseBegunBy`; v28). This point is now argued both ways (Findings, A). Treat as oscillation and freeze, unless it rests on evidence that review 27, fix 27, R28-01 and fix 28 did not consider:
   - restoring `startOf(c, e.treatment) ≠ ∅` in INV-103, or any other condition that drops the post-stop view of such a course;
   - dropping the INV-070 presence conjunct, or taking R28-01's option (a) (no on-treatment period without a stated start);
   - returning the on-treatment bound to `∀ s ∈ startOf` (vacuous without a start);
   - restoring the v27 E-049 Notes classification of the post-stop view and its on-treatment period as start-aligned content.

   **Not a reversal:** moving the ask from INV-070 into the E-049 `when` clause as a disjunct for unstated starts only, provided the stated-start cases stay as they are. A stop on the start day asks for its period; a reduction on the start day asks for none (iteration-24 watch point 4).
2. **The original pre-treatment baseline** (E-008 `originalStart`, `resumes`, `resumesFrom`; E-049 `baseline` `when`; INV-070 baseline conjunct; v26, v27). Treat as oscillation:
   - re-adding a fallback to `originalStart` (v26), or taking R27-01's option (a), a bound by the dated course events, which fix 27 declined with evidence;
   - admitting a baseline where `originalStart = ∅`, or returning the INV-070 conjunct to `∀ s ∈ …` or to `startOf`;
   - dropping `resumes` or its INV-001 conjuncts, or replacing the link by a reading of `paused` (R26-01's option (b), declined by fix 26).

   **Not a reversal, but a new decision:** moving the reading of "original" to section 8 as a Stage 1 issue. Fix 26 found Stage 1 clear. Such a move must not change the v27 predicates without the human.
3. **One stop per course; a restart is a new course** (INV-001 v25; section 2.8; E-008). Admitting several stops of one course again, or a dose change after the stop, would reverse fix 25. Watch point 4 of the iteration-24 check still applies to every course-event date.
4. **The start-tied bounds of v28** (INV-064, INV-067, INV-068, INV-078, INV-079, INV-109; the 46 rows of fix 28's table).
   - **Reversals:** `courseBegunBy` back to `∀ s ∈ startOf`; INV-068 back to `∀ s`; INV-109's end ties back inside `∀ b ∈ startOf`; INV-078 back to neighbouring pairs; dropping INV-079's duration conjunct.
   - **A contested row.** A remark that a row of fix 28's table is misclassified (start-aligned or event-aligned) must say which, with Stage 1 evidence.
   - **Review 28's reason.** Review 28's "a SHOULD invariant already needs a response comparison" was rebutted by fix 28. Re-raising it as a reason to loosen needs new evidence.
5. **Two places for one ask.**
   - **What.** The on-treatment period is asked for by E-049's `when` clause where the start is stated, and by INV-070 where it is not. Section 3.3 (2) makes this consistent.
   - **If a remark calls it a duplication,** the fix may merge the two asks. It must not change either case (watch points 1 and 4).
6. **All earlier watch points.** Unchanged in v25–v28; all 49 blocks they name are byte-identical v24 → v28:
   - the v24 by-dates relations and INV-006's identity (check 24, watch point 1);
   - INV-111 and INV-008 (2);
   - the cluster view (3);
   - the day convention and the stop bounds (4);
   - `fillsPeriod` (5);
   - the formulation ties (6);
   - the text-only ISS items (7);
   - INV-105 with E-067, the history-wide `acuteMedications`, the identity ties, responder labels, E-041, INV-098 and co-presence (8);
   - periods beyond the as-of date (10).

   Their reversal triggers still apply. Output-wide agreement of counts stays a new decision, not a reversal (reviews 25, 25b and 26).
7. **Change volume and remark pattern.**
   - Items changed: 39, 41, 36 and 84 in v25–v28; formal blocks: 1, 4, 3 and 9. Remarks: 0 + 1, 1, 1 and 2, all on the treatment-course cluster.
   - Check that volume falls after v28.
   - **The cluster.** A sixth consecutive remark on it should be read against watch points 1–4. If it reverses nothing, check whether it finds a genuinely new case, or whether the cluster keeps generating consequences of its own fixes. A self-feeding cascade that does not end by iteration 32 is a question for the human, even without a reversal.
   - **Fixer sweeps.** A fix that again changes more items than its remarks name, on items its review set aside, should be checked for reversals of the review's stated reasons.

## Conclusion

No item of the model oscillates after twenty-eight iterations, and nothing is frozen.

- **Returns.** The only item that returns to an earlier state is `aged12OrOlder` (added in v06, removed in v12), which the iteration-12 check assessed. In v25–v28, no element, attribute, field, invariant, `omn` block, conformance level, source, section, value set, Realises field or traceability row returns to an earlier state. No admitted set re-widens in any scenario.
- **Point-level returns.** One new return, without a return of any item:
  - the on-treatment period asked for a course without a stated start: asked in v00–v01, not asked in v02–v27, asked in v28 where placeable and bounded;
  - with it, the INV-103 Reading went from no start condition (v00), to "that has started" (v10), to "whether or not the context states the start" (v28).

  Each predicate changed once, and the first change was a side effect of fix 02. The competing positions (fix 27's start-aligned precedent, fix 28's event-aligned reading) changed the model once (Findings, A).
- **Questions asked of this check:**
  - **The fallback.** The `originalStart` fallback (v26 added, v27 removed) is not an A → B → A. The states are absent, fallback and first-course only, and the admitted baselines are nested v25 ⊇ v26 ⊇ v27 = v28 (Findings, B).
  - **v27's decision.** v27's decision ("no original baseline without a stated original start") was kept verbatim in v28. Only its third, analogical argument was withdrawn (Findings, A).
  - **INV-103.** The v00–v27 condition had been defended by no remark or fix before fix 27 cited it as a precedent (Findings, A).
  - **Fixes 05 and 14.** The v28 changes of INV-064 and INV-109 keep fix 05 and fix 14 and extend them to courses without a stated start (Findings, C).
- **Change volume:** 39, 41, 36 and 84 items in v25–v28; formal blocks 1, 4, 3 and 9.
- **Remark counts:** 0 + 1, 1, 1 and 2.
- **Convergence.** The treatment-course cascade R25b-01 → fix 25 → R26-01 → fix 26 → R27-01 → fix 27 → R28-01/02 → fix 28 is a monotone refinement. Each step narrows the admitted outputs or adds requirements that can be met, and no step undoes an earlier fix. The loop has not converged: the remark count is flat, v28's volume is high, and the cluster has drawn five remarks in a row.

The scripts are in the session scratchpad (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/osc28/`): `split.py`, `analyse.py`, `cluster.py`, `volume.py`, `omn.py`, `omntraj.py`, `omndiff.py`, `hist.py`, `nearret.py`, `ngram.py`, `docwide.py`, `wdiff.py`, `dels.py`, `multi.py`, `conf.py`, `guar.py`, `course.py`, `remarks.py` and `book.py`. FROZEN_ITEMS.md was not written, and OUTPUT_MODEL.md and the history snapshots were not changed.
