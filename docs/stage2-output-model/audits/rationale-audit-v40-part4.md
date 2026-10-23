# RATIONALE audit — part 4 (lines 1799–2359), model v40
Date: 2026-10-23
FINDINGS: 1 (CONTRADICTION 0, OVERCLAIM 0, STALE 0, WRONG-REFERENCE 1)
Entries audited: 102 — D 54, S 22, W 2, Q 24 (non-quote prose only), N 0, X 0. Also the entry-less texts of sections 2.5 and 2.7.

Range: `RATIONALE.md` v39 (companion of `OUTPUT_MODEL.md` v40), from `#### INV-114/D01` (line 1799) to `#### INV-123/S02` (line 2355). It covers the rest of section 2.4, sections 2.5 to 2.7, and section 2.8.

## Method

All scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/ra4/`. Every script was run with `python3 -I`.

1. **Reading.**
   - I read PROCESS.md in full, and `RATIONALE.md` section 1 (its rules, in particular the moved-text rule and the meaning of "X Notes" in moved text).
   - I read the whole of `OUTPUT_MODEL.md` v40: sections 1–4, all elements and invariants, and sections 7, 8, 9 and 11.
   - I read review 41 (R41-01) and the oscillation check after iteration 40 (watch point 8).
   - I read the "Checked and not raised" sections of reviews 36–40, and fixes 35, 35-equivalence (section 5, EQ35-04 sweep) and 38. From `restructure/plan-v35.md` I read the section 9.2 dispositions of every v34 Notes paragraph that an entry in my range points to.
2. **Extraction** (`entries.py`). It found 102 entries in the range, with their kinds.
3. **Settled entries** (`mentions.py`, `ctx.py`). Every entry ID was searched in reviews 35–41, fixes 35–40, the equivalence check and the oscillation checks after iterations 36 and 40, and each hit was read in context. Already raised or declined:
   - INV-076/D01 is R41-01 (open);
   - INV-075/D01, INV-085/D01 and INV-110/S01 were declined (watch point 8);
   - INV-073/D01, INV-089/D01 and INV-109/D02 were checked by review 41 for type scope;
   - INV-087/D01 was checked by review 36 (window marks);
   - INV-074/D01, INV-078/D02, INV-079/D01, INV-109/D01, INV-109/D03 (its INV-123 references only), INV-112/D01, INV-103/D01, INV-105/D05, INV-105/S02, INV-123/D02 and INV-123/D06 were edited or examined by the EQ35-04 sweep;
   - INV-096/D01 and INV-096/D02 were set by fix 38;
   - INV-118/D02 was confirmed by fix 38.
4. **Claim-by-claim comparison.** Every sentence of every D, S and W entry, and the non-quote prose of every Q entry, was compared with the v40 formal text it describes:
   - what the item says, its level and `when` clauses, which item holds the rule;
   - the W2 markers, the case tables and section 9.

   `phrases.py` also listed every sentence that states a reason as a fact about the model ("derivation", "cannot", "never", "only where", "is required", MUST …). Each was re-read against the predicate.
5. **Mechanical checks.**
   - `fields.py`: every Kind field matches its ID, the anchor is the first Concerns ID, and every Concerns ID is live or a "v34" ID listed in model section 9. Result: 0 problems.
   - `refs.py`: no entry in the range names a merged v34 invariant as if it were live (outside the "Text (v34 … Notes)" labels), and no entry ID it cites dangles. Result: 0.
   - `notesrefs.py` and `classscan.py`: every "X Notes" pointer in the range, and every "X Notes, **Heading**" pointer in the whole file, was resolved against the model's Notes field of X and the entries anchored at X (RATIONALE section 1), and against the plan's disposition (K, D or R) of the v34 paragraph. Result: one pointer does not resolve (RA-4-01).
6. **Enumerations of the predicates as written.**
   - `dates.py`: INV-079/W01 (41 and 294 days), INV-105/D02 (43 days), INV-094/D01 (15 August–20 October is 67 days, and is no run of whole months, 28-day periods or weeks). Result: all as stated.
   - `sdrc.py` (INV-116/S01): the score components of `critIhsQ6` and `critDmkg` name instruments of their `alsoRestsOn`, no named criterion has an attack-reduction component, and the six names are pairwise distinct. Result: as stated.
   - `enum1.py`, over 211 type contexts (antichains over a code tree with subtypes):
     - `scopeFor` ⇒ `onlyOfType`, and exactly one scope (INV-088/S01);
     - an all-types summary of a subject with cluster headache and another possible type is not "of cluster headache only" (INV-073/D01).

     Result: 0 counterexamples.
   - `enum1.py`, the E-049 `onTreatmentPeriod` `when` clause in 939 course-event cases, against the descriptions of INV-070/S01, INV-097/S01 and INV-103/D01 (always asked after a stop; not after a reduction on the start day; without a stated start, only after a reduction that another dated course event precedes). Result: 0 mismatches.
   - `enum1.py`, `originalStart` over 12,139 `resumes` contexts admitted by INV-001 (INV-112/D02, INV-103/D01). Results:
     - the original start is never after the course's own start;
     - it is empty whenever the own start is unstated;
     - 0 counterexamples.
   - `enum1.py`, `courseNotOutside` (INV-105/D05): `courseNotOutside(t, s.period) ∧ within(s.period, covers)` ⇒ `courseNotOutside(t, covers)`. Result: 0 counterexamples.
   - `enum1.py`, INV-116/D02 (200,000 random criteria): leaving out components whose condition fails leaves the INV-063 category set unchanged. Result: 0 differences.
   - `fills.py` (INV-104/D01, INV-105/D02), over 51,600 covered periods and three granularities. Results:
     - a `fillsPeriod` series exists exactly when `containsPeriodOf` holds;
     - it leaves less than one period at either end, and nothing at the start for 28-day periods;
     - it equals the run where the covered period is a run of whole periods;
     - 0 counterexamples.

## Findings

### RA-4-01 WRONG-REFERENCE: INV-109/D03 points to an E-008 Notes paragraph that v35 replaced by R-MCF (2)
- Entry: `RATIONALE.md` INV-109/D03 (line 1994), moved v34 INV-109 Notes, **Period.**
- Entry text: "Its summary still ends with the course, on its stop date or on the as-of date, which do not depend on the start, and it begins on or before the first dated course event, so that it covers every day that the context places on the course (E-008 Notes, **Course start not stated**), not, for example, a period after the course has stopped."
- Model text:
  - `RATIONALE.md` section 1, **Moved text**: "A reference "X Notes" in moved text refers to the Notes of item X in v34, which v35 keeps in the model's Notes field of X and in the entries anchored at X."
  - v40 E-008 Notes, in full: "`PreventiveTreatmentType` lists the treatment types to which the guidance time points of E-041 refer … Every preventive treatment has at least one type (INV-001): `otherPreventive` is the type of a preventive treatment that none of the other values describes. Rationale: E-008/D01, E-008/D02, E-008/D03, E-008/D04." It has no **Course start not stated** paragraph.
  - None of the entries anchored at E-008 has it either:
    - E-008/D01 is **Pause, restart and discontinuation.**;
    - E-008/D02 is **Resumed courses.**;
    - E-008/D03 and E-008/D04 are v34 Meaning text.
  - `restructure/plan-v35.md` section 9.2, row E-008: ""**Course start not stated.**" R (its first two sentences go into model section 3.8, R-MCF (2))". The paragraph was added in v28 (commit c541f8a) and removed in v35 (commit 3b67179).
  - Where the content now is:
    - model section 3.8, clause 2: "**Content aligned to other facts of the same course** is asked for whether or not the context states the course's start. … Where such content is bounded by the start ("on or after the start of the course"), the bound reads "on or after a dated course event of the course" (`courseBegunBy`, E-008)";
    - E-008 Meaning: "`courseBegunBy(c, t, d)` holds when a course event of t is dated on or before d, so that the context places the course of t as begun by d: every course event is dated on or after the day its course began (section 2.8)";
    - the INV-109 conjunct itself: `(∀ f ∈ ctx.subject.courseEvents • f.treatment = l.treatment ⇒ s.period.start ≤ f.date)`.
- Why they conflict:
  - The entry cites, as the place that defines "every day that the context places on the course", a paragraph that v40 no longer has, neither in E-008's Notes field nor in any entry anchored at E-008.
  - So the pointer dangles, and section 1's statement about "X Notes" is false for it.
  - The claim the pointer supports is still true of the formal text: the INV-109 conjunct above, with the stop and as-of conjuncts. What is wrong is the place named for the rule.
  - The four moved-text exceptions of section 1 cover references to merged invariants and moved conjuncts. They do not cover a reference to a v34 Notes paragraph that v35 replaced by a model rule, so the v35 rewrite left this pointer as it was.
  - Not raised or declined before. Fix 35, D-13 updated such pointers in kept model text only. EQ35-04 edited INV-109/D03 for its INV-123 references only. It is not one of the watch point 8 entries.
  - `classscan.py`: across the whole file, this is the only "X Notes, **Heading**" pointer that does not resolve. Outside my range, E-049/D03 (line 1072) has the same dangling pointer without a heading: "the course began on a day the context does not state, on or before its first dated course event (E-008 Notes)". The text it cites is that same removed paragraph, whose content is now in E-008 Meaning and section 3.8. INV-001/D03's "(E-008 Notes)" resolves to E-008/D01.
- Correction (entry only; no model change):
  - In INV-109/D03, replace "(E-008 Notes, **Course start not stated**)" with "(R-MCF (2), section 3.8; `courseBegunBy`, E-008)".
  - For the class, make the same change in E-049/D03's "(E-008 Notes)" ("… on or before its first dated course event (`courseBegunBy`, E-008; R-MCF (2))").
  - Optionally add to section 1's list of moved-text exceptions: "a reference to a v34 Notes paragraph that v35 replaced by a rule of the model names that rule". That keeps the "X Notes" sentence of section 1 true.

## Checked and consistent

- **INV-114/D01, S01.** The ties are as stated:
  - INV-114 is definitional;
  - INV-079 has `∀ r ∈ l.preventiveResponse • r.treatment = l.treatment`;
  - `comparison` is SHOULD (E-046, INV-062);
  - every predicate of E-046 tests `rc.treatment = L.treatment`;
  - `ran L.evaluated ⊆ ran rc.onTreatment` is in INV-062;
  - without a stated start no comparison exists (INV-123 `courseEvent` of kind `start`).
- **INV-116/Q00 (prose), D01, D02, S01.**
  - INV-116 is definitional, and INV-058 and INV-082 are the analogous ties.
  - `criterion` is SHOULD and labels are MAY.
  - A component whose condition fails is never met and always decided (`reductionMet`/`Decided`, `attackReduction…`, `score…`), and INV-062's per-component conjuncts carry `conditionHolds`. The category sets of INV-063 are unchanged (`enum1.py`).
  - The S01 facts hold (`sdrc.py`).
  - "E-045 Notes, **Named criteria**" resolves to E-045/D05, which says the same. Its "not constrained" is read as "not constrained by this tie", as the sentence's context gives.
- **INV-063/Q00, INV-064/Q00 (prose).** Their pointers resolve: E-045/D09 (**Type scope**) and E-046/D05 (**After a stop or pause**).
- **INV-064/D01, S01.**
  - The months begin on or after a dated course event (`courseBegunBy`) and end by every stop (`evaluatedOnTreatment`).
  - "they begin on or after its start" is implied, because every course event is dated on or after the day its course began (E-008 Meaning).
  - The S01 construction meets INV-056, INV-062 and INV-064, since `insufficientControl` admits any count.
- **INV-066/D01, S01; INV-067/D01.**
  - `adherenceFor` makes the window contain its on-treatment period and end with it.
  - INV-067 bounds only the first day, and neither it nor INV-056 bounds the window by a stop.
  - INV-003 places the window and INV-011 its completeness. "E-047 Notes" resolves to E-047/D02.
- **INV-068/D01, S01, W01.**
  - INV-068 needs a stated start and `notStoppedBefore`, and INV-056 has no stop bound.
  - The S01 periods meet INV-068 (one stop per course; no course event precedes the start, INV-001).
  - In W01, a view of a treatment with no stated start does not meet INV-068.
- **INV-069/D01, S01.** The `i₁`/`a₁` ties, `onSameScale` and `inSameForm` are as stated. "one definition that the view follows" is E-011's Meaning and INV-111.
- **INV-070/Q00 (prose), S01; INV-112/Q00 (prose), D01, D02, S01.**
  - The INV-112 conjuncts, `firstChangedDay` and the E-049 `when` clauses are as described (`enum1.py`: 0 mismatches).
  - The original start is never after the own start (`enum1.py`).
  - Pointers resolve: "E-049 Notes" to E-049/D01, **Original start not stated** to E-049/D02, and E-049/D04.
  - INV-112/D01's "(INV-123, with the same `eventOn`)": INV-123 tests `CourseEvent(…) ∈ c.subject.courseEvents`, which is `eventOn` by definition (E-008), so the test is the same.
- **INV-072/D01, D02.**
  - The outcomes and lines are placed in the summary's view by E-051 `outcomes`, `sequence` (W2 SHOULD).
  - The INV-071 single-formulation summaries name `{m.formulation}`, and INV-074 allows at most one formulation.
  - D01's list of views omits the cluster view (INV-088), which E-051 Conformance names. The list illustrates the general "wherever a view shows a summary", which holds through W2; it does not claim to be complete. Examined by EQ35-04.
- **INV-073/D01.** It agrees with INV-073, INV-088 and `scopeFor` (`enum1.py`; checked by review 41).
- **INV-074/D01.** It agrees with INV-074's formulation conjunct, INV-072 and INV-123 (`usedMedication`). The "names none" clause concerns a summary of all formulations, as its apposition says.
- **INV-075/D01, INV-085/D01, INV-110/S01.** Declined earlier (watch point 8); I have no new evidence.
- **INV-076/D01.** Subject of R41-01; not raised again.
- **INV-078/D01, D02.**
  - The lines are in the view (INV-078), and cycle lines are the content of the menstrual-relation view (INV-087).
  - The order compares every two lines that show a start date, and INV-123 ties a shown start date to a stated start.
- **INV-079/Q00 (prose), D01, W01.**
  - The duration conjuncts are as stated, and the date ties are now in INV-123 (examined by EQ35-04).
  - The W01 numbers are correct (`dates.py`).
- **INV-109/D01, D02, D04, D05, S01.**
  - The dose-change conjunct is with INV-123.
  - The `allTypes` summary (checked by review 41).
  - `summarisesMedication`: "E-051 Notes" resolves to E-051/D01, which states the two readings.
  - Every acute line has a summary (INV-001, INV-079, INV-123).
  - `adherenceFor`.
  - The S01 construction is in order under INV-001.
- **INV-082/Q00 (prose), D01.** `publishedGrading` gates the category (INV-082), SD-IN gives HALT-30 `false` and no case for MSQ v2.1, M-TOQ and PGIC, E-058 asks for `category` only `when publishedGrading`, and no invariant asks for one.
- **INV-083/Q00 (prose), D01; INV-085/Q00 (prose).** INV-083 asks for both HADS subscales. INV-085 admits only the SD-SR subscales, once each.
- **INV-086/D01.** It agrees with INV-086 (`menstruatesDuring(c, c.timeRange)`) and E-060's lead-in Meaning. Its sentence "A time range that begins before the subject's first menstruation requires it" is read with the sentence before it ("A time range during which the subject does not menstruate at all … does not require the view"). It concerns a time range during which menstruation begins. Optional clarifying words: "… and during which the subject menstruates".
- **INV-087/Q00 (prose), D01.** The window claims, with their exception, follow from INV-087 and INV-124 (checked by review 36).
- **INV-088/D01, S01.**
  - The summaries are of the covered period.
  - INV-003 Notes put them in the cluster view.
  - `scopeFor` ⇒ `onlyOfType` gives 15 minutes through INV-073 (`enum1.py`).
- **INV-089/Q00 (prose), D01, D02, S01.**
  - The rate relation, `lastDay`, the remission bound tested on the whole period, and the `s ≤ e` guard are as stated.
  - "E-063 Notes" resolves to E-063/D01.
  - D01's type-scope sentence was checked by review 41.
- **INV-110/D01.** INV-110 and INV-074 are as stated, and section 3.6 and the INV-011 Reading are as cited.
- **INV-115/D01, S01.**
  - INV-115 is definitional and limited to `concerns(…, c1)`.
  - INV-061 is its counterpart.
  - `components` is SHOULD with W2 SHOULD, and INV-092 is per dimension.
  - "E-033 Notes" resolves to E-033/D01.
  - INV-003 and INV-011 cover `referencedValues`.
- **INV-094/D01, S01.**
  - INV-001 makes the selected time range a run of whole periods. 67 days is no such run (`dates.py`).
  - `chosenPeriod` is bounded only by the as-of date.
  - "its Notes give the construction" resolves to INV-104/S01.
- **INV-096/D01, D02.**
  - Age is read per result and per period (`childOn`).
  - A time range that begins in childhood is exactly the case in which it contains a childhood period.
  - `∃ g` as in section 3.4 and C1-12.
  - The `let C` restriction and the uniform choice of form cannot be stated by a `ppRequired` case.
- **INV-097/D01, S01.**
  - INV-039 does not ask for unequal-length comparisons for children.
  - `childIn` reads the age on the periods' first days.
  - The S01 constructions meet INV-055, INV-056, INV-068, INV-070 and INV-112 (`when` clauses: `enum1.py`).
- **INV-103/D01, S01.**
  - The E-049 `after` and `onTreatmentPeriod` `when` clauses are as described.
  - A course with no stated start resumes no course, so `originalStart` is empty (INV-001; `enum1.py`).
  - Pointers resolve: "E-049 Notes, **Course start not stated**" to E-049/D03, "INV-070 and INV-112 Notes" to INV-070/S01 and INV-112/S01.
- **INV-104/D01, S01.**
  - Every conjunct named is in INV-104 or `summaryTimeCourse`: the marks, migraine days under `hasType`, the monthly series when a monthly period fits, otherwise weekly, the weekly medication series, and the MOI per monthly period.
  - The `fillsPeriod` properties hold (`fills.py`).
  - The adherence is the one INV-066 asks for (the comparison is in the same view).
- **INV-105/D01–D05, S01, S02.**
  - Migraine days carry no condition.
  - `fillsPeriod` series (`fills.py`; D02's 43 days, `dates.py`).
  - `onSameScale` with `i₁`.
  - The cycle line overlaps the covered period (INV-087).
  - `courseOverlaps`, `courseNotOutside` and the inference to the covered period (`enum1.py`).
  - `summarisesMedication`.
  - The S02 list of placing items includes the W2 markers.
  - D02's "naturally covers the period since the previous consultation" is a design reason, not a claim that the model asks for that overview.
- **ISS-01/Q00 to ISS-12/Q03 (prose).** No claim about the model disagrees with it:
  - classes of 8.2.6 without 8.2.8 (`classesOf826`);
  - the A1.1 window (E-060);
  - [S-010]'s one count (E-018);
  - the four control levels (E-046);
  - `ruleRuChildren`;
  - NICE ages 12 and over;
  - "the model applies no diagnostic criterion" (section 1).
- **Sections 2.5 and 2.7 (no entries).** The section 2.7 statement agrees with review 41's check that every Rationale cell of a source-data row names entries that list the row under Concerns; rows with a Stage 1 cell rest on Stage 1. "No entries in v35" is still true in v39.
- **Section 2.8: INV-118/D01, D02; INV-119/D01, D02, D03; INV-120/Q00 (prose), D01, D02, S01; INV-123/D02, D06, S01, S02.**
  - Each Concerns field names the v34 invariant(s), and each agrees with model section 9:
    - INV-016 → C1-03;
    - INV-017 → C1-05;
    - INV-108 → C1-04, C1-06;
    - INV-028 → C1-13 (withdrawn) and `byTypeCases`;
    - INV-101 → C2-01;
    - INV-106 → C2-05;
    - INV-107 → C2-07;
    - INV-100 → C3-05, C3-07 to C3-10;
    - INV-098 → C3-11;
    - INV-117 and INV-113 → INV-123.
  - The receiving cases have the levels and bearers the texts state:
    - SHOULD in C1-03 and C1-05, MUST in C1-04 and C1-06;
    - C2-04 at MUST NOT and C2-05 at MUST NOT, with OUT-020 as second part;
    - C2-07 at SHOULD NOT;
    - C3-11's antecedent covers `{v.covers} ∪ (v.content ∩ Period)` and dated instrument results;
    - `factsShown` has the members INV-123/D02 lists, with INV-058 for time points.
  - In the v34 INV-016 and INV-017 texts, "(INV-118 (C1-04, C1-06), …)" is the mechanical section-9 place of v34 INV-108. It includes the applicable case: C1-04 for moderate/severe headache days, C1-06 for attacks.
  - INV-120/D01 (a) covers a PedMIDAS result that shows its completion date, which E-058 asks for at SHOULD.
