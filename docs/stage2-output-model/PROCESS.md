# Stage 2 — Formal model of the headache diary output data: process and rules

This file is binding for every agent working in this folder: the author, the reviewer/fact-checker, the fixer and the oscillation checker. Read it in full before doing anything else.

## 1. Goal

Build and maintain a **formal model of the output data** of a headache diary, grounded in evidence-based medicine (EBM).

The model states precisely and unambiguously the information content of the diary's outputs:

- which kinds of output exist (reports, summaries, measures, indicators, views, labels, caveats);
- which elements each output contains;
- the type, value domain and unit of each element;
- which elements are mandatory, recommended or optional, and when they apply (conformance);
- how elements of an output relate to each other (composition, references, co-presence, comparisons);
- the invariants that every valid output satisfies.

"Output" has the same meaning as in Stage 1: anything the diary produces for a reader. Readers are patients, parents and caregivers, clinicians, researchers and registries.

**Baseline.** The requirements baseline is Stage 1, `docs/stage1-output-requirements/OUTPUT_REQUIREMENTS.md`, version v18, status converged. Stage 1 is read-only for Stage 2: no agent edits any file under `docs/stage1-output-requirements/`.

## 2. Hard scope exclusions

The following must **not** appear anywhere in text written for this stage: the model, its notes, review remarks, fix logs or oscillation reports.

1. **Input data**: what is entered or recorded, data fields, data-entry questions, how often data is entered, reminders, the data-entry interface. The model has no input entities: no "entry", "record", "log item", "questionnaire answer" or similar types, and no element is described as entered, recorded or captured.
2. **Storage format**: persistence, databases, tables as storage, files, record or file layouts, serialization or exchange formats (for example JSON, XML, CSV, HL7 FHIR), encodings, storage keys or identifiers that exist only for storage, versioning of stored records, retention.
3. **Derivation from input**: any function `f(input) -> output`, that is, any rule, formula, counting procedure, algorithm, decision logic or threshold whose arguments include input or recorded data. Examples:
   - how headache days are obtained from what the patient recorded;
   - how a recorded attack is classified as migraine;
   - how an instrument's total score is obtained from the patient's answers.

**Thresholds, formulas and computed fields that are part of the output data are in scope, and the model must contain them.** "Part of the output data" means either of these:

- **Shown to the reader.** For example:
  - a named responder criterion with its threshold (OUT-020);
  - the levels of regular use of ICHD-3 code 8.2 shown next to the medication-overuse indicator (OUT-016);
  - an instrument's category shown with its score;
  - the evaluation time points shown with a response comparison (OUT-018).
- **A relation among output elements only.** It ties a shown value to other shown values, with every argument an element of the output model. For example:
  - a percentage change and the absolute change and baseline value shown with it;
  - a total across drug classes and the per-class values;
  - the medication-overuse indicator and the per-class medication days, reporting periods and reference levels it refers to;
  - an instrument category and the total score shown with it.

The test is the arguments. A rule over output elements only is in scope. A rule that needs input or recorded data is out of scope.

How to stay in scope:

- **The model describes what a reader is shown**, never where the shown information comes from. An output may list individual attacks, days or treatments (for example a per-attack line of OUT-023 or a treatment line of OUT-024). Model such a line as an output item defined by what it shows, not as a recorded event.
- **The model is an abstract information model of outputs, not a storage or exchange schema.** Stage 1 excluded "data models" as a storage format. That exclusion still holds for anything that models storage. The Stage 2 model is a different thing: a representation-independent specification of output content.
- **Computed (derived) fields that an output shows are output data and must be in the model.** Examples are a change from baseline (absolute and percentage), a total across drug classes, a proportion of days, a per-period average or median, an instrument's total score and category, and an indicator. Each is modelled as an element with its type, unit and conformance. Mark it as derived in the notation and give its relation to the other output elements it depends on, where that relation is part of the output data as defined above.
- **Thresholds and formulas from standards and instruments.** When a standard or validated instrument defines a value set, the model gives it with its source and section or code. Examples are ICHD-3 codes, instrument grades and categories, score ranges, and the perimenstrual window of ICHD-3 A1.1.
  - The model states the category labels exactly as the source names them.
  - When a cut-off, reference level or formula is part of the output data, the model states it in full. Examples are a grade boundary on a total score, the reference levels of ICHD-3 code 8.2, or a responder threshold.
  - Every number and every formula taken from a source cites it under section 4: a verbatim quote, its location and a URL.
  - Criteria whose arguments are input or recorded data stay out (item 3 above).
- **Invariants and relations are constraints on outputs.** They state what holds in every valid output. Examples:
  - a value lies in its domain;
  - a period does not end before it starts;
  - every measure states the reporting period it refers to;
  - a number of days within a period does not exceed the length of that period in days;
  - two periods compared in one comparison have equal length;
  - a label or caveat is present whenever the element it qualifies is shown;
  - a relative change is shown together with the absolute values it compares;
  - a percentage change agrees with the absolute change and the baseline value;
  - a period's stated length agrees with its stated start and end dates.

  Equalities, arithmetic and threshold comparisons are allowed when every argument is an output element. A relation must be correct under the definitions the output names: for example, it must not assume something about missing diary days that the definitions do not state.
- **Conditions of applicability** (for example "for patients with migraine", "for patients who menstruate", "where results of validated instruments are available") are stated as Stage 1 states them, as properties of the output's subject, audience or context. They must not become decision logic over input or recorded data.
- **Presentation properties** that Stage 1 requires are in scope: a time series of consecutive periods, a weekly view, co-presence of elements in one view, plain-language wording, labels, captions, caveats. They are modelled abstractly, as views and the elements they must contain together. They are not modelled as screen layouts.
- **Technical delivery formats** (file formats, interoperability standards) stay out of scope unless a clinical source explicitly requires them.
- **Choosing quotes.** Pick quotes that show the clinical meaning, value set, threshold or formula of an output element. Do not pick quotes whose substance is data collection, storage, or deriving a value from input data. Never alter a quote. If a relevant passage mixes in-scope and out-of-scope content, quote only the part that supports the model element and mark omissions with `[...]`, without changing the meaning.

## 3. Formal notation

- The author chooses one formal, representation-independent notation and defines it in section 2 "Notation" of `OUTPUT_MODEL.md`. That section gives the notation's syntax and semantics and its primitive types (for example calendar dates, durations, non-negative integers, percentages, text).
- The notation must support:
  - named types;
  - records with named attributes;
  - enumerations;
  - tagged variants;
  - optionality and multiplicity;
  - references between elements;
  - derived (computed) elements and their relations to other output elements, including arithmetic and threshold comparisons;
  - invariants written as predicates (for example in first-order logic).
- A notation from a formal specification language (for example a subset of Z, Alloy or VDM) is acceptable when its subset is defined in the document. Programming, database, schema or serialization languages are not acceptable: SQL, JSON Schema, XML Schema, Protobuf, FHIR profiles, class code and the like.
- Once the notation is defined, it is stable. A wish for a different notation is a style preference, not a remark. Only a defect counts as a remark: undefined syntax, ambiguous semantics, or an inability to express what Stage 1 requires.

## 4. Evidence and fidelity rules

- **Every model element and every invariant traces to the Stage 1 requirement(s) it realises** (`Realises: OUT-NNN, ...`). The evidence of those requirements, including their sources, quotes and strength, carries over by reference. Stage 1 quotes are not repeated.
- **Fidelity to Stage 1.** The model must not contradict, narrow or broaden a Stage 1 requirement. Every observable property in a Stage 1 Statement must be represented: what is reported, per what period, at what granularity, the comparisons it must allow, labels, caveats, audience-specific views and conditions of applicability. Each part of a Stage 1 Statement keeps its own strength.
- **Conformance follows Stage 1 strength.** An element or invariant has the conformance level (MUST / SHOULD / MAY / SHOULD NOT / MUST NOT) of the Stage 1 statement part it realises. A model element may be marked stronger than one Stage 1 statement part only when another Stage 1 statement part of at least that strength directly requires it; the element then cites both parts. Purely structural primitives needed to express a requirement (for example a reporting period, which OUT-001 makes mandatory) take the strength of the requirement that needs them.
- **New facts need new evidence.** A model element may add detail that Stage 1 does not state, but only where that detail is needed to make a Stage 1 requirement formally precise: the value set of a named instrument or classification, a score range, a unit, a category label, a code list, or a threshold, reference level or formula that is part of the output data (section 2). Stage 1 did not state thresholds or formulas because of its own scope rule. Stating them in the model where they are part of the output data makes Stage 1 precise and does not broaden it. Each such detail cites a source under the Stage 1 evidence rules:
  - a verbatim quote in the original language;
  - a faithful English translation if the source is not in English;
  - the location in the source;
  - a URL where the quoted text can actually be read;
  - the DOI and/or PMID when they exist;
  - the source type and grading;
  - the access date.

  Prefer the instrument developer's or standard owner's own publication, and the most recent version.
- **Source IDs.** Stage 1 sources are cited by their Stage 1 IDs (`S-001` to `S-046`) and are not re-listed. New Stage 2 sources are numbered from `S-101` upward and listed in the model's Sources section.
- **No new kinds of output.** An output that EBM supports but that no Stage 1 requirement covers is not added to the model. Record it, with source, quote and link, in section 8 "Stage 1 issues for the human". The same applies to a factual error, an outdated source or a contradiction found in Stage 1. The model keeps following Stage 1 and does not deviate silently. Where an issue directly affects a model element, add a pointer to the issue in that element's Notes.
- **Multilingual search.** New searches cover all relevant languages, under the rule in Stage 1 PROCESS.md section 4. Record them in the model's search log.

## 5. Files

```
docs/stage2-output-model/
  PROCESS.md                          this file
  OUTPUT_MODEL.md                     the current model (the single living document)
  history/vNN.md                      snapshot of OUTPUT_MODEL.md for each version
                                      (v00 = initial draft, vNN = after the fix of iteration NN)
  reviews/review-iter-NN.md           fact-check and review of iteration NN
  reviews/review-iter-NNb.md          first re-check of iteration NN (only after a NO_REMARKS review)
  reviews/review-iter-NNc.md          second re-check of iteration NN (only after a NO_REMARKS re-check)
  fixes/fix-iter-NN.md                the fixer's response to review NN, remark by remark
  oscillation/check-after-iter-NN.md  loop and oscillation check
  FROZEN_ITEMS.md                     items frozen after oscillation, awaiting the human's decision
```

Agents write only the files assigned to them. Agents do not commit or push; the orchestrator does that. All files are written in English.

## 6. Structure of OUTPUT_MODEL.md

```
# Headache diary — formal model of output data (Stage 2)
Version: vNN · Iteration: NN · Status: draft | under review | converged
Baseline: Stage 1 OUTPUT_REQUIREMENTS.md v18 (converged)

## 1. Scope and exclusions       (short restatement of section 2 above)
## 2. Notation                   (syntax and semantics of the notation; primitive types)
## 3. Conformance                (how MUST/SHOULD/MAY/SHOULD NOT apply to elements, attributes
                                  and invariants; conditional applicability)
## 4. Model overview             (the output kinds and how they relate)
## 5. Model elements             (grouped by topic; the grouping is the author's choice)
### E-001 <name>
- Definition: <formal definition in the notation>
- Meaning: <what the element is in the output and for whom>
- Conformance: <level, per attribute where levels differ; applicability condition>
- Realises: OUT-NNN, ...
- Evidence: Stage 1 OUT-NNN; plus, for each detail not in Stage 1:
  - [S-1NN] "<verbatim quote>" (<location>). Translation: "<English>" (only if not English)
- Notes: ... (optional)
## 6. Invariants
### INV-001 <name>
- Predicate: <formal predicate in the notation>
- Reading: <plain-English reading>
- Conformance: ...
- Realises: OUT-NNN, ...
- Evidence: as for elements
## 7. Traceability               (every Stage 1 requirement OUT-001 ... OUT-039 -> the elements
                                  and invariants that realise it, with coverage: full / partial
                                  and why)
## 8. Stage 1 issues for the human  (gaps or defects found in Stage 1, with evidence; may be empty)
## 9. Withdrawn elements         (ID, name, iteration withdrawn, reason)
## 10. Sources                   (new sources S-101 ... only, with the Stage 1 fields: ID, full
                                  citation, type and grading, language, year, DOI/PMID, URL where
                                  quotes can be verified, access date)
## 11. Search log                (Stage 2 searches: languages, queries, sites, results)
## 12. Change log                (one entry per version)
```

## 7. Stable identifiers

- Model elements are numbered `E-NNN`, invariants `INV-NNN`, new sources `S-1NN`. Never renumber or reuse an ID. A removed element or invariant moves to "Withdrawn elements" with its reason and the iteration in which it was withdrawn.
- Attributes are referred to as `E-NNN.attributeName`.
- Review remarks are numbered `R{iteration}-{n}`, for example `R03-07`. Remarks from re-checks carry the re-check letter: `R07b-01`, `R07c-02`.
- Oscillation findings are numbered `OSC-{iteration}-{n}`.

## 8. The loop

0. **Author** reads Stage 1 in full, does any research needed, and writes `v00`.
1. **Reviewer** (a new agent each iteration) fact-checks and reviews the current version and writes `reviews/review-iter-NN.md`.
2. If the verdict is `NO_REMARKS`, a new, independent reviewer re-checks the same version (`review-iter-NNb.md`). If that re-check also returns `NO_REMARKS`, one more new reviewer re-checks it (`review-iter-NNc.md`). So there are at most two extra re-checks, run one after another.
   - The loop ends only when the review and both re-checks all return `NO_REMARKS`.
   - As soon as any of them returns `REMARKS`, no further re-check runs. A **fixer** (a new agent) then addresses every remark of that review. It fixes each remark or declines it with evidence, and it may rewrite the document if needed. It writes the new version, its snapshot and `fixes/fix-iter-NN.md`. The loop then continues with iteration NN+1.
   - Re-checks belong to iteration NN and do not count as separate iterations.
3. An **oscillation checker** (a new agent) runs after iterations 4, 8, 12 and so on, and after the final iteration. It looks for items that keep changing back and forth. Oscillating items are frozen and handed to the human (section 10).

The orchestrator may stop the loop after 32 iterations if it has not converged, and hand the question back to the human.

## 9. What counts as a remark

Raise only issues that require a change:

- **Scope violation** (section 2): input data, storage format, or any rule, formula, threshold or procedure whose arguments include input or recorded data. Thresholds, formulas and relations whose arguments are all output elements are not a scope violation.
- **Infidelity to Stage 1**:
  - an element or invariant contradicts, narrows or broadens a Stage 1 requirement;
  - a conformance level does not match the Stage 1 strength (section 4);
  - an applicability condition is wrong.
- **Coverage gap**:
  - a Stage 1 requirement, or an observable property in its Statement, has no representation in the model, including a computed field, threshold or formula that is part of the output data (section 2);
  - the traceability table is wrong or incomplete.
- **Unsupported element**: an element, attribute, value or invariant that traces to no Stage 1 requirement and has no cited evidence.
- **Factual error** compared with the source, in a value set, unit, range, code, category label, instrument name or version, or standard reference.
- **Citation defect**:
  - a misquote, or a quote that cannot be found at its URL;
  - a broken or wrong link, or wrong citation metadata;
  - an outdated source, where a newer version exists and changes the element.
- **Formal defect**:
  - an undefined type or symbol;
  - an ill-typed expression;
  - ambiguous semantics;
  - a missing multiplicity or optionality;
  - a dangling reference;
  - contradictory or unsatisfiable invariants;
  - an invariant that excludes an output Stage 1 permits, or admits an output Stage 1 forbids.
- **Contradiction or duplication** between elements or invariants.
- **Stage 1 issue handling**: a Stage 1 issue that the model silently works around instead of recording it in section 8, or an entry in section 8 that is unfounded.

These are **not** remarks:

- stylistic preferences;
- naming;
- alternative wordings or notations with the same meaning;
- an alternative but equivalent structuring of the model;
- optional additions without evidence.

A remark that an earlier fixer declined with a justification may be raised again only with new evidence showing that the justification is wrong.

## 10. Frozen items after oscillation

When an oscillation check reports `OSCILLATION_DETECTED`:

- **Freezing.** Each oscillating item (an element, an attribute, an invariant, a source, or a section) is **frozen** in its current state. The oscillation checker does not pick a winner.
- **Record.** The checker records each frozen item in `FROZEN_ITEMS.md`:
  - the item ID;
  - the version-by-version trace of the back-and-forth;
  - the remarks and fixes that drove it;
  - the competing positions with their evidence (quotes and links).

  The human decides these items later; agents do not.
- **Marker.** The checker marks each frozen item in `OUTPUT_MODEL.md` with the line `- Status: FROZEN (see FROZEN_ITEMS.md, OSC-NN-n)`. That marker line is the only change the checker makes to the model.
- **Fixers** must not change a frozen item.
- **Reviewers** do not raise remarks on frozen items, and these items never count toward the verdict. A reviewer who finds a factual defect in a frozen item (a misquote, a broken link, wrong citation metadata, a newer superseding source, a formal defect) lists it under "Notes on frozen items (for the human)" in the review. The orchestrator copies those notes into `FROZEN_ITEMS.md`.
- An item stays frozen until the human decides it.

## 11. Practical notes for agents

- **Web tools.** Load them with `ToolSearch` (query `select:WebSearch,WebFetch`).
- **Verifying quotes.** `WebFetch` answers through a small summarising model, so its output is not proof of verbatim wording. To check a quote word for word, download the page or PDF with `curl` (it goes through the configured proxy) and search the text. `pdftotext` and Python `pypdf` are installed. PubMed E-utilities, PubMed Central and the Europe PMC REST API are reachable.
- **Unreachable sites.** Some sites may be unreachable from this environment. Retry once, then look for an official copy elsewhere: the instrument developer's site, a society website, a journal publication of the same text, or PMC. Record unreachable sites in the search log.
- **Downloads.** Put downloaded files in a fresh directory under your scratchpad or `/tmp`, never inside the repository.
- **Reading Stage 1.** Stage 1 `OUTPUT_REQUIREMENTS.md` is long (about 250 KB). Read all of it: sections 1–3 in full, and sections 5–7 as needed. Each Stage 1 requirement has a Statement (what must be output), a Rationale, an Evidence basis with its strength, Evidence quotes and Caveats. Statements and Caveats define what the model must represent.
- **Checking the model mechanically.** Use scripts for the mechanical checks: every ID resolves, no ID is duplicated, every Stage 1 requirement appears in the traceability table, every type used is defined, and the conformance levels match. Report such checks with their results.
