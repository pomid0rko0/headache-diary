# Review — iteration 05
VERDICT: REMARKS
REMARK_COUNT: 1
Reviewed version: v04
Date: 2026-10-20

## Summary
I downloaded all 44 sources again with curl into a new scratch folder and did not reuse earlier agents' files. I extracted every quoted string in v04 by script and matched it against the downloaded text (NFKC-, dash- and whitespace-insensitive; quotes with "[...]" checked segment by segment, in order). That covers 202 strings: 194 distinct evidence and caveat quotes including list items (216 occurrences), 4 grade labels, and 4 source-text quotes in the S-028, S-032 and S-036 entries. All 202 are verbatim at their URLs.

I also checked the following and found them correct:
- every PDF quote's page (page splits plus each source's page offset);
- every XML quote's section (JATS section path);
- every NICE recommendation number and every AAN level (on a page render);
- every "[...]" omission and every translation;
- bibliographic metadata against PubMed esummary, Crossref and the documents' title pages;
- the RFC 2119 totals (39 requirements: 10 MUST, 23 SHOULD, 5 MAY, 1 SHOULD NOT; 44 sources, all cited).

The two v04 changes (R04-01: OUT-003 location of the S-013 quote; R04-02: OUT-027 evidence basis) are correct and introduced no defect. I found no scope violation, contradiction or duplication.

I also checked the section names quoted inside locations and statements. One location defect has been present since v00: ICHD-3's glossary heading is cited nine times as "Definition of terms", but the source reads "Definitions of terms". In the same source, one location says "end of comments" for a sentence that is mid-way through the comments (R05-01).

My own search in English, German, Swedish, Hungarian, Spanish, Czech and Chinese found no missing output requirement that has verifiable evidence (see "Checked and not raised" below).

## Verification coverage

Counts are distinct quoted strings per source, including list items, grade labels and section-5 source quotes. "ws" means the string matched only when whitespace or line-break hyphens were ignored; I inspected each such case. "Manual" means I confirmed the string on the page, in a layout extraction or on a render because the text layer is interrupted.

| Source ID | Quotes checked | Verified verbatim | Not found | Unreachable (what you tried) |
|---|---|---|---|---|
| S-001 | 14 | 14 (locations: see R05-01) | 0 | — |
| S-002 | 16 (incl. 3 list items) | 16 (1 ws: "moderate/ severe") | 0 | — |
| S-003 | 2 | 2 | 0 | — |
| S-004 | 3 | 3 | 0 | — (Europe PMC fullTextXML of PMC6501455) |
| S-005 | 7 | 7 (1 ws: line-break hyphen in "meta-analyses") | 0 | — |
| S-006 | 4 | 4 | 0 | — |
| S-007 | 4 | 4 | 0 | — |
| S-008 | 8 | 8 | 0 | — |
| S-009 | 3 | 3 | 0 | — |
| S-010 | 4 | 4 (1 ws); both abstract quotes also exact in the PubMed efetch abstract | 0 | PubMed web page not used; E-utilities efetch used |
| S-011 | 3 | 3 | 0 | — (Europe PMC fullTextXML) |
| S-012 | 4 | 4 | 0 | — (Europe PMC fullTextXML) |
| S-013 | 4 | 4; the v04 location (third paragraph after Table 3 in Results) confirmed in the XML | 0 | — (Europe PMC fullTextXML) |
| S-014 | 12 | 12 | 0 | — (Europe PMC fullTextXML) |
| S-015 | 13 (incl. 2 list items) | 13; recommendation numbers 1.2.6, 1.2.7, 1.3.1, 1.3.24, 1.3.27–1.3.29, 1.3.37 and 1.3.48 confirmed; "Last updated: 03 June" 2025 | 0 | — |
| S-016 | 9 | 9 (PDF page = printed page + 6); "R" for 5 confirmed as a strong ("should") recommendation; 7.3 checklist "based on their experience" confirmed | 0 | First download reset by peer; retry succeeded |
| S-017 | 3 | 3, all on the 2.1.3 page (sections B and E); footer "BASH Guideline V2.0 2026" and dateModified 2026-09-14 on both pages | 0 | — |
| S-018 | 8 | 8 (1 manual: 15B interrupted by "Level C"); levels of 12A, 14A, 14D, 14E, 15A–15D confirmed on a render of pp. 7–8 | 0 | — |
| S-019 | 2 | 2 | 0 | — |
| S-020 | 2 | 2 (printed p. 4 = PDF p. 7) | 0 | — |
| S-021 | 3 | 3; CPMP/EWP/788/01 Rev. 1, 24 January 2007, in effect 31 July 2007 confirmed | 0 | — |
| S-022 | 6 | 6 (all manual: lines 383–384, 393–394, 421–425, 427–429, 464–465 and pp. 11–13 confirmed in the layout text) | 0 | — |
| S-023 | 4 | 4 ("Frage 3" final paragraph confirmed) | 0 | — (Europe PMC fullTextXML) |
| S-024 | 6 | 6 (PDF page + 394 = printed page) | 0 | — |
| S-025 | 1 | 1 | 0 | — |
| S-026 | 2 | 2 | 0 | — |
| S-027 | 6 | 6 | 0 | — |
| S-028 | 2 (incl. 1 in section 5) | 2 | 0 | — |
| S-029 | 2 | 2 | 0 | — |
| S-030 | 4 | 4 | 0 | — |
| S-031 | 9 (incl. 2 grade labels) | 9 (6 ws: line breaks inside Japanese sentences; 1 manual: side tab in CQ II-2-14, PDF p. 207 = printed p. 191); CQ labels I-4, I-10, II-1-6, II-1-12, II-2-14, VI-3 confirmed | 0 | — |
| S-032 | 5 (3 evidence quotes; 2 in section 5) | 5; section headings "预防性治疗有效性指标" and "证据的检索、评价与分级" present | 0 | Two resets by peer, then success on retry |
| S-033 | 6 (incl. 1 grade label) | 6; grade C/5 of sections 2.5 and 7.1, tables 3в and 4а confirmed | 0 | — |
| S-034 | 4 (incl. 1 grade label) | 4; title page (image) rendered: "Год утверждения 2024", developers as cited | 0 | Two resets by peer, then success |
| S-035 | 3 | 3; Kutu 8 / bullet list (PDF p. 48) and Algoritma 13 (PDF p. 78) confirmed | 0 | — |
| S-036 | 3 (incl. 1 in section 5) | 3 | 0 | — |
| S-037 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-038 | 1 | 1 | 0 | — (Europe PMC fullTextXML) |
| S-039 | 2 | 2 | 0 | — |
| S-040 | 2 | 2 | 0 | — |
| S-041 | 1 | 1 ("Conclusion") | 0 | — (Europe PMC fullTextXML) |
| S-042 | 2 | 2 | 0 | — (Europe PMC fullTextXML) |
| S-043 | 1 | 1 | 0 | — (Europe PMC fullTextXML; abstract also via efetch) |
| S-044 | 1 | 1 | 0 | Abstract via E-utilities efetch |
| **Total** | **202** | **202** (177 exact; 17 ws, including the 8 grade-label and section-5 strings; 8 manual) | **0** | — |

### Checked and not raised
- **VA/DoD Clinical Practice Guideline for the Management of Headache (2023), not in the search log.** Full PDF from healthquality.va.gov. It lists the diary only as an assessment tool and reprints the ICHD-3 notes. None of its recommendations concerns diary outputs.
- **German DGN S1 guideline on medication overuse and MOH (Diener et al., Neurol Res Pract 2022, PMC9422154), not in the search log.** It says: "In the months thereafter, a headache diary should be kept to decide whether prophylactic drug therapy is necessary". It also bases the MOH diagnosis on "days of headache medication use documented in a headache diary". OUT-014, OUT-016 and OUT-017 already cover both.
- **German S1 guideline 030-057.** register.awmf.org still serves the Anubis page. dmkg.de hosts only a two-page topiramate amendment dated 4 January 2024.
- **Swedish national guideline, available at an official copy the search log does not list.** The log says the Swedish national knowledge support could not be accessed. "Riktlinje för migrän" (NPO Nervsystemets sjukdomar, decided 2022-10-25) can be read at https://vardpersonal.1177.se/globalassets/nkk/nationell/media/dokument/kunskapsstod/vardriktlinjer/riktlinje-for-migran.pdf. Its diary statements are already covered:
  - evaluation every 3–6 months, a 50% reduction in migraine days, intensity, work ability and quality of life (OUT-018, OUT-010, OUT-027);
  - CGRP stop criteria that include sick-leave days (OUT-025, OUT-027);
  - a diary "helst webbaserad och åtkomlig även från journalsystemen" (OUT-034, which asks for a shareable summary);
  - PROMs: HIT-6, MIDAS, HADS, PSS-14 (OUT-026, OUT-033).

  The author may add this copy to the search log, but it changes no requirement.
- **Hungarian joint guideline on CGRP therapies (Orv Hetil 2025;166(50):1963–1974), full text from akjournals.com.** It recommends a diary before starting, a first evaluation after at least 3 months based on headache days, acute medication use and quality of life, and a repeat at month 6. OUT-018 and OUT-021 already cover this.
- **Other 2024–2026 guidance with no new output:**
  - Headache Society of Singapore consensus (PMC13405573);
  - updated Canadian Headache Society prevention guideline (Can J Neurol Sci 2024, doi 10.1017/cjn.2024.285). Its expert guidance on diaries, the 50% criterion, MIDAS/HIT-6 and evaluation after 3 months (CGRP mAbs) or after 2–3 cycles (onabotulinumtoxinA) is consistent with OUT-018 and OUT-026;
  - Ibero-American consensus (Neurology Perspectives 2025);
  - international Delphi on refractory migraine (Robblee et al., Cephalalgia 2025; copy at ricerca.univaq.it). It has no diary statement and does not replace S-013.
- **AAN/AHS 2026 recommendations not quoted in the document:** 14B (24 weeks for onabotulinumtoxinA, level B), 16B (monitor adverse effects, level A) and 17A/17B (stopping). They support OUT-018, OUT-024 and OUT-022, and none requires a strength change, because they address clinician actions, not diary outputs.
- **Unreachable:**
  - BASH 2026 consensus on advanced preventive treatments (J Neurol Neurosurg Psychiatry, PMID 42469019): BMJ and the Birmingham repository copy both return a Cloudflare 403;
  - Taiwan 2026 acute guideline (PMID 42723131): closed access on Ovid;
  - NHG-Standaard: still HTTP 401;
  - Czech CGRP recommendations on csnn.eu: still behind a declaration page;
  - the BASH guideline PDF: still 404.
- **S-032 DOI.** The DOI 10.3969/j.issn.1006-9852.2022.12.001 resolves to Wanfang, but the landing page returns HTTP 500. I could not confirm that the DOI belongs to S-032, so "DOI not verified" remains accurate.

## Remarks

### R05-01 [link/citation] — target: OUT-001, OUT-002, OUT-004, OUT-007, OUT-031 (S-001 heading "Definition of terms"); OUT-013 (S-001 location "end of comments")
- Problem: two S-001 location labels do not match the source. PROCESS.md section 3 requires the location in the source, and section 2 says not to alter quoted text. R01-02 and R04-01 corrected wrong section labels as defects.
  - (a) ICHD-3's glossary is headed "Definitions of terms" (plural). The document writes "Definition of terms" nine times:
    - in quotation marks in the Statements of OUT-001 (ICHD-3 "Definition of terms" [S-001]), OUT-002, OUT-004 and OUT-007;
    - in the locations of the [S-001] quotes in OUT-001 (twice), OUT-004, OUT-007 and OUT-031.

    The singular form does not occur anywhere in the source text, so a reader who searches the PDF for the quoted heading finds nothing.
  - (b) OUT-013 locates the [S-001] quote "After an initial consultation, use of an aura diary may clarify the diagnosis." as "(1.2 Migraine with aura, end of comments, p. 21)". The sentence ends a paragraph in the middle of the 1.2 comments. Six further comment paragraphs follow on the same page, before "1.2.1 Migraine with typical aura". They begin:
    - "Migraine aura is sometimes associated with a headache that does not fulfil criteria for 1.1 Migraine without aura …";
    - "Before or simultaneously with the onset of aura symptoms …";
    - "The previously defined syndromes …";
    - "The diagnosis is usually evident after a careful history alone …";
    - "Prodromal symptoms may begin hours or a day or two before …";
    - "Postdromal symptoms, most commonly feeling tired or weary …".

    The page (p. 21) is correct.
- Evidence: https://ichd-3.org/wp-content/uploads/2018/01/The-International-Classification-of-Headache-Disorders-3rd-Edition-2018.pdf (downloaded 2026-10-20, 211 pages; pdftotext and `-layout`).
  - PDF p. 209 carries the heading "Definitions of terms", followed by "Accompanying symptoms: Symptoms that typically accompany rather than precede or follow headache." The quoted definitions "Frequency of attacks" and "Cluster period" are on p. 209 and "Headache days" on p. 210, under this heading.
  - A case-insensitive search of the whole text finds "Definitions of terms" once and "Definition of terms" nowhere.
  - On PDF p. 21 the paragraph "Patients often find it hard to describe their aura symptoms, in which case they should be instructed to time and record them prospectively. … After an initial consultation, use of an aura diary may clarify the diagnosis." is followed by the six comment paragraphs listed above. Then comes the heading "1.2.1 Migraine with typical aura", on the same page.
- Earlier history of this item: none. Both labels have been unchanged since v00, and no earlier remark or fix touched them. OUT-031 itself changed in v01 (R01-09 added an S-007 quote), but not its S-001 location. OUT-001, OUT-002, OUT-004, OUT-007 and OUT-013 have been unchanged since v00.
- Required change:
  - (a) Replace "Definition of terms" with "Definitions of terms" at all nine places: the Statements of OUT-001, OUT-002, OUT-004 and OUT-007, and the [S-001] locations in OUT-001 (two quotes), OUT-004, OUT-007 and OUT-031. Page numbers stay as they are.
  - (b) In OUT-013, change the location to "(1.2 Migraine with aura, comments, p. 21)", or to "(1.2 Migraine with aura, comments, end of the paragraph beginning "Patients often find it hard to describe their aura symptoms", p. 21)".
  - No quote, requirement text or strength changes.

## Notes on frozen items (for the human)
None.
