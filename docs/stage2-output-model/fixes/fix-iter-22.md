# Fix log — iteration 22
Input review: reviews/review-iter-22b.md · Input version: v21 · Output version: v22
Date: 2026-10-21

## What was read and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026);
- v21 (`OUTPUT_MODEL.md`, byte-identical to `history/v21.md` and to HEAD):
  - sections 1–4, E-001 to E-009, E-039 and E-066 to E-067;
  - INV-001 to INV-004, INV-049 to INV-052 and INV-094, INV-095, INV-104 and INV-105;
  - the traceability table, section 9, the search log of iterations 16–21 and the change log;
  - the other elements and invariants in outline, with every use of `fillsPeriod`, `containsPeriodOf`, "whole periods", "grid" and "first day" found by search;
- re-check 22b (one remark, R22b-01) and review 22 (no remarks).

**Earlier loop files read, so that no fix is undone:**
- R03-04 (review 03) and fix 03. R03-04 (i) asked: "Require the series to consist of all whole periods of its granularity within the covered period". Fix 03 adopted the review's formula and checked it only by construction ("consecutive 28-day periods from the first covered day").
- Fix 05 (R05-01). It moved INV-105 to `containsPeriodOf` and `fillsPeriod`, and kept INV-050's start tie. Its satisfiability script built 28-day series "from the first day".
- Review 06: "`fillsPeriod` still excludes a one-period series of a long covered period (the R03-04 guarantee)"; review 05 says the same. For `mostRecent` (INV-041), review 06 found that "Stage 1 fixes no grid for 28-day periods".
- Fix 16: the granularity of the overview's series is not fixed by Stage 1 (R05-01, unchanged).
- The oscillation checks after iterations 08, 12 and 16:
  - **Watch point 4 (iteration 08), repeated after iterations 12 and 16.** INV-050 and E-039: "re-adding the exact end tie, or loosening `fillsPeriod` or the start tie" would be oscillation.
  - **Watch point 1 (iteration 16).** The treatment-effect conjunct of INV-105.
  - **The settled points**, among them "INV-050 and E-039".

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**No download and no web search.** The remark concerns a predicate of the model. It was checked against the Stage 1 text in the repository and against v21.

**Scripts.** All are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix22/` and were run with `python3 -I`.
- **`fills22.py`.** It implements `ofKind` (E-005), `within`, `consecutive` (INV-004) and `fillsPeriod` over calendar dates, in three forms:
  - literally as written in v21, by brute force over every pair d₁ ≤ d₂ in p;
  - by enumerating the spans of kind g within p;
  - as a min/max test.

  The three forms agree:
  - enumeration against min/max: 560,753 and 574,836 candidate series in the two runs;
  - literal against the other two: 5,727 + 14,065 and 5,459 + 16,738 series;
  - 0 mismatches.

  The v22 form adds the new conjunct. Calendar weeks were tested under both week conventions (Monday and Sunday first), because `isWeekSpan` (section 2.8) leaves the convention to the output.
- **`run_review.py`.** The review's three examples and its length count.
- **`sat22c.py`.** The satisfiability and rejection checks (see "Satisfiability").
- **`cmp2122.py`.** v21 against v22 on random covered periods.
- **`mech22.py`.** The mechanical checks of PROCESS.md section 11, with a per-block comparison of all `omn` blocks with v21.

## Verification of the remark

The remark is correct. By script, with `fillsPeriod` evaluated literally as written in v21:

| Review example | Covered period | Series | v21 | v22 |
|---|---|---|---|---|
| (A) exact run of 28-day periods | 5 Jan – 29 Mar 2026 (84 days) | 19 Jan–15 Feb, 16 Feb–15 Mar | admitted | rejected; the only admitted 28-day series is 5 Jan–1 Feb, 2 Feb–1 Mar, 2 Mar–29 Mar, the three selected periods |
| (B) one period of a longer covered period | 1 Mar – 9 May 2026 (70 days) | 22 Mar–18 Apr | admitted | rejected; admitted: 1–28 Mar, 29 Mar–25 Apr (14 days left at the end) |
| (C) six-month summary | 1 Jan – 1 Jul 2026 (182 days) | five periods, 28 Jan – 16 Jun | admitted | rejected; admitted: six periods from 1 January, 1 Jan – 17 Jun (14 days left) |

**The review's count.** For every covered length from 56 to 399 days (344 lengths), the script looked for a 28-day series with one period fewer than fit.
- **v21** admits one for 332 lengths. The 12 exceptions are exactly the lengths of 27 mod 28, as the review states.
- **v22** admits none.

**On random covered periods** (3,000 periods of 28 to 800 days; `cmp2122.py`):
- **v21:**
  - it admits 82,594 different 28-day series;
  - it admits more than one 28-day series for 2,997 of the periods;
  - it admits a series with fewer periods than fit for 2,797 of the periods.
- **v22:** it admits exactly one 28-day series for each period (3,000 in all).
- **Calendar months and calendar weeks:** no series has a different verdict in v21 and v22.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R22b-01 | fixed (the review's option (a), form (a1): an anchor) | **E-006:** Definition (`fillsPeriod`, one conjunct), Meaning, Notes. **INV-104:** Reading, Notes. **INV-105:** Reading, Notes. **INV-050:** Notes (one phrase). **Section 7:** rows OUT-034 and OUT-035, coverage reason only. | **Formal change.** One conjunct is added to `fillsPeriod` (E-006):<br>`(sr.granularity = fourWeekPeriod ⇒ first(sr.periods).start = p.start) ∧   -- 28-day periods are counted from the first day of p`<br>Together with the unchanged conjuncts (`within` the covered period; no whole period of the granularity before the first or after the last period), a 28-day series now consists of the consecutive 28-day periods from the first day of the covered period that end within it. That is as many as fit, ⌊lengthDays ÷ 28⌋, with fewer than 28 days left at the end and none at the start. This is exactly what the model's text claimed: "consists of all whole periods of its granularity within the covered period", "cannot shrink to a single period of a longer covered period", and "Where the covered period is a run of whole periods, a series of their granularity spans it exactly".<br>**Why (a1) and not (a2) or (b).**<br>1. **(a2), maximality only.** It would still leave the place of the series open wherever the length is not a multiple of 28. In example (B), offsets of 0 to 14 days would all be admitted. "All whole periods of its granularity within the covered period" would then remain undefined for 28-day periods, and the text of E-006, INV-104 and INV-105 would still need the corrections of option (b) for those lengths.<br>2. **(b), keep the predicate and correct the text.** It would keep a time course, and medication-overuse indicators, for 28-day periods that are not the selected periods and are one fewer, for the summary and the overview of a selected time range (INV-094, INV-095). The review shows that the selected time range has a grid of its own, the one INV-001 gives it.<br>3. **(a1) follows the model's own convention for 28-day periods,** which have no calendar grid:<br>• INV-001 counts the periods of the selected time range from its first day;<br>• INV-050 counts the follow-up series from the start of withdrawal, which is the first day of the covered period;<br>• the satisfiability constructions of fix 03, fix 05 and the INV-104 and INV-105 Notes count 28-day periods from the first day of the covered period.<br>It also matches the Stage 1 OUT-009 evidence on 28-day time courses: [S-005] "each 28-day interval can also be compared with baseline to demonstrate the trajectory of response", intervals counted from the start of the observed period.<br>**Fidelity.** The change does not narrow Stage 1.<br>• Stage 1 fixes no alignment of 28-day periods within a summary period. The model must fix one so that "all whole periods" has a meaning.<br>• INV-104 and INV-105 are existential, SHOULD-level requirements. A view may show further series, for example 28-day periods aligned to the end of the covered period (open world, section 3.7).<br>• Calendar months and calendar weeks are unchanged. So is the free choice of granularity in INV-104 and INV-105 (fix 16: granularity "not fixed by Stage 1").<br>**`mostRecent` (INV-041) is not touched.** Review 06's "Stage 1 fixes no grid for 28-day periods" concerns the most recent periods before the as-of date. Here the grid is relative to a covered period whose first day the output states.<br>**Text** (each paraphrase now matches the predicate):<br>• **E-006 Meaning.** It states the anchor and what "all whole periods of its granularity within p" is for each granularity: the whole calendar months or calendar weeks within p, or the consecutive 28-day periods from the first day of p that end within p. It says why 28-day periods are counted from the first day (they do not follow the calendar; as INV-001 counts the selected time range), and that fewer than 28 days are left after the last period and none before the first.<br>• **E-006 Notes.** 28-day periods are counted from the first day of the covered period; for the withdrawal follow-up view, that day is the start of withdrawal (INV-050).<br>• **INV-104 and INV-105 Readings.** "(28-day periods counted from its first day)" after "all whole periods of its granularity within the covered period".<br>• **INV-104 and INV-105 Notes.**<br>  – The meaning of the series for each granularity.<br>  – "up to fewer days than one period at either end (for 28-day periods, at its end only)".<br>  – "cannot shrink to a single period of a longer covered period" is made precise: "cannot shrink to a single period where two or more whole periods of its granularity fit in the covered period". A 43-day covered period, or 5 January – 29 March with calendar months, has a one-period series, and the old wording, read literally, denied that.<br>  – Where the covered period is a run of whole periods of one granularity, a series of that granularity consists of exactly these periods. For a summary of the selected time range (INV-094), or an overview of it (INV-095), that is the periods into which INV-001 divides it.<br>• **INV-050 Notes.** The same "shrink" phrase, made precise in the same way ("… whole periods of its granularity from the start of withdrawal fit in the covered period"). Its "as INV-104 and INV-105 do" is now true for 28-day series as well.<br>• **Rows OUT-034 and OUT-035.** "28-day periods counted from its first day (`fillsPeriod`, E-006)" is added to the description of the time course.<br>**Not changed:**<br>• the predicates of INV-050, INV-104 and INV-105;<br>• `containsPeriodOf`, `wholePeriodFrom`, `tiles`, `summaryTimeCourse` and `mostRecent`;<br>• E-039, INV-049, INV-094 and INV-095;<br>• the E-067 Notes ("over all whole periods within it"), which are true under the E-006 definition;<br>• every Conformance, Realises and Evidence field, and the Elements and Invariants columns of section 7.<br>**Oscillation.**<br>• Watch point 4: `fillsPeriod` is tightened, not loosened; the start tie of INV-050 is unchanged; no exact end tie is added, so a 28-day series may still end up to 27 days before the covered period does.<br>• INV-050 is unchanged in effect: for every series that begins on the start of withdrawal, the v21 and v22 verdicts agree (0 differences by script).<br>• This is the completion of R03-04 (i) that the review names, on evidence no earlier loop file examined: offset 28-day series. It reverses no fix.<br>• The INV-105 watch points of iteration 16 (the treatment-effect conjunct) are untouched. |

## Satisfiability

`sat22c.py` was run twice:
- weeks starting on Monday, seed 7;
- weeks starting on Sunday, seed 2022.

Each run evaluated `fillsPeriod` with the v22 conjunct on three sets:
- 4,000 random covered periods of 1 to 800 days, starting between 2020 and 2029. INV-001 bounds a chosen period and the period since the previous consultation only by the as-of date, so each of these is a covered period of a clinician-facing summary that INV-094 can require, and of a patient-facing overview, which may cover any period (R05-01);
- 1,500 runs of 1 to 14 whole periods of a random granularity, each starting on a first day of its granularity (the selected time ranges of INV-001);
- 3,000 withdrawal follow-up views from a random start of withdrawal, of 1 to 800 days.

| Check | Monday weeks | Sunday weeks |
|---|---|---|
| **(i) A conforming series exists where an invariant requires one.** | | |
| INV-104, monthly conjunct: a calendar month or 28-day period fits (`containsPeriodOf`), so a monthly series with `fillsPeriod` is needed: the 28-day series from the first day, or the whole calendar months | 3,874 needed, 0 failures | 3,848 needed, 0 failures |
| INV-104, the two weekly conjuncts: a calendar week fits, so the whole calendar weeks are needed | 3,954, 0 failures | 3,945, 0 failures |
| INV-105: a whole period of some granularity fits | 3,954, 0 failures | 3,945, 0 failures |
| E-039, INV-050 (the running follow-up of v11; a covered period from the start of withdrawal to any end): a whole period that begins on the start of withdrawal fits (`wholePeriodFrom`), so a series from the start of withdrawal with `fillsPeriod` is needed | 2,907 of 3,000 views, 0 failures | 2,917 of 3,000, 0 failures |
| INV-049, first conjunct: a time range of whole periods from the start of withdrawal, ending within the following year; its tiling series meets `fillsPeriod` | 1,183, 0 failures | 1,179, 0 failures |
| Runs of whole periods (the selected time range of INV-001, for INV-094 and INV-095): for each granularity, the only admitted series is the run itself, so it is spanned exactly | 1,500, 0 failures | 1,500, 0 failures |
| **(ii) Shifted and one-period-short series are rejected.** | | |
| Uniqueness: for every covered period and every granularity, among all consecutive series within it, exactly the construction is admitted (none where no whole period fits) | 0 failures | 0 failures |
| 28-day series shifted by 1 to 27 days, with as many periods or one fewer | 151,910 tested, 0 admitted | 151,103 tested, 0 admitted |
| One period short (the first or the last period dropped), all granularities | 22,606 tested, 0 admitted | 22,434 tested, 0 admitted |
| An admitted 28-day series begins on the first day and leaves fewer than 28 days at the end | 0 failures | 0 failures |
| **INV-050 unchanged in effect.** Every series that begins on the start of withdrawal has the same verdict under v21 and v22 | 0 differences | 0 differences |

**The other invariants on the same views are unaffected:**
- INV-003, INV-006 and INV-011, the medication-overuse indicators of INV-104 (INV-044 to INV-046), and INV-051 and INV-052;
- the admitted 28-day series is the one that the v21 satisfiability arguments already built, so every argument that used it still applies.

The clinician summary of a `chosenPeriod` (R11-03) is covered by the random covered periods: they have any dates and any length, including 1 to 27 days. The patient overview of an arbitrary period (R05-01) is covered by the same set.

## Other changes

- **Bookkeeping:**
  - the header (v22, iteration 22, under review);
  - section 9 ("as of v22");
  - one search-log paragraph for iteration 22: no web search, no download and no new source; the script check;
  - the v22 change-log entry.
- **Items changed: 10 fields in 6 items:**
  - E-006 (Definition, Meaning, Notes);
  - INV-050 (Notes);
  - INV-104 (Reading, Notes);
  - INV-105 (Reading, Notes);
  - rows OUT-034 and OUT-035 (coverage reason only).

  Bookkeeping comes on top. One `omn` block changed, by one added line. No Predicate, Conformance, Realises or Evidence field, no Elements or Invariants column, and no source row changed.

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), none missing and none duplicated. Issues: ISS-01 to ISS-06 and ISS-08 to ISS-12. ISS-07 appears only as withdrawn. |
| References | No dangling E-, INV- or ISS- reference. 36 distinct S references, all within S-001–S-046 or S-101–S-106. Exactly the 39 Stage 1 OUT IDs are referenced. |
| Fields | Each of the 177 items has exactly one Realises, one Conformance and one Evidence field, and at most one Notes field. Each element has one Definition and one Meaning; each invariant has one Predicate and one Reading. |
| Fields changed against v21 | Definition: E-006. Meaning: E-006. Reading: INV-104, INV-105. Notes: E-006, INV-050, INV-104, INV-105. No Conformance, Realises, Evidence or Predicate field changed. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every requirement, the row's E and INV sets equal the reverse index of the Realises fields: 0 mismatches. Only the coverage reasons of OUT-034 and OUT-035 changed; no Elements or Invariants column changed. |
| Formal text | 181 `omn` blocks; 180 are byte-identical to v21. The one that differs is the E-006 block, with one added line, the new conjunct of `fillsPeriod` (diff `@@ -14,0 +15 @@` of that block). |
| Types and names | 305 declared paragraph names, none declared twice; no new name. Every identifier of `fillsPeriod` is declared: `Series`, `Period`, `Date`, `within`, `ofKind`, `periods`, `granularity`, `start`, `end`, `fourWeekPeriod`; `first` and `last` come from section 2.6. The new conjunct is well typed:<br>• `sr.granularity : Granularity ⊆ PeriodKind` is compared with the `PeriodKind` constant `fourWeekPeriod`;<br>• `first(sr.periods)` is defined because `periods` is `seq1`;<br>• `.start` and `p.start` are `Date`. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. 0 violations. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33; total 110, unchanged. Every MUST NOT and SHOULD NOT predicate begins with `¬`, and no MUST or SHOULD predicate does. |
| Diff against v21 | `git diff -U0`: 13 hunks, 29 lines added and 11 removed:<br>• line 2: the header;<br>• line 364 (new): the `fillsPeriod` conjunct;<br>• lines 368 and 372: E-006 Meaning and Notes;<br>• line 2590: INV-050 Notes;<br>• lines 3477 and 3481: INV-104 Reading and Notes;<br>• lines 3502 and 3506: INV-105 Reading and Notes;<br>• lines 3572–3573: rows OUT-034 and OUT-035;<br>• line 3663: section 9;<br>• two lines after the iteration-21 search-log paragraph;<br>• fifteen lines after the v21 change-log entry.<br>No other line changed. |
| Quotes | No source quote added or changed. The quoted strings on the added lines are the model's own text, quoted in the change log. |
| Scope sweep | The added lines were searched for enter/entry, record, input, captur, logged, store/storage, persist, database, JSON, XML, CSV, FHIR, HL7, serializ/serialis, encod, retention, reminder, answer, algorithm, obtained, calculat, comput, field, questionnaire, "derived from", "decision logic" and diagnos. The only hit is "field", for the document's own fields. The new conjunct relates two output elements, the first period of a series and the covered period of its view. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v22.md`: identical. `history/v21.md` is unchanged (equal to HEAD). |
