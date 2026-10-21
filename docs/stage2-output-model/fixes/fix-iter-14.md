# Fix log — iteration 14
Input review: reviews/review-iter-14.md · Input version: v13 · Output version: v14
Date: 2026-10-21

## What was read and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3;
- v13 (`OUTPUT_MODEL.md`, byte-identical to `history/v13.md`);
- review 14.

**Earlier loop files read, so that no fix is undone:**
- fix logs 07 (R07-02, the `excludes` component; the completeness sweep of the rule list, which read the Turkish protocol's sections 3.6.2, 3.6.3 and 6, not its chapter 7), 08 (R08b-02, the stated `excludes` criterion) and 13 (R13-01 type scopes; the open point on the formulation scope);
- review 08b, remark R08b-02;
- the oscillation check after iteration 12, with its seven watch points.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**Downloads.** [S-035], the Turkish Ministry of Health Migraine Clinical Protocol (Stage 1 URL), was downloaded with `curl` into the fresh directory `/tmp/fix14-dl-lpwJ`, outside the repository: HTTP 200, 1,310,852 bytes, 92 pages, PDF created 28 August 2025. All 92 pages were extracted with `pdftotext -raw`, and the key pages also with `-layout`. Pages 57, 82, 83 and 86 were rendered with `pdftoppm` and read by eye.

**Scripts.** All are in the session scratchpad (`fix14/`) and were run with `python3 -I`:
- `quotes.py` and `quotes_en.py`: every quoted fragment that is new in v14, checked against the page texts or against Stage 1 v18;
- `mech.py`: headings, references, traceability, invariant levels, the typing rule and attribute declarations (run on v13 and v14);
- `rules.py`: the rule constants of v13 and v14, compared component by component;
- `omndiff.py`: the `omn` lines changed between v13 and v14, and the names they use;
- `scope.py`: the scope-term sweep.

### Verification of the remarks

**R14-01 holds.**
- **Section 7.3, PDF p. 86.** Text layer and rendered page agree. The section is headed "7.3. Botulinum Toksin Enjeksiyonu", in chapter "7. MİGRENDE GİRİŞİMSEL İŞLEMLER". Its items read:
  - "Uygulanım yeri ve dozu: … 31 nokta, her noktaya 5 ünite (toplam 155 ünite), 3 ay aralıklarla,"
  - "Etkisini değerlendirmek için en az 2 k ez uygulanmalıdır," The space inside "kez" is printed on the page.
  - "Bir yılın sonunda … uygulama süreleri uzatılabilir."
- **Never accounted for.** No loop file mentions this passage. fix-iter-07 lists the Turkish sections it read (3.6.2, 3.6.3, 6), and chapter 7 is not among them.
- **It counts as a time point.** The model's own precedents treat a minimum before evaluating as an evaluation time point (`atLeastOffset`): AAN/AHS 14B "wait 24 weeks … before assessing efficacy", the Russian "минимум через 6 месяцев", EHF "a minimum of 3 consecutive months" and IHS Q2 "a minimum of …". Option (b), which would list 7.3 as not a time point, would contradict them.
- **The drug.** The botulinum toxin of 7.3 is given at 155 units over 31 points. Section 3.6.3.9 (PDF p. 57) gives the same dose for onabotulinumtoxin A: "standardize edilmiş 31 adet noktaya toplamda 155 ünite onabotulinum toksin A". So the rule is named for `onabotulinumtoxinA`.
- **Completeness sweep.** I searched all 92 pages for "değerlendir", "en az", "ay sonra", "hafta sonra", "siklus" and counts of months and weeks. Beyond the items already in E-041, chapter 7 holds only:
  - the greater occipital nerve block schedule (7.1, p. 83: "Başlangıçta haftalık 4 kez sonra aylık …");
  - the check right after a block that it has taken effect (7.1, p. 83).
  
  Neither is an evaluation time point of a treatment's response against baseline. No other part of the protocol names a missing time point.

**R14-02 holds.** The v13 predicates fix no period:
- INV-109 (with INV-079) requires only `s.drug = l.drug` and one summary with `s.typeScope = allTypes`;
- INV-104 requires `s.drug = m.drug ∧ s.typeScope = allTypes`;
- INV-088 requires drug, scope, the 15-minute time point and the rescue outcome;
- INV-105 requires any all-types summary.

A summary of a period without treated attacks satisfies INV-072 to INV-074. I reproduced the review's examples against v13:
- the sumatriptan line (course 2020–2021) with a September 2026 summary of 0 attacks;
- a clinician-facing summary of 15 August – 20 October 2026, and a cluster view of January – March 2026, each with March 2019 summaries.

All three satisfy v13. All three are excluded in v14.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R14-01 | fixed: the review's option (a), with the `excludes` criterion refined as the review and the orchestrator allow; every existing rule value unchanged | E-041 (Definition: new `ruleTr73`, `evaluationRules`, `excludes` comment; Meaning; Evidence; Notes); E-043 Notes; INV-055 Reading and Notes; INV-059 Reading; row OUT-018; ISS-10 (Effect on the model); section 11 | **New rule** `ruleTr73`:<br>• guidance "Turkish Ministry of Health Migraine Clinical Protocol 2025, section 7.3 (botulinum toxin injection)";<br>• `c1`, `anyAge` (no age is stated, as for Box 8 and 3.6.3.9);<br>• `{onabotulinumtoxinA}`, anchored at `endOfCycleAnchor(2)`, `atLeastOffset`, `weeks(0)`, `maxOffset ∅`.<br>**Reading.** Each administration begins a cycle, and the effect of the second one is evaluated once its cycle has ended. The model reads NICE 1.3.29 "after 2 treatment cycles" the same way. "en az" (at least) gives `atLeastOffset`.<br>**Evidence.** Three new [S-035] quotes, with translations: 7.3 items 3 and 4, and the 3.6.3.9 dose sentence. The chapter heading names migraine.<br>**`excludes` — the criterion as written.** It would give `ruleTr73.excludes = {onabotulinumtoxinA}`, because 3.6.3.9 gives that type a later time point (after 3 cycles). The rule would then apply to no treatment.<br>**Why that result is wrong.** The criterion's own rationale is that a general rule would assess a type before "the guidance's own time point for it". Section 7.3 *is* the protocol's own botulinum statement: it names its minimum as the condition "Etkisini değerlendirmek için" (to evaluate its effect). Excluding it would drop a time point named in current guidance, which narrows OUT-018 (MUST).<br>**Refinement.** A type is excluded only from a rule named for all preventive treatment, when the same guidance gives that type a later time point in a rule for that type. A rule named for particular types is itself a time point of its guidance and excludes nothing. Where one guidance names two time points for the same type, each in a type-specific rule, neither is more specific, and the comparison is available at both.<br>**Existing values unchanged** (`rules.py`):<br>• every exclusion of v13 (14A, Russian 7.1, Box 8) is in a rule named for all preventive treatment;<br>• every type-specific rule already had ∅;<br>• the 17 earlier rule constants are byte-identical to v13;<br>• `ruleNice1327.excludes`, `ruleTrBox8.excludes`, every `timing`, `ages` and `AgeCoverage` are unchanged.<br>Box 8's exclusion is now also supported by 7.3 (about 6 months, after its 2–3-month window).<br>**Paraphrases aligned** (the R08b-02 / R10b-02 class), each now limited to rules named for all preventive treatment:<br>• the `excludes` comment, the E-041 Meaning and Notes;<br>• the INV-055 Reading and Notes, the INV-059 Reading and row OUT-018.<br>The E-008 Notes and the INV-001 Reading already speak of the rules named for all preventive types, and the E-043 sentence describes only excluded types, so they were left unchanged. The INV-058 Reading states no criterion.<br>**As the review asked:**<br>• the "every rule except NICE 1.3.29 and Turkish 3.6.3.9" sentences now include 7.3 (E-041 Notes, E-043 Notes, INV-055 Notes);<br>• the 7.3 interval statement (fifth item) is added, with its quote, to "course lengths and injection intervals";<br>• the completeness statements (E-041 Notes, row OUT-018) name the protocol's chapters on pharmacological and on interventional treatment;<br>• ISS-10 no longer says the list has been complete since v07 (7.3 was added in v14). |
| R14-02 | fixed: the review's options (a) to (d) | INV-109 (Predicate, Reading, Notes); INV-104 (Predicate, Reading, Notes); INV-088 (Predicate, Reading, new Notes); INV-105 (Predicate, Reading, Notes); Conformance of E-051, E-055 and E-062; rows OUT-024, OUT-031, OUT-034, OUT-035 | **(a) INV-109.** The all-types summary of an acute line whose treatment has a start is of the span of its course:<br>• `s.period.start` is the start;<br>• if the treatment has stopped, `s.period.end` is a stop date of the course, and the stop date the line shows where it shows one;<br>• otherwise `s.period.end` is the as-of date.<br>This is the span of the line's duration (INV-079). Basis: OUT-024 asks for "the response summary … for each treatment", listed "with start and stop dates, dose changes, treatment duration"; OUT-023 asks for effectiveness "across the attacks treated with it". The preventive counterpart is aligned to its treatment start (INV-056). For a course without a stated start (no stated span, start date or duration, E-055), the period stays unconstrained, as the review's "for an acute line of a treatment that has a start" provides.<br>**(b) INV-104.** `s.period = v.covers`, as for its acute-medication days (OUT-034 "for the period since the previous consultation (or a period chosen by the clinician)"). Past courses are shown by their lines through (a).<br>**(c) INV-088.** `s.period = v.covers`, the selected time range. Because the summary now refers to the view's covered-period atom, INV-003 also places it in the cluster view (INV-003 Notes). That is where OUT-031 reports it; the new INV-088 Notes say so.<br>**(d) INV-105.** `within(s.period, v.covers)`: the covered period or a period within it. The treatment effect is still one item (a settled point), and the response-comparison alternative is unchanged.<br>**Not adopted:** the review's optional formulation condition for INV-109, because the formulation scope stays open (Other changes, 2).<br>**Watch points kept:**<br>• the R11-02 per-drug requirement, the R13-01 type scopes, `#L.evaluated = 1` and the INV-062 period ties (INV-062 is unchanged);<br>• no E-041 value is touched by R14-02;<br>• no co-presence item of watch point 3 and no E-008 time-frame component is touched. |

## Other changes

**1. Section 7.1 of the Turkish protocol (same passage class as R14-01, chapter 7 not read before).** Two statements of section 7.1 (greater occipital nerve block, PDF p. 83) are listed in the E-041 Notes as named, but not evaluation time points, each with its quote and translation:
- the schedule "Başlangıçta haftalık 4 kez sonra aylık …", under course lengths and injection intervals;
- the check right after a block that it has taken effect ("Enjeksiyon sonrası blokajın etkinliği araştırılmalı …"). It concerns the technique of the block, not the response of a treatment against its baseline.

So the completeness statement for the protocol, chapter 7 included, rests on an account of every time it names. No rule value changed.

**2. Noted, not changed: the formulation scope of per-drug acute summaries (fix 13, "Noted, not changed").**
- **Same class, but the reading is not clear from Stage 1.** It is the same defect class as R13-01 and R14-02: a dimension of a required summary is left free. But the reading is not clear:
  - OUT-023 asks "For each acute medication" for "per-drug outcomes", and also for their separate presentation "for each formulation of the same drug";
  - the model's acute medication is a drug-and-formulation pair (E-008).

  "Per drug" would call for a summary of all formulations. "Per medication" would call for one of the medication's own formulation. A disjunction of the two would fit neither reading exactly.
- **Scope of the change.** Deciding it would also change INV-062, INV-069 and INV-071, which R14-02 does not touch.
- **Decision.** Per the orchestrator's instruction, it is left open again. The new text claims nothing about formulations. The review's optional formulation condition for INV-109 is not adopted for the same reason.

**3. Wording.** Two textual clarifications made while fixing:
- E-051 Conformance names the period that each requiring invariant fixes;
- the INV-109 Notes no longer say that the acute lines in the clinician-facing summary refer to the INV-104 summaries, which are now of the covered period. They refer to the summaries of their courses, which INV-109 places in the same view.

**No other change.**
- No element or invariant was added, withdrawn or renumbered, and no level changed.
- No watch-point item changed beyond what is stated above:
  - E-008, E-039, E-045, E-046, E-060, E-061 are byte-identical to v13;
  - so are INV-001, INV-003, INV-049, INV-050, INV-054, INV-056, INV-062, INV-063, INV-064, INV-078, INV-086, INV-087 and INV-097.
- No whole-model sweep was run.

### Satisfiability pass

Every changed invariant was checked together with the invariants that constrain the same elements and views. No admissible context (INV-001) makes the MUST and SHOULD constraints jointly unsatisfiable. No derived attribute was added or changed.

- **`ruleTr73` with INV-055, INV-056, INV-057, INV-058, INV-059, INV-066, INV-097, INV-003 and INV-011.** Take a botulinum course with start s and a `cycleEnd(2)` event a. INV-001 gives s ≤ a ≤ as-of date.
  - Where `fitsMonthlyPeriod` holds (a at least 27 days after s), INV-055 asks for an on-treatment period that ends at a. A 28-day period ending at a, with a 28-day baseline ending before s, meets INV-055 to INV-057 and INV-097. An adherence window equal to that period meets INV-066 and INV-067.
  - INV-059 shows the time point with every comparison of the treatment. INV-058 gives earliest = a and latest = ∅.
  - The 3.6.3.9 time point (end of the third cycle) can be met by the same comparison or by another one. INV-055 asks for a comparison per rule and anchor, not one comparison for all.
  - Where a lies less than 27 days after s, no comparison is required at it (as for NICE 1.3.29 and 3.6.3.9), and the time point can still be shown.
- **INV-109 with INV-079, INV-072 to INV-074, INV-076, INV-003, INV-011, INV-098 and INV-104.**
  - The course span can be shown as a period of kind `otherSpan`, which INV-002 admits for any dates in order. The dates are in order: the start precedes every course event and the as-of date (INV-001).
  - The summary lists every treated attack of the drug in the span, in order (INV-072, INV-074), or none. Its time point follows its scope (INV-073), and its lines carry symptom statuses (INV-076).
  - INV-003 shows its period in the line's view, INV-011 adds that period's completeness, and INV-098 adds an annotation where the span begins in childhood.
  - In a clinician-facing summary, the course summary and the INV-104 summary of the covered period are different atoms. No invariant limits the number of summaries per drug.
- **INV-104, INV-088 and INV-105 with INV-003, INV-011, INV-072 to INV-074.**
  - A summary whose period is the covered period (or a period within it, INV-105) refers to a period that INV-003 already shows in the view, and it may have 0 treated attacks.
  - For INV-088, `scopeFor` implies `onlyOfType`, so INV-073 gives 15 minutes, as INV-088 requires. The rescue outcome is one of `requiredOutcomes` (INV-072). INV-011 asks for the completeness of the covered period, which a view with bouts needs anyway.
- **Levels.** Unchanged:
  - INV-055 and INV-059 MUST (OUT-018);
  - INV-088 SHOULD (OUT-031);
  - INV-104 SHOULD (OUT-034);
  - INV-105 SHOULD (OUT-035);
  - INV-109 SHOULD (OUT-024).

  Each change narrows what meets a requirement. It does not change the strength of the Stage 1 part the invariant realises.

### Watch points (oscillation/check-after-iter-12.md)

1. **E-041.**
   - No change to `ruleNice1327.excludes`, `ruleTrBox8.excludes`, any `timing`, `ages` or the four `AgeCoverage` values. The age is still read on the treatment start.
   - The criterion text was refined. The refinement rests on new evidence (section 7.3, never considered by R07-02 or R08b-02) and changes no value.
   - The short Readings were aligned with it, which the check names as not oscillation.
2. **Responder labels.** Untouched. The guarantee-term counts are equal to v13 (Checks).
3. **Co-presence.** INV-003, INV-054, INV-056 and INV-078 are unchanged. The only new placement consequence is in the direction of more (INV-088 summaries in the cluster view), on an object no earlier fix removed.
4. **Menstrual-relation view and overview.** INV-086, INV-087, E-060 and E-061 are unchanged. INV-105 changed only in its acute treatment-effect alternative.
5. **Withdrawal follow-up.** Unchanged.
6. **E-008 time-frame components.** Unchanged.
7. **Change volume.** No sweep was run. This version changes:
   - 5 elements (E-041, E-043, E-051, E-055, E-062);
   - 6 invariants (INV-055, INV-059, INV-088, INV-104, INV-105, INV-109);
   - 1 Stage 1 issue (ISS-10);
   - 5 traceability rows (OUT-018, OUT-024, OUT-031, OUT-034, OUT-035);
   - the header and sections 9, 11 and 12.

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-11; ISS-07 appears only as withdrawn. |
| References | No dangling E-, INV- or ISS- reference. S references lie in S-001–S-046 and S-101–S-106; every S-1NN has a row in section 10. OUT references lie in 001–039. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025). Exactly one Realises and one Conformance field per item. Each row's E and INV columns equal the union of the Realises fields (no Realises field changed). All rows say "full". |
| Types and names | Every name in the changed `omn` lines is declared: `ruleTr73`, `startOf`, `stopped`, `eventOn`, `StopKind`, `stop`, `within`, `endOfCycleAnchor`, `atLeastOffset`.<br>Every selection is declared on its type:<br>• `stopDate` on `TreatmentLine`;<br>• `period` on `AcuteTreatmentSummary` (a `PeriodValue`);<br>• `start` and `end` on `Period`;<br>• `acute` on `ClusterView`;<br>• `covers` on `View`.<br>`l.stopDate` (`opt Date`) is used only inside a quantifier. No new partial term. The precedence of the new INV-109 conjunct is as intended: the `∀ e` body ends at its parenthesis, and `∧` binds before `⇒`. |
| Rule constants | 18 constants. The `const` list, the axiom and `evaluationRules` name the same 18. The 17 earlier constants are byte-identical to v13. Under the refined criterion, every stored `excludes` value is the computed one. |
| Typing rule for levels | Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33; total 110, unchanged. Scopes: output 77, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Guarantee terms (v13 → v14) | All equal:<br>• `#L.evaluated = 1` 7;<br>• `rc.treatment = L.treatment` 13;<br>• `evaluationResult(L` 7;<br>• `pretreatmentBaseline(L` 6;<br>• `otherValueNamed` 6;<br>• `ch.reference.typeScope = allTypes` 7;<br>• `attackScope(` 5;<br>• `conditionHolds(` 10;<br>• `scopeFor(` 8;<br>• "has a headache type" 9;<br>• `fillsPeriod` 15;<br>• `containsPeriodOf` 12;<br>• `dayOneShown` 9;<br>• `ruleRuChildren` 6;<br>• `s.typeScope = allTypes` 9. |
| Quotes | Seven new [S-035] fragments, each found verbatim by script in the page text of its stated page:<br>• p. 86: 7.3 items 3, 4 and 5;<br>• p. 57: the 3.6.3.9 dose sentence;<br>• pp. 82–87: the chapter heading;<br>• p. 83: two 7.1 sentences.<br>Each was also read on the rendered page. The new English fragments quoted from Stage 1 ("with start and stop dates, dose changes, treatment duration", "for the period since the previous consultation (or a period chosen by the clinician)", "after 2 treatment cycles") occur verbatim in Stage 1 v18. |
| Scope sweep | The whole document was searched for enter, entry, record, input, captur, logged, store/storage, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field, questionnaire and data-entry. Every count equals v13, and no added or changed line contains any of these terms.<br>The new relations take only output elements and context properties as arguments: covered periods, the subject's course events and as-of date, the stop date a line shows, and rule components. No input entity, no storage term, and no relation with an input argument. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v14.md`: identical. |
