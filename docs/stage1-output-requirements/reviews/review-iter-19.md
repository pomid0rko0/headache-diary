# Review — iteration 19
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v18
Date: 2026-10-20

## Summary
I downloaded every section-5 source again with curl into a new, empty folder of my own (`scratchpad/r19/src`), and did not use files left by earlier agents. The downloads also included the English SFEMC Parts 1 and 2, the BASH contents page, the Swedish Kela page, the FDA and SEN landing pages, the PubMed records (E-utilities) and the Europe PMC fullTextXML of every PMC source. All 310 quoted strings on the Evidence and Caveats lines are verbatim at their URLs (297 by script, 6 by script after removing the printed margin line numbers, 7 by hand on page renders or in the `-layout` text). The 156 strings quoted inside locations are also correct, every stated page matches, and I judged all 70 translations faithful. I read every distinct quote in context, with the v18 passages read in full. The v18 changes to OUT-020, OUT-023, OUT-024 and OUT-031 are accurate and in scope. With them, the EHF definitions that OUT-023 and OUT-024 say their outputs let a reader apply are fully covered, and the claims in OUT-024 and OUT-031 are properly qualified. None of the three "Observed, not changed" items in fix-iter-18.md requires a change. Completeness searches in Canadian English and French, Hungarian, Mexican Spanish, Catalan and Brazilian Portuguese, a re-read of the Italian Delphi, and PubMed 2025–2026 found no missing output requirement and no superseding edition.

## Verification coverage
"Quotes checked" counts the quoted strings on the Evidence and Caveats lines of section 3 once per citation: quotes, list items and grade labels, 310 in all. "Read in context" means I read each distinct quote with at least 450 characters on each side in the downloaded text, and the whole section where its role mattered. I read in full: S-012 Results > Consensus and Discussion; S-013 Results and Discussion; S-008 p. 12; S-010 p. 6; S-021 pp. 5–6; S-045 PDF pp. 112–113. Location strings (156) were checked separately: 153 by script, and 3 figure headings on the images. Each stated page was checked against the page where the quote was found, using the page conventions in section 5.

| Source ID | Quotes checked | Verified verbatim | Read in context (yes/no) | Not found | Unreachable (what you tried) |
|---|---|---|---|---|---|
| S-001 | 24 | 24 (1 by hand: 8.2.2 note 1, in the right column of the p. 123 `-layout` text and on a 150-dpi render). PDF page = printed page | yes | 0 | — |
| S-002 | 26 | 26 (printed = PDF + 1025); section labels 1.1.4, 1.1.9 and 1.3.4 spot-checked against the preceding headings | yes | 0 | — |
| S-003 | 6 | 6 (printed = PDF + 814) | yes | 0 | — |
| S-004 | 10 | 10 | yes | 0 | The PMC page returned a bot-challenge page to curl; the Europe PMC fullTextXML was used |
| S-005 | 9 | 9 (printed = PDF + 802) | yes | 0 | — |
| S-006 | 9 | 9 (1 by hand: the 2.3.3.2 recommendation, whose text-layer line displaces "curve"; read in the `-layout` text and on a render of p. 10) | yes | 0 | — |
| S-007 | 8 | 8 (accepted manuscript pp. 20–22 and 25; printed page = PDF page) | yes | 0 | — |
| S-008 | 14 | 14 (v18 Q6 introduction and list items on p. 12) | yes | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | yes | 0 | — |
| S-010 | 9 | 9 (abstract quotes in the efetch abstract; v18 "Optimal Control" quote on p. 6) | yes | 0 | The PubMed page returned HTTP 203 (a challenge page) to curl; E-utilities efetch was used |
| S-011 | 3 | 3 | yes | 0 | The PMC page returned a challenge page; Europe PMC was used |
| S-012 | 15 | 15 (also matched on the PMC page; v18 sentences: paragraph "This definition is not specific for triptans", s6–s7; Discussion ¶1) | yes (whole Results > Consensus and Discussion) | 0 | — |
| S-013 | 13 | 13 (also on the PMC page; v18 Caveat sentences: "Drug failure" ¶5 s2; "Debilitating headache" ¶1 s1) | yes (full text) | 0 | — |
| S-014 | 14 | 14 | yes | 0 | The PMC page returned a challenge page; Europe PMC was used |
| S-015 | 13 | 13 (Published 19 September 2012; last updated 03 June 2025) | yes | 0 | — |
| S-016 | 11 | 11 (PDF = printed + 6; "First published February 2018 / Revised May 2026") | yes | 0 | — |
| S-017 | 3 | 3 (all from the 2.1.3 page; footer "BASH Guideline V2.0 2026" and dateModified 2026-09-14 on both section pages; contents page shows "V1.0 2019") | yes | 0 | — |
| S-018 | 15 | 15 (1 by hand: 15B, interrupted by "Level C"; levels of 12A, 14A–14F and 15A–15D read in the `-layout` text) | yes | 0 | — (aan.com redirects twice to the aanfiles.blob.core.windows.net PDF dated 2026-08-31) |
| S-019 | 3 | 3 (p. 3) | yes | 0 | — (same redirect pattern as S-018) |
| S-020 | 5 | 5 (printed = PDF − 3; landing page: "Final", February 2018) | yes | 0 | — |
| S-021 | 5 | 5 (v18 quote on p. 5, the sentence directly before the duration sentence) | yes | 0 | — (HTTP 301 to ...revision-1_en.pdf, 12 pages, the same guideline) |
| S-022 | 6 | 6 (by script after removing margin line numbers; lines 383–384, 393–394, 421–425, 427–429 and 464–465 confirmed in the `-layout` text) | yes | 0 | — |
| S-023 | 4 | 4 | yes | 0 | — |
| S-024 | 13 | 13 (1 by hand: Rd5 and "Fort" on the render of PDF p. 8 = printed p. 402; English Part 1 Table 3, Rd5 "Strong", PDF p. 7) | yes | 0 | — |
| S-025 | 5 | 5 (2 by hand: RT25 under "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE," with "Fort", on the render of PDF p. 3 = printed p. 414; English Table 6, Rt25 "Strong", PDF p. 10 = printed p. 743) | yes | 0 | — |
| S-026 | 0 (not cited) | — (URL returns HTTP 200) | — | — | — |
| S-027 | 7 | 7 (Publicatiedatum 04-12-2023) | yes | 0 | — |
| S-028 | 1 | 1 (Publicatiedatum 11-01-2018) | yes | 0 | — |
| S-029 | 2 | 2 (Publicatiedatum 04-12-2023) | yes | 0 | — |
| S-030 | 4 | 4 (PDF page = printed page) | yes | 0 | — (http redirects to https) |
| S-031 | 11 | 11 (1 by hand: CQ II-2-14, across the side tab, on the render of PDF p. 207 = printed p. 191, grade A; printed = PDF − 16 confirmed on pp. 32, 123 and 355) | yes | 0 | — |
| S-032 | 5 | 5 | yes | 0 | Connection reset twice; a retry succeeded. The listed URL redirects to https://www.brainmed.com/info/detail?id=34408, which carries the same text |
| S-033 | 5 | 5 (printed = PDF page; grade C/5 after 2.5 and 7.1) | yes | 0 | Connection reset on the first attempts; a retry succeeded |
| S-034 | 3 | 3 (cover page rendered: "дети", "Год утверждения 2024") | yes | 0 | — |
| S-035 | 5 | 5 (PDF pp. 48 and 78; ISBN 978-975-590-958-5 for publication no. 1344, revision "Ağustos - 2025") | yes | 0 | — |
| S-036 | 2 | 2 (PDF p. 16; DOI printed on PDF p. 5) | yes | 0 | — |
| S-037 | 1 | 1 | yes | 0 | — |
| S-038 | 1 | 1 | yes | 0 | — |
| S-039 | 2 | 2 | yes | 0 | — |
| S-040 | 2 | 2 | yes | 0 | — |
| S-041 | 1 | 1 (panel of 14 from the 7 places listed; the chair from Singapore was not a panellist) | yes | 0 | — |
| S-042 | 3 | 3 | yes | 0 | The PMC page returned a challenge page; Europe PMC was used |
| S-043 | 1 | 1 (eDelphi, 18 experts) | yes | 0 | The PMC page returned a challenge page; Europe PMC was used |
| S-044 | 1 | 1 (efetch abstract) | yes | 0 | — |
| S-045 | 4 | 4 (PDF pp. 113 and 395; printed = PDF − 2; ISBNs, fifth edition, Tabla 3 on PDF p. 17; landing page "21 de enero de 2026") | yes | 0 | — |
| S-046 | 3 | 3 (printed = PDF − 3; landing page "Draft", June 2023, FDA-2022-D-1729) | yes | 0 | — |
| **Total** | **310** | **310** (297 script, 6 script after removing margin line numbers, 7 by hand) | **all ~265 distinct quoted strings** | **0** | none unreachable |

### Other checks
- **v18 changes.** `diff history/v17.md history/v18.md` and `git diff --word-diff` show changes only in the header, OUT-020, OUT-023, OUT-024 (a new Caveat), OUT-031 (one Caveat sentence), section 4 and the change log. The only deleted words are the version numbers, "OUT-019)." and "2018);", which matches the v18 change log. history/v18.md is byte-identical to OUTPUT_REQUIREMENTS.md.
  - **OUT-023.** The new Statement, Rationale and Evidence-basis text paraphrases S-012 correctly. The definition's time frame ("Reaching, within 2 h ... and maintaining, for at least 24 h") governs all three components, and the panel preferred a broad notion of non-pain symptoms (s6–s7). The definition is patient-centred (Discussion ¶1), and item C reads "No meaningful drug-related adverse events". The EMA 2007 sentence names "the maintenance of the effect, relapses and effects on migraine-associated symptoms other than pain ... at short-term" as important secondary endpoints, so "also supported by" is a fair description. "No recommendation grade" is true for both S-012 statements.
  - **OUT-020.** The S-008 Q6 Optimal-level list (p. 12) and the S-010 Optimal Control definition (p. 6) match the new Rationale and Evidence-basis text. The DMKG/ÖKSG/SKG criterion in the existing [S-023] quote names HIT-6 and MIDAS.
  - **OUT-024 and OUT-031 Caveats.** They match S-013 ("Contraindicated drugs are considered ..."; "rely on the presence of a given number of days of debilitating headache attacks"), NICE 1.3.24 ("or are unsuitable because of safety concerns") and the ICHD-3 remission definition (p. 209).
  - **Scope.** No v18 text says how anything is recorded or computed, and none restates a numeric criterion. The per-attack status at 2 and 24 hours and the patient's view of adverse events are described as properties of the output.
- **Definition coverage (fix-iter-18 analysis).** I re-derived the elements of each named definition from the sources and found no gap.
  - **EHF effective attack treatment and triptan response [S-012].** Components A, B and C at 2 hours and 24 hours; consecutive attacks; timing of intake; formulation; rescue use. Dose is cross-referenced to OUT-024, and no EHF definition uses dose as a criterion.
  - **EHF triptan refractoriness.** Covered by the per-triptan list grouped by class, with formulation.
  - **Limited claims.** The claims in OUT-016 (criterion B of ICHD-3 8.2 only), OUT-018, OUT-021, OUT-025, OUT-028 and OUT-030 are already limited to what their outputs show.
  - **Qualified claims.** The claims in OUT-024 (EHF resistant/refractory categories, NICE 1.3.24) and OUT-031 (remission non-inducibility) are now properly qualified.
  - **ICHD-3 A1.2.0.1/A1.2.0.2.** ICHD-3 also defines pure menstrual and menstrually related migraine with aura, with the same window. OUT-030 names only A1.1, but it claims only to distinguish the window as defined, so this is not a defect.
- **Translations and omissions.** I read all 70 translations against their originals (Dutch, Danish, German, French, Spanish, Portuguese, Italian, Finnish, Russian, Turkish, Chinese, Japanese) and found all faithful. I also checked every "[...]" and every quote cut at its start or end. Examples: S-001 A1.1 omits "prospectively recorded"; S-002 1.3.2.1.6 omits "can be calculated with data from electronic diaries,"; S-031 CQ II-1-6 is cut before the clause on prospective daily collection; S-006 2.3.3.2 omits "However, there are problems with recording ...". Each omission removes data-collection text, references, list items or age limits, and none changes the meaning.
- **Grades and types.** The following match the sources: AAN levels (12A, 14A–14F, 15A–15D); the Japanese grades A and B; the Russian C/5 grades; the SFEMC "Fort"/"Strong" ratings (Figure 3, Figure 1, Table 3, Table 6) and the abstract wording "we suggest" (PMID 34340812); SIGN "R" (pp. 6 and 31); the ICHD-3 statement that the day limits are based on expert opinion (p. 123); the ungraded status of SIGN 4.1, China 3.2, SEN 2026 (box items and the running-text MIDAS/HIT-6 sentence), Japan CQ VI-3 and SFEMC p. 401.
- **Metadata.** All 27 PMIDs I queried (esummary) match authors, journals, years, volumes, pages, DOIs and PMCIDs. S-018 is Neurology 2026;107(7):e214881 (issue date October 2026; the document gives online publication on 31 August 2026, and the AAN PDF is dated 2026-08-31). The S-022 consultation dates match the PDF.
- **Totals and IDs.** The stated rule gives 39 requirements: 10 MUST, 24 SHOULD, 4 MAY and 1 SHOULD NOT. There are 46 source rows, 45 of them cited (all but S-026). No ID is duplicated and no OUT reference dangles. Every [S-NNN] tag in a Statement, Rationale or Evidence basis has a quote in the same requirement. No RFC 2119 term appears in an Evidence-basis line before "Strength:".
- **Scope (whole document).** I read every Statement, Rationale, Evidence basis and Caveat. None describes input data, storage or a derivation rule beyond the unit and statistic examples accepted in earlier iterations.

### Decisions on fix-iter-18 "Observed, not changed"
1. **S-021 URL redirect.** No change required. The listed URL answers HTTP 301 and resolves to the same 12-page guideline, with every quote on its stated page. A working redirect is neither a broken nor a wrong link (PROCESS.md section 9). The same holds for the other redirects I observed: S-018 and S-019 (aan.com to the AAN blob-storage PDFs), S-030 (http to https) and S-032 (to www.brainmed.com/info/detail?id=34408).
2. **Search log, Italian row (Barbanti et al. 2026 Delphi).** No change required. The row states nothing false: it records the AIFA search and the SISC/ANIRCEF gap. PROCESS.md section 4 asks for a log of searches, and an item a reviewer found and the fixer declined to cite does not make that log wrong. I read the Delphi myself (Europe PMC, PMC13183690):
   - its diary statements concern recording (statements 9, 10, 14);
   - statement 21 restates the EHF definition already covered by OUT-023;
   - statement 27 ("≥ 10 triptans or ≥ 15 NSAIDs per month") is a referral trigger in doses, not a redefinition of medication overuse.
   It is an industry-funded single-country panel and supports no missing output or strength change.
3. **OUT-019 Rationale ("EHF defines difficult-to-treat migraine by absolute numbers of debilitating days").** No change required. S-013 Discussion ("Cut-offs values") says the group "opted to use 8 days per month as cut-off values" rather than percent reductions. OUT-019 does not claim to let that definition be applied.

### Checked and not raised
- **Canadian Headache Society, Updated Migraine Prevention Guideline (Medrea I, Cooper P, et al. Can J Neurol Sci 2024; PMID 39506371; doi 10.1017/cjn.2024.285; full text served on the Cambridge Core page).** Canada (English and French) has no row in the search log. Its Part 2 expert-consensus answers support existing requirements and add no output:
  - "Headache diaries are important in evaluating treatment effectiveness ..." (OUT-018, OUT-034);
  - "Headache frequency or intensity is reduced by 50% or more ..." (OUT-010, OUT-018);
  - MIDAS and HIT-6 change (OUT-026);
  - tapering and restarting if symptoms recur (OUT-022).
  So the language-coverage gap hides no requirement, and I do not raise it.
- **Hungary.** Search results summarise a 2026 Hungarian ministerial decree (12/2026 BM rendelet, via a Semmelweis University neurology clinic letter): CGRP-antibody reimbursement requires a headache diary kept for at least 3 months, and stopping after 12 weeks without a 50% (chronic migraine: 30%) reduction documented by diary. These are further scheme-specific windows of the kind OUT-025 (MAY) already covers. They do not change OUT-025.
- **Mexico (IMSS GPC IMSS-047-08, 2016 update, GER and GRR PDFs from imss.gob.mx).** No headache-diary statement.
- **Catalan and Brazilian Portuguese.** No Catalan guideline text was found. The SBCe chronic-migraine consensus is from 2019, and no newer edition was found.
- **PubMed 2025–2026 (IHS, EHF and AHS in titles).** Nothing new bears on outputs:
  - AHS telemedicine position statement 2026 (PMC12951699): mentions e-diaries with video consultations, no output requirement;
  - EHF community-pharmacist position statement 2025 (PMC12054158): no diary statement;
  - EHF sex-specific consensus 2026: already logged;
  - AAN/AHS full guideline (PMID 42673560): S-018 is its clinician summary;
  - no new edition of the IHS trial guidelines, ICHD-3 or the EHF documents cited.
  The IHS classification committee page lists an ICHD-IV workshop (September 2025) but no published ICHD-4. The FDA acute guidance is still the final February 2018 version; the preventive guidance is still a June 2023 draft. apicr.minzdrav.gov.ru returns the same files for 295_5/295_6 and 169_4/169_5.
- **Sources still unreachable (already recorded in the search log).** No reachable copy found:
  - **IHS Real-World Evidence guideline 2025 (PMID 40095946).** Tried the University of Copenhagen repository PDF (Cloudflare challenge, HTTP 403, also via WebFetch), the Leiden handle (connection reset), recercat (403), the Pavia IRIS record (metadata only) and SAGE (403). Europe PMC lists it as not open access.
  - **IHS paediatric 2023 update (PMID 37226450).** Tried SAGE (403), the sage.cnpereading.com mirror (HTML only) and DuEPublico (proof-of-work challenge).
  - **AWMF 030-057 and NHG-Standaard Hoofdpijn.** Still behind Anubis challenges (HTTP 200 challenge page; HTTP 401).
- **OUT-023 Rationale, "national guidelines recommend switching after repeated failure of the same triptan".** BASH is quoted, and SIGN 155 (p. 7, not quoted) says "it is worth sequencing through different triptans to find the most effective one". The plural paraphrase is fair.
- **S-017.** The section-5 row lists the 2.2.1 page as well, but all three quotes are from the 2.1.3 page. The extra page is part of the cited guideline and misleads no one.
- **S-045 PGIC.** The running text above the box carries "(NE-IV; GR-GECSEN)", while the quoted box item carries no tag, as the document says. Mentioning it would not change OUT-026 (SHOULD).

## Remarks
None.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
