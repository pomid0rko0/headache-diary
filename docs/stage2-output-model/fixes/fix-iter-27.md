# Fix log — iteration 27
Input review: reviews/review-iter-27.md · Input version: v26 · Output version: v27
Date: 2026-10-22

## What was read and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039). OUT-022, OUT-018 and OUT-021 and their evidence were read closely. The key wordings:
  - OUT-022: "compare it with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible";
  - [S-011]: "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal.";
  - [S-022]: "to detect possible rebound phenomena (i.e. frequency of migraine days per month going above its baseline)";
  - OUT-018 and OUT-021: "pre-treatment baseline", not "original";
- v26 (`OUTPUT_MODEL.md`, byte-identical to `history/v26.md`): sections 1–11 in full, and from section 12 the entries for v00–v11 and v24–v26. E-008, E-041 Notes, E-042, E-043, E-048, E-049, E-055, E-067, INV-001, INV-027, INV-055, INV-056, INV-064, INV-068, INV-070, INV-097, INV-102, INV-103 and row OUT-022 were read closely;
- review 27 (one remark, R27-01), with its "Checked and not raised" list.

**Earlier loop files read, so that no fix is undone:**
- review 26, fix 26 (the `resumes` link, `resumesFrom`, `originalStart`, the INV-001 chain conjuncts, and its consequences table) and fix 25 (one stop or pause per course; a restart is a new course);
- the oscillation check after iteration 24, with its ten watch points; in particular watch point 4 (the course-event dates of section 2.8, `atTimePoint`, `fitsMonthlyPeriod`, `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, `firstChangedDay` and the E-049 `when` clause of `onTreatmentPeriod`) and watch point 9 (the items aligned in v22–v24).

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. No earlier fixer declined a remark on the original baseline of a resumed course.

**No download and no web search.** No quote was added or changed; every quoted fragment on a changed line is verbatim in Stage 1 v18 or already in v26 (`quotes27.py`).

**Scripts.** All are in the session scratchpad, folder `fix27/` (`/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix27/`), and were run with `python3 -I`:
- `chain27.py` (output `chain27.out`) evaluates, as written in v26, in v27 and in the review's option (a): INV-001 (course-event and `resumes` conjuncts, unchanged), `startOf`, `resumesFrom`, `originalStart`, INV-070, the E-049 `when` clauses, `firstChangedDay` and INV-103. It runs them on the review's examples B, B2 and Kn, on the stated-start contrasts (the R26-01 example and fix 26's chain K), on every view of these contexts with every calendar month from January 2024 to October 2026 as the baseline, and on the watch-point examples of fixes 25 and 26.
- `random27.py` (output `random27.out`, reproducible: two runs byte-identical) runs 40,000 random admissible contexts with a chain of 1–4 courses of one drug, the first start stated in half of them, and unrelated courses (another drug, or the same drug tried again unlinked, some without a start). For every stop, pause or reduction of every preventive course it builds views with about 13 baselines each (random spans and spans next to every bound) and random on-treatment and after periods: 2,176,160 views. It also builds the satisfiability construction.
- `mech27.py`, `names27.py`, `tokcheck27.py`, `omndiff27.py`, `itemdiff27.py`, `quotes27.py` and `scope27.py` are copies of the fix-26 scripts, read before use.

### Verification of the remark

**R27-01 holds** (`chain27.py`, predicates as written in v26). In each case INV-001 admits the context and INV-103 requires the view.

| Example | `originalStart` of the view's course (v26) | Calendar months admitted as the baseline by v26 INV-070 | Of which the review names |
|---|---|---|---|
| **B**: course t1 with no stated start, `doseChange(reduction)` 15 March 2026, `stop(paused)` 30 June 2026; t2 starts 1 September 2026, reduced 1 October; (t1, t2) ∈ `resumes`; view of t2's reduction | {1 September 2026}, the restart | 32 (January 2024 to August 2026) | August 2026 (the pause) and May 2026 (on t1, after its reduction) |
| **B2**: as B, t1's only event its pause | {1 September 2026} | 32 | August 2026 |
| **Kn**: a → b → k, a with no stated start and `stop(paused)` 31 October 2025; b 1 December 2025 – 30 June 2026; k from 1 September 2026, paused 15 October; view of k's pause | {1 December 2025}, the start of b | 23 (to November 2025) | November 2025 (the pause between a and b) |

With the first start stated (the R26-01 example and K), v26 admits only months before that start (24 and 14 months, the last December 2025 and February 2025), as fix 26 reported. The INV-070 Notes sentence "no month of an interval off treatment between the courses [...] stands for the original pre-treatment baseline" is therefore not secured by the v26 predicate, as the review states.

The views that INV-103 does not require show the same defect. The views of the first course itself (t1 in B and B2, a in Kn), which has no stated start, admit every month as the baseline in v26: 34 of 34. This is because `originalStart` equals `startOf`, which is empty.

### Choice between the review's options

**Option (b), without the fallback: the original pre-treatment baseline is asked for and admitted only where the context states the start of the course as the treatment was first started.** Chosen, on this evidence.

1. **Option (a) does not secure "original".**
   - Where the first course of the chain has no stated start, the context places that start nowhere. That course was taken before its first dated event for a time the context does not state.
   - A bound by the dated course events of the chain rejects the pause months and the months after the first dated event. It still admits every month before that event as "the original pre-treatment baseline":
     - in B, February 2026, which is on t1 at its earlier dose or before t1 began, the context not saying which;
     - in B2, May 2026, before t1's only dated event, its pause on 30 June;
     - in Kn, February to September 2025, on course a or before it.
   - The review describes t1 as a treatment that "the patient was already taking". So option (a) still admits on-treatment months as the original baseline. That is the R26-01 output in a third form, and a later reviewer could raise it again.
   - On the random contexts, in chains of 2–4 courses, option (a) accepts 249,051 baselines. Of these, 115,321 lie in the open interval of a first course whose start is not stated (`random27.out`).
2. **Option (b) secures it.**
   - Where the context states the original start, every admitted baseline ends before it, with the same verdicts as v26.
   - Where it states none, no period is admitted.
   - On the random contexts, 0 of 250,908 baselines that v27 admits overlap a course or pause interval of their chain (check (iv)).
3. **Option (b) follows the model's general treatment of unstated starts.** The model asks for content aligned to a treatment start only where the context states that start:
   - the response comparison (INV-055 first conjunct; INV-056 `rc.treatmentStart ∈ startOf(ctx, rc.treatment)`; E-041 Notes: "A treatment whose start the context does not state [...] has no response comparison, which is aligned to the start (INV-056)");
   - the treatment review view (INV-102) and the post-stop view itself (INV-103);
   - the on-treatment period of this very view (E-049 `when` clause of `onTreatmentPeriod`);
   - the start date, duration, response summary and adherence of a treatment line (E-055: "The `when` clauses state when the content can exist").

   The original pre-treatment baseline is aligned to the original start, so it is asked for where the context states that start.
4. **Size.**
   - Three `omn` blocks change, each by one line: the `originalStart` body (with its comment), the `when` clause of E-049 `baseline`, and the INV-070 baseline conjunct.
   - Nothing is added to INV-001, and no name is declared.

**One deliberate extension beyond the review's examples.**
- **What it is.** Option (b) is applied to every course whose original start the context does not state, not only to courses that resume another course. This covers:
  - the first course of a chain whose start is not stated (t1, a);
  - a course in no link whose start is not stated.
- **Why.** For these courses v26 admitted any month as the original baseline, including months after the course's dated events. Examples are May 2026 in t1's own pause view in B, or a month after the reduction of a course never resumed.
- **What changes, and what does not.**
  - The views of these courses are not required by INV-103, which requires a view only for a course with a stated start. That requirement is unchanged.
  - The only difference is that no baseline is asked for or admitted in them.
- **The trade-off with the orchestrator's check (iii).** The requirement to secure the original baseline for every admissible chain, first start stated or not, conflicts with check (iii) ("treatments never resumed behave exactly as in v26") for exactly one case: a course in no link without a stated start, which is a chain of one course whose first start is not stated. I resolved the conflict in favour of securing the baseline. The result for check (iii) is identical for every course in no link whose start is stated (see Checks).
- **Review 27's position.** Review 27 set this case aside ("Checked and not raised", the general treatment of unstated starts). It also noted that the fixer may bound such a view's baseline. The extension does not touch INV-068, INV-102 or INV-103.

**Option (b) does not narrow Stage 1 OUT-022 (SHOULD) for a patient already on treatment when the diary begins.**
- **Where the context states the treatment's original start.** This includes a start before the diary began: the context describes the subject's history, and the model never refers to when the diary begins. In this case the baseline is asked for (SHOULD) and bounded exactly as in v26 (check (ii): 908,103 of 908,103 views).
- **Where the context states no start for the course as first started.**
  - **No period can be placed before the original start.** Every month before a restart or before the first dated event may lie in the pause or on the first course.
  - **Such a period does not show what OUT-022 asks for.** A period shown as "the original pre-treatment baseline" is then not the baseline OUT-022 asks for. Comparing with it could hide the "worsening or rebound above baseline" that OUT-022 exists to show ([S-011]: migraine "worsens after treatment withdrawal"; [S-022]: "going above its baseline").
  - **So nothing satisfiable is lost.** v27 excludes only outputs that present such a period as the original baseline. It drops no requirement that any output could meet.
- **Everything else OUT-022 asks for stays required for this patient:**
  - the post-stop view of each stop, pause or reduction of every course with a stated start, including the resumed course (INV-103, unchanged);
  - the headache and migraine days from the first changed day (E-049 `after`);
  - the on-treatment period (E-049 `onTreatmentPeriod` and its `when` clause, unchanged).
- **Unchanged from v26.** That INV-103 requires no view for a course whose own start is not stated is the v26 reading, which review 27 did not raise. v27 does not change it.

**No Stage 1 issue.** OUT-022 says "original". Where the context places no original start, the model requires what can be placed and excludes what would misstate the baseline, so it does not work around Stage 1. As the review asks, the E-049 Notes now state that the original baseline of a treatment whose first start is not stated cannot be placed.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R27-01 | fixed: the review's option (b), without the fallback, applied to every course whose original start the context does not state | E-008 (Definition, Meaning, Notes); E-049 (Definition, Meaning, Conformance, Notes); INV-070 (Predicate, Reading, Notes); INV-001 (Notes); INV-097 (Notes); row OUT-022 (coverage reason) | **E-008, Definition:** `originalStart(c, t) ≙ {d : Date \| ∃ u : Treatment • resumesFrom(c, u, t) ∧ (∀ p ∈ c.subject.resumes • p.2 ≠ u) ∧ d ∈ startOf(c, u)}`, the start that the context states for the first course of the chain, the one that resumes no course; ∅ where it states none. The v26 fallback ("the earliest start that the context states for t or for a course that t resumes") is dropped, and the comment no longer claims more than the body.<br>**Same value as v26** wherever the first course states its start, because starts along a chain are in chronological order (INV-001). Also the same for every course that resumes no course: `startOf(c, t)`. At most one member: the first course is unique (INV-001: at most one predecessor and successor, acyclic, finite), and it has at most one start.<br>**E-008, text:**<br>• Meaning: the original start is the start that the context states for the first course, where it states one;<br>• Notes, **Resumed courses**: `originalStart` is empty where the context states no start for the first course, for example for a treatment already being taken at its first stated course event, since the start of a later course is a restart and the context does not state when the first course began; the original baseline is asked for and shown only where `originalStart` is not empty.<br>**E-049, Definition:** `baseline : opt →Period SHOULD when originalStart(ctx, self.treatment) ≠ ∅` (the comment unchanged).<br>**E-049, text:**<br>• Meaning: the baseline is shown where the context states the original start; otherwise no period is shown as the original pre-treatment baseline;<br>• Conformance: the same, with "INV-070 admits none";<br>• Notes, new paragraph **Original start not stated**: the review's example B (August 2026 in the pause, May 2026 on the first course, February 2026 on the first course or before it); why no period can be placed; the same for a course whose own start is not stated, whose view INV-103 does not require; the precedent of the other start-aligned content (the on-treatment period, INV-055, INV-056, INV-102, INV-103, E-055 Notes).<br>**INV-070, Predicate:** `(∀ b ∈ v.baseline • ∃ s ∈ originalStart(ctx, v.treatment) • b.end < s)` replaces `(∀ b ∈ v.baseline; s ∈ originalStart(ctx, v.treatment) • b.end < s)`. Where `originalStart` has its one member, the two are equivalent; where it is empty, the new conjunct admits no baseline. Nothing else in the predicate changed.<br>**INV-070, text:**<br>• Reading: where the context states no start for the course as it was first started, the view shows no period as that baseline;<br>• Notes, **Original baseline**: a baseline is shown only where the context states the original start, and ends before it; why none is shown otherwise; every baseline shown ends before the start of the view's own course;<br>• the satisfiability sentence: with no baseline where the context states no original start.<br>**INV-001, Notes:** the original baseline of a resumed course's monitoring, with "where the context states no start for that first course, the monitoring shows no baseline (E-049)"; and in **Resumed courses**, "`originalStart` is the start that the context states for that course, and is empty where it states none" instead of "or the earliest start the context states for the chain".<br>**INV-097, Notes:** the post-stop satisfiability clause adds "and no baseline where the context states no original start".<br>**Row OUT-022:** the original baseline is "a period that ends before the treatment was first started, wherever the context states that start; where it states none, no period can be placed before that start, and none is shown as the original baseline". The Elements and Invariants columns are unchanged.<br>**Not changed:**<br>• INV-001 and its conjuncts, the `resumes` component and `resumesFrom` (fix 26);<br>• fix 25 (one stop or pause per course; a restart is a new course);<br>• every watch-point-4 item, including the E-049 `when` clause of `onTreatmentPeriod` and the on-treatment and after conjuncts of INV-070;<br>• INV-056 and INV-068 (the review: "need no change");<br>• INV-103;<br>• section 2.8. |

## Other changes

Bookkeeping only:
- header (v27, iteration 27);
- section 9 ("as of v27");
- section 11 (iteration 27 entry: no web search, no download, no new source);
- section 12 (v27 entry).

**Items changed (diff v26 → v27, `itemdiff27.py`).**
- **6 content items:**
  - 2 elements: E-008 (Definition, Meaning, Notes) and E-049 (Definition, Meaning, Conformance, Notes);
  - 3 invariants: INV-070 (Predicate, Reading, Notes), INV-001 (Notes) and INV-097 (Notes);
  - row OUT-022.
- **4 bookkeeping items:** the header and sections 9, 11 and 12.
- **Formal blocks:** 3 of 182 `omn` blocks changed (`omndiff27.py`); every other block is byte-identical:

| Block | Change |
|---|---|
| E-008 | the `originalStart` body (2 lines → 1) and its comment (2 → 3 lines) |
| E-049 | the `baseline` declaration gains `when originalStart(ctx, self.treatment) ≠ ∅` (the comment moves to the next line) |
| INV-070 | the baseline conjunct: `∀ b ∈ v.baseline; s ∈ … • b.end < s` → `∀ b ∈ v.baseline • ∃ s ∈ … • b.end < s` |

- **Not changed:**
  - no element or invariant added, withdrawn or renumbered;
  - no level, value, axiom, Realises field or declared name;
  - no Elements or Invariants column of the traceability table;
  - no source or quote.

## Checks

| Check | Result |
|---|---|
| (i) The review's scenarios (`chain27.py`) | **B:** v26 admits 32 calendar months (January 2024 – August 2026), among them August 2026 and May 2026; **v27 admits none**, and E-049 asks for no baseline (`originalStart(t2) = ∅`). Option (a) would admit 26 (to February 2026).<br>**B2:** v26 32, among them August 2026; **v27 none**. Option (a) would admit 29 (to May 2026).<br>**Kn:** v26 23, among them November 2025; **v27 none**. Option (a) would admit 21 (to September 2025).<br>**Every view of these contexts** (also t1's and a's own views, not required by INV-103, and b's stop in Kn): v26 admits 23–34 months each, all overlapping a course or pause interval of the chain; **v27 admits 0**. A view without a baseline is admitted by v26 and v27 alike.<br>So pause months and on-treatment months are rejected as the original baseline in every view of the scenarios. |
| (ii) Chains whose first start is stated behave as in v26 | **Contrasts.** R26-01 example and fix 26's K: v26, v27 and option (a) give identical verdicts on every month (24 and 14 admitted, all before the first start, none overlapping).<br>**Random contexts** (`random27.py`): on every view of a course of a chain whose first start is stated, v27 gives the v26 verdict and the same E-049 baseline requirement (908,103 of 908,103). `originalStart` v27 = v26 wherever the first course states its start (77,461 of 77,461 courses). |
| (iii) Treatments never resumed | **Courses in no link whose start is stated:** v27 = v26 on every view, verdict and E-049 baseline requirement (455,221 of 455,221).<br>**Courses in no link without a stated start** (views not required by INV-103):<br>• 160,668 views. 65,660 keep their verdict. The other 95,008 differ only in that v26 admits their baseline and v27 does not.<br>• E-049 no longer asks for a baseline.<br>• This is the deliberate extension explained above.<br>**`originalStart`:** v27 = v26 = `startOf` for every course that resumes no course (80,103 of 80,103). |
| (iv) No accepted original baseline overlaps a course or pause interval of its chain | Random contexts, chains of 1–4 courses, the first start stated in 19,748 and not stated in 20,252.<br>A course without a stated start counts as taken from an unknown day, so its interval is open to the left.<br>• **v27:** 0 of 250,908 accepted baselines overlap (chains of 2–4: 0 of 133,730). Every accepted baseline also ends before the start of the view's own course (250,908 of 250,908).<br>• **v26:** 286,244 of 561,986 overlap.<br>• **Option (a):** 184,603 of 435,511 overlap (chains of 2–4: 115,321 of 249,051).<br>v27 admits no view that v26 rejects (0), and every v26 → v27 difference is a baseline that v27 rejects where the first start is not stated (311,078 of 311,078). |
| Watch-point examples (`chain27.py`) | Unchanged from v26:<br>• stop on the start day (1-day on-treatment period required and admitted);<br>• reduction on the start day (no on-treatment period required; view admitted);<br>• reduction 1 March with pause 30 June (both views admitted);<br>• fix-25 restart example with the link: December 2025 admitted, April 2026 (the pause) rejected, in v26 and v27. |
| Satisfiability pass | **INV-001.** Predicate byte-identical, so `Ctx` is unchanged (40,000 random admissible contexts).<br>**E-008.** `originalStart` is a total defined function (a comprehension); it has at most one member (140,067 of 140,067 courses), every course has exactly one first course of its chain (140,067 of 140,067), and it is never after `startOf` (140,067 of 140,067).<br>**E-049.** `baseline` keeps an `opt` type, so the typing rule for a SHOULD attribute with `when` holds; the `when` clause refers only to `ctx` and the view's own attribute (section 3.5).<br>**INV-070 with E-049 and INV-103.** For every INV-103 event of 20,000 random admissible contexts, the fix-26 construction was built with every SHOULD attribute that E-049 asks for: a baseline of L days ending on the day before the original start where `originalStart ≠ ∅`, an on-treatment period where its `when` clause holds, and L days from `firstChangedDay`. It meets v27 INV-070 and INV-097 in 62,234 of 62,234 views, 17,074 of them without a baseline. The views of courses without a stated start (not required) meet v27 INV-070 with periods after the event only: 19,187 of 19,187.<br>**Where E-049 asks for a baseline, INV-070 admits one.** Its `when` clause is exactly the condition under which INV-070 admits a baseline, so the SHOULD attribute and the SHOULD invariant never conflict.<br>**INV-097, INV-003, INV-011, INV-098.** A view without a baseline has fewer periods, which only weakens their antecedents.<br>**INV-056, INV-068, INV-055.** Unchanged; they do not read `originalStart`.<br>**Result.** No MUST or SHOULD combination of the invariants that constrain the post-stop view or the context becomes unsatisfiable, and no derived attribute is required where its relation is undefined. |
| Headings and IDs (`mech27.py`) | 67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111), none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn). No dangling E-, INV-, ISS- or source reference. 37 source IDs cited, all within S-001–S-046 or S-101–S-106. Every OUT reference exists in Stage 1. Output identical to the v26 run. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Types and names (`names27.py`, `tokcheck27.py`) | 749 declared names, none declared twice, as in v26. The token report is identical to v26 (106 flagged tokens, each a declared attribute; none added, none removed).<br>The changed text is well typed:<br>• `p.2 ≠ u` on a pair of `Treatment` (section 2.4);<br>• `(∀ p ∈ c.subject.resumes • …)` parenthesised inside the body of `∃ u`;<br>• `originalStart(ctx, self.treatment) ≠ ∅` on a `set Date`;<br>• `∃ s ∈ originalStart(…) • b.end < s` with `<` on dates.<br>Brackets are balanced in the three changed blocks. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34, unchanged. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged, with no typing-rule violation. INV-070 stays SHOULD (OUT-022), and `baseline` stays SHOULD, now with a `when` clause. |
| Diff of formal blocks (`omndiff27.py`, `itemdiff27.py`) | Only the E-008, E-049 and INV-070 `omn` blocks changed.<br>Byte-identical:<br>• INV-001;<br>• section 2.8 and every other watch-point-4 item (`atTimePoint`, `fitsMonthlyPeriod`, `notStoppedBefore`, `intervalOnTreatment`, `evaluatedOnTreatment`, `firstChangedDay`, the E-049 `when` clause of `onTreatmentPeriod`);<br>• E-041, E-042, E-046, E-055, E-067;<br>• INV-055, INV-056, INV-058, INV-059, INV-062 to INV-064, INV-066 to INV-068, INV-079, INV-103 to INV-105, INV-109;<br>• the rows OUT-009, OUT-018, OUT-021, OUT-024 and OUT-039.<br>INV-097 changed in its Notes only. |
| Quotes (`quotes27.py`) | 11 quoted fragments on changed lines, all verbatim in Stage 1 v18 or already in v26 (for example "the original pre-treatment baseline", "aligned to the treatment start date", the [S-011] fragment). None is unmatched, and no source quote was added or changed. |
| Scope sweep (`scope27.py`) | Term counts v26 → v27 are all equal except four:<br>• "stor" (66 → 67) is the path `history/v26.md`;<br>• "taken" (57 → 60) is "a treatment already being taken" (twice) and "Not taken" (section 12);<br>• "states" and "stated" are "the context states", the model's phrase for a context property.<br>No element is described as entered or recorded. The changed relations take only context properties (`resumes`, `courseEvents`) and output elements as arguments. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v27.md`: identical. `history/v26.md` is unchanged (equal to HEAD). |
