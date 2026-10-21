# Fix log — iteration 09
Input review: reviews/review-iter-09.md · Input version: v08 · Output version: v09
Date: 2026-10-21

## What was downloaded and checked

**Frozen items and watch points.** FROZEN_ITEMS.md does not exist, and the oscillation checks after iterations 04 and 08 froze nothing, so no item is frozen. The fix respects watch point 5 of oscillation/check-after-iter-08.md:
- no list is closed: `UnderlyingKind` gains a tag, `PeriodValueKind` is unchanged, and `otherValueNamed` is kept;
- `#L.evaluated = 1` (R01-04) is unchanged in all four deciding predicates;
- the `evaluationResult` / `pretreatmentBaseline` pair and the `rc.treatment = L.treatment` tie (R05-02) are unchanged;
- intensity and duration thresholds stay `judgement` components (fix-08 decision).

The other watch points are untouched: the 17 evaluation rules and the six named criteria are byte-identical to v08 (checked by script), and nothing changed in E-041, E-060, E-061, INV-050, INV-087, INV-104 or INV-105.

**Earlier work read so that no fix is undone.**
- PROCESS.md; Stage 1 v18, sections 1–3 in full; v08 in full; review 09.
- Fix logs 05 and 08, the iterations that shaped the responder relations.
- Review 01 ("INV-091 / INV-093 (`concerns` for all-types values of mixed-type subjects): the scope reading is defensible"), review 02 (labels under a criterion that does not apply are not a defect), fix 05 (R05-03 introduced the cluster-rate scope tie with `concerns`).
- The oscillation check after iteration 08.

**Downloads.** All downloads went with `curl` into the fresh directory `/tmp/fix09-dl-Ayuv`, outside the repository, and all returned HTTP 200. PDFs were extracted with `pdftotext -raw` and `-layout`; the web page and the Europe PMC XML had their markup removed. Scripts were kept in the session scratchpad (`fix09/`) and run with `python3 -I`.
- **[S-035] Turkish Ministry of Health Migraine Clinical Protocol** (92-page PDF):
  - Kutu 8 (PDF p. 48): "Ölçüt atak sıklığında en az %50 azalma olması," is the second item, under "Kutu 8. Migren Profilaktik Tedavi-Yönetim-6".
  - Section 3.3 "Farmakolojik Tedavi", item "b. Profilaksi" (PDF p. 23, printed p. 13): "Migren önleyici tedavi; migren ataklarının sıklığını, şiddetini ve süresini azaltmayı ve hastanın genel yaşam kalitesini iyileştirmeyi amaçlar." This is the new quote.
  - Section 3.6 (PDF p. 44) and Kutu 1 speak of the attacks of migraine patients in the same sense.
- **[S-015] NICE CG150 Recommendations page**: 1.3.28 "the frequency of migraines"; 1.3.29 "the frequency of headache days per month".
- **[S-008] IHS 2024** (31 pages): Q6 "monthly migraine days or moderate-to-severe headache days" (p. 12).
- **[S-023] DMKG/ÖKSG/SKG** (Europe PMC XML of PMC9607711): "die Migränetage um mindestens 50 %".
- **[S-033] Russian clinical recommendations for adults** (92 pages): section 7.1, "число дней с ГБ" (p. 53).
- **[S-010] IHS position statement 2025** (11 pages): every control level counts "days with migraine or moderate-to-severe headache" (p. 6).
- **[S-030] Danish reference programme** (86 pages): "hyppigheden eller styrken af migræne" (PDF p. 19).
- **[S-001] ICHD-3**: downloaded for reference; no new quote.

**Quote check.** Every double-quoted string that is new in v09, outside the `omn` blocks, was searched by script in the downloaded texts, in Stage 1 v18 and in v08, after normalising whitespace, quotes and dashes (script `newquotes.py`):
- 12 were found verbatim in a source;
- 2 are Stage 1 text;
- 1 is an English translation;
- 1 is a model term ("∃ sc", in the change log).

**Verification of the remark.** R09-01 holds. I checked the v08 text myself:
- `reductionMet` and `reductionDecided` accept a change `ch ∈ rc.changes` of any `typeScope`.
- INV-053 requires only that a change compares two values of the same scope. INV-056 requires the all-types changes of headache and migraine days but admits further changes, for example per headache type.
- `attackReductionMet` and `attackReductionDecided` require only `b.typeScope = f.typeScope`.
- INV-062 required the per-period values "∃ sc : TypeScope", so a label could show the attack counts of one type only.
- The scenario script (`scen09.py`) reproduces the review's examples on the v08 predicates:
  - `critRu71` with all-types headache days 20 → 14 (30 %) and tension-type headache days 10 → 4: v08 forces "responder";
  - only tension-type attack counts 6 → 5 shown under an attack criterion: v08 forces "non-responder".

**Not followed: the review's option (a) for attack counts.** The review takes the Turkish Box 8 criterion to count all of the person's attacks. The protocol's own text says otherwise. The Box 8 item names "atak sıklığı" (attack frequency) without a type, and the same protocol states that migraine preventive treatment aims to reduce "migren ataklarının sıklığını" (the frequency of migraine attacks; section 3.3 b).

With option (a), a subject with migraine and tension-type headache would show the opposite defect. Example: migraine attacks fall 6 → 2 (67 %), tension-type attacks rise 6 → 8, so all attacks fall 12 → 10 (17 %). The all-types counts would force "non-responder", although the criterion, applied to the attacks it names, is met.

So the attack component takes the review's option (b). Its scope is stated from the criterion's own source text, with a verbatim quote, as PROCESS.md section 4 requires. For the reduction components, the sources state no restriction to a headache type, so option (a) applies (see the table).

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R09-01 | fixed: option (a) for reduction components; option (b) for attack-reduction components | E-012 (Definition: new `onlyOfType`, `scopeFor`; Meaning; Realises +OUT-020 +OUT-023 +OUT-031; Evidence; Notes); E-045 (Definition: `AttackReductionComponent.headacheType`, new `UnderlyingKind` tag `typeValuesOf`, `where` clause, `valueAvailable`, comments; Meaning; Evidence with one new [S-035] quote; Notes "Other values", "Thresholds…", new "**Type scope**"); E-046 (Definition: `reductionMet`, `reductionDecided`, new `attackScope`, `attackReductionMet`, `attackReductionDecided`; Meaning; Conformance; Notes); INV-062 (Predicate, Reading, Evidence, Notes); INV-063 (Reading, Evidence); section 7 row OUT-020 | **Principle (E-045 Notes, Type scope).** A component is decided only on values of the headache types its measure refers to. It is never decided on values of another type scope. The reader applies the named criterion to such values, which INV-062 still shows.<br>**Reduction components: option (a).** `ch.reference.typeScope = allTypes` was added to `reductionMet` and `reductionDecided`; INV-053 gives the compared value the same scope.<br>• Every named criterion with a reduction component names a day measure of the person and does not restrict it to the days of one headache type: "the frequency of migraines" (NICE 1.3.28), "the frequency of headache days per month" (NICE 1.3.29), "monthly migraine days or moderate-to-severe headache days" (IHS Q6), "die Migränetage" (DMKG/ÖKSG/SKG) and "число дней с ГБ" (Russian 7.1). All are Stage 1 quotes, listed in the E-045 Evidence.<br>• The measure itself states which days it counts. Headache days are days "affected by headache" ([S-001]), and migraine days follow the definition the view names.<br>• All-types is also the scope of the comparison's own values (INV-056, INV-057) and of `levelDays`.<br>• The six criterion constants are therefore unchanged.<br>• A criterion whose day measure is restricted to one headache type, which no named criterion is, is a `judgement` component that names its values with `typeValuesOf`.<br>**Attack-reduction components: option (b).** New component `headacheType : opt HeadacheType`: the headache type whose attacks the component counts; ∅ means the attacks of all types combined.<br>• An attack count has no headache type of its own (E-019; ICHD-3 "frequency of attacks").<br>• Box 8, the only attack criterion in the evidence, counts migraine attacks (new [S-035] quote above), so its component has `headacheType = {c1}`. It is an example in the Notes, not a named constant.<br>• New `attackScope(c, a, sc)`. `attackReductionMet` and `attackReductionDecided` now test only counts b and f with `attackScope(…, a, b.typeScope) ∧ f.typeScope = b.typeScope`.<br>**Which scope holds the values of one type (E-012).**<br>• New `onlyOfType(c, sc, t) ≙ concerns(c, sc, t) ∧ (sc = allTypes ⇒ ∀ h ∈ possibleHeadacheTypes • h ⊑ t)`.<br>• New `scopeFor(c, sc, t)`. It is all types combined where the subject has a type and every type it has or may have falls under t; otherwise it is `ofType(t)`. Exactly one scope satisfies it.<br>• "May have" counts because OUT-029 presents values per type whenever the patient "has, or may have" more than one type (INV-028). An all-types value of such a subject includes headaches that the output presents under the other type.<br>• `scopeFor` is a single canonical scope, so a component is never decided on a subtype value that covers only some of the type's headaches. Example: migraine with aura only, in a subject who also has migraine without aura.<br>**Values the label shows (INV-062, SHOULD).**<br>• `periodValuesOf(k)` now means values over all types combined, and INV-062 requires them at `allTypes` instead of "∃ sc".<br>• New tag `typeValuesOf ⟨PeriodValueKind × HeadacheType⟩` for the values of one type, required in the scope `scopeFor`. `valueAvailable` adds `mayHaveType(c, h)` for it, and acute-medication use for its acute-summary kind. An example is the frequency or intensity "af migræne" of [S-030] for a subject who also has another type.<br>• The `where` clause makes an attack component list `periodValuesOf(eventCountsOf(attacks))`, or `typeValuesOf((eventCountsOf(attacks), t))` when it names t.<br>• The changes of reduction measures are required over all types combined.<br>• The two tags together express every scope that "∃ sc" admitted, but each criterion now states its scope. No list is closed.<br>**Effect (script `scen09.py`, v08 → v09; the expected result is the named criterion applied to the measure it names):**<br>• review example (headache days, all 20 → 14, TTH 10 → 4): responder → non-responder;<br>• only the TTH change shown: responder → not decided;<br>• Box 8, only TTH attacks 6 → 5 shown: non-responder → not decided;<br>• Box 8, TTH 6 → 2, all 12 → 10, migraine 6 → 8: responder → non-responder;<br>• Box 8, migraine-only subject, 6 → 3: responder in both;<br>• Box 8, subject who has migraine and may have TTH, only all-types counts 12 → 6 shown: responder → not decided;<br>• Box 8, chronic migraine and TTH, only `ofType(c1_3)` 6 → 5 shown: non-responder → not decided;<br>• IHS Q6, all-types MSHD 10 → 8, migraine-type MSHD 6 → 2: responder → non-responder.<br>Every v09 result equals the expected one.<br>**Text.** E-045 Meaning and Notes; E-046 Notes ("Every component is evaluated on values of the label's own treatment, of the periods the label refers to and of the headache types its measure refers to"), with the review's example; INV-062 Reading and Notes; INV-063 Reading; row OUT-020.<br>**Scope.** Every changed relation takes output elements only (shown changes, counts, periods and type scopes), the subject's headache types (a context property, section 3.5) and `provides`. |

## Other changes

**1. Sweep for the same kind of defect.** I looked for relations, labels, indicators or comparisons decided on values whose scope (headache type, period, treatment or instrument) is not tied to what the decision is about. Every relation of sections 5 and 6 that fixes a value, category, status or admissibility from other values was listed and checked.
- **Fixed: values attributed to cluster headache.** `concerns` treats an all-types value as one of type t when every type the subject *has* falls under t. A subject who has cluster headache and *may have* migraine (or another type) therefore had:
  - all-types cluster attack rates admitted by INV-089 (definitional), although they count attacks that OUT-029 and INV-028 present under the other type;
  - all-types acute-treatment summaries given the 15-minute time point by INV-073.
  
  Both now use `onlyOfType`, which is strictly stronger than `concerns`. The script table shows that the change concerns only all-types values of a subject who has cluster headache and may have another type: the rate is no longer admitted, and the time point becomes 2 hours. Every other case is unchanged. Changed items:
  - INV-073: Predicate, Reading, Evidence (+OUT-029), new Notes;
  - INV-089: Predicate, Reading, Evidence (+OUT-029), Notes;
  - E-064: Meaning and Notes;
  - rows OUT-023 and OUT-031 (E-012 added; text).
- **Checked, not changed.**
  - **INV-091, INV-092, INV-093 and E-033 `components`** ("for migraine", "for tension-type headache", OUT-037) keep `concerns`. Review 01 judged this reading "defensible", and it errs towards applying the OUT-037 restriction. With `onlyOfType`, an all-types composite index of a subject who has migraine and may have tension-type headache would escape the SHOULD NOT of INV-091, which would narrow OUT-037. The E-012 Notes now state why the two predicates differ.
  - **INV-061 (residual burden).** Its values have the scope of the change they are shown with. Every response comparison shows the all-types changes in headache and migraine days (INV-056), so the person's residual burden is always shown (INV-060). A per-type change gets the residual burden of its own type, which is what makes that change readable.
  - **INV-062, `acuteTreatmentEffectiveness`.** This is a presence requirement, and no relation decides on it: INV-064 does not force "optimal control" from the acute response. So it can force no category.
  - **INV-064 and `levelDays`.**
    - type scope: all types, as [S-010] counts the person's "days with migraine or moderate-to-severe headache";
    - period: monthly, consecutive;
    - treatment: months begin on or after the start of the label's treatment.
  - **INV-045 and INV-046 (medication-overuse indicator).**
    - type scope: the basis is all types (INV-045);
    - period: span and period tied;
    - class: `classShownUsed` and `classUseExcluded` read the class indicators of the same period, whose spans are equal.
  - **Score components (R05-02).**
    - instrument: `r.instrument = s.instrument`;
    - period: the result lies within the last evaluated period;
    - treatment: the treatment start of the label's own comparison;
    - pair: `pretreatmentBaseline`.
  - **Per-view relations.** INV-012, INV-024, INV-030, INV-031, INV-032, INV-033, INV-053 and INV-089 (count relation) relate values of the same view, period and type scope. INV-074 relates the lines of the same summary, drug, period and formulation. INV-082 relates results of the same instrument.
  - **Time points and adherence.** INV-055, INV-058 and INV-059 (rules applicable within their population), INV-066 and INV-067 (adherence window of the same treatment).
  - **Subject conditions.** INV-022, INV-076 and E-053 (`hasType(ctx, c1)`) are conditions on the subject, not on a value's scope.

**2. Satisfiability pass.** It covers every changed or added invariant and attribute, and every invariant that constrains the same elements or views, against INV-001 and the context definitions.
- **INV-063 (definitional).** Its two forcing antecedents stay mutually exclusive: "responder" needs a component met, and "non-responder" needs none met. The changed predicates only add conjuncts to `reductionMet`, `reductionDecided`, `attackReductionMet` and `attackReductionDecided`. So INV-063 forces in fewer cases, and a consistent category exists for any shown values.
- **INV-062 (SHOULD), all-types values of each provided kind.** A value of every `PeriodValueKind` can be shown at `allTypes` for any monthly period, with consistent numbers:
  - day and attack counts (INV-005, INV-006, INV-024, INV-030, INV-031, INV-033);
  - intensity (INV-032);
  - duration (INV-020 annotation, INV-033);
  - symptoms, the most bothersome symptom and caregiver impact;
  - composite indices (INV-091 and INV-092 met by a secondary or exploratory role with components of the same scope);
  - acute-treatment summaries (INV-073 time point by `onlyOfType`, INV-072, INV-074 with 0 attacks).

  No invariant forbids an all-types value of these kinds. INV-089 restricts only cluster attack rates, and INV-012 only completeness indicators; neither is a `PeriodValueKind`. All-types attack counts are available per calendar month or 28-day period wherever provided (INV-108).
- **INV-062, `typeValuesOf`.** Values in the scope `scopeFor` are either all-types values (see above) or `ofType(t)` values. The latter are admissible for every kind:
  - INV-030 (≤ all types) holds with consistent counts;
  - INV-073 sets the time point by `onlyOfType(ofType(t), c3_1)`, that is t ⊑ c3_1;
  - INV-091 and INV-092 can be met.

  The values are required only where the subject has or may have the type (`mayHaveType`).
- **INV-062, changes over all types.** A response comparison can show an all-types change for any provided day measure. Such a change meets:
  - INV-053 and INV-054;
  - INV-056, which admits further changes;
  - INV-097, because a change compares the comparison's own periods, which have equal length for children (INV-055 Notes);
  - INV-060 and INV-061, whose all-types residual burden INV-056 already provides.
- **`where` clause.** The six named criteria have no attack component, so they satisfy it unchanged. Any criterion a reader names can list the kind its attack component needs.
- **INV-073 with INV-088, INV-071, INV-069, INV-104 (all SHOULD).**
  - INV-088 needs, in the cluster view, a 15-minute summary per acute medication. A summary scoped `ofType(c3_1)` satisfies `onlyOfType` and so meets INV-073.
  - INV-071, INV-069 and INV-104 do not constrain the scope.
- **INV-089 with INV-088.** Rates scoped `ofType(c3_1)` are always admissible, and the count relation holds with the attack count of that scope.
- **Derived attributes.** No derived attribute was added or changed, and none is required where its relation is undefined. The attack test keeps its guard `b.count > 0` and has no division.
- **Result.** No admissible context makes the MUST or SHOULD invariants jointly unsatisfiable. No conflict needed fixing.

**3. Bookkeeping.**
- Header "Version: v09 · Iteration: 09 · Status: under review".
- Section 9 "as of v09".
- Section 10: no new source; the new quote is from the Stage 1 source S-035.
- Section 11: iteration 09 paragraph (no web search; downloads listed).
- Section 12: v09 entry.

## Checks

Scripts in the session scratchpad (`fix09/mech.py`, `names.py`, `scope.py`, `newquotes.py`, `scen09.py`) were run on the final OUTPUT_MODEL.md.

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108). None missing, no duplicates, none withdrawn. |
| References | No dangling E- or INV- reference.<br>S references lie within S-001–S-046 and S-101–S-106, and every S-1NN used has a row in section 10.<br>OUT references lie within 001–039.<br>ISS headings are ISS-01–06 and ISS-08–11; ISS-07 occurs only as the withdrawn ID. |
| Realises and traceability | Every element and invariant has exactly one Realises field.<br>39 rows, in Stage 1 order (OUT-039 after OUT-025); all 39 Stage 1 requirements are present.<br>0 differences between the rows and the union of the Realises fields. The new links E-012 → OUT-020, OUT-023 and OUT-031 are in their rows.<br>No coverage text names an ID outside its row.<br>39 × "full". |
| Names and types in `omn` blocks | 325 declared names (v08: 322); the new ones are `onlyOfType`, `scopeFor` and `attackScope`. None is declared twice.<br>218 enumeration constants and variant tags (v08: 217; new `typeValuesOf`), with no clash with declared names.<br>Every attribute selection is declared on some type; `headacheType` is now also a component of `AttackReductionComponent`.<br>The set of remaining undeclared identifiers equals v08's: all are bound variables or parameters.<br>Every type used in the new text is declared: `OutputContext`, `TypeScope`, `ICHD3Code`, `HeadacheType`, `PeriodValueKind`, `AttackReductionComponent`, `PeriodValue`, `AttackCount`. |
| Typing rule for levels | 172 level-annotated attribute declarations, as in v08; 0 violations. |
| Conformance levels | MUST 19, MUST NOT 2, SHOULD 47, SHOULD NOT 8, definitional 32, all unchanged.<br>No invariant changed level or scope. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. |
| Unchanged values | The 17 rule constants of E-041, the 6 criterion constants of E-045 and `levelDays` are byte-identical to v08. |
| Quotes | 16 new quoted strings: 12 found verbatim in the downloaded sources, 2 Stage 1 text, 1 translation, 1 model term. The new [S-035] quote (section 3.3 b) is on PDF p. 23. |
| Scope sweep (enter, entry, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, reminder, field, obtained, calculated, computed, algorithm, "diary information", "diary data") | 85 occurrences, as in v08. The only differences are the shifted context of the section heading "Change log". In the changed lines the single hit is an unchanged E-064 sentence ("the rate rests on the attacks that the summarised diary information shows"). All occurrences are exclusion statements, out-of-scope notes, Stage 1 wording or quotes, as review 09 confirmed for v08.<br>No input entity, storage term or derivation from input was added. The new relations take shown values, their type scopes, the subject's headache types and `provides`. |
| Satisfiability | See Other changes 2: no conflict. Scenario script: all 13 label scenarios and all 8 cluster cases behave as stated. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v09.md`: identical. |
| Files written | Only OUTPUT_MODEL.md, history/v09.md and this fix log. Nothing under docs/stage1-output-requirements/ was changed, and nothing was committed or pushed. |
