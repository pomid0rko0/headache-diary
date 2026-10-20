# Review — iteration 16, re-check c
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v15
Date: 2026-10-20

## Summary
I downloaded all 55 URLs (the 46 section-5 sources, the English SFEMC Parts 1 and 2, the IHS listing page, the BASH contents page, the Swedish Kela page, the SEN and FDA landing pages and two PubMed abstracts) with curl into a new folder of my own. I did not use files that earlier agents left in the shared scratchpad. All returned HTTP 200 on the first attempt. The 11 PMC sources were read in the Europe PMC fullTextXML.

All 295 quoted strings in section 3 are verbatim at their URLs:
- 280 matched by script;
- 15 were confirmed by hand: the S-022 margin line numbers, the ICHD-3 8.2.2 note, two line-break hyphens, AAN 15B, Japan CQ II-2-14, and the SFEMC Rd5 and RT25 rows on the embedded figure images.

Every stated page and JATS path, the grades, all 37 PMIDs, the section-5 strings, the totals and the cross-references are correct. I read every quote in its source context, with about 350 characters on each side. That reading found one defect that script checks cannot find.

OUT-037 cites the IHS tension-type headache trial guideline (S-006) as support for "SHOULD NOT present a composite headache index … as a primary measure". But the section it quotes from recommends that such an index, the area under the headache curve (AUC), which S-006 itself calls a "headache index", *can be* the primary efficacy measure. The requirement does not state this conflict (R16c-01). My searches in Indonesian, Vietnamese, Hungarian, Korean and Italian, and PubMed for 2025–2026, found no missing output requirement and no superseding edition.

## Verification coverage
"Quotes checked" counts quoted strings in section 3 outside the location parentheses (evidence and caveat quotes, list items and grade labels), once per citation. "Manual" means confirmed in the `-layout` text, on a page render or on the embedded figure image. The 164 strings quoted inside locations were checked separately (see below).

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 24 | 24 (1 manual: 8.2.2 note 1, `-layout` text of p. 123). PDF page = printed page. A1.1 notes 3 (p. 190) and the "expert opinion" sentence (p. 123) behind the caveats confirmed. | 0 | — |
| S-002 | 26 | 26 (printed = PDF + 1025) | 0 | — |
| S-003 | 6 | 6 (printed = PDF + 814) | 0 | — |
| S-004 | 10 | 10 (JATS 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5, recommendation and comment paragraphs) | 0 | Europe PMC fullTextXML |
| S-005 | 9 | 9 (1 manual: "meta-analyses" hyphenated at a line end; printed = PDF + 802) | 0 | — |
| S-006 | 5 | 5 (p. 10; the context of the 2.3.3.2 quote is the subject of R16c-01) | 0 | — |
| S-007 | 8 | 8 (accepted manuscript v. 3.2, April 2022; pp. 20, 21, 22, 25) | 0 | — |
| S-008 | 11 | 11 | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | 0 | — |
| S-010 | 8 | 8 (2 manual: "patient-reported" split at a line end, PDF p. 7; abstract quotes in the efetch abstract) | 0 | E-utilities efetch for the abstract |
| S-011 | 3 | 3 | 0 | Europe PMC fullTextXML |
| S-012 | 10 | 10 | 0 | Europe PMC fullTextXML |
| S-013 | 10 | 10 (Results ¶4; "Drug failure" ¶1–4, "Assessment of patients" ¶3, "Debilitating headache" ¶1 and ¶3, "Cut-offs values" ¶1) | 0 | Europe PMC fullTextXML |
| S-014 | 14 | 14 (all JATS paths as stated, including the three v15 "Introduction" locations) | 0 | Europe PMC fullTextXML |
| S-015 | 13 | 13 (1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37, 1.3.48 as `H5`/`H6` headings; 1.3.28 and 1.3.29 tagged [2025]) | 0 | — |
| S-016 | 11 | 11 (PDF = printed + 6; "First published February 2018 / Revised May 2026"; "R" marker before the section 5 recommendation) | 0 | — |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026" and dateModified 2026-09-14 on both section pages; contents page "V1.0 2019") | 0 | — |
| S-018 | 15 | 15 (1 manual: 15B interrupted by "Level C") | 0 | — |
| S-019 | 3 | 3 (p. 3) | 0 | — |
| S-020 | 5 | 5 (printed = PDF − 3) | 0 | — |
| S-021 | 4 | 4 (24 January 2007; in effect 31 July 2007) | 0 | — |
| S-022 | 6 | 6 (all manual: margin numbers stripped; lines 383–384, 393–394, 421–425, 427–429, 464–465; pp. 11–13; consultation 10 Sep 2026 – 31 Jan 2027) | 0 | — |
| S-023 | 4 | 4 ("Hintergrund" ¶5 and ¶8; "Frage 3" final paragraph) | 0 | Europe PMC fullTextXML |
| S-024 | 15 | 15 (1 manual: Rd5 and "Fort" on the 2006 × 1337 px Figure 3; English Part 1 section 2.2 and Table 3 strings on pp. 726 and 731) | 0 | — |
| S-025 | 5 | 5 (2 manual: RT25, cited twice, on the 1864 × 2452 px Figure 1 under "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE,", "Fort"; RT15–RT32 "Fort", RT33–RT34 "Modéré") | 0 | — |
| S-026 | 0 (not cited) | — (former strings on 2020 PDF pp. 306 and 127; ISBN on PDF p. 4) | — | — |
| S-027 | 7 | 7 | 0 | — |
| S-028 | 1 | 1 | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19; "3. udgave", 2020) | 0 | — |
| S-031 | 11 (incl. 2 grade labels) | 11 (1 manual: CQ II-2-14 across the side tab, PDF p. 207; grades A and B; printed = PDF − 16) | 0 | — |
| S-032 | 5 | 5 | 0 | — |
| S-033 | 5 | 5 (grade C/5 after 2.5 and 7.1; title page) | 0 | — |
| S-034 | 3 | 3 (grade C/5 after 7.1; cover page read on a render) | 0 | — |
| S-035 | 5 | 5 (PDF pp. 48, 78) | 0 | — |
| S-036 | 2 | 2 (PDF p. 16; Supplement 1, Volume 21, May 2021) | 0 | — |
| S-037 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-038 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | Europe PMC fullTextXML |
| S-042 | 3 | 3 (Table 2 row Question 6; Results ¶23) | 0 | Europe PMC fullTextXML |
| S-043 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-044 | 1 | 1 | 0 | E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113, 395) | 0 | — |
| S-046 | 3 | 3 (printed = PDF − 3; "Draft", June 2023, docket on the landing page) | 0 | — |
| **Total** | **295** | **295** (280 script, 15 manual) | **0** | — |

Other checks:
- **Locations and pages.** 171 page-located quotes were compared by script with their stated page under each source's page convention: no mismatch. Every Europe PMC quote's JATS path matches its stated location.
- **Headings and labels inside locations.** 164 strings: 149 matched by script. The others are authored labels (for example "NICE CG150 rec. 1.3.28"), figure text read on the images, or English Part 1 strings matched in the IHS copy.
- **Section 5.** Every source-language string matches. These were confirmed: the SFEMC English grading text, Tables 3 and 6, the S-028, S-032 and S-036 grading sentences, the S-045 edition, methodology and landing-page strings, the S-046 draft labels, and the Kela, AIFA and BASH titles.
- **Metadata.** All 37 PMIDs (esummary) match authors, journals, volumes, pages, DOIs and PMCIDs.
- **Translations and omissions.** I read every quote with the source text before and after it. Every "[...]" and every cut at the start or end leaves out only recording, calculation, cross-reference or age-limit text, and the translations are faithful.
- **Totals and IDs.** 39 requirements (10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT); 46 source rows, 45 cited; 276 quote citations (267 evidence items and 9 caveat quotes), as the v15 change log states; no dangling OUT reference.

Checked and not raised:
- **OUT-034, NICE 1.3.1.** NICE 1.2.6 points to "recommendation 1.1.4" for the headache diary. Both 1.1.3/1.1.4 (diagnostic diary) and 1.3.1 (diary for monitoring and discussion) exist, and the quoted wording is 1.3.1's. Correct.
- **OUT-021, the [S-016] section 4.1 sentence on when to start prophylaxis.** It concerns the start decision, not efficacy review, but it supports judging migraine by its impact rather than by counts alone. No change required.
- **OUT-010, "average peak intensity".** S-006 2.3.3.3 states that pain ratings "are typically treated as approximate interval scales for analysis". No conflict.
- **Section 3 preamble.** The RFC 2119 list omits MUST NOT, which OUT-016 uses. The list is not stated to be exhaustive, and OUT-016's Strength line covers the clause. Not raised.
- **IHS paediatric update 2023 (PMID 37226450).** Unreachable:
  - SAGE PDF and full text: 403 to curl and to WebFetch.
  - OpenAlex lists only the SAGE copy.
  - Europe PMC: not open access.
  - The IHS guidelines page links only the 1st edition.
  - This matches the S-005 note.
- **PMID 41839119 (2026).** It is an American Family Physician summary of the IHS 2024 acute recommendations (S-009), not a new guideline.
- **Newer editions.** PubMed 2025–2026 shows no new EHF or IHS edition of S-002 to S-014, and no tension-type headache trial guideline after S-006 (2010).
- **Completeness searches with no new output requirement:**
  - Indonesian (PERDOSSI): no guideline text found.
  - Vietnamese (Bộ Y tế): no national migraine guideline found.
  - Hungarian: the 2025 CGRP guideline, already reviewed in iteration 05.
  - Korean: press reports only.
  - Italian (SISC): press reports only.

## Remarks
### R16c-01 [unsupported/overstated] — target: OUT-037 (Rationale, Evidence basis, Evidence; possibly Statement scope)
- **Problem.** OUT-037 says "The diary output SHOULD NOT present a composite headache index that multiplies or otherwise combines frequency, intensity and/or duration into one score as a primary measure", and that such an index "SHOULD be labelled as exploratory". Its Evidence basis lists "international trial-methodology guideline (IHS TTH 2010)" as support. Its Rationale says "Regulatory guidance and IHS methodology warn that composite indices …".
  - The only S-006 quote is "[...] when used in headache indices, faulty weighting in the arbitrary numerical intensity score will be increased by multiplication." It is taken from the comments to recommendation 2.3.3.2 "Area-under-the-headache curve".
  - That recommendation states the opposite of what OUT-037 cites it for: AUC, which the same comments describe as "(also called headache index)", can be the primary efficacy measure.
  - The comments add that AUC "seems to be more sensitive than days with headache for trials in CTTH" and that there are "no conclusive data" on whether days with TTH or AUC should be preferred.
  - Read in context, the quoted sentence is a caveat attached to a recommendation that *permits* an index as the primary measure. It does not support "SHOULD NOT … as a primary measure" or "labelled as exploratory".
  - The two EMA sources that do support the SHOULD NOT (S-021, S-022) are guidelines for migraine (and, for S-022, cluster headache) trials. The document's outputs also cover tension-type headache (OUT-029). For tension-type headache, the only international methodology guideline cited endorses the index as a possible primary measure.
  - The Evidence basis does not state that the evidence conflicts, contrary to PROCESS.md section 3 ("Say so when the evidence is weak or conflicting"). It also lists S-006 as support, which misstates the source's position.
- **Evidence.** All verified on 2026-10-20 at https://ihs-headache.org/wp-content/uploads/2020/05/156_clinical-trials-tension-type-headache-guidelines-cha.pdf (S-006, section 2.3.3.2, p. 10, in the text layer and on a 150-dpi render; the text layer displaces the word "curve" from the justified line, and the render reads as quoted):
  - Recommendation: "Recommendations: Area-under-the-headache curve (AUC) can be the primary efficacy measure."
  - Comments: "(also called headache index)"
  - Comments: "AUC seems to be more sensitive than days with headache for trials in CTTH (38, 39)."
  - Comments, directly after the sentence OUT-037 quotes: "When AUC is used as the primary efficacy measure, days with headache should be presented as a secondary efficacy measure. At present there are no conclusive data indicating whether days with TTH or AUC should be preferred as the primary efficacy measure in CTTH."
  - Optional support for the migraine side, in an international methodology guideline already cited: [S-002] "If composite endpoints are used, each of the components must be clinically relevant and sufficient to establish treatment benefit, as success of the composite may be determined by results of any component. Composite endpoints are problematic when response for a component is inconsistent or when findings for the composite endpoints move in different directions (some positive, others negative)." (section 1.3, comments before 1.3.1, p. 1035, https://ihs-headache.org/wp-content/uploads/2025/04/Clinical-Trials-Controlled-trials-of-preventive-treatment-of-migraine-attacks-in-episodic-migraine-in-adults-CEP.pdf).
- **Earlier history of this item.**
  - OUT-037 is unchanged since v00. The oscillation check after iteration 12 lists it as unchanged.
  - Fix-iter-14 checked only its "shown together with its component measures" element against S-022 and left it unchanged.
  - No earlier remark or fix mentions AUC or the S-006 2.3.3.2 recommendation, so this remark reverses no earlier change. OUT-037 is not frozen.
- **Required change.**
  1. **Evidence basis.** Stop presenting the IHS TTH guideline as support for the SHOULD NOT. State that the evidence is conflicting:
     - EMA 2007 (in force) and the EMA 2026 draft, both migraine guidelines, advise against headache indices or treat them as exploratory unless validated;
     - the IHS TTH guideline (S-006, 2.3.3.2) recommends that AUC can be the primary efficacy measure in CTTH trials, while warning of faulty weighting and asking for days with headache to be presented as a secondary measure.
  2. **Caveats.** Add the S-006 2.3.3.2 recommendation sentence above, verbatim with its location, as conflicting evidence, in the way OUT-011, OUT-023 and OUT-026 record theirs.
  3. **Rationale.** Correct "Regulatory guidance and IHS methodology warn that …". It should say that the IHS TTH guideline warns only of faulty weighting by multiplication, and that it nonetheless allows AUC as a primary efficacy measure.
  4. **Strength and scope.** Decide on the evidence, and record the reason, whether to:
     - keep SHOULD NOT and "labelled as exploratory" for all outputs, with the conflict stated; or
     - limit them to migraine outputs (where the EMA support applies, optionally with the S-002 composite-endpoint quote) and say how a tension-type headache index is to be shown, for example together with headache days, as S-006 asks.

     The S-006 quote may stay in Evidence only if its role is stated accurately.
  5. **Scope rule.** Do not restate how AUC is calculated (PROCESS.md section 2).

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
