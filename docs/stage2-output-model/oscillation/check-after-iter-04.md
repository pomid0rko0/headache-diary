# Oscillation check — after iteration 04
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: versions v00, v01, v02, v03 and v04 (history/v00.md to history/v04.md; OUTPUT_MODEL.md is identical to v04); reviews review-iter-01 to review-iter-04 (no b or c re-checks exist, because every review returned REMARKS); fixes fix-iter-01 to fix-iter-04; earlier oscillation checks: none (this is the first Stage 2 check).
Date: 2026-10-21

## Method

1. **Git history.**
   - Checks:
     - each snapshot was added in exactly one commit: f5eeb50 (v00), 060cdd8 (v01), d2201c8 (v02), d42ada3 (v03), 38b9ab2 (v04);
     - the committed snapshot equals the snapshot in the working tree;
     - OUTPUT_MODEL.md at each of these commits is byte-identical to that commit's snapshot.
   - All checks passed. The current OUTPUT_MODEL.md equals v04, and the working tree was clean before this check.
2. **Item split (script).** Each snapshot was split into items. Across the five versions there are 1,995 distinct items:
   - the header;
   - 12 sections and 43 subsections;
   - 67 elements and 461 element fields (heading, Definition, Meaning, Conformance, Realises, Evidence, Notes);
   - 165 attributes (`E-NNN.Type.attribute`, each with its comment lines) and 233 other declarations of the `omn` blocks (const, pred, axiom, enum, variant, type);
   - 108 invariants and 669 invariant fields;
   - 9 Stage 1 issues and 34 issue fields;
   - 39 traceability rows, each also split into its element, invariant and coverage columns;
   - the source rows S-101 to S-105, the withdrawn rows, the search-log lines and the change-log entries.
3. **State trajectories.** Each item was hashed in each version, giving a state string over v00 to v04 (for example `AABCC`; `-` = absent). The script flagged every item whose state returns to its state at a non-adjacent earlier version after a different state in between (A → B → A, including add → remove → add).
4. **Word-level diff.** For every item and every pair of versions vj < vi, the script compared 6-word n-grams in two directions:
   - n-grams deleted at vj and re-inserted at vi;
   - n-grams inserted at vj and deleted at vi.

   The same comparison was run over sections 1–9 as a whole, to catch text moved between items. Every hit was read in context.
5. **Conformance keywords.** The script tracked, across versions:
   - for every attribute, its type, its level and its `when` clause;
   - for every invariant, the level in its Conformance field;
   - for every element Conformance field, its MUST / SHOULD / MAY / SHOULD NOT / MUST NOT keywords.
6. **Remark topics.** The script mapped the `Item(s)` of all 30 remarks (R01-01 to R04-04) to E-, INV-, ISS- and S- IDs, and listed the IDs named in remarks of two or more iterations. Every remark that cites an earlier remark or fix was read, to see whether it asks to undo that fix.
7. **Judgement.** Each item changed in two or more versions was read against the remark that drove each change, and classified as convergent (one direction, with earlier guarantees kept) or oscillating (back and forth on the same point).
   - The menstrual-relation view was checked in more depth:
     - the conjuncts of INV-087 were compared version by version;
     - the conjuncts of the menstrual-relation view in v02, v03 and v04 were written as a script and evaluated on eight scenarios taken from R03-02 and R04-01 (see Findings).

**Results of the mechanical steps**

- **Step 3.** No item returns to a non-adjacent earlier state (0 flags).
  - 420 items changed at least once, and 86 changed in two or more versions.
  - Of these 86, some change in every version by construction: the header (version line), the introduction of section 9 ("as of vNN"), sections 11 and 12 (one paragraph or entry appended per version), and sections 5–9 as wholes.
- **Step 4, re-insertions.** The script found 11 n-grams re-inserted within the same item. All are fragments of formal syntax or ID lists that recur when a predicate or a row is restructured around unchanged terms: for example "∀ v : MenstrualRelationView • v", "( a . inPerimenstrualWindow ⇔ ∃" and "cycles ( E - 060 ,". None restores a deleted condition, value or statement.
  - Document-wide, 33 n-grams were re-inserted. They are of the same kind, or common phrases in unrelated places. For example, "moderate/severe headache days of" occurs in a v00 residual-burden Reading and in the v04 section 3.4 text.
- **Step 4, insert-then-delete.** Every such hit is a rewording that keeps the earlier content. Read in context for: E-041, E-043, INV-001, INV-087, INV-104, INV-105, E-060, E-061 and the rows OUT-030, OUT-034 and OUT-035.
- **Step 5.**
  - No attribute changed its level or `when` clause more than once, and no `when` clause was added and later removed.
  - No invariant changed level. The MUST count runs 18, 18, 18, 18, 19; the only change is the new INV-108 (v04).
  - Every change to an element Conformance field adds a level statement; none removes one.
- **Step 6.**
  - 20 IDs are named in remarks of two or more iterations (next sections).
  - No remark asks to revert an earlier fix.
  - No remark was declined, so no declined remark was raised again.

## Change history of items changed in two or more versions

Items that changed in only one version are not listed. Each row groups the fields and attributes of one element or invariant, and the traceability row that follows them. "Fields" names the fields that changed in two or more versions.

| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| **E-060** MenstrualRelationView, CycleLine.<br>Fields: Definition (v01, v04); Notes (v01–v04); `cycle` (v01, v04); `complete` (added v01, comment v04).<br>Changed once: `menstruationDays`, `firstDayOfMenstruation`, `perimenstrualWindow` (v04).<br>Added: `dayOneShown`, `nextWindowDays` (v04). | v01, v02, v03, v04 | **v01:** `complete` added; an unfinished last cycle runs to the end of the covered period.<br>**v02:** Notes: the line relations hold in every view, including the overview.<br>**v03:** Notes: the lines are exactly those that overlap the covered period; days −2/−1 of the next menstruation are window days for attack marks.<br>**v04:** a lead-in kind of line (`dayOneShown` false). For such a line, `menstruationDays` may be empty (`set` instead of `set1`), and day 1 and window are present only `when self.dayOneShown`. `nextWindowDays` added. | R01-08; R02-07 with the fix-iter-02 sweep (other change 8); R03-02, R03-03; R04-01, R04-04 | Convergent (see Findings). |
| **INV-087**.<br>Fields: Predicate and Reading (v01–v04); Notes and Evidence (v02–v04). | v01, v02, v03, v04 | **v01:** `completeCycles` is defined as the number of complete cycles within the covered period (it replaces `≤ #cycles`); only the last cycle can be unfinished, and it runs to the end of the covered period; the cycles are items of the view.<br>**v02:** the per-line and in-window relations are moved from the menstrual-relation view to every view.<br>**v03:** new conjuncts:<br>• the lines span the covered period (`first(v.cycles).cycle.from ≤ v.covers.start ∧ v.covers.end ≤ last(v.cycles).cycle.to`);<br>• the view's cycle lines are exactly `ran v.cycles`;<br>• in every view, each attack mark belongs to exactly one line;<br>• days −2/−1 of the next menstruation are window days.<br>**v04:** new lead-in branch: only the first line; it begins at `covers.start`; no day 1 or window; it ends before every day 1 the output shows. Also:<br>• `completeCycles` counts only lines with `dayOneShown`;<br>• new `nextWindowDays` relation;<br>• the second in-window disjunct is rewritten through `nextWindowDays`, an equivalent form. | R01-08; R02-07 sweep; R03-02, R03-03; R04-01, R04-04 | Convergent. Every conjunct that a fix added is present in v04, verbatim or in an equivalent form. v04 narrows the v00 day-1 relations to lines that show a day 1. |
| **E-061** AttackMark.<br>Fields: Meaning (v03, v04); Notes (v02, v03, v04). | v02, v03, v04 | **v02:** the relation holds in every view.<br>**v03:** a mark is relative to its own line and includes the next menstruation's window days.<br>**v04:** its line may be a lead-in; the next-window days are named through `nextWindowDays`. | R02-07 sweep; R03-03; R04-01, R04-04 | Convergent (follows INV-087). The attributes are unchanged v00–v04. |
| **INV-105**: Predicate (v02 only); Reading (v02, v04); Notes (v02, v03, v04).<br>**E-067** Notes (v02, v03, v04). | v02, v03, v04 | **v02:** a cycle line that overlaps the covered period, instead of one that begins in it; the treatment-effect antecedent applies only to started treatments.<br>**v03:** Notes on attached attack marks.<br>**v04:** Reading: the line may be a lead-in. | R02-07, fix-iter-02 other change 9; R03-03; R04-01 | Convergent. Each change admits more correct overviews, always in the same direction. The predicate is unchanged since v02. |
| **INV-086** (named in R03-02 and R04-01) | none | Unchanged v00–v04. | — | Stable. |
| **Traceability** rows OUT-030 (v01–v04) and OUT-035 (v02–v04) | v01–v04 | The coverage text follows the rows above. | as above | Convergent (consequential). |
| **INV-104**: Predicate, Reading, Notes (v01, v02, v03); Evidence (v01, v03).<br>**E-006**: Definition, Meaning, Notes (v02, v03).<br>Row OUT-034 (v01–v03). | v01, v02, v03 | **v01:** the series also shows migraine days, moderate/severe headache days, attacks and migraine-free marks; days with severe impairment are added.<br>**v02:** the series is required only when the covered period contains a whole period (new `containsPeriodOf`); the mark for the covered period is moved outside that condition.<br>**v03:** the series fills the covered period and is monthly whenever the covered period has at least 28 days, with overuse indicators per period (new `fillsPeriod`, `summaryTimeCourse`). For 7–27 days the series is weekly. The weekly acute-medication series is conditioned and tied to the covered period. | R01-09; R02-02 (a); R03-04 | Convergent.<br>• v02 relaxed the requirement only where v01 could not be satisfied.<br>• v03 keeps that condition for short periods and keeps the R01-09 content (now in `summaryTimeCourse`).<br>• Unchanged in v04. |
| **INV-001**: Predicate, Reading, Realises, Evidence (v01, v02).<br>**E-008** Notes (v01, v02).<br>**E-041** Notes (v01, v02).<br>**E-043** Conformance, Notes (v01, v02).<br>**E-045** (Notes v01; Definition and Meaning v02).<br>Row OUT-018 (v01, v02). | v01, v02 | **v01:**<br>• every preventive treatment has a type;<br>• NVN and Russian 7.1 evaluation rules;<br>• response comparisons over calendar months or 28-day periods;<br>• continuation-decision claim.<br>**v02:**<br>• no course event precedes the start;<br>• INV-055 is conditioned on `fitsMonthlyPeriod`;<br>• `valueAvailable`. | R01-01, R01-02, R01-03, R01-05; R02-01; fix-iter-02 other change 7 | Convergent.<br>• R02-01 repaired, with a condition, an unsatisfiable combination that the R01-03 fix had created.<br>• The monthly restriction and the R01-01 rules, all of whose time points lie at least 8 weeks after the start, are kept.<br>• No change since v02. |
| **E-046**: Definition, Conformance (v01, v02).<br>Row OUT-020 (v01, v02, v04). | v01, v02, v04 (row) | **v01:** `#L.evaluated = 1` in `reductionMet` and `reductionDecided`; MUST NOT continuation decision.<br>**v02:** the other values are shown where they are available.<br>**v04 (row only):** the IHS 2025 count follows the [S-010] definition. | R01-04, R01-05; fix-iter-02 other change 7; R04-03 | Convergent. Each change addresses a different point and adds to the text. |
| **E-053** Conformance (v01, v02).<br>Row OUT-012 (v01, v02). | v01, v02 | **v01:** each line shows a result for every outcome measure.<br>**v02:** applies to subjects with migraine (`hasType(ctx, c1)`), with all three symptom statuses. | R01-07; R02-06 | Convergent. |
| **E-037, E-048, E-049** Conformance (v02, v03).<br>Row OUT-021 (v02, v03). | v02, v03 | **v02:**<br>• E-037: for children, INV-039 applies to selections of equal length;<br>• E-048: per-class and per-drug days;<br>• E-049: an on-treatment period when the event falls after the start.<br>**v03:** each of the three adds the paediatric equal-length rule of INV-097. | R02-02 (b), R02-03, fix-iter-02 other change 5; R03-05 | Convergent. In v02 the paediatric rule was kept strict (INV-039 was restricted, INV-097 was not weakened); v03 extends it to more comparisons. |
| **E-032** Notes (v01, v03) | v01, v03 | **v01:** pointer to ISS-09.<br>**v03:** the two-class condition of ICHD-3 8.2.6. | R01-06; R03-01 | Convergent (additions on different points). |
| **E-057**: Definition, Notes (v01, v03).<br>**E-058** (v02, v03).<br>Row OUT-026 (v01, v03). | v01, v02, v03 | **v01:** `wholeNumberScores`; meaning of `high = ∅`.<br>**v02:** `baselineResult` only when there is an earlier result.<br>**v03:**<br>• `Instrument` becomes an open variant with `otherInstrument`;<br>• `publishedGrading(pgic)` removed; it was in v00 and was never added by a fix. | R01-10, R01-12; fix-iter-02 other change 6; R03-06, R03-07 | Convergent. Each change addresses a different point, and no value set returns after removal. |
| **ISS-04** (v01, v04)<br>**ISS-06** (v02, v03) | v01–v04 | **ISS-04:** v01 adds the migraine-free mark; v04 adds the reading of "Frequency outputs".<br>**ISS-06:** v02 adds the change-from-baseline consequence for HURT; v03 extends it to other instruments. | R01-09; R04-02; fix-iter-02 other change 12; R03-06 sweep | Convergent (additions). |
| Header; section 9 introduction; sections 11 and 12 | v01–v04 | Version line, "as of vNN", and one entry or paragraph appended per version. | — | Bookkeeping, not applicable. |

## Recurring remark topics

| Topic (IDs) | Remarks | Pattern | Assessment |
|---|---|---|---|
| Menstrual-relation view and cycle lines (E-060, E-061, E-067, INV-086, INV-087, INV-105; OUT-030, OUT-035) | R01-08, R02-07, R03-02, R03-03, R04-01, R04-04 | Six different defects; none asks to undo an earlier fix.<br>• R04-01 is a side effect of the R03-02 fix (its start conjunct). It asks for a change "without reintroducing the R03-02 defect (cycles chosen at will)".<br>• R04-04 carries the R03-03 fix over from attack marks to migraine days. | Convergent, with the most changes of any topic. Watch point 1 in the Conclusion. |
| Response comparison and evaluation time points (E-008, E-041, E-043, INV-001, INV-055, INV-056) | R01-01, R01-02, R01-03, R02-01 | R02-01: together with the R01-01 rules and NICE 1.3.29, the R01-03 fix made a MUST unsatisfiable. It was repaired with a condition, and R01-03 was kept. | Convergent. No remark since iteration 02. |
| Clinician-facing summary (E-006, E-066, INV-104) | R01-09, R02-02 (a), R03-04 | Content added; then a condition for periods that no series can fill; then the series tied to the covered period. | Convergent. No remark in iteration 04. |
| Paediatric equal-length comparisons (E-037, E-040, E-048, E-049, INV-039, INV-097) | R02-02 (b), R03-05 | Both changes widen the reach of INV-097. | Convergent. |
| Instrument value sets (E-057, E-058) | R01-10, R01-12, R03-06, R03-07 | Four different points: whole-number scores, the withdrawn ISS-07, the open instrument list, and the unsupported PGIC grading. | Convergent. |
| Acute-treatment lines (E-051, E-053) | R01-07, R02-06 | Per-line results, then symptom statuses for subjects with more than one headache type. | Convergent. |
| One defect pattern applied to further items | • total-only reading of OUT-014: R01-06 (INV-028), then R02-03 (INV-068);<br>• days with severe impairment: R01-09 (c) (INV-104), then R02-04 (INV-027);<br>• unfinished unit at the end of a covered period: R01-08 (INV-087), then R02-05 (INV-079), then R03-03 and R04-04 (INV-087) | Each later remark applies an earlier fix's pattern to an item that fix did not touch. | Propagation, not cycling. No earlier fix is reversed. |

**Settled points.** Reviews 02, 03 and 04 list the same settled decisions as "not reopened (no new evidence)", and none of the items concerned changed after being settled:

- INV-106 at MUST NOT;
- the AAN/AHS 14A and NVN window readings;
- INV-023 at any granularity;
- the MIDAS label choice;
- the 24-hour outcomes for cluster summaries;
- "history of previous bouts";
- the context as properties of the subject.

**Remark counts per iteration:** 12, 7, 7, 4.

## Findings

None.

### Assessment of the menstrual-relation view (E-060, E-061, INV-086, INV-087, INV-105)

The view was changed in all four iterations (R01-08; R02-07 and its sweep; R03-02, R03-03; R04-01, R04-04). The table lists every guarantee of the view, the version and remark that introduced it, and its state in v04.

| Guarantee | Introduced | State in v04 |
|---|---|---|
| G1. The lines are consecutive, earliest first. | v00 | Kept. v04 adds that every line after the first shows its day 1. |
| G2. Every line overlaps the covered period. | v00 | Kept. |
| G3. Only the last line can be unfinished, and an unfinished line runs to the end of the covered period. | v01, R01-08 | Kept. |
| G4. `completeCycles` is the number of complete lines that lie wholly within the covered period. | v01, R01-08 | Kept. A lead-in is also excluded (`dayOneShown`). |
| G5. The line relations hold in every view, including the patient-facing overview. | v02, R02-07 sweep | Kept. |
| G6. The overview requires a line that overlaps the covered period, not one that begins in it. | v02, R02-07 | Kept. The line may be a lead-in. |
| G7. The lines span the covered period (`first(v.cycles).cycle.from ≤ v.covers.start ∧ v.covers.end ≤ last(v.cycles).cycle.to`). | v03, R03-02 | Kept verbatim. |
| G8. The view's cycle lines are exactly `ran v.cycles`. | v03, R03-02 | Kept verbatim. |
| G9. Every attack mark belongs to exactly one line of its view, in every view. | v03, R03-03 | Kept verbatim. |
| G10. Days −2 and −1 of the next menstruation are window days for attack marks. | v03, R03-03 | Kept, rewritten through `nextWindowDays`. The two forms are equivalent because the onset lies in its line: given `from ≤ onset ≤ to`, `onset ∈ [max(to − 1, from), to]` holds exactly when `to − 1 ≤ onset`. |
| G11. The same for the migraine days of the line. | v04, R04-04 | New. |
| G12. Day 1 is the first day of the line and the earliest menstruation day; the window is day 1 ± 2. | v00 | Kept for every line that shows its day 1. It does not apply to a lead-in, which shows no day 1. |
| G13. No lead-in is shown where the output shows a day 1 on or before its last day. | v04, R04-01 | New. INV-087 has output scope (section 2.9), so `∀ cl₂ : CycleLine` ranges over the lines of the same output. |

No conjunct that a fix added was removed. The in-window relation was extended in v02 (every view), v03 (the next menstruation, attached marks) and v04 (migraine days, lead-in), always in the same direction.

**The start of the view** is the one point that moved in both directions. The scenario script gives these results (✓ = admitted by the conjuncts of that version):

| Scenario (covered period 1 January – 30 June) | v02 | v03 | v04 |
|---|---|---|---|
| S1. R03-02 example: only the March and April cycles shown | ✓ | ✗ | ✗ |
| S2. All cycles that overlap the covered period shown | ✓ | ✓ | ✓ |
| S3′. R04-01 example (first menstruation on 10 March), v02 form: cycles from 10 March, and no line for 1 January – 9 March | ✓ | ✗ | ✗ |
| S3. R04-01 example, v04 form: a lead-in from 1 January to 9 March, then the cycles | ✗ | ✗ | ✓ |
| S3b. R04-01 example with a day 1 on 1 January that did not occur | ✓ | ✓ | ✓ |
| S4. A lead-in that covers January and February cycles that occurred, when no view of the output shows their day 1 | ✗ | ✗ | ✓ |
| S4b. As S4, but another view of the same output shows the 18 January day 1 | ✗ | ✗ | ✗ |
| S5. A lead-in, then the March and April cycles only (end cut off) | ✗ | ✗ | ✗ |

**Reading of the scenarios.**

- **The menarche case.** The information is admitted in v02 (form S3′), excluded in v03 except with an invented date (S3b), and admitted again in v04 (form S3). This is the closest thing to an A → B → A pattern that this check found.
- **Why it is not an oscillation:**
  1. **The item did not return to an earlier state.**
     - The v04 predicate differs from v02: G7 and G8 hold, so every day of the covered period lies in a line (S3′, which leaves days outside any line, is still rejected).
     - The R03-02 target, S1, is still rejected, and so is the end cut-off, S5.
     - v04 admits the menarche case only in a new, explicit form (a lead-in that shows no day 1, has no window and is never counted). That form did not exist in v02.
  2. **The remarks did not compete.**
     - R03-02 targeted cycles chosen at will (S1), and its required change itself offered an explicit alternative at the start: "Or, if the author holds that the first day of the cycle in progress at the start need not be shown, an explicit alternative with its reason".
     - R04-01 targeted only the collateral exclusion of correct views, and required a change "without reintroducing the R03-02 defect (cycles chosen at will)".
     - No remark argues for admitting S1, and none argues for excluding S3. Both remarks aim at the same set of admitted views, so there are no competing positions to freeze.
  3. **The R03-02 guarantee keeps its strength.**
     - In v04, S4 is admitted by the predicate only through a lead-in that contradicts the lead-in's own Meaning: by E-060, no first day of menstruation lies in a lead-in.
     - In v03, the corresponding view had to state an invented day 1 (S3b).
     - In both versions, defeating the R03-02 guarantee therefore requires a false statement in the output, which no predicate over output elements can exclude. In v02 it required none: S1 is admitted with correct dates.
     - The v03 and v04 Notes both keep the sentence "the number of complete cycles does not depend on a choice of which cycles to show".
- **Judgement.** Convergent refinement. v03 overreached at the start of the view, and v04 corrected that overreach while keeping every v03 guarantee. Later fixes do not undo earlier guarantees.

## Conclusion

No item of the model oscillates after four iterations, and nothing is frozen.

- No item (element, attribute, field, invariant, source, section, value set, conformance level or traceability row) returns to an earlier state.
- No conformance level changed more than once.
- No remark asks to undo an earlier fix, and no declined remark was raised again.
- The number of remarks falls from 12 to 7, 7 and 4.
- Every item changed in two or more versions shows a one-directional series of additions or narrowings. Each new remark either repairs a side effect of the previous fix or carries a fixed pattern over to another item.

**Watch points for the next checker** (not findings):

1. **Start of the menstrual-relation view** (INV-087: the conjunct `first(v.cycles).cycle.from ≤ v.covers.start` and the lead-in branch).
   - Changed in v03 (tightened, R03-02) and in v04 (qualified, R04-01).
   - A further change on this point, in either direction, would be the third change on the same point. Examples: restricting or removing the lead-in on the R03-02 ground, or relaxing the start of the view further on the R04-01 ground.
   - Unless it rests on evidence that neither R03-02 nor R04-01 considered, such a change should be treated as oscillation.
2. **The menstrual-relation view as a whole.** It has drawn six remarks in four iterations, and two of them followed from the previous fix (R04-01 from R03-02; R04-04 from R03-03). Further remarks caused by fixes on E-060, E-061, INV-087 or INV-105 should be checked for reversal.
3. **INV-104.** The pattern so far is: content added, then a condition for short periods, then the series tied to the covered period. It has been stable since v03. A remark that asks to drop the R02-02 (a) condition, or to loosen the R03-04 tie to the covered period, would reverse an earlier fix.

The scripts used are in the session scratchpad: `split.py`, `analyse.py`, `ngram.py`, `conf.py`, `wdiff.py` and `mrv.py`. FROZEN_ITEMS.md was not written, and OUTPUT_MODEL.md and the history snapshots were not changed.
