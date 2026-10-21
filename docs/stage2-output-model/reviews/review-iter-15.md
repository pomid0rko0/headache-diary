# Review — iteration 15
VERDICT: REMARKS
REMARK_COUNT: 3
Reviewed version: v14
Date: 2026-10-21

## Summary

This is the main review of iteration 15: an independent fact-check and review of v14. `OUTPUT_MODEL.md` is byte-identical to `history/v14.md` (checked with `cmp`).

**What I read in full:**
- Stage 2 PROCESS.md;
- Stage 1 v18, sections 1–3 (OUT-001 to OUT-039, with OUT-039 after OUT-025), and section 5;
- v14: every element, every invariant, and sections 7 to 12;
- review 14, fix 14 and the word-level v13 → v14 diff;
- the oscillation check after iteration 12 and its seven watch points;
- the parts of earlier reviews and fixes that touch my topics: fix 02 item 14 (INV-060/INV-061), review 02 (baseline alignment), fixes 11, 13 and 14 (co-presence table, "treatment effect" by one item, the formulation scope noted twice and left open).

**Earlier decisions.** FROZEN_ITEMS.md does not exist, and no item carries a FROZEN marker. None of my remarks reverses an earlier fix or re-raises a declined remark. Each remark states its relation to the watch points.

**Result.**
- **Citations.** No defect. Every reachable fragment is verbatim at its stated location. This includes the seven new [S-035] fragments of v14 (PDF pp. 57, 82–86, 83), which I also read on the text layer of p. 86 and in context. 9 fragments of S-007 and S-028 could not be re-checked because both sites were unreachable again. They are unchanged since v05/v06 and were verified by reviews 05–11.
- **Value sets, codes, labels, thresholds, offsets.** No defects. This includes the new rule `ruleTr73` and the refined `excludes` criterion, which I applied to all 18 rules.
- **Mechanical checks.** All pass.
- **Scope sweep.** No input, storage or derivation-from-input content.
- **Three remarks.** All three are coverage gaps of the kind that R13-01 and R14-02 fixed: a dimension of a required item is left free, so the requirement can be met by an item that shows none of what Stage 1 asks for.
  - **R15-01 (OUT-020, OUT-021, OUT-023, OUT-024, OUT-031, OUT-034).** The per-drug acute-treatment summaries required by INV-062, INV-069, INV-071 (second conjunct), INV-088, INV-104 and INV-109 do not fix their formulation scope. Example: for a drug used both orally and subcutaneously, one oral-only summary meets the requirement for both medications. Fixes 13 and 14 noted this ("same class") and left it open because of the per-drug vs per-medication reading. Both readings exclude these outputs.
  - **R15-02 (OUT-039).** The adherence summary that INV-066 puts next to each response comparison must end with an on-treatment period, but its start is free. A one-day window therefore meets the requirement, and it shows nothing about intake over the evaluated period.
  - **R15-03 (OUT-035).** v14 tied the acute alternative of the overview's "treatment effect" (INV-105) to the covered period, "so that the effect the patient follows is that of the period the overview shows, not of an earlier one". The response-comparison alternative of the same disjunction is still free. A comparison of a preventive treatment stopped years before the covered period meets it.

## Verification coverage

### Method

- **Downloads.** All were made with `curl` (through the configured proxy) into the fresh directory `r15dl/` of the session scratchpad, outside the repository.
  - **Stage 1 URLs (HTTP 200):**
    - PDFs: S-001 (211 pp.), S-002 (19), S-003 (18), S-005 (14), S-008 (31; the first attempt failed with a broken pipe and the retry succeeded), S-010 (11), S-016 (64), S-018 (12), S-030 (86), S-033 (92), S-034 (53; the first attempt was reset by the peer and the retry succeeded), S-035 (92; created 28 August 2025);
    - S-015: the Recommendations page (`datetime` 2012-09-19 and 2025-06-03) and the Overview page.
  - **Europe PMC full-text XML (HTTP 200):** S-011 (PMC9188162), S-012 (PMC9555163), S-013 (PMC7296705), S-014 (PMC6734476), S-023 (PMC9607711), S-042 (PMC12279330), S-101 (PMC3057423), S-102 (PMC4406925), S-104 (PMC183845).
  - **Other new-source pages (HTTP 200):**
    - S-103 (footer "© 2026 Cincinnati Children's Hospital Medical Center");
    - S-105 (9 pp.; PDF metadata: author Kurt Kroenke, created 2010-06-22, modified 2014-04-16);
    - S-106: chapter 2, chapter 1 (for the search-log phrase) and the overview page ("Last reviewed: 11 January 2016", published 27 June 2012).
  - **Unreachable:**
    - S-007: UCL Discovery returned HTTP 503 "Temporary disruption | UCL" for both URL forms. web.archive.org reset the connection.
    - S-028: richtlijnendatabase.nl returned HTTP 200 twice, both times with the page "Deze pagina is tijdelijk niet bereikbaar … vanwege onderhoudswerkzaamheden". web.archive.org reset the connection.
- **Extraction.**
  - PDFs were extracted page by page with `pdftotext -raw` and `-layout`. HTML and XML were stripped of scripts and markup, and entities were unescaped.
  - Rendered with `pdftoppm` and read by eye:
    - ICHD-3 p. 190: the A1.1.1 and A1.1.2 windows "day 1 ± 2 (i.e. days −2 to +3)", whose "±", "−" and "+" have no text mapping;
    - the S-034 title page, an image that reads "Возрастная группа" followed by "дети".
- **Scripts.** All are in the session scratchpad, `r15/`, and were run with `python3 -I`:
  - `quotes.py`: every double-quoted string outside `omn` blocks on a line with an `[S-NNN]` tag, split at `[...]` and "…", 473 fragments. Each fragment is searched in three normalisation passes (NFKC, quotes, dashes and whitespace; line-end hyphens; letters and digits only), first in its tagged source page by page, then in the other sources tagged on the line, then in Stage 1 v18;
  - `mech.py`: headings, references, traceability, levels, scopes, prohibition form;
  - `names.py`: declarations and uses of names and attribute selections in `omn` blocks;
  - `html2txt.py`;
  - an inline check of the attribute levels and the typing rule.
- **Newer versions.**
  - No final ICHD-4 exists; there are only the 2024 "Work in Progress" paper and the 2025 workshop (web search).
  - The NICE CG150 page still shows its last update as 3 June 2025.
  - TA260 was last reviewed on 11 January 2016.
  - Nothing newer changes an element.

### Citations

| Source | Fragments | Verified verbatim | Not found | Unreachable (what was tried) |
|---|---|---|---|---|
| S-001 ICHD-3 | 65 | 64. By script, 57: labels pp. 8, 9, 12; 8.2–8.2.8 pp. 122–125; 8.2.3 comment p. 123; "Definitions of terms" pp. 209–210; remission p. 209; A1.1 note 2 p. 190. By hand on the rendered p. 190, 3: the two window fragments and their echo in INV-087. As Stage 1 fragments, 4. The remaining 1 is a search-log row label. "Simple analgesics" occurs only on p. 139 (ISS-02). | 0 | 0 |
| S-002, S-003, S-005 | 14 | 14. By script, 10 (S-002 PDF pp. 10–12, i.e. printed pp. 1035–1037). As Stage 1 fragments, 4 | 0 | 0 |
| S-007 IHS cluster | 10 | 6 (Stage 1 fragments, checked against Stage 1 v18) | 0 | 4 (the E-064 fragment "a persistent high attack frequency (e.g. ≥ 14 attacks per week on average)", its section title and its two echoes; tried as above) |
| S-008 IHS 2024 | 28 | 28. Q2 pp. 5, 9; Q4 p. 11; Q6 pp. 6, 12; Q6 Evidence p. 13; Q13 p. 17; the "acceptable for treatment continuation beyond three months" echoes of E-008 and E-045 (p. 12) | 0 | 0 |
| S-010 IHS 2025 | 44 | 44. 36 at p. 6: the four control levels, both migraine-day sentences, the "proxy" sentence, and the insufficient-control sentence across the running header. 8 are Stage 1 fragments | 0 | 0 |
| S-011, S-014, S-023, S-030, S-042 | 60 | 60. S-014 includes the HALT recall sentences, "whole days per one or 3 months" and Table 18 "Grading of HALT-90" with its "≥20" row. 9 S-014 fragments are Stage 1 fragments. 1 fragment on an S-014 line is the S-008 phrase "acceptable for treatment continuation beyond three months", found in S-008 p. 12 | 0 | 0 |
| S-015 NICE CG150 | 49 | 49 (1.3.9, 1.3.24, 1.3.26–1.3.29, 1.3.39, 1.3.48; Overview population sentence; 12 Stage 1 fragments) | 0 | 0 |
| S-016 SIGN 155, S-018 AAN/AHS | 19 | 19 (S-016 PDF pp. 7, 20; S-018 pp. 1, 7, 8) | 0 | 0 |
| S-028 NVN, S-029, S-032 | 14 | 9 Stage 1 fragments, including the [S-028] Aanbeveling fragments of E-041. 1 is a translation | 0 | 4 Stage 2 fragments, plus their echo "kinderen en volwassenen" in the E-041 Notes: the PICO sentence of "Zoeken en selecteren" and the section name (tried as above) |
| S-033 Russian adults | 45 | 40. By script, 38: p. 1 title; p. 4 "М – мигрень"; pp. 39, 40, 41, 53; some found in other sources tagged on the same line. As Stage 1 fragments, 2. The remaining 4 are translations | 0 | 1 (the S-028 echo, counted above) |
| S-034 Russian children | 22 | 18. By script, 12 (p. 17; p. 52 flowchart). By hand on the rendered title page, 2. As Stage 1 fragments, 4. The remaining 4 are translations | 0 | 0 |
| S-035 Turkish protocol | 50 | 37 by script: Kutu 8 p. 48 (second and seventh items); 3.3 b p. 23; 3.6.3.9 p. 57 (evaluation, interval and the new dose sentence); section 6 heading p. 77; chapter 7 heading pp. 82–86; 7.1 p. 83 (both new sentences); 7.3 p. 86 (items 3, 4 and 5, "2 k ez" as printed). The other 13 are translations | 0 | 0 |
| S-101 to S-106 | 53 | 38. S-101: "Data sources", 4. S-102: "Migraine-related disability", 10. S-103: grading table, 12. S-104, 4 (one is a Stage 1 fragment). S-105: P. 5/6–6/9, developers sentence P. 8/9, 3. S-106: chapter 2 para. 2.1, plus the chapter 1 phrase "less than a 30% reduction in headache days per month after 2 treatment cycles" (searched in the downloaded chapter 1), 5. The remaining 15 are search-log queries | 0 | 0 |
| **Total** | **473** | **426 verified** (360 by script in the downloaded sources; 6 by hand: 3 on the rendered ICHD-3 p. 190, 2 on the rendered S-034 title page, 1 in TA260 chapter 1; 60 as Stage 1 v18 fragments); 22 are translations, 16 are search-log text | **0** | **9** (S-007, S-028) |

**Translations.** Every new translation was checked against the source text, including the four [S-035] translations new in v14:
- "Uygulanım yeri ve dozu … 3 ay aralıklarla" (at 3-month intervals);
- "Etkisini değerlendirmek için en az 2 k ez uygulanmalıdır" (to evaluate its effect, it should be administered at least 2 times);
- "Bir yılın sonunda … uygulama süreleri uzatılabilir" (application intervals may be extended);
- the 7.1 nerve-block sentences.

All are faithful.

**Metadata.** PubMed esummary confirms the following:
- S-101: Yang M, Rendas-Baum R, Varon SF, Kosinski M; Cephalalgia 2011;31(3):357–67; 10.1177/0333102410379890; PMC3057423.
- S-102: Pavlović JM … Lipton RB; J Headache Pain 2015;16:24; 10.1186/s10194-015-0503-y; PMC4406925.
- S-104: Snaith RP; HQLO 2003;1:29; 10.1186/1477-7525-1-29; PMC183845.
- The PedMIDAS developer paper: PMID 11739822; 10.1212/wnl.57.11.2034.

Types, years, URLs and access dates are as stated.

### Value sets, codes, units, labels and thresholds

All were checked against the downloaded sources, and all are correct:
- ICHD-3 code labels (E-009);
- the 8.2 reference levels 10/15 with "> 3 months" (E-032), and 8.2.6 criterion B and note 2;
- the A1.1 window and "there is no day 0" (E-060);
- remission "must exceed three months" (E-063);
- HIT-6: 36–78, ≤49/50–55/56–59/60–78;
- MIDAS: I–IV, 0–5/6–10/11–20/≥21, three months;
- PedMIDAS: 0–10/11–30/31–50/>50;
- HALT-90: 0–5/6–10/11–20/≥20; HALT-30 one month, no grading;
- HADS 0–21 per subscale; PHQ-9 0–27; GAD-7 0–21;
- IHS Q6: 50 %, the 30 % alternative, MIDAS ≥5 points for baseline 11–20 and ≥30 % for ≥20, HIT-6 ≥5;
- DMKG/ÖKSG/SKG: 50 %, 5 points, 30 %;
- NICE 1.3.28 (50/30 %), 1.3.29 (30 %) and the Russian 7.1 criterion (50 %);
- the IHS 2025 control levels;
- NICE 1.3.48: 4–8 weeks.

**Evaluation rules (E-041).** All 18 rules were checked against their sources: offsets, anchors, timings and populations.
- **`ruleTr73`:**
  - `{onabotulinumtoxinA}`: the 7.3 dose "155 ünite … 31 nokta" equals the 3.6.3.9 onabotulinumtoxin A dose;
  - `endOfCycleAnchor(2)`, `atLeastOffset`: "en az 2 kez";
  - `anyAge`;
  - `c1`: the chapter heading "7. MİGRENDE GİRİŞİMSEL İŞLEMLER".
- **The refined `excludes` criterion.** I applied it to all 18 rules, and it reproduces every stored value:
  - 14A, Russian 7.1 and Box 8 exclude onabotulinumtoxinA;
  - NICE 1.3.27 excludes nothing (12 weeks lies before its window, 24 weeks within it);
  - every rule named for particular types has ∅.
- **Rule list complete.** I re-searched the cited guidance for evaluation time points missing from the rule list, the class of R14-01, and found none beyond those E-041 lists:
  - S-033: "через", "в течение", "минимум", "не менее";
  - S-035: "değerlendir", "etkinli", and month and week counts;
  - S-016: weeks, months and cycles near "assess", "review" and "effect";
  - S-008: Q2–Q13;
  - the S-015 Recommendations page.

### Fidelity to Stage 1 (all 39 requirements)

| OUT | Result |
|---|---|
| 001 | Periods with dates and length at MUST (E-005, INV-002, INV-003); monthly frequency outputs (INV-014, INV-015, INV-108); equal-length comparisons (INV-037, INV-055); Caveat. OK. |
| 002 | SHOULD labels in every reporting form (INV-008); ICHD-3 for headache days at MUST (INV-009, from OUT-004). OK. |
| 003 | SHOULD indicator for every summarised period (INV-011, INV-012); SHOULD NOT cut-off (INV-013). OK. |
| 004–008 | Levels and conditions match (INV-014 to INV-017, INV-108; OUT-008 MAY). OK. |
| 009 | Time course with markers in the view and weekly values (INV-034 to INV-036). OK. |
| 010–013 | Intensity on a stated scale with comparison; duration with label and Caveat (SHOULD NOT); symptoms and most bothersome symptom across periods and per attack; aura MAY. OK. |
| 014–016 | Total, classes and drugs; weekly view; indicator with code, level, span and basis, prompt at MUST, diagnosis at MUST NOT. OK. |
| 017 | Follow-up view with window, year and worsening label. OK. |
| 018 | Comparison, changes, time points (18 rules), Caveat at MUST NOT. OK (R14-01 fixed; checked above). |
| 019 | Residual burden next to percentage changes (INV-060, INV-061). OK. |
| 020 | Label, criterion, values, decidable components, not sole indicator, no continuation decision. **R15-01**: the acute-treatment effectiveness the label rests on is not tied to formulation. |
| 021 | MUST/SHOULD split; acute effectiveness for the same periods. **R15-01** (INV-069, INV-071). |
| 022 | Post-stop view with on-treatment and baseline periods. OK. |
| 023 | All named outcomes, timing, formulation, baseline/on-treatment split, 15 minutes, Caveat. The time-range summaries of INV-071 are tied to formulation. **R15-01** for the per-phase summaries. |
| 024 | History with dates, dose changes, duration, response, adverse effects, stop reason, formulation; course summary tied to the span (v14). **R15-01** (course summary formulation). |
| 025 | MAY scheme windows. OK. |
| 039 | Adherence next to the comparison, in the history and in the summary. **R15-02**: the window is not tied to the evaluated period. |
| 026, 027 | Instrument results with value sets; functional impact with baseline comparison. OK. |
| 028–030 | Three-month view; per-type outputs; menstrual-relation view. OK. |
| 031 | Bouts, remissions, rates, 15-minute effectiveness of the covered period (v14). **R15-01** (formulation of the 15-minute summaries). |
| 032, 033 | Trigger view with caveats and dates in its period; screening results. OK. |
| 034 | All components; acute effectiveness of the covered period (v14). **R15-01**. |
| 035 | Overview components. **R15-03**: the response-comparison alternative of "treatment effect" is not tied to the covered period. Optionally **R15-01** for the acute alternative. |
| 036–038 | Paediatric outputs; composite index; caveats. OK. |

### Mechanical checks (scripts, on v14)

| Check | Result |
|---|---|
| IDs | 67 elements (E-001 to E-067) and 110 invariants (INV-001 to INV-110), with no gaps and no duplicates. Every E- and INV- reference resolves. ISS references resolve; ISS-07 is referenced only as withdrawn (section 9). S references lie in S-001–S-046 or S-101–S-106, and S-101 to S-106 each have a row. Every OUT reference exists in Stage 1. |
| Realises and Conformance | Exactly one of each in every element and invariant. |
| Traceability | 39 rows in Stage 1 order (OUT-039 after OUT-025). For every OUT, the row's element and invariant sets equal the sets derived from the Realises fields. All rows say "full". |
| Invariant levels | MUST 19, MUST NOT 2, SHOULD 48, SHOULD NOT 8, definitional 33. Scopes: output 77, repertoire 32, context 1. All 10 MUST NOT / SHOULD NOT predicates begin with `¬`. These match the v14 change log. |
| Attribute levels | 172 level-annotated declarations (core 94, MUST 29, SHOULD 47, MAY 2), as stated. The typing rule holds: every SHOULD, MAY or MUST-with-`when` attribute has an `opt`, `set` or `seq` type. |
| Names in `omn` blocks | No duplicate declaration. Every attribute selection names a declared attribute or component. The only names without an `omn` declaration are:<br>• `c`, the free context variable of INV-001 (section 2.9);<br>• `sc`, bound by `∀ sc ∈` in INV-028, which the regex missed;<br>• `refs`, defined in section 2.5. |
| v14 changes (by hand) | Well typed, with partial terms guarded:<br>• INV-109: `l.stopDate` is used inside a quantifier; precedence as intended;<br>• INV-104 and INV-088: `s.period = v.covers` (both `→Period`);<br>• INV-105: `within(s.period, v.covers)`;<br>• `ruleTr73`: in the `const` list, the axiom and `evaluationRules`.<br>`fitsMonthlyPeriod` holds for `ruleTr73` wherever the second cycle ends at least 27 days after the start. |

### Scope sweep

- A grep for enter-/entry, record-, input, captur-, logged, stor-, persist-, database, JSON/XML/CSV/FHIR/HL7, serializ-, encod-, retention, reminder, answer, data field, algorithm and "obtained from" returns only:
  - the scope statements of sections 1, 2.1, 2.7 and 3.5;
  - the "obtained from diary information; how is out of scope" notes of E-014 and E-019;
  - the S-014 HALT-30 recall quote;
  - the E-057 notes that scoring from answers is out of scope;
  - the INV-076 note.
- The v14 relations take only output elements, constants and context properties as arguments (course events, the as-of date, covered periods, stop dates shown).

## Remarks

### R15-01 Coverage gap: the per-drug acute-treatment summaries required by INV-062, INV-069, INV-071, INV-088, INV-104 and INV-109 leave their formulation free, so one formulation's summary (or that of a formulation never used) meets the requirement for every formulation of the drug

- Item(s):
  - INV-062 (the `acuteTreatmentEffectiveness`, `periodValuesOf(acuteTreatmentSummaries)` and `typeValuesOf((acuteTreatmentSummaries, h))` branches);
  - INV-069 (acute-treatment conjunct);
  - INV-071 (second conjunct, per preventive phase);
  - INV-088 (acute conjunct);
  - INV-104 (acute conjunct);
  - INV-109 (the course summary of an acute line);
  - optionally INV-105 (the acute alternative);
  - E-051 Conformance and Notes;
  - section 7, rows OUT-020, OUT-021, OUT-023, OUT-024, OUT-031, OUT-034 (and OUT-035).
- Problem:
  - In the model an acute medication is a drug-and-formulation pair (E-008 `AcuteMedication`), and an `AcuteTreatmentSummary` has a `formulationScope` (`allFormulations` or `singleFormulation`) and the formulations it summarises (E-051).
  - Only INV-071's first conjunct (the selected time range) ties the formulation. Every other requirement quantifies over the subject's acute medications, `∀ m ∈ ctx.subject.acuteMedications`, but ties only the summary's drug (`s.drug = m.drug`), period and type scope.
  - So, for a drug used in two formulations, one single-formulation summary meets the requirement for both medications. The attacks treated with the other formulation are reported in no summary.
  - For a drug used in one formulation, a single-formulation summary of a formulation the subject never used meets it with 0 treated attacks. INV-072 constrains only summaries of all formulations, and INV-074 only the lines of a single-formulation summary.
  - This is the R13-01 / R14-02 defect on the formulation dimension: a required summary can be met by one that reports none of the effectiveness Stage 1 asks for. Fix 13 ("Noted, not changed") and fix 14 ("Same class, but the reading is not clear from Stage 1") recorded it and left it open. It was never a reviewer remark, so no decline is being re-raised.
- Evidence:
  - **Predicates (v14):**
    - INV-104: `(∀ m ∈ ctx.subject.acuteMedications • ∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.drug = m.drug ∧ s.period = v.covers ∧ s.typeScope = allTypes)`;
    - INV-069: `∀ am ∈ ctx.subject.acuteMedications • ∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.drug = am.drug ∧ s.period = p ∧ s.typeScope = allTypes`;
    - INV-071, second conjunct: `∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.drug = m.drug ∧ s.period = p ∧ s.typeScope = allTypes`;
    - INV-088: `∀ m ∈ c.subject.acuteMedications • ∃ s ∈ v.acute • s.drug = m.drug ∧ s.period = v.covers ∧ scopeFor(c, s.typeScope, c3_1) ∧ s.earlyTimePoint = fifteenMinutes ∧ …`;
    - INV-062: `∃ s ∈ L.otherValues ∩ AcuteTreatmentSummary • s.period = p ∧ s.typeScope = allTypes ∧ s.drug = am.drug` (twice; the third branch has `scopeFor(ctx, s.typeScope, h)` in place of the all-types scope);
    - INV-109: `∃ s ∈ l.acuteResponse • s.typeScope = allTypes ∧ ∀ b ∈ startOf(ctx, l.treatment) • s.period.start = b ∧ …`, with INV-079 `s.drug = l.drug`.
  - **Contrast**, INV-071 first conjunct: `s.formulationScope = allFormulations` and `s.formulationScope = singleFormulation ∧ s.formulations = {m.formulation}`. The other constraints on formulation are INV-072 (`s.formulationScope = allFormulations ⇒ ∀ am … • am.formulation ∈ s.formulations`) and INV-074 (`s.formulationScope = singleFormulation ⇒ #s.formulations ≤ 1`; lines of that formulation only).
  - **Example admitted by v14 (two used formulations).**
    - Setting: a subject with `acuteMedications = {(sumatriptan, oral), (sumatriptan, subcutaneous)}`, and a clinician-facing summary of 15 August – 20 October 2026.
    - The summary shows one sumatriptan summary: `singleFormulation`, `formulations = {oral}`, all types, period = covered period, listing the orally treated attacks.
    - These all hold: INV-104 (for both medications), INV-072, INV-073, INV-074, INV-003 and INV-011.
    - The subcutaneously treated attacks of the period are in no summary.
    - The same construction meets:
      - INV-069 in the treatment review view;
      - INV-071's per-phase conjunct;
      - INV-062 for an optimal-control label;
      - INV-088 in a cluster view, where subcutaneous sumatriptan is the treatment whose 15-minute effect OUT-031 asks for;
      - INV-109 for the line of a sumatriptan course.
  - **Example admitted by v14 (unused formulation).** The drug was used orally only. A summary with `formulations = {subcutaneous}` has 0 treated attacks, 0 attacks assessed in every outcome summary and no lines, and it meets each requirement above.
  - **Stage 1:**
    - OUT-023: "For each acute medication, the diary output SHOULD report, across the attacks treated with it, the outcome measures …"; "SHOULD allow the per-drug outcomes and their consistency across treated attacks to be shown separately for each formulation of the same drug, so that a non-response to one formulation is not read as a non-response to the drug";
    - OUT-021: "the effectiveness of acute treatment for the attacks treated in each of these periods (OUT-023)";
    - OUT-020: "the effectiveness of acute treatment in OUT-023";
    - OUT-024: "the response summary from OUT-018 or OUT-023 for each treatment";
    - OUT-031: "for acute treatments, effectiveness at 15 minutes and the need for rescue treatment";
    - OUT-034: "current and past treatments with response (OUT-018, OUT-023, OUT-024)".
    - The OUT-023 evidence shows why formulation matters: [S-012] "The Consensus Panel agreed that subcutaneous formulations are generally more effective than oral formulations".
  - **The justification of fixes 13 and 14 does not apply to these outputs.** The two readings it weighs are:
    - per drug: a summary of all formulations;
    - per medication: a summary of each formulation used.

    Both readings exclude both examples above, because under each the attacks treated with a used formulation must be in a summary shown.

    The fixes say that "a disjunction of the two would fit neither reading exactly". The condition needed here is weaker than either reading, and both readings imply it: every formulation of the drug that the subject has used is covered by a summary shown. Requiring it therefore narrows neither reading. It does not decide between pooled and per-formulation presentation, which INV-071 already offers for the selected time range.
- Required change: tie the formulation of the required summaries so that every formulation used is covered, and align E-051 Conformance and the rows.
  - **(a)** In each requirement quantified over the subject's acute medications (INV-062's three acute branches, INV-069, INV-071 second conjunct, INV-088, INV-104), add `s.formulationScope = allFormulations ∨ s.formulations = {m.formulation}` (with `am` where the invariant uses it). With INV-072 this covers the medication's formulation either way, and it admits both readings.
  - **(b)** Alternatively, adopt the per-drug reading and require `s.formulationScope = allFormulations` in these invariants, stating the reading.
  - **INV-109.** For the course summary of an acute line, require `allFormulations`, or a summary per formulation the line shows (`l.formulations`), or per formulation of the drug that the subject has used. The fixer chooses, consistently with (a) or (b).
  - **Optionally, INV-105.** Require that the acute summary shown as treatment effect is of all formulations, or of a formulation of its drug that the subject has used.

  Satisfiability: a summary of all formulations can always be shown. It names every formulation used (INV-072), lists the attacks of its drug and period (INV-074), and may have 0 treated attacks. INV-073 and the period and type-scope ties of fixes 13 and 14 are unchanged.

  Watch points: this keeps the R11-02 per-drug, per-period requirement (watch point 2), the R13-01 type scopes and the R14-02 periods. It touches no E-041 value, no co-presence item and no E-008 component.

### R15-02 Coverage gap: the adherence summary next to a response comparison (INV-066) may cover a single day, because only the end of its window is tied to the evaluated period

- Item(s):
  - INV-066 (with INV-067);
  - E-047 Conformance and Notes;
  - optionally E-055 `adherence` with INV-109, and INV-104 (the adherence of the treatment line and of the clinician-facing summary);
  - section 7, row OUT-039.
- Problem:
  - OUT-039 asks for adherence "over the evaluation window, next to the response comparison of OUT-018, so that a reader can see whether an apparent lack of effect coincided with inconsistent intake".
  - INV-066 requires an adherence summary that begins on or after the treatment start and ends on the last day of one of the comparison's on-treatment periods. Its start is otherwise free.
  - A window of one day, or of a few days at the end of the evaluated month, therefore meets the requirement. Such a window says nothing about intake over the period whose values the comparison evaluates. Every on-treatment period of a response comparison has at least 28 days (INV-056).
  - The window is unchanged since v00, and no loop file has discussed it. It is the same kind of free dimension as in R14-02.
- Evidence:
  - INV-066: `∀ rc : ResponseComparison • ∃ a ∈ viewOf(rc).content ∩ AdherenceSummary • a.treatment = rc.treatment ∧ rc.treatmentStart ≤ a.window.start ∧ ∃ p ∈ ran rc.onTreatment • a.window.end = p.end`. INV-067 adds only `s ≤ a.window.start`.
  - E-047: `window : →Period core -- the evaluation window the adherence refers to`. Its Meaning: "The patient-reported adherence to the prescribed preventive regimen over the evaluation window, shown next to the response comparison".
  - **Example admitted by v14:**
    - Topiramate started 3 February 2026. The response comparison has a 28-day baseline (6 January – 2 February 2026) and the on-treatment period 3 March – 30 March 2026.
    - The adherence summary has the window 30 March – 30 March 2026 (`otherSpan`, 1 day) and `proportionOfPrescribedIntake(100)`.
    - These all hold: INV-066, INV-067, INV-002, INV-003 and INV-011 (the completeness of that day).
    - The reader cannot see whether intake from 3 to 29 March was consistent, which is the purpose OUT-039 states.
  - **Stage 1 OUT-039:**
    - Rationale: "Without an adherence output, the response comparison of OUT-018 cannot distinguish non-response from inconsistent intake."
    - Its quotes place adherence over the time on treatment before evaluation: [S-018] "14D. If no efficacy is observed after 8–12 weeks of treatment and other contributing factors are identified (e.g., inconsistent treatment adherence …)"; [S-008] "In cases of partial (or no) effectiveness, the adherence to treatment, adequate trial of at least eight weeks at the target dose … should be reviewed."
- Required change: tie the window to the period the comparison evaluates, and align the INV-066 Reading, E-047 and row OUT-039.
  - **(a)** Require the window to contain the on-treatment period it ends with: `∃ p ∈ ran rc.onTreatment • a.window.start ≤ p.start ∧ a.window.end = p.end`.
  - **(b)** Alternatively, require it to run from the treatment start to the end of that period (`a.window.start = rc.treatmentStart`), the time on treatment before the evaluation as in [S-018] 14D.
  - **Optionally**, tie the line's `adherence` (E-055, INV-109) and the adherence summary that INV-104 requires to the same window, or to the INV-066 summary of the response comparison shown with them.

  Satisfiability: `p` begins on or after the treatment start (INV-056), so a window equal to `p` or from the start to `p.end` meets INV-067. INV-003 and INV-011 already show `p` and its completeness in the comparison's view.

  Watch points: none is touched. The co-presence of the adherence summary with the comparison (watch point 3) is unchanged.

### R15-03 Coverage gap: the response-comparison alternative of the overview's "treatment effect" (INV-105) is not tied to the period the overview covers, so a comparison of a treatment stopped years earlier meets it; v14 tied only the acute alternative

- Item(s):
  - INV-105 (the treatment-effect conjunct and its antecedent; Reading and Notes);
  - E-067 Notes;
  - section 7, row OUT-035.
- Problem:
  - OUT-035 asks for an overview of "treatment effect … so that patients can follow the effect of their treatment".
  - Fix 14 (R14-02 (d)) tied the acute-summary alternative of INV-105 to the covered period or a period within it. The INV-105 Notes now give the reason: "so that the effect the patient follows is that of the period the overview shows, not of an earlier one".
  - The other alternative of the same disjunction, `v.content ∩ ResponseComparison ≠ ∅`, accepts the response comparison of any preventive treatment of the subject's history, whatever its dates. The antecedent is also history-wide ("a preventive treatment that has started", ever).
  - So an overview of the current period meets INV-105 with the comparison of a treatment that was stopped long before. Meanwhile, the treatment the patient takes during that period appears in no treatment-effect item.
  - The R14-02 review offered option (d) only for the acute alternative, and the fix applied it only there. The response-comparison alternative has not been considered.
  - This is not the settled point "treatment effect by one item" (review 13; fix 11). One item still suffices. What is missing is which item.
- Evidence:
  - INV-105 (v14): `((∃ t ∈ ctx.subject.preventiveTreatments • startOf(ctx, t) ≠ ∅) ∨ ctx.subject.acuteMedications ≠ ∅ ⇒ v.content ∩ ResponseComparison ≠ ∅ ∨ ∃ s ∈ v.content ∩ AcuteTreatmentSummary • s.typeScope = allTypes ∧ within(s.period, v.covers))`.
  - INV-105 Notes (v14): "An acute-treatment summary that shows the treatment effect is one of the covered period or of a period within it (`within`, E-005), so that the effect the patient follows is that of the period the overview shows, not of an earlier one".
  - **Example admitted by v14:**
    - Setting: topiramate from 1 February 2019, stopped 31 December 2019; erenumab from 15 March 2026, ongoing; acute sumatriptan. The patient-facing overview covers 15 August – 20 October 2026, the period since the previous consultation, which E-067 names as an example.
    - Its only treatment-effect item is topiramate's response comparison: baseline January 2019, on-treatment periods February–April 2019, with its values, changes and time points.
    - These all hold: INV-105, INV-003, INV-011, INV-054, INV-056, INV-057 and INV-059.
    - The overview shows no effect of erenumab, the preventive treatment the patient takes throughout the covered period, and no acute effectiveness in that period.
  - **Stage 1 OUT-035:**
    - Statement: "… an understandable overview of their own headache pattern over time (… treatment effect …) … so that patients can follow the effect of their treatment and prepare consultations";
    - [S-027]: "Bovendien kunnen de patiënten het effect van acute en eventueel preventieve behandeling zelf monitoren in het e-dagboek" (translation in Stage 1: "patients can themselves monitor the effect of acute and possibly preventive treatment").
- Required change: tie the response-comparison alternative to the treatment of the period the overview covers, as v14 did for the acute alternative. Keep one item.
  - **(a)** Require the comparison shown to be of a preventive treatment whose course overlaps the covered period: started on or before `v.covers.end` and with no stop before `v.covers.start` (`startOf`, `courseEvents`, E-008). Restrict the antecedent's preventive part to such treatments, so that the conjunct is required, and satisfiable, exactly where such a treatment exists. The acute alternative stays as in v14.
  - **(b)** Alternatively, where several preventive treatments overlap the covered period, require the comparison of the most recently started one. Otherwise proceed as (a).

  The comparison's own periods are not required to lie in the covered period: a treatment started before the covered period has its baseline and early months before it.

  Satisfiability:
  - INV-055 makes a comparison available for every started preventive treatment, and it can be shown in the overview with its values, changes and time points (INV-003, INV-054, INV-056, INV-059).
  - Where no preventive course overlaps, the acute alternative remains.

  Watch points:
  - Watch point 4 concerns the overview's menstruation conjunct, which is untouched.
  - The fix-11 "one item" decision and the v14 acute tie are kept, and the change goes in the same direction as v14.

## Checked and not raised

- **The v14 changes.**
  - `ruleTr73` matches its source. Its reading "from the end of the second cycle" (`endOfCycleAnchor(2)`, `atLeastOffset`) is the model's stated reading, consistent with NICE 1.3.29.
  - Section 7.3 also says "Kronik migren hastalarında endikasyon vardır". Every rule has `headacheType c1`, as `ruleNice1329` and `ruleTr3639` do for treatments used in chronic migraine.
  - The refined `excludes` criterion leaves every v13 value unchanged (watch point 1 not touched). The "eleven" plus "seven" rule counts (E-041 Evidence) and the "every rule except NICE 1.3.29 and Turkish sections 3.6.3.9 and 7.3" sentences are consistent.
  - INV-088, INV-104 and INV-109 now tie their acute summaries' periods, and INV-105 ties its acute alternative's period. All are well typed and satisfiable.
- **Several stop events in one course.** INV-001 bounds a treatment to one start but not to one stop. A course with `stop(paused)` and later `stop(discontinued)` lets a line (INV-079, INV-109) show either stop date. Stage 1 does not say whether a resumed or later-discontinued pause is one course. The model's ordering requirements hold either way. Not raised.
- **INV-060 with INV-061 for compared periods shorter than 28 days.** Declined in fix 02 (item 14), with a justification. I have no new evidence.
- **The position of the pre-treatment baseline** (INV-056: any monthly period that ends before the start) and the baseline of the post-stop view (INV-070). Judged in review 02, since Stage 1 does not define the baseline more precisely. No new evidence.
- **The period of a cluster attack rate within its bout** (INV-088, INV-089). Stage 1 asks for "attacks per day and per week during active periods". A rate over any period within the bout is such a value.
- **`refs`** is defined in section 2.5, not in an `omn` block. It is part of the notation (section 2.10 admits names defined there).
- **HALT-90 grade values** "I"–"IV" without the table's parentheticals "(indicates high need for care)". The grade names are those of the table, and the Evidence quotes the full cells.
- **Settled questions not reopened (no new evidence):**
  - the OUT-017 window values;
  - the monthly baseline (R01-03);
  - INV-023 at any granularity;
  - the "> 3 months" readings;
  - the MIDAS labels;
  - HIT-6 recall;
  - the "baseline administration";
  - R10b-01 and R11-01 (a)/(b) (watch point 3);
  - INV-091 to INV-093;
  - "treatment effect" by one item;
  - the E-041 timings, ages and `excludes` values (watch point 1);
  - INV-087 and the lead-in (watch point 4);
  - INV-049 and INV-050 (watch point 5);
  - the E-008 time frames (watch point 6).
- **Section 8.** ISS-01 to ISS-06 and ISS-08 to ISS-11 are founded. I re-verified:
  - 8.2.6 criterion B (p. 124);
  - "simple analgesics" only on p. 139;
  - NICE 1.3.9 and 1.3.39 without a review time point;
  - 1.3.48 and the CG150 population;
  - the [S-034] flowchart (p. 52).

  ISS-10 correctly lists the Turkish protocol among the guidance that can apply to treatments started in childhood. No Stage 1 issue is silently worked around. R15-01 to R15-03 concern the model, not Stage 1.

## Notes on frozen items (for the human)

None. FROZEN_ITEMS.md does not exist, and no item of v14 carries a FROZEN marker.
