# Fix log — iteration 06
Input review: reviews/review-iter-06.md · Input version: v05 · Output version: v06
Date: 2026-10-21

## What was downloaded and checked

No FROZEN_ITEMS.md exists, and the oscillation check after iteration 04 froze nothing, so no item is frozen.

**Earlier work read so that no fix is undone.** PROCESS.md, Stage 1 v18 (sections 1–3 in full, section 5), v05 in full, the reviews and fix logs of iterations 01 to 05 and oscillation/check-after-iter-04.md were read.
- **Guarantees of R01-01, R01-02 and R02-01 (E-041, INV-001, INV-055) are kept.**
  - R01-01: the NVN and Russian rules stay in `evaluationRules`, with their offsets and anchors unchanged.
  - R01-02: INV-001 still requires a guidance type for every preventive treatment, with `otherPreventive` as the fallback. Within a rule's population, the rules for all preventive types still apply whatever the type listing. The new population condition cannot be met vacuously either: INV-001 now requires every preventive treatment to be given for at least one headache type.
  - R02-01: `fitsMonthlyPeriod`, the INV-055 guard and the INV-001 order of course events are unchanged.
- **Watch points of the oscillation check:** INV-087, the lead-in, E-060, E-061, INV-105 and INV-104 are not touched.
- **Settled points:** the "labels under a criterion that does not apply" decision (review 02) is not reopened (Other changes 1).

**Downloads.** All went with `curl` into a fresh directory under `/tmp` (`/tmp/fix06-dl-b5q8`), outside the repository. PDFs were extracted with `pdftotext -raw` and `-layout`; web pages and the Europe PMC XML had their markup removed. Scripts were kept in the session scratchpad and run with `python3 -I`.
- **[S-015] NICE CG150.**
  - Recommendations page (Stage 1 URL, HTTP 200):
    - 1.3.27–1.3.29 stand under "Migraine with or without aura" > "Prophylactic treatment review".
    - 1.3.24 and 1.3.26 recommend CGRP inhibitors and botulinum toxin type A "in adults".
    - Cluster headache prophylaxis (1.3.39, verapamil) and chronic tension-type headache prophylaxis (1.3.9, acupuncture) are recommended with no review time point.
    - 1.3.48 stands in the section on medication overuse headache.
  - Overview page https://www.nice.org.uk/guidance/cg150 (HTTP 200): "This guideline covers [...] in young people (aged 12 years and older) and adults."
- **[S-018] AAN/AHS 2026 Clinician Summary** (Stage 1 URL, HTTP 200; the URL returns a 12-page PDF).
  - The title is "Pharmacologic treatment for migraine prevention in adults practice guideline".
  - The first sentence names the guideline "Pharmacologic Treatment for Migraine Prevention in Adults".
  - 14A (p. 7) reads as quoted in Stage 1.
- **[S-016] SIGN 155** (Stage 1 URL, HTTP 200). Section 1.2.1 (PDF p. 7, printed p. 1):
  - "acute and prophylactic management of adults with migraine";
  - "Studies of children with migraine were not included, however the recommendations could be considered for treating adolescents with migraine."
- **[S-011] EHF 2022** (Europe PMC full text of PMC9188162 and the PMC page, HTTP 200).
  - The Background describes the 2019 guideline as one "for migraine prevention in adults" and says that "the EHF council decided to update the 2019 guideline".
  - Its PICO questions name "individuals with migraine", and question 3 names "individuals with episodic or chronic migraine". No age is stated.
- **[S-008] IHS 2024** (Stage 1 URL, univaq PDF, HTTP 200).
  - Q2 (p. 9) concerns "a migraine preventive treatment" and states no age.
  - Q13 (p. 17) addresses children and adolescents.
- **[S-028] NVN module** (Stage 1 URL, HTTP 200).
  - The PICO in "Zoeken en selecteren" reads "P: Patiënten (kinderen en volwassenen) met migraine, bij wie preventieve behandeling geïndiceerd is".
  - The Aanbeveling has titration schedules for children and for adults.
- **[S-033] Russian adult recommendations** (Stage 1 URL). The connection was reset twice; HTTP 200 on the third attempt, 92 pages.
  - Title page: "Возрастная категория: взрослые".
  - Abbreviations, p. 4: "М – мигрень".
  - Section 7.1 reads as quoted in Stage 1.
- **[S-034] Russian paediatric recommendations** (Stage 1 URL, HTTP 200).
  - Section 7.1 (p. 34) reads as quoted in Stage 1 OUT-036.
  - The flowchart of Приложение Б (p. 52) names a time point for preventive therapy of migraine in children: "Контроль эффективности терапии через 3мес." Stage 1 does not quote it (used in ISS-10).

**No web search and no new source.** All new quotes come from the Stage 1 sources S-008, S-011, S-015, S-016, S-018, S-028, S-033 and S-034, and are cited by their Stage 1 IDs.

**Verification of the remark before fixing. R06-01 holds, and is somewhat wider than stated.**
- **v05 behaviour.**
  - `applicable(c, t, r)` tested only the treatment's guidance type and anchor.
  - With the INV-001 fallback type, `ruleNice1327`, `ruleAan14A` and `ruleRu71` applied to every started preventive treatment of every subject, at MUST through INV-055, INV-059 and E-043 `timePoints`.
  - The review's verapamil example (cluster headache only) and its 10-year-old example were reproduced by script.
- **Guidance populations, from the downloaded texts:**
  - all eleven rules concern preventive treatment of migraine;
  - adults only: AAN/AHS 2026 and the Russian recommendations, as the review says, and also SIGN 155 ("adults with migraine") and the EHF 2022 guideline (the update of a guideline for adults);
  - NICE 1.3.28 and 1.3.29 are the stopping rules for treatments that NICE recommends "in adults" (1.3.24, 1.3.26);
  - NICE 1.3.27: CG150 covers people aged 12 years and older;
  - all ages: IHS 2024 (Q13 addresses children) and NVN ("kinderen en volwassenen").
- **Not a reversal.** R01-02 asked only that the rules not be met vacuously for lack of a type listing. Its INV-001 fallback is kept.

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R06-01 | fixed (the review's option (a), precise) | E-041 (new components `headacheType` and `ages`, new `AgeCoverage`, new `ageCovered` and `inPopulation`, `applicable`, all eleven rule constants, Meaning, Evidence, Notes); E-008 (new components `aged12OrOlder` and `preventiveFor`, Meaning, Evidence, Notes); INV-001 (three new conjuncts, Reading, Evidence, Notes); INV-055 (Reading, Evidence, Notes); INV-058 and INV-059 (Readings); E-042 and E-043 Notes; section 7 rows OUT-018 and OUT-036; section 8 new ISS-10 | **The population of each rule.** `EvaluationRule` has two new components:<br>• `headacheType`, the headache type whose preventive treatment the guidance concerns. It is `c1` for all eleven rules, from the Stage 1 quotes and titles ("migraine prophylaxis", "frequency of migraines", "medications for migraine prevention", "Pharmacological management of migraine", "individuals with episodic or chronic migraine", "Preventive Pharmacological Treatment of Migraine", "Profylactische behandeling migraine", "профилактическое лечение М").<br>• `ages : AgeCoverage`:<br>  – `anyAge`: IHS Q2 monthly and quarterly, and NVN;<br>  – `aged12AndOver`: NICE 1.3.27;<br>  – `adultsOnly`: NICE 1.3.28 and 1.3.29, AAN/AHS 14A, SIGN titrated and fixed-dose, EHF Q3, and Russian 7.1.<br>Each value is supported by a verbatim quote and location from the guidance itself (E-041 Evidence: [S-015] Overview, headings, 1.3.24 and 1.3.26; [S-018] p. 1; [S-016] 1.2.1; [S-011] Background; [S-008] Q2 and Q13 headings; [S-028] PICO; [S-033] title page).<br>**The subject.** E-008 has two new properties, of the subject and not derived from input (section 3.5):<br>• `preventiveFor : set (Treatment × HeadacheType)`, the headache type or types each preventive treatment is given for;<br>• `aged12OrOlder : 𝔹`. `AgeGroup` cannot separate the 12–17-year-olds whom NICE CG150 covers from younger children, so the review's "state the reading chosen" is replaced by a precise property.<br>**`applicable`** now also requires `inPopulation(c, t, r)`: the treatment is given for a headache type h with `h ⊑ r.headacheType`, and `ageCovered(c, r.ages)` holds.<br>**INV-001, three new conjuncts:**<br>• every `preventiveFor` pair names a preventive treatment and one of the subject's possible headache types;<br>• every preventive treatment is given for at least one headache type, so that the population condition cannot be met vacuously, the R01-02 point carried over;<br>• an adult is aged 12 or older.<br>**INV-055, INV-058, INV-059 and E-043 `timePoints`:** the predicates are unchanged. Through `applicable`, they now require or admit time points only within each rule's population.<br>**Review examples (script `applic.py`):**<br>• verapamil for cluster headache only: no rule applies, and the response comparison is still required (INV-055, first conjunct);<br>• a 10-year-old with migraine on a titrated preventive: NVN only;<br>• a 14-year-old: NVN and NICE 1.3.27;<br>• an adult with migraine: as in v05, as long as the treatment is given for migraine;<br>• a subject with migraine and TTH: amitriptyline given for TTH only gets none; given for both, it gets the migraine rules.<br>**SIGN 155 for adolescents** ("could be considered") is read as permitted, not named. It is therefore not required, and INV-058 does not admit it as an `EvaluationTimePoint`; a diary may show it as an `OtherItem` (E-041 Notes).<br>**Not filled by attribution.** For preventive treatments of other headache types, and for children outside the guidance ages, the Stage 1 evidence names no time point. The gap is recorded as ISS-10, with NICE 1.3.9 and 1.3.39 (prophylaxis with no review time point) and the [S-034] paediatric flowchart time point that Stage 1 does not quote. The rule list stays the Stage 1 evidence, so that time point is not added.<br>**Text.** E-041 Meaning and Notes no longer say "applies to every preventive type" for the headache disorder. They separate the type list (`appliesTo`) from the population of the guidance. Also updated: E-008 Meaning, Evidence and Notes; INV-055, INV-058 and INV-059 Readings; INV-055 Evidence and Notes; E-042 and E-043 Notes; rows OUT-018 and OUT-036. |

## Other changes

**1. Sweep for the same kind of defect** (a rule, criterion, threshold, value set or window taken from guidance for a specific headache type or age group, applied to every subject). Every constant and condition in the `omn` blocks that comes from a guidance or instrument was listed and checked.
- **Applied only to the population it comes from (no change):**
  - IHS cluster time point of 15 minutes, cluster remission > 3 months, cluster attack rates: `concerns(…, c3_1)` and `hasType(ctx, c3_1)` (INV-073, INV-088, INV-089);
  - migraine-associated symptoms: `hasType(ctx, c1)` (INV-022, INV-076);
  - composite indices and AUC: `concerns(…, c1)` and `concerns(…, c2)` (INV-091 to INV-093);
  - PedMIDAS and the paediatric caveat, equal lengths and intensity comparison: `childOrAdolescent` (INV-096 to INV-098, INV-039).
- **Instrument value sets** (MIDAS, HIT-6, PedMIDAS, HALT bands, ranges and recall; HADS, PHQ-9, GAD-7 ranges). They belong to the instrument, not to a population, and are required only where a result of that instrument is available (INV-081, INV-082, INV-083, INV-085). No guidance is attributed to the subject. No change.
- **Responder criteria and the IHS 2025 control levels.**
  - No invariant requires a responder label or a criterion for any subject. Labels are MAY, and a label names the criterion a reader chooses (OUT-018 Caveats).
  - Review 02 settled that labels under a criterion that does not apply are not a defect.
  - So the model attributes no criterion to a subject outside its population.
  - **E-045 Notes** now state this. They also state that a component condition (`anySubject` and the others) is a condition within the criterion's own population, which is migraine for all, and adults for `critRu71`.
  - No predicate changed.
- **Applied to every subject because Stage 1 says so (no model change):**
  - the ICHD-3 8.2 levels (ICHD-3 is not age- or type-limited);
  - the A1.1 window for patients who menstruate (OUT-030);
  - the ICHD-3 1.3 reference of the three-month view (OUT-028; ISS-03);
  - the 2-hour time point and the OUT-023 outcome measures for every non-cluster acute medication. OUT-023 names them "For each acute medication", with cluster headache as the only exception; the output names the measures, not a guidance; and the cluster 24-hour outcomes are a settled point.
- **One more case of this kind, in Stage 1 itself: new ISS-11.**
  - OUT-017 asks, "For patients withdrawing from overused medication", for "the review window 4 to 8 weeks after the start of withdrawal named in NICE CG150 recommendation 1.3.48". NICE CG150 covers "young people (aged 12 years and older) and adults".
  - The model follows Stage 1: the window is still SHOULD for every subject who is withdrawing (E-039, INV-050, INV-051). The issue is recorded for the human, with a pointer from the E-039 Notes and from row OUT-017.
- **OUT-025 scheme windows** are selected by the clinician and labelled with the scheme (MAY). No change.

**2. Satisfiability pass** over the changed invariants and attributes and those that constrain the same elements and views, against INV-001 and the context definitions.
- **INV-001.**
  - The three new conjuncts are satisfiable together with the others: let `preventiveFor` pair each preventive treatment with one of the subject's possible headache types, and set `aged12OrOlder` true for every adult.
  - They exclude two kinds of context: one in which a preventive treatment exists while the subject has no possible headache type, and one with an adult younger than 12. Both are incoherent.
  - Script check: an indication outside the possible types, a missing indication and an adult under 12 are each rejected; ten coherent contexts are accepted.
- **INV-055, INV-058, INV-059, E-042, E-043.**
  - `applicable` only became stronger. So the time-point clauses of INV-055 and INV-059 (MUST) and E-043 `timePoints` (MUST when) became weaker, and INV-058 (definitional) became stronger.
  - INV-058 admits exactly the time points of applicable rules, and INV-055 and INV-059 require only time points of applicable rules, so they cannot conflict.
  - Where no rule applies, `timePoints` is required to be empty by INV-058 and is not required by E-043.
  - The R02-01 argument for INV-055 + INV-056 + INV-097 is unchanged: for a time point that fits, a 28-day on-treatment period ends at it and a 28-day baseline period precedes the start.
- **INV-062 to INV-064, INV-066, INV-097, INV-104, INV-105, INV-027, INV-071** constrain the same response comparisons. None refers to time points or to `applicable`, so they are unaffected.
- **Derived attributes.** No new derived attribute. E-042 `earliest` and `latest` are still defined by `shift` wherever a time point exists.
- **Partial terms.** No new partial term: `⊑` is total, and the new terms are set memberships and Boolean properties.
- **Result:** no MUST or SHOULD invariants are jointly unsatisfiable in any admissible context, so no conflict needed fixing.

**3. Text and bookkeeping.**
- Header "Version: v06 · Iteration: 06 · Status: under review".
- Section 9 "as of v06".
- Section 11: an iteration 06 paragraph (downloads, no web search).
- Section 12: the v06 entry.
- Section 10 is unchanged (no new source).
- Section 7: rows OUT-017, OUT-018 and OUT-036 updated. The element and invariant columns are unchanged, because no Realises field changed.
- Three words in new text were reworded to keep the scope grep clean: "algorithm" (twice, for the [S-034] flowchart) and "obtained" (a download).

## Checks

Scripts in the session scratchpad (`mech.py`, `names.py`, `levels.py`, `quotes.py`, `applic.py`) were run on the final OUTPUT_MODEL.md.

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108); every ID present once, no duplicates, none withdrawn. |
| References | no dangling E-/INV- reference<br>ISS headings: ISS-01–06, ISS-08–ISS-11; ISS-07 appears only in the section 8 note, the section 9 table and the change log<br>S references are within S-001–S-046 or S-101–S-105<br>OUT references are within 001–039 |
| Realises and traceability | every element and invariant has exactly one Realises field<br>39 rows, in Stage 1 order (OUT-039 after OUT-025)<br>0 differences between the rows and the union of the Realises fields<br>no coverage text names an E-/INV- ID outside its columns<br>39 × "full" |
| Names and types in `omn` blocks | 304 declared names (v05: 301; new: `AgeCoverage`, `ageCovered`, `inPopulation`), none declared twice<br>202 enumeration constants and variant tags (v05: 199; new: `anyAge`, `aged12AndOver`, `adultsOnly`), no duplicates and no clash with declared names<br>187 distinct attribute and component names (v05: 183; new: `headacheType`, `ages`, `preventiveFor`, `aged12OrOlder`)<br>0 unresolved identifiers; every attribute selection is declared on some type<br>every rule constant lists all eight `EvaluationRule` components<br>types used in the new terms are declared: `HeadacheType`, `AgeCoverage`, `EvaluationRule`, `Treatment`, `OutputContext`, `AgeGroup`, 𝔹 |
| Typing rule for levels | 166 attribute declarations with a level, as in v05; no violation. The new components belong to value types and carry no level. |
| Conformance levels | MUST 19 (INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054–057, 059, 068, 086, 102, 108)<br>MUST NOT 2 (INV-048, 106)<br>SHOULD NOT 8 (INV-013, 021, 043, 065, 084, 091, 101, 107)<br>SHOULD 47; definitional 32; total 108<br>no level or scope changed; every MUST NOT and SHOULD NOT predicate has the form `¬ F` |
| Quotes | 54 double-quoted strings are new outside the `omn` blocks:<br>• 49 found verbatim in Stage 1 v18, in v05 or in the downloaded source texts (whitespace and non-breaking spaces normalised);<br>• 3 are translations;<br>• "Overall objectives" is the SIGN 155 section heading, printed in upper case;<br>• the NICE 1.3.9 sentence matches up to the final period, which follows a link in the HTML (`headache</a>.`). |
| Scope sweep (enter, entry, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, reminder, field, obtained, calculated, computed, algorithm, "diary information", "diary data") | 81 occurrences (v05: 80). The one new occurrence is "diary data" inside the Stage 1 OUT-036 (d) quote in ISS-10 ("present efficacy of treatment from diary data as recommended in paediatric guidance").<br>No input entity, storage term or derivation from input was added. The new properties (`preventiveFor`, `aged12OrOlder`) are subject properties (section 3.5), and `inPopulation` and `ageCovered` take only context properties and rule constants. |
| Satisfiability | See Other changes 2: no conflict; scripted scenarios behave as intended. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v06.md`: identical |
| Files written | only OUTPUT_MODEL.md, history/v06.md and this fix log; nothing under docs/stage1-output-requirements/ was changed; nothing committed or pushed |
