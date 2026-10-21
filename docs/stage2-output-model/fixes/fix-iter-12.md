# Fix log — iteration 12
Input review: reviews/review-iter-12.md · Input version: v11 · Output version: v12
Date: 2026-10-21

## What was downloaded and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3;
- v11 (`OUTPUT_MODEL.md`, byte-identical to `history/v11.md`);
- review 12.

**Earlier loop files read, so that no fix is undone:**
- fix log 11 (all sweeps; the satisfiability item on acute lines that R12-01 cites);
- the "Checked and not raised" lists of reviews 01, 02 (labels under a criterion that does not apply), 04 (R04-01, the lead-in) and 11;
- the oscillation check after iteration 08 and its eight watch points.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**Downloads.** All with `curl` into a fresh directory in the session scratchpad (`fix12dl/`), outside the repository. They re-check the wording on which the new reading of the responder-criterion conditions rests (Other changes, 1).
- [S-015] NICE CG150 Recommendations page (Stage 1 URL), HTTP 200; text extracted with the markup removed:
  - 1.3.24 "For CGRP inhibitors recommended as options for preventing episodic or chronic migraine in adults";
  - 1.3.26 "Intramuscular injection of botulinum toxin type A is recommended as an option for preventing chronic migraine in adults";
  - 1.3.28 "at least 50% in episodic migraine" and "at least 30% in chronic migraine".

  All read as quoted.
- [S-008] IHS 2024 (univaq PDF, Stage 1 URL), HTTP 200; `pdftotext -layout`. The Q6 sentence ending "is acceptable for treatment continuation beyond three months" reads as quoted in E-045.

**Quote fragments.** No quote was added or changed. Every quoted fragment of the new text was checked by script (22 fragments). Each occurs verbatim either in Stage 1 v18 or in a model quote that review 12 verified:
- OUT-001 to OUT-003, OUT-008, OUT-010, OUT-017, OUT-030 to OUT-032, OUT-036 and OUT-039 Statements, Rationales and Caveats;
- [S-014] "The relapse rate is high within the first year";
- [S-023] "Bei der episodischen Migräne (eM)";
- [S-015] 1.3.24 and the CG150 population;
- [S-008] Q6.

**Scripts.** All are in the session scratchpad (`fix12/`) and were run with `python3 -I`:
- `mech.py`: headings, references, traceability, levels and the typing rule;
- `names.py`: declared names and attribute selections in the `omn` blocks;
- `applic.py`: `applicable` (E-041) under the v11 and the v12 definitions, on the six scenarios of the oscillation check and two age-boundary scenarios.

There are also inline checks for the scope words, the quote fragments and the item diff against v11.

### Verification of the remarks

**R12-01 holds.**
- **The defect.** E-008 declared `acuteMedications` "the acute medications (drug and formulation) the subject uses", with no time frame. The fix-11 log (section 4, the INV-109 item) reads it as the current medications.
- **The review's examples, checked under that reading:**
  - INV-023 and INV-024 for January admit only a total ≤ 6, while the correct total is 12. The class-to-drug conjunct fails in the same way for a switch from rizatriptan to sumatriptan.
  - INV-044 requires no triptan indicator. So `classUseExcluded(i, triptans)` holds, and INV-046 forces the April 8.2.6 indication to "not reached", although criterion B of 8.2.6 is met: 12 combined days in each of four months, with no class at its own level.
  - INV-071 and INV-062 require no per-drug summary for rizatriptan.
- **The time frame is the cause.** Under "used up to the as-of date" all three hold correctly: 12 ≤ 6 + 6; the triptan indicator shows 6 days, and the combined indicator is "reached" by the sufficient antecedent of INV-046; and the rizatriptan summaries are required.
- **The same defect elsewhere.** The class of defect, a context component without a time frame, is also present in other components (Other changes, 1).

**R12-02 holds.**
- **INV-008.** It fires only on a `PeriodValue` for which `isMeasure` holds.
- **INV-011.** It fires only on the period of a `PeriodValue`.
- **The review's output.** A menstrual-relation view of 1 July – 30 September with three cycle lines, 5 migraine days and 4 attack marks satisfies INV-086, INV-087, INV-008 and INV-011, with no label and no indicator.
- **Further cases.** The same holds for:
  - the trigger co-occurrence view;
  - a cluster view with rates and no attack count (no attack label);
  - a peak-intensity distribution without a headache-day count (no label).

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R12-01 | fixed: the review's option (a), with its optional INV-001 link, in both directions | E-008 (comment of `acuteMedications`, Meaning, Realises +OUT-014, +OUT-016, +OUT-021, Notes); INV-001 (Predicate, Reading, Notes); E-029 (Conformance, Notes); E-032 (comment of `classUseExcluded`, Conformance, Notes); E-045 (Meaning); E-046, E-048, E-051 and E-062 (Conformance); Readings of INV-023, INV-024, INV-044, INV-046, INV-062, INV-071 and INV-072; Notes of INV-062 and INV-072; rows OUT-014, OUT-016, OUT-020, OUT-021 and OUT-023 | **Definition.** `acuteMedications` is now every acute medication, drug and formulation, that the subject has used at any time up to the as-of date. A medication stays in the set after its use has stopped (E-008 comment and Meaning). The Meaning states the consequence: for a period in which a medication was not taken, the required values are 0 days, a summary of 0 treated attacks or an indication that is not reached. These are correct values.<br>**No predicate of the dependent invariants changed:** INV-023, INV-024, INV-028, INV-044, INV-046 / `classUseExcluded`, INV-062, INV-068, INV-069, INV-071, INV-072, INV-088 and INV-104. Under the stated time frame they give the correct outputs in the review's examples (Verification).<br>**INV-001.** It now ties the acute treatment courses and the acute medications:<br>• the drug of every acute treatment course is the drug of an acute medication (the review's optional link);<br>• the drug of every acute medication is the drug of an acute treatment course (the converse).<br>Both follow from the definitions, since a course is a course of a medication that the subject has used. Together they keep the acute-medication outputs (OUT-014, OUT-016, OUT-023) and the acute lines of the history (OUT-024) about the same drugs. They remove only contexts that describe no possible subject, so no required output is lost. The fix-11 remark on "an acute line whose drug is no longer among `acuteMedications`" no longer applies.<br>**Wording.** "Uses" became "has used (up to the as-of date)" wherever a paraphrase reads the set, and the Readings that the review names state the time frame.<br>**Traceability.** E-008 now realises OUT-014, OUT-016 and OUT-021, which its Meaning cites for `acuteMedications`.<br>**Oscillation.** None of these items is a watch point. The E-041 and responder-label watch points are untouched by this remark. |
| R12-02 | fixed: the review's options (a) and (b), extended by the trigger sweep (Other changes, 2) | E-011 (new `referencedValues` and `reports`; Meaning, Conformance, Notes); INV-008 (Predicate, Reading, Evidence, new Notes); INV-011 (Predicate, Reading, Evidence, new Notes); Conformance of E-013, E-022, E-023, E-033, E-040, E-044, E-047, E-060, E-062, E-064 and E-065; Notes of E-013, E-018, E-040 and E-045; rows OUT-002, OUT-003, OUT-030, OUT-031, OUT-032 and OUT-039 | **(a) OUT-002.** INV-008 now reads `reports(v, lm) ⇒ ∃ l ∈ v.content ∩ DefinitionLabel • l.measure = lm`. `reports` covers every form in which the model shows the days or attacks of the four measures:<br>• a per-period value of the measure (`isMeasure`), shown in the view or referred to by a change, a residual burden or a composite index shown in it (`referencedValues`);<br>• for headache days, a peak-intensity distribution (OUT-010 "the distribution of headache days by peak intensity category");<br>• for migraine days, the mark of a period without migraine days (OUT-008 "periods without migraine days");<br>• for migraine days and attacks, a cycle line (OUT-030), which shows both; cycle lines are triggered whether or not the view shows an attack, because a view without attacks still reports their absence;<br>• for attacks, a cluster attack rate (OUT-031) or a trigger co-occurrence view (OUT-032).<br>INV-009 and INV-010 constrain the labels as before.<br>**(b) OUT-003.** INV-011 adds three conjuncts:<br>• a completeness indicator for a period with the dates of each value that a change, a residual burden or a composite index refers to;<br>• one for the window of every adherence summary shown (OUT-039, "patient-reported adherence [...] over the evaluation window");<br>• one for the covered period of a view that shows cycle lines, cluster or remission periods, or is a trigger co-occurrence view.<br>Following the review, the treatment history view is not required to have one: it lists treatments with dates, and its response summaries bring their own periods and indicators.<br>**Text.** The E-045 Notes now say "with the period of every summary measure". The OUT-002 and OUT-003 rows state the forms.<br>**Not extended.**<br>• The single count of the IHS position statement 2025 (E-018). It is none of the four OUT-002 measures. It has one definition, stated by E-018, and wherever the model requires it, the control-level label names that criterion (INV-062). Reasons in the E-018 and E-011 Notes.<br>• The attacks with an associated symptom (E-025), the treated attacks and outcomes of acute summaries (E-050 to E-053), and headache-free and symptom-free days. These are other measures, which count a part, or the complement, of these days or attacks (E-011 Notes).<br>**Watch point 7.** E-060 changed in its Conformance text only. E-061 and INV-087 are unchanged. The label and the indicator are items of the view. |

## Other changes

### 1. Time-frame sweep (R12-01 class): every context component

**Method.** I took every component of `OutputContext` (E-007) and `SubjectProfile` (E-008), and the subject-derived predicates (`hasType`, `mayHaveType`, `concerns`, `onlyOfType`, `scopeFor`, `conditionHolds`, `ageCovered`, `inPopulation`, `valueAvailable`, `stopped`). For each I stated a time frame and read every invariant that uses it for a past period: a medication, treatment, headache type, age group, menstrual status, withdrawal or instrument that applied in that period but not on the as-of date.

**Result.** Five components had a time frame that was wrong for some use, and all five are fixed:
- the menstrual status;
- the age group;
- the start of withdrawal;
- the IHS Q6 situation;
- the episodic and chronic conditions.

The other components now state a time frame under which every use is correct. Section 3.5 states the three time frames, and E-007 and E-008 state each component's own. The table below gives the details.

| Component | Time frame (v11 → v12) | Uses | Result |
|---|---|---|---|
| `audience`, `weeklyGranularityRelevant` (E-007) | unstated → a property of the output, as of the as-of date | INV-094, INV-095; INV-034, INV-001 | stated. INV-001 forces the flag for a subject who has had tension-type or cluster headache, which only adds weekly outputs. |
| `asOf`, `timeRange`, `granularity`, `comparedSpans`, `chosenPeriod`, `schemeSelection` | dated spans, already bounded by the as-of date (INV-001) | INV-014 family, INV-037, INV-039, INV-094, E-056 | ok |
| `previousConsultation` | "previous" → the most recent consultation on or before the as-of date | INV-094 | stated. An earlier inter-consultation period is a chosen period. |
| `headacheTypes`, `possibleHeadacheTypes` | "has" / "has or may have" → the subject's history up to the as-of date ("has or has had", "may have or may have had") | migraine content (INV-015, INV-022, INV-035, INV-068, INV-076, INV-104), INV-088, E-027, INV-001 (weekly flag, `preventiveFor` ⊆ possible types), INV-028, INV-029, INV-042, `concerns` / `onlyOfType` / `scopeFor` (INV-062, INV-073, INV-089, INV-091 to INV-093) | **stated (E-008, E-009 Meaning, E-012 Notes, INV-001).**<br>An "as of" reading is wrong for past periods in two ways:<br>• a stopped preventive treatment of a type the subject no longer has makes the context inadmissible (INV-001: `p.2 ∈ possibleHeadacheTypes`);<br>• the OUT-029 per-type outputs (MUST) are dropped for past periods with two types.<br>Under the history reading, content for a type that occurred in a past period is still required, with 0 where it did not occur. The scope predicates are conservative: a value over all types is of one type only if every type of the history falls under it.<br>The episodic and chronic conditions are wrong under both readings; see the conditions row. |
| `menstruates : 𝔹` | unstated → **wrong under both readings**. "As of the as-of date" drops the MUST view of OUT-030 for a time range during which the subject menstruated (pregnancy, or menopause since). "At any time" requires it for a time range wholly after menopause. | INV-086 (MUST), INV-105 | **fixed.**<br>• `menstruationSpans : set DateSpan` (the spans up to the as-of date during which the subject menstruates) and `menstruatesDuring(c, r)` (E-008).<br>• INV-086 applies to a time range that overlaps such a span; INV-105 to an overview whose covered period does.<br>• INV-001 bounds the spans.<br>• The R04-01 lead-in is kept for every period that begins before the first day 1 the output shows: the menarche example of R04-01 still requires the view, with a lead-in.<br>• A week wholly before menarche no longer requires an overview cycle line, an option that R04-01 itself named ("or condition that requirement").<br>• Text: E-060 Conformance, E-067 Notes, INV-086 (new Notes), INV-105 Reading and Notes, rows OUT-030 and OUT-035. |
| `ageGroup`, `aged12OrOlder` | unstated (read as of the as-of date) → **wrong for E-041, for INV-096 to INV-098 and for INV-039**.<br>`applic.py`, scenario G: a treatment started at 17, subject adult on the as-of date. v11 required the AAN 14A, SIGN (titrated) and Russian 7.1 time points, and excluded the Russian paediatric one (INV-058 definitional, INV-059 MUST), attributing adult guidance to an adolescent's treatment.<br>Scenario H: NICE 1.3.27 applied to a treatment started at 11.<br>A now-adult lost the paediatric outputs of the periods of its childhood. | E-041 (INV-055, INV-058, INV-059), INV-039, INV-096, INV-097, INV-098, INV-001 | **fixed.**<br>• The dates `adultFrom` and `aged12From`, with `childOn` and `childIn` (E-008); enum `AgeGroup` removed.<br>• `ageCovered(c, a, d)` and `inPopulation` judge the population on the start of the treatment (E-041). A treatment without a stated start is in no population; it has no response comparison either (INV-056), so no required output is lost.<br>• INV-039, INV-097 and INV-098 read the age on the compared or covered periods. INV-096 reads it on the result dates and the periods of the series.<br>• INV-001 states `aged12From ≤ adultFrom`, which keeps "every adult is aged 12 or older".<br>• Text: E-030, E-031, E-037, E-040, E-048, E-049 and E-058 Conformance; E-041 Meaning and Notes (**Age on the treatment start**); E-043 Notes; INV-055 Reading, Evidence and Notes; INV-058 and INV-059 Readings; ISS-10; rows OUT-018 and OUT-036. |
| `preventiveTreatments`, `acuteTreatments`, `courseEvents` | unstated → every course up to the as-of date, ongoing or stopped; the course events are dated | INV-027, INV-035, INV-055, INV-071, INV-077, INV-079, INV-102 to INV-104, INV-109, `stopped` | stated. Every use quantifies over all courses, past ones included, or over dated events. |
| `preventiveTypes`, `preventiveFor` | per course | E-041, `conditionHolds` (new) | stated. |
| `acuteMedications` | R12-01 | see R12-01 | fixed (R12-01), with the INV-001 link. |
| `withdrawalStart : opt Date` | "for a subject who is withdrawing", one date → **wrong**: with relapse common (OUT-017, [S-014]), an earlier withdrawal's follow-up year is a past period that OUT-017 covers, but only one start could be stated. | INV-049, INV-050, E-039 | **fixed**: `set Date`, every start up to the as-of date. INV-001, INV-049 and INV-050 use membership and are unchanged. Text: E-039 Conformance and Notes, INV-049 Reading, row OUT-017. |
| `ihsQ6ChronicAlternative : 𝔹` | a subject-level flag → **wrong**. Once true it decided by the 30 % alternative the label of every treatment of the subject, including an earlier one started before multiple options had failed. INV-063 is definitional, so "responder" was forced. | `conditionHolds` (E-045), E-046, INV-062, INV-063 | **fixed**: `set Treatment`, the treatments to which the IHS Q6 situation applies ("acceptable for treatment continuation beyond three months" is said of a treatment). INV-001: ⊆ preventive treatments. |
| episodic / chronic conditions (`hasType(c, c1)`, `hasType(c, c1_3)` in `conditionHolds`) | read on the subject's types → **wrong for a subject whose migraine was chronic at one time and episodic at another**. A label of a treatment started in the episodic phase was decided under the 30 % threshold of NICE 1.3.28 for chronic migraine. Under DMKG/ÖKSG/SKG it was forced to "non-responder", although that criterion applies to that treatment. | E-045, E-046 (six component predicates), INV-062, INV-063 | **fixed.** `conditionHolds(c, t, s)` reads the condition on the label's treatment:<br>• episodic = given for migraine but not for chronic migraine (`givenFor`, on `preventiveFor`);<br>• chronic = given for chronic migraine;<br>• IHS Q6 = `t ∈ ihsQ6ChronicAlternative`.<br>Basis: 1.3.28 names the thresholds "in episodic migraine" and "in chronic migraine" for CGRP inhibitors "recommended as options for preventing episodic or chronic migraine" (1.3.24; re-checked at the source); DMKG/ÖKSG/SKG judges a prophylaxis "Bei der episodischen Migräne (eM)".<br>The settled point of review 02 (a criterion with no applicable component forces "non-responder") is unchanged. Only the time frame of "applicable" changed.<br>Text: E-045 Meaning and Notes (**Conditions on the treatment**), INV-062 and INV-063 Readings, row OUT-020. |
| `instrumentAdministrations`, `screeningAdministrations` | "available" → available results up to the as-of date, each dated | INV-062, INV-069, INV-081 to INV-083, INV-085, INV-096, INV-104, `valueAvailable` | ok. Every use is dated, except the availability condition of INV-062. That condition asks a label to show a result of an instrument whenever one is available, and the result at the evaluation where one exists (fix 11). A result from outside the evaluated periods is shown with its completion date (E-058), so no value is misattributed. Unchanged: watch point 5, and the availability condition has been settled since fix 03. |
| `drugOf`, `classOf`, `drugClassOf`, `label`, `showsValueNamed`; the 17 rules ("current guidance", fixed as of the model date, as OUT-018 says) | timeless or per course | — | ok |

### 2. Trigger-coverage sweep (R12-02 class): every cross-cutting requirement

**Method.** For each cross-cutting requirement I listed every element kind that reports the measure or summary it concerns. I then checked that the realising invariant is triggered by each of them. "Shown" means an item of the view's content, or a value that an item of the view refers to and shows as part of itself.

**Result.**
- Three triggers were incomplete and are extended: OUT-001 (INV-003), OUT-002 (INV-008) and OUT-003 (INV-011).
- The others are complete.
- Nothing is extended beyond a Stage 1 statement.

| Requirement (level) | Invariant | Element kinds that report it | v11 trigger | Result |
|---|---|---|---|---|
| OUT-001 period stated (MUST) | INV-003 | every view; every item that refers to a period; **a change, a residual burden or a composite index, which report values that may be shown in another view of the output (W1)** | periods that an item refers to directly | **extended.** The view of such an item shows a period with the dates of each referenced value's period (`referencedValues`, E-011). This is the period of a change shown apart from its values, which INV-054 does not place for changes outside a response comparison. R10b-01 is kept: the values themselves are not required next to the change. |
| OUT-002 labels (SHOULD) | INV-008 | day and attack counts; values referred to by a change, a residual burden or a composite index; peak-intensity distributions; marks of periods without migraine days; cycle lines and attack marks; cluster attack rates; trigger views | `PeriodValue` with `isMeasure` | **extended** (R12-02). Not extended: the E-018 count; symptom-attack counts; acute summaries and treated-attack lines; headache-free and symptom-free days (E-011 Notes). |
| OUT-003 completeness (SHOULD) | INV-011 | per-period values; referenced values; adherence windows (OUT-039 "over the evaluation window"); cycle lines, cluster and remission periods, and trigger views over the covered period | `PeriodValue` only | **extended** (R12-02). Not included:<br>• the history's treatment lists, which give dates, not a diary summary of a period;<br>• instrument and screening results, which are not diary coverage;<br>• evaluation time points and markers, which are dates. |
| OUT-038 caveats (SHOULD) | INV-099 | every view | every view | ok |
| OUT-038 indicators (SHOULD) | INV-100 | the overuse indicator, responder labels (also in scheme-window views), trigger views, graded instrument results, screening results | the same kinds | ok. The Notes now state that each named indicator is shown only by its own element kind, other content being an `OtherItem`, and that cluster and remission periods are dated periods under ICHD-3 definitions of terms, not indicators. |
| OUT-035 plain language (SHOULD) | INV-105 | the patient-facing overview, which INV-105 makes hold all of the overview's content | `PatientOverview` | ok |
| OUT-034 concise (SHOULD) | INV-104 | the clinician-facing summary | `ClinicianSummary` | ok |
| OUT-019 residual burden (SHOULD) | INV-060 | a change with a percentage form, the only element that shows a relative change | every such change | ok |
| OUT-011 label and Caveat | INV-020, INV-021 | duration summaries of treated attacks. Bout durations and treatment durations are not attack durations. | the same | ok |
| OUT-016 prompt, no diagnosis, interpretation | INV-047, INV-048, INV-100 | the overuse indicator only | the same | ok |
| OUT-020 criterion, values, not sole indicator | INV-062, INV-065 | responder labels, wherever shown | the same | ok |
| OUT-032 caveats | INV-090 | the trigger co-occurrence view | the same | ok |
| OUT-036 (c) and Caveat | INV-097, INV-098 | the five comparison kinds; every view | the same | ok. Their time frame changed in sweep 1. Series views are not comparisons; OUT-001 allows calendar months with their lengths visible. |
| OUT-037 | INV-091 to INV-093 | composite indices | the same | ok |
| OUT-030 window and cycles | INV-087 | cycle lines and attack marks in every view | the same | ok |
| OUT-009 markers | INV-035, INV-104 | the time-course view, and the clinician-facing summary, which names OUT-009 | the same | ok. OUT-009 asks for a time-course output with markers, not for markers on every series. |

### 3. Satisfiability pass

For every changed invariant and attribute, together with the invariants that constrain the same elements and views, I built a construction by hand. No admissible context makes the MUST and SHOULD constraints jointly unsatisfiable. No new derived attribute was added, so none is required where its relation is undefined.
- **INV-001.** The new conjuncts hold for any profile in which:
  - `aged12From ≤ adultFrom`;
  - the menstruation spans end by the as-of date;
  - `ihsQ6ChronicAlternative` ⊆ preventive treatments;
  - acute courses and acute medications have the same drugs (both may be empty).

  `Ctx` is not empty. No repertoire invariant relied on the removed contexts (an acute course without a medication, or the reverse).
- **INV-003 (MUST).** A period atom with given dates and the kind of the value's period can be added to any view. It satisfies INV-002, and no invariant limits the periods of a view, including INV-035, INV-041, INV-050 and INV-087. Where the value is in the same view, its own period atom satisfies the conjunct.
- **INV-008.** A label has no period. INV-009 (MUST) and INV-010 fix its definition for headache days and attacks. INV-031 applies only where a migraine-day label names `ihs2025MigraineDay`, which holds only where the view's migraine days follow that definition.
- **INV-011.**
  - The covered period, an adherence window and the periods of per-period values are in the view (INV-003). So is a period with the dates of each referenced value (INV-003, last conjunct).
  - An indicator with any of these periods and scope `allTypes` (INV-012) can be added.
  - Indicators are excluded from the first conjunct, so they create no new obligation.
- **INV-086 and INV-105.** The consequents are unchanged, and the antecedents are narrower. The lead-in (E-060, INV-087) keeps every required view satisfiable without a false date, for example a time range that begins before menarche.
- **E-041 with INV-055 (MUST), INV-058 (definitional) and INV-059 (MUST).** All three use the same `applicable`, so they stay mutually consistent. `adultsOnly` on the start implies `aged12AndOver` on the start (INV-001).
  - `applic.py`: scenarios A–F of the oscillation check give the same applicable rules as in v11.
  - Only the age-boundary scenarios G and H differ, in the direction of the population guarantee of R06-01.
  - A treatment without a stated start has no comparison (INV-056), so no requirement is lost.
- **INV-039, INV-096, INV-097, INV-098.** The age conditions only restrict the antecedents. In INV-096 the set C of child periods is not empty whenever its guard holds. The v11 constructions (28-day periods; a series of the time range with the values per period) meet them.
- **`conditionHolds` with E-046, INV-062 (SHOULD) and INV-063 (definitional).** The structure is unchanged. Only the argument of the condition changed, so every v11 construction remains valid. The counts of the watch-point guarantees are unchanged.
- **R12-01, under the stated time frame.**
  - INV-024: 12 ≤ 6 + 6 for January.
  - INV-044 and INV-046 for April 2026: the combined basis is 12 in each of the four periods of the span; triptans and non-opioid analgesics show days in each; neither reaches its level. So the sufficient antecedent forces "reached", and the necessary conditions hold.
  - For September (ibuprofen only, 12 days a month), the triptan indicator shows 0 days and excludes the class, so only one 8.2.6 class is left, giving "not reached". This is correct under the 8.2.3 comment.
  - INV-071, INV-072, INV-062 and INV-088: a summary of a medication not taken in a period has 0 treated attacks (INV-072, INV-074). In the cluster view it is scoped to cluster headache, at 15 minutes (INV-073).
- **`withdrawalStart` as a set.** Each start has its own views, so INV-049 to INV-052 hold per view, also for overlapping follow-up years.

### 4. Levels and paraphrases

- **No level changed.** Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 32. The extensions keep the level of the Stage 1 part they realise:
  - INV-003 MUST (OUT-001 "Every summary output MUST state the reporting period it covers (start date, end date and length)");
  - INV-008 SHOULD (OUT-002);
  - INV-011 SHOULD (OUT-003);
  - INV-086 MUST (OUT-030);
  - INV-039, INV-096, INV-097, INV-098 and INV-105 SHOULD (OUT-010, OUT-036, OUT-035);
  - INV-001 definitional.
- **Attribute declarations.** 172 (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. The changed context components belong to a value type.
- **Paraphrases.** Every changed Reading, Meaning, Conformance field, Notes field and row was compared with its predicate or declaration. "Has" in the readings of `hasType` means "has or has had" (E-009 Meaning). The coverage texts name no ID outside their row.
- **Two drafting errors were corrected before the final version:**
  - an INV-105 Notes example that contradicted its own sentence ("need not contain" a first day, for a month that contains menarche);
  - an E-008 Notes sentence that attributed the menstrual-relation view to INV-105.

### 5. Watch points (oscillation/check-after-iter-08.md)

- **Byte-identical to v11:** E-042, E-061, INV-050, INV-064, INV-087 and INV-104. The values are unchanged: `excludes` (17), `timing` (17), `fillsPeriod` (15 occurrences) and `containsPeriodOf` (12).
- **1 and 8.** No rule value changed.
- **2.** E-041 applicability:
  - (i) the INV-001 fallback type is unchanged;
  - (ii) the population guarantee is kept and made exact in time: age on the start of the treatment;
  - (iii) `excludes` is unchanged.

  Scenarios A–F are unchanged (`applic.py`).
- **3.** `ruleRuChildren` and the rule list are unchanged.
- **4.** INV-050 and the series tie of E-039 are unchanged. E-039 changed only in its Conformance and Notes (every start of withdrawal).
- **5.** In the responder labels these are unchanged: `#L.evaluated = 1` (7 occurrences, 7 before); `rc.treatment = L.treatment` (13, 13); `evaluationResult(L, r)` (6, 6); `pretreatmentBaseline(L, b)` (5, 5); `otherValueNamed` (6, 6); `UnderlyingKind` and `PeriodValueKind` stay open. The only change is the argument of `conditionHolds` (sweep 1).
- **6.** INV-100 changed only in its Notes (added text); `otherCompletenessExpression` and the `namedCriteria` gloss are unchanged.
- **7.**
  - E-060 changed in its Conformance text only.
  - INV-105 changed in the antecedent of its cycle-line conjunct (time frame); its consequent, the R02-07 overlap, is unchanged. The R04-01 lead-in is kept for every period that begins before the first day 1 shown.
  - INV-104 is unchanged.

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 109 invariants (INV-001 to INV-109), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-11; ISS-07 appears only as withdrawn. |
| References | No dangling E-, INV- or ISS- reference. S references lie in S-001–S-046 and S-101–S-106, and each S-1NN has a row in section 10. OUT references lie in 001–039. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025). Exactly one Realises field per item. Each row's E and INV columns equal the union of the Realises fields: E-008 +OUT-014, +OUT-016, +OUT-021, +OUT-035. No coverage text names an ID outside its row (ranges expanded). All rows say "full". |
| `omn` names | `names.py`: every new name is declared once: `menstruationSpans`, `adultFrom`, `aged12From`, `givenFor`, `childOn`, `childIn`, `menstruatesDuring`, `referencedValues` and `reports`. The removed names `ageGroup`, `aged12OrOlder` and `AgeGroup`, and the component `menstruates`, no longer occur in sections 1–11; the verb "menstruates" remains in prose. Every attribute selection names a declared attribute or component. The residual parser flags (inline value components; the free context variable `c` of INV-001, 8 more uses for its new conjuncts) are those of v11.<br>The new terms were type-checked by hand: `sameSpan(Period, DateSpan)` with `spanOf(m.period)`; `childIn(ctx, set →Period)`; `i.summary is peakIntensityDistribution`; `{ch ∈ {x} ∩ Change • ch.reference}`; `conditionHolds(ctx(outputOf(L)), L.treatment, …)`; `let C == {p ∈ ran sr.periods | childOn(c, p.start)}`. |
| Typing rule for levels | Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 32; total 109. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Scope sweep | Whole document searched for: enter, entry, record, input, captur, logged, stor, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field and questionnaire. 61 occurrences, as in v11, and no changed line contains any of them. The new occurrences of "diary information" (Stage 1 OUT-003's wording), of "taken" (the subject's medication history) and of "reported" (outputs reported) were read in context and are legitimate. No input entity, no storage term, and no relation or threshold with an input argument. |
| Quotes | No quote added or changed. 22 quoted fragments of the new text were checked by script against Stage 1 v18 and v11. The [S-015] and [S-008] wording was re-checked at the source (HTTP 200). |
| Snapshot | `cmp OUTPUT_MODEL.md history/v12.md`: identical. |
