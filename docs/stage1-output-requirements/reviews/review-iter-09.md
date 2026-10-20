# Review — iteration 09
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v08
Date: 2026-10-20

## Summary
I downloaded all 46 sources again with curl into a new scratch folder and did not reuse earlier agents' files. That includes S-026 (2020), the S-045 landing and listing pages, the S-046 landing page and PubMed abstracts through E-utilities. I matched every quoted string by script, NFKC-, dash- and whitespace-insensitive, with "[...]" segments checked in order. In section 3 that is 213 distinct strings (235 occurrences): evidence quotes, list items, caveat quotes and grade labels. I also matched 53 headings quoted inside locations and 28 source-text strings in section 5. All are verbatim at their URLs.

I also found these correct:
- PDF page offsets, JATS section paths, NICE recommendation numbers and AAN levels;
- the Japanese and Russian grade labels, translations and "[...]" omissions;
- PubMed and Crossref metadata;
- the totals: 39 requirements (10 MUST, 23 SHOULD, 5 MAY, 1 SHOULD NOT); 46 source rows, 45 of them cited.

The v08 changes are verbatim, correctly located and in scope:
- **R08-01 (OUT-023):** the [S-012] definition with its three list items, the [S-004] recommendation 1.3.4.5.1 and comment, and the two Caveat passages from sections 1.3.4.5 and 1.3.4.2. Each Caveat passage is continuous in the source.
- **R08-02 (OUT-016):** the ICHD-3 8.2 note 2 quote on p. 122. ICHD-3's "based on expert opinion" sentence on p. 123 covers all subtypes, so the widened caveat holds.

Both additions name their standards and restate no criteria.

There is one remark. The lead on S-024 Figure 3 is a real defect. OUT-033 calls the French support for HADS a "suggestion", but the SFEMC's own summary figures rate the HAD recommendations "Fort" (strong):
- Rd5 in S-024;
- RT25 (systematic HIT-6 and HAD at every visit) in S-025.

With the evidence basis corrected, MAY understates the support.

## Verification coverage

Counts are distinct quoted strings in section 3 per source: evidence quotes, list items, caveat quotes and grade labels. Headings and section-5 strings are reported below the table.
- "ws" means the string matched only when whitespace was ignored.
- "Manual" means I confirmed the string in the layout text or the raw HTML because the plain text layer is interrupted.

Totals: 194 exact, 7 ws, 6 with printed line numbers stripped, 6 manual.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 15 | 15 (PDF page = printed page). v08 note 2 is on p. 122; 8.2.6 criterion B is on p. 124; "based on expert opinion rather than on formal evidence" is on p. 123. The A1.1 note 3 ("not mandatory for clinical diagnosis") is on p. 190. | 0 | — |
| S-002 | 17 (incl. 3 list items) | 17 (1 ws). PDF page + 1025 = printed page. | 0 | — |
| S-003 | 2 | 2 | 0 | — |
| S-004 | 7 | 7. JATS sections 1.3.2, 1.3.3, 1.3.4.2 and 1.3.4.5 confirmed; recommendation label "1.3.4.5.1." confirmed. | 0 | — (Europe PMC fullTextXML of PMC6501455) |
| S-005 | 7 | 7 (1 manual: the layout text shows "meta-" at a line break) | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 | 0 | — |
| S-008 | 8 | 8 | 0 | — |
| S-009 | 3 | 3 | 0 | — |
| S-010 | 4 | 4 (1 manual: "patient-" at a line break). The abstract quotes are also in the PubMed efetch abstract. | 0 | PubMed web page not used; E-utilities efetch used |
| S-011 | 3 | 3 | 0 | — (Europe PMC fullTextXML) |
| S-012 | 8 (incl. 3 list items) | 8. Results > Consensus > "Definition of effective treatment of a migraine attack", "Definition of triptan-responder" and "Definition of triptan failure" confirmed. | 0 | — (Europe PMC fullTextXML) |
| S-013 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-014 | 12 | 12 | 0 | — (Europe PMC fullTextXML) |
| S-015 | 13 (incl. 2 list items) | 13. Numbers 1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37 and 1.3.48 confirmed; "Last updated: 03 June 2025". | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6); "Revised May 2026" | 0 | — |
| S-017 | 3 | 3. Footer "BASH Guideline V2.0 2026" on both section pages; the TOC page shows "V1.0 2019". | 0 | — |
| S-018 | 8 | 8 (1 manual: "Level C" interrupts 15B). Levels 12A, 14A, 14D, 14E and 15A–15D confirmed in the layout text. | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 | 0 | — |
| S-021 | 3 | 3 | 0 | — |
| S-022 | 6 | 6 (line numbers stripped); stated lines and pp. 11–13 confirmed | 0 | — |
| S-023 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-024 | 6 | 6 (PDF page + 394 = printed page). Figure 3 (p. 402) is image-only; I read it on the embedded image (see R09-01). | 0 | — |
| S-025 | 1 | 1 (PDF p. 2 = p. 413). Figure 1 (p. 414) is image-only; I read it on the embedded image (see R09-01). | 0 | — |
| S-026 | 0 (not cited) | — | — | — (downloaded; superseded entry) |
| S-027 | 6 | 6 | 0 | — |
| S-028 | 1 | 1 | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (6 ws; 1 manual: side tab in CQ II-2-14, PDF p. 207). The CQ I-10 recommendation on PDF p. 48 is followed by "強い推奨/エビデンスの確実性B". | 0 | — |
| S-032 | 3 | 3. Headings 七、治疗 > 病人教育 and 3.2 预防性治疗有效性指标 confirmed. Section 3.2 has no grade, which supports "ungraded text". | 0 | Two connection resets; third attempt succeeded |
| S-033 | 6 (incl. 1 grade label) | 6. The quoted 7.1 sentence (p. 53, grade C/5) is distinct from a similar sentence on p. 39. The 2 English table titles in locations are faithful renderings. | 0 | One reset; retry succeeded |
| S-034 | 4 (incl. 1 grade label) | 4 | 0 | Three resets; fourth attempt succeeded |
| S-035 | 3 | 3 | 0 | — |
| S-036 | 2 | 2 | 0 | — |
| S-037 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-038 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 (manual: present in the raw HTML; "è&nbsp;eliminata" normalises to the quoted text) | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | — (Europe PMC fullTextXML) |
| S-042 | 2 | 2 | 0 | — (Europe PMC fullTextXML) |
| S-043 | 1 | 1 | 0 | — (Europe PMC fullTextXML; efetch abstract) |
| S-044 | 1 | 1 | 0 | Abstract via E-utilities efetch |
| S-045 | 4 | 4 (PDF pp. 113 and 395) | 0 | — |
| S-046 | 3 | 3 (printed p. 5 = PDF p. 8, margin lines as stated) | 0 | — |
| **Total** | **213** | **213** | **0** | — |

Other strings checked:
- **Headings.** 53 headings quoted inside locations: 51 match the source and 2 are faithful English renderings of the S-033 Russian table titles.
- **Section 5.** 28 source-text strings match, including:
  - the S-045 landing-page date string on https://www.sen.es/profesionales/guias-y-protocolos/3843-manual-de-practica-clinica-en-cefaleas-edicion-2026;
  - the S-046 "Draft" label and "Content current as of: 06/01/2023".

  The 2 remaining quoted strings in section 5 are the document's own English translations.

### Checked and not raised
- **The S-024 Figure 3 lead in other requirements.** All ten recommendations Rd1–Rd10 are rated "Fort", including:
  - Rd4 (calendar);
  - Rd6 (HIT-6);
  - Rd8 (M-TOQ at every visit).

  OUT-004 and OUT-026 make no grade claim for SFEMC that contradicts this. OUT-023 calls the SFEMC support "advice" and makes no grade claim; its sentence "neither of which carries a recommendation grade" refers only to EHF and IHS. Only OUT-033 misstates the grade (R09-01).
- **SFEMC acute-treatment part** (Presse Med Form 2022;3:404–411; https://sfemc.fr/wp-content/uploads/2023/02/recommandations-2021-pour-le-diagnostic-et-la-prise-en-ch_2022_la-presse-m-d.pdf; recommendations figure on PDF p. 3, image-only). Each of the following is rated "Fort" in the image:
  - Rt1: "le soulagement complet des céphalées deux heures (ou à défaut un soulagement significatif de la douleur) après la prise du médicament, avec une réponse soutenue pendant 24 heures et sans effets indésirables";
  - Rt5: a calendar reviewed at every visit;
  - Rt11: acute efficacy and tolerance assessed after three attacks;
  - Rt14: triptan resistance only after at least two triptans, each tried on at least three attacks.

  These are consistent with the v08 additions to OUT-023 and with OUT-010 and OUT-014. They would add support but would not change a strength, because SFEMC names no grading system and these requirements already rest on international methodology guidelines. This is an optional addition.
- **AAN/AHS 2026 recommendation 1B (level B):** "Clinicians should offer preventive treatments to patients with migraine who experience ≥4 migraine days per month, or ≥4 moderate to severe headache days per month, to reduce headache frequency." It is not cited in OUT-006. SHOULD remains proportionate, because the document keeps outputs that rest on a level B dimension at SHOULD (OUT-010, OUT-012, OUT-039). This is an optional addition.
- **S-025 Figure 1 RT25/RT26/RT17 ("Fort")** also support OUT-018, OUT-022, OUT-026 and OUT-039:
  - evaluation after the third month, and after 6 months for botulinum toxin A;
  - restarting if attacks increase after stopping;
  - adherence ("l'observance").

  None of these requirements misstates its support, so this is an optional addition.
- **OUT-016 "(see the total across classes in OUT-014)".** It is a pointer, and the code itself defines which classes count for 8.2.6. Spelling that out would restate criteria.
- **Newer editions, none found.** I checked:
  - PubMed 2025–2026 for IHS, EHF and AHS titles: only neuromodulation guidelines, a corrigendum, the EHF sex-specific consensus, the AAN/AHS 2026 parallel publications and AHS position statements on other topics;
  - Japan: the 2021 guideline is still listed as current in June 2026;
  - China: 2022 (the CMA 2023 guideline is already logged as not accessible);
  - sfemc.fr: still the 2021/2022 parts;
  - SEN: the guidelines listing shows no headache document after the 2026 manual except a migraine communication style guide;
  - NICE CG150: 3 June 2025. SIGN 155: May 2026. BASH: V2.0 2026;
  - FDA preventive guidance: still a draft. EMA Rev. 2: still under consultation.
- **Unreachable or nothing new:**
  - AWMF 030-057 (2025-11): Anubis anti-bot page again;
  - Korean, Italian, Czech and Norwegian searches: press reports and review articles only, with no new guideline text containing diary-output statements.

## Remarks

### R09-01 [strength-mismatch] — target: OUT-033 (Rationale, Evidence basis, Evidence, Statement strength); S-024 and S-025 (section 5, "Type and grading")
- **Problem.** OUT-033 describes the French guideline's support for HADS as weak.
  - The Rationale reads "the French guideline suggests HADS as an assessment tool".
  - The Evidence basis reads "National guideline (SFEMC, France, suggestion)". The Strength is MAY.
  - The cited source's own grading marker contradicts this. S-024 says its SFEMC recommendations "sont résumées sur la figure 3", and Figure 3 rates the HAD recommendation (Rd5) "Fort" (strong).
  - The companion SFEMC article on preventive treatment (S-025, already in section 5) rates RT25 "Fort". RT25 requires systematic use of the HIT-6 and HAD scales at every visit.
  - Nothing in S-024's French text presents HAD as a suggestion. The word "suggest" occurs only in the separate English abstract (PMID 34340812). That abstract uses the same verb for the calendar and HIT-6, which the document treats as strong support: OUT-004 lists SFEMC as support for a MUST, and OUT-026 relies on SFEMC HIT-6 ("doit être évalué à chaque visite") for SHOULD.

  The Evidence basis therefore misstates the grade, contrary to PROCESS.md section 3. The strength is also out of line with the document's own calibration:
  - SHOULD for outputs backed by national-guideline recommendations (OUT-017, OUT-022, OUT-026, OUT-027, OUT-034, OUT-035);
  - MAY only where evidence is weak, exploratory, conflicting or scheme-specific (OUT-008, OUT-013, OUT-025, OUT-032).

  RT25 names HIT-6 and HAD in one recommendation. Yet the document makes reporting HIT-6 results SHOULD (OUT-026) and reporting HAD results MAY (OUT-033).
- **Evidence.** All checked on 2026-10-20.
  - **S-024** (https://sfemc.fr/wp-content/uploads/2023/02/recommandations-pour-la-prise-en-charge-de-la-migraine-_2022_la-presse-m-dic.pdf):
    - **p. 401 (PDF p. 7), text layer**, under the heading "Recommandations SFEMC pour le diagnostic et évaluation de la migraine": "Elles sont résumées sur la figure 3." Translation: "They are summarised in figure 3."
    - **p. 402 (PDF p. 8), Figure 3.** The figure is an embedded image of 2006 × 1337 px with no text layer; I read it on the extracted image. Its header is "RECOMMANDATIONS SFEMC POUR LE DIAGNOSTIC ET ÉVALUATION DE LA MIGRAINE" and its strength column is "FORCE DE LA RECOMMANDATION". Row Rd5 reads "Évaluer les comorbidités, et conséquences émotionnelles avec l'échelle HAD.", rated "Fort". Translation: "Assess comorbidities and emotional consequences with the HAD scale."
    - **p. 400 (PDF p. 6), text layer**, section "Facteurs de risque modifiables": "Parmi les facteurs de risque modifiables de la progression de la migraine, la fréquence initiale des crises de migraine, la présence d'une dépression et la surconsommation de médicaments sont les facteurs les plus significatifs, à chercher systématiquement lors de chaque consultation." Translation: "Among the modifiable risk factors for progression of migraine, the initial frequency of migraine attacks, the presence of depression and medication overuse are the most significant factors, to be looked for systematically at every consultation."
  - **S-025** (https://sfemc.fr/wp-content/uploads/2023/02/recommandations-pour-le-diagnostic-et-la-prise-en-charge_2022_traitement-preventif.pdf):
    - **p. 413 (PDF p. 2), text layer:** "L'objectif de cet article est de faire une mise au point sur les recommandations concernant le traitement préventif pharmacologique de la migraine (figure 1)."
    - **p. 414 (PDF p. 3), Figure 1.** The caption in the text layer is "Résumé des recommandations pour la prophylaxie pharmacologique de la migraine". The figure itself is an embedded image of 1864 × 2452 px with no text layer; its strength column is "FORCE".
    - **RT25**, under "POUR ÉVALUER ET ADAPTER LE TRAITEMENT PROPHYLACTIQUE,", rated "Fort": "Évaluer l'efficacité, la tolérance, l'observance et le fardeau de la migraine par un entretien, l'examen du calendrier et l'utilisation systématique des échelles HIT-6 et HAD à chaque visite. L'efficacité de la prophylaxie doit être évaluée après le troisième mois de traitement, sauf pour la toxine botulinique A dont l'efficacité doit être évaluée après 6 mois." Translation: "Assess efficacy, tolerability, adherence and the burden of migraine by interview, review of the calendar and systematic use of the HIT-6 and HAD scales at every visit. The efficacy of prophylaxis must be assessed after the third month of treatment, except for botulinum toxin A, whose efficacy must be assessed after 6 months."
    - **RT15**, rated "Fort": "Déterminer l'éligibilité de chaque patient à une prophylaxie sur la base de la préférence du patient, du journal ou du calendrier des jours de migraine, des critères de migraine sévère et de migraine chronique, des échelles HIT-6 et HAD." Translation: "Determine each patient's eligibility for prophylaxis on the basis of the patient's preference, the diary or calendar of migraine days, the criteria for severe and chronic migraine, and the HIT-6 and HAD scales."
    - **Tableau I**, text layer: S-025 uses the strength scale "Fort", "Modéré" and "Faible" ("Force de la recommandation par la Société française des céphalées") and a "Niveau de preuve de l'efficacité" column.
  - **Grading system.** Neither S-024 nor S-025 names a grading system.
  - **English abstract** (PMID 34340812, via E-utilities efetch), the source of the "suggest" wording:
    - "Migraine-related disability has to be assessed and we suggest to use the 6 questions of the headache impact test (HIT-6)."
    - "We suggest to use a migraine calendar and the Hospital Anxiety and Depression scale (HAD)."
- **Earlier history of this item.** No earlier remark or fix addresses it.
  - OUT-033 and the S-024 and S-025 rows are byte-identical from v00 to v08.
  - Fix-iter-08 read Rd8 "Fort" on Figure 3 for OUT-023, but did not check Rd5 or OUT-033.
  - Review 08 noted that S-024 names no grading system. That is still true, and this remark does not contradict it.
  - The remark reverses no earlier fix, and OUT-033 is not frozen.
- **Required change.**
  1. **OUT-033 Rationale.** Replace "the French guideline suggests HADS as an assessment tool" with an accurate statement. For example: the French guideline (SFEMC) makes a strong recommendation to assess comorbidities and emotional consequences with the HAD scale, and to use the HAD scale systematically at every visit when evaluating preventive treatment.
  2. **OUT-033 Evidence.** Add the [S-024] Rd5 quote with its translation, located as: (Figure 3 "Recommandations SFEMC pour le diagnostic et évaluation de la migraine", Rd5, "Force de la recommandation": "Fort", p. 402; the figure is an image without a text layer). Add [S-025] RT25 as well, with its translation, located as: (Figure 1 "Résumé des recommandations pour la prophylaxie pharmacologique de la migraine", RT25, "Force": "Fort", p. 414; image without a text layer). The first sentence of RT25 is enough for this output; omissions must be marked "[...]". The p. 400 risk-factor sentence may also be quoted.
  3. **OUT-033 Evidence basis.** Replace "National guideline (SFEMC, France, suggestion)" with the grade the source states. For example: "National guideline (SFEMC, France: Rd5 [S-024] and RT25 [S-025], both rated 'Fort' (strong) in the guideline's summary figures; no grading system is named)".
  4. **OUT-033 strength.** Raise the Statement and the Strength line from MAY to SHOULD: "Where results ... are available, the diary output SHOULD report them ...". The corrected support is two strong national-society recommendations that name HAD, one of them for use at every visit, plus the IHS trial-methodology comment. This is the level the document rates SHOULD elsewhere, and it matches OUT-026, where HIT-6 from the same RT25 supports SHOULD. MUST is not supported, because no classification standard, evidence-graded recommendation or international methodology guideline requires the output. The English abstract's "we suggest" is not a reason to keep MAY, because it uses the same verb for HIT-6 and the calendar. The fixer may record it as a wording difference between the language versions.
  5. **Section 5.** In the "Type and grading" of S-024, state that its summary recommendations (Figure 3, p. 402) carry a "Force de la recommandation" (Rd1–Rd10, all "Fort") and that no grading system is named. Make the same addition to S-025: Figure 1 (p. 414) "Force" ("Fort", "Modéré"), Tableau I "Niveau de preuve" and "Force de la recommandation", and no grading system named. This makes the grade cited in OUT-033 traceable.
  6. **Section 7.** Update the totals: 10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT.

  No other Statement needs to change. PHQ-9 and GAD-7 remain examples that no cited source names. The Rationale must not attribute them to a source.

## Notes on frozen items (for the human)
None.
