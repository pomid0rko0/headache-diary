# Review — iteration 25 (re-check b)
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v24
Date: 2026-10-22

## Summary

This is the first independent re-check of iteration 25. The main review (review-iter-25.md) found no remarks on v24. I checked v24 myself against its sources and against Stage 1 v18, and I read the earlier loop files only to avoid reopening settled points or reversing earlier fixes.

**State of the files.**
- `OUTPUT_MODEL.md` is byte-identical to `history/v24.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18: sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source table of section 5.
- v24, every section: notation, conformance, all 67 elements and 111 invariants, traceability, section 8, sources, search log and the change log from v20 on.
- Review 25, the oscillation check after iteration 24 (settled points and watch points), and the earlier review and fix passages on each point I considered raising (reviews 01, 02, 05, 15, 18, 19, 22b; fixes 01, 02, 18).

**Result.**
- **Citations.** I re-downloaded every source with a quote in the model and found every quoted fragment verbatim on its stated page or section. Metadata, translations and versions are correct.
- **Values.** All value sets, ranges, bands, code labels, reference levels, offsets, thresholds and control levels match their sources.
- **Scope.** The model contains no input, storage or input-derivation content. Every threshold, formula and computed field that is part of the output data is present and cited.
- **Fidelity.** All 39 Stage 1 requirements are represented at their Stage 1 strengths.
- **Mechanical checks.** All pass.

**One formal defect (R25b-01).**
- INV-001 lets a treatment course have several stop events.
- Since v17 (the day convention) and v18 (the stop bounds), part of the model treats the earliest stop as the end of the course: E-042, INV-055, INV-068, E-046 and E-067.
- Another part treats any stop as the course's stop: INV-079, INV-109, and INV-070 with INV-103.
- For one admissible course, the model therefore admits two treatment durations, and it admits a "post-stop" view whose "on-treatment period" lies wholly after the course has ended.
- Review 15 set this case aside before v17 because the ordering requirements hold. That argument does not cover the disagreement, which v17 and v18 introduced.

## Verification coverage

### Downloads and tools

**Where.** Each source was downloaded fresh with `curl` through the proxy into `/tmp/r25b_src`, outside the repository. Scripts are in `/tmp/r25b_scripts` and were run with `python3 -I`: `build.py`, `quotes.py`, `pages.py`, `mech.py`, `names.py`, `dates.py` and `stops.py`.

**Extraction.**
- PDFs: page by page with `pdftotext -raw` and `-layout`.
- HTML pages and Europe PMC full-text XML: markup stripped.

**Rendered and read** (pages without a usable text layer):
- [S-001] p. 190: A1.1.1 and A1.1.2 criterion B, "day 1 ± 2 (i.e. days −2 to +3)", and note 2. The text layer maps "+" to "þ" and drops "±" and "−".
- [S-034] p. 1, an image: "Возрастная группа" … "дети".

**Sources downloaded:**
- PDFs: [S-001] (211 pp.), [S-002], [S-003], [S-005], [S-006], [S-007] (39 pp.), [S-008] (31 pp.), [S-009], [S-010] (11 pp.), [S-016] (64 pp.), [S-018] (12 pp.; the URL serves a PDF), [S-020], [S-021], [S-022], [S-030], [S-033] (92 pp.), [S-034] (53 pp.), [S-035] (92 pp.), [S-046] and [S-105] (9 pp.).
- Europe PMC full texts:
  - [S-004], [S-011], [S-012], [S-013], [S-014], [S-023], [S-042], [S-043], [S-101], [S-102] and [S-104];
  - also PMC8684566 and PMC6537129, for the MIDAS label variants that the search log names, and PMC5796955.
- Web pages:
  - [S-015]: the Recommendations and Overview pages;
  - [S-028] and [S-029];
  - [S-103];
  - [S-106]: the overview, chapter 1 and chapter 2.

**Not retrieved (no model quote depends on them):**
- [S-024] and [S-025]: sfemc.fr returned a "Maintenance en cours" HTML page instead of the PDF. The model has no Stage 2 quote from either source.
- [S-032]: brainmed.com reset the connection, and a retry returned HTTP 301. The model reuses only the Stage 1 quote of [S-032], which I checked against the Stage 1 text.

**Metadata.**
- PubMed esummary confirms the citation of each source:
  - S-101: PMID 20819842; Cephalalgia 2011;31(3):357–67; DOI 10.1177/0333102410379890; PMC3057423.
  - S-102: PMID 25902814; J Headache Pain 2015;16:24; PMC4406925.
  - S-104: PMID 12914662; Health Qual Life Outcomes 2003;1:29; PMC183845.
  - The S-103 developer paper: PMID 11739822; Neurology 2001;57(11):2034–9.
- [S-105] PDF metadata: author Kurt Kroenke, created 22 June 2010, modified 16 April 2014. The developers' sentence is on P. 8/9.
- [S-106] overview: "Published: 27 June 2012" and "Last reviewed: 11 January 2016".
- [S-015]: "Last updated: 03 June 2025".

### Quote check (`quotes.py`, `pages.py`)

**Method.**
1. For every line outside the `omn` blocks, take each double-quoted string and attribute it to the nearest preceding `[S-NNN]` tag on the line.
2. Split the string at "[...]" and keep fragments of at least 6 letters or digits.
3. Normalise each fragment: NFKC, soft hyphens removed, case folded, letters and digits only.
4. Search the tagged source page by page, then every other downloaded text, then Stage 1 v18.
5. Compare the page found with the "p." or "PDF p." stated after the quote. Page offsets: S-016 printed page + 6; S-005 and S-002 journal pages.

**Results.**
- Every new Stage 2 quote is on its stated page or section. The location checks included:
  - [S-001]: pp. 8, 9, 12, 122–125, 139, 190 and 209;
  - [S-007]: p. 10; [S-008]: pp. 9, 12, 13 and 17; [S-010]: p. 6; [S-016]: printed p. 1; [S-018]: pp. 1, 7 and 8;
  - [S-033]: pp. 1, 39, 40 and 41; [S-034]: pp. 17 and 52;
  - [S-035]: PDF pp. 23, 48, 57, 77, 82, 83 and 86;
  - [S-101]: "Methods > Data sources"; [S-102]: "Headache impact on functioning > Migraine-related disability";
  - [S-104]: "Construction of the Hospital Anxiety And Depression Scale (HADS)"; [S-105]: P. 6/9; [S-106]: 2.1, last sentence;
  - [S-011]: Background, paragraphs 1 and 2.
- Translations read in context and judged faithful: Russian ([S-033], [S-034]), Turkish ([S-035]) and Dutch ([S-028]).

**Columns of the table.**
- "Verbatim elsewhere": the fragment is in another source tagged on the same line, or is Stage 1 wording. Lines often cite a source after its quote.
- "Not source text": English translations, model terms, search-log queries and labels. Each was read in place.

| Source (nearest tag) | Fragments | Verbatim in tagged source | Verbatim elsewhere | Confirmed on rendered page | Not source text | Not found | Unreachable |
|---|---|---|---|---|---|---|---|
| S-001 | 75 | 70 | 3 | 1 | 1 | 0 | 0 |
| S-002 | 6 | 2 | 4 | 0 | 0 | 0 | 0 |
| S-005 | 9 | 2 | 7 | 0 | 0 | 0 | 0 |
| S-007 | 9 | 8 | 1 | 0 | 0 | 0 | 0 |
| S-008 | 27 | 19 | 8 | 0 | 0 | 0 | 0 |
| S-010 | 38 | 33 | 5 | 0 | 0 | 0 | 0 |
| S-011 | 9 | 7 | 2 | 0 | 0 | 0 | 0 |
| S-012 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| S-013 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| S-014 | 37 | 31 | 6 | 0 | 0 | 0 | 0 |
| S-015 | 42 | 35 | 7 | 0 | 0 | 0 | 0 |
| S-016 | 9 | 7 | 2 | 0 | 0 | 0 | 0 |
| S-018 | 13 | 10 | 3 | 0 | 0 | 0 | 0 |
| S-023 | 6 | 5 | 1 | 0 | 0 | 0 | 0 |
| S-028 | 13 | 10 | 2 | 0 | 1 | 0 | 0 |
| S-029 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| S-030 | 4 | 3 | 1 | 0 | 0 | 0 | 0 |
| S-032 | 1 | 0 | 1 (Stage 1) | 0 | 0 | 0 | 0 (source unreachable; Stage 1 quote only) |
| S-033 | 47 | 21 | 22 | 0 | 4 | 0 | 0 |
| S-034 | 17 | 8 | 3 | 2 | 4 | 0 | 0 |
| S-035 | 50 | 33 | 4 | 0 | 13 | 0 | 0 |
| S-042 | 3 | 1 | 2 | 0 | 0 | 0 | 0 |
| S-101 | 4 | 4 | 0 | 0 | 0 | 0 | 0 |
| S-102 | 9 | 6 | 3 | 0 | 0 | 0 | 0 |
| S-103 | 10 | 10 | 0 | 0 | 0 | 0 | 0 |
| S-104 | 3 | 3 | 0 | 0 | 0 | 0 | 0 |
| S-105 | 3 | 3 | 0 | 0 | 0 | 0 | 0 |
| S-106 | 5 | 4 | 1 | 0 | 0 | 0 | 0 |
| No tag on the line (Stage 1 wording, model terms, search queries) | 421 | 0 | 371 | 0 | 50 | 0 | 0 |
| **Total** | **873** | **338** | **459** | **3** | **73** | **0** | **0** |

### Values checked against the sources

- **ICHD-3 code labels** of E-009, character for character: classification list, pp. 8, 9 and 12.
- **Reference levels of 8.2 and its subtypes**, read in the text of pp. 122–125: ergotamine, triptans, opioids, combination analgesics, 8.2.6 and 8.2.8 at 10 days per month; non-opioid analgesics at 15; "for more than three months" / ">3 months".
- **Classes.** `classesOf826` is 8.2.6 criterion B; 8.2.6 note 2 refers to 8.2.1–8.2.5.
- **Perimenstrual window.** A1.1 window and note 2, read on the rendered p. 190.
- **Remission.** "must exceed three months" (p. 209).
- **Instruments.**
  - HIT-6: range 36–78 and four bands ([S-101]).
  - MIDAS: four grades with labels and bands, and 3-month recall ([S-102]).
  - PedMIDAS: table rows ([S-103]).
  - HALT-90: Table 18, including the overlap at 20; HALT-90 and HALT-30 recall and unit ([S-014]).
  - HADS 0–21 per subscale ([S-104]); PHQ-9 0–27 and GAD-7 0–21 ([S-105]).
- **Evaluation rules.** For all 18 rules of E-041, the offset, anchor, timing, ages and `excludes` were read against their quotes.
- **Named criteria.** The thresholds and conditions of the six criteria of E-045, including the IHS Q6 MIDAS baseline ranges and the DMKG/ÖKSG/SKG items.
- **Control levels.** The four levels of [S-010].
- **Worked examples** (`dates.py`), all correct:
  - E-042 and INV-055: 1 April; 26 March; 26 February – 25 March; intervals ending 28 February, 25 March and 31 March; 4–31 December = 28 days.
  - INV-049: day 43; window 7 April – 5 May; 6 April.
  - E-007: 67 days. E-063: 42 and 143 days. INV-105: 43 days.
  - INV-045: every calendar month 2020–2030 gives a span of four periods.

### Fidelity to Stage 1, requirement by requirement

| OUT | Parts and Stage 1 strength | Realised by | Result |
|---|---|---|---|
| 001 | MUST: period with start, end and length; monthly or 28-day; equal-length comparison. Caveat: days per month visible | E-003, E-005, INV-002, INV-003, INV-014, INV-015, INV-108, INV-037, INV-038 | ok |
| 002 | SHOULD: state the definition of each measure followed | E-011, INV-008, INV-111 | ok |
| 003 | SHOULD: indicator next to the measures. SHOULD NOT: cut-off presented as validated | E-013, INV-011 to INV-013 | ok |
| 004 | MUST: every period of the time range; ICHD-3 definition | INV-014, INV-009, INV-006 | ok |
| 005 | MUST for patients with migraine; SHOULD: label | INV-015, INV-008 | ok |
| 006 | SHOULD; MUST per month or 28 days where provided (OUT-001) | INV-016, INV-108, INV-008 | ok |
| 007 | SHOULD; separate from day counts; ICHD-3 definition | E-019, INV-017, INV-108, INV-010 | ok |
| 008 | MAY | E-020 to E-022, INV-031 | ok |
| 009 | SHOULD: series, markers for start, dose change and stop; weekly where relevant | E-034, E-035, INV-034 to INV-036, INV-001 | ok |
| 010 | SHOULD: per period, stated scale, comparison | INV-018, INV-032, INV-039 | ok |
| 011 | SHOULD: summary and label. Caveat as SHOULD NOT | INV-019 to INV-021 | ok |
| 012 | SHOULD: across periods and per treated attack, for migraine | INV-022, INV-072, INV-076 | ok |
| 013 | MAY, separately from headache measures | E-027 | ok |
| 014 | MUST: total, per class and per drug, per period, together | INV-023, INV-024 | ok |
| 015 | SHOULD: per calendar week | E-036, INV-025 | ok |
| 016 | MUST: per period, per class and combined (8.2.6), with levels and span; MUST: prompt. MUST NOT: diagnosis | E-032, INV-044 to INV-048 | ok (values verified; ISS-01) |
| 017 | SHOULD: from the start of withdrawal; 4–8-week window; following year; worsening label | E-039, INV-049 to INV-052 | ok |
| 018 | MUST: comparison, values, absolute and percentage change, time points. Caveat: no decision (MUST NOT) | E-040 to E-043, INV-053 to INV-059, INV-106 | ok (these predicates already read the end of a course as its earliest stop; see R25b-01) |
| 019 | SHOULD: residual burden next to a percentage change | E-044, INV-060, INV-061 | ok |
| 020 | SHOULD: criterion, values, other values. SHOULD NOT: sole indicator | E-045, E-046, INV-062 to INV-065 | ok |
| 021 | MUST: three components for the same periods. SHOULD: the others where provided | E-048, INV-068, INV-069, INV-102 | ok |
| 022 | SHOULD: after a stop, pause or reduction, against the on-treatment period and the baseline | E-049, INV-070, INV-103 | **R25b-01** |
| 023 | SHOULD: outcomes, consistency, timing, formulation, phases, 15 min. Caveat as SHOULD NOT | E-050 to E-053, INV-071 to INV-075, INV-107 | ok |
| 024 | SHOULD: chronological list by class with dates, dose changes, duration, response, adverse effects, stop reason, acute formulation | E-054, E-055, INV-077 to INV-079, INV-109 | **R25b-01** (duration and course span) |
| 025 | MAY | E-056, INV-080 | ok |
| 039 | SHOULD: next to the comparison, in the history, in the clinician summary | E-047, INV-066, INV-067, INV-104, INV-109 | ok |
| 026 | SHOULD: name, date, recall, total score, grading, change from the baseline administration | E-057, E-058, INV-081, INV-082 | ok (ISS-06) |
| 027 | SHOULD: three domains and severe impairment per period; comparison with the baseline | E-030, INV-026, INV-027 | ok |
| 028 | MUST: three-month view. SHOULD: definitions. SHOULD NOT: diagnosis | E-038, INV-040 to INV-043 | ok |
| 029 | MUST: frequency and acute-medication outputs per type and combined. SHOULD: intensity per type | INV-028 to INV-030 | ok (ISS-09) |
| 030 | MUST: cycles, the A1.1 window, the number of complete cycles | E-060, E-061, INV-086, INV-087 | ok (ISS-03) |
| 031 | SHOULD: bouts and remissions with dates and durations, rates, 15 min and rescue, previous bouts | E-062 to E-064, INV-088, INV-089 | ok (ISS-12) |
| 032 | MAY; caveats SHOULD | E-065, INV-090, INV-100, INV-110 | ok |
| 033 | SHOULD: name, date and score next to the headache outputs; not diagnoses | E-059, INV-083 to INV-085 | ok |
| 034 | SHOULD: concise summary for the period since the previous consultation or a chosen period, with the named components | E-066, INV-094, INV-104, INV-109 | ok (ISS-04) |
| 035 | SHOULD: plain-language overview with the named components | E-067, INV-095, INV-105 | ok |
| 036 | SHOULD: (a) to (d) and the Caveat | INV-055, INV-096 to INV-098 | ok |
| 037 | SHOULD NOT and SHOULD as stated | E-033, INV-091 to INV-093 | ok |
| 038 | SHOULD, and SHOULD NOT as the negative form | INV-099 to INV-101 | ok |

### Mechanical checks (scripts)

| Check | Result |
|---|---|
| IDs (`mech.py`) | <ul><li>67 elements (E-001 to E-067) and 111 invariants (INV-001 to INV-111): none missing, none duplicated.</li><li>Issues ISS-01 to ISS-12 without ISS-07, which section 9 lists as withdrawn.</li><li>No dangling E-, INV- or ISS- reference.</li><li>Every OUT ID exists in Stage 1.</li><li>36 source IDs cited, all within S-001 to S-046 or S-101 to S-106.</li></ul> |
| Fields | <ul><li>Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field.</li><li>Every invariant has exactly one Predicate, Reading, Conformance, Realises and Evidence field.</li></ul> |
| Traceability | <ul><li>39 rows in Stage 1 order, all "full".</li><li>The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches.</li></ul> |
| Invariant levels and scopes | <ul><li>Levels: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 34.</li><li>Each level matches the Stage 1 strength of the part realised.</li><li>Every MUST NOT and SHOULD NOT predicate has the form `¬ F`.</li><li>Scopes: output 78, repertoire 32, context 1.</li></ul> |
| Names (`names.py`) | <ul><li>557 declared names, none declared twice; 190 attribute names.</li><li>Every identifier in the `omn` blocks is declared, a primitive or library name, a keyword, or a bound variable.</li><li>Every attribute selection `.a` names a declared attribute.</li></ul> |
| Typing and definedness, by hand | <ul><li>The partial terms (`÷`, `s(i)`, `first`, `last`, `max`, `days`) are guarded in every invariant I read, including the v24 changes: `daysOf`, `sameIndicatedPeriod`, the INV-012 conjunct, INV-111 and the E-046 components.</li><li>`opt` attributes are used as single values only under a quantifier.</li></ul> |
| Prose claims (`dates.py`, `stops.py`) | <ul><li>The worked examples hold (Values).</li><li>The claim that a stop or pause is "the last day of the course" (section 2.8, E-042, INV-079, INV-109) fails for a course with two stops (R25b-01).</li></ul> |
| Scope sweep | <ul><li>Searched for: record, enter, entry, input, captur*, stor*, persist*, database, JSON, XML, CSV, FHIR, encod*, retention, reminder, "diary information", answer(s).</li><li>The hits are section 1 exclusions; Stage 1 wording ("diary information"); quotes; out-of-scope notes (scoring from answers; INV-076); and the E-060 lead-in wording, settled in review 05.</li><li>Every threshold, formula and relation takes output elements, or context properties used as applicability conditions.</li><li>Every threshold, formula and computed field that is part of the output data is present and cited.</li></ul> |
| Section 8 | <ul><li>ISS-01 to ISS-06 and ISS-08 to ISS-12 are founded. Their Stage 1 citations and source quotes are as described.</li><li>Checks: ISS-02 ("simple analgesic" occurs only on p. 139); ISS-11 (1.3.48 stands in the NICE section on medication overuse headache); ISS-12 (pp. 42 and 209).</li><li>Apart from R25b-01, which is a formal defect of the model, not a Stage 1 issue, no Stage 1 ambiguity is resolved silently.</li></ul> |

## Remarks

### R25b-01 Formal defect: a treatment course may have several stops, and the model reads the end of the course in two incompatible ways
- **Item(s):** INV-001 (admissible contexts); INV-070 with E-049 and INV-103; INV-079 and INV-109 with E-055; section 2.8 and E-008 (day convention). Also affected, already consistent with the earliest-stop reading: E-042 (`notStoppedBefore`, `intervalOnTreatment`), INV-055, INV-058, INV-059, INV-068, E-046 (`evaluatedOnTreatment`) and E-067 (`courseOverlaps`, `courseNotOutside`).

- **Problem:**
  - **What the model says about stops.**
    - Section 2.8 and E-008 date "a stop or a pause … on the last day of the course".
    - INV-001 bounds a course to at most one start. It does not bound the number of stop events, and it does not keep dose changes on or before a stop.
  - **Reading 1: the course ends at its earliest stop.**
    - `notStoppedBefore` (E-042) reads: "no stop or pause of the course of treatment t is dated before d; a stop or pause being dated on the last day of the course (section 2.8), the course has not ended before d".
    - INV-055, INV-058, INV-059, INV-068 and E-046 (`evaluatedOnTreatment`) use it, and `courseOverlaps` and `courseNotOutside` (E-067) read stops the same way.
    - Review 19 confirmed this reading: "a stop before the anchor date also ends the course before the interval".
  - **Reading 2: the course ends at whichever stop a line or view takes.**
    - INV-079 lets a treatment line show any stop event as its stop date, with the duration `days(start, that date)`.
    - INV-109 lets the course summary of an acute line end at any stop event.
    - INV-103 asks for a post-stop monitoring view for every stop event.
    - INV-070 bounds that view's on-treatment period only by `s ≤ q.start ∧ q.end < x`, where x is the first changed day. Unlike INV-068, it does not bound it by `notStoppedBefore`.
  - **Consequence.** For such a course, the model admits both a duration to the earliest stop and a longer one to a later stop. It also admits, as the "on-treatment period" of OUT-022, a period after the course has ended.

- **Evidence:**
  - **Instance** (`stops.py`, predicates as written). A preventive course starts on 1 January 2026, is paused on 10 February 2026 (its last day on treatment), and is discontinued on 30 March 2026 without a restart. INV-001 admits this context.
    - INV-079 admits both a line "stop 10 February 2026, 41 days" and a line "stop 30 March 2026, 89 days".
    - INV-068 excludes an on-treatment period that ends on 28 March: the course ended on 10 February. `courseOverlaps(…, March 2026)` is false.
    - INV-103 requires a post-stop view for the 30 March event. E-049 requires its `onTreatmentPeriod`, because the start precedes 31 March.
    - INV-070 admits 1–28 March 2026, a period wholly within the pause, as that "on-treatment period". The view's periods "after the event" begin on 31 March, although treatment ended on 10 February.
    - E-049 Notes describe that period as ending "on or before the date of a stop or pause, the last day of the course". That holds only for the earliest stop.
  - **The same class: a dose change dated after a stop.** INV-001 does not bound it either, although section 2.8 dates a dose change "on the first day at the new dose", which is a day of the course. INV-103 asks for a post-stop view of a reduction dated after the course has ended, and INV-070 again admits an on-treatment period after that end.
  - **Why the difference matters (Stage 1).**
    - OUT-024 asks for "start and stop dates, dose changes, treatment duration". Its evidence makes the duration decisive for judging a failed preventive:
      - [S-013] "It is not reasonable to test again preventive medications used in the past with no efficacy or with intolerable side effects provided that information on duration, dose and adverse events is sufficient and reliable."
      - [S-013] "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed."
    - So 89 days shown for a course taken for 41 days presents an inadequate trial as adequate. It is shorter than the 8 weeks of OUT-018 ([S-016], [S-018] 14A), and the displayed duration exceeds 12 weeks.
    - OUT-022 asks for the frequency after the stop, pause or reduction to be compared "with both the on-treatment period and the original pre-treatment baseline, so that worsening or rebound above baseline is visible". A period without treatment, shown as the on-treatment period, defeats that comparison.
    - A pause that later becomes definitive is a situation Stage 1 covers: OUT-022 quotes [S-011] "In individuals with migraine who pause treatment, we suggest restarting the treatment if migraine worsens after treatment withdrawal."
  - **New evidence against the earlier "not raised".**
    - Review 15 set the case aside: "Several stop events in one course. … Stage 1 does not say whether a resumed or later-discontinued pause is one course. The model's ordering requirements hold either way. Not raised."
    - Fix 18 referred back to it ("A course with several stop events is the review-15 case, which was not raised"). The oscillation check after iteration 16 listed it as settled.
    - Review 15 predates the v17 day convention and the v18 stop bounds. Those made the earliest stop the end of the course in E-042, INV-055, INV-068, E-046 and E-067, while INV-070, INV-079 and INV-109 still take any stop.
    - The defect is this disagreement between predicates, shown above with the predicates as written, not the ordering that review 15 checked. Fix 18 did not evaluate INV-070 or INV-079 for several stops.
  - **No reversal.** Nothing fixed earlier is reversed:
    - no course-event date of section 2.8 changes (oscillation watch point 4);
    - R18-01's `a ≤ e.date` is not re-added;
    - no v24 by-dates relation is touched.

- **Required change** (one of):
  - **(a) One stop per course, as section 2.8 already reads the dates.**
    - In INV-001, admit at most one stop or pause per treatment course: `∀ t ∈ c.subject.preventiveTreatments ∪ c.subject.acuteTreatments • #{e ∈ c.subject.courseEvents | e.treatment = t ∧ e.kind is stop} ≤ 1`.
    - Also admit no dose change dated after that stop.
    - In E-008, state that a paused course that is later discontinued keeps its one stop, dated on its last day on treatment, and that a treatment resumed after a pause is a new course with its own start.
    - The "every stop or pause" wordings of E-042, INV-055 and INV-068 then remain correct.
  - **(b) Keep several stops, and make the earliest stop the end of the course everywhere.**
    - INV-079 and INV-109 use the earliest stop date for the stop date, the duration and the course span.
    - INV-070 bounds the on-treatment period with `notStoppedBefore(ctx, v.treatment, q.end)`, as INV-068 does.
    - INV-103 asks for no post-stop view of a course event dated after the end of the course, or the model states what such a view shows.
  - **In either case:**
    - align the Readings and Notes of INV-070, INV-079, INV-109, E-049 and E-055, and section 2.8;
    - check the same defect wherever a course event is read against the end of the course, for example the dose-change markers of INV-035 and INV-104 and the dose changes of INV-109.

## Checked and not raised

- **ISS-09: the description of Group D.**
  - ISS-09 describes Stage 1 Group D as containing OUT-014, OUT-015 and OUT-016. Group D also contains OUT-017, whose view shows headache days and acute-medication days from the start of withdrawal.
  - Those measures are the ones that INV-028 already gives per headache type, so the omission changes no reading of OUT-029. Not raised.
  - Fix 02 declined migraine-scoped acute summaries, saying "ISS-09 covers which acute outputs OUT-029 breaks down by type". ISS-09 names only OUT-015 and OUT-016. OUT-023, however, sits in Group E as a treatment-response output, not under "acute medication use". Not raised.
- **ISS-03, "refer to OUT-005 by its ID".**
  - For OUT-009 and OUT-034, the reference is through a range ("OUT-004 to OUT-007", "OUT-004 to OUT-009") that includes OUT-005.
  - The statement is accurate in substance, and fix 20 found the list complete. Not raised.
- **Agreement of counts across the views of one output** (main review 25). Oscillation watch point 1 calls output-wide agreement a new decision, not a defect, and no text claims it. Not raised.
- **INV-111.**
  - It excludes one view that shows migraine days under two labelled definitions. This follows from R24-02 (a), and watch point 2 asks for new evidence, which I do not have.
  - A change whose two values sit in two views with different definitions can satisfy INV-008 only by labelling against INV-111. No invariant requires such a change. Not raised.
- **Settled points, not reopened without new evidence:**
  - the `concerns` reading for all-types indices of mixed subjects (INV-091 to INV-093; reviews 01, 19b, 21);
  - 𝔹-valued given functions and attributes used as formulas (review 22b);
  - the E-060 lead-in wording on diary information (review 05);
  - the baseline month not tied to the month before the start (review 02);
  - the OUT-031 bout-end Caveat as a reading instruction (fix 01);
  - the "> 3 months" readings of INV-045 and INV-089;
  - the E-041 window readings, timings, ages and `excludes`;
  - INV-106 at MUST NOT;
  - the HIT-6 one-month recall; HADS subscales only; the MIDAS labels;
  - "baseline administration"; the HALT-90 total;
  - the 24-hour outcomes of 15-minute summaries;
  - INV-060 with INV-061 for short compared periods;
  - the MUST cycle-line attributes in the overview.
- **A side effect of the INV-012 conjunct.** With `cj = ci`, a lone proportion must be the rounding of a whole number of days divided by the length. This is correct under the definition and section 2.7.
- **The search-log preamble** names S-001, S-007, S-008, S-010 and S-014 as the Stage 1 sources of new quotes. Later iteration entries document the others ([S-011], [S-015], [S-016], [S-018], [S-028], [S-033], [S-034], [S-035]). This is bookkeeping, not a remark category.
- **[S-106] metadata.** The overview page shows the dates cited. Chapter 2, which the model quotes, is unchanged.
- **Unretrieved sources.**
  - [S-024] and [S-025] (site in maintenance) carry no Stage 2 quote.
  - [S-032] (connection reset, then HTTP 301) is reused only through its Stage 1 quote.

## Notes on frozen items (for the human)

None. No item is frozen.
