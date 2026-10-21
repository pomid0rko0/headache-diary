# Oscillation check — after iteration 12
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: versions v00 to v12 (history/v00.md to history/v12.md; OUTPUT_MODEL.md is byte-identical to v12); reviews review-iter-01 to review-iter-12 with the re-checks review-iter-08b and review-iter-10b (14 files, 47 remarks: 12, 7, 7, 4, 3, 1, 3, 0 + 2, 1, 0 + 2, 3 and 2); fixes fix-iter-01 to fix-iter-12; the earlier oscillation checks oscillation/check-after-iter-04.md (3 watch points) and oscillation/check-after-iter-08.md (8 watch points).
Date: 2026-10-21

## Method

1. **Git history.**
   - Checks:
     - each snapshot was added in exactly one commit and never changed afterwards: f5eeb50 (v00), 060cdd8 (v01), d2201c8 (v02), d42ada3 (v03), 38b9ab2 (v04), 1b495c9 (v05), 577e35f (v06), 7e168fa (v07), f82f45c (v08), 227a542 (v09), 68b0ad0 (v10), 0ca1cb4 (v11), f8ab130 (v12);
     - the committed snapshot equals the snapshot in the working tree;
     - OUTPUT_MODEL.md at each of these commits is byte-identical to that commit's snapshot;
     - every review, re-check, fix log and earlier check was added in its own commit, in the order of the loop (review 09 in 1249d2a; review 10 in f3c9a9d; re-check 10b in 2771fb3; review 11 in a1a30ca; review 12 in ea9c24b).
   - All checks passed. The working tree was clean before this check, and OUTPUT_MODEL.md equals v12.
2. **Item split (`split.py`, as in the iteration-08 check, extended to 13 versions).** Across v00 to v12 there are 2,412 distinct items:
   - the header, the sections (whole and introduction) and their subsections;
   - every element and element field (heading, Definition, Meaning, Conformance, Realises, Evidence, Notes);
   - every attribute (`E-NNN.Type.attribute`, with its comment lines) and every other declaration of the `omn` blocks (const, fun, pred, axiom, enum, variant, value, element);
   - the 17 `EvaluationRule` constants of E-041 and the 6 `ResponderCriterion` constants of E-045, each split out of its axiom;
   - every invariant and invariant field;
   - every Stage 1 issue and issue field;
   - the 39 traceability rows, each also split into its element, invariant and coverage columns;
   - the source rows, the withdrawn row, the search-log lines and the change-log entries.
3. **State trajectories (`analyse.py`).** Each item was hashed in each version, giving a state string over v00 to v12 (`-` = absent). The script flagged every item whose state returns to its state at a non-adjacent earlier version after a different state in between (A → B → A, including add → remove → add and add → remove).
4. **Rule and criterion components (`rules.py`).** Each component of the 17 rules (`guidance`, `headacheType`, `ages`, `appliesTo`, `excludes`, `anchor`, `timing`, `minOffset`, `maxOffset`) and of the 6 criteria was tracked across versions.
5. **Word-level diff (`show.py`, `show2.py`, `ngram.py`, `docwide.py`).**
   - A word-level diff of every changed item between consecutive versions; every item changed in v09 to v12 that belongs to a watch point or to a remark of iterations 09–12 was read.
   - For every item and every pair of versions vj < vi, 6-word n-grams compared in two directions: n-grams deleted at vj and re-inserted at vi, and n-grams inserted at vj and deleted at vi.
   - The same comparison over sections 1–9 as a whole, to catch text moved between items.
6. **Conformance (`conf.py`, `types.py`).** Tracked across versions:
   - for every attribute, its full declaration: type, level, `when` clause and `derived` mark;
   - for every invariant, its Conformance field and level;
   - for every element Conformance field, the count of each MUST / SHOULD / MAY / SHOULD NOT / MUST NOT keyword, with a flag on any count that drops.
7. **Guarantee counts.** In v08 to v12, the occurrences of the terms that carry earlier fixes were counted: `#L.evaluated = 1` (R01-04), `rc.treatment = L.treatment`, `evaluationResult(L`, `pretreatmentBaseline(L` (R05-02), `otherValueNamed` (R08b-01), `ch.reference.typeScope = allTypes`, `attackScope(`, `scopeFor(` (R09-01), "has a headache type" (R10b-02), "a later time point of its own" and "after its latest date" (R08b-02), `withinWindow`, `fillsPeriod`, `containsPeriodOf`, `dayOneShown`, `ruleRuChildren` and `otherCompletenessExpression`. Every Realises field and every traceability row was also checked for an ID that was removed.
8. **Remark topics (`remarks12.py`).** The multi-line `Item(s)` of all 47 remarks were mapped to E-, INV-, ISS-, S- and OUT- IDs. The script listed the IDs named in remarks of two or more iterations and every remark that cites an earlier remark. Each remark of iterations 09–12 was read, together with the fix of the remark it cites, to see whether it asks to undo an earlier fix.
9. **Scenario checks.**
   - `applic12.py`: E-041 `applicable` under the semantics of every version, with the rule components parsed from each snapshot, on 12 subject scenarios. Seven are the scenarios of the iteration-08 check; five are new age-boundary and no-start scenarios.
   - `inv050.py`: the iteration-08 scenarios of INV-050, extended with the views that INV-049 requires (v05–v10 against v11–v12).
   - `mens12.py`: whether INV-086 requires a menstrual-relation view (and INV-105 an overview cycle line) in v00, v02, v04, v11 and v12, on six menstrual-history scenarios. For v00–v11 the Boolean `menstruates`, whose time frame was unstated, was read both ways: as of the as-of date, and at any time.
10. **Judgement.** Each item changed in two or more versions, at least once in v09–v12, was read against the remark or fixer sweep that drove each change. It was classified as convergent (one direction, earlier guarantees kept) or oscillating (back and forth on the same point).

**Results of the mechanical steps**

- **Step 3.** One item returns to a non-adjacent earlier state.
  - `E-008.attr.SubjectProfile.aged12OrOlder` (`------AAAAAA-`) was added in v06 (R06-01) and removed in v12. It was replaced by the date `aged12From` (Findings, A).
  - 853 items changed at least once, and 313 in two or more versions. 460 items changed in v09–v12: 85 in v09, 112 in v10, 161 in v11 and 264 in v12.
  - Ten items were ever removed:
    - ISS-07 and its fields (v01) and `enum Instrument` (v03), as in the earlier checks;
    - in v12, `menstruates`, `ageGroup`, `AgeGroup` and `aged12OrOlder`, replaced by `menstruationSpans`, `adultFrom` and `aged12From`.

    No removed item was re-added.
  - The change log is append-only (13 entries, none changed after its version). S-101 to S-106 are unchanged apart from the v01 change of S-105, and no source was added after v08. The withdrawn row is unchanged.
  - No Realises field lost an OUT ID, and no traceability row lost an E- or INV- ID, in any version.
- **Step 4.** No rule or criterion component changed after it was set.
  - The 17 rule constants are byte-identical from v07 to v12.
  - `headacheType` and `ages` were set in v06 (or at creation in v07). `excludes` was set in v07. `timing`, offsets, anchors and `appliesTo` are unchanged since each rule was added.
  - The 6 criterion constants and `namedCriteria` are byte-identical from v00 to v12.
- **Step 5, re-insertions within an item.** 7 hits. These are the same 7 hits the iteration-08 check read (E-041 v01→v06 and v07→v08; E-060, INV-087 and INV-104 within v01–v03). None was added in v09–v12.
- **Step 5, insert-then-delete.** 439 hits, 232 of them with the deletion in v09–v12. All were read for the focus items. All are rewordings that keep the earlier content:
  - the v12 time-frame wording ("uses" → "has used up to the as-of date"; "for subjects meeting the condition" → "where the label's treatment meets its condition"; "children" → "a child or adolescent on the first day of …");
  - R10b-02's completion of the v09 `scopeFor` paraphrases;
  - the v12 replacement of the `aged12OrOlder` and `ageGroup` sentences by `aged12From` and `adultFrom` sentences with the same population content.

  No deletion removes a condition, value or guarantee that a fix had inserted.
- **Step 5, document-wide.** 41 n-grams were deleted from sections 1–9 and later re-inserted; 12 of them were re-inserted in v09–v12. They are:
  - `ch.reference.typeScope = allTypes`. Its v00 occurrence is in INV-056. In v01 only the neighbouring conjunct of INV-056 moved; INV-056 kept the all-types tie in every version. v09 re-used the phrase in `reductionMet` and `reductionDecided` (R09-01).
  - Fragments of the Stage 1 OUT-024 and OUT-017 Statements. They were deleted from E-055 (v02) and E-039 (v05), and re-used in the INV-109 and INV-049 Evidence (v11).
  - "the two values it compares (INV-054)." It was deleted from E-040 Conformance by R10b-01 (v10) and re-used in the E-043 Notes (v11). E-043 is the response comparison, for which R10b-01 keeps the MUST.
  - A syntax fragment, `∧ (∀ a ∈ v.content ∩`: INV-087 in v02, INV-011 in v12.

  None restores a deleted statement in its own item.
- **Step 6.** No conformance level returned.
  - No attribute declaration (type, level, `when`, `derived`) returns to an earlier state, and none changed more than once. Since v08, these changed once each:
    - E-040 `absolute` and `relative`: `MUST` → `opt … MUST when ofResponseComparison(self)` (v10, R10b-01);
    - E-008 `withdrawalStart`: `opt Date` → `set Date` (v12);
    - E-008 `ihsQ6ChronicAlternative`: `𝔹` → `set Treatment` (v12).
  - No invariant Conformance field has changed in any version from v00 to v12. The level totals changed only through new invariants: INV-106 (MUST NOT) and INV-107 (SHOULD NOT) in v01, INV-108 (MUST) in v04 and INV-109 (SHOULD) in v11. In v12 they are MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8 and definitional 32.
  - No element Conformance field lost a level keyword in any version.
- **Step 7.** Every guarantee count is equal or higher in each later version, from v08 to v12. For example:
  - `#L.evaluated = 1`: 5, 6, 6, 7, 7;
  - `rc.treatment = L.treatment`: 10, 11, 11, 13, 13;
  - "a later time point of its own": 4 in v08 and in v12;
  - `fillsPeriod`: 15 in v08 and in v12.
- **Step 8.**
  - 52 IDs are named in remarks of two or more iterations (next sections).
  - No remark of iterations 09–12 asks to revert an earlier fix. R09-01, R10b-01, R10b-02, R11-01 and R11-02 each state which earlier fixes they keep.
  - One remark was partly declined, for the first time in the loop: R11-01 (a) and (b), on the ground that the co-presence is already required at MUST. It has not been raised again.
  - No earlier declined remark was raised again.
- **Step 9.** See Findings. In every scenario set, each scenario changes at most once in v09–v12, and only scenario C of E-041 (known since v06, unchanged since) has a value that returns.

## Change history of items changed in two or more versions

Listed: items that changed in two or more versions, at least once in v09–v12. Items whose changes all lie in v00–v08 and that are unchanged since were assessed in the earlier checks (last row). "Fields" names the fields that changed in two or more versions.

| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| **E-041** EvaluationRule.<br>Fields: Definition, Meaning (v01, v06, v07, v08, v12); Notes (v01, v02, v06, v07, v08, v12); `ageCovered` (v06, v07, v12); `inPopulation` (v06, v12).<br>**E-008** SubjectProfile: Definition, Meaning (v06, v07, v12); Notes (v01, v02, v06, v07, v08, v12); Evidence (v06, v12); `aged12OrOlder` (added v06, removed v12); `preventiveFor` comment (v06, v12).<br>**INV-001**: Predicate (v01, v02, v06, v11, v12); Reading (v01, v02, v06, v07, v08, v10, v11, v12); Notes (v02, v06, v07, v11, v12).<br>**INV-055** (Reading, Notes, Evidence), **INV-058**, **INV-059** Readings; **ISS-10** Effect on the model (v06, v07, v12); rows **OUT-018**, **OUT-036** | v01, v02, v06, v07, v08, v10, v11, v12 | **v01–v08:** see check-after-iter-08 (rule list, type listing, population, exclusions, criterion text).<br>**v10:** INV-001 Reading states conditions it had dropped (screening results up to the as-of date; guidance types for preventive treatments only).<br>**v11:** INV-001 bounds `chosenPeriod` by the as-of date; Realises +OUT-034.<br>**v12:**<br>• `ageCovered(c, a, d)` reads the age on a date, and `inPopulation` reads it on the start of the treatment;<br>• `aged12OrOlder`, `ageGroup` and `AgeGroup` are replaced by the dates `aged12From` and `adultFrom`, with `childOn` and `childIn`;<br>• INV-001: `aged12From ≤ adultFrom` replaces `ageGroup = adult ⇒ aged12OrOlder`. New conjuncts: `ihsQ6ChronicAlternative` ⊆ preventive treatments; menstruation spans end by the as-of date; acute courses and acute medications name the same drugs;<br>• Readings, Notes and ISS-10 say "on the start of the treatment". | R01-01, R01-02, R02-01, R06-01, R07-01 to R07-03, R08b-02 (earlier); fix-10 prose sweep (R10b-02 class); R11-03; R12-01 and the fix-12 time-frame sweep | **Convergent** (Findings, A).<br>• No rule component changed after it was set.<br>• `applicable` only gained conjuncts. `ageCovered` keeps its four coverage values, now read on a date.<br>• The INV-001 fallback type (R01-02), `preventiveFor` (R06-01) and the event order (R02-01) are verbatim in v12.<br>• In all 12 scenarios, each rule's applicability changes at most once after v05. |
| **E-045** ResponderCriterion: Meaning (v02, v05, v08, v09, v10, v11, v12); Notes (v01, v06, v08, v09, v10, v11, v12); Definition (v02, v08, v09, v12); `valueAvailable` (v02, v08, v09), `UnderlyingKind` (v08, v09), `AttackReductionComponent` (added v08, changed v09); `conditionHolds` (v12).<br>**E-046** ResponderLabel: Conformance (v01, v02, v05, v08, v09, v11, v12); Definition (v01, v02, v05, v08, v09, v12); `reductionMet`, `reductionDecided` (v01, v05, v09, v12); `attackReductionMet`, `attackReductionDecided` (v08, v09, v12); `scoreDecided` (v05, v08, v09, v12).<br>**INV-062** (Predicate and Reading in every version v08–v12, and in v02 and v05); **INV-063** Reading (v01, v05, v08, v09, v10, v12).<br>**E-012** Meaning (v09, v10), Notes (v09, v10, v12).<br>Row **OUT-020** (v01, v02, v04, v05, v08 to v12) | v01, v02, v04, v05, v06, v08, v09, v10, v11, v12 | **v01–v08:** see check-after-iter-08.<br>**v09:**<br>• reduction components are decided on all-types changes (`ch.reference.typeScope = allTypes`), attack components in `attackScope` (`headacheType`; `scopeFor`, E-012);<br>• INV-062: "∃ sc" becomes `allTypes`, plus the new tag `typeValuesOf` in the scope `scopeFor`.<br>**v10:**<br>• prose only: the `scopeFor` paraphrases gain "where the subject has a headache type";<br>• INV-063 Reading completed;<br>• INV-062 reads the now optional `relative` inside a quantifier.<br>**v11:** INV-062 requires an acute-treatment summary for every acute medication and evaluated period, and the evaluation result of each instrument the criterion rests on.<br>**v12:**<br>• `conditionHolds(c, t, s)` reads the episodic, chronic and IHS Q6 conditions on the label's treatment (`givenFor`; `t ∈ ihsQ6ChronicAlternative`) instead of on the subject;<br>• "uses" → "has used up to the as-of date". | R01-04, R01-05, R01-12, R04-03, R05-02, R08b-01 (earlier); R09-01; R10b-02 and the fix-10 prose sweep; R11-02 and the fix-11 presence sweep; R12-01 and the fix-12 time-frame sweep | **Convergent.**<br>• The six criterion constants are byte-identical from v00 to v12.<br>• Every deciding predicate only gained conjuncts or an argument.<br>• INV-062 only gained conjuncts, or replaced "∃ sc" by stricter scopes.<br>• The R01-04, R05-02 and R08b-01 terms are present in equal or higher counts (Method, step 7).<br>• No list was closed: `UnderlyingKind` gained a tag; `PeriodValueKind` is unchanged since v08.<br>• Intensity and duration thresholds are still `judgement` components (fix-08 decision, same sentence in v08 and v12).<br>(Findings, F) |
| **INV-089** (Predicate, Reading, Evidence, Notes v05, v09); **INV-073** (v09); **E-064** Meaning, Notes (v05, v09); row **OUT-031** (v05, v09, v12) | v05, v09, v12 (row) | **v05:** the cluster attack rate is admitted only in a scope that `concerns` cluster headache, and it agrees with the attack count of its period (R05-03).<br>**v09:** `concerns` → `onlyOfType`, which is strictly stronger (fix-09 sweep). INV-073 likewise.<br>**v12 (row):** the definition labels and completeness for rates. | R05-03; fix-09 sweep; R12-02 | **Convergent.** Each change tightens. INV-091 to INV-093 keep `concerns`, as review 01 judged defensible and fix 09 explained. |
| **E-040** Change: Conformance (v03, v10, v12); Evidence (v03, v10); Notes (v10, v12); `absolute`, `relative` (v10).<br>**INV-054** (Predicate, Reading, Evidence v10; Notes v10, v11); **INV-053** (v10); **INV-060** (v10).<br>**INV-003** (Predicate, Reading v12; Notes v11, v12).<br>**E-043** Conformance (v01, v02, v11), Notes (v01, v02, v06, v07, v08, v11, v12); **E-037** Conformance (v02, v03, v11, v12); **INV-056** Reading (v01, v10, v11), Evidence (v01, v11); **INV-037** Reading (v10, v11).<br>Rows **OUT-001** (v04, v11, v12), **OUT-018**, **OUT-010** (v02, v11) | v01, v02, v03, v04, v10, v11, v12 | **v03:** E-040 Conformance and Evidence: the paediatric equal-length rule (R03-05).<br>**v10:**<br>• INV-054 (MUST) is restricted to the changes of a response comparison;<br>• E-040 `absolute` and `relative` are `MUST when ofResponseComparison(self)`;<br>• INV-053 requires at least one form;<br>• the Notes say a change outside a response comparison needs no values next to it.<br>**v11:** R11-01 (a) and (b) were declined as formal changes. The co-presence of a comparison's values follows from INV-003 with INV-056 or INV-038. It is now stated in the INV-003 Notes, the INV-054 Notes, E-037, E-043, the INV-037 and INV-056 Readings and the rows.<br>**v12:**<br>• INV-003 (MUST): a view that shows a change, residual burden or composite index states the periods (dates and length) of the values it refers to (`referencedValues`);<br>• E-040 Conformance says so;<br>• the E-040 and E-037 paediatric sentences take the period time frame. | R03-05; R10b-01 and the fix-10 level sweep; R11-01; R12-02 and the fix-12 trigger sweep; R12-01 time-frame sweep | **Convergent** (Findings, B).<br>• INV-054 changed once.<br>• The R10b-01 statement ("not constrained by this invariant, because no Stage 1 statement part requires the two values it compares next to it") is verbatim in v12.<br>• v12 adds periods, not values, under OUT-001's MUST, and says "this does not require the two values next to the change".<br>• No predicate of INV-037, INV-038, INV-054 or INV-056 changed in v11. |
| **INV-049** (Predicate v05, v11; Reading v05, v11, v12); **E-039** Conformance (v05, v11, v12), Notes (v05, v06, v12); **INV-050** Reading (v03, v05, v10); row **OUT-017** (v05, v06, v11, v12) | v03, v05, v06, v10, v11, v12 | **v03, v05:** see check-after-iter-08 (INV-050 tie tightened, then qualified).<br>**v10:** INV-050 Reading: "the subject's" start of withdrawal (prose).<br>**v11:** INV-049 also requires, while the as-of date lies within the follow-up year, the view from the start of withdrawal to the as-of date (fix-11 context-range sweep).<br>**v12:** `withdrawalStart` is a set of starts; Readings and Notes say "each start". | fix-03 and fix-05 sweeps (earlier); fix-10 prose sweep; fix-11 context-range sweep (R11-03 class); fix-12 time-frame sweep (R12-01 class) | **Convergent** (Findings, C).<br>• The INV-050 Predicate and E-039 `series` are byte-identical from v05 to v12.<br>• The v11 change concerns which views are required, not the tie between the covered period and the series. |
| **INV-105** (Predicate v02, v05, v12; Reading v02, v04, v05, v12; Notes v02 to v05, v12); **INV-086** (Predicate, Reading, new Notes v12); **E-060** Conformance (v04, v12); **E-067** Notes (v02 to v05, v12); rows **OUT-030** (v01 to v04, v12), **OUT-035** (v02 to v05, v11, v12) | v01–v05, v11, v12 | **v01–v05:** see check-after-iter-04 and -08.<br>**v11 (row OUT-035):** the overview's treatment effect is shown with its values and changes, or with its outcomes and attack lines (R11-01 consequences).<br>**v12:**<br>• the antecedents `c.subject.menstruates` become `menstruatesDuring(c, c.timeRange)` (INV-086) and `menstruatesDuring(ctx, spanOf(v.covers))` (INV-105), over `menstruationSpans`;<br>• E-060 Conformance: the view applies to every time range during which the subject menstruates, and shows labels and completeness (R12-02);<br>• the example in the E-067 and INV-105 Notes changes from "week before" to "month in which" menarche falls. | R01-08, R02-07, R03-02, R03-03, R04-01, R04-04, R05-01 (earlier); R11-01 sweep; fix-12 time-frame sweep; R12-02 | **Convergent** (Findings, D).<br>• E-061, INV-087 and every E-060 attribute are byte-identical from v04 to v12. The lead-in is kept.<br>• The INV-105 cycle-line consequent (the R02-07 overlap) is unchanged since v02.<br>• Only the time frame of the antecedent changed, once. |
| **INV-035** (Reading v10, v11; Predicate v11); **INV-072** (Predicate, Evidence v01, v11; Reading v01, v11, v12; Notes v11, v12); **INV-078** (v11); **INV-109** (new, v11); **INV-083** (v11); **E-051** Conformance (v01, v11, v12), Notes (v05, v11); **E-053**, **E-055** Conformance (v01/v02, v11); **INV-069** Reading (v03, v11); **INV-071** Reading (v11, v12); rows **OUT-021** (v02, v03, v11, v12), **OUT-023** (v01, v09, v11, v12), **OUT-024** (v02, v11), **OUT-039** (v02, v11, v12), **OUT-033** (v08, v11) | v01–v03, v05, v08–v12 | **v11:**<br>• markers in the time-course view (INV-035);<br>• outcome summaries and lines in the summary's view, and every formulation of a summary of all formulations (INV-072);<br>• history groups and lines in the history view (INV-078);<br>• every dose change, and the response summary and adherence with each treatment line (INV-109);<br>• both HADS subscales (INV-083).<br>**v12:** time-frame wording ("has used up to the as-of date"); INV-072 Notes. | R01-07, R02-03, R02-06 (earlier); R11-01 (c), (d) and the fix-11 same-view and presence sweeps; R12-01 | **Convergent.**<br>• Every v11 conjunct is present in v12. The predicates of INV-035, INV-072, INV-078, INV-083 and INV-109 did not change in v12.<br>• INV-078 settles in one direction a point that review 03 left as "not raised" (Findings, E). |
| **E-007** OutputContext (Definition, Meaning v11, v12; `chosenPeriod` new v11); **INV-094** (v11); **E-066** (v11); row **OUT-034** (v01, v02, v03, v11) | v01–v03, v11, v12 | **v11:** `chosenPeriod`, a period chosen by the clinician that need not consist of whole periods; INV-094 requires a clinician-facing summary for it, besides the time-range summary (kept).<br>**v12:** comments state the time frame of `audience`, `weeklyGranularityRelevant` and `previousConsultation`. | R01-09, R02-02 (a), R03-04 (earlier, INV-104 only); R11-03; fix-12 time-frame sweep | **Convergent.** `chosenPeriod` is unchanged since v11. INV-104 is byte-identical from v03 to v12, except a v10 Reading change (prose). |
| **INV-039** (Predicate, Reading, Notes v02, v12); **INV-097** (Predicate, Reading v03, v12; Notes v03, v12); **INV-098**, **INV-096** (Predicate v12; INV-096 Reading v10, v12); **E-030**, **E-048**, **E-049**, **E-058** Conformance (v02/v03 or v08/v10, and v12); row **OUT-036** (v03, v06, v07, v12) | v02, v03, v06, v07, v08, v10, v12 | **v02, v03:** the paediatric equal-length rule, extended to every comparison (R02-02 (b), R03-05).<br>**v10:** E-058 and INV-096 prose completed.<br>**v12:** the age is read on the first day of each period (`childIn`, `childOn`), on the result date (INV-096) or on the start of the covered period (INV-098), instead of on the as-of date. | R02-02 (b), R03-05; fix-02 other change 6; fix-10 prose sweep; fix-12 time-frame sweep | **Convergent.** A subject who is a child on the as-of date was a child on every earlier date. So every v11 requirement holds unchanged in v12, and v12 adds the childhood periods of a subject who is now an adult. The reach widens in the direction of R02-02 (b) and R03-05. |
| **INV-008** (Predicate, Reading, Evidence, new Notes v12); **INV-011** (Reading v08, v12; Predicate, Evidence, new Notes v12); **E-011** (Definition, Meaning, Notes v04, v12); **E-013** Notes (v08, v12); **E-018** Notes (v04, v12); row **OUT-003** (v08, v12); row **OUT-002** (v12) | v04, v08, v12 | **v12:** INV-008 is triggered by `reports(v, lm)`, which covers every form of the four measures. INV-011 adds completeness for referenced values, adherence windows, and views with cycle lines, cluster periods or trigger summaries. | R04-03 (E-011, earlier); fix-08 sweep (E-013); R12-02 and the fix-12 trigger sweep | **Convergent.** Additions only. E-013 `otherCompletenessExpression` (watch point 6) is unchanged since v08. |
| **INV-024**, **INV-023**, **INV-044**, **INV-046** Readings; **E-029** Notes (v01, v10, v12); **E-032** comment of `classUseExcluded`, Notes (v01, v03, v12); row **OUT-016** (v03, v12); row **OUT-014** (v12) | v01, v03, v10, v12 | **v10:** INV-024 and E-029: the conditions of the upper bounds stated (prose).<br>**v12:** `acuteMedications` is every acute medication the subject has used up to the as-of date; the Readings say so. | R01-06, R03-01 (earlier); fix-10 prose sweep; R12-01 | **Convergent.** The INV-024, INV-044 and INV-046 predicates and `classShownUsed` / `classUseExcluded` are unchanged in v12. The R03-01 two-class condition of 8.2.6 is intact. |
| **INV-104** Reading (v01, v02, v03, v10) | v01–v03, v10 | **v10:** the Reading states conditions it had dropped (started treatments, results completed within the covered period, the migraine condition). | R01-09, R02-02 (a), R03-04 (earlier); fix-10 prose sweep | **Convergent.** Predicate unchanged since v03 (watch point 7). |
| Header; introductions of sections 4 (v11, v12), 7, 9, 11 and 12 | every version | Version line, "as of vNN", one search-log paragraph and one change-log entry per version; section 4 item 1 (`chosenPeriod`, time frames). | — | Bookkeeping, not applicable. |
| Items whose changes all lie in v00–v08 and that are unchanged since: the 17 rule and 6 criterion constants; E-041 `excludes`, `timing` and population components; E-060 attributes, E-061, INV-087; INV-050 Predicate and E-039 `series`; INV-100 Predicate; E-013 `expressions`; ISS-04, ISS-06, ISS-08, ISS-09, ISS-11 | within v01–v08 | See check-after-iter-04 and check-after-iter-08. | as there | Convergent (earlier checks). Unchanged in v09–v12. |

## Recurring remark topics

| Topic (IDs) | Remarks | Pattern | Assessment |
|---|---|---|---|
| **Responder labels** (E-045, E-046, INV-062, INV-063, E-012; OUT-020) | R01-04, R01-05, R01-12, R04-03, R05-02, R08b-01, R09-01, R10b-02, R11-02; fix-12 sweep (`conditionHolds`) | Nine remarks in eight iterations, each on a different defect:<br>• the single evaluated period (R01-04);<br>• no continuation decision (R01-05);<br>• the ISS-08 pointer (R01-12);<br>• the IHS 2025 count (R04-03);<br>• the score pair of the label's treatment (R05-02);<br>• the open list of other values (R08b-01);<br>• the type scope of the deciding values (R09-01);<br>• the prose of that scope (R10b-02);<br>• acute effectiveness per drug and per period (R11-02).<br>Each remark states the earlier ties it keeps. The fix-12 sweep moved the criterion conditions from the subject to the treatment; no remark drove that move. | Convergent. The most active topic in iterations 09–12 (watch point 2). |
| **Co-presence in a view** (INV-003, INV-035, INV-054, INV-056, INV-072, INV-078; E-037, E-040, E-043) | review 03 and review 06 ("checked and not raised"), R10b-01, R11-01, R12-02 with the fix-12 trigger sweep | Two directions, on different objects:<br>• **less:** R10b-01 removed the MUST that a change outside a response comparison has its two *values* in its view;<br>• **more:** R11-01 (c), (d) and the fix-11 sweep placed markers, outcome summaries, lines, and history groups and lines in their holder's view; fix 12 placed the *periods* of referenced values, their labels and their completeness in the view of the change.<br>R11-01 (a) and (b) asked for the response-comparison values, a point that reviews 03 and 06 had judged "no gap". Fix 11 declined them with the INV-003 derivation, and review 12 verified it. R11-01 states that it "does not touch the R10b-01 restriction of INV-054", and fix 12 that "R10b-01 is kept". | Convergent, but with the closest approach to a two-way pattern in this period (Findings, B and E; watch point 3). |
| **Conformance level against Stage 1 strength** (INV-054, E-040; earlier R04-02) | R04-02, R10b-01 and the fix-10 level sweep | Each concerns a different item. The fix-10 sweep checked all 108 invariants and 172 attribute declarations and found no other mismatch. | Convergent. No level returned (Method, step 6). |
| **Prose against formal text** (E-041 `excludes`; E-045, INV-063; 23 Readings; INV-037, INV-056) | R08b-02, R10b-02 and the fix-10 prose sweep; R11-01 (a), (b) | Each aligns prose with formal text that stayed unchanged. No formal change was reverted to fit the prose, and no prose fix was later undone (insert-then-delete check). | Convergent. |
| **Presence quantifiers ("each" read as "some")** (INV-062, INV-072, INV-083, INV-109; earlier INV-023, INV-028, INV-068) | R01-06, R02-03 (earlier); R11-02 and the fix-11 presence sweep | Each changes ∃ into ∀ over drugs, periods, formulations, dose changes or subscales. None narrows back. | Convergent. |
| **Context range and time frame** (E-007, E-008, INV-001; INV-049, INV-094; E-041 ages; INV-086, INV-105; `conditionHolds`) | R11-03, R12-01; the fix-11 context-range sweep and the fix-12 time-frame sweep | New topic in iterations 11–12. Each step admits more contexts (a chosen period that is not a run of whole periods; the running follow-up) or makes a time frame explicit: acute medications used up to the as-of date; age on the treatment start or on a period; menstruation spans; every start of withdrawal; IHS Q6 per treatment; episodic or chronic per treatment. No v11 context restriction or reading is reinstated. | Convergent. These are first changes, and some touch watch-point items (Findings, A, C, D, F; watch points 1, 4, 5). |
| **Triggers of cross-cutting requirements** (INV-003, INV-008, INV-011) | R12-02 and the fix-12 trigger sweep | New topic in iteration 12. Each change adds trigger cases. | Convergent. |
| **Evaluation time points** (E-041, INV-001, INV-055, INV-058, INV-059; OUT-018, OUT-036) | R01-01, R01-02, R02-01, R06-01, R07-01, R07-02, R07-03, R08b-02 | No remark since R08b-02. In v12 only the age time frame moved, through the fix-12 sweep (Findings, A). | Convergent (watch point 1). |
| **Menstrual-relation view** (E-060, E-061, INV-086, INV-087, INV-105; OUT-030, OUT-035) | R01-08, R02-07, R03-02, R03-03, R04-01, R04-04; R12-02 (E-060 Conformance text only) | No remark on the view's structure since R04-04. v12 changed the antecedents of INV-086 and INV-105 through the time-frame sweep. | Stable in structure since v04 (Findings, D; watch point 4). |
| **Clinician-facing summary** (E-066, INV-094, INV-104; OUT-034) | R01-09, R02-02 (a), R03-04, R11-03 | R11-03 touched only INV-094, E-066 and the context, not INV-104. | Convergent. INV-104 Predicate is unchanged since v03. |

**Settled points.** Reviews 09 to 12 list these as "not reopened (no new evidence)", and every item behind them is unchanged in v09–v12 (or, where marked, changed only in an unrelated dimension):

- INV-106 at MUST NOT;
- INV-023 at any granularity;
- the "> 3 months" readings of INV-045 and INV-089;
- the E-041 window readings and the `excludes` values;
- `ruleRuChildren` and the rule-list boundary (ISS-10 changed only in its age wording);
- INV-091 to INV-093 with `concerns`;
- labels under a criterion that does not apply (`conditionHolds` now reads the condition on the treatment, but a criterion with no applicable component is treated as before);
- "history of previous bouts" and the OUT-031 end-of-bout Caveat;
- the E-060 lead-in wording;
- the HIT-6 one-month recall and the MIDAS label choice;
- "baseline administration" as any earlier administration;
- INV-060 with INV-061 for compared periods shorter than 28 days (fix 02, item 14);
- a response comparison right after the treatment start;
- the context as subject properties (all new v12 components are still subject properties of E-008);
- INV-050 and E-039 (watch point 4 of iteration 08).

**Remark counts per iteration:** 12, 7, 7, 4, 3, 1, 3, 0 + 2, 1, 0 + 2, 3, 2.

## Findings

None.

No item oscillates, so nothing is frozen, FROZEN_ITEMS.md is not written and OUTPUT_MODEL.md is not changed. The mechanical flag (`aged12OrOlder`) and five other points come closest to a back-and-forth pattern. Each is assessed below.

### A. Age in E-041 applicability: `aged12OrOlder` (added v06, removed v12) and the age on the treatment start

**Trace.**
- v00–v05: E-041 has no population.
- v06 (R06-01): `ages` per rule; `ageCovered` reads `aged12OrOlder` and `ageGroup`, with no stated time frame (in effect, as of the as-of date).
- v07 (R07-01): `childrenAndAdolescentsOnly`.
- v12 (fix-12 time-frame sweep, no remark): `ageCovered(c, a, d)` with the dates `aged12From` and `adultFrom`; `inPopulation` reads it on the start of the treatment; `aged12OrOlder` and `ageGroup` are removed.

**Scenario script** (`applic12.py`; Y = applies, . = does not, - = rule not yet in the model; columns v00 to v12):

| Scenario | Rules whose applicability changed in v09–v12 |
|---|---|
| A–F (the iteration-08 scenarios: adult topiramate; no type listing; cluster headache only, with and without a listing; 10-year-old; onabotulinumtoxinA; erenumab) | none. Scenario C (`.YYYYY.......` for NICE 1.3.27 and AAN 14A) is unchanged since v06. |
| G. Treatment started at 17, adult on the as-of date | AAN 14A, SIGN titrated `YYYYYYYYYYYY.`; Russian 7.1 `-YYYYYYYYYYY.`; Russian children `-------.....Y` |
| H. Started at 11, aged 12 on the as-of date | NICE 1.3.27 `YYYYYYYYYYYY.` |
| I. Started at 12, still a child | none in v09–v12 (NICE 1.3.27 `YYYYYYYYYYYYY`) |
| J. Started at 11, adult on the as-of date | NICE 1.3.27, AAN 14A, SIGN titrated `YYYYYYYYYYYY.`; Russian 7.1 `-YYYYYYYYYYY.`; Russian children `-------.....Y` |
| K. Adult, no start event, target dose reached | AAN 14A, SIGN titrated `YYYYYYYYYYYY.`; IHS Q2 oral `-------YYYYY.` |

**Why it is not an oscillation:**

1. **The item did not return to its v05 state.**
   - The attribute was removed, but its content was kept in dated form. v05 could not separate the 12–17-year-olds from younger children; v12 can.
   - The four `AgeCoverage` values are unchanged, and each maps to a test on a date: `aged12From ≤ d`, `¬ childOn(c, d)`, `childOn(c, d)`.
   - INV-001's "every adult is aged 12 or older" is kept as `aged12From ≤ adultFrom`.
   - `preventiveFor` and the requirement that every preventive treatment is given for some headache type (R06-01) are verbatim in v12.
2. **Every rule changes at most once after v05, in one direction.** A subject's age on the treatment start is at most the age on the as-of date. So:
   - for `adultsOnly` and `aged12AndOver`, the rules applicable in v12 are a subset of those in v11;
   - for `childrenAndAdolescentsOnly`, they are a superset.

   A rule cannot go Y → . → Y or . → Y → . across v06–v12, and the script confirms this for every scenario.
3. **No earlier position is reversed.**
   - No review or fix stated the reference date of the age. R06-01 and fix 06 introduced the population ("the ages it covers"), and R07-01 and R07-02 the rule list and exclusions. None names the as-of date.
   - The v12 move makes the R06-01 guarantee (a rule applies only within its guidance population) exact in time. G and J no longer attribute adult guidance to a treatment started in adolescence.
   - The R07-01 rule list, the R07-02 `excludes` values and the R08b-02 criterion text are unchanged. Scenario E (onabotulinumtoxinA) is identical in v08 and v12.
4. **Scenario K loses no requirement.**
   - INV-055 requires time points only for a treatment with a start (`s ∈ startOf(c, t)`), and INV-056 ties every response comparison to a start.
   - In v12, INV-058 no longer admits a time point for a treatment without a stated start. No required output depended on one.

**Judgement:** convergent. This is the first change of the age dimension since it was introduced, and it was made by a fixer sweep (watch point 1).

### B. What is shown with a change: values (R10b-01) against periods (v12, INV-003)

**Trace.**
- v00–v09: INV-054 (MUST) placed the two values of every change in the change's view.
- v10 (R10b-01): the MUST covers only the changes of a response comparison. E-040: "A change shown outside a response comparison is permitted, in either form or in both."
- v11 (R11-01 (a), declined as already required): the co-presence of a response comparison's values is stated, through INV-003 with INV-056.
- v12 (R12-02 class, trigger sweep): a new INV-003 conjunct (MUST). The view of a change, residual burden or composite index shows a period with the dates of each referenced value's period. INV-008 and INV-011 (SHOULD) add the label and the completeness for these values.

**Why it is not an oscillation:**
1. **Different objects.** R10b-01 concerns the two *values* next to a change. v12 concerns the *periods* those values refer to, which OUT-001 requires at MUST for every summary output ("Every summary output MUST state the reporting period it covers").
   - The v12 E-040 Notes say: "this does not require the two values next to the change".
   - The R10b-01 sentence of the INV-054 Notes is verbatim in v12.
2. **No item returned.** INV-054 changed once (v10). E-040 `absolute` and `relative` changed once (v10). The v12 change is a new conjunct of another invariant.
3. **No remark takes the opposite position.**
   - R11-01 explicitly kept R10b-01, and fix 12 states "R10b-01 is kept".
   - No remark asks to restore the v09 INV-054, or to remove periods from the view of a change.

**Judgement:** convergent. This is the nearest two-way pattern in iterations 09–12, because both directions concern what is shown with a change (watch point 3).

### C. INV-049 / INV-050: the follow-up view of a withdrawal that is still running

The iteration-08 scenarios (`inv050.py`; withdrawal from 1 March 2026, monthly series; "adm" = admitted by INV-050 and E-039; "req" = a view with this covered period is required by INV-049 for some admissible context):

| Scenario | adm v02 / v03 / v05–v12 | req v05–v10 | req v11–v12 |
|---|---|---|---|
| S1. Covers 1 March – 31 August, series = March only (R03-04 kind) | ok / no / no | req | req |
| S2. Covers 1 March – 31 August, all six months | ok / ok / ok | req | req |
| S3. Review day: covers 1 March – 15 April, series = March | ok / no / ok | — | req |
| S3b. Covers 1–31 March | ok / ok / ok | req | req |
| S4. Covers 1–20 March, no series | no / no / ok | — | req |
| S5. Covers 5 March – 15 April | ok / no / no | — | — |

**Why it is not an oscillation:**
1. **The tie that moved twice is unchanged.**
   - The INV-050 Predicate and E-039 `series` are byte-identical from v05 to v12, so every admissibility value is the same as at iteration 08.
   - The v03 guarantees hold: S1 and S5 are still rejected. The v05 qualification holds too: S3 and S4 are admitted.
2. **The v11 change is on another dimension.** It concerns which views must be available, not the shape of an admitted view. It moves S3 and S4 from "admitted" to "required while the as-of date lies in the follow-up year", in the direction of v05.
3. **New evidence.** It rests on evidence that neither earlier sweep considered:
   - the context-range class of R11-03;
   - OUT-017 "from the start of withdrawal onward", read against INV-001's whole-period time ranges. With a mid-month start and calendar months, no view at all was required before v11.
4. **The v12 change** (every start of withdrawal, `set Date`) uses membership, as INV-049 and INV-050 always did. Their predicates did not change.

**Judgement:** convergent. Iteration-08 watch point 4 named re-adding the end tie, or loosening `fillsPeriod` or the start tie, as oscillation. None of these happened.

### D. The menstrual-relation view: from "subject who menstruates" to "menstruates during the period"

`mens12.py` (R = a menstrual-relation view is required for the selected time range; columns v00, v02, v04, v11, v12; the as-of date is 30 June 2026):

| Scenario | v00–v11 read "as of the as-of date" | v00–v11 read "at any time" |
|---|---|---|
| M1. Menarche 10 March 2026; time range January–June 2026 (the R04-01 example) | RRRRR | RRRRR |
| M2. Menarche 10 March 2026; time range January–February 2026 | RRRR. | RRRR. |
| M3. Menstruation ended December 2024; time range January–June 2026 | ..... | RRRR. |
| M4. Menstruation ended December 2024; time range January–June 2024 | ....R | RRRRR |
| M5. No menstruation July 2025 – March 2026; time range October–December 2025 | RRRR. | RRRR. |
| M6. Menstruating throughout | RRRRR | RRRRR |

**Why it is not an oscillation:**
1. **The structure of the view is unchanged.**
   - INV-087, E-061 and every E-060 attribute (including `dayOneShown` and the lead-in) are byte-identical from v04 to v12.
   - The INV-105 consequent (a cycle line that overlaps the covered period, R02-07) is unchanged since v02.
   - The R03-02 targets stay rejected, because INV-087 is unchanged.
2. **One change per scenario, on a new dimension.**
   - Only the antecedents of INV-086 and INV-105 changed, from a Boolean with no time frame to a span overlap.
   - Under either reading of v00–v11, every scenario changes at most once, in v12.
3. **R04-01 is kept.**
   - The R04-01 example (M1) is still required, and still needs the lead-in for 1 January – 9 March.
   - For an overview, R04-01 itself offered the alternative "or condition that requirement on a cycle that can be shown" (review-iter-04.md). Fix 04 chose the lead-in. v12 conditions the requirement only for periods with no menstruation at all (M2, M3, M5), where no cycle can be shown. For periods that straddle menarche, the lead-in remains.
   - So v12 does not switch R04-01's decision; it narrows the antecedent in time.
4. **No remark drove it, and none opposes it.** It came from the fix-12 time-frame sweep. No review has argued for a view of a period with no menstruation.

**Judgement:** convergent. This is the first change to INV-086 since v00 and to INV-105 since v05 (watch point 4).

### E. Settled questions revisited without a model reversal

- **Co-presence of a response comparison's values.**
  - Review 03 (checked, "No gap") and review 06 judged this already required. R11-01 (a) and (b) raised it, fix 11 declined both with the INV-003 derivation, and review 12 verified the derivation.
  - The predicates of INV-037, INV-038, INV-054 and INV-056 did not change; only explanatory text was added (v11).
  - This is a remark-level recurrence, not a back-and-forth of an item.
- **Treatment-history groups and lines.**
  - Review 03 noted, without raising it, that they "may be shown in another view of the same output". The fix-11 sweep placed them in the history view (INV-078, one change). Review 12 accepted this as "superseded in the direction review 03 left open".
  - A later remark that relies on review 03's note to remove the INV-078 co-presence would make INV-078 go A → B → A.

**Judgement:** no oscillation. Both are watch points (watch point 3).

### F. Responder-criterion conditions read on the label's treatment (`conditionHolds`, v12)

**Trace.** From v00 to v11, `conditionHolds(c, s)` read "episodic migraine", "chronic migraine" and the IHS Q6 situation on the subject:
- `hasType(c, c1) ∧ ¬ hasType(c, c1_3)`;
- `hasType(c, c1_3)`;
- `c.subject.ihsQ6ChronicAlternative : 𝔹`.

In v12 (fix-12 time-frame sweep, R12-01 class) it reads them on the label's treatment:
- `givenFor(c, t, c1) ∧ ¬ givenFor(c, t, c1_3)`;
- `givenFor(c, t, c1_3)`;
- `t ∈ ihsQ6ChronicAlternative`.

**Why it is not an oscillation:**
1. **First change.** `conditionHolds` and `SubjectCondition` changed for the first time since v00.
2. **The deciding relations are unchanged.** The six criterion constants, the structure of `reductionMet`, `reductionDecided`, `scoreMet` and `scoreDecided`, and the counts of the R01-04, R05-02, R08b-01 and R09-01 terms are unchanged.
3. **Review 02's settled point is untouched.** A criterion with no applicable component is treated as before; only the time frame of "applicable" changed.
4. **"Subject property" scope point.** The settled point "the context as subject properties, including `ihsQ6ChronicAlternative`" (reviews 05 and 06) concerns scope, not granularity. The component is still a property in E-008.

**Judgement:** convergent. A later move back to the subject-level reading would be A → B → A (watch point 2).

## Things the next checker should watch

1. **E-041 (age on the treatment start; `excludes`; timings).**
   - **History:**
     - the population was added in v06 (R06-01);
     - the age has been read on the treatment start since v12, through a fixer sweep that no remark asked for;
     - the `excludes` values (v07) and the criterion text (v08) are unchanged.
   - **Treat as oscillation**, unless the change rests on evidence that neither R06-01 nor the fix-12 sweep considered:
     - a return to reading the age on the as-of date (`aged12OrOlder`, `ageGroup` or an equivalent);
     - a change of the four `AgeCoverage` values or of any rule's `ages`;
     - any change of `ruleNice1327.excludes`, `ruleTrBox8.excludes` or a rule's `timing` (iteration-08 watch points 1 and 8, still open).
   - **Not oscillation:** aligning the short Readings ("a later time point of its own") with the full criterion, with no value changed.
   - The three dimensions of applicability (fallback type, population, exclusion; iteration-08 watch point 2) and scenario C (`.YYYYY.......`) are unchanged since v07 and v06.
2. **Responder labels (E-045, E-046, INV-062, INV-063, E-012).** They changed in iterations 01, 02, 05, 08, 09, 10, 11 and 12. A remark that does any of the following would reverse an earlier fix:
   - closes `UnderlyingKind` or `PeriodValueKind`, or removes `otherValueNamed` (R08b-01);
   - relaxes `#L.evaluated = 1` (R01-04), the `evaluationResult` / `pretreatmentBaseline` pair or `rc.treatment = L.treatment` (R05-02);
   - decides a reduction component on a value other than all types combined, or an attack component outside `attackScope` (R09-01);
   - drops "where the subject has a headache type" from the `scopeFor` paraphrases (R10b-02);
   - returns the acute-effectiveness requirement to one summary (R11-02);
   - reads the episodic, chronic or IHS Q6 condition on the subject again (v12; Findings, F).

   A remark on whether `givenFor` can separate episodic from chronic migraine for every admissible `preventiveFor` should be met by a fix that keeps the treatment-level reading, or the fix should state the new evidence that justifies leaving it.
3. **Co-presence (INV-003, INV-054, INV-056, INV-078; E-040).** This is the only area in which changes went in both directions, on different objects (Findings, B and E). Each of the following should be checked for reversal:
   - a remark that asks for the two *values* of a change outside a response comparison in its view (reversing R10b-01);
   - a remark that lowers or removes the v12 INV-003 conjunct on the *periods* of referenced values on R10b-01's ground;
   - a remark that raises R11-01 (a) or (b) again without new evidence against the INV-003 derivation (PROCESS section 9);
   - a remark that removes INV-078's placement of history groups and lines on review 03's ground.
4. **Menstrual-relation view and overview (INV-086, INV-087, INV-105, E-060, E-061).**
   - The view's structure and the lead-in are unchanged since v04. The v12 time frame (`menstruatesDuring`) is the first change of the antecedents.
   - **Treat as oscillation,** unless it rests on evidence not considered by R03-02, R04-01 or the fix-12 sweep:
     - restoring a subject-level `menstruates`;
     - requiring the view or a cycle line for a period with no menstruation;
     - removing or restricting the lead-in;
     - relaxing the start of the view (iteration-04 watch point 1, still open).
5. **INV-049 / INV-050 / E-039 (withdrawal follow-up).**
   - INV-050 and E-039 `series` are unchanged since v05. INV-049 gained the running follow-up view in v11, and every start of withdrawal in v12.
   - Iteration-08 watch point 4 stands: re-adding the end tie, or loosening `fillsPeriod` or the start tie, would be oscillation.
   - Dropping the v11 running-follow-up conjunct would reverse the fix-11 sweep.
6. **The v12 time-frame components (E-008).** The v12 sweep replaced:
   - `menstruates` by `menstruationSpans`;
   - `ageGroup` and `aged12OrOlder` by `adultFrom` and `aged12From`;
   - `withdrawalStart : opt Date` by `set Date`;
   - `ihsQ6ChronicAlternative : 𝔹` by `set Treatment`.

   It also fixed the time frames of `acuteMedications` (R12-01) and of `headacheTypes` and `possibleHeadacheTypes` ("has or has had"). Restoring any of the v11 forms would be A → B → A. A scope remark against these properties (review 01 asked future reviewers to watch that the subject properties stay subject properties) would be a new topic, but its fix must not restore a v11 form that a time-frame defect removed.
7. **Change volume.** The number of items changed per version rose (85, 112, 161, 264 in v09–v12), while the remark counts stayed low (1, 2, 3, 2). The growth comes from the fixer sweeps that follow each remark class:
   - prose (v10);
   - co-presence, presence quantifiers and context range (v11);
   - time frames and triggers (v12).

   So far no sweep has undone an earlier sweep. The next checker should run the insert-then-delete comparison on v12 → v13 onward against the v10–v12 sweep additions in particular.

## Conclusion

No item of the model oscillates after twelve iterations, and nothing is frozen.

- **Returns.** One item returns mechanically to an earlier state: `aged12OrOlder`, added in v06 and removed in v12. Its content is kept in dated form (`aged12From`, with the INV-001 link to `adultFrom`), so the item did not return in substance (Findings, A). No other item returns to an earlier state:
  - element, attribute, field, invariant;
  - rule or criterion constant, source, section, value set;
  - conformance level, Realises field or traceability row.
- **Rule and criterion values.** No component of the 17 evaluation rules or the 6 responder criteria changed after it was set. The criteria are byte-identical from v00 to v12, and the rules from v07 to v12.
- **Conformance levels.** No invariant Conformance field has ever changed. No attribute declaration changed more than once, and no element Conformance field lost a level keyword. R10b-01 narrowed the range of INV-054 (v10), but not its level.
- **Remarks.**
  - No remark of iterations 09–12 asks to undo an earlier fix. Each states which earlier ties it keeps.
  - The one partly declined remark, R11-01 (a) and (b), has not been raised again.
  - The guarantee terms of earlier fixes occur in equal or higher numbers in every later version.
- **Watch points of the earlier checks.**
  - Unchanged: the `excludes` values and timings, the rule list and `ruleRuChildren`, INV-050 and E-039 `series`, INV-087, E-061, the lead-in, INV-104, the INV-100 Predicate, `otherCompletenessExpression` and `namedCriteria`.
  - Changed, each for the first time on that dimension, in one direction and keeping every earlier guarantee: the E-041 population (age on the treatment start), the INV-086 and INV-105 antecedents (menstruation during the period), INV-049 (the running follow-up) and the responder labels (type scope, per-drug acute values, conditions on the treatment).
- **Near-patterns.** The closest is in co-presence: R10b-01 removed a value requirement, while v11 and v12 added placement and period requirements on other objects (Findings, B and E). It is listed as a watch point, not frozen, because no item went back and forth and no remark takes the opposite position.
- **Remark counts:** 12, 7, 7, 4, 3, 1, 3, 0 + 2, 1, 0 + 2, 3, 2. The number of changed items per version is rising (watch point 7).

The scripts used are in the session scratchpad (`osc12/`): `split.py`, `analyse.py`, `rules.py`, `conf.py`, `types.py`, `ngram.py`, `docwide.py`, `show.py`, `show2.py`, `remarks12.py`, `applic12.py`, `inv050.py` and `mens12.py`. FROZEN_ITEMS.md was not written, and OUTPUT_MODEL.md and the history snapshots were not changed.
