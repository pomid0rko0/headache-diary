# Review — iteration 19, re-check c
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v18
Date: 2026-10-20

## Summary
I downloaded all 46 section-5 sources again with curl into a new, empty folder of my own (`scratchpad/r19c/src`) and did not use any file that earlier agents left in the scratchpad. I also downloaded the English SFEMC Parts 1 and 2, the Swedish Kela page, the BASH contents page, the IHS "Affiliate Society and other guidelines" page, the SEN and FDA landing pages, the PubMed records (E-utilities efetch and esummary) and the Europe PMC fullTextXML of every PMC source. Every request returned HTTP 200. All 310 quoted strings on the Evidence and Caveats lines are verbatim at their URLs: 294 matched by script, 6 by script after the S-022 margin line numbers were removed, and 10 by hand, either in the `-layout` text or on the embedded figure images. Every page-located quote is on its stated page. I read all 267 distinct quotes in their source context and checked each Statement clause by clause against them. I found no misquote, no wrong metadata, no element unsupported at its stated strength, no source that says the opposite in context, no definition coverage gap, no scope violation and no contradiction. My completeness searches (German, Danish, Chinese, Japanese, Italian, Polish, Korean, Norwegian, and Europe PMC 2021–2026) found no missing evidence-based output requirement and no superseding edition.

## Verification coverage
"Quotes checked" counts the quoted strings on the Evidence and Caveats lines of section 3, once per citation: quotes, list items and grade labels, 310 in all.

"Verified verbatim" means the string matched the downloaded text after normalising Unicode form, quote marks, dashes and whitespace, with "[...]" segments matched in order. "By hand" means I confirmed it in the `-layout` text or on the image.

"Read in context" means I read each distinct quote with 300–450 characters on each side, and the whole section where its role or a definition was at issue. I read these sections in full:
- ICHD-3 item 12, 1.3 notes, 2.2 comment, 8.2 notes and subtypes, A1.1 (pp. 189–190) and "Definitions of terms";
- S-012 Results > Consensus and Discussion;
- S-013 Discussion;
- S-010 "Setting goals";
- S-008 Q2, Q4, Q6 and Q7;
- S-021 p. 5 and Annex;
- S-022 sections 5.1.3–5.2.5;
- S-005 primary and pharmacoeconomic endpoints;
- S-018 pp. 7–8;
- S-031 CQ I-10, II-1-6, II-1-12, II-2-14 and VI-3;
- S-032 sections 2.2–3.2.

Pages were checked by script against the page where each quote was found, using the conventions in section 5. I checked 171 tagged strings inside locations: 160 by script, 5 case-insensitively (headings printed in capitals), 3 in the English SFEMC Part 1, and 3 figure headings on the images. I read all 61 distinct translations against their originals.

| Source ID | Quotes checked | Verified verbatim | Read in context (yes/no) | Not found | Unreachable (what you tried) |
|---|---|---|---|---|---|
| S-001 | 24 | 24 (1 by hand: 8.2.2 note 1 in the right column of the p. 123 `-layout` text); PDF page = printed page | yes | 0 | — |
| S-002 | 26 | 26 (PDF page labels 1026–1044) | yes | 0 | — |
| S-003 | 6 | 6 (printed = PDF + 814) | yes | 0 | — |
| S-004 | 10 | 10 (Europe PMC fullTextXML) | yes | 0 | — |
| S-005 | 9 | 9 (1 by hand: "meta-" line-end hyphen, PDF p. 8 = p. 810) | yes | 0 | — |
| S-006 | 9 | 9 (1 by hand: 2.3.3.2 recommendation, where the text layer displaces "curve"; read in the `-layout` text of p. 10) | yes | 0 | — |
| S-007 | 8 | 8 (accepted manuscript pp. 20–22, 25) | yes | 0 | — |
| S-008 | 14 | 14 (pp. 9, 11–13; Q6 list items in the p. 12 wording "person with migraine") | yes | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | yes | 0 | — |
| S-010 | 9 | 9 (2 citations by hand: "patient-" line-end hyphen, p. 7; abstract quotes in the efetch abstract) | yes | 0 | — |
| S-011 | 3 | 3 | yes | 0 | — |
| S-012 | 15 | 15 | yes | 0 | — |
| S-013 | 13 | 13 | yes | 0 | — |
| S-014 | 14 | 14 | yes | 0 | — |
| S-015 | 13 | 13 (recommendation numbers 1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37 and 1.3.48 confirmed; published 19 September 2012, last updated 03 June 2025) | yes | 0 | — |
| S-016 | 11 | 11 (PDF = printed + 6; "Revised May 2026"; SIGN key to strong/conditional recommendations, PDF p. 2) | yes | 0 | — |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026", dateModified 2026-09-14 on both section pages; contents page "BASH Guideline V1.0 2019") | yes | 0 | — |
| S-018 | 15 | 15 (1 by hand: 15B, interrupted by "Level C"; levels of 12A, 14A, 14C–14F and 15A–15D read in the `-layout` text of pp. 7–8) | yes | 0 | — (aan.com redirects to the AAN blob-storage PDF) |
| S-019 | 3 | 3 (p. 3) | yes | 0 | — |
| S-020 | 5 | 5 (printed = PDF − 3) | yes | 0 | — |
| S-021 | 5 | 5 (pp. 5, 6, 11) | yes | 0 | — (HTTP 301 to the ...revision-1_en.pdf copy of the same guideline) |
| S-022 | 6 | 6 (after removing the margin line numbers; lines 383–384, 393–394, 421–425, 427–429 and 464–465 on pp. 11–13) | yes | 0 | — |
| S-023 | 4 | 4 | yes | 0 | — |
| S-024 | 13 | 13 (1 by hand: Rd5 and "Fort" on the 2006 × 1337 px Figure 3 image; English Part 1: grading text p. 726, Table 3 Rd4–Rd8 "Strong"; abstract "We suggest" wording via efetch) | yes | 0 | — |
| S-025 | 5 | 5 (2 by hand: RT25, cited twice, with "Fort", under "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE," on the 1864 × 2452 px Figure 1 image; column "FORCE") | yes | 0 | — |
| S-026 | 0 (not cited) | — (URL returns HTTP 200) | — | — | — |
| S-027 | 7 | 7 | yes | 0 | — |
| S-028 | 1 | 1 | yes | 0 | — |
| S-029 | 2 | 2 | yes | 0 | — |
| S-030 | 4 | 4 | yes | 0 | — (http redirects to https) |
| S-031 | 11 | 11 (1 by hand: CQ II-2-14 across the side tab, PDF p. 207 = printed p. 191, grade A; grades B on PDF p. 48) | yes | 0 | — |
| S-032 | 5 | 5 | yes | 0 | — (redirects to www.brainmed.com/info/detail?id=34408) |
| S-033 | 5 | 5 (grade C/5 after 2.5 and 7.1) | yes | 0 | — |
| S-034 | 3 | 3 (grade C/5 after 7.1) | yes | 0 | — |
| S-035 | 5 | 5 (PDF pp. 48, 78) | yes | 0 | — |
| S-036 | 2 | 2 | yes | 0 | — |
| S-037 | 1 | 1 | yes | 0 | — |
| S-038 | 1 | 1 | yes | 0 | — |
| S-039 | 2 | 2 | yes | 0 | — |
| S-040 | 2 | 2 | yes | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | yes | 0 | — |
| S-042 | 3 | 3 | yes | 0 | — |
| S-043 | 1 | 1 | yes | 0 | — |
| S-044 | 1 | 1 (efetch abstract) | yes | 0 | — |
| S-045 | 4 | 4 (PDF pp. 113, 395; 612 pages; landing page "Documento PDF incluido en la web de la SEN el 21 de enero de 2026") | yes | 0 | — |
| S-046 | 3 | 3 (landing page "Draft", "Not for implementation. Contains non-binding recommendations.", FDA-2022-D-1729) | yes | 0 | — |
| **Total** | **310** | **310** (294 script, 6 script after removing margin numbers, 10 by hand) | **all 267 distinct quotes** | **0** | none unreachable |

### Other checks
- **Section 5 strings.** I checked every source-language string quoted in section 5, including:
  - the SFEMC grading text and the Table 3 and Table 6 labels;
  - the S-028, S-032 and S-036 grading sentences;
  - the S-045 edition, methodology and Tabla 3 strings;
  - the S-046 draft labels;
  - the BASH version strings;
  - the IHS listing page with both English SFEMC PDFs.

  All match. The remaining unmatched strings are the document's own English translations.
- **Metadata.** esummary for 27 PMIDs matches first authors, journals, years, volumes, issues, pages, DOIs and PMCIDs. S-018 was published online on 31 August 2026 (epubdate) in Neurology 2026;107(7):e214881. The French SFEMC articles list Demarquay, Donnet, Ducros (Part 1) and A. Ducros, G. Demarquay, "E. Donnet" (Part 2), as cited.
- **Totals and IDs.** By the stated rule there are 39 requirements: 10 MUST, 24 SHOULD, 4 MAY and 1 SHOULD NOT. There are 46 source rows, 45 of them cited (all but S-026). No ID is duplicated and no OUT reference dangles. Every [S-NNN] tag in a Statement, Rationale or Evidence basis has a quote in the same requirement, and no RFC 2119 term appears before "Strength:".
  - history/v18.md is identical to OUTPUT_REQUIREMENTS.md.
  - The word diff of v17 and v18 deletes only "v17", "17", "OUT-019).", "2018);" and "v17)", as the v18 change log says.
- **Scope.** I read every Statement, Rationale, Evidence basis and Caveat, and ran a keyword scan of the authored text with quotes removed. I found nothing beyond the unit and statistic examples accepted in earlier iterations ("proportion of days", "average peak intensity", "median attack duration").
- **MUST elements, clause by clause.** Each MUST clause rests on a classification standard, a graded recommendation or an international methodology guideline, read in context:
  - OUT-001: ICHD-3 and IHS paediatric "equivalent" periods;
  - OUT-004: ICHD-3 and Japan CQ I-10 (strong recommendation, certainty B);
  - OUT-005: AAN 15A (level B) and IHS;
  - OUT-014: ICHD-3 8.2 notes for class and individual drug;
  - OUT-016: ICHD-3, SIGN "R" and AAN 12A;
  - OUT-018: NICE 1.3.27–1.3.29, AAN 14A and IHS;
  - OUT-021 core: AAN 15D and IHS section 1;
  - OUT-028: ICHD-3 1.3 and NICE 1.3.29;
  - OUT-029: ICHD-3 item 12 and the 2.2 comment, which continues "if they are to select the right treatment for each while avoiding medication overuse", so it also supports the per-type acute-medication output;
  - OUT-030: NICE 1.2.6 and Japan CQ II-2-14 (strong recommendation, certainty A).
- **Definition coverage.** I re-derived the elements of every definition or criterion that a Statement says its outputs let a reader apply, relate to or follow. All are covered or properly qualified:
  - the EHF effective-treatment, triptan-responder and triptan-refractoriness definitions (OUT-023, OUT-024);
  - ICHD-3 8.2 and 8.2.6 (OUT-014, OUT-016);
  - ICHD-3 1.3 and 2.3 (OUT-028, "relate the pattern to");
  - ICHD-3 A1.1 (OUT-030);
  - the ICHD-3 cluster period and remission period (OUT-031, qualified);
  - the IHS 2025 control levels, IHS Q6, NICE 1.3.28 and DMKG (OUT-020; the levels count days with migraine or moderate-to-severe headache under the panel's own migraine-day definition, which the general clause of OUT-020 and the label of OUT-002 cover);
  - the scheme windows (OUT-025).

### Checked and not raised
- **Page conventions for S-002, S-003, S-005 and S-020.** Their bare page numbers are printed pages, and section 5 gives no offset for them. Fix-iter-15 noted this, and review 16 decided it with a justification ("No location sends a reader to the wrong passage"). I have no new evidence against that decision:
  - the S-002 PDF's own page labels are 1026–1044;
  - the S-003 and S-005 journal pages cannot be mistaken for PDF indices;
  - the S-020 locations name section III.B.5.
- **OUT-028 Rationale, "national guidelines direct clinicians to establish headache and migraine days per month over the last three months from the diary".** Only the Russian recommendations (S-033) say "over the last 3 months". Japan (CQ II-1-12: at least one month of diary for the diagnosis) and NVN support diary-based classification without that period. The national reimbursement schemes cited in OUT-025 (Kela, AIFA) also use the three preceding months. The MUST rests on ICHD-3 and NICE 1.3.29, and the plural is a compression of the Rationale rather than a misstatement that changes any element or strength.
- **OUT-011 example "hours with moderate/severe pain per 28 days" against OUT-037.** S-002 1.3.2.1.6 lists cumulative hours of moderate/severe pain as a headache-related secondary endpoint whose reductions "may be clinically meaningful". Neither EMA document calls such a measure a headache index. OUT-011 does not present it as a primary measure, and OUT-037 restricts only indices presented as primary measures for migraine. There is no contradiction.
- **OUT-021 "against the patient's own goals" (AAN 15C, level A).** No cited source asks a diary output to show the goals. S-010 speaks of supplementing migraine frequency "with personalized goals and patient-reported outcome measures" in the clinician's approach. Fix-iter-18 reached the same conclusion, and the Statement does not claim that the output shows the goals.
- **ICHD-3 A1.1 comments on withdrawal bleeding.** The comments say that research should separate natural menses from progestogen-withdrawal bleeding and that "Management strategies may also differ". This is a research and management note, not a criterion of A1.1. OUT-030 claims only to distinguish the window as defined.
- **S-021 Annex.** The Annex asks for efficacy to be shown separately for children (6 to under 12 years) and adolescents (12 to 18 years). This is a requirement for regulatory trials; no clinical source asks a diary output for that split. Not a missing requirement.
- **AAN 16B (level A, monitor adverse events at follow-up).** This is a clinician action, as earlier reviews noted. OUT-024 shows adverse effects at SHOULD, by the same reasoning the document applies to SFEMC Rd5 and RT25 in OUT-033.
- **National reimbursement schemes not in the search log.** These are further examples of the scheme-specific windows that OUT-025 already covers at MAY. None changes a requirement:
  - Norway (Legemiddelverket and Helsedirektoratet, individual reimbursement of CGRP antibodies): a diary from 4 weeks before the start, and assessment after 12 weeks against a reduction in days with moderate to severe migraine; known only from a 2022 NHI.no summary;
  - Poland (drug programme B.133): a diary of at least 3 months, with MIDAS;
  - Korea: reimbursement criteria reported in the medical press.
- **Newer editions.** None supersedes a cited source:
  - Japan 2021 is still current (only a provisional JHS CGRP guidance has been added);
  - the DHOS reference programme is still the 3rd edition (2020);
  - apicr.minzdrav.gov.ru serves byte-identical files for 295_4/295_6 (MD5 8fc92ed7adc7…) and 169_4/169_5 (MD5 aa1f5e033134…; 295_5 and 169_3 reset the connection on this run);
  - the SIGN 155 front page reads "Revised May 2026", and NICE CG150 was last updated on 03 June 2025;
  - the EMA Rev. 2 consultation runs from 10 September 2026 to 31 January 2027, and the FDA preventive guidance is still a draft;
  - Europe PMC 2025–2026 searches of IHS, EHF and AHS titles, of guideline and consensus titles, and of diary consensus and core outcome sets found no new edition and no diary-output consensus; COSMIG was already assessed in review 19b.
- **Still unreachable.** I did not try to get past any protection:
  - AWMF S1 030-057 (2025-11): curl received the Anubis page "Making sure you're not a bot!";
  - IHS paediatric update 2023 (PMID 37226450): SAGE returned HTTP 403 to curl and WebFetch, Unpaywall lists only the SAGE copy, and Europe PMC lists it as not open access;
  - CMA (CSN) 2023 Chinese migraine guideline: no full text found;
  - Italian SISC: only press reports of the 2025 SISC–IHS guideline (PMID 40277319, already assessed in review 11 as drug-choice guidance).

  These match the S-005 entry and the search log.

## Remarks
None.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
