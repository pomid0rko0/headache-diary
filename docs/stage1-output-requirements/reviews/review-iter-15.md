# Review — iteration 15
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v14
Date: 2026-10-20

## Summary
I downloaded all 46 sources again with curl into a new, empty folder of my own and did not use the files that earlier agents left in the shared scratchpad. All 50 URLs (including the English SFEMC versions, the Swedish Kela page and the PubMed abstracts) returned HTTP 200; brainmed.com (S-032) and apicr.minzdrav.gov.ru (S-033, S-034) reset the connection and loaded on retry. A script extracted every quoted string in section 3 and matched it against the downloaded text (NFKC, quote marks, dashes and whitespace normalised; "[...]" segments in order), then checked each match against the stated page or JATS section. All 252 distinct source quotes are verbatim at their URLs: 241 by script and 11 by hand (S-022 margin line numbers, ICHD-3 8.2.2 note, AAN 15B, Japan CQ II-2-14, and the SFEMC Rd5 and RT25 figure rows, read on the embedded images). Translations, "[...]" omissions, grades, metadata (28 PMIDs via esummary), totals and cross-references are correct, and no authored text breaks the scope rules.

All v14 changes are correct: the R14-01 to R14-04 fixes and the 29 sweep quotes are verbatim, correctly located and support the elements they were added for; the indirect-support notes (OUT-010, OUT-024, OUT-034) and the corrected OUT-033 caveat are accurate. There is one remark. Three S-014 quote locations in OUT-026 and OUT-027, unchanged since v00, name a subsection heading that is the title of a different subsection from the one holding the quote. v14 made this visible: the new OUT-026 locations use those same headings, correctly, for the subsections "Scoring HALT" and "The HURT questionnaire" (R15-01). My searches in German, Korean, Croatian, Thai, Norwegian, Portuguese (Brazil), Italian, Chinese and Arabic, and PubMed 2023–2026, found no missing output requirement and no superseding edition.

## Verification coverage
"Script" means the string matched the downloaded text on its stated page or section. "Manual" means I confirmed it in the `-layout` text, in the whitespace-free text or on the embedded figure image. Counts are distinct quoted strings in section 3 outside location parentheses (evidence and caveat quotes, list items, grade labels). The 94 headings and labels quoted inside locations were checked separately (see below).

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 21 | 21 (1 manual: 8.2.2 note 1, `-layout` text of p. 123; v14 "Cluster remission period" p. 209 and "Headache days" p. 210 confirmed; PDF page = printed page) | 0 | — |
| S-002 | 22 | 22 (PDF page + 1025; v14: 1.3.1 comments sentence after 1.3.1.1–1.3.1.3, rec. b, 1.3.2.1.8, 1.3.2.3.1, 1.3.2.3.2, 1.3.2.6.1 all on the stated pages) | 0 | — |
| S-003 | 4 | 4 (PDF page + 814; the 1.3.1 comment paragraph before the quote begins "A migraine day or a moderate to severe headache day is defined as"; 1.3.2.5 and 1.3.2.5.2 p. 824; 1.3.1.3 p. 822) | 0 | — |
| S-004 | 9 | 9 (JATS 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5; the 1.3.3 comment sentence directly precedes "To align outcomes ...") | 0 | Europe PMC fullTextXML |
| S-005 | 7 | 7 (PDF page + 802) | 0 | — |
| S-006 | 4 | 4 (p. 10) | 0 | — |
| S-007 | 6 | 6 (accepted manuscript pp. 20, 21, 22, 25; 3.8 list B items c and d; 4.2.1 comments continue on p. 25) | 0 | — |
| S-008 | 8 | 8 (Q2 p. 9, Q4 p. 11, Q6 pp. 12–13, Q7 Optimal p. 13; the Q6 and Q7 sentences also recur in the summary table on p. 6) | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | 0 | — |
| S-010 | 4 | 4 (abstract quotes in the efetch abstract; pp. 3, 7) | 0 | E-utilities efetch for the abstract |
| S-011 | 3 | 3 | 0 | Europe PMC fullTextXML |
| S-012 | 10 | 10 (Discussion has 7 paragraphs; quotes at paragraph 2 sentence 1 and paragraph 7 sentences 1–4) | 0 | Europe PMC fullTextXML |
| S-013 | 10 | 10 (v14: "Drug failure" ¶3 s3 and ¶4 s1, "Assessment of patients" ¶3 s2, "Debilitating headache" ¶1 last sentence; Results ¶ "Refractory migraine is defined" is the third after Table 3) | 0 | Europe PMC fullTextXML |
| S-014 | 14 | 14 (v14 "Scoring HALT" paragraph after Table 18 and HURT sentence after Fig. 5 located correctly; three older locations wrong, R15-01) | 0 | Europe PMC fullTextXML; the PMC page served a reCAPTCHA page to curl |
| S-015 | 13 | 13 (1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37, 1.3.48 confirmed; "Published: 19 September 2012", "Last updated: 03 June 2025") | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6) | 0 | — |
| S-017 | 3 | 3 (section 2.1.3 B and E; footer "BASH Guideline V2.0 2026", dateModified 2026-09-14 on both pages; TOC page "V1.0 2019") | 0 | — |
| S-018 | 10 | 10 (1 manual: 15B, "Level C" interrupts it in the text layer). Levels in the `-layout` text: 12A B, 14A B, 14C B, 14D B, 14E B, 14F B, 15A B, 15B C, 15C A, 15D B | 0 | — |
| S-019 | 2 | 2 (p. 3) | 0 | — |
| S-020 | 5 | 5 (III.B.5, printed pp. 4–5 = PDF pp. 7–8; the two v14 list items belong to the list introduced by the quoted sentence; the omitted text is the definition of relapse) | 0 | — |
| S-021 | 4 | 4 (pp. 5, 6, 11; heading printed "MIGRAINE IN CHILDREN AND ADOLESCENTS"; omitted text "(i.e. <15 versus > 15 year)") | 0 | — |
| S-022 | 6 | 6 (all manual: margin line numbers stripped from the `-layout` text; lines 383–384, 393–394, 421–425, 427–429, 464–465 and pp. 11–13 confirmed; consultation 10 Sep 2026 – 31 Jan 2027) | 0 | — |
| S-023 | 4 | 4 ("Frage 3" has two paragraphs; the quote is the final one) | 0 | Europe PMC fullTextXML |
| S-024 | 12 | 12 (1 manual: Rd5 on the 2006 × 1337 px Figure 3 image, title row, "FORCE DE LA RECOMMANDATION", Rd1–Rd10 "Fort"; v14 Introduction quote p. 396; PDF page + 394). English Part 1: section 2.2 strings p. 726, Table 3 Rd5 "Strong" | 0 | — |
| S-025 | 3 | 3 (1 manual: RT25 first sentence, heading "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE,", "FORCE", RT15–RT32 "Fort", RT33–RT34 "Modéré" on the 1864 × 2452 px image). English Part 2: methods sentence p. 735, Table 6 Rt25 "Strong", Rt33–34 "Moderate" | 0 | — |
| S-026 | 0 (not cited) | — | — | Downloaded (superseded entry) |
| S-027 | 6 | 6 (Aanbeveling, Overwegingen, Waarden en voorkeuren, Rationale van de aanbeveling; "Publicatiedatum: 04-12-2023") | 0 | — |
| S-028 | 1 | 1 (Aanbeveling; GRADE sentence under Verantwoording; 11-01-2018) | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19) | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (1 manual: CQ II-2-14 across the side tab "‑II2", PDF p. 207 = printed p. 191, grade A; CQ I-10 in the 推奨 box, grade B, PDF p. 48; printed = PDF − 16) | 0 | — |
| S-032 | 3 | 3 (3.2 "预防性治疗有效性指标"; 七、治疗 > 病人教育; GRADE text in section 5) | 0 | Connection reset once; retry succeeded |
| S-033 | 5 | 5 (pp. 18, 19, 26, 53; grade C/5; table titles 3в and 4а rendered faithfully) | 0 | Connection reset three times; fourth attempt succeeded |
| S-034 | 3 | 3 (pp. 34, 50; grade C/5) | 0 | Connection reset once; retry succeeded |
| S-035 | 3 | 3 (PDF pp. 48, 78) | 0 | — |
| S-036 | 2 | 2 (PDF p. 16) | 0 | — |
| S-037 | 1 | 1 ("PRINCIPLES OF PROPHYLAXIS > General principles") | 0 | Europe PMC fullTextXML |
| S-038 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | Europe PMC fullTextXML |
| S-042 | 2 | 2 (the OUT-011 wording "based on patient’s headache diary" is the Table 2 summary of the statements; the Results list reads "based on the patient’s") | 0 | Europe PMC fullTextXML |
| S-043 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-044 | 1 | 1 | 0 | E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113, 395; printed = PDF − 2) | 0 | — |
| S-046 | 3 | 3 (printed p. 5 = PDF p. 8, lines 163–167 and 174–175) | 0 | — |
| **Total** | **252** | **252** (241 script, 11 manual) | **0** | — |

Other checks:
- **Headings and labels in locations (94).** All match the sources, apart from: the authored labels "Fort", "Optimal" and "consider"; the figure headings, confirmed on the images; the English SFEMC strings, matched in the English Part 1; and the two English renderings of S-033 table titles, which are faithful. The S-014 headings are discussed in R15-01.
- **Section 5.** Every source string matched, including the landing pages, which I downloaded: BASH TOC "BASH Guideline V1.0 2019"; the IHS "Affiliate Society and other guidelines" page, which links both English SFEMC PDFs; the SEN page "incluido en la web de la SEN el 21 de enero de 2026"; the FDA page "Draft", "Not for implementation. Contains non-binding recommendations." and docket FDA-2022-D-1729. The English abstract of PMID 34340812 words the calendar, HIT-6, HAD and M-TOQ recommendations as "we suggest", as OUT-033 says. Authors, journals, volumes, pages, DOIs and PMCIDs of all 28 PMIDs match esummary.
- **Translations and omissions.** I read all 61 distinct original/translation pairs; all are faithful. Every "[...]" omits only recording or calculation details, age limits, other list items or a back-reference.
- **Totals and IDs.** 39 requirements (10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT) by the stated rule; no RFC 2119 term before "Strength:". 46 source rows; 45 cited (all but S-026). No duplicate ID and no dangling OUT reference. Every [S-NNN] cited in a Statement, Rationale or Evidence basis has a quote in the same requirement. history/v14.md is byte-identical to OUTPUT_REQUIREMENTS.md, and v14 changed no Statement or Rationale (only the OUT-033 caveat).
- **Scope.** I read every Statement, Rationale, Evidence basis and Caveat. None carries input, storage or derivation content. The v14 quotes carry no counting rule or recording instruction; the S-003 definition sentence, the S-001 remission duration criterion and the S-013 minimum-duration sentences were correctly left out.

Checked and not raised:
- **Indirect support (v14).** OUT-024's acute-treatment dates and duration, OUT-010's "on a stated scale" and OUT-034's completeness indicator are stated as indirectly supported. Fix 14 justified keeping the OUT-024 elements (the dates place each entry in a chronological list that S-012 and S-019 support); I have no new evidence against that. "On a stated scale" is the output's unit (PROCESS.md section 2), and the OUT-034 completeness element applies OUT-003 directly.
- **Unquoted caveat statements.** The OUT-007 caveat on [S-022], the OUT-016 caveat ("based on expert opinion") and the OUT-030 caveat ("not mandatory for clinical diagnosis") are accurate. ICHD-3 p. 123 reads "... are based on expert opinion rather than on formal evidence", A1.1 note 3 on p. 190 reads "For research purposes a prospective diary is recommended, but this is not mandatory for clinical diagnosis", and the S-022 primary endpoint is quoted in OUT-005.
- **OUT-026 paraphrase of S-014.** The Evidence basis says "the summed scores" where the source says "the individual summed scores". The meaning is the same, and the Statement's "total score" is consistent with it.
- **Completeness searches, no new output requirement:**
  - **German:** S1 guideline 030-057 (2025-11) still serves the AWMF anti-bot page; the dgbfb.de copy is a one-page press note. I did not try to get past the protection.
  - **Korean:** press reports only; the Korean Headache Society says its new guideline is in preparation.
  - **Croatian:** CGRP-mAb guideline 2024 (Acta Clin Croat, PMC11912851), not in the search log. It evaluates treatment "every three months through headache diary" and by disability scales; this is covered by OUT-018, OUT-025 and OUT-026.
  - **Thai:** gepant consensus 2025 (PMC12131429) has no diary-output statement.
  - **Norwegian:** only a 2012 Tidsskriftet article and registry studies.
  - **Brazil:** no Ministry of Health PCDT for migraine exists.
  - **Italian and Chinese:** no SISC/ANIRCEF diary text and no CSN 2023 full text found.
  - **Arabic:** no Arabic-language guideline.
  - **PubMed 2023–2026:** diary, app and outcome consensus queries returned reviews and trials only. Regional guideline queries returned items already logged or reviewed (Saudi, UAE, Hungarian, Argentine, Singapore, ACP 2025).
- **Newer editions.** The IHS paediatric update 2023 (PMID 37226450) is open access on SAGE per OpenAlex, but SAGE returned 403 to curl and WebFetch, and no repository or Europe PMC copy exists. This matches the S-005 note, and I cannot show that it changes OUT-036.

## Remarks
### R15-01 [link/citation] — target: OUT-026 and OUT-027 (locations of three [S-014] quotes)
- **Problem.** Three quotes from the S-014 aids are located in a subsection whose exact title belongs to a different subsection from the one that holds the quote. PROCESS.md section 3 requires the location in the source, and R01-02, R04-01 and R05-01 (b) treated comparable wrong locations as defects.
  - **The sections involved.** In S-014, section 3.4 "The Headache-Attributed Lost Time (HALT) Indices: measures of burden for headache management in primary care" has the subsections "Introduction" (3 paragraphs) and "The Headache-Attributed Lost Time (HALT) Indices" (which contains "Scoring HALT"). Section 3.5 "The Headache Under-Response to Treatment (HURT) questionnaire: a guide to follow-up in primary care" has the subsections "Introduction" (3 paragraphs) and "The Headache Under-Response to Treatment (HURT) questionnaire". The article's own cross-references number these subsections "3.4.2 The Headache-Attributed Lost Time (HALT) Indices" and "3.5.2 The Headache Under-Response to Treatment (HURT) questionnaire" (for example in "European principles of management ..." > "General aspects of headache management" > "Follow-up").
  - **OUT-027, two quotes.** "Assessment of a headache disorder requires more than diagnosis: ..." and "the result is expressed by a number with intuitively meaningful units (eg, days/month)." are both located `(section "The Headache-Attributed Lost Time (HALT) Indices")`. They are in 3.4 > "Introduction": paragraph 1, and paragraph 2, last sentence (after the semicolon). They are not in the subsection "The Headache-Attributed Lost Time (HALT) Indices" (3.4.2).
  - **OUT-026, one quote.** "Lifting The Burden developed the HURT questionnaire [10] as an instrument ..." is located `(section "The Headache Under-Response to Treatment (HURT) questionnaire")`. It is in 3.5 > "Introduction", paragraph 3. It is not in the subsection "The Headache Under-Response to Treatment (HURT) questionnaire" (3.5.2).
  - **Why v14 matters.** Fix 14 (R14-04) added two S-014 quotes to OUT-026 with full paths that use these same titles, correctly, for the subsections: `... > "The Headache-Attributed Lost Time (HALT) Indices" > "Scoring HALT"` and `... > "The Headache Under-Response to Treatment (HURT) questionnaire", the paragraph directly after Fig. 5`. Within OUT-026, the two HURT quotes are now located in the same subsection, although they are in different ones. OUT-035 already shows the document's form for an Introduction subsection: `(section "Headache diary and calendar to aid diagnosis and follow-up in primary care", Introduction)`.
- **Evidence.** Europe PMC fullTextXML of PMC6734476 (https://www.ebi.ac.uk/europepmc/webservices/rest/PMC6734476/fullTextXML; the PMC page https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/ served a reCAPTCHA page to curl). JATS paths of the quotes:
  - "Assessment of a headache disorder requires more than diagnosis: there needs to be some measure of impact on the patient’s life and lifestyle, both as a prelude to planning best management and to establish the baseline against which to evaluate treatment." In: Instruments and other materials ... > The Headache-Attributed Lost Time (HALT) Indices: measures of burden for headache management in primary care > Introduction, paragraph 1.
  - "The concept behind MIDAS is estimation of productive time lost through the disabling effect of headache; the result is expressed by a number with intuitively meaningful units (eg, days/month)." In: the same > Introduction, paragraph 2, last sentence.
  - "Lifting The Burden developed the HURT questionnaire [10] as an instrument that would not only assess outcome but also provide answers to these two questions, offering guidance to non-specialists on appropriate actions towards treatment optimisation." In: Instruments and other materials ... > The Headache Under-Response to Treatment (HURT) questionnaire: a guide to follow-up in primary care > Introduction, paragraph 3.
  - Cross-references in the article: "(see 3.5.2 The Headache Under-Response to Treatment (HURT) questionnaire (also, Additional file 20))" and "(see 3.4.2 The Headache-Attributed Lost Time (HALT) Indices (also, Additional file 19))".
- **Earlier history of this item.**
  - All three locations are unchanged since v00, and no earlier remark or fix addressed them. Reviews 11, 11b, 12 and 14 reported the S-014 section paths as correct in their coverage tables, without discussing these headings.
  - OUT-026 changed in v01 (R01-02), v06 (R06-01) and v14 (R14-04 and the sweep). OUT-027 changed in v04 (R04-02) and v14 (the sweep's S-024 quote). This remark changes none of those items, no quote text, no Statement and no strength, and reverses no fix.
  - OUT-026 is on the oscillation watch list (SEN 2026 conflict, SHOULD). This remark does not touch either point. No item is frozen.
- **Required change.** Change the three locations only. Quote texts, Statements and strengths stay as they are.
  - OUT-027, first [S-014] quote: `(section "The Headache-Attributed Lost Time (HALT) Indices: measures of burden for headache management in primary care", Introduction, first paragraph)`.
  - OUT-027, second [S-014] quote: `(section "The Headache-Attributed Lost Time (HALT) Indices: measures of burden for headache management in primary care", Introduction, second paragraph, last sentence)`.
  - OUT-026, [S-014] "Lifting The Burden developed ..." quote: `(section "The Headache Under-Response to Treatment (HURT) questionnaire: a guide to follow-up in primary care", Introduction, third paragraph)`.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
