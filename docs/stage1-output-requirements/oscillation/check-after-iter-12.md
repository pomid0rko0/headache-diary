# Oscillation check — after iteration 12
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: v00–v12; reviews 01–12 (incl. 11b); fixes 01–12
Date: 2026-10-20

## Method
I read PROCESS.md, the 13 snapshots, all 13 reviews (01–12 and 11b), the 12 fix logs, the iteration-04 and iteration-08 checks, and `git log -p` for OUTPUT_REQUIREMENTS.md. Each fix commit's document is byte-identical to its `history/vNN.md`, OUTPUT_REQUIREMENTS.md equals v12, no other commit touched the document, and FROZEN_ITEMS.md does not exist. A script split every snapshot into items (the header; sections 1, 2 and 4; the section 3 preamble; each OUT-xxx block and each of its fields; each S-xxx row; each search-log row; each change-log entry), hashed each item per version and flagged any state equal to an earlier one; at a finer grain it tracked every sentence and clause of every item (flagging removed-then-restored and added-then-removed patterns), every quote with its location, the RFC 2119 keywords of each Statement and "Strength:" line, the strength totals and the set of sources cited per requirement. I then word-diffed every changed item version by version and searched all reviews and fixes for remarks, offered options and "Checked and not raised" notes that push an item the other way.

## Change history of items changed in two or more versions
| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| Header (version line) | v01–v12 | v01: "Version: v00 · Iteration: 00 · Status: draft" became "Version: v01 · Iteration: 01 · Status: under review". v02–v12: version and iteration +1 each time; status stays "under review". | Loop bookkeeping | Convergent. Mechanical, one direction. |
| Section 4 (Withdrawn requirements) | v01–v12 | "None (v00)." became "None (as of v01).", then "(as of v02)" … "(as of v12)". No requirement was ever withdrawn. | Fixers' "Other changes" | Convergent. Mechanical, one direction. |
| Section 7 (Change log) | v01–v12 | One entry appended per version. The only in-place edit is still v02's correction of the v01 counting rule (R02-02). Every entry is byte-identical from the version after it was written. The v09 entry moved the totals from 10 MUST, 23 SHOULD, 5 MAY, 1 SHOULD NOT to 10/24/4/1; v10–v12 repeat 10/24/4/1. | R02-02; otherwise bookkeeping | Convergent. Append-only since v02. |
| Section 6 (Search log) | v06, v07, v10, v11 | Four different rows, each changed once. v06 "Spanish" (SEN 2026, S-045). v07 "English — regulators" (FDA 2023 draft, S-046). v10 "French": "sfemc.fr (Recommandations page)." gained the IHS page "Affiliate Society and other guidelines", and the row now records the English versions of SFEMC Parts 1 and 2 "found on the IHS website and used from v10", plus "In iteration 09 the English full texts of Parts 1 and 2 could not be read (doi.org redirected to ScienceDirect, which returned HTTP 403 …)". v11 "Finnish": "No current Käypä hoito migraine guideline appeared in the kaypahoito.fi recommendation list." became a record of the Käypä hoito recommendation "Migreeni" (published 28.03.2024), "found in iteration 11 and not used", with "Up to v10 this row said that no … list; that was wrong (R11b-02)". All other rows and the gap list are unchanged since v00. | R06-01; R07-02; R10-01; R11b-02 | Convergent. No row has been touched twice. The v10 and v11 edits correct or extend text unchanged since v00. |
| OUT-005 | v01, v07 | v01: the definition label split out of the MUST into a SHOULD sentence. v07: the [S-046] FDA primary-endpoint quote added; Evidence basis "(EMA 2026; FDA 2023)". | R01-04; R07-02 | Convergent. Unchanged since v07 (six versions). |
| OUT-011 | v01, v02 | v01: [S-035] quote added; v02: its location corrected. | R01-08; consequential to R02-01 | Convergent. Unchanged since v02. |
| OUT-014 | v06, v07, v11 | v06: [S-026] "debe promoverse el uso de diarios para monitorizar su cefalea y el uso de medicación (nivel de evidencia II, grado de recomendación B)" replaced by [S-045] "Debe promoverse el uso de diarios para monitorizar su cefalea y el uso de medicación." ("no level of evidence or grade of recommendation is attached"); "SEN, grade B" removed from the graded recommendations and "SEN 2026, Spain, a statement without a level of evidence or grade of recommendation" listed under national guidelines. v07: [S-046] "Change from baseline in the number of days per month subjects use an acute/rescue medication to treat an acute migraine" added; "regulatory draft guidance (FDA 2023)" added to Rationale and Evidence basis. v11: five [S-001] ICHD-3 notes added after the item-12 quote, beginning with 8.2 note 1 "Patients should be coded for one or more subtypes of 8.2 Medication-overuse headache according to the specific medication(s) overused and the criteria for each below." and 8.2.2 note 1 "The triptan(s) will usually be specified in parenthesis.", plus the 8.2.3.2, 8.2.4 and 8.2.5 notes. One sentence was inserted into the Evidence basis: "The breakdown by drug class and by individual drug rests on ICHD-3, which codes medication-overuse headache according to the specific medication(s) overused (code 8.2, note 1) and, in the notes to subtypes 8.2.2, 8.2.3.2, 8.2.4 and 8.2.5, provides for the individual drugs to be specified in parenthesis with the code." The Statement has been unchanged since v00, and the Strength has been "MUST" in all 13 versions. | R06-01; R07-02; R11b-01 (option a) | Convergent. The v11 word diff contains only insertions. The v06 SEN quote with its ungraded label and the v07 FDA quote are verbatim in v12, and "SEN, grade B" has not returned. R11b-01 offered option (b), moving "and by individual drug" to SHOULD. No earlier remark or fix had touched that clause, so (b) would not have reversed anything; the fixer chose (a). See the watch list. |
| OUT-018 | v01, v07 | v01: the [S-015] 1.3.29 and [S-002] 1.3.1 quotes added. v07: SIGN 155 relabelled as "national guideline text (SIGN 155, section 4.1 introduction; not a graded recommendation or good-practice point)". | R01-08; R07-01 | Convergent. Unchanged since v07. |
| OUT-021 | v01, v02 | v01: MUST core OUT-004/005/014; other components SHOULD. v02: OUT-023 component added at SHOULD. | R01-05 (option b), R01-08; R02-01 | Convergent. Byte-identical from v02 to v12 (eleven versions). |
| OUT-023 | v01, v02, v08 | v01: timing-of-intake SHOULD sentence; the cluster sentence cites [S-007]. v02: baseline versus on-treatment SHOULD sentence. v08: headache relief at 2 hours [S-004], "whether that relief was maintained to 24 hours" and per-attack "drug-related adverse events after intake"; conflicting-evidence Caveat. Strength "SHOULD" throughout. | R01-09, R01-11; R02-01; R08-01 | Convergent. Every step was a pure insertion. Byte-identical from v08 to v12. See the watch list. |
| OUT-026 | v01, v06 | v01: [S-041] location "(Discussion)" became "(Conclusion)". v06: SEN 2020 support removed; SEN 2026 MIDAS/HIT-6 position added as conflicting evidence; [S-045] PGIC sentence added. | R01-02; R06-01 | Convergent. Unchanged since v06. |
| OUT-031 | v01, v05, v12 | v01: [S-007] "Pain-freedom at 15 minutes without recurrence of any level of pain within 3 hours in the 1st treated attack." added (section 3.7). v05: [S-001] location "(Definition of terms, p. 209)" became "(Definitions of terms, p. 209)". v12: [S-007] list items "Percentage of attacks with need for rescue therapy" and "Number of attacks per day during the study period" (section 3.8 "Secondary endpoints", list B, items c and d, p. 22) added directly after the 3.7 quote. Statement, Rationale, Evidence basis and Strength ("SHOULD") unchanged since v00. | R01-09; R05-01; R12-02 (option a) | Convergent. These are three different defects. v12 is a pure insertion, and the v01 quote and the v05 location are verbatim in v12. R01-09 and R12-02 each offered "quote it or remove the element", and each fixer quoted. Both pushes went the same way. See the watch list. |
| OUT-033 | v09, v10 | v09: Statement "the diary output MAY report them" became "… SHOULD report them". The Rationale "the French guideline suggests HADS as an assessment tool" became an SFEMC "strong recommendation (rated "Fort" in its summary figure)" for HAD (Rd5), plus RT25 (HIT-6 and HAD "at every visit"). The Evidence basis "National guideline (SFEMC, France, suggestion); international trial-methodology guideline (IHS). Strength: MAY." became "National guideline (SFEMC, France: recommendation Rd5 [S-024] and recommendation RT25 [S-025], both rated "Fort" (strong) in the guideline's summary figures, which give a strength of recommendation but no level of evidence for these items; neither article names a grading system); … Strength: SHOULD. MUST is not supported, …". The [S-024] Rd5, [S-025] RT25 and [S-024] p. 400 quotes were added, with a new Caveats line (PHQ-9 and GAD-7 are not named in any cited source; a HAD score is not specific). v10: Evidence basis only. "neither article names a grading system" was replaced by "The guideline's grading system is defined in the English version of Part 1 (section 2.2 "Guideline development", p. 726 …): strength-of-recommendation grades "Strong", "Moderate", "Weak" and "Not recommended", given "for clinical implication", and, separately, levels of evidence "High", "Moderate" and "Low"", with the definition of "Strong". The "Strong" ratings in English Tables 3 and 6 were added, and the MUST reasoning gained "not a diary output, and give no level of evidence". | R09-01; R10-01 | Convergent. Strength went MAY → SHOULD once, and no remark has argued for MAY or MUST since. v10 removed only the clause "neither article names a grading system" and kept every other v09 element. See Findings (rejected candidate 1) and the watch list. |
| S-024 | v09, v10 | v09: "Clinical practice guideline (national society, SFEMC)" was extended with the p. 401 pointer "Elles sont résumées sur la figure 3.", "all ten are rated "Fort" (strong)" and "The article names no grading system, does not define the strength labels and gives no level of evidence for Rd1–Rd10." v10: the type became "(national society, SFEMC; levels of evidence "High", "Moderate" and "Low"; strength-of-recommendation grades "Strong", "Moderate", "Weak" and "Not recommended"; …)". "The article names no grading system, does not define the strength labels" became "The French article does not restate the grading system; it is defined in the English version, section 2.2 …", with that passage quoted. Also added: Table 3 rates Rd1–Rd10 "Strong"; "Neither Figure 3 nor Table 3 gives a level of evidence for Rd1–Rd10."; the full English citation, DOI/PMID, IHS URL and a language note. | R09-01; R10-01 | Convergent. v10 kept the v09 Figure 3 text, the "Fort" ratings and the absence of a level of evidence. Only the factual sub-claim about the grading system was refined, using newly reachable evidence. |
| S-025 | v09, v10 | v09: Figure 1 ratings added (RT15–RT32 "Fort", RT33–RT34 "Modéré"), the Tableaux I/II columns, "The article names no grading system and does not define these labels." and "(PDF page + 411 = printed page)". v10: the type now names the SFEMC 2021 grading system by reference to S-024. "names no grading system and does not define these labels" became "The French article does not restate the grading system." Added: the English methods sentence "Methods are described in the first part of the updated guidelines [1] (Appendix 1)." (p. 735), the note on the English evidence-level values, the Table 6 ratings, and the English citation, DOI/PMID and URL. | R09-01; R10-01 | Convergent. Same pattern as S-024. |

Items changed in exactly one version, so no back-and-forth is possible for them:
- **v01:** OUT-015, OUT-020, OUT-022, OUT-028, OUT-029 and OUT-035; OUT-039 was added; S-017, S-028 and S-032.
- **v02:** S-010.
- **v03:** S-036.
- **v04:** OUT-003 and OUT-027.
- **v05:** OUT-001, OUT-002, OUT-004, OUT-007 and OUT-013.
- **v06:** S-026 (marked superseded); S-045 was added.
- **v07:** OUT-006; S-046 was added.
- **v08:** OUT-016.
- **v12:** OUT-024. Two [S-013] "Drug failure" quotes were added: "One of the main criteria to define resistance and refractoriness to treatment is the number of failed classes of medications." and "The Consensus group agreed to select failure of drug classes, rather than single medications, …". One Evidence-basis sentence was inserted. The Statement, Rationale and Strength (SHOULD) are unchanged since v00.

Unchanged since v00:
- OUT-008, 009, 010, 012, 017, 019, 025, 030, 032, 034, 036, 037 and 038;
- S-001–S-009, S-011–S-016, S-018–S-023, S-027, S-029–S-031, S-033–S-035 and S-037–S-044;
- sections 1 and 2, and the preambles of sections 3, 5, 6 and 7;
- 21 of the 25 search-log rows.

## Findings
None.

No item returns to an earlier state, either whole or in part. No quote was removed and later restored, and no quote location has had more than two states. No source cited in a requirement was dropped and re-added; the only removals are the two [S-026] quotes, taken out once in v06. No requirement or source was withdrawn and re-added. RFC 2119 keywords changed only in v01 (the four MUST/SHOULD splits) and once in v09 (OUT-033, MAY → SHOULD), and none has flipped back. No fixer declined a remark, so no declined remark was re-raised.

These candidates were examined and rejected:
1. **S-024, S-025 and OUT-033: "no grading system" (v09, R09-01), replaced in v10 (R10-01).** This is the only clause in the loop that was introduced by one fix and taken out by the next.
   - **No return to an earlier state.** The sequence of states is:
     - v00–v08: the entries say nothing about a grading system;
     - v09: they state that none is named;
     - v10: they name the system and quote its definition.
   - **No opposite pushes.** R09-01 and R10-01 push the same way: both make the SFEMC strength label traceable, and both support SHOULD. R10-01 states that "the "Fort" ratings, the quotes, the "no level of evidence for these items" statement and OUT-033's SHOULD all stand".
   - **What the v10 word diff shows.** It removes only "names no grading system, does not define the strength labels" (S-024), "names no grading system and does not define these labels" (S-025) and "neither article names a grading system" (OUT-033). The replacement, "The French article does not restate the grading system; it is defined in the English version", keeps the v09 point about the French article.
   - **New evidence.** R10-01 rests on the IHS-hosted English full texts, which the v09 fixer could not reach (ScienceDirect HTTP 403, recorded in fix-iter-09).
   - This is the correction of a different defect (the grading system is not named, PROCESS.md section 3) by refinement, not a reversal. Review 08 ("It names no grading system, so there is nothing to require") and review 09 ("because SFEMC names no grading system") said the opposite only under "Checked and not raised". Those notes were not remarks and drove no change.
2. **OUT-033 strength.** It went MAY → SHOULD once, in v09. Before iteration 09 no remark addressed OUT-033; review 05 listed it only as coverage for HADS. Since then:
   - review 10 states "The strength of OUT-033 (SHOULD) is not affected";
   - review 11 finds the AAN/AHS paediatric statement 6a supports OUT-033 "at SHOULD";
   - reviews 11b and 12 raise nothing on it.

   Fix-iter-11 cites OUT-033 as a case of "ungraded national text" that cannot carry a MUST. That label does not match the v10 Evidence basis, which records a "Strong" grade under a named system but no level of evidence. It is a description in a log only; it changed nothing and was not a remark, so it is recorded on the watch list.
3. **OUT-014, the per-drug clause.** R11b-01's option (b) would have lowered "and by individual drug" to SHOULD. The clause has been MUST and unchanged since v00, and no earlier remark raised it, so option (b) was not a reversal of any fix. The fixer kept MUST with classification-standard quotes. The iteration-08 condition still holds: the MUST does not rest on SEN.
4. **OUT-014 per drug (R11b-01) against OUT-024 per class (R12-01).** The new [S-013] quote prefers "drug classes, rather than single medications". The two remarks act on different items and different outputs: acute-medication days in OUT-014, the preventive treatment history in OUT-024. Neither Statement changed. OUT-024 still lists individual treatments, grouped by class, as fix-iter-12 notes. These are not opposite pushes on one item.
5. **OUT-024 and OUT-031, option (b) of R12-01 and R12-02 (remove the unquoted elements).** These elements have been unchanged since v00, and no earlier fix strengthened them. Both fixers chose (a), adding quotes, as the fixer of R01-09 did for OUT-031's 15-minute element. All three point the same way.
6. **Finnish search-log row.** Review 08 noted under "Checked and not raised" that "there is still no Käypä hoito migraine guideline". R11b-02 showed that there is one. The row was unchanged from v00 to v10 and changed once, in v11. The review 08 note drove no change. This is the same pattern as R07-02 (regulators row).
7. **OUT-023, the iteration-08 watch points.** "Whether that relief was maintained to 24 hours" and per-attack adverse events are unchanged since v08. Review 09 found SFEMC Rt1 ("avec une réponse soutenue pendant 24 heures et sans effets indésirables", rated "Fort") consistent with them, and no remark proposed removing them.

## Watch list
- **OUT-014** (changed in v06, v07 and v11). Convergent: each change kept the earlier ones, and v11 is a pure insertion after the v06 SEN quote and the v07 FDA quote. Any of these would be oscillation:
  - the MUST resting again on "SEN, grade B";
  - removing the v11 ICHD-3 per-drug notes;
  - lowering "by individual drug" to SHOULD while those notes stay quoted.
- **OUT-023** (changed in v01, v02 and v08; unchanged for four versions). Convergent and carried over. Removing headache relief, sustained relief or per-attack adverse events, or reversing any element added in v01 or v02, would be oscillation.
- **OUT-031** (changed in v01, v05 and v12). Convergent: three different defects. v12 kept the v01 3.7 quote and the v05 "Definitions of terms" location verbatim. Removing "attacks per day", "the need for rescue treatment" or the 15-minute element while their quotes stand would be oscillation.
- **Header, section 4 and section 7** (changed in v01–v12). Bookkeeping by design; the change log has been append-only since v02.
- **Section 6** (changed in v06, v07, v10 and v11). Four different rows, each changed once. Touching any of them again in the opposite direction would be oscillation.
- **Also under observation** (two changes each, convergent):
  - **OUT-033, S-024 and S-025** (v09, v10). OUT-033 is SHOULD, resting on SFEMC Rd5 and RT25, rated "Fort"/"Strong" under the named SFEMC 2021 grading system, with no level of evidence. Any of these would be oscillation:
    - restoring "suggestion" or MAY;
    - describing the SFEMC entries again as having no grading system, or as ungraded (the fix-iter-11 wording is a latent instance);
    - removing the English-version grading text.

    Raising OUT-033 to MUST would be a new direction rather than a reversal, but fix-iter-10 and review 11 have both argued against it.
  - **OUT-005, OUT-018, OUT-021 and OUT-026**, unchanged since v07, v07, v02 and v06 respectively. The iteration-08 conditions still hold:
    - OUT-005 keeps its v01 MUST/SHOULD split;
    - SIGN 155 section 4.1 stays labelled ungraded in OUT-018;
    - OUT-021 keeps its MUST core OUT-004/005/014;
    - in OUT-026, SEN 2026 stays as conflicting evidence and the strength stays SHOULD.

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

The loop is converging, slowly:
- **Remarks per iteration:** 11 → 2 → 1 → 2 → 1 → 1 → 2 → 2 → 1 → 1 → 0 + 2 → 2. The count has stayed at 1–2 since iteration 02. Iteration 11 produced the first NO_REMARKS verdict, but its first re-check found 2 remarks.
- **Depth of change is falling.** No Statement and no strength has changed since v09. v10–v12 changed only evidence, source metadata and search-log rows. Removed lines per version went from −7 to −6, −4 and −3, and in v12 the only removed lines are the two bookkeeping lines.
- **No looping.** No item returned to an earlier state. Every remark was fixed (28 in total, counting 11b) and none was declined or re-raised. The totals are stable: 39 requirements (10 MUST, 24 SHOULD, 4 MAY, 1 SHOULD NOT since v09) and 46 source rows, 45 of them cited, since v07.
- **One new pattern.** R10-01 is the first remark in the loop that corrected wording added by the immediately preceding fix. It refined that wording with newly reachable evidence and did not revert it.
- **Remaining remark type.** R11b-01, R12-01 and R12-02, like R01-09 earlier, all concern Statement elements present since v00 that had no supporting quote. Each was resolved by quoting a source already cited. Other requirements may hold more such elements, so the 1–2 plateau may continue for a few iterations. These remarks add evidence and do not move items back and forth.
- **Quote accuracy.** Reviews 09–12 re-verified every quote in section 3 (213, 217, 218, 213 in 11b, and 220 distinct strings) and found no misquote.
