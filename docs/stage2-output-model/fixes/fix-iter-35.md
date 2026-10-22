# Fix — iteration 35
Version produced: v35
Date: 2026-10-22

Step 2 of the restructuring of iteration 35 (PROCESS.md section 8): the rewrite of the model under the committed plan [`restructure/plan-v35.md`](../restructure/plan-v35.md). Inputs: `history/v34.md`, `reviews/review-iter-35.md` (R35-01), `audits/consistency-audit-v34.md` (CA-01 to CA-19), the oscillation checks after iterations 12 to 32, Stage 1 v18.

Files written: `OUTPUT_MODEL.md` (v35, 420,865 bytes), `RATIONALE.md` (v35, new, 318,367 bytes), `history/v35.md` and `history/v35-rationale.md` (byte-identical copies), and this log.

## 1. Summary

- **Formal content.** 67 elements, all kept with their IDs; 87 invariants: 79 kept v34 invariants (50 with byte-identical `omn` blocks, 29 edited exactly as plan section 8 states) and the new generic invariants INV-118 to INV-125. 38 v34 invariants were merged into generic invariants, placement markers (rule W2) or an element's attribute type, and are listed in model section 9 with the item they went into. 37 element blocks are byte-identical to v34; 30 are edited as plan section 8 states.
- **Levels** (C8). v35: MUST 11, SHOULD 33, SHOULD NOT 1, MUST NOT 0, definitional 38, level-indexed 4 (INV-118, INV-119, INV-120, INV-125), whose cases are: must 8 (C1 6, C3 1, SD-DF 1), should 19 (C1 8, C3 10, SD-DF 1), shouldNot 7 (C2), mustNot 2 (C2), may 1 (C3-02). Scopes: output 66, repertoire 20 (INV-118 and 19 kept availability invariants), context 1.
- **New structure** (plan section 2): output catalogue (model section 4.3, OC-01 to OC-45), case tables C1 (14 rows), C2 (9), C3 (12) (section 4.4), case tables as a notation construct (section 2.11), placement markers (rule W2, section 2.5), level-indexed invariants (section 3.3, item 7), the general rule on facts the context does not state (R-MCF, section 3.8), 13 source data tables with 94 rows (section 11), ISS-13 (section 8).
- **RATIONALE.md**: 397 entries (Q 111, D 228, N 8, S 36, W 12, X 2) and 35 search-log entries (SL-001 to SL-035, the v34 search log verbatim).
- **Method.** Everything that moves was moved by script from `history/v34.md`: the formal edits of plan section 8 (`formal.py`, exact string edits with a count check), the source data tables (`sd_tables.py`, generated from the v34 terms and parsed back), the catalogue and case tables C1–C3 (`plan_tables.py`, taken from the plan), and the prose (`prose.py`, sentence-level dispositions in `disp_meaning.py`, `disp_reading.py`, `disp_notes.py`, corrections in `corr.py`). The new text (sections 2.11 and 3.8, rule W2, section 3 additions, the catalogue head, INV-118 to INV-125, the element Conformance templates, the Readings of the edited invariants, ISS-13, the traceability rows, the new RATIONALE entries and the change-log entry) was written by hand. The scripts are in the author's scratchpad (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/v35-author/`), which is not in the repository.
- **Decisions on plan section 15** (taken by the orchestrator under the human's instruction to restructure) were applied: ISS-13 recorded as planned (CHG-03); output-wide consistency of dated phases, option (a) (CHG-01, CHG-02); the remaining exception of R35-01 (lines that have not ended) kept and stated; CA-02 conjunct removed (CHG-04); CA-07 conjunct definitional (CHG-06); CA-09 fix 11 kept; E-049/INV-070 merge as planned, with the stated-start clause verbatim; CHG-05 as planned.

## 2. Remark R35-01 and audit findings CA-01 to CA-19

Each is handled as a review remark: disposition, what changed, where.

**R35-01** (formal defect: cycle lines outside the menstrual-relation view may overlap).
- Disposition: fixed (CHG-01).
- Change: new generic invariant INV-124, first conjunct: no cycle line of the output spans a first day of menstruation that the output shows, where the shown first days are those of `shownDayOnes` (new in E-060: the day 1 of a line, and the day after a line that has ended). Output-wide (the review's option (a)), on fix 04's ground that all views of one output summarise one diary as of one date. The class rule ("the dated phases that one output shows describe one history") also covers the cluster and remission periods (CHG-02).
- Prose: the claims that every attack mark is correct were corrected to what the predicate gives (plan section 10): in every view, an attack mark shows the attack as in the window exactly when its onset lies in the window of a menstruation whose first day the view shows, except for an attack on a line that has not ended. Places: E-061/D02, INV-087/D01, INV-105/D04; the E-060 Notes sentence "So every day of a line …" was dropped with the restatement of INV-087 (plan 9.2); rows OUT-030 and OUT-035 no longer carry coverage reasons (section 7 template).
- Check: `r3501_v35.py` (refined test of the v35 rules, INV-087 per line and INV-124 with `shownDayOnes`): 1 view, 127,688 admitted outputs, 3,742 with a wrong mark, 0 of them on a line that has ended; 2 views, 131,481, 2,084, 0. The remaining exception is the one stated.
- Where: model E-060 (`shownDayOnes`), INV-124; RATIONALE INV-124/D01, E-061/D02, INV-087/D01, INV-105/D04.

| ID | Disposition | What changed | Where |
|---|---|---|---|
| CA-01 | fixed (CHG-03) | INV-060's antecedent gains `ch.compared.period.lengthDays ≥ shortestMonthlyDays`; new ISS-13 puts the question of OUT-019's "wherever" for shorter periods to the human. The Reading says the same | INV-060; ISS-13; INV-060/D02; catalogue OC-22 |
| CA-02 | fixed (CHG-04) | INV-031's last conjunct (a view that marks one period without migraine days marks every such period) removed; "a mark implies 0" stays; INV-104 keeps the marks of the clinician-facing summary at SHOULD | INV-031; INV-031/X01 |
| CA-03 | fixed (CHG-05) | INV-123's `factsShown` has the member `usedScope` for an acute-medication day count above 0, tied by `stated` to an acute medication of the scope (`inMedicationScope`, E-008). INV-046 unchanged; its guarantees (INV-046/S01) now hold | E-001 `factsShown`; E-008 `ShownFact`, `inMedicationScope`, `stated`; INV-123; INV-123/D07 |
| CA-04 | fixed (prose) | The E-032 Relations paraphrase and the OUT-016 coverage reason were dropped (Relations: IDs only; section 7 template) | E-032 Notes; section 7 row OUT-016 |
| CA-05 | fixed (no change of meaning) | INV-050's conditional review-window conjunct removed as implied by E-039 `reviewWindow` (SHOULD, no `when`); the settled reading kept (fix 02, item 14). The prose says the review window SHOULD be shown in every follow-up view and INV-051 fixes its dates, which may lie after the covered period and the as-of date | INV-050; E-039/D02, INV-049/D01, INV-050/D01, INV-050/D02 |
| CA-06 | fixed (prose) | "A remission period that shows its start date lasts more than three months; every fully conformant output shows it (E-063 `start`, SHOULD)" in INV-089 Reading, E-062/D01, E-063/D01 and ISS-12 Effect; the E-063 Relations paraphrase dropped; no re-tying of E-063 (check 32, watch point 1) | INV-089 Reading; ISS-12; E-062/D01; E-063/D01 |
| CA-07 | fixed (CHG-06) | INV-111 gains a third, definitional conjunct: the values that one change, residual burden or composite index refers to come from views that, where both state a definition for the measure, state the same one. INV-008/S01 and INV-111/S01 rewritten; they now hold as written | INV-111; INV-008/S01; INV-111/S01; INV-111/D02 |
| CA-08 | fixed (prose) | R-MCF (1) (section 3.8) and its wording rule: "a treatment whose start the context states". Element Conformance fields use the template (E-043: "For each preventive treatment", whose start the context states — R-MCF (1)); "has started" replaced in the Readings of INV-027, INV-055, INV-071, INV-102, INV-104, INV-105, in the E-067 Meaning (`courseOverlaps`) and in ISS-10; the comment of `courseOverlaps` in the unchanged E-067 block is a gloss without formal force | section 3.8; E-043, E-048, E-051 Conformance; the Readings named; ISS-10 |
| CA-09 | kept (fix 11) | No placement markers on the cluster view's references. The INV-088 Reading says "refers to" for bouts, remissions and rates; the alternative is recorded as rejected | INV-088 Reading; E-062/X01; section 6.0 list of markers |
| CA-10 | fixed (prose) | E-019 Meaning worded as E-016 and E-017: attacks under the one definition the view follows, which its labels name; INV-125 (SD-DF-02) asks at SHOULD that the label name ICHD-3 "frequency of attacks" | E-019 Meaning |
| CA-11 | fixed (no change of meaning) | Section 2.3: the domain of a given partial function is stated by a case table, an axiom or the library list of section 2.8; otherwise only through invariants that use `dom` (`classOf`, INV-001). The domain comments of `publishedRecall`, `scoreRange` and `classOf` deleted; the first two are fixed by SD-IN. Section 3.2: the conditions on `Ctx`, `Rep`, `ctx` and `parts` are normative sentences after the block; the comments keep only glosses | sections 2.3, 3.2; E-028; E-057; SD-IN |
| CA-12 | fixed (prose) | INV-003/D02 limits the agreement to counts (INV-006), completeness (INV-012), the combined indication (INV-046) and cluster attack rates (INV-089), and says that other values, for example two intensity summaries, are not tied | INV-003/D02 |
| CA-13 | kept | The difference is stated by the W2 markers: E-038 `series` `shown` (definitional), E-035 `series` `shown SHOULD`. OUT-028 (MUST) defines the three-month view by its periods; the time-course tie is OUT-009 content at SHOULD (reviews 31 and 32; check 32, watch point 1) | E-035, E-038; section 6.0 list |
| CA-14 | fixed (prose) | INV-123/S01 (ex INV-117 Notes): "a responder or non-responder label can refer to any preventive treatment of the subject; a control-level label only to one that has a whole monthly period on treatment (INV-064)" | INV-123/S01 |
| CA-15 | fixed (prose) | INV-062/D03: "No acute-treatment summary, and no result of an instrument without a score component (for example PGIC), decides a category; the results at the evaluation and at the pre-treatment baseline decide score components (INV-063)" | INV-062/D03 |
| CA-16 | fixed (prose) | INV-105 Reading says what the conjunct says ("a cycle line that overlaps that period"); the lead-in remark is in INV-105/D04 as one way to meet the conjunct | INV-105 Reading; INV-105/D04 |
| CA-17 | fixed | Section 2.4: `ℙ T` is also used for parameters of functions, result types of defined functions and components of values that hold sets of atoms (`fiDays`, the catalogue columns) | section 2.4 |
| CA-18 | fixed | Section 2.8: "under the week convention of the diary (one convention for all its outputs)" | section 2.8 |
| CA-19 | fixed | Section 4.1, layer 3: the medication-overuse indicator (E-032) is an item for one period and one class or combined use, not a `PeriodValue` | section 4.1 |

## 3. Intended changes of meaning

The only changes of meaning are those of plan section 12. Every other difference is a move or an equivalent reformulation (sections 5 and 9 below, plan sections 5 to 8).

| ID | Formal change | Where implemented |
|---|---|---|
| CHG-01 | A cycle line of any view does not span a first day of menstruation that the same output shows (`shownDayOnes`) | INV-124, first conjunct; E-060 `shownDayOnes` |
| CHG-02 | Output-wide, for items that show their start and last day: two cluster periods (or two remission periods) are the same or do not overlap; a cluster period and a remission period do not overlap | INV-124, second and third conjuncts; INV-089 loses its bout–remission conjunct (implied) |
| CHG-03 | The residual burden is asked for only next to a percentage change whose compared period has at least 28 days | INV-060 antecedent; ISS-13 |
| CHG-04 | A view that marks one period without migraine days is no longer required to mark every such period | INV-031 (last conjunct removed) |
| CHG-05 | A shown acute-medication day count above 0 implies that the context lists an acute medication of its scope | INV-123 (`usedScope` member of `factsShown`; `inMedicationScope`, `stated` in E-008) |
| CHG-06 | The values that one change, residual burden or composite index refers to come from views that, where both state a definition for the measure, state the same one | INV-111, third conjunct (definitional) |
| CHG-07 | A prohibited claim carried by an annotation that qualifies the element counts as presenting the element with it, also for C2-03 (v34 INV-021) and C2-06 (v34 INV-065) | INV-119 with `presents` (E-001) |
| CHG-R1 | The treatment and start facts of v34 INV-056 and INV-068 move from MUST to definitional; no change of the admitted repertoires | INV-123 (`preventiveCourse`, `courseEvent` of kind `start`); INV-056, INV-068 lose these conjuncts |

## 4. Mapping of every v34 element and invariant to its v35 place

The table of plan section 11, with the dispositions as implemented (differences are marked with the deviation number of section 5).

| v34 ID | v34 title | v35 place | Disposition |
| --- | --- | --- | --- |
| E-001 | Element | E-001 | kept; Definition + `presents` (INV-119), `factsShown` (INV-123) |
| E-002 | Output | E-002 | kept; formal text unchanged |
| E-003 | View | E-003 | kept; formal text unchanged |
| E-004 | Item and OtherItem | E-004 | kept; formal text unchanged |
| E-005 | Period | E-005 | kept; formal text unchanged |
| E-006 | Series | E-006 | kept; formal text unchanged |
| E-007 | OutputContext | E-007 | kept; formal text unchanged |
| E-008 | SubjectProfile | E-008 | kept; Definition + `ShownFact`, `inMedicationScope`, `stated` (INV-123) |
| E-009 | ICHD-3 code references | E-009 | kept; label axiom → SD-IC-01…15 (`axiom table SD-IC`); hierarchy axioms stay |
| E-010 | Annotation | E-010 | kept; `qualifies` gets marker `shown` (W2, ex INV-007) |
| E-011 | DefinitionLabel | E-011 | kept; + `fixedDefinition`, `fixedDefinitionLevel`, `axiom table SD-DF` (INV-125) |
| E-012 | PeriodValue | E-012 | kept; + `daysWithin` (INV-121); catalogue OC-35 for the `ofType` scopes |
| E-013 | CompletenessIndicator | E-013 | kept; formal text unchanged |
| E-014 | DayCount | E-014 | kept; + `nestedIn` (INV-122) |
| E-015 | HeadacheDays | E-015 | kept; formal text unchanged |
| E-016 | MigraineDays | E-016 | kept; formal text unchanged |
| E-017 | ModerateSevereHeadacheDays | E-017 | kept; formal text unchanged |
| E-018 | MigraineOrModerateSevereHeadacheDays | E-018 | kept; formal text unchanged |
| E-019 | EventCount and AttackCount | E-019 | kept; formal text unchanged |
| E-020 | HeadacheFreeDays | E-020 | kept; formal text unchanged |
| E-021 | SymptomFreeDays | E-021 | kept; formal text unchanged |
| E-022 | MigraineFreePeriodMark | E-022 | kept; formal text unchanged |
| E-023 | IntensitySummary | E-023 | kept; formal text unchanged |
| E-024 | DurationSummary | E-024 | kept; formal text unchanged |
| E-025 | AssociatedSymptomSummary | E-025 | kept; formal text unchanged |
| E-026 | MostBothersomeSymptomItem | E-026 | kept; formal text unchanged |
| E-027 | Aura measures | E-027 | kept; formal text unchanged |
| E-028 | AcuteDrugClass | E-028 | kept; `classCode` axiom → SD-CLS (`axiom table SD-CLS`, which also gives `overuseLevel` of each class, D-6); domain comment of `classOf` reduced to its gloss (plan section 3.4) |
| E-029 | AcuteMedicationDays | E-029 | kept; + `medicationKinds` (C1-10, C1-13) |
| E-030 | FunctionalImpactDays | E-030 | kept; formal text unchanged |
| E-031 | CaregiverImpact | E-031 | kept; formal text unchanged |
| E-032 | MedicationOveruseIndicator | E-032 | kept; general `ofClassUse` axiom stays; combined-use parts → SD-CMB (`axiom table SD-CMB`); `overuseLevel` of each class → SD-CLS, stated once in E-028 (D-6); `overuseSpanMonths` → SD-FX-06 |
| E-033 | CompositeIndex | E-033 | kept; `components` gets marker `shown SHOULD when concerns(…, c1)` (W2, ex INV-092) |
| E-034 | TreatmentMarker | E-034 | kept; `event` typed `{k : CourseEventKind \ | markedKind(k)}` (ex INV-036) |
| E-035 | TimeCourseView | E-035 | kept; `series`, `markers` get marker `shown SHOULD` (W2, ex INV-035) |
| E-036 | WeeklyMedicationView | E-036 | kept unchanged; catalogue kind of OC-16 (availability now C1-11) |
| E-037 | PeriodComparison | E-037 | kept; formal text unchanged |
| E-038 | ThreeMonthPatternView | E-038 | kept; `series` gets marker `shown` (W2, ex INV-041) |
| E-039 | WithdrawalFollowUpView | E-039 | kept; `series` gets marker `shown SHOULD` (W2, ex INV-050); three `const` → SD-FX-03, 04, 05 (a comment names the table, D-7) |
| E-040 | Change | E-040 | kept; `reference`, `compared` get marker `shown MUST when ofResponseComparison(self)` (W2, ex INV-054) |
| E-041 | EvaluationRule | E-041 | kept; rule constants, axiom and `evaluationRules` → SD-ER-01…18 (`≙ table SD-ER`) |
| E-042 | EvaluationTimePoint | E-042 | kept; `shortestMonthlyDays` → SD-FX-08 (a comment names the table, D-7) |
| E-043 | ResponseComparison | E-043 | kept; `timePoints` gets marker `shown MUST` (W2, ex INV-059) |
| E-044 | ResidualBurden | E-044 | kept; formal text unchanged |
| E-045 | ResponderCriterion | E-045 | kept; criteria constants, axiom and `namedCriteria` → SD-RC-01…06 (`≙ table SD-RC`) |
| E-046 | ResponderLabel | E-046 | kept; `comparison`, `residual`, `otherValues` get marker `shown SHOULD` (W2, ex INV-062); + `inControlRange`, `controlMinMonths`, `forcedAbove` (SD-CL) |
| E-047 | AdherenceSummary | E-047 | kept; formal text unchanged |
| E-048 | TreatmentReviewView | E-048 | kept; formal text unchanged |
| E-049 | PostStopMonitoringView | E-049 | kept; `event` typed (ex INV-112); `onTreatmentPeriod` `when` gains INV-070's ask as a disjunct for unstated starts (R-MCF (2); equivalent; check 28, watch point 1) |
| E-050 | AcuteOutcomeMeasure | E-050 | kept; + `earlyTimePointType` (SD-ET) |
| E-051 | AcuteTreatmentSummary | E-051 | kept; `outcomes`, `sequence` get marker `shown SHOULD` (W2, ex INV-072) |
| E-052 | OutcomeSummary | E-052 | kept; formal text unchanged |
| E-053 | TreatedAttackLine | E-053 | kept; formal text unchanged |
| E-054 | TreatmentHistoryView and ClassGroup | E-054 | kept; `preventiveGroups`, `acuteGroups` get marker `shown SHOULD` (W2, ex INV-078) |
| E-055 | TreatmentLine | E-055 | kept; `preventiveResponse`, `acuteResponse`, `adherence` get marker `shown SHOULD` (W2, ex INV-109) |
| E-056 | SchemeWindowView | E-056 | kept; formal text unchanged |
| E-057 | Instrument value sets | E-057 | kept; value-set axioms → SD-IN-01…09 (`axiom table SD-IN`), `gradeBands` → SD-GB-01…16 (`≙ table SD-GB`); domain comments deleted; `otherInstrument` name axiom kept |
| E-058 | InstrumentResult | E-058 | kept; formal text unchanged |
| E-059 | ScreeningResult | E-059 | kept; `screeningName` axiom → SD-SC-01…03; + `screeningMax` with SD-SR-01…04 |
| E-060 | MenstrualRelationView and CycleLine | E-060 | kept; `attacks` gets marker `shown` (W2, ex INV-087); + `shownDayOnes` (INV-124); two `const` → SD-FX-01, 02 (a comment names the table, D-7) |
| E-061 | AttackMark | E-061 | kept; formal text unchanged |
| E-062 | ClusterView | E-062 | kept; formal text unchanged |
| E-063 | ClusterPeriodItem and RemissionPeriodItem | E-063 | kept; `remissionMoreThanMonths` → SD-FX-07 (a comment names the table, D-7) |
| E-064 | ClusterAttackRate | E-064 | kept; formal text unchanged |
| E-065 | TriggerCooccurrenceView | E-065 | kept; formal text unchanged |
| E-066 | ClinicianSummary | E-066 | kept; formal text unchanged |
| E-067 | PatientOverview | E-067 | kept; formal text unchanged |
| INV-001 | Admissible contexts | INV-001 | kept; formal text unchanged |
| INV-002 | Period length and kind agree with the dates | INV-002 | kept; formal text unchanged |
| INV-003 | Every view states its period, and every period it uses is shown in it | INV-003 | kept; formal text unchanged |
| INV-004 | A series consists of consecutive periods of its granularity | INV-004 | kept; formal text unchanged |
| INV-005 | A number of days does not exceed the period length | INV-121 | withdrawn as merged (model section 9) |
| INV-006 | One value per measure, period and scope in a view | INV-006 | kept; formal text unchanged |
| INV-007 | An annotation is shown with what it qualifies | W2: E-010 `qualifies` | withdrawn as merged (model section 9) |
| INV-008 | Definition labels for the defined measures | INV-008 | kept; formal text unchanged |
| INV-009 | Headache days follow ICHD-3 | INV-125 (SD-DF-01) | withdrawn as merged (model section 9) |
| INV-010 | Attacks follow ICHD-3 | INV-125 (SD-DF-02) | withdrawn as merged (model section 9) |
| INV-111 | One definition per measure in a view | INV-111 | kept, edited: third conjunct added (CHG-06) |
| INV-011 | A completeness indicator accompanies each reporting period | INV-011 | kept; formal text unchanged |
| INV-012 | Completeness values agree with the period | INV-012 | kept, edited: covered days ≤ length → INV-121 |
| INV-013 | No completeness cut-off presented as clinically validated | INV-119 (C2-02) | withdrawn as merged (model section 9) |
| INV-014 | Headache days per reporting period | INV-118 (C1-01) | withdrawn as merged (model section 9) |
| INV-015 | Migraine days per reporting period, for patients with migraine | INV-118 (C1-02) | withdrawn as merged (model section 9) |
| INV-016 | Moderate/severe headache days per reporting period | INV-118 (C1-03) | withdrawn as merged (model section 9) |
| INV-017 | Attacks per reporting period | INV-118 (C1-05) | withdrawn as merged (model section 9) |
| INV-108 | Moderate/severe headache days and attacks per calendar month or 28-day period, where provided | INV-118 (C1-04, C1-06) | withdrawn as merged (model section 9) |
| INV-018 | Intensity summary per reporting period | INV-118 (C1-07) | withdrawn as merged (model section 9) |
| INV-019 | Duration summary per reporting period | INV-118 (C1-08) | withdrawn as merged (model section 9) |
| INV-020 | Durations of treated attacks are labelled as influenced by acute treatment | INV-120 (C3-03) | withdrawn as merged (model section 9) |
| INV-021 | Durations of treated attacks are not a stand-alone efficacy measure | INV-119 (C2-03; CHG-07) | withdrawn as merged (model section 9) |
| INV-022 | Associated symptoms and most bothersome symptom across periods, for migraine | INV-118 (C1-09) | withdrawn as merged (model section 9) |
| INV-023 | Acute-medication days per reporting period: total, by class and by drug | INV-118 (C1-10) | withdrawn as merged (model section 9) |
| INV-024 | Totals, classes and drugs agree | INV-024 | kept, edited: four ≤ bounds → INV-122; keeps the three sum bounds |
| INV-025 | Weekly view of acute-medication days | INV-118 (C1-11) | withdrawn as merged (model section 9) |
| INV-026 | Functional impact per reporting period | INV-118 (C1-12) | withdrawn as merged (model section 9) |
| INV-027 | Functional impact compared with the baseline period | INV-027 | kept; formal text unchanged |
| INV-028 | Separate presentation per headache type | INV-118 (C1-13) | withdrawn as merged (model section 9) |
| INV-029 | Intensity per headache type, where provided | INV-118 (C1-14) | withdrawn as merged (model section 9) |
| INV-030 | Values per headache type do not exceed the combined values | INV-122 | withdrawn as merged (model section 9) |
| INV-031 | Relations between day measures | INV-031 | kept, edited: two nesting bounds → INV-122; last conjunct removed (CHG-04) |
| INV-032 | Intensity values lie on their scale | INV-032 | kept, edited: level days ≤ length → INV-121 |
| INV-033 | Further bounds of per-period values | INV-033 | kept, edited: pain time, symptom days, caregiver days → INV-121; functional-impact bounds → INV-122; keeps attacks-with-symptom bound |
| INV-034 | Time-course view available | INV-034 | kept; formal text unchanged |
| INV-035 | Time-course content and treatment markers | INV-035 | kept, edited: two placements → W2 (E-035) |
| INV-036 | Markers show the treatment course | INV-123 + E-034 attribute type | withdrawn as merged (model section 9) |
| INV-037 | Comparison of selected periods of equal length | INV-037 | kept; formal text unchanged |
| INV-038 | Comparison values refer to the compared periods | INV-038 | kept; formal text unchanged |
| INV-039 | Intensity can be compared between periods | INV-039 | kept; formal text unchanged |
| INV-040 | Three-month pattern view available | INV-040 | kept; formal text unchanged |
| INV-041 | Structure of the three-month pattern view | INV-041 | kept, edited: `v.series ∈ v.content` → W2 (E-038) |
| INV-042 | Three-month view shows the definitions it refers to | INV-042 | kept; formal text unchanged |
| INV-043 | Three-month view assigns no diagnosis | INV-119 (C2-08) | withdrawn as merged (model section 9) |
| INV-044 | Medication-overuse indicator per period, per class and for combined use | INV-044 | kept; formal text unchanged |
| INV-045 | Medication-overuse indicator agrees with its code, level, span and basis | INV-045 | kept; formal text unchanged |
| INV-046 | Combined use of ICHD-3 8.2.6 | INV-046 | kept; formal text unchanged |
| INV-047 | Indicator worded as a prompt for clinical review | INV-120 (C3-04) | withdrawn as merged (model section 9) |
| INV-048 | Indicator is not a diagnosis of medication-overuse headache | INV-119 (C2-04) | withdrawn as merged (model section 9) |
| INV-049 | Withdrawal follow-up view available | INV-049 | kept; formal text unchanged |
| INV-050 | Withdrawal follow-up content | INV-050 | kept, edited: `sr ∈ v.content` → W2 (E-039); review-window conjunct removed as implied (CA-05, no change) |
| INV-113 | A withdrawal follow-up view shows a start of withdrawal of the subject | INV-123 | withdrawn as merged (model section 9) |
| INV-051 | The NICE CG150 1.3.48 review window | INV-051 | kept; formal text unchanged |
| INV-052 | Label of the expected transient worsening | INV-120 (C3-06) | withdrawn as merged (model section 9) |
| INV-053 | Absolute and percentage change agree with the values they compare | INV-053 | kept; formal text unchanged |
| INV-054 | A change of a response comparison is shown with the values it compares | W2: E-040 `reference`, `compared` | withdrawn as merged (model section 9) |
| INV-055 | Response comparison for each preventive treatment, at the evaluation time points | INV-055 | kept; formal text unchanged |
| INV-056 | Response comparison content | INV-056 | kept, edited: treatment and start facts → INV-123 (CHG-R1) |
| INV-057 | Moderate/severe headache days in the comparison, where reported | INV-057 | kept; formal text unchanged |
| INV-058 | Evaluation time points agree with their rule and anchor | INV-058 | kept; formal text unchanged |
| INV-059 | Evaluation time points shown with the comparison | INV-059 | kept, edited: `tp ∈ viewOf(rc).content` → W2 (E-043) |
| INV-060 | Residual burden next to a percentage change | INV-060 | kept, edited: antecedent restricted to compared periods ≥ 28 days (CHG-03) |
| INV-061 | Residual burden refers to a monthly on-treatment period | INV-061 | kept; formal text unchanged |
| INV-062 | A responder label shows its criterion and the values it rests on | INV-062 | kept, edited: three placements → W2 (E-046) |
| INV-114 | A responder label's response comparison is one of the label's treatment | INV-114 | kept; formal text unchanged |
| INV-116 | A criterion shown under the name of a named criterion is that criterion | INV-116 | kept; formal text unchanged |
| INV-117 | A responder label concerns one of the subject's preventive treatments | INV-123 | withdrawn as merged (model section 9) |
| INV-063 | A responder label agrees with the decidable components of its criterion | INV-063 | kept; formal text unchanged |
| INV-064 | Control levels of the IHS position statement 2025 | INV-064 | kept, edited: reformulated with SD-CL (equivalent) |
| INV-065 | A responder label is not the sole indicator of individual benefit | INV-119 (C2-06; CHG-07) | withdrawn as merged (model section 9) |
| INV-066 | Adherence next to the response comparison | INV-066 | kept; formal text unchanged |
| INV-067 | Adherence refers to the time on treatment | INV-067 | kept, edited: treatment fact → INV-123 |
| INV-068 | Treatment review view: frequency and medication for the same periods | INV-068 | kept, edited: treatment fact → INV-123 (CHG-R1) |
| INV-069 | Treatment review view: further dimensions where provided | INV-069 | kept; formal text unchanged |
| INV-070 | Post-stop monitoring content | INV-070 | kept, edited: presence ask → E-049 `when` (equivalent) |
| INV-112 | Post-stop monitoring shows the subject's event and its periods | INV-112 | kept, edited: treatment and event facts → INV-123, event kinds → E-049 type; keeps the period bounds |
| INV-071 | Acute-treatment summaries per drug, per formulation and per preventive phase | INV-071 | kept; formal text unchanged |
| INV-072 | Acute-treatment summary content | INV-072 | kept, edited: two placements → W2 (E-051) |
| INV-073 | Early time point: 15 minutes for cluster headache, otherwise 2 hours | INV-073 | kept, edited: reformulated with SD-ET (equivalent) |
| INV-074 | Outcome counts agree with the summary and its attack lines | INV-074 | kept; formal text unchanged |
| INV-075 | Attack lines are consistent | INV-075 | kept, edited: medication fact → INV-123 |
| INV-076 | Associated symptoms in the response of treated attacks, for migraine | INV-076 | kept; formal text unchanged |
| INV-077 | Treatment history lists every treatment | INV-077 | kept; formal text unchanged |
| INV-078 | Treatment history is chronological and grouped by drug class | INV-078 | kept, edited: group placement → W2 (E-054); keeps line placement |
| INV-079 | Treatment lines agree with the treatment course | INV-079 | kept, edited: course facts and formulation fact → INV-123; keeps drug, durations, identity ties |
| INV-109 | A treatment line shows every dose change, and its response summary and adherence with it | INV-109 | kept, edited: three placements → W2 (E-055) |
| INV-080 | Scheme windows are the selected windows | INV-080 | kept; formal text unchanged |
| INV-081 | Results of validated instruments where available | INV-081 | kept; formal text unchanged |
| INV-082 | Instrument results agree with the instrument's published value set | INV-082 | kept, edited: availability → INV-123 |
| INV-083 | Screening results next to the headache outputs | INV-083 | kept; formal text unchanged |
| INV-084 | Screening results are not psychiatric diagnoses | INV-119 (C2-09) | withdrawn as merged (model section 9) |
| INV-085 | Screening scores lie in the instrument's range | INV-085 | kept, edited: availability → INV-123; ranges reformulated with SD-SR (equivalent) |
| INV-086 | Menstrual-relation view for patients who menstruate | INV-086 | kept; formal text unchanged |
| INV-087 | Menstrual cycles, the perimenstrual window and attacks | INV-087 | kept, edited: attack placement → W2 (E-060) |
| INV-088 | Cluster-headache view | INV-088 | kept; formal text unchanged |
| INV-089 | Cluster periods, remissions and rates are consistent | INV-089 | kept, edited: bout–remission non-overlap → INV-124 (output-wide) |
| INV-090 | Caveats of the trigger co-occurrence view | INV-120 (C3-09) | withdrawn as merged (model section 9) |
| INV-110 | The dates of a trigger co-occurrence view lie in the period it covers | INV-110 | kept; formal text unchanged |
| INV-091 | No composite index as a primary measure for migraine | INV-091 | kept; formal text unchanged |
| INV-092 | A migraine composite index is exploratory and shown with its components | INV-092 | kept, edited: annotation → INV-120 (C3-12); placement → W2 (E-033); keeps dimension coverage |
| INV-115 | The components of a composite index for migraine are of its period and type scope | INV-115 | kept; formal text unchanged |
| INV-093 | AUC as a primary measure for tension-type headache is shown with headache days | INV-093 | kept; formal text unchanged |
| INV-094 | Clinician-facing summary available | INV-094 | kept; formal text unchanged |
| INV-095 | Patient-facing overview available | INV-095 | kept; formal text unchanged |
| INV-096 | Paediatric outputs: PedMIDAS, school days and caregiver impact | INV-096 | kept; formal text unchanged |
| INV-097 | Paediatric comparisons use periods of equal length | INV-097 | kept; formal text unchanged |
| INV-098 | Paediatric outputs are presented as supportive information | INV-120 (C3-11) | withdrawn as merged (model section 9) |
| INV-099 | Interpretive caveats on every summary | INV-120 (C3-01) | withdrawn as merged (model section 9) |
| INV-100 | Indicators, labels and associations require clinical interpretation | INV-120 (C3-05, C3-07, C3-08, C3-09, C3-10) | withdrawn as merged (model section 9) |
| INV-101 | No output presented as replacing clinical assessment or as a diagnosis | INV-119 (C2-01) | withdrawn as merged (model section 9) |
| INV-102 | Treatment review view available for each preventive treatment | INV-102 | kept; formal text unchanged |
| INV-103 | Post-stop monitoring available after a stop, pause or reduction | INV-103 | kept; formal text unchanged |
| INV-104 | Clinician-facing summary content | INV-104 | kept; formal text unchanged |
| INV-105 | Patient-facing overview content | INV-105 | kept; formal text unchanged |
| INV-106 | No output decides on the continuation of a preventive treatment | INV-119 (C2-05) | withdrawn as merged (model section 9) |
| INV-107 | No output decides which definition of acute treatment response applies | INV-119 (C2-07) | withdrawn as merged (model section 9) |

## 5. Deviations from the plan

Each is the minimal choice that keeps the meaning of v34 (or of the planned change); none changes the meaning of a formal text.

1. **D-1, section 2.1.** "Everything outside these blocks (Meaning, Reading, comments) is explanatory" would contradict section 2.11 (case tables have formal columns). It now reads that OMN text appears in `omn` blocks and in the formal columns of case tables.
2. **D-2, section 2.7.** The bullet on thresholds said each is supported by a quote "in the element's Evidence". The quotes are now in `RATIONALE.md` (PROCESS.md section 6, from v35), and values sit in the source data tables; the bullet says so.
3. **D-3, section 3.5.** "The Audience line … is stated in the element's Meaning" became "… in the catalogue (section 4.3, column Audience)", because plan 9.1 moves the audience sentences out of the Meanings.
4. **D-4, section 2.11.** Four additions to the planned text: (a) every case table denotes its paragraphs wherever it stands, and the paragraph forms name a table where its functions are declared (SD-FX has no single declaration to carry a reference); (b) **form D** (defined constants, `` `k` ``, `` `type` ``, `` `value` ``), which the plan uses for SD-FX ("V-like") but does not define; (c) in form C, the arguments of a header may be terms built from the key variables, as the plan's SD-CLS header `overuseLevel(ofClassUse(k))` requires; (d) a scope bullet (no case table holds input data, storage or a derivation from input; check C9) and a pointer to the worked unfoldings (RATIONALE SEC-2.11/W01).
5. **D-5, rule W2.** Two clarifications of the planned text: `shown` is a keyword that ends a `when` clause; a marker without its own `when` applies to every atom, and the attribute's `when φ` does not restrict it (the plan's E-046 `otherValues` row: "no marker `when`; the attribute keeps its own"). W2 is a bullet after rule W1 in section 2.5, and section 6.0 lists the marked attributes as an index.
6. **D-6, `axiom table SD-CLS` once.** Plan section 8 puts `axiom table SD-CLS` in E-028 (for `classCode`) and again in E-032 (for `overuseLevel`). Stating the same axioms twice would be a duplication; v35 states it once, in E-028, and E-032 has `axiom table SD-CMB` with a comment that points to SD-CLS for the levels of the classes.
7. **D-7, constants moved to SD-FX.** The `const` lines of E-032, E-039, E-042, E-060 and E-063 are removed (form D denotes them); E-039, E-042, E-060 and E-063 keep a comment line that names table SD-FX, and E-032's comment names SD-CLS and SD-CMB. Values, names and types are unchanged (C4).
8. **D-8, catalogue column Realises.** Plan section 4.3 says the column equals the union of the Realises fields of the items named in the row; the plan's own values are not that union (OC-05 names E-014, whose Realises lists nine requirements). v35 keeps the plan's values and defines the column as "the requirements whose statements name this kind of output; each is in the Realises field of an item named in the row", checked by script (C3). Two catalogue cells that cited fix-log IDs were rewritten to cite model items: OC-22 "(…, CHG-03, ISS-13)" → "(…: INV-060; ISS-13)"; OC-37 "— (no placement: fix 11 kept; CA-09)" → "— (no placement: E-062/X01)".
9. **D-9, Realises of INV-122.** The plan's list plus OUT-036: the functional-impact nesting of v34 INV-033 covers the school days missed or impaired of OUT-036 (b) (`paidWorkOrSchool`), which v34 INV-033 realised.
10. **D-10, RATIONALE layout.** Entry headings are level 4 under the subsections of section 2. A `Q` entry has the fields Location, Quote and Translation where the v34 bullet had exactly the form `[S-NNN] "quote" (location)[. Translation: "…"]` (62 entries; each reconstructs the v34 text exactly, C5); otherwise (the lead texts Q00 and bullets with several quotes) it has one verbatim Text field. An Evidence lead without a source quote stays in the model verbatim (a Stage 1 citation, sometimes with Stage 1 wording); pointer bullets became entry IDs (E-028 → E-009/Q03; E-032 → E-028/Q02, E-028/Q03, INV-046/Q01; E-045 → E-046/Q01 to Q05).
11. **D-11, entries of merged invariants.** INV-054's Notes merged into E-040/D01 as a second Text field, all of it, together with E-040 Notes [3]–[4], which the plan marked R: these sentences are quoted by oscillation check 12 for its watch point 3 ("this does not require the two values next to the change"; "The R10b-01 sentence of the INV-054 Notes"), so rule P0 keeps them as D text. For the same reason E-043 Notes [1]–[2] ("the two values it compares (INV-054)", quoted by check 12) went to E-043/D01, and E-057 Notes [12] (CA-11 sentence) to E-057/D07 instead of R. The Notes of v34 INV-028 (not in plan 9.2) went to INV-118/D02, and those of v34 INV-113 to INV-123/D06 and S02.
12. **D-12, the INV-070 Reading.** The purpose clause "so that worsening or rebound above baseline is visible" is kept in the rewritten Reading (check 32 records its re-insertion as an artefact; keeping it avoids another change of the text).
13. **D-13, references to v34 Notes paragraphs** in kept model text were updated to the entries that hold them: E-041 Meaning "(Notes, **Readings**)" → E-041/D05; E-045 Meaning "(Notes, **Other values**)" → E-045/D07; section 9 ISS-07 row "described in the Notes of E-057 and E-045" → "described in E-057/D02 and E-045/D03"; ISS-10 "(E-041 Notes)" → "(E-041/D01, E-041/D02)"; ISS-12 "(E-063 Notes)" → "(E-063/D01)". In moved text, "X Notes" is kept and defined in RATIONALE section 1 (the v34 Notes of X, now the model's Notes of X and the entries anchored at X).
14. **D-14, P0 for kept invariants that lost a conjunct** (plan 11, last paragraph): moved text that cites such an invariant for the moved conjunct now cites its new place (15 entries: E-008/D02, E-041/D03, E-043/D01, E-048/D01, E-051/D01, E-057/D07, INV-027/S01, INV-035/D01, INV-062/D01, S01, S02, INV-112/D01, S01, INV-114/S01, INV-123/D03). INV-049's example became INV-049/W01 (plan: "D01 with its example W01"); the sentence was split at its colon.
15. **D-15, E-019 Meaning (CA-10).** The corrected wording keeps the reference to ICHD-3 "Definitions of terms" [S-001], so that the source attribution of v34 is not lost.
16. **D-16, new RATIONALE entries not named in the plan:** INV-118/D03, INV-119/D04, INV-120/D03, INV-121/D01, INV-122/D02, INV-123/D07, INV-124/D01, INV-125/D01 (the equivalence arguments of plan section 5, shortened), INV-123/D01 (fix 32's attribute table, updated to v35, as plan section 5 states), E-049/D04 (the merged `when` clause), INV-031/X01 (CHG-04), INV-060/D02 (CHG-03), INV-111/D02 (CHG-06), INV-050/D02 (CA-05), E-062/X01 (CA-09), the 35 case-row entries C1-NN/D01, C2-NN/D01, C3-NN/D01 (the v34 origin of each case, risk R3), SEC-2.11/W01 (worked unfoldings), SEC-3.4/D01 (the moved argument of section 3.4) and SEC-3.8/D01 (the v34 places of R-MCF, plan section 7.2).
17. **D-17, model section 12.** One introductory sentence; the first bullet line of each version v00 to v34, verbatim; the v35 entry.
18. **D-18, ISS fields.** The Evidence field of each issue names the entries ISS-NN/Qnn; the two general paragraphs that followed ISS-12 in v34 ("ISS-07 was withdrawn …", "No output was found …") now follow ISS-13.

## 6. Prose

- **Rules applied** (plan section 9): Meanings keep what the element shows, the glosses and value-domain remarks; 37 audience sentences dropped from the Meanings (the Audience lines are in the catalogue); reasons and date examples moved (E-001, E-007, E-008, E-042, E-045). Readings: the 29 edited invariants and INV-055 have new Readings that paraphrase their predicates; INV-001, INV-008, INV-037, INV-038, INV-081, INV-104, INV-110 lost consequences drawn with other items; the CA-08, CA-09 and CA-16 wording was applied. Element Conformance fields follow the template (availability, applicability with R-MCF, content, definitional, labels and caveats, prohibited, placement), as IDs only. Notes keep "Relations: <IDs>", at most the short formal explanations that plan 9.2 marks K, the pointers to issues and to R-MCF, and "Rationale: <entry IDs>".
- **Moved verbatim:** every quote (C5), every Notes paragraph that plan 9.2 marks D, N, S, W or X (and the default dispositions for Notes under 900 bytes), the search log (97 lines, identical), the section 3.4 argument.
- **Dropped as restatements** (plan 9.2, R): 139 sentences of Notes and Meanings (31,042 bytes), and the coverage reasons of section 7. None contains a source quote (C5) or a sentence quoted in a watch point of oscillation checks 12 to 32 (C6; D-11).
- **Corrected** (P0 exception 2): the sentences named in section 2 above for R35-01, CA-05, CA-06, CA-07, CA-12, CA-14, CA-15, CA-16; references to merged invariants replaced by their v35 places throughout (script `p0.py`, with ranges such as "INV-030 to INV-033" expanded).

## 7. Checks

All checks were run by script (`checks.py`, `c7/`, `witness.py`) on the files as written; the results:

| Check | Result | Numbers |
|---|---|---|
| C1 ID accounting | pass | E kept 67/67; INV kept 79, merged rows 38; new INV INV-118..INV-125 (8); OC 45, C1 14, C2 9, C3 12, SD rows 94; ISS-13 True; missing []; both []; map mismatches []; duplicates [] |
| C2 Formal identity | pass | byte-identical to v34: 37 elements, 50 invariants; edited exactly by the scripted plan section 8 edits: 30 elements, 29 invariants; problems [] |
| C3 Traceability | pass | Realises mapped through section 9 and the generic invariants: no (v34 item, OUT) pair lost and no v35 OUT without a v34 source (0 problems: []); traceability rows 39/39; catalogue rows whose Realises names an OUT that no item named in the row realises: [] |
| C4 Case tables | pass | source data tables parsed back from the model: tables 13 rows 94 cell checks 121 mismatches 0; C1/C2/C3 rows identical to the plan (minus the Replaces column): 35/35; key subterms found in the replaced v34 predicates: 13/13 |
| C5 Quotes | pass | source-attributed quotes in v34 sections 1-11: 398 occurrences (308 distinct); each found in v35 model + RATIONALE at least as often; lost: []; structured Q entries whose [S] "quote" (location) reconstructs the v34 text exactly: 62/62 (bad []) |
| C6 Watch-point text | pass | protected texts present 5/5 (missing []); sentences that must not be restored found: []; ISS-02/ISS-03 fields verbatim 6/6; section 3.5 list verbatim (Audiences line edited): True |
| C7 Equivalence re-run | pass | generic predicates and reformulated INV-064/073/085 are the plan's text verbatim (white space aside), which the re-run scripts encode; differing: []. Script results: see c7/results.txt |
| C8 Levels | pass | v34 {'definitional': 40, 'MUST': 19, 'SHOULD': 48, 'SHOULD NOT': 8, 'MUST NOT': 2}; withdrawn {'MUST': 8, 'SHOULD NOT': 7, 'SHOULD': 15, 'definitional': 6, 'MUST NOT': 2}; v35 {'level-indexed': 4, 'definitional': 38, 'MUST': 11, 'SHOULD': 33, 'SHOULD NOT': 1}; level-indexed cases by level: C tables {'must': 7, 'should': 18, 'shouldNot': 7, 'mustNot': 2, 'may': 1} + SD-DF {must: 1, should: 1}; kept levels unchanged except CHG-R1 (conjuncts only) |
| C9 Scope | pass | new formal text (2.11, section 4, 6.0, section 11) contains no input, storage or derivation-from-input terms: []; whole-document counts v34 -> v35+RATIONALE: {'JSON': 0, 'FHIR': 0, 'database': 0, 'recorded': 0, 'entered': 0} -> {'JSON': 0, 'FHIR': 0, 'database': 0, 'recorded': 0, 'entered': 0} |
| C10 Prose | pass | overclaiming sentences of CA-04/06/08/10/12/14/15/16 and R35-01 remaining: []; every element Conformance field is the template: True; Readings of the 29 edited invariants rewritten to their predicates (disp_reading.RT/RS) |
| IDs and entries | pass | E/INV/ISS IDs referenced: 205, unresolved []; RATIONALE entries 432 (duplicates []); entry IDs referenced from model 362, from RATIONALE 397, unresolved []; entries with unknown anchor []; entries not referenced from the model (C, SEC excluded) 0: []; OC/C/SD references unresolved [] |

**C7 re-run** (the architect's scripts, copied unchanged, and a refined R35-01 test on the v35 rules):
- `eq_g1.py`: 200,000 models, 0 mismatches (INV-118 with C1 against v34 INV-014–019, 022, 023, 025, 026, 028, 029, 108); `eq_g1_mut.py`: 1,161 mismatches (the test detects quantifier placement).
- `eq_g2g3.py`: 100,000 models; MUST NOT 0 mismatches; SHOULD NOT 349 differences, all of the kind of CHG-07 (0 unexplained); annotations (INV-120 with C3) 0 at SHOULD and 0 at MUST.
- `eq_misc.py`: INV-122 nesting 0 mismatches; INV-064 with SD-CL 29,520 cases, 0; INV-085 with SD-SR 1,296 cases, 0; INV-123 role facts 0; E-049/INV-070 merge 970 cases, 0.
- `r3501_v35.py`: see R35-01 above (0 wrong marks on lines that have ended, in 259,169 admitted outputs).
- The generic predicates, the case cells and the reformulated INV-064, INV-073 and INV-085 are the plan's text verbatim (white space aside), which is what these scripts encode.

**Satisfiability witness** (`witness.py`): a repertoire of two contexts (28-day and weekly granularity; a subject with migraine and tension-type headache, one triptan, one preventive treatment with a stated start) and two outputs (589 atoms: series, day counts of every C1 kind for all types and per type, intensity, duration and symptom summaries, completeness indicators, definition labels, the C3 annotations, a treatment marker, a lead-in and three cycle lines, a cluster period and a remission period). It satisfies every instance of INV-118 (must, should), INV-119 (shouldNot, mustNot), INV-120 (must, should), INV-121, INV-122, INV-123, INV-124, INV-125 (must, should), together with the kept invariants they interact with: INV-001 (the parts used), INV-002, INV-003, INV-004, INV-006, INV-008, INV-011, INV-012, INV-024, INV-031, INV-087 (per line), INV-089 and INV-111. A second witness (`r3501_v35.py`) shows two views whose cycle lines meet INV-087 and INV-124 together.

**Other checks.** Every E-, INV- and ISS- ID referenced in the model and in `RATIONALE.md` resolves (205 IDs); every OC, C1–C3 and SD row referenced exists; no ID is duplicated (items, rows, entries); every RATIONALE entry is anchored to an existing item, row or section; every entry ID referenced from the model or from RATIONALE exists; every entry except the case-row and section entries is referenced from the model (the case-row entries are named in section 4.4, the section entries in sections 2.11, 3.4 and 3.8). `cmp OUTPUT_MODEL.md history/v35.md` and `cmp RATIONALE.md history/v35-rationale.md`: identical.

## 8. Diff summary of the formal blocks

- **Byte-identical to v34** (37 elements, 50 invariants): E-002, E-003, E-004, E-005, E-006, E-007, E-013, E-015, E-016, E-017, E-018, E-019, E-020, E-021, E-022, E-023, E-024, E-025, E-026, E-027, E-030, E-031, E-036, E-037, E-044, E-047, E-048, E-052, E-053, E-056, E-058, E-061, E-062, E-064, E-065, E-066, E-067; INV-001, INV-002, INV-003, INV-004, INV-006, INV-008, INV-011, INV-027, INV-034, INV-037, INV-038, INV-039, INV-040, INV-042, INV-044, INV-045, INV-046, INV-049, INV-051, INV-053, INV-055, INV-057, INV-058, INV-061, INV-063, INV-066, INV-069, INV-071, INV-074, INV-076, INV-077, INV-080, INV-081, INV-083, INV-086, INV-088, INV-091, INV-093, INV-094, INV-095, INV-096, INV-097, INV-102, INV-103, INV-104, INV-105, INV-110, INV-114, INV-115, INV-116.
- **Changed** (exactly the edits of plan section 8, applied by `formal.py`; 30 elements, 29 invariants): E-001, E-008, E-009, E-010, E-011, E-012, E-014, E-028, E-029, E-032, E-033, E-034, E-035, E-038, E-039, E-040, E-041, E-042, E-043, E-045, E-046, E-049, E-050, E-051, E-054, E-055, E-057, E-059, E-060, E-063; INV-012, INV-024, INV-031, INV-032, INV-033, INV-035, INV-041, INV-050, INV-056, INV-059, INV-060, INV-062, INV-064, INV-067, INV-068, INV-070, INV-072, INV-073, INV-075, INV-078, INV-079, INV-082, INV-085, INV-087, INV-089, INV-092, INV-109, INV-111, INV-112.
  - New declarations inside changed elements: `presents`, `factsShown` (E-001); `ShownFact`, `inMedicationScope`, `stated` (E-008); `fixedDefinition`, `fixedDefinitionLevel` (E-011); `daysWithin` (E-012); `nestedIn` (E-014); `medicationKinds` (E-029); `inControlRange`, `controlMinMonths`, `forcedAbove` (E-046); `earlyTimePointType` (E-050); `screeningMax` (E-059); `shownDayOnes` (E-060).
  - Placement markers: E-010, E-033, E-035, E-038, E-039, E-040, E-043, E-046, E-051, E-054, E-055, E-060 (section 6.0 list). Attribute types narrowed by moved conjuncts: E-034 `event`, E-049 `event`. `when` clause: E-049 `onTreatmentPeriod` (two disjuncts; the first is v34's, verbatim).
  - Values moved to source data tables (`axiom table …`, `≙ table …`): E-009 (SD-IC), E-028 (SD-CLS), E-032 (SD-CMB; SD-FX-06), E-039 (SD-FX-03 to 05), E-041 (SD-ER), E-042 (SD-FX-08), E-045 (SD-RC), E-057 (SD-IN, SD-GB), E-059 (SD-SC; SD-SR), E-060 (SD-FX-01, 02), E-063 (SD-FX-07); INV-064 (SD-CL), INV-073 (SD-ET), INV-085 (SD-SR) reformulated.
- **Changed blocks outside items:** section 3.2 (`Ctx`, `Rep`, `ctx`, `parts`: comments reduced to glosses; their conditions are normative sentences after the block, CA-11). The section 2.8 and 3.4 blocks are byte-identical.
- **New blocks:** section 3.1 (`enum Level`), section 4.4 (`CatalogueRow`, `ppGranularities`, `ppRequired`, `prohibitedClaims`, `requiredAnnotations`), INV-118 to INV-125; the case tables C1–C3 (section 4.4) and SD-IC to SD-ET (section 11).
- **Removed blocks:** the 38 merged invariants: INV-005, INV-007, INV-009, INV-010, INV-013, INV-014, INV-015, INV-016, INV-017, INV-018, INV-019, INV-020, INV-021, INV-022, INV-023, INV-025, INV-026, INV-028, INV-029, INV-030, INV-036, INV-043, INV-047, INV-048, INV-052, INV-054, INV-065, INV-084, INV-090, INV-098, INV-099, INV-100, INV-101, INV-106, INV-107, INV-108, INV-113, INV-117.

## 9. Watch points

Plan section 13 lists every watch point of the oscillation checks after iterations 12 to 32 with the decision it protects; v35 implements it as stated there. In particular: every tie of the "truth of a shown fact" class is a verbatim member of `factsShown`/`stated` in INV-123, at definitional level (two moved up, CHG-R1; none moved down); INV-112, INV-114, INV-115 and INV-116 are kept; fix 30's duration conjunct and fix 28's `∀ d ∈ l.duration • startOf(…) ≠ ∅` stay in INV-079; no declined tie was added; `E-046.comparison` stays `opt`; INV-027, INV-039, INV-069, INV-105 and INV-008 are byte-identical; the E-049 stated-start clause is verbatim, and E-049/D03 keeps "aligned to the event, not to the start"; INV-089 keeps `ongoing`, `lastDay`, `e ≤ ctx.asOf`, the remission bound in its `plusMonths` form (the constant in SD-FX-07, same name and value), `onlyOfType` and the rate relation; section 2.8, `notStoppedBefore`, `intervalOnTreatment` and `evaluatedOnTreatment` are unchanged; `fillsPeriod` and the INV-050 start ties are unchanged; the E-039 `reviewWindow` keeps no `when` clause; INV-087's lead-in conjunct is unchanged; the formulation ties are members of INV-123 and INV-074 is unchanged; the text-only entries (E-057 Notes, ISS-02, ISS-03, ISS-12) moved verbatim, with the planned CA-06 qualification of ISS-12 and the plan's drop of E-057 Notes' last sentence replaced by a move (D-11). The three fix-28 sentences that fix 29 corrected are not restored (C6).
