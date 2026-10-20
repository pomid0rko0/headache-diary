# Review — iteration 19, re-check b
VERDICT: NO_REMARKS
REMARK_COUNT: 0
Reviewed version: v18
Date: 2026-10-20

## Summary
I downloaded all 46 section-5 sources again with curl into a new, empty scratch folder of my own (`scratchpad/r19b/src`) and did not use files left by earlier agents. I also downloaded the English SFEMC Parts 1 and 2, the BASH contents page, the Swedish Kela page, the SEN and FDA landing pages, the PubMed records (E-utilities) and the Europe PMC fullTextXML of every PMC source. All 310 quoted strings on the Evidence and Caveats lines are verbatim at their URLs: 297 matched by script and 13 by hand, on page renders, in the `-layout` text or after removing printed margin line numbers. All 153 strings quoted inside locations are correct, and every stated page, line range, paragraph and sentence position I checked is right. I read all 267 distinct quotes in their source context, with the whole section where a quote's role mattered, and checked each Statement clause by clause against them. I found no misquote, no wrong citation metadata, no unsupported or mis-graded element, no scope violation, no contradiction and no definition that the outputs claim to let a reader apply but do not cover. My completeness searches (Swedish Läkemedelsboken, Korean, Thai, Vietnamese, Indonesian, Malaysian, Greek, Austrian, Taiwanese, PubMed 2025–2026 and core outcome sets) found no evidence-based output requirement that the document misses and no edition that supersedes a cited source.

## Verification coverage
"Quotes checked" counts the quoted strings on the Evidence and Caveats lines of section 3 once per citation: quotes, list items and the four grade labels, 310 in all. "Read in context" means that I printed each distinct quote with at least 450 characters on each side in the downloaded text and checked it against the clause it supports. Where a quote's role or a definition was at issue, I read the whole section: S-012 Background, Results > Consensus and Discussion; S-013 Results after Table 3 and the whole Discussion; S-006 section 2.3.3; S-008 Q2, Q4, Q6 and Q7; S-010 pp. 3, 6 and 7; S-021 pp. 4–6 and the Annex; S-022 sections 5.2.2–5.2.5; S-031 CQ I-10, CQ II-2-14 and CQ VI-3; S-045 PDF pp. 111–113 and 393–395. Page numbers were checked by script against the page where each quote was found, using the page conventions in section 5, and by hand for the rest.

| Source ID | Quotes checked | Verified verbatim | Read in context (yes/no) | Not found | Unreachable (what you tried) |
|---|---|---|---|---|---|
| S-001 | 24 | 24 (1 by hand: 8.2.2 note 1 in the right column of the p. 123 `-layout` text; render made). PDF page = printed page | yes | 0 | — |
| S-002 | 26 | 26 (printed = PDF + 1025) | yes | 0 | — |
| S-003 | 6 | 6 (printed = PDF + 814) | yes | 0 | — |
| S-004 | 10 | 10 (Europe PMC fullTextXML) | yes | 0 | — |
| S-005 | 9 | 9 (printed = PDF + 802) | yes | 0 | — |
| S-006 | 9 | 9 (1 by hand: the 2.3.3.2 recommendation, read on a 150-dpi render of p. 10) | yes | 0 | — |
| S-007 | 8 | 8 (accepted manuscript, printed page = PDF page) | yes | 0 | — |
| S-008 | 14 | 14 (Q6 list on p. 12 reads "person with migraine"; the p. 6 summary table reads "subject") | yes | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | yes | 0 | — |
| S-010 | 9 | 9 (abstract quotes also in the efetch abstract; pp. 3, 6, 7) | yes | 0 | — |
| S-011 | 3 | 3 | yes | 0 | — |
| S-012 | 15 | 15 (all sentence and paragraph positions recounted) | yes (Background, Results > Consensus, Discussion in full) | 0 | — |
| S-013 | 13 | 13 (Table 3 + 3 paragraphs; "Drug failure" ¶2–¶5; "Assessment of patients" ¶3; "Debilitating headache" ¶1) | yes (Discussion in full) | 0 | — |
| S-014 | 14 | 14 | yes | 0 | — |
| S-015 | 13 | 13 ("19 September 2012", "03 June 2025") | yes | 0 | — |
| S-016 | 11 | 11 (PDF = printed + 6; "R" markers on PDF pp. 12 and 37; "Revised May 2026") | yes | 0 | — |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026" on both section pages, dateModified 2026-09-14; contents page "V1.0 2019") | yes | 0 | — |
| S-018 | 15 | 15 (1 by hand: 15B, interrupted by "Level C"; levels of 12A, 14A–14F, 15A–15D read on renders of pp. 7–8) | yes | 0 | — (aan.com redirects to the AAN blob-storage PDF dated 2026-08-31) |
| S-019 | 3 | 3 (p. 3) | yes | 0 | — |
| S-020 | 5 | 5 (printed = PDF − 3) | yes | 0 | — |
| S-021 | 5 | 5 (24 January 2007; in effect 31 July 2007; Annex title in capitals on p. 11) | yes | 0 | — (HTTP 301 to the ...revision-1_en.pdf copy of the same 12-page guideline) |
| S-022 | 6 | 6 (by script after removing margin line numbers; lines 383–384, 393–394, 421–425, 427–429, 464–465 in the `-layout` text) | yes | 0 | — |
| S-023 | 4 | 4 | yes | 0 | — |
| S-024 | 13 | 13 (1 by hand: Rd5 and "Fort" on the render of PDF p. 8 = printed p. 402; English Part 1 grading text p. 726 and Table 3 Rd5 "Strong" on a render of p. 731) | yes | 0 | — |
| S-025 | 5 | 5 (2 by hand: RT25, cited twice, with "Fort" on the render of PDF p. 3 = printed p. 414; English Table 6 Rt25 "Strong" on a render of p. 743) | yes | 0 | — |
| S-026 | 0 (not cited) | — (URL returns HTTP 200) | — | — | — |
| S-027 | 7 | 7 (Publicatiedatum 04-12-2023) | yes | 0 | — |
| S-028 | 1 | 1 (11-01-2018; GRADE sentence present) | yes | 0 | — |
| S-029 | 2 | 2 (04-12-2023) | yes | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19) | yes | 0 | — (http redirects to https) |
| S-031 | 11 | 11 (1 by hand: CQ II-2-14 across the side tab, PDF p. 207 = printed p. 191, grade A; printed = PDF − 16) | yes | 0 | — |
| S-032 | 5 | 5 (section-5 GRADE sentences and IPGRP2022CN297 also present) | yes | 0 | Connection reset on the first attempt; the retry redirected to https://www.brainmed.com/info/detail?id=34408, same text |
| S-033 | 5 | 5 (cover rendered: "взрослые", "Год утверждения: 2024") | yes | 0 | Connection reset on the first attempt; the retry succeeded |
| S-034 | 3 | 3 (cover rendered: "дети", 2024) | yes | 0 | — |
| S-035 | 5 | 5 (PDF pp. 48, 78) | yes | 0 | — |
| S-036 | 2 | 2 (PDF p. 16; no grade attached; DOI present) | yes | 0 | — |
| S-037 | 1 | 1 (heading printed in capitals) | yes | 0 | — |
| S-038 | 1 | 1 | yes | 0 | — |
| S-039 | 2 | 2 (page title "3007 Atogepantti, eptinetsumabi, …") | yes | 0 | — |
| S-040 | 2 | 2 ("G.U. 93 del 22/04/2025") | yes | 0 | — |
| S-041 | 1 | 1 (Conclusion) | yes | 0 | — |
| S-042 | 3 | 3 | yes | 0 | — |
| S-043 | 1 | 1 | yes | 0 | — |
| S-044 | 1 | 1 (efetch abstract) | yes | 0 | — |
| S-045 | 4 | 4 (PDF pp. 113, 395; printed = PDF − 2; 612 pages; ISBNs; Tabla 3 on PDF p. 17; landing page "21 de enero de 2026") | yes | 0 | — |
| S-046 | 3 | 3 (printed = PDF − 3; landing page "Draft", June 2023, FDA-2022-D-1729) | yes | 0 | — |
| **Total** | **310** | **310** (297 by script, 13 by hand) | **all 267 distinct quoted strings** | **0** | none unreachable |

### Other checks
- **Locations.** 153 strings quoted inside locations: 148 matched by script; the other 5 (the S-021 Annex title and S-037 heading in capitals, and three S-024/S-025 figure headings) I read in the capitals text or on the figure images.
- **Translations and omissions.** I read all 70 translations against their originals (Dutch, Danish, German, French, Spanish, Portuguese, Italian, Finnish, Russian, Turkish, Chinese, Japanese) and found all faithful, including the bracketed subjects in S-033 2.5 and S-032 3.2. I read the source text behind every "[...]" and every quote cut at its start or end. Each omission removes recording or calculation detail, age limits, other list items, references, timing of evaluation (RT25) or a back-reference, and none changes the meaning. The S-033 guillemets «…» are as printed.
- **Grades and types.** These match the sources:
  - AAN levels: 12A, 14A–14F, 15A, 15B (C), 15C (A) and 15D;
  - Japan CQ I-10 (B) and CQ II-2-14 (A);
  - Russian grades C/5 after sections 2.5 and 7.1 (adult) and 7.1 (paediatric);
  - SFEMC "Fort"/"Strong" for Rd5 and RT25, and the English abstract wording "we suggest" (PMID 34340812);
  - SIGN "R" on PDF pp. 12 and 37;
  - the ICHD-3 statements used in unquoted caveats: "based on expert opinion rather than on formal evidence" (p. 123) and "not mandatory for clinical diagnosis" (A1.1 note 3, p. 190).
- **Metadata.** esummary for all 37 PMIDs in section 5 and the search log matches authors, journals, years, volumes, issues, pages, DOIs and PMCIDs. The S-024 and S-025 DOIs, page ranges and author strings ("E. Donnet") match the PDFs. The correction to S-043 (PMID 42210057) only adds a competing-interest sentence.
- **Totals and IDs.** By the stated rule: 39 requirements, 10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT. There are 46 source rows, 45 of them cited (all but S-026). No ID is duplicated and no OUT reference dangles. Every [S-NNN] tag in a Statement, Rationale or Evidence basis has a quote in the same requirement, and no RFC 2119 term occurs before "Strength:".
  - history/v18.md is byte-identical to OUTPUT_REQUIREMENTS.md.
  - A word diff of v17 and v18 deletes only "v17", "17", "OUT-019).", "2018);" and "v17).", as the v18 change log says.
  - FROZEN_ITEMS.md does not exist.
- **Scope.** I read every Statement, Rationale, Evidence basis and Caveat and also scanned the authored text, with quotes removed, for input, storage and derivation terms. I found nothing beyond the unit and statistic examples accepted in earlier iterations ("proportion of days", "average peak intensity", "median attack duration").
- **Definition coverage.** I re-derived from the sources the elements of every definition or criterion that a requirement says its outputs let a reader apply, relate to or label. All are covered or properly qualified:
  - the EHF effective-treatment, triptan-responder and triptan-refractoriness definitions (OUT-023, OUT-024);
  - ICHD-3 8.2, its subtypes and the 8.2.6 total across classes (OUT-014, OUT-016);
  - ICHD-3 1.3 and 2.3 ("relate the pattern to"; OUT-028);
  - ICHD-3 A1.1 window and cycles (OUT-030);
  - ICHD-3 cluster period and remission (OUT-031, qualified);
  - the named responder criteria (OUT-020);
  - the EHF resistant and refractory categories and NICE 1.3.24 (OUT-024, qualified);
  - the scheme windows (OUT-025).

### Checked and not raised
- **Quantity of acute medication (doses rather than days).** Three cited sources name drug consumption as an outcome:
  - S-002 1.3.2.2.1 (recording "the number and dose of drugs");
  - S-006 2.3.3.5 ("Drug consumption can be used as a secondary efficacy measure", supplemented "by a count of dosage units");
  - S-021 ("Drug consumption for acute treatment totalled over an evaluation period", one possible secondary endpoint).

  OUT-014 reports days only. Not raised, because the evidence is weak and conflicting:
  - S-006 itself calls the measure "dubious in between-patient comparisons" and says "There is no satisfactory way of quantifying the consumption";
  - S-003, S-005, the FDA guidance (S-046) and the ICHD-3 8.2 criteria are day-based, and S-022 names only "Acute migraine medication use";
  - the clinical guidance cited states the risk in terms of frequency ("Frequency, regularity and duration of intake are important determinants of risk", S-014);
  - no clinical practice source asks a diary output to show dose counts.

  Review 18 reached the same conclusion for the Polish 2021 recommendations.
- **Japan CQ VI-3 recommendation box (PDF p. 369, printed p. 353).** The 推奨 text itself says that after withdrawal the frequency of use of triptans, ergotamine and analgesics should be checked with a headache diary, graded "弱い推奨/エビデンスの確実性 B". OUT-017 quotes the commentary on p. 355 and lists Japan without a grade. That is not false, and a weak recommendation would not change OUT-017 (SHOULD). Citing the box would be optional.
- **Sweden: Läkemedelsboken, chapter "Migrän och annan huvudvärk"** (Läkemedelsverket; published and last updated 27 October 2025; https://lakemedelsboken.se/terapiomraden/nervsystemets-sjukdomar/migran-och-annan-huvudvark/migran/lakemedel-vid-migran/). It is not in the search log. Its diary statements support OUT-007, OUT-010 and OUT-018 and add no output:
  - "Migrändagbok är ett viktigt hjälpmedel för att utvärdera den profylaktiska läkemedelsbehandlingens effekt. Målet är att minska anfallsintensitet och frekvens med minst en tredjedel. Utvärdera effekten efter 3 månader.";
  - "Migrändagbok och en skala för intensitetsskattning är värdefulla hjälpmedel …".

  It carries no grade. The Swedish row's "no Läkemedelsverket migraine recommendation found" records the author's search, and Läkemedelsboken is a reference text rather than a treatment recommendation, so I do not treat the row as a factual error or the language as a gap.
- **COSMIG core outcome set** (BMJ Open 2021; PMC8634270; not in the document). Its two core domains are migraine-specific pain (headache or migraine days, and intensity on an 11-point NRS) and migraine-specific quality of life (MFIQ). Both are covered by OUT-004/OUT-005, OUT-010 and OUT-026 (any validated instrument). It would only add optional direct support for the scale element of OUT-010, which the Evidence basis already describes accurately as indirectly supported.
- **New 2025–2026 items found in PubMed.**
  - The 2026 Taiwan acute-treatment guidelines (J Chin Med Assoc, PMID 42723131) are closed access (Ovid), and the abstract has no diary statement.
  - The Brazilian MOH position statement (PMC12886480) is a survey whose diary mentions are instructions.
  - The Brazilian anti-CGRP position statement (PMC13552630) has no diary statement.
  - The Japanese Headache Society CGRP position statement (27 October 2025, jhsnet.net) repeats the 3-month evaluation already covered by OUT-018 and OUT-025.
  - None changes a requirement.
- **PGIC in OUT-026.** "The change from the baseline administration" has no meaning for a change scale such as PGIC. Read with "Where results … are available", this is not a defect.
- **No reachable copy.** I tried these and could not reach them:
  - IHS paediatric update 2023 (PMID 37226450): SAGE Cloudflare 403; OpenAlex and Semantic Scholar list only the SAGE copy; not in Europe PMC.
  - AWMF S1 030-057 (2025-11) and the TUM repository copy: Anubis challenge pages, which I did not try to bypass. The Tübingen records 10900/146941–146942 are S-023, not the guideline.

  The S-005 entry and the search log already record these gaps.
- **Other completeness searches with no quotable output requirement:** Korean (press reports only), Thai, Vietnamese, Indonesian (PERDOSSI), Malaysian, Greek, Austrian (ÖKSG) and Japanese (all 32 diary passages in S-031 add nothing beyond the cited requirements).

## Remarks
None.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
