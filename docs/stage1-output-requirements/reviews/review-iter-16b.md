# Review — iteration 16, re-check b
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v15
Date: 2026-10-20

## Summary
I downloaded every source again with curl into a new, empty folder of my own, and did not reuse the files that earlier agents left in the shared scratchpad. That covers all 46 URLs in section 5, the English SFEMC Parts 1 and 2, the IHS listing page, the BASH contents page, the Swedish Kela page, the SEN and FDA landing pages, 11 Europe PMC full texts and the PubMed records through E-utilities. Every download returned HTTP 200. SIGN and brainmed.com reset the connection once and loaded on retry. A script extracted 295 quoted strings from section 3 (288 evidence and caveat quotes, including list items, plus 7 grade or figure labels) and 138 headings quoted inside locations. All are verbatim at their URLs: 282 quotes matched by script, and I confirmed 13 by hand. Every stated page, JATS section path, NICE number, AAN level and Japanese and Russian grade is correct, and so are the 61 distinct translations, the "[...]" omissions, the citation metadata (27 PMIDs), the totals and the cross-references. I read every Statement clause by clause against its quotes and found no overreach, no strength mismatch and no scope violation. My completeness searches covered Swedish, Norwegian, German, Austrian, Italian, Korean, Japanese, Ukrainian, Bulgarian and Latin-American Spanish sources, plus the US VA/DoD and ACP guidelines and PubMed for 2025–2026. They found no missing output requirement that I could support with a verified quote, and no superseding edition.

## Verification coverage
"Quotes checked" counts quoted strings in section 3 outside the location parentheses: Evidence and Caveat quotes, list items, and grade or figure labels. A quote repeated in several requirements is counted once per citation. "Manual" means confirmed by hand, on the `-layout` text or on the embedded figure image.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 24 | 24 (1 manual: 8.2.2 note 1, `-layout` text of p. 123; pp. 7, 21, 24, 37, 122–124, 190, 209–210 confirmed; PDF page = printed page) | 0 | — |
| S-002 | 26 | 26 (printed = PDF + 1025; 1.1.4, 1.1.9, 1.3.1 a/b and comments, 1.3.2.0, 1.3.2.1.6–8, 1.3.2.3.1–2, 1.3.2.5–5.1, 1.3.2.6.1–3, 1.3.4 confirmed) | 0 | — |
| S-003 | 6 | 6 (printed = PDF + 814; pp. 822–824) | 0 | — |
| S-004 | 10 | 10 (JATS 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5 with their recommendation and comment paragraphs) | 0 | Europe PMC fullTextXML |
| S-005 | 9 | 9 (printed = PDF + 802; "meta-analyses" hyphenated at a line end) | 0 | — |
| S-006 | 5 | 5 (p. 10) | 0 | — |
| S-007 | 8 | 8 (accepted manuscript "v. 3.2", "April 2022"; pp. 20, 21, 22, 25) | 0 | — |
| S-008 | 11 | 11 (Q2 Optimal and Evidence p. 9, Q4 p. 11, Q6 pp. 12–13, Q7 Optimal p. 13) | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | 0 | — |
| S-010 | 8 | 8 (abstract quotes in the efetch abstract; pp. 3, 7) | 0 | pubmed.ncbi.nlm.nih.gov served a challenge page (HTTP 203) to curl; E-utilities efetch used |
| S-011 | 3 | 3 (Methods > "Development of evidence-based recommendations"; questions 3 and 4) | 0 | Europe PMC fullTextXML |
| S-012 | 10 | 10 (Results > Consensus subsections; Discussion paragraphs 2, 5, 6, 7) | 0 | Europe PMC fullTextXML |
| S-013 | 10 | 10 (Results paragraph 4; Discussion > "Drug failure", "Assessment of patients", "Debilitating headache", "Cut-offs values" at the stated paragraph and sentence positions) | 0 | Europe PMC fullTextXML |
| S-014 | 14 | 14 (all JATS paths as stated, including the three v15 "Introduction" locations) | 0 | Europe PMC fullTextXML; the PMC page also loaded |
| S-015 | 13 | 13 (1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37, 1.3.48; "Published: 19 September 2012", "Last updated: 03 June 2025") | 0 | — |
| S-016 | 11 | 11 (PDF = printed + 6; "R" markers on PDF p. 37; 7.3 checklist "based on their experience"; "Revised May 2026") | 0 | First request reset; retry succeeded |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026" on both section pages, dateModified 2026-09-14; contents page "V1.0 2019") | 0 | — |
| S-018 | 15 | 15 (1 manual: 15B, interrupted by "Level C"; levels 12A B, 14A B, 14C B, 14D B, 14E B, 14F B, 15A B, 15B C, 15C A, 15D B in the `-layout` text) | 0 | — |
| S-019 | 3 | 3 (p. 3) | 0 | — |
| S-020 | 5 | 5 (III.B.5, printed pp. 4–5 = PDF pp. 7–8; "February 2018") | 0 | — |
| S-021 | 4 | 4 (pp. 5, 6, 11; Annex title in capitals; "24 January 2007", in effect "31 July 2007") | 0 | — |
| S-022 | 6 | 6 (all manual: margin line numbers removed; lines 383–384, 393–394, 421–425, 427–429, 464–465; sections 5.2.2, 5.2.3, 5.2.5.2; consultation 10 September 2026 – 31 January 2027) | 0 | — |
| S-023 | 4 | 4 ("Hintergrund" paragraphs 5 and 8; "Frage 3", final paragraph) | 0 | Europe PMC fullTextXML |
| S-024 | 13 | 13 (2 manual: Rd5 and "Fort" on the 2006 × 1337 px Figure 3 image; PDF page + 394. English Part 1: section 2.2 grading text p. 726, Table 3 Rd1–Rd10 "Strong" p. 731; English abstract "we suggest" for calendar, HIT-6, HAD and M-TOQ) | 0 | — |
| S-025 | 5 | 5 (2 manual: RT25, cited twice, on the 1864 × 2452 px Figure 1 image, heading "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE,", column "FORCE", "Fort"; RT15–RT32 "Fort", RT33–RT34 "Modéré". English Part 2: methods sentence p. 735; Table 6 Rt15–Rt26 on p. 743 and Rt27–Rt32 on p. 744 "Strong", Rt33–Rt34 "Moderate") | 0 | — |
| S-026 | 0 (not cited) | — | — | Downloaded (superseded entry) |
| S-027 | 7 | 7 (title "Migraine: Organisatie van zorg - digitale dagboeken"; "Publicatiedatum" 04-12-2023) | 0 | — |
| S-028 | 1 | 1 (11-01-2018) | 0 | — |
| S-029 | 2 | 2 (title "Migraine: Monoklonale antilichamen"; 04-12-2023) | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19; "3. udgave", 2020) | 0 | — |
| S-031 | 11 (incl. 2 grade labels) | 11 (1 manual: CQ II-2-14 across the side tab, PDF p. 207 = printed p. 191, grade A. CQ I-10 in the 推奨 box with grade B on PDF p. 48; CQ I-4, II-1-6, II-1-12 and VI-3 on the stated printed pages; ISBN 978-4-260-04698-5) | 0 | — |
| S-032 | 5 | 5 (3.2 "预防性治疗有效性指标", which carries no grade label; 七、治疗 > 1 病人教育; IPGRP2022CN297) | 0 | — |
| S-033 | 6 (incl. 1 grade label) | 6 (pp. 18, 19, 26, 53; grade C/5 after 2.5 and 7.1; "Год утверждения: 2024"; three developers) | 0 | — |
| S-034 | 4 (incl. 1 grade label) | 4 (pp. 34, 50; grade C/5 after 7.1) | 0 | — |
| S-035 | 5 | 5 (PDF pp. 48, 78; ISBN 978-975-590-958-5, Revizyon 01, Ağustos 2025; first edition 2020) | 0 | — |
| S-036 | 2 | 2 (PDF p. 16; Supplement 1, Volume 21, May 2021) | 0 | — |
| S-037 | 1 | 1 (heading printed "PRINCIPLES OF PROPHYLAXIS") | 0 | Europe PMC fullTextXML |
| S-038 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-039 | 2 | 2 (h1 "3007 Atogepantti, … (migreenin estohoito)") | 0 | — |
| S-040 | 2 | 2 (G.U. 93 del 22/04/2025; the square brackets are in the source) | 0 | — |
| S-041 | 1 | 1 ("Conclusion"; panel of 14 specialists from the seven countries named; chair from Singapore) | 0 | Europe PMC fullTextXML |
| S-042 | 3 | 3 (Table 2 row Question 6; Results panel discussion) | 0 | Europe PMC fullTextXML |
| S-043 | 1 | 1 (Abstract > Background; 18 experts; a consensus definition is proposed) | 0 | Europe PMC fullTextXML |
| S-044 | 1 | 1 | 0 | pubmed.ncbi.nlm.nih.gov challenge page (HTTP 203); E-utilities efetch used |
| S-045 | 4 | 4 (PDF pp. 113 and 395 = printed pp. 111 and 393; box items 3 and 4; editors, publisher and both ISBNs) | 0 | — |
| S-046 | 3 | 3 (printed p. 5 = PDF p. 8; lines 163–167, 174–175; landing page "Draft", June 2023, FDA-2022-D-1729) | 0 | — |
| **Total** | **295** | **295** (282 script, 13 manual) | **0** | — |

### Other checks
- **Headings and labels inside locations.** 138 strings. 130 matched by script. I confirmed the other 8 by hand: the S-021 Annex title and the S-037 heading, both printed in capitals, and six figure headings and column labels, read on the S-024 and S-025 images.
- **Translations and omissions.** I read every non-English quote with its translation, and each has one. All translations are faithful. For every quote I also read the source text directly before and after it, to check both the "[...]" omissions and quotes cut at the start or end. Each omission leaves out only recording or calculation detail, age limits, other list items, a back-reference, examples or citation numbers.
- **Metadata.** Authors, journals, years, volumes, pages, DOIs and PMCIDs of 27 PMIDs match esummary. The full AAN/AHS guideline (PMID 42673560, Neurology 2026;107(7):e214881) states in its abstract that it follows "the 2017 edition of the American Academy of Neurology Clinical Practice Guideline Process Manual", as the S-018 entry says.
- **Totals and IDs.** By the stated rule, there are 39 requirements: 10 MUST, 24 SHOULD, 4 MAY and 1 SHOULD NOT. No RFC 2119 term appears before "Strength:". There are 46 source rows, and 45 sources are cited (all but S-026). No ID is duplicated and no OUT reference dangles. Every source named in a Statement, Rationale or Evidence basis has a quote in the same requirement. history/v15.md is byte-identical to OUTPUT_REQUIREMENTS.md, and FROZEN_ITEMS.md does not exist.
- **Support and strength.** Every MUST clause rests on a classification standard, a graded recommendation or an IHS trial-methodology guideline. Every mixed-strength requirement names each strength in its Strength line. Each evidence-basis grade claim matches the source, including the claims that statements are ungraded: SIGN 4.1, China 3.2, SEN 2026 and Japan CQ VI-3, which is commentary text.
- **Scope.** I read every Statement, Rationale, Evidence basis and Caveat, and also ran a keyword scan of the authored text with the quotes stripped out. Neither found input, storage or derivation content beyond the unit and statistic examples accepted in earlier iterations.

### Checked and not raised
- **OUT-016, the ICHD-3 1.3 note 5 quote, cut at the end.** It ends "may be inappropriate for these". The source continues "(assuming that chronicity induced by drug overuse is always reversible)." The parenthesis makes the source's statement more cautious but does not weaken what OUT-016 uses the quote for. The point is that the diagnosis is uncertain, so the indicator must not be presented as a diagnosis, and SIGN 155 states the same point directly: "not all patients overusing acute treatments have MOH". No change is required.
- **OUT-032, Japan CQ II-1-6, cut at the end.** The sentence continues "が，… 頭痛ダイアリーなどでプロスペクティブに毎日収集していくことが重要である". The omitted part is a data-collection instruction (PROCESS.md section 2), and the translation of the quoted part is accurate.
- **OUT-019, S-017.** The next BASH sentence says that for some patients quality of life may be a better marker of success than an absolute number of days. This does not contradict showing absolute values next to relative change, and the Rationale's "BASH states an absolute aim" is accurate.
- **OUT-026 Caveat, "HIT-6 per [S-002] section 1.3.2.6.2".** The licensing sentence is not quoted, but the source reads "Note that HIT-6 needs to be licensed." directly after the quoted sentence. The claim is accurate, which matches how review 15 treated unquoted caveat facts.
- **Completeness searches, no new output requirement:**
  - Swedish: Socialstyrelsen plans national migraine guidelines for 2027. Nationellt kliniskt kunskapsstöd still fails TLS with an expired certificate, and I did not bypass it.
  - Norwegian: no NNF guideline text.
  - German: AWMF 030-057 (2025-11) and the patient version still serve the Anubis page, and so does a TUM repository copy (mediatum 1761606); dgn.org loads only through JavaScript. The DMKG registry document "DMKG-Empfehlungen für die Inhalte eines Kopfschmerz-Arztbriefs" (portal.kopfschmerzregister.de, 2025) lists headache days per month with the severe ones, analgesic days per month, previous prophylaxis with doses and reason for stopping, and questionnaire results. All of these are already covered by OUT-004, OUT-006, OUT-014, OUT-024, OUT-026 and OUT-034.
  - Austrian (ÖKSG) and Italian (SISC/ANIRCEF): only press reports.
  - Korean: press reports only.
  - Japanese: no edition after 2021.
  - Ukrainian: no national migraine protocol; the 2025 Ministry of Health protocol on post-concussion headache is not a migraine source.
  - Bulgarian: nothing found.
  - Mexican and Colombian guidelines: already logged or reviewed.
  - US VA/DoD headache guideline 2023 (healthquality.va.gov): it recommends no diary output and reproduces ICHD-3 text.
  - ACP 2025 prevention and acute guidelines, and the ACP 2026 performance-measure review: drug-choice guidance and performance measures; acpjournals.org returned a Cloudflare 403.
  - EHF sex-specific consensus 2026: no diary statement, as the search log says.
  - PubMed 2025–2026 for IHS, EHF and ICHD: only items already logged, ICHD-4 work-in-progress papers and comments.
- **Still unreachable:** the IHS paediatric update 2023 (SAGE 403; OpenAlex lists no repository copy), as the S-005 entry states.

## Remarks
None.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
