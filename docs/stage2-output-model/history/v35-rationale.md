# Headache diary — rationale of the output model (Stage 2)
Version: v35 (companion of OUTPUT_MODEL.md v35)

## 1. Purpose and rules

This file holds what the model does not state formally: the verbatim evidence quotes, the reasons for design choices, what is deliberately not modelled, satisfiability arguments, worked examples and the search log (Stage 2 PROCESS.md sections 5, 6 and 6a). The model governs: an entry states no constraint that the model does not state, and a difference between an entry and the model is a defect of this file.

**Entry IDs.** An entry is identified by `<anchor>/<kind><nn>`, for example `E-041/Q07`, `INV-055/S01`, `C1-02/D01`, `SEC-3.8/D01`. The anchor is the ID of the model item the entry concerns (an element, an invariant, a case-table row, a Stage 1 issue, or a section `SEC-n.m`); `nn` is numbered per anchor and kind. Entry IDs are never renumbered or reused; an entry that becomes wrong is corrected in place or marked "withdrawn in vNN" and kept. Search-log entries are `SL-NNN`.

**Entry kinds.**

| Kind | Content |
|---|---|
| `Q` | Evidence quote: the source ID and the URL where it can be read (model section 10, or Stage 1 section 5 for S-001 to S-046), and the evidence text of v34, verbatim: location, quote, translation and the notes on the text layer; where the v34 text was not a single quote with its location, the whole text verbatim |
| `D` | Design reason, or a reading of a source or of Stage 1 |
| `N` | What is deliberately not modelled |
| `S` | Satisfiability argument |
| `W` | Worked example |
| `X` | Rejected alternative |

**Moved text.** The text of an entry moved from v34 (`Text (v34 <field>)`, or `Text (v34 <ID> <field>)` for text from another item, for example a merged invariant) is verbatim, with two exceptions: a reference to a v34 invariant that v35 merged into another item names its v35 place (model section 9), and a sentence that the consistency audit of v34 or remark R35-01 found to claim more than the model is corrected (`fixes/fix-iter-35.md`). A reference "X Notes" in moved text refers to the Notes of item X in v34, which v35 keeps in the model's Notes field of X and in the entries anchored at X.

**Order.** Section 2 lists the entries in model order: notation and conformance (2.1), catalogue and case-table rows (2.2), elements (2.3), invariants (2.4), traceability (2.5), Stage 1 issues (2.6), source data rows (2.7), and the text of invariants that v35 merged into another item, under that item (2.8). Within an anchor, entries are ordered by kind (Q, D, N, S, W, X) and number.

## 2. Entries, in model order

### 2.1 Notation and conformance

#### SEC-2.11/W01
- Kind: W
- Concerns: SEC-2.11
- Text: Worked unfoldings of the case-table forms (section 2.11):
- Form V, SD-ER-02: `const ruleNice1328 : EvaluationRule` and `axiom ruleNice1328 = EvaluationRule(guidance ↦ "NICE CG150 rec. 1.3.28", headacheType ↦ c1, ages ↦ adultsOnly, appliesTo ↦ {cgrpInhibitor}, excludes ↦ ∅, anchor ↦ treatmentStartAnchor, timing ↦ atOffset, minOffset ↦ weeks(12), maxOffset ↦ ∅)`; with the other rows, `const evaluationRules : set1 EvaluationRule ≙ {ruleNice1327, …, ruleTr73}`.
- Form M, SD-GB-01: the member `GradeBand(instrument ↦ midas, grade ↦ {"I"}, label ↦ "little or no disability", low ↦ 0, strictLow ↦ false, high ↦ {5})` of `gradeBands`.
- Form C, given function, SD-IC-01: `axiom label(c1) = "1. Migraine"`; given partial function, SD-SR-03: `axiom screeningMax(phq9, wholeScale) = 27`, and `(phq9, wholeScale) ∈ dom screeningMax`; 𝔹-valued, SD-IN-05: `axiom ¬ publishedGrading(halt30)`.
- Form C, defined predicate and function, SD-CL-02: `inControlRange(optimalControl, n) ⇔ n < 4` and `controlMinMonths(optimalControl) = {3}`; for a key with the cell `—`, the default: `controlMinMonths(modestControl) = ∅`.
- Form C, catalogue cases, C1-02: `ppGranularities(oc06, must) = MonthlyKind` and `ppRequired(oc06, must, c) = {q ∈ {(allTypes, {MigraineDays})} | hasType(c, c1)}`, so the instance of INV-118 for `l = must` and row `oc06` reads `∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ⇒ ∀ q ∈ ppRequired(oc06, must, c) • reportedTogether(c, q.2, q.1)`, which is v34 INV-015.
- Form D, SD-FX-08: `const shortestMonthlyDays : ℕ₁ ≙ 28`.

#### SEC-3.4/D01
- Kind: D
- Concerns: SEC-3.4
- Text (v34 section 3.4): OUT-001 names calendar months and 28-day periods for its frequency outputs ("Frequency outputs MUST be available per calendar month or per 28-day (4-week) period"). The model reads these as the frequency measures of OUT-004 to OUT-007, as OUT-009 names them ("frequency measures (OUT-004 to OUT-007)"): headache days, migraine days, moderate/severe headache days and attacks. Each part of a Stage 1 statement keeps its own strength (Stage 2 PROCESS.md section 4):

- Whether a measure is provided at all keeps the level of its own requirement: MUST for headache days, and for migraine days for patients with migraine (INV-118 (C1-01, C1-02)); SHOULD for moderate/severe headache days and attacks (INV-118 (C1-03, C1-05)).
- Availability per calendar month or 28-day period, for every period of the selected time range, is MUST wherever the measure is provided. For headache days, and for migraine days for patients with migraine (the condition of OUT-005), this is INV-118 (C1-01, C1-02); for moderate/severe headache days and attacks it is INV-118 (C1-04, C1-06) (`provides(K)`), as in their comparisons of equal-length periods (INV-037), per headache type (INV-118 (C1-13)) and in response comparisons (INV-057).
- The exploratory measures of residual burden of OUT-008 (headache-free days, symptom-free days, periods without migraine days) and the aura counts of OUT-013 are not read as frequency outputs. OUT-008 itself calls its measures "exploratory measures of residual burden", and OUT-013 belongs to Stage 1 group C, not to group B on headache frequency. See ISS-04.

#### SEC-3.8/D01
- Kind: D
- Concerns: SEC-3.8
- Text: The places of v34 to which R-MCF applies (restructure/plan-v35.md, section 7.2). In every place the formal test is that of v34; the prose that restated the rule in each place was replaced by "R-MCF (n)".
- (1) E-041 `inPopulation` (`∃ s ∈ startOf(c, t)`), hence `applicable`, E-043 `timePoints` `when`, INV-055, INV-058, INV-059: no evaluation rule applies, and no time point is asked or admitted, without a stated start.
- (1) INV-055 first conjunct, INV-102, INV-027, INV-071 (per-phase conjunct), INV-104 (response comparisons): `startOf(c, t) ≠ ∅ ⇒ …`, asked only where the start is stated.
- (1) the start fact of a response comparison (INV-123, `courseEvent` of kind `start`) and INV-068 `∃ s ∈ startOf(…) • …`: admitted only where the start is stated.
- (1) E-055 `startDate`, `duration`, `preventiveResponse`, `adherence` (`when startOf(ctx, self.treatment) ≠ ∅`) and INV-079 `∀ d ∈ l.duration • startOf(…) ≠ ∅`; E-055 `stopDate`, `stopReason` (`when stopped(…)`) and the stop facts of INV-123.
- (1) E-049 `baseline` (`when originalStart(…) ≠ ∅`) and INV-112 `∀ b ∈ v.baseline • ∃ s ∈ originalStart(…) • b.end < s`.
- (2) E-049 `onTreatmentPeriod` `when` (E-049/D04); INV-112 `courseBegunBy(ctx, v.treatment, q.start)`; INV-064 `courseBegunBy(…, p.start)`; INV-067 `courseBegunBy(…, a.window.start)`; INV-103 (no start condition); INV-109 (`∀ b ∈ startOf(…) • s.period.start = b` and `∀ f … • s.period.start ≤ f.date`).
- (1) and (2) INV-105 `courseOverlaps` (preventive) and `courseNotOutside` (acute), E-067.
- (1) INV-078: a line without a start date is not ordered.
- (1), (4) E-046 `evaluationResult`, `pretreatmentBaseline` (through `rc.treatmentStart`); INV-062 instrument conjuncts.
- (3) INV-094 (`previousConsultation`, `chosenPeriod`), INV-037 and INV-039 (`#c.comparedSpans ≥ 2`), E-056 and INV-080 (`schemeSelection`).
- (4) INV-081, INV-083, INV-096; the availability facts of INV-123; E-045 `valueAvailable` and INV-062; INV-069; INV-104; E-058 `baselineResult`.
- (1), for the anchor event: E-041 `applicable` (`anchorDates(c, t, r.anchor) ≠ ∅`); E-042 `intervalOnTreatment`.

### 2.2 Catalogue and case-table rows

#### C1-01/D01
- Kind: D
- Concerns: C1-01
- Text: Origin in v34: v34 INV-014 (Headache days per reporting period). Stage 1 part: OUT-001 (MUST), OUT-004 (MUST).

#### C1-02/D01
- Kind: D
- Concerns: C1-02
- Text: Origin in v34: v34 INV-015 (Migraine days per reporting period, for patients with migraine). Stage 1 part: OUT-001, OUT-005 (MUST).

#### C1-03/D01
- Kind: D
- Concerns: C1-03
- Text: Origin in v34: v34 INV-016 (Moderate/severe headache days per reporting period). Stage 1 part: OUT-006 (SHOULD).

#### C1-04/D01
- Kind: D
- Concerns: C1-04
- Text: Origin in v34: v34 INV-108 (Moderate/severe headache days and attacks per calendar month or 28-day period, where provided) (first measure). Stage 1 part: OUT-001 (MUST).

#### C1-05/D01
- Kind: D
- Concerns: C1-05
- Text: Origin in v34: v34 INV-017 (Attacks per reporting period). Stage 1 part: OUT-007 (SHOULD).

#### C1-06/D01
- Kind: D
- Concerns: C1-06
- Text: Origin in v34: v34 INV-108 (Moderate/severe headache days and attacks per calendar month or 28-day period, where provided) (second measure). Stage 1 part: OUT-001 (MUST).

#### C1-07/D01
- Kind: D
- Concerns: C1-07
- Text: Origin in v34: v34 INV-018 (Intensity summary per reporting period). Stage 1 part: OUT-010 (SHOULD).

#### C1-08/D01
- Kind: D
- Concerns: C1-08
- Text: Origin in v34: v34 INV-019 (Duration summary per reporting period). Stage 1 part: OUT-011 (SHOULD).

#### C1-09/D01
- Kind: D
- Concerns: C1-09
- Text: Origin in v34: v34 INV-022 (Associated symptoms and most bothersome symptom across periods, for migraine). Stage 1 part: OUT-012 (SHOULD).

#### C1-10/D01
- Kind: D
- Concerns: C1-10
- Text: Origin in v34: v34 INV-023 (Acute-medication days per reporting period: total, by class and by drug). Stage 1 part: OUT-014 (MUST).

#### C1-11/D01
- Kind: D
- Concerns: C1-11
- Text: Origin in v34: v34 INV-025 (Weekly view of acute-medication days). Stage 1 part: OUT-015 (SHOULD).

#### C1-12/D01
- Kind: D
- Concerns: C1-12
- Text: Origin in v34: v34 INV-026 (Functional impact per reporting period). Stage 1 part: OUT-027 (SHOULD).

#### C1-13/D01
- Kind: D
- Concerns: C1-13
- Text: Origin in v34: v34 INV-028 (Separate presentation per headache type). Stage 1 part: OUT-029 (MUST).

#### C1-14/D01
- Kind: D
- Concerns: C1-14
- Text: Origin in v34: v34 INV-029 (Intensity per headache type, where provided). Stage 1 part: OUT-029 (SHOULD, where OUT-010 is provided).

#### C2-01/D01
- Kind: D
- Concerns: C2-01
- Text: Origin in v34: v34 INV-101 (No output presented as replacing clinical assessment or as a diagnosis). Stage 1 part: OUT-038 (SHOULD).

#### C2-02/D01
- Kind: D
- Concerns: C2-02
- Text: Origin in v34: v34 INV-013 (No completeness cut-off presented as clinically validated). Stage 1 part: OUT-003 (SHOULD NOT).

#### C2-03/D01
- Kind: D
- Concerns: C2-03
- Text: Origin in v34: v34 INV-021 (Durations of treated attacks are not a stand-alone efficacy measure). Stage 1 part: OUT-011 Caveat (SHOULD).

#### C2-04/D01
- Kind: D
- Concerns: C2-04
- Text: Origin in v34: v34 INV-048 (Indicator is not a diagnosis of medication-overuse headache). Stage 1 part: OUT-016 (MUST NOT).

#### C2-05/D01
- Kind: D
- Concerns: C2-05
- Text: Origin in v34: v34 INV-106 (No output decides on the continuation of a preventive treatment). Stage 1 part: OUT-018 Caveat (MUST); OUT-020 Rationale (second part).

#### C2-06/D01
- Kind: D
- Concerns: C2-06
- Text: Origin in v34: v34 INV-065 (A responder label is not the sole indicator of individual benefit). Stage 1 part: OUT-020 (SHOULD NOT).

#### C2-07/D01
- Kind: D
- Concerns: C2-07
- Text: Origin in v34: v34 INV-107 (No output decides which definition of acute treatment response applies). Stage 1 part: OUT-023 Caveat (SHOULD).

#### C2-08/D01
- Kind: D
- Concerns: C2-08
- Text: Origin in v34: v34 INV-043 (Three-month view assigns no diagnosis). Stage 1 part: OUT-028 (SHOULD NOT).

#### C2-09/D01
- Kind: D
- Concerns: C2-09
- Text: Origin in v34: v34 INV-084 (Screening results are not psychiatric diagnoses). Stage 1 part: OUT-033 Caveat (SHOULD).

#### C3-01/D01
- Kind: D
- Concerns: C3-01
- Text: Origin in v34: v34 INV-099 (Interpretive caveats on every summary). Stage 1 part: OUT-038 (SHOULD).

#### C3-02/D01
- Kind: D
- Concerns: C3-02
- Text: Origin in v34: none; E-010 Conformance stated that the `exploratoryMeasure` annotation of the OUT-008 measures is MAY, which imposes no constraint. Stage 1 part: OUT-008 (MAY).

#### C3-03/D01
- Kind: D
- Concerns: C3-03
- Text: Origin in v34: v34 INV-020 (Durations of treated attacks are labelled as influenced by acute treatment). Stage 1 part: OUT-011 (SHOULD).

#### C3-04/D01
- Kind: D
- Concerns: C3-04
- Text: Origin in v34: v34 INV-047 (Indicator worded as a prompt for clinical review). Stage 1 part: OUT-016 (MUST).

#### C3-05/D01
- Kind: D
- Concerns: C3-05
- Text: Origin in v34: v34 INV-100 (Indicators, labels and associations require clinical interpretation), first conjunct. Stage 1 part: OUT-038 (SHOULD).

#### C3-06/D01
- Kind: D
- Concerns: C3-06
- Text: Origin in v34: v34 INV-052 (Label of the expected transient worsening). Stage 1 part: OUT-017 (SHOULD).

#### C3-07/D01
- Kind: D
- Concerns: C3-07
- Text: Origin in v34: v34 INV-100 (Indicators, labels and associations require clinical interpretation), second conjunct. Stage 1 part: OUT-038.

#### C3-08/D01
- Kind: D
- Concerns: C3-08
- Text: Origin in v34: v34 INV-100 (Indicators, labels and associations require clinical interpretation), fourth conjunct. Stage 1 part: OUT-038, OUT-026.

#### C3-09/D01
- Kind: D
- Concerns: C3-09
- Text: Origin in v34: v34 INV-090 (Caveats of the trigger co-occurrence view); v34 INV-100 (Indicators, labels and associations require clinical interpretation), third conjunct. Stage 1 part: OUT-032 (caveats SHOULD), OUT-038.

#### C3-10/D01
- Kind: D
- Concerns: C3-10
- Text: Origin in v34: v34 INV-100 (Indicators, labels and associations require clinical interpretation), fifth conjunct. Stage 1 part: OUT-038, OUT-033.

#### C3-11/D01
- Kind: D
- Concerns: C3-11
- Text: Origin in v34: v34 INV-098 (Paediatric outputs are presented as supportive information). Stage 1 part: OUT-036 Caveat (SHOULD).

#### C3-12/D01
- Kind: D
- Concerns: C3-12
- Text: Origin in v34: v34 INV-092 (A migraine composite index is exploratory and shown with its components), first conjunct. Stage 1 part: OUT-037 (SHOULD).

### 2.3 Elements

#### E-001/D01
- Kind: D
- Concerns: E-001
- Text (v34 Meaning): The claims that Stage 1 forbids or discourages are enumerated so that the prohibitions can be stated (INV-119 (C2-02, C2-03, C2-08, C2-04, C2-06, C2-09, C2-01, C2-05, C2-07)).
- Text (v34 Notes): The claim values exist only so that prohibitions can name them; no Stage 1 requirement asks for any claim to be made.

#### E-003/D01
- Kind: D
- Concerns: E-003
- Text (v34 Notes): `plainLanguage` and `concise` are declared qualities of the wording; whether wording is plain or concise is judged by readers and is not further formalised (Stage 1 states no measurable criterion).

#### E-006/D01
- Kind: D
- Concerns: E-006
- Text (v34 Notes): `containsPeriodOf` and `fillsPeriod` are used in INV-104 and INV-105, and `fillsPeriod` also in INV-050: a series of periods within a covered period exists only when the covered period contains at least one whole period, and the series of the clinician-facing summary, of the patient-facing overview and of the withdrawal follow-up view consists of all whole periods of its granularity within the period the view covers, 28-day periods being counted from the first day of that period (for the withdrawal follow-up view, the start of withdrawal, INV-050).

#### E-007/D01
- Kind: D
- Concerns: E-007
- Text (v34 Meaning): The selected time range consists of whole periods of the selected granularity (INV-001), because the outputs over it are given for every period in it (OUT-004). A period chosen by the clinician for the clinician-facing summary (`chosenPeriod`) is subject to no such condition: OUT-034 places none on it, so it may have any dates up to the as-of date (for example 15 August to 20 October, 67 days). A selected time range that a clinician reader selects is a period chosen by the clinician as well (INV-094).

#### E-008/Q00
- Kind: Q
- Concerns: E-008
- Source: [S-011] — https://pmc.ncbi.nlm.nih.gov/articles/PMC9188162/
- Source: [S-014] — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Source: [S-022] — https://www.ema.europa.eu/en/documents/scientific-guideline/draft-guideline-clinical-investigation-medicinal-products-treatment-migraine-cluster-headache-revision-2_en.pdf
- Text: Stage 1 statements of the requirements listed; preventive treatments of other headache types than migraine: Stage 1 OUT-009 (weekly values "Where weekly granularity is clinically relevant (tension-type headache, cluster headache, early onset of effect)", in the view with "dated markers for the start, dose change and stop of preventive treatments") and OUT-031 ([S-014] "optimum acute and preventative treatments are maintained", for active cluster headache). Repeated withdrawals: Stage 1 OUT-017 ([S-014] "The relapse rate is high within the first year"). A restart after a pause: Stage 1 OUT-022 ("stopped, paused or reduced"; [S-011] "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal."). The course that a resumed course resumes, and the original start of the treatment (`resumes`, `originalStart`): Stage 1 OUT-022 ("compare it with both the on-treatment period and the original pre-treatment baseline"; [S-022] "to detect possible rebound phenomena (i.e. frequency of migraine days per month going above its baseline)"), with the [S-011] quote above. `ihsQ6ChronicAlternative` is the condition of the IHS Q6 statement quoted in E-045, which concerns the continuation of a treatment ("acceptable for treatment continuation beyond three months"). `aged12From` is the age limit of the population of NICE CG150, quoted in E-041 ([S-015], "young people (aged 12 years and older) and adults").

#### E-008/D01
- Kind: D
- Concerns: E-008
- Text (v34 Notes): **Pause, restart and discontinuation.** A course ends with its one stop or pause, dated on its last day on treatment. A treatment that is resumed after a stop or pause, for example restarted after a pause because migraine worsens ([S-011], Stage 1 OUT-022), is a new course: another member of `preventiveTreatments` (or of `acuteTreatments`) with the same drug (`drugOf`) and its own start, course events, guidance types and headache types.

#### E-008/D02
- Kind: D
- Concerns: E-008
- Text (v34 Notes): **Resumed courses.** For a preventive treatment, the context also states which earlier course the new course resumes: (t₁, t₂) ∈ `resumes` when the course t₂ resumes the treatment of the course t₁ after the stop or pause of t₁. A course resumes at most one course, a preventive course of the same drug that has stopped or paused before it starts, and is resumed by at most one (INV-001); so the courses that a course resumes, directly or through intermediate courses (`resumesFrom`), form one chain in chronological order, whose first course is the treatment as it was first started. `originalStart(c, t)` is the start that the context states for that first course; for a course that resumes no course, it is the course's own start (`startOf`). Where the context states no start for the first course, for example for a treatment that the subject was already taking at the first course event the context states for it, `originalStart` is empty: the start of a later course of the chain is a restart, and the context does not state when the first course began, so no date places the treatment's original start. It bounds the original pre-treatment baseline of post-stop monitoring (OUT-022: "the original pre-treatment baseline"), which is asked for and shown only where `originalStart` is not empty (E-049, INV-112). Everything else that is aligned to a treatment start keeps the start of its own course: the response comparison and its time points, the treatment review view, adherence, the treatment line and the markers (OUT-018: "aligned to the treatment start date"; INV-001 Notes). A later course of the same drug that does not resume the treatment of an earlier course, for example a drug tried again as a new treatment, is not linked, and its original start is its own start. A link may follow a stop that the context states as a pause or as a discontinuation, because the model treats the two kinds alike (below): a discontinuation trial to check whether the prophylaxis is still needed is among the cases of OUT-022 (Stage 1 OUT-022, [S-023] and [S-030]). Like the courses themselves, `resumes` describes the subject's history up to the as-of date. A pause that is later made definitive without a restart adds no course event: the course keeps its one stop, dated on its last day on treatment. The context states that stop as a pause or as a discontinuation; every relation of the model treats the two kinds alike (`e.kind is stop`), except that a marker and a post-stop monitoring view show the kind the context states (INV-123).

#### E-008/D03
- Kind: D
- Concerns: E-008
- Text (v34 Meaning): For a period in which a headache type, a medication or a treatment did not occur, the values that these sets require are 0 days, a summary of 0 treated attacks or an indication that is not reached, which are correct values; so none of these sets makes an output for such a period wrong.

#### E-008/D04
- Kind: D
- Concerns: E-008
- Text (v34 Meaning): A pause ends its course: a treatment restarted after it, as in the [S-011] statement that OUT-022 quotes ("we suggest restarting the treatment if migraine worsens after treatment withdrawal"), is a new course with its own start that resumes the earlier course (`resumes`), so that the treatment's original start, the start of the treatment as it was first started (`originalStart`), is the start that the context states for the first course, where it states one; and a pause that is later made definitive without a restart adds no course event (Notes).

#### E-009/Q01
- Kind: Q
- Concerns: E-009; SD-IC-01; SD-IC-02; SD-IC-03; SD-IC-04; SD-IC-05
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: [S-001] "1. Migraine", "1.2 Migraine with aura", "1.3 Chronic migraine", "2. Tension-type headache (TTH)", "2.3 Chronic tension-type headache" (classification list, p. 8)

#### E-009/Q02
- Kind: Q
- Concerns: E-009; SD-IC-06
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: classification list, p. 9
- Quote: "3.1 Cluster headache"

#### E-009/Q03
- Kind: Q
- Concerns: E-009; SD-IC-07; SD-IC-08; SD-IC-09; SD-IC-10; SD-IC-11; SD-IC-12; SD-IC-13; SD-IC-14; SD-IC-15; SD-CLS-01; SD-CLS-02; SD-CLS-03; SD-CLS-04; SD-CLS-05; SD-CLS-06
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: [S-001] "8.2 Medication-overuse headache (MOH)", "8.2.1 Ergotamine-overuse headache", "8.2.2 Triptan-overuse headache", "8.2.3 Non-opioid analgesic-overuse headache", "8.2.4 Opioid-overuse headache", "8.2.5 Combination-analgesic-overuse headache", "8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused", "8.2.7 Medication-overuse headache attributed to unspecified or unverified overuse of multiple drug classes", "8.2.8 Medication-overuse headache attributed to other medication" (classification list, p. 12)

#### E-009/D01
- Kind: D
- Concerns: E-009
- Text (v34 Notes): The hierarchy axioms follow the code numbering of the classification list. Diagnostic criteria are not restated. `c8_2_7` is listed only to make explicit that OUT-016 does not refer to it.

#### E-011/D01
- Kind: D
- Concerns: E-011
- Text (v34 Notes): `ihs2025MigraineDay` is named because the count on which the IHS 2025 control levels rest follows it (E-018), and INV-031 relates that count to the migraine days of a view only where the view's label names it.

#### E-011/D02
- Kind: D
- Concerns: E-011
- Text (v34 Notes): **Forms of the measures.** OUT-002 applies to "Outputs that report migraine days, headache days, moderate/severe headache days or attacks", whatever form the report takes, because different definitions select different days and attacks (OUT-002 Rationale). `reports` therefore covers every form in which the model shows the days or the attacks that these measures count, as a number for a period, a rate per day or per week, a distribution, a change, or as the days and attacks themselves in a view over time. It does not cover the values of other measures, which count a part of these days or attacks selected by another property, or their complement: the attacks with an associated symptom (E-025, a form of the symptom presence of OUT-012); the treated attacks of an acute-treatment summary and their outcomes (E-050 to E-053, whose outcome measures OUT-023 takes from the IHS acute trial guideline, FDA guidance and the EHF definitions); and headache-free and symptom-free days (E-020, E-021, measures of OUT-008 that OUT-002 does not name). Nor does it cover the single count of the IHS position statement 2025 (E-018), whose definition this element names (`ihs2025MigraineDay`) and which the model requires only with a label that names that criterion (INV-062; E-018 Notes).

#### E-012/D01
- Kind: D
- Concerns: E-012
- Text (v34 Notes): **Type scope of a value.** `concerns` reads the conditions "for migraine" and "for tension-type headache" of OUT-037 on a value (E-033, INV-091 to INV-093, INV-115): a value over all types concerns t when the subject has a headache type and every type it has falls under t, so that the restriction of OUT-037 applies to it. `onlyOfType` and `scopeFor` are used where a value is taken to consist of the headaches of one type only: the attacks of a cluster attack rate (INV-089) and of an acute-treatment summary with the 15-minute time point (INV-073), the rates and acute-treatment summaries that the cluster view shows for the subject's cluster headache (INV-088), and the values on which a responder criterion is decided or that it names (E-045, E-046, INV-062). A value over all types consists of the headaches of type t only when the subject has a headache type and every type it has or may have falls under t. When the subject has or may have another type, OUT-029 presents the values separately for each type ("has, or may have"), and the value over all types includes headaches that the output presents under the other type. `scopeFor` picks one scope for the values of all the subject's headaches of type t, so that a criterion is decided on one value per period, not on the value of a subtype that covers only some of these headaches. For a subject whose types under t are a single subtype of t (for example chronic migraine, `c1_3`, and tension-type headache), this scope is `ofType(t)`, a value of its own next to the per-type value of OUT-029 (INV-118 (C1-13)) with the same headaches.

#### E-013/D01
- Kind: D
- Concerns: E-013
- Text (v34 Notes): Stage 1 gives the proportion of days as an example ("for example expressed as the proportion of days of the period that the diary covers"), so the form is open: the number of covered days, the proportion, or another expression as the output words it (`otherCompletenessExpression`, for example the number of days of the period without diary information), alone or together; INV-012 relates the two numeric forms to the period.

#### E-013/D02
- Kind: D
- Concerns: E-013
- Text (v34 Notes): OUT-003 asks for the indicator with "Each reporting period", next to "the summary measures", so INV-011 covers every kind of summary that a view shows for a period, not only per-period values: cycle lines, cluster periods and remissions, and attack and trigger dates summarise the diary information of the view's covered period, and a change, a residual burden or a composite index reports values of other periods (`referencedValues`, E-011).

#### E-013/N01
- Kind: N
- Concerns: E-013
- Text (v34 Notes): The 80 % working-group figure and trial exclusion rules are not clinical cut-offs (OUT-003 Caveats); the model states none.

#### E-014/D01
- Kind: D
- Concerns: E-014
- Text (v34 Notes): The value is obtained from diary information; how is out of scope.

#### E-016/D01
- Kind: D
- Concerns: E-016
- Text (v34 Notes): Published definitions of a migraine day count different days (OUT-002 Rationale), so migraine days are related to no count that rests on another definition.

#### E-018/Q01
- Kind: Q
- Concerns: E-018
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Location: section "Setting goals of migraine burden while on treatment", p. 6
- Quote: "Modest Control. This is defined as four to six days with migraine or moderate-to-severe headache per month."

#### E-018/Q02
- Kind: Q
- Concerns: E-018
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Location: same section, p. 6, the paragraph directly after the four control levels, which are "the above goals"; in the PDF text layer line ends break "definition" and "following". The three definitions that follow classify a day from what the patient reports and are not quoted, section 1, item 3.
- Quote: "The assessment of the above goals requires a clear definition of migraine day. The panel decided to adopt the following three definitions of a migraine day, as modified from van der Arend et al. (45), in subjects with a diagnosis of migraine:"

#### E-018/Q03
- Kind: Q
- Concerns: E-018
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Location: same section, p. 6, the paragraph after the three definitions; the omitted words describe the days included
- Quote: "We included in our definitions of treatment goals also moderate-to-severe headache days as a proxy of migraine days [...]"

#### E-018/D01
- Kind: D
- Concerns: E-018
- Text (v34 Notes): Published definitions of a migraine day count different days (OUT-002 Rationale), so the count is not related to migraine days that follow another definition. [S-010] includes moderate-to-severe headache days as a proxy of migraine days and adopts no definition of them, while the moderate/severe headache days of a view follow the definition its label names (OUT-002, E-017); so the count is related neither to moderate/severe headache days nor to the sum of migraine days and moderate/severe headache days.

#### E-018/D02
- Kind: D
- Concerns: E-018
- Text (v34 Notes): The count is none of the four measures of OUT-002, each of which has several published definitions; it has one definition, that of [S-010], which this element states and which every control-level label that the count is shown with names as its criterion (INV-062). So the definition labels of OUT-002 (INV-008, `reports`) are not asked for it.

#### E-019/D01
- Kind: D
- Concerns: E-019
- Text (v34 Notes): The value is obtained from diary information; how is out of scope. Being a separate element type from `DayCount`, an attack count is never merged with a day count ("separately from the number of headache or migraine days"). OUT-007 Caveat (the EMA draft moves the primary endpoint to migraine days) does not constrain the output.

#### E-020/D01
- Kind: D
- Concerns: E-020
- Text (v34 Notes): The relation is an inequality because days not covered by diary information are neither (definitions state nothing about them).

#### E-022/D01
- Kind: D
- Concerns: E-022
- Text (v34 Notes): A period without migraine days may be marked for every subject, without the condition "for patients with migraine", as OUT-008 states it; see ISS-03.

#### E-023/Q00
- Kind: Q
- Concerns: E-023
- Source: [S-030] — http://dhos.dk/wp-content/uploads/2020/06/2932-Referenceprogram_2020_final_web-24.06.20.pdf
- Text: Stage 1 OUT-010. One scale and one form for the periods compared: Stage 1 OUT-010 (Evidence basis: "a change in intensity between periods (for example the halving of intensity in [S-030]) can only be read when the scale is known"), OUT-021 ("The purpose is that efficacy can be judged across these dimensions") and OUT-035 ("so that patients can follow the effect of their treatment").

#### E-023/D01
- Kind: D
- Concerns: E-023
- Text (v34 Notes): The forms are those Stage 1 gives as examples; `otherIntensitySummary` keeps the list open, as Stage 1 does, and states the form of each such summary as the output names it (`OtherSummary`), for example a median peak intensity or the share of headache days with severe pain. Two other forms are not one form, so `onSameScale` holds for two summaries in other forms only where they state the same form, compared by equality as texts are (section 2.8).

#### E-023/D02
- Kind: D
- Concerns: E-023
- Text (v34 Notes): **Periods compared.** A change in intensity between two periods can be read only where their summaries are on the same scale and in the same form (OUT-010 Evidence basis). So wherever the model asks for intensity for several periods in order to compare them, the summaries of these periods are on one scale and in one form (`onSameScale`): in a comparison of selected periods (INV-039; OUT-010: "allow comparison between periods"), for the baseline and on-treatment periods of the treatment review view (INV-069, OUT-021) and over the time course of the patient-facing overview (INV-105; OUT-035: "over time"). Which scale and which form is the diary's choice; the relation fixes neither. The per-period summaries of INV-118 (C1-07, C1-14) report intensity for each period on a stated scale; the comparison between periods that OUT-010 asks for is that of INV-039.

#### E-025/D01
- Kind: D
- Concerns: E-025
- Text (v34 Notes): Stage 1 fixes no form of "presence"; the two forms are the natural ones and `otherPresenceSummary` keeps the list open, stating the form of each such summary (`OtherSummary`, E-023). In the treatment review view, which presents these values "for the same pre-treatment baseline and on-treatment periods" (OUT-021), the summaries of one symptom for these periods are in one form (INV-069): a number of days and a number of attacks have different units and cannot be compared, nor can two other forms, for example the share of headache days and the share of attacks with the symptom (`inSameForm` holds for two summaries in other forms only where they state the same form). The relation fixes no form.

#### E-027/D01
- Kind: D
- Concerns: E-027
- Text (v34 Notes): Being separate element kinds, aura values are never merged with headache values. Aura counts are not read as frequency outputs in the sense of OUT-001 ("Frequency outputs MUST be available per calendar month or per 28-day (4-week) period"; section 3.4), so their availability per calendar month or 28-day period is not required; see ISS-04.

#### E-028/Q01
- Kind: Q
- Concerns: E-028
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2.3 Non-opioid analgesic-overuse headache, comments, p. 123; the text layer breaks "non-opioid" at a line end
- Quote: "For the purposes of ICHD-3, all non-opioid analgesics are regarded as a single class"

#### E-028/Q02
- Kind: Q
- Concerns: E-028; SD-CMB-01
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2.6, diagnostic criterion B, p. 124; the omitted text is a footnote marker; "≥" is a glyph without a text mapping in the PDF text layer
- Quote: "Regular intake of any combination of ergotamine, triptans, non-opioid analgesics and/or opioids [...] on a total of ≥10 days/month for >3 months without overuse of any single drug or drug class alone."

#### E-028/Q03
- Kind: Q
- Concerns: E-028; SD-CMB-01
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2.6, note 2, p. 125
- Quote: "Without overuse of any single drug or drug class alone means that criterion B has not been fulfilled for any of the specific subtypes 8.2.1–8.2.5."

#### E-028/D01
- Kind: D
- Concerns: E-028
- Text (v34 Notes): The paracetamol, NSAID, acetylsalicylic-acid and other subforms of 8.2.3 are not separate classes, because ICHD-3 regards all non-opioid analgesics as one class; the individual drugs are shown by the per-drug breakdown (E-029). Stage 1's example label "simple analgesics" is not the ICHD-3 class name; see ISS-02. See ISS-01 on the classes of 8.2.6 (`classesOf826`).

#### E-029/D01
- Kind: D
- Concerns: E-029
- Text (v34 Notes): The bounds by the sum hold for every period up to the as-of date because the subject's acute medications include every medication it has used up to that date, including those it no longer uses (E-008): a day with acute medication in any such period is a day with a medication of one of their classes and one of their drugs. A medication not used in a period shows 0 days for it.

#### E-032/Q01
- Kind: Q
- Concerns: E-032; SD-CLS-01; SD-CLS-02; SD-CLS-03; SD-CLS-04; SD-CLS-05; SD-CLS-06; SD-CMB-01; SD-FX-06
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2 Medication-overuse headache, Description, p. 122
- Quote: "[...] regular overuse of acute or symptomatic headache medication (on 10 or more or 15 or more days/month, depending on the medication) for more than three months."

#### E-032/Q02
- Kind: Q
- Concerns: E-032; SD-CLS-01; SD-FX-06
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2.1, Description, p. 123
- Quote: "[...] regular use of ergotamine on 10 or more days/month for more than three months."

#### E-032/Q03
- Kind: Q
- Concerns: E-032; SD-CLS-02; SD-FX-06
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2.2, Description, p. 123
- Quote: "[...] regular use of one or more triptans on 10 or more days/month for more than three months."

#### E-032/Q04
- Kind: Q
- Concerns: E-032; SD-CLS-03; SD-FX-06
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2.3, Description, p. 123
- Quote: "[...] regular use of one or more non-opioid analgesics on 15 or more days/month for more than three months."

#### E-032/Q05
- Kind: Q
- Concerns: E-032; SD-CLS-04; SD-FX-06
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2.4, diagnostic criterion B, p. 124; the omitted text is a footnote marker; "≥" is a glyph without a text mapping in the PDF text layer
- Quote: "Regular intake of one or more opioids [...] on ≥10 days/month for >3 months."

#### E-032/Q06
- Kind: Q
- Concerns: E-032; SD-CLS-05; SD-FX-06
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2.5, diagnostic criterion B, p. 124; omitted footnote markers; same note on "≥"
- Quote: "Regular intake of one or more combination-analgesic medications [...] on ≥10 days/month for >3 months."

#### E-032/Q07
- Kind: Q
- Concerns: E-032; SD-CLS-06; SD-FX-06
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2.8, diagnostic criterion B, p. 125; omitted footnote marker; same note on "≥"
- Quote: "Regular overuse, on ≥10 days/month for >3 months, of one or more medications other than those described above, [...] taken for acute or symptomatic treatment of headache."

#### E-032/D01
- Kind: D
- Concerns: E-032
- Text (v34 Notes): ICHD-3 expresses the levels per month and does not define the month; the model applies them to calendar months or 28-day periods and the output states which (OUT-001).

#### E-032/D02
- Kind: D
- Concerns: E-032
- Text (v34 Notes): The reading "on ≥ 10 days/month for > 3 months" as "in every month of a span longer than three months" is the model's; ICHD-3 states that these numbers rest on expert opinion (OUT-016 Caveats).

#### E-032/D03
- Kind: D
- Concerns: E-032
- Text (v34 Notes): Because the basis values are shown medication days, a missing diary day can only make the shown count lower than the true count; the completeness indicator (E-013) shows the coverage of each period.

#### E-032/N01
- Kind: N
- Concerns: E-032
- Text (v34 Notes): Only the medication-use part of ICHD-3 8.2 is shown; the headache-day criterion of 8.2 is not part of this indicator.

#### E-033/D01
- Kind: D
- Concerns: E-033
- Text (v34 Notes): The formula of an index is computed from diary information and is out of scope. Stage 1 OUT-037 covers only migraine and tension-type headache; the model states nothing for other headache types (OUT-037 Caveats).

#### E-036/D01
- Kind: D
- Concerns: E-036
- Text (v34 Notes): The weekly and monthly limits of IHS Q12 [S-009] belong to that source and are not part of the output (OUT-015 Caveats). The weekly view is required for all headache types combined, not per headache type; see ISS-09.

#### E-037/D01
- Kind: D
- Concerns: E-037
- Text (v34 Notes): `values` is a reference (section 2.5); the values are nevertheless shown side by side in the comparison's view, at MUST: each refers to a compared period, which INV-003 places in the comparison's view, and an item that refers to a period atom is part of the view that atom is part of (INV-003 Notes). Equal length is required where OUT-001 asks for it, not for every comparison: calendar months differ in length, and OUT-001 makes the lengths visible instead (OUT-001 Caveats).

#### E-038/D01
- Kind: D
- Concerns: E-038
- Text (v34 Notes): The ICHD-3 criteria for 1.3 and 2.3 are not shown or restated: the view refers to the codes, and applying the criteria is the clinician's diagnosis.

#### E-039/Q00
- Kind: Q
- Concerns: E-039
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Text: Stage 1 OUT-017 (the window "4 to 8 weeks after the start of withdrawal" is in the Stage 1 statement and in its quote [S-015] rec. 1.3.48; "from the start of withdrawal onward").

#### E-039/D01
- Kind: D
- Concerns: E-039
- Text (v34 Notes): "The following year" is read as the 12 months after the start of withdrawal: the days from the start of withdrawal to the day before `plusMonths(withdrawalStart, followUpMonths)` (day convention, section 2.8).

#### E-039/D02
- Kind: D
- Concerns: E-039
- Text (v34 Notes): The view begins on the start of withdrawal, and its covered period may end on any day, for example on the day of the review 4 to 8 weeks after the start or on the as-of date of a running follow-up ("from the start of withdrawal onward", OUT-017); so it need not be a run of whole periods. The series consists of the whole periods of its granularity from the start of withdrawal within the covered period (`fillsPeriod`, E-006), and the headache days and acute-medication days of the covered period itself show the days after its last whole period as well (INV-050). A view shorter than any whole period that begins on the start of withdrawal has no series and shows the values of its covered period only. The review window SHOULD be shown in every follow-up view (E-039 `reviewWindow`); INV-051 fixes its dates, which may lie after the covered period and the as-of date.

#### E-039/D03
- Kind: D
- Concerns: E-039
- Text (v34 Notes): OUT-017 asks for the review window of NICE CG150 1.3.48 for every patient withdrawing from overused medication; NICE CG150 covers young people aged 12 years and older and adults (E-041), so for a child under 12 the model follows Stage 1; see ISS-11.

#### E-039/D04
- Kind: D
- Concerns: E-039
- Text (v34 Notes): A subject may withdraw from overused medication more than once (relapse is common within the first year, OUT-017), so the context holds every start of withdrawal up to the as-of date (E-008), and each has its own follow-up view; the follow-up of an earlier withdrawal stays available for its own year after a later one has begun.

#### E-040/D01
- Kind: D
- Concerns: E-040; v34 INV-054
- Text (v34 Notes): The two forms, and the two values compared next to them, are required at MUST only for the changes of a response comparison, because OUT-018 (MUST) requires them for its comparison ("showing both the values of each period and the absolute and percentage change from baseline"). No Stage 1 statement part requires them for a change shown elsewhere, for example as the treatment effect in the patient-facing overview (OUT-035), in the post-stop monitoring view (OUT-022) or in a scheme-window view (OUT-025): OUT-019 asks, wherever a percentage change in migraine or headache days is shown, for the residual burden next to it (INV-060), and OUT-020 for the underlying values of a responder label, whose changes are those of its response comparison (INV-062). Such a change may therefore show one form only, and it is still a change, to which INV-053, INV-060 and, for children and adolescents, INV-097 apply. Its two values may be shown in another view of the output, so the view that shows the change states the periods they refer to (INV-003, OUT-001: every summary output states the reporting period it covers), the definition of its measure (INV-008, OUT-002), which, where the view of the two values also states a definition for the measure, is the definition stated there, the one the values follow (INV-111), and the completeness of these periods (INV-011, OUT-003); this does not require the two values next to the change (E-040/D01).
- Text (v34 INV-054 Notes): The invariant constrains the changes of response comparisons only. For them the MUST of OUT-018 requires the values of each period together with the change. Because the values of a response comparison are shown in the comparison's view (INV-056 with INV-003; INV-003 Notes), each of its changes is shown in that view as well. OUT-020 (SHOULD) asks for the same values with a responder label, whose changes are those of its response comparison (INV-062); it is the second part cited (section 3.3, item 6). A change shown outside a response comparison, for example as the treatment effect in the patient-facing overview, in the post-stop monitoring view or in a scheme-window view, is not constrained by this invariant, because no Stage 1 statement part requires the two values it compares next to it. INV-053 (definitional), INV-060 (SHOULD, OUT-019: the residual burden next to a percentage change in migraine or headache days) and, for children and adolescents, INV-097 (SHOULD, OUT-036 (c)) apply to it (E-040 Notes).

#### E-041/Q00
- Kind: Q
- Concerns: E-041; SD-ER-01; SD-ER-02; SD-ER-03; SD-ER-04; SD-ER-05; SD-ER-06; SD-ER-07; SD-ER-08; SD-ER-09; SD-ER-10; SD-ER-11; SD-ER-12; SD-ER-13; SD-ER-14; SD-ER-15; SD-ER-16; SD-ER-17; SD-ER-18
- Source: [S-008] — https://ricerca.univaq.it/retrieve/b7f186a9-06ec-4e9c-b132-4f785bbeb121/puledda-et-al-2024-international-headache-society-global-practice-recommendations-for-preventive-pharmacological.pdf
- Source: [S-011] — https://pmc.ncbi.nlm.nih.gov/articles/PMC9188162/
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Source: [S-016] — https://www.sign.ac.uk/media/2408/sign-155-migraine-2026-update-002.pdf
- Source: [S-018] — https://www.aan.com/Guidelines/Home/GetGuidelineContent/1180
- Source: [S-028] — https://richtlijnendatabase.nl/richtlijn/hoofdpijn/migraine/profylactische_behandeling_migraine.html
- Source: [S-033] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=295_4
- Source: [S-034] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=169_3
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Text: Stage 1 OUT-018; OUT-036 (d) ("present efficacy of treatment from diary data as recommended in paediatric guidance") for the paediatric guidance [S-034]. The offsets of eleven rules are in Stage 1 quotes of OUT-018: [S-015] recs 1.3.27 ("3 to 6 months after starting"), 1.3.28 ("after 12 weeks of treatment"), 1.3.29 ("after 2 treatment cycles"); [S-018] rec. 14A ("at least 8–12 weeks at the recommended tolerated dose of most medications"); [S-016] section 4.1 ("eight weeks at the target dose or maximum tolerated dose (for those with a titration schedule)"; "For treatments of fixed dose [...] assessed at 3 months"); [S-011] question 3 ("a minimum of 3 consecutive months on treatment"); [S-008] Q2 ("a minimum of three months for injectable drugs taken on a monthly basis, and a minimum of six months for injectable drugs administered quarterly"); [S-028] module "Profylactische behandeling migraine", Aanbeveling ("Titreer naar de ondergrens van de geadviseerde therapeutische breedte" and "evalueer het effect niet eerder dan na 2-3 maanden behandeling"); [S-033] section 7.1 ("через 3 месяца терапии"). The [S-028] and [S-033] fragments are parts of the Stage 1 quotes of OUT-018, whose translations carry over. The headache type of every rule is in the Stage 1 quotes and source titles: "migraine prophylaxis" ([S-015] 1.3.27), "the frequency of migraines" ([S-015] 1.3.28), "changed to episodic migraine" ([S-015] 1.3.29), "medications for migraine prevention" ([S-018] 14A), "SIGN 155: Pharmacological management of migraine" ([S-016]), "In individuals with episodic or chronic migraine" ([S-011] question 3), "Preventive Pharmacological Treatment of Migraine" ([S-008]), module "Profylactische behandeling migraine" ([S-028]), "профилактическое лечение М" ([S-033]; its list of abbreviations, p. 4, reads "М – мигрень", that is, М is migraine), «Мигрень» (the titles of [S-033] and [S-034]) and "Migren Klinik Protokolü" ([S-035]); the new quotes below, or the headings they stand under, name migraine as well: "a new migraine oral preventive treatment" ([S-008] Q2), "for migraine prevention" ([S-018] 14B), "для профилактики хронической М" ([S-033] section 3.3), "профилактической терапии мигрени" ([S-034]), "Migren Profilaktik Tedavi-Yönetim-6" (Kutu 8 of [S-035]), "3. MİGREN BAŞ AĞRISI TEDAVİSİ" (the section of [S-035] that contains section 3.6.3.9) and "7. MİGRENDE GİRİŞİMSEL İŞLEMLER" (the heading of the chapter of [S-035] that contains section 7.3, PDF p. 82, and the running header of its pages; translation: "7. Interventional procedures in migraine"). The offsets of the other seven rules (AAN/AHS 14B, IHS 2024 Q2 for oral preventives, the Russian botulinum time point, the Russian paediatric time point, Turkish Box 8, section 3.6.3.9 and section 7.3), the ages each guidance covers, the migraine section of NICE CG150, the drug of Turkish section 7.3, and the injection intervals of botulinum toxin type A on which the exclusions of NICE CG150 1.3.27 and Turkish Box 8 depend (Notes, **Types and exclusions**) are not stated in Stage 1:

#### E-041/Q01
- Kind: Q
- Concerns: E-041; SD-ER-01; SD-ER-02; SD-ER-03
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Location: Overview page of CG150, https://www.nice.org.uk/guidance/cg150
- Quote: "This guideline covers the diagnosis and management of tension-type headache, migraine (including migraine with aura and menstrual-related migraine), cluster headache and medication overuse headache in young people (aged 12 years and older) and adults."

#### E-041/Q02
- Kind: Q
- Concerns: E-041; SD-ER-01; SD-ER-02; SD-ER-03
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Text: [S-015] the headings "Migraine with or without aura" and, within it, "Prophylactic treatment review", under which recommendations 1.3.27, 1.3.28 and 1.3.29 stand (Recommendations, section 1.3 "Management"; the Stage 1 URL)

#### E-041/Q03
- Kind: Q
- Concerns: E-041; SD-ER-02
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Location: recommendation 1.3.24; the omitted text is the condition on earlier preventive medicines, quoted in Stage 1 OUT-024, and the list of technology appraisals
- Quote: "For CGRP inhibitors recommended as options for preventing episodic or chronic migraine in adults who have at least 4 migraine days a month [...]"

#### E-041/Q04
- Kind: Q
- Concerns: E-041; SD-ER-03
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Location: recommendation 1.3.26; the omitted text gives further conditions
- Quote: "Intramuscular injection of botulinum toxin type A is recommended as an option for preventing chronic migraine in adults [...]"

#### E-041/Q05
- Kind: Q
- Concerns: E-041; SD-ER-04; SD-ER-05
- Source: [S-018] — https://www.aan.com/Guidelines/Home/GetGuidelineContent/1180
- Location: Clinician Summary, p. 1, the sentence below the title "Pharmacologic treatment for migraine prevention in adults practice guideline"
- Quote: "This is a summary of the American Academy of Neurology (AAN) guideline, “Pharmacologic Treatment for Migraine Prevention in Adults,”"

#### E-041/Q06
- Kind: Q
- Concerns: E-041; SD-ER-05
- Source: [S-018] — https://www.aan.com/Guidelines/Home/GetGuidelineContent/1180
- Location: Recommendation 14 "When to Assess Treatment Efficacy", level B, p. 7; the repeated phrase "before assessing efficacy" is in the source
- Quote: "14B. Clinicians should wait 24 weeks at the recommended dose before assessing efficacy of onabotulinumtoxinA injections for migraine prevention before assessing efficacy."

#### E-041/Q07
- Kind: Q
- Concerns: E-041; SD-ER-04
- Source: [S-018] — https://www.aan.com/Guidelines/Home/GetGuidelineContent/1180
- Location: Recommendation 14, level B, p. 8
- Quote: "14H. If suboptimal response is observed after 12–24 weeks (see 14A and 14B), and other options are available and not contraindicated, clinicians should engage in shared decision making with the patient to initiate an alternate medication for migraine prevention."

#### E-041/Q08
- Kind: Q
- Concerns: E-041; SD-ER-06; SD-ER-07
- Source: [S-016] — https://www.sign.ac.uk/media/2408/sign-155-migraine-2026-update-002.pdf
- Location: section 1.2.1 "Overall objectives", p. 1
- Quote: "This guideline provides recommendations based on current evidence for best practice in the acute and prophylactic management of adults with migraine using pharmacological therapies or devices."

#### E-041/Q09
- Kind: Q
- Concerns: E-041; SD-ER-06; SD-ER-07
- Source: [S-016] — https://www.sign.ac.uk/media/2408/sign-155-migraine-2026-update-002.pdf
- Location: same section, p. 1, two sentences later
- Quote: "Studies of children with migraine were not included, however the recommendations could be considered for treating adolescents with migraine."

#### E-041/Q10
- Kind: Q
- Concerns: E-041; SD-ER-08
- Source: [S-011] — https://pmc.ncbi.nlm.nih.gov/articles/PMC9188162/
- Location: Background, first paragraph; the omitted text is a reference number
- Quote: "In 2019 the European Headache Federation (EHF) issued the first guideline for the use of CGRP-mAbs for migraine prevention in adults [...]"

#### E-041/Q11
- Kind: Q
- Concerns: E-041; SD-ER-08
- Source: [S-011] — https://pmc.ncbi.nlm.nih.gov/articles/PMC9188162/
- Location: Background, second paragraph
- Quote: "Considering the new knowledge on the topic, the EHF council decided to update the 2019 guideline."

#### E-041/Q12
- Kind: Q
- Concerns: E-041; SD-ER-09
- Source: [S-008] — https://ricerca.univaq.it/retrieve/b7f186a9-06ec-4e9c-b132-4f785bbeb121/puledda-et-al-2024-international-headache-society-global-practice-recommendations-for-preventive-pharmacological.pdf
- Location: Q2 "When should the effectiveness of a migraine preventive treatment be assessed?", Recommendations, Optimal, first sentence, p. 9, directly before the sentence on injectable drugs quoted in Stage 1 OUT-018; the asterisk refers to the footnote "*See Q6 for the criteria for assessing the effectiveness of a preventive therapy."
- Quote: "In individuals initiating a new migraine oral preventive treatment, we suggest evaluating effectiveness* after three months at the target dose."

#### E-041/Q13
- Kind: Q
- Concerns: E-041; SD-ER-09
- Source: [S-008] — https://ricerca.univaq.it/retrieve/b7f186a9-06ec-4e9c-b132-4f785bbeb121/puledda-et-al-2024-international-headache-society-global-practice-recommendations-for-preventive-pharmacological.pdf
- Location: Q2, Recommendations, Essential, p. 9
- Quote: "In individuals initiating a new oral preventive treatment, we suggest evaluating effectiveness* after three months of treatment at target dose."

#### E-041/Q14
- Kind: Q
- Concerns: E-041; SD-ER-09; SD-ER-10; SD-ER-11
- Source: [S-008] — https://ricerca.univaq.it/retrieve/b7f186a9-06ec-4e9c-b132-4f785bbeb121/puledda-et-al-2024-international-headache-society-global-practice-recommendations-for-preventive-pharmacological.pdf
- Text: [S-008] "Q2 – When should the effectiveness of a migraine preventive treatment be assessed?" (heading of Q2, p. 9) and "Q13 – What are the suggested drugs for migraine prevention in children and adolescents?" (heading of Q13, p. 17)

#### E-041/Q15
- Kind: Q
- Concerns: E-041; SD-ER-12
- Source: [S-028] — https://richtlijnendatabase.nl/richtlijn/hoofdpijn/migraine/profylactische_behandeling_migraine.html
- Location: module "Profylactische behandeling migraine", section "Zoeken en selecteren"
- Quote: "P: Patiënten (kinderen en volwassenen) met migraine, bij wie preventieve behandeling geïndiceerd is"
- Translation: "P: Patients (children and adults) with migraine in whom preventive treatment is indicated"

#### E-041/Q16
- Kind: Q
- Concerns: E-041; SD-ER-13; SD-ER-14
- Source: [S-033] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=295_4
- Location: title page, p. 1
- Quote: "Возрастная категория: взрослые"
- Translation: "Age category: adults"

#### E-041/Q17
- Kind: Q
- Concerns: E-041; SD-ER-13; SD-ER-14
- Source: [S-033] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=295_4
- Location: section 3.3 "Профилактическая терапия", Комментарии to the recommendation "Рекомендуется считать профилактическое лечение эффективным, если частота дней с ГБ сокращается через 3 месяца терапии на 50% и более от исходной", which section 7.1 repeats, p. 39
- Quote: "при отсутствии эффекта в течение 3 месяцев следует заменить выбранное профилактическое средство на другой препарат; эффективность БТА – минимум через 6 месяцев терапии."
- Translation: "if there is no effect within 3 months, the chosen preventive agent should be replaced by another drug; efficacy of BTA – after a minimum of 6 months of therapy."

#### E-041/Q18
- Kind: Q
- Concerns: E-041; SD-ER-14
- Source: [S-033] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=295_4
- Location: section 3.3, p. 40; the asterisks are in the source
- Quote: "Рекомендуется для профилактики хронической М в качестве средства первого выбора ботулинический токсин типа А - гемагглютинин комплекс** 155 - 195 Ед по протоколу PREEMPT [85]"
- Translation: "Botulinum toxin type A–haemagglutinin complex, 155–195 U according to the PREEMPT protocol, is recommended as a first-choice agent for the prevention of chronic migraine [85]"

#### E-041/Q19
- Kind: Q
- Concerns: E-041; SD-ER-15
- Source: [S-034] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=169_3
- Location: Приложение Б "Алгоритмы действий врача", flowchart "Алгоритм диагностики и ведения пациента с мигренью", p. 52; the text layer gives the box as quoted
- Quote: "назначение препаратов для профилактической терапии мигрени с учетом коморбидности. Контроль эффективности терапии через 3мес."
- Translation: "prescription of medicines for the preventive therapy of migraine taking comorbidity into account. Monitoring of the efficacy of therapy after 3 months."

#### E-041/Q20
- Kind: Q
- Concerns: E-041; SD-ER-15
- Source: [S-034] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=169_3
- Text: [S-034] "Возрастная группа" followed by "дети" (title page, p. 1; the title page is an image without a text layer). Translation: "Age group: children"

#### E-041/Q21
- Kind: Q
- Concerns: E-041; SD-ER-15
- Source: [S-034] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=169_3
- Location: section 2, "Критерии постановки диагноза", p. 17
- Quote: "Диагностика мигрени у детей и подростков показана всем пациентам при подозрении на её наличие."
- Translation: "Diagnosis of migraine in children and adolescents is indicated in all patients in whom it is suspected."

#### E-041/Q22
- Kind: Q
- Concerns: E-041; SD-ER-16
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Location: section 3.6.2 "Farmakolojik Tedavi Stratejileri: Profilaktik Tedavi", Kutu 8 "Migren Profilaktik Tedavi-Yönetim-6", box headed "Farmakolojik Profilaktik Tedavide Yol Haritası", seventh item, PDF p. 48
- Quote: "Yeterli süre, etkinlik için en az 2-3 ay ve tedavi için en az 6 aydır,"
- Translation: "The adequate duration is at least 2–3 months for efficacy and at least 6 months for treatment,"

#### E-041/Q23
- Kind: Q
- Concerns: E-041; SD-ER-17
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Location: section 3.6.3.9 "Onabotulinumtoxin A", PDF p. 57
- Quote: "Hastalar 3 enjeksiyon siklusu sonra değerlendirilmeli ve fayda görmeyen hastalarda tedavi kesilmelidir."
- Translation: "Patients should be evaluated after 3 injection cycles, and treatment should be stopped in patients who do not benefit."

#### E-041/Q24
- Kind: Q
- Concerns: E-041; SD-ER-16; SD-ER-17; SD-ER-18
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Location: heading of section 6, PDF p. 77; also in the table of contents, PDF p. 7
- Quote: "6. ÇOCUK VE ERGENDE MİGREN"
- Translation: "6. Migraine in children and adolescents"

#### E-041/Q25
- Kind: Q
- Concerns: E-041; SD-ER-16
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Location: section 3.6.3.9 "Onabotulinumtoxin A", PDF p. 57, two sentences before the sentence on the evaluation after 3 injection cycles quoted above
- Quote: "Hasta fayda görüyorsa enjeksiyonlar 3 ayda bir, hasta epizodik forma dönüşünceye dek devam edilmelidir."
- Translation: "If the patient benefits, the injections should be continued every 3 months until the patient returns to the episodic form."

#### E-041/Q26
- Kind: Q
- Concerns: E-041; SD-ER-18
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Location: section 3.6.3.9 "Onabotulinumtoxin A", PDF p. 57, the first sentence of the paragraph after the one that names the PREEMPT 1 and PREEMPT 2 trials
- Quote: "Bu tedavide baş ve boyun bölgesinde standardize edilmiş 31 adet noktaya toplamda 155 ünite onabotulinum toksin A enjekte edilmektedir."
- Translation: "In this treatment, a total of 155 units of onabotulinum toxin A is injected at 31 standardised points in the head and neck region."

#### E-041/Q27
- Kind: Q
- Concerns: E-041; SD-ER-16; SD-ER-18
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Location: section 7.3 "Botulinum Toksin Enjeksiyonu", third item, PDF p. 86
- Quote: "Uygulanım yeri ve dozu: frontal, temporal, oksipital ve servikal bölgeler, 31 nokta, her noktaya 5 ünite (toplam 155 ünite), 3 ay aralıklarla,"
- Translation: "Site and dose of administration: frontal, temporal, occipital and cervical regions, 31 points, 5 units per point (155 units in total), at 3-month intervals,"

#### E-041/Q28
- Kind: Q
- Concerns: E-041; SD-ER-18
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Location: section 7.3 "Botulinum Toksin Enjeksiyonu", fourth item, PDF p. 86, directly after the item quoted above; the space inside "kez" (times) is printed so on the page and in the text layer
- Quote: "Etkisini değerlendirmek için en az 2 k ez uygulanmalıdır,"
- Translation: "To evaluate its effect, it should be administered at least 2 times,"

#### E-041/Q29
- Kind: Q
- Concerns: E-041; SD-ER-01
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Source: [S-106] — https://www.nice.org.uk/guidance/ta260/chapter/2-The-technology
- Location: recommendation 1.3.26, the sentence after the one quoted above; the guidance it names is [S-106]
- Quote: "For full details, see NICE's technology appraisal guidance on botulinum toxin type A (TA260, 2012)."

#### E-041/Q30
- Kind: Q
- Concerns: E-041; SD-ER-01
- Source: [S-106] — https://www.nice.org.uk/guidance/ta260/chapter/2-The-technology
- Location: section 2 "The technology", paragraph 2.1, last sentence
- Quote: "The recommended re-treatment schedule is every 12 weeks (see the summary of product characteristics)."

#### E-041/D01
- Kind: D
- Concerns: E-041
- Text (v34 Notes): **The rule list.** OUT-018 requires the comparison "at the evaluation time points named in current guidance"; its parenthesis ("for example […]") gives examples of these time points and does not limit them. The rule list is the set of evaluation time points for a person's preventive treatment that the guidance which Stage 1 cites for OUT-018 names in its recommendations and guidance text, read in full and not only in the passages Stage 1 quotes: NICE CG150 [S-015], AAN/AHS 2026 [S-018], SIGN 155 [S-016], the EHF 2022 guideline [S-011], IHS 2024 [S-008], the NVN module [S-028], the Russian clinical recommendations for adults [S-033] and the Turkish Ministry of Health protocol [S-035], with its chapters on pharmacological and on interventional treatment; and, for children and adolescents, the Russian clinical recommendations for children [S-034], the paediatric guidance that Stage 1 cites for OUT-036 (d). The IHS trial guideline [S-002], also cited in OUT-018, names durations and analysis periods of controlled trials, not time points for evaluating a person's treatment.

#### E-041/D02
- Kind: D
- Concerns: E-041
- Text (v34 Notes): **Population.** Every rule is a rule of its guidance for the population that guidance addresses, and applies only within it (`inPopulation`): its type list (`appliesTo`) says which preventive treatments of that population the time point is named for, not which headache disorder or which people the guidance concerns. All the guidance quoted is guidance on preventive treatment of migraine, so every rule has the headache type `c1`, and a preventive treatment given only for another headache type (for example verapamil for cluster headache, or a preventive treatment for tension-type headache) has none of these time points; NICE CG150, which covers cluster and tension-type headache as well, names no review time point for their prophylaxis (ISS-10). The ages are those the guidance states: AAN/AHS 2026 and the Russian clinical recommendations for adults are guidance for adults; SIGN 155 makes recommendations for "adults with migraine", and its sentence that they "could be considered for treating adolescents" permits but does not name them for adolescents, so the model reads SIGN 155 as adult guidance; the EHF 2022 guideline names its population "individuals with episodic or chronic migraine" and is the update of the 2019 guideline "for migraine prevention in adults", so the model reads it as adult guidance; NICE CG150 covers young people aged 12 years and older and adults (`aged12AndOver` for 1.3.27), while 1.3.28 and 1.3.29 are the stopping rules for CGRP inhibitors and botulinum toxin type A, which NICE recommends "in adults" (1.3.24, 1.3.26), so they are `adultsOnly`; the IHS 2024 recommendations also address children and adolescents (Q13) and Q2 states no age, and the NVN module concerns "kinderen en volwassenen" (children and adults), so both are `anyAge`; the Russian clinical recommendations for children concern children and adolescents (`childrenAndAdolescentsOnly`); the Turkish protocol has a section on migraine in children and adolescents, and its Box 8 and sections 3.6.3.9 and 7.3 state no age, so it is `anyAge`, as IHS 2024 Q2 is. A time point that a guidance only permits for a subject outside its population (for example SIGN 155 for an adolescent) is not an `EvaluationTimePoint` of the rule (INV-058); a diary may show it as an `OtherItem`.

#### E-041/D03
- Kind: D
- Concerns: E-041
- Text (v34 Notes): **Age on the treatment start.** The subject's age is read on the start of the treatment (`inPopulation`, with `adultFrom` and `aged12From`, E-008), not on the as-of date: a treatment is started, and evaluated at the time points its anchor sets, as a treatment of a person of that age, so a treatment started in childhood or adolescence keeps the time points of guidance for children and adolescents, and does not take those of guidance for adults, when the subject has become an adult by the as-of date, and conversely. A treatment whose start the context does not state is within the population of no rule; it also has no response comparison, which is aligned to the start (INV-123).

#### E-041/D04
- Kind: D
- Concerns: E-041
- Text (v34 Notes): **Types and exclusions.** One criterion decides the members of `excludes`, and it is applied to every rule of the list: a type is excluded from a rule that the guidance names for all preventive treatment (`appliesTo = allPreventiveTypes`), and so for that type, when the same guidance gives the type, in another rule of the list that it names for that type and not for all preventive treatment, a time point that lies after this rule's time point or, for a window, after its latest date, both as the guidance states them or as a guidance to which it refers for details states them; the guidance's statement for the type is then the more specific one, and this rule would place an assessment of a treatment of that type before the guidance's own time point for it. A rule that the guidance names for particular types is itself a time point that the guidance names for these types, and it excludes none of them: where the same guidance names two time points for the same type, each in a rule for particular types, neither statement is more specific than the other, and the comparison is available at each (Turkish sections 7.3 and 3.6.3.9, below). A time point named for all preventive treatment, a time point that does not lie after this rule's time point or window, and a time that the guidance names but that is not an evaluation time point of the list (above) exclude nothing. Applied to every rule: `ruleAan14A` (8 to 12 weeks after the tolerated dose is reached) excludes onabotulinumtoxinA, because 14B gives it 24 weeks at the recommended dose, after the window, and 14H refers to both ("after 12–24 weeks (see 14A and 14B)"); `ruleRu71` (3 months after the start) excludes onabotulinumtoxinA, because the comments of the Russian section 3.3 give botulinum toxin type A ("БТА") a minimum of 6 months of therapy, after it, while their time point for anti-CGRP monoclonal antibodies is the same 3 months; `ruleTrBox8` (2 to 3 months after the start) excludes onabotulinumtoxinA, because section 3.6.3.9 evaluates it after 3 injection cycles, given every 3 months, that is, about 9 months after the first injection, after the window, and section 7.3 after at least 2 administrations at 3-month intervals, from the end of the second cycle, about 6 months after the first injection, also after the window; `ruleNice1327` (3 to 6 months after the start) excludes nothing, because 1.3.28 gives CGRP inhibitors 12 weeks after the start, before the window, and 1.3.29 gives botulinum toxin type A the end of the second treatment cycle, which, with the re-treatment every 12 weeks of the technology appraisal guidance to which 1.3.26 refers for full details ([S-106]), is 24 weeks after the first injection and lies within the window, so that an assessment within the window can coincide with the 1.3.29 time point; `ruleRuChildren` (3 months after the start) excludes nothing, because the Russian clinical recommendations for children name no other evaluation time point; and every rule named for particular types excludes nothing, because it is itself a time point that its guidance names for these types. For all of these rules but one, the guidance gives their types no later time point of its own either (NICE 1.3.28 and 1.3.29; AAN/AHS 14B; SIGN 155 for titrated and for fixed-dose treatment, which are different types; the EHF 2022 guideline, whose re-evaluation in selected cases is not an evaluation time point of the list; IHS 2024 Q2 for oral preventives and for monthly and quarterly injectables, which are different types, its dose increase of onabotulinumtoxinA after the first cycle being no evaluation time point; NVN; the Russian section 3.3 time point; Turkish section 3.6.3.9). The one exception is Turkish section 7.3 (at least 2 administrations, from the end of the second cycle): section 3.6.3.9 of the same protocol evaluates onabotulinumtoxinA later, after 3 injection cycles, but both rules are named for that type alone, so neither is more specific than the other; section 7.3 states its minimum as the condition for evaluating the effect ("Etkisini değerlendirmek için", to evaluate its effect), and the comparison is available at the end of the second and at the end of the third cycle. A treatment may have several types (a course of onabotulinumtoxinA is also a quarterly injectable, E-008), so the exclusion is a component of its own (`excludes`), not a narrower `appliesTo`, and only a listed type excludes a rule (E-008, INV-001). "БТА" is not expanded in the list of abbreviations of [S-033] (pp. 4–5); the recommendation on botulinum toxin type A quoted above, which names the PREEMPT protocol at 155–195 U, shows its meaning. The botulinum toxin type A of [S-033] and of NICE CG150 is modelled as the type `onabotulinumtoxinA`.

#### E-041/D05
- Kind: D
- Concerns: E-041
- Text (v34 Notes): **Readings.** AAN/AHS 14A ("at least 8–12 weeks") is modelled as a window from 8 to 12 weeks after the tolerated dose is reached. NVN ("niet eerder dan na 2-3 maanden behandeling", no earlier than after 2–3 months of treatment) is modelled in the same way, as a window from 2 to 3 months after the treatment start, and so is Turkish Box 8 ("etkinlik için en az 2-3 ay", at least 2–3 months for efficacy). NVN applies to dose-titrated preventives, because the recommendation concerns prophylactics titrated to their therapeutic range ("Titreer naar de ondergrens van de geadviseerde therapeutische breedte"). The Russian section 7.1 time point ("через 3 месяца терапии", after 3 months of therapy) is the time point of the criterion `critRu71` (E-045); the recommendation concerns preventive treatment of migraine in general, so it applies to every preventive treatment type within its population (preventive treatment of migraine in adults) except botulinum toxin type A. AAN/AHS 14B ("wait 24 weeks at the recommended dose before assessing efficacy") and the Russian botulinum time point ("минимум через 6 месяцев терапии", after a minimum of 6 months of therapy) are minimum times (`atLeastOffset`), from the date the recommended dose was reached and from the treatment start; for a course given at the recommended dose from its start, the date the target dose was reached is its start. IHS 2024 Q2 for oral preventives ("after three months at the target dose") is modelled as `atOffset` from the date the target dose was reached, as NICE 1.3.28 ("after 12 weeks of treatment") and the Russian section 7.1 are from the start; the Russian paediatric "Контроль эффективности терапии через 3мес." (monitoring of the efficacy of therapy after 3 months), in the flowchart box on prescribing preventive therapy, is `atOffset` from the treatment start. Turkish section 7.3 ("en az 2 k ez", at least 2 times, given "3 ay aralıklarla", at 3-month intervals) is a minimum (`atLeastOffset`) from the end of the second treatment cycle: each administration begins a treatment cycle, and the effect of the second one is evaluated once its cycle has ended, as the model reads NICE 1.3.29 ("after 2 treatment cycles"); its botulinum toxin, 155 units at 31 points, is the onabotulinumtoxinA to which section 3.6.3.9 gives the same dose (Evidence), so the rule is named for `onabotulinumtoxinA`, as the botulinum toxin type A of [S-033] and of NICE CG150 is (above). NICE 1.3.29 and Turkish sections 3.6.3.9 and 7.3 are anchored at the end of the second, the third and the second treatment cycle, with no further offset (`weeks(0)`). Every preventive treatment has at least one type and is given for at least one headache type that the subject has or may have (INV-001), so `applicable` holds for the rules of all preventive types whenever the treatment is given for migraine or a subtype of it, the subject was, on the start of the treatment, of the ages the rule's guidance covers, the treatment is not of a type the rule excludes, and the treatment has the rule's anchor; a missing type listing cannot make these rules inapplicable, because only a listed type excludes a rule. At each anchor date, the time point of such a rule is then shown and required where the course is taken through its interval (**Stop or pause**, below). Because no course event precedes the treatment start (INV-001), every rule except NICE 1.3.29 and Turkish sections 3.6.3.9 and 7.3 puts its time point at least 8 weeks after the start; the time point of these three rules is the date of the end of a treatment cycle itself, the first day after the cycle (E-008; for section 7.3, the earliest time point), and where that date is less than 28 days after the start, no calendar month or 28-day period beginning on or after the start can end at it, that is, on the day before it (`fitsMonthlyPeriod`, `atTimePoint`, E-042; INV-055).

#### E-041/D06
- Kind: D
- Concerns: E-041
- Text (v34 Notes): **Stop or pause.** Every rule's guidance names its time point for a treatment taken over an interval from the anchor, for example: "after 12 weeks of treatment" and "after 2 treatment cycles" ([S-015] 1.3.28 and 1.3.29), the review of "the need for continuing migraine prophylaxis 3 to 6 months after starting prophylactic treatment" ([S-015] 1.3.27), "after a minimum of 3 consecutive months on treatment" ([S-011]), "at least 8–12 weeks at the recommended tolerated dose" ([S-018] 14A), "eight weeks at the target dose" ([S-016]), "after three months at the target dose" ([S-008] Q2), "через 3 месяца терапии" (after 3 months of therapy, [S-033] section 7.1), "niet eerder dan na 2-3 maanden behandeling" (no earlier than after 2–3 months of treatment, [S-028]) and "etkinlik için en az 2-3 ay" (at least 2–3 months for efficacy, [S-035] Kutu 8) (Evidence). So the time point is named for a course that is taken through that interval. `applicable` judges the rule for the treatment (type, population, exclusion, anchor), and `intervalOnTreatment` (E-042) the anchor date: the time point is shown and required only where no stop or pause of the course is dated before the last day of the interval, the day before the time point (for a window, before its first date, the end of the minimum interval the guidance names); a stop or pause is dated on the last day of the course (section 2.8), so a course stopped on that last day has completed the interval. A course stopped or paused earlier, or before the anchor date, has no time point of the rule at that anchor date, whatever the anchor kind, just as a course has no time point of a rule anchored at the end of a treatment cycle that did not take place; a course that has not stopped, or stopped after the interval, has every time point of the rules that apply to it. A stop or pause after the first date of a window leaves the window's time point in place, and the comparison at it then ends on or before the stop (INV-055).

#### E-041/N01
- Kind: N
- Concerns: E-041
- Text (v34 Notes): **Named, but not evaluation time points** (not modelled): a dose-optimisation check (AAN/AHS 14C, "by 8 weeks"; IHS 2024 Q2 comment, a dose increase of onabotulinumtoxinA after the first cycle); the check, right after a nerve block, that the block has taken effect, which concerns the technique of the block, not the response of a treatment against its baseline (Turkish section 7.1: [S-035] "Enjeksiyon sonrası blokajın etkinliği araştırılmalı hipoestezi ya da parestezi bulunmaz ise tekrarlanmalıdır.", PDF p. 83; translation: "After the injection, the effectiveness of the block should be examined; if there is no hypoaesthesia or paraesthesia, it should be repeated."); the decisions after the assessments of 14A and 14B (AAN/AHS 14D and 14H, which refer to their 8–12 and 12–24 weeks); the adequate trial of "at least eight weeks at the target dose" reviewed when the effect is partial (IHS 2024 Q4, Evidence); periods of continuation, tapering, pause or phasing out (IHS 2024 Q5; AAN/AHS 17B; EHF 2022 question 4; SIGN 155 section 4.1 and its key recommendations; the Russian adult section 3.3, 6–12 months; Turkish Box 8, at least 6 months of treatment; Turkish section 6.2.2, at least 4 months for children; the minimum courses of 3 months of the Russian paediatric recommendations); the continuation of IHS 2024 Q6 "beyond three months" under its 30 % alternative (a criterion, E-045); a restart (IHS 2024 Q7); statements that report other guidelines or trials (IHS 2024 Q2 Evidence; IHS 2024 Q6 Background, a two- to three-month period from the maximally tolerated dose that it attributes to other expert recommendations; NVN, the placebo response that stabilises after 16 weeks); the onset and the maximum of the effect (Turkish protocol, 2–3 months and six months); course lengths and injection intervals (NICE CG150 1.3.21, acupuncture over 5 to 8 weeks; the Russian 12-week interval of botulinum toxin type A; Turkish section 7.1, greater occipital nerve blocks once a week, four times, at first and then monthly: [S-035] "Başlangıçta haftalık 4 kez sonra aylık yapılması etkinliği artırmaktadır.", PDF p. 83; translation: "Performing it weekly, 4 times, at first and then monthly increases its efficacy."; Turkish section 7.3, longer intervals between botulinum toxin injections after one year in patients who benefit: [S-035] "Bir yılın sonunda ağrı sıklığı ve şiddetinde azalma gözlenen hastalarda uygulama süreleri uzatılabilir.", fifth item, PDF p. 86; translation: "In patients in whom a decrease in pain frequency and severity is observed at the end of one year, the application intervals may be extended."); stopping after success (NICE CG150 1.3.29, second clause; Turkish section 3.6.3.9); consultations scheduled from an earlier consultation (SIGN 155 patient checklist, after 2–8 and 6–8 weeks); and a re-evaluation left to the clinician in selected cases (EHF 2022 question 3, guidance text: "In selected cases decision on treatment maintenance can be readdressed after an additional period of 3 months."). The comment on anti-CGRP monoclonal antibodies in the Russian section 3.3 ([S-033] "Эффективность терапии следует оценивать через 3 мес. после ее начала.", p. 41; translation: "The efficacy of therapy should be assessed 3 months after its start.") names the time point of `ruleRu71` for these antibodies and adds no rule. A diary may show any further time point, for example of other guidance, as an `OtherItem`.

#### E-042/Q00
- Kind: Q
- Concerns: E-042
- Source: [S-005] — https://ihs-headache.org/wp-content/uploads/2025/04/Clinical-Trials-Controlled-trials-of-preventive-treatment-of-migraine-in-children-and-adolescents-1st-ed-CEP.pdf
- Source: [S-011] — https://pmc.ncbi.nlm.nih.gov/articles/PMC9188162/
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Text: Stage 1 OUT-018 (see E-041); Stage 1 OUT-001 for the 28-day (4-week) period. That the evaluated period ends with the interval of treatment the guidance names, not one day after it: Stage 1 OUT-001 and OUT-036, [S-005] "the final 28 days of the treatment period should be assessed"; Stage 1 OUT-018, [S-011] "after a minimum of 3 consecutive months on treatment" and [S-015] "after 12 weeks of treatment". That the time point is named for a course taken through that interval: the same Stage 1 OUT-018 quotes, and the other wordings of a duration of treatment quoted in E-041 (Notes, **Stop or pause**).

#### E-042/D01
- Kind: D
- Concerns: E-042
- Text (v34 Notes): **Stop or pause.** A course stopped or paused before the last day of the interval has no time point of the rule at that anchor date: the guidance names none for it (E-041 Notes, **Stop or pause**). Showing the time point with the comparison, or requiring a comparison "at" it whose on-treatment period then lies after the end of the course, would present the course as evaluated after the treatment interval the guidance names, as an adequate trial, while Stage 1 OUT-024 quotes the EHF consensus that "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed." ([S-013]). The comparison itself is still required for every started treatment (INV-055), with its periods after the treatment start as OUT-018 states them (INV-056), and a diary may state the stop next to it as an `OtherItem` (section 3.7). The post-stop monitoring view shows the periods after the stop (E-049).

#### E-042/W01
- Kind: W
- Concerns: E-042
- Text (v34 Meaning): For example, for an anti-CGRP monoclonal antibody started on 1 January 2026, the calendar month of March, the third consecutive month on treatment, ends at the 3-month time point, 1 April; and the final 28 days of the 12 weeks of treatment, 26 February to 25 March, end at the NICE CG150 1.3.28 time point, 26 March.

#### E-042/W02
- Kind: W
- Concerns: E-042
- Text (v34 Meaning): For example, an anti-CGRP monoclonal antibody started on 1 January 2026 and stopped on 10 February 2026, its last day on treatment, has not been taken through the interval of any of its time points (these intervals end on 28 February for Turkish Box 8, on 25 March for NICE CG150 1.3.28, and on 31 March for the 3-month time points), so none of them is shown or required (INV-055, INV-058, INV-059); stopped on 31 March, it keeps them all.

#### E-043/D01
- Kind: D
- Concerns: E-043
- Text (v34 Notes): `values`, `changes` and `timePoints` are references (section 2.5), and all three are shown in the comparison's view at MUST: the time points by the placement marker on `timePoints` (W2); the values because each refers to the baseline or an on-treatment period of the comparison (INV-056), which INV-003 places in the comparison's view, so that the value is part of that view (INV-003 Notes); and the changes because each is shown with the two values it compares (E-040 `reference`, `compared` (W2)). So the comparison is never shown apart from the values and changes that it shows (OUT-018: "showing both the values of each period and the absolute and percentage change from baseline"), wherever it is shown, for example with a responder label (INV-062) or as the treatment effect of the patient-facing overview (INV-105).

#### E-044/D01
- Kind: D
- Concerns: E-044
- Text (v34 Notes): "Per month" is represented by a monthly period, so no conversion formula is needed. The residual migraine days are shown next to every percentage change in migraine or headache days without the condition "for patients with migraine", as OUT-019 states them; see ISS-03.

#### E-045/Q00
- Kind: Q
- Concerns: E-045; SD-RC-01; SD-RC-02; SD-RC-03; SD-RC-04; SD-RC-05; SD-RC-06
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Source: [S-008] — https://ricerca.univaq.it/retrieve/b7f186a9-06ec-4e9c-b132-4f785bbeb121/puledda-et-al-2024-international-headache-society-global-practice-recommendations-for-preventive-pharmacological.pdf
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Source: [S-023] — https://pmc.ncbi.nlm.nih.gov/articles/PMC9607711/
- Source: [S-030] — http://dhos.dk/wp-content/uploads/2020/06/2932-Referenceprogram_2020_final_web-24.06.20.pdf
- Source: [S-032] — https://brainmed.com/guidance/detail/article/34408
- Source: [S-033] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=295_4
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Source: [S-042] — https://pmc.ncbi.nlm.nih.gov/articles/PMC12279330/
- Text: Stage 1 OUT-020 (criteria named: "NICE CG150 rec. 1.3.28", "IHS global practice recommendations Q6", "IHS position statement 2025 control levels"; thresholds of NICE 1.3.28 [S-015] "at least 50% in episodic migraine" and "at least 30% in chronic migraine"; IHS Q6 [S-008] "a ≥ 50% decrease in monthly migraine days or moderate-to-severe headache days" and the PGIC and MIDAS/HIT-6 items; DMKG/ÖKSG/SKG [S-023] "mindestens 50 %", "um mindestens 5 Punkte", "um mindestens 30 %"); Stage 1 OUT-018 (NICE 1.3.29 [S-015] "at least 30% after 2 treatment cycles"; Russian section 7.1 [S-033] "на 50% и более", Caveats naming these criteria). The other values on which criteria rest, beyond those OUT-020 gives as examples, in Stage 1 quotes: attack frequency and duration and the response to acute treatment ([S-035] section 3.6.2, Stage 1 OUT-011, OUT-021, OUT-023: "atak sıklığında ve süresinde %50'lik bir azalma ve akut atakta ilaçlara artan yanıt"); the frequency or intensity of migraine and bothersome side effects ([S-030], Stage 1 OUT-010: "hvis hyppigheden eller styrken af migræne kan halveres uden at der forekommer for generende bivirkninger"); attack duration ([S-042], Stage 1 OUT-011: "Significant decrease in attack duration based on patient’s headache diary"); attack duration or severity, the response to acute treatments, the ability to function and disability ([S-042] panel discussion, Stage 1 OUT-021, OUT-023); attack frequency, headache duration and severity, functional impairment and the response to acute treatment ([S-032] section 3.2, Stage 1 OUT-011, OUT-021). The day measures of the reduction components of the named criteria, in Stage 1 quotes, are measures of the person that no criterion restricts to the days of one headache type: "the frequency of migraines" ([S-015] 1.3.28, OUT-018, OUT-020), "the frequency of headache days per month" ([S-015] 1.3.29, OUT-018), "monthly migraine days or moderate-to-severe headache days" ([S-008] Q6, OUT-006, OUT-021), "die Migränetage" ([S-023], OUT-020) and "число дней с ГБ" ([S-033] section 7.1, OUT-018; the number of headache days); headache days are days "affected by headache" ([S-001], OUT-004). The frequency or intensity of [S-030] is restricted to one headache type: "hyppigheden eller styrken af migræne" (OUT-010; the frequency or intensity of migraine). Thresholds not quoted in Stage 1:

#### E-045/Q01
- Kind: Q
- Concerns: E-045; SD-RC-03
- Source: [S-008] — https://ricerca.univaq.it/retrieve/b7f186a9-06ec-4e9c-b132-4f785bbeb121/puledda-et-al-2024-international-headache-society-global-practice-recommendations-for-preventive-pharmacological.pdf
- Location: Q6, Recommendations, Optimal, p. 12
- Quote: "For patients with chronic migraine who have not achieved a ≥ 50% decrease in monthly migraine days or moderate-to-severe headache days with multiple preventive options (including oral drugs, onabotulinumtoxinA and drugs targeting the CGRP pathway), a ≥ 30% decrease in monthly migraine days or moderate-to-severe headache days is acceptable for treatment continuation beyond three months."

#### E-045/Q02
- Kind: Q
- Concerns: E-045; SD-RC-03
- Source: [S-008] — https://ricerca.univaq.it/retrieve/b7f186a9-06ec-4e9c-b132-4f785bbeb121/puledda-et-al-2024-international-headache-society-global-practice-recommendations-for-preventive-pharmacological.pdf
- Location: Q6, Evidence, p. 13
- Quote: "The clinically meaningful improvement in MIDAS score is defined by the AHS as i) reduction of ≥5 points for baseline score 11–20 or ii) reduction of ≥30% for baseline score ≥20. The clinically meaningful improvement in HIT-6 score is a reduction of ≥ 5 points (9)."

#### E-045/Q03
- Kind: Q
- Concerns: E-045
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Text: [S-035] "Ölçüt atak sıklığında en az %50 azalma olması" (section 3.6.2, Kutu 8 "Migren Profilaktik Tedavi-Yönetim-6", box headed "Farmakolojik Profilaktik Tedavide Yol Haritası", second item, PDF p. 48). Translation: "The criterion is a reduction of at least 50% in attack frequency" (a threshold on attack frequency, `attackReduction`; Notes)

#### E-045/Q04
- Kind: Q
- Concerns: E-045
- Source: [S-035] — https://noroloji.org.tr/TNDData/Uploads/files/Migren%20Klinik%20Protokol%c3%bc%20(Revizyon
- Text: [S-035] "Migren önleyici tedavi; migren ataklarının sıklığını, şiddetini ve süresini azaltmayı ve hastanın genel yaşam kalitesini iyileştirmeyi amaçlar." (section 3.3 "Farmakolojik Tedavi", item "b. Profilaksi", PDF p. 23). Translation: "Migraine preventive treatment aims to reduce the frequency, severity and duration of migraine attacks and to improve the patient's overall quality of life." (the attacks whose frequency the criterion of Box 8 counts are migraine attacks; Notes, **Type scope**)

#### E-045/D01
- Kind: D
- Concerns: E-045
- Text (v34 Meaning): `namedCriteria` are the criteria for judging an individual's response that the Stage 1 evidence of OUT-018 and OUT-020 names; the "50% responder rate" of [S-002] in OUT-018 is a trial endpoint over a population, which [S-003] and [S-005] (OUT-020) exclude from judging individuals, and is not among them.

#### E-045/D02
- Kind: D
- Concerns: E-045
- Text (v34 Notes): NICE 1.3.28 words its measure "frequency of migraines"; the model applies it to migraine days, the frequency measure of OUT-018.

#### E-045/D03
- Kind: D
- Concerns: E-045
- Text (v34 Notes): The IHS Q6 MIDAS ranges overlap at a baseline score of 20, as the source states them; either component may then apply.

#### E-045/D04
- Kind: D
- Concerns: E-045
- Text (v34 Notes): Each named criterion is a criterion of its guidance for the population that guidance addresses: all of them concern migraine, and `critRu71` is named for adults. The condition of a component (`anySubject` and the others) states only a further condition within that population.

#### E-045/D05
- Kind: D
- Concerns: E-045
- Text (v34 Notes): **Named criteria.** A label shows its criterion by its name, with its thresholds (E-046 `criterion`), and the thresholds of a named criterion are those of its source, quoted in the Evidence. So a criterion that a label shows under the name of a named criterion is that criterion (INV-116): it rests on the same values (`alsoRestsOn`), each of its components is a component of the named criterion, and it leaves out only components whose condition the label's treatment does not meet, for example the threshold "in chronic migraine" of NICE 1.3.28 on the label of a treatment given for episodic migraine. Such a component is never met and always decided for that label (`componentMet`, `componentDecided`, E-046) and asks for no value (INV-062), so leaving it out changes no category that INV-063 forces or admits and no value that INV-062 asks for. A criterion shown under any other name is not constrained: OUT-020 names criteria as examples ("for example"), and a label may apply any criterion (E-046). The names compared are those that this element states for the named criteria, as an instrument is shown by the name that E-057 states for it.

#### E-045/D06
- Kind: D
- Concerns: E-045
- Text (v34 Notes): **Conditions on the treatment.** The conditions are read on the treatment the label refers to (`conditionHolds(c, t, s)`): any treatment (`anySubject`); a treatment given for migraine but not for chronic migraine (`episodicMigraineOnly`, `givenFor`, E-008); a treatment given for chronic migraine (`chronicMigraineOnly`); or a treatment to which the IHS Q6 situation applies (`ihsQ6ChronicAlternativeOnly`). They are not read on the headache types the subject has had at any time (E-008), because a subject's migraine may be chronic at one time and episodic at another, and the criteria name the migraine for which the treatment is given and the treatment that is continued: NICE 1.3.28 sets one threshold "in episodic migraine" and one "in chronic migraine" for CGRP inhibitors, which NICE CG150 recommends "as options for preventing episodic or chronic migraine" ([S-015] 1.3.24, quoted in E-041); the DMKG/ÖKSG/SKG criterion judges a prophylaxis "Bei der episodischen Migräne (eM)" (Stage 1 OUT-020); and IHS Q6 accepts a ≥ 30 % decrease "for treatment continuation beyond three months" (Evidence). So a label of a treatment given for episodic migraine is decided under the episodic threshold even if the subject has had chronic migraine at another time, and a label of a treatment given for chronic migraine under the chronic threshold even if the subject's migraine has since become episodic. No invariant requires a responder label, or a named criterion, for any subject: a label is optional and names the criterion that a reader chooses to apply (OUT-018 Caveats, E-046), so the model requires no criterion for a subject outside its population.

#### E-045/D07
- Kind: D
- Concerns: E-045
- Text (v34 Notes): **Other values.** OUT-020 gives the results of instruments and of patient global impression of change and the effectiveness of acute treatment as examples ("for example") of the other values a criterion may rest on, so the kinds are open, and criteria quoted in Stage 1 rest on further values (Evidence): attack counts, intensity, duration, functional impact, the response to acute treatment before and on treatment, and adverse effects. `periodValuesOf` and `typeValuesOf` cover every kind of per-period value of the model on which a criterion can rest, over all headache types combined or for one headache type, and `otherValueNamed` a value of any other kind, for example the adverse effects of the treatment that [S-030] names, shown by the treatment line (E-055). Completeness indicators (E-013), which INV-011 shows with the period of every summary measure, marks of periods without migraine days (E-022), which restate a migraine-day count of 0, and cluster attack rates (E-064), which restate an attack count over a period within a bout (INV-089), are not kinds of their own; a criterion that rests on cluster attacks names the attack counts. `acuteTreatmentEffectiveness` asks for the effectiveness of each acute medication the subject has used, over all headache types combined, in each evaluated period, which the optimal-control level of [S-010] uses ("for three months, with a satisfactory response to acute treatment"); a criterion that rests on a change in the response to acute treatment ([S-032], [S-035], [S-042]) names `periodValuesOf(acuteTreatmentSummaries)`, which asks for a summary of each acute medication for the baseline period as well (INV-062). The results of an instrument on which a criterion rests include the result at the evaluation, where one is available (INV-062).

#### E-045/D08
- Kind: D
- Concerns: E-045
- Text (v34 Notes): **Thresholds on attacks, intensity and duration.** A threshold on attack frequency is a component of its own (`attackReduction`), decided on the attack counts that the label shows of the headache types whose attacks it counts (E-046, INV-063), for example the criterion of the Turkish protocol, Box 8 (Evidence), which counts migraine attacks (`headacheType = {c1}`): the item of Box 8 names the attack frequency ("atak sıklığında"), and the same protocol states that preventive treatment of migraine aims to reduce the frequency of migraine attacks ("migren ataklarının sıklığını", Evidence). A threshold on intensity or duration is a `judgement` component: the criteria quoted name no statistic, scale or form of summary on which a shown value could be tested (a halving of intensity, [S-030]; a 50 % reduction in attack duration, [S-035]; a significant decrease in attack duration, [S-042]), while an intensity or duration summary has several forms and statistics (E-023, E-024). A criterion whose parts must all be met is one `judgement` component, because the components of a criterion are alternatives: for example [S-035] section 3.6.2 (a 50 % reduction in attack frequency and duration and an increased response to acute treatment) or [S-030] (frequency or intensity halved without bothersome side effects). The values it rests on are listed in `alsoRestsOn`, so that INV-062 asks for them with the label.

#### E-045/D09
- Kind: D
- Concerns: E-045
- Text (v34 Notes): **Type scope.** Each component is decided only on values of the headache types its measure refers to (E-046), never on values of another type scope. The day measures of a reduction component are counted over all headache types combined (`allTypes`): each named criterion names a day measure of the person that it does not restrict to the days of one headache type (Evidence), and the measure itself states which days it counts (headache days and moderate/severe headache days are days with headache of any type; migraine days are days with migraine under the definition the view names). This is also the scope at which the response comparison shows its own values (INV-056, INV-057) and at which the control levels are read (`levelDays`, E-046). A criterion whose day measure is restricted to the days of one headache type, as none of the named criteria is, is a `judgement` component that names the values of that type with `typeValuesOf`. An attack count has no headache type of its own (E-019, the "frequency of attacks" of ICHD-3), so an attack-reduction component names the headache type whose attacks it counts, or none for the attacks of all types combined; the attack criterion of the evidence, Turkish Box 8, counts migraine attacks (Evidence). A criterion that rests on per-period values of one headache type, for example the frequency or intensity of migraine of [S-030] (Evidence), names them with `typeValuesOf`; `periodValuesOf` names values over all types combined. The values of one headache type are those in the scope `scopeFor` (E-012): over all types combined where the subject has a headache type and every headache type it has or may have falls under that type, and otherwise in the scope of the type itself. So the values of a single headache type of a subject who also has, or may have, another type never meet or decide a component whose measure covers all types, and values over all types never meet or decide a component that counts the attacks of one type of such a subject; the reader applies the named criterion to the values shown (INV-062).

#### E-045/N01
- Kind: N
- Concerns: E-045
- Text (v34 Notes): The second clause of NICE 1.3.29 ("or if their condition has changed to episodic migraine for 3 consecutive months") is a reason to stop after success, not a response criterion, and is not modelled.

#### E-045/N02
- Kind: N
- Concerns: E-045
- Text (v34 Notes): The scheme criteria of OUT-025 (Kela, AIFA, Poland, Zorgverzekeraars Nederland) are not responder criteria of this element; OUT-025 Caveats state that they are not requirements.

#### E-046/Q01
- Kind: Q
- Concerns: E-046; SD-RC-04; SD-CL-01
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Location: section "Setting goals of migraine burden while on treatment", p. 6
- Quote: "Migraine Freedom. This is defined as the complete elimination of days with migraine or moderate-to-severe headache, ideally over a period of three months."

#### E-046/Q02
- Kind: Q
- Concerns: E-046; SD-RC-04; SD-CL-02
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Location: same section, p. 6
- Quote: "Optimal Control. This is defined as less than four days with migraine or moderate-to-severe headache per month for three months, with a satisfactory response to acute treatment, defined as pain-freedom within two hours from the intake."

#### E-046/Q03
- Kind: Q
- Concerns: E-046; SD-RC-04; SD-CL-03
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Location: same section, p. 6
- Quote: "Modest Control. This is defined as four to six days with migraine or moderate-to-severe headache per month."

#### E-046/Q04
- Kind: Q
- Concerns: E-046; SD-RC-04; SD-CL-04
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Location: same section, p. 6; in the PDF text layer the running header "Cephalalgia 45(2)" interrupts the sentence after "per", at a column break
- Quote: "Insufficient Control. This is defined as more than six days with migraine or moderate-to-severe headache per month."

#### E-046/Q05
- Kind: Q
- Concerns: E-046; SD-RC-04; SD-CL-04
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Location: same section, p. 6
- Quote: "In some cases, insufficient control may be present when there are less than six MMDs, especially when attacks are associated with very high levels of disabling symptoms"

#### E-046/D01
- Kind: D
- Concerns: E-046
- Text (v34 Notes): A label may refer to several on-treatment periods (for example the three months of optimal control). For a reduction component, the cited criteria do not state how several months are combined (at a time point, on their mean, in every month, or in a share of the months). The reduction relations therefore decide only a label with a single evaluated period (`#L.evaluated = 1`). For a label over several periods, a reduction component is not decided by the values shown, as for a judgement component, and the reader applies the named criterion to the values shown with the label (INV-062).

#### E-046/D02
- Kind: D
- Concerns: E-046
- Text (v34 Notes): Every component is evaluated on values of the label's own treatment, of the periods the label refers to and of the headache types its measure refers to (E-045 Notes, **Type scope**). The periods of these values are matched with the periods the label refers to, and with the baseline of its response comparison, by their dates (`sameSpan`), so that a value shown for one of these periods decides a component whichever period atom with those dates it refers to, as the control levels are read (`levelDays`, `daysOf`, E-014); a view shows one value per measure, period dates and scope (INV-006). A reduction component is tested only on a change of the response comparison of the label's treatment (`rc.treatment = L.treatment`) over all headache types combined (`ch.reference.typeScope = allTypes`), the scope of the day measures of every named criterion and of the comparison's own values (INV-056, INV-057). A change for a single headache type, or attack counts of another scope than the one the component counts, therefore neither meet nor decide a component. Otherwise, in a subject who also has another headache type, they could force a category that the named criterion, applied to the measure it names, does not give: for example, under a criterion on headache days with a 50 % threshold, a 60 % fall in the headache days of tension-type headache next to a 30 % fall in the person's headache days would force "responder". The reader applies the named criterion to such values (INV-062).

#### E-046/D03
- Kind: D
- Concerns: E-046
- Text (v34 Notes): A score component is a criterion of response to the preventive treatment: IHS Q6 names success criteria "that determine whether preventive therapy is effective" (Stage 1 OUT-020, [S-008]) and measures the MIDAS improvement from the "baseline score" (E-045), and DMKG/ÖKSG/SKG judges the prophylaxis effective if the impairment "sinkt" (falls) by the threshold (Stage 1 OUT-020, [S-023]). A score component is therefore tested only on the pair that the criterion compares: the score at the evaluation, which the model reads as the latest result of the instrument completed after the treatment start within the last period the label refers to (`evaluationResult`), and the pre-treatment baseline score, which the model reads as the latest result of the instrument completed on or before the treatment start (`pretreatmentBaseline`); the result shows the baseline result as its baseline administration (E-058). Both dates are compared with the treatment start shown in the label's response comparison, and the result's date with the last evaluated period; all are output elements, and "available" refers to the subject's available results (section 3.5), as in INV-081 and INV-082. A pair of pre-treatment results, a baseline result that is not the latest one before the start, or a result outside the last evaluated period decides nothing, so a change between two administrations before the treatment, or one measured from an older baseline, can neither force nor exclude a label; the reader applies the named criterion to the results shown (INV-062). Reading the evaluation score as the result within the last evaluated period is the model's; the cited criteria name the baseline score and the evaluation of the preventive therapy, but no administration dates.

#### E-046/D04
- Kind: D
- Concerns: E-046
- Text (v34 Notes): The control-level labels are exactly the four level names of [S-010]; "per month" is read as applying to each evaluated monthly period. The control levels are goals for the migraine burden while on treatment ([S-010] section "Setting goals of migraine burden while on treatment"), so the months a control-level label evaluates begin on or after the start of the label's treatment (where the context states no start, on or after a dated course event of it, `courseBegunBy`, E-008) and end on or before the date of every stop or pause of it, the last day of the course (`evaluatedOnTreatment`; INV-064).

#### E-046/D05
- Kind: D
- Concerns: E-046
- Text (v34 Notes): **After a stop or pause.** The named criteria judge the response to the treatment over the time on treatment: NICE 1.3.28 stops a CGRP inhibitor "after 12 weeks of treatment" ([S-015], Stage 1 OUT-018 and OUT-020), IHS Q6 names the criteria that determine "whether preventive therapy is effective and should be continued" ([S-008], Stage 1 OUT-020), and the Russian section 7.1 judges the reduction "через 3 месяца терапии" (after 3 months of therapy; [S-033], Stage 1 OUT-018). A responder or non-responder label that refers to a period ending after a stop or pause of its treatment (`evaluatedOnTreatment` false) is therefore decided by no component (INV-063): the values of such a period neither force nor exclude a category, and the reader applies the named criterion to the values shown (INV-062), as for a label over several periods.

#### E-046/D06
- Kind: D
- Concerns: E-046
- Text (v34 Notes): Because [S-010] allows insufficient control with fewer than six migraine days, the model does not require more than six days for that level.

#### E-047/D01
- Kind: D
- Concerns: E-047
- Text (v34 Notes): Stage 1 fixes no measure of adherence. The proportion of prescribed intake is the natural numeric form; `otherAdherenceStatement` keeps the form open.

#### E-047/D02
- Kind: D
- Concerns: E-047
- Text (v34 Notes): **The evaluation window.** OUT-039 asks for adherence "over the evaluation window, next to the response comparison of OUT-018, so that a reader can see whether an apparent lack of effect coincided with inconsistent intake". The window therefore covers an on-treatment period whose values the comparison evaluates: it contains that period and ends with it (`adherenceFor`). It may also begin earlier, as early as the treatment start, so that it can be the evaluated period itself or the time on treatment up to the end of that period, which the Stage 1 quotes of OUT-039 name ([S-018] "If no efficacy is observed after 8–12 weeks of treatment"); Stage 1 does not decide between the two, and both meet `adherenceFor`. A window of a few days at the end of the evaluated period does not show the intake over that period, and does not meet it. Stage 1 names one evaluation window next to the comparison, so `adherenceFor` asks for one on-treatment period, not for each.

#### E-048/D01
- Kind: D
- Concerns: E-048
- Text (v34 Notes): The patient's own goals are what the reader brings to the view; Stage 1 does not ask the output to show them. The on-treatment periods lie within the course: they begin on or after the treatment start and end on or before every stop or pause of the treatment, the last day of its course (INV-068; section 2.8). A treatment review view is shown only for a treatment whose start the context states (INV-068), as a response comparison is (INV-123): where the context states no start, for example for a treatment that the subject was already taking, no period can be placed before the start, and a period shown as the pre-treatment baseline could be a month on treatment (INV-068/W01).

#### E-049/D01
- Kind: D
- Concerns: E-049
- Text (v34 Notes): **Resumed treatment.** For a course that resumes the treatment of an earlier course (`resumes`, E-008), the original pre-treatment baseline lies before the start of the first course of the chain (`originalStart`), not before the restart. The on-treatment period stays within the course of the event, as before: OUT-022 qualifies only the baseline as "original", and the period on treatment before the change is that of the course which the event stops, pauses or reduces; so the `when` clause of `onTreatmentPeriod` and `firstChangedDay` are those of the course. For a course that resumes no course, the original start is its own start.

#### E-049/D02
- Kind: D
- Concerns: E-049
- Text (v34 Notes): **Original start not stated.** Where the context states no start for the first course of the chain, `originalStart` is empty, and no baseline is asked for or admitted (the `when` clause of `baseline`; INV-112). The context does not place the original start, so no period of the output can be shown to lie before it, and a period shown as the original baseline could be a month of the pause or on treatment, which could hide the worsening or rebound above baseline that OUT-022 is to make visible. The same holds for the view of a stop, pause or reduction of a course whose own start the context does not state, which resumes no course (INV-001). So the model asks for the original pre-treatment baseline where the context states the original start, as it asks for the other content aligned to a start where the context states that start (INV-055, INV-056, INV-068, INV-102; E-055 Notes).

#### E-049/D03
- Kind: D
- Concerns: E-049
- Text (v34 Notes): **Course start not stated.** The view itself, its periods after the event and its on-treatment period are aligned to the event, not to the start: the periods after the event begin on `firstChangedDay`, which the kind and date of the event fix, and the on-treatment period is a period of the course before the changed regimen. So the view is asked for after every stop, pause or reduction of a preventive course, whether or not the context states the start of the course (INV-103). Where the context states no start for the view's own course, the course began on a day the context does not state, on or before its first dated course event (E-008 Notes), and the on-treatment period begins on or after a dated course event of the course (`courseBegunBy`) and ends before the first changed day (INV-112). It is asked for whenever a course event of the course is dated before the changed regimen: for every stop or pause, whose date is the last day of the course, and for a reduction that another dated course event precedes (INV-070).

#### E-049/D04
- Kind: D
- Concerns: E-049
- Text: The `when` clause of `onTreatmentPeriod` has two disjuncts. The first is the v34 clause, verbatim: the context states the start of the course, and the start precedes the first changed day. The second is the presence condition of v34 INV-070 for a course whose start the context does not state, with its `∀ x` over `firstChangedDay` written `∃ x`; `firstChangedDay` has at most one value, so the two are equivalent. Oscillation check 28 allows this move (watch point 1: "Not a reversal: moving the ask from INV-070 into the E-049 `when` clause as a disjunct for unstated starts only, provided the stated-start cases stay as they are"; watch point 5). R-MCF (2).

#### E-049/W01
- Kind: W
- Concerns: E-049
- Text (v34 Notes): For example, for a treatment started on 1 January 2026, paused on 30 June 2026, its last day on treatment, and restarted as a new course on 1 September after migraine worsened ([S-011], Stage 1 OUT-022) and reduced on 1 October, the view of the reduction compares the periods from 1 October with an on-treatment period in September, on the resumed course, and with a baseline period that ends before 1 January 2026, for example December 2025 (INV-070, INV-112). August 2026, a month of the interval off treatment, is not the original pre-treatment baseline: it lies after the treatment was first started, in the time in which migraine worsened after the withdrawal, and a comparison with it could hide the worsening or rebound above baseline that OUT-022 is to make visible.

#### E-049/W02
- Kind: W
- Concerns: E-049
- Text (v34 Notes): For example, for a treatment that the subject was already taking, whose start the context does not state, reduced on 15 March 2026, paused on 30 June 2026 and restarted as a new course on 1 September, the view of a reduction of the resumed course on 1 October shows the periods from 1 October and an on-treatment period in September, and no baseline: August 2026 lies in the interval off treatment, May 2026 on the first course, and a month before 15 March, such as February 2026, on the first course at its earlier dose or before that course began, the context not saying which.

#### E-049/W03
- Kind: W
- Concerns: E-049
- Text (v34 Notes): For example, for a treatment that the subject was already taking, reduced on 15 March 2026 and paused on 30 June 2026, its last day on treatment, the view of the pause shows the periods from 1 July and an on-treatment period within 15 March to 30 June, for example June 2026; August 2026, after the pause, and February 2026, before the first dated course event, are not admitted as the on-treatment period. The view of the reduction of 15 March shows the periods from 15 March and no on-treatment period, because no course event of the treatment is dated before the reduction, so the context places no earlier day on treatment. Neither view shows a baseline (above).

#### E-050/D01
- Kind: D
- Concerns: E-050
- Text (v34 Notes): Pain freedom and headache relief are shown side by side; the output does not itself decide which definition of response applies (OUT-023 Caveats, INV-119 (C2-07)).

#### E-051/D01
- Kind: D
- Concerns: E-051
- Text (v34 Notes): **Formulation of a required summary.** OUT-023 reports the outcomes "For each acute medication, [...] across the attacks treated with it", speaks of "per-drug outcomes", and asks that these "be shown separately for each formulation of the same drug, so that a non-response to one formulation is not read as a non-response to the drug". In the model an acute medication is a drug and a formulation (E-008), so the summaries that other requirements take from OUT-023 can be read in two ways: per drug, as a summary of all formulations of the drug; or per drug and formulation, as a summary of each formulation the subject has used. `summarisesMedication` is implied by both readings and decides neither: under either, the attacks treated with every formulation that the subject has used are in a summary shown, so a summary of one formulation does not stand in for another formulation of the same drug, and a summary of a formulation the subject never used stands in for none. A summary of all formulations names every formulation of the drug that the subject has used (INV-072), and one of a single formulation lists only attacks treated with it (INV-074). Every attack line shows a drug, and a formulation, in which the subject has used it (INV-123), as the formulations of an acute treatment line do (INV-123); a summary itself may name a formulation that the subject has never used, with 0 treated attacks, which shows that the formulation was not tried and states no use of it. For the selected time range, INV-071 asks for both presentations. The question is one of the model's representation of an acute medication, not a defect of Stage 1, whose statement asks for both the per-drug outcomes and their separate presentation per formulation.

#### E-054/D01
- Kind: D
- Concerns: E-054
- Text (v34 Notes): `DrugClass` is a given set because Stage 1 names no class system for preventive drugs.

#### E-055/D01
- Kind: D
- Concerns: E-055
- Text (v34 Notes): Every course event lies on or before the as-of date (INV-001), so whether a treatment has stopped is judged as of that date, and the duration of a treatment that has not stopped runs to it; the period the history view covers need not contain the treatment's start, because the history lists every treatment (INV-077).

#### E-055/D02
- Kind: D
- Concerns: E-055
- Text (v34 Notes): The stop reasons name the failure modes of the OUT-024 rationale (lack of efficacy, adverse effects); `otherStopReason` keeps the list open.

#### E-056/D01
- Kind: D
- Concerns: E-056
- Text (v34 Notes): Scheme criteria are not shown as requirements of the model (OUT-025 Caveats).

#### E-057/Q00
- Kind: Q
- Concerns: E-057; SD-IN-02; SD-IN-05; SD-IN-06; SD-IN-08
- Source: [S-002] — https://ihs-headache.org/wp-content/uploads/2025/04/Clinical-Trials-Controlled-trials-of-preventive-treatment-of-migraine-attacks-in-episodic-migraine-in-adults-CEP.pdf
- Source: [S-005] — https://ihs-headache.org/wp-content/uploads/2025/04/Clinical-Trials-Controlled-trials-of-preventive-treatment-of-migraine-in-children-and-adolescents-1st-ed-CEP.pdf
- Source: [S-014] — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Text: Stage 1 OUT-026 (recall periods of HIT-6 "1-month recall period" and MIDAS "3-month recall period" [S-002]; HURT "no concern" and three flagged areas, and "Grading is not used by HALT-30" [S-014]), OUT-036 (PedMIDAS "over the previous 3 months" [S-005]). Details not stated in Stage 1:

#### E-057/Q01
- Kind: Q
- Concerns: E-057; SD-IN-02
- Source: [S-101] — https://pmc.ncbi.nlm.nih.gov/articles/PMC3057423/
- Location: Methods, "Data sources", HIT-6 paragraph; the omitted words describe how the score is obtained
- Quote: "[...] ranges between 36 and 78, with larger scores reflecting greater impact"

#### E-057/Q02
- Kind: Q
- Concerns: E-057; SD-IN-02; SD-GB-05; SD-GB-06; SD-GB-07; SD-GB-08
- Source: [S-101] — https://pmc.ncbi.nlm.nih.gov/articles/PMC3057423/
- Location: Methods, "Data sources", HIT-6 paragraph
- Quote: "The four headache impact severity categories are little or no impact (49 or less), some impact (50–55), substantial impact (56–59), and severe impact (60–78)."

#### E-057/Q03
- Kind: Q
- Concerns: E-057; SD-IN-01; SD-GB-01; SD-GB-02; SD-GB-03; SD-GB-04
- Source: [S-102] — https://pmc.ncbi.nlm.nih.gov/articles/PMC4406925/
- Location: Methods, section "Migraine-related disability"
- Quote: "[...] four grades based on total days of impaired functioning (i.e., Grade I or little or no disability, 0 to 5; Grade II or mild disability, 6 to 10; Grade III or moderate disability, 11 to 20; Grade IV or severe disability, ≥21, with an option of dividing Grade IV into IVA and IVB)."

#### E-057/Q04
- Kind: Q
- Concerns: E-057; SD-IN-01
- Source: [S-102] — https://pmc.ncbi.nlm.nih.gov/articles/PMC4406925/
- Location: same section, the sentence after the grades
- Quote: "The recall period for the MIDAS is three months"

#### E-057/Q05
- Kind: Q
- Concerns: E-057; SD-IN-08; SD-GB-09; SD-GB-10; SD-GB-11; SD-GB-12
- Source: [S-103] — https://www.cincinnatichildrens.org/service/h/headache-center/pedmidas
- Text: [S-103] "The PedMIDAS grading scale is as follows:" followed by the table rows "0 to 10" "Little to none", "11 to 30" "Mild", "31 to 50" "Moderate" and "Greater than 50" "Severe" under the headings "PedMIDAS Score Range" and "Disability Grade" (section "PedMIDAS Grading Scale")

#### E-057/Q06
- Kind: Q
- Concerns: E-057; SD-IN-04
- Source: [S-014] — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Location: section "The Headache-Attributed Lost Time (HALT) Indices", paragraph beginning "There are three versions of HALT"; quoted from the Europe PMC full text, where figure references are rendered with spaces
- Quote: "HALT-90 (Fig. 3 (also, Additional file 18 )) counts days affected by headache during the preceding 3 months (90 days)."

#### E-057/Q07
- Kind: Q
- Concerns: E-057; SD-IN-05
- Source: [S-014] — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Location: same paragraph
- Quote: "HALT-30 (Fig. 4 (also, Additional file 19 )) accordingly records days affected during the preceding 1 month (30 days)."

#### E-057/Q08
- Kind: Q
- Concerns: E-057; SD-IN-04; SD-IN-05
- Source: [S-014] — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Location: subsection "Scoring HALT", first sentence
- Quote: "the unit of each being whole days per one or 3 months"

#### E-057/Q09
- Kind: Q
- Concerns: E-057; SD-IN-04; SD-GB-13; SD-GB-14; SD-GB-15; SD-GB-16
- Source: [S-014] — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Text: [S-014] Table 18 "Grading of HALT-90", columns "Days lost in last 3 months", "Assessed impact" and "Grade (indicating increasing need for medical care)", rows "0–5" "Minimal or infrequent" "I", "6–10" "Mild or infrequent" "II", "11–20" "Moderate" "III (indicates high need for care)" and "≥20" "Severe" "IV (indicates high need for care)" (subsection "Scoring HALT")

#### E-057/Q10
- Kind: Q
- Concerns: E-057; SD-IN-01; SD-IN-02; SD-IN-04; SD-IN-05; SD-IN-08
- Source: [S-014] — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Source: [S-101] — https://pmc.ncbi.nlm.nih.gov/articles/PMC3057423/
- Source: [S-102] — https://pmc.ncbi.nlm.nih.gov/articles/PMC4406925/
- Source: [S-103] — https://www.cincinnatichildrens.org/service/h/headache-center/pedmidas
- Text: Whole-number scores (`wholeNumberScores`), from the quotes above: the MIDAS grades rest on "total days of impaired functioning" [S-102], and the HALT unit is "whole days per one or 3 months" [S-014]; the published bands of MIDAS [S-102], HIT-6 [S-101], PedMIDAS [S-103] and HALT-90 [S-014] have consecutive whole-number limits (for example 0 to 5 and 6 to 10 for MIDAS, 49 or less and 50–55 for HIT-6, 0 to 10 and 11 to 30 for PedMIDAS), so the categories that these sources define over the score range cover it only for whole-number scores.

#### E-057/D01
- Kind: D
- Concerns: E-057
- Text (v34 Notes): MIDAS grade labels differ between publications of the MIDAS developers (for example "minimal or infrequent disability" in other papers); the model uses the labels of [S-102] and the same score bands.

#### E-057/D02
- Kind: D
- Concerns: E-057
- Text (v34 Notes): The HALT-90 bands of [S-014] overlap at 20 ("11–20" and "≥20"), as also printed in the HALT developers' 2018 paper; at a score of 20 either grade III or IV satisfies the relation.

#### E-057/D03
- Kind: D
- Concerns: E-057
- Text (v34 Notes): The lower bound 0 of MIDAS, PedMIDAS and HALT-90 follows from their lowest band, and that of HALT-30, which has no grading ("Grading is not used by HALT-30" [S-014]), from the unit of its summed scores, "whole days per one or 3 months" [S-014], because a number of days is not negative.

#### E-057/D04
- Kind: D
- Concerns: E-057
- Text (v34 Notes): The total scores of MIDAS, PedMIDAS, HALT-90, HALT-30 and HIT-6 are whole numbers (`wholeNumberScores`, INV-082); source sentences that describe how a total is obtained from the answers are not quoted, because that derivation is out of scope.

#### E-057/D05
- Kind: D
- Concerns: E-057
- Text (v34 Notes): `publishedGrading` is fixed by the model only where a cited source states the grading: MIDAS [S-102], HIT-6 [S-101], PedMIDAS [S-103] and HALT-90 [S-014] (graded), HURT (graded areas) and HALT-30 (no grading) by the Stage 1 [S-014] quotes of OUT-026. It is not fixed for MSQ v2.1, M-TOQ, PGIC and other instruments (`otherInstrument`); it follows those instruments' own publications, which the model does not tabulate. It decides both whether a result is asked for a grade or category (E-058) and whether it may show one (INV-082), so that a HALT-30 result shows none.

#### E-057/D06
- Kind: D
- Concerns: E-057
- Text (v34 Notes): PGIC in particular exists in several versions with different wordings (search log, section 3 of this file), and no source verified in Stage 2 defines its response categories, so whether a PGIC result shows a category follows the version used.

#### E-057/D07
- Kind: D
- Concerns: E-057
- Text (v34 Notes): The value-set functions `publishedRecall`, `scoreRange` and `gradeBands` are defined only for the tabulated instruments, so INV-082 and INV-123 constrain the results of other instruments only by the availability of a result of the instrument (INV-123), their dates, their baseline administration, their change from baseline and the form of their category (a published category, not a tabulated band), which they show only where the instrument has a published grading or categories (`publishedGrading`).

#### E-057/N01
- Kind: N
- Concerns: E-057
- Text (v34 Notes): The scoring of every instrument from its answers is out of scope.

#### E-058/D01
- Kind: D
- Concerns: E-058
- Text (v34 Notes): The output reports results and their change; it does not make MIDAS or HIT-6 a criterion of efficacy (OUT-026 Caveats), except where a named responder criterion that the reader applies uses them (E-045).

#### E-059/Q01
- Kind: Q
- Concerns: E-059; SD-SR-01; SD-SR-02
- Source: [S-104] — https://pmc.ncbi.nlm.nih.gov/articles/PMC183845/
- Location: section "Construction of the Hospital Anxiety And Depression Scale (HADS)"; the omitted words describe how the scores are obtained
- Quote: "[...] the possible scores ranged from 0 to 21 for anxiety and 0 to 21 for depression."

#### E-059/Q02
- Kind: Q
- Concerns: E-059; SD-SR-03
- Source: [S-105] — https://manual.jointcommission.org/pub/BHCInstruments/RomInstr00054/instructions_PHQ.pdf
- Location: section "Use of some screeners as severity and outcome measures", P. 6/9
- Quote: "PHQ-9 total score for the nine items ranges from 0 to 27."

#### E-059/Q03
- Kind: Q
- Concerns: E-059; SD-SR-04
- Source: [S-105] — https://manual.jointcommission.org/pub/BHCInstruments/RomInstr00054/instructions_PHQ.pdf
- Location: same section, P. 6/9
- Quote: "GAD-7 total score for the seven items ranges from 0 to 21."

#### E-059/D01
- Kind: D
- Concerns: E-059
- Text (v34 Notes): Stage 1 asks for the score only; severity categories of these instruments are not part of the output and are not stated. An instrument shown under another name is not one of HADS, PHQ-9 and GAD-7 (`OtherScreeningName`), so a result of these three is always subject to the ranges of INV-085.

#### E-060/Q01
- Kind: Q
- Concerns: E-060; SD-FX-01; SD-FX-02
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: [S-001] "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)" (A1.1.1 Pure menstrual migraine without aura, diagnostic criterion B, p. 190; the "±" and "−" signs are glyphs without a text mapping in the PDF text layer); the same window appears in A1.1.2 criterion B ("Occurring on day 1 ± 2 (i.e. days −2 to +3)", p. 190)

#### E-060/Q02
- Kind: Q
- Concerns: E-060; SD-FX-01; SD-FX-02
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: A1.1.1, note 2, p. 190; the text layer breaks "preceding" at a line end
- Quote: "The first day of menstruation is day 1 and the preceding day is day −1; there is no day 0."

#### E-060/D01
- Kind: D
- Concerns: E-060
- Text (v34 Notes): Reading "complete cycles the view covers" as cycles that have ended and lie wholly within the covered period is the model's; a cycle that began before the covered period, or ends after it, is shown but not counted, and a lead-in is never counted.

#### E-060/D02
- Kind: D
- Concerns: E-060
- Text (v34 Notes): A lead-in rests on the summarised diary information, as every value of the view does: it states that this information gives no first day of menstruation for its days. It therefore represents a covered period that begins before the subject's first menstruation, or before the first menstruation for which the diary information gives a first day, without a false date, as a lower day count represents missing diary days (E-032/D03). It cannot remove a cycle from the view: it lies only at the start of the covered period, it ends before the earliest day 1 that the output shows, and every later line shows its day 1.

#### E-060/D03
- Kind: D
- Concerns: E-060
- Text (v34 Notes): A prospective diary is not mandatory for the clinical diagnosis of A1.1.1 and A1.1.2 (OUT-030 Caveats); the view states no diagnosis.

#### E-060/N01
- Kind: N
- Concerns: E-060
- Text (v34 Notes): Only the window of the criterion is shown; the frequency criterion ("in at least two out of three menstrual cycles") is a diagnostic criterion and is not applied by the view.

#### E-061/D01
- Kind: D
- Concerns: E-061
- Text (v34 Notes): An attack in a lead-in is therefore in the window only on days −2 and −1 of the earliest day 1 that the view shows.

#### E-061/D02
- Kind: D
- Concerns: E-061
- Text (v34 Notes): The mark states nothing about the window of a menstruation whose first day the view does not show. In every view, an attack mark shows the attack as in the perimenstrual window exactly when its onset lies in the window of a menstruation whose first day the view shows (as the day 1 of a line, or as the day after a line that has ended; INV-124). The exception is an attack on a line that has not ended: its mark states nothing about a menstruation that begins after the line's last day.

#### E-062/D01
- Kind: D
- Concerns: E-062
- Text (v34 Notes): Attack frequency may decrease at the end of a bout, so such changes are not treatment effects (OUT-031 Caveats); the model adds no annotation for this because Stage 1 does not ask the output to state it. A remission period that shows its start date is an attack-free period of more than three months, as the ICHD-3 Definitions of terms require (E-063, INV-089); every fully conformant output shows the start date (E-063 `start`, SHOULD). The length is that of the whole attack-free period, to its end or, while it has not ended by the as-of date, to the as-of date, not that of its part within the period the view covers (E-063/D01); so a view of a past period shows a remission period that overlaps it and has exceeded three months by the as-of date. Attack-free periods of three months or less, among them those that ICHD-3 3.1.2 Chronic cluster headache calls remissions, are not shown as remission periods that show their start date; see ISS-12.

#### E-062/X01
- Kind: X
- Concerns: E-062
- Text: Rejected alternative (CA-09 of the consistency audit of v34): placement markers `shown SHOULD` on the cluster view's `bouts`, `remissions` and `rates`. Fix 11 declined such a placement ("OUT-031 lists what to report … without asking for one view"), and review 24 kept it; no new evidence shows fix 11 wrong. v35 keeps the references unplaced, and the Reading of INV-088 says that the view refers to them. INV-011 asks for completeness where phase items are in the view's content.

#### E-063/Q01
- Kind: Q
- Concerns: E-063; SD-FX-07
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: Definitions of terms, Cluster remission period, p. 209
- Quote: "To be considered a remission, the attack-free period must exceed three months."

#### E-063/D01
- Kind: D
- Concerns: E-063
- Text (v34 Notes): **Time frame.** Whether a period has ended is judged as of the as-of date, as whether a treatment has stopped (E-055, INV-079), and as a cycle line that has ended is shown to the day before the next first day of menstruation also when that day lies after the covered period (E-060): every period is shown with its own dates and duration, whatever period the view covers. A period that began before the covered period is shown with its start, one that ended after the covered period with its end, and one that has not ended by the as-of date with its duration to date (`lastDay`). So the duration bound of a remission period is tested on the length of the attack-free period itself, to its end or, while it continues, to the as-of date, not on its part within the covered period, and a remission period that the ICHD-3 Definitions of terms recognise as of the as-of date can be shown in a view of any covered period that it overlaps. The duration bound is that of the ICHD-3 Definitions of terms, whose definition of the cluster remission period Stage 1 quotes for OUT-031 ("using the ICHD-3 definitions"). ICHD-3 words the duration of a remission differently for 3.1.1 Episodic cluster headache (remission periods of at least three months) and for 3.1.2 Chronic cluster headache (remissions lasting less than three months), so an attack-free period of three months or less is not shown as a remission period that shows its start date, also where 3.1.2 calls it a remission; the time between two bouts that the view shows is visible from the end date of the one and the start date of the next.

#### E-063/N01
- Kind: N
- Concerns: E-063
- Text (v34 Notes): The output shows the start, end and duration of each remission period it shows, but not the ICHD-3 element "cannot be induced with alcohol or nitroglycerine" (OUT-031 Caveats).

#### E-063/W01
- Kind: W
- Concerns: E-063
- Text (v34 Notes): For example, in a cluster view of 1 January – 31 July 2026 with the as-of date 21 October 2026, a bout from 10 July to 20 August 2026 is shown with its end date and its duration of 42 days; and, for a subject whose last bout ended on 31 May 2026, the attack-free period from 1 June 2026 that continues on the as-of date (143 days) is shown in such a view as an ongoing remission period.

#### E-064/Q00
- Kind: Q
- Concerns: E-064
- Source: [S-007] — https://discovery.ucl.ac.uk/id/eprint/10161405/2/Matharu_IHS%20Guidelines%20for%20Clinical%20Trials%20in%20Cluster%20Headache.pdf
- Text: Stage 1 OUT-031 ("attacks per day and per week during active periods"; [S-007] "Number of attacks per day during the study period" and "the number of weekly attacks for the entire double-blind phase", both rates over a period longer than one day or one week). Not quoted in Stage 1:

#### E-064/Q01
- Kind: Q
- Concerns: E-064
- Source: [S-007] — https://discovery.ucl.ac.uk/id/eprint/10161405/2/Matharu_IHS%20Guidelines%20for%20Clinical%20Trials%20in%20Cluster%20Headache.pdf
- Location: section 2.2 "Specific patient populations and attack characteristics", Recommendations, item a, p. 10 of the accepted manuscript; quoted for "attacks per week on average", a weekly rate averaged over a longer period; the number 14 concerns trial subgroups and is not part of the output
- Quote: "a persistent high attack frequency (e.g. ≥ 14 attacks per week on average)"

#### E-064/D01
- Kind: D
- Concerns: E-064
- Text (v34 Notes): The rate is shown with its period, whose length is always stated (INV-003, E-005), and in the same view as the attack count where the view shows both, so the relation is between output elements only.

#### E-064/D02
- Kind: D
- Concerns: E-064
- Text (v34 Notes): Like every count of the model, the rate rests on the attacks that the summarised diary information shows for its period; the completeness indicator (E-013) shows how completely the period is covered.

#### E-064/D03
- Kind: D
- Concerns: E-064
- Text (v34 Notes): The type scope must be of cluster headache only (`onlyOfType`, E-012), because a rate over all headache types of a subject who also has, or may have, another type would count attacks that are not cluster headache attacks, or that the output presents under that other type (OUT-029, INV-118 (C1-13)).

#### E-066/D01
- Kind: D
- Concerns: E-066
- Text (v34 Notes): "Shareable with the treating clinician" is represented by availability for contexts whose audience is a clinician; the means of sharing is delivery and out of scope. See ISS-04 on OUT-008 within "OUT-004 to OUT-009". `summaryTimeCourse(v, sr)` is the time course of the frequency measures that INV-104 requires over the series of the summary: headache days, migraine days (for patients with migraine), moderate/severe headache days and attacks for every period of the series, and the mark of every period that shows 0 migraine days.

#### E-067/W01
- Kind: W
- Concerns: E-067
- Text (v34 Notes): The overview may cover any period, for example the period since the previous consultation, which a patient uses to prepare the consultation; INV-105 then requires the headache days, migraine days, intensity and acute-medication days of the covered period and their time course over all whole periods within it, wherever it contains one.

### 2.4 Invariants

#### INV-118/D03
- Kind: D
- Concerns: INV-118
- Text: Equivalence with v34. For each case of table C1 the instance of INV-118 unfolds to the v34 predicate it replaces (C1-NN/D01): `reportedTogether(c, {K}, sc)` is `reportedPerPeriod(c, K, sc)` (section 3.4); a case whose `ppRequired` holds several pairs asks `reportedTogether` for each pair, as v34 INV-022, INV-028 and INV-029 did; an applicability condition inside `ppRequired` (`hasType`, `provides`, `#possibleHeadacheTypes ≥ 2`) makes the set empty outside the condition, which is the v34 implication; `MonthlyKind`, `Granularity` and `{calendarWeek}` are non-empty. Every v34 invariant that had its own existential granularity is its own case: the two measures of v34 INV-108 are C1-04 and C1-06, and v34 INV-018 and INV-029 are C1-07 and C1-14; one existential quantifier over both would strengthen the rule. For C1-11 (v34 INV-025), a series that tiles the selected time range at the granularity `calendarWeek` has that granularity (`tiles`, E-006), so its view is a `WeeklyMedicationView` (E-036); the converse is immediate.

#### INV-119/D04
- Kind: D
- Concerns: INV-119
- Text: Equivalence with v34. Where the bearer of a case of table C2 is every element (C2-01, C2-02, C2-05, C2-07), the annotation disjunct of `presents` adds nothing, because an annotation is itself an element. For C2-08 the annotations that qualify the three-month view or its items are in the view's content (E-010 `qualifies`, W2), so they are bearers. C2-04 and C2-09 had the annotation disjunct in v34 (INV-048, INV-084). For C2-03 and C2-06 the disjunct is new in v35: a claim carried by an annotation that qualifies the element counts as presenting the element with it, as v34 already read for INV-048 and INV-084 (CHG-07 in `fixes/fix-iter-35.md`).

#### INV-120/D03
- Kind: D
- Concerns: INV-120
- Text: Equivalence with v34. Each case of table C3 is the replaced v34 conjunct with its bearer set (C3-NN/D01). In C3-11 and C3-12, `ctx(outputOf(…))` replaces the bare `ctx` of v34 INV-098 and INV-092, because a cell is a term outside any invariant; in the output-scope INV-120 the two are the same context (section 2.9).

#### INV-121/D01
- Kind: D
- Concerns: INV-121
- Text: Equivalence with v34. `daysWithin` (E-012) has one member per replaced conjunct: the day count of v34 INV-005, the covered days of v34 INV-012, the days of a level of v34 INV-032, the days with a symptom and the caregiver days of v34 INV-033; the second conjunct is the pain-time conjunct of v34 INV-033, verbatim.

#### INV-122/D01
- Kind: D
- Concerns: INV-122; v34 INV-031
- Text (v34 INV-031 Notes): A moderate/severe headache day is, under the published definitions, a day with headache, and so a headache day as ICHD-3 defines it (OUT-004, INV-125 (SD-DF-01)). A symptom-free day is free of headache by the definition quoted in Stage 1 OUT-008.

#### INV-122/D02
- Kind: D
- Concerns: INV-122
- Text: Equivalence with v34. `nestedIn` (E-014) has one disjunct per replaced bound, with the same quantifier ranges: the four ≤ bounds of v34 INV-024, the two bounds of v34 INV-031 (moderate/severe within headache days, symptom-free within headache-free days) and the functional-impact bound of v34 INV-033. The last two conjuncts are v34 INV-030, verbatim.

#### INV-123/D01
- Kind: D
- Concerns: INV-123
- Text: The class of INV-123 (fix 32, R32b-02, updated to v35 IDs): an attribute whose value names an entity of the context (a treatment, a course event, an instrument or screening administration, a start of withdrawal, a rule, a scheme window), or whose presence presupposes an event of the context (a stop reason presupposes a stop).

| Element.attribute | Fact of the context | Tie in v35 |
|---|---|---|
| E-046 `treatment` | one of the subject's preventive treatments | INV-123 (`preventiveCourse`) |
| E-055 `stopReason` | the treatment has stopped | INV-123 (`stoppedCourse`) |
| E-058 `instrument`, `completionDate` | a result of the instrument is available | INV-123 (`availableResult`) |
| E-059 `instrument`, `date` | a screening result of the instrument is available | INV-123 (`availableScreening`) |
| E-034 `treatment`, `event`, `date` | a course event of a preventive treatment | INV-123 (`preventiveCourse`, `courseEvent`); the event kinds by the type of `event` |
| E-039 `withdrawalStart` | a start of withdrawal | INV-123 (`withdrawal`) |
| E-042 `rule`, `treatment`, `anchorDate` | a rule of the list, an applicable preventive treatment, its anchor event | INV-058 |
| E-043 `treatment`, `treatmentStart` | a preventive treatment and its start | INV-123 (`preventiveCourse`, `courseEvent` of kind `start`) |
| E-047 `treatment`, `window` start | a preventive treatment; the window begins on or after the course | INV-123 (`preventiveCourse`); INV-067 (`courseBegunBy`) |
| E-048 `treatment` | a preventive treatment with a stated start | INV-123 (`preventiveCourse`); INV-068 (the start) |
| E-049 `treatment`, `event`, `eventDate`, periods | the course event and the days of the course | INV-123 (`preventiveCourse`, `courseEvent`); the event kinds by the type of `event`; the periods by INV-112 |
| E-053 `drug`, `formulation` | an acute medication the subject has used | INV-123 (`usedMedication`) |
| E-055 `treatment`, `role`, `startDate`, `stopDate`, `doseChanges`, `formulations` | the course and its events | INV-123 (`preventiveCourse`, `acuteCourse`, `courseEvent`, `stopOn`, `usedMedication`) |
| E-055 `drug`, `duration`, `preventiveResponse`, `adherence` | the course | INV-079 |
| E-056 `scheme`, `windows` | the selected scheme and windows | INV-080 |
| E-058 `baselineResult` | an available earlier result | INV-082 |
| E-063 `end`, `ongoing` | the as-of date | INV-089 |
| E-014 (E-029) acute-medication day count above 0 | use of medication of the count's scope | INV-123 (`usedScope`; v35, CHG-05) |
| E-046 `evaluated` | periods on the label's treatment | not in the class for responder and non-responder labels (fix 18); INV-064 for control levels |
| E-051 `drug`, `formulations` | none by themselves | not in the class (fix 17): a summary with 0 treated attacks states no use |
| other derived counts (treated attacks of a summary, the basis of an overuse indicator, cycle-line menstruation days, values of one type scope) | values obtained from diary information | not in the class; a count of 0 for a medication, type or treatment that did not occur is a correct value |
| E-054 `drugClass`; E-055 `adverseEffects`, `DoseChangeItem.newDose` | none | not in the class |
| E-046 `residual`, `otherValues` | none: references to output items | not context facts |

A future fix that finds a new attribute of the class adds a member to `factsShown` (PROCESS.md section 6a).

#### INV-123/D03
- Kind: D
- Concerns: INV-123; v34 E-055; v34 INV-079
- Text (v34 E-055 Notes): A stop reason states why the course ended, so it is shown only for a treatment that has stopped by the as-of date (INV-123), whatever dates the line shows; the `when` clause of `stopReason` asks for it at SHOULD for every such treatment.
- Text (v34 INV-079 Notes): **Stop reason.** The reason for stopping states why the course ended (OUT-024: "the reason for stopping"), so a line shows one only for a treatment that has stopped by the as-of date, whatever dates the line shows; the line of a treatment that has not stopped, whose course has not ended, shows none. E-055 asks for the reason at SHOULD exactly where the treatment has stopped (`stopped`), so the conjunct makes nothing more required.

#### INV-123/D04
- Kind: D
- Concerns: INV-123; v34 INV-079
- Text (v34 INV-079 Notes): **Formulation.** The formulation an acute line shows states in which formulation the patient took the drug, on which the EHF definition of triptan refractoriness turns (OUT-024). The context states the formulations of the subject's acute medications, not of each course (`acuteMedications`, E-008; courses are courses of a drug, `drugOf`), so each formulation shown is one in which the subject has used the line's drug up to the as-of date. A non-empty set of such formulations always exists, because the drug of every acute treatment is the drug of an acute medication (INV-001), so the SHOULD of `formulations` (E-055) can be met.

#### INV-123/D05
- Kind: D
- Concerns: INV-123; v34 INV-082
- Text (v34 INV-082 Notes): A result reports an available result of its instrument (OUT-026; the subject's available results, E-008), so the tie to the subject's available results holds whether or not the result shows its completion date, which E-058 asks for at SHOULD: a result of an instrument of which no result is available is not a result that the diary can report. It makes nothing more required: every result that an invariant asks for is an available result of its instrument (INV-062, INV-069, INV-081, INV-096, INV-104), and a baseline result is one of the same instrument.

#### INV-123/D07
- Kind: D
- Concerns: INV-123
- Text: Equivalence with v34. For each replaced conjunct, the member of `factsShown` and the clause of `stated` give the same verdict: `rc.treatmentStart ∈ startOf(ctx, t)` is the membership of `CourseEvent(t, start, rc.treatmentStart)` in the course events (definition of `startOf`); `eventOn` is membership of the course event; `AcuteMedication(drug ↦ l.drug, formulation ↦ f)` is in the acute medications exactly when some medication has that drug and that formulation (value equality); the two role conjuncts of v34 INV-079 equal the two role facts because INV-001 makes the preventive and acute treatments disjoint. The facts of v34 INV-056 and INV-068 were MUST conjuncts and are definitional in v35 (CHG-R1); no output whose context lacks these facts met MUST in v34, so the conformant repertoires are the same. The `usedScope` member is new in v35 (CHG-05, CA-03): a shown acute-medication day count above 0 implies that the subject has used medication of its scope, which the subject profile lists (E-008); a count of 0 stays admitted.

#### INV-124/D01
- Kind: D
- Concerns: INV-124
- Text: R35-01 and the class rule. v34 INV-087 ordered the cycle lines only inside the menstrual-relation view; cycle lines of other views (for example the patient-facing overview, INV-105) could overlap, so an attack could be marked outside the A1.1 window on a window day of a menstruation the same view shows. The first conjunct closes this for the whole output: all views of one output summarise the same diary information as of one as-of date (fix 04). It quantifies over both kinds of shown first day of menstruation, the day 1 of a line and the day after a line that has ended (`shownDayOnes`, E-060), because E-060 states that an ended line shows the next first day. One exception remains: an attack on a line that has not ended may lie in the window of a menstruation that begins after the line's last day; its mark states nothing about that menstruation (E-061/D02). The same rule, that the dated phases one output shows describe one history, applies to the cluster periods and remission periods of E-063, whose non-overlap v34 stated only inside one cluster view (INV-089); the second and third conjuncts state it for the whole output, for items that show their start and last day. Stage 1 basis: OUT-030 (MUST, the A1.1 window), OUT-035, OUT-031 ("using the ICHD-3 definitions": a remission period is attack-free and a cluster period has attacks).

#### INV-125/D01
- Kind: D
- Concerns: INV-125
- Text: Equivalence with v34. Each row of table SD-DF unfolds to one of the two v34 predicates: SD-DF-01 to v34 INV-009 at MUST, SD-DF-02 to v34 INV-010 at SHOULD.

#### INV-001/Q00
- Kind: Q
- Concerns: INV-001
- Source: [S-011] — https://pmc.ncbi.nlm.nih.gov/articles/PMC9188162/
- Source: [S-013] — https://pmc.ncbi.nlm.nih.gov/articles/PMC7296705/
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Text: Stage 1 OUT-001, OUT-004, OUT-009 ("where weekly granularity is clinically relevant (tension-type headache, cluster headache, early onset of effect)"), OUT-014, OUT-034 ("(or a period chosen by the clinician)", with no condition on that period), OUT-018 ("For each preventive treatment [...] at the evaluation time points named in current guidance, which differ by treatment type"; periods "after treatment start, aligned to the treatment start date"), OUT-022 ("stopped, paused or reduced"; "compare it with both the on-treatment period and the original pre-treatment baseline"; [S-011] "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal."), OUT-024 ("start and stop dates, dose changes, treatment duration"; [S-013] "information on duration, dose and adverse events is sufficient and reliable"), OUT-029; the population of NICE CG150, "young people (aged 12 years and older) and adults" ([S-015], quoted in E-041).

#### INV-001/D01
- Kind: D
- Concerns: INV-001
- Text (v34 Notes): The whole-period condition applies to the selected time range only, which the outputs given "for every period in the selected time range" (OUT-004) tile. Outputs for other periods rest on the context parts that state them, none of which is subject to that condition: the comparison periods (INV-037, INV-039), the period since the previous consultation and the period chosen by the clinician (INV-094), the start of withdrawal (INV-049), each with any dates up to the as-of date, and the scheme windows (E-056, MAY). The order of course events is part of what a treatment's start is: the course of a treatment begins with it. It ensures that a stop date shown in the treatment history is not before the start date (INV-079), and that the anchor of every evaluation rule lies on or after the start (E-041 Notes).

#### INV-001/D02
- Kind: D
- Concerns: INV-001
- Text (v34 Notes): **One stop or pause per course.** A course also ends with its one stop or pause, dated on its last day on treatment (section 2.8), and no dose change, and no reaching of the target or tolerated dose, follows it, because each of these is dated on a day at the new dose, a day of the course. So the stop date and the duration of a treatment line (INV-079), the span of the course (INV-109; `courseOverlaps` and `courseNotOutside`, E-067), the end of the course that bounds evaluated and on-treatment periods (`notStoppedBefore`, E-042; INV-055, INV-068, E-046) and the on-treatment period before a stop, pause or reduction (INV-112) all refer to the same last day, and every event that the markers (INV-035, INV-104) and the post-stop monitoring (INV-103) take is a day of the course. A treatment that is resumed after a stop or pause, for example restarted after a pause because migraine worsens (OUT-022, [S-011]), is a new course with its own start that resumes the earlier course (`resumes`, E-008): its treatment line, markers, response comparison, treatment review view and post-stop monitoring are its own. The baseline of its response comparison and of its treatment review view is a pre-treatment baseline before its own start, which may be the original one (INV-056, INV-068; OUT-018 and OUT-021 say "pre-treatment baseline"). The baseline of its post-stop monitoring is the original pre-treatment baseline: a period that ends before the original start of the treatment, the start of the first course of its chain (`originalStart`, E-008; INV-112; OUT-022: "the original pre-treatment baseline"), not a period of the interval off treatment between the courses; where the context states no start for that first course, the monitoring shows no baseline (E-049). A pause that is later made definitive without a restart adds no course event: its monitoring is that of the pause (INV-070, INV-103), whose periods after the event continue from the first day off treatment onward. The end of a treatment cycle is not bounded by the stop: it is dated on the first day after the cycle (section 2.8), which for a course stopped on the last day of its last cycle is the day after the stop, as when onabotulinumtoxinA is stopped after 2 treatment cycles (NICE CG150 1.3.29, E-041); a time point at a cycle end is shown and required only where the course is taken through its interval (`intervalOnTreatment`, E-042).

#### INV-001/D03
- Kind: D
- Concerns: INV-001
- Text (v34 Notes): **Resumed courses.** A course that resumes the treatment of another course (`resumes`, E-008) starts after the stop or pause of that course, the last day of that course, which is not before that course's start (no course event precedes a start). So along a chain of resumptions every start follows the start of the course before it, no course resumes itself, directly or through other courses, and the chain is finite: it has at most as many courses as the subject has preventive treatment courses. Because each course resumes at most one course and is resumed by at most one, the courses that a course resumes, directly or through others, form one chain, and its first course, the treatment as it was first started, is unique; `originalStart` is the start that the context states for that course, and is empty where it states none (E-008). The link is between preventive courses, because OUT-022, whose original pre-treatment baseline it serves, concerns preventive treatment; it relates two courses of the same drug, as a resumed treatment is a course of the drug of the course it resumes (E-008 Notes); and it reads the stop as `e.kind is stop`, as every relation of the model does. A context that states no link (`resumes = ∅`) is admissible whenever it is admissible without the component, so the conjuncts exclude only links that are not resumptions of a stopped or paused course by a later course of the same drug. A preventive treatment is a treatment of a headache disorder: it is given for at least one of the headache types the subject has or may have, or has had or may have had; the headache-type sets cover the subject's history up to the as-of date (E-008), so a stopped preventive treatment of a headache type that the subject no longer has stays admissible. Together with the guidance type, this makes the rules for all preventive types apply to every preventive treatment within the population of their guidance (E-041 `inPopulation`) that has their anchor and is not of a type the rule excludes, whatever the type listing otherwise (only a listed type excludes a rule), and keeps every rule from applying outside its population.

#### INV-003/D01
- Kind: D
- Concerns: INV-003
- Text (v34 Notes): **Periods of referenced values.** A change, a residual burden and a composite index refer to per-period values, not to periods (`referencedValues`, E-011), so the conjunct on `refs(x) ∩ Period` does not place the periods of these values in the item's view, and the values themselves may be shown in another view of the output (rule W1; E-040 `reference`, `compared` (W2) places them in the view only for the changes of a response comparison). The last conjunct shows in the item's view a period with the dates of the period of each such value: the period atom of the value itself where the value is shown in the same view, and otherwise another period atom with the same dates, since every atom is part of one view. So every summary output states the reporting periods of every measure it reports (OUT-001), also for a change shown apart from the two values it compares (E-040 Notes).

#### INV-003/D02
- Kind: D
- Concerns: INV-003
- Text (v34 Notes): **Period atoms with the same dates.** A view may thus show several period atoms with the same dates, for example such an added atom, or a month of its series and the same month as a period of a response comparison that it shows. For the reader they are one reporting period. So these values that one view shows for periods with the same dates agree: counts (INV-006), completeness (INV-012), the combined medication-overuse indication (INV-046) and cluster attack rates (INV-089); other values, for example two intensity summaries, are not tied by any invariant. The relations among per-period values compare periods by their dates, not by atom (`daysOf`, E-014; INV-024, INV-031 to INV-033, INV-089, INV-122; INV-053; E-032 `sameIndicatedPeriod`; E-046). Membership of a value in a comparison stays tied to the comparison's own period atoms (INV-038, INV-056), and the placement of items in one view above is unchanged.

#### INV-003/S01
- Kind: S
- Concerns: INV-003
- Text (v34 Notes): Satisfiability: a period atom with given dates and the kind of the value's period can be added to any view, and it satisfies INV-002; INV-011 then asks for the completeness of these periods in the same view.

#### INV-006/D01
- Kind: D
- Concerns: INV-006
- Text (v34 Notes): A reporting period is identified to the reader by its dates (E-005), and a view may show several period atoms with the same dates (INV-003 Notes), for example a month of a series and the same month as an on-treatment period of a response comparison, or a calendar month and a 28-day period with the same dates (February of a common year). The number of days, or of attacks or auras, of a measure and type scope in a span of days is one number, whatever the atom or the kind of the period, so the invariant compares periods by their dates. For migraine days and moderate/severe headache days, whose published definitions count different days (OUT-002 Rationale), the counts of one view follow the one definition that the view follows for the measure (E-011, INV-111). The invariant holds within one view, as the relations among per-period values do (INV-024, INV-122, INV-031, INV-032, INV-033, INV-089); views of one output may follow different definitions for a measure (the definition labels of INV-008 are stated per view), so their values are not compared.

#### INV-006/S01
- Kind: S
- Concerns: INV-006
- Text (v34 Notes): Satisfiable: a view that shows one number for each measure, or event, type scope and dates meets it, whatever the number of period atoms with those dates.

#### INV-008/S01
- Kind: S
- Concerns: INV-008
- Text (v34 Notes): Satisfiable in every view: a label has no period and no other constraints than INV-125, which fixes its definition for headache days and attacks (table SD-DF), and INV-111, which a view meets by stating, for each measure, the definition its values follow, which is the definition of the views that show the values a change, a residual burden or a composite index of the view refers to where those views state one; by the third conjunct of INV-111, those views state one definition for the measure.

#### INV-111/D01
- Kind: D
- Concerns: INV-111
- Text (v34 Notes): A definition label states the definition that its view follows for the measure (E-011), and the values of a measure in one view follow one definition: the view shows one value per measure, period dates and type scope (INV-006), and its relations among values (INV-024, INV-122, INV-031) compare values of one measure under one definition (E-011 Notes). A second label of the view naming another definition, or a label naming another definition than that of the view whose values a change, a residual burden or a composite index refers to, would state a definition that the values do not follow. So the invariant is definitional: it excludes only outputs whose labels contradict the values they label. It does not require a label; INV-008 (SHOULD) does, and with this invariant a view that meets INV-008 states exactly one definition for each measure it reports (`labelledAs`, E-011). Values of one measure under two published definitions are shown in two views, each with its label.

#### INV-111/D02
- Kind: D
- Concerns: INV-111
- Text: The third conjunct (v35, CHG-06, CA-07): the values that one change, residual burden or composite index refers to come from views that, where both state a definition for the measure, state the same one. A change between values under two definitions is not a change of one measure (E-011: relations compare values of one measure under one definition; OUT-002 Rationale: different definitions give different numbers). Without it, INV-008 could not be met in a view that shows such a change.

#### INV-111/S01
- Kind: S
- Concerns: INV-111
- Text (v34 Notes): Satisfiability: a label has no period. A view that states one definition per measure meets the first conjunct, and INV-125 fixes one definition for headache days and attacks. The second conjunct is met by stating, in the view of a change, a residual burden or a composite index, the definition stated in the view of its values. The third conjunct holds where the values that one such item refers to come from views that state the same definition, or none, for the measure; no invariant requires such an item to refer to values in views that state different definitions: the changes of a response comparison and their residual burden are shown with their values (E-040 `reference`, `compared`, W2; INV-060), and a composite index for migraine with its components (E-033 `components`, W2).

#### INV-011/D01
- Kind: D
- Concerns: INV-011
- Text (v34 Notes): Every view is a summary output with a stated reporting period (section 3.6). The first conjunct covers per-period values; the others cover the kinds of summary that the model shows otherwise, each for the period it summarises (E-013 Notes). A view whose only content is not a summary of diary information over a period, for example a treatment history view that lists treatments with their dates (E-054), needs no indicator for its covered period; the response summaries it shows bring their periods and their indicators by the first and second conjuncts.

#### INV-011/S01
- Kind: S
- Concerns: INV-011
- Text (v34 Notes): Satisfiable in every view: the covered period, the window of an adherence summary and the periods of the shown per-period values are in the view (INV-003), and so is a period with the dates of each referenced value (INV-003, last conjunct); an indicator with that period and the scope of all headache types (INV-012) can be added for each. Where a view shows several period atoms with the same dates (INV-003 Notes), the first conjunct asks for an indicator with each of them, and INV-012 makes the indicators of the same dates agree.

#### INV-012/D01
- Kind: D
- Concerns: INV-012
- Text (v34 Notes): The last conjunct makes the indicators of one reporting period agree where a view shows several period atoms with its dates (INV-003 Notes, INV-011): the days of a period that the diary covers are one number, so two indicators of the same dates state the same covered days, and their proportions are roundings of the same exact value, each to the decimal places with which it is shown (`≈`, section 2.7). The comparison is pairwise; because the numbers of covered days that a shown proportion admits are consecutive, indicators that agree pairwise rest on one number. An `otherCompletenessExpression` is worded text and is not compared.

#### INV-012/S01
- Kind: S
- Concerns: INV-012
- Text (v34 Notes): Satisfiable: indicators that state the covered days of the period, the proportion of the period's days that these days make, or both, meet it.

#### INV-027/D01
- Kind: D
- Concerns: INV-027
- Text (v34 Notes): The days with severe functional impairment may be counted in one domain or for any activity (`anyActivity`, E-030). Severe impairment counted in paid work for one period and for any activity for another counts different days and cannot be compared, so the comparison with the baseline period that OUT-027 asks for shows it in one domain for all its periods (`∃ sd`); which domain is the diary's choice.

#### INV-027/S01
- Kind: S
- Concerns: INV-027
- Text (v34 Notes): Satisfiable: any domain serves, and INV-122 bounds the severe-impairment days of a domain only by the days affected in that domain where the view shows these.

#### INV-031/Q00
- Kind: Q
- Concerns: INV-031
- Source: [S-002] — https://ihs-headache.org/wp-content/uploads/2025/04/Clinical-Trials-Controlled-trials-of-preventive-treatment-of-migraine-attacks-in-episodic-migraine-in-adults-CEP.pdf
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Text: Stage 1 OUT-008 (symptom-free days defined as "the days free of premonitory, aura, headache, and postdromal symptoms" [S-002]), OUT-006, OUT-020; OUT-002 Rationale ("There is no single universally adopted definition of a migraine day; different definitions give different numbers."); [S-010] the count of E-018 and the definition of a migraine day on which it rests, quoted in E-018.

#### INV-031/D01
- Kind: D
- Concerns: INV-031
- Text (v34 Notes): The relations are inequalities: days without diary information are neither headache days nor headache-free days, and the definitions say nothing about them. Every relation compares counts whose definitions the output names and which are nested under them. A headache-free day has no headache. The mark of a period without migraine days refers to the migraine days shown in the same view for a period with its dates. The counts compared follow the one definition that the view follows for each measure (E-011, INV-111). Migraine days are not related to headache days because published migraine-day definitions differ (OUT-002). For the same reason, migraine days are related to the count of E-018 only where the view's label states that they follow the definition of [S-010] on which that count rests (`labelledAs`, E-011). The count of E-018 is related neither to moderate/severe headache days nor to the sum of the two counts: [S-010] adopts no definition of a moderate-to-severe headache day, and the view's moderate/severe headache days follow the definition its label names (E-018 Notes).

#### INV-031/X01
- Kind: X
- Concerns: INV-031
- Text: Removed in v35 (CHG-04, CA-02): the conjunct by which a view that marks one period without migraine days marks every period of the view whose migraine-day count for the type scope is 0. A definitional invariant cannot make an element more required (section 3.3, item 5), and marking every such period is content of OUT-008 (MAY), which no SHOULD or MUST part of Stage 1 asks for. In the clinician-facing summary, INV-104 (SHOULD) still asks for the marks of the covered period and of each period of its series that shows 0 migraine days. The conjunct "a mark implies a count of 0" stays.

#### INV-035/D01
- Kind: D
- Concerns: INV-035
- Text (v34 Notes): `markers` is a reference (section 2.5), and a marker refers to no period, so INV-003 does not place it in the view; the placement marker on `markers` (E-035, W2) does, because OUT-009 asks for the series "with dated markers", so that the onset of effect and the trajectory of response can be related to the treatment course in the same view. The values of the series are in the view by `perPeriod`, and the periods of the series by INV-003. The clinician-facing summary places its markers in its own content in the same way (INV-104).

#### INV-039/Q00
- Kind: Q
- Concerns: INV-039
- Source: [S-030] — http://dhos.dk/wp-content/uploads/2020/06/2932-Referenceprogram_2020_final_web-24.06.20.pdf
- Text: Stage 1 OUT-010 ("and allow comparison between periods"; Evidence basis: "a change in intensity between periods (for example the halving of intensity in [S-030]) can only be read when the scale is known"); OUT-036 (c) ("apply equal-length period comparisons as in OUT-001") for children and adolescents.

#### INV-039/D01
- Kind: D
- Concerns: INV-039
- Text (v34 Notes): Where the subject is a child or adolescent on the first day of one of its periods, every comparison SHOULD compare periods of equal length (INV-097, OUT-036 (c)). OUT-010 asks only that comparison between periods be allowed and names no lengths, so for such a selection a comparison of selected periods of equal length allows it; requiring a comparison of a selection of unequal lengths as well would contradict INV-097. The age is read on the selected periods, as in INV-097 (E-008), not on the as-of date.

#### INV-039/D02
- Kind: D
- Concerns: INV-039
- Text (v34 Notes): **One scale and one form.** A comparison allows intensity to be compared between its periods only where their summaries share the scale and the form: a mean of 6.0 on a 0–10 numerical scale next to a distribution of headache days over a four-level verbal scale shows no change that a reader can read. So the summaries of the compared periods share the scale and the form of one intensity summary of the comparison (`onSameScale` with `i₁`, E-023), and so with each other; summaries in forms other than the two that Stage 1 names share a form only where they state the same form (`OtherSummary`, E-023), so that a median peak intensity for one period and the share of headache days with severe pain for another are not in one form; the comparison may show further summaries, for example of the same period in another form. Which scale and form is the diary's choice.

#### INV-039/S01
- Kind: S
- Concerns: INV-039
- Text (v34 Notes): Satisfiable: INV-032 holds for summaries on any scale and in any form, so the compared periods can be summarised alike.

#### INV-045/D01
- Kind: D
- Concerns: INV-045
- Text (v34 Notes): The span is the shortest one so that the indication of a period is unambiguous; with calendar months or 28-day periods it has four periods. The basis values are day counts of the indicator's view (INV-003 Notes), so where one view shows indicators whose spans include periods with the same dates, for example the indicators of consecutive months, each on period atoms of its own, the basis values of those periods are one number (INV-006); the indication of a class therefore rests on the same days as every other indication of the view that refers to those dates.

#### INV-046/Q00
- Kind: Q
- Concerns: INV-046
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: Stage 1 OUT-016 ("for ICHD-3 subtype 8.2.6, for the combined use of acute medication across classes"; [S-001] 8.2 note 2, "Patients who use multiple drugs [...] such patients should be coded 8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused"); [S-001] 8.2.6 criterion B ("Regular intake of any combination of ergotamine, triptans, non-opioid analgesics and/or opioids") and note 2 quoted in E-028. Not quoted in Stage 1:

#### INV-046/Q01
- Kind: Q
- Concerns: INV-046
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Location: 8.2.3 Non-opioid analgesic-overuse headache, Comments, second paragraph, p. 123; in the PDF text layer line ends break "non-opioid", "therefore", "analgesic-overuse" and "headache"
- Quote: "For the purposes of ICHD-3, all non-opioid analgesics are regarded as a single class; therefore, a patient who uses more than one non-opioid analgesic cumulatively, but not any single drug, on 15 or more days/month is coded 8.2.3 Non-opioid analgesic-overuse headache (with the individual drugs specified in parenthesis) and not 8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused."

#### INV-046/D01
- Kind: D
- Concerns: INV-046
- Text (v34 Notes): The per-class days are read from the class indicators of the same period (`classShownUsed`, `classUseExcluded`, E-032). INV-044 shows these indicators in the same view as the combined indicator, and their spans have the dates of its span, because each span is the shortest run of consecutive monthly periods of one kind that ends with the indicated period and lasts more than three months (INV-045). The same period is matched by its dates and kind in the view of the indicator (`sameIndicatedPeriod`, E-032), not by period atom, so that a class indicator shown for the same month on a period atom of its own is not left out; the kind is part of the match because a calendar month and a 28-day period with the same dates have spans with different dates. Two class indicators of the same period and class rest on the same days (INV-045, INV-006) and so give the same indication; for combined use the last conjunct states it, because the relation leaves the status open between its two cases.

#### INV-046/S01
- Kind: S
- Concerns: INV-046
- Text (v34 Notes): The two directions agree: when the second antecedent holds, the two classes that show days in the first period of the span are not excluded, so the conditions of "reached" hold. For a subject without acute medication, or with medication of one class of 8.2.6 only, the combined indicator that INV-044 requires is shown as "not reached".

#### INV-049/D01
- Kind: D
- Concerns: INV-049
- Text (v34 Notes): The selected time range consists of whole periods of the selected granularity (INV-001), so the first conjunct cannot reach every day after the start of withdrawal (INV-049/W01). The second conjunct requires the view of the running follow-up, from the start of withdrawal to the as-of date, which "from the start of withdrawal onward" asks for and which E-039 already admits (its covered period may end on any day). Its content is that of INV-050: the values of the covered period itself, a series of the whole periods from the start of withdrawal within it wherever one fits, and the review window. The review window SHOULD be shown in every follow-up view (E-039 `reviewWindow`); INV-051 fixes its dates, which may lie after the covered period and the as-of date.

#### INV-049/S01
- Kind: S
- Concerns: INV-049
- Text (v34 Notes): Satisfiability: the start of withdrawal lies on or before the as-of date (INV-001), so the covered period is a span; INV-050 is satisfiable for a covered period of any length that begins on the start of withdrawal (INV-050 Notes), and INV-003, INV-051 and INV-120 (C3-06) hold with it.

#### INV-049/W01
- Kind: W
- Concerns: INV-049
- Text (v34 Notes): With 28-day periods from a start on 10 March and an as-of date of 21 April (day 43, within the NICE review window), the longest such time range ends on 6 April.

#### INV-050/D01
- Kind: D
- Concerns: INV-050
- Text (v34 Notes): The covered period may end on any day (E-039/D02), so the series is not required to span it exactly. `fillsPeriod` (E-006) keeps the series tied to the covered period, as INV-104 and INV-105 do: it spans the covered period up to fewer days than one period at its end, and it cannot shrink to a single period where two or more whole periods of its granularity from the start of withdrawal fit in the covered period. The values of the covered period itself show every day from the start of withdrawal onward, including those after the last whole period. The series is present wherever a whole period that begins on the start of withdrawal fits in the covered period (E-039, `series` SHOULD when `wholePeriodFrom`). The review window SHOULD be shown in every follow-up view (E-039 `reviewWindow`); INV-051 fixes its dates, which may lie after the covered period and the as-of date.

#### INV-050/D02
- Kind: D
- Concerns: INV-050
- Text: v34 INV-050 also asked for the review window once the covered period reaches the end of the window. v35 removes that conjunct as implied by E-039 `reviewWindow` (SHOULD, without a `when` clause), which asks for the review window in every follow-up view at the same level (CA-05; no change of meaning). The settled reading of fix 02, item 14, is kept: the review window SHOULD be shown in every follow-up view, and INV-051 fixes its dates.

#### INV-050/S01
- Kind: S
- Concerns: INV-050
- Text (v34 Notes): Satisfiability: consecutive 28-day periods from the start of withdrawal fill any covered period of at least 28 days that begins on it, and a covered period with no such whole period needs only its own values; the review window lies within the covered period when the condition of the last conjunct holds, so INV-003 and INV-051 hold with it; for a time range of INV-049, which consists of whole periods of the selected granularity from the start of withdrawal (INV-001), the series of these periods spans the covered period exactly.

#### INV-055/Q00
- Kind: Q
- Concerns: INV-055
- Source: [S-034] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=169_3
- Text: Stage 1 OUT-018 ("The output MUST allow this comparison at the evaluation time points named in current guidance"), OUT-001 ("for example a pre-treatment baseline period against a later period of the same length"), OUT-036 (d) (efficacy of treatment from diary data, for children and adolescents; the MUST of OUT-018 covers every subject, and the time points required for a treatment started in childhood or adolescence are those of guidance that covers the subject's age on that start, including the paediatric guidance [S-034] that Stage 1 cites for (d), E-041).

#### INV-055/D01
- Kind: D
- Concerns: INV-055
- Text (v34 Notes): A preventive treatment given only for another headache type, for example verapamil for cluster headache, has a response comparison without the time points of these rules; for a treatment started in childhood or adolescence, the rules that can apply are those of the NVN module, IHS 2024 Q2, the Turkish protocol and the Russian clinical recommendations for children, and, for a start from the age of 12, also NICE CG150 1.3.27, whatever the subject's age on the as-of date (see ISS-10).

#### INV-055/D02
- Kind: D
- Concerns: INV-055
- Text (v34 Notes): The on-treatment periods of a comparison are calendar months or 28-day periods that begin on or after the treatment start (INV-056), so the last day of each is at least 27 days after the start, and a period ends at a time point when its last day is the day before it (`atTimePoint`, E-042). A time point less than 28 days after the start therefore cannot be the end of such a period, and the comparison is not required at it (`fitsMonthlyPeriod`, E-042). Because no course event precedes the start (INV-001), this can happen only for the rules whose time point is the end of a treatment cycle: NICE CG150 1.3.29 (the second cycle) and the Turkish protocol sections 3.6.3.9 (the third cycle) and 7.3 (the second cycle, as the earliest time point) (E-041 Notes).

#### INV-055/D03
- Kind: D
- Concerns: INV-055
- Text (v34 Notes): **Stop or pause.** A time point is required only where the course is taken through its interval (`intervalOnTreatment`, E-042; E-041 Notes, **Stop or pause**), and the on-treatment period of the comparison at it ends on or before every stop or pause of the course (`notStoppedBefore`), which matters for a course stopped within a window. A treatment that has started still has a response comparison, whatever its stops (first conjunct), with its periods after the treatment start (INV-056). For a course that has not stopped, the requirement is the same as without these conditions.

#### INV-055/S01
- Kind: S
- Concerns: INV-055
- Text (v34 Notes): Satisfiability: for a time point that fits, a 28-day on-treatment period whose last day is the day before the time point (for a window, the day before the later of its earliest date and the 28th day after the start, which the condition places within the window) begins on or after the start, and a 28-day baseline period that ends before the start has the same length; so INV-055, INV-056 and, for children and adolescents, INV-097 hold together in every admissible context. That period lies within the course: every window of the list begins at least 8 weeks after the start (E-041 Notes), so for every rule its last day is the last day of the interval, on or before every stop or pause of the course where `intervalOnTreatment` holds.

#### INV-055/W01
- Kind: W
- Concerns: INV-055
- Text (v34 Notes): For example, for an anti-CGRP monoclonal antibody started on 1 January 2026, the calendar months of December 2025 and March 2026 (31 days each) are compared at the 3-month time point, 1 April, of EHF 2022 question 3, IHS 2024 Q2 for monthly injectables and the Russian section 7.1, and at the earliest date of the NICE CG150 1.3.27 window; and 4 to 31 December 2025 and 26 February to 25 March 2026, the final 28 days of the 12 weeks of treatment, are compared at the NICE CG150 1.3.28 time point, 26 March. If the same antibody is stopped on 10 February 2026, its last day on treatment, no time point is required: the course does not reach the last day of any interval (28 February for Turkish Box 8, 25 March for NICE CG150 1.3.28, 31 March for the others), and a comparison of the treatment is still required. If it is stopped on 30 March, the time points of NICE CG150 1.3.28 and Turkish Box 8 are required, and the 3-month time points are not.

#### INV-056/D01
- Kind: D
- Concerns: INV-056
- Text (v34 Notes): The co-presence of OUT-018 ("showing both the values of each period and the absolute and percentage change from baseline") is thus required at MUST, wherever the comparison is shown.

#### INV-060/D01
- Kind: D
- Concerns: INV-060
- Text (v34 Notes): Neither the antecedent nor the residual migraine days carry a subject condition, as OUT-019 states none: a percentage change in the headache days of a subject without migraine SHOULD also be shown with its residual migraine days, which are 0; see ISS-03.

#### INV-060/D02
- Kind: D
- Concerns: INV-060
- Text: v35 restricts the antecedent to changes whose compared period has at least `shortestMonthlyDays` (28) days (CHG-03, CA-01). A residual burden "per month" refers to a calendar month or 28-day period within the compared period (INV-061); within a shorter compared period no such month exists, so v34 INV-060 was unmeetable there and excluded from full conformance every percentage change in migraine or headache days over a period shorter than 28 days. The reading of fix 02, item 14, is kept, and the open question goes to the human (ISS-13).

#### INV-062/Q00
- Kind: Q
- Concerns: INV-062
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Text: Stage 1 OUT-020; [S-010] for the count on which the control levels rest (E-018), and for the acute-treatment part of optimal control, which holds "for three months" (quoted in E-046). The other values keep the applicability conditions of the requirements OUT-020 refers to (section 3.5, reference rule): OUT-026 ("Where results of validated instruments are available") and OUT-023 ("For each acute medication"). OUT-020 names these values as examples ("for example"); the further kinds, and the criteria quoted in Stage 1 that rest on them, are in E-045 (Evidence and Notes). A per-period value or a value of another kind is required where the diary provides it (`provides`, section 3.5). The values of one headache type are those in the scope `scopeFor` (E-012): the values over all headache types combined where the subject has a headache type and every headache type it has or may have falls under that type, and otherwise the values scoped to that type (`ofType`), as in the separate presentation per headache type of OUT-029 ("When the patient has, or may have, more than one headache type").

#### INV-062/D01
- Kind: D
- Concerns: INV-062
- Text (v34 Notes): An instrument result SHOULD show its completion date (E-058), and that date is the date of an available result (INV-123); a result of an instrument for which no result is available therefore cannot be shown. Without the availability condition, a label under a criterion that rests on such an instrument (for example IHS Q6, which also rests on PGIC, MIDAS and HIT-6) could not satisfy this invariant together with E-058 and INV-123. A score component rests on the score at the evaluation and on the pre-treatment baseline score (E-046 Notes), so these two results, where they are available, are the values of OUT-020 "those values as well" for that component; a result of the instrument from another time does not show them, and INV-063 decides the component only on this pair.

#### INV-062/D02
- Kind: D
- Concerns: INV-062
- Text (v34 Notes): The per-period values of a kind are shown for the baseline and evaluated periods, which the label's response comparison shows in the same view (INV-003): where the diary provides values of the kind, a value can be shown for each of these monthly periods, a value that the view already shows for the period and scope (INV-006) is referenced rather than repeated, attack counts over all headache types combined in particular are available per calendar month or 28-day period wherever they are provided (INV-118 (C1-04, C1-06)), and a value of any kind can be shown in any type scope, consistently with INV-122. The changes of the measures of a reduction component compare values over all headache types combined of the comparison's own baseline and on-treatment periods (INV-053, E-040 `reference`, `compared` (W2), INV-056, INV-057, and INV-097 for children); the residual burden (INV-060) concerns only changes in migraine or headache days, which INV-056 shows anyway. These attack counts and changes are the values on which INV-063 decides attack-reduction and reduction components (E-046), and they are required in the scope in which the components are decided: over all headache types combined, or, for the attacks of one headache type, in the scope `scopeFor` (E-012). Values of another type scope may be shown as well; they decide nothing (E-045 Notes, **Type scope**).

#### INV-062/D03
- Kind: D
- Concerns: INV-062
- Text (v34 Notes): **Acute treatment and instrument results.** The effectiveness of acute treatment on which a criterion rests is that of every acute medication the subject has used up to the as-of date (E-008), in every evaluated period, including one it no longer uses, with a summary of 0 treated attacks for a period in which it was not taken: OUT-020 refers to it as "the effectiveness of acute treatment in OUT-023", which OUT-023 reports "For each acute medication", and the optimal-control level of [S-010] holds "for three months, with a satisfactory response to acute treatment". So the label shows a summary of each acute medication, over all headache types combined, for each evaluated period, and, for a criterion that rests on acute-treatment summaries as per-period values (a change in the response to acute treatment, E-045 Notes), for the baseline period as well, as INV-069 and INV-071 do for the treatment review. Each of these summaries summarises the attacks treated with its medication: it is a summary of all formulations of the medication's drug or of the medication's own formulation (`summarisesMedication`, E-051), so that a summary of one formulation does not stand in for another formulation of the same drug; both readings of OUT-023 (per drug, or per drug and formulation) meet this (E-051 Notes). A summary may have 0 treated attacks (INV-072, INV-074). The results of an instrument on which a criterion rests are those of its evaluation: where a result completed after the treatment start within the last evaluated period is available, the label shows the latest such result (`evaluationResult`, E-046), as it does for a score component, whose baseline result it also shows; this covers instruments that a criterion names without a score threshold, for example PGIC under IHS Q6. No acute-treatment summary, and no result of an instrument without a score component (for example PGIC), decides a category; the results at the evaluation and at the pre-treatment baseline decide score components (INV-063).

#### INV-062/S01
- Kind: S
- Concerns: INV-062
- Text (v34 Notes): Satisfiable with E-058, INV-082 and INV-123: both are available results of the instrument, and the baseline result is completed before the result, on or before the treatment start, which the result's date follows.

#### INV-062/S02
- Kind: S
- Concerns: INV-062
- Text (v34 Notes): Satisfiable with INV-003, INV-011 and INV-072: the summaries refer to the evaluated and baseline periods, which INV-003 places in the label's view through the label and its response comparison, and the results are available results (E-058, INV-123).

#### INV-114/D01
- Kind: D
- Concerns: INV-114
- Text (v34 Notes): A label classifies the response to its treatment (E-046), and `comparison` is declared as its underlying values (OUT-018), so the tie holds wherever the label shows a comparison (section 3.3, item 5): a label shown with the comparison of another treatment would stand, as "responder" or "non-responder", next to the values of a treatment it does not classify. It is the counterpart of the tie of a treatment line to its response comparison (INV-079: `∀ r ∈ l.preventiveResponse • r.treatment = l.treatment`). It makes nothing more required: `comparison` stays SHOULD (E-046, INV-062), and a label without one meets it. It changes no decision of INV-063, whose components are tested only on the comparison of the label's treatment (`rc.treatment = L.treatment` in the predicates of E-046). That the comparison covers the periods the label refers to (`ran L.evaluated ⊆ ran rc.onTreatment`) is part of the underlying values that OUT-020 asks to "always show", and stays at its level (INV-062).

#### INV-114/S01
- Kind: S
- Concerns: INV-114
- Text (v34 Notes): Satisfiability: a comparison of the label's treatment can be shown wherever the context states the start of that treatment (INV-055, INV-056); where it states none, no response comparison of the treatment exists (INV-123), and the label shows none.

#### INV-116/Q00
- Kind: Q
- Concerns: INV-116
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Text: Stage 1 OUT-020 ("it SHOULD name the criterion applied (for example "NICE CG150 rec. 1.3.28", "IHS global practice recommendations Q6", "IHS position statement 2025 control levels")"); the thresholds of the named criteria, quoted in E-045 and E-046 and in Stage 1 OUT-018 and OUT-020, for example [S-015] 1.3.28 ("at least 50% in episodic migraine"; "at least 30% in chronic migraine").

#### INV-116/D01
- Kind: D
- Concerns: INV-116
- Text (v34 Notes): A label shows its criterion by its name, with its thresholds (E-046 `criterion`), and E-045 states the named criteria with the thresholds and other values of their sources: a named responder criterion with its threshold is part of the output data (section 1). A criterion shown under such a name with a threshold that the source does not state, for example "NICE CG150 rec. 1.3.28" with a 30 % threshold for every treatment, would misstate the source, and INV-063 would force the category that the misstated threshold gives. So the tie holds wherever a label shows a criterion (section 3.3, item 5), as an evaluation time point is one of the rule list (INV-058) and a grade band one of the bands of its instrument (INV-082). It makes nothing more required: `criterion` stays SHOULD (E-046, INV-062), labels stay optional, and a criterion shown under any other name is not constrained (OUT-020: "for example"; E-045 Notes, **Named criteria**).

#### INV-116/D02
- Kind: D
- Concerns: INV-116
- Text (v34 Notes): A component whose condition the label's treatment does not meet is never met and always decided for that label (`componentMet`, `componentDecided`, E-046), and INV-062 asks for no change or result for it. So a criterion that leaves out only such components, and rests on the same values, admits under INV-063 the categories that the named criterion admits, and is asked by INV-062 for the same values. The names compared are those that E-045 states for the named criteria; an output that names one of these criteria shows that name, as it shows an instrument by the name that E-057 states for it.

#### INV-116/S01
- Kind: S
- Concerns: INV-116
- Text (v34 Notes): Satisfiability: each named criterion meets the `where` clause of `ResponderCriterion` (the score components of `critIhsQ6` and `critDmkg` name instruments that their `alsoRestsOn` lists, and no named criterion has an attack-reduction component), the six names are pairwise distinct, and a label can show the named criterion itself.

#### INV-063/Q00
- Kind: Q
- Concerns: INV-063
- Source: [S-008] — https://ricerca.univaq.it/retrieve/b7f186a9-06ec-4e9c-b132-4f785bbeb121/puledda-et-al-2024-international-headache-society-global-practice-recommendations-for-preventive-pharmacological.pdf
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Source: [S-033] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=295_4
- Text: Stage 1 OUT-020; thresholds quoted in E-045, and the headache types of the measures of its criteria (E-045 Evidence and Notes, **Type scope**); the time on treatment over which the named criteria judge the response, Stage 1 OUT-018 and OUT-020 ([S-015] "after 12 weeks of treatment"; [S-008] "whether preventive therapy is effective and should be continued"; [S-033] "через 3 месяца терапии", after 3 months of therapy; E-046 Notes, **After a stop or pause**).

#### INV-064/Q00
- Kind: Q
- Concerns: INV-064
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Text: Stage 1 OUT-020; [S-010] quoted in E-046, whose control levels are goals of its section "Setting goals of migraine burden while on treatment".

#### INV-064/D01
- Kind: D
- Concerns: INV-064
- Text (v34 Notes): The level is read from the days of the evaluated months, so those months are tied to the label's treatment: they begin on or after its start, as the on-treatment periods of its response comparison do (INV-056, INV-062), and they end on or before every stop or pause of it, since the levels are goals "while on treatment" ([S-010]). Without the ties, a control-level label could classify months before the treatment, or after its stop or pause, as the response to it, for example "optimal control" over three months after a course stopped at six weeks.

#### INV-064/S01
- Kind: S
- Concerns: INV-064
- Text (v34 Notes): Satisfiable: a control-level label is optional (E-046), and INV-062 can be met with on-treatment periods of its response comparison that lie within the course; where no such months exist, no control-level label is shown.

#### INV-066/D01
- Kind: D
- Concerns: INV-066
- Text (v34 Notes): The window contains the on-treatment period it ends with, so the adherence shown covers the intake over a period whose values the comparison evaluates, not only its last days (E-047 Notes).

#### INV-066/S01
- Kind: S
- Concerns: INV-066
- Text (v34 Notes): Satisfiability: an on-treatment period begins on or after the treatment start (INV-056), so a window equal to that period, or from the treatment start to its end, meets `adherenceFor` and INV-067; INV-003 shows the window in the comparison's view and INV-011 its completeness.

#### INV-067/D01
- Kind: D
- Concerns: INV-067
- Text (v34 Notes): INV-067 bounds only the first day of the window. Whether or not the context states the start, it does not bound the window by the stop or pause of the course: a window may reach past the stop or pause, or begin after it. Where the context states the start, this holds for the evaluation windows of the response comparison as well: each ends with an on-treatment period of the comparison (`adherenceFor`, E-047), and these periods are not bounded by a stop (INV-056).

#### INV-068/D01
- Kind: D
- Concerns: INV-068
- Text (v34 Notes): OUT-021 presents the values "for the same pre-treatment baseline and on-treatment periods", so that "efficacy can be judged", and its on-treatment periods lie within the course: they begin on or after the treatment start and end on or before every stop or pause of it (`notStoppedBefore`, E-042). The periods after a stop or pause are shown by the post-stop monitoring view (E-049, INV-070). The comparison of OUT-018, whose periods Stage 1 names "periods after treatment start", is not bounded in this way (INV-056).

#### INV-068/S01
- Kind: S
- Concerns: INV-068
- Text (v34 Notes): Satisfiable together with INV-069, INV-097 and INV-102: the periods of the view are of any kind (E-048), and for a course that has stopped or paused, a period that begins on the treatment start and ends on the date of its stop or pause (a course has one, INV-001), or a shorter one within it, lies within the course, because no course event precedes the start (INV-001); for a course that has not stopped, the conjunct constrains nothing. A baseline period of the same length ends before the start.

#### INV-068/W01
- Kind: W
- Concerns: INV-068
- Text (v34 Notes): Where the context states no start, for example for a treatment that the subject was already taking, no period can be placed before the start: for such a treatment reduced on 15 March 2026 and paused on 30 June 2026, April 2026 lies on treatment, and a view that presented it as the pre-treatment baseline next to June 2026 would compare two months on treatment and hide the treatment effect by which "efficacy can be judged" (OUT-021).

#### INV-069/D01
- Kind: D
- Concerns: INV-069
- Text (v34 Notes): **Values that can be compared.** OUT-021 presents these values "for the same pre-treatment baseline and on-treatment periods" so that efficacy can be judged across them ("The purpose is that efficacy can be judged across these dimensions"). The counts of the view are counts of one measure under the one definition that the view follows (E-011, INV-111). Intensity summaries can differ in scale and form, and symptom summaries in form and unit (E-023, E-025), so the summaries of all the view's periods share the scale and the form of one intensity summary of the view (`i₁`), and those of each symptom the form of one summary of that symptom (`a₁`), summaries in other forms sharing a form only where they state the same form (`OtherSummary`, E-023; for example not the share of headache days and the share of attacks with a symptom); which scale and form is the diary's choice.

#### INV-069/S01
- Kind: S
- Concerns: INV-069
- Text (v34 Notes): Satisfiable: INV-032 and INV-033 hold for summaries on any scale and in any form, so the periods can be summarised alike.

#### INV-070/Q00
- Kind: Q
- Concerns: INV-070
- Source: [S-011] — https://pmc.ncbi.nlm.nih.gov/articles/PMC9188162/
- Source: [S-022] — https://www.ema.europa.eu/en/documents/scientific-guideline/draft-guideline-clinical-investigation-medicinal-products-treatment-migraine-cluster-headache-revision-2_en.pdf
- Text: Stage 1 OUT-022 ("compare it with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible"; [S-011] "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal."; [S-022] "to detect possible rebound phenomena (i.e. frequency of migraine days per month going above its baseline)").

#### INV-070/S01
- Kind: S
- Concerns: INV-070
- Text (v34 Notes): Satisfiability: periods of a common length no longer than the days on treatment before the changed regimen (from the treatment start, or, where the context states none, from the first dated course event, to the stop date, or to the day before a reduction) meet this invariant, INV-112 and INV-097, the baseline being such a period that ends on the day before the original start, which exists for any length, where the context states that start; where it states none, E-049 asks for no baseline, and the view without one meets them; for a reduction on the start day, or, where the context states no start, for a reduction that no other dated course event precedes, no on-treatment period is asked for.

#### INV-112/Q00
- Kind: Q
- Concerns: INV-112
- Source: [S-011] — https://pmc.ncbi.nlm.nih.gov/articles/PMC9188162/
- Source: [S-022] — https://www.ema.europa.eu/en/documents/scientific-guideline/draft-guideline-clinical-investigation-medicinal-products-treatment-migraine-cluster-headache-revision-2_en.pdf
- Text: Stage 1 OUT-022 ("After a preventive treatment is stopped, paused or reduced, the diary output SHOULD continue to show headache and migraine frequency and compare it with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible"; [S-011] "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal."; [S-022] "to detect possible rebound phenomena (i.e. frequency of migraine days per month going above its baseline)").

#### INV-112/D01
- Kind: D
- Concerns: INV-112
- Text (v34 Notes): The conjuncts of v34 INV-112 stated what the view is and what its periods are: the event it monitors (in v35, INV-123 and the type of `event`, E-049) and the three terms of its comparison (E-049). They hold wherever the view is shown (section 3.3, item 5), as the event of a treatment marker does (INV-123, with the same `eventOn`). A view of an event that the subject's course does not have, a baseline period that does not end before the original start, an on-treatment period outside the days of the course before the changed regimen, or a period after the event that contains a day of the earlier regimen would present a course of events that did not take place, or compare periods that are not those it names, and could hide the worsening or rebound above baseline that OUT-022 is to make visible. That the periods after the event are consecutive from the first day of the changed regimen is the structure that E-049 declares for `after` ("consecutive periods from the first day of the changed regimen onward"), as a series is consecutive (INV-004), the span of a medication-overuse indicator is a run of consecutive periods that ends with the indicated period (INV-045) and the months of a control-level label are consecutive (INV-064). The conjuncts make nothing more required: `baseline`, `onTreatmentPeriod` and `after` keep their levels and `when` clauses (E-049), an absent period meets every period conjunct, and the values of the periods, and the on-treatment period where the context states no start, are asked for by INV-070 at the level of OUT-022. Under the day convention (section 2.8), a stop or pause is dated on the last day of the course, which its duration and span include (INV-079, INV-109), and a dose reduction on the first day at the reduced dose. The periods after the event therefore begin on `firstChangedDay` (E-049), the day after a stop or pause and the day of a reduction, so that no period after the event contains a day of the earlier regimen, and the on-treatment period may end on the last day of the course, for example the final 28 days before a stop.

#### INV-112/D02
- Kind: D
- Concerns: INV-112
- Text (v34 Notes): **Original baseline.** The view shows a baseline only where the context states the original start of the treatment (`originalStart`, E-008), and the baseline ends before it. For a course that resumes no course, that is the course's own start. For a course that resumes the treatment of an earlier course after its stop or pause (`resumes`), it is the start of the first course of that chain, so that no month of an interval off treatment between the courses, in which migraine may have worsened after the withdrawal ([S-011]), and no month on an earlier course of the chain stands for the original pre-treatment baseline (E-049 Notes). Where the context states no start for the course as it was first started, no date places the original start, and the view shows no baseline: a period that ends before a restart, or before the dated course events of the first course, may lie in an interval off treatment or on that course (E-049 Notes, **Original start not stated**). Every baseline that the view shows ends before the start of the view's own course, because the original start is not after it. The on-treatment period and the periods after the event keep the start and the first changed day of the view's own course.

#### INV-112/S01
- Kind: S
- Concerns: INV-112
- Text (v34 Notes): Satisfiability: every view that INV-103 asks for is of a stop, pause or dose reduction of a preventive course that the context states, with its kind and date (`v.event = e.kind ∧ v.eventDate = e.date`), so it meets INV-123 and the type of `event` (E-049); its periods can be chosen as INV-070/S01 describes, and a view that shows no baseline, no on-treatment period or no periods after the event meets the conjuncts on them.

#### INV-072/D01
- Kind: D
- Concerns: INV-072
- Text (v34 Notes): The outcome measures and the per-attack lines are the effectiveness that the summary reports for its drug and period (OUT-023), and wherever a view shows a summary, it thereby shows that effectiveness: in the treatment review view for each acute medication and each of its periods (INV-069, OUT-021: "the same view"), next to the response comparison (INV-071), in the clinician-facing summary (INV-104), the patient-facing overview (INV-105), with a responder label (INV-062) and with a treatment line (INV-109).

#### INV-072/D02
- Kind: D
- Concerns: INV-072
- Text (v34 Notes): A summary of one formulation names at most one formulation (INV-074), which for the summaries of INV-071 is that of the medication; a summary of all formulations names every formulation of the drug that the subject has used up to the as-of date (`acuteMedications`, E-008), so that the formulation of "each acute medication it summarises" is stated (OUT-023).

#### INV-073/D01
- Kind: D
- Concerns: INV-073
- Text (v34 Notes): The type scope is tied by `onlyOfType` (E-012). A summary over all headache types of a subject who has cluster headache and also has, or may have, another type covers the attacks of all these types, which OUT-029 presents separately (INV-118 (C1-13)), so it is not a summary of cluster-headache attacks only and uses 2 hours, as for a subject who has both types. The 15-minute summaries of such a subject's cluster view (INV-088) are scoped to cluster headache.

#### INV-074/D01
- Kind: D
- Concerns: INV-074
- Text (v34 Notes): The formulations that a summary names are those it summarises (E-051), so a line that the summary lists shows one of them; a summary that names none, a deviation from the SHOULD of E-051 `formulations` for one of all formulations, constrains its lines' formulations only through INV-075. A summary of all formulations names every formulation of its drug that the subject has used (INV-072), and every line shows a formulation in which the subject has used its drug (INV-075), so in a fully conformant output the formulation of every line is among those its summary names.

#### INV-075/D01
- Kind: D
- Concerns: INV-075
- Text (v34 Notes): A treated-attack line states with which drug, and in which formulation, the patient treated the attack. The subject's acute medications are every acute medication, drug and formulation, that it has used up to the as-of date as of which the output is produced (E-007, E-008), so the line's drug and formulation are those of one of them. The relation takes only an output element and a context property as arguments, as INV-123 and INV-079 do.

#### INV-076/D01
- Kind: D
- Concerns: INV-076
- Text (v34 Notes): "For migraine" is the subject condition `hasType(ctx, c1)` for both parts of OUT-012, here and across periods (INV-118 (C1-09)), and it is the condition of `symptomStatus` (E-053). A subject with migraine may also have another headache type (OUT-029); the treated-attack lines are not assigned to headache types, because such an assignment would be a derivation from input (section 1, item 3), so every treated-attack line of a subject with migraine shows the three statuses.

#### INV-078/D01
- Kind: D
- Concerns: INV-078
- Text (v34 Notes): OUT-024 asks for "a chronological list" that shows the treatments with their details ("the list SHOULD also show the formulation"), so the groups and lines are the content of the history view, as the cycle lines are the content of the menstrual-relation view (INV-087). OUT-024 asks for no co-presence of the history with other outputs, and the view may be the only view of its output.

#### INV-078/D02
- Kind: D
- Concerns: INV-078
- Text (v34 Notes): **Order.** The order compares every two lines of a group, not only neighbouring ones, so that a line without a start date, such as the line of a course whose start the context does not state (E-055, INV-079), does not interrupt the order of the lines around it; such a line may stand anywhere in its group.

#### INV-079/Q00
- Kind: Q
- Concerns: INV-079
- Source: [S-012] — https://pmc.ncbi.nlm.nih.gov/articles/PMC9555163/
- Source: [S-013] — https://pmc.ncbi.nlm.nih.gov/articles/PMC7296705/
- Text: Stage 1 OUT-024 ("start and stop dates, dose changes, treatment duration"; "and the reason for stopping"; "For acute treatments, the list SHOULD also show the formulation of each treatment (see OUT-023), so that different formulations of the same drug can be told apart and the EHF definition of triptan refractoriness [S-012] can be applied"; [S-012] "failure to subcutaneous triptans was considered mandatory for the definition of triptan refractoriness"; for the duration of the course, [S-013] "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed.").

#### INV-079/D01
- Kind: D
- Concerns: INV-079
- Text (v34 Notes): **Duration and the course.** A line may show its duration without its start date or its stop date, which are SHOULD (E-055), so the duration is tied to the course itself, not only to the dates the line shows: where the context states the start, it is the number of days from that start to the one stop or pause of the course, its last day on treatment (section 2.8), or, for a treatment that has not stopped, to the as-of date, whichever dates the line shows. Where the line shows these dates, the conjuncts on the shown dates give the same value, because the dates it shows are those of the course events (`eventOn`). The arguments of the relation are the course events of the context and the as-of date, as for the shown dates and in INV-109; `days` is defined because no course event precedes the start and every course event lies on or before the as-of date (INV-001). The relation fixes the value of a duration that is shown; it does not require the dates to be shown with it, which E-055 asks for at SHOULD, so a line that shows its correct duration without them is not excluded (section 3.3, item 5).

#### INV-079/W01
- Kind: W
- Concerns: INV-079
- Text (v34 Notes): For example, for a course started on 1 January 2026 and discontinued on 10 February 2026, a line that shows a duration shows 41 days, also where it omits its start date, its stop date or both; for a course started on 1 January 2026 that has not stopped, as of 21 October 2026, it shows 294 days, also where it omits its start date.

#### INV-109/D01
- Kind: D
- Concerns: INV-109
- Text (v34 Notes): **Dose changes.** `doseChanges` is SHOULD whenever the treatment has a dose change (E-055), which a single shown dose change already meets; OUT-024 lists the dose changes of each treatment, so the first conjunct requires every dose change of the treatment's course (E-008), and INV-079 makes every shown dose change one of them.

#### INV-109/D02
- Kind: D
- Concerns: INV-109
- Text (v34 Notes): **Type scope.** OUT-024 asks for "the response summary from OUT-018 or OUT-023 for each treatment", and OUT-023 reports the effectiveness of an acute medication "across the attacks treated with it", so the response summaries of an acute line include one over all headache types combined; a summary of one headache type may be shown with it, but does not stand in for it.

#### INV-109/D03
- Kind: D
- Concerns: INV-109
- Text (v34 Notes): **Period.** That summary is the response summary of the treatment, the course the line lists "with start and stop dates, dose changes, treatment duration" (OUT-024); its preventive counterpart, the response comparison, is aligned to the start of the same treatment (INV-056, INV-079). So, where the treatment has a start, the summary over all headache types combined is of the span of the course: from its start to its stop (on the stop date the line shows, where it shows one) or, for a treatment that has not stopped, to the as-of date, the span of the line's duration (INV-079). A summary of another period, for example one in which the medication was not taken, may be shown with it, but does not stand in for it. A course whose start the context does not state has no stated span, as it has no stated start date or duration (E-055, INV-079). Its summary still ends with the course, on its stop date or on the as-of date, which do not depend on the start, and it begins on or before the first dated course event, so that it covers every day that the context places on the course (E-008 Notes, **Course start not stated**), not, for example, a period after the course has stopped.

#### INV-109/D04
- Kind: D
- Concerns: INV-109
- Text (v34 Notes): **Formulation.** OUT-024 asks for the formulation of each acute treatment "so that different formulations of the same drug can be told apart", and OUT-023 for the per-drug outcomes "separately for each formulation of the same drug, so that a non-response to one formulation is not read as a non-response to the drug". So, for each acute medication of the line's drug that the subject has used (E-008), the line shows a summary of the span of its course that summarises the attacks treated with it: one of all formulations of the drug, which serves every formulation, or one of that medication's formulation (`summarisesMedication`, E-051 Notes, which state the two readings of OUT-023 that this condition admits). A summary of one formulation does not stand in for another. The drug of every acute treatment is the drug of an acute medication (INV-001), so a summary is required for every acute line.

#### INV-109/D05
- Kind: D
- Concerns: INV-109
- Text (v34 Notes): **Adherence.** The line's adherence is the adherence output of OUT-039, "over the evaluation window" of the response comparison: where the line shows its response comparison, the adherence it shows is over an evaluation window of that comparison (`adherenceFor`, E-047), as INV-066 asks next to the comparison; an adherence summary of another window does not stand in for it.

#### INV-109/S01
- Kind: S
- Concerns: INV-109
- Text (v34 Notes): Satisfiability: a response comparison with 28-day baseline and on-treatment periods meets INV-055 to INV-057, INV-059 and, for children, INV-097 in any view; the line's adherence summary can be the one INV-066 asks for next to the comparison, with a window that contains one of its on-treatment periods and ends with it (`adherenceFor`, INV-067), which INV-066 places in the comparison's view, the line's view; an acute-treatment summary over all headache types combined may have 0 treated attacks (INV-072, INV-074) and has the time point of INV-073, and one of all formulations of the line's drug meets `summarisesMedication` for every acute medication of that drug, naming every formulation of it that the subject has used (INV-072); the span of a course can be shown as a period of kind `otherSpan`, which INV-002 admits for any start and end in order, and they are in order: the treatment start lies on or before every course event of the treatment and on or before the as-of date (INV-001), so the end (a stop date or the as-of date) is not before it; where the context states no start, a period from the earliest course event of the treatment (from the end itself where it has no course event) to the end is in order as well, because every course event lies on or before the as-of date (INV-001) and the stop, the end of a stopped course, is itself a course event; INV-003 and INV-011 place and qualify the periods of all of them in the line's view.

#### INV-082/Q00
- Kind: Q
- Concerns: INV-082
- Source: [S-014] — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Source: [S-101] — https://pmc.ncbi.nlm.nih.gov/articles/PMC3057423/
- Source: [S-102] — https://pmc.ncbi.nlm.nih.gov/articles/PMC4406925/
- Source: [S-103] — https://www.cincinnatichildrens.org/service/h/headache-center/pedmidas
- Text: Stage 1 OUT-026 ("Where results of validated instruments are available"; "the instrument's own published grading or categories"; [S-014] "Grading is not used by HALT-30."), OUT-036; [S-101], [S-102], [S-103], [S-014] quoted in E-057.

#### INV-082/D01
- Kind: D
- Concerns: INV-082
- Text (v34 Notes): **Grading.** The grade or category of a result is the instrument's own published grading or categories (OUT-026), so a result shows one only for an instrument whose developer publishes a grading or categories (`publishedGrading`, E-057), whatever the form of the category: never for HALT-30 ([S-014] "Grading is not used by HALT-30.", quoted in Stage 1 OUT-026), and for MSQ v2.1, M-TOQ, PGIC and other instruments as their own publications state. This too makes nothing more required: E-058 asks for a category only where `publishedGrading` holds, and no invariant asks for one elsewhere.

#### INV-083/Q00
- Kind: Q
- Concerns: INV-083
- Source: [S-104] — https://pmc.ncbi.nlm.nih.gov/articles/PMC183845/
- Text: Stage 1 OUT-033 ("report them with instrument name, date and score"); [S-104] quoted in E-059 (the HADS scores "ranged from 0 to 21 for anxiety and 0 to 21 for depression").

#### INV-083/D01
- Kind: D
- Concerns: INV-083
- Text (v34 Notes): The score of a HADS result consists of its two subscale scores, one for anxiety and one for depression ([S-104], E-059; INV-085 admits no other score for HADS), so a HADS result reported with one of them only would report half of its score; PHQ-9 and GAD-7 have one total score each (INV-085).

#### INV-085/Q00
- Kind: Q
- Concerns: INV-085
- Source: [S-104] — https://pmc.ncbi.nlm.nih.gov/articles/PMC183845/
- Source: [S-105] — https://manual.jointcommission.org/pub/BHCInstruments/RomInstr00054/instructions_PHQ.pdf
- Text: Stage 1 OUT-033 ("Where results of depression or anxiety screening instruments (for example HADS, PHQ-9, GAD-7) are available"); [S-104], [S-105] quoted in E-059.

#### INV-085/D01
- Kind: D
- Concerns: INV-085
- Text (v34 Notes): A screening result reports an available result (OUT-033; the subject's available screening results, E-008), so the tie to these results holds whether or not the result shows its date, which E-059 asks for at SHOULD. It makes nothing more required: the results that INV-083 asks for are available results.

#### INV-086/D01
- Kind: D
- Concerns: INV-086
- Text (v34 Notes): "For patients who menstruate" is read for the period the view covers (`menstruatesDuring`, E-008), not on the as-of date. A subject who menstruated during the selected time range keeps the view of that time range after menstruation has stopped, for example in pregnancy or after menopause. A time range during which the subject does not menstruate at all, for example after menopause, does not require the view. A time range that begins before the subject's first menstruation requires it, with a lead-in from its first day (E-060, INV-087). OUT-030 states no migraine condition, so the view is required whether or not the subject has migraine; see ISS-03.

#### INV-087/Q00
- Kind: Q
- Concerns: INV-087
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: Stage 1 OUT-030; OUT-035 ("where relevant, the relationship to menstruation"); [S-001] A1.1 quoted in E-060 (window "day 1 ± 2 (i.e. days −2 to +3)"; "The first day of menstruation is day 1 and the preceding day is day −1; there is no day 0").

#### INV-087/D01
- Kind: D
- Concerns: INV-087
- Text (v34 Notes): Migraine days and attacks are thus matched against the window of the line's own menstruation (its days +1 to +3) and against the window of the next menstruation (its days −2 and −1). This holds whether or not the next cycle is shown, for example when the next menstruation begins after the period the view covers, and for a lead-in that ends before the earliest day 1 the view shows. In every view, an attack mark shows the attack as in the perimenstrual window exactly when its onset lies in the window of a menstruation whose first day the view shows (as the day 1 of a line, or as the day after a line that has ended; INV-124). The exception is an attack on a line that has not ended: its mark states nothing about a menstruation that begins after the line's last day. The attack's onset lies in its line, so an onset in `nextWindowDays` is one of the line's last two days.

#### INV-088/D01
- Kind: D
- Concerns: INV-088
- Text (v34 Notes): The acute-treatment summaries are those of the selected time range, the period the view covers, so that the view shows the effectiveness of acute treatment in that time range, not in an unrelated period, as the clinician-facing summary does for its covered period (INV-104). Each refers to the covered period, which INV-003 shows in the view, so each is shown in the cluster view itself (INV-003 Notes). Each summary summarises the attacks treated with its medication (`summarisesMedication`, E-051): for a drug used both orally and subcutaneously, a summary of the oral formulation does not stand in for the subcutaneous one, and a summary of all formulations of the drug serves both.

#### INV-088/S01
- Kind: S
- Concerns: INV-088
- Text (v34 Notes): Satisfiability: a summary of the covered period may have 0 treated attacks (INV-072, INV-074); `scopeFor` implies `onlyOfType` (E-012), so INV-073 gives it the 15 minutes required here; INV-011 asks for the completeness of that period. A summary of all formulations meets `summarisesMedication` for every medication of its drug.

#### INV-089/Q00
- Kind: Q
- Concerns: INV-089
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Source: [S-007] — https://discovery.ucl.ac.uk/id/eprint/10161405/2/Matharu_IHS%20Guidelines%20for%20Clinical%20Trials%20in%20Cluster%20Headache.pdf
- Text: Stage 1 OUT-031 ("using the ICHD-3 definitions"; "attacks per day and per week during active periods"); [S-001] remission duration quoted in E-063; [S-007] quoted in E-064 for a weekly rate as an average over a longer period; OUT-029 ("When the patient has, or may have, more than one headache type") for the type scope of a rate.

#### INV-089/D01
- Kind: D
- Concerns: INV-089
- Text (v34 Notes): The rate relation compares output elements only: the rate, the length of its period (INV-002) and the attack count (E-019) of the same view, period dates and type scope, which the view shows with one number (INV-006); periods are compared by their dates, so a rate and a count, or a per-day and a per-week rate, of the same dates rest on one number whichever period atoms they refer to. Shown rates may be rounded (`≈`, section 2.7). The relation holds whatever the length of the period, for example a calendar week (where the weekly rate is the count) or a month within a bout. The rate's type scope is tied by `onlyOfType` (E-012): a rate over all types of a subject who has cluster headache and also has, or may have, another type would count attacks that the output presents under that other type (OUT-029, INV-118 (C1-13)). The remission bound (`remissionMoreThanMonths`, E-063) is that of the ICHD-3 Definitions of terms; ICHD-3 3.1.1 and 3.1.2 word the duration of a remission differently (E-063/D01); see ISS-12.

#### INV-089/D02
- Kind: D
- Concerns: INV-089
- Text (v34 Notes): **Time frame.** The last day of a period (`lastDay`, E-063) is its end date or, while it has not ended by the as-of date, the as-of date, as for a treatment that has not stopped (INV-079). The duration, the remission bound, the order of the periods and the period of a rate therefore refer to the dates of the period itself, not to its part within the period the view covers, so the remission bound is tested on the whole attack-free period (E-063 Notes). Where the covered period ends on the as-of date, the last day of an ongoing period is the last day of the covered period.

#### INV-089/S01
- Kind: S
- Concerns: INV-089
- Text (v34 Notes): Satisfiability: an end date shown is a date of the summarised diary information, which lies on or before the as-of date; `days(s, e)` is guarded by `s ≤ e` (section 2.6), which an ongoing period meets because it has started by the as-of date; and the period of a rate can be any period within its bout, for example the part of the bout within the covered period, which is not empty for every bout that overlaps the covered period, the bouts whose rates INV-088 asks for.

#### INV-110/D01
- Kind: D
- Concerns: INV-110
- Text (v34 Notes): The view summarises the diary information of the period it covers (section 3.6; INV-011 Reading), so the dates it shows are dates of that period, as the treated-attack lines of an acute-treatment summary lie in the summary's period (INV-074). Without the relation, a view could state one reporting period and show the dates of another, next to the completeness of the wrong period.

#### INV-110/S01
- Kind: S
- Concerns: INV-110
- Text (v34 Notes): Satisfiability: E-065 is MAY, and the covered period of a trigger co-occurrence view is otherwise constrained only by INV-003 and INV-011, so it can be chosen to contain every date the view shows; the annotations of INV-120 (C3-09, C3-11, C3-01, C3-05, C3-07, C3-08, C3-09, C3-10) and the definition label of INV-008 can be added whatever the covered period is.

#### INV-115/D01
- Kind: D
- Concerns: INV-115
- Text (v34 Notes): The components are declared as "the component measures shown with it" (E-033), the measures that the index combines into one score, so for an index for migraine the tie holds wherever the index shows them (section 3.3, item 5): a value of another period or type scope is not a component of the index, and would show the measures of another month, or of other headaches, as those that the score combines. It is the counterpart of the tie of a residual burden to its change (INV-061). It makes nothing more required: `components` stays SHOULD for migraine (E-033, INV-092), which also asks for the components in the index's view and for one of each dimension the index combines. The tie keeps the scope of INV-092, the indices for migraine (`concerns`, E-012), for which OUT-037 asks for the component measures; for other indices Stage 1 asks for none (OUT-037; E-033 Notes).

#### INV-115/S01
- Kind: S
- Concerns: INV-115
- Text (v34 Notes): Satisfiability: for each dimension, a per-period value of the index's period and type scope can be shown (E-012), and INV-003 and INV-011 place its period and its completeness in the view.

#### INV-094/D01
- Kind: D
- Concerns: INV-094
- Text (v34 Notes): OUT-034 places no condition on the period chosen by the clinician. The selected time range consists of whole periods of the selected granularity (INV-001), so it cannot represent a chosen period such as 15 August to 20 October (67 days); `chosenPeriod` (E-007) can, because only its end is bounded, by the as-of date.

#### INV-094/S01
- Kind: S
- Concerns: INV-094
- Text (v34 Notes): Satisfiability: INV-104 applies to a summary of any covered period (its Notes give the construction: a series of the whole periods within the covered period wherever it contains one, and the values of the covered period itself), and INV-003 and INV-011 hold with it, as for the period since the previous consultation.

#### INV-096/D01
- Kind: D
- Concerns: INV-096
- Text (v34 Notes): PedMIDAS results can be reported only where they exist; the condition is that of OUT-026 ("Where results of validated instruments are available"). The age is read on the date of each result and on the first day of each period (`childOn`, E-008), not on the as-of date: a subject who has become an adult by the as-of date keeps these outputs for the periods of its childhood, and the periods after its childhood are not asked for school days or caregiver impact. The series conjunct is required where the selected time range begins in childhood, the case in which it contains such a period.

#### INV-097/D01
- Kind: D
- Concerns: INV-097
- Text (v34 Notes): Comparisons for children of selected periods of unequal length are not required (INV-039). The age is read on the compared periods (`childIn`, E-008), not on the as-of date, so a comparison that reaches into the subject's childhood keeps equal lengths after the subject has become an adult; adding the condition only weakens the invariant, so satisfiability is kept.

#### INV-097/S01
- Kind: S
- Concerns: INV-097
- Text (v34 Notes): Satisfiable together with the other constraints on the same views in every admissible context: 28-day baseline and on-treatment periods meet INV-055 and INV-056; for the treatment review view, baseline and on-treatment periods of a common length no longer than the days of the course up to its stop or pause, where it has one, meet INV-068; for post-stop monitoring, periods of a common length no longer than the days on treatment before the changed regimen (from the treatment start, or, where the context states none, from the first dated course event, to the stop date, or to the day before a reduction) meet INV-070 and INV-112 (with no on-treatment period for a reduction on the start day, or, where the context states no start, for a reduction that no other dated course event precedes, and no baseline where the context states no original start, E-049); a change within a response comparison compares two of its periods.

#### INV-103/D01
- Kind: D
- Concerns: INV-103
- Text (v34 Notes): OUT-022 asks for the monitoring after a preventive treatment "is stopped, paused or reduced", with no condition on the start, and the view is aligned to the event (E-049 Notes, **Course start not stated**). Where the context states no start for the course, E-049 asks for the periods after the event and INV-070 for an on-treatment period wherever a course event of the course is dated before the changed regimen; no original pre-treatment baseline is asked for (E-049).

#### INV-103/S01
- Kind: S
- Concerns: INV-103
- Text (v34 Notes): Satisfiable: a view of periods of a common length, the periods after the event from the first changed day and, where asked for, an on-treatment period that ends on the day before it, meets INV-070, INV-112, INV-097, INV-003 and INV-011 (INV-070 and INV-112 Notes).

#### INV-104/D01
- Kind: D
- Concerns: INV-104
- Text (v34 Notes): Headache-free days, symptom-free days and the marks of periods without migraine days are included because OUT-034 names "frequency measures [...] (OUT-004 to OUT-009)", which includes OUT-008; see ISS-04. The covered period and each period of the series are marked as without migraine days where the summary shows 0 migraine days for them. Migraine days themselves, for the covered period and in the time course, are required for patients with migraine, the OUT-005 condition that OUT-034 keeps by its reference to OUT-005 (section 3.5), as in INV-035. A time course consists of whole periods of one granularity (E-006, INV-004). The series is tied to the period the summary covers: it consists of all whole periods of its granularity within it (`fillsPeriod`, E-006), the whole calendar months or calendar weeks within it or the consecutive 28-day periods from its first day, so it spans the covered period up to fewer days than one period at either end (for 28-day periods, at its end only), and it cannot shrink to a single period where two or more whole periods of its granularity fit in the covered period. Where the covered period is a run of whole periods of one granularity, a series of that granularity consists of exactly these periods; so for a summary of the selected time range (INV-094), a series of the selected granularity consists of the periods into which INV-001 divides it. It is monthly whenever a calendar month or 28-day period fits in the covered period (any covered period of at least 28 days contains a 28-day period), so that the monthly frequency outputs of OUT-001 and the medication-overuse indicators of OUT-016, which are given per calendar month or 28-day period, are shown for each such period. The weekly acute-medication days of OUT-015 are shown for every whole calendar week within the covered period. The period since the previous consultation may be shorter than a week, or contain no whole calendar week (INV-094 admits any previous-consultation date up to the as-of date); such a period has no time course of its own, so a series, with the marks and medication-overuse indicators of its periods, is required only when the covered period contains at least one whole period (`containsPeriodOf`, E-006).

#### INV-104/S01
- Kind: S
- Concerns: INV-104
- Text (v34 Notes): Satisfiability: a covered period of at least 28 days is filled by consecutive 28-day periods from its first day; one of 7 to 27 days that contains a whole calendar week is filled by its whole calendar weeks; INV-003 places the periods of the series, and of the spans of their overuse indicators (INV-045), in the summary. Every other component applies to any covered period, including the mark of the covered period itself and the treatment markers for every event within it. The effectiveness of each acute medication is that of the covered period, as its acute-medication days are, because OUT-034 brings its outputs together "for the period since the previous consultation (or a period chosen by the clinician)"; the response of a past acute treatment is shown by its treatment line, with the summary of its course (INV-109). Each of these summaries refers to the covered period, which INV-003 shows in the summary and for which INV-011 asks for the completeness indicator; it may have 0 treated attacks (INV-072, INV-074) and has the time point of INV-073. Each of them summarises the attacks treated with its medication, as a summary of all formulations of the medication's drug or of the medication's own formulation (`summarisesMedication`, E-051 Notes). The adherence shown for each preventive treatment is the adherence output of OUT-039, "over the evaluation window, next to the response comparison of OUT-018": that over an evaluation window of the treatment's response comparison shown in the summary (`adherenceFor`, E-047), which is also the adherence that INV-066 places next to that comparison; an adherence summary of another window does not stand in for it.

#### INV-105/D01
- Kind: D
- Concerns: INV-105
- Text (v34 Notes): Migraine days are included as OUT-035 names them, without the OUT-005 condition; see ISS-03.

#### INV-105/D02
- Kind: D
- Concerns: INV-105
- Text (v34 Notes): OUT-035 names no period, and an overview used to prepare a consultation naturally covers the period since the previous consultation, which need not be a run of whole calendar months, 28-day periods or calendar weeks (for example 10 March to 21 April, 43 days), and may be shorter than a week. The overview is therefore not required to show a series that spans its covered period exactly. It shows the four measures for the covered period itself, so that every day of that period is summarised, and, wherever the covered period contains a whole period of some granularity, their time course over a series that consists of all whole periods of its granularity within the covered period (`containsPeriodOf`, `fillsPeriod`, E-006: the whole calendar months or calendar weeks within it, or the consecutive 28-day periods from its first day), as the clinician-facing summary does (INV-104). The series is thus tied to the covered period: it spans it up to fewer days than one period at either end (for 28-day periods, at its end only), and it cannot shrink to a single period where two or more whole periods of its granularity fit in the covered period. Where the covered period is a run of whole periods of one granularity, such as the selected time range of an overview of INV-095 (INV-001), a series of that granularity spans it exactly and consists of these periods.

#### INV-105/D03
- Kind: D
- Concerns: INV-105
- Text (v34 Notes): The intensity summaries of the time course share the scale and the form of one intensity summary of the overview (`onSameScale` with `i₁`, E-023): the overview shows the pattern "over time" so that patients "can follow the effect of their treatment" (OUT-035), which a time course that changes its scale or form from one period to the next does not allow; which scale and form is the diary's choice, and INV-032 holds for summaries on any scale and in any form.

#### INV-105/D04
- Kind: D
- Concerns: INV-105
- Text (v34 Notes): A period need not contain the first day of a menstruation (for example a single calendar week), so the cycle line is required to overlap the covered period, as the cycles of the menstrual-relation view do (INV-087), not to begin in it; INV-087 also defines the cycle line in this view and requires every attack mark shown in it to be an attack of one of its cycle lines, so that an attack mark of the overview shows the attack as in the perimenstrual window exactly when its onset lies in the window of a menstruation whose first day the overview shows (as the day 1 of a line, or as the day after a line that has ended; INV-124), except for an attack on a line that has not ended, whose mark states nothing about a menstruation that begins after the line's last day. A covered period during which the subject menstruates may begin before any first day of menstruation that the overview can show (for example a month in which an adolescent's first menstruation falls, or a week for whose menstruation in progress the diary information gives no first day); a lead-in (E-060, INV-087) is then one way to meet this conjunct without a false date. "Where relevant" is read for the covered period (`menstruatesDuring`, E-008): the relationship to menstruation is asked for where the subject menstruates during that period, not for a period that lies wholly before its first menstruation or after menstruation has stopped.

#### INV-105/D05
- Kind: D
- Concerns: INV-105
- Text (v34 Notes): The effect of a preventive treatment is shown by a response comparison, which exists only for a treatment that has started (INV-056). An acute-treatment summary that shows the treatment effect is one of the covered period or of a period within it (`within`, E-005), so that the effect the patient follows is that of the period the overview shows, not of an earlier one; the covered period and the periods of its series are in the overview (INV-003), and the summary may have 0 treated attacks (INV-072, INV-074). For the same reason, a response comparison that shows the treatment effect is one of a preventive treatment taken during the covered period: its course has started on or before the last day of that period and has not stopped or been paused before its first day (`courseOverlaps`, E-067). The comparison of a treatment stopped before the covered period shows the effect of an earlier treatment, not of the treatment the patient follows in that period, and does not stand in for it. The comparison's own periods need not lie in the covered period: a treatment started before it has its baseline and its early on-treatment months before it. The preventive part of the antecedent is restricted to such treatments, so that the conjunct is required exactly where a treatment effect of the covered period can be shown. An acute-treatment summary that shows the treatment effect is one of an acute medication the subject has used, of all formulations of its drug or of its own formulation (`summarisesMedication`, E-051), not of a drug or formulation the subject has never used. For the same reason as the comparison, its drug is that of an acute treatment course taken during the summary's own period: a course that the context does not place outside that period, because it has not started after the period's last day and has not stopped or been paused before its first day (`courseNotOutside`, E-067). The subject's acute medications are every acute medication it has used up to the as-of date, including those whose use has stopped (E-008); a summary of a medication each of whose courses stopped before the summary's period or started after it shows no effect of a treatment the patient follows in that period, and does not stand in for it. Because the summary's period lies within the covered period, such a course is also not outside the covered period. The acute part of the antecedent is restricted in the same way, to acute treatment courses that the context does not place outside the covered period; a subject none of whose preventive treatments is taken during the covered period, and each of whose acute treatment courses stopped before that period or started after it, is not asked for a treatment effect of that period. Unlike a preventive course, an acute course whose start the context does not state counts as started: the effect of a preventive treatment is a response comparison aligned to its start (INV-056), while an acute-treatment summary of a period can be shown whether or not the start of the course is stated, as with the summary of an acute treatment line whose start is not stated (INV-109). Such a course is therefore excluded only where it has stopped before the period, and the treatment effect is not dropped for an acute treatment that the context does not date. Which formulations of a drug were taken during a period is stated neither by the context, whose courses are courses of a drug (`drugOf`, E-008), nor by the acute-medication days, which are given by class and by drug (OUT-014). A summary of all formulations of the drug of such a course therefore covers every formulation taken during its period, and a summary of one formulation is one of a formulation of that drug that the subject has used (`summarisesMedication`). One treatment-effect item still suffices.

#### INV-105/S01
- Kind: S
- Concerns: INV-105
- Text (v34 Notes): Satisfiability: a covered period of at least 28 days is filled by consecutive 28-day periods from its first day, one that contains a whole calendar week by its whole calendar weeks, and one that contains neither needs only the values of the covered period; INV-003 places the periods of the series in the overview, and INV-011 asks for the completeness of each of them and of the covered period.

#### INV-105/S02
- Kind: S
- Concerns: INV-105
- Text (v34 Notes): Satisfiability of the treatment-effect conjunct: where a preventive treatment is taken during the covered period, it has started (`courseOverlaps`), so a response comparison of it can be shown in the overview with its values, changes, time points and adherence (E-040 `reference`, `compared` (W2), INV-055, INV-056, INV-057, INV-059, INV-066, INV-003, INV-011); otherwise the antecedent holds only where an acute treatment course is not placed outside the covered period; the drug of that course is the drug of an acute medication of the subject (INV-001), and a summary of all formulations of that drug, of the covered period, meets the acute alternative, with 0 treated attacks where none was treated in it.

### 2.5 Traceability

No entries in v35: no reading of a Stage 1 statement is argued outside the entries of the items that realise it.

### 2.6 Stage 1 issues

#### ISS-01/Q00
- Kind: Q
- Concerns: ISS-01
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: ICHD-3 8.2.6 criterion B counts a total over named classes only: [S-001] "Regular intake of any combination of ergotamine, triptans, non-opioid analgesics and/or opioids [...] on a total of ≥10 days/month for >3 months without overuse of any single drug or drug class alone." (8.2.6, diagnostic criterion B, p. 124). Medications of 8.2.8 ("medications other than those described above") are not among these classes.

#### ISS-02/Q00
- Kind: Q
- Concerns: ISS-02
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: ICHD-3 names this class non-opioid analgesics: [S-001] "8.2.3 Non-opioid analgesic-overuse headache" (classification list, p. 12) and "For the purposes of ICHD-3, all non-opioid analgesics are regarded as a single class" (8.2.3, comments, p. 123). In the downloaded ICHD-3 text, "simple analgesics" occurs only once, in the comments on 10.1.1 High-altitude headache (section 10, p. 139). There it refers informally to drugs of the 8.2.3 class and is not the name of an 8.2 class: [S-001] "Most cases of 10.1.1 High-altitude headache respond to simple analgesics such as paracetamol (acetaminophen) or ibuprofen." (10.1.1 High-altitude headache, comments, second paragraph, first sentence, p. 139; the text layer breaks "acetaminophen" at a line end). Paracetamol is the drug of 8.2.3.1, and ibuprofen is an NSAID, a drug of 8.2.3.2: [S-001] "8.2.3.1 Paracetamol (acetaminophen)-overuse headache" and "8.2.3.2 Non-steroidal anti-inflammatory drug (NSAID)-overuse headache" (classification list, p. 12), and "ibuprofen or other NSAIDS" (7.3.2 Headache attributed to aseptic (non-infectious) meningitis, comment, p. 105).

#### ISS-03/Q00
- Kind: Q
- Concerns: ISS-03
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: OUT-030 concerns a subclassification of migraine. Its Rationale reads "Distinguishing pure menstrual from menstrually related migraine matters for treatment", and the perimenstrual window it names is that of ICHD-3 A1.1.1 Pure menstrual migraine without aura and A1.1.2 Menstrually related migraine without aura (E-060), which belong to a subclassification of migraine without aura: [S-001] "This subclassification of 1.1 Migraine without aura is clearly applicable only to menstruating women as defined above." (A1.1.3 Non-menstrual migraine without aura, comments, first sentence, p. 190; the comments follow the diagnostic criteria and note of A1.1.3, the last code of A1.1; the text layer breaks "without" at a line end). The Rationale of OUT-019 also refers to migraine: "EHF defines difficult-to-treat migraine by absolute numbers of debilitating days".

#### ISS-05/Q00
- Kind: Q
- Concerns: ISS-05
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Text: [S-010] defines its levels on one count, the days with migraine or moderate-to-severe headache: "Modest Control. This is defined as four to six days with migraine or moderate-to-severe headache per month." (section "Setting goals of migraine burden while on treatment", p. 6).

#### ISS-06/Q00
- Kind: Q
- Concerns: ISS-06
- Source: [S-008] — https://ricerca.univaq.it/retrieve/b7f186a9-06ec-4e9c-b132-4f785bbeb121/puledda-et-al-2024-international-headache-society-global-practice-recommendations-for-preventive-pharmacological.pdf
- Source: [S-014] — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Text: HURT grades its responses into areas rather than giving one total score: [S-014] "In either case, responses either fall into an area of “no concern” or are graded into one of three flagged areas indicating increasingly important treatment deficiencies; clinical advice is provided for each of latter." (quoted in Stage 1 OUT-026). PGIC is named by [S-008] among the "Patient Global Impression scales"; no source verified in Stage 2 defines a total score for it.

#### ISS-08/Q00
- Kind: Q
- Concerns: ISS-08
- Source: [S-010] — https://pubmed.ncbi.nlm.nih.gov/39980456/
- Text: [S-010] defines "Migraine Freedom", "Optimal Control", "Modest Control" and "Insufficient Control" (section "Setting goals of migraine burden while on treatment", p. 6; quoted in E-046).

#### ISS-09/Q00
- Kind: Q
- Concerns: ISS-09
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: the ICHD-3 8.2 levels to which the OUT-016 indicator refers concern the use of acute or symptomatic headache medication as such, not the medication taken for one headache type: [S-001] "[...] regular overuse of acute or symptomatic headache medication (on 10 or more or 15 or more days/month, depending on the medication) for more than three months." (8.2 Medication-overuse headache, Description, p. 122; quoted in E-032).

#### ISS-10/Q00
- Kind: Q
- Concerns: ISS-10
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Source: [S-034] — https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=169_3
- Text: NICE CG150 recommends prophylaxis for cluster headache and for chronic tension-type headache without naming a review time point: [S-015] "Consider verapamil for prophylactic treatment during a bout of cluster headache." (recommendation 1.3.39) and "Consider a course of up to 10 sessions of acupuncture over 5 to 8 weeks for the prophylactic treatment of chronic tension-type headache." (recommendation 1.3.9). The Russian paediatric clinical recommendations, which Stage 1 cites for OUT-036 (d) but not for OUT-018, name a time point for the preventive treatment of migraine in children in their flowchart for the physician: [S-034] "назначение препаратов для профилактической терапии мигрени с учетом коморбидности. Контроль эффективности терапии через 3мес." (Приложение Б "Алгоритмы действий врача", flowchart "Алгоритм диагностики и ведения пациента с мигренью", p. 52; the text layer gives the box as quoted). Translation: "prescription of medicines for the preventive therapy of migraine taking comorbidity into account. Monitoring of the efficacy of therapy after 3 months."

#### ISS-11/Q00
- Kind: Q
- Concerns: ISS-11
- Source: [S-015] — https://www.nice.org.uk/guidance/cg150/chapter/Recommendations
- Text: NICE CG150 covers "young people (aged 12 years and older) and adults" ([S-015], Overview page; quoted in E-041), and recommendation 1.3.48 stands in its section on medication overuse headache: [S-015] "Review the diagnosis of medication overuse headache and further management 4 to 8 weeks after the start of withdrawal of overused medication." (recommendation 1.3.48, quoted in Stage 1 OUT-017).

#### ISS-12/Q01
- Kind: Q
- Concerns: ISS-12
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: Definitions of terms: [S-001] "To be considered a remission, the attack-free period must exceed three months." (Definitions of terms, Cluster remission period, p. 209; quoted in E-063)

#### ISS-12/Q02
- Kind: Q
- Concerns: ISS-12
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: 3.1.1 Episodic cluster headache: [S-001] "Cluster headache attacks occurring in periods lasting from seven days to one year, separated by pain-free periods lasting at least three months." (3.1.1 Episodic cluster headache, Description, p. 42; the text layer breaks "periods" at a line end) and "At least two cluster periods lasting from seven days to one year (when untreated) and separated by pain-free remission periods of ≥3 months." (3.1.1, diagnostic criterion B, p. 42; "≥" is a glyph without a text mapping in the PDF text layer)

#### ISS-12/Q03
- Kind: Q
- Concerns: ISS-12
- Source: [S-001] — https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf
- Text: 3.1.2 Chronic cluster headache: [S-001] "Cluster headache attacks occurring for one year or longer without remission, or with remission periods lasting less than three months." (3.1.2 Chronic cluster headache, Description, p. 42) and "Occurring without a remission period, or with remissions lasting <3 months, for at least one year." (3.1.2, diagnostic criterion B, p. 42)
Two other passages describe chronic cluster headache as being without remission, in the sense of the Definitions of terms: [S-001] "About 10–15% of patients have 3.1.2 Chronic cluster headache, without such remission periods." (3.1 Cluster headache, Comments, first paragraph, second sentence, p. 42) and "The trigeminal autonomic cephalalgias are the exception: in these disorders, chronic is not used until the disorder has been unremitting for more than one year." (Definitions of terms, Chronic, last sentence, p. 209). The diagnostic criteria of 3.1.1 and 3.1.2 are quoted only for the duration they give remission periods; the model applies no diagnostic criterion (section 1).

### 2.7 Source data rows

No entries in v35: the quotes of each source data row are in the entries that its Rationale cell names (model section 11); those entries name the rows under Concerns.

### 2.8 Merged invariants

#### INV-118/D01
- Kind: D
- Concerns: INV-118; v34 INV-016; v34 INV-017; v34 INV-108
- Text (v34 INV-016 Notes): SHOULD is the level of OUT-006 for providing the measure at all. Wherever the diary provides it, its availability per calendar month or 28-day period is MUST (INV-118 (C1-04, C1-06), OUT-001; section 3.4).
- Text (v34 INV-017 Notes): SHOULD is the level of OUT-007 for providing the measure at all. Wherever the diary provides it, its availability per calendar month or 28-day period is MUST (INV-118 (C1-04, C1-06), OUT-001; section 3.4).
- Text (v34 INV-108 Notes): The SHOULD of OUT-006 and OUT-007 governs whether the diary provides these measures at all (INV-118 (C1-03, C1-05)); the MUST of OUT-001 governs their availability per calendar month or 28-day period once they are provided (section 3.4). Each measure may use its own monthly granularity. `provides(K)` is the "where provided" of section 3.5, as in INV-118 (C1-13), INV-037 and INV-057. The invariant is placed with INV-118 (C1-03, C1-05), whose measures it concerns.

#### INV-118/D02
- Kind: D
- Concerns: INV-118; v34 INV-028
- Text (v34 INV-028 Notes): Migraine days are by definition migraine-specific and are not broken down further by type. "Acute medication outputs" is read as the acute-medication days of OUT-014 (total, per class and per drug); the weekly view (OUT-015, INV-118 (C1-11)) and the medication-overuse indicator (OUT-016, INV-044) are required for all headache types combined; see ISS-09.

#### INV-119/D01
- Kind: D
- Concerns: INV-119; v34 INV-101
- Text (v34 INV-101 Notes): The negative counterpart of the caveat of C3-01: an output that carried the caveat and at the same time claimed to replace clinical assessment or to make a diagnosis would contradict itself. C2-08 (SHOULD NOT, OUT-028), C2-04 (MUST NOT, OUT-016) and C2-09 (SHOULD NOT, OUT-033) state the same prohibition for particular outputs, C2-04 at the stronger level that OUT-016 requires; they are consistent with the general one (C2-01). C2-05 (MUST NOT, OUT-018) and C2-07 (SHOULD NOT, OUT-023) prohibit two particular decisions that Stage 1 leaves to the reader.

#### INV-119/D02
- Kind: D
- Concerns: INV-119; v34 INV-106
- Text (v34 INV-106 Notes): The level is MUST NOT because the prohibition is the negative form of a Caveat of OUT-018, whose strength is MUST (section 3.3, item 6); OUT-020 (SHOULD) states the same in its Rationale and is the second part cited. A responder or control-level label (E-046) classifies the response under a named criterion; it is not a continuation decision, so this invariant does not restrict the labels that OUT-020 permits.

#### INV-119/D03
- Kind: D
- Concerns: INV-119; v34 INV-107
- Text (v34 INV-107 Notes): The level is SHOULD NOT, the negative form of a Caveat of OUT-023, whose strength is SHOULD (section 3.3, item 6).

#### INV-120/Q00
- Kind: Q
- Concerns: INV-120; v34 INV-100
- Source: [S-014] — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Text: Stage 1 OUT-038 ("indicators such as possible medication overuse (OUT-016), responder labels (OUT-020) and trigger associations (OUT-032) require clinical interpretation"); OUT-026 ([S-014] "Grading has value in indicating the level of a patient’s personal need and, perhaps, priority for treatment."; the HURT areas "indicating increasingly important treatment deficiencies"); OUT-033 Caveats ("A high HAD score is not specific"; "The output therefore reports scores as screening results, not as psychiatric diagnoses (see OUT-038)").

#### INV-120/D01
- Kind: D
- Concerns: INV-120; v34 INV-098
- Text (v34 INV-098 Notes): The paediatric outputs of the OUT-036 Caveat are read as the views that show a period that begins, or an instrument result completed, while the subject is a child or adolescent (`childIn`, `childOn`, E-008), whatever the subject's age on the as-of date. A view's content is not confined to its covered period: it shows every period its items use (INV-003), for example the baseline of a response comparison, which lies before the treatment start (INV-056). So the antecedent covers each output of OUT-036 wherever it is shown: (a) a PedMIDAS result completed in childhood or adolescence; (b) school days and caregiver impact, which are values of periods that begin then (INV-096) and whose periods the view shows; (c) and (d) a comparison or change that reaches into childhood or adolescence, to which INV-097 applies, including the response comparison of a treatment started then, whose periods the view shows, also in a clinician-facing summary of a later period. The covered period is named in the predicate, so the invariant holds for a view whose covered period begins in childhood or adolescence independently of INV-003.

#### INV-120/D02
- Kind: D
- Concerns: INV-120; v34 INV-100
- Text (v34 INV-100 Notes): OUT-038 names its three indicators as examples ("such as"). The model reads an indicator as an output element that points the reader to a possible clinical condition, or that classifies the subject's state under a criterion or a published grading. Besides the three, these are the grade or category shown with a validated instrument's result (E-058), which [S-014] describes as "indicating" the patient's need for care, and a screening result for depression or anxiety (E-059), which OUT-033 reports "as screening results" with reference to OUT-038. The other elements of the model report counts, durations, scores without a category, dates or coverage, or place a date against a stated window: for example the completeness indicator (E-013) states how completely a period is covered by diary information, so that readers can judge the reliability of its measures (OUT-003), not a clinical finding; an attack mark (E-061) places an attack's onset against the perimenstrual window; cluster periods and remission periods (E-063) state the dates and durations of periods under the ICHD-3 definitions of terms, as headache days state days under them; and the three-month pattern view (E-038) names the codes it refers to and assigns no diagnosis (INV-119 (C2-08)). Every element kind that shows the three named indicators is covered: the medication-overuse indication is shown only by the indicator (E-032), a responder or control-level label only by a responder label (E-046), and trigger associations only by the trigger co-occurrence view (E-065); other content is an `OtherItem` (section 3.7). Every view also carries the caveats of INV-120 (C3-01).

#### INV-120/S01
- Kind: S
- Concerns: INV-120; v34 INV-098
- Text (v34 INV-098 Notes): Satisfiability: an annotation can be added to any view (E-010 `qualifies` (W2)), and INV-120 (C3-01) already annotates every view.

#### INV-123/D02
- Kind: D
- Concerns: INV-123; v34 INV-117
- Text (v34 INV-117 Notes): A label classifies the response to a preventive treatment (E-046), the response that OUT-018 compares with the pre-treatment baseline and to which its underlying values belong, so the tie holds wherever a label is shown (section 3.3, item 5): a label of a treatment that the subject does not have, or of an acute treatment course, would classify as "responder", "non-responder" or a control level the response of a preventive treatment that did not take place. It is the counterpart of the ties of the other elements that show a treatment: a marker (INV-123), an evaluation time point (INV-058), an adherence summary (INV-067), a treatment line (INV-079) and a post-stop monitoring view (INV-112) show a treatment of the subject wherever they are shown, and a response comparison (INV-056) and a treatment review view (INV-068) do so at MUST. It makes nothing more required: labels stay optional (E-046). In a fully conformant output it changes nothing: a label that meets INV-062 shows a response comparison, which is one of the label's treatment (INV-114) and one of the subject's preventive treatments (INV-056).

#### INV-123/D06
- Kind: D
- Concerns: INV-123; v34 INV-113
- Text (v34 INV-113 Notes): The view is the follow-up of a withdrawal of the subject (E-039 Meaning), so the tie holds wherever the view is shown (section 3.3, item 5): a view of a withdrawal that did not take place would show, for that withdrawal, a NICE CG150 1.3.48 review window (INV-051) and the label of the expected transient worsening (INV-120 (C3-06)). It makes nothing more required. The covered period that begins on the start of withdrawal, the series of whole periods from it and the review window are the content that OUT-017 asks for "from the start of withdrawal onward", and stay at its level (INV-050); a view that deviates from them still states its covered period and its start of withdrawal truly (INV-003 and this invariant).

#### INV-123/S01
- Kind: S
- Concerns: INV-123; v34 INV-117
- Text (v34 INV-117 Notes): Satisfiability: labels are optional, and a responder or non-responder label can refer to any preventive treatment of the subject; a control-level label only to one that has a whole monthly period on treatment (INV-064).

#### INV-123/S02
- Kind: S
- Concerns: INV-123; v34 INV-113
- Text (v34 INV-113 Notes): Satisfiability: every view that INV-049 asks for shows a start of withdrawal of the subject (`v.withdrawalStart = ws`).

## 3. Search log

The search log of v34 (model section 11 of v34), verbatim, one entry per paragraph, table or iteration.

#### SL-001
Search date: 2026-10-21. Tools: direct download with `curl` through the configured proxy; PubMed E-utilities (esearch, esummary, efetch); Europe PMC REST API (full-text XML); general web search; text extraction with `pdftotext` and Python `pypdf`. Every new quote in sections 5 and 8 was checked by script against the text downloaded from the URL listed in section 10 (or, for S-001, S-007, S-008, S-010 and S-014, in Stage 1 section 5), with whitespace, ligatures, line-end hyphens and glyphs without a text mapping (ICHD-3: "≥", "±", "−") normalised. One sentence of [S-010] is interrupted in the PDF text layer by a running header at a column break and was checked in its two parts.

#### SL-002
| Language / region | Queries and sites | Found and used | Found but not used, not found, or unreachable |
|---|---|---|---|
| English — classification standard | ichd-3.org (ICHD-3 PDF, the Stage 1 URL of S-001); page-by-page search of the text layer for 8.2 and its subtypes, appendix A1.1, and "Definitions of terms". | [S-001] code labels (pp. 8, 9, 12), reference levels and time span of 8.2 and its subtypes (pp. 122–125), the perimenstrual window of A1.1.1 and A1.1.2 (p. 190), the duration of a cluster remission period (p. 209). | The "≥", "±" and "−" signs are glyphs without a text mapping in the PDF text layer; quotes give the signs as printed. "Simple analgesics" occurs only in section 10 (ISS-02). |
| English — IHS practice recommendations and position statement | ricerca.univaq.it PDFs of S-008 and S-010 (Stage 1 URLs). | [S-008] Q6: the chronic-migraine 30 % alternative and the MIDAS and HIT-6 thresholds (pp. 12–13). [S-010]: the four control levels (p. 6). | The AHS consensus statement that IHS Q6 cites for the MIDAS and HIT-6 thresholds (its reference 9) was not retrieved; the Stage 1 search log notes that Wiley returns HTTP 403 for AHS full texts. |
| English — MIDAS | PubMed: "Stewart WF[au] AND Lipton RB[au] AND MIDAS[ti]" (6 results); Europe PMC: "MIDAS AND AUTH:\"Stewart WF\" AND OPEN_ACCESS:y" (4 results); neurology.org (S-044 full text); web search "MIDAS questionnaire pdf Grade I Little or no disability Grade IV". | [S-102] (open access, MIDAS developers as co-authors): grade labels with score bands, recall period. | S-044 full text: neurology.org returned HTTP 403; Lipton et al. 2001 (Headache, PMID 11703471) and Stewart et al. 2000 (Pain, PMID 11098098): not open access. Other developer-co-authored open papers use other labels: PMC8684566 (2021, "little or none", "mild", "moderate", "severe") and PMC6537129 (2019, "minimal or infrequent disability", grades IVa and IVb); noted in E-057 Notes. headaches.org MIDAS form: HTTP 403 (also with a browser user agent); migrainecanada.org: HTTP 429; a hospital copy of the form (scripps.org) was downloaded but not used, being a third-party adaptation. |
| English — HIT-6 | PubMed: "Kosinski M[au] AND HIT-6[ti]" (3 results). | [S-101] (open access, co-authored by a HIT-6 developer): score range and the four impact categories with their bands. | Kosinski et al. 2003 (Qual Life Res, PMID 14651415): not open access. Rendas-Baum et al. 2014 (PMC4243819): found, not needed. The HIT-6 form itself is copyrighted and was not retrieved; the recall period follows Stage 1 ([S-002]). |
| English — PedMIDAS | PubMed: "Hershey AD[au] AND PedMIDAS[tiab] AND 2001[dp]" (1 result); web search "PedMIDAS questionnaire Cincinnati Children's grading". | [S-103] (developers' institution): the four disability grades with score ranges. | Hershey et al. 2001 (Neurology, PMID 11739822): not open access. NIH common-data-element form (nih.gov .docx): found, not used. No upper bound of the PedMIDAS score was found in a developer source; none is stated. |
| English — HALT and HURT | Europe PMC full texts of S-014 (Stage 1 source), PMC5796955 (HALT indices, 2018) and PMC5812954 (HURT, 2018). | [S-014]: HALT-90 and HALT-30 recall, units and the HALT-90 grading table. | The two 2018 developer papers print the same HALT-90 table and HURT description; not cited separately. HURT has no total score in these sources (ISS-06). |
| English — MSQ v2.1, M-TOQ, PGIC | PubMed: "\"Migraine-Specific Quality of Life\" AND (version 2.1 OR v2.1) AND (Martin BC[au] OR Jhingran P[au])" (1 result: Martin et al. 2000, Headache, PMID 10759923); "Lipton RB[au] AND Migraine Treatment Optimization Questionnaire[tiab]" (first 15 results reviewed). | — | MSQ v2.1 and M-TOQ developer papers are not open access (Wiley; SAGE returned HTTP 403 in Stage 1). PGIC exists in several versions with different wordings. Their value sets are therefore not tabulated; results show the instruments' own published scores and categories by name (E-057). |
| English — HADS, PHQ-9, GAD-7 | PubMed: "Snaith RP[au] AND Hospital Anxiety and Depression Scale[ti]"; "Kroenke K[au] AND Spitzer RL[au] AND PHQ-9[ti] AND 2001[dp]"; "Spitzer RL[au] AND GAD-7[ti] AND 2006[dp]"; pmc.ncbi.nlm.nih.gov; europepmc.org; phqscreeners.com; web search "phqscreeners.com instruction manual PHQ-9 GAD-7". | [S-104]: HADS subscale ranges. [S-105]: PHQ-9 and GAD-7 score ranges. | Kroenke et al. 2001 (PMC1495268): Europe PMC lists it as not open access and its PDF render returned HTTP 403; pmc.ncbi.nlm.nih.gov returned a browser-check page. Spitzer et al. 2006 (Arch Intern Med, PMID 16717171): not retrieved. phqscreeners.com: home page reached, no link to the manual found; the developers' manual was taken from the copy hosted by The Joint Commission. Zigmond and Snaith 1983 (PMID 6880820): not open access. |
| German | Web search "HIT-6 Auswertung Punktwert 36 bis 78 Kategorien \"schwere Beeinträchtigung\" Kopfschmerz Fragebogen". | — | No German-language source returned; results were English trial protocols that state the same HIT-6 range and categories as [S-101]. The DMKG/ÖKSG/SKG thresholds are those of S-023, quoted in Stage 1. |
| French, Italian | Web search "questionnaire MIDAS grade I II III IV score 0-5 6-10 11-20 21 handicap migraine interprétation". | — | French and Italian copies of the MIDAS form (for example aslroma1.it) use the same score bands with translated labels; not used, because the model states the labels of the developer-co-authored English source. |
| Spanish | Web search "PedMIDAS grados discapacidad 0-10 11-30 31-50 >50 cuestionario migraña infantil validación española". | — | No Spanish PedMIDAS validation with grade labels found; a Spanish MIDAS validation (PMC7038557) was found and not needed. |
| Other languages | — | — | The value sets added in Stage 2 are defined by English-language standard owners and instrument developers; national-language versions are translations with the same score bands. Stage 1's multilingual sources (for example S-023, German; S-033, Russian) are reused by their Stage 1 quotes for responder criteria (E-045). No further languages were searched in this iteration. |

#### SL-003
Iteration 01 (fix, 2026-10-21): no new searches. To verify review remarks, the following were downloaded again with `curl` into a fresh directory outside the repository and checked by script: the Stage 1 URLs of [S-028] (NVN module page, HTTP 200; the Aanbeveling contains the OUT-018 quote and begins with the advice to start prophylactics low and titrate slowly), [S-033] (official PDF, 92 pages; the OUT-018 quote is in section 7.1 "Оценка эффекта проводимой терапии", p. 53) and [S-001] (8.2 Description, p. 122); the Europe PMC full texts of [S-014], [S-101] and [S-102]; the [S-103] page; and the [S-105] PDF (the developers sentence is on page "P.8/9"). No new source was added.

#### SL-004
Iteration 02 (fix, 2026-10-21): no new searches and no new source; the iteration 02 remarks concern the formal model. To verify them, the Stage 1 URL of [S-015] (NICE CG150 recommendations page, HTTP 200) was downloaded again with `curl` into a fresh directory outside the repository: recommendation 1.3.29 reads "after 2 treatment cycles", the time point that `ruleNice1329` anchors at the end of the second cycle with no further offset. The [S-001] PDF (211 pages) was downloaded again and page 190 extracted: the A1.1.1 window and note 2 used by INV-087 are as quoted in E-060.

#### SL-005
Iteration 03 (fix, 2026-10-21): no new searches and no new source. To verify the review remarks, the Stage 1 URL of [S-001] (ICHD-3 PDF, 211 pages, HTTP 200) was downloaded again with `curl` into a fresh directory under `/tmp`, outside the repository, and pages 122–125 and 190 were extracted with `pdftotext`. The full 8.2.3 comment on cumulative use of non-opioid analgesics (p. 123), quoted in INV-046, was checked by script and is verbatim apart from line-end breaks in the text layer; 8.2.6 criterion B and note 2 (pp. 124–125), 8.2 note 2 (p. 122) and the A1.1.1 window and note 2 (p. 190) read as quoted in E-028, Stage 1 OUT-016 and E-060. No source was found or searched for the response categories of PGIC: the model leaves its grading to the version used, as for MSQ v2.1 and M-TOQ (row "MSQ v2.1, M-TOQ, PGIC" above; E-057).

#### SL-006
Iteration 04 (fix, 2026-10-21): no new searches and no new source. To verify the review remarks, the following were downloaded again with `curl` into a fresh directory under `/tmp`, outside the repository, and extracted with `pdftotext` (`-raw` and `-layout`): the Stage 1 URLs of [S-010] (univaq PDF, HTTP 200, 11 pages), [S-002] and [S-003] (ihs-headache.org PDFs, HTTP 200), [S-008] (univaq PDF, HTTP 200) and [S-001] (ICHD-3 PDF, HTTP 200).
- [S-010], section "Setting goals of migraine burden while on treatment", p. 6. The paragraph directly after the four control levels states that their assessment requires a definition of migraine day and that the panel adopts three definitions of its own. The next paragraph includes moderate-to-severe headache days "as a proxy of migraine days". The two sentences quoted in E-018 were checked by script, with line-end breaks and the "ﬁ" ligature normalised.
- [S-002] sections 1.3.1.1 and 1.3.1.2 (p. 1035) and [S-001] 1.1 criteria C and D (p. 19) define migraine days differently from [S-010], which confirms that the definitions count different days (INV-031).
- [S-008] states no definition of a migraine day of its own (text searched for "migraine day" near "defin").
- The [S-001] A1.1.1 window and note 2 (p. 190) read as quoted in E-060.

#### SL-007
Iteration 05 (fix, 2026-10-21): no new searches and no new source. To verify the review remarks, the following were downloaded again with `curl` into a fresh directory under `/tmp`, outside the repository, and extracted with `pdftotext` (`-raw` and `-layout`) or, for the Europe PMC full text, with the markup removed:
- [S-008] (univaq PDF, HTTP 200), Q5 and Q6, pp. 11–13. The Q6 success criteria are those "that determine whether preventive therapy is effective", and the MIDAS improvement is measured from the "baseline score" (quoted in Stage 1 OUT-020 and in E-045); the Q6 Background places the evaluation after an evaluation period of two to three months. This supports the reading of score components in E-046.
- [S-023] (Europe PMC full text of PMC9607711 through its REST API, HTTP 200): the Stage 1 OUT-020 quote with "sinkt" (falls) reads as quoted.
- [S-007] (UCL Discovery accepted manuscript, HTTP 200, 39 pages; PDF page = manuscript page). The new fragment quoted in E-064 ("≥ 14 attacks per week on average", section 2.2, p. 10) was found verbatim. The Stage 1 OUT-031 quotes "Number of attacks per day during the study period" (p. 22) and "the number of weekly attacks for the entire double-blind phase" (p. 25) were found as well.
- [S-001] (ICHD-3 PDF, HTTP 200): downloaded for reference; no new quote.

#### SL-008
Iteration 06 (fix, 2026-10-21): no web search and no new source. To verify the review remark and to state the population of each evaluation rule (E-041), the Stage 1 sources of the rules were downloaded again with `curl` into a fresh directory under `/tmp`, outside the repository, and extracted with `pdftotext` (`-raw` and `-layout`) or, for web pages, with the markup removed. Every new quote was checked by script, with whitespace and non-breaking spaces normalised.
- [S-015] NICE CG150: the Recommendations page (Stage 1 URL, HTTP 200) and the Overview page https://www.nice.org.uk/guidance/cg150 (HTTP 200). The Overview states the population (young people aged 12 years and older and adults). In the Recommendations, 1.3.27–1.3.29 stand under "Migraine with or without aura" and "Prophylactic treatment review"; 1.3.24 and 1.3.26 recommend CGRP inhibitors and botulinum toxin type A "in adults"; 1.3.9 (chronic tension-type headache) and 1.3.39 (cluster headache) recommend prophylaxis without a review time point (ISS-10); 1.3.48 is in the section on medication overuse headache (ISS-11).
- [S-018] AAN/AHS 2026 Clinician Summary (Stage 1 URL, HTTP 200; the URL returns a 12-page PDF): title and first sentence name the guideline "Pharmacologic Treatment for Migraine Prevention in Adults"; 14A reads as quoted in Stage 1.
- [S-016] SIGN 155 (Stage 1 URL, HTTP 200): section 1.2.1 "Overall objectives" (PDF p. 7, printed p. 1) states adults with migraine, and that the recommendations could be considered for adolescents.
- [S-011] EHF 2022 guideline (Europe PMC full text of PMC9188162 and the PMC page, HTTP 200): the Background describes the 2019 guideline as one "for migraine prevention in adults" and the 2022 guideline as its update; its questions name "individuals with migraine" and no age.
- [S-008] IHS 2024 practice recommendations (Stage 1 URL, univaq PDF, HTTP 200): the Q2 heading (p. 9) concerns migraine preventive treatment and states no age; Q13 (p. 17) addresses children and adolescents.
- [S-028] NVN module "Profylactische behandeling migraine" (Stage 1 URL, HTTP 200): the PICO of section "Zoeken en selecteren" names "Patiënten (kinderen en volwassenen) met migraine", and the Aanbeveling has titration schedules for children and for adults.
- [S-033] Russian adult clinical recommendations (Stage 1 URL; the connection was reset by the peer twice, and the official PDF, 92 pages, was downloaded on the third attempt): title page "Возрастная категория: взрослые".
- [S-034] Russian paediatric clinical recommendations (Stage 1 URL, HTTP 200): the flowchart of Приложение Б (p. 52) names a time point for preventive therapy of migraine in children (ISS-10); section 7.1 (p. 34) reads as quoted in Stage 1 OUT-036.

#### SL-009
Iteration 07 (fix, 2026-10-21): no web search and no new source. To verify the review remarks and to complete the evaluation rules of E-041, the Stage 1 sources cited for OUT-018, and the paediatric sources cited for OUT-036 (d), were downloaded again with `curl` into a fresh directory under `/tmp`, outside the repository (all HTTP 200), and extracted with `pdftotext` (`-raw` and `-layout`) or, for web pages and the Europe PMC full text, with the markup removed; the image-only title page of [S-034] and page 48 of [S-035] were rendered and read. Every new quote was checked by script against these texts, with whitespace, quotes, dashes and line-end hyphens normalised. The section of each source on the evaluation and duration of preventive treatment was read in full, and every time point it names was listed and classified (fixes/fix-iter-07.md, completeness sweep):
- [S-018] AAN/AHS 2026 Clinician Summary (12-page PDF): recommendations 14A–14H (pp. 7–8) and 17A–17B (p. 9). New rule from 14B (24 weeks at the recommended dose, onabotulinumtoxinA); 14H refers to "12–24 weeks (see 14A and 14B)".
- [S-008] IHS 2024 (univaq PDF, 31 pages): Q2–Q13 (pp. 9–17). New rule from the first Q2 Optimal sentence and the Q2 Essential sentence (three months at the target dose, oral preventives).
- [S-011] EHF 2022 (Europe PMC full text of PMC9188162 and the PMC page): expert consensus statements 1–7 and the clinical guidance of questions 3 and 4. No new rule. The two Background paragraphs quoted in E-041 are the first and the second paragraph of the section (Par12 and Par13 in the Europe PMC full text; two separate paragraphs on the PMC page).
- [S-015] NICE CG150 recommendations page: all recommendations naming weeks, months or cycles. No new rule.
- [S-016] SIGN 155 (64-page PDF): every page searched for weeks, months and cycles; section 4.1 (p. 14), the key recommendations (p. 5), section 4.6 on botulinum toxin A (p. 18) and the patient checklist of section 7.3 (pp. 34–35). No new rule.
- [S-028] NVN module "Profylactische behandeling migraine" (web page): Aanbeveling and Overwegingen. No new rule.
- [S-033] Russian clinical recommendations for adults (92-page PDF): sections 3.3 (pp. 38–42) and 7.1 (p. 53), list of abbreviations (pp. 4–5). New rule from the section 3.3 comments (botulinum toxin type A, a minimum of 6 months); "БТА" is not in the list of abbreviations.
- [S-035] Turkish Ministry of Health Migraine Clinical Protocol (92-page PDF): sections 3.6.2 and 3.6.3 (PDF pp. 47–57) and section 6 on children and adolescents (PDF pp. 77–80). New rules from Box 8 (at least 2–3 months for efficacy) and section 3.6.3.9 (onabotulinumtoxinA after 3 injection cycles).
- [S-034] Russian clinical recommendations for children (53-page PDF): sections 3 and 7.1 (pp. 23–34), the flowchart of Приложение Б (p. 52), the patient information (p. 53) and the title page (an image, which reads "Возрастная группа" followed by "дети"). New rule from the flowchart (3 months).
- [S-002] and [S-005] IHS trial guidelines for adults and for children (ihs-headache.org PDFs): sections on treatment phases, endpoints and analysis periods. Trial-design durations only; no rule.
- [S-029] NVN module "Migraine: Monoklonale antilichamen" (web page), a Stage 1 source not cited for OUT-018, was read to check the boundary of the sweep: its time points (two months for topiramate or valproate, at least six months for onabotulinumtoxine type A) are insurer conditions for reimbursement (the context of OUT-025); not used.

#### SL-010
Iteration 08 (fix, 2026-10-21): no web search. One new source, [S-106] (NICE technology appraisal guidance TA260), reached through the link that NICE CG150 recommendation 1.3.26 [S-015] gives "For full details". The following were downloaded with `curl` into a fresh directory under `/tmp`, outside the repository (all HTTP 200), and extracted with `pdftotext` (`-raw` and `-layout`) or, for web pages, with the markup removed. Every new quote was checked by script against these texts, with whitespace, non-breaking spaces and quotes normalised.
- [S-035] Turkish Ministry of Health Migraine Clinical Protocol (92-page PDF): Kutu 8 (PDF p. 48), whose second item states the criterion "Ölçüt atak sıklığında en az %50 azalma olması" (E-045); section 3.6.3.9 (PDF p. 57), which gives the injections of onabotulinumtoxinA "3 ayda bir" (every 3 months) (E-041); Table 6 (PDF p. 52) gives the same interval as "12 haftada bir" (every 12 weeks).
- [S-015] NICE CG150 Recommendations page ("Last updated: 03 June 2025"): 1.3.26 refers to TA260 for full details; 1.3.27 to 1.3.29 read as quoted.
- [S-106] NICE TA260: the overview page (published 27 June 2012, last reviewed 11 January 2016), section 1 (recommendation 1.2 stops the treatment at "less than a 30% reduction in headache days per month after 2 treatment cycles", which CG150 1.3.29 restates) and section 2 "The technology" (re-treatment every 12 weeks).
- [S-018] AAN/AHS 2026 Clinician Summary (12-page PDF): 14A, 14B and 14H read as quoted in Stage 1 and in E-041.

#### SL-011
Iteration 09 (fix, 2026-10-21): no web search and no new source. To verify the review remark and to read the measure of each responder criterion in its own source, the following Stage 1 sources were downloaded with `curl` into a fresh directory under `/tmp`, outside the repository (all HTTP 200), and extracted with `pdftotext` (`-raw` and `-layout`) or, for the web page and the Europe PMC full text, with the markup removed. Every new quote was checked by script against these texts, with whitespace normalised.
- [S-035] Turkish Ministry of Health Migraine Clinical Protocol (92-page PDF): Kutu 8 (PDF p. 48) reads as quoted in E-045. Section 3.3 "Farmakolojik Tedavi", item "b. Profilaksi" (PDF p. 23, printed p. 13), states that preventive treatment of migraine aims to reduce "migren ataklarının sıklığını" (the frequency of migraine attacks), the attacks whose frequency the Box 8 criterion counts (new quote, E-045). Section 3.6 (PDF p. 44) and Kutu 1 name the attack frequency of migraine patients in the same sense.
- [S-015] NICE CG150 Recommendations page: 1.3.28 ("the frequency of migraines") and 1.3.29 ("the frequency of headache days per month").
- [S-008] IHS 2024 (univaq PDF, 31 pages): Q6, "monthly migraine days or moderate-to-severe headache days" (p. 12).
- [S-023] DMKG/ÖKSG/SKG (Europe PMC full text of PMC9607711): "die Migränetage".
- [S-033] Russian clinical recommendations for adults (official PDF, 92 pages): section 7.1, "число дней с ГБ" (p. 53).
- [S-010] IHS position statement 2025 (univaq PDF, 11 pages): the control levels rest on "days with migraine or moderate-to-severe headache" of the person (p. 6).
- [S-030] Danish reference programme (PDF, 86 pages): "hyppigheden eller styrken af migræne" (PDF p. 19), a criterion restricted to migraine.
- [S-001] ICHD-3 (PDF, 211 pages): downloaded for reference; no new quote.

#### SL-012
Iteration 10 (fix, 2026-10-21): no web search, no download and no new source. The two remarks of re-check 10b concern a conformance level and two explanatory paraphrases of a predicate; they were verified against the Stage 1 v18 text in the repository (OUT-018 to OUT-020, OUT-022, OUT-025, OUT-029, OUT-035 and OUT-036) and against v09 itself. No quote was added or changed.

#### SL-013
Iteration 11 (fix, 2026-10-21): no web search, no download and no new source. The three remarks of review 11 concern the co-presence of the parts of an item in its view, the quantifier of a presence requirement and the range of a context component; they and the three whole-model sweeps were verified against the Stage 1 v18 text in the repository and against v10 itself (`history/v10.md`), with a small instance check of the co-presence scenarios. No quote was added or changed: the Evidence of INV-062, INV-083 and E-045 cites fragments of quotes already given and verified in E-046 ([S-010], the optimal-control level) and E-059 ([S-104], the HADS score ranges).

#### SL-014
Iteration 12 (fix, 2026-10-21): no web search and no new source. The two remarks of review 12 and the two whole-model sweeps (time frames of the context components; triggers of the cross-cutting requirements) were verified against the Stage 1 v18 text in the repository and against v11 itself (`history/v11.md`). The new reading of the conditions of responder criteria (E-045, read on the treatment a label refers to) rests on wording that the model already quotes; it was re-checked at the source. The Stage 1 URLs of [S-015] (NICE CG150 Recommendations page, HTTP 200) and [S-008] (univaq PDF, HTTP 200) were downloaded with `curl` into a fresh directory in the session scratchpad, outside the repository, and searched after the markup was removed ([S-015]) or after `pdftotext -layout` ([S-008]). Recommendation 1.3.24 ("For CGRP inhibitors recommended as options for preventing episodic or chronic migraine in adults"), 1.3.26 ("recommended as an option for preventing chronic migraine in adults"), 1.3.28 ("at least 50% in episodic migraine", "at least 30% in chronic migraine") and the IHS Q6 sentence that ends "is acceptable for treatment continuation beyond three months" read as quoted. No quote was added or changed: every quoted fragment of the new text occurs verbatim in Stage 1 v18 or in a quote of the model that review 12 verified (checked by script).

#### SL-015
Iteration 13 (fix, 2026-10-21): no web search, no download and no new source. The three remarks of review 13 concern the type scope of required values, the trigger of the paediatric caveat and the dates of the trigger co-occurrence view; they were verified against the Stage 1 v18 text in the repository and against v12 itself (`history/v12.md`). No quote was added or changed: every quoted fragment of the new text occurs verbatim in Stage 1 v18 (checked by script).

#### SL-016
Iteration 14 (fix, 2026-10-21): no web search and no new source. To verify remark R14-01, the Stage 1 URL of [S-035] (Turkish Ministry of Health Migraine Clinical Protocol, 92-page PDF, HTTP 200, created 28 August 2025) was downloaded with `curl` into a fresh directory under `/tmp`, outside the repository, and extracted page by page with `pdftotext` (`-raw` and `-layout`); PDF pages 57, 82, 83 and 86 were also rendered with `pdftoppm` and read.
- Chapter 7 "MİGRENDE GİRİŞİMSEL İŞLEMLER" (PDF pp. 82–86, interventional procedures), which the earlier sweeps of the protocol (iterations 07 to 09: sections 3.3, 3.6.2, 3.6.3 and 6) had not covered, was read in full. Section 7.3 "Botulinum Toksin Enjeksiyonu" (PDF p. 86) gives the dose and the 3-month interval of the injections, the evaluation after at least 2 administrations (new rule `ruleTr73`, E-041) and the longer intervals after one year; section 7.1 (PDF p. 83) gives the schedule of greater occipital nerve blocks and the check that a block has taken effect (E-041 Notes, not evaluation time points). The rendered p. 86 prints "2 k ez" with a space, as the text layer does.
- Section 3.6.3.9 (PDF p. 57) gives the same dose, 155 units at 31 standardised points, for onabotulinumtoxin A (E-041 Evidence).
- The whole text was searched for "değerlendir" (evaluate), "en az" (at least), "ay sonra", "hafta sonra" (months, weeks after), "siklus" (cycle) and month and week counts; besides the passages above, it names no evaluation time point of preventive treatment that the rule list does not hold (Kutu 8, sections 3.6.3.9 and 6.2.2 and the items of PDF p. 48 are as described in E-041).

Every new quote was checked by script against the page texts, with whitespace normalised. Remark R14-02 concerns the formal model and was verified against the Stage 1 v18 text in the repository and against v13 itself (`history/v13.md`).

#### SL-017
Iteration 15 (fix, 2026-10-21): no web search, no download and no new source. The three remarks of review 15 concern the formulation of required acute-treatment summaries, the window of the adherence shown with a response comparison and the treatment of the overview's treatment effect; they and the identifying-property check of every presence requirement (fixes/fix-iter-15.md) were verified against the Stage 1 v18 text in the repository and against v14 itself (`history/v14.md`). No source quote was added or changed: every quoted fragment of the new text occurs verbatim in Stage 1 v18 (checked by script).

#### SL-018
Iteration 16 (fix, 2026-10-21): no web search, no download and no new source. The one remark of review 16 concerns the treatment to which the acute alternative of the overview's treatment effect is tied; it was verified against the Stage 1 v18 text in the repository (OUT-014, OUT-023, OUT-024, OUT-035) and against v15 itself (`history/v15.md`), with an instance check of the review's two examples (fixes/fix-iter-16.md). No source quote was added or changed.

#### SL-019
Iteration 17 (fix, 2026-10-21): no web search and no new source. The three remarks of review 17 concern the day on which an evaluated period ends relative to its evaluation time point, the formulations that treatment lines and treated-attack lines state, and the declaration form of two given functions; they were verified against the Stage 1 v18 text in the repository (OUT-001, OUT-018, OUT-022, OUT-023, OUT-024, OUT-036) and against v16 itself (`history/v16.md`), with a script check of the date arithmetic (fixes/fix-iter-17.md). To confirm the wording on which the day convention rests, the Stage 1 URLs of [S-015] (NICE CG150 Recommendations page, HTTP 200, "Last updated: 03 June 2025") and [S-005] (ihs-headache.org PDF, HTTP 200) were downloaded with `curl` into a fresh directory under `/tmp`, outside the repository: recommendations 1.3.27 ("3 to 6 months after starting"), 1.3.28 ("after 12 weeks of treatment"), 1.3.29 ("after 2 treatment cycles") and 1.3.48 ("4 to 8 weeks after the start of withdrawal") and the [S-005] sentence "Thus, if a baseline period is 28 days, the final 28 days of the treatment period should be assessed." (found verbatim in the `pdftotext -raw` text) read as Stage 1 quotes them. The new text quotes only fragments of Stage 1 quotes; no source quote was added or changed.

#### SL-020
Iteration 18 (fix, 2026-10-21): no web search and no new source. The one remark of review 18 concerns the stop or pause of a preventive course, which the evaluation time points of a response comparison and the periods of responder labels did not take into account; it was verified against the Stage 1 v18 text in the repository (OUT-018, OUT-020, OUT-021, OUT-022, OUT-024, OUT-039) and against v17 itself (`history/v17.md`), with a script check of the date arithmetic of the 18 rules (fixes/fix-iter-18.md). To confirm the wording on which the fix rests, the following were downloaded with `curl` into a fresh directory under `/tmp`, outside the repository: the Stage 1 URL of [S-015] (NICE CG150 Recommendations page, HTTP 200, "Last updated: 03 June 2025": recommendations 1.3.27, 1.3.28 and 1.3.29 read as Stage 1 quotes them) and the Europe PMC full texts of [S-011] (PMC9188162, HTTP 200: question 3, "after a minimum of 3 consecutive months on treatment", and question 4 on pausing treatment) and [S-013] (PMC7296705, HTTP 200: "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed."). The new text quotes only fragments of Stage 1 quotes and of quotes already given in E-041; no source quote was added or changed.

#### SL-021
Iteration 19 (fix, 2026-10-21): no web search and no new source. The two remarks of re-check 19c concern the stated basis of the lower bound of HALT-30 (E-057 Notes) and the description of the one ICHD-3 passage that uses "simple analgesics" (ISS-02). To verify them, the Stage 1 URL of [S-001] (ICHD-3 PDF, HTTP 200, 211 pages) and the Europe PMC full text of [S-014] (PMC6734476, HTTP 200) were downloaded with `curl` into a fresh directory under `/tmp`, outside the repository, and extracted page by page with `pdftotext` (`-raw` and `-layout`) or with the markup removed. Every new quote was checked by script against these texts, with whitespace and line-end hyphens normalised.
- [S-001]: a page-by-page search of the text layer finds "simple analgesic" only on p. 139, in the second paragraph of the comments on 10.1.1 High-altitude headache; acute mountain sickness is introduced in the sentence after it. The new ISS-02 quotes (p. 139; the 8.2.3.1 and 8.2.3.2 labels of the classification list, p. 12; the comment on 7.3.2, p. 105) were found verbatim.
- [S-014]: subsection "Scoring HALT" gives the unit "whole days per one or 3 months" for the three summed scores of HALT (30 or 90), and the paragraph after Table 18 reads "Grading is not used by HALT-30."

#### SL-022
Iteration 20 (fix, 2026-10-21): no web search and no new source. The one remark of review 20 concerns the Stage 1 statements that ISS-03 lists; it was verified against the Stage 1 v18 text in the repository, whose Statements were searched by script for every mention of migraine (fixes/fix-iter-20.md). To verify the one new quote of ISS-03, the Stage 1 URL of [S-001] (ICHD-3 PDF, HTTP 200, 211 pages) was downloaded with `curl` into a fresh directory under `/tmp`, outside the repository, and p. 190 was extracted with `pdftotext` (`-raw` and `-layout`) and rendered with `pdftoppm` and read. The comments of A1.1 begin "This subclassification of 1.1 Migraine without aura is clearly applicable only to menstruating women as defined above." (checked by script, with the line-end hyphen in "with-out" joined and the "ﬁ" ligature normalised); the A1.1.1 and A1.1.2 windows and note 2 read as quoted in E-060.

#### SL-023
Iteration 21 (fix, 2026-10-21): no web search and no new source. The one remark of re-check 21b concerns the duration of a cluster remission period, which ICHD-3 words differently in its Definitions of terms and in 3.1.1 and 3.1.2 (ISS-12). To verify it, the Stage 1 URL of [S-001] (ICHD-3 PDF, HTTP 200, 211 pages) was downloaded with `curl` into a fresh directory under `/tmp`, outside the repository; pages 41–43 and 208–211 were extracted with `pdftotext` (`-raw` and `-layout`), and pages 42 and 209 were rendered with `pdftoppm` and read. Every new quote of ISS-12 was checked by script against the page texts, with whitespace and line-end hyphens normalised: the 3.1.1 Description ("peri-ods" joined at a line end) and criterion B, the 3.1.2 Description and criterion B and the second sentence of the 3.1 Comments (p. 42), and the last sentence of the definition of "Chronic" in the Definitions of terms (p. 209). The "≥" of 3.1.1 criterion B is a glyph without a text mapping in the text layer and was read on the rendered page; the "<" of 3.1.2 criterion B is mapped. The remission sentence quoted in E-063 (p. 209) reads as quoted.

#### SL-024
Iteration 22 (fix, 2026-10-21): no web search, no download and no new source. The one remark of re-check 22b concerns the predicate `fillsPeriod` (E-006) for 28-day series; it was verified against the Stage 1 v18 text in the repository (OUT-001, OUT-004, OUT-009, OUT-017, OUT-034, OUT-035) and against v21 itself (`history/v21.md`), with a script that evaluates the predicate as written on the review's examples and on random covered periods (fixes/fix-iter-22.md). No source quote was added or changed.

#### SL-025
Iteration 24 (fix, 2026-10-21): no web search, no download and no new source. The two remarks of review 24 concern the identity of a reporting period in the relations among per-period values and the number of definitions that one view states for a measure. They were verified against the Stage 1 v18 text in the repository (OUT-002, OUT-003, OUT-004, OUT-014, OUT-016, OUT-029) and against v23 itself, with scripts that evaluate the predicates as written on the review's two counter-example views, on further instances, and on random views whose values are mutually consistent by construction (fixes/fix-iter-24.md). The only quotes added are Stage 1 quotes of OUT-002, cited in the Evidence of INV-111.

#### SL-026
Iteration 25 (fix, 2026-10-22): no web search, no download and no new source. The one remark of re-check 25b concerns the number of stops or pauses of one treatment course, which INV-001 did not bound, and the end of the course that the predicates read from them. It was verified against the Stage 1 v18 text in the repository (OUT-009, OUT-018, OUT-021, OUT-022, OUT-024) and against v24 itself (`history/v24.md`), with a script that evaluates the predicates as written on the review's example (a course started on 1 January 2026, paused on 10 February and discontinued on 30 March), on a pause followed by a restart, on a dose change dated after a stop, on the earlier watch-point examples and on random contexts (fixes/fix-iter-25.md). The only quotes added are fragments of Stage 1 quotes of OUT-022 and OUT-024 ([S-011], [S-013]), cited in E-008 and INV-001.

#### SL-027
Iteration 26 (fix, 2026-10-22): no web search, no download and no new source. The one remark of review 26 concerns the original pre-treatment baseline of OUT-022 for a preventive treatment resumed after a stop or pause, which INV-070 bounded only by the start of the resumed course. It was verified against the Stage 1 v18 text in the repository (OUT-009, OUT-018, OUT-021, OUT-022, OUT-023, OUT-024, OUT-027, OUT-035, OUT-039 and their evidence) and against v25 itself (`history/v25.md`), with a script that evaluates the predicates as written in v25 and in v26 on the review's example (a course started on 1 January 2026 and paused on 30 June, a new course of the same drug started on 1 September and reduced on 1 October, as of 21 October 2026), on chains of resumed courses, on the earlier watch-point examples and on random contexts (fixes/fix-iter-26.md). The only quotes added are the Stage 1 statement of OUT-022 and fragments of its Stage 1 quotes ([S-011], [S-022]), cited in E-008 and INV-070.

#### SL-028
Iteration 27 (fix, 2026-10-22): no web search, no download and no new source. The one remark of review 27 concerns the original pre-treatment baseline of OUT-022 for a resumed course whose first course has no stated start, where `originalStart` fell back to the start of a restart. It was verified against the Stage 1 v18 text in the repository (OUT-018, OUT-021, OUT-022 and its evidence) and against v26 itself (`history/v26.md`), with a script that evaluates the predicates as written in v26, in v27 and in the review's option (a) on the review's examples (a treatment already being taken, reduced on 15 March 2026 and paused on 30 June, restarted on 1 September and reduced on 1 October; the same with the pause only; a chain of three courses whose first course has no stated start), on the stated-start contrasts and on random contexts with chains of one to four courses (fixes/fix-iter-27.md). No quote was added or changed.

#### SL-029
Iteration 28 (fix, 2026-10-22): no web search, no download and no new source. The two remarks of review 28 concern preventive courses whose start the context does not state: the post-stop monitoring of OUT-022, which INV-103 did not require for such a course and whose on-treatment period INV-070 did not bound, and the pre-treatment baseline of the treatment review view of OUT-021, which INV-068 did not bound. They were verified against the Stage 1 v18 text in the repository (OUT-020, OUT-021, OUT-022, OUT-024, OUT-039 and their evidence) and against v27 itself (`history/v27.md`), with scripts that evaluate the predicates as written in v27 and in v28 on the review's example (a treatment already being taken, reduced on 15 March 2026 and paused on 30 June, restarted on 1 September and reduced on 1 October, as of 21 October 2026), on the same course started on 1 January 2026, on the watch-point examples and on random contexts (fixes/fix-iter-28.md). The only quotes added are fragments of the Stage 1 statements of OUT-021 and OUT-022, cited in INV-068 and INV-103.

#### SL-030
Iteration 29 (fix, 2026-10-22): no web search, no download and no new source. The one remark of review 29 concerns a Notes sentence of INV-067 that described the adherence window of a course whose start the context does not state as referring to days that the context places on the course, a bound that INV-067 does not have. It was verified against the Stage 1 v18 text in the repository (OUT-018, OUT-020, OUT-021, OUT-022, OUT-024, OUT-039 and their evidence) and against v28 itself (`history/v28.md`), with a script that evaluates the predicates as written in v28 on the review's example (a treatment already being taken, reduced on 15 March 2026 and paused on 30 June 2026, as of 21 October 2026, with an adherence window in August 2026), on a course started on 1 January 2026 and stopped on 10 February 2026, and on enumerated admissible contexts, and the same script checks every prose claim that fix 28 added or changed (fixes/fix-iter-29.md). No quote was added or changed.

#### SL-031
Iteration 30 (fix, 2026-10-22): no web search, no download and no new source. The one remark of review 30 concerns the duration of a treatment line (E-055), which INV-079 tied to the start and stop dates only where the line shows them. It was verified against the Stage 1 v18 text in the repository (OUT-024 and its evidence, OUT-034, OUT-039) and against v29 itself (`history/v29.md`), with a script that evaluates the date and duration conjuncts of INV-079 as written in v29 and in v30 on the review's examples (a course started on 1 January 2026 and discontinued on 10 February 2026, and a course started on 1 January 2026 that has not stopped, as of 21 October 2026), on courses without a stated start and on enumerated admissible one-course contexts, and that compares the duration with the course span of INV-109; a second script lists every derived attribute of the model with the attributes it may be shown without (fixes/fix-iter-30.md). The only quote added is a Stage 1 quote of OUT-024 ([S-013]), cited in the Evidence of INV-079.

#### SL-032
Iteration 31 (fix, 2026-10-22): no web search, no download and no new source. The one remark of review 31 concerns four content invariants (INV-050, INV-062, INV-070, INV-092) that also stated, at SHOULD only, what their element is: the start of withdrawal of a follow-up view, the treatment of a responder label's response comparison, the event and the periods of post-stop monitoring, and the period and type scope of the components of a composite index. It was verified against the Stage 1 v18 text in the repository (OUT-017, OUT-018, OUT-020, OUT-022, OUT-037 and their evidence) and against v30 itself (`history/v30.md`), with a script that lists, by level, the invariants that constrain these attributes and evaluates the transcribed predicates of v30 and v31 on the review's four outputs (a preventive treatment started on 1 January 2026 and discontinued on 30 June 2026, a second one started on 1 August 2026, no start of withdrawal, as of 21 October 2026), and with enumerations that compare the views, labels and indices that v30 and v31 admit (fixes/fix-iter-31.md). The only quotes added are fragments of the Stage 1 statements of OUT-017, OUT-018, OUT-020, OUT-022 and OUT-037; INV-112 repeats the Stage 1 quotes of INV-070 ([S-011], [S-022]).

#### SL-033
Iteration 32 (fix, 2026-10-22): no web search, no download and no new source. The three remarks of re-check 32b concern the named responder criteria, whose thresholds no invariant tied to the name under which a label shows a criterion (R32b-01); four facts of the context that an output could state falsely at every level: the treatment of a responder label, the reason for stopping of a treatment that has not stopped, and the instrument of an instrument or screening result shown without its date (R32b-02); and intensity summaries of compared periods that need not share a scale (R32b-03). They were verified against the Stage 1 v18 text in the repository (OUT-010, OUT-018, OUT-020, OUT-021, OUT-024, OUT-026, OUT-027, OUT-033, OUT-035 and their evidence) and against v31 itself (`history/v31.md`), with scripts that evaluate the transcribed predicates of v31 and v32 on the review's examples (a CGRP monoclonal antibody given for episodic migraine whose migraine days fall from 10 to 7; an adult with a preventive treatment started on 1 January 2026 and not stopped, an acute course of sumatriptan and no available instrument or screening result, as of 21 October 2026; a comparison of January and March 2026 with intensity on two scales), on every criterion that can be shown under the six names in enumerated contexts, and on random configurations of compared periods; a further script traces every constant and function of the model to the invariants that use it (fixes/fix-iter-32.md). The only quotes added are fragments of the Stage 1 text of OUT-010 (Evidence basis), OUT-018, OUT-020, OUT-021, OUT-024, OUT-026, OUT-033 and OUT-035.

#### SL-034
Iteration 33 (fix, 2026-10-22): no web search, no download and no new source. The two remarks of review 33 concern intensity and symptom summaries in forms other than the two named ones, which `onSameScale` and `inSameForm` counted as one form (R33-01), and a grade or category shown with a HALT-30 result, which no invariant excluded although the model fixes that HALT-30 has no grading (R33-02). They were verified against the Stage 1 v18 text in the repository (OUT-010, OUT-012, OUT-021, OUT-026, OUT-035 and their evidence) and against v32 itself (`history/v32.md`), with scripts that evaluate the transcribed predicates of v32 and v33 on the review's examples (a comparison of January and March 2026 on a 0–10 numerical scale with a median peak intensity for one month and the share of headache days with severe pain for the other; nausea as a share of headache days and as a count of attacks; a HALT-30 result with total score 12 that shows a HALT-90 category label), on random configurations of compared periods and on enumerated instrument results; a further script traces every constant and function of the model to the invariants, `where` clauses and `when` clauses that use it (fixes/fix-iter-33.md). The only quotes added are fragments of the Stage 1 text of OUT-026.

#### SL-035
Iteration 34 (fix, 2026-10-22): no web search and no new source. The one remark of review 34 concerns the stated location of the two [S-102] quotes in E-057. To verify it, and to check the stated location of every quote that Stage 2 added, the following were downloaded with `curl` into a fresh directory outside the repository, each source in its own folder (all HTTP 200), and extracted page by page with `pdftotext` (`-raw` and `-layout`), or, for the JATS full texts and web pages, into text units with their section or heading paths:
- [S-102]: the Europe PMC full text of PMC4406925 (`fullTextXML`) and PMC's own JATS copy (PubMed Central efetch, `db=pmc&id=4406925`). In both, "Headache impact on functioning" (Sec5, one sentence listing the measures used) and "Migraine-related disability" (Sec6) are sibling sections of Methods, followed by "Lost productive time" (Sec7); both quoted sentences are in Sec6.
- The Stage 1 URLs of [S-001], [S-007], [S-008], [S-010], [S-015] (Recommendations page and Overview page), [S-016], [S-018], [S-028], [S-033], [S-034] and [S-035]; the Europe PMC full texts of [S-011], [S-012], [S-013], [S-014], [S-023], [S-042], [S-101] and [S-104]; and the section 10 URLs of [S-103], [S-105] and [S-106] (chapter 2 and Overview page). The image-only title page of [S-034] was rendered with `pdftoppm` and read.
- ichd-3.org, the web edition of [S-001]: the pages of A1.1 Migraine without aura and A1.1.3 Non-menstrual migraine without aura. The A1.1 page has no text of its own; the comments that begin "This subclassification of 1.1 Migraine without aura" stand on the A1.1.3 page under "Comments:", as they follow the criteria and note of A1.1.3 in the PDF (p. 190).

A script located each quote, split at "[...]", in its source with letters and digits normalised, and reported its PDF page, or its JATS section path and paragraph number, or its heading path and recommendation or paragraph number; item numbers, paragraph and sentence order, and headings were then read on the page (fixes/fix-iter-34.md). Of 142 stated locations of quotes and quoted fragments that Stage 2 added or located in sections 5, 8 and 10 (123 of them not Stage 1 text), three did not match the source's structure and were corrected: the two [S-102] quotes of E-057 and the [S-001] quote of ISS-03. The 39 locations that the model restates for Stage 1 quotes all match.
