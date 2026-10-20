# Review — iteration 18
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v17
Date: 2026-10-20

## Summary
I downloaded all 46 section-5 sources again with curl into a new, empty folder of my own, together with the English SFEMC Parts 1 and 2, the BASH contents page, the Swedish Kela page, the FDA landing page, the PubMed abstracts (E-utilities) and both the Europe PMC fullTextXML and the PMC pages of S-012 and S-013. I did not use files that earlier agents left in the shared scratchpad. Every one of these requests returned HTTP 200; S-032 needed one retry after a connection reset. All 301 quoted strings on the Evidence and Caveats lines are verbatim at their URLs (288 by script, 13 by hand on page renders, the `-layout` text or the embedded figure images), all 164 strings quoted inside locations are correct, every stated page matches, and the 70 translations, the grades, the 37 PMIDs, the section-5 dates and the totals are correct. The v17 changes to OUT-023 and OUT-024 are accurate: the three new S-012 sentences and the S-013 sentence are verbatim at the stated positions on both the PMC pages and in the XML, and the corrected S-013 paraphrase is faithful. Reading OUT-023 against the EHF definition it says it lets readers apply found one gap: the outputs give the non-pain-symptom component of that definition only at 2 hours and only for the most bothersome symptom and three named symptoms, while the definition requires that component to be reached within 2 h and maintained for 24 h (R18-01). Searches in Romanian, Hebrew, Slovak, Ukrainian, Persian, Bulgarian and Macedonian, and in PubMed for 2025–2026, found no other missing output requirement and no superseding edition.

## Verification coverage
"Quotes checked" counts the quoted strings on the Evidence and Caveats lines of section 3 (quotes, list items, grade labels and figure labels), once per citation. "Manual" means confirmed on a 150-dpi page render, in the `-layout` text or on the embedded figure image. "Read in context" means that I read each distinct quote with the surrounding paragraph and section (at least 300 characters on each side, the whole section where its role was in doubt; S-012 and S-013 in full) and checked it against the clause it is attached to. Checked separately: 164 strings quoted inside locations (153 by script; the other 11 are the S-021 Annex title and the S-037 heading, printed in capitals, three English Part 1 strings read in the English S-024 PDF, and four figure headings read on the images), 70 translations, and the strings and dates in section 5.

| Source ID | Quotes checked | Verified verbatim | Read in context (yes/no) | Not found | Unreachable (what you tried) |
|---|---|---|---|---|---|
| S-001 | 24 | 24 (1 manual: 8.2.2 note 1 in the right column of the p. 123 `-layout` text). PDF page = printed page. A1.1 note 3 and the 8.2 "expert opinion" sentence behind the caveats also confirmed | yes | 0 | — |
| S-002 | 26 | 26 (printed = PDF + 1025) | yes | 0 | — |
| S-003 | 6 | 6 (printed = PDF + 814) | yes | 0 | — |
| S-004 | 10 | 10 (JATS 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5) | yes | 0 | Europe PMC fullTextXML |
| S-005 | 9 | 9 ("meta-analyses" hyphenated at a line end; printed = PDF + 802) | yes | 0 | — |
| S-006 | 9 | 9 (1 manual: the 2.3.3.2 recommendation, read on a 150-dpi render of p. 10) | yes | 0 | — |
| S-007 | 8 | 8 (accepted manuscript pp. 20–22, 25) | yes | 0 | — |
| S-008 | 11 | 11 (pp. 9, 11–13) | yes | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | yes | 0 | — |
| S-010 | 8 | 8 (abstract quotes in the efetch abstract; pp. 3 and 7) | yes | 0 | E-utilities efetch for the abstract |
| S-011 | 3 | 3 | yes | 0 | Europe PMC fullTextXML |
| S-012 | 13 | 13 (also matched on the PMC page, which served the full article to curl; v17 sentences at Background ¶3 s5 and "Definition of triptan failure", paragraph "As stated above", s5 and s6) | yes (full text) | 0 | — |
| S-013 | 11 | 11 (also on the PMC page; "Debilitating headache" ¶1 last sentence) | yes (full text) | 0 | — |
| S-014 | 14 | 14 ("charting outcomes" occurs both under "Diaries and calendars" and in the stated section) | yes | 0 | Europe PMC fullTextXML |
| S-015 | 13 | 13 (Published 19 September 2012; last updated 03 June 2025) | yes | 0 | — |
| S-016 | 11 | 11 (PDF = printed + 6; "Revised May 2026") | yes | 0 | — |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026", dateModified 2026-09-14 on both section pages; contents page "V1.0 2019") | yes | 0 | — |
| S-018 | 15 | 15 (1 manual: 15B, interrupted by "Level C"; levels of 12A, 14A–14F and 15A–15D confirmed in the `-layout` text) | yes | 0 | — |
| S-019 | 3 | 3 (p. 3) | yes | 0 | — |
| S-020 | 5 | 5 (printed = PDF − 3) | yes | 0 | — |
| S-021 | 4 | 4 (pp. 5, 6, 11; 24 January 2007, 31 July 2007) | yes | 0 | — |
| S-022 | 6 | 6 (all manual: margin line numbers removed; lines 383–384, 393–394, 421–425, 427–429, 464–465 on pp. 11–13) | yes | 0 | — |
| S-023 | 4 | 4 | yes | 0 | Europe PMC fullTextXML |
| S-024 | 13 | 13 (1 manual: Rd5 and "Fort" on the 2006 × 1337 px Figure 3 image; English Part 1 grading text p. 726 and Table 3 p. 731) | yes | 0 | — |
| S-025 | 5 | 5 (2 manual: RT25, cited twice, under "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE," with "Fort", on the 1864 × 2452 px Figure 1 image; RT15–RT32 "Fort", RT33–RT34 "Modéré") | yes | 0 | — |
| S-026 | 0 (not cited) | — (URL returns HTTP 200) | — | — | — |
| S-027 | 7 | 7 | yes | 0 | — |
| S-028 | 1 | 1 | yes | 0 | — |
| S-029 | 2 | 2 | yes | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19; section 2.4 heading confirmed) | yes | 0 | — |
| S-031 | 11 (incl. 2 grade labels) | 11 (1 manual: CQ II-2-14 across the side tab, render of PDF p. 207 = printed p. 191, grade A) | yes | 0 | — |
| S-032 | 5 | 5 (full-width "：" and "；" as in the source HTML; section 3.2 carries no grade) | yes | 0 | Connection reset once; retry succeeded |
| S-033 | 5 | 5 (grade C/5 after 2.5 and 7.1) | yes | 0 | — |
| S-034 | 3 | 3 (p. 34 with grade C/5; p. 50) | yes | 0 | — |
| S-035 | 5 | 5 (PDF pp. 48, 78) | yes | 0 | — |
| S-036 | 2 | 2 (PDF p. 16) | yes | 0 | — |
| S-037 | 1 | 1 | yes | 0 | Europe PMC fullTextXML |
| S-038 | 1 | 1 | yes | 0 | Europe PMC fullTextXML |
| S-039 | 2 | 2 | yes | 0 | — |
| S-040 | 2 | 2 | yes | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | yes | 0 | Europe PMC fullTextXML |
| S-042 | 3 | 3 (Table 2 row Question 6; Results panel discussion) | yes | 0 | Europe PMC fullTextXML |
| S-043 | 1 | 1 (Abstract, Background; article number 135) | yes | 0 | Europe PMC fullTextXML |
| S-044 | 1 | 1 | yes | 0 | E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113, 395; printed = PDF − 2; section 5.4.7.1 heading on p. 394) | yes | 0 | — |
| S-046 | 3 | 3 (printed = PDF − 3; landing page "Draft", June 2023, FDA-2022-D-1729) | yes | 0 | — |
| **Total** | **301** | **301** (288 script, 13 manual) | **all 259 distinct quotes** | **0** | — |

### Other checks
- **v17 changes (OUT-023, OUT-024).** `diff history/v16.md history/v17.md` touches only the header, OUT-023, OUT-024, section 4 and the change log. The three new OUT-023 quotes and the new OUT-024 quote are verbatim at their stated positions. The new Rationale and Evidence-basis sentences paraphrase S-012, S-013 and S-024 (p. 401, "la posologie, le moment et la voie d'administration", running text "il est recommandé") faithfully, and "none of these statements carries a recommendation grade" is true. The corrected OUT-024 paraphrase of S-013 now names timing, dosage and formulations, as the source does. No new text describes input, storage or derivation, and the S-012 triptan-failure definitions with numeric criteria are still not quoted.
- **Translations and omissions.** I read all 70 translations against their originals (Dutch, Danish, German, French, Spanish, Portuguese, Italian, Finnish, Russian, Turkish, Chinese, Japanese). All are faithful. Every "[...]" and every quote cut at its start or end leaves out recording instructions, age limits, references, list items or a trailing clause about data collection (for example the S-031 CQ II-1-6 sentence, cut before "が" and the clause on prospective daily collection). None changes the meaning.
- **Grades and types.** AAN levels (12A, 14A–14F, 15A–15D), the Japanese grades A and B, the Russian C/5 grades, the SFEMC "Fort"/"Strong" ratings, and the ungraded status of SIGN 4.1, China 3.2, SEN 2026 (the quoted box items and the running-text sentence on MIDAS/HIT-6), Japan CQ VI-3 and SFEMC p. 401 match the sources.
- **Metadata.** All 37 PMIDs (esummary) match authors, journals, years, volumes, pages, DOIs and PMCIDs; S-018 was published online on 31 August 2026 (ArticleDate) in Neurology 2026;107(7):e214881.
- **Totals and IDs.** By the stated rule: 39 requirements, 10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT; 46 source rows, 45 cited (all but S-026); no duplicate ID and no dangling OUT reference.
- **Scope.** I read every Statement, Rationale, Evidence basis and Caveat. None describes input data, storage or a derivation rule beyond the unit and statistic examples accepted in earlier iterations.

### Checked and not raised
- **OUT-023, dose.** The three sources quoted for the v17 formulation element also name dose (S-012 Background: "a higher dose and a different formulation"; S-013: "dosage"; S-024: "la posologie"), and OUT-023 does not split per-drug outcomes by dose. Dose is already an output of OUT-024 ("dose changes", acute list included, with the S-013 support named in its Evidence basis), and none of the EHF definitions that OUT-023 and OUT-024 name uses dose as a criterion (formulation, by contrast, is named in the refractoriness definition). No change required.
- **OUT-018, "aligned to the treatment start date" versus time points such as "8–12 weeks at target dose" and "after onabotulinumtoxinA cycles".** The output shows the value of every period after the start, so a reader can make the comparison at any of these time points; the date the dose changed is shown by the OUT-009 markers and in OUT-024. The requirement does not claim to mark the time points. Not raised.
- **OUT-020, "underlying values (OUT-018, OUT-019)" when the named criterion is IHS Q6 or the DMKG criterion, which also use MIDAS, HIT-6 or PGIC.** Showing the frequency values meets the stated purpose (a label is never the sole indicator), and OUT-021 shows the instrument results for the same periods. Not raised.
- **AAN/AHS 2026 recommendations not cited.** 14B (level B, onabotulinumtoxinA assessed after 24 weeks) agrees with the OUT-018 examples; 16B (level A, monitor adverse events at follow-up) and 17A/17B (level B, counselling on discontinuation) concern clinician actions, not a diary output, which is the reasoning the document already applies to SFEMC Rd5/RT25 in OUT-033. They would not change any strength.
- **SFEMC Figure 1, RT26 ("Fort").** Continue prophylaxis 6–12 months, taper, and resume if attack frequency rises during tapering or after stopping. It agrees with OUT-022 (SHOULD) and would not change it.
- **OUT-028 and ICHD-3 1.3 ("for >3 months").** ICHD-3 note 2 asks for a diary of at least one month; the duration beyond the view comes from history. No change.
- **Italian expert Delphi (Barbanti P, Tassorelli C, Vernieri F, et al. Neurol Sci 2026;47(6):500; PMID 42151647; PMC13183690; industry-funded medical writing).** Its statements 22 and 27 express acute-medication overuse in doses per month, which conflicts with the ICHD-3 day-based criteria that OUT-014 and OUT-016 follow. A single funded Delphi does not support a new output. Its statement 21 corroborates R18-01 (see there).
- **Polish 2021 recommendations (PMID 33507529).** The search log records them as not retrieved; the full text is now downloadable from journals.viamedica.pl. Their diary statements (headache days, severity, other symptoms, number and doses of medications; diary-based response to CGRP antibodies) add no output beyond OUT-004, OUT-010, OUT-012, OUT-014 and OUT-018.
- **Completeness searches with no quotable output requirement:** Romanian (no national guideline text), Hebrew (patient information only), Slovak (paywalled review articles), Ukrainian (no current migraine protocol), Persian (no national guideline), Bulgarian (none), Macedonian (the MoH "Glavobolka" PDF returns HTTP 404). PubMed 2025–2026: the IHS position statement on early treatment (Cephalalgia 2025, PMID 41134822) concerns when to start prevention; there is no new edition of the IHS trial guidelines, ICHD-3 or the EHF documents cited.

## Remarks
### R18-01 [missing-requirement] — target: OUT-023 (Statement, Rationale, Evidence basis, Evidence, or Caveats); consequentially OUT-024 (refractoriness purpose clause)
- **Problem.** OUT-023 says its outputs exist "so that the EHF definitions of effective attack treatment and triptan response [S-012] can be applied", and adds, "To allow the EHF definition of effective attack treatment [S-012] to be applied", headache relief at 2 hours and "whether that relief was maintained to 24 hours", and drug-related adverse events. The EHF definition, quoted in OUT-023, requires a well-being status that is reached within 2 h **and maintained for at least 24 h**, defined by all three of: improved headache (A), "Absent or minimal disturbances due to migraine-related non-pain symptoms" (B), and no meaningful drug-related adverse events (C). The document provides the 24-hour maintenance for A, and C, but for B it provides only:
  - OUT-023: "absence of the most bothersome symptom at 2 hours";
  - OUT-012: "the presence of migraine-associated symptoms (nausea/vomiting, photophobia, phonophobia) and the patient's most bothersome symptom ... in the response of individual treated attacks", with no time point.

  No output shows whether non-pain symptoms stayed absent or minimal to 24 hours, and the symptom set is narrower than the EHF's, which the panel deliberately left broad. An attack whose headache stays mild but whose nausea returns at 6 hours appears effectively treated in the specified outputs although it is not under the EHF definition. The triptan-responder definition ("at least 3 out of 4 consecutive attacks" effectively treated) and the triptan-refractoriness category that OUT-024 says it lets readers apply ("so that ... the EHF definition of triptan refractoriness [S-012] can be applied") inherit the gap, because both rest on the per-attack EHF status. This is the defect type of R08-01 and R17b-01: a definition the requirement names cannot be applied from the outputs it specifies.
- **Evidence.** All verified verbatim on 2026-10-20.
  - [S-012] https://pmc.ncbi.nlm.nih.gov/articles/PMC9555163/ (also in the Europe PMC fullTextXML), Results > Consensus > "Definition of effective treatment of a migraine attack" — already quoted in OUT-023: "Reaching, within 2 h from intake of the drug, and maintaining, for at least 24 h a well-being status as defined by all the following:" followed by the list items "Improvement of headache from severe or moderate to mild or absent;", "Absent or minimal disturbances due to migraine-related non-pain symptoms;" and "No meaningful drug-related adverse events."
  - [S-012] same section, the paragraph beginning "This definition is not specific for triptans", sixth and seventh sentences (not yet quoted): "However, the Panel recognized that less common symptoms (e.g. cognitive disturbance) may also have a relevant impact on single individuals. Hence, a broader definition of “non-pain symptoms” was preferred over a precise description of symptoms."
  - Optional corroboration, already-cited source: [S-021] https://www.ema.europa.eu/en/documents/scientific-guideline/guideline-clinical-investigation-medicinal-products-treatment-migraine_en.pdf, section "Acute migraine attack trials", p. 5 (the sentence directly before the duration sentence quoted in the OUT-011 Caveat): "In general the maintenance of the effect, relapses and effects on migraine-associated symptoms other than pain (e.g. nausea, vomiting, photophobia, phonophobia) at short-term are considered as important secondary endpoints."
  - Optional corroboration, new source (Italian expert Delphi, 17 panellists, medical writing funded by Pfizer Italy): Barbanti P, Tassorelli C, Vernieri F, et al. Building bridges in migraine management: consensus pathways on best practices across primary and specialist care in Italy. Neurol Sci 2026;47(6):500. doi 10.1007/s10072-026-09088-z; PMID 42151647; https://pmc.ncbi.nlm.nih.gov/articles/PMC13183690/ (Table 1, Area 2, statement 21, 100.0% agreement): "Acute treatment is considered effective and should be continued if the subject, within 2 h of drug administration and for at least 24 h, reports all of the following conditions: 1) reduction of migraine intensity from moderate/severe to mild/absent in the majority of attacks (2 out of 3); 2) absence or minimal presence of associated non-painful symptoms; 3) absence of adverse events". If cited, quote it without the numeric criterion (for example with "[...]" in place of item 1), and add it to section 5 and to the Italian search-log row.
- **Earlier history of this item.**
  - OUT-023 changed in v01 (R01-09, R01-11), v02 (R02-01), v08 (R08-01), v14 (sweep) and v17 (R17b-01); OUT-024 in v12, v13, v14 and v17.
  - R08-01 (review-iter-08.md) and the R08-01 row of fix-iter-08.md stated that element B "is covered through OUT-012 and the most-bothersome-symptom element". That assessment holds for the 2-hour status of the named symptoms only; neither text considered the 24-hour maintenance that R08-01 itself listed for A, or the breadth of "non-pain symptoms". No remark on B was raised or declined.
  - This remark only adds an element (or a caveat); it removes or reverses nothing added in v01, v02, v08, v14 or v17, so the watch-list conditions of the oscillation check after iteration 16 still hold. Neither item is frozen.
- **Required change.** Choose one.
  - **(a) Add the element (preferred).**
    1. **OUT-023 Statement.** In the SHOULD sentence that begins "To allow the EHF definition of effective attack treatment [S-012] to be applied", add, for the same attacks, whether migraine-related non-pain symptoms were absent or minimal at 2 hours and whether that status was maintained to 24 hours, named as the non-pain-symptom component of the EHF definition [S-012]. Name the component; do not restate the definition or the 3-of-4 criterion as a rule, and describe only what the output shows, not how symptoms are recorded (PROCESS.md section 2). A cross-reference to OUT-012 is fine, but the 24-hour status and the broader symptom set must be stated in OUT-023 or OUT-012.
    2. **Evidence.** Add the S-012 sentences 6–7 above with their location; the definition is already quoted. The S-021 and Italian quotes are optional.
    3. **Rationale.** One clause: the EHF definition requires the non-pain-symptom status, like the headache status, to be reached within 2 h and kept for at least 24 h, and its non-pain symptoms are broader than the most bothersome symptom.
    4. **Evidence basis.** Name the support: consensus (EHF 2022 [S-012], no recommendation grade); optionally regulatory guidance (EMA 2007 [S-021]) and the Italian Delphi. The strength stays SHOULD.
    5. OUT-024 needs no change under this option.
  - **(b) Qualify the claims.** If the fixer judges the support insufficient for a new element, add a Caveat to OUT-023, with the S-012 sentences above, stating that the outputs show non-pain symptoms only at 2 hours and only for the symptoms named in OUT-012 and the most bothersome symptom, so the EHF definition of effective attack treatment, and with it the EHF triptan-responder and triptan-refractoriness categories, can be applied only in part. Reword the purpose clauses of OUT-023 ("so that the EHF definitions ... can be applied", "To allow the EHF definition ... to be applied") and OUT-024 ("and the EHF definition of triptan refractoriness [S-012] can be applied") so that they do not claim full applicability.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
