# Fix — iteration 37
Version produced: v37
Reviewed version: v36
Date: 2026-10-22

Input: [`reviews/review-iter-37.md`](../reviews/review-iter-37.md) (verdict REMARKS, one remark, R37-01). Every comparison uses the committed v36 as its baseline (`git show HEAD:docs/stage2-output-model/OUTPUT_MODEL.md` and `…/RATIONALE.md`).

Files written:
- `OUTPUT_MODEL.md` (v37): header `Version: v37 · Iteration: 37 · Status: under review`; one change-log entry.
- `history/v37.md` and `history/v37-rationale.md`: byte-identical copies of the two files.
- this log.

`RATIONALE.md` is unchanged. The fix needs no change there, for three reasons:
- it has no `OC-NN` entries;
- its `C1-NN`, `C2-NN` and `C3-NN` entries state only the v34 origin of each case row, and no case row changed;
- no entry describes what a catalogue cell contains.

The model's companion line therefore still reads `RATIONALE.md v36`.

Scripts (all run with `python3 -I`) are outside the repository, in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix37/scripts/`:
- `omntypes.py`: type hierarchy and attributes from the `omn` blocks;
- `catrows.py`: catalogue rows and case-table keys;
- `applies.py`: which output-wide invariants apply to each row;
- `apply37.py` to `apply37e.py`: exact string replacements, each required to match once;
- `verify37.py`: the catalogue check;
- `checks37.py`, `trace.py` and `bal.py`: general checks, adapted from fix 36.

The outputs of `applies.py` are `fix37/applies-v36.txt` and `fix37/applies-v37.txt`.

## 1. Summary

| Remark | Verified | Disposition | Places changed |
|---|---|---|---|
| R37-01: rule stated per case in the output catalogue | yes, by script (`applies.py`, `verify37.py`) | fixed, option (a) of the review | section 4.2 (the definitions of Availability, Shown with it and Prohibited; new paragraph "Stated once for all rows"); section 4.3 (abbreviation line; 38 cells in 34 rows); section 12 |

Unchanged:
- every `omn` block (all 160 byte-identical to v36);
- every case-table row, source-data row, level, Realises field and traceability row;
- every quote;
- `RATIONALE.md`.

## 2. R37-01: the catalogue restates generic invariants row by row

### Verification

**Method.** For each of the 45 rows, `applies.py` determines which output-wide invariants apply to the row's element kinds by their predicates. It uses two inputs:
- **The type hierarchy of the `omn` blocks.** For example, E-051 `AcuteTreatmentSummary` and E-064 `ClusterAttackRate` extend `PeriodValue`, and the kinds of E-027 are an `EventCount` and a `DurationSummary`.
- **The quantifier types of each predicate:**
  - INV-003: every view; every item that refers to a period; `referencedValues`.
  - INV-006: `DayCount`, `EventCount`.
  - INV-008 (`reports`):
    - the four labelled measures and `referencedValues`;
    - a peak-intensity distribution and the migraine-free mark;
    - cycle lines, cluster attack rates and trigger views;
    - the views whose content invariants ask for such values: INV-035, INV-050, INV-068, INV-070, INV-104, INV-105, and the series of E-038.
  - INV-011: every `PeriodValue` except a completeness indicator; `referencedValues`; adherence windows; views with cycle lines, cluster phases or trigger co-occurrence.
  - INV-121: the kinds in `daysWithin`, and the total time with moderate/severe pain.
  - INV-122: every `DayCount` measure except `migraineOrModerateSevereHeadacheDays`, which is in no `nestedIn` pair and not in the per-type list; and `EventCount`.
  - INV-123: the kinds in `factsShown`.

The script then compares this with what each row's Availability and Shown with it cells name: by ID, by the keys "label" and "completeness", or in the "def." list.

**Result on v36.** The remark is confirmed, and the class is wider than the review lists.

| Invariant | Rows to which it applies | Rows that named it in v36 |
|---|---|---|
| INV-003 | 39 | 5: OC-01, OC-02, OC-19, OC-21, OC-33 |
| INV-006 | 11 | 1: OC-05 |
| INV-008 | 22 | 10: OC-03 (as its own availability), OC-05 to OC-09, OC-11, OC-19, OC-36, OC-38 |
| INV-011 | 33 | 13: OC-04 (as its own availability), OC-01, OC-05 to OC-09, OC-15, OC-16, OC-19, OC-25, OC-36, OC-38 |
| INV-121 | 13 | 7: OC-04, OC-05, OC-11, OC-12, OC-13, OC-32, OC-42 |
| INV-122 | 10 | 5: OC-05, OC-09, OC-15, OC-32, OC-35 |
| INV-123 | 14 | 12: OC-15 (in Availability), and OC-10, OC-18, OC-21, OC-23, OC-25 to OC-29, OC-31, OC-39 (in Shown with it) |

In v36, 91 pairs of a row and an invariant applied without the row naming the invariant. They lie in 37 rows. Every case that the review lists is among them. The script also found cases that the review does not list:
- **OC-37.** The cluster view shows attack rates, which are `PeriodValue`s and report attacks (INV-008, INV-011 first conjunct), and cluster and remission periods (INV-011 fourth conjunct). Its cell named neither label nor completeness.
- **OC-27.** INV-070 asks for headache days and migraine days in the post-stop monitoring view, so INV-008 and INV-011 apply.
- **OC-35.** INV-006, INV-008, INV-011, INV-121 and INV-123 apply; INV-123 applies through `usedScope` of the per-type acute-medication days. Only INV-122 was named.
- **OC-42.** INV-006, INV-011 and INV-122 apply to school days, which are `FunctionalImpactDays`. INV-123 applies to the PedMIDAS results (E-058). Only INV-121 was named.
- **OC-14.** Aura counts are `EventCount`s, so INV-006 and INV-122 apply. The cell read "MAY (no invariant)".
- **OC-24.** INV-003, INV-006, INV-011 and INV-121 apply, and none was named. INV-122 does not apply.
- **OC-16, OC-17, OC-30.** INV-003 applies.
- **Placement of INV-123.** OC-15 named INV-123 in Availability; the other eleven rows named it in Shown with it.

The same class also appears in two places outside the two columns that the review names. They were found by the sweep (below):
- **Prohibited.** OC-45 listed C2-01, C2-02, C2-05 and C2-07, whose bearers are all elements. These cases belong to other rows: their key `r` is `oc01`, `oc04`, `oc21` and `oc28`. No other row on whose elements they bear listed them.
- **Shown with it, placement.** Section 2.5 and the section 6.0 index name the constructs that place references:
  - **The W2 markers.** 12 elements carry them, and every one is named in its row.
  - **INV-078, INV-060 and INV-087.** INV-078 was named, in OC-29. INV-060 and INV-087 were not named in OC-22 and OC-36.
  - **INV-003**, which places in one view every two items that refer to the same period atom. OC-21 restated this consequence (with INV-056) and OC-33 restated it (with INV-038). The same consequence of INV-045 (OC-17), INV-115 (OC-43) and INV-062 (OC-23) was not listed. For INV-062 the W2 markers of E-046 ask for the same placement at the same level.

### The list of output-wide invariants, determined by predicate

| Invariant | Quantifies over |
|---|---|
| INV-003, INV-006, INV-008, INV-011, INV-122 | every view (`∀ v : View`) |
| INV-121 | every per-period value (`∀ x : PeriodValue`; `DurationSummary` is a subtype) |
| INV-123 | every element (`∀ x : Element`) |

Each constrains the kinds of between 10 and 39 rows (table above). The list equals the review's list.

Considered and kept row-specific:
- **INV-002, INV-004, INV-012, INV-111.** Each quantifies over the kind of one row (`Period`, `Series`, `CompletenessIndicator`, `DefinitionLabel`), and that row names it (OC-01, OC-02, OC-04, OC-03).
- **INV-124.** It quantifies over `CycleLine` and `ClusterPhaseItem`, the kinds of OC-36 and OC-37, and both rows name it.
- **INV-118, INV-119, INV-120, INV-125.** These are level-indexed. Each case or SD-DF row belongs to one row and is named there:
  - C1 cases in Availability;
  - C2 cases in Prohibited;
  - C3 cases in Shown with it;
  - SD-DF-01 and SD-DF-02 in OC-03, OC-05 and OC-08.
- **INV-104, INV-105, INV-069 and the other content invariants of a view kind.** Each asks for the kinds of other rows inside one view kind. A row names one only where it states the level of the row's own kind. That holds for OC-09 (SHOULD in the clinician-facing summary, where the kind is otherwise MAY) and for OC-25 (no availability invariant of its own). These entries are levels, not restatements.
- **INV-001.** It constrains contexts and belongs to no row.

### Disposition: fixed, with option (a)

**Why (a).** PROCESS.md section 6a, "State a rule once":
- Option (b) would add the 91 missing pairs to the rows and keep them consistent by hand.
- Option (a) makes the rows consistent by construction.

**Why (b) is not required:**
- **The catalogue is an index without formal force** (section 4.2, second paragraph).
- **The plan's column definitions are informative.** `restructure/plan-v35.md` fixes the section layout and the columns. Both are unchanged; only what three columns contain changes, and section 6a governs that.
- **No watch point concerns these columns.**

### What changed

**Section 4.2, column definitions** (lines 313–315):

| Column | v36 | v37 |
|---|---|---|
| Availability | the level and the item that states it (`INV-NNN`, `C1-NN`), and the definitional invariants of the kind | the levels of the kind and of its content, with the items that state them (`INV-NNN`, `C1-NN`); after "def.", the definitional invariants whose Conformance field names an element of the row, except those stated once below |
| Shown with it | companions, by ID: periods (INV-003), definition labels (INV-008, "label"), completeness (INV-011, "completeness"), placement markers (W2), C3 cases, specific companions, shown context facts (INV-123) | companions specific to the row, by ID: the placement of its elements' references by W2 markers and by INV-060, INV-078 and INV-087 (section 6.0), the C3 cases of the row, the definition that SD-DF fixes for its label (INV-125), and other content that an item specific to the row asks for next to it (for example the scale of E-023, INV-056, INV-066) |
| Prohibited | C2 cases, and INV-091 | the C2 cases of the row, and INV-091 |

The Availability definition now states how the "def." list is formed: by the invariant's Conformance field, as section 3.3, item 5 specifies. It also covers the content levels that the cells already gave ("content SHOULD (INV-050)").

**Section 4.2, new paragraph** (line 318):

> **Stated once for all rows.** INV-003, INV-006, INV-008, INV-011 and INV-122 quantify over every view, INV-121 over every per-period value and INV-123 over every element. They apply, as their Conformance fields state, to the elements of every row wherever their predicates apply, and the rows do not repeat them; a row names one of them only as the item that states the level of its own kind (INV-003 in OC-01, INV-008 in OC-03, INV-011 in OC-04). INV-003 also places in one view every two items that refer to the same period atom (INV-003 Notes; section 2.5), and so places in the view of their holder, for example, the values of a comparison (INV-038, INV-056), the basis of a medication-overuse indicator (INV-045) and the components of a composite index for migraine (INV-115); a row that names such a companion cites an item specific to the row, not INV-003. A case of table C2 or C3 is named in the row that its key `r` names; its bearers are the elements that its cell names, and they may belong to other rows (the bearers of C2-01, C2-02, C2-05 and C2-07 are all elements, and those of C3-01 all views).

Every claim in the paragraph was checked against the formal text:
- **The quantifiers** are those of the seven predicates.
- **The three exceptions** are the only places where a row names one of the seven invariants (`verify37.py`).
- **The placement sentence** rests on the INV-003 Notes and on these ties:
  - INV-038: `m.period ∈ ran pc.periods`;
  - INV-056: `m.period ∈ {rc.baseline} ∪ ran rc.onTreatment`;
  - INV-045: `i.basis(j).period = i.span(j)`;
  - INV-115: `m.period = x.period`, for migraine.
- **The bearers** are those in the cells of C2-01, C2-02, C2-05 and C2-07 (`Element`) and of C3-01 (`View`).

**Section 4.3, abbreviation line** (line 324). `Abbreviations: "label" = INV-008, "completeness" = INV-011, "def." = definitional.` becomes `Abbreviation: "def." = definitional.`

**Section 4.3, cells.** The Output kind, Audience, Period and granularity, Applicability and Realises cells of every row are unchanged.

| Row (line) | Column | v36 | v37 | Reason |
|---|---|---|---|---|
| OC-01 (328) | Shown with it | its periods (INV-003); caveats C3-01; completeness | caveats C3-01 | INV-003, INV-011 stated once |
| OC-02 (329) | Shown with it | its periods (INV-003) | — | INV-003 stated once |
| OC-04 (331) | Availability | SHOULD (INV-011); def. INV-012, INV-121 | SHOULD (INV-011); def. INV-012 | INV-121 stated once; INV-011 kept as its own availability |
| OC-05 (332) | Availability | MUST (C1-01); def. INV-006, INV-121, INV-122 | MUST (C1-01) | stated once |
| OC-05 (332) | Shown with it | label (fixed: SD-DF-01); completeness | the definition its label names (INV-125: SD-DF-01 MUST) | INV-008, INV-011 stated once; the SD-DF row kept |
| OC-06 (333) | Shown with it | label; completeness | — | stated once |
| OC-07 (334) | Shown with it | label; completeness | — | stated once |
| OC-08 (335) | Shown with it | label (fixed: SD-DF-02); completeness | the definition its label names (INV-125: SD-DF-02 SHOULD) | as OC-05 |
| OC-09 (336) | Availability | …; def. INV-031, INV-122 | …; def. INV-031 | INV-122 stated once |
| OC-09 (336) | Shown with it | exploratory label MAY (C3-02); label where a mark is shown; completeness | exploratory label MAY (C3-02) | INV-008, INV-011 stated once |
| OC-10 (337) | Shown with it | series and markers (W2 SHOULD, E-035); marker facts (INV-123) | series and markers (W2 SHOULD, E-035) | INV-123 stated once |
| OC-11 (338) | Availability | …; def. INV-032, INV-121 | …; def. INV-032 | INV-121 stated once |
| OC-11 (338) | Shown with it | scale SHOULD (E-023); label where a distribution is shown | scale SHOULD (E-023) | INV-008 stated once |
| OC-12 (339) | Availability | SHOULD (C1-08); def. INV-121 | SHOULD (C1-08) | stated once |
| OC-13 (340) | Availability | SHOULD (C1-09); def. INV-033, INV-121 | SHOULD (C1-09); def. INV-033 | stated once |
| OC-14 (341) | Availability | MAY (no invariant) | MAY | "(no invariant)" was false (INV-006, INV-122 apply to aura counts); now as the other MAY rows (OC-30, OC-38) |
| OC-15 (342) | Availability | MUST (C1-10); def. INV-024, INV-122; usage fact (INV-123) | MUST (C1-10); def. INV-024 | stated once |
| OC-15 (342) | Shown with it | completeness | — | stated once |
| OC-16 (343) | Shown with it | completeness | — | stated once |
| OC-18 (345) | Shown with it | …; start fact (INV-123) | series (W2 SHOULD); worsening label (C3-06) | stated once |
| OC-19 (346) | Shown with it | the two values, in a response comparison (W2 MUST); periods (INV-003); residual burden (INV-060); label; completeness | the two values, in a response comparison (W2 MUST); residual burden (INV-060) | stated once |
| OC-21 (348) | Shown with it | values and changes (INV-003, INV-056, W2); …; start fact (INV-123) | values and changes (INV-056, W2); … | INV-003 placement and INV-123 stated once |
| OC-22 (349) | Shown with it | — | its change and its two day counts, in one view, for the burden that INV-060 asks for next to a percentage change (INV-060) | placement by INV-060 (section 6.0), now named as INV-078's is in OC-29 |
| OC-23 (350) | Shown with it | …; treatment fact (INV-123) | comparison, residual burden, other values (W2 SHOULD); clinical-interpretation caveat (C3-07) | stated once |
| OC-25 (352) | Shown with it | completeness of its window; treatment fact (INV-123) | — | INV-011 (third conjunct), INV-123 stated once |
| OC-26 (353) | Shown with it | treatment fact (INV-123) | — | stated once |
| OC-27 (354) | Shown with it | event fact (INV-123) | — | stated once |
| OC-28 (355) | Shown with it | …; medication fact of lines (INV-123) | outcome summaries and lines (W2 SHOULD) | stated once |
| OC-29 (356) | Shown with it | …; course facts (INV-123) | groups (W2 SHOULD) and their lines (INV-078); response summaries and adherence (W2 SHOULD) | stated once |
| OC-31 (358) | Shown with it | …; availability fact (INV-123) | clinical-interpretation caveat where a category is shown (C3-08) | stated once |
| OC-32 (359) | Availability | …; def. INV-121, INV-122 | SHOULD (C1-12); comparison with the baseline period SHOULD (INV-027) | stated once |
| OC-33 (360) | Shown with it | values in its view (INV-038 with INV-003) | its values, of the compared periods (E-037, INV-038) | INV-003 placement stated once; the values (E-037 `values`) and their tie (INV-038) kept |
| OC-35 (362) | Availability | …; def. INV-122 | MUST (C1-13); intensity SHOULD where provided (C1-14) | stated once |
| OC-36 (363) | Shown with it | attack marks (W2, def.); label; completeness | cycle lines (INV-087, def.); attack marks (W2, def.) | INV-008, INV-011 stated once; placement by INV-087 (section 6.0) named |
| OC-38 (365) | Shown with it | caveats C3-09; label; completeness | caveats C3-09 | stated once |
| OC-39 (366) | Shown with it | …; availability fact (INV-123) | clinical-interpretation caveat (C3-10) | stated once |
| OC-42 (369) | Availability | SHOULD (INV-096, INV-097); def. INV-121 | SHOULD (INV-096, INV-097); def. INV-082 | INV-121 stated once; INV-082 is definitional for E-058 (PedMIDAS results), which the row names |
| OC-45 (372) | Prohibited | the C2 cells whose bearer is every element (C2-01, C2-02, C2-05, C2-07) | — | no C2 case is keyed to `oc45`; the bearers are stated once in section 4.2 (and in E-004 Conformance and section 3.7) |

All other content of these rows is unchanged. Each removed entry is either covered by the new paragraph or corrected:
- every removed ID or key is one of the seven output-wide invariants, or a C2 case covered by the bearer sentence (`verify37.py`);
- the removed phrase "(no invariant)" was a false claim.

The six added entries are row-specific:
- INV-125 in OC-05 and OC-08: the SD-DF rows, reworded;
- INV-060 in OC-22 and INV-087 in OC-36: placements;
- E-037 in OC-33: the values attribute that INV-038 ties;
- INV-082 in OC-42: the "def." list by the column's definition.

### Class and sweep

**Class.** A catalogue cell that restates, row by row, a rule that applies to the kinds of several rows, so that rows of the same kind differ or miss cases. Such a rule can be:
- an output-wide invariant;
- a consequence of one (INV-003's placement of items that refer to the same period atom);
- a case whose bearers reach beyond its row (C2 and C3);
- the placement rule of section 2.5.

**Swept:** all 9 columns of all 45 rows, and the 16 case-table captions.

| Place | Result |
|---|---|
| Availability | Fixed. Output-wide invariants removed (14 IDs in 10 cells). "def." lists recomputed from the invariants' Conformance fields: equal in all 45 rows; OC-42 gains INV-082. OC-14's "(no invariant)" removed. The C1 cases (14 of 14) and the level items are each in the row that their key or subject names. |
| Shown with it | Fixed. Removed: "label" and "completeness" (21 keys), INV-003 (5) and INV-123 (11). Now complete in its closed categories: the 12 W2-marked elements, the three placement invariants and the 12 C3 cases, each in its row (C3 by key), and the two SD-DF rows. |
| Prohibited | Fixed. Only C2 cases keyed to the row, and INV-091 in OC-43. OC-45 → "—". |
| Applicability | Not in the class. Each cell gives the row's own condition. R-MCF is cited by reference, the form that section 3.8 prescribes ("cite "R-MCF (n)" … and do not restate it"). The 7 citations (OC-21, OC-26, OC-27, OC-30, OC-31, OC-33, OC-39) each name the clause that fits their condition. Unchanged. |
| Output kind, Audience, Period and granularity, Realises | No generic rule restated. Unchanged. Realises re-checked: every requirement is still realised by an item named in its row. |
| Case-table captions (16) | All in the form "Case table <ID> — <form>" of section 2.11. No caption restates a rule. The 7 "read by INV-NNN" pointers are references, and each is true: INV-118 uses `ppGranularities` and `ppRequired`; INV-119 `prohibitedClaims`; INV-120 `requiredAnnotations`; INV-125 `fixedDefinition` and `fixedDefinitionLevel`; INV-064 `inControlRange`, `controlMinMonths` and `forcedAbove`; INV-085 `screeningMax`; INV-073 `earlyTimePointType`. Unchanged. |

### Examined and not changed

- **Element Conformance fields** (for example E-003, E-004, E-011, E-014, E-040) also name output-wide invariants and the C2 cases that bear on every element. These are the elements' own fields, outside the catalogue and outside this sweep. They agree with the new paragraph.
- **OC-43** names the placement of the components by the W2 marker of E-033, at SHOULD. INV-115 ties the components (for migraine) to the index's own period atom, so INV-003 also places them; the new paragraph names this as an example. The cell is true as written, and no formal block changed. INV-115/D01 ("It makes nothing more required: `components` stays SHOULD for migraine") speaks of whether the components are present, and does not contradict this.
- **OC-23.** INV-062 ties the label's other values and comparison to the label's `evaluated` periods. The resulting placement through INV-003 has the level of INV-062 (SHOULD), the same as the W2 markers that the cell names. It is covered by the paragraph's placement sentence.
- **`RATIONALE.md`.** SEC-3.8/D01 mentions "the start fact of a response comparison (INV-123 …)" and "the availability facts of INV-123". Both describe the invariant, not catalogue cells.

## 3. Every changed location

Line numbers are those of v37.

| # | File | Line | Place | Change |
|---|---|---|---|---|
| 1 | model | 2 | header | v36 → v37, iteration 37 |
| 2 | model | 313 | 4.2, Availability definition | as section 2 |
| 3 | model | 314 | 4.2, Shown with it definition | as section 2 |
| 4 | model | 315 | 4.2, Prohibited definition | as section 2 |
| 5 | model | 318 | 4.2, new paragraph "Stated once for all rows" | new |
| 6 | model | 324 | 4.3, abbreviation line | "label" and "completeness" removed |
| 7–40 | model | 328–372 | 4.3, rows OC-01, 02, 04 to 16, 18, 19, 21 to 23, 25 to 29, 31 to 33, 35, 36, 38, 39, 42, 45 | 38 cells (11 Availability, 26 Shown with it, 1 Prohibited), as the table in section 2 |
| 41 | model | 3849 | section 12 | v37 entry |
| 42 | `history/v37.md` | — | snapshot | copy of `OUTPUT_MODEL.md` |
| 43 | `history/v37-rationale.md` | — | snapshot | copy of `RATIONALE.md` (unchanged, identical to `history/v36-rationale.md`) |

## 4. Checks

All checks were run on the files as written.

| Check | Result |
|---|---|
| Formal identity against HEAD (`checks37.py`) | 160 `omn` blocks in HEAD and v37, 0 differing. All 161 fenced blocks identical, including the plain relations sketch of section 4.1 |
| Brace balance | 160 `omn` blocks, 0 unbalanced in `{}`, `()`, `[]`, `⟨⟩`. 1,508 backticked spans (v36: 1,505), of which 1 is unbalanced in both versions. That one is a regex artefact in section 2.11 prose (text between two code spans), not a formal cell |
| IDs, model → items | headings E 67, INV 87, ISS 12, no duplicates; 192 E/INV/ISS IDs referenced, 0 unresolved |
| IDs, `RATIONALE.md` → items | 180 referenced, 0 unresolved |
| Row IDs, both files | 174 rows (OC, C1–C3, SD), 0 unresolved in either file |
| `RATIONALE.md` entries, both directions | 434 entries (113 Q), no duplicates. 364 entry IDs referenced from the model and 399 from `RATIONALE.md`, 0 unresolved. Every entry except the search-log, case-row and section entries is referenced from the model (as in v36) |
| Evidence pointers | every `[S-NNN] <entry>` pair names an entry whose Source lines include S-NNN. The two entries with extra reference lines (E-041/Q29, E-057/Q10) are as in v36 (fix 36, section 2) |
| Traceability (`trace.py`) | section 7 recomputed from the Realises fields: 0 differences in all 39 rows |
| Catalogue Realises (`trace.py`) | after the removals, every requirement in a row's Realises is in the Realises of an item named in the row; every requirement is in some row. Same result as v36 |
| Catalogue cells (`verify37.py`) | All pass. The 4.2 paragraph lists exactly the seven output-wide invariants. A row names one of them only in OC-01, OC-03, OC-04 (Availability); no "label" or "completeness" key remains. "def." equals the computed list in all 45 rows. Every Shown with it entry is classified as W2, placement invariant, C3 case keyed to the row, SD-DF row, or a listed row-specific item. Every W2-marked element (12), placement invariant (3) and C3 case (12) appears in its row. Prohibited equals the keyed C2 cases (and INV-091 for OC-43) in all 45 rows. All 56 removed tokens are covered by the 4.2 paragraph or were false ("(no invariant)") |
| Applicability by predicate (`applies.py`) | v37: the only output-wide invariants that rows name are INV-003 (OC-01), INV-008 (OC-03) and INV-011 (OC-04). Every other applicable pair (141) is covered by the 4.2 statement |
| Quotes | 706 distinct double-quoted strings of the HEAD model and `RATIONALE.md`, all present in v37; no new quoted string; `RATIONALE.md` byte-identical to v36 |
| Scope | counts of JSON, FHIR, database, recorded, entered, captured, storage, stored, XML, CSV, algorithm in model + `RATIONALE.md` unchanged. No input, storage or derivation-from-input text added |
| Satisfiability | not needed: no formal block, case row or source-data row changed |
| Header | `Version: v37 · Iteration: 37 · Status: under review` |
| Snapshots | `cmp OUTPUT_MODEL.md history/v37.md` and `cmp RATIONALE.md history/v37-rationale.md`: identical |

## 5. Diff summary of the formal blocks, and size

- **Formal blocks.** None changed or added: all 160 `omn` blocks are byte-identical to v36.
- **Tables.**
  - No case-table row (C1, C2, C3), source-data row or traceability row changed.
  - The catalogue has 45 rows in v36 and v37. 38 informative cells in 34 rows changed. Their Output kind, Audience, Period and granularity, Applicability and Realises cells are unchanged.
- **Meaning.** No change. The catalogue has no formal force (section 4.2). The new paragraph and column definitions state only what the predicates, Conformance fields and case-table keys give.
- **Watch points** (check after iteration 36): none reversed.
  - WP 3 (INV-123): membership and level untouched; only per-row index mentions removed.
  - WP 1 (INV-060, ISS-13): the OC-22 cell names INV-060's placement and refers to "the burden that INV-060 asks for", not to its antecedent.
  - WP 2: OC-09 keeps INV-031.
  - WP 12 (bookkeeping after the restructuring): this fix closes the class by stating once, as the review's option (a) intended, rather than adding per-row entries.
  - WP 13: 0 formal changes.

Size:

| Part | v36 (bytes / lines) | v37 (bytes / lines) | Change |
|---|---|---|---|
| Section 4 (whole) | 27,605 / 163 | 28,343 / 165 | +738 B |
| 4.2 Catalogue: row IDs and columns | 2,158 / 20 | 3,553 / 22 | +1,395 B (new paragraph, column definitions) |
| 4.3 The catalogue | 14,821 / 52 | 14,164 / 52 | −657 B |
| 4.4 Formal columns | 7,840 / 64 | 7,840 / 64 | 0 |
| Section 12 (change log) | 16,025 / 42 | 16,666 / 43 | +641 B |
| `OUTPUT_MODEL.md` and `history/v37.md` | 421,917 / 3,846 | 423,296 / 3,849 | +1,379 B (+0.33 %) |
| `RATIONALE.md` and `history/v37-rationale.md` | 322,333 | 322,333 | 0 |

In the catalogue table:

| Measure | v36 | v37 |
|---|---|---|
| ID mentions, Availability (45 cells) | 119 | 106 |
| ID mentions, Shown with it | 53 | 43 |
| ID mentions, Prohibited | 14 | 10 |
| "label" / "completeness" keys | 21 | 0 |
| Rows naming INV-003 | 5 | 1 |
| Rows naming INV-006 | 1 | 0 |
| Rows naming INV-121 | 7 | 0 |
| Rows naming INV-122 | 5 | 0 |
| Rows naming INV-123 | 12 | 0 |
| Bytes of the Availability cells | 2,355 | 2,190 |
| Bytes of the Shown with it cells | 1,786 | 1,408 |
| Bytes of the Prohibited cells | 259 | 191 |

The table shrinks. Section 4 as a whole grows by 738 B, because the rule is now stated once in 4.2, and the column definitions say exactly what each column holds.
