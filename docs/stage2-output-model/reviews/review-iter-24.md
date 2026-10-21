# Review — iteration 24
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v23
Date: 2026-10-21

## Summary

This is the main review of iteration 24. I am a new, independent reviewer. I checked v23 against its sources and against Stage 1 v18 myself. I read the earlier loop files only so that I would not reopen settled points or reverse earlier fixes.

**State of the files.**
- The working tree was clean at HEAD ac1e28a ("Stage 2 / iter 23: fix (v23)"), and `OUTPUT_MODEL.md` is byte-identical to `history/v23.md` (`cmp`).
- `FROZEN_ITEMS.md` does not exist, and no item carries a `Status: FROZEN` line.

**What I read in full:**
- Stage 2 PROCESS.md.
- Stage 1 v18: sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026), the source table of section 5, and Stage 1 PROCESS.md section 4.
- v23, every section: notation, conformance, all 67 elements and 110 invariants, the traceability table, section 8, sources, search log, and the change log entry for v23.
- Review 23, fix 23, and the oscillation check after iteration 16 with its findings, watch points and settled points.
- By search, the earlier reviews and fixes on every topic below: R04-03 and its sweep, R10b-01, R11-01, review 13 on content outside the covered period, review 16 on caregiver days, fix 11 on cluster-view co-presence, and reviews 03, 10b and 22 on cycle-line levels.

**Result.**
- **Citations.** Every quote in the model is verbatim at its URL, on its stated page or section: 530 fragments, 0 not found. The six new sources (S-101 to S-106) have correct metadata. Translations are faithful. I found no newer version of a source that changes an element: there is no published ICHD-4, only "Work in Progress" papers, and NICE CG150 and TA260 are current.
- **Values.** Every value set, range, band, code label, reference level, offset and threshold matches its source.
- **Scope.** The scope sweep finds no input, storage or input-derivation content.
- **Mechanical checks.** All pass: IDs, references, traceability, levels, names and attribute selections.
- **The v23 change (R23-01).** It is consistent with INV-088, INV-089, INV-011 and the day convention.
- **Two remarks, both formal:**
  - **R24-01.** The relations among per-period values identify a reporting period by its period *atom*, not by its dates. A view may contain several period atoms with the same dates, and the model itself adds such atoms (INV-003). So INV-006 ("one value per measure, period and scope") and the definitional relations INV-024, INV-030 to INV-033 and INV-089 can be evaded. A script shows two examples, each admitted by every relation as written:
    - one view shows two different headache-day counts for March 2026, and more moderate/severe headache days than headache days for that month;
    - one view shows two different April triptan-day counts, with the April and May medication-overuse indicators (MUST) each resting on a different one.
  - **R24-02.** INV-008 lets a view state two different published definitions for the same measure, for example two migraine-day definitions. Nothing then says which definition the shown values follow. This defeats the OUT-002 property and makes the E-016 and E-017 Meanings ("the definition named by the view's definition label") ambiguous. It also breaks the assumption of the R04-03 sweep that counts in one view follow one definition.

## Verification coverage

### Downloads and tools

**Where.** Everything was downloaded with `curl` through the proxy into the fresh directory `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r24/dl`, outside the repository. Scripts are in `…/r24/scripts` and were run with `python3 -I`: `strip.py`, `match.py`, `pages.py`, `mech.py`, `names.py`, `atoms.py` and `atoms2.py`.

**Text extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML pages and Europe PMC XML were stripped of markup.

**HTTP status.** Every request returned HTTP 200. The only exceptions were [S-033] and [S-034]: the first attempt for each was reset by the peer, and both loaded on retry.

**PDFs** (pages, from `pdfinfo`):

| Source | Pages |
|---|---|
| [S-001] | 211 |
| [S-002] | 19 |
| [S-005] | 14 |
| [S-007] | 39 |
| [S-008] | 31 |
| [S-010] | 11 |
| [S-016] | 64 |
| [S-018] | 12 |
| [S-030] | 86 |
| [S-033] | 92 |
| [S-034] | 53 |
| [S-035] | 92 |
| [S-105] | 9 |

**Web pages:**
- [S-015]: the Recommendations page and the Overview page. The Overview reads "Published: 19 September 2012", "Last updated: 03 June 2025" and "Last reviewed: 23 September 2026".
- [S-028]: the NVN module.
- [S-103]: the Cincinnati Children's PedMIDAS page (footer "© 2026").
- [S-106]: TA260, the Overview (published 27 June 2012, last reviewed 11 January 2016), chapter 1 and chapter 2.

**Europe PMC full-text XML:**
- PMC6501455 [S-004], PMC9188162 [S-011], PMC9555163 [S-012], PMC7296705 [S-013], PMC6734476 [S-014], PMC9607711 [S-023];
- PMC3057423 [S-101], PMC4406925 [S-102], PMC183845 [S-104];
- PMC8684566 and PMC6537129, for the MIDAS label variants that the search log names. "little or none" is in PMC8684566. "minimal or infrequent disability" and grades IVa and IVb are in PMC6537129.

**Rendered and read:**
- [S-001] p. 190: the A1.1.1 and A1.1.2 windows "day 1 ± 2 (i.e. days −2 to +3)", whose "±" and "−" have no text mapping;
- [S-034] p. 1, an image: "Возрастная группа" … "дети".

**Metadata.** PubMed esummary confirms the authors, journal, year, volume, issue, pages, DOI and PMCID of S-101 (PMID 20819842), S-102 (25902814), S-104 (12914662) and the S-103 developer paper (11739822). The [S-105] PDF metadata read author Kurt Kroenke, created 2010, modified 2014.

**Newer versions.** A web search finds no published ICHD-4, only "International Classification of Headache Disorders-4 – Work in Progress 1" (Cephalalgia 2024).

### Quote check (`match.py`, `pages.py`)

**Method.**
1. For every line outside the `omn` blocks that carries an `[S-NNN]` tag, the script takes each quoted string. It attributes the string to the nearest preceding tag and splits it at "[...]".
2. It normalises each fragment of at least 6 letters or digits: NFKC, soft hyphens removed, case folded, letters and digits only. It then searches:
   - the tagged source, page by page;
   - the other sources tagged on the line;
   - Stage 1 v18;
   - all downloaded texts.
3. For page-based sources, it compares the page on which each fragment was found with the "p." or "PDF p." of the parenthesis that follows the quote. Offsets: S-016 printed page + 6; S-002 printed page − 1025; S-005 printed page − 802.
   - 75 fragments match their stated page, and none mismatches.
   - The other fragments carry their location in another parenthesis or are short phrases. I read the pages found for each: [S-001] pp. 8, 9, 12, 122–125, 139, 190, 209; [S-008] pp. 9, 12, 13; [S-033] pp. 1, 39, 41, 53; [S-034] pp. 17, 52; [S-035] PDF pp. 23, 48, 57, 83, 86; [S-018] pp. 1, 7, 8; [S-016] PDF p. 7 (printed p. 1) and p. 20 (printed p. 14). All are on the stated pages.

**Results.** Notes on the columns:
- "Verbatim elsewhere": found in another source tagged on the line, or as Stage 1 wording.
- "Not source text": a translation, or a search-log query or row label.

| Source (nearest tag) | Fragments | Verbatim in tagged source | Verbatim elsewhere | Confirmed on rendered page | Not source text | Not found | Unreachable |
|---|---|---|---|---|---|---|---|
| S-001 | 88 | 78 | 7 | 2 | 1 | 0 | 0 |
| S-002 | 11 | 7 | 4 | 0 | 0 | 0 | 0 |
| S-005 | 9 | 2 | 7 | 0 | 0 | 0 | 0 |
| S-007 | 10 | 8 | 2 | 0 | 0 | 0 | 0 |
| S-008 | 29 | 21 | 8 | 0 | 0 | 0 | 0 |
| S-010 | 48 | 39 | 9 | 0 | 0 | 0 | 0 |
| S-011 | 9 | 7 | 2 | 0 | 0 | 0 | 0 |
| S-012 | 3 | 1 | 2 | 0 | 0 | 0 | 0 |
| S-013 | 2 | 2 | 0 | 0 | 0 | 0 | 0 |
| S-014 | 45 | 34 | 11 | 0 | 0 | 0 | 0 |
| S-015 | 56 | 39 | 17 | 0 | 0 | 0 | 0 |
| S-016 | 9 | 7 | 2 | 0 | 0 | 0 | 0 |
| S-018 | 14 | 10 | 4 | 0 | 0 | 0 | 0 |
| S-023 | 6 | 5 | 1 | 0 | 0 | 0 | 0 |
| S-028 | 13 | 10 | 2 | 0 | 1 | 0 | 0 |
| S-029, S-032 | 2 | 0 | 2 | 0 | 0 | 0 | 0 |
| S-030 | 4 | 3 | 1 | 0 | 0 | 0 | 0 |
| S-033 | 49 | 21 | 24 | 0 | 4 | 0 | 0 |
| S-034 | 20 | 8 | 6 | 2 | 4 | 0 | 0 |
| S-035 | 50 | 33 | 4 | 0 | 13 | 0 | 0 |
| S-042 | 3 | 0 | 3 | 0 | 0 | 0 | 0 |
| S-101 | 7 | 4 | 0 | 0 | 3 | 0 | 0 |
| S-102 | 15 | 7 | 2 | 0 | 6 | 0 | 0 |
| S-103 | 12 | 10 | 0 | 0 | 2 | 0 | 0 |
| S-104 | 8 | 3 | 1 | 0 | 4 | 0 | 0 |
| S-105 | 3 | 3 | 0 | 0 | 0 | 0 | 0 |
| S-106 | 5 | 4 | 1 | 0 | 0 | 0 | 0 |
| **Total** | **530** | **366** | **122** | **4** | **38** | **0** | **0** |

**New sources, read in context:**
- **[S-101] PMC3057423, Methods, "Data sources".** "ranges between 36 and 78" and the four categories with their bands are verbatim.
- **[S-102] PMC4406925, "Migraine-related disability".** The four grades with their bands, the IVA/IVB option, and "The recall period for the MIDAS is three months" are verbatim.
- **[S-103] "PedMIDAS Grading Scale".** The rows are verbatim: 0 to 10 Little to none; 11 to 30 Mild; 31 to 50 Moderate; Greater than 50 Severe.
- **[S-104].** "0 to 21 for anxiety and 0 to 21 for depression" is verbatim.
- **[S-105].** The PHQ-9 range 0–27 and the GAD-7 range 0–21 are on P. 6/9. The developers sentence is on P. 8/9.
- **[S-106] TA260 chapter 2.** "The recommended re-treatment schedule is every 12 weeks (see the summary of product characteristics)." is verbatim.

**Translations read and judged faithful:**
- Russian: [S-033] pp. 1, 39, 40, 41; [S-034] pp. 1, 17, 52.
- Turkish: [S-035] PDF pp. 23, 48 (Kutu 8: "Ölçüt…" is its second item and "Yeterli süre…" its seventh, as stated), 57, 77, 83, 86.
- Dutch: the [S-028] PICO.

### Fidelity to Stage 1, requirement by requirement

For each OUT requirement I compared every observable property of the Statement, and every Caveat that constrains the output, with the elements and invariants that realise it. I also compared the level of each part with its Stage 1 strength.

| OUT | Parts and strength | Realised by | Result |
|---|---|---|---|
| 001 | MUST: period with start, end and length; monthly or 28-day; equal-length comparison. Caveat: days per month visible | E-003, E-005, INV-002, INV-003, INV-014, INV-015, INV-108, INV-037, INV-038 | ok |
| 002 | SHOULD: state which definition each measure follows | E-011, INV-008 | **R24-02** |
| 003 | SHOULD: indicator next to the measures. SHOULD NOT: cut-off presented as validated | E-013, INV-011 to INV-013 | ok (see R24-01, last point) |
| 004 | MUST: per period of the time range; ICHD-3 definition | INV-014, INV-009 | ok (relations: R24-01) |
| 005 | MUST for migraine; SHOULD: label | INV-015, INV-008 | ok |
| 006 / 007 | SHOULD; MUST monthly where provided | INV-016, INV-017, INV-108, INV-010 | ok |
| 008 | MAY | E-020 to E-022 | ok |
| 009 | SHOULD: series, markers, weekly where relevant | INV-034 to INV-036 | ok |
| 010 | SHOULD: per period, stated scale, comparison | INV-018, INV-039, INV-032 | ok |
| 011 | SHOULD: summary and label. Caveat as SHOULD NOT | INV-019 to INV-021 | ok |
| 012 | SHOULD: across periods and per treated attack | INV-022, INV-072, INV-076 | ok |
| 013 | MAY | E-027 | ok |
| 014 | MUST: total, class and drug per period | INV-023, INV-024 | ok (relations: R24-01) |
| 015 | SHOULD: per calendar week | INV-025 | ok |
| 016 | MUST: per period, per class and combined; MUST: prompt. MUST NOT: diagnosis | E-032, INV-044 to INV-048 | ok (basis consistency: R24-01) |
| 017 | SHOULD: from start of withdrawal; 4–8-week window; following year; worsening label | E-039, INV-049 to INV-052 | ok |
| 018 | MUST: comparison, values, absolute and percentage change, time points. Caveat: no decision | E-040 to E-043, INV-053 to INV-059, INV-106 | ok |
| 019 | SHOULD: residual burden next to a percentage change | INV-060, INV-061 | ok |
| 020 | SHOULD: criterion, values, other values. SHOULD NOT: sole indicator | E-045, E-046, INV-062 to INV-065 | ok |
| 021 | MUST: three components for the same periods. SHOULD: the others where provided | INV-068, INV-069, INV-102 | ok |
| 022 | SHOULD: after stop, pause or reduction, against on-treatment period and baseline | INV-070, INV-103 | ok |
| 023 | SHOULD: all outcomes, consistency, timing, formulation, phases, 15 min. Caveat as SHOULD NOT | E-050 to E-053, INV-071 to INV-075, INV-107 | ok |
| 024 | SHOULD: chronological, grouped by class, all details, acute formulation | E-054, E-055, INV-077 to INV-079, INV-109 | ok |
| 025 | MAY | E-056, INV-080 | ok |
| 039 | SHOULD: next to comparison, in history, in clinician summary | E-047, INV-066, INV-067, INV-104, INV-109 | ok |
| 026 | SHOULD: name, date, recall, total score, grading, change | E-057, E-058, INV-081, INV-082 | ok |
| 027 | SHOULD: three domains, severe impairment, comparison with baseline | INV-026, INV-027, INV-033 | ok |
| 028 | MUST: three-month view. SHOULD: definitions. SHOULD NOT: diagnosis | INV-040 to INV-043 | ok |
| 029 | MUST: frequency and medication per type and combined. SHOULD: intensity per type | INV-028 to INV-030 | ok (relations: R24-01) |
| 030 | MUST: cycles, A1.1 window, number of complete cycles | E-060, E-061, INV-086, INV-087 | ok |
| 031 | SHOULD: bouts and remissions, rates, 15 min, previous bouts | E-062 to E-064, INV-088, INV-089 | ok (v23 checked) |
| 032 | MAY; caveats SHOULD | E-065, INV-090, INV-110 | ok |
| 033 | SHOULD: name, date, score next to headache outputs; not diagnoses | E-059, INV-083 to INV-085 | ok |
| 034 / 035 | SHOULD | E-066, E-067, INV-094, INV-095, INV-104, INV-105 | ok |
| 036 | SHOULD: (a) to (d) and the Caveat | INV-055, INV-096 to INV-098 | ok |
| 037 | SHOULD NOT and SHOULD as stated | INV-091 to INV-093 | ok |
| 038 | SHOULD; SHOULD NOT as the negative form | INV-099 to INV-101 | ok |

### Mechanical checks (scripts)

| Check | Result |
|---|---|
| IDs (`mech.py`) | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110): none missing, none duplicated. Issues ISS-01 to ISS-12 without ISS-07, which is withdrawn in section 9. No dangling E-, INV-, ISS- or S- reference. 36 source IDs cited, all within S-001 to S-046 or S-101 to S-106. |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. Every invariant states its scope. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every row, the Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. Every OUT ID named exists in Stage 1. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33, as stated. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`. |
| Attribute levels | 172 level-annotated attributes: core 94, MUST 29, SHOULD 47, MAY 2. The section 2.5 typing rule holds for all of them. |
| Names (`names.py`) | 745 declarations (paragraph names, constants, tags and attributes); no paragraph name declared twice. Every identifier in the `omn` blocks is declared, a primitive, a bound variable or `refs`. Every attribute selection `.a` names a declared attribute. |
| Partial terms | Every `÷`, `s(i)`, `first`, `last`, `max`, `min`, `days`, `classOf`, `periodEndFrom`, `publishedRecall` and `scoreRange` term was read by hand; all are guarded. Every `opt` attribute is used inside a quantifier or compared as a set. |
| Date examples | All correct:<br>• E-042 and INV-055: 1 April; 26 March; 26 February – 25 March; stops on 10 February, 30 March and 31 March;<br>• INV-049: day 43; review window 7 April – 5 May; 6 April;<br>• E-007: 67 days;<br>• INV-105: 43 days;<br>• E-063: 42 and 143 days.<br>INV-045: the shortest span of more than three months has four calendar months, or four 28-day periods. |
| Property claims | `scopeFor` picks exactly one scope. `courseNotOutside` agrees with `courseOverlaps` for a course with one stated start. The INV-003 Notes derivation holds. **INV-006 "same period" fails for same-dated period atoms (`atoms.py`, `atoms2.py`): R24-01.** |
| Scope sweep | grep for record, enter, entry, input, capture, store, database, serialisation, JSON, XML, CSV, FHIR, encoding, retention, persist, reminder, data field, data-entry, logged and answers. The only hits are:<br>• the section 1 exclusions;<br>• the section 2.1 disclaimer;<br>• the [S-014] HALT-30 sentence "accordingly records days affected" (an instrument's recall; settled since review 01);<br>• the E-057 Notes that leave scoring from answers out of scope;<br>• INV-076's statement that it avoids a derivation.<br>Every derived attribute's relation takes output elements, context properties or cited constants as arguments. Every threshold and formula that is part of the output data is present and cited: 8.2 levels and span; A1.1 window; remission duration; review window; 18 time points; responder thresholds and control levels; instrument bands and ranges; completeness proportion; percentage change; rate; outcome proportion. |

## Remarks

### R24-01 Formal defect: the relations among per-period values identify a reporting period by its period atom, not by its dates, so one view can show contradictory values for the same reporting period
- Item(s): INV-006 (Predicate, Reading); E-014 `daysOf`; the relations that rest on it, INV-024, INV-030, INV-031, INV-032 and INV-033; the EventCount conjuncts of INV-030 and INV-033 and the rate–count conjunct of INV-089; INV-011 and INV-012 (completeness indicators); E-032 / INV-045 (the basis of the medication-overuse indicator); section 7 rows OUT-004, OUT-014, OUT-016 and OUT-029.
- Problem:
  - **What the predicates compare.** INV-006 forbids two different counts "of the same count for the same period and type scope" in a view, but tests `m.period = n.period`, the identity of the period *atom*. `daysOf(v, k, p, sc)` (E-014) collects the counts whose `m.period = p`, also an atom. The relations INV-024, INV-030, INV-031, INV-032 and INV-033 use `daysOf`. The EventCount comparisons of INV-030 and INV-033 (`e.period = f.period`, `e.period = a.period`) and the rate–count conjunct of INV-089 (`e.period = p`) also compare atoms.
  - **The model admits several period atoms with the same dates in one view.**
    - Period atoms have identity (section 2.5), and nothing ties a period atom to its dates: no invariant says that two periods of a view with the same start and end are one atom.
    - The model adds such atoms itself. INV-003's last conjunct shows "another period atom with the same dates" in a view. The INV-003 Notes add: "a period atom with given dates and the kind of the value's period can be added to any view".
    - Views that must show both a series and comparisons naturally contain the same month twice: for example, the clinician-facing summary (INV-104) holds its monthly series and the response comparison of each preventive treatment (INV-056), whose monthly periods may have the same dates as months of the series.
  - **Consequence.** Every relation "in one view, for the same period" holds only per atom. A view can therefore show, for one reporting period as the reader sees it (its dates), values that contradict the definitions those relations encode. Section 3.3 item 5 says definitional invariants exclude exactly such outputs: "an atom that does not satisfy it is not an instance of the element … it excludes only outputs that show a value contradicting the definition of the element". The Readings claim more than the predicates guarantee:
    - INV-006: "A view does not show two different values of the same count for the same period and type scope."
    - INV-024: "In one view, for the same period and type scope: the days with any acute medication are at least the days with each class …"
    - INV-031: "In one view, for the same period and scope: moderate/severe headache days do not exceed headache days …"
    - INV-030: "In one view and period …"
    - INV-089: "In one view, the attack rates of one period and type scope rest on one whole number of attacks, which is the attack count shown for that period and scope where the view shows one".
  - **Script check (`atoms2.py`).** It evaluates INV-002, INV-005, INV-006, the first conjunct of INV-011, INV-024 (class ≤ total, drug ≤ class), INV-031 (moderate/severe ≤ headache days) and INV-045 literally on two views. Every one of these predicates holds in both.
    - **View 1 (for example a treatment review view, INV-068 MUST).**
      - It contains three period atoms for March 2026 (1–31 March) and one for December 2025.
      - It shows, all over all headache types and all for March 2026:
        - headache days 5 (atom 1) and headache days 7 (atom 3);
        - moderate/severe headache days 9 (atom 2);
        - days with any acute medication 4 (atom 1);
        - triptan-class days 9 (atom 2);
        - sumatriptan days 8 (atom 1).
      - So the view shows two different headache-day counts for one month, more moderate/severe headache days than either, and more triptan days and more sumatriptan days than days with any acute medication.
    - **View 2 (the medication-overuse indicators of INV-044, MUST).**
      - The April 2026 triptan indicator has the span January–April, with basis 11, 11, 11 and 8 days, and shows `levelNotReached`.
      - The May 2026 triptan indicator has the span February–May on its own February, March and April atoms, with basis 11, 11, 12 and 11 days, and shows `levelReached`.
      - So the view shows April 2026 triptan days as both 8 and 12, and the May "reached" rests on the 12.
      - INV-045 holds for each indicator. INV-006 holds because the two April counts refer to different atoms.
  - **The same gap for completeness.** INV-011 asks for an indicator with `ci.period = m.period` for each atom, and INV-012 relates the forms within one indicator only. So two completeness indicators for the same dates (one per atom) may state different covered days.
  - **Stage 1.**
    - OUT-004 asks for "the number of headache days per reporting period", with headache days as ICHD-3 defines them (INV-009). A view that shows two different numbers for one reporting period does not report that number.
    - OUT-016 (MUST) asks whether use "reached the levels of regular use", which the reader can judge only from one consistent basis.
    - OUT-003 asks for "an indicator" per reporting period.
  - **Not considered before.**
    - No earlier review raised the identity of a reporting period in these relations. The R04-03 sweep (fix 04) states: "INV-024, INV-030, INV-032 and INV-033 compare counts of one measure and one definition (same view, same period)". Here "same period" is read as dates, which the predicates do not secure.
    - INV-006 and `daysOf` have been unchanged since v00, so the change below reverses no fix.
    - It does not touch the co-presence decisions (R10b-01, R11-01; iteration-16 watch point 7): membership of values in a comparison stays tied to its period atoms (INV-038, INV-056), and a value in another view with a period of the same dates stays "not a value of that comparison" (INV-003 Notes). No other watch-point item is involved.
- Evidence:
  - INV-006: `(∀ v : View • ∀ m, n ∈ v.content ∩ DayCount • m.measure = n.measure ∧ m.period = n.period ∧ m.typeScope = n.typeScope ⇒ m = n) ∧ (… EventCount …)`; Reading as quoted above.
  - E-014: `fun daysOf(v : View, k : DayMeasure, p : Period, sc : TypeScope) : set ℕ ≙ {m ∈ v.content ∩ DayCount | m.measure = k ∧ m.period = p ∧ m.typeScope = sc • m.days}   -- at most one member (INV-006)`.
  - INV-003 Notes: "the period atom of the value itself where the value is shown in the same view, and otherwise another period atom with the same dates, since every atom is part of one view"; "Satisfiability: a period atom with given dates and the kind of the value's period can be added to any view".
  - INV-031 Notes: "Every relation compares counts whose definitions the output names and which are nested under them. A moderate/severe headache day is, under the published definitions, a day with headache".
  - Section 3.3 item 5, as quoted above.
  - Stage 1 OUT-004 Statement: "The diary output MUST report the number of headache days per reporting period, with 'headache days' as defined in ICHD-3 'Definitions of terms' [S-001]"; OUT-016 Statement: "whether acute medication use reached the levels of regular use that ICHD-3 code 8.2 and its subtypes … describe".
  - Script output (`…/r24/scripts/atoms2.py`): "INV-002 True INV-005 True INV-006 True INV-031 (MSHD<=HD) True INV-024 (class<=total, drug<=class) True INV-011 c1 True"; "INV-045 April True INV-045 May True INV-005 True INV-006 True"; "April 2026 triptan days shown in the view: [8, 12]".
- Required change: make the uniqueness of INV-006, and the relations among per-period values, hold for a reporting period as its dates identify it, at least within one view as their Readings state. Update the Readings and Notes of the items listed, and the INV-003 Notes. Options:
  - **(a) Compare by dates.**
    - In INV-006, require that two counts of the same measure (or event) and type scope whose periods have the same start and end show the same number. For example: `∀ v : View • ∀ m, n ∈ v.content ∩ DayCount • m.measure = n.measure ∧ m.typeScope = n.typeScope ∧ sameSpan(m.period, spanOf(n.period)) ⇒ m.days = n.days`, and the same for `EventCount.count`.
    - Let `daysOf` collect the counts whose period has the dates of p (`sameSpan(m.period, spanOf(p))`). Compare the periods of the EventCount conjuncts of INV-030 and INV-033 and of the rate–count conjunct of INV-089 by dates as well.
    - Then INV-024, INV-030 to INV-033 and INV-089 apply to every value of the same reporting period.
    - Do the same for completeness indicators: two indicators of the same dates state the same covered days and the same proportion.
    - For migraine days and moderate/severe headache days, whose published definitions differ, this presupposes that the values of a measure in one view follow one definition (R24-02).
  - **(b) One period atom per dates in a view.**
    - Require that the periods a view shows with the same start and end are one atom.
    - Then check every invariant that fixes a period's kind in the same view. February of a common year is both a calendar month and a 28-day period, and INV-004 fixes the kind of the periods of a series, while INV-045 and INV-056 fix the kinds of span and comparison periods.

  Either option may also be applied output-wide, so that two views of one output do not show different values for the same measure, scope and dates. That is a choice for the fixer.

### R24-02 Formal defect / coverage gap: a view may state two different published definitions for the same measure, and nothing states which one its values follow (OUT-002)
- Item(s): INV-008 (Predicate, Reading); E-011 (`labelledAs`, Meaning, Notes); E-016 and E-017 (Meaning); INV-030 (migraine days and moderate/severe headache days per type against combined); E-040 Notes and INV-003 (changes whose values are shown in another view); section 7 row OUT-002.
- Problem:
  - **INV-008 asks only that a label exist.**
    - The predicate is `reports(v, lm) ⇒ ∃ l ∈ v.content ∩ DefinitionLabel • l.measure = lm`.
    - A view may therefore show two labels for migraine days that name different published definitions, and one migraine-day count per period. For example, the IHS trial guideline section 1.3.1.1 [S-002] and the 2026 eDelphi definition [S-043], both named as examples in OUT-002.
    - INV-008 holds, and no element ties a shown count to one of the labels. A `DayCount` has no definition attribute, and a `DefinitionLabel` refers to no value.
    - Only for headache days (INV-009, MUST) and attacks (INV-010, SHOULD) is the definition fixed. For migraine days and moderate/severe headache days a view may state several.
  - **The model presupposes one definition per measure and view, but does not require it.**
    - E-016 defines migraine days "under the published definition named by the view's definition label", and E-017 does the same for moderate/severe headache days: one label.
    - E-011 defines `labelledAs(v, lm, d)` as "the view states a definition for the measure lm and every definition it states for lm is d". So the model foresees views that state several definitions, and uses the single-definition case only as the antecedent of one INV-031 conjunct.
    - With two labels, the meaning of E-016 and E-017 is undefined: ambiguous semantics.
  - **OUT-002 is not secured.**
    - OUT-002 asks outputs to "state which published definition of each measure they follow", because "different definitions give different numbers" and a reader can compare a diary value with guideline or trial values "only if the definition used is visible" (Rationale).
    - A view with two migraine-day labels and unlabelled counts does not state which definition its migraine days follow, yet the model counts it as conformant to INV-008.
  - **The relations rely on one definition.**
    - The R04-03 sweep (fix 04) accepted INV-024, INV-030, INV-032 and INV-033 because they "compare counts of one measure and one definition (same view, same period)". INV-008 does not guarantee this.
    - In such a view, INV-030 compares the migraine days (and moderate/severe headache days) of one headache type with those of all types combined. These may follow different definitions, under which the relation does not hold (R04-03 showed that published migraine-day definitions count different days).
  - **A change whose values are in another view.**
    - E-040 Notes: a change shown outside a response comparison may have "its two values … shown in another view of the output, so the view that shows the change states … the definition of its measure (INV-008, OUT-002)".
    - Nothing ties that statement to the definition followed by the values in their own view. The view of the change may name definition A while the values it refers to are shown, and labelled, under definition B. The same holds for a residual burden and a composite index (`referencedValues`).
  - **Not considered before, and no reversal.** No earlier review or fix raised a view with several labels for one measure. The R04-03 fix introduced `labelledAs` for INV-031 and kept INV-008 as it was. Neither INV-008 nor E-011 is a watch-point item.
- Evidence:
  - INV-008 Predicate as quoted above; Reading: "A view that reports migraine days, headache days, moderate/severe headache days or attacks … states which published definition of each it follows."
  - E-011: `pred labelledAs(v : View, lm : LabelledMeasure, d : PublishedDefinition) ≙ (∃ l ∈ v.content ∩ DefinitionLabel • l.measure = lm) ∧ ∀ l ∈ v.content ∩ DefinitionLabel • l.measure = lm ⇒ l.definition = d`; Meaning: "`labelledAs(v, lm, d)` holds when the view states a definition for the measure lm and every definition it states for lm is d."
  - E-016 Meaning: "under the published definition named by the view's definition label"; E-017 Meaning: "under the definition named by the view's definition label".
  - fixes/fix-iter-04.md, R04-03 row: "INV-024, INV-030, INV-032 and INV-033 compare counts of one measure and one definition (same view, same period)."
  - E-040 Notes, as quoted above.
  - Stage 1 OUT-002 Statement: "Outputs that report migraine days, headache days, moderate/severe headache days or attacks SHOULD state which published definition of each measure they follow (for example ICHD-3 'Definitions of terms' [S-001], IHS trial guidelines [S-002][S-003], or the 2026 eDelphi consensus definition of a migraine day [S-043])"; Rationale: "There is no single universally adopted definition of a migraine day; different definitions give different numbers. A reader can compare a diary value with guideline or trial values only if the definition used is visible."
- Required change: make every value of a defined measure follow one stated definition, so that the definition each shown value follows is stated. Update INV-008 (Reading), E-011 (Meaning, Notes), E-016, E-017, the E-040 Notes and row OUT-002. Options:
  - **(a) One definition per measure in a view.**
    - Replace the consequent of INV-008 by `∃ d : PublishedDefinition • labelledAs(v, lm, d)`, keeping SHOULD.
    - State, definitionally, that the values of one measure shown in or referred to by a view follow one definition, the one its label names.
    - For a change, residual burden or composite index whose values are shown in another view, require that where both views state a definition for the measure, the two are the same. Alternatively, require that the values follow the definition the referring view states.
  - **(b) Tie each value to its definition.**
    - Give the counts of migraine days and moderate/severe headache days (and, if the model allows other definitions, of attacks) a definition, for example an attribute naming a `PublishedDefinition`. Require that the definition of every shown value is stated in its view.
    - State the relations INV-030 and INV-031 (and R24-01's agreement) only between values of the same definition.

## Checked and not raised

- **The v23 change (R23-01).**
  - `ongoing`, `lastDay = ctx(outputOf(x)).asOf` and the new conjunct `∀ e ∈ x.end • e ≤ ctx.asOf` are well-typed (`ctx` and `outputOf` are total) and guarded (`days(s, e)` behind `s ≤ e`).
  - The INV-088 overlap test asks for rates for the same bouts as before, because the as-of date is not before the start of the selected time range. The rate period stays within its bout.
  - The E-063, E-062, INV-089 and row OUT-031 texts agree with the predicates, and the example dates are correct (42 days; 143 days; 1 September).
  - Phase items that reach beyond the covered period without a completeness indicator for those days: by design (review 13, "the history of previous bouts"; fix 23 checked E-013 and INV-011). Not raised.
- **Cluster view bouts, remissions and rates are references not placed in the view.** Fix 11 declined this with a reason (OUT-031 asks for no co-presence), and I have no new evidence. Not raised.
- **Caregiver lost productive days bounded by the period length (INV-033).** Review 16 settled it: other figures can be shown as `otherCaregiverImpact`. Not raised.
- **HALT-90 total and question 5.**
  - [S-014] "Scoring HALT" says that question 5 "gives rise to a simple count for which the unit is not whole days" and that it is included in the HALT-90 total that is graded.
  - The total is still a whole number (`wholeNumberScores` holds), and Table 18 heads its bands "Days lost in last 3 months", so the unit comment "days for … HALT" has a source. Not raised.
- **MUST attributes of a `CycleLine` shown in the patient-facing overview.** Reviews 03, 10b and 22 examined them. Not raised.
- **Antichain of `possibleHeadacheTypes` (INV-001) with treatment conditions read on `givenFor`.** A subject whose earlier migraine is coded only as "1." cannot also list 1.3 for later chronic migraine. This is an edge case of how a context is stated, with no Stage 1 basis for a change. Not raised.
- **The most bothersome symptom "in the response of individual treated attacks" (OUT-012).** It is represented by the outcome `mostBothersomeSymptomAbsent` on every attack line, and the symptom itself per period by E-026. Ok.
- **Value sets.** All match their sources:
  - the HIT-6, MIDAS, PedMIDAS and HALT-90 bands and labels (including the overlaps at 20);
  - the HADS, PHQ-9 and GAD-7 ranges and the recall periods;
  - the ICHD-3 8.2 levels (15 for 8.2.3, 10 otherwise), the `classesOf826` of criterion B and the 8.2.6 note 2 exclusion of 8.2.1–8.2.5;
  - the A1.1 window (`plusDays(d1, −2)` to `plusDays(d1, 2)`, day 0 absent) and the remission bound;
  - the code labels (pp. 8, 9, 12);
  - the 18 evaluation rules: offset, anchor, timing, ages and `excludes` each checked against its quote;
  - the six named criteria, including the IHS Q6 MIDAS ranges, and the four control levels.
- **Section 8.**
  - Each of ISS-01 to ISS-06 and ISS-08 to ISS-12 is founded, and its quotes are verbatim on the stated pages.
  - For ISS-02, a page-by-page search confirms that "simple analgesic" occurs only on [S-001] p. 139. The other hits for "simple" are "simplex", "a simple skin biopsy", "Simple advice" and "herpes simplex".
  - No Stage 1 issue is worked around silently. R24-01 and R24-02 are model defects, not Stage 1 issues.
- **Search log.**
  - There is no entry for iteration 23; fix 23 made no search. The languages covered by the Stage 2 searches are justified in the log ("national-language versions are translations with the same score bands").
  - Neither point is a remark category of PROCESS section 9.
  - The author of S-102 is "Pavlović" in PubMed, written without the diacritic in the model; trivial.
- **Settled points, not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the "> 3 months" readings of INV-045 and INV-089;
  - INV-023 at any granularity, and INV-027 tied to preventive treatments;
  - the HIT-6 one-month recall, and MIDAS Grade IV undivided;
  - "baseline administration" as any earlier administration;
  - INV-060 with INV-061 for compared periods shorter than 28 days;
  - `mostRecent` with 28-day periods;
  - empty `remissions` in chronic cluster headache (ISS-12);
  - the 24-hour outcomes in 15-minute summaries;
  - the Turkish Box 8 and Danish criteria outside `namedCriteria`;
  - the history-wide `acuteMedications` (watch point 2);
  - "one item suffices" and the ties of INV-105 (watch point 1);
  - INV-098 read on period starts (watch point 6);
  - E-039 `reviewWindow`;
  - the CycleLine lead-in (watch point 7).
- **Oscillation watch points.**
  - R24-01 concerns INV-006, `daysOf` and the relations among per-period values. R24-02 concerns INV-008 and the definition labels.
  - Neither names an item of watch points 1–8. Neither reverses an earlier fix: R04-03 is extended, and the co-presence derivations of R10b-01 and R11-01 are kept.

## Notes on frozen items (for the human)

None. No item is frozen.
