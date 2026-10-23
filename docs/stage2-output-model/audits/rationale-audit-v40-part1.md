# RATIONALE audit — part 1 (lines 1–853), model v40
Date: 2026-10-23
FINDINGS: 2 (CONTRADICTION 2, OVERCLAIM 0, STALE 0, WRONG-REFERENCE 0)
Entries audited: 136 entries in lines 1–853, plus section 1 "Purpose and rules": D 82, N 3, W 1, S 0, X 0 (none in this range), and the non-quote prose of 50 Q entries (Text prose, Concerns lines, Location notes).

## Method

I read PROCESS.md in full, the whole of `OUTPUT_MODEL.md` v40 (sections 1–11), `RATIONALE.md` lines 1–853, review 41 (R41-01), the oscillation check after iteration 40 (watch points), and the parts of reviews 18, 19, 25b, 36–41, fixes 18, 32, 35, 35-equivalence and 36–40, plan-v35 §7.2 and equivalence-v35 that bear on the entries in this range. I compared every statement that an entry makes about the model with the v40 formal text. I did not re-verify quotes against their sources.

Scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/ra1/`. Each was run with `python3 -I`.

- `inventory.py`: the 136 entries by kind. Kind order within each anchor is Q, D, N, S, W, X; elements appear in model order. Every entry in the range is named by the model, except the 35 C1–C3 origin entries, which section 4.4 names collectively. `order_all.py` repeats the order check over the whole file: 0 violations.
- `origins.py`: the 35 C1-NN/C2-NN/C3-NN/D01 entries against v34. Every "Origin in v34" title equals the v34 heading. Every "Stage 1 part" equals the table's Stage 1 part column. The conjunct numbers of v34 INV-100 and INV-092 were read in `history/v34.md`.
- `movedcmp.py`: every `Text (v34 …)` block against its v34 field, sentence by sentence. The differences are only the re-pointed references (moved-text exception 1), the v35 qualifications (E-040/D01, ISS-13) and the CA-05 correction (E-039/D02). Each was read.
- `refs.py`: every item ID in the range resolves. The only reference to a withdrawn item is C1-13/D01's own Concerns line.
- `concerns.py`: for each Q entry, every SD row in its Concerns names the entry in its Rationale cell, and every item in its Concerns cites the entry in its Evidence field. 0 exceptions.
- `dates.py`:
  - E-007/D01 example: 15 August to 20 October = 67 days.
  - E-041/D05, "at least 8 weeks after the start": for every rule except the three end-of-cycle rules, the minimum gap between anchor and time point over 8 years of anchor dates is ≥ 56 days. The smallest are 14A and SIGN titrated (56) and NVN and Box 8 (59).
- `resumes.py`: INV-001's `resumes` conjuncts, `resumesFrom` and `originalStart` transcribed. Checked over 11,677 admissible contexts (3 courses, 4 dates) against E-008/D02's claims: one backward chain, chronological, `originalStart` is the start of the first course or the course's own start, at most one member. 0 violations.
- `stopanchor.py`: `notStoppedBefore`, `intervalOnTreatment`, `shift` and the INV-001 course-event constraints transcribed, for the three end-of-cycle rules (SD-ER-03, -17, -18). Result: 261 cases in which a stop dated before the anchor date leaves the time point asked by INV-059 and admitted by INV-058; in every case the stop is dated on the day before the anchor (RA-1-02).
- Inline greps (shown in the session) located the uses of `concerns`, `onlyOfType`, `scopeFor`, `containsPeriodOf`, `fillsPeriod`, `onSameScale`, `inSameForm`, `presents`, `labelledAs`, `notStoppedBefore`, `intervalOnTreatment`, `fitsMonthlyPeriod`, `c8_2_7`, `.claims`, and `paused`/`discontinued`.

## Findings

### RA-1-01 CONTRADICTION: SEC-3.4/D01 says attacks are required, where provided, in response comparisons (INV-057); INV-057 asks only for moderate/severe headache days, and a response comparison cannot hold attack counts
- Entry: SEC-3.4/D01 (moved verbatim from v34 section 3.4; in the model since v04, fix 04, R04-02), second bullet.
- Entry text: "Availability per calendar month or 28-day period, for every period of the selected time range, is MUST wherever the measure is provided. For headache days, and for migraine days for patients with migraine (the condition of OUT-005), this is INV-118 (C1-01, C1-02); for moderate/severe headache days and attacks it is INV-118 (C1-04, C1-06) (`provides(K)`), as in their comparisons of equal-length periods (INV-037), per headache type (INV-118 (`byTypeCases`)) and in response comparisons (INV-057)."
- Model text:
  - INV-057 "Moderate/severe headache days in the comparison, where reported": `∀ rc : ResponseComparison • provides(ModerateSevereHeadacheDays) ⇒ (∀ p ∈ {rc.baseline} ∪ ran rc.onTreatment • ∃ m ∈ rc.values • m.measure = moderateSevereHeadacheDays ∧ …) ∧ (∀ p ∈ ran rc.onTreatment • ∃ ch ∈ rc.changes • ch.reference.measure = moderateSevereHeadacheDays ∧ …)`. Reading: "Where the diary reports moderate/severe headache days, the response comparison also shows them, with their changes from baseline."
  - E-043: `values : set1 →DayCount  MUST`, `changes : set1 →Change  MUST`. E-040: `reference : →DayCount`, `compared : →DayCount`. E-019: `element EventCount extends PeriodValue` (an attack count is not a `DayCount`).
  - E-043 Meaning: "monthly migraine days and monthly headache days (and, where the diary reports them, moderate/severe headache days)".
- Why they conflict:
  - "Their" refers to moderate/severe headache days and attacks. The entry places both, at MUST where provided, in response comparisons and names INV-057 as the item that does so.
  - INV-057 names only moderate/severe headache days. No item asks for attacks in a response comparison.
  - The model's types exclude them: a response comparison's values and the values its changes compare are `DayCount`s, and an attack count is an `EventCount`.
  - The other two places in the sentence are correct for both measures: INV-037 has `provides(AttackCount) ⇒ …`, and `byTypeCases` contains `(oc08, must)`.
  - The model is right. Stage 1 OUT-018 reads "(and, where reported, moderate/severe headache days)" and names no attacks.
  - New evidence against review 39 ("SEC-3.4/D01 states the reading precisely"): that review tested the model's §3.4 sentence through INV-037 only. It did not test INV-057's scope for attacks or E-043's value types. No watch point names SEC-3.4/D01 or INV-057.
- Correction, to the entry only (no formal change): "… for moderate/severe headache days and attacks it is INV-118 (C1-04, C1-06) (`provides(K)`), as in their comparisons of equal-length periods (INV-037) and per headache type (INV-118 (`byTypeCases`)), and, for moderate/severe headache days, in response comparisons (INV-057)."
  - Class (section 6a): entries that attribute attack counts to response comparisons. I searched the whole RATIONALE for INV-057 and for "attack… response comparison". The only other entry citing INV-057 is INV-118/D01 (outside this range), which cites it only for the `provides(K)` form, and that is correct. INV-118/D02 cites it, correctly, for the type scope "at which the response comparison shows its own values". SEC-3.4/D01 is the only member.

### RA-1-02 CONTRADICTION: E-041/D06 says a course stopped before the anchor date has no time point at that anchor date, whatever the anchor kind; for the end-of-cycle rules with no further offset, a stop on the day before the anchor date keeps the time point
- Entry: E-041/D06 (v34 E-041 Notes, **Stop or pause**; written by fix 18, R18-01, in v18).
- Entry text: "… the time point is shown and required only where no stop or pause of the course is dated before the last day of the interval, the day before the time point (for a window, before its first date, the end of the minimum interval the guidance names); a stop or pause is dated on the last day of the course (section 2.8), so a course stopped on that last day has completed the interval. A course stopped or paused earlier, or before the anchor date, has no time point of the rule at that anchor date, whatever the anchor kind, just as a course has no time point of a rule anchored at the end of a treatment cycle that did not take place; …"
- Model text:
  - E-042: `pred intervalOnTreatment(c, t, a, r) ≙ notStoppedBefore(c, t, plusDays(shift(a, r.minOffset), −1))` and `pred notStoppedBefore(c, t, d) ≙ ¬ ∃ e ∈ c.subject.courseEvents • e.treatment = t ∧ e.kind is stop ∧ e.date < d`.
  - INV-058 (definitional) admits, and INV-059 (MUST) asks for, a time point exactly where `applicable ∧ intervalOnTreatment` holds.
  - SD-ER-03 `ruleNice1329`, SD-ER-17 `ruleTr3639` and SD-ER-18 `ruleTr73`: `endOfCycleAnchor(n)` with `minOffset` `weeks(0)`.
  - Section 2.8: "The end of treatment cycle n (`cycleEnd(n)`) is dated on the first day after that cycle"; a stop "is dated on the last day of the course".
  - INV-001 orders dose changes and the target dose before the stop, but not cycle ends.
- Why they conflict:
  - For these three rules, `shift(a, weeks(0)) = a`, so the last day of the interval is a − 1, the day before the anchor date.
  - A course stopped on a − 1 has no stop dated before a − 1. So `intervalOnTreatment` holds, INV-059 asks for the time point, and INV-058 admits it. Yet the stop is dated before the anchor date. The model therefore contradicts the second sentence quoted, which also contradicts the entry's own first sentence (a course stopped on the last day of the interval has completed it).
  - This is the ordinary case for these rules, not a contrived one. Example: an onabotulinumtoxinA course starts 2026-01-05, with re-treatment every 12 weeks. `cycleEnd(1)` is 2026-03-30. The course is discontinued after its second cycle, so the stop is dated 2026-06-21 (the last day of cycle 2) and `cycleEnd(2)` is 2026-06-22. NICE 1.3.29 then has its time point at 2026-06-22. INV-055 (MUST) asks for a comparison whose 28-day on-treatment period, 2026-05-25 to 2026-06-21, ends on the stop date, because `fitsMonthlyPeriod` holds and `notStoppedBefore(c, t, p.end)` holds.
  - `stopanchor.py` finds 261 such cases. In every one the stop is on a − 1, and for stops earlier than a − 1 the entry is correct.
  - For start and dose anchors the clause is vacuous, because INV-001 puts the start and the target dose on or before the stop. So the clause is false for the only anchor kind on which it has content.
  - The model is right, and fix 18 intended it so. Its log says, on dropping the review's `a ≤ e.date`: "For cycle-end anchors with `weeks(0)` the two forms agree". Under both forms a stop on a − 1 keeps the time point.
  - E-042/D01 (outside this range) already states the rule correctly: "A course stopped or paused before the last day of the interval has no time point of the rule at that anchor date". So E-041/D06 also disagrees with that entry.
  - New evidence against review 19's note ("a stop before the anchor date also ends the course before the interval"): that note does not hold for zero offsets. No watch point names this sentence. Checks 08–24 watch E-041's values, `excludes`, ages and timings; check 24 watches the day convention and the stop bounds, which the correction leaves unchanged.
- Correction, to the entry only (no formal change): replace the quoted sentence with "A course stopped or paused earlier has no time point of the rule at that anchor date, whatever the anchor kind (for a rule anchored at the end of a treatment cycle with no further offset, the last day of the interval is the last day of that cycle, the day before the anchor date, so a course stopped on that day keeps the time point), just as a course has no time point of a rule anchored at the end of a treatment cycle that did not take place; …".
  - Class (section 6a): claims that a stop before the anchor date removes a time point. I searched the RATIONALE and the model for "before the anchor date", "whatever the anchor" and "anchor date". E-041/D06 is the only member, and E-042/D01 is correct.

## Checked and consistent

- **Header, line 2** ("Version: v39 (companion of OUTPUT_MODEL.md v39)"): the established convention for an unchanged RATIONALE. v37 kept "v36 (companion of … v36)", and the model's header reads "Companion: RATIONALE.md v39". Not a statement about the model's content.
- **Section 1** (purpose, entry IDs, kinds, moved-text exceptions, order): the eight subsections 2.1–2.8 exist as listed, kind order holds in the whole file, and "X Notes" in moved text is used as defined.
- **SEC-2.11/W01**: every unfolding equals the v40 row:
  - SD-ER-02, all nine components of `EvaluationRule`, with `evaluationRules` from `ruleNice1327` to `ruleTr73`;
  - SD-GB-01;
  - SD-IC-01;
  - SD-SR-03 with its domain;
  - SD-IN-05 `¬ publishedGrading(halt30)`;
  - SD-CL-02 and the `—` default;
  - C1-02, whose instance of INV-118's first conjunct is as stated (the second conjunct is vacuous for `oc06`) and is equivalent to v34 INV-015 (`reportedTogether` over one kind = `reportedPerPeriod`);
  - SD-FX-08.
- **SEC-3.4/D01**, first and third bullets: C1-01, C1-02, C1-03 and C1-05 levels; OUT-008 and OUT-013 measures not frequency outputs (ISS-04). The second bullet is RA-1-01.
- **SEC-3.8/D01**: every listed formal test holds in v40 at the stated R-MCF clause (16 places, as plan-v35 §7.2). "The formal test is that of v34" was confirmed by equivalence-v35 ("The 16 places … keep their v34 formal tests"). INV-070's own "R-MCF (2)" note is covered by the E-049 `onTreatmentPeriod` entry (the merged conjunct).
- **C1-01/D01 … C3-12/D01** (35 entries): v34 origins, conjunct numbers (INV-100: indicator, label, trigger view, instrument category, screening; INV-092: the annotation conjunct) and Stage 1 parts all match. C3-02/D01 matches v34 E-010 Conformance. C1-13/D01 matches section 9 and INV-118/D04.
- **E-001/D01**: the nine C2 cases; `presents` is used only by INV-119, and no item asks for a claim to be made.
- **E-003/D01**: `qualities` is not formalised beyond membership (INV-104, INV-105).
- **E-006/D01**: `containsPeriodOf` is used only in INV-104 and INV-105, and `fillsPeriod` in these and INV-050. The 28-day start rule holds (`fillsPeriod`; INV-050 `covers.start = withdrawalStart`).
- **E-007/D01**: INV-001 (whole periods; `chosenPeriod` bounded only by the as-of date); INV-094 Reading; 67 days.
- **E-008/D01–D04**:
  - one stop per course, and the `resumes` constraints of INV-001 (script);
  - E-049 `baseline` `when` and INV-112;
  - every relation uses `e.kind is stop`; only markers and the post-stop view show the stated kind, through `factsShown`/INV-123 (no other use of `paused` or `discontinued`);
  - 0-attack summaries are admitted (INV-072 Notes, INV-074).
- **E-009/D01**: `c8_2_7` occurs only in the constant list, the hierarchy axiom and SD-IC-14; no indicator code is 8.2.7 (SD-CLS, SD-CMB).
- **E-011/D01, D02**: INV-031 relates the IHS 2025 count only under `labelledAs(…, ihs2025MigraineDay)`. `reports` covers the listed forms and excludes `AssociatedSymptomSummary`, acute summaries and lines, headache-free and symptom-free days, and the E-018 count. Since v39, E-056 `frequencyValues` are shown in the view and so are covered.
- **E-012/D01**: `concerns` is used in E-033, C3-12, INV-091, INV-092, INV-093 and INV-115; `onlyOfType` in INV-073 and INV-089; `scopeFor` in INV-062, INV-088 and E-046 `attackScope`. The definitions give the stated readings. For example, for {c1_3, c2}, `scopeFor(…, c1)` is `ofType(c1)`, next to the per-type `ofType(c1_3)` of INV-118 (`byTypeCases`). Consistent with review 41's class check.
- **E-013/D01, D02, N01**: INV-012 (one value per numeric form, the proportion tied to the length); INV-011's four conjuncts cover the listed summaries; no 80 % or trial cut-off in the model; C2-02.
- **E-014/D01, E-019/D01, E-033/D01**: derived values with no input relation (section 2.7); `EventCount` and `DayCount` are disjoint types.
- **E-016/D01, E-018/D01, D02**: no relation ties migraine days or the E-018 count to a count under another definition (INV-031, INV-122). Control-level labels carry the `controlLevels` criterion (INV-062 SHOULD; INV-063).
- **E-020/D01**: INV-031 is an inequality.
- **E-022/D01**: E-022 and INV-104 have no `hasType` condition (ISS-03).
- **E-023/D01, D02**:
  - `onSameScale` compares `OtherSummary.form` by equality;
  - the only uses of `onSameScale` are INV-039, INV-069 and INV-105;
  - INV-062's per-period values of a criterion are not "asked … in order to compare them", the reading fix 32 recorded when it declined a scale tie there (check 36, watch point 10).
- **E-025/D01**: `inSameForm` is used only in INV-069.
- **E-027/D01**: unchanged from v34. Aura counts and durations are separate kinds (`event = auras`, `auraDuration`), excluded from attack counts, from C1-08, from C2-03 and from C3-03; MAY, not frequency outputs.
- **E-028/D01**: `classesOf826` is declared in E-028, and SD-CMB uses it; ISS-01 and ISS-02.
- **E-029/D01**: INV-024 is bounded over the history-wide `acuteMedications` (E-008).
- **E-032/D01–D03, N01**: INV-045 (MonthlyKind periods; the span is the shortest run lasting more than three months; for a class, the level is reached iff every period of the span reaches it); no headache-day criterion.
- **E-036/D01**: C1-11 is `allTypes` only (ISS-09); no IHS Q12 limits in the model.
- **E-037/D01**: INV-038 with INV-003 and the INV-003 Note put the values in the comparison's view at MUST; equal length is required only by INV-037 (and by INV-097 for children).
- **E-038/D01**: `referencedCodes`; no criteria are restated.
- **E-039/D01–D04**:
  - INV-049 `< plusMonths(ws, followUpMonths)`, with SD-FX-05 = 12;
  - INV-050 `covers.start`, `fillsPeriod` and the covered-period counts;
  - "has no series" is what INV-050 allows when `wholePeriodFrom` fails;
  - `reviewWindow` is SHOULD with no `when`, and INV-051 has no bound to the covered period;
  - no age condition (ISS-11);
  - INV-049 covers each start separately.
  - The v38 removal of INV-049's series tie leaves these sentences true (fix 38).
- **E-040/D01** (both texts):
  - E-040 `when` clauses and the W2 MUST markers (the v35 place of v34 INV-054, section 9);
  - INV-053, INV-060 (≥ 28 days), INV-097 last conjunct, INV-003, INV-008, INV-011 and INV-111 second conjunct, all as stated.
  - The self-reference "(E-040/D01)" correctly re-points v34 "(INV-054 Notes)", whose text is this entry's second block.
  - A change outside a response comparison may show one form (INV-053).
- **E-041/D01–D05, N01**: checked against SD-ER and E-041/E-042:
  - the guidance set; ages per rule; `c1` for every rule; the `excludes` cells of 14A, Ru71 and Box 8 and the ∅ cells (both checked against the same-guidance later time points);
  - anchors, timings and offsets of every reading;
  - `applicable` with INV-001 (at least one type; only a listed type excludes);
  - "at least 8 weeks" (`dates.py`); `fitsMonthlyPeriod`;
  - age read on the start; no comparison without a stated start (INV-123);
  - N01: none of the listed items is a rule, and `ruleRu71` covers anti-CGRP monoclonal antibodies.
  - E-041/D06: correct except the sentence of RA-1-02. Its window reading and "the comparison at it then ends on or before the stop" are correct (INV-055).
- **Q entries, non-quote prose** (E-008/Q00, E-009/Q01–Q03, E-018/Q01–Q03, E-023/Q00, E-028/Q01–Q03, E-032/Q01–Q07, E-039/Q00, E-041/Q00–Q30):
  - Concerns lines agree with the model's Evidence fields and the SD Rationale cells (`concerns.py`, 0 exceptions).
  - E-041/Q00's count: 11 rules with offsets in Stage 1 quotes, 7 without; 18 = SD-ER-01 to -18.
  - E-008/Q00's pointers: the IHS Q6 sentence is in E-045/Q01, and "aged 12 years and older" is in E-041/Q01.
  - E-018/Q02's scope note agrees with E-011 (`ihs2025MigraineDay` is named, its definitions are not stated).
  - E-023/Q00 supports `onSameScale` in INV-039, INV-069 and INV-105.
