# Review — iteration 11
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v10
Date: 2026-10-20

## Summary
I downloaded all 46 sources again with curl into a new, empty scratch folder and did not reuse any earlier agent's files. That includes the English SFEMC Parts 1 and 2 from the IHS website, the IHS "Affiliate Society and other guidelines" page, the BASH, NICE, NVN, Kela, AIFA, SEN and FDA landing pages, Europe PMC full texts and PubMed records through E-utilities. A script matched every quoted string in section 3 against the downloaded text: 218 distinct strings, 241 occurrences. Matching was NFKC-, dash-, apostrophe- and whitespace-insensitive, and "[...]" segments were checked in order. 214 strings matched by script. I confirmed the other 4 by hand: two on figure images and two where layout elements interrupt the text layer.

I also checked these by script, on page renders or on the figure images:
- 71 headings and labels quoted inside locations;
- 72 quoted strings in section 5;
- the PDF page of every page-located quote against the stated page offsets;
- the JATS section path of every Europe PMC quote;
- NICE recommendation numbers;
- Japanese and Russian grade labels;
- PubMed and Crossref metadata.

All v10 changes are accurate: the S-024 and S-025 entries, the OUT-033 Evidence basis and the French search-log row. The section 2.2 grading passage of English Part 1 is verbatim on p. 726 (PDF p. 2), and its reference 13 is Pringsheim 2012. Table 3 (p. 731) rates Rd1–Rd10 "Strong". The Part 2 methods sentence is on p. 735, Table 6 (pp. 743–744) rates Rt15–Rt32 "Strong" and Rt33–Rt34 "Moderate", and Rt25 is "Strong". Both page offsets (+724, +733) are correct, and the English-abstract claim is correct. My searches in several languages found no missing output requirement, no superseding edition that changes a requirement and no scope violation. The totals are correct.

## Verification coverage
"ws" means the string matched only with whitespace or line breaks ignored. "Manual" means I confirmed it on the page, in the `-layout` text or on the embedded figure image. Section-5 strings are counted in brackets.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 15 | 15 (PDF page = printed page; A1.1 note 3 "not mandatory for clinical diagnosis" behind the OUT-030 caveat confirmed, p. 190) | 0 | — |
| S-002 | 17 | 17 (1 ws "moderate/ severe"; PDF page + 1025) | 0 | — |
| S-003 | 2 | 2 (PDF page + 814) | 0 | — |
| S-004 | 7 | 7 (4 ws; JATS sections 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5) | 0 | — (Europe PMC fullTextXML) |
| S-005 | 7 | 7 (1 line-break hyphen: "meta-analyses", confirmed with pypdf; PDF page + 802) | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 (accepted manuscript "v. 3.2, April 2022"; pp. 20, 21, 25) | 0 | — |
| S-008 | 8 | 8 | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | 0 | — |
| S-010 | 4 | 4 (1 line-break hyphen: "patient-reported", confirmed with pypdf). The abstract quotes are also in the efetch abstract, and "control" tiers are present. | 0 | PubMed web page not used; E-utilities efetch used |
| S-011 | 3 | 3 | 0 | — (Europe PMC) |
| S-012 | 8 | 8 (1 ws) | 0 | — (Europe PMC) |
| S-013 | 4 | 4 | 0 | — (Europe PMC) |
| S-014 | 12 | 12 (5 ws; "charting outcomes" also occurs in the stated section) | 0 | — (Europe PMC) |
| S-015 | 13 [+4] | 13 [+4]; recommendation numbers 1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37 and 1.3.48 confirmed; "Last updated: 03 June 2025" | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6; "Revised May 2026") | 0 | — |
| S-017 | 3 [+5] | 3 [+5]. Sections B and E of 2.1.3 confirmed. The footer "BASH Guideline V2.0 2026" and dateModified 2026-09-14 are on both pages, and the TOC page shows "V1.0 2019". | 0 | — |
| S-018 | 8 | 8 (1 manual: "Level C" interrupts 15B in the text layer; levels of 12A, 14A, 14D, 14E and 15A–15D confirmed) | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 (printed p. 4 = PDF p. 7) | 0 | — |
| S-021 | 3 | 3 | 0 | — |
| S-022 | 6 | 6 (margin line numbers stripped; pp. 11–13 and lines confirmed; front page: draft, consultation 10 Sep 2026 – 31 Jan 2027) | 0 | — |
| S-023 | 4 | 4 (1 ws) | 0 | — (Europe PMC) |
| S-024 | 11 [+17] | 11 [+17]. 1 manual: Rd5, on the 2006 × 1337 px Figure 3 image (the script also matched "Fort" elsewhere in the text, so I confirmed it on the image too), with the title row, column "FORCE DE LA RECOMMANDATION" and Rd1–Rd10 all "Fort". The English Part 1 strings (section 2.2 passage, "Guideline development", "for clinical implication", the definition of "Strong", Table 3 "Strong") were matched in the IHS PDF. PDF page + 394; English PDF page + 724. | 0 | — |
| S-025 | 3 [+25] | 3 [+25]. 1 manual: RT25 first sentence, heading "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE," and "FORCE", with RT15–RT32 "Fort" and RT33–RT34 "Modéré", on the 1864 × 2452 px Figure 1 image. Also confirmed: the Tableau I/II headers (pp. 415–417), the English methods sentence (p. 735), Table 6 (pp. 743–744), and the English Table 4 evidence values "High", "Medium", "Fair" and "Unknown". | 0 | — |
| S-026 | 0 (not cited) | — | — | — (downloaded; superseded entry) |
| S-027 | 6 [+1] | 6 [+1] (Publicatiedatum 04-12-2023) | 0 | — |
| S-028 | 1 [+4] | 1 [+4] (11-01-2018; 1 string is the document's own translation) | 0 | — |
| S-029 | 2 [+1] | 2 [+1] (04-12-2023) | 0 | — |
| S-030 | 4 | 4 | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (6 ws; 1 manual: the side tab interrupts CQ II-2-14 on PDF p. 207 = printed p. 191, grade A confirmed; CQ I-10 grade B confirmed on PDF p. 48) | 0 | — |
| S-032 | 3 [+4] | 3 [+4] (1 section-5 string is the document's own translation) | 0 | First connection reset; retry succeeded |
| S-033 | 5 | 5. The grade label C/5 in the OUT-029 location and the section 7.1 grade C/5 confirmed. The 2 table titles in locations are faithful English renderings. | 0 | — |
| S-034 | 3 | 3 (the grade label C/5 in the OUT-036 location confirmed) | 0 | — |
| S-035 | 3 | 3 | 0 | — |
| S-036 | 2 [+2] | 2 [+2] (PDF p. 7 introduction sentence, reference 5 on PDF p. 80) | 0 | — |
| S-037 | 1 | 1 (heading printed "PRINCIPLES OF PROPHYLAXIS") | 0 | — (Europe PMC) |
| S-038 | 1 | 1 | 0 | — (Europe PMC) |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | — (Europe PMC) |
| S-042 | 2 | 2 | 0 | — (Europe PMC) |
| S-043 | 1 | 1 | 0 | — (Europe PMC; Crossref article number 135) |
| S-044 | 1 | 1 | 0 | Abstract via E-utilities efetch |
| S-045 | 4 [+5] | 4 [+5] (PDF pp. 11, 14, 17, 113, 395; printed page = PDF page − 2) | 0 | — |
| S-046 | 3 [+4] | 3 [+4] (printed p. 5 = PDF p. 8; landing page "Draft", docket FDA-2022-D-1729) | 0 | — |
| **Total** | **218 [+72]** | **218 [+72]** (193 exact, 19 ws, 2 line-break hyphen, 4 manual) | **0** | — |

The bracketed totals count every quoted string in section 5, including labels and the document's own translations. Examples are NICE's wording label "do not", the S-028 and S-032 translations, the IHS page title, and grade names such as "Strong" and "Moderate". The 37 PMIDs were checked against PubMed esummary. These DOIs were checked against Crossref: S-024 and S-025 (French), S-036 and S-043. Authors, titles, journals, volumes, issues, pages, DOIs and PMCIDs are correct, including the English SFEMC citations added in v10.

### Checked and not raised
- **OUT-026 and the SFEMC grades.** Rd6 (HIT-6), Rd8 (M-TOQ) and RT25 are rated "Fort"/"Strong", and OUT-026 does not cite their ratings. This is not a defect. The document treats SFEMC "Strong" as a strength without a level of evidence, so it is not an evidence-graded recommendation (OUT-033). On that logic, AAN/AHS 15B (level C) is correctly listed first, and SHOULD is unchanged. Review 09 judged this an optional addition.
- **OUT-007 and AAN/AHS 15A.** 15A ("document the frequency of migraine attacks", level B) is cited for migraine days (OUT-005), not for attack counts (OUT-007). The AAN rationale measures "days with migraine" and "migraine attack days", so 15A does not unambiguously require attack counts. SHOULD stays proportionate.
- **New or newly reachable guidance, none of which changes a requirement:**
  - **IHS evidence-based pharmacological guideline 2025** (PMID 40277319). Now readable at ricerca.univaq.it (handle 11697/264022), although the log lists it as not retrieved. It covers drug choice only, and its "persisting monthly migraine days" is an outcome of its systematic review, not a recommendation.
  - **Canadian Headache Society prevention guideline 2024** (Can J Neurol Sci, PMID 39506371, CC-BY, cambridge.org). Its diary, frequency/intensity, MIDAS/HIT-6 and acute-medication statements are expert guidance, and they support OUT-018, OUT-010, OUT-026 and OUT-014.
  - **International refractory-migraine Delphi 2025** (PMID 40953156). Builds on EHF 2020 and has no diary statement, so OUT-003 and S-013 are unaffected.
  - **Singapore consensus 2023** (PMC13405573). Recommends diaries for reviewing efficacy and side effects and for guiding withdrawal; already covered by OUT-018, OUT-022 and OUT-024.
  - **East Asia consensus 2026** (PMC13321575). Reports that the Korean guideline advises a diary for efficacy, side effects and compliance; already covered.
  - **Hungarian CGRP practical guideline 2025** (Orv Hetil, PMID 41391059, u-szeged repository). Requires a diary before therapy and an assessment at 3 and 6 months of headache days, acute medication use and quality of life; already covered by OUT-018 and OUT-021.
  - **Russian clinical recommendations on tension-type headache 2024** (ID 162_3, apicr.minzdrav.gov.ru). Listed as a gap; now retrieved. Its diary recommendation (grade C/5) and its section 7.1 ≥50% headache-day criterion at 3 months are covered by OUT-029 and OUT-018.
  - **AAN/AHS paediatric prevention guideline 2019** (PMC6746206). Readable at PMC, although the log says the full text was empty. Statement 6a (level B) recommends screening for mood and anxiety disorders, and statement 5a (level A) recommends monitoring effectiveness and adverse events. Both concern clinician actions, so they support OUT-033 and OUT-024 at SHOULD.
  - **SFEMC position paper 2024** (Rev Neurol 2024;180:1087–1099, PMID 39406556). Its abstract updates only drug positioning (CGRP agents first line; topiramate in women of childbearing age), so the S-024 and S-025 passages cited in OUT-013 and OUT-033 are unaffected. The full text was unreachable: HAL serves an Anubis page and ScienceDirect returned 403.
- **No newer editions found** of ICHD-3, the IHS trial guidelines, the EHF documents, NICE CG150 (3 June 2025), SIGN 155 (May 2026), BASH (V2.0 2026; a guidelines launch is announced for February 2027), the Japanese 2021 guideline, the NVN modules or the FDA draft.
- **Still unreachable:**
  - AWMF 030-057 (2025-11): Anubis/BotStopper, both with curl and with WebFetch; no copy on dmkg.de or dgn.org.
  - NHG-Standaard: HTTP 401.
  - IHS paediatric update 2023: SAGE 403, and no repository copy (OpenAlex).
  - Acta Med Port 2025 consensus: publisher 403, and the run.unl.pt repository reset the connection three times.
  - CSN China 2023 guideline: only a summary reprint found.
  - Korean guideline full text: press reports only.
- **Scope.** A scan of the authored (unquoted) text found no input, storage or derivation content beyond the unit and statistic examples accepted in earlier iterations.

## Remarks
None.

## Notes on frozen items (for the human)
None.
