# Review — iteration 03
VERDICT: REMARKS
REMARK_COUNT: 7
Reviewed version: v02
Date: 2026-10-21

## Summary

v02 fixes the seven remarks of iteration 02 correctly, and its citation base is sound:

- every Stage 2 quote of S-001, S-008, S-010, S-014 and S-101 to S-105 was found verbatim at its stated location and URL;
- the metadata of the new sources is correct;
- ICHD-3 (2018) and NICE CG150 (last updated 3 June 2025) are still the current versions.

The mechanical checks are clean: IDs, references, the traceability table against the Realises fields, declared names, attribute selections, the typing rule for levels, and the level counts. The scope sweep found no input, storage or derivation-from-input content.

The remaining defects are in formal relations and in coverage:

- **Factual error.** INV-046 forces the ICHD-3 8.2.6 indicator ("multiple drug classes") to "level reached" for a patient who uses a single drug class (R03-01).
- **Menstrual-relation view (OUT-030).**
  - The view need not show the cycles of the period it covers, so the stated number of complete cycles can be wrong (R03-02).
  - INV-087 forces a wrong "outside the window" mark for attacks in the perimenstrual window of a menstruation that the view does not show as a cycle line (R03-03).
- **Coverage.**
  - The clinician-facing summary's time course, weekly view and overuse indicators are not tied to the period it covers, and can shrink to one period or vanish (R03-04).
  - The paediatric equal-length rule omits three kinds of comparison (R03-05).
  - The list of validated instruments is closed, although Stage 1 lists them as examples (R03-06).
- **Evidence.** One instrument value is asserted with no cited source (R03-07).
- **Section 8.** The entries are founded; no new Stage 1 issue was found.

## Verification coverage

Downloads were made with `curl` into a fresh directory under the session scratchpad (`.../scratchpad/r03/dl`), outside the repository. Scripts were kept in a separate directory (`.../r03/scripts`) and run with `python3 -I`.

- **Text extraction.** PDFs were extracted with `pdftotext`, in raw and `-layout` modes and page by page (`-f/-l`). XML and HTML were tag-stripped.
- **Quote passes.** Each quote was split at `[...]` and checked in three passes:
  1. exact, after collapsing whitespace;
  2. after normalising typographic quotes, dashes, ligatures and line-end hyphens, and removing the ICHD-3 glyphs "≥", "±" and "−", which have no text mapping;
  3. alphanumeric only.
- **Inspection of pass-2/3 matches.** Every such match was inspected in context. The only differences were:
  - the "ﬁ" ligature;
  - footnote markers ("opioids1");
  - line-end breaks ("nonopioid", "combinationanalgesic");
  - the unmapped ICHD-3 glyphs;
  - the S-010 running header "Cephalalgia 45(2)" inside the Insufficient Control sentence, which was checked in its two parts.

### Citations

| Source | Where checked | Quotes checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|---|
| S-001 ICHD-3 (Stage 1 URL; PDF page = printed page) | ichd-3.org PDF, 211 pages | 29:<br>• 15 code labels (pp. 8, 9, 12, also in `-layout` mode);<br>• the 8.2.3 comment;<br>• 8.2.6 criterion B and note 2;<br>• the 8.2, 8.2.1, 8.2.2 and 8.2.3 Descriptions;<br>• 8.2.4, 8.2.5 and 8.2.8 criterion B;<br>• A1.1.1 and A1.1.2 criterion B, and A1.1.1 note 2 (p. 190);<br>• cluster remission (p. 209).<br>Also the ISS-02 claim, by a page-by-page search: "simple analgesics" occurs only on p. 139 (10.1.1). | 29; ISS-02 claim confirmed | 0 | 0 |
| S-008 IHS 2024 prevention (Stage 1 URL) | univaq PDF, pp. 9, 12, 13 | 3 new: the Q6 30 % alternative (p. 12), the AHS MIDAS/HIT-6 definition (p. 13), the PGIC wording of `critIhsQ6` (p. 12). Also 2 Stage 1 fragments re-checked: Q2 (p. 9) and Q6 50 % (p. 12). | 3 (+2) | 0 | 0 |
| S-010 IHS position statement 2025 (Stage 1 URL) | univaq PDF, p. 6 | 5: the four control levels and the "In some cases" sentence | 5 | 0 | 0 |
| S-014 Lifting The Burden/EHF (Stage 1 source) | Europe PMC XML of PMC6734476; the PMC URL serves the same text (HTTP 200) | 5:<br>• HALT-90 and HALT-30 recall;<br>• the "whole days" unit;<br>• Table 18: heading, 3 columns, 4 rows, with "≥20" for grade IV;<br>• the HURT sentence (ISS-06) | 5 | 0 | 0 |
| S-101 Yang et al. 2011 | Europe PMC XML; PMC URL HTTP 200 with the text | 2 | 2 | 0 | 0 |
| S-102 Pavlović et al. 2015 | Europe PMC XML; PMC URL HTTP 200 with the text | 2 | 2 | 0 | 0 |
| S-103 Cincinnati Children's PedMIDAS page | listed URL, HTTP 200; title "PedMIDAS Tool \| Headache Center"; heading "PedMIDAS Tool for Assessing Migraine Disability"; footer "2026 Cincinnati Children's" | 1: lead sentence, 2 headings, 4 rows | 1 | 0 | 0 |
| S-104 Snaith 2003 | Europe PMC XML; PMC URL HTTP 200 with the text | 1 | 1 | 0 | 0 |
| S-105 PHQ/GAD-7 instructions (Joint Commission copy) | listed PDF, HTTP 200; PDF metadata author Kurt Kroenke, created 2010-06-22, modified 2014-04-16 | 3:<br>• PHQ-9 and GAD-7 ranges (P.6/9);<br>• the developers sentence (P.8/9) | 3 | 0 | 0 |
| **Total** | | **51** (+2 re-checked Stage 1 fragments) | **51** | **0** | **0** |

- **Metadata** (PubMed esummary), all correct:
  - S-101: Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMID 20819842, PMC3057423; authors as listed.
  - S-102: J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMID 25902814, PMC4406925; 7 authors as listed.
  - S-104: HQLO 2003;1:29, DOI 10.1186/1477-7525-1-29, PMID 12914662, PMC183845.
  - S-103 developer paper: Neurology 2001;57(11):2034–9, PMID 11739822, DOI 10.1212/wnl.57.11.2034.
- **Newer versions.**
  - A web search finds only "ICHD-4 – Work in Progress 1" (Cephalalgia 2024) and an IHS ICHD-IV workshop (September 2025). No published ICHD-4 exists.
  - The NICE CG150 recommendations page (Stage 1 URL, HTTP 200) still shows "Last updated: 03 June 2025". Recommendations 1.3.27, 1.3.28, 1.3.29 and 1.3.48 read as modelled in E-039, E-041 and E-045.
- **Other quoted fragments.** A script checked all 346 strings in double quotes outside the `omn` blocks:
  - 201 are exact substrings of Stage 1 v18, and 22 more differ only in case or in nested quote marks;
  - 65 occur in the downloaded sources;
  - the other 58 are search queries, model wording, or source quotes that match only after the ligature and glyph normalisation above.
- **Translations.** No new non-English quote. The S-023, S-028 and S-033 fragments are substrings of Stage 1 quotes, whose translations carry over.

### Per-OUT fidelity check (Statement, Caveats, strength, traceability row)

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK | 021 | OK (see R03-05 for children) |
| 002 | OK | 022 | OK (ISS-03); see R03-05 for children |
| 003 | OK (SHOULD / SHOULD NOT) | 023 | OK |
| 004 | OK | 024 | OK |
| 005 | OK | 025 | OK (MAY) |
| 006 | OK | 039 | OK |
| 007 | OK | 026 | **R03-06**, **R03-07** (ISS-06 founded) |
| 008 | OK (MAY) | 027 | OK |
| 009 | OK | 028 | OK (ISS-03) |
| 010 | OK | 029 | OK (ISS-09) |
| 011 | OK | 030 | **R03-02**, **R03-03** |
| 012 | OK | 031 | OK |
| 013 | OK (MAY) | 032 | OK |
| 014 | OK | 033 | OK |
| 015 | OK | 034 | **R03-04** |
| 016 | **R03-01** (MUST / MUST NOT levels OK; ISS-01, ISS-09) | 035 | OK (ISS-03); see R03-03 for attack marks in the overview |
| 017 | OK | 036 | **R03-05** |
| 018 | OK | 037 | OK |
| 019 | OK (ISS-05) | 038 | OK |
| 020 | OK (ISS-08) | | |

Conformance levels were compared with the Stage 1 strengths for all 107 invariants and for the attribute levels of every element:

- MUST 18: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054–057, 059, 068, 086, 102;
- MUST NOT 2: INV-048, 106;
- SHOULD NOT 8: INV-013, 021, 043, 065, 084, 091, 101, 107;
- SHOULD 47;
- definitional 32.

No level mismatch was found. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`.

### Mechanical checks (scripts in `.../scratchpad/r03/scripts`)

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 107 invariants (INV-001–INV-107); consecutive, no duplicates |
| Dangling references | none<br>ISS headings: ISS-01–06, 08, 09; ISS-07 appears only in sections 8 (note), 9 and 12<br>S references are within S-001–S-046 or S-101–S-105; OUT references are within 001–039 |
| Realises fields and traceability | every item has exactly one Realises field<br>39 rows, in Stage 1 order (OUT-039 after OUT-025)<br>0 differences between the rows and the union of the Realises fields<br>39 × "full" (but see R03-01 to R03-06) |
| ISS pointers | every ISS is pointed to from the elements it names:<br>• ISS-01: E-028/029/032;<br>• ISS-02: E-028;<br>• ISS-03: E-038/043/049/067, INV-105;<br>• ISS-04: E-020–022, E-066, INV-104;<br>• ISS-05: E-018/044;<br>• ISS-06: E-057/058;<br>• ISS-08: E-046;<br>• ISS-09: E-029/032/036, INV-028 |
| Names in `omn` blocks | 296 declared names, none declared twice<br>198 enumeration constants and variant tags, no duplicate<br>after removing declared names, attributes, tags and bound variables, only `refs` (defined in section 2.5) and `ℙ` (section 2.4) remain |
| Attribute selections `e.a` | every selected attribute is declared in an element or value type |
| Typing rule for levels | 170 attribute declarations; no SHOULD, MAY or MUST-with-`when` attribute lacks an `opt`/`set`/`seq` type, and none uses `set1`/`seq1` |
| Partial terms (by hand) | all guarded:<br>• `÷` in INV-012, 053, 074 and E-046;<br>• `days` in INV-037, 079, 089 and E-006;<br>• `first`/`last` only on `seq1` or guarded;<br>• `i.span(2)` guarded by `#i.span ≥ 2`;<br>• `max A` guarded by `A ≠ ∅`;<br>• `periodEndFrom` by INV-002/004;<br>• `classOf` by INV-001 |
| Scope sweep (enter, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, entry, reminder, field) | only the exclusion statements (sections 1, 2.7, 3.5), the out-of-scope Notes of E-057 and INV-076, the [S-014] HALT-30 recall quote (used for the recall value), "answered" in the INV-014 Reading, "Conformance field", and tool names |
| Thresholds, formulas, derived attributes | every relation takes output elements, context properties (section 3.5) or cited constants. Every threshold and formula of a named standard or instrument that the output shows is present, apart from the coverage gaps of R03-04 and R03-06. One relation is wrong against its source (R03-01). |
| Satisfiability | no contradiction found in:<br>• INV-055 + INV-056 + INV-059 + INV-097 + INV-001;<br>• INV-094 + INV-104;<br>• INV-039 + INV-097;<br>• INV-044 + INV-045 + INV-046 + INV-003;<br>• INV-086 + INV-087 + INV-105;<br>• INV-071 to INV-076;<br>• INV-077 + INV-079;<br>• INV-062 + INV-063 + INV-064.<br>Satisfiable but wrong against the source: INV-046 (R03-01) and INV-087 (R03-03). |
| Snapshot | `cmp OUTPUT_MODEL.md history/v02.md`: identical |

## Remarks

### R03-01 Factual error: INV-046 forces the ICHD-3 8.2.6 indicator ("multiple drug classes") to "level reached" when only one drug class is used
- Item(s): INV-046, E-032 (`status`, Notes), E-028 (`classesOf826`), section 7 row OUT-016
- Problem:
  - **What the second conjunct of INV-046 does.** It makes the combined-use indicator `levelReached` whenever both of these hold:
    - the basis (days with any medication of `classesOf826`) is at least 10 in every period of the span;
    - every class of 8.2.1–8.2.5 that the subject uses is shown as not reached.
  - **Why it misfires.** Nothing requires two or more classes to have been used. The non-opioid analgesic level is 15, while the 8.2.6 total is 10. So single-class use of non-opioid analgesics on 10–14 days a month satisfies the antecedent.
  - **Example.** A subject whose only acute medication is ibuprofen takes it on 12 days in each of four monthly periods.
    - The 8.2.3 class indicator is `levelNotReached` (12 < 15; INV-045).
    - The basis is exactly 12 in each period (INV-024: between the largest class value, 12, and the sum of the class values, 12).
    - INV-046 then forces the output to show "8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused — level reached".
    - The same happens for a subject who has several classes but used only non-opioid analgesics in the span.
  - **Why this is wrong.** ICHD-3 restricts 8.2.6 to the use of several classes, and states that cumulative use within the single non-opioid class is coded 8.2.3, not 8.2.6.
  - **Consequence.** A definitional invariant forces a value that contradicts the standard the indicator refers to. The OUT-016 MUST indicator then shows a combined-use level as reached that ICHD-3 does not describe. The iteration 01 and 02 reviews checked INV-046 against note 2 but not this single-class case.
- Evidence:
  - [S-001] "8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused" (classification list, p. 12; already quoted in E-009).
  - [S-001] "Regular intake of any combination of ergotamine, triptans, non-opioid analgesics and/or opioids [...] on a total of ≥10 days/month for >3 months without overuse of any single drug or drug class alone." (8.2.6, criterion B, p. 124; already quoted in E-028).
  - [S-001] "Patients who use multiple drugs for acute or symptomatic treatment of headache may do so in a manner that constitutes overuse even though no individual drug or class of drug is overused; such patients should be coded 8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused." (8.2, note 2, p. 122; Stage 1 OUT-016 quote).
  - [S-001] "For the purposes of ICHD-3, all non-opioid analgesics are regarded as a single class; therefore, a patient who uses more than one non-opioid analgesic cumulatively, but not any single drug, on 15 or more days/month is coded 8.2.3 Non-opioid analgesic-overuse headache (with the individual drugs specified in parenthesis) and not 8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused." (8.2.3, Comments, p. 123; the text layer breaks "non-opioid" at a line end). Only its first clause is quoted in E-028.
  - Model, INV-046: `((∀ j ∈ dom i.basis • i.basis(j).days ≥ i.referenceLevel) ∧ (∀ k ∈ classesOf821to825 • (∃ m ∈ ctx.subject.acuteMedications • classOf(m.drug) = k) ⇒ ∃ i₂ : MedicationOveruseIndicator • i₂.period = i.period ∧ i₂.scope = ofClassUse(k) ∧ i₂.status = levelNotReached) ⇒ i.status = levelReached)`.
- Required change:
  - Add to both directions of INV-046 the condition that the use rests on at least two of the classes of 8.2.6. This is a relation over shown output elements:
    - INV-044 puts the class indicators of the same period in the same view;
    - by INV-045 and INV-003, their per-class basis day counts are for the same span periods.
    - Possible form: `∃ k₁, k₂ ∈ classesOf826 • k₁ ≠ k₂ ∧` each has a shown `acuteMedicationDays(ofClass(k))` value greater than 0 for a period of the span (or in each period of the span, if the author reads "regular intake of any combination" that way, stating the reading).
  - With fewer than two such classes, the combined indicator is `levelNotReached`, or it is not required (adjust INV-044).
  - Quote the full 8.2.3 comment or 8.2 note 2 as evidence, and update the INV-046 Reading, the E-032 Notes and the OUT-016 traceability text.

### R03-02 Formal defect: the menstrual-relation view need not show the cycles of the period it covers, so "how many complete cycles the view covers" can be misstated
- Item(s): INV-086, INV-087, E-060 (`cycles`, `completeCycles`, Notes), section 7 row OUT-030
- Problem:
  - **What INV-087 requires of the cycles shown.** They must be consecutive, each must overlap the covered period, and only the last may be unfinished.
  - **What it does not require.** It does not require the cycles shown to include every cycle that overlaps the covered period. The first shown cycle may begin long after `v.covers.start`, and a complete last cycle may end long before `v.covers.end`.
  - **The count follows the choice.** `completeCycles` is defined over the cycles shown, so the stated number depends on which cycles the output chooses to show.
  - **Example.** INV-086 requires `v.covers` = January to June, and the view must state that period (OUT-001, INV-003). An admitted view shows only the March and April cycles, both complete, and states "2 complete cycles". About five complete cycles lie in the covered period, and the attacks and migraine days of January, February, May and June are not related to menstruation at all.
  - **Consequences.**
    - The model's own reading of the count (E-060 Notes: "cycles that have ended and lie wholly within the period the view covers") is not enforced.
    - The MUST "across consecutive cycles" can be met by a view of one cycle for any time range (`seq1`).
  - **Why this matters.** Stage 1 requires the count because sources differ on 2 or 3 cycles (OUT-030 Rationale), so a wrong count defeats the purpose of the requirement.
- Evidence:
  - OUT-030 Statement: "MUST be able to show migraine attacks and migraine days in relation to the days of menstruation across consecutive cycles, [...] and MUST state how many complete cycles the view covers."
  - OUT-030 Rationale: "The sources differ on the number of cycles (NICE: at least 2; ICHD-3 research criterion and Japan: 3), which is why the number of cycles covered must be visible."
  - INV-087, the only conjuncts on the view's cycles:
    - `ran v.cycles ⊆ v.content`;
    - `v.completeCycles = #{cl ∈ ran v.cycles | cl.complete ∧ v.covers.start ≤ cl.cycle.from ∧ cl.cycle.to ≤ v.covers.end}`;
    - consecutiveness;
    - `(∀ cl ∈ ran v.cycles • cl.cycle.from ≤ v.covers.end ∧ v.covers.start ≤ cl.cycle.to)`.
  - INV-086: `∃ v ∈ o.views ∩ MenstrualRelationView • sameSpan(v.covers, c.timeRange)`.
  - Compare `tiles` (E-006), which makes a time series span its time range.
- Required change: require the cycles of a menstrual-relation view to be the cycles that overlap its covered period, for example:
  - at the end: `v.covers.end ≤ last(v.cycles).cycle.to`. An unfinished last cycle meets this by definition, and a complete last cycle then ends on or after the end of the covered period;
  - at the start: `first(v.cycles).cycle.from ≤ v.covers.start`. Or, if the author holds that the first day of the cycle in progress at the start need not be shown, an explicit alternative with its reason, for example letting the view's covered period begin on the first day of its first cycle, with INV-086 adjusted.

  Update the INV-087 Reading, the E-060 Notes and the OUT-030 traceability text.

### R03-03 Formal defect: INV-087 forces an attack in the perimenstrual window of a menstruation that the view does not show to be marked as outside the window
- Item(s): INV-087 (in-window conjunct, MRV conjuncts), E-061 (`inPerimenstrualWindow`), E-060 (`complete`, `cycle`), INV-105, section 7 rows OUT-030 and OUT-035
- Problem:
  - **The relation.** INV-087 defines `a.inPerimenstrualWindow ⇔ ∃ cl ∈ viewOf(a).content ∩ CycleLine • inSpan(a.onset, cl.perimenstrualWindow)`. A mark is "in the window" only if the window belongs to a cycle line shown in the same view.
  - **Case 1: an unshown next cycle (menstrual-relation view).**
    - Example: the view covers 1–30 September, the as-of date is 5 October, and menstruation began on 3 September and 1 October.
    - The cycle of 3 September is complete and is shown to 30 September (E-060: "shown to the day before the next first day of menstruation"). Day 1 of the next cycle is therefore an output fact: 1 October.
    - An attack with onset on 29 or 30 September is on day −2 or −1 of that menstruation, inside the ICHD-3 A1.1 window.
    - The 1 October cycle cannot be shown in the view, for two reasons. It does not overlap the covered period, so it cannot be in `v.cycles`. And as an unfinished cycle it would have to end on `covers.end`, 30 September, which is before it begins, and no `DateSpan` admits that.
    - INV-087 therefore forces the 29 and 30 September attacks to be shown as outside the perimenstrual window.
  - **Case 2: attack marks without a shown cycle (patient-facing overview).**
    - INV-105 requires only one cycle line that overlaps the period.
    - Attack marks there need not belong to a cycle line shown in the view: the `∃₁ cl` conjunct applies only to the menstrual-relation view.
    - A shown attack on day 1 to +3 of a menstruation whose cycle line is not shown is therefore also forced to "outside".
  - **Consequence.** A definitional relation excludes the correct value and admits only a value that contradicts ICHD-3 A1.1. That breaks OUT-030's MUST to distinguish the perimenstrual window as ICHD-3 defines it.
- Evidence:
  - [S-001] "Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3)" (A1.1.1, criterion B, p. 190).
  - [S-001] "The first day of menstruation is day 1 and the preceding day is day −1; there is no day 0." (A1.1.1, note 2, p. 190).
  - Both are quoted in E-060.
  - OUT-030: "distinguishing the perimenstrual window as defined in ICHD-3 appendix A1.1 [S-001] from other days of the cycle".
  - INV-087, the per-cycle conjunct `(¬ cl.complete ⇒ cl.cycle.to = viewOf(cl).covers.end)` and the MRV conjunct requiring every cycle to overlap the covered period.
  - The E-060 and INV-087 Notes consider only windows that begin in the previous cycle shown ("so attacks are matched against the windows of all cycles shown in the view").
- Required change:
  - Make the in-window relation correct for every cycle line, using the fact that a complete cycle shows the next day 1 (`next(cl.cycle.to)`). For example: `a.inPerimenstrualWindow ⇔ ∃ cl ∈ viewOf(a).content ∩ CycleLine • a ∈ cl.attacks ∧ (inSpan(a.onset, cl.perimenstrualWindow) ∨ (cl.complete ∧ plusDays(cl.cycle.to, −1) ≤ a.onset))`. Here `plusDays(cl.cycle.to, −1)` is day −2 of the next menstruation, and `windowDaysBefore − 1` may be written for the 1.
  - Require in every view, not only in the menstrual-relation view, that each attack mark belongs to the attacks of exactly one cycle line shown in the same view. Alternatively, restrict the relation to such marks and state what an unattached mark means.
  - Update the INV-087 Reading, the E-060 and E-061 Notes and the OUT-030 and OUT-035 traceability text.

### R03-04 Coverage gap: in the clinician-facing summary, the time course, the weekly view and the medication-overuse indicators are not tied to the period the summary covers
- Item(s): INV-104, E-066, section 7 row OUT-034
- Problem: INV-104 requires, when the covered period contains a whole period, "a series" whose first and last periods lie within the covered period. Nothing requires the series to span the covered period or to be monthly. Three consequences follow, all of which the model admits:
  - **(a) A one-period time course.** A summary of the six months since the previous consultation can show, as its "time course", one calendar week or one month. OUT-009 asks for a time series of consecutive periods "so that onset of effect, the trajectory of response and spontaneous fluctuation can be seen".
  - **(b) No overuse indicator.** The medication-overuse indicators are required only `sr.granularity ∈ MonthlyKind ⇒ ∀ p ∈ ran sr.periods • …`. If the chosen series is weekly, the summary is required to show no medication-overuse indicator at all, although OUT-034 names "acute medication use and any medication-overuse indicator (OUT-014 to OUT-016)". A one-month series reduces the indicators to one month.
  - **(c) An unanchored weekly view.** The weekly acute-medication series, `(∃ sr ∈ v.content ∩ Series • sr.granularity = calendarWeek ∧ perPeriod(v, sr, TotalAcuteMedicationDays, allTypes))`, has no relation to the covered period at all. Any week, even one years earlier, satisfies it.
- Evidence:
  - OUT-034 Statement: "a concise clinician-facing summary for the period since the previous consultation (or a period chosen by the clinician) that brings together [...] frequency measures and their time course (OUT-004 to OUT-009), acute medication use and any medication-overuse indicator (OUT-014 to OUT-016) [...]".
  - OUT-009: "as a time series of consecutive reporting periods [...] so that onset of effect, the trajectory of response and spontaneous fluctuation can be seen".
  - OUT-015: "acute medication days per calendar week".
  - INV-104: `((∃ g : Granularity • containsPeriodOf(spanOf(v.covers), g)) ⇒ ∃ sr ∈ v.content ∩ Series • within(first(sr.periods), v.covers) ∧ within(last(sr.periods), v.covers) ∧ … ∧ (sr.granularity ∈ MonthlyKind ⇒ … MedicationOveruseIndicator …))`.
  - Compare INV-035 and INV-105, which make their series tile the covered period.
- Required change: in INV-104:
  - **(i)** Require the series to consist of all whole periods of its granularity within the covered period. Possible form, together with the existing `within` conjuncts: `¬ ∃ d₁, d₂ : Date • v.covers.start ≤ d₁ ∧ d₁ ≤ d₂ ∧ d₂ ≤ v.covers.end ∧ ofKind(d₁, d₂, sr.granularity) ∧ (d₂ < first(sr.periods).start ∨ last(sr.periods).end < d₁)`.
  - **(ii)** Require such a series of calendar months or 28-day periods, with its overuse indicators, whenever the covered period contains a whole calendar month or 28-day period (`containsPeriodOf` for a `MonthlyKind`).
  - **(iii)** Require the weekly acute-medication series to satisfy the same condition for calendar weeks whenever the covered period contains a whole calendar week, and drop the unguarded weekly conjunct otherwise.

  Update the INV-104 Reading and Notes and the OUT-034 traceability text.

### R03-05 Coverage gap: for children and adolescents, the equal-length rule omits the treatment review view, post-stop monitoring and changes outside response comparisons
- Item(s): INV-097, E-037 Conformance, E-048, E-049, E-040, section 7 row OUT-036
- Problem:
  - **The model's reading.** The model reads OUT-036 (c) as "for children and adolescents, the periods compared in one comparison have equal length" (INV-097 Reading).
  - **Where it applies.** The predicate applies only to `PeriodComparison` and `ResponseComparison`.
  - **Comparisons it leaves out.** Three other kinds of comparison of periods are not constrained:
    - the treatment review view (E-048), which presents its measures "for the same pre-treatment baseline and on-treatment periods" (OUT-021) so that efficacy can be judged;
    - the post-stop monitoring view (E-049), which by OUT-022 must "compare it with both the on-treatment period and the original pre-treatment baseline";
    - every `Change` (E-040) outside a response comparison, which compares a reference period with a compared period (for example in a scheme-window view).
  - **Example.** For a child, an output may compare a 90-day baseline with 28-day on-treatment periods in the treatment review view, or a 14-day post-stop period with a 3-month baseline, and satisfies every invariant.
  - **Earlier reviews.** Iterations 01 and 02 recorded INV-097 as applying "to every paediatric comparison". That is not what its predicate says.
- Evidence:
  - OUT-036 Statement: "(c) apply equal-length period comparisons as in OUT-001".
  - OUT-022: "compare it with both the on-treatment period and the original pre-treatment baseline".
  - OUT-021: "present together, for the same pre-treatment baseline and on-treatment periods".
  - INV-097: `ctx.subject.ageGroup = childOrAdolescent ⇒ (∀ pc : PeriodComparison • equalLengths(ran pc.periods)) ∧ (∀ rc : ResponseComparison • equalLengths({rc.baseline} ∪ ran rc.onTreatment))`.
  - INV-068 and INV-070 place no length constraint on their periods.
- Required change:
  - Extend INV-097 to:
    - `TreatmentReviewView` (`{v.baseline} ∪ ran v.onTreatment`);
    - `PostStopMonitoringView` (`v.baseline ∪ v.onTreatmentPeriod ∪ ran v.after`);
    - every `Change` (`ch.reference.period` and `ch.compared.period`).

    These are satisfiable together with INV-068 and INV-070: choose periods of a common length no longer than the time between the treatment start and the event. Alternatively, state the Stage 1 reason why OUT-036 (c) does not apply to these comparisons.
  - Update E-037 Conformance, E-048 and E-049 Conformance and the OUT-036 traceability text.

### R03-06 Infidelity (narrowing): the validated instruments are a closed list, although OUT-026 names them only as examples
- Item(s): E-057 (`enum Instrument`), E-008 (`InstrumentAdministration`), E-058, INV-081, INV-069, section 7 rows OUT-026 and OUT-021
- Problem:
  - **The closed list.** `Instrument` is a closed enumeration of the nine instruments named in OUT-026. `InstrumentAdministration.instrument` and `InstrumentResult.instrument` have that type.
  - **What OUT-026 actually asks.** It asks for the results of validated instruments "where [they] are available", and introduces the named instruments with "include".
  - **Consequences.**
    - A context cannot express an available result of any other validated impact, disability or quality-of-life instrument.
    - INV-081 never requires such a result to be reported.
    - E-058 (name, completion date, recall period, total score, published grading, change from baseline) and INV-069 ("the most recent results of disability, impact or quality-of-life instruments", OUT-021) do not apply to it.
  - **Inconsistency.** For OUT-033, whose instruments are likewise examples ("for example HADS, PHQ-9, GAD-7"), the model keeps the list open with `otherScreeningInstrument ⟨Text⟩` (E-059). Stage 1's Caveat on MIBS-4 explains why that instrument is not named; it does not restrict the Statement to the named list.
- Evidence:
  - OUT-026 Statement: "Where results of validated instruments are available, the diary output SHOULD report them with the instrument name, completion date, recall period, total score and the instrument's own published grading or categories, and the change from the baseline administration. Instruments named in the evidence include MIDAS, HIT-6, MSQ v2.1, HALT, HURT, the Migraine Treatment Optimization Questionnaire (mTOQ/M-TOQ), PedMIDAS for children, and Patient Global Impression of Change (PGIC)."
  - E-057: `enum Instrument ::= midas | hit6 | msq21 | halt90 | halt30 | hurt | mtoq | pedmidas | pgic`.
  - E-059: `variant ScreeningInstrument ::= hads | phq9 | gad7 | otherScreeningInstrument ⟨Text⟩`.
- Required change:
  - Keep the instrument set open in the same way as `ScreeningInstrument`. For example, make `Instrument` a variant with an additional `otherInstrument ⟨Text⟩` (a validated impact, disability or quality-of-life instrument, named as the output shows it), with `instrumentName(otherInstrument(x)) = x`.
  - The value-set functions (`publishedRecall`, `scoreRange`, `gradeBands`) stay defined only for the tabulated instruments.
  - Update the E-057 Meaning and the OUT-026 traceability text.

### R03-07 Citation defect: `publishedGrading(pgic)` is asserted without a cited source
- Item(s): E-057 (`publishedGrading` axiom, Evidence, Notes), E-058 (`category … SHOULD when publishedGrading(self.instrument)`), section 11
- Problem:
  - **The assertion.** The axiom states that the developer of PGIC publishes a grading or categories (`publishedGrading(pgic)`).
  - **Its effect.** Through E-058 it makes a category SHOULD on every PGIC result.
  - **Missing evidence.** No quote in E-057 or in Stage 1 supports it. Every other value of the axiom is supported:
    - MIDAS, HIT-6, PedMIDAS and HALT-90 by [S-102], [S-101], [S-103] and [S-014];
    - HURT and the negative for HALT-30 by the Stage 1 [S-014] quotes.
  - **The model's own search.** The model left this value unsupported deliberately: the search log says "PGIC exists in several versions with different wordings. Their value sets are therefore not tabulated". ISS-06 says that "no source verified in Stage 2 defines a total score for it". For MSQ v2.1 and M-TOQ the model leaves `publishedGrading` unfixed for the same reason.
  - **The rule.** PROCESS.md section 4 requires each detail not in Stage 1 about a named instrument's value set to cite a source.
- Evidence:
  - E-057: `axiom publishedGrading(midas) ∧ publishedGrading(hit6) ∧ publishedGrading(pedmidas) ∧ publishedGrading(halt90) ∧ publishedGrading(hurt) ∧ publishedGrading(pgic) ∧ ¬ publishedGrading(halt30)`.
  - E-057 Notes: "`publishedGrading` is not fixed by the model for MSQ v2.1 and M-TOQ; it follows those instruments' own publications".
  - Section 11, row "MSQ v2.1, M-TOQ, PGIC": "PGIC exists in several versions with different wordings."
- Required change: do one of the following.
  - Cite, with a verbatim quote, location and URL, a source that defines the PGIC response categories (the version the model refers to).
  - Or remove `publishedGrading(pgic)` from the axiom and treat PGIC like MSQ v2.1 and M-TOQ in the E-057 Notes.

## Checked and not raised

- **Value sets, all matching their quotes:**
  - the ICHD-3 code labels and hierarchy;
  - the 8.2 reference levels (15 for 8.2.3, including its subforms 8.2.3.1–8.2.3.4; 10 for 8.2.1, 8.2.2, 8.2.4, 8.2.5, 8.2.6 and 8.2.8);
  - the "> 3 months" span, which gives four calendar months or four 28-day periods under INV-045 (checked by hand);
  - `classesOf826`;
  - the A1.1 window, day 1 − 2 to day 1 + 2, that is days −2 to +3;
  - the remission duration (`plusMonths(s, 3) ≤ e` encodes "must exceed three months");
  - the HIT-6 range and bands, and the MIDAS, PedMIDAS and HALT-90 bands and labels;
  - the HADS, PHQ-9 and GAD-7 ranges;
  - the HIT-6, MIDAS, PedMIDAS, HALT-90 and HALT-30 recall periods;
  - the IHS Q6, NICE 1.3.28/1.3.29, DMKG/ÖKSG/SKG and Russian 7.1 thresholds;
  - the IHS 2025 control levels in INV-064;
  - the eleven evaluation rules of E-041 against their Stage 1 quotes.
- **HALT-90 grade labels.** Table 18 prints the grades as "III (indicates high need for care)" and "IV (indicates high need for care)". The model shows the grade numeral and the "Assessed impact" label. The parenthetical describes the grade and is not a category label, so this is not a misstatement.
- **HIT-6 recall "1 month".** The HIT-6 form words its items "in the past 4 weeks". The model follows Stage 1 [S-002] ("1-month recall period") and [S-101] ("a one-month recall of the HIT-6"), whose last author is a HIT-6 developer. Not raised.
- **Optimal control and acute response.** INV-064 does not test the acute-response part of "Optimal Control" ("satisfactory response to acute treatment"). [S-010] gives no threshold for how many treated attacks must be pain-free, so that part cannot be decided from shown values. INV-062 requires the acute-treatment values to be shown. Not raised.
- **Co-presence of response-comparison values.** Every item is part of exactly one view (section 2.5). By INV-003, a period atom referenced by an item must be in that item's view. So the values and changes of a response comparison, whose periods are its baseline and on-treatment periods (INV-056), are necessarily in the comparison's view. The same holds for the basis of an overuse indicator (INV-045). No gap.
- **A response comparison right after the treatment start.** INV-055 requires a comparison for every started treatment, even when no monthly on-treatment period has ended by the as-of date. Stage 1 states the MUST "for each preventive treatment" without such a condition, so this follows Stage 1. Not raised.
- **Cycle lines in the patient-facing overview.** These carry the MUST attributes of E-060. A diary that shows the relationship to menstruation differently deviates only from the SHOULD of INV-105, so MUST conformance is unaffected. Not raised.
- **Treatment-history groups.** The groups and lines of a treatment-history view are references and may be shown in another view of the same output. OUT-024 requires no co-presence with other content. Not raised.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT for the OUT-018 Caveat (model section 3.3(6); iteration 01 fix);
  - the AAN/AHS 14A and NVN window readings;
  - INV-023 at any granularity;
  - INV-060 with INV-061 for compared periods shorter than 28 days (considered by the iteration 02 fixer);
  - the cluster remission "> 3 months" (Definitions of terms) against "≥3 months" in 3.1.1 criterion B, which iteration 02 found to be an inconsistency inside ICHD-3;
  - the context (`SubjectProfile`) as subject properties, not input entities;
  - the MIDAS label choice;
  - the 24-hour outcomes for cluster summaries;
  - "history of previous bouts".
- **Section 8.**
  - ISS-01 to ISS-06, ISS-08 and ISS-09 are founded and carry pointers from the affected elements.
  - ISS-02 was re-verified: the only "simple analgesics" in ICHD-3 is on p. 139.
  - R03-01 is a defect of the model's relation, not a Stage 1 issue.
  - No Stage 1 issue is silently worked around.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md and oscillation reports do not exist for Stage 2.
