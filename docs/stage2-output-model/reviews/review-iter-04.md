# Review — iteration 04
VERDICT: REMARKS
REMARK_COUNT: 4
Reviewed version: v03
Date: 2026-10-21

## Summary

v03 fixes the seven remarks of iteration 03 correctly:

- INV-046 now matches ICHD-3 8.2.6 and the 8.2.3 comment;
- the cycles of the menstrual-relation view can no longer be chosen arbitrarily;
- attack marks near an unshown next menstruation are marked correctly;
- the clinician-facing summary's time course is tied to its covered period;
- the paediatric equal-length rule covers every comparison;
- the instrument set is open;
- the PGIC grading is no longer asserted.

The citation base is sound:

- all 59 Stage 2 quotes were found verbatim at their stated locations and URLs;
- the metadata of S-101 to S-105 is correct;
- ICHD-3 (2018) and NICE CG150 (last updated 3 June 2025) are still current.

The mechanical checks are clean (IDs, references, traceability against the Realises fields, declared names, typing rule for levels, level counts), and the scope sweep found no input, storage or derivation-from-input content.

Four defects remain:

- **Menstrual-relation view, start (R04-01).** INV-087 (new in v03) makes every menstrual-relation view begin with a cycle whose first day of menstruation lies on or before the first day of the covered period. When no such day exists (menarche inside the covered period) or the output cannot show it, the MUST of INV-086 can be met only by a view that states a false date. Stage 1 permits the truthful view.
- **OUT-001 strength (R04-02).** OUT-001's MUST that frequency outputs be available per calendar month or 28-day period is realised only at SHOULD for moderate/severe headache days and attacks (INV-016, INV-017). The model itself applies this MUST "where provided" only for subjects with two or more headache types (INV-028).
- **IHS 2025 count (R04-03).** INV-031 ties the count on which the IHS 2025 control levels rest to migraine days under whatever definition the view names. [S-010] defines its own migraine day, and other published definitions count different days, so the relation excludes correct outputs.
- **Menstrual-relation view, end (R04-04).** For the last cycle of a view that has ended, days −2 and −1 of the next menstruation are not shown as perimenstrual for migraine days. v03 fixed this only for attack marks.

Section 8 is founded, and no Stage 1 issue is silently worked around.

## Verification coverage

Downloads were made with `curl` into a fresh directory under `/tmp` (`/tmp/r04-dl-9656`), outside the repository. Scripts were kept in the session scratchpad and run with `python3 -I`.

- **Text extraction.** PDFs were extracted page by page with `pdftotext`, in `-raw` and `-layout` modes, and each quote was searched on its stated page. XML and HTML were tag-stripped.
- **Quote passes.** Each quote was split at `[...]` and checked in three passes:
  1. exact, after collapsing whitespace;
  2. after normalising quotes, dashes and ligatures and removing the glyphs ≥ ± − + > <;
  3. alphanumeric only.
- **Inspection.** Every pass-2 or pass-3 match was inspected in context. The only differences were:
  - line-end breaks ("non-/opioid", "there-/fore", "analge-/sic", "head-/ache", "con-/sidered");
  - footnote markers ("opioids1", "medications1,2", "above,1");
  - the "ﬁ" ligature;
  - the ICHD-3 glyphs without a text mapping ("≥", "±", "−", "+" rendered as "þ");
  - in S-008, "a≥30%" printed without spaces.

### Citations

| Source | Where checked | Quotes checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|---|
| S-001 ICHD-3 (Stage 1 URL; HTTP 200, 211 pages; PDF page = printed page) | pp. 8, 9, 12, 122–125, 190, 209 | 30:<br>• 15 code labels (pp. 8, 9, 12);<br>• 8.2, 8.2.1, 8.2.2 and 8.2.3 Descriptions;<br>• 8.2.4, 8.2.5, 8.2.6 and 8.2.8 criterion B;<br>• 8.2.6 note 2;<br>• the 8.2.3 comment, both the short quote (E-028) and the full quote (INV-046);<br>• A1.1.1 and A1.1.2 criterion B, and A1.1.1 note 2;<br>• cluster remission (p. 209) | 30 | 0 | 0 |
| S-008 IHS 2024 (Stage 1 URL, univaq PDF; HTTP 200) | pp. 12, 13 | 3: the Q6 30 % alternative, the AHS MIDAS/HIT-6 definition, the PGIC wording of `critIhsQ6` | 3 | 0 | 0 |
| S-010 IHS 2025 (Stage 1 URL, univaq PDF; HTTP 200) | p. 6 | 5: the four control levels and the "In some cases" sentence | 5 | 0 | 0 |
| S-014 (Stage 1 source) | Europe PMC XML of PMC6734476 and the listed PMC URL (HTTP 200, article text) | 12:<br>• HALT-90 and HALT-30 recall;<br>• the "whole days" unit;<br>• Table 18: title, 3 headings, 4 rows;<br>• the HURT sentence (ISS-06) | 12 (at both URLs) | 0 | 0 |
| S-101 Yang 2011 | Europe PMC XML and the listed PMC URL (HTTP 200) | 2 | 2 | 0 | 0 |
| S-102 Pavlović 2015 | Europe PMC XML and the listed PMC URL (HTTP 200) | 2 | 2 | 0 | 0 |
| S-103 PedMIDAS page | listed URL, HTTP 200, title "PedMIDAS Tool \| Headache Center", footer "2026 Cincinnati Children's" | 1 (lead sentence, section heading, 2 column headings, 4 rows) | 1 | 0 | 0 |
| S-104 Snaith 2003 | Europe PMC XML and the listed PMC URL (HTTP 200) | 1 | 1 | 0 | 0 |
| S-105 PHQ/GAD-7 instructions | listed PDF, HTTP 200, 9 pages; metadata author Kurt Kroenke, created 2010-06-22, modified 2014-04-16 | 3: PHQ-9 and GAD-7 ranges (P.6/9), developers sentence (P.8/9) | 3 | 0 | 0 |
| **Total** | | **59** | **59** | **0** | **0** |

- **Metadata** (PubMed esummary), all correct:
  - S-101: Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMID 20819842, PMC3057423.
  - S-102: J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMID 25902814, PMC4406925; 7 authors.
  - S-104: Health Qual Life Outcomes 2003;1:29, DOI 10.1186/1477-7525-1-29, PMID 12914662, PMC183845.
  - S-103 developer paper: Neurology 2001;57(11):2034–9, DOI 10.1212/wnl.57.11.2034, PMID 11739822.
- **Newer versions.**
  - Web search and the IHS classification committee page list only "ICHD-4 – Work in Progress 1" (Cephalalgia 2024) and an ICHD-IV workshop (September 2025). No published ICHD-4 exists.
  - The NICE CG150 page (Stage 1 URL, HTTP 200) shows "Last updated: 03 June 2025". Recommendations 1.3.28, 1.3.29 and 1.3.48 read as modelled.
- **Translations.** No new non-English quote in v03.
- **New evidence used in this review** (verified verbatim the same way):
  - [S-010] p. 6, the three migraine-day definitions;
  - [S-002] (Stage 1 URL, ihs-headache.org PDF, HTTP 200) section 1.3.1.1, p. 1035;
  - [S-001] 1.1 criteria C and D, p. 19.

### Per-OUT fidelity check (Statement, Caveats, strength, traceability row)

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | **R04-02** | 021 | OK |
| 002 | OK | 022 | OK (ISS-03) |
| 003 | OK (SHOULD / SHOULD NOT) | 023 | OK |
| 004 | OK | 024 | OK |
| 005 | OK | 025 | OK (MAY) |
| 006 | **R04-02**; **R04-03** (INV-031) | 039 | OK |
| 007 | **R04-02** | 026 | OK (open instrument set; ISS-06 founded) |
| 008 | OK (MAY; see R04-02 on the reading of "frequency outputs") | 027 | OK |
| 009 | OK | 028 | OK (ISS-03) |
| 010 | OK | 029 | OK (ISS-09) |
| 011 | OK | 030 | **R04-01**, **R04-04** |
| 012 | OK | 031 | OK |
| 013 | OK (MAY) | 032 | OK |
| 014 | OK | 033 | OK |
| 015 | OK | 034 | OK (R03-04 fix verified) |
| 016 | OK (INV-046 verified against ICHD-3 8.2.3 comment, 8.2.6 B and note 2; ISS-01, ISS-09) | 035 | OK at SHOULD; the overview's cycle lines share R04-01 and R04-04 |
| 017 | OK | 036 | OK (R03-05 fix verified) |
| 018 | OK | 037 | OK |
| 019 | OK (ISS-05) | 038 | OK |
| 020 | **R04-03**; otherwise OK (ISS-08) | | |

Conformance levels were compared with the Stage 1 strength of the statement part each realises, for all 107 invariants and the attribute levels of every element:

- MUST 18: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054–057, 059, 068, 086, 102;
- MUST NOT 2: INV-048, 106;
- SHOULD NOT 8: INV-013, 021, 043, 065, 084, 091, 101, 107;
- SHOULD 47;
- definitional 32.

The only mismatch found is R04-02. Every MUST NOT and SHOULD NOT predicate has the form `¬ F`.

### Mechanical checks (scripts in the session scratchpad)

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 107 invariants (INV-001–INV-107); consecutive, no duplicates |
| Dangling references | none<br>ISS headings: ISS-01–06, 08, 09; ISS-07 appears only in sections 8 (note), 9 and 12<br>S references are within S-001–S-046 or S-101–S-105; OUT references are within 001–039 |
| Realises fields and traceability | every item has exactly one Realises field<br>39 rows, in Stage 1 order (OUT-039 after OUT-025)<br>0 differences between the rows and the union of the Realises fields<br>no row text names an ID outside its columns<br>39 × "full" (but see R04-01 to R04-04) |
| Names in `omn` blocks | 302 declared names, none declared twice<br>199 enumeration constants and variant tags, no duplicates<br>after removing declared names, attributes, tags and bound variables, only `ℙ` (section 2.4), `refs` (section 2.5) and the `_` of `_⊑_` remain |
| Typing rule for levels | 170 attribute declarations; no SHOULD, MAY or MUST-with-`when` attribute lacks an `opt`/`set`/`seq` type, and none uses `set1`/`seq1` |
| Partial terms in v03 changes (by hand) | `i₂.basis(j)` guarded by `j ∈ dom i₂.basis`<br>`first`/`last` only on `seq1` (`sr.periods`, `v.cycles`, `v.series.periods`)<br>`days` inside `ofKind` guarded by `d₁ ≤ d₂`<br>`min` on the `set1` `menstruationDays`<br>`classOf` guarded by INV-001 |
| Scope sweep (enter, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, entry, reminder, field, obtained, calculated, computed, algorithm) | only the exclusion statements (sections 1, 2.1, 2.7, 3.5), the out-of-scope Notes of E-014, E-057 and INV-076, the omission notes of the [S-101] and [S-104] quotes ("the omitted words describe how the score is obtained"), the [S-014] HALT-30 recall quote (used for the recall value), "answered" in the INV-014 Reading, and "Conformance field" |
| Thresholds, formulas, derived attributes | every relation takes output elements, context properties (section 3.5) or cited constants<br>every threshold and formula of a named standard or instrument that the output shows is present<br>one relation is not correct under the definitions the output names (R04-03) |
| Satisfiability | no contradiction found in:<br>• INV-044 + INV-045 + INV-046 + INV-003;<br>• INV-094 + INV-104 + INV-045 + INV-011;<br>• INV-097 + INV-055 + INV-056 + INV-068 + INV-070;<br>• INV-081 + INV-082 + INV-069;<br>• INV-086 + INV-087 + INV-105 for contexts in which a menstruation day precedes the covered period.<br>R04-01 is the exception: in other admissible contexts, INV-086 and INV-087 hold only for a view that shows a false date. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v03.md`: identical |

## Remarks

### R04-01 Formal defect: every menstrual-relation view must begin with a cycle whose first day of menstruation lies on or before the first day of the covered period, which a correct output often cannot show
- Item(s): INV-087 (conjunct `first(v.cycles).cycle.from ≤ v.covers.start`), E-060 (`menstruationDays`, `firstDayOfMenstruation`, Notes), E-061, INV-086; INV-105 (SHOULD); section 7 rows OUT-030 and OUT-035
- Problem:
  - **What the model requires.**
    - INV-086 (MUST) requires a menstrual-relation view whose covered period is the selected time range. This holds for every admissible context of a subject who menstruates, and any time range of whole periods ending by the as-of date is admissible.
    - INV-087 (definitional) requires that the first cycle shown begins on or before `v.covers.start`, a conjunct added in v03 (R03-02).
    - Every cycle line begins on its first day of menstruation, the earliest of its shown menstruation days: `cl.firstDayOfMenstruation = cl.cycle.from`, `= min cl.menstruationDays`, with `menstruationDays : set1 Date MUST`.
    - So every such view must show a first day of menstruation on or before the first day of the covered period.
  - **When that day does not exist.** OUT-030 applies to all "patients who menstruate", and OUT-036 covers adolescents.
    - Example: an adolescent's first menstruation (menarche) is on 10 March; the as-of date is 5 July and the selected time range is January to June.
    - No cycle is in progress on 1 January.
    - A truthful view shows the cycles from 10 March, states the number of complete cycles among them, and shows 1 January to 9 March without a cycle.
    - The model admits no such view. Every view it admits states a first day of menstruation on or before 1 January that did not occur.
    - So the MUST of INV-086 can be met only by a false date.
  - **When the output cannot show that day.** The same holds for a covered period that begins before the first menstruation the output can show, for example the first months of diary use, or a time range chosen before them.
    - Day counts have a representation of missing information: a lower count, with the completeness indicator (E-013; E-032 Notes, "a missing diary day can only make the shown count lower").
    - A cycle line has none: it must show a date.
    - PROCESS.md section 2: "A relation must be correct under the definitions the output names: for example, it must not assume something about missing diary days that the definitions do not state."
  - **Stage 1 permits the truthful view.** OUT-030 asks to show attacks and migraine days "in relation to the days of menstruation across consecutive cycles" and to "state how many complete cycles the view covers". It does not require every day of the covered period to lie in a cycle. So INV-087 excludes an output that Stage 1 permits (PROCESS.md section 9).
  - **Why the earlier fix missed it.** fix-iter-03 (R03-02) assumed that "the first cycle shown is the one in progress on the first day of the covered period". In these cases that cycle does not exist or cannot be shown.
  - **The overview has the same defect at SHOULD.** INV-105 requires an overlapping cycle line in any patient-facing overview of a subject who menstruates, for example an overview of a week before menarche.
- Evidence:
  - INV-087: `∀ cl : CycleLine • … cl.firstDayOfMenstruation = cl.cycle.from ∧ cl.firstDayOfMenstruation = min cl.menstruationDays …` and `first(v.cycles).cycle.from ≤ v.covers.start ∧ v.covers.end ≤ last(v.cycles).cycle.to`.
  - E-060: `cycles : seq1 →CycleLine core`; `menstruationDays : set1 Date MUST`.
  - INV-086: `∀ c ∈ Ctx • c.subject.menstruates ⇒ … sameSpan(v.covers, c.timeRange)`.
  - E-060 Notes: "the first is the cycle in progress on the first day of the covered period, which may have begun before it".
  - Stage 1 OUT-030 Statement (quoted above); OUT-036 "For children and adolescents"; OUT-003 Rationale "Missing diary days bias frequency measures".
- Required change:
  - **Goal.** Admit a menstrual-relation view whose first days precede the first day of menstruation it shows, without reintroducing the R03-02 defect (cycles chosen at will). Options:
    - (a) **Lead-in element.** An explicit element of the view, for example `leadIn : opt DateSpan`.
      - It runs from `v.covers.start` to the day before `first(v.cycles).cycle.from`.
      - Its meaning: no first day of menstruation is shown in it. It is not a cycle and is not counted in `completeCycles`.
      - INV-087 then requires either `first(v.cycles).cycle.from ≤ v.covers.start` or such a lead-in.
      - State how attacks with onset in the lead-in are shown. The attachment rule `∃₁ cl` must admit them, and days −2 and −1 of the first day 1 shown lie in the lead-in and are window days.
    - (b) **First cycle line without a shown day 1.** This mirrors the unfinished last cycle: it is shown from `v.covers.start`, has no day 1 and no window of its own, and is never counted.
  - **Overview.** Apply the same change to the cycle line required by INV-105, or condition that requirement on a cycle that can be shown.
  - **Text.** Update the E-060 and E-061 Notes and the OUT-030 and OUT-035 rows.

### R04-02 Infidelity (conformance level): OUT-001's MUST that frequency outputs be available per calendar month or 28-day period is realised only at SHOULD for moderate/severe headache days and attacks
- Item(s): INV-016, INV-017, E-017, E-019, section 3.4 (last paragraph); section 7 rows OUT-001, OUT-006, OUT-007
- Problem:
  - **The Stage 1 parts.**
    - OUT-001 (MUST) states: "Frequency outputs MUST be available per calendar month or per 28-day (4-week) period".
    - Stage 1 names OUT-004 to OUT-007 as the frequency measures (OUT-009: "frequency measures (OUT-004 to OUT-007)").
    - Providing moderate/severe headache days (OUT-006) and attacks (OUT-007) is SHOULD. Once they are provided, OUT-001 makes their availability per calendar month or 28-day period MUST.
  - **The model.** It states this monthly requirement for these two measures only in INV-016 and INV-017, at SHOULD, merging the MUST part of OUT-001 into the SHOULD of OUT-006 and OUT-007.
  - **Consequence.** A diary that provides moderate/severe headache days or attack counts only per calendar week, or only for selected spans, breaches a MUST of Stage 1. Under the model it is still MUST-conformant, because it deviates only from a SHOULD.
  - **The model is inconsistent.** It already applies this MUST "where provided" elsewhere:
    - INV-028 (MUST) requires monthly moderate/severe headache days and attacks, including the combined scope `allTypes`, "where the diary provides them";
    - INV-057 (MUST) requires them in every response comparison where reported.
    - But INV-028 applies only to subjects with two or more possible headache types. For a subject with one headache type, outside a response comparison, no MUST requires monthly availability of these outputs.
  - **The rule.** PROCESS.md section 4: "Each part of a Stage 1 Statement keeps its own strength."
- Evidence:
  - Stage 1 OUT-001 Statement (quoted above), Strength MUST; OUT-006 "SHOULD report the number of days with headache of moderate or severe intensity per reporting period"; OUT-007 "SHOULD report the number of attacks per reporting period"; OUT-009 "frequency measures (OUT-004 to OUT-007)".
  - INV-016 and INV-017: `∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ⇒ reportedPerPeriod(c, …, allTypes)`, Conformance SHOULD, Realises OUT-001 and OUT-006 / OUT-007.
  - INV-028 (MUST): `… ∪ {K ∈ {ModerateSevereHeadacheDays, AttackCount} | provides(K)}, sc)` under `#c.subject.possibleHeadacheTypes ≥ 2`.
- Required change:
  - **New MUST invariant** (a new ID), realising OUT-001 together with OUT-006 and OUT-007. Where the diary provides moderate/severe headache days or attack counts, they are available per calendar month or 28-day period for every period of the selected time range. Possible form: `∃ g ∈ MonthlyKind • ∀ c ∈ Ctx • c.granularity = g ⇒ ∀ K ∈ {ModerateSevereHeadacheDays, AttackCount} • provides(K) ⇒ reportedPerPeriod(c, K, allTypes)`, or one invariant per measure.
  - **Keep INV-016 and INV-017 at SHOULD** for providing these measures at all.
  - **Text.** Update the E-017 and E-019 Conformance and the OUT-001, OUT-006 and OUT-007 rows.
  - **OUT-008.** If the author reads "frequency outputs" as all Group B outputs, as ISS-04 reads OUT-034's "OUT-004 to OUT-009", apply the same to the OUT-008 measures where provided, and state that reading.

### R04-03 Formal defect: INV-031 relates the count of the IHS 2025 control levels to migraine days of any definition, although [S-010] bases that count on its own migraine-day definition
- Item(s): INV-031 (conjunct on `migraineOrModerateSevereHeadacheDays`), E-018 (Meaning, Notes), E-016, E-011; section 7 rows OUT-006, OUT-008 and OUT-020
- Problem:
  - **The relation.** INV-031 (definitional) requires, in one view and for the same period and scope, `a ≤ u ∧ b ≤ u ∧ u ≤ a + b`, where:
    - a is the migraine-day count;
    - b is the moderate/severe-headache-day count;
    - u is the E-018 count, "the single count on which the control levels of the IHS position statement 2025 rest".
  - **Why it fails.** [S-010] rests that count on its own definition of a migraine day, quoted below. OUT-002 lets the view's migraine days follow any published definition, for example the IHS trial guideline [S-002], which OUT-002 names. The two definitions count different days:
    - **Counterexample 1 (`a ≤ u` fails).** A month whose only headache is mild, unilateral and pulsating, with nausea, lasts six hours and is untreated.
      - It meets ICHD-3 1.1 criteria C and D, so it is a migraine day under [S-002]: a = 1.
      - It is not a migraine day under [S-010], which needs "more than two of four characteristics" and "more than one" of the symptoms.
      - It is not a moderate/severe headache day: b = 0.
      - So u = 0 (migraine freedom under [S-010]), and INV-031 forbids showing these correct values together.
    - **Counterexample 2 (`u ≤ a + b` fails).** A month whose only event is a 20-minute visual aura without headache.
      - [S-010] definition 2 counts it: u = 1.
      - [S-002] does not, because it requires headache: a = 0.
      - It is not a headache day: b = 0.
  - **Why it matters in practice.** INV-062 places the count of each evaluated month in the label's view. That view also holds the response comparison, which shows migraine days for the same month and scope (INV-054, INV-056). So the relation constrains exactly the outputs that OUT-020 asks for.
  - **Inconsistent with the model's own statements.**
    - INV-031 Notes: "Migraine days are not related to headache days because published migraine-day definitions differ (OUT-002)."
    - Section 3.3(5) says that definitional invariants exclude only outputs that contradict the element's definition. Here they exclude correct outputs.
- Evidence:
  - [S-010] "The panel decided to adopt the following three definitions of a migraine day, as modified from van der Arend et al. (45), in subjects with a diagnosis of migraine:" followed by "A day with headache satisfying criteria (a) + (b)", "(a) matching more than two of four characteristics: unilateral, pulsating, moderate-to-severe pain, aggravated by or causing avoidance of routine physical activity;", "(b) during headache, more than one of the following: nausea and/or vomiting, photophobia and phonophobia.", "2. A day with a (visual) aura lasting 5–60 minutes." and "3. A day with headache for which a migraine-specific acute migraine medication or a usually effective acute migraine medication is taken." (section "Setting goals of migraine burden while on treatment", p. 6; https://ricerca.univaq.it/bitstream/11697/264025/1/sacco-et-al-2025-setting-higher-standards-for-migraine-prevention-a-position-statement-of-the-international-headache.pdf)
  - [S-002] "A migraine day is defined as a day with headache lasting at least 30 minutes without intake of analgesics and meeting ICHD-3 criteria for migraine or probable migraine (25)." (section 1.3.1.1, p. 1035; Stage 1 URL of S-002)
  - [S-001] "C. Headache has at least two of the following four characteristics:" and "D. During headache at least one of the following:" followed by "1. nausea and/or vomiting" (1.1 Migraine without aura, diagnostic criteria, p. 19)
  - Stage 1 OUT-002 Rationale: "There is no single universally adopted definition of a migraine day; different definitions give different numbers."
  - PROCESS.md section 2: "A relation must be correct under the definitions the output names".
- Required change: make the relation hold under the definitions that the output names. Options:
  - (a) **State the count's definition and restrict the relation.**
    - State in E-018 that its count follows the [S-010] definition of a migraine day, with that quote as new cited detail.
    - Apply the conjuncts of INV-031 that relate u to a only where the view's migraine-day definition label names that same definition. The same goes for b where the count's moderate/severe headache days are not those of the view.
  - (b) **Remove the conjuncts** that relate u to a and to a + b, and keep only relations that hold under every published definition.

  Update the E-018 Notes and the INV-031 Reading and Notes.

### R04-04 Coverage gap: for the last cycle of a view that has ended, days −2 and −1 of the next menstruation are not distinguished as perimenstrual for migraine days
- Item(s): E-060 (`perimenstrualWindow`, `migraineDays`, Notes), INV-087, E-067; section 7 rows OUT-030 and OUT-035
- Problem:
  - **How windows are shown.** A perimenstrual window is shown only as `perimenstrualWindow` of a cycle line, around that cycle's own day 1. The window of a menstruation begins two days before its day 1, in the previous cycle (INV-087 Notes).
  - **Consecutive cycles are covered.** When two consecutive cycles are shown, the window of the later one covers the last two days of the earlier one.
  - **The last cycle is not.** Take the last cycle of a view, when it has ended but the next cycle is not shown because the next menstruation begins after the covered period (the R03-03 case). Days −2 and −1 of that next menstruation lie in the covered period and in the shown cycle, but in no window that the view shows.
  - **What v03 fixed.** v03 corrected the attack marks for this case (second disjunct of the INV-087 in-window relation). Migraine days on these two days are still shown like any other day of the cycle.
  - **Example.**
    - The view covers 1–30 September; menstruation began on 3 September and 1 October; migraine days are 28, 29 and 30 September (attack onset 28 September, day −3).
    - The shown windows are 1–5 September (of 3 September) and that of the earlier cycle.
    - So the migraine days of 29 and 30 September, days −2 and −1 of the 1 October menstruation, are not distinguished. That menstruation's day 1 is an output fact, the day after the last day of a complete cycle line (E-060 Notes).
  - **Consequence.** OUT-030 (MUST) requires migraine days to be shown "in relation to the days of menstruation [...] distinguishing the perimenstrual window as defined in ICHD-3 appendix A1.1 [S-001] from other days of the cycle". For migraine days this property is not represented in this case. The same holds for cycle lines in the patient-facing overview (OUT-035, SHOULD). Both rows claim full coverage.
- Evidence:
  - Stage 1 OUT-030 Statement (quoted above).
  - [S-001] "The first day of menstruation is day 1 and the preceding day is day −1; there is no day 0." (A1.1.1 note 2, p. 190; quoted in E-060).
  - E-060: `perimenstrualWindow : DateSpan derived MUST -- ICHD-3 appendix A1.1: day 1 ± 2`, `migraineDays : set Date MUST`.
  - INV-087: the window is `DateSpan(from ↦ plusDays(cl.firstDayOfMenstruation, − windowDaysBefore), to ↦ plusDays(cl.firstDayOfMenstruation, windowDaysAfter))`, and the next menstruation's window is used only for attack marks (`cl.complete ∧ plusDays(cl.cycle.to, 1 − windowDaysBefore) ≤ a.onset`).
  - INV-087 Notes: "The window of a menstruation begins two days before its day 1, in the previous cycle."
- Required change: show the window days of the next menstruation for every cycle line that has ended. Options:
  - a derived attribute such as `nextWindowDays : opt DateSpan derived MUST when self.complete`, related in INV-087 by `nextWindowDays = {DateSpan(from ↦ plusDays(cycle.to, 1 − windowDaysBefore), to ↦ cycle.to)}`;
  - or a derived in-window mark for each migraine day of a cycle line, defined like the attack-mark relation.

  Update the E-060 Notes and the OUT-030 and OUT-035 rows.

## Checked and not raised

- **INV-046 (R03-01 fix).**
  - Both directions were checked against the verbatim ICHD-3 texts: 8.2.6 criterion B, 8.2.6 note 2 and 8.2.3 comment 2.
  - Single-class use, including several non-opioid analgesics, gives "not reached".
  - Two classes with days in every period of the span and no class at its own level give "reached".
  - The two directions are consistent.
  - `classShownUsed` and `classUseExcluded` take only output elements and context properties.
  - The ICHD-3 8.2.5 note 1 (combinations of two non-opioid analgesics are not combination analgesics) agrees with E-028.
- **INV-087 in-window relation (R03-03 fix).** `plusDays(cl.cycle.to, 1 − windowDaysBefore)` is day −2 of the next menstruation, and the first disjunct gives days +1 to +3. This is correct for attack marks. Its gaps are R04-01 (start) and R04-04 (migraine days).
- **INV-104 (R03-04 fix).**
  - `fillsPeriod` and `summaryTimeCourse` were checked: any covered period of at least 28 days is filled by consecutive 28-day periods, and one of 7 to 27 days by its whole weeks.
  - INV-003 places the overuse-indicator spans in the summary.
  - With calendar months, a 59-day covered period has one whole month. That is a property of calendar months, not a defect.
- **INV-097 (R03-05 fix)** is satisfiable with INV-055, INV-056, INV-068 and INV-070, as the fix log states.
- **`OtherInstrumentName` (R03-06 fix).**
  - The guard excludes only nine exact strings, so other spellings remain possible, for example "HALT" or "mTOQ", which Stage 1 itself uses.
  - The E-057 Meaning defines `otherInstrument(x)` as "any other validated impact, disability or quality-of-life instrument". So the Meaning fixes the semantics: a named instrument shown under another name is not an instance. Criteria that rest on MIDAS or HIT-6 use the tags in any case.
  - Not raised.
- **`publishedGrading(pgic)` left open (R03-07 fix)** is consistent with MSQ v2.1 and M-TOQ, and the E-057 Notes disclose it.
- **INV-050.** The covered period of the withdrawal view is tied to its series. With calendar months, INV-049 applies only when withdrawal starts on the first of a month; the 28-day and weekly contexts cover OUT-017.
- **Value sets** were checked again against the downloaded sources and match:
  - ICHD-3 labels and hierarchy; 8.2 levels (15 / 10) and the "> 3 months" span (4 periods by INV-045);
  - `classesOf826`; the A1.1 window; the remission duration;
  - HIT-6 range and bands; MIDAS, PedMIDAS and HALT-90 bands and labels;
  - HADS, PHQ-9 and GAD-7 ranges;
  - recall periods;
  - the IHS Q6, NICE, DMKG and Russian thresholds; the IHS 2025 control levels.
- **S-010 location note.** E-046 says that a running header interrupts the "Insufficient Control" sentence. In the `-raw` extraction the sentence is continuous, so the note describes only the `-layout` text layer. The quote is correct and the note is harmless.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the AAN/AHS 14A and NVN window readings;
  - INV-023 at any granularity, where acute-medication days are not frequency outputs (review 01), which is consistent with R04-02;
  - the "> 3 months" reading of INV-045;
  - the MIDAS label choice;
  - the 24-hour outcomes for cluster summaries;
  - "history of previous bouts";
  - the context as subject properties;
  - the labels under a criterion that does not apply (review 02).
- **Section 8.**
  - ISS-01 to ISS-06, ISS-08 and ISS-09 are founded and are pointed to from the affected elements.
  - The ISS-06 extension to other instruments without a total score is founded.
  - R04-01 to R04-04 are defects of the model, not Stage 1 issues.
  - No Stage 1 issue is silently worked around.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md and oscillation reports do not exist for Stage 2.
