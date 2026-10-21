# Review — iteration 05
VERDICT: REMARKS
REMARK_COUNT: 3
Reviewed version: v04
Date: 2026-10-21

## Summary

v04 fixes the four remarks of iteration 04 correctly:

- the lead-in gives every covered period a menstrual-relation view without a false date, and keeps every R03-02 and R03-03 guarantee;
- `nextWindowDays` distinguishes days −2 and −1 of the next menstruation for migraine days as well as attacks;
- INV-108 applies the OUT-001 MUST to moderate/severe headache days and attacks wherever they are provided;
- INV-031 relates the IHS 2025 count to migraine days only under the definition that count rests on.

The citation base is sound:

- all 63 Stage 2 quotes were found verbatim at their stated locations and URLs;
- the metadata of S-101 to S-105 is correct;
- ICHD-3 (2018) and NICE CG150 (last updated 3 June 2025) are still current, and no ICHD-4 has been published.

The mechanical checks are clean. The scope sweep found no input, storage or derivation-from-input content. Section 8 is founded, and no Stage 1 issue is silently worked around.

Three defects remain:

- **Patient-facing overview (R05-01).** INV-105 requires a series that tiles the covered period exactly. No correct overview of a period that is not a run of whole calendar months, 28-day periods or calendar weeks can meet it. An example is the period since the previous consultation, which a patient uses to "prepare consultations". The clinician-facing summary was fixed for the same case in iterations 02 and 03 (INV-104).
- **Score components of responder criteria (R05-02).** `scoreMet` and `scoreDecided` (E-046, used by INV-063) do not tie the instrument results they test to the label's treatment. A change between two pre-treatment administrations therefore forces a "responder" label, and pre-treatment results alone can force "non-responder".
- **Cluster attack rate (R05-03).** The computed rate (E-064) has no stated relation to the attack count and period length it is computed from, where these are shown in the same view. Model section 2.7 and PROCESS.md section 2 require that relation.

## Verification coverage

Downloads were made with `curl` into a fresh directory under `/tmp` (`/tmp/r05-dl-lrTs`), outside the repository. Scripts were kept in the session scratchpad and run with `python3 -I`.

- **Extraction.**
  - PDFs were extracted page by page with `pdftotext -raw` and `-layout`, and each quote was searched on its stated page.
  - Europe PMC full-text XML and the listed `pmc.ncbi.nlm.nih.gov` HTML pages were both tag-stripped and searched. Every PMC quote was found at both, so it can be read at the listed URL.
- **Quote passes.** Each quote was split at `[...]` and checked in three passes:
  1. exact, after collapsing whitespace;
  2. after normalising quotes, dashes and ligatures, and removing the ICHD-3 glyphs ≥ ± + > < (which have no text mapping);
  3. alphanumeric only.
- **Inspection.** Every pass-2 or pass-3 match was inspected in context. The only differences were:
  - line-end breaks ("non-/opioid", "there-/fore", "con-/sidered", "def-/inition", "fol-/lowing", "disab-/ling");
  - footnote markers ("opioids1", "medications1,2", "above,1");
  - the "ﬁ" ligature;
  - the unmapped ICHD-3 glyphs ("≥", "±", "−"; "+3" rendered "þ3");
  - in S-008, "a≥30%" and "a ≥50%" printed without some spaces.

### Citations

| Source | Where checked | Quotes checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|---|
| S-001 ICHD-3 (Stage 1 URL; HTTP 200, 211 pages; PDF page = printed page) | pp. 8, 9, 12, 122–125, 190, 209 | 30:<br>• 15 code labels;<br>• 8.2, 8.2.1, 8.2.2 and 8.2.3 Descriptions;<br>• 8.2.4, 8.2.5, 8.2.6 and 8.2.8 criterion B;<br>• 8.2.6 note 2;<br>• the 8.2.3 comment, short (E-028) and full (INV-046);<br>• A1.1.1 and A1.1.2 criterion B, and A1.1.1 note 2;<br>• cluster remission | 30 | 0 | 0 |
| S-008 IHS 2024 (Stage 1 URL, univaq PDF; HTTP 200) | pp. 12, 13 | 4:<br>• the Q6 30 % alternative;<br>• the AHS MIDAS/HIT-6 definition;<br>• the PGIC wording and the 50 % item of `critIhsQ6` | 4 | 0 | 0 |
| S-010 IHS 2025 (Stage 1 URL, univaq PDF; HTTP 200) | p. 6 | 7:<br>• the four control levels;<br>• the "In some cases" sentence;<br>• the definition-adoption sentence and the "proxy" sentence (E-018) | 7 | 0 | 0 |
| S-014 (Stage 1 source) | Europe PMC XML of PMC6734476 and the listed PMC page (HTTP 200) | 12:<br>• HALT-90 and HALT-30 recall;<br>• the "whole days" unit;<br>• Table 18: title, 3 headings, 4 rows;<br>• the HURT sentence (ISS-06) | 12 | 0 | 0 |
| S-101 Yang 2011 | Europe PMC XML and the listed PMC page (HTTP 200); section "Methods" > "Data sources" | 2 | 2 | 0 | 0 |
| S-102 Pavlović 2015 | Europe PMC XML and the listed PMC page (HTTP 200); "Headache impact on functioning" > "Migraine-related disability" | 2 | 2 | 0 | 0 |
| S-103 PedMIDAS page | listed URL, HTTP 200; title "PedMIDAS Tool \| Headache Center"; heading "PedMIDAS Tool for Assessing Migraine Disability"; footer "© 2026 Cincinnati Children's Hospital Medical Center" | 1 (lead sentence, section heading, 2 column headings, 4 rows) | 1 | 0 | 0 |
| S-104 Snaith 2003 | Europe PMC XML and the listed PMC page (HTTP 200); section "Construction of the Hospital Anxiety And Depression Scale (HADS)" | 1 | 1 | 0 | 0 |
| S-105 PHQ/GAD-7 instructions | listed PDF, HTTP 200, 9 pages; metadata author Kurt Kroenke, created 2010-06-22, modified 2014-04-16 | 4:<br>• PHQ-9 and GAD-7 ranges and section heading (P. 6/9);<br>• developers sentence (P. 8/9) | 4 | 0 | 0 |
| **Total** | | **63** | **63** | **0** | **0** |

- **Metadata** (PubMed esummary), all correct:
  - S-101: Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMID 20819842, PMC3057423, 4 authors as cited.
  - S-102: J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMID 25902814, PMC4406925, 7 authors as cited.
  - S-104: Health Qual Life Outcomes 2003;1:29, DOI 10.1186/1477-7525-1-29, PMID 12914662, PMC183845.
  - S-103 developer paper: Neurology 2001;57(11):2034–9, DOI 10.1212/wnl.57.11.2034, PMID 11739822.
- **Fragments of Stage 1 quotes.**
  - 366 double-quoted strings in sections 1–8 were compared by script with Stage 1 v18.
  - Every string that cites a Stage 1 quote is a verbatim substring of it, apart from capitalisation at the start of a fragment or nested quotation marks. Examples are the [S-015], [S-016], [S-018], [S-011], [S-008], [S-028] and [S-033] fragments of E-041, and the [S-015], [S-023] and [S-033] thresholds of E-045.
  - The other strings are the Stage 2 quotes above, or the model's own names and labels.
  - Also verified on ICHD-3 p. 190: "in at least two out of three menstrual cycles" (E-060 Notes). On p. 209: the cluster-period wording (E-063 Meaning).
- **Newer versions.**
  - Web search and the IHS classification pages show only "ICHD-4 – Work in Progress 1" (2024) and a September 2025 workshop report (posted January 2026). No published ICHD-4 exists.
  - The NICE CG150 recommendations page (Stage 1 URL, HTTP 200) shows "Last updated: 03 June 2025". Recommendations 1.3.27, 1.3.28, 1.3.29 and 1.3.48 read as modelled.
- **Translations.** v04 has no new non-English quote. The Dutch and Russian fragments in E-041 and E-045 are parts of Stage 1 quotes, whose translations carry over.
- **Value sets re-checked against the downloaded texts**, all matching:
  - ICHD-3 labels and hierarchy; 8.2 levels (15 for 8.2.3, 10 otherwise) and the "> 3 months" span; `classesOf826`; the A1.1 window; the remission duration;
  - HIT-6 range and bands; MIDAS, PedMIDAS and HALT-90 bands and labels; recall periods;
  - HADS, PHQ-9 and GAD-7 ranges;
  - the IHS Q6 thresholds (including the MIDAS ranges "11–20" and "≥20", which overlap at 20 as printed); the NICE, DMKG and Russian thresholds; the IHS 2025 control levels.

### Per-OUT fidelity check (Statement, Caveats, strength, traceability row)

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK (INV-108 verified) | 021 | OK |
| 002 | OK | 022 | OK (ISS-03) |
| 003 | OK (SHOULD / SHOULD NOT) | 023 | OK |
| 004 | OK | 024 | OK |
| 005 | OK | 025 | OK (MAY) |
| 006 | OK (INV-031 after R04-03 verified) | 039 | OK |
| 007 | OK | 026 | OK (ISS-06) |
| 008 | OK (MAY; ISS-04) | 027 | OK |
| 009 | OK | 028 | OK (ISS-03) |
| 010 | OK | 029 | OK (ISS-09) |
| 011 | OK | 030 | OK (lead-in and `nextWindowDays` verified, see below) |
| 012 | OK | 031 | **R05-03**; otherwise OK |
| 013 | OK (MAY) | 032 | OK |
| 014 | OK | 033 | OK |
| 015 | OK | 034 | OK |
| 016 | OK (ISS-01, ISS-09) | 035 | **R05-01**; otherwise OK |
| 017 | OK | 036 | OK |
| 018 | OK | 037 | OK |
| 019 | OK (ISS-05) | 038 | OK |
| 020 | **R05-02**; otherwise OK (ISS-08) | | |

Conformance levels were compared with the Stage 1 strength of the statement part each realises, for all 108 invariants and the attribute levels of every element:

- MUST 19: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054–057, 059, 068, 086, 102, 108;
- MUST NOT 2: INV-048, 106;
- SHOULD NOT 8: INV-013, 021, 043, 065, 084, 091, 101, 107;
- SHOULD 47;
- definitional 32.

No mismatch was found. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`.

### Mechanical checks (scripts in the session scratchpad)

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108); none missing, no duplicates. INV-108 is placed after INV-017 by topic, as fix-iter-04 states. |
| Dangling references | none<br>ISS headings: ISS-01–06, 08, 09; ISS-07 appears only in sections 8 (note), 9 and 12<br>S references are within S-001–S-046 or S-101–S-105; OUT references are within 001–039 |
| Realises fields and traceability | every element and invariant has exactly one Realises field<br>39 rows, in Stage 1 order (OUT-039 after OUT-025)<br>0 differences between the rows and the union of the Realises fields<br>no row text names an E-/INV- ID outside its columns<br>39 × "full" (but see R05-01 to R05-03) |
| Names in `omn` blocks | 304 declared names, none declared twice<br>199 enumeration constants and variant tags, no duplicates<br>after removing declared names, attributes, tags, parameters and bound variables, nothing unresolved apart from the `let`-bound `A` and `D` and the semantic constants of section 3.2 |
| Typing rule for levels | 172 attribute declarations; no SHOULD, MAY or MUST-with-`when` attribute lacks an `opt`/`set`/`seq` type, and none uses `set1`/`seq1` |
| Partial terms in v04 changes (by hand) | `min cl.menstruationDays` guarded by `≠ ∅`<br>`max {…}` on two dates<br>`DateSpan` `where` clauses hold<br>`first`/`last` only on `seq1`<br>`opt` attributes used only inside quantifiers |
| Scope sweep (enter, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, entry, reminder, field, obtained, calculated, computed, algorithm) | only the exclusion statements (sections 1, 2.1, 2.7, 3.5), the out-of-scope notes of E-014, E-018, E-057 and INV-076, the omission notes of the [S-101] and [S-104] quotes, the [S-014] HALT-30 recall quote, "answered" in the INV-014 Reading, and "Conformance field" |
| Thresholds, formulas, derived attributes | Every relation takes output elements, context properties (section 3.5) or cited constants. Every threshold and formula of a named standard or instrument that the output shows is present.<br>One computed field lacks its relation (R05-03), and one relation is not correct under the named criterion (R05-02). |
| Satisfiability | No contradiction found in:<br>• INV-086 + INV-087 + INV-105 + INV-003 with lead-ins: the menarche example; a covered period with no day 1; a complete last line extending beyond the covered period whose next day 1 is at covers.end + 2, admitted with `nextWindowDays`;<br>• INV-108 + INV-014 to INV-017 + INV-028 + INV-001;<br>• INV-031 + INV-062 + INV-064;<br>• INV-044 + INV-045 + INV-046 + INV-104 + INV-003 + INV-011.<br>R05-01 is a case where a SHOULD cannot be met by any correct output of a Stage-1-permitted kind. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v04.md`: identical; working tree clean before this review |

## Remarks

### R05-01 Formal defect: INV-105 can be met only by a patient-facing overview whose covered period is a run of whole calendar months, 28-day periods or calendar weeks
- Item(s): INV-105 (the series conjunct `tiles(sr, spanOf(v.covers), sr.granularity)`), E-067; section 7 row OUT-035
- Problem:
  - **What INV-105 requires.** It applies (SHOULD) to every `PatientOverview`. It requires a series that tiles the covered period exactly: `first(sr.periods).start = v.covers.start ∧ last(sr.periods).end = v.covers.end`, with all periods of the series granularity (INV-002, INV-004).
  - **What follows.** A covered period that is not a run of whole calendar months, of 28-day periods or of calendar weeks has no such series. So every overview of such a period violates INV-105, however correct its content.
    - Example: the period since the previous consultation, 10 March to 21 April (43 days). 43 is not a multiple of 7 or 28, and the span is not a run of whole months.
    - The same holds for a rolling "last 30 days", and for any period shorter than a week.
  - **Stage 1 permits these overviews.**
    - OUT-035 names no period. It gives as purpose "so that patients can follow the effect of their treatment and prepare consultations", and the natural period for preparing a consultation is the one since the previous consultation.
    - So a fully conformant diary (model section 3.2) could not offer them. INV-105 excludes outputs that Stage 1 permits (PROCESS.md section 9, formal defect).
    - INV-095 requires only an overview of the selected time range, which is tileable by INV-001. So there is no contradiction between invariants, only this exclusion.
  - **The model already treats the same case correctly elsewhere.** For the clinician-facing summary, iterations 02 and 03 (R02-02 (a), R03-04) replaced the same kind of requirement by `containsPeriodOf` and `fillsPeriod`. INV-104 Notes: "The period since the previous consultation may be shorter than a week, or contain no whole calendar week [...]; such a period has no time course of its own, so a series [...] is required only when the covered period contains at least one whole period".
  - **Not a reversal of an earlier fix** (oscillation watch point 2).
    - The series conjunct of INV-105 is unchanged since v00, and no earlier remark concerned it. R02-07, R03-03 and R04-01 concerned the overview's cycle line, which this remark does not touch.
    - R03-04 and fix-iter-03 cited INV-105 as an example of a series tied to its covered period. The required change keeps that tie: `fillsPeriod` still excludes a one-period series of a long covered period, the R03-04 defect. Those remarks and fixes did not consider covered periods that are not whole periods.
- Evidence:
  - INV-105: `∀ v : PatientOverview • plainLanguage ∈ v.qualities ∧ (∃ sr ∈ v.content ∩ Series • tiles(sr, spanOf(v.covers), sr.granularity) ∧ perPeriod(v, sr, HeadacheDays, allTypes) ∧ …)`, Conformance SHOULD.
  - E-006: `pred tiles(sr : Series, r : DateSpan, g : Granularity) ≙ sr.granularity = g ∧ first(sr.periods).start = r.from ∧ last(sr.periods).end = r.to`.
  - E-005 / INV-002: `ofKind` makes every series period a whole calendar month, 28 days or a calendar week.
  - Stage 1 OUT-035 Statement: "The diary output SHOULD give the patient an understandable overview of their own headache pattern over time (headache and migraine days, intensity, acute medication use, treatment effect and, where relevant, the relationship to menstruation), in plain language, so that patients can follow the effect of their treatment and prepare consultations."
  - INV-104 (predicate and Notes, quoted above); E-006 `containsPeriodOf`, `fillsPeriod`.
- Required change: make INV-105 satisfiable by a correct overview of any covered period. Options:
  - (a) **The INV-104 pattern.**
    - Where the covered period contains a whole period of some granularity (`containsPeriodOf`), require a series of that granularity with `fillsPeriod(sr, v.covers)` and the four measures for every period of it.
    - In every case, require headache days, migraine days, intensity and acute-medication days for the covered period itself, so that a short overview still shows them.
  - (b) **A condition.** Keep the tiling series only for covered periods that consist of whole periods of some granularity. Require the covered-period values otherwise.

  Update the INV-105 Reading and Notes, the E-067 Notes and the OUT-035 row.

### R05-02 Formal defect: the score components of a responder criterion are tested on any instrument results, not on results before and under the label's treatment, so INV-063 can force a label that contradicts the named criterion
- Item(s): E-046 (`scoreMet`, `scoreDecided`, Notes), INV-063 (Reading), INV-062; E-045 (`critIhsQ6`, `critDmkg`); section 7 row OUT-020
- Problem:
  - **The relation.**
    - `scoreMet(L, s)` holds when some instrument result `r` in `L.otherValues`, with its baseline result `b`, shows a decrease of at least the threshold from a baseline score in the stated range.
    - `scoreDecided(L, s)` holds when some such pair has both total scores.
    - Neither relates `r` or `b` to the label's treatment. Nothing requires `b` to precede the treatment start, `r` to follow it, or `r` to relate to the evaluated period(s).
    - INV-063 (definitional) then forces `responder` when any component is met. It forces `nonResponder` when every component is decided and none is met.
  - **Why this is wrong.**
    - The score components are criteria of response to the preventive treatment. Under IHS Q6 they are success criteria that "determine whether preventive therapy is effective", with a reduction measured from the "baseline score". Under DMKG/ÖKSG/SKG, prophylaxis is judged effective if the impairment "sinkt" (falls) by the threshold.
    - The reduction components are tied correctly: `reductionMet` requires `ch.reference.period = rc.baseline`, the pre-treatment baseline (INV-056), and `ch.compared.period ∈ ran L.evaluated`. The score components have no such tie.
    - PROCESS.md section 2: "A relation must be correct under the definitions the output names".
  - **Example 1: "responder" is forced.**
    - Treatment T starts on 1 April. MIDAS results are available for 5 January (18), 30 March (12) and 1 July (14).
    - A label under "IHS global practice recommendations Q6" refers to June, with migraine days down 20 %.
    - The output shows the pre-treatment MIDAS of 30 March, the baseline score the criterion refers to. By E-058 (`baselineResult` SHOULD when an earlier result exists) and INV-082, that result has 5 January as its baseline result.
    - Then `scoreMet` holds for the component "≥ 5 points for baseline score 11–20": y = 18, y − x = 6.
    - So INV-063 forces "responder", although MIDAS rose from 12 to 14 under T. A "non-responder" label, the reader's reading of the values under T, is excluded.
  - **Example 2: "non-responder" is forced.**
    - An episodic-migraine subject; a label under "DMKG/ÖKSG/SKG consensus statement (episodic migraine)", whose three components are all decidable.
    - Migraine days fall by 40 %, and HIT-6 falls under T from 63 (25 March, before the start) to 56 (1 July), that is by 7 points, which meets the criterion.
    - INV-062 is satisfied by showing any HIT-6 and MIDAS result: `∃ r ∈ L.otherValues ∩ InstrumentResult • r.instrument = ins`. If the output shows only pre-treatment results with their own earlier baselines (no decrease), every component is decided and none is met.
    - INV-063 then forces "non-responder", which the criterion contradicts. The label depends on which results the output happens to show.
  - **In scope.** The required tie uses only output elements: completion dates, the response comparison's `treatmentStart`, and `L.evaluated`.
- Evidence:
  - E-046: `pred scoreMet(L, s) ≙ conditionHolds(…) ∧ ∃ r ∈ L.otherValues ∩ InstrumentResult; b ∈ r.baselineResult; x ∈ r.totalScore; y ∈ b.totalScore • r.instrument = s.instrument ∧ (∀ lo ∈ s.baselineAtLeast • y ≥ lo) ∧ …` and `pred scoreDecided(L, s) ≙ ¬ conditionHolds(…) ∨ ∃ r ∈ L.otherValues ∩ InstrumentResult; b ∈ r.baselineResult • r.instrument = s.instrument ∧ r.totalScore ≠ ∅ ∧ b.totalScore ≠ ∅`.
  - Compare `reductionMet`: `∃ rc ∈ L.comparison; ch ∈ rc.changes • ch.reference.period = rc.baseline ∧ ch.compared.period ∈ ran L.evaluated ∧ …`.
  - E-058: `baselineResult : opt →InstrumentResult SHOULD when ∃ d ∈ self.completionDate • ∃ a ∈ ctx.subject.instrumentAdministrations • a.instrument = self.instrument ∧ a.date < d`. INV-082: the baseline result is any earlier result of the same instrument.
  - [S-008] "The success criteria that determine whether preventive therapy is effective and should be continued [...] are any one or more of the following:" (Q6, Optimal, p. 12; Stage 1 OUT-020). [S-008] "The clinically meaningful improvement in MIDAS score is defined by the AHS as i) reduction of ≥5 points for baseline score 11–20 or ii) reduction of ≥30% for baseline score ≥20." (Q6, Evidence, p. 13; quoted in E-045; verified on the Stage 1 URL).
  - [S-023] "Bei der episodischen Migräne (eM) wird eine Prophylaxe als wirksam beurteilt, wenn [...] die migränebedingte Alltagseinschränkung gemessen mit dem Headache Impact Test (HIT-6) um mindestens 5 Punkte oder dem Migraine Disability Assessment Score (MIDAS) um mindestens 30 % sinkt" (Stage 1 OUT-020; translation there: "prophylaxis is judged effective if [...] falls by at least 5 points [...]").
  - PROCESS.md section 2 (quoted above).
- Required change: make the score relations correct under the named criteria. Options:
  - (a) **Tie the results to the treatment** in `scoreMet` and `scoreDecided`.
    - Use only a pair of results in which the baseline result `b` was completed on or before the treatment start of the label's response comparison: `∃ rc ∈ L.comparison; db ∈ b.completionDate • db ≤ rc.treatmentStart`.
    - The result `r` must be completed after that start and relate to the evaluated period(s): for example its completion date lies in, or at the end of, a period of `L.evaluated`. The exact tie to `L.evaluated` is the author's choice, but a pair of pre-treatment results must never decide a component.
    - A pair without these dates does not decide the component.
  - (b) **Treat score components as undecided.** If the author holds that the shown values cannot fix which administrations a criterion compares, then score components are not decided by the values shown, like judgement components. Remove them from `componentMet` and `componentDecided` and state why.

  Update the E-046 Notes, the INV-063 Reading and the OUT-020 row.

### R05-03 Coverage gap: the computed cluster attack rate has no relation to the attack count and period length it rests on
- Item(s): E-064 (`rate`, Notes), INV-089; section 7 row OUT-031
- Problem:
  - **The rate is a computed field.** `ClusterAttackRate.rate : ℚ derived core` is "the number of cluster headache attacks per day or per week" during a period within a bout. It is a computed field of the output: attacks over the period divided by its length in days (per day), or seven times that (per week).
  - **No relation is stated.** The model states only `r.rate ≥ 0` and that the rate's period lies within its bout (INV-089, E-064 Notes).
  - **Consequence.** A view that shows, for the same period and type scope, an attack count (`AttackCount`, E-019) and a rate may show values that contradict each other: for example 10 attacks in a 7-day period next to "3.0 attacks per day". The period length is always shown with the rate (INV-003, E-005).
  - **The model's own rule requires it.** Section 2.7: "Where all arguments of its relation are output elements, the relation is an invariant of section 6 and is listed under 'Relations' in the element's Notes."
  - **It also departs from the model's practice** for every other computed proportion or rate shown with its arguments:
    - INV-012, the completeness proportion against covered days and period length;
    - INV-053, the percentage change against the absolute change and baseline;
    - INV-074, the outcome proportion against the attack counts.
  - **PROCESS.md section 2** names "a proportion of days" and "a per-period average" among the computed fields whose relation to the other output elements must be in the model.
- Evidence:
  - E-064: `element ClusterAttackRate extends PeriodValue { basis : RateBasis core; rate : ℚ derived core -- unit: attacks per day or attacks per week; bout : →ClusterPeriodItem core }`; Notes: "Relations: INV-089 (the rate's period lies within its bout; the rate is not negative)."
  - INV-089, last conjunct: `∀ r : ClusterAttackRate • r.rate ≥ 0 ∧ (∀ s ∈ r.bout.start • s ≤ r.period.start) ∧ (∀ e ∈ lastDay(r.bout) • r.period.end ≤ e)`.
  - Stage 1 OUT-031 Statement: "attacks per day and per week during active periods".
  - PROCESS.md section 2: "Computed (derived) fields that an output shows are output data and must be in the model. [...] give its relation to the other output elements it depends on, where that relation is part of the output data as defined above."
- Required change:
  - **Definitional relation** (in INV-089 or a new invariant): for a rate `r` and an attack count `e` shown in the same view for the same period and type scope:
    - `r.basis = perDay ⇒ r.rate ≈ e.count ÷ r.period.lengthDays`;
    - `r.basis = perWeek ⇒ r.rate ≈ 7 × e.count ÷ r.period.lengthDays`.
  - **Optionally**, state that a per-day and a per-week rate of the same period and scope rest on one whole number of attacks, for example `∃ n : ℕ • rate_day ≈ n ÷ lengthDays ∧ rate_week ≈ 7 × n ÷ lengthDays`.
  - **Text.** Update the E-064 Notes and the OUT-031 row.

## Checked and not raised

- **Lead-in (R04-01 fix, oscillation watch point 1).**
  - Verified:
    - only the first line can be a lead-in;
    - it begins on the first covered day;
    - it ends before every day 1 the output shows;
    - it is never counted;
    - G7, G8 and the `∃₁` attachment of attack marks hold.
  - The E-060 Meaning sentence "A lead-in is shown when no first day of menstruation [...] is known from the summarised diary information" reads as a statement of what a lead-in asserts, like the meaning of a day count. It is not a procedure over input, so it is not raised as a scope violation. Raising it would also be a third change at the watch point without new evidence.
- **`nextWindowDays` (R04-04 fix).**
  - The formula gives days −2 and −1 of the next menstruation, cut at the line's first day.
  - When the next menstruation begins two days after the covered period, a complete last line may extend beyond the covered period (`v.covers.end ≤ last(v.cycles).cycle.to`), so day −2 is still shown as a window day.
  - A line marked as not ended although it has ended is a false statement, which no predicate can exclude.
- **INV-108 (R04-02 fix).** The level and per-measure `∃ g` are correct, and nothing interacts with INV-028, INV-037 or INV-057.
- **INV-031 and E-018 (R04-03 fix).** `labelledAs` is well-typed. The remaining relations hold under every published definition the output can name.
- **INV-104** (watch point 3): unchanged and not touched by any remark here.
- **HADS subscales only (INV-085).** [S-104] states that "the two subscales, anxiety and depression, were independent measures", and OUT-033 asks only for "score". The model's exclusion of a HADS total follows the developer.
- **HALT-30 lower bound.**
  - The E-057 Notes say that the lower bound 0 "follows from their lowest band", although HALT-30 has no bands.
  - The value 0 is correct for a count in "whole days per one or 3 months" ([S-014]). This is an imprecise justification, not a wrong value.
- **Time points as period ends.**
  - `atTimePoint` makes an on-treatment period end on `shift(anchor, offset)`. For example, a period ends on 26 March for "after 12 weeks" from 1 January.
  - Stage 1 fixes no day convention, and INV-055 remains satisfiable with 28-day periods. Not raised.
- **Further bound `treatedAttacks ≤ AttackCount`.** Not stated, but it is a bound, not the defining relation of a computed field, and no Stage 1 property depends on it. Not raised.
- **Notation.**
  - The bounded form `∃₁ x ∈ S` is used (INV-087) but listed in section 2.6 only as `∃₁ x : T`. Its meaning is unambiguous, and earlier reviews accepted it.
  - The section 4 diagram's "TreatmentHistoryView ⊃ ClassGroup" is explanatory text. Formally the groups are references.
- **Search languages.** The Stage 2 searches concern instrument value sets published by English-language developers. The search log covers German, French, Italian and Spanish and states why other languages were not needed.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the AAN/AHS 14A and NVN window readings;
  - INV-023 at any granularity;
  - the "> 3 months" reading of INV-045;
  - the MIDAS label choice;
  - the 24-hour outcomes for cluster summaries;
  - "history of previous bouts";
  - the OUT-031 end-of-bout Caveat as a reading instruction (fix-iter-01);
  - the context as subject properties, including `ihsQ6ChronicAlternative`;
  - the HIT-6 one-month recall;
  - the cluster remission "> 3 months";
  - labels under a criterion that does not apply.
- **Section 8.**
  - ISS-01 to ISS-06, ISS-08 and ISS-09 are founded, and each is pointed to from the elements it affects.
  - ISS-02 was re-verified: the only "simple analgesics" in ICHD-3 is on p. 139 (10.1.1).
  - The ISS-04 extension (the reading of "Frequency outputs") is founded.
  - R05-01 to R05-03 are defects of the model, not Stage 1 issues.
  - No Stage 1 issue is silently worked around.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and the oscillation check after iteration 04 froze nothing.
