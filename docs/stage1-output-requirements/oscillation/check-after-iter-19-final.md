# Oscillation check — final, after iteration 19
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: v00–v18; reviews 01–19 (incl. 11b, 16b, 16c, 17b, 19b, 19c); fixes 01–18
Date: 2026-10-21

## Method
I read PROCESS.md, all 25 reviews, all 18 fix logs and the four earlier checks (after iterations 04, 08, 12 and 16), and confirmed with `git log` that each of the 19 document commits is byte-identical to its `history/vNN.md`, that OUTPUT_REQUIREMENTS.md equals v18 and that FROZEN_ITEMS.md does not exist. A script split every snapshot into items (header; sections 1, 2, 4; section 3 preamble and group headings; each OUT-xxx block and each of its fields; each S-xxx row; each search-log row; each change-log entry), hashed each item per version and flagged any state equal to a non-adjacent earlier one. At a finer grain it tracked all 292 distinct quotes (keyed by requirement, field, source and text) with their location in every version, the RFC 2119 keywords of every Statement and "Strength:" line, the claim wording ("can be applied", "to be applied", "relate the pattern to", "supports, but does not"), and a word diff of every field between consecutive versions, flagging any inserted text that had been deleted earlier and any deleted text that had been inserted earlier. I then compared the actual text of every changed item with the remarks, the options they offered, and the "Checked and not raised" notes of all reviews.

## Change history of items changed in two or more versions
| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| Header | v01–v18 | "Version: v00 · Iteration: 00 · Status: draft" became "Version: v01 · Iteration: 01 · Status: under review". After that the version and iteration go up by one each time, ending at "Version: v18 · Iteration: 18 · Status: under review". | Loop bookkeeping | Convergent. Mechanical, one direction. |
| Section 4 (Withdrawn requirements) | v01–v18 | "None (v00)." became "None (as of v01).", then "None (as of v02)." and so on up to "None (as of v18).". Nothing was ever withdrawn. | Bookkeeping | Convergent. |
| Section 7 (Change log) | v01–v18 | One entry was appended per version. The only in-place edit is v02's correction of the v01 counting rule: "counted by the strongest keyword in each statement" became "counted by the primary strength, that is, the first RFC 2119 term in each requirement's "Strength:" line". By script, every entry from v02 to v18 is unchanged after the version that wrote it. | R02-02; otherwise bookkeeping | Convergent. Append-only since v02. |
| Section 6 (Search log) | v06, v07, v10, v11 | Four different rows, each changed once: <br>• Spanish (SEN 2026, S-045); <br>• "English — regulators": "FDA guidance on preventive migraine drugs: none found." became a record of S-046, with "that was wrong (R07-02)"; <br>• French (English SFEMC versions on the IHS site); <br>• Finnish: "No current Käypä hoito migraine guideline …" became a record of "Migreeni", with "that was wrong (R11b-02)". <br>No row has changed since v11. Reviews 19 and 19b decided that the Italian and Swedish rows need no change. | R06-01; R07-02; R10-01; R11b-02 | Convergent. |
| OUT-002 | v05, v14, v15 | **v05:** in the Statement, "Definition of terms" became "Definitions of terms". **v14:** [S-001], [S-002] and [S-021] quotes added; the [S-003] location clarified; one Evidence-basis sentence added. **v15:** [S-027] label 'module "Digitale dagboeken"' became 'module "Migraine: Organisatie van zorg - digitale dagboeken"'; [S-021] label '(section "Migraine in children and adolescents" …)' became '(Annex "Clinical investigation of medicinal products for the treatment of migraine in children and adolescents" …)'. | R05-01 (a); sweep 14; sweep 15 | Convergent. Each label has two states. The singular heading has been absent since v05, and the v14 "section" label since v15. |
| OUT-003 | v04, v15 | **v04:** [S-013] location '(section "Proposed updated definition of resistant and refractory migraine")' became '(Results, paragraph beginning "Refractory migraine is defined", the third paragraph after Table 3 …)'. **v15:** [S-027] label became the full module title. | R04-01; sweep 15 | Convergent. Two different quotes. |
| OUT-005 | v01, v07 | **v01:** "labelled with the definition used" moved out of the MUST sentence into "The output SHOULD label the definition of a migraine day that it follows". **v07:** [S-046] quote added; "(EMA)" became "(EMA 2026; FDA 2023)". | R01-04; R07-02 | Convergent. Unchanged since v07. |
| OUT-006 | v07, v14 | **v07:** [S-046] chronic-migraine quote added, with FDA in the Rationale and Evidence basis. **v14:** [S-003] 1.3.1 comment quote added, with the label sentence. | R07-02; sweep 14 | Convergent. Insertions only. |
| OUT-010 | v14, v15 | **v14:** Evidence basis gained the sentence that "on a stated scale" is supported only indirectly. **v15:** [S-029] label became "Migraine: Monoklonale antilichamen". | sweep 14; sweep 15 | Convergent. |
| OUT-011 | v01, v02, v15 | **v01:** [S-035] added at "(Kutu 8 …, preventive treatment principles, PDF p. 48)". **v02:** that location became "(section 3.6.2 … bulleted list … directly below Kutu 8 …, PDF p. 48)". **v15:** [S-042] "(Question 6, consensus statement)" became "(Table 2 "Summary of the Expert Consensus Statements", row "Question 6. …", column "Statements" …)". | R01-08; consequential to R02-01; sweep 15 | Convergent. Two quotes, each relocated once. |
| OUT-014 | v06, v07, v11, v15 | **v06:** [S-026] "… (nivel de evidencia II, grado de recomendación B)" replaced by [S-045] "Debe promoverse el uso de diarios para monitorizar su cefalea y el uso de medicación."; "SEN, grade B" removed from the graded recommendations. **v07:** [S-046] secondary endpoint a added. **v11:** five ICHD-3 8.2 notes and "The breakdown by drug class and by individual drug rests on ICHD-3 …" added. **v15:** [S-033] title "diagnostic criteria of medication-overuse headache" became "Диагностические критерии лекарственно-индуцированной головной боли (согласно МКГБ-3, 2018) [8]", that is, … | R06-01; R07-02; R11b-01 (a); sweep 15 | Convergent. The Statement is unchanged since v00, and the strength is MUST in all 19 versions. Unchanged since v15. |
| OUT-018 | v01, v07, v14 | **v01:** [S-015] 1.3.29 and [S-002] recommendation a added. **v07:** "Graded guideline recommendations (NICE CG150 1.3.27–1.3.29; SIGN 155; AAN/AHS 2026 14A level B)" lost "SIGN 155;", and "national guideline text (SIGN 155, section 4.1 introduction; not a graded recommendation or good-practice point)" was added. **v14:** [S-002] recommendation b added. | R01-08; R07-01; R14-03 (a) | Convergent. Unchanged since v14. |
| OUT-020 | v01, v18 | **v01:** [S-015] 1.3.28 (with its list items) and [S-023] "Hintergrund" added. **v18:** "… SHOULD always show the underlying values (OUT-018, OUT-019)." became "… (OUT-018, OUT-019) and, where the named criterion also rests on other values, those values as well (for example the results of instruments and of patient global impression of change in OUT-026, or the effectiveness of acute treatment in OUT-023)."; one Rationale sentence, one Evidence-basis sentence and the [S-008] Q6 and [S-010] p. 6 quotes added. | R01-08; definition-coverage pass 18 | Convergent. See Findings, candidate 3. |
| OUT-021 | v01, v02, v14 | **v01:** the MUST core became "headache days (OUT-004), migraine days (OUT-005) and acute medication days (OUT-014)", and the other components "SHOULD also include". **v02:** OUT-023 component added at SHOULD. **v14:** [S-008] Q6 and [S-002] 1.3.2.1.8 quotes added. | R01-05 (b), R01-08; R02-01; sweep 14 | Convergent. Statement unchanged since v02. |
| OUT-023 | v01, v02, v08, v14, v17, v18 | **v01:** "For the treated attacks it summarises, the output SHOULD also show when the acute medication was taken relative to attack onset …"; the cluster sentence now ends "… 15 minutes, as in the IHS cluster headache trial guideline [S-007] (see OUT-031)". **v02:** "When a preventive treatment is started (OUT-018), the output SHOULD allow these per-drug outcomes to be shown separately for the pre-treatment baseline period and for the on-treatment periods …". **v08:** "To allow the EHF definition of effective attack treatment [S-012] to be applied, the output SHOULD also report … headache relief at 2 hours … and whether that relief was maintained to 24 hours, and drug-related adverse events after intake …", plus a Caveat on conflicting evidence. **v14:** four quotes added; "(IHS 2019; IHS 2022, for the cluster headache time point)". **v17:** "The output SHOULD also state the formulation or route of administration (for example oral or subcutaneous) of each acute medication … shown separately for each formulation of the same drug …"; three quotes; "consensus (EHF 2020; EHF 2022)". **v18:** inserted "whether disturbances due to migraine-related non-pain symptoms were absent or minimal at 2 hours and whether that status was maintained to 24 hours (…)", "and whether the patient regarded them as meaningful" and "Dose changes of each acute medication are shown in the treatment history (OUT-024)."; three quotes; "(FDA 2018)" became "(FDA 2018; EMA 2007)". | R01-09, R01-11; R02-01; R08-01; sweep 14; R17b-01 (a); R18-01 (a) and definition-coverage pass 18 | Convergent. Every word diff contains only insertions, except the list "2018);" → "2018; EMA 2007);". The strength is SHOULD in all versions. See Findings, candidates 1–2. |
| OUT-024 | v12, v13, v14, v17, v18 | **v12:** two [S-013] "Drug failure" quotes and "The grouping by drug class rests on the EHF consensus (2020) …". **v13:** that sentence now begins "The grouping of preventive treatments by drug class rests on … [S-013]"; an acute-grouping sentence [S-012], two S-012 quotes and a Rationale clause added. **v14:** three [S-013] quotes, AAN/AHS 14C and 14F, and the dates/dose/duration sentence added. **v17:** Statement sentence "For acute treatments, the list SHOULD also show the formulation of each treatment (see OUT-023), so that … the EHF definition of triptan refractoriness [S-012] can be applied."; the paraphrase "the dose rests on the same EHF consensus, which states that the dosage used is to be considered" became "the dose and the formulation rest on the same EHF consensus, which states that adequate timing of drug administration, the dosage and the formulations used are to be considered"; one [S-012] quote added. **v18:** new Caveats ending "The list therefore supports, but does not by itself establish, eligibility for later treatments or for the EHF categories of resistant and refractory migraine.", with two [S-013] quotes. | R12-01 (a); R13-01 (a); R14-01 (a); R17b-01 (a); definition-coverage pass 18 | Convergent. See Findings, candidate 4. |
| OUT-026 | v01, v06, v14, v15 | **v01:** [S-041] "(Discussion)" became "(Conclusion)". **v06:** the [S-026] "Evaluación objetiva" quote and "SEN, Spain" as support removed; the SEN 2026 MIDAS/HIT-6 sentences added to Caveats as conflicting evidence; PGIC sentence added. **v14:** MSQ v2.1, PedMIDAS, "Scoring HALT" and HURT quotes added. **v15:** [S-014] '(section "The Headache Under-Response to Treatment (HURT) questionnaire")' became '(… questionnaire: a guide to follow-up in primary care", Introduction, third paragraph)'. | R01-02; R06-01; R14-04 (a) and sweep 14; R15-01 | Convergent. Unchanged since v15; SHOULD throughout. |
| OUT-027 | v04, v14, v15 | **v04:** "SBCe, Brazil" moved from national guidelines to "consensus (SBCe, Brazil; EHF 2020)". **v14:** [S-024] Introduction quote and "SFEMC, France, introductory text, for household tasks and leisure" added. **v15:** two [S-014] labels '(section "The Headache-Attributed Lost Time (HALT) Indices")' became '(… measures of burden for headache management in primary care", Introduction, first paragraph)' and '… second paragraph, last sentence)'. | R04-02; sweep 14; R15-01 | Convergent. |
| OUT-028 | v01, v14, v15 | **v01:** "The view MUST show the source definitions" became "SHOULD show … (see OUT-002)". **v14:** [S-027] quote and NVN added; Strength line gained "; SHOULD NOT for assigning a diagnosis, as in OUT-038.". **v15:** [S-033] Russian table title and [S-027] full module label. | R01-04; sweep 14; sweep 15 | Convergent. |
| OUT-031 | v01, v05, v12, v14, v18 | **v01:** [S-007] 3.7 quote added. **v05:** "(Definition of terms, p. 209)" became "(Definitions of terms, p. 209)". **v12:** [S-007] 3.8 B items c and d added. **v14:** [S-001] "Cluster remission period: …" added. **v18:** Caveat sentence added: "The ICHD-3 definition of a cluster remission period, quoted above, also refers to attacks that cannot be induced with alcohol or nitroglycerine. The output shows the start date, end date and duration of each attack-free period, but not that element." | R01-09; R05-01; R12-02 (a); sweep 14; definition-coverage pass 18 | Convergent. See Findings, candidate 5. |
| OUT-033 | v09, v10, v14 | **v09:** "MAY report them" became "SHOULD report them"; "National guideline (SFEMC, France, suggestion)" became "… both rated "Fort" (strong) …; neither article names a grading system"; Caveat "… are not named in any cited source." added. **v10:** "neither article names a grading system" became "The guideline's grading system is defined in the English version of Part 1 …". **v14:** the Caveat became "The SFEMC recommendations name only the HAD scale (HADS). PHQ-9 and GAD-7 are named, with HADS, among the validated scales … in the IHS trial-methodology guideline …; none of the clinical-practice recommendations cited in this requirement names them."; two [S-002] quotes added. | R09-01; R10-01; sweep 14 | Convergent. See Findings, candidate 6. |
| OUT-034 | v14, v15 | **v14:** RT25 and [S-019] quotes added, with an indirect-support sentence. **v15:** [S-027] label. | sweep 14; sweep 15 | Convergent. |
| OUT-035 | v01, v15 | **v01:** [S-031] CQ I-10 quote added. **v15:** [S-027] label. | R01-08; sweep 15 | Convergent. |
| OUT-038 | v14, v15 | **v14:** [S-003] 1.3.1.3 and [S-024] trigger quotes added. **v15:** [S-027] label. | sweep 14; sweep 15 | Convergent. |
| OUT-039 | v01 (added), v14 | **v01:** new SHOULD requirement. **v14:** [S-013] adherence quote and "consensus (EHF 2020, …)" added. | R01-10; sweep 14 | Convergent. |
| S-024 | v09, v10 | **v09:** Figure 3 "Fort" ratings added, with "The article names no grading system, does not define the strength labels and gives no level of evidence for Rd1–Rd10.". **v10:** that became "The French article does not restate the grading system; it is defined in the English version …", with the section 2.2 passage quoted, Table 3 "Strong", and the English citation, DOI/PMID and URL. | R09-01; R10-01 | Convergent. See Findings, candidate 6. |
| S-025 | v09, v10 | Same pattern: v09 added the Figure 1 and Tableaux I/II text with "names no grading system and does not define these labels"; v10 changed it to "The French article does not restate the grading system." and added the English methods sentence, Table 6 and the citation. | R09-01; R10-01 | Convergent. |

Items changed in exactly one version (no back-and-forth possible):
- **v01:** OUT-015, OUT-022 and OUT-029; S-017, S-028 and S-032.
- **v02:** S-010.
- **v03:** S-036.
- **v05:** OUT-001, OUT-004, OUT-007 and OUT-013.
- **v06:** S-026 (marked superseded); S-045 added.
- **v07:** S-046 added.
- **v08:** OUT-016.
- **v14:** OUT-008, OUT-009, OUT-012, OUT-019 and OUT-036.
- **v15:** OUT-025.
- **v16:** OUT-037.

Unchanged since v00:
- OUT-017, OUT-030 and OUT-032;
- the other 36 S-xxx rows;
- sections 1 and 2, the section 3 preamble and group headings, and the preambles of sections 5, 6 and 7;
- 21 of the 25 search-log rows.

## Findings
None.

No item, field or clause returns to an earlier state:
- **Quotes.** None was removed and later restored. The only quotes ever removed are the two [S-026] quotes, taken out once in v06. Quote citations grew from 184 (v00) to 290 (v18).
- **Locations.** Every quote location has at most two states.
- **Strength.** RFC 2119 keywords changed only in v01 (the OUT-005, OUT-021, OUT-028 and OUT-029 splits), v09 (OUT-033, MAY to SHOULD) and v16 (OUT-037, scope limited to migraine). None has flipped back.
- **Withdrawals.** No requirement or source was withdrawn and re-added.
- **Remarks.** All 37 remarks were fixed and none was declined, so no declined remark was re-raised. No remark proposed removing an element that an earlier fix had added.

The following candidates were examined and rejected.

1. **OUT-023 and OUT-024, the "qualify the claims" options of R17b-01 and R18-01.**
   - **What the options proposed.** Both remarks offered an option (b). R18-01 (b) said: "Reword the purpose clauses of OUT-023 ("so that the EHF definitions ... can be applied", "To allow the EHF definition ... to be applied") and OUT-024 ("and the EHF definition of triptan refractoriness [S-012] can be applied") so that they do not claim full applicability". The second and third clauses were written by fix 08 and fix 17.
   - **Why this is not a push in the opposite direction:**
     - R08-01, R17b-01 and R18-01 name the same defect, a claim that the specified outputs do not meet, and each prefers (a), adding the missing component.
     - Option (b) offered to qualify a claim, not to remove any element added earlier.
     - Both fixers chose (a), so the claim wording never changed. The v00 clause "so that the EHF definitions of effective attack treatment and triptan response [S-012] can be applied" is verbatim in all 19 versions, and "To allow the EHF definition … to be applied" in v08–v18.
     - Reviews 19, 19b and 19c re-derived the definitions and found them fully covered.
2. **OUT-023, element C ("meaningful") and element B.**
   - **Element C.** R08-01 asked for "meaningful drug-related adverse events after intake". Fix 08 wrote "drug-related adverse events after intake". v18 inserted "and whether the patient regarded them as meaningful". This moves towards R08-01's own wording, restores no earlier document state, and no review argued against it.
   - **Element B.** R18-01 corrected R08-01's and fix 08's assessment that element B "is covered through OUT-012". That assessment was a statement in a remark and a log, not document text, and v18 only inserted elements.
3. **OUT-020 (v18): a reviewer's note and the fixer's pass point different ways.**
   - Review 18, under "Checked and not raised": "Showing the frequency values meets the stated purpose (a label is never the sole indicator), and OUT-021 shows the instrument results for the same periods. Not raised."
   - Fix 18's definition-coverage pass extended the Statement anyway: "Review 18 relied on OUT-021, but OUT-021 is a separate view, and OUT-020 promises the values behind the label."
   - **Why this is not oscillation:**
     - The note was not a remark and asked for no change.
     - The v18 edit is the first change to the OUT-020 Statement since v00, and it is an insertion.
     - Reviews 19, 19b and 19c checked it against S-008 Q6, S-010 p. 6 and S-023 and accepted it.
   - It stays under observation (see the watch list).
4. **OUT-024: the v18 Caveat against the v00 Rationale and fix 12.**
   - The v00 Rationale "The number and classes of failed preventives determine eligibility …" is verbatim in v18. Fix 12 called it "now supported".
   - The v18 Caveat adds that contraindicated drugs and debilitating headache days also count, so the list "supports, but does not by itself establish" eligibility.
   - It removes no element, quote or claim (the grouping by class and the classes clause stand), and no remark pushed either way. This is a one-time qualification.
   - The v17 paraphrase edit extended the v14 text ("the dosage used" became "adequate timing of drug administration, the dosage and the formulations used"), as R17b-01 required. It did not revert anything.
5. **OUT-031, the v18 Caveat against the v14 remission quote.**
   - The [S-001] "Cluster remission period" quote added in v14 is kept verbatim.
   - The Caveat names the one element of that definition (non-inducibility) that the output does not show.
   - This qualifies the claim once and reverses nothing.
6. **S-024, S-025 and OUT-033 (v09 → v10; Caveat v09 → v14).**
   - **The two corrections.** "Names no grading system" (v09) was replaced in v10 on newly reachable evidence: the English full texts at the IHS site, which fix 09 could not reach (HTTP 403). "Not named in any cited source" (v09) was corrected in v14, because [S-002], cited since v00, names PHQ-9 and GAD-7. Each is a factual error corrected once, giving three states with none repeated.
   - **Where the old wording still appears.** In the document body (sections 1–6), "France, suggestion" last appears in v08, "names no grading system" in v09 and "not named in any cited source" in v13.
   - **No recurrence elsewhere.** No review or fix from 12 to 19 describes the SFEMC support as ungraded, so the latent fix-iter-11 wording has not recurred. SHOULD has stood since v09.
7. **Location labels changed in v04, v05 and v15.**
   - Each of these labels changed once.
   - v15 changed none of the v04 labels (OUT-003 [S-013]) or the v05 labels (ICHD-3 "Definitions of terms"; OUT-013).
   - The only labels that one fix created and a later fix changed are OUT-011 [S-035] (v01 → v02) and OUT-002 [S-021] (v14 → v15). Neither returned.
   - In the body, the singular "Definition of terms" last appears in v04, and the English renderings of the [S-033] table titles in v14.
8. **Watch-list conditions of the iteration-16 check.** All of them still hold in v18:
   - OUT-014's MUST does not rest on "SEN, grade B";
   - OUT-002 keeps the plural heading and the Annex label;
   - OUT-018 keeps SIGN 155 section 4.1 labelled as ungraded, and its moderate/severe clause at MUST;
   - OUT-021 keeps its MUST core;
   - OUT-026 keeps the SEN 2026 conflict and SHOULD;
   - OUT-033 stays SHOULD, with the grading system named;
   - OUT-037 stays limited to migraine, with [S-006] as a counter-position (unchanged since v16; reviews 17–19c raised nothing on it);
   - OUT-005 keeps its v01 split.

## Watch list
Bookkeeping by design:
- **Header, section 4 and section 7** (changed in v01–v18). The change log has been append-only since v02.
- **Section 6** (changed in v06, v07, v10 and v11). Four different rows, each changed once, and none since v11.

Requirements changed in three or more versions. All are convergent, and every later change preserved the earlier ones:
- **OUT-023** (v01, v02, v08, v14, v17, v18). Every step was an insertion, and all v01, v02, v08, v14 and v17 elements and quotes are verbatim in v18. Any of these would be oscillation:
  - removing headache relief, sustained relief, non-pain symptoms, adverse events, timing or formulation;
  - rewording the "can be applied" purpose clauses to partial applicability while those elements stand.
- **OUT-024** (v12, v13, v14, v17, v18). v13 narrowed only the attribution. v14 and v17 were insertions, plus the required paraphrase extension. v18 added a Caveat. Removing the grouping, the dates/dose/duration or the formulation, or dropping the v18 Caveat to restore an unqualified eligibility claim, would be oscillation.
- **OUT-031** (v01, v05, v12, v14, v18). Five different defects, each fixed once. All earlier quotes and the plural heading are verbatim in v18.
- **OUT-014** (v06, v07, v11, v15). Every step preserved the earlier ones, and it is unchanged since v15. The MUST, the per-drug clause, the ICHD-3 notes and the Russian [S-033] title stand.
- **OUT-026** (v01, v06, v14, v15). Unchanged since v15. The SEN 2026 conflict and SHOULD have stood since v06.
- **OUT-002** (v05, v14, v15). The plural heading and the Annex label stand.
- **OUT-011** (v01, v02, v15). Two quotes, each relocated once.
- **OUT-018** (v01, v07, v14). The SIGN label is ungraded; v14 was an insertion.
- **OUT-021** (v01, v02, v14). The MUST core and SHOULD components are unchanged since v02.
- **OUT-027** (v04, v14, v15). SBCe stays under consensus.
- **OUT-028** (v01, v14, v15). The v01 MUST/SHOULD split stands.
- **OUT-033** (v09, v10, v14). SHOULD and the named SFEMC grading system stand, and the factual corrections have not been reverted.

Also under observation (fewer than three changes):
- **OUT-020** (v01, v18): the latent divergence in Findings, candidate 3. Removing the v18 "other values" clause would be oscillation.
- **OUT-037** (v16 only).
- **OUT-010 and OUT-029:** both cite the S-006 2.3.3.2 intensity sentence; fix 16 kept them.
- **S-024 and S-025:** unchanged since v10.
- **OUT-005:** unchanged since v07.

## Loop summary
| Iteration | Remarks (incl. re-checks) | Fixed / declined | Lines changed (+/−) | Statements changed | Strength changes |
|---|---|---|---|---|---|
| 01 | 11 | 11 / 0 | +61 / −21 | OUT-005, 021, 023, 028, 029; OUT-039 added | four MUST/SHOULD splits |
| 02 | 2 | 2 / 0 | +24 / −11 | OUT-021, 023 | none |
| 03 | 1 | 1 / 0 | +7 / −3 | none | none |
| 04 | 2 | 2 / 0 | +9 / −4 | none | none |
| 05 | 1 | 1 / 0 | +17 / −12 | OUT-001, 002, 004, 007 (heading name only) | none |
| 06 | 1 | 1 / 0 | +18 / −10 | none | none |
| 07 | 2 | 2 / 0 | +23 / −9 | none | none |
| 08 | 2 | 2 / 0 | +18 / −8 | OUT-016, 023 | none |
| 09 | 1 | 1 / 0 | +21 / −7 | OUT-033 | OUT-033 MAY → SHOULD |
| 10 | 1 | 1 / 0 | +14 / −6 | none | none |
| 11 | 0 + 11b: 2 | 2 / 0 | +14 / −4 | none | none |
| 12 | 2 | 2 / 0 | +11 / −3 | none | none |
| 13 | 1 | 1 / 0 | +14 / −4 | none | none |
| 14 | 4 (plus sweep) | 4 / 0 | +66 / −19 | none | none |
| 15 | 1 (plus sweep) | 1 / 0 | +28 / −17 | none | none |
| 16 | 0 + 16b: 0 + 16c: 1 | 1 / 0 | +21 / −7 | OUT-037 | OUT-037 SHOULD NOT limited to migraine |
| 17 | 0 + 17b: 1 | 1 / 0 | +25 / −7 | OUT-023, 024 | none |
| 18 | 1 (plus definition-coverage pass) | 1 / 0 | +31 / −9 | OUT-020, 023 | none |
| 19 | 0 + 19b: 0 + 19c: 0 | — | none (v18 final) | — | — |

- **Totals.** There were 37 remarks over 19 iterations: 37 fixed, 0 declined. Every option-type remark was resolved by its "add support" or "add element" option. None was resolved by removal.
- **How the loop converged.**
  - Remark counts fell from 11 to a plateau of 1–2 per iteration. The only exception was the iteration-14 spike of 4 unquoted Statement elements, after which the fixer swept that whole class of defect.
  - From iteration 16 on, NO_REMARKS verdicts became common. Each later remark (R16c-01, R17b-01, R18-01) was a defect present since v00 or v08 and visible only by reading quotes in context. Each was fixed additively.
  - Iteration 19 ended the loop: the review and both re-checks returned NO_REMARKS on v18.
- **Stability.** Totals have been 39 requirements (10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT) since v09, and 46 source rows (45 cited) since v07. No item ever returned to an earlier state.
