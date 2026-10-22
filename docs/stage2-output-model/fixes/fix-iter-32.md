# Fix log — iteration 32
Input review: reviews/review-iter-32b.md · Input version: v31 · Output version: v32
Date: 2026-10-22

## What was read and checked

**Read:**
- PROCESS.md, in full (scope exclusions of section 2, notation of section 3, fidelity and evidence of section 4, structure of section 6, identifiers of section 7, frozen items of section 10, practical notes of section 11).
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039). Read closely: OUT-010 (Statement and Evidence basis: "the element "on a stated scale" is supported only indirectly, because a change in intensity between periods [...] can only be read when the scale is known"), OUT-018, OUT-020, OUT-021, OUT-024, OUT-026, OUT-027, OUT-033 and OUT-035.
- v31 (`OUTPUT_MODEL.md`, byte-identical to `history/v31.md`), sections 1–10 and the iteration-31 entries of sections 11 and 12. Read closely: section 3.3 (items 2 and 5), E-023, E-025, E-030, E-045, E-046, E-055, E-057, E-058, E-059 and INV-018, INV-022, INV-026, INV-027, INV-029, INV-032, INV-033, INV-039, INV-062 to INV-064, INV-069, INV-079, INV-082, INV-085, INV-104, INV-105, INV-114.
- Re-check 32b (three remarks) and review 32 (NO_REMARKS, read for context).
- Earlier loop files: fix 31 (format, the identity-tie check and its two noted points); the oscillation checks after iterations 12, 16, 24 and 28 with their watch points (responder labels: iteration-12 watch point 2, iteration-16 watch point 4; the treatment-course cluster: iteration-28 watch points 1–5); reviews 08, 08b and 17 on `namedCriteria`; reviews 01 and 02 and fix 02 on the severe-impairment days of INV-027.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**No download and no web search.** The fix adds no fact, value or source. Every quote added is a fragment of Stage 1 text, checked by script.

**Scripts.** All are in a fresh scratchpad folder, `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix32/`, and were run with `python3 -I`.
- `model32.py`: the library: `omn` blocks by item, the E-008 condition predicates, the six named criteria of E-045 transcribed, the E-046 component predicates and INV-063 for a label with one evaluated period, the criterion-dependent asks of INV-062, and INV-116.
- `verify32.py` (`verify32_v31.out`): reproduces the review's examples under v31; 18 fragments of the transcribed predicates are asserted verbatim in their v31 blocks.
- `sweep32.py` (`sweep32_v31.out`) and `constuse32.py` (`constuse32_v31.out`): the same-defect sweeps (constants and functions with their transitive uses; attributes with the invariants that mention them).
- `check32.py` (`check32.out`): checks (i)–(iii) on v32; 18 fragments of the v32 transcriptions are asserted verbatim, and the v31 blocks used unchanged are asserted byte-identical.
- `apply32.py` builds v32 from `history/v31.md` by 53 exact replacements, each asserted to occur once; `entry32.py` adds the section 11 and 12 entries.
- `blockcheck32.py` (`blockcheck32.out`): line-level diff of every changed `omn` block and counts of the protected tie terms.
- `quotes32b.py`: every quotation added, checked verbatim against Stage 1 v18 (fragments split at "[...]").
- Copies of fix 31's check scripts, read before use: `mech31.py`, `names27.py`, `tokcheck27.py`, `omndiff27.py`, `itemdiff27.py`, `scope27.py`, `quotes32.py` (from `quotes31.py`; label "already in v31"); and the re-check's own `mech.py` (`mech_r32b.py`).

### Verification of the remarks under v31 (`verify32_v31.out`)

**R32b-01 holds.**
- `namedCriteria` and the six `crit…` constants occur only in E-045's own block (`namedCriteria` once, each constant three times). No invariant uses them, directly or through other names (`constuse32_v31.out`).
- The review's label (a CGRP monoclonal antibody given for episodic migraine; migraine days 10 → 7, −30 %; one evaluated period): under `critNice1328` INV-063 admits only "non-responder"; under a criterion with the same name and one 30 % component for any treatment it admits only "responder". Both criteria meet the `where` clause.

**R32b-02 holds.** Context: an adult with migraine; preventive treatment t started on 1 January 2026, not stopped; an acute course u of sumatriptan; no instrument or screening result available; as of 21 October 2026.

| Output | Invariants that could reject it in v31 | Result in v31 |
|---|---|---|
| (a) "Responder" label of u (or of a treatment not in the context), evaluated March 2026, criterion IHS Q6, no comparison | INV-062 fails (SHOULD: no comparison); INV-114 vacuous; INV-063 admits both "responder" and "non-responder" (no reduction component decided without a comparison; Q6 has a judgement component); INV-064 vacuous. `L.treatment` occurs only in E-046, INV-062, INV-064 and INV-114 | MUST-conformant |
| (b) Treatment line of t with `stopReason = {lackOfEfficacy}`, no stop date | INV-079's date and duration conjuncts hold; E-055's `when` clause (`stopped`) is false, so no presence obligation; `stopReason` occurs in no invariant | admitted at every level |
| (c) MIDAS result, total score 14, band III, no completion date | every INV-082 conjunct holds | MUST-conformant |
| (d) HADS result, subscale scores 9 and 11, no date | every INV-085 conjunct holds | MUST-conformant |

**R32b-03 holds.** A comparison of January and March 2026 (31 days each) with a mean peak intensity of 6.0 on a 0–10 numerical scale for January and a distribution of headache days over a four-level verbal scale for March meets the witness of INV-039 and the intensity conjunct of INV-069; INV-032 holds for both summaries. Scale and form differ.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R32b-01 | fixed: the review's option (a), with one refinement | **New:** INV-116.<br>**Changed:** E-045 (Meaning, Conformance, Notes), E-046 (Conformance, Notes), row OUT-020 | **INV-116** "A criterion shown under the name of a named criterion is that criterion" (definitional, E-045, E-046; Realises OUT-020):<br>`∀ L : ResponderLabel; K ∈ L.criterion; n ∈ namedCriteria • K.name = n.name ⇒ K.alsoRestsOn = n.alsoRestsOn ∧ K.components ⊆ n.components ∧ ∀ k ∈ n.components \ K.components • (reduction, attack-reduction or score component whose condition the label's treatment does not meet)`.<br>**Why definitional.** A label shows its criterion by its name, with its thresholds (E-046 `criterion`). E-045 states the named criteria with the thresholds of their sources, and section 1 counts "a named responder criterion with its threshold" among the output data. A criterion shown under such a name with other thresholds misstates the source, and INV-063 then forces the category that the misstated threshold gives. This is the same kind of tie as INV-058 (`tp.rule ∈ evaluationRules`) and INV-082 (bands of `gradeBands`).<br>**Refinement of option (a).** `K = n` would also exclude a truthful label that shows only the threshold that applies to its treatment, for example "NICE CG150 rec. 1.3.28: at least 50 % in episodic migraine" on the label of a treatment given for episodic migraine. Stage 1 asks only that the label "name the criterion applied". A component whose condition the label's treatment does not meet is never met and always decided for that label (`componentMet`, `componentDecided`), and INV-062 asks for no value for it, because its reduction and score conjuncts require `conditionHolds`. So leaving such components out changes neither the categories that INV-063 admits nor the values that INV-062 asks for. The enumeration in `check32.out` confirms this: 0 mismatches.<br>**Kept (watch points).** A criterion under any other name is not constrained (OUT-020 "for example"; R08b-01; reviews 08, 08b and 17). E-045 and E-046 are byte-identical, including the six named criteria's values, `#L.evaluated = 1`, the R05-02 pair, `rc.treatment = L.treatment` and the R09-01 scope ties.<br>**Text.** E-045 Meaning, Conformance and Notes: Relations, and a new paragraph **Named criteria**. E-046 Conformance and Notes, Relations. Row OUT-020: Invariants column and coverage reason. |
| R32b-02 | fixed: the review's four conjuncts | **New:** INV-117.<br>**Changed:**<br>• INV-079, INV-082, INV-085 (Predicate, Reading, Evidence, Notes);<br>• E-046 (Conformance, Notes); E-055 (Notes); E-057 (Notes); E-058, E-059 (Conformance, Notes);<br>• rows OUT-020, OUT-024, OUT-026, OUT-033 | **(a) INV-117** "A responder label concerns one of the subject's preventive treatments" (definitional, E-046; Realises OUT-020): `∀ L : ResponderLabel • L.treatment ∈ ctx.subject.preventiveTreatments`.<br>• It is a new invariant rather than a conjunct of INV-114, so that fix 31's INV-114 stays byte-identical.<br>• Counterparts: INV-036, INV-058, INV-067, INV-079 and INV-112 (definitional), and INV-056 and INV-068 (MUST).<br>**(b) INV-079:** `(l.stopReason ≠ ∅ ⇒ stopped(ctx, l.treatment))`. A reason for stopping states why the course ended (OUT-024 "and the reason for stopping"), and E-055 asks for it at SHOULD exactly where `stopped` holds.<br>**(c) INV-082:** `(∃ a ∈ ctx.subject.instrumentAdministrations • a.instrument = r.instrument)`. The result reports an available result (OUT-026 "Where results of validated instruments are available"), whether or not it shows its date.<br>**(d) INV-085:** `(∃ a ∈ ctx.subject.screeningAdministrations • a.instrument = r.instrument)`, the same for OUT-033.<br>**Unchanged:** no `when` clause, level or date. Each conjunct only narrows what is admitted, and holds for every element that the model asks for (Checks (ii), (iii)).<br>**Text:**<br>• E-046 Conformance and Relations;<br>• E-055 Notes: a stop reason only for a stopped treatment;<br>• E-057 Notes: "INV-082 constrains the results of other instruments only by …" now names the availability of a result of the instrument, so that the paraphrase stays true;<br>• E-058 and E-059 Conformance and Relations;<br>• Readings, Evidence (Stage 1 fragments) and new Notes paragraphs of INV-079, INV-082 and INV-085;<br>• rows OUT-020 (INV-117), OUT-024, OUT-026, OUT-033. |
| R32b-03 | fixed: the review's change, with one form as the review prefers | **Changed:**<br>• E-023 (Definition: new predicate `onSameScale`; Meaning, Conformance, Evidence, Notes);<br>• INV-039 (Predicate, Reading, Evidence, Notes), INV-069 (Predicate, Reading, Notes), INV-105 (Predicate, Reading, Notes);<br>• rows OUT-010, OUT-021, OUT-035 | **`onSameScale(i₁, i₂)`** (E-023): `i₁.scale = i₂.scale` and the same form (both `peakIntensityDistribution`, both `meanPeakIntensity`, or both of another form). It is an equivalence relation.<br>**INV-039** (SHOULD, OUT-010): `∃ i₁ ∈ pc.values ∩ IntensitySummary • ∀ p ∈ ran pc.periods • ∃ m … ∧ m.scale ≠ ∅ ∧ onSameScale(m, i₁)`. The summaries of the compared periods share the scale and form of one summary of the comparison, and so with each other.<br>• This is less strict than the review's all-pairs formula, which would also forbid showing a second form for the same period (for example a mean next to a distribution).<br>**INV-069** (SHOULD, OUT-021): the intensity conjunct is moved out of `∀ p` and anchored in the same way (`∃ i₁ ∈ v.content ∩ IntensitySummary`).<br>**INV-105** (SHOULD, OUT-035): the review's further check. The overview shows the pattern "over time" "so that patients can follow the effect of their treatment", so the intensity summaries of its time course are on one scale and in one form:<br>`∃ i₁ ∈ v.content ∩ IntensitySummary • perPeriod(v, sr, {m : IntensitySummary \| onSameScale(m, i₁)}, allTypes)`.<br>The treatment-effect conjunct and the other conjuncts of INV-105 are verbatim (iteration-16 watch point 1).<br>**Not changed: INV-018 and INV-029.** They state per-period summaries on a stated scale. The comparison between periods that OUT-010 asks for is INV-039, which now holds for any selection of periods (E-023 Notes).<br>**Levels:** SHOULD throughout, the strength of OUT-010, OUT-021 and OUT-035. The scale and the form are not fixed.<br>**Evidence:** the OUT-010 Evidence basis, OUT-021 ("The purpose is that efficacy can be judged across these dimensions") and OUT-035, all Stage 1 text. |

## Same-defect checks

### R32b-01: named constants and value sets used by no invariant (`constuse32_v31.out`, `sweep32_v31.out`)

Every `const` and `fun` of the model was traced, directly or through other declared names (predicates, functions, constants, and the axioms that fix them), to the invariants and attribute declarations that use it.

| Name(s) | Use | Result |
|---|---|---|
| `critNice1328` … `critRu71`, `namedCriteria` | none in v31 | the defect; fixed (INV-116) |
| the 18 `rule…` constants, `allPreventiveTypes` | through `evaluationRules` (INV-055, INV-058, INV-059, E-043) | used |
| `classCode`, `c8_2_1` … `c8_2_8` | through the axioms of `overuseCode` (INV-045) | used |
| `shortestMonthlyDays` | through `fitsMonthlyPeriod` (INV-055) | used |
| `gradeBands`, `scoreRange`, `publishedRecall`, `wholeNumberScores`, `banded` | INV-082 | used |
| `publishedGrading` | E-058 `when` clause | used |
| `instrumentName`, `screeningName`, `label` (E-009) | display functions: the attribute holds the instrument or code, and its shown name is a function of that value. `OtherInstrumentName` and `OtherScreeningName` keep the names of the named instruments for those instruments | not a value set that a shown value can contradict; no change |
| `minutes`, `hours` | library constructors of `Duration` (section 2.8) | not a source value set; no change |
| `c1_2`, `c8_2_7` | named in E-027's Conformance and E-009's Notes (`c8_2_7` only to make explicit that OUT-016 does not refer to it) | no threshold or value set; no change |

No other named constant or value set is unused. In v32, `namedCriteria` and the six constants are used by INV-116 (`constuse32.py` on v32).

### R32b-02: attributes that state a fact the context holds

The class of the remark is an attribute whose value names an entity of the context (a treatment, a course event, an instrument or screening administration, a start of withdrawal, a rule, a scheme window), or whose presence presupposes an event of the context (a stop reason presupposes a stop). Every element attribute was listed with the invariants that mention it (`sweep32_v31.out`) and read against its declaration.

| Element.attribute | Fact of the context | Tie in v31 | Result |
|---|---|---|---|
| E-046 `treatment` | one of the subject's preventive treatments | none (INV-114 only for a shown comparison; INV-064 only for control levels) | fixed: INV-117 |
| E-055 `stopReason` | the treatment has stopped | none | fixed: INV-079 |
| E-058 `instrument` | a result of the instrument is available | only through a shown date (INV-082) | fixed: INV-082 |
| E-059 `instrument` | a screening result of the instrument is available | only through a shown date (INV-085) | fixed: INV-085 |
| E-034 `treatment`, `event`, `date` | a course event of a preventive treatment | INV-036 (definitional) | tied |
| E-039 `withdrawalStart` | a start of withdrawal | INV-113 (definitional) | tied |
| E-042 `rule`, `treatment`, `anchorDate` | a rule of the list, an applicable preventive treatment, its anchor event | INV-058 (definitional) | tied |
| E-043 `treatment`, `treatmentStart` | a preventive treatment and its start | INV-056 (MUST) | tied |
| E-047 `treatment`, `window` start | a preventive treatment; the window begins on or after the course | INV-067 (definitional) | tied |
| E-048 `treatment` | a preventive treatment with a stated start | INV-068 (MUST) | tied |
| E-049 `treatment`, `event`, `eventDate`, periods | the course event and the days of the course | INV-112 (definitional) | tied |
| E-053 `drug`, `formulation` | an acute medication the subject has used | INV-075 (definitional) | tied |
| E-055 `treatment`, `role`, `drug`, `startDate`, `stopDate`, `doseChanges`, `duration`, `formulations`, `preventiveResponse`, `adherence` | the course and its events | INV-079 (definitional) | tied |
| E-056 `scheme`, `windows` | the selected scheme and windows | INV-080 (definitional) | tied |
| E-058 `completionDate`, `baselineResult`; E-059 `date` | available administrations | INV-082, INV-085 (definitional) | tied |
| E-063 `end`, `ongoing` | the as-of date | INV-089 (definitional) | tied |
| E-046 `evaluated` | periods on the label's treatment | none for responder and non-responder labels; INV-064 for control levels | settled by fix 18 (a definitional bound "would exclude an optional label that Stage 1 does not forbid") and noted in fix 31; INV-063 decides no component for such a label. Not reopened |
| E-051 `drug`, `formulations` | none by themselves | — | E-051 Notes: a summary may name a formulation that the subject has never used, with 0 treated attacks, which "states no use of it"; a summary of a drug with 0 treated attacks likewise states none. Not in the class |
| Derived counts: acute-medication days of a drug or class, the treated attacks of a summary, the basis of an overuse indicator, cycle-line menstruation days, values of one type scope | values obtained from diary information | relations to other output elements (INV-005, INV-024, INV-030 to INV-033, INV-045, INV-074, INV-087) | not attributes that name or presuppose a context fact. A count of 0 for a medication, type or treatment that did not occur is a correct value (E-008 Meaning). The model relates no diary-derived value to the context's history beyond these relations, and no remark has asked it to. No change |
| E-054 `drugClass`; E-055 `adverseEffects`, `DoseChangeItem.newDose` | none: the class is the given `drugClassOf`; the context states no adverse effects or doses | INV-078 (SHOULD; set aside by review 31) | not in the class |
| E-046 `residual`, `otherValues` | none: references to output items | INV-062 (SHOULD) | not context facts. A residual burden or a value shown in addition states a true value of its own period (INV-061, INV-003). Outside the class |

Result: the four attributes of the remark were the only ones of the class without a tie.

### R32b-03: comparisons of values that need a common scale, unit or definition

I checked every place where the model asks for values of one dimension for several periods so that they can be compared (Stage 1: "compare", "allow comparison", "for the same pre-treatment baseline and on-treatment periods … so that efficacy can be judged", "over time … so that patients can follow the effect").

| Place | Values | Common scale, unit or definition in v31 | Result |
|---|---|---|---|
| INV-039 (OUT-010) | intensity of the compared periods | none | fixed (the remark) |
| INV-069 (OUT-021) | intensity of the baseline and on-treatment periods | none | fixed (the remark) |
| INV-069 (OUT-021) | presence of each associated symptom | none: days in one period and attacks in another, different units | **fixed**: `inSameForm` (E-025) and the symptom conjunct of INV-069, anchored as for intensity. Review 32b left this to the fixer. Its basis is OUT-021's same-periods presentation "so that efficacy can be judged", not OUT-012 |
| INV-027 (OUT-027 "allow comparison with the baseline period") | days with severe functional impairment | none: `∃ d : ImpactDomain` inside `∀ p` lets one period count paid work and another any activity | **fixed**: `∃ sd : ImpactDomain • ∀ p …` (the domain is chosen once for all the periods). E-030 Conformance, INV-027 Reading and new Notes, row OUT-027. The conjunct, added by fix 02 (R02-04), keeps its level, and no watch point names it |
| INV-105 (OUT-035 "over time") | intensity of the time course | none | fixed (the review's further check) |
| INV-037, INV-056, INV-057, INV-068, INV-070, INV-108 | day and attack counts | one measure; one definition per view (E-011, INV-111); days and attacks are their own units | already tied |
| INV-053, Change across views | the two values of a change | same measure and scope (INV-053, definitional). Where the change's view states a definition, which INV-008 asks at the SHOULD of OUT-002, each value's view that states a definition for the measure states the same one (INV-111) | tied at the level of OUT-002; no change |
| INV-069, INV-071, INV-062 (acute-treatment summaries) | outcomes per medication and period | the outcome measures of one early time point per type scope (INV-072, INV-073); each summary states its formulations (E-051) | Requiring one formulation scope for all the periods would decide part of the OUT-023 reading that E-051 Notes leave open (iteration-16 watch point 3). No change |
| INV-062 (values a criterion rests on, for the baseline and evaluated periods) | for example intensity summaries | none | Not changed. OUT-020 asks the label to "show" the values; it asks for no comparison of them. The criteria on intensity, duration or symptoms are judgement components that the reader applies, and they name no scale or form (E-045 Notes). INV-062 is a watched invariant, and its kinds are open (R08b-01) |
| INV-018, INV-029, INV-022, INV-026, INV-019 | per-period values on a stated scale or form | — | per-period reporting, not a comparison. OUT-010's comparison is INV-039, and OUT-027's is INV-027 |
| INV-097 | lengths of compared periods | equal lengths for children (SHOULD) | already tied |
| INV-082 | an instrument result and its baseline result | same instrument (definitional) | already tied |

## Other changes

**Bookkeeping:**
- header: "Version: v32 · Iteration: 32 · Status: under review";
- section 9: "(as of v32)";
- section 11: the iteration-32 entry (no web search, no download, no new source);
- section 12: the v32 entry (2026-10-22).

**Items changed (diff v31 → v32, `itemdiff27.py`): 30.**
- **2 new invariants:** INV-116 and INV-117.
- **24 content items changed:**
  - 9 elements: E-023, E-025, E-030, E-045, E-046, E-055, E-057, E-058, E-059;
  - 7 invariants: INV-027, INV-039, INV-069, INV-079, INV-082, INV-085, INV-105;
  - 8 rows: OUT-010, OUT-020, OUT-021, OUT-024, OUT-026, OUT-027, OUT-033, OUT-035.
- **4 bookkeeping items:** the header and sections 9, 11 and 12.
- **Not changed:**
  - no element added, withdrawn or renumbered; no invariant withdrawn or renumbered;
  - no Realises field of an existing item; no Elements column of the traceability table;
  - no source, value, axiom, `when` clause, level-annotated attribute declaration or level of an existing invariant.
- `git diff --stat` of OUTPUT_MODEL.md: 110 insertions, 53 deletions.

**Watch points kept** (oscillation checks after iterations 12, 16, 24 and 28):
- **Responder labels.** INV-114 and the `omn` blocks of E-045, E-046, INV-062, INV-063 and INV-064 are byte-identical. The following are verbatim:
  - `#L.evaluated = 1`, the `evaluationResult` / `pretreatmentBaseline` pair, `rc.treatment = L.treatment` (10 occurrences) and `attackScope`;
  - `conditionHolds` (read on the treatment), `UnderlyingKind`, `PeriodValueKind`, `otherValueNamed` and the six criteria's values.

  INV-116 leaves criteria under other names open, and INV-117 only narrows what is admitted.
- **Treatment-course cluster.** Section 2.8, E-008, INV-001, E-049, INV-068, INV-070, INV-103, INV-109, INV-112 and INV-113 are byte-identical. INV-079 gains one conjunct, and its duration conjunct and `∀ s ∈ startOf` are verbatim.
- **INV-105.** The treatment-effect conjunct, `fillsPeriod` and the cycle-line conjunct are verbatim; only the intensity term of the series changed.
- **Direction.** Every admitted set narrows or stays equal. No fix is reversed.

## Checks

| Check | Result |
|---|---|
| (i) The review's examples (`check32.out`) | Under v32 each is rejected:<br>• the 30 % "NICE CG150 rec. 1.3.28" criterion, and a reduction threshold under the name of the IHS 2025 control levels, by INV-116 (definitional);<br>• the label of u, and of a treatment outside the context, by INV-117 (definitional);<br>• the stop reason of the ongoing t by INV-079;<br>• the MIDAS and HADS results by INV-082 and INV-085;<br>• the January–March comparison by INV-039 and by INV-069's intensity conjunct (and INV-105 for a time course with these two months).<br>**Further instances:** nausea as days in January and as attacks in March fails INV-069; severe impairment in paid work in January and for any activity in March fails INV-027. |
| (ii) Outputs fully conformant and truthful under v31 stay fully conformant (`check32.out`) | **INV-116.** 3,560 pairs of a criterion under one of the six names that meets the `where` clause (subsets of components, `alsoRestsOn` with a value added or removed) and an enumerated context (given for migraine, chronic migraine, both, tension-type headache, migraine with aura; IHS Q6 situation or not).<br>• INV-116 admits 113 pairs. Each gives, in 280 value scenarios, the categories of INV-063 and the criterion-dependent asks of INV-062 of the named criterion: 0 mismatches.<br>• 53 of the admitted pairs leave out a component whose condition fails. Option (a) would reject all 53.<br>• The named criteria are admitted in every context, and a criterion under another name (Turkish Box 8) always.<br>**R32b-02.** Random contexts, 0 violations of the new ties:<br>• 23,850 labels with a comparison (INV-062, INV-114, INV-056) meet INV-117;<br>• 50,063 lines with a stop reason exactly where the treatment has stopped meet the new INV-079 conjunct;<br>• 29,232 instrument results and 19,709 screening results that show the date of an available result meet the new INV-082 and INV-085 conjuncts.<br>So the ties hold in every output that meets the SHOULD content v31 already asks for (comparison of a label, stop reason only where stopped, dates of results). Only outputs that state a false fact lose conformance.<br>**R32b-03.** 30,000 random configurations:<br>• the changed SHOULD conjuncts (INV-039, INV-069 intensity and symptoms, INV-027) admit only what v31 admits;<br>• 13,837 configurations are no longer admitted, each without one scale and form, or one domain, for all its periods;<br>• on 30,000 like-for-like configurations the v31 and v32 verdicts are equal.<br>The other invariants are unchanged (177 of 186 v31 blocks are byte-identical in v32, in order). |
| (iii) Nothing becomes unsatisfiable (`check32.out`) | **INV-116.** The six named criteria meet the `where` clause and have pairwise distinct names. INV-063 admits at least one category for every named criterion, context and scenario (16,800 cases). A label can show the named criterion itself, and labels stay optional.<br>**INV-117.** Labels are optional, and every label that meets INV-062 shows a comparison of a preventive treatment (INV-114, INV-056).<br>**INV-079, INV-082, INV-085.** E-055 asks for a stop reason only where `stopped` holds. Every result that INV-062, INV-069, INV-081, INV-083, INV-096 or INV-104 asks for is one of an available administration, and a baseline result is of the same instrument.<br>**INV-039, INV-069, INV-105.** In 30,000 constructions, one summary per period on one scale and in one form met INV-032 (levels on the scale, sum of the days not above the headache days, mean within the scale) and the three new conjuncts together. Symptom summaries in one form meet INV-033 with true counts.<br>**INV-027.** Any domain serves; INV-033 bounds severe-impairment days only by the days affected in the same domain where both are shown. |
| Headings and IDs (`mech31.py`, `mech_r32b.py`) | 67 elements (E-001 to E-067) and 117 invariants (INV-001 to INV-117), none missing, none duplicated.<br>Issues: ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn).<br>References: no dangling E-, INV-, ISS- or source reference; 37 source IDs cited, all within S-001–S-046 or S-101–S-106. Every OUT reference exists in Stage 1. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field. Every invariant has exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full", covering all 39 Stage 1 requirements.<br>The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. INV-116 and INV-117 are in row OUT-020. |
| Types and names (`names27.py`, `tokcheck27.py`) | 752 declared names (two new: `onSameScale`, `inSameForm`), none declared twice.<br>The token report is identical for v31 and v32: 106 flagged tokens, each a declared attribute.<br>Every type used is defined. The new predicates use `is` on the declared tags of `IntensitySummaryValue` and `SymptomPresence`. The anchors `i₁`, `a₁` and `sd` are bound variables; `₁` is a listed subscript digit (section 2.2). No partial term is added. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 40 (38 + 2). Scopes: output 84, repertoire 32, context 1.<br>Every MUST NOT and SHOULD NOT predicate has the form `¬ F`, and no repertoire or context invariant uses a bare `ctx`.<br>172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged, with no typing-rule violation.<br>INV-116 and INV-117 are definitional for E-045/E-046 and E-046 (section 3.3 (5)). The changed SHOULD invariants keep SHOULD: OUT-010, OUT-021 (the SHOULD part), OUT-027 and OUT-035 are SHOULD. |
| Diff of formal blocks (`omndiff27.py`, `blockcheck32.py`) | 186 `omn` blocks in v31, 188 in v32.<br>• Changed: E-023 (`onSameScale` added), E-025 (`inSameForm` added), INV-027, INV-039, INV-069, INV-079, INV-082, INV-085, INV-105.<br>• New: INV-116, INV-117.<br>• The other 177 blocks are byte-identical, in the same order (SHA-256).<br>• Line-level, each changed block differs from v31 only by the lines shown in `blockcheck32.out`.<br>• Protected-term counts, v31 → v32, are unchanged except `conditionHolds(` 9 → 12 (INV-116) and `stopped(` 7 → 8 (INV-079). Unchanged: `notStoppedBefore(` 6, `intervalOnTreatment(` 6, `evaluatedOnTreatment(` 4, `courseBegunBy(` 6, `originalStart(` 4, `courseOverlaps(` 4, `courseNotOutside(` 4, `summarisesMedication(` 11, `sameSpan(` 30, `#L.evaluated = 1` 4, `rc.treatment = L.treatment` 10, `evaluationResult(` 6, `pretreatmentBaseline(` 5, `attackScope(` 4, `otherValueNamed(` 2, `allTypes` 105. |
| Quotes (`quotes32b.py`, `quotes32.py`) | 20 quotations added or reused on changed lines. Each is verbatim in Stage 1 v18 (fragments split at "[...]"), or already in v31. No source quote was changed.<br>`quotes32.py` reports one "NOT FOUND" fragment. It is model text between two quotation marks in the INV-116 Evidence, an artefact of the nested quotes of the OUT-020 example list; that list was checked whole by `quotes32b.py`. |
| Scope sweep (`scope27.py`) | Term counts v31 → v32 are equal except three, each read in context:<br>• "stor" +1: `history/v31.md` in the search-log entry;<br>• "taken" +1: "was not taken as it stands" in the change log;<br>• "states" +8: "the context states", "the name that E-057 states", and similar.<br>No new text describes input, storage or a derivation from input. The new relations take as arguments only output elements and context properties that the model already uses as such (`preventiveTreatments`, course events through `stopped`, `instrumentAdministrations`, `screeningAdministrations`, the treatment conditions of `conditionHolds`). |
| Snapshot and files | `cmp OUTPUT_MODEL.md history/v32.md`: identical. `history/v31.md` and everything under `docs/stage1-output-requirements/` are unchanged (equal to HEAD). Only `OUTPUT_MODEL.md`, `history/v32.md` and this log were written. |
