# Review — iteration 08
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v07
Date: 2026-10-20

## Summary
I downloaded all 46 sources again with curl into a new scratch folder and did not reuse earlier agents' files. That includes S-026 (2020) and the S-045 and S-046 landing pages. Russian PDFs and S-032 needed retries after connection resets. I matched every quoted string in section 3 by script (NFKC-, dash- and whitespace-insensitive, with "[...]" segments checked in order): 204 distinct strings in 226 occurrences, including list items, caveat quotes and grade labels. I also matched the 14 source-text strings quoted in section 5. All 218 are verbatim at their URLs.

I also found these correct, among others:
- the PDF page offsets, JATS section paths, NICE recommendation numbers and AAN levels;
- the Japanese and Russian grade labels, translations and "[...]" omissions;
- PubMed metadata for all 27 PMIDs, and the totals (39 requirements: 10 MUST, 23 SHOULD, 5 MAY, 1 SHOULD NOT; 46 source rows, 45 cited).

The v07 changes are correct:
- **R07-01:** OUT-018 now labels SIGN 155 section 4.1 as ungraded text.
- **R07-02:** the three [S-046] quotes are verbatim at the stated margin lines (163–164, 164–167, 174–175) on printed p. 5 (PDF p. 8, printed page = PDF page − 3) of section III.A.5. The "[...]" in OUT-005 omits only "(see the migraine day example below)". The S-046 entry's draft status, docket number and landing-page strings are accurate, and no final version exists.

There is no scope violation in authored text. Two defects, both present since v00, remain:
- **R08-01.** OUT-023 says its outputs let the EHF definition of effective attack treatment be applied. That definition needs headache relief to mild or none, kept to 24 h, and the absence of meaningful drug-related adverse events, and OUT-023 asks for neither.
- **R08-02.** OUT-016 restricts its medication-overuse indicator to "per acute medication class". Yet it names ICHD-3 subtype 8.2.6, which by definition is overuse with no single class overused.

## Verification coverage

Counts are distinct quoted strings per source in section 3: evidence quotes, list items, caveat quotes and grade labels. Section-5 source-text strings are listed separately below the table. "ws" means the string matched only when whitespace or line-break hyphens were ignored; I inspected each such case. "Manual" means I confirmed the string on the page or in a layout extraction because the text layer is interrupted. Totals: 178 exact, 18 ws (15 whitespace and 3 line-break hyphens), 8 manual.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 14 | 14. PDF page = journal page. "Definitions of terms" (pp. 209–210) includes "Cluster remission period"; the 8.2 notes are on p. 122. | 0 | — |
| S-002 | 17 (incl. 3 list items) | 17 (1 ws). PDF page + 1025 = journal page. | 0 | — |
| S-003 | 2 | 2. PDF page + 814. | 0 | — |
| S-004 | 3 | 3 (1 ws). Sections 1.3.2, 1.3.3 and 1.3.4.2 confirmed in JATS. | 0 | — (Europe PMC fullTextXML of PMC6501455) |
| S-005 | 7 | 7 (1 ws: line-break hyphen). PDF page + 802. | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 (accepted-manuscript pp. 20, 21 and 25) | 0 | — |
| S-008 | 8 | 8. Q2, Q4 > Evidence, Q6 > Background/Evidence, Q7 and the "Optimal" labels confirmed. | 0 | — |
| S-009 | 3 | 3 (Q12 "Recommendations Optimal", p. 22) | 0 | — |
| S-010 | 4 | 4 (2 ws: line-break hyphens). Abstract quotes also in the PubMed efetch abstract. | 0 | PubMed web page not used; E-utilities efetch used |
| S-011 | 3 | 3 (Methods; Expert consensus statements, questions 3 and 4) | 0 | — (Europe PMC fullTextXML) |
| S-012 | 4 | 4 (1 ws) | 0 | — (Europe PMC fullTextXML) |
| S-013 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-014 | 12 | 12 (5 ws: spacing around citations) | 0 | — (Europe PMC fullTextXML) |
| S-015 | 13 (incl. 2 list items) | 13. Recommendations 1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37 and 1.3.48 confirmed. Published 19 September 2012, last updated 3 June 2025. | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6). "Revised May 2026". The "R" marker on the OUT-016 quote (PDF pp. 12 and 37) confirmed. Section 4.1 is unmarked prose, as the v07 OUT-018 wording states. | 0 | — |
| S-017 | 3 | 3. Footer "BASH Guideline V2.0 2026" and dateModified 2026-09-14 on both section pages; the TOC page shows "V1.0 2019". | 0 | — |
| S-018 | 8 | 8 (1 manual: "Level C" interrupts 15B). Levels of 12A, 14A, 14D, 14E and 15A–15D confirmed in the layout text. | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 (section III.B.5, printed p. 4 = PDF p. 7) | 0 | — |
| S-021 | 3 | 3 (24 January 2007; in effect 31 July 2007) | 0 | — |
| S-022 | 6 | 6 (all manual, with line numbers stripped). Lines 383–384, 393–394, 421–425, 427–429 and 464–465; sections 5.2.2, 5.2.3 and 5.2.5.2; pp. 11–13. | 0 | — |
| S-023 | 4 | 4 (1 ws) | 0 | — (Europe PMC fullTextXML) |
| S-024 | 6 | 6 (PDF page + 394) | 0 | — |
| S-025 | 1 | 1 (PDF p. 2 = p. 413) | 0 | — |
| S-026 | 0 (not cited) | — | — | — (downloaded; superseded entry) |
| S-027 | 6 | 6 | 0 | — |
| S-028 | 1 | 1 | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (6 ws; 1 manual: the side tab in CQ II-2-14, PDF p. 207 = printed p. 191). Printed page = PDF page − 16 for all quotes. | 0 | — |
| S-032 | 3 | 3 | 0 | First connection reset; retry succeeded |
| S-033 | 6 (incl. 1 grade label) | 6; grade C/5 of sections 2.5 and 7.1 confirmed | 0 | Two resets; third attempt succeeded |
| S-034 | 4 (incl. 1 grade label) | 4 | 0 | Succeeded on retry |
| S-035 | 3 | 3 | 0 | — |
| S-036 | 2 | 2 | 0 | — |
| S-037 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-038 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-039 | 2 | 2; page title "3007 Atogepantti, … ja rimegepantti (migreenin estohoito)" | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | — (Europe PMC fullTextXML) |
| S-042 | 2 | 2 | 0 | — (Europe PMC fullTextXML) |
| S-043 | 1 | 1 (elocation-id 135) | 0 | — (Europe PMC fullTextXML) |
| S-044 | 1 | 1 | 0 | Abstract via E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113 and 395; the box has four items, PGIC third and MIDAS/HIT-6 last) | 0 | — |
| S-046 | 3 | 3 (margin lines and printed p. 5 as stated) | 0 | — |
| **Total** | **204** | **204** (178 exact, 18 ws, 8 manual) | **0** | — |

Section-5 source-text strings, all verified (14):
- S-017: the 3 footer and TOC strings;
- S-028: the GRADE sentence;
- S-032: the 2 GRADE quotes;
- S-036: the DGS sentence;
- S-045: 3 strings plus the landing-page date string;
- S-046: "Contains Nonbinding Recommendations" and "Draft — Not for Implementation" on the guidance pages, plus the landing-page "Not for implementation. Contains non-binding recommendations." (docket FDA-2022-D-1729, content current as of 06/01/2023).

### Checked and not raised
- **OUT-034, Japan CQ I-10 cited as a strong recommendation while the quoted sentence is from the Background.** The graded recommendation text of CQ I-10 (PDF p. 48, "強い推奨/エビデンスの確実性 B") itself says the diary is useful for patient–physician communication ("患者‑医師間コミュニケーションの向上をはかる意味でも有用であり"). The graded claim is therefore substantively supported, unlike the SIGN case in R07-01.
- **S-024 grading system.** The Presse Med Form article is a French summary ("L'essentiel des recommandations"). It names no grading system, so there is nothing to require.
- **Search log, India row.** The query as written returns no Indian headache guideline in PubMed (12 hits, none relevant), so the row is accurate. An older English guideline exists (Ravishankar et al., Ann Indian Acad Neurol 2011, PMC3152170), but this is not a language gap.
- **New 2026 sources not in the search log.** Two Brazilian position statements (anti-CGRP mAbs, Cureus 2026, PMC13552630; MOH, Front Pain Res 2026, PMC12886480) contain no diary-output statement beyond survey answers.
- **Searches with no new output requirement:**
  - Korean: the KHS guideline revision is still only in press reports.
  - Finnish: there is still no Käypä hoito migraine guideline.
  - Japanese: no edition after 2021.
  - Chinese: no CMA 2023–2025 text.
  - Latin-American Spanish: the Colombian 2014 consensus and the Ibero-American consensus were already assessed in review 05.
- **Newer editions, none found:**
  - FDA acute guidance: content current as of 08/24/2018.
  - EMA: Rev. 1 is the current effective version, and the Rev. 2 consultation is open.
  - NICE CG150: 3 June 2025. SIGN 155: May 2026. BASH: V2.0 2026.
  - AAN/AHS 2026: Neurology PMID 42673560, with a parallel publication in Headache, PMID 42673606.
  - The IHS guidelines page lists no new trial-guideline edition and no PDF of the 2023 paediatric update.
  - PubMed 2025–2026 EHF/IHS scan: nothing superseding.
- **Unreachable:**
  - register.awmf.org 030-057: Anubis anti-bot page again.
  - IHS paediatric update 2023 (PMID 37226450): Unpaywall reports it closed.

## Remarks

### R08-01 [missing-requirement] — target: OUT-023 (Statement, Rationale, Evidence)
- **Problem.** OUT-023 says its per-drug outputs exist "so that the EHF definitions of effective attack treatment and triptan response [S-012] can be applied". The outputs it lists are:
  - pain freedom at 2 hours;
  - absence of the most bothersome symptom at 2 hours;
  - sustained pain freedom to 24 hours;
  - use of rescue or repeat medication;
  - relapse;
  - consistency across attacks;
  - timing of intake.

  The EHF definition, however, judges an attack effectively treated on a well-being status, reached within 2 h and kept for 24 h, that requires all of:
  - (A) improvement of headache from moderate/severe to mild or absent, which is headache relief and not pain freedom;
  - (B) absent or minimal non-pain symptoms;
  - (C) no meaningful drug-related adverse events.

  (B) is covered through OUT-012 and the most-bothersome-symptom element. (A) and (C) are not output anywhere for treated attacks. An attack that falls from severe to mild within 2 h and stays mild, without adverse events, is effectively treated under EHF, but in the specified output it appears only as "not pain-free". The EHF triptan-responder definition ("effective attack treatment in at least 3 out of 4 consecutive attacks") therefore cannot be applied, contrary to the Statement's stated purpose. Triptan failure is what the EHF definition is used to establish (S-012 title and Discussion).
- **Evidence.** All verified verbatim.
  - [S-012] https://pmc.ncbi.nlm.nih.gov/articles/PMC9555163/, checked in the Europe PMC fullTextXML. Section path Results > Consensus > "Definition of effective treatment of a migraine attack":
    - "Reaching, within 2 h from intake of the drug, and maintaining, for at least 24 h a well-being status as defined by all the following:"
    - followed by the list items "Improvement of headache from severe or moderate to mild or absent;", "Absent or minimal disturbances due to migraine-related non-pain symptoms;" and "No meaningful drug-related adverse events."
  - [S-012] Results > Consensus > "Definition of triptan-responder": "A given triptan leads to effective attack treatment in at least 3 out of 4 consecutive attacks."
  - [S-004] https://pmc.ncbi.nlm.nih.gov/articles/PMC6501455/, checked in the Europe PMC fullTextXML. Section 1.3.4.5 "Headache relief", recommendation 1.3.4.5.1: "Headache relief (45), defined as the decrease in headache pain from moderate or severe at baseline to mild or none at 2 hours after treatment and before taking any rescue medication (refer to Section 1.2.11), should be used as a secondary efficacy measure."
  - [S-004] same section, comments: "Since headache relief is associated with relief of disability, it can be used in clinical trials as a proxy for pain improvement and restoration of function."
  - Conflicting definitions already in OUT-023, which the fixer should keep visible:
    - [S-016] "Treatment response is defined as pain free at 2 hours and sustained pain free at 24 hours." (section 3.1, p. 7).
    - The S-004 1.3.4.5 comments also note that patients expect pain freedom.

    Pain freedom stays. Headache relief is added next to it, so that each named definition can be applied, as OUT-020 does for preventive responder criteria.
- **Earlier history of this item.**
  - The EHF purpose clause and the list of measures have been unchanged since v00, and no earlier review or fix raised headache relief or per-attack adverse events.
  - The OUT-023 Statement was extended in v01 (R01-09, R01-11: cluster time point, timing of intake) and in v02 (R02-01: baseline versus on-treatment view). The oscillation check after iteration 04 put OUT-023 on its watch list.
  - This remark adds elements and reverses none of those changes.
- **Required change.**
  - In the OUT-023 Statement, add to the per-drug outcomes reported across the attacks treated with each acute medication, at SHOULD:
    - (a) headache relief at 2 hours, as defined in the IHS acute trial guideline section 1.3.4.5 [S-004], and whether it was maintained to 24 hours;
    - (b) meaningful drug-related adverse events after intake (cross-reference OUT-024 for adverse effects per treatment).

    Name the standard rather than restating its criteria (PROCESS.md section 2), and describe only the output, not how it is recorded or derived.
  - Add the [S-012] definition quote (with its three list items) and the [S-004] 1.3.4.5.1 quote above to Evidence. Optionally add the triptan-responder sentence.
  - Update the Rationale: the EHF definition requires improvement to mild or absent and the absence of meaningful drug-related adverse events, and IHS uses headache relief as a secondary measure. Keep the existing pain-freedom elements and state that definitions of acute response differ (EHF versus SIGN 155 3.1 / IHS pain freedom).
  - Evidence basis: consensus (EHF 2022) and international trial-methodology guideline (IHS 2019). Strength stays SHOULD.

### R08-02 [contradiction/duplication] — target: OUT-016 (Statement)
- **Problem.** The OUT-016 Statement requires the output to "indicate, per reporting period and per acute medication class, whether acute medication use reached the levels of regular use that ICHD-3 code 8.2 and its subtypes 8.2.1–8.2.6 and 8.2.8 [S-001] describe". The statement contradicts itself and the code it cites:
  - Subtype 8.2.6 is defined by ICHD-3 as overuse in which no individual drug or drug class is overused, only their combined use.
  - An indicator given per acute medication class can therefore never show 8.2.6.
  - Implemented as written, this MUST requirement silently omits one of the subtypes it names. OUT-014 provides the total across classes, but OUT-016's indicator is not tied to it.
- **Evidence.** https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf, verified in pdftotext and layout output.
  - 8.2 Medication-overuse headache, Notes, note 2, p. 122: "Patients who use multiple drugs for acute or symptomatic treatment of headache may do so in a manner that constitutes overuse even though no individual drug or class of drug is overused; such patients should be coded 8.2.6 Medication-overuse headache attributed to multiple drug classes not individually overused."
  - 8.2.6, diagnostic criterion B, p. 124, ends "without overuse of any single drug or drug class alone".
- **Earlier history of this item.** None. The OUT-016 Statement is identical in v00–v07 (same text hash in every snapshot). Review 06 checked only that the subtype numbering "8.2.1–8.2.6 and 8.2.8" matches ICHD-3, not this granularity.
- **Required change.**
  - Make the granularity consistent with the codes named. For example: "per reporting period, per acute medication class and, for ICHD-3 subtype 8.2.6, for the combined use of acute medication classes across classes (see the total in OUT-014)".
  - Alternatively, if the author intends to exclude 8.2.6, remove it from the list of subtypes and state why.
  - Do not restate the ICHD-3 day limits. Name the code as now.
  - Strength, wording as a prompt for clinical review, and the caveats are unchanged.

## Notes on frozen items (for the human)
None.
