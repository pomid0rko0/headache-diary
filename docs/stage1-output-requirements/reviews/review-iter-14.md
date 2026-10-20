# Review — iteration 14
VERDICT: REMARKS
REMARK_COUNT: 4
Reviewed version: v13
Date: 2026-10-20

## Summary
I downloaded all 46 sources again with curl into a new, empty folder of my own and did not reuse files left by earlier agents. Every URL in section 5 returned HTTP 200. The brainmed.com reprint (S-032) reset the connection once and loaded on retry.

A script extracted every quoted string in section 3 and matched it against the downloaded text. Matching ignored NFKC form, quote marks, dashes and whitespace, and "[...]" segments had to occur in order. All 229 distinct strings (252 occurrences) are verbatim: 224 by script and 5 by hand, on page renders or in the `-layout` text. I also read all 66 translations and all 13 "[...]" omissions, re-derived every page offset, and checked all 37 PMIDs against PubMed esummary. The totals, IDs and cross-references are correct, and no authored text breaks the scope rules.

The v13 change is correct. Both new S-012 quotes are verbatim. Their locations are right: Discussion paragraph 7 of 7, sentences 1–4, and paragraph 2, sentence 1. The new Evidence-basis and Rationale clauses paraphrase S-012 accurately.

The four remarks have one cause. Four Statements, unchanged since v00, each contain an element that no quote under that requirement supports. This is the defect type of R11b-01, R12-01, R12-02 and R13-01. Each source is already cited in the document, and I verified the missing support in it.
- **OUT-024:** dose changes and treatment duration.
- **OUT-009:** markers for dose changes and stops.
- **OUT-018:** moderate/severe headache days, inside a MUST sentence.
- **OUT-026:** the instrument's grading or categories.

I searched in Serbian, Slovak, Lithuanian, Belarusian/Kazakh (Russian-language), Arabic/Egyptian and New Zealand English, and ran PubMed 2024–2026 guideline queries. These found no missing output requirement and no superseding edition.

## Verification coverage
"Script" means the string matched the downloaded text. "Manual" means I confirmed it on a 150–300 dpi page render or in the `-layout` text. Counts are distinct quoted strings in section 3: quotes, list items, caveat quotes, and grade or figure labels quoted in Evidence or Evidence-basis lines.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 20 | 20 (1 manual: 8.2.2 note 1, `-layout` text of p. 123; PDF page = printed page; 1.3 note 5, A1.1, 8.2 notes, Definitions of terms pp. 209–210 confirmed) | 0 | — |
| S-002 | 17 (incl. 3 list items) | 17 (PDF page + 1025) | 0 | — |
| S-003 | 2 | 2 (PDF page + 814) | 0 | — |
| S-004 | 7 | 7 (JATS 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5) | 0 | Europe PMC fullTextXML; PMC page also returned full text |
| S-005 | 7 | 7 (PDF page + 802) | 0 | — |
| S-006 | 4 | 4 (p. 10) | 0 | — |
| S-007 | 6 | 6 (accepted manuscript pp. 20, 21, 22, 25) | 0 | — |
| S-008 | 8 | 8 (Q2 p. 9, Q4 p. 11, Q6 pp. 12–13, Q7 p. 13) | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | 0 | — |
| S-010 | 4 | 4 (abstract quotes in the efetch abstract; pp. 3, 7) | 0 | E-utilities efetch for the abstract |
| S-011 | 3 | 3 | 0 | Europe PMC fullTextXML |
| S-012 | 10 (2 new in v13) | 10. Discussion has 7 paragraphs. The v13 quotes are paragraph 7, sentences 1–4, and paragraph 2, sentence 1. The source has a no-break space in "(Fig. 4)". | 0 | Europe PMC fullTextXML; PMC page also returned full text |
| S-013 | 6 | 6 (Results; Discussion > "Drug failure" paragraphs 1–2, "Debilitating headache") | 0 | Europe PMC fullTextXML. PMC7296705 served a reCAPTCHA page to curl. |
| S-014 | 12 | 12 (all JATS section paths as stated) | 0 | Europe PMC fullTextXML |
| S-015 | 13 (incl. 2 list items) | 13. Numbers 1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37 and 1.3.48 confirmed. "Published 19 September 2012", "Last updated 03 June 2025". The 1.3.1 omissions leave out only the recording clause. | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6; section 5 "R" markers; 7.3 checklist "based on their experience") | 0 | — |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026" on both section pages, dateModified 2026-09-14; TOC "V1.0 2019") | 0 | — |
| S-018 | 8 | 8 (1 manual: 15B, interrupted by "Level C"). Levels 12A B, 14A B, 14D B, 14E B, 15A B, 15B C, 15C A, 15D B confirmed in the `-layout` text of pp. 7–8. "published in Neurology® online on August 31, 2026" | 0 | — |
| S-019 | 2 | 2 (p. 3) | 0 | — |
| S-020 | 2 | 2 (printed p. 4 = PDF p. 7) | 0 | — |
| S-021 | 3 | 3 ("Page 5/12", "Page 6/12") | 0 | — |
| S-022 | 6 | 6 (margin line numbers stripped; lines and pp. 11–13 confirmed; consultation 10 Sep 2026 – 31 Jan 2027) | 0 | — |
| S-023 | 4 | 4 | 0 | Europe PMC fullTextXML |
| S-024 | 11 (incl. grade and figure labels) | 11 (1 manual: Rd5 on a 300 dpi crop of Figure 3, p. 402, with the title row, "FORCE DE LA RECOMMANDATION" and Rd1–Rd10 "Fort"). The English Part 1 strings in the OUT-033 Evidence basis matched in the IHS copy, and Table 3 Rd5 is "Strong". PDF page + 394. | 0 | — |
| S-025 | 3 | 3 (1 manual: RT25, first sentence plus "[...]", on the render of Figure 1, p. 414, with the heading "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE," and "Fort"). English Table 6: Rt25 "Strong" (PDF p. 10). | 0 | — |
| S-026 | 0 (not cited) | — | — | Downloaded (superseded entry) |
| S-027 | 6 | 6 | 0 | — |
| S-028 | 1 | 1 | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19) | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (1 manual: CQ II-2-14 across the side tab, render of PDF p. 207 = printed p. 191, grade A). The CQ I-10 sentence is in the 推奨 box, grade B (PDF p. 48). Printed = PDF − 16. | 0 | — |
| S-032 | 3 | 3 (section 3.2; 七 > 病人教育; the omitted items are the other criteria) | 0 | First request reset by peer; retry succeeded |
| S-033 | 5 | 5 (pp. 18, 19, 26, 53; grade C/5 after 2.5 and 7.1) | 0 | — |
| S-034 | 3 | 3 (pp. 34, 50; grade C/5 after 7.1) | 0 | — |
| S-035 | 3 | 3 (PDF pp. 48, 78) | 0 | — |
| S-036 | 2 | 2 (PDF p. 16) | 0 | — |
| S-037 | 1 | 1 (heading printed "PRINCIPLES OF PROPHYLAXIS") | 0 | Europe PMC fullTextXML |
| S-038 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-042 | 2 | 2. Question 6: the acute-response parameter is in the panel discussion only, not in the final list, as OUT-021 and OUT-023 state. | 0 | Europe PMC fullTextXML |
| S-043 | 1 | 1 | 0 | Europe PMC fullTextXML |
| S-044 | 1 | 1 | 0 | E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113, 395; landing page "incluido en la web de la SEN el 21 de enero de 2026") | 0 | — |
| S-046 | 3 | 3 (printed p. 5 = PDF p. 8). "Contains Nonbinding Recommendations" appears on each of 9 pages. The docket is on the landing page. | 0 | — |
| **Total** | **229** | **229** (224 script, 5 manual) | **0** | — |

Other checks:
- **Section 5.** 72 quoted source strings. 67 matched by script. 3 I confirmed by hand: NICE prints "Do not" with a capital, and "FORCE DE LA RECOMMANDATION" and "FORCE" are figure text. The last 2 are the document's own translations, which are faithful. All 37 PMIDs, DOIs and PMCIDs match esummary.
- **Headings quoted in locations.** 125 strings. The ones not matched by script are:
  - authored labels;
  - figure headings, confirmed on the images;
  - "Principles of prophylaxis", printed in capitals;
  - English Part 1 strings, matched in S-024en.
- **Translations.** I read all 66 against their originals. All are faithful.
- **Omissions.** All 13 quotes with "[...]" leave out only recording or calculation details, cross-references or other list items. No omission changes the meaning.
- **Totals and IDs.** 39 requirements (10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT) by the stated rule, with no RFC 2119 term before "Strength:". 46 source rows; 45 cited (all but S-026). No duplicate ID, and every reference resolves. history/v13.md is byte-identical to OUTPUT_REQUIREMENTS.md.
- **Scope.** I read every Statement, Rationale, Evidence basis and Caveat. Nothing in them is input, storage or derivation content. The v13 quotes carry no numeric criteria.

Checked and not raised:
- **OUT-027, "household work".** No quote names it. The quoted domains "family ... life" (S-016) and "family or social activities" (S-013), with the MIDAS/HALT lost-productive-time quotes (S-014), cover it. The only S-014 sentences that name household work describe the questions or the scoring, which section 2 excludes.
- **OUT-008, "headache-free days".** This is a MAY output. S-002 1.3.2.5.2 ("Headache and symptom-free days") is consistent with it. Not raised.
- **OUT-023, "repeat medication" and "most bothersome symptom at 2 hours".** The Statement attributes these to the named standards. FDA S-020 lists "The proportion of patients requiring additional medication (either a second dose or rescue medication) within 24 hours" and co-primary endpoints at 2 hours.
- **AAN/AHS 2026 16B (level A, monitoring AEs).** It is a clinician action, as review 06 noted. OUT-024 is SHOULD.
- **Serbian national guideline.** "Glavobolja" (Serbian Neurological Society, 2005, https://drustvoneurologasrbije.org/vodici/galvobolja.pdf) asks for a diary of attack frequency, severity and acute therapy, reviewed every 2–3 months. This is covered by OUT-004, OUT-005, OUT-010, OUT-014 and OUT-018.
- **Other searches.** Slovak, Lithuanian, Belarusian, Kazakh, Egyptian and New Zealand searches found no guideline text with diary-output statements. PubMed 2024–2026 found only items already logged or reviewed, plus a 2026 Belgian review article (Rev Med Liege, PMID 41987542) and a 2026 systematic review of paediatric guidelines (PMID 41699419). Neither is a guideline.
- **Newer editions.** The Japanese 2021 guideline is still current. The IHS paediatric update 2023 (PMID 37226450) is still unreadable: SAGE returned 403 to curl and WebFetch, and OpenAlex lists no repository copy. This matches the S-005 note.

## Remarks
### R14-01 [unsupported/overstated] — target: OUT-024 (Statement elements "start and stop dates, dose changes, treatment duration"; Evidence; Evidence basis)
- **Problem.** The Statement requires each treatment to be listed "with start and stop dates, dose changes, treatment duration, ...". None of the eight quotes in OUT-024 mentions dose or duration:
  - S-013 covers drug failure and classes.
  - S-012 covers triptan resistance and other classes.
  - NICE 1.3.24 counts preventives that "have not worked or are not tolerated".
  - S-002 concerns adverse events and discontinuation.
  - S-019 concerns a list of medicines tried.

  The Rationale and Evidence basis do not mention dose or duration either. PROCESS.md section 3 requires support for each element, and R11b-01, R12-01, R12-02 and R13-01 treated unquoted Statement elements as remarks.
- **Evidence.** Each item below was verified verbatim.
  - **S-013**, Europe PMC fullTextXML of PMC7296705 (https://pmc.ncbi.nlm.nih.gov/articles/PMC7296705/). Both sentences concern preventives.
    - Discussion > "Assessment of patients", third paragraph, second sentence: "It is not reasonable to test again preventive medications used in the past with no efficacy or with intolerable side effects provided that information on duration, dose and adverse events is sufficient and reliable."
    - Discussion > "Drug failure", third paragraph, third sentence: "If therapy was inadequate (low dose or incorrect duration) the failure is to be reassessed."
  - **S-013, for the acute list.** Discussion > "Debilitating headache", first paragraph, last sentence: "In order to assess the efficacy of acute headache medications, adequate timing of drug administration, dosage and formulations used, should be considered."
  - **Graded alternative for preventive dose changes.** [S-018] p. 7, Recommendation 14, both level B (https://www.aan.com/Guidelines/Home/GetGuidelineContent/1180):
    - "14C. If suboptimal treatment response is observed by 8 weeks, physicians should optimize the dose of the medication for migraine prevention to the maximum tolerated dose or predetermined maximum based on efficacy studies."
    - "14F. If side effects are not tolerable, clinicians should consider a dose reduction."
  - **Do not quote** the later sentences of "Drug failure" paragraph 3 ("Minimal duration of drug trials was set at 2 months ..."). They carry numeric criteria, which section 2 excludes.
- **Earlier history of this item.**
  - The OUT-024 Statement is unchanged from v00 to v13. Its Evidence and Evidence basis changed in v12 (R12-01) and v13 (R13-01), both times only for the "grouped by drug class" element.
  - This remark leaves those additions untouched and reverses no fix.
  - No earlier review raised dose or duration. OUT-024 is not frozen and is not on the oscillation watch list.
- **Required change.** Choose one:
  - **(a) Add support.** Add the first S-013 sentence to OUT-024's Evidence; the second S-013 sentence and AAN 14C/14F are optional. For the acute list, add the "Debilitating headache" sentence. Add one Evidence-basis clause, for example: "The start and stop dates, dose changes and duration of each treatment rest on the EHF consensus (2020) [S-013], which treats information on duration, dose and adverse events as necessary to accept a past treatment failure". If 14C/14F are quoted, add "(AAN/AHS 2026 14C, 14F, level B)". The strength stays SHOULD.
  - **(b) Remove the unsupported elements.** Remove from the Statement whichever of these elements are left without a quote.

### R14-02 [unsupported/overstated] — target: OUT-009 (Statement element "dated markers for the start, dose change and stop of preventive treatments"; Evidence)
- **Problem.** The Statement requires "dated markers for the start, dose change and stop of preventive treatments". Two quotes support a start marker:
  - [S-002] "Understanding the onset of action of a preventive treatment ...";
  - [S-005], the trajectory of response compared with baseline.

  No quote in OUT-009 mentions a dose change or stopping a treatment, and the Rationale and Evidence basis do not mention them either. OUT-009 has no cross-reference to OUT-018 or OUT-022, where such support is quoted.
- **Evidence.** These quotes are already in the document and I verified them in this review:
  - **Dose change.** [S-016] section 4.1, p. 14 (PDF p. 20), quoted in OUT-018: "Prophylactic treatment should be used for eight weeks at the target dose or maximum tolerated dose (for those with a titration schedule) before deciding if it is effective or not." Alternatives:
    - [S-018] 14A, level B, p. 7 ("... at the recommended tolerated dose ..."), quoted in OUT-018;
    - [S-018] 14C, level B, p. 7, quoted in R14-01.
  - **Stop.** [S-008] Q7, Optimal-level recommendation, p. 13, quoted in OUT-022: "Monitoring of headache frequency with a headache diary or a monthly calendar is recommended after stopping a migraine preventive treatment."
  - The numbers in the S-016 and S-018 quotes belong to those sources; section 1 already covers them.
- **Earlier history of this item.** OUT-009 has been byte-identical from v00 to v13. No earlier remark or fix touched it, and it is not frozen or on the watch list.
- **Required change.** Choose one:
  - **(a) Add support.** Add a dose quote and the S-008 Q7 quote to OUT-009's Evidence. Name their sources in the Evidence basis, for example: "graded guideline recommendation (AAN/AHS 2026 14A, level B)" or "national guideline text (SIGN 155 section 4.1)", and "IHS 2024 Q7". The strength stays SHOULD.
  - **(b) Keep only the start marker.** Remove "dose change and stop" from the Statement.

### R14-03 [unsupported/overstated] — target: OUT-018 (MUST sentence, clause "(and, where reported, moderate/severe headache days)"; Evidence)
- **Problem.** The first Statement sentence is MUST. It requires the baseline comparison to cover "(and, where reported, moderate/severe headache days)". None of the 12 quotes in OUT-018 mentions moderate/severe headache days:
  - NICE 1.3.27–1.3.29 concern frequency of migraines and headache days;
  - S-002 recommendation a concerns migraine days;
  - S-018, S-016, S-011, S-008 Q2 and S-028 give time points;
  - S-033 concerns headache days;
  - S-035 concerns the diary.

  OUT-018 does not cross-reference OUT-006, where the support is quoted. The clause is conditional, so a diary without OUT-006 still complies, and R01-05's objection to OUT-021 does not apply. However, the MUST-level clause has no quoted support under its own requirement.
- **Evidence.** Both quotes were verified verbatim and are already quoted in OUT-006:
  - [S-002] section 1.3.1, recommendation b, p. 1035 (PDF p. 10), an international trial-methodology guideline that meets the MUST test of PROCESS.md section 3: "Alternative primary endpoints include change from baseline in moderate/severe headache days or 50% responder rate for the reduction of migraine days." (https://ihs-headache.org/wp-content/uploads/2025/04/Clinical-Trials-Controlled-trials-of-preventive-treatment-of-migraine-attacks-in-episodic-migraine-in-adults-CEP.pdf)
  - Practice support: [S-008] Q6, Optimal-level recommendation, p. 12: "a ≥ 50% decrease in monthly migraine days or moderate-to-severe headache days, optimally based on the use of a headache diary;".
- **Earlier history of this item.**
  - The OUT-018 Statement is unchanged from v00 to v13. Its Evidence and Evidence basis changed in v01 (R01-08: [S-015] 1.3.29 and [S-002] recommendation a) and v07 (R07-01: SIGN 155 relabelled as ungraded text).
  - OUT-018 is on the oscillation watch list ("SIGN 155 section 4.1 stays labelled ungraded"). This remark changes neither of those items and reverses no fix. No earlier review raised this clause.
- **Required change.** Choose one:
  - **(a) Keep MUST.** Add the S-002 recommendation b quote to OUT-018's Evidence; the S-008 Q6 quote is optional. Optionally add "(see OUT-006)" after the clause. No change to the strength or the Evidence basis is needed: it already lists the IHS trial-methodology guideline.
  - **(b) Lower the clause.** Move the clause into a separate SHOULD sentence, as OUT-021 does for components that are SHOULD in their own requirements. State the split in the Strength line.

### R14-04 [unsupported/overstated] — target: OUT-026 (Statement element "the instrument's own published grading or categories"; Evidence)
- **Problem.** The Statement requires instrument results to be reported with "total score and the instrument's own published grading or categories". None of the 14 quotes in OUT-026 mentions grading or categories. They support:
  - using the instruments;
  - the recall periods (S-002);
  - score improvement (S-008 Q6).

  The Rationale and Evidence basis are also silent on grading.
- **Evidence.** [S-014], Europe PMC fullTextXML of PMC6734476 (https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/), verified verbatim:
  - Section "The Headache-Attributed Lost Time (HALT) Indices: measures of burden for headache management in primary care" > "Scoring HALT", the paragraph directly after the table "Grading of HALT-90" (Table 18), first two sentences: "Grading has value in indicating the level of a patient’s personal need and, perhaps, priority for treatment. But for assessment as a prelude to planning management, or for establishing the baseline impact, the individual summed scores are more informative than overall grades."
    - The second sentence qualifies the first. The Statement already requires the total score next to the grade, so it stays consistent. The Evidence basis may note that grades are secondary to summed scores for baseline assessment.
  - Optional, for categories: section "The Headache Under-Response to Treatment (HURT) questionnaire: a guide to follow-up in primary care" > "The Headache Under-Response to Treatment (HURT) questionnaire", third paragraph, last sentence: "In either case, responses either fall into an area of “no concern” or are graded into one of three flagged areas indicating increasingly important treatment deficiencies; clinical advice is provided for each of latter."
- **Earlier history of this item.**
  - The OUT-026 Statement is unchanged from v00 to v13. OUT-026 changed in v01 (R01-02: S-041 location) and v06 (R06-01: SEN 2026 conflict).
  - OUT-026 is on the watch list: SEN 2026 stays as conflicting evidence, and the strength stays SHOULD. This remark changes neither and reverses no fix. No earlier review raised the grading element.
- **Required change.** Choose one:
  - **(a) Add support.** Add the two S-014 "Scoring HALT" sentences to OUT-026's Evidence; the HURT sentence is optional. Mention the support in the Evidence basis as expert guidance (Lifting The Burden/EHF), which is already listed there. The strength stays SHOULD.
  - **(b) Remove the element.** Remove "and the instrument's own published grading or categories" from the Statement.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
