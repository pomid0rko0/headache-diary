# Review — iteration 12
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v11
Date: 2026-10-20

## Summary
I downloaded all 46 sources again with curl into a new, empty folder of my own and did not use files left by earlier agents. This includes S-026, the English SFEMC Parts 1 and 2, the IHS listing page, the NICE, BASH, NVN, Kela, AIFA, SEN and FDA pages, the Käypä hoito "Migreeni" page, the Europe PMC full texts and the PubMed records (E-utilities).

A script extracted every quoted string in section 3 and matched it against the downloaded text, segment by segment for "[...]": 220 distinct strings in 242 occurrences, all verbatim. 215 matched by script. I confirmed the other 5 by hand:
- the v11 ICHD-3 8.2.2 note, on a render of p. 123;
- AAN 15B, in the `-layout` text;
- Japan CQ II-2-14, across the side tab;
- SFEMC Rd5 and RT25, on the embedded figure images.

I also checked the following and found them correct: pages, sections, translations, "[...]" omissions, the section-5 strings, PubMed metadata for all 37 PMIDs, the totals, the cross-references and the scope of the authored text.

The v11 changes are accurate:
- **OUT-014.** The five ICHD-3 note quotes and their note numbers and pages are correct. No day criterion is quoted, and the new Evidence-basis sentence matches the source.
- **Finnish search-log row.** Every claim is confirmed in the raw HTML of the Käypä hoito "Migreeni" page.

The two remarks concern Statement elements, present since v00, that have no supporting quote:
- **R12-01.** OUT-024 asks for the treatment history "grouped by drug class", but none of its quotes mentions drug classes.
- **R12-02.** OUT-031 asks for cluster "attacks per day" and the "need for rescue treatment", but none of its quotes mentions either.

Both sources are already cited, and they contain the missing support.

My searches found no missing output requirement and no superseding edition. They covered Korean, Italian, German (Swiss SKG), Norwegian, Czech, Thai, Vietnamese and Latin-American Spanish sources, and PubMed (IHS and EHF 2025–2026).

## Verification coverage
"Script" means the string matched in the downloaded text, ignoring NFKC form, dashes, apostrophes and whitespace; "hyph" means it matched only once line-break hyphens were joined. "Manual" means I confirmed it on a page render, in the `-layout` text or on the embedded figure image.

Counts are distinct quoted strings in section 3: quotes, list items, caveat quotes and grade labels. Section-5 strings and headings are reported below the table.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 20 (5 new in v11) | 20. 19 script; 1 manual: the 8.2.2 note "The triptan(s) will usually be specified in parenthesis.", which the text layer breaks into single words, read on a 150-dpi render of p. 123. 8.2 note 1 (p. 122), 8.2.3.2 note 1, 8.2.4 note 1 and 8.2.5 note 2 (p. 124) are under the stated headings and note numbers. PDF page = printed page. | 0 | — |
| S-002 | 17 (incl. 3 list items) | 17 (1 ws: "moderate/ severe"; PDF page + 1025) | 0 | — |
| S-003 | 2 | 2 (PDF page + 814) | 0 | — |
| S-004 | 7 | 7 (JATS sections 1.3.2, 1.3.3, 1.3.4.2 and 1.3.4.5) | 0 | PMC serves a challenge page to curl; used the Europe PMC fullTextXML |
| S-005 | 7 | 7 (1 hyph: "meta-analyses"; PDF page + 802) | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 (accepted-manuscript pp. 20, 21 and 25) | 0 | — |
| S-008 | 8 | 8 | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | 0 | — |
| S-010 | 4 | 4 (1 hyph: "patient-reported"). The abstract quotes are also in the efetch abstract. | 0 | PubMed web page not used; E-utilities efetch used |
| S-011 | 3 | 3 | 0 | Europe PMC fullTextXML |
| S-012 | 8 (incl. 3 list items) | 8 | 0 | Europe PMC fullTextXML |
| S-013 | 4 | 4 (Results; Discussion > "Cut-offs values", "Drug failure", "Debilitating headache") | 0 | Europe PMC fullTextXML |
| S-014 | 12 | 12 | 0 | Europe PMC fullTextXML |
| S-015 | 13 (incl. 2 list items) | 13. Numbers 1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37 and 1.3.48 checked against the HTML. "Last updated: 03 June 2025". | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6; "Revised May 2026") | 0 | — |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026" on both section pages; TOC page "V1.0 2019") | 0 | — |
| S-018 | 8 | 8 (1 manual: the margin label "Level C" interrupts 15B on p. 8) | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 (printed p. 4 = PDF p. 7) | 0 | — |
| S-021 | 3 | 3 | 0 | — |
| S-022 | 6 | 6 (margin line numbers stripped; pp. 11–13; front page: EMA/137055/2026 Rev. 2, consultation 10 Sep 2026 – 31 Jan 2027) | 0 | — |
| S-023 | 4 | 4 | 0 | Europe PMC fullTextXML |
| S-024 | 9 | 9 (1 manual: Rd5 on the 2006 × 1337 px Figure 3 image, where Rd1–Rd10 are all "Fort"; PDF page + 394) | 0 | — |
| S-025 | 2 | 2 (1 manual: RT25 first sentence and heading on the 1864 × 2452 px Figure 1 image, where RT15–RT32 are "Fort" and RT33–RT34 "Modéré") | 0 | — |
| S-026 | 0 (not cited) | — | — | Downloaded; superseded entry (ISBN 978-84-18420-19-1 confirmed, PDF p. 4) |
| S-027 | 6 | 6 | 0 | — |
| S-028 | 1 | 1 | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19) | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (6 ws: line breaks inside Japanese sentences; 1 manual: the side tab interrupts CQ II-2-14 on PDF p. 207 = printed p. 191; printed = PDF − 16; ISBN on PDF p. 2) | 0 | — |
| S-032 | 3 | 3 | 0 | The first connection was reset; a retry succeeded |
| S-033 | 5 | 5 (pp. 18, 19, 26 and 53). The two English table titles are faithful renderings of "Таблица 3в" and "Таблица 4а". | 0 | — |
| S-034 | 3 | 3 (pp. 34, 50) | 0 | — |
| S-035 | 3 | 3 (PDF pp. 48, 78) | 0 | — |
| S-036 | 2 | 2 (PDF p. 16) | 0 | — |
| S-037 | 1 | 1 (heading printed "PRINCIPLES OF PROPHYLAXIS") | 0 | Europe PMC fullTextXML |
| S-038 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | Europe PMC fullTextXML |
| S-042 | 2 | 2 | 0 | Europe PMC fullTextXML |
| S-043 | 1 | 1 | 0 | Europe PMC fullTextXML and efetch |
| S-044 | 1 | 1 | 0 | PubMed web page not used; abstract via E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113, 395; printed = PDF − 2) | 0 | — |
| S-046 | 3 | 3 (printed p. 5 = PDF p. 8; margin lines as stated) | 0 | — |
| **Total** | **220** | **220** (206 exact, 7 ws, 2 hyph, 5 manual) | **0** | — |

Other strings checked:
- **Section 5.** There are 79 quoted strings: 9 are the document's own translations, which I checked for faithfulness, and 70 are source strings. 67 of the source strings matched by script, including:
  - the S-024 grading passage and Table 3 strings in the IHS copy of English Part 1;
  - the S-025 methods sentence and Table 6 strings in English Part 2;
  - the SEN 2026 imprint, methodology and landing-page strings;
  - the FDA "Draft" strings;
  - the BASH footers.

  I confirmed 3 by hand: "FORCE" and "FORCE DE LA RECOMMANDATION" on the figure images, and NICE's "do not", which the source prints "Do not".
- **Headings.** 73 headings and labels quoted inside locations or authored text: all occur in their sources, are confirmed on the figure images, or are faithful English renderings of the S-033 Russian table titles.
- **Translations.** All translations of section-3 quotes (66 occurrences) read faithfully. The bracketed subject in the OUT-004 S-033 translation renders the omitted "Ведение дневника ГБ в течение 1 - 3 месяцев до осмотра" ("keeping a headache diary for 1–3 months before the examination") without its duration, which is input content. The meaning is kept.
- **Omissions.** All 12 quotes with "[...]" omit only cross-references, recording or calculation details, or list items. The meaning is unchanged.
- **Metadata.** All 37 PMIDs were checked against PubMed esummary: authors, titles, journals, volumes, pages, DOIs and PMCIDs match section 5 and the search log. I also checked these items on the title pages: S-031 ISBN 978-4-260-04698-5 (PDF p. 2), S-033 "Год утверждения: 2024" and its developers, S-016 "Revised May 2026", and S-021 CPMP/EWP/788/01 Rev. 1.
- **Totals and cross-references.** 39 requirements: 10 MUST, 24 SHOULD, 4 MAY and 1 SHOULD NOT, by the stated rule; no RFC 2119 term occurs before "Strength:". There are 46 source rows, and 45 sources are cited (all except S-026). No ID is duplicated, and every OUT and S reference resolves.
- **v11, Finnish row.** I checked these points in the raw HTML of https://www.kaypahoito.fi/hoi36050:
  - the header "Käypä hoito -suositus | Julkaistu: 28.03.2024 | Tila: päivityksessä";
  - the Duodecim and Suomen Neurologinen yhdistys working group;
  - the headings "Keskeinen sisältö", "Potilasohjaus", "Lääkkeellinen estohoito", "Onabotuliinitoksiini A", "Hoidon seuranta" (an H2) and "Diagnoosi";
  - that none of the blocks mentioning a "päänsärkypäiväkirja" (headache diary) or "kalenteri" (calendar) carries a `duo-evidence` tag;
  - the Kela criteria (weeks 9–12, link to laake3007) in "Erillisselvitys".

  The row is accurate.
- **Scope.** A keyword scan of all unquoted authored text in sections 1–4 and 6, followed by reading every Statement, Rationale and Caveat, found no input, storage or derivation content. The unit and statistic examples ("proportion of days", "average peak intensity", "median attack duration") were accepted in earlier iterations, and I see no new reason to object. The v11 ICHD-3 quotes contain no day criteria.

Searched with no remark:
- **Swiss SKG.** The treatment recommendations on the IHS site (German, © 2019, 10th edition, https://ihs-headache.org/wp-content/uploads/2020/06/3685_swiss-treatment-guidelines-2018-german.pdf) and the 2024 Ars Medici summary. The paediatric sentence "Ein Kopfwehtagebuch – inkl. Zykluskalender bei Adoleszentinnen – ist aus diagnostischen Gründen und zur Therapieüberwachung wichtig." ("A headache diary – including a cycle calendar in adolescent girls – is important for diagnostic reasons and for monitoring therapy") is covered by OUT-030 and OUT-036.
- **Korea.** "The Development of Evidence-Based Guideline for Diagnosis and Management of Headache in Korea" (Psychiatry Investig 2019, PMID 30934187, PMC6444101). It is a methods paper on adapting NICE CG150 and lists diary use only as health questions.
- **Europe.** The EHF/EAN-endorsed "Diagnosis and management of migraine in ten steps" (Nat Rev Neurol 2021, PMC8321897). Its diary and calendar statements (frequency, severity, acute medication use, menstruation, mTOQ-4, HURT) are covered by OUT-004, OUT-005, OUT-010, OUT-014, OUT-026 and OUT-030.
- **Italy.** No SNLG/ISS headache guideline was found.
- **Other languages.** Norwegian, Thai, Vietnamese and Argentine searches found only reviews or news items. PubMed 2025–2026 shows no new IHS global practice recommendations and no new EHF guideline. The AAN/AHS 2026 recommendations 14B, 16B and 17A concern clinician actions that OUT-018, OUT-024 and OUT-022 already reflect; review 05 recorded the same.
- **Unreachable:**
  - AWMF 030-057 (2025-11): bot-check page ("Making sure you're not a bot!").
  - csnn.eu Czech CGRP criteria: declaration page.
  - IHS paediatric update 2023 (PMID 37226450): OpenAlex lists SAGE as an open copy, but SAGE returned HTTP 403 to curl and to WebFetch, and Europe PMC has no full text. This matches the S-005 note and the search log.

## Remarks

### R12-01 [unsupported/overstated] — target: OUT-024 (Statement clause "grouped by drug class"; Rationale; Evidence)
- **Problem.** The OUT-024 Statement requires the treatment history to be "grouped by drug class". The Rationale justifies this with "The number and classes of failed preventives determine eligibility for later treatments and for the EHF categories of resistant and refractory migraine". None of the four quotes in OUT-024 mentions drug classes:
  - [S-013] "Establishing drug failure or contraindication is pivotal to identifying resistant or refractory migraine."
  - [S-015] 1.3.24 counts "at least 3 preventive medicines", not classes.
  - [S-002] concerns adverse events.
  - [S-019] concerns a list of medicines tried.

  The grouping element and the "classes" claim in the Rationale therefore have no quoted support. PROCESS.md section 3 requires a verbatim quote for every citation, and earlier iterations treated an unquoted Statement element as a remark: R01-09 (the 15-minute time point) and R11b-01 (the per-drug clause). The support exists in S-013, which OUT-024 already cites, in the same subsection as the quote it already uses.
- **Evidence.** Verified verbatim in the Europe PMC fullTextXML of PMC7296705 (https://pmc.ncbi.nlm.nih.gov/articles/PMC7296705/), section Discussion > "Drug failure":
  - In the paragraph directly after the one beginning "Establishing drug failure or contraindication is pivotal", first sentence: "One of the main criteria to define resistance and refractoriness to treatment is the number of failed classes of medications."
  - The same paragraph, third sentence: "The Consensus group agreed to select failure of drug classes, rather than single medications, since a patient who fails a drug has a very low probability of responding to another drug within the same class based on expert opinion."
  - Do not quote the Results definition "Resistant migraine is defined by having failed at least 3 classes of migraine preventatives and suffer from at least 8 debilitating headache days per month ...". It carries numeric day criteria, which PROCESS.md section 2 excludes.
- **Earlier history of this item.** None. OUT-024 is byte-identical in all 12 snapshots, v00–v11, and no review or fix has raised the grouping element. Reviews 03, 05, 07 and 11 mentioned OUT-024 only as covering adverse effects or efficacy.
- **Required change.** Choose one:
  - **(a)** Add the first S-013 sentence above to OUT-024's Evidence, and optionally the second, which should be labelled expert opinion. Locate the first as (Discussion, "Drug failure", first sentence of the paragraph following the one quoted above). No change to the Statement, Evidence basis (which already lists "consensus (EHF 2020)") or strength (SHOULD) is needed.
  - **(b)** Remove "grouped by drug class" from the Statement and "and classes" from the Rationale.

### R12-02 [unsupported/overstated] — target: OUT-031 (Statement elements "attacks per day" and "the need for rescue treatment"; Evidence)
- **Problem.** The OUT-031 Statement requires "attacks per day and per week during active periods" and, for acute treatments, "effectiveness at 15 minutes and the need for rescue treatment (see OUT-023)". None of the six quotes in OUT-031 mentions attacks per day or rescue treatment:
  - [S-001] defines a cluster period;
  - [S-007] gives weekly attacks (4.2.3), time to effect (3.6.3), pain freedom at 15 minutes (3.7) and the course of a bout (4.2.1);
  - [S-015] concerns triptan supply;
  - [S-014] concerns follow-up.

  The cross-reference to OUT-023 does not supply cluster-specific support, because OUT-023's rescue quotes come from the IHS migraine acute-trial guideline [S-004]. This is the same defect type as R01-09, which added the S-007 3.7 quote for the 15-minute element of this requirement. The cluster trial guideline already cited, S-007, names both measures.
- **Evidence.** Verified verbatim at https://discovery.ucl.ac.uk/id/eprint/10161405/2/Matharu_IHS%20Guidelines%20for%20Clinical%20Trials%20in%20Cluster%20Headache.pdf, the S-007 URL (pdftotext and `-layout`; p. 22 of the accepted manuscript, the PDF page). The text is in section 3.8 "Secondary endpoints", Recommendations, under the heading "B. Additional secondary endpoints:", which lists items a–h. Two of them are:
  - "c. Percentage of attacks with need for rescue therapy";
  - "d. Number of attacks per day during the study period".

  The draft EMA guideline [S-022] lists the same two measures among the secondary endpoints for acute cluster-headache trials, in section 7.1.1, margin lines 564–565, p. 15: "Intake of rescue medication and percentage of attacks with need for rescue therapy." and "Number of attacks per day during the study period". That can serve as an alternative or additional source.
- **Earlier history of this item.** The OUT-031 Statement is unchanged since v00. Its Evidence changed in v01 (R01-09: the S-007 3.7 quote) and v05 (R05-01: the heading "Definitions of terms"). This remark extends R01-09 to the two remaining unquoted elements and reverses no earlier fix. OUT-031 is not frozen or on the oscillation watch list.
- **Required change.** Choose one:
  - **(a)** Add to OUT-031's Evidence the [S-007] section 3.8 recommendation items c and d, quoted verbatim as list items, located as (section 3.8 "Secondary endpoints", Recommendations, B. "Additional secondary endpoints", items c and d, p. 22 of the accepted manuscript), with or without the [S-022] lines. If the [S-022] lines are added, also add the EMA draft to OUT-031's Evidence basis. No change to the Statement or strength (SHOULD) is needed.
  - **(b)** Remove "attacks per day" and "the need for rescue treatment" from the Statement.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
