# Fix — iteration 35, after the equivalence check
Version produced: v35 (corrected)
Date: 2026-10-22

This is step 3 of the restructuring of iteration 35 (PROCESS.md section 8): "If the check finds defects, a new fixer corrects v35 before the review of iteration 36". The input is [`restructure/equivalence-v35.md`](../restructure/equivalence-v35.md), with its verdict DEFECTS and the five defects EQ35-01 to EQ35-05. The intended changes CHG-01 to CHG-07 and CHG-R1, and the mapping of v34 items to v35, are taken from [`fixes/fix-iter-35.md`](fix-iter-35.md). The baseline for every comparison below is the committed v35 (`git show HEAD:docs/stage2-output-model/OUTPUT_MODEL.md` and `…/RATIONALE.md`).

Files written:
- `OUTPUT_MODEL.md` and `RATIONALE.md`, the corrected v35. The header is unchanged (`Version: v35 · Iteration: 35 · Status: under review`). The v35 change-log entry has one added line pointing to this log.
- `history/v35.md` and `history/v35-rationale.md`, byte-identical copies of those two files.
- This log.

All checks were run by my own scripts with `python3 -I`. The scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix-eq35/`, outside the repository:
- `braces.py`, `checks.py`: bracket balance, formal identity against HEAD, quotes, ID resolution, scope terms, watch-point texts;
- `urls_all.py`, `srclines.py`: URLs against Stage 1 and v34;
- `sweep.py`, `sweep_filter.py`, `byid.py`, `ent.py`: the class sweep of EQ35-04;
- `apply.py` to `apply5.py`: the edits, each an exact string replacement that must match exactly once;
- `edits.json`: the record of every edit.

## 1. Summary

| Defect | Verified | Disposition | Places changed: named by the check / found by the class sweep |
|---|---|---|---|
| EQ35-01 stray `}` in E-045 | yes, by script | fixed | 1 / 0 |
| EQ35-02 truncated S-035 URL | yes, by script and by HTTP | fixed | 11 / 0 |
| EQ35-03 residual burden "next to every percentage change" | yes | fixed | 4 / 0 |
| EQ35-04 references that name the v34 home or level of a moved conjunct | yes | fixed | 11 places (13 edits) / 11 places (14 edits) |
| EQ35-05 INV-118 Reading claims more than its predicate | yes | fixed | 1 / 3 (the Readings of INV-119, INV-120 and INV-124) |

One consequential edit was needed: the "Moved text" rule of `RATIONALE.md` section 1. Moved text is no longer verbatim in the places that EQ35-03 and EQ35-04 correct, so the rule now names these exceptions (section 7).

The change-log line is the only other edit. Formal content:
- Only one `omn` block changed: E-045, by the deletion of one character.
- The other 159 `omn` blocks are byte-identical to the committed v35.
- Every table row of the model is unchanged: the catalogue, the case tables C1–C3, the source data tables and the traceability table.
- No quote, location or translation changed.

Every edit keeps the meaning of the model. EQ35-03 and EQ35-04 bring prose into line with the formal text, which is unchanged.

## 2. EQ35-01 — stray `}` in the formal block of E-045

**Verification.**
- `braces.py` over the 160 `omn` blocks of v35 finds exactly one unbalanced block: E-045, with 12 `{` and 13 `}`. All 188 blocks of v34 are balanced.
- The last line of the block read `const namedCriteria : set1 ResponderCriterion ≙ table SD-RC}`. Section 2.3 defines the form `const S : set1 T ≙ table N`, and plan section 8 gives the line as `≙ table SD-RC`.

**Disposition.** Fixed.

**What changed.** The trailing `}` is deleted. The line now reads `const namedCriteria : set1 ResponderCriterion ≙ table SD-RC`.

**Where.** `OUTPUT_MODEL.md` line 1469 (E-045 Definition), and the same line in `history/v35.md`.

**Class sweep.** The class is a formal text left ill-formed by a scripted move into a case table.
- **`omn` blocks.** All 160 are balanced in `{}`, `()`, `[]` and `⟨⟩`.
- **Formal table cells.** All 696 backticked cells of the model's tables are balanced. These are the formal columns of C1–C3 and of the source data tables, and the other code cells.
- **Paragraphs that refer to a table.** All 18 `≙ table` and `axiom table` paragraphs have the form of section 2.3. These are the lines of E-009, E-011, E-028, E-032, E-041, E-045, E-046 (three), E-050, E-057 (two), E-059 (two), and the four `pp…`/`…Claims`/`…Annotations` functions of section 4.4.

Result: no further defect.

## 3. EQ35-02 — truncated S-035 URL

**Verification.**
- **Source lines.** `srclines.py` compares the URL of each of the 153 `- Source:` lines of `RATIONALE.md` with the URLs of that source's row in Stage 1 section 5, or in model section 10. 142 match. The 11 that do not are exactly the S-035 lines, each cut at the first `)`: `…Protokol%c3%bc%20(Revizyon`.
- **Stage 1.** Stage 1 line 662 (S-035) gives `https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon)%20(92%20Sayfa).pdf`.
- **HTTP.** A ranged request for the full URL returns HTTP 206 with `application/pdf`. The truncated URL returns HTTP 404.

**Disposition.** Fixed.

**What changed.** The full Stage 1 URL is given in the 11 Source lines. Nothing else in these entries changed: their quotes, locations and translations are byte-identical (check Q in section 9).

**Where.** `RATIONALE.md`, the Source line of each of these entries:
- E-041/Q00 (line 594);
- E-041/Q22 to E-041/Q28 (lines 750, 758, 766, 774, 782, 790, 798);
- E-045/Q00 (896), E-045/Q03 (917) and E-045/Q04 (923).

**Class sweep.** The class is any URL lost or altered in the move to `RATIONALE.md`.
- **All URLs.** `urls_all.py` takes every URL in `OUTPUT_MODEL.md` (7 occurrences) and in `RATIONALE.md` (155 occurrences, 29 distinct). It compares each with the 66 URLs of Stage 1 and v34, and reports any that is only a prefix of a known URL.
- **Before the fix.** 11 mismatches, all of them the S-035 prefix.
- **After the fix.** 0 mismatches, and all 153 Source lines match their source row.
- **Other URLs with parentheses.** Stage 1 has one URL that contains parentheses (S-035). The others in Stage 1 that end in `)` carry only a closing bracket of the surrounding prose, and no Source line uses them.

Result: no other truncated or altered URL.

## 4. EQ35-03 — residual burden "next to every percentage change"

**Verification.**
- **INV-060 and ISS-13.** The v35 predicate of INV-060 has the antecedent `ch.compared.period.lengthDays ≥ shortestMonthlyDays` (CHG-03), and its Reading says so. ISS-13 states that the residual burden "is not asked for next to a change over a shorter compared period".
- **ISS-03.** The OUT-019 bullet of ISS-03 Effect said "next to every percentage change in migraine or headache days". This contradicts ISS-13 in the same section.
- **RATIONALE entries.** E-044/D01 said the same and contradicted INV-060. E-040/D01 cited INV-060 for "wherever a percentage change … is shown". INV-060/D01 said that a percentage change in the headache days of a subject without migraine SHOULD be shown with its residual migraine days, with no restriction on the compared period.

**Disposition.** Fixed, by qualifying each sentence with the condition of the changed predicate. This is a qualification that CHG-03 requires, not a return to earlier wording. So the text-only watch point on ISS-03 (oscillation check 24, watch point 7) is not touched: no earlier wording is restored. The "For the human" field of ISS-03 is unchanged.

**What changed and where.**
- `OUTPUT_MODEL.md` line 3494, ISS-03 Effect, OUT-019 bullet: "… next to every percentage change in migraine or headache days **whose compared period has at least 28 days (ISS-13)**, whatever the subject's headache types (E-044, INV-060, INV-061), …".
- `RATIONALE.md` line 884, E-044/D01: "… next to every percentage change in migraine or headache days **whose compared period has at least 28 days (INV-060; ISS-13)**, without the condition …".
- `RATIONALE.md` line 580, E-040/D01: "OUT-019 asks, wherever a percentage change … is shown, for the residual burden next to it (INV-060**, where the compared period has at least 28 days; ISS-13**)". The sentence still states OUT-019's own wording; the parenthesis now says how far INV-060 realises it.
- `RATIONALE.md` line 1722, INV-060/D01: "a percentage change in the headache days of a subject without migraine**, over a compared period of at least 28 days (INV-060/D02; ISS-13),** SHOULD also be shown with its residual migraine days".

**Class sweep.** The class is any statement in the model or in `RATIONALE.md` about where the residual burden is shown, or about a percentage change with "every", "each", "wherever" or "any". The sweep found nothing else to change:
- the INV-060 Reading, ISS-13, catalogue row OC-22 and traceability row OUT-019 already state the 28-day condition or cite ISS-13;
- the E-044 Meaning describes the element without "every";
- E-040/D01's second text ("INV-060 … apply to it") and INV-062/D02 ("the residual burden (INV-060) concerns only changes in migraine or headache days") are true of the changed predicate;
- the INV-062 Reading paraphrases INV-062's own conjunct, which has no 28-day antecedent. The changes of a response comparison are monthly (INV-056), so this agrees with INV-060.

## 5. EQ35-04 — references that name the v34 home or level of a moved conjunct

**Verification.** I read each place that the check names against the v35 predicates and against the formal diff of v34 → v35. Each place either names an item that no longer holds the cited constraint, or states the level that CHG-R1 changed:
- INV-056 and INV-068 lost their treatment facts to INV-123 at definitional level (CHG-R1);
- INV-070 lost its presence ask to E-049's `onTreatmentPeriod` `when` clause;
- INV-072 lost its placements to the W2 markers on E-051 `outcomes`, `sequence`;
- INV-075, INV-079 and INV-082 lost their medication, course-event and availability facts to INV-123;
- INV-050 lost its review-window conjunct, now implied by E-039 `reviewWindow` (CA-05).

**Disposition.** Fixed. Each reference now names the item that holds the constraint in v35, and the level where it changed. The wording is otherwise kept.

**Places named by the check** (11 places, 13 edits):
- `OUTPUT_MODEL.md` line 2850, INV-069 Reading: "whose outcome summaries and treated-attack lines ~~INV-072 shows~~ **E-051 `outcomes` and `sequence` (W2) place** in the same view".
- `OUTPUT_MODEL.md` line 2898, INV-071 Reading: "in the same view (~~INV-072~~ **E-051 `outcomes`, `sequence` (W2)**)".
- `OUTPUT_MODEL.md` line 3538, ISS-11 Effect: "(E-039 **`reviewWindow`**, ~~INV-050,~~ INV-051)".
- `RATIONALE.md` line 2299, INV-123/D02, two edits:
  - The list of ties now reads: "a marker, an adherence summary, a treatment line, a post-stop monitoring view, a response comparison and a treatment review view (INV-123) and an evaluation time point (INV-058) show a treatment of the subject wherever they are shown; the ties of a response comparison and a treatment review view are definitional from v35 on (in v34 MUST conjuncts of INV-056 and INV-068; CHG-R1)". It replaces "… (INV-067) … (INV-079) … (INV-112) …, and a response comparison (INV-056) and a treatment review view (INV-068) do so at MUST".
  - "one of the subject's preventive treatments (~~INV-056~~ **INV-123**)".
- `RATIONALE.md` line 1877, INV-112/D01: "the values of the periods are asked for by INV-070, and the on-treatment period where the context states no start by the `when` clause of `onTreatmentPeriod` (E-049/D04), both at the level of OUT-022". Before, both were attributed to INV-070.
- `RATIONALE.md` line 2109, INV-103/D01: "E-049 asks for the periods after the event and, by the `when` clause of `onTreatmentPeriod` (E-049/D04), for an on-treatment period …". Before: "… and INV-070 for an on-treatment period …".
- `RATIONALE.md` line 1907, INV-074/D01, two edits: "only through ~~INV-075~~ **INV-123 (`usedMedication`)**" and "has used its drug (~~INV-075~~ **INV-123**)".
- `RATIONALE.md` line 1949, INV-109/D01: "~~INV-079~~ **INV-123** makes every shown dose change one of them".
- `RATIONALE.md` line 1029, E-046/D03: "as in INV-081 and ~~INV-082~~ **INV-123**".
- `RATIONALE.md` line 1656, INV-049/D01: "Its content is that of INV-050 **and E-039 `reviewWindow`**: …, and the review window". The next sentence of the entry already names E-039 `reviewWindow`.
- `RATIONALE.md` line 2304, INV-123/D06: "stay at its level (INV-050**; E-039 `reviewWindow`**)".

**Class sweep.**

*Method.* The items in scope are of three kinds:
- the 38 invariants merged in section 9;
- the 27 kept invariants that lost a conjunct or changed meaning, per the mapping of `fixes/fix-iter-35.md` section 4: INV-012, 024, 031, 032, 033, 035, 041, 050, 056, 059, 060, 062, 067, 068, 070, 072, 075, 078, 079, 082, 085, 087, 089, 092, 109, 111, 112;
- the elements whose attribute types or `when` clauses took a moved conjunct: E-034, E-049.

`sweep.py` extracted every sentence of model prose and of `RATIONALE.md` (outside `omn` blocks, model section 12 and the search log) that cites one of these items: 591 sentences, 243 in the model and 348 in `RATIONALE.md`. I read every sentence.

In addition:
- I read the 38 non-Q entries anchored at the reduced invariants.
- I read every ordinal reference to a conjunct: 31 in `RATIONALE.md` and 6 in the model, for example "the last conjunct".
- I re-ran the checker's own `stale.py` on the result.

*Rule applied.* This is plan section 11, last paragraph: "A reference to a kept invariant that lost a conjunct names the item that now holds the conjunct, wherever the sentence is about that conjunct." A reference was corrected only when its sentence attributes a moved constraint to an item that no longer holds it, or states a level that the move changed. References whose cited constraint is still in the cited item were left as they are. Three examples:
- "the on-treatment periods … begin on or after the treatment start (INV-056)": the start date of the comparison, E-043 `treatmentStart`;
- "a stop date … not before the start date (INV-079)";
- "INV-062 asks for …" where the ask is still in INV-062.

References to merged items are all provenance ("v34 INV-…", "Replaces …", case-row origins), as the check found.

*Places found by the sweep* (11 places, 14 edits):
- `OUTPUT_MODEL.md` line 143, section 2.8, "Course events": "the first day off treatment is the day after it (~~INV-070~~ **`firstChangedDay`, E-049**)".
  - v35 INV-070 no longer uses `firstChangedDay`. The definition is in E-049, which also holds the moved `when` clause, and INV-112 uses it.
  - Only the reference changed. The day convention and every course-event date are unchanged (oscillation check 24, watch point 4).
- `RATIONALE.md` line 1074, E-049/D03: "for a reduction that another dated course event precedes (~~INV-070~~ **the `when` clause of `onTreatmentPeriod`; E-049/D04**)". The entry keeps "aligned to the event, not to the start".
- `RATIONALE.md` line 1681, INV-050/S01: "when ~~the condition of the last conjunct holds~~ **the covered period reaches the end of the window (INV-050/D02)**". The "last conjunct" of INV-050 was the review-window conjunct that v35 removed; v35's last conjunct is the series conjunct.
- `RATIONALE.md` line 2074, INV-115/D01: "`components` stays SHOULD for migraine (E-033, INV-092)**; the placement marker of E-033 `components` (W2) asks for the components in the index's view, and INV-092** for one of each dimension the index combines". Before, INV-092 was said to ask for the components in the index's view; that conjunct moved to W2.
- `RATIONALE.md` line 1927, INV-078/D02: "the line of a course whose start the context does not state (E-055, ~~INV-079~~ **INV-123**)". The tie of a shown start date to a stated start is the `courseEvent` member of INV-123.
- `RATIONALE.md` line 1959, INV-109/D03, two edits:
  - "aligned to the start of the same treatment (INV-056, INV-079**, INV-123**)";
  - "no stated start date or duration (E-055, INV-079**, INV-123**)".

  The start fact of a comparison and the start date of a line are in INV-123.
- `RATIONALE.md` line 2149, INV-105/D05, two edits:
  - "exists only for a treatment that has started (~~INV-056~~ **INV-123**)";
  - "a response comparison aligned to its start (INV-056**, INV-123**)".
- `RATIONALE.md` line 2159, INV-105/S02: the satisfiability list for a comparison shown "with its values, changes, time points and adherence" now has **E-043 `timePoints` (W2)** after INV-059. The placement of time points moved from INV-059 to W2; the list already cites the analogous E-040 `reference`, `compared` (W2).
- `RATIONALE.md` line 1500, INV-001/D02, two edits:
  - "the stop date and the duration of a treatment line (INV-079**, INV-123**)": the stop date is the `stopOn` member of INV-123;
  - "a pre-treatment baseline before its own start … (INV-056, INV-068**, INV-123**; …)": the comparison's start is its course's own start by INV-123.
- `RATIONALE.md` line 1808, INV-064/D01: "as the on-treatment periods of its response comparison do (INV-056, INV-062**, INV-123**)".
- `RATIONALE.md` line 1442, INV-123/D01, the row for E-058 `baselineResult` in the column "Tie in v35": "INV-082**; INV-123 (`availableResult`)**". The availability of the baseline result moved from INV-082 to INV-123.

*Examined and left unchanged* (the reference still names where the rule lives):
- INV-075/D01, INV-079/D01 and INV-085/D01 explain conjuncts that moved to INV-123. They name no item as the holder: their anchor is fixed by the plan, and "as INV-123 and INV-079 do" is true.
- INV-072/D01 and E-043/D01 list the items that ask for summaries or comparisons in a view ("with a responder label (INV-062)", "with a treatment line (INV-109)"). These asks are still in INV-062 and INV-109.
- Sentences that cite INV-056 for periods "after the treatment start", which is E-043 `treatmentStart`: E-042/D01, INV-055/D02, INV-055/D03, INV-055/S01, INV-066/S01, INV-120/D01.
- References to constants that moved to SD-FX. Each element named keeps a comment line naming table SD-FX, and SD-FX names the element in its own column (D-7).
- The Conformance fields, catalogue cells and traceability rows. They already name the v35 places (INV-121 to INV-125, W2, INV-123).

## 6. EQ35-05 — INV-118 Reading, and the Readings of the other generic invariants

**Verification.**
- The predicate of INV-118 asks `reportedTogether(c, q.2, q.1)` separately for each pair `q ∈ ppRequired(r, l, c)`.
- C1-09 has four pairs and C1-13 has one pair per type scope. Different pairs may be met by different outputs, views and series.
- The Reading asked for "values of each kind that the case asks for, with the type scope it names" in one view and one series. That claims more than the predicate. "The type scope it names" is also undefined for C1-13.

**Disposition.** Fixed.

**What changed.** `OUTPUT_MODEL.md` line 2017, INV-118 Reading, now reads: "… such that, for every admissible context of that granularity and for every pair of a type scope and kinds of per-period value that the case asks for in that context (`ppRequired`), the diary can produce an output in which one view and one series that spans the selected time range show, for every period of the series, values of each of these kinds with that type scope (`reportedTogether`, section 3.4)."

**Class sweep.** I checked the Readings of INV-119 to INV-125 against their predicates and the case tables.
- **INV-119** (line 2028) and **INV-120** (line 2039) have the same quantifier shape as INV-118: `∀ q ∈ prohibitedClaims(r, l)` and `∀ q ∈ requiredAnnotations(r, l)`.
  - Their Readings spoke of "a claim of that case" and "an annotation of the kind of that case".
  - C3-01 has two pairs and C3-09 has three. For these cases "the kind of that case" is undefined, and it can be read as asking for one annotation where the predicate asks for one of each kind.
  - Every C2 case has one pair, so INV-119's per-case wording happened to be exact for the current table. It still claimed more than its predicate, which is per pair.
  - Both Readings now follow the per-pair quantifier: "For every pair of a set of claims and a set of bearers in a case of table C2 at level l, no element of the output among those bearers is presented with a claim of that set, …". INV-120 is worded the same way: "… every element of the output among those bearers is qualified by an annotation of that kind".
- **INV-124** (line 2093). The Reading said that two cluster periods, or two remission periods, "are the same period or do not overlap". The predicate gives `(xs = ys ∧ xe = ye)`: equal dates, not one item. Two items in two views may show the same period. The Reading now says "have the same start date and last day or do not overlap".
- **INV-121, INV-122, INV-123 and INV-125.** Their Readings state exactly their predicates and the definitions they name (`daysWithin`, `nestedIn`, `factsShown`/`stated`, SD-DF). No change.
- **RATIONALE entries.** INV-118/D01 to D03, INV-119/D01 to D04, INV-120/D01 to D03, INV-124/D01 and SEC-2.11/W01 state the unfolding per pair or per case correctly. No change.

## 7. Consequential edit: the "Moved text" rule of RATIONALE.md

`RATIONALE.md` section 1 (line 21) said that moved text is verbatim "with two exceptions": merged-invariant references, and the CA/R35-01 corrections. EQ35-03 and EQ35-04 change moved text in ways the rule did not list:
- references to kept invariants for moved conjuncts. This is plan section 11's rule; D-14 of `fixes/fix-iter-35.md` already applied it in 15 entries.
- qualifications that an intended change requires.

The rule now lists three exceptions:
- a merged-invariant reference names its v35 place, as does a reference to a kept invariant for a conjunct that v35 moved;
- the CA/R35-01 corrections;
- "a sentence that an intended change of meaning of v35 made false is qualified (`fixes/fix-iter-35-equivalence.md`)".

Without this edit, the file's own rule would be false of the corrected entries.

## 8. Every changed location

Line numbers are those of the corrected files. The two files have the same number of lines as before, except for the added change-log line.

| # | File | Line | Place | Defect | Change |
|---|---|---|---|---|---|
| 1 | `OUTPUT_MODEL.md` | 143 | section 2.8, Course events | EQ35-04 (sweep) | "(INV-070)" → "(`firstChangedDay`, E-049)" |
| 2 | `OUTPUT_MODEL.md` | 1469 | E-045 Definition | EQ35-01 | "≙ table SD-RC}" → "≙ table SD-RC" |
| 3 | `OUTPUT_MODEL.md` | 2017 | INV-118 Reading | EQ35-05 | per-pair quantifier (section 6) |
| 4 | `OUTPUT_MODEL.md` | 2028 | INV-119 Reading | EQ35-05 (sweep) | per-pair quantifier |
| 5 | `OUTPUT_MODEL.md` | 2039 | INV-120 Reading | EQ35-05 (sweep) | per-pair quantifier |
| 6 | `OUTPUT_MODEL.md` | 2093 | INV-124 Reading | EQ35-05 (sweep) | "are the same period" → "have the same start date and last day" |
| 7 | `OUTPUT_MODEL.md` | 2850 | INV-069 Reading | EQ35-04 | "INV-072 shows" → "E-051 `outcomes` and `sequence` (W2) place" |
| 8 | `OUTPUT_MODEL.md` | 2898 | INV-071 Reading | EQ35-04 | "(INV-072)" → "(E-051 `outcomes`, `sequence` (W2))" |
| 9 | `OUTPUT_MODEL.md` | 3494 | ISS-03 Effect, OUT-019 bullet | EQ35-03 | + "whose compared period has at least 28 days (ISS-13)" |
| 10 | `OUTPUT_MODEL.md` | 3538 | ISS-11 Effect | EQ35-04 | "(E-039, INV-050, INV-051)" → "(E-039 `reviewWindow`, INV-051)" |
| 11 | `OUTPUT_MODEL.md` | 3845 | section 12, v35 entry | change log | + line "Corrected after the equivalence check: see `fixes/fix-iter-35-equivalence.md`." |
| 12 | `RATIONALE.md` | 21 | section 1, Moved text | consequential | two → three exceptions (section 7) |
| 13 | `RATIONALE.md` | 580 | E-040/D01 | EQ35-03 | "(INV-060)" → "(INV-060, where the compared period has at least 28 days; ISS-13)" |
| 14–21 | `RATIONALE.md` | 594, 750, 758, 766, 774, 782, 790, 798 | E-041/Q00, E-041/Q22 to Q28, Source line | EQ35-02 | truncated → full S-035 URL |
| 22 | `RATIONALE.md` | 884 | E-044/D01 | EQ35-03 | + "whose compared period has at least 28 days (INV-060; ISS-13)," |
| 23–25 | `RATIONALE.md` | 896, 917, 923 | E-045/Q00, Q03, Q04, Source line | EQ35-02 | truncated → full S-035 URL |
| 26 | `RATIONALE.md` | 1029 | E-046/D03 | EQ35-04 | "INV-081 and INV-082" → "INV-081 and INV-123" |
| 27 | `RATIONALE.md` | 1074 | E-049/D03 | EQ35-04 (sweep) | "(INV-070)" → "(the `when` clause of `onTreatmentPeriod`; E-049/D04)" |
| 28 | `RATIONALE.md` | 1442 | INV-123/D01, row E-058 `baselineResult` | EQ35-04 (sweep) | "INV-082" → "INV-082; INV-123 (`availableResult`)" |
| 29 | `RATIONALE.md` | 1500 | INV-001/D02 | EQ35-04 (sweep) | "(INV-079)" → "(INV-079, INV-123)" (stop date) |
| 30 | `RATIONALE.md` | 1500 | INV-001/D02 | EQ35-04 (sweep) | "(INV-056, INV-068; …" → "(INV-056, INV-068, INV-123; …" (own start) |
| 31 | `RATIONALE.md` | 1656 | INV-049/D01 | EQ35-04 | "that of INV-050:" → "that of INV-050 and E-039 `reviewWindow`:" |
| 32 | `RATIONALE.md` | 1681 | INV-050/S01 | EQ35-04 (sweep) | "the condition of the last conjunct holds" → "the covered period reaches the end of the window (INV-050/D02)" |
| 33 | `RATIONALE.md` | 1722 | INV-060/D01 | EQ35-03 | + ", over a compared period of at least 28 days (INV-060/D02; ISS-13)," |
| 34 | `RATIONALE.md` | 1808 | INV-064/D01 | EQ35-04 (sweep) | "(INV-056, INV-062)" → "(INV-056, INV-062, INV-123)" |
| 35 | `RATIONALE.md` | 1877 | INV-112/D01 | EQ35-04 | ask of the on-treatment period → E-049 `when` (E-049/D04); values → INV-070 |
| 36 | `RATIONALE.md` | 1907 | INV-074/D01 | EQ35-04 | "only through INV-075" → "only through INV-123 (`usedMedication`)" |
| 37 | `RATIONALE.md` | 1907 | INV-074/D01 | EQ35-04 | "(INV-075)" → "(INV-123)" |
| 38 | `RATIONALE.md` | 1927 | INV-078/D02 | EQ35-04 (sweep) | "(E-055, INV-079)" → "(E-055, INV-123)" |
| 39 | `RATIONALE.md` | 1949 | INV-109/D01 | EQ35-04 | "INV-079 makes" → "INV-123 makes" |
| 40 | `RATIONALE.md` | 1959 | INV-109/D03 | EQ35-04 (sweep) | "(INV-056, INV-079)" → "(INV-056, INV-079, INV-123)" |
| 41 | `RATIONALE.md` | 1959 | INV-109/D03 | EQ35-04 (sweep) | "(E-055, INV-079)" → "(E-055, INV-079, INV-123)" |
| 42 | `RATIONALE.md` | 2074 | INV-115/D01 | EQ35-04 (sweep) | view placement → E-033 `components` (W2); dimensions → INV-092 |
| 43 | `RATIONALE.md` | 2109 | INV-103/D01 | EQ35-04 | "and INV-070 for an on-treatment period" → "and, by the `when` clause of `onTreatmentPeriod` (E-049/D04), for an on-treatment period" |
| 44 | `RATIONALE.md` | 2149 | INV-105/D05 | EQ35-04 (sweep) | "has started (INV-056)" → "has started (INV-123)" |
| 45 | `RATIONALE.md` | 2149 | INV-105/D05 | EQ35-04 (sweep) | "aligned to its start (INV-056)" → "(INV-056, INV-123)" |
| 46 | `RATIONALE.md` | 2159 | INV-105/S02 | EQ35-04 (sweep) | + "E-043 `timePoints` (W2)," |
| 47 | `RATIONALE.md` | 2299 | INV-123/D02 | EQ35-04 | ties → INV-123; CHG-R1 level (section 5) |
| 48 | `RATIONALE.md` | 2299 | INV-123/D02 | EQ35-04 | "preventive treatments (INV-056)" → "(INV-123)" |
| 49 | `RATIONALE.md` | 2304 | INV-123/D06 | EQ35-04 | "(INV-050)" → "(INV-050; E-039 `reviewWindow`)" |

Entries changed in `RATIONALE.md` (32 entries, plus section 1):
- E-040/D01, E-041/Q00, E-041/Q22 to Q28, E-044/D01, E-045/Q00, E-045/Q03, E-045/Q04, E-046/D03, E-049/D03;
- INV-001/D02, INV-049/D01, INV-050/S01, INV-060/D01, INV-064/D01, INV-074/D01, INV-078/D02, INV-103/D01, INV-105/D05, INV-105/S02, INV-109/D01, INV-109/D03, INV-112/D01, INV-115/D01, INV-123/D01, INV-123/D02, INV-123/D06;
- section 1.

## 9. Checks

| Check | Result |
|---|---|
| Brace balance (`braces.py`, `checks.py`) | 160 `omn` blocks, 0 unbalanced (before: 1, E-045). 696 backticked table cells, 0 unbalanced |
| Formal identity against HEAD | `omn` blocks compared in order: 1 of 160 differs, E-045. Model table rows: 0 changed |
| Line diff against HEAD | model: 10 lines replaced, 1 inserted (the change-log line); RATIONALE: 33 lines replaced, one per changed entry and one for section 1 (lines 1500, 1907, 1959, 2149 and 2299 hold two edits each) |
| ID resolution, model | 205 E/INV/ISS IDs referenced, all resolve (headings or section 9). 174 OC/C/SD row references, all resolve. 362 entry IDs, all present in `RATIONALE.md`. Headings: 67 E, 87 INV, 12 ISS |
| ID resolution, RATIONALE | 192 E/INV/ISS IDs referenced, all resolve. 118 row references, all resolve. 397 entry IDs referenced, all exist. 432 entries, no duplicate |
| URLs (`urls_all.py`, `srclines.py`) | model 7, RATIONALE 155 URL occurrences: all in Stage 1 or v34 (66 known), 0 truncated. Source lines: 153 of 153 match their source row (before: 142 of 153). HTTP: full S-035 URL 206 `application/pdf`; truncated 404 |
| Quotes | 111 Q entries: none changed outside its Source line. Every double-quoted string of the HEAD files is present, and no new one was added |
| Scope | counts of JSON, FHIR, database, recorded, entered, captured, storage, stored: unchanged (0, 0, 0, 0, 0, 0, 4, 4 in model + RATIONALE); no input, storage or derivation terms added |
| Watch points | the three fix-28 sentences that fix 29 corrected (check 32, watch point 4) are absent. E-049/D03 keeps "aligned to the event, not to the start". The section 2.8 day convention is unchanged (only a reference). E-039 `reviewWindow` keeps no `when`. ISS-03: one qualification, no earlier wording restored |
| Header | `Version: v35 · Iteration: 35 · Status: under review` (unchanged) |
| Snapshots | `cmp OUTPUT_MODEL.md history/v35.md` and `cmp RATIONALE.md history/v35-rationale.md`: identical |
| Re-run of the checker's `stale.py` | every remaining hit is a keyword match whose reference is correct (section 5, "Examined and left unchanged") |

File sizes:

| File | Before (bytes) | After (bytes) |
|---|---|---|
| `OUTPUT_MODEL.md` and `history/v35.md` | 420,865 | 421,294 |
| `RATIONALE.md` and `history/v35-rationale.md` | 318,367 | 319,452 |

## 10. Diff summary of the formal blocks

- **Changed:** one block, E-045 (Definition). The last line loses its trailing `}`:
  ```
  - const namedCriteria : set1 ResponderCriterion ≙ table SD-RC}
  + const namedCriteria : set1 ResponderCriterion ≙ table SD-RC
  ```
  This is now the text of plan section 8. Its meaning is that of v35 as intended and as the equivalence check unfolded it: `namedCriteria` is defined by table SD-RC, with the six criteria of v34.
- **Unchanged:** the other 159 `omn` blocks, byte-identical to the committed v35. This includes:
  - every block of sections 2, 3 and 4;
  - E-001 to E-067 except E-045;
  - INV-001 to INV-125;
  - the watch-point blocks of oscillation checks 12 to 32.
- **Tables:** every row of the catalogue, of C1–C3, of the source data tables SD-IC to SD-ET and of the traceability table is unchanged.
- **Added or removed:** no block.
