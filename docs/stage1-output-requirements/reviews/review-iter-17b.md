# Review — iteration 17, re-check b
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v16
Date: 2026-10-20

## Summary
I downloaded all 55 URLs again with curl into a new, empty folder of my own and did not use files that earlier agents left in the shared scratchpad. That covers the 46 section-5 sources, the English SFEMC Parts 1 and 2, the IHS listing page, the BASH contents page, the Swedish Kela page, the SEN and FDA landing pages, the PubMed abstracts through E-utilities and the PMC sources as Europe PMC fullTextXML. Only S-032 and S-034 needed one retry after a connection reset. All 297 quoted strings in section 3 are verbatim at their URLs: 284 matched by script, and I confirmed 13 by hand on page renders, the `-layout` text or the embedded figure images. Every stated page, line range and JATS paragraph or sentence position I checked is correct, and so are all 61 distinct translations, the grades, the metadata of all 37 PMIDs, the section-5 dates and strings, and the totals. I then read every one of the 256 distinct quotes in its source context. That reading found one gap that script checks cannot find. Three sources already cited (S-012, S-013, S-024) name the formulation or route of an acute medication as a factor in judging its effect, and the EHF consensus makes a subcutaneous formulation mandatory for triptan refractoriness. Yet no output shows formulation or route, although OUT-023 and OUT-024 say they let the EHF definitions be applied (R17b-01). My completeness and newer-edition searches found nothing else that requires a change: Portuguese, Russian-language Kazakh and Belarusian, Latin-American Spanish, Australian sources, the German S1 guideline, and PubMed for 2025–2026.

## Verification coverage
"Quotes checked" counts the quoted strings on the Evidence and Caveats lines of section 3: quotes, list items, grade labels and figure labels, once per citation. "Manual" means confirmed on a 150-dpi page render, the `-layout` text or the embedded figure image. "Read in context" means that I read each distinct quote of the source with at least 700 characters either side, and the full section where its role was in doubt, and checked it against the clause it supports. Separately from the table, I checked 144 strings quoted inside locations: 141 matched by script, and the other 3 are figure headings that I read on the images. I also checked the quoted strings and dates in section 5.

| Source ID | Quotes checked | Verified verbatim | Read in context (yes/no) | Not found | Unreachable (what you tried) |
|---|---|---|---|---|---|
| S-001 | 24 | 24 (1 manual: 8.2.2 note 1 in the right column of the p. 123 `-layout` text). PDF page = printed page | yes | 0 | — |
| S-002 | 26 | 26 (printed = PDF + 1025) | yes | 0 | — |
| S-003 | 6 | 6 (printed = PDF + 814) | yes | 0 | — |
| S-004 | 10 | 10 (JATS 1.3.2, 1.3.3, 1.3.4.2, 1.3.4.5) | yes | 0 | PMC page not used; Europe PMC fullTextXML |
| S-005 | 9 | 9 (printed = PDF + 802; "meta-" hyphenated at a line end) | yes | 0 | — |
| S-006 | 9 | 9 (1 manual: the 2.3.3.2 recommendation, where the text layer displaces "curve"; read on a 150-dpi render of p. 10, which also shows the 2.3.3.1 sentences) | yes | 0 | — |
| S-007 | 8 | 8 (accepted manuscript pp. 20–22, 25) | yes | 0 | — |
| S-008 | 11 | 11 (Q6 and Q7 strings recur in the p. 6 summary table; also present on the stated pp. 12 and 13; the Q4 sentence is at the foot of the left column of p. 11) | yes | 0 | — |
| S-009 | 3 | 3 (pp. 22, 33) | yes | 0 | — |
| S-010 | 8 | 8 (abstract quotes in the efetch abstract; full-text quotes on pp. 3 and 7; "patient-reported" split at a line end) | yes | 0 | E-utilities efetch for the abstract |
| S-011 | 3 | 3 | yes | 0 | Europe PMC fullTextXML |
| S-012 | 10 | 10 (Discussion ¶2 s1, ¶5 s4, ¶6 s5, ¶7 s1–4, as stated) | yes | 0 | PMC page served a reCAPTCHA to curl; Europe PMC fullTextXML |
| S-013 | 10 | 10 ("Drug failure" ¶1, ¶2 s1 and s3, ¶3 s3, ¶4 s1; "Assessment of patients" ¶3 s2; "Debilitating headache" ¶1 last sentence and ¶3; "Cut-offs values"; Results ¶ on refractory migraine) | yes | 0 | Europe PMC fullTextXML |
| S-014 | 14 | 14 | yes | 0 | Europe PMC fullTextXML |
| S-015 | 13 | 13 ("Published 19 September 2012", "Last updated 03 June 2025") | yes | 0 | — |
| S-016 | 11 | 11 (PDF = printed + 6; "Revised May 2026"; the section 5 R on PDF pp. 12 and 37) | yes | 0 | — |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026" on both section pages; contents page "V1.0 2019") | yes | 0 | — |
| S-018 | 15 | 15 (1 manual: 15B, where "Level C" interrupts the sentence; levels 12A, 14A, 14C–14F and 15A–15D confirmed in the `-layout` text) | yes | 0 | — |
| S-019 | 3 | 3 (p. 3) | yes | 0 | — |
| S-020 | 5 | 5 (printed = PDF − 3) | yes | 0 | — |
| S-021 | 4 | 4 (pp. 5, 6, 11; 24 January 2007; in effect 31 July 2007) | yes | 0 | — |
| S-022 | 6 | 6 (all manual: margin line numbers removed; lines 383–384, 393–394, 421–425, 427–429 and 464–465 on pp. 11–13; consultation 10 September 2026 – 31 January 2027) | yes | 0 | — |
| S-023 | 4 | 4 | yes | 0 | Europe PMC fullTextXML |
| S-024 | 13 | 13 (2 manual: the Rd5 row and its "Fort", read on the 2006 × 1337 px Figure 3 image under "FORCE DE LA RECOMMANDATION". English Part 1: section 2.2 on p. 726; Table 3 rates Rd5 "Strong") | yes | 0 | — |
| S-025 | 5 | 5 (all on the 1864 × 2452 px Figure 1 image: RT25, cited twice, under "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE,", with "Fort"; RT15–RT32 "Fort", RT33–RT34 "Modéré". English Part 2: Table 6 rates Rt25 "Strong") | yes | 0 | — |
| S-026 | 0 (not cited) | — (URL returns HTTP 200) | — | — | — |
| S-027 | 7 | 7 ("Publicatiedatum: 04-12-2023") | yes | 0 | — |
| S-028 | 1 | 1 (11-01-2018; the GRADE sentence) | yes | 0 | — |
| S-029 | 2 | 2 | yes | 0 | — |
| S-030 | 4 | 4 (PDF pp. 12, 16, 19) | yes | 0 | — |
| S-031 | 11 (incl. 2 grade labels) | 11 (1 manual: CQ II-2-14 across the side tab, PDF p. 207 = printed p. 191, grade A; CQ I-10 in the 推奨 box on PDF p. 48, grade B; CQ I-4, II-1-6, II-1-12 and VI-3 on the stated printed pages) | yes | 0 | — |
| S-032 | 5 | 5 | yes | 0 | Connection reset once; retry succeeded |
| S-033 | 5 | 5 (pp. 18, 19, 26, 53; grade C/5 after 2.5 and 7.1; "Год утверждения: 2024") | yes | 0 | — |
| S-034 | 3 | 3 (p. 34 with grade C/5; p. 50) | yes | 0 | Connection reset once; retry succeeded |
| S-035 | 5 | 5 (PDF pp. 48, 78; ISBN, "Ağustos - 2025") | yes | 0 | — |
| S-036 | 2 | 2 (PDF p. 16) | yes | 0 | — |
| S-037 | 1 | 1 | yes | 0 | Europe PMC fullTextXML |
| S-038 | 1 | 1 | yes | 0 | Europe PMC fullTextXML |
| S-039 | 2 | 2 | yes | 0 | — |
| S-040 | 2 | 2 | yes | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | yes | 0 | Europe PMC fullTextXML |
| S-042 | 3 | 3 (Table 2 row Question 6; Results panel discussion) | yes | 0 | Europe PMC fullTextXML |
| S-043 | 1 | 1 | yes | 0 | Europe PMC fullTextXML |
| S-044 | 1 | 1 | yes | 0 | E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113, 395; printed = PDF − 2) | yes | 0 | — |
| S-046 | 3 | 3 (printed = PDF − 3; landing page "Draft", June 2023, FDA-2022-D-1729) | yes | 0 | — |
| **Total** | **297** | **297** (284 script, 13 manual) | **all 256 distinct quotes** | **0** | — |

### Other checks
- **Translations and omissions.** I read all 61 distinct non-English quotes against their translations: Dutch, Danish, German, French, Spanish, Portuguese, Italian, Finnish, Russian, Turkish, Chinese and Japanese. All are faithful. I also read the source text around every "[...]" and every quote cut at its start or end. None of them changes the meaning.
- **Grades and types.** The AAN levels, the Japanese and Russian grades, the SFEMC "Fort"/"Strong" ratings and the ungraded status of the SIGN 4.1, China 3.2, SEN 2026 and Japan CQ VI-3 passages all match the sources.
- **Metadata.** All 37 PMIDs match section 5 and the search log in esummary: authors, journal, year, volume, issue, pages, DOI and PMCID.
- **Totals and IDs.** By the stated rule there are 39 requirements: 10 MUST, 24 SHOULD, 4 MAY and 1 SHOULD NOT. No RFC 2119 term appears before "Strength:". There are 46 source rows and 45 cited sources (all but S-026), and no OUT reference dangles.
- **Scope.** I read every Statement, Rationale, Evidence basis and Caveat, and ran a keyword scan with the quotes stripped out. Neither found input, storage or derivation content beyond the unit and statistic examples accepted in earlier iterations.

### Checked and not raised
- **OUT-007 Caveat.** In S-022 section 5.2.3, the secondary endpoints for prophylaxis do not include attack counts. The Caveat's clause "attack counts remain useful as a secondary measure" is not attributed to S-022, and the S-002 1.3.2.0 quote in the same requirement supports it ("The secondary outcome with highest priority is the reduction in migraine attacks."). No change is required.
- **OUT-023 Rationale, "national guidelines recommend switching after repeated failure of the same triptan".** Only BASH is quoted. SIGN 155 section 3.1 says the same thing in its own words: "it is worth sequencing through different triptans to find the most effective one". The plural is accurate.
- **OUT-018 Rationale, "All guidelines judge preventive treatment by the change … from baseline at defined time points".** The guidelines cited all do so. The IHS position statement proposes absolute goals in addition, and OUT-019 and OUT-020 already state that conflict. No change is required.
- **OUT-024 and S-013 "Drug failure" paragraph 2.** The source later says "we support the use of drugs in the same class, but with a different mechanism of action". The list still shows each treatment, so this does not contradict grouping by class (review 17 reached the same conclusion).
- **Newer editions.** PubMed for 2025–2026 shows no new IHS trial guideline and no new EHF guideline or consensus that supersedes S-002 to S-014. The new items are neuromodulation guidelines, the RWE guideline, a summary of the IHS acute recommendations in American Family Physician, and primary studies. The IHS guidelines page still links only the 1st edition of the paediatric guideline. The 2023 update (PMID 37226450) still gives HTTP 403 at SAGE (its only Unpaywall location) and is not in Europe PMC, as the S-005 entry says. The SPC 2021 recommendations (S-036) have no newer edition that I could find.
- **Completeness searches, no new quotable output requirement:**
  - **Portuguese:** the Acta Médica Portuguesa 2025 consensus (PMID 40359119) returned a Cloudflare challenge (HTTP 403), and Europe PMC lists it as subscription-only. It is already logged as unreachable.
  - **Russian (Kazakhstan, Belarus):** no national migraine protocol was found. The Belarusian 2023 protocol that appeared concerns maxillofacial neurogenic disorders.
  - **Latin-American Spanish:** only the Ibero-American consensus (Neurology Perspectives 2025), already assessed in review 05.
  - **English (Australia):** the PBAC 2024 stakeholder statement on the PBS diary-based continuation criteria. OUT-025 already covers scheme-specific windows at MAY.
  - **German:** register.awmf.org still serves the Anubis anti-bot page for S1 030-057, and Europe PMC has no copy.

## Remarks
### R17b-01 [missing-requirement] — target: OUT-023 (Statement, Rationale, Evidence basis, Evidence) and OUT-024 (Statement, acute-treatment list; Evidence basis)
- **Problem.** No output shows the formulation or route of administration of an acute medication. The document's own sources say this matters for exactly the purposes that OUT-023 and OUT-024 claim to serve.
  - **What OUT-023 claims.** It reports outcomes "For each acute medication … across the attacks treated with it" and how consistently "the drug" was effective, "so that the EHF definitions of effective attack treatment and triptan response [S-012] can be applied". For the same purpose it adds the timing of intake, so that "an apparent non-response after late intake is visible" (added in v01, R01-11, from S-012 and S-024).
  - **What OUT-024 claims.** It lists acute treatments grouped by class. Its Rationale and Evidence basis rest the acute grouping on S-012's reference to "an individual's resistance and refractoriness to triptans".
  - **What S-012 says about formulation.** A person may respond "to a higher dose and a different formulation of the same triptan". Subcutaneous formulations are generally more effective than oral ones. Failure of a subcutaneous triptan is "mandatory for the definition of triptan refractoriness" (quotes below).
  - **Consequence for OUT-023.** As specified, it pools attacks treated with different formulations of the same drug into one per-drug summary. A non-response to an oral form is then shown as a non-response to the drug.
  - **Consequence for OUT-024.** The list cannot show whether the EHF refractoriness category, which OUT-024 invokes, applies.
  - **The sources already quoted name formulation and route next to the elements the document turned into outputs.**
    - **S-013, quoted in OUT-024:** "In order to assess the efficacy of acute headache medications, adequate timing of drug administration, dosage and formulations used, should be considered." Timing became an output in OUT-023 and dosage in OUT-024, but formulations did not. OUT-024's Evidence basis paraphrases this sentence as stating only "that the dosage used is to be considered".
    - **S-024, quoted in OUT-014 and OUT-023:** "… la posologie, le moment et la voie d'administration …" ("dosage, timing and route of administration"), to be reviewed at every visit. OUT-023 uses "le moment" for its timing element and leaves the route out.
  - **Precedents.** This is the same defect type as R08-01, where an EHF definition that OUT-023 claims to support could not be applied from the specified outputs. It is also the counterpart of R01-11.
- **Evidence.** Each quote below was verified verbatim on 2026-10-20 in the Europe PMC fullTextXML of PMC9555163 (https://www.ebi.ac.uk/europepmc/webservices/rest/PMC9555163/fullTextXML). This is the full text of S-012, whose section-5 URL is https://pmc.ncbi.nlm.nih.gov/articles/PMC9555163/; that PMC page served a reCAPTCHA page to curl.
  - [S-012] Background, third paragraph (the paragraph beginning "In randomized clinical trials (RCTs), several endpoints have been used"): "In fact, individuals with migraine might respond to the same triptan during a different attack, or to a higher dose and a different formulation of the same triptan or another triptan type."
  - [S-012] Results > Consensus > "Definition of triptan failure", second paragraph. This is the paragraph whose first sentence OUT-023 already quotes ("As stated above, the assessment of effectiveness of a triptan should consider early administration."). It contains:
    - "The Consensus Panel agreed that subcutaneous formulations are generally more effective than oral formulations, as also reported in some trials (Fig. 2; Table S6 in Supplementary File)."
    - "Although not deemed necessary to define resistance to triptans (Table S8 in Supplementary File), failure to subcutaneous triptans was considered mandatory for the definition of triptan refractoriness as subcutaneous formulations have the fastest absorption; thus, other triptan formulations with slower absorption are not expected to lead to triptan response."
  - [S-012] Discussion, fifth paragraph, second sentence: "Studies available in the literature assessed some factors that potentially influence response to triptans, including the route and timing of administration."
  - Already in the document, verified at the section-5 URLs:
    - [S-013] "In order to assess the efficacy of acute headache medications, adequate timing of drug administration, dosage and formulations used, should be considered." (OUT-024; Discussion, "Debilitating headache", first paragraph, last sentence).
    - [S-024] "À chaque visite, il est recommandé de revoir le traitement de crise, à savoir le type de médicament, le nombre de jours de prise (calendrier des maux de tête), la tolérance, la posologie, le moment et la voie d'administration, ainsi que le respect des contre-indications." (OUT-014, OUT-023; p. 401).
- **Earlier history of this item.**
  - OUT-023 changed in v01 (R01-09, R01-11), v02 (R02-01), v08 (R08-01) and v14 (sweep). OUT-024 changed in v12 (R12-01), v13 (R13-01) and v14 (R14-01).
  - No review, fix or oscillation check mentions formulation or route; I searched all of them for "formulation", "route", "voie" and "subcutaneous".
  - This remark only adds an element (or a caveat) and removes or reverses nothing. All elements on the oscillation watch list for OUT-023 and OUT-024 stay as they are.
  - Neither item is frozen.
- **Required change.** Choose one.
  - **(a) Add the element (preferred).**
    1. **OUT-023 Statement.** Add at SHOULD that, for each acute medication, the output identifies its formulation or route of administration (for example oral, nasal or subcutaneous), and shows the per-drug outcomes and their consistency separately for each formulation of the same drug. The purpose is that a non-response to one formulation is not read as a non-response to the drug.
    2. **OUT-024 Statement.** Show the formulation or route in each entry of the acute-treatment list, so that the EHF triptan-refractoriness category that OUT-024 invokes can be judged.
    3. **Evidence.** Add the S-012 Background sentence and the two S-012 "Definition of triptan failure" sentences above, with their locations. Adding the Discussion sentence is optional.
    4. **Rationale.** Add one clause on formulation.
    5. **Evidence basis.** Name the support: consensus (EHF 2022 [S-012]; EHF 2020 [S-013]) and national guideline text (SFEMC [S-024], running text "il est recommandé", not a graded recommendation). The strength stays SHOULD.
    6. **OUT-024 Evidence-basis paraphrase.** Correct it so that it reflects that S-013 names timing, dosage and formulations.
  - **(b) Qualify the claims.** If the fixer judges the support insufficient for a new element, add a Caveat to OUT-023 and OUT-024, with the S-012 sentences, stating three things: the outputs do not distinguish formulations; a non-response may concern only one formulation of a drug; and the EHF triptan-refractoriness category, for which S-012 makes failure of a subcutaneous triptan mandatory, cannot be judged from these outputs. The OUT-024 paraphrase of S-013 must still be corrected.

  **Constraints for either option (PROCESS.md section 2).** Describe only the output's breakdown and labelling, not how formulation or route is recorded. Do not quote or restate the numeric criteria of the S-012 triptan-failure definitions (as R13-01 advised). The "mandatory" sentence quoted above contains no numeric criterion.

## Notes on frozen items (for the human)
None. FROZEN_ITEMS.md does not exist.
