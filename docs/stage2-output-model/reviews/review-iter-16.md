# Review — iteration 16
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v15
Date: 2026-10-21

## Summary

This is the main review of iteration 16: an independent fact-check and review of v15. `OUTPUT_MODEL.md` is byte-identical to `history/v15.md` (checked with `cmp`).

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 after OUT-025), and the source table of section 5;
- v15: every element, every invariant, and sections 7 to 12;
- review 15, fix 15 and the word-level v14 → v15 diff;
- the oscillation check after iteration 12 and its seven watch points;
- the parts of earlier reviews and fixes that touch my topics: review 03 ("a response comparison right after the treatment start"), the INV-068 discussions (reviews 02, 03, 10–13; fix 15 identifying-property table), fix 11 ("treatment effect" by one item), fix 14 (R14-02 (d), the period tie of the acute alternative of INV-105).

**Earlier decisions.** FROZEN_ITEMS.md does not exist, and no item of v15 carries a FROZEN marker. My remark does not reverse an earlier fix and does not re-raise a declined remark; its relation to the watch points and to fix 15 is stated in the remark.

**Result.**
- **Citations.** No defect. 475 quoted fragments were extracted by script; every reachable fragment is verbatim at its stated location. This time UCL Discovery was reachable, so the four [S-007] fragments that reviews 13–15 could not re-check (E-064, "≥ 14 attacks per week on average", section 2.2, p. 10) are verified verbatim. Only [S-028] (richtlijnendatabase.nl, maintenance page) remained unreachable: 5 fragments, unchanged since v06 and verified by earlier reviews.
- **Value sets, codes, labels, thresholds.** No defect.
- **Mechanical checks.** All pass.
- **Scope sweep.** No input, storage or derivation-from-input content. The three predicates new in v15 (`summarisesMedication`, `adherenceFor`, `courseOverlaps`) take only output elements and subject properties as arguments.
- **One remark (R16-01, OUT-035).** The acute alternative of the overview's treatment effect (INV-105) is tied, since v15, to "an acute medication the subject has used". `acuteMedications` is the subject's whole history up to the as-of date (E-008), so a 0-attack summary of a medication last taken years before the covered period meets the conjunct. The overview then shows no effect of any treatment the patient follows in that period. The v15 Notes say the treatment effect "is that of the treatment the patient follows during the covered period", and v15 already applied this to the preventive alternative (`courseOverlaps`). The acute part of the antecedent is still history-wide too.

## Verification coverage

### Method

- **Downloads.** All were made with `curl` (through the configured proxy) into the fresh directory `/tmp/r16-dl-xWi2`, outside the repository.
  - **Stage 1 URLs, HTTP 200:**
    - PDFs: S-001 (211 pp.), S-002 (19), S-007 (39; UCL Discovery reachable this time), S-008 (31), S-010 (11), S-016 (64), S-018 (12), S-030 (86), S-033 (92; the first attempt was reset by the peer, the second succeeded), S-034 (53; two resets, the third attempt succeeded), S-035 (92; created 28 August 2025);
    - S-015: the Recommendations page and the Overview page (`datetime` 2012-09-19 and 2025-06-03).
  - **Europe PMC full-text XML (HTTP 200):** S-011 (PMC9188162), S-012 (PMC9555163), S-014 (PMC6734476), S-023 (PMC9607711), S-042 (PMC12279330), S-101 (PMC3057423), S-102 (PMC4406925), S-104 (PMC183845).
  - **New-source pages (HTTP 200):**
    - S-103 (footer "© 2026 Cincinnati Children's Hospital Medical Center");
    - S-105 (9 pp.; metadata: author Kurt Kroenke, created 2010-06-22, modified 2014-04-16);
    - S-106: chapter 2, chapter 1 and the overview page ("Published 27 June 2012", "Last reviewed: 11 January 2016").
  - **Unreachable:** S-028. The page returned HTTP 200 twice with "Deze pagina is tijdelijk niet bereikbaar". The Wayback availability API names a snapshot of 9 February 2026. Fetching it over http was refused by the egress policy (HTTP 403 "Blocked by egress policy"), and over https the connection was reset twice.
- **Extraction.** PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML and XML were stripped of scripts and markup, and entities were unescaped.
- **Read by eye after rendering with `pdftoppm`:**
  - ICHD-3 p. 190: the A1.1.1 and A1.1.2 windows "day 1 ± 2 (i.e. days −2 to +3)", whose "±", "−" and "+" have no text mapping, and note 2;
  - the S-034 title page, an image that reads "Возрастная группа" followed by "дети".
- **Scripts.** All are in the session scratchpad, `r16/`, and were run with `python3 -I`:
  - `quotes.py`: every double-quoted string outside `omn` blocks on a line with an `[S-NNN]` tag, split at `[...]` and "…", 475 fragments. Each fragment is searched in three normalisation passes (NFKC, quotes, dashes and whitespace; line-end hyphens; letters and digits only). It is searched first in the source of the nearest preceding tag, page by page, then in the other sources tagged on the line, then in Stage 1 v18. Every match made only in the third pass was read in context (ICHD-3 "≥" glyphs and line-end breaks, section headings);
  - `mech.py`: headings, references, traceability, levels, scopes, prohibition form, attribute levels and the typing rule;
  - `names.py`: declarations and uses of names and attribute selections in `omn` blocks;
  - `html2txt.py`.
- **Metadata.** PubMed esummary confirms:
  - S-101: Yang M, Rendas-Baum R, Varon SF, Kosinski M; Cephalalgia 2011;31(3):357–67; 10.1177/0333102410379890; PMC3057423;
  - S-102: Pavlović JM … Lipton RB; J Headache Pain 2015;16:24; 10.1186/s10194-015-0503-y; PMC4406925;
  - S-104: Snaith RP; HQLO 2003;1:29; 10.1186/1477-7525-1-29; PMC183845;
  - the PedMIDAS developer paper: PMID 11739822; 10.1212/wnl.57.11.2034.
- **Newer versions.**
  - A web search finds no published ICHD-4, only the 2024 "Work in Progress" paper.
  - The NICE CG150 page still shows its last update as 3 June 2025, and TA260 was last reviewed on 11 January 2016.
  - Nothing newer changes an element.

### Citations

"Script" = found verbatim in the downloaded source at the stated location. "Stage 1" = a fragment of a Stage 1 quote, checked against Stage 1 v18. Fragments are counted under the nearest preceding source tag on their line.

| Source | Fragments | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 | 65 | 64. By script, 57: labels pp. 8, 9, 12; 8.2–8.2.8 pp. 122–125; 8.2.3 comment p. 123; Definitions of terms pp. 209–210; remission p. 209; A1.1 note 2 p. 190. By hand on the rendered p. 190, 3. As Stage 1 fragments, 4. The remaining 1 is a search-log row label. "Simple analgesics" occurs only on p. 139 (10.1.1 comments). | 0 | 0 |
| S-002, S-005 | 14 | 14. By script, 10 (S-002 PDF pp. 10–12). As Stage 1 fragments, 4 | 0 | 0 |
| S-007 IHS cluster | 10 | 10. By script, 8: p. 10 (section 2.2, item a, "≥ 14 attacks per week on average", and its echoes), p. 22, p. 25. As Stage 1 fragments, 2 | 0 | 0 |
| S-008 IHS 2024 | 28 (+2 on lines tagged otherwise) | 30. By script, 27: Q2 pp. 5, 9; Q6 pp. 6, 12; Q6 Evidence p. 13; Q13 p. 17. As a Stage 1 fragment, 1. By hand, 2: "acceptable for treatment continuation beyond three months" (E-008 Evidence) and "for treatment continuation beyond three months" (E-045 Notes), on p. 12, where a line break splits the phrase | 0 | 0 |
| S-010 IHS 2025 | 44 | 44. By script, 36, at p. 6: the four control levels, the migraine-day definition paragraph, the "proxy" sentence, the insufficient-control sentence. As Stage 1 fragments, 8 | 0 | 0 |
| S-011, S-014, S-016, S-018, S-023, S-030, S-032, S-042 | 82 | 81. By script, 70: S-011 Background and question 3; S-014 HALT recall, units and Table 18 "Grading of HALT-90" with its "≥20" row; S-016 PDF pp. 7, 20; S-018 pp. 1, 7, 8; S-023 "mindestens 50 %", "um mindestens 5 Punkte", "um mindestens 30 %", "sinkt"; S-030 PDF p. 19. As Stage 1 fragments, 11. The other 1 is counted under S-008 above | 0 | 0 |
| S-015 NICE CG150 | 49 | 48. By script, 36: 1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48 and the Overview population sentence. As Stage 1 fragments, 12. The other 1 is the S-008 phrase above | 0 | 0 |
| S-028 NVN, S-029 | 13 | 8. As Stage 1 fragments, 7 (including the [S-028] Aanbeveling fragments of E-041). By script, 1 (a fragment of another source on the same line). 1 is a translation | 0 | 4 Stage 2 fragments: the PICO sentence and the section name "Zoeken en selecteren", in E-041 and in the search log. 1 more is counted under S-033: the echo "kinderen en volwassenen". Tried as above |
| S-033 Russian adults | 45 | 40. By script, 38: p. 1 title; p. 4 "М – мигрень"; pp. 39, 40, 41, 53; fragments of other sources on the same lines. As Stage 1 fragments, 2. The remaining 4 are translations | 0 | 1 (the S-028 echo above) |
| S-034 Russian children | 22 | 18. By script, 12: p. 17; p. 52 flowchart. By hand on the rendered title page, 2. As Stage 1 fragments, 4. The remaining 4 are translations | 0 | 0 |
| S-035 Turkish protocol | 50 | 37 by script: Kutu 8 p. 48 (second and seventh items); 3.3 b p. 23; 3.6.3.9 p. 57; section 6 heading p. 77; chapter 7 heading pp. 82–86; 7.1 p. 83; 7.3 p. 86 ("2 k ez" as printed). The other 13 are translations | 0 | 0 |
| S-101 to S-106 | 53 | 38. S-101: "Data sources", 4. S-102: "Migraine-related disability", 10. S-103: grading table, 12. S-104: 3 by script, plus 1 Stage 1 fragment. S-105: P. 5/9–6/9, 3. S-106: chapter 2 para. 2.1 (last sentence) and chapter 1 ("less than a 30% reduction in headache days per month after 2 treatment cycles"), 5. The remaining 15 are search-log queries and labels | 0 | 0 |
| **Total** | **475** | **432 verified**: 369 by script in the downloaded sources; 7 by hand (3 on the rendered ICHD-3 p. 190, 2 on the rendered S-034 title page, 2 S-008 phrases split by a line break); 56 as Stage 1 v18 fragments. 22 more are translations and 16 search-log text | **0** | **5** (S-028) |

**Translations.** Every new translation was checked against the source text: the [S-033], [S-034] and [S-035] translations of E-041 and E-045, and the [S-028] PICO sentence ("Patiënten (kinderen en volwassenen) met migraine, bij wie preventieve behandeling geïndiceerd is"). All are faithful.
- "uygulama süreleri uzatılabilir" is rendered as "the application intervals may be extended". It literally says the application periods may be prolonged. The rendering fits the context, a sentence on injections at 3-month intervals, and the sentence is quoted only as a time that is not an evaluation time point (E-041 Notes). It supports no element.

### Value sets, codes, units, labels and thresholds

All were checked against the downloaded sources, and all are correct:
- ICHD-3 code labels (E-009; pp. 8, 9, 12);
- the 8.2 reference levels 10/15 with "> 3 months" (E-032; pp. 122–125);
- 8.2.6 criterion B (p. 124) and note 2 (p. 125); the 8.2.3 comment (p. 123);
- the A1.1 window and "there is no day 0" (E-060; rendered p. 190);
- remission "must exceed three months" (E-063);
- HIT-6: 36–78, ≤49/50–55/56–59/60–78 and the four category labels;
- MIDAS: I–IV with the [S-102] labels, 0–5/6–10/11–20/≥21, three-month recall;
- PedMIDAS: 0–10/11–30/31–50/>50 with labels "Little to none", "Mild", "Moderate", "Severe";
- HALT-90: 0–5/6–10/11–20/≥20 with the Table 18 labels; HALT-30 one month, no grading;
- HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21;
- IHS Q6: 50 %, the 30 % chronic alternative, MIDAS ≥5 points for baseline 11–20 and ≥30 % for ≥20, HIT-6 ≥5;
- DMKG/ÖKSG/SKG: 50 %, 5 points, 30 %;
- NICE 1.3.28 (50/30 %), 1.3.29 (30 %, two cycles) and the Russian 7.1 criterion (50 %);
- the IHS 2025 control levels;
- NICE 1.3.48: 4–8 weeks; TA260 re-treatment every 12 weeks.

The 18 E-041 rule constants and the 6 criterion constants are unchanged from v14 (watch point 1). I re-read their source passages as quoted (offsets, anchors, timings, populations); no value differs from its source.

### Fidelity to Stage 1 (all 39 requirements)

| OUT | Result |
|---|---|
| 001 | Periods with dates and length at MUST (E-005, INV-002, INV-003); monthly frequency outputs (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); Caveat by `lengthDays`. OK. |
| 002 | SHOULD labels in every reporting form (INV-008); ICHD-3 for headache days at MUST (INV-009, from OUT-004). OK. |
| 003 | SHOULD indicator for every summarised period, including adherence windows (INV-011, INV-012); SHOULD NOT cut-off (INV-013). OK. |
| 004–008 | Levels and conditions match (INV-014 to INV-017, INV-108; OUT-008 at MAY). OK. |
| 009 | Time course with markers in the view; weekly values where relevant (INV-034 to INV-036, INV-001). OK. |
| 010–013 | Intensity on a stated scale, compared between periods; duration with label and the Caveat as SHOULD NOT; symptoms and the most bothersome symptom across periods and per attack; aura at MAY. OK. |
| 014–016 | Total, classes and drugs; weekly view; indicator with code, level, span and basis, prompt at MUST, diagnosis at MUST NOT. OK. |
| 017 | Follow-up view with window, year and worsening label. OK. |
| 018 | Comparison, changes, time points (18 rules), Caveat at MUST NOT. OK. |
| 019 | Residual burden next to percentage changes (INV-060, INV-061). OK. |
| 020 | Label, criterion, values, decidable components, not sole indicator, no continuation decision; acute summaries per medication tied by `summarisesMedication` (v15). OK. |
| 021 | MUST/SHOULD split; acute effectiveness per medication and period (v15 formulation tie). OK. |
| 022 | Post-stop view with on-treatment and baseline periods. OK. |
| 023 | All named outcomes, timing, formulation, baseline/on-treatment split, 15 minutes, Caveat; `summarisesMedication` admits both readings and excludes the R15-01 examples. OK. |
| 024 | History with dates, dose changes, duration, response (course span, formulation), adverse effects, stop reason, adherence over an evaluation window (v15). OK. |
| 025 | MAY scheme windows. OK. |
| 039 | Adherence next to the comparison over a window that contains an on-treatment period and ends with it (`adherenceFor`, v15), in the history and the clinician summary. OK. |
| 026, 027 | Instrument results with value sets and change; functional impact with baseline comparison. OK. |
| 028–030 | Three-month view; per-type outputs; menstrual-relation view. OK. |
| 031 | Bouts, remissions, rates, 15-minute effectiveness per medication of the covered period. OK. |
| 032, 033 | Trigger view with caveats and dates in its period; screening results next to headache outputs. OK. |
| 034 | All components, with v15 formulation and adherence-window ties. OK. |
| 035 | Overview components; preventive treatment effect tied to a course that overlaps the covered period (v15). **R16-01**: the acute alternative is tied only to a medication used at some time up to the as-of date, so it can show the effect of a medication not taken in the covered period; the acute part of the antecedent is history-wide. |
| 036–038 | Paediatric outputs; composite index; caveats. OK. |

### Mechanical checks (scripts, on v15)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), with no gaps and no duplicates. Every E- and INV- reference resolves. Issues ISS-01 to ISS-06 and ISS-08 to ISS-11; ISS-07 is referenced only as withdrawn (section 9). S references lie in S-001–S-046 or S-101–S-106, and S-101 to S-106 each have a row. Every OUT reference exists in Stage 1 (39 requirements). |
| Realises and Conformance | Exactly one of each in every element and invariant. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025). For every OUT, the row's element and invariant sets equal the sets derived from the Realises fields. All rows say "full". |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Scopes: output 77, repertoire 32, context 1. All 10 MUST NOT / SHOULD NOT predicates begin with `¬`. These match the v15 change log. |
| Attribute levels | 172 level-annotated declarations (core 94, MUST 29, SHOULD 47, MAY 2), as stated. The typing rule holds: every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. |
| Names in `omn` blocks | No duplicate declaration. Every attribute selection names a declared attribute or component. The only name without an `omn` declaration is `refs`, which section 2.5 defines. |
| v15 changes (by hand) | Well typed: `summarisesMedication(s : AcuteTreatmentSummary, m : AcuteMedication)`, `adherenceFor(a : AdherenceSummary, rc : ResponseComparison)` and `courseOverlaps(c, t, p : Period)` are applied to arguments of those types (`v.covers : →Period` matches `Period`, section 2.10). `e.kind is stop` is defined (section 2.6). Precedence in INV-105 (`A ∨ B ⇒ C ∨ ∃ s, m • …`, closed by the outer parenthesis), INV-104 and INV-109 is as the Readings state. No new partial term. |

### Scope sweep

- A grep for enter-/entry, record-, input, captur-, logged, stor-, persist-, database, JSON/XML/CSV/FHIR/HL7, serializ-, encod-, retention, reminder, answer, data field, algorithm and "obtained from" returns only:
  - the scope statements of sections 1, 2.1, 2.7 and 3.5;
  - the "obtained from diary information; how is out of scope" notes of E-014 and E-019;
  - the S-014 HALT-30 recall quote ("records days affected");
  - the E-057 notes that scoring from answers is out of scope;
  - the INV-076 note.
- The v15 relations take only output elements, constants and subject properties as arguments: summaries, medications, response comparisons, adherence windows, course events and covered periods.
- Every threshold, reference level, score band and offset that is part of the output data is present with its quote. No missing threshold or formula was found.

## Remarks

### R16-01 Coverage gap: the acute alternative of the overview's treatment effect (INV-105) admits a medication that was not taken in the covered period, and the acute part of the antecedent is history-wide, so the overview can show the effect of no treatment the patient follows in that period

- Item(s):
  - INV-105 (the treatment-effect conjunct: its antecedent and its acute alternative; Reading and Notes);
  - E-067 Notes;
  - E-051 Conformance (the INV-105 clause);
  - section 7, row OUT-035.
- Problem:
  - v15 ties the response-comparison alternative of INV-105 to "a preventive treatment taken during the covered period" (`courseOverlaps`). It also restricts the preventive part of the antecedent to such treatments, "so that the conjunct is required exactly where a treatment effect of the covered period can be shown".
  - The acute alternative is tied only to "an acute medication the subject has used" (`∃ m ∈ ctx.subject.acuteMedications • summarisesMedication(s, m)`). The acute part of the antecedent is `ctx.subject.acuteMedications ≠ ∅`.
  - By E-008, `acuteMedications` holds every acute medication the subject has used up to the as-of date, and "a medication stays in the set after its use has stopped". So:
    - **(i) Gap.** The overview can meet the conjunct with a 0-attack summary of a medication last taken years before the covered period. It then shows the effect neither of the acute medication actually taken in the period nor of the preventive treatment taken in it. Under "one item suffices", the acute alternative alone discharges the conjunct.
    - **(ii) Broadening.** A subject who has taken no treatment at all during the covered period, but used an acute medication at some earlier time, is still asked for a treatment effect of that period. The only way to meet it is a 0-attack summary of a medication no longer used. For preventive treatments v15 removes exactly this case.
  - The model's own text states the intended reading, and the predicate does not realise it for the acute alternative:
    - E-067 Notes: "The treatment effect is that of the treatment the patient follows during the covered period (INV-105)";
    - INV-105 Notes: "so that the effect the patient follows is that of the period the overview shows, not of an earlier one", and "The comparison of a treatment stopped before the covered period shows the effect of an earlier treatment, not of the treatment the patient follows in that period, and does not stand in for it".
  - **Relation to earlier fixes.** Fix 15 ("Other changes", item 1) closed only the case of "a drug the subject has never used". Its stated basis is OUT-035 "so that patients can follow the effect of their treatment", but it did not consider that `acuteMedications` includes medications no longer used (E-008). This remark tightens the same tie in the same direction. It keeps:
    - the fix-11 decision that one treatment-effect item suffices;
    - the v14 period tie (`within`);
    - the v15 `summarisesMedication` and `courseOverlaps`.
  - **Watch points.** The remark touches no E-008 component (watch point 6), no co-presence item (watch point 3), no responder-label item (watch point 2) and not the INV-105 menstruation conjunct (watch point 4).
- Evidence:
  - **INV-105 (v15):** `((∃ t ∈ ctx.subject.preventiveTreatments • courseOverlaps(ctx, t, v.covers)) ∨ ctx.subject.acuteMedications ≠ ∅ ⇒ (∃ rc ∈ v.content ∩ ResponseComparison • courseOverlaps(ctx, rc.treatment, v.covers)) ∨ ∃ s ∈ v.content ∩ AcuteTreatmentSummary; m ∈ ctx.subject.acuteMedications • s.typeScope = allTypes ∧ summarisesMedication(s, m) ∧ within(s.period, v.covers))`.
  - **E-008:** `acuteMedications : set AcuteMedication -- every acute medication (drug and formulation) the subject has used at any time up to the as-of date; a medication stays in the set after its use has stopped`.
  - **INV-105 Notes (v15):** "a subject whose preventive treatments have all stopped before the covered period, and who has used no acute medication, is not asked for a treatment effect of that period", and "An acute-treatment summary that shows the treatment effect is one of an acute medication the subject has used [...] not of a drug or formulation the subject has never used."
  - **Example admitted by v15.**
    - Setting:
      - as-of date 20 October 2026; audience `adultPatient`; time range 1 August – 30 September 2026, calendar months; the subject has migraine and does not menstruate;
      - acute treatment courses: ibuprofen from 10 January 2018, stopped (discontinued) 31 December 2018; sumatriptan (oral) from 10 January 2025, ongoing;
      - `acuteMedications = {(ibuprofen, oral), (sumatriptan, oral)}`, which satisfies the INV-001 link in both directions;
      - preventive treatment: erenumab from 15 March 2026, ongoing.
    - The patient-facing overview covers 1 August – 30 September 2026. It shows:
      - headache days, migraine days, intensity (with scale) and total acute-medication days for the covered period and for August and September (for example 6 and 5 acute-medication days, all with sumatriptan);
      - as its only treatment-effect item, an ibuprofen summary: all formulations, `formulations = {oral}`, all types, period = the covered period, 2 hours, 0 treated attacks, eleven outcome summaries of 0 attacks assessed, no lines;
      - completeness, labels and caveats.
    - These all hold: INV-105 (through `summarisesMedication(s, (ibuprofen, oral))` and `within`), INV-003, INV-011, INV-072, INV-073, INV-074, INV-095 and INV-099.
    - The overview shows no effect of erenumab, the preventive treatment the patient takes throughout the covered period, and no effect of sumatriptan, the only acute medication taken in it.
  - **Example of (ii).** The same subject in 2019, with no treatment in 2019, has an overview of 2019. It must show a treatment effect, which only a 0-attack summary of ibuprofen, last taken in 2018, can provide.
  - **Stage 1 OUT-035:** "an understandable overview of their own headache pattern over time (… treatment effect …) … so that patients can follow the effect of their treatment and prepare consultations". Its quote [S-027]: "Bovendien kunnen de patiënten het effect van acute en eventueel preventieve behandeling zelf monitoren in het e-dagboek" (Stage 1 translation: "patients can themselves monitor the effect of acute and possibly preventive treatment in the e-diary").
- Required change: tie the acute alternative, and the acute part of the antecedent, to the acute treatment taken during the covered period, as v15 did for the preventive part. Keep one item, the `within` period tie and `summarisesMedication`. Align the INV-105 Reading and Notes, the E-067 Notes, the INV-105 clause of E-051 Conformance and row OUT-035.
  - **(a) Preferred: through the subject's acute treatment courses (E-008, unchanged).**
    - Require the summary's medication to be that of an acute treatment course taken during the covered period: `∃ t ∈ ctx.subject.acuteTreatments • drugOf(t) = m.drug ∧ courseOverlaps(ctx, t, v.covers)`.
    - Replace `ctx.subject.acuteMedications ≠ ∅` in the antecedent by `∃ t ∈ ctx.subject.acuteTreatments • courseOverlaps(ctx, t, v.covers)`.
    - An acute course may have no stated start (E-055 and INV-109 Notes). If such courses should count, use a variant of `courseOverlaps` that treats a course without a stated start as started, and only excludes a course stopped before the first day of the period. The fixer chooses.
    - Satisfiability: by INV-001, the drug of every acute course is the drug of an acute medication. So wherever the acute part of the antecedent holds, an all-formulations summary of that drug for the covered period can be shown, with 0 treated attacks where none was treated (INV-072, INV-074). Where no preventive or acute course overlaps the covered period, nothing is required.
  - **(b) Alternative: through output elements of the overview.**
    - Tie the summary's drug to the acute-medication days that the overview shows for the covered period. The summary is of a drug whose per-drug acute-medication days of the covered period, shown in the overview, are above 0.
    - Restrict the acute part of the antecedent to an overview whose total acute-medication days of the covered period are above 0, and require the per-drug days of the covered period in the overview, so that INV-024 makes some drug's count positive.
    - Every argument is an output element or a context property, so the relation is in scope.

## Checked and not raised

- **The v15 changes (R15-01 to R15-03).**
  - `summarisesMedication` excludes both R15-01 examples and admits both readings of OUT-023.
  - `adherenceFor` excludes the R15-02 one-day window.
  - `courseOverlaps` excludes the R15-03 example.
  - All three are well typed and satisfiable with the invariants that constrain the same items (fix-15 satisfiability pass re-checked on the examples above).
  - The E-051 Notes rightly treat the per-drug versus per-formulation question as one of the model's representation, not a Stage 1 defect: OUT-023 itself asks for both presentations.
- **Which on-treatment period the adherence window covers (INV-066).** `adherenceFor` lets the window end with any on-treatment period of the comparison. For a comparison of months 1–3, the adherence of month 1 alone meets it.
  - Stage 1 does not define "the evaluation window" (OUT-039). Every on-treatment period of a comparison is compared with the baseline (INV-056).
  - Fix 15 decided, with a stated reason, that one window suffices (E-047 Notes). I have no new evidence. Not raised.
- **The periods of the overview's response comparison (INV-105).** A comparison of an ongoing treatment started years ago may show only its early months. Review 15 (R15-03) stated that "The comparison's own periods are not required to lie in the covered period", and fix 15 adopted this. The identifying-property table of fix 15 also records the comparison's periods as "not fixed by Stage 1" (INV-104). I have no new evidence. Not raised.
- **Periods of the treatment review view (INV-068).** The baseline and on-treatment periods are tied to the start but not to a monthly kind. OUT-021 does not fix them ("for the same pre-treatment baseline and on-treatment periods"), and reviews 02, 03 and 10–13 and fix 15 judged INV-068 complete. Not raised.
- **Caregiver lost productive days bounded by the period length (INV-033).** Lost productive time added up over two caregivers could exceed the period length. Such a figure can be shown as `otherCaregiverImpact`, and OUT-036 fixes no form, so no permitted output is excluded. Not raised.
- **ISS-02 wording.** "Simple analgesics" occurs in ICHD-3 only on p. 139, in the comments to 10.1.1 High-altitude headache ("Most cases of 10.1.1 High-altitude headache respond to simple analgesics"). The next sentence deals with acute mountain sickness. ISS-02 calls the passage "on acute mountain sickness, section 10". That is loose but not wrong in substance, and the issue itself is founded. Not raised.
- **[S-035] translation "application intervals may be extended"** for "uygulama süreleri uzatılabilir". It fits the context and supports no element (Verification coverage). Not raised.
- **Settled questions, not reopened (no new evidence):**
  - INV-060 with INV-061 for compared periods shorter than 28 days (fix 02, item 14);
  - a response comparison right after the treatment start (review 03);
  - the monthly baseline;
  - INV-023 at any granularity;
  - the "> 3 months" readings of INV-045 and INV-089;
  - the MIDAS labels and the HIT-6 recall;
  - the "baseline administration";
  - R10b-01 and R11-01 (a)/(b) (watch point 3);
  - INV-091 to INV-093;
  - "treatment effect" by one item;
  - the E-041 timings, ages and `excludes` values (watch point 1);
  - INV-087 and the lead-in (watch point 4);
  - INV-049 and INV-050 (watch point 5);
  - the E-008 time frames (watch point 6);
  - the period of a cluster attack rate within its bout;
  - several stop events in one course.
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded. I re-verified:
  - 8.2.6 criterion B (p. 124);
  - "simple analgesics" only on p. 139;
  - NICE 1.3.9 and 1.3.39 without a review time point;
  - 1.3.48 and the CG150 population;
  - the [S-034] flowchart (p. 52).

  No Stage 1 issue is silently worked around. R16-01 concerns the model, not Stage 1.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and no item of v15 carries a FROZEN marker.
