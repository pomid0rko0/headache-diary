# Review — iteration 07
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v06
Date: 2026-10-20

## Summary
I downloaded all 45 sources again with curl into a new scratch folder and did not reuse earlier agents' files. That includes S-026 (2020) for the superseded-entry claims and the S-045 landing page. I extracted every quoted string in sections 3 and 5 by script and matched it against the downloaded text. Matching was NFKC-, dash- and whitespace-insensitive, and quotes with "[...]" were checked segment by segment, in order. That covers 275 distinct strings: 192 distinct evidence and caveat quotes (214 occurrences), 5 list items, 4 grade labels, the source-text quotes in section 5, and the headings quoted inside locations. None is missing from its source. Where the text layer is broken I checked by hand, and the two English renderings of Russian table titles in S-033 locations are faithful.

The v06 additions are correct, as are all PDF pages, JATS section paths, NICE recommendation numbers, AAN levels, Japanese and Russian grade labels, translations, "[...]" omissions, PubMed metadata and the totals (39 requirements: 10 MUST, 23 SHOULD, 5 MAY, 1 SHOULD NOT; 45 source entries, 44 cited). For S-045 this covers:
- the citation, both ISBNs, the editors and the publisher;
- the edition and supersession sentences, the grade tables and the landing-page date;
- the three OUT-026 quotes and the OUT-014 quote, with their locations ("third item" and "last item" of the box) and the offset printed page = PDF page − 2.

I found no scope violation.

There are two remarks, both on defects present since v00:
- **R07-01.** OUT-018's evidence basis lists SIGN 155 among the graded guideline recommendations, but the quoted SIGN passage is ungraded introductory text.
- **R07-02.** The search log says no FDA guidance on preventive migraine drugs was found. FDA published a draft guidance on exactly this in June 2023, and it addresses diary-based endpoints.

## Verification coverage

Counts are distinct quoted strings per source. They include list items, grade labels, section-5 source-text quotes and headings quoted inside locations; translations are excluded. "ws" means the string matched only when whitespace or line-break hyphens were ignored. "Manual" means I confirmed the string on the page, in a layout extraction or on a render, because the text layer is interrupted. Script totals: 251 exact, 9 ws, 15 manual.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 15 | 15. "Definitions of terms" on PDF pp. 209–210; the OUT-016 caveat ("based on expert opinion rather than on formal evidence") confirmed on PDF p. 123. | 0 | — |
| S-002 | 17 (incl. 3 list items) | 17 (1 ws) | 0 | — |
| S-003 | 2 | 2 | 0 | — |
| S-004 | 3 | 3; JATS sections 1.3.2, 1.3.3 and 1.3.4.2 confirmed | 0 | — (Europe PMC fullTextXML of PMC6501455) |
| S-005 | 10 | 10 (1 manual: line-break hyphen in "meta-analyses") | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 5 | 5 | 0 | — |
| S-008 | 8 | 8 | 0 | — |
| S-009 | 3 | 3 | 0 | — |
| S-010 | 6 | 6 (1 manual: "patient-reported" split at a line break); the three abstract quotes also matched in the PubMed efetch abstract | 0 | PubMed web page not used; E-utilities efetch used |
| S-011 | 3 | 3 | 0 | — (Europe PMC fullTextXML) |
| S-012 | 6 | 6 | 0 | — (Europe PMC fullTextXML) |
| S-013 | 8 | 8 | 0 | — (Europe PMC fullTextXML) |
| S-014 | 19 | 19. The OUT-009 quote also occurs under "Headache diary and calendar to aid diagnosis and follow-up in primary care" > Introduction, as stated. | 0 | — (Europe PMC fullTextXML) |
| S-015 | 17 (incl. 2 list items) | 17 (1 manual: "do not" in the S-015 type line occurs as "Do not"); "Last updated: 03 June 2025" | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6). Section 4.1 is ungraded; see R07-01. | 0 | — |
| S-017 | 8 | 8 (1 manual: "BASH Guideline V1.0 2019" confirmed on https://bash.org.uk/0-0-table-of-contents/). Footer "BASH Guideline V2.0 2026" and dateModified 2026-09-14 on both section pages. | 0 | — |
| S-018 | 9 | 9 (1 manual: "Level C" interrupts 15B); levels 12A, 14A, 14D, 14E and 15A–15D confirmed in the layout text | 0 | — |
| S-019 | 3 | 3 | 0 | — |
| S-020 | 2 | 2 | 0 | — |
| S-021 | 5 | 5 | 0 | — |
| S-022 | 6 | 6 (all manual, with line numbers stripped by script); lines 383–384, 393–394, 421–425, 427–429 and 464–465 and pp. 11–13 confirmed | 0 | — |
| S-023 | 6 | 6 | 0 | — (Europe PMC fullTextXML) |
| S-024 | 10 | 10 (PDF page + 394 = printed page) | 0 | — |
| S-025 | 3 | 3 | 0 | — |
| S-026 | 0 (not cited) | The two former v05 strings are on PDF pp. 306 and 127 of the 2020 PDF and absent from the 2026 PDF, as the S-026 and S-045 entries say | — | — |
| S-027 | 8 | 8 | 0 | — |
| S-028 | 4 | 4 (1 ws); publication date 11-01-2018 is still current | 0 | — |
| S-029 | 4 | 4 | 0 | — |
| S-030 | 4 | 4 | 0 | — |
| S-031 | 10 (incl. 2 grade labels) | 10 (6 ws: line breaks in Japanese sentences; 1 manual: the side tab in CQ II-2-14 on PDF p. 207 = printed p. 191) | 0 | — |
| S-032 | 7 | 7 (1 ws) | 0 | The first connection reset; the retry succeeded |
| S-033 | 8 | 6 verbatim. The 2 English table titles in locations faithfully render "Таблица 3в. Диагностические критерии хронической мигрени" and "Таблица 4а. Диагностические критерии лекарственно-индуцированной головной боли" (PDF pp. 18–19). Grade C/5 of sections 2.5 and 7.1 confirmed. | 0 | — |
| S-034 | 5 | 5 | 0 | — |
| S-035 | 6 | 6 | 0 | — |
| S-036 | 4 | 4 | 0 | — |
| S-037 | 2 | 2 (1 manual: the heading is printed "PRINCIPLES OF PROPHYLAXIS") | 0 | — (Europe PMC fullTextXML) |
| S-038 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | — (Europe PMC fullTextXML) |
| S-042 | 3 | 3 | 0 | — (Europe PMC fullTextXML) |
| S-043 | 1 | 1 | 0 | — (Europe PMC fullTextXML; abstract also via efetch) |
| S-044 | 1 | 1 | 0 | Abstract via E-utilities efetch |
| S-045 | 15 | 15. Chapter 11 / 5.4 (heading PDF p. 385) / 5.4.7.1 (heading PDF p. 394), quote on PDF p. 395 = printed p. 393. Chapter 4 section 4 (heading PDF p. 112); box on PDF p. 113 = printed p. 111, PGIC item third and MIDAS/HIT-6 item fourth (last). Imprint PDF p. 4; Introducción PDF p. 11; Revisión bibliográfica PDF p. 14; Tabla 3 PDF p. 17. Landing-page date string and dateCreated 2026-01-21 confirmed. | 0 | — |
| **Total** | **275** | **275** (251 exact, 9 ws, 15 manual) | **0** | — |

### Checked and not raised
- **S-045, the PGIC grade.** The quoted box sentence on PGIC carries no NE/GR label, as the document says. The running-text sentence above the box that describes PGIC ends with "(NE-IV; GR-GECSEN)". The document's wording ("a statement without a level of evidence or grade of recommendation") refers to the quoted sentence and is accurate. Either way the support is at most consensus, so no strength is affected.
- **OUT-021 and the SEN 2026 MIDAS/HIT-6 position.** OUT-021 includes instrument results (OUT-026) at SHOULD in the treatment-review view. The conflict is stated in OUT-026, which OUT-021 references. AAN/AHS 15D (level B) names QOL among the efficacy dimensions, and SEN 2026 itself says that the score change "puede proporcionar información adicional". The iteration-06 fixer considered this, and I see no evidence that requires a change.
- **SEN 2026 evaluation time points** (PDF p. 114). Oral preventives are evaluated at 3 months, and anti-CGRP and onabotulinumtoxinA at 6 months (NE-IV; GR-GECSEN). This is consistent with OUT-018 ("for example ... a minimum of 3 consecutive months").
- **French Headache Society position paper 2024** (Moisset et al., Rev Neurol 2024;180(10):1087–1099, PMID 39406556). It is not in the search log. Its abstract says it updates "certain elements" of the 2021 recommendations: the anti-CGRP/gepant position and topiramate. Nothing shows a change to the S-024 or S-025 passages quoted. The full text could not be read: the HAL copy (hal-04803610) is behind an anti-bot page, and ScienceDirect returns 403.
- **Newer editions, checked with no supersession found:**
  - ICHD: only ICHD-4 committee commentary exists, for example PMID 41166141 (2025) on "medication overuse". ICHD-3 remains the classification.
  - No new edition of the IHS trial guidelines (S-002 to S-007) or the IHS global practice recommendations (S-008, S-009), and no EHF update of S-011 to S-014.
  - The international Delphi on refractory migraine (Robblee et al., Cephalalgia 2025, PMID 40953156) builds on the EHF 2020 definitions and does not replace S-013.
  - NICE CG150: last updated 3 June 2025. SIGN 155: "Revised May 2026". BASH: V2.0 2026.
  - NVN modules: S-027 and S-029 dated 04-12-2023, S-028 dated 11-01-2018. The NVN MOH, TTH, triptan and timing modules (2018) contain no diary statement.
  - DHOS still lists the 2020 programme.
  - Japan 2021 and China 2022 remain the latest.
  - Russia: apicr serves byte-identical PDFs for 295_5/295_6 (= S-033) and 169_4/169_5 (= S-034).
  - Portugal: no newer SPC treatment edition (only a 2025 emergency-department consensus).
- **Other searches with no new output requirement:**
  - East-Asian expert consensus (J Headache Pain 2026, PMC13321575). It reports that Korean guidelines advise a diary "to monitor efficacy, side effects, and compliance", which OUT-018, OUT-024 and OUT-039 already cover.
  - Korea: only a press-reported cluster-headache guideline; no migraine guideline text.
  - Norway: Tidsskriftet review articles only.
  - Italy (SISC-IHS 2025): no diary-output text found.
  - German S1 030-057: no copy outside AWMF (Europe PMC search).

## Remarks

### R07-01 [unsupported/overstated] — target: OUT-018 (Evidence basis; source S-016)
- **Problem.** OUT-018's evidence basis begins "Graded guideline recommendations (NICE CG150 1.3.27–1.3.29; SIGN 155; AAN/AHS 2026 14A level B)". The only S-016 quote in OUT-018 is not a SIGN recommendation:
  - The quote is "Prophylactic treatment should be used for eight weeks at the target dose or maximum tolerated dose (for those with a titration schedule) before deciding if it is effective or not. For treatments of fixed dose (for example, oral CGRP receptor antagonist), treatment effectiveness should be assessed at 3 months." (section 4.1, p. 14).
  - The sentence is narrative text in "4.1 INTRODUCTION". It has no "R" marker, no good-practice tick and no level of evidence in the margin.
  - SIGN 155 contains no graded recommendation or good-practice point on when to assess preventive efficacy. The 8-week and 3-month statements occur only in this introductory paragraph.
  - Listing SIGN 155 among the graded recommendations therefore misstates the nature of the support. PROCESS.md section 3 requires each requirement to state whether its support is evidence-graded, consensus or expert opinion.
  - The document is also inconsistent with itself. OUT-010 cites the same section 4.1 paragraph as "national guidelines (SIGN; ...)", without a grade.
- **Evidence.** All from https://www.sign.ac.uk/media/2408/sign-155-migraine-2026-update-002.pdf, checked in the text layer and on a render of PDF p. 20.
  - Key to evidence statements and recommendations (PDF p. 2):
    - "R For ‘strong’ recommendations on interventions that ‘should’ be used, the guideline development group is confident that, for the vast majority of people, the intervention (or interventions) will do more good than harm."
    - "R For ‘conditional’ recommendations on interventions that should be ‘considered’ ..."
    - "Good-practice points: Recommended best practice based on the clinical experience of the guideline development group."
  - PDF p. 20 (printed p. 14) has the heading "4.1 INTRODUCTION". The quoted sentence is in the second paragraph of this plain prose, with no marker. The first "R" box in section 4 is under "4.2 CANDESARTAN" on the same page: "R Candesartan (16 mg daily) can be considered as a prophylactic treatment for patients with episodic or chronic migraine."
  - A search of the whole PDF text finds "eight weeks ... before deciding" and "assessed at 3 months" only in this 4.1 paragraph.
  - By contrast, OUT-016's "SIGN, recommendation R" is correct: PDF p. 37 reads "R In patients overusing acute treatment, medication overuse should be addressed."
- **Earlier history of this item.** None. The phrase "Graded guideline recommendations (NICE CG150 1.3.27–1.3.29; SIGN 155; AAN/AHS 2026 14A level B)" has been unchanged since v00 (commit 25f09e2). OUT-018 changed in v01 (R01-08 added the [S-002] 1.3.1 and [S-015] 1.3.29 quotes), but not this phrase, and no review has raised it. R04-02 corrected the same kind of mislabelling of a source's support type in OUT-027.
- **Required change.**
  - In OUT-018's Evidence basis, remove "SIGN 155" from "Graded guideline recommendations (...)". List it as ungraded national guideline text, for example: "national guideline text (SIGN 155, section 4.1 introduction; not a graded recommendation or good-practice point)".
  - No quote and no Statement text changes.
  - The strength stays MUST. It rests on NICE CG150 1.3.27–1.3.29, AAN/AHS 2026 14A (level B) and the IHS trial-methodology guideline [S-002], which meet PROCESS.md section 3.

### R07-02 [factual-error] — target: section 6, Search log, row "English — regulators"
- **Problem.** The row lists fda.gov among the sites searched and states "FDA guidance on preventive migraine drugs: none found."
  - FDA has published exactly such a guidance on fda.gov: the draft guidance for industry "Migraine: Developing Drugs for Preventive Treatment" (June 2023, Docket FDA-2022-D-1729, CDER).
  - It is the preventive counterpart of S-020, and it speaks directly to the diary-based outputs the document requires: monthly migraine days, monthly headache days including moderate/severe days, days of acute medication use, and a prospectively defined migraine day.
  - The log statement is therefore factually wrong and misreports the regulatory evidence available.
  - PROCESS.md section 4 requires the log to record what was and was not found, and section 9 counts factual errors as remarks.
- **Evidence.** All verified on 2026-10-20.
  - Landing page: https://www.fda.gov/regulatory-information/search-fda-guidance-documents/migraine-developing-drugs-preventive-treatment. It reads "Migraine: Developing Drugs for Preventive Treatment", "June 2023", "Download the Draft Guidance Document", "Docket Number: FDA-2022-D-1729" and "Issued by: ... Center for Drug Evaluation and Research".
  - PDF: https://www.fda.gov/media/168871/download (HTTP 200, application/pdf, 12 pages). The quotes below are from section III.A.5 "Efficacy Endpoints", printed p. 5 = PDF p. 8, verified by script against pdftotext output with line numbers removed:
    - lines 163–164: "In episodic migraine trials, the primary efficacy endpoint should assess the change from baseline in the number of monthly migraine days";
    - lines 164–167: "For chronic migraine trials, sponsors may use the change from baseline in the number of monthly migraine days or in the number of monthly headache days (of moderate/severe intensity and/or requiring use of an acute migraine medication) as the primary efficacy endpoint.";
    - lines 174–175 (secondary endpoint a): "Change from baseline in the number of days per month subjects use an acute/rescue medication to treat an acute migraine";
    - line 188: "A migraine (and/or headache) day should be prospectively defined based on prespecified criteria."
  - These statements agree with OUT-002, OUT-005, OUT-006, OUT-014 and OUT-018. I found nothing in the guidance that would change a Statement or a strength.
- **Earlier history of this item.** None. The "English — regulators" row has been unchanged since v00, and no earlier review or fix mentions the FDA preventive guidance.
- **Required change.** Replace "FDA guidance on preventive migraine drugs: none found." with an accurate record of the FDA draft guidance "Migraine: Developing Drugs for Preventive Treatment" (June 2023; Docket FDA-2022-D-1729; https://www.fda.gov/media/168871/download). Do one of the following:
  - (a) Record it as found but not used, because it adds no output beyond OUT-002, OUT-005, OUT-006, OUT-014 and OUT-018. This alone resolves the remark.
  - (b) Cite it as a new source (next free ID S-046; type "Regulatory guidance (draft, nonbinding)") where it supports existing requirements. In that case the section 5 entry and the change-log totals must be updated as well.

  No requirement Statement or strength needs to change.

## Notes on frozen items (for the human)
None.
