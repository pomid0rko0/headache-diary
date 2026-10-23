# Stage 2 — why the first attempt failed, and what a restart must do differently

Date: 2026-10-23. The human stopped the first attempt after iteration 41 and decided to build the formal output model again, from scratch. The model of the first attempt (v00–v40) is wrong in its conception, not only slow to converge. This file says what is wrong with it and how the restart must differ.

## 1. What is wrong with the model itself

### 1.1 Input data entered the model under the name "context"
The human's first constraint was that input data must not appear at any stage. The model broke it from v00 on.

**What `SubjectProfile` held.** Every output was given an `OutputContext`, whose `SubjectProfile` (E-008) held:

- every preventive and acute treatment course of the patient;
- every dated course event of each course: start, dose increase or reduction, target dose reached, treatment cycle end, stop or pause, and (from v28) which course resumes which;
- every acute medication (drug and formulation) the patient has ever used;
- every start of withdrawal of overused medication;
- the dates on which instrument and screening results are available;
- the spans during which the patient menstruates;
- the date of adulthood and of the 12th birthday.

**Why it is input data.** This is the diary's recorded data under another name.

**How outputs were tied to it.** About 45 places in v40 constrain outputs against this profile. Examples:

- INV-123: a fact an output shows must be a fact the context states;
- the general rule R-MCF (section 3.8) on "facts the context does not state";
- `originalStart` and `courseBegunBy`, which work out the start of a treatment from its course events;
- INV-112 and INV-113: a view refers to the patient's own stop event or withdrawal start;
- INV-117: a label concerns one of the patient's own treatments.

Each of these is a rule that the output must agree with the recorded data. That is the excluded derivation rule f(input) → output, written as a constraint.

**Why nobody caught it.** The scope rule's test was that a rule is in scope when all its arguments are output elements. That test was passed by calling the recorded data "context" and its contents "properties of the subject". The author, 49 reviews, 10 oscillation checks and the orchestrator all accepted the label. None of them checked what the context actually contained.

**Consequence.** The longest remark cascades were all about the meaning of this hidden input:

- treatment courses: several stops, restarts, resumptions and unstated starts (iterations 25–28);
- the truth of shown facts against the context (iterations 30–32);
- the general rule for facts the context does not state (iteration 35).

None of this belongs in an output model.

### 1.2 It became a logic of conformance, not a model of data
**What a data model answers.** What does each output contain: which fields, of which type, with which values and units, and how many of each.

**What v40 answers.** Mostly a different question: under which conditions, at which conformance level, must which output exist and be placed where. In v40 that takes:

- 87 invariants (117 before merging);
- conformance levels attached to single conjuncts;
- level-indexed invariants;
- placement markers;
- case tables;
- an enumeration of catalogue rows.

**The result.** A reader cannot see from it what a report contains. It is a formal restatement of Stage 1's requirement text, not a model of the data those requirements describe.

### 1.3 It tried to make every edge of Stage 1's prose formally exact
Where Stage 1 left a case open, the model chose one reading and encoded it in predicates. Reviewers then probed each reading. Examples:

- a treatment whose start is unknown;
- a remission period that has not ended;
- a cycle line that has not ended;
- a percentage change over a period shorter than a month.

Twelve Stage 1 issues (ISS-01–ISS-06, ISS-08–ISS-13) were found this way. None was decided.

## 2. What went wrong in the process

1. **The loop did not fail; the model did.** The same loop, with the same stop rule, converged in Stage 1 (v18, about 13 hours).
   - In Stage 2, the main review was clean seven times (iterations 8, 10, 19, 21, 22, 25 and 32), and each time a re-check found a narrow new case.
   - Those cases came mostly from the conception described in section 1: the hidden model of the patient's records, and conformance attached to single conjuncts. A construction like that has no end of edge cases, so each fresh reviewer found another one. The stop rule only made that visible.
   - An earlier version of this file blamed the stop rule. That was wrong.
2. **Fixes only added.** Each fix added a clause or a special case. The model grew from 268 KB (v00) to 822 KB (v34) before anything was merged.
3. **Each iteration was serial and slow, about one hour.**
   - One reviewer read about 1 MB of text and re-verified about 300 quotes every time.
   - The full run took about 47 hours, 41 iterations and 111 commits.
4. **The orchestrator missed the signals.**
   - It did not question what the "context" contained.
   - It did not flag the growth before the human asked, at iteration 35.
   - It kept running the loop toward the iteration limit instead of proposing a change of approach once the remarks had plateaued.

## 3. What the restart must do

### 3.1 The model contains outputs and nothing else
- **What the model consists of.**
  - Kinds of output (reports, views, summaries, labels, caveats).
  - Their fields, with type, unit, value set and multiplicity.
  - A conformance level for each element or field, taken from Stage 1.
- **Constraints.** Only relations among fields of outputs. Examples:
  - a number of days in a period does not exceed the period's length;
  - compared periods have equal length;
  - a percentage change agrees with the absolute change and the baseline shown with it;
  - an indicator agrees with the per-class values and reference levels shown with it;
  - a category agrees with the score shown with it;
  - a label or caveat is present whenever the element it qualifies is shown.
- **No model of the patient or of the diary's records.** That means:
  - no context entity, subject profile, treatment course or course event;
  - no "facts" that outputs must agree with.
- **Applicability conditions** ("for patients with migraine", "for patients who menstruate", "where results of validated instruments are available") are named conditions attached to an output, worded as Stage 1 words them. They are not defined further.
- **The test for every element and constraint.** Can it be checked by looking at the output alone? If it needs anything outside the output, it is out of the model.

### 3.2 Keep it small and readable
- **A plain notation.** Typed records, enumerations, value sets, multiplicities, and short constraint predicates over fields.
- **One description per output kind** that a clinician or developer can read and that says what the output contains.
- **A size budget**, for example 150 KB or less for the model. Rationale and quotes go in a separate file.
- **Open cases go to an issues list**, not into predicates. Ideally the human decides the Stage 1 issues before the model is written.

### 3.3 The loop
The human's loop stays as it is: review, then up to two re-checks, then a fix, with oscillation checks. What changes is the orchestrator's part:

- **Check the scope first.** In the first review, and in every re-check, include an explicit check that the model contains no model of the patient, the records or the context. Any element that describes the patient's history rather than what an output shows is a scope violation.
- **Verify quotes once.** After that, verify only quotes that were added or changed; the re-checks still verify all of them (as the human decided at iteration 41).
- **Watch the trend and report it.** Track the size and the kind of remark in every iteration. If the size grows steadily, or the same kind of remark keeps coming back, report it to the human with a proposed cause after a few iterations, instead of running on.

### 3.4 What to take from the first attempt
- **The structure: nothing.** Start from Stage 1 (`docs/stage1-output-requirements/OUTPUT_REQUIREMENTS.md` v18), not from v40, and work in a new folder.
- **Rules worth reading:**
  - `PROCESS.md` section 2, the scope rule, to be tightened as in section 3.1 above;
  - `PROCESS.md` section 6a, the generality rules.
- **Evidence, optional, as a lookup only.** Quotes and source values that the first attempt verified many times may be consulted, not copied as structure:
  - `RATIONALE.md` Q entries;
  - section 11 of `OUTPUT_MODEL.md` v40 (ICHD-3 codes and reference levels, instrument value sets and bands, responder criteria, guidance time points).

### 3.5 Stage 1 issues found by the first attempt
These are recorded with evidence in section 8 of `OUTPUT_MODEL.md` v40.

| ID | Issue |
|---|---|
| ISS-01 | The basis of the ICHD-3 8.2.6 indicator is not the total across all classes |
| ISS-02 | "Simple analgesics" is not the ICHD-3 name of the class |
| ISS-03 | Migraine days without the "patients with migraine" condition |
| ISS-04 | The clinician-facing summary includes MAY measures at SHOULD level, and the frequency outputs of OUT-001 |
| ISS-05 | OUT-019 and the single count of the IHS position statement 2025 |
| ISS-06 | "Total score" for instruments that have none |
| ISS-08 | Control levels under "responder or non-responder label" |
| ISS-09 | Which "acute medication outputs" OUT-029 breaks down by headache type |
| ISS-10 | Evaluation time points for preventive treatments outside the populations of the guidance quoted in OUT-018 |
| ISS-11 | The NICE CG150 1.3.48 review window for children under 12 |
| ISS-12 | Cluster remission duration in ICHD-3 |
| ISS-13 | Residual burden next to a percentage change over a period shorter than a month |
