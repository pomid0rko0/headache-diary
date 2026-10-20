# Review — iteration 01
VERDICT: REMARKS
REMARK_COUNT: 11
Reviewed version: v00
Date: 2026-10-20

## Summary
I downloaded all 44 sources with curl and checked every quote against the extracted text: all 173 distinct quotes (184 occurrences) and the 4 quoted grade labels exist verbatim at their URLs. 162 matched by script (NFKC-, whitespace-, dash- and hyphenation-insensitive); 11 were confirmed manually where layout breaks the text layer (S-022 line numbers, line-break hyphens in S-005/S-010, the "Level C" margin label in S-018, the chapter side tab in S-031, and the S-044 abstract read via E-utilities). Page and section locations, translations, "[...]" omissions and bibliographic metadata (checked against PubMed E-utilities and the documents' title pages) are correct, apart from the defects listed below. No scope violation was found in the authored text. The remarks cover:
- one wrong version/year (BASH) and one wrong location (S-041);
- two sources whose grading system is not named;
- strength inconsistencies, where MUST requirements embed SHOULD-level outputs or labelling (OUT-005/OUT-028 against OUT-002, OUT-021, OUT-029);
- evidence-basis entries and one statement element with no supporting quote;
- two evidence-backed output elements that are missing: adherence to preventive treatment, and timing of acute-medication intake.

These were checked and are not remarks:
- The SEN published a 5th edition of its manual in January 2026 (Redacción Médica, 21 Jan 2026), but no copy could be obtained, so I could not show that it changes S-026.
- The IHS/SISC 2025 evidence-based guideline (PMID 40277319), which the search log lists as not retrieved, can be read in the FLENI repository. It contains no statements about diary outputs.

## Verification coverage

Counts are distinct quotes per source. "Manual" means the script failed because of a text-layer artefact and the quote was confirmed by reading the page.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 14 | 14 | 0 | — |
| S-002 | 13 | 13 | 0 | — |
| S-003 | 2 | 2 | 0 | — |
| S-004 | 3 | 3 | 0 | — (Europe PMC XML and PMC HTML) |
| S-005 | 7 | 7 (1 manual: "meta-analyses" split by a line-break hyphen) | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 3 | 3 | 0 | — |
| S-008 | 7 | 7 | 0 | — |
| S-009 | 2 | 2 | 0 | — |
| S-010 | 3 | 3 (1 manual: "patient-reported" split by a hyphen); abstract quotes also matched in the PubMed abstract via efetch | 0 | pubmed.ncbi.nlm.nih.gov returns a cookie/JS challenge to curl; used E-utilities |
| S-011 | 3 | 3 | 0 | PMC HTML gives a challenge page to curl; verified in Europe PMC fullTextXML (same PMCID) |
| S-012 | 2 | 2 | 0 | as S-011 |
| S-013 | 4 | 4 | 0 | as S-011 |
| S-014 | 10 | 10 | 0 | as S-011 |
| S-015 | 9 | 9 | 0 | — |
| S-016 | 9 | 9 | 0 | — |
| S-017 | 3 | 3 | 0 | — (see R01-01 on the version) |
| S-018 | 7 | 7 (1 manual: 15B interrupted by "Level C"); levels checked on a page render | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 | 0 | — |
| S-021 | 3 | 3 | 0 | — |
| S-022 | 6 | 6 (all manual: line numbers interrupt the text; lines and pages correct) | 0 | — |
| S-023 | 2 | 2 | 0 | — |
| S-024 | 6 | 6 | 0 | — |
| S-025 | 1 | 1 | 0 | — |
| S-026 | 2 | 2 | 0 | — |
| S-027 | 6 | 6 | 0 | — |
| S-028 | 1 | 1 | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 | 0 | — |
| S-031 | 7 + 2 grade labels | 9 (1 manual: side tab in CQ II-2-14) | 0 | — |
| S-032 | 2 | 2 | 0 | brainmed.com reset the first connection; the retry succeeded |
| S-033 | 5 + 1 grade label | 6 | 0 | — |
| S-034 | 3 + 1 grade label | 4 (title page is an image; metadata confirmed from a render) | 0 | — |
| S-035 | 2 | 2 | 0 | — |
| S-036 | 2 | 2 | 0 | — |
| S-037 | 1 | 1 | 0 | — |
| S-038 | 1 | 1 | 0 | as S-011 |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 | 0 | — (location wrong, R01-02) |
| S-042 | 1 | 1 | 0 | as S-011 |
| S-043 | 1 | 1 | 0 | as S-011 |
| S-044 | 1 | 1 (manual, via E-utilities efetch) | 0 | PubMed web page gives a challenge to curl |
| **Total** | **173 + 4 grade labels** | **177** | **0** | — |

### Completeness search
Sources I checked beyond those in the document:
- **AWMF S1 030-057 (2025).** Anubis anti-bot page on both the clinician and patient PDFs, confirmed.
- **NHG-Standaard Hoofdpijn.** Anubis anti-bot page, HTTP 401, confirmed.
- **Swedish SKR and Nationellt kliniskt kunskapsstöd.** The certificate does not match the host, confirmed.
- **AHS 2019, 2021 and 2024 statements, and the IHS RWE guideline 2025.** Wiley and SAGE return 403, and none is in Europe PMC.
- **IHS paediatric update 2023.** SAGE returns 403 and the IHS site has no copy.
- **Korean Headache Society guideline.** Only press reports found.
- **Italian sources.** SISC: the 2025 IHS/SISC guideline (FLENI copy) has no diary-output statement. The Calabria regional 2024 guidance repeats existing requirements.
- **Russian CR "Головная боль напряжения" 2024 (ID 162_3).** Reachable at apicr.minzdrav.gov.ru. It repeats the statements of S-033 and adds no new output.
- **Danish, Japanese and EHF sources, ICHD.** No newer edition of S-030, S-031 or S-011 was found, and ICHD-4 exists only as work-in-progress documents.

## Remarks

### R01-01 [link/citation] — target: S-017 (used in OUT-015, OUT-019, OUT-023)
- Problem: S-017 is cited as "BASH Guideline V1.0 2019", with year "2019 (web version)". The pages at both cited URLs now carry a different version.
  - Both pages show the footer "BASH Guideline V2.0 2026".
  - Their page metadata gives `dateModified` 2026-09-14.
  - The 2.1.3 page refers to events of 2026: "NICE have announced approval of atogepant as acute treatment of migraine (May, 2026)".
  - Only the table-of-contents page (https://bash.org.uk/0-0-table-of-contents/) still shows "BASH Guideline V1.0 2019".
  - The three quotes are present on the current pages, so only the metadata is wrong.
- Evidence: footer "BASH Guideline V2.0 2026" on https://bash.org.uk/2-1-3-migraine-management/ and on https://bash.org.uk/2-2-1-medication-overuse-headache-epidemiology-diagnosis/ (accessed 2026-10-20).
- Required change: in section 5, change S-017's version to "BASH Guideline V2.0 2026 (web version; pages last modified 14 September 2026)" and its year to 2026. Keep the URLs.

### R01-02 [link/citation] — target: OUT-026 / S-041
- Problem: the quote "For assessment, they favoured the use of a headache diary as the primary tool, followed by the MIDAS and HIT-6 scales." is located as "(Discussion)". In PMC13253248 (Europe PMC fullTextXML) the sentence occurs only in the section "Conclusion", in the paragraph beginning "Consensus was achieved on several key aspects of migraine diagnosis and management." It does not occur in "Discussion".
- Required change: change the location to "(Conclusion)".

### R01-03 [link/citation] — target: S-028 and S-032 (section 5, type and grading)
- Problem: PROCESS.md section 3 requires a clinical practice guideline's grading system to be named. Both sources state GRADE, but their entries do not say so.
- Evidence:
  - S-032 currently reads "Clinical practice guideline (registered in the International Practice Guidelines Registry Platform, IPGRP2022CN297)". The guideline states: "按照推荐分级的评估和制订与评价（The Grading of Recommendations Assessment Development and Evaluation, GRADE）的要求将证据质量分为4级，采用证据到推荐表方式" (https://brainmed.com/guidance/detail/article/34408, section on guideline methods). Translation: "In accordance with GRADE, the quality of evidence was divided into 4 levels, using evidence-to-recommendation tables". The same paragraph ends "给出2级推荐意见" ("2 grades of recommendation are given").
  - S-028 currently reads "Clinical practice guideline (national; recommendation)". The module page states: "Hierbij is gebruik gemaakt van de GRADE methodiek." (https://richtlijnendatabase.nl/richtlijn/hoofdpijn/migraine/profylactische_behandeling_migraine.html, Verantwoording, "Methode richtlijnontwikkeling"). Translation: "The GRADE methodology was used for this."
- Required change:
  - S-032: name GRADE (4 levels of evidence quality, 2 grades of recommendation).
  - S-028: name the GRADE methodology.

### R01-04 [contradiction/duplication] — target: OUT-005 and OUT-028 against OUT-002
- Problem: the same labelling property has two different strengths.
  - OUT-002 sets labelling of the definition behind migraine days and headache days at SHOULD.
  - OUT-005 puts it inside a MUST: "MUST report the number of migraine days ..., labelled with the definition used (see OUT-002)".
  - OUT-028 likewise states "The view MUST show the source definitions it refers to".
  - The evidence behind OUT-002 cannot carry a MUST under PROCESS.md section 3. It consists of a trial-methodology comment about cross-study comparison in trials (S-003), an eDelphi consensus (S-043) and a working-group consideration (S-027). No classification standard or graded recommendation requires the label.
- Required change: make the labelling strength consistent.
  - Either move the labelling clause of OUT-005 out of the MUST sentence and set it at SHOULD with a reference to OUT-002, and change "MUST show the source definitions" in OUT-028 to SHOULD;
  - or give direct evidence that supports MUST and raise OUT-002 to match.

### R01-05 [strength-mismatch] — target: OUT-021
- Problem: OUT-021 is a MUST, but it requires several outputs to be presented together that are only SHOULD in their own requirements: OUT-006, OUT-007, OUT-010, OUT-012 and OUT-026. A diary that legitimately omits one of those SHOULD outputs cannot satisfy OUT-021.
  - The recommendation that names these dimensions is AAN/AHS 15D. It is Level B, which the S-018 entry maps to "should"; I checked the level on the rendered p. 8 of the clinician summary.
  - 15C (Level A) requires patient-centric, goal-based assessment but does not list the dimensions.
  - "Global impression of change" is not part of 15D at all.
- Evidence: the 15C and 15D quotes already in OUT-021, at https://www.aan.com/Guidelines/Home/GetGuidelineContent/1180 (p. 8, Level A and Level B respectively).
- Required change: choose one, and align the Evidence basis line with it.
  - (a) Restate OUT-021 at SHOULD.
  - (b) Keep MUST only for presenting together the MUST-level components (OUT-004, OUT-005 and OUT-014) for the same baseline and on-treatment periods. Make the inclusion of the OUT-006, OUT-007, OUT-010, OUT-012 and OUT-026 components SHOULD, applying where those outputs are provided.

### R01-06 [strength-mismatch] — target: OUT-029 (intensity clause)
- Problem: OUT-029 states "MUST present frequency, intensity and acute medication outputs separately for each headache type".
  - The intensity summary (OUT-010) is only SHOULD.
  - None of OUT-029's five quotes concerns intensity. They concern the quantity of each headache type (ICHD-3 item 12), identifying the types because treatments differ, differential diagnosis, medication overuse, and days with tension-type headache.
  - The clause therefore makes an intensity summary mandatory for patients with more than one headache type, without support and contrary to OUT-010.
- Required change: limit the MUST in OUT-029 to the frequency (and acute-medication) outputs per headache type. State intensity per headache type as SHOULD, applying where the OUT-010 output is provided.

### R01-07 [unsupported/overstated] — target: OUT-015
- Problem: the Evidence basis names "International practice recommendations (IHS 2024, ...)" as the highest-level support, and the rationale says IHS expresses limits per week. But the only S-009 quote given is a Background sentence: "Excessive acute medication use is associated with an increase in headache pain and associated symptoms and medication overuse headache." It says nothing about use within a week, so it does not support a weekly view. The weekly element currently rests only on the BASH quote.
- Evidence: S-009 contains a passage that does support it. Q12, Recommendations, Optimal, p. 22 (verified at https://www.aslroma1.it/uploads/files/06_07_IHS_recommendations_acute_treatment_migraine_2024.pdf): "We suggest limiting the use of analgesics, nonsteroidal anti-inflammatory drugs or lasmiditan to 2–3 days per week and to less than 10 days per month."
- Required change: replace or supplement the S-009 Background quote with the Q12 recommendation quoted above, located as "Q12, Recommendations, Optimal, p. 22". Section 1 of the document already allows a source's numeric criteria to be quoted. Otherwise, remove IHS from OUT-015's Evidence basis and rationale.

### R01-08 [unsupported/overstated] — target: Evidence basis of OUT-011, OUT-018, OUT-020, OUT-021, OUT-022, OUT-035
- Problem: each of these Evidence basis lines (or rationales) names a source that has no quote in that requirement. PROCESS.md section 3 requires a verbatim quote for every citation. The unquoted sources are:
  - OUT-011: "Turkey" (S-035).
  - OUT-018: "international trial-methodology guideline (IHS)". NICE "1.3.29" is also named but not quoted; it is the only source given for the onabotulinumtoxinA time point in the statement.
  - OUT-020: "NICE" and "DMKG/ÖKSG/SKG".
  - OUT-021: "international practice recommendations (IHS, consensus)".
  - OUT-022: "national consensus (DMKG/ÖKSG/SKG)", which also underlies "German-speaking countries" in the rationale.
  - OUT-035: "Japan".
- Evidence: candidate quotes, all verified verbatim at the URLs in section 5:
  - OUT-011, S-035 (PDF p. 48, preventive treatment principles): "Profilaktik tedavinin başarısı, atak sıklığında ve süresinde %50'lik bir azalma ve akut atakta ilaçlara artan yanıt ile değerlendirilir." Translation: "The success of prophylactic treatment is assessed by a 50% reduction in attack frequency and duration and an increased response to drugs in the acute attack."
  - OUT-018, S-002 (section 1.3.1, recommendation a, p. 1035): "The primary endpoint in controlled trials of preventive treatment of episodic migraine should be the change from baseline in migraine days per unit time."
  - OUT-018, S-015 (rec. 1.3.29): "Stop botulinum toxin type A if the frequency of headache days per month does not reduce by at least 30% after 2 treatment cycles, or if their condition has changed to episodic migraine for 3 consecutive months."
  - OUT-020, S-015 (rec. 1.3.28): "Stop CGRP inhibitors after 12 weeks of treatment if the frequency of migraines does not reduce by:" followed by the list items "at least 50% in episodic migraine" and "at least 30% in chronic migraine".
  - OUT-020, S-023 (section "Hintergrund"): "Bei der episodischen Migräne (eM) wird eine Prophylaxe als wirksam beurteilt, wenn die Migränetage um mindestens 50 % reduziert werden [...]". Translation: "In episodic migraine, prophylaxis is judged effective if migraine days are reduced by at least 50% [...]".
  - OUT-021, S-008 (Q6, Background, p. 13; already quoted in OUT-020): "Therefore, in addition to headache frequency and intensity responses, patient-centered outcomes (such as disability, quality of life, medication use for acute migraine attacks, and effect) should be considered (9,14,16)."
  - OUT-022, S-023 (section "Hintergrund"): "Es hat sich bewährt, im Verlauf einer Therapie die fortbestehende Indikation für eine wirksame Prophylaxe durch einen Absetzversuch oder die Reduktion der Dosis, oder die Verlängerung des Dosierungsintervalls zu überprüfen." Translation: "It has proved useful, in the course of therapy, to check whether an effective prophylaxis is still indicated by a discontinuation trial, a dose reduction or an extension of the dosing interval."
  - OUT-035, S-031 (CQ I-10, Background, p. 32; already quoted in OUT-034): "頭痛ダイアリーの目的は，患者が自分自身の頭痛の状況を把握し，正確な情報を効率よく医師に伝えることにより，適切な医療を推進することである．"
- Required change: for each item, either add a supporting quote (such as the candidates above) with location and translation, or delete the source from that requirement's Evidence basis and rationale.

### R01-09 [unsupported/overstated] — target: OUT-031 (and the last sentence of OUT-023)
- Problem: the 15-minute time point has no supporting quote.
  - OUT-031 requires "for acute treatments, effectiveness at 15 minutes".
  - OUT-023 states "For cluster headache, the corresponding time point is 15 minutes (see OUT-031)".
  - None of the quotes in either requirement mentions 15 minutes. The S-007 quotes concern weekly attacks, time to effect in general, and the course of a bout.
- Evidence: S-007, section 3.7 "Primary endpoint", Recommendations, p. 21 of the accepted manuscript (https://discovery.ucl.ac.uk/id/eprint/10161405/2/Matharu_IHS%20Guidelines%20for%20Clinical%20Trials%20in%20Cluster%20Headache.pdf): "Pain-freedom at 15 minutes without recurrence of any level of pain within 3 hours in the 1st treated attack."
- Required change: add this quote to OUT-031's evidence and point OUT-023's cluster-headache sentence to it, or remove the 15-minute time point from both statements.

### R01-10 [missing-requirement] — target: Group E (new requirement, or an addition to OUT-018/OUT-024)
- Problem: no output shows adherence to preventive treatment. Without it, OUT-018 and OUT-024 cannot distinguish non-response from inconsistent intake. A graded recommendation and two sources already cited identify adherence as something to review when judging preventive efficacy.
- Evidence (all verified verbatim):
  - [S-018] "14D. If no efficacy is observed after 8–12 weeks of treatment and other contributing factors are identified (e.g., inconsistent treatment adherence, frequent exposure to known triggers), physicians should engage in shared decision making with patients to continue an additional observation period." (Recommendation 14, Level B, p. 7) — https://www.aan.com/Guidelines/Home/GetGuidelineContent/1180
  - [S-008] "In cases of partial (or no) effectiveness, the adherence to treatment, adequate trial of at least eight weeks at the target dose, and any potential medication overuse should be reviewed." (Q4, Evidence, p. 12) — S-008 URL in section 5.
  - [S-014] "A calendar should be kept by every patient on prophylaxis to assess efficacy and promote adherence." and "Poor adherence is a major factor impairing efficacy of migraine prophylactics; once-daily dosing is associated with better adherence." (section "Prophylactic management of episodic migraine", "Principles of prophylaxis") — https://pmc.ncbi.nlm.nih.gov/articles/PMC6734476/
- Required change: add a SHOULD requirement. For each preventive treatment, the output shows patient-reported adherence to the prescribed preventive regimen over the evaluation window, presented next to the response comparison of OUT-018 (and available to OUT-024 and OUT-034). Suggested Evidence basis: AAN/AHS 2026 14D, Level B; IHS 2024 practice recommendations, consensus; EHF/Lifting The Burden, expert guidance. Describe only the output; do not specify how adherence is recorded or computed.

### R01-11 [missing-requirement] — target: OUT-023
- Problem: OUT-023 says its per-drug outputs exist "so that the EHF definitions of effective attack treatment and triptan response [S-012] can be applied". However, S-012 says that triptan response must be assessed with regard to the timing of the dose, and S-024 recommends reviewing the timing of acute treatment at every visit. OUT-023 has no timing element, so the output cannot show whether an apparent non-response followed a late dose.
- Evidence (verified verbatim):
  - [S-012] "When assessing the response to a triptan, it is also important to ensure prompt dosing, i.e. as close as possible to headache onset or when the pain is still mild (Table S7), as early treatment can enhance the effectiveness of acute drugs." (Results, Consensus, "Definition of triptan-responder")
  - [S-012] "As stated above, the assessment of effectiveness of a triptan should consider early administration." (Results, Consensus, "Definition of triptan failure") — https://pmc.ncbi.nlm.nih.gov/articles/PMC9555163/
  - [S-024] "À chaque visite, il est recommandé de revoir le traitement de crise, à savoir le type de médicament, le nombre de jours de prise (calendrier des maux de tête), la tolérance, la posologie, le moment et la voie d'administration, ainsi que le respect des contre-indications." (p. 401; already quoted in OUT-014). Here "le moment" means "the timing".
- Required change: add to OUT-023, at SHOULD, that for the treated attacks it summarises, the output shows when the acute medication was taken relative to attack onset (or the pain intensity at intake). This makes apparent non-response after late intake visible when the EHF definitions are applied. Cite the S-012 quotes above and S-024, and describe only the output property.

## Notes on frozen items (for the human)
None.
