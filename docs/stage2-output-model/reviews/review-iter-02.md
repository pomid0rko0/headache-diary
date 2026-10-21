# Review — iteration 02
VERDICT: REMARKS
REMARK_COUNT: 7
Reviewed version: v01
Date: 2026-10-21

## Summary

v01 fixes the twelve remarks of iteration 01 correctly. The citation base is sound:

- every quote of the five new sources (S-101 to S-105) and every Stage 2 quote of S-001, S-008, S-010 and S-014 was found verbatim at its stated location and URL;
- the metadata is correct;
- ICHD-3 is still the current edition.

The mechanical checks are clean (IDs, references, traceability, declarations, attribute selections, typing rule for levels). The scope sweep found no input, storage or derivation-from-input content.

The remaining defects are of three kinds:

- **Satisfiability.**
  - The MUST invariants INV-055 and INV-056 cannot both hold in some admissible contexts, so no diary can be MUST-conformant (R02-01).
  - Two pairs of SHOULD invariants contradict each other (R02-02).
  - Two invariants exclude correct outputs or leave a derived value undefined (R02-05, R02-07).
- **Fidelity.**
  - OUT-021 MUST is narrowed to the total of acute-medication days (R02-03).
  - The baseline comparison of OUT-027 omits days with severe impairment (R02-04).
  - The per-attack part of OUT-012 has a narrower applicability condition than its across-period part (R02-06).
- **Section 8.** No defect found.

## Verification coverage

Downloads were made with `curl` into fresh directories under the session scratchpad (`.../scratchpad/r02/dl_*`), outside the repository:

- PDFs were split into pages with `pdftotext -f/-l`. The ICHD-3 classification list was also extracted with `-layout`, because it is a two-column table.
- HTML and XML were tag-stripped by script, and Python was run with `-I`.
- Each quote was split at `[...]` and checked in three passes: (1) exact after collapsing whitespace; (2) after normalising typographic quotes, dashes, ligatures and line-end hyphens and removing the ICHD-3 glyphs "≥", "±" and "≤", which have no text mapping; (3) alphanumeric only.
- Every pass-2 or pass-3 match was inspected in context. The only differences were:
  - the ligature "ﬁ";
  - footnote markers (for example "opioids1");
  - line-end breaks ("nonopioid", "combinationanalgesic");
  - unmapped glyphs ("≥", "±", "−"; "+3" renders as "þ3");
  - the S-010 running header "Cephalalgia 45(2)" inside the Insufficient Control sentence.

### Citations

| Source | Where checked | Quotes checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|---|
| S-001 ICHD-3 (Stage 1 URL, PDF page = printed page) | ichd-3.org PDF, 211 pages | 29: 15 code labels (pp. 8, 9, 12, layout mode); 8.2.3 comment; 8.2.6 criterion B and note 2; 8.2, 8.2.1, 8.2.2, 8.2.3 Descriptions; 8.2.4, 8.2.5, 8.2.8 criterion B; A1.1.1 and A1.1.2 criterion B; A1.1.1 note 2; cluster remission (p. 209) | 29 | 0 | 0 |
| S-008 IHS 2024 prevention (Stage 1 URL) | univaq PDF | 3: Q6 30 % alternative (p. 12); MIDAS/HIT-6 AHS definition (p. 13); PGIC judgement wording of `critIhsQ6` (p. 12, Q6 list) | 3 | 0 | 0 |
| S-010 IHS position statement 2025 (Stage 1 URL) | univaq PDF | 5: four control levels and the "In some cases" sentence (p. 6) | 5 | 0 | 0 |
| S-014 Lifting The Burden/EHF (Stage 1 source) | Europe PMC XML of PMC6734476; the PMC URL serves the text (HTTP 200) | 5: HALT-90 and HALT-30 recall; "whole days" unit; Table 18 (heading, 3 columns, 4 rows); HURT sentence (ISS-06) | 5 | 0 | 0 |
| S-101 Yang et al. 2011 | Europe PMC XML; PMC URL HTTP 200 with the text | 2 | 2 | 0 | 0 |
| S-102 Pavlović et al. 2015 | Europe PMC XML; PMC URL HTTP 200 with the text | 2 | 2 | 0 | 0 |
| S-103 Cincinnati Children's PedMIDAS page | listed URL, HTTP 200; heading "PedMIDAS Tool for Assessing Migraine Disability"; footer "© 2026" | 1 (lead sentence, 2 headings, 4 rows) | 1 | 0 | 0 |
| S-104 Snaith 2003 | Europe PMC XML; PMC URL HTTP 200 with the text | 1 | 1 | 0 | 0 |
| S-105 PHQ/GAD-7 instructions (Joint Commission copy) | listed PDF, HTTP 200; pages headed "P.6/9" (section "USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES") and "P.8/9" ("QUESTIONS REGARDING DEVELOPMENT, ACKNOWLEDGMENTS AND USE") | 3 | 3 | 0 | 0 |
| **Total** | | **51** | **51** | **0** | **0** |

Notes on the citation check:

- The PMC article pages first returned a reCAPTCHA browser-check page to a browser user agent. With curl's default user agent they returned the full text, so the quotes can be read at the listed URLs.
- **Metadata** (PubMed esummary), all correct:
  - S-101: Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMID 20819842, PMC3057423; authors as listed.
  - S-102: J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMID 25902814, PMC4406925; 7 authors as listed.
  - S-104: HQLO 2003;1:29, DOI 10.1186/1477-7525-1-29, PMID 12914662, PMC183845.
  - S-103 developer paper: Neurology 2001;57(11):2034–9, PMID 11739822, DOI 10.1212/wnl.57.11.2034.
  - S-105 PDF metadata: author Kurt Kroenke, created 2010-06-22, modified 2014-04-16.
- **Newer versions.**
  - A web search finds only "International Classification of Headache Disorders-4 – Work in Progress 1" (Cephalalgia 2024) and an ICHD-IV workshop (September 2025); ICHD-3 (2018) is still current.
  - The HIT-6 bands of S-101 are attributed there to the developer's interpretation guide.
- **Stage 1 fragments and other quoted strings.** A script checked all 263 quoted strings in the Evidence, Notes, Meaning, Reading and Conformance fields and the traceability rows:
  - 166 are exact substrings of Stage 1 v18;
  - 84 occur in the downloaded sources;
  - the remaining 13 are model wording, case-only variants of Stage 1 phrases ("where weekly granularity…" vs Stage 1 "Where…"; "The following year"; "Headache and migraine frequency"; "Shareable…"; "Acute medication outputs"), single quotes nested in double quotes, or the S-010 sentence checked in two parts.
- **No new non-English quotes.** There are no new non-English quotes in Stage 2.

### Per-OUT fidelity check (Statement, Caveats, strength, traceability row)

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK | 021 | **R02-03** |
| 002 | OK | 022 | OK (ISS-03) |
| 003 | OK (SHOULD / SHOULD NOT) | 023 | OK |
| 004 | OK | 024 | **R02-05** |
| 005 | OK | 025 | OK (MAY) |
| 006 | OK | 039 | OK |
| 007 | OK | 026 | OK (ISS-06) |
| 008 | OK (MAY) | 027 | **R02-04** |
| 009 | OK | 028 | OK (ISS-03) |
| 010 | OK; see R02-02 (b) for INV-039 | 029 | OK (ISS-09) |
| 011 | OK | 030 | OK |
| 012 | **R02-06** | 031 | OK |
| 013 | OK (MAY) | 032 | OK |
| 014 | OK | 033 | OK |
| 015 | OK | 034 | OK; see R02-02 (a) for INV-094/INV-104 |
| 016 | OK (MUST / MUST NOT; ISS-01, ISS-09) | 035 | **R02-07** |
| 017 | OK | 036 | OK; see R02-02 (b) for INV-097 |
| 018 | **R02-01** (satisfiability of the MUST) | 037 | OK |
| 019 | OK (ISS-05) | 038 | OK |
| 020 | OK (ISS-08) | | |

Conformance levels were compared with the Stage 1 strengths for all 107 invariants and for the attribute levels of every element:

- MUST 18: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054–057, 059, 068, 086, 102;
- MUST NOT 2: INV-048, 106;
- SHOULD NOT 8: INV-013, 021, 043, 065, 084, 091, 101, 107;
- SHOULD 47;
- definitional 32.

No level mismatch was found. MUST NOT INV-106 for the OUT-018 Caveat follows model section 3.3(6).

### Mechanical checks (scripts in `.../scratchpad/r02/scripts`)

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067), 107 invariants (INV-001–INV-107); consecutive, no duplicates |
| Dangling references | none. ISS headings: ISS-01–06, 08, 09; ISS-07 appears only in sections 8 (note), 9 and 12. S-refs are within S-001–S-046 or S-101–S-105; OUT-refs are within 001–039 |
| Realises fields and traceability | every item has a Realises field; 39 rows in Stage 1 order (OUT-039 after OUT-025); 0 differences between the rows and the union of Realises fields; 39 × "full" |
| ISS pointers | every ISS is pointed to from the Notes of the elements it names (ISS-01: E-028/029/032; ISS-03: E-038/043/049/067; ISS-04: E-020–022, E-066; ISS-05: E-018/044; ISS-06: E-057/058; ISS-08: E-046; ISS-09: E-029/032/036) |
| Names in `omn` blocks | 293 declared names, none declared twice; 198 enumeration constants and variant tags, no duplicates |
| Attribute selections `e.a` | every selected attribute is declared in an element or value type |
| Typing rule for levels | 164 attribute declarations parsed (2 refinement-typed core attributes checked by hand); no SHOULD, MAY or MUST-with-`when` attribute lacks an `opt`/`set`/`seq` type; none uses `set1`/`seq1` |
| Partial terms | `first`/`last` only on `seq1` or guarded; `÷` guarded; `days` guarded by `s ≤ e`; `max A` by `A ≠ ∅`; `i.span(2)` by `#i.span ≥ 2` |
| Scope sweep (enter, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, entry, reminder, field, obtained, calculated, computed, algorithm) | only the exclusion statements (sections 1, 2.1, 2.7); the "out of scope" Notes of E-014, E-033 and E-057; the S-014 HALT-30 recall quote (used for the recall value); "answered" in the INV-014 Reading; tool names |
| Thresholds, formulas, derived attributes: arguments | every relation takes output elements, context properties (section 3.5) or cited constants. Derived attributes without a relation are those obtained from diary information, which is correct, except `TreatmentLine.duration` for ongoing treatments (R02-05) |
| Satisfiability of invariant combinations | contradictions found: INV-055 + INV-056 under INV-001 (R02-01); INV-094 + INV-104 and INV-039 + INV-097 (R02-02). Checked without contradiction: INV-003 + INV-044 + INV-045; INV-040 + INV-041; INV-086 + INV-087; INV-071 + INV-072 + INV-074; INV-031 + INV-104 |

## Remarks

### R02-01 Formal defect: the MUST invariants INV-055 and INV-056 cannot both hold in some admissible contexts
- Item(s): INV-055, INV-056, INV-001, E-041 (`ruleNice1329`, `anchorDates`), E-008 (`courseEvents`)
- Problem:
  - **What INV-055 requires (MUST).** For each applicable rule r and anchor date a with `shift(a, r.minOffset) ≤ c.asOf`, a response comparison must exist with an on-treatment period p such that `atTimePoint(p, tp)`. For `atOffset` and `atLeastOffset` rules this means `p.end = shift(a, r.minOffset)`; for `withinWindow` rules, a p.end between the offsets.
  - **What INV-056 requires (MUST).** Every on-treatment period is a calendar month or a 28-day period and begins on or after the treatment start s. So p.end ≥ s + 27 days.
  - **What INV-001 leaves open.** INV-001 does not order a treatment's course events relative to its start. It only requires `e.date ≤ c.asOf` and at most one start. In addition, `ruleNice1329` has `minOffset ↦ weeks(0)` and is anchored at the end of the second treatment cycle.
  - **Two admissible counterexamples.**
    - (i) An onabotulinumtoxinA treatment with start s and a `cycleEnd(2)` event on s + 20 days. INV-055 requires p.end = s + 20, and INV-056 requires p.end ≥ s + 27.
    - (ii) A preventive treatment whose `targetDoseReached` event is dated more than 4 weeks before its start. The AAN/AHS 14A window `[anchor + 8 weeks, anchor + 12 weeks]` then ends before s + 27.
  - **Consequence.** `Ctx` contains every `OutputContext` value that satisfies the context invariants (section 3.2), and INV-055 quantifies over all of `Ctx`. So no repertoire satisfies INV-055 and INV-056 together, and no diary can be MUST-conformant.
- Evidence:
  - E-041: `ruleNice1329 = EvaluationRule(... anchor ↦ endOfCycleAnchor(2), timing ↦ atOffset, minOffset ↦ weeks(0), maxOffset ↦ ∅)`.
  - INV-056: `(∀ p ∈ ran rc.onTreatment • p.kind ∈ MonthlyKind) ∧ ... (∀ p ∈ ran rc.onTreatment • rc.treatmentStart ≤ p.start)`.
  - E-042: `atTimePoint`: `tp.rule.timing ∈ {atOffset, atLeastOffset} ⇒ p.end = tp.earliest`.
  - INV-001 (the only conjuncts on course events): `(∀ e ∈ c.subject.courseEvents • e.treatment ∈ ... ∧ e.date ≤ c.asOf) ∧ (∀ t ∈ ... • #{e ∈ c.subject.courseEvents | e.treatment = t ∧ e.kind = start} ≤ 1)`.
  - The satisfiability argument in fixes/fix-iter-01.md (R01-03) rests on two premises that the model does not contain: "Every rule's offset is at least 8 weeks from its anchor, and the anchor is on or after the start".
- Required change: make INV-055 satisfiable in every admissible context. Ordering the course events alone does not suffice, because of the 0-week offset of `ruleNice1329`. Options:
  - (a) Guard the time-point clause of INV-055 so that it applies only when a monthly on-treatment period ending at the time point can begin on or after the start. For `atOffset` and `atLeastOffset`: `plusDays(s, 27) ≤ shift(a, r.minOffset)`. For `withinWindow`: `plusDays(s, 27) ≤` the latest date, with the period then ending between the later of the earliest date and s + 27, and the latest date. Optionally, also add to INV-001 that a treatment's course events other than its start do not precede its start, and that cycle ends follow the order of their numbers.
  - (b) Another construction with the same effect, with a stated reason.

  After the change, re-check INV-055 + INV-056 + INV-097 for satisfiability.

### R02-02 Formal defect: two pairs of SHOULD invariants contradict each other in admissible contexts
- Item(s): INV-094, INV-104, E-066; INV-039, INV-097
- Problem:
  - **(a) Clinician-facing summary since the previous consultation.**
    - INV-001 admits any previous-consultation date d ≤ `c.asOf`, including d = `c.asOf` or a date a few days earlier.
    - INV-094 (SHOULD) then requires a `ClinicianSummary` that covers exactly [d, `c.asOf`].
    - INV-104 (SHOULD) requires every `ClinicianSummary` to contain a series whose first and last periods lie within the covered period.
    - A series period is a whole calendar month, a 28-day period or a calendar week (E-006 `Granularity`, INV-002, INV-004). It cannot lie within a covered period of fewer than 7 days, nor within a covered period that contains no whole calendar week. For example, a covered period from a Wednesday to the Friday of the following week (10 days) contains no whole Monday-to-Sunday week.
    - So for follow-up intervals shorter than about two weeks, the two SHOULD invariants cannot both hold.
  - **(b) Paediatric comparisons.**
    - INV-039 (SHOULD) requires, for every context with two or more selected comparison periods, a `PeriodComparison` whose periods are exactly the selected spans (`matchesSelection`). It places no condition on their lengths.
    - INV-097 (SHOULD) forbids, for children and adolescents, any `PeriodComparison` whose periods differ in length.
    - Example: a child with the selected spans January (31 days) and February (28 days). The two invariants contradict each other.

  The model defines full conformance as satisfying every SHOULD constraint unless a valid reason justifies a deviation (section 3.2). Here a deviation is forced by the model itself, not by circumstances.
- Evidence:
  - INV-094: `(∀ d ∈ c.previousConsultation • ∃ o : Output • (c, o) ∈ Rep ∧ ∃ v ∈ o.views ∩ ClinicianSummary • v.covers.start = d ∧ v.covers.end = c.asOf)`.
  - INV-104: `(∃ sr ∈ v.content ∩ Series • within(first(sr.periods), v.covers) ∧ within(last(sr.periods), v.covers) ∧ ...)`.
  - INV-001: `(∀ d ∈ c.previousConsultation • d ≤ c.asOf)`.
  - INV-039: `∀ c ∈ Ctx • #c.comparedSpans ≥ 2 ⇒ ∃ o ... pc ∈ v.content ∩ PeriodComparison • matchesSelection(pc, c) ∧ ...`.
  - INV-097: `ctx.subject.ageGroup = childOrAdolescent ⇒ (∀ pc : PeriodComparison • equalLengths(ran pc.periods)) ∧ ...`.
  - Stage 1 OUT-034 ("for the period since the previous consultation (or a period chosen by the clinician)"), OUT-010 ("allow comparison between periods") and OUT-036 (c) ("apply equal-length period comparisons as in OUT-001") are compatible with each other. The conflict comes from the formalisation.
- Required change:
  - (a) Make INV-104 satisfiable for every covered period that INV-094 requires. Options:
    - require the time-course series only when the covered period contains at least one whole period of some granularity;
    - or let the series extend beyond the covered period (for example, ending with the period that contains `v.covers.end`);
    - or another construction with the same effect.
  - (b) Remove the conflict, either by restricting INV-039 for children and adolescents to selections of equal length, or by exempting comparisons of a selection from INV-097. Give the Stage 1 reason for whichever reading is chosen.

### R02-03 Infidelity (narrowing): the treatment review view requires only the total of acute-medication days, although OUT-021 includes the acute-medication days of OUT-014 at MUST
- Item(s): INV-068, E-048 (Meaning, Conformance), section 7 row OUT-021
- Problem:
  - OUT-021 makes it a MUST to present, for the same baseline and on-treatment periods, "acute medication days (OUT-014)".
  - The output of OUT-014 is the number of acute-medication days "broken down by drug class ... and by individual drug, together with the total across classes".
  - INV-068 requires only `acuteMedicationDays(allAcuteMedication)`. Neither the per-class nor the per-drug days are required in the treatment review view, and no Stage 1 issue records this reading.
  - The model reads the same kind of reference to OUT-014 as total, class and drug elsewhere:
    - INV-104 for OUT-034 ("acute medication use ... (OUT-014 to OUT-016)");
    - INV-028 for OUT-029, after R01-06, where a total-only reading was accepted as a narrowing and fixed.
  - Section 3.5 (reference rule) also treats a component cited by its requirement ID as that requirement's output.
- Evidence:
  - OUT-021 Statement: "the diary output MUST present together, for the same pre-treatment baseline and on-treatment periods, headache days (OUT-004), migraine days (OUT-005) and acute medication days (OUT-014)"; Strength: "MUST for presenting OUT-004, OUT-005 and OUT-014 together for the same periods".
  - OUT-014 Statement: "MUST report, per reporting period, the number of days with acute (symptomatic) headache medication, broken down by drug class as used in ICHD-3 code 8.2 and its subtypes [...] and by individual drug, together with the total across classes."
  - INV-068: `... shownDay(v, acuteMedicationDays(allAcuteMedication), p, allTypes)`, the only acute-medication conjunct.
- Required change: one of the following.
  - Extend INV-068 so that, for every baseline and on-treatment period of the view, it also requires the per-class and per-drug acute-medication days of the subject's acute medications, as INV-023 and INV-104 do. Update E-048 Meaning and Conformance and the OUT-021 traceability text.
  - Or, if the author reads "acute medication days (OUT-014)" in OUT-021 as the total only, record that reading as a Stage 1 ambiguity in section 8, with pointers from E-048 and INV-068. Do not narrow the MUST silently.

### R02-04 Coverage gap: the comparison of functional impact with the baseline period omits the days with severe functional impairment
- Item(s): INV-027, E-030 (Conformance), section 7 row OUT-027
- Problem:
  - OUT-027 asks the output to report per period the days affected in three domains, "including days with severe functional impairment", and to "allow comparison with the baseline period".
  - INV-027 requires, for the baseline and on-treatment periods, only the days affected in the three domains. The severe-impairment days are not required in the comparison, although INV-026 requires them per period.
  - Iteration 01 fixed the same omission in INV-104 (R01-09 (c)) but did not fix it in INV-027.
- Evidence:
  - OUT-027 Statement: "The diary output SHOULD report, per reporting period, the number of days on which headache affected paid work or school, household work and social or leisure activities, including days with severe functional impairment, expressed in days per period, and SHOULD allow comparison with the baseline period."
  - INV-027: `∀ p ∈ {rc.baseline} ∪ ran rc.onTreatment; d ∈ {paidWorkOrSchool, householdWork, socialOrLeisure} • ∃ m ∈ v.content ∩ fiDays(d, affected) • m.period = p ∧ m.typeScope = allTypes`.
  - INV-026 includes `{m : DayCount | ∃ d : ImpactDomain • m.measure = functionalImpactDays((d, severelyImpaired))}`.
- Required change: add to INV-027, for every baseline and on-treatment period, the days with severe functional impairment, as in INV-026 and INV-104. Update the INV-027 Reading and the OUT-027 traceability text.

### R02-05 Formal defect: the derived duration of a treatment line has no defined meaning for an ongoing treatment
- Item(s): E-055 (`duration`, Notes), INV-079
- Problem:
  - `duration : opt Duration derived SHOULD` has no `when` clause, so it is required for every treatment line, including treatments that have not stopped. OUT-024 lists "treatment duration" for every treatment of the list.
  - Its only relation is in INV-079, and that relation applies only when both a start date and a stop date are shown: `∀ s ∈ l.startDate; e ∈ l.stopDate • s ≤ e ∧ ∀ d ∈ l.duration • d = daysLong(days(s, e))`.
  - For an ongoing treatment, no stop date is shown (`stopDate` is SHOULD only `when stopped(...)`). The shown duration is then unconstrained: any value satisfies the model.
  - The model does not say up to which date an ongoing treatment's duration runs (the as-of date, or the end of the period the view covers). This is a derived output field without a relation, although its relation is to shown output elements: the start date and the end of the covered period.
  - The model solves the same problem for ongoing cluster periods with `ongoing` and `lastDay` (E-063, INV-089), and for unfinished menstrual cycles in INV-087 (R01-08).
- Evidence:
  - E-055: `startDate : opt Date SHOULD`, `stopDate : opt Date SHOULD when stopped(ctx, self.treatment)`, `duration : opt Duration derived SHOULD`; E-055 Notes: "Relations: INV-079 (... duration agrees with the dates ...)".
  - OUT-024 Statement: "a chronological list of preventive (and, separately, acute) treatments with start and stop dates, dose changes, treatment duration, ...".
- Required change:
  - Define the duration of a treatment that has not stopped, for example from the start date to the last day of the period the view covers, as `lastDay` does in E-063.
  - Add that relation to INV-079 and its Reading.
  - Alternatively, if the author decides that no duration is shown for ongoing treatments, make `duration` SHOULD only `when stopped(ctx, self.treatment)` and give the Stage 1 reason.

### R02-06 Infidelity (applicability condition): migraine-associated symptoms on treated-attack lines are not required for subjects who have migraine and another headache type
- Item(s): INV-076, E-053 (`symptomStatus`), INV-022, E-051, INV-071
- Problem:
  - OUT-012 asks, "For migraine", for the presence of nausea/vomiting, photophobia and phonophobia "both across periods and in the response of individual treated attacks". The model gives the two parts different applicability conditions.
  - **Across periods (INV-022).** INV-022 applies to every subject with migraine (`hasType(c, c1)`), with scope `allTypes`.
  - **Per treated attack (INV-076).** INV-076 applies only to summaries with `concerns(ctx, s.typeScope, c1)`. For an `allTypes` summary, that condition holds only when all of the subject's headache types fall under migraine.
  - **No migraine-scoped summary is ever required.** INV-069, INV-071 and INV-104 require acute-treatment summaries without any type scope. So for a subject with migraine and, for example, tension-type headache (the situation of OUT-029), no invariant requires the three symptom statuses on any treated-attack line.
  - **What remains.** Only the presence constraint of E-053 applies: `symptomStatus ... SHOULD when hasType(ctx, c1)`, a non-empty set, so a single symptom suffices. E-053's condition (`hasType`) and INV-076's condition (`concerns`) are themselves inconsistent.
- Evidence:
  - OUT-012 Statement: "For migraine, the diary output SHOULD report the presence of migraine-associated symptoms (nausea/vomiting, photophobia, phonophobia) and the patient's most bothersome symptom, both across periods and in the response of individual treated attacks (see OUT-023)."
  - INV-076: `∀ s : AcuteTreatmentSummary • hasType(ctx, c1) ∧ concerns(ctx, s.typeScope, c1) ⇒ ∀ l ∈ ran s.sequence; a : AssociatedSymptom • ∃ st ∈ l.symptomStatus • st.symptom = a`.
  - E-012: `concerns(c, sc, t)` for `allTypes` requires `∀ h ∈ c.subject.headacheTypes • h ⊑ t`.
  - INV-071: `∃ s ∈ parts(o) ∩ AcuteTreatmentSummary • s.drug = m.drug ∧ s.formulationScope = allFormulations ∧ sameSpan(s.period, c.timeRange)`, with no type scope.
- Required change: make the per-attack part of OUT-012 apply to every subject with migraine, as the across-period part does. Options:
  - condition INV-076 on `hasType(ctx, c1)` alone, as in INV-022 and E-053;
  - or require, for subjects with migraine and another possible headache type, acute-treatment summaries scoped to migraine (`ofType`), so that INV-076 applies to them;
  - or another construction that requires the three statuses on the treated migraine attacks.

  Make E-053's `when` clause consistent with the chosen condition.

### R02-07 Formal defect: the patient-facing overview must show a menstruation onset within its period, which a correct output often cannot
- Item(s): INV-105, E-067, E-060 (`CycleLine.cycle`)
- Problem:
  - **What INV-105 requires.** For a subject who menstruates, every patient-facing overview must contain a cycle line whose cycle begins within the covered period: `inSpan(cl.cycle.from, spanOf(v.covers))`.
  - **What a cycle's start means.** By E-060 and INV-087, a cycle begins on a first day of menstruation.
  - **Why a correct output can fail.** INV-095 requires an overview for every selected time range, and a time range may be a single calendar week or any other period without a menstruation onset. A correct overview of such a period has no cycle beginning in it, so it cannot satisfy INV-105.
  - **Broadening.** Stage 1 asks only for "the relationship to menstruation". It does not ask for a menstruation onset to fall in every overview period.
  - **Inconsistency.** INV-087 relates cycles to the covered period by overlap: `cl.cycle.from ≤ v.covers.end ∧ v.covers.start ≤ cl.cycle.to`.
- Evidence:
  - INV-105: `(ctx.subject.menstruates ⇒ ∃ cl ∈ v.content ∩ CycleLine • inSpan(cl.cycle.from, spanOf(v.covers)))`.
  - E-060: `cycle : DateSpan core -- from the first day of menstruation to the day before the next one`.
  - INV-095: `∃ v ∈ o.views ∩ PatientOverview • sameSpan(v.covers, c.timeRange)`.
  - OUT-035 Statement: "(headache and migraine days, intensity, acute medication use, treatment effect and, where relevant, the relationship to menstruation)".
- Required change: require a cycle line that overlaps the covered period instead of one that begins in it, as INV-087 does for the menstrual-relation view. Alternatively, use another formulation that a correct overview of any period can satisfy. Update the INV-105 Reading.

## Checked and not raised

- **Quotes and metadata.** All 51 Stage 2 quotes are verbatim at their stated locations. The S-001 note to A1.1.1 note 2 says that the text layer breaks "preceding" at a line end; in the extraction used here the word is not broken. That is a harmless remark on the text layer and the quote is correct.
- **ICHD-3 cluster remission.** Definitions of terms says the attack-free period "must exceed three months" (p. 209), while 3.1.1 criterion B (p. 42) has "remission periods of ≥3 months" ("≥" unmapped in the text layer). OUT-031 asks for "the ICHD-3 definitions" and quotes Definitions of terms, so E-063 and INV-089 (`plusMonths(s, 3) ≤ e`, "more than three months") follow Stage 1. This is an inconsistency inside ICHD-3, not a model defect.
- **HALT units.** S-014 states that question 5 "gives rise to a simple count for which the unit is not whole days" and that it is included in the HALT-90 total summed score. Its own Table 18 nevertheless heads the graded total "Days lost in last 3 months". The E-058 unit comment "days for ... HALT" therefore matches the table, and the source does not settle the question. The whole-number claim (`wholeNumberScores`) holds either way.
- **MSQ v2.1 total score.** S-002 (Stage 1 URL, section 1.3.2.6.1): "This 14-item instrument includes a global scale and three subscales". A total score exists, so ISS-06 does not need to name MSQ v2.1.
- **HADS bands.** S-104 also describes the HADS ranges normal, mild, moderate and severe, and caseness ≥ 11. OUT-033 asks only for "instrument name, date and score", so the model correctly states no categories (E-059 Notes).
- **Value sets.** The following match their quotes:
  - the ICHD-3 8.2 reference levels and span: 15 for 8.2.3, 10 for the other classes and for 8.2.6, "> 3 months" giving 4 calendar months or 4 × 28 days by INV-045;
  - `classesOf826` (8.2.6 criterion B);
  - the INV-046 combined-use relation (8.2.6 note 2);
  - the A1.1 window (day 1 − 2 to day 1 + 2 = days −2 to +3);
  - the HIT-6 range 36–78 and its four bands;
  - the MIDAS, PedMIDAS and HALT-90 bands and labels;
  - the HADS, PHQ-9 and GAD-7 ranges;
  - the IHS Q6, NICE 1.3.28/1.3.29, DMKG and Russian thresholds;
  - the IHS 2025 control levels in INV-064.

  The S-008 Q6 list has exactly the three items that `critIhsQ6` models, plus the chronic-migraine 30 % alternative.
- **Labels under a criterion that does not apply.** Under INV-063, a label whose criterion has no applicable component is forced to "non-responder", because `reductionDecided` and `scoreDecided` treat an unmet condition as decided and not met. An example is "DMKG/ÖKSG/SKG consensus statement (episodic migraine)" shown for a chronic-migraine subject. The criterion's name states its condition, Stage 1 says nothing about such misapplied labels, and for criteria with at least one applicable component the semantics is correct. Not a remark.
- **"Aligned to the treatment start date" (OUT-018).** INV-056 does not require the baseline month to be the one directly before the start. Stage 1 does not define the baseline more precisely, and the on-treatment periods at the guidance time points are anchored to the start (INV-055). Not raised.
- **Context invariants.** These relate shown values to subject properties (course events, available administrations), not to recorded data, which is within section 3.5. This confirms the iteration 01 judgement.
- **Earlier decisions not reopened.** The following were accepted in iteration 01 and I found no new evidence against them:
  - INV-097 applied to every paediatric comparison (the conflict raised in R02-02 is new);
  - the AAN/AHS 14A and NVN window readings;
  - INV-091/INV-093 scope for mixed-type subjects;
  - INV-023 at any granularity;
  - "history of previous bouts";
  - the 24-hour outcomes for cluster summaries;
  - the MIDAS label choice.
- **Section 8.** ISS-01 to ISS-06, ISS-08 and ISS-09 are founded and carry pointers from the affected elements. Apart from R02-03, no Stage 1 issue is silently worked around.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md and oscillation reports do not exist for Stage 2.
