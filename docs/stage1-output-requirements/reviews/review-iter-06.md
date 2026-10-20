# Review — iteration 06
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v05
Date: 2026-10-20

## Summary
I downloaded all 44 sources again with curl into a new scratch folder and did not reuse earlier agents' files. I extracted every quoted string in v05 by script and matched it against the downloaded text. Matching was NFKC-, dash- and whitespace-insensitive, and quotes with "[...]" were checked segment by segment, in order. That covers 202 strings: 194 distinct evidence and caveat quotes including list items, 4 grade labels, and 4 source-text quotes in the S-028, S-032 and S-036 entries. All 202 are verbatim at their URLs.

I also checked the following and found them correct:
- every PDF quote's page, using page splits and each source's page offset;
- every XML quote's section, using the JATS section path;
- every heading quoted inside a location;
- every NICE recommendation number, every AAN level, the SIGN strong-recommendation wording, and the Japanese and Russian grade labels;
- every "[...]" omission and every translation;
- bibliographic metadata, against PubMed esummary and the documents' title pages;
- the totals: 39 requirements (10 MUST, 23 SHOULD, 5 MAY, 1 SHOULD NOT) and 44 sources, all cited.

The v05 change (R05-01: "Definitions of terms" at nine places, and the OUT-013 location) is correct and introduced no defect. I found no scope violation, contradiction or duplication.

The one remark is about an outdated source. The 5th edition (2026) of the Spanish SEN headache manual is now online and supersedes S-026 (2020). In that edition, the diary recommendation quoted in OUT-014 no longer carries a grade. The edition also states that MIDAS and HIT-6 are not recommended for judging preventive efficacy, which reverses the S-026 passage quoted in OUT-026 (R06-01).

## Verification coverage

Counts are distinct quoted strings per source, including list items, grade labels and section-5 source quotes. "ws" means the string matched only when whitespace or line-break hyphens were ignored. "Manual" means I confirmed the string on the page, in a layout extraction or on a render, because the text layer is interrupted. Script totals: 169 exact, 15 ws (plus the 8 grade-label and section-5 strings, matched ws-insensitively), 10 manual.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 14 | 14. The v05 heading "Definitions of terms" was confirmed on PDF pp. 4 and 209; the singular form occurs nowhere. The v05 OUT-013 location was confirmed on p. 21. The OUT-030 caveat ("not mandatory for clinical diagnosis") was confirmed in the A1.1 notes, p. 190. | 0 | — |
| S-002 | 16 (incl. 3 list items) | 16 (1 ws); sections 1, 1.1.4, 1.1.9, 1.3.1, 1.3.2.0–1.3.2.6.3 and 1.3.4 confirmed | 0 | — |
| S-003 | 2 | 2 | 0 | — |
| S-004 | 3 | 3 | 0 | — (Europe PMC fullTextXML of PMC6501455) |
| S-005 | 7 | 7 (1 manual: pdftotext drops the line-break hyphen in "meta-analyses"; the layout text shows "meta-") | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 | 0 | — |
| S-008 | 8 | 8; Q2, Q4, Q6 and Q7 headings and the "Optimal" labels confirmed | 0 | — |
| S-009 | 3 | 3; Q12 "Optimal" confirmed | 0 | — |
| S-010 | 4 | 4 (1 manual: "patient-reported" split at a line break); abstract quotes also matched in the PubMed efetch abstract | 0 | PubMed web page not used; E-utilities efetch used |
| S-011 | 3 | 3 | 0 | — (Europe PMC fullTextXML) |
| S-012 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-013 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-014 | 12 | 12 | 0 | — (Europe PMC fullTextXML) |
| S-015 | 13 (incl. 2 list items) | 13; recommendation numbers 1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37 and 1.3.48 confirmed; "Last updated: 03 June 2025" | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6); "Revised May 2026" | 0 | First connection reset; retry succeeded |
| S-017 | 3 | 3; footer "BASH Guideline V2.0 2026" and dateModified 2026-09-14 confirmed | 0 | — |
| S-018 | 8 | 8 (1 manual: "Level C" interrupts 15B); levels of 12A, 14A, 14D, 14E and 15A–D confirmed in the layout text | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 | 0 | — |
| S-021 | 3 | 3 (Page 5/12 and 6/12) | 0 | — |
| S-022 | 6 | 6 (all manual, with line numbers stripped by script; lines 383–384, 393–394, 421–425, 427–429 and 464–465 and pp. 11–13 confirmed) | 0 | — |
| S-023 | 4 | 4; "Frage 3, final paragraph" and "Hintergrund" confirmed in the JATS tree | 0 | — (Europe PMC fullTextXML) |
| S-024 | 6 | 6 (PDF page + 394 = printed page) | 0 | — |
| S-025 | 1 | 1 | 0 | — |
| S-026 | 2 | 2 in the 2020 edition at the cited URL. Neither string occurs in the 2026 edition (see R06-01). | 0 | — |
| S-027 | 6 | 6; sub-headings (Overwegingen, Waarden en voorkeuren van patiënten, Rationale van de aanbeveling) confirmed | 0 | — |
| S-028 | 2 (incl. 1 in section 5) | 2 | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4; sections 2.4, 3.3 and 3.5.2 confirmed on PDF pp. 12, 16 and 19 | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (1 manual: the side tab interrupts CQ II-2-14, PDF p. 207 = printed p. 191) | 0 | — |
| S-032 | 5 (3 evidence quotes; 2 in section 5) + 1 heading | 6 | 0 | First two attempts reset by peer; third succeeded |
| S-033 | 6 (incl. 1 grade label) | 6; grades of 2.5 and 7.1 confirmed; tables 3в and 4а confirmed | 0 | — |
| S-034 | 4 (incl. 1 grade label) | 4 | 0 | First attempt reset; retry succeeded |
| S-035 | 3 | 3 | 0 | — |
| S-036 | 3 (incl. 1 in section 5) | 3 | 0 | — |
| S-037 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-038 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-042 | 2 | 2 | 0 | — (Europe PMC fullTextXML) |
| S-043 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-044 | 1 | 1 | 0 | Abstract via E-utilities efetch |
| **Total** | **202** | **202** | **0** | — |

### Checked and not raised
- **Newer editions, checked with no supersession found:**
  - PubMed (2023–2026) shows no new edition of S-002 to S-007, S-011 or S-014. The new IHS trial guidelines cover post-traumatic headache and IIH.
  - SFEMC (sfemc.fr/recommandations) still lists the 2021/2022 migraine guidelines (S-024, S-025).
  - DHOS (dhos.dk/referenceprogram) still lists the 2020 programme (S-030).
  - Japan: 2021 is still the latest edition (S-031).
  - China: the 2022 professional edition is current; the 2025 publication is a patient version (S-032).
  - Russia: the apicr API returns byte-identical files for 295_6 and 169_4 (S-033, S-034).
  - No newer Polish, Brazilian or DMKG documents were found.
- **IHS paediatric update 2023 (PMID 37226450).** It is still not readable: SAGE returns 403 (Unpaywall's "OA" link is that same 403), the DuEPublico record is behind a security-check page, and the Pavia record is the 2019 edition. The abstract does not show a change to the S-005 statements used.
- **German S1 guideline 030-057 (2025-11).** register.awmf.org still serves the Anubis anti-bot page. The dgbfb.de file is a one-page summary.
- **Portuguese consensus 2025 (Acta Med Port, PMID 40359119).** The publisher returns a Cloudflare 403. The abstract describes a primary-care consensus, not a replacement for S-036.
- **Searches with no new evidence-based output requirement:**
  - Austrian (ÖKSG): only the co-authored S-023.
  - Korean: press reports only; no guideline full text.
  - Thai: no national guideline text.
  - Italian (SISC/ANIRCEF): only press reports of the 2025 SISC-IHS guideline, which an earlier review read with no diary-output statement.
- **AAN/AHS 2026 recommendations not quoted.**
  - 14B (24 weeks for onabotulinumtoxinA) is consistent with OUT-018's "after onabotulinumtoxinA cycles".
  - 14C, 16A/16B and 17A/17B address clinician actions, not diary outputs.
  - Review 05 already recorded this.
- **OUT-016 subtype list.** The ICHD-3 numbering (8.2.6 "multiple drug classes not individually overused", 8.2.7 "unspecified or unverified", 8.2.8 "other medication") matches the "8.2.1–8.2.6 and 8.2.8" in the Statement.

## Remarks

### R06-01 [outdated-source] — target: S-026 (section 5); OUT-014; OUT-026; section 6 (Spanish row)
- **Problem.** S-026 cites the 4th edition (2020) of the SEN "Manual de Práctica Clínica en Cefaleas". The SEN has published a 5th edition, "Recomendaciones diagnóstico-terapéuticas de la SEN 2026", which supersedes it. The SEN guidelines page lists it as "Documento PDF incluido en la web de la SEN el 21 de enero de 2026". The 2026 methodology says the 2020–2024 literature "ha complementado o sustituido a la que figuraba en la bibliografía del manual de 2020". PROCESS.md section 3 requires the most recent version, and requires the evidence basis to say when evidence conflicts. The newer edition changes what the document states for two requirements:
  - **(a) OUT-014.** The 2020 quote ends "(nivel de evidencia II, grado de recomendación B)", and OUT-014's Evidence basis lists "SEN, grade B" among the graded guideline recommendations. In the 2026 edition the same sentence carries no level of evidence and no grade.
  - **(b) OUT-026.** The 2020 passage "Recomendamos usar calendarios, escalas como HIT-6, MIDAS o de calidad de vida para valorar la eficacia de forma objetiva" is not in the 2026 edition. The 2026 edition says the opposite: MIDAS and HIT-6 are not recommended for assessing the efficacy of preventive treatment in clinical practice, and PGIC is recommended as a complementary tool. OUT-026 still lists "SEN, Spain" as support. Its rationale ("several guidelines name MIDAS and HIT-6 as success criteria alongside frequency") and its Evidence basis do not record the conflict.
  - **(c) Search log, Spanish row.** It says "A newer edition is reported in the press but was not found on the SEN site; not verified." That is no longer accurate.
- **Evidence.** All quotes below were verified verbatim by script in the pdftotext output of https://www.sen.es/pdf/2026/Manual_Cefaleas_2026.pdf (HTTP 200, 612 pages, downloaded 2026-10-20). The page layouts were checked on renders. Printed page = PDF page − 2.
  - **Landing pages.** https://www.sen.es/profesionales/guias-y-protocolos/3843-manual-de-practica-clinica-en-cefaleas-edicion-2026 ("Manual de Práctica Clínica en Cefaleas. EDICIÓN 2026"), and the listing at https://www.sen.es/profesionales/guias-y-protocolos.
  - **Edition and citation.**
    - PDF p. 4: "Título original: Manual de Práctica Clínica en Cefaleas. Recomendaciones diagnóstico-terapéuticas de la SEN 2026. ISBN papel: 979-13-87731-63-2. ISBN digital: 979-13-87731-64-9"; publisher "Editorial UFV Universidad Francisco de Vitoria"; "© 2026, Sociedad Española de Neurología".
    - PDF p. 3: editors Robert Belvís Nieto and Pablo Irimia Sieira.
    - PDF p. 11 (Introducción): "Presentamos la quinta edición del Manual de Práctica Clínica en Cefaleas de la Sociedad Española de Neurología (SEN)".
  - **Grading system** (Metodología, PDF pp. 15–17).
    - Levels of evidence NE-I to NE-IV (Tabla 1).
    - Grades of recommendation A, B, C and D (Tablas 2 and 3). Grade D is "una recomendación de consenso por parte de los autores y coordinadores del manual".
    - The running text also uses "GR-GECSEN".
  - **For OUT-014.** Chapter 11 "Otras cefaleas secundarias", 5.4 "Cefalea por uso excesivo de medicación", 5.4.7.1 "Educación y otras terapias", PDF p. 395 (printed p. 393):
    - Quote: "Debe promoverse el uso de diarios para monitorizar su cefalea y el uso de medicación."
    - Translation: "The use of diaries to monitor their headache and medication use should be promoted."
    - No NE or GR label is attached to this sentence. No NE or GR label occurs anywhere on PDF pp. 393–397.
  - **For OUT-026.** Chapter 4 "Tratamiento preventivo de la migraña", section 4 "Criterios de eficacia del tratamiento preventivo", PDF p. 113 (printed p. 111). The first two quotes are in the shaded box headed "El tratamiento preventivo se considera eficaz cuando:".
    - "Las escalas MIDAS y HIT-6 no se recomiendan para evaluar la eficacia del tratamiento preventivo en la práctica clínica." Translation: "The MIDAS and HIT-6 scales are not recommended for assessing the efficacy of preventive treatment in clinical practice."
    - "La escala PGIC es una herramienta complementaria recomendada para evaluar la eficacia del tratamiento preventivo, ya que refleja la percepción subjetiva del paciente y su impacto en la calidad de vida." Translation: "The PGIC scale is a recommended complementary tool for assessing the efficacy of preventive treatment, because it reflects the patient's subjective perception and its impact on quality of life."
    - In the running text above the box: "El cambio en las puntuaciones de los cuestionarios MIDAS y HIT-6 puede proporcionar información adicional sobre el impacto del fármaco preventivo en la discapacidad y la calidad de vida, pero no es imprescindible para valorar la eficacia del tratamiento." Translation: "The change in MIDAS and HIT-6 questionnaire scores can provide additional information on the impact of the preventive drug on disability and quality of life, but it is not essential for assessing treatment efficacy."
  - **2020 strings.** A whitespace-insensitive search finds neither 2020 string quoted in OUT-014 (with its grade) or OUT-026 in the 2026 text, and the row label "Evaluación objetiva" does not occur in it.
- **Earlier history of this item.** No remark or fix has addressed it.
  - Review 01 noted a press report of the 5th edition but obtained no copy. Reviews 03 and 04 found only the 2020 manual on the SEN site.
  - The S-026 entry, OUT-014 and the Spanish search-log row have been unchanged since v00.
  - OUT-026 changed only in v01 (R01-02, the S-041 location), not in its S-026 quote or its Evidence basis.
  - The remark reverses no earlier fix.
- **Required change.**
  1. **Section 5.** Cite the 2026 (5th) edition. Either update S-026 to it, stating that it supersedes the 2020 4th edition, or add a new source ID for it and mark S-026 as superseded. Do not renumber. The entry should give:
     - **Citation:** Belvís Nieto R, Irimia Sieira P (eds). Manual de Práctica Clínica en Cefaleas. Recomendaciones diagnóstico-terapéuticas de la SEN 2026. Pozuelo de Alarcón (Madrid): Editorial UFV; 2026. ISBN 979-13-87731-64-9 (digital).
     - **Type:** "Clinical practice guideline (national society; levels of evidence NE-I–NE-IV and grades of recommendation A–D, Tablas 1–3; GR-GECSEN used in the text)".
     - **URL:** https://www.sen.es/pdf/2026/Manual_Cefaleas_2026.pdf, with the page note "printed page = PDF page − 2" and the access date.
  2. **OUT-014.** Replace the 2020 quote with the 2026 sentence above, located as given. In the Evidence basis, remove "SEN, grade B" from the graded guideline recommendations and list SEN 2026 as an ungraded national-guideline statement. The MUST strength is unaffected; it rests on ICHD-3, AAN/AHS 2026 15D (level B) and Japan CQ I-10 (strong, certainty B).
  3. **OUT-026.**
     - Remove the 2020 "Evaluación objetiva" quote, and remove "SEN, Spain" from the national guidelines cited as supporting MIDAS/HIT-6 use.
     - State in the Evidence basis, and in the rationale sentence about MIDAS and HIT-6 as success criteria, that the evidence conflicts. Quote the 2026 MIDAS/HIT-6 sentence for this.
     - The 2026 PGIC sentence may be cited in support of the PGIC element.
     - The Statement (report results where available) and SHOULD remain supportable by AAN/AHS 15B (level C), SFEMC, SPC, Japan and IHS. Whatever strength the fixer keeps, the conflict must be stated.
  4. **Section 6, Spanish row.** Replace "not found on the SEN site; not verified" with a record that the 2026 (5th) edition was found at the URL above and used.

## Notes on frozen items (for the human)
None.
