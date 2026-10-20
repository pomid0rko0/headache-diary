# Stage 1 — Output requirements for the headache diary: process and rules

This file is binding for every agent working in this folder: the author, the reviewer/fact-checker, the fixer and the oscillation checker. Read it in full before doing anything else.

## 1. Goal

Collect and maintain the requirements for the **outputs** of a headache diary, grounded in evidence-based medicine (EBM).

"Output" means anything the diary produces for a reader: reports, summaries, measures, indicators, warnings, charts, tables, clinical summaries, exports of results. Readers can be patients, clinicians (primary care, neurology, headache specialists), or researchers.

## 2. Hard scope exclusions

The following must **not** appear anywhere in text written for this stage: requirement statements, rationale, notes, review remarks, fix logs or oscillation reports.

1. **Input data**: what is entered or recorded, data fields, data-entry questions, how often data is entered, reminders, the data-entry interface.
2. **Storage format**: data models, schemas, databases, record or file layouts, encodings, how long data is kept.
3. **Derivation rules**: any function `f(input) -> output`, such as algorithms, formulas, counting procedures, decision logic, or thresholds applied to recorded data.

How to stay in scope:

- Describe **what** an output is, **who** it is for, **why** it is needed (the evidence), and observable properties of the output itself. Examples are its unit, reporting period, granularity, the comparisons it must allow, how it is presented, its labelling, and the caveats it must show.
- When a standard fixes an output's clinical meaning (for example ICHD-3 or the IHS trial guidelines), name the standard and the section or code, as in "as defined in ICHD-3 code 8.2 [S-003]". Do not restate the criteria as a rule.
- Choose quotes that show the clinical need for the output. Do not choose quotes whose substance is data collection, storage, or how to compute the output. Never alter a quote. If a relevant passage mixes in-scope and out-of-scope content, quote only the part that supports the output requirement and mark omissions with `[...]`, without changing the meaning.
- Technical delivery formats, such as file formats or interoperability standards, are out of scope unless a clinical source explicitly requires them.

## 3. Evidence rules

- Every requirement cites at least one source. For each citation give:
  - a **verbatim quote** in the original language;
  - a faithful **English translation** if the source is not in English;
  - the **location** in the source (section, page, table or recommendation number);
  - a **URL where the quoted text can actually be read**: open full text, PubMed Central, an official PDF, or the abstract page if the quote comes from the abstract;
  - the DOI and/or PMID when they exist.
- Never fabricate a quote, and never paraphrase inside quotation marks. A quote that cannot be found at its URL is a defect.
- Type each source in the bibliography:
  - classification standard;
  - clinical practice guideline (name the grading system, for example GRADE, SIGN or AWMF S1–S3);
  - consensus statement or expert recommendation;
  - trial-methodology guideline;
  - systematic review or meta-analysis;
  - primary study (RCT, cohort, validation study and so on);
  - regulatory guidance;
  - other.
- Each requirement states its **evidence basis**: the highest-level source supporting it, and whether that support is evidence-graded, consensus, or expert opinion. Say so when the evidence is weak or conflicting.
- State requirement strength with RFC 2119 words (MUST / SHOULD / MAY), in proportion to the evidence. Use MUST only when a classification standard, a graded guideline recommendation, or an international methodology guideline directly supports the requirement.
- Prefer the most recent version of a source, and note when a newer version supersedes an older one.
- Record the access date for every URL.

## 4. Multilingual search

Search in all languages, not only English. At a minimum, look for guidance in English, Russian, German, French, Spanish, Italian, Portuguese, Dutch, the Scandinavian languages, Polish, Czech, Turkish, Chinese, Japanese, Korean and Arabic. Also cover any other language in which national headache guidelines or diary-related evidence exist. National headache societies and health authorities publish in their own language, so query their sites and use native-language search terms.

The document keeps a **search log**: languages, queries, databases and sites, and what was or was not found.

## 5. Files

```
docs/stage1-output-requirements/
  PROCESS.md                          this file
  OUTPUT_REQUIREMENTS.md              the current requirements (the single living document)
  history/vNN.md                      snapshot of OUTPUT_REQUIREMENTS.md for each version
                                      (v00 = initial draft, vNN = after the fix of iteration NN)
  reviews/review-iter-NN.md           fact-check and review of iteration NN
  fixes/fix-iter-NN.md                the fixer's response to review NN, remark by remark
  oscillation/check-after-iter-NN.md  loop and oscillation check
  FROZEN_ITEMS.md                     items frozen after oscillation, awaiting the human's decision
```

Agents write only the files assigned to them. Agents do not commit or push; the orchestrator does that.

## 6. Structure of OUTPUT_REQUIREMENTS.md

```
# Headache diary — output requirements (Stage 1)
Version: vNN · Iteration: NN · Status: draft | under review | converged

## 1. Scope and exclusions        (short restatement of section 2 above)
## 2. Audiences                   (who reads the outputs)
## 3. Requirements                (grouped by topic; the grouping is the author's choice)
### OUT-001 <short title>
- Statement: The diary output MUST/SHOULD/MAY ...
- Audience: ...
- Rationale: ...
- Evidence basis: <highest-level support; graded / consensus / expert opinion; strength>
- Evidence:
  - [S-001] "<verbatim quote>" (<location>). Translation: "<English>" (only if not English)
- Caveats: ... (optional)
## 4. Withdrawn requirements     (ID, title, iteration withdrawn, reason)
## 5. Sources                    (ID, full citation, type and grading, language, year,
                                  DOI/PMID, URL where quotes can be verified, access date)
## 6. Search log
## 7. Change log                 (one entry per version)
```

## 7. Stable identifiers

- Requirements are numbered `OUT-NNN` and sources `S-NNN`. Never renumber or reuse an ID. A removed requirement moves to "Withdrawn requirements" with its reason and the iteration in which it was withdrawn.
- Review remarks are numbered `R{iteration}-{n}`, for example `R03-07`.
- Oscillation findings are numbered `OSC-{iteration}-{n}`.

## 8. The loop

0. **Author** researches and writes `v00`.
1. **Reviewer** (a new agent each iteration) fact-checks and reviews the current version and writes `reviews/review-iter-NN.md`.
2. If the verdict is `NO_REMARKS`, the loop ends. Otherwise a **fixer** (a new agent) addresses every remark, either fixing it or declining it with evidence. It may rewrite the document if needed. It writes the new version, its snapshot and `fixes/fix-iter-NN.md`.
3. An **oscillation checker** (a new agent) runs after iterations 4, 8, 12 and so on, and after the final iteration. It looks for items that keep changing back and forth. Oscillating items are frozen and handed to the human (section 10).

The orchestrator may stop the loop after 12 iterations if it has not converged, and hand the question back to the human.

## 9. What counts as a remark

Raise only issues that require a change:

- a factual error;
- a misquote, or a quote that cannot be found at its URL;
- a broken or wrong link, or wrong citation metadata;
- a requirement that its quotes do not support, or one stated more strongly or weakly than the evidence allows (wrong MUST/SHOULD/MAY);
- an outdated source, where a newer version exists and changes the requirement;
- a missing output requirement that EBM sources support (give the source, quote and link);
- a scope violation (section 2);
- a contradiction or duplication between requirements;
- a gap in language coverage that plausibly hides relevant guidance (name the language and the likely source).

These are **not** remarks: stylistic preferences, alternative wordings with the same meaning, and optional additions without evidence.

A remark that an earlier fixer declined with a justification may be raised again only with new evidence showing that the justification is wrong.

## 10. Frozen items after oscillation

When an oscillation check reports `OSCILLATION_DETECTED`:

- Each oscillating item (a requirement, a source, or a section) is **frozen** in its current state. The oscillation checker does not pick a winner.
- The checker records each frozen item in `FROZEN_ITEMS.md`: the item ID, the version-by-version trace of the back-and-forth, the remarks and fixes that drove it, and the competing positions with their evidence (quotes and links). The human decides these items later; agents do not.
- The checker marks each frozen item in `OUTPUT_REQUIREMENTS.md` with the line `- Status: FROZEN (see FROZEN_ITEMS.md, OSC-NN-n)`. That marker line is the only change the checker makes to the requirements document.
- Fixers must not change a frozen item.
- Reviewers do not raise remarks on frozen items, and these items never count toward the verdict. A reviewer who finds a factual defect in a frozen item (misquote, broken link, wrong citation metadata, a newer superseding source) lists it under "Notes on frozen items (for the human)" in the review. The orchestrator copies those notes into `FROZEN_ITEMS.md`.
- An item stays frozen until the human decides it.

## 11. Practical notes for agents

- Load the web tools with `ToolSearch` (query `select:WebSearch,WebFetch`).
- `WebFetch` answers through a small summarising model, so its output is not proof of verbatim wording. To check a quote word for word, download the page or PDF with `curl` (it goes through the configured proxy) and search the text: `pdftotext` and Python `pypdf` are installed. PubMed E-utilities and PubMed Central are reachable.
- Some sites may be unreachable from this environment; for example `cr.minzdrav.gov.ru` reset the connection during setup. Retry once, then look for an official copy elsewhere (a society website, a journal publication of the same guideline, PMC, CyberLeninka, eLibrary). Record unreachable sites in the search log.
- Put downloaded files in a fresh directory under your scratchpad or `/tmp`, never inside the repository.
