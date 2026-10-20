# Oscillation check — after iteration 04
VERDICT: NO_OSCILLATION
FROZEN_COUNT: 0
Examined: v00–v04; reviews 01–04; fixes 01–04
Date: 2026-10-20

## Method
I read PROCESS.md, all five snapshots, all four reviews and fix logs, and `git log -p` for OUTPUT_REQUIREMENTS.md; each fix commit's document equals its `history/vNN.md` snapshot, and OUTPUT_REQUIREMENTS.md equals v04. A script split every snapshot into items: each OUT-xxx block and each of its fields (title, Statement, Audience, Rationale, Evidence basis, Evidence, Caveats), each S-xxx row of section 5, the header, and sections 1–7. It hashed every item in every version to find the versions in which each item changed, and flagged any state that returned to an earlier hash. At a finer grain it tracked each quote line (with and without its location), the RFC 2119 keywords of each Statement and "Strength:" line, and the set of sources cited per requirement. I then compared the actual text of every changed item, version by version, against the remarks and fix decisions that drove it, and checked whether remarks in different iterations pushed the same item in opposite directions.

## Change history of items changed in two or more versions
| Item | Versions in which it changed | What changed each time | Driving remarks | Assessment (convergent / oscillating) |
|---|---|---|---|---|
| Header (version line) | v01, v02, v03, v04 | v01: "Version: v00 · Iteration: 00 · Status: draft" became "Version: v01 · Iteration: 01 · Status: under review". v02–v04: the version and iteration number went up by one each time; the status stayed "under review". | Loop bookkeeping, done by each fixer as instructed | Convergent. Mechanical, one direction only. |
| Section 4 (Withdrawn requirements) | v01, v02, v03, v04 | "None (v00)." became "None (as of v01).", then "None (as of v02).", "None (as of v03).", "None (as of v04)." No requirement was ever withdrawn. | Fixers' "Other changes" in fixes 01–04 | Convergent. Mechanical date stamp, one direction only. |
| Section 7 (Change log) | v01, v02, v03, v04 | v01: v01 entry appended, with totals "counted by the strongest keyword in each statement". v02: that phrase in the v01 entry replaced in place by "counted by the primary strength, that is, the first RFC 2119 term in each requirement's "Strength:" line", with a bracketed note "[Corrected in v02 (R02-02): ...]"; v02 entry appended. v03, v04: entries appended only. The totals (10 MUST, 23 SHOULD, 5 MAY, 1 SHOULD NOT) have been the same since v01. | R02-02 (the v02 in-place correction); otherwise bookkeeping | Convergent. Append-only apart from one defect fix that has not been reverted or challenged. |
| OUT-011 | v01, v02 | v01: added [S-035] "Profilaktik tedavinin başarısı, atak sıklığında ve süresinde %50'lik bir azalma ve akut atakta ilaçlara artan yanıt ile değerlendirilir.", located "(Kutu 8 "Migren Profilaktik Tedavi-Yönetim-6", preventive treatment principles, PDF p. 48)". v02: location only, changed to "(section 3.6.2 "Farmakolojik Tedavi Stratejileri: Profilaktik Tedavi", bulleted list of preventive treatment principles directly below Kutu 8 "Migren Profilaktik Tedavi-Yönetim-6", PDF p. 48)". The quote text was not changed. | R01-08 (add the quote); consequential edit for R02-01 (fix-iter-02, "Other changes") | Convergent. The location went from absent, to a wrong label, to a correct one, and never returned to an earlier state. Review 03 confirmed the v02 location on a page render, and it has not changed in v03 or v04. |
| OUT-021 | v01, v02 | v01: Statement "MUST present together ... frequency (OUT-004 to OUT-007), severity (OUT-010), migraine-associated symptoms (OUT-012), acute medication use (OUT-014), and ... (OUT-026)" was split. MUST now covers only "headache days (OUT-004), migraine days (OUT-005) and acute medication days (OUT-014)", and "Where the corresponding outputs are provided, the same view SHOULD also include" OUT-006, OUT-007, OUT-010, OUT-012 and OUT-026. Strength "MUST." became "MUST for presenting OUT-004, OUT-005 and OUT-014 together for the same periods; SHOULD for including the other components where they are provided." Quotes [S-002] section 1, [S-008] Q6 and [S-010] p. 7 were added, and the rationale and evidence basis were aligned. v02: "the effectiveness of acute treatment for the attacks treated in each of these periods (OUT-023)" was added to the SHOULD list. Rationale and evidence basis were extended (ungraded national guideline, protocol, position statement, consensus). Quotes [S-032] (second sentence, with "[...]"), [S-035], [S-042] and [S-010] p. 3 were added. | R01-05 (option b), R01-08; R02-01 | Convergent. The MUST core has not changed since v01. v02 added a new component at SHOULD, inside the structure that v01 set up, and R02-01 states that it "does not reverse that fix". No component returned to MUST, no quote was removed, and no later remark contested either change. |
| OUT-023 | v01, v02 | v01: the cluster sentence "For cluster headache, the corresponding time point is 15 minutes (see OUT-031)." became "..., as in the IHS cluster headache trial guideline [S-007] (see OUT-031)." A new SHOULD sentence was added: "For the treated attacks it summarises, the output SHOULD also show when the acute medication was taken relative to attack onset (or the pain intensity at the time of intake) ...". Quotes [S-012] ×2 and [S-024] were added, and the evidence basis gained "SFEMC, France". v02: a new SHOULD sentence was added: "When a preventive treatment is started (OUT-018), the output SHOULD allow these per-drug outcomes to be shown separately for the pre-treatment baseline period and for the on-treatment periods ...". Quotes [S-032], [S-035], [S-042] and [S-010] p. 3 were added, and the rationale and evidence basis were extended. | R01-09, R01-11; R02-01 | Convergent. Each change adds a distinct element. Strength is SHOULD throughout, and nothing was removed or restored. |

Items changed in exactly one version, so no back-and-forth is possible for them:
- **v01:** OUT-005, OUT-015, OUT-018, OUT-020, OUT-022, OUT-026, OUT-028, OUT-029, OUT-031 and OUT-035; OUT-039 was added; S-017, S-028 and S-032.
- **v02:** S-010 ("full-text quote:" became "full-text quotes:").
- **v03:** S-036 (grading system and DOI).
- **v04:** OUT-003 (location of the [S-013] quote) and OUT-027 (the Evidence basis moves "SBCe, Brazil" from "national guidelines" to "consensus").

Unchanged since v00: OUT-001, 002, 004, 006–010, 012–014, 016, 017, 019, 024, 025, 030 and 032–038; all other S-xxx entries; sections 1, 2 and 6.

## Findings
None.

These candidates were examined and rejected:
- **Clauses that moved from MUST to SHOULD in v01**: OUT-005 (definition label), OUT-021 (non-core components), OUT-028 ("show the source definitions") and OUT-029 (intensity per headache type). All four have stayed at SHOULD in v02–v04, and no later remark argued for MUST.
- **OUT-021, R01-05 followed by R02-01.** R01-05 narrowed the MUST scope, and R02-01 added a component, so the two might look like opposite pushes. They act on different axes: R01-05 calibrates the strength of existing components, while R02-01 adds a missing component at SHOULD under R01-05's own rule. Neither undoes the other.
- **Quoting numeric criteria.** R01-07 led to the IHS Q12 limits being quoted in full in OUT-015. Fix 02 omitted the 50% criterion from the new [S-032] quote with "[...]". These are different items, and both follow the same rule (document section 1: quoted criteria are not requirements). OUT-015 was not touched again.
- **OUT-027 and S-036/S-037.** R03-01 changed the S-036 entry and R04-02 changed OUT-027's Evidence basis. Both move towards more precise typing of the sources, and neither reverses the other.

## Watch list
- **Header, Section 4 and Section 7**: each changed in v01–v04. These are bookkeeping updates the loop makes by design (version stamp, "as of vNN" note, appended change-log entry). The single in-place edit to an older change-log entry (R02-02) was a defect fix and has not been revisited. No risk of oscillation.
- No requirement or source entry has changed in 3 or more versions. Note for the next check: OUT-021 and OUT-023 have each had their Statement extended twice (v01, v02). Another change to either would put it on this list, and any reversal of an R01-05, R01-11 or R02-01 element there would be oscillation.

## Trend
| Iteration | Remarks | Fixed / declined | Lines changed in the document (+/−) | Statements changed | Strength changes |
|---|---|---|---|---|---|
| 01 | 11 (3 link/citation, 1 contradiction, 2 strength-mismatch, 3 unsupported/overstated, 2 missing-requirement) | 11 / 0 | +61 / −21 | OUT-005, OUT-021, OUT-023, OUT-028, OUT-029; OUT-039 added | SHOULD clauses split out of 4 MUST requirements |
| 02 | 2 (1 missing-requirement, 1 factual error in the change log) | 2 / 0 | +24 / −11 | OUT-021, OUT-023 (one SHOULD element added to each) | none |
| 03 | 1 (link/citation: S-036 grading system) | 1 / 0 | +7 / −3 | none | none |
| 04 | 2 (link/citation: OUT-003 location; contradiction: OUT-027 source typing) | 2 / 0 | +9 / −4 | none | none |

The loop is converging:
- **Remarks per iteration:** 11 → 2 → 1 → 2.
- **Requirement statements and totals:** no statement has changed since v02. The totals (39 requirements: 10 MUST, 23 SHOULD, 5 MAY, 1 SHOULD NOT; 44 sources) have been the same since v01.
- **Iterations 03 and 04:** these touched only source metadata, one quote location and one evidence-basis label.
- **The rise from 1 to 2 remarks in iteration 04** does not mean the loop is regressing. Both remarks concern defects that have existed since v00 and that no earlier remark or fix had touched. Neither remark reverses an earlier change.
- **Reviews and fixes:** every review re-verified all quotes (173 → 199 → 203 → 204 strings) with no misquote found. No remark has been declined, so no declined remark has been re-raised.
