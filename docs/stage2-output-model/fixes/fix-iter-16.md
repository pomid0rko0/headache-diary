# Fix log — iteration 16
Input review: reviews/review-iter-16.md · Input version: v15 · Output version: v16
Date: 2026-10-21

## What was read and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039);
- v15 (`OUTPUT_MODEL.md`, byte-identical to `history/v15.md`, checked with `cmp`);
- review 16.

**Earlier loop files read, so that no fix is undone:**
- fix log 15 and review 15 (R15-01 `summarisesMedication`, R15-03 `courseOverlaps`, "Other changes" item 1 on the drug of the overview's acute summary);
- fix log 14 (R14-02 (d), the `within` period tie of the acute alternative);
- fix log 11 ("treatment effect" by one item);
- the oscillation check after iteration 12, with its seven watch points.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**Downloads.** None. The remark concerns the formal model. I verified it against the Stage 1 v18 text in the repository (OUT-014, OUT-023, OUT-024, OUT-035 and its [S-027] quote) and against v15. No source quote was added or changed, and the new text quotes no source.

**Scripts.** All are in the session scratchpad (`fix16/`) and were run with `python3 -I`:
- `inst16.py`: the INV-105 treatment-effect conjunct in its v15 and v16 forms, `courseOverlaps` and `courseNotOutside`, on the review's examples, on edge cases and on 20 000 random admissible contexts;
- `mech16.py`: headings, references, traceability, invariant levels and scopes, prohibition form, attribute declarations and the typing rule, declarations and uses of predicates, bracket balance, and the list of items changed from v15;
- `types16.py`: every capitalised name used in an `omn` block is a declared type, constant or bound variable;
- `scope16.py`: scope-term counts in v15 and v16, and the hits on changed lines.

### Verification of the remark

**R16-01 holds.**
- **The defect.** In v15 the acute alternative of the INV-105 treatment effect is `∃ s ∈ v.content ∩ AcuteTreatmentSummary; m ∈ ctx.subject.acuteMedications • s.typeScope = allTypes ∧ summarisesMedication(s, m) ∧ within(s.period, v.covers)`, and the acute part of the antecedent is `ctx.subject.acuteMedications ≠ ∅`. By E-008, `acuteMedications` holds every acute medication used up to the as-of date, including those no longer used. So:
  - (i) a 0-attack summary of a medication last taken years before the covered period meets the conjunct;
  - (ii) a subject with no treatment in the covered period, but with past acute use, is asked for a treatment effect of that period.
- **Stage 1.** OUT-035 asks for the treatment effect "so that patients can follow the effect of their treatment"; its [S-027] quote speaks of monitoring "the effect of acute and possibly preventive treatment". The model already reads this as the effect of the treatment the patient follows during the covered period (E-067 Notes; INV-105 Notes since v14 and v15), and v15 applied that reading to the preventive alternative and to the preventive part of the antecedent only.
- **The review's examples** (`inst16.py`):
  - (i) overview of 1 August – 30 September 2026, with only a 0-attack ibuprofen summary (ibuprofen course stopped 31 December 2018): v15 holds, v16 fails;
  - the same overview with a sumatriptan summary (course from 10 January 2025, ongoing), or with the erenumab comparison (from 15 March 2026): both hold under v16;
  - (ii) the overview of 2019 with no treatment-effect item: v15 fails (it asks for one), v16 holds (nothing is asked).

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R16-01 | fixed: the review's option (a), with the variant for a course without a stated start that the review leaves to the fixer | E-067 (Definition: new `courseNotOutside`; Meaning; Notes); INV-105 (Predicate, Reading, Notes); E-051 Conformance; row OUT-035 | **New predicate** (E-067, next to `courseOverlaps`): `courseNotOutside(c, t, p) ≙ (∀ s ∈ startOf(c, t) • s ≤ p.end) ∧ ¬ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is stop ∧ e.date < p.start`. It reads: the context does not place the course outside p, because it has not started after p's last day and has not stopped or been paused before p's first day. For a course with a stated start it equals `courseOverlaps` (a course has at most one start, INV-001); a course without a stated start counts as started.<br>**INV-105 acute alternative:** `… ∧ within(s.period, v.covers) ∧ ∃ t ∈ ctx.subject.acuteTreatments • drugOf(t) = m.drug ∧ courseNotOutside(ctx, t, s.period)`. The summary's drug is that of an acute treatment course taken during the summary's own period.<br>**Why the summary's period, not only the covered period.** The review's formula ties the course to `v.covers`. A summary may be of a period within the covered period (`within`, v14), for example September of an August–September overview, when the course stopped on 15 August. Tying the course to `s.period` closes that case too. It implies the review's tie, because `courseNotOutside(c, t, q) ∧ within(q, p) ⇒ courseNotOutside(c, t, p)` (checked by `inst16.py`). It costs no satisfiability, because a summary of the covered period itself can always be chosen.<br>**INV-105 antecedent:** `ctx.subject.acuteMedications ≠ ∅` is replaced by `(∃ t ∈ ctx.subject.acuteTreatments • courseNotOutside(ctx, t, v.covers))`. It is parenthesised, so that the quantifier does not take in the implication. The preventive part is unchanged.<br>**Courses without a stated start count (the fixer's choice).** The review leaves it open whether an acute course with no stated start (E-055, INV-109 Notes) should count. I count it, and exclude it only where the context states a stop before the period:<br>• the effect of a preventive treatment is a response comparison aligned to its start (INV-056), so `courseOverlaps` needs a start; an acute-treatment summary of a period needs none;<br>• the model already keeps the requirement for an acute course without a stated start, leaving only its period free (INV-109 Notes); dropping the overview's treatment effect for such a course would narrow OUT-035 where the remark asks for nothing;<br>• a course without a stop event is ongoing up to the as-of date in the model (E-055 `duration`, INV-079), so a course that has neither a stated start nor a stated stop is not placed outside any period;<br>• both review examples are decided as the review asks under either choice.<br>**Formulation.** `summarisesMedication` is kept (v15). Which formulations were taken during a period is stated neither by the context, whose courses are courses of a drug (`drugOf`, E-008), nor by the acute-medication days, which OUT-014 gives by class and by drug. So a summary of all formulations of the course's drug covers every formulation taken in its period, and a single-formulation summary is one of a formulation of that drug that the subject has used. This is stated in the INV-105 Notes. I considered and rejected `s.formulationScope = allFormulations ∨ s.treatedAttacks > 0`. It would exclude a 0-attack summary of the formulation the patient follows, which no output element can tell apart from that of another formulation, and in that case it would decide the reading of OUT-023 that fix 15 left open.<br>**Aligned text:**<br>• INV-105 Reading and Notes: the acute alternative, the acute part of the antecedent, the reason for counting undated acute courses, the formulation limit, and the satisfiability sentence;<br>• E-067 Meaning (`courseNotOutside`) and Notes;<br>• E-051 Conformance (the INV-105 clause);<br>• row OUT-035.<br>**Kept, as the review asks:**<br>• one treatment-effect item suffices (fix 11);<br>• the `within` period tie (v14);<br>• `summarisesMedication` and `courseOverlaps` (v15; `courseOverlaps` is byte-identical);<br>• the type scope `allTypes` (v13);<br>• the menstruation conjunct and the R05-01 series conjunct (byte-identical);<br>• E-008 (byte-identical). |

## Identifying-property check of INV-105

I read INV-105 as a whole and checked that every item it requires is tied to the subject, treatment, drug and formulation, headache-type scope and period that Stage 1 OUT-035 implies. Abbreviations: **S** subject, **T** headache-type scope, **P** period, **Tr** treatment or course, **D** drug, **F** formulation, **K** measure, **V** view. "Not fixed by Stage 1" names a property that Stage 1 leaves free, so it is not a gap.

| Required item | Properties and how they are tied | Gap after v16 |
|---|---|---|
| Plain-language quality | `plainLanguage ∈ v.qualities` | n |
| Headache days, migraine days, total acute-medication days of the covered period | S (`ctx`), K, P (`v.covers`), T (`allTypes`), V (`shownDay`). Migraine days without the OUT-005 condition: ISS-03. Acute-medication use is the total: OUT-035 names "acute medication use" only (not fixed by Stage 1 per class or drug) | n |
| Intensity of the covered period | K, P, T, V; scale SHOULD on every intensity summary (E-023 attribute level) | n |
| Time course | series of all whole periods of one granularity within the covered period (`fillsPeriod`), the four measures for each of its periods, `allTypes`, V. Granularity: not fixed by Stage 1 (R05-01, unchanged) | n |
| Treatment effect, antecedent | S; Tr: a preventive course that overlaps the covered period (`courseOverlaps`, v15), or an acute course that the context does not place outside it (`courseNotOutside`, **v16**); P: the covered period | n (was **y** for the acute part) |
| Treatment effect, response comparison | Tr: a preventive treatment taken during the covered period (`courseOverlaps`; `rc.treatment` a preventive treatment of the subject, INV-056); K and T: monthly headache and migraine days over all types (INV-056, INV-057); V: values, changes and time points in the overview (INV-003, INV-054, INV-059), adherence next to it (INV-066). The comparison's own periods: not fixed by Stage 1 (settled in R15-03 and fix 15; review 16 "checked and not raised") | n |
| Treatment effect, acute-treatment summary | T: `allTypes` (v13); P: the covered period or a period within it (`within`, v14); D: the drug of an acute medication the subject has used (`summarisesMedication`, v15); **Tr: that drug is the drug of an acute course not placed outside the summary's own period (`courseNotOutside`, v16), and so not outside the covered period either**; F: all formulations of that drug, or one formulation of it that the subject has used (`summarisesMedication`). A per-period formulation is neither a context property (courses are courses of a drug) nor an output element (OUT-014 days by class and drug), so it cannot be tied more finely without a new subject property; E-008 stays unchanged (watch point 6). Early time point: INV-073. Outcomes and lines in the overview: INV-072 | n (was **y** for Tr) |
| Cycle line | overlaps the covered period, where the subject menstruates during it (`menstruatesDuring`); lead-in and window by INV-087. Unchanged | n |

**Result.** The only open properties were the acute course of the acute alternative and the acute part of the antecedent, both history-wide in v15. v16 ties both. Every other property is fixed as far as Stage 1 fixes it, or is a settled point.

**Same defect elsewhere.** I searched for every other use of the history-wide sets `acuteMedications` and `acuteTreatments` that one item could discharge (`grep` for `acuteMedications ≠ ∅`, `∃ m ∈ … acuteMedications`, `acuteTreatments ≠ ∅`). There is none. The other uses (E-045 `valueAvailable` with INV-062, E-062 `acute` with INV-088, INV-071, INV-104, INV-109, INV-046) are universal requirements for each medication. For a medication not used in the period they ask for a 0-attack summary or 0 days, which E-008 states as correct values (watch point 6). So no other item was changed.

## Other changes

None besides the housekeeping:
- header (v16, iteration 16);
- section 9 ("as of v16");
- section 11 (iteration 16 entry: no web search, no download, no new source);
- section 12 (v16 entry).

No element or invariant was added, withdrawn or renumbered, no level changed, and no source was added.

### Satisfiability pass

The changed invariant (INV-105) and the new predicate (`courseNotOutside`) were checked together with the invariants that constrain the same elements and views:
- the overview view: INV-003, INV-008, INV-011, INV-087, INV-095, INV-098, INV-099, INV-101, INV-106, INV-107;
- the response comparison: INV-054 to INV-061, INV-066, INV-067, INV-097;
- the acute-treatment summary: INV-072 to INV-076;
- the context: INV-001.

Results:
- **No admissible context makes the MUST and SHOULD constraints jointly unsatisfiable.** The cases are:
  - **A preventive course overlaps the covered period.** A response comparison of it can be shown in the overview, as in v15: 28-day baseline and on-treatment periods meet INV-055 to INV-057, INV-059 and, for children, INV-097, with adherence (INV-066, INV-067), residual burden (INV-060, INV-061), completeness and labels.
  - **Otherwise, an acute course t is not placed outside the covered period.** INV-001 gives an acute medication m with `m.drug = drugOf(t)`. A summary of all formulations of that drug, of the covered period, with type scope `allTypes`, then meets the acute alternative:
    - INV-003 already shows the covered-period atom in the overview, and INV-011 asks for its completeness;
    - INV-072 asks it to name every formulation of the drug that the subject has used, which it can;
    - INV-073 fixes its time point by its type scope;
    - INV-074 holds with any number of lines equal to its treated attacks, 0 included;
    - `courseNotOutside(ctx, t, s.period)` holds because `s.period = v.covers`.
  - **Neither holds.** Nothing is required.

  `inst16.py` built this witness on 20 000 random contexts that satisfy the INV-001 link. In the 15 012 contexts where the v16 antecedent holds, the witness met the conjunct.
- **v16 narrows nothing that v15 required outside the remark.** Under the INV-001 link, the v16 antecedent implies the v15 antecedent, and the v16 consequent implies the v15 consequent. Both were checked on the same random contexts. So v16 removes exactly the requirement of case (ii) and the items of case (i).
- **Definedness.** No derived attribute was added or changed. `courseNotOutside` uses `startOf` (a set), `courseEvents` and the MUST attributes `start` and `end` of a period. `s.period` is a core reference. `drugOf` is total. No partial term is used.
- **Level.** INV-105 stays SHOULD, the strength of OUT-035.

### Watch points (oscillation/check-after-iter-12.md)

1. **E-041.** Byte-identical. No `excludes`, `timing`, `ages` or `AgeCoverage` value touched.
2. **Responder labels.** E-012, E-045, E-046, INV-062 and INV-063 are byte-identical.
3. **Co-presence.** INV-003, INV-054, INV-056, INV-078 and E-040 are byte-identical.
4. **Menstrual-relation view and overview.** INV-086, INV-087, E-060 and E-061 are byte-identical. The INV-105 menstruation conjunct is byte-identical (`diff`).
5. **Withdrawal follow-up.** INV-049, INV-050 and E-039 are byte-identical.
6. **E-008.** Byte-identical. `courseNotOutside` is declared in E-067, as `courseOverlaps` is, and uses `startOf` and `courseEvents` as they are.
7. **Change volume.** This version changes:
   - 3 model items (E-051, E-067, INV-105);
   - 1 traceability row (OUT-035);
   - the header and sections 9, 11 and 12.

   That is **3 model items** (4 counting the row). Every change ties the acute treatment-effect item more closely to the covered period or restricts the antecedent to it. No earlier tie is removed.

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-11; ISS-07 appears only as withdrawn (section 9). |
| References | No dangling E- or INV- reference; ISS-07 is referenced only as withdrawn. S references lie in S-001–S-046 and S-101–S-106, and every S-1NN has a row in section 10. Every OUT reference exists in Stage 1 (39 requirements). |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". Exactly one Realises and one Conformance field in every element and invariant. Each row's E and INV columns equal the union of the Realises fields. No Realises field changed. |
| Types and names | Every capitalised name in the `omn` blocks is a declared type, constant or bound variable; the only others are the level keywords MUST, SHOULD and MAY (`types16.py`, same as v15). No predicate or function is declared twice. `courseNotOutside` is declared once (E-067) and occurs 4 times in `omn` blocks (its comment line, its declaration, and two uses in INV-105: the antecedent and the acute alternative). The only applied names without a `pred` or `fun` declaration are `refs` (section 2.5) and the sequence application `s(i)`, as in v15. Every `omn` block has balanced brackets.<br>**Argument types:**<br>• `t` ranges over `ctx.subject.acuteTreatments : set Treatment`;<br>• `s.period` and `v.covers` are `→Period`, matching `p : Period` (section 2.10);<br>• `drugOf(t) : Drug` = `m.drug : Drug`.<br>**Precedence in INV-105:** `(∃ t • courseOverlaps(…)) ∨ (∃ t • courseNotOutside(…)) ⇒ (∃ rc • …) ∨ ∃ s; m • … ∧ within(…) ∧ ∃ t • drugOf(t) = m.drug ∧ courseNotOutside(ctx, t, s.period)`, closed by the outer parenthesis before `∧ (menstruatesDuring …)`. No new partial term. |
| Typing rule for levels | Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33; total 110, unchanged. Scopes: output 77, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Changed items (script, v15 → v16) | E-051, E-067 and INV-105; row OUT-035. Plus the header and sections 9, 11 and 12. |
| Guarantee terms (v15 → v16) | All equal:<br>• `within(s.period, v.covers)` 1;<br>• `s.typeScope = allTypes` 9;<br>• `summarisesMedication(s, m)` 9;<br>• `courseOverlaps(ctx, rc.treatment, v.covers)` 1;<br>• `courseOverlaps(ctx, t, v.covers)` 1;<br>• `menstruatesDuring` 9;<br>• `fillsPeriod` 15;<br>• `containsPeriodOf` 12;<br>• `#L.evaluated = 1` 7;<br>• `rc.treatment = L.treatment` 13;<br>• `adherenceFor(` 7;<br>• `scopeFor(` 8;<br>• `conditionHolds(` 10;<br>• `dayOneShown` 9;<br>• `ruleRuChildren` 6;<br>• `otherCompletenessExpression` 3;<br>• `withinWindow` 9;<br>• `s.period = v.covers` 2. |
| Instance check (`inst16.py`) | **The review's examples:**<br>• (i) the ibuprofen-only overview: v15 holds, v16 fails;<br>• the sumatriptan summary and the erenumab comparison hold under v16;<br>• (ii) the 2019 overview without a treatment-effect item: v15 fails, v16 holds.<br>**Sub-period case.** A September summary, with the course stopped on 15 August, fails under v16; an August summary holds.<br>**Undated courses.**<br>• A course without a stated start or stop still requires the treatment effect, and a summary of its drug meets it.<br>• A course without a stated start that stopped before the period requires nothing.<br>**Boundaries:**<br>• a course starting on the period's last day, or stopping on its first day, is not outside it;<br>• one starting the day after, or stopping the day before, is outside it;<br>• `courseOverlaps` gives the same results for these dated courses.<br>**Random contexts (20 000).** The antecedent narrows and the consequent strengthens. The satisfiability witness holds. `courseNotOutside` is monotone under `within` and equals `courseOverlaps` for a course with a stated start. |
| Quotes | No new source quote, and no source quote changed. The new text cites Stage 1 requirements by ID only. |
| Scope sweep | **Terms searched** in the whole document: enter, entry, record, input, captur, logged, store/storage, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field, questionnaire, data-entry, "derived from", "diary information", intake and "decision logic".<br>**Counts.** Every count equals v15.<br>**Hits on changed lines.** The only one is the unchanged lead-in sentence of the INV-105 Notes ("the diary information gives no first day").<br>**Other occurrences.** All are legitimate and were present in v15:<br>• the scope statements of sections 1, 2.1, 2.7 and 3.5;<br>• the "obtained from diary information; how is out of scope" notes of E-014 and E-019, and the E-033 note that the formula of an index is out of scope;<br>• the [S-014] HALT-30 quote ("records days affected") and the [S-007] quote ("persistent high attack frequency");<br>• E-057 and E-059, which state that scoring from answers is out of scope and omit from quotes the words on how scores are obtained;<br>• the INV-076 note (assigning attack lines to headache types would be a derivation from input);<br>• the INV-014 Reading ("can be answered with headache days");<br>• the document's "Realises" and "Conformance" fields;<br>• the change log ("ISS-04 records it", "computed field");<br>• the search log's Europe PMC full-text XML;<br>• "diary information" (30), what the outputs summarise and how completely a period is covered by it, in the wording of OUT-003 and OUT-038;<br>• "intake" (20): the [S-001] and [S-010] quotes, the timing of intake shown for each treated attack (OUT-023), and the "inconsistent intake" of OUT-039.<br>**New relation.** `courseNotOutside` takes only context properties (course events) and output periods as arguments, like `courseOverlaps`. It adds no input entity, no storage term and no relation with an input argument. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v16.md`: identical. `history/v15.md` is unchanged. |
