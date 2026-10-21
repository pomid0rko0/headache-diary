# Review — iteration 11
VERDICT: REMARKS
REMARK_COUNT: 3
Reviewed version: v10
Date: 2026-10-21

## Summary

This is the main review of iteration 11. It is an independent review of v10. `OUTPUT_MODEL.md` is byte-identical to `history/v10.md`.

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 after OUT-025) and section 5;
- v10, every element, every invariant, and sections 7 to 12;
- the oscillation check after iteration 08 and its eight watch points;
- review 10, re-check 10b and fix 10;
- the "checked and not raised" lists of reviews 03, 09 and 10.

**Earlier decisions.** FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. No fixer has declined a remark in iterations 01–10. I checked every remark below against the earlier loop files.

**Sources.** I downloaded every source myself and checked every quote by script, and by hand where the text layer is unusable.

**Result.**
- **Citations, value sets, scope sweep and section 8.** All clean. All 370 source-quote fragments are verbatim at their stated locations. Every threshold, band, range, recall period, code label and evaluation offset agrees with its source. No input, storage or derivation-from-input content was found.
- **Three remarks.** None reverses an earlier fix or changes a value at an oscillation watch point (details in each remark).
  - **R11-01 (coverage gap / formal defect).** Some items have parts that Stage 1 requires to be shown with the item, but the model never places those parts in the item's view. This affects:
    - the values and changes of a response comparison (OUT-018, MUST);
    - the values of a period comparison (OUT-001, MUST; OUT-010);
    - the treatment markers of a time-course view (OUT-009);
    - the outcome summaries of an acute-treatment summary (OUT-021, OUT-023).

    In the model a reference creates no part (section 2.5), and the model states co-presence explicitly wherever it needs it. For these four cases it does not. As a result, a MUST-conformant diary may show a response comparison in one view and its migraine-day and headache-day values and changes only in another view.
  - **R11-02 (coverage gap).** A responder label whose criterion rests on the effectiveness of acute treatment needs only **one** acute-treatment summary, for **one** drug in **one** evaluated month. A three-month "optimal control" label of a patient who uses two acute drugs can therefore show one drug for one month. OUT-020 asks for "those values as well", and INV-069 asks for every drug and period.
  - **R11-03 (infidelity, narrowing).** OUT-034 asks for the clinician-facing summary "for the period since the previous consultation (or a period chosen by the clinician)". The model reads the chosen period as the selected time range, which INV-001 restricts to runs of whole calendar months, 28-day periods or calendar weeks. So a summary of a chosen period such as 15 August to 20 October 2026 (67 days) is never required.

## Verification coverage

### Method

- **Downloads.** Every source was downloaded with `curl` into the fresh directory `/tmp/r11-dl`, outside the repository. Every download returned HTTP 200; S-034 needed a retry after a connection reset. The downloads were:
  - the Stage 1 URLs of S-001, S-002, S-005, S-007, S-008, S-010, S-015 (Recommendations and Overview pages), S-016, S-018, S-028, S-030, S-033, S-034 and S-035;
  - the Europe PMC full-text XML of S-011, S-014, S-023, S-042, S-101, S-102 and S-104;
  - the S-103 page, the S-105 PDF, and the S-106 pages (overview, section 1 "Guidance" and section 2 "The technology").
- **Extraction.**
  - PDFs were extracted page by page with `pdftotext -raw` and `-layout`.
  - HTML and XML had their scripts and markup removed and entities unescaped.
  - ICHD-3 p. 190 and the S-034 title page were rendered with `pdftoppm` and read as images.
- **Scripts.** All are in the session scratchpad (`r11/`) and were run with `python3 -I`: `quotes.py`, `where.py`, `mech.py`, `names.py`, `comp.py` and `html2txt.py`.
- **Quote search.** I took every double-quoted string outside the `omn` blocks on a line that carries an `[S-NNN]` tag, and split it at `[...]`. That gave 440 fragments. Each fragment was searched in every source tagged on its line, in three passes:
  1. whitespace, quotes and dashes normalised;
  2. also line-end hyphens and unmapped glyphs (`≥`, `±`, `+`, `−`) removed;
  3. letters and digits only.

  `where.py` then listed every page on which each key quote occurs, and I compared that page with the stated location.

### Citations

| Source (URL as listed; HTTP) | Fragments checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 (ichd-3.org PDF; 200; 211 pp.) | 61 | 61: 58 by script, and 3 by hand on rendered p. 190, where the text layer lacks "±", "−" and "+".<br>Code labels on pp. 8, 9 and 12.<br>8.2–8.2.8 on pp. 122–125.<br>The 8.2.3 comment on p. 123.<br>The remission duration on p. 209.<br>"simple analgesics" only on p. 139. | 0 | 0 |
| S-002, S-005, S-042 (Stage 1 quotes and terms reused) | 9 | 9 | 0 | 0 |
| S-007 (UCL manuscript; 200; 39 pp.) | 8 | 8 (pp. 10, 22 and 25) | 0 | 0 |
| S-008 IHS 2024 (univaq PDF; 200; 31 pp.) | 26 | 26.<br>Q2 on p. 9: both "effectiveness*" sentences and the footnote. They also appear in the summary on p. 5.<br>Q6 on p. 12, Q6 Evidence on p. 13, the Q13 heading on p. 17. | 0 | 0 |
| S-010 IHS 2025 (univaq PDF; 200; 11 pp.) | 36 | 36 (p. 6: the four control levels, "requires a clear definition of migraine day", "as a proxy of migraine days") | 0 | 0 |
| S-011 EHF 2022 (Europe PMC XML; 200) | 8 | 8 | 0 | 0 |
| S-014 (Europe PMC XML; 200) | 35 | 35 (HALT-90 and HALT-30 recall; "whole days per one or 3 months"; Table 18 with "≥20"; HURT; "Grading is not used by HALT-30") | 0 | 0 |
| S-015 NICE CG150 (200; "Last updated: 03 June 2025") | 37 | 37: 35 by script, and 2 by hand (two fragments of 1.3.28 and 1.3.29 that the script had attributed to another tag on the same line) | 0 | 0 |
| S-016 SIGN 155 (200; 64 pp.) | 9 | 9 (section 1.2.1 on PDF p. 7; section 4.1 on PDF p. 20) | 0 | 0 |
| S-018 AAN/AHS Clinician Summary (200; 12 pp.) | 15 | 15 (p. 1; 14A and 14B on p. 7; 14H on p. 8) | 0 | 0 |
| S-023, S-028, S-030 (200) | 25 | 25 | 0 | 0 |
| S-033 Russian adult (200; 92 pp.) | 25 | 25 (p. 1 title; p. 4 "М – мигрень"; pp. 39, 40, 41 and 53) | 0 | 0 |
| S-034 Russian paediatric (200 after one retry; 53 pp.) | 13 | 13: 11 by script, and 2 by hand on the rendered title page ("Возрастная группа" "дети"). The flowchart is on p. 52, section 2 on p. 17. | 0 | 0 |
| S-035 Turkish protocol (200; 92 pp.) | 28 | 28 (Kutu 8 on p. 48; 3.6.3.9 on p. 57; 3.3 b on p. 23; the heading of section 6 on p. 77) | 0 | 0 |
| S-101 HIT-6 (Europe PMC XML; 200) | 5 | 5 | 0 | 0 |
| S-102 MIDAS (Europe PMC XML; 200) | 8 | 8 | 0 | 0 |
| S-103 PedMIDAS page (200; "© 2026") | 12 | 12 (0 to 10, 11 to 30, 31 to 50, "Greater than 50", with their labels) | 0 | 0 |
| S-104 HADS (Europe PMC XML; 200) | 2 | 2 | 0 | 0 |
| S-105 PHQ/GAD-7 manual (200; 9 pp.) | 4 | 4 (P.6/9 under "USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES"; the developers sentence on P.8/9) | 0 | 0 |
| S-106 NICE TA260 (200) | 4 | 4: §2.1, the dates, and the §1 fragment of the search log ("less than a 30% reduction in headache days per month after 2 treatment cycles") from a separate download of section 1 | 0 | 0 |
| **Total** | **370** | **370** (362 by script, 8 by hand or by a separate download) | **0** | **0** |

**The other 70 tagged strings are not source quotes.**
- 15 are English translations. All are faithful: the Russian, Turkish and Dutch translations of E-041 and E-045, and the S-034 flowchart in ISS-10.
- 39 are Stage 1 text, requirement names, or a Stage 1 module title, reused by reference.
- 16 are PubMed or web query strings and search-log labels.

**Metadata.**
- PubMed esummary confirms S-101 (PMID 20819842), S-102 (25902814), S-104 (12914662) and the S-103 developer paper (11739822): journal, year, volume, pages, authors, DOI and PMCID all match section 10.
- S-106: "Published 27 June 2012", "Last reviewed: 11 January 2016".
- S-015: "Last updated 03 June 2025".

**Newer versions.** A web search found no published ICHD-4, only "Work in Progress 1" (2024) and committee activity in 2025. No newer version that changes an element was found.

### Per-OUT fidelity check

For each requirement I compared every Statement part and every constraining Caveat with the items that realise it, the strength of each part with the item's level, and the traceability row.

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK, except that the side-by-side presentation of a period comparison is not required (R11-01 (b)) | 021 | INV-068 MUST and INV-102 OK. The acute-treatment effectiveness "in the same view" is incomplete (R11-01 (d)) |
| 002 | OK (INV-008) | 022 | OK (INV-070, INV-103; ISS-03) |
| 003 | OK (INV-011, INV-012, INV-013 SHOULD NOT) | 023 | OK for content (INV-071 to INV-075, INV-107). See R11-01 (d) |
| 004 | OK (INV-014, INV-009) | 024 | OK (INV-077 to INV-079) |
| 005 | OK (INV-015; label SHOULD) | 025 | OK (MAY; INV-080) |
| 006 | OK (INV-016, INV-108) | 039 | OK (INV-066, INV-067, E-055, INV-104) |
| 007 | OK (E-019, INV-010, INV-017, INV-108) | 026 | OK (INV-081, INV-082, INV-100; ISS-06) |
| 008 | OK (MAY) | 027 | OK (INV-026, INV-027) |
| 009 | Series and content OK. The markers are not required in the time-course view (R11-01 (c)) | 028 | OK (INV-040 to INV-043) |
| 010 | OK, except as in OUT-001 for intensity comparisons (R11-01 (b)) | 029 | OK (INV-028 to INV-030; ISS-09) |
| 011 | OK (INV-019 to INV-021) | 030 | OK (INV-086, INV-087) |
| 012 | OK (INV-022, INV-072, INV-076) | 031 | OK (INV-088, INV-089) |
| 013 | OK (MAY, E-027) | 032 | OK (MAY; INV-090) |
| 014 | OK (INV-023, INV-024; ISS-02) | 033 | OK (INV-083 to INV-085) |
| 015 | OK (INV-025) | 034 | Content OK (INV-104). The chosen period is narrowed (R11-03) |
| 016 | OK (INV-044 to INV-048; ISS-01) | 035 | OK (INV-095, INV-105; ISS-03). The comparison values in the overview fall under R11-01 (a) |
| 017 | OK (INV-049 to INV-052; ISS-11) | 036 | OK (INV-055, INV-096 to INV-098; ISS-10) |
| 018 | Content, time points and levels OK (INV-053 to INV-059, INV-106). The values and changes are not required with the comparison (R11-01 (a)) | 037 | OK (INV-091 to INV-093) |
| 019 | OK (INV-060, INV-061; ISS-05) | 038 | OK (INV-099 to INV-101) |
| 020 | Criteria, thresholds, ties and prohibitions OK (INV-062 to INV-065). The acute-treatment values are incomplete (R11-02). The underlying values with the label are affected by R11-01 (a) | | |

### Mechanical checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108). None missing, none duplicated. |
| References | No dangling E- or INV- reference.<br>S references lie in S-001–S-046 and S-101–S-106, and every S-1NN has a row in section 10.<br>OUT references lie in 001–039.<br>ISS headings are 01–06 and 08–11; ISS-07 appears only as withdrawn. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025).<br>Exactly one Realises field per item.<br>Each row equals the union of the Realises fields.<br>No coverage text names an ID outside its row. All rows say "full"; see R11-01 to R11-03. |
| `omn` names | No name declared twice.<br>Every attribute selection `e.a` names a declared attribute or component.<br>The remaining identifiers are bound variables, parameters, `refs` (section 2.5) and words inside text literals. |
| Composition | Only `Output.views` and `View.content` hold element atoms without `→` (`comp.py`). So every other element-typed attribute is a reference, which places nothing in the holder's view (basis of R11-01). |
| Levels | Invariants: MUST 19, MUST NOT 2, SHOULD 47, SHOULD NOT 8, definitional 32, as the change log states. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v10.md`: identical. |
| Scope sweep | Searched sections 1–8 for: enter, entry, record, input, captur, logged, store, stora, persist, database, JSON, XML, CSV, FHIR, HL7, serializ, encod, retention, answer, reminder, algorithm, obtained, calculat, comput, field, "diary data", "diary information", questionnaire.<br>Every hit was read in context. The hits are exclusion statements, out-of-scope notes, Stage 1 wording, verbatim quotes, or an instrument name.<br>No input entity, storage term or derivation from input. Every relation and threshold takes output elements or context properties only. |
| Thresholds and formulas that are part of the output data | All present and quoted, against [S-001] or the stated source:<br>• the 8.2 levels (10/15) and span;<br>• the A1.1 window;<br>• the remission duration;<br>• the instrument ranges, bands and recalls;<br>• the six named criteria and the IHS 2025 control levels;<br>• the 17 evaluation offsets;<br>• the percentage change, the covered-day proportion, the outcome proportion, the cluster rates, the change from the baseline instrument result and the treatment duration. |

## Remarks

### R11-01 Coverage gap / formal defect: the parts of a comparison, a time course and an acute-treatment summary are never placed in the view of the item they belong to
- Item(s):
  - (a) E-043 and INV-056, with the consequences for INV-054, INV-062 and INV-105;
  - (b) E-037, INV-037, INV-038 and INV-039;
  - (c) E-034, E-035 and INV-035;
  - (d) E-051, E-052, INV-072 and INV-074, with the consequences for INV-069, INV-071 and INV-104;
  - section 7 rows OUT-001, OUT-009, OUT-010, OUT-018, OUT-020, OUT-021, OUT-023, OUT-034 and OUT-035.
- Problem:
  - **The model's semantics.**
    - Section 2.5 says that only `Output.views` and `View.content` are composition attributes, that "every `Item` atom is part of exactly one `View` atom", and that "References create no parts". Rule W1 only puts referenced atoms in the same output.
    - I confirmed by script that no other attribute holds element atoms without `→`.
    - So an item's reference attributes never place the referenced items in the item's view.
  - **The model states co-presence explicitly wherever it needs it.** Examples:
    - INV-003 (periods: "every period that the view or one of its items refers to … is shown … in the same view");
    - INV-054 (`ch.reference ∈ viewOf(ch).content`);
    - INV-059 (time points: `tp ∈ viewOf(rc).content`);
    - INV-060 and INV-062 (`rc ∈ viewOf(L).content`, `x ∈ viewOf(L).content`);
    - INV-066 (adherence in `viewOf(rc)`);
    - INV-087 (`a ∈ viewOf(cl).content` for the attacks of a cycle line);
    - INV-092 (`m ∈ viewOf(x).content` for the components of a composite index);
    - INV-035 itself (`v.series ∈ v.content`);
    - INV-104 (`∃ mk ∈ v.content ∩ TreatmentMarker`).

    Review 03 also relied on this reading for treatment-history groups ("references and may be shown in another view of the same output").
  - **Four places lack it, although Stage 1 requires the parts to be shown with the item.**
    - **(a) Response comparison (OUT-018, MUST).**
      - INV-056 requires `rc.values` and `rc.changes` to exist with the right periods and measures, but not in `viewOf(rc)`.
      - INV-054 ties each change to its two values in the change's own view, not to the comparison.
      - **An output that passes every MUST and SHOULD invariant.** View A shows the response comparison for erenumab: its baseline and on-treatment periods (INV-003), its evaluation time points (INV-059), adherence (INV-066), functional impact (INV-027) and acute-treatment summaries (INV-071). View B shows the March and June migraine-day and headache-day counts with their changes (INV-054) and the residual burden (INV-060).
      - The comparison "at the evaluation time points" is then never shown with the values it compares.
      - A responder label in view A (INV-062: `rc ∈ viewOf(L).content`) is not shown with the "underlying values (OUT-018, OUT-019)" either. Its residual-burden items can sit in A while the day counts they reference sit in B.
      - INV-105 accepts the same hollow comparison as the overview's "treatment effect".
    - **(b) Period comparison (OUT-001, MUST; OUT-010).**
      - E-037 defines "A side-by-side comparison of values for two or more periods", and the INV-037 Reading says "the diary can show, side by side for exactly those periods …".
      - However, `pc.values` is a reference, and neither INV-037, INV-038 nor INV-039 places the values in `viewOf(pc)`. The predicates therefore do not state what the Meaning and Reading say.
    - **(c) Time-course markers (OUT-009).**
      - E-034 defines "A dated marker in a time-course view".
      - INV-035 requires `∃ mk ∈ v.markers`, a reference, so the markers may be shown in another view.
      - INV-104 requires the markers of the clinician-facing summary in `v.content`. INV-035 does not.
    - **(d) Acute-treatment effectiveness (OUT-021, OUT-023).**
      - The effectiveness of an acute-treatment summary is its outcome summaries (`outcomes : set →OutcomeSummary`), plus its per-attack lines (`sequence`).
      - INV-069 places the summary in the treatment review view, and so do INV-071 ("next to the response comparison") and INV-104. The INV-069 Reading says the view "shows … the effectiveness of each acute medication for the attacks treated in each period".
      - No invariant places the outcome summaries or the lines in the summary's view. The treatment review view may therefore show a summary that states only the drug, the period and the number of treated attacks.
  - **These are observable properties of the Statements.** The co-presence is part of what each Statement asks for:
    - a comparison that shows its values and changes (OUT-018);
    - a comparison of periods (OUT-001; the model's own "side by side");
    - a series "with dated markers" (OUT-009);
    - "the same view SHOULD also include … the effectiveness of acute treatment" (OUT-021).

    PROCESS section 2 lists "co-presence of elements in one view" among the presentation properties the model must represent. PROCESS section 9 lists a missing observable property as a coverage gap, and ambiguous semantics (here, a Meaning or Reading that the predicate does not state) as a formal defect.
- Evidence:
  - Stage 1:
    - OUT-018: "the diary output MUST compare monthly migraine days and monthly headache days […] in a pre-treatment baseline period with periods after treatment start, aligned to the treatment start date, showing both the values of each period and the absolute and percentage change from baseline. The output MUST allow this comparison at the evaluation time points named in current guidance";
    - OUT-001: "the output MUST allow comparison of periods of equal length";
    - OUT-009: "as a time series of consecutive reporting periods […], with dated markers for the start, dose change and stop of preventive treatments, so that onset of effect, the trajectory of response and spontaneous fluctuation can be seen";
    - OUT-021: "the same view SHOULD also include […] the effectiveness of acute treatment for the attacks treated in each of these periods (OUT-023)";
    - OUT-020: "SHOULD always show the underlying values (OUT-018, OUT-019)".
  - Model:
    - section 2.5 as quoted above;
    - E-043 Meaning: "showing the values of each period and the absolute and percentage change from baseline, with the guidance evaluation time points";
    - E-043 `values : set1 →DayCount MUST`, `changes : set1 →Change MUST`;
    - INV-056 predicate (no `viewOf`);
    - INV-054 Reading: "Every change that a response comparison shows is shown together with the two values it compares";
    - E-037 Meaning and INV-037 Reading ("side by side");
    - E-034 Meaning;
    - INV-035 `∃ mk ∈ v.markers`, against INV-104 `∃ mk ∈ v.content ∩ TreatmentMarker`;
    - INV-069 Reading;
    - E-046 comment `comparison : opt →ResponseComparison SHOULD -- the underlying values (OUT-018)`.
  - Earlier loop files: review 03, "Checked and not raised" ("Treatment-history groups. The groups and lines of a treatment-history view are references and may be shown in another view of the same output. OUT-024 requires no co-presence with other content."). OUT-018, OUT-001, OUT-009 and OUT-021, unlike OUT-024, do state the co-presence.
- Required change: state the co-presence, each at the level of the Stage 1 part it realises. Then update the Readings, the E-035, E-037, E-043 and E-051 Conformance and Notes, and the section 7 rows listed above.
  - **(a)** Add to INV-056 (MUST, OUT-018): `(∀ m ∈ rc.values • m ∈ viewOf(rc).content) ∧ (∀ ch ∈ rc.changes • ch ∈ viewOf(rc).content)`. Alternatively, make this a definitional conjunct of E-043, as INV-007 does for annotations.
    - INV-054 then places the compared values in the same view as well.
    - INV-062's `rc ∈ viewOf(L).content` then brings the underlying values to the label.
  - **(b)** Add `∀ m ∈ pc.values • m ∈ viewOf(pc).content` to INV-038 (definitional, the "side-by-side" of E-037). Alternatively, add it to INV-037 (MUST) and INV-039 (SHOULD).
  - **(c)** Add `∀ mk ∈ v.markers • mk ∈ v.content` to INV-035 (SHOULD), as INV-104 does.
  - **(d)** Add `(∀ os ∈ s.outcomes • os ∈ viewOf(s).content) ∧ (∀ l ∈ ran s.sequence • l ∈ viewOf(s).content)` to INV-072 (SHOULD, OUT-023) or to INV-074 (definitional). Alternatively, require the outcome summaries in the view in INV-069 (OUT-021), and likewise in INV-071 and INV-104.
  - **Satisfiability (to be confirmed by the fixer).**
    - Values that a view already shows for the same measure, period and scope are referenced, not repeated (INV-006).
    - Every response comparison, period comparison or summary atom belongs to one view, so each view that shows one also shows its parts. INV-003, INV-011, INV-060, INV-062 and INV-097 then hold in that view.
  - **Oscillation.**
    - None of INV-035, INV-037, INV-038, INV-039, INV-056, INV-072 or INV-074 is a watch point. INV-104 and INV-105 (watch point 7) need no change under the options above.
    - The remark does not reopen review 03's judgement on treatment-history groups (OUT-024), or the fix-10 decision that the basis of the medication-overuse indicator need not be in the indicator's view.
    - It does not touch the R10b-01 restriction of INV-054.

### R11-02 Coverage gap: the acute-treatment effectiveness on which a responder criterion rests is required for only one drug in only one evaluated period
- Item(s):
  - INV-062: the `acuteTreatmentEffectiveness` conjunct, and in the same class the `periodValuesOf` and `typeValuesOf` conjuncts for `acuteTreatmentSummaries`;
  - E-045 Meaning and Notes;
  - E-046 Conformance;
  - section 7 row OUT-020.
- Problem:
  - **The predicate.** `(u = acuteTreatmentEffectiveness ⇒ ∃ s ∈ L.otherValues ∩ AcuteTreatmentSummary • s.period ∈ ran L.evaluated)`. One summary, of any one drug, for any one evaluated period, meets it.
  - **What the prose says.** The prose states more than the predicate:
    - E-045 Meaning: "the effectiveness of acute treatment in the evaluated periods";
    - E-045 Notes: "`acuteTreatmentEffectiveness` asks for the effectiveness in the evaluated periods, which the optimal-control level of [S-010] uses";
    - INV-062 Reading: "the effectiveness of acute treatment in the evaluated periods, where the subject uses acute medication".
  - **Example.** A patient uses sumatriptan and ibuprofen. The output shows an IHS position statement 2025 "optimal control" label over three months; INV-064 requires `#L.evaluated ≥ 3`.
    - The criterion's acute part is "for three months, with a satisfactory response to acute treatment, defined as pain-freedom within two hours from the intake".
    - INV-062 is met by a single ibuprofen summary for the first month. The sumatriptan response, and both drugs in months 2 and 3, are never required.
    - Yet these are values on which the criterion rests (OUT-020: "those values as well").
  - **Inconsistent with the model's own treatment of the same values.**
    - For OUT-021, INV-069 requires a summary "for each acute medication [...] for the attacks treated in each of these periods": `∀ am ∈ ctx.subject.acuteMedications • ∃ s … s.drug = am.drug ∧ s.period = p`.
    - INV-071 does the same for the baseline and each on-treatment period.
    - OUT-023, which OUT-020 names for these values, is stated "For each acute medication".
  - **The same gap in the generic conjunct.** `periodValuesOf(acuteTreatmentSummaries)` asks for one value of the kind per period, which for acute-treatment summaries means one drug. This conjunct serves the criteria that rest on an improved response to acute treatment ([S-032], [S-035], [S-042]; E-045 Notes). The `typeValuesOf` conjunct has the same gap.
- Evidence:
  - Stage 1 OUT-020: "and, where the named criterion also rests on other values, those values as well (for example […] the effectiveness of acute treatment in OUT-023)".
  - Stage 1 OUT-023: "For each acute medication, the diary output SHOULD report, across the attacks treated with it, the outcome measures …".
  - Stage 1 OUT-021: "the effectiveness of acute treatment for the attacks treated in each of these periods (OUT-023)".
  - [S-010] "Optimal Control. This is defined as less than four days with migraine or moderate-to-severe headache per month for three months, with a satisfactory response to acute treatment, defined as pain-freedom within two hours from the intake." (p. 6; verified, quoted in E-046).
  - Model: INV-062 predicate and Reading, E-045 Meaning and Notes, INV-064 (`#L.evaluated ≥ 3` for optimal control), INV-069, INV-071.
- Required change (either option):
  - **(a)** For `u = acuteTreatmentEffectiveness`, require for every acute medication m of the subject and every evaluated period p a summary `s ∈ L.otherValues ∩ AcuteTreatmentSummary` with `s.drug = m.drug ∧ s.period = p`.
  - **(b)** Require one summary per acute medication over a period that spans the evaluated periods.
  - **Either way**, apply the same per-drug requirement to `periodValuesOf(acuteTreatmentSummaries)` and `typeValuesOf((acuteTreatmentSummaries, h))`, for the baseline and each evaluated period. Then align the E-045, E-046 and INV-062 prose and the OUT-020 row.
  - **Satisfiability.** A summary may have 0 treated attacks; INV-072, INV-073, INV-074 and INV-011 hold for it, as they do for INV-069.
  - **Oscillation (watch point 5).** The change only tightens a presence requirement:
    - it keeps `#L.evaluated = 1`, the `evaluationResult` / `pretreatmentBaseline` pair, `rc.treatment = L.treatment`, and the open `UnderlyingKind` and `PeriodValueKind`;
    - no relation decides a category on acute effectiveness (fix 09), so no category is forced or excluded;
    - the conjunct has been unchanged since v00, and no earlier remark or fix concerned it.

### R11-03 Infidelity (narrowing): the clinician-facing summary is required for "a period chosen by the clinician" only when that period is a run of whole calendar months, 28-day periods or calendar weeks
- Item(s): INV-094 (predicate and Reading); E-007 (Definition and Meaning); INV-001 (the time-range conjunct, as it bears on OUT-034); E-066 Meaning and Conformance; section 7 row OUT-034.
- Problem:
  - **How the model reads the chosen period.** The E-007 Meaning maps "a period chosen by the clinician (OUT-034)" to the selected time range. INV-094 then requires a clinician-facing summary with `sameSpan(v.covers, c.timeRange)`, besides the one for the period since the previous consultation.
  - **The restriction.** INV-001 admits only time ranges that consist of whole periods of the selected granularity (`∃ s : seq1 DateSpan • … ofKind(s(i).from, s(i).to, c.granularity) …`).
  - **Example.** A clinician chooses 15 August 2026 (a Saturday) to 20 October 2026 (a Tuesday), 67 days.
    - It is not a run of calendar months. 67 is not a multiple of 28 or of 7, so it is not a run of 28-day periods or of whole calendar weeks.
    - So no admissible context has this time range, and INV-094 requires no summary for it.
  - **What Stage 1 says.** OUT-034 places no condition on the chosen period. The model itself recognises that consultation-related periods "need not be a run of whole calendar months, 28-day periods or calendar weeks" (INV-105 Notes; INV-104 Notes). INV-104 is built to serve any covered period, through `containsPeriodOf` and `fillsPeriod`.
  - **Reading against predicate.** The INV-094 Reading ("available for the period chosen by the clinician") is broader than its predicate.
  - This narrows a SHOULD statement part of OUT-034 (PROCESS section 9).
- Evidence:
  - Stage 1 OUT-034: "The diary output SHOULD provide a concise clinician-facing summary for the period since the previous consultation (or a period chosen by the clinician) that brings together the outputs most used in consultations".
  - Model:
    - E-007 Meaning: "Stage 1 refers to these as the selected time range (OUT-004), a period chosen by the clinician (OUT-034), …";
    - INV-001 time-range conjunct;
    - INV-094 predicate and Reading;
    - INV-104 Notes: "The period since the previous consultation may be shorter than a week, or contain no whole calendar week";
    - INV-105 Notes: "which need not be a run of whole calendar months, 28-day periods or calendar weeks (for example 10 March to 21 April, 43 days)".
  - Earlier loop files: no review or fix discusses the chosen period of OUT-034 beyond quoting it (reviews 02 and 03).
- Required change (either option):
  - **(a)** Add to `OutputContext` an optional period chosen by the clinician (for example `chosenPeriod : opt DateSpan`, with `∀ r ∈ c.chosenPeriod • r.to ≤ c.asOf` in INV-001) that is not subject to the whole-period condition. Require in INV-094 a clinician-facing summary whose covered period has its dates.
  - **(b)** Quantify INV-094 over every span that ends on or before the as-of date (`∀ r : DateSpan • r.to ≤ c.asOf ⇒ ∃ o … sameSpan(v.covers, r)`).
  - **Either way**, align the E-007 Meaning, the E-066 Meaning and Conformance, the INV-094 Reading and the OUT-034 row.
  - **Satisfiability.** INV-104 already holds for any covered period (its Notes give the construction), and INV-003 and INV-011 hold with it.
  - **Oscillation.** E-007, INV-001 and INV-094 are not watch points. INV-104 (watch point 7) needs no change, and the INV-001 time-range condition for the other availability invariants stays as it is.

## Checked and not raised

- **v10 changes.**
  - E-040 `absolute` and `relative` are `opt … derived MUST when ofResponseComparison(self)`, which is well typed and follows the typing rule for levels.
  - INV-053 requires at least one form, and INV-060 and INV-062 read `relative` inside a quantifier.
  - The restricted INV-054 is MUST over the OUT-018 range only, with OUT-020 cited second.
  - I read every Reading, Meaning and Notes field that changed in v10 against its predicate. Apart from the prose cited in R11-01 and R11-02, which v10 did not introduce, they match.
- **Co-presence in other places, not raised.**
  - The cluster view's bouts, rates and acute summaries are references: OUT-031 asks for no co-presence.
  - The treatment-history groups and lines: review 03 settled these on OUT-024.
  - The basis of the medication-overuse indicator: fix 10 decided this, and OUT-016 asks for the indication with the levels and span, which E-032 shows.
  - The baseline result of an instrument result: the change from it is an attribute of the result.
- **HADS whole-scale score (INV-085).** INV-085 admits only the two subscales. [S-104] states that "the two subscales, anxiety and depression, were independent measures", so this follows the developer. Not raised.
- **DMKG/ÖKSG/SKG criterion for chronic migraine.** [S-023] also gives 50 % (in practice 30 %) for chronic migraine. Stage 1 quotes only the episodic sentence, the named criteria are examples, and a label may name any `ResponderCriterion`. Not a gap.
- **OUT-017 values for the review window itself.** INV-050 shows the window as a period, and the headache and acute-medication days of the covered period and its whole periods from the start of withdrawal. "Including the review window" is satisfied by that reading. INV-050 is watch point 4, and I have no evidence beyond the two earlier sweeps.
- **INV-060 for a percentage change after a stop.** "Per month that remain on treatment" is read on the compared period. This is a SHOULD and a reading of OUT-019's "Wherever". Not raised.
- **Values re-verified in the sources.**
  - ICHD-3:
    - the 8.2 Description and the 8.2.1–8.2.3 Descriptions (10/15 days per month, more than three months);
    - 8.2.4, 8.2.5, 8.2.6 and 8.2.8 criterion B, and 8.2.6 note 2;
    - the A1.1.1 and A1.1.2 window and "there is no day 0" (rendered p. 190);
    - "must exceed three months" (p. 209);
    - the code labels (pp. 8, 9, 12).
  - IHS 2024 Q6 thresholds, including the MIDAS ranges overlapping at 20.
  - The IHS 2025 control levels.
  - HIT-6: 36–78; ≤ 49, 50–55, 56–59, 60–78.
  - MIDAS: grades I–IV with 0–5, 6–10, 11–20 and ≥ 21; three-month recall.
  - PedMIDAS: 0–10, 11–30, 31–50, > 50.
  - HALT-90: Table 18, including "≥20". "Grading is not used by HALT-30".
  - HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
  - The 17 evaluation rules against their texts, and the six named criteria.
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded, and each is pointed to from the elements it affects. Re-verified:
  - 8.2.6 criterion B;
  - "simple analgesics" only on p. 139, in the comments on 10.1.1 High-altitude headache;
  - NICE 1.3.9 and 1.3.39 without a review time point;
  - 1.3.48 and the CG150 population;
  - the [S-034] flowchart on p. 52.

  No Stage 1 issue is silently worked around. R11-01 to R11-03 are defects of the model, not of Stage 1.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - INV-023 at any granularity;
  - the "> 3 months" readings of INV-045 and INV-089;
  - the window readings and `excludes` values of E-041 (watch points 1 and 8);
  - `ruleRuChildren` (watch point 3);
  - INV-091 to INV-093 with `concerns`;
  - labels under a criterion that does not apply;
  - "history of previous bouts";
  - the E-060 lead-in wording;
  - the HIT-6 recall;
  - the MIDAS label choice;
  - "baseline administration" as any earlier administration;
  - INV-060 with INV-061 for compared periods shorter than 28 days (fix 02, item 14);
  - a response comparison right after the treatment start (review 03).

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and no item of v10 carries a FROZEN marker.
