# Review — iteration 03
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v02
Date: 2026-10-20

## Summary
I downloaded all 44 sources again with curl into a new scratch directory; I did not reuse any earlier agent's files. I extracted every quoted string from v02 by script and matched each one against the downloaded text (NFKC-, whitespace- and dash-insensitive; quotes with "[...]" were checked segment by segment and in order). That gives 203 distinct strings in 225 occurrences:
- 186 evidence quotes;
- 4 caveat quotes;
- 5 list items;
- 4 grade labels;
- 3 source-text quotes and 1 quoted section heading in the S-028 and S-032 entries of section 5.

All 203 are verbatim at their URLs:
- 193 matched by exact script;
- 2 matched by script once line-break hyphens were ignored (S-005, S-010);
- 8 I confirmed by hand: the 6 S-022 quotes (line numbers break the text), S-018 15B (margin label "Level C") and S-031 CQ II-2-14 (chapter side tab).

I checked every PDF quote's page against the page splits and every XML quote's section against the XML section titles. I also checked every "[...]" omission against the full sentence and every translation. I checked bibliographic metadata against PubMed esummary and the documents' title pages.

The v02 changes for R02-01 and R02-02 are correct and introduced no defect:
- The new [S-032], [S-042] and [S-010] quotes are verbatim and correctly located.
- The [S-032] omissions keep the meaning, because the source says any one criterion suffices.
- The relocated [S-035] quote sits in the bulleted list below the framed Kutu 8 box on PDF p. 48. I confirmed this on a page render.
- The Saudi panel's final list of success parameters indeed omits acute-treatment response.
- The totals reproduce under the stated rule.

I found no scope violation, contradiction or ID or total inconsistency. One metadata defect remains: S-036's grading system is not named (R03-01).

Checked and not raised:
- **Canadian Headache Society guidelines.** The 2012 prophylaxis guideline and the 2013 acute guideline are English sources that the search log does not list. They contain no output that the document lacks. The 2012 guideline calls a better response to acute medication under prophylaxis "anecdotal" and cites one negative topiramate–triptan study. OUT-021 and OUT-023 already state that their support for this component is ungraded. The requirement only asks that any change be visible, so this does not alter it.
- **Italian GP/specialist Delphi consensus 2026** (Neurol Sci, PMC13183690). Its diary statements concern what is recorded, such as blood pressure and contraceptive days, which is out of scope.
- **Mexican IMSS-047-08 guideline (2016).** It has no diary-output statement.
- **Other sources with no new output.** The IHS HTA position statement 2021, the AHS telemedicine position statement 2026 and Korean press reports of the KHS guideline add nothing new. The KHS guideline recommends diaries for efficacy, adverse effects and adherence, which OUT-018, OUT-024 and OUT-039 already cover.
- **S-043 correction** (PMC13217784). It only adds a competing-interest sentence.
- **No newer editions** of S-011 (EHF), S-026 (the SEN site still lists the 2020 manual) or S-030 (the DHOS site still lists 2020) were found.
- **S-030 type label.** S-030 is typed "consensus-based". The programme itself (section 1.3, PDF p. 7) says that comprehensive evidence assessments underlie the recommended treatment and that evidence levels were deliberately omitted. No requirement's strength depends on this label, so I did not raise it.

## Verification coverage

Counts are distinct quoted strings per source, including list items, grade labels and section-5 quotes. "Manual" means the script failed because of a text-layer artefact and I confirmed the quote by reading the page or a layout extraction.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 14 | 14 | 0 | — |
| S-002 | 17 (incl. 3 list items) | 17 | 0 | — |
| S-003 | 2 | 2 | 0 | — |
| S-004 | 3 | 3 | 0 | — (Europe PMC fullTextXML) |
| S-005 | 7 | 7 (1 line-break hyphen) | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 | 0 | — |
| S-008 | 8 | 8 | 0 | — |
| S-009 | 3 | 3 | 0 | — |
| S-010 | 4 (1 new in v02) | 4 (1 line-break hyphen); abstract quotes also matched in the PubMed efetch abstract | 0 | PubMed web page not used (challenge to curl); E-utilities efetch used |
| S-011 | 3 | 3 | 0 | — (Europe PMC fullTextXML) |
| S-012 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-013 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-014 | 12 | 12 | 0 | — (Europe PMC fullTextXML) |
| S-015 | 13 (incl. 2 list items) | 13 | 0 | — |
| S-016 | 9 | 9 | 0 | — |
| S-017 | 3 | 3 (footer "BASH Guideline V2.0 2026", `dateModified` 2026-09-14 confirmed) | 0 | — |
| S-018 | 8 | 8 (1 manual: 15B interrupted by "Level C") | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 | 0 | — |
| S-021 | 3 | 3 | 0 | — |
| S-022 | 6 | 6 (all manual: lines 383–384, 393–394, 421–425, 427–429, 464–465 and their pages confirmed in a layout extraction) | 0 | — |
| S-023 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-024 | 6 | 6 | 0 | — |
| S-025 | 1 | 1 | 0 | — |
| S-026 | 2 | 2 | 0 | — |
| S-027 | 6 | 6 | 0 | — |
| S-028 | 2 (incl. 1 in section 5) | 2 | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (1 manual: side tab in CQ II-2-14, PDF p. 207 = printed p. 191) | 0 | — |
| S-032 | 6 (3 evidence quotes, 1 new in v02; 2 quotes and 1 section heading in section 5) | 6 | 0 | — |
| S-033 | 6 (incl. 1 grade label) | 6 | 0 | first connection reset; retry succeeded |
| S-034 | 4 (incl. 1 grade label) | 4 | 0 | — |
| S-035 | 3 | 3 (location of the relocated quote checked on a page render) | 0 | — |
| S-036 | 2 | 2 | 0 | — |
| S-037 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-038 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-042 | 2 (1 new in v02) | 2 | 0 | — (Europe PMC fullTextXML) |
| S-043 | 1 | 1 | 0 | — (Europe PMC fullTextXML; abstract also via efetch) |
| S-044 | 1 | 1 | 0 | PubMed web page not used; abstract via E-utilities efetch |
| **Total** | **203** | **203** (193 exact script, 2 script ignoring line-break hyphens, 8 manual) | **0** | — |

### Completeness search (beyond the document's sources)
- **AWMF S1 030-057 (2025-11).** The register still serves the Anubis anti-bot page. Only a 2019 copy exists elsewhere (Uniklinikum Dresden), and it is superseded.
- **NHG-Standaard Hoofdpijn.** Still returns HTTP 401.
- **IHS paediatric update 2023 (PMID 37226450).** Unpaywall lists only the SAGE copy, which returns 403. The Pavia repository holds only the 2019 edition. The abstract shows the update concerns classification, attack duration, age groups, e-diaries, outcome measures, interim analysis and placebo response.
- **Searched with no new output found:**
  - Canada: CHS 2012 and 2013 (e-lactancia copies).
  - Italy: the 2026 Delphi consensus.
  - Mexico: IMSS GPC 2016.
  - Korea: press reports only; no full text found.
  - Greece: the Hellenic Headache Society paper is behind a Springer challenge and is in English.
  - PubMed: recent EHF, EAN and AHS publications, including the AHS telemedicine statement 2026 (PMC12951699) and a 2026 systematic review of paediatric guidelines (abstract only).

## Remarks

### R03-01 [link/citation] — target: S-036 (section 5, "Type and grading"; source used in OUT-026, OUT-027)
- **Problem.** PROCESS.md section 3 requires each clinical practice guideline's entry to name its grading system. S-036 is typed "Clinical practice guideline (national society; grades of recommendation)", which names no system. The guideline itself states that it uses the grades of recommendation and levels of evidence adopted by the Portuguese Direção-Geral da Saúde, and it defines them in Tables 1.1 and 1.2. This is the same defect that R01-03 corrected for S-028 and S-032.
- **Evidence.** All quotes below were verified verbatim at https://old.sinapse.pt/edition_download.php?id=67, section "1. Introdução", PDF p. 7 (printed p. 5):
  - Statement of the system: "Abordaremos o tratamento farmacológico das várias entidades considerando os níveis de evidência e os graus de recomendação adotados pela Direção Geral de Saúde (Tabelas 1.1 e 1.2)." Translation: "We will address the pharmacological treatment of the various entities considering the levels of evidence and the grades of recommendation adopted by the Directorate-General of Health (Tables 1.1 and 1.2)."
  - Table 1.1 defines the grades "Grau I", "Grau II", "Grau IIa", "Grau IIb" and "Grau III".
  - Table 1.2 defines the levels "Nível A", "Nível B" and "Nível C".
- **Earlier history of this item.** None. S-036's entry has not changed since v00, and no earlier remark or fix touched it. R01-03 is the precedent for the same defect type.
- **Required change.** In section 5, change S-036's "Type and grading" to name the system, for example: "Clinical practice guideline (national society; grades of recommendation I, IIa, IIb, III and levels of evidence A–C as adopted by the Direção-Geral da Saúde, Tables 1.1 and 1.2, PDF p. 7)". You may quote the source sentence with its translation, as the S-028 and S-032 entries do. No requirement text needs to change: the S-036 passages quoted in OUT-026 and OUT-027 carry no grade, and their evidence-basis lines claim none.

## Notes on frozen items (for the human)
None.
