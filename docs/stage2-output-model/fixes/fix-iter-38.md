# Fix — iteration 38
Version produced: v38
Reviewed version: v37
Date: 2026-10-22

Input: [`reviews/review-iter-38.md`](../reviews/review-iter-38.md) (verdict REMARKS, three remarks: R38-01, R38-02, R38-03). Every comparison uses the committed v37 as its baseline (`git show HEAD:docs/stage2-output-model/OUTPUT_MODEL.md` and `…/RATIONALE.md`; `RATIONALE.md` was unchanged in v37, so its baseline is the v36 text).

Files written:
- `OUTPUT_MODEL.md` (v38): header `Version: v38 · Iteration: 38 · Status: under review`; `Companion: RATIONALE.md v38`; one change-log entry.
- `RATIONALE.md` (v38): header `Version: v38 (companion of OUTPUT_MODEL.md v38)`.
- `history/v38.md` and `history/v38-rationale.md`: byte-identical copies of the two files.
- this log.

No web search, no download and no new source; the search log of `RATIONALE.md` is unchanged.

Scripts (all run with `python3 -I`) are outside the repository, in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix38/scripts/`:
- `verify_c1.py`: every case of table C1 with its granularities, type scopes, kinds, the Stage 1 requirements of those kinds, and whether one pair joins kinds of different requirements;
- `verify_gran.py`: every invariant that quantifies over `Ctx`, and how it binds the granularity of a series;
- `witness.py` and `scenarios.py`: a bounded-universe evaluator (all admissible contexts of three granularities between 1 January and 30 April 2026) of INV-118, INV-049 and INV-096 in their v37 and v38 forms, together with the invariants they interact with;
- `stage1match.py`: the cases named by `byTypeCases`, resolved against table C1, and the Stage 1 wording that each changed requirement rests on, searched verbatim in Stage 1 v18;
- `isshist.py` and `issdiff.py`: the history of every field of the section 8 issues in `history/v00.md` … `history/v37.md`, and word diffs of each later change;
- `apply38_model.py` and `apply38_rat.py`: exact string replacements, each required to match the stated number of times;
- `checks38.py`, `trace.py`, `defcheck.py`, `bal.py`, and the reviewer's `names.py` and `model_ids.py` (pointed at the v38 files): general checks.

The outputs of the checks are in `fix38/checks-v38.txt`.

## 1. Summary

| Remark | Verified | Disposition | Places changed |
|---|---|---|---|
| R38-01: C1-13 asks acute-medication days per calendar month or 28-day period, in one view with the frequency measures | yes, by script (`verify_c1.py`, `scenarios.py`) and against the verbatim Stage 1 text | fixed, option (a) of the review, stated once for the whole class | section 4.4 (`omn` block: new constant `byTypeCases`; prose; row C1-13 withdrawn); INV-118 (Predicate, Reading, Conformance, Evidence, Notes); OC-35; E-029 (`omn` comment, Conformance); section 3.4; section 4.2; INV-068 Evidence; OUT-029 traceability row; ISS-09; section 9; `RATIONALE.md` |
| R38-02: INV-049 and INV-096 ask for their series at every granularity a reader can select | yes, by script (`verify_gran.py`, `scenarios.py`) | fixed: INV-096 with one granularity of the diary's choice (`∃ g`); INV-049 by the review's first way (the view for every time range, the series left to E-039 and INV-050) | INV-096 (Predicate, Reading, Notes); INV-049 (Predicate, Reading, Notes); section 3.4; `RATIONALE.md` |
| R38-03: ISS-10 counts four adult-only sources and omits [S-002] | yes, against Stage 1 OUT-018 and section 5 | fixed, the review's first option (count [S-002]) | ISS-10 (Stage 1 field) |

Unchanged: every quote; every source-data row; every case-table row except C1-13; every level of an existing case; every Realises field; the Elements, Invariants and Catalogue-rows columns of the traceability table; 155 of 160 `omn` blocks.

## 2. R38-01: case C1-13

### Verification

**What C1-13 asked (v37).** `verify_c1.py` lists every case of table C1:

| Case | Key | Granularities | Scopes | Kinds of one pair (their Stage 1 requirements) |
|---|---|---|---|---|
| C1-01 | `oc05`, `must` | `MonthlyKind` | all types | headache days (OUT-004) |
| C1-02 | `oc06`, `must` | `MonthlyKind` | all types | migraine days (OUT-005) |
| C1-03 / C1-04 | `oc07`, `should` / `must` | `MonthlyKind` | all types | moderate/severe headache days (OUT-006) |
| C1-05 / C1-06 | `oc08`, `should` / `must` | `MonthlyKind` | all types | attacks (OUT-007) |
| C1-07 | `oc11`, `should` | `Granularity` | all types | intensity (OUT-010) |
| C1-08 | `oc12`, `should` | `Granularity` | all types | duration (OUT-011) |
| C1-09 | `oc13`, `should` | `Granularity` | all types | each symptom, most bothersome symptom: separate pairs (OUT-012) |
| C1-10 | `oc15`, `must` | `Granularity` | all types | total, class, drug acute-medication days (OUT-014) |
| C1-11 | `oc16`, `should` | `{calendarWeek}` | all types | total acute-medication days (OUT-015) |
| C1-12 | `oc32`, `should` | `Granularity` | all types | days affected in three domains, severe impairment (OUT-027) |
| **C1-13** | `oc35`, `must` | **`MonthlyKind`** | **all types and each type, in one case** | **headache days, acute-medication days, moderate/severe headache days and attacks where provided, in one pair (OUT-004, OUT-006, OUT-007, OUT-014)** |
| C1-14 | `oc35`, `should` | `Granularity` | each type | intensity (OUT-010) |

C1-13 is the only case:
- whose single pair joins kinds of several Stage 1 requirements, so that one view and one series must show them all (`reportedTogether`);
- that asks for the acute-medication days of OUT-014 at `MonthlyKind`; C1-10 asks for the same kinds over all types combined at `Granularity`;
- that shares one existential granularity between the combined scope and the type scopes, and among four measures. The other per-type case, C1-14, is a separate case from its combined counterpart C1-07, with the same granularities.

The review's description is correct in every point.

**What Stage 1 asks (verbatim, `stage1match.py`).**
- OUT-029 Statement: "the diary output MUST present frequency and acute medication outputs separately for each headache type (for example migraine and tension-type headache), as well as combined." Strength: "MUST for frequency and acute medication outputs per headache type". No granularity, and no presentation of frequency and acute-medication outputs together. OUT-021, by contrast, says "MUST present together".
- OUT-001: "Frequency outputs MUST be available per calendar month or per 28-day (4-week) period". Section 3.4 reads these as the frequency measures of OUT-004 to OUT-007 (ISS-04).
- OUT-014: "The diary output MUST report, per reporting period, the number of days with acute (symptomatic) headache medication, broken down […] together with the total across classes". By section 3.4, at any granularity; C1-10 states it so. This reading has been settled since review 01 ("INV-023 at any granularity … OUT-001's monthly MUST concerns frequency outputs"; oscillation checks 04 to 32, settled points).

**The narrowing, by script.** `scenarios.py` builds the review's example: a subject with migraine and tension-type headache who uses sumatriptan. Headache days and moderate/severe headache days are shown per calendar month in one view, for every scope; acute-medication days (total, triptans, sumatriptan) are shown per calendar week in another view, for every scope. The evaluation covers 350 admissible contexts.
- v37: C1-01, C1-02, C1-04 and C1-10 hold, and C1-06 is vacuous (no attacks provided). C1-13 fails: no monthly view shows medication days. So the v37 MUST instance of INV-118 is violated.
- v38: every case and every per-type instance holds (headache days and moderate/severe headache days per type at `calendarMonth`, medication days per type at `calendarWeek`).

### Disposition: fixed, option (a)

Stage 1's text decides the question. OUT-029 names no granularity and no joint presentation, and the granularity of each output is fixed by its own requirement. So the model is made faithful, and no Stage 1 issue is recorded (option (b) would record a reading that Stage 1 does not state).

**Why the per-type cases are not four new rows of table C1.** Table C1 is keyed by `(r, l)`, and its keys must be pairwise distinct (section 2.11, "Type checking"). Row `oc35` has only two usable keys: `(oc35, must)` and `(oc35, should)`, the latter used by C1-14. The other levels cannot be used: `may` imposes nothing, and `shouldNot` and `mustNot` are prohibitions. So "each measure as its own case, with its own existential granularity" cannot be written as several `(oc35, must)` rows.

Two other ways were considered and rejected:
- **Adding the per-type pairs to C1-01, C1-04, C1-06 and C1-10.** This would make each per-type measure share the existential granularity of its combined-scope case. A diary showing combined values per calendar month and per-type values per 28-day period would then fail, which Stage 1 permits. It would also differ from the C1-07 / C1-14 pair, which are separate cases.
- **New catalogue rows for each per-type measure, or a third key column of table C1.** Either adds catalogue or table structure that changes every row, for no difference in meaning.

**The fix: the rule stated once.** The per-type requirement is stated as the per-type instance of each combined-scope case (PROCESS.md section 6a, "state a rule once"; the review's heading "state the per-period rule once for every type scope"):
- **Section 4.4.** New defined constant `const byTypeCases : set (CatalogueRow × Level) ≙ {(oc05, must), (oc07, must), (oc08, must), (oc15, must)}`, that is, C1-01, C1-04, C1-06 and C1-10.
- **INV-118.** A second conjunct:
  ```
  (∀ r : CatalogueRow • (r, l) ∈ byTypeCases ⇒
     ∃ g ∈ ppGranularities(r, l) • ∀ c ∈ Ctx • c.granularity = g ∧ #c.subject.possibleHeadacheTypes ≥ 2 ⇒
       ∀ q ∈ ppRequired(r, l, c); t ∈ c.subject.possibleHeadacheTypes • reportedTogether(c, q.2, ofType(t)))
  ```
  The first conjunct is verbatim, now parenthesised.

So, for a subject who has or may have two or more headache types, each measure is asked for each headache type:
- with the granularities of its combined-scope case: `MonthlyKind` for headache days, moderate/severe headache days and attacks (OUT-001), and `Granularity` for acute-medication days (OUT-014);
- with the kinds and conditions of that case: total, class and drug together, as OUT-014 says "together with the total across classes"; `provides(K)` for moderate/severe headache days and attacks;
- with the level of that case (MUST, the OUT-029 part, cited in INV-118 Evidence);
- with a granularity of its own, as C1-07 and C1-14 have;
- with no view shared with another measure.

The combined values of OUT-029 ("as well as combined") are those of C1-01, C1-04, C1-06 and C1-10, which apply to every subject.

**What `byTypeCases` contains, and why.**
- Migraine days (C1-02) are not broken down by type. They are migraine-specific (INV-118/D02, unchanged since v00).
- The weekly view (C1-11) and the overuse indicator (INV-044) are for all types combined (ISS-09). This is unchanged.
- The SHOULD cases C1-03 and C1-05 decide whether a measure is provided at all. Where the diary provides it, C1-04 and C1-06 make its per-type values MUST. This is the same `provides(K)` reading as v37 C1-13.

**Effect on conformance.** Every repertoire that meets v37 C1-13 meets the new conjunct. Proof: take the granularity g₀ ∈ `MonthlyKind` of C1-13. Then g₀ ∈ `ppGranularities` of all four cases. Each case's kinds are a subset of C1-13's kinds, and `reportedTogether` is monotone in its kinds. The script confirms this on a v37-style diary that shows one monthly view per scope with all kinds: both versions hold.

The v38 rule no longer asks for:
- acute-medication days per calendar month or 28-day period;
- one view with the frequency measures;
- one granularity shared by all kinds, or by the combined and the type scopes.

INV-122, which binds per-type values to combined values shown in one view, is unchanged.

**IDs.** C1-13 is withdrawn (PROCESS.md section 7) and listed in section 9 with the items its content went into. Its ID is not reused, and no new C1 row is created. The `RATIONALE.md` entry C1-13/D01 is kept and states the withdrawal.

### What changed, and where

- **Section 4.4.**
  - `omn` block: the constant `byTypeCases`.
  - Prose: one sentence on `byTypeCases`.
  - Table C1: row C1-13 removed.
- **INV-118.**
  - Predicate: second conjunct.
  - Reading: second sentence.
  - Conformance: MUST cases now C1-01, C1-02, C1-04, C1-06, C1-10, and the per-type instances of C1-01, C1-04, C1-06, C1-10.
  - Evidence: OUT-029 (MUST) for the per-type instances.
  - Notes: own granularity of each per-type instance; C1-13 withdrawn; INV-118/D04.
- **OC-35.**
  - Period and granularity: per measure.
  - Availability: "MUST (INV-118, `byTypeCases`: C1-01, C1-04, C1-06 and C1-10 for each headache type)".
- **E-029.**
  - `omn` comment on `medicationKinds`: "row C1-10; per headache type: byTypeCases".
  - Conformance: "per headache type MUST (INV-118, C1-10 by `byTypeCases`)".
- **Section 3.4**, second paragraph: the per-type monthly cases.
- **Section 4.2**: the formal force of the catalogue includes `byTypeCases`.
- **INV-068 Evidence**: "as in INV-118 (C1-10) and INV-104".
- **Traceability, OUT-029 coverage line**: per type, `byTypeCases`; combined, C1-01, C1-04, C1-06, C1-10.
- **ISS-09 Effect**: C1-10 combined, `byTypeCases` per type.
- **Section 9.**
  - Intro sentence.
  - New row C1-13.
  - Row INV-028 points to it.
- **`RATIONALE.md`.**
  - New INV-118/D04 (the reading and the design reasons).
  - INV-118/D03: the v35 equivalence qualified for the withdrawn case.
  - C1-13/D01: withdrawal.
  - Six moved v34 texts named the withdrawn case "INV-118 (C1-13)": SEC-3.4/D01, E-012/D01, E-064/D03, INV-073/D01, INV-089/D01 and INV-118/D01. They now name its v38 place, "INV-118 (`byTypeCases`)". This is the moved-text exception for a reference to a merged item (`RATIONALE.md` section 1).
  - INV-118/D02 (v34 INV-028 Notes) is unchanged. It is still accurate, and INV-118/D04 cites it for the content of `byTypeCases`.

### The class and the sweep

**Class:** availability requirements per type scope, and joint presentations, that differ in granularity or co-presence from the counterpart that Stage 1 makes them a version of.

| Item | Counterpart | Result |
|---|---|---|
| C1-13 | C1-01, C1-04, C1-06, C1-10 | Fixed (above). |
| C1-14 (intensity per type) | C1-07 | Same granularities (`Granularity`), own case, SHOULD where provided. This matches "Where the intensity summary of OUT-010 is provided, it SHOULD also be presented separately for each headache type". Its kinds omit C1-07's `scale ≠ ∅`, but E-023 `scale` is SHOULD on every intensity summary, so at the case's level (SHOULD) the two ask the same. Unchanged. |
| C1-02 (migraine days) | — | Not per type (INV-118/D02). Unchanged. |
| C1-11, INV-044 | — | Weekly view and overuse indicator for all types combined (ISS-09). Unchanged. |
| C1-10 (one pair: total, class, drug) | — | One Stage 1 output: "together with the total across classes" (OUT-014). Unchanged. |
| C1-12 (one pair: three domains and severe impairment) | — | One Stage 1 output, listed in one sentence: "the number of days on which headache affected paid work or school, household work and social or leisure activities, including days with severe functional impairment" (OUT-027). Not a combination of separate requirements. Unchanged. |
| C1-09 | — | Each symptom is its own pair, so no joint view. Unchanged. |
| INV-122 | — | Per type ≤ combined, only where one view shows both. Definitional, no availability. Unchanged. |
| Scope ties: E-045, E-046, INV-062 (`scopeFor`); INV-073, INV-088, INV-089 (`onlyOfType`, `scopeFor`); INV-091 to INV-093, INV-115 (`concerns`) | — | They fix which scope a value has, not its availability, granularity or co-presence. Unchanged. |
| Comparisons (INV-037, INV-039), response comparisons (INV-055 to INV-057), treatment review (INV-068) | — | Over all types combined, as in v37. OUT-029 asks for the outputs per type, and v37 C1-13 did not extend to comparisons either. Unchanged. |

After the fix, no case joins kinds of different Stage 1 requirements in one pair (`verify_c1.py` on v38). Every per-type availability has the granularities of its combined counterpart: C1-07/C1-14 as in v37, and the four `byTypeCases` instances by construction.

**Watch points.**
- The per-class and per-drug kinds that R01-06 / fix 01 added are kept: `medicationKinds(c)` is used unchanged through C1-10.
- No watch point names C1-13 or INV-028.
- INV-118's quantification (`∃ g` before `∀ c`) is kept in both conjuncts.
- The kinds of every remaining C1 case are byte-identical: 0 case or source-data rows changed besides the removed C1-13.

## 3. R38-02: INV-049 and INV-096

### Verification

`verify_gran.py` lists every invariant that quantifies over `Ctx`:

| Binding of a series' granularity | Invariants (v37) |
|---|---|
| one granularity of the diary's choice (`∃ g` before `∀ c ∈ Ctx`) | INV-118 (table C1), INV-034 (first conjunct, `MonthlyKind`), INV-040 (`MonthlyKind`), INV-044 (`MonthlyKind`) |
| calendar weeks, where Stage 1 names them | INV-034 second conjunct (`c.weeklyGranularityRelevant`, OUT-009); C1-11 (OUT-015) |
| **every granularity: `tiles(sr, c.timeRange, c.granularity)` under an unrestricted `∀ c ∈ Ctx`** | **INV-049 (first conjunct), INV-096 (series conjunct)** |
| no series tied to the selected granularity | INV-027, INV-037, INV-039, INV-055, INV-071, INV-077, INV-081, INV-083, INV-086, INV-088, INV-094, INV-095, INV-102, INV-103 |

No output-scope invariant uses `ctx.granularity`. The review's finding is confirmed: INV-049 and INV-096 are the only two invariants that tie a series to the reader-selected granularity for every context.

Stage 1 (verbatim):
- OUT-036 (b): "(b) report school days missed or impaired and the impact on parents or caregivers (for example their lost productive time)". No period, no granularity.
- OUT-017: "SHOULD show headache days and acute medication days from the start of withdrawal onward". No granularity.
- Weekly values are asked only by OUT-009 ("Where weekly granularity is clinically relevant (tension-type headache, cluster headache, early onset of effect), weekly values SHOULD be available") and OUT-015 ("the diary output SHOULD show acute medication days per calendar week").

`scenarios.py` reproduces both examples of the review.
- **A child with migraine.** School days and caregiver impact are shown per calendar month and per 28-day period. v37 INV-096 fails for the 136 weekly contexts; v38 holds with g = `calendarMonth`. With calendar months only, v37 fails for 340 contexts of the other two granularities; v38 holds. For a subject who becomes an adult on 15 March 2026, with values for 28-day periods that begin in childhood only, v37 fails for 124 contexts; v38 holds with g = `fourWeekPeriod`. The `let C` restriction to childhood periods works as before.
- **A withdrawal that started on Monday 2 February 2026.** The follow-up series is in 28-day periods.
  - With a weekly series in views shorter than 28 days, v37 INV-049 fails for 9 weekly contexts (time ranges of 4 or more weeks, which a 28-day series fills but does not tile at the weekly granularity); v38 holds.
  - With the review's literal example (28-day series only), v37 fails for 12 contexts and v38 INV-049 holds.
  - With the v37 form (a series of the selected granularity), both versions hold.

### Disposition: fixed

**INV-096.** The series conjunct is quantified as the general rule does:

`(∃ g ∈ Granularity • ∀ c ∈ Ctx • c.granularity = g ∧ childOn(c, c.timeRange.from) ⇒ …)`

The body is verbatim. The PedMIDAS conjunct is the same formula, with `∀ c ∈ Ctx` distributed over the two conjuncts.

`Granularity`, not `MonthlyKind`: OUT-036 (b) names no granularity. This matches the functional-impact days of OUT-027 (C1-12).

The review's alternative, moving these values into table C1 as cases of OC-42, was not taken. A case of `ppRequired` asks for pairs that one view shows for every period of the series. INV-096, however, asks only for the periods that begin while the subject is a child or adolescent (`let C`), and in one of two forms (days affected, or days missed and days impaired). A case can state neither, so the move would change the meaning (INV-096/D02).

**INV-049.** The review's first way is taken. The first conjunct asks, for every context whose time range begins on a start of withdrawal and ends within the following year, for a follow-up view with `v.withdrawalStart = ws ∧ sameSpan(v.covers, c.timeRange)`. It no longer asks `∃ sr ∈ v.series • tiles(sr, c.timeRange, c.granularity)`.

The series of the view is that of E-039 (`series`, SHOULD when `wholePeriodFrom`) and INV-050 (start tie, `fillsPeriod`), both unchanged. Its granularity is the diary's choice in each view. For a time range of whole periods of the selected granularity, a series of that granularity still spans it exactly (INV-050/S01). A series of another granularity fills it up to fewer days than one of its periods at the end, and the values of the covered period include those days (INV-050).

Why not a literal `∃ g` over the contexts of INV-049:
- A granularity whose periods cannot begin on a start of withdrawal (calendar months, for any start that is not the first day of a month) would leave that start with no view for its time ranges. This would reverse, in substance, R11-03's guarantee and fix 12's "every start of withdrawal" for past follow-up years. The running-follow-up conjunct covers only an as-of date within the year.
- The review's other way, "∃ g over a granularity whose periods can begin on every start of withdrawal", leaves only `fourWeekPeriod`. That would fix the granularity at 28-day periods, which Stage 1 does not name.

So the "granularity of the diary's choice" of the general rule is applied per view, not per diary. The same holds for the views that INV-094/INV-104 and INV-095/INV-105 ask for every context: their series fill the covered period at a granularity that does not depend on the reader's selection.

**E-039 kept.** E-039 `series` asks for a series wherever a whole period that begins on the start of withdrawal fits in the covered period. In a view of 7 to 27 days that begins on the first day of a calendar week, that is a series of calendar weeks. The script finds 3 such views for the review's literal example (time ranges of 1, 2 and 3 weeks): they deviate from E-039 at SHOULD, as they already did in v37. In v37 they also failed INV-049. In v37, as in v38, a running follow-up view of the first four weeks after such a start fails E-039 in the same way.

This is the content of a view of a given covered period: the series of whole periods within it, which INV-104 and INV-105 also state. It is not a tie to the reader-selected granularity. The review's own option leaves it in place, and E-039 `series` belongs to a watched pair (check 08, watch point 4; check 12, watch point 5). It is unchanged (INV-049/D02).

### What changed, and where

- **INV-096.**
  - Predicate: `∃ g ∈ Granularity` before the series conjunct; `∀ c ∈ Ctx` distributed.
  - Reading: "For the contexts of one granularity, of the diary's choice, …".
  - Notes: "Granularity: section 3.4", and INV-096/D02.
- **INV-049.**
  - Predicate: the conjunct `∃ sr ∈ v.series • tiles(sr, c.timeRange, c.granularity)` removed.
  - Reading: "…, and it covers that time range."
  - Notes: "The view's series, of a granularity of the diary's choice: E-039 `series`, INV-050", and INV-049/D02.
- **Section 3.4**, first paragraph. The general rule now also covers values that Stage 1 asks for without naming a period: the school days and caregiver impact of OUT-036 (b), which INV-096 asks for. The rule is stated once there, and INV-096 refers to it.
- **`RATIONALE.md`.**
  - New entries INV-049/D02 and INV-096/D02.
  - INV-096/D01: its last sentence is qualified ("for the contexts of one granularity").
  - INV-049/D01, INV-049/S01, INV-049/W01, INV-050/S01, E-039/D02 and E-006/D01 are still accurate and unchanged.

### The class and the sweep

**Class:** every invariant that ties a series or value to the reader-selected granularity, or quantifies "for every context" over granularity, checked against the granularity that Stage 1 names for that output (table above).

After the fix, `verify_gran.py` on v38 finds:
- no invariant with `tiles(…, c.granularity)` under an unrestricted `∀ c ∈ Ctx`;
- INV-096 binds `∃ g ∈ Granularity`;
- INV-049 has no series tie;
- INV-034, INV-040 and INV-044 are unchanged, and INV-118 keeps `∃ g` before `∀ c` in both conjuncts.

The weekly bindings that remain (INV-034 second conjunct, C1-11, INV-104's weekly acute-medication series) are those Stage 1 names (OUT-009, OUT-015). The content rules that choose a series by the length of a covered period (E-039, INV-104, INV-105, INV-041) do not depend on the reader's selection.

**Watch points kept.** By script, the `omn` blocks of these items are byte-identical to v37: E-006 (`fillsPeriod`, 28-day anchor), E-039 (`series` `when`, `reviewWindow` without `when`), INV-050 (start ties, `fillsPeriod`, no end tie), INV-051, E-008, INV-001, INV-034, INV-040, INV-044, INV-104, INV-105, INV-097, E-030 and E-031.

INV-049 keeps, verbatim:
- the running-follow-up conjunct (v11);
- `∀ ws ∈ c.subject.withdrawalStart` (v12);
- `<` (v17);
- `sameSpan(v.covers, c.timeRange)` (v05).

The removed tie is not one of check 08 watch point 4's items, which are re-adding the end tie, or loosening `fillsPeriod` or the start tie, of INV-050 and E-039. It had been carried unchanged since v00 and was never discussed. Its removal rests on evidence that neither the fix-03 nor the fix-05 sweep considered: Stage 1's granularity statements, raised in R38-02. INV-096's age reading (check 12) is unchanged.

## 4. R38-03: ISS-10

### Verification

- **Stage 1 OUT-018** cites nine sources (`stage1match.py`): [S-002], [S-008], [S-011], [S-015], [S-016], [S-018], [S-028], [S-033] and [S-035].
- **[S-002]'s Stage 1 citation** is "Guidelines of the International Headache Society for controlled trials of preventive treatment of migraine attacks in episodic migraine in adults" (verbatim, Stage 1 section 5). It concerns preventive treatment of migraine, and adults only.
- **ISS-10's account before the fix.**
  - It named four adult-only sources: AAN/AHS 2026 [S-018], SIGN 155 [S-016], EHF 2022 [S-011] and the Russian recommendations for adults [S-033]. These are the readings of E-041/D02.
  - It named four further sources: NICE CG150 [S-015], IHS 2024 [S-008], NVN [S-028] and the Turkish protocol [S-035].
  - It left out [S-002].
- **The count is wrong under the widened scope.** "Five of them concern adults only" is correct for "Every guidance that Stage 1 cites for OUT-018".
- **History (`isshist.py`, `issdiff.py`).** The ISS-10 "Stage 1" field changed only in v07. The word diff v06 → v07 shows "quotes for these time points" replaced by "Stage 1 cites for", with the count left unchanged, as the review says.

### Disposition: fixed (the review's first option)

ISS-10, "Stage 1" field, now reads: "… and five of them concern adults only (AAN/AHS 2026, SIGN 155, the EHF 2022 guideline, the Russian clinical recommendations for adults, and the IHS guidelines for controlled trials of preventive treatment of episodic migraine in adults [S-002], which name durations and analysis periods of trials, not evaluation time points for a person's treatment, E-041/D01)."

The clause on [S-002] restates E-041/D01. This is text only. Effect on the model and For the human are unchanged.

The second option (restoring the v06 scope "that OUT-018 quotes for these time points") was not taken. The "cites" wording was set by fix 07 and is the scope the sentence's later clauses use: NICE, IHS 2024, NVN and the Turkish protocol are cited for OUT-018, whatever their time points.

### The class and the sweep

**Class:** a count or list in a section 8 description that a later widening of its scope left stale. Every field of ISS-01 to ISS-13 was traced through `history/v00.md` … `history/v37.md` (`isshist.py`), and every later change was word-diffed (`issdiff.py`).

| Issue and field | Later change | Count or list after the change | Result |
|---|---|---|---|
| ISS-03 Stage 1 | v20: OUT-008, OUT-019, OUT-030, OUT-020, OUT-002 and OUT-007 added to the lists | The lists name the requirements; review 38 checked them against every Stage 1 Statement that mentions migraine | correct |
| ISS-04 Stage 1, Effect | v04: the OUT-001 reading added; v35: references renamed | The cases named are the four combined-scope frequency cases | correct. Effect still names C1-01, C1-02, C1-04 and C1-06, the cases of OUT-001's combined values; the per-type instances are stated in section 3.4 |
| ISS-06 Effect | v02, v03: change from baseline; any other instrument | no count | correct |
| ISS-09 Stage 1, Effect | v01 / v35 | Effect named C1-13 | Updated for R38-01. The Stage 1 field's Group D description without OUT-017 is settled (reviews 25b, 31) |
| ISS-10 Stage 1 | v07: scope widened | "four" → "five" | fixed (above) |
| ISS-10 Effect | v12, v14: ages on the start of treatment; Turkish 7.3 | The lists of guidance for children match E-041 (SD-ER ages) | correct |
| ISS-11, ISS-12 For the human | v21, v35: the closing paragraph moved | no count | correct |
| ISS-01, ISS-02, ISS-05, ISS-08, ISS-13 | none after their first version (Evidence only moved in v35) | ISS-02 "the one use"; ISS-08 "four levels" | correct (review 38 verified ISS-02 p. 139; SD-CL has four levels) |

No other stale count or description was found.

## 5. All changed locations

**`OUTPUT_MODEL.md`:**
- header: Version line and Companion line;
- section 3.4: both paragraphs after the `reportedTogether` block;
- section 4.2: the "formal force" sentence;
- section 4.3: row OC-35;
- section 4.4: the `omn` block, the prose paragraph, and table C1 (row C1-13 removed);
- E-029: the `omn` comment and Conformance;
- INV-118: Predicate, Reading, Conformance, Evidence, Notes;
- INV-049: Predicate, Reading, Notes;
- INV-068: Evidence;
- INV-096: Predicate, Reading, Notes;
- section 7: the OUT-029 coverage cell;
- ISS-09: Effect on the model;
- ISS-10: Stage 1;
- section 9: intro, row INV-028, new row C1-13;
- section 12: entry v38.

**`RATIONALE.md`:**
- header;
- SEC-3.4/D01, E-012/D01, E-064/D03, INV-073/D01, INV-089/D01, INV-118/D01: the reference to the withdrawn case;
- C1-13/D01: the withdrawal;
- INV-118/D03: qualified;
- INV-096/D01: qualified;
- new entries INV-118/D04, INV-049/D02, INV-096/D02.

## 6. Diff summary of formal blocks and case-table rows

`omn` blocks: 160 in v37 and in v38. 5 changed and 155 are byte-identical (`checks38.py`).

| Block | Change | Remark |
|---|---|---|
| section 4.4 | added: `const byTypeCases : set (CatalogueRow × Level) ≙ {(oc05, must), (oc07, must), (oc08, must), (oc15, must)}`, with a comment | R38-01 |
| E-029 | comment only: `(table C1, rows C1-10 and C1-13)` → `(table C1, row C1-10; per headache type: byTypeCases)` | R38-01 (reference to the withdrawn row) |
| INV-118 | first conjunct verbatim, parenthesised; second conjunct added (section 2 above) | R38-01 |
| INV-049 | first conjunct: `∧ ∃ sr ∈ v.series • tiles(sr, c.timeRange, c.granularity)` removed; the rest verbatim | R38-02 |
| INV-096 | `∀ c ∈ Ctx` distributed over the two conjuncts; series conjunct prefixed with `∃ g ∈ Granularity •` and antecedent `c.granularity = g ∧`; both bodies verbatim | R38-02 |

Case-table and source-data rows: 129 in v37 and 128 in v38 (outside section 9). The only change is C1-13, withdrawn; no row was added, and every other row is byte-identical. Catalogue rows: only OC-35 changed (informative cells). No level of an existing case or invariant changed. INV-049 and INV-096 stay SHOULD.

## 7. Check results

| Check | Result |
|---|---|
| IDs (`checks38.py`, reviewer's `model_ids.py`) | 67 E, 87 INV and 12 ISS headings, no duplicate. 0 unresolved E-, INV- or ISS- references in the model or `RATIONALE.md`. 0 unresolved row references (C1-13 resolves to its section 9 row). The withdrawn C1-13 is referenced only in the INV-118 Notes, section 9 (intro, its row, row INV-028), the change log and `RATIONALE.md` (C1-13/D01, INV-118/D03, INV-118/D04). |
| `RATIONALE.md` entries, both directions | 437 entries (113 Q), no duplicate. 367 model → `RATIONALE.md` references and 402 internal references, 0 unresolved. Every entry except the C1/C2/C3 D01 entries (cited generically in section 4.4) and the search-log entries SL-001 to SL-035 is cited from the model, the three new entries included. |
| Evidence pointers | Unchanged from v37. The two informational findings (E-041/Q29 and E-057/Q10 hold more sources than the pointer cites) are the same in v37. |
| Brace balance | 160 `omn` blocks balanced. 1 unbalanced backticked span in the model, the same one as in v37 (section 2.11 prose with nested backticks, a regex artefact). `RATIONALE.md`: none. |
| Declared names (reviewer's `names.py`) | Same output as on v37. `byTypeCases` is declared once (section 4.4) and used in INV-118; `ofType` and `possibleHeadacheTypes` are declared. |
| Traceability (`trace.py`) | 39 rows. The Catalogue-rows, Elements and Invariants columns equal the values recomputed from the Realises fields (0 differences). Every OUT in a catalogue row's Realises is realised by an item the row names. Every OUT is in some row. |
| Catalogue "def." lists (`defcheck.py`) | For all 45 rows, "def." equals the definitional invariants whose Conformance names an element of the row, minus those stated once (section 4.2): 0 differences. |
| Quotes | All 704 double-quoted strings of v37 (model and `RATIONALE.md`) are present in v38. Strings quoted in the changed text: "frequency and acute medication outputs per headache type", "present frequency and acute medication outputs separately for each headache type [...] as well as combined", "present together", "per reporting period", "together". All are verbatim Stage 1 v18 (OUT-029 Strength and Statement, OUT-021, OUT-014). |
| Scope terms | Counts unchanged from v37. No input, storage or derivation-from-input text added. |
| Stage 1 wording and level (`stage1match.py`) | Per-type instances: MUST (OUT-029 MUST). Their granularities are `MonthlyKind` for C1-01, C1-04 and C1-06 (OUT-001, "Frequency outputs MUST be available per calendar month or per 28-day (4-week) period") and `Granularity` for C1-10 (OUT-014, "per reporting period"). Kinds as OUT-014 ("together with the total across classes"); no joint view (OUT-029: "separately … as well as combined"). INV-096: SHOULD, one granularity (OUT-036 (b), no granularity). INV-049: SHOULD, series granularity free (OUT-017, no granularity). ISS-10: count matches the nine sources cited for OUT-018. All quoted fragments found verbatim. |
| Satisfiability (`scenarios.py`, 350 admissible contexts per subject) | See below. |
| Snapshots | `cmp OUTPUT_MODEL.md history/v38.md` and `cmp RATIONALE.md history/v38-rationale.md`: identical. |

**Satisfiability, in detail.**
- **INV-118 (v38 MUST instance).** It holds together with INV-002, INV-003, INV-004, INV-006, INV-024, INV-121, INV-122 (including per type ≤ combined in one view) and INV-123 (`usedScope`), with 0 structural findings. This holds for the review's example and for the v37-style diary.
- **INV-096 (v38).** It holds with C1-12, INV-003, INV-004, INV-006, INV-121 and INV-122 (0 findings), for three child scenarios.
- **INV-049 (v38).** It holds with INV-050, E-039 (series and review window), INV-051, INV-003, INV-121, INV-006 and INV-123 (0 findings) for a diary that follows E-039.
- **Monotonicity.** Each change only removes or weakens a requirement. v37's witnesses satisfy v38, so no new conflict with other invariants is possible.

## 8. Watch points (oscillation checks after iterations 04 to 36)

- **No watch-point decision is reversed.**
  - INV-049: running follow-up, every start of withdrawal, `<`, `sameSpan`.
  - INV-050 and E-039, byte-identical: start ties, `fillsPeriod`, the 28-day anchor in E-006, no end tie, `reviewWindow` without `when`.
  - INV-118's quantification: `∃ g` before `∀ c`, kept in both conjuncts.
  - The kinds of the C1 cases: byte-identical; R01-06's per-class and per-drug kinds kept through `medicationKinds`.
  - The settled "INV-023 at any granularity" (now C1-10) is kept, and now also applies per headache type.
  - INV-096's age reading and ISS-10's "Effect" and "For the human" fields (check 08, watch point 3) are unchanged.
- **Volume.**
  - Formal: 5 `omn` blocks, 1 of them a comment; 1 case-table row withdrawn.
  - Prose: the items listed in section 5.
  - Each formal change removes or weakens a requirement that Stage 1 does not state. The one addition, `byTypeCases` with the INV-118 conjunct, replaces C1-13 with a weaker rule.
