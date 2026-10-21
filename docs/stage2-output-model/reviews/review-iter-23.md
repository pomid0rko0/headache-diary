# Review — iteration 23
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v22
Date: 2026-10-21

## Summary

This is the main review of iteration 23. I am a new, independent reviewer. I checked v22 against its sources and against Stage 1 v18 myself, and I read the earlier loop files only to avoid reopening settled points.

**State of the files.**
- The working tree was clean at HEAD 2096923 ("Stage 2 / iter 22: fix (v22)"). `OUTPUT_MODEL.md` is byte-identical to `history/v22.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item of v22 carries a `Status: FROZEN` line.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026), and the source table of section 5.
- v22, all sections: notation, conformance, every element and invariant, the traceability table, section 8, sources, search log, and the change log (v14–v22 in full).
- Review 22b (R22b-01), fix 22, the oscillation check after iteration 16 with its watch points and settled points, the "Checked and not raised" lists of all 28 earlier reviews and re-checks, R04-04 with the fix-04 sweep that followed it, and every loop-file passage on E-039 `reviewWindow`, on `ongoing` and on `lastDay`.

**Result.**
- **Citations.** Every quote is verbatim at its URL, on its stated page or section. The six new sources (S-101 to S-106) have correct metadata. Every Stage 2 translation I read is faithful. I found no newer version of a source that changes an element.
- **Values.** Every value set, range, band, code label, reference level, offset and threshold matches its source.
- **Scope.** The scope sweep finds no input, storage or input-derivation content.
- **Mechanical and formal checks.** They pass. This includes the v22 `fillsPeriod`, which I checked by brute force.
- **Fidelity.** Every OUT requirement is represented at its Stage 1 strength. Section 8 is founded.
- **One remark (R23-01, a formal defect)** on the cluster phase items (E-063) and INV-089.
  - The meaning of `ongoing` is stated two ways:
    - the attribute comment says "continues at the end of the period the view covers";
    - the E-063 Meaning and the INV-089 Reading say "has no end date yet".
  - INV-089 admits different outputs under the two readings.
  - Under either reading, INV-089 tests the ICHD-3 remission duration only up to the end of the covered period. So a view of a past period cannot show an attack-free period that, by the as-of date, has exceeded three months, and is therefore a remission under the definition the model follows.
  - The fix-04 sweep for this class of defect ("a property of the next unit lost at the end of a covered period") did not consider the remission bound.

## Verification coverage

### Downloads

Everything was downloaded with `curl` through the proxy into the fresh directory `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r23/dl`, outside the repository.
- **Text extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML pages and Europe PMC XML were stripped of markup.
- **Scripts.** They are in `…/r23/scripts` and were run with `python3 -I`: `strip.py`, `match.py`, `mech.py`, `names.py`, `fills.py` and `cluster.py`, plus inline checks.
- **HTTP status.** Every request returned HTTP 200. The only exception was [S-034]: the connection was reset by the peer on the first attempt, and the file loaded on the retry.
- **PDFs** (page counts from `pdfinfo`): [S-001] 211, [S-002] 19, [S-003] 18, [S-005] 14, [S-006] 16, [S-007] 39, [S-008] 31, [S-010] 11, [S-016] 64, [S-018] 12, [S-030] 86, [S-033] 92, [S-034] 53, [S-035] 92, [S-105] 9.
- **Web pages:**
  - [S-015]: the CG150 Recommendations page and Overview page ("Last reviewed: 23 September 2026"; last update 3 June 2025, unchanged);
  - [S-028]: the NVN module;
  - [S-103]: the Cincinnati Children's PedMIDAS page;
  - [S-106]: the TA260 Overview, chapter 1 and chapter 2 (published 27 June 2012, last reviewed 11 January 2016).
- **Europe PMC full-text XML:**
  - Stage 1 sources: PMC6501455 [S-004], PMC9188162 [S-011], PMC9555163 [S-012], PMC7296705 [S-013], PMC6734476 [S-014] and PMC9607711 [S-023];
  - new sources: PMC3057423 [S-101], PMC4406925 [S-102] and PMC183845 [S-104];
  - PMC8684566 and PMC6537129, the MIDAS label variants that the search log names.
- **Rendered and read:**
  - [S-001] p. 190: the A1.1.1 and A1.1.2 windows, whose "±" and "−" have no text mapping;
  - the [S-034] title page, an image that reads "Возрастная группа" … "дети".
- **Metadata.** PubMed esummary confirms the authors, journal, year, volume, pages, DOI and PMCID of S-101, S-102 and S-104, and of the S-103 developer paper (PMID 11739822).
- **Newer versions.** A web search finds no published ICHD-4, only "Work in Progress" papers. NICE CG150 and TA260 are current.

### Quote check (`match.py`)

**Method.**
1. For every line outside the `omn` blocks that carries an `[S-NNN]` tag, the script takes each double-quoted string. It attributes the string to the nearest preceding tag and splits it at "[...]".
2. It searches each fragment of at least 6 letters or digits after normalisation (NFKC, soft hyphens removed, line-end hyphens joined, case folded, letters and digits only). It searches, in this order:
   - the tagged source, page by page;
   - the other sources tagged on the line;
   - Stage 1 v18;
   - all downloaded texts.
3. For page-based sources, a second pass compares the page on which each fragment was found with the "p." or "PDF p." of the parenthesis after it:
   - 83 fragments match their stated page;
   - the 4 mismatches are search-log lines on which the parenthesis belongs to a neighbouring item; I read each, and each quote is on the page its own parenthesis states;
   - the fragments without a parsable page in that parenthesis (code lists, section titles, sentences located in a later parenthesis) were read by hand against the pages found. All are on the stated pages, for example [S-001] pp. 8, 9, 12, 105, 122–125, 139, 190, 209 and 42, [S-008] pp. 9, 12, 13, [S-010] p. 6, [S-033] pp. 1, 39, 40, 41, 53, [S-034] pp. 17, 52, [S-035] PDF pp. 23, 48, 57, 83, 86, [S-007] pp. 10, 22, 25 and [S-105] P. 6/9 and P. 8/9.

**Results.** 530 fragments. Notes on the columns:
- "Verbatim elsewhere" means found in another source tagged on the same line, or as Stage 1 wording.
- "Not source text" means a translation (22) or a search-log query or row label (14).
- "Confirmed otherwise" means confirmed on a rendered page or in an additional download:
  - S-001: the two A1.1 windows, read on the rendered p. 190;
  - S-034: "Возрастная группа", twice, read on the rendered title page;
  - S-102: "little or none", found in PMC8684566;
  - S-106: "less than a 30% reduction in headache days per month after 2 treatment cycles", found in TA260 chapter 1.

| Source (nearest tag) | Fragments | Verbatim in tagged source | Verbatim elsewhere | Not source text | Confirmed otherwise | Not found | Unreachable |
|---|---|---|---|---|---|---|---|
| S-001 ICHD-3 | 88 | 78 | 7 | 1 | 2 | 0 | 0 |
| S-002 | 11 | 7 | 4 | 0 | 0 | 0 | 0 |
| S-005 | 9 | 2 | 7 | 0 | 0 | 0 | 0 |
| S-007 | 10 | 8 | 2 | 0 | 0 | 0 | 0 |
| S-008 | 29 | 21 | 8 | 0 | 0 | 0 | 0 |
| S-010 | 48 | 39 | 9 | 0 | 0 | 0 | 0 |
| S-011 | 9 | 7 | 2 | 0 | 0 | 0 | 0 |
| S-012 / S-013 | 5 | 3 | 2 | 0 | 0 | 0 | 0 |
| S-014 | 45 | 34 | 11 | 0 | 0 | 0 | 0 |
| S-015 | 56 | 39 | 17 | 0 | 0 | 0 | 0 |
| S-016 | 9 | 7 | 2 | 0 | 0 | 0 | 0 |
| S-018 | 14 | 10 | 4 | 0 | 0 | 0 | 0 |
| S-023 | 6 | 5 | 1 | 0 | 0 | 0 | 0 |
| S-028 | 13 | 10 | 2 | 1 | 0 | 0 | 0 |
| S-029, S-032, S-042 | 5 | 0 | 5 | 0 | 0 | 0 | 0 |
| S-030 | 4 | 3 | 1 | 0 | 0 | 0 | 0 |
| S-033 | 49 | 21 | 24 | 4 | 0 | 0 | 0 |
| S-034 | 20 | 8 | 6 | 4 | 2 | 0 | 0 |
| S-035 | 50 | 33 | 4 | 13 | 0 | 0 | 0 |
| S-101 | 7 | 4 | 0 | 3 | 0 | 0 | 0 |
| S-102 | 15 | 7 | 3 | 4 | 1 | 0 | 0 |
| S-103 | 12 | 10 | 0 | 2 | 0 | 0 | 0 |
| S-104 | 8 | 3 | 1 | 4 | 0 | 0 | 0 |
| S-105 | 3 | 3 | 0 | 0 | 0 | 0 | 0 |
| S-106 | 5 | 3 | 1 | 0 | 1 | 0 | 0 |
| **Total** | **530** | **365** | **123** | **36** | **6** | **0** | **0** |

**New sources and their quotes, read in context:**
- **[S-101] PMC3057423, Methods, "Data sources", HIT-6 paragraph.** The 36–78 range and the four categories with their bands are verbatim.
- **[S-102] PMC4406925, Methods, "Headache impact on functioning", subsection "Migraine-related disability".** The four grades with their bands, the IVA/IVB option and "The recall period for the MIDAS is three months" are verbatim.
- **[S-103] Cincinnati Children's page, section "PedMIDAS Grading Scale".** The table rows 0 to 10 / 11 to 30 / 31 to 50 / Greater than 50 are verbatim, with the labels Little to none / Mild / Moderate / Severe.
- **[S-104] PMC183845, section "Construction of the Hospital Anxiety And Depression Scale (HADS)".** "0 to 21 for anxiety and 0 to 21 for depression" is verbatim.
- **[S-105].** The PHQ-9 range 0–27 and the GAD-7 range 0–21 are on P. 6/9. The developers sentence is on P. 8/9. The PDF metadata show author Kurt Kroenke, created 2010, modified 2014.
- **[S-106] TA260, chapter 2.** "The recommended re-treatment schedule is every 12 weeks (see the summary of product characteristics)." is verbatim.

**Translations read.**
- Russian: [S-033] pp. 1, 39, 40, 41; [S-034] pp. 17, 52 and the title page.
- Turkish: [S-035] PDF pp. 23, 48, 57, 77, 82, 83, 86.
- Dutch: the [S-028] PICO.
- All are faithful.

### Fidelity to Stage 1, requirement by requirement

For each OUT requirement I compared every observable property of the Statement and every constraining Caveat with the elements and invariants that realise it, and the level of each part with its Stage 1 strength.

| OUT | Parts and strength | Realisation checked | Result |
|---|---|---|---|
| 001 | MUST: period with start, end and length; monthly or 28-day; equal-length comparison. Caveat: days per month visible. | E-003, E-005, INV-002, INV-003, INV-014, INV-015, INV-108, INV-037, INV-038 | ok |
| 002 | SHOULD: definition label | E-011 `reports`, INV-008 | ok |
| 003 | SHOULD: indicator next to the measures. SHOULD NOT: cut-off presented as validated | E-013, INV-011, INV-012, INV-013 | ok |
| 004 | MUST: per period of the time range; ICHD-3 definition | INV-014, INV-009 | ok |
| 005 | MUST: for migraine. SHOULD: label | INV-015, INV-008 | ok |
| 006 / 007 | SHOULD; MUST monthly where provided (OUT-001) | INV-016, INV-017, INV-108, INV-010 | ok |
| 008 | MAY | E-020 to E-022 | ok |
| 009 | SHOULD: series, markers, weekly where relevant | INV-034 to INV-036 | ok |
| 010 | SHOULD: per period, stated scale, comparison | INV-018, INV-039, INV-032 | ok |
| 011 | SHOULD: summary and label. Caveat as SHOULD NOT | INV-019 to INV-021 | ok |
| 012 | SHOULD: across periods and per treated attack | INV-022, INV-072, INV-076 | ok |
| 013 | MAY | E-027 | ok |
| 014 | MUST: total, class and drug per period | INV-023, INV-024 | ok |
| 015 | SHOULD: per calendar week | INV-025 | ok |
| 016 | MUST: per period, per class and combined. MUST: prompt. MUST NOT: diagnosis | E-032, INV-044 to INV-048 | ok |
| 017 | SHOULD: from start of withdrawal, 4–8-week window, following year, worsening label | E-039, INV-049 to INV-052 | ok |
| 018 | MUST: comparison, values, absolute and percentage change, time points. Caveat: no decision | E-040 to E-043, INV-053 to INV-059, INV-106 | ok |
| 019 | SHOULD: residual burden next to a percentage change | INV-060, INV-061 | ok |
| 020 | SHOULD: criterion, values and other values. SHOULD NOT: sole indicator | E-045, E-046, INV-062 to INV-065 | ok |
| 021 | MUST: three components for the same periods. SHOULD: the others where provided | INV-068, INV-069, INV-102 | ok |
| 022 | SHOULD: after stop, pause or reduction, against on-treatment period and baseline | INV-070, INV-103 | ok |
| 023 | SHOULD: all outcomes, consistency, timing, formulation, phases, 15 min. Caveat as SHOULD NOT | E-050 to E-053, INV-071 to INV-075, INV-107 | ok |
| 024 | SHOULD: chronological, grouped by class, all details, acute formulation | E-054, E-055, INV-077 to INV-079, INV-109 | ok |
| 025 | MAY | E-056, INV-080 | ok |
| 039 | SHOULD: next to comparison, in history and in clinician summary | E-047, INV-066, INV-067, INV-104, INV-109 | ok |
| 026 | SHOULD: name, date, recall, total score, grading, change from baseline | E-057, E-058, INV-081, INV-082 | ok |
| 027 | SHOULD: three domains, severe impairment, comparison with baseline | INV-026, INV-027, INV-033 | ok |
| 028 | MUST: three-month view. SHOULD: definitions. SHOULD NOT: diagnosis | INV-040 to INV-043 | ok |
| 029 | MUST: frequency and medication per type and combined. SHOULD: intensity per type | INV-028 to INV-030 | ok |
| 030 | MUST: cycles, A1.1 window, number of complete cycles | E-060, E-061, INV-086, INV-087 | ok |
| 031 | SHOULD: bouts and remissions "using the ICHD-3 definitions", rates, 15 min, previous bouts | E-062 to E-064, INV-088, INV-089 | **R23-01** |
| 032 | MAY; caveats SHOULD | E-065, INV-090, INV-110 | ok |
| 033 | SHOULD: name, date and score next to headache outputs; not diagnoses | E-059, INV-083 to INV-085 | ok |
| 034 / 035 | SHOULD | E-066, E-067, INV-094, INV-095, INV-104, INV-105 | ok |
| 036 | SHOULD: (a) to (d) and the supportive-information caveat | INV-055, INV-096 to INV-098 | ok |
| 037 | SHOULD NOT and SHOULD as stated | INV-091 to INV-093 | ok |
| 038 | SHOULD; SHOULD NOT as the negative form | INV-099 to INV-101 | ok |

### Mechanical checks (scripts)

| Check | Result |
|---|---|
| IDs (`mech.py`) | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110): none missing, none duplicated. Issues ISS-01 to ISS-12 without ISS-07, which is withdrawn in section 9. New sources S-101 to S-106. No dangling E-, INV-, ISS- or S- reference. 46 Stage 1 sources. |
| Traceability (`mech.py`) | 39 rows in Stage 1 order (OUT-039 after OUT-025). For every row, the Elements and Invariants columns equal exactly the sets of items whose Realises field names the requirement: 0 mismatches. Every row reads "full". Every element and invariant has a Realises field, and each OUT ID it names exists. |
| Names (`names.py`) | 712 declared names and 133 bound-variable forms. The only tokens not matched are the constants of the three multi-line enumerations and variants (`AnnotationKind`, `IntensitySummaryValue`, `AcuteOutcomeMeasure`), which I checked by hand as declared, and `refs` (section 2.5). No duplicate declaration. |
| Attribute levels | 172 level-annotated attributes: core 94, MUST 29, SHOULD 47, MAY 2, as the change log states. The section 2.5 typing rule holds for every attribute. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33, as stated. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. |
| Partial terms | Every `÷`, `s(i)`, `first`, `last`, `max`, `min`, `days` and `classOf` term was read by hand and is guarded. |
| `fillsPeriod` (`fills.py`) | v22 predicate as written, with INV-002 and INV-004. Setup: 1,500 random covered periods of 1 to 200 days, each with calendar months, 28-day periods and calendar weeks (4,500 cases), and every candidate series of 1 to 8 periods. In every case the only satisfying series is exactly "all whole periods of the granularity within p, 28-day periods counted from p's first day", or none where no whole period fits. 0 violations. So the E-006, INV-050, INV-104 and INV-105 prose claims hold: "consists of all whole periods", "spans it exactly" for a run of whole periods, and "cannot shrink to a single period". |
| Date examples | Every one is correct: E-042 and INV-055 (1 April, 26 March, 26 February – 25 March, 4–31 December, the 28 February / 25 March / 31 March interval ends); INV-049 (6 April, day 43, review window 7 April – 5 May); E-007 (67 days); INV-105 (43 days); the v22 change-log example (5 January – 29 March: 84 days; 19 January – 15 March: 56 days). |
| INV-045 span | For random starts, the shortest span "of more than three months" always has 4 periods, for calendar months and for 28-day periods, as the Notes state. |
| Cluster bound (`cluster.py`) | INV-089 as written, on the R23-01 scenarios. See the remark. |
| Scope sweep | grep for record, enter, input, capture, store, database, serialisation, JSON, XML, CSV, FHIR, encoding, retention, persist, reminder, data field and data-entry. The only hits are section 1, the section 2.1 notation disclaimer, one [S-014] instrument quote on recall (settled since review 01) and INV-076's statement that it avoids a derivation. Every derived attribute's relation has output elements, context properties or cited constants as its arguments. Where the value comes from diary information, only its type and unit are given. Every shown threshold and formula of the output data is present and cited: ICHD-3 8.2 levels and span; A1.1 window; remission duration; review window; time points; responder thresholds and control levels; instrument bands and ranges; the completeness proportion; the percentage change; the rate. |

## Remarks

### R23-01 Formal defect: `ongoing` has two meanings, and the remission bound of INV-089 excludes attack-free periods of more than three months that continue past the covered period
- Item(s): E-063 (`ongoing`, `lastDay`, Meaning, Notes), INV-089 (Predicate, Reading), E-062 Notes, section 7 row OUT-031
- Problem:
  - **Two meanings of `ongoing`.** In a view whose covered period ends before the as-of date, the two meanings give different outputs.
    - **The attribute comment** reads `ongoing : 𝔹 core -- the period continues at the end of the period the view covers`, and `lastDay` takes the covered period's end for an ongoing item.
    - **The other texts:**
      - the E-063 Meaning ("An ongoing period has no end date yet");
      - the INV-089 Reading (the same words);
      - the E-063 Notes ("`ongoing` is needed so that the end-date obligation can be met for a current bout").

      They describe a period that has not ended.
    - **Example.** Take a bout from 10 July to 20 August 2026, shown in a cluster view of 1 January – 31 July 2026, with the as-of date 21 October 2026.
      - Under the comment the bout is `ongoing`. INV-089 (`x.ongoing ⇒ x.end = ∅`) forbids its end date, and its duration is 22 days (10–31 July).
      - Under the Meaning it is not ongoing. It shows its end date, 20 August, and its duration of 42 days.
    - **A start before the covered period.** For a bout from 10 December 2025 to 10 February 2026 in a view of January 2026, the comment reading gives a duration of 53 days (10 December – 31 January). That is neither the bout's duration (63 days) nor its days within the view (31).
    - **Conclusion.** INV-089 is definitional, so the set of valid outputs depends on which reading is taken: ambiguous semantics.
  - **The remission bound truncates the attack-free period.** INV-089 requires `plusMonths(s, remissionMoreThanMonths) ≤ e` for `e ∈ lastDay(x)`. For an item that continues at the end of the covered period, `lastDay` is that end under both readings. So the bound is tested on the attack-free period's length up to the end of the covered period, not on its length.
  - **Example (`cluster.py`).**
    - As-of date 21 October 2026. A bout from 1 March to 31 May 2026, then no attacks from 1 June to the as-of date, 143 days.
    - INV-088 requires the cluster view of the selected time range, here 1 January – 31 July 2026. INV-001 admits that range, which ends before the as-of date.
    - In that view, the attack-free period from 1 June is ongoing, `lastDay` is 31 July, and `plusMonths(1 June, 3)` is 1 September, which is not on or before 31 July. INV-089 fails, so the view cannot show this remission.
    - A view ending on the as-of date shows the same period as a remission (`lastDay` 21 October, bound holds).
    - Under the comment reading, the same holds for an attack-free period that ended after the covered period, for example on 15 October (137 days).
  - **Why this matters.** E-063 and E-062 state the intent: a remission period shown is "an attack-free period of more than three months, the duration that the ICHD-3 Definitions of terms require of a remission". The 1 June period is such a period as of the as-of date. The predicate is stronger than this intent and excludes a correct output: a cluster view of a past period that shows a remission which began within it.
  - **The rest of the model uses what is known on the as-of date beyond the covered period:**
    - A cycle line that has ended is shown complete to the day before the next first day of menstruation "whether or not the next cycle is shown in the view (for example when it begins after the covered period)" (E-060 Notes; INV-087 lets the last line end after the covered period).
    - Whether a treatment has stopped "is judged as of that date", and the duration of a treatment that has not stopped runs to the as-of date (E-055 Notes, INV-079).
    - A bout that began before the covered period is shown with its real start.

    Only the end of a cluster phase is cut at the covered period.
  - **Not considered before.** No earlier review raised the meaning of `ongoing` or the remission bound for a view of a past period. The fix-04 sweep for R04-04-kind defects ("a property of the next unit lost at the end of a covered period") cited "The ongoing cluster period has `ongoing` and `lastDay` (E-063)" as the reason why there was none. It did not consider that the remission's defining property, its length of more than three months, is exactly such a property lost at the end of a covered period.
  - **No settled point or watch point is reversed:**
    - the "> 3 months" reading of INV-089 is unchanged;
    - ISS-12 and the Definitions-of-terms bound are unchanged;
    - the period of a cluster attack rate within its bout (review 15, settled) is unchanged.
- Evidence:
  - E-063: `ongoing : 𝔹 core -- the period continues at the end of the period the view covers`; `fun lastDay(x : ClusterPhaseItem) : set Date ≙ {d : Date | (x.ongoing ∧ d = viewOf(x).covers.end) ∨ (¬ x.ongoing ∧ d ∈ x.end)}`; Meaning: "An ongoing period has no end date yet."; Notes: "`ongoing` is needed so that the end-date obligation can be met for a current bout."
  - INV-089: `(∀ x : ClusterPhaseItem • (x.ongoing ⇒ x.end = ∅) ∧ (∀ s ∈ x.start; e ∈ lastDay(x) • s ≤ e ∧ ∀ d ∈ x.duration • d = daysLong(days(s, e))) ∧ (x ∈ RemissionPeriodItem ⇒ ∀ s ∈ x.start; e ∈ lastDay(x) • plusMonths(s, remissionMoreThanMonths) ≤ e))`. The Reading says: "An ongoing period has no end date yet; a duration is the number of days from start to end (or to the end of the covered period while ongoing); a remission period lasts more than three months".
  - [S-001] "To be considered a remission, the attack-free period must exceed three months." (Definitions of terms, Cluster remission period, p. 209; quoted in E-063, verified on the page). The criterion is the length of the attack-free period, not its length within a reporting period.
  - Stage 1 OUT-031 Statement: "cluster periods (bouts) and cluster remission periods with their start dates, end dates and durations, using the ICHD-3 definitions [S-001]".
  - E-008 Meaning: "An output may concern periods long before the as-of date". INV-001 admits a selected time range ending before the as-of date, and INV-088 requires the cluster view of that time range.
  - fixes/fix-iter-04.md, "Sweep for R04-04-kind defects elsewhere (a property of the next unit lost at the end of a covered period). None was found. — The ongoing cluster period has `ongoing` and `lastDay` (E-063)."
- Required change:
  - **What must change.** Fix one meaning of `ongoing` and state it the same way in the attribute comment, the E-063 Meaning and Notes and the INV-089 Reading. Make the remission bound test the attack-free period's own length: to its end, or to the as-of date while it continues. Then a remission period that the ICHD-3 Definitions of terms recognise as of the as-of date can be shown in a view of any covered period that it overlaps. Update the E-062 Notes and row OUT-031 accordingly. Options:
    - **(a)** Read `ongoing` as "the period has not ended by the as-of date", as `stopped` is read for treatment lines (INV-079) and `complete` for cycle lines (INV-087). Let `lastDay` of an ongoing item be the as-of date: `{d : Date | (x.ongoing ∧ d = ctx(outputOf(x)).asOf) ∨ (¬ x.ongoing ∧ d ∈ x.end)}`. Then:
      - a period that ended after the covered period shows its end date and its full duration;
      - the duration of a period that has not ended is its duration to date;
      - the remission bound is tested on the remission's length.

      INV-088 (overlap with the covered period) and the INV-089 rate conjunct (rate period within its bout) keep their form.
    - **(b)** Keep `ongoing` relative to the covered period, but then:
      - reword the Meaning, Notes and Reading to that meaning ("continues at the end of the covered period", not "has no end date yet");
      - test the remission conjunct against the attack-free period's end where it has ended after the covered period, or against the as-of date while it continues. This needs that date as an output element of the item, for example a derived end-or-as-of date shown with it.

## Checked and not raised

- **The v22 change (R22b-01).**
  - The new `fillsPeriod` conjunct, and every v22 text, agree with the predicate. `fills.py` found 0 violations in 4,500 cases.
  - INV-050's start tie already implied the conjunct.
  - INV-094's selected time range, read through INV-104, gets the INV-001 periods.
  - No oscillation trigger is touched: no exact end tie was re-added, and neither `fillsPeriod` nor the start tie was loosened (iteration-08 watch point 4).
- **Two class indicators of one period and class with different statuses (INV-046).** The two directions of INV-046 conflict only if one view shows two indicators of the same class and period with different statuses. That output shows contradictory values, which no Stage 1 requirement permits. Not a defect.
- **The INV-046 Notes argument.** "The two directions agree" holds: the classes that show days in the first period of the span are not excluded.
- **E-039 `reviewWindow` SHOULD without `when` against INV-050.** Settled by reviews 06, 12 and 19c. No new evidence.
- **The CycleLine lead-in when the output shows an earlier day 1 in another view.** This is part of the menstrual-relation watch point (iteration 12, points 3–6, repeated after iteration 16). I have no evidence that the earlier decisions did not consider. Not raised.
- **The Turkish Box 8 and Danish criteria outside `namedCriteria`.** Settled (reviews 08, 08b and 17).
- **Value sets.** The HIT-6, MIDAS, PedMIDAS and HALT-90 bands, the HADS, PHQ-9 and GAD-7 ranges, the recall periods, the ICHD-3 8.2 levels, the A1.1 window arithmetic (day −2 to +3 as `plusDays(d1, −2)` to `plusDays(d1, 2)`, and `nextWindowDays`), the remission duration and every responder threshold (NICE 1.3.28 and 1.3.29, IHS Q6 including the MIDAS ranges, DMKG, Russian 7.1, IHS 2025 levels) all match their sources.
- **The 18 evaluation rules.** Every offset, anchor, timing, age coverage and `excludes` value matches its quote (watch point 5; nothing changed).
- **Section 8.** Each of ISS-01 to ISS-06 and ISS-08 to ISS-12 is founded. Their quotes are verbatim on the stated pages:
  - [S-001] pp. 12, 42, 105, 122–125, 139, 190, 209;
  - [S-015] 1.3.9, 1.3.39, 1.3.48 and the Overview;
  - [S-034] p. 52;
  - [S-010] p. 6;
  - [S-014] the HURT paragraph.

  No Stage 1 issue is worked around silently. R23-01 is a model defect, not a Stage 1 issue.
- **Settled points, not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the "> 3 months" readings (INV-045, INV-089);
  - the HIT-6 one-month recall, HADS subscales only, and the MIDAS labels of [S-102] with Grade IV undivided;
  - "baseline administration" as any earlier administration;
  - INV-023 at any granularity, and INV-027 tied to preventive treatments;
  - INV-060 with INV-061 for compared periods shorter than 28 days;
  - `mostRecent` with 28-day periods;
  - empty `remissions` in chronic cluster headache (ISS-12);
  - the 24-hour outcomes in 15-minute summaries;
  - the history-wide `acuteMedications` (watch point 2);
  - "one item suffices" and the ties of INV-105 (watch point 1);
  - INV-098 read on period starts (watch point 6).
- **Oscillation watch points.** R23-01 concerns E-063 and INV-089, which no watch point names. Neither option changes the remission threshold, ISS-12, the settled rate-within-bout reading or any watch-point item.

## Notes on frozen items (for the human)

None. No item is frozen.
