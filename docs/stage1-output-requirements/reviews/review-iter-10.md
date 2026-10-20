# Review — iteration 10
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v09
Date: 2026-10-20

## Summary
I downloaded all 46 sources again with curl into a new scratch folder, without reusing earlier agents' files. That includes S-026 (2020), the S-045 and S-046 landing pages, the three BASH pages and PubMed abstracts through E-utilities. I extracted every quoted string from v09 by script and matched it against the downloaded text (NFKC-, dash-, apostrophe- and whitespace-insensitive, with "[...]" segments checked in order). That covers 217 distinct quoted strings in section 3: evidence quotes, list items, caveat quotes and grade labels. All 217 are verbatim at their URLs. I also checked the headings and labels quoted inside locations, and the 27 strings quoted in section 5.

The two v09 figure quotes I checked on the embedded images at full resolution:
- S-024 Figure 3, row Rd5, rated "Fort";
- S-025 Figure 1, row RT25, rated "Fort".

Both are exact, and so are the figure headings and the ratings stated in the S-024 and S-025 entries: Rd1–Rd10 are all "Fort"; RT15–RT32 are "Fort" and RT33–RT34 "Modéré". Pages, translations, the "[...]" in RT25, the new OUT-033 caveat, the English-abstract claim (PMID 34340812) and the totals (10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT; 46 source rows, 45 cited) are all correct. I found no scope violation.

There is one remark (R10-01), on items changed in v09. The S-024 and S-025 entries and OUT-033 say that the SFEMC articles name no grading system and do not define "Fort". That is true of the French summary articles. However, the English parallel publications of the same guideline, which the S-024 and S-025 entries cite, define the SFEMC 2021 grading system: levels of evidence High/Moderate/Low and strength grades Strong/Moderate/Weak/Not recommended. Their full texts can be read on the IHS website. The iteration-09 fixer could not reach them (ScienceDirect 403). PROCESS.md section 3 requires a guideline's grading system to be named. The strength of OUT-033 (SHOULD) is not affected.

## Verification coverage

Counts are distinct quoted strings per source in section 3: evidence quotes, list items, caveat quotes and grade labels. Section-5 strings are counted in brackets.
- "ws" means the string matched only when whitespace or line-break hyphens were ignored.
- "Manual" means I confirmed the string on the page, in the `-layout` text or on the figure image, because the text layer is interrupted or absent.

Totals for section 3: 197 exact, 7 ws, 13 manual. Headings, figure titles and grade labels quoted inside locations: 85 distinct strings. All occur in their sources, with three exceptions, none of them a defect: the 2 S-033 table titles are faithful English renderings of the Russian titles; the S-037 heading is printed in capitals; and the OUT-020 criterion names are example labels, not quotations.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 15 | 15 (PDF page = printed page; "Definitions of terms" pp. 209–210; 8.2 note 2 p. 122) | 0 | — |
| S-002 | 17 (incl. 3 list items) | 17 (1 ws; PDF page + 1025) | 0 | — |
| S-003 | 2 | 2 (PDF page + 814) | 0 | — |
| S-004 | 7 | 7 (JATS sections 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5) | 0 | — (Europe PMC fullTextXML of PMC6501455) |
| S-005 | 7 | 7 (1 manual: line-break hyphen in "meta-analyses"; PDF page + 802) | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 (accepted manuscript pp. 20, 21, 25) | 0 | — |
| S-008 | 8 | 8 | 0 | — |
| S-009 | 3 | 3 (p. 22, p. 33) | 0 | — |
| S-010 | 4 | 4 (1 manual: "patient-" at a line break). The abstract quotes are also in the efetch abstract. | 0 | PubMed web page not used; E-utilities efetch used |
| S-011 | 3 | 3 | 0 | — (Europe PMC fullTextXML) |
| S-012 | 8 (incl. 3 list items) | 8 | 0 | — (Europe PMC fullTextXML) |
| S-013 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-014 | 12 | 12 (full JATS section paths checked) | 0 | — (Europe PMC fullTextXML) |
| S-015 | 13 (incl. 2 list items) | 13 ("Last updated: 03 June 2025") | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6; "Revised May 2026") | 0 | — |
| S-017 | 3 [+4] | 3 [+4]. The footer "BASH Guideline V2.0 2026" and dateModified 2026-09-14 are on both section pages; the TOC page shows "V1.0 2019". | 0 | — |
| S-018 | 8 | 8 (1 manual: "Level C" interrupts 15B; levels in the layout text) | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 (printed p. 4 = PDF p. 7) | 0 | — |
| S-021 | 3 | 3 | 0 | — |
| S-022 | 6 | 6 (manual, with line numbers stripped). Lines 383–384, 393–394, 421–425, 427–429 and 464–465, and pp. 11–13, confirmed. | 0 | — |
| S-023 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-024 | 10 [+4] | 10 [+4]. 2 manual: Rd5 and its "Fort", on the 2006 × 1337 px Figure 3 image. Title row, column "FORCE DE LA RECOMMANDATION" and Rd1–Rd10 "Fort" confirmed. PDF page + 394. | 0 | — |
| S-025 | 3 [+7] | 3 [+7]. Manual: RT25 (first sentence; "l’observance" has a typographic apostrophe), "FORCE", the heading "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE," and the RT15–RT34 ratings, on the 1864 × 2452 px Figure 1 image. Tableaux I/II columns confirmed on pp. 415–417. | 0 | — |
| S-026 | 0 (not cited) | — | — | — (downloaded; superseded entry) |
| S-027 | 6 [+1] | 6 [+1] (publication date 04-12-2023 still shown) | 0 | — |
| S-028 | 1 [+1] | 1 [+1] (11-01-2018) | 0 | — |
| S-029 | 2 [+1] | 2 [+1] (04-12-2023) | 0 | — |
| S-030 | 4 | 4 | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (6 ws; 1 manual: the side tab interrupts CQ II-2-14 on PDF p. 207 = printed p. 191, grade A confirmed) | 0 | — |
| S-032 | 3 [+3] | 3 [+3] (2 of the section-5 strings are the document's translations) | 0 | — |
| S-033 | 6 (incl. 1 grade label) | 6. Title page "Год утверждения: 2024" and developers confirmed. | 0 | — |
| S-034 | 4 (incl. 1 grade label) | 4. Title page (image) rendered: "Год утверждения 2024", developers as cited. | 0 | — |
| S-035 | 3 | 3 | 0 | — |
| S-036 | 2 [+1] | 2 [+1] | 0 | — |
| S-037 | 1 | 1 (heading printed "PRINCIPLES OF PROPHYLAXIS") | 0 | — (Europe PMC fullTextXML) |
| S-038 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | — (Europe PMC fullTextXML) |
| S-042 | 2 | 2 | 0 | — (Europe PMC fullTextXML) |
| S-043 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-044 | 1 | 1 | 0 | Abstract via E-utilities efetch |
| S-045 | 4 [+2] | 4 [+2] (PDF pp. 113 and 395; landing-page date string present) | 0 | — |
| S-046 | 3 [+3] | 3 [+3] (printed p. 5 = PDF p. 8, margin lines as stated; landing page "Draft", docket FDA-2022-D-1729) | 0 | — |
| **Total** | **217 [+27]** | **217 [+27]** | **0** | — |

Bibliographic metadata was checked against PubMed esummary for all 37 PMIDs in the document, and against Crossref for the S-024, S-025, S-036, S-041, S-043 and S-018 DOIs. Authors, titles, journals, volumes, pages, DOIs and PMCIDs are correct.

### Checked and not raised
- **Newer editions, none found that change a requirement:**
  - PubMed 2025–2026 IHS/ICHD titles: only ICHD-4 committee commentary and work-in-progress papers, position statements on other topics, and neuromodulation guidelines.
  - EHF 2025–2026: only the sex-specific consensus, already in the log.
  - Japan: no edition after 2021. China: the 2025 publication is a patient version.
  - NICE CG150: 3 June 2025. SIGN 155: May 2026. BASH: V2.0 2026.
  - NVN module dates are unchanged. FDA preventive guidance: still a draft.
- **Polish experts' consensus 2023 update** (Arch Med Sci 2024, PMC10895940). It is not in the search log. It covers drug positioning only and contains no diary or reimbursement-programme statement, so it does not supersede the S-038 passage quoted in OUT-025.
- **Italian national Delphi on women with migraine** (Healthcare 2026, PMC13361374): no diary statement.
- **AAN/AHS 2026 recommendations 8A/8B (level B) on comorbid psychiatric conditions.** They concern the choice of a combined or independent treatment, not assessment or reporting, so they do not change OUT-033.
- **Scope.** The authored phrases "proportion of days", "average peak intensity" and "median attack duration" (OUT-003, OUT-010, OUT-011) describe the unit or statistic shown, not how it is computed. Earlier iterations accepted them, and I found no new reason to object.
- **Unreachable:**
  - The AWMF S1 guideline 030-057 (2025-11): register.awmf.org still serves the Anubis anti-bot page. archive.org lists a 2026-10-10 Wayback snapshot, but web.archive.org reset the connection five times through the proxy, and WebFetch cannot fetch it.
  - The BASH 2026 advanced-preventives consensus (JNNP, PMID 42469019) is not open access in Europe PMC.
  - Korean Headache Society: a Korean-language web search again found only press reports of the 2021 guideline.

## Remarks

### R10-01 [link/citation] — target: S-024 and S-025 (section 5, "Type and grading"); OUT-033 (Evidence basis); section 6 (French row)
- **Problem.** PROCESS.md section 3 requires each clinical practice guideline's entry to name its grading system. The v09 text instead states that none exists:
  - S-024: "The article names no grading system, does not define the strength labels and gives no level of evidence for Rd1–Rd10."
  - S-025: "The article names no grading system and does not define these labels."
  - OUT-033, Evidence basis: "neither article names a grading system".

  These sentences are literally true of the French summary articles (Presse Med Form). But the guideline they summarise, the SFEMC 2021 guideline, does have a grading system. It defines "Strong" ("Fort") and the levels of evidence in the English parallel publications that the S-024 and S-025 entries themselves cite as "English version". Both full texts can be read on the IHS website. As written, a reader is told that the "Fort" on which OUT-033's SHOULD rests is an undefined label. PROCESS.md section 3 has not been met for two guideline entries. R01-03 (S-028, S-032) and R03-01 (S-036) treated the same omission as a remark.
- **Evidence.** All checked on 2026-10-20 by pdftotext and the `-layout` text.
  - **English Part 1** (= English version of S-024): Demarquay G, et al. Rev Neurol 2021;177(7):725–733, doi 10.1016/j.neurol.2021.07.001. URL: https://ihs-headache.org/wp-content/uploads/2022/12/French-guidelines-migraine-in-adults-Part-1-diagnosis-English.pdf (HTTP 200, application/pdf, 9 pages; PDF title matches PMID 34340812; listed on https://ihs-headache.org/en/resources/guidelines/affiliate-society-and-other-guidelines/). Section 2.2 "Guideline development", p. 726 (PDF p. 2):
    - "We first graded the levels of evidence in three categories ‘‘High = We are confident that the true effect lies close to the estimate given by the evidence available’’, ‘‘Moderate = We are moderately confident in the effect estimate, but there is a possibility it is substantially different’’, ‘‘Low = Our confidence in the effect estimate is limited. The true effect may be substantially different’’."
    - "Secondly, we provided the strength of recommendation grades for clinical implication [13]: ‘‘Strong = Benefits clearly outweigh risks and burdens for most patients = Can apply to most patients in most circumstances’’, ‘‘Moderate = Benefits clearly outweigh risks and burdens for most patients = Can apply to most patients, but there is a chance the recommendation may change with more research’’, ‘‘Weak = Benefits clearly outweigh risks and burdens for most patients = Can apply to most patients, but there is a good chance the recommendation could change with more research’’ or ‘‘Not recommended’’."
    - Reference 13 is "Pringsheim T, Davenport WJ, Mackie G, Worthington I, Aubé M, Christie SN, et al. Canadian Headache Society guideline for migraine prophylaxis. Can J Neurol Sci J Can Sci Neurol 2012;39:S1–59."
    - The next sentence of the same paragraph: "A reading committee scored the proposals by attributing a score ranging from 1 to 9 (best score)."
    - Table 3 "Recommendations about the diagnosis and assessment of migraine" (p. 731, PDF p. 7) has a column "Strength of the recommendation" and rates all ten Rd1–Rd10 "Strong". This includes "Assess comorbidities, and emotional burden with the HAD scale", the English wording of Rd5. Like Figure 3 of S-024, the table gives no level of evidence for these items.
  - **English Part 2** (= English version of S-025): Ducros A, et al. Rev Neurol 2021;177(7):734–752, doi 10.1016/j.neurol.2021.07.006. URL: https://ihs-headache.org/wp-content/uploads/2022/12/French-guidelines-migraine-in-adults-Part-2-treatment-pharmacological-English.pdf (HTTP 200, 19 pages; PDF title matches PMID 34340810).
    - Section 2 "Methods", p. 735 (PDF p. 2): "Methods are described in the first part of the updated guidelines [1] (Appendix 1)."
    - Table 6 "Recommendations for pharmacological prophylaxis of migraine" (p. 743, PDF p. 10) rates Rt25 "Assess efficacy, tolerability, compliance, and burden of migraine by interview, review of the calendar, and systematic use of HIT-6 and HAD scales at each visit. …" "Strong".
  - **French articles.** I confirmed that the French summary articles contain no methods or grading text: S-024 and S-025 have no "méthod…" passage, and the only "niveau de preuve" mentions are in running text and in the Tableau I/II column headings.
- **Earlier history of this item.**
  - R09-01 (iteration 09) asked the fixer to state "no grading system is named". Fix-iter-09 did so and changed S-024, S-025 and the OUT-033 Evidence basis in v09. It recorded that the English full text could not be read: doi.org redirected to ScienceDirect, which returned HTTP 403, and Europe PMC lists both articles as not open access.
  - Review 08 had noted under "Checked and not raised" that S-024 names no grading system.
  - The new evidence is the two IHS-hosted English full texts above. This remark completes the v09 fix and does not reverse it: the "Fort" ratings, the quotes, the "no level of evidence for these items" statement and OUT-033's SHOULD all stand. OUT-033 is not frozen.
- **Required change.**
  1. **S-024, "Type and grading".** Name the grading system of the SFEMC 2021 guideline:
     - levels of evidence "High", "Moderate" and "Low";
     - strength-of-recommendation grades "Strong", "Moderate", "Weak" and "Not recommended", "for clinical implication", after the Canadian Headache Society 2012 prophylaxis guideline (the source's ref. 13);
     - proposals scored 1–9 by a reading group.

     Quote at least the strength-grade sentence above, with its location: English version, section 2.2 "Guideline development", p. 726. Give the IHS URL of the English version, where it can be read. State that the English Table 3 (p. 731) rates Rd1–Rd10 "Strong", the counterpart of "Fort" in Figure 3. Replace "The article names no grading system, does not define the strength labels" with wording that is accurate, for example: "the French article does not restate the grading system; it is defined in the English version". Keep "gives no level of evidence for Rd1–Rd10".
  2. **S-025, "Type and grading".** Make the same correction. Quote the English Part 2 sentence "Methods are described in the first part of the updated guidelines [1] (Appendix 1)." (section 2 "Methods", p. 735), with the IHS URL. Replace "names no grading system and does not define these labels" accordingly. You may add that Table 6 (p. 743) rates Rt25 "Strong".
  3. **OUT-033, Evidence basis.** Replace "neither article names a grading system" with the system named in item 1. Optionally give its definition of "Strong" ("Benefits clearly outweigh risks and burdens for most patients = Can apply to most patients in most circumstances"). Keep that no level of evidence is given for Rd5 and RT25. The strength stays SHOULD, and the existing MUST reasoning still holds: Rd5 and RT25 concern the clinician's assessment with the HAD scale, not a diary output, and they carry no level of evidence. Do not change the Statement.
  4. **Section 6, French row.** Record that the English full texts of Parts 1 and 2 were found at the IHS URLs above. Fix-iter-09 had recorded that ScienceDirect returned 403 for them.
  5. **Section 5, URL column for S-024 and S-025 (optional).** You may add the IHS URLs next to the existing SFEMC URLs, marked as the location of the grading-system text.

  No quote in section 3 and no strength changes.

## Notes on frozen items (for the human)
None.
