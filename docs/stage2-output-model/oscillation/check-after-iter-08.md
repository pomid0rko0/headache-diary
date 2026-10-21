# Oscillation check — after iteration 08
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: versions v00 to v08 (history/v00.md to history/v08.md; OUTPUT_MODEL.md is byte-identical to v08); reviews review-iter-01 to review-iter-08 and the re-check review-iter-08b (39 remarks: 12, 7, 7, 4, 3, 1, 3, 0 and 2); fixes fix-iter-01 to fix-iter-08; the earlier oscillation check oscillation/check-after-iter-04.md and its three watch points.
Date: 2026-10-21

## Method

1. **Git history.**
   - Checks:
     - each snapshot was added in exactly one commit and never changed afterwards: f5eeb50 (v00), 060cdd8 (v01), d2201c8 (v02), d42ada3 (v03), 38b9ab2 (v04), 1b495c9 (v05), 577e35f (v06), 7e168fa (v07), f82f45c (v08);
     - the committed snapshot equals the snapshot in the working tree;
     - OUTPUT_MODEL.md at each of these commits is byte-identical to that commit's snapshot;
     - every review, fix log and the earlier check was added in its own commit, in the order of the loop (review 08 in 7472dce, re-check 08b in ce23675, fix 08 in f82f45c).
   - All checks passed. The current OUTPUT_MODEL.md equals v08, and the working tree was clean before this check.
2. **Item split (script `split.py`).** Each snapshot was split into items. Across the nine versions there are 2,357 distinct items:
   - the header, 12 sections (whole and introduction) and 78 subsections;
   - 67 elements and 461 element fields (heading, Definition, Meaning, Conformance, Realises, Evidence, Notes);
   - 202 attributes (`E-NNN.Type.attribute`, each with its comment lines) and 431 other declarations of the `omn` blocks (const, fun, pred, axiom, enum, variant, value, element);
   - 23 rule and criterion constants, each split out of its axiom: the 17 `EvaluationRule` constants of E-041 and the 6 `ResponderCriterion` constants of E-045;
   - 108 invariants and 673 invariant fields;
   - 11 Stage 1 issues and 52 issue fields;
   - 39 traceability rows, each also split into its element, invariant and coverage columns (156 items);
   - the source rows S-101 to S-106, the withdrawn row, 54 search-log lines and 9 change-log entries.
3. **State trajectories (`analyse.py`).** Each item was hashed in each version, giving a state string over v00 to v08 (for example `AABBBCCCD`; `-` = absent). The script flagged every item whose state returns to its state at a non-adjacent earlier version after a different state in between (A → B → A, including add → remove → add and remove → re-add).
4. **Rule and criterion components (`rules.py`).** Each `EvaluationRule` and `ResponderCriterion` constant was parsed into its components (`guidance`, `headacheType`, `ages`, `appliesTo`, `excludes`, `anchor`, `timing`, `minOffset`, `maxOffset`; criterion components and `alsoRestsOn`), and each component was tracked across versions.
5. **Word-level diff (`show.py`, `ngram.py`, `docwide.py`).**
   - A word-level diff of every changed item between consecutive versions.
   - For every item and every pair of versions vj < vi, 6-word n-grams compared in two directions: n-grams deleted at vj and re-inserted at vi, and n-grams inserted at vj and deleted at vi.
   - The same comparison over sections 1–9 as a whole, to catch text moved between items.
   - Every hit in a formal item, and every hit in E-041, E-008, E-045, E-046, INV-001, INV-050, INV-055, INV-058, INV-059, INV-062, INV-063, INV-104, INV-105 and rows OUT-017, OUT-018, OUT-020 and OUT-036, was read in context.
6. **Conformance keywords (`conf.py`).** Tracked across versions:
   - for every attribute, its level, `when` clause and `derived` mark;
   - for every invariant, the level in its Conformance field;
   - for every element Conformance field, the count of each MUST / SHOULD / MAY / SHOULD NOT / MUST NOT keyword.
7. **Remark topics (`remarks.py`).** The `Item(s)` of all 39 remarks were mapped to E-, INV-, ISS-, S- and OUT- IDs. The script listed the IDs named in remarks of two or more iterations, and every remark that cites an earlier remark. Each such remark was read, to see whether it asks to undo an earlier fix.
8. **Scenario checks.**
   - `applic.py`: the `applicable` predicate of E-041, as it stood in v00, v01, v05, v06, v07 and v08, evaluated for every rule on seven subject scenarios.
   - `excl.py`: the stated membership criterion of `EvaluationRule.excludes` (v07 wording and v08 wording) applied mechanically to the 17 rules, for every treatment start date from 1 January 2024 to 29 December 2028, and compared with the 17 `excludes` values.
   - `inv050.py`: the conjuncts of INV-050 on the tie between the covered period and the series, as they stood in v02, v03 and v05 (unchanged in v08), evaluated on six withdrawal follow-up views.
9. **Judgement.** Each item changed in two or more versions was read against the remark or fixer sweep that drove each change, and classified as convergent (one direction, earlier guarantees kept) or oscillating (back and forth on the same point).

**Results of the mechanical steps**

- **Step 3.** No item returns to a non-adjacent earlier state: 0 flags.
  - 615 items changed at least once; 167 changed in two or more versions (118 without the aggregate items: whole sections, whole elements and invariants, header).
  - Only 6 items were ever removed, all in v01 (ISS-07 and its fields, withdrawn by R01-12) or v03 (`enum Instrument`, replaced by an open variant by R03-06). None was re-added.
  - Every change-log entry is unchanged after its version, so section 12 is append-only. S-101 to S-104 never changed; S-105 changed once (R01-11); S-106 is new in v08.
- **Step 4.** No component of any rule or criterion changed value after it was set.
  - For all 17 rules, `guidance`, `appliesTo`, `anchor`, `timing`, `minOffset` and `maxOffset` are unchanged since the rule was added.
  - `headacheType` and `ages` were set once: in v06 for the 11 rules then present, and at creation for the 6 rules added in v07.
  - `excludes` was set once, in v07: `{onabotulinumtoxinA}` for `ruleAan14A`, `ruleRu71` and `ruleTrBox8`, and ∅ for the 14 other rules.
  - The 6 criterion constants of E-045 are byte-identical from v00 to v08.
  - The one textual change in a v00 rule constant (`ruleIhsQ2Quarterly`, v01) is a trailing `∧` added when rules were appended.
- **Step 5, re-insertions within an item.** 7 hits.
  - Four are in INV-087, E-060 and INV-104 between v01 and v03. They were already read by the iteration-04 check, which found them to be fragments around restructured, unchanged terms.
  - Three are in E-041:
    - "and the end of the second" in the Meaning (deleted in v01 when the list of time points was extended, re-inserted in v06 when the list was regrouped by guidance);
    - "the end of the second treatment cycle" (Notes) and "the migraine section of NICE CG150" (Evidence), from v07 to v08. These are phrases re-used in the rewritten exclusion argument and Evidence introduction.

    None of the three restores a deleted condition, value or statement.
- **Step 5, insert-then-delete.** 205 hits. Every hit in the focus items was read.
  - All but one are rewordings that keep the earlier content: for example, the E-041 Meaning list of time points rewritten in v06 and v07, and the v07 Readings "names another time point" replaced in v08.
  - The exception is INV-050. The conjunct `v.covers.end = last(v.series.periods).end` was inserted in v03 and deleted in v05 (Findings, B).
- **Step 5, document-wide.** 29 n-grams were deleted from sections 1–9 and later re-inserted.
  - The largest group (14) is the `(∃ g : Granularity • containsPeriodOf(spanOf(v.covers), g)) ⇒` condition and its prose. It was deleted from INV-104 in v03, when INV-104 was tightened to monthly series, and re-used in INV-105 in v05 by the R05-01 fix ("the INV-104 pattern").
    - This is text re-used in a different item, not a return within one item.
    - INV-105 v05 also carries the v03 tie (`fillsPeriod`), so it does not reproduce the INV-104 v02 defect that R03-04 removed.
  - The other hits are common phrases or the hits listed above.
- **Step 6.** No conformance level changed twice, and none returned.
  - No attribute changed its level, `when` clause or `derived` mark more than once. The 12 attributes that changed did so once each: 11 in v01–v04 and E-039 `series` (`core` → `SHOULD when wholePeriodFrom(…)`, v05).
  - No invariant changed level. MUST runs 18 (v00–v03) and 19 (v04–v08); MUST NOT 1 → 2 and SHOULD NOT 7 → 8 (v01, new INV-106 and INV-107); SHOULD 47 and definitional 32 throughout.
  - No element Conformance field lost a level keyword in any version.
- **Step 7.**
  - 34 IDs are named in remarks of two or more iterations (next sections).
  - No remark asks to revert an earlier fix, and no declined remark was raised again: all 39 remarks were fixed, and none was declined.
  - Two remarks reject the premise of an earlier remark or review note, each with new evidence, while keeping the earlier fix (Recurring remark topics; Findings, A).
- **Step 8.** See Findings: in each scenario set, at most one point moved twice, and only through two changes on different dimensions or through a tightening that a later fix qualified.

## Change history of items changed in two or more versions

Items that changed in only one version are not listed. Items whose changes all lie in v00–v04, and are unchanged since, were assessed in check-after-iter-04 and are summarised in the last rows. "Fields" names the fields that changed in two or more versions.

| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| **E-041** EvaluationRule.<br>Fields: Definition, Meaning, Evidence (v01, v06, v07, v08); Notes (v01, v02, v06, v07, v08).<br>`applicable` (v06, v07); 9 rule constants (v06, v07); `evaluationRules` (v01, v07); `excludes` (added v07, comment v08).<br>Changed once: `appliesTo` comment and `allPreventiveTypes` (+`oralPreventive`, v07); Realises (+OUT-036, v07). | v01, v02, v06, v07, v08 | **v01:** rules `ruleNvnTitrated` and `ruleRu71` added; Notes: the rule list is the Stage 1 evidence of OUT-018; the rules for all preventive types apply to every preventive treatment (fallback type, INV-001).<br>**v02:** Notes: no course event precedes the start; `fitsMonthlyPeriod` (E-042).<br>**v06:** components `headacheType` and `ages`, `AgeCoverage`, `ageCovered` and `inPopulation`; `applicable` gains `inPopulation`; all rules are `c1`, with ages per guidance.<br>**v07:**<br>• six rules added (`ruleIhsQ2Oral`, `ruleAan14B`, `ruleRu33Bta`, `ruleRuChildren`, `ruleTrBox8`, `ruleTr3639`);<br>• component `excludes`, and `applicable` gains `¬ ∃ ty ∈ r.excludes …`;<br>• the rule list becomes the time points of the guidance cited for OUT-018, read in full, plus [S-034];<br>• R07-03 location.<br>**v08:** the stated criterion of `excludes` is corrected to match the unchanged values (comment, Meaning, Notes: "a time point after this rule's time point or, for a window, after its latest date"); NICE rationale "names no exception" replaced by the timing argument with [S-106]; Meaning glosses of `atLeastOffset` and `withinWindow` aligned with the settled window readings. | R01-01, R01-02; R02-01; R06-01; R07-01, R07-02, R07-03 and the fix-07 completeness sweep; R08b-02 and the fix-08 sweep (Other changes 2) | Convergent (Findings, A and C).<br>• No rule component changed after it was set (Method, step 4).<br>• `applicable` only gained conjuncts.<br>• The rule list only grew: 9 → 11 → 17 rules.<br>• Each step works on a different dimension: list completeness, type listing, population, type exclusion, then criterion text. |
| **E-008** SubjectProfile.<br>Fields: Definition, Meaning (v06, v07); Notes (v01, v02, v06, v07, v08). | v01, v02, v06, v07, v08 | **v01:** Notes: `otherPreventive` is the fallback type.<br>**v02:** Notes: course events and the start.<br>**v06:** `preventiveFor` and `aged12OrOlder` added.<br>**v07:** `oralPreventive` added; Notes on several types per treatment and on exclusion.<br>**v08:** Notes: the exclusion criterion restated. | R01-02; R02-01; R06-01; R07-01, R07-02; R08b-02 | Convergent. Every change adds a value, a property or a sentence. No value set lost a member. |
| **INV-001**.<br>Fields: Predicate, Evidence (v01, v02, v06); Reading (v01, v02, v06, v07, v08); Realises (v01, v02); Notes (v02, v06, v07). | v01, v02, v06, v07, v08 | **v01:** new conjunct: every preventive treatment has a guidance type (R01-02).<br>**v02:** new conjunct: no course event precedes the treatment start (R02-01).<br>**v06:** new conjuncts: `preventiveFor` names preventive treatments and possible headache types; every preventive treatment is given for some headache type; an adult is aged 12 or older.<br>**v07, v08:** Reading and Notes on exclusions: "names another time point" (v07), then "a later time point of its own" (v08). | R01-02; R02-01; R06-01; R07-02; R08b-02 | Convergent. The predicate only gained conjuncts. The R01-02 conjunct is present verbatim in v08. |
| **INV-055** (Predicate v02; Reading v02, v06, v07, v08; Evidence v06, v07; Notes v02, v06, v07, v08).<br>**INV-058** Reading (v06, v07); **INV-059** Reading (v06, v07, v08).<br>**E-042** Notes (v02, v06, v07); **E-043** Conformance (v01, v02) and Notes (v01, v02, v06, v07, v08).<br>Rows **OUT-018** (v01, v02, v06, v07, v08) and **OUT-036** (v03, v06, v07). | v01, v02, v03, v06, v07, v08 | **v01–v02:** E-043 monthly periods (R01-03); INV-055 guarded by `fitsMonthlyPeriod` (R02-01).<br>**v06:** Readings and Notes describe the population.<br>**v07:** they describe the six new rules and the exclusions.<br>**v08:** they describe the corrected exclusion criterion.<br>The OUT-036 row follows E-041's new Realises (v07). | R01-03, R02-01; R03-05 (row OUT-036); R06-01; R07-01, R07-02; R08b-02 | Convergent. The INV-058 and INV-059 predicates are unchanged from v00 to v08. INV-055 changed once (v02). Every later change is text that follows `applicable`. |
| **E-045** ResponderCriterion (Definition v02, v08; Meaning v02, v05, v08; Notes v01, v06, v08).<br>**E-046** ResponderLabel (Definition, Conformance v01, v02, v05, v08; Notes v01, v05, v08).<br>**INV-062** (Predicate, Reading v02, v05, v08; Evidence v02, v08; Notes v05, v08); **INV-063** Reading (v01, v05, v08); **INV-064** (v05).<br>Row **OUT-020** (v01, v02, v04, v05, v08). | v01, v02, v04 (row), v05, v06 (Notes), v08 | **v01:** `#L.evaluated = 1` in `reductionMet` and `reductionDecided` (R01-04); MUST NOT continuation decision (R01-05).<br>**v02:** `valueAvailable`; `otherValues` and INV-062 apply where values are available.<br>**v04 (row only):** the IHS 2025 count (R04-03).<br>**v05:** `rc.treatment = L.treatment` in the reduction relations; `evaluationResult` and `pretreatmentBaseline` in `scoreMet` and `scoreDecided`; new INV-062 conjunct for the score pair; INV-064 tie to the treatment start (R05-02 and its sweep).<br>**v06 (Notes):** each criterion is a criterion of its guidance's population.<br>**v08:** `UnderlyingKind` gains `periodValuesOf` and `otherValueNamed`; `PeriodValueKind`, `valueOfKind`, `showsValueNamed`; component `attackReduction` with `attackReductionMet` and `attackReductionDecided`; INV-062 conjuncts (a)–(c); the `alsoRestsOn` comment and the `namedCriteria` gloss aligned with the values (R08b-01 and the fix-08 sweep). | R01-04, R01-05, R01-12; fix-02 other change 7; R04-03; R05-02; fix-06 sweep; R08b-01 | Convergent.<br>• The INV-063 predicate and the six criterion constants are unchanged from v00 to v08.<br>• Every change to `reductionMet`, `reductionDecided`, `scoreMet`, `scoreDecided`, `componentMet` and `componentDecided` adds a conjunct or a disjunct for a new component.<br>• The new attack component keeps the R01-04 rule (one evaluated period) and the R05-02 tie (the label's own comparison).<br>• No conjunct was removed. |
| **INV-050** (Predicate, Reading v03, v05).<br>**E-039** WithdrawalFollowUpView (`series` v05; Notes v05, v06).<br>**INV-049** (v05).<br>Row **OUT-017** (v05, v06). | v03, v05, v06 (Notes, row) | **v03:** the covered period equals the span of the series (`v.covers.start = first(…).start ∧ v.covers.end = last(…).end`).<br>**v05:**<br>• the end tie is removed;<br>• `v.covers.start = v.withdrawalStart`;<br>• headache days and acute-medication days for the covered period itself;<br>• where present, the series begins on the start of withdrawal and fills the covered period (`fillsPeriod`);<br>• the review window is triggered by `v.covers.end`;<br>• E-039 `series` becomes `SHOULD when wholePeriodFrom(…)`;<br>• INV-049 keeps the exact span for the time ranges of INV-001.<br>**v06:** E-039 Notes and the OUT-017 row point to ISS-11. | fix-03 sweep (R03-04 kind); fix-05 sweep (R05-01 kind); R06-01 sweep | Convergent, with one point that moved in both directions (Findings, B). |
| **INV-105** (Predicate v02, v05; Reading v02, v04, v05; Notes v02–v05).<br>**E-067** Notes (v02–v05); **E-006** Notes (v02, v03, v05).<br>Row **OUT-035** (v02–v05). | v02, v03, v04, v05 | **v02:** the cycle line overlaps the covered period; the treatment-effect antecedent applies only to started treatments.<br>**v03, v04:** Notes and Reading on attached marks and the lead-in.<br>**v05:** the series conjunct `tiles(…)`, unchanged from v00 to v04, becomes the four measures for the covered period, plus a `fillsPeriod` series where the covered period contains a whole period. | R02-07; R03-03; R04-01; R05-01 | Convergent. The v05 change concerns a conjunct no earlier remark had touched. The cycle-line conjunct is unchanged since v02, and the R03-04 guarantee (no one-period series of a longer covered period) holds. Unchanged in v06–v08. |
| **E-058** Conformance (v02, v08).<br>Row **OUT-026** (v01, v03, v08). | v01, v02, v03, v08 | **v02:** the baseline result and the change SHOULD be shown.<br>**v08:** a result with a grade or category SHOULD carry the clinical-interpretation caveat (INV-100); the row adds INV-100. | fix-02 other change 6; R01-10, R03-06; fix-08 sweep (OUT-038) | Convergent (additions on different points). |
| **ISS-10** (fields v06, v07) | v06, v07 | **v06:** new issue; the [S-034] paediatric time point is put to the human in ISS-10 and not modelled.<br>**v07:** the time point is modelled as `ruleRuChildren`, and the issue asks the human to confirm it. | R06-01; R07-01 and the fix-07 sweep | Convergent (a single move from "not modelled" to "modelled, human asked"). Watch point 3. |
| **E-060, E-061, INV-087**; rows OUT-030 (menstrual-relation view) | v01–v04 | See check-after-iter-04. | R01-08, R02-07, R03-02, R03-03, R04-01, R04-04 | Convergent (earlier check). **Unchanged in v05–v08**, and not touched by any remark since iteration 04 (iteration-04 watch points 1 and 2). |
| **INV-104, E-066**; row OUT-034 | v01–v03 | See check-after-iter-04. | R01-09, R02-02 (a), R03-04 | Convergent (earlier check). **Unchanged in v04–v08** (iteration-04 watch point 3). |
| E-032, E-037, E-048, E-049, E-053, E-057; ISS-04, ISS-06, ISS-09; rows OUT-012 and OUT-021 | within v01–v04, plus ISS-09 "For the human" in v06 | See check-after-iter-04. ISS-09 (v06): a sentence on the population. | as in check-after-iter-04; R06-01 sweep | Convergent. Unchanged since, apart from the ISS-09 addition. |
| Header; section 9 introduction; sections 11 and 12; section 10 introduction (v01, v08) | every version | Version line, "as of vNN", one entry or paragraph appended per version, and the S-106 row. | — | Bookkeeping, not applicable. |

## Recurring remark topics

| Topic (IDs) | Remarks | Pattern | Assessment |
|---|---|---|---|
| **Evaluation time points** (E-041, E-008, E-042, E-043, INV-001, INV-055, INV-058, INV-059; OUT-018, OUT-036) | R01-01, R01-02, R02-01, R06-01, R07-01, R07-02, R07-03, R08b-02 | Eight remarks in five iterations, each on a different dimension:<br>• **List completeness:** R01-01 (time points in the Stage 1 quotes), then R07-01 (the cited guidance read in full). Same direction.<br>• **Applicability:** R01-02 (missing type listing), R06-01 (population; new evidence), R07-02 (type exclusion; new evidence), R08b-02 (the stated criterion of the R07-02 mechanism; values kept).<br>• **Other:** R02-01, a satisfiability side effect of R01-03; R07-03, a citation location.<br>Two remarks reject an earlier premise with new evidence:<br>• R06-01 rejects R01-02's premise ("NICE 1.3.27 applies to any prophylactic treatment") with the CG150 headings, 1.3.9 and 1.3.39, and the AAN and Russian population statements. It explicitly keeps the R01-02 fix: "Keep the R01-02 guarantee."<br>• R07-02 revisits review 01's not-raised note that 14A applied to all types is "a defensible reading", with 14B, 14H and the Russian section 3.3 comment, which no earlier file cited. It leaves the settled 14A window reading untouched.<br>R08b-02 is a side effect of the R07-02 fix (its gloss). Review 08 judged the same gloss not a remark; re-check 08b raised it with the Turkish case as new evidence. The fix kept all 17 values. | Convergent, but the most active topic since iteration 05 (watch points 1–3). |
| **Responder labels** (E-045, E-046, INV-062, INV-063, INV-064; OUT-020) | R01-04, R01-05, R01-12, R04-03, R05-02, R08b-01 | Six different defects:<br>• the single evaluated period (R01-04);<br>• no continuation decision (R01-05);<br>• the ISS-08 pointer (R01-12);<br>• the IHS 2025 count (R04-03);<br>• the score pair tied to the treatment (R05-02);<br>• the open list of other values (R08b-01).<br>R08b-01 carries the R03-06 pattern (a closed list opened) over to `UnderlyingKind`. None asks to undo an earlier fix. | Convergent (watch point 5). |
| **Covered period and its series** (INV-104, INV-105, INV-050, INV-087 start) | R02-02 (a), R03-04, R04-01, R05-01; fixer sweeps fix-03 (INV-050) and fix-05 (INV-050, INV-049, E-039) | An exact-span requirement is replaced, item by item, by a condition plus `fillsPeriod` (or the lead-in), keeping the R03-04 guarantee:<br>• INV-104 in v02–v03;<br>• INV-087 in v03–v04;<br>• INV-105 in v05;<br>• INV-050 in v03–v05.<br>INV-050 is the one item where a sweep tightened (v03) and a later sweep qualified (v05). | Propagation, convergent (watch point 4). |
| **Closed lists vs Stage 1 "for example"** (E-057, E-045, E-013, INV-100) | R03-06, R08b-01, and the fix-08 sweep (OUT-003, OUT-038) | Every step opens a list. None closes one. | Convergent (watch point 6). |
| **Applicability by population** (INV-076, E-053, E-041) | R02-06, R06-01, R07-02 | Each makes applicability more precise: symptoms for subjects with migraine and another type; guidance populations; type-specific time points. | Convergent. |
| **Menstrual-relation view** (E-060, E-061, INV-086, INV-087; OUT-030) | R01-08, R02-07, R03-02, R03-03, R04-01, R04-04 | No remark since iteration 04. R05-01 touched only the series conjunct of INV-105, not its cycle-line conjunct. | Stable since v04 (iteration-04 watch points 1 and 2). |
| **Clinician-facing summary** (E-066, INV-104; OUT-034) | R01-09, R02-02 (a), R03-04 | No remark since iteration 03. | Stable since v03 (iteration-04 watch point 3). |

**Settled points.** Reviews 05 to 08b list the same decisions as "not reopened (no new evidence)". The items behind them are unchanged since they were settled:

- INV-106 at MUST NOT (unchanged since v01);
- the AAN/AHS 14A and NVN window readings: `timing ↦ withinWindow` is unchanged since each rule was added, and the v08 Meaning only states that reading;
- INV-023 at any granularity, and the "> 3 months" reading of INV-045 (unchanged v00–v08);
- the MIDAS label choice; the 24-hour outcomes for cluster summaries; "history of previous bouts"; the OUT-031 end-of-bout Caveat;
- the context as subject properties; the HIT-6 one-month recall; the cluster remission "> 3 months";
- labels under a criterion that does not apply;
- the E-060 lead-in wording (unchanged since v04);
- NICE 1.3.27 applying to onabotulinumtoxinA: `ruleNice1327.excludes ↦ ∅` since v07, settled in review 07 and explicitly not reopened by R08b-02;
- "baseline administration" as any earlier administration: INV-082 and E-058 `baselineResult` are unchanged since v02. R05-02 restricts only which pair decides a responder score component.

**Remark counts per iteration:** 12, 7, 7, 4, 3, 1, 3, then 0 in review 08 and 2 in re-check 08b.

## Findings

None.

No item oscillates, so nothing is frozen and FROZEN_ITEMS.md is not written. Three points come closest to a back-and-forth pattern. Each is assessed below.

### A. E-041 applicability for a preventive treatment of another headache type without a type listing

The scenario script evaluates `applicable` as it stood in each version (anchors present). Y = the rule applies, . = it does not, - = the rule does not exist yet. Columns: v00, v01, v05, v06, v07, v08.

| Scenario | Rules whose applicability changed |
|---|---|
| A. Adult, migraine, topiramate (titrated, oral) | NVN `-YYYYY`; Ru71 `-YYYYY`; IHS Q2 oral and Turkish Box 8 `----YY`; NICE 1.3.27, AAN 14A, SIGN titrated `YYYYYY` |
| B. Adult, migraine, preventive with no type listing | NICE 1.3.27 and AAN 14A `.YYYYY`; Ru71 `-YYYYY`; Turkish Box 8 `----YY` |
| **C. Adult, cluster headache only, verapamil with no type listing** | **NICE 1.3.27 and AAN 14A `.YY...`**; Ru71 `-YY...` |
| C2. As C, with the listing `otherPreventive` | NICE 1.3.27 and AAN 14A `YYY...`; Ru71 `-YY...` |
| D. 10-year-old, migraine, titrated oral preventive | NICE 1.3.27, AAN 14A, SIGN titrated `YYY...`; Ru71 `-YY...`; NVN `-YYYYY`; IHS Q2 oral, Russian children, Turkish Box 8 `----YY` |
| E. Adult, migraine, onabotulinumtoxinA (also a quarterly injectable) | AAN 14A `YYYY..`; Ru71 `-YYY..`; AAN 14B, Russian 3.3 and Turkish 3.6.3.9 `----YY`; NICE 1.3.27, NICE 1.3.29, IHS quarterly `YYYYYY` |
| F. Adult, migraine, erenumab | all applicable rules `YYYYYY`; Ru71 `-YYYYY`; Turkish Box 8 `----YY` |

Only scenario C has a rule whose applicability changed twice (no → yes → no).

**Why it is not an oscillation:**

1. **The two changes are on different points, and neither was reversed.**
   - v00 → v01 (R01-02): a missing type listing can no longer switch the rules off. That guarantee holds verbatim in v08: scenario B is `.YYYYY`, and the fallback conjunct of INV-001 is unchanged.
   - v05 → v06 (R06-01): a rule applies only within its guidance population. That holds in v08: C2 is `YYY...`.
   - The v00 "no" in scenario C was the vacuous case that R01-02 removed, not a position on cluster headache. With a listing (C2), v00 already applied the rules.
2. **No item returns to an earlier state.** `applicable` and INV-001 only gained conjuncts (v01, v02, v06, v07). No rule component changed after it was set.
3. **The remarks do not compete.**
   - R06-01 corrected R01-02's premise with evidence that R01-02 had not considered: "R01-02's premise, 'NICE 1.3.27 applies to any prophylactic treatment', did not consider: that 1.3.27 is a recommendation on migraine prophylaxis" (review-iter-06.md). It required "Keep the R01-02 guarantee."
   - No remark argues that migraine guidance time points should apply to a cluster-headache or tension-type-headache preventive, or that a missing listing should switch rules off. There are no competing positions to freeze.

**Judgement:** convergent. The scenario-level "no → yes → no" is the composition of two one-directional changes on different dimensions (watch point 2).

### B. INV-050: the covered period of the withdrawal follow-up view and its series

The conjunct `v.covers.end = last(v.series.periods).end` was added in v03 by the fix-03 sweep ("This is the R03-04 kind of defect") and removed in v05 by the fix-05 sweep: "v04 required `v.covers.end = last(v.series.periods).end`, which no view ending between period boundaries can meet". The scenario script, with withdrawal starting on 1 March 2026 and monthly series:

| Scenario | v02 | v03 | v05 (= v08) |
|---|---|---|---|
| S1. Covers 1 March – 31 August, series = March only (the R03-04 kind of defect) | ✓ | ✗ | ✗ |
| S2. Covers 1 March – 31 August, series = all six months | ✓ | ✓ | ✓ |
| S3. Review day: covers 1 March – 15 April, series = March | ✓ | ✗ | ✓ |
| S3b. The same values, with the covered period stated as 1–31 March | ✓ | ✓ | ✓ |
| S4. Covers 1–20 March (no whole month), no series | ✗ | ✗ | ✓ |
| S5. Covers 5 March – 15 April, series from 1 March | ✓ | ✗ | ✗ |

S3 is admitted in v02, excluded in v03 and admitted again in v05. This is the same shape as the start of the menstrual-relation view assessed in check-after-iter-04 (its scenario S3′/S3).

**Why it is not an oscillation:**

1. **The item did not return to its v02 state.**
   - v05 still rejects the v03 targets: S1 (a series that shrinks to one period of a longer covered period, through `fillsPeriod`) and S5 (a covered period that does not begin on the start of withdrawal).
   - v05 adds what v02 lacked: headache days and acute-medication days for the covered period itself.
   - v05 also admits a short follow-up (S4), which no earlier version admitted.
2. **The v03 guarantee keeps its strength.** The v05 Notes keep it in so many words: the series "cannot shrink to a single period of a longer covered period".
3. **No remark drove either change, and no positions compete.** Both changes were fixer sweeps, applying R03-04 and R05-01 respectively to INV-050. No review asked to exclude S3. Review 06 verified the v05 form: "E-039, INV-049 and INV-050 for follow-up views that end between period boundaries" are "sound". Reviews 07, 08 and 08b raised nothing on it.

**Judgement:** convergent refinement. v03 overreached at the end of the covered period, and v05 qualified the overreach while keeping every v03 guarantee. This is now the second change on this point, one in each direction (watch point 4).

### C. The criterion of `EvaluationRule.excludes` (E-041) against its values

The criterion text changed once (v07 → v08), and the values never changed. The script `excl.py` applied each wording mechanically to all 17 rules, for every start date from 1 January 2024 to 29 December 2028. Cycle lengths were taken as the guidance states them: 12 weeks per cycle for NICE, from [S-106]; 3 months for the Turkish protocol, from [S-035] 3.6.3.9.

- **The v08 criterion reproduces all 17 values for every start date**, with no date-dependent case:
  - `ruleNice1327` excludes nothing: the end of the second 12-week cycle (168 days) lies inside the window, and 6 months is at least 181 days;
  - `ruleAan14A`, `ruleRu71` and `ruleTrBox8` exclude exactly onabotulinumtoxinA;
  - the 14 other rules exclude nothing.
- **The v07 wording, read literally, disagreed with 6 values.** Read literally, "the types for which the same guidance names another time point" would make `ruleNice1327` exclude CGRP inhibitors and onabotulinumtoxinA. It would also make `ruleNice1328`, `ruleNice1329`, `ruleAan14B`, `ruleRu33Bta` and `ruleTr3639` exclude their own type.
- **Populations and exclusions never moved back.** Rule populations (`headacheType`, `ages`) and `excludes` values were each set once and never changed (Method, step 4).
- The change v07 → v08 moves the text toward the values. The NICE rationale went from absent (v00–v06) to "names no exception" (v07) to the timing argument (v08). That sequence is A → B → C, not a return.

**Judgement:** convergent. The criterion and the values agree in v08.

**One imprecision remains (not a finding of this check).** The short form of the Readings of INV-001, INV-055 and INV-059, and of the E-043 Notes, is "a later time point of its own". The full criterion in E-041 is "after this rule's time point or, for a window, after its latest date". Read as "later than the window's first date", the short form would again point at excluding onabotulinumtoxinA from NICE 1.3.27, because 168 days is later than 3 months. See watch point 1.

## Things the next checker should watch

1. **`excludes` and the NICE 1.3.27 / Turkish Box 8 pair (E-041).**
   - History: the values were set in v07 (R07-02) and the criterion text was corrected in v08 (R08b-02). Review 07 settled NICE 1.3.27 for onabotulinumtoxinA, and R08b-02 did not reopen it.
   - **Treat as oscillation:** any change of `ruleNice1327.excludes` or `ruleTrBox8.excludes`, for example R08b-02's option (b) "treating NICE 1.3.27 and Turkish Box 8 alike", unless it rests on evidence beyond the TA260 12-week interval and the [S-035] 3-monthly injections.
   - **Not oscillation:** aligning the short Readings ("a later time point of its own") with the full criterion, provided no value changes.
2. **Dimensions of E-041 applicability.** Three guarantees are now in place:
   - (i) the INV-001 fallback type (R01-02);
   - (ii) the guidance population (R06-01);
   - (iii) the type exclusion (R07-02).

   Scenario C (Findings, A) has already moved twice through (i) and (ii). Re-applying migraine or adult guidance outside its population, dropping the fallback, or letting a missing listing switch rules off would reverse an earlier fix.
3. **The rule list boundary and `ruleRuChildren` (E-041, ISS-10).**
   - v06 kept the [S-034] paediatric time point out of the list and put it to the human in ISS-10.
   - v07 modelled it as a rule, through a sweep that no remark asked for, and ISS-10 now asks the human to confirm it.
   - Removing `ruleRuChildren`, or the Turkish rules, on the ground that their guidance is not OUT-018 guidance would be A → B → A. That question already belongs to the human through ISS-10.
   - Likewise, returning the boundary to "the Stage 1 quotes only" would reverse R07-01.
4. **INV-050 and E-039 (covered period vs series).** The point was tightened in v03 (fix-03 sweep) and qualified in v05 (fix-05 sweep). A third change in either direction should be treated as oscillation unless it rests on evidence neither sweep considered. Examples: re-adding the exact end tie, or loosening `fillsPeriod` or the start tie.
5. **Responder labels (E-045, E-046, INV-062, INV-063).** They changed in iterations 01, 02, 05 and 08. A remark that does any of the following would reverse an earlier fix:
   - closes `UnderlyingKind` or `PeriodValueKind` again, or removes `otherValueNamed` (R08b-01);
   - relaxes `#L.evaluated = 1` (R01-04);
   - relaxes the `evaluationResult` / `pretreatmentBaseline` pair or the `rc.treatment = L.treatment` tie (R05-02).

   The fix-08 decision to keep intensity and duration thresholds as `judgement` components is new. A remark that makes them decidable should name a cited statistic; otherwise it would contest that decision without new evidence.
6. **v08 sweep items (first change in v08):**
   - INV-100 now covers instrument grades and screening results as indicators (Realises +OUT-026, +OUT-033);
   - E-013 `otherCompletenessExpression`;
   - the E-045 `namedCriteria` gloss.

   A remark narrowing these back would be a reversal.
7. **Iteration-04 watch points.**
   - The start of the menstrual-relation view (INV-087 and the lead-in), and E-060, E-061 and INV-087 as a whole: unchanged since v04.
   - INV-104: unchanged since v03.
   - INV-105: changed once since then, in v05 (series conjunct, R05-01; the cycle-line conjunct unchanged since v02).

   Keep watching them. A change to any of them would now be the first since iteration 04 or 05, and should be checked for reversal of R02-07, R03-02, R03-03, R04-01, R04-04, R02-02 (a), R03-04 or R05-01.
8. **Timing readings.** The v08 E-041 Meaning states the settled rule: a range worded as a minimum is a window (AAN 14A, NVN, Turkish Box 8). Any change of a rule's `timing` would reopen the settled window readings.

## Conclusion

No item of the model oscillates after eight iterations, and nothing is frozen.

- **No returns.** No item (element, attribute, field, invariant, rule or criterion constant, source, section, value set, conformance level or traceability row) returns to an earlier state.
- **Rule values.** No component of the 17 evaluation rules or the 6 responder criteria changed after it was set. Rule populations and `excludes` values were each set once.
- **Conformance levels.** No conformance level changed more than once, and no invariant changed level.
- **Remarks.** No remark asks to undo an earlier fix, and no declined remark was raised again. Two remarks (R06-01, R07-02) revised an earlier premise or not-raised judgement, each with evidence that no earlier file had considered, and each kept the earlier fix.
- **Focus items.**
  - **E-041 and its invariants (INV-001, INV-055, INV-058, INV-059).** Every change since v01 has been a one-directional addition on a new dimension: the rule list, the population, then the type exclusion. The v08 change brings the stated `excludes` criterion into agreement with all 17 unchanged values.
  - **Responder labels (E-045, E-046, INV-062, INV-063).** They gained conjuncts and open kinds only.
  - **Iteration-04 watch points.** They are untouched since v04 (menstrual-relation view) and v03 (INV-104).
- **Near-patterns.** Two points came closest to a back-and-forth: scenario C of E-041 applicability, and S3 of INV-050. Both are compositions of changes that keep every earlier guarantee, and in neither case does any remark take the opposite position. They are listed above as watch points, not frozen.
- **Remark counts** fall overall: 12, 7, 7, 4, 3, 1, 3, then 0 + 2 in iteration 08.

The scripts used are in the session scratchpad (`osc08/`): `split.py`, `analyse.py`, `rules.py`, `show.py`, `ngram.py`, `docwide.py`, `conf.py`, `remarks.py`, `applic.py`, `excl.py` and `inv050.py`. FROZEN_ITEMS.md was not written, and OUTPUT_MODEL.md and the history snapshots were not changed.
