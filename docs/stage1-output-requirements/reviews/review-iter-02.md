# Review — iteration 02
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v01
Date: 2026-10-20

## Summary
I downloaded all 44 sources again with curl, using a new scratch directory and not reusing earlier agents' files. I checked every quoted string in v01 against the extracted text. That covers 199 distinct strings (216 occurrences): 187 evidence quotes, 5 list items, 4 grade labels, and 3 source-text quotes in the S-028 and S-032 entries of section 5. All 199 are verbatim at their URLs. 189 matched by script (NFKC-, whitespace- and dash-insensitive). I confirmed the other 10 by hand where the text layer is broken:
- S-022: line numbers break up the text;
- S-018 15B: the margin label "Level C" interrupts the sentence;
- S-031 CQ II-2-14: the chapter side tab interrupts the sentence;
- S-005 and S-010: a hyphen falls at a line break.

Using page splits, XML section paths and the NICE recommendation numbering, I re-checked all v01 additions and every location of a PDF quote, every section label of an XML quote, every NICE recommendation number, and the AAN levels on a layout render. All are correct. The v01 fixes for R01-01 to R01-11 are correct and introduced no misquote, scope violation or strength mismatch. The two remarks below are:
- an evidence-backed dimension of preventive-treatment success that no output covers: response to acute treatment. Two quotes already in the document name it.
- a counting rule in the v01 change log that does not produce the totals it reports.

Checked and not raised as remarks:
- The IHS Real-World Evidence guideline 2025 and the IHS 2025 position statement "Early treatment in migraine" are now readable in the Leiden University repository, although the search log lists the first as not retrieved. Neither contains a diary-output statement that changes a requirement. The RWE guideline's diary content concerns data collection, and its advice to say "4 weeks" instead of "1 month" is for research studies; OUT-001 already handles this with its period-length caveat.
- The 2024 SEN/semFYC/SEMERGEN/AEMICE migraine treatment consensus (Med Clin (Barc), PMID 38643025) is readable only as an abstract.

## Verification coverage

Counts are distinct quoted strings per source, including list items, grade labels and quotes in section 5. "Manual" means the script failed because of a text-layer artefact, and I confirmed the quote by reading the page or a layout render.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 14 | 14 | 0 | — |
| S-002 | 17 (incl. 3 list items) | 17 | 0 | — |
| S-003 | 2 | 2 | 0 | — |
| S-004 | 3 | 3 | 0 | — (PMC HTML and Europe PMC XML both retrieved) |
| S-005 | 7 | 7 (1 manual: "meta-analyses" split by a line-break hyphen) | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 | 0 | — |
| S-008 | 8 | 8 | 0 | — |
| S-009 | 3 | 3 | 0 | — |
| S-010 | 3 | 3 (1 manual: "patient-reported" split by a line-break hyphen) | 0 | pubmed.ncbi.nlm.nih.gov returns a cookie challenge to curl; I read the abstract quotes through E-utilities efetch |
| S-011 | 3 | 3 | 0 | used Europe PMC fullTextXML (same PMCID) |
| S-012 | 4 | 4 | 0 | as S-011 |
| S-013 | 4 | 4 | 0 | as S-011 |
| S-014 | 12 | 12 | 0 | as S-011 |
| S-015 | 13 (incl. 2 list items) | 13 | 0 | — |
| S-016 | 9 | 9 | 0 | — |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026" and `dateModified` 2026-09-14 confirmed) | 0 | — |
| S-018 | 8 | 8 (1 manual: 15B interrupted by "Level C"); levels of 12A, 14A, 14D, 14E and 15A–D confirmed on a layout render | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 | 0 | — |
| S-021 | 3 | 3 | 0 | — |
| S-022 | 6 | 6 (all manual: line numbers removed; page and line references correct) | 0 | — |
| S-023 | 4 | 4 | 0 | as S-011 |
| S-024 | 6 | 6 | 0 | — |
| S-025 | 1 | 1 | 0 | — |
| S-026 | 2 | 2 | 0 | — |
| S-027 | 6 | 6 | 0 | — |
| S-028 | 2 (incl. GRADE sentence in section 5) | 2 | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (1 manual: side tab in CQ II-2-14, PDF p. 207 = printed p. 191) | 0 | — |
| S-032 | 4 (incl. 2 GRADE quotes in section 5) | 4 | 0 | — |
| S-033 | 6 (incl. 1 grade label) | 6 | 0 | — |
| S-034 | 4 (incl. 1 grade label) | 4 (title page is an image; year 2024 and developers confirmed on a render) | 0 | — |
| S-035 | 3 | 3 | 0 | — |
| S-036 | 2 | 2 | 0 | — |
| S-037 | 1 | 1 | 0 | as S-011 |
| S-038 | 1 | 1 | 0 | as S-011 |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 (section "Conclusion" confirmed) | 0 | as S-011 |
| S-042 | 1 | 1 | 0 | as S-011 |
| S-043 | 1 | 1 | 0 | as S-011; abstract also checked through efetch |
| S-044 | 1 | 1 | 0 | PubMed web page gives a challenge; abstract read through E-utilities efetch |
| **Total** | **199** | **199** (189 by script, 10 manual) | **0** | — |

Bibliographic metadata was checked against PubMed esummary for every source that has a PMID, and against the title pages of the other documents. Authors, titles, journals, volumes, pages, DOIs and PMCIDs are correct. NICE CG150 is last updated 3 June 2025. SIGN 155 is "Revised May 2026". The EMA draft is EMA/137055/2026 Rev. 2, with consultation from 10 September 2026 to 31 January 2027. The AAN guideline was published online on 31 August 2026.

### Completeness search (beyond the document's sources)
- **AWMF S1 030-057 (2025-11) and NHG-Standaard Hoofdpijn.** Both still return an anti-bot page (Anubis; NHG HTTP 401). dgn.org returns a JavaScript-only page. Europe PMC has no open copy.
- **Swedish national knowledge support.** webbutik.skr.se fails with a certificate-name mismatch and nationelltklinisktkunskapsstod.se with an expired certificate. Both confirmed.
- **AHS consensus statements 2019 and 2021.** Wiley returns a Cloudflare challenge (403). Unpaywall reports both as closed.
- **IHS paediatric update 2023 (PMID 37226450).** SAGE returns 403. The Pavia repository holds only the 2019 edition, and the IHS site has no PDF of the update.
- **IHS RWE guideline 2025 (PMID 40095946).** Retrieved from https://scholarlypublications.universiteitleiden.nl/handle/1887/4289175; the KU copy is behind a Cloudflare challenge. No change to any requirement, as stated in the summary.
- **IHS position statement "Early treatment in migraine" 2025 (PMID 41134822).** Retrieved from https://hdl.handle.net/1887/4296121. It has no diary-output statement.
- **EHF/Lifting The Burden community-pharmacist position statement 2025 (PMC12054158).** No diary statement.
- **Korean Headache Society 2021 guideline.** Only press reports were found, in a Korean-language search.
- **Russian clinical recommendations.** No separate recommendation on medication-overuse headache was found; MOH is covered inside S-033. The apicr API returns the same 2024 files for other version suffixes, so no newer version could be identified.
- **SEN manual, 5th edition.** Reported in the press; no copy found.

## Remarks

### R02-01 [missing-requirement] — target: OUT-021 (with OUT-023)
- Problem: no output shows whether the response to acute treatment changes after a preventive treatment is started.
  - Several national guidelines and a national consensus list improved response to acute treatment as a dimension, or a success criterion, of preventive treatment.
  - Quotes already in the document say so: the S-032 quote in OUT-021 lists "对急性期治疗的反应" ("the response to acute treatment") among the indicators of preventive effectiveness, and the S-035 quote in OUT-011 includes "akut atakta ilaçlara artan yanıt" ("an increased response to drugs in the acute attack").
  - Despite that, OUT-021 omits acute-treatment response from its components.
  - OUT-023 summarises acute-treatment effectiveness per drug across treated attacks but never asks for it per period. OUT-034 shows it only for the period since the last consultation.
  - As a result, an improvement in acute-treatment response after a preventive is started cannot be seen.
- Evidence (all verified verbatim):
  - [S-032] section 3.2 "预防性治疗有效性指标", https://brainmed.com/guidance/detail/article/34408. This sentence is already quoted in OUT-011 and OUT-021: "主要包括偏头痛发作频率、头痛持续时间、头痛程度、头痛的功能损害程度及对急性期治疗的反应。"
  - [S-032], the sentence that follows it in the same paragraph: "满足以下任意1条可以认为预防性治疗有效：偏头痛或中重度头痛天数显著减少（如减少50%）；程度显著减轻；持续时间显著缩短；对急性期治疗的反应改善；偏头痛相关失能的改善；偏头痛引起的心理痛苦减少。" Translation: "Preventive treatment can be considered effective if any one of the following is met: a significant reduction in days with migraine or with moderate-to-severe headache (for example a 50% reduction); a significant reduction in severity; a significant shortening of duration; an improvement in the response to acute treatment; an improvement in migraine-related disability; a reduction in migraine-induced psychological distress."
  - [S-035] Kutu 8 / preventive treatment principles, PDF p. 48. Already quoted in OUT-011: "Profilaktik tedavinin başarısı, atak sıklığında ve süresinde %50'lik bir azalma ve akut atakta ilaçlara artan yanıt ile değerlendirilir."
  - [S-042] Results, "Question 6. What are the parameters used to define successful migraine treatment for migraine patients?", panel discussion, https://pmc.ncbi.nlm.nih.gov/articles/PMC12279330/ (verified in the Europe PMC fullTextXML): "Additional parameters include reduced attack duration or severity, enhanced response to acute treatments, improved ability to function, and reduced disability."
- Earlier history of this item: OUT-021 was restated in v01 (R01-05, R01-08). This remark adds a SHOULD component and does not reverse that fix. Not raised before.
- Required change:
  - In OUT-021, add to the SHOULD list (applies where the output is provided): acute-treatment effectiveness (OUT-023), shown for the same pre-treatment baseline and on-treatment periods.
  - In OUT-023, add a matching SHOULD clause: its per-drug outcomes can be shown separately for the pre-treatment baseline and the on-treatment periods of a preventive treatment.
  - Cite [S-032] (the section 3.2 quote already present, and optionally the second sentence above), [S-035] and [S-042].
  - Evidence basis: national guidelines (China; Turkish Ministry of Health protocol) and national expert consensus (Saudi Arabia). Strength: SHOULD. Update the OUT-021 rationale.
  - If the second S-032 sentence is quoted, its 50% figure is the source's criterion and not a requirement (document section 1). Do not restate the criteria as a rule; describe only the output.

### R02-02 [factual-error] — target: section 7, v01 change-log entry ("Totals")
- Problem: the v01 entry says the totals are "counted by the strongest keyword in each statement: 10 MUST, 23 SHOULD, 5 MAY, 1 SHOULD NOT". That rule does not give those numbers.
  - The OUT-032 statement contains "MAY" and "SHOULD" ("Any such output SHOULD state ..."), so its strongest keyword is SHOULD. Under the stated rule the totals would be 24 SHOULD and 4 MAY.
  - The OUT-037 statement contains both "SHOULD NOT" and "SHOULD", so the stated rule does not decide how it is counted.
  - The reported totals do match the primary strength in each requirement's "Strength:" line (OUT-032 "MAY (caveats SHOULD)", OUT-037 "SHOULD NOT").
- Evidence: OUT-032 Statement and Evidence basis lines; OUT-037 Statement and Evidence basis lines (document lines 449, 452, 516 and 519).
- Earlier history of this item: introduced in v01 (fix-iter-01, "Other changes", section 7). Not raised before.
- Required change: make the rule and the totals agree, either by:
  - changing the rule to "counted by the primary strength stated in each requirement's Strength line", which keeps 10/23/5/1; or
  - keeping the rule and correcting the totals (24 SHOULD, 4 MAY) and saying how OUT-037 is counted.

  Make the correction in the v01 entry, or as a dated correction note in the v02 entry, and use the same rule for the v02 totals.

## Notes on frozen items (for the human)
None.
