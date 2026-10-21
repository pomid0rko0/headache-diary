# Fix log — iteration 07
Input review: reviews/review-iter-07.md · Input version: v06 · Output version: v07
Date: 2026-10-21

## What was downloaded and checked

No FROZEN_ITEMS.md exists, and the oscillation check after iteration 04 froze nothing, so no item is frozen. None of its watch points (INV-087 and the lead-in; E-060, E-061, INV-105; INV-104) is touched.

**Earlier work read so that no fix is undone.** PROCESS.md, Stage 1 v18 (sections 1–3 in full, section 5), v06 in full, reviews 01, 06 and 07, the fix logs of iterations 01, 02 and 06, and oscillation/check-after-iter-04.md. The guarantees of the earlier fixes of E-041 are kept:
- R01-01: the NVN and Russian section 7.1 rules stay, with their offsets, anchors and readings.
- R01-02: INV-001 still gives every preventive treatment a guidance type, with `otherPreventive` as the fallback. The new exclusion of a rule needs a *listed* type, so a missing type listing still cannot make any rule inapplicable.
- R02-01: `fitsMonthlyPeriod`, the INV-055 guard and the INV-001 order of course events are unchanged.
- R06-01: every new rule has the headache type and the ages of its guidance, each supported by a quote.
- Settled readings are not reopened: the 14A and NVN window readings; NICE 1.3.27 applying to onabotulinumtoxinA.

**Downloads.** All went with `curl` into a fresh directory under `/tmp` (`/tmp/fix07-dl-53LH`), outside the repository; every download returned HTTP 200. Scripts were kept in the session scratchpad and run with `python3 -I`. PDFs were extracted page by page with `pdftotext -raw` and `-layout`; web pages and the Europe PMC full text had their markup removed. The [S-034] title page (an image without a text layer) and page 48 of [S-035] were rendered with `pdftoppm` and read.
- [S-018] AAN/AHS 2026 Clinician Summary (12-page PDF).
- [S-008] IHS 2024 practice recommendations (univaq PDF, 31 pages).
- [S-011] EHF 2022 guideline: Europe PMC full text of PMC9188162 and the listed PMC page.
- [S-015] NICE CG150 Recommendations page.
- [S-016] SIGN 155 (64-page PDF).
- [S-028] NVN module "Profylactische behandeling migraine" (web page).
- [S-033] Russian clinical recommendations for adults (92-page PDF; HTTP 200 at the first attempt).
- [S-034] Russian clinical recommendations for children (53-page PDF).
- [S-035] Turkish Ministry of Health Migraine Clinical Protocol (92-page PDF).
- [S-002] and [S-005] IHS trial guidelines (ihs-headache.org PDFs).
- [S-029] NVN module "Migraine: Monoklonale antilichamen" (web page), to check the boundary of the sweep.

**Quote check.** Every quoted string that is new in v07 (outside the `omn` blocks, 50 strings) was checked by script, split at `[...]`, after normalising whitespace, quotes, dashes and line-end hyphens:
- 34 strings were found verbatim in the downloaded texts, in Stage 1 v18 or in v06;
- 15 are English translations or the model's own words;
- "Возрастная группа" is on the image-only title page of [S-034], and was read from the rendered page.

**Verification of the remarks before fixing.** All three remarks hold.
- **R07-01.** IHS 2024 Q2 (p. 9) opens its Optimal recommendation with "In individuals initiating a new migraine oral preventive treatment, we suggest evaluating effectiveness* after three months at the target dose.", directly before the injectable sentence that Stage 1 quotes. The Essential level names the same time point. AAN/AHS 2026 14B (p. 7) reads "14B. Clinicians should wait 24 weeks at the recommended dose before assessing efficacy of onabotulinumtoxinA injections for migraine prevention before assessing efficacy." (the phrase is repeated in the source). Neither was in v06. The E-041 Notes justified the restriction to Stage 1 quotes with "for example", which qualifies only the parenthesis of OUT-018.
- **R07-02.** 14H (p. 8) refers to "after 12–24 weeks (see 14A and 14B)", so the "most medications" of 14A does not include onabotulinumtoxinA, which 14B covers. The comments of the Russian section 3.3 (p. 39) read "при отсутствии эффекта в течение 3 месяцев следует заменить выбранное профилактическое средство на другой препарат; эффективность БТА – минимум через 6 месяцев терапии." "БТА" is not in the list of abbreviations (pp. 4–5); the next recommendation (p. 40) concerns "ботулинический токсин типа А - гемагглютинин комплекс** 155 - 195 Ед по протоколу PREEMPT". In v06, `ruleAan14A` and `ruleRu71` applied to onabotulinumtoxinA. A script reproduced the review's example (an adult on onabotulinumtoxinA from 5 January 2026): v06 required a 14A window of 2 to 30 March and a section 7.1 time point on 5 April 2026.
- **R07-03.** In the Europe PMC full text, the Background section opens with paragraph Par12 ("The landscape of migraine prevention […] for migraine prevention in adults [1]. […]"), followed by Par13 ("Considering the new knowledge on the topic, the EHF council decided to update the 2019 guideline."). The listed PMC page shows them as two separate paragraphs.

| Remark | Decision (fixed / declined / partly fixed) | Changed items | What changed / justification |
|---|---|---|---|
| R07-01 | fixed, and extended by the completeness sweep below | E-041 (new rule constants, `evaluationRules`, Meaning, Realises +OUT-036, Evidence, Notes); E-008 (`PreventiveTreatmentType` +`oralPreventive`, Meaning, Notes); INV-055 (Reading, Evidence, Notes); section 7 rows OUT-018 and OUT-036; ISS-10; section 11 | **The two time points of the review.**<br>• `ruleIhsQ2Oral`: "IHS global practice recommendations Q2 (oral preventives)"; `c1`; `anyAge`, as the model reads IHS 2024 Q2; `appliesTo {oralPreventive}`; anchor `toleratedOrTargetDoseAnchor`; `atOffset` `months(3)` ("after three months at the target dose", modelled like NICE 1.3.28 and the Russian section 7.1).<br>• `ruleAan14B`: "AAN/AHS 2026 rec. 14B"; `c1`; `adultsOnly`; `appliesTo {onabotulinumtoxinA}`; anchor `toleratedOrTargetDoseAnchor` ("at the recommended dose"); `atLeastOffset` `weeks(24)` ("wait 24 weeks … before assessing efficacy").<br>• New value `oralPreventive` of `PreventiveTreatmentType`, the IHS 2024 Q2 category, added to `allPreventiveTypes`. The E-008 Notes state that the listing contains every type that describes a treatment (for example topiramate: `doseTitratedPreventive` and `oralPreventive`). INV-001's fallback type stays.<br>**The rule list.** The E-041 Notes no longer limit the list to the Stage 1 quotes. The list is now every evaluation time point for a person's preventive treatment that the guidance cited in Stage 1 for OUT-018 names, read in full. For children and adolescents it also holds the time point of the paediatric guidance that Stage 1 cites for OUT-036 (d) (see the sweep). The Notes list, by source, the time points that are named but are not evaluation time points, so that the list can be checked. E-041 Evidence quotes every new offset and population (verbatim, with location; translations for non-English text).<br>**Rules added by the sweep** (not named in the review):<br>• `ruleTrBox8`: [S-035] Box 8, at least 2–3 months, a window from the start like NVN;<br>• `ruleTr3639`: [S-035] section 3.6.3.9, onabotulinumtoxinA after 3 injection cycles, anchored at the end of the third cycle like NICE 1.3.29;<br>• `ruleRuChildren`: [S-034], 3 months after the start, children and adolescents (new `AgeCoverage` value `childrenAndAdolescentsOnly`).<br>The rule list grows from 11 to 17 rules (with `ruleRu33Bta` of R07-02).<br>**Satisfiability.** Every new rule except `ruleTr3639` puts its time point at least 8 weeks after the start (2 months for the windows), so the R02-01 argument for INV-055, INV-056 and INV-097 carries over. `ruleTr3639` is handled by the `fitsMonthlyPeriod` guard, like NICE 1.3.29. The INV-055 and E-043 Notes now name both cycle-anchored rules.<br>**Examples of the review** (script `applic.py`):<br>• Topiramate from 1 February 2026, target dose 1 March 2026, as-of 15 August 2026: the "IHS global practice recommendations Q2 (oral preventives)" time point of 1 June 2026 is now required.<br>• A child under 12 on a titrated oral preventive: IHS Q2 (oral), NVN, Turkish Box 8 and the Russian paediatric rule now apply.<br>• onabotulinumtoxinA from 5 January 2026: the 14B time point of 22 June 2026 is required. |
| R07-02 | fixed (the review's mechanism, and the Russian rule added) | E-041 (new component `excludes`, `applicable`, all rule constants, Meaning, Notes); new rule `ruleRu33Bta`; E-008 Notes; E-042 and E-043 Notes; INV-001 Reading and Notes; INV-055 Reading and Notes; INV-058 and INV-059 Readings; section 7 row OUT-018 | **New component** `excludes : set PreventiveTreatmentType`: the types for which the same guidance names another time point. `applicable` adds `¬ ∃ ty ∈ r.excludes • (t, ty) ∈ c.subject.preventiveTypes`.<br>• `ruleAan14A` and `ruleRu71` exclude `{onabotulinumtoxinA}`.<br>• So does the new `ruleTrBox8`, for the same reason: [S-035] section 3.6.3.9 evaluates onabotulinumtoxinA after 3 injection cycles.<br>• Every other rule has `excludes ↦ ∅`.<br>• A course of onabotulinumtoxinA is also a `quarterlyInjectable`, so the exclusion is its own component, as the review notes. A quarterly anti-CGRP antibody keeps 14A.<br>**Russian rule added** (the review's first option): `ruleRu33Bta` = "Russian clinical recommendations «Мигрень» (adults) 2024, section 3.3 (botulinum toxin type A)"; `c1`; `adultsOnly`; `{onabotulinumtoxinA}`; from the treatment start; `atLeastOffset` `months(6)` ("минимум через 6 месяцев терапии"). It comes with the quote, its translation and the note on "БТА" (E-041 Evidence and Notes).<br>**For onabotulinumtoxinA the model now requires:**<br>• NICE 1.3.27 (no exception in NICE) and 1.3.29;<br>• IHS Q2 (quarterly);<br>• AAN 14B, Russian 3.3 and Turkish 3.6.3.9.<br>It no longer requires AAN 14A, Russian 7.1 or Turkish Box 8. Example (script): from 5 January 2026, the 14B time point is 22 June 2026 and the Russian one 5 July 2026; no time point in March or April.<br>**R01-02 guarantee.** Exclusion needs a *listed* excluded type. A treatment without a listing has `otherPreventive` (INV-001), which no rule excludes. So the rules named for all types still apply whatever the listing otherwise, and a missing listing cannot make them inapplicable. Each guidance that excludes onabotulinumtoxinA names its own time point for it.<br>**Text.** The phrase "applying to every preventive treatment type" in the E-041 Notes now names the exclusion. The E-008 and INV-001 Notes and the INV-055, INV-058 and INV-059 Readings state the exclusion. |
| R07-03 | fixed | E-041 Evidence | The first [S-011] quote keeps "(Background, first paragraph; the omitted text is a reference number)"; the second now has "(Background, second paragraph)". |

## Completeness sweep of E-041 (time points named in the Stage 1 sources of OUT-018 and OUT-036 (d))

Each source's sections on the evaluation and duration of preventive treatment were read in full, and each PDF was also searched page by page for "week", "month" and "cycle" (or their equivalents in the source's language). Every time point found is listed below with its treatment type and population. "Rule" means it is in `evaluationRules`. The other decisions are explained in the last column and summarised in the E-041 Notes.

| Source (sections read) | Time point named (location) | Type / population | Decision |
|---|---|---|---|
| [S-015] NICE CG150, all recommendations | 1.3.27 "3 to 6 months after starting prophylactic treatment" | all prophylaxis of migraine / 12+ | rule, already present (`ruleNice1327`) |
| | 1.3.28 "after 12 weeks of treatment" | CGRP inhibitors / adults | already present (`ruleNice1328`) |
| | 1.3.29 "after 2 treatment cycles" | botulinum toxin type A / adults | already present (`ruleNice1329`) |
| | 1.3.29 "for 3 consecutive months" (changed to episodic migraine) | botulinum toxin type A | not added: stopping after success, not an evaluation of response (as in v06, E-045 Notes) |
| | 1.3.21 "consider a course of up to 10 sessions of acupuncture over 5 to 8 weeks" (migraine, after propranolol, topiramate and amitriptyline; also 1.3.9 for chronic TTH) | acupuncture | not added: length of a course, not an evaluation time point; the TTH case is in ISS-10 |
| | 1.3.48 "4 to 8 weeks after the start of withdrawal" | withdrawal of overused medication | not a preventive-treatment time point; modelled in E-039 (OUT-017) |
| [S-018] AAN/AHS 2026, recs 14A–14H (pp. 7–8), 17A–17B (p. 9) | 14A "at least 8–12 weeks at the recommended tolerated dose of most medications" | most medications / adults | present (`ruleAan14A`); now excludes onabotulinumtoxinA (R07-02) |
| | 14B "wait 24 weeks at the recommended dose" | onabotulinumtoxinA / adults | **added** `ruleAan14B` (R07-01) |
| | 14C "If suboptimal treatment response is observed by 8 weeks, physicians should optimize the dose" | all / adults | not added: a dose-optimisation check, not the assessment of efficacy, for which 14A says to wait at least 8–12 weeks; the dose change is shown by OUT-009 markers |
| | 14D "If no efficacy is observed after 8–12 weeks of treatment and other contributing factors are identified […]" | all / adults | not added: what to do after the 14A assessment (its 8–12 weeks); no new time point |
| | 14H "after 12–24 weeks (see 14A and 14B)" | all / adults | not added: refers to the time points of 14A and 14B |
| | 17B "tapering a migraine preventive medication after 6 months of treatment" | all / adults | not added: a tapering discussion (continuation, OUT-022), not an evaluation of response |
| | Rationale of rec. 14 (trials of CGRP mAbs at 12 and 24 weeks) | — | not added: rationale about trials, not a recommendation |
| [S-016] SIGN 155, section 4.1 (p. 14), key recommendations (p. 5), section 4.6 (p. 18), checklist 7.3 (pp. 34–35); all pages searched | "eight weeks at the target dose or maximum tolerated dose (for those with a titration schedule)" | titrated / adults | already present (`ruleSignTitrated`) |
| | "For treatments of fixed dose […] assessed at 3 months" | fixed dose / adults | already present (`ruleSignFixedDose`) |
| | "the need for ongoing prophylaxis considered after 12 months" (4.1); "The need for ongoing prophylaxis should be considered after six to 12 months." (key recommendations) | all / adults | not added: continuation and phasing out, not an evaluation of response |
| | Checklist "First follow up with GP (after 2–8 weeks)", "Follow-up review with GP (after 6–8 weeks)" | consultations | not added: a consultation schedule counted from the previous consultation, not anchored on a treatment; SIGN's time points for deciding effectiveness are those of section 4.1 |
| | Section 4.6 (botulinum toxin A) and the CGRP sections: trial durations only | — | no time point for practice; nothing to add |
| [S-011] EHF 2022, consensus statements 1–7 and the clinical guidance of questions 3 and 4 | Q3 "evaluating efficacy after a minimum of 3 consecutive months on treatment" | anti-CGRP mAbs / adults | already present (`ruleEhf2022Q3`) |
| | Q3 guidance: "In selected cases decision on treatment maintenance can be readdressed after an additional period of 3 months." | anti-CGRP mAbs / adults | not added: an optional re-evaluation ("can") for cases the clinician selects. Its condition is a clinical judgement on the individual's response, not a property of the output context, so making it a rule would be decision logic. The first evaluation, "a minimum of 3" months, is modelled; a diary may show the later one as an `OtherItem`. |
| | Q4 "considering a pause […] after 12-18 months of continuous treatment" | anti-CGRP mAbs | not added: a pause (OUT-022), not an evaluation of response |
| [S-008] IHS 2024, Q2–Q13 (pp. 9–17); all pages searched | Q2 Optimal: oral preventives "after three months at the target dose"; Essential: "after three months of treatment at target dose" | oral / any age | **added** `ruleIhsQ2Oral` (R07-01) |
| | Q2 Optimal: monthly injectables "a minimum of three months"; quarterly injectables "a minimum of six months" | injectables / any age | already present |
| | Q2 Comment: "In non-responders to onabotulinumtoxinA after the first cycle, the dose should be increased from 155 U to 195 U in the subsequent cycle (25,26)." | onabotulinumtoxinA | not added: a dose-optimisation check, like AAN 14C; the IHS time point for quarterly injectables is six months |
| | Q2 Evidence: four to six weeks to maximum benefit; "Most recent guidelines recommend a minimum treatment duration of 4–12 weeks" | — | not added: evidence that reports trials and other guidelines |
| | Q3 footnote: "after an appropriate period of time (see Q2) at adequate doses" | — | refers to Q2; nothing to add |
| | Q4 Evidence: "adequate trial of at least eight weeks at the target dose" reviewed "In cases of partial (or no) effectiveness" | all | not added: the adequacy of an earlier trial, reviewed when the effect is partial; IHS names its own time point in Q2 |
| | Q5: "continued for at least six months for oral drugs and 12 months for non-oral treatments before considering discontinuation"; stopping after "less than four monthly migraine days over a period of three consecutive months" | all | not added: continuation and stopping (OUT-022) |
| | Q6: "a ≥30% decrease […] is acceptable for treatment continuation beyond three months" (text layer "a≥30%") | chronic migraine | not added: a continuation criterion (modelled in `critIhsQ6`, E-045), not a separate time point |
| | Q6 Background: "a two- to three-month evaluation period (starting once the maximally tolerated dose has been reached)", attributed to "Expert recommendations" (its reference 82) | all | not added: background that reports other expert recommendations; the IHS's own recommendation is Q2 |
| | Q7: "waiting at least one month before considering restarting treatment" | all | not added: a restart (OUT-022) |
| | Q10–Q13 (switching, add-on, nerve blocks, children): trial durations only | — | nothing to add |
| [S-028] NVN module, Aanbeveling and Overwegingen | "evalueer het effect niet eerder dan na 2-3 maanden behandeling" | titrated / children and adults | already present (`ruleNvnTitrated`) |
| | "Blijf actief en kritisch evalueren over effect en bijwerkingen en bespreek hoe lang de behandeling voortgezet kan worden." | all | no time point |
| | Overwegingen: a placebo response "die na 16 weken weer stabiliseert op het uitgangsniveau" | — | not added: a consideration about trials |
| [S-033] Russian adult recommendations, sections 3.3 (pp. 38–42) and 7.1 (p. 53), abbreviations (pp. 4–5) | 3.3 and 7.1: "через 3 месяца терапии"; "осуществляется через 3 мес на приеме" | all / adults | present (`ruleRu71`); now excludes onabotulinumtoxinA (R07-02) |
| | 3.3 comments: "эффективность БТА – минимум через 6 месяцев терапии" | botulinum toxin type A / adults | **added** `ruleRu33Bta` (R07-02) |
| | 3.3 comments: "в течение достаточного для развития клинического эффекта времени (от 3 месяцев и более)" | all / adults | not added: the same 3 months as `ruleRu71` |
| | 3.3 comment on anti-CGRP mAbs (p. 41): "Эффективность терапии следует оценивать через 3 мес. после ее начала." | mAbs / adults | not added as a separate rule: the same date as `ruleRu71` for these treatments (noted in E-041 Notes) |
| | 3.3: "продолжительное (6-12 месяцев) использование"; mAbs "от 6 до 12 месяцев", up to "18 месяцев"; topiramate "до 12 месяцев" | — | not added: continuation |
| | 3.3: botulinum toxin injections "рекомендуется повторять каждые 12 недель" | botulinum toxin type A | not added: an injection interval |
| [S-035] Turkish protocol, sections 3.6.2–3.6.3 (PDF pp. 47–57) and 6 (PDF pp. 77–80) | Kutu 8: "Yeterli süre, etkinlik için en az 2-3 ay ve tedavi için en az 6 aydır," | all / any age | **added** `ruleTrBox8`: a window of 2 to 3 months from the start (as NVN and 14A); excludes onabotulinumtoxinA. The "at least 6 months for treatment" is a treatment duration and is not added. |
| | 3.6.3.9: "Hastalar 3 enjeksiyon siklusu sonra değerlendirilmeli ve fayda görmeyen hastalarda tedavi kesilmelidir." | onabotulinumtoxinA / any age | **added** `ruleTr3639`: end of the third cycle, `weeks(0)` (as NICE 1.3.29) |
| | 3.6.3.9: stop "3 ay boyunca ayda 10 günün altında seyrediyorsa" | onabotulinumtoxinA | not added: stopping after success |
| | Bullets below Kutu 8: "Tedavinin etkinliğinin başlamasının 2-3 ay sürebileceği ve maksimum terapötik etkinin altı ay içinde oluşacağı unutulmamalıdır." | all | not added: the onset and the maximum of the effect |
| | 6.2.2 (children): "Tedavi süresi en az 4 ay olup, bu süre zarfında yan etkiler takip edilmelidir." | children | not added: a treatment duration; Algoritma 13 and 14 name no time point |
| | **Population.** The protocol covers migraine at all ages and has its own section "6. ÇOCUK VE ERGENDE MİGREN"; Kutu 8 and 3.6.3.9 state no age. | | Read as `anyAge`, as IHS 2024 Q2 is. |
| [S-034] Russian paediatric recommendations, sections 3 and 7.1 (pp. 23–34), Приложение Б (p. 52), Приложение В (p. 53), title page | Flowchart: "Контроль эффективности терапии через 3мес." | all / children and adolescents | **added** `ruleRuChildren`. OUT-036 (d) asks for efficacy "as recommended in paediatric guidance" and cites [S-034]; the time point is a time point "named in current guidance" in the sense of OUT-018. ISS-10 is updated and asks the human to confirm. The population quotes are "Возрастная группа" with "дети" on the title page (image) and "Диагностика мигрени у детей и подростков" (p. 17). |
| | Flowchart: "Отсутствие положительной динамики частоты и тяжести приступов в течение 3мес: коррекция профилактической терапии" | all / children | the same 3 months as the rule |
| | Drug paragraphs: "минимальная продолжительность курса терапии 3мес"; Приложение В: "в течении минимум 3 месяцев" | children | not added: course minimums and observation; the same 3 months |
| [S-002] IHS trial guideline, episodic migraine (sections 1.1.13, 1.2.7, 1.3.1, 1.3.2) | "Use a double-blind treatment phase lasting at least 12 weeks."; 24-week phases; analysis of the last 4 or 12 weeks; onset in the first 4 weeks; PGIC "(e.g. 4, 8, or 12 weeks)"; the definition of previous failure "after an adequate trial of medication (usually for 1–3 months for oral drugs […])" | trials | not added: the design and analysis of controlled trials, and trial eligibility, not the evaluation of a person's treatment. Stage 1 cites S-002 in OUT-018 for the change from baseline. |
| [S-005] IHS trial guideline, children (treatment periods, disability) | 84 days (12 weeks) treatment periods; shorter 8-week periods; disability "over the previous 3 months" | trials | not added: trial design (the PedMIDAS recall is modelled in E-057) |
| [S-029] NVN mAbs module (boundary check; a Stage 1 source not cited for OUT-018) | "Evaluatie van effect dient na twee maanden topiramaat/valproinezuur en tenminste zes maanden onabotulinumtoxine type A te gebeuren" | prior treatments, as insurer conditions | not used: S-029 is cited only for OUT-010 and OUT-025; the passage states reimbursement conditions (OUT-025 Caveats: scheme criteria are not requirements), which E-056 covers as scheme windows |

Result: 6 time points added (`ruleIhsQ2Oral`, `ruleAan14B`, `ruleRu33Bta`, `ruleTrBox8`, `ruleTr3639`, `ruleRuChildren`), 11 kept, and 3 rules now exclude onabotulinumtoxinA.

## Other changes

1. **Sweep for the R07-02 kind of defect**: a general time point applied to a type for which the same guidance names another time point.
   - NICE 1.3.27: no exception in NICE, and the end of the second botulinum cycle (about 24 weeks) lies within its 3–6-month window. Unchanged; settled in review 07.
   - IHS Q2: its three rules are type-specific.
   - SIGN 155 and NVN: neither names a botulinum time point, so `excludes ↦ ∅`.
   - EHF: specific to mAbs.
   - Russian paediatric recommendations: they do not mention botulinum toxin, so `excludes ↦ ∅`.
   - Turkish Box 8: excludes onabotulinumtoxinA (3.6.3.9). This is the one further case, fixed with the R07-02 mechanism.
2. **ISS-10** keeps its ID and title. Its text now says:
   - that the [S-034] time point is modelled since v07, because OUT-036 (d) cites [S-034] for efficacy "as recommended in paediatric guidance";
   - which rules can apply to a child or adolescent.

   The human is asked to confirm the [S-034] rule. The open question about preventive treatments of other headache types remains.
3. **Satisfiability pass** over the changed constructs and the invariants that constrain the same elements: E-041, E-042, E-043 `timePoints`, INV-001, INV-055, INV-056, INV-058, INV-059, INV-066 and INV-097.
   - `applicable` became stronger for the three rules that have exclusions, and holds for new rules. INV-058 (definitional) admits exactly the time points of applicable rules, and INV-055, INV-059 and E-043 (MUST) require only these. So the four cannot conflict.
   - For every new time point that passes the `fitsMonthlyPeriod` guard, the following can be shown together in every admissible context, also for children (INV-097, equal lengths):
     - a 28-day on-treatment period that ends at the time point (for the Turkish window, at its earliest date, which is at least 59 days after the start);
     - a 28-day baseline period before the start.
   - `ruleTr3639` can fall less than 28 days after the start only through cycle-end dates that the context allows. The guard then removes the obligation, as for NICE 1.3.29.
   - Derived attributes: `earliest` and `latest` of E-042 are defined by `shift`, which is total; `latest` is required exactly when `maxOffset ≠ ∅`.
   - INV-001: no new conjunct. `childrenAndAdolescentsOnly` uses the existing `ageGroup`.
   - Script `applic.py` checked seven scenarios and found no conflict:
     - adult topiramate;
     - adult onabotulinumtoxinA;
     - adult erenumab;
     - a 10-year-old on a titrated oral preventive;
     - a 14-year-old with only the fallback type;
     - verapamil for cluster headache only (no time point; R06-01 kept);
     - onabotulinumtoxinA with cycle ends 10 and 20 days after the start (the guard applies to both cycle-anchored rules; R02-01 kept).
4. **Wording.**
   - The [S-034] title page is described as "Возрастная группа" followed by "дети", so that no scope-sensitive word is needed.
   - The search log says "Europe PMC full text" instead of naming its format.
5. **Bookkeeping.**
   - Header "Version: v07 · Iteration: 07 · Status: under review"; section 9 "as of v07".
   - Section 11: iteration 07 paragraph (downloads; no web search; no new source).
   - Section 12: v07 entry.
   - Section 10 is unchanged.

## Checks

Scripts in the session scratchpad (`mech.py`, `names.py`, `levels.py`, `scope.py`, `newquotes.py`, `qcheck.py`, `applic.py`) were run on the final OUTPUT_MODEL.md.

| Check | Result |
|---|---|
| E-/INV- headings | 67 elements (E-001–E-067) and 108 invariants (INV-001–INV-108); none missing, no duplicates, none withdrawn |
| References | no dangling E- or INV- reference<br>ISS headings ISS-01–06 and ISS-08–11; ISS-07 occurs only in section 8 ("withdrawn"), section 9 and the change log<br>S references within S-001–S-046 and S-101–S-105<br>OUT references within 001–039 |
| Realises and traceability | every element and invariant has exactly one Realises field<br>39 rows in Stage 1 order (OUT-039 after OUT-025)<br>0 differences between the rows and the union of the Realises fields (E-041 now Realises OUT-036, and row OUT-036 lists it)<br>no coverage text names an ID outside its row<br>39 × "full" |
| Names and types in `omn` blocks | 311 declared names (v06: 305; new: the six rule constants), none declared twice<br>204 enumeration constants and variant tags (v06: 202; new: `oralPreventive`, `childrenAndAdolescentsOnly`), no duplicates and no clash with declared names<br>203 attribute and component names (v06: 202; new: `excludes`)<br>every attribute selection is declared on some type<br>the only identifier not declared in a block is `refs`, defined in section 2.5<br>all 17 rule constants list the nine `EvaluationRule` components in order<br>`evaluationRules` contains exactly the 17 constants<br>the new terms use only declared types (`PreventiveTreatmentType`, `AgeCoverage`, `AgeGroup`) |
| Typing rule for levels | 172 level-annotated attribute declarations, as in v06; no violation (the new component belongs to a value type and has no level) |
| Conformance levels | MUST 19 (INV-003, 009, 014, 015, 023, 028, 037, 040, 044, 047, 054–057, 059, 068, 086, 102, 108)<br>MUST NOT 2 (INV-048, 106)<br>SHOULD 47<br>SHOULD NOT 8 (INV-013, 021, 043, 065, 084, 091, 101, 107)<br>definitional 32; total 108<br>no level or scope changed; every MUST NOT and SHOULD NOT predicate has the form `¬ F` |
| Quotes | 50 new quoted strings, all accounted for (see "Quote check" above); the quotes of this fix log were also checked by script (`qcheck.py`) |
| Scope sweep (enter, entry, record, input, capture, log, store, persist, database, JSON, XML, CSV, FHIR, HL7, serialise, encode, retention, answer, reminder, field, obtained, calculated, computed, algorithm, "diary information", "diary data") | 83 occurrences (v06: 81). The two new ones are "diary data" inside the Stage 1 OUT-036 (d) quote, and "search log" in the v07 change-log entry. No input entity, storage term or derivation from input was added. The new rule components and predicates take only context properties (`preventiveTypes`, `ageGroup`) and rule constants. |
| Satisfiability | see Other changes 3: no conflict |
| Snapshot | `cmp OUTPUT_MODEL.md history/v07.md`: identical |
| Files written | only OUTPUT_MODEL.md, history/v07.md and this fix log; nothing under docs/stage1-output-requirements/ was changed; nothing committed or pushed |
