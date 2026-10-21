# Fix log — iteration 05
Input review: reviews/review-iter-05.md · Input version: v04 · Output version: v05
Date: 2026-10-21

## What was downloaded and checked

No FROZEN_ITEMS.md exists, and the oscillation check after iteration 04 froze nothing, so no item is frozen.

**Earlier work read so that no fix is undone.** The reviews and fix logs of iterations 01 to 04 and oscillation/check-after-iter-04.md were read. The three watch points of that check are respected:
- **Start of the menstrual-relation view and the lead-in (INV-087, E-060).** Not touched. The cycle-line conjunct of INV-105 is unchanged.
- **The menstrual-relation view as a whole.** No change to E-060, E-061, INV-086 or INV-087.
- **INV-104.** Not touched. R05-01 applies the INV-104 pattern to INV-105; it does not loosen the R02-02 (a) condition or the R03-04 tie.

The iteration 03 change to INV-050 (covered period tied to the series, the R03-04 kind) is kept in substance: the series of the withdrawal follow-up view still begins on the start of withdrawal and still consists of all whole periods of its granularity within the covered period (`fillsPeriod`), so it cannot shrink to one period of a longer covered period.

**Downloads.** All went with `curl` into a fresh directory under `/tmp` (`/tmp/fix05-dl-ABsY`), outside the repository. PDFs were extracted with `pdftotext -raw` and `-layout`, and the Europe PMC full text with its markup removed. Scripts were kept in the session scratchpad and run with `python3 -I`.
- **[S-008] IHS 2024 practice recommendations** (Stage 1 URL, univaq PDF, HTTP 200).
  - Q5 (p. 11) and Q6 (p. 12): the success criteria are those "that determine whether preventive therapy is effective and should be continued according to the recommendations provided in Q5".
  - The Q6 Background (p. 12) places the evaluation after "a two- to three-month evaluation period (starting once the maximally tolerated dose has been reached)".
  - The Q6 Evidence (p. 13) measures the MIDAS improvement from the "baseline score" (the E-045 quote reads as quoted).
  - So the score components compare a score at the evaluation of the preventive therapy with the pre-treatment baseline score. This supports R05-02.
- **[S-023] DMKG/ÖKSG/SKG consensus** (Europe PMC full text of PMC9607711, HTTP 200). The Stage 1 OUT-020 sentence with "um mindestens 5 Punkte oder [...] um mindestens 30 % sinkt" reads as quoted.
- **[S-007] IHS cluster headache trial guideline** (Stage 1 URL, UCL Discovery accepted manuscript, HTTP 200, 39 pages; PDF page = manuscript page, checked from the page footers).
  - Section 2.2 "Specific patient populations and attack characteristics", Recommendations, item a (p. 10): "a persistent high attack frequency (e.g. ≥ 14 attacks per week on average)". Found verbatim; the "≥" has a text mapping in this PDF.
  - The Stage 1 OUT-031 quotes "Number of attacks per day during the study period" (p. 22) and "the number of weekly attacks for the entire double-blind phase" (p. 25) were also found.
  - These are attack rates over a period longer than one day or one week, that is, averages per day or per week. This supports the R05-03 relation.
- **[S-001] ICHD-3** (Stage 1 URL, HTTP 200): downloaded for reference; no new quote.
- **Stage 1 v18.** Sections 1–3 were read in full, with OUT-017, OUT-020, OUT-031 and OUT-035 in detail.

**No new source and no new web search.** The only new quote is a fragment of the Stage 1 source S-007. Every double-quoted string new in v05 (16) was checked by script: each is a substring of Stage 1 v18, of v04 or of the downloaded source text.

**Verification of each remark before fixing.**
- **R05-01 holds.**
  - INV-105 (SHOULD, every `PatientOverview`) required `tiles(sr, spanOf(v.covers), sr.granularity)`.
  - The review's covered period, 10 March to 21 April 2026 (43 days), contains no run of whole calendar months, 28-day periods or calendar weeks that spans it exactly. Checked by script.
  - OUT-035 names no period, and its purpose ("so that patients can follow the effect of their treatment and prepare consultations") makes the period since the previous consultation a natural covered period.
  - INV-095 only asks for an overview of the selected time range, which INV-001 makes tileable. So there is no contradiction between invariants, but INV-105 excludes an overview that Stage 1 permits.
- **R05-02 holds.**
  - v04 `scoreMet` and `scoreDecided` accept any shown result with any baseline result.
  - Review example 1 (MIDAS 18 on 5 January, 12 on 30 March, treatment start 1 April, June label): the pre-treatment pair (30 March, baseline 5 January) met "≥ 5 points for baseline 11–20", so INV-063 forced "responder".
  - Review example 2 (DMKG): a label that shows only pre-treatment HIT-6 and MIDAS pairs had every component decided and none met, so INV-063 forced "non-responder".
  - Both were reproduced by script.
- **R05-03 holds.**
  - E-064 `rate` is `derived`, but INV-089 stated only `rate ≥ 0` and that the rate's period lies within its bout.
  - So "10 attacks" in a 7-day period next to "3.0 attacks per day" was admitted.
  - Section 2.7 requires the relation where all its arguments are output elements, which is the case here: the rate, its period's length and the attack count of the same view, period and scope.

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R05-01 | fixed (the review's option (a), the INV-104 pattern) | INV-105 (predicate, Reading, Evidence, Notes); E-067 Notes; E-006 Notes; section 7 row OUT-035 | **Predicate:** the series conjunct `∃ sr • tiles(sr, spanOf(v.covers), sr.granularity) ∧ perPeriod(…)×4` is replaced by two parts:<br>• **always**, headache days, migraine days, an intensity summary and total acute-medication days for the covered period itself (`shownDay(v, …, v.covers, allTypes)`, `∃ m ∈ v.content ∩ IntensitySummary • m.period = v.covers ∧ m.typeScope = allTypes`), so that a short overview still shows them and every day of the covered period is summarised;<br>• **where the covered period contains a whole period of some granularity** (`∃ g : Granularity • containsPeriodOf(spanOf(v.covers), g)`), a series with `fillsPeriod(sr, v.covers)` and the four measures for every period of it.<br>**R03-04 guarantee kept:** `fillsPeriod` excludes a one-period series of a long covered period (checked by script: a one-month series of January–June does not fill it). Where the covered period is a run of whole periods, a series of that granularity still spans it exactly.<br>**Granularity:** left free, as in v04. OUT-035 names none, unlike OUT-034, which brings in the monthly outputs of OUT-001 and OUT-016 and so made INV-104 monthly.<br>**Unchanged:** `plainLanguage`, the treatment-effect conjunct and the cycle-line conjunct (watch point 1).<br>**Migraine days:** still without the OUT-005 condition (ISS-03).<br>**Text:** the Reading and Notes state the reading and its satisfiability; the Evidence quotes the OUT-035 Statement; E-067 Notes; the E-006 Notes now name INV-105 (and INV-050) as users of `containsPeriodOf` and `fillsPeriod`; OUT-035 row. |
| R05-02 | fixed (the review's option (a)) | E-046 (new `evaluationResult`, `pretreatmentBaseline`; `scoreMet`, `scoreDecided`; Meaning, Conformance, Notes); E-045 Meaning; INV-063 Reading; section 7 row OUT-020 | **New predicates (E-046), over output elements and the subject's available results (section 3.5):**<br>• `evaluationResult(L, r)`: r is the latest available result of its instrument that was completed after the `treatmentStart` of the label's response comparison (`rc.treatment = L.treatment`) and within the last evaluated period, `inPeriod(d, last(L.evaluated))`.<br>• `pretreatmentBaseline(L, b)`: b is the latest available result of its instrument that was completed on or before that start.<br>**`scoreMet` and `scoreDecided`** now use only a shown result r with baseline result b such that `evaluationResult(L, r) ∧ pretreatmentBaseline(L, b)`.<br>**Effects:**<br>• a pair of pre-treatment results, a baseline that is not the latest one before the start, or a result outside the last evaluated period decides nothing;<br>• so INV-063 can no longer force "responder" from a change between two pre-treatment administrations, or "non-responder" from pre-treatment results alone;<br>• a result without these dates, or a label without a comparison, decides nothing ("A pair without these dates does not decide the component").<br>**Why "latest" on both sides:** IHS Q6 and the AHS definition measure the improvement from the "baseline score", and the DMKG criterion asks whether the score "sinkt" (falls) under prophylaxis. The baseline is the score before the treatment starts. Without "latest", an older pre-treatment baseline could force "responder" although the score rose under the treatment. Example, checked by script: 25 on 5 January, 12 on 30 March, 14 in June; the 5 January baseline gives a 44 % fall.<br>**Why the last evaluated period:** the score at the evaluation belongs to the end of what the label evaluates (IHS Q6 Background: evaluation after the evaluation period). A result completed after the last evaluated period, for example at the following consultation, is not tied to the evaluated periods by the values shown, so it decides nothing and the reader applies the criterion. The Notes state that this reading is the model's.<br>**Review examples (script):**<br>• example 1: the 30 March / 5 January pair decides nothing; with a July label and the 1 July result, the component is decided and not met (12 → 14);<br>• example 2: the 1 July / 25 March HIT-6 pair is decided and met (63 → 56); the pre-treatment-only pair decides nothing.<br>**Text:** the E-045 Meaning describes `scoreDecrease` as a decrease from the pre-treatment baseline score to the score at the evaluation. The INV-063 Reading and the OUT-020 row are updated. |
| R05-03 | fixed (the review's definitional relation and its optional whole-number relation) | INV-089 (two new conjuncts, Reading, Evidence, new Notes); E-064 (Meaning, Evidence with a new [S-007] fragment, Notes); section 7 row OUT-031 | **New conjunct of INV-089 (definitional):** for every view v, period p and type scope sc with a cluster attack rate, `∃ n : ℕ` such that:<br>• every attack count of v, p and sc equals n (INV-006 allows at most one);<br>• every rate of v, p and sc satisfies `r.basis = perDay ⇒ r.rate ≈ n ÷ p.lengthDays` and `r.basis = perWeek ⇒ r.rate ≈ 7 × n ÷ p.lengthDays`.<br>This gives the review's relation to the shown attack count. It also ties a per-day and a per-week rate of the same period and scope to one whole number of attacks when no count is shown, which was the review's optional relation.<br>**Second new conjunct:** `concerns(ctx, r.typeScope, c3_1)`. E-064 defines the rate as one of *cluster headache* attacks, so a rate over all types for a subject who also has another type would make the relation compare cluster attacks with all attacks. A rate scoped to `ofType(c3_1)` always satisfies it, so INV-088 is unaffected.<br>**Rounding:** `≈` (section 2.7). `p.lengthDays` is in ℕ₁, so `÷` is defined.<br>**Check (script):** 10 attacks in a 7-day period admit 1.4 per day and 10.0 per week, and reject 3.0 per day.<br>**Text:** E-064 Meaning (per day = attacks ÷ days; per week = 7 × that, an average for other lengths), Evidence and Notes (the rate rests on the summarised diary information like every count, and the completeness indicator qualifies its period); INV-089 Reading, Evidence and Notes; OUT-031 row. |

## Other changes

**1. Sweep for the R05-01 kind** (a view whose series must tile its covered period exactly where Stage 1 permits arbitrary covered periods).

Every `tiles` and every covered-period tie in the model was checked:
- **INV-014 to INV-019, INV-108, INV-022, INV-023, INV-025, INV-026, INV-028, INV-029, INV-034, INV-044, INV-049 and INV-096** tile the selected time range (through `tiles`, `reportedPerPeriod` or `reportedTogether`), which INV-001 makes a run of whole periods of the selected granularity. Unchanged.
- **INV-104 (clinician-facing summary)** already uses `containsPeriodOf` and `fillsPeriod`. Unchanged (watch point 3).
- **INV-041 (three-month pattern view).** OUT-028 fixes its covered period to the three most recent months or 28-day periods. Unchanged.
- **INV-035 (time-course view).** Unchanged. OUT-009 asks for the frequency measures "as a time series of consecutive reporting periods", so the view's content is that series, and the period it covers is the span of its whole periods. Every time course over whole periods, including that of the whole periods within any reader-chosen period, is admitted. A larger stated covered period would claim days that the chart does not show. Time courses within arbitrary covered periods are required where Stage 1 asks for them: in the clinician summary (INV-104) and now in the overview (INV-105).
- **INV-050 (withdrawal follow-up view): changed (same kind as R05-01).**
  - OUT-017 asks for headache days and acute-medication days "from the start of withdrawal onward" and continued monitoring "over the following year". The view's start is fixed, but its end is any day, for example the day of the NICE 1.3.48 review 4–8 weeks after the start, or the as-of date of a running follow-up.
  - v04 required `v.covers.end = last(v.series.periods).end`, which no view ending between period boundaries can meet. Its core `series` also excluded a follow-up shorter than one whole period.
  - **E-039:** `series` is now `opt →Series SHOULD when wholePeriodFrom(self.withdrawalStart, self.covers)`. New `pred wholePeriodFrom(d, p)`: a whole calendar month, 28-day period or calendar week that begins on d ends on or before p.end. The `days` term in `ofKind` is guarded by `d ≤ e`.
  - **INV-050:**
    - `v.covers.start = v.withdrawalStart`;
    - headache days and total acute-medication days for the covered period;
    - for the series, if present: it is in the view, begins on the start of withdrawal, fills the covered period (`fillsPeriod`), and has both measures for every period;
    - the review window is required once `v.covers.end` (no longer the series end) reaches 8 weeks after the start.
  - **INV-049** now states `sameSpan(v.covers, c.timeRange) ∧ ∃ sr ∈ v.series • tiles(sr, c.timeRange, c.granularity)`. This keeps, for its tileable time ranges, what INV-049 and INV-050 required together in v04.
  - Also updated: E-039 Meaning, Conformance, Evidence and Notes; INV-049 and INV-050 Reading; INV-050 Evidence and new Notes; OUT-017 row.
  - **Not a reversal of iteration 03.** The tie of the covered period to the series is kept: the series begins on the start of withdrawal and consists of all whole periods within the covered period.

**2. Sweep for the R05-02 kind** (a criterion component evaluated on values not tied to the treatment and periods it refers to).
- **Reduction components.** `reductionMet` and `reductionDecided` used any comparison in `L.comparison`. Only INV-062 (SHOULD) tied that comparison to the label's treatment. Both now require `rc.treatment = L.treatment`, so a reduction is tested only on the comparison of the label's own treatment. The compared periods were already tied to the evaluated periods, and the baseline to `rc.baseline`.
- **Control levels.** INV-064 classified the label by the counts of `L.evaluated`, with no tie of those months to the treatment. The tie existed only in INV-062, at SHOULD, through `ran L.evaluated ⊆ ran rc.onTreatment`.
  - New conjunct: `∀ s ∈ startOf(ctx, L.treatment); p ∈ ran L.evaluated • s ≤ p.start`.
  - The [S-010] levels are goals of its section "Setting goals of migraine burden while on treatment".
  - INV-064 Reading, Evidence and new Notes; E-046 Notes.
  - Satisfiable: on-treatment periods begin on or after the start (INV-056), which is what INV-062 asks.
- **Values shown for score components (INV-062, SHOULD).**
  - INV-062 was met by any result of the instrument, for example pre-treatment results only. After the R05-02 fix, such results decide nothing.
  - OUT-020 asks for "those values as well", the values that the criterion rests on, which for a score component are the evaluation result and the pre-treatment baseline result.
  - New conjunct: for each score component of the criterion whose condition holds, and where a result of its instrument completed after the start within the last evaluated period is available, the label shows the latest such result (`evaluationResult`). Where a pre-treatment result is available, that result shows the latest one as its baseline result (`pretreatmentBaseline`).
  - INV-062 Reading and Notes; E-046 Conformance; OUT-020 row.
  - Satisfiable with E-058, INV-081 and INV-082: both are available results, and the baseline is earlier than the result.
- **Other components.** `judgement` components are never decided, so nothing changed for them.

**3. Sweep for the R05-03 kind** (a computed field shown with its arguments but lacking its relation to them).

Every `derived` attribute was listed by script, with the "Relations" entry in its element's Notes:
- **With their relation already stated:** E-005 `lengthDays` (INV-002); E-013 (INV-012); E-032 (INV-045, INV-046); E-039 `reviewWindow` (INV-051); E-040 (INV-053); E-042 (INV-058); E-052 (INV-074); E-055 `duration` (INV-079); E-058 `category` and `changeFromBaseline` (INV-082); E-060 and E-061 (INV-087); E-063 `duration` (INV-089).
- **Obtained from diary information, with only bounds** (out of scope, section 2.7): E-014 `days`; E-019 `count`; E-023 `summary`; E-024 `value`; E-025 `presence`; E-031 `impact`; E-033 `value`; E-047 `adherence`; E-058 `totalScore`.
- **Two Notes lacked the "Relations" pointer that section 2.7 requires, and now have it:**
  - E-019: INV-006, INV-030, INV-033 and the new INV-089 relation to cluster attack rates;
  - E-051 `treatedAttacks`: INV-074, which relates it to the per-attack lines shown with it.
- **Considered and not changed:**
  - **E-023 `meanPeakIntensity` against a `peakIntensityDistribution` of the same period.** Stage 1 ("an average peak intensity on the scale used") does not say whether the average is over headache days or over attacks. So the distribution of headache days is not its argument under the definitions the output names, and a formula would assume one.
  - **A mean against a total `DurationSummary` and the attack count.** The attacks whose durations are summarised are not stated to be the attacks counted, for example where an attack's duration is not shown.
  - **`treatedAttacks ≤` the attack count.** This is a bound, not a defining relation. The review records it as "not raised".

**4. Satisfiability pass** over every changed invariant and attribute and those that constrain the same elements and views, against INV-001 and the context definitions:
- **INV-105** with INV-095, INV-003, INV-006, INV-008, INV-011, INV-031, INV-032, INV-087, INV-098 and INV-099.
  - Script: 4,000 random covered periods of 1 to 401 days. Wherever the condition holds, a `fillsPeriod` series of some granularity exists, built from the first day for 28-day periods or from whole weeks or months. Where it does not hold, only the covered-period values are needed: 0 unsatisfiable.
  - The review's 43-day example is filled by one 28-day period or by five whole weeks.
  - The overview of an INV-095 time range is tiled exactly.
- **E-039, INV-049, INV-050** with INV-003, INV-011, INV-051 and INV-052.
  - Script: 3,000 follow-up views from a random start of withdrawal, of 1 to 401 days: 0 unsatisfiable.
  - The review window lies within the covered period whenever INV-050 requires it.
  - For INV-049 time ranges, the series tiles them (INV-001).
- **E-046, INV-062, INV-063, INV-064** with E-045, E-058, INV-056, INV-065, INV-069, INV-081, INV-082, INV-100, INV-104 and INV-106.
  - Every change to `scoreMet`, `scoreDecided`, `reductionMet` and `reductionDecided` adds conjuncts, so INV-063 only became weaker (it forces less). Its two forcing antecedents remain mutually exclusive.
  - The new conjunct of INV-064 is met by on-treatment months.
  - The new conjunct of INV-062 is met by the two available results described above.
  - Labels remain MAY.
- **INV-089** with INV-088, INV-006, INV-030, INV-033, INV-003 and INV-011.
  - Take n as the shown count, or as the true number of attacks when no count is shown.
  - Rates scoped to `ofType(c3_1)` satisfy `concerns` and INV-088.
  - Script: rounding is checked for 10 attacks in 7 days and 45 in 30 days.
- **Derived attributes.** No derived attribute is required where its relation is undefined: E-064 `rate` has `lengthDays ≥ 1`; E-039 `reviewWindow` is defined from the start of withdrawal; no new derived attribute was added.
- **Result.** No MUST or SHOULD invariants are jointly unsatisfiable in any admissible context, so no conflict needed fixing. The Stage 1 issue recorded in ISS-06 is unchanged.

**5. Text and bookkeeping.**
- Header "Version: v05 · Iteration: 05 · Status: under review".
- Section 9 "as of v05".
- Section 11: the search-log introduction lists S-007 among the Stage 1 sources checked at their Stage 1 URL, and a paragraph for iteration 05 is added.
- Section 12: the v05 entry.
- Section 10 is unchanged (no new source).
- Section 7 rows OUT-017, OUT-020, OUT-031 and OUT-035 are updated. The element and invariant columns are unchanged, because no Realises field changed.

## Checks

The checks were run by scripts in the session scratchpad (`mech.py`, `names.py`, `levels.py`, `quotes.py`, `scope.py`, `scen.py`) on the final OUTPUT_MODEL.md.

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108). Every ID is present once, with no duplicates and none withdrawn. The headings are in ascending order except INV-108, placed after INV-017 by topic since v04. |
| References | no dangling E-/INV- reference<br>ISS headings: ISS-01–ISS-06, ISS-08, ISS-09; ISS-07 appears only in the section 8 note, the section 9 table and the v01 change log<br>S references are within S-001–S-046 or S-101–S-105<br>OUT references are within 001–039 |
| Realises and traceability | every element and invariant has exactly one Realises field<br>39 rows, in Stage 1 order (OUT-039 after OUT-025)<br>0 differences between each row's element and invariant columns and the union of the Realises fields<br>no row text names an E-/INV- ID outside its columns<br>39 × "full" |
| Names in `omn` blocks | 307 declared names (v04: 304; new: `evaluationResult`, `pretreatmentBaseline`, `wholePeriodFrom`), none declared twice<br>199 enumeration constants and variant tags (unchanged), no duplicates and no clash with declared names<br>after removing declared names, attributes, tags, parameters, bound variables and the semantic constants of section 3.2, nothing is unresolved<br>no identifier was removed |
| Types used | every type in the changed text is declared: `Granularity`, `ScoreComponent`, `InstrumentResult`, `TypeScope`, `Period`, `View`, `ClusterAttackRate`, `AttackCount`, `IntensitySummary`, `Series`, ℕ<br>attribute selections in the changed predicates are declared on their types: `completionDate`, `treatmentStart`, `evaluated`, `typeScope`, `basis`, `rate`, `count`, `lengthDays`, `series`, `covers`, `withdrawalStart`, `reviewWindow` |
| Typing rule for levels | 166 attribute declarations with a level (as in v04); no SHOULD, MAY or MUST-with-`when` attribute lacks an `opt`/`set`/`seq` type, and none uses `set1`/`seq1`<br>the changed `WithdrawalFollowUpView.series` is `opt →Series SHOULD when …` |
| Partial terms in new or changed formulas | `last(L.evaluated)` and `first(sr.periods)` only on `seq1`<br>`n ÷ p.lengthDays`: the divisor is in ℕ₁<br>`days` inside `ofKind` is guarded by `d ≤ e` in `wholePeriodFrom` and by the existing guard in `fillsPeriod`<br>`spanOf(v.covers)` is guarded by INV-002<br>`opt` attributes (`v.series`, `r.completionDate`, `b.completionDate`, `r.baselineResult`, `L.comparison`, `r.totalScore`) are used only inside quantifiers or in `≠ ∅` |
| Conformance levels | MUST 19 (INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054–057, 059, 068, 086, 102, 108)<br>MUST NOT 2 (INV-048, 106)<br>SHOULD NOT 8 (INV-013, 021, 043, 065, 084, 091, 101, 107)<br>SHOULD 47; definitional 32; total 108<br>no invariant changed level or scope; every MUST NOT and SHOULD NOT predicate has the form `¬ F`<br>levels of the changed invariants: INV-049, INV-050, INV-062, INV-105 SHOULD; INV-063, INV-064, INV-089 definitional, each with its own element<br>the one changed attribute level (`series` core → SHOULD when) follows OUT-017 (SHOULD) |
| Quotes | 16 double-quoted strings are new in v05 outside the `omn` blocks, and all were found:<br>• 9 fragments of Stage 1 v18 (OUT-017, OUT-020, OUT-031 and OUT-035), 2 of which are also in the downloaded [S-007] text;<br>• 4 strings of the new [S-007] quote and its location (the quote, its section heading, "attacks per week on average" and "≥ 14 attacks per week on average"), verbatim in the downloaded p. 10 text;<br>• "baseline score" and "sinkt", in v04 or Stage 1 and in the downloaded [S-008] and [S-023] texts;<br>• the single word "available" in the E-046 Notes |
| Scope sweep (enter, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, entry, reminder, field, obtained, calculated, computed, algorithm, "diary information", "diary data") | 82 occurrences (v04: 76), and the 76 of v04 are unchanged. The 6 new ones are all legitimate:<br>• "computed field" in the v05 change log (two matched words), the PROCESS term for output fields;<br>• one meaning statement about "the summarised diary information" (E-064 Notes), the wording of E-013, E-032 and E-060;<br>• "The value is obtained from diary information; how is out of scope." (E-019 Notes; two matched words), the out-of-scope note of E-014;<br>• "persistent" inside the [S-007] quote.<br>Two search-log mentions of the source download format were reworded to avoid the term. No input entity, storage term or derivation from input was added. The new relations take only output elements (rates, counts, period lengths, completion dates, the shown treatment start, evaluated periods, covered periods), context properties (available results, treatment start, withdrawal start) and the cited constants. |
| Satisfiability | See Other changes 4: no conflict found, and scripted scenarios gave 0 unsatisfiable cases. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v05.md`: identical |
| Files written | only OUTPUT_MODEL.md, history/v05.md and this fix log; nothing under docs/stage1-output-requirements/ was changed; nothing committed or pushed |
