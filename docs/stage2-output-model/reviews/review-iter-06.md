# Review — iteration 06
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v05
Date: 2026-10-21

## Summary

v05 fixes the three remarks of iteration 05 correctly:

- **R05-01.** INV-105 now asks for the four measures of the covered period itself, and for a `fillsPeriod` series wherever the covered period contains a whole period. This is the INV-104 pattern, so an overview of any period, including the period since the previous consultation, can conform.
- **R05-02.** Score components are decided only on the pair of results that the criterion compares. These are the latest result after the treatment start within the last evaluated period (`evaluationResult`) and the latest result on or before the start (`pretreatmentBaseline`).
- **R05-03.** INV-089 relates the cluster attack rates to one whole number of attacks and the period length, and to the attack count where the view shows one.

The fixer's sweep changes are also sound: E-039, INV-049 and INV-050 for follow-up views that end between period boundaries; the treatment tie in `reductionMet`, `reductionDecided` and INV-064; and the new INV-062 conjunct.

The citation base is sound:

- all 65 Stage 2 quotes were found verbatim at their stated locations and URLs;
- the metadata of S-101 to S-105 is correct;
- ICHD-3 (2018) and NICE CG150 (last updated 3 June 2025) are still current.

The mechanical checks are clean, the scope sweep found no input, storage or derivation-from-input content, and section 8 is founded.

One defect remains (R06-01). The eleven evaluation rules of E-041 come from migraine guidance, two of them from guidance for adults only. The model nevertheless applies them, at MUST (INV-055, INV-059), to every preventive treatment of every subject:

- a preventive treatment of cluster headache or tension-type headache;
- a child's treatment.

So a conformant output must show, for example for verapamil in cluster headache, a time point labelled "NICE CG150 rec. 1.3.27", which NICE gives only for migraine prophylaxis. OUT-018 asks only for the time points "named in current guidance".

## Verification coverage

Downloads were made with `curl` into a fresh directory under `/tmp` (`/tmp/r06-dl-lY7S`), outside the repository. Scripts were kept in the session scratchpad and run with `python3 -I`.

- PDFs were extracted page by page with `pdftotext -raw` and `-layout`.
- Europe PMC full-text XML and the listed `pmc.ncbi.nlm.nih.gov` HTML pages were both tag-stripped and searched. Every PMC quote was found at both, so it can be read at the listed URL.
- Each quote was split at `[...]` and searched in three passes:
  1. exact, after collapsing whitespace;
  2. after normalising quotes, dashes, ligatures and line-end hyphens, and removing the ICHD-3 glyphs without a text mapping;
  3. alphanumeric only.
- Every pass-2 or pass-3 match was read in context. The only differences were:
  - line-end breaks ("non-/opioid", "pre-/ceding", "con-/sidered", "base-/line");
  - footnote markers ("opioids1", "medications1,2", "above,1");
  - the "ﬁ" ligature;
  - the unmapped ICHD-3 glyphs ("≥", "±", "−"; "+3" rendered "þ3");
  - "a≥30%" printed without a space in S-008;
  - the upper-case section heading of S-105.

### Citations

| Source | Where checked | Quotes checked | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|---|
| S-001 ICHD-3 (Stage 1 URL; HTTP 200, 211 pages) | pp. 8, 9, 12, 122–125, 190, 209; p. 139 for ISS-02 | 30:<br>• 15 code labels;<br>• 8.2, 8.2.1, 8.2.2 and 8.2.3 Descriptions;<br>• 8.2.4, 8.2.5, 8.2.6 and 8.2.8 criterion B;<br>• 8.2.6 note 2;<br>• the 8.2.3 comment, short (E-028) and full (INV-046);<br>• A1.1.1 and A1.1.2 criterion B, and A1.1.1 note 2;<br>• cluster remission | 30 | 0 | 0 |
| S-008 IHS 2024 (Stage 1 URL, univaq PDF; HTTP 200) | pp. 12, 13 | 4:<br>• the Q6 30 % alternative;<br>• the AHS MIDAS/HIT-6 definition;<br>• the Q6 judgement wording and the 50 % item used in `critIhsQ6` | 4 | 0 | 0 |
| S-010 IHS 2025 (Stage 1 URL, univaq PDF; HTTP 200) | p. 6 | 7:<br>• the four control levels;<br>• "In some cases";<br>• the definition-adoption sentence and the "proxy" sentence (E-018) | 7 | 0 | 0 |
| S-014 (Stage 1 source) | Europe PMC XML of PMC6734476 and the listed PMC page (HTTP 200) | 12:<br>• HALT-90 and HALT-30 recall;<br>• the "whole days" unit;<br>• Table 18: title, 3 headings, 4 rows;<br>• the HURT sentence (ISS-06) | 12 | 0 | 0 |
| S-007 (Stage 1 source; UCL Discovery PDF, HTTP 200, 39 pages) | pp. 10, 22, 25 | 3:<br>• the new E-064 fragment "≥ 14 attacks per week on average" (p. 10);<br>• the two Stage 1 fragments re-used in E-064 (pp. 22, 25) | 3 | 0 | 0 |
| S-101 Yang 2011 | Europe PMC XML and listed PMC page (HTTP 200) | 2 | 2 | 0 | 0 |
| S-102 Pavlović 2015 | Europe PMC XML and listed PMC page (HTTP 200) | 2 | 2 | 0 | 0 |
| S-103 PedMIDAS page | listed URL, HTTP 200; title "PedMIDAS Tool \| Headache Center"; footer "© 2026 Cincinnati Children's Hospital Medical Center" | 1 (lead sentence, section heading, 2 column headings, 4 rows) | 1 | 0 | 0 |
| S-104 Snaith 2003 | Europe PMC XML and listed PMC page (HTTP 200) | 1 | 1 | 0 | 0 |
| S-105 PHQ/GAD-7 instructions | listed PDF, HTTP 200, 9 pages; metadata author Kurt Kroenke, created 2010-06-22, modified 2014-04-16 | 3:<br>• PHQ-9 and GAD-7 ranges (P. 6/9, under "USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES");<br>• the developers sentence (P. 8/9) | 3 | 0 | 0 |
| **Total** | | **65** | **65** | **0** | **0** |

Further checks:

- **Other quoted strings.** All 378 double-quoted strings in sections 1–8 (outside the `omn` blocks) were compared by script:
  - 277 are verbatim substrings of Stage 1 v18;
  - 87 are verbatim in the downloaded sources;
  - 14 match after glyph and line-break normalisation;
  - 16 are the model's own terms or example wording ("K is available when C", "not reached", "total score, where the instrument defines one", and the like).
- **Stage 1 quotes re-checked at their sources.**
  - NICE CG150 (Stage 1 URL, HTTP 200, "Last updated: 03 June 2025"): recommendations 1.2.6, 1.3.27, 1.3.28, 1.3.29 and 1.3.48 read as modelled.
  - The Russian adult guideline (Stage 1 URL, HTTP 200 on the second attempt, 92 pages): section 7.1, p. 53, "через 3 месяца терапии" reads as quoted. The title page states "Возрастная категория: взрослые" (age category: adults; used in R06-01).
  - The AAN/AHS clinician summary (Stage 1 URL, HTTP 200): titled "Pharmacologic treatment for migraine prevention in adults practice guideline" (used in R06-01).
- **Metadata** (PubMed esummary), all correct:
  - S-101: Cephalalgia 2011;31(3):357–67, DOI 10.1177/0333102410379890, PMID 20819842, PMC3057423, authors as cited;
  - S-102: J Headache Pain 2015;16:24, DOI 10.1186/s10194-015-0503-y, PMID 25902814, PMC4406925, 7 authors as cited;
  - S-104: Health Qual Life Outcomes 2003;1:29, DOI 10.1186/1477-7525-1-29, PMID 12914662, PMC183845;
  - S-103 developer paper: Neurology 2001;57(11):2034–9, DOI 10.1212/wnl.57.11.2034, PMID 11739822.
- **Newer versions.**
  - Web search shows only "ICHD-4 – Work in Progress 1" and the IHS September 2025 classification workshop report (posted January 2026); no ICHD-4 has been published.
  - NICE CG150 is unchanged since 3 June 2025.
- **Translations.** v05 adds no non-English quote. The Russian and Dutch fragments in E-041 and E-045 are parts of Stage 1 quotes, whose translations carry over.
- **Value sets re-checked against the downloaded texts**, all matching:
  - ICHD-3 labels and hierarchy; the 8.2 levels (15 for 8.2.3, 10 otherwise) and the "> 3 months" span (4 monthly periods by INV-045); `classesOf826`; the A1.1 window; the remission duration;
  - the HIT-6 range and bands; the MIDAS, PedMIDAS and HALT-90 bands and labels; the recall periods;
  - the HADS, PHQ-9 and GAD-7 ranges;
  - the IHS Q6 thresholds; the NICE, DMKG and Russian thresholds; the IHS 2025 control levels;
  - the eleven evaluation rules of E-041 against their Stage 1 quotes.

### Per-OUT fidelity check (Statement, Caveats, strength, traceability row)

| OUT | Result | OUT | Result |
|---|---|---|---|
| 001 | OK | 021 | OK |
| 002 | OK | 022 | OK (ISS-03) |
| 003 | OK (SHOULD / SHOULD NOT) | 023 | OK (INV-107) |
| 004 | OK | 024 | OK |
| 005 | OK | 025 | OK (MAY) |
| 006 | OK | 039 | OK |
| 007 | OK | 026 | OK (ISS-06) |
| 008 | OK (MAY; ISS-04) | 027 | OK |
| 009 | OK | 028 | OK (ISS-03) |
| 010 | OK | 029 | OK (ISS-09) |
| 011 | OK | 030 | OK |
| 012 | OK | 031 | OK (R05-03 fix verified) |
| 013 | OK (MAY) | 032 | OK |
| 014 | OK (ISS-02) | 033 | OK |
| 015 | OK | 034 | OK |
| 016 | OK (ISS-01, ISS-09) | 035 | OK (R05-01 fix verified) |
| 017 | OK (sweep change to E-039, INV-049, INV-050 verified) | 036 | OK, except the R06-01 age facet (adult guidance time points required for children and adolescents) |
| 018 | **R06-01**; otherwise OK | 037 | OK |
| 019 | OK (ISS-05) | 038 | OK |
| 020 | OK (R05-02 fix verified; ISS-08) | | |

**Conformance levels.** These were compared with the Stage 1 strength of the statement part each realises, for all 108 invariants and the attribute levels of every element:

- MUST 19: INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054–057, 059, 068, 086, 102, 108;
- MUST NOT 2: INV-048, 106;
- SHOULD NOT 8: INV-013, 021, 043, 065, 084, 091, 101, 107;
- SHOULD 47;
- definitional 32.

No mismatch was found, and every MUST NOT and SHOULD NOT predicate has the form `¬ F`. Every MUST attribute belongs to an element that a MUST statement part requires (OUT-001, OUT-016, OUT-018, OUT-021, OUT-030).

### Mechanical checks (scripts in the session scratchpad: `quotes.py`, `allquotes.py`, `mech.py`, `names.py`)

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108); none missing, no duplicates |
| Dangling references | none<br>ISS headings: ISS-01–06, 08, 09; ISS-07 appears only in sections 8 (note), 9 and 12<br>S references are within S-001–S-046 or S-101–S-105; OUT references are within 001–039 |
| Realises fields and traceability | every element and invariant has exactly one Realises field<br>39 rows, in Stage 1 order (OUT-039 after OUT-025)<br>0 differences between the rows and the union of the Realises fields<br>no coverage text names an E-/INV- ID outside its columns<br>39 × "full" (but see R06-01) |
| Names in `omn` blocks | 308 declared names; the only "duplicate" is a word inside a text literal<br>199 enumeration constants and variant tags<br>every attribute selection `.a` is declared on some type<br>after removing declared names, attributes, tags, parameters and bound variables, only words inside text literals and `refs` (defined in section 2.5) remain |
| Typing rule for levels | 172 attribute declarations; no SHOULD, MAY or MUST-with-`when` attribute lacks an `opt`/`set`/`seq` type, and none uses `set1`/`seq1` |
| Partial terms in v05 changes (by hand) | `last(L.evaluated)`, `first(sr.periods)` only on `seq1`<br>`n ÷ p.lengthDays` with divisor in ℕ₁<br>`days` in `wholePeriodFrom` guarded by `d ≤ e`<br>`opt` attributes used only in quantifiers or `≠ ∅` |
| Scope sweep (enter, entry, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, reminder, field, obtained, calculated, computed, algorithm, "diary information", "diary data") | only:<br>• the exclusion statements (sections 1, 2.1, 2.7, 3.5);<br>• the out-of-scope notes of E-014, E-019, E-033, E-057 and INV-076;<br>• the omission notes of the [S-101] and [S-104] quotes;<br>• "records" inside the [S-014] HALT-30 quote;<br>• the meaning statements about "the summarised diary information" (E-013, E-060, E-064);<br>• "answered" in the INV-014 Reading;<br>• "Conformance field" |
| Thresholds, formulas, derived attributes | every relation takes output elements, context properties (section 3.5) or cited constants<br>every threshold, reference level, band and offset that the output shows is present and quoted<br>every derived attribute has its relation listed, or is noted as obtained from diary information |
| Satisfiability | No contradiction found in:<br>• INV-105 + INV-095 + INV-003 + INV-011 + INV-087 (43-day and 5-day covered periods);<br>• E-039 + INV-049 + INV-050 + INV-051 (follow-up views of 10, 40 and 70 days);<br>• E-046 + INV-062 + INV-063 + INV-064 (the R05-02 examples);<br>• INV-088 + INV-089 (10 attacks in 7 days; mixed migraine and cluster subject with `ofType(c3_1)` rates) |
| Snapshot | `cmp OUTPUT_MODEL.md history/v05.md`: identical; working tree clean before this review |

## Remarks

### R06-01 Infidelity (applicability condition): evaluation time points from migraine guidance, two of them from adult-only guidance, are required at MUST for preventive treatments of every headache type and every age group
- Item(s): E-041 (`EvaluationRule`, the `appliesTo` of the eleven rules, `applicable`, Meaning, Notes), E-008 (`SubjectProfile`), INV-001 (the fallback type), E-043 (`timePoints`), INV-055, INV-058, INV-059; section 7 rows OUT-018 and OUT-036
- Problem:
  - **What the model requires.**
    - `applicable(c, t, r)` holds for every preventive treatment t whose listed type is in `r.appliesTo` and that has the rule's anchor. Nothing in it refers to the headache type the treatment is for, or to the subject's age group.
    - By INV-001 every preventive treatment has a type, with `otherPreventive` as the fallback. So the rules with `appliesTo ↦ allPreventiveTypes` apply to every preventive treatment of every subject: `ruleNice1327`, `ruleAan14A` and `ruleRu71`. So do `ruleSignTitrated` and `ruleNvnTitrated` for any titrated preventive.
    - INV-059 (MUST) then requires every response comparison to show these time points, labelled with the guidance name. INV-055 (MUST) requires comparisons ending at them. E-043 `timePoints` is MUST under the same condition.
  - **What the guidance names.** All eleven rules come from guidance on migraine prevention, and two of them from guidance for adults only (evidence below):
    - NICE CG150 1.3.27 is a review of "migraine prophylaxis". It stands under the heading "Migraine with or without aura" > "Prophylactic treatment review". CG150's prophylaxis of cluster headache (1.3.39, verapamil) and of tension-type headache (1.3.9) name no review time point.
    - AAN/AHS 2026 14A concerns "medications for migraine prevention", in a guideline on "Migraine Prevention in Adults".
    - Russian section 7.1 concerns "профилактическое лечение М" (preventive treatment of migraine), in a guideline whose age category is adults. The model's own rule name says "(adults)".
    - SIGN 155, the EHF 2022 guideline, IHS 2024 and the NVN module are all migraine guidance by their titles.
  - **Stage 1.**
    - OUT-018 requires the comparison "at the evaluation time points named in current guidance, which differ by treatment type".
    - Stage 1 also covers preventive treatments of other headache types: OUT-009 (weekly values and treatment markers for "tension-type headache, cluster headache"), and OUT-031 with [S-014] ("optimum acute and preventative treatments are maintained" in cluster headache). The model itself names "a preventive treatment for tension-type headache" in ISS-03.
    - For children and adolescents, OUT-036 (d) refers to "paediatric guidance".
    - No guidance in the Stage 1 evidence names these migraine and adult time points for a cluster-headache or tension-type-headache preventive, or the adult-only ones for a child.
  - **Example: a cluster-headache preventive.**
    - An adult subject has episodic cluster headache only. Verapamil starts on 2 March 2026 (type `otherPreventive` by INV-001, or `doseTitratedPreventive`); the as-of date is 15 August 2026.
    - INV-059 (MUST): every response comparison for verapamil must show the time point "NICE CG150 rec. 1.3.27" (2 June to 2 September 2026) and the time point "Russian clinical recommendations «Мигрень» (adults) 2024, section 7.1" (2 June 2026). With a titrated type and a reached target dose, it must also show AAN/AHS 14A, SIGN 155 and NVN.
    - INV-055 (MUST): comparisons must end at those time points.
    - A diary that correctly shows the verapamil comparison without any migraine-guidance time point satisfies OUT-018 but violates two MUST invariants.
    - A diary that conforms must attribute to NICE 1.3.27 and to the Russian migraine guideline a time point they do not give for this treatment.
  - **Example: a child.** For a 10-year-old with migraine on a titrated preventive, INV-059 requires the "AAN/AHS 2026 rec. 14A" and "Russian clinical recommendations «Мигрень» (adults)" time points. Both come from guidance for adults.
  - **Which rule of section 9 this breaks.** The applicability condition of the evaluation rules is wrong. The MUST invariants exclude outputs that Stage 1 permits, and require attributions that the cited guidance does not support. PROCESS.md section 2: "A relation must be correct under the definitions the output names."
  - **Not a reversal of an earlier fix, and not a watch point.**
    - R01-02 asked that the type-independent rules not be met vacuously when a treatment has no type listing. Its required change, the INV-001 fallback type, can stay.
    - R01-02's premise, "NICE 1.3.27 applies to any prophylactic treatment", did not consider:
      - that 1.3.27 is a recommendation on migraine prophylaxis, in CG150's migraine section;
      - that the model admits preventive treatments of other headache types (ISS-03) and of children.
    - R01-01 asked for the NVN and Russian rules to be added. It did not concern their population.
    - None of the oscillation watch points (INV-087 and the lead-in; E-060, E-061, INV-105 as a whole; INV-104) is touched.
- Evidence:
  - E-041 (model):
    - `ruleNice1327 = EvaluationRule(guidance ↦ "NICE CG150 rec. 1.3.27", appliesTo ↦ allPreventiveTypes, …)`;
    - `ruleAan14A = EvaluationRule(guidance ↦ "AAN/AHS 2026 rec. 14A", appliesTo ↦ allPreventiveTypes, …)`;
    - `ruleRu71 = EvaluationRule(guidance ↦ "Russian clinical recommendations «Мигрень» (adults) 2024, section 7.1", appliesTo ↦ allPreventiveTypes, …)`;
    - `pred applicable(c, t, r) ≙ t ∈ c.subject.preventiveTreatments ∧ (∃ ty ∈ r.appliesTo • (t, ty) ∈ c.subject.preventiveTypes) ∧ anchorDates(c, t, r.anchor) ≠ ∅`.
  - E-041 Notes (model):
    - "\"most medications\" is modelled as applying to every preventive type";
    - "the recommendation concerns preventive treatment of migraine in general, so it applies to every preventive type";
    - "Every preventive treatment has at least one type (INV-001), so `applicable` holds for the rules of all preventive types whenever the treatment has the rule's anchor."
  - INV-001 (model): `(∀ t ∈ c.subject.preventiveTreatments • ∃ ty : PreventiveTreatmentType • (t, ty) ∈ c.subject.preventiveTypes)`.
  - INV-059 (model, MUST): `∀ r ∈ evaluationRules; a ∈ anchorDates(ctx, rc.treatment, r.anchor) • applicable(ctx, rc.treatment, r) ⇒ ∃ tp ∈ rc.timePoints • tp.rule = r ∧ tp.anchorDate = a`.
  - ISS-03 (model): "For a subject without migraine (for example a preventive treatment for tension-type headache), these outputs show migraine days that are all 0."
  - Stage 1 OUT-018 Statement: "The output MUST allow this comparison at the evaluation time points named in current guidance, which differ by treatment type".
  - Stage 1 OUT-036 Statement: "(d) present efficacy of treatment from diary data as recommended in paediatric guidance".
  - Stage 1 OUT-009 Statement: "Where weekly granularity is clinically relevant (tension-type headache, cluster headache, early onset of effect), weekly values SHOULD be available"; the same view carries "dated markers for the start, dose change and stop of preventive treatments".
  - Stage 1 quotes:
    - [S-015] "Review the need for continuing migraine prophylaxis 3 to 6 months after starting prophylactic treatment." (rec. 1.3.27);
    - [S-018] "14A. Clinicians should wait at least 8–12 weeks at the recommended tolerated dose of most medications for migraine prevention before assessing efficacy.";
    - [S-033] "Рекомендуется считать профилактическое лечение М эффективным, если число дней с ГБ сокращается через 3 месяца терапии [...]" (section 7.1). Translation in Stage 1: "It is recommended to consider preventive treatment of migraine effective [...]".
  - Stage 1 section 5 titles:
    - S-015 "Headaches in over 12s: diagnosis and management";
    - S-016 "SIGN 155: Pharmacological management of migraine";
    - S-018 "Pharmacologic treatment for migraine prevention in adults practice guideline";
    - S-033 "Клинические рекомендации «Мигрень» (взрослые)";
    - S-011 "… for migraine prevention – 2022 update";
    - S-008 "… for Preventive Pharmacological Treatment of Migraine";
    - S-028 module "Profylactische behandeling migraine".
  - Downloaded and checked for this review:
    - NICE CG150 recommendations page (https://www.nice.org.uk/guidance/cg150/chapter/Recommendations, HTTP 200, page title "Headaches in over 12s: diagnosis and management"):
      - 1.3.27 follows the headings "Migraine with or without aura" … "Prophylactic treatment review";
      - cluster prophylaxis: "1.3.39 Consider verapamil for prophylactic treatment during a bout of cluster headache.", with no review time point;
      - TTH prophylaxis: "1.3.9 Consider a course of up to 10 sessions of acupuncture over 5 to 8 weeks for the prophylactic treatment of chronic tension-type headache."
    - Russian guideline, title page (https://apicr.minzdrav.gov.ru/api.ashx?op=GetClinrecPdf&id=295_4): "Клинические рекомендации Мигрень […] Возрастная категория: взрослые" (age category: adults).
    - AAN/AHS clinician summary (https://www.aan.com/Guidelines/Home/GetGuidelineContent/1180): title "Pharmacologic treatment for migraine prevention in adults practice guideline"; "This is a summary of the American Academy of Neurology (AAN) guideline, “Pharmacologic Treatment for Migraine Prevention in Adults,”".
- Required change:
  - **Give each evaluation rule the population its guidance names, and require that population in `applicable`.** Both are properties of the rule and of the subject (section 3.5), not derivations from input. Options:
    - (a) **Precise.**
      - Add to `EvaluationRule` the headache type its guidance concerns. This is `c1` for all eleven rules, and allows a non-migraine rule to be added later.
      - Add the age groups it covers: `adult` only for `ruleAan14A` and `ruleRu71`. For the NICE rules, CG150 covers people over 12, which `AgeGroup` cannot separate from younger children; state the reading chosen.
      - Add to `SubjectProfile` the headache type(s) each preventive treatment is given for, as `preventiveTypes` is already a subject property.
      - `applicable` then requires that the treatment is given for a type `h` with `h ⊑` the rule's headache type, and that the subject's age group is covered.
    - (b) **Coarser.** Require `hasType(c, c1)` (or `mayHaveType(c, c1)`) and the age condition in `applicable`. State in the Notes that, for a subject with migraine and another headache type, the rules then also apply to a preventive treatment given for the other type.
  - **Keep the R01-02 guarantee.** For every preventive treatment within a rule's population, the rules of all preventive types still apply whatever the type listing (INV-001's fallback type stays).
  - **If the author holds that OUT-018 requires guidance time points for these treatments too,** they must come from guidance that names them for those treatments. The Stage 1 evidence contains none, so the gap belongs in section 8 as a Stage 1 issue, with this evidence. It must not be filled by attributing migraine or adult guidance to them.
  - **Text.** Update:
    - the E-041 Meaning and Notes: replace "applies to every preventive type", which conflates the guidance type of a drug with the headache disorder and population the guidance addresses;
    - the E-008 Meaning and Notes;
    - the INV-055, INV-058 and INV-059 Readings;
    - section 7 rows OUT-018 and OUT-036.

## Checked and not raised

- **v05 fixes (R05-01 to R05-03) and the sweep.**
  - **INV-105.**
    - The 43-day example has a 28-day or weekly `fillsPeriod` series, and the covered-period values are always required.
    - `fillsPeriod` still excludes a one-period series of a long covered period (the R03-04 guarantee).
    - The cycle-line and treatment-effect conjuncts are unchanged (watch point 1).
  - **`evaluationResult` and `pretreatmentBaseline`.**
    - They take only output elements and the subject's available results.
    - In iteration 05 example 1 the pre-treatment pair now decides nothing; in example 2 the 1 July / 25 March pair is decided and met.
    - INV-063 only became weaker, and its two forcing antecedents remain exclusive.
  - **INV-089.**
    - The new relation compares output elements only.
    - The `concerns` conjunct is met by `ofType(c3_1)` rates for mixed subjects, which INV-028 can accompany with counts of the same scope.
  - **INV-064.** The new tie to the start of the label's treatment is met by on-treatment months (INV-056).
- **E-039 `reviewWindow`.**
  - It is `SHOULD` without a `when` clause, while INV-050 requires it only once the covered period reaches its end. So a short follow-up view SHOULD still show the (future) review window.
  - This does not contradict INV-050, INV-003 or INV-051, and it matches OUT-017 ("including the review window 4 to 8 weeks after the start of withdrawal"). Unchanged since v00.
- **Rule U1 (section 2.7)** carries no conformance level. Every Stage 1 unit property is carried by the element types and their unit comments (for example "expressed in days per period", OUT-027), so no observable property is lost.
- **`⊑` and codes not declared as constants.** ICHD-3 codes such as 1.1 are not declared as constants, and the hierarchy axioms list only the constants used. `⊑` is a given function whose meaning is stated by its comment (the ICHD-3 code hierarchy), like `classOf` and `label`. Earlier reviews accepted this, and no Stage 1 property depends on an undeclared code.
- **Wording in section 3.3 and section 10.**
  - "supports but does not replace clinical assessment and diagnosis" in section 3.3 is a conjugated example of the OUT-038 wording, not a cited quote.
  - "Pavlovic" in S-102 lacks the diacritic of PubMed's "Pavlović"; this is not wrong metadata.
- **INV-040 / INV-041.** With 28-day periods, the "most recent" series may end up to 27 days before the as-of date, as with calendar months, where up to 30 days may be left out. Stage 1 fixes no grid for 28-day periods.
- **Co-presence through INV-003.** Period atoms are items and belong to exactly one view, so a value or basis that shares a period with a response comparison or an overuse indicator is in the same view. This confirms review 03.
- **Section 8.**
  - ISS-01 to ISS-06, ISS-08 and ISS-09 are founded, and each is pointed to from the elements it affects.
  - ISS-02 was re-verified: the only "simple analgesics" in ICHD-3 is on p. 139 (10.1.1).
  - R06-01 is a defect of the model's rule applicability, not a Stage 1 issue, unless the author takes the last option of its required change.
- **Earlier decisions not reopened (no new evidence):**
  - INV-106 at MUST NOT;
  - the AAN/AHS 14A and NVN window readings;
  - INV-023 at any granularity;
  - the "> 3 months" reading of INV-045;
  - the MIDAS label choice;
  - the 24-hour outcomes for cluster summaries;
  - "history of previous bouts";
  - the OUT-031 end-of-bout Caveat;
  - the context as subject properties, including `ihsQ6ChronicAlternative`;
  - the HIT-6 one-month recall;
  - the cluster remission "> 3 months";
  - labels under a criterion that does not apply;
  - the E-060 lead-in wording.

  R06-01 does not reopen the AAN/AHS 14A window reading; it concerns only whom the rule applies to.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and the oscillation check after iteration 04 froze nothing.
