# Oscillation check — after iteration 16
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: versions v00 to v16 (history/v00.md to history/v16.md; OUTPUT_MODEL.md is byte-identical to v16); reviews review-iter-01 to review-iter-16 with the re-checks review-iter-08b and review-iter-10b (18 files, 56 remarks: 12, 7, 7, 4, 3, 1, 3, 0 + 2, 1, 0 + 2, 3, 2, 3, 2, 3 and 1); fixes fix-iter-01 to fix-iter-16; the earlier oscillation checks after iterations 04, 08 and 12, with the seven watch points of check-after-iter-12.md. Reviews 13–16 and fixes 13–16 were read in full; the earlier reviews and fixes were read where they concern an item that changed in v13–v16 or a watch point.
Date: 2026-10-21

## Method

1. **Git history.**
   - Checks:
     - each snapshot was added in exactly one commit and never changed afterwards: v00 f5eeb50 … v12 f8ab130 (as in the iteration-12 check), v13 ea5017e, v14 5382630, v15 8d12fa3, v16 864b796;
     - the committed snapshot equals the snapshot in the working tree;
     - OUTPUT_MODEL.md at each of these commits is byte-identical to that commit's snapshot;
     - every review, fix log and earlier check was added in its own commit, in the order of the loop: check 12 bb149a1; review 13 6104823; fix 13 ea5017e; review 14 bfa8ba3; fix 14 5382630; review 15 aad549c; fix 15 8d12fa3; review 16 bd8f9bd; fix 16 864b796;
     - each fix commit of iterations 13–16 touches only OUTPUT_MODEL.md, its snapshot and its fix log, and each review commit only its review; Stage 1 has not changed since bfec74f (v18 converged).
   - All checks passed. The working tree was clean before this check, and OUTPUT_MODEL.md equals v16.
2. **Item split** (the splitter of the iteration-08 and iteration-12 checks, extended to 17 versions). Across v00 to v16 there are 2,442 distinct items:
   - the header, the sections (whole and introduction) and their subsections;
   - every element and element field (heading, Definition, Meaning, Conformance, Realises, Evidence, Notes);
   - every attribute and every other declaration of the `omn` blocks (const, fun, pred, axiom, enum, variant, value, element);
   - the 18 `EvaluationRule` constants of E-041 and the 6 `ResponderCriterion` constants of E-045, each split out of its axiom;
   - every invariant and invariant field; every Stage 1 issue and issue field;
   - the 39 traceability rows, also split into their element, invariant and coverage columns;
   - the source rows, the withdrawn row, the search-log lines and the change-log entries.
3. **State trajectories.** Each item was hashed in each version, giving a state string over v00–v16 (`-` = absent). The script flags every item whose state returns to its state at a non-adjacent earlier version after a different state in between (A → B → A, including add → remove → add and add → remove).
4. **Rule components and the `excludes` criterion** (`rules.py`, `excl16.py`).
   - Each component of the 18 rules and of the 6 criteria was tracked across versions.
   - `excl16.py` parses the rules of each version v07–v16 and applies each of the three `excludes` wordings (the attribute comment of v07, of v08 and of v14, with the criterion sentences of the E-041 Notes) to them. Each rule's time point or window is expressed in weeks from its anchor, with a treatment cycle of 12 weeks (NICE TA260 "every 12 weeks"; Turkish "3 ay aralıklarla"). The script compares what each wording gives with the stated values, and tests whether the three wordings are nested for every rule of every version.
5. **Word-level diff** (`show.py`, `show3.py`, `ngram.py`, `dels16.py`, `docwide.py`).
   - A word-level diff of every item changed in v13–v16. Every predicate change was read, together with every deleted prose span of four or more words.
   - For every item and every pair of versions vj < vi, 6-word n-grams compared in both directions: n-grams deleted at vj and re-inserted at vi, and n-grams inserted at vj and deleted at vi.
   - The same comparison over sections 1–9 as a whole, to catch text moved between items.
6. **Conformance** (`conf.py`, `attrtypes.py`). Tracked across versions:
   - for every attribute, its full declaration (type, level, `when` clause, `derived` mark);
   - for every invariant, its Conformance level;
   - for every element Conformance field, the count of each MUST / SHOULD / MAY / SHOULD NOT / MUST NOT keyword, with a flag on any count that drops.
7. **Guarantee terms** (`guar16.py`). In v08 to v16, the occurrences of 39 terms that carry earlier fixes: the 22 terms of the fix-15 and fix-16 lists, the R12-01 and time-frame terms (`givenFor(`, `childIn(`, `childOn(`, `aged12From`, `adultFrom`, `menstruationSpans`), the v13–v16 ties (`s.typeScope = allTypes`, `s.period = v.covers`, `within(s.period, v.covers)`, `summarisesMedication(`, `adherenceFor(`, `courseOverlaps(`, `courseNotOutside(`, `inPeriod(d, v.covers)`), and "lead-in", `referencedValues`, "R10b-01", "treatment-effect item" and "does not stand in for it". Every Realises field and every traceability row was also checked for an ID that was removed.
8. **Remark topics** (`remarks16.py`). The `Item(s)` of all 56 remarks were mapped to E-, INV-, ISS-, S- and OUT- IDs. The script lists the IDs named in remarks of two or more iterations, the remarks each remark cites, and every sentence of remarks 13–16 that uses revert, undo, reverse, restore, remove, drop, loosen or relax. Each remark of iterations 13–16 was read together with the fixes of the remarks it builds on.
9. **Scenario checks.**
   - `inv105.py`: the INV-105 treatment-effect conjunct under its formulas of v00, v02 (unchanged to v12), v13, v14, v15 and v16, on 4,000 random contexts. Each context has 0–2 preventive and 0–2 acute courses, with or without a stated start and stop, acute medications of up to two formulations, and a covered period. Each context is tested against 72–74 candidate treatment-effect items: response comparisons, and acute-treatment summaries of four drugs × three formulation scopes × two type scopes × three periods. The script checks that the antecedent never goes from false to true, that no item goes from rejected to accepted, and which outputs change conformance more than once, and why.
   - `inv105ant.py`: the INV-105 antecedent on 20,000 random contexts, with `acuteMedications` in v00–v11 read in two ways: as the medications in use on the as-of date (the reading of the fix-11 log that R12-01 reports) and as every medication used.
   - INV-098: the v11, v12 and v13 antecedents compared as predicates (the v16 antecedent is that of v13).
10. **Judgement.** Each item changed in two or more versions, at least once in v13–v16, was read against the remark or fixer change that drove each change. It was classified as convergent (one direction, earlier guarantees kept) or oscillating (back and forth on the same point).

**Results of the mechanical steps**

- **Step 3.** One item returns to a non-adjacent earlier state: `E-008.attr.SubjectProfile.aged12OrOlder` (`------AAAAAA-----`), added in v06 and removed in v12. The iteration-12 check assessed it (Findings A there). Nothing new in v13–v16.
  - 908 items changed at least once, and 342 in two or more versions. 174 items changed in v13–v16; 117 of them changed in two or more versions in all (39 IDs: 25 elements, invariants and issues, and 14 traceability rows).
  - **Change volume per version** (items changed, at the iteration-12 check's granularity): v09 85, v10 112, v11 161, v12 264, **v13 110, v14 73, v15 90, v16 28**.
    - Top-level elements, invariants and issues changed: v12 56, v13 21, v14 12, v15 12, v16 3.
    - Traceability rows: 16, 11, 5, 8, 1.
    - Invariant predicates changed: v13 10 (INV-110 new), v14 4, v15 8, v16 1.
    - These agree with the counts in fix logs 13 to 16.
  - No item was removed after v12, and no removed item was re-added. The change log is append-only (17 entries, none changed after its version). S-101 to S-106 are unchanged since v08, and no source was added in v13–v16. The withdrawn row is unchanged.
  - No Realises field lost an OUT ID, and no traceability row lost an E- or INV- ID, in any version.
  - `E-067.decl.pred.courseOverlaps` appears as changed in v16. This is a split artefact: the comment line of the new `courseNotOutside` follows it. The `courseOverlaps` declaration itself is byte-identical in v15 and v16.
- **Step 4.** No rule or criterion component changed after it was set.
  - The 17 rule constants of v07–v13 are unchanged in v14–v16, apart from a trailing `∧` on `ruleTr3639` (it is no longer the last conjunct of the axiom). `ruleTr73` is new in v14. The 6 criterion constants are byte-identical from v00 to v16.
  - The stated `excludes` value of every rule is unchanged since it was set (v07, or at creation). Only `ruleAan14A`, `ruleRu71` and `ruleTrBox8` exclude a type, onabotulinumtoxinA each.
  - The three `excludes` wordings applied to the rules (Findings, C):

    | Wording | In versions | What it gives against the stated values |
    |---|---|---|
    | v07 comment, read literally: "the types for which the same guidance names another time point" | v07 | Six (v07–v13) or seven (v14–v16) rules would exclude a type whose stated value is ∅: NICE 1.3.27 {cgrpInhibitor, onabotulinumtoxinA}, 1.3.28 {cgrpInhibitor}, 1.3.29, AAN 14B, Russian 3.3 BTA, Turkish 3.6.3.9 {onabotulinumtoxinA}, and from v14 Turkish 7.3. This is the defect R08b-02 found. |
    | v08 comment and criterion: a type-specific rule of the same guidance with a later time point | v08–v13 | All 17 values. On the 18 rules of v14 it would give `ruleTr73.excludes = {onabotulinumtoxinA}`, the result R14-01 foresaw. |
    | v14: as v08, but only for a rule named for all preventive treatment; ∅ for a rule named for particular types | v14–v16 | All 18 values. On the 17 rules of v07–v13 it also gives all 17 values. |

    For every rule of every version, what the v14 wording excludes ⊆ what the v08 wording excludes ⊆ what the v07 wording excludes.
- **Step 5, re-insertions within an item.** 11 hits, 4 of them with the re-insertion in v13–v16. All four are artefacts, not returns of content:
  - E-041 Notes v07 → v14 "the second treatment cycle, with no further": the anchor list "the end of the second and the third treatment cycle" became "the second, the third and the second" when `ruleTr73` was added;
  - INV-109 Notes v14 → v15 "not stand in for it. Satisfiability:": in v13 a paragraph ending "does not stand in for it" preceded the satisfiability sentence; the v14 paragraph was inserted between them, and the v15 adherence paragraph, which ends with the same words, again stands before it;
  - row OUT-010 v11 → v13: a boundary n-gram across the v11 insertion ("the values side by side …") and the v13 insertion ("over all headache types combined").
- **Step 5, insert-then-delete.** 637 hits, 198 of them with the deletion in v13–v16. They fall into four groups:
  - **Predicates.** Every predicate change in v13–v16 is either an added conjunct or the replacement of a term by a defined predicate that implies it:
    - `summarisesMedication(s, m)` ≙ `s.drug = m.drug ∧ (…)` replaces `s.drug = m.drug` (v15);
    - `adherenceFor(a, rc)` replaces `a.treatment = rc.treatment ∧ rc.treatmentStart ≤ a.window.start ∧ ∃ p … a.window.end = p.end` and adds `a.window.start ≤ p.start` (v15);
    - in INV-105 (v16), `ctx.subject.acuteMedications ≠ ∅` is replaced in the antecedent (Findings, A and B).
  - **Deleted prose spans of four or more words.** There are seven in v13–v16, and each is subsumed by its replacement:
    - INV-098 Reading (v13): "every view whose covered period begins while the subject is a child or adolescent" is kept as a special case;
    - E-041 Meaning and the `excludes` comment (v14): the criterion refinement;
    - INV-105 Notes, INV-105 Reading and row OUT-035 (v16): the acute antecedent. The v15 sentence "a subject whose preventive treatments have all stopped before the covered period, and who has used no acute medication, is not asked" is replaced by a sentence that covers it and more.
  - **Bookkeeping.** The header and version lines.
  - **No guarantee removed.** No deletion removes a condition, value or guarantee that an earlier fix inserted.
- **Step 5, document-wide.** 59 n-grams were deleted from sections 1–9 and later re-inserted; 18 of them were re-inserted in v13–v16. All are generic phrases ("the period the view covers", "not a defect of Stage 1", "have 0 treated attacks (INV-072, INV-074);") or the artefacts above. None restores a deleted statement in its own item. For example, "periods and over all headache types" left the INV-037 Reading in v11 only because a parenthesis was inserted inside it; the INV-037 statement is intact.
- **Step 6.** No conformance level returned.
  - No attribute declaration changed in v13–v16. No attribute declaration returns to an earlier state, and none changed more than once.
  - No invariant has changed its level in any version. The level totals changed only through new invariants; in v13–v16 only INV-110 (definitional, v13). In v16 they are MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8 and definitional 33.
  - No element Conformance field lost a level keyword in any version.
- **Step 7.** Every guarantee term occurs as often or more often in each later version, from v08 to v16. For example:
  - `#L.evaluated = 1`: 5, 6, 6, 7, 7, 7, 7, 7, 7;
  - `s.typeScope = allTypes`: 1 in v12, then 9 from v13;
  - `s.period = v.covers`: 2 from v14;
  - `summarisesMedication(`: 14 from v15;
  - `courseOverlaps(`: 6 from v15;
  - `menstruatesDuring`: 9 from v12;
  - "a later time point of its own": 4 in every version from v08.
- **Step 8.**
  - 34 IDs are named in remarks of two or more iterations, at least one of them in iterations 13–16. INV-105 leads (10 remarks: R02-07, R03-03, R04-01, R05-01, R11-01, R13-01, R14-02, R15-01, R15-03, R16-01), followed by seven IDs with 9 remarks each: E-041, INV-055, INV-062, INV-104, OUT-018, OUT-020 and OUT-035.
  - No remark of iterations 13–16 asks to revert an earlier fix. The flagged sentences say the opposite. For example, R13-02: "does not restore `ageGroup` or the as-of-date reading of v11"; R14-01: "Adding a rule with new evidence reverses no earlier fix".
  - No remark of iterations 13–16 was declined. No earlier declined remark was raised again. The formulation scope, which fixes 13 and 14 noted and left open, was never a remark before R15-01 (next sections).
- **Step 9.** See Findings A, B and E.

## Change history of items changed in two or more versions

Listed: items that changed in two or more versions, at least once in v13–v16. Items whose changes all lie in v00–v12 and that are unchanged since were assessed in the earlier checks (last row). "Fields" names the fields that changed.

| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| **INV-105** treatment-effect conjunct.<br>Fields: Predicate (v02, v05, v12, v13, v14, v15, v16); Reading (v02, v04, v05, v12–v16); Notes (v02–v05, v12, v14–v16).<br>**E-067**: Definition and Meaning (v15, v16: `courseOverlaps`, `courseNotOutside`); Notes (v02–v05, v12, v15, v16).<br>Row **OUT-035** (v02–v05, v11–v16); the INV-105 clause of **E-051** Conformance (v13–v16) | v02, v05, v12 (other conjuncts), v13, v14, v15, v16 | **v00:** antecedent `preventiveTreatments ≠ ∅ ∨ acuteMedications ≠ ∅`; consequent: one response comparison or acute-treatment summary, any.<br>**v02:** preventive part of the antecedent limited to started treatments ("treatment effect only where it can exist", fix 02 item 9).<br>**v05, v12:** series and cycle-line conjuncts only. In v12 the treatment-effect text is unchanged, but R12-01 widened `acuteMedications` to every medication used up to the as-of date (Findings, B).<br>**v13:** the acute alternative is over all headache types combined.<br>**v14:** the acute summary is of the covered period or a period within it (`within`).<br>**v15:** the preventive part of the antecedent and the comparison alternative are tied to a course taken during the covered period (`courseOverlaps`); the acute summary is of a medication the subject has used (`summarisesMedication`).<br>**v16:** the acute part of the antecedent becomes an acute course that the context does not place outside the covered period; the acute summary's drug is that of an acute course not placed outside the summary's period (`courseNotOutside`). | R02-07 (cycle line), R05-01 (series), fix-02 item 9; R13-01 (optional item); R14-02 (d); R15-01 (optional item) and the fix-15 identifying-property check (other change 1); R15-03; R16-01 | **Convergent** (Findings, A and B).<br>• The antecedent only narrowed (v02, v15, v16), always on the ground that a treatment effect is asked for only where one can be shown.<br>• The alternatives only gained conjuncts (v13, v14, v15, v16).<br>• "One item suffices" holds in every version: the conjunct is `∃ … ∨ ∃ …`, never per treatment.<br>• v16 keeps every v13–v15 tie verbatim. |
| **Acute-summary identity ties**: INV-062 (Predicate v13, v15; earlier v02, v05, v08–v12); INV-069 (Predicate v13, v15; Reading v03, v11, v13, v15); INV-071 (Predicate v13, v15; Reading v11–v13, v15); INV-088 (Predicate v13, v14, v15; Reading v10, v13–v15; Notes v14, v15); INV-104 (Predicate v01–v03, v13–v15; Reading v01–v03, v10, v13–v15); INV-109 (new v11; v13, v14, v15).<br>**E-051** Conformance (v01, v11–v16), Definition (v01, v15), Notes (v05, v11, v15); **E-055** Conformance (v02, v11, v13–v15); **E-062** Conformance (v02, v12, v14); **E-045** Meaning and Notes, **E-046** Conformance, **E-012** Notes and Evidence (v13).<br>Rows **OUT-020**, **OUT-021**, **OUT-023**, **OUT-024**, **OUT-031**, **OUT-034** | v13, v14, v15 (and earlier) | **v13:** headache-type scope `allTypes` in INV-062 (acute branch), INV-069, INV-071, INV-104, INV-105 and INV-109 (INV-039: next rows); the cluster subtype scope `scopeFor(c, …, c3_1)` in INV-088; functional-impact scope in INV-104.<br>**v14:** period: the span of the course (INV-109), the covered period (INV-104, INV-088).<br>**v15:** formulation: `summarisesMedication` in INV-062 (three acute branches), INV-069, INV-071 (per-phase conjunct), INV-088, INV-104 and INV-109. | R13-01 and fix-13 other changes 1–2; R14-02; R15-01 | **Convergent** (Findings, D).<br>• One dimension per iteration; no dimension revisited.<br>• Every change adds a conjunct or replaces `s.drug = m.drug` by a predicate that implies it.<br>• R11-02's per-drug, per-period requirement, R09-01's type scope of deciding values and R02-06 (INV-076) are kept; the watch-point-2 terms are equal (step 7). |
| **INV-066 / E-047** adherence window: INV-066 (v15); E-047 Conformance (v11, v12, v15), Definition (v15: `adherenceFor`); the adherence conjuncts of INV-104 and INV-109 (v15); row **OUT-039** (v02, v11, v12, v15) | v11, v12, v15 | **v11, v12:** co-presence and wording (fix-11 and fix-12 sweeps).<br>**v15:** the window contains the on-treatment period it ends with (`a.window.start ≤ p.start`, new); the same window for the adherence of INV-104 and INV-109. | fix-11 and fix-12 sweeps; R15-02 | **Convergent.** First change of the window since v00. One window still suffices (E-047 Notes; review 16 "checked and not raised"). INV-067 is unchanged. |
| **E-041** EvaluationRule: Definition (v01, v06, v07, v08, v12, v14), Meaning, Evidence and Notes (v14 among others); `excludes` declaration (v07, v08, v14); the const list and `evaluationRules` (v01, v07, v14); `ruleTr73` (new, v14).<br>**INV-055** Reading and Notes, **INV-059** Reading (v14 among others); **E-043** Notes (v14); **ISS-10** Effect on the model (v06, v07, v12, v14); row **OUT-018** (v14 among others) | v01, v02, v06, v07, v08, v12, v14 | **v01–v12:** see the iteration-08 and iteration-12 checks.<br>**v14:** new rule `ruleTr73` (Turkish section 7.3: at least two administrations, from the end of the second cycle, `atLeastOffset`). The `excludes` criterion now excludes only from a rule named for all preventive treatment; a type-specific rule is itself a time point and excludes nothing. Readings and Notes aligned; 7.1 statements listed as not time points; completeness statements now name the protocol's interventional chapter. | R14-01 (new evidence: [S-035] section 7.3, PDF p. 86, never read before) | **Convergent** (Findings, C).<br>• No stated `excludes` value, timing, age, `AgeCoverage` value or anchor changed.<br>• The three wordings are nested (step 4): the excluded sets only narrow, toward the stated values.<br>• R14-01's option (b) (7.3 not a time point) was not taken, and no remark argues for it. |
| **INV-098** paediatric caveat: Predicate, Reading and Notes (v12, v13); **E-008** Notes (v13 among others); row **OUT-036** (v12, v13) | v12, v13 | **v11:** a subject who is a child on the as-of date ⇒ every view.<br>**v12 (sweep):** a view whose covered period begins in childhood.<br>**v13:** a view that shows any period beginning in childhood, or an instrument result completed in childhood. | fix-12 time-frame sweep; R13-02 | **Convergent** (Findings, E). The antecedent widened twice in one direction; the v12 case is kept explicitly. |
| **INV-039** (Predicate, Reading v02, v12, v13); **E-023** Conformance (v10, v12, v13); row **OUT-010** (v02, v11, v13) | v02, v12, v13 | **v13:** intensity summaries of compared periods over all headache types combined. | R02-02 (b) (earlier); fix-12 sweep; R13-01 | **Convergent.** Addition only. |
| **E-065**, **INV-011** Reading (v08, v12, v13), new **INV-110** (v13); rows **OUT-001** (v04, v11, v12, v13), **OUT-032** (v12, v13) | v12, v13 | **v12:** completeness for the trigger view (R12-02 sweep).<br>**v13:** dates shown by the trigger view lie in its covered period (INV-110); the INV-011 Reading points to it. | R12-02; R13-03 | **Convergent.** INV-110 supplies the premise that the v12 Reading already stated. |
| Header; introductions of sections 9, 11 and 12 | every version | Version line, "as of vNN", one search-log paragraph and one change-log entry per version. | — | Bookkeeping, not applicable. |
| Items whose changes all lie in v00–v12 and that are unchanged since. Examples: E-008 Definition (all v12 time-frame components); INV-001; INV-003, INV-054, INV-056, INV-078, E-040; INV-086, INV-087, E-060, E-061; INV-049, INV-050, E-039; INV-063, INV-064; INV-060, INV-061, INV-068, INV-070, INV-072 to INV-074, INV-089, INV-091 to INV-093 | within v00–v12 | See check-after-iter-04, check-after-iter-08 and check-after-iter-12. | as there | Convergent (earlier checks). Unchanged in v13–v16. |

## Recurring remark topics

| Topic (IDs) | Remarks | Pattern | Assessment |
|---|---|---|---|
| **One identifying property of a required item left open** (INV-062, INV-066, INV-069, INV-071, INV-088, INV-104, INV-105, INV-109; E-047, E-051, E-055) | R13-01, R14-02, R15-01, R15-02, R15-03, R16-01; R13-03 (dates of a view) is of a related kind; fix 13 and fix 14 "noted, not changed" (formulation) | Each remark names a different dimension, or a different alternative of INV-105:<br>• headache-type scope (R13-01, v13);<br>• period (R14-02, v14);<br>• formulation (R15-01), adherence window (R15-02) and the comparison's course in INV-105 (R15-03), all in v15;<br>• the acute course in INV-105 (R16-01, v16).<br>Fix 15 then ran an identifying-property check over all 81 invariants with a presence requirement. R16-01 found one residual gap, in the drug tie that fix 15 had itself added to INV-105, which was history-wide. Fix 16 searched for the same pattern elsewhere and found none.<br>Counts per iteration (13 → 16):<br>• remarks of this class: 1 (+ R13-03), 1, 3, 1;<br>• predicates changed: 8, 4, 8, 1;<br>• model items changed: 21, 12, 12, 3.<br>Every remark states the earlier ties it keeps, and every guarantee term is kept (step 7). | **Converging, not cycling.** No dimension was reopened, and no tie was loosened. The findings narrow from many invariants (R13-01: eight predicates) to one conjunct of one invariant (R16-01). Findings D. |
| **Overview treatment effect** (INV-105, E-067, OUT-035) | R13-01 (optional item), R14-02 (d), R15-01 (optional item), R15-03, R16-01; fix-15 other change 1 | Five remarks in four iterations on one conjunct, each on a dimension or alternative not yet tied:<br>• type scope;<br>• period;<br>• drug and formulation;<br>• the course of the comparison and of the preventive antecedent;<br>• the acute course and the acute antecedent.<br>Each keeps the "one item suffices" decision (fix 11; review 13 "settled"; R15-03 "One item still suffices"; R16-01; fix 16). | Convergent (Findings, A and B). The most active item of iterations 13–16 (watch point 1). |
| **Formulation of a required acute summary** (E-051, INV-062, INV-069, INV-071, INV-088, INV-104, INV-105, INV-109) | fix 13 (noted), fix 14 (noted; the optional INV-109 formulation condition of R14-02 not adopted), R15-01 | Left open twice for a stated reason ("a disjunction of the two would fit neither reading exactly"). R15-01 showed that a weaker condition implied by both readings closes the gap without deciding the reading, and fix 15 adopted it. The reading question itself stays open and is stated in the E-051 Notes. | Convergent. A deferral resolved in one direction. It was never a declined remark, so PROCESS section 9 was not engaged. |
| **Responder labels** (E-045, E-046, INV-062, INV-063, E-012) | R13-01 (acute branch), R15-01 (acute branches) | INV-062 gained the type scope (v13) and `summarisesMedication` (v15) in its acute branches only. INV-063 and INV-064 are unchanged since v12 and v05, and E-045 and E-046 changed only in v13 text. | Convergent (watch point 2). |
| **Evaluation time points** (E-041, INV-055, INV-058, INV-059; OUT-018) | R01-01, R01-02, R02-01, R06-01, R07-01 to R07-03, R08b-02, R14-01 | R14-01 is the third remark that found a time point missing from the list (after R01-01 and R07-01), each fixed by adding a rule on new evidence. The `excludes` criterion was rewritten a second time (after R08b-02), with no value changed. | Convergent (Findings, C; watch point 1). |
| **Paediatric caveat** (INV-098, E-008, OUT-036) | fix-12 sweep, R13-02 | Trigger widened twice in one direction. | Convergent (Findings, E). |
| **Dates and periods of shown content** (E-065, INV-110, INV-011; OUT-001, OUT-003, OUT-032) | R12-02, R13-03 | Additions only. | Convergent. |

**Settled points.** Reviews 13 to 16 list these as "not reopened (no new evidence)". Every item behind them is unchanged in v13–v16, or changed only on another dimension (marked):
- INV-106 at MUST NOT; INV-023 at any granularity; the "> 3 months" readings of INV-045 and INV-089;
- the E-041 window readings, timings, ages and `excludes` values (only the criterion text changed, Findings C);
- `ruleRuChildren`; INV-091 to INV-093 with `concerns`;
- the MIDAS labels and the Grade IV subdivision; the HIT-6 one-month recall; "baseline administration" as any earlier administration;
- R10b-01 and the R11-01 (a)/(b) derivation (INV-003, INV-054, INV-056 unchanged since v12 and v11);
- INV-060 with INV-061 for compared periods shorter than 28 days; the monthly baseline (R01-03); the baseline of the post-stop view (INV-070, never changed);
- "treatment effect" by one item (INV-105: ties added on other dimensions, Findings A);
- INV-087 and the lead-in (unchanged since v04); INV-049 and INV-050 (unchanged since v12 and v10); the E-008 time frames (E-008 Definition unchanged since v12);
- the period of a cluster attack rate within its bout (INV-089, unchanged since v09); several stop events in one course (INV-001, unchanged since v12);
- new in iterations 15–16: one adherence window per comparison (E-047 Notes, v15), and the periods of the overview's response comparison not tied to the covered period (R15-03, fix 15, review 16).

**Remark counts per iteration:** 12, 7, 7, 4, 3, 1, 3, 0 + 2, 1, 0 + 2, 3, 2, 3, 2, 3, 1.

## Findings

None.

No item oscillates, so nothing is frozen, FROZEN_ITEMS.md is not written and OUTPUT_MODEL.md is not changed. Five points come closest to a back-and-forth pattern; each is assessed below.

### A. INV-105, the treatment-effect conjunct (v13 to v16)

**Trace of the conjunct** (antecedent ⇒ consequent):
- v00: `preventiveTreatments ≠ ∅ ∨ acuteMedications ≠ ∅` ⇒ `∃ x ∈ v.content • x ∈ ResponseComparison ∪ AcuteTreatmentSummary`.
- v02 (fix 02, item 9): the preventive part becomes `∃ t • startOf(ctx, t) ≠ ∅`.
- v13 (R13-01): the acute alternative requires `s.typeScope = allTypes`.
- v14 (R14-02 (d)): it also requires `within(s.period, v.covers)`.
- v15 (R15-03; R15-01 optional item; fix-15 other change 1):
  - the preventive part becomes `courseOverlaps(ctx, t, v.covers)`;
  - the comparison alternative requires `courseOverlaps(ctx, rc.treatment, v.covers)`;
  - the acute alternative requires `m ∈ ctx.subject.acuteMedications ∧ summarisesMedication(s, m)`.
- v16 (R16-01):
  - the acute part becomes `∃ t ∈ ctx.subject.acuteTreatments • courseNotOutside(ctx, t, v.covers)`;
  - the acute alternative also requires `∃ t ∈ ctx.subject.acuteTreatments • drugOf(t) = m.drug ∧ courseNotOutside(ctx, t, s.period)`.

**Scenario script** (`inv105.py`; 4,000 random contexts, 290,049 context–item pairs):
- **The antecedent never goes from false to true** between consecutive formulas. It only narrows: v00 ⊇ v02 ⊇ v15 ⊇ v16 (v13 and v14 equal v02).
- **No item goes from rejected to accepted.** The set of items that meet the consequent only shrinks.
- **"One item" is kept.** The consequent is an existential disjunction in every version; no version asks for an item per treatment.
- **Conformance of an output.** In 587 of the 4,000 contexts, the conformance of some output to the conjunct returns. For example, an overview whose only treatment-effect item is the comparison of a preventive treatment stopped years before the covered period:
  - conforming v00–v14;
  - not conforming in v15;
  - conforming in v16.

  In every one of these cases the output conforms again **because the requirement itself lapses** in that context, not because an item is accepted again. These are the contexts in which no preventive course overlaps the covered period and no acute course lies in it. The patterns, over the formulas of v00, v02, v13, v14, v15 and v16:

  | Output conforms | Requirement in force | Count |
  |---|---|---|
  | `YY...Y` | `RRRRR.` | 14,580 |
  | `YYYY.Y` | `RRRRR.` | 7,290 |
  | `YY..YY` | `RRRR..` | 6,552 |
  | `YYY..Y` | `RRRRR.` | 4,848 |
  | `YYY.YY` | `RRRR..` | 2,184 |

**Why it is not an oscillation:**
1. **No dimension changed twice in opposite directions.** Each version ties one more dimension: type scope, period, drug and formulation, the course of the comparison, the course of the acute summary. v16 keeps every v13–v15 conjunct verbatim; only `acuteMedications ≠ ∅` in the antecedent is replaced (Findings, B).
2. **The antecedent narrowings share one ground, stated each time:**
   - fix 02: "treatment effect only where it can exist";
   - fix 15: "so that the conjunct is required … exactly where such a treatment exists";
   - R16-01 (ii) and fix 16: the same restriction, for the acute part.

   They are the counterpart of the consequent ties. Once a stale comparison or a stale summary no longer counts as the effect of the covered period, a context with no treatment in that period has no admissible item, and the requirement is lifted there.
3. **No remark argues the other side.** No review or fix asked to keep a treatment effect for a period in which no treatment is followed, or to admit an item of another period. R15-03 and R16-01 each state that they keep the fix-11 "one item" decision and the earlier ties.
4. **Did any change undo an earlier one?**
   - **The antecedent.** v15 and v16 narrow it, as v02 did; none widens it.
   - **"One item suffices".** It is unchanged.
   - **R16-01 and fix 15.** R16-01 tightens the drug tie that fix 15 added ("an acute medication the subject has used"); it does not remove it. `summarisesMedication(s, m)` stays.
   - **Undated courses.** Fix 16's choice to count an acute course without a stated start as started is new. It is consistent with the v00–v15 acute antecedent, which never required a start, and with the INV-109 Notes on undated acute courses.

**Judgement:** convergent, monotone refinement in one direction. INV-105 is the most-changed item of iterations 13–16 (watch point 1).

### B. INV-105's acute antecedent and the time frame of `acuteMedications` (v11 → v12 → v16)

**Trace:**
- **v00–v11.** E-008 declared `acuteMedications` "the acute medications (drug and formulation) the subject uses", with no time frame. R12-01 reports that the fix-11 log read it as current: "An acute line whose drug is no longer among `acuteMedications` can refer to a summary with 0 attacks." Fix 02 (item 9) paraphrased the INV-105 antecedent as "the subject uses acute medication".
- **v12 (R12-01, option (a)).** "every acute medication … the subject has used at any time up to the as-of date". R12-01 listed INV-023, INV-024, INV-028, INV-044, INV-046, INV-062, INV-068, INV-069, INV-071, INV-088 and INV-104, but not INV-105. Fix 12 does not mention the INV-105 treatment effect. So the INV-105 antecedent became history-wide without its own text changing.
- **v16 (R16-01 (ii)).** The acute part becomes "an acute treatment course that the context does not place outside the covered period". E-008 stays history-wide (byte-identical since v12).

**Scenario script** (`inv105ant.py`; 20,000 random contexts; antecedent over v00, v02, v11, v12, v15, v16):
- **v00–v11 read as "used at any time".** No context sees the requirement return.
- **v00–v11 read as "in use on the as-of date"** (the fix-11 reading). The requirement returns in 2,510 contexts:
  - `...RR.` (859): a subject whose acute courses all ended before the covered period, with no started preventive treatment. Not required up to v11, required v12–v15, not required in v16.
  - `R..RR.` (662): the same, where the subject also has a preventive treatment that has not started; the v00 requirement came from that treatment and was removed in v02.
  - `R..RRR` (989): an unstarted preventive treatment (v00) and an acute course in the covered period that has ended by the as-of date (v12 onward). The two R states have different grounds.

**Why it is not an oscillation:**
1. **The item did not return to an earlier state.**
   - The v16 antecedent is neither "in use on the as-of date" (v11 under the fix-11 reading) nor "used at any time" (v12). It is a period-based condition.
   - It differs from the v11 reading wherever a course overlaps the covered period but has ended by the as-of date: v16 requires a treatment effect there, and the v11 reading did not.
   - The INV-105 text never returns to an earlier form.
2. **Different points, no competing positions.**
   - v12 decided the time frame of a subject property, to repair INV-023, INV-024 and INV-044 to INV-046. That repair is kept: E-008 is unchanged, and INV-071, INV-088 and INV-104 still ask for every medication used up to the as-of date.
   - Its effect on INV-105 was not examined by R12-01 or fix 12. No remark or fix ever argued that a patient whose acute use has ended should be shown a treatment effect for a later period.
   - The only argued positions (fix 02; fix 15; R16-01 and fix 16) all point the same way: a treatment effect only where one of the covered period can be shown.
3. **The return depends on a reading** of the v00–v11 text that R12-01 itself called unstated. Under the other reading of that text, the antecedent changes at most once.

**Judgement:** convergent, but this is the nearest approach to A → B → A in iterations 13–16. A change that makes INV-105's acute antecedent history-wide again (for example `acuteMedications ≠ ∅`, on R12-01's ground) would be a real return and should be frozen (watch point 2).

### C. E-041: the `excludes` criterion wording in v07, v08 and v14

**Trace.**
- **v07 (R07-02).** `excludes` was added with its values. Its comment: "the types for which the same guidance names another time point".
- **v08 (R08b-02).** The comment and the Notes criterion: a type is excluded when the same guidance gives it, in a rule of its own for the type, a time point after this rule's time point or window. The Notes added: "every rule named for particular types excludes nothing, because its guidance gives these types no later time point of its own".
- **v14 (R14-01).**
  - The criterion applies "for a rule named for all preventive treatment", with "∅ for a rule named for particular types".
  - The reason given for type-specific rules became "it is itself a time point that its guidance names for these types". With `ruleTr73` (7.3) and `ruleTr3639` (3.6.3.9) in one guidance, the v08 reason no longer held.

**Script results** (`excl16.py`, step 4):
- **Values.** Every stated value is unchanged since it was set.
- **What each wording gives.**
  - The v07 comment, read literally, never matched the values; this was R08b-02's defect.
  - The v08 criterion matches all 17 values of v08–v13. Applied to v14 it would make `ruleTr73` exclude onabotulinumtoxinA, so that the rule applies to no treatment, as R14-01 foresaw.
  - The v14 criterion matches all 18 values of v14–v16, and also all 17 values of v07–v13.
- **Nesting.** For every rule of every version, what v14 excludes ⊆ what v08 excludes ⊆ what v07 excludes.

**Why it is not an oscillation:**
1. **Values constant, wording monotone.** The three wordings narrow monotonically toward a fixed set of values; none widens again what an earlier one narrowed.
2. **Each step rests on its own evidence.**
   - v08: R08b-02, the TA260 12-week interval against the [S-035] 3-monthly injections.
   - v14: R14-01, [S-035] section 7.3, PDF p. 86, a passage no earlier loop file had read.
3. **Watch-point items untouched.** `ruleNice1327.excludes`, `ruleTrBox8.excludes`, every `timing`, `ages`, `AgeCoverage` value and anchor are unchanged (iteration-08 watch points 1 and 8; iteration-12 watch point 1). The age is still read on the treatment start.
4. **The aligned Readings narrow the same way.** INV-055 and INV-059 Readings, the INV-055 Notes and row OUT-018 now limit the displacement rule to rules named for all preventive treatment. "a later time point of its own" occurs 4 times in every version from v08 to v16.

**Judgement:** convergent. The values have been unchanged since v07, and the wording was corrected twice in one direction (watch point 5).

### D. The "one identifying property left open" remark class

The question is whether this class is converging or cycling. The facts:
- **Dimensions.** Type scope (R13-01) → period (R14-02) → formulation, adherence window, course of the comparison (R15-01, R15-02, R15-03) → course of the acute summary (R16-01). Each dimension was tied once and never loosened. The guarantee terms only increase (step 7).
- **Breadth.** R13-01 named five invariants plus two optional ones, and the fix touched eight predicates. R14-02 touched four, R15-01 to R15-03 together eight, and R16-01 one conjunct of one invariant.
- **Systematic check.** Fix 15 checked every invariant with a presence requirement (81) for identifying properties that Stage 1 fixes. R16-01 is a residual in the one item whose tie fix 15 added itself (the drug of the overview's acute summary, tied only to a history-wide set). Fix 16 searched the rest of the model for the same pattern (a history-wide set that one item can discharge) and found none: the other uses are universal per-medication requirements, met by 0-attack summaries.
- **No remark undoes another.** Each remark of the class cites the earlier ties it keeps (R13-01: R02-06, R09-01, R11-02; R14-02: R11-02, R13-01; R15-01: R11-02, R13-01, R14-02; R15-02, R15-03: R14-02; R16-01: fix 15, v14, v15).

**Judgement:** converging. The remark count is 1, 1, 3, 1 and the number of affected predicates is 8, 4, 8, 1. The findings are narrowing from whole families of invariants to a single conjunct, and none returns to a dimension already tied. Another remark of this class on INV-105, or on a dimension already tied, should be read as cycling (watch point 1).

### E. INV-098: the paediatric caveat trigger widened twice (v12, v13)

- v11: `ctx.subject.ageGroup = childOrAdolescent ⇒ ∀ v : View • annotated(v, supportiveInformation)`.
- v12: `childOn(ctx, v.covers.start)`.
- v13: `childIn(ctx, {v.covers} ∪ (v.content ∩ Period)) ∨ ∃ r, d • childOn(ctx, d)`.

**Why it is not an oscillation:**
- **v12 includes v11.** A subject who is a child on the as-of date is a child on the first day of every covered period that begins by then.
- **v13 includes v12.** `v.covers` is named in the set.
- **The text keeps the earlier case.** The v13 Reading keeps "this includes every view whose covered period begins while the subject is a child or adolescent".
- **Watch point 6 untouched.** No remark asks to read the age on the as-of date again.

**Judgement:** convergent.

## Things the next checker should watch

1. **INV-105, the treatment-effect conjunct** (E-067; E-051 Conformance; row OUT-035). It changed in every iteration from 13 to 16. Treat any of the following as oscillation unless it rests on evidence that R13-01, R14-02, R15-01, R15-03, R16-01 and fixes 02, 11 and 13–16 did not consider:
   - dropping or weakening `allTypes`, `within(s.period, v.covers)`, `summarisesMedication`, `courseOverlaps` or `courseNotOutside` in the alternatives;
   - widening the antecedent again: the preventive part back to any started treatment, or the acute part back to `acuteMedications ≠ ∅` (Findings, B);
   - requiring a treatment-effect item per treatment, against the "one item" decision (fix 11, settled in reviews 13–16);
   - reversing fix 16's choice that an acute course without a stated start counts as started, or extending it to preventive courses (a comparison needs a start, INV-056);
   - requiring R15-03's option (b) (the most recently started treatment), which fix 15 did not adopt for want of a Stage 1 basis;
   - tying the comparison's own periods to the covered period, which R15-03, fix 15 and review 16 left free.

   A further remark that finds a new free dimension of this conjunct should be checked for whether that dimension was already tied in v13–v16. If it was, the remark class is cycling.
2. **History-wide `acuteMedications` in antecedents.** R12-01 made `acuteMedications` history-wide in v12. Two presence conditions still depend on it as a whole: E-062 `acute` ("SHOULD when ctx.subject.acuteMedications ≠ ∅") and E-045 `valueAvailable` for acute effectiveness. A remark that narrows either to the covered period would follow the same path as Findings B (F → T → F under the v11 as-of reading). Such a change should:
   - keep E-008 history-wide;
   - use a period-based condition, as `courseNotOutside` does;
   - keep the per-medication requirements of INV-071, INV-088 and INV-104.

   Any change of E-008 `acuteMedications` back to the medications in use on the as-of date would reverse R12-01 and should be frozen.
3. **Identity ties of required acute summaries and adherence** (INV-062, INV-066, INV-069, INV-071, INV-088, INV-104, INV-109; E-047, E-051, E-055).
   - **Reversal.** Loosening the type scope (R13-01), the period (R14-02), `summarisesMedication` (R15-01) or `adherenceFor` (R15-02) would reverse a fix.
   - **New decision, not a reversal.** Deciding the OUT-023 reading (per drug or per drug and formulation; E-051 Notes, "Formulation of a required summary") would be a new decision. It must keep a condition that implies `summarisesMedication`.
   - **Rejected options.** Fix 16 rejected `allFormulations ∨ treatedAttacks > 0`; fix 15 kept one adherence window and chose R15-02's option (a) over (b). Re-raising these needs new evidence.
4. **Responder labels** (E-045, E-046, INV-062, INV-063, E-012). Every reversal listed in iteration-12 watch point 2 still applies. Since v13 the acute branches of INV-062 also carry `allTypes` and `summarisesMedication`, and removing either would reverse R13-01 or R15-01.
5. **E-041.** The `excludes` values have been unchanged since v07, and the criterion was narrowed in v08 and v14. `ruleTr73` is new in v14. Treat as oscillation, unless it rests on evidence beyond R08b-02 and R14-01:
   - any change of an `excludes` value;
   - a criterion that again excludes from a type-specific rule, so that `ruleTr73` would apply to no treatment, or that widens the excluded set again (for example back to "another time point");
   - removing `ruleTr73` (R14-01's option (b), not taken);
   - any change of a `timing`, `ages`, `AgeCoverage` value or anchor;
   - a return to reading the age on the as-of date.
6. **INV-098.** Narrowing the trigger back to the first day of the covered period, or to the as-of date, would reverse R13-02 or the v12 sweep.
7. **Earlier watch points still open, all unchanged in v13–v16:**
   - co-presence (INV-003, INV-054, INV-056, INV-078, E-040; R10b-01 and the R11-01 (a)/(b) derivation);
   - the menstrual-relation view (INV-086, INV-087, E-060, E-061, the lead-in; the INV-105 cycle-line conjunct);
   - withdrawal follow-up (INV-049, INV-050, E-039);
   - the E-008 time-frame components of v12.

   The reversal triggers of iteration-12 watch points 3 to 6 still apply.
8. **Change volume.**
   - Items changed per version: 110, 73, 90 and 28 in v13–v16, after the peak of 264 in v12.
   - Top-level items changed: 21, 12, 12 and 3; predicates changed: 10, 4, 8 and 1.
   - Remark counts: 3, 2, 3 and 1.
   - No fixer ran a whole-model rewording sweep in v13–v16; fix 15 ran a check that changed only the items it found.

   A rise in volume driven by a sweep, or a remark count that stops falling while the remarks stay on INV-105, should be examined for cycling.

## Conclusion

No item of the model oscillates after sixteen iterations, and nothing is frozen.

- **Returns.** The only item that returns to an earlier state is `aged12OrOlder` (added in v06, removed in v12), which the iteration-12 check assessed. No element, attribute, field, invariant, rule or criterion constant, source, section, value set, conformance level, Realises field or traceability row returns to an earlier state in v13–v16.
- **INV-105.** The treatment-effect conjunct changed in v13, v14, v15 and v16, each time on a new dimension and in one direction:
  - the antecedent only narrowed, on the fix-02 ground "only where it can exist", now read for the covered period;
  - the alternatives only gained ties;
  - "one item suffices" holds in every version;
  - the antecedent changed in v16 without undoing any earlier change.

  The nearest approach to A → B → A is reading-dependent and has no competing positions (Findings, B). It is the first watch point.
- **E-041 `excludes`.** Every rule value is unchanged since v07. The three wordings (v07, v08, v14) are nested, each narrower than the one before, and the v14 wording reproduces all 18 values.
- **The "one identifying property left open" class** is converging. It tied one new dimension per iteration and never loosened one. The findings narrowed from eight predicates (v13) to one conjunct (v16).
- **Change volume:** 110, 73, 90 and 28 items in v13–v16, against 264 in v12. **Remark counts:** 12, 7, 7, 4, 3, 1, 3, 0 + 2, 1, 0 + 2, 3, 2, 3, 2, 3, 1.

The scripts used are in the session scratchpad (`osc16/`): `split.py`, `analyse.py`, `volume.py`, `multi16.py`, `rules.py`, `excl16.py`, `exclnotes.py`, `conf.py`, `attrtypes.py`, `ngram.py`, `docwide.py`, `dels16.py`, `show.py`, `show3.py`, `guar16.py`, `ids16.py`, `wp16.py`, `remarks16.py`, `inv105.py` and `inv105ant.py`. FROZEN_ITEMS.md was not written, and OUTPUT_MODEL.md and the history snapshots were not changed.
