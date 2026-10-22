# Fix — iteration 40
Version produced: v40
Reviewed version: v39
Date: 2026-10-22

Input: [`reviews/review-iter-40.md`](../reviews/review-iter-40.md) (verdict REMARKS, one remark: R40-01). Every comparison uses the committed v39 as its baseline (`git show HEAD:docs/stage2-output-model/OUTPUT_MODEL.md` and `…/RATIONALE.md`).

Files written:
- `OUTPUT_MODEL.md` (v40, 431,035 bytes): header `Version: v40 · Iteration: 40 · Status: under review`; the Readings of INV-061 and INV-075; one change-log entry. The `Companion:` line stays `RATIONALE.md v39`, because `RATIONALE.md` did not change (as in v37).
- `history/v40.md` and `history/v40-rationale.md`: byte-identical copies of `OUTPUT_MODEL.md` and `RATIONALE.md` (332,923 bytes, unchanged, header v39).
- this log.

No web search, no download and no new source.

Scripts (all run with `python3 -I`) are outside the repository, in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix40/`:
- `witness.py`: the R40-01 counter-examples against the predicates as written, the v39 and v40 Readings, the reviewer's two alternatives, and an exhaustive comparison of each v40 Reading with its predicate;
- `reading_text.py`: ties the witness to the v40 file (predicates byte-identical, v39 phrases gone, encoded clauses present);
- `inv063_scope.py`: the INV-063 check of the class sweep (section 4);
- `extract.py`, `readings_pass.py`, `meaning_hits.py`, `conf_levels.py`: the sweep of invariant Readings, element Meanings and Conformance fields;
- `check40.py`: the general checks (section 6).

Outputs: `witness.out`, `readings_pass.txt`, `meaning_hits.txt`, `checks-v40.txt`.

## 1. Summary

| Part | Verified | Disposition | Places changed |
|---|---|---|---|
| R40-01 (a): the INV-061 Reading says the residual burden shows its two counts "for one calendar month or 28-day period"; the predicate checks each count separately | yes, by script | fixed: Reading reworded (the review's preferred option). The predicate is unchanged: neither OUT-019 nor E-044 requires the two counts to share a month | INV-061 Reading |
| R40-01 (b): the INV-075 Reading says a line "lists adverse events only when it shows a drug-related adverse event"; the predicate excludes adverse events only where the line shows that none occurred | yes, by script | fixed: Reading reworded (the review's preferred option). The predicate is unchanged: neither OUT-023 nor E-053 makes listing an adverse event depend on a shown result | INV-075 Reading |

**Class sweep.** The class is prose that claims a guarantee the predicate does not give. It has no member besides the two Readings of the remark. I checked:
- the invariant Readings, by a targeted pass that confirms the review's count;
- every element Meaning and Conformance field;
- the catalogue and traceability cells and Stage 1 issues about the residual burden and attack lines;
- every `RATIONALE.md` entry that restates the INV-061 or INV-075 relation.

**Formal text.** No `omn` block changed: 160 of 160 are byte-identical to v39. The 191 table rows with code cells (catalogue, case tables, source data tables) are byte-identical too. No level, Realises field, catalogue row, traceability row, Stage 1 issue or quote changed.

## 2. R40-01 (a): INV-061

### Verification

`witness.py` transcribes the INV-061 predicate as written. A change compares 1 October – 29 December 2025 with 1 January – 31 March 2026. Both are 90-day periods of kind `otherSpan`, for example the selected periods of an OUT-001 comparison. Results:
- **Counter-example: admitted.** The residual burden shows the migraine days of January (calendar month) and the moderate/severe headache days of March (calendar month). INV-061 holds, and the v39 Reading ("for one calendar month or 28-day period") is false.
- **Same month for both counts:** admitted, and the v39 Reading holds.
- **Monthly compared period (May 2026):** both counts must be of the compared period atom itself. A count of another May atom is rejected.

INV-060 (SHOULD) asks for a residual burden next to every percentage change in migraine or headache days whose compared period has at least 28 days. That includes changes outside response comparisons, whose compared period need not be monthly. So the case is reachable. In every response comparison the compared period is monthly (INV-056), so there the two counts are of one period and the v39 Reading held.

### Decision: reword the Reading; keep the predicate

The predicate has no gap. What the v39 Reading adds, one month shared by both counts, is required neither by Stage 1 nor by the element's definition.
- **Stage 1 OUT-019**, Statement (SHOULD): "Wherever the output shows a relative (percentage) change in migraine or headache days, it SHOULD show next to it the absolute number of migraine days and moderate/severe headache days per month that remain on treatment."
  - "Per month" gives the unit of the two absolute numbers. The Statement does not say that they are of one and the same month, or which month within a longer compared period they are of.
  - OUT-019 has no Caveat. Its Rationale ("A large percentage reduction can leave a substantial number of disabling days") is met by each count on its own.
- **E-044 (ResidualBurden)** declares two separate references, `migraineDays : →DayCount core -- migraine days per month that remain on treatment` and `moderateSevereHeadacheDays : →DayCount core -- moderate/severe headache days per month that remain on treatment`. Each has its own period, and the element has no period of its own. Its Meaning ("the absolute numbers of migraine days and of moderate/severe headache days per month that remain on treatment") does not say "of one month" either.
- **E-040 (Change)**, which the burden refers to, defines the reference and compared values only. It says nothing about the month of a residual count.
- **Section 3.3, item 5.** A definitional invariant "excludes only outputs that show a value contradicting the definition of the element". January's migraine days and March's moderate/severe headache days, within a compared period of January to March, are two true counts per month. Nothing in them contradicts E-044.
  - The reviewer's alternative, `sameSpan(rb.migraineDays.period, spanOf(rb.moderateSevereHeadacheDays.period))`, would exclude such an output, which Stage 1 permits. That narrows OUT-019 (PROCESS.md section 4).
  - Being definitional, it would also bind MUST-conformance (section 3.2) for content that Stage 1 asks at SHOULD.
- **No SHOULD tie either.** No Stage 1 statement part asks for one month at any level.
- **History.** Fix 01 (R01-03) kept "a monthly period within the compared period" for changes outside response comparisons and left the choice of month open. For shorter compared periods, ISS-13 asks the human "which month the residual burden then refers to". Fixing the month shared by the two counts would answer part of that open design question without a Stage 1 basis.

**Watch point 1** (CHG-03 / ISS-13): not touched. The INV-060 predicate, with its antecedent `ch.compared.period.lengthDays ≥ shortestMonthlyDays`, and the INV-061 predicate are byte-identical. No per-month residual is added for shorter compared periods.

### What changed

INV-061 Reading only. v39:

> The residual burden shows migraine days and moderate/severe headache days, with the scope of the change, for one calendar month or 28-day period: the compared on-treatment period itself when that is a calendar month or 28-day period (as in every response comparison, INV-056), and otherwise one such period within the compared period.

v40:

> The residual burden shows migraine days and moderate/severe headache days, with the scope of the change, each count for a calendar month or 28-day period within the compared period of the change: for the compared period itself when that is a calendar month or 28-day period (as in every response comparison, INV-056), and otherwise for a calendar month or 28-day period within it, which may differ between the two counts.

**The "on-treatment" wording.** The v39 Reading also called the compared period "on-treatment", and the predicate does not say that. INV-060 also asks for a residual burden next to changes outside response comparisons, for example in the post-stop monitoring view (E-049), whose compared periods follow a stop.
- Review 11 settled that "per month that remain on treatment" is read on the compared period. The v40 Reading states that reading: "the compared period of the change".
- The heading ("Residual burden refers to a monthly on-treatment period") keeps OUT-019's words and the indefinite article. It is a name, so it is unchanged.

## 3. R40-01 (b): INV-075

### Verification

`witness.py` transcribes the INV-075 predicate as written:
- **Counter-example: admitted.** The line shows `(painFreedom(twoHours), true)` and `(relapse, false)` but no result for `drugRelatedAdverseEvent`, and lists one adverse event. INV-075 holds. The v39 clause "it lists adverse events only when it shows a drug-related adverse event", read on the line's results, is false.
- **Control: rejected.** The same line, also showing `(drugRelatedAdverseEvent, false)`.

At the definitional and MUST levels nothing else closes the gap:
- E-053 `adverseEvents … SHOULD when AttackOutcomeResult(measure ↦ drugRelatedAdverseEvent, achieved ↦ true) ∈ self.results` constrains presence only.
- INV-072, which asks every line of a summary's sequence to show every required outcome, is SHOULD.

### Decision: reword the Reading; keep the predicate

The predicate has no gap. What the v39 Reading adds is not part of the definition of the element.
- **Stage 1 OUT-023**, Statement (SHOULD): "the output SHOULD also report, for the same attacks, […] drug-related adverse events after intake and whether the patient regarded them as meaningful (adverse effects per treatment are also listed in OUT-024)".
  - The Statement asks for the adverse events and the patient's view of them. It does not make the listing of an adverse event depend on a shown outcome result.
  - The Caveats concern the definition of response (pain freedom against headache relief), not adverse events.
- **E-053 (TreatedAttackLine)** declares `results : set AttackOutcomeResult core`, so a line may show any subset of the outcome results. Its Meaning describes "any drug-related adverse events and whether the patient regarded them as meaningful".
  - A line that lists an adverse event and shows no result for `drugRelatedAdverseEvent` states that a drug-related adverse event occurred, and states nothing else about that outcome.
  - So it shows no value that contradicts the definition (section 3.3, item 5).
- **The reviewer's alternative** is `l.adverseEvents ≠ ∅ ⇒ AttackOutcomeResult(measure ↦ drugRelatedAdverseEvent, achieved ↦ true) ∈ l.results`.
  - It requires a result to be shown whenever adverse events are listed, which is a presence requirement.
  - A definitional invariant "cannot make an element more or less required" (section 3.3, item 5). The audit found the same defect in INV-031 (CA-02), and v35 removed that conjunct (CHG-04).
  - It would also exclude lines that no Stage 1 part forbids; the review notes this.
- **At SHOULD the content is already asked for.** INV-072 asks every line of a summary's sequence to show a result for every required outcome, `drugRelatedAdverseEvent` included. With INV-075's first and third conjuncts, a line of a fully conformant summary that lists an adverse event therefore shows `(drugRelatedAdverseEvent, true)`.
  - This consequence is recorded here only. The Reading states its own predicate (PROCESS.md section 6a).

### What changed

INV-075 Reading only. v39:

> A treated-attack line shows each outcome once and the status of each associated symptom once; it lists adverse events only when it shows a drug-related adverse event; a meaningful adverse event is a drug-related adverse event; and an adverse event the patient regarded as meaningful is not contradicted by the line's results.

v40:

> A treated-attack line shows at most one result for each outcome measure and at most one status for each associated symptom. Where it shows that no drug-related adverse event occurred, it lists no adverse event. Where it shows that the patient regarded a drug-related adverse event as meaningful, it also shows that a drug-related adverse event occurred. Where it lists an adverse event that the patient regarded as meaningful, it does not show that the patient regarded no drug-related adverse event as meaningful.

I rewrote the Reading clause by clause, so that each clause states one conjunct in the line's own terms (results, listed adverse events):
- **Clause 2** is the R40-01 correction.
- **Clause 1:** "shows each outcome once" could be read as "shows every outcome". INV-072 asks that at SHOULD; INV-075 does not. It now says "at most one".
- **Clause 3:** "a meaningful adverse event is a drug-related adverse event" was vacuous if read on the listed items, which are drug-related by E-053. It now states the results relation of the fourth conjunct.
- **Clause 4:** "is not contradicted by the line's results" now names the result that the fifth conjunct excludes.
- Clauses 1, 3 and 4 claim nothing more or less than before.

## 4. Class sweep

**The class.** Prose that restates the relation of a predicate or definition and claims a guarantee the predicate does not give: a different quantifier, a value shared where the predicate has separate ones, the converse, or a stronger condition (PROCESS.md sections 6a and 9, "Prose overclaim").

**Invariant Readings.** The review read all 87, and the review asks the fix to confirm. I made a targeted pass over the phrases that carry the two defects: "only when", "only if", "only where", "one … period", "one month", "same period", "same month", "for one". `readings_pass.py` (output `readings_pass.txt`) found 17 sentences in 14 invariants. Apart from INV-061 and INV-075, each agrees with its predicate:
- **INV-006, INV-024, INV-031, INV-032, INV-089, INV-122:** "the same period" is defined as "periods with the same dates", as `daysOf` and `sameSpan` state.
- **INV-069, INV-093:** "the same period(s)" are the same period atoms (`m.period = p`, `shownDay`).
- **INV-046:** "reached only if" matches the first conjunct.
- **INV-073:** "one of cluster headache only when" matches `onlyOfType`.
- **INV-074:** "only where the outcome is shown for at least one attack" matches `os.attacksAssessed > 0`.
- **INV-063:** I checked this one in detail. "A reduction or attack-reduction component is decided only for a label that refers to one on-treatment period" is not a member.
  - The sentence before it ("Each component counts only where the label's treatment meets its condition") scopes it.
  - A component whose condition fails is never met and is always decided (`reductionDecided`, `attackReductionDecided`, `scoreDecided`, E-046). So it changes neither of INV-063's two conclusions, as review 02 noted.
  - `inv063_scope.py` compares the categories that the predicate forces with those of the Reading, over counting components only. They agree for all 259 criteria of up to three abstract components.

**Element Meanings (67).** `meaning_hits.py` lists the 85 Meaning sentences that contain relational words (one, only, same, exactly, at most, never, every, each, all, next to, together, an INV-ID). I read every Meaning in full. Each Meaning sentence that restates the relation of a definitional invariant, a placement marker or the element's own defined predicates agrees with the formal text:
- E-011 and INV-111; E-012 `scopeFor` ("exactly one scope"); E-014 `daysOf` and INV-006 ("at most one member");
- E-016, E-017 and E-019 with INV-111; E-023 `onSameScale`; E-025 `inSameForm`;
- E-032 with INV-045: code and level are attributes of the indicator, and its span and basis are placed in its view by INV-003 through the shared period atoms;
- E-040 and INV-053 (a zero reference); E-045 and INV-063 ("met when any one of its components is met");
- E-046: `evaluationResult`, `pretreatmentBaseline`, `attackScope`, `evaluatedOnTreatment`;
- E-047 `adherenceFor`; E-049 `firstChangedDay` ("one member for these kinds of event"); E-051 `summarisesMedication`; E-052 and INV-074; E-056 and INV-080 with its W2 markers;
- E-061 and INV-087; E-064 and INV-089; E-067 `courseOverlaps` and `courseNotOutside`.

The two elements of the remark state neither relation:
- **E-044:** "the absolute numbers of migraine days and of moderate/severe headache days per month that remain on treatment" claims no shared month.
- **E-053:** "any drug-related adverse events and whether the patient regarded them as meaningful" claims no "only when".

I also read the E-060 lead-in Meaning (settled, checks 04 and 12) and the E-063 remission Meaning (CA-06, settled), and did not re-examine them. They state no relation of this kind.

**Outside the class: role descriptions.** Some Meanings describe an element in the presentation that Stage 1 asks for, and the element's own Conformance field names the item and level that ask for it. Examples:
- E-013: "shown next to the summary measures of that period", with INV-011 SHOULD;
- E-042: "shown with the response comparison", with INV-059 MUST (E-043 `timePoints`, W2 MUST);
- E-044: "Next to a percentage change in migraine or headache days", with INV-060 SHOULD;
- E-046: "It is shown with the criterion it applies, the values it rests on, and the residual burden", with INV-062 and W2 SHOULD;
- E-047: "shown next to the response comparison", with INV-066 SHOULD;
- E-059: "shown next to the headache outputs", with INV-083 SHOULD.

These state what the element is for. They do not restate a predicate with a different relation. Each matches the content of the item its Conformance field names, at the level that field states, so they are not in the class and I did not change them. Rewording all of them would be a sweep of a different, adjacent class, which watch points 12 and 13 of the check after iteration 36 caution against.

**Element Conformance fields.** `conf_levels.py` checked the 187 invariant references in the 67 element Conformance fields. Wherever a field states a level next to an invariant, it is that invariant's level, and every invariant in a "Definitional:" list is definitional. Ten references stand in clauses without a level. Nine are index phrases ("used by …", "also asked for by …"). The tenth (E-011, "`reports`; INV-008") follows the level SHOULD stated earlier in its sentence, which is INV-008's level. The seven index asymmetries that review 40 lists under "Checked and not raised" are unchanged and state no level.

**Catalogue, traceability and Stage 1 issues.**
- **OC-22, Period cell:** "a calendar month or 28-day period within the compared period" names the kind of period, as the OC-17 cell does for the indicator, whose span has several periods. It is true of each count and claims no shared month. Not changed.
- **OC-28** and the OUT-012, OUT-019 and OUT-023 rows state no adverse-event or one-month relation.
- **ISS-03 and ISS-13** speak of "the residual burden" without a shared month. ISS-13's question ("which month the residual burden then refers to") concerns compared periods shorter than 28 days.

**`RATIONALE.md`.**
- No entry is anchored to INV-061.
- INV-075/D01 concerns the drug and formulation of a line (a tie that v35 moved to INV-123; declined in review 37). It states no adverse-event relation.
- Two entries restate INV-061, and both name the kind of period without claiming a shared month:
  - INV-060/D02: "A residual burden "per month" refers to a calendar month or 28-day period within the compared period (INV-061)". This is the existence argument for compared periods shorter than 28 days.
  - E-044/D01: "'Per month' is represented by a monthly period".
- No entry restates INV-075's adverse-event relation. The four occurrences of "adverse" are in E-045/D07, E-055/D02, the INV-123/D01 table and INV-001/Q00.
- `RATIONALE.md` is unchanged.

## 5. All changed locations

`OUTPUT_MODEL.md`: three lines replaced and one line added.
1. Line 2, header: `Version: v40 · Iteration: 40 · Status: under review`.
2. INV-061 Reading (section 2).
3. INV-075 Reading (section 3).
4. Section 12: the v40 change-log entry.

`history/v40.md` and `history/v40-rationale.md`: new snapshots.

Nothing else changed: no `omn` block, Definition, Predicate, Meaning, Conformance, Realises, Evidence or Notes field, catalogue, case or source-data row, traceability row, Stage 1 issue, withdrawn row, source, or `RATIONALE.md` entry.

## 6. Checks

All checks were run on v40 with `check40.py`. Checks 1 to 5 give identical results on v39.

| Check | Result |
|---|---|
| Headings and IDs | 67 E, 87 INV, 12 ISS; no duplicate. 205 distinct E/INV/ISS references in the model and `RATIONALE.md`; 0 unresolved (40 withdrawn IDs in section 9). 174 table rows (OC, C1–C3, SD-*), none duplicated; 0 row references unresolved. |
| `RATIONALE.md` entries, both directions | 440 entries, none duplicated. All 370 entry IDs that the model names exist. Every entry's anchor is a model item, a table row or a section, and every ID in its Concerns field resolves. The 35 entries the model does not name are all anchored to case-table rows C1–C3, which have no Rationale column (as in v39). |
| Brace balance | All 160 `omn` blocks balanced for `()`, `[]`, `{}` and `⟨⟩`, with comments and string literals removed. |
| Formal text against v39 | 160 of 160 `omn` blocks byte-identical. The 191 table rows with code cells are byte-identical. |
| Traceability | 39 rows, in Stage 1 order (OUT-039 after OUT-025). The Elements and Invariants columns equal the reverse index of the Realises fields, and the catalogue column equals the rows whose Realises cell names the requirement: 0 differences. |
| Catalogue "def." lists | For each of the 45 rows, the "def." list equals the definitional invariants whose Conformance field names an element of the row, minus the invariants stated once for all rows (INV-006, INV-121, INV-122, INV-123; section 4.2): 0 differences. |
| Readings against predicates (`witness.py`, `reading_text.py`) | Both counter-examples are admitted by the unchanged predicates and contradict the v39 Readings. The v40 Readings agree with the predicates on every case: 392 of 392 residual burdens (INV-061) and 4,096 of 4,096 attack lines (INV-075) in the exhaustive runs. In the v40 file, both predicates and their Conformance, Realises and Evidence fields are byte-identical to v39, the v39 overclaim phrases are absent, and every encoded clause is present. |
| Satisfiability | No predicate changed, so the set of admitted outputs is that of v39. |
| Scope | The added lines contain none of the scope terms (input, record, entered, captured, questionnaire, answer, storage, database, JSON, XML, FHIR, algorithm, computed from, calculated, reminder). |
| Snapshots | `cmp OUTPUT_MODEL.md history/v40.md` and `cmp RATIONALE.md history/v40-rationale.md`: identical. `RATIONALE.md` is identical to the v39 baseline. |

## 7. Diff summary of formal blocks

None. 0 `omn` blocks changed or added; 160 of 160 are byte-identical to v39. 0 formal table cells changed. The fix is prose only.

Watch points of the check after iteration 36:
- **Watch point 1** (INV-060 antecedent, ISS-13): untouched.
- **Watch point 2** (definitional presence ties): no presence tie is added at definitional level. This is why the INV-075 alternative was declined.
- **Watch point 12** (bookkeeping cascades): the sweep stayed in the remark's class, and the adjacent role-description pattern was recorded, not swept.
- **Watch point 13** (volume): 0 formal changes.
