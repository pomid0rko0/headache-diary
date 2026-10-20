# Oscillation check — after iteration 16
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: v00–v16; reviews 01–16 (incl. 11b, 16b, 16c); fixes 01–16
Date: 2026-10-20

## Method
I read the following:
- PROCESS.md;
- all 17 snapshots, including OUTPUT_REQUIREMENTS.md in full;
- all 19 reviews and all 16 fix logs;
- the checks after iterations 04, 08 and 12;
- `git log -p` for OUTPUT_REQUIREMENTS.md.

Each fix commit's document is byte-identical to its `history/vNN.md`. OUTPUT_REQUIREMENTS.md equals v16, and FROZEN_ITEMS.md does not exist.

A script split every snapshot into items: the header; sections 1, 2 and 4; the preambles of sections 3, 5, 6 and 7; each OUT-xxx block and each of its fields; each S-xxx row; each search-log row; and each change-log entry. It hashed each item in each version and flagged any state equal to an earlier one. At a finer grain it tracked:
- every clause of every field, flagging clauses that were added and then removed, or removed and then restored;
- every quote, keyed by source and text, with its location history and its presence across versions;
- the RFC 2119 keywords of each Statement and each "Strength:" line.

I then word-diffed every changed item version by version. I compared the changes with the remarks, offered options and "Checked and not raised" notes of all reviews, looking for pushes in opposite directions.

## Change history of items changed in two or more versions
| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| Header (version line) | v01–v16 | v01: "Version: v00 · Iteration: 00 · Status: draft" became "Version: v01 · Iteration: 01 · Status: under review". v02–v16: version and iteration +1 each time; the status stays "under review". | Loop bookkeeping | Convergent. Mechanical, one direction. |
| Section 4 (Withdrawn requirements) | v01–v16 | "None (v00)." became "None (as of v01).", and so on up to "None (as of v16).". No requirement was ever withdrawn. | Fixers' "Other changes" | Convergent. Mechanical, one direction. |
| Section 7 (Change log) | v01–v16 | One entry appended per version. The only in-place edit is still v02's correction of the v01 counting rule (R02-02). Ignoring trailing whitespace, every entry is unchanged after the version that wrote it. Totals: 10 MUST / 23 SHOULD / 5 MAY / 1 SHOULD NOT in v01–v08; 10/24/4/1 in v09–v16. | R02-02; otherwise bookkeeping | Convergent. Append-only since v02. |
| Section 6 (Search log) | v06, v07, v10, v11 | Four different rows, each changed once: Spanish (v06, SEN 2026, S-045); "English — regulators" (v07, FDA 2023 draft, S-046, "that was wrong (R07-02)"); French (v10, English SFEMC versions on the IHS site); Finnish (v11, Käypä hoito "Migreeni", "that was wrong (R11b-02)"). No row has changed since v11; fix 16 made no new search. | R06-01; R07-02; R10-01; R11b-02 | Convergent. No row was touched twice. |
| OUT-002 | v05, v14, v15 | **v05:** in the Statement, ICHD-3 "Definition of terms" became "Definitions of terms". **v14 (sweep):** <br>• added [S-001] "Headache days: …" (Definitions of terms, p. 210), [S-002] "The definitions of migraine day, moderate/severe headache day, and responder rate are designed to facilitate the use of a relatively simple headache diary." (1.3.1 comments, p. 1035) and [S-021] "It is noted here that the definition of attack is different for pre-/post-pubertal subjects [...] …"; <br>• the [S-003] location "(section 1.3.1, comments, p. 823)" gained "; the comment paragraph directly before it begins "A migraine day or a moderate to severe headache day is defined as""; <br>• the Evidence basis gained "for attacks, regulatory guidance (EMA 2007 …)" and "The ICHD-3 and IHS episodic-migraine quotes show only that the published definitions named as examples exist; they say nothing about labelling." <br>**v15 (sweep):** <br>• the [S-027] location 'module "Digitale dagboeken"' became 'module "Migraine: Organisatie van zorg - digitale dagboeken"'; <br>• the [S-021] location '(section "Migraine in children and adolescents", printed in capitals, p. 11; …)' became '(Annex "Clinical investigation of medicinal products for the treatment of migraine in children and adolescents", printed in capitals, introductory text before the subheading "Acute treatment", p. 11; …)'. | R05-01 (a); sweep 14; sweep 15 | Convergent. Each location changed at most once: the S-021 label was created in v14 and corrected once in v15. The plural heading from v05 stands, and the singular form has not occurred anywhere in v05–v16. The Statement and SHOULD have been unchanged since v05. |
| OUT-003 | v04, v15 | **v04:** the [S-013] location '(section "Proposed updated definition of resistant and refractory migraine")' became '(Results, paragraph beginning "Refractory migraine is defined", the third paragraph after Table 3 …)'. **v15:** the [S-027] location became the full module title. | R04-01; sweep 15 | Convergent. These are two different quotes, each changed once. |
| OUT-005 | v01, v07 | **v01:** the definition label was split out of the MUST sentence into a SHOULD sentence. **v07:** the [S-046] primary-endpoint quote was added, and the Evidence basis became "(EMA 2026; FDA 2023)". | R01-04; R07-02 | Convergent. Unchanged since v07 (ten versions). |
| OUT-006 | v07, v14 | **v07:** the [S-046] chronic-migraine quote was added, and FDA was named in the Rationale and Evidence basis. **v14:** the [S-003] 1.3.1 comment quote was added, with "The definition label rests on the IHS chronic migraine trial guideline [S-003] …". | R07-02; sweep 14 | Convergent. Insertions only. |
| OUT-010 | v14, v15 | **v14:** the Evidence basis gained "… the element "on a stated scale" is supported only indirectly …". **v15:** the [S-029] label became 'module "Migraine: Monoklonale antilichamen"'. | sweep 14; sweep 15 | Convergent. A latent divergence that changed nothing is described under Findings, candidate 6. |
| OUT-011 | v01, v02, v15 | **v01:** the [S-035] quote was added at "(Kutu 8 …, preventive treatment principles, PDF p. 48)". **v02:** that location became "(section 3.6.2 "Farmakolojik Tedavi Stratejileri: Profilaktik Tedavi", bulleted list … directly below Kutu 8 …, PDF p. 48)". **v15:** the [S-042] location "(Question 6, consensus statement)" became "(Table 2 "Summary of the Expert Consensus Statements", row "Question 6. …", column "Statements"; the list under Question 6 in the Results reads "based on the patient’s headache diary")". | R01-08; consequential to R02-01; sweep 15 | Convergent. These are two different quotes, each relocated once. The S-035 location has been unchanged since v02. Reviews 04 and 15 had noted, in their coverage tables and not as remarks, that the wording of the S-042 quote is the Table 2 wording. v15 follows that direction. |
| OUT-014 | v06, v07, v11, v15 | **v06:** the graded SEN 2020 quote was replaced by the ungraded SEN 2026 quote. **v07:** the [S-046] secondary endpoint a was added. **v11:** five ICHD-3 note quotes were added, with one Evidence-basis sentence. **v15:** the [S-033] location 'comment to table 4а "diagnostic criteria of medication-overuse headache"' became 'comment to table 4а "Диагностические критерии лекарственно-индуцированной головной боли (согласно МКГБ-3, 2018) [8]", that is, diagnostic criteria of medication-overuse headache according to ICHD-3'. The Statement is unchanged since v00, and the strength is MUST in all 17 versions. | R06-01; R07-02; R11b-01 (a); sweep 15 | Convergent. v15 changed a location label only and kept the English meaning. "SEN, grade B" has not returned, and the v11 ICHD-3 notes and the per-drug MUST are intact. |
| OUT-018 | v01, v07, v14 | **v01:** [S-015] 1.3.29 and [S-002] recommendation a were added. **v07:** SIGN 155 was relabelled "national guideline text (SIGN 155, section 4.1 introduction; not a graded recommendation or good-practice point)". **v14:** [S-002] recommendation b, "Alternative primary endpoints include change from baseline in moderate/severe headache days …", was added after recommendation a. The Statement and MUST are unchanged since v00, and the Evidence basis since v07. | R01-08; R07-01; R14-03 (a) | Convergent. v14 is a pure insertion, and the SIGN 155 label is intact. See Findings, candidate 5. |
| OUT-021 | v01, v02, v14 | **v01:** the MUST core became OUT-004/005/014, with the other components at SHOULD. **v02:** the OUT-023 component was added at SHOULD. **v14:** the [S-008] Q6 Optimal quote and the [S-002] 1.3.2.1.8 quote were added, with one Evidence-basis sentence on the moderate/severe-headache-day and most-bothersome-symptom components. The Statement is unchanged since v02. | R01-05 (b), R01-08; R02-01; sweep 14 | Convergent. v14 is a pure insertion, and the MUST core and SHOULD components stand. |
| OUT-023 | v01, v02, v08, v14 | **v01:** the timing-of-intake sentence was added, and the cluster sentence cites [S-007]. **v02:** the baseline versus on-treatment sentence was added. **v08:** headache relief, sustained relief, per-attack adverse events and a conflicting-evidence Caveat were added. **v14:** these quotes were added: <br>• [S-004] on the most bothersome symptom at 2 hours; <br>• [S-007] 3.7, on pain freedom at 15 minutes; <br>• the [S-020] "additional secondary endpoints" list items on repeat or rescue medication and "The incidence of pain relapse, [...]". <br>The Evidence basis became "(IHS 2019; IHS 2022, for the cluster headache time point)". The Statement is unchanged since v08, and the strength is SHOULD throughout. | R01-09, R01-11; R02-01; R08-01; sweep 14 | Convergent. Every step was an insertion, and all v01, v02 and v08 elements are verbatim in v16. |
| OUT-024 | v12, v13, v14 | **v12:** two [S-013] "Drug failure" quotes were added, with "The grouping by drug class rests on the EHF consensus (2020) …". **v13:** <br>• two [S-012] Discussion quotes were added; <br>• "consensus (EHF 2020)" became "consensus (EHF 2020; EHF 2022)"; <br>• the v12 sentence now begins "The grouping of preventive treatments by drug class rests on the EHF consensus (2020) [S-013]"; <br>• a new sentence covers the grouping of acute treatments [S-012]; <br>• one Rationale clause was added. <br>**v14:** three [S-013] sentences and AAN/AHS 14C and 14F were added. The Evidence basis gained "graded guideline recommendations (AAN/AHS 2026, 14C and 14F, level B)" and a sentence on dates, dose and duration ending "the start and stop dates and the duration of acute treatments have no direct quoted support and rest only indirectly on the list of medicines tried [S-019]". The Statement and SHOULD are unchanged since v00. | R12-01 (a); R13-01 (a); R14-01 (a) | Convergent. See Findings, candidate 3. |
| OUT-026 | v01, v06, v14, v15 | **v01:** the [S-041] location "(Discussion)" became "(Conclusion)". **v06:** the SEN 2020 support was removed, and the SEN 2026 MIDAS/HIT-6 position was added as conflicting evidence. **v14:** these quotes were added, with one Evidence-basis sentence on grading: <br>• [S-002] MSQ v2.1; <br>• [S-005] PedMIDAS; <br>• [S-014] "Scoring HALT"; <br>• [S-014] HURT (the paragraph after Fig. 5). <br>**v15:** the [S-014] location '(section "The Headache Under-Response to Treatment (HURT) questionnaire")' became '(section "The Headache Under-Response to Treatment (HURT) questionnaire: a guide to follow-up in primary care", Introduction, third paragraph)'. The Statement and SHOULD are unchanged since v00. | R01-02; R06-01; R14-04 (a) and sweep 14; R15-01 | Convergent. The SEN 2026 conflict in the Rationale, Evidence basis and Caveats has been unchanged since v06. v14 is an insertion. v15 corrected a v00 label and left the v14 labels as they were. |
| OUT-027 | v04, v14, v15 | **v04:** "SBCe, Brazil" moved from national guidelines to consensus. **v14:** the [S-024] Introduction quote (household tasks, leisure) was added, and "SFEMC, France, introductory text, for household tasks and leisure" was added to the national guidelines. **v15:** the two [S-014] locations '(section "The Headache-Attributed Lost Time (HALT) Indices")' became '(section "…: measures of burden for headache management in primary care", Introduction, first paragraph)' and '(…, Introduction, second paragraph, last sentence)'. | R04-02; sweep 14; R15-01 | Convergent. "consensus (SBCe, Brazil; EHF 2020)" stands, and SFEMC is correctly a national guideline (S-024 is typed as a clinical practice guideline). |
| OUT-028 | v01, v14, v15 | **v01:** "The view MUST show the source definitions" became "SHOULD show … (see OUT-002)". **v14:** the [S-027] quote was added, with "NVN, very low certainty of evidence, for leaving the diagnosis to the physician", and the Strength line gained "; SHOULD NOT for assigning a diagnosis, as in OUT-038.". **v15:** the [S-033] table 3в title is now given in Russian, and the [S-027] module label is the full title. | R01-04; sweep 14; sweep 15 | Convergent. The v01 MUST/SHOULD split is intact. |
| OUT-031 | v01, v05, v12, v14 | **v01:** the [S-007] 3.7 quote was added. **v05:** "Definition of terms" became "Definitions of terms" in the location. **v12:** the [S-007] 3.8 B items c and d were added. **v14:** [S-001] "Cluster remission period: …" was added (Definitions of terms, p. 209; the duration criterion is not quoted). The Statement and SHOULD are unchanged since v00. | R01-09; R05-01; R12-02 (a); sweep 14 | Convergent. Every element from v01, v05 and v12 is verbatim in v16. |
| OUT-033 | v09, v10, v14 | **v09:** MAY became SHOULD; the "Fort" ratings, quotes and a new Caveat were added. **v10:** the SFEMC grading system was named. **v14:** two [S-002] quotes were added (1.3.2.3.1, PHQ-9; 1.3.2.3.2, GAD-7), and the Evidence basis was extended. The Caveat "The cited sources name only the HAD scale (HADS); PHQ-9 and GAD-7 … are not named in any cited source." became "The SFEMC recommendations name only the HAD scale (HADS). PHQ-9 and GAD-7 are named, with HADS, among the validated scales for depression and anxiety in the IHS trial-methodology guideline (quoted above); none of the clinical-practice recommendations cited in this requirement names them." | R09-01; R10-01; sweep 14 | Convergent. See Findings, candidate 1. |
| OUT-034 | v14, v15 | **v14:** the [S-025] RT25 and [S-019] quotes were added. The Evidence basis gained SFEMC RT25 ("Fort"), the AAN/AHS patient summary and an indirect-support sentence for the completeness indicator. **v15:** the [S-027] label became the full module title. | sweep 14; sweep 15 | Convergent. |
| OUT-035 | v01, v15 | **v01:** the [S-031] CQ I-10 Background quote was added. **v15:** the [S-027] label became the full module title. | R01-08; sweep 15 | Convergent. |
| OUT-038 | v14, v15 | **v14:** the [S-003] 1.3.1.3 and [S-024] trigger quotes were added, and the Evidence basis gained SFEMC and IHS 2018. **v15:** the [S-027] label became the full module title. | sweep 14; sweep 15 | Convergent. |
| OUT-039 | v01 (added), v14 | **v01:** the new SHOULD requirement was added. **v14:** the [S-013] adherence quote and "consensus (EHF 2020, …)" were added. | R01-10; sweep 14 | Convergent. |
| S-024 | v09, v10 | **v09:** the Figure 3 "Fort" ratings were added, with "The article names no grading system, …". **v10:** this became "The French article does not restate the grading system; it is defined in the English version …", with the grading passage quoted and the English citation, DOI/PMID and URL added. | R09-01; R10-01 | Convergent. Unchanged since v10 (seven versions); assessed at the iteration-12 check. |
| S-025 | v09, v10 | Same pattern as S-024: Figure 1 and Tableaux in v09, then the English methods sentence, Table 6 ratings, citation and URL in v10. | R09-01; R10-01 | Convergent. Unchanged since v10. |

Items changed in exactly one version, so no back-and-forth is possible for them:
- **v01:** OUT-015, OUT-020, OUT-022 and OUT-029; S-017, S-028 and S-032.
- **v02:** S-010.
- **v03:** S-036.
- **v05:** OUT-001, OUT-004, OUT-007 and OUT-013.
- **v06:** S-026 (marked superseded); S-045 was added.
- **v07:** S-046 was added.
- **v08:** OUT-016.
- **v14:** OUT-008, OUT-009, OUT-012, OUT-019 and OUT-036. Each of these was a pure insertion of quotes and/or Evidence-basis text.
- **v15:** OUT-025 (the [S-029] label only).
- **v16:** OUT-037 (see Findings, candidate 2).

Unchanged since v00:
- OUT-017, OUT-030 and OUT-032;
- S-001–S-009, S-011–S-016, S-018–S-023, S-027, S-029–S-031, S-033–S-035 and S-037–S-044;
- sections 1 and 2, and the preambles of sections 3, 5, 6 and 7;
- 21 of the 25 search-log rows.

## Findings
None.

No item, field or clause returns to an earlier state:
- **Quotes.** None was removed and later restored. The only quotes ever removed are the two [S-026] quotes, taken out once in v06.
- **Quote locations.** No location has had more than two states. Every location was corrected at most once: in v01, v02, v04, v05, v14 or v15. The 15 labels changed in v15 include none of those corrected in v04 or v05, and the singular "Definition of terms" has not reappeared since v05.
- **Strength.** RFC 2119 keywords changed only in v01 (four MUST/SHOULD splits), v09 (OUT-033, MAY to SHOULD) and v16 (OUT-037, scope narrowed to migraine). None has flipped back.
- **Withdrawals and sources.** No requirement or source was withdrawn and re-added.
- **Remarks.** All 35 remarks were fixed. None was declined, so no declined remark was re-raised. No remark proposed reversing an earlier fix.

The following candidates were examined and rejected:

1. **OUT-033, the Caveat on PHQ-9 and GAD-7 (added in v09, corrected in v14).**
   - **Trace.**
     - v00–v08: the Statement names "HADS, PHQ-9, GAD-7" as examples, and nothing in the requirement says which sources name them.
     - v09: the fixer added a Caveat on its own initiative ("The remark did not ask for this line"), based on R09-01's statement "PHQ-9 and GAD-7 remain examples that no cited source names". It reads: "PHQ-9 and GAD-7 … are not named in any cited source."
     - v14: the sweep found that [S-002], cited in OUT-033 since v00, names both (1.3.2.3.1 "include … PHQ-9"; 1.3.2.3.2 "GAD-7 … can be used"). It quoted both and rewrote the Caveat as shown in the table above.
   - **Why this is not oscillation.**
     - The v14 state is new. It is neither the silent v00–v08 state nor the v09 state: it adds quotes and keeps the correct part of v09 ("The SFEMC recommendations name only the HAD scale"; "none of the clinical-practice recommendations cited … names them").
     - The v09 claim was false when it was written, so this is the correction of a factual error, made once.
     - The v14 change was not driven by a remark, and no later remark contests it. Review 15 found "the corrected OUT-033 caveat" accurate, and reviews 16, 16b and 16c raised nothing on it.
     - R09-01's rule that "The Rationale must not attribute them to a source" still holds: the Rationale has not changed since v09.
   - This is the same pattern as the v09 "no grading system" wording, which v10 replaced and which the iteration-12 check rejected.
2. **OUT-037, re-scoped in v16 (R16c-01).**
   - **Trace.** OUT-037 was byte-identical from v00 to v15. Its Statement then read "SHOULD NOT present a composite headache index … as a primary measure", its Evidence basis listed "international trial-methodology guideline (IHS TTH 2010)" as support, and its Rationale began "Regulatory guidance and IHS methodology warn that …".
   - **What v16 changed:**
     - the title gained "for migraine";
     - the SHOULD NOT and the exploratory-label SHOULD now apply to migraine;
     - a new SHOULD sentence covers tension-type headache: show headache days with AUC;
     - [S-006] became a counter-position, its quote's location now states its role as a caveat, two [S-006] quotes were added to Evidence and two more to a new Caveats line;
     - the Strength line names all three clauses, and the primary strength is still SHOULD NOT.
   - **Why this is not oscillation.**
     - No review or fix from 01 to 16b mentions AUC, "headache index" in S-006, or S-006 as support for OUT-037. Fix 14 checked only the component-measures element, against S-022.
     - Reviews 16 and 16b returned NO_REMARKS. That is not a remark, so it is not an opposite push.
     - The change is the first since v00 and runs in one direction. Fix 16 also declined the optional S-002 composite-endpoint quote, which no one had added before.
3. **OUT-024 (v12, v13, v14).**
   - **What each remark offered.** R12-01, R13-01 and R14-01 each offered "(a) add support" or "(b) remove or restrict the element", and each fixer chose (a).
   - **What v13 changed.** It narrowed the attribution in the v12 Evidence-basis sentence, from "The grouping by drug class rests on the EHF consensus (2020)" to "The grouping of preventive treatments …". It added [S-012] support for the acute list. The claim that both lists are supported by consensus was kept.
   - **Further checks:**
     - R13-01 states that it "does not reverse R12-01", and R14-01 that it "reverses no fix".
     - The v14 word diff shows only insertions.
     - Review 15 checked the "indirect support" sentence and did not raise it.
   - Every push went the same way: towards adding support for Statement elements present since v00.
4. **Location labels changed in v04, v05 and v15.**
   - **Script results.** Every quote's location has at most two states. v15 touched none of the v04 labels (OUT-003 [S-013]) or the v05 labels (ICHD-3 "Definitions of terms"; OUT-013 "end of the paragraph beginning …").
   - **Three v15 changes had been viewed differently earlier, but none came from a remark:**
     - **[S-033] table titles (OUT-014, OUT-028).** Reviews 07, 09, 10, 11, 11b, 12, 13 and 15 called the English titles faithful renderings, in coverage notes and not as remarks. The v15 sweep replaced them with the Russian titles as printed and kept the English meaning after them. Review 16 confirmed the change. This is a single change.
     - **[S-021] label in OUT-002.** It was created in v14, accepted in review 15's coverage table and corrected once in v15 to the Annex title. Reviews 16 and 16b confirmed it.
     - **[S-042] label in OUT-011.** v15 moved it to Table 2, the place that reviews 04 and 15 had noted holds the quoted wording.
   - None of these labels has returned to an earlier value.
5. **OUT-018, R14-03 against R01-05.**
   - R14-03 kept the conditional clause "(and, where reported, moderate/severe headache days)" at MUST by adding [S-002] recommendation b. R01-05 had set moderate/severe headache days at SHOULD among the components of OUT-021.
   - These are different requirements and different questions:
     - OUT-018's clause has been unchanged since v00 and applies only where the output is reported;
     - OUT-021's v01 component list is unchanged.
   - R14-03 explains why R01-05's objection does not apply. Neither item has moved back.
6. **OUT-010, a latent divergence.** It drove no change.
   - Fix 14 did not quote the intensity-scale passages (S-002 1.3.2.1.4–1.3.2.1.5 and others), calling them rating instructions excluded by PROCESS.md section 2.
   - Review 16, under "Checked and not raised", called adding S-020 III.B.5 ("A four-point Likert scale should be used for headache pain") or S-002 1.3.2.1.4 "optional".
   - Neither is a remark, and OUT-010 did not change after v15.
7. **Earlier watch-list conditions.** Every condition from the iteration-12 check still holds:
   - OUT-014's MUST does not rest on "SEN, grade B";
   - OUT-023 keeps headache relief, sustained relief and per-attack adverse events;
   - OUT-031 keeps the 15-minute, attacks-per-day and rescue elements with their quotes;
   - OUT-033 stays SHOULD, with the SFEMC grading system named; neither "suggestion" nor "no grading system" has returned, and the wording of fix-iter-11 has not recurred;
   - OUT-005 keeps its v01 split;
   - OUT-018 keeps SIGN 155 section 4.1 labelled as ungraded;
   - OUT-021 keeps its MUST core OUT-004/005/014;
   - OUT-026 keeps SEN 2026 as conflicting evidence, and SHOULD.

## Watch list
Bookkeeping by design:
- **Header, section 4 and section 7** (changed in v01–v16). The change log has been append-only since v02.
- **Section 6** (changed in v06, v07, v10 and v11). Four different rows, each changed once, and unchanged since v11.

Requirements changed in three or more versions. Each is convergent, and every later change kept the earlier ones:
- **OUT-002** (v05, v14, v15). v14 added quotes and clarified the [S-003] location. v15 fixed two labels and kept the v05 plural heading. Restoring the singular heading, or the v14 [S-021] "section" label, would be oscillation.
- **OUT-011** (v01, v02, v15). Two quotes, each relocated once. The S-035 location from v02 is intact.
- **OUT-014** (v06, v07, v11, v15). Every step kept the earlier ones. The MUST, the per-drug clause, the ICHD-3 notes and the ungraded SEN 2026 label stand. Returning the [S-033] title to an English rendering would be oscillation.
- **OUT-018** (v01, v07, v14). v14 was an insertion. SIGN 155 section 4.1 stays labelled as ungraded, and lowering the moderate/severe clause while its v14 quote stands would be oscillation.
- **OUT-021** (v01, v02, v14). v14 was an insertion. The MUST core and the SHOULD components are unchanged since v02.
- **OUT-023** (v01, v02, v08, v14). Every step was an insertion. Removing any element added in v01, v02 or v08, or a quote added in v14, would be oscillation.
- **OUT-024** (v12, v13, v14). v13 narrowed only the attribution of the v12 sentence. v14 was an insertion, and the Statement is unchanged since v00. Removing "grouped by drug class", or the dates, dose or duration elements, while their quotes stand would be oscillation.
- **OUT-026** (v01, v06, v14, v15). The SEN 2026 conflict and SHOULD are unchanged since v06. v14 was an insertion, and v15 changed one v00 label.
- **OUT-027** (v04, v14, v15). SBCe stays under consensus. v14 was an insertion, and v15 changed two v00 labels.
- **OUT-028** (v01, v14, v15). The v01 MUST/SHOULD split is intact. v14 named the SHOULD NOT clause, and v15 changed labels only.
- **OUT-031** (v01, v05, v12, v14). Four different defects, each fixed once. All earlier elements are verbatim in v16.
- **OUT-033** (v09, v10, v14). SHOULD and the named SFEMC grading system stand. v14 corrected the factual error about PHQ-9 and GAD-7. Restoring "not named in any cited source", MAY or "suggestion" would be oscillation.

Also under observation (fewer than three changes, or flagged by the orchestrator):
- **OUT-037** (v16 only). It is now limited to migraine, with [S-006] as a counter-position and a SHOULD for tension-type headache. Re-extending the SHOULD NOT to all headache types, or listing [S-006] as support again, would be oscillation.
- **OUT-010 and OUT-029.** Both cite the S-006 2.3.3.2 sentence on intensity. Fix 16 notes that, in context, the sentence argues for AUC as the primary measure, but judged that it still supports the intensity outputs, and neither requirement was changed. A later remark on their use of this quote would concern items that are now stable.
- **OUT-010** also has the latent divergence on scale quotes (Findings, candidate 6).
- **OUT-005, S-024 and S-025** (two changes each). Unchanged since v07, v10 and v10 respectively. The iteration-12 conditions still hold.

## Trend
| Iteration | Remarks (types) | Fixed / declined | Lines changed in the document (+/−) | Statements changed | Strength changes |
|---|---|---|---|---|---|
| 01 | 11 (3 link/citation, 1 contradiction, 2 strength-mismatch, 3 unsupported/overstated, 2 missing-requirement) | 11 / 0 | +61 / −21 | OUT-005, 021, 023, 028, 029; OUT-039 added | SHOULD clauses split out of 4 MUST requirements |
| 02 | 2 (1 missing-requirement, 1 factual-error) | 2 / 0 | +24 / −11 | OUT-021, OUT-023 | none |
| 03 | 1 (link/citation) | 1 / 0 | +7 / −3 | none | none |
| 04 | 2 (1 link/citation, 1 contradiction) | 2 / 0 | +9 / −4 | none | none |
| 05 | 1 (link/citation) | 1 / 0 | +17 / −12 | OUT-001, 002, 004, 007 (heading name only) | none |
| 06 | 1 (outdated-source) | 1 / 0 | +18 / −10 | none | none |
| 07 | 2 (1 unsupported/overstated, 1 factual-error) | 2 / 0 | +23 / −9 | none | none |
| 08 | 2 (1 missing-requirement, 1 contradiction) | 2 / 0 | +18 / −8 | OUT-016, OUT-023 | none |
| 09 | 1 (strength-mismatch) | 1 / 0 | +21 / −7 | OUT-033 | OUT-033 MAY → SHOULD (totals 10/24/4/1) |
| 10 | 1 (link/citation) | 1 / 0 | +14 / −6 | none | none |
| 11 | review: 0 (NO_REMARKS); re-check 11b: 2 (1 unsupported/overstated, 1 factual-error) | 2 / 0 | +14 / −4 | none | none |
| 12 | 2 (2 unsupported/overstated) | 2 / 0 | +11 / −3 | none | none |
| 13 | 1 (unsupported/overstated) | 1 / 0 | +14 / −4 | none | none |
| 14 | 4 (4 unsupported/overstated), plus a fixer's sweep for unquoted Statement elements (32 elements in 18 requirements) | 4 / 0 | +66 / −19 | none (no Statement text changed) | none |
| 15 | 1 (link/citation), plus a fixer's sweep of quote locations (12 further labels) | 1 / 0 | +28 / −17 | none | none |
| 16 | review: 0 (NO_REMARKS); re-check 16b: 0 (NO_REMARKS); re-check 16c: 1 (unsupported/overstated) | 1 / 0 | +21 / −7 | OUT-037 (title and Statement narrowed to migraine; new SHOULD sentence for tension-type headache) | OUT-037: SHOULD NOT now limited to migraine; totals unchanged (10/24/4/1) |

The loop is converging slowly, without looping:
- **Remark counts.** Per iteration: 11 → 2 → 1 → 2 → 1 → 1 → 2 → 2 → 1 → 1 → 0+2 → 2 → 1 → 4 → 1 → 0+0+1. That is 35 remarks in total, all fixed and none declined.
- **Iteration 16.** It came closest to ending: the review and the first re-check both returned NO_REMARKS, and only the second re-check found a defect.
- **The spike in iteration 14.** Four remarks of one type were found at once: unquoted Statement elements present since v00. The fixer then swept the whole class, and iterations 15 and 16 each produced only one remark.
- **The sweeps.** Both were one-directional: v14 only inserted quotes and Evidence-basis text, and v15 only corrected location labels. Neither reversed any earlier change.
- **Depth of change.** v13–v15 changed no Statement and no strength. v16 changed one Statement (OUT-037), for a defect present since v00. Removed lines in v14–v16 are replaced labels or extended clauses, not withdrawn content.
- **Stability.** Since v09 there have been 39 requirements (10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT). Since v07 there have been 46 source rows, 45 of them cited. No S-xxx row has changed since v10, and no search-log row since v11.
- **Quote accuracy.** Reviews 13–16c re-verified every quote: 227, 229, 252, 288, 295 and 295 strings. None found a misquote.
- **Remaining remark type.** R16c-01 found a quote whose surrounding source text contradicts the use made of it. Script checks cannot find this kind of defect. A few more such cases may surface. They are new defects in content unchanged since v00, not reversals.
