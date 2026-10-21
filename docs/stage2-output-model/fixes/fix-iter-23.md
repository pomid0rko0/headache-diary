# Fix log — iteration 23
Input review: reviews/review-iter-23.md · Input version: v22 · Output version: v23
Date: 2026-10-21

## What was read and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026);
- v22 (`OUTPUT_MODEL.md`, byte-identical to `history/v22.md` and to HEAD):
  - sections 1–4, E-001 to E-033 and the frame invariants INV-001 to INV-013;
  - every element and invariant with an open end, a duration or a time span: E-032, E-034, E-035, E-039, E-047 to E-049, E-051 to E-055, E-060 to E-065 and E-067, and INV-045, INV-046, INV-049 to INV-052, INV-077 to INV-079, INV-086 to INV-090, INV-109 and INV-110;
  - section 7, ISS-12, section 9 and the change log of v14–v22;
  - the other items by search, for every use of `ongoing`, `lastDay`, `asOf`, `covers.end`, `covers.start`, "has ended", "has not ended" and "end of the covered period";
- review 23 (one remark, R23-01).

**Earlier loop files read, so that no fix is undone:**
- **R01-08 and R02-05 (reviews 01, 02; fixes 01, 02).** Both cited E-063 `lastDay` as the model for an open end. Fix 02 chose the as-of date, not the end of the covered period, for the duration of a treatment that has not stopped. Its reasons were that "has not stopped" is itself judged as of that date (INV-001), and that two end points must not be mixed.
- **R04-04 and the fix-04 sweep** ("a property of the next unit lost at the end of a covered period"). The sweep found none and named E-063 `ongoing` and `lastDay` as the reason.
- **R05-03 (fix 05).** The rate relation of INV-089.
- **R09-01 (fix 09).** `onlyOfType` for cluster rates.
- **R13-01 (fix 13).** `scopeFor` in INV-088.
- **R14-02 (fix 14).** The acute summaries of the cluster view are tied to the covered period.
- **R21b-01 / ISS-12 (fix 21).** The "> 3 months" remission bound of the Definitions of terms.
- **The oscillation check after iteration 16:**
  - its watch points 1–8;
  - its settled points: "the '> 3 months' readings of INV-045 and INV-089"; "the period of a cluster attack rate within its bout (INV-089, unchanged since v09)"; "INV-087 and the lead-in"; "INV-049 and INV-050".
- **The history of `ongoing` and `lastDay`.** By search in `history/v00.md` to `history/v22.md`: the comment of `ongoing`, the definition of `lastDay`, the E-063 Meaning sentence and the INV-089 Reading have been unchanged since v00. So v23 changes them for the first time, and this is not a return to an earlier state.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**No download and no web search.** The remark concerns the meaning of an attribute and a predicate of the model. No source, quote or value changes. The ICHD-3 remission sentence that INV-089 rests on ([S-001] p. 209, quoted in E-063) was checked by reviews 21b and 23 and is not touched.

**Scripts.** All are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix23/` and were run with `python3 -I`.
- **`cluster23.py`.** It implements the first three conjunct groups of INV-089 literally, under v22 and under v23:
  - the phase conjunct (with `lastDay`, `plusMonths` and `days` of section 2.8);
  - the order and non-overlap conjuncts;
  - a rate's period within its bout.

  It also implements the overlap antecedent of INV-088. It runs the review's examples and further cases.
- **`cmp2223.py`.** v22 against v23:
  - exhaustively over a 10-day window for views of the current period (covered period ending on the as-of date);
  - at random for views of the current period and of a past period.
- **`sat23.py`.** Satisfiability on truthful cluster views built from random histories of bouts and attack-free periods.
- **`mech23.py`.** The mechanical checks of PROCESS.md section 11, with a per-block comparison of all `omn` blocks with v22.

## Verification of the remark

The remark is correct. These are the results of `cluster23.py` with v22 as written. The as-of date is 21 October 2026 in every case.

| Review example | Output | v22 | v23 |
|---|---|---|---|
| **1.** Bout 10 Jul – 20 Aug 2026; view 1 Jan – 31 Jul 2026 | comment reading: `ongoing`, no end, duration 22 days (10–31 Jul) | admitted | rejected |
| | Meaning reading: not ongoing, end 20 Aug, duration 42 days | admitted | admitted |
| **2.** Bout 10 Dec 2025 – 10 Feb 2026; view 1–31 Jan 2026 | comment reading: `ongoing`, duration 53 days (10 Dec – 31 Jan) | admitted | rejected |
| | Meaning reading: not ongoing, end 10 Feb, duration 63 days | admitted | admitted |
| **3.** Bout 1 Mar – 31 May 2026; attack-free from 1 Jun to the as-of date (143 days) | view 1 Jan – 31 Jul: remission `ongoing`, duration 61 (v22 `lastDay` 31 Jul) | rejected | rejected |
| | view 1 Jan – 31 Jul: remission `ongoing`, duration 143 (to the as-of date) | rejected | admitted |
| | view 1 Jan – 21 Oct (ends on the as-of date): remission `ongoing`, duration 143 | admitted | admitted |
| **4.** Attack-free 1 Jun – 15 Oct 2026 (137 days), then a bout from 16 Oct | view Jan – Jul, comment reading: remission `ongoing`, duration 61 | rejected | rejected |
| | view Jan – Jul: remission ended 15 Oct, duration 137 | admitted | admitted |
| | the same, with the later bout from 16 Oct shown as `ongoing` | rejected | admitted |

`plusMonths(1 Jun 2026, 3)` is 1 September 2026, which lies after 31 July and on or before 21 October.

**What the script confirms:**
- **Examples 1 and 2.** v22 admits both readings, so the set of valid outputs depends on the reading.
- **Example 3.** v22 cannot show the remission in a view of 1 January – 31 July, under either reading. It can show it in a view that ends on the as-of date.
- **Bouts after a past covered period.** In a view of a past period, v22 cannot show as `ongoing` a bout that is still running on the as-of date but began after the covered period (example 4, last row).
- **Rates of an ongoing bout.** In v22, a rate of a bout that has not ended is cut at the end of the covered period. A rate of August 2026 for a bout from 1 July that is still running is rejected in a view of January – July.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R23-01 | fixed (the review's option (a)) | **E-063:** Definition (comment of `ongoing`; `lastDay`), Meaning, Notes. **INV-089:** Predicate (one conjunct added), Reading, Notes. **E-062:** Notes. **Section 7:** row OUT-031, coverage reason only. | **One meaning of `ongoing`.** `ongoing` now means "the period has not ended by the as-of date of the output". This is how the model already judges whether a treatment has stopped (E-055, INV-079): on course events dated on or before the as-of date (INV-001).<br>• The comment reads `-- the period has not ended by the as-of date of the output`.<br>• `lastDay` of an ongoing period is the as-of date: `{d : Date \| (x.ongoing ∧ d = ctx(outputOf(x)).asOf) ∨ (¬ x.ongoing ∧ d ∈ x.end)}`. This is the review's formula.<br>• The E-063 Meaning and Notes, the INV-089 Reading and the E-062 Notes now state that meaning in the same words. No text of v23 reads `ongoing` relative to the covered period.<br>**New conjunct of INV-089:** `(∀ e ∈ x.end • e ≤ ctx.asOf)`, so an end date shown lies on or before the as-of date. This is the other half of the same meaning: a period that is not ongoing has ended by the as-of date. Without it, a period still running on the as-of date could be shown as ended, with an end date after the as-of date. Its duration and the remission bound would then rest on a date that no diary information gives. In a view of the current period, v22's own comment of `ongoing` already implied the conjunct.<br>**Effect** (`cluster23.py`, table above):<br>• Every bout and remission period is shown with its own dates and duration, whatever period the view covers. A period that ended after the covered period shows its end and its whole duration (example 1: 42 days). A period that has not ended shows its duration to date, as a treatment line does.<br>• The remission bound is tested on the whole attack-free period, to its end or, while it continues, to the as-of date. A remission period that the ICHD-3 Definitions of terms recognise as of the as-of date can therefore be shown in a view of any covered period it overlaps (example 3).<br>• The ambiguity is gone: the two outputs of examples 1 and 2 that v22 admitted under the comment reading are rejected.<br>**Unchanged in form** (as the review asks):<br>• INV-088 (overlap with the covered period);<br>• the order, non-overlap and rate-within-bout conjuncts of INV-089, and the rate relation.<br>For an ongoing bout, `lastDay` is now the as-of date, which lies on or after the end of the selected time range (INV-001). So the INV-088 overlap test requires a rate for exactly the same bouts as before. A rate's period lies within the bout's own extent, which review 15 settled as "a rate over any period within the bout".<br>**Why (a) and not (b).** Option (b) keeps `ongoing` relative to the covered period. It would then need a new derived element, an end-or-as-of date, to test the remission bound, and two end points for one item. Fix 02 rejected that mix for treatment lines. Option (a) needs no new name: `ctx`, `outputOf` and `asOf` are declared. It follows the time frame the model uses for treatment courses (INV-079, INV-109) and for cycle lines that have ended (E-060 Notes: shown to the day before the next first day of menstruation "whether or not the next cycle is shown in the view").<br>**Side effect.** In v22, `lastDay` used `viewOf(x).covers.end`, the covered period of the view the item is part of. Bouts are referenced by the cluster view (`→ClusterPeriodItem`), so that view need not be the cluster view. `lastDay` now depends only on the output's as-of date, which is the same for every atom of an output (rule W1).<br>**Fidelity.**<br>• OUT-031 asks for bouts and remissions "with their start dates, end dates and durations, using the ICHD-3 definitions". v23 shows each period's own dates and duration, and the remission duration of the Definitions of terms ("To be considered a remission, the attack-free period must exceed three months", [S-001] p. 209, quoted in E-063) is tested on the attack-free period, not on its part within a reporting period.<br>• No level, value, Realises field or Evidence field changes.<br>**Text** (each paraphrase now matches the predicate):<br>• **E-063 Meaning.** What an ongoing period is, and what one that has ended shows.<br>• **E-063 Notes.** The relations now include the end-date bound. The end-date obligation applies to "a period that has not ended by the as-of date, such as a current bout". A new **Time frame** paragraph gives the review's examples: the bout of 10 July – 20 August 2026, 42 days, in a view of January – July; and the attack-free period from 1 June 2026, 143 days, shown as an ongoing remission period in such a view.<br>• **INV-089 Reading.** The one meaning, the end-date bound, the duration to date and the remission bound to the end or the as-of date.<br>• **INV-089 Notes.** A Time frame paragraph and satisfiability.<br>• **E-062 Notes.** The length of a remission period is that of the whole attack-free period.<br>• **Row OUT-031.**<br>**Not changed:**<br>• the "> 3 months" bound (`remissionMoreThanMonths`), ISS-12 and the E-063 Evidence;<br>• INV-088, `onlyOfType`, `scopeFor`, `summarisesMedication`, and the period of the cluster view's acute summaries (R14-02);<br>• the rate relation (R05-03), INV-008, INV-011, E-064 and every other item. |

## Same defect elsewhere

I checked every item with an open end, a duration or a time-span bound for the same two defects: two meanings of "not ended", or a length tested only up to the end of the covered period. No other instance was found.

| Item | Open end, duration or bound | Finding |
|---|---|---|
| E-063, INV-089: bouts and remission periods | `ongoing`, `lastDay`, duration, the "> 3 months" bound | Fixed (R23-01). |
| E-064, INV-089: cluster attack rates | rate period within its bout | Follows from `lastDay`: the bout's own extent. No separate defect. |
| E-060, INV-087: cycle lines | `complete`, `cycle.to`, `nextWindowDays`, `completeCycles` | **No instance.**<br>• `complete` has one meaning, "the line has ended". A line that has ended is shown to the day before the next first day of menstruation, also when that day lies after the covered period (E-060 Notes, INV-087 Notes, R04-04). So the window days −2 and −1 of the next menstruation are not lost at the end of the covered period.<br>• A line that has not ended is shown to the end of the covered period. But a cycle line has no duration and no length bound, and nothing that the view shows depends on its days after the covered period. `completeCycles` counts only lines within the covered period, as the E-060 Notes state.<br>• The menstrual-relation view is a watch point (iteration 16, item 7). Not changed. |
| E-055, INV-079, INV-109: treatment lines | stop date, duration, span of the course | **No instance.** `stopped` is judged on course events dated on or before the as-of date (INV-001). The duration and the course span run to the stop or to the as-of date, whatever the history view covers (E-055 Notes). |
| E-039, INV-049 to INV-051: withdrawal follow-up | review window (4 to 8 weeks), "the following year" | **No instance.**<br>• Both are fixed spans anchored on the start of withdrawal (INV-051, E-039 Notes). Neither is an open end with two meanings.<br>• The review window is required once the covered period reaches its end (INV-050), and its dates do not depend on the covered period.<br>• Watch point; not changed. |
| E-049, INV-070: post-stop monitoring | periods after the event | **No instance.** Consecutive periods from the first day of the changed regimen; no open end and no length bound. |
| E-053, INV-074: treated-attack lines | onset date | **No instance.** No end and no duration. |
| E-047, INV-066, INV-067: adherence | evaluation window | **No instance.** A closed span tied to an on-treatment period of the comparison (`adherenceFor`). |
| E-032, INV-045, INV-046: medication-overuse span | "> 3 months" span | **No instance.** The span runs backwards from the indicated period, with periods of its own that INV-003 shows in the view, whatever the covered period. The bound is tested on the span itself. |
| E-034, E-035, INV-035: treatment markers | dated events | **No instance.** Point events within the covered period; no duration. |
| E-042, INV-055, INV-058, INV-059: time points | "on treatment" through an interval | **No instance.** Judged on course events up to the as-of date (`notStoppedBefore`, `intervalOnTreatment`), not at the end of a covered period. |
| E-013 Notes, INV-011 Reading | "cluster periods and remissions … summarise the diary information of the view's covered period" | **Checked, not changed.** The indicator is still asked for the covered period of a view that shows cluster phases. That such an item may reach beyond the covered period was already so in v22: a bout that began before the covered period was shown with its real start, and previous bouts are shown as history. The sentence remains true: these items summarise the covered period's information, among other information. |

## Other changes

- Header: "Version: v23 · Iteration: 23 · Status: under review".
- Section 9: "(as of v23)".
- Section 12: change-log entry for v23.

No other item was changed.

## Satisfiability

The changed constructs were checked together with every invariant that constrains the same elements: E-062 to E-064, INV-088, INV-089, INV-008 and INV-011 (and INV-003, which places the periods), and INV-110.

- **INV-089 (v23) and INV-088, on truthful views (`sat23.py`).**
  - **Setup.** Two seeds (3 and 2026), 20,000 views each. Each view comes from a random history of alternating bouts (7–119 days) and attack-free gaps (1–699 days). The covered period ends on the as-of date (two thirds of the views) or 1 to 399 days before it. The view shows every phase that overlaps the covered period, plus the earlier bouts. Each item has:
    - its own start;
    - its end if it has ended by the as-of date, and otherwise `ongoing`;
    - its duration to its end or to the as-of date.

    A gap is shown as a remission period when it lasts more than three months to its end or to the as-of date. Every bout that overlaps the covered period has a per-day and a per-week rate over its part within the covered period.
  - **Result.**
    - INV-089 holds in 40,000 of 40,000 views.
    - The INV-088 rate requirement is met in every view.
  - **The same histories under v22.** v22, read by its attribute comment, rejects 1,169 and 1,143 of these views. These are exactly the views that show a remission period whose bound fails at the end of the covered period.
- **INV-088.**
  - The overlap antecedent is unchanged for every bout. For an ongoing bout, the as-of date is not earlier than the start of the selected time range, because that range ends on or before the as-of date (INV-001).
  - The rate it requires can have the part of the bout within the covered period as its period. That part is not empty for an overlapping bout: the bout's start is on or before the end of the covered period, its last day is on or after the start of the covered period, and its start is on or before its last day.
  - The scope (`scopeFor`) and the acute summaries of the covered period (R14-02) are untouched.
- **INV-089, rate relation.** It is unchanged. Its `n ÷ p.lengthDays` is defined for every period (`lengthDays` ∈ ℕ₁).
- **INV-003, INV-011 and INV-008.**
  - A rate's period may now end after the covered period, up to the as-of date. INV-003 places that period in the view, and INV-011 asks for its completeness indicator. An indicator for any period can be added: covered days not above the period length, scope all types, as INV-012 requires.
  - The covered-period indicator for a view with cluster phases is unchanged.
  - The attack definition label (INV-008, INV-010) can be added to any view.
- **INV-110.** It concerns the trigger co-occurrence view only, does not mention cluster phases, and is unchanged.
- **Definedness.**
  - `days(s, e)` in INV-089 is guarded by `s ≤ e` in the same conjunction (section 2.6).
  - `ctx(outputOf(x)).asOf` is total: `outputOf` and `ctx` are total functions (E-002, section 3.2).
  - The new conjunct quantifies over `x.end`, an `opt Date`, as section 2.6 requires.
- **Views of the current period behave as in v22 (`cmp2223.py`).** Where the covered period ends on the as-of date, the last day of an ongoing period is the same in v22 and v23.
  - **Exhaustive check.** Two covered periods ending on the as-of date (21 Oct 2026, from 1 Oct and from 15 Oct). Bouts and remission periods with every start and end over 14–23 Oct (or none), both `ongoing` values, and seven durations (1, 3, 5, 7, 8, 9 and 10 days) or none. 7,744 single-item views. The verdicts of INV-089 and of the INV-088 overlap antecedent:
    - agree in 7,616 views;
    - differ in 128 views, all of which show an end date after the as-of date and are rejected by v23 only;
    - differ in no other view.
  - **Random check.** Views of 0–2 bouts and 0–2 remission periods, with rates, and as-of dates from 2024 to 2027.
    - Seed 1: 200,000 views; 198,908 agree; 1,092 differ, and each of these shows an end date after the as-of date.
    - Seed 23: 200,000 views; 198,868 agree; 1,132 differ, all for the same reason.
    - Seed 7, with every end date on or before the as-of date: 200,000 of 200,000 agree.
  - So, for a view of the current period, v23 behaves exactly as v22 except that it excludes an end date after the as-of date. v22's own comment of `ongoing` already excluded that date in such a view; v23 makes it formal.
  - **Past periods.** For views of a past period (seed 5), 5,030 of 200,000 verdicts differ. This is the intended change.

## Oscillation

- `ongoing` and `lastDay` have been unchanged from v00 to v22, so v23 does not return to an earlier state.
- No watch point of the iteration-16 check is touched:
  - INV-105;
  - `acuteMedications` and E-062 `acute`;
  - the acute and adherence identity ties;
  - responder labels;
  - E-041;
  - INV-098;
  - co-presence;
  - the menstrual-relation view;
  - the withdrawal follow-up view;
  - the E-008 time frames.
- **The settled points are kept.**
  - The "> 3 months" reading of INV-089 is unchanged (`plusMonths(s, remissionMoreThanMonths) ≤ e`).
  - ISS-12 is unchanged.
  - The rate's period still lies within its bout.
  - The type-scope ties of R09-01 and R13-01 are unchanged.
  - The covered period of the cluster view's acute summaries (R14-02) is unchanged.
- **The R02-05 choice is extended, not reversed.** Fix 02 already preferred the as-of date to the end of the covered period for an open end. v23 applies the same choice to cluster phases.
- **The fix-04 sweep is completed.** Its reason for finding no instance ("The ongoing cluster period has `ongoing` and `lastDay`") was the defect that R23-01 found.

## Checks

Run by script (`mech23.py`) on the final `OUTPUT_MODEL.md`, against `history/v22.md` and Stage 1 v18.

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110): none missing, none duplicated. Issues ISS-01 to ISS-06 and ISS-08 to ISS-12 (ISS-07 withdrawn, section 9). |
| References | No dangling E-, INV- or ISS- reference. 36 source IDs, all within S-001 to S-046 or S-101 to S-106. 39 OUT IDs referenced, all in Stage 1. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant one Predicate, Reading, Conformance, Realises and Evidence field. No item has more than one Notes field. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal, for every row, the items whose Realises field names the requirement: 0 mismatches. Rows changed: OUT-031 only, in its coverage reason. No Elements or Invariants column changed. |
| Conformance levels | Invariants: definitional 33, MUST 19, SHOULD 48, SHOULD NOT 8, MUST NOT 2, unchanged. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. Attributes: 172 level-annotated declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. No typing-rule violation. No Conformance, Realises or Evidence field changed. |
| Types and names | 305 declared paragraph names, the same as in v22, none declared twice. The identifiers on the changed `omn` lines are `ClusterPhaseItem`, `Date`, `ongoing`, `end`, `ctx`, `outputOf` and `asOf`, plus the level keyword `core` and the primitive `𝔹`. Each is declared: `ctx` (section 3.2), `outputOf` (E-002), `asOf` (E-007), `end` and `ongoing` (E-063). `ctx(outputOf(x))` has type `OutputContext`, and `.asOf` has type `Date`. In INV-089, `ctx` is the context of the output (output scope, section 2.9), as in its rate conjunct. |
| Changed `omn` blocks (diff against v22) | 181 blocks in both versions. Two differ:<br>• **E-063.** The comment of `ongoing` (`-- the period continues at the end of the period the view covers` → `-- the period has not ended by the as-of date of the output`). In `lastDay`, `d = viewOf(x).covers.end` → `d = ctx(outputOf(x)).asOf`, and the comment `-- the end date, or the end of the covered period while ongoing` → `-- the end date, or the as-of date while ongoing`.<br>• **INV-089.** The first line gains `(∀ e ∈ x.end • e ≤ ctx.asOf) ∧`. |
| Changed fields (diff against v22) | E-062 Notes; E-063 Definition, Meaning and Notes; INV-089 Predicate, Reading and Notes; row OUT-031. Also the header, the section 9 sentence and the change log. `git diff --stat`: 1 file changed (OUTPUT_MODEL.md), 18 insertions and 11 deletions, before the snapshot was written. |
| Scope sweep of the added text | No hit for record, enter, input, capture, store, database, serialisation, JSON, XML, CSV, FHIR, encoding, retention, persist, reminder, data field, data-entry, entry or logged. The new relations take output elements (dates, durations, `ongoing`) and the context's as-of date as arguments. |
| Snapshot | `history/v23.md` is byte-identical to `OUTPUT_MODEL.md` (`cmp`; SHA-256 2dd7f6c7…b968 for both). `history/v22.md` equals the model at HEAD. |

**Items changed: 3 model items (E-062, E-063, INV-089; 7 fields; 2 `omn` blocks) and 1 traceability row (OUT-031), plus the header, section 9 and the change log.**
