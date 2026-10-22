# Fix log — iteration 24
Input review: reviews/review-iter-24.md · Input version: v23 · Output version: v24
Date: 2026-10-21

**What I read.** Stage 2 PROCESS.md. Stage 1 v18 sections 1–3, with OUT-001 to OUT-004, OUT-014, OUT-016 and OUT-029 read again for this fix. v23 in full. Review 24, with the reviewer's scripts (`r24/scripts/atoms.py`, `atoms2.py`, `mech.py`, `names.py`). By search, the fix-04 row of R04-03 and its sweep, the fix-12 row of R12-02, and the oscillation checks after iterations 12 and 16 with their watch points. `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line.

**What I checked before changing anything.**
- **R24-01.** I ran `atoms2.py` under v23. Both of the review's views are admitted by every predicate it evaluates:
  - view 1: March 2026 is shown as three period atoms, with headache days 5 and 7, moderate/severe headache days 9, total acute-medication days 4, triptan days 9 and sumatriptan days 8;
  - view 2: April 2026 triptan days are 8 under the April indicator and 12 under the May indicator.
  - I confirmed in the text that INV-006, `daysOf` (E-014), the EventCount conjuncts of INV-030 and INV-033 and the rate–count conjunct of INV-089 compare period atoms (`m.period = p`).
  - INV-003 admits several atoms with the same dates in one view (its last conjunct and Notes).
  - The remark holds.
- **R24-02.** INV-008 asks only for `∃ l • l.measure = lm`. A view with two migraine-day labels naming [S-002] and [S-043] satisfies it, and so does a change labelled A whose values are shown, labelled B, in another view. Both are admitted by v23 (script below). E-016 and E-017 presuppose one label. The remark holds.
- **Same defect elsewhere.** I swept every predicate that compares a period atom (`.period =`, `∈ ran …`, `i₂.period = i.period`) and sorted each comparison into one of two kinds.
  - **Relations between shown values meant to hold "for the same period".** Comparing atoms admits contradictory values here. Changed (see Other changes).
  - **Presence and structural ties.** These ask for a value, mark, indicator or summary for a given period atom, or tie an item to its own atoms: `dayCount`, `shownDay`, `perPeriod`, INV-011 conjuncts 1, 3 and 4, INV-027, INV-037 to INV-039, INV-044, INV-045 (basis and span), INV-056, INV-057, INV-061, INV-062, INV-069, INV-071, INV-088, INV-092, INV-104 and INV-105. Comparing atoms is stricter here and admits no contradictory value. They also carry the co-presence decisions (watch point 3: R10b-01, R11-01). Not changed.

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R24-01 | fixed: the review's option (a), compare by dates, within one view | E-014 (`daysOf`, Meaning, Notes); INV-006 (Predicate, Reading, new Notes); INV-030 (Predicate, Reading); INV-031 (Predicate, Reading, Notes); INV-033 (Predicate, Reading); INV-089 (Predicate, Reading, Notes); INV-012 (Predicate, Reading, new Notes); INV-011 (Notes); E-032 (new `sameIndicatedPeriod`; `classShownUsed`, `classUseExcluded`; Notes); INV-045 (Notes); INV-046 (Predicate, Reading, Notes); INV-003 (Notes); E-013, E-019, E-022 and E-064 (Notes); INV-024 (Reading); rows OUT-003, OUT-004, OUT-014, OUT-016 and OUT-029 (coverage reason) | **INV-006.**<br>• The new form is `m.measure = n.measure ∧ m.typeScope = n.typeScope ∧ sameSpan(m.period, spanOf(n.period)) ⇒ m.days = n.days ∧ (m.period = n.period ⇒ m = n)`, and the same for `EventCount.count`.<br>• Counts of the same dates agree, whatever the atom or the kind of the period. The number of days with a property in a span of days does not depend on the period's kind, so February 1–28 as a calendar month and as a 28-day period show one number.<br>• The v23 identity for one atom is kept, so no v23 guarantee is lost. The INV-062 Notes ("referenced rather than repeated") stay true.<br>**`daysOf`** collects the counts of a period with the dates of p (`sameSpan(m.period, spanOf(p))`). Through it, INV-024, INV-030 (conjunct 1), INV-031, INV-032, INV-033 (conjunct 3) and `levelDays` (INV-062, INV-064) apply to every value of the same reporting period.<br>**EventCount and rate conjuncts** compare dates:<br>• INV-030 conjunct 2: `sameSpan(e.period, spanOf(f.period))`;<br>• INV-033 conjunct 2: `sameSpan(e.period, spanOf(a.period))`;<br>• INV-089, rate–count conjunct: the attack counts and the rates of a period with the dates of the rate's period. The antecedent is unchanged (`r.period = p`), so p still ranges over the rates' own atoms.<br>**INV-031, last conjunct** (marks): `sameSpan(mk.period, spanOf(p))`. This change is needed, not optional. With date-based `daysOf` and the atom form, a 0-day count in v together with a same-dated atom p of another view would require a mark in v whose period is p. INV-003 excludes that (script: unsatisfiable). The fifth conjunct (`mk.period = p`) already works by dates through `daysOf` and is unchanged.<br>**Completeness (INV-012).** New conjunct: for every two indicators of one view with the same dates, `∃ n • ∀ e ∈ ci.expressions ∪ cj.expressions • (e = coveredDays(k) ⇒ k = n) ∧ (e = proportionCovered(q) ⇒ q ≈ 100 × n ÷ lengthDays)`.<br>• Covered days are equal, and proportions are roundings of the same exact value. Two proportions shown with different numbers of decimals (90.3 % and 90 %) are therefore still admitted, which an equality would have excluded.<br>• By script, pairwise agreement implies one common number (0 counter-examples in 20,000 random sets). The INV-012 Notes state this.<br>• INV-011's presence conjunct is unchanged.<br>**Medication-overuse indicators.**<br>• The basis values of one view now agree for periods with the same dates (INV-006), which rejects the review's view 2 (INV-045 Notes).<br>• The "class indicators of the same period" that `classShownUsed`, `classUseExcluded` and INV-046 read are matched by a new predicate, `sameIndicatedPeriod(i₂, i) ≙ i₂ ∈ viewOf(i).content ∧ sameSpan(i₂.period, spanOf(i.period)) ∧ i₂.period.kind = i.period.kind`. Atom equality implied the same view; the new predicate states it.<br>• The kind is part of the match because a calendar month and a 28-day period with the same dates have spans with different dates (INV-045). An indicator for February as a calendar month (November–February) and one for 1–28 February as a 28-day period (9 November – 27 February) may legitimately differ.<br>• New INV-046 conjunct: combined-use indicators of the same period in one view give the same indication. The combined status is left open between the two cases of INV-046, so it is not implied. For a class, the status follows from the basis (INV-045 with INV-006).<br>**Not output-wide.** The review leaves this choice to the fixer. Views of one output may follow different definitions for migraine days and moderate/severe headache days (INV-008 labels are per view), and the model has no per-value definition. So the agreement is stated within one view, as the Readings of INV-006, INV-024, INV-030, INV-031 and INV-089 already said.<br>**Watch points.**<br>• The INV-003 predicate (the v12 period requirement) is unchanged.<br>• The co-presence derivations (INV-038, INV-054, INV-056; R10b-01, R11-01) are unchanged. A value of a comparison is still tied to the comparison's own atoms, and "a value shown in another view with a period of the same dates … is not a value of that comparison" stays.<br>• The INV-003 Notes gain a paragraph on same-dated atoms that says so. |
| R24-02 | fixed: the review's option (a), with the uniqueness stated definitionally | new INV-111 (definitional, E-011); E-011 (Meaning, Conformance, Notes); E-016 and E-017 (Meaning); E-040 (Conformance, Notes); INV-008 (Reading, Notes); INV-031 (Notes); row OUT-002 (INV-111 added; coverage reason) | **INV-111** (definitional, E-011, Realises OUT-002). Two conjuncts:<br>• (1) all the definition labels of one view for one measure name the same definition;<br>• (2) a view that shows a change, a residual burden or a composite index whose values of a labelled measure are shown in another view states, where both views state a definition for the measure, the definition of that view.<br>The review's second part asked for this, for values shown in another view; conjunct (2) takes its first alternative ("where both views state a definition for the measure, the two are the same").<br>**Why definitional, and why INV-008's predicate is unchanged.**<br>• A label states the definition its view follows for the measure. The values of one measure in one view follow one definition: one value per measure, period dates and scope (INV-006), and the R04-03 premise of INV-024, INV-030 and INV-031. So a second label with another definition is a false statement about the values it labels. Section 3.3 item 5 places exactly such outputs outside the element. This is the "definitionally" of option (a).<br>• With INV-111, `∃ l • l.measure = lm` (INV-008) is equivalent to `∃ d • labelledAs(v, lm, d)`. The review's replacement of INV-008's consequent would therefore duplicate INV-111's first conjunct, so INV-008 keeps its predicate and SHOULD level, and its Reading and Notes now state the consequence: a view that meets INV-008 states exactly one definition per measure.<br>**Meanings.** E-016 and E-017 now read "under the one published definition that the view follows …, which its definition labels name (E-011, INV-111)". The E-011 Meaning states that every value of the measure the view shows or refers to follows that definition. The E-040 Notes and Conformance state that the change's label names the definition its values follow.<br>**Kept.**<br>• R04-03: `labelledAs` and the INV-031 conjunct are unchanged.<br>• R12-02: `reports` and `referencedValues` are unchanged, and so is the INV-008 antecedent.<br>• INV-009 and INV-010 are unchanged.<br>**Level.** OUT-002 is SHOULD, and INV-008 keeps it. INV-111 adds no presence requirement: a view without a label meets it. Values under two definitions are shown in two views. Neither Stage 1 nor the model requires one view to show both: INV-006 already allowed one value per measure, atom and scope in a view since v00.<br>**Satisfiability.**<br>• A view meets conjunct (1) by stating one definition per measure. INV-009 and INV-010 fix one definition for headache days and attacks. INV-042 needs one headache-day and one migraine-day label.<br>• A view meets conjunct (2) by stating the definition of the view of its values.<br>• No invariant requires an item to refer to values in views with different definitions. The changes of a response comparison are shown with their values (INV-054, MUST). The residual burden's day counts are in the change's view (INV-060), and a migraine index's components in the index's view (INV-092). The changes outside comparisons, which may have their values elsewhere (R10b-01), are optional. |

## Other changes

The same defect, a relation that compares period atoms where it is meant to hold for the same period, was found in three more places. Each is changed to compare dates.

1. **INV-053** (definitional, E-040). `ch.reference.period ≠ ch.compared.period` admitted a "change" between two atoms of the same month. It is now `¬ sameSpan(ch.reference.period, spanOf(ch.compared.period))`. The Reading reads "two different periods, periods with different dates", and the E-040 Notes are updated. Every change that an invariant requires compares periods with different dates: the baseline of a response comparison ends before the treatment start, and its on-treatment periods begin on or after it (INV-056).
2. **E-046 `reductionMet`, `reductionDecided`, `attackReductionMet`, `attackReductionDecided`** (used by INV-063, definitional). These matched the change's compared period, and the attack counts' periods, with the label's evaluated periods and the comparison's baseline by atom.
   - A label whose evaluated period is an atom of its own with the dates of its comparison's on-treatment period was decided by no component. A label "non-responder" next to a 60 % fall for the same month was therefore admitted. This needs only a deviation from INV-062's SHOULD that `ran L.evaluated ⊆ ran rc.onTreatment`, or the comparison shown in another view.
   - The four predicates now match these periods by dates (`∃ p ∈ ran L.evaluated • sameSpan(…, spanOf(p))`; `sameSpan(b.period, spanOf(rc.baseline))`), as `levelDays` (INV-064) now does through `daysOf`. The E-046 Notes state it.
   - Watch point 2 (iteration 12) is kept. `#L.evaluated = 1`, `rc.treatment = L.treatment`, `ch.reference.typeScope = allTypes`, `attackScope`, the `evaluationResult` / `pretreatmentBaseline` pair, `conditionHolds` and `evaluatedOnTreatment` are verbatim. `ch.reference.period = rc.baseline` is kept; INV-056 requires it of every change of a comparison.
   - For a label that meets INV-062, the evaluated periods are atoms of its comparison, and the decision is the same as in v23.
3. **INV-062, control-level conjunct.** It reads `levelDays`, and so now accepts the days with migraine or moderate-to-severe headache of the evaluated month shown on any atom with its dates in the label's view. It still requires them in the label's view. No predicate text of INV-062 changed.

**Text aligned** (no formal change):
- the Readings of INV-024, INV-030, INV-031 and INV-033, which now say "periods with the same dates";
- the Notes of E-013, E-019, E-022 and E-064;
- the INV-011 Notes (several atoms ask for several indicators; INV-012 makes them agree).

**Bookkeeping:**
- the header ("Version: v24 · Iteration: 24 · Status: under review");
- section 9 ("as of v24");
- section 11 (an iteration-24 paragraph: no search, no download, no new source);
- section 12 (the v24 entry).

**Checked and not changed:**
- INV-061 (`m.period = rb.change.compared.period`): a structural tie, stricter than dates, in the settled INV-060/INV-061 area.
- INV-045 basis and span ties: the indicator's own atoms.
- INV-038 and INV-056 membership: watch point 3.
- The non-count per-period values (intensity, duration and symptom summaries, caregiver impact, indices). INV-006 has never constrained their uniqueness, even by atom, so this is not R24-01's defect and is not added.

**Items changed.** 31 items and rows. One invariant was added and none was withdrawn.
- Elements (11): E-011, E-013, E-014, E-016, E-017, E-019, E-022, E-032, E-040, E-046, E-064.
- Invariants (14): INV-003, INV-006, INV-008, INV-011, INV-012, INV-024, INV-030, INV-031, INV-033, INV-045, INV-046, INV-053, INV-089, and the new INV-111.
- Traceability rows (6): OUT-002, OUT-003, OUT-004, OUT-014, OUT-016, OUT-029.
- Formal (`omn`) blocks changed (12, by script against `history/v23.md`): E-014, E-032, E-046, INV-006, INV-012, INV-030, INV-031, INV-033, INV-046, INV-053, INV-089, and the new INV-111.
- Not changed in any existing item: values, axioms, attribute declarations, conformance levels and Realises fields.

## Checks

All scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix24/` and were run with `python3 -I`.

- **Counter-examples and correct outputs** (`check24.py`). The script evaluates the changed predicates literally, in their v23 form (atoms) and their v24 form (dates): INV-002, the INV-003 period part, INV-005, INV-006, INV-012, INV-024 (conjuncts 1 and 2), INV-030, INV-031 (conjuncts 1, 2, 5 and 6), INV-033 (conjunct 2), INV-045, INV-046, INV-053, INV-089 (rate conjunct), INV-008, INV-111, and INV-063 with E-046 for a reduction component.
  - **(i) Review counter-examples, admitted by v23 and rejected by v24:**
    - R24-01 view 1: rejected by INV-006, INV-024 and INV-031;
    - R24-01 view 2: rejected by INV-006;
    - R24-02, two migraine-day labels in one view: rejected by INV-111;
    - R24-02, a change labelled A whose values are labelled B in another view: rejected by INV-111.
  - **Further instances of the same defect, admitted by v23 and rejected by v24:**
    - two March indicators stating 28 and 20 covered days, or 28 days and 50 % (INV-012);
    - 31 attacks with 1.0 per day on one atom and 14.0 per week on another (INV-089);
    - a change from March to March (INV-053);
    - 5 migraine attacks against 3 attacks of all types (INV-030);
    - 6 attacks with nausea against 4 attacks (INV-033);
    - combined use "reached" next to triptans "reached" on another atom for the same months (INV-046);
    - two combined indications for April that differ (INV-046);
    - a "non-responder" label on its own April atom next to a 60 % fall (INV-063).
    - In all, 13 of 13 counter-examples are admitted by v23 and rejected by v24.
  - **(ii) Correct outputs, all admitted by v24 (6 of 6):**
    - March on three period atoms, as INV-003 permits, with one value per measure and scope, indicators stating 28 days / 90.3 %, 90 % and 28 days, marks and rates;
    - April and May triptan indicators on atoms of their own, with April at 12 days in both;
    - February 2026 shown as a calendar month and as a 28-day period (1–28 February) in one view: equal day counts, and overuse indicators of each kind with different spans and different statuses;
    - a change labelled A whose values are labelled A in another view, next to a third view that labels migraine days B;
    - a "responder" label on its own April atom;
    - a 0-migraine-day month marked on another atom, with a third March atom in another view of the output.
    - v23 rejects two of these six: it asks for a migraine-free mark on every atom (INV-031 conjunct 6).
- **Satisfiability** (`sat24.py`). 150 random views over October 2025 – June 2026, each a witness whose values are mutually consistent by construction:
  - one random set of calendar days for each property (headache, moderate/severe headache, migraine, headache-free, each drug, coverage) and a number of attacks per day; every count of a span is then the number of days of that span in the set, as E-014 defines a count, so all counts of one span agree and the relations among counts hold;
  - each view with 0 to 2 extra atoms per period, and 24 or more period atoms per view;
  - with calendar months and the four 28-day periods ending 28 February 2026;
  - with completeness stated at random precisions, marks on random atoms of their dates, and rates;
  - with class and combined overuse indicators for February–June and for the 28-day February, each on random atoms;
  - with one definition label per measure.
  - Result: 0 failures of the v24 predicates (INV-002, INV-003, INV-005, INV-006, INV-012, INV-024, INV-030, INV-031, INV-033, INV-045, INV-046, INV-089, INV-008, INV-111).
  - The same script shows that INV-031 conjunct 6 in its atom form, combined with date-based `daysOf`, fails as soon as another view of the output has an atom of the same month.
- **Satisfiability argument for the constraints on the same elements.**
  - INV-006 with INV-003, INV-005, INV-014 to INV-017, INV-108, INV-024, INV-030 to INV-033, INV-037, INV-038, INV-040, INV-041, INV-044, INV-045, INV-050, INV-054, INV-056, INV-057, INV-062, INV-068 to INV-070, INV-104 and INV-105: a consistent view gives every count of one measure, scope and dates the number of days of that span that have the property, so the presence requirements, which still name atoms, and the relations, which now compare dates, hold together.
  - INV-012 with INV-011: indicators that state the covered days of their dates, or a proportion obtained from them, agree.
  - INV-111 with INV-008, INV-009, INV-010, INV-031 and INV-042: one definition per measure and view.
  - INV-046 with INV-044, INV-045, INV-047, INV-048, INV-100 and INV-104: the indicators of the same dates and kind rest on the same basis.
  - INV-053 with INV-056, INV-060, INV-061 and INV-097.
  - INV-089 with INV-088.
  - E-046 with INV-062 to INV-064.
- **Mechanical checks** (PROCESS.md section 11; the reviewer's `mech.py` with the invariant range extended to INV-111, and `names.py`). All pass.
  - IDs: 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111), none missing or duplicated. ISS-01 to ISS-12 without ISS-07 (withdrawn). No dangling E-, INV-, ISS- or S- reference; 36 source IDs cited.
  - Fields: every element and invariant has its five fields exactly once and at most one Notes field, and every invariant states its scope.
  - Traceability: 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every row, the Elements and Invariants columns equal the items whose Realises field names the requirement (0 mismatches); INV-111 is in row OUT-002.
  - Invariant levels: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34 (v23: 33, plus INV-111). Every MUST NOT and SHOULD NOT predicate has the form `¬ F`.
  - Attribute levels: 172 level-annotated declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged; the typing rule holds for all.
  - Names: 746 declarations (v23: 745, plus `sameIndicatedPeriod`), no paragraph name declared twice. The script's residue list of tokens is byte-identical to that of v23. In the 39 changed or new `omn` lines, every attribute selection names a declared attribute, and the only new identifiers are `sameIndicatedPeriod` (declared in E-032) and the bound variables `l₁`, `l₂` and `cj`.
  - Typing and definedness, checked by hand: `sameSpan : Period × DateSpan` and `spanOf : Period → DateSpan`, whose `where` clause INV-002 guarantees (section 2.6); `viewOf` is total on items, including the per-period values of INV-111 and the indicators of `sameIndicatedPeriod`; `÷` in INV-012 divides by `lengthDays : ℕ₁`.
- **Quotes.** The only quotes added are the Stage 1 OUT-002 Statement and Rationale, in the INV-111 Evidence and the E-011 Notes. Both were found verbatim in Stage 1 v18 (`grep`, 1 hit each).
- **Scope sweep.** The added lines were searched for record, enter, entry, input, captur, store/storage, database, serialis/serializ, JSON, XML, CSV, FHIR, encod, retention, persist, reminder, data field, data-entry, logged, answer and question: 0 hits. Every changed relation takes output elements only: counts, periods and their dates, indicators, labels, rates and changes.
- **Diff check.** Against `history/v23.md`: 59 fields changed in 31 items and rows, plus the header and sections 9, 11 and 12. The `omn` blocks changed are the 12 listed above. No source row, search-log row, Stage 1 issue or withdrawn row changed. `history/v24.md` is byte-identical to `OUTPUT_MODEL.md` (`cmp`). Only `OUTPUT_MODEL.md`, `history/v24.md` and this log were written; nothing was committed.
