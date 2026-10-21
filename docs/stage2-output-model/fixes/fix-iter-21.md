# Fix log — iteration 21
Input review: reviews/review-iter-21b.md · Input version: v20 · Output version: v21
Date: 2026-10-21

## What was read, downloaded and checked

**Read in full:**
- PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 between OUT-025 and OUT-026), the S-001 row of section 5, and the change-log passages on OUT-031 (R01-09, R05-01, R12-02 and the v18 definition-coverage pass, which added the OUT-031 Caveat sentence);
- v20 (`OUTPUT_MODEL.md`, byte-identical to `history/v20.md` and to HEAD): every element and invariant, the traceability table, section 8, the sources, the search log, and the change log in outline;
- re-check 21b (one remark, R21b-01) and review 21 (no remarks).

**Earlier loop files read, so that no fix is undone:**
- the oscillation check after iteration 16, with its eight watch points and its settled points. "The '> 3 months' readings of INV-045 and INV-089" are listed as settled. No watch point concerns E-062 to E-064 or INV-088 and INV-089;
- review 02, "Checked and not raised": it compared only the Definitions of terms (p. 209) with 3.1.1 criterion B ("≥3 months") and called the difference "an inconsistency inside ICHD-3, not a model defect";
- fix 02, item 14: an empty E-062 `remissions` is a deviation from its SHOULD "for a reason in particular circumstances";
- reviews 12, 17, 19b and 19c on the remission bound. Review 19c lists "A 10-week attack-free period shown as a remission" as correctly excluded by INV-089;
- fix 20 (format and checks);
- every review and fix passage on "remission", "3.1.1", "3.1.2" and "chronic cluster", found by search. No remark on the remission duration was ever raised, so no fixer declined one, and no fix ever changed INV-089's remission conjunct.

FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker.

**Downloads.** With `curl` into the fresh directory `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix21-dl-Egw0`, outside the repository.
- [S-001] ICHD-3, the Stage 1 URL: HTTP 200, 1,047,291 bytes, 211 pages.
- Pages 41–43 and 208–211 were extracted with `pdftotext -raw` and `-layout` into `…/scratchpad/fix21-txt-qpwV`.
- Pages 42 and 209 were rendered with `pdftoppm` (`…/scratchpad/fix21-render-V19p`) and read.

**What the pages show** (all verbatim, by script and on the rendered pages):
- **p. 209, Definitions of terms:**
  - "Cluster remission period: The time during which attacks cease to occur spontaneously and cannot be induced with alcohol or nitroglycerine. To be considered a remission, the attack-free period must exceed three months."
  - Under "Chronic": "The trigeminal autonomic cephalalgias are the exception: in these disorders, chronic is not used until the disorder has been unremitting for more than one year."
- **p. 42, 3.1 Cluster headache, Comments, first paragraph:** "Attacks occur in series lasting for weeks or months (so-called cluster periods or bouts) separated by remission periods usually lasting months or years. About 10–15% of patients have 3.1.2 Chronic cluster headache, without such remission periods."
- **p. 42, 3.1.1 Episodic cluster headache:**
  - Description: "separated by pain-free periods lasting at least three months" (the text layer breaks "peri-ods" at a line end);
  - criterion B: "separated by pain-free remission periods of ≥3 months". In the text layer "≥" is the unmapped glyph `\x02`; it was read on the rendered page.
- **p. 42, 3.1.2 Chronic cluster headache:**
  - Description: "without remission, or with remission periods lasting less than three months";
  - criterion B: "Occurring without a remission period, or with remissions lasting <3 months, for at least one year." The "<" is mapped in the text layer.

The review's quotes are therefore correct, and so is its point: ICHD-3 itself calls attack-free periods of less than three months "remissions" in 3.1.2, and v20 neither recorded this nor described E-063 accurately ("an attack-free period that ICHD-3 considers a remission").

No web search and no new source.

**Scripts.** All are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix21-scripts/` and were run with `python3 -I`:
- `quotes.py`: every double-quoted string on an added line of the diff, searched after normalisation (NFKC, `\x02` read as "≥", line-end hyphens joined, whitespace collapsed) in the ICHD-3 page texts, Stage 1 v18 and v20;
- `onpage.py`: each new ISS-12 quote as an exact string on its stated page;
- `mech.py`: the mechanical checks of PROCESS.md section 11, with a comparison of all `omn` blocks with v20.

Inline checks covered the `plusMonths` arithmetic of the remission bound, the backticked names on added lines, and a scope sweep of the added lines.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R21b-01 | fixed (the review's option (a)) | Section 8: new **ISS-12** "Cluster remission duration in ICHD-3". E-063 Meaning. Notes of E-062, E-063 and INV-089. Section 7, row OUT-031, coverage reason only. | **Verified.** See the quotes above. INV-089 states `plusMonths(s, remissionMoreThanMonths) ≤ e`, a remission of more than three months under the day convention of section 2.8. By script, from 1 January 2026:<br>• a remission ending 31 March (90 days, exactly three months) is excluded;<br>• one ending 1 April is admitted.<br>So no attack-free period that 3.1.2 calls a remission (< 3 months), and no remission of exactly three months (3.1.1 "≥3 months"), can be shown as a remission period. v20 recorded this nowhere.<br>**Why option (a) and not (b).** The evidence decides it.<br>1. **Stage 1 names the definition.** OUT-031 asks for remission periods "using the ICHD-3 definitions". Its Evidence quotes the Definitions-of-terms definition of "Cluster remission period" and calls the duration sentence "the next sentence of the definition", left unquoted only by the Stage 1 rule on thresholds. INV-089 states exactly that sentence. Option (b) would show as remission periods attack-free periods that this definition excludes. That broadens what Stage 1 names, which PROCESS.md section 4 does not allow; the model must keep following Stage 1 and record the issue in section 8.<br>2. **ICHD-3 is split, not one-sided.** Three passages use "remission" in the sense of the Definitions of terms:<br>• the remission definition (p. 209);<br>• "Chronic", under which a trigeminal autonomic cephalalgia is chronic when "unremitting for more than one year" (p. 209);<br>• the 3.1 Comments, under which patients with 3.1.2 are "without such remission periods" (p. 42).<br>Only the 3.1.2 Description and criterion B call shorter periods "remissions", and 3.1.1 criterion B differs from the Definitions of terms by one day. Which usage OUT-031 means is a question for the human (section 8), not one the model can settle.<br>3. **No reversal.** The 3.1.2 wording is new evidence (review 02 compared 3.1.1 only), and it justifies recording the issue. It does not show that the settled "> 3 months" reading (oscillation check after iteration 16) misstates the definition Stage 1 quotes. Option (a) keeps that reading and changes no formal block.<br>**ISS-12** (the next free number; ISS-07 is not reused):<br>• **"Stage 1".** It quotes the OUT-031 Statement and the two OUT-031 passages that bear on the definition: the Evidence note on the duration sentence, and the Caveat phrase "each attack-free period".<br>• **"Evidence".** Seven [S-001] quotes, each with its location: the Definitions-of-terms remission sentence (p. 209; already in E-063); the 3.1.1 Description and criterion B, and the 3.1.2 Description and criterion B (p. 42); and the two passages on chronic cluster headache as being without remission (3.1 Comments, p. 42; "Chronic", p. 209). The diagnostic criteria are quoted only for the duration they give remission periods; the model applies no diagnostic criterion.<br>• **"Effect on the model".** E-063 and INV-089 follow the Definitions of terms, so an attack-free period of three months or less (one that 3.1.2 calls a remission, or one of exactly three months) is not shown as a remission period. The time between two bouts stays visible from the bouts' dates. The Caveat's "attack-free period" is read as the remission period whose definition the Caveat discusses. Where no longer attack-free period exists, for example in chronic cluster headache since onset, `remissions` stays empty: a SHOULD deviation, as fix 02 item 14 found. No other kind of attack-free period is added.<br>• **"For the human".** Which ICHD-3 usage OUT-031 means: in particular, whether attack-free periods of less than three months in chronic cluster headache, and of exactly three months, should be shown as remission periods, and if so whether they should be distinguished from remissions in the sense of the Definitions of terms.<br>**E-063 Meaning.** "an attack-free period that ICHD-3 considers a remission" now reads "an attack-free period of more than three months, the duration that the ICHD-3 Definitions of terms require of a remission". This is the review's suggested wording, adjusted to the model's style.<br>**Pointers** (one sentence each, appended):<br>• **E-062 Notes:** the remission periods shown are attack-free periods of more than three months; shorter ones, among them those that 3.1.2 calls remissions, are not shown as remission periods; see ISS-12.<br>• **E-063 Notes:** the bound is that of the Definitions of terms, which Stage 1 quotes; 3.1.1 and 3.1.2 word it differently; see ISS-12.<br>• **INV-089 Notes:** the remission bound is that of the Definitions of terms; see ISS-12.<br>• **Row OUT-031:** "a remission period shown lasts more than three months, as the ICHD-3 Definitions of terms require (E-063, INV-089); see ISS-12 on the other ICHD-3 wordings of its duration".<br>**Paraphrase corrected in E-063 Notes**, a touched item. "The output shows start, end and duration of each attack-free period" was inconsistent with INV-089, which admits no attack-free period of three months or less as a remission period. It now reads "of each remission period it shows".<br>**Not changed:**<br>• INV-089 Predicate, Reading, Conformance and Evidence;<br>• `remissionMoreThanMonths`, `lastDay` and the E-063 Evidence;<br>• E-062 Meaning ("using the ICHD-3 definitions", as Stage 1);<br>• the INV-100 Notes ("under the ICHD-3 definitions of terms");<br>• every `omn` block. |

## Satisfiability

No formal text changed: all 181 `omn` blocks are byte-identical to v20. So the predicates of E-062 to E-064, INV-088, INV-089, INV-073, INV-008 and INV-011 are those that reviews 19 to 21b found satisfiable together, and nothing in them was touched.

The new text adds no obligation. In particular:
- it requires no remission period;
- an empty `remissions` satisfies every remission conjunct of INV-089, because they are universally quantified;
- INV-088 requires no remission period;
- the SHOULD of E-062 `remissions` is unchanged.

## Other changes

- **Bookkeeping:**
  - the header (v21, iteration 21, under review);
  - section 9 ("as of v21");
  - one search-log paragraph for iteration 21: the [S-001] download, the pages extracted and rendered, and the quote checks; no web search and no new source;
  - the v21 change-log entry.
- **Items changed: 6 fields in 5 items:**
  - E-062 Notes;
  - E-063 Meaning and Notes;
  - INV-089 Notes;
  - row OUT-031 (coverage reason only);
  - ISS-12 (new).

  Bookkeeping comes on top: header, section 9, search log and change log. No `omn` block, Predicate, Reading, Conformance field, Realises field, Evidence field, or Elements or Invariants column changed, and no source row.
- **Wording.** "Entry", for an ICHD-3 glossary term, was avoided in the new text ("the definition of … in the Definitions of terms"), so that no reader confuses it with data entry.

## Checks

| Check | Result |
|---|---|
| Headings | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), none missing and none duplicated. Issues: ISS-01 to ISS-06 and ISS-08 to ISS-12. ISS-07 appears only as withdrawn: the section 8 note, section 9 and the change log. |
| References | No dangling E-, INV- or ISS- reference. Every S reference lies in S-001–S-046 or S-101–S-106 (36 distinct; no new row). Exactly the 39 Stage 1 OUT IDs are referenced. |
| Fields | 177 items. Each has exactly one Realises, one Conformance and one Evidence field, and at most one Notes field. Each element has one Definition and one Meaning; each invariant has one Predicate and one Reading. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". For every requirement, the row's E and INV sets equal the reverse index of the Realises fields: 0 mismatches. Only the coverage reason of row OUT-031 changed. |
| ISS-12 pointers | The Notes of E-062, E-063 and INV-089 and row OUT-031 name ISS-12. These are every element and invariant that ISS-12 names as affected. |
| Formal text | All 181 `omn` blocks are byte-identical to v20. |
| Types and names | The declared names, and every use of them, are those of v20 (identical blocks), so every type used is defined, as reviews 21 and 21b found. Every backticked model name on an added line is declared in an `omn` block: `remissionMoreThanMonths`, `lastDay`, `bouts`, `remissions` and `ongoing`, plus `onlyOfType`, `scopeFor` and `summarisesMedication` in the unchanged parts of the changed lines. |
| Typing rule for levels | 172 level-annotated attribute declarations (core 94, MUST 29, SHOULD 47, MAY 2), unchanged. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33; total 110, unchanged. Every MUST NOT and SHOULD NOT predicate begins with `¬`, and no MUST or SHOULD predicate does. |
| Diff against v20 | `git diff -U0`: 10 hunks, 27 lines added and 7 removed.<br>• Line 2: the header.<br>• Lines 1807, 1824 and 1829: E-062 Notes, E-063 Meaning and E-063 Notes.<br>• Line 3249: INV-089 Notes.<br>• Line 3568: row OUT-031.<br>• Lines 3645–3655: ISS-12, inserted after ISS-11.<br>• Line 3662: section 9.<br>• Two lines after the iteration-20 search-log paragraph.<br>• Seven lines after the v20 change-log entry.<br>No other line changed. |
| Quotes (`quotes.py`, `onpage.py`) | 28 quoted strings on added lines.<br>• 26 were found in their sources:<br>  – the six new [S-001] quotes, and the existing p. 209 remission sentence, each as an exact string on its stated page (p. 42 or p. 209), with "≥" also read on the rendered page;<br>  – the OUT-031 fragments (Statement, Evidence note, Caveat) in Stage 1 v18;<br>  – the v20 wording quoted in the change log in v20.<br>• The other 2 are the model's own new text, quoted in the change log: the ISS-12 title and the new E-063 wording. |
| Scope sweep | The added lines were searched for enter/entry, record, input, captur, logged, store/storage, persist, database, JSON, XML, CSV, FHIR, HL7, serializ/serialis, encod, retention, reminder, answer, algorithm, obtained, calculat, comput, field, questionnaire, data-entry, "derived from", "decision logic" and diagnos. The hits are:<br>• "field" for the document's own fields;<br>• "diagnostic criteria", named only to say that they are quoted for their wording and that the model applies none.<br>The new text states a duration bound on a shown remission period, an output relation already in INV-089, and no derivation from input. |
| Snapshot | `cmp OUTPUT_MODEL.md history/v21.md`: identical. `history/v20.md` is unchanged (equal to HEAD). |
