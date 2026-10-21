# Fix log — iteration 20
Input review: reviews/review-iter-20.md · Input version: v19 · Output version: v20
Date: 2026-10-21

## What was read, downloaded and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026) and the source rows of section 5 that concern the remark (S-001);
- v19 (`OUTPUT_MODEL.md`, byte-identical to `history/v19.md` and to HEAD), all sections: every element and invariant, the traceability table, section 8, and the search log and change log;
- review 20 (one remark, R20-01).

**Earlier loop files read, so that no fix is undone:**
- the oscillation checks after iterations 12 and 16, with their watch points. INV-060, INV-086, INV-087, INV-105, E-060 and E-061 are watch-point items. Their formal text is not touched: all 181 `omn` blocks are byte-identical to v19. INV-087 and INV-105 are not changed at all. E-060, E-061, INV-060 and INV-086 receive one Notes sentence each, a pointer, which changes no predicate, attribute, level or antecedent. The responder-label items (INV-062 and the others of watch point 4) are not changed; INV-062 is only named in ISS-03;
- fix 19 (format and checks);
- every review and fix passage on ISS-03, found by search. Reviews 01–19c found ISS-03 founded. Reviews 02 and 03 checked its pointers (E-038, E-043, E-049, E-067, INV-105). No remark on ISS-03 or on the section 3.5 list was ever raised, so no fixer declined one. ISS-03 and the section 3.5 list are unchanged since v00.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**Downloads.** With `curl` into the fresh directory `/tmp/r20fix-dl-8noW`, outside the repository. The text was extracted into `/tmp/r20fix-txt-jrVH`.
- [S-001] ICHD-3, the Stage 1 URL: HTTP 200, 1,047,291 bytes, 211 pages. Page 190 was extracted with `pdftotext -raw` and `-layout`, and rendered with `pdftoppm` and read.
- **The new quote.** The comments of A1.1 begin "This subclassification of 1.1 Migraine without aura is clearly applicable only to menstruating women as defined above." The text layer breaks "with-out" at a line end and gives "subclassification" with the "ﬁ" ligature. The rendered page reads as quoted.
- **E-060 quotes.** On the rendered page, A1.1.1 and A1.1.2 criterion B read "day 1 ± 2 (i.e. days −2 to +3)", and note 2 reads "there is no day 0", as quoted in E-060.
- **Stage 1 quote.** The Stage 1 OUT-030 quote "The importance of distinguishing between A1.1.1 Pure menstrual migraine without aura and A1.1.2 Menstrually related migraine without aura is that hormone prophylaxis is more likely to be effective for the former." is on the same page.

No web search and no new source.

**Scripts.** All are in the session scratchpad, `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/r20fix/`, and were run with `python3 -I`:
- `stmts.py`: every Stage 1 Statement that mentions migraine, with its context;
- `qcheck.py`: normalised search of the p. 190 text (NFKC, line-end hyphens joined, whitespace collapsed);
- `quotes.py`: every double-quoted string on an added line of the diff, searched in Stage 1 v18, the ICHD-3 p. 190 text and v19;
- `mech.py`: the mechanical checks, with a comparison with v19;
- `types.py`: declared names and undeclared identifiers, v20 against v19;
- `whichitem.py`: the item and field of every changed line.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R20-01 | fixed (the review's option (a), with its optional OUT-008) | Section 8, ISS-03 ("Stage 1"; new "Evidence"; "Effect on the model"; "For the human"); section 3.5 (reference rule); Notes of E-022, E-044, E-060, E-061, INV-060 (new Notes field) and INV-086; section 7, coverage reasons of rows OUT-008, OUT-019 and OUT-030 | **Verified.** The review is right.<br>• **OUT-019** (SHOULD): "the absolute number of migraine days and moderate/severe headache days per month that remain on treatment". **OUT-030** (MUST): "For patients who menstruate, the diary output MUST be able to show migraine attacks and migraine days in relation to the days of menstruation". Neither states the OUT-005 condition, and neither refers to OUT-005.<br>• The model reads both without the condition: E-044, INV-060 and INV-061; E-060, E-061, INV-086 and INV-087.<br>• In v19 neither ISS-03, nor the section 3.5 list, nor those items' Notes, nor rows OUT-019 and OUT-030 said so.<br>**Why option (a).** One entry lets the human decide the migraine-day condition once, for every statement of the same kind. Option (b) would split that decision into two entries.<br>**ISS-03 "Stage 1".**<br>• The list adds OUT-008 ("periods without migraine days", MAY), OUT-019 (with its trigger, "a relative (percentage) change in migraine or headache days") and OUT-030 ("migraine attacks and migraine days in relation to the days of menstruation", MUST, "whose only stated condition is "For patients who menstruate"").<br>• It adds that OUT-020 refers to OUT-018 and OUT-019 by their IDs ("the underlying values (OUT-018, OUT-019)").<br>• It adds that OUT-002 and OUT-007 name migraine days but require none. This sentence states the outcome of the completeness check (below) in the issue itself.<br>**New "Evidence".**<br>• The OUT-030 Rationale ("Distinguishing pure menstrual from menstrually related migraine matters for treatment").<br>• The A1.1.1 and A1.1.2 window of E-060.<br>• One new quote: [S-001] "This subclassification of 1.1 Migraine without aura is clearly applicable only to menstruating women as defined above." (A1.1 comments, first sentence, p. 190), verified above.<br>• A fragment of the OUT-019 Rationale ("EHF defines difficult-to-treat migraine by absolute numbers of debilitating days").<br>**"Effect on the model".** The v19 sentences are kept. "The same holds for" introduces three sub-items:<br>• OUT-008: E-022, MAY for every subject; INV-104 marks the covered period and each period of the time course for which the summary shows 0 migraine days (ISS-04);<br>• OUT-019: E-044, INV-060 and INV-061; also with a responder label, which shows the residual burden by its reference to OUT-019 (INV-062);<br>• OUT-030: E-060, E-061, INV-086 and INV-087 at MUST, for every selected time range during which the subject menstruates, whether or not the subject has migraine; the cycle lines of the overview (INV-105).<br>The closing sentence adds a subject who menstruates and has only tension-type headache, and "no migraine attacks".<br>**"For the human".** The decision is extended to OUT-008, OUT-019 and "the menstrual-relation view of OUT-030, which is MUST". "May have" now covers OUT-030 as well as OUT-028, "which Stage 1 groups among the outputs that support diagnosis and classification" (Stage 1 Group G).<br>**Section 3.5.** The list reads "(OUT-008, OUT-018, OUT-019, OUT-022, OUT-028, OUT-030, OUT-035)".<br>**Pointers.**<br>• One sentence each in the Notes of E-022, E-044, E-060, E-061 and INV-086, and a new Notes field in INV-060.<br>• Every element that ISS-03 names now points to it. The invariants that ISS-03 names point to it where their antecedent carries the reading: INV-060 and INV-086 (new), and INV-105 (since v00). The others (INV-035, INV-040, INV-056, INV-061, INV-062, INV-068, INV-070, INV-087, INV-104) are named without a pointer, as INV-035, INV-040, INV-056, INV-068, INV-070 and INV-104 were in v19.<br>**Rows.** OUT-008 ("see ISS-03 on periods without migraine days"), OUT-019 ("see ISS-03 on the residual migraine days, and ISS-05") and OUT-030 ("see ISS-03").<br>**Not changed**, as the review requires:<br>• no predicate, condition, antecedent, attribute, level, Realises field, or Elements or Invariants column;<br>• no migraine condition is added to INV-060, INV-086, INV-105 or any other item, so the model keeps following Stage 1;<br>• the ISS-03 title. OUT-030 also names migraine days, so the title stays accurate. |

## ISS-03 completeness check (the same defect)

`stmts.py` lists every Stage 1 v18 Statement that contains "migrain" (case-insensitive). It finds 17 statements: OUT-002, 005, 007, 008, 012, 013, 018, 019, 021, 022, 023, 026, 028, 029, 030, 035 and 037. No other Statement contains "migrain". OUT-009, OUT-020 and OUT-034 were added to the check by hand, because they include migraine-day outputs by requirement ID without the word. So 20 statements are classified below.

| Statement | What it names | Result |
|---|---|---|
| OUT-005 | migraine days "For patients with migraine" | The condition itself. |
| OUT-018, OUT-022, OUT-028, OUT-035 | migraine days, no condition, no reference | In the ISS-03 list since v00. |
| OUT-019 | "the absolute number of migraine days [...] per month that remain on treatment", no condition, no reference | **Added** (R20-01). |
| OUT-030 | "migraine attacks and migraine days", condition "For patients who menstruate" only | **Added** (R20-01). |
| OUT-008 | "periods without migraine days" (MAY), no condition, no reference | **Added**, the review's optional item. The model reads it without the condition: E-022 is MAY for every subject. INV-104 asks for the mark wherever the clinician-facing summary shows 0 migraine days, because OUT-034 includes OUT-008 by ID. So a decision of the human on OUT-008 would carry over to INV-104. |
| OUT-009, OUT-021, OUT-034 | migraine days by reference to OUT-005 ("OUT-004 to OUT-007", "migraine days (OUT-005)", "OUT-004 to OUT-009") | Listed in ISS-03 since v00. The components keep the condition (INV-035, INV-068, INV-104). |
| OUT-020 | "the underlying values (OUT-018, OUT-019)", by reference | **Now named** in ISS-03 "Stage 1". By the reference rule it keeps the reading of OUT-018 and OUT-019 (INV-062), so the human's decision on them carries over. It does not itself name migraine days. |
| OUT-002 | "Outputs that report migraine days [...] SHOULD state which published definition" | **Excluded, with reason now stated in ISS-03.** It requires no migraine days. It asks for a label wherever an output reports them, for every subject (INV-008). |
| OUT-007 | attacks "separately from the number of headache or migraine days" | **Excluded, with reason now stated in ISS-03.** It requires attack counts, not migraine days. Its attacks are "frequency of attacks" of ICHD-3, of any headache type (E-019). |
| OUT-012 | "For migraine", migraine-associated symptoms | Excluded. It names no migraine days or migraine attacks, and it states its own migraine condition, which the model keeps (INV-022, INV-076). |
| OUT-013 | "For patients with migraine with aura", auras | Excluded. It names auras, with its own condition (E-027). |
| OUT-037 | "For migraine", composite index | Excluded. It names no migraine days, and it states its own condition (`concerns`, INV-091, INV-092). |
| OUT-023 | "migraine-related non-pain symptoms" | Excluded. It names neither migraine days nor migraine attacks; the attacks treated with an acute medication are of any headache type. |
| OUT-026 | "Migraine Treatment Optimization Questionnaire" | Excluded. This is an instrument name. |
| OUT-029 | "(for example migraine and tension-type headache)" | Excluded. These are headache types of the per-type breakdown. It names no migraine days. |

**Result.** After the fix, every Stage 1 Statement that names migraine days or migraine attacks without the OUT-005 condition is in the ISS-03 list and in the section 3.5 list. There are seven: OUT-008, OUT-018, OUT-019, OUT-022, OUT-028, OUT-030 and OUT-035. Every other statement that mentions migraine is covered in one of three ways:
- it refers to OUT-005 by ID (named in ISS-03);
- it requires no migraine days (OUT-002 and OUT-007, named in ISS-03 with the reason);
- it names no migraine days or migraine attacks (this table).

No other item of the model applies the no-condition reading without being named in ISS-03, for these reasons:
- the time-course, treatment-review and clinician-summary components keep the condition by reference (INV-035, INV-068, INV-104);
- the cycle-line forms of `reports` (E-011, INV-008) and of INV-011 are labels and completeness wherever cycle lines are shown, not readings of a condition.

## Other changes

- **Bookkeeping:**
  - the header (v20, iteration 20, under review);
  - section 9 ("as of v20");
  - one search-log paragraph for iteration 20: the [S-001] download and the p. 190 check, no web search and no new source;
  - the v20 change-log entry.
- **Items changed: 11:**
  - six Notes fields: E-022, E-044, E-060, E-061, INV-060 (new) and INV-086;
  - ISS-03;
  - the section 3.5 reference rule;
  - three traceability coverage reasons: OUT-008, OUT-019 and OUT-030.

  Bookkeeping comes on top: header, section 9, search log and change log. No `omn` block, Conformance field, Realises field, Reading or Predicate changed. No Elements or Invariants column of the traceability table changed, and no source row.

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), none missing and none duplicated. Issues: ISS-01 to ISS-06 and ISS-08 to ISS-11. ISS-07 appears only as withdrawn (section 8 note, section 9, change log). |
| References | No dangling E- or INV- reference. Every S reference lies in S-001–S-046 or S-101–S-106 (no new row). Exactly the 39 Stage 1 OUT IDs are referenced. |
| Fields | 177 items, each with exactly one Realises and one Conformance field and at most one Notes field (INV-060 now has one). Each invariant has one Predicate and one Reading. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every requirement, the row's E and INV sets equal the reverse index of the Realises fields: 0 mismatches. Only the coverage reasons of rows OUT-008, OUT-019 and OUT-030 changed. |
| ISS-03 pointers | The Notes of E-022, E-038, E-043, E-044, E-049, E-060, E-061, E-067, INV-060, INV-086 and INV-105 point to ISS-03. Every element named in ISS-03 (E-022, E-044, E-060, E-061) is among them. Rows OUT-008, OUT-018, OUT-019, OUT-022, OUT-028, OUT-030 and OUT-035 name ISS-03: exactly the seven statements of the section 3.5 list. |
| Formal text | All 181 `omn` blocks are byte-identical to v19. |
| Types and names | 540 declared names, counting enum constants and variant tags: the same set as v19, none declared twice. The only capitalised identifiers in `omn` blocks that are not declared are the bound variables A, C, D, K, Ks and L and the level keywords MUST, SHOULD and MAY. Every type used is defined. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. Every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type: 0 violations. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33; total 110, unchanged. Scopes: output 77, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate begins with `¬`. |
| Diff against v19 | `git diff -U0`: 15 hunks, 32 lines added and 14 removed.<br>• Line 2: the header.<br>• Line 215: section 3.5, the reference-rule list.<br>• Lines 714, 1245, 1777, 1791 and 3179: one sentence appended to the Notes of E-022, E-044, E-060, E-061 and INV-086.<br>• Line 2727: the new INV-060 Notes line, after its Evidence.<br>• Lines 3544, 3555 and 3567: rows OUT-008, OUT-019 and OUT-030, coverage reasons only.<br>• Lines 3594–3602: ISS-03.<br>• Line 3651: section 9, "as of v20".<br>• Two lines after the iteration-19 search-log paragraph.<br>• Nine lines after the v19 change-log entry.<br>No other line changed. INV-087 and INV-105 are unchanged. |
| Quotes (`quotes.py`) | Every quoted string on an added line was found in its source.<br>• **Stage 1 v18:** the OUT-008, OUT-018, OUT-019, OUT-022, OUT-028, OUT-030, OUT-035, OUT-020 and OUT-007 fragments, the OUT-030 Rationale and the OUT-019 Rationale fragment.<br>• **ICHD-3 p. 190:** the new [S-001] quote, also read on the rendered page.<br>• **v19:** the field names and "for patients with migraine".<br>"with-out" describes the text layer and is not a quote. |
| Scope sweep | The added lines were searched for enter, entry, record, input, captur, logged, store/storage, persist, database, JSON, XML, CSV, FHIR, HL7, serializ/serialis, encod, retention, reminder, answer, algorithm, obtained, calculat, comput, field, questionnaire, data-entry, "derived from" and "decision logic". The only hits are "field" for the document's own fields (Evidence field, Notes field, Realises field). The new text states applicability conditions of Stage 1 as Stage 1 states them, and no derivation from input. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v20.md`: identical. `history/v19.md` is unchanged (equal to HEAD). |
