# Fix log — iteration 10
Input review: reviews/review-iter-10b.md · Input version: v09 · Output version: v10
Date: 2026-10-21

## What was downloaded and checked

**Nothing was downloaded.** Both remarks concern a conformance level and explanatory paraphrases of a predicate. No quote was added or changed, and no source value was touched. The remarks were verified against the Stage 1 v18 text in the repository and against v09 itself (`history/v09.md`, byte-identical to the input OUTPUT_MODEL.md).

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3;
- v09;
- review 10 (NO_REMARKS) with its "checked and not raised" list, and re-check 10b.

**Earlier work read so that no fix is undone:**
- review 03 (R03-05: changes outside response comparisons);
- fix logs 02 (item 14: INV-060 / INV-061 for compared periods shorter than 28 days; E-062 `remissions`), 03 (R03-05), 08 and 09;
- the oscillation checks after iterations 04 and 08, with their watch points.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. E-040, INV-053 and INV-054 had never changed since v00 (checked in history/v00–v09), so this is their first change.

**Watch points (oscillation/check-after-iter-08.md).** Checked by script against v09 (`fix10/` scripts in the session scratchpad, run with `python3 -I`).
- **Unchanged items.** These are byte-identical: E-008, E-013, E-039, E-041, E-042, E-043, E-046, E-060, E-061, INV-055, INV-058, INV-059, INV-064, INV-087, INV-100 and INV-105.
- **Changed in explanatory text only.** The predicates of INV-001, INV-050, INV-063 and INV-104, and the E-045 definition, are byte-identical; only Readings, Meaning or Notes changed. INV-001 keeps the settled short form "a later time point of its own" (watch point 1). INV-104 keeps the series description of R02-02 (a), R03-04 and R05-01 (watch point 7).
- **Watch point 5 (responder labels).** These are unchanged:
  - `#L.evaluated = 1` (4 occurrences);
  - the `evaluationResult` / `pretreatmentBaseline` pair;
  - `rc.treatment = L.treatment` (6 occurrences);
  - the open `UnderlyingKind` and `PeriodValueKind`, with `otherValueNamed`.

  The only formal change in INV-062 rewrites `ch.relative is percent` as `(∃ q ∈ ch.relative • q is percent)`, because `relative` is now optional (R10b-01). For the changes of a response comparison, which must show both forms, the meaning is the same.

**Verification of the remarks.** Both hold.
- **R10b-01.**
  - Nothing in v09 restricts `Change` atoms to response comparisons. INV-097 ("every change"), the E-037 Conformance and R03-05 treat other changes as possible.
  - In Stage 1, OUT-018 alone states at MUST that the values are shown with the change, and it states it for its own comparison ("showing both the values of each period and the absolute and percentage change from baseline").
  - OUT-019 (SHOULD) asks, "Wherever the output shows a relative (percentage) change in migraine or headache days", for the absolute residual days next to it. OUT-020 (SHOULD) asks for the underlying values of a label.
  - No MUST part covers a change in the patient-facing overview (OUT-035, SHOULD), the post-stop monitoring view (OUT-022, SHOULD) or a scheme-window view (OUT-025, MAY).
  - Scenario check (`scen10.py`): the review's example, an overview change "−4 (−40 %)" whose values are in another view, fails INV-054 at MUST in v09.
- **R10b-02.**
  - `scopeFor(c, allTypes, t)` requires `onlyOfType(c, allTypes, t)`, hence `concerns(c, allTypes, t)`, hence `c.subject.headacheTypes ≠ ∅`.
  - INV-001 admits `headacheTypes = ∅` with `possibleHeadacheTypes = {c1}`. For that subject the v09 paraphrases give all types, while the predicate gives `ofType(c1)`.
  - The same omission was found in the paraphrase of `concerns` (E-012 Meaning and Notes).

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R10b-01 | fixed: the review's option (a), in its alternative form ("state that other changes are constrained only by INV-060"), with the same mismatch fixed in E-040 | INV-054 (name, Predicate, Reading, Evidence, new Notes); E-040 (Definition: `absolute`, `relative` and new `ofResponseComparison`; Meaning; Conformance; Evidence; Notes); INV-053 (Predicate, Reading); INV-060 and INV-062 (Predicate, consequential); E-044 (comment of `change`); section 7 rows OUT-018, OUT-019 and OUT-020 | **INV-054.** It is now `∀ rc : ResponseComparison • ∀ ch ∈ rc.changes • ch.reference ∈ viewOf(ch).content ∧ ch.compared ∈ viewOf(ch).content`, at MUST.<br>• Its whole range is now covered by the MUST of OUT-018.<br>• OUT-020 stays in Realises as the second part cited, which section 3.3 item 6 prescribes. A label's changes are those of its response comparison (INV-062). INV-106 follows the same pattern.<br>**No SHOULD invariant for the other changes.** The review's first form (a new SHOULD invariant on all other changes, realising OUT-019 and OUT-020) would itself fail the level sweep:<br>• OUT-019 asks only for the residual migraine and moderate/severe headache days next to a percentage change in migraine or headache days, which INV-060 already requires;<br>• it says nothing of the baseline value or of changes of other measures;<br>• OUT-020 concerns only a label's comparison.<br>So a change outside a response comparison is constrained by INV-053 (definitional), INV-060 (SHOULD, OUT-019) and, for children, INV-097 (SHOULD, OUT-036 (c)). The INV-054 and E-040 Notes say so.<br>**E-040, the same defect class (found by the level sweep).** In v09, `absolute` and `relative` were MUST without `when`, so they were part of the identity of every change.<br>• A change shown in one form only (for example "−40 %" in the overview) was therefore not a `Change`. It was an `OtherItem` and escaped INV-060 and INV-097, although OUT-019 says "Wherever the output shows a relative (percentage) change" and OUT-036 (c) covers every comparison for a child.<br>• Stage 1 requires both forms only for the response comparison (OUT-018).<br>• Both attributes are now `opt … derived MUST when ofResponseComparison(self)`, and INV-053 requires at least one form (definitional).<br>• INV-060 and INV-062 read `relative` inside a quantifier.<br>• Scenarios (`scen10.py`):<br>&nbsp;&nbsp;– the review's example now passes;<br>&nbsp;&nbsp;– a percentage-only overview change without residual burden now fails INV-060 at SHOULD (v09: unconstrained);<br>&nbsp;&nbsp;– an absolute-only change of a child over 28 vs 7 days now fails INV-097 at SHOULD (v09: unconstrained);<br>&nbsp;&nbsp;– a response-comparison change with one form fails at MUST, as in v09 (there through INV-056).<br>**Levels.** The totals are unchanged (MUST 19), because the restricted INV-054 stays MUST.<br>**Oscillation.** INV-054 is not a watch point, and the responder-label ties keep their MUST basis. |
| R10b-02 | fixed: the review's option (a), no formal change; the optional INV-062 Evidence alignment was also done | E-045 Notes (**Type scope**); INV-063 Reading; E-012 Meaning and Notes (`concerns`, same omission); INV-062 Evidence | **E-045 Notes and INV-063 Reading.** Both now read "over all types combined where the subject has a headache type and every headache type it has or may have falls under that type, and otherwise in the scope of the type itself", which is exactly `scopeFor`.<br>**E-012.** The `concerns` paraphrases gain "who has a headache type" (Meaning) and "the subject has a headache type and" (Notes). The necessary condition for an all-types value to be one of type t is completed in the same way.<br>**INV-062 Evidence.** It now describes the scope `scopeFor`: the all-types values in the case above, and otherwise the values scoped to the type, as in the per-type presentation of OUT-029. It no longer says that these values are always those of the OUT-029 presentation.<br>**INV-063 Reading.** The sweep found further dropped conditions, and the Reading was corrected for them as well (Other changes 2).<br>**Change log.** The v09 change-log entry, which repeats the short wording, was left as history; the v10 entry says so.<br>**Oscillation.** The R09-01 formal text, `#L.evaluated = 1`, the score pair, `rc.treatment = L.treatment` and the open kinds are untouched (watch point 5). |

## Other changes

### 1. Level fidelity sweep (R10b-01 class)

**Method.**
- The script `levels.py` listed every invariant with its level and every level-annotated attribute with its level and `when` clause. It found 108 invariants and 172 attribute declarations.
- For each item I read the Stage 1 statement part(s) it realises, with their strength, and the whole range of outputs the predicate or presence constraint covers. This includes elements shown in views of another level, for example a response comparison in a SHOULD view, a cycle line in the overview, or a change outside a response comparison.
- I checked that the level equals the strength over the whole range, in both directions (not stronger than a SHOULD/MAY part, not weaker than a MUST part).
- Core attributes carry no level. I also checked whether a core or MUST-without-`when` attribute makes content escape a constraint whose Stage 1 basis says "wherever" or "if shown". This is how the E-040 defect showed up.

**Result.** Two mismatches, both fixed under R10b-01:
- INV-054;
- E-040 `absolute` and `relative`.

All other items match.

**MUST and MUST NOT invariants (21)**

| Item | Stage 1 part (strength) | Range constrained | Result |
|---|---|---|---|
| INV-003 | OUT-001 "Every summary output MUST state the reporting period" (MUST) | every view (section 3.6) and every period its items refer to | match |
| INV-009 | OUT-004 "as defined in ICHD-3" (MUST) | every headache-day definition label (labels themselves SHOULD, INV-008) | match |
| INV-014, INV-015 | OUT-001, OUT-004 / OUT-005 (MUST; OUT-005 for patients with migraine) | contexts of one monthly granularity; INV-015 only `hasType(c, c1)` | match |
| INV-108 | OUT-001 frequency outputs per month or 28 days (MUST) | moderate/severe days and attacks once provided; provision itself SHOULD (INV-016, INV-017) | match |
| INV-023 | OUT-014 (MUST) | every context: total, class, drug | match |
| INV-028 | OUT-029 frequency and acute-medication outputs per type (MUST) | contexts with ≥ 2 possible types; moderate/severe days and attacks where provided | match |
| INV-037 | OUT-001 "MUST allow comparison of periods of equal length" | selections of equal length | match |
| INV-040 | OUT-028 three-month view (MUST) | every context | match |
| INV-044, INV-047 | OUT-016 (MUST; "MUST be worded as a prompt") | every context; every indicator | match |
| INV-048 | OUT-016 "MUST NOT be presented as a diagnosis" | every indicator and the annotations qualifying it | match |
| **INV-054** | OUT-018 values with the change (MUST); OUT-019/OUT-020 (SHOULD) | **v09: every change, also outside response comparisons, which Stage 1 covers at most at SHOULD → mismatch.** v10: the changes of response comparisons | fixed (R10b-01) |
| INV-055, INV-059 | OUT-018 time points (MUST) | every started preventive treatment; every response comparison | match |
| INV-056, INV-057 | OUT-018 content (MUST; mod/sev "where reported") | every response comparison. E-043 is by its Meaning the OUT-018 comparison; INV-105 accepts only a full comparison as the overview's treatment effect | match |
| INV-068, INV-102 | OUT-021 MUST part (OUT-004, OUT-005, OUT-014 together) | every treatment review view; every started preventive treatment | match |
| INV-086 | OUT-030 (MUST) | subjects who menstruate | match |
| INV-106 | OUT-018 Caveat (MUST → MUST NOT, section 3.3 item 6); OUT-020 Rationale second | every element | match (settled, reviews 05–10b) |

**SHOULD NOT invariants (8)**

| Invariants | Stage 1 part | Result |
|---|---|---|
| INV-013, INV-043, INV-065, INV-091 | OUT-003, OUT-028, OUT-020 and OUT-037 statement parts at SHOULD NOT | match |
| INV-021, INV-084, INV-101, INV-107 | negative forms of SHOULD parts or Caveats: OUT-011, OUT-033, OUT-038 and OUT-023 | match. INV-048 (MUST NOT) is stronger for the overuse indicator by OUT-016 |

**SHOULD invariants (47).** Every one realises SHOULD parts only. None covers outputs that a Stage 1 MUST part requires, and none covers content that Stage 1 does not ask for.

| Invariants | Stage 1 parts (SHOULD) | Note |
|---|---|---|
| INV-008, INV-010, INV-042 | OUT-002, OUT-005 label, OUT-006, OUT-007, OUT-028 | |
| INV-011 | OUT-003 | |
| INV-016–INV-019, INV-022 | OUT-006, OUT-007, OUT-010, OUT-011, OUT-012 | |
| INV-020 | OUT-011 label | |
| INV-025–INV-027 | OUT-015, OUT-027 | |
| INV-029, INV-039 | OUT-029 intensity per type; OUT-010 comparison | INV-039 also uses OUT-036 (c) for children |
| INV-034, INV-035 | OUT-009 | |
| INV-049, INV-050, INV-052 | OUT-017 | |
| INV-060 | OUT-019 "Wherever …" | v10: also changes shown in percentage form only (E-040) |
| INV-062 | OUT-020 (OUT-019 for the residual) | |
| INV-066 | OUT-039 | |
| INV-069 | OUT-021 SHOULD components; OUT-023 | |
| INV-070, INV-103 | OUT-022 | |
| INV-071–INV-073, INV-076 | OUT-023; OUT-012; OUT-031 | 15 minutes for cluster headache |
| INV-077, INV-078 | OUT-024 | |
| INV-081 | OUT-026 | |
| INV-083 | OUT-033 | |
| INV-088 | OUT-031 | |
| INV-090 | OUT-032 caveats | |
| INV-092, INV-093 | OUT-037 | |
| INV-094, INV-104 | OUT-034 | OUT-008 measures at SHOULD through OUT-034's range, ISS-04; OUT-039 |
| INV-095, INV-105 | OUT-035 | |
| INV-096–INV-098 | OUT-036 (a)–(c) and Caveat | INV-097 covers every comparison and change for a child. INV-055's MUST requires only one equal-length comparison to exist |
| INV-099, INV-100 | OUT-038 (with the OUT-026 and OUT-033 examples) | |

**Definitional invariants (32).** INV-001 (context), INV-002, INV-004–INV-007, INV-012, INV-024, INV-030–INV-033, INV-036, INV-038, INV-041, INV-045, INV-046, INV-051, INV-053, INV-058, INV-061, INV-063, INV-064, INV-067, INV-074, INV-075, INV-079, INV-080, INV-082, INV-085, INV-087 and INV-089.
- Each states a relation of a derived attribute, a bound that follows from the element's definition, or the element's structure (section 3.3 item 5).
- INV-007 belongs here because "the same view" is part of the definition of `qualifies` (E-010). No other one is an availability or co-presence requirement in disguise.
- The new INV-053 conjunct (at least one of the two forms) is structure.

**Attributes**

| Attributes | Level | Stage 1 part / range | Result |
|---|---|---|---|
| E-003 `covers`; E-005 `start`, `end`, `lengthDays` | MUST | OUT-001, every summary output and period | match |
| E-032 `code`, `referenceLevel`, `span`, `basis` | MUST | OUT-016 MUST, every indicator (an "indicator" not referring to the ICHD-3 levels is not the OUT-016 indicator) | match |
| **E-040 `absolute`, `relative`** | MUST | **v09: every change (by typing), although only OUT-018 requires both forms, for its comparison; one-form changes escaped INV-060 and INV-097 → mismatch.** v10: MUST when `ofResponseComparison(self)` | fixed (R10b-01) |
| E-042 `anchorDate`, `earliest`, `latest` (when); E-043 six attributes | MUST | OUT-018, every time point and response comparison; `latest` is also implied by INV-058 | match |
| E-048 `baseline`, `onTreatment` | MUST | OUT-021 MUST part | match |
| E-060 `completeCycles` | MUST | OUT-030 | match |
| E-060 cycle-line attributes; E-061 `inPerimenstrualWindow` | MUST | OUT-030 in the menstrual-relation view. In the patient-facing overview (OUT-035, SHOULD): `menstruationDays`, `migraineDays`, `attacks` and `inPerimenstrualWindow` are identity, and the three `when` attributes are implied by the definitional INV-087 wherever a line is shown. So the level adds no constraint on outputs, and INV-105 (SHOULD) decides whether a line is shown | match (review 10b: not raised; unchanged since v04) |
| 47 SHOULD attributes (E-023, E-033, E-035, E-038, E-039, E-046, E-049, E-051, E-053, E-054, E-055, E-058, E-059, E-062, E-063) | SHOULD | the SHOULD parts of OUT-010, 037, 009, 028, 017, 020, 022, 023/012, 024/039, 026/036, 033, 031. E-038 `referencedCodes` is the SHOULD part of the MUST view of OUT-028 | match |
| E-010 `wording`, E-052 `proportion` | MAY | no Stage 1 part asks for a wording or a proportion | match |
| 94 core attributes | — | identity. Escape check: E-024 and INV-020 (open statistic and attack scope); E-032 and INV-047/048; E-046 (`evaluated` is a reference, shown by INV-003 at MUST); E-044 and INV-060; E-051 (INV-071); E-060 (INV-105 requires a line) | no other escape |

### 2. Prose-vs-formal sweep (R10b-02 class)

**Method.** Every explanatory field was read against its formal counterpart:
- 108 Readings against their predicates;
- 67 Meanings and 67 element Conformance fields against the definitions, attribute levels and `when` clauses;
- 86 Notes fields (85 in v09), in particular each "Relations: INV-NNN (…)" gloss against that invariant;
- the 208 comment lines of the `omn` blocks (206 in v09; the 2 new ones are the E-040 `relative` comment and the `ofResponseComparison` comment);
- the 39 traceability coverage texts.

**The script.** `prosecheck.py` flagged every invariant whose predicate contains a condition whose keyword is missing from its Reading, for 26 kinds of condition (for example `startOf … ≠ ∅` / "started", `hasType(…, c1)` / "migraine", `provides` / "provide", `auraDuration` / "aura", `inSpan(…, timeRange)` / "time range", `childOrAdolescent`, `scopeFor` / `onlyOfType`, `MonthlyKind`, `> 0` guards). Every flag was read.

**Flags that remain, not mismatches:**
- **"All types" (23 invariants).** An unqualified per-period value of the person is the value over all headache types combined. Readings name a type wherever one is meant, and none names a different scope. A blanket convention sentence was considered and rejected, because some content invariants (for example INV-069, INV-071) leave the scope open.
- **INV-055.** `applicable` is paraphrased in words.
- **INV-019 and INV-057.** "attack or headache duration" excludes aura; "reports" is "provides".

**Mismatches found and fixed (no formal change):**

| Item | Field | Mismatch | Change |
|---|---|---|---|
| E-012 | Meaning, Notes | `concerns` paraphrased without `headacheTypes ≠ ∅` (R10b-02 class) | condition added |
| E-045 | Notes | R10b-02 | condition added |
| E-045 | Meaning | `scoreDecrease` paraphrase dropped the subject condition (`conditionHolds` in `scoreMet`, `scoreDecided`); `attackReduction` paraphrase did not say that the attacks are taken in the scope `scopeFor` | added |
| INV-063 | Reading | R10b-02. Also dropped: the conjunct "control-level label ⇔ control-levels component", the antecedent "responder or non-responder" of the forcing relations, and the guards `reference.days > 0` / `b.count > 0` in met and decided. "the first relation" was ambiguous | added; "the relation for 'responder'" |
| INV-062 | Reading | dropped `ran L.evaluated ⊆ ran rc.onTreatment`, and that the residual burden is required for percentage changes in migraine or headache days of the evaluated periods | added |
| INV-062 | Evidence | R10b-02 optional | aligned with `scopeFor` |
| INV-001 | Reading | dropped: screening results on or before the as-of date; course events belong to the subject's treatments; guidance types and `preventiveFor` for preventive treatments only. "tension-type and cluster headache" stood for `hasType`, not "may have" | added |
| INV-012 | Reading | "refers to the whole period" for `typeScope = allTypes` | "stated for all headache types combined" |
| INV-014 | Reading | "every output context", without "of that granularity" | added |
| INV-020, INV-021 | Reading | dropped `kind ≠ auraDuration` | "other than an aura duration" |
| INV-024 / E-029 | Reading / Notes | upper bounds stated without their conditions (every class of the set, every class of the subject's medications, every drug of the class that the subject uses, shown) | conditions added |
| INV-027, INV-103 | Reading | dropped `startOf(…) ≠ ∅` | "that has started" |
| INV-028 | Reading | dropped the calendar-month / 28-day granularity and "together" (`reportedTogether`) | added |
| INV-032 / E-023 | Reading / Notes | claimed that the sum of the distribution counts does not exceed the period length; the predicate bounds each count by the length and the sum by the headache days | corrected |
| E-023 | Conformance | cited INV-018 for comparisons, which are INV-039 | INV-039 |
| INV-035 | Reading | dropped the series in the view and the covered period equal to its span | added |
| INV-037 | Reading | "the frequency measures", without the migraine and `provides` conditions | listed with conditions |
| INV-050 | Reading | "the start of withdrawal" for `v.withdrawalStart ∈ ctx.subject.withdrawalStart` | "the subject's" |
| INV-056 | Reading | dropped: the treatment is the subject's preventive treatment; values only of its periods; periods ordered without overlap; all types | added |
| INV-068 | Reading | dropped: baseline before the start, on-treatment periods on or after it; all types | added |
| INV-074 | Reading | dropped: proportion only where `attacksAssessed > 0`; `os ∈ os.summary.outcomes`; `#sequence ≤ treatedAttacks`; at most one formulation for a single-formulation summary | added |
| INV-081 | Reading | "with the change from the baseline administration"; the predicate requires the baseline result (the change follows from E-058) | corrected |
| INV-082 / E-058 | Reading / Notes | "a published band of that instrument" for every instrument; bands exist only for MIDAS, HIT-6, PedMIDAS and HALT-90 | restricted; other instruments show a published category |
| E-058 | Conformance | dropped the completion-date condition of the `baselineResult` `when` clause, and the condition of `changeFromBaseline` | added |
| INV-088 | Reading | rates "for every active period within the selected time range", and bouts and remissions as content of the invariant. The predicate requires rates for the bouts the view shows that overlap the range; bouts and remissions are E-062 attributes | corrected |
| INV-096 | Reading | dropped "within the selected time range" for PedMIDAS, and the `affected` alternative to missed and impaired | added |
| INV-104 | Reading | dropped: "that has started" (response comparison, adherence); "completed within the covered period" (instrument results); the migraine condition; the scope of the treatment markers; marks of series periods | added |
| E-022 | Notes | "exactly when" overstated INV-031: a mark is constrained only where a count is shown, and the converse holds only in a view that marks such periods | corrected |
| E-032 | Meaning | "together with the medication days" (same view by the E-003 convention). `basis` references days that the output shows, and Stage 1 asks for no same-view display | "and it shows the medication days" |
| E-044 | comment | "the relative change it is shown next to". `change` need not be a percentage change (v10) nor in the same view; INV-060 places it next to percentage changes | "the change it refers to; shown next to it where INV-060 requires" |
| row OUT-019 | coverage | "every percentage change", without "in migraine or headache days" | added |

All other Readings, Meanings, Conformance fields, Notes, comments and coverage texts agree with their formal counterparts.

### 3. Satisfiability pass

**Scope.** The pass covered:
- the changed formal items: E-040 (`absolute`, `relative`, `ofResponseComparison`), INV-053, INV-054, INV-060 and INV-062;
- the items that constrain the same elements and views: INV-003, INV-006, INV-008, INV-011, INV-055–INV-057, INV-061, INV-063, INV-097, INV-104, INV-105, E-043 and E-044.

All were checked against INV-001 and the context definitions. The prose-only changes have no formal effect.

**Changes of a response comparison.** For every admissible context and every response comparison that INV-055 requires, each change shows both forms.
- `absolute = compared − reference` is always an integer.
- `relative` is `percent(q)`, q rounded, when the reference is above 0, and `undefinedForZeroReference` otherwise. So no derived attribute is required where its relation is undefined.
- Placing the comparison, its values and its changes in one view satisfies INV-054 together with:
  - INV-056 and INV-057;
  - INV-006 (one atom per measure, period and scope);
  - INV-003 (the monthly periods in the view);
  - INV-011 and INV-008 (completeness and labels added);
  - INV-060 and INV-061 (a residual burden of the same monthly compared period);
  - INV-097 (28-day periods for children; INV-055 Notes);
  - INV-062 (rc in the label's view) and INV-063 (unchanged: `reductionMet` reads days, not forms).

**Changes outside a response comparison.** No invariant requires one.
- INV-053 needs one form only.
- INV-060 (SHOULD) can be met wherever the compared period contains a monthly period.
- A percentage change in migraine or headache days over fewer than 28 days has no residual "per month" (INV-061). This is the fix-02 decision (item 14), unchanged. v10 only classifies one-form changes as changes and adds no requirement to show one.
- INV-097 (SHOULD) never forces a change of unequal periods.

**Typing.** The optional `absolute` and `relative` are used only inside quantifiers or compared with ∅ (INV-053, INV-060, INV-062). `÷` stays guarded by `reference.days > 0`.

**Result.** No admissible context makes the MUST or SHOULD invariants jointly unsatisfiable. No conflict needed fixing.

### 4. Bookkeeping

- Header "Version: v10 · Iteration: 10 · Status: under review".
- Section 9 "as of v10"; nothing withdrawn.
- Section 10 unchanged: no new source.
- Section 11: iteration 10 paragraph (no web search, no download).
- Section 12: v10 entry with totals.

## Checks

The scripts in the session scratchpad (`fix10/`: `parse.py`, `mech.py`, `names.py`, `levels.py`, `prosecheck.py`, `scope.py`, `scen10.py`) were run with `python3 -I` on the final OUTPUT_MODEL.md.

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108). None missing, no duplicates, none withdrawn. |
| References | No dangling E- or INV- reference.<br>S references lie within S-001–S-046 and S-101–S-106, and every S-1NN used has a row in section 10.<br>OUT references lie within 001–039.<br>ISS headings are ISS-01–06 and ISS-08–11; ISS-07 occurs only as the withdrawn ID. |
| Realises and traceability | Exactly one Realises field per item.<br>39 rows in Stage 1 order (OUT-039 after OUT-025); all 39 requirements present.<br>0 differences between each row and the union of the Realises fields.<br>No coverage text names an ID outside its row; 39 × "full". |
| Names and types in `omn` blocks | 326 declared names (v09: 325; new `ofResponseComparison`), none declared twice.<br>218 enumeration constants and variant tags, with no clash.<br>Every attribute selection names a declared attribute or component.<br>The remaining identifiers (86, the same set as v09) are bound variables or parameters, plus `_` of the infix `_⊑_`.<br>Every type used in the changed text is declared (`Change`, `ResponseComparison`, `RelativeChange`, `DayCount`). |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2); 0 violations. E-040 `absolute` and `relative` are `opt` with `MUST when`. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 47, SHOULD NOT 8, definitional 32, all unchanged.<br>Every MUST NOT and SHOULD NOT predicate begins with `¬`.<br>No invariant changed level or scope. INV-054 stays MUST with a narrower range. |
| Partial terms | The new terms are guarded: `÷` by `ch.reference.days > 0`; the optional `absolute` and `relative` are used only in quantifiers or with `≠ ∅`. |
| Watch-point items | Byte-identical: E-008, E-013, E-039, E-041, E-042, E-043, E-046, E-060, E-061, INV-055, INV-058, INV-059, INV-064, INV-087, INV-100 and INV-105.<br>The predicates of INV-001, INV-050, INV-063 and INV-104 and the E-045 definition are unchanged. |
| Scope sweep (enter, entry, record, input, capture, logged, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, reminder, algorithm, obtained, calculated, computed, field, "diary data", "diary information"; sections 1–8) | 77 hits, as in v09, with the same counts per term.<br>The only changed context is the INV-014 Reading ("can be answered", an output context answered by an output). As review 10b confirmed for v09, all hits are exclusion statements, out-of-scope notes, Stage 1 wording or quotes.<br>The new text contains no input entity, storage term or derivation from input. The changed relations take only output elements (shown changes, values and their views). |
| Satisfiability | No conflict (Other changes 3). Scenario script: the six change scenarios behave as stated. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v10.md`: identical. |
| Files written | Only OUTPUT_MODEL.md, history/v10.md and this fix log. Nothing under docs/stage1-output-requirements/ was changed, and nothing was committed or pushed. |
