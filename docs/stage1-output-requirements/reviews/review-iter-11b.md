# Review — iteration 11, re-check b
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v10
Date: 2026-10-20

## Summary
I downloaded all 46 sources again with curl into a new, empty folder of my own. I did not use the files that earlier agents left in the shared scratchpad. I extracted every quoted string in section 3 by script: 213 distinct strings (235 occurrences), including list items. I matched them against the downloaded text, ignoring differences in Unicode form, dashes, apostrophes and whitespace, and checked "[...]" segments in order. 207 matched by script, and I confirmed the other 6 by hand: two line-break hyphens, the AAN "Level C" margin label, the Japanese side tab, and the two SFEMC figure rows, which I read on the embedded images. I also checked the following, and all are correct:
- page offsets, JATS section paths and quoted headings;
- NICE numbers, AAN levels, and the Japanese, Russian and SFEMC grade labels;
- translations, "[...]" omissions, metadata (37 PMIDs through esummary) and totals.

There are two remarks. First, OUT-014 makes a breakdown "by individual drug" a MUST, but none of its quotes from a source that meets the MUST test mentions individual drugs. ICHD-3 notes that do require the individual drugs to be specified are not quoted (R11b-01). Second, the Finnish search-log row says there is no current Käypä hoito migraine guideline. There is one: "Migreeni", published 28 March 2024 (R11b-02). My searches in Swedish, German, Norwegian, Czech, Romanian, Indonesian, Korean, Japanese, Greek and Italian, plus the Moldovan national protocol, found no missing output requirement and no superseding edition. I found no scope violation in authored text.

## Verification coverage
"Script" means the string matched in the downloaded text. "Manual" means I confirmed it in the `-layout` text, on a page render or on the embedded figure image. Bracketed numbers are quoted strings in section 5. Of the 79 section-5 strings, 70 are source strings: 67 matched by script, and 3 I confirmed by hand (NICE prints "Do not" with a capital; "FORCE" and "FORCE DE LA RECOMMANDATION" are figure text). The other 9 are the document's own translations, which I checked for faithfulness. I also checked 59 headings quoted inside locations: 54 by script and 5 by hand (2 figure titles, 2 English renderings of S-033 table titles, 1 heading printed in capitals). The 6 grade labels (S-031 ×2, S-033, S-034, S-024 "Fort", S-025 "Fort") are verified and not counted in the table.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 15 | 15 (PDF page = printed page; p. 122 note 2, p. 190 A1.1, pp. 209–210) | 0 | — |
| S-002 | 17 | 17 (PDF page + 1025) | 0 | — |
| S-003 | 2 | 2 (PDF page + 814) | 0 | — |
| S-004 | 7 | 7 (JATS 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5) | 0 | PMC page serves a challenge page to curl; used Europe PMC fullTextXML |
| S-005 | 7 | 7 (1 manual: "meta-" at a line break in the layout text; PDF page + 802) | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 (accepted manuscript pp. 20, 21, 25) | 0 | — |
| S-008 | 8 | 8 | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | 0 | — |
| S-010 | 4 | 4 (1 manual: "patient-" at a line break; abstract quote in the efetch abstract) | 0 | PubMed page returns HTTP 203 challenge; used E-utilities efetch |
| S-011 | 3 | 3 | 0 | used Europe PMC fullTextXML |
| S-012 | 8 | 8 | 0 | used Europe PMC fullTextXML |
| S-013 | 4 | 4 | 0 | used Europe PMC fullTextXML |
| S-014 | 12 | 12 | 0 | used Europe PMC fullTextXML |
| S-015 | 13 [+4] | 13 [+4]; recommendation numbers and "Last updated: 03 June 2025" confirmed | 0 | — |
| S-016 | 9 | 9 (PDF page = printed + 6; "Revised May 2026") | 0 | — |
| S-017 | 3 [+5] | 3 [+5] (sections B and E of 2.1.3; footer V2.0 2026; dateModified 2026-09-14; TOC "V1.0 2019") | 0 | — |
| S-018 | 8 | 8 (1 manual: 15B, "Level C"); levels confirmed on renders of pp. 7–8 | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 (printed p. 4 = PDF p. 7) | 0 | — |
| S-021 | 3 | 3 (in effect 31 July 2007) | 0 | — |
| S-022 | 6 | 6 (margin line numbers and sections 5.2.2, 5.2.3, 5.2.5.2 confirmed in the layout text; consultation 10 Sep 2026 – 31 Jan 2027) | 0 | — |
| S-023 | 4 | 4 | 0 | used Europe PMC fullTextXML |
| S-024 | 9 [+18] | 9 [+17] (+1 translation; 1 manual: Rd5 and all Rd1–Rd10 "Fort" on the 2006 × 1337 px image; English Part 1 strings matched; PDF page + 394, English + 724) | 0 | — |
| S-025 | 2 [+25] | 2 [+25] (1 manual: RT25, heading, "FORCE", RT15–RT32 "Fort" and RT33–RT34 "Modéré" on the 1864 × 2452 px image; English Part 2 strings matched) | 0 | — |
| S-026 | 0 (not cited) | — | — | downloaded; superseded entry |
| S-027 | 6 [+1] | 6 [+1] ("80% respons rate" is diary completion in context; "uitkomstaten" is the source's spelling) | 0 | — |
| S-028 | 1 [+4] | 1 [+3] (+1 translation) | 0 | — |
| S-029 | 2 [+1] | 2 [+1] | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19) | 0 | — |
| S-031 | 7 | 7 (1 manual: side tab, PDF p. 207 = printed p. 191; printed = PDF − 16 for all; grades B and A confirmed) | 0 | — |
| S-032 | 3 [+5] | 3 [+3] (+2 translations) | 0 | — |
| S-033 | 5 | 5 (grade C/5 after 2.5 and 7.1 confirmed; title page "Год утверждения: 2024") | 0 | — |
| S-034 | 3 | 3 (grade C/5 after 7.1 confirmed) | 0 | — |
| S-035 | 3 | 3 (PDF pp. 48, 78; Revizyon 01, Ağustos 2025, ISBN 978-975-590-958-5) | 0 | — |
| S-036 | 2 [+3] | 2 [+2] (+1 translation; DOI printed in the PDF) | 0 | — |
| S-037 | 1 | 1 | 0 | used Europe PMC fullTextXML |
| S-038 | 1 | 1 | 0 | used Europe PMC fullTextXML |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 (square brackets are in the source; G.U. 93 of 22/04/2025) | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | used Europe PMC fullTextXML |
| S-042 | 2 | 2 (Question 6 consensus statement and panel discussion) | 0 | used Europe PMC fullTextXML |
| S-043 | 1 | 1 (elocation 135) | 0 | used Europe PMC fullTextXML and efetch |
| S-044 | 1 | 1 | 0 | PubMed page returns HTTP 203 challenge; used E-utilities efetch |
| S-045 | 4 [+9] | 4 [+5] (+4 translations; PDF pp. 113, 395; imprint and ISBNs PDF p. 4) | 0 | — |
| S-046 | 3 [+4] | 3 [+4] (printed p. 5 = PDF p. 8; landing page "Draft", FDA-2022-D-1729) | 0 | — |
| **Total** | **213 [+79]** | **213 [+70 source strings, 9 translations]** (207 script, 6 manual) | **0** | — |

Other checks:
- **Totals.** 39 requirements (10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT), 46 source rows, and 45 sources cited (all except S-026) reproduce under the stated rule.
- **Cross-references.** They resolve, and no ID is reused.
- **Scope.** A scan of the authored, unquoted text found no input, storage or derivation content.
- **Completeness searches.** Searched with no new output requirement or superseding edition:
  - **Sweden:** "Riktlinje för migrän", NPO 2022, PDF at vardpersonal.1177.se. Its diary, PROM and stop criteria are covered by OUT-018, OUT-025, OUT-026, OUT-027, OUT-033 and OUT-034.
  - **Germany:** AWMF 030-057 (2025-11) still serves an anti-bot page. I did not try to get past it, and no other copy was found.
  - **Moldova (Romanian):** the Moldovan national protocol PCN-284 (2017) repeats S-014.
  - **Greece:** the Hellenic consensus 2019 (PMC6911284).
  - **Other languages:** Czech, Romanian, Indonesian, Korean and Italian found only press items or reviews. The Japanese 2021 guideline is still the current edition.
  - **IHS:** PubMed 2025–2026 shows no new IHS migraine trial-guideline edition.

## Remarks
### R11b-01 [unsupported/overstated] — target: OUT-014 (Statement clause "and by individual drug"; Evidence; Evidence basis)
- **Problem.** The OUT-014 Statement makes it a MUST that acute medication days are broken down "by drug class as used in ICHD-3 code 8.2 and its subtypes [S-001] ... and by individual drug". None of the quotes from a source that meets the MUST test (PROCESS.md section 3) supports the per-drug part:
  - ICHD-3 item 12 speaks of "a more precise judgement of medication consumption".
  - AAN/AHS 15D speaks of "use of acute therapy".
  - Japan CQ I-10 speaks of "服薬日数" (medication days).
  - IHS section 1 and FDA III.A.5 speak of acute medication use or days.

  Only two quotes mention the type of medicine:
  - S-024 p. 401, "le type de médicament", which is running text;
  - S-033 p. 19, "определение типа препаратов злоупотребления", which is a comment to a table, not a graded recommendation.

  Elsewhere the document does not let such national text carry a MUST (see OUT-018 for SIGN 4.1, and OUT-033). The Statement's reference to ICHD-3 covers drug classes and subtypes, not individual drugs. As documented, the per-drug clause therefore has no MUST-level support. That support does exist: the classification standard asks for the individual drugs to be specified, but it is not quoted.
- **Evidence.** All verified in https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf (PDF page = printed page). Pages 123 and 124 were also checked on renders.
  - 8.2, note 1, p. 122: "Patients should be coded for one or more subtypes of 8.2 Medication-overuse headache according to the specific medication(s) overused and the criteria for each below."
  - 8.2.2 Triptan-overuse headache, note 1, p. 123: "The triptan(s) will usually be specified in parenthesis." In the text layer the justified line breaks this sentence apart, so confirm it on the page.
  - 8.2.3 Non-opioid analgesic-overuse headache, comments, p. 123: "A patient who fulfils criteria for more than one of the subforms of 8.2.3 Non-opioid analgesic-overuse headache should be given all applicable codes."
  - 8.2.3.2 NSAID-overuse headache, note 1, p. 124: "The NSAID(s) should be specified in parenthesis."
  - 8.2.4 Opioid-overuse headache, note 1, p. 124: "The opioid(s) should be specified in parenthesis."
  - 8.2.5 Combination-analgesic-overuse headache, note 2, p. 124: "The combination-analgesic(s) should be specified in parenthesis."
- **Earlier history of this item.**
  - The OUT-014 Statement is identical in all 11 snapshots, v00–v10.
  - The OUT-014 Evidence and Evidence basis changed in v06 (R06-01, the SEN 2026 quote) and v07 (R07-02, the FDA quote). The oscillation watch list notes that its MUST must not again rest on "SEN, grade B".
  - This remark adds ICHD-3 evidence for an unquoted clause. It does not touch the SEN or FDA items and reverses no earlier fix.
  - No earlier review raised the per-drug clause. Review 04 discussed only the class names.
- **Required change.** Choose one:
  - **(a) Keep MUST.** Add to OUT-014's Evidence 8.2 note 1 (p. 122) and at least one of the subtype notes above, for example 8.2.2 note 1 and 8.2.4 note 1. Add one clause to the Rationale or Evidence basis: ICHD-3 codes medication-overuse headache according to the specific medications overused and asks for the individual drugs to be specified. Quote only the notes, not the day criteria next to them. No Statement change is needed.
  - **(b) Lower the per-drug clause.** Move "and by individual drug" into a separate SHOULD sentence that rests on its current support (SFEMC, Russia), and state the split in the Strength line, as OUT-005 does.

### R11b-02 [factual-error] — target: section 6, Search log, row "Finnish"
- **Problem.** The row reads "No current Käypä hoito migraine guideline appeared in the kaypahoito.fi recommendation list." This is wrong. The Finnish national clinical practice guideline "Migreeni" is published on kaypahoito.fi as a current Käypä hoito recommendation, and it makes several statements on diary-based outputs.
  - PROCESS.md section 4 requires the log to record what was and was not found, and section 9 counts factual errors as remarks. R07-02 is the precedent: a log row said "FDA guidance on preventive migraine drugs: none found" when the guidance existed.
  - At present the document's only Finnish source is the Kela reimbursement page (S-039).
- **Evidence.** All verified on 2026-10-20 in the raw HTML of https://www.kaypahoito.fi/hoi36050 (HTTP 200, page title "Migreeni"). The page is linked as "Migreenin Käypä hoito –suositus 2024 https://www.kaypahoito.fi/hoi36050" in a 2024 Finnish Institute of Occupational Health presentation: https://ttl.fi/sites/default/files/2024-09/migreenin-hoito-2024_perjantai-meeting.pdf.
  - **Header.**
    - "Käypä hoito -suositus | Julkaistu: 28.03.2024 | Tila: päivityksessä". Translation: "Käypä hoito recommendation | Published: 28.03.2024 | Status: being updated".
    - "Suomalaisen Lääkäriseuran Duodecimin ja Suomen Neurologinen yhdistys ry:n asettama työryhmä". Translation: "Working group appointed by the Finnish Medical Society Duodecim and the Finnish Neurological Society".
  - **Section "Keskeinen sisältö":** "Päänsärkypäiväkirja tai -kalenteri on hoitosuunnitelman ja seurannan peruste." Translation: "A headache diary or calendar is the basis of the treatment plan and of follow-up."
  - **Section "Lääkkeellinen estohoito":**
    - "Hoidon tehon seurannassa käytetään päänsärkypäiväkirjaa jo ennen estohoidon aloitusta." Translation: "In monitoring treatment efficacy, a headache diary is used already before preventive treatment is started."
    - "Estolääkityksen tehoa ja sietoa arvioidaan 2–3 kuukauden kuluttua sen aloituksesta." Translation: "The efficacy and tolerability of preventive medication are assessed 2–3 months after it is started."
  - **Section "CGRP-reitin monoklonaaliset vasta-aineet aikuisten migreenin estohoidossa", subsection "Hoidon seuranta":** "Vastetta arvioidaan potilaan täyttämän päänsärkypäiväkirjan avulla, johon on hyvä merkitä erikseen migreenipäivät, mahdolliset muut päänsärkypäivät ja kohtauslääkkeiden käyttö." Translation: "The response is assessed with the headache diary completed by the patient, in which it is good to mark separately migraine days, any other headache days and the use of acute medication."
  - **Grading.** The guideline grades its evidence summaries A–D (the page carries "Näytönastekatsaukset" and evidence-level tags A, B and C). None of the four sentences above carries an evidence-level tag.
  - **Content.** The statements agree with OUT-004, OUT-005, OUT-014, OUT-018, OUT-021 and OUT-029. I found no output the guideline requires that the document lacks, and no Statement or strength needs to change.
- **Earlier history of this item.**
  - The Finnish row is identical in all 11 snapshots, v00–v10. No remark or fix has addressed it.
  - Review 08 repeated the error under "Checked and not raised" ("Finnish: there is still no Käypä hoito migraine guideline").
  - The remark reverses no earlier fix.
- **Required change.** Replace the sentence with an accurate record of the Käypä hoito recommendation "Migreeni" (Duodecim and Suomen Neurologinen yhdistys working group; published 28.03.2024; status "päivityksessä"; https://www.kaypahoito.fi/hoi36050). Do one of the following:
  - **(a) Record it as found and not used**, because its diary statements add no output beyond OUT-004, OUT-005, OUT-014, OUT-018, OUT-021 and OUT-029. This alone resolves the remark.
  - **(b) Cite it as new source S-047** where it supports an existing requirement, for example OUT-018 (a diary before preventive treatment; assessment at 2–3 months). Its type would be "Clinical practice guideline (national; Käypä hoito evidence summaries graded A–D; the quoted statements carry no evidence level)". Section 5 and the change-log source totals must then be updated. If the "Hoidon seuranta" sentence is quoted, quote only its output-relevant part, because its second half ("johon on hyvä merkitä erikseen ...") is a recording instruction (PROCESS.md section 2).

## Notes on frozen items (for the human)
None.
