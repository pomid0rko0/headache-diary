# Review — iteration 14
VERDICT: REMARKS
REMARK_COUNT: 2
Reviewed version: v13
Date: 2026-10-21

## Summary

This is the main review of iteration 14: an independent fact-check and review of v13. `OUTPUT_MODEL.md` is byte-identical to `history/v13.md` (checked with `cmp`).

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 after OUT-025), and section 5 as needed;
- v13: every element, every invariant, sections 7 to 12;
- review 13, fix 13 and the v12 → v13 diff;
- the oscillation check after iteration 12 and its seven watch points;
- the remark list of reviews 01 to 13 and the decisions in the fix logs (no remark was declined outright; R11-01 (a)/(b) was declined as a formal change);
- the parts of earlier reviews and fixes that concern my two topics: review 11 on the OUT-017 window, the fix-11 co-presence sweep table, fix 09 on the type scope of acute summaries, and fix 13 on R13-01.

**Earlier decisions.** FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. Neither remark reverses an earlier fix. Each remark states its relation to the watch points.

**Result.**
- **Citations.** No defect in the quotes as given. Every reachable fragment is verbatim at its stated location. 6 fragments could not be re-checked, because S-007 and S-028 were unreachable. All 6 are unchanged since v05/v06, and earlier reviews verified them. The metadata of S-101 to S-106 is correct.
- **Value sets, codes, labels, thresholds, offsets.** No defects.
- **Mechanical checks.** All pass.
- **Scope sweep.** No input, storage or derivation-from-input content.
- **Two remarks:**
  - **R14-01 (coverage gap, OUT-018).** The E-041 rule list is said to hold every evaluation time point that the cited guidance names, "read in full". It omits one: the Turkish Ministry of Health protocol [S-035], section 7.3 "Botulinum Toksin Enjeksiyonu" (PDF p. 86), says that botulinum toxin must be administered at least twice before its effect is evaluated. No loop file mentions this passage.
  - **R14-02 (coverage gap, OUT-024, OUT-031, OUT-034 and optionally OUT-035).** The acute-treatment summaries required by INV-109, INV-104 and INV-088 (and the one in INV-105) have no constraint on their period. A summary of a period in which the medication was not taken (0 treated attacks) therefore meets the requirement while reporting none of the effectiveness that Stage 1 asks for. R13-01 fixed the same kind of gap for the type scope, but not for the period.

## Verification coverage

### Method

- **Downloads.** All were made with `curl` (through the configured proxy) into the fresh directory `r14dl/` of the session scratchpad, outside the repository.
  - **Stage 1 URLs (HTTP 200):**
    - PDFs: S-001 (211 pp.), S-002 (19), S-003 (18), S-005 (14), S-008 (31), S-010 (11), S-016 (64), S-018 (12), S-030 (86), S-033 (92; the first attempt was reset by the peer, the retry succeeded), S-034 (53), S-035 (92);
    - S-015: Recommendations page (`datetime` "2025-06-03" for the last update) and Overview page.
  - **Europe PMC full-text XML (HTTP 200):** S-011, S-014, S-023, S-042, S-101, S-102, S-104.
  - **Other pages (HTTP 200):**
    - S-103 (Cincinnati Children's PedMIDAS page; footer "2026 Cincinnati Children's Hospital Medical Center");
    - S-105 (PHQ/GAD-7 manual, 9 pp.; PDF metadata: author Kurt Kroenke, created 2010-06-22, modified 2014-04-16);
    - S-106 (TA260 chapter 2, chapter 1 and the overview page, "Last reviewed: 11 January 2016").
  - **Unreachable:**
    - S-007: UCL Discovery returned HTTP 503 "Temporary disruption" for both URL forms, twice. The SAGE PDF returned 403. Europe PMC lists the article as not open access. web.archive.org reset the connection. The IHS guidelines page lists only the 1995 cluster headache guideline.
    - S-028: richtlijnendatabase.nl returned HTTP 200 twice, both times with the page "Deze pagina is tijdelijk niet bereikbaar". web.archive.org reset the connection.
- **Extraction.**
  - PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML and XML were stripped of scripts and markup, and entities were unescaped.
  - Rendered with `pdftoppm` and read by eye:
    - ICHD-3 p. 190: the "±", "−" and "+" glyphs have no text mapping;
    - the S-034 title page, which is an image;
    - S-035 p. 86 (R14-01).
- **Scripts.** All are in the session scratchpad, `r14/`, and were run with `python3 -I`:
  - `extract_quotes.py`: every double-quoted string outside `omn` blocks on a line with an `[S-NNN]` tag, split at `[...]`, giving 454 fragments;
  - `search_quotes.py`: three normalisation passes (NFKC/whitespace/quotes/dashes; line-end hyphens; letters and digits only). Each fragment is searched in its tagged source, then in the other sources tagged on the line, then in Stage 1 v18. The hit page is compared with the stated location;
  - `mech.py`: IDs, references, traceability, levels, prohibition form;
  - `names.py`: names in `omn` blocks;
  - `html2txt.py`.

### Citations

| Source | Fragments | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 | 65 | 64. By script, 57: labels pp. 8, 9, 12; 8.2–8.2.8 pp. 122–125; 8.2.3 comment p. 123; "Definitions of terms" pp. 209–210; remission p. 209. By hand on the rendered page, 3: the A1.1.1/A1.1.2 window, p. 190. As Stage 1 statement fragments, 4. The remaining 1 is a search-log row label. "Simple analgesics" occurs only on p. 139 (ISS-02). | 0 | 0 |
| S-002, S-003, S-005 | 17 | 17. 7 at S-002 pp. 10–12 PDF; 6 found in another source tagged on the same line (multi-source lines of E-041/E-045 Notes); 4 Stage 1 fragments | 0 | 0 |
| S-007 IHS cluster | 10 | 4 (Stage 1 fragments, checked against Stage 1 v18); 3 are search-log text | 0 | 3 (E-064 "≥ 14 attacks per week on average" and its section heading; tried as above) |
| S-008 IHS 2024 | 28 | 28. Q2 pp. 5, 9; Q4 p. 11; Q6 pp. 6, 12; Q6 Evidence p. 13; Q13 p. 17. Also "acceptable for treatment continuation beyond three months" (E-008, E-045 Notes), p. 12 | 0 | 0 |
| S-010 IHS 2025 | 44 | 44 (36 at p. 6, among them all control levels and both migraine-day sentences; 8 Stage 1 fragments) | 0 | 0 |
| S-011, S-014, S-023, S-042 | 57 | 57. S-014 includes Table 18 "Grading of HALT-90" with the "≥20" row as printed, the HALT recall sentences, and "whole days per one or 3 months". Some of these fragments are Stage 1 fragments | 0 | 0 |
| S-015 NICE CG150 | 49 | 49 (1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48; Overview population sentence; 12 Stage 1 fragments) | 0 | 0 |
| S-016 SIGN 155, S-018 AAN/AHS | 19 | 19 (S-016 PDF pp. 7, 20; S-018 pp. 1, 7, 8) | 0 | 0 |
| S-028 NVN | 12 | 4 Stage 1 fragments; 1 found in another tagged source; 1 is a translation; 4 are search-log text | 0 | 2 Dutch fragments on line 1152 (the population sentence and the section name "Zoeken en selecteren"), plus their echo "kinderen en volwassenen" on line 1165, which is counted under S-033 (tried as above) |
| S-029, S-030, S-032 | 6 | 6 (S-030 PDF p. 19) | 0 | 0 |
| S-033 Russian adults | 42 | 35 (p. 1 title; pp. 39, 40, 41, 53; p. 4 "М – мигрень"), 15 of them in other sources tagged on line 1165; 2 Stage 1 fragments; 4 are translations | 0 | 1 (the S-028 echo on line 1165, see S-028) |
| S-034 Russian children | 22 | 17. By script, 10 (p. 17; p. 52 flowchart). By hand, 1: "Возрастная группа" … "дети" on the rendered title page. Others: 2 in another tagged source; 4 Stage 1 fragments. The remaining 5 are 4 translations and 1 search-log entry | 0 | 0 |
| S-035 Turkish protocol | 30 | 24 (Kutu 8 PDF p. 48, second and seventh items; 3.6.3.9 p. 57; 3.3 b p. 23; section 6 heading p. 77); 6 are translations | 0 | 0 |
| S-101 HIT-6 | 7 | 4 (Methods, "Data sources"); 3 are search-log queries | 0 | 0 |
| S-102 MIDAS | 16 | 10 (Methods, "Headache impact on functioning" > "Migraine-related disability"); 6 are search-log text | 0 | 0 |
| S-103 PedMIDAS | 14 | 12 (grading table); 2 are search-log queries | 0 | 0 |
| S-104 HADS | 8 | 4; 4 are search-log queries | 0 | 0 |
| S-105 PHQ/GAD-7 | 4 | 4 (P. 6/9; developers sentence P. 8/9) | 0 | 0 |
| S-106 TA260 | 4 | 4 (chapter 2, para. 2.1; the chapter 1 "less than a 30% reduction" phrase of the search log) | 0 | 0 |

**Metadata.** PubMed esummary confirms the following:
- S-101: Yang M, Rendas-Baum R, Varon SF, Kosinski M; Cephalalgia 2011;31(3):357–67; 10.1177/0333102410379890; PMC3057423.
- S-102: Pavlović JM … Lipton RB; J Headache Pain 2015;16:24; 10.1186/s10194-015-0503-y; PMC4406925.
- S-104: Snaith RP; HQLO 2003;1:29; 10.1186/1477-7525-1-29; PMC183845.
- The PedMIDAS developer paper: PMID 11739822, 10.1212/wnl.57.11.2034.

Source types, years and access dates are as stated.

**Newer versions.**
- ICHD-3 (2018) is current: ICHD-4 exists only as "Work in Progress" papers (2024) and a 2025 workshop (web search).
- NICE CG150 shows the same last update, 3 June 2025.
- TA260 was last reviewed on 11 January 2016.
- Nothing newer changes an element.

### Value sets, codes, units, labels and thresholds (checked against the downloaded sources)

All are correct:
- ICHD-3 code labels (E-009) and the 8.2 reference levels 10/15 with "> 3 months" (E-032).
- 8.2.6 criterion B and note 2.
- A1.1 window "day 1 ± 2 (i.e. days −2 to +3)" and "there is no day 0" (E-060).
- Remission "must exceed three months" (E-063).
- HIT-6: 36–78 and four categories ≤49/50–55/56–59/60–78.
- MIDAS: grades I–IV, 0–5/6–10/11–20/≥21, "three months".
- PedMIDAS: 0–10/11–30/31–50/>50.
- HALT-90: 0–5/6–10/11–20/≥20; HALT-30 one month, no grading.
- HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21.
- IHS Q6: 50 %, 30 % alternative, MIDAS ≥5 points for 11–20 and ≥30 % for ≥20, HIT-6 ≥5.
- DMKG/ÖKSG/SKG: 50 %, 5 points, 30 %.
- IHS 2025 control levels (0; <4 for three months with pain-freedom at 2 h; 4–6; >6).
- The 17 evaluation-rule offsets, anchors and populations.
- NICE 1.3.48: 4–8 weeks.

### Fidelity to Stage 1 (all 39 requirements)

| OUT | Result |
|---|---|
| 001 | Represented at MUST: periods with dates and length (E-005, INV-002, INV-003); monthly frequency outputs (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); Caveat. No change. |
| 002 | SHOULD labels in every reporting form (INV-008); MUST ICHD-3 for headache days (INV-009, from OUT-004). No change. |
| 003 | SHOULD indicator (INV-011, INV-012); SHOULD NOT cut-off (INV-013). No change. |
| 004–008 | Levels and conditions match (INV-014 to INV-017, INV-108; OUT-008 MAY). No change. |
| 009 | Time course with markers and weekly values (INV-034 to INV-036). No change. |
| 010–013 | Intensity, duration with label and Caveat as SHOULD NOT, symptoms and MBS (also per attack), aura MAY. No change. |
| 014–016 | Totals, classes and drugs; weekly view; indicator with code, level, span and basis, prompt MUST, MUST NOT diagnosis. No change. |
| 017 | Follow-up view with window, year and worsening label. No change (the window values are already settled, review 11). |
| 018 | Comparison, changes, time points, Caveat as MUST NOT. **R14-01**: a guidance time point is missing. |
| 019–022 | Residual burden; responder labels; treatment review view MUST/SHOULD split; post-stop view. No change. |
| 023 | All named outcomes, timing, formulation, baseline/on-treatment split, 15 min, Caveat. The per-drug summaries of INV-071 are tied to their periods. See **R14-02** for summaries required elsewhere. |
| 024 | **R14-02**: an acute line's response summary is not tied to the treatment course. The rest of the list is represented. |
| 025, 039 | Scheme windows MAY; adherence next to the comparison, in the history and in the summary. No change. |
| 026, 027 | Instrument results with value sets; functional impact with baseline comparison. No change. |
| 028–030 | Three-month view; per-type outputs; menstrual-relation view. No change. |
| 031 | Bouts, remissions, rates, 15-minute effectiveness. **R14-02**: the period of the 15-minute summaries is not tied. |
| 032, 033 | Trigger view with caveats; screening results. No change. |
| 034 | **R14-02**: the per-medication effectiveness is not tied to the period the summary covers. The other components are represented. |
| 035 | Overview components. Optionally part of **R14-02** (the acute summary as treatment effect). |
| 036–038 | Paediatric outputs (v13 INV-098 trigger checked); composite index; caveats. No change. |

### Mechanical checks (scripts, on v13)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110): no gaps, no duplicate headings. Every `E-`/`INV-` reference resolves. ISS references resolve; ISS-07 is withdrawn and listed in section 9. S-101 to S-106 are cited and listed. |
| Realises and Conformance | Present in every element and invariant. Every OUT ID referenced exists in Stage 1. |
| Traceability | 39 rows in Stage 1 order, with none missing and none extra. For every OUT, the row's element and invariant sets equal the sets derived from the Realises fields. |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Scopes: output 77, repertoire 32, context 1. All 10 MUST NOT / SHOULD NOT predicates have the form `¬ F`. |
| Names in `omn` blocks | No undeclared name. The 14 flags are tags of the two variants written with a line break after `::=`, and they are declared. No duplicate type, function, predicate or constant declaration. |
| Partial terms (by hand) | `÷`, `days`, `first`/`last`, `max`/`min`, `s(i)`, `classOf`, `periodEndFrom`, `publishedRecall` and `scoreRange` are guarded at every use, including the v13 changes (INV-039, INV-069, INV-071, INV-088, INV-098, INV-104, INV-105, INV-109, INV-110). |

### Scope sweep

- A grep for enter-, record-, captur-, input, stor-, persist-, database, serializ-, JSON/XML/FHIR/CSV/HL7, encod-, retention, reminder, data field and "answers" returns only:
  - the scope statements of sections 1 and 2.1;
  - the S-014 quote on the HALT-30 recall period, whose substance is the recall;
  - two notes saying that scoring from answers is out of scope;
  - INV-076 Notes, which state that a derivation from input is not made.
- Every formula and threshold in the invariants has output elements, constants or applicability properties of the context as its arguments.
- Every derived attribute has its relation or is marked as obtained from diary information.

## Remarks

### R14-01 Coverage gap: an evaluation time point of the Turkish protocol (section 7.3, botulinum toxin) is missing from the rule list, which the model states to be complete

- Item(s):
  - E-041: the rule list `evaluationRules`, and the Notes **The rule list**, **Named, but not evaluation time points**, **Types and exclusions** and **Readings**;
  - through E-041: INV-055, INV-058 and INV-059;
  - section 7, row OUT-018;
  - ISS-10 (the list of rules that can apply to a treatment started in childhood).
- Problem:
  - OUT-018 (MUST) requires the comparison "at the evaluation time points named in current guidance, which differ by treatment type (for example [...] after onabotulinumtoxinA cycles)".
  - The model states that its rule list is complete for the guidance Stage 1 cites, read in full. The Turkish Ministry of Health protocol [S-035] is one of that guidance.
  - The protocol names two evaluation statements for botulinum toxin type A. The model has one of them, section 3.6.3.9, "after 3 injection cycles" (`ruleTr3639`).
  - It does not have the other: section 7.3 requires at least two administrations, at 3-month intervals, before the effect is evaluated.
  - This passage appears nowhere in the model: not as a rule, not among "Named, but not evaluation time points", and not in the `excludes` analysis. A search of all review, fix and oscillation files finds no mention of section 7.3, "Botulinum Toksin Enjeksiyonu", "en az 2" or p. 86.
  - So three statements are wrong:
    - the completeness claim in E-041 Notes;
    - the claim in row OUT-018;
    - the statement that the `excludes` criterion "is applied to every rule".
  - A time point named in current guidance is either missing or not accounted for.
- Evidence:
  - [S-035] Stage 1 URL (`Migren Klinik Protokolü (Revizyon) (92 Sayfa).pdf`), chapter 7 "MİGRENDE GİRİŞİMSEL İŞLEMLER", section 7.3 "Botulinum Toksin Enjeksiyonu", PDF p. 86 (printed p. 76). Text layer and rendered page agree. The bulleted items read:
    - "Kronik migren hastalarında endikasyon vardır," (second item). Translation: "It is indicated in patients with chronic migraine,"
    - "Uygulanım yeri ve dozu: frontal, temporal, oksipital ve servikal bölgeler, 31 nokta, her noktaya 5 ünite (toplam 155 ünite), 3 ay aralıklarla," (third item). Translation: "Site and dose of administration: frontal, temporal, occipital and cervical regions, 31 points, 5 units per point (155 units in total), at 3-month intervals,"
    - "Etkisini değerlendirmek için en az 2 k ez uygulanmalıdır," (fourth item; the space inside "kez" is printed so on the page). Translation: "To evaluate its effect, it should be administered at least 2 times,"
    - "Bir yılın sonunda ağrı sıklığı ve şiddetinde azalma gözlenen hastalarda uygulama süreleri uzatılabilir." (fifth item). Translation: "In patients in whom a reduction in pain frequency and severity is observed at the end of one year, the application intervals may be extended." This one is an injection-interval statement, not a time point.
  - The model's claims:
    - E-041 Notes: "The rule list is the set of evaluation time points for a person's preventive treatment that the guidance which Stage 1 cites for OUT-018 names in its recommendations and guidance text, read in full and not only in the passages Stage 1 quotes: [...] and the Turkish Ministry of Health protocol [S-035]".
    - Row OUT-018: "The time points are all those that the guidance cited in Stage 1 for OUT-018 names for evaluating a person's preventive treatment, read in full".
    - E-041 Notes, **Types and exclusions**: "One criterion decides the members of `excludes`, and it is applied to every rule of the list".
  - The model's rule values show that a statement of this kind ("at least two administrations before evaluation") counts as an evaluation time point:
    - NICE CG150 1.3.29, "after 2 treatment cycles", is `ruleNice1329`, with `endOfCycleAnchor(2)`;
    - minimum wordings ("минимум через 6 месяцев", "wait 24 weeks [...] before assessing efficacy") are modelled as `atLeastOffset` rules (`ruleRu33Bta`, `ruleAan14B`).
  - Precedent: R01-01 and R07-01 found time points missing from the same list, and both were fixed by adding rules.
  - I searched the other cited guidance in full for similar omissions and found none:
    - SIGN 155 (all 64 PDF pages: only the two section 4.1 time points and the checklist consultations);
    - the AAN/AHS Clinician Summary (14A, 14B; 14C, 14D, 14H as noted);
    - IHS 2024 (Q2, Q4, Q5, Q6 Background as noted);
    - EHF 2022 (question 3 and its "additional period of 3 months", as noted);
    - NICE CG150 Recommendations page;
    - the Russian adult and paediatric recommendations (pp. 39–41, 53; pp. 30, 52, 53);
    - the rest of the Turkish protocol (Kutu 8, 3.6.3.9, 6.2.2, p. 48 "Remisyonda tedavi tekrar değerlendirilmeli").
  - NVN [S-028] could not be searched (unreachable).
- Required change: account for section 7.3 in E-041, by one of the following.
  - **(a)** Add a rule, for example `ruleTr73`:
    - guidance "Turkish Ministry of Health Migraine Clinical Protocol 2025, section 7.3 (botulinum toxin injection)";
    - `headacheType ↦ c1`, `ages ↦ anyAge` (no age is stated, as for Box 8 and 3.6.3.9);
    - `appliesTo ↦ {onabotulinumtoxinA}`, `anchor ↦ endOfCycleAnchor(2)`, `timing ↦ atLeastOffset`, `minOffset ↦ weeks(0)`;
    - with the verbatim quote, translation and location above, added to `evaluationRules`.

    Then apply the `excludes` criterion to it and state the result. As written, the criterion would put `onabotulinumtoxinA` into `ruleTr73.excludes`, because the same guidance gives the type a later time point in a rule of its own (3.6.3.9, after 3 cycles). The new rule would then apply to no treatment. If the fixer finds that result wrong (both are the guidance's own time points for the type), refine the criterion with a stated reason, applied to every rule.
  - **(b)** If the fixer concludes that "at least 2 administrations" names no evaluation time point of its own, list section 7.3 under **Named, but not evaluation time points** (or in **Types and exclusions**). Give the verbatim quote, translation, location and the reason, for example that it is a minimum which the guidance's own later time point after 3 cycles (3.6.3.9) satisfies.

  In both cases:
  - correct the completeness statements in E-041 Notes and row OUT-018;
  - extend the "every rule except NICE 1.3.29 and Turkish section 3.6.3.9" sentences (E-041 Notes, E-043 Notes, INV-055 Notes) if a rule anchored at the end of a cycle is added;
  - update ISS-10 and the change log if a rule is added;
  - add the injection-interval item (fifth bullet) to the "course lengths and injection intervals" list.

  Watch point 1 is not touched: `ruleTrBox8.excludes`, `ruleNice1327.excludes` and every existing `timing` stay unchanged. Box 8's exclusion rests on 3.6.3.9, and a time point at the end of the second 3-month cycle also lies after Box 8's 2–3-month window. Adding a rule with new evidence reverses no earlier fix.

### R14-02 Coverage gap: the period of the acute-treatment summaries required by INV-109, INV-104 and INV-088 (and INV-105) is unconstrained, so they can be met by summaries of periods in which the medication was not taken

- Item(s):
  - INV-109 (with INV-079 and E-055 `acuteResponse`);
  - INV-104 (E-066);
  - INV-088 (E-062 `acute`);
  - optionally INV-105 (E-067);
  - section 7, rows OUT-023, OUT-024, OUT-031, OUT-034 (and OUT-035).
- Problem: four requirements ask for an acute-treatment summary (E-051) of a medication but fix only its drug, type scope, time point or outcomes. None fixes its period.
  - INV-109 with INV-079: the response summary of an acute treatment line needs only `s.drug = l.drug` and one summary with `s.typeScope = allTypes`. It is not tied to the treatment course whose start, stop and duration the same line shows.
  - INV-104: the clinician-facing summary needs, for each acute medication, `∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.drug = m.drug ∧ s.typeScope = allTypes`, for any period. Every other per-period component of INV-104 is tied to `v.covers`, including the acute-medication days by drug.
  - INV-088: the cluster view of the selected time range needs, for each acute medication, a 15-minute summary with the rescue outcome, for any period.
  - INV-105: the treatment effect may be an acute summary of any period.

  A summary of a period in which the drug was not taken has 0 treated attacks. INV-072 and INV-074 explicitly admit that, and so do INV-003, INV-011 and INV-073. It therefore satisfies these SHOULD constraints while it reports none of the effectiveness that OUT-023, OUT-024, OUT-031 and OUT-034 ask for.
  - This is the R13-01 defect on another dimension. R13-01 showed that INV-071 was met by "a sumatriptan summary scoped `ofType(c2)` with 0 treated attacks". Fix 13 constrained the type scope of these same requirements but not their period.
  - Elsewhere the model ties the period of every required acute summary: the selected time range (INV-071), the baseline and on-treatment periods (INV-069, INV-071), and the evaluated and baseline periods (INV-062). The preventive counterpart of the line's response summary, the response comparison, is aligned to the treatment start (INV-056, INV-079 `r.treatment = l.treatment`).
- Evidence:
  - The predicates:
    - INV-109: `(l.role = acute ⇒ ∃ s ∈ l.acuteResponse • s.typeScope = allTypes)`;
    - INV-079: `(∀ s ∈ l.acuteResponse • s.drug = l.drug)`;
    - INV-104: `(∀ m ∈ ctx.subject.acuteMedications • ∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.drug = m.drug ∧ s.typeScope = allTypes)`;
    - INV-088: `(∀ m ∈ c.subject.acuteMedications • ∃ s ∈ v.acute • s.drug = m.drug ∧ scopeFor(c, s.typeScope, c3_1) ∧ s.earlyTimePoint = fifteenMinutes ∧ ∃ os ∈ s.outcomes • os.measure = rescueOrRepeatMedication)`;
    - INV-105: `… ∨ ∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.typeScope = allTypes`.
  - The model's own Reading of INV-104: "The clinician-facing summary is concise and brings together, for the period it covers: [...] the effectiveness of each acute medication over all headache types combined".
  - Stage 1:
    - OUT-024 "the response summary from OUT-018 or OUT-023 for each treatment", with "start and stop dates [...] treatment duration", and the formulation "so that [...] the EHF definition of triptan refractoriness [S-012] can be applied";
    - OUT-023 "For each acute medication, the diary output SHOULD report, across the attacks treated with it, the outcome measures";
    - OUT-034 "a concise clinician-facing summary for the period since the previous consultation (or a period chosen by the clinician) that brings together [...] current and past treatments with response (OUT-018, OUT-023, OUT-024)";
    - OUT-031 "for acute treatments, effectiveness at 15 minutes and the need for rescue treatment".
  - The model's acute treatment courses have dated starts and stops (E-008: "every acute treatment course of the subject up to the as-of date, ongoing or stopped"; `courseEvents` cover "start [...] and stop of each treatment"; INV-001 covers acute treatments). So the span of a course is available as for preventive treatments.
  - An example admitted by v13:
    - The subject took oral sumatriptan as an acute course from 1 January 2020 to 31 December 2021 (stopped), and rizatriptan from 2022 onward. The as-of date is 20 October 2026.
    - In the treatment history view, the sumatriptan line shows the dates 2020–2021, the duration and the formulation. Its `acuteResponse` is a sumatriptan summary, all types, for 1–28 September 2026, with 0 treated attacks, 0 attacks assessed in every outcome summary and no lines.
    - INV-072, INV-073, INV-074, INV-079, INV-109, INV-003 and INV-011 all hold.
    - The line shows no response of the course it lists, so the triptan history that OUT-024 provides for the EHF definitions is empty.
  - In the same way, a clinician-facing summary of 15 August – 20 October 2026, or a cluster view of January–March 2026, meets its acute-effectiveness requirement with summaries of March 2019.
  - No earlier remark or fix decided that these periods should stay free. The fix-11 co-presence table created INV-109 without a period condition. Fix 13 addressed only the type scope.
- Required change: tie the period of these summaries to what Stage 1 names, and align the Readings, the Conformance of E-055, E-062, E-066 and E-067, and the rows.
  - **(a) INV-109.** For an acute line of a treatment that has a start, require at least one summary over all headache types combined whose period is the span of the course. That span runs from its start to its stop or, if it has not stopped, to the as-of date, which is the span INV-079 already uses for the duration. A weaker alternative: a summary whose period lies within that span and contains its last treated attack. Optionally, also require that a single-formulation summary of the line names one of the formulations the line shows.
  - **(b) INV-104.** Require the per-medication summaries for the period the clinician-facing summary covers (`s.period = v.covers`), as its acute-medication days by drug already are. The responses of past courses are then shown by the treatment lines, which INV-104 requires for every treatment and which (a) ties to their courses.
  - **(c) INV-088.** Require the 15-minute summaries for the period the cluster view covers (`s.period = v.covers`, which is the selected time range), as INV-071 does for the time range.
  - **(d) Optionally, INV-105.** Require the acute summary shown as treatment effect for the overview's covered period, or for a period within it.

  Satisfiability:
  - each required period can be added to the view (INV-002, INV-003), with its completeness indicator (INV-011);
  - a summary of a period without treated attacks shows 0 attacks (INV-072, INV-074);
  - INV-073 and the type-scope conditions of fix 13 are unchanged.

  Watch points: this keeps the R11-02 per-drug requirement, the R13-01 type scopes, `#L.evaluated = 1` and the INV-062 period ties. It touches no E-041 value, no co-presence item of watch point 3 and no time-frame component of watch point 6.

## Checked and not raised

- **The v13 changes.**
  - The R13-01 type scopes (INV-039, INV-062, INV-069, INV-071, INV-104, INV-105, INV-109) are consistent with INV-073 and INV-088. `scopeFor` with all types implies `onlyOfType`, which gives 15 minutes, as INV-088 requires.
  - INV-098 (`childIn` over `{v.covers} ∪ (v.content ∩ Period)`) is well typed and satisfiable.
  - INV-110 is consistent with INV-003 and INV-011.
- **Section 3.3 item 2 and the three `set … MUST` attributes of `CycleLine`** (`menstruationDays`, `migraineDays`, `attacks`). The first sentence (with `when` optional) would make them non-empty at MUST, and cycles without migraine would then be unshowable. The second sentence ("An attribute of level `MUST` without `when`, or of level `core`, is present by typing") governs them, as it governs the `core` sets (`claims`, empty "in the normal case"). INV-087's explicit `cl.menstruationDays ≠ ∅` for lines that show day 1 confirms that reading. Not ambiguous enough to raise.
- **Subject-profile components used beyond applicability** (course-event dates in INV-036, INV-058 and INV-079; medication history in INV-046 `classUseExcluded`). These are facts about the subject's treatments and medications, stated as properties of the output's subject (PROCESS section 2, "Conditions of applicability"), and used for identity with shown dates or for consistency of an indicator. They are not formulas over recorded diary data. Not raised (watch point 6; review 01's watch).
- **OUT-023 for cluster headache.** The 24-hour measures are kept with the 15-minute time point, as OUT-023 states ("the corresponding time point is 15 minutes"). [S-007] pairs 15 minutes with "within 3 hours" for its primary endpoint. The model follows Stage 1 and works nothing around, so this is no section 8 omission.
- **OUT-019 and moderate/severe headache days.** INV-060 asks for the residual burden next to percentage changes in migraine days and headache days only, as OUT-019 words it. In a response comparison, the residual burden is shown anyway through the migraine and headache-day changes (INV-056, INV-061).
- **Migraine days not broken down by headache type in INV-028.** The INV-028 Notes give a reason ("by definition migraine-specific"), and no Stage 1 example requires it.
- **Settled questions not reopened (no new evidence):**
  - the OUT-017 review-window values (review 11);
  - the monthly baseline of E-043 (R01-03);
  - INV-023 at any granularity;
  - the "> 3 months" readings;
  - MIDAS label choice and Grade IV subdivision;
  - HIT-6 one-month recall;
  - "baseline administration" as any earlier administration;
  - R10b-01 and R11-01 (a)/(b) (watch point 3);
  - INV-091 to INV-093 with `concerns`;
  - INV-105 "treatment effect" by one item;
  - the E-041 timings and `excludes` values (watch point 1);
  - INV-087 and the lead-in (watch point 4);
  - INV-049/INV-050 (watch point 5).
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded. I re-verified:
  - 8.2.6 criterion B (p. 124);
  - "simple analgesics" only on p. 139;
  - NICE 1.3.9 and 1.3.39 without a review time point;
  - 1.3.48 and the CG150 population;
  - the [S-034] flowchart (p. 52).

  No Stage 1 issue is silently worked around. R14-01 concerns the model's rule list, not Stage 1. If R14-01 is fixed by adding a rule, ISS-10's list of rules for children needs the addition.
- **Search log and sources.** The S-103 footer, the S-105 PDF metadata, the TA260 dates and the PubMed metadata are as stated.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and no item of v13 carries a FROZEN marker.
