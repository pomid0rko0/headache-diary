# Fix — iteration 36
Version produced: v36
Reviewed version: v35
Date: 2026-10-22

Input: [`reviews/review-iter-36.md`](../reviews/review-iter-36.md) (verdict REMARKS, R36-01 to R36-03). Baseline of every comparison: the committed v35 (`git show HEAD:docs/stage2-output-model/OUTPUT_MODEL.md` and `…/RATIONALE.md`).

Files written:
- `OUTPUT_MODEL.md` (v36; header `Version: v36 · Iteration: 36 · Status: under review`; companion line `RATIONALE.md v36`; one change-log entry);
- `RATIONALE.md` (v36; header updated);
- `history/v36.md` and `history/v36-rationale.md`, byte-identical copies of the two files;
- this log.

Scripts (all run with `python3 -I`) and downloads are outside the repository, in `/tmp/claude-0/-home-user-headache-diary/e999335c-a019-5d6e-9071-b9ae8c72cf6c/scratchpad/fix36/`. `scripts/` holds the scripts and `dl/` the downloads, one fresh folder per source. Every edit was an exact string replacement that had to match exactly once (`apply36.py`; `retrace.py` for section 7).

## 1. Summary

| Remark | Verified | Disposition | Places changed: named by the review / found by the class sweep |
|---|---|---|---|
| R36-01 citation defect: Source lines that do not give a URL where the quoted text can be read | yes, by download and script | fixed | 16 entries / 2 entries (E-041/Q01; the [S-008] line of E-008/Q00), and the rule of the `Q` kind |
| R36-02 bookkeeping of kept invariants that lost conjuncts in v35 | yes, by script and by reading the 29 edited invariants | fixed | INV-031, INV-033, INV-075, INV-079, section 7 (4 rows), section 9 (INV-036), OC-08 / INV-078, INV-082, INV-085, INV-122, INV-123, section 7 row OUT-013, section 3.3 item 5 |
| R36-03 prose overclaim in sections 2.5 and 4.2 | yes | fixed | section 2.5, section 4.2 (E-014), section 6.0 / section 4.2 (second paragraph), section 4.1 (layer 3 and two lines of the relations sketch) |

No `omn` block changed: all 160 are byte-identical to v35. No case-table or source-data row changed. No quote, translation or location was altered: quotes were only moved between fields and entries (section 3), and every quoted string of v35 is still present (section 6). Section 5 lists every changed place.

## 2. R36-01 — quote entries whose Source line names a page where the quote cannot be read

### Verification

I downloaded each source with `curl`, into `dl/s010`, `dl/s015`, `dl/s106` and one folder for each other source. `qcheck.py` and `fullq.py` split every quoted string of a Q entry at `[...]`. They searched each fragment in the text behind each URL, first exactly (only white space, quote marks, dashes and ligatures normalised), then with line-end hyphens joined, then with letters and digits only.

- **[S-010].** The univaq full-text PDF (Stage 1: "full-text quotes") returned HTTP 200, 11 pp. The PubMed HTML page returned only a cookie wall (HTTP 203), so I read the abstract through E-utilities `efetch`.
  - All 18 quoted fragments of the 13 entries are on PDF p. 6. Three of them are found only after line-end hyphens are joined: E-018/Q02, E-046/Q02, E-046/Q05.
  - The abstract contains none of them. It has the four level names only in lower case, and not the section heading "Setting goals of migraine burden while on treatment".
- **[S-015].** "young people (aged 12 years and older) and adults" occurs on `https://www.nice.org.uk/guidance/cg150` (the Overview page) and not on the Recommendations page.
  - E-008/Q00, INV-001/Q00 and ISS-11/Q00 named only the Recommendations page.
  - E-041/Q01 named the Recommendations page in its Source line and the Overview page in its Location.
  - Every other [S-015] fragment (recommendations 1.3.9, 1.3.24, 1.3.26 to 1.3.29, 1.3.39, 1.3.48 and the section headings) is on the Recommendations page.
- **[S-106].** E-041/Q30 quotes paragraph 2.1, which is on the chapter 2 page that it names. E-041/Q29 quotes an [S-015] sentence, which is on the Recommendations page. Its [S-106] line names the guidance that the sentence refers to; the entry quotes no [S-106] text.

Disposition: **fixed**.

### What changed

All changes are in `RATIONALE.md`, except the E-008 Evidence field, which is in the model.

- **[S-010].** The Source line of the 13 entries now gives the Stage 1 full-text URL `https://ricerca.univaq.it/bitstream/11697/264025/1/sacco-et-al-2025-setting-higher-standards-for-migraine-prevention-a-position-statement-of-the-international-headache.pdf`. The entries are E-018/Q01 to Q03, E-046/Q01 to Q05, INV-031/Q00, INV-062/Q00, INV-064/Q00, ISS-05/Q00 and ISS-08/Q00. No entry quotes the abstract, so the PubMed URL stays nowhere.
- **[S-015].**
  - E-008/Q00 and INV-001/Q00: the [S-015] Source line now gives the Overview page. Their only [S-015] text is the population phrase.
  - ISS-11/Q00: a second [S-015] Source line gives the Overview page. The Recommendations line stays for recommendation 1.3.48.
  - E-041/Q01 (found by the sweep): the Source line now gives the Overview page. The Location already named it and is unchanged.
- **[S-008] in E-008/Q00** (found by the sweep). The entry quotes the IHS Q6 fragment "acceptable for treatment continuation beyond three months" but had no [S-008] Source line. It now has one, with the Stage 1 URL. The fragment stands on pp. 6 and 12 of that PDF (the Q6 statement is on p. 12). The model's E-008 Evidence field now lists [S-008] with the other sources of E-008/Q00.
  - The review listed this entry under "Checked and not raised", because the entry says "quoted in E-045".
  - It is the same class as the [S-015] phrase in the same entry, which the entry also marks "quoted in E-041" and which the review did raise. So both are treated alike.
- **The rule of the class**, `RATIONALE.md` section 1, kind `Q`. It now says that the Source lines give the URL at which the quoted text can be read. That URL is one of the source's URLs in model section 10 or Stage 1 section 5, or another page of the same publication on which the text stands, for example the CG150 Overview page. An entry has one Source line per page used.
  - Before, the rule said only "the URL where it can be read (model section 10, or Stage 1 section 5)".
  - The Overview page is not in Stage 1's [S-015] row, so without this change the corrected entries would break the file's own rule.

### Class and sweep

**Class.** A Q entry whose Source lines do not give a URL at which its quoted text can be read. This covers two cases:
- (1) a quoted fragment that can be read at no URL that the entry gives;
- (2) a Source line that names a page with none of the entry's text from that source, where the entry does quote that source.

**Sweep, part 1 (as asked): sources with more than one URL, and their Q entries.**
- *Stage 1 sources with more than one URL:* S-010, S-017, S-024, S-025, S-033, S-039, S-045, S-046 (script `srcurls.py` over Stage 1 section 5 and model section 10).
- *Sources added to the sweep:* S-015 (Overview and Recommendations pages) and S-106 (chapter 2 and overview), which the review names.
- *Q entries:*
  - S-010: 13 entries, all corrected.
  - S-015: 15 entries, 4 corrected.
  - S-033: 6 entries, all quoting the official PDF, as they should. The landing page is not used.
  - S-106: 2 entries, correct as described above.
  - S-017, S-024, S-025, S-039, S-045, S-046: no Q entry cites them.
  - In all, 32 entries were checked.

**Sweep, part 2: every Q entry.** I fetched all 28 sources that Source lines name. PMC articles were read in their Europe PMC `fullTextXML` form. `fullq.py` checked 303 fragments of the 113 Q entries against the URLs each entry gives.
- **v35:** 18 fragments could be read only at a URL that their entry did not give: 16 of R36-01 (13 in the [S-010] entries, among them the section heading in INV-064/Q00, ISS-05/Q00 and ISS-08/Q00, and 3 occurrences of the [S-015] population phrase), the [S-008] fragment of E-008/Q00, and the words "for example" in INV-062/Q00, which are Stage 1 wording.
- **v36:** 0.
- **The 67 fragments not found at a listed URL in v36:**
  - 55 are Stage 1 wording found in Stage 1;
  - 5 are English translations;
  - 1 is the S-034 title page, which is an image without a text layer (E-041/Q20 says so);
  - 6 are artefacts of the quote-mark parser.

**Case (2)** (`cond2.py`): 18 Source lines name a page with no quoted fragment of their entry. None of them is a defect:
- 14 are reference-only lines: the entry quotes nothing of that source and points to where it is quoted ("quoted in E-057", "[S-030]" inside Stage 1 wording, and so on). These lines are E-023/Q00 and INV-039/Q00 (S-030); E-041/Q29 (S-106); E-057/Q10 (S-101, S-103); INV-031/Q00 (S-010); INV-055/Q00 (S-034); INV-082/Q00 (S-101, S-102, S-103); INV-085/Q00 (S-104, S-105); INV-089/Q00 (S-001, S-007).
- 3 are the [S-022] sentence, whose PDF text layer has the margin line number "383" inside it (E-008/Q00, INV-070/Q00, INV-112/Q00).
- 1 is the S-034 image title page.

**URL membership** (`urlcheck.py`). All 155 Source lines name a URL of their source's row in Stage 1 section 5 or model section 10, or the CG150 Overview page.

**Reachability.** All 29 distinct Source URLs answered HTTP 200 or 206. `apicr.minzdrav.gov.ru …169_3` and `brainmed.com` reset the connection once and answered on the second attempt.

## 3. R36-02 — Conformance, Realises and Evidence of invariants that lost conjuncts in v35

### Verification

- `deflist.py` checks every definitional invariant against its Conformance field. For each element listed there, it looks for a name that the element declares, in the predicate or in a function the predicate uses. A kind of `DayMeasure` counts as a use of the type abbreviation that selects it (for example `moderateSevereHeadacheDays` of E-017).
  - Listed but unused in v35: INV-031 {E-017, E-021} and INV-033 {E-024, E-030, E-031}, exactly as the review says.
- `defx.py` cross-checks the element "Definitional:" lists against the invariant lists, and gives the same five pairs.
- I read the v34 and v35 predicates of all 29 edited invariants of `fixes/fix-iter-35.md` section 4, with their Conformance, Realises, Evidence and Q entries (table below).
- The review's other points hold:
  - section 7 rows OUT-006, OUT-011, OUT-027 and OUT-036 list INV-031 or INV-033 only because of the stale Realises fields;
  - the INV-036 row of section 9 omits E-034 `event`;
  - OC-08 lists OUT-013, which names auras, not attacks.

Disposition: **fixed**.

### The class and its rule

**Class.** A kept invariant whose conjuncts v35 moved out still carries, in a bookkeeping field, an element, requirement, citation or rule that only the moved conjuncts used. The bookkeeping fields are Conformance, Realises, Evidence (with the Q entry it points to) and the R-MCF pointer of its Notes. The moved content's Realises and Evidence live with the item that took it.

The model now states the rule for the Conformance field. Section 3.3 item 5 said that a definitional invariant is marked "definitional" "with the requirement whose element they define". Every definitional Conformance field names elements instead: `definitional (E-…)`, or, for INV-001, `Ctx`. Item 5 now reads "with the elements whose definition they are part of (for INV-001, the set `Ctx` that it characterises)".

For moved evidence text, `RATIONALE.md` section 1 ("Moved text") gains a fourth exception: evidence text of a kept invariant that supports only conjuncts that v35 moved to another item is moved, verbatim, to an entry of that item. Text that also supports a remaining conjunct stays.

### The 29 edited invariants

"—" means nothing in that field refers to a moved conjunct.

| INV | Moved in v35 → place | Conformance | Realises | Evidence and Q entry | Notes (R-MCF) | v36 |
|---|---|---|---|---|---|---|
| 012 | covered days ≤ length → INV-121 | — | — | — | — | none |
| 024 | four ≤ bounds → INV-122 | — | — (OUT-016 by the 8.2.6 sum bound) | — | — | none |
| 031 | two nesting bounds → INV-122; last conjunct removed (CHG-04) | E-017, E-021 unused | OUT-006 only by the moved bound | OUT-006 and the [S-002] symptom-free definition support only the moved bounds | — | fixed |
| 032 | level days ≤ length → INV-121 | — | — | — | — | none |
| 033 | pain time, symptom days, caregiver days → INV-121; functional impact → INV-122 | E-024, E-030, E-031 unused | OUT-011, OUT-027, OUT-036 only by moved bounds | generic | — | fixed |
| 035 | two placements → W2 (E-035) | — | — | — | — | none |
| 041 | series placement → W2 (E-038) | — | — | — | — | none |
| 050 | series placement → W2 (E-039); review window implied by E-039 `reviewWindow` | — | — | — | — | none |
| 056 | treatment and start facts → INV-123 (CHG-R1) | — | — | — | — | none |
| 059 | time-point placement → W2 (E-043) | — | — | — | (1) still applies | none |
| 060 | none (CHG-03 antecedent) | — | — | — | — | none |
| 062 | three placements → W2 (E-046) | — | — | — ([S-010] URL: R36-01) | (1), (4) still apply | none |
| 064 | reformulated with SD-CL | — | — | — ([S-010] URL: R36-01) | (2) still applies | none |
| 067 | treatment fact → INV-123 | — | — | — | (2) still applies | none |
| 068 | treatment fact → INV-123 | — | — | — | (1) still applies | none |
| 070 | presence ask → E-049 `onTreatmentPeriod` `when` | — | — | — | (2): its ask has no start condition | none |
| 072 | two placements → W2 (E-051) | — | — | formulation quote supports the kept `formulationScope` conjunct | — | none |
| 073 | reformulated with SD-ET | — | — | — | — | none |
| 075 | medication fact → INV-123 (`usedMedication`) | — | — | the OUT-023 formulation sentence supports only the moved tie | — | fixed |
| 078 | group placement → W2 (E-054) | — | — | the OUT-024 formulation sentence (cited since v15) supports no conjunct | (1) still applies | fixed (sweep) |
| 079 | role, start, stop, stop-reason, dose-change and formulation facts → INV-123 | — | — | OUT-023, "and the reason for stopping", the formulation sentence and [S-012] support only moved ties | (1) still applies | fixed |
| 082 | availability → INV-123 (`availableResult`) | — (E-057 value sets are used) | — | "Where results of validated instruments are available" supports only the moved conjunct | R-MCF (4) no longer applies | fixed (sweep) |
| 085 | availability → INV-123 (`availableScreening`) | — | — | the OUT-033 phrase also names the instruments whose ranges it bounds: stays | R-MCF (4) no longer applies | fixed (sweep) |
| 087 | attack placement → W2 (E-060) | — | — | — | — | none |
| 089 | bout–remission non-overlap → INV-124 | — | — | — | — | none |
| 092 | annotation → INV-120 (C3-12); placement → W2 (E-033) | — | — | — | — | none |
| 109 | three placements → W2 (E-055) | — | — | — | (2) still applies | none |
| 111 | none (CHG-06 adds a conjunct) | — | — | — | — | none |
| 112 | treatment and event facts → INV-123; event kinds → E-049 `event` type | — | — | the OUT-022 sentence and [S-011], [S-022] support the kept period bounds | (1), (2) still apply | none |

### What changed

**Model.**
- **INV-031.**
  - Conformance: `definitional (E-018, E-020, E-022)`.
  - Realises: `OUT-008, OUT-020`.
  - Evidence: `Stage 1 OUT-008, OUT-020, OUT-002; [S-010] INV-031/Q00`.
- **INV-033.** Conformance: `definitional (E-025)`; Realises: `OUT-012`.
  - The review allowed adding E-019 and OUT-007, which INV-033 only bounds against. I did not add them, because INV-033 is part of the definition of E-025, not of E-019.
  - For the same reason INV-031 does not gain E-015 and E-016. Its listed elements are those whose definition it is part of (section 3.3 item 5), as in v34.
- **INV-075 Evidence:** `Stage 1 OUT-012, OUT-023.`
- **INV-078 Evidence:** `Stage 1 OUT-024 ("a chronological list [...] grouped by drug class").` The formulation sentence, which no conjunct of INV-078 uses in v34 or v35, is dropped. Its wording stays in `RATIONALE.md` INV-123/Q01, inside the longer OUT-024 quote.
- **INV-079 Evidence:** `Stage 1 OUT-024; [S-013] INV-079/Q00.`
- **INV-082 and INV-085 Notes:** "R-MCF (4)." is removed. Neither predicate refers to available results any longer.
- **INV-122 Evidence:** gains `[S-002] INV-122/Q01`.
- **INV-123.** The Evidence gains `[S-012] INV-123/Q01`. The Notes gain "R-MCF (1), (4).", the rules that its start, stop and availability facts apply, as `RATIONALE.md` SEC-3.8/D01 lists them.
- **Catalogue OC-08 Realises:** `OUT-001, OUT-002, OUT-007`.
- **Section 9.**
  - The INV-036 row, column "Went into", reads "INV-123; E-034 `event` (attribute type)", as in the mapping of `fixes/fix-iter-35.md`.
  - The section's lead now says "the item or items named in the last column".
- **Section 7** was recomputed by `retrace.py` from the Realises fields:
  - OUT-006: INV-031 removed from the Invariants column;
  - OUT-011, OUT-027 and OUT-036: INV-033 removed;
  - OUT-013: OC-08 removed from the Catalogue rows column.

  No coverage line named INV-031 or INV-033 in these rows, so none changed.
- **Section 3.3 item 5** (the rule, above).

**`RATIONALE.md`.**
- **INV-031/Q00.** The [S-002] Source line is removed. The Text no longer has "(symptom-free days defined as "the days free of premonitory, aura, headache, and postdromal symptoms" [S-002])" and ", OUT-006".
- **INV-122/Q01 (new).** Concerns `INV-122; v34 INV-031`; Source [S-002]; `Text (v34 INV-031 Evidence)`: that fragment, verbatim.
- **INV-079/Q00.** The [S-012] Source line is removed. The Text keeps "start and stop dates, dose changes, treatment duration", which supports the kept date and duration conjuncts, and the [S-013] quote.
- **INV-082/Q00.** The Text no longer has "Where results of validated instruments are available".
- **INV-123/Q01 (new).** Concerns `INV-123; v34 INV-075; v34 INV-079; v34 INV-082`; Source [S-012]. It has three `Text (v34 … Evidence)` fields with the moved fragments, verbatim:
  - the OUT-023 formulation sentence of INV-075;
  - "and the reason for stopping", the OUT-024 formulation sentence and the [S-012] quote of INV-079;
  - the OUT-026 availability phrase of INV-082.
- **Section 1, "Moved text":** the fourth exception (above).

### Destinations of the moved content

Each moved conjunct lives with an item whose Realises names the requirement it served:
- INV-121: OUT-003, OUT-010, OUT-011, OUT-012, OUT-036;
- INV-122: OUT-006, OUT-008, OUT-014, OUT-016, OUT-027, OUT-036;
- INV-123: OUT-018, OUT-021, OUT-022, OUT-023, OUT-024, OUT-026, OUT-033, OUT-036, OUT-039;
- INV-124: OUT-031;
- INV-120 (C3-12) and E-033: OUT-037;
- W2 on E-035 (OUT-009), E-038 (OUT-028), E-039 (OUT-017), E-043 (OUT-018), E-046 (OUT-020), E-051 (OUT-023), E-054 (OUT-024), E-055 (OUT-024, OUT-039) and E-060 (OUT-030, OUT-035);
- E-049 `when` and `event` (OUT-022) and E-034 `event` (OUT-009).

`merged.py` also checks the 38 merged invariants of section 9: every v34 Realises requirement is in the Realises of the item or items they went into.

### Catalogue sweep

I checked all 118 (row, requirement) pairs of the Realises column against its definition: "the requirements whose statements name this kind of output; each is in the Realises field of an item named in the row".
- Every requirement is realised by an item named in its row.
- Only OC-08/OUT-013 fails the "names this kind" test.
- Borderline pairs kept, with their reason:
  - OC-12/OUT-013: OUT-013 names the duration of auras, a duration summary;
  - OC-17/OUT-014: the indicator shows the per-class day counts of OUT-014 as its basis;
  - OC-26/OUT-023: OUT-023 names the per-phase outputs "(see OUT-021)".

### Coverage

No requirement loses coverage:
- **OUT-006.** Per-period availability (INV-118, C1-03 SHOULD and C1-04 MUST), label (INV-008) and nesting (INV-122).
- **OUT-011.** C1-08 SHOULD, the bound of INV-121, C3-03 and C2-03.
- **OUT-013.** E-019 aura counts, E-024 and E-027 (MAY), rows OC-12 and OC-14.
- **OUT-027.** C1-12 SHOULD, INV-121, INV-122, and INV-027 SHOULD.
- **OUT-036 (a)–(d) and its Caveat.**
  - (a) and (b): E-030, E-031, E-058 and INV-096 SHOULD, with INV-121 and INV-122 for the bounds;
  - (c): INV-097;
  - (d): E-041 (SD-ER-15) and INV-055;
  - Caveat: C3-11.

Every level is unchanged: only the bookkeeping fields named above changed.

### Examined and not changed

- **Cross-links in the other direction.** These element–invariant pairs are uses through another element's function or type, not stale listings, and none is a listed element that the predicate does not use:
  - E-001/INV-123 (`factsShown`);
  - E-029/INV-045 (`basis`);
  - E-030/INV-121 (`daysWithin`);
  - E-040/INV-111 (`referencedValues`);
  - E-053/INV-074 (attack lines);
  - INV-123/E-014 (`DayCount`);
  - INV-082/E-057 (value sets).
- **D entries anchored at trimmed invariants.** INV-031/D01, INV-075/D01 and INV-085/D01 are rationale, not Evidence. The equivalence fix examined them and kept them at the anchors that the plan fixes (`fixes/fix-iter-35-equivalence.md`, section 5).
- **Evidence pointers.** E-041/Q29 and E-057/Q10 have more Source lines than the [S-NNN] pairs that cite them in the model. These lines are reference lines, as in v35, and not URL defects.

## 4. R36-03 — prose overclaim in the notation and the catalogue

### Verification

- **Section 2.5.** The sentence said that for references other than periods, the placement in the holder's view is a W2 marker. A script listed every predicate conjunct of the form `x ∈ v.content`, `x ∈ viewOf(…).content` or `v.content ∩ T = ran …`. Three conjuncts place a non-period reference that carries no marker:
  - INV-060: `ResidualBurden.migraineDays` and `moderateSevereHeadacheDays`, and, through `rb.change = ch`, its `change`;
  - INV-078: `ClassGroup.lines`;
  - INV-087: `MenstrualRelationView.cycles`.

  The other matches are not placements of a referenced atom: the periods of INV-003, quantifier ranges, and items asked for in a view.
- **Section 4.2.** E-014 declares `element DayCount extends PeriodValue { … }`, which is not `abstract`. The parser of element declarations finds 4 abstract types: `Element`, `Item`, `PeriodValue`, `ClusterPhaseItem`. The same sentence said that E-014 has no row and is not an output, but OC-05 names E-014 ("Headache days (E-015; E-014)"), and day counts are shown to the reader.

Disposition: **fixed**.

### What changed

- **Section 2.5, References.** "…; for the other references, a placement marker (rule W2) or one of the invariants INV-060, INV-078 and INV-087, which section 6.0 names with the references they place." The lead also changed from "an invariant states it" to "the model states it", because a marker is not an invariant.
- **Section 6.0, "Not marked".** Now also lists "`ResidualBurden.change`, `migraineDays` and `moderateSevereHeadacheDays` (INV-060 places, for the residual burden it asks for next to a percentage change, the burden and its two day counts in the view of the change)". It now names all three invariant placements.
- **Section 4.2, last paragraph.** "Elements without a row of their own: … and E-014 (`DayCount`, whose kinds E-015 to E-018, E-020, E-021, E-029 and E-030 have rows; nesting in INV-122)." `abstract` is deleted, and the lead no longer says that these elements are not outputs and have no row.

### Class and sweep

**Class.** Notation, overview or catalogue prose that asserts a formal property that the formal text does not give. Such properties are:
- the kind of a type (abstract, a `PeriodValue`);
- composition ("part of");
- which constructs place which references;
- what the catalogue cells contain.

**Swept.** Section 2 (2.1 to 2.11), section 3.3, section 4 (4.1 to 4.4 prose and the relations sketch), and the section 6.0 marker index. The sweep found four more cases and fixed them:
- **Section 4.1, layer 3.** E-028 (`enum AcuteDrugClass`) was listed among the per-period values ("E-014 to E-031"). The layer now reads "E-014 to E-027, E-029 to E-031, …, the acute drug classes by which acute-medication days are broken down (E-028, not a `PeriodValue`)". The parsed declarations confirm that every element in the new list is `PeriodValue`, one of its 12 subtypes or a kind of one of them; the remaining subtype, E-013, is in layer 2.
- **Section 4.1, relations sketch, `TreatmentHistoryView ⊃ ClassGroup`.**
  - The legend reads ⊂ as "part of". Section 2.5 makes only `Output.views` and `View.content` composition attributes, and the parser confirms that these are the only two.
  - The groups are referenced (`→ClassGroup`) and placed in the view only at SHOULD (W2).
  - The line now reads `TreatmentHistoryView → ClassGroup → …`.
- **Section 4.1, relations sketch, DefinitionLabel.** "names the definition of a measure shown in its view": no formal text requires the measure to be shown in the label's view. INV-008 asks for a label where the view reports the measure, which is the converse. The sketch now says "names the definition that its view follows for a measure", as E-011 defines.
- **Section 4.2, second paragraph.** The cells "restate no predicate", but by the column's own definition the Applicability cells give "the OMN predicate that states it" (for example `hasType(c, c1)`). The sentence now reads "… quote Stage 1 wording and repeat the OMN predicates of applicability conditions; they state no constraint of their own and have no formal force".

**Checked and true.**
- Section 2.5: only `Output.views` and `View.content` are composition attributes, and the W2 index of section 6.0 matches the 20 marked attributes.
- Section 2.4: the uses of `ℙ T` are parameters, the result types of defined functions, and the semantic constants.
- Section 2.7: every element with a `derived` attribute lists its relations under "Relations".
- Section 4.4: the prose on the C1–C3 functions.
- The other lines of the relations sketch match the declared references.

## 5. Every changed location

Line numbers are those of the v36 files.

| # | File | Line | Place | Remark | Change |
|---|---|---|---|---|---|
| 1 | model | 2 | header | — | v35 → v36, iteration 36 |
| 2 | model | 4 | header | — | companion `RATIONALE.md v36` |
| 3 | model | 67 | section 2.5, References | R36-03 | W2 or INV-060, INV-078, INV-087 (section 6.0) |
| 4 | model | 213 | section 3.3, item 5 | R36-02 (rule) | "with the elements whose definition they are part of …" |
| 5 | model | 281 | section 4.1, layer 3 | R36-03 (sweep) | E-028 not a per-period value |
| 6 | model | 295 | section 4.1, sketch | R36-03 (sweep) | `TreatmentHistoryView → ClassGroup` |
| 7 | model | 297 | section 4.1, sketch | R36-03 (sweep) | DefinitionLabel wording |
| 8 | model | 304 | section 4.2, second paragraph | R36-03 (sweep) | cells repeat applicability predicates |
| 9 | model | 318 | section 4.2, last paragraph | R36-03 | E-014 not `abstract`; "without a row of their own" |
| 10 | model | 333 | catalogue OC-08, Realises | R36-02 | OUT-013 removed |
| 11 | model | 710 | E-008 Evidence | R36-01 (sweep) | + [S-008] |
| 12 | model | 2071 | INV-122 Evidence | R36-02 | + `[S-002] INV-122/Q01` |
| 13 | model | 2082 | INV-123 Evidence | R36-02 | + `[S-012] INV-123/Q01` |
| 14 | model | 2083 | INV-123 Notes | R36-02 (sweep) | + "R-MCF (1), (4)." |
| 15 | model | 2129 | section 6.0, "Not marked" | R36-03 | + references of a residual burden (INV-060) |
| 16 | model | 2329–2331 | INV-031 Conformance, Realises, Evidence | R36-02 | as section 3 |
| 17 | model | 2357–2358 | INV-033 Conformance, Realises | R36-02 | as section 3 |
| 18 | model | 2970 | INV-075 Evidence | R36-02 | formulation quote moved to INV-123/Q01 |
| 19 | model | 3012 | INV-078 Evidence | R36-02 (sweep) | formulation sentence dropped |
| 20 | model | 3031 | INV-079 Evidence | R36-02 | `Stage 1 OUT-024; [S-013] INV-079/Q00` |
| 21 | model | 3099 | INV-082 Notes | R36-02 (sweep) | "R-MCF (4)." removed |
| 22 | model | 3127 | INV-085 Notes | R36-02 (sweep) | "R-MCF (4)." removed |
| 23 | model | 3438, 3443, 3445, 3460, 3469 | section 7, rows OUT-006, OUT-011, OUT-013, OUT-027, OUT-036 | R36-02 | recomputed columns |
| 24 | model | 3559 | section 9, lead | R36-02 (consequential) | "the item or items named" |
| 25 | model | 3584 | section 9, row INV-036 | R36-02 | + E-034 `event` (attribute type) |
| 26 | model | 3846 | section 12 | — | v36 entry |
| 27 | RATIONALE | 2 | header | — | v36 |
| 28 | RATIONALE | 14 | section 1, kind `Q` | R36-01 (rule) | URL at which the quoted text can be read; one Source line per page |
| 29 | RATIONALE | 21 | section 1, Moved text | R36-02 (rule) | fourth exception |
| 30 | RATIONALE | 269, 272 | E-008/Q00 | R36-01 | + [S-008] line (sweep); [S-015] → Overview page |
| 31 | RATIONALE | 363, 370, 377 | E-018/Q01–Q03 | R36-01 | [S-010] → full-text PDF |
| 32 | RATIONALE | 601 | E-041/Q01 | R36-01 (sweep) | [S-015] → Overview page |
| 33 | RATIONALE | 985, 992, 999, 1006, 1013 | E-046/Q01–Q05 | R36-01 | [S-010] → full-text PDF |
| 34 | RATIONALE | 1411–1415 | INV-122/Q01 | R36-02 | new entry |
| 35 | RATIONALE | 1427–1433 | INV-123/Q01 | R36-02 | new entry |
| 36 | RATIONALE | 1504 | INV-001/Q00 | R36-01 | [S-015] → Overview page |
| 37 | RATIONALE | 1600–1601 | INV-031/Q00 | R36-01, R36-02 | [S-010] → full-text PDF; [S-002] line and fragment moved to INV-122/Q01 |
| 38 | RATIONALE | 1746 | INV-062/Q00 | R36-01 | [S-010] → full-text PDF |
| 39 | RATIONALE | 1816 | INV-064/Q00 | R36-01 | [S-010] → full-text PDF |
| 40 | RATIONALE | 1946–1947 | INV-079/Q00 | R36-02 | [S-012] line and moved fragments → INV-123/Q01 |
| 41 | RATIONALE | 1996 | INV-082/Q00 | R36-02 (sweep) | availability phrase → INV-123/Q01 |
| 42 | RATIONALE | 2201, 2214 | ISS-05/Q00, ISS-08/Q00 | R36-01 | [S-010] → full-text PDF |
| 43 | RATIONALE | 2233 | ISS-11/Q00 | R36-01 | + [S-015] Overview line |

## 6. Checks

All checks were run on the files as written (`checks36.py`, `trace.py`, `deflist.py`, `defx.py`, `urlcheck.py`, `fullq.py`, `cond2.py`).

| Check | Result |
|---|---|
| Formal identity against HEAD | 160 `omn` blocks in HEAD and v36, 0 differing. The only fenced block that changed is the plain (non-`omn`) relations sketch of section 4.1 |
| Brace balance | 160 `omn` blocks: 0 unbalanced in `{}`, `()`, `[]`, `⟨⟩`. Backticked table cells: 697 (696 + the new `event` cell), 0 unbalanced |
| IDs, model → items | headings E 67, INV 87, ISS 12, no duplicates; 192 E/INV/ISS IDs referenced, 0 unresolved |
| IDs, RATIONALE → items | 180 referenced, 0 unresolved |
| Row IDs | 174 rows (OC, C1–C3, SD), 0 unresolved in either file |
| Entries | 434 entries (432 + INV-122/Q01, INV-123/Q01), 113 Q, no duplicates. 364 entry IDs referenced from the model and 399 from `RATIONALE.md`, 0 unresolved. Every entry except the case-row, section and search-log entries is referenced from the model |
| Evidence pointers | every `[S-NNN] <entry>` pair names an entry whose Source lines include S-NNN (0 mismatches) |
| Traceability | section 7 recomputed from the Realises fields: 0 differences in the Catalogue rows, Elements and Invariants columns of all 39 rows |
| Catalogue | every requirement in a row's Realises is realised by an item named in the row; every requirement is in some row |
| Coverage lines | every item named is in its row's columns, except INV-104 (OUT-008) and INV-069 (OUT-012), as in v35 (review 36, "Checked and not raised") |
| Definitional lists | 0 listed elements unused (v35: 5) |
| Quotes | 707 distinct double-quoted strings of the HEAD model and `RATIONALE.md`: all present in v36; no new quoted string |
| URLs | 155 Source lines, all a URL of their source (or the CG150 Overview page); 29 distinct URLs, all HTTP 200/206; quoted fragments readable only at another URL: 18 in v35 → 0 |
| Scope | counts of JSON, FHIR, database, recorded, entered, captured, storage, stored, XML, CSV, algorithm in model + `RATIONALE.md`: unchanged from v35. No input, storage or derivation-from-input text added |
| Satisfiability | not needed: no formal block changed |
| Header | `Version: v36 · Iteration: 36 · Status: under review` |
| Snapshots | `cmp OUTPUT_MODEL.md history/v36.md` and `cmp RATIONALE.md history/v36-rationale.md`: identical |

File sizes:

| File | v35 (bytes) | v36 (bytes) |
|---|---|---|
| `OUTPUT_MODEL.md` and `history/v36.md` | 421,294 | 421,917 |
| `RATIONALE.md` and `history/v36-rationale.md` | 319,452 | 322,333 |

## 7. Diff summary of the formal blocks

- **Changed:** none. All 160 `omn` blocks are byte-identical to v35, including every block that the watch points of the oscillation checks after iterations 12 to 32 name.
- **Tables:** every case-table and source-data row is unchanged. Two informative cells changed: OC-08 Realises and the section 9 row of INV-036. Five traceability rows changed in their computed columns.
- **No change of meaning.** Every edit is in Conformance, Realises, Evidence or Notes fields, in prose, in the traceability and withdrawn-item tables, or in `RATIONALE.md`.

**Watch points.** No watch-point decision is reversed.
- The ties of the "truth of a shown fact" class stay in INV-123 at definitional level. Only their evidence and R-MCF pointer now sit there as well (check 32, watch point 1).
- No tie returns to INV-082 or INV-085, and no class is widened.
- The cluster view keeps no placement (E-062/X01; CA-09).
- ISS-03 and the other text-only items are untouched.
