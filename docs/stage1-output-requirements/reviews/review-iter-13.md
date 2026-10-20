# Review — iteration 13
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v12
Date: 2026-10-20

## Summary
I downloaded all 46 sources again with curl into a new, empty folder of my own and did not reuse files left by earlier agents. The downloads include S-026, the English SFEMC Parts 1 and 2, the IHS listing page, the NICE, BASH (3 pages), NVN, Kela (Finnish and Swedish), AIFA, SEN and FDA pages, the Europe PMC full texts and the PubMed records (E-utilities); all returned HTTP 200. A script extracted every quoted string in sections 3 and 5 and matched it against the downloaded text (NFKC-, dash-, apostrophe- and whitespace-insensitive, "[...]" segments in order). In section 3, all 227 distinct strings (250 occurrences) are verbatim: 220 matched by script and I confirmed 7 by hand. I also checked these and found them correct:
- every page, line and JATS section location, the NICE recommendation numbers, and the AAN, Japanese, Russian and SFEMC grade labels;
- every translation and every "[...]" omission;
- the metadata of all 37 PMIDs, the totals and the cross-references;
- the scope of all authored text.

The v12 changes are verbatim and correctly located. The two S-013 sentences are sentences 1 and 3 of the second "Drug failure" paragraph. The two S-007 list items are B.c and B.d under 3.8, p. 22. One defect remains: the v12 Evidence-basis sentence of OUT-024 attributes the whole "grouped by drug class" clause to the EHF 2020 consensus. That consensus concerns classes of preventives, and the clause also covers the separate list of acute treatments, which has no supporting quote (R13-01). My searches in Estonian, Persian, Hebrew, Croatian/Slovenian, Belgian, Chilean/Argentine Spanish, Malaysian, Japanese, Chinese and German sources, and PubMed for 2025–2026, found no missing output requirement and no superseding edition.

## Verification coverage
"Script" means the string matched in the downloaded text. "Manual" means I confirmed it in the `-layout` text, with pypdf, on a page render or on the embedded figure image. Counts are distinct quoted strings in section 3: quotes, list items, caveat quotes, and grade labels quoted in Evidence or Evidence-basis lines.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 20 | 20 (19 script; 1 manual: 8.2.2 note 1, whose justified line the text layer spreads out, read in the `-layout` text of p. 123). PDF page = printed page. "Cluster remission period" is also defined on p. 209, which supports OUT-031's "remission periods ... using the ICHD-3 definitions". | 0 | — |
| S-002 | 17 (incl. 3 list items) | 17 (PDF page + 1025) | 0 | — |
| S-003 | 2 | 2 (PDF page + 814) | 0 | — |
| S-004 | 7 | 7 (JATS 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5) | 0 | Europe PMC fullTextXML used, as section 5 provides |
| S-005 | 7 | 7 (1 manual: "meta-" at a line break, confirmed with pypdf on PDF p. 8; PDF page + 802) | 0 | — |
| S-006 | 4 | 4 (p. 10) | 0 | — |
| S-007 | 6 (2 new in v12) | 6. pp. 20, 21, 22 and 25 of the accepted manuscript. Section 3 is headed "3. Specific recommendations for attack treatment trials in episodic and chronic cluster headache" (p. 17). The 4.2.1 caveat sentence is on p. 25, before the 4.2.2 heading. | 0 | — |
| S-008 | 8 | 8. The Q2, Q4, Q6 and Q7 labels were checked in the two-column layout of pp. 9, 11, 12 and 13. | 0 | — |
| S-009 | 3 | 3 (Q12 p. 22; Q17 p. 33) | 0 | — |
| S-010 | 4 | 4 (1 manual: "patient-" at a line break, p. 7; abstract quotes matched in the efetch abstract) | 0 | PubMed web page not used; E-utilities efetch used |
| S-011 | 3 | 3 (Methods; Expert consensus statements, questions 3 and 4) | 0 | Europe PMC fullTextXML |
| S-012 | 8 (incl. 3 list items) | 8 | 0 | Europe PMC fullTextXML |
| S-013 | 6 (2 new in v12) | 6. Discussion > "Drug failure" has six paragraphs. The v12 quotes are whole sentences 1 and 3 of paragraph 2. The OUT-003 paragraph is the third after Table 3. | 0 | Europe PMC fullTextXML |
| S-014 | 12 | 12 (all JATS section paths as stated) | 0 | Europe PMC fullTextXML |
| S-015 | 13 (incl. 2 list items) | 13. The numbers 1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37 and 1.3.48 were mapped to the `article` elements. The page shows "Published 19 September 2012" and "Last updated 03 June 2025". | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6; "Revised May 2026") | 0 | — |
| S-017 | 3 | 3. Both section pages have the footer "BASH Guideline V2.0 2026", dateModified 2026-09-14; the TOC page shows "V1.0 2019". | 0 | — |
| S-018 | 8 | 8 (1 manual: the margin label "Level C" interrupts 15B, p. 8). Levels: 12A B, 14A B, 14D B, 14E B, 15A B, 15B C, 15C A, 15D B. "Published in Neurology® online on August 31, 2026" matches the PubMed epubdate. | 0 | — |
| S-019 | 2 | 2 (p. 3) | 0 | — |
| S-020 | 2 | 2 (printed p. 4 = PDF p. 7) | 0 | — |
| S-021 | 3 | 3 (CPMP/EWP/788/01 Rev. 1; 24 January 2007; in force 31 July 2007) | 0 | — |
| S-022 | 6 | 6 (margin lines 383–384, 393–394, 421–425, 427–429 and 464–465 and pp. 11–13 confirmed in the layout text; sections 5.2.2, 5.2.3 and 5.2.5.2; consultation 10 Sep 2026 – 31 Jan 2027) | 0 | — |
| S-023 | 4 | 4 ("Hintergrund"; "Frage 3") | 0 | Europe PMC fullTextXML |
| S-024 | 11 (incl. grade labels) | 11 (1 manual: Rd5 on the 2006 × 1337 px Figure 3 image, with the title row, "FORCE DE LA RECOMMANDATION" and Rd1–Rd10 all "Fort"). The English Part 1 strings ("Guideline development", "for clinical implication", the definition of "Strong", Table 3 Rd1–Rd10 "Strong") were matched in the IHS copy. Page offsets: PDF page + 394 (French); + 724 (English). | 0 | — |
| S-025 | 3 | 3 (1 manual: RT25 first sentence, the heading "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE," and "FORCE" on the 1864 × 2452 px Figure 1 image; RT15–RT32 "Fort", RT33–RT34 "Modéré"). English Table 6 rates Rt25 "Strong" (PDF p. 10 = p. 743). | 0 | — |
| S-026 | 0 (not cited) | — | — | Downloaded; superseded entry |
| S-027 | 6 | 6 (Publicatiedatum 04-12-2023) | 0 | — |
| S-028 | 1 | 1 (11-01-2018; "Hierbij is gebruik gemaakt van de GRADE methodiek." present) | 0 | — |
| S-029 | 2 | 2 (04-12-2023) | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19; "3. udgave") | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (1 manual: CQ II-2-14 across the side tab, read on a 150-dpi render of PDF p. 207 = printed p. 191, with grade A). CQ I-10: the quoted sentence is in the 推奨 box, grade B (PDF p. 48). Printed = PDF − 16. | 0 | — |
| S-032 | 3 | 3. Section 3.2 and 七、治疗 > 病人教育 confirmed; the "[...]" items omitted are the other criteria. Citation line "中国疼痛医学杂志 ... 2022, 28 (12), 881-898" is on the reprint page. | 0 | — |
| S-033 | 5 | 5 (pp. 18, 19, 26, 53). Grade C/5 follows the 2.5 and 7.1 recommendations. The two English table titles are faithful renderings of "Таблица 3в" and "Таблица 4а". | 0 | — |
| S-034 | 3 | 3 (pp. 34, 50; grade C/5 after 7.1). The scanned title page shows "Возрастная группа дети", "Год утверждения 2024" and the three developers. | 0 | — |
| S-035 | 3 | 3 (PDF pp. 48, 78; ISBN 978-975-590-958-5; "Ağustos - 2025", Revizyon No 01) | 0 | — |
| S-036 | 2 | 2 (PDF p. 16; DOI printed in the PDF) | 0 | — |
| S-037 | 1 | 1 (heading printed "PRINCIPLES OF PROPHYLAXIS") | 0 | Europe PMC fullTextXML |
| S-038 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 ("G.U. 93 del 22/04/2025") | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | Europe PMC fullTextXML |
| S-042 | 2 | 2 (Results, Question 6) | 0 | Europe PMC fullTextXML |
| S-043 | 1 | 1 (Abstract > Background) | 0 | Europe PMC fullTextXML and efetch |
| S-044 | 1 | 1 | 0 | Abstract via E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113, 395; printed = PDF − 2) | 0 | — |
| S-046 | 3 | 3 (printed p. 5 = PDF p. 8; margin lines 163–167 and 174–175; item a is under "Sponsors should assess the following secondary efficacy endpoints") | 0 | — |
| **Total** | **227** | **227** (220 script, 7 manual) | **0** | — |

Other checks:
- **Section 5.** All quoted source strings are on their stated pages, including:
  - the S-024 and S-025 English grading, methods and table strings;
  - the S-045 edition, methodology and grade-D strings (PDF pp. 11, 14 and 17) and both ISBNs;
  - the S-036 introduction sentence (PDF p. 7);
  - the S-032 GRADE sentences;
  - the S-046 "Draft" strings and docket FDA-2022-D-1729.

  "FORCE DE LA RECOMMANDATION" and "FORCE" are figure text and were confirmed on the images. NICE prints "Do not" with a capital. The remaining unmatched strings are the document's own translations, which are faithful.
- **Headings and labels.** 125 headings and labels are quoted inside locations or authored text. The unmatched ones are:
  - authored labels in Statements (e.g. "NICE CG150 rec. 1.3.28");
  - English renderings of the S-033 table titles;
  - figure headings, confirmed on the images;
  - "Principles of prophylaxis", which is printed in capitals;
  - three English Part 1 strings in the OUT-033 Evidence basis, which my script attributed to S-025 but which are in S-024en, where I matched them.
- **Translations.** I read all 66 translation occurrences against their originals. All are faithful.
- **Omissions.** All 13 quotes with "[...]" omit only recording or calculation details, cross-references or other list items. No omission changes the meaning.
- **Totals and IDs.** 39 requirements (10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT) by the stated rule, with no RFC 2119 term before "Strength:". 46 source rows; 45 cited (all but S-026). No duplicate ID; every OUT and S reference resolves. history/v12.md is identical to OUTPUT_REQUIREMENTS.md.
- **Scope.** I read every Statement, Rationale, Caveat and Evidence-basis line. None contains input, storage or derivation content; the unit and statistic examples were accepted in earlier iterations. The v12 quotes contain no numeric criteria.

Checked and not raised:
- **Estonian national guideline.** "Migreeni esmane diagnostika ja farmakoteraapia täiskasvanutel. Ravijuhend. RJ-G/61.1-2022" (Eesti Haigekassa) is not in the search log.
  - The professional version is not on ravijuhend.ee: I fetched every guideline id from 1 to 480.
  - Its patient version, PJ-G/62.1-2022 (published 19.10.2022), is at https://ravijuhend.ee/patsiendivarav/juhendid/238/migreeni-diagnoosimine-ja-ravi. It says "Migreeniravi tõhususe jälgimiseks pea peavalupäevikut." ("To monitor the effectiveness of migraine treatment, keep a headache diary."). Its other diary sentences are recording instructions.
  - It adds no output beyond OUT-014, OUT-018, OUT-023 and OUT-034. The author may log it, but it changes no requirement.
- **Persian.** An Iranian adult headache guideline ("راهنمای بالینی تشخیص و مدیریت سردرد در بالغین", hosted at hlt.bums.ac.ir) could not be read. curl got a connection reset over HTTPS and HTTP 503 over HTTP, and WebFetch got HTTP 503. Nothing suggests it holds output guidance absent from the international sources, so I do not raise a language gap.
- **Other searches with no guideline text found:** Hebrew (Israel), Croatian and Slovenian, Belgian, Chilean and Argentine Spanish, Malaysian.
- **Newer editions.** No Japanese edition after 2021 was found. The CSN 2023 Chinese guideline has a different issuer and is already logged as inaccessible. PubMed for 2025–2026 (IHS, EHF and ICHD titles) shows no edition superseding S-001 to S-014. NICE (3 June 2025), SIGN (May 2026), BASH (V2.0 2026), the FDA draft and the EMA draft are current.
- **German S1 030-057 (2025-10/11).** Both AWMF PDFs (long and patient versions) still return the anti-bot page. I did not try to get past it, and I found no other copy.
- **Wearing-off at the end of the dosing interval.** Only S-023 mentions it, as a criterion for discontinuation trials, and no graded or consensus recommendation on an output was found. This is unchanged from review 04.

## Remarks
### R13-01 [unsupported/overstated] — target: OUT-024 (Statement clause "grouped by drug class" as applied to the separate list of acute treatments; Evidence basis sentence added in v12; Evidence)
- **Problem.** The Statement reads: "The diary output SHOULD provide a chronological list of preventive (and, separately, acute) treatments with start and stop dates, ..., and the reason for stopping, grouped by drug class." The grouping therefore applies to the acute list as well.
  - **What v12 changed.** v12 (R12-01) added the only quoted support for the grouping: two S-013 sentences on failed classes of medications in resistant and refractory migraine. It also added this Evidence-basis sentence: "The grouping by drug class rests on the EHF consensus (2020), which names the number of failed classes of medications as one of the main criteria for resistant and refractory migraine; ...".
  - **Why S-013 does not cover acute treatments.** Its classes are classes of preventive drugs. The sentence between the two quoted ones says so: "The specific classes were picked because they have shown clinical efficacy in randomized-controlled trials and are supported by evidence-based guidelines for migraine prevention [13, 22, 25, 26]." (Discussion, "Drug failure", second paragraph, second sentence; verified in the Europe PMC fullTextXML of PMC7296705).
  - **Result.** For acute treatments, the unqualified Evidence-basis sentence is inaccurate. No quote in OUT-024 supports grouping acute treatments by class. The Rationale mentions only preventives.
  - **Precedent.** PROCESS.md section 3 requires a supporting quote for each element. R12-01, R12-02 and R11b-01 treated unquoted Statement elements as remarks.
- **Evidence.** Support exists in S-012 (EHF 2022 consensus on effective acute treatment and triptan failure), which the document already cites in OUT-012 and OUT-023. Each quote below was verified verbatim in the Europe PMC fullTextXML of PMC9555163 (https://pmc.ncbi.nlm.nih.gov/articles/PMC9555163/):
  - Discussion, paragraph beginning "The present Consensus not only provided a definition referring to response to each single drug", fourth sentence: "In individuals who are resistant to triptans, the drugs could still be used after optimization, while in those who are refractory the drugs should be abandoned in favor of other classes."
  - Discussion, paragraph beginning "The initial intention of the Panel", first sentence: "The initial intention of the Panel was to focus on response, resistance, and refractoriness to triptans; however, when considering each single drug, the same barriers to effective care are present for any drug class."
  - Discussion, same paragraph as the first quote, second sentence, which gives the nature of the support: "The cutoffs for resistance and refractoriness were arbitrary and mostly based on the Panel members’ clinical experience."
  - Do not quote the triptan-resistant and triptan-refractory definitions under Results > "Definition of triptan failure". They contain numeric criteria, which PROCESS.md section 2 excludes.
- **Earlier history of this item.**
  - OUT-024 was byte-identical from v00 to v11. It changed only in v12, through R12-01 (fix-iter-12, option a): two S-013 quotes and the Evidence-basis sentence above.
  - Review 12 raised the grouping element as a whole. Neither the review nor the fix considered that it also covers the acute list.
  - This remark does not reverse R12-01. The S-013 quotes and the grouping of preventive treatments stay. It narrows the v12 sentence to what S-013 supports and asks for support for, or removal of, the acute half of the clause.
  - OUT-024 is not frozen and is not on the oscillation watch list.
- **Required change.** Choose one:
  - **(a) Keep the grouping for acute treatments.**
    - Add the first S-012 quote above to OUT-024's Evidence, with its location (Discussion, paragraph beginning "The present Consensus not only provided a definition referring to response to each single drug", fourth sentence). The second quote may also be added.
    - In the Evidence basis, add EHF 2022 to the consensus sources, for example "consensus (EHF 2020; EHF 2022)".
    - Rewrite the v12 sentence so it covers each list separately. The grouping of preventive treatments by drug class rests on the EHF consensus (2020), as now stated. The grouping of acute treatments rests on the EHF consensus (2022) [S-012], which judges triptan resistance and refractoriness across the class and states that its cutoffs are "arbitrary and mostly based on the Panel members’ clinical experience".
    - The Rationale may gain a matching clause.
    - The strength stays SHOULD.
  - **(b) Restrict the grouping to preventive treatments.**
    - Rephrase the Statement so that only the preventive list is "grouped by drug class".
    - Begin the Evidence-basis sentence "The grouping of preventive treatments by drug class rests on ...".
    - The strength stays SHOULD.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
