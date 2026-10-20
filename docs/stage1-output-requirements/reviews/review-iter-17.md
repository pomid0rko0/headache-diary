# Review — iteration 17
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v16
Date: 2026-10-20

## Summary
I downloaded every source again with curl into a new, empty folder of my own and used no files that earlier agents left in the shared scratchpad. All 54 URLs returned HTTP 200: the 46 section-5 sources (S-026 included), the English SFEMC Parts 1 and 2, the IHS listing page, the BASH contents page, the Swedish Kela page, the SEN and FDA landing pages, and the PubMed abstracts through E-utilities. S-034 needed two retries after connection resets. A script extracted 300 quoted strings from the Evidence and Caveats lines of section 3: quotes, list items, grade labels and figure column headers. 286 matched by script, and I confirmed the other 14 by hand on the `-layout` text, on page renders or on the embedded figure images. All 300 are verbatim at their URLs, and all 175 page-located quotes are on their stated page.

Then I read every one of the 258 distinct quotes in its source context, with at least 700 characters either side and the full section where relevance was in doubt. I read all 70 translations against their originals, and I re-derived the v16 change to OUT-037 from a 150-dpi render of S-006 p. 10. Every v16 statement about S-006, S-021 and S-022 is accurate. S-006 is now cited only for the tension-type headache clause and as a counter-position, and the conflict is stated. None of the other passages, read in context, contradicts or limits the requirement it supports beyond what the document already says. Strengths, totals, cross-references, scope and citation metadata (37 PMIDs) are in order. Searches in Greek, Latvian, Chinese (Taiwan), German (Austria), Korean and English (India, Pakistan, Philippines, Malaysia, South Africa), and PubMed for 2023–2026, found no missing output requirement I could support with a verified quote, and no superseding edition.

## Verification coverage
"Quotes checked" counts quoted strings on the Evidence and Caveats lines of section 3: quotes, list items, grade labels and figure headers, once per citation. "Manual" means confirmed on the `-layout` text, a page render or the embedded figure image. "Read in context" means I read every distinct quote of that source in its surrounding paragraph and section, and checked it against the clause it supports. Checked separately and not counted here: 142 strings quoted inside locations, 16 quoted strings in Evidence-basis text, and the section 5 strings. All are verbatim or are faithful renderings (see "Other checks").

| Source ID | Quotes checked | Verified verbatim | Read in context (yes/no) | Not found | Unreachable (what you tried) |
|---|---|---|---|---|---|
| S-001 | 24 | 24 (1 manual: 8.2.2 note 1 in the right column of the p. 123 `-layout` text). PDF page = printed page. Also confirmed: 8.2 "expert opinion" sentence (p. 123); A1.1.1 and A1.1.2 note 3 (p. 190) | yes | 0 | — |
| S-002 | 26 | 26 (printed = PDF + 1025) | yes | 0 | — |
| S-003 | 6 | 6 (printed = PDF + 814) | yes | 0 | — |
| S-004 | 10 | 10 (JATS 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5) | yes | 0 | Europe PMC fullTextXML |
| S-005 | 9 | 9 (printed = PDF + 802) | yes | 0 | — |
| S-006 | 9 | 9 (1 manual: the 2.3.3.2 recommendation, where the text layer displaces "curve"; read on a 150-dpi render of p. 10, together with the "second-ary" and "conclu-sive" line breaks). Section 2 is "Drug trials dealing with TTH prophylaxis" (p. 7) | yes | 0 | — |
| S-007 | 8 | 8 (accepted manuscript pp. 20–22, 25) | yes | 0 | — |
| S-008 | 11 | 11 (Q6 Optimal on p. 12 and Q7 Optimal on p. 13, confirmed on renders, not the p. 6 summary table) | yes | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | yes | 0 | — |
| S-010 | 8 | 8 (abstract quotes in the efetch abstract; full-text quotes on pp. 3, 7) | yes | 0 | E-utilities efetch for the abstract |
| S-011 | 3 | 3 | yes | 0 | Europe PMC fullTextXML |
| S-012 | 10 | 10 | yes | 0 | Europe PMC fullTextXML |
| S-013 | 10 | 10 | yes | 0 | Europe PMC fullTextXML |
| S-014 | 14 | 14 | yes | 0 | Europe PMC fullTextXML |
| S-015 | 13 | 13 (U+2011 in "menstrual‑related" is in the NICE HTML too; "Published 19 September 2012", "Last updated 3 June 2025") | yes | 0 | — |
| S-016 | 11 | 11 (PDF = printed + 6; "Revised May 2026"; checklist "based on their experience") | yes | 0 | — |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026" on both section pages; dateModified 2026-09-14; contents page "V1.0 2019") | yes | 0 | — |
| S-018 | 15 | 15 (1 manual: 15B, interrupted by "Level C"; levels 12A, 14A–F, 15A–D as stated) | yes | 0 | — |
| S-019 | 3 | 3 (p. 3) | yes | 0 | — |
| S-020 | 5 | 5 (printed = PDF − 3) | yes | 0 | — |
| S-021 | 4 | 4 (pp. 5, 6, 11; 24 January 2007, in force 31 July 2007) | yes | 0 | — |
| S-022 | 6 | 6 (all manual: margin line numbers removed; lines 383–384, 393–394, 421–425, 427–429, 464–465 on pp. 11–13) | yes | 0 | — |
| S-023 | 4 | 4 | yes | 0 | Europe PMC fullTextXML |
| S-024 | 14 | 14 (2 manual: the Rd5 row and the "FORCE DE LA RECOMMANDATION" header with "Fort", on the 2006 × 1337 px Figure 3 image). English Part 1: grading text p. 726, Table 3 p. 731; PubMed abstract of PMID 34340812 uses "we suggest" | yes | 0 | — |
| S-025 | 7 | 7 (2 manual: RT25, cited twice, on the 1864 × 2452 px Figure 1 image under "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE,", "Fort"). English Part 2: methods sentence p. 735; Table 6 pp. 743–744, with Rt25 "Strong" | yes | 0 | — |
| S-026 | 0 (not cited) | — (URL returns HTTP 200; ISBN 978-84-18420-19-1 on PDF p. 4) | — | — | — |
| S-027 | 7 | 7 | yes | 0 | — |
| S-028 | 1 | 1 | yes | 0 | — |
| S-029 | 2 | 2 | yes | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19; "3. udgave") | yes | 0 | — |
| S-031 | 11 (incl. 2 grade labels) | 11 (1 manual: CQ II-2-14 across the side tab, PDF p. 207; grades A and B; printed = PDF − 16) | yes | 0 | — |
| S-032 | 5 | 5 | yes | 0 | — |
| S-033 | 5 | 5 (grade C/5 after 2.5 and 7.1) | yes | 0 | — |
| S-034 | 3 | 3 (cover read on a render: "Год утверждения 2024", three developers) | yes | 0 | Connection reset twice; third attempt succeeded |
| S-035 | 5 | 5 (PDF pp. 48, 78; "Revizyon 01", "Ağustos - 2025") | yes | 0 | — |
| S-036 | 2 | 2 | yes | 0 | — |
| S-037 | 1 | 1 | yes | 0 | Europe PMC fullTextXML |
| S-038 | 1 | 1 | yes | 0 | Europe PMC fullTextXML |
| S-039 | 2 | 2 | yes | 0 | — |
| S-040 | 2 | 2 | yes | 0 | — |
| S-041 | 1 | 1 | yes | 0 | Europe PMC fullTextXML |
| S-042 | 3 | 3 | yes | 0 | Europe PMC fullTextXML |
| S-043 | 1 | 1 | yes | 0 | Europe PMC fullTextXML |
| S-044 | 1 | 1 | yes | 0 | E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113, 395; printed = PDF − 2) | yes | 0 | — |
| S-046 | 3 | 3 (printed = PDF − 3; "Draft", docket FDA-2022-D-1729 on the landing page) | yes | 0 | — |
| **Total** | **300** | **300** (286 script, 14 manual) | **all 258 distinct quotes** | **0** | — |

### Other checks
- **Translations.** I read all 70 translations against their originals: Dutch, Danish, German, French, Spanish, Portuguese, Italian, Finnish, Russian, Turkish, Chinese and Japanese. All are faithful. Bracketed subjects ("[Keeping a headache diary before the consultation]", "[Indicators of the effectiveness of preventive treatment]") render omitted source text correctly.
- **Omissions and cut quotes.** Every "[...]" omits only recording or calculation text, cross-references, age limits or other list items. I read each omitted passage in the source.
  - Quotes cut at the start or end without "[...]" do not change their meaning. Examples are S-015 1.3.24 and 1.3.29, S-031 CQ I-4 and CQ II-1-6, and the ICHD-3 1.3 note 5.
  - The S-031 CQ I-4 quote leaves out the lead-in "また，客観的に頭痛による生活支障度や治療効果を評価するツールとして，" ("also, as tools to objectively evaluate headache-related impairment of daily life and treatment effect"). Keeping it would only strengthen the support for OUT-026.
- **Locations.** All 175 quotes with a page are on the stated page under the page conventions in section 5. I checked these by hand on renders:
  - the S-008 Q6 and Q7 "Optimal" columns (pp. 12–13);
  - the S-031 CQ VI-3 sentence, which falls after the p. 354 footer and so is on p. 355;
  - the S-034 7.1 recommendation on p. 34 and the S-035 Algoritma 13 on PDF p. 78.
- **Section 5.** These strings were checked in the downloaded sources:
  - S-016 "Revised May 2026";
  - S-021 and S-022 dates and document numbers;
  - S-024 and S-025 grading texts and tables in the English versions;
  - S-028 GRADE sentence; S-032 GRADE sentences and IPGRP2022CN297;
  - S-035 ISBN and revision; S-036 volume, supplement and DOI;
  - S-045 ISBNs, "quinta edición", methodology and landing-page date;
  - S-046 draft labels and docket; NICE dates; BASH footers and dateModified;
  - the IHS listing page, which links both English SFEMC PDFs.
- **Metadata.** All 37 PMIDs (esummary) match the authors, titles, journals, volumes, pages, DOIs and PMCIDs given in section 5 and the search log.
- **Totals and IDs.** By the stated rule there are 39 requirements: 10 MUST, 24 SHOULD, 4 MAY and 1 SHOULD NOT. There are 46 source rows, and 45 sources are cited (all but S-026). There is no dangling OUT reference and no RFC 2119 term before "Strength:". The v16 change-log counts are correct: OUT-037 has 6 Evidence quotes, up from 4, and 2 Caveat quotes. history/v16.md is byte-identical to OUTPUT_REQUIREMENTS.md, and `diff history/v15.md history/v16.md` touches only the header, OUT-037, section 4 and the change log.
- **Scope.** I read every Statement, Rationale, Evidence basis and Caveat. None describes input data, storage or a derivation rule beyond the unit and statistic examples accepted in earlier iterations. The v16 OUT-037 text names AUC without restating how it is calculated: the fixer paraphrased "(also called headache index)" rather than quote the calculation sentence.

### OUT-037 (changed in v16, R16c-01): verified in context
- **S-006 section 2.3.3.2 (p. 10, in section 2 "Drug trials dealing with TTH prophylaxis").** The text supports each part of v16:
  - the recommendation allows AUC as the primary efficacy measure, so "in preventive trials" in the Statement is accurate;
  - the comments call one form of AUC a headache index;
  - they find AUC "more sensitive than days with headache for trials in CTTH";
  - they warn of faulty weighting by multiplication, and they also mention problems with recording intensity and duration, which is not an EMA reason. "Of the EMA reasons, it shares only the warning about faulty weighting" is therefore accurate;
  - they ask for days with headache to be presented as a secondary measure, and they end with "no conclusive data".
- **S-021 (EMA 2007).** It is a migraine-only guideline, and the index sentence sits under "Migraine prophylaxis trials".
- **S-022 (EMA 2026 draft).** It covers migraine and cluster headache. Lines 421–425 sit in 5.2.3 "Endpoints" of the migraine prophylaxis section.
- **Caveat on other headache types.** PubMed shows no newer IHS TTH trial guideline (searches for 2011–2026 and for IHS guideline titles 2023–2026), and the IHS guidelines of 2023–2026 cover other topics. The caveat's statement that neither source applies its position to the other headache type is therefore accurate.
- **Strength.** SHOULD NOT for migraine rests on regulatory guidance, below the MUST threshold. SHOULD for the TTH clause rests on an international trial-methodology guideline's "should". Both are proportionate, and the Strength line names all three clauses.

### Checked and not raised
- **Section 3 preamble and Strength lines.** The preamble's list "(MUST, SHOULD, MAY, SHOULD NOT)" omits MUST NOT, which OUT-016 uses. The Strength lines of OUT-003, OUT-016 and OUT-020 do not name their SHOULD NOT or MUST NOT clauses, while those of OUT-028 and OUT-037 do. No rule requires an exhaustive list, each negative clause matches the strength of its requirement, and review 16 reached the same conclusion for the preamble. No change is required.
- **OUT-024 and S-013 "Drug failure", paragraph 2.** After the quoted third sentence, the source says "we support the use of drugs in the same class, but with a different mechanism of action (e.g. topiramate and valproate)". This does not contradict grouping by class: the list still shows each treatment individually.
- **OUT-029 and S-033 section 2.5.** The graded C/5 recommendation applies "в специализированных центрах боли и головной боли" (in specialised pain and headache centres). The translation states this, and the MUST rests on ICHD-3, so nothing is misstated.
- **OUT-039 and OUT-034.** OUT-039 asks for adherence in the clinician summary. OUT-034's list ("the outputs most used in consultations") does not name OUT-039. The list is not stated to be exhaustive, both are SHOULD, and the link was designed that way in fix 01. No contradiction.
- **OUT-007 caveat.** It cites [S-022] without a quote in OUT-007. The S-022 primary-endpoint sentence is quoted in OUT-005, as earlier reviews noted.
- **OUT-028 and S-027.** In context, the NVN working group advises e-questionnaire plus e-diary screening as a tool before consultations, with the diagnosis made by the physician. This is consistent with OUT-028's SHOULD NOT on assigning a diagnosis.
- **Completeness searches, no new quotable output requirement:**
  - **Greek:** only press items on the Hellenic Headache Society.
  - **Latvian:** no national migraine guideline on spkc.gov.lv; a doctus.lv review article only.
  - **Chinese (Taiwan):** the 2022 Taiwan prevention guideline (Acta Neurol Taiwan 31(3):164–202, PMID 36089629) is abstract-only and concerns drug choice. Taiwanese media report that diaries support National Health Insurance reimbursement applications, which OUT-025 already covers.
  - **German (Austria):** no ÖKSG recommendation text. The DMKG Arztbrief contents document was already assessed in review 16b.
  - **Korean:** no guideline text after 2019.
  - **English (India):** only a 2024 industry-supported amitriptyline Delphi (Cureus) and the 2011 IAN guideline.
  - **English (Philippines):** only a practice survey.
  - **English (Malaysia, South Africa):** no guideline found.
  - **English (Pakistan):** "National Guidelines for The Treatment Of Common Headaches Disorders in Pakistan" (Pak J Neurol Sci 2023;18(2), article 8; https://ecommons.aku.edu/pjns/vol18/iss2/8/) is not in the search log. The PDF returned a Cloudflare challenge (HTTP 403) to curl, and WebFetch showed only the title and authors. It could not be quoted, so it supports no remark. It is in English, so it is not a language gap.
  - **Spanish:** the SEN/semFYC/SEMERGEN/AEMICE consensus (Med Clin 2024) was already logged by review 02 as abstract-only. The SEN 2026 manual (S-045) is the current Spanish source.
- **Newer editions.** None supersedes a cited source. There is no IHS TTH trial guideline after S-006 (2010). The IHS guidelines of 2023–2026 cover the paediatric update, PTH, IIH, RWE and neuromodulation. ICHD-4 is still work in progress. S-015, S-016, S-017, S-018, S-021/S-022 and S-046 carry the dates stated in section 5.

## Remarks
None.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
