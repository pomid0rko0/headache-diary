# Review — iteration 04
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v03
Date: 2026-10-20

## Summary
I downloaded all 44 sources again with curl into a new scratch directory and did not reuse earlier agents' files. I extracted every quoted string from v03 by script and matched it against the downloaded text. Matching was NFKC-, whitespace- and dash-insensitive, and quotes with "[...]" were checked segment by segment and in order. That gives 204 strings (195 evidence and caveat quotes including 5 list items, 4 grade labels, and 5 source-text quotes or headings in the S-028, S-032 and S-036 entries of section 5). All 204 are verbatim at their URLs: 183 matched exactly, 13 only when whitespace or line-break hyphens were ignored, and 8 by hand. I also confirmed that the 45 section headings quoted inside location parentheses exist in the sources.

I checked the following and found them correct:
- every PDF page against the page splits and every XML section path against the JATS section titles;
- every NICE recommendation number against the recommendation `article` elements, and the AAN levels on the layout text;
- every "[...]" omission against the full source sentence, and every translation;
- bibliographic metadata against PubMed esummary, Crossref and the documents' title pages.

The only v03 change, R03-01 (S-036 grading system, source sentence, reference 5 and DOI), is correct and introduced no defect. Totals (10 MUST, 23 SHOULD, 5 MAY, 1 SHOULD NOT; 44 sources) reproduce under the stated rule. I found no scope violation. Two small defects untouched since v00 remain:
- a quote location that names a table caption as a section (S-013 in OUT-003);
- one evidence-basis line that calls a consensus statement a national guideline (S-037 in OUT-027).

Checked and not raised:
- **SEN manual.** The SEN guidelines page (https://www.sen.es/profesionales/guias-y-protocolos) still links only the 2020 manual (S-026). No copy of the reported 5th edition was found.
- **German S1 guideline 030-057 (2025-11).** register.awmf.org still serves the Anubis anti-bot page and dgn.org a JavaScript-only page. dgbfb.de holds only a one-page press note. No other copy was found.
- **NHG-Standaard Hoofdpijn.** Still HTTP 401 behind a security check on richtlijnen.nhg.org and nhg.org.
- **Polish 2021 recommendations (PMID 33507529, the log's "full text not retrieved").** Now read in full at https://journals.viamedica.pl/neurologia_neurochirurgia_polska/article/download/PJNNS.a2021.0007/54346. The diary statements (triptan intake, headache days, MIDAS, 50% reduction in monthly headache days) add no output beyond OUT-005, OUT-014, OUT-018 and OUT-026.
- **Swiss SKG recommendations.** The 2024 summary in Ars Medici and the FMH "Guidelines Schweiz" entry add no output. The full 10th edition is not on headache.ch.
- **Korean Headache Society.** A June 2026 press report says new guidelines are still in preparation; no full text exists.
- **Hungarian.** No national guideline was found.
- **Newer editions.** PubMed shows no ICHD-4 (only work-in-progress papers) and no newer edition of S-002 to S-007, S-011 or S-013.
- **Wearing-off.** A view of headache frequency against the end of the injection interval rests only on one bullet in S-023 (Frage 1) and is not raised for lack of a recommendation.
- **OUT-014 class names.** OUT-014's "simple analgesics" is equivalent to ICHD-3's "non-opioid analgesic" class, so it is not raised.

## Verification coverage

Counts are distinct quoted strings per source, including list items, caveat quotes, grade labels and source-text quotes in section 5. Quoted section headings inside location parentheses were also checked, but are not counted here. "Script (ws)" means the string matched only when whitespace and line-break hyphens were ignored; I inspected each such case in the source. "Manual" means I confirmed the string on the page or in a layout extraction because the text layer is interrupted.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 14 | 14 | 0 | — |
| S-002 | 17 (incl. 3 list items) | 17 (1 script (ws): "moderate/ severe") | 0 | — |
| S-003 | 2 | 2 | 0 | — |
| S-004 | 3 | 3 (1 script (ws)) | 0 | — (Europe PMC fullTextXML of PMC6501455) |
| S-005 | 7 | 7 (1 script (ws): line-break hyphen in "meta-analyses") | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 | 0 | — |
| S-008 | 8 | 8 | 0 | — |
| S-009 | 3 | 3 | 0 | — |
| S-010 | 4 | 4 (2 script (ws): line-break hyphens); abstract quotes also exact in the PubMed efetch abstract | 0 | PubMed web page not used (it challenges curl); E-utilities efetch used |
| S-011 | 3 | 3 | 0 | — (Europe PMC fullTextXML) |
| S-012 | 4 | 4 (1 script (ws)) | 0 | — (Europe PMC fullTextXML) |
| S-013 | 4 | 4 (location defect: R04-01) | 0 | — (Europe PMC fullTextXML) |
| S-014 | 12 | 12 (5 script (ws): XML spacing around citations) | 0 | — (Europe PMC fullTextXML) |
| S-015 | 13 (incl. 2 list items) | 13; all recommendation numbers confirmed; last updated 3 June 2025 | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6 throughout) | 0 | — |
| S-017 | 3 | 3; footer "BASH Guideline V2.0 2026" and dateModified 2026-09-14 confirmed; TOC page still "V1.0 2019" | 0 | — |
| S-018 | 8 | 8 (1 manual: 15B is interrupted by "Level C"); levels of 12A, 14A, 14D, 14E and 15A–D confirmed in the layout text | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 | 0 | — |
| S-021 | 3 | 3 | 0 | — |
| S-022 | 6 | 6 (all manual: line numbers removed; lines 383–384, 393–394, 421–425, 427–429 and 464–465 and pages 11–13 confirmed) | 0 | — |
| S-023 | 4 | 4 (1 script (ws): "[ 7 ]") | 0 | — (Europe PMC fullTextXML) |
| S-024 | 6 | 6 (PDF page + 394 = printed page) | 0 | — |
| S-025 | 1 | 1 | 0 | — |
| S-026 | 2 | 2 | 0 | — |
| S-027 | 6 | 6 | 0 | — |
| S-028 | 2 (incl. 1 in section 5) | 2 (1 script (ws)) | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (1 manual: the chapter side tab interrupts CQ II-2-14 on PDF p. 207 = printed p. 191) | 0 | — |
| S-032 | 6 (3 evidence quotes; 2 quotes and 1 heading in section 5) | 6 | 0 | The listed URL reset the connection twice, then succeeded (redirect to www.brainmed.com/info/detail?id=34408). Attribution "中国疼痛医学杂志 … 2022, 28 (12), 881-898" confirmed. No Crossref DOI exists. |
| S-033 | 6 (incl. 1 grade label) | 6; grade C/5 of section 7.1 also confirmed (OUT-018 evidence basis) | 0 | — |
| S-034 | 4 (incl. 1 grade label) | 4 | 0 | The first two attempts reset; the retry succeeded |
| S-035 | 3 | 3 | 0 | — |
| S-036 | 3 (incl. 1 new in v03, section 5) | 3; Tables 1.1/1.2, reference 5 (PDF p. 80) and DOI (PDF p. 5, Crossref) confirmed; no grade on PDF p. 16 | 0 | — |
| S-037 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-038 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-042 | 2 | 2 (the OUT-011 quote is the Table 2 wording "patient’s headache diary"; the Results text reads "the patient’s") | 0 | — (Europe PMC fullTextXML) |
| S-043 | 1 | 1 | 0 | — (Europe PMC fullTextXML; abstract also via efetch) |
| S-044 | 1 | 1 | 0 | PubMed web page not used; abstract via E-utilities efetch |
| **Total** | **204** | **204** (183 exact script, 13 script (ws), 8 manual) | **0** | — |

## Remarks

### R04-01 [link/citation] — target: OUT-003 (quote from S-013)
- Problem: the [S-013] quote in OUT-003, "For refractory migraine, chart review alone is not sufficient and a minimum period of observation of 6 months is required together with completed diaries.", is located as `(section "Proposed updated definition of resistant and refractory migraine")`. The source has no section with that name.
  - In the PMC full text (Europe PMC fullTextXML of PMC7296705), the article has a "Results" section with no subsections.
  - "Proposed updated definition of resistant and refractory migraine" is the caption of Table 3. The table body is an image (`graphic`), not text.
  - The quoted sentence is in the running text of "Results". It is the paragraph beginning "Refractory migraine is defined by having failed all of the available preventatives …", two paragraphs after Table 3.
  - PROCESS.md section 3 requires the location in the source, and R01-02 treated a wrong section label as a defect.
- Evidence: Results section of https://pmc.ncbi.nlm.nih.gov/articles/PMC7296705/ (checked in the Europe PMC fullTextXML). The Results children are, in order: a paragraph ending "… are reported in Table 3."; table-wrap "Table 3 Proposed updated definition of resistant and refractory migraine"; a paragraph "Definitions are based on fulfilling ICHD III criteria …"; a paragraph "Resistant migraine is defined …"; and a paragraph "Refractory migraine is defined by having failed all of the available preventatives and suffer from at least 8 debilitating headache days per month for at least 6 consecutive months. For refractory migraine, chart review alone is not sufficient and a minimum period of observation of 6 months is required together with completed diaries."
- Earlier history of this item: none. The location has been unchanged since v00, and no earlier remark or fix touched it.
- Required change: in OUT-003, change the location of this [S-013] quote to, for example, `(Results, paragraph defining refractory migraine, after Table 3 "Proposed updated definition of resistant and refractory migraine")`. The quote text and the requirement are unchanged.

### R04-02 [contradiction/duplication] — target: OUT-027 (Evidence basis; source S-037)
- Problem: OUT-027's Evidence basis lists S-037 among national guidelines: "national guidelines (SIGN 155 patient-information checklist, based on the experience of the guideline development group; SBCe, Brazil; SPC, Portugal)". Section 5 types S-037 as "Consensus statement (national society)", and the source describes itself as a consensus that rests on literature and personal experience.
  - PROCESS.md section 3 requires each requirement to state whether its support is evidence-graded, consensus or expert opinion. Listing S-037 under guidelines misstates the nature of that support and contradicts section 5.
  - Elsewhere the document keeps the two types apart, for example "national guidelines and consensus (Russia; SFEMC, France; DMKG/ÖKSG/SKG)" in OUT-004 and "national consensus (Poland)" in OUT-025.
  - This is the only evidence-basis line where a consensus source is labelled a guideline.
- Evidence: S-037 abstract, https://pmc.ncbi.nlm.nih.gov/articles/PMC9703891/ (verified in the Europe PMC fullTextXML): "The Brazilian Headache Society (Sociedade Brasileira de Cefaleia, SBCe, in Portuguese) nominated a Committee of Authors with the aim of establishing a consensus with recommendations regarding prophylactic treatment for episodic migraine based on articles published in the worldwide literature, as well as personal experience."
- Earlier history of this item: none. The OUT-027 Evidence basis has been unchanged since v00. R03-01 changed the S-036 entry, which is also cited in OUT-027, but not this line.
- Required change: in OUT-027's Evidence basis, move "SBCe, Brazil" out of "national guidelines (…)" and into the consensus part, for example "national guidelines (SIGN 155 patient-information checklist, based on the experience of the guideline development group; SPC, Portugal); consensus (SBCe, Brazil; EHF 2020)". The strength stays SHOULD.

## Notes on frozen items (for the human)
None.
