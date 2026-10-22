# Fix — iteration 39
Version produced: v39
Reviewed version: v38
Date: 2026-10-22

Input: [`reviews/review-iter-39.md`](../reviews/review-iter-39.md) (verdict REMARKS, one remark: R39-01). Every comparison uses the committed v38 as its baseline (`git show HEAD:docs/stage2-output-model/OUTPUT_MODEL.md` and `…/RATIONALE.md`). The class sweep compares `history/v34.md` with v38, using the mapping of `fixes/fix-iter-35.md`, section 4.

Files written:
- `OUTPUT_MODEL.md` (v39, 430,136 bytes): header `Version: v39 · Iteration: 39 · Status: under review`; `Companion: RATIONALE.md v39`; one change-log entry.
- `RATIONALE.md` (v39, 332,923 bytes): header `Version: v39 (companion of OUTPUT_MODEL.md v39)`; three new entries.
- `history/v39.md` and `history/v39-rationale.md`: byte-identical copies of the two files.
- this log.

No web search, no download and no new source. The search log of `RATIONALE.md` is unchanged.

Scripts (all run with `python3 -I`) are outside the repository, in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix39/scripts/`:
- `parse.py`: splits a model snapshot into items and fields, `omn` blocks and sentences, and `RATIONALE.md` into entries;
- `sweep.py`, `sweep_moved.py`, `sweep_sections.py` (with `sweep_lib.py`): the class sweep (section 3);
- `views.py`: every `View` subtype with its attributes, and the invariants and case rows that name it;
- `apply39_model.py` and `apply39_rat.py`: exact string replacements, each required to match the stated number of times;
- `witness39.py`: the satisfiability witness and mutation tests (section 5);
- `ids_trace.py` and `names.py` (the reviewer's scripts of review 39), `entries.py`, `blocks39.py`, `catalogue39.py`: the general checks.

The outputs are in `fix39/out/`: `sweep_candidates.txt`, `sweep_content_nomissing.txt`, `sweep_nocontent.txt`, `sweep_moved.txt`, `sweep_sections.txt`, `witness39.txt` and `checks-v39.txt`.

## 1. Summary

| Remark | Verified | Disposition | Places changed |
|---|---|---|---|
| R39-01: OUT-025's "the frequency, disability and treatment-history outputs for those windows" has no formal representation; the E-056 Meaning claims it; the OUT-025 row says "full" without a line for it; the Realises fields are inconsistent | yes: Stage 1 text; `history/v00.md` to `history/v34.md`; `views.py` on v38 | fixed, option (a) of the review | E-056 (`omn` block, Meaning, Conformance, Notes); INV-080 (title, `omn` block, Reading, Notes); section 6.0 marker list; Realises of E-015, E-016, E-017, E-019, E-046, E-055; catalogue rows OC-05 to OC-08, OC-23, OC-29, OC-30; traceability row OUT-025; ISS-04; `RATIONALE.md` E-056/D02, E-056/S01, E-056/X01 |

**Class sweep.** The sweep covered every Meaning, Conformance, Reading and Notes sentence of the 184 v34 elements and invariants (1,536 sentences), the v34 prose of sections 1 to 4 and the 39 v34 coverage reasons. It found **one** Stage 1 statement part that v35 left without representation: the E-056 Conformance sentence of R39-01. Every other sentence that stated output content, a level or an applicability condition is still stated by the v38 formal text. No other statement part needed restoring.

Unchanged:
- every quote, source-data row, case-table row (C1, C2, C3) and section 8 issue other than ISS-04;
- every level of an existing element, attribute or invariant;
- 158 of the 160 `omn` blocks, byte-identical to v38.

## 2. R39-01: the content of the scheme-window view

### Verification

**What Stage 1 states.** The OUT-025 Statement (Stage 1 v18) reads: "The diary output MAY allow the clinician to select evaluation windows defined by national reimbursement or monitoring schemes (for example specified treatment weeks, the three months preceding an application, month-by-month responder views, or six-monthly reassessments) and to show the frequency, disability and treatment-history outputs for those windows, labelled with the name of the scheme."
- The Evidence basis ends "Strength: MAY". There is one strength for the whole Statement, so each of its three parts is MAY. The level the review proposes is the Stage 1 level.
- The Caveats state that scheme criteria "are not requirements of this document".

**What v38 represents.** Each point of the review holds:
- **Part 1 (selection of windows):** `OutputContext.schemeSelection` (E-007), E-056 `windows` and INV-080.
- **Part 3 (label):** E-056 `scheme` ("shown as the label of the view") and INV-080.
- **Part 2 (outputs for the windows):** nothing formal. `SchemeWindowView` declared only `scheme` and `windows`, and INV-080 constrained only these two. A view with no other content was an instance of E-056.
- **Other views.** `views.py` lists every subtype of `View`. Each states its content through attributes or invariants:
  - E-035: INV-034, INV-035;
  - E-036: a type defined by its series;
  - E-038: INV-040 to INV-042;
  - E-039: INV-049 to INV-051;
  - E-048: INV-068, INV-069, INV-102;
  - E-049: INV-070, INV-103, INV-112;
  - E-054: INV-077, INV-078;
  - E-060: INV-086, INV-087;
  - E-062: its attributes and INV-088;
  - E-065: its core attributes and INV-110;
  - E-066: INV-094, INV-104;
  - E-067: INV-095, INV-105.

  E-056 had none. This confirms the class of the review ("a view kind whose Stage 1 content is stated only in prose"): **E-056 is its only member.**
- **Meaning.** The E-056 Meaning claimed content the formal text did not state (prose overclaim).
- **Traceability.**
  - Row OUT-025 said "full" with one line, "evaluation windows of a scheme, labelled with the scheme (MAY)", and no line for part 2.
  - Its columns listed E-046 and E-058 (and OC-23, OC-31), which no item tied to the scheme-window view.
  - The frequency elements and the treatment-history elements did not list OUT-025.

**History.**
- `history/v00.md` to `history/v34.md` give E-056 the Conformance sentence "Its content (headache days and migraine days per window, instrument results, treatment lines, responder labels) is MAY." It was never formalised.
- The template for element Conformance fields (plan-v35, section 9.1) dropped every sentence outside the template, and the mapping of fix 35 records E-056 as "kept; formal text unchanged".
- No review, fix, audit or oscillation check discussed the view's content. No watch point of the check after iteration 36 names E-056, INV-080 or OUT-025.
- The fix therefore reverses no decision.

### Disposition: fixed, option (a)

The content can be represented without narrowing OUT-025, so option (b) does not apply. The part is formalised at MAY: it asks for nothing and fixes the type and meaning of the content (model section 3.2). It reuses existing elements and existing generic mechanisms: the placement markers of rule W2, the period tie `sameSpan`, R-MCF (3) and the catalogue. No new predicate, function, element type or case row is added.

**Content attributes (E-056).** Three reference attributes of level MAY, each with the definitional placement marker `shown` (rule W2), so that what they reference is part of the view:

```
frequencyValues : set →PeriodValue  MAY  shown           -- frequency outputs for the windows (INV-080)
instrumentResults : set →InstrumentResult  MAY  shown    -- disability outputs: results of validated instruments
treatmentLines : set →TreatmentLine  MAY  shown          -- treatment-history outputs
```

- **Frequency outputs.** These are read as the frequency measures of OUT-004 to OUT-007: headache days, migraine days, moderate/severe headache days and attacks. This is the reading the model already uses for OUT-001's "frequency outputs" (section 3.4) and that ISS-04 puts to the human. ISS-04 now says that OUT-025's frequency outputs follow it.
- **Disability outputs.** These are the results of validated impact, disability and quality-of-life instruments (OUT-026, whose title names "disability", and E-058). OUT-027 ("Functional impact and lost productive time") is not called disability in Stage 1. Like every other content, its values may still be shown in the view (open world, section 3.7).
- **Treatment-history outputs.** These are the treatment lines of OUT-024 (E-055), as in the v34 prose.

**The tie (INV-080, definitional).** The first conjunct is kept verbatim, now in parentheses. A second conjunct is added:

```
∀ m ∈ v.frequencyValues • m ∈ HeadacheDays ∪ MigraineDays ∪ ModerateSevereHeadacheDays ∪ AttackCount ∧
  ∃ w ∈ ran v.windows • sameSpan(m.period, spanOf(w))
```

A frequency output for a window is a count of one of the four measures for a period with the dates of that window. The tie is by dates, as the model relates periods elsewhere: `sameSpan`, as in INV-006, INV-122 and the first conjunct of INV-080 itself. A month-by-month presentation is a selection of monthly windows: a selection admits any number of windows with any dates (E-007; INV-001 states no condition on them).

**No tie for instrument results and treatment lines.** These are related to the windows only by being shown in the view that shows the windows and carries the scheme's label. The review asks to tie them "only as far as OUT-025's 'for those windows' can be read without inventing scheme rules":
- Stage 1 states no date relation for them.
- The schemes it quotes relate them to their windows in different ways. Kela [S-039] asks for the previous treatment and its results. AIFA [S-040] uses a MIDAS score, whose recall is 3 months (SD-IN-01).
- Any date relation would be a scheme criterion, which the Caveats exclude (E-056/D01).

E-056/D02 and E-056/X01 record the reading and the rejected alternatives.

**Responder labels.** v34 listed them as content. OUT-025 does not:
- "month-by-month responder views" is one of its examples of an evaluation window that a scheme defines;
- a label under a scheme's own responder rule would apply a scheme criterion (E-045/N02).

They are not content of the view, and E-046 no longer realises OUT-025.

**Realises.** The kinds that the view shows now realise OUT-025: E-015, E-016, E-017, E-019 (`AttackCount`), E-055 and E-058 (unchanged). OUT-025's statement names them, which is the catalogue's rule for the Realises column (section 4.2). The trace of OUT-025 therefore runs through E-056's content, as option (a) asks, and is consistent within the requirement. The Realises fields of the other view requirements (OUT-021, OUT-028, OUT-034, OUT-035) are not changed:
- their content is formal;
- each statement part has a coverage line that names the items that state it;
- reviews 36 to 39 judged each of these requirements "ok" in their requirement-by-requirement fidelity tables;
- they are not part of this remark's class.

**Prose.**
- **E-056 Meaning:** what the view is, and that its frequency outputs are counts of the four measures for periods with the dates of a window, its disability outputs are instrument results and its treatment-history outputs are treatment lines, all shown in the view. It claims no date relation for the last two.
- **E-056 Conformance:** follows the template ("Placement: … (W2, definitional)"). The attribute levels stay in the declaration.
- **INV-080 Reading:** paraphrases both conjuncts.

### What changed, and where

- **E-056.**
  - `omn` block: three attribute lines added; the two existing lines are verbatim.
  - Meaning: rewritten to the formal text.
  - Conformance: adds "Placement: `frequencyValues`, `instrumentResults`, `treatmentLines` (W2, definitional)".
  - Notes: adds "See ISS-04" and the rationale entries E-056/D02, S01, X01.
  - Realises and Evidence are unchanged (OUT-025).
- **INV-080.**
  - Title: "Scheme windows are the selected windows, and frequency values are values of these windows".
  - `omn` block: the first conjunct verbatim, parenthesised; the second conjunct new.
  - Reading: a second sentence.
  - Notes: adds "Rationale: E-056/D02, E-056/S01".
  - Conformance (definitional, E-056), Realises and Evidence are unchanged.
- **Section 6.0, marker list:** new row "E-056 | `frequencyValues`, `instrumentResults`, `treatmentLines` | `shown` (definitional)".
- **Realises fields.** OUT-025 is added to E-015, E-016, E-017, E-019 and E-055, and removed from E-046.
- **Catalogue (section 4.3).**
  - OC-05, OC-06, OC-07, OC-08, OC-29: Realises cell gains OUT-025.
  - OC-23: Realises cell loses OUT-025.
  - OC-30, four cells:
    - Output kind: "Scheme-window view and the frequency, disability and treatment-history outputs it shows (E-056)";
    - Period and granularity: "the selected windows; frequency values: periods with the dates of a window (INV-080)";
    - Availability: "MAY; content MAY (E-056); def. INV-080";
    - Shown with it: "frequency values, instrument results and treatment lines (W2, def.)".
- **Traceability, row OUT-025.**
  - Catalogue rows: OC-05, OC-06, OC-07, OC-08, OC-29, OC-30, OC-31.
  - Elements: E-007, E-015, E-016, E-017, E-019, E-055, E-056, E-058.
  - Invariants: INV-080.
  - Coverage: "full", with one line for each of the three statement parts, each at MAY.
- **ISS-04.**
  - Effect on the model: one sentence, "The frequency outputs of the scheme-window view of OUT-025 (MAY) are read in the same way (E-056 `frequencyValues`, INV-080)".
  - For the human: a clause saying that the decision on OUT-001's frequency outputs also decides those of the scheme-window view.
- **Header and change log:** the v39 entry.
- **`RATIONALE.md`.**
  - Header.
  - New entries:
    - E-056/D02: the reading of the part, the reasons for the ties and for leaving responder labels out, and the Realises fields;
    - E-056/S01: satisfiability;
    - E-056/X01: rejected alternatives (a `within` tie; date ties for results and lines; responder labels).
  - E-056/D01 is unchanged.

## 3. The class: Stage 1 statement parts lost in the v35 restructuring

**Root cause.** The v35 restructuring rewrote element Conformance fields to a template. It dropped Meaning sentences "stating levels, applicability or other items' content" and dropped the Notes paragraphs marked R (plan-v35, sections 9.1 and 9.2). The equivalence check compared formal meaning only. A sentence that was the only representation of a Stage 1 statement part therefore disappeared without notice. So the sweep asks, for every v34 prose sentence that stated output content, a level or an applicability condition: does v38 still represent that content, formally or in prose that the formal text supports?

### Method

1. **Parse** (`parse.py`). The 184 v34 elements and invariants of `history/v34.md` (67 E, 117 INV) were split into fields, and the Meaning, Conformance, Reading and Notes fields into sentences: 1,536 sentences (Meaning 218, Conformance 367, Reading 185, Notes 766). Each v34 item was mapped to its v38 places by the table of `fixes/fix-iter-35.md`, section 4: a kept item to itself, a merged invariant to the generic invariant, case row or W2 element it went into.
2. **Kept or dropped** (`sweep.py`). Each sentence was compared with the whole of v38 and `RATIONALE.md`. IDs were masked, because moved text renames merged IDs. The measure is the share of its word 5-grams found there.
   - 1,130 sentences have a coverage of at least 0.8: they are kept in the model or moved verbatim.
   - 406 have a lower coverage: they were dropped or rewritten (Meaning 42, Conformance 128, Reading 86, Notes 150).
3. **Candidates** (`sweep.py`).
   - Of the 406, 267 contain content words (a level, "asks for", "required", "shows", "applies", "for each", "where provided", "available" and the like).
   - For each of these, the key terms were extracted: element and invariant IDs, OUT IDs, levels, code-formatted names, and the element kinds named by type name or by their natural phrase ("instrument results", "treatment lines", "responder labels").
   - Each term was looked up in the v38 places of the item and in their `RATIONALE.md` entries.
   - **80 candidates** have a key term without a counterpart there. 187 sentences have all their terms there.
4. **Moved text** (`sweep_moved.py`). Of the 1,130 kept or moved sentences, 104 are only in `RATIONALE.md` (coverage in the model below 0.8) and state a level or an ask. A Stage 1 part could have survived there only as rationale prose, so these were read too.
5. **Prose outside the items** (`sweep_sections.py`). The v34 prose of sections 1 to 4 has no dropped sentence with a level or an ask. The 39 v34 coverage reasons of section 7 were dropped as planned (plan-v35, section 9.3); the 40 of their sentences with a level or an ask were read.
6. **Reading.** All of these sentences were read against the v38 formal text: the 80 candidates, the other 187 content sentences, the 139 dropped sentences without content words, the 104 moved sentences and the 40 coverage sentences.

### The 80 candidates, with the verdict for each

"Verdict" names the v38 formal text that states the content of the sentence. Only candidate 43 states content that v38 does not represent.

| # | v34 item, field | Sentence (start) | Verdict: where v38 states it |
|---|---|---|---|
| 1 | E-001 Conformance | The prohibitions carry their own levels (MUST NOT, SHOULD NOT). | INV-119 is level-indexed; C2 rows carry MUST NOT / SHOULD NOT |
| 2 | E-008 Notes | Content aligned to the start itself is not shown for such a course, because the context gives no date to … | R-MCF (1) (section 3.8); E-055 `when` clauses, INV-079, INV-056, INV-068, E-049 `baseline`, INV-112 |
| 3 | E-008 Notes | Menstruation and age change with time and are dated: an output asks for the menstrual-relation view for a … | INV-086 (`menstruatesDuring`), INV-105, INV-039, INV-096, INV-097 (`childOn`, `childIn`), C3-11, E-041 `ageCovered` |
| 4 | E-010 Conformance | structural; each kind is required by the invariant that names it (INV-020, INV-047, INV-052, INV-090, … | INV-120 with table C3 |
| 5 | E-010 Conformance | `exploratoryMeasure` for OUT-008 measures is MAY (E-020 to E-022). | C3-02 (`may`) |
| 6 | E-010 Notes | Relations: INV-007 (an annotation is shown in the same view as what it qualifies). | W2: E-010 `qualifies` `shown` |
| 7 | E-011 Notes | With INV-008, a view that reports a measure SHOULD state exactly one definition for it (`labelledAs`), the … | INV-008, INV-111 (conjuncts 1 to 3) |
| 8 | E-013 Conformance | SHOULD for each reporting period of a summary measure that a view shows (INV-011): the period of every … | INV-011, its four conjuncts |
| 9 | E-013 Conformance | SHOULD NOT: presenting a fixed completeness cut-off as clinically validated (INV-013). | INV-119 (C2-02) |
| 10 | E-013 Notes | The treatment history view (E-054) lists treatments with their dates; the response summaries it shows … | consequence of INV-003 and INV-011 (not requirement content) |
| 11 | E-016 Notes | Relations: INV-031 (not more than the count of E-018 shown for the same period and scope, where the view's … | INV-031, second conjunct |
| 12 | E-018 Notes | Relations: INV-031 (in one view, for the same period and scope, the count is not lower than the migraine … | INV-031, second conjunct |
| 13 | E-020 Conformance | An `exploratoryMeasure` annotation MAY qualify it. | C3-02 (`may`) |
| 14 | E-021 Conformance | MAY, per reporting period; `exploratoryMeasure` annotation MAY. | C3-02 (`may`) |
| 15 | E-022 Conformance | MAY; `exploratoryMeasure` annotation MAY. | C3-02 (`may`) |
| 16 | E-022 Notes | Relations: INV-031 (where the view shows a migraine-day count for the marked period, or a period with its … | INV-031, third conjunct; the "marks every period" conjunct was removed by CHG-04 (intended change of v35) |
| 17 | E-023 Conformance | A view that shows a distribution of headache days by peak intensity reports headache days and SHOULD show … | `reports` (E-011), INV-008, INV-125 (SD-DF-01) |
| 18 | E-024 Conformance | SHOULD NOT: such a summary is presented as a stand-alone efficacy measure (INV-021, OUT-011 Caveats). | INV-119 (C2-03) |
| 19 | E-025 Conformance | SHOULD be available per reporting period for migraine, `hasType(ctx, c1)`, for each of the three symptoms, … | INV-118 (C1-09); INV-069 (`inSameForm`) |
| 20 | E-025 Notes | Relations: INV-033 (days with the symptom do not exceed the period length; attacks with the symptom do not … | INV-033; INV-121 |
| 21 | E-026 Conformance | SHOULD be available across periods for migraine, over all headache types combined (INV-022), also in the … | INV-118 (C1-09); INV-069 |
| 22 | E-032 Conformance | MUST be available per reporting period (calendar month or 28-day period), for each class of the subject's … | INV-044 (MUST) |
| 23 | E-032 Notes | The class indicators are given for every class of the acute medications that the subject has used up to … | E-008 `acuteMedications`; INV-044, INV-046 |
| 24 | E-033 Conformance | The view of an index states the periods of its component measures (INV-003) and SHOULD show their … | INV-003 (`referencedValues`), INV-008 (`reports`), INV-011 (second conjunct) |
| 25 | E-037 Conformance | Where the subject is a child or adolescent on the first day of one of the compared periods, the compared … | INV-097 |
| 26 | E-038 Conformance | SHOULD show the definitions it refers to: definition labels and the referenced codes (INV-042). | INV-042 |
| 27 | E-038 Conformance | SHOULD NOT assign a diagnosis (INV-043). | INV-119 (C2-08) |
| 28 | E-041 Conformance | structural (a value set); its use is MUST (E-042, INV-055, INV-059). | INV-055, INV-059 (MUST); W2 E-043 `timePoints` `shown MUST` |
| 29 | E-042 Notes | Relations: INV-058 (`earliest = shift(anchorDate, rule.minOffset)`; `latest = shift(anchorDate, … | INV-058 |
| 30 | E-043 Notes | The comparison shows the change and does not itself decide on continuation (OUT-018 Caveats, INV-106); … | INV-119 (C2-05); E-046 MAY |
| 31 | E-043 Notes | The comparison shows the time points of the rules that apply to its treatment, each within the population … | INV-059 with E-041 `applicable`, `excludes` |
| 32 | E-043 Notes | Nor does it show the time point of a rule at an anchor date whose interval the course is not taken … | `intervalOnTreatment` (E-042) in INV-055, INV-058, INV-059 |
| 33 | E-044 Conformance | Its view states the periods of its two day counts (INV-003) and SHOULD show their definition labels and … | INV-003, INV-008, INV-011 |
| 34 | E-046 Conformance | SHOULD NOT: presented as the sole indicator of individual benefit (INV-065). | INV-119 (C2-06) |
| 35 | E-047 Conformance | SHOULD next to each response comparison, over an evaluation window of that comparison (INV-066); SHOULD … | INV-066; E-055 `adherence` (W2 SHOULD) with INV-109 (`adherenceFor`); INV-104 |
| 36 | E-047 Conformance | Its view SHOULD show the completeness of its window (INV-011). | INV-011, third conjunct |
| 37 | E-048 Conformance | MUST be available for each preventive treatment whose start the context states (INV-102), with headache … | INV-102; INV-068 (`hasType(ctx, c1)` for migraine days); INV-069 |
| 38 | E-051 Conformance | SHOULD be available per acute medication, per formulation, and separately for the baseline and … | INV-062, INV-069, INV-071, INV-072, INV-073, INV-088, INV-104, INV-105, INV-109; W2 E-051 |
| 39 | E-051 Conformance | SHOULD NOT: deciding which definition of response applies (INV-107). | INV-119 (C2-07) |
| 40 | E-053 Notes | Relations: INV-075 (one result per measure; one status per symptom; adverse-event results agree with the … | INV-074, INV-075; INV-123 (`usedMedication`) |
| 41 | E-055 Conformance | Every dose change of the treatment SHOULD be shown, and the response summary and the adherence SHOULD be … | INV-109; W2 E-055 |
| 42 | E-055 Notes | The `when` clauses state when the content can exist: a start date and a duration (INV-079) and a response … | E-055 `when` clauses; R-MCF (1) |
| 43 | E-056 Conformance | Its content (headache days and migraine days per window, instrument results, treatment lines, responder … | **not represented in v38: lost in v35 (R39-01); restored formally in v39** (E-056 attributes, INV-080; responder labels not content, E-056/D02) |
| 44 | E-059 Conformance | SHOULD NOT: presented as a psychiatric diagnosis (INV-084). | INV-119 (C2-09) |
| 45 | E-060 Conformance | MUST be available for every selected time range during which the subject menstruates (`menstruatesDuring`, … | INV-086; E-060 `completeCycles` MUST |
| 46 | E-060 Conformance | A view that shows cycle lines reports migraine days and attacks, and SHOULD show their definition labels … | `reports` (cycle lines), INV-008; INV-011, fourth conjunct |
| 47 | E-060 Notes | For every cycle line, in whichever view it is shown (here, or in the patient-facing overview, INV-105): a … | INV-087, INV-124 |
| 48 | E-061 Notes | Relations: INV-087 (in every view in which an attack mark is shown, the mark is an attack of exactly one … | INV-087 (`nextWindowDays`) |
| 49 | E-062 Conformance | `acute` SHOULD where the subject has used acute medication up to the as-of date (OUT-031: "for acute … | E-062 `acute` (SHOULD `when`); INV-088 (`s.period = v.covers`, which INV-003 places in the view) |
| 50 | E-064 Conformance | A view that shows a rate reports attacks and SHOULD show their definition label (INV-008); the … | `reports` (cluster attack rates), INV-008; INV-011, first conjunct (a rate is a per-period value) |
| 51 | E-065 Conformance | MAY; when shown, the two caveats SHOULD (INV-090) and the clinical-interpretation caveat SHOULD (INV-100). | E-065 MAY; INV-120 (C3-09) |
| 52 | E-065 Conformance | The view reports attacks and SHOULD show their definition label (INV-008) and the completeness of the … | `reports` (trigger view), INV-008; INV-011, fourth conjunct |
| 53 | E-066 Conformance | SHOULD be available for clinician audiences, for a period chosen by the clinician, whatever its dates … | INV-094, INV-104 |
| 54 | E-067 Notes | The relationship to menstruation is shown by cycle lines (E-060) that overlap the covered period; INV-087 … | INV-105, INV-087 |
| 55 | INV-003 Notes | In particular: - every value of a response comparison refers to its baseline or one of its on-treatment … | INV-003; W2 E-040; INV-038, INV-056, INV-061 |
| 56 | INV-003 Notes | A referenced item that shares no period atom with its holder is not placed in the holder's view by … | W2 markers (section 6.0); INV-078, INV-087 |
| 57 | INV-023 Reading | The subject's acute medications are every acute medication it has used up to the as-of date (E-008), so a … | INV-118 (C1-10): `medicationKinds(c)` over `c.subject.acuteMedications` (E-008) |
| 58 | INV-037 Reading | For any selection of two or more periods of equal length (for example a baseline period and a later period … | INV-037, INV-038, INV-003 |
| 59 | INV-038 Reading | Together with INV-003, this places every value of a comparison in the comparison's view, so that the … | consequence of INV-003 and INV-038 |
| 60 | INV-050 Notes | The start of withdrawal that the view shows is one of the subject's wherever the view is shown (INV-113, … | INV-123 (`withdrawal`) |
| 61 | INV-055 Reading | For each evaluation time point that current guidance names for the treatment (for its type, unless the … | INV-055 (`applicable`, `excludes`) |
| 62 | INV-055 Notes | So the comparison is required for every preventive treatment that has started, but at the time points of a … | INV-055 (`applicable`, `excludes`) |
| 63 | INV-056 Reading | Because every value refers to one of the comparison's periods, which INV-003 places in the comparison's … | W2: E-040 `reference`, `compared` `shown MUST when ofResponseComparison(self)` |
| 64 | INV-056 Notes | Each change is shown with the two values it compares (INV-054), hence in the same view. | W2: E-040 (as row 63) |
| 65 | INV-059 Reading | Every response comparison shows, in its view, the evaluation time points of all guidance rules that apply … | INV-059 |
| 66 | INV-059 Reading | For a treatment outside the population of every rule, no time point of these rules is required, and … | INV-058, INV-059 |
| 67 | INV-062 Reading | A responder label names the criterion it applies, with its thresholds; it is shown with its response … | INV-062; INV-114 |
| 68 | INV-062 Notes | The response comparison that a label shows as its underlying values is one of the label's treatment … | INV-062; INV-114 |
| 69 | INV-068 Notes | **Start not stated.** The start conjunct is existential, so a treatment review view is admitted only for a … | INV-068 (`∃ s ∈ startOf(…)`) |
| 70 | INV-070 Notes | **Course start not stated.** The conjunct `startOf(ctx, v.treatment) = ∅ ∧ courseBegunBy(ctx, v.treatment, … | E-049 `onTreatmentPeriod` `when` clause, second disjunct |
| 71 | INV-072 Notes | `outcomes` and `sequence` are references (section 2.5), and outcome summaries and attack lines refer to no … | W2: E-051 `outcomes`, `sequence` |
| 72 | INV-078 Notes | `preventiveGroups`, `acuteGroups` and `lines` are references (section 2.5), and groups and lines refer to … | W2: E-054; INV-078 (lines) |
| 73 | INV-078 Notes | Each line's response summary and adherence are shown with the line (INV-109). | W2: E-055 `preventiveResponse`, `acuteResponse`, `adherence` |
| 74 | INV-079 Notes | A course whose start the context does not state shows no start date (the first conjunct) and no duration: … | E-055 `when` clauses; INV-079 (`∀ d ∈ l.duration • startOf(…) ≠ ∅`) |
| 75 | INV-109 Notes | A response comparison shown with a line shows its values, changes and time points in the same view (E-043 … | W2: E-043, E-051, E-055 |
| 76 | INV-109 Notes | The lines of the treatment history are shown in the history view (INV-078); in the clinician-facing … | INV-078, INV-104, INV-109 |
| 77 | INV-081 Reading | Every available instrument result in the selected time range is reported, and, where an earlier … | INV-081; E-058 `baselineResult`, `changeFromBaseline` (`when`) |
| 78 | INV-110 Reading | Every day on which a trigger co-occurrence view shows the potential trigger factor as present, and every … | INV-110, INV-003; INV-011, fourth conjunct |
| 79 | INV-092 Reading | If a composite index is shown for migraine, it is labelled exploratory and shown, in the same view, with a … | INV-115; W2 E-033 |
| 80 | INV-092 Notes | The component measures shown with an index for migraine are of its period and type scope wherever the … | INV-115; W2 E-033 |

### The other sentences

- **187 content sentences whose key terms all have a counterpart** (`sweep_content_nomissing.txt`). Each was read. All are represented by the v38 formal text. They fall into four groups:
  - the v34 element Conformance enumerations that restated availability, content, caveat and prohibition invariants, now C1 to C3 rows, INV-118 to INV-120 and the kept invariants;
  - relation paraphrases in Notes ("Relations: INV-… (…)");
  - Readings of merged invariants, for example INV-014 to INV-029, INV-047, INV-054, INV-099 and INV-106;
  - restated `when` clauses and attribute levels.

  Three needed a direct check, and each holds:
  - **v34 E-062.** "with a summary of the period the view covers for each acute medication, shown in the view": INV-088 states `s.period = v.covers`, and INV-003 places a summary that refers to the covered-period atom in that view.
  - **v34 INV-107 Reading.** "shows pain freedom and headache relief side by side": INV-072 asks every summary for all `requiredOutcomes`, which include `painFreedom` and `headacheRelief`, and W2 places them in the summary's view.
  - **v34 E-022 and INV-031.** "a view that marks such periods marks every period whose migraine-day count it shows as 0": removed by CHG-04, an intended change of v35, which watch point 2 of the check after iteration 36 protects.
- **139 dropped sentences without content words** (`sweep_nocontent.txt`). These are:
  - audience sentences of Meanings, now the catalogue's Audience column;
  - "structural" Conformance stubs;
  - pointers ("See ISS-…");
  - relation paraphrases and design reasons.

  None states a Stage 1 part that v38 lacks.
- **104 sentences moved only to `RATIONALE.md`** (`sweep_moved.txt`). These are design reasons, readings of Stage 1 and consequences of the formal text: "makes nothing more required", satisfiability, examples, level reasons of merged invariants. Each content claim among them is stated by the formal text it cites.
- **40 v34 coverage-reason sentences** (`sweep_sections.txt`). Each restates content of the items it names, which the item checks above cover. The v34 OUT-025 reason ("MAY view for selected scheme windows labelled with the scheme name") did not mention the content either.

### Result

**One lost Stage 1 statement part: OUT-025, "the frequency, disability and treatment-history outputs for those windows" (MAY).** It is restored by R39-01 (section 2). No other v34 sentence carried requirement content that v38 lacks.
- Nothing that is still represented was changed.
- No rationale prose was restored to the model.
- The class of the review, view kinds whose content is stated only in prose, has E-056 as its only member (`views.py`, section 2).

## 4. All changed locations

`OUTPUT_MODEL.md`:
- header lines 2 and 4;
- section 4.3: rows OC-05, OC-06, OC-07, OC-08, OC-23, OC-29, OC-30;
- E-015, E-016, E-017, E-019, E-046, E-055: Realises;
- E-056: `omn` block, Meaning, Conformance, Notes;
- section 6.0, "Placement markers (rule W2)": row E-056 added;
- INV-080: title, `omn` block, Reading, Notes;
- section 7: row OUT-025;
- ISS-04: Effect on the model, For the human;
- section 12: entry v39.

`RATIONALE.md`:
- header line 2;
- new entries E-056/D02, E-056/S01 and E-056/X01, after E-056/D01.

## 5. Checks

All checks were run on the files as installed in the repository, against the committed v38. The outputs are in `fix39/out/checks-v39.txt` and `fix39/out/witness39.txt`.

| Check | Result |
|---|---|
| IDs (`ids_trace.py`) | 67 E, 87 INV and 12 ISS headings, none duplicated. 0 unresolved E-, INV- or ISS- references in the model and in `RATIONALE.md`. 174 table rows, none duplicated, 0 unresolved row references. References to withdrawn IDs: the same set as in v38 (section 9 rows and "v34 …" texts). |
| `RATIONALE.md` entries, both directions (`entries.py`) | 440 entries (v38: 437; +E-056/D02, S01, X01), none duplicated, each anchored to an existing item, row, section or OUT. 370 entry IDs referenced from the model, 0 unresolved; 405 referenced from `RATIONALE.md`, 0 unresolved. Every entry except the case-row, section and search-log entries is referenced from the model. The only Concerns that name no current item are the 25 "v34 INV-…" origin notes of v38. |
| Traceability recomputed from the Realises fields (`ids_trace.py`) | 39 rows, in Stage 1 order (OUT-039 after OUT-025). For every requirement, the Elements and Invariants columns equal the reverse index of the Realises fields (0 mismatches), and the Catalogue-rows column equals the rows whose Realises cell names it (0 mismatches). Coverage lines that name items outside their columns: only the two of v38 (INV-104 in OUT-008, INV-069 in OUT-012). OUT-025 has one line per statement part. |
| Catalogue (`catalogue39.py`) | "def." lists: in every row equal to the definitional invariants whose Conformance names an element of the row's kind cell, minus those stated once (0 differences). Realises cells: every requirement named is in the Realises field of an item, case row or source-data row named in the row (0 exceptions). |
| Declared names (`names.py`) | `frequencyValues`, `instrumentResults` and `treatmentLines` are declared. Every selected attribute is declared. The residue of applied names and capitalised names is identical to v38's: sequence applications, bound variables, table IDs and one-line element declarations that the script's pattern does not read. |
| Brace balance (`blocks39.py`) | Every `omn` block is balanced ((), [], {}, ⟨⟩; comments excluded). Of 1,542 code spans, one reads as unbalanced: a regex artefact in the section 2.11 prose, identical in v38. |
| Levels | Invariants by Conformance: level-indexed 4, definitional 38, MUST 11, SHOULD 33, SHOULD NOT 1, the same counts as v38. INV-080 stays definitional. E-056 stays MAY. The new attributes are MAY, the strength of OUT-025, and their markers are definitional. |
| Satisfiability (`witness39.py`) | See below. |
| Scope | No term of input, storage or derivation from input in the added text (enter, record, input, answer, questionnaire, stored, storage, database, JSON, XML, FHIR, algorithm, computed from, derived from, calculated, captured). No relation takes input data; the new conjunct relates output elements only. |
| Quotes | Every quoted string of v38 is present in v39 with the same count, in the model and in `RATIONALE.md`. The new quotations are Stage 1 OUT-025 Statement text, verbatim: "to show the frequency, disability and treatment-history outputs for those windows, labelled with the name of the scheme", "for those windows" and "month-by-month responder views" in `RATIONALE.md`, and "the frequency, disability and treatment-history outputs for those windows" in the change log. No source quote was added or changed. |
| Snapshots | `cmp OUTPUT_MODEL.md history/v39.md` and `cmp RATIONALE.md history/v39-rationale.md`: identical. |

**Satisfiability witness** (`witness39.py`, an evaluator written for these constraints). It covers:
- definitional and MUST: the new and old conjuncts of INV-080; the W2 placement of the three new attributes and of E-010 `qualifies`; INV-002; INV-003; INV-006; INV-012; INV-079; INV-082; INV-111; INV-121; INV-122 (nesting); INV-123 (the members for treatment lines and instrument results); INV-125 (SD-DF-01);
- SHOULD: INV-008, INV-011, INV-120 (C3-01) and INV-125 (SD-DF-02).

The context: a subject with migraine, erenumab started on 15 January 2026, sumatriptan, two MIDAS results, and a Kela 3007 selection with two windows (treatment weeks 9–12, 12 March to 8 April 2026, and the three months before the start, 15 October 2025 to 14 January 2026).

| Case | Expected | Result |
|---|---|---|
| W0: the view with headache days, migraine days, moderate/severe headache days and attacks for both windows, one of them on a second period atom with the dates of a window; completeness indicators; definition labels; two MIDAS results with baseline and change; a preventive treatment line; the C3-01 annotations | admitted | admitted |
| W1: the same view without content attributes (the v38 shape) | admitted | admitted |
| M1: a frequency value of 9 April to 6 May 2026, not a window | rejected | rejected by INV-080 (window dates) |
| M1b: the same value shown in the view but not referenced by `frequencyValues` | admitted (open world) | admitted |
| M2: an intensity summary among `frequencyValues` | rejected | rejected by INV-080 (kind) |
| M3, M4: an instrument result or a treatment line referenced by the view but shown in another view | rejected | rejected by W2 (E-056); the added bare view also lacks its SHOULD annotations |
| M5: a label other than the selected scheme | rejected | rejected by INV-080 (selection) |
| M6: a context without a scheme selection | rejected | rejected by INV-080 (selection), R-MCF (3) |
| M7: a moderate/severe count above the headache days of the same window | rejected | rejected by INV-122 |

So the new conjunct and markers are satisfiable together with the invariants they interact with. Every v38 scheme-window view is still admitted, because the attributes are MAY and may be empty. The conjunct rejects exactly frequency values of other kinds or other dates.

## 6. Diff summary of the formal blocks and rows

- **`omn` blocks:** 160 in v38 and in v39. 158 are byte-identical; two changed:
  - **E-056:** three attribute declarations added: `frequencyValues : set →PeriodValue MAY shown`, `instrumentResults : set →InstrumentResult MAY shown`, `treatmentLines : set →TreatmentLine MAY shown`. The `scheme` and `windows` lines are verbatim.
  - **INV-080:** the v38 predicate is kept verbatim inside parentheses. A new conjunct `∀ m ∈ v.frequencyValues • m ∈ HeadacheDays ∪ MigraineDays ∪ ModerateSevereHeadacheDays ∪ AttackCount ∧ ∃ w ∈ ran v.windows • sameSpan(m.period, spanOf(w))` is added.
- **Case tables C1, C2, C3 and source data tables (section 11):** no row changed.
- **Catalogue (section 4.3):**
  - OC-05, OC-06, OC-07, OC-08 and OC-29: Realises, +OUT-025;
  - OC-23: Realises, −OUT-025;
  - OC-30: Output kind, Period and granularity, Availability, Shown with it.
- **Section 6.0 marker list:** one row added (E-056).
- **Traceability:** row OUT-025 (Catalogue rows, Elements and Coverage); its Strength and Invariants cells are unchanged.
- **Realises fields:**
  - E-015, E-016, E-017, E-019, E-055: +OUT-025;
  - E-046: −OUT-025.
- **Levels:** no level of an existing element, attribute or invariant changed.
- **IDs:** no item added, withdrawn or renumbered.

## 7. Watch points (check after iteration 36)

- **No watch point is touched.**
  - Watch points 1 to 13 do not name E-056, INV-080 or OUT-025.
  - INV-123 and its member list are unchanged (watch point 3).
  - No source-data row changed (watch point 9).
  - No comparability tie was added (watch point 10).
  - The declined ties are unchanged: the E-058 `changeFromBaseline` tie of fix 02, item 14, and the others.
- **Watch point 12** (bookkeeping after the restructuring). R39-01 is a remark of the adjacent kind that the watch point describes: a v35 drop that the equivalence check could not see. Section 3 is the one-off audit of that class, over every v34 prose sentence. It found no further case.
- **Watch point 13** (volume). Two `omn` blocks changed, and nine table rows changed or were added: seven catalogue rows, one traceability row and one marker row.
