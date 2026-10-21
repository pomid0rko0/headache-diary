# Fix log — iteration 15
Input review: reviews/review-iter-15.md · Input version: v14 · Output version: v15
Date: 2026-10-21

## What was read and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039);
- v14 (`OUTPUT_MODEL.md`, byte-identical to `history/v14.md`, checked with `cmp`);
- review 15.

**Earlier loop files read, so that no fix is undone:**
- fix logs 13 and 14, with their "Noted, not changed" points on the formulation scope;
- fix log 11 (presence sweep: `formulations` of an all-formulations summary; "treatment effect" by one item);
- the oscillation check after iteration 12, with its seven watch points.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**Downloads.** None. All three remarks concern the formal model. I verified them against the Stage 1 v18 text in the repository and against v14. No source quote was added or changed. Every quoted fragment of the new text occurs verbatim in Stage 1 v18 (checked by script):
- OUT-023: "For each acute medication, [...] across the attacks treated with it", "per-drug outcomes", "be shown separately for each formulation of the same drug, so that a non-response to one formulation is not read as a non-response to the drug";
- OUT-024: "so that different formulations of the same drug can be told apart";
- OUT-039: "over the evaluation window, next to the response comparison of OUT-018, so that a reader can see whether an apparent lack of effect coincided with inconsistent intake", and [S-018] "If no efficacy is observed after 8–12 weeks of treatment".

**Scripts.** All are in the session scratchpad (`fix15/`) and were run with `python3 -I`:
- `mech.py`: headings, references, traceability, invariant levels and scopes, prohibition form, attribute declarations and the typing rule (run on v14 and v15);
- `names.py`: the `omn` lines changed from v14 to v15, the names they use and their attribute selections;
- `inst.py`: the review's examples and the satisfying constructions, evaluated under the v14 and the v15 conditions;
- `quotes.py`: the quoted fragments of the changed lines, against Stage 1 v18;
- `invlist.py`: the list of invariants with a presence requirement, for the identifying-property check.

There are also inline checks: bracket balance of each changed `omn` block, the scope-term sweep, the guarantee-term counts, and a byte comparison of the watch-point items.

### Verification of the remarks

**R15-01 holds.**
- **The defect.** In v14, the per-medication requirements tie only the summary's drug (`s.drug = m.drug`), never its formulation:
  - INV-062 (three acute branches);
  - INV-069;
  - INV-071, second conjunct;
  - INV-088;
  - INV-104;
  - INV-109.

  Only INV-071's first conjunct ties the formulation.
- **The review's examples** (`inst.py`). Both meet the v14 condition and fail the v15 condition:
  - one oral sumatriptan summary for a subject who has used oral and subcutaneous sumatriptan;
  - a subcutaneous summary for a subject who has used only the oral form.
- **The readings.** A summary of all formulations, or one summary per formulation used, meets both v14 and v15.
- **Fixes 13 and 14 do not stand in the way.** Their ground was that "a disjunction of the two would fit neither reading exactly". The condition needed here is not that disjunction of requirements. It is weaker than each reading, and each reading implies it, so it narrows neither.

**R15-02 holds.**
- **The defect.** INV-066 fixes only the end of the window and its lower bound (the treatment start).
- **The review's example** (topiramate, window 30 March – 30 March 2026, on-treatment period 3–30 March) meets v14 and fails v15 (`inst.py`).
- **What meets v15.** A window equal to the on-treatment period, or from the treatment start (3 February) to 30 March, meets both v14 and v15.
- **Stage 1.** OUT-039 asks for adherence "over the evaluation window, next to the response comparison of OUT-018, so that a reader can see whether an apparent lack of effect coincided with inconsistent intake". A one-day window cannot serve that purpose.

**R15-03 holds.**
- **The defect.** In v14 the response-comparison alternative of INV-105 is `v.content ∩ ResponseComparison ≠ ∅`, and the antecedent is history-wide. Yet the v14 INV-105 Notes give, for the acute alternative, the reason "so that the effect the patient follows is that of the period the overview shows, not of an earlier one".
- **The review's example** (`inst.py`). Topiramate stopped 31 December 2019; overview of 15 August – 20 October 2026:
  - `courseOverlaps` is false for topiramate;
  - it is true for erenumab (from 15 March 2026);
  - it is true for a course stopped on 16 August 2026, or started on 20 October 2026;
  - it is false for a course started on 21 October 2026.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R15-01 | fixed: the review's option (a), reading-neutral, with its INV-109 alternative "per formulation of the drug that the subject has used" and its optional INV-105 item | E-051 (Definition: new `summarisesMedication`; Meaning; Conformance; Notes); INV-062, INV-069, INV-071, INV-088, INV-104, INV-105, INV-109 (Predicates, Readings); Notes of INV-062, INV-088, INV-104, INV-105, INV-109; E-055 Conformance; rows OUT-020, OUT-021, OUT-023, OUT-024, OUT-031, OUT-034, OUT-035 | **New predicate** `summarisesMedication(s, m) ≙ s.drug = m.drug ∧ (s.formulationScope = allFormulations ∨ s.formulations = {m.formulation})`. It is the review's condition (a), named once instead of written out seven times.<br>**Where it is used:** in place of `s.drug = m.drug` / `s.drug = am.drug` in:<br>• INV-062 (`acuteTreatmentEffectiveness`, `periodValuesOf(acuteTreatmentSummaries)`, `typeValuesOf((acuteTreatmentSummaries, h))`);<br>• INV-069;<br>• INV-071, second conjunct;<br>• INV-088;<br>• INV-104.<br>**INV-109.** For an acute line: `∀ m ∈ ctx.subject.acuteMedications • m.drug = l.drug ⇒ ∃ s ∈ l.acuteResponse • s.typeScope = allTypes ∧ summarisesMedication(s, m) ∧ <the v14 course-span tie>`. I chose the review's third alternative, "per formulation of the drug that the subject has used". It is the one consistent with (a): the other invariants quantify over the subject's acute medications too. The second alternative (`l.formulations`) rests on a value that no invariant ties to the subject's medications. One summary of all formulations of the course span meets it for every formulation. The quantifier is never empty: INV-001 makes the drug of every acute treatment the drug of an acute medication, so the existence requirement of v14 is kept.<br>**INV-105 (optional item).** The acute alternative is `∃ s ∈ v.content ∩ AcuteTreatmentSummary; m ∈ ctx.subject.acuteMedications • s.typeScope = allTypes ∧ summarisesMedication(s, m) ∧ within(s.period, v.covers)`. Its drug is now also tied (see Other changes).<br>**Why it is reading-neutral.**<br>• Per drug: the per-drug reading of OUT-023 gives a summary of all formulations, which meets the condition for every formulation of the drug.<br>• Per drug and formulation: that reading gives a summary of each formulation used, which meets it as well.<br>• So the condition narrows neither reading. It excludes exactly the review's two examples: one formulation standing in for another, and a formulation never used.<br>**The reading question** is stated in the new E-051 Notes ("Formulation of a required summary"), not in section 8. It is not a Stage 1 defect: the OUT-023 Statement itself asks for "per-drug outcomes" and for their separate presentation "for each formulation of the same drug". The question arises from the model's representation of an acute medication as a drug and a formulation (E-008). INV-071's first conjunct already offers both presentations for the selected time range.<br>**Unchanged:**<br>• the R11-02 per-drug, per-period requirement (watch point 2), now with a stronger tie;<br>• the R13-01 type scopes;<br>• the R14-02 periods;<br>• INV-072, INV-073, INV-074;<br>• E-008;<br>• every E-041 value. |
| R15-02 | fixed: the review's option (a), reading-neutral, with its optional INV-104 and INV-109 items | E-047 (Definition: new `adherenceFor`; Meaning; Conformance; Notes); INV-066 (Predicate, Reading, Evidence, new Notes); INV-104 and INV-109 (Predicate, Reading, Notes); E-055 Conformance; rows OUT-024, OUT-034, OUT-039 | **New predicate** `adherenceFor(a, rc) ≙ a.treatment = rc.treatment ∧ rc.treatmentStart ≤ a.window.start ∧ ∃ p ∈ ran rc.onTreatment • a.window.start ≤ p.start ∧ a.window.end = p.end`. Compared with v14, the only new part is `a.window.start ≤ p.start`: the window contains the on-treatment period it ends with.<br>**Option (a) rather than (b).** (a) admits both:<br>• the evaluated period itself;<br>• the time on treatment up to its end, from the treatment start, as in [S-018] 14D "after 8–12 weeks of treatment".<br>Stage 1 does not decide between these. (b) would require the second only.<br>**Not added:** a window for every on-treatment period. OUT-039 names one evaluation window next to the comparison, so INV-066 still asks for one on-treatment period (E-047 Notes).<br>**Uses:**<br>• INV-066: `∃ a ∈ viewOf(rc).content ∩ AdherenceSummary • adherenceFor(a, rc)`;<br>• INV-104: the started treatment's comparison and an adherence summary over an evaluation window of it, both in the summary;<br>• INV-109: the line's adherence is over an evaluation window of the response comparison the line shows.<br>**Why INV-104 and INV-109 as well.** OUT-039 asks for "The adherence output", the one over the evaluation window, in the history and in the clinician-facing summary. In v14, a one-day adherence summary met the INV-104 conjunct and the line's `adherence`, even where INV-066 placed the right summary in the same view.<br>**Watch point 3.** The placement of the adherence next to the comparison (INV-066 `viewOf(rc)`) is unchanged. |
| R15-03 | fixed: the review's option (a) | E-067 (Definition: new `courseOverlaps`; Meaning; Notes); INV-105 (Predicate, Reading, Notes); row OUT-035 | **New predicate** `courseOverlaps(c, t, p) ≙ (∃ s ∈ startOf(c, t) • s ≤ p.end) ∧ ¬ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is stop ∧ e.date < p.start`. It reads: started on or before the last day of the period, and not stopped or paused before its first day. A stop on the first day counts as overlapping, as in the INV-109 course span (start to stop date, both included).<br>**INV-105 treatment-effect conjunct:** `(∃ t ∈ ctx.subject.preventiveTreatments • courseOverlaps(ctx, t, v.covers)) ∨ ctx.subject.acuteMedications ≠ ∅ ⇒ (∃ rc ∈ v.content ∩ ResponseComparison • courseOverlaps(ctx, rc.treatment, v.covers)) ∨ <acute alternative, R15-01>`.<br>**Antecedent.** It is restricted to overlapping courses, as the review asks, so the conjunct is required, and satisfiable, exactly where such a treatment exists. A subject whose preventive treatments all stopped before the covered period, and who has used no acute medication, is not asked for a treatment effect of that period. This follows the v14 reasoning already stated in the INV-105 Notes: "the effect the patient follows is that of the period the overview shows".<br>**Not adopted:** option (b), the most recently started treatment, which has no Stage 1 basis.<br>**The comparison's own periods** are not required to lie in the covered period (INV-105 Notes).<br>**Kept:** the fix-11 "one item" decision and the v14 period tie of the acute alternative. The menstruation conjunct (watch point 4) is byte-identical.<br>**Where `courseOverlaps` is declared.** In E-067, not in E-008, so that no E-008 item (watch point 6) changes. |

## Identifying-property check

**Scope.** Every invariant whose predicate requires an item to be present or shown (`∃ …`, `shownDay`, `perPeriod`, `reportedPerPeriod`, `reportedTogether`, `annotated`, `≠ ∅`, `∈ v.content`) was listed by `invlist.py`. That gives 81 invariants: 63 with a level, all in the table below, and 18 definitional ones (after the table).

**Method.** For each one, I listed the properties that identify what the required item is about. Abbreviations:
- **T** headache-type scope;
- **P** period or window;
- **Tr** treatment or course;
- **D** drug or class;
- **F** formulation;
- **I** instrument;
- **A** subject age period;
- **V** view;
- **K** kind or measure.

I then checked that the predicate fixes each property that the Stage 1 statement part fixes for that item.

**"Not fixed by Stage 1"** names a property that the predicate leaves free because Stage 1 leaves it free. Such a property is not a gap.

| Invariant | Required item | Properties checked | Gap (y/n) | Change |
|---|---|---|---|---|
| INV-003 (MUST) | covered period; periods referred to; periods with the dates of referenced values | P (`sameSpan`), V | n | — |
| INV-008 (SHOULD) | definition label of each reported measure | K, V; the definition is fixed where Stage 1 names it (INV-009, INV-010) | n | — |
| INV-011 (SHOULD) | completeness indicator | P (value's period, `sameSpan`, adherence window, covered period), T (INV-012), V | n | — |
| INV-014, INV-015, INV-016, INV-017, INV-108 | headache, migraine, moderate/severe days, attacks per period | K, P (series tiling the selected time range at a monthly granularity), T (`allTypes`), V | n | — |
| INV-018, INV-019, INV-022 | intensity (with scale), duration, symptom presence, most bothersome symptom per period | K (symptom; non-aura duration), P, T, scale | n | — |
| INV-023 | acute-medication days in total, per class and per drug | K, D (each medication's class and drug), P, T, V (together) | n | — |
| INV-025 | weekly total acute-medication days | P (weeks tiling the time range), T, V | n | — |
| INV-026 | functional-impact days per domain and severe impairment | K (domain, severity), P, T, V | n | — |
| INV-027 | functional-impact days next to the comparison | Tr (`rc.treatment = t`), P (the comparison's periods), K, T, V | n | — |
| INV-028, INV-029 | values per headache type and combined | T (each type and all types), K, D, P, V | n | — |
| INV-034, INV-035 | time-course view; its values and markers | P (`tiles`, covers = series), K, T; markers: Tr, event, date, V | n | — |
| INV-037, INV-039 | comparison of selected periods | P (`matchesSelection`), K, T, scale (INV-039), A (equal lengths for children, INV-039) | n | — |
| INV-040, INV-042 | three-month view; labels and codes | P (most recent, INV-041), K, T; label measure; codes | n | — |
| INV-044 | overuse indicators | P (each period of the series), scope (each class used; combined use), V; span and basis by INV-045 | n | — |
| INV-020, INV-047, INV-052, INV-090, INV-098, INV-099, INV-100 | annotations | kind, qualified element, V (INV-007), A (INV-098 `childIn`, `childOn`) | n | — |
| INV-049, INV-050 | follow-up view and its content | start of withdrawal, P (covered period, series, review window by INV-051), K, T | n | — |
| INV-054 (MUST) | the two values of a change of a comparison | the change's own `reference` and `compared`, V | n | — |
| INV-055 (MUST) | comparison per started treatment; at each time point | Tr, rule, anchor, P (`atTimePoint`, equal lengths) | n | — |
| INV-056, INV-057 (MUST) | values and changes of a comparison | K, P (baseline, on-treatment), T | n | — |
| INV-059 (MUST) | time points | Tr (`tp.treatment = rc.treatment`), rule, anchor, V | n | — |
| INV-060 | residual burden | the change (`rb.change = ch`), K, T and P by INV-061, V | n | — |
| INV-062 | the label's comparison, residual burden and other values | **Comparison:** Tr, P (evaluated periods among its on-treatment periods).<br>**Instrument results:** I, and the result at the evaluation where one is available.<br>**Acute summaries:** P, T, D, **F**.<br>**Per-period values:** K, P, T.<br>**Changes:** K, T, P.<br>**Score pair:** I, dates.<br>**Control-level counts:** P.<br>**V** for all. | **y** (F) | `summarisesMedication` in the three acute branches (R15-01) |
| INV-066 | adherence next to the comparison | Tr, **P (window)**; *not fixed by Stage 1:* which on-treatment period (one window) | **y** (window) | `adherenceFor` (R15-02) |
| INV-068 (MUST) | headache, migraine and acute-medication days of the review periods | Tr, P (baseline before, on-treatment after the start), K, D, T | n | — |
| INV-069 | further dimensions of the review view | **Values:** P, T, K.<br>**Acute summaries:** D, **F**.<br>**Instrument:** I, the latest up to the end of the last on-treatment period. | **y** (F) | `summarisesMedication` (R15-01) |
| INV-070 | post-stop values | Tr, event, P (on-treatment before the event, periods from the event), K, T; *not fixed by Stage 1:* the position of the original baseline (settled in review 02) | n | — |
| INV-071 | per-drug acute summaries | **Conjunct 1:** D, F, P (time range), T.<br>**Conjunct 2:** Tr, P (the comparison's periods), T, D, **F**, V. | **y** (F, conjunct 2) | `summarisesMedication` (R15-01) |
| INV-072 | outcome summaries, attack lines, formulations | measure (time point), lines (count; drug, period and single formulation by INV-074), V | n | — |
| INV-076 | symptom status on each attack line | each symptom | n | — |
| INV-077, INV-078 | history, groups, lines | Tr (each treatment), role, class, V | n | — |
| INV-081 | instrument results | I, completion date, baseline (an earlier result of the same instrument, INV-082; settled) | n | — |
| INV-083 | screening results next to headache outputs | I, date, scores and subscales, V; *not fixed by Stage 1:* the period of the headache outputs | n | — |
| INV-086 (MUST) | menstrual-relation view | P (time range) | n | — |
| INV-088 | cluster view, rates, acute summaries | **View:** P (time range).<br>**Rates:** bout, basis, T (`scopeFor`); the period within the bout is settled (INV-089).<br>**Acute summaries:** D, **F**, P, T, time point, rescue outcome. | **y** (F) | `summarisesMedication` (R15-01) |
| INV-092, INV-093 | components of an index; headache days with AUC | P, T, dimension, V | n | — |
| INV-094, INV-095 | clinician summary; overview | audience, P (time range, chosen period, since the previous consultation) | n | — |
| INV-096 | PedMIDAS; school days; caregiver impact | I, date, recall, A (`childOn`), P, T | n | — |
| INV-102 (MUST), INV-103 | review view; post-stop view | Tr, event, date; P by INV-068 and INV-070 | n | — |
| INV-104 | clinician summary components | **Values:** P (covered period and series), K, T, D.<br>**Markers:** Tr, event, date.<br>**Comparison:** Tr; *not fixed by Stage 1:* its periods (INV-059 shows the time points with it).<br>**Adherence:** Tr, **P (window)**.<br>**Acute summaries:** D, **F**, P, T.<br>**Lines:** Tr.<br>**Instrument results:** I, a date within the covered period.<br>**Functional impact:** K, T. | **y** (window, F) | `adherenceFor` (R15-02, optional item); `summarisesMedication` (R15-01) |
| INV-105 | overview components | **Values:** P (covered period and series), K, T.<br>**Treatment effect — comparison:** **Tr (a course taken during the covered period)**.<br>**Treatment effect — acute summary:** P (`within`), T, **D**, **F**.<br>**Cycle line:** overlaps the covered period. | **y** (Tr; D, F) | `courseOverlaps` (R15-03); `∃ m ∈ ctx.subject.acuteMedications • summarisesMedication(s, m)` (R15-01 optional item; the drug tie is new, see Other changes) |
| INV-109 | a line's dose changes, response summary, adherence | **Dose changes:** every course event.<br>**Preventive response:** Tr (INV-079).<br>**Acute response:** D (INV-079), T, P (course span), **F**.<br>**Adherence:** Tr (INV-079), **P (window)**. | **y** (F, window) | `summarisesMedication` per acute medication of the line's drug (R15-01); `adherenceFor` (R15-02, optional item) |

**Definitional invariants with an existence clause.** These are relations within an element, not requirements to show an item about something:
- INV-001: the tiling sequence of the context;
- INV-031: the mark of a period with 0 migraine days, of the same period and scope;
- INV-041: the series in its view;
- INV-087: each attack mark in exactly one cycle line of its view;
- INV-089: one number of attacks per period and scope.

I also looked at INV-006, INV-007, INV-024, INV-030, INV-033, INV-046, INV-053, INV-063, INV-064, INV-074, INV-079, INV-080 and INV-082. None leaves the identity of a required item free.

**Attribute presence requirements whose value is a referenced item** (section 3.3, item 2). The properties of each are fixed by the invariant named. No further gap:
- E-035 `markers` (INV-035, INV-036);
- E-039 `series` and `reviewWindow` (INV-050, INV-051);
- E-042 `latest` (INV-058);
- E-046 `comparison`, `residual` and `otherValues` (INV-062);
- E-049 `baseline`, `onTreatmentPeriod` and `after` (INV-070);
- E-051 `outcomes` and `sequence` (INV-072, INV-074);
- E-054 groups (INV-078);
- E-055 `preventiveResponse` (Tr, INV-079); `acuteResponse` (D, INV-079; T, P and F, INV-109); `adherence` (Tr, INV-079; window, INV-109, now);
- E-058 `baselineResult` (INV-082);
- E-062 references (INV-088, INV-089).

**Outside this class.** Values of attributes that are not references (dates, scores, the formulation a line shows) are shown values, not required items, and the check does not cover them. None was changed.

**Result.** The gaps are exactly:
- the formulation of the per-medication acute summaries (INV-062 ×3, INV-069, INV-071, INV-088, INV-104, INV-109);
- the adherence window (INV-066, INV-104, INV-109);
- the treatment of the overview's comparison (INV-105);
- the drug and formulation of the overview's acute summary (INV-105).

All are fixed by the three predicates above. No other presence requirement leaves free a property that Stage 1 fixes.

## Other changes

**1. INV-105, the drug of the acute treatment-effect summary (found by the identifying-property check).**
- **The defect.** In v14 the acute alternative fixed neither the drug nor the formulation. A summary of a drug the subject has never used, with 0 treated attacks, met it.
- **Compared with the review.** The review's optional item for INV-105 asked only for "all formulations, or a formulation of its drug that the subject has used". Read literally, that still leaves the drug of an all-formulations summary free.
- **The fix.** The fixed predicate quantifies over the subject's medications (`∃ m ∈ ctx.subject.acuteMedications • summarisesMedication(s, m)`), which ties the drug too.
- **Basis.** OUT-035: "so that patients can follow the effect of their treatment".
- **Satisfiability.** The acute alternative is needed only where the antecedent holds through `acuteMedications ≠ ∅`, and then such an m exists.

**2. Wording.** Paraphrases aligned with the new formal text:
- E-055 Conformance (formulation of the course summaries; adherence window);
- E-047 Conformance;
- the Readings and Notes listed in the table.

No other text changed.

**No other change.**
- No element or invariant was added, withdrawn or renumbered, and no level changed.
- No E-041 value changed.
- The following are byte-identical to v14 (checked by script): E-008, E-039, E-041, E-043, E-045, E-046, E-060, E-061, E-062, INV-001, INV-003, INV-049, INV-050, INV-054, INV-055, INV-056, INV-059, INV-063, INV-064, INV-067, INV-072, INV-073, INV-074, INV-078, INV-079, INV-086, INV-087 and INV-097.

### Satisfiability pass

Every changed invariant was checked together with the invariants that constrain the same elements and views. No admissible context (INV-001) makes the MUST and SHOULD constraints jointly unsatisfiable. No derived attribute was added or changed, and none is required where its relation is undefined. The three new names are defined predicates over core or MUST attributes and guarded set terms:
- `a.window` is core;
- `rc.treatmentStart` is MUST;
- `s.formulationScope` is core;
- `s.formulations` is a set;
- `startOf` is a set.

**`summarisesMedication`** (INV-062, INV-069, INV-071, INV-088, INV-104, INV-105, INV-109), with INV-003, INV-011, INV-071 (first conjunct), INV-072, INV-073, INV-074, INV-076 and INV-079:
- **One summary always suffices.** A summary of all formulations of a drug, of the required period and scope, meets it for every acute medication of that drug. INV-072 asks it to name every formulation of the drug that the subject has used, which it can do. INV-074 constrains only single-formulation summaries. INV-073 fixes the time point by the type scope only. The summary may have 0 treated attacks.
- **INV-088.** `scopeFor` implies `onlyOfType`, so INV-073 gives 15 minutes, and the rescue outcome is among `requiredOutcomes` (INV-072).
- **INV-109.** INV-079 gives `s.drug = l.drug`. The span of the course is a period of kind `otherSpan` (INV-002), as in v14.
- **INV-071.** The first conjunct still asks for both presentations for the selected time range. It is unaffected.

**`adherenceFor`** (INV-066, INV-104, INV-109), with INV-002, INV-003, INV-011, INV-056, INV-067 and INV-079:
- **The window.** An on-treatment period p begins on or after the treatment start (INV-056). So a window equal to p, or from the start to p's end, meets `adherenceFor` and INV-067. INV-003 shows the window in the view, and INV-011 adds its completeness.
- **INV-104.** It places the comparison in the summary. INV-066 then asks, in the same view, for an adherence summary that meets `adherenceFor`, and the same item meets INV-104.
- **INV-109.** It places the line's comparison r in the line's view. The INV-066 summary of r is in that view, and the line can reference it. INV-079 holds: the summary's treatment is the line's treatment.

**`courseOverlaps`** (INV-105), with INV-003, INV-011, INV-054 to INV-057, INV-059, INV-060, INV-066, INV-097, INV-098 and INV-095:
- **A preventive course overlaps.** The course has a start (`courseOverlaps`). A comparison of it is admissible (INV-056: a 28-day baseline before the start and 28-day on-treatment periods from it; INV-055 already requires one for every started treatment). It can be shown in the overview with its values, changes, time points, adherence, residual burden, completeness and, for children, equal lengths and the supportive-information caveat. A view may show periods outside its covered period (INV-003, INV-098 Notes).
- **No preventive course overlaps.** The antecedent holds only if `acuteMedications ≠ ∅`. A summary of all formulations of such a medication's drug, of the covered period, meets the acute alternative.
- **Neither holds.** Nothing is required.
- **The other conjuncts of INV-105** (values, series, menstruation) are unchanged.

**Levels.** Unchanged:
- INV-062, INV-066, INV-069, INV-071, INV-088, INV-104, INV-105 and INV-109 stay SHOULD, the strength of OUT-020, OUT-039, OUT-021, OUT-023, OUT-031, OUT-034, OUT-035 and OUT-024.

Each change narrows what meets a requirement, within the Stage 1 statement part the invariant realises.

### Watch points (oscillation/check-after-iter-12.md)

1. **E-041.** Byte-identical. No `excludes`, `timing`, `ages` or `AgeCoverage` value touched.
2. **Responder labels.**
   - INV-062 changed only in its three acute branches. `s.drug = am.drug` became `summarisesMedication(s, am)`, which implies it.
   - The R11-02 per-drug, per-period requirement is kept and tied more closely.
   - E-045, E-046 and INV-063 are byte-identical.
   - The guarantee-term counts are equal (Checks).
   - No condition is read on the subject.
3. **Co-presence.**
   - INV-003, INV-054, INV-056 and INV-078 are byte-identical.
   - INV-066 still places the adherence in `viewOf(rc)`.
   - No placement was removed.
4. **Menstrual-relation view and overview.**
   - INV-086, INV-087, E-060 and E-061 are byte-identical.
   - The INV-105 menstruation conjunct is byte-identical. Only the treatment-effect conjunct changed.
5. **Withdrawal follow-up.** INV-049, INV-050 and E-039 are byte-identical.
6. **E-008 (v12 subject properties).** Byte-identical. `courseOverlaps` uses `startOf` and `courseEvents` as they are and is declared in E-067.
7. **Change volume.** No sweep beyond the identifying-property check. This version changes:
   - 4 elements (E-047, E-051, E-055, E-067);
   - 8 invariants (INV-062, INV-066, INV-069, INV-071, INV-088, INV-104, INV-105, INV-109);
   - 8 traceability rows (OUT-020, OUT-021, OUT-023, OUT-024, OUT-031, OUT-034, OUT-035, OUT-039);
   - the header and sections 9, 11 and 12.

   That is **12 model items** (20 counting the rows). Every change adds an identity tie; none removes a condition. INV-104's earlier conditions (`s.period = v.covers`, `s.typeScope = allTypes`, the series, markers and functional-impact ties) are unchanged.

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-11; ISS-07 appears only as withdrawn (section 9). |
| References | No dangling E- or INV- reference; ISS-07 is referenced only as withdrawn. S references lie in S-001–S-046 and S-101–S-106, and every S-1NN has a row in section 10. Every OUT reference exists in Stage 1. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". Exactly one Realises and one Conformance field in every element and invariant. Each row's E and INV columns equal the union of the Realises fields; no Realises field changed. |
| Types and names | The three new predicates are each declared once, in E-047, E-051 and E-067. Uses (`names.py`, counting the declaration and its comment line): `adherenceFor` 5, `summarisesMedication` 11, `courseOverlaps` 4.<br>Every attribute selection in the 28 changed `omn` lines names a declared attribute. Every identifier in them is declared or bound. Every changed block has balanced brackets.<br>Argument types:<br>• `m` and `am` range over `AcuteMedication`;<br>• `s` over `AcuteTreatmentSummary` (`v.acute` and `l.acuteResponse` are sets of references to it);<br>• `a` over `AdherenceSummary`;<br>• `rc` and `r` over `ResponseComparison`;<br>• `v.covers` is a `Period`.<br>Precedence:<br>• INV-109: `l.role = acute ⇒ ∀ m • (m.drug = l.drug ⇒ ∃ s • …)`;<br>• INV-104: `startOf(ctx, t) ≠ ∅ ⇒ ∃ rc • (rc.treatment = t ∧ ∃ a • adherenceFor(a, rc))`;<br>• INV-105: `A ∨ B ⇒ C ∨ ∃ s, m • …`.<br>No new partial term. |
| Typing rule for levels | Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33; total 110, unchanged. Scopes: output 77, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Guarantee terms (v14 → v15) | All equal:<br>• `#L.evaluated = 1` 7;<br>• `rc.treatment = L.treatment` 13;<br>• `evaluationResult(L` 7;<br>• `pretreatmentBaseline(L` 6;<br>• `otherValueNamed` 6;<br>• `ch.reference.typeScope = allTypes` 7;<br>• `attackScope(` 5;<br>• `conditionHolds(` 10;<br>• `scopeFor(` 8;<br>• "has a headache type" 9;<br>• `fillsPeriod` 15;<br>• `containsPeriodOf` 12;<br>• `dayOneShown` 9;<br>• `ruleRuChildren` 6;<br>• `s.typeScope = allTypes` 9;<br>• `within(s.period, v.covers)` 1;<br>• `s.period = v.covers` 2;<br>• `menstruatesDuring` 9;<br>• `otherCompletenessExpression` 3;<br>• "a later time point of its own" 4;<br>• "after its latest date" 2;<br>• `withinWindow` 9. |
| Instance check (`inst.py`) | **R15-01.** Under v15, both review examples fail, and the two reading-conforming constructions (one all-formulations summary; one summary per formulation used) hold. Under v14, all four hold.<br>**R15-02.** Under v15, the one-day window fails, and the evaluated period and the span from the start to its end hold. Under v14, all three hold.<br>**R15-03.** `courseOverlaps` gives the expected values on five courses. |
| Quotes | No new source quote. Every quoted fragment on a changed line occurs verbatim in Stage 1 v18 (`quotes.py` and a direct check of the ten fragments), or is unchanged v14 text on a changed line. |
| Scope sweep | The whole document was searched for: enter, entry, record, input, captur, logged, store/storage, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field, questionnaire, data-entry, "derived from" and "diary information".<br>Every count equals v14. The only hit on a changed line is the unchanged "diary information" sentence of the INV-105 Notes (the lead-in). "Intake" occurs only in the OUT-039 wording ("inconsistent intake") and the existing E-047 wording.<br>The new relations take only output elements and context properties as arguments: summaries, medications, response comparisons, adherence windows, course events and covered periods. No input entity, no storage term, and no relation with an input argument. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v15.md`: identical. `history/v14.md` is unchanged. |
