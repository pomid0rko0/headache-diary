# Fix log — iteration 34
Input review: reviews/review-iter-34.md · Input version: v33 · Output version: v34
Date: 2026-10-22

## What was read, downloaded and checked

**Read:**
- PROCESS.md, in full. The binding rule here is section 4: every quote carries "the location in the source".
- v33 (`OUTPUT_MODEL.md`, byte-identical to `history/v33.md`):
  - sections 1 to 4;
  - every Evidence field (194 fields), E-057 in full;
  - section 8 (ISS-01 to ISS-12), section 9 and section 10;
  - the located quotes in Notes fields: E-041 Notes and the pointers in E-045, E-046 and INV-063;
  - the iteration-33 entries of sections 11 and 12.
- Review 34 (one remark).
- Fix 33, for the log format, and fix 07 (R07-03), the earlier location remark of the same size.
- The oscillation check after iteration 32. Its watch points name no Evidence location. The nearest is "Availability of instrument and screening results", which names E-057 Notes; this fix does not touch E-057 Notes.
- `FROZEN_ITEMS.md` does not exist, and no item carries a FROZEN marker.

**Downloaded** with `curl` through the proxy, all HTTP 200. Every source went into its own new folder under `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix34/dl/`. Scripts are in `…/fix34/scripts/` and outputs in `…/fix34/out/`. All Python ran with `python3 -I`.
- [S-102]:
  - the Europe PMC full text, `https://www.ebi.ac.uk/europepmc/webservices/rest/PMC4406925/fullTextXML`;
  - PMC's own JATS copy, `https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pmc&id=4406925`;
  - the PubMed esummary of PMID 25902814: J Headache Pain 2015;16:24, PMC4406925, DOI 10.1186/s10194-015-0503-y, seven authors, as section 10 cites it.
- Europe PMC full texts of [S-011] (PMC9188162), [S-012] (PMC9555163), [S-013] (PMC7296705), [S-014] (PMC6734476), [S-023] (PMC9607711), [S-042] (PMC12279330), [S-101] (PMC3057423) and [S-104] (PMC183845).
- PDFs at their Stage 1 or section 10 URLs:
  - [S-001] ICHD-3, 211 pp.;
  - [S-007], 39 pp.;
  - [S-008], 31 pp.;
  - [S-010], 11 pp.;
  - [S-016], 64 pp.;
  - [S-018], 12 pp.;
  - [S-033], 92 pp.;
  - [S-034], 53 pp.;
  - [S-035], 92 pp.;
  - [S-105], 9 pp.
- Web pages:
  - [S-015]: the Recommendations page and the Overview page;
  - [S-028];
  - [S-103];
  - [S-106]: chapter 2 and the Overview page.
- ichd-3.org, the ICHD-3 web edition of [S-001]: the pages of A1.1 and A1.1.3, to settle the location found in ISS-03.

**Extraction:**
- PDFs: per page, with `pdftotext -raw` and `-layout`. Page 6 of [S-010] was also extracted in default reading order. The image-only title page of [S-034] was rendered with `pdftoppm` and read.
- JATS: every `p`, table cell, caption and label, with its section path (titles of the enclosing `sec` elements), its paragraph number within the section, its `id`, and the enclosing table or box (`jats_units.py`).
- HTML: every `p`, `li`, `td` and `th`, with its heading path and the enclosing element `id` (`html_units.py`). For NICE pages, the `id` gives the recommendation or paragraph number, for example `cg150-1_3_26` or `ta260-2_1`.

**Page conventions,** read on the page headers and footers:
- PDF page = printed page for [S-001], [S-007], [S-008], [S-010], [S-018], [S-033] and [S-034];
- [S-016]: printed page = PDF page − 6;
- [S-035]: printed page = PDF page − 10. The model states "PDF p." for this source;
- [S-105]: "P. n/9" = PDF page n.

## Remarks

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R34-01 | fixed (the review's wording) | E-057 (Evidence: the locations of the two [S-102] bullets) | The quotes go from "(Methods, "Headache impact on functioning", subsection "Migraine-related disability")" and "(same subsection, the sentence after the grades)" to "(Methods, section "Migraine-related disability")" and "(same section, the sentence after the grades)". **Verified** in both JATS copies of PMC4406925 (Europe PMC `fullTextXML` and PMC efetch). Under `sec` Sec2 "Methods" stand, as siblings:<br>• Sec5 "Headache impact on functioning": one paragraph, "We used the following migraine/headache impact measures: MIDAS (scored by grade), a MIDAS measure of lost productive time (LPT) [22,23] and the HIT-6 [21].";<br>• Sec6 "Migraine-related disability";<br>• Sec7 "Lost productive time".<br>Both quotes are in the single paragraph of Sec6, and the recall sentence is the sentence right after the grades sentence. Both quotes are verbatim and unchanged. No other text of v33 gave this location: "Headache impact on functioning" occurred only on line 1725. |

## Location check of all Stage 2 quotes

**Method** (`checks_spec.py`, `run_checks.py`, `findlib.py`, `ichd_struct.py`, `ctx_pdf.py`; results in `out/checks_v33.json`).
- **Check list.** Every quote and quoted fragment in sections 5, 8 and 10 whose location in a source the model states was taken into the list, with its model line. That covers:
  - all Evidence bullets with a new-source quote ([S-101] to [S-106]);
  - every new passage quoted from a Stage 1 source;
  - the located quotes in E-041 Notes;
  - the located fragments in the E-041 Evidence prose;
  - the section 10 citations.

  The script pulls each quote from its model line by its exact opening words. Untagged quotes without a stated location, and Stage 1 quotes cited only by requirement, carry no location and are not in the list.
- **Matching.** Each quote is split at "[...]". Every piece is found in the downloaded source after NFKD normalisation, case folding and removal of everything but letters and digits (soft hyphens and the ICHD-3 "þ" glyph removed). The match is mapped back to its PDF page(s), to its JATS unit (section path, paragraph number, `id`) or to its HTML unit (heading path, `id`).
- **Comparison.**
  - The stated page or section path was compared with the actual one by script.
  - The finer claims were read on the page or in the unit: code, Description, criterion letter, note or comment of ICHD-3 (`ichd_struct.py` lists the nearest preceding code heading, field label and item); item numbers; paragraph numbers; "first", "second" or "last" sentence; "two sentences later"; "directly after"; the box, heading or recommendation named.
  - The "Origin" column says whether the quoted text is Stage 1 text: S1 = verbatim in Stage 1 v18 after normalisation, S2 = not in Stage 1.
- **Batch 2.** A second list (`checks_spec2.py`, `out/checks2_v33.json`) covers the Stage 1 quotes whose source location the Stage 2 text restates (recommendation, question, section or page). They are not Stage 2 additions and were checked for completeness.
- **Re-run on v34.** All three corrected locations match (`out/checks_v34.txt`, `out/checks2_v34.txt`).

**Result.**
- **Batch 1:** 142 stated locations (123 of quotes that are not Stage 1 text, 19 of fragments that also occur in Stage 1 text but are located by the Stage 2 text). 139 are correct. **Three were wrong and are fixed:**
  - rows 99 and 100: R34-01;
  - row 122: ISS-03, below.
- **Batch 2:** 39 restated Stage 1 locations, all correct.
- The automatic test also flagged six correct rows (batch 1: 30, 31, 70, 75, 140; batch 2: B13), because its comparison was too crude for them. Each was settled by reading, as the "Actual location" column shows:
  - rows 30 and 31: a heading path, not a text unit;
  - row 70: a source title that is the Stage 1 citation title;
  - rows 75 and B13: EHF 2022 question 3 is the expert consensus question 3, as Stage 1 cites it;
  - row 140: the [S-103] page title.
- Row 142, the image-only title page of [S-034], was checked by rendering it.

**The further instance (ISS-03).**
- **The error.** v33 located [S-001] "This subclassification of 1.1 Migraine without aura is clearly applicable only to menstruating women as defined above." at "(A1.1 comments, first sentence, p. 190; …)". A1.1 has no comments of its own.
- **Placement in the PDF** (p. 190, layout text). The heading A1.1 Migraine without aura is followed directly by A1.1.1, A1.1.2 and A1.1.3, each with its criteria and notes. The "Comments:" that begin with the quoted sentence follow the diagnostic criteria and the note of A1.1.3 Non-menstrual migraine without aura, and they run on to p. 191, before A1.2.
- **ICHD-3's convention.** ICHD-3 prints the comments of a code after that code's description, criteria and notes and before its subcodes:
  - 3.1 Cluster headache: its Comments stand before 3.1.1 (p. 42);
  - 8.2.3: its Comments stand after its Description and before 8.2.3.1 (p. 123).

  So comments that follow A1.1.3's criteria and note are the comments of A1.1.3.
- **The web edition agrees.** The standard owner's web edition (ichd-3.org) has no text on the A1.1 page, and shows these comments on the A1.1.3 page under "Comments:".
- **New location:** "(A1.1.3 Non-menstrual migraine without aura, comments, first sentence, p. 190; the comments follow the diagnostic criteria and note of A1.1.3, the last code of A1.1; the text layer breaks "without" at a line end)".
- **Unchanged:** the quote, and the ISS-03 argument, which rests on the words of the quote ("This subclassification of 1.1 Migraine without aura").
- **Earlier positions.** A case-insensitive search of all reviews, fixes and oscillation checks for "A1.1 comment", "A1.1.3" and "This subclassification" found:
  - review 20, which proposed the quote with the location "(A1.1, Comments, first sentence, p. 190; …)" for R20-01;
  - fix 20, which adopted it;
  - review 21, which repeated "the A1.1 comment".

  None examined which code these comments belong to, so the evidence above is new, and the change reverses no fix that rested on such an examination.
- **Historical entries left as they are.** The iteration-20 entries of sections 11 and 12 record the location as stated then. They are records of that iteration and are not edited; the v34 entries record the correction.

**Batch 1: quotes and fragments that Stage 2 added or located** (stated location as in v33, abridged; "Actual location" from the downloaded source; line numbers are the same in v33 and v34).

| # | Item (line) | Source | Origin | Quote (opening words) | Stated location (v33, abridged) | Actual location | Result |
|---|---|---|---|---|---|---|---|
| 1 | E-009 (507) | S-001 | S2 | 1. Migraine | classification list, p. 8 | p. 8, classification list | ok |
| 2 | E-009 (507) | S-001 | S1 | 1.2 Migraine with aura | classification list, p. 8 | p. 8, classification list | ok |
| 3 | E-009 (507) | S-001 | S1 | 1.3 Chronic migraine | classification list, p. 8 | p. 8, classification list | ok |
| 4 | E-009 (507) | S-001 | S2 | 2. Tension-type headache (TTH) | classification list, p. 8 | p. 8, classification list | ok |
| 5 | E-009 (507) | S-001 | S1 | 2.3 Chronic tension-type headache | classification list, p. 8 | p. 8, classification list | ok |
| 6 | E-009 (508) | S-001 | S1 | 3.1 Cluster headache | classification list, p. 9 | p. 9, classification list | ok |
| 7 | E-009 (509) | S-001 | S2 | 8.2 Medication-overuse headache (MOH) | classification list, p. 12 | p. 12, classification list | ok |
| 8 | E-009 (509) | S-001 | S2 | 8.2.1 Ergotamine-overuse headache | classification list, p. 12 | p. 12, classification list | ok |
| 9 | E-009 (509) | S-001 | S1 | 8.2.2 Triptan-overuse headache | classification list, p. 12 | p. 12, classification list | ok |
| 10 | E-009 (509) | S-001 | S2 | 8.2.3 Non-opioid analgesic-overuse headache | classification list, p. 12 | p. 12, classification list | ok |
| 11 | E-009 (509) | S-001 | S1 | 8.2.4 Opioid-overuse headache | classification list, p. 12 | p. 12, classification list | ok |
| 12 | E-009 (509) | S-001 | S1 | 8.2.5 Combination-analgesic-overuse headache | classification list, p. 12 | p. 12, classification list | ok |
| 13 | E-009 (509) | S-001 | S1 | 8.2.6 Medication-overuse headache attributed to multiple dru … | classification list, p. 12 | p. 12, classification list | ok |
| 14 | E-009 (509) | S-001 | S2 | 8.2.7 Medication-overuse headache attributed to unspecified  … | classification list, p. 12 | p. 12, classification list | ok |
| 15 | E-009 (509) | S-001 | S2 | 8.2.8 Medication-overuse headache attributed to other medica … | classification list, p. 12 | p. 12, classification list | ok |
| 16 | E-018 (677) | S-010 | S2 | Modest Control. This is defined as four to six days with mig … | section "Setting goals of migraine burden while on treatment", p. 6 | p. 6, under the heading "Setting goals of migraine burden while on treatment" | ok |
| 17 | E-018 (678) | S-010 | S2 | The assessment of the above goals requires a clear definitio … | same section, p. 6, the paragraph directly after the four control levels | p. 6, same section, the paragraph right after the four level paragraphs | ok |
| 18 | E-018 (679) | S-010 | S2 | We included in our definitions of treatment goals also moder … | same section, p. 6, the paragraph after the three definitions | p. 6, same section, the paragraph right after the three numbered definitions | ok |
| 19 | E-028 (842) | S-001 | S2 | For the purposes of ICHD-3, all non-opioid analgesics are re … | 8.2.3 Non-opioid analgesic-overuse headache, comments, p. 123 | p. 123, 8.2.3 Comments (after the 8.2.3 Description, before 8.2.3.1) | ok |
| 20 | E-028 (843) | S-001 | S2 | Regular intake of any combination of ergotamine, triptans, n … | 8.2.6, diagnostic criterion B, p. 124 | p. 124, 8.2.6 Diagnostic criteria, B | ok |
| 21 | E-028 (844) | S-001 | S2 | Without overuse of any single drug or drug class alone means … | 8.2.6, note 2, p. 125 | p. 125, 8.2.6 Notes (after criterion B across the page break), note 2 | ok |
| 22 | E-032 (928) | S-001 | S2 | [...] regular overuse of acute or symptomatic headache medic … | 8.2 Medication-overuse headache, Description, p. 122 | p. 122, 8.2 Description | ok |
| 23 | E-032 (929) | S-001 | S2 | [...] regular use of ergotamine on 10 or more days/month for … | 8.2.1, Description, p. 123 | p. 123, 8.2.1 Description | ok |
| 24 | E-032 (930) | S-001 | S2 | [...] regular use of one or more triptans on 10 or more days … | 8.2.2, Description, p. 123 | p. 123, 8.2.2 Description | ok |
| 25 | E-032 (931) | S-001 | S2 | [...] regular use of one or more non-opioid analgesics on 15 … | 8.2.3, Description, p. 123 | p. 123, 8.2.3 Description | ok |
| 26 | E-032 (932) | S-001 | S2 | Regular intake of one or more opioids [...] on ≥10 days/mont … | 8.2.4, diagnostic criterion B, p. 124 | p. 124, 8.2.4 Diagnostic criteria, B | ok |
| 27 | E-032 (933) | S-001 | S2 | Regular intake of one or more combination-analgesic medicati … | 8.2.5, diagnostic criterion B, p. 124 | p. 124, 8.2.5 Diagnostic criteria, B | ok |
| 28 | E-032 (934) | S-001 | S2 | Regular overuse, on ≥10 days/month for >3 months, of one or  … | 8.2.8, diagnostic criterion B, p. 125 | p. 125, 8.2.8 Diagnostic criteria, B | ok |
| 29 | E-041 (1179) | S-015 | S2 | This guideline covers the diagnosis and management of tensio … | Overview page of CG150 | CG150 Overview page | ok |
| 30 | E-041 (1180) | S-015 | S2 | Migraine with or without aura | Recommendations, section 1.3 "Management" | Recommendations page: heading "Migraine with or without aura" under "1.3 Management" | ok |
| 31 | E-041 (1180) | S-015 | S2 | Prophylactic treatment review | within "Migraine with or without aura"; recs 1.3.27-1.3.29 under it | heading "Prophylactic treatment review" within it; recs 1.3.27, 1.3.28 and 1.3.29 stand under it | ok |
| 32 | E-041 (1181) | S-015 | S2 | For CGRP inhibitors recommended as options for preventing ep … | recommendation 1.3.24 | rec. 1.3.24 | ok |
| 33 | E-041 (1182) | S-015 | S2 | Intramuscular injection of botulinum toxin type A is recomme … | recommendation 1.3.26 | rec. 1.3.26, first sentence | ok |
| 34 | E-041 (1207) | S-015 | S2 | For full details, see NICE's technology appraisal guidance o … | recommendation 1.3.26, the sentence after the one quoted above | rec. 1.3.26, second sentence, right after the first | ok |
| 35 | E-041 (1183) | S-018 | S2 | This is a summary of the American Academy of Neurology (AAN) … | Clinician Summary, p. 1, the sentence below the title | p. 1, first sentence below the title lines ("... practice guideline", "Clinician Summary") | ok |
| 36 | E-041 (1184) | S-018 | S2 | 14B. Clinicians should wait 24 weeks at the recommended dose … | Recommendation 14 "When to Assess Treatment Efficacy", level B, p. 7 | p. 7, under "When to Assess Treatment Efficacy" / "Recommendation 14", marked "Level B" | ok |
| 37 | E-041 (1185) | S-018 | S2 | 14H. If suboptimal response is observed after 12–24 weeks (s … | Recommendation 14, level B, p. 8 | p. 8, rec. 14H, marked "Level B" | ok |
| 38 | E-041 (1186) | S-016 | S2 | This guideline provides recommendations based on current evi … | section 1.2.1 "Overall objectives", p. 1 (PDF p. 7) | PDF p. 7 = printed p. 1; 1.2.1 OVERALL OBJECTIVES, first sentence | ok |
| 39 | E-041 (1187) | S-016 | S2 | Studies of children with migraine were not included, however … | same section, p. 1, two sentences later | PDF p. 7 = printed p. 1; same section, third sentence | ok |
| 40 | E-041 (1188) | S-011 | S2 | In 2019 the European Headache Federation (EHF) issued the fi … | Background, first paragraph | Background, paragraph 1 (Par12) | ok |
| 41 | E-041 (1189) | S-011 | S2 | Considering the new knowledge on the topic, the EHF council  … | Background, second paragraph | Background, paragraph 2 (Par13) | ok |
| 42 | E-041 (1190) | S-008 | S2 | In individuals initiating a new migraine oral preventive tre … | Q2, Recommendations, Optimal, first sentence, p. 9 | p. 9, Q2 > Recommendations > Optimal, first sentence; the next sentence is the one on injectable drugs | ok |
| 43 | E-041 (1190) | S-008 | S2 | *See Q6 for the criteria for assessing the effectiveness of  … | footnote of the Q2 sentence, p. 9 | p. 9, footnote below the Q2 recommendations | ok |
| 44 | E-041 (1191) | S-008 | S2 | In individuals initiating a new oral preventive treatment, w … | Q2, Recommendations, Essential, p. 9 | p. 9, Q2 > Recommendations > Essential | ok |
| 45 | E-041 (1192) | S-008 | S2 | Q2 – When should the effectiveness of a migraine preventive  … | heading of Q2, p. 9 | p. 9, heading of Q2 | ok |
| 46 | E-041 (1192) | S-008 | S2 | Q13 – What are the suggested drugs for migraine prevention i … | heading of Q13, p. 17 | p. 17, heading of Q13 | ok |
| 47 | E-041 (1193) | S-028 | S2 | P: Patiënten (kinderen en volwassenen) met migraine, bij wie … | module "Profylactische behandeling migraine", section "Zoeken en selecteren" | module page, section "Zoeken en selecteren" | ok |
| 48 | E-041 (1194) | S-033 | S2 | Возрастная категория: взрослые | title page, p. 1 | p. 1, title page (text layer) | ok |
| 49 | E-041 (1195) | S-033 | S2 | при отсутствии эффекта в течение 3 месяцев следует заменить  … | section 3.3 "Профилактическая терапия", Комментарии, p. 39 | p. 39, section 3.3 "Профилактическая терапия" (pp. 38–43), Комментарии to the recommendation | ok |
| 50 | E-041 (1195) | S-033 | S2 | Рекомендуется считать профилактическое лечение эффективным,  … | the recommendation the comment belongs to (p. 39); repeated in section 7.1 | p. 39, the recommendation of section 3.3; section 7.1 (p. 53) repeats it | ok |
| 51 | E-041 (1196) | S-033 | S2 | Рекомендуется для профилактики хронической М в качестве сред … | section 3.3, p. 40 | p. 40, section 3.3 | ok |
| 52 | E-041 (1197) | S-034 | S2 | назначение препаратов для профилактической терапии мигрени с … | Приложение Б, flowchart, p. 52 | p. 52, Приложение Б. Алгоритмы действий врача, flowchart "Алгоритм диагностики и ведения пациента с мигренью" | ok |
| 53 | E-041 (1199) | S-034 | S2 | Диагностика мигрени у детей и подростков показана всем пацие … | section 2 "Критерии постановки диагноза", p. 17 | p. 17, section 2, opening "Критерии постановки диагноза." | ok |
| 54 | E-041 (1200) | S-035 | S2 | Yeterli süre, etkinlik için en az 2-3 ay ve tedavi için en a … | section 3.6.2, Kutu 8, box "Farmakolojik Profilaktik Tedavide Yol Haritası", seventh item, PDF p. 48 | PDF p. 48, section 3.6.2 (PDF pp. 47–49), Kutu 8, box "Farmakolojik Profilaktik Tedavide Yol Haritası", item 7 | ok |
| 55 | E-041 (1201) | S-035 | S2 | Hastalar 3 enjeksiyon siklusu sonra değerlendirilmeli ve fay … | section 3.6.3.9 "Onabotulinumtoxin A", PDF p. 57 | PDF p. 57, section 3.6.3.9 | ok |
| 56 | E-041 (1202) | S-035 | S2 | 6. ÇOCUK VE ERGENDE MİGREN | heading of section 6, PDF p. 77; TOC PDF p. 7 | PDF p. 77 (heading of section 6) and PDF p. 7 (table of contents) | ok |
| 57 | E-041 (1203) | S-035 | S2 | Hasta fayda görüyorsa enjeksiyonlar 3 ayda bir, hasta epizod … | section 3.6.3.9, PDF p. 57, two sentences before the 3-cycles sentence | PDF p. 57, 3.6.3.9, two sentences before "Hastalar 3 enjeksiyon siklusu ..." | ok |
| 58 | E-041 (1204) | S-035 | S2 | Bu tedavide baş ve boyun bölgesinde standardize edilmiş 31 a … | section 3.6.3.9, PDF p. 57, first sentence of the paragraph after the PREEMPT paragraph | PDF p. 57, 3.6.3.9, first sentence of the paragraph after the PREEMPT paragraph | ok |
| 59 | E-041 (1205) | S-035 | S2 | Uygulanım yeri ve dozu: frontal, temporal, oksipital ve serv … | section 7.3, third item, PDF p. 86 | PDF p. 86, section 7.3, item 3 | ok |
| 60 | E-041 (1206) | S-035 | S2 | Etkisini değerlendirmek için en az 2 k ez uygulanmalıdır, | section 7.3, fourth item, PDF p. 86 | PDF p. 86, section 7.3, item 4, right after item 3 | ok |
| 61 | E-041 (1208) | S-106 | S2 | The recommended re-treatment schedule is every 12 weeks (see … | section 2 "The technology", paragraph 2.1, last sentence | section 2 "The technology", paragraph 2.1, last sentence | ok |
| 62 | E-041 (1178) | S-033 | S2 | М – мигрень | list of abbreviations, p. 4 | p. 4, Список сокращений | ok |
| 63 | E-041 (1178) | S-035 | S2 | 7. MİGRENDE GİRİŞİMSEL İŞLEMLER | heading of chapter 7, PDF p. 82, and running header | PDF p. 82 (heading of chapter 7) and running header of PDF pp. 82–87 | ok |
| 64 | E-041 (1178) | S-035 | S2 | 3. MİGREN BAŞ AĞRISI TEDAVİSİ | section containing 3.6.3.9 | running header of the chapter 3 pages, including PDF p. 57 | ok |
| 65 | E-041 (1178) | S-035 | S1 | Migren Profilaktik Tedavi-Yönetim-6 | Kutu 8 | PDF p. 48, title of Kutu 8 | ok |
| 66 | E-041 (1178) | S-033 | S2 | для профилактики хронической М | section 3.3 | p. 40, within the section 3.3 recommendation | ok |
| 67 | E-041 (1178) | S-034 | S2 | профилактической терапии мигрени | [S-034] flowchart | p. 52, within the flowchart box | ok |
| 68 | E-041 (1178) | S-008 | S2 | a new migraine oral preventive treatment | Q2 | p. 9, within the Q2 Optimal sentence | ok |
| 69 | E-041 (1178) | S-018 | S1 | for migraine prevention | 14B | p. 7, within rec. 14B | ok |
| 70 | E-041 (1178) | S-016 | S1 | SIGN 155: Pharmacological management of migraine | title of S-016 | cover (PDF pp. 1–2); the Stage 1 citation title; no page stated | ok |
| 71 | E-041 (1178) | S-035 | S1 | Migren Klinik Protokolü | title of S-035 | p. 1, title; the Stage 1 citation title; no page stated | ok |
| 72 | E-041 Notes (1209) | S-035 | S2 | Enjeksiyon sonrası blokajın etkinliği araştırılmalı hipoeste … | Turkish section 7.1, PDF p. 83 | PDF p. 83, section 7.1 (PDF pp. 82–83, before 7.2 on p. 83) | ok |
| 73 | E-041 Notes (1209) | S-035 | S2 | Başlangıçta haftalık 4 kez sonra aylık yapılması etkinliği a … | Turkish section 7.1, PDF p. 83 | PDF p. 83, section 7.1 | ok |
| 74 | E-041 Notes (1209) | S-035 | S2 | Bir yılın sonunda ağrı sıklığı ve şiddetinde azalma gözlenen … | Turkish section 7.3, fifth item, PDF p. 86 | PDF p. 86, section 7.3, item 5 | ok |
| 75 | E-041 Notes (1209) | S-011 | S2 | In selected cases decision on treatment maintenance can be r … | EHF 2022 question 3, guidance text | Results > Expert consensus statements > question 3 > Clinical guidance | ok |
| 76 | E-041 Notes (1209) | S-033 | S2 | Эффективность терапии следует оценивать через 3 мес. после е … | Russian section 3.3 comment on anti-CGRP mAbs, p. 41 | p. 41, section 3.3, Комментарии on anti-CGRP antibodies | ok |
| 77 | E-041 Notes (1209) | S-008 | S1 | at least eight weeks at the target dose | IHS 2024 Q4, Evidence | p. 11, Q4 > Evidence | ok |
| 78 | E-041 Notes (1209) | S-018 | S1 | by 8 weeks | AAN/AHS 14C | p. 7, rec. 14C | ok |
| 79 | E-041 Notes (1209) | S-018 | S2 | wait 24 weeks at the recommended dose before assessing effic … | AAN/AHS 14B | p. 7, rec. 14B | ok |
| 80 | E-041 Notes (1209) | S-033 | S2 | минимум через 6 месяцев терапии | Russian botulinum time point (section 3.3) | p. 39, section 3.3 comment | ok |
| 81 | E-041 Notes (1209) | S-034 | S2 | Контроль эффективности терапии через 3мес. | flowchart box | p. 52, flowchart | ok |
| 82 | E-041 Notes (1209) | S-035 | S2 | en az 2 k ez | section 7.3 | PDF p. 86, section 7.3, item 4 | ok |
| 83 | E-041 Notes (1209) | S-035 | S2 | 3 ay aralıklarla | section 7.3 | PDF p. 86, section 7.3, item 3 | ok |
| 84 | E-041 Notes (1209) | S-035 | S2 | Etkisini değerlendirmek için | section 7.3 | PDF p. 86, section 7.3, item 4 | ok |
| 85 | E-041 Notes (1209) | S-035 | S2 | etkinlik için en az 2-3 ay | Kutu 8 | PDF p. 48, Kutu 8, item 7 | ok |
| 86 | E-041 Notes (1209) | S-008 | S2 | after three months at the target dose | IHS 2024 Q2 | p. 9, Q2 Optimal | ok |
| 87 | E-045 (1365) | S-008 | S2 | For patients with chronic migraine who have not achieved a ≥ … | Q6, Recommendations, Optimal, p. 12 | p. 12, Q6 > Recommendations > Optimal | ok |
| 88 | E-045 (1366) | S-008 | S2 | The clinically meaningful improvement in MIDAS score is defi … | Q6, Evidence, p. 13 | p. 13, Q6 > Evidence | ok |
| 89 | E-045 (1368) | S-035 | S2 | Ölçüt atak sıklığında en az %50 azalma olması | section 3.6.2, Kutu 8, box "Farmakolojik Profilaktik Tedavide Yol Haritası", second item, PDF p. 48 | PDF p. 48, Kutu 8 box, item 2 | ok |
| 90 | E-045 (1369) | S-035 | S2 | Migren önleyici tedavi; migren ataklarının sıklığını, şiddet … | section 3.3 "Farmakolojik Tedavi", item "b. Profilaksi", PDF p. 23 | PDF p. 23, section 3.3 "Farmakolojik Tedavi", item "b. Profilaksi" | ok |
| 91 | E-045 (1364) | S-035 | S1 | atak sıklığında ve süresinde %50'lik bir azalma ve akut atak … | [S-035] section 3.6.2 (Stage 1 quote) | PDF p. 48, section 3.6.2, list after the Kutu 8 box | ok |
| 92 | E-046 (1445) | S-010 | S2 | Migraine Freedom. This is defined as the complete eliminatio … | section "Setting goals ...", p. 6 | p. 6, same section | ok |
| 93 | E-046 (1446) | S-010 | S2 | Optimal Control. This is defined as less than four days with … | same section, p. 6 | p. 6, same section | ok |
| 94 | E-046 (1447) | S-010 | S2 | Modest Control. This is defined as four to six days with mig … | same section, p. 6 | p. 6, same section | ok |
| 95 | E-046 (1448) | S-010 | S2 | Insufficient Control. This is defined as more than six days  … | same section, p. 6; running header interrupts after "per" | p. 6, same section; in pdftotext reading order the header "Cephalalgia 45(2)" stands between "per" and "month" | ok |
| 96 | E-046 (1449) | S-010 | S2 | In some cases, insufficient control may be present when ther … | same section, p. 6 | p. 6, same section | ok |
| 97 | E-057 (1723) | S-101 | S2 | [...] ranges between 36 and 78, with larger scores reflectin … | Methods, "Data sources", HIT-6 paragraph | Methods > Data sources, paragraph 4 (the HIT-6 paragraph) | ok |
| 98 | E-057 (1724) | S-101 | S2 | The four headache impact severity categories are little or n … | Methods, "Data sources", HIT-6 paragraph | Methods > Data sources, paragraph 4 (the HIT-6 paragraph) | ok |
| 99 | E-057 (1725) | S-102 | S2 | [...] four grades based on total days of impaired functionin … | Methods, "Headache impact on functioning", subsection "Migraine-related disability" | Methods > "Migraine-related disability" (Sec6), a sibling of "Headache impact on functioning" (Sec5); same in PMC efetch JATS | fixed |
| 100 | E-057 (1726) | S-102 | S2 | The recall period for the MIDAS is three months | same subsection, the sentence after the grades | Methods > "Migraine-related disability" (Sec6), the sentence right after the grades | fixed |
| 101 | E-057 (1727) | S-103 | S2 | The PedMIDAS grading scale is as follows: | section "PedMIDAS Grading Scale" | heading "PedMIDAS Grading Scale", text and table | ok |
| 102 | E-057 (1728) | S-014 | S2 | HALT-90 (Fig. 3 (also, Additional file 18 )) counts days aff … | section "The Headache-Attributed Lost Time (HALT) Indices", paragraph beginning "There are three versions of HALT" | "The Headache-Attributed Lost Time (HALT) Indices", paragraph 5 (Par1145), which begins "There are three versions of HALT" | ok |
| 103 | E-057 (1729) | S-014 | S2 | HALT-30 (Fig. 4 (also, Additional file 19 )) accordingly rec … | same paragraph | same paragraph (Par1145) | ok |
| 104 | E-057 (1730) | S-014 | S2 | the unit of each being whole days per one or 3 months | subsection "Scoring HALT", first sentence | "Scoring HALT" (child of the HALT Indices section), paragraph 1, first sentence | ok |
| 105 | E-057 (1731) | S-014 | S1 | Grading of HALT-90 | Table 18 in subsection "Scoring HALT" | Table 18, within "Scoring HALT" | ok |
| 106 | E-059 (1776) | S-104 | S2 | [...] the possible scores ranged from 0 to 21 for anxiety an … | section "Construction of the HADS" | Discussion > "Construction of the Hospital Anxiety And Depression Scale (HADS)" | ok |
| 107 | E-059 (1777) | S-105 | S2 | PHQ-9 total score for the nine items ranges from 0 to 27. | section "Use of some screeners as severity and outcome measures", P. 6/9 | P. 6/9, under "USE OF SOME SCREENERS AS SEVERITY AND OUTCOME MEASURES" (the sentence also occurs on P. 5/9) | ok |
| 108 | E-059 (1778) | S-105 | S2 | GAD-7 total score for the seven items ranges from 0 to 21. | same section, P. 6/9 | P. 6/9, same section | ok |
| 109 | E-060 (1812) | S-001 | S2 | Occurring exclusively on day 1 ± 2 (i.e. days −2 to +3) | A1.1.1 criterion B, p. 190 | p. 190, A1.1.1 Diagnostic criteria, B | ok |
| 110 | E-060 (1812) | S-001 | S2 | Occurring on day 1 ± 2 (i.e. days −2 to +3) | A1.1.2 criterion B, p. 190 | p. 190, A1.1.2 Diagnostic criteria, B | ok |
| 111 | E-060 (1813) | S-001 | S2 | The first day of menstruation is day 1 and the preceding day … | A1.1.1, note 2, p. 190 | p. 190, A1.1.1 Notes, note 2 | ok |
| 112 | E-063 (1865) | S-001 | S2 | To be considered a remission, the attack-free period must ex … | Definitions of terms, Cluster remission period, p. 209 | p. 209, Definitions of terms, "Cluster remission period" | ok |
| 113 | E-064 (1882) | S-007 | S2 | a persistent high attack frequency (e.g. ≥ 14 attacks per we … | section 2.2, Recommendations, item a, p. 10 | p. 10, section 2.2 "Specific patient populations and attack characteristics", Recommendations, item a) | ok |
| 114 | INV-046 (2605) | S-001 | S2 | For the purposes of ICHD-3, all non-opioid analgesics are re … | 8.2.3, Comments, second paragraph, p. 123 | p. 123, 8.2.3 Comments, second paragraph | ok |
| 115 | ISS-01 (3744) | S-001 | S2 | Regular intake of any combination of ergotamine, triptans, n … | 8.2.6, diagnostic criterion B, p. 124 | p. 124, 8.2.6 Diagnostic criteria, B | ok |
| 116 | ISS-02 (3750) | S-001 | S2 | 8.2.3 Non-opioid analgesic-overuse headache | classification list, p. 12 | p. 12, classification list | ok |
| 117 | ISS-02 (3750) | S-001 | S2 | For the purposes of ICHD-3, all non-opioid analgesics are re … | 8.2.3, comments, p. 123 | p. 123, 8.2.3 Comments | ok |
| 118 | ISS-02 (3750) | S-001 | S2 | Most cases of 10.1.1 High-altitude headache respond to simpl … | 10.1.1, comments, second paragraph, first sentence, p. 139 | p. 139, 10.1.1 Comments, second paragraph, first sentence | ok |
| 119 | ISS-02 (3750) | S-001 | S2 | 8.2.3.1 Paracetamol (acetaminophen)-overuse headache | classification list, p. 12 | p. 12, classification list | ok |
| 120 | ISS-02 (3750) | S-001 | S1 | 8.2.3.2 Non-steroidal anti-inflammatory drug (NSAID)-overuse … | classification list, p. 12 | p. 12, classification list | ok |
| 121 | ISS-02 (3750) | S-001 | S2 | ibuprofen or other NSAIDS | 7.3.2, comment, p. 105 | p. 105, 7.3.2 Comment | ok |
| 122 | ISS-03 (3756) | S-001 | S2 | This subclassification of 1.1 Migraine without aura is clear … | A1.1 comments, first sentence, p. 190 | p. 190, "Comments:" printed after the criteria and note of A1.1.3 Non-menstrual migraine without aura, first sentence (ichd-3.org: on the A1.1.3 page under "Comments:"; the A1.1 page has no text) | fixed |
| 123 | ISS-05 (3772) | S-010 | S2 | Modest Control. This is defined as four to six days with mig … | section "Setting goals ...", p. 6 | p. 6, same section | ok |
| 124 | ISS-08 (3784) | S-010 | S1 | Migraine Freedom | p. 6 (level names) | p. 6 (also in the abstract and a figure) | ok |
| 125 | ISS-08 (3784) | S-010 | S2 | Insufficient Control | p. 6 (level names) | p. 6 (also in the abstract and a figure) | ok |
| 126 | ISS-09 (3790) | S-001 | S2 | [...] regular overuse of acute or symptomatic headache medic … | 8.2 Description, p. 122 | p. 122, 8.2 Description | ok |
| 127 | ISS-10 (3796) | S-015 | S2 | Consider verapamil for prophylactic treatment during a bout  … | recommendation 1.3.39 | rec. 1.3.39 | ok |
| 128 | ISS-10 (3796) | S-015 | S2 | Consider a course of up to 10 sessions of acupuncture over 5 … | recommendation 1.3.9 | rec. 1.3.9 | ok |
| 129 | ISS-10 (3796) | S-034 | S2 | назначение препаратов для профилактической терапии мигрени с … | Приложение Б flowchart, p. 52 | p. 52, flowchart | ok |
| 130 | ISS-11 (3802) | S-015 | S2 | young people (aged 12 years and older) and adults | Overview page | CG150 Overview page | ok |
| 131 | ISS-11 (3802) | S-015 | S1 | Review the diagnosis of medication overuse headache and furt … | recommendation 1.3.48 | rec. 1.3.48 | ok |
| 132 | ISS-12 (3809) | S-001 | S2 | To be considered a remission, the attack-free period must ex … | Definitions of terms, Cluster remission period, p. 209 | p. 209, Definitions of terms, "Cluster remission period" | ok |
| 133 | ISS-12 (3810) | S-001 | S2 | Cluster headache attacks occurring in periods lasting from s … | 3.1.1 Description, p. 42 | p. 42, 3.1.1 Description | ok |
| 134 | ISS-12 (3810) | S-001 | S2 | At least two cluster periods lasting from seven days to one  … | 3.1.1 criterion B, p. 42 | p. 42, 3.1.1 Diagnostic criteria, B | ok |
| 135 | ISS-12 (3811) | S-001 | S2 | Cluster headache attacks occurring for one year or longer wi … | 3.1.2 Description, p. 42 | p. 42, 3.1.2 Description | ok |
| 136 | ISS-12 (3811) | S-001 | S2 | Occurring without a remission period, or with remissions las … | 3.1.2 criterion B, p. 42 | p. 42, 3.1.2 Diagnostic criteria, B | ok |
| 137 | ISS-12 (3813) | S-001 | S2 | About 10–15% of patients have 3.1.2 Chronic cluster headache … | 3.1 Comments, first paragraph, second sentence, p. 42 | p. 42, 3.1 Comments (before 3.1.1), paragraph 1, sentence 2 | ok |
| 138 | ISS-12 (3813) | S-001 | S2 | The trigeminal autonomic cephalalgias are the exception: in  … | Definitions of terms, Chronic, last sentence, p. 209 | p. 209, Definitions of terms, "Chronic", last sentence | ok |
| 139 | Section 10 (3839) | S-105 | S2 | were developed by Drs. Robert L. Spitzer, Janet B.W. William … | manual, P. 8/9, section "Questions regarding development, acknowledgments and use" | P. 8/9, under "QUESTIONS REGARDING DEVELOPMENT, ACKNOWLEDGMENTS AND USE" | ok |
| 140 | Section 10 (3837) | S-103 | S2 | PedMIDAS Tool for Assessing Migraine Disability | web page "PedMIDAS Tool" | page title "PedMIDAS Tool \| Headache Center"; main heading "PedMIDAS Tool for Assessing Migraine Disability" | ok |
| 141 | Section 10 (3840) | S-015 | S2 | For full details | recommendation 1.3.26 | rec. 1.3.26 (the same phrase also in 1.3.25) | ok |
| 142 | E-041 (1198) | S-034 | S2 | Возрастная группа … дети | title page, p. 1 (image without text layer) | p. 1, rendered with `pdftoppm` and read: "Возрастная группа" with "дети" | ok |

**Batch 2: Stage 1 quotes whose location the Stage 2 text restates** (checked for completeness; not Stage 2 additions).

| # | Item (line) | Source | Origin | Quote (opening words) | Stated location (v33, abridged) | Actual location | Result |
|---|---|---|---|---|---|---|---|
| B1 | E-041 Evidence (1178) | S-015 | S1 | 3 to 6 months after starting | [S-015] rec. 1.3.27 | Prophylactic treatment review > 1.3.27 (cg150-1_3_27) | ok |
| B2 | E-041 Evidence (1178) | S-015 | S1 | after 12 weeks of treatment | [S-015] rec. 1.3.28 | Prophylactic treatment review > 1.3.28 (cg150-1_3_28) | ok |
| B3 | E-041 Evidence (1178) | S-015 | S1 | after 2 treatment cycles | [S-015] rec. 1.3.29 | Prophylactic treatment review > 1.3.29 (cg150-1_3_29) | ok |
| B4 | E-041 Evidence (1178) | S-015 | S1 | migraine prophylaxis | [S-015] rec. 1.3.27 | Migraine with or without aura > Prophylactic treatment (cg150-prophylactic-treatment-2), Prophylactic treatment review > 1.3.27 (cg150-1_3_27) | ok |
| B5 | E-041 Evidence (1178) | S-015 | S1 | the frequency of migraines | [S-015] rec. 1.3.28 | Prophylactic treatment review > 1.3.28 (cg150-1_3_28) | ok |
| B6 | E-041 Evidence (1178) | S-015 | S1 | changed to episodic migraine | [S-015] rec. 1.3.29 | Prophylactic treatment review > 1.3.29 (cg150-1_3_29) | ok |
| B7 | E-041 Evidence (1178) | S-018 | S1 | at least 8–12 weeks at the recommended tolerated dose of mos … | [S-018] rec. 14A | p. 7 | ok |
| B8 | E-041 Evidence (1178) | S-018 | S1 | medications for migraine prevention | [S-018] 14A | p. 7, p. 8 | ok |
| B9 | E-041 Evidence (1178) | S-016 | S1 | eight weeks at the target dose or maximum tolerated dose (fo … | [S-016] section 4.1 (printed p. 14) | p. 20 | ok |
| B10 | E-041 Evidence (1178) | S-016 | S1 | For treatments of fixed dose [...] assessed at 3 months | [S-016] section 4.1 | p. 20 | ok |
| B11 | E-041 Evidence (1178) | S-016 | S1 | assessed at 3 months | [S-016] section 4.1 | p. 20 | ok |
| B12 | E-041 Evidence (1178) | S-011 | S1 | a minimum of 3 consecutive months on treatment | [S-011] question 3 | Results > Expert consensus statements (Par54), Results > Expert consensus statements, Expert consensus statement – question 3 > Clinical guidance (Par62) | ok |
| B13 | E-041 Evidence (1178) | S-011 | S1 | In individuals with episodic or chronic migraine | [S-011] question 3 | Results > Expert consensus statements > question 3 > Clinical guidance (statement box) | ok |
| B14 | E-041 Evidence (1178) | S-008 | S1 | a minimum of three months for injectable drugs taken on a mo … | [S-008] Q2 | p. 5, p. 9 | ok |
| B15 | E-041 Evidence (1178) | S-028 | S1 | Titreer naar de ondergrens van de geadviseerde therapeutisch … | [S-028] Aanbeveling | Profylactische behandeling migraine > Aanbeveling (recommendations) | ok |
| B16 | E-041 Evidence (1178) | S-028 | S1 | evalueer het effect niet eerder dan na 2-3 maanden behandeli … | [S-028] Aanbeveling | Profylactische behandeling migraine > Aanbeveling (recommendations) | ok |
| B17 | E-041 Evidence (1178) | S-033 | S1 | через 3 месяца терапии | [S-033] section 7.1 | p. 39, p. 53 | ok |
| B18 | E-041 Evidence (1178) | S-033 | S1 | профилактическое лечение М | [S-033] (section 7.1 recommendation) | p. 53, p. 89 | ok |
| B19 | E-045 Evidence (1364) | S-015 | S1 | at least 50% in episodic migraine | NICE 1.3.28 | Prophylactic treatment review > 1.3.28 (cg150-1_3_28) | ok |
| B20 | E-045 Evidence (1364) | S-015 | S1 | at least 30% in chronic migraine | NICE 1.3.28 | Prophylactic treatment review > 1.3.28 (cg150-1_3_28) | ok |
| B21 | E-045 Evidence (1364) | S-015 | S1 | at least 30% after 2 treatment cycles | NICE 1.3.29 | Prophylactic treatment review > 1.3.29 (cg150-1_3_29) | ok |
| B22 | E-045 Evidence (1364) | S-015 | S1 | the frequency of headache days per month | NICE 1.3.29 | Prophylactic treatment review > 1.3.29 (cg150-1_3_29) | ok |
| B23 | E-045 Evidence (1364) | S-008 | S1 | a ≥ 50% decrease in monthly migraine days or moderate-to-sev … | IHS Q6 | p. 6, p. 12 | ok |
| B24 | E-045 Evidence (1364) | S-008 | S1 | monthly migraine days or moderate-to-severe headache days | IHS Q6 | p. 6 | ok |
| B25 | E-045 Evidence (1364) | S-033 | S1 | на 50% и более | Russian section 7.1 | p. 39, p. 41, p. 53 | ok |
| B26 | E-045 Evidence (1364) | S-033 | S1 | число дней с ГБ | Russian section 7.1 | p. 18, p. 26, p. 53 | ok |
| B27 | E-045 Evidence (1364) | S-035 | S1 | atak sıklığında ve süresinde %50'lik bir azalma ve akut atak … | [S-035] section 3.6.2 | p. 48 | ok |
| B28 | E-045 Evidence (1364) | S-023 | S1 | mindestens 50 % | [S-023] | body > Hintergrund, Daten zur Therapiedauer von Migräneprophylaxen und Verlauf nach Beenden der Medikation > OnabotulinumtoxinA bei chronischer Migräne | ok |
| B29 | E-045 Evidence (1364) | S-023 | S1 | die Migränetage | [S-023] | body > Hintergrund | ok |
| B30 | E-045 Evidence (1364) | S-042 | S1 | Significant decrease in attack duration based on patient’s h … | [S-042] (Stage 1 OUT-011) | body > Results | ok |
| B31 | E-041 Notes (1209) | S-015 | S1 | the need for continuing migraine prophylaxis 3 to 6 months a … | [S-015] 1.3.27 | Prophylactic treatment review > 1.3.27 (cg150-1_3_27) | ok |
| B32 | E-041 Notes (1209) | S-018 | S2 | after 12–24 weeks (see 14A and 14B) | AAN/AHS 14H | p. 8 | ok |
| B33 | E-041 Notes (1209) | S-028 | S1 | niet eerder dan na 2-3 maanden behandeling | [S-028] | Profylactische behandeling migraine > Aanbeveling (recommendations) | ok |
| B34 | E-041 Notes (1209) | S-011 | S1 | after a minimum of 3 consecutive months on treatment | [S-011] | Results > Expert consensus statements (Par54), Results > Expert consensus statements, Expert consensus statement – question 3 > Clinical guidance (Par62) | ok |
| B35 | E-045 Notes (1370) | S-015 | S2 | as options for preventing episodic or chronic migraine | [S-015] 1.3.24 | Prophylactic treatment > 1.3.24 (cg150-1_3_24) | ok |
| B36 | E-045 Notes (1370) | S-023 | S1 | Bei der episodischen Migräne (eM) | [S-023] | body > Hintergrund | ok |
| B37 | E-045 Notes (1370) | S-008 | S2 | for treatment continuation beyond three months | IHS Q6 | p. 6, p. 12 | ok |
| B38 | E-046 Notes (1450) | S-008 | S1 | that determine whether preventive therapy is effective | IHS Q6 | p. 6, p. 12 | ok |
| B39 | E-046 Notes (1450) | S-008 | S1 | whether preventive therapy is effective and should be contin … | IHS Q6 | p. 6, p. 12 | ok |

## Other changes

- **Header:** "Version: v34 · Iteration: 34 · Status: under review".
- **Section 9:** "(as of v34)".
- **Section 11:** a new entry "Iteration 34 (fix, 2026-10-22)". It records:
  - the downloads (all HTTP 200);
  - the JATS structure of [S-102] in both copies;
  - the ichd-3.org pages of A1.1 and A1.1.3;
  - the method and the result of the location check: 142 locations with three corrected, and 39 restated Stage 1 locations, all correct.
- **Section 12:** a new entry "v34 (iteration 34, 2026-10-22)", with R34-01, the same-defect check with the ISS-03 correction, the text changed, and the totals.
- **Not changed:**
  - every `omn` block and the overview block of section 4;
  - every quote, value, axiom, `when` clause, level, Realises field, traceability row and source entry;
  - section 10;
  - the iteration-20 entries of sections 11 and 12, which are records of that iteration.

**Items changed: 2.**
- E-057: the Evidence field, two location texts (R34-01).
- ISS-03: the Evidence field, one location text (same-defect check).

Beyond these two items, only the header, section 9 and the log entries of sections 11 and 12 changed. In sections 1 to 10, `diff` shows exactly 5 changed lines: the header, the two E-057 bullets, the ISS-03 Evidence line, and section 9.

## Checks

All scripts are in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix34/scripts/` and were run with `python3 -I`.

**Snapshot.** `cmp OUTPUT_MODEL.md history/v34.md`: identical.

**Formal blocks** (`fences34.py`, `blocks34.py`).
- v33 and v34 each have 189 fenced blocks: 188 `omn` blocks and the plain overview block of section 4.
- All 189 are byte-identical and in the same order; no index differs.
- The SHA-256 of the concatenated `omn` blocks is `1ace3c681d070d3d…` in both versions.

**Quotes** (inline script).
- Quoted strings in sections 1 to 10, outside fenced blocks: 807 in v33 and 806 in v34.
- The only string that disappears is the heading name "Headache impact on functioning", which was part of the wrong E-057 location.
- No quote of a source was added, removed or changed.

**Mechanical checks of PROCESS.md section 11** (`mech34.py`, run on v33 and on v34; the two outputs are identical).

| Check | Result (v34) |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 117 invariants (INV-001 to INV-117), none missing, none duplicated. Issues: ISS-01 to ISS-06 and ISS-08 to ISS-12; ISS-07 is listed as withdrawn in section 9. |
| References | No dangling E-, INV- or ISS- reference. Every OUT reference is one of the 39 Stage 1 requirements. 35 source IDs are cited in sections 1 to 10, each in the Stage 1 source table (S-001 to S-046) or in section 10 (S-101 to S-106). |
| Fields | Every element has exactly one Definition, Meaning, Conformance, Realises and Evidence field, and every invariant exactly one Predicate, Reading, Conformance, Realises and Evidence field. No item has two Notes fields. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025), all "full". The Elements and Invariants columns equal the items whose Realises field names the requirement: 0 mismatches. |
| Conformance levels | Invariants: MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 40. Scopes: output 84, repertoire 32, context 1. Every MUST NOT and SHOULD NOT predicate begins with `¬`. Level-annotated attribute declarations: 172 (core 94, MUST 29, SHOULD 47, MAY 2). All equal v33; no level changed. |
| Types and names | 347 declared names (the heads of `given`, `type`, `enum`, `variant`, `value`, `element`, `const`, `fun` and `pred` declarations), none declared twice. Capitalised names used but not declared:<br>• the `let` names `A`, `C` and `D`;<br>• the parameters and bound variables `K`, `Ks` and `L` (section 2.2);<br>• the level keywords `MUST`, `SHOULD` and `MAY`.<br>Every type used is defined. |

**Location re-check on v34.** The batch 1 and batch 2 checks were re-run on v34 with the corrected expectations (`checks_v34.txt`, `checks2_v34.txt`).
- The three corrected locations match their sources.
- Every other row gives the same result as on v33.
