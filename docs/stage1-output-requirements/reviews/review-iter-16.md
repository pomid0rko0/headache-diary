# Review — iteration 16
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v15
Date: 2026-10-20

## Summary
I downloaded every source again with curl into a new, empty folder of my own and did not reuse files from earlier agents. All 46 source URLs, the English SFEMC versions, the Swedish Kela page, the SEN, FDA and IHS landing pages and the BASH contents page returned HTTP 200. brainmed.com (S-032) reset the connection once and loaded on retry. The 11 PMC sources were read in the Europe PMC fullTextXML, and the PubMed abstracts through E-utilities. A script extracted all 276 quote citations in section 3 (288 quoted strings, counting list items separately) and matched them against the downloaded text, then compared each match with the stated page under the conventions in section 5. 280 strings matched by script. I confirmed the other 8 by hand: the ICHD-3 8.2.2 note, AAN 15B, Japan CQ II-2-14, the two AIFA sentences in the raw HTML, and the SFEMC Rd5 and RT25 rows on the embedded figure images. All 288 strings are verbatim at their URLs, and every stated page is right. The v15 location changes (15 labels in 12 requirements) are all correct, and v15 changed nothing but location labels. Translations, "[...]" omissions, grades, citation metadata (27 PMIDs through esummary and efetch), strengths, totals, cross-references and scope are in order. My searches in German (including Swiss), Korean, Czech, Greek, Swedish, Japanese and Chinese, and PubMed 2023–2026, found no missing output requirement that I could support with a verified quote, and no superseding edition. None of the four "Observed, not changed" items in fix-iter-15.md requires a change (see "Decisions on fix-iter-15 'Observed, not changed'").

## Verification coverage
In the table, "quotes checked" counts quoted strings in section 3 outside the location parentheses: Evidence and Caveat quotes, list items, and repeated quotes counted once per citation. The 84 distinct headings and labels quoted inside locations were checked separately (see below).

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 24 | 24 (1 manual: 8.2.2 note 1, `-layout` text of p. 123. PDF page = printed page. Checked: 1.3 notes 2 and 5 (p. 24), A1.1 comments and notes 3 (p. 190), item 12 (p. 7)) | 0 | — |
| S-002 | 26 | 26 (printed = PDF + 1025; the PDF's own page labels are 1026–1044. Section numbers from the heading list: 1.1.4, 1.1.9, 1.3.1, 1.3.2.0, 1.3.2.1.6–8, 1.3.2.3.1–2, 1.3.2.5, 1.3.2.6.1–3, 1.3.4) | 0 | — |
| S-003 | 6 | 6 (printed = PDF + 814; pp. 822–824) | 0 | — |
| S-004 | 10 | 10 (JATS: 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5, with their recommendation and comment paragraphs) | 0 | Europe PMC fullTextXML |
| S-005 | 9 | 9 (printed = PDF + 802; "meta-analyses" is hyphenated at a line end) | 0 | — |
| S-006 | 5 | 5 (p. 10) | 0 | — |
| S-007 | 8 | 8 (accepted manuscript v. 3.2, April 2022; pp. 20, 21, 22, 25) | 0 | — |
| S-008 | 11 | 11 (Q2 Evidence p. 9; Q4 Evidence p. 11; Q6 Optimal p. 12; Q6 Background and Evidence p. 13; Q7 Optimal p. 13) | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | 0 | — |
| S-010 | 8 | 8 (abstract quotes in efetch; pp. 3, 7; "patient-reported" is hyphenated at a line end) | 0 | E-utilities efetch for the abstract |
| S-011 | 3 | 3 (Methods > "Development of evidence-based recommendations"; consensus statements for questions 3 and 4, "Clinical guidance") | 0 | Europe PMC fullTextXML |
| S-012 | 10 | 10 (Results > Consensus subsections; Discussion paragraphs 2, 5, 6 and 7 of 7) | 0 | Europe PMC fullTextXML |
| S-013 | 10 | 10 (Results paragraph 8 of 17; Discussion subsections "Drug failure", "Assessment of patients", "Debilitating headache" and "Cut-offs values", with paragraph and sentence positions as stated) | 0 | Europe PMC fullTextXML |
| S-014 | 14 | 14 (JATS paths of all 14, including the three v15 "Introduction" locations: HALT Introduction paragraphs 1 and 2 of 3, HURT Introduction paragraph 3 of 3) | 0 | Europe PMC fullTextXML |
| S-015 | 13 | 13 ("Published 19 September 2012", "Last updated 03 June 2025") | 0 | — |
| S-016 | 11 | 11 (PDF = printed + 6; "Revised May 2026"; "R" key on PDF p. 2) | 0 | — |
| S-017 | 3 | 3 (both section pages carry the footer "BASH Guideline V2.0 2026"; the contents page reads "V1.0 2019") | 0 | — |
| S-018 | 15 | 15 (1 manual: 15B, where the margin label "Level C" interrupts the sentence. Levels from the layout text: 12A B, 14A B, 14C B, 14D B, 14E B, 14F B, 15A B, 15B C, 15C A, 15D B) | 0 | — |
| S-019 | 3 | 3 (p. 3) | 0 | — |
| S-020 | 5 | 5 (III.B.5 on printed pp. 4–5 = PDF pp. 7–8; the omitted text is the definition of relapse) | 0 | — |
| S-021 | 4 | 4 (pp. 5, 6, 11; Annex title and the subheading "Acute treatment" on p. 11, as the v15 location says) | 0 | — |
| S-022 | 6 | 6 (margin line numbers removed; lines 383–384, 393–394, 421–425, 427–429 and 464–465 confirmed) | 0 | — |
| S-023 | 4 | 4 ("Hintergrund" paragraphs 5 and 8 of 9; "Frage 3", final paragraph) | 0 | Europe PMC fullTextXML |
| S-024 | 12 | 12 (1 manual: Rd5 on the 2006 × 1337 px Figure 3 image, rated "Fort". PDF page + 394. English Part 1: section 2.2 strings on p. 726; Table 3, p. 731, rates Rd1–Rd10 "Strong") | 0 | — |
| S-025 | 3 | 3 (2 manual, the same RT25 row cited in OUT-033 and OUT-034: read on the 1864 × 2452 px Figure 1 image, under the heading "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE,", rated "Fort", in the column "FORCE". English Table 6: Rt25 "Strong" p. 743; Rt33–Rt34 "Moderate") | 0 | — |
| S-026 | 0 (not cited) | — (2020 p. 306 grade B text confirmed) | — | Downloaded (superseded entry) |
| S-027 | 7 | 7 (title and h1 "Migraine: Organisatie van zorg - digitale dagboeken"; run-in headings confirmed for each quote; "Publicatiedatum: 04-12-2023") | 0 | — |
| S-028 | 1 | 1 (Aanbeveling; GRADE sentence; 11-01-2018) | 0 | — |
| S-029 | 2 | 2 (title and h1 "Migraine: Monoklonale antilichamen"; Overwegingen; "Aanvaardbaarheid, haalbaarheid en implementatie") | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19; DHOS still lists the 2020 programme) | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (1 manual: CQ II-2-14 across the side tab, PDF p. 207 = printed p. 191, grade A. CQ I-10 in the 推奨 box, grade B (PDF p. 48). CQ I-4 p. 14, II-1-6 p. 106, II-1-12 p. 123 and VI-3 p. 355 confirmed under their CQ headers) | 0 | — |
| S-032 | 5 | 5 (七、治疗 > 病人教育 1; 3.2 预防性治疗有效性指标) | 0 | Connection reset once; retry succeeded |
| S-033 | 5 | 5 (pp. 18, 19, 26, 53; grade C/5 on pp. 26 and 53. The v15 table titles 3в and 4а are printed exactly as quoted. 295_5 and 295_6 are byte-identical to the cited PDF) | 0 | — |
| S-034 | 3 | 3 (p. 34 confirmed on a render; p. 50; grade C/5; the cover image reads "Год утверждения 2024" and lists the three developers) | 0 | — |
| S-035 | 5 | 5 (PDF pp. 48, 78) | 0 | — |
| S-036 | 2 | 2 (PDF p. 16, section 3.3; Tables 1.1 and 1.2 on PDF p. 7) | 0 | — |
| S-037 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-038 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-039 | 2 | 2 (h1 "3007 Atogepantti, … (migreenin estohoito)") | 0 | — |
| S-040 | 2 | 2 (both manual: confirmed in the raw HTML of the notice, where my text extractor missed the nested `<p>` block) | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | Europe PMC fullTextXML |
| S-042 | 3 | 3 (the v15 OUT-011 location: table-wrap "Table 2", caption "Summary of the Expert Consensus Statements.", columns "Questions" and "Statements", row Question 6. The Results list reads "based on the patient’s headache diary") | 0 | Europe PMC fullTextXML |
| S-043 | 1 | 1 (Abstract > Background) | 0 | Europe PMC fullTextXML |
| S-044 | 1 | 1 | 0 | E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113, 395; printed = PDF − 2; no grade on the quoted box items or on the p. 395 sentence) | 0 | — |
| S-046 | 3 | 3 (printed p. 5 = PDF p. 8; lines 163–167 and 174–175) | 0 | — |
| **Total** | **288** | **288** (280 script, 8 manual) | **0** | — |

### Other checks
- **Headings and labels inside locations.** Each of the 84 distinct strings occurs in its source. The exception is the S-025 figure heading, which I read on the image.
- **Section 5 strings.** All source-language strings match, including: the SFEMC English grading text (p. 726), Table 3 and Table 6; "Elles sont résumées sur la figure 3."; the S-028 GRADE sentence; the S-032 GRADE text; the S-036 sentence (PDF p. 7); the S-045 Introducción, Metodología and Tabla 3 strings (PDF pp. 11, 14 and 17); the SEN and FDA landing pages; and the IHS "Affiliate Society and other guidelines" page, which links both English PDFs.
- **Metadata.** For all cited PMIDs, authors, journals, years, volumes, pages, DOIs and PMCIDs match esummary. S-018 was published online on 31 August 2026 (ArticleDate). S-043 carries article number 135, and S-041 1770966.
- **Translations and omissions.** I read all 60 distinct non-English quotes and the 9 translated strings in section 5, and all are faithful. Every "[...]" omits only recording or calculation details, age limits, other list items, a back-reference or a definition. I read each omitted passage in the source.
- **Totals and IDs.** By the stated rule: 39 requirements (10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT), 46 source rows, 45 cited (all but S-026), no dangling OUT reference and no duplicate ID. Repeated quotes carry the same location everywhere. history/v15.md is byte-identical to OUTPUT_REQUIREMENTS.md. FROZEN_ITEMS.md does not exist.
- **Fixes.** `diff history/v14.md history/v15.md` changes only the header, section 4, the change log and 15 location labels. I checked each new label against the source: S-027 and S-029 module titles; the S-021 Annex; S-042 Table 2; the S-033 table titles; the three S-014 Introduction paragraphs. The change-log counts are right (12 sweep locations in 10 requirements; 15 in 12 with R15-01).
- **Strength and support.** I read each Statement clause by clause against its quotes. Every MUST clause rests on a classification standard, a graded recommendation or an international methodology guideline, and every mixed-strength requirement names each strength in its Strength line.
- **Scope.** I read every Statement, Rationale, Evidence basis and Caveat. None carries input, storage or derivation content, and no quote carries a counting rule or recording instruction that could be omitted without changing the meaning.
- **Versions.** No newer version exists of:
  - ICHD-3: only the ICHD-4 "Work in progress 1/2" commentaries (PMID 38388354, 40239022);
  - NICE CG150 (3 June 2025), SIGN 155 (May 2026) or BASH (V2.0 2026);
  - AAN/AHS 2026, or the FDA 2018 guidance (final) and FDA 2023 guidance (still draft);
  - EMA Rev. 1 (in force) and the Rev. 2 draft (consultation to 31 January 2027);
  - the NVN modules (04-12-2023, 11-01-2018), DHOS 2020, Japan 2021 or the Russian 2024 recommendations.

### Decisions on fix-iter-15 "Observed, not changed"
1. **Section 3 preamble and page conventions (S-002, S-003, S-005, S-020).** No change required. Every page given is the number printed on that page of the PDF at the listed URL, and it is correct.
   - For S-002, the PDF's own page labels are 1026–1044, so a viewer resolves "p. 1035" correctly.
   - The S-003 and S-005 page numbers (pp. 822–824 and 810–812) cannot be mistaken for page indices of PDFs with 18 and 14 pages.
   - The three S-020 locations also name section III.B.5, which identifies the passage without the page.

   No location sends a reader to the wrong passage, and nothing in section 5 is false. The offset notes for the other six sources are extra help, and their absence for these four is not an error under PROCESS.md section 9.
2. **Coarse but accurate locations** (S-038, S-013 in OUT-019, S-014 in OUT-009 and OUT-028, S-011 "Methods", S-039 and S-040). I confirmed each passage where the location places it: S-038 is a three-page letter without headings, and S-039 and S-040 are single web notices. No change required.
3. **Heading case and abbreviated unquoted run-in headings** (S-037, S-027). These differences are cosmetic and require no change.
4. **S-034 appendix numbering.** The contents list reads "Приложение А3. Дневник головной боли", and section 7.1 refers to "(приложение А3)". In the body, the diary text sits under the subheading "Дневник головной боли" inside the body's Приложение А3 (p. 50). So the label "appendix А3 'Дневник головной боли'" is right whichever reading is used. No change required.

### Checked and not raised
- **OUT-034, Japan CQ I-10 cited as a strong recommendation, certainty of evidence B, while the quoted sentence is from the Background.** The graded 推奨 text on PDF p. 48 itself recommends the diary for patient–physician communication ("患者‑医師間コミュニケーションの向上をはかる意味でも有用であり"). Review 08 reached the same conclusion, and I have no new evidence against it.
- **OUT-010, "on a stated scale" described as only indirectly supported.** Some sources not quoted in OUT-010 do name an intensity scale: S-020 III.B.5 ("A four-point Likert scale should be used for headache pain", printed p. 5) and S-002 1.3.2.1.4. The Evidence-basis sentence speaks only of "the quoted sources", so it is accurate. Adding these quotes would be optional.
- **OUT-020, the example "IHS position statement 2025 control levels".** S-010 defines four tiers (migraine freedom; optimal, modest and insufficient control), so the example names a real criterion.
- **OUT-036 (c) at SHOULD against OUT-001 at MUST.** OUT-001 requires every output to allow equal-length comparisons. OUT-036 (c) asks paediatric efficacy presentations to apply them. The two do not conflict.
- **Section 6 rows.** These rows describe the author's search: the IHS RWE guideline and IHS 2025 evidence-based guideline as "not retrieved", and the Russian TTH recommendations as a gap. Later reviews found some of these sources readable and changed no requirement. The rows are accurate for the iteration they describe.
- **Completeness searches with no new output requirement:**
  - EHF consensus on community pharmacists (J Headache Pain 2025, PMC12054158): no diary or calendar statement in the full text.
  - Swiss SKG treatment recommendations (FMH listing PDF; 2024 Ars Medici summary): no diary statement.
  - IHS early-treatment position statement 2025 (PMID 41134822): its abstract adds no output.
  - Korean Headache Society: press reports only.
  - Hellenic Headache Society: no guideline text found.
  - Swedish: only regional material. The national knowledge-support site still fails TLS (expired certificate).
  - Czech CGRP recommendations (csnn.eu): still behind the declaration page.
  - Japanese guideline: no edition after 2021.
- **Unreachable (official copies tried):**
  - German S1 guideline 030-057: register.awmf.org still serves the anti-bot page. Its journal version (DGNeurologie 2025;8:654–665, doi 10.1007/s42451-025-00829-6, not in the search log) is closed access and Springer returned a client challenge.
  - BASH 2026 advanced-preventives consensus (JNNP, doi 10.1136/jnnp-2026-339062): BMJ and the Birmingham repository both returned 403.
  - IHS RWE guideline 2025: the Copenhagen repository returned 403, and the Leiden repository is a JavaScript application.
  - IHS paediatric update 2023: SAGE returned 403, and there is no repository or PMC copy.

  None of these could be quoted, so none can support a remark.

## Remarks
None.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
